# SatsBacked USD (SBUSD)

## Bitcoin-Collateralized Stablecoin Protocol on Stacks

## Overview

**SatsBacked USD (SBUSD)** is a decentralized, Bitcoin-collateralized stablecoin protocol built on the [Stacks blockchain](https://www.stacks.co/). It allows Bitcoin holders to unlock liquidity and mint USD-pegged stablecoins without selling their BTC.

The protocol ensures price stability and solvency through over-collateralization, decentralized oracles, automated liquidations, and transparent on-chain governance.

## Key Features

* **Bitcoin-Collateralized Stablecoin**: Mint SBUSD using BTC as collateral while maintaining ownership of your Bitcoin.
* **Decentralized Vault System**: Securely manage your collateral with user-owned vaults.
* **Over-Collateralization Enforcement**: Protects against insolvency via protocol-defined collateralization ratios.
* **Oracle-Based Price Feeds**: Decentralized and authenticated BTC price oracles ensure accurate valuations.
* **On-Chain Liquidation Engine**: Automatically liquidates undercollateralized vaults to maintain protocol solvency.
* **Governance Controls**: Protocol parameters are managed by the contract owner with upgradeable settings.

## Protocol Components

### Vault System

Users can open vaults, deposit BTC as collateral, and mint SBUSD tokens within protocol-defined risk limits.

* Vaults are indexed by `(owner, id)`
* Each vault tracks: `collateral-amount`, `stablecoin-minted`, and `created-at` height

### Collateralization Rules

* **Collateralization Ratio**: `150%` (default) – vaults must be over-collateralized
* **Liquidation Threshold**: `125%` – vaults below this threshold are eligible for liquidation

### Stablecoin Minting & Redemption

* **Minting**: Users mint SBUSD against their BTC collateral
* **Redemption**: Burn SBUSD to reclaim BTC collateral

### Liquidation Engine

* Non-owners can liquidate vaults that fall below the liquidation threshold
* Collateral is seized, and SBUSD debt is burned to restore protocol balance

### Oracle System

* Whitelisted oracle addresses can update BTC price feeds
* Each price update includes a timestamp and must be within reasonable bounds

### Governance Functions

* Update collateralization ratios
* Add new oracles
* Set protocol fees and mint limits

## Error Handling

All functions provide detailed error messages using consistent error codes:

| Code    | Meaning                   |
| ------- | ------------------------- |
| `u1000` | Not authorized            |
| `u1001` | Insufficient balance      |
| `u1002` | Invalid collateral        |
| `u1003` | Vault undercollateralized |
| `u1004` | BTC price unavailable     |
| `u1005` | Liquidation failed        |
| `u1006` | Mint limit exceeded       |
| `u1007` | Invalid parameters        |
| `u1008` | Unauthorized vault action |

## Security Constants

* `MAX-BTC-PRICE`: Prevents manipulation with unreasonably high BTC prices
* `MAX-TIMESTAMP`: Ensures safe timestamp values in oracle updates

## Developer Guide

### Requirements

* Stacks blockchain
* Clarity smart contract tools (e.g., [Clarinet](https://docs.stacks.co/docs/clarity/clarinet))

### Deployment

To deploy and test the SBUSD protocol:

```bash
clarinet check
clarinet deployment
```

### Core Contracts

* `sip-010-token` Trait – Compliant token interface
* `SatsBacked USD` – Main protocol contract

## Read-Only Functions

| Function               | Description                |
| ---------------------- | -------------------------- |
| `get-latest-btc-price` | Returns latest BTC price   |
| `get-vault-details`    | Returns vault metadata     |
| `get-total-supply`     | Returns SBUSD total supply |

## SIP-010 Token Compatibility

SBUSD follows [SIP-010](https://github.com/stacksgov/sips/blob/main/sips/sip-010/sip-010-fungible-token-standard.md), ensuring interoperability with Stacks DeFi platforms and wallets.

## Contributing

Contributions, audits, and community participation are welcome!

1. Fork the repo
2. Make your changes
3. Submit a PR

## Connect

* Protocol Governance: \[TBD]
* Documentation: Coming soon
* Community: Discord | Twitter | GitHub Discussions

**SatsBacked USD** is a step toward unlocking the liquidity of Bitcoin in decentralized finance. Stay sats-backed, not price-locked.
