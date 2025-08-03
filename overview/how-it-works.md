# How It Works

Unite DeFi orchestrates cross-chain swaps through a sophisticated yet elegant protocol. Here's how the magic happens:

## The Swap Flow

### Step 1: User Initiates Swap

<figure><img src="../.gitbook/assets/flow-step1.png" alt=""><figcaption><p>User approves tokens and signs order</p></figcaption></figure>

1. User selects source chain, token, and amount
2. User selects destination chain and desired token
3. User approves token spending to the Relayer
4. User signs the swap order with their secret hash

### Step 2: Dutch Auction Begins

<figure><img src="../.gitbook/assets/flow-step2.png" alt=""><figcaption><p>Relayer broadcasts order to resolver network</p></figcaption></figure>

The Relayer broadcasts the order to all Resolvers with a declining price:
- Starting price: User's maximum acceptable rate
- Ending price: User's minimum acceptable rate
- Duration: Typically 30-60 seconds
- Resolvers monitor and wait for profitable pricing

### Step 3: Resolver Commits

<figure><img src="../.gitbook/assets/flow-step3.png" alt=""><figcaption><p>Resolver commits when price is attractive</p></figcaption></figure>

When the Dutch auction price becomes profitable:
1. Resolver commits to fulfill the order
2. Resolver deploys escrow contracts on both chains
3. Resolver deposits safety collateral (native tokens)
4. Commitment is recorded on-chain

### Step 4: Funds Lock in Escrows

<figure><img src="../.gitbook/assets/flow-step4.png" alt=""><figcaption><p>Both parties lock funds in escrows</p></figcaption></figure>

1. **Source Chain**: Relayer transfers user's tokens to source escrow
2. **Destination Chain**: Resolver deposits promised tokens to destination escrow
3. Both escrows are now locked with the same secret hash
4. Funds are time-locked (typically 24 hours)

### Step 5: Secret Reveal & Completion

<figure><img src="../.gitbook/assets/flow-step5.png" alt=""><figcaption><p>Secret revealed, swaps complete atomically</p></figcaption></figure>

1. Relayer reveals the secret publicly
2. Resolver uses secret to unlock source escrow (gets user's tokens)
3. User uses secret to unlock destination escrow (gets resolver's tokens)
4. Resolver recovers safety deposits from both chains
5. Swap completes successfully!

## The Key Components

### 1. Hash Time-Locked Contracts (HTLCs)

The core primitive enabling trustless swaps:

```solidity
// Simplified HTLC logic
contract Escrow {
    function withdraw(bytes32 secret) {
        require(sha256(secret) == secretHash, "Invalid secret");
        require(block.timestamp < deadline, "Expired");
        // Transfer funds to recipient
    }
    
    function cancel() {
        require(block.timestamp >= deadline, "Not expired");
        // Return funds to sender
    }
}
```

### 2. Dutch Auction Mechanism

Ensures competitive pricing through declining rates:

```typescript
function getCurrentPrice(auction) {
    const elapsed = Date.now() - auction.startTime;
    const progress = elapsed / auction.duration;
    
    return auction.startPrice - 
           (auction.startPrice - auction.endPrice) * progress;
}
```

### 3. Safety Deposits

Resolvers stake collateral to ensure good behavior:
- Prevents griefing attacks
- Incentivizes timely completion
- Covers potential gas costs
- Refunded upon successful completion

### 4. Rescue Mechanism

If a resolver fails to complete:
1. 5-minute grace period for original resolver
2. After grace period, any resolver can complete
3. Rescue resolver earns the safety deposits
4. Ensures swaps always complete

## Why It's Secure

### Atomic Guarantees
- Either both transfers happen, or neither happens
- No possibility of partial execution
- Cryptographically enforced by secret/hash mechanism

### Economic Security
- Resolvers have skin in the game (safety deposits)
- Dutch auction prevents price manipulation
- Time locks prevent indefinite fund locking

### Decentralized Execution
- No single point of failure
- Multiple resolvers compete for orders
- Permissionless participation

## Example Swap: Ethereum to Aptos

Let's trace a real swap:

1. **Alice** has 1 ETH on Ethereum, wants APT on Aptos
2. **Alice** approves 1 ETH to Relayer, signs order with secret hash
3. **Relayer** broadcasts: "1 ETH → 100-95 APT" (Dutch auction)
4. **Bob** (Resolver) commits at 97 APT when profitable
5. **Bob** deploys escrows on both chains with safety deposits
6. **Relayer** transfers Alice's 1 ETH to Ethereum escrow
7. **Bob** deposits 97 APT to Aptos escrow
8. **Relayer** reveals secret: `0x1234...`
9. **Bob** uses secret to claim 1 ETH from Ethereum escrow
10. **Alice** uses secret to claim 97 APT from Aptos escrow
11. **Bob** recovers his safety deposits
12. Swap complete! Alice has APT, Bob has ETH

## Performance Characteristics

- **Swap Time**: 2-5 minutes typical
- **Gas Efficiency**: Optimized contracts minimize costs
- **Success Rate**: >99% with rescue mechanism
- **Supported Volume**: No theoretical limit

## Next Steps

Now that you understand how Unite DeFi works:
- See it in action with our [User Guide](../getting-started/user-guide.md)
- Dive deeper into the [Architecture](../architecture/overview.md)
- Learn about [becoming a Resolver](../technical/resolver-guide.md)