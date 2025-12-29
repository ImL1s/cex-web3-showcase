<div align="center">

<!-- System Architecture Banner -->
<img src="assets/images/system_architecture.png" alt="CEX Web3 Platform Architecture" width="100%">

# CEX Web3 Exchange Platform

**Enterprise-Grade Cryptocurrency Exchange Infrastructure**

[![License](https://img.shields.io/badge/license-AGPL--3.0-blue?style=for-the-badge)](./LICENSE)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![NestJS](https://img.shields.io/badge/NestJS-11-E0234E?style=for-the-badge&logo=nestjs&logoColor=white)](https://nestjs.com/)
[![Flutter](https://img.shields.io/badge/Flutter-3.x-02569B?style=for-the-badge&logo=flutter&logoColor=white)](https://flutter.dev/)
[![Next.js](https://img.shields.io/badge/Next.js-15-000000?style=for-the-badge&logo=next.js&logoColor=white)](https://nextjs.org/)

[🚀 Live Demo](#-live-demo) • [📱 Download APK](#-download-apk) • [💼 Commercial License](#-commercial-license) • [📖 Documentation](#-documentation)

</div>

---

## ⚠️ Important Disclaimer

> **READ BEFORE USE**
> 
> This software is provided **"AS IS"** without warranty of any kind. The authors are **NOT** operating a cryptocurrency exchange and are **NOT** responsible for how this software is used.
> 
> **If you operate a service using this software, YOU are solely responsible for:**
> - Obtaining required licenses and permits
> - Implementing AML/KYC compliance
> - Safeguarding user funds
> - All legal and regulatory obligations
>
> See [LEGAL_DISCLAIMER.md](./LEGAL_DISCLAIMER.md) for full details.

---

## ✨ Features

<table>
<tr>
<td width="50%">

### 🔐 High-Performance Trading Engine
- Real-time order matching via WebSocket
- Multiple order types: Limit, Market, Stop-Loss, OCO
- Order book with depth visualization
- Sub-second trade execution

</td>
<td width="50%">

### 💼 Multi-Chain Wallet System
- **10+ Blockchains Supported**
- EVM: Ethereum, BSC, Polygon, Arbitrum
- UTXO: Bitcoin, Litecoin, Dogecoin
- Others: Solana, Tron, TON, Cardano, Polkadot
- HD Wallet derivation for user addresses

</td>
</tr>
<tr>
<td>

### 🛡️ Security & Compliance
- KYC/AML verification system
- Two-Factor Authentication (TOTP)
- Withdrawal approval workflow
- Rate limiting & DDoS protection
- Comprehensive audit logging

</td>
<td>

### 📱 Cross-Platform Applications
- **Web**: Next.js 15 trading interface
- **Mobile**: Flutter iOS & Android apps
- **Admin**: Management dashboard
- **API**: RESTful + WebSocket for algo trading

</td>
</tr>
</table>

---

## 🏗️ System Architecture

<div align="center">
<img src="assets/images/system_architecture.png" alt="System Architecture" width="90%">
</div>

### Architecture Overview

**CEX Web3 Platform** is built on a modular microservices architecture:

| Layer | Description |
|-------|-------------|
| **Client Layer** | Web (Next.js), Mobile (Flutter), Admin Dashboard |
| **API Gateway** | NestJS REST API + WebSocket for real-time updates |
| **Core Services** | Auth, Trading Engine, Wallet, KYC/AML, Deposits/Withdrawals |
| **Data Layer** | PostgreSQL (persistent), Redis (cache/sessions) |
| **Blockchain Layer** | 12+ chain integrations via abstracted providers |

---

## 💹 Trading Flow

<div align="center">
<img src="assets/images/trading_flow.png" alt="Trading Flow" width="90%">
</div>

### How Orders Are Processed

1. **Order Submission** → User places Buy/Sell order via API or WebSocket
2. **Validation** → System checks balance, rate limits, and risk controls
3. **Matching Engine** → Real-time order book matching algorithm
4. **Trade Execution** → Matched orders are settled, balances updated atomically
5. **Notification** → Real-time WebSocket push to all connected clients

---

## 💼 Multi-Chain Wallet

<div align="center">
<img src="assets/images/wallet_multichain.png" alt="Multi-Chain Support" width="80%">
</div>

### Supported Chains

Our wallet system supports **12+ blockchains** with unified HD wallet derivation:

| Chain | Type | Tokens | Status |
|-------|------|--------|--------|
| **Ethereum** | EVM | ETH, ERC-20 | ✅ Production Ready |
| **BNB Smart Chain** | EVM | BNB, BEP-20 | ✅ Production Ready |
| **Polygon** | EVM | MATIC, ERC-20 | ✅ Production Ready |
| **Arbitrum** | EVM | ETH, ERC-20 | ✅ Production Ready |
| **Bitcoin** | UTXO | BTC | ✅ Production Ready |
| **Litecoin** | UTXO | LTC | ✅ Production Ready |
| **Dogecoin** | UTXO | DOGE | ✅ Production Ready |
| **Solana** | Account | SOL, SPL | ✅ Production Ready |
| **Tron** | Account | TRX, TRC-20 | ✅ Production Ready |
| **TON** | Account | TON, Jettons | ✅ Production Ready |
| **Cardano** | UTXO | ADA | ✅ Production Ready |
| **Polkadot** | Account | DOT | ✅ Production Ready |

---

## 💰 Deposit & Withdrawal Flow

<div align="center">
<img src="assets/images/deposit_withdrawal_flow.png" alt="Deposit & Withdrawal Flow" width="90%">
</div>

### Deposit Process
1. User requests deposit address → System generates unique HD wallet address
2. User sends crypto → Deposit Scanner monitors blockchain
3. Transaction confirmed → Balance credited automatically

### Withdrawal Process
1. User requests withdrawal → KYC/AML verification
2. Large amounts → Admin approval required
3. Hot wallet signs transaction → Broadcast to blockchain
4. Confirmation → User notified via push/email

---

## 📸 Product Screenshots

> 🔜 Coming Soon - Real product screenshots will be added

<table>
<tr>
<td width="33%">
<p align="center"><b>💹 Trading Interface</b></p>
<p align="center">Real-time order book, TradingView charts, multiple order types</p>
</td>
<td width="33%">
<p align="center"><b>💼 Wallet Dashboard</b></p>
<p align="center">Multi-chain balances, deposit/withdraw, transaction history</p>
</td>
<td width="33%">
<p align="center"><b>📱 Mobile App</b></p>
<p align="center">Full-featured trading on iOS & Android</p>
</td>
</tr>
</table>

---

## 🚀 Live Demo

| Platform | Link | Status |
|----------|------|--------|
| 🌐 Web App | [Coming Soon](#) | 🔜 |
| 👨‍💼 Admin Panel | [Coming Soon](#) | 🔜 |

---

## 📱 Download APK

> ⚠️ **Demo Backend Not Yet Available**
> 
> The APK is available for download, but the demo backend server is **not yet deployed**.
> Currently, the app will not be able to connect to any server.
> 
> **What you can explore:**
> - UI/UX design and navigation
> - App architecture and code quality
> 
> **Coming soon:**
> - Live demo backend for full functionality testing
> - Web demo deployment
>
> **Interested in a live demo?** Contact us at aa22396584@gmail.com

| Platform | Download | Version | Status |
|----------|----------|---------|--------|
| Android | [📥 Download APK](https://github.com/ImL1s/cex-web3-showcase/releases/latest) | v1.0.0 | ⚠️ UI Only |
| iOS | TestFlight (Coming Soon) | - | 🔜 |

---

## 🛠️ Tech Stack

| Layer | Technologies |
|-------|--------------|
| **Backend** | NestJS 11, TypeScript 5, Prisma ORM, PostgreSQL, Redis |
| **Web/Admin** | Next.js 15, React 19, Tailwind CSS, TanStack Query |
| **Mobile** | Flutter 3.x, Riverpod, go_router |
| **Blockchain** | ethers.js v6, @solana/web3.js, bitcoinjs-lib, tronweb |
| **Infrastructure** | Docker, GitHub Actions, Vercel |

---

## 📖 Documentation

| Document | Description |
|----------|-------------|
| [Architecture](./docs/ARCHITECTURE.md) | System design and module breakdown |
| [API Examples](./docs/API_EXAMPLES.md) | REST and WebSocket API usage |
| [Deployment Guide](./docs/DEPLOYMENT.md) | Production deployment checklist |

---

## 💼 Commercial License

This project is dual-licensed:

| License | Use Case | Price |
|---------|----------|-------|
| **AGPL-3.0** | Open source use (modifications must be shared) | Free |
| **Commercial** | Proprietary use, white-label solutions | Contact for pricing |

### Interested in Commercial License?

📧 **Email**: [aa22396584@gmail.com](mailto:aa22396584@gmail.com)

**What's Included:**
- ✅ Full source code access
- ✅ Private repository access
- ✅ Deployment support
- ✅ 90 days technical support
- ✅ Custom feature development (optional)

---

## ⚖️ License

This project is licensed under the **GNU Affero General Public License v3.0 (AGPL-3.0)**.

See [LICENSE](./LICENSE) for full license text.

See [LEGAL_DISCLAIMER.md](./LEGAL_DISCLAIMER.md) for important legal information.

---

## 🔒 Security

For security vulnerabilities, please email: [security@cex-web3.io](mailto:security@cex-web3.io)

**Do NOT open public issues for security vulnerabilities.**

---

<div align="center">

**Built with ❤️ for the crypto community**

[⬆ Back to Top](#cex-web3-exchange-platform)

</div>
