---
id: pos-using-metamask
title: PoS Using Metamask
description: "Transfer tokens between Ethereum and Polygon with Metamask."
keywords:
  - docs
  - matic
  - metamask
image: https://matic.network/banners/matic-network-16x9.png
---

import useBaseUrl from '@docusaurus/useBaseUrl';

This tutorial is a brief introduction on how to transfer tokens between Ethereum and Polygon on PoS bridge using **_matic.js SDK and Metamask_**. Polygon-Ethereum bridge provides a cross-chain channel where users can transfer tokens from Ethereum to Polygon and vice-versa. More details on using the bridge can be found [here](/docs/develop/ethereum-polygon/pos/getting-started). This **tutorial mainly focuses on using the bridge from a front end perspective**. We will be using Metamask for this purpose.

The most important thing to be understood from this tutorial is the **proper usage of the web3 provider in the matic.js instance** we create. Whether using PoS or Plasma, certain actions need to be performed on Polygon and some on Ethereum. Due to this reason, **different providers are required in different scenarios. Hence correctly setting the providers is necessary.**

1. An **example react app that demonstrates the usage of the Plasma and PoS bridge** can be found [here](https://github.com/maticnetwork/pos-plasma-tutorial) .
2. Install the dependencies using `npm install` .
3. Replace the token addresses in src/config.json with your corresponding token addresses

```jsx

posRootERC20: ERC20 root token address on pos bridge
posChildERC20: ERC20 child token address on pos bridge
posWETH: PoS Weth
rootChainWETH: WETH deployed on root chain
plasmaWETH: Plasma WETH
plasmaRootERC20: ERC20 root token deployed on plasma
plasmaChildERC20: ERC20 child token deployed on plasma
MATIC_RPC: RPC for child chain,
ETHEREUM_RPC: RPC for root chain,
VERSION: network version,
NETWORK: "testnet" or "mainnet"
MATIC_CHAINID: Chain ID of child chain,
ETHEREUM_CHAINID: Chain ID of root chain

```

- The configuration and key values for Polygon mainnet and mumbai testnet can be found here
  1. [Mumbai Testnet Config](https://static.matic.network/network/testnet/mumbai/index.json)
  2. [Polygon Mainnet Config](https://static.matic.network/network/mainnet/v1/index.json)

4. Run the project using `npm start` .

## Example using PoS ERC20 Test Token

:::note 
For the mainnet, Ethereum is the root chain and Polygon Mainnet is the child chain and for the testnet, Goerli is the root chain and Mumbai is the child chain. The values in the `config.json` file should be set accordingly. Goerli and Mumbai networks are used as the root and child chain in this tutorial.
:::

`posClientParent()` and `posClientChild` are used to initialize the root and child chain matic.js object for the PoS bridge. Code snippets mentioned below, under each step, can be found in the [tutorial](https://github.com/maticnetwork/pos-plasma-tutorial) repo as well.

### Deposit

To deposit ERC20 tokens, an approve function call has to be made before calling the deposit function. Upon clicking the deposit button, Metamask will first ask to approve the transfer of a specified number of tokens and after the confirmation of the approval transaction, Metamask will ask to confirm the deposit transaction. Make sure the root chain network is selected in Metamask for deposit functionality.

```js
// approve amount 10 on parent token
const approveResult = await erc20ParentToken.approve(10);

const erc20RootToken = posClient.erc20(<root token address>, true);

//deposit 100 to user address
const result = await erc20Token.deposit(100, <user address>);

```

During deposit of ERC20 tokens, the providers are specified as below

`maticProvider: maticprovider`

`parentProvider: window.web3`

:::note 

Deposits from Ethereum to Polygon happen using a state sync mechanism and takes about ~22-30 minutes. After waiting for this time interval, it is recommended to check the balance using web3.js/matic.js library or using Metamask. The explorer will show the balance only if at least one asset transfer has happened on the child chain. This [link](/docs/develop/ethereum-polygon/pos/deposit-withdraw-event-pos/) explains how to track the deposit events.

:::

<div align="center">
  <img src={useBaseUrl("img/pos-using-metamask/deposit.png")} />
</div>

### Transfer

Once deposited, the token can be transfered to any other account on the Polygon chain.

During Transfer, only the `maticProvider` needs to be set as `window.web3`.

```js
const erc20Token = posClient.erc20(<token address>);

const result = await erc20Token.transfer(<amount>,<to>);

const txHash = await result.getTransactionHash();

const txReceipt = await result.getReceipt();

```

### Burn

For withdrawing tokens back to root chain, tokens have to be first burn on child chain. Make sure child chain network is selected in Metamask.
The `withdrawStart()` method can be used to initiate the withdrawal process which will burn the specified amount on the Polygon chain.

```js
const erc20Token = posClient.erc20(<token address>);

// start withdraw process for 100 amount
const result = await erc20Token.withdrawStart(100);

const txHash = await result.getTransactionHash();

const txReceipt = await result.getReceipt();

```

During burning of ERC20 tokens, providers are specified as below:

`maticProvider: window.web3`

`parentProvider: ethereumprovider`

<div align= "center">
  <img src={useBaseUrl("img/pos-using-metamask/burn.png")} />
</div>

### Exit

The exit process takes place on Ethereum and upon confirmation, an equivalent amount of tokens that were burned on child chain is released to the users address on root chain. Make sure the root chain network is selected in Metamask. The burn hash obtained after burning of tokens is given as the input. Wait for the checkpointing to complete before doing this exit process. Checkpoint time is usually around 30 minutes.

During exit of ERC20 tokens, the providers are specified as below:

`maticProvider: maticprovider`

`parentProvider: window.web3`

The `withdrawExit()` function in the PoS bridge involves block proof generation by querying the child chain multiple times and hence it may take 4-5 seconds for Metamask to pop up as it consumes time to build the transaction object.

```js
const erc20RootToken = posClient.erc20(<root token address>, true);

// start withdraw process for 100 amount
const result = await erc20Token.withdrawExit(<burn tx hash>);

const txHash = await result.getTransactionHash();

const txReceipt = await result.getReceipt();

```
You can also use the `withdrawExitFaster()` method to exit the withdrawal process faster. For more details please visit this [guide](https://maticnetwork.github.io/matic.js/docs/pos/erc20/withdraw-exit-faster/).

<div align= "center">
  <img src={useBaseUrl("img/pos-using-metamask/exit.png")} />
</div>
