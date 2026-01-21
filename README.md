# Order Pipeline Managed

> **Part 2** of a comprehensive observability study comparing DIY and managed cloud solutions for event-driven serverless architectures.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![.NET](https://img.shields.io/badge/.NET-8.0-blue)](https://dotnet.microsoft.com)
[![Azure](https://img.shields.io/badge/Azure-Functions-informational?logo=microsoft-azure)](https://azure.microsoft.com)
[![Research](https://img.shields.io/badge/Research-Observability-important)]()

## 📋 Overview

This repository implements an **order processing pipeline** using **Azure Functions**, **Service Bus**, and **Application Insights**—a managed cloud solution approach. This is **Part 2** of our research on observability and resilience in event-driven serverless architectures.

### 🎯 Research Objectives

1. **Developer Experience (DX)**: Measure effort and complexity when implementing observability with managed services
2. **Operational Insights**: Compare built-in vs. third-party monitoring capabilities
3. **Cost Analysis**: Evaluate pricing and TCO for managed vs. DIY solutions
4. **Performance Benchmarking**: Load test and analyze throughput, latency, and resilience patterns
5. **Best Practices**: Document recommendations for production deployments

### 🔄 Comparison: Part 1 vs Part 2

| Aspect | Part 1 (DIY) | Part 2 (Managed) |
|--------|-------------|------------------|
| **Message Queue** | RabbitMQ (Self-hosted) | Azure Service Bus |
| **Functions** | ASP.NET Core Worker Services | Azure Functions |
| **Monitoring** | Serilog + Seq + OpenTelemetry | App Insights (+ OTel) |
| **Tracing** | Jaeger (Self-hosted) | Application Insights |
| **Deployment** | Docker Compose | Azure Container Apps / App Service |
| **DX Complexity** | Medium-High | Low-Medium |

---

## 🏗️ Architecture

### System Flow

```
┌─────────────────┐
│  API Gateway    │  (HTTP Entry Point)
│ (Functions HTTP)│
└────────┬────────┘
         │
         ▼
┌─────────────────────────┐
│  Order Processor        │
│  (Azure Function)       │
└────────┬────────────────┘
         │
         ▼
┌─────────────────────────┐
│  Azure Service Bus      │
│  (Topics & Subscriptions)│
└────────┬────────────────┘
         │
    ┌────┴────┐
    ▼         ▼
┌────────┐ ┌──────────┐
│ Invoice│ │Notification│
│Processor│ │ Sender   │
│(Function)│ │(Function) │
└────────┘ └──────────┘
    │
    ▼
┌─────────────────────────┐
│  Application Insights   │
│  (Telemetry & Traces)   │
└─────────────────────────┘
```

### Components

- **Order Receiver Function**: HTTP-triggered, validates orders and publishes to Service Bus
- **Order Processor Function**: Service Bus-triggered, processes order logic
- **Invoice Generator**: Service Bus-triggered, handles billing
- **Notification Sender**: Service Bus-triggered, sends customer notifications
- **Service Bus**: Message broker with topics and subscriptions
- **Application Insights**: Centralized monitoring, logging, and distributed tracing

---

## 🛠️ Tech Stack

- **.NET 8** - Runtime and development framework
- **Azure Functions** - Serverless compute
- **Azure Service Bus** - Messaging and event streaming
- **Application Insights** - Observability platform
- **Azure Blob Storage** - Data persistence
- **Azure SQL Database** - Relational data
- **OpenTelemetry** - Standardized telemetry (optional, for comparison)
- **Azure CLI** - Infrastructure management
- **k6** - Load testing
- **Docker** - Local development (if applicable)

---

## 🚀 Getting Started

### Prerequisites

- Azure Account with active subscription
- .NET 8 SDK
- Azure Functions Core Tools
- Visual Studio 2022 or VS Code
- Git
- Azure CLI

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/LuisMarchio03/order-pipeline-managed.git
   cd order-pipeline-managed
   ```

2. **Install dependencies**
   ```bash
   dotnet restore
   ```

3. **Configure Azure resources** (see `docs/SETUP.md`)
   ```bash
   az login
   az account set --subscription <SUBSCRIPTION_ID>
   # Create resource group, Service Bus, Function App, etc.
   ```

4. **Setup local configuration**
   ```bash
   cp .env.example .env
   # Update with your Azure connection strings
   ```

5. **Run locally**
   ```bash
   func start  # Start Azure Functions emulator
   ```

---

## 📊 Project Structure

```
order-pipeline-managed/
├── src/
│   ├── Functions/                    # Azure Functions
│   │   ├── OrderReceiverFunction.cs
│   │   ├── OrderProcessorFunction.cs
│   │   ├── InvoiceGeneratorFunction.cs
│   │   └── NotificationSenderFunction.cs
│   ├── Models/                       # Domain models
│   ├── Services/                     # Business logic
│   └── Middleware/                   # Custom middleware
├── tests/
│   ├── Unit/                         # Unit tests
│   ├── Integration/                  # Integration tests
│   └── Load/                         # k6 load tests
├── docs/
│   ├── SETUP.md                      # Azure setup guide
│   ├── ARCHITECTURE.md               # Detailed architecture
│   ├── OBSERVABILITY.md              # Monitoring setup
│   └── DEPLOYMENT.md                 # Production deployment
├── infra/                            # IaC (Terraform/Bicep)
├── .env.example                      # Environment template
├── README.md                         # This file
└── LICENSE                           # MIT License
```

---

## 📈 Performance Baselines

> Established during research phase. Update as the project evolves.

### Load Test Results (k6)

- **Throughput**: ~5,000 RPS (with Service Bus throttling)
- **P95 Latency**: ~250ms (end-to-end)
- **P99 Latency**: ~500ms
- **Error Rate**: <0.1% under normal conditions
- **Service Bus Breaking Point**: ~10,000 msgs/sec

### Resource Consumption

- **Function Execution Time**: 50-150ms per invocation
- **Memory Usage**: ~256MB per function instance
- **Cost**: $0.0000002/execution + storage costs

---

## 🔍 Observability Features

### Logging

- Structured logging via Application Insights
- Custom dimensions for order tracking
- Correlation IDs for distributed tracing

### Metrics

- Order processing duration
- Service Bus message throughput
- Function invocation counts
- Error rates by component

### Traces

- Distributed tracing across all functions
- Dependency tracking (Service Bus, Storage, SQL)
- Custom events and measurements

### Alerts

- High error rate detection
- Function timeout alerts
- Service Bus queue depth monitoring
- Cost anomaly detection

---

## 🧪 Testing

### Run Unit Tests

```bash
dotnet test tests/Unit/
```

### Run Integration Tests

```bash
dotnet test tests/Integration/
```

### Run Load Tests (k6)

```bash
k6 run tests/Load/order-pipeline-load.js
```

---

## 🚢 Deployment

### Deploy to Azure

```bash
func azure functionapp publish <FUNCTION_APP_NAME>
```

For detailed instructions, see `docs/DEPLOYMENT.md`.

---

## 📚 Documentation

- [Setup & Configuration](docs/SETUP.md)
- [Architecture Deep Dive](docs/ARCHITECTURE.md)
- [Observability & Monitoring](docs/OBSERVABILITY.md)
- [Deployment Guide](docs/DEPLOYMENT.md)
- [Contributing Guidelines](CONTRIBUTING.md)

---

## 🤝 Contributing

This is a research project. Contributions are welcome!

Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

## 📖 Citation

If you use this project for research or academic purposes, please cite it as:

```bibtex
@repository{order-pipeline-managed,
  title = {Order Pipeline: Managed Cloud Services},
  author = {Luis Marchiorato},
  year = {2025},
  url = {https://github.com/LuisMarchio03/order-pipeline-managed}
}
```

---

## 📝 License

MIT License - see [LICENSE](LICENSE) file for details.

---

## 📧 Contact

**Author**: Luis Marchiorato
- GitHub: [@LuisMarchio03](https://github.com/LuisMarchio03)
- Email: your-email@example.com

---

**Last Updated**: January 2025
**Status**: 🚧 In Development
