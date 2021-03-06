Soma - Validator Governance
====================================

Autonity adds the ability of users to govern the validators on a network through a smart contract, Soma, deployed upon network initialisation. 

Soma restricts who has the ability to create and validate blocks on the network. However it also allows each consortia, running an Autonity network, to define the governance mechanism through which the validator set is maintained. Soma merely requires a number of smart contract interfaces to be implemented that allow the consensus mechanism to access the validator set when creating new blocks, otherwise Soma is unopinionated as to how the validator set is governed.

Currently Soma is only available for the IBFT consensus mechanism in Autonity or any kind of consensus protocol which ensures block finality (i.e. no forks).

Design Goals
----------------

Soma design goals are:
    - Govern the network validator set.
    - Create an open interface whereby many governance mechanisms can be implemented to suit all requirements.

**Set of Network Validators.**
The set of validators who create and validate blocks are stored in a smart contract. Validators are identified via their public address.

Addresses not contained in the list should be prevented from creating blocks but should be able to view and submit transactions on the network (see Glienicke_ docs).

The initial configuration of the list is defined at the genesis file. It should be noted that this list must be non-empty, as only members in the network can vote to add new validators. The size of the list is dynamic. However, the details of the governance
processes (e.g. the maximum size of the list) is defined in the smart contract.

**Modular Governance.**
The logic in the smart contract sets the rules to add and remove validators from the whitelist. Thus, the user can customize
the governance of the member set writing the contract functions which satisfy a defined interface. Examples of variables
that can be defined at the contract level are:

- The minimum quorum and threshold required to add/remove nodes.
- The minimum and maximum size of the whitelist.
- The voting mechanics to add/remove nodes.

Implementation Details
------------------------

**Soma Contract Interface**

The Soma governance contract **must** define a number of properties and interfaces to allow communication with the consensus layer.

.. note:: The following interface is Solidity specific however other Smart contract languages can be used.

.. code-block:: javascript

    contract Soma {

    address[] public validators;

    // constructor get called at block #1 with msg.owner equal to Soma's deployer
    // configured in the genesis file.
    constructor (address[] _validators) public {
        for (uint256 i = 0; i < _validators.length; i++) {
            validators.push(_validators[i]);
        }
    }

    function getValidators() public view returns (address[]) {
        return validators;
    }

For the consensus layer to be able to access the validator whitelist a function ``getValidators()`` must be implemented that returns the property ``validators`` containing the whitelist of validators. It is up to users to decide how to implement functions governing this whitelist.

**Deploying Soma**

1. The smart contract logic is defined at network deployment time by including the Solidity contract bytecode at the Genesis file along with the initial whitelisted nodes.
2. The Autonity protocol deploys automatically the smart contract at block #1.
3. Each member retrieve the current state of the whitelist after each mined block (i.e. once per block height) and enforces the addition/removal of peers.

To use Soma three additional fields must be added the config of the `genesis.json` which define the Soma contracts binary, ABI and the contract deployer:

.. code-block:: json

    {
        "istanbul" : {
            "epoch": 30000,
            "policy": 0,
            "Bytecode": "608060405234801561001057...",
            "ABI": "[{'constant':false,'inputs': ...}]",
            "Deployer": "0x1337000000000000000000000000000000000000"
        }
    }

The bytecode and ABI must be generated from the same compiled smart contract. The deployer *may* be important to the smart contract logic however by design Soma is unopionated, natively it only has the effect of determining the address at which the contract is deployed at.

**Soma Contract API**

In addition to the standard JSON RPC API of Geth_, Autonity console implements the following of IPC methods for nodes
to retrieve information from the Soma contract via ``web3``:

``istanbul.getValidators(<0x + blockNumber>)`` retrieves the validator set at a given block height.
``ìstanbul.getValidatorsAtHash(<blockHash>)`` retrieves the validator set given the hash of a block.
``istanbul.getSomaContractAddress()`` returns the address of the Soma contract.

.. _Glienicke: http://docs.autonity.io/network-perm/glienicke.html
.. _Geth: https://github.com/ethereum/wiki/wiki/JSON-RPC
