# Setting up Development Environment

## Install Node.js

Install Node.js by your favorite method, or use Node Version Manager by following directions at https://github.com/creationix/nvm

```bash
nvm install v4
```

## Fork and Download Repositories

To develop vipstarcoincore-node:

```bash
cd ~
git clone git@github.com:<yourusername>/vipstarcoincore-node.git
git clone git@github.com:<yourusername>/vipstarcoin-lib.git
```

To develop vipstarcoin or to compile from source:

```bash
git clone git@github.com:<yourusername>/vipstarcoin.git
git fetch origin <branchname>:<branchname>
git checkout <branchname>
```
**Note**: See vipstarcoin documentation for building vipstarcoin on your platform.


## Install Development Dependencies

For Ubuntu:
```bash
sudo apt-get install libzmq3-dev
sudo apt-get install build-essential
```
**Note**: Make sure that libzmq-dev is not installed, it should be removed when installing libzmq3-dev.


For Mac OS X:
```bash
brew install zeromq
```

## Install and Symlink

```bash
cd bitcore-lib
npm install
cd ../bitcore-node
npm install
```
**Note**: If you get a message about not being able to download vipstarcoin distribution, you'll need to compile vipstarcoind from source, and setup your configuration to use that version.


We now will setup symlinks in `vipstarcoincore-node` *(repeat this for any other modules you're planning on developing)*:
```bash
cd node_modules
rm -rf vipstarcoin-lib
ln -s ~/vipstarcoin-lib
rm -rf vipstarcoind-rpc
ln -s ~/vipstarcoind-rpc
```

And if you're compiling or developing vipstarcoin:
```bash
cd ../bin
ln -sf ~/vipstarcoin/src/vipstarcoind
```

## Run Tests

If you do not already have mocha installed:
```bash
npm install mocha -g
```

To run all test suites:
```bash
cd vipstarcoincore-node
npm run regtest
npm run test
```

To run a specific unit test in watch mode:
```bash
mocha -w -R spec test/services/vipstarcoind.unit.js
```

To run a specific regtest:
```bash
mocha -R spec regtest/vipstarcoind.js
```

## Running a Development Node

To test running the node, you can setup a configuration that will specify development versions of all of the services:

```bash
cd ~
mkdir devnode
cd devnode
mkdir node_modules
touch vipstarcoincore-node.json
touch package.json
```

Edit `vipstarcoincore-node.json` with something similar to:
```json
{
  "network": "livenet",
  "port": 3001,
  "services": [
    "vipstarcoind",
    "web",
    "vipstarcoin-api",
    "insight-ui",
    "<additional_service>"
  ],
  "servicesConfig": {
    "vipstarcoind": {
      "spawn": {
        "datadir": "/home/<youruser>/.vipstarcoin",
        "exec": "/home/<youruser>/vipstarcoin/src/vipstarcoind"
      }
    }
  }
}
```

**Note**: To install services [vipstarcoin-api](https://github.com/VIPSTARCOIN/vipstarcoin-api) and [vipstarcoin-explorer](https://github.com/VIPSTARCOIN/vipstarcoin-explorer) you'll need to clone the repositories locally.

Setup symlinks for all of the services and dependencies:

```bash
cd node_modules
ln -s ~/vipstarcoin-lib
ln -s ~/vipstarcoincore-node
ln -s ~/vipstarcoin-api
ln -s ~/vipstarcoin-explorer
```

Make sure that the `<datadir>/vipstarcoin.conf` has the necessary settings, for example:
```
server=1
whitelist=127.0.0.1
txindex=1
addressindex=1
timestampindex=1
spentindex=1
zmqpubrawtx=tcp://127.0.0.1:28332
zmqpubhashblock=tcp://127.0.0.1:28332
rpcallowip=127.0.0.1
rpcuser=user
rpcpassword=password
rpcport=31915
reindex=1
gen=0
addrindex=1
logevents=1
```

From within the `devnode` directory with the configuration file, start the node:
```bash
../vipstarcoincore-node/bin/vipstarcoincore-node start
```
