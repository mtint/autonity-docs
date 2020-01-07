Tendermint Byzantine Fault Tolerance (TBFT)
===========================================

What it is
----------
Tendermint BFT is a software implementation of Byzantine Fault Tolerance adapted for blockchain technology with emphasis on P2P networking and cryptography. 

It replicates software on multiple machines with these characteristics:

* **securely** - functions even if 1/3 of machines fail
* **consistently** - every non-faulty machine sees the same transaction log and computes the same state 

How it does it
--------------
* Tendermint Core - the consensus engine (every machine sees the same transactions in the same order)
* Application BlockChain Interface (ABCI) - transactions processed in any programming language (or Dev Env)

How the validator is chosen - consensus state transitions
----------------------------------------------------------

STEPS (States)
*****

1. Algorithm chooses a proposer Validator
2. This Validator proposes a new block with PRE-PREPARE message
3. A Validator verifies if the proposal is valid and enters PRE-PREPARED state
4. This Validator broadcasts a PREPARE message - ensures that all validators are in synch
5. The Validator receives a 2F+1 PREPARE message and enters the PREPARE state and broadcasts a COMMIT message to say that it accepts the proposed block and is ready to insert the block into the chain
6. The Validator accepts the 2F+1 and enters COMMITED state and inserts the block into the chain
7. The Validator enters FINAL COMMITED state and moves to the next sequence


.. image:: state_transition.jpg

* a sequence represents the current block on which validators are trying to reach consensus
* a round consists of the states (steps) mentioned above in reaching consensus on the block 
* a sequence can contain multiple rounds - but there is only one sequence per block
* a round change can happen if:
	- there is a timeout
	- the proposal is invalid
	- the block insertion fails 
* upon these events the validators enter the `ROUND CHANGE` state and wait for `2F+1 ROUND CHANGE` messages before moving into a new round


.. toctree::
   :maxdepth: 2

   TBFT/test.rst
	


Consensus State Transitions - alternate version
------------------------------------------------

The algorithm chooses a validator (the proposer), in a round robin fashion, which proposes a new block to the validators along with a `PRE-PREPARE` message. Upon reception of this new block and the `PRE-PREPARE` message, a validator verifies whether the `proposal` is valid and enters the `PRE-PREPARED` state, the validator broadcasts a `PREPARE` message. The `PREPARE` message is to ensure that validators are working on the same block and round. Upon receiving `2F+1` `PREPARE` message the validator enters the `PREPARED` state and broadcasts a `COMMIT` message. The `COMMIT` message informs the other peers that it has accepted the proposed block and is ready to insert the block into the chain. After receiving `2F+1 COMMIT` messages the validator enters the `COMMITTED` state and attempts to insert the block into the chain, if successful, the validators enters `FINAL COMMITTED` state and moves to the next sequence.

A sequence: represents the current block on which validators are trying to reach consensus. 
A round consists of the states (steps) mentioned above in reaching consensus on the block. A sequence can contain multiple rounds, however, there is only one sequence per block. A round change can happen if there is a timeout, the proposal is invalid or the block insertion fails, upon these events the validators enter the `ROUND CHANGE` state and waits for `2F+1 ROUND CHANGE` messages before moving into a new round.