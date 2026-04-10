---
date: 2026-04-11
type: entity
name: AWS Certified Cloud Practitioner
aliases: [CLF-C02, Cloud Practitioner, AWS CCP]
tags: [certification, aws, cloud, fundamentals]
sources: 0
---

# AWS Certified Cloud Practitioner

**Type:** product/certification
**Also known as:** CLF-C02, AWS CCP, Cloud Practitioner

## Overview

The AWS Certified Cloud Practitioner (CLF-C02) is Amazon Web Services' foundational certification — the entry point to the entire AWS certification track. Like Microsoft's PL-900, it is a breadth exam: it tests conceptual understanding of cloud computing, AWS global infrastructure, core services, security, and pricing, rather than hands-on technical execution.

The target audience is business stakeholders, non-technical project managers, IT professionals starting on AWS, and developers from other clouds building AWS fluency. No CLI commands or architecture design are required. The exam rewards candidates who can describe what each service does, identify the right service for a given scenario, and understand the cost and security model of the cloud.

It is the prerequisite credential before associate-level exams (Solutions Architect, Developer, SysOps Administrator) and a common requirement for teams onboarding to AWS for the first time.

## Skill Domains

The exam (CLF-C02) is organized into four domains:

| Domain | Weight |
|---|---|
| Cloud Concepts | 24% |
| Security and Compliance | 30% |
| Cloud Technology and Services | 34% |
| Billing, Pricing, and Support | 12% |

## Key Conceptual Areas

- **Cloud concepts**: IaaS/PaaS/SaaS distinctions, cloud deployment models (public/private/hybrid), 6 advantages of cloud computing, economies of scale
- **AWS global infrastructure**: Regions, Availability Zones, Edge Locations, Local Zones — what they are and when each matters
- **Shared responsibility model**: AWS responsibility (infrastructure, hardware, physical security) vs. customer responsibility (data, IAM, OS patching, encryption)
- **IAM**: users, groups, roles, policies, MFA, root account best practices, principle of least privilege
- **Core compute**: EC2 (instance types, pricing models: on-demand, reserved, spot, savings plans), Lambda, Elastic Beanstalk, Lightsail, ECS, EKS
- **Core storage**: S3 (storage classes: Standard, IA, Glacier, Intelligent-Tiering), EBS, EFS, Storage Gateway, Snow family
- **Core databases**: RDS, Aurora, DynamoDB, ElastiCache, Redshift — conceptual use cases
- **Networking**: VPC, subnets, security groups vs. NACLs, Route 53, CloudFront, Direct Connect, VPN, API Gateway
- **Security services**: Shield (DDoS), WAF (web app firewall), GuardDuty (threat detection), Inspector (vulnerability scanning), Macie (data sensitivity), Security Hub, KMS, Secrets Manager
- **Management and monitoring**: CloudWatch (metrics/logs/alarms), CloudTrail (API audit), Config (compliance tracking), Trusted Advisor (optimization), Systems Manager
- **Well-Architected Framework**: 6 pillars — Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization, Sustainability
- **Pricing and billing**: pay-as-you-go model, pricing calculator, Cost Explorer, Budgets, Consolidated Billing, AWS Organizations
- **Support plans**: Basic, Developer, Business, Enterprise On-Ramp, Enterprise — response times and key differences
- **Migration and innovation**: Snow family (Snowcone/Snowball/Snowmobile), Migration Hub, CAF (Cloud Adoption Framework)

## Connections

- [[wiki/concepts/ultralearning]] — framework for accelerating exam preparation
- [[wiki/analyses/ultralearning-for-aws-cloud-practitioner]] — full study plan applying ultralearning to this exam
- [[wiki/entities/microsoft-pl900]] — analogous Microsoft fundamentals exam for conceptual comparison
- [[wiki/concepts/shared-responsibility-model]] — security concept already in the wiki; maps directly to AWS's own shared responsibility model

## Open Questions

- How heavily does CLF-C02 test newer services (Bedrock, CodeWhisperer/Q) vs. the classic core?
- Which domain trips up candidates most in practice — Security (highest weight at 30%) or Services (most surface area)?
- Are there reliable third-party question banks that better reflect current exam difficulty than AWS's official sample questions?
