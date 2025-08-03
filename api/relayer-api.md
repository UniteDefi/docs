# Relayer API Reference

The Relayer API is the core orchestration service for Unite DeFi cross-chain swaps. It manages order lifecycle, coordinates with resolvers, and handles secret revelation.

## Base URL

```
Production: https://api.unite-defi.com
Testnet: https://testnet-api.unite-defi.com
```

## Authentication

Currently, the API is open for public use. API keys will be introduced in future versions.

## Endpoints

### Create Swap Order

Create a new cross-chain swap order.

```http
POST /api/create-swap
```

#### Request Body

```json
{
  "userAddress": "0x742d35Cc6634C0532925a3b844Bc9e7595f6E123",
  "sourceChain": "ethereum",
  "destChain": "aptos",
  "tokenIn": "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
  "tokenOut": "0x1::aptos_coin::AptosCoin",
  "amountIn": "1000000000",
  "minAmountOut": "95000000",
  "maxAmountOut": "100000000",
  "userSignature": "0x...",
  "userSecretHash": "0x9c22ff5f21f0b81b113e63f7db6da94fe4e5b3dc"
}
```

#### Response

```json
{
  "orderId": "550e8400-e29b-41d4-a716-446655440000",
  "status": "CREATED",
  "dutchAuction": {
    "startPrice": "100000000",
    "endPrice": "95000000",
    "startTime": 1704067200,
    "endTime": 1704067260
  },
  "expiryTime": 1704153600
}
```

### Get Order Status

Retrieve the current status of a swap order.

```http
GET /api/order-status/:orderId
```

#### Response

```json
{
  "orderId": "550e8400-e29b-41d4-a716-446655440000",
  "status": "RESOLVER_COMMITTED",
  "userAddress": "0x742d35Cc6634C0532925a3b844Bc9e7595f6E123",
  "resolver": "0x853f35Cc6634C0532925a3b844Bc9e7595f6E456",
  "sourceChain": "ethereum",
  "destChain": "aptos",
  "tokenIn": "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48",
  "tokenOut": "0x1::aptos_coin::AptosCoin",
  "amountIn": "1000000000",
  "amountOut": "97500000",
  "createdAt": 1704067200,
  "updatedAt": 1704067245
}
```

### Commit as Resolver

Commit to fulfill a swap order as a resolver.

```http
POST /api/commit-resolver
```

#### Request Body

```json
{
  "orderId": "550e8400-e29b-41d4-a716-446655440000",
  "resolverAddress": "0x853f35Cc6634C0532925a3b844Bc9e7595f6E456",
  "signature": "0x...",
  "committedAmount": "97500000"
}
```

#### Response

```json
{
  "success": true,
  "commitment": {
    "orderId": "550e8400-e29b-41d4-a716-446655440000",
    "resolver": "0x853f35Cc6634C0532925a3b844Bc9e7595f6E456",
    "committedAmount": "97500000",
    "commitTime": 1704067245,
    "status": "COMMITTED"
  }
}
```

### Notify Escrows Ready

Notify that escrow contracts have been deployed and funded.

```http
POST /api/escrows-ready
```

#### Request Body

```json
{
  "orderId": "550e8400-e29b-41d4-a716-446655440000",
  "sourceEscrow": "0x123...",
  "destEscrow": "0x456...",
  "sourceTxHash": "0xabc...",
  "destTxHash": "0xdef..."
}
```

### Get Resolver Orders

Get all orders available for resolvers.

```http
GET /api/resolver-orders
```

#### Query Parameters

- `status` (optional): Filter by order status
- `sourceChain` (optional): Filter by source chain
- `destChain` (optional): Filter by destination chain
- `minAmount` (optional): Minimum order amount

#### Response

```json
{
  "orders": [
    {
      "orderId": "550e8400-e29b-41d4-a716-446655440000",
      "sourceChain": "ethereum",
      "destChain": "aptos",
      "tokenIn": "USDC",
      "tokenOut": "APT",
      "amountIn": "1000000000",
      "currentPrice": "98750000",
      "dutchAuction": {
        "startPrice": "100000000",
        "endPrice": "95000000",
        "remainingTime": 15
      }
    }
  ]
}
```

### Reveal Secret

Reveal the secret for a completed order (called by relayer).

```http
POST /api/reveal-secret
```

#### Request Body

```json
{
  "orderId": "550e8400-e29b-41d4-a716-446655440000",
  "secret": "0x7465737453656372657456616c7565313233"
}
```

## Order Status Values

| Status | Description |
|--------|-------------|
| `CREATED` | Order created and being broadcast |
| `DUTCH_AUCTION` | In Dutch auction phase |
| `RESOLVER_COMMITTED` | Resolver committed to order |
| `ESCROWS_DEPLOYED` | Escrow contracts deployed |
| `FUNDS_LOCKED` | Funds locked in escrows |
| `SECRET_REVEALED` | Secret revealed by relayer |
| `COMPLETED` | Swap completed successfully |
| `CANCELLED` | Order cancelled |
| `EXPIRED` | Order expired without completion |

## Error Responses

### 400 Bad Request

```json
{
  "error": "INVALID_PARAMETERS",
  "message": "Invalid token address format",
  "details": {
    "field": "tokenIn",
    "value": "invalid-address"
  }
}
```

### 404 Not Found

```json
{
  "error": "ORDER_NOT_FOUND",
  "message": "Order with ID 550e8400-e29b-41d4-a716-446655440000 not found"
}
```

### 409 Conflict

```json
{
  "error": "ORDER_ALREADY_COMMITTED",
  "message": "This order already has a committed resolver"
}
```

### 500 Internal Server Error

```json
{
  "error": "INTERNAL_ERROR",
  "message": "An unexpected error occurred"
}
```

## Rate Limiting

- **Global limit**: 100 requests per minute per IP
- **Order creation**: 10 orders per minute per address
- **Status checks**: 60 requests per minute per IP

## WebSocket Events

Connect to WebSocket for real-time updates:

```javascript
const ws = new WebSocket('wss://api.unite-defi.com/ws');

ws.on('message', (data) => {
  const event = JSON.parse(data);
  console.log('Event:', event.type, event.data);
});
```

### Event Types

- `order.created`
- `order.committed`
- `order.escrows_ready`
- `order.secret_revealed`
- `order.completed`
- `auction.price_update`

## SDK Usage

### JavaScript/TypeScript

```typescript
import { UniteRelayerClient } from '@unite-defi/sdk';

const client = new UniteRelayerClient({
  endpoint: 'https://api.unite-defi.com'
});

// Create order
const order = await client.createOrder({
  sourceChain: 'ethereum',
  destChain: 'aptos',
  tokenIn: 'USDC',
  tokenOut: 'APT',
  amountIn: '1000',
  slippage: 0.02
});

// Monitor status
const status = await client.getOrderStatus(order.orderId);
```

## Best Practices

1. **Order Creation**
   - Always verify token addresses
   - Set reasonable slippage (2-5%)
   - Check chain compatibility

2. **Resolver Integration**
   - Monitor WebSocket for new orders
   - Calculate profitability including gas
   - Commit quickly during auction

3. **Error Handling**
   - Implement exponential backoff
   - Handle network disruptions
   - Monitor order expiry

## Changelog

### v1.0.0 (January 2025)
- Initial release
- Support for 26 chains
- Dutch auction mechanism
- WebSocket events