Autonity API
------------

So you have nice and running 5 node cluster. Let's examine it and try
*Soma* and *Glienicke* features. First of all we need to connect to one
of the nodes: ``autonity attach http://0.0.0.0:8541``

In the Genesis file ``genesis-ibft.json`` we've defined the while list
of nodes that have permission to connect to the network:

.. code:: bash

        [
            "enode://438a5c2cd8fdc2ecbc508bf7362e41c0f0c3754ba1d3267127a3756324caf45e6546b02140e2144b205aeb372c96c5df9641485f721dc7c5b27eb9e35f5d887b@172.25.0.14:30303",
            "enode://d73b857969c86415c0c000371bcebd9ed3cca6c376032b3f65e58e9e2b79276fbc6f59eb1e22fcd6356ab95f42a666f70afd4985933bd8f3e05beb1a2bf8fdde@172.25.0.11:30303",
            "enode://3ce6c053cb563bfd94f4e0e248510a07ccee1bc836c9784da1816dba4b10564e7be1ba42e0bd8d73c8f6274f8e9878dc13814adb381c823264265c06048b4b59@172.25.0.15:30303"
            "enode://1f207dfb3bcbbd338fbc991ec13e40d204b58fe7275cea48cfeb53c2c24e1071e1b4ef2959325fe48a5893de8ff37c73a24a412f367e505e5dec832813da546a@172.25.0.12:30303",
            "enode://e766ac390e2d99b559aef773c3656fa8d50df2310496ac26ca6c3fc84e21dabb8a0162cc8e34f938d45e0a8ed04955f8ddf1c380182f8ef17a3f08885064505f@172.25.0.13:30303",
        ]

We have 5 validators so we expect to see 4 connected peers of each node:

.. code:: bash

    net.peerCount
        4

Let's check what are this peers:

.. code:: bash

    admin.peers.map(function(peer) {return peer.enode;});
        [  
           "enode://438a5c2cd8fdc2ecbc508bf7362e41c0f0c3754ba1d3267127a3756324caf45e6546b02140e2144b205aeb372c96c5df9641485f721dc7c5b27eb9e35f5d887b@172.25.0.14:59360",
           "enode://d73b857969c86415c0c000371bcebd9ed3cca6c376032b3f65e58e9e2b79276fbc6f59eb1e22fcd6356ab95f42a666f70afd4985933bd8f3e05beb1a2bf8fdde@172.25.0.11:30303",
           "enode://3ce6c053cb563bfd94f4e0e248510a07ccee1bc836c9784da1816dba4b10564e7be1ba42e0bd8d73c8f6274f8e9878dc13814adb381c823264265c06048b4b59@172.25.0.15:30303",
           "enode://1f207dfb3bcbbd338fbc991ec13e40d204b58fe7275cea48cfeb53c2c24e1071e1b4ef2959325fe48a5893de8ff37c73a24a412f367e505e5dec832813da546a@172.25.0.12:30303"
        ]

Validators
~~~~~~~~~~

We can get the list of actual validator for any block:

.. code:: bash

    // for 10th block
    istanbul.getValidators(web3.toHex(10))

    // for current block
    istanbul.getValidators(web3.toHex(eth.blockNumber))

        [
           "0x4ad219b58a5b46a1d9662beaa6a70db9f570dea5",
           "0x4b07239bd581d21aefcdee0c6db38070f9a5fd2d",
           "0x850c1eb8d190e05845ad7f84ac95a318c8aab07f",
           "0xc443c6c6ae98f5110702921138d840e77da67702"
        ]

If you want you can get the same information by hash:

.. code:: bash

    //for current block
    istanbul.getValidatorsAtHash(eth.getBlock(eth.blockNumber).hash)

Adding and removing from validators
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

First of all we need to get *Soma* contract ABI and address:

.. code:: bash

    var somaContractAbi = eth.contract(JSON.parse(istanbul.getSomaContractABI()));
    var somaContract = somaContractAbi.at(istanbul.getSomaContractAddress());

    // check somaContract
    somaContract

        ...
        AddValidator: function(),
        RemoveValidator: function(),
        allEvents: function(),
        getValidators: function(),
        validators: function()
        ...
        

Now it's possible to use ``somaContract`` object to call *Soma*.

Add a validator
'''''''''''''''

::

    // getValidators
    somaContract.getValidators();

        [
           "0x4ad219b58a5b46a1d9662beaa6a70db9f570dea5",
           "0x4b07239bd581d21aefcdee0c6db38070f9a5fd2d",
           "0x850c1eb8d190e05845ad7f84ac95a318c8aab07f",
           "0xc443c6c6ae98f5110702921138d840e77da67702"
        ]

    // AddValidator
    web3.personal.unlockAccount(eth.accounts[0], 'test');
    somaContract.AddValidator("0x000000000000000000000000000000", {from: eth.accounts[0]});

    somaContract.getValidators()
        [
           "0x4ad219b58a5b46a1d9662beaa6a70db9f570dea5",
           "0x4b07239bd581d21aefcdee0c6db38070f9a5fd2d",
           "0x850c1eb8d190e05845ad7f84ac95a318c8aab07f",
           "0xc443c6c6ae98f5110702921138d840e77da67702",
           "0x0000000000000000000000000000000000000000"
        ]

A new validator ``0x0000000000000000000000000000000000000000`` has been
added.

If you try to add an incorrect node ID, you get an error:

.. code:: bash

    somaContract.AddValidator("incorrect_ID", {from: eth.accounts[0]});

        Error: new BigNumber() not a number: incorrect_ID

Remove a validator
''''''''''''''''''

.. code:: bash

    somaContract.RemoveValidator("0x0000000000000000000000000000000000000000", {from: eth.accounts[0]});

    somaContract.getValidators()

        [
           "0x4ad219b58a5b46a1d9662beaa6a70db9f570dea5",
           "0x4b07239bd581d21aefcdee0c6db38070f9a5fd2d",
           "0x850c1eb8d190e05845ad7f84ac95a318c8aab07f",
           "0xc443c6c6ae98f5110702921138d840e77da67702"
        ]

Permissioned network
~~~~~~~~~~~~~~~~~~~~

As it was done for *Soma* we need to get *Glienicke* contract:

::

    var glienickeContractAbi = eth.contract(JSON.parse(istanbul.getGlienickeContractABI()));
    var glienickeContract = glienickeContractAbi.at(istanbul.getGlienickeContractAddress());

    glienickeContract;

        ...
        transactionHash: null,
        AddEnode: function(),
        RemoveEnode: function(),
        allEvents: function(),
        compareStringsbyBytes: function(),
        enodes: function(),
        getWhitelist: function()
        ...

Remove and add a user to the white list
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The current white list can be gotten:

::

    istanbul.getWhitelist();

        [
           "enode://d73b857969c86415c0c000371bcebd9ed3cca6c376032b3f65e58e9e2b79276fbc6f59eb1e22fcd6356ab95f42a666f70afd4985933bd8f3e05beb1a2bf8fdde@172.25.0.11:30303",
           "enode://1f207dfb3bcbbd338fbc991ec13e40d204b58fe7275cea48cfeb53c2c24e1071e1b4ef2959325fe48a5893de8ff37c73a24a412f367e505e5dec832813da546a@172.25.0.12:30303",
           "enode://e766ac390e2d99b559aef773c3656fa8d50df2310496ac26ca6c3fc84e21dabb8a0162cc8e34f938d45e0a8ed04955f8ddf1c380182f8ef17a3f08885064505f@172.25.0.13:30303",
           "enode://438a5c2cd8fdc2ecbc508bf7362e41c0f0c3754ba1d3267127a3756324caf45e6546b02140e2144b205aeb372c96c5df9641485f721dc7c5b27eb9e35f5d887b@172.25.0.14:30303",
           "enode://3ce6c053cb563bfd94f4e0e248510a07ccee1bc836c9784da1816dba4b10564e7be1ba42e0bd8d73c8f6274f8e9878dc13814adb381c823264265c06048b4b59@172.25.0.15:30303"
        ]

Lets remove one peer from white list and check that the node will be
dropped. At the moment we have 4 connections on each node:

::

    // current network connections
    net.peerCount;

        4

    // list of connected peers
    admin.peers.map(function(peer) {return peer.enode;});

        [
           "enode://438a5c2cd8fdc2ecbc508bf7362e41c0f0c3754ba1d3267127a3756324caf45e6546b02140e2144b205aeb372c96c5df9641485f721dc7c5b27eb9e35f5d887b@172.25.0.14:57262",
           "enode://d73b857969c86415c0c000371bcebd9ed3cca6c376032b3f65e58e9e2b79276fbc6f59eb1e22fcd6356ab95f42a666f70afd4985933bd8f3e05beb1a2bf8fdde@172.25.0.11:30303",
           "enode://3ce6c053cb563bfd94f4e0e248510a07ccee1bc836c9784da1816dba4b10564e7be1ba42e0bd8d73c8f6274f8e9878dc13814adb381c823264265c06048b4b59@172.25.0.15:60654",
           "enode://1f207dfb3bcbbd338fbc991ec13e40d204b58fe7275cea48cfeb53c2c24e1071e1b4ef2959325fe48a5893de8ff37c73a24a412f367e505e5dec832813da546a@172.25.0.12:30303"
        ]

    // current white list
    istanbul.getWhitelist();

        [
           "enode://d73b857969c86415c0c000371bcebd9ed3cca6c376032b3f65e58e9e2b79276fbc6f59eb1e22fcd6356ab95f42a666f70afd4985933bd8f3e05beb1a2bf8fdde@172.25.0.11:30303",
           "enode://1f207dfb3bcbbd338fbc991ec13e40d204b58fe7275cea48cfeb53c2c24e1071e1b4ef2959325fe48a5893de8ff37c73a24a412f367e505e5dec832813da546a@172.25.0.12:30303",
           "enode://e766ac390e2d99b559aef773c3656fa8d50df2310496ac26ca6c3fc84e21dabb8a0162cc8e34f938d45e0a8ed04955f8ddf1c380182f8ef17a3f08885064505f@172.25.0.13:30303",
           "enode://438a5c2cd8fdc2ecbc508bf7362e41c0f0c3754ba1d3267127a3756324caf45e6546b02140e2144b205aeb372c96c5df9641485f721dc7c5b27eb9e35f5d887b@172.25.0.14:30303",
           "enode://3ce6c053cb563bfd94f4e0e248510a07ccee1bc836c9784da1816dba4b10564e7be1ba42e0bd8d73c8f6274f8e9878dc13814adb381c823264265c06048b4b59@172.25.0.15:30303"
        ]
        

To remove a peer from white list we should use ``glienickeContract``:

::

    glienickeContract.RemoveEnode("enode://1f207dfb3bcbbd338fbc991ec13e40d204b58fe7275cea48cfeb53c2c24e1071e1b4ef2959325fe48a5893de8ff37c73a24a412f367e505e5dec832813da546a@172.25.0.12:30303", {from: eth.accounts[0], gas: 100000000});

    net.peerCount;

        3

    admin.peers.map(function(peer) {return peer.enode;});

        [
           "enode://e766ac390e2d99b559aef773c3656fa8d50df2310496ac26ca6c3fc84e21dabb8a0162cc8e34f938d45e0a8ed04955f8ddf1c380182f8ef17a3f08885064505f@172.25.0.13:30303",
           "enode://438a5c2cd8fdc2ecbc508bf7362e41c0f0c3754ba1d3267127a3756324caf45e6546b02140e2144b205aeb372c96c5df9641485f721dc7c5b27eb9e35f5d887b@172.25.0.14:40640",
           "enode://3ce6c053cb563bfd94f4e0e248510a07ccee1bc836c9784da1816dba4b10564e7be1ba42e0bd8d73c8f6274f8e9878dc13814adb381c823264265c06048b4b59@172.25.0.15:53914"
        ]

    istanbul.getWhitelist();

        [
           "enode://d73b857969c86415c0c000371bcebd9ed3cca6c376032b3f65e58e9e2b79276fbc6f59eb1e22fcd6356ab95f42a666f70afd4985933bd8f3e05beb1a2bf8fdde@172.25.0.11:30303",
           "enode://e766ac390e2d99b559aef773c3656fa8d50df2310496ac26ca6c3fc84e21dabb8a0162cc8e34f938d45e0a8ed04955f8ddf1c380182f8ef17a3f08885064505f@172.25.0.13:30303",
           "enode://438a5c2cd8fdc2ecbc508bf7362e41c0f0c3754ba1d3267127a3756324caf45e6546b02140e2144b205aeb372c96c5df9641485f721dc7c5b27eb9e35f5d887b@172.25.0.14:30303",
           "enode://3ce6c053cb563bfd94f4e0e248510a07ccee1bc836c9784da1816dba4b10564e7be1ba42e0bd8d73c8f6274f8e9878dc13814adb381c823264265c06048b4b59@172.25.0.15:30303"
        ]

The connection with the removed peer won't be established until the peer
will be added to white list again. If this happened, the connection will
be established in few seconds:

::

    glienickeContract.AddEnode("enode://1f207dfb3bcbbd338fbc991ec13e40d204b58fe7275cea48cfeb53c2c24e1071e1b4ef2959325fe48a5893de8ff37c73a24a412f367e505e5dec832813da546a@172.25.0.12:30303", {from: eth.accounts[0], gas: 100000000});

    net.peerCount;

        4

    admin.peers.map(function(peer) {return peer.enode;});

        [
           "enode://e766ac390e2d99b559aef773c3656fa8d50df2310496ac26ca6c3fc84e21dabb8a0162cc8e34f938d45e0a8ed04955f8ddf1c380182f8ef17a3f08885064505f@172.25.0.13:30303",
           "enode://438a5c2cd8fdc2ecbc508bf7362e41c0f0c3754ba1d3267127a3756324caf45e6546b02140e2144b205aeb372c96c5df9641485f721dc7c5b27eb9e35f5d887b@172.25.0.14:40640",
           "enode://3ce6c053cb563bfd94f4e0e248510a07ccee1bc836c9784da1816dba4b10564e7be1ba42e0bd8d73c8f6274f8e9878dc13814adb381c823264265c06048b4b59@172.25.0.15:53914",
           "enode://1f207dfb3bcbbd338fbc991ec13e40d204b58fe7275cea48cfeb53c2c24e1071e1b4ef2959325fe48a5893de8ff37c73a24a412f367e505e5dec832813da546a@172.25.0.12:33168"
        ]


    istanbul.getWhitelist();

        [
           "enode://d73b857969c86415c0c000371bcebd9ed3cca6c376032b3f65e58e9e2b79276fbc6f59eb1e22fcd6356ab95f42a666f70afd4985933bd8f3e05beb1a2bf8fdde@172.25.0.11:30303",
           "enode://e766ac390e2d99b559aef773c3656fa8d50df2310496ac26ca6c3fc84e21dabb8a0162cc8e34f938d45e0a8ed04955f8ddf1c380182f8ef17a3f08885064505f@172.25.0.13:30303",
           "enode://438a5c2cd8fdc2ecbc508bf7362e41c0f0c3754ba1d3267127a3756324caf45e6546b02140e2144b205aeb372c96c5df9641485f721dc7c5b27eb9e35f5d887b@172.25.0.14:30303",
           "enode://3ce6c053cb563bfd94f4e0e248510a07ccee1bc836c9784da1816dba4b10564e7be1ba42e0bd8d73c8f6274f8e9878dc13814adb381c823264265c06048b4b59@172.25.0.15:30303",
           "enode://1f207dfb3bcbbd338fbc991ec13e40d204b58fe7275cea48cfeb53c2c24e1071e1b4ef2959325fe48a5893de8ff37c73a24a412f367e505e5dec832813da546a@172.25.0.12:30303"
        ]

Error handling
^^^^^^^^^^^^^^

If we try to add an incorrect enode:

.. code:: bash

    glienickeContract.AddEnode("incorrect_Enode", {from: eth.accounts[0]});

The error should be logged in cluster. To get logs run the command
``docker-compose logs | grep "ERROR"``:

::

    ERROR[04-11|08:48:09.034] Invalid whitelisted enode                returned enode=incorrect_Enode error="invalid URL scheme, want \"enode\""
