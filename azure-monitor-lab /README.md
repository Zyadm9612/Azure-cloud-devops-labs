# Lab 04 – Azure Monitor

## Overview
This lab demonstrates how to monitor Azure resources using Azure Monitor, visualize metrics, and configure metric alerts to detect unusual activity.

## Objectives
- Create an Azure Storage Account.
- Monitor storage transactions using Azure Monitor Metrics.
- Create a Metric Alert Rule.
- Configure an Action Group for notifications.
- Trigger and verify an alert.

## Architecture
- **Azure Storage Account** – Resource being monitored.
- **Azure Monitor Metrics** – Collects and visualizes transaction metrics.
- **Metric Alert Rule** – Detects when transactions exceed the configured threshold.
- **Action Group** – Defines notification actions when the alert is triggered.

## Implementation

### 1. Storage Account
Created an Azure Storage Account and generated transactions by uploading and deleting files.

### 2. Azure Monitor Metrics
Configured a metrics chart to monitor:
- Metric: Transactions
- Aggregation: Sum
- Time range: Last hour

### 3. Metric Alert
Created an alert rule with the following configuration:

| Setting | Value |
|---|---|
| Alert Name | `alert-storage-transactions` |
| Metric | Transactions |
| Threshold | 2 |
| Severity | 3 – Informational |
| Evaluation Frequency | 1 Minute |
| Lookback Period | 5 Minutes |

### 4. Action Group
Created an Action Group to configure notifications when the alert is triggered.

### 5. Alert Testing
Generated additional storage transactions to test the alert rule.

The alert successfully fired when transactions reached **295**, exceeding the configured threshold of **2**.

## Result
Successfully configured Azure Monitor to track Storage Account transactions and detect threshold violations through metric alerts.

## Skills Learned
- Azure Monitor
- Azure Metrics
- Metric Alert Rules
- Action Groups
- Azure Storage Monitoring
- Cloud Monitoring and Alerting

## Cleanup
Deleted the lab Resource Group after completing the experiment to avoid unnecessary Azure costs.
