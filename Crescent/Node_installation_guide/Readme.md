# Manual installation
### Preparing the server
```python
sudo apt update 
sudo apt install curl tar wget clang pkg-config libssl-dev libleveldb-dev jq build-essential bsdmainutils git make htop unzip bc htop -y
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
git clone https://github.com/crescent-network/crescent crescent
cd crescent
git checkout v4.0.0
### Build binaries
make build
```
# Initialize Node
### Replace Moniker with your own name for node.
```python
crescentd init Moniker --chain-id crescent-1
```
# Download genesis and addrbook
```pythom
curl -Ls https://snapshot.max-node.xyz/crescent/genesis.json > $HOME/.crescent/config/genesis.json
curl -Ls https://snapshot.max-node.xyz/crescent/addrbook.json > $HOME/.crescent/config/addrbook.json
```
# Setup daemon procces
```python
sudo tee /etc/systemd/system/crescentd.service > /dev/null <<EOF 
[Unit] 
Description=Crescent Node 
After=network-online.target 

[Service] 
User=$USER 
ExecStart=$(which crescentd) start 
Restart=on-failure 
RestartSec=3 
LimitNOFILE=65535 

[Install] 
WantedBy=multi-user.target 
EOF
```
# Download latest chain snapshot
```python
curl -L https://snapshot.max-node.xyz/crescent/crescent-1_latest.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.crescent
[[ -f $HOME/.crescent/data/upgrade-info.json ]] && cp $HOME/.crescent/data/upgrade-info.json $HOME/.crescenty/cosmovisor/genesis/upgrade-info.json
```
# Start service and check the logs
```python
sudo journalctl -fu crescentd -o cat
```
