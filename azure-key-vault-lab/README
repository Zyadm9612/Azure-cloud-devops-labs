# Lab 05 – Azure Key Vault

## Overview
This lab demonstrates how to securely store and manage sensitive information using Azure Key Vault. It covers creating a Key Vault, configuring access permissions using Azure RBAC, and storing and retrieving secrets.

## Objectives
- Create an Azure Key Vault.
- Configure Azure RBAC permissions.
- Store sensitive information as Secrets.
- Retrieve secret values securely.
- Understand the role of Managed Identity in secure cloud applications.

## Azure Services Used
- Azure Key Vault
- Azure RBAC (Role-Based Access Control)

## Implementation

### 1. Key Vault Creation
Created an Azure Key Vault with the Standard pricing tier and configured Azure RBAC as the permission model.

### 2. Access Management
Assigned the following role to manage secrets:

- **Key Vault Secrets Officer** – Allows managing secrets within the Key Vault.

### 3. Secret Management
Created a test secret:

| Setting | Value |
|---|---|
| Secret Name | `LabSecret` |
| Secret Value | `AzureLab-Secret-123` |
| Content Type | `Lab secret` |

Retrieved the secret value successfully through the Azure Portal.

### 4. Security Concepts
Explored how Azure Key Vault helps protect sensitive information such as:

- Database credentials
- API keys
- Application secrets
- Connection strings

Learned how applications can use Managed Identity to access secrets without hardcoding credentials.

## Architecture

Application → Managed Identity → Azure Key Vault → Secret

## Skills Learned
- Azure Key Vault
- Secrets Management
- Azure RBAC
- Identity and Access Management
- Managed Identity Concepts
- Cloud Security Best Practices

## Cleanup
Deleted the lab Resource Group after completing the experiment to avoid unnecessary Azure costs.
