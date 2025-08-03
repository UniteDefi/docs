# Developer Guide

Welcome to the Unite DeFi developer guide! This comprehensive guide will help you integrate Unite DeFi's cross-chain swap functionality into your applications.

## Overview

Unite DeFi provides a simple yet powerful API for enabling cross-chain swaps in your dApp. Whether you're building a wallet, DEX aggregator, or DeFi protocol, our SDK makes integration straightforward.

## Installation

### NPM/Yarn

```bash
# Using npm
npm install @unite-defi/sdk

# Using yarn
yarn add @unite-defi/sdk

# Using pnpm
pnpm add @unite-defi/sdk
```

### CDN

```html
<script src="https://unpkg.com/@unite-defi/sdk@latest/dist/unite.min.js"></script>
```

## Quick Start

### Basic Swap Integration

```typescript
import { UniteSDK, ChainId, TokenSymbol } from '@unite-defi/sdk';

// Initialize SDK
const unite = new UniteSDK({
  environment: 'mainnet', // or 'testnet'
  relayerUrl: 'https://api.unite-defi.com'
});

// Create a swap
async function performSwap() {
  // 1. Get quote
  const quote = await unite.getQuote({
    sourceChain: ChainId.ETHEREUM,
    destChain: ChainId.APTOS,
    tokenIn: TokenSymbol.USDC,
    tokenOut: TokenSymbol.APT,
    amountIn: '1000' // 1000 USDC
  });

  console.log(`You'll receive: ${quote.amountOut} APT`);

  // 2. Create swap order
  const order = await unite.createOrder({
    ...quote,
    userAddress: '0xYourAddress',
    slippage: 0.02 // 2% slippage
  });

  // 3. Sign order
  const signedOrder = await unite.signOrder(order);

  // 4. Submit swap
  const swap = await unite.submitSwap(signedOrder);

  // 5. Monitor status
  const status = await unite.trackSwap(swap.orderId);
  console.log('Swap status:', status);
}
```

## Core Concepts

### 1. Chain Identifiers

```typescript
enum ChainId {
  // EVM Chains
  ETHEREUM = 1,
  ARBITRUM = 42161,
  OPTIMISM = 10,
  BASE = 8453,
  POLYGON = 137,
  
  // Non-EVM Chains
  APTOS = 'aptos',
  SUI = 'sui',
  COSMOS = 'cosmoshub-4',
  STELLAR = 'stellar',
  // ... more chains
}
```

### 2. Token Addressing

```typescript
// EVM tokens use contract addresses
const USDC_ETHEREUM = '0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48';

// Non-EVM tokens use chain-specific formats
const APT_APTOS = '0x1::aptos_coin::AptosCoin';
const SUI_TOKEN = '0x2::sui::SUI';
```

### 3. Order Structure

```typescript
interface SwapOrder {
  orderId: string;
  userAddress: string;
  sourceChain: ChainId;
  destChain: ChainId;
  tokenIn: string;
  tokenOut: string;
  amountIn: string;
  minAmountOut: string;
  maxAmountOut: string;
  secretHash: string;
  deadline: number;
  nonce: number;
}
```

## Advanced Features

### Custom Relayer Configuration

```typescript
const unite = new UniteSDK({
  relayerUrl: 'https://custom-relayer.com',
  wsUrl: 'wss://custom-relayer.com/ws',
  timeout: 30000,
  retries: 3
});
```

### WebSocket Subscriptions

```typescript
// Subscribe to order updates
unite.subscribe('order.updated', (event) => {
  console.log('Order update:', event);
});

// Subscribe to specific order
unite.subscribeToOrder(orderId, (status) => {
  console.log('Status changed:', status);
  
  if (status === 'COMPLETED') {
    console.log('Swap completed!');
  }
});
```

### Resolver Integration

Build your own resolver to provide liquidity:

```typescript
import { ResolverSDK } from '@unite-defi/resolver-sdk';

const resolver = new ResolverSDK({
  privateKey: process.env.RESOLVER_PRIVATE_KEY,
  chains: [ChainId.ETHEREUM, ChainId.APTOS]
});

// Monitor profitable opportunities
resolver.on('opportunity', async (order) => {
  const profit = calculateProfit(order);
  
  if (profit > MIN_PROFIT_THRESHOLD) {
    await resolver.commitToOrder(order);
  }
});

// Handle order execution
resolver.on('committed', async (commitment) => {
  // Deploy escrows
  await resolver.deployEscrows(commitment);
  
  // Deposit funds
  await resolver.depositFunds(commitment);
  
  // Wait for secret and claim
  await resolver.waitAndClaim(commitment);
});
```

## Testing

### Using Testnets

```typescript
const unite = new UniteSDK({
  environment: 'testnet',
  chains: {
    ethereum: 'sepolia',
    arbitrum: 'arbitrum-sepolia',
    aptos: 'testnet'
  }
});

// Get test tokens
const faucets = unite.getTestnetFaucets();
console.log('Get test tokens:', faucets);
```

### Mock Mode

```typescript
const unite = new UniteSDK({
  mock: true // Simulates swaps without blockchain interaction
});

// All methods work the same but return mock data
const swap = await unite.createOrder({...});
// Returns immediately with mock success
```

## Error Handling

```typescript
import { UniteError, ErrorCode } from '@unite-defi/sdk';

try {
  const swap = await unite.submitSwap(order);
} catch (error) {
  if (error instanceof UniteError) {
    switch (error.code) {
      case ErrorCode.INSUFFICIENT_LIQUIDITY:
        console.error('No resolvers available');
        break;
      case ErrorCode.SLIPPAGE_EXCEEDED:
        console.error('Price moved too much');
        break;
      case ErrorCode.ORDER_EXPIRED:
        console.error('Order expired');
        break;
      default:
        console.error('Swap failed:', error.message);
    }
  }
}
```

## Best Practices

### 1. Slippage Management

```typescript
// Dynamic slippage based on volatility
const slippage = await unite.getRecommendedSlippage({
  tokenIn,
  tokenOut,
  amount
});

const order = await unite.createOrder({
  ...params,
  slippage: Math.min(slippage * 1.2, 0.05) // Max 5%
});
```

### 2. Gas Optimization

```typescript
// Check gas costs before swapping
const gasCosts = await unite.estimateGasCosts(order);

if (gasCosts.total > maxAcceptableGas) {
  // Wait for lower gas or use different route
}
```

### 3. Multi-Chain Balance Management

```typescript
// Check balances across chains
const balances = await unite.getBalances(userAddress);

// Find best source chain for swap
const bestSource = unite.findBestSourceChain({
  token: 'USDC',
  amount: '1000',
  destination: ChainId.APTOS
});
```

## UI Components

### React Integration

```tsx
import { UniteProvider, SwapWidget } from '@unite-defi/react';

function App() {
  return (
    <UniteProvider config={{ environment: 'mainnet' }}>
      <SwapWidget 
        theme="dark"
        defaultSourceChain={ChainId.ETHEREUM}
        defaultDestChain={ChainId.APTOS}
        onSwapComplete={(result) => {
          console.log('Swap completed:', result);
        }}
      />
    </UniteProvider>
  );
}
```

### Custom UI

```tsx
import { useUnite, useSwapQuote } from '@unite-defi/react';

function CustomSwap() {
  const { createSwap, trackSwap } = useUnite();
  const { quote, loading } = useSwapQuote({
    sourceChain: ChainId.ETHEREUM,
    destChain: ChainId.SUI,
    tokenIn: 'USDC',
    amountIn: '100'
  });

  return (
    <div>
      {loading ? (
        <Spinner />
      ) : (
        <div>
          You'll receive: {quote?.amountOut} SUI
          <button onClick={() => createSwap(quote)}>
            Swap Now
          </button>
        </div>
      )}
    </div>
  );
}
```

## API Rate Limits

| Endpoint | Rate Limit | Window |
|----------|------------|---------|
| Get Quote | 30 req | 1 minute |
| Create Order | 10 req | 1 minute |
| Status Check | 60 req | 1 minute |
| WebSocket | 1 connection | Per IP |

## Support & Resources

### Documentation
- [API Reference](../api/relayer-api.md)
- [Smart Contracts](../technical/contract-reference.md)
- [Integration Examples](https://github.com/unite-defi/examples)

### Community
- [Discord](https://discord.gg/unite-defi)
- [GitHub](https://github.com/unite-defi)
- [Twitter](https://twitter.com/unitedefi)

### Getting Help
- Technical issues: [GitHub Issues](https://github.com/unite-defi/sdk/issues)
- Integration support: dev@unite-defi.com
- Security concerns: security@unite-defi.com

## Changelog

### v1.0.0
- Initial release
- Support for 26 chains
- TypeScript SDK
- React components

### Coming Soon
- Advanced routing algorithms
- Limit orders
- Batch swaps
- Mobile SDKs (React Native, Flutter)