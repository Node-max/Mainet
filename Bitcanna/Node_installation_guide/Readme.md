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
cd $HOME
rm -rf bcna
git clone https://github.com/BitCannaGlobal/bcna.git
cd bcna
git checkout v1.7.0
### Build binaries
make build
```
### Prepare binaries for Cosmovisor
```python
mkdir -p $HOME/.bcna/cosmovisor/genesis/bin
mv build/bcnad $HOME/.bcna/cosmovisor/genesis/bin/
rm -rf build
``` 
### Create application symlinks
```python
sudo ln -s $HOME/.bcna/cosmovisor/genesis $HOME/.bcna/cosmovisor/current -f
sudo ln -s $HOME/.bcna/cosmovisor/current/bin/bcnad /usr/local/bin/bcnad -f
```
# Install Cosmovisor and create a service
### Download and install Cosmovisor
```python
go install cosmossdk.io/tools/cosmovisor/cmd/cosmovisor@v1.4.0
```
### Create service
```python
sudo tee /etc/systemd/system/bcnad.service > /dev/null << EOF
[Unit]
Description=bitcanna node service
After=network-online.target

[Service]
User=$USER
ExecStart=$(which cosmovisor) run start
Restart=on-failure
RestartSec=10
LimitNOFILE=65535
Environment="DAEMON_HOME=$HOME/.bcna"
Environment="DAEMON_NAME=bcnad"
Environment="UNSAFE_SKIP_BACKUP=true"
Environment="PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:$HOME/.bcna/cosmovisor/current/bin"

[Install]
WantedBy=multi-user.target
EOF
sudo systemctl daemon-reload
sudo systemctl enable bcnad
```
# Initialize the node
### Set node configuration
```python
bcnad config chain-id bitcanna-1
bcnad config keyring-backend file
bcnad config node tcp://localhost:14257
```
### Initialize the node
```python
bcnad init $MONIKER --chain-id bitcanna-1
```
### Download genesis and addrbook
```pythom
curl -Ls https://snapshots.max-node.xyz/bitcanna/genesis.json > $HOME/.bcna/config/genesis.json
curl -Ls https://snapshots.max-node.xyz/bitcanna/addrbook.json > $HOME/.bcna/config/addrbook.json
```
### Add seeds
```python
sed -i -e "s|^seeds *=.*|seeds = \"400f3d9e30b69e78a7fb891f60d76fa3c73f0ecc@rpc.bitcanna.max-node.xyz:29656\"|" $HOME/.bcna/config/config.toml
```
### Set minimum gas price
```python
sed -i -e "s|^minimum-gas-prices *=.*|minimum-gas-prices = \"0ubcna\"|" $HOME/.bcna/config/app.toml
```
### Set pruning
```python
sed -i \
  -e 's|^pruning *=.*|pruning = "custom"|' \
  -e 's|^pruning-keep-recent *=.*|pruning-keep-recent = "100"|' \
  -e 's|^pruning-keep-every *=.*|pruning-keep-every = "0"|' \
  -e 's|^pruning-interval *=.*|pruning-interval = "19"|' \
  $HOME/.bcna/config/app.toml
```
### Set custom ports
```python
sed -i -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:14258\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:14257\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:14260\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:14256\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":14266\"%" $HOME/.bcna/config/config.toml
sed -i -e "s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:14217\"%; s%^address = \":8080\"%address = \":14280\"%; s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:14290\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:14291\"%; s%:8545%:14245%; s%:8546%:14246%; s%:6065%:14265%" $HOME/.bcna/config/app.toml
```
### Download latest chain snapshot
```python
curl -L https://snapshots.max-node.xyz/bitcanna/bitcanna-1_latest.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.bcna
[[ -f $HOME/.bcna/data/upgrade-info.json ]] && cp $HOME/.bcna/data/upgrade-info.json $HOME/.bcna/cosmovisor/genesis/upgrade-info.json
```
### Start service and check the logs
```python
sudo systemctl start bcnad && sudo journalctl -u bcnad -f --no-hostname -o cat
```

