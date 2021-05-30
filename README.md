# HyperLedger Fabric 1.4 'minimal' setup (one organization, one peer, one ca, one orderer)

This repo is created mostly for educational/practicing purposes, as the demo for the [Hyperledger Fabric and SoftEthic DevOps Tools: some practices for dedicated Hyperledger Organization setup](https://blog.softethic.com/hyperledger-fabric-and-softethic-devops-tools/) article, so it does not include `Installer`, `Gateway` SEDOT services.

## Binaries installation
You must have `cryptogen` and `configtxgen` tools installed, the easiest way is to take those we have attached (the `tools` folder):

```shell
sudo cp tools/cryptogen /usr/bin/
sudo cp tools/configtxgen /usr/bin/
```

## Organization setup
We create volumes for all Hyperledger Fabric data at /var/sedot/ but you can use your own volumes structure if you need, just edit those `volumes` sections of `docker-compose.yml` file.

1. Build crypto-materials, genesis block and channel transactions:
```shell
sudo ./build.sh
```
2. Start organization, create channel and join peer on it.
```shell
sudo ./create.sh
```
Done!

## Check if peer has joined the channel
Enter the peer container:
```shell
sudo docker exec -it peer0.org1.example.com bash
```
Check the channels list:
```shell
peer channel list
```
NOTICE, the channel name is `channel` (not `mychannel` as it is usually used in tutorials). 

## Other useful scripts
We have added more scripts along with `build.sh` and `create` sh:
- `start.sh` - starts your containers
- `stop.sh`  - stops those
- `redeploy.sh` - completely kills everything, including data volumes and installs everything from scratch.
- `clean.sh` - part of the previous script, stops and removes everything

If you are interested in getting more information about SEDOT - feel free to visit our [SoftEthic DevOps Tools site](https://softethic.com/) and [SoftEthic Blog](https://blog.softethic.com/).


