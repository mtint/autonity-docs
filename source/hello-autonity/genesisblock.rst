---
# Options for genesis block. Must be the same for all validator nodes (optional value only for new networks)
genesis:
  config:
    homesteadBlock: 0
    eip150Block: 0
    eip150Hash: '0x0000000000000000000000000000000000000000000000000000000000000000'
    eip155Block: 0
    eip158Block: 0
    petersburgBlock: 0
    constantinopleBlock: 0
    byzantiumBlock: 0
    tendermint:
      policy: 0
      block-period: 1
    chainId: 1489
    autonityContract:
      deployer: '0x0000000000000000000000000000000000000002'
      bytecode: ''
      abi: ''
      minGasPrice: 10000000000000
      operator: '0xae223655126e514C9C80096d99765A98547247D3' (GOVERNENCE OPERATOR value)
      users:
      - enode: fqdn://val-0-workshop.4c621a00-2099-45c8-b50c-f06f95c0bcf3.com
        type: validator
        stake: 50000
      - enode: fqdn://val-1-workshop.4c621a00-2099-45c8-b50c-f06f95c0bcf3.com
        type: validator
        stake: 50000
      - enode: fqdn://validator2.autonity.online
        type: validator
        stake: 50000
      - enode: fqdn://validator3.autonity.online
        type: validator
        stake: 50000
      - enode: fqdn://operator0.autonity.online
        type: participant
  nonce: '0x0'
  timestamp: '0x0'
  gasLimit: '100000000'
  difficulty: '0x1'
  coinbase: '0x0000000000000000000000000000000000000000'
  number: '0x0'
  gasUsed: '0x0'
  parentHash: '0x0000000000000000000000000000000000000000000000000000000000000000'
  mixHash: '0x63746963616c2062797a616e74696e65206661756c7420746f6c6572616e6365'
  alloc:
    0x981dfa463bE3c247Fe311a05EeD4c67265204417:
      balance: '0x200000000000000000000000000000000000000000000000000000000000000' (TREASURY OPERATOR value)