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
```
## Step 6 
(Running the experimental)

* We need at least 5 terminals to run the experimental.
Running the comment from the diffrent terminals or tmux new session and splite the screen.
Tew options a or b.
```
cd ../test-network-nano-bash/
```
a.
- In the first orderer terminal, run `./generate_artifacts.sh BFT` to generate crypto material (calls cryptogen) and application channel genesis block and configuration transactions (calls configtxgen). The artifacts will be created in the `crypto-config` and `channel-artifacts` directories.
- In the four orderer terminals, run `./orderer1.sh`, `./orderer2.sh`, `./orderer3.sh`, `./orderer4.sh` respectively.
- Note that each orderer and peer write their data (including their ledgers) to their own subdirectory under the `data` directory
- Open a different terminal and run `./join_orderers.sh BFT`.

b.
`tmux` use to create new session then split till you get five sessions.

```
tmux new -s mysession
tmux split-window -v
tmux select-pane -t 0
```
The uses like:
```
./generate_artifacts.sh BFT
./orderer1.sh & tmux select-pane -t 1
./orderer2.sh & tmux select-pane -t 2
./orderer3.sh & tmux select-pane -t 3
./orderer4.sh & tmux select-pane -t 4
./join_orderers.sh BFT
```

![image](https://github.com/BDLS-bft/experiment-guide/assets/9446035/89b07b97-1abd-4a51-80b2-940744252734)

 





