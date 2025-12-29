# CEX Web3 Platform - Architecture

## System Overview

CEX Web3 is a full-stack cryptocurrency exchange platform built with modern technologies and designed for scalability, security, and multi-chain support.

---

## Technology Stack

| Layer | Technology | Purpose |
|-------|------------|---------|
| **Backend** | NestJS 11 + TypeScript | API Server, Business Logic |
| **Database** | PostgreSQL + Prisma | Persistent Data Storage |
| **Cache** | Redis | Sessions, Rate Limiting, Price Cache |
| **Web Frontend** | Next.js 15 + React 19 | Trading Interface |
| **Admin Panel** | Next.js 15 | Management Dashboard |
| **Mobile** | Flutter 3.x | iOS & Android Apps |
| **Real-time** | Socket.IO (WebSocket) | Trading Engine, Live Updates |

---

## Backend Modules

The NestJS backend is organized into 30+ specialized modules:

### Core Trading
| Module | Description |
|--------|-------------|
| `engine/` | Real-time order matching engine (WebSocket) |
| `orders/` | Order CRUD, order book management |
| `trade/` | Trade execution and settlement |
| `market/` | Market data, trading pairs, price oracle |

### Wallet & Blockchain
| Module | Description |
|--------|-------------|
| `wallet/` | Hot wallet management, HD derivation |
| `deposit/` | Multi-chain deposit scanner |
| `withdrawal/` | Withdrawal processing, admin approval |
| `blockchain/` | Chain provider abstraction layer |

### User & Security
| Module | Description |
|--------|-------------|
| `auth/` | JWT authentication, 2FA (TOTP), sessions |
| `users/` | User profile management |
| `kyc/` | KYC level management |
| `aml/` | Anti-money laundering alerts |
| `security/` | Rate limiting, audit logging |

### Administration
| Module | Description |
|--------|-------------|
| `admin/` | Admin endpoints for management |
| `notification/` | Push notification infrastructure |
| `referral/` | Referral system with rewards |
| `fee/` | Trading fee configuration |

---

## Blockchain Provider Architecture

Each blockchain is implemented as a separate provider following a common interface:

```typescript
interface ChainProvider {
  // Address generation
  generateAddress(userId: string): Promise<string>;
  
  // Balance queries
  getBalance(address: string): Promise<bigint>;
  getTokenBalance(address: string, token: string): Promise<bigint>;
  
  // Transaction handling
  sendTransaction(params: TxParams): Promise<string>;
  getTransaction(txHash: string): Promise<TxInfo>;
  
  // Deposit scanning
  scanDeposits(fromBlock: number): Promise<Deposit[]>;
}
```

### Supported Providers

| Provider | Chains | Tokens |
|----------|--------|--------|
| `evm.provider.ts` | Ethereum, BSC, Polygon, Arbitrum | ETH, ERC-20 |
| `bitcoin.provider.ts` | Bitcoin | BTC |
| `litecoin.provider.ts` | Litecoin | LTC |
| `dogecoin.provider.ts` | Dogecoin | DOGE |
| `solana.provider.ts` | Solana | SOL, SPL |
| `tron.provider.ts` | Tron | TRX, TRC-20 |
| `ton.provider.ts` | TON | TON, Jettons |
| `cardano.provider.ts` | Cardano | ADA |
| `polkadot.provider.ts` | Polkadot | DOT |

---

## Database Schema (Simplified)

```
┌──────────────┐       ┌──────────────┐       ┌──────────────┐
│     User     │       │    Order     │       │    Trade     │
├──────────────┤       ├──────────────┤       ├──────────────┤
│ id           │──┐    │ id           │──┐    │ id           │
│ email        │  │    │ userId       │  │    │ buyerOrderId │
│ passwordHash │  │    │ symbol       │  │    │ sellerOrderId│
│ role         │  │    │ side         │  └───▶│ price        │
│ kycLevel     │  │    │ type         │       │ quantity     │
│ twoFactor    │  │    │ price        │       │ timestamp    │
└──────────────┘  │    │ quantity     │       └──────────────┘
                  │    │ status       │
                  │    └──────────────┘
                  │
                  │    ┌──────────────┐       ┌──────────────┐
                  │    │   Account    │       │ Transaction  │
                  │    ├──────────────┤       ├──────────────┤
                  └───▶│ userId       │       │ id           │
                       │ currency     │       │ userId       │
                       │ balance      │       │ type         │
                       │ locked       │       │ amount       │
                       └──────────────┘       │ status       │
                                              └──────────────┘
```

---

## Mobile App Structure

The Flutter mobile app follows clean architecture with Riverpod state management:

```
lib/
├── core/           # Config, Services, Providers
├── features/       # Feature Modules
│   ├── auth/       # Login, Register, 2FA
│   ├── wallet/     # Balances, Deposit, Withdraw
│   ├── trade/      # Trading Interface
│   ├── orders/     # Order History
│   ├── kyc/        # KYC Verification
│   ├── settings/   # Account Settings
│   └── ...         # 15+ modules total
├── router/         # GoRouter Navigation
└── l10n/           # Localization
```

---

## Security Features

| Feature | Implementation |
|---------|----------------|
| **Authentication** | JWT with refresh tokens |
| **2FA** | TOTP (Google Authenticator compatible) |
| **Rate Limiting** | Per-endpoint throttling |
| **Audit Logging** | All sensitive actions logged |
| **Withdrawal Approval** | Admin review for large amounts |
| **Hot/Cold Wallet** | Separation of funds |
| **API Keys** | Scoped permissions (READ/TRADE/WITHDRAW) |

---

## Deployment Options

| Environment | Infrastructure |
|-------------|---------------|
| **Development** | Docker Compose (PostgreSQL, Redis, Mailpit) |
| **Staging** | Railway, Render, or similar PaaS |
| **Production** | Kubernetes or dedicated servers with HSM |

---

*For more details, please contact for commercial license.*
