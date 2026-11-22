# Azure App Service — Deploying a Python Web Application

## Overview

This lab demonstrates deploying a Python Flask web application to Azure App Service using GitHub Actions for automated deployment.

The objective was to understand the deployment process, configure Azure App Service, connect GitHub to Azure, and explore the fundamentals of CI/CD.

## Architecture

```text
Developer
    |
    | Push code to GitHub
    v
GitHub Repository
    |
    | GitHub Actions Workflow
    v
GitHub Actions Runner
    |
    | Build & Deploy
    v
Azure App Service
    |
    v
Python Flask Web Application
```

## Azure Resources

| Resource | Configuration |
|---|---|
| App Service | `zyad-link-obfuscator-2026` |
| App Service Plan | `asp-link-obfuscator-lab` |
| Resource Group | `rg-azure-Vnet-lab` |
| Region | Canada East |
| Operating System | Linux |
| Runtime Stack | Python 3.12 |
| Pricing Plan | Free (F1) |

## Technologies Used

- Microsoft Azure
- Azure App Service
- Python 3.12
- Flask
- GitHub
- GitHub Actions
- CI/CD
- Linux

## Implementation Steps

### 1. Create Azure App Service

Created an Azure App Service to host the Python web application.

Configured the following:

- Linux operating system
- Python 3.12 runtime
- Free F1 pricing tier
- Canada East region

### 2. Connect GitHub Repository

Connected the application repository to Azure App Service.

Configured GitHub Actions as the deployment provider and selected the `master` branch as the deployment source.

### 3. Configure Deployment Authentication

Downloaded the App Service Publish Profile and configured it as a GitHub Repository Secret:

```text
AZURE_WEBAPP_PUBLISH_PROFILE
```

The secret is used by GitHub Actions to authenticate with Azure during deployment.

### 4. GitHub Actions CI/CD Workflow

Azure generated a GitHub Actions workflow to automate application deployment.

The workflow performs the following steps:

1. Checkout the GitHub repository.
2. Set up Python 3.12.
3. Install application dependencies.
4. Deploy the application to Azure App Service.

Workflow file:

```text
.github/workflows/
```

### 5. Automated Deployment

The workflow is triggered whenever code is pushed to the `master` branch.

Deployment can also be triggered manually using `workflow_dispatch`.

## GitHub Actions Workflow

The workflow uses the following components:

| Component | Purpose |
|---|---|
| `actions/checkout` | Retrieves the source code |
| `actions/setup-python` | Configures Python 3.12 |
| `pip install` | Installs project dependencies |
| `azure/webapps-deploy` | Deploys the application to Azure App Service |

## Configuration

Application configuration and sensitive values should be managed using Azure App Service Environment Variables rather than hardcoded in the source code.

Examples:

```text
SECRET_KEY
DB_HOST
DB_USER
DB_PASSWORD
DB_NAME
```

Sensitive credentials should never be committed to GitHub.

## Troubleshooting

### Publish Profile Download Issue

The Publish Profile download was initially blocked because Basic Authentication was disabled.

Enabled the required authentication setting in Azure App Service to allow downloading the Publish Profile.

### HTTP 503 — Service Unavailable

After deployment, the application returned HTTP 503.

This demonstrated that successful deployment does not necessarily guarantee successful application startup.

Runtime troubleshooting requires checking:

- Azure App Service Log Stream
- Application startup errors
- Python dependencies
- Application configuration
- Environment variables

## Key Learnings

- Understanding Azure App Service and App Service Plans.
- Deploying Python applications to Azure.
- Connecting GitHub repositories to Azure.
- Understanding GitHub Actions workflows.
- Introduction to CI/CD automation.
- Using GitHub Secrets for deployment authentication.
- Differentiating deployment success from application runtime health.
- Troubleshooting application deployment issues.


