---
id: calling-plasma-contracts
title: Calling Plasma Contracts
description: Build your next blockchain app on Matic.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png 
---

For most developers, it is advisable and recommended to use the Matic.js library to interact with Matic.

However, this page helps developers, who have a good understanding of smart contracts in Ethereum, to bypass the Matic.js library and interact directly with the Matic smart contracts. This might help developers to understand the inner workings of Matic Network, as well as to customise their interaction with Matic to some extent.

## Important Addresses and Links

**Matic RPC endpoint**: `https://testnetv3.matic.network`

| Contract           | ABI | Ropsten | Matic |
|--------------------|--|--|--|
| TEST (ERC20) token |<a target="_blank" href="https://raw.githubusercontent.com/maticnetwork/static/master/network/testnet/v3/artifacts/ChildERC20.json"><img src="https://img.icons8.com/metro/26/000000/download.png" width="25px" style={{padding: '2px'}} /></a>|`0xEc5C207897C4378658F52bCCCE0ea648D1f17D65`|`0xBc0AEe9f7b65fd3d8be30ba648e00dB5F734942b`|
|Registry Root Contract|<a target="_blank" href="https://raw.githubusercontent.com/maticnetwork/static/master/network/testnet/v3/artifacts/Registry.json"><img src="https://img.icons8.com/metro/26/000000/download.png" width="25px" style={{padding: '2px'}} /></a>|`0x82a72315E16cE224f28E1F1fB97856d3bF83f010`|   |
|DepositManager (Proxy) Contract|<a target="_blank" href="https://raw.githubusercontent.com/maticnetwork/static/master/network/testnet/v3/artifacts/DepositManager.json"><img src="https://img.icons8.com/metro/26/000000/download.png" width="25px" style={{padding: '2px'}} /></a>|`0x3Bc6701cA1C32BBaC8D1ffA2294EE3444Ad93989`|||
|Child Chain Contract|<a target="_blank" href="https://raw.githubusercontent.com/maticnetwork/static/master/network/testnet/v3/artifacts/ChildChain.json"><img src="https://img.icons8.com/metro/26/000000/download.png" width="25px" style={{padding: '2px'}} /></a>||`0xa2EF03edfA084ac9e5Bf110e409Ed5483BAe4101`|
|WithdrawManager (Proxy) Contract|<a target="_blank" href="https://raw.githubusercontent.com/maticnetwork/static/master/network/testnet/v3/artifacts/WithdrawManager.json"><img src="https://img.icons8.com/metro/26/000000/download.png" width="25px" style={{padding: '2px'}} /></a>|`0x3cf9aD3395028a42EAfc949e2EC4588396b8A7D4`||

### Tokens for testing

To get some `TEST` tokens on Ropsten network, you can access the Matic Faucet by clicking on the link below:

<div style={{textAlign: 'center', paddingTop: '15px', paddingBottom: '15px'}}>
        <button className="btn btn-primary btn-md" style={{padding: '15px', backgroundColor: '#000', color: '#fff', borderRadius: '4px', cursor: 'pointer', boxShadow: '0px 4px 7px -4px rgba(0,0,0,0.75)'}}>
          <a href="https://faucet.matic.network" target="_blank" style={{color: 'inherit'}}>
            Get Test Tokens
          </a>
        </button>
      </div>

### Matic Explorer

You can also check transaction procesed on the Matic Sidechain using the Matic Explorer.

Link to the explorer - https://testnetv3-explorer.matic.network/

## Workflow

### 1. Deposit ERC20 token from Ropsten to Matic

**Description**: To deposit assets (ERC20) from Ropsten to Matic

Let the required amount of tokens be **X**.

1. The Deposit Manager Contract is approved to spend **X** on behalf of `msg.sender`
   - **Contract**: `ERC20.sol` and `DepositManager.sol`
   - **Network**: Ropsten
   - **Function**: `approve`

  Call the standard `approve` function in ERC20 contract, approving `DepositManager` to transfer the amount of tokens.
  
  ```javascript
  RootERC20Contract.methods
    .approve(
      this.depositManagerContract.options.address,
      this.encode(amount)
    )
  ```

2. The Deposit Manager transfers the amount from `msg.sender` to itself

   - **Contract**: `DepositManager.sol`
   - **Network**: Ropsten
   - **Function**: [`despositERC20ForUser()`](https://github.com/maticnetwork/contracts/blob/6413308db75ecdbf8ab9ec2beee1db0d362acea3/contracts/root/depositManager/DepositManager.sol#L129)

  Transfers the amount of tokens from msg.sender to DepositManager. Emits [NewDepositBlock](https://github.com/maticnetwork/contracts/blob/6413308db75ecdbf8ab9ec2beee1db0d362acea3/contracts/root/depositManager/DepositManager.sol#L223) event.

  ```javascript
  depositManagerContract.methods
    .depositERC20ForUser(
      token, 
      user, 
      this.encode(amount)
    )
  ```

> Depositing tokens on Matic, mints new tokens for ChildERC20 contract on Matic network. ChildERC20 contract is the contract that is deployed with the process of mapping, which is representative of the token present on main network.

### 2. Transfer tokens on Matic

**Description**: To transfer tokens on Matic testnet

  1. Invokes the standard `transfer` function of ERC20 contract.
      - **Contract**: `ChildERC20.sol`
      - **Network**: Matic
      - **Function**: `transfer`
    ```javascript
    ChildERC20.methods
      .transfer(
        recipientAddress,
        this.encode(amount)
      )
    ```

### 3. Display account balances for users on Matic

**Description**: Query ERC20 token balances for user on Matic and Ropsten

  1. Invokes the standard `balanceOf` function of ERC20 contract.
      - **Contract**: `ChildERC20.sol`
      - **Network**: Matic
      - **Function**: `balanceOf` 
        ```javascript
        // ERC20TokenContract can be either on Ropsten or Matic
        ERC20TokenContract.methods
          .balanceOf(
            owner
          )
        ```

### 4. Withdraw ERC20 tokens from Matic to Ropsten

**Description**: To withdraw assets (ERC20) from Matic testnet to Ropsten

Procedure of Withdrawal:


1. Burn tokens on Matic sidechain
2. Submit proof of burn (the receipt of burn tx) on Root Chain
   1. This step is executed only after the block consisting of the burn tx has been included in a checkpoint on the Root Chain.
   2. After checkpoint submission, a successful execution of this step 
      1. marks the initiation of the Challenge Exit Period (which is a 7-day period on main network, and set to 5 minute on test networks)
      2. Mints an `ExitNFT` token to the exitor's account - which is representative of the exit initiated on the child chain by the exitor
   3. After the challenge period has ended, processExits burns the Exit NFT and transfers the tokens back from Deposit manager to the exitor.

Let **X** be the amount of tokens to be withdrawn.

1. Submit withdraw request of **X** tokens on Matic - burns the tokens and returns a tx ID.
      - **Contract**: `ChildERC20.sol`
      - **Network**: Matic
      - **Function**: `withdraw`

    Burns tokens on Matic and emits [Withdraw](https://github.com/maticnetwork/contracts/blob/6413308db75ecdbf8ab9ec2beee1db0d362acea3/contracts/child/ChildERC20.sol#L52) event
    ```javascript
    ChildToken.methods
      .withdraw(
        amount
      )
    ```
2. Use tx ID from previous step to create a withdraw transaction on Ropsten
       - **Contract**: `ERC20Predicate.sol`
       - **Network**: Ropsten
       - **Function**: `startExitWithBurntTokens`

    The function accepts payload data, which is the proof of burn of tokens performed in the previous transaction. This payload is generated off-chain.
      ```javascript
      payload = await _buildPayloadForExit(burnTxHash)
      erc20PredicateContract.methods
        .startExitWithBurntTokens(
          payload,
        )
      ```

    To build payload for the exit: 
      1. Get last child block from RootChain.sol - this is the number of block which was checkpointed last on the root chain
      2. If the last checkpointed block is less than the block containing the burn transaction - wait until the block is checkpointed.
      3. If the checkpoint has been included
         1. find HeaderBlockNumber from RootChain.sol
            1. From the last checkpointed block to the block consisting of burn transaction perform search (matic.js performs a binary search) to find the block with the burn tx.
            2. Query RootChain.sol with the header block number 
         2. Build Block Proof, sample: https://github.com/maticnetwork/contracts/blob/fa6862dc6ddae97351aa1b4d16c087861b5a489e/contracts-core/helpers/proofs.js#L24
         3. Build Receipt Proof, sample: https://github.com/maticnetwork/contracts/blob/fa6862dc6ddae97351aa1b4d16c087861b5a489e/contracts-core/helpers/proofs.js#L106
      4. Return hex encoded string of bytes: `headernumber`, `blockProof`, `block number of burn transaction`, `timestamp of the burn tx block`, `root of block`, `root of receipts`, `RLP encoded receipt bytes`, `receipt parent nodes`, `receipt path`, `logIndex`

      ```javascript
      private async _buildPayloadForExit(burnTxHash) {
        // check checkpoint
        const lastChildBlock = await rootChain.getLastChildBlock()
        const burnTx = await web3.eth.getTransaction(burnTxHash)
        const receipt = await web3.eth.getTransactionReceipt(burnTxHash)
        const block = await web3.eth.getBlock(
          burnTx.blockNumber, 
          true /* returnTransactionObjects */
        )

        // check here if the burn tx has been checkpointed or not
        logger.info( { 'burnTx.blockNumber': burnTx.blockNumber, lastCheckPointedBlockNumber: lastChildBlock } )
        assert.ok(
          new BN(lastChildBlock).gte(new BN(burnTx.blockNumber)),
          'Burn transaction has not been checkpointed as yet',
        )
          // if the block has been checkpointed, move ahead

          const headerBlockNumber = await rootChainContract.findHeaderBlockNumber(burnTx.blockNumber)
          const headerBlock = await web3.call(
            rootChainContract
              .getRawContract()
              .methods.headerBlocks(this.encode(headerBlockNumber)),
          )
          logger.info({ 'headerBlockNumber': headerBlockNumber.toString(), headerBlock })

            // build block proof
            const blockProof = await Proofs.buildBlockProof(
              this.web3Client.getMaticWeb3(),
              headerBlock.start,
              headerBlock.end,
              burnTx.blockNumber,
            )
            // build receipt proof
            const receiptProof = await Proofs.getReceiptProof(
              receipt,
              block,
              this.web3Client.getMaticWeb3(),
            )
            return this._encodePayload(
              headerBlockNumber,
              blockProof,
              burnTx.blockNumber,
              block.timestamp,
              Buffer.from(block.transactionsRoot.slice(2), 'hex'),
              Buffer.from(block.receiptsRoot.slice(2), 'hex'),
              Proofs.getReceiptBytes(receipt), // rlp encoded
              receiptProof.parentNodes,
              receiptProof.path,
              // @todo logIndex can vary
              1, // logIndex
            )
          }
        ```

        To encode payload (returned in the previous function)

        ```javascript
          function _encodePayload(
            headerNumber,
            buildBlockProof,
            blockNumber,
            timestamp,
            transactionsRoot,
            receiptsRoot,
            receipt,
            receiptParentNodes,
            path,
            logIndex,
          ) {
            return ethUtils.bufferToHex(
              ethUtils.rlp.encode([
                headerNumber,
                buildBlockProof,
                blockNumber,
                timestamp,
                ethUtils.bufferToHex(transactionsRoot),
                ethUtils.bufferToHex(receiptsRoot),
                ethUtils.bufferToHex(receipt),
                ethUtils.bufferToHex(ethUtils.rlp.encode(receiptParentNodes)),
                ethUtils.bufferToHex(ethUtils.rlp.encode(path)),
                logIndex,
              ]),
            )
          }

          ```

3. Process Exits

    Third and final step for the withdrawal process is to Process pending exits on the root chain. 

    - **Contract**: `WithdrawManager.sol`
    - **Network**: Ropsten
    - **Function**: `processExits`
        ```javascript
          withdrawManager.methods
            .processExits(
              token
            )
        ```