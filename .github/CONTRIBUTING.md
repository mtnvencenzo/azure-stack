# 🔵 Contributing to Azure Stack

Thank you for your interest in contributing to the Azure Stack project! We welcome contributions that help improve our Azure service emulators setup, documentation, and developer experience for local Azure development.

## 📋 Table of Contents

- [Getting Started](#-getting-started)
- [Development Setup](#-development-setup)
- [Contributing Process](#-contributing-process)
- [Code Standards](#-code-standards)
- [Testing](#-testing)
- [Getting Help](#-getting-help)

## 🚀 Getting Started

### 🧰 Prerequisites

Before you begin, ensure you have the following installed:
- Docker and Docker Compose
- Git

### 🗂️ Project Structure

```text
├── docker-compose.yml             # Azure service emulators configuration
├── volumes/                       # Persistent data directories
│   ├── azurite-data/             # Azurite storage data
│   └── cosmosdb-data/            # CosmosDB emulator data
├── assets/                       # Documentation and guides
│   ├── readme-azurite.md         # Azurite setup guide
│   └── readme-cosmos.md          # CosmosDB setup guide
└── .github/                      # GitHub workflows and templates
```

## 💻 Development Setup

1. **Fork and Clone the Repository**
   ```bash
   git clone https://github.com/mtnvencenzo/azure-stack.git
   cd azure-stack
   ```

2. **Start the Azure Services**
   ```bash
   # Start all services
   docker compose up -d
   
   # Verify services are running
   docker compose ps
   ```

3. **Test the Setup**
   ```bash
   # Test Azurite
   curl http://localhost:10000/devstoreaccount1?comp=list
   
   # Test CosmosDB (may need to trust certificate first)
   curl -k https://localhost:8081/_explorer/emulator.pem
   ```

## 🔄 Contributing Process

### 1. 📝 Before You Start

- **Check for existing issues** to avoid duplicate work
- **Create or comment on an issue** to discuss your proposed changes
- **Wait for approval** from maintainers before starting work (required for this repository)

### 2. 🛠️ Making Changes

1. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   # or
   git checkout -b fix/your-bug-fix
   ```

2. **Make your changes** following our [code standards](#-code-standards)

4. **Commit your changes**
   ```bash
   git add .
   git commit -m "feat(api): add new endpoint for ..."
   ```
   
   Use [conventional commit format](https://www.conventionalcommits.org/):
   - `feat:` for new features
   - `fix:` for bug fixes
   - `docs:` for documentation changes
   - `style:` for formatting changes
   - `refactor:` for code refactoring
   - `test:` for adding tests
   - `chore:` for maintenance tasks

### 3. 📬 Submitting Changes

1. **Push your branch**
   ```bash
   git push origin feature/your-feature-name
   ```

2. **Create a Pull Request**
   - Use our [PR template](pull_request_template.md)
   - Fill out all sections completely
   - Link related issues using `Closes #123` or `Fixes #456`
   - Request review from maintainers

## 📏 Code Standards

### 🐳 Docker & Docker Compose

- Use official Microsoft Azure service images
- Follow Docker best practices for service configuration
- Use meaningful container and service names
- Include proper health checks where available
- Document any custom configurations

### 📝 Documentation

- Update documentation when making changes
- Use clear, concise language
- Include code examples for setup instructions
- Update service endpoint information when ports change

### 🗂️ File Organization

- Keep service-specific documentation in the `assets/` folder
- Use consistent naming conventions
- Update docker-compose.yml with proper comments

### 🔍 Validation Steps

Before submitting changes:

```bash
# Verify services start correctly
docker compose up -d

# Check service health
docker compose ps

# Test Azurite connectivity
curl http://localhost:10000/devstoreaccount1?comp=list

# Test CosmosDB connectivity (may require certificate trust)
curl -k https://localhost:8081/_explorer/emulator.pem

# Clean up
docker compose down -v
```

### 📏 Test Requirements

- **Service Startup**: All services must start without errors
- **Port Accessibility**: All documented ports must be accessible
- **Data Persistence**: Volume mounts must work correctly
- **Documentation**: Any changes must be documented

## 🆘 Getting Help

### 📡 Communication Channels

- **Issues**: Use GitHub issues for bugs and feature requests
- **Discussions**: Use GitHub Discussions for questions and ideas
- **Email**: Contact maintainers directly for sensitive issues

### 📄 Issue Templates

Use our issue templates for:
- [Task Stories](./ISSUE_TEMPLATE/task-template.md)
- [User Stories](./ISSUE_TEMPLATE/user-story-template.md)

### ❓ Common Questions

**Q: How do I run the Azure services locally?**
A: Follow the [Development Setup](#-development-setup) section above. Use `docker compose up -d`.

**Q: How do I test if the services are working?**
A: Check the service health endpoints and try connecting with Azure Storage Explorer (for Azurite) or the CosmosDB Data Explorer.

**Q: Can I contribute without approval?**
A: No, all contributors must be approved by maintainers before making changes.

**Q: How do I add a new Azure service emulator?**
A: Add the service to docker-compose.yml, create documentation in the assets/ folder, and update the main README.md.
A: Please email the maintainers directly rather than creating a public issue.

## 📜 License

By contributing to this project, you agree that your contributions will be licensed under the same license as the project (see [LICENSE](../LICENSE)).

---

**Happy Contributing! 🍸**

For any questions about this contributing guide, please open an issue or contact the maintainers.
