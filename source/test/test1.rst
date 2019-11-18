XXXX - Validator Governance
====================================

Autonity adds the ability of users to govern the validators on a network through a smart contract, Soma, deployed upon network initialisation. 

Soma restricts who has the ability to create and validate blocks on the network. However it also allows each consortia, running an Autonity network, to define the governance mechanism through which the validator set is maintained. Soma merely requires a number of smart contract interfaces to be implemented that allow the consensus mechanism to access the validator set when creating new blocks, otherwise Soma is unopinionated as to how the validator set is governed.

Currently Soma is only available for the IBFT consensus mechanism in Autonity or any kind of consensus protocol which ensures block finality (i.e. no forks).

Design Goals
----------------
