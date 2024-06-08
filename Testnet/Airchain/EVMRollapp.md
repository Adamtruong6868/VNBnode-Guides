### Recommended Hardware Requirements

|   SPEC      |       Recommend          |
| :---------: | :-----------------------:|
|   **CPU**   |        4 Cores           |
|   **RAM**   |        8 GB              |
| **Storage** |        200 GB            |

### Update and install packages for compiling
```
cd $HOME && source <(curl -s https://raw.githubusercontent.com/vnbnode/binaries/main/update-binary.sh)
```
```
git clone https://github.com/airchains-network/evm-station.git
```
```
git clone https://github.com/airchains-network/tracks.git
```
```
git clone https://github.com/availproject/availup.git
```
##  Evm-Station
```
screen -S evmstation
```
```
cd evm-station
```
```
go mod tidy
```
#### Edit the MONIKER or Chain ID.
```
nano ./scripts/local-setup.sh
```
#### Setup
```
/bin/bash ./scripts/local-setup.sh
```
```
/bin/bash ./scripts/local-start.sh
```
```
/bin/bash ./scripts/local-keys.sh
```
#### Custom your ports (defaut = 16)
```
echo "export G_PORT="16"" >> $HOME/.bash_profile
source $HOME/.bash_profile
```
```
sed -i.bak -e "s%:1317%:${G_PORT}317%g;
s%:8080%:${G_PORT}080%g;
s%:9090%:${G_PORT}090%g;
s%:9091%:${G_PORT}091%g;
s%:8545%:${G_PORT}545%g;
s%:8546%:${G_PORT}546%g;
s%:6065%:${G_PORT}065%g" $HOME/.evmosd/config/app.toml
```
```
sed -i.bak -e "s%:26658%:${G_PORT}658%g;
s%:26657%:${G_PORT}657%g;
s%:6060%:${G_PORT}060%g;
s%:26656%:${G_PORT}656%g;
s%^external_address = \"\"%external_address = \"$(wget -qO- eth0.me):${G_PORT}656\"%;
s%:26660%:${G_PORT}660%g" $HOME/.evmosd/config/config.toml
```
#### Change address to 0.0.0.0
```
nano $HOME/.evmosd/config/app.toml
```
<img width="500" alt="image" src="https://github.com/Adamtruong6868/VNBnode-Guides/assets/91002010/ec37b3d4-0b4c-4637-b2b5-964aac2650e6">

## Avail DA
```
screen -S avail
```
```
cd availup
```
```
/bin/bash availup.sh --network "turing" --app_id 36
```
ctrl + a + d to escape
#### Check your avail wallet and seed phrase
```
nano /root/.avail/identity/identity.toml
```

## Tracking
```
screen -S track
```
```
sudo rm -rf ~/.tracks
```
```
cd tracks
```
```
go mod tidy
```
```
go run cmd/main.go init --daRpc "http://127.0.0.1:7000" --daKey "AVAIL-PUB-KEY" --daType "avail" --moniker "YOUR-NAME-VNBnode" --stationRpc "http://127.0.0.1:16545" --stationAPI "http://127.0.0.1:16545" --stationType "evm"
```
#### Create Airchain wallet
```
go run cmd/main.go keys junction --accountName "YOUR-NAME-VNBnode" --accountPath $HOME/.tracks/junction-accounts/keys
```
Faucet here: [https://airchains.faucetme.pro/](https://airchains.faucetme.pro/)
```
go run cmd/main.go prover v1EVM
```
#### get node ID
```
nano /root/.tracks/config/sequencer.toml
```
<img width="334" alt="image" src="https://github.com/vnbnode/VNBnode-Guides/assets/128967122/02b096e8-8fe1-49bf-b328-d3d990624c23">

```
go run cmd/main.go create-station --accountName "YOUR-NAME-VNBnode" --accountPath $HOME/.tracks/junction-accounts/keys --jsonRPC "https://airchains-testnet-rpc.cosmonautstakes.com/" --info "EVM Track" --tracks YOUR-AIRCHAIN-ADDRESS --bootstrapNode "/ip4/your-server-ip4/tcp/2300/p2p/YOUR-NODE-ID"
```
```
go run cmd/main.go start
```
# Monitoring your appchain:
[https://points.airchains.io/](https://points.airchains.io/)

# Add chain to metamask:

Chain Name:

Chain ID: 1234

RPC: http://YOUR-SERVER-IP4:16545

## Thank to support VNBnode.
### Visit us at:

<img src="https://user-images.githubusercontent.com/50621007/183283867-56b4d69f-bc6e-4939-b00a-72aa019d1aea.png" width="30"/> <a href="https://t.me/VNBnodegroup" target="_blank">VNBnodegroup</a>

<img src="https://user-images.githubusercontent.com/50621007/183283867-56b4d69f-bc6e-4939-b00a-72aa019d1aea.png" width="30"/> <a href="https://t.me/Vnbnode" target="_blank">VNBnode News</a>

<img src="https://github.com/vnbnode/binaries/blob/main/Logo/VNBnode.jpg" width="30"/> <a href="https://VNBnode.com" target="_blank">VNBnode.com</a>
