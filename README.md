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

## Build new Orderer base on BDLS
```
cd fabric
rm -f build/bin/orderer & make orderer
```
![image](https://github.com/BDLS-bft/experiment-guide/assets/9446035/2c493ea2-fd7d-4009-b65d-580bd4f82fd5)

Verfy the new Orderer binery
* NOTE! make sure you build other binery as listed brlow if you have new environment 

![image](https://github.com/BDLS-bft/experiment-guide/assets/9446035/1e460c03-883f-4ac9-9664-f8cec2754034)


