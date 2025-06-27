# FormApp Stack Helm Chart

A production-ready Helm chart that deploys a FormApp with PostgreSQL database, powered by KRO (Kubernetes Resource Operator) for advanced orchestration.

## Features

- **KRO-Powered Orchestration**: Uses KRO for sophisticated resource management and reconciliation
- **Helm Package Management**: Leverages Helm for versioning, templating, and release management
- **Auto-scaling**: Built-in HPA configuration for the application
- **Persistent Storage**: Configurable persistent storage for PostgreSQL
- **Pre-install Hooks**: Ensures proper installation order (CRD → RGD → Instance)

## Prerequisites

- Kubernetes 1.19+
- Helm 3.0+
- KRO Controller installed and running in your cluster
- Storage class configured (default: longhorn)

## Installation

```bash
# Add and update the repository (if you have a chart repository)
helm repo add formapp-stack https://your-chart-repo.com
helm repo update

# Install the chart
helm install my-formapp formapp-stack/formapp-stack

# Install with custom values
helm install my-formapp formapp-stack/formapp-stack -f custom-values.yaml

# Install in a specific namespace
helm install my-formapp formapp-stack/formapp-stack --namespace kro-apps --create-namespace