HTMLCOINCORE Node
============

A HTMLCOIN full node for building applications and services with Node.js. A node is extensible and can be configured to run additional services.

## Install

```bash
npm install -g htmlcoincore-node
htmlcoincore-node start
```

## Configuration

HTMLCOINCORE includes a Command Line Interface (CLI) for managing, configuring and interfacing with your HTMLCOINCORE Node.

```bash
htmlcoincore-node create -d <data-dir> mynode
cd mynode
htmlcoincore-node install <service>
htmlcoincore-node install https://github.com/yourname/helloworld
```

This will create a directory with configuration files for your node and install the necessary dependencies. For more information about (and developing) services, please see the [Service Documentation](docs/services.md).

## Add-on Services

There are several add-on services available to extend the functionality of HTMLCOINCORE:

- [HTMLCOIN Insight API](https://github.com/HTMLCOIN/htmlcoin-api)
- [HTMLCOIN Explorer](https://github.com/HTMLCOIN/htmlcoin-explorer)

## Contributing



## License
