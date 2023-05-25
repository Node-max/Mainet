# Snapshot

### install dependencies, if needed
```pyton
sudo apt update
sudo apt install lz4 -y
```
## Instructions
Stop the service and reset the data
```python
sudo systemctl stop crescentd
cp $HOME/.crescent/data/priv_validator_state.json $HOME/.crescent/priv_validator_state.json.backup
rm -rf $HOME/.crescent/data
```
## Download latest snapshot
```python
curl -L https://snapshot.max-node.xyz/crescent/crescent-1_latest.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.crescent
mv $HOME/.crescent/priv_validator_state.json.backup $HOME/.crescent/data/priv_validator_state.json
```
## Restart the service and check the log
```python
sudo systemctl start archwayd && sudo journalctl -u archwayd -f --no-hostname -o cat
```
