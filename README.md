# FormApp Stack Helm Chart - Integration Strategy

This repository demonstrates two different approaches for deploying a FormApp with PostgreSQL database using Helm charts, showcasing the evolution from KRO-powered orchestration to purely native Helm implementations.

## Repository Structure

This repository contains two distinct Helm chart implementations:

### 1. KRO-Powered Helm Chart (`formapp-kro-powered-helm/`)
A production-ready Helm chart that leverages KRO (Kubernetes Resource Operator) for advanced orchestration and resource management.

### 2. Purely Native Helm Chart (`formapp-purely-helm-native/`)
A traditional Helm chart implementation that uses only native Kubernetes resources and Helm templating capabilities without external operators.

## Comparison Overview

| Feature | KRO-Powered | Purely Native |
|---------|-------------|---------------|
| **Orchestration** | KRO-based resource management | Native Helm templating |
| **Complexity** | Higher (requires KRO) | Lower (standard Helm) |
| **Reconciliation** | Advanced KRO reconciliation | Standard Kubernetes controllers |
| **Dependencies** | KRO Controller required | No external dependencies |
| **Learning Curve** | Steeper (KRO concepts) | Standard Helm knowledge |

## Common Features

Both implementations provide:
- **FormApp Deployment**: Complete application stack deployment
- **PostgreSQL Database**: Integrated database with persistent storage
- **Auto-scaling**: HPA configuration for the application
- **Persistent Storage**: Configurable storage for PostgreSQL
- **Production-Ready**: Suitable for production environments

## KRO-Powered Implementation

Located in `formapp-kro-powered-helm/`

### Features
- **KRO-Powered Orchestration**: Uses KRO for sophisticated resource management and reconciliation
- **Helm Package Management**: Leverages Helm for versioning, templating, and release management
- **Advanced Reconciliation**: KRO handles complex dependency management
- **Pre-install Hooks**: Ensures proper installation order (CRD → RGD → Instance)

### Prerequisites
- Kubernetes 1.19+
- Helm 3.0+
- KRO Controller installed and running in your cluster
- Storage class configured (default: longhorn)

## Purely Native Implementation

Located in `formapp-purely-helm-native/`

### Features
- **Native Helm Templates**: Uses standard Helm templating without external operators
- **Standard Kubernetes Resources**: Deployments, Services, ConfigMaps, Secrets
- **Simplified Dependencies**: No operator dependencies
- **Traditional Helm Patterns**: Follows conventional Helm chart structure

### Prerequisites
- Kubernetes 1.19+
- Helm 3.0+
- Storage class configured (default: longhorn)

## Installation

### KRO-Powered Version
```bash
# Install the KRO-powered version
helm install my-formapp ./formapp-kro-powered-helm

# Install with custom values
helm install my-formapp ./formapp-kro-powered-helm -f custom-values.yaml

# Install in a specific namespace
helm install my-formapp ./formapp-kro-powered-helm --namespace kro-apps --create-namespace
```

### Purely Native Version
```bash
# Install the purely native version
helm install my-formapp ./formapp-purely-helm-native

# Install with custom values
helm install my-formapp ./formapp-purely-helm-native -f custom-values.yaml

# Install in a specific namespace
helm install my-formapp ./formapp-purely-helm-native --namespace formapp --create-namespace
```

## Configuration

Both charts support similar configuration options through `values.yaml`:

```yaml
# Common configuration options
app:
  name: formapp
  replicas: 3
  image:
    repository: formapp
    tag: latest

database:
  storage: 10Gi
  storageClass: longhorn

ingress:
  enabled: true
  host: formapp.example.com
```

## When to Use Which Implementation

### Choose KRO-Powered When:
- You need advanced resource orchestration
- Your team is comfortable with operator patterns
- You require sophisticated dependency management
- KRO is already part of your infrastructure

### Choose Purely Native When:
- You prefer standard Helm patterns
- You want to minimize external dependencies
- Your team is new to Kubernetes operators
- You need a simpler, more portable solution

## Migration Path

The repository structure allows for easy comparison and migration between approaches:

1. **KRO to Native**: Extract resource definitions from KRO templates to standard Helm templates
2. **Native to KRO**: Wrap existing resources in KRO ResourceGroup definitions

## Contributing

When contributing to this repository:
- Maintain feature parity between both implementations
- Update both chart versions when adding new features
- Document differences in approach and reasoning
- Test both implementations in your changes

## Support

For questions and issues:
- KRO-specific issues: Check KRO documentation and community
- General Helm issues: Refer to Helm documentation
- FormApp-specific issues: Create an issue in this repository
