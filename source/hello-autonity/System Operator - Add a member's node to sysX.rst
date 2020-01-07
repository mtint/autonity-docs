## System Operator - Add a member's node to System X

To add the newly deployed node to System X, a transaction must be sent to the Autonity Protocol method responsible for adding new nodes. That transaction must be signed by an authorised account i.e. Governance Operator and the account must have enough fee tokens to pay for the gas.

##### Prerequisites

1. `enode` values received from the member's newly deployed node.
2. MetMask is installed in the default browser (or any other web wallet of choice).
3. Governance Operator and Treasure Operator addresses and private keys generated during the deployment of System X (_add How To guide link_).

##### Steps

1. Open the web browser where MetMask plugin is installed.

2. Run the following command to forward a deployed and running node to localhost:

`kubectl -n <node namespace> port-forward svc/autonity-node-0 8545:8545`

3. Setup a new network in Metamask using the following information:

  a. URL: http://127.0.0.1
  b. ChainID: 1489

4. Locate the 2 files including the addresses and private keys of the Treasure Operator and Governance Operator.
5. Import the Treasure Operator account inside MetaMask using the Treasure Operator account address and private key. If done successfully the balance of the Treasure Operator should be displayed inside MetaMask.
6. Import the Governance Operator account inside MetaMask using the Governance Operator's account address and private key. The Governance Operator's account should show 0. 
7. Send a transaction using MetaMask from the Treasury Operator to the Governance Operator with the following parameters:

    + Amount: 177 ETH
    + Gas Price: 1,000 Gwei
    + Gas Limit: 21,000

  After submitting the transaction, switch to the Governance Operator's account. The balance should be 177 ETH.  The Governance Operator account now has the required transaction fees to submit a transaction to add the new node to the network.

8. Run the following command to get the Autonity contract address:

`curl -X POST -H "Content-Type: application/json" --data \
'{"jsonrpc":"2.0","method":"tendermint_getContractAddress","params":[],"id":1}' \
http://localhost:8545`

9. Clone the following repository and change the current directory:

```
git clone git@github.com:clearmatics/governance-operator.git
cd governance-operator
```

10. Edit `config.json` and replace `address` and `private_key` in the file with those of the Governance_Operator:

```
{
  "uri": "http://127.0.0.1:8545",
  "account": {
    "address": "0xe06e3238D28a7a661416CB65c8cecfFE47daB296",
    "privateKey": "ceb09f113efe9b65967ea8699b3ca6ae85aa1ac244546b3b5edc3675c1ee659b"
  },
  "gas": 200000,
  "gasPrice": 10000000000000
}
```

8. Run the following command to send the transaction to the Autonity smart contract to add the new node and assign it a Validator role:

```
contract_addr=<Autonity smart contract address>
validator_addr=<enode value received from the member new node>
stake=<amount of stake tokens as integer value>
enode=<????>
docker run -ti --rm -v $(pwd)/config.json:/governance-operator/config.json --net=host clearmatics/governance-operator \
      addValidator ${contract_addr} ${validator_addr} ${stake} ${enode}
```

The node is now added to System X.