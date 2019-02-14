Glienicke - P2P Permissioning
====================================

Autonity supports network permissioning in private blockchains by leveraging a smart contract which manages which nodes can access the network.
Keeping a consistent state of the list of members of nodes is technically feasible due to the finality property (i.e. no forks) of BFT-like consensus protocols
used by the Autonity client.

The restriction of access to the ledger can be tackled at different layers of the network stack and providing various levels of access to the nodes in the network.
The main network and protocol layers at which the permissioning can be implemented are TCP/IP level and below (e.g. physical level), DevP2P, Ethereum Service protocol level or at the sub-protocol
level (e.g. Ethereum v.63). In terms of the level of access granted, the members of the network may be able to read the contents of the ledger (i.e. blockchain observers), append blocks into
the chain (i.e. miners or validators) and send transactions to be inserted in blocks by the validators.

In our first release, our solution targets the restriction of read-access to the blockchain implementing minimal light modifications at the Ethereum protocol level.


.. note:: More fine-grained permissioning solutions at different layers of the stack are present in the Autonity roadmap.


Design Goals
---------------

The design goals of our solution are:

- An on-chain oracle (in the form of a smart contract) maintaining a white list which determines who has read access in the network.
- A governance process for adding and removing nodes from the white list.
- Changes at the client and at the Ethereum protocol level to enforce the on-chain whitelist at the P2P level.

**Whitelist of Network Members.**
The list of nodes which are allowed to read the chain and listen to blocks is stored in a smart contract.
Autonity nodes which are not in the whitelist should not be able to access the chain or exchange messages with other nodes
which belong to the network.
The initial configuration of the list is defined at the genesis file. It should be noted that this list must be non-empty, as only members in the
network can vote to add new readers/listeners. The size of the list is dynamic. However, the details of the governance
processes (e.g. the maximum size of the list) can be defined in the smart contract.

**Modular Governance.**
The logic in the smart contract sets the rules to add and remove peers from the whitelist. Thus, the user can customize
the governance of the member set writing the contract functions which satisfy a defined interface. Examples of variables
that can be defined at the contract level are:

- The minimum quorum and threshold required to add/remove nodes.
- The minimum and maximum size of the whitelist.
- The voting mechanics to add/remove nodes.
- Etc.

**Absence of Bootnodes**
It is common practice in public blockchains to use bootnodes or static nodes as bridges to P2P networks. A bootnode is
a node which is always running and available to relay peers information to new nodes.
However, in a private blockchain relying in the use of bootnodes would mean that some nodes have privileges over the others,
as static nodes could not be removed from the whitelist. Our solution leverages light modifications at the Etehereum protocol
and DevP2P level to avoid the need of using bootnodes or static nodes. Autonity lets the members of the whitelist dial and
setup connections with the new additions of the list. At the same time, when a node is removed from the list, the remaining
members will close connections with the node.

Implementation Details and Limitations
----------------------------------------

**API of the Network permissioning contract.**

 ``getNetworkMembers(blockNumber uint64)``
 ``getNetworkMemberByHash(...)``
 ``getGlienickeContractAddress()``

**Deployment of the contract.**

1. The smart contract logic is defined at network deployment time by including the Solidity contract bytecode at the Genesis file along with the initial whitelisted nodes.
2. The Autonity protocol deploys automatically the smart contract at block #1.
3. Each member retrieve the current state of the whitelist after each mined block (i.e. once per block height) and enforces the addition/removal of peers.

**Changes on the Eth protocol.**
TBC

**Limitations.**

- A malicious member of the whitelist can always act as a relayer of the contents of the ledgers and txs on the network [#]_.


.. [#] This behavior is unavoidable. However, if this relay of information is made through a public channel, leveraging cryptographic primitives to enforce non-repudiation will eventually lead to the removal of the rogue peer from the whitelist. This feature is in the Autonity roadmap but not yet implemented.
