Ion
====================================

The Ion Interoperability Framework is an interoperability protocol that supports the trustless transfer of state and value between Ethereum and non-Ethereum chains. In conjunction with a deterministic consensus algorithm Ion can model PvP and DvP use cases with deterministic finality. Non-deterministic consensus algorithms are also supported.

The Ion project currently has validation contracts for 

- Ethereum IBPFT
- Ethereum Clique
- Hyperledger

The Ion_ Github repository contains a full example of interoperating between Rinkeby and a local Ethereum chain. The `Simple Shares`_ example shows a full implementation of a DvP flow modeling issuance of a security on Hyperledger Fabric network and settling a transaction on an Ethereum network.

.. _Ion: https://www.github.com/clearmatics/ion/
.. _Simple Shares: https://github.com/clearmatics/simpleshares
