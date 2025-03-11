# Cross-Chain NFT Bridge with Chainlink CCIP

This documentation outlines the implementation of a Cross-Chain NFT Bridge between the **Avalanche blockchain** and other supported networks. Initially, the bridge leverages **Avalanche’s Inter-Chain Communication** (ICM) and **Teleporter Contracts** to enable decentralized validation and secure NFT transfers between Avalanche and non-EVM blockchains.

In this phase, **ICM** ensures that NFTs can be securely locked on the source chain and minted on the destination chain, while Teleporter efficiently handles the minting process on the target blockchain, providing interoperability across different networks.

For **EVM-compatible chains**, the bridge will later integrate **Chainlink’s Cross-Chain Interoperability Protocol** (CCIP), which will provide decentralized validation, allowing NFTs to be securely transferred across multiple blockchains with enhanced scalability and flexibility. This phase will extend the bridge’s functionality to include EVM chains, ensuring a wider network of supported blockchains.

## Table of Contents
1. [Introduction](#1-introduction)
2. [How the Bridge Works](#2-how-the-bridge-works)
3. [Avalanche ICM Overview](#3-avalanche-icm-overview)
4. [ICM Smart Contract Architecture](#4-icm-smart-contract-architecture)
5. [CCIP Smart Contract Architecture](#5-ccip-smart-contract-architecture)
6. [Roadmap](#5-roadmap)

## 1. Introduction

The Cross-Chain NFT Bridge enables users to securely transfer NFTs between Avalanche and other L1 blockchains, facilitating seamless interoperability. NFTs locked on one chain can be minted on the destination chain through the use of **Avalanche ICM** and **Teleporter Contracts**, providing a decentralized and trustless validation mechanism for cross-chain operations. With ICM’s validator-backed communication and Teleporter’s efficient NFT minting process, the bridge ensures secure and reliable asset transfers across different blockchain networks.

## 2. How the Bridge Works

The bridge operates by locking NFTs on the source blockchain and minting an equivalent NFT on the target blockchain. Below are the core steps of the process:

1. **Lock Tokens on the Source Chain**: When a user wishes to transfer an NFT from one network to another, they lock the NFT on the source blockchain. The **Teleporter Contract** locks the NFT on the source blockchain and sends a message via **ICM** (Inter-Chain Communication), notifying the destination blockchain of the event
2. **Validation with ICM**: **ICM** validates the lock event by utilizing validator nodes across the networks. These validator nodes verify the lock state on the source blockchain and send confirmation to the target blockchain to trigger the minting of an equivalent NFT.
3. **Minting on the Target Chain**: Once ICM confirms the lock event, the **Teleporter Contract** mints an equivalent NFT on the target blockchain. The **minted NFT** is now represented on the destination blockchain, while the original remains locked on the source chain.
4. **Unlocking the NFT**: If the user wants to return the NFT to the source chain, they can initiate a reverse transaction, unlocking the NFT on the target chain and burning the minted NFT on the destination.

## 3. Avalanche ICM Overview

Avalanche’s **Inter-Chain Communication** (ICM) and **Teleporter Contracts** are utilized to create decentralized bridges for transferring NFTs and data between blockchains. By leveraging ICM and Teleporter, we enable secure and efficient cross-chain operations without relying on centralized intermediaries.

- **Security**: Validator-backed ICM ensures that cross-chain communications are securely validated, eliminating single points of failure and preserving the integrity of the transactions across different blockchains.
- **Scalability**: ICM supports communication between an unlimited number of chains, allowing for flexibility as additional networks are integrated into the bridge. Teleporter facilitates the minting of NFTs on destination blockchains while maintaining security and operational efficiency across various ecosystems.

## 4. ICM Smart Contract Architecture

The architecture consists of two primary smart contracts: one deployed on the source blockchain and another on the target blockchain, leveraging **ICM** and **Teleporter** for cross-chain NFT transfers.

### **Source Chain Bridge Contract**
- **`Lock Tokens`**: This function locks NFTs on the source blockchain before initiating the transfer process.
- **`Request Validation via ICM`**: Sends a request to the **ICM** protocol to validate the lock event and notify the target blockchain to begin the minting process.
- **`Receive Validation`**: Accepts the validation message from the **ICM** protocol and triggers the minting process on the target chain.

### **Target Chain Bridge Contract**
- **`Mint Tokens`**: Mints the equivalent NFT on the target blockchain once the validation is confirmed via **ICM**.
- **`Burn Tokens`**: Burns the minted NFT on the target blockchain if the user initiates a reverse transaction, unlocking the NFT on the source blockchain.

### **ICM Validator Contract**
- **`Cross-Chain Validation`**: Ensures the event (e.g., locking the NFT on the source chain) is confirmed by **ICM** before triggering the actions on the target blockchain. The validator ensures the integrity of the cross-chain transaction using **validator-backed messaging** system provided by **ICM**.

## 5. CCIP Smart Contract Architecture

The architecture consists of two primary smart contracts: one deployed on the source blockchain and another on the target blockchain.

### Source Chain Bridge Contract
- **Lock Tokens**: This function allows users to lock their NFTs on the source blockchain.
- **Request Validation**: Sends a request to the Chainlink CCIP oracle to validate the lock event and trigger the minting process on the target chain.
- **Receive Validation**: Accepts the validation response from the oracle, triggering the minting on the target chain.

### Target Chain Bridge Contract
- **Mint Tokens**: This function allows the minting of the NFT on the target blockchain once validation is received.
- **Burn Tokens**: This function allows the burning of NFTs if the user wants to return them to the source blockchain.

### Chainlink Oracle Contract
- **Cross-Chain Validation**: The oracle ensures that the event (e.g., locking an NFT on the source chain) is confirmed before triggering actions on the target chain.



![System Architecture](https://github.com/HKskn/Cross-Chain-NFT-Bridge/blob/main/ccip-diagram-04_v04.webp?raw=true)



## 5. Roadmap

### Step 1: Avalanche ICM NFT Bridge

In the initial phase, leveraging Teleporter and ICM, the bridge will expand to include other **Layer-1** blockchains. This phase will focus on:

- **Enabling seamless communication between Avalanche Layer-1 and its main network for cross-chain NFT transfers**: The bridge will leverage **Inter-Chain Communication (ICM)** protocols to allow Avalanche Layer-1 and the Avalanche main network to seamlessly exchange data and NFTs. This ensures that NFTs locked on one chain can be accurately minted or transferred on the other using validator-backed BLS signatures for security and efficiency.
- Testing and ensuring smooth operation for cross-chain transfers.

### Step 2: ChainLink CCIP-Based Bridge

In the next phase, Integrating Chainlink CCIP, this bridge connects Avalanche to external EVM chains (e.g., Ethereum to Avalanche, or vice versa). It facilitates secure NFT transfers using CCIP’s decentralized oracle network and messaging protocol, expanding Avalanche’s reach to broader blockchain ecosystems. This phase will focus on:

- Developing and deploying the smart contracts for locking and minting NFTs.
- Integrating **Chainlink CCIP** for secure, decentralized validation between the two chains.
- Testing and ensuring smooth operation for cross-chain transfers.

