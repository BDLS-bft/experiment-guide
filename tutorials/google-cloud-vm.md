# Run BDLS-Fabric 
Google-cloud Ubuntu VM

## Step 1
```
sudo apt update && sudo apt upgrade -y

sudo snap install go --classic
sudo apt install jq -y
sudo apt install curl -y

sudo snap install yq
sudo apt install build-essential
```
## Step 2
```
mkdir -p $HOME/go/src/github.com/BDLS-bft/
cd $HOME/go/src/github.com/BDLS-bft/
curl -sSLO https://raw.githubusercontent.com/hyperledger/fabric/main/scripts/install-fabric.sh && chmod +x install-fabric.sh

./install-fabric.sh samples binary

```
## Step 3
```
cd fabric-samples/
yq -i 'del(.chaincode.externalBuilders) | .chaincode.externalBuilders[0].name = "ccaas_builder" | .chaincode.externalBuilders[0].path = env(PWD) + "/builders/ccaas" | .chaincode.externalBuilders[0].propagateEnvironment[0] = "CHAINCODE_AS_A_SERVICE_BUILDER_CONFIG"' config/core.yaml

cd test-network-nano-bash
./configureExternalBuilders.sh
```
## Step 4
```
cd ../..
git clone https://github.com/hyperledger-labs/bdls fabric

cd fabric 
make configtxlator configtxgen cryptogen orderer osnadmin peer discover ledgerutil
```
## Step 5
```
edit Orderer 
 cd fabric-samples/config/
 vi orderer.yaml 
 delete Kafka section
```
*************************
```
vi ~/.bashrc
 export FABRIC_CFG_PATH=${PWD}/../config
source ~/.bashrc

cd ../test-network-nano-bash/
tmux new -s mysession
tmux split-window -v
tmux select-pane -t 0
```

![image](https://github.com/BDLS-bft/experiment-guide/assets/9446035/89b07b97-1abd-4a51-80b2-940744252734)

 





