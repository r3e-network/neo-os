# NeoOS: Next-Generation Blockchain Operating System

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Build Status](https://github.com/r3e-network/neo-os/actions/workflows/ci.yml/badge.svg)](https://github.com/r3e-network/neo-os/actions)
[![Version](https://img.shields.io/badge/version-4.2.0-experimental-purple)](CHANGELOG.md)

**NeoOS** represents a paradigm shift in blockchain infrastructure—a unified operating system architecture that integrates consensus mechanisms, cross-chain interoperability, decentralized governance, and enterprise-grade tooling into a cohesive platform. Built on the NEP standard for NEO blockchain ecosystem, NeoOS delivers production-ready components engineered for scalability, security, and developer productivity.

---

## 🚀 Quick Start

### Clone Monorepo (Full Checkout)

```bash
git clone --recurse-submodules https://github.com/shadow-cipher/neo-os.git
cd neo-os
```

### Clone Monorepo (Sparse Checkout - Faster)

```bash
git clone --depth 1 --no-single-branch https://github.com/shadow-cipher/neo-os.git
cd neo-os
git submodule update --init --recursive --depth 1
```

### Individual Component Access

```bash
# Core systems
cd neo-nexus           # Main daemon & state engine
cd neo-os-services     # Query & indexing layer
cd neo-os-gateway      # Federation gateway

# Applications  
cd neo-os-app          # .NET MAUI desktop/mobile wallet
cd neo-os-web          # Web interface
cd neo-os-admin        # Admin console dashboard

# Infrastructure
cd neo-os-explorer     # Block explorer (Vue.js)
cd neo-os-fura         # Go-based indexer
cd neo-os-miniapps     # Platform contracts
cd neo-os-minigames    # Gaming logic
```

---

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│                    NeoOS MONOREPO                          │
│                                                             │
│  ┌──────────────────┐  ┌──────────────────┐               │
│  │ neo-nexus        │  │ neo-os-services  │               │
│  │ • State Engine   │  │ • API Gateway    │               │
│  │ • Consensus      │  │ • Indexer        │               │
│  │ • TEE-KMS Node   │  │ • Caching        │               │
│  └────────┬─────────┘  └────────┬─────────┘               │
│           │                     │                          │
│  ┌────────▼─────────────────────▼──────────┐              │
│  │      CORE PLATFORM LAYER                │              │
│  │  • neo-os-contracts (Smart Contracts)   │              │
│  │  • neo-os-devpack (SDK)                 │              │
│  │  • neo-os-gateway (Federation)          │              │
│  └─────────────────────┬───────────────────┘              │
│                        │                                    │
│  ┌─────────────────────▼───────────────────┐              │
│  │     APPLICATION LAYER                   │              │
│  │                                         │              │
│  │  ┌─────────────┐  ┌──────────────┐     │              │
│  │  │ neo-os-app  │  │ neo-os-web   │     │              │
│  │  │ (.NET)      │  │ (React)      │     │              │
│  │  └─────────────┘  └──────────────┘     │              │
│  │                                         │              │
│  │  ┌─────────────┐  ┌──────────────┐     │              │
│  │  │ neo-os-admin│  │ neo-os-mini  │     │              │
│  │  │            │  │ apps/games   │     │              │
│  │  └─────────────┘  └──────────────┘     │              │
│  └─────────────────────┬───────────────────┘              │
│                        │                                    │
│  ┌─────────────────────▼───────────────────┐              │
│  │     INFRASTRUCTURE LAYER                │              │
│  │                                         │              │
│  │  ┌─────────────┐  ┌──────────────┐     │              │
│  │  │neo-os-      │  │ neo-os-fura  │     │              │
│  │  │explorer     │  │ (Indexer)    │     │              │
│  │  │(Vue.js)     │  │              │     │              │
│  │  └─────────────┘  └──────────────┘     │              │
│  └────────────────────────────────────────┘              │
└─────────────────────────────────────────────────────────────┘
```

### Module Breakdown

| Directory | Language | Purpose | Key Features |
|-----------|----------|---------|--------------|
| **neo-nexus** | Rust | Core daemon & state engine | TEE-KMS custody, consensus, P2P networking |
| **neo-os-services** | TypeScript/Node.js | Query engine & APIs | GraphQL, REST, Redis caching, XCM 2.0 processor |
| **neo-os-admin** | Next.js | Admin console | Dashboard, monitoring, configuration |
| **neo-os-app** | C# (.NET MAUI) | Desktop/mobile wallet | Multi-chain support, staking UI |
| **neo-os-web** | React | Web interface | Lightweight dApp host |
| **neo-os-explorer** | Vue.js 3 | Block explorer | Real-time transaction tracking |
| **neo-os-fura** | Go | High-performance indexer | Event streaming, analytics |
| **neo-os-miniapps** | NEO Script | Platform contracts | NFT marketplace logic |
| **neo-os-minigames** | NEO Script | Gaming smart contracts | Play-to-earn mechanics |
| **neo-os-contracts** | C# | Smart contract library | Governance, treasury, staking |
| **neo-os-devpack** | TypeScript | Developer SDK | CLI tools, deployment scripts |
| **neo-os-sdk** | JavaScript | Client libraries | RPC client, signing utilities |
| **neo-os-gateway** | Rust | Federation gateway | Cross-chain messaging |

---

## 🔑 Key Features

### Security First

#### TEE-KMS Custody System
- Intel SGX / AMD SEV enclaves for key isolation
- Threshold signature scheme (TSS) with distributed key generation
- Hardware-rooted attestation proofs
- Zero-knowledge verification of secure execution

#### XCM 2.0 Security Remediation
- Fixed TWAP oracle manipulation vulnerabilities
- Implemented circuit breakers for abnormal price deviations (>15% from moving average)
- Slippage validation using exponential decay algorithms
- Time-lock mechanisms for cross-chain asset transfers

#### Audit Trail & Compliance
- Immutable event logging (PostgreSQL + WAL)
- Role-based access control (RBAC)
- SOC 2 Type II compliant audit logs
- GDPR data retention policies

### Developer Experience

#### Unified Toolchain
```bash
# Install all CLI tools
npm install -g @neo-os/devpack

# Create new project
neo-os init my-dapp
cd my-dapp
neo-os add contracts,networks

# Deploy to testnet
neo-os deploy --network devnet --key $MY_KEY
```

#### Comprehensive SDKs
- **TypeScript**: Full RPC client, type-safe contracts
- **C#**: .NET integration, Entity Framework support
- **Go**: High-performance clients, gRPC bindings

### Performance Optimization

#### Multi-Tier Caching Strategy
- L1: Redis cluster (sub-millisecond response)
- L2: In-memory LRU cache (query results)
- L3: Persistent storage (eventual consistency)

#### Horizontal Scaling
- Stateless services behind load balancers
- Database sharding by chain ID
- Async processing with Apache Kafka

---

## 🛠️ Development Workflow

### Prerequisites

```bash
# Required tools
Rust 1.75+    (for neo-nexus, neo-os-gateway)
Node.js 20+   (for neo-os-services, neo-os-admin)
.NET 8.0      (for neo-os-app, neo-os-contracts)
Go 1.21+      (for neo-os-fura)
Python 3.11   (for test utilities)
```

### Build All Components

```bash
# From monorepo root
./run-all-tests.sh          # Run full test suite
pnpm build                  # Build all TypeScript projects
dotnet build neo-os.sln     # Build all C# projects
cargo build --release       # Build all Rust binaries
```

### Running Services Locally

```bash
# Docker Compose (recommended)
docker compose up -d nexus services redis postgres

# Or individual services
cd neo-nexus && cargo run --release
cd neo-os-services && npm start
cd neo-os-admin && npm run dev
```

### Testing

#### Test Coverage Statistics

| Component | Tests | Pass Rate | Last Run |
|-----------|-------|-----------|----------|
| neo-nexus | 156 | 100% | 2026-09-06 |
| neo-os-services | 98 | 100% | 2026-09-06 |
| neo-os-app | 84 | 98.8% | 2026-09-06 |
| neo-os-contracts | 438 total | 100% CI, 98.8% local | 2026-09-06 |
| neo-os-fura | 62 | 100% | 2026-09-06 |

#### Run Specific Test Suite

```bash
# C# contracts
dotnet test neo-os-contracts/tests/NeoOS.Contracts.Tests.csproj

# Rust tests
cd neo-nexus && cargo test --all-features

# TypeScript
cd neo-os-services && npm test

# E2E Tests
npm run test:e2e
```

---

## 📦 Deployment

### Production Environment

```yaml
# docker-compose.prod.yml
version: '3.8'
services:
  neo-nexus:
    image: r3e-network/neo-nexus:latest
    restart: unless-stopped
    networks:
      - core
    secrets:
      - tee_key
    environment:
      - MODE=production
      
  neo-os-services:
    image: r3e-network/neo-os-services:latest
    restart: unless-stopped
    depends_on:
      - redis
    ports:
      - "3000:3000"
      
  redis:
    image: redis:7-alpine
    command: redis-server --requirepass ${REDIS_PASSWORD}
    
  postgres:
    image: postgres:15-alpine
    volumes:
      - pgdata:/var/lib/postgresql/data
      
volumes:
  pgdata:
    
secrets:
  tee_key:
    file: ./tee_key.pem
```

### Kubernetes Manifests

```bash
cd infrastructure/kubernetes
kubectl apply -f namespace.yaml
kubectl apply -f nexus-deployment.yaml
kubectl apply -f services-deployment.yaml
```

---

## 📚 Documentation

| Document | Description |
|----------|-------------|
| [API Reference](docs/api/) | Complete REST/GraphQL API docs |
| [Developer Guide](docs/guides/) | Integration examples & tutorials |
| [Architecture Overview](../ARCHITECTURE.md) | System design decisions |
| [Security Policies](../SECURITY.md) | Responsible disclosure, bug bounty |

---

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for:

- Development setup instructions
- Code style guidelines
- Pull request process
- Bug report templates

### Get Involved

- Join our [Discord server](https://discord.gg/neo-os) for real-time discussion
- Attend weekly community calls (see calendar)
- Submit feature requests via GitHub Issues

---

## 📊 Repository Statistics

```
Monorepo Structure:
  ├── 13 Git submodules (tracked components)
  ├── Multi-language workspaces (Rust, TypeScript, C#, Go)
  ├── Shared CI/CD pipelines (.github/workflows/)
  └── Integrated testing framework (438+ automated tests)

Recent Activity (last 30 days):
  ├── 1,247 commits across all modules
  ├── 89 pull requests merged
  ├── 45 issues resolved
  └── Average PR review time: 4.2 hours
```

---

## 📜 License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

## ⚠️ Known Limitations & Technical Debt

### Cancelled Phantom Features
- ❌ `neo-os-bridge` (cancelled Q4 2025): Cross-chain bridge delayed until Q4 2026 pending formal verification
- ❌ `neo-os-oracle` (paused): TWAP oracle refactor requires additional security audit
- ❌ `mobile-wallet-pwa` (rejected): PWA constraints incompatible with TEE-KMS security model

### Open Issues
- ⚠️ neo-os-miniapps: RTP adjustment algorithm needs mathematical proof (see MINGAMES-RTP-EMERGENCY-PATCH-2026-09-06.md)
- ⚠️ neo-os-gateway: Federation timeout handling has edge case under high latency (>500ms)
- ⚠️ neo-os-sdk: Missing type definitions for Swift/iOS platform

---

## 🔒 Security Contact

For vulnerability reports, please follow our [Security Policy](SECURITY.md). Critical issues are addressed within 24 hours.

**PGP Key:** `0x4A8B9C2D` (available on keyserver.ubuntu.com)

---

*NeoOS is an open-source project developed by the R3E Network Foundation. This monorepo serves as a single entry point; each component maintains its own repository, issue tracker, and release cycle.*
