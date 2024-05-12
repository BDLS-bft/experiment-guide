# Running Fabric-BDLS Experimental 

For reference/Prereqs please check the the readme file in: 
https://github.com/hyperledger/fabric-samples/blob/main/test-network-nano-bash/README.md

# experiment-guide
![image](https://github.com/BDLS-bft/experiment-guide/assets/9446035/ac386ed8-4bbb-4217-8437-ec2e49049dce)

* Please verify Go Environment by run `go env`

![image](https://github.com/BDLS-bft/experiment-guide/assets/9446035/c1505f61-7339-4392-9f00-c37acdb33153)

## Clone the repositories to the work space 
```shell
mkdir -R ~/go/src/github.com/BDLS-bft/
```
1. Clone Fabric repository:
```
git clone https://github.com/BDLS-bft/fabric.git
git checkout branch BDLS-RAFT-TPS-readyc
```
![image](https://github.com/BDLS-bft/experiment-guide/assets/9446035/026e3ca7-101c-4b3e-9565-3690d2c4c108)

2. Clone Test Network repository:
```
git clonehttps://github.com/BDLS-bft/fabric-samples.git
```

# Fabric
## Build new Orderer base on BDLS

navigate to the fabric location the w cloned in `/home/ahmed/go/src/github.com/BDLS-bft/fabric`
```
cd fabric
rm -f build/bin/orderer & make orderer
```
![image](https://github.com/BDLS-bft/experiment-guide/assets/9446035/2c493ea2-fd7d-4009-b65d-580bd4f82fd5)

Verfy the new Orderer binery
* NOTE! make sure you build other binery as listed brlow if you have new environment 

![image](https://github.com/BDLS-bft/experiment-guide/assets/9446035/1e460c03-883f-4ac9-9664-f8cec2754034)

# Fabric-samples
step out the Fabric directory `cd ..`. navigate into fabric-samples `cd fabric-samples`
```
pwd
~/go/src/github.com/BDLS-bft/fabric-samples/
```
We are working on the `/test-network-nano-bash` test network project.

1. Generate the network artifact
```
./generate_artifacts.sh BFT
```
![image](https://github.com/BDLS-bft/experiment-guide/assets/9446035/a689a995-77a7-4bc5-8fbc-cffb833fdd96)

2. Run the Orderer nodes.

open four terminal windows in the directory. rune:
*  `./orderer1.sh BFT` in terminal one
*  `./orderer2.sh BFT` in terminal two
*  `./orderer3.sh BFT` in terminal three
*  `./orderer4.sh BFT` in terminal four

![image](https://github.com/BDLS-bft/experiment-guide/assets/9446035/03dca8fe-3e19-4095-9052-c7c9a251f079)

The terminals output should look like this:
![image](https://github.com/BDLS-bft/experiment-guide/assets/9446035/89438f21-f4d3-473a-9cea-f3d08d6d9870)

Keep the four terminals running, we will continue work in other terminal.

3. Join the network
open new terminal window and type this commend to join the Orderers nodes.
```
./join_orderers.sh BFT
```
![image](https://github.com/BDLS-bft/experiment-guide/assets/9446035/89a45eec-f566-4865-b141-93ae03139f16)


The benchmark test will trigger automaticly, navigate to the Orderers four windows 

![image](https://github.com/BDLS-bft/experiment-guide/assets/9446035/3e947eab-2b20-4f2e-b0bc-78ce83c7612f)


To change the Configuring the fabric sample network to run the network, in the `configtx.yaml` located in the `bft-config`, as `fabric-samples/test-network-nano-bash/bft-config`
```
test-network-nano-bash/bft-config/configtx.yaml
```
![image](https://github.com/BDLS-bft/experiment-guide/assets/9446035/42883214-956b-40ba-9651-431c17ef7e68)

