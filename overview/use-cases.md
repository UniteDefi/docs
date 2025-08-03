# Use Cases

Unite DeFi enables a wide range of cross-chain use cases that were previously impossible or required complex multi-step processes. Here are the key scenarios where Unite DeFi shines:

## 🏦 Cross-Chain DeFi

### Yield Farming Optimization

<figure><img src="../.gitbook/assets/yield-farming-flow.png" alt=""><figcaption><p>Chase yields across chains seamlessly</p></figcaption></figure>

**Scenario**: APY on Aptos lending is 15%, but your funds are on Ethereum.

**Traditional Way**:
1. Bridge ETH to wrapped token
2. Wait for bridge confirmation (30+ minutes)
3. Swap wrapped token on Aptos
4. Deposit into lending protocol
5. Complex unwinding process

**Unite DeFi Way**:
1. Single swap: ETH (Ethereum) → APT (Aptos)
2. 3-5 minute completion
3. Native APT ready for DeFi
4. No wrapped tokens or bridges

### Multi-Chain Portfolio Management

```typescript
// Rebalance portfolio across chains
const rebalance = await unite.batchSwap([
  { from: 'ethereum', token: 'USDC', amount: '5000', to: 'arbitrum' },
  { from: 'polygon', token: 'MATIC', amount: '1000', to: 'sui' },
  { from: 'bnb', token: 'BNB', amount: '10', to: 'aptos' }
]);
```

## 💱 Arbitrage Opportunities

### Cross-Chain Price Differences

**Example**: USDC/APT price discrepancy
- Ethereum: 1 USDC = 0.1 APT
- Aptos: 1 USDC = 0.095 APT

**Arbitrage Flow**:
1. Buy APT with USDC on Aptos
2. Swap APT to USDC on Ethereum via Unite DeFi
3. Profit from price difference
4. Automated via resolver bots

### Market Making

Resolvers act as cross-chain market makers:
- Provide liquidity across chains
- Earn fees on spreads
- Balance inventory automatically
- No impermanent loss risk

## 🎮 Gaming & NFTs

### Cross-Chain Gaming Assets

<figure><img src="../.gitbook/assets/gaming-assets.png" alt=""><figcaption><p>Move gaming assets between chains</p></figcaption></figure>

**Use Case**: Move gaming tokens between chains
- Play on Polygon for low fees
- Trade items on Ethereum for liquidity
- Store value on Bitcoin L2s
- All with native tokens

### NFT Trading

**Scenario**: Buy NFT on Ethereum with tokens from Sui

1. Swap SUI → ETH via Unite DeFi
2. ETH arrives in your Ethereum wallet
3. Purchase NFT directly
4. No wrapped tokens or bridges

## 🏢 Enterprise Use Cases

### Cross-Border Payments

**Traditional**: Multiple intermediaries, 3-5 days, high fees

**Unite DeFi**: 
- Convert stablecoins across chains
- Settlement in minutes
- Transparent fees
- No intermediary risk

### Treasury Management

Enterprises managing multi-chain treasuries:
```typescript
// Move funds to chain with best yield
const optimization = await unite.findBestYield({
  token: 'USDC',
  amount: '1000000',
  acceptableChains: ['ethereum', 'arbitrum', 'polygon', 'aptos']
});

await unite.moveToOptimalChain(optimization);
```

## 👤 Personal Finance

### Remittances

**Example**: Send money from US to Philippines
1. Sender: USD → USDC on Ethereum
2. Unite DeFi: USDC (Ethereum) → PHP stablecoin (Stellar)
3. Recipient: Receives PHP stablecoin
4. Total time: 5 minutes vs days

### Multi-Chain Savings

Optimize savings across chains:
- High-yield stablecoin farms
- Native staking opportunities
- Risk diversification
- Easy rebalancing

## 🛍️ E-Commerce

### Accept Any Token

Merchants can accept any token from any chain:
```typescript
// Merchant integration
const payment = await unite.acceptPayment({
  amount: '99.99 USD',
  acceptedTokens: ['any'], // Accept any token
  settlementToken: 'USDC',
  settlementChain: 'polygon'
});
```

### Cross-Chain Subscriptions

- User pays with tokens on their preferred chain
- Merchant receives payment on their preferred chain
- Automatic monthly conversions
- No manual bridge management

## 🔧 Developer Scenarios

### Multi-Chain dApps

Build applications that work across all chains:
```typescript
// User on any chain can interact
async function crossChainAction(userChain, userToken) {
  // Convert to required token/chain
  const required = await unite.swap({
    from: userChain,
    token: userToken,
    to: 'aptos',
    targetToken: 'APT'
  });
  
  // Execute action with native tokens
  await myProtocol.execute(required);
}
```

### Liquidity Aggregation

Aggregate liquidity from all chains:
- Access Ethereum's deep liquidity
- Utilize Solana's speed
- Leverage Cosmos's ecosystem
- All through one interface

## 🌐 DAO Operations

### Cross-Chain Governance

**Scenario**: DAO with members on different chains

1. Members hold governance tokens on various chains
2. Voting requires tokens on Ethereum
3. Unite DeFi enables participation without bridges
4. Democratic access for all members

### Treasury Diversification

DAOs can efficiently manage multi-chain treasuries:
- Diversify holdings across chains
- Access best yield opportunities
- Pay contributors on their preferred chains
- Maintain decentralization

## 📊 Real-World Examples

### Example 1: DeFi Power User

**Sarah** manages a $100k DeFi portfolio:
- Morning: Moves funds from Ethereum to Aptos for 20% APY
- Afternoon: Arbitrages price differences between Sui and Polygon
- Evening: Consolidates profits back to Ethereum
- All through Unite DeFi's simple interface

### Example 2: Web3 Game Studio

**GameFi Studio** operates across chains:
- Game runs on Polygon (low fees)
- NFTs traded on Ethereum (liquidity)
- Rewards distributed on Aptos (speed)
- Unite DeFi handles all token movements

### Example 3: International Business

**TechCorp** pays global contractors:
- Receives revenue in USDC on Ethereum
- Pays US contractors in USDC on Arbitrum
- Pays Asian contractors in stablecoins on Stellar
- Pays European contractors in EUR stablecoins on Polygon
- One platform, multiple chains, simple accounting

## 🚀 Future Use Cases

### Automated Strategies

Coming soon:
- Cross-chain yield optimization bots
- Automated portfolio rebalancing
- Risk-adjusted position management
- AI-driven chain selection

### Social Features

Planned features:
- Cross-chain token gifting
- Social trading across chains
- DAO token airdrops any chain
- Community rewards distribution

## Why These Use Cases Matter

Unite DeFi transforms these use cases from complex multi-day processes into simple, single transactions. This unlocks:

1. **Capital Efficiency**: Move funds where they're most productive
2. **User Freedom**: Use any chain without lock-in
3. **Innovation**: Build apps impossible before
4. **Global Access**: Financial services for everyone

Ready to explore these use cases? [Start swapping](../getting-started/quickstart.md) or [integrate Unite DeFi](../technical/developer-guide.md) into your application!