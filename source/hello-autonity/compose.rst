How to run the network with docker-compose
==========================================

.. NOTE:: tl;dr; 
  
  Run

    .. code:: bash

        git clone https://github.com/clearmatics/autonity.git
        cd autonity/helloworld/
        docker-compose up -d

    and off you go!


Install Docker
--------------

Install Docker and Docker-Compose. 
The versions we used in development were:
 
.. code:: bash
    $ docker --version
    Docker version 19.03.4, build 9013bf5
    $ docker-compose --version
    docker-compose version 1.24.1, build 4667896b
    $ docker-machine --version
    docker-machine version 0.16.2, build bd45ab13



Clone the GitHUb repository
--------------------

Run

.. code:: bash

    git clone https://github.com/clearmatics/autonity.git

.. code:: bash

    cd autonity/helloworld/


Deploy the network
------------------

To deploy the network run:

.. code:: bash

    $ docker-compose up -d

and off you go!

.. NOTE:: What is docker-compose?
  A simple script to start an Autonity network with IBFT



What should it look like when it is running?
--------------------------------------------

When you start the ``docker-compose up -d`` it should print out
this information:

.. code:: bash

    $ docker-compose up -d
    WARNING: The Docker Engine you're using is running in swarm mode.

    Compose does not use swarm mode to deploy services to multiple nodes in a swarm. All containers will be scheduled on the current node.

    To deploy your application across the swarm, use `docker stack deploy`.

    Creating network "helloworld_chainnet" with driver "bridge"
    Creating autonity-node-2 ... done
    Creating autonity-node-1 ... done
    Creating autonity-node-5 ... done
    Creating autonity-node-3 ... done
    Creating autonity-node-4 ... done
    Creating nodes-connector ... done

When the nodes have all been deployed and connected to each other, the
``nodes-connector`` should have exited. You can check this by doing the
``docker-compose ps`` command:

.. code:: bash

    $ docker-compose ps
         Name                Command          State                                      Ports
         -----------------------------------------------------------------------------------------------------------------------------
         autonity-node-1   ./autonity-start.sh     Up       0.0.0.0:30313->30303/tcp, 0.0.0.0:30313->30303/udp, 0.0.0.0:8541->8545/tcp
         autonity-node-2   ./autonity-start.sh     Up       0.0.0.0:30323->30303/tcp, 0.0.0.0:30323->30303/udp, 0.0.0.0:8542->8545/tcp
         autonity-node-3   ./autonity-start.sh     Up       0.0.0.0:30333->30303/tcp, 0.0.0.0:30333->30303/udp, 0.0.0.0:8543->8545/tcp
         autonity-node-4   ./autonity-start.sh     Up       0.0.0.0:30343->30303/tcp, 0.0.0.0:30343->30303/udp, 0.0.0.0:8544->8545/tcp
         autonity-node-5   ./autonity-start.sh     Up       0.0.0.0:30353->30303/tcp, 0.0.0.0:30353->30303/udp, 0.0.0.0:8545->8545/tcp
         nodes-connector   ./autonity-connect.sh   Exit 0

How can I use the nodes?
------------------------

You can connect to the nodes through the autonity console. All the RPC
ports are open. Here is an example of attaching a console to
``autonity-node-1``:

.. code:: bash

    $ autonity attach http://0.0.0.0:8541
    Welcome to the Autonity JavaScript console!

    instance: Autonity/v1.0.0-alpha-7bcaa485/linux-amd64/go1.11.5
    coinbase: 0x850c1eb8d190e05845ad7f84ac95a318c8aab07f
    at block: 298 (Wed, 13 Feb 2019 15:31:50 GMT)
    datadir: /autonity-data
    modules: admin:1.0 istanbul:1.0 debug:1.0 eth:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 txpool:1.0 web3:1.0

    >

You can also run a simple Javascript command without having an
interactive console:

.. code:: bash

    $ autonity attach http://0.0.0.0:8541 --exec '[eth.coinbase, eth.getBlock("latest").number, eth.getBlock("latest").hash, eth.mining]'
    ["0x850c1eb8d190e05845ad7f84ac95a318c8aab07f", 298, "0xba609a7786a70a0c1be27c3f3325279512c004ba48c3a82e945cc3f45f1d045d", true]

What are all these files in the ``helloword`` directory?
--------------------------------------------------------

The files in the ``helloworld`` directory are used to deploy and run the
network. You can alter them and redeploy to see how the changes affected
the network. Here is the file list:

.. code:: bash

    $ ls -lh
    total 60K
    -rwxr-xr-x 1 clearmatics clearmatics 2.2K Feb 13 15:12 autonity-connect.sh
    -rwxr-xr-x 1 clearmatics clearmatics  577 Feb 13 15:13 autonity-start.sh
    -rw-r--r-- 1 clearmatics clearmatics 3.1K Feb 13 00:15 docker-compose.yml
    -rw-r--r-- 1 clearmatics clearmatics  410 Feb 12 16:35 Dockerfile
    -rw-r--r-- 1 clearmatics clearmatics 1.4K Feb 13 13:41 genesis-clique.json
    -rw-r--r-- 1 clearmatics clearmatics 2.6K Feb 12 12:15 genesis-ibft.json
    drwx------ 2 clearmatics clearmatics 4.0K Feb 12 14:19 keystore
    -rw-r--r-- 1 clearmatics clearmatics   65 Feb 12 23:40 nodekey1
    -rw-r--r-- 1 clearmatics clearmatics   65 Feb 12 23:40 nodekey2
    -rw-r--r-- 1 clearmatics clearmatics   65 Feb 12 23:40 nodekey3
    -rw-r--r-- 1 clearmatics clearmatics   65 Feb 12 23:41 nodekey4
    -rw-r--r-- 1 clearmatics clearmatics   65 Feb 12 23:41 nodekey5
    -rw-r--r-- 1 clearmatics clearmatics 3.3K Feb 13 15:35 README.md

-  ``Dockerfile`` is used by Docker to build the image that will be
   reused everytime you deploy a container
-  ``docker-compose.yml`` is used by Docker-Compose and it describes how
   the nodes should be deployed (what are the container names, what
   images should be used, what is the order of deployment)
-  ``autonity-start.sh`` script to start an autonity node, used evertime
   a container is deployed
-  ``autonity-connect.sh`` script run everytime the
   ``autonity-connector`` container is started (it connects 5 nodes to
   each other, sets the coinbase value, and starts the miner)
-  ``keystore`` directory with all the keystores (keystores are used to
   keep the private keys of the accounts, our keystores all use the
   password ``test``)
-  ``nodekey1`` file containing Node Key used to generate ENode (this
   way the enodes never change, although it is not relevant for the
   Clique Hello World, it will be used in the future for the IBFT Hello
   World)

How can the validator set be changed?
--------------------------------------

There are three steps to update the validator set:

1. Update the Soma and Glienicke smart contracts
2. Update the ``nodekey`` files
3. Change the ``genesis-ibft.json``

Update Glienicke and Soma contracts
-----------------------------------

The *Glienicke* contract is responsible for making sure that only nodes
in its list are able to connect to the Autonity client.

In the default Docker Compose deployment, the contract can be found at
the ``0x522B3294E6d06aA25Ad0f1B8891242E335D3B459`` address. You can find
the contract deployed in the Autonity code in the
```contracts`` <https://github.com/clearmatics/autonity/tree/master/contracts/Glienicke>`__
directory.

The *Soma* contract allows anyone to vote on the IBFT set of validators.

In the default Docker Compose deployment, the contract can be found at
the ``0xc3d854209eF19803954916F2fe4712448094363e`` address. You can find
the contract deployed in the Autonity code in the
```contracts`` <https://github.com/clearmatics/autonity/tree/master/contracts/Soma>`__
directory.

Change the ``genesis-ibft.json`` and update the ``nodekey`` files
------------------------------------------------------------------

*The Autonity Hello World instance limits the number of validators to 4, but in a
real world application you can have more validators.*

It is possible update the set of validators by updating the genesis file
and the nodekey files. The steps are:

-  Update the ``nodekey1`` file (or 2,3,4) with the private key of the
   validator
-  Update the ``enodeWhitelist`` property in the genesis file. Enode
   address can be a few formats:

   -  Ethereum enodeV4

   ::

           enode://d73b857969c86415c0c000371bcebd9ed3cca6c376032b3f65e58e9e2b79276fbc6f59eb1e22fcd6356ab95f42a666f70afd4985933bd8f3e05beb1a2bf8fdde@172.25.0.11:30303

   -  with domain instead of IP

   ::

       enode://d73b857969c86415c0c000371bcebd9ed3cca6c376032b3f65e58e9e2b79276fbc6f59eb1e22fcd6356ab95f42a666f70afd4985933bd8f3e05beb1a2bf8fdde@domain.com:30303

   -  any of the above without port

      ::

          enode://d73b857969c86415c0c000371bcebd9ed3cca6c376032b3f65e58e9e2b79276fbc6f59eb1e22fcd6356ab95f42a666f70afd4985933bd8f3e05beb1a2bf8fdde@domain.com

   -  by default, if it's not specified port ``30303`` will be used.

-  Update the ``validators`` property in the genesis file by with a
   proper node ID, eg:

::

    "validators": [
        "0x850C1Eb8D190e05845ad7F84ac95a318C8AaB07f",
        "0x4AD219b58a5b46A1D9662BeAa6a70DB9F570deA5",
        "0x4B07239Bd581d21AEfcdEe0c6dB38070F9A5FD2D",
        "0xc443C6c6AE98F5110702921138D840e77dA67702",
        "0x09428e8674496e2d1e965402f33a9520c5fcbbe2"
    ]

The ``validators`` has higher priority compare to ``extraData`` and if
both are specified, than ``extraData`` will be rewritten.

What are the keystore passwords?
---------------------------------

All the keystores use the same password: ``test`` (*please do not use in
any production enviroment*)
