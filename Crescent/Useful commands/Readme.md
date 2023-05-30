### Bank: Send
```python
crescentd tx bank send KEY RECEIVER_ADDRESS 1000000ucre \
  --chain-id crescent-1 \
  --node https://rpc.crescent.max-node.xyz:443 --fees 9000ucre  --gas auto --gas-adjustment 1.5 \
  --from KEY
  ```
### Distribution: Withdraw Rewards including Commission
```python
crescentd tx distribution withdraw-rewards VALIDATOR_OPERATOR \
  --commission \
  --chain-id crescent-1 \
  --node https://rpc.crescent.max-node.xyz:443 --fees 9000ucre  --gas auto --gas-adjustment 1.5 \
  --from KEY
  ```
### Gov: Query Proposal
```python
crescentd query gov proposal PROPOSAL_NUMBER \
  --chain-id crescent-1 \
  --node https://rpc.crescent.max-node.xyz:443 \
  --output json | jq
  ```
## Gov: Vote
### VOTE_OTION: yes, no, no_with_veto and abstain.
```python
crescentd tx gov vote PROPOSAL_NUMBER VOTE_OPTION \
  --chain-id crescent-1 \
  --node https://rpc.crescent.max-node.xyz:443 --fees 9000ucre  --gas auto --gas-adjustment 1.5 \
  --from KEY
  ```
### Slashing: Unjail
```python
crescentd tx slashing unjail \
  --chain-id crescent-1 \
  --node https://rpc.crescent.max-node.xyz:443 --fees 9000ucre  --gas auto --gas-adjustment 1.5 \
  --from KEY
  ```
## Staking: Create Validator

### Note: We use example filed values instead of capitalized dummy words for demo purpose in this command. Please make sure to adjust accordingly for your use.
```python
crescentd tx staking create-validator \
  --amount 1000000ucre \
  --commission-max-change-rate "0.05" \
  --commission-max-rate "0.10" \
  --commission-rate "0.05" \
  --min-self-delegation "1" \
  --pubkey=$(crescentd tendermint show-validator) \
  --moniker 'CrescentNodeMax' \
  --website "https://github.com/Node-max" \
  --identity "56AEB33B1C7FC85D" \
  --details "CrescentProof-of-Stake" \
  --security-contact="apofiiss.san@gmail.com" \
  --chain-id crescent-1 \
  --node https://rpc.crescent.max-node.xyz:443 --fees 9000ucre  --gas auto --gas-adjustment 1.5 \
  --from KEY
  ```
