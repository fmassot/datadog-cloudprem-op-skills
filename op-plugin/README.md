# Observability Pipelines Plugin for Claude Code

A comprehensive skill for deploying and managing Datadog Observability Pipelines across multiple platforms with an API-first approach.

## Overview

This plugin helps users deploy, configure, and operate Datadog Observability Pipelines (OP) - a log processing and routing solution based on the OSS Vector engine. It covers all major deployment platforms and emphasizes using the OP API for pipeline management.

## Features

### Deployment Platforms
- **AWS EC2** - Standalone instances with systemd
- **AWS Fargate** - ECS containerized deployments
- **AWS EKS** - Kubernetes on AWS
- **Azure AKS** - Kubernetes on Azure
- **Google GKE** - Kubernetes on Google Cloud
- **Vanilla Kubernetes** - Self-managed clusters

### API-First Configuration
- Create pipelines programmatically via OP API
- Remote configuration for zero-downtime updates
- Pipeline CRUD operations (Create, Read, Update, Delete)
- Example configurations for common use cases

### DevOps Operations
- **Scaling**: Manual and autoscaling (HPA) configurations
- **Debugging**: Comprehensive troubleshooting guides
- **Monitoring**: Key metrics, health checks, and alerting
- **Upgrades**: Version upgrade procedures per platform

### Pipeline Processing
- Log filtering, sampling, and deduplication
- Sensitive data redaction (PII scrubbing)
- Log parsing and enrichment
- Multi-destination routing (dual-shipping)
- Buffer management and reliability

## Usage

### Invoke the skill

```
/observability-pipelines
```

Or mention it in conversation:
```
Help me deploy Observability Pipelines on EKS
```

### Common workflows

**1. Deploy OP on Kubernetes and create a pipeline:**
```
I need to deploy Observability Pipelines on EKS and create a pipeline that:
- Receives logs via HTTP server
- Filters out debug logs
- Samples 10% of remaining logs
- Sends to both CloudPrem and Datadog
```

**2. Scale OP workers:**
```
My OP deployment is hitting CPU limits. Help me scale it properly.
```

**3. Debug data flow issues:**
```
Logs aren't reaching CloudPrem from my OP pipeline. How do I debug this?
```

**4. Create API-driven pipeline:**
```
Show me how to create an OP pipeline using the API with filtering and PII redaction.
```

## Plugin Structure

```
op-plugin/
├── .claude-plugin/
│   └── plugin.json          # Plugin metadata
├── commands/
│   └── observability-pipelines.md  # Command entry point
├── skills/
│   └── observability-pipelines/
│       └── SKILL.md         # Main skill content (comprehensive guide)
├── plugin.yaml              # Plugin configuration
└── README.md               # This file
```

## Key Sections in the Skill

1. **Architecture**: OP components, sizing, and throughput calculations
2. **API Configuration**: Complete API reference with examples
3. **Deployment Guides**: Platform-specific step-by-step instructions
4. **Scaling**: Manual and autoscaling strategies
5. **Debugging**: Common issues and troubleshooting workflows
6. **Monitoring**: Metrics, alerts, and observability
7. **Upgrades**: Version management and updates

## Examples

### Create a CloudPrem pipeline via API

```bash
curl -X POST "https://api.datadoghq.com/api/v2/observability_pipelines/pipelines" \
  -H "DD-API-KEY: ${DD_API_KEY}" \
  -H "DD-APPLICATION-KEY: ${DD_APP_KEY}" \
  -H "Content-Type: application/json" \
  -d '{
    "data": {
      "attributes": {
        "name": "cloudprem-pipeline",
        "is_enabled": true,
        "config": {
          "sources": {
            "http_server": {
              "type": "http_server",
              "address": "0.0.0.0:8282"
            }
          },
          "sinks": {
            "cloudprem": {
              "type": "http",
              "inputs": ["http_server"],
              "uri": "http://cloudprem-indexer:7280/api/v2/datadog"
            }
          }
        }
      }
    }
  }'
```

### Deploy on Kubernetes with Helm

```bash
helm install opw datadog/observability-pipelines-worker \
  -n observability-pipelines \
  --create-namespace \
  --set datadog.apiKey="${DD_API_KEY}" \
  --set datadog.pipelineId="${PIPELINE_ID}" \
  --set datadog.site="datadoghq.com" \
  --set replicaCount=3
```

## Reference Documentation

- [Observability Pipelines Docs](https://docs.datadoghq.com/observability-pipelines/)
- [OP API Reference](https://docs.datadoghq.com/api/latest/observability-pipelines/)
- [CloudPrem + OP Guide](https://docs.datadoghq.com/cloudprem/guides/send_otel_logs_observability_pipelines/)
- [Vector Documentation](https://vector.dev/docs/)

## Author

François Massot (francois.massot@datadoghq.com)
Product Manager - Observability Pipelines @ Datadog

## Version

1.0.0
