---
id: getting-started
title: Ethereum↔Polygon Bridge
sidebar_label: Overview
description: A two-way transaction channel between Polygon and Ethereum.
keywords:
  - docs
  - matic
  - crosschain bridge
  - polygon
  - ethereum
image: https://matic.network/banners/matic-network-16x9.png
---

Polygon brings you a trustless two-way transaction channel between Polygon and Ethereum by introducing the cross-chain bridge with Plasma and PoS security. With this users can transfer tokens across Polygon without incurring third-party risks and market liquidity limitations. **_The Plasma and PoS Bridge is available on both Mumbai as well as Mainnet._**

**Polygon bridge provides a scaling solution which is near-instant, low-cost, and quite flexible**. Polygon uses a dual-consensus architecture(Plasma + Proof-of-Stake (PoS) platform)
to optimise for speed and decentralisation. We consciously architected the system to support arbitrary state transitions on our sidechains, which are EVM-enabled.

**There is no change to the circulating supply of your token when it crosses the bridge**;

- Tokens that leave the Ethereum network are locked and the same number of tokens are minted on Polygon as a pegged token (1:1).
- To move the tokens back to the Ethereum network, tokens are burned on Polygon network and unlocked on Ethereum network during the process.

## PoS vs Plasma

|                                      | PoS Bridge(Recommended)                                                                  | Plasma Bridge                                                                             |
| ------------------------------------ | ---------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| **Short description**                | DApp Developers looking for flexibility and faster withdrawals with POS system security. | DApp Developers looking for increased security guarantees with Plasma exit mechanism\.   |
| **Structure**                        | Highly flexible                                                                          | Rigid, Less Flexible                                                                      |
| **Deposit\(Ethereum → Polygon\)**    | 22-30 mins                                                                                 | 22-30 mins                                                                                  |
| **Withdrawal\(Polygon → Ethereum\)** | 1 checkpoint = ~ 30 mins to 6 hours                                                      | Call to the process-exit procedure on Ethereum's contract                               |
| **Security**                         | Proof\-of\-Stake system, secured by a robust set of external validators\.                | Polygon’s Plasma contracts piggybacks on Ethereum’s security.                             |
| **Support Standards**                | ETH, ERC20, ERC721, ERC1155 and Others                                                   | Only ETH, ERC20, ERC721                                                                   |

## Additional Resources

- [Introduction to Blockchain Bridges](https://ethereum.org/en/bridges/)
- [What are Cross-Chain Bridges](https://www.alchemy.com/overviews/cross-chain-bridges)
