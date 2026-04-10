---
date: 2026-04-11
type: entity
name: AWS Certified Developer - Associate
aliases: [DVA-C02, AWS Developer Associate, AWS CDA]
tags: [certification, aws, cloud, developer, associate]
sources: 0
---

# AWS Certified Developer - Associate

**Type:** product/certification
**Also known as:** DVA-C02, AWS Developer Associate, AWS CDA

## Overview

The AWS Certified Developer – Associate (DVA-C02) is the developer-track associate certification from AWS. It sits one level above the Cloud Practitioner and targets software developers who build, deploy, debug, and optimize applications on AWS — with an emphasis on serverless architectures, CI/CD pipelines, and application-layer security.

Unlike the Cloud Practitioner (conceptual breadth) or Solutions Architect Associate (infrastructure design), this exam is specifically developer-oriented: it tests how you write code that integrates with AWS services, how you configure those services for application workloads, and how you troubleshoot failures in a running system. Hands-on SDK and CLI fluency is expected.

The exam favors serverless-first thinking. Lambda, API Gateway, DynamoDB, SQS, SNS, and EventBridge are the core stack. The CI/CD toolchain (CodeCommit, CodeBuild, CodeDeploy, CodePipeline) and observability tools (X-Ray, CloudWatch) round out the developer surface area.

## Skill Domains

The exam (DVA-C02) is organized into four domains:

| Domain | Weight |
|---|---|
| Development with AWS Services | 32% |
| Security | 26% |
| Deployment | 24% |
| Troubleshooting and Optimization | 18% |

## Key Technical Areas

- **Lambda**: invocation models (synchronous, asynchronous, event source mapping), execution environment lifecycle (init/invoke/shutdown), layers, reserved vs. provisioned concurrency, destinations, dead-letter queues, error handling, cold starts
- **API Gateway**: REST vs. HTTP vs. WebSocket APIs, integration types (Lambda proxy, AWS service, HTTP), caching, throttling, usage plans, authorization (IAM auth, Cognito User Pools, Lambda authorizer)
- **DynamoDB**: partition key design and hot partition avoidance, GSI vs. LSI, DynamoDB Streams, TTL, transactions (TransactWriteItems), DAX caching, provisioned vs. on-demand capacity, pagination (LastEvaluatedKey), conditional writes
- **S3**: presigned URLs, multipart upload, event notifications, S3 Select, encryption options (SSE-S3, SSE-KMS, SSE-C, client-side), CORS configuration, versioning, lifecycle rules
- **SQS**: standard vs. FIFO queues, visibility timeout, dead-letter queues, long polling vs. short polling, message deduplication, batch operations
- **SNS**: topics, subscriptions, fan-out pattern with SQS, FIFO topics, message filtering policies
- **EventBridge**: event rules, targets, event patterns, scheduled rules (cron), custom event buses
- **Kinesis**: Data Streams (shards, partition keys, GetRecords, enhanced fan-out via subscriptions), Data Firehose (delivery to S3/Redshift/OpenSearch), sequence numbers and checkpointing
- **Elastic Beanstalk**: deployment policies (all-at-once, rolling, rolling with additional batch, immutable, blue/green), .ebextensions configuration files, environment tiers (web vs. worker)
- **CI/CD**: CodeCommit (Git), CodeBuild (buildspec.yml), CodeDeploy (appspec.yml, deployment types: in-place vs. blue/green, hooks), CodePipeline (stages, actions, artifacts), CodeArtifact
- **CloudFormation and SAM**: template anatomy (Resources, Parameters, Mappings, Outputs), stacks, change sets, cross-stack references, SAM (serverless transforms, `sam build`, `sam deploy`)
- **IAM and security**: identity-based vs. resource-based policies, permission boundaries, STS AssumeRole, cross-account access, Cognito User Pools vs. Identity Pools, JWT token validation
- **KMS**: CMK types (AWS-managed, customer-managed, custom key store), envelope encryption pattern, GenerateDataKey, Decrypt, automatic key rotation
- **Secrets Manager vs. SSM Parameter Store**: when to use each (rotation, cost, use case), SecureString in Parameter Store
- **Observability**: X-Ray (segments, subsegments, annotations vs. metadata, sampling rules, service map, groups), CloudWatch (custom metrics, log groups/streams, metric filters, alarms, Logs Insights queries), CloudWatch Embedded Metric Format
- **ElastiCache**: Redis vs. Memcached trade-offs, caching strategies (lazy loading, write-through, cache-aside), TTL management
- **ECS/Fargate**: task definitions, task role vs. execution role, service auto-scaling, placement strategies
- **Step Functions**: state machine types (standard vs. express), task/choice/wait/parallel states, error handling (Catch, Retry), integration with Lambda and other services

## Connections

- [[wiki/concepts/ultralearning]] — framework for accelerating exam preparation
- [[wiki/analyses/ultralearning-for-aws-developer-associate]] — full study plan applying ultralearning to this exam
- [[wiki/entities/aws-certified-cloud-practitioner]] — foundational exam; cloud concepts and service awareness transfer directly
- [[wiki/concepts/shared-responsibility-model]] — security model; developer exam tests the application layer of this boundary
- [[wiki/concepts/agentic-ai]] — Lambda + Step Functions + EventBridge are the building blocks for agentic AI workflows on AWS

## Open Questions

- How heavily does DVA-C02 test Step Functions vs. SQS/SNS for orchestration scenarios?
- Are there significant questions on newer services (Bedrock, CodeWhisperer, Amplify) in the current exam version?
- What is the practical difficulty gap between DVA-C02 and SAA-C03 (Solutions Architect Associate)?
