# 🔐 Identity Service v6 - Complete Project Documentation

[![TypeScript](https://img.shields.io/badge/TypeScript-5.3-blue.svg)](https://www.typescriptlang.org/)
[![Node.js](https://img.shields.io/badge/Node.js-18+-green.svg)](https://nodejs.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16.3-blue.svg)](https://www.postgresql.org/)
[![Prisma](https://img.shields.io/badge/Prisma-5.7-2D3748.svg)](https://www.prisma.io/)
[![Express](https://img.shields.io/badge/Express-4.18-000000.svg)](https://expressjs.com/)
[![Jest](https://img.shields.io/badge/Jest-29+-C21325.svg)](https://jestjs.io/)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED.svg)](https://www.docker.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> **Enterprise-grade TypeScript identity and authentication service** for the Topcoder platform. Modern, scalable, and production-ready with comprehensive testing and documentation.

---

## 📋 Table of Contents

- [🌟 Project Overview](#-project-overview)
- [✨ Key Features](#-key-features)
- [🏗️ Architecture](#️-architecture)
- [🛠 Technology Stack](#-technology-stack)
- [📁 Project Structure](#-project-structure)
- [🚀 Quick Start](#-quick-start)
- [🔧 Configuration](#-configuration)
- [📚 API Documentation](#-api-documentation)
- [🧪 Testing](#-testing)
- [🐳 Docker Deployment](#-docker-deployment)
- [🔒 Security Features](#-security-features)
- [📊 Database Schema](#-database-schema)
- [🌐 Environment Setup](#-environment-setup)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

---

## 🌟 Project Overview

The **Identity Service v6** is a complete rewrite of Topcoder's identity management system, migrated from Java/MySQL to a modern TypeScript/PostgreSQL stack. This service provides:

- **🔐 Authentication**: JWT-based user authentication
- **👥 User Management**: Complete CRUD operations with profile management
- **🎭 Role & Group Management**: Dynamic role assignment and group membership
- **🚀 Performance**: Redis caching and Kafka event streaming
- **🔒 Security**: Enterprise-grade security with rate limiting and validation
- **📊 Monitoring**: Health checks and comprehensive logging

### 🎯 Migration Goals

| Old Stack | New Stack | Benefits |
|-----------|-----------|----------|
| Java | TypeScript | Type safety, better DX |
| MySQL | PostgreSQL | JSON support, better performance |
| Hibernate | Prisma | Type-safe queries, migrations |
| Manual Setup | Docker | Consistent environments |

---

## ✨ Key Features

<table>
<tr>
<td width="50%">

### 🔐 **Authentication & Security**
- JWT access & refresh tokens
- Password hashing (bcrypt)
- Role-based access control (RBAC)
- Rate limiting & request validation
- Security headers & CORS
- API key authentication

</td>
<td width="50%">

### 👥 **User Management**
- Complete user CRUD operations
- Profile management & avatars
- Email verification & password reset
- User search & filtering
- Account activation/deactivation
- Bulk operations support

</td>
</tr>
<tr>
<td>

### 🎭 **Role & Group System**
- Dynamic role creation & assignment
- Hierarchical permission system
- Group membership management
- Privacy controls (public/private)
- Role inheritance
- Permission caching

</td>
<td>

### 🚀 **Performance & Scalability**
- Redis caching layer
- Database connection pooling
- Kafka event streaming
- Query optimization
- Background job processing
- Health monitoring

</td>
</tr>
</table>

---

## 🏗️ Architecture

```mermaid
graph TB
    Client[Client Applications] --> Gateway[API Gateway]
    Gateway --> Auth[Auth Controller]
    Gateway --> Users[User Controller]
    Gateway --> Roles[Role Controller]
    Gateway --> Groups[Group Controller]
    
    Auth --> AuthService[Auth Service]
    Users --> UserService[User Service]
    Roles --> RoleService[Role Service]
    Groups --> GroupService[Group Service]
    
    AuthService --> DB[(PostgreSQL)]
    UserService --> DB
    RoleService --> DB
    GroupService --> DB
    
    AuthService --> Redis[(Redis Cache)]
    UserService --> Redis
    
    AuthService --> Kafka[Kafka Events]
    UserService --> Kafka
    
    DB --> Prisma[Prisma ORM]
```

### 🏛️ Architectural Principles

- **🔄 Separation of Concerns**: Clear separation between controllers, services, and data layers
- **🎯 Single Responsibility**: Each service handles one domain
- **🔌 Dependency Injection**: Loose coupling between components
- **📦 Domain-Driven Design**: Business logic organized by domain
- **🚀 Event-Driven**: Async communication through Kafka
- **💾 Caching Strategy**: Redis for frequently accessed data

---

## 🛠 Technology Stack

### 🖥️ **Backend Technologies**

| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| **Node.js** | 18+ | Runtime environment | [docs](https://nodejs.org/docs/) |
| **TypeScript** | 5.3+ | Type-safe JavaScript | [docs](https://www.typescriptlang.org/docs/) |
| **Express.js** | 4.18+ | Web framework | [docs](https://expressjs.com/) |
| **Prisma** | 5.7+ | Database ORM | [docs](https://www.prisma.io/docs/) |
| **PostgreSQL** | 16.3 | Primary database | [docs](https://www.postgresql.org/docs/) |
| **Redis** | 7.0+ | Caching & sessions | [docs](https://redis.io/docs/) |
| **Kafka** | 3.0+ | Event streaming | [docs](https://kafka.apache.org/docs/) |

### 🧪 **Development & Testing**

| Tool | Purpose | Configuration |
|------|---------|---------------|
| **Jest** | Testing framework | `jest.config.json` |
| **ESLint** | Code linting | `eslint.config.mjs` |
| **Prettier** | Code formatting | `.prettierrc` |
| **Nodemon** | Development server | `nodemon.json` |
| **Docker** | Containerization | `Dockerfile`, `docker-compose.yml` |

### 📦 **Key Dependencies**

```json
{
  "dependencies": {
    "express": "^4.18.2",
    "@prisma/client": "^5.7.1",
    "bcrypt": "^5.1.1",
    "jsonwebtoken": "^9.0.2",
    "joi": "^17.11.0",
    "redis": "^4.6.10",
    "kafkajs": "^2.2.4",
    "winston": "^3.11.0",
    "cors": "^2.8.5",
    "helmet": "^7.1.0",
    "express-rate-limit": "^7.1.5"
  },
  "devDependencies": {
    "typescript": "^5.3.3",
    "jest": "^29.7.0",
    "@types/node": "^20.10.5",
    "eslint": "^8.56.0",
    "prisma": "^5.7.1",
    "nodemon": "^3.0.2"
  }
}
```

---

## 📁 Project Structure

```
identity-service-v6/
├── 📁 src/                          # Source code
│   ├── 📁 controllers/              # HTTP request handlers
│   │   ├── auth.controller.ts       # Authentication endpoints
│   │   ├── user.controller.ts       # User management
│   │   ├── role.controller.ts       # Role management
│   │   └── group.controller.ts      # Group management
│   ├── 📁 services/                 # Business logic layer
│   │   ├── auth.service.ts          # Authentication logic
│   │   ├── user.service.ts          # User operations
│   │   ├── role.service.ts          # Role operations
│   │   └── group.service.ts         # Group operations
│   ├── 📁 middleware/               # Express middleware
│   │   ├── auth.ts                  # JWT authentication
│   │   ├── validation.ts            # Request validation
│   │   ├── rateLimiting.ts          # Rate limiting
│   │   └── errorHandler.ts          # Error handling
│   ├── 📁 routes/                   # API route definitions
│   │   ├── auth.routes.ts           # Auth endpoints
│   │   ├── user.routes.ts           # User endpoints
│   │   ├── role.routes.ts           # Role endpoints
│   │   └── group.routes.ts          # Group endpoints
│   ├── 📁 types/                    # TypeScript type definitions
│   │   ├── index.ts                 # Common types
│   │   ├── auth.ts                  # Auth-related types
│   │   ├── user.ts                  # User types
│   │   └── api.ts                   # API response types
│   ├── 📁 utils/                    # Utility functions
│   │   ├── constants.ts             # Application constants
│   │   ├── helpers.ts               # Helper functions
│   │   ├── logger.ts                # Logging configuration
│   │   └── validators.ts            # Custom validators
│   ├── 📁 config/                   # Configuration files
│   │   ├── index.ts                 # Main config
│   │   ├── database.ts              # DB configuration
│   │   ├── redis.ts                 # Redis config
│   │   └── kafka.ts                 # Kafka config
│   └── index.ts                     # Application entry point
├── 📁 tests/                        # Test files
│   ├── 📁 unit/                     # Unit tests
│   ├── 📁 integration/              # Integration tests
│   ├── 📁 fixtures/                 # Test data
│   └── setup.ts                     # Test setup
├── 📁 prisma/                       # Database schema & migrations
│   ├── schema.prisma                # Database schema
│   ├── 📁 migrations/               # Migration files
│   └── seed.ts                      # Database seeding
├── 📁 docs/                         # Documentation
│   ├── api.md                       # API documentation
│   ├── deployment.md                # Deployment guide
│   └── architecture.md              # Architecture overview
├── 📁 scripts/                      # Build & deployment scripts
├── 📁 .github/                      # GitHub workflows & templates
│   ├── 📁 workflows/                # CI/CD pipelines
│   └── 📁 ISSUE_TEMPLATE/           # Issue templates
├── docker-compose.yml               # Docker services
├── Dockerfile                       # Application container
├── package.json                     # Dependencies & scripts
├── tsconfig.json                    # TypeScript configuration
├── jest.config.json                 # Test configuration
├── eslint.config.mjs                # Linting rules
└── README.md                        # Project documentation
```

---

## 🚀 Quick Start

### 🔧 **Prerequisites**

```bash
# Required versions
node --version    # >= 18.0.0
npm --version     # >= 9.0.0
psql --version    # >= 16.3
docker --version  # >= 20.0.0 (optional)
```

### ⚡ **5-Minute Setup**

```bash
# 1. Clone and install
git clone https://github.com/topcoder/identity-service-v6.git
cd identity-service-v6
npm install

# 2. Environment setup
cp .env.example .env
# Edit .env with your database credentials

# 3. Database setup
npm run prisma:generate
npm run prisma:migrate
npm run db:seed

# 4. Start development server
npm run dev
```

🎉 **Server running at**: `http://localhost:3000`

### 🐳 **Docker Quick Start**

```bash
# One command to rule them all
docker-compose up -d

# Verify services
docker-compose ps
curl http://localhost:3000/health
```

---

## 🔧 Configuration

### 📄 **Environment Variables**

Create a `.env` file in the project root:

```env
# 🗄️ Database Configuration
DATABASE_URL="postgresql://username:password@localhost:5432/identity_service"
DB_POOL_MIN=5
DB_POOL_MAX=20

# 🔐 JWT Configuration
JWT_SECRET="your-super-secret-jwt-key-minimum-32-characters"
JWT_EXPIRES_IN="24h"
JWT_REFRESH_EXPIRES_IN="7d"
JWT_ALGORITHM="HS256"

# 🚀 Redis Configuration (Optional)
REDIS_HOST="localhost"
REDIS_PORT=6379
REDIS_PASSWORD=""
REDIS_DB=0
REDIS_TTL=3600

# 📡 Kafka Configuration (Optional)
KAFKA_BROKERS="localhost:9092"
KAFKA_CLIENT_ID="identity-service"
KAFKA_GROUP_ID="identity-service-group"

# 🌐 Server Configuration
NODE_ENV="development"
PORT=3000
HOST="0.0.0.0"
API_VERSION="v1"

# 🛡️ Security Configuration
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX_REQUESTS=100
BCRYPT_ROUNDS=12
SESSION_SECRET="your-session-secret"

# 📧 Email Configuration (Optional)
SMTP_HOST="smtp.gmail.com"
SMTP_PORT=587
SMTP_USER="your-email@gmail.com"
SMTP_PASS="your-app-password"

# 📊 Monitoring Configuration
LOG_LEVEL="info"
LOG_FILE="logs/app.log"
ENABLE_METRICS=true
HEALTH_CHECK_INTERVAL=30000
```

### ⚙️ **TypeScript Configuration**

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "lib": ["ES2020"],
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true,
    "declaration": true,
    "declarationMap": true,
    "sourceMap": true,
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true,
    "allowSyntheticDefaultImports": true,
    "baseUrl": "./src",
    "paths": {
      "@/*": ["*"],
      "@/controllers/*": ["controllers/*"],
      "@/services/*": ["services/*"],
      "@/models/*": ["models/*"],
      "@/middleware/*": ["middleware/*"],
      "@/utils/*": ["utils/*"],
      "@/config/*": ["config/*"],
      "@/types/*": ["types/*"]
    }
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist", "**/*.test.ts", "**/*.spec.ts"]
}
```

---

## 📚 API Documentation

### 🔗 **Base URL**: `http://localhost:3000/api/v1`

### 🔐 **Authentication Endpoints**

#### POST `/auth/login`
User authentication with email and password.

**Request:**
```json
{
  "email": "user@example.com",
  "password": "securePassword123"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "user": {
      "id": "123e4567-e89b-12d3-a456-426614174000",
      "email": "user@example.com",
      "firstName": "John",
      "lastName": "Doe",
      "roles": ["user"]
    }
  },
  "meta": {
    "timestamp": "2024-01-01T00:00:00.000Z",
    "requestId": "req_123456789"
  }
}
```

#### POST `/auth/refresh`
Refresh access token using refresh token.

**Headers:**
```
Authorization: Bearer <refresh-token>
```

#### POST `/auth/logout`
Invalidate user session and tokens.

### 👥 **User Management Endpoints**

#### GET `/users`
Retrieve paginated list of users.

**Query Parameters:**
- `page` (number): Page number (default: 1)
- `limit` (number): Items per page (default: 10, max: 100)
- `search` (string): Search in name/email
- `role` (string): Filter by role
- `status` (string): Filter by status (active/inactive)

**Response:**
```json
{
  "success": true,
  "data": {
    "users": [
      {
        "id": "123e4567-e89b-12d3-a456-426614174000",
        "email": "user@example.com",
        "firstName": "John",
        "lastName": "Doe",
        "status": "active",
        "createdAt": "2024-01-01T00:00:00.000Z"
      }
    ],
    "pagination": {
      "page": 1,
      "limit": 10,
      "total": 150,
      "totalPages": 15
    }
  }
}
```

#### POST `/users`
Create a new user account.

**Request:**
```json
{
  "email": "newuser@example.com",
  "firstName": "Jane",
  "lastName": "Smith",
  "password": "securePassword123",
  "roles": ["user"]
}
```

#### GET `/users/:id`
Retrieve user by ID.

#### PUT `/users/:id`
Update user information.

#### DELETE `/users/:id`
Delete user account (soft delete).

### 🎭 **Role Management Endpoints**

#### GET `/roles`
List all available roles.

#### POST `/roles`
Create a new role.

**Request:**
```json
{
  "name": "moderator",
  "description": "Community moderator with enhanced permissions",
  "permissions": ["user.read", "user.moderate", "content.moderate"]
}
```

### 👥 **Group Management Endpoints**

#### GET `/groups`
List all groups.

#### POST `/groups`
Create a new group.

**Request:**
```json
{
  "name": "developers",
  "description": "Software development team",
  "type": "private",
  "members": ["user-id-1", "user-id-2"]
}
```

### 📊 **Response Format**

All API responses follow a consistent structure:

**Success Response:**
```json
{
  "success": true,
  "data": { /* response data */ },
  "message": "Operation completed successfully",
  "meta": {
    "timestamp": "2024-01-01T00:00:00.000Z",
    "requestId": "req_123456789",
    "version": "v1"
  }
}
```

**Error Response:**
```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input data",
    "details": [
      {
        "field": "email",
        "message": "Email is required",
        "code": "REQUIRED"
      }
    ]
  },
  "meta": {
    "timestamp": "2024-01-01T00:00:00.000Z",
    "requestId": "req_123456789"
  }
}
```

### 🔒 **Authentication**

Most endpoints require authentication. Include the JWT token in the Authorization header:

```
Authorization: Bearer <your-jwt-token>
```

### 📝 **Interactive Documentation**

When running in development mode, access the full Swagger documentation:

🔗 **http://localhost:3000/api-docs**

---

## 🧪 Testing

### 🎯 **Testing Strategy**

Our comprehensive testing approach ensures code quality and reliability:

- **Unit Tests**: Test individual functions and methods
- **Integration Tests**: Test API endpoints and database interactions
- **Service Tests**: Test business logic in services
- **Contract Tests**: Ensure API contract compliance

### 🏃‍♂️ **Running Tests**

```bash
# Run all tests
npm test

# Run tests with coverage report
npm run test:coverage

# Run tests in watch mode (development)
npm run test:watch

# Run only unit tests
npm run test:unit

# Run only integration tests
npm run test:integration

# Run specific test file
npm test -- user.service.test.ts

# Run tests with specific pattern
npm test -- --testNamePattern="should create user"
```

### 📊 **Coverage Reports**

Test coverage reports are generated in the `coverage/` directory:

```bash
# Generate and view coverage report
npm run test:coverage
open coverage/lcov-report/index.html
```

**Coverage Targets:**
- **Overall**: 90%+
- **Services**: 95%+
- **Controllers**: 85%+
- **Utils**: 100%

### 🧪 **Test Structure**

```typescript
// Example test file: user.service.test.ts
describe('UserService', () => {
  let userService: UserService;
  let mockPrisma: jest.Mocked<PrismaClient>;

  beforeEach(async () => {
    // Setup test environment
    mockPrisma = createMockPrismaClient();
    userService = new UserService(mockPrisma);
  });

  describe('createUser', () => {
    it('should create user with valid data', async () => {
      // Arrange
      const userData = {
        email: 'test@example.com',
        firstName: 'John',
        lastName: 'Doe',
        password: 'securePassword123'
      };

      mockPrisma.user.create.mockResolvedValue({
        id: '123',
        ...userData,
        createdAt: new Date(),
        updatedAt: new Date()
      });

      // Act
      const result = await userService.createUser(userData);

      // Assert
      expect(result).toBeDefined();
      expect(result.email).toBe(userData.email);
      expect(mockPrisma.user.create).toHaveBeenCalledWith({
        data: expect.objectContaining({
          email: userData.email,
          firstName: userData.firstName,
          lastName: userData.lastName
        })
      });
    });

    it('should throw error for duplicate email', async () => {
      // Test duplicate email scenario
    });
  });
});
```

### 🛠️ **Test Configuration**

```json
{
  "preset": "ts-jest",
  "testEnvironment": "node",
  "roots": ["<rootDir>/src", "<rootDir>/tests"],
  "testMatch": ["**/__tests__/**/*.ts", "**/?(*.)+(spec|test).ts"],
  "transform": {
    "^.+\\.ts$": "ts-jest"
  },
  "collectCoverageFrom": [
    "src/**/*.ts",
    "!src/**/*.d.ts",
    "!src/index.ts"
  ],
  "coverageDirectory": "coverage",
  "coverageReporters": ["text", "lcov", "html"],
  "setupFilesAfterEnv": ["<rootDir>/tests/setup.ts"]
}
```

---

## 🐳 Docker Deployment

### 🚀 **Quick Docker Setup**

```bash
# Build and run with Docker Compose
docker-compose up -d

# View logs
docker-compose logs -f api

# Stop services
docker-compose down
```

### 📦 **Docker Services**

The `docker-compose.yml` includes all necessary services:

- **PostgreSQL**: Primary database
- **Redis**: Caching layer
- **Kafka**: Event streaming
- **Identity API**: Main application

### 🏗️ **Custom Build**

```bash
# Build application image
docker build -t identity-service-v6 .

# Run with custom environment
docker run -d \
  --name identity-api \
  -p 3000:3000 \
  -e DATABASE_URL="postgresql://user:pass@db:5432/identity" \
  -e JWT_SECRET="your-secret" \
  identity-service-v6
```

### 🔧 **Production Docker Configuration**

```yaml
# docker-compose.prod.yml
version: '3.8'
services:
  api:
    image: identity-service-v6:latest
    environment:
      - NODE_ENV=production
      - DATABASE_URL=${DATABASE_URL}
      - JWT_SECRET=${JWT_SECRET}
      - REDIS_HOST=redis
    deploy:
      replicas: 3
      restart_policy:
        condition: on-failure
        max_attempts: 3
      resources:
        limits:
          memory: 512M
          cpus: '0.5'
```

### 🏥 **Health Checks**

```bash
# Check service health
curl http://localhost:3000/health

# Expected response
{
  "success": true,
  "message": "Identity Service is healthy",
  "data": {
    "uptime": 3600,
    "database": "connected",
    "redis": "connected",
    "memory": "45.2 MB",
    "version": "1.0.0"
  }
}
```

---

## 🔒 Security Features

### 🛡️ **Authentication Security**

- **JWT Tokens**: Secure token-based authentication
- **Refresh Tokens**: Long-lived tokens for token renewal
- **Password Hashing**: bcrypt with configurable rounds
- **Token Expiration**: Configurable token lifetimes
- **Blacklist Support**: Revoked token management

### 🚨 **API Security**

- **Rate Limiting**: Configurable request rate limits
- **CORS**: Cross-origin request security
- **Helmet**: Security headers middleware
- **Input Validation**: Request validation with Joi
- **SQL Injection Protection**: Prisma ORM prevents SQL injection
- **XSS Protection**: Input sanitization

### 🔐 **Authorization**

- **Role-Based Access Control (RBAC)**: Fine-grained permissions
- **Resource-Level Security**: Object-level permissions
- **API Key Authentication**: Service-to-service authentication
- **Scope-Based Access**: Limited permission scopes

### 📋 **Security Headers**

```typescript
// Automatically applied security headers
{
  "X-Content-Type-Options": "nosniff",
  "X-Frame-Options": "DENY",
  "X-XSS-Protection": "1; mode=block",
  "Strict-Transport-Security": "max-age=31536000; includeSubDomains",
  "Content-Security-Policy": "default-src 'self'",
  "Referrer-Policy": "strict-origin-when-cross-origin"
}
```

### 🔍 **Security Best Practices**

- **Environment Variables**: Sensitive data in environment variables
- **Secrets Management**: Secure secret storage
- **Regular Updates**: Dependency vulnerability scanning
- **Error Handling**: No sensitive data in error messages
- **Logging**: Security event logging without sensitive data

---

## 📊 Database Schema

### 🏗️ **Entity Relationship Diagram**

```mermaid
erDiagram
    User ||--o{ UserRole : has
    User ||--o{ UserGroup : belongs_to
    Role ||--o{ UserRole : assigned_to
    Group ||--o{ UserGroup : contains
    User ||--o{ Session : creates
    
    User {
        uuid id PK
        string email UK
        string firstName
        string lastName
        string passwordHash
        string status
        datetime createdAt
        datetime updatedAt
    }
    
    Role {
        uuid id PK
        string name UK
        string description
        json permissions
        datetime createdAt
        datetime updatedAt
    }
    
    Group {
        uuid id PK
        string name UK
        string description
        string type
        datetime createdAt
        datetime updatedAt
    }
    
    UserRole {
        uuid userId FK
        uuid roleId FK
        datetime assignedAt
    }
    
    UserGroup {
        uuid userId FK
        uuid groupId FK
        string membershipType
        datetime joinedAt
    }
    
    Session {
        uuid id PK
        uuid userId FK
        string token
        datetime expiresAt
        datetime createdAt
    }
```

### 📋 **Database Tables**

#### Users Table
```sql
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    status VARCHAR(20) DEFAULT 'active',
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_status ON users(status);
```

#### Roles Table
```sql
CREATE TABLE roles (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(50) UNIQUE NOT NULL,
    description TEXT,
    permissions JSONB DEFAULT '[]',
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

CREATE INDEX idx_roles_name ON roles(name);
```

#### Groups Table
```sql
CREATE TABLE groups (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(100) UNIQUE NOT NULL,
    description TEXT,
    type VARCHAR(20) DEFAULT 'public',
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

CREATE INDEX idx_groups_name ON groups(name);
CREATE INDEX idx_groups_type ON groups(type);
```

### 🔧 **Prisma Schema**

```prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id           String   @id @default(uuid())
  email        String   @unique
  firstName    String   @map("first_name")
  lastName     String   @map("last_name")
  passwordHash String   @map("password_hash")
  status       String   @default("active")
  createdAt    DateTime @default(now()) @map("created_at")
  updatedAt    DateTime @updatedAt @map("updated_at")

  // Relations
  roles    UserRole[]
  groups   UserGroup[]
  sessions Session[]

  @@map("users")
}

model Role {
  id          String   @id @default(uuid())
  name        String   @unique
  description String?
  permissions Json     @default("[]")
  createdAt   DateTime @default(now()) @map("created_at")
  updatedAt   DateTime @updatedAt @map("updated_at")

  // Relations
  users UserRole[]

  @@map("roles")
}

model Group {
  id          String   @id @default(uuid())
  name        String   @unique
  description String?
  type        String   @default("public")
  createdAt   DateTime @default(now()) @map("created_at")
  updatedAt   DateTime @updatedAt @map("updated_at")

  // Relations
  members UserGroup[]

  @@map("groups")
}

model UserRole {
  userId     String   @map("user_id")
  roleId     String   @map("role_id")
  assignedAt DateTime @default(now()) @map("assigned_at")

  // Relations
  user User @relation(fields: [userId], references: [id], onDelete: Cascade)
  role Role @relation(fields: [roleId], references: [id], onDelete: Cascade)

  @@id([userId, roleId])
  @@map("user_roles")
}

model UserGroup {
  userId         String   @map("user_id")
  groupId        String   @map("group_id")
  membershipType String   @default("member") @map("membership_type")
  joinedAt       DateTime @default(now()) @map("joined_at")

  // Relations
  user  User  @relation(fields: [userId], references: [id], onDelete: Cascade)
  group Group @relation(fields: [groupId], references: [id], onDelete: Cascade)

  @@id([userId, groupId])
  @@map("user_groups")
}

model Session {
  id        String   @id @default(uuid())
  userId    String   @map("user_id")
  token     String   @unique
  expiresAt DateTime @map("expires_at")
  createdAt DateTime @default(now()) @map("created_at")

  // Relations
  user User @relation(fields: [userId], references: [id], onDelete: Cascade)

  @@map("sessions")
}
```

---

## 🌐 Environment Setup

### 💻 **Development Environment**

```bash
# Install Node.js 18+
nvm install 18
nvm use 18

# Install PostgreSQL
# macOS
brew install postgresql@16
brew services start postgresql@16

# Ubuntu
sudo apt update
sudo apt install postgresql-16

# Install Redis (optional)
# macOS
brew install redis
brew services start redis

# Ubuntu
sudo apt install redis-server
```

### 📦 **Package Scripts**

```json
{
  "scripts": {
    "dev": "nodemon src/index.ts",
    "build": "tsc",
    "start": "node dist/index.js",
    "test": "jest",
    "test:watch": "jest --watch",
    "test:coverage": "jest --coverage",
    "lint": "eslint src/**/*.ts",
    "lint:fix": "eslint src/**/*.ts --fix",
    "format": "prettier --write src/**/*.ts",
    "prisma:generate": "prisma generate",
    "prisma:migrate": "prisma migrate dev",
    "prisma:studio": "prisma studio",
    "prisma:reset": "prisma migrate reset --force",
    "db:seed": "tsx prisma/seed.ts",
    "docker:build": "docker build -t identity-service-v6 .",
    "docker:run": "docker-compose up -d",
    "docker:stop": "docker-compose down",
    "precommit": "npm run lint && npm run test",
    "prepare": "husky install"
  }
}
```

### 🔄 **Development Workflow**

```bash
# 1. Start development services
npm run docker:run  # or manually start postgres/redis

# 2. Run database migrations
npm run prisma:migrate

# 3. Start development server
npm run dev

# 4. Run tests in watch mode (separate terminal)
npm run test:watch

# 5. Format and lint before committing
npm run format
npm run lint:fix
npm run test
```

### 🏗️ **Build Process**

```bash
# Development build
npm run build

# Production build with optimization
NODE_ENV=production npm run build

# Build and test
npm run build && npm test

# Build Docker image
npm run docker:build
```

---

## 🤝 Contributing

### 📋 **Contribution Guidelines**

We welcome contributions! Please follow these guidelines:

1. **🍴 Fork the repository** and create a feature branch
2. **📝 Write tests** for new functionality
3. **✅ Ensure all tests pass** and coverage remains high
4. **🎨 Follow code style** guidelines (ESLint + Prettier)
5. **📖 Update documentation** as needed
6. **🔍 Submit a pull request** with detailed description

### 🌟 **Development Standards**

- **TypeScript**: Strict mode with proper typing
- **Testing**: 90%+ code coverage required
- **Documentation**: JSDoc comments for public APIs
- **Git**: Conventional commit messages
- **Code Review**: All changes require review

### 🚀 **Feature Development Process**

```bash
# 1. Create feature branch
git checkout -b feature/user-profile-enhancement

# 2. Implement feature with tests
# ... code changes ...

# 3. Run quality checks
npm run lint:fix
npm run test
npm run build

# 4. Commit with conventional message
git commit -m "feat: add user profile picture upload

- Implement multer middleware for file uploads
- Add image validation and resizing
- Update user model with avatar field
- Add comprehensive tests

Closes #123"

# 5. Push and create PR
git push origin feature/user-profile-enhancement
```

### 📝 **Commit Message Format**

```
type(scope): description

body

footer
```

**Types**: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

### 🐛 **Bug Reports**

Use the [bug report template](.github/ISSUE_TEMPLATE/bug_report.md):

- Clear description of the issue
- Steps to reproduce
- Expected vs actual behavior
- Environment details
- Relevant logs or screenshots

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2024 Topcoder

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 📞 Support & Contact

### 🆘 **Getting Help**

- **📖 Documentation**: Check this README and `/docs` folder
- **🐛 Issues**: [GitHub Issues](../../issues) for bugs and feature requests
- **💬 Discussions**: [GitHub Discussions](../../discussions) for questions
- **📧 Email**: platform@topcoder.com for urgent matters

### 🏢 **Topcoder Platform**

- **Website**: [topcoder.com](https://www.topcoder.com)
- **Community**: [topcoder.com/community](https://www.topcoder.com/community)
- **Documentation**: [docs.topcoder.com](https://docs.topcoder.com)

### 👥 **Team**

- **Platform Team**: platform@topcoder.com
- **Security Team**: security@topcoder.com
- **DevOps Team**: devops@topcoder.com

---

<div align="center">

**🚀 Ready to build the future of identity management? 🚀**

[![GitHub Stars](https://img.shields.io/github/stars/topcoder/identity-service-v6?style=social)](https://github.com/topcoder/identity-service-v6/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/topcoder/identity-service-v6?style=social)](https://github.com/topcoder/identity-service-v6/network/members)

*Built with ❤️ by the Topcoder Platform Team*

</div>

---

*Last updated: June 29, 2025 | Version: 1.0.0 | Identity Service v6*
