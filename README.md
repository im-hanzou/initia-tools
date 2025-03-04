[<img src='assets\Initia-Banner.png' alt='banner' width= '99.9%'>]()

<font size = 7><center><b><u>About Initia</u></b></center></font>

* ### **[Initia](https://initia.xyz/)** is a pioneering network for interwoven rollups, revolutionizing blockchain by simplifying complexity and providing a unified platform akin to using your favorite smartphone, inspired by Apple's design philosophy.

<div align="center">
  <a href="https://initia.xyz/"><img src="https://github.com/bartosian/celestia-tools/assets/20209819/85aaef48-7ea4-4857-b339-985645c6850c" alt="Website" width="16%"></a>
  <a href="https://github.com/initia-labs"><img src="https://github.com/bartosian/celestia-tools/assets/20209819/229ec400-72ff-48ee-ac18-7bdb1f5e221a" alt="Github" width="16%"></a>
  <a href="https://twitter.com/initiaFDN"><img src="https://github.com/bartosian/celestia-tools/assets/20209819/3978b7fc-d575-44a6-8d41-327c14c8ba31" alt="Twitter" width="16%"></a>
  <a href="https://discord.com/invite/initia"><img src="https://github.com/bartosian/celestia-tools/assets/20209819/944a0b87-548d-4109-ad0c-def572d307cb" alt="Discord" width="16%"></a>
  <a href="https://medium.com/@initiafdn"><img src="https://github.com/bartosian/celestia-tools/assets/20209819/ac52729b-64d7-44d1-9a66-1e0d159848f6" alt="Blog" width="16.2%"></a>
</div>

### Navigation Menu
- [Hardware requirements](#hardware-requirements)
- [TrustedPoint Services](#trustedpoint-services)
- [Installation guide](#installation-guide)
  - [1. Install required packages](#1-install-required-packages)
  - [2. Install Go](#2-install-go)
  - [3. Install `initia` binary](#3-install-initia-binary)
  - [4. Set up variables](#4-set-up-variables)
  - [5. Initialize the node](#5-initialize-the-node)
  - [6. Download genesis.json](#6-download-genesisjson)
  - [7. Add seeds and peers to the config.toml](#7-add-seeds-and-peers-to-the-configtoml)
  - [8. Change ports (Optional)](#8-change-ports-optional)
  - [9. Configure prunning to save storage (Optional)](#9-configure-prunning-to-save-storage-optional)
  - [10. Set min gas price](#10-set-min-gas-price)
  - [11. Enable indexer (Optional)](#11-enable-indexer-optional)
  - [12. Create a service file](#12-create-a-service-file)
  - [13. Start the node](#13-start-the-node)
  - [14. Create a wallet for your validator](#14-create-a-wallet-for-your-validator)
  - [15. Request tokens from the faucet on Discord](#15-request-tokens-from-the-faucet-on-discord)
  - [16. Check wallet balance](#16-check-wallet-balance)
  - [17. Create a validator](#17-create-a-validator)
- [State sync](#state-sync)
  - [1. Stop the node](#1-stop-the-node)
  - [2. Backup priv\_validator\_state.json](#2-backup-priv_validator_statejson)
  - [3. Reset DB](#3-reset-db)
  - [4. Setup required variables (One command)](#4-setup-required-variables-one-command)
  - [4. Move priv\_validator\_state.json back](#4-move-priv_validator_statejson-back)
  - [5. Start the node](#5-start-the-node)
  - [6. Check the synchronization status](#6-check-the-synchronization-status)
  - [7. Disable state sync](#7-disable-state-sync)
- [Download fresh addrbook.json](#download-fresh-addrbookjson)
  - [1. Stop the node and use `wget` to download the file](#1-stop-the-node-and-use-wget-to-download-the-file)
  - [2. Restart the node](#2-restart-the-node)
  - [3. Check the synchronization status](#3-check-the-synchronization-status)
- [Add fresh persistent peers](#add-fresh-persistent-peers)
  - [1. Extract persistent\_peers from our endpoint](#1-extract-persistent_peers-from-our-endpoint)
  - [2. Restart the node](#2-restart-the-node-1)
  - [3. Check the synchronization status](#3-check-the-synchronization-status-1)
- [Download Snapshot](#download-snapshot)
  - [1. Download latest snapshot from our endpoint](#1-download-latest-snapshot-from-our-endpoint)
  - [2. Stop the node](#2-stop-the-node)
  - [3. Backup priv\_validator\_state.json](#3-backup-priv_validator_statejson)
  - [4. Reset DB](#4-reset-db)
  - [5. Extract files fromt the arvhive](#5-extract-files-fromt-the-arvhive)
  - [6. Move priv\_validator\_state.json back](#6-move-priv_validator_statejson-back)
  - [7. Restart the node](#7-restart-the-node)
  - [8. Check the synchronization status](#8-check-the-synchronization-status)
- [Useful commands](#useful-commands)
  - [Check node status](#check-node-status)
  - [Query your validator](#query-your-validator)
  - [Query missed blocks counter \& jail details of your validator](#query-missed-blocks-counter--jail-details-of-your-validator)
  - [Unjail your validator](#unjail-your-validator)
  - [Delegate tokens to your validator](#delegate-tokens-to-your-validator)
  - [Get your p2p peer address](#get-your-p2p-peer-address)
  - [Edit your validator](#edit-your-validator)
  - [Send tokens between wallets](#send-tokens-between-wallets)
  - [Query your wallet balance](#query-your-wallet-balance)
  - [Monitor server load](#monitor-server-load)
  - [Query active validators](#query-active-validators)
  - [Query inactive validators](#query-inactive-validators)
  - [Check logs of the node](#check-logs-of-the-node)
  - [Restart the node](#restart-the-node)
  - [Stop the node](#stop-the-node)
  - [Delete the node from the server](#delete-the-node-from-the-server)
  - [Example gRPC usage](#example-grpc-usage)
  - [Example REST API query](#example-rest-api-query)

## Hardware requirements
```py
- Memory: 16 GB RAM
- CPU: 4 cores
- Disk: 1 TB SSD
- Bandwidth: 1 Gbps
- Linux amd64 arm64 (Ubuntu LTS release)
```
## TrustedPoint Services

| Parameter | Value
|-|-
| indexing | kv
| pruning | custom (100/17)
| min-retain-blocks | 0
| snapshot-interval | 2000
| snapshot-keep-recent | 2
| minimum-gas-prices | 0.15uinit

---
- RPC: https://rpc-initia-testnet.trusted-point.com:443
- REST API: https://rpc-initia-testnet.trusted-point.com:443
- WSS: wss://rpc-initia-testnet.trusted-point.com:443/websocket
- P2P Persistent Peer: a63a6f6eae66b5dce57f5c568cdb0a79923a4e18@peer-initia-testnet.trusted-point.com:26628
---
- State sync: [Guide](#state-sync)
- Fresh Snapshot: [URL](https://rpc-initia-testnet.trusted-point.com/latest_snapshot.tar.lz4) / [Guide](#download-snapshot) **(Being updated every 10 hours)**
- Fresh addrbook: [URL](https://rpc-initia-testnet.trusted-point.com/addrbook.json) / [Guide](#download-fresh-addrbookjson) **(Being updated every 5 minutes)**
- Live Peers scanner: [URL](https://rpc-initia-testnet.trusted-point.com/peers.txt) / [Guide](#add-fresh-persistent-peers) **(Being updated every 5 minutes)**

## Installation guide

### 1. Install required packages
```bash
sudo apt update && \
sudo apt install curl git jq build-essential gcc unzip wget lz4 -y
```
### 2. Install Go
```bash
cd $HOME && \
ver="1.22.0" && \
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz" && \
sudo rm -rf /usr/local/go && \
sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz" && \
rm "go$ver.linux-amd64.tar.gz" && \
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bash_profile && \
source $HOME/.bash_profile && \
go version
```
### 3. Install `initia` binary
```bash
git clone https://github.com/initia-labs/initia.git
cd initia
git checkout v0.2.14
make install
initiad version
```
### 4. Set up variables
```bash
# Customize if you need
echo 'export MONIKER="My_Node"' >> ~/.bash_profile
echo 'export CHAIN_ID="initiation-1"' >> ~/.bash_profile
echo 'export WALLET_NAME="wallet"' >> ~/.bash_profile
echo 'export RPC_PORT="26657"' >> ~/.bash_profile
source $HOME/.bash_profile
```
### 5. Initialize the node
```bash
cd $HOME
initiad init $MONIKER --chain-id $CHAIN_ID
initiad config set client chain-id $CHAIN_ID
initiad config set client node tcp://localhost:$RPC_PORT
initiad config set client keyring-backend os # You can set it to "test" so you will not be asked for a password
```
### 6. Download genesis.json
```bash
wget https://initia.s3.ap-southeast-1.amazonaws.com/initiation-1/genesis.json -O $HOME/.initia/config/genesis.json
```
### 7. Add seeds and peers to the config.toml
```bash
PEERS="e3ac92ce5b790c76ce07c5fa3b257d83a517f2f6@178.18.251.146:30656,2692225700832eb9b46c7b3fc6e4dea2ec044a78@34.126.156.141:26656,2a574706e4a1eba0e5e46733c232849778faf93b@84.247.137.184:53456,40d3f977d97d3c02bd5835070cc139f289e774da@168.119.10.134:26313,1f6633bc18eb06b6c0cab97d72c585a6d7a207bc@65.109.59.22:25756,4a988797d8d8473888640b76d7d238b86ce84a2c@23.158.24.168:26656,e3679e68616b2cd66908c460d0371ac3ed7795aa@176.34.17.102:26656,d2a8a00cd5c4431deb899bc39a057b8d8695be9e@138.201.37.195:53456,329227cf8632240914511faa9b43050a34aa863e@43.131.13.84:26656,517c8e70f2a20b8a3179a30fe6eb3ad80c407c07@37.60.231.212:26656,07632ab562028c3394ee8e78823069bfc8de7b4c@37.27.52.25:19656,028999a1696b45863ff84df12ebf2aebc5d40c2d@37.27.48.77:26656,3c44f7dbb473fee6d6e5471f22fa8d8095bd3969@185.219.142.137:53456,8db320e665dbe123af20c4a5c667a17dc146f4d0@51.75.144.149:26656,c424044f3249e73c050a7b45eb6561b52d0db456@158.220.124.183:53456,767fdcfdb0998209834b929c59a2b57d474cc496@207.148.114.112:26656,edcc2c7098c42ee348e50ac2242ff897f51405e9@65.109.34.205:36656,140c332230ac19f118e5882deaf00906a1dba467@185.219.142.119:53456,4eb031b59bd0210481390eefc656c916d47e7872@37.60.248.151:53456,ff9dbc6bb53227ef94dc75ab1ddcaeb2404e1b0b@178.170.47.171:26656,ffb9874da3e0ead65ad62ac2b569122f085c0774@149.28.134.228:26656" && \
SEEDS="2eaa272622d1ba6796100ab39f58c75d458b9dbc@34.142.181.82:26656,c28827cb96c14c905b127b92065a3fb4cd77d7f6@testnet-seeds.whispernode.com:25756" && \
sed -i \
    -e "s/^seeds *=.*/seeds = \"$SEEDS\"/" \
    -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" \
    "$HOME/.initia/config/config.toml"
```
### 8. Change ports (Optional)
```bash
# Customize if you need
EXTERNAL_IP=$(wget -qO- eth0.me) \
PROXY_APP_PORT=26658 \
P2P_PORT=26656 \
PPROF_PORT=6060 \
API_PORT=1317 \
GRPC_PORT=9090 \
GRPC_WEB_PORT=9091
```
```bash
sed -i \
    -e "s/\(proxy_app = \"tcp:\/\/\)\([^:]*\):\([0-9]*\).*/\1\2:$PROXY_APP_PORT\"/" \
    -e "s/\(laddr = \"tcp:\/\/\)\([^:]*\):\([0-9]*\).*/\1\2:$RPC_PORT\"/" \
    -e "s/\(pprof_laddr = \"\)\([^:]*\):\([0-9]*\).*/\1localhost:$PPROF_PORT\"/" \
    -e "/\[p2p\]/,/^\[/{s/\(laddr = \"tcp:\/\/\)\([^:]*\):\([0-9]*\).*/\1\2:$P2P_PORT\"/}" \
    -e "/\[p2p\]/,/^\[/{s/\(external_address = \"\)\([^:]*\):\([0-9]*\).*/\1${EXTERNAL_IP}:$P2P_PORT\"/; t; s/\(external_address = \"\).*/\1${EXTERNAL_IP}:$P2P_PORT\"/}" \
    $HOME/.initia/config/config.toml
```
```bash
sed -i \
    -e "/\[api\]/,/^\[/{s/\(address = \"tcp:\/\/\)\([^:]*\):\([0-9]*\)\(\".*\)/\1\2:$API_PORT\4/}" \
    -e "/\[grpc\]/,/^\[/{s/\(address = \"\)\([^:]*\):\([0-9]*\)\(\".*\)/\1\2:$GRPC_PORT\4/}" \
    -e "/\[grpc-web\]/,/^\[/{s/\(address = \"\)\([^:]*\):\([0-9]*\)\(\".*\)/\1\2:$GRPC_WEB_PORT\4/}" \
    $HOME/.initia/config/app.toml
```
### 9. Configure prunning to save storage (Optional)
```bash
sed -i \
    -e "s/^pruning *=.*/pruning = \"custom\"/" \
    -e "s/^pruning-keep-recent *=.*/pruning-keep-recent = \"100\"/" \
    -e "s/^pruning-interval *=.*/pruning-interval = \"10\"/" \
    "$HOME/.initia/config/app.toml"
```
### 10. Set min gas price 
```bash
sed -i -e "s/^minimum-gas-prices *=.*/minimum-gas-prices = \"0.15uinit,0.01uusdc\"/" $HOME/.initia/config/app.toml
```
### 11. Enable indexer (Optional)
```bash
sed -i "s/^indexer *=.*/indexer = \"kv\"/" $HOME/.initia/config/config.toml
```
### 12. Create a service file
```bash
sudo tee /etc/systemd/system/initiad.service > /dev/null <<EOF
[Unit]
Description=Initia Node
After=network.target

[Service]
User=$USER
Type=simple
ExecStart=$(which initiad) start --home $HOME/.initia
Restart=on-failure
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
```
### 13. Start the node
```bash
sudo systemctl daemon-reload && \
sudo systemctl enable initiad && \
sudo systemctl restart initiad && \
sudo journalctl -u initiad -f -o cat
```
P.S. Consider [downloading snapshot](#download-snapshot) or using [state-sync](#state-sync) for the quick sync.

### 14. Create a wallet for your validator
```bash
initiad keys add $WALLET_NAME

# DO NOT FORGET TO SAVE THE SEED PHRASE
# You can add --recover flag to restore existing key instead of creating
```
### 15. Request tokens from the faucet on Discord
-> <a href="https://faucet.testnet.initia.xyz/"><font size="4"><b><u>FAUCET</u></b></font></a> <-
### 16. Check wallet balance
Make sure your node is fully synced unless it won't work.
```bash
initiad status | jq -r .sync_info
```
```bash
initiad q bank balances $(initiad keys show $WALLET_NAME -a) 
```
### 17. Create a validator
```bash
initiad tx mstaking create-validator \
  --amount=1000000uinit \
  --pubkey=$(initiad tendermint show-validator) \
  --moniker=$MONIKER \
  --chain-id=$CHAIN_ID \
  --commission-rate=0.05 \
  --commission-max-rate=0.10 \
  --commission-max-change-rate=0.01 \
  --from=$WALLET_NAME \
  --identity="" \
  --website="" \
  --details="Initia to the moon!" \
  --gas=2000000 --fees=300000uinit \
  -y
```
Do not forget to save `priv_validator_key.json` file located in $HOME/.initia/config/

## State sync

### 1. Stop the node
```bash
sudo systemctl stop initiad
```
### 2. Backup priv_validator_state.json 
```bash
cp $HOME/.initia/data/priv_validator_state.json $HOME/.initia/priv_validator_state.json.backup
```
### 3. Reset DB
```bash
initiad tendermint unsafe-reset-all --home $HOME/.initia --keep-addr-book
```
### 4. Setup required variables (One command)
```bash
PEERS="a63a6f6eae66b5dce57f5c568cdb0a79923a4e18@peer-initia-testnet.trusted-point.com:26628" && \
RPC="https://rpc-initia-testnet.trusted-point.com:443" && \
LATEST_HEIGHT=$(curl -s --max-time 3 --retry 2 --retry-connrefused $RPC/block | jq -r .result.block.header.height) && \
TRUST_HEIGHT=$((LATEST_HEIGHT - 1500)) && \
TRUST_HASH=$(curl -s --max-time 3 --retry 2 --retry-connrefused "$RPC/block?height=$TRUST_HEIGHT" | jq -r .result.block_id.hash) && \

if [ -n "$PEERS" ] && [ -n "$RPC" ] && [ -n "$LATEST_HEIGHT" ] && [ -n "$TRUST_HEIGHT" ] && [ -n "$TRUST_HASH" ]; then
    sed -i.bak \
        -e "/\[statesync\]/,/^\[/{s/\(enable = \).*$/\1true/}" \
        -e "/^rpc_servers =/ s|=.*|= \"$RPC,$RPC\"|;" \
        -e "/^trust_height =/ s/=.*/= $TRUST_HEIGHT/;" \
        -e "/^trust_hash =/ s/=.*/= \"$TRUST_HASH\"/" \
        -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" \
        $HOME/.initia/config/config.toml
    echo -e "\nLATEST_HEIGHT: $LATEST_HEIGHT\nTRUST_HEIGHT: $TRUST_HEIGHT\nTRUST_HASH: $TRUST_HASH\nPEERS: $PEERS\n\nALL IS FINE"
else
    echo -e "\nError: One or more variables are empty. Please try again or change RPC\nExiting...\n"
fi
```
### 4. Move priv_validator_state.json back
```bash
mv $HOME/.initia/priv_validator_state.json.backup $HOME/.initia/data/priv_validator_state.json
```
### 5. Start the node
```bash
sudo systemctl restart initiad && sudo journalctl -u initiad -f -o cat
```
You should see the following logs. It may take up to 5 minutes for the snapshot to be discovered. If doesn't work, try downloading [snapshot](#download-snapshot)
```py
2:39PM INF sync any module=statesync msg="Discovering snapshots for 15s" server=node
2:39PM INF Discovered new snapshot format=3 hash="?^��I��\r�=�O�E�?�CQD�6�\x18�F:��\x006�" height=602000 module=statesync server=node
2:39PM INF Discovered new snapshot format=3 hash="%���\x16\x03�T0�v�f�C��5�<TlLb�5��l!�M" height=600000 module=statesync server=node
2:42PM INF VerifyHeader hash=CFC07DAB03CEB02F53273F5BDB6A7C16E6E02535B8A88614800ABA9C705D4AF7 height=602001 module=light server=node
```
After some time you should see the following logs. It make take 5 minutes for the node to catch up the rest of the blocks
```py
2:43PM INF indexed block events height=602265 module=txindex server=node
2:43PM INF executed block height=602266 module=state num_invalid_txs=0 num_valid_txs=0 server=node
2:43PM INF commit synced commit=436F6D6D697449447B5B31313720323535203139203132392031353920313035203136352033352031353320313220353620313533203139352031372036342034372033352034372032333220373120313939203720313734203620313635203338203336203633203235203136332039203134395D3A39333039417D module=server
2:43PM INF committed state app_hash=75FF13819F69A523990C3899C311402F232FE847C707AE06A526243F19A30995 height=602266 module=state num_txs=0 server=node
2:43PM INF indexed block events height=602266 module=txindex server=node
2:43PM INF executed block height=602267 module=state num_invalid_txs=0 num_valid_txs=0 server=node
2:43PM INF commit synced commit=436F6D6D697449447B5B323437203134322032342031313620323038203631203138362032333920323238203138312032333920313039203336203420383720323238203236203738203637203133302032323220313431203438203337203235203133302037302032343020313631203233372031312036365D3A39333039427D module=server
```
### 6. Check the synchronization status
```bash
initiad status | jq -r .sync_info
```
### 7. Disable state sync
```bash
sed -i.bak -e "/\[statesync\]/,/^\[/{s/\(enable = \).*$/\1false/}" $HOME/.initia/config/app.toml
```
## Download fresh addrbook.json

### 1. Stop the node and use `wget` to download the file
```bash
sudo systemctl stop initiad && \
wget -O $HOME/.initia/config/addrbook.json https://rpc-initia-testnet.trusted-point.com/addrbook.json
```
### 2. Restart the node
```bash
sudo systemctl restart initiad && sudo journalctl -u initiad -f -o cat
```
### 3. Check the synchronization status
```bash
initiad status | jq -r .sync_info
```
The file is being updated every 5 minutes

## Add fresh persistent peers

### 1. Extract persistent_peers from our endpoint
```bash
PEERS=$(curl -s --max-time 3 --retry 2 --retry-connrefused "https://rpc-initia-testnet.trusted-point.com/peers.txt")
if [ -z "$PEERS" ]; then
    echo "No peers were retrieved from the URL."
else
    echo -e "\nPEERS: "$PEERS""
    sed -i "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" "$HOME/.initia/config/config.toml"
    echo -e "\nConfiguration file updated successfully.\n"
fi
```
### 2. Restart the node
```bash
sudo systemctl restart initiad && sudo journalctl -u initiad -f -o cat
```
### 3. Check the synchronization status
```bash
initiad status | jq -r .sync_info
```
Peers are being updated every 5 minutes

## Download Snapshot

### 1. Download latest snapshot from our endpoint
```bash
wget https://rpc-initia-testnet.trusted-point.com/latest_snapshot.tar.lz4 -O latest_snapshot.tar.lz4
```
### 2. Stop the node
```bash
sudo systemctl stop initiad
```
### 3. Backup priv_validator_state.json 
```bash
cp $HOME/.initia/data/priv_validator_state.json $HOME/.initia/priv_validator_state.json.backup
```
### 4. Reset DB
```bash
initiad tendermint unsafe-reset-all --home $HOME/.initia --keep-addr-book
```
### 5. Extract files fromt the arvhive 
```bash
lz4 -d -c ./latest_snapshot.tar.lz4 | tar -xf - -C $HOME/.initia
```
### 6. Move priv_validator_state.json back
```bash
mv $HOME/.initia/priv_validator_state.json.backup $HOME/.initia/data/priv_validator_state.json
```
### 7. Restart the node
```bash
sudo systemctl restart initiad && sudo journalctl -u initiad -f -o cat
```
### 8. Check the synchronization status
```bash
initiad status | jq -r .sync_info
```
Snapshot is being updated every 3 hours

## Useful commands
### Check node status 
```bash
initiad status | jq
```
### Query your validator
```bash
initiad q mstaking validator $(initiad keys show $WALLET_NAME --bech val -a) 
```
### Query missed blocks counter & jail details of your validator
```bash
initiad q slashing signing-info $(initiad tendermint show-validator)
```
### Unjail your validator 
```bash
initiad tx slashing unjail --from $WALLET_NAME --gas=2000000 --fees=300000uinit -y
```
### Delegate tokens to your validator 
```bash 
initiad tx mstaking delegate $(initiad keys show $WALLET_NAME --bech val -a)  <AMOUNT>uinit --from $WALLET_NAME --gas=2000000 --fees=300000uinit -y
```
### Get your p2p peer address
```bash
initiad status | jq -r '"\(.NodeInfo.id)@\(.NodeInfo.listen_addr)"'
```
### Edit your validator
```bash 
initiad tx mstaking edit-validator --website="<WEBSITE>" --details="<DESCRIPTION>" --moniker="<NEW_MONIKER>" --from=$WALLET_NAME --gas=2000000 --fees=300000uinit -y
```
### Send tokens between wallets 
```bash
initiad tx bank send $WALLET_NAME <TO_WALLET> <AMOUNT>uinit --gas=2000000 --fees=300000uinit -y
```
### Query your wallet balance 
```bash
initiad q bank balances $WALLET_NAME
```
### Monitor server load
```bash 
sudo apt update
sudo apt install htop -y
htop
```
### Query active validators
```bash
initiad q mstaking validators -o json --limit=1000 \
| jq '.validators[] | select(.status=="BOND_STATUS_BONDED")' \
| jq -r '.voting_power + " - " + .description.moniker' \
| sort -gr | nl
```
### Query inactive validators
```bash
initiad q mstaking validators -o json --limit=1000 \
| jq '.validators[] | select(.status=="BOND_STATUS_UNBONDED")' \
| jq -r '.voting_power + " - " + .description.moniker' \
| sort -gr | nl
```
### Check logs of the node
```bash
sudo journalctl -u initiad -f -o cat
```
### Restart the node
```bash
sudo systemctl restart initiad
```
### Stop the node
```bash
sudo systemctl stop initiad
```
### Delete the node from the server
```bash
# !!! IF YOU HAVE CREATED A VALIDATOR, MAKE SURE TO BACKUP `priv_validator_key.json` file located in $HOME/.initia/config/ 
sudo systemctl stop initiad
sudo systemctl disable initiad
sudo rm /etc/systemd/system/initiad.service
rm -rf $HOME/.initia
sudo rm /usr/local/bin/initiad
```
### Example gRPC usage
```bash
wget https://github.com/fullstorydev/grpcurl/releases/download/v1.7.0/grpcurl_1.7.0_linux_x86_64.tar.gz
tar -xvf grpcurl_1.7.0_linux_x86_64.tar.gz
chmod +x grpcurl
./grpcurl  -plaintext  localhost:$GRPC_PORT list
### MAKE SURE gRPC is enabled in app.toml
# grep -A 3 "\[grpc\]" $HOME/.initia/config/app.toml
```
### Example REST API query
```bash
curl localhost:$API_PORT/cosmos/mstaking/v1beta1/validators
### MAKE SURE API is enabled in app.toml
# grep -A 3 "\[api\]" $HOME/.initia/config/app.toml
```

