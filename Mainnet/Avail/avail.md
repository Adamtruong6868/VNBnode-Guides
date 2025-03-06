# Avail Mainnet validator
|  Chain ID       |    Version  |
|-----------------|-----------|
|mainnet          |  v2.2.0   |
# Minimum hardware
|   Spec  |        Requirements      |
| :---------: | :-----------------------: |
|   **CPU**   |          8 Cores (Intel / AMD)        |
|   **RAM**   |          16 GB            |
|   **NVME**   |          500 GB            | 

## Snapshot
✅ Auto Snapshot daily: 
```
https://github.com/vnbnode/VNBnode-Guides/blob/main/Avail/snapshot.md
```
## Setup validator name
Replace YOUR_MONIKER with your validator name
```
MONIKER="YOUR_MONIKER"
```
## Install dependencies
```
# UPDATE SYSTEM AND INSTALL BUILD TOOLS
sudo apt -q update
sudo apt -qy install curl git jq lz4 build-essential
sudo apt -qy upgrade
```
## Download binaries and check version
```
curl -L https://github.com/availproject/avail/releases/download/v2.2.5.0/x86_64-ubuntu-$(lsb_release -sr | tr -d .)-avail-node.tar.gz | tar -xz -C /usr/local/bin

avail-node --version
# Should be: avail-node 2.2.0-a6600ea38c9
```
## Create a service file
```
sudo tee /etc/systemd/system/avail.service > /dev/null << EOF
[Unit]
Description=Avail node
After=network-online.target

[Service]
User=$USER
ExecStart=$(which avail-node) \
  --base-path $HOME/.avail/data/ \
  --chain mainnet \
  --name "$MONIKER" \
  --rpc-external \
  --rpc-cors all \
  --rpc-methods safe
Restart=on-failure
RestartSec=10
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
```
```
sudo systemctl daemon-reload
sudo systemctl enable avail.service
```
## Start service and check the logs
```
sudo systemctl start avail.service && journalctl -u avail.service -f --no-hostname -o cat
```
