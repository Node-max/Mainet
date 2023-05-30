# Manual installation
### Setup validator name
```python
MONIKER="YOUR_MONIKER_GOES_HERE"
```
### Preparing the server
```python
sudo apt -q update
sudo apt -qy install curl git jq lz4 build-essential
sudo apt -qy upgrade
```
### GO 1.19
```python
sudo rm -rf /usr/local/go
curl -Ls https://go.dev/dl/go1.20.2.linux-amd64.tar.gz | sudo tar -xzf - -C /usr/local
eval $(echo 'export PATH=$PATH:/usr/local/go/bin' | sudo tee /etc/profile.d/golang.sh)
eval $(echo 'export PATH=$PATH:$HOME/go/bin' | tee -a $HOME/.profile)
```
# Node installation
### Clone project repository
```python
cd || return
rm -rf desmos
git clone https://github.com/desmos-labs/desmos.git
cd desmos || return
git checkout v4.8.1
### Build binaries
make build
```
### Init your node
```python
desmos config chain-id desmos-mainnet
desmos init "$NODE_MONIKER" --chain-id desmos-mainnet
``` 
### Create service
```python
sudo tee /etc/systemd/system/desmosd.service > /dev/null << EOF
[Unit]
Description=Desmos Node
After=network-online.target
[Service]
User=$USER
ExecStart=$(which desmos) start
Restart=on-failure
RestartSec=10
LimitNOFILE=10000
[Install]
WantedBy=multi-user.target
EOF
```
### Download genesis and addrbook
```pythom
curl -Ls https://snapshot.max-node.xyz/desmos/genesis.json > $HOME/.desmos/config/genesis.json
curl -Ls https://snapshot.max-node.xyz/desmos/addrbook.json > $HOME/.desmos/config/addrbook.json
```
### Add seeds
```python
SEEDS="bd972cd40e9c7a641aa1d5dc51cba1da3a0ead3b@rpc.desmos.max-node.xyz:27656,5c86915026093f9a2f81e5910107cf14676b48fc@seed-2.mainnet.desmos.network:26656,45105c7241068904bdf5a32c86ee45979794637f@seed-3.mainnet.desmos.network:26656"
PEERS=""
sed -i 's|^seeds *=.*|seeds = "'$SEEDS'"|; s|^persistent_peers *=.*|persistent_peers = "'$PEERS'"|' $HOME/.desmos/config/config.toml
```
### Set minimum gas price
```python
sed -i 's|^minimum-gas-prices *=.*|minimum-gas-prices = "0.0001udsm"|g' $HOME/.desmos/config/app.toml
```
### Set pruning
```python
sed -i 's|^pruning *=.*|pruning = "custom"|g' $HOME/.desmos/config/app.toml
sed -i 's|^pruning-keep-recent  *=.*|pruning-keep-recent = "100"|g' $HOME/.desmos/config/app.toml
sed -i 's|^pruning-interval *=.*|pruning-interval = "10"|g' $HOME/.desmos/config/app.toml
sed -i 's|^snapshot-interval *=.*|snapshot-interval = 0|g' $HOME/.desmos/config/app.toml
```
### Set custom ports
```python
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:30658\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:30657\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:6460\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:30656\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":30660\"%" $HOME/.desmos/config/config.toml && sed -i.bak -e "s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:9490\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:9491\"%; s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:1717\"%; s%^address = \"0.0.0.0:8545\"%address = \"0.0.0.0:8945\"%; s%^ws-address = \"0.0.0.0:8546\"%ws-address = \"0.0.0.0:8946\"%; s%^address = \"127.0.0.1:8545\"%address = \"127.0.0.1:8945\"%; s%^ws-address = \"127.0.0.1:8546\"%ws-address = \"127.0.0.1:8946\"%" $HOME/.desmos/config/app.toml && sed -i.bak -e "s%^node = \"tcp://localhost:26657\"%node = \"tcp://localhost:30657\"%" $HOME/.desmos/config/client.toml 
```
### Download latest chain snapshot
```python
curl -L https://snapshot.max-node.xyz/desmos/_latest.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.desmos
[[ -f $HOME/.desmos/data/upgrade-info.json ]] && cp $HOME/.desmos/data/upgrade-info.json
```
### Start service and check the logs
```python
sudo systemctl start desmosd && sudo journalctl -u desmosd -f --no-hostname -o cat
`
