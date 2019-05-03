
Decentralised Applications (DApps)
===========================================

Our DApps provide an interface to manage an Autonity network, consisting of at least four validators. The permissioning of a network is based on both validator governance
and P2P permissioning. The smart contracts in charge of this are `Soma <https://docs.autonity.io/network-perm/soma.html>`_ and `Glienicke <https://docs.autonity.io/network-perm/glienicke.html>`_, respectively.

Both DApps have similar characteristics but there are important differences between them. These can be summarised as follows:

Similarities
------------
- An abilitiy to add and remove nodes
- An interface which allows the use of a custom protocol
- An interface to deny or allow connection from a peer

Differences
-----------
- Soma restricts access to participate in the consensus mechanism
- Glienicke restricts connection access and ability to interact with the network
- All validators are observers but an observer is not necessarily a validator

Guides: Installation
--------------------
.. toctree::
   :maxdepth: 1

   validator.rst
   observer.rst

.. note:: Both of the DApps can also be found on our Github page: `Validator <https://github.com/clearmatics/validator-dapp>`_ and `Observer <https://github.com/clearmatics/observer-dapp>`_ 