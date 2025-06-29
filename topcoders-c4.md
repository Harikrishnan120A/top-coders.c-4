# 🔐 Identify 📋 Contents

- [✨ Features](#-features) • [🛠 Tech Stack](#-tech-stack) • [🚀 Quick Start](#-quick-start)
- [📚 API Docs](#-api-docs) • [🧪 Testing](#-testing) • [🐳 Docker](#-docker)
- [🚀 Deploy](#-deploy) • [🤝 Contributing](#-contributing) • [🆘 Help](#-help)[![Build](https://img.shields.io/github/workflow/status/topcoder/identity-service-v6/CI)](https://github.com/topcoder/identity-service-v6/actions)
[![Coverage](https://img.shields.io/codecov/c/github/topcoder/identity-service-v6)](https://codecov.io/gh/topcoder/identity-service-v6)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.3-blue.svg)](https://www.typescriptlang.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> **Enterprise-grade TypeScript identity service** for Topcoder platform. Migrated from Java/MySQL to TypeScript/PostgreSQL with Prisma ORM.

**⚡ Quick Start**: `git clone → npm install → npm run dev` ([Full Setup](#-quick-start))

## � Table of Contents

- [✨ Features](#-features)
- [🛠 Technology Stack](#-technology-stack)
- [📋 Prerequisites](#-prerequisites)
- [🚀 Quick Start](#-quick-start)
- [🔧 Installation & Setup](#-installation--setup)
- [🏃‍♂️ Running the Application](#️-running-the-application)
- [🧪 Testing](#-testing)
- [📚 API Documentation](#-api-documentation)
- [🐳 Docker Support](#-docker-support)
- [🚀 Deployment](#-deployment)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)
- [🆘 Troubleshooting](#-troubleshooting)

---

## ✨ Features

| 🔐 **Auth & Security** | 👥 **User Management** | 🎭 **Roles & Groups** |
|------------------------|-------------------------|------------------------|
| • JWT authentication  | • Complete CRUD ops    | • Dynamic role creation |
| • RBAC authorization  | • Profile management   | • Group membership     |
| • Rate limiting       | • Search & filtering   | • Privacy controls     |
| • Password hashing    | • Account activation   | • Permission caching   |

| 🚀 **Performance** | 🛠 **Developer Experience** | 📊 **Monitoring** |
|--------------------|-----------------------------|--------------------|
| • Redis caching   | • TypeScript strict mode   | • Health checks    |
| • Kafka events    | • Hot-reload development    | • Structured logs  |
| • Connection pooling | • 90%+ test coverage     | • Error tracking   |
| • Query optimization | • API documentation      | • Performance metrics |

## 🛠 Tech Stack

**Core**: TypeScript 5.3 • Node.js 18+ • Express.js 4.18+  
**Database**: PostgreSQL 16.3 • Prisma ORM 5.7+  
**Cache/Events**: Redis 7.0+ • Kafka 3.0+  
**Testing**: Jest 29+ • 90%+ Coverage  
**DevOps**: Docker • GitHub Actions CI/CD

<details>
<summary>📦 <b>Key Dependencies</b></summary>

```json
{
  "dependencies": {
    "express": "^4.18.2", "@prisma/client": "^5.7.1",
    "bcrypt": "^5.1.1", "jsonwebtoken": "^9.0.2",
    "joi": "^17.11.0", "redis": "^4.6.10", "kafkajs": "^2.2.4"
  },
  "devDependencies": {
    "typescript": "^5.3.3", "jest": "^29.7.0",
    "eslint": "^8.56.0", "prisma": "^5.7.1"
  }
}
```
</details>

## 🚀 Quick Start

```bash
# 1. Install (requires Node.js 18+, PostgreSQL 16.3)
git clone https://github.com/topcoder/identity-service-v6.git
cd identity-service-v6 && npm install

# 2. Configure
cp .env.example .env  # Edit with your DB credentials

# 3. Database
npm run prisma:generate && npm run prisma:migrate

# 4. Run
npm run dev  # → http://localhost:3000
```

**� Docker**: `docker-compose up -d` (starts everything)

## 🧪 Testing

```bash
npm test              # Run all tests
npm run test:coverage # With coverage report (90%+ target)
npm run test:watch    # Watch mode for development
```

## 📚 API Docs

**📖 Interactive Docs**: http://localhost:3000/api-docs (Swagger UI)

### Core Endpoints

| Endpoint | Method | Description | Auth |
|----------|--------|-------------|------|
| `/api/v1/auth/login` | POST | User login | ❌ |
| `/api/v1/auth/logout` | POST | User logout | ✅ |
| `/api/v1/users` | GET/POST | List/Create users | ✅ |
| `/api/v1/users/:id` | GET/PUT/DELETE | User operations | ✅ |
| `/api/v1/roles` | GET/POST | List/Create roles | ✅ |
| `/api/v1/groups` | GET/POST | List/Create groups | ✅ |

### Quick Examples

<details>
<summary><b>🔐 Authentication</b></summary>

**Login:**
```bash
curl -X POST http://localhost:3000/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email": "user@example.com", "password": "password"}'
```

**Response:**
```json
{
  "success": true,
  "data": {
    "accessToken": "eyJhbGci...",
    "user": {"id": "123", "email": "user@example.com"}
  }
}
```
</details>

<details>
<summary><b>👥 User Management</b></summary>

**Create User:**
```bash
curl -X POST http://localhost:3000/api/v1/users \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{"email": "new@example.com", "firstName": "John", "lastName": "Doe"}'
```

**List Users:**
```bash
curl -H "Authorization: Bearer <token>" \
  "http://localhost:3000/api/v1/users?page=1&limit=10"
```
</details>

### Response Format
```json
{
  "success": true,
  "data": { /* response data */ },
  "meta": {"timestamp": "2024-01-01T00:00:00.000Z", "requestId": "uuid"}
}
```

## 🐳 Docker

**One-command setup:**
```bash
docker-compose up -d  # Starts PostgreSQL + Redis + Kafka + API
curl http://localhost:3000/health  # Verify
```

**Individual containers:**
```bash
docker build -t identity-service-v6 .
docker run -p 3000:3000 -e DATABASE_URL="..." identity-service-v6
```

<details>
<summary>📄 <b>Environment Variables</b></summary>

```env
# Required
DATABASE_URL="postgresql://user:pass@localhost:5432/identity_service"
JWT_SECRET="your-super-secret-jwt-key-minimum-32-chars"

# Optional
REDIS_HOST="localhost"
KAFKA_BROKERS="localhost:9092"
NODE_ENV="development"
PORT=3000
```
</details>

## 🚀 Deploy

**Production Environment:**
```env
NODE_ENV=production
DATABASE_URL=<production-database-url>
JWT_SECRET=<secure-random-secret-64-chars>
```

**PM2 Deployment:**
```bash
npm install -g pm2
npm run build
pm2 start dist/index.js --name identity-service
pm2 monit
```

**Health Check:** `curl http://localhost:3000/health`

## 🤝 Contributing

1. **Fork & Branch**: `git checkout -b feature/your-feature`
2. **Develop**: Add tests, ensure coverage ≥90%
3. **Quality**: `npm run lint:fix && npm test && npm run build`
4. **Commit**: Use [conventional commits](https://conventionalcommits.org/)
5. **PR**: Submit with detailed description

**Code Standards**: TypeScript strict • ESLint • Prettier • JSDoc

## 🆘 Help

**Common Issues:**
- **DB Connection**: Check PostgreSQL running + DATABASE_URL format
- **Prisma Error**: Run `npm run prisma:generate`
- **JWT Error**: Verify JWT_SECRET is set (≥32 chars)

**Support:**
- 📖 [Issues](../../issues) for bugs/features
- 📧 platform@topcoder.com
- 📚 [Wiki](../../wiki)

---

**🎯 Quick Commands:**
```bash
npm run dev        # Start development
npm test          # Run tests
npm run build     # Build production
docker-compose up # Full stack
```

**📄 License**: MIT | **👨‍💻 Developed by**: Hari | **📅 Created**: June 29, 2025
