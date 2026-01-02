# CEX Web3 平台 - API 範例

🌐 [English](./API_EXAMPLES.md) | **繁體中文**

## 基本 URL

```
生產環境: https://backend-production-ae3a.up.railway.app/api
WebSocket: wss://backend-production-ae3a.up.railway.app/engine
```

---

## 身份驗證

### 註冊

```bash
curl -X POST https://backend-production-ae3a.up.railway.app/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@example.com",
    "password": "SecurePass123!",
    "name": "王小明"
  }'
```

**回應：**
```json
{
  "message": "User registered successfully",
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": "uuid",
    "email": "user@example.com",
    "name": "王小明"
  }
}
```

### 登入

```bash
curl -X POST https://backend-production-ae3a.up.railway.app/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@example.com",
    "password": "SecurePass123!"
  }'
```

### 使用雙因素認證登入

```bash
curl -X POST https://backend-production-ae3a.up.railway.app/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@example.com",
    "password": "SecurePass123!",
    "totpCode": "123456"
  }'
```

---

## 交易

### 下限價單

```bash
curl -X POST https://backend-production-ae3a.up.railway.app/api/orders \
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

**回應：**
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

### 下市價單

```bash
curl -X POST https://backend-production-ae3a.up.railway.app/api/orders \
  -H "Authorization: Bearer <access_token>" \
  -H "Content-Type: application/json" \
  -d '{
    "symbol": "BTC-USDT",
    "side": "SELL",
    "type": "MARKET",
    "quantity": 0.01
  }'
```

### 取消訂單

```bash
curl -X DELETE https://backend-production-ae3a.up.railway.app/api/orders/<order-id> \
  -H "Authorization: Bearer <access_token>"
```

### 取得訂單簿

```bash
curl https://backend-production-ae3a.up.railway.app/api/market/orderbook/BTC-USDT
```

**回應：**
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

## 錢包

### 取得餘額

```bash
curl https://backend-production-ae3a.up.railway.app/api/users/me/accounts \
  -H "Authorization: Bearer <access_token>"
```

**回應：**
```json
{
  "data": [
    { "currency": "BTC", "balance": "0.5", "locked": "0.01", "available": "0.49" },
    { "currency": "USDT", "balance": "10000", "locked": "500", "available": "9500" }
  ]
}
```

### 取得充值地址

```bash
curl https://backend-production-ae3a.up.railway.app/api/deposit/address?chain=ethereum&currency=ETH \
  -H "Authorization: Bearer <access_token>"
```

**回應：**
```json
{
  "address": "0x1234567890abcdef...",
  "chain": "ethereum",
  "currency": "ETH"
}
```

### 請求提現

```bash
curl -X POST https://backend-production-ae3a.up.railway.app/api/withdrawal \
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

## WebSocket（即時）

### 連接

```javascript
const socket = io('wss://backend-production-ae3a.up.railway.app/engine', {
  auth: { token: '<access_token>' }
});
```

### 訂閱訂單簿

```javascript
socket.emit('subscribe', { channel: 'orderbook:BTC-USDT' });

socket.on('orderbook:BTC-USDT', (data) => {
  console.log('訂單簿更新:', data);
});
```

### 訂閱成交

```javascript
socket.emit('subscribe', { channel: 'trades:BTC-USDT' });

socket.on('trades:BTC-USDT', (trade) => {
  console.log('新成交:', trade);
});
```

### 訂閱用戶訂單

```javascript
socket.emit('subscribe', { channel: 'user:orders' });

socket.on('user:orders', (order) => {
  console.log('訂單更新:', order);
});
```

---

## 錯誤回應

所有錯誤遵循以下格式：

```json
{
  "statusCode": 400,
  "message": "錯誤說明",
  "error": "Bad Request"
}
```

| 狀態碼 | 含義 |
|--------|------|
| 400 | 錯誤請求 - 參數無效 |
| 401 | 未授權 - Token 無效或缺失 |
| 403 | 禁止訪問 - 權限不足 |
| 404 | 未找到 - 資源不存在 |
| 429 | 請求過多 - 已達速率限制 |
| 500 | 內部伺服器錯誤 |

---

*如需完整 API 文件，請聯繫取得商業授權。*

📧 **聯繫方式**: [aa22396584@gmail.com](mailto:aa22396584@gmail.com)
