# Snapshot

### install dependencies, if needed
```pyton
sudo apt update
sudo apt install lz4 -y
```
## Instructions
Stop the service and reset the data
```python
sudo systemctl stop bcnad
cp $HOME/.bcna/data/priv_validator_state.json $HOME/.bcna/priv_validator_state.json.backup
rm -rf $HOME/.bcna/data
```
## Download latest snapshot
```python
curl -L https://snapshots.max-node.xyz/bitcanna/bitcanna/bitcanna-1_latest.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.bcna
mv $HOME/.bcna/priv_validator_state.json.backup $HOME/.bcna/data/priv_validator_state.json
```
## Restart the service and check the log
```python
sudo systemctl start bcnad && sudo journalctl -u bcnad -f --no-hostname -o cat
```
