
Network Permissioning
=====================

The Autonity client approach to network permissioning leverages the use of smart contracts to manage the validator set and the nodes that have access to the network.

This form of on-chain governance enables the deployer of a private blockchain to fully customize the governance mechanism of the network.

Autonity network permissioning is composed of two main components a modular architecture: 

* Soma -  which manages the validator set governance 

* Glienicke - that controls the node permissioning at the P2P network level


.. toctree::
   :maxdepth: 1

   soma.rst
   glienicke.rst


From GitHub discussion
----------------------

The network is symmetric in that all participants have identical priviledges. They use mutual authentication.

Network permissioning uses the Glienecke Smart Contract (GSC) interface to retrieve the list of authorized enodes. The problem in the blockchain context is that there is no guaranteed synchronized node state. The node ID alone is not sufficient since we need to know how far ahead a peer node is and this can only be retrieved post Ethereum sub-protocol handshake via the total difficulty parameter.

Here's a description of the current protocol:

* Ethereum service updates an internal white list via the GSC before block insertion
* Every node is dialled periodically
* RLP ensures peers have the private key associated with its nodeID (this happens on the Dev P2P layer)
* ETH Sub-protocol initiates a handshake/current total difficulty is exchanged (this is equal to the chain height with xBFT)
	* If peer total difficulty is > than ours, we accept the incoming connection
	* If peer present, local whitelist accepts incoming connection (nodeID and IP address checked)
	* Else, connection rejected
