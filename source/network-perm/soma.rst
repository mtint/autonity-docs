Soma Validator Governance
====================================

Autonity adds the ability of users to govern the validators on a network through a smart contract, Soma, deployed upon network initialisation.

Soma restricts who has the ability to create and validate blocks on the network. However it also allows each consortia creating a network to define the governance mechanism through which the validator set is maintained.

Currently Soma is only available for the IBFT consensus mechanism in Autonity.

Design Rationale
----------------

Soma design goals are:
    - Govern the network validator whitelist
    - Create an open interface whereby many governance mechanisms can be implemented to suit all requirements

**Whitelist of Network Members.**
The list of nodes which create and validate blocks stored in a smart contract.

Nodes not contained in the whitelist should be prevented from creating blocks but should be able view and submit transactions on the network.

The initial configuration of the list is defined at the genesis file. It should be noted that this list must be non-empty, as only members in the network can vote to add new readers/listeners. The size of the list is dynamic. However, the details of the governance
processes (e.g. the maximum size of the list) can be defined in the smart contract.

**Modular Governance.**
The logic in the smart contract sets the rules to add and remove peers from the whitelist. Thus, the user can customize
the governance of the member set writing the contract functions which satisfy a defined interface. Examples of variables
that can be defined at the contract level are:

- The minimum quorum and threshold required to add/remove nodes.
- The minimum and maximum size of the whitelist.
- The voting mechanics to add/remove nodes.

How To Use Soma
---------------
To use Soma three additional fields must be added the config of the `genesis.json` which define the Soma contracts binary, ABI and the contract deployer:

.. code-block:: json

    {
        ...
        "istanbul" : {
            "epoch": 30000,
            "policy": 0,
            "Bytecode": "608060405234801561001057...",
            "ABI": `[{"constant":false,"inputs": ...}]`,
            "Deployer": "0x1337000000000000000000000000000000000000"
        }
        ...
    }  

The bytecode and ABI must be generated from the same compiled smart contract. The deployed *may* be important to the smart contract logic however by design Soma is unopionated, natively it only has the effect of determining the address at which the contract is deployed at.
