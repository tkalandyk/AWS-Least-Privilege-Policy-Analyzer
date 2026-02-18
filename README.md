
<img width="1536" height="1024" alt="ChatGPT Image Feb 17, 2026, 08_16_46 PM" src="https://github.com/user-attachments/assets/a721a81a-031b-4d73-8644-f9aa2b2862c0" />

# AWS Least Privilege Policy Analyzer

## Overview

The AWS Least Privilege Policy Analyzer is an automated IAM auditing tool designed to help organizations enforce least privilege access across AWS environments.

It scans IAM Users and Roles, identifies excessive permissions, assigns risk scores, and generates audit-ready evidence reports that help security, compliance, and cloud teams quickly understand access risk across an AWS account.

This project demonstrates how GRC engineering can move from manual access reviews and screenshots to automated, repeatable, evidence-driven security controls.

---
## 🎥Click Below to Watch the Demo Video ⬇️

[![Watch the video](https://github.com/user-attachments/assets/REPLACE_WITH_IMAGE_ID)](https://youtu.be/REPLACE_WITH_VIDEO_ID)




## Who This Is For

This tool is designed for:

- GRC Engineers  
- Cloud Security Engineers  
- Security Compliance Teams  
- Internal Audit Teams  
- Cloud Platform Teams  

Especially useful for organizations that must prove access reviews during audits but want to reduce manual effort.

---

## What It Does

The analyzer:

- Scans IAM Users and Roles across an AWS account  
- Reviews attached managed policies and inline policies  
- Detects administrative access and high-risk permissions  
- Flags wildcard permissions and overly broad resource access  
- Assigns quantitative risk scores to identities  
- Generates audit-ready JSON and CSV evidence reports  
- Produces executive-level compliance summaries  

---

## Audit Readiness

This tool supports preparation for common audit and compliance frameworks including:

- SOC 2 (Logical Access Controls – CC6 family)  
- NIST 800-53 (AC-6 Least Privilege)  
- CIS AWS Foundations Benchmark (IAM controls)  

It helps demonstrate:

- Access review processes  
- Least privilege enforcement  
- Detection of over-privileged identities  
- Evidence of continuous monitoring capability  

---

## Business Value & Organizational Impact

### Audit Readiness
Reduces manual IAM review effort by generating evidence-ready reports automatically instead of requiring screenshots or spreadsheets.

### Attack Surface Reduction
Identifies over-privileged identities, shadow admin patterns, and wildcard permission usage that increase breach risk.

### Operational Efficiency
Automates repetitive IAM review work and provides consistent risk scoring across environments.

### Visibility for Leadership
Executive summary output makes it easy for leadership and auditors to understand overall privilege posture.

---

## How Risk Scoring Works (High Level)

The analyzer evaluates:

- Administrative policies (AdministratorAccess, PowerUserAccess, IAMFullAccess)  
- High-risk IAM and privilege escalation actions (e.g., `sts:AssumeRole`, `iam:PutRolePolicy`)  
- Wildcard permissions (`Action: *` or broad service wildcards like `s3:*`)  
- Wildcard resources (`Resource: *`)  

Risk levels:

- **Critical** (score >= 70) – Immediate remediation required  
- **High** (score >= 40) – Significant privilege risk  
- **Medium** (score >= 20) – Poor access hygiene  
- **Low** (score < 20) – Aligned with least privilege  

Note: Risk scoring is intentionally conservative to help teams surface privilege creep early.

---

## Features

- **Automated Risk Scoring**: Assigns a numerical risk score to each identity for fast triage.  
- **Policy Coverage**: Reviews both attached managed policies and inline policies.  
- **Privilege Risk Detection**: Flags admin policy assignments, high-risk actions, and wildcard access.  
- **Role Awareness**: Scans IAM roles (including application roles) so privilege risk isn’t missed.  
- **Multi-Format Reporting**: Produces JSON (automation-friendly) and CSV (auditor-friendly).  
- **Executive Summary**: Generates a simple compliance snapshot for leadership and auditors.

---

## Tech Stack

**Language**  
Python 3.9+

**AWS SDK**  
Boto3 (IAM, STS)

**Logic**  
Custom risk scoring and findings engine

**Outputs**  
- JSON report (detailed evidence)  
- CSV report (summary for auditors / leadership)

---

## Architecture Summary

At a high level, the analyzer:

1. Authenticates using default AWS credentials or a specified AWS CLI profile  
2. Enumerates IAM Users and Roles in the account  
3. Collects attached managed policies and inline policies  
4. Evaluates permissions for admin assignments, risky actions, and wildcard scope  
5. Generates a structured report + summary artifacts (JSON and/or CSV)

Reports are stored locally by default and can be extended to centralized evidence storage.

---

## Installation

### Requirements

- Python 3.9+  
- AWS CLI configured  
- IAM read permissions (e.g., `iam:List*`, `iam:Get*`)  
- STS access for account identification (`sts:GetCallerIdentity`)  

---


### Usage
## Basic Run (default AWS credentials)
python privilege_analyzer.py

## Run Against a Specific AWS Profile
python privilege_analyzer.py --profile prod

## Specify Region and Output Format
python privilege_analyzer.py --region us-east-1 --output-format both

## JSON Report (Evidence Pack)

<img width="585" height="625" alt="image" src="https://github.com/user-attachments/assets/8cbb7c13-9adb-45f1-8a38-31aa28631ec0" />


Best for:

Audit evidence retention

Automation pipelines

Ingestion into SIEM / dashboards


## CSV Report (Audit + Leadership Friendly)

<img width="1177" height="548" alt="image" src="https://github.com/user-attachments/assets/3fac96ad-b3f3-4287-9a30-65eba14e9093" />


Best for:

Quick triage

Auditor review

Executive reporting

## Console Summary

<img width="972" height="185" alt="image" src="https://github.com/user-attachments/assets/b96464f3-5faa-4428-ad91-241a2dc6e3a6" />


## Current Scope

Today, this project supports:

- Single AWS account analysis  
- IAM Users and Roles privilege evaluation  
- Attached managed policies and inline policies evaluation  
- Group membership visibility (group policy evaluation can be added)  
- Local evidence artifact generation (JSON/CSV)  

---

## Audit Readiness Notes (How This Helps in Practice)

This tool helps teams demonstrate that access is being reviewed and least privilege is being enforced, which supports:

- SOC 2: logical access controls and review evidence  
- NIST 800-53: least privilege (AC-6) and access governance practices  
- CIS AWS Foundations: IAM hygiene and access scope controls  

In an audit context, the reports can serve as supporting evidence that:

- IAM entities are inventoried  
- privilege risk is evaluated consistently  
- exceptions can be tracked and remediated over time  

---

## Future Enhancements

Planned upgrades that move this from “audit-ready lab” to “enterprise-ready control”:

### Multi-Account / AWS Organizations Support
Centralized least privilege visibility across multiple AWS accounts.

### Group Policy Evaluation
Evaluate group-attached policies and group-level privilege inheritance.

### CloudTrail Usage Analysis
Compare assigned permissions vs. actually used permissions to recommend scoped-down policies (true least privilege).

### S3 Evidence Storage
Automatically upload reports to S3 (with versioning) for centralized evidence retention.

### Drift Tracking
Diff scan results over time to detect privilege creep and highlight changes.

### ChatOps Notifications
Send summaries to Slack/Teams when high-risk privileges appear.

### Optional Auto-Remediation
Support a `--fix` mode to remove high-risk access behind an approval gate.

### Visual Relationship Mapping
Graph identity → policy → trust relationships for faster review and investigation.

---

## Why This Project Matters

Many teams still rely on manual IAM reviews, screenshots, and spreadsheets to prove compliance.

This project shows how GRC engineering can automate access governance in AWS, produce repeatable evidence artifacts, and surface risk in a way that both technical teams and auditors can act on.






