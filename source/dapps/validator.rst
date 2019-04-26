Validator DApp
====================================

The Validator DApp provides an interface to manage the validator set of nodes. To manage this set, it is possible to
add and remove nodes. To identify nodes, the `account address <https://github.com/ethereum/go-ethereum/wiki/Managing-your-accounts>`_ is used.

.. note:: Metamask is having issues running on Firefox. This bug was reported back in August 2018 and we're awaiting a fix. Until then please use Chrome.


Prerequisites
---------------
* `Git <https://git-scm.com/book/en/v2/Getting-Started-Installing-Git>`_
* `npm <https://www.npmjs.com/get-npm>`_
* `MetaMask (Chrome) <https://metamask.io/>`_


Download the DApp
--------------------------
First, clone the Validator DApp `repository <https://github.com/clearmatics/validator-dapp>`_ using your terminal

.. code-block:: none

    git clone git@github.com:clearmatics/validator-dapp.git

Please write the following in your terminal before proceeding to the next section

.. code-block:: none

    cd validator-dapp


Start the DApp
---------------
To get the DApp up and running, we use a package manager (npm). In your terminal write

.. code-block:: none

    npm install

As long as the terminal doesn't display any error messages, you can now proceed with starting the app by writing

.. code-block:: none

    npm start

This should automatically open a tab in your Chrome browser which shows the user interface. If this is not the case,
you can see it at http://localhost:3000/. 


Next steps
------------------
That's it. Since the contracts are pre-deployed as part of the Autonity client, you should now be able to adjust the network permissioning. If your MetaMask is properly set up and your
account has sufficient funds, you should be able to add and remove a node.

For further information about managing the deployed contracts, please visit `Soma <https://docs.autonity.io/network-perm/soma.html>`_ and `Glienicke <https://docs.autonity.io/network-perm/glienicke.html>`_.

