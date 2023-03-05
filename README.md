# Nolus Testnet Snapshots Guide

1. Follow official documentation in order to setup a full node in Nolus Testnet: https://docs-nolus-protocol.notion.site/Run-a-Full-Node-7a92545223e7483bb4a02cce30b53aa8#9915251c4cf046e0a0470cfffd46935d.
Make sure you use the actual version of ``nolusd``.

2. Set up a service to run ``nolusd`` binary.
3. Install lz4.
```
apt install lz4
```
4. Stop the service, backup priv_validator_state.json, then reset the database.
```
systemctl stop nolusd
cp $HOME/.nolus/data/priv_validator_state.json $HOME/.nolus/priv_validator_state.json.backup
rm -r $HOME/.nolus/data
rm -r $HOME/.nolus/wasm
```
5. Download the snapshot.
```
curl -L http://31.220.82.52/nolus-rila/data.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.nolus
```
6. Download the wasm folder.
```
curl -L http://31.220.82.52/nolus-rila/wasm.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.nolus
```
7. Restore priv_validator_state.json.
```
mv $HOME/.nolus/priv_validator_state.json.backup $HOME/.nolus/data/priv_validator_state.json
```
8. Restart the service, then check logs.
```
systemctl restart nolusd
journalctl -u nolusd -f -o cat
```
