.. autonity documentation master file, created by
   sphinx-quickstart on Thu Jan 24 13:28:37 2019.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


Autonity Enterprise Ethereum Client
===================================

*Ethereum based, protocol enabling, permissioned, decentralized, and interoperable transacting member-mutual networks*


**What is Autonity?**

* blockchain-based distributed computing platform and operating system
* a fork of the Go Ethereum protocol
* open source and public

**it:**

* features smart contract functionality
* supports deterministic finality
* implements the Tendermint consensus algorithmn (BFT type)
* implements Proof of Work (Ethash) and Proof of Authority (IBFT 2.0 and Clique) consensus mechanisms
* functions with Ion_, a general interoperabillity framework, to support interoperability between Ethereum chains, and non-Ethereum platforms


**What can you do with Autonity?**

Develop:

* crypto economic systems
* smart contracts
* decentralised apps
* private (permissioned) network enterprise applications that need secure, high-performance processing
* an economic layer for new business models - fee redistribution/decentralised applications


**How can you interact with Autonity?**

Run, maintain, debug and monitor nodes in an Ethereum network through:

* CLI (link to reference) 
* JSON-RPC API (link to reference)



Alternative introduction
========================

**What is Autonity?**

Autonity is a blockchain-based, distributed computing platform and operating system. It is open source and public, and features smart contract functionality. It is a fork of the Go Ethereum protocol, has features that make it suitable for permissioned (private) networks, supports deterministic finality, and implements the Tendermint consensus algorithmn (BFT type).

Autonity implements Proof of Work (Ethash) and Proof of Authority (IBFT 2.0 and Clique) consensus mechanisms. 
It works in harmony with Ion_, a general interoperabillity framework, to support interoperability between Ethereum chains, and even Ethereum and non-Ethereum platforms.



**Get started**

Run Autonity Hello World to get started with your Autonity network.

.. toctree::
   :maxdepth: 2

   hello-autonity/index.rst
   network-perm/index-nw.rst
   dapps/index-dapps.rst
   TBFT/index.rst
   ion/index.rst
   deploy/index.rst


.. note:: Have a question? You can reach the Autonity team on Github_ or in the `Autonity Gitter`_ channel


.. 2Ethereum Protocol: https://www.ethereum.org/
.. _Ion: https://www.github.com/clearmatics/ion/
.. _Github: https://www.github.com/clearmatics/autonity/
.. _Autonity Gitter: https://gitter.im/clearmatics/autonity

**System Requirements**
same - archive or client
RAM - remove Eth Mainnet sentence

** Build with Binary or Docker - same address as System X

* How to start an Auntonity Network

** Create a new network

***Prerequisites

1. Generate a Genesis file
2. Add initial members
3. Ask member for their public key/IP Address (Domain name url - not recommended for production)/Listening port

1. How to generate an enode - use the Autonity command - returns public key part of the enode and then special listening port and IP Address
2. Assign nodes to validators
   Explain the Genesis file in its own section - see the Github section
3. Configure the following parameters:
      * validator
      * stakeholder
      * participant
.. note:: your network must have at least one validator

All enodes need permission to access network

* Configure Autonity

Change minimum gas price
operator - priviledged account can access restricted functions for the Autonity contract


New section Autonity Contract Customisation - see the section on Github (Andres to finish)

stake - customisable

Don't need Free Gas Network

Get started with Autonity

   * System requirements
   * Install binary distribution
   * Build from source
   * Start Autonity
   * Run Autonity from a Docker image

Configure Autonity

   * Consensus protocols
   * Create Autonity genesis file
   * Configure a GAS network
   * High availability
   * APIs?
   * Load balancing
   * Mining
   * Passing LVM options?

Interact with node

   * Autonity APIs
   * Use JSON-RPC API over HTTP or Websockets
   * Use GraphQL over HTTP
   * Authenticate JSON-RPC requests

Client libraries?

   * Use the web3.js-eea Client Library

Filters

   * Accessing logs using the Autonity API

Find and connect to peers

   * Start a bootnode
   * Configure ports for access
   * Manage peers
   * Use UPnp

Send transactions

   * Use wallets for key management
   * Create and send transactions
   * Create and send private transactions
   * Include reason in transaction receipts

* Limit access to node
* Use local permissioning
* Update onchain permissioing whitelists

* Use privacy features
* Use EEA-compliant privacy
* Use Autonity-extended privacy




