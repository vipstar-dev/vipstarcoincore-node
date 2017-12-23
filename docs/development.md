# Setting up Development Environment

## Install Node.js

Install Node.js by your favorite method, or use Node Version Manager by following directions at https://github.com/creationix/nvm

```bash
nvm install v4
```

## Fork and Download Repositories

To develop htmlcoincore-node:

```bash
cd ~
git clone git@github.com:<yourusername>/htmlcoincore-node.git
git clone git@github.com:<yourusername>/htmlcoin-lib.git
```

To develop htmlcoin or to compile from source:

```bash
git clone git@github.com:<yourusername>/htmlcoin.git
git fetch origin <branchname>:<branchname>
git checkout <branchname>
```
**Note**: See htmlcoin documentation for building htmlcoin on your platform.


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
**Note**: If you get a message about not being able to download htmlcoin distribution, you'll need to compile htmlcoind from source, and setup your configuration to use that version.


We now will setup symlinks in `htmlcoincore-node` *(repeat this for any other modules you're planning on developing)*:
```bash
cd node_modules
rm -rf htmlcoin-lib
ln -s ~/htmlcoin-lib
rm -rf htmlcoind-rpc
ln -s ~/htmlcoind-rpc
```

And if you're compiling or developing htmlcoin:
```bash
cd ../bin
ln -sf ~/htmlcoin/src/htmlcoind
```

## Run Tests

If you do not already have mocha installed:
```bash
npm install mocha -g
```

To run all test suites:
```bash
cd htmlcoincore-node
npm run regtest
npm run test
```

To run a specific unit test in watch mode:
```bash
mocha -w -R spec test/services/htmlcoind.unit.js
```

To run a specific regtest:
```bash
mocha -R spec regtest/htmlcoind.js
```

## Running a Development Node

To test running the node, you can setup a configuration that will specify development versions of all of the services:

```bash
cd ~
mkdir devnode
cd devnode
mkdir node_modules
touch htmlcoincore-node.json
touch package.json
```

Edit `htmlcoincore-node.json` with something similar to:
```json
{
  "network": "livenet",
  "port": 3001,
  "services": [
    "htmlcoind",
    "web",
    "htmlcoin-api",
    "insight-ui",
    "<additional_service>"
  ],
  "servicesConfig": {
    "htmlcoind": {
      "spawn": {
        "datadir": "/home/<youruser>/.htmlcoin",
        "exec": "/home/<youruser>/htmlcoin/src/htmlcoind"
      }
    }
  }
}
```

**Note**: To install services [htmlcoin-api](https://github.com/HTMLCOIN/htmlcoin-api) and [htmlcoin-explorer](https://github.com/HTMLCOIN/htmlcoin-explorer) you'll need to clone the repositories locally.

Setup symlinks for all of the services and dependencies:

```bash
cd node_modules
ln -s ~/htmlcoin-lib
ln -s ~/htmlcoincore-node
ln -s ~/htmlcoin-api
ln -s ~/htmlcoin-explorer
```

Make sure that the `<datadir>/htmlcoin.conf` has the necessary settings, for example:
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
rpcport=18332
reindex=1
gen=0
addrindex=1
logevents=1
```

From within the `devnode` directory with the configuration file, start the node:
```bash
../htmlcoincore-node/bin/htmlcoincore-node start
```