---
title: "[WIP] DevOps Learning Path"
pubDate: "2025-10-09"
description: "A comprehensive learning path for DevOps with practical projects, time estimates, and clear milestones. This is my ongoing list which I will update as I progress in this learning path."
tags: ["DevOps","learning", "path"]
---
**Imporrtant Note**: This page is an on going work in progress, and changes every few weeks. If you see any issues, or have suggestions feel free to contact me.

<style>
  table {
    border-collapse: collapse; 
    width: 100%;
  }
  th, td {
    border: 1px solid black; 
    padding: 8px; 
    text-align: left;
  }
  th {
    background-color: #f2f2f2; 
  }
</style>

## Table of Contents

| Phase | Key Areas | Est. Time | Difficulty | Jump to |
|-------|-----------|-----------|------------|---------|
| **Phase 1** | Linux, Programming, Git, Networking, Cloud Fundamentals | 2-3 months | Beginner to Intermediate | [Go to Phase 1](#phase-1-core-refresh--cloud-infrastructure) |
| **Phase 2** | Docker, IaC (Terraform), Secrets, CI/CD | 3-4 months | Novice to Advanced | [Go to Phase 2](#phase-2-core-devops-tools-cicd--automation) |
| **Phase 3** | Kubernetes, GitOps, Observability, API Management | 4-5 months | Advanced | [Go to Phase 3](#phase-3-more-containers--orchestration) |
| **Phase 4** | SRE, Troubleshooting, Security, Chaos Engineering | 6+ months | Advanced to Expert | [Go to Phase 4](#phase-4-sre-mindset-advanced-ops-and-specialization) |

---

## Phase 1: Core Refresh & Cloud Infrastructure
**Time Estimate:** 2-3 months | **Difficulty:** Beginner to Intermediate


---

### 1. Operating System (Linux) and Terminal
**Time:** 3-4 weeks (60-80 hours) | **Difficulty:** Novice

**Key Areas:** Permissions, services, logging, systemd, bash scripting, Vim, Nano

**Learn at:**
- [LinuxCommand.org](http://linuxcommand.org/)
- [Introduction to Linux (LFS101)](https://training.linuxfoundation.org/training/introduction-to-linux/)
- [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)
- [Linux Foundation Certified Systems Administrator - LFCS](https://www.udemy.com/course/linux-foundation-certified-systems-administrator-lfcs/?couponCode=NVD20PMUS) 
- [Ubuntu linux professional certificate by canonical](https://www.linkedin.com/learning/paths/ubuntu-linux-professional-certificate-by-canonical)

**Certifications:**
- [Linux Foundation Certified IT Associate (LFCA)](https://training.linuxfoundation.org/certification/certified-it-associate/) - Beginner level
- [CompTIA Linux+](https://www.comptia.org/en-us/certifications/linux/) - Entry to mid level

**You should be able to:**
- Navigate the filesystem (`cd`, `ls`, `pwd`, `find`)
- Use file operations (`cp`, `mv`, `rm`, `cat`, `less`, `head`, `tail`)
- Edit files with `nano` or `vim`
- Manage users and permissions (`chmod`, `chown`, `groups`, `useradd`)
- Use process tools (`ps`, `top`, `kill`, `htop`)
- Work with services (`systemctl`, `service`)
- Use package managers (`apt`, `yum`, or `dnf`)
- Read and understand basic log files in `/var/log/`
- Write simple bash scripts with conditionals and loops
- Understand basic systemd concepts and cron jobs

**Milestone Project:** Set up a Linux server, configure users, install services, and write automation scripts

---

### 2. Learning a Programming Language
**Time:** 4-6 weeks (80-120 hours) | **Difficulty:** Novice

**Key Areas:** Python, Go
- **Learn at:**
  - [python.org](https://docs.python.org/3/tutorial/index.html)
  - [A Tour of Go](https://go.dev/tour/welcome/1)
  - [Learning Go (on linkedin)](https://www.linkedin.com/learning/learning-go-24516285/learn-to-program-with-go)
- **You should at minimum be able to:**
  - Write basic scripts/functions
  - Understand data structures and control flow
  - Use libraries for automation or REST API calls
  - For Go, write simple programs with concurrency concepts

**Milestone Project:** Build a CLI tool that automates a common DevOps task (file processing, API calls, system monitoring)

---

### 3. Version Control (Git)
**Time:** 2-3 weeks (40-60 hours) | **Difficulty:** Beginner

**Key Areas:** Git workflows, branching strategies, collaboration
- **Learn at:**
  - [Git Documentation](https://git-scm.com/doc)
  - [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)
  - [GitHub Learning Lab](https://lab.github.com/)
- **You should at minimum be able to:**
  - Use basic Git commands (clone, add, commit, push, pull)
  - Create and merge branches
  - Resolve merge conflicts
  - Use GitHub/GitLab for collaboration (PRs, issues, reviews)
  - Understand Git workflows (GitFlow, GitHub Flow)

**Milestone Project:** Contribute to an open-source project or create a portfolio repository with proper branching strategy

---

### 4. Networking Fundamentals
**Time:** 2-3 weeks (40-60 hours) | **Difficulty:** Novice

**Key Areas:** TCP/IP, DNS, load balancing, firewalls, cloud networking
- **Learn at:**
  - [Computer Networks Course](https://www.coursera.org/learn/computer-networking)
  - [AWS Networking Fundamentals](https://aws.amazon.com/training/learning-paths/networking/)
  - [Google Cloud Networking](https://cloud.google.com/learn/what-is-cloud-networking)
- **You should at minimum be able to:**
  - Understand TCP/IP stack and common protocols
  - Configure DNS and understand domain resolution
  - Set up basic firewall rules and security groups
  - Understand load balancing concepts
  - Configure VPCs, subnets, and routing in cloud platforms

**Milestone Project:** Set up a multi-tier network with load balancers, configure DNS, and implement security groups

---

### 5. Cloud Fundamentals
**Time:** 4-6 weeks (80-120 hours) | **Difficulty:** Novice

- Ideally you should have a good understanding of a cloud provider. It really doesn't matter between the large providers, as their market share isn't too drastic. My recommendation is AWS. 

#### A. General Cloud Infrastructure
- **Learn at:**
  - [Introduction to Cloud Infrastructure Technologies (LFS151)](https://training.linuxfoundation.org/training/introduction-to-cloud-infrastructure-technologies/)

#### B. AWS Fundamentals (Recommended)
**Key Areas:** IAM, VPC, EC2, S3, CloudWatch, Lambda, CLI, CloudFormation or Terraform  
- **Learn at:**
  - [AWS Skill Builder](https://skillbuilder.aws/)
  - [Stephane Maarek's Ultimate AWS Certified Solutions Architect Associate 2025](https://www.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/?couponCode=MT300725A)
- **Certs:** AWS Cloud Practitioner (optional), AWS SAA (core), AWS DevOps Pro (later)
**You should at minimum be able to:**  
    - Navigate AWS Management Console and AWS CLI  
    - Create/manage IAM users, groups, roles with least privilege  
    - Launch, SSH into, and manage EC2 instances  
    - Create and configure S3 buckets with policies  
    - Understand and configure VPC components: subnets, route tables, security groups, NACLs  
    - Use CloudWatch for basic monitoring and alarms  
    - Run simple Lambda functions and understand event triggers  
    - Write and deploy basic infrastructure as code (IaC) via CloudFormation or Terraform  

#### C. GCP Fundamentals (Alternative)
**Key Areas:** IAM, Compute Engine, Cloud Functions, GCS, VPC, Cloud Logging  
- **Learn at:**
  - [Google Cloud Skills Boost](https://www.cloudskillsboost.google/)
  - [GCP Associate Cloud Engineer - Google Cloud Certification](https://www.udemy.com/course/google-cloud-certification-associate-cloud-engineer/)
  - [GCP ACE Google Associate Cloud Engineer Practice Test Exam](https://www.udemy.com/course/latest-gcp-ace-google-associate-cloud-engineer-practice-exams-tests)
  - [Associate Cloud Engineer](https://cloud.google.com/learn/certification/cloud-engineer)
- **Certs:** 
    - [Google](https://cloud.google.com/learn/certification?hl=en#why-get-google-cloud-certified)
      - See Associate certification
      - Professional certification 
**You should at minimum be able to:**  
    - Navigate Google Cloud Console and gcloud CLI  
    - Manage IAM roles and permissions  
    - Launch and SSH into Compute Engine VMs  
    - Create and configure Google Cloud Storage buckets  
    - Understand GCP networking basics (VPCs, firewall rules)  
    - Use Cloud Logging for monitoring and troubleshooting  
    - Deploy simple Cloud Functions 

**Milestone Project:** Deploy a full-stack application to the cloud with proper networking, security, and monitoring

---

### 6. CLI Practice & Scripting
**Time:** 2-3 weeks (40-60 hours) | **Difficulty:** Novice

**Key Areas:** Bash, pipes, grep/awk/sed, cron, jq, aws/gcloud CLI  
- **Learn at:**
  - [ExplainShell](https://explainshell.com/)
  - [Linux Shell Tips](https://linuxshelltips.com/category/bash/)
  - Bash
- **You should at minimum be able to:**  
    - Use Unix shell utilities and piping to manipulate text and files  
    - Write bash scripts automating common tasks  
    - Schedule jobs with cron  
    - Use `jq` for JSON parsing and filtering in CLI workflows  
    - Use AWS CLI and gcloud CLI for routine cloud tasks 

**Milestone Project:** Create a comprehensive automation script that manages cloud resources

---

### 7. Database Management
**Time:** 2-3 weeks (Est hours: 40-60) 
**Difficulty:** Novice

**Key Areas:** SQL basics, database migrations, backup/restore, NoSQL options
- **Learn at:**
  - [SQL Tutorial](https://www.w3schools.com/sql/)
  - [PostgreSQL Documentation](https://www.postgresql.org/docs/)
  - [MongoDB University](https://university.mongodb.com/)
- **You should at minimum be able to:**
  - Write basic SQL queries (SELECT, INSERT, UPDATE, DELETE)
  - Design simple database schemas
  - Perform database backups and restores
  - Understand database migrations and versioning
  - Use NoSQL databases (Redis, MongoDB) for caching and document storage

**Milestone Project:** Set up a database cluster with backup/restore procedures and monitoring.

---

## Phase 1 Completion

### Phase 1 Checkpoint - Build a simple web app, deploy to cloud, set up monitoring
- Can you deploy a full-stack application to the cloud with proper networking, security, monitoring, and database management?

### Phase 1 Project
- Build and deploy a complete web application to the cloud with a database, proper networking, security groups, and monitoring. 
- The application should demonstrate your understanding of Linux administration, programming, Git workflows, networking concepts, and cloud fundamentals.

**Project Deliverables:**
- Working web application deployed to cloud
- Database integration with proper security
- Network configuration with load balancers
- Monitoring and logging setup
- Git repository with proper branching
- Automation scripts for deployment

---

## Phase 2: Core DevOps Tools, CI/CD & Automation
**Time Estimate:** 3-4 months 
**Difficulty:** Novice to Advanced

### 1. Docker
**Time:** 3-4 weeks (60-80 hours) | **Difficulty:** Novice

**Key Areas:** Dockerfile, volumes, multi-stage builds, networking  
- **Learn at:**
  - [Docker Docs](https://docs.docker.com/get-started/)
  - [Linkedin Learning](https://www.linkedin.com/learning/paths/docker-foundations-professional-certificate)
  - [Docker Deep Dive](https://www.udemy.com/course/docker-deep-dive-zero-to-docker-certified-associate/)
- **Certs:** 
    - [Docker Certified Associate](https://training.mirantis.com/certification/dca-certification-exam/)
- **You should at minimum be able to:**  
    - Write Dockerfiles to containerize applications  
    - Build and run Docker containers locally  
    - Use Docker volumes for persistent storage  
    - Implement multi-stage builds to optimize image size  
    - Configure container networking basics  

**Milestone Project:** Containerize a full-stack application with multi-stage builds and proper networking

---

### 2. Infrastructure as Code (IaC) with Terraform
**Time:** 4-5 weeks (80-100 hours) | **Difficulty:** Intermediate

**Key Areas:** Providers, resources, variables, modules, state, backends  
- **Learn at:**
  - [Terraform Learn Portal](https://developer.hashicorp.com/terraform/learn)
- **Certs:** 
  - [Terraform Associate](https://developer.hashicorp.com/certifications/infrastructure-automation)
- **You should at minimum be able to:**  
    - Write Terraform configurations for common resources (VMs, networking, storage)  
    - Use variables and outputs effectively  
    - Initialize, plan, apply, and destroy Terraform infrastructure  
    - Understand state files and how to manage them (local and remote backends)  
    - Organize code into modules for reuse and clarity  
    
**Milestone Project:** Create a complete infrastructure setup using Terraform with modules and remote state

---

### 3. Secrets Management
**Time:** 1-2 weeks (20-40 hours) | **Difficulty:** Novice

**Tools:** AWS Secrets Manager, Vault, GitHub secrets  
- Securely store/rotate secrets and inject into CI/CD
- **You should at minimum be able to:**  
    - Store secrets securely outside code repositories  
    - Inject secrets into pipelines and runtime environments securely  
    - Rotate and audit secrets regularly

**Milestone Project:** Implement a complete secrets management strategy for your infrastructure

---

### 4. CI/CD Concepts & Tools
**Time:** 4-6 weeks (80-120 hours) | **Difficulty:** Advanced

**Key Areas:** Writing Jenkinsfiles, GitHub workflows, automating tests, builds, and artifact management.
 
- **Learn at:**
  - [GitHub Actions Docs](https://docs.github.com/en/actions)
  - [Jenkins Book](https://www.jenkins.io/doc/book/)
  - [Jenkins Official website](https://www.jenkins.io/doc/tutorials/)
  - [Learn DevOps: CI/CD with Jenkins using Pipelines and Docker](https://www.udemy.com/course/learn-devops-ci-cd-with-jenkins-using-pipelines-and-docker)
  - [GitHub Actions](https://docs.github.com/en/actions)
- **Certs:**
  - Register For Jenkins Exam on [Cloud Bees](https://university.cloudbees.com/)
- **You should at minimum be able to:**  
    - Explain the purpose and flow of CI/CD pipelines  
    - Configure webhooks to trigger pipelines  
    - Understand build, test, deploy stages and artifact management  
    - Use secrets securely in pipelines  
    - Implement approval gates and manual interventions  
    - Write basic Jenkins files and GitHub Actions workflows  
    - Automate running tests, builds, and artifact uploads  
    - Integrate Docker builds into pipelines  
    - Use pipeline environment variables and secrets  

**Milestone Project:** Build a complete CI/CD pipeline that automatically tests, builds, and deploys your application

---

## Phase 2 Completion

### Phase 2 Checkpoint - Build, test, and deploy with containers and automation
- Can you build, test, and deploy applications using containers, infrastructure as code, and automated pipelines?

### Phase 2 Project
- Create a complete DevOps pipeline that automatically builds, tests, and deploys a containerized application using Docker, Terraform for infrastructure, and CI/CD tools.
- The pipeline should include proper secrets management and demonstrate your mastery of core DevOps automation practices.

**Project Deliverables:**
- Containerized application with Docker
- Infrastructure defined with Terraform
- Automated CI/CD pipeline
- Secure secrets management
- Automated testing and deployment

---

## Phase 3: More Containers & Orchestration
**Time Estimate:** 4-5 months 
**Difficulty:** Advanced

### 1. Kubernetes
**Time:** 6-8 weeks (120-160 hours) | **Difficulty:** Advanced

**Key Areas:** Pods, Deployments, Services, ConfigMaps, Ingress  
- **Learn at:**
  - [Kubernetes Docs](https://kubernetes.io/docs/)
  - [Introduction to Kubernetes (LFS158)](https://training.linuxfoundation.org/training/introduction-to-kubernetes/)
- **Certs:**
  - [Certified Kubernetes Administrator (CKA)](https://training.linuxfoundation.org/certification/certified-kubernetes-administrator-cka/)
  - [Certified Kubernetes Security Specialist (CKS)](https://training.linuxfoundation.org/certification/certified-kubernetes-security-specialist/)
  - Advanced cert to set you apart
- **You should at minimum be able to:**  
  - Understand core Kubernetes architecture components  
  - Deploy applications using kubectl and YAML manifests  
  - Manage pods, deployments, and services  
  - Use ConfigMaps and Secrets for configuration management  
  - Configure Ingress controllers to expose services externally 

**Milestone Project:** Deploy a microservices application to Kubernetes with proper networking, storage, and configuration management

---

### 2. GitOps
**Time:** 2-3 weeks (40-60 hours) | **Difficulty:** Advanced

**Key Areas:** ArgoCD, Flux, declarative deployment patterns
- **Learn at:**
  - [ArgoCD Documentation](https://argo-cd.readthedocs.io/)
  - [Flux Documentation](https://fluxcd.io/docs/)
- **You should at minimum be able to:**
  - Set up GitOps workflows with ArgoCD or Flux
  - Implement declarative deployment patterns
  - Manage application deployments through Git

**Milestone Project:** Implement a complete GitOps workflow for your Kubernetes applications

---

### 3. Helm & Observability
**Time:** 3-4 weeks (60-80 hours) | **Difficulty:** Advanced

**Tools:** Helm, Prometheus, Grafana  
- Templating, dashboards, alerts, metrics
- **You should at minimum be able to:**  
    - Use Helm to package and deploy Kubernetes applications  
    - Install and configure Prometheus for metrics collection  
    - Create Grafana dashboards for visualizing metrics  
    - Set up alerts based on key performance indicators  

**Milestone Project:** Set up a complete observability stack with monitoring, alerting, and dashboards

---

### 4. API Management
**Time:** 2-3 weeks (40-60 hours) | **Difficulty:** Intermediate

**Key Areas:** REST/GraphQL, API gateways, rate limiting
- **Learn at:**
  - [API Design Best Practices](https://docs.microsoft.com/en-us/azure/architecture/best-practices/api-design)
- **You should at minimum be able to:**
  - Design RESTful APIs and understand GraphQL basics
  - Configure API gateways and rate limiting
  - Implement API versioning and documentation

**Milestone Project:** Design and implement a complete API management solution

---

## Phase 3 Completion

### Phase 3 Checkpoint - Orchestrate applications at scale with monitoring
- Can you orchestrate containerized applications at scale with proper monitoring and API management?

### Phase 3 Project
- Deploy a complete microservices architecture to Kubernetes with GitOps workflows, comprehensive monitoring, and API management.
- The project should demonstrate your ability to manage complex distributed systems at scale with proper observability and deployment automation.

**Project Deliverables:**
- Kubernetes microservices deployment
- GitOps workflow implementation
- Comprehensive monitoring and alerting
- API management and gateway configuration
- Scalable distributed system architecture

---

## Phase 4: SRE Mindset, Advanced Ops and Specialization
**Time Estimate:** 6+ months 
**Difficulty:** Advanced to Expert

### 1. Troubleshooting & Debugging
**Time:** 3-4 weeks (60-80 hours) | **Difficulty:** Advanced

**Key Areas:** Log analysis, performance profiling, network debugging
- **Learn at:**
  - [Linux Performance Tools](https://www.brendangregg.com/linuxperf.html)
  - [Debugging Distributed Systems](https://www.oreilly.com/library/view/distributed-systems-observability/9781492033431/)
- **You should at minimum be able to:**
  - Analyze application and system logs effectively
  - Use performance profiling tools (htop, iostat, netstat)
  - Debug network connectivity issues
  - Troubleshoot container and Kubernetes problems
  - Use debugging tools for distributed systems

**Milestone Project:** Create a comprehensive troubleshooting playbook and demonstrate debugging skills

---

### 2. Documentation & Communication
**Time:** 2-3 weeks (40-60 hours) | **Difficulty:** Intermediate

**Key Areas:** Technical writing, runbooks, incident post-mortems
- **Learn at:**
  - [Google Technical Writing Course](https://developers.google.com/tech-writing)
  - [Incident Response Documentation](https://response.pagerduty.com/)
- **You should at minimum be able to:**
  - Write clear technical documentation and runbooks
  - Conduct effective incident post-mortems
  - Create system architecture diagrams
  - Communicate technical concepts to non-technical stakeholders

**Milestone Project:** Create a complete documentation suite for your infrastructure and processes

---

### 3. Monitoring & Logging
**Time:** 4-5 weeks (80-100 hours) | **Difficulty:** Advanced

**Key Areas:** SLIs/SLOs, alerting, log pipelines, incident response  
- **Learn at:**
  - [Google SRE Book](https://sre.google/books/)
  - [Introduction to DevOps and Site Reliability Engineering (LFS162)](https://training.linuxfoundation.org/training/introduction-to-devops-and-site-reliability-engineering-lfs162/)
  - [Getting Started with Prometheus and Grafana](https://grafana.com/docs/grafana/latest/getting-started/get-started-grafana-prometheus/)
  - CloudWatch, Datadog, New Relic
- **You should at minimum be able to:**  
    - Define and measure SLIs and SLOs for services  
    - Configure alerting rules and escalation paths  
    - Set up centralized log aggregation pipelines  
    - Participate in incident response workflows

**Milestone Project:** Implement a complete SRE monitoring and alerting system with SLIs/SLOs

---

### 4. Advanced Infrastructure Automation and Configuration Management
**Time:** 3-4 weeks (60-80 hours) | **Difficulty:** Advanced

**Tools:** Ansible, Chef, Puppet 
**Key Areas:** Configuration Management
- **Learn at:**
  - TBD
- **Certs:**
  - Puppet Certified Professional
  - Red Hat Certified Specialist in Ansible Automation

**Milestone Project:** Automate the configuration of a complete infrastructure stack

---

### 5. Service Mesh & Microservices
**Time:** 3-4 weeks (60-80 hours) | **Difficulty:** Advanced

**Key Areas:** Istio, Linkerd, microservices communication patterns
- **Learn at:**
  - [Istio Documentation](https://istio.io/latest/docs/)
  - [Linkerd Documentation](https://linkerd.io/2.11/overview/)
- **You should at minimum be able to:**
  - Understand service mesh concepts and benefits
  - Deploy and configure Istio or Linkerd
  - Implement traffic management and security policies
  - Monitor microservices communication

**Milestone Project:** Implement a service mesh for a microservices architecture

---

### 6. Security & Cost Optimization
**Time:** 3-4 weeks (60-80 hours) | **Difficulty:** Advanced

**Key Areas:** IAM, MFA, budgets, encryption, tagging  
- **Learn at:**
  - TBD
- **You should at minimum be able to:**  
    - Apply least privilege principles to IAM roles and policies  
    - Enable and enforce MFA for critical accounts  
    - Tag cloud resources for cost allocation and tracking  
    - Use encryption at rest and in transit  
    - Monitor and optimize cloud costs regularly 

**Milestone Project:** Implement a comprehensive security and cost optimization strategy

---

### 7. Chaos Engineering
**Time:** 2-3 weeks (40-60 hours) | **Difficulty:** Expert

**Tools:** LitmusChaos, Gremlin  
- Learn failure injection and resiliency testing
- **Learn at:**
  - TBD
- **You should at minimum be able to:**  
    - Understand principles of failure injection and resiliency testing  
    - Use tools to simulate failures and validate system behavior  
    - Analyze results and improve system fault tolerance

**Milestone Project:** Design and implement a chaos engineering strategy for your systems

---

## Phase 4 Completion

### Phase 4 Checkpoint - Design and maintain reliable, secure systems at scale
- Can you design, implement, and maintain highly reliable, secure, and cost-optimized systems at scale?

### Phase 4 Project
- Design and implement a complete SRE system with comprehensive monitoring, incident response procedures, security hardening, cost optimization, and chaos engineering practices.
- This project should demonstrate your mastery of advanced DevOps and SRE principles at an expert level.

**Project Deliverables:**
- Complete SRE monitoring and alerting system
- Incident response procedures and documentation
- Security hardening and compliance measures
- Cost optimization strategies and implementation
- Chaos engineering testing framework
- Expert-level system design and architecture

## Ongoing Practice & Interview Prep

- Practice explaining:
  - CI/CD pipeline from commit to prod
  - Docker to K8s rollout process
  - Terraform state and modules
- Mock interviews: deployment scenarios, incident response, YAML debugging
- Build a public GitHub repo: pipelines, IaC, dashboards, diagrams

---

## Why This Order?

**Phase 1 (Foundation):** Linux + Programming + Cloud fundamentals create the essential foundation. You need these core skills before automating anything. This phase builds the fundamental knowledge required for all subsequent phases.

**Phase 2 (Core DevOps):** Docker + IaC + CI/CD form the core DevOps workflow. These tools represent the essential automation pipeline that defines modern DevOps practices. You learn to package, provision, and deploy applications systematically.

**Phase 3 (Scale & Orchestration):** Kubernetes + Observability handle production-scale systems. Orchestration and monitoring become critical when moving from single applications to distributed systems. This phase prepares you for real-world production environments.

**Phase 4 (SRE & Specialization):** SRE practices + Advanced certifications differentiate you in the market. This phase focuses on reliability, security, cost optimization, and advanced system design - the skills that separate senior engineers from junior ones.

**Dependencies:** Each phase builds on the previous one. You cannot effectively learn Kubernetes without understanding containers (Phase 2). You cannot implement SRE practices without understanding monitoring and orchestration (Phase 3). The progression ensures you have the necessary context and skills for each subsequent phase.

---

## TODOs: Work to add to this page

### Advanced Improvements (TODO)
- Add missing topics:
  - Security Fundamentals (move earlier)
  - Testing Strategies (unit, integration, e2e)
  - Performance Optimization
  - Disaster Recovery & Backup Strategies
- Create learning paths by role:
  - DevOps Engineer path
  - SRE path  
- Include soft skills:
  - Communication
  - Collaboration
  - Problem-solving
  - Leadership
- Add cost considerations:
  - Free tier limitations
  - Cost effective learning strategies
  - Local alternatives (minikube, kind, etc.)
- Add practical projects for each phase:
  - Phase 1: Build a simple web app, deploy to cloud, set up monitoring
  - Phase 2: Create a full CI/CD pipeline with Docker + Terraform
  - Phase 3: Deploy a microservices app to Kubernetes with observability
  - Phase 4: Build a complete SRE setup with SLIs/SLOs
- Add interview preparation section:
  - Interview questions for each phase
  - Scenario-based questions
  - "Tell me about a time when..." examples
- Add certification strategy:
  - Which certs to prioritize based on career goals
  - Certification timelines and study plans
  - Cost-benefit analysis of each cert
- Role-specific paths (SRE vs DevOps Engineer vs Platform Engineer)
