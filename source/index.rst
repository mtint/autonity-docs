.. autonity documentation master file, created by
   sphinx-quickstart on Thu Jan 24 13:28:37 2019.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Autonity
====================================

**What it is**

Autonity is a generalisation of the `Ethereum Protocol`_ and has features that make it applicable for permissioned networks: 

- Autonity supports deterministic finality, and has the ability to permission validators and network access 
- Autonity works in harmony with Ion_, a general interoperabillity framework, to support interoperability between Ethereum chains, and even Ethereum and non-Ethereum platforms

**Get started**

Run Autonity Hello World to get started with your Autonity network.

.. toctree::
   :maxdepth: 2

   hello-autonity/index.rst
   network-perm/index-nw.rst
   dapps/index-dapps.rst
   IBFT/index.rst
   ion/index.rst
   deploy/index.rst



.. note:: Have a question? You can reach the Autonity team on Github_ or in the `Autonity Gitter`_ channel


.. _Ethereum Protocol: https://www.ethereum.org/
.. _Ion: https://www.github.com/clearmatics/ion/
.. _Github: https://www.github.com/clearmatics/autonity/
.. _Autonity Gitter: https://gitter.im/clearmatics/autonity



* Autonity Enterprise Ethereum Client

** What is Autonity?
Autonity - Fork of Go Ethereum
targeted for private networks
implements the Tendermint consensus algorithmn (BFT type)
Autonity client protocol use case - financial apps/enterprise applications/high performance and secure
Economic layer for new business models - fee redistribution/decentralised applications

Hyperledger Autonity is an open-source Ethereum client developed under the Apache 2.0 license and written in Java. 
It runs on a fork of the Go Ethereum public network and is targeted for private networks. Autonity implements Proof of Work (Ethash) and Proof of Authority (IBFT 2.0 and Clique) consensus mechanisms. 

You can use Autonity to develop private network enterprise applications that need secure, high-performance 
processing. 

Autonity supports enterprise features including privacy and permissioning. 

** What can you do with Autonity?
crypto economic system development
smart contracts
decentralised apps

Autonity includes a [command line interface](Reference/CLI/CLI-Syntax.md) and [JSON-RPC API](HowTo/Interact/APIs/API.md)
for running, maintaining, debugging, and monitoring nodes in an Ethereum network. You can use the API via RPC
over HTTP or via WebSockets, and Pub/Sub is supported. The API supports typical Ethereum functionalities such as:

* Smart contract development
* Decentralized application (Dapp) development

** What does Autonity support?

The Autonity client supports smart contract and Dapp development, deployment, and operational use cases and API Autonity related RPC-APIs. And all standard Key management and standard Ethereum tooling. The aim of Autonity is to stay close to Go Ethereum and all features compatible with the Open Source.

** Develop Crypto Edconomic Systems

** System Requirements
same. - archive or client
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

DOnt need Free Gas Network






