# Datadog CloudPrem & Observability Pipelines Skills

Official AI assistant skills for deploying and managing Datadog CloudPrem and Observability Pipelines across cloud platforms.

## Overview

This repository contains two comprehensive AI skills designed to help you deploy, configure, and operate Datadog solutions with AI assistants like Claude Code and Gemini CLI:

### 🔷 CloudPrem Plugin
Deploy and manage Datadog CloudPrem on Kubernetes (AWS EKS, Azure AKS, Google GKE, vanilla K8s). Get expert guidance on deployment, scaling, debugging, monitoring, and upgrades.

### 🔶 Observability Pipelines Plugin
Deploy and manage Datadog Observability Pipelines on AWS EC2, Fargate, EKS, Azure AKS, Google GKE, and Kubernetes. API-first configuration for log processing, routing, filtering, and PII redaction.

## Features

### CloudPrem Plugin
- Kubernetes deployment across all major cloud providers
- Architecture sizing and resource planning
- Scaling strategies (manual and autoscaling)
- Comprehensive debugging workflows
- Monitoring and alerting setup
- Version upgrades and maintenance

### Observability Pipelines Plugin
- Multi-platform deployment (EC2, Fargate, Kubernetes)
- API-driven pipeline configuration
- Log filtering, sampling, and deduplication
- Sensitive data redaction (PII scrubbing)
- Multi-destination routing (dual-shipping to CloudPrem + Datadog)
- Buffer management and reliability
- Comprehensive troubleshooting guides

## Installation

Choose your AI assistant platform:

### Claude Code

1. **Install Claude Code CLI** (if not already installed):
   ```bash
   npm install -g @anthropic-ai/claude-code
   ```

2. **Install the plugins**:
   ```bash
   # Navigate to your Claude plugins directory
   cd ~/.claude/plugins/local

   # Clone this repository
   git clone https://github.com/DataDog/datadog-cloudprem-op-skills

   # Copy plugins to the local plugins directory
   cp -r datadog-cloudprem-op-skills/cloudprem-plugin ./
   cp -r datadog-cloudprem-op-skills/op-plugin ./
   ```

3. **Verify installation**:
   ```bash
   claude
   ```
   Type `/help` and you should see the new skills listed.

For detailed Claude Code installation instructions, see [docs/claude-code-installation.md](docs/claude-code-installation.md)

### Gemini CLI

1. **Install Gemini CLI** (if not already installed):
   ```bash
   # Follow Gemini CLI installation instructions
   # https://github.com/google/gemini-cli
   ```

2. **Install the skills**:
   ```bash
   # Navigate to Gemini skills directory
   cd ~/.gemini/skills

   # Clone this repository
   git clone https://github.com/DataDog/datadog-cloudprem-op-skills

   # The skills should now be available
   ```

For detailed Gemini CLI installation instructions, see [docs/gemini-cli-installation.md](docs/gemini-cli-installation.md)

## Usage

### CloudPrem

**Invoke the skill:**
```
/cloudprem
```

**Or mention it in conversation:**
```
Help me deploy CloudPrem on EKS with 3 indexer replicas
```

**Common workflows:**

1. **Initial deployment:**
   ```
   I need to deploy CloudPrem on AKS for a 1TB/day log volume
   ```

2. **Scale indexers:**
   ```
   My CloudPrem indexers are at 80% CPU. Help me scale them.
   ```

3. **Debug ingestion issues:**
   ```
   Logs aren't being ingested. How do I debug CloudPrem indexers?
   ```

### Observability Pipelines

**Invoke the skill:**
```
/observability-pipelines
```

**Or mention it in conversation:**
```
Help me deploy Observability Pipelines on EKS
```

**Common workflows:**

1. **Deploy and create pipeline:**
   ```
   Deploy OP on EKS and create a pipeline that filters debug logs,
   samples 10%, and sends to both CloudPrem and Datadog
   ```

2. **API-driven configuration:**
   ```
   Show me how to create an OP pipeline via API with PII redaction
   ```

3. **Scale workers:**
   ```
   My OP deployment is hitting CPU limits. Help me scale it.
   ```

4. **Debug routing:**
   ```
   Logs aren't reaching CloudPrem from my OP pipeline. Debug this.
   ```

## Requirements

- Kubernetes cluster (for CloudPrem and OP on K8s)
- AWS/Azure/GCP account (for cloud-specific deployments)
- Datadog account with API and Application keys
- `kubectl`, `helm`, AWS CLI/Azure CLI/gcloud as needed

## Examples

### Deploy CloudPrem on EKS
```
I need to deploy CloudPrem on AWS EKS in us-east-1 for 500GB/day.
Use 3 indexer replicas and enable autoscaling.
```

### Create OP Pipeline with Dual-Shipping
```
Create an OP pipeline that:
- Receives logs via HTTP on port 8282
- Filters out logs with level=debug
- Redacts credit card numbers
- Sends to both CloudPrem indexer and Datadog intake
Use the API to create this pipeline.
```

### Debug CloudPrem Indexer Issues
```
My CloudPrem indexers are showing "429 Too Many Requests" errors.
Help me diagnose and fix this.
```

## Support & Documentation

### Datadog Documentation
- [CloudPrem Documentation](https://docs.datadoghq.com/cloudprem/)
- [Observability Pipelines Documentation](https://docs.datadoghq.com/observability-pipelines/)
- [OP API Reference](https://docs.datadoghq.com/api/latest/observability-pipelines/)
- [CloudPrem + OP Integration Guide](https://docs.datadoghq.com/cloudprem/guides/send_otel_logs_observability_pipelines/)

### Claude Code
- [Claude Code Documentation](https://docs.anthropic.com/claude-code)
- [Claude Code GitHub](https://github.com/anthropics/claude-code)

### Gemini CLI
- [Gemini CLI Documentation](https://github.com/google/gemini-cli)

## Contributing

This repository is maintained by the Datadog CloudPrem and Observability Pipelines team. For issues, questions, or contributions, please open an issue or pull request.

## License

Copyright Datadog, Inc.

## Version

- CloudPrem Plugin: 1.0.0
- Observability Pipelines Plugin: 1.0.0
