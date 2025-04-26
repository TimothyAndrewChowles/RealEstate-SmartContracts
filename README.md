# RealEstate-SmartContracts
IT 250 Project

# Real-Estate Tokenization Smart Contract

A minimal Solidity contract that executes a trustless property sale on Ethereum.
Used for my IT 250 “Financial Cybersecurity Analyst” presentation.

## Key Features
* **Immutable Ledger** – every deed transfer is hash-stamped forever.
* **Automation** – self-executing escrow via `executeSale()`.

## How to Test Locally
1. `npm i -g ganache-cli`
2. `ganache-cli -p 8545`
3. Open [Remix](https://remix.ethereum.org), import `RealEstateSale.sol`.
4. Compile (Solidity v0.8.21) → Deploy (price = `1000000000000000000`, IPFS = `Qm...`).
5. From a second Ganache account, call `executeSale()` with exactly 1 ETH.

## Security Checklist
- Re-entrancy guard (not needed here – no external calls before state changes).
- Input validation (`require(msg.value == priceWei)`).
- Formal-verification path: Slither + MythX.

---

*Author: Timothy Chowles – aspiring cybersecurity & real-estate finance professional.*
