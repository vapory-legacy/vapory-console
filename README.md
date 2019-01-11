# vapory-console

Commandline console for Vapory nodes.

`vapconsole` connects to an Vapory node running in the background (tested with vap and gvap) via IPC
and provides an interactive javascript console containing the `web3` object with admin additions.

Note that the admin additions are not yet official and may change any time.

## Installation / Usage

    # npm install -g vapory-console
    npm http GET https://registry.npmjs.org/vapory-console
    npm http 304 https://registry.npmjs.org/vapory-console
    npm http GET https://registry.npmjs.org/web3
    ...
    # vapconsole
    Connecting to node at /home/user/.vapory/gvap.ipc
    Connection successful.
    Current block number: 1083107
    Entering interactive mode.
    > web3.admin.getNodeInfo(function(err, info) { console.log(info.name); } )
    vap/v1.2.0-2192c209/Debug-Linux/clang/int

## Usage of the Test Interface

vapconsole provides access to the cpp-vapory test interface, which can
be used to test smart contracts that depend on timing and blocks being
mined.

    # Install the development version of cpp-vapory on Ubuntu:
    # sudo add-apt-repository -y ppa:vapory/vapory-qt
    # sudo add-apt-repository -y ppa:vapory/vapory
    # sudo add-apt-repository -y ppa:vapory/vapory-dev
    # sudo apt-get -y update
    # sudo apt-get -y install vap
    #
    # Start vap in test-mode using data directory /tmp/test 
    $ vap --test -d /tmp/test &
    # Wait for it to start up...
    # Run the example:
    $ vapconsole /tmp/test/gvap.ipc example.js

These testing interfaces exist in cpp-vapory:

    web3.test.setChainParams({}, cb(err, bool))
        set chain parameters using the json chain description
        you can use the function chainParams in utils.js to create such a description
    web3.test.mineBlocks(x, cb(err, bool))
        start mining and stop again after exactly x blocks
    web3.test.modifyTimestamp(x, cb(err, bool))
        set the timestamp of the current block to x
    web3.test.rewindToBlock(x, cb(err, bool))
        rewind the blockchain to block number x
    web3.test.addBlock(x, cb(err, bool)
        inject an RLP-encoded block
