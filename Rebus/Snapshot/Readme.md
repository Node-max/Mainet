# Snapshot

### install dependencies, if needed
```pyton
sudo apt update
sudo apt install lz4 -y
```
## Instructions
Stop the service and reset the data
```python
sudo systemctl stop rebusd
cp $HOME/.rebusd/data/priv_validator_state.json $HOME/.rebusd/priv_validator_state.json.backup
rm -rf $HOME/.rebusd/data
```
## Download latest snapshot
```python
curl -L https://snapshots.max-node.xyz/rebusd/reb_1111-1_latest.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.rebusd
mv $HOME/.rebusd/priv_validator_state.json.backup $HOME/.rebusd/data/priv_validator_state.json
```
## Restart the service and check the log
```python
sudo systemctl start rebusd && sudo journalctl -u rebusd -f -o cat
```

