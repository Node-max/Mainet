# Chain ID: crescent-1 | Latest Version Tag:  v4.1.0
# [Website](https://app.crescent.network/) | [Discord](https://discord.gg/crescentnetwork) | [Twitter](https://twitter.com/CrescentHub)

# Chain explorer
https://crescent.explorers.guru/
# [RESTAKE](https://restake.app/crescent) - [Stake Here](https://restake.app/crescent)

### Validator: CrescentNodeMax crevaloper1x77p6m3w6xddqy253jtup32n97fr8mdwrlgzez

# [Stake Here](https://restake.app/crescent/crevaloper1x77p6m3w6xddqy253jtup32n97fr8mdwrlgzez)

# Public endpoints
api: https://api.crescent.max-node.xyz \
rpc: https://rpc.crescent.max-node.xyz \
grpc: rpc.crescent.max-node.xyz

# Peering
### state-sync
```python
272b0aa26afbcee20835e8a5020297d5d5e5bd13@rpc.crescent.max-node.xyz:26656
```

### addrbook
```python
curl -Ls https://snapshot.max-node.xyz/crescent/addrbook.json > $HOME/.crescent/config/addrbook.json
```
### genesis
```python
curl -Ls https://snapshot.max-node.xyz/vrescent/genesis.json > $HOME/.crescent/config/genesis.json
```

### live-peers
```python
peers="d85a3bb3ea9522c34b5afc1f4dbd537112a7bde8@5.9.99.172:14556,8597198c3ca246680cf970a03d804fa7dfdda2ce@65.108.99.37:26756,1bdadb5876d3a34379a3e243b1bb5f2191aa342d@66.45.251.38:56656,08379b23453595f34271381cdb299c4157fbc1a0@51.250.105.195:26656,291d178f780f495b0c0baca0a7a22123e0cac7e8@65.108.234.105:3000,e680384785a00bad821ddf33f949381c06eb8537@144.126.133.37:10113,cbca2e1a3bbfa734ba23c15f5a1a74b2bc4f1e79@193.70.45.106:14556,2277e8d7a7d21f7cfebd1d8dcfa222afb7abcb99@103.180.28.212:26656"
sed -i -e "s|^persistent_peers *=.*|persistent_peers = \"$peers\"|" $HOME/.crescent/config/config.toml
```


