---
id: overview
title: "Polygon ID: An Introduction"
sidebar_label: Introduction
description: "Polygon ID main concepts."
keywords: 
  - docs
  - polygon
  - id
  - holder
  - issuer
  - verifier
image: https://matic.network/banners/matic-network-16x9.png
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Based on the principles of Self-Sovereign Identity (SSI) and cryptography, Polygon ID is a decentralised and permissionless identity framework for web2 and web3 applications. The SSI framework lets individuals own and control their identities. 

:::tip Contact

You can always refer to our [<ins>twitter page</ins>](https://twitter.com/0xpolygonid) to stay updated with the Polygon ID latest development.  

:::

## Why Polygon ID?

Polygon ID, with the help of zero-knowledge proofs, lets users prove their identity without the need of exposing their private information. This ensures both the **Freedom of Expression** to anyone who intends to use the Polygon ID and **Privacy by Default**, as users' identities are secured by zero-knowledge cryptography.

## Core Concepts of Polygon ID: Claim, Identity Holder, Issuer and Verifier (Triangle of Trust)

Every identity-based information is represented via a [Claim](https://docs.iden3.io/protocol/claims-structure/). In the simplest terms, a claim represents any type of information related to an individual/enterprise/object. The claim could be as simple as the age of the entity or the highest degree held by it or even a membership certificate issued by a DAO. 

The architecture of the framework is composed of three modules: Identity Holder, Issuer, and Verifier. These three, together, form what we call the `triangle of trust`. Let us see what role each entity plays in Polygon ID. 

1. **Identity Holder**: An entity that holds claims in its [Wallet](wallet/wallet-overview). A claim, as mentioned above, is issued by an Issuer to the Holder. The Identity holder creates the zero-knowledge proofs of the claims issued and presents these proofs to the Verifier (which verifies the correctness and authenticity of the claim). A Holder is also called Prover as it needs to prove to the Verifier that the credential it holds is authentic and matches specific criteria. 

2. [**Issuer**](issuer/issuer-overview): An entity (person, organization, or thing) that issues claims to the Holders. Claims are cryptographically signed by the Issuer. Every claim comes from an Issuer. 

3. [**Verifier**](./verifier/verifier-overview): A Verifier verifies the claims presented by a Holder. It requests the Holder to send proof of the claim issued from an Issuer and on receiving the zero-knowledge proofs from the Holder, verifies it. The verification process includes checking the veracity of the signature of the Issuer. The simplest real-world examples of a Verifier can be a recruiter that verifies your educational background or a voting platform that verifies your age. 

:::note
The verification of a claim can happen either off-chain or on-chain.
:::

<div align= "center">
<img src= {useBaseUrl("img/polygonid/triangle-of-trust-polygonID.png")} width="500"/>
</div>

<br></br>

## Role of a Wallet

A [Wallet](./wallet/wallet-overview.md) plays a crucial role in the seamless exchange of claims and other related data with the Issuer, on one hand, and with the Verifier, on the other. As stated above, an Identity Holder carries his/her personal data, in the form of a claim, within their wallet. At its core, the wallet stores the private key of a user, fetch claims from the Issuer, and create zero-knowledge proofs to be presented to the Verifier. Being the carrier of the sensitive information, the Wallet has been designed to ensure that the identity of its Holder is protected and preserved, and no sensitive data can be revealed to the third party without the consent of the Holder.  

## What can you achieve using Polygon ID?

1. **Privacy using Zero-Knowledge Proofs**: An Identity Holder, using zero-knowledge proofs, can keep his/her/its personal data private. During the process of claim verification, it just needs to show that he is the owner of that claim without letting the Verifier know of the actual claim. For example, an Identity Holder can prove to a Verifier authority that s/he is above 18 years of age by presenting the proof that s/he is above 18 without revealing his/her actual age. This ensures minimum data exposure and hence ensures the safety of any sensitive data. 
Another aspect of privacy comes from the fact that the Issuer would not be able to track an individual's credential once it has been issued. 

2. **Off-Chain and On-Chain Verification**: Verification of proofs can be done either off-chain or on-chain via Smart Contracts. For example, developers can set up a contract that airdrops tokens only to users that meet certain criteria based on their claims.

3. **Self-Sovereignty**: Polygon ID renders self-sovereignty in the hands of the user. The user is the only custodian of his/her private keys; user-controlled data can be shared with third parties without taking any permission from the Issuer that has issued the claims to the user.

4. **Transitive Trust**: A transitive trust between the players of an SSI system (Holder, Issuer, and Verifier) means that the trust between two entities in one domain or context can be easily extended to other domains or contexts. For instance, the information generated by an Issuer can be conveniently used by more than one Verifier. Along the similar lines, an Identity Holder can build up his/her trust by collecting multiple credentials from different Issuers in one digital wallet. 

## Polygon ID and Iden3

<a href="https://iden3.io/" target="_blank">Iden3</a> is the open-source protocol at the basis of Polygon ID. The protocol defines on a low-level how the parties listed above communicate and interact with each other. Polygon ID is an abstraction layer to enable developers to build applications leveraging the Iden3 protocol.

<hr></hr>

[**Polygon ID on GitHub**](https://github.com/0xPolygonID)






