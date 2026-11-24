# Project 21: CloudWatch Monitoring Dashboard

## Description

Created an Amazon CloudWatch monitoring dashboard to visualize the performance and health of an existing AWS EC2 instance.

Configured a custom dashboard using AWS CLI and JSON to monitor CPU utilization, incoming network traffic, outgoing network traffic, and EC2 status check failures.

The dashboard provides a centralized view of EC2 performance metrics, making it easier to monitor server health and resource utilization.

## Objectives

- Monitor EC2 instance performance using Amazon CloudWatch.
- Create a custom CloudWatch dashboard using AWS CLI.
- Visualize CPU and network utilization.
- Monitor EC2 instance status checks.
- Verify dashboard configuration through AWS CLI.

## AWS Resources Used

- **Amazon EC2:** Existing EC2 instance used as the monitoring target.
- **Amazon CloudWatch:** Collects and displays EC2 performance metrics.
- **CloudWatch Dashboard:** Displays monitoring metrics through graphical widgets.

## Technologies Used

- AWS
- Amazon EC2
- Amazon CloudWatch
- AWS CLI
- JSON
- Linux / Ubuntu

## EC2 Instance Details

| Property | Value |
|---|---|
| Instance ID | `i-05f77feff5714ab6a` |
| Instance Type | `t3.micro` |
| Region | `ap-south-1` (Mumbai) |
| Monitoring | CloudWatch Basic Monitoring |

## Dashboard Configuration

Created a CloudWatch dashboard named:

`Project21-EC2-Monitoring`

The dashboard contains four monitoring widgets:

| Metric | Description |
|---|---|
| CPUUtilization | Monitors EC2 CPU usage percentage. |
| NetworkIn | Monitors incoming network traffic in bytes. |
| NetworkOut | Monitors outgoing network traffic in bytes. |
| StatusCheckFailed | Monitors EC2 status check failures. |

The dashboard uses a 300-second (5-minute) metric period.

## Implementation Steps

1. Identified an existing running EC2 instance.
2. Verified EC2 CloudWatch metrics using AWS CLI.
3. Checked CPU utilization using the `get-metric-statistics` command.
4. Created a `dashboard.json` configuration file.
5. Defined four CloudWatch metric widgets in the JSON configuration.
6. Created the dashboard using the AWS CLI `put-dashboard` command.
7. Verified dashboard creation using `list-dashboards`.
8. Retrieved the dashboard configuration using `get-dashboard`.
9. Opened the CloudWatch dashboard and verified all four widgets.

## AWS CLI Commands

### 1. Verify EC2 Metrics

```bash
aws cloudwatch list-metrics \
  --namespace AWS/EC2 \
  --dimensions Name=InstanceId,Value=i-05f77feff5714ab6a \
  --region ap-south-1
```

### 2. Check CPU Utilization

```bash
aws cloudwatch get-metric-statistics \
  --namespace AWS/EC2 \
  --metric-name CPUUtilization \
  --dimensions Name=InstanceId,Value=i-05f77feff5714ab6a \
  --start-time "$(date -u -d '1 hour ago' +%Y-%m-%dT%H:%M:%SZ)" \
  --end-time "$(date -u +%Y-%m-%dT%H:%M:%SZ)" \
  --period 300 \
  --statistics Average \
  --region ap-south-1
```

### 3. Create CloudWatch Dashboard

```bash
aws cloudwatch put-dashboard \
  --dashboard-name Project21-EC2-Monitoring \
  --dashboard-body file://dashboard.json \
  --region ap-south-1
```

### 4. Verify Dashboard

```bash
aws cloudwatch list-dashboards \
  --region ap-south-1
```

### 5. Retrieve Dashboard Configuration

```bash
aws cloudwatch get-dashboard \
  --dashboard-name Project21-EC2-Monitoring \
  --region ap-south-1
```

## Project Structure

```text
project-21-cloudwatch-dashboard/
│
├── dashboard.json
├── dashboard-screenshot.png
└── README.md
```

## Dashboard Screenshot

The CloudWatch dashboard contains four widgets displaying:

- EC2 CPU Utilization
- EC2 Network In
- EC2 Network Out
- EC2 Status Check Failed

Screenshot: `dashboard-screenshot.png`

## Outcome

Successfully created and configured a custom Amazon CloudWatch dashboard using AWS CLI.

Verified the dashboard configuration and visualized four EC2 performance and health metrics in a centralized monitoring dashboard.

## Key Learnings

- Understanding Amazon CloudWatch and EC2 monitoring.
- Working with AWS CLI for monitoring automation.
- Creating CloudWatch dashboards using JSON configurations.
- Understanding EC2 performance metrics.
- Retrieving and verifying CloudWatch dashboard configurations.

## AWS Region

`Asia Pacific (Mumbai) – ap-south-1`

---

**GitHub Repository:** [Add your repository URL here]
