# Chain ID: desmos-mainnet | Latest Version Tag:  v4.8.0 
# [Website](https://www.desmos.network/) | [Discord](https://discord.com/invite/ckFcU5vxxc) | [Twitter](https://twitter.com/DesmosNetwork)

# Chain explorer
https://testnet.archway.explorers.guru/

# Stake with DesmosNodeMax - [Stake Here](https://restake.app/desmos/desmosvaloper1lqjzccauwa0wn93nu04q337h6q44yxpmfc6kl7)

# Validator: CrescentNodeMax crevaloper1x77p6m3w6xddqy253jtup32n97fr8mdwrlgzez

# [Stake Here](https://ping.pub/desmos/staking/desmosvaloper1lqjzccauwa0wn93nu04q337h6q44yxpmfc6kl7)

# Public endpoints
api: https://api.desmos.max-node.xyz \
rpc: https://rpc.desmos.max-node.xyz \
grpc: grpc.desmos.max-node.xyz:15690

# Peering
### state-sync
```python
bd972cd40e9c7a641aa1d5dc51cba1da3a0ead3b@rpc.desmos.max-node.xyz:27656
```

### addrbook
```python
curl -Ls https://snapshots.max-node.xyz/desmos/addrbook.json > $HOME/.desmos/config/addrbook.json
```
### genesis
```python
curl -Ls https://snapshots.max-node.xyz/desmos/genesis.json > $HOME/.desmos/config/genesis.json
```

### live-peers
```python
PEERS="f090ead239426219d605b392314bdd73d16a795f@desmos.nodejumper.io:32656,dc26591f9dff06f8d9d7b4431c5534cb759c3ace@65.108.213.177:26656,23721024ea06e3610ab1f6a34b51f592cd1a3589@139.162.81.104:26656,961d438daf13016d580e5809e3255c2aaae928ad@5.9.50.59:22656,277db61bd47123c873520b53f2d7bc3e67946695@15.235.50.175:26664,e507fb82435b5d7fab42967f3914501d4a8a6240@159.65.4.71:26656,dfc0639d17b290db7339d16cca2673f7812d4e5f@65.108.4.28:26656,6dabce67a9e75edb290bda7bf80b26aa47d87192@67.211.210.50:26656,e25f8952bd1a664053602507aeec5536713b7d6a@51.81.155.189:10456,699f701c6e9c05626c11dd8ec4ece52b20270f19@178.79.171.139:26656,9ba7ce8d39b5161fcd6cf2447010bbec42d4692b@141.94.73.39:36756"
sed -i 's|^persistent_peers *=.*|persistent_peers = "'$PEERS'"|' $HOME/.desmos/config/config.toml
```

