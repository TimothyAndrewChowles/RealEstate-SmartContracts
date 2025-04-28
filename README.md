# Real-Estate Tokenization Smart-Contract Demo

Solidity contract + walkthrough for my IT 250 “Financial Cybersecurity Analyst” project.

## How it works
* Seller sets price & IPFS doc hash at deploy.
* Buyer calls `executeSale()` with exact ETH ➜ funds auto-forward, `SaleExecuted` logs.

## Try it locally
1. Open [Remix](https://remix.ethereum.org)
2. Paste `RealEstateSale.sol`, compile (0.8.21).
3. Deploy in Remix VM with `priceWei = 1e18`, `cid = Qm...`.
4. Switch account, send 1 ETH to `executeSale()`.

## Security notes
* Uses `require` checks to prevent incorrect payments.
* Minimal surface → no storage writes after fund transfer (mitigates re-entrancy).
* For prod, add OpenZeppelin ReentrancyGuard & a `bool isSold`.

---

© 2025 Timothy Chowles
