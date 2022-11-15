---
id: web-wallet-v2-guide
title: Web Wallet Usage Guide
description: Learn how to use the Polygon Wallet Suite.
keywords:
  - wallet
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

import useBaseUrl from '@docusaurus/useBaseUrl';

What follows is a set of instructions to deposit and withdraw funds using [Polygon's network](https://wallet.polygon.technology/). For performing those actions, you need to connect a wallet to Polygon's environmnet. In this tutorial, we used Metamask, but Polygon is integrated with other wallets such as Coinbase, Bitski, Venly and WalletConnect.

:::note

Please refer to [<ins>this guide</ins>](https://docs.polygon.technology/docs/develop/metamask/config-polygon-on-metamask/) to learn how to connect Polygon to Metamask.
:::

## Logging into the Polygon Wallet Suite


To log into the Polygon Wallet Suite you need to access the following URL: https://wallet.polygon.technology/.

To log into the **testnet version** of Polygon Wallet Suite, you need to access the following URL: https://wallet-dev.polygon.technology/.


Once you connect your account with the Web Wallet, you will be taken to the landing page with various means on how to transact with the web wallet. Polygon POS chain currently offers the following services:
- The Polygon Wallet for sending, receiving and storing your assets on the Polygon network
- the Polygon Bridge, for withdrawals and deposits across networks.
- Polygon Staking: your go-to place for staking and getting rewards with your MATIC
- and the Widget Dashboard.

Click on the Polygon Wallet or Polygon Bridge, and you will see all your token balances on the Polygon Wallet across the bridges(PoS and Plasma).

<img src={useBaseUrl("img/wallet/wallet-landing-page.png")} width="100%" height="100%"/>

<!-- <img src={useBaseUrl("img/wallet/wallet-one.png")} width="100%" height="100%"/> -->

:::tip Metamask

Be attentive to all Metamask's popups. Throughout the deposit and withdraw processes, you will be prompted with Metamask's popups to confirm transactions, switch networks and for other procedures. You can only proceed with those transactions if you confirm the actions on Metamask.
::: 

## Depositing Funds from Ethereum to Polygon

You can either watch the **video tutorial** below or follow the **step-by-step guide**.

<video loop autoplay width="70%" height="70%" controls="true" >
  <source type="video/mp4" src="/img/wallet/depositv2.mov"></source>
  <p>Your browser does not support the video element.</p>
</video>

### Step-by-step guide

Click on the ‘Move Funds to Polygon Mainnet’ button or on the ‘Deposit’ button from any of the token types on ‘Your tokens on Polygon Mainnet’ section.
<img src={useBaseUrl("img/wallet/deposit-wallet.png")} width="100%" height="100%" />

You will be redirected to the bridge page where you need to enter the deposit amount.
<img src={useBaseUrl("img/wallet/bridge.png")} width="100%" height="100%"/>

:::note

The **transfer mode** will be enabled based on the token chosen.

:::

Once you have added the amount that you want to deposit, you can then click on the “Transfer” button.

After you click on the “Transfer” button, you need to click on the “continue” button on the “Important (Deposit Disclaimer)” popup.

<img src={useBaseUrl("img/wallet/Wallet-5.png")} width="50%" height="50%"/>

You will see a “Transfer Overview” popup with an estimate of the total gas required for the transaction:

<img src={useBaseUrl("img/wallet/Wallet-6.png")} width="50%" height="50%" />

After that, you can review your transaction details:

<img src={useBaseUrl("img/wallet/Wallet-7.png")} width="50%" height="50%" />

Once you confirm the transaction, you will see a “Transfer in Progress” popup which will show you the Deposit status.
It will take ~22-30 minutes for the tokens to show up on Polygon.

<img src={useBaseUrl("img/wallet/Wallet-8.png")} width="50%" height="50%"/>

After the required time, the transaction will be completed.

<img src={useBaseUrl("img/wallet/Wallet-11.png")} width="50%" height="50%" />

:::note

You can always check your past and current transactions by clicking on the "Transactions" tab on the left.

:::

##  Withdrawing Funds from Polygon Back to Ethereum on PoS Bridge

You can either watch the **video tutorial** below or follow the **step-by-step guide**.

<video loop autoplay width="70%" height="70%" controls="true" >
  <source type="video/mp4" src="/img/wallet/withdraw-pos.mov"></source>
  <p>Your browser does not support the video element.</p>
</video>

### Step-by-step guide

Withdrawing funds from Polygon back to the Ethereum mainnet via PoS Bridge is a simple 2-step process. For the funds to be available back on Ethereum it will take about 3 hours. To withdraw funds, click on the ‘Withdraw’ link from any of the PoS token on ‘Your tokens on Polygon Mainnet’ section.

<img src={useBaseUrl("img/wallet/withdraw-POS-1.png")} width="100%" height="100%"/>

You will be redirected to the bridge page where you need to enter the Withdraw amount.

<img src={useBaseUrl("img/wallet/withdraw-POS-2.png")} width="100%" height="100%" />

:::note

The **transfer mode** will be enabled based on the token chosen.

:::

Once you have added the amount that you want to withdraw, you can then click on the “Transfer” button.

After you click on the “Transfer” button, you need to click on the “continue” button on the “Important(Withdraw Disclaimer)” popup.

<img src={useBaseUrl("img/wallet/Wallet-14.png")} width="50%" height="50%" />

You will see a “Transfer Overview” popup with an estimate of the total gas required for the transaction:

<img src={useBaseUrl("img/wallet/Wallet-15.png")} width="50%" height="50%"/>

After that, you can review your transaction details:

<img src={useBaseUrl("img/wallet/Wallet-16.png")}  width="50%" height="50%"/>

Once the transaction is approved, you will see a popup on your screen like this:

<img src={useBaseUrl("img/wallet/Wallet-17.png")} width="50%" height="50%"/>

The first transaction is to initiate your withdrawal.

You need to wait for the checkpoint to arrive. This could take up to 3 hours to complete.

<img src={useBaseUrl("img/wallet/Wallet-19.png")} width="50%" height="50%"/>

Once the checkpoint has arrived, you will need to confirm the second transaction.
Then, when you have confirmed the second transaction, you will receive your funds back on Ethereum.

## Withdrawing Funds from Polygon Back to Ethereum on Plasma Bridge

You can either watch the **video tutorial** below or follow the **step-by-step guide**.

<video loop autoplay width="70%" height="70%" controls="true" >
  <source type="video/mp4" src="/img/wallet/Withdraw-plasma-main.mov"></source>
  <p>Your browser does not support the video element.</p>
</video>

### Step-by-step guide

Withdrawing funds from Polygon back to the Ethereum mainnet via Plasma Bridge is a 3-step process but with a challenge period.

To withdraw funds, click on the ‘Withdraw’ link from any of the Plasma token type on ‘Your tokens on Polygon Mainnet’ section.

<img src={useBaseUrl("img/wallet/withdraw-plasma-1.png")} width="100%" height="100%"/>

You will be redirected to the bridge page where you need to enter the Withdraw amount.

<img src={useBaseUrl("img/wallet/withdraw-plasma-2.png")} width="100%" height="100%"/>

Once you have added the amount that you want to withdraw, you can then click on the “Transfer” button.
After that, you need to click on the “continue” button on “Important(Withdraw Disclaimer)” popup.

<img src={useBaseUrl("img/wallet/Wallet-24.png")} width="50%" height="50%" />

You will see a “Transfer Overview” popup with an estimate of the total gas required for the transaction:

<img src={useBaseUrl("img/wallet/Wallet-25.png")} width="50%" height="50%"/>

Click on the “Continue” button from the “Transfer Overview” popup and you will see a popup opening, similar to the previous one where you can review your transaction details.

<img src={useBaseUrl("img/wallet/Wallet-26.png")} width="50%" height="50%" />

This will be the first of 3 transactions that will need to be completed.

<img src={useBaseUrl("img/wallet/plasma-progress.png")} width="50%" height="50%"/>

The first transaction is to initiate your withdrawal.
Once the withdraw transaction is initiated, you need to wait for the checkpoint to arrive. This could take up to 3 hours to complete.

<img src={useBaseUrl("img/wallet/checkpoint-arrived.png")} width="50%" height="50%"/>

Once the checkpoint has arrived, you need to confirm a new transaction to enter the 7-day challenge period.

<img src={useBaseUrl("img/wallet/challenge-completed.png")} width="50%" height="50%"/>

To get funds back to Ethereum you will need to confirm one last time.
Once you have confirmed all these transactions, you will receive your funds back on Ethereum.

<img src={useBaseUrl("img/wallet/transfer-completed.png")} width="50%" height="50%"/>

:::tip

In case you have any queries, feel free to raise a ticket here: <ins>https://support.polygon.technology/support/home</ins>

:::
