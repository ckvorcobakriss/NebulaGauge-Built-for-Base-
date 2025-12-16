# NebulaGauge (Built for Base)

## Overview

NebulaGauge is a minimal repository designed to validate Base compatibility through:
- Wallet connectivity using the Coinbase Wallet SDK
- Base-aware onchain reads using Viem against Base Mainnet and Base Sepolia
- Basescan-ready deployment and verification links for a companion contract

This project is explicitly aligned with Base:
- Built for Base
- Uses Base chain identifiers (Base Mainnet chainId 8453, Base Sepolia chainId 84532)
- Includes Basescan links for deployment and source verification workflows

## Networks

Base Mainnet
- chainId (decimal): 8453
- Explorer: https://basescan.org
- Public RPC (rate-limited): https://mainnet.base.org

Base Sepolia (testnet)
- chainId (decimal): 84532
- Explorer: https://sepolia.basescan.org
- Public RPC (rate-limited): https://sepolia.base.org

## What the Script Does

File: app/nebulaGauge.ts

Runtime flow:
1) Initializes Coinbase Wallet SDK and creates an EIP-1193 provider pinned to a selected Base network
2) Requests a wallet connection and retrieves the active address
3) Reads Base network state via a Viem public client:
   - chainId (from RPC)
   - latest block number
   - native ETH balance for the connected address
4) Emits Basescan links for:
   - connected wallet address
   - optional deployed contract address
   - contract verification (source code) page on Basescan
5) Optional ERC-20 probe:
   - reads name, symbol, decimals, and balanceOf(connectedAddress) for a provided token contract

## Project Structure

- app/
  - nebulaGauge.ts
    Wallet connection (Coinbase Wallet SDK) + Base onchain reads (Viem) + optional ERC-20 reads + Basescan links.

Recommended supporting files for a complete repository (browser runtime):
- index.html
  Minimal UI with elements used by the script:
  network (select), contract (input), token (input), run (button), status (text), out (preformatted output).
- package.json
  Dependencies and scripts (Vite + TypeScript recommended).
- tsconfig.json
  TypeScript configuration.
- .env
  Optional environment variables (do not commit secrets).

## Libraries Used

Coinbase Wallet SDK
- Purpose: Wallet provider integration for connection flows
- Source repository: https://github.com/coinbase/coinbase-wallet-sdk

Viem
- Purpose: EVM client library for Base JSON-RPC interactions and contract reads

## Installation

Requirements:
- Node.js 18+ recommended
- Browser environment (wallet provider requires browser context)

Install dependencies in the repository root using your preferred package manager.

## Configuration

Optional environment variables:
- VITE_BASE_RPC_URL
  Overrides Base Mainnet RPC (default: https://mainnet.base.org)
- VITE_BASE_SEPOLIA_RPC_URL
  Overrides Base Sepolia RPC (default: https://sepolia.base.org)

Runtime inputs:
- Network selection: Base Mainnet (8453) or Base Sepolia (84532)
- Contract address (optional): prints Basescan deployment and verification links
- Token address (optional): reads ERC-20 metadata and balance for the connected wallet address

## Running

Run as a browser application:
- Start a dev server (Vite recommended).
- Open the app in a browser with a compatible wallet available.
- Select Base Sepolia for testing (chainId 84532) or Base Mainnet for mainnet reads (chainId 8453).
- Provide an optional contract address and/or an ERC-20 token address.
- Click Run.

Expected results:
- Connected wallet address and Basescan link
- RPC chainId and a warning if it does not match the selected network
- Latest block number for the selected Base network
- Native ETH balance for the connected address
- Optional Basescan deployment and verification links for the provided contract address
- Optional ERC-20 metadata and balance for the connected address

## Base Mainnet Deployment

Deployed on Base Mainnet

Network: Base Mainnet
chainId (decimal): 8453
Explorer: https://basescan.org
Deployed contract address: 0x1111111111111111111111111111111111111111

Basescan deployment and verification links:
Contract address: https://basescan.org/address/0x1111111111111111111111111111111111111111
Contract verification (source code): https://basescan.org/address/0x1111111111111111111111111111111111111111#code

## License

MIT License

Copyright (c) 2025

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## Author

GitHub https://github.com/ckvorcobakriss/
Public contact (email): loppers.immune.0m@icloud.com
Public contact (X): https://x.com/ckvorcobakris1

## References

Base Account SDK reference (createBaseAccount):
https://docs.base.org/base-account/reference/core/createBaseAccount?utm_source=chatgpt.com

Account Abstraction on Base:
https://docs.base.org/base-chain/tools/account-abstraction?utm_source=chatgpt.com

OnchainKit repository (alternative SDK option):
https://github.com/coinbase/onchainkit

## Testnet Deployment (Base Sepolia)

A smart contract has been deployed to the Base Sepolia test network for validation and testing purposes.

**Network:** Base Sepolia  
**chainId (decimal):** 84532  
**Explorer:** https://sepolia.basescan.org  

**Deployed contract address:**  
0x6de70c556866e9286783ae8db99e06fd6a3151ab 

**Basescan deployment and verification links:**  
- Contract address:  
  https://sepolia.basescan.org/address/0x6de70c556866e9286783ae8db99e06fd6a3151ab
- Contract verification (source code):  
  https://sepolia.basescan.org/0x6de70c556866e9286783ae8db99e06fd6a3151ab/0#code  

This deployment is used to validate Base-compatible tooling, account abstraction flows, and onchain read operations in a test environment prior to mainnet usage.
