# Supported Chains

Unite DeFi supports an unprecedented range of blockchain networks, connecting EVM and non-EVM ecosystems seamlessly. Here's our comprehensive chain support:

## 🌐 Total Networks: 26+

<figure><img src="../.gitbook/assets/supported-chains-map.png" alt=""><figcaption><p>Unite DeFi's Multi-Chain Universe</p></figcaption></figure>

## Non-EVM Chains

### Move-Based Chains

#### [Aptos](non-evm/aptos.md)
- **Type**: Layer 1, Move VM
- **Features**: Parallel execution, sub-second finality
- **Tokens**: APT, USDC, USDT
- **Wallet**: Petra, Martian, Pontem
- **Status**: ✅ Mainnet

#### [Sui](non-evm/sui.md)
- **Type**: Layer 1, Move VM
- **Features**: Object-centric model, horizontal scaling
- **Tokens**: SUI, USDC, USDT
- **Wallet**: Sui Wallet, Martian, Ethos
- **Status**: ✅ Mainnet

### Cosmos Ecosystem

#### [Osmosis](non-evm/cosmos.md#osmosis)
- **Type**: Cosmos App Chain
- **Features**: DEX-specific chain, superfluid staking
- **Tokens**: OSMO, ATOM, USDC
- **Wallet**: Keplr, Leap
- **Status**: ✅ Mainnet

#### [Secret Network](non-evm/cosmos.md#secret-network)
- **Type**: Privacy-focused Cosmos chain
- **Features**: Encrypted smart contracts
- **Tokens**: SCRT, sSCRT
- **Wallet**: Keplr, Leap
- **Status**: ✅ Mainnet

### Payment-Focused Chains

#### [Stellar](non-evm/stellar.md)
- **Type**: Payment network
- **Features**: Fast settlements, built-in DEX
- **Tokens**: XLM, USDC, Various anchored assets
- **Wallet**: Freighter, Albedo
- **Status**: ✅ Mainnet

#### [XRP Ledger](non-evm/xrp.md)
- **Type**: Payment & DeFi
- **Features**: Built-in DEX, payment channels
- **Tokens**: XRP, Issued currencies
- **Wallet**: Xumm, Gem Wallet
- **Status**: ✅ Mainnet

### Smart Contract Platforms

#### [Cardano](non-evm/cardano.md)
- **Type**: Layer 1, UTXO-based
- **Features**: Plutus smart contracts, Hydra L2
- **Tokens**: ADA, Native tokens
- **Wallet**: Nami, Eternl, Yoroi
- **Status**: ✅ Mainnet

#### [TON](non-evm/ton.md)
- **Type**: Layer 1, Sharded
- **Features**: Infinite sharding, async messaging
- **Tokens**: TON, Jettons
- **Wallet**: Tonkeeper, OpenMask
- **Status**: ✅ Mainnet

#### [Near](non-evm/near.md)
- **Type**: Layer 1, Sharded
- **Features**: Human-readable accounts, meta-transactions
- **Tokens**: NEAR, NEP-141 tokens
- **Wallet**: Near Wallet, Meteor
- **Status**: ✅ Mainnet

#### [Internet Computer](non-evm/icp.md)
- **Type**: World Computer
- **Features**: Web-speed, reverse gas model
- **Tokens**: ICP, ICRC tokens
- **Wallet**: Plug, Stoic
- **Status**: ✅ Mainnet

#### [Starknet](non-evm/starknet.md)
- **Type**: ZK-Rollup
- **Features**: Cairo VM, STARK proofs
- **Tokens**: STRK, ETH
- **Wallet**: Argent X, Braavos
- **Status**: ✅ Mainnet

## EVM Chains

### Ethereum & Layer 2s

#### [Ethereum](evm/ethereum-l2s.md#ethereum)
- **Type**: Layer 1
- **Features**: Largest DeFi ecosystem
- **Status**: ✅ Mainnet

#### [Arbitrum](evm/ethereum-l2s.md#arbitrum)
- **Type**: Optimistic Rollup
- **Features**: EVM compatible, low fees
- **Status**: ✅ Mainnet

#### [Optimism](evm/ethereum-l2s.md#optimism)
- **Type**: Optimistic Rollup
- **Features**: EVM equivalent
- **Status**: ✅ Mainnet

#### [Base](evm/ethereum-l2s.md#base)
- **Type**: Optimistic Rollup
- **Features**: Coinbase's L2
- **Status**: ✅ Mainnet

#### [Polygon](evm/ethereum-l2s.md#polygon)
- **Type**: Sidechain/L2
- **Features**: High throughput
- **Status**: ✅ Mainnet

### Alternative Layer 1s

#### [BNB Chain](evm/alt-l1s.md#bnb-chain)
- **Type**: EVM Layer 1
- **Features**: High throughput, low fees
- **Status**: ✅ Mainnet

#### [Avalanche](evm/alt-l1s.md#avalanche)
- **Type**: EVM Layer 1
- **Features**: Subnets, sub-second finality
- **Status**: ✅ Mainnet

### Sponsor Chains

#### [Monad](evm/emerging.md#monad)
- **Type**: High-performance EVM
- **Features**: 10,000 TPS, 1s blocks
- **Status**: 🚧 Testnet

#### [Aurora](evm/emerging.md#aurora)
- **Type**: Near EVM
- **Features**: Near's EVM layer
- **Status**: ✅ Mainnet

#### [Etherlink](evm/emerging.md#etherlink)
- **Type**: Tezos EVM
- **Features**: Tezos's EVM layer
- **Status**: 🚧 Testnet

#### [Sei](evm/emerging.md#sei)
- **Type**: Cosmos EVM
- **Features**: Parallel EVM execution
- **Status**: ✅ Mainnet

#### [Injective](evm/emerging.md#injective)
- **Type**: Cosmos chain with EVM
- **Features**: MEV-resistant, order book
- **Status**: ✅ Mainnet

#### [Tron](evm/emerging.md#tron)
- **Type**: Alternative EVM
- **Features**: High throughput, low fees
- **Status**: ✅ Mainnet

### Additional EVM Chains

- **Unichain**: Uniswap's upcoming L2
- **Scroll**: ZK-rollup
- **Celo**: Mobile-first blockchain

## Chain Status Legend

- ✅ **Mainnet**: Fully operational on mainnet
- 🚧 **Testnet**: Available on testnet only
- 🔜 **Coming Soon**: Integration in progress

## Integration Features by Chain

### Universal Features
- ✅ Atomic Swaps (HTLC)
- ✅ Dutch Auction Pricing
- ✅ Safety Deposits
- ✅ Gasless Transactions

### Chain-Specific Optimizations
- **EVM Chains**: CREATE2 deterministic addresses
- **Move Chains**: Resource-oriented escrows
- **Cosmos**: IBC compatibility
- **UTXO Chains**: Script-based locks

## Adding New Chains

Unite DeFi's modular architecture makes it easy to add new chains:

1. **Requirements**:
   - Smart contract capability (or scripting)
   - Time-lock functionality
   - Hash verification
   - Atomic operations

2. **Integration Time**: ~1-2 weeks per chain

3. **Contact**: Reach out for chain integration

## Performance Metrics

| Chain | Avg Swap Time | Success Rate | Gas Cost |
|-------|---------------|--------------|----------|
| Ethereum | 3-5 min | 99.5% | $5-20 |
| Arbitrum | 2-3 min | 99.8% | $0.50-2 |
| Polygon | 2-3 min | 99.7% | $0.01-0.10 |
| Aptos | 1-2 min | 99.9% | $0.01-0.05 |
| Sui | 1-2 min | 99.9% | $0.01-0.05 |
| Cosmos | 2-3 min | 99.6% | $0.01-0.10 |

## Next Steps

- Explore specific [Non-EVM chains](non-evm/README.md)
- Learn about [EVM chains](evm/README.md)
- Start swapping on [Unite DeFi](https://app.unite-defi.com)