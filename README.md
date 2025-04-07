# BitMixer L2 - Privacy-First Bitcoin Mixing Protocol

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Clarity Version](https://img.shields.io/badge/Clarity-2.0-blue)](https://docs.stacks.co/docs/clarity/)

A non-custodial Bitcoin mixing solution offering regulatory-compliant privacy through trustless transactions and programmable compliance controls on Stacks Layer 2.

## Table of Contents

- [BitMixer L2 - Privacy-First Bitcoin Mixing Protocol](#bitmixer-l2---privacy-first-bitcoin-mixing-protocol)
	- [Table of Contents](#table-of-contents)
	- [Project Overview](#project-overview)
	- [Key Features](#key-features)
		- [Mixer Pools](#mixer-pools)
		- [Multi-Signature Security](#multi-signature-security)
		- [Transaction Controls](#transaction-controls)
	- [Technical Specifications](#technical-specifications)
		- [System Limits](#system-limits)
		- [Data Structures](#data-structures)
		- [Error Codes](#error-codes)
	- [Workflows](#workflows)
		- [Standard Mixing Process](#standard-mixing-process)
		- [Multi-Sig Operations](#multi-sig-operations)
	- [Security Considerations](#security-considerations)
		- [Protocol Safeguards](#protocol-safeguards)
		- [Audit Recommendations](#audit-recommendations)
	- [Compliance Features](#compliance-features)
		- [Built-in Controls](#built-in-controls)
		- [Enterprise Extensions](#enterprise-extensions)
	- [Installation \& Usage](#installation--usage)
		- [Requirements](#requirements)
	- [Contributing](#contributing)
	- [References](#references)

## Project Overview

BitMixer L2 implements advanced privacy-preserving Bitcoin transactions while maintaining regulatory compliance through:

- Trustless mixer pools with programmable participation thresholds
- Multi-signature wallet infrastructure (up to 10 signers)
- Automated compliance controls (1,000 BTC daily limit, 24h cooling period)
- Transparent 1% mixing fee structure
- Stacks L2 execution for Bitcoin-native smart contracts

## Key Features

### Mixer Pools

- Create pools with custom IDs (1-1000)
- Join existing pools with minimum 100,000 sats
- Maximum 100 participants per pool
- Pool auto-deactivation when limits reached

### Multi-Signature Security

- Configurable signing thresholds (1-N)
- Signer permission management
- Transaction cooling period enforcement
- Last activity tracking

### Transaction Controls

- Global 10,000 BTC transaction cap
- 1,000 BTC daily user limit
- 1% protocol fee on all mixes
- Anti-flooding protections

## Technical Specifications

### System Limits

| Constant                 | Value             | Description             |
| ------------------------ | ----------------- | ----------------------- |
| `MAX_TRANSACTION_AMOUNT` | 10,000 BTC        | Per-transaction maximum |
| `MAX_DAILY_LIMIT`        | 1,000 BTC         | User daily limit        |
| `COOLING_PERIOD`         | 144 blocks (~24h) | Wallet cooldown         |

### Data Structures

- **Balances**: Principal → sats mapping
- **Mixer Pools**:
  ```clarity
  {
    amount: uint,
    participants: uint,
    participant-list: (list 100 principal),
    active: bool
  }
  ```
- **Multi-Sig Wallets**:
  ```clarity
  {
    threshold: uint,
    total-signers: uint,
    active: bool,
    last-activity: uint
  }
  ```

### Error Codes

| Code    | Description                              |
| ------- | ---------------------------------------- |
| 100-106 | Authorization/Initialization Errors      |
| 107-114 | Protocol Violations (Limits, Duplicates) |

## Workflows

### Standard Mixing Process

1. **Deposit**: User funds account within daily limits
2. **Pool Creation**: Initialize mixer pool with unique ID
3. **Pool Joining**: Participants commit funds to pool
4. **Auto-Mix**: Protocol executes trustless distribution
5. **Withdrawal**: Users claim mixed funds post-cooling period

### Multi-Sig Operations

1. Wallet initialization with threshold
2. Signer permission assignment
3. Transaction proposal creation
4. Threshold signature collection
5. Cooling period enforcement
6. Final execution

## Security Considerations

### Protocol Safeguards

- Reentrancy protection through state locks
- Integer overflow/underflow checks
- Principal validation for all transactions
- Signature replay protection

### Audit Recommendations

- Formal verification of critical paths
- Threshold signature scheme validation
- Stress testing pool capacity limits
- Fee calculation audit trails

## Compliance Features

### Built-in Controls

- Automatic daily limit tracking
- Participant anonymity sets
- Mixing fee transparency
- Activity timestamp logging

### Enterprise Extensions

- KYC/AML integration hooks
- Transaction memo fields
- Regulatory reporting modules
- Whitelist/blacklist management

## Installation & Usage

### Requirements

- Clarinet SDK v2.0+
- Stacks node v3.0+
- Bitcoin testnet environment

## Contributing

1. Fork repository
2. Create feature branch (`feat/your-feature`)
3. Submit PR with test coverage
4. Complete security checklist

## References

- [Stacks Documentation](https://docs.stacks.co)
- [Clarity Language Spec](https://clarity-lang.org)
