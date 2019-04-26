Observer DApp
====================================

The Observer DApp provides an interface to manage the observer set of nodes. To manage this set, it is possible to
add and remove nodes. To identify nodes, the `enode address <https://github.com/ethereum/wiki/wiki/enode-url-format>`_ is used.

Prerequisites
---------------
* `Git <https://git-scm.com/book/en/v2/Getting-Started-Installing-Git>`_
* `npm <https://www.npmjs.com/get-npm>`_
* `Docker <https://www.docker.com/get-started>`_
* `MetaMask (Chrome) <https://metamask.io/>`_

.. note:: MetaMask is having issues running on Firefox. This bug was reported back in August 2018 and we're awaiting a fix. Until then please use Chrome.

Download the DApp
--------------------------

First, clone the Observer DApp `repository <https://github.com/clearmatics/observer-dapp>`_ using your terminal

.. code-block:: none

    git clone git@github.com:clearmatics/observer-dapp.git

Please write the following in your terminal before proceeding to the next section

.. code-block:: none

    cd observer-dapp


Start the DApp
---------------

There are two options to get the DApp up and running:

Option 1: Packet manager
^^^^^^^^^^^^^^^^^^^^^^^^
The first thing you need to do is to install the dependencies, in your terminal write

.. code-block:: none

    npm install

As long as the terminal doesn't display any error messages, you can now proceed with starting the app by writing

.. code-block:: none

    npm start

This should automatically open a tab in your Chrome browser which shows the user interface. If this is not the case,
you can see it at http://localhost:3000/. 

Option 2: Docker
^^^^^^^^^^^^^^^^
The first thing is to build the image so in your terminal write

.. code-block:: none

    make build

The last line of the output in the terminal should show a success message of the type

.. code-block:: none

    Successfully tagged clearmatics/observer-dapp:latest

You can now process with building the image. In your terminal write

.. code-block:: none

    make run

In your browser, you can now see the user interface at http://localhost:3000/.


Next steps
------------------
That's it. Since the contracts are pre-deployed as part of the Autonity client, you should now be able to adjust the network permissioning. If your MetaMask is properly set up and your
account has sufficient funds, you should be able to add and remove a node.

For further information about managing the deployed contracts, please visit `Soma <https://docs.autonity.io/network-perm/soma.html>`_ and `Glienicke <https://docs.autonity.io/network-perm/glienicke.html>`_.

