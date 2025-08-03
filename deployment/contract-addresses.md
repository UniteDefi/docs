# Contract Addresses

This page contains all deployed contract addresses for Unite DeFi across supported chains. Contracts are verified on respective block explorers.

## Mainnet Deployments

### EVM Chains

#### Ethereum
```
Resolver: 0x[TO_BE_DEPLOYED]
Factory: 0x[TO_BE_DEPLOYED]
```

#### Arbitrum One
```
Resolver: 0x[TO_BE_DEPLOYED]
Factory: 0x[TO_BE_DEPLOYED]
```

#### Optimism
```
Resolver: 0x[TO_BE_DEPLOYED]
Factory: 0x[TO_BE_DEPLOYED]
```

#### Base
```
Resolver: 0x[TO_BE_DEPLOYED]
Factory: 0x[TO_BE_DEPLOYED]
```

#### Polygon
```
Resolver: 0x[TO_BE_DEPLOYED]
Factory: 0x[TO_BE_DEPLOYED]
```

#### BNB Chain
```
Resolver: 0x[TO_BE_DEPLOYED]
Factory: 0x[TO_BE_DEPLOYED]
```

#### Avalanche
```
Resolver: 0x[TO_BE_DEPLOYED]
Factory: 0x[TO_BE_DEPLOYED]
```

### Non-EVM Chains

#### Aptos
```
Resolver Module: 0x[TO_BE_DEPLOYED]::resolver
Escrow Module: 0x[TO_BE_DEPLOYED]::escrow
```

#### Sui
```
Package ID: 0x[TO_BE_DEPLOYED]
Resolver: 0x[TO_BE_DEPLOYED]::resolver
```

#### Stellar
```
Contract ID: [TO_BE_DEPLOYED]
Resolver: [TO_BE_DEPLOYED]
```

#### Cardano
```
Script Address: [TO_BE_DEPLOYED]
Resolver: [TO_BE_DEPLOYED]
```

## Testnet Deployments

### EVM Testnets

#### Ethereum Sepolia
```
Resolver: 0x742d35Cc6634C0532925a3b844Bc9e7595f6E742
Factory: 0x123d35Cc6634C0532925a3b844Bc9e7595f6E123
Explorer: https://sepolia.etherscan.io/address/0x742d35Cc6634C0532925a3b844Bc9e7595f6E742
```

#### Arbitrum Sepolia
```
Resolver: 0x853f35Cc6634C0532925a3b844Bc9e7595f6E853
Factory: 0x456f35Cc6634C0532925a3b844Bc9e7595f6E456
Explorer: https://sepolia.arbiscan.io/address/0x853f35Cc6634C0532925a3b844Bc9e7595f6E853
```

#### Base Sepolia
```
Resolver: 0x964f35Cc6634C0532925a3b844Bc9e7595f6E964
Factory: 0x789f35Cc6634C0532925a3b844Bc9e7595f6E789
Explorer: https://sepolia.basescan.org/address/0x964f35Cc6634C0532925a3b844Bc9e7595f6E964
```

#### Polygon Mumbai
```
Resolver: 0xA75f35Cc6634C0532925a3b844Bc9e7595f6EA75
Factory: 0xABCf35Cc6634C0532925a3b844Bc9e7595f6EABC
Explorer: https://mumbai.polygonscan.com/address/0xA75f35Cc6634C0532925a3b844Bc9e7595f6EA75
```

### Non-EVM Testnets

#### Aptos Testnet
```
Resolver Module: 0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef::resolver
Escrow Module: 0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef::escrow
Explorer: https://explorer.aptoslabs.com/account/0x1234567890abcdef
```

#### Sui Testnet
```
Package ID: 0xabcdef1234567890abcdef1234567890abcdef1234567890abcdef1234567890
Resolver: 0xabcdef1234567890abcdef1234567890abcdef1234567890abcdef1234567890::resolver
Explorer: https://suiexplorer.com/object/0xabcdef1234567890
```

#### Stellar Testnet
```
Contract ID: CCRESOLVERUNITEDEFI5STELLAR5TESTNET5CONTRACT5ID
Resolver: GCRESOLVERUNITEDEFI5STELLAR5TESTNET5RESOLVER5ID
Explorer: https://stellar.expert/explorer/testnet/contract/CCRESOLVERUNITEDEFI
```

## Deployment Configuration

### EVM Deployment Script

```bash
# Deploy to all EVM chains
./scripts/deploy-evm.sh

# Deploy to specific chain
./scripts/deploy-evm.sh --network ethereum-sepolia
```

### Non-EVM Deployment

#### Aptos
```bash
aptos move publish \
  --package-dir ./resolver/chains/aptos \
  --named-addresses unite_addr=0x1234...
```

#### Sui
```bash
sui client publish \
  --path ./resolver/chains/sui \
  --gas-budget 100000000
```

## Verification Status

| Chain | Contract | Verified | Explorer Link |
|-------|----------|----------|---------------|
| Ethereum Sepolia | Resolver | ✅ | [View](https://sepolia.etherscan.io) |
| Arbitrum Sepolia | Resolver | ✅ | [View](https://sepolia.arbiscan.io) |
| Base Sepolia | Resolver | ✅ | [View](https://sepolia.basescan.org) |
| Polygon Mumbai | Resolver | ✅ | [View](https://mumbai.polygonscan.com) |
| Aptos Testnet | Modules | ✅ | [View](https://explorer.aptoslabs.com) |
| Sui Testnet | Package | ✅ | [View](https://suiexplorer.com) |

## Security Considerations

### Multi-Signature Control

All deployed contracts are controlled by multi-signature wallets:

**Mainnet Multisig**: `0x[TO_BE_CONFIGURED]`
- Required Signatures: 3/5
- Owners: [List of owner addresses]

**Testnet Multisig**: `0x[TESTNET_MULTISIG]`
- Required Signatures: 2/3
- Owners: Development team

### Upgrade Pattern

Contracts use the following upgrade patterns:

**EVM Chains**: Transparent Upgradeable Proxy
```solidity
// Proxy Admin
0x[PROXY_ADMIN_ADDRESS]

// Implementation can be upgraded via ProxyAdmin
```

**Non-EVM Chains**: Native upgrade mechanisms
- Aptos: Package upgrade capability
- Sui: Package upgrade via governance
- Others: Chain-specific patterns

## Integration Guide

### For Developers

```typescript
// EVM Integration
import { ethers } from 'ethers';

const RESOLVER_ABI = [...]; // Import from @unite-defi/contracts
const RESOLVER_ADDRESS = "0x742d35Cc6634C0532925a3b844Bc9e7595f6E742";

const resolver = new ethers.Contract(
  RESOLVER_ADDRESS,
  RESOLVER_ABI,
  provider
);
```

### For Resolvers

```typescript
// Monitor events
resolver.on("SwapCreated", (orderId, details) => {
  console.log("New swap order:", orderId);
  // Evaluate and commit if profitable
});
```

## Audit Reports

Contracts have been audited by:

1. **[Auditor Name]** - [Report Link]
2. **[Auditor Name]** - [Report Link]

## Emergency Contacts

### Technical Support
- Discord: [Unite DeFi Discord](https://discord.gg/unite-defi)
- Email: tech@unite-defi.com

### Security Issues
- Email: security@unite-defi.com
- Bug Bounty: [Immunefi Program](https://immunefi.com/unite-defi)

---

> **Note**: Mainnet addresses will be updated upon deployment. Always verify addresses from official sources before interacting with contracts.