# Automated-WordPress-Deployment-on-GCP

![Google Cloud](https://img.shields.io/badge/Google_Cloud-Platform-blue?logo=google-cloud)
![Kubernetes](https://img.shields.io/badge/Container-GKE-blue?logo=kubernetes)

## Project Overview
![GCP](https://github.com/user-attachments/assets/2588c537-4b68-4c05-9b7a-618bc8f0f738)


### Business Context
This project establishes a secure WordPress hosting environment, migrating from traditional infrastructure to Google Cloud Platform (GCP) with proper network isolation and security controls.

### Technical Objectives
- Implement multi-environment network architecture
- Establish secure access patterns
- Deploy managed database services
- Containerize WordPress using GKE
- Enable comprehensive monitoring

## Architecture Design

### Network Topology
```mermaid
graph TD
    A[Internet] --> B[Cloud Load Balancer]
    B --> C[GKE Cluster]
    C --> D[WordPress Pods]
    D --> E[Cloud SQL Proxy]
    E --> F[Cloud SQL Instance]
    G[Bastion Host] --> C
    G --> F
Key Components
Component	Technology Used	Purpose
Virtual Networks	Google VPC	Environment isolation
Database	Cloud SQL (MySQL)	Managed relational database
Compute	GKE (e2-standard-4)	WordPress container orchestration
Access Control	IAM, Bastion Host	Secure administrative access
Implementation Details
1. Network Infrastructure
Development VPC (griffin-dev-vpc)

Subnet: griffin-dev-wp (192.168.16.0/20)

Subnet: griffin-dev-mgmt (192.168.32.0/20)

Production VPC (griffin-prod-vpc)

Subnet: griffin-prod-wp (192.168.48.0/20)

Subnet: griffin-prod-mgmt (192.168.64.0/20)

2. Security Implementation
Bastion Host

Dual NIC configuration

SSH access only

e2-medium machine type

Database Security

Private IP configuration

Application-specific credentials

IAM-based access control

3. Kubernetes Deployment
Cluster Configuration

2 node cluster

e2-standard-4 machine type

VPC-native networking

WordPress Setup

Secrets management for DB credentials

Persistent volume for wp-content

Cloud SQL Proxy sidecar

Operational Considerations
Monitoring
Uptime checks configured

Alert policies established

Logging enabled for all components

Access Management
Least privilege principle applied

Separate service accounts for components

Editor role granted to team members

Project Artifacts
├── infrastructure/
│   ├── vpc/               # Network definitions
│   ├── sql/               # Database configuration
│   └── gke/               # Cluster setup
├── applications/
│   ├── wordpress/         # WordPress manifests
│   └── monitoring/        # Monitoring configs
└── documentation/
    ├── ARCHITECTURE.md    # Design decisions
    └── OPERATIONS.md      # Runbook
Team Structure
Role	Responsibilities
Cloud Architect	Infrastructure design
DevOps Engineer	Implementation & automation
Security Specialist	Access controls & hardening
Lessons Learned
Network Design: Proper CIDR planning prevented IP conflicts

Security: Bastion host reduced attack surface

Cost Control: Right-sizing resources saved 30% costs
