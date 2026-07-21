# Muslim Chain Smart Contract Explorer

[![HTML5](https://img.shields.io/badge/HTML5-Semantic-E34F26?logo=html5&logoColor=white)](index.html)
[![JavaScript](https://img.shields.io/badge/JavaScript-Vanilla-F7DF1E?logo=javascript&logoColor=black)](index.html)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A responsive smart-contract explorer interface for the MuslimLogs blockchain ecosystem. The dashboard presents contract metadata, balances, transactions, token transfers, ABI functions, verified source code, and emitted events through configurable REST endpoints.

## Features

- Contract-address lookup with EVM address validation
- Contract metadata and verification status
- Balance, transaction, holder, and creation summaries
- Lazy-loaded transaction and token-transfer tables
- ABI-driven read/write function interface
- Verified Solidity source-code viewer
- Contract event and log viewer
- Copy-to-clipboard and local follow state
- Responsive desktop, tablet, and mobile layout
- Safe escaping of backend values rendered into HTML

## Run locally

No build process is required.

```bash
git clone https://github.com/sohailblockchain/muslim-chain-contract-explorer.git
cd muslim-chain-contract-explorer
python -m http.server 8000
```

Open `http://localhost:8000` and optionally provide an address:

```text
http://localhost:8000/?address=0x0000000000000000000000000000000000000000
```

## Backend integration

Update `CONFIG.BASE` and the endpoint builders near the bottom of `index.html`:

```javascript
const CONFIG = {
  BASE: 'https://api.muslimlogs.com',
  endpoints: {
    contract: address => `/api/v1/contract/${address}`,
    transactions: address => `/api/v1/contract/${address}/transactions`,
    transfers: address => `/api/v1/contract/${address}/token-transfers`,
    abi: address => `/api/v1/contract/${address}/abi`,
    source: address => `/api/v1/contract/${address}/source`,
    events: address => `/api/v1/contract/${address}/events`
  }
};
```

The backend must allow requests from the explorer's deployed origin. Transaction signing and RPC execution intentionally remain host-application integration points; the static UI does not request wallet permissions by itself.

## Security notes

- API-provided values are escaped before insertion into generated markup.
- Contract addresses are validated before navigation.
- Never place private keys, seed phrases, or privileged API secrets in frontend code.
- Validate and normalize all request parameters again on the backend.
- Add rate limiting, authentication, and a strict Content Security Policy before production deployment.

## Recommended repository details

**Name:** `muslim-chain-contract-explorer`

**Description:** Responsive smart-contract explorer for viewing Muslim Chain contract metadata, transactions, token transfers, ABI functions, source code, and events.

**Topics:** `blockchain-explorer`, `smart-contracts`, `ethereum`, `web3`, `javascript`, `html5`, `muslimlogs`, `evm`

## Author

**Sohail Ahmed**

Senior Blockchain Engineer · Founder, BlockForge Labs

## License

Available under the [MIT License](LICENSE).
