# Quick Start Guide

Get started with Unite DeFi in under 5 minutes! This guide will walk you through making your first cross-chain swap.

## Prerequisites

Before you begin, make sure you have:

1. **A Web3 Wallet**: MetaMask, Phantom, Keplr, or any supported wallet
2. **Some Tokens**: On any supported chain (even testnet tokens work!)
3. **A Modern Browser**: Chrome, Firefox, Safari, or Brave

## Step 1: Connect Your Wallet

<figure><img src="../.gitbook/assets/connect-wallet.png" alt=""><figcaption><p>Connect your preferred wallet</p></figcaption></figure>

1. Visit [Unite DeFi Swap Interface](https://app.unite-defi.com)
2. Click "Connect Wallet" in the top right
3. Select your wallet type:
   - **EVM Wallets**: MetaMask, WalletConnect, Coinbase Wallet
   - **Aptos**: Petra, Martian, Pontem
   - **Sui**: Sui Wallet, Martian, Ethos
   - **Cosmos**: Keplr, Leap
   - **And more...**

## Step 2: Select Your Swap

<figure><img src="../.gitbook/assets/select-swap.png" alt=""><figcaption><p>Choose source and destination</p></figcaption></figure>

1. **Source Chain & Token**:
   - Select your source blockchain
   - Choose the token you want to swap
   - Enter the amount

2. **Destination Chain & Token**:
   - Select your destination blockchain
   - Choose the token you want to receive
   - See estimated output amount

## Step 3: Review & Approve

<figure><img src="../.gitbook/assets/review-swap.png" alt=""><figcaption><p>Review swap details</p></figcaption></figure>

1. **Review Details**:
   - Exchange rate
   - Estimated fees
   - Minimum received amount
   - Estimated completion time

2. **Approve Token** (first time only):
   - Click "Approve Token"
   - Confirm in your wallet
   - Wait for confirmation

## Step 4: Execute Swap

<figure><img src="../.gitbook/assets/execute-swap.png" alt=""><figcaption><p>Sign and submit your swap</p></figcaption></figure>

1. Click "Swap" button
2. Sign the order in your wallet
3. Transaction is submitted automatically
4. No gas fees required on source chain!

## Step 5: Track Your Swap

<figure><img src="../.gitbook/assets/track-swap.png" alt=""><figcaption><p>Monitor swap progress</p></figcaption></figure>

Your swap progresses through these stages:
1. ⏳ **Order Created**: Your order is being broadcast
2. 📢 **Dutch Auction**: Resolvers are bidding
3. ✅ **Resolver Committed**: A resolver accepted your order
4. 🔒 **Funds Locked**: Both escrows are funded
5. 🔓 **Secret Revealed**: Swap is completing
6. ✨ **Completed**: Tokens arrived at destination!

## Example Swaps to Try

### Testnet Swaps (Free tokens!)

1. **Ethereum Sepolia → Aptos Testnet**
   - Get ETH from [Sepolia Faucet](https://sepoliafaucet.com)
   - Swap to APT on Aptos testnet

2. **Polygon Mumbai → Sui Testnet**
   - Get MATIC from [Mumbai Faucet](https://mumbaifaucet.com)
   - Swap to SUI on Sui testnet

### Popular Mainnet Routes

1. **Ethereum → Arbitrum** (Popular L2 route)
2. **BNB Chain → Polygon** (Cross-chain DeFi)
3. **Avalanche → Cosmos** (EVM to Cosmos)

## Troubleshooting

### Common Issues

**"Insufficient Balance"**
- Ensure you have tokens on the source chain
- Check you're on the correct network

**"No Resolvers Available"**
- Try a different token pair
- Adjust your swap amount
- Wait a few moments and retry

**"Transaction Failed"**
- Check wallet connection
- Ensure token approval succeeded
- Try refreshing the page

### Need Help?

- 📚 Read the [detailed User Guide](user-guide.md)
- 🔧 Check [Troubleshooting](../resources/troubleshooting.md)
- 💬 Join our [Discord Community](https://discord.gg/unite-defi)

## What's Next?

Congratulations on your first swap! 🎉

### Explore More:
- [Understand How It Works](../overview/how-it-works.md)
- [Become a Resolver](../technical/resolver-guide.md)
- [Integrate Unite DeFi](../technical/integration-guide.md)

### Advanced Features:
- Set custom slippage tolerance
- Use limit orders (coming soon)
- Track all your swaps in the dashboard

---

> **Pro Tip**: Bookmark the [Logs Dashboard](https://app.unite-defi.com/logs) to monitor all network activity and find the best trading opportunities!