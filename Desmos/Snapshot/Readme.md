# Snapshot

### install dependencies, if needed
```pyton
sudo apt update
sudo apt install lz4 -y
```
## Instructions
Stop the service and reset the data
```python
sudo systemctl stop desmosd
cp $HOME/.desmos/data/priv_validator_state.json $HOME/.desmos/priv_validator_state.json.backup 
desmos tendermint unsafe-reset-all --home $HOME/.desmos --keep-addr-book
```
## Download latest snapshot
```python
curl https://snapshot.max-node.xyz/desmos/_latest.tar.lz4 | lz4 -dc - | tar -xf - -C $HOME/.desmos
mv $HOME/.desmos/priv_validator_state.json.backup $HOME/.desmos/data/priv_validator_state.json
```
## Restart the service and check the log
```python
sudo systemctl start desmosd && sudo journalctl -u desmosd -f --no-hostname -o cat
```
