# Claude Code Installation Guide

This guide provides detailed instructions for installing the Datadog CloudPrem and Observability Pipelines skills in Claude Code.

## Prerequisites

- Node.js 18+ and npm installed
- Access to terminal/command line
- Datadog API and Application keys (for using the skills)

## Step 1: Install Claude Code

If you haven't already installed Claude Code:

```bash
npm install -g @anthropic-ai/claude-code
```

Verify installation:
```bash
claude --version
```

## Step 2: Set Up Anthropic API Key

You'll need an Anthropic API key to use Claude Code:

1. Get your API key from [console.anthropic.com](https://console.anthropic.com/)
2. Set it as an environment variable:

```bash
# Add to your ~/.bashrc, ~/.zshrc, or equivalent
export ANTHROPIC_API_KEY="your-api-key-here"
```

3. Reload your shell or run:
```bash
source ~/.bashrc  # or ~/.zshrc
```

## Step 3: Install the Datadog Skills

### Method 1: Direct Git Clone (Recommended)

```bash
# Navigate to Claude's local plugins directory
cd ~/.claude/plugins/local

# Clone the repository
git clone https://github.com/DataDog/datadog-cloudprem-op-skills

# Copy the plugins to the local directory
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
cp -r /path/to/extracted/cloudprem-plugin ~/.claude/plugins/local/
cp -r /path/to/extracted/op-plugin ~/.claude/plugins/local/
```

### Method 3: Symlink (For Development)

If you want to keep the plugins synced with the git repository:

```bash
cd ~/.claude/plugins/local
git clone https://github.com/DataDog/datadog-cloudprem-op-skills
ln -s datadog-cloudprem-op-skills/cloudprem-plugin ./cloudprem-plugin
ln -s datadog-cloudprem-op-skills/op-plugin ./op-plugin
```

## Step 4: Verify Installation

Start Claude Code:
```bash
claude
```

Check available skills by typing:
```
/help
```

You should see both skills listed:
- `cloudprem` - Deploy and manage Datadog CloudPrem on Kubernetes
- `observability-pipelines` - Deploy and manage Datadog Observability Pipelines

## Step 5: Test the Skills

Try invoking a skill:
```
/cloudprem
```

Or use natural language:
```
Help me understand how to deploy CloudPrem on EKS
```

## Directory Structure

After installation, your directory structure should look like:

```
~/.claude/
└── plugins/
    └── local/
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
cd ~/.claude/plugins/local

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
cd ~/.claude/plugins/local/datadog-cloudprem-op-skills
git pull origin main
```

## Troubleshooting

### Skills Not Appearing

1. **Check plugin directory exists:**
   ```bash
   ls -la ~/.claude/plugins/local/
   ```

2. **Verify plugin.json files:**
   ```bash
   cat ~/.claude/plugins/local/cloudprem-plugin/.claude-plugin/plugin.json
   cat ~/.claude/plugins/local/op-plugin/.claude-plugin/plugin.json
   ```

3. **Restart Claude Code:**
   Exit and restart the Claude CLI

### Permission Issues

If you encounter permission errors:
```bash
chmod -R 755 ~/.claude/plugins/local/cloudprem-plugin
chmod -R 755 ~/.claude/plugins/local/op-plugin
```

### Skills Not Working

1. **Verify your Anthropic API key is set:**
   ```bash
   echo $ANTHROPIC_API_KEY
   ```

2. **Check Claude Code logs:**
   ```bash
   # Logs are typically in ~/.claude/logs/
   tail -f ~/.claude/logs/latest.log
   ```

3. **Reinstall the skills:**
   Follow the installation steps again

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

# GCP
gcloud auth login
```

## Best Practices

1. **Keep skills updated:** Check for updates regularly
2. **Use descriptive prompts:** Give Claude clear context about your deployment
3. **Review generated commands:** Always review kubectl/helm commands before executing
4. **Save configurations:** Keep generated YAML files in version control
5. **Use skill memory:** Claude can remember context across your session

## Additional Resources

- [Claude Code Documentation](https://docs.anthropic.com/claude-code)
- [Claude Code GitHub Repository](https://github.com/anthropics/claude-code)
- [Datadog CloudPrem Docs](https://docs.datadoghq.com/cloudprem/)
- [Datadog Observability Pipelines Docs](https://docs.datadoghq.com/observability-pipelines/)

## Support

For issues with:
- **Claude Code itself:** [GitHub Issues](https://github.com/anthropics/claude-code/issues)
- **These skills:** [GitHub Issues](https://github.com/DataDog/datadog-cloudprem-op-skills/issues)
- **Datadog products:** [Datadog Support](https://help.datadoghq.com/)
