# Key Features

Unite DeFi offers a comprehensive suite of features that make it the most advanced cross-chain swap protocol in the ecosystem.

## 🌐 Universal Chain Support

### 26+ Blockchains
Unite DeFi connects more blockchains than any other protocol:
- **10 Non-EVM chains**: Aptos, Sui, Cosmos, Stellar, TON, and more
- **16+ EVM chains**: Ethereum, L2s, and alternative L1s
- **Unified interface**: One API, one experience, all chains

### True Interoperability
- Swap between any supported chains
- No wrapped tokens or synthetic assets
- Native token support on each chain

## 🔒 Trustless Architecture

### Atomic Swaps
- **Hash Time-Locked Contracts (HTLCs)**: Cryptographically guaranteed execution
- **No intermediaries**: Direct peer-to-peer swaps via resolvers
- **No custody risk**: Funds never held by the protocol

### Security First
- Audited smart contracts
- Economic incentives align all participants
- Time-locked escrows prevent indefinite locks
- Rescue mechanisms ensure completion

## ⚡ Superior User Experience

### Gasless Transactions
- Users don't need native tokens on source chain
- Relayer handles gas payments
- One-click swaps without gas management

### Fast Execution
- Average swap time: 2-5 minutes
- Optimized for each chain's characteristics
- Parallel processing for efficiency

### Simple Integration
- Connect wallet and swap
- No bridge tokens to manage
- No complex multi-step processes

## 💰 Efficient Pricing

### Dutch Auction Mechanism
<figure><img src="../.gitbook/assets/dutch-auction.png" alt=""><figcaption><p>Price discovery through competition</p></figcaption></figure>

- **Competitive pricing**: Resolvers compete for orders
- **Market-driven rates**: Best execution prices
- **No price manipulation**: Transparent auction process
- **Slippage protection**: Set your acceptable range

### Low Fees
- Minimal protocol fees
- Competitive resolver margins
- Gas-optimized contracts
- Batch processing capabilities

## 🤖 Advanced Resolver Network

### Permissionless Participation
- Anyone can become a resolver
- No KYC or approval process
- Stake collateral and start earning

### Automated Market Making
- Programmatic order evaluation
- Risk management tools
- Portfolio rebalancing opportunities
- Cross-chain arbitrage

### Safety Deposits
- Resolvers stake collateral
- Ensures good behavior
- Protects users from griefing
- Creates reliable execution

## 🔧 Developer-Friendly

### Comprehensive SDK
```typescript
// Simple integration
const swap = await unite.createSwap({
  from: 'ethereum',
  to: 'aptos',
  amount: '1000 USDC'
});
```

### Multiple Integration Options
- JavaScript/TypeScript SDK
- REST API
- WebSocket subscriptions
- React components

### Extensive Documentation
- Step-by-step guides
- API references
- Code examples
- Video tutorials

## 📊 Real-Time Monitoring

### Logs Dashboard
<figure><img src="../.gitbook/assets/logs-dashboard.png" alt=""><figcaption><p>Monitor all network activity</p></figcaption></figure>

- Track all swaps in real-time
- Monitor resolver performance
- View historical data
- Analyze trade patterns

### WebSocket Events
- Order updates
- Price changes
- Completion notifications
- Network statistics

## 🌟 1inch Fusion Integration

### Battle-Tested Infrastructure
- Leverages 1inch's proven technology
- Inherits security best practices
- Benefits from optimization research
- Access to resolver ecosystem

### Fusion Extensions
- Extended order types
- Advanced signature schemes
- Gas-efficient settlement
- Compatibility with 1inch tools

## 🚀 Scalability

### Horizontal Scaling
- Stateless architecture
- Multiple relayer instances
- Distributed resolver network
- Cloud-native deployment

### High Throughput
- Handle thousands of swaps
- Parallel order processing
- Efficient state management
- Optimized for growth

## 🔄 Flexible Order Types

### Market Orders
- Immediate execution
- Best available price
- Simple and fast

### Limit Orders (Coming Soon)
- Set your desired rate
- Execute when profitable
- No constant monitoring

### Batch Swaps (Coming Soon)
- Multiple swaps in one transaction
- Reduced gas costs
- Portfolio rebalancing

## 🛡️ Risk Management

### Slippage Protection
- Set maximum acceptable slippage
- Automatic cancellation if exceeded
- Real-time price updates

### Timeout Protection
- Orders expire after set time
- Funds automatically returned
- No indefinite locks

### Rescue Mechanism
- Backup resolvers can complete swaps
- Ensures high success rate
- Protects against resolver failure

## 🌈 Multi-Wallet Support

### EVM Wallets
- MetaMask
- WalletConnect
- Coinbase Wallet
- Rainbow
- And more...

### Non-EVM Wallets
- Petra (Aptos)
- Sui Wallet
- Keplr (Cosmos)
- Phantom (Solana)
- And more...

## 📈 Future Features

### Advanced Routing
- Multi-hop swaps
- Liquidity aggregation
- Optimal path finding

### Privacy Features
- ZK-proof integration
- Private swaps
- Shielded amounts

### DeFi Integrations
- Lending protocol bridges
- Yield farming across chains
- Automated strategies

## Summary

Unite DeFi combines cutting-edge technology with user-friendly design to create the most comprehensive cross-chain swap protocol. Whether you're a user looking for simple swaps, a developer building cross-chain applications, or a liquidity provider seeking opportunities, Unite DeFi has the features you need.

Ready to experience these features? [Get Started](../getting-started/quickstart.md) now!