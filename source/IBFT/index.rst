Istanbul Byzantine Fault Tolerance (IBFT)
=========================================

`Istanbul Byzantine Fault Tolerance (IBFT) <https://github.com/ethereum/EIPs/issues/650>`_ is a blockchain adaptation of the `PBFT paper <http://pmg.csail.mit.edu/papers/osdi99.pdf>`_. BFT consensus algorithms support a rate of failure of `F` validators, where `F` has to be less than 1/3 of the validators in the network. Failures here include crashes, slow network or any malicious behaviours. Therefore, given a maximum `F` faulty validators the network size must be of size `3F+1` (More details can be found in the `Byzantine General Problem paper <http://www-inst.eecs.berkeley.edu/~cs162/fa12/hand-outs/Original_Byzantine.pdf>`_).

Blocks in IBFT are final, ie no forks can occur, validators reach consensus on the current block by appending `COMMIT` signatures to the `extraData` field of the header. Each validator appends `2F+1 COMMIT` signatures received to the block header before inserting the block into the chain. Therefore, blocks can be easily verified and the light client is also supported.

Consensus State Transitions
---------------------------

The algorithm chooses a validator (the proposer), in a round robin fashion, which proposes a new block to the validators along with a `PRE-PREPARE` message. Upon reception of this new block and the `PRE-PREPARE` message, a validator verifies whether the `proposal` is valid and enters the `PRE-PREPARED` state, the validator broadcasts a `PREPARE` message. The `PREPARE` message is to ensure that validators are working on the same block and round. Upon receiving `2F+1` `PREPARE` message the validator enters the `PREPARED` state and broadcasts a `COMMIT` message. The `COMMIT` message informs the other peers that it has accepted the proposed block and is ready to insert the block into the chain. After receiving `2F+1 COMMIT` messages the validator enters the `COMMITTED` state and attempts to insert the block into the chain, if successful, the validators enters `FINAL COMMITTED` state and moves to the next sequence.

.. image:: state_transition.jpg

A sequence represents the current block on which validators are trying to reach consensus on, while a round consists of the states mentioned above in reaching consensus on the block. A sequence can contain multiple rounds, however, there is only one sequence per block. A round change can happen if there is a timeout, the proposal is invalid or the block insertion fails, upon these events the validators enter the `ROUND CHANGE` state and waits for `2F+1 ROUND CHANGE` messages before moving into a new round.