# Chain ID: bitcanna-1 | Latest Version Tag:  v1.7.0
# [Website](https://www.bitcanna.io/) | [Discord](https://discord.gg/QBkZVAyp) | [Twitter](https://twitter.com/BitCannaGlobal)

# Chain explorer
https://explorer.kjnodes.com/
# [RESTAKE](https://restake.app/bitcanna/bcnavaloper1v4m3g2njdlnap5hthz0fslwyvkujjx8djkdy57) - [Stake Here](https://restake.app/bitcanna/bcnavaloper1v4m3g2njdlnap5hthz0fslwyvkujjx8djkdy57)

### Validator: CrescentNodeMax crevaloper1x77p6m3w6xddqy253jtup32n97fr8mdwrlgzez

# [Stake Here](https://explorer.kjnodes.com/bitcanna/staking/bcnavaloper1v4m3g2njdlnap5hthz0fslwyvkujjx8djkdy57)

# Public endpoints
api: https://api.bitcanna.max-node.xyz \
rpc: https://rpc.bitcanna.max-node.xyz \
grpc: rpc.bitcanna.max-node.xyz:9390

# Peering
### state-sync
```python
cd28921e4ee6253a17da2ffd52d37406b520d7a6@rpc.bitcanna.max-node.xyz:29656
```
### genesis
```python
curl -Ls https://snapshots.max-node.xyz/bitcanna/bitcanna/genesis.json > $HOME/.bcna/config/genesis.json
```
### addrbook
```python
curl -Ls https://snapshots.max-node.xyz/bitcanna/bitcanna/addrbook.json > $HOME/.bcna/config/addrbook.json
```

### live-peers
```python
peers="7c00beb4956bc40cd33ced6e2c2ffe07d4fa32e7@95.216.242.82:36656,88c6b1fa1c7fef98b4449b769eb2705476586664@65.109.92.241:21326,b212d5740b2e11e54f56b072dc13b6134650cfb5@169.155.168.54:26656,b587bf827b5f680c417601b536ffbd505c88bb07@193.70.45.106:13056,803fc66e3bd7b724921ef9c40636067f36e880c6@65.108.199.222:32656,b765241852675e8e698715db13b832cbf95a720f@136.243.1.82:28656,a66bce0ddb49dcf60a5b83fd94a7bd4d0878f127@154.53.40.9:26656,dd4d3c0de38aa0575436c34c237b33bc0dda3ef2@142.132.158.93:13056,cb0848b84987c37ba0fa465585c6b9d6cec6deab@65.108.77.98:26696,d9bfa29e0cf9c4ce0cc9c26d98e5d97228f93b0b@65.109.88.38:14256"
sed -i -e "s|^persistent_peers *=.*|persistent_peers = \"$peers\"|" $HOME/.bcna/config/config.toml
```



