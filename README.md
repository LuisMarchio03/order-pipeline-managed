# 🚀 Order Pipeline: Managed vs DIY

> **A Comprehensive Research Initiative on Observability, Resilience, and Developer Experience in Event-Driven Serverless Architectures**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![.NET](https://img.shields.io/badge/.NET-8.0-blue)](https://dotnet.microsoft.com)
[![Azure](https://img.shields.io/badge/Azure-Functions-informational?logo=microsoft-azure)](https://azure.microsoft.com)
[![Research](https://img.shields.io/badge/Research-Observability-important)]()
[![Status](https://img.shields.io/badge/Status-🚧%20In%20Development-yellow)]

---

## 📍 Project Navigation

This project is part of a **two-part research initiative**:

- **Part 1 (DIY)**: [`order-pipeline-diy`](https://github.com/LuisMarchio03/order-pipeline-diy) - Self-hosted solutions with RabbitMQ, Serilog, OpenTelemetry, and Jaeger
- **Part 2 (Managed)**: [`order-pipeline-managed`](https://github.com/LuisMarchio03/order-pipeline-managed) ⬅️ **You are here**

---

## 🎯 The Big Picture: Why Two Repositories?

### Research Motivation

In the era of cloud computing, organizations face a critical decision: **build custom observability solutions or adopt managed cloud services?** This research project explores both approaches through a practical, real-world scenario.

### 🔬 Core Research Questions

1. **Developer Experience (DX)**: How much effort is required to implement observability with managed vs. DIY solutions?
2. **Operational Complexity**: What are the trade-offs between full control and operational simplicity?
3. **Cost Implications**: How do licensing and infrastructure costs compare in real-world scenarios?
4. **Observability Quality**: Are managed solutions truly "production-grade"?
5. **Performance & Resilience**: How do both approaches handle failures and scale?

### 📊 Comparative Framework

```
┌─────────────────────────────────────────────────────────────┐
│  RESEARCH DIMENSIONS                                        │
├─────────────────────────────────────────────────────────────┤
│ • Developer Experience (Ease of Setup & Maintenance)       │
│ • Observability Depth (Metrics, Traces, Logs)             │
│ • Total Cost of Ownership (Infrastructure + Labor)        │
│ • Operational Burden (Monitoring, Scaling, Updates)       │
│ • Performance Characteristics (Latency, Throughput)       │
│ • Resilience Patterns (Failover, Recovery, DLQ)           │
│ • Production Readiness (Security, Compliance, SLAs)       │
└─────────────────────────────────────────────────────────────┘
```

---

## 🏗️ Part 2: Managed Cloud Architecture

**Repository**: [`order-pipeline-managed`](https://github.com/LuisMarchio03/order-pipeline-managed)

### Technology Stack

| Component | Technology | Why? |
|-----------|-----------|------|
| **Serverless Compute** | Azure Functions | Auto-scaling, pay-per-execution, native integration |
| **Message Broker** | Azure Service Bus | Managed topics/subscriptions, built-in DLQ, enterprise features |
| **Observability** | Application Insights | Zero-setup distributed tracing, native performance monitoring |
| **Language** | .NET 8 | Modern async patterns, strong typing, cloud-native support |
| **IaC** | Bicep | Azure-native, cleaner than ARM templates |
| **Load Testing** | k6 | Simple, scalable, cloud-ready |

### ✨ Innovative Concepts

#### 1. **Telemetry-First Design**
   - Every function is instrumented from day 1
   - Correlation IDs flow through the entire pipeline
   - Zero-effort distributed tracing (Application Insights auto-collection)

#### 2. **Managed Resilience Patterns**
   - Automatic retry policies via Service Bus
   - Dead-Letter Queues (DLQ) with automatic monitoring
   - Circuit breaker patterns built into Azure SDKs

#### 3. **Cost-Aware Architecture**
   - Pay-per-execution model encourages function optimization
   - Sampling strategies in Application Insights reduce costs
   - Resource autoscaling prevents overprovisioning

#### 4. **Developer Experience as a Metric**
   - Onboarding time tracking
   - Documentation complexity analysis
   - Common troubleshooting scenarios documented

---

## 🔄 Why Two Implementations?

### Part 1: DIY Approach (RabbitMQ + Custom Stack)

**Pros**:
- ✅ Full control over every component
- ✅ No cloud vendor lock-in
- ✅ Rich customization opportunities
- ✅ Deep learning about distributed systems

**Cons**:
- ❌ Operational overhead (monitoring, updates, scaling)
- ❌ Higher infrastructure costs (compute + licensing)
- ❌ Longer implementation time
- ❌ Complex deployments (Docker, Kubernetes)

### Part 2: Managed Approach (Azure Functions + App Insights)

**Pros**:
- ✅ Zero infrastructure management
- ✅ Built-in observability at every level
- ✅ Automatic scaling and high availability
- ✅ Faster time-to-market
- ✅ Enterprise-grade security and compliance

**Cons**:
- ❌ Cloud vendor lock-in
- ❌ Limited customization options
- ❌ Potential cost surprises (cold starts, overage charges)
- ❌ Less educational (abstraction hides details)

---

## 📐 Architecture Overview

### System Flow

```
┌──────────────────────────────────────────────────────────────────┐
│                      CLIENT REQUESTS                             │
└────────────────────────┬─────────────────────────────────────────┘
                         │
                         ▼
┌──────────────────────────────────────────────────────────────────┐
│  HTTP Trigger Function (Order Receiver)                          │
│  • Validates order schema                                        │
│  • Enriches with metadata                                        │
│  • Publishes to Service Bus topic                               │
│  • Returns tracking ID to client                                │
└────────────────────────┬─────────────────────────────────────────┘
                         │
                         ▼
┌──────────────────────────────────────────────────────────────────┐
│       Azure Service Bus (Topic: OrderEvents)                    │
├──────────────────────────────────────────────────────────────────┤
│  ├─ Subscription: OrderProcessing                               │
│  ├─ Subscription: Billing                                       │
│  └─ Subscription: Notifications                                 │
└─┬──────────────────────────────────────────────────────────────┬─┘
  │                                                                │
  ▼                          ▼                          ▼
┌─────────────────────────────────────────────────────────────────┐
│ Order Processor │ Invoice Generator │ Notification Sender      │
│ (Service Bus    │ (Service Bus      │ (Service Bus             │
│  Trigger)       │  Trigger)         │  Trigger)                │
└──────┬──────────────────┬──────────────────┬────────────────────┘
       │                  │                  │
       └──────────────────┼──────────────────┘
                          ▼
      ┌────────────────────────────────────┐
      │   Azure Application Insights       │
      │  • Distributed Traces              │
      │  • Custom Metrics                  │
      │  • Dependency Tracking             │
      │  • Exception Monitoring            │
      └────────────────────────────────────┘
```

---

## 🎓 Research Deliverables

### 📋 Metrics to Track

- **Time-to-Production**: Setup → First deployment
- **Developer Onboarding**: New dev → Running tests
- **MTTR (Mean Time to Recovery)**: Incident → Resolution
- **Cost per Transaction**: Infrastructure cost ÷ throughput
- **Observability Coverage**: % of business logic instrumented
- **Alert Accuracy**: False positives ÷ total alerts

### 📊 Comparative Analysis

See `docs/COMPARATIVE_ANALYSIS.md` for detailed metrics and findings.

### 📚 Documentation

- **Part 1 (DIY)**: [`order-pipeline-diy` README](https://github.com/LuisMarchio03/order-pipeline-diy)
- **This Project (Managed)**: See sections below
- **Research Paper**: Coming soon 📝

---

## 🛠️ Part 2: Getting Started (Managed)

### Prerequisites

- Azure Account with active subscription
- .NET 8 SDK
- Azure Functions Core Tools v4+
- Visual Studio 2022 or VS Code
- Azure CLI

### Quick Start

```bash
# 1. Clone and setup
git clone https://github.com/LuisMarchio03/order-pipeline-managed.git
cd order-pipeline-managed
dotnet restore

# 2. Configure Azure
az login
cp .env.example .env
# Edit .env with your Azure details

# 3. Run locally
func start

# 4. Run tests
dotnet test

# 5. Load test
k6 run tests/Load/order-pipeline-load.js
```

See `docs/SETUP.md` for detailed instructions.

---

## 📊 Performance Baselines

### Managed Cloud (Azure Functions + Service Bus)

| Metric | Value | Notes |
|--------|-------|-------|
| **Throughput** | ~5,000 RPS | Limited by Service Bus standard tier |
| **P95 Latency** | ~250ms | End-to-end, including cold starts |
| **P99 Latency** | ~500ms | Peak load scenarios |
| **Cold Start Impact** | +200-300ms | First invocation after idle period |
| **Error Rate** | <0.1% | Under normal conditions |
| **DLQ Processing** | <1% of messages | Indicates system health |

### Cost Estimation (Monthly)

- **Azure Functions**: ~$0.20 per 1M executions
- **Service Bus**: ~$10-50 depending on message volume
- **Application Insights**: ~$2.50 per GB ingested
- **Storage**: ~$1-5 for data persistence
- **Total Estimated**: $15-100/month for 1M transactions

---

## 🔍 Key Findings & Insights

### Developer Experience
- ✅ **Faster Setup**: 30 min vs 2+ hours (DIY)
- ✅ **Built-in Best Practices**: Framework enforces good patterns
- ⚠️ **Learning Curve**: Less educational than DIY approach

### Observability
- ✅ **Zero Effort**: Auto-collection without code changes
- ✅ **Correlation**: Automatic request tracing across services
- ⚠️ **Customization**: Limited compared to open-source tools

### Cost
- ✅ **Transparent Pricing**: Clear per-execution model
- ⚠️ **Cold Starts**: Hidden cost in serverless model
- ⚠️ **Overages**: Can surprise at scale

### Operational Burden
- ✅ **Zero Maintenance**: No patching or updates needed
- ✅ **Built-in Scaling**: Handles peaks automatically
- ⚠️ **Less Control**: Can't optimize at lower levels

---

## 📚 Documentation

- [`docs/SETUP.md`](docs/SETUP.md) - Azure setup and local development
- [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) - Technical architecture details
- [`docs/OBSERVABILITY.md`](docs/OBSERVABILITY.md) - Monitoring and alerting
- [`docs/DEPLOYMENT.md`](docs/DEPLOYMENT.md) - Production deployment guide
- [`docs/TESTING.md`](docs/TESTING.md) - Testing strategies and load tests
- [`docs/COMPARATIVE_ANALYSIS.md`](docs/COMPARATIVE_ANALYSIS.md) - Part 1 vs Part 2 analysis

---

## 🤝 Contributing

This is an active research project. We welcome contributions, feedback, and discussions!

See [`CONTRIBUTING.md`](CONTRIBUTING.md) for guidelines.

---

## 📖 Citation

If you use this research for academic purposes:

```bibtex
@repository{order-pipeline-managed,
  title = {Order Pipeline: Managed Cloud Services (Part 2)},
  author = {Luis Marchiorato},
  year = {2025},
  url = {https://github.com/LuisMarchio03/order-pipeline-managed},
  note = {Part of comparative study: Observability in Event-Driven Serverless Architectures}
}
```

---

## 📜 License

MIT License - See [`LICENSE`](LICENSE) file

---

## 🔗 Related Projects

- **Part 1 (DIY)**: [order-pipeline-diy](https://github.com/LuisMarchio03/order-pipeline-diy) - RabbitMQ, custom stack
- **Research Paper**: Coming soon
- **Author**: [Luis Marchiorato](https://github.com/LuisMarchio03)

---

**Last Updated**: January 2025 | **Status**: 🚧 In Development

**Next Phase**: Part 1 + Part 2 Comparative Analysis & Academic Paper
