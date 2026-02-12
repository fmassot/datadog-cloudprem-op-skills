# Gemini CLI Installation Guide

This guide provides detailed instructions for installing the Datadog CloudPrem and Observability Pipelines skills in Gemini CLI.

## Prerequisites

- Python 3.8+ installed
- Access to terminal/command line
- Google Cloud account with Gemini API access
- Datadog API and Application keys (for using the skills)

## Step 1: Install Gemini CLI

Install the Gemini CLI tool:

```bash
pip install google-generativeai-cli
```

Or using pipx (recommended for isolation):
```bash
pipx install google-generativeai-cli
```

Verify installation:
```bash
gemini --version
```

## Step 2: Set Up Google API Key

You'll need a Google AI API key to use Gemini:

1. Get your API key from [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Set it as an environment variable:

```bash
# Add to your ~/.bashrc, ~/.zshrc, or equivalent
export GOOGLE_API_KEY="your-api-key-here"
```

3. Reload your shell or run:
```bash
source ~/.bashrc  # or ~/.zshrc
```

## Step 3: Install the Datadog Skills

### Method 1: Direct Git Clone (Recommended)

```bash
# Navigate to Gemini's skills directory
# Note: The exact path may vary based on your Gemini CLI installation
cd ~/.gemini/skills

# Clone the repository
git clone https://github.com/DataDog/datadog-cloudprem-op-skills

# Copy the plugins to the skills directory
cp -r datadog-cloudprem-op-skills/cloudprem-plugin ./
cp -r datadog-cloudprem-op-skills/op-plugin ./

# Optional: Remove the cloned repo to save space
rm -rf datadog-cloudprem-op-skills
```

### Method 2: Manual Download

1. Download the repository as a ZIP from GitHub
2. Extract the archive
3. Copy the plugin directories:
```bash
cp -r /path/to/extracted/cloudprem-plugin ~/.gemini/skills/
cp -r /path/to/extracted/op-plugin ~/.gemini/skills/
```

### Method 3: Symlink (For Development)

If you want to keep the skills synced with the git repository:

```bash
cd ~/.gemini/skills
git clone https://github.com/DataDog/datadog-cloudprem-op-skills
ln -s datadog-cloudprem-op-skills/cloudprem-plugin ./cloudprem-plugin
ln -s datadog-cloudprem-op-skills/op-plugin ./op-plugin
```

## Step 4: Verify Installation

Start Gemini CLI:
```bash
gemini
```

List available skills:
```
/skills list
```

You should see both skills listed:
- `cloudprem-plugin` - Deploy and manage Datadog CloudPrem on Kubernetes
- `op-plugin` - Deploy and manage Datadog Observability Pipelines

## Step 5: Test the Skills

Try using a skill with natural language:
```
Help me deploy CloudPrem on GKE with 3 indexer replicas
```

Or:
```
Show me how to create an Observability Pipelines pipeline via API
```

## Directory Structure

After installation, your directory structure should look like:

```
~/.gemini/
└── skills/
    ├── cloudprem-plugin/
    │   ├── .claude-plugin/
    │   │   └── plugin.json
    │   ├── commands/
    │   │   └── cloudprem.md
    │   └── skills/
    │       └── cloudprem/
    │           └── SKILL.md
    └── op-plugin/
        ├── .claude-plugin/
        │   └── plugin.json
        ├── commands/
        │   └── observability-pipelines.md
        ├── skills/
        │   └── observability-pipelines/
        │       └── SKILL.md
        ├── plugin.yaml
        └── README.md
```

## Updating the Skills

To update to the latest version:

```bash
cd ~/.gemini/skills

# Remove old versions
rm -rf cloudprem-plugin op-plugin

# Clone and install latest
git clone https://github.com/DataDog/datadog-cloudprem-op-skills
cp -r datadog-cloudprem-op-skills/cloudprem-plugin ./
cp -r datadog-cloudprem-op-skills/op-plugin ./
rm -rf datadog-cloudprem-op-skills
```

Or if you used symlinks:
```bash
cd ~/.gemini/skills/datadog-cloudprem-op-skills
git pull origin main
```

## Troubleshooting

### Skills Not Appearing

1. **Check skills directory exists:**
   ```bash
   ls -la ~/.gemini/skills/
   ```

2. **Verify plugin files:**
   ```bash
   cat ~/.gemini/skills/cloudprem-plugin/.claude-plugin/plugin.json
   cat ~/.gemini/skills/op-plugin/.claude-plugin/plugin.json
   ```

3. **Restart Gemini CLI:**
   Exit and restart the CLI

### Permission Issues

If you encounter permission errors:
```bash
chmod -R 755 ~/.gemini/skills/cloudprem-plugin
chmod -R 755 ~/.gemini/skills/op-plugin
```

### Skills Not Working

1. **Verify your Google API key is set:**
   ```bash
   echo $GOOGLE_API_KEY
   ```

2. **Check Gemini CLI configuration:**
   ```bash
   gemini config show
   ```

3. **Reinstall the skills:**
   Follow the installation steps again

### Model Selection

For best results with these comprehensive skills, use the latest Gemini models:

```bash
gemini config set model gemini-2.0-pro
```

Or:
```bash
gemini config set model gemini-1.5-pro
```

## Environment Setup for Datadog

To use these skills effectively, set up your Datadog credentials:

```bash
# Add to ~/.bashrc or ~/.zshrc
export DD_API_KEY="your-datadog-api-key"
export DD_APP_KEY="your-datadog-app-key"
export DD_SITE="datadoghq.com"  # or datadoghq.eu, etc.
```

For cloud provider credentials (AWS, Azure, GCP), ensure those are configured separately:

```bash
# AWS
aws configure

# Azure
az login

# GCP (you may already have this configured for Gemini)
gcloud auth login
```

## Usage Examples

### CloudPrem Deployment

```
I need to deploy CloudPrem on GKE in us-central1 for a 1TB/day log volume.
Use 5 indexer replicas with autoscaling enabled.
```

### Observability Pipelines Configuration

```
Create an OP pipeline that:
- Receives logs via HTTP server
- Filters out debug logs
- Redacts PII (emails, phone numbers)
- Routes to both CloudPrem and Datadog
Show me the API curl commands.
```

### Debugging

```
My CloudPrem indexers are showing high CPU usage and slow query times.
Walk me through debugging this issue.
```

## Best Practices

1. **Keep skills updated:** Check for updates regularly
2. **Use descriptive prompts:** Provide clear context about your deployment requirements
3. **Review generated commands:** Always review kubectl/helm commands before executing
4. **Save configurations:** Keep generated YAML files in version control
5. **Session context:** Gemini can maintain context throughout your session

## Skill Compatibility Notes

These skills were originally designed for Claude Code but are compatible with Gemini CLI. The skills contain comprehensive markdown documentation that Gemini can process effectively. Some differences to note:

- Command invocation syntax may differ (Gemini uses natural language primarily)
- File paths and examples reference both platforms when applicable
- Core functionality and guidance remain the same

## Additional Resources

- [Gemini CLI Documentation](https://github.com/google/generativeai-python)
- [Google AI Studio](https://makersuite.google.com/)
- [Datadog CloudPrem Docs](https://docs.datadoghq.com/cloudprem/)
- [Datadog Observability Pipelines Docs](https://docs.datadoghq.com/observability-pipelines/)

## Support

For issues with:
- **Gemini CLI itself:** [GitHub Issues](https://github.com/google/generativeai-python/issues)
- **These skills:** [GitHub Issues](https://github.com/DataDog/datadog-cloudprem-op-skills/issues)
- **Datadog products:** [Datadog Support](https://help.datadoghq.com/)

## Contributing

If you find ways to improve Gemini CLI compatibility or have suggestions for these skills, please contribute via pull requests or issues on GitHub.
