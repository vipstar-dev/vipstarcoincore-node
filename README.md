VIPSTARCOINCORE Node
============

A VIPSTARCOIN full node for building applications and services with Node.js. A node is extensible and can be configured to run additional services.

## Install

```bash
npm install -g vipstarcoincore-node
vipstarcoincore-node start
```

## Configuration

VIPSTARCOINCORE includes a Command Line Interface (CLI) for managing, configuring and interfacing with your VIPSTARCOINCORE Node.

```bash
vipstarcoincore-node create -d <data-dir> mynode
cd mynode
vipstarcoincore-node install <service>
vipstarcoincore-node install https://github.com/yourname/helloworld
```

This will create a directory with configuration files for your node and install the necessary dependencies. For more information about (and developing) services, please see the [Service Documentation](docs/services.md).

## Add-on Services

There are several add-on services available to extend the functionality of VIPSTARCOINCORE:

- [VIPSTARCOIN Insight API](https://github.com/VIPSTARCOIN/vipstarcoin-api)
- [VIPSTARCOIN Explorer](https://github.com/VIPSTARCOIN/vipstarcoin-explorer)

## Contributing



## License
