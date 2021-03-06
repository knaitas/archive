---
title: Storj  Decentralized Cloud Object Storage
summary: Storj is an open-source protocol and network for decentralized cloud object storage with client-side encryption This article originally appeared in the Storj wiki Storj Test Network The storj-sim tool enables you to run all the components of the Storj network (Satellite, Storage Nodes, Console and Gateway) and test them on your local machine. In every day Storj usage, the Satellite, Storage Node, and Uplink are run on separate servers and computers, but for the purposes of the test network, all
authors:
  - Kauri Team (@kauri)
date: 2019-05-15
some_url: 
---

# Storj  Decentralized Cloud Object Storage

![](https://ipfs.infura.io/ipfs/QmXS1sVX9Fyq3X137dW5KYw8hqtNwPyZLvkv9w3HwCytiA)


> Storj is an open-source protocol and network for decentralized cloud object storage with client-side encryption

_This article originally appeared in the [Storj wiki](https://github.com/storj/storj/wiki)_

## Storj Test Network

The `storj-sim` tool enables you to run all the components of the Storj network (Satellite, Storage Nodes, Console and Gateway) and test them on your local machine.

![](https://ipfs.infura.io/ipfs/QmYvsEQznkm9cdkKh7Q1eQ9AdmqFEtREDswUbbKmnowGkQ)

In every day Storj usage, the Satellite, Storage Node, and Uplink are run
on separate servers and computers, but for the purposes of the test network,
all of the components are run locally.

## Installation and configuration

First, you'll need at least [Go 1.11](https://www.golang.org/). Once Go is
installed run:

```bash
git clone https://github.com/storj/storj.git storj
cd storj
make install-sim
```

_Ensure that `storj` folder is outside of `GOPATH`, otherwise you may see errors._

This will install the storj-sim satellite storage node gateway and uplink binaries to wherever Go is configured to output binaries on your system. By default, this is `~/go/bin`.


Next, run setup:

```bash
storj-sim network setup
```

You now have a configured Storj test network with default configuration options.

You might also want to take a look at the config by navigating to the root 
directory `--config-dir` where all the configs are specified.
You can tweak the configuration settings there as needed.

For insight into what is happening under the hood you can use `-x` or `--print-commands` to see how the processes are started.

The next step is to run it!

## Running the test network

Now that the configuration has been completed, we can fire up the test network with:

```bash
storj-sim network run
```

Your test network is now running. You should see output containing your
Amazon S3 gateway access and secret keys, which you will need to connect
Amazon S3 compatible clients.

At the moment it's assinging ports in the following way:

* Gateways start from port `9000`
* Bootstrap server is at port `9999`
* Satellites start from port `10000`
* Satellite Console starts on port `10100`
* Storage Nodes public ports start from port `12000`
* Storage Nodes private ports start from port `13000`

To get access to a gateway and test your keys, you open http://127.0.0.1:9000 in a web browser.

You can access a storage node dashboard using the storage command. For example for accessing storage node 4 dashboard using the default configuration:
```bash
storagenode dashboard --config-dir ~/.local/share/storj/local-network/storagenode/4/ --identity-dir ~/.local/share/storj/local-network/storagenode/4 --address :13004 --color
```

#### Running Tests

`storj-sim network test <command>` can be used to run tests.

`storj-sim` will start up the network and once it's up and running it will execute the specified `<command>`.

The information about the network is exposed via environment flags. All the flags start with a prefix and an index.

* Address: `STORAGENODE_0_ADDR`, `SATELLITE_0_ADDR`, `GATEWAY_0_ADDR`
* Keys: `GATEWAY_0_ACCESS_KEY`, `GATEWAY_0_SECRET_KEY`
* Directory: `STORAGENODE_0_DIR`, `SATELLITE_0_DIR`, `GATEWAY_0_DIR`

You can obtain the list of environment flags by running:
```bash
storj-sim network env
```

For a real-world example you can take a look in [test-sim.sh](https://github.com/storj/storj/blob/master/scripts/test-sim.sh) and [test-sim-aws.sh](https://github.com/storj/storj/blob/master/scripts/test-sim-aws.sh).

#### Wiping the Testnet

`storj-sim network destroy` can be used to wipe the network easily.

While developing it's often nice to be able to delete the network and set it up from scratch.

For convenience, you may run the command in a single line, like so:

`storj-sim network destroy && storj-sim network setup && storj-sim network test bash my-test-script.sh`

***

### Next Steps
Please see the [Uplink CLI](https://github.com/storj/docs/blob/master/Uplink-CLI.md) or [S3 Gateway](https://github.com/storj/docs/blob/master/S3-Gateway.md)
tutorial for how to upload and download data to the test network.

Let's 'be the cloud' and decentralize all the things together!


---

- **Kauri original title:** Storj  Decentralized Cloud Object Storage
- **Kauri original link:** https://kauri.io/storj-decentralized-cloud-object-storage/a585dad1cd354e49994f3235452a8bb1/a
- **Kauri original author:** Kauri Team (@kauri)
- **Kauri original Publication date:** 2019-05-15
- **Kauri original tags:** storage
- **Kauri original hash:** QmYvQt1cw5iUPULTdqu1s61dBm1uAoEZhKTurTWFL3DEcF
- **Kauri original checkpoint:** Qmekp5iiDi5N5M4KdtAVGBEJEF3ahMgWYZJqL7s1qmkQ9g



