# Real-Estate Tokenization — Smart-Contract Demo  
*IT 250 • Fundamentals of Information Assurance and Security*

---

## Project Snapshot
| Field | Details |
|-------|---------|
| **Role** | Financial Cybersecurity Analyst |
| **Toolset** | Remix IDE (tool) + Solidity 0.8.21 (language) |
| **Focus** | Secure, trust-less transfer of real-estate ownership on Ethereum |
| **Status** | Proof-of-concept — classroom demo (not production) |

---

## Why This Matters
Traditional property deals crawl through title offices and escrow agents, costing time and money.  
Tokenizing real estate turns a deed into blockchain tokens and settles in seconds.  
**Security is the make-or-break factor**: one bug can drain funds or void ownership.  
This repo shows a minimal, auditable smart contract that:

1. **Accepts an exact payment** (in wei)  
2. **Auto-forwards funds** to the seller  
3. **Emits an immutable on-chain receipt** (`SaleExecuted` event)

---

## Contract at a Glance

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.21;

contract RealEstateSale {
    address public seller;
    uint256 public priceWei;
    string  public propertyIPFS;

    event SaleExecuted(address indexed buyer, uint256 price, uint256 time);

    constructor(uint256 _priceWei, string memory _cid) {
        seller = msg.sender;
        priceWei = _priceWei;
        propertyIPFS = _cid;
    }

    function executeSale() external payable {
        require(msg.value == priceWei, "Incorrect payment");
        (bool ok, ) = seller.call{value: msg.value}("");
        require(ok, "Transfer failed");
        emit SaleExecuted(msg.sender, msg.value, block.timestamp);
    }
}
