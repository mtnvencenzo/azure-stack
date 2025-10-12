# Azure Stack - Local Development Environment

This repository provides a Docker Compose setup for running Azure service emulators locally, giving you a complete Azure development environment without needing cloud resources. Perfect for local development, testing, and CI/CD pipelines.

![Azure Stack Architecture](./assets/azure-stack.drawio.svg)

## 📁 Contents

- **docker-compose.yml**: Docker Compose configuration for Azure service emulators
- **volumes/**: Persistent data directories for Azurite and CosmosDB
- **assets/**: Documentation and setup guides for individual services
- **README.md**: This documentation file

## ⚙️ Prerequisites

- [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/) installed on your machine

## 🏗️ Architecture

This setup provides the following Azure service emulators:

- **Azurite** - Azure Storage emulator for Blob, Queue, and Table storage (ports 10000-10002)
- **CosmosDB Emulator** - Azure Cosmos DB emulator for NoSQL database development (ports 8081, 1234)

All containers run within a dedicated `azure-network` bridge network for secure inter-service communication.

## 🚀 Setup & Usage

> This setup is designed for local development and testing. Do not use in production environments.

1. **Start the Azure service emulators:**

    ```bash
    docker compose -p azure-stack -f docker-compose.yml up -d

    # Or if the containers have already been created
    docker compose -p azure-stack -f docker-compose.yml start

    ```

    This will start all Azure service emulators and create the necessary network and volumes for data persistence.

2. **Stop the services:**
    ```bash
    docker compose -p azure-stack -f docker-compose.yml down -v
    ```

3. **Rebuild and restart a specific service:**
    ```bash
    docker compose -p azure-stack -f docker-compose.yml up -d --force-recreate --no-deps --build <service_name>
    ```

4. **Verify Services are Running:**
    ```bash
    # Check all services status
    docker compose ps
    
    # Test Azurite (Azure Storage)
    curl http://localhost:10000/devstoreaccount1?comp=list
    
    # Test CosmosDB Emulator
    curl -k https://localhost:8081/_explorer/emulator.pem
    ```

5. **Connect to Services:**

    **Azurite (Azure Storage):**
    - Blob Storage: `http://localhost:10000`
    - Queue Storage: `http://localhost:10001`
    - Table Storage: `http://localhost:10002`
    - Connection String: `DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;`

    **CosmosDB Emulator:**
    - Endpoint: `https://localhost:8081`
    - Data Explorer: `http://localhost:1234`
    - Connection String: `AccountEndpoint=https://localhost:8081/;AccountKey=C2y6yDjf5R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==;`

## 🛠️ Customization

- Modify `docker-compose.yml` to adjust service configurations, ports, or resource limits as needed for your environment.
- Update volume mounts in `volumes/` directory for persistent data storage requirements.
- See individual service documentation in the `assets/` folder for detailed configuration options.

## 📊 Service Endpoints & Ports

### Azure Storage (Azurite)
- **Blob Storage**: `localhost:10000` (HTTP)
- **Queue Storage**: `localhost:10001` (HTTP)
- **Table Storage**: `localhost:10002` (HTTP)
- **Account Name**: `devstoreaccount1`
- **Account Key**: `Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==`

> Note: When adding blob containers for pulic access `PublicAccessType` = `BlobContainer or Container` you might have manually use the storage explorer to set the public access type *(even when setting the access type in code when creating the container)* 

### Azure CosmosDB Emulator
- **CosmosDB Endpoint**: `localhost:8081` (HTTPS)
- **Data Explorer**: `localhost:1234` (HTTP)
- **Account Key**: `C2y6yDjf5R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==`

## 🐞 Troubleshooting

- Check container logs for errors:
  ```bash
  docker compose logs
  
  # Or for a specific service
  docker compose logs azurite
  docker compose logs cosmosdb
  ```
- Ensure no port conflicts with existing services on your machine.
- Validate that Docker has sufficient resources allocated for all containers.
- Check that volumes have proper permissions for data persistence.
- For CosmosDB certificate issues, see the [CosmosDB setup guide](./assets/readme-cosmos.md).
- For Azurite connection issues, see the [Azurite setup guide](./assets/readme-azurite.md).

## 📚 Additional Resources

- **Azurite**: [Official Documentation](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azurite)
- **CosmosDB Emulator**: [Official Documentation](https://learn.microsoft.com/en-us/azure/cosmos-db/emulator-linux)
- **Azure Storage Explorer**: [Download](https://azure.microsoft.com/en-us/products/storage/storage-explorer)

## 🌐 Community & Support

- 🤝 Contributing Guide – see [CONTRIBUTING.md](.github/CONTRIBUTING.md)
- 🤗 Code of Conduct – see [CODE_OF_CONDUCT.md](.github/CODE_OF_CONDUCT.md)
- 🆘 Support Guide – see [SUPPORT.md](.github/SUPPORT.md)
- 🔒 Security Policy – see [SECURITY.md](.github/SECURITY.md)

## 📄 License

This project is licensed under the terms of the repository's main LICENSE file.

---
For more information about Azure service emulators, see the official [Azure documentation](https://docs.microsoft.com/azure/).
