# System Architecture Overview

Unite DeFi is built on a modular, scalable architecture that enables trustless cross-chain swaps across diverse blockchain ecosystems.

## High-Level Architecture

<figure><img src="../.gitbook/assets/architecture-overview.png" alt=""><figcaption><p>Unite DeFi System Architecture</p></figcaption></figure>

## Core Components

### 1. Relayer Service

The orchestration layer that manages the entire swap lifecycle:

```typescript
// Core Relayer responsibilities
interface RelayerService {
  // Order management
  createSwapOrder(params: SwapParams): Order;
  broadcastToResolvers(order: Order): void;
  
  // Escrow coordination
  deployUserEscrow(order: Order): void;
  transferUserFunds(order: Order): void;
  
  // Secret management
  revealSecret(orderId: string): void;
  
  // Monitoring
  trackOrderStatus(orderId: string): OrderStatus;
}
```

**Key Features:**
- Gasless transactions for users
- Order validation and signing
- Dutch auction orchestration
- Secret revelation timing
- Multi-chain monitoring

### 2. Resolver Network

Decentralized network of liquidity providers:

```typescript
// Resolver participation flow
interface Resolver {
  // Monitor and commit
  monitorOrders(): void;
  evaluateProfitability(order: Order): boolean;
  commitToOrder(order: Order): Commitment;
  
  // Execute swap
  deployEscrows(commitment: Commitment): void;
  depositFunds(escrow: Address): void;
  claimFunds(secret: string): void;
}
```

**Resolver Characteristics:**
- Permissionless participation
- Automated or manual operation
- Multi-chain inventory management
- Risk management systems

### 3. Smart Contract Layer

Chain-specific implementations maintaining consistent interfaces:

#### EVM Implementation (Solidity)
```solidity
contract UniteEscrow {
    struct SwapData {
        address token;
        uint256 amount;
        address recipient;
        bytes32 secretHash;
        uint256 deadline;
    }
    
    function deposit(SwapData memory data) external payable;
    function withdraw(bytes32 secret) external;
    function cancel() external;
}
```

#### Move Implementation (Aptos/Sui)
```move
module unite::escrow {
    struct Escrow<phantom CoinType> {
        amount: u64,
        recipient: address,
        secret_hash: vector<u8>,
        deadline: u64,
    }
    
    public fun deposit<CoinType>(...);
    public fun withdraw<CoinType>(...);
    public fun cancel<CoinType>(...);
}
```

### 4. User Interface Layer

Three specialized interfaces for different user types:

1. **Swap Interface**: End-user trading interface
2. **Logs Dashboard**: Real-time monitoring for resolvers
3. **Landing Page**: Educational and onboarding

## Data Flow

### 1. Order Creation Flow
```
User → UI → Relayer API → Order Validation → Database → Event Stream
```

### 2. Resolver Commitment Flow
```
Event Stream → Resolver → Profitability Check → Commitment → Relayer
```

### 3. Execution Flow
```
Relayer → Source Chain → Escrow Deploy → Fund Transfer → Secret Reveal
Resolver → Destination Chain → Escrow Deploy → Fund Transfer → Claim
```

## Technology Stack

### Backend Services
- **Runtime**: Node.js with TypeScript
- **Framework**: Express.js
- **Database**: DynamoDB
- **Message Queue**: AWS SQS
- **Deployment**: Docker + PM2

### Blockchain Integration
- **EVM**: Ethers.js v6
- **Aptos**: Aptos TypeScript SDK
- **Sui**: Sui TypeScript SDK
- **Cosmos**: CosmJS
- **Multi-chain**: Custom adapters per chain

### Frontend
- **Framework**: Next.js 14
- **Styling**: Tailwind CSS
- **State Management**: React Context + Hooks
- **Wallet Integration**: RainbowKit + Custom Adapters

## Scalability Considerations

### Horizontal Scaling
- Stateless relayer design
- Multiple resolver instances
- Load-balanced API endpoints
- Distributed order matching

### Performance Optimizations
- Efficient order broadcasting
- Batched blockchain queries
- Caching layer for chain data
- Optimized gas usage

## Security Architecture

### Multi-Layer Security
1. **Protocol Level**: Atomic swaps via HTLCs
2. **Economic Level**: Safety deposits and incentives
3. **Implementation Level**: Audited smart contracts
4. **Operational Level**: Monitoring and alerts

### Trust Model
- **Trustless**: No custody of user funds
- **Non-custodial**: Direct user-to-resolver swaps
- **Decentralized**: No single point of failure
- **Transparent**: All transactions on-chain

## Integration with 1inch Fusion

Unite DeFi leverages 1inch Fusion Extensions for:

```typescript
// Fusion integration points
interface FusionExtension {
  // Order standardization
  createFusionOrder(params: UniteParams): FusionOrder;
  
  // Signature schemes
  signOrder(order: FusionOrder): SignedOrder;
  
  // Settlement logic
  settleOrder(order: SignedOrder): SettlementResult;
}
```

**Benefits:**
- Battle-tested order format
- Proven signature schemes
- Gas-efficient settlement
- Existing resolver ecosystem

## Monitoring & Observability

### Metrics Tracked
- Order volume and success rates
- Resolver performance metrics
- Chain-specific latencies
- Gas consumption patterns

### Logging Infrastructure
- Structured logging with context
- Distributed tracing
- Real-time alerting
- Historical analysis

## Future Architecture Enhancements

### Planned Improvements
1. **ZK Proof Integration**: Privacy-preserving swaps
2. **Aggregated Liquidity**: Multi-resolver order filling
3. **Advanced Routing**: Multi-hop swap optimization
4. **Layer 2 Scaling**: Rollup-specific optimizations

### Modular Extensions
- Plugin system for new chains
- Custom resolver strategies
- Advanced order types
- Liquidity aggregation

## Next Steps

- Dive into [Cross-Chain Protocol](cross-chain-protocol.md) details
- Understand the [Relayer Service](relayer-service.md) implementation
- Explore [Smart Contracts](smart-contracts.md) for each chain
- Learn about the [Security Model](security-model.md)