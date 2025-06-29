# Contributing to Identity Service v6

🎉 Thank you for your interest in contributing to the Identity Service v6! This document provides guidelines and information for contributors.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Process](#development-process)
- [Pull Request Process](#pull-request-process)
- [Coding Standards](#coding-standards)
- [Testing Guidelines](#testing-guidelines)
- [Documentation](#documentation)

## 📜 Code of Conduct

This project adheres to the [Topcoder Code of Conduct](https://www.topcoder.com/community/code-of-conduct). By participating, you are expected to uphold this code.

## 🚀 Getting Started

### Prerequisites

- Node.js 18+
- PostgreSQL 16.3
- Git
- IDE with TypeScript support (VS Code recommended)

### Setup Development Environment

1. **Fork the repository**
   ```bash
   # Fork on GitHub, then clone your fork
   git clone https://github.com/YOUR_USERNAME/identity-service-v6.git
   cd identity-service-v6
   ```

2. **Add upstream remote**
   ```bash
   git remote add upstream https://github.com/topcoder/identity-service-v6.git
   ```

3. **Install dependencies**
   ```bash
   npm install
   ```

4. **Setup environment**
   ```bash
   cp .env.example .env
   # Edit .env with your local configuration
   ```

5. **Setup database**
   ```bash
   npm run prisma:generate
   npm run prisma:migrate
   ```

6. **Verify setup**
   ```bash
   npm test
   npm run build
   npm run lint
   ```

## 🔄 Development Process

### Branch Naming Convention

- `feature/description` - New features
- `bugfix/description` - Bug fixes
- `hotfix/description` - Critical fixes
- `docs/description` - Documentation updates
- `refactor/description` - Code refactoring

### Workflow

1. **Create a feature branch**
   ```bash
   git checkout -b feature/user-profile-enhancement
   ```

2. **Make your changes**
   - Write code following our [coding standards](#coding-standards)
   - Add tests for new functionality
   - Update documentation as needed

3. **Test your changes**
   ```bash
   npm test
   npm run test:coverage
   npm run lint
   npm run build
   ```

4. **Commit your changes**
   ```bash
   git add .
   git commit -m "feat: add user profile enhancement
   
   - Add profile picture upload
   - Implement bio field validation
   - Update user model schema
   
   Closes #123"
   ```

5. **Push and create PR**
   ```bash
   git push origin feature/user-profile-enhancement
   ```

## 🔀 Pull Request Process

### Before Submitting

- [ ] Code follows project coding standards
- [ ] Tests are added/updated and passing
- [ ] Documentation is updated
- [ ] No merge conflicts
- [ ] PR description is clear and detailed

### PR Template

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature  
- [ ] Breaking change
- [ ] Documentation update

## Testing
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] Manual testing completed

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-review completed
- [ ] Comments added for complex logic
- [ ] Documentation updated
```

### Review Process

1. **Automated Checks**
   - CI/CD pipeline runs tests
   - Code coverage checks
   - Linting validation

2. **Code Review**
   - At least 2 approvals required
   - Address all review comments
   - Maintain conversation until resolved

3. **Merge**
   - Squash and merge for feature branches
   - Use conventional commit messages

## 📏 Coding Standards

### TypeScript Guidelines

```typescript
// ✅ Good
interface CreateUserRequest {
  email: string;
  firstName: string;
  lastName: string;
  password: string;
}

export class UserService {
  /**
   * Creates a new user account
   * @param userData - User registration data
   * @returns Promise resolving to created user
   * @throws UserAlreadyExistsError if email is taken
   */
  async createUser(userData: CreateUserRequest): Promise<User> {
    // Implementation
  }
}

// ❌ Avoid
export class UserService {
  async createUser(data: any): Promise<any> {
    // Implementation
  }
}
```

### Code Style

- **ESLint**: Follow project ESLint configuration
- **Prettier**: Use for code formatting
- **Naming**: Use camelCase for variables/functions, PascalCase for classes
- **Comments**: JSDoc for public APIs, inline for complex logic

### File Organization

```
src/
├── controllers/     # HTTP request handlers
├── services/        # Business logic
├── models/          # Data models and schemas
├── middleware/      # Express middleware
├── utils/           # Helper functions
├── types/           # Type definitions
└── config/          # Configuration files
```

## 🧪 Testing Guidelines

### Test Structure

```typescript
describe('UserService', () => {
  describe('createUser', () => {
    it('should create user with valid data', async () => {
      // Arrange
      const userData = {
        email: 'test@example.com',
        firstName: 'John',
        lastName: 'Doe',
        password: 'securepassword'
      };

      // Act
      const result = await userService.createUser(userData);

      // Assert
      expect(result).toBeDefined();
      expect(result.email).toBe(userData.email);
    });

    it('should throw error for duplicate email', async () => {
      // Test implementation
    });
  });
});
```

### Coverage Requirements

- **Minimum**: 90% code coverage
- **Services**: 95% coverage required
- **Controllers**: 85% coverage minimum
- **Utils**: 100% coverage expected

### Test Commands

```bash
npm test                 # Run all tests
npm run test:watch       # Watch mode
npm run test:coverage    # Coverage report
npm run test:unit        # Unit tests only
npm run test:integration # Integration tests only
```

## 📚 Documentation

### Code Documentation

- **JSDoc**: All public methods and classes
- **README**: Keep updated with changes
- **API Docs**: Update Swagger definitions
- **Architecture**: Document design decisions

### API Documentation

```typescript
/**
 * @swagger
 * /api/v1/users:
 *   post:
 *     summary: Create a new user
 *     tags: [Users]
 *     requestBody:
 *       required: true
 *       content:
 *         application/json:
 *           schema:
 *             $ref: '#/components/schemas/CreateUserRequest'
 *     responses:
 *       201:
 *         description: User created successfully
 *         content:
 *           application/json:
 *             schema:
 *               $ref: '#/components/schemas/User'
 */
```

## 🐛 Reporting Issues

### Bug Reports

Use the [bug report template](.github/ISSUE_TEMPLATE/bug_report.md) and include:

- Clear description
- Steps to reproduce
- Expected vs actual behavior
- Environment details
- Relevant logs/screenshots

### Feature Requests

Use the [feature request template](.github/ISSUE_TEMPLATE/feature_request.md) and include:

- Problem description
- Proposed solution
- Use cases
- API design (if applicable)

## 💬 Community

- **GitHub Discussions**: For questions and ideas
- **Issues**: For bugs and feature requests
- **Slack**: #identity-service channel
- **Email**: platform@topcoder.com

## 🏆 Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Mentioned in release notes
- Eligible for Topcoder community rewards

Thank you for contributing to make Identity Service v6 better! 🚀
