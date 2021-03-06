# RChain-API

An API for dApp frontends to communicate with the RChain blockchain.

The [RChain Cooperative][1] is developing a decentralized, economically sustainable public compute infrastructure. Decentralized applications or "dApps" will run their business logic as smart contracts on the blockchain. Their user interfaces will be more traditional programs that interact with the blockchain as a backend. This separation allows dApp developers to create nice abstract interfaces, and allows end users to create their own sovereign interfaces should they choose to do so.

[1]: https://www.rchain.coop/


## Quickstart
### Find an RChain node whose grpc endpoint you can use.
At the moment that likely means [running your own RNode](2). We're working on a community node at rnode-test.rhobot.net

Make note of your RNode's hostname and gRPC port. If you're not sure, `localhost` and `40401` are good guesses.

[2]: https://rchain.atlassian.net/wiki/spaces/CORE/pages/428376065/User+guide+for+running+RNode

### Grab RChain-API
Clone this repository with eg `git clone https://github.com/JoshOrndorff/RChain-API`

And install dependencies with `npm install`

### (Recommended) Run the integration test

Run `rnodeAPI.js` with _host_ and _port_ arguments, as in: `node rnodeAPI.js rnode-test.rhobot.net 50000`.

You should see something like:

```
stuffToSign serialized {
  "type": "Buffer",
  "data": "0a300a110a0f2a031a01784a08000000000000000012112a051a036162634a0800000000000000002a0800000000000000004a080000000000000000"
}
...
doDeploy result: { success: true, message: 'Success!' }
@@createBlock():  {
  "block": {
    "blockHash": {
      "type": "Buffer",
      "data": "3c5d97e2627432026b6d4a17c8027afb95b72e8d08a936d785b58459eff5859e"
```

### Deploy contract to RNode
There are not yet nice truffle-style build tools, so you will probably deploy your code directly using the `rnode deploy` thin client or using RChain-API itself.

```javascript
const myNode = RNode('localhost', 40401);
rchain.doDeploy({
  term: '@"aliceUpdates"!("Having fun traveling!")',
  timestamp: clock().valueOf(),
  // from: '0x1',
  // nonce: 0,
})
```

### Interact with the blockchain
TODO Better docs would be great.

For now see the integration test examples in rnodeAPI.js


## Examples and Related Projects
* [Nth Caller](https://github.com/JoshOrndorff/nth-caller-game) a minimal RChain-based dApp game that uses RChain-API
* [Status](https://github.com/JoshOrndorff/RChain-Status) a moderately complex dapp that uses more RChain-API features as well as [RSign](https://github.com/dckc/RSign)
* [Coin Faucet](https://github.com/BlockSpaces/coin-faucet/) An advanced robust dApp that use raspberry PI to airdrop tokens to devices in physical proximity
* [RChain-dbr](https://github.com/dckc/rchain-dbr) A web-of-trust based distributed budgeting and rewards dApp
* [RSign](https://github.com/dckc/RSign) A chrome extension for generating client-side signatures akin to metamask
* [node-client](https://github.com/rchain/rchain/tree/dev/node-client) A similar but less mature RChain API written in python

## RChain Protocol Buffer Dependency
* Commit hash [27d722e](https://github.com/rchain/rchain/tree/dev/models/src/main/protobuf) 


## License
Copyright 2018 RChain Cooperative

Apache 2.0 License (See LICENSE.txt)

Contributions welcome (See CONTRIBUTING.md)
