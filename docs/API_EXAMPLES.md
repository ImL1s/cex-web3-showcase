# CEX Web3 Platform - API Examples

**English** | 🌐 [繁體中文](./API_EXAMPLES.zh-TW.md)

## Base URL

```
Production: https://api.cex-web3.io/api
WebSocket:  wss://api.cex-web3.io/engine
```

---

## Authentication

### Register

```bash
curl -X POST https://api.cex-web3.io/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@example.com",
    "password": "SecurePass123!",
    "name": "John Doe"
  }'
```

**Response:**
```json
{
  "message": "User registered successfully",
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": "uuid",
    "email": "user@example.com",
    "name": "John Doe"
  }
}
```

### Login

```bash
curl -X POST https://api.cex-web3.io/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@example.com",
    "password": "SecurePass123!"
  }'
```

### Login with 2FA

```bash
curl -X POST https://api.cex-web3.io/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@example.com",
    "password": "SecurePass123!",
    "totpCode": "123456"
  }'
```

---

## Trading

### Place Limit Order

```bash
curl -X POST https://api.cex-web3.io/api/orders \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{
    "symbol": "BTC-USDT",
    "side": "BUY",
    "type": "LIMIT",
    "price": 50000,
    "quantity": 0.01
  }'
```

**Response:**
```json
{
  "id": "order-uuid",
  "symbol": "BTC-USDT",
  "side": "BUY",
  "type": "LIMIT",
  "price": "50000",
  "quantity": "0.01",
  "status": "OPEN",
  "createdAt": "2024-01-01T00:00:00Z"
}
```

### Place Market Order

```bash
curl -X POST https://api.cex-web3.io/api/orders \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{
    "symbol": "BTC-USDT",
    "side": "SELL",
    "type": "MARKET",
    "quantity": 0.01
  }'
```

### Cancel Order

```bash
curl -X DELETE https://api.cex-web3.io/api/orders/<order-id> \
  -H "Authorization: Bearer <access_token>"
```

### Get Order Book

```bash
curl https://api.cex-web3.io/api/market/orderbook/BTC-USDT
```

**Response:**
```json
{
  "bids": [
    { "price": "49990", "quantity": "1.5" },
    { "price": "49980", "quantity": "2.0" }
  ],
  "asks": [
    { "price": "50010", "quantity": "0.8" },
    { "price": "50020", "quantity": "1.2" }
  ]
}
```

---

## Wallet

### Get Balances

```bash
curl https://api.cex-web3.io/api/users/me/accounts \
  -H "Authorization: Bearer <access_token>"
```

**Response:**
```json
{
  "data": [
    { "currency": "BTC", "balance": "0.5", "locked": "0.01", "available": "0.49" },
    { "currency": "USDT", "balance": "10000", "locked": "500", "available": "9500" }
  ]
}
```

### Get Deposit Address

```bash
curl https://api.cex-web3.io/api/deposit/address?chain=ethereum&currency=ETH \
  -H "Authorization: Bearer <access_token>"
```

**Response:**
```json
{
  "address": "0x1234567890abcdef...",
  "chain": "ethereum",
  "currency": "ETH"
}
```

### Request Withdrawal

```bash
curl -X POST https://api.cex-web3.io/api/withdrawal \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{
    "chain": "ethereum",
    "currency": "ETH",
    "address": "0xRecipientAddress...",
    "amount": "0.1"
  }'
```

---

## WebSocket (Real-time)

### Connect

```javascript
const socket = io('wss://api.cex-web3.io/engine', {
  auth: { token: '<access_token>' }
});
```

### Subscribe to Order Book

```javascript
socket.emit('subscribe', { channel: 'orderbook:BTC-USDT' });

socket.on('orderbook:BTC-USDT', (data) => {
  console.log('Order book update:', data);
});
```

### Subscribe to Trades

```javascript
socket.emit('subscribe', { channel: 'trades:BTC-USDT' });

socket.on('trades:BTC-USDT', (trade) => {
  console.log('New trade:', trade);
});
```

### Subscribe to User Orders

```javascript
socket.emit('subscribe', { channel: 'user:orders' });

socket.on('user:orders', (order) => {
  console.log('Order update:', order);
});
```

---

## Error Responses

All errors follow this format:

```json
{
  "statusCode": 400,
  "message": "Error description",
  "error": "Bad Request"
}
```

| Status Code | Meaning |
|-------------|---------|
| 400 | Bad Request - Invalid parameters |
| 401 | Unauthorized - Invalid or missing token |
| 403 | Forbidden - Insufficient permissions |
| 404 | Not Found - Resource doesn't exist |
| 429 | Too Many Requests - Rate limited |
| 500 | Internal Server Error |

---

*For complete API documentation, please contact for commercial license.*
