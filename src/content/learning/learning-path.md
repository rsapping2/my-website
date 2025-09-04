---
title: "[WIP] DevOps Learning Path"
pubDate: "2025-09-02"
description: "A learning path for DevOps. This is my ongoing list which I will update as I progress in this learning path."
tags: ["DevOps","learning", "path"]
---
Note: This page is an on going work in progress. I'll update the last updated tag when I update this page.

#### TODOS: Work to add to this page
- For each section, add projects.
- For each section, tie in interview questions.
- Finish writing out section 4
---

## Phase 1: Core Refresh & Cloud Infrastructure

### 1. Learning a Programming language
**Key Areas:**: Python, Go
- **Learn at:**
  - [python.org](https://docs.python.org/3/tutorial/index.html)
  - [A Tour of Go](https://go.dev/tour/welcome/1)
  - [Learning Go (on linkedin)](https://www.linkedin.com/learning/learning-go-24516285/learn-to-program-with-go)
- **You should at minimum be able to:**
  - Write basic scripts/functions
  - Understand data structures and control flow
  - Use libraries for automation or REST API calls
  - For Go, write simple programs with concurrency concepts


### 2. Operating System (Linux) and Terminal

#### A. Linux / Ubuntu / Debian

**Key Areas:** Permissions, services, logging, systemd, bash scripting, Vim, Nano  
- **Learn at:**
  - [LinuxCommand.org](http://linuxcommand.org/)
  - [Introduction to Linux (LFS101)](https://training.linuxfoundation.org/training/introduction-to-linux/)
  - [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)
  - [Linux Foundation Certified Systems Administrator - LFCS](https://www.udemy.com/course/linux-foundation-certified-systems-administrator-lfcs/?couponCode=NVD20PMUS) 
  - [Ubuntu linux professional certificate by canonical](https://www.linkedin.com/learning/paths/ubuntu-linux-professional-certificate-by-canonical)

- **Certs:** 
    - [Linux Foundation Certified IT Associate (LFCA)](https://training.linuxfoundation.org/certification/certified-it-associate/)
      - This is more of a beginner Cert
    - [CompTIA Linux+](https://www.comptia.org/en-us/certifications/linux/)
      - This is more of a entry to mid level cert.
- **You should at minimum be able to:**
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


### 3. Cloud Fundamentals

- Ideally you should have a good understanding of a cloud provider. It really doesn't matter between the large providers, as their market share isn't too drastic. My recommendation is AWS. 

### A. General Cloud Infrastructure
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

### C. GCP Fundamentals (Alternative)
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

### 4. CLI Practice & Scripting
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

## Phase 2: Core DevOps Tools, CI/CD & Automation

### 1. Docker
**Key Areas:** Dockerfile, volumes, multi-stage builds, networking  
- **Learn at:**
  - [Docker Docs](https://docs.docker.com/get-started/)
  - [Linkedin Learning](https://www.linkedin.com/learning/paths/docker-foundations-professional-certificate)
  - [Learning Path - Terraform Associate (003) ](https://developer.hashicorp.com/terraform/tutorials/certification-003/associate-study-003)
- **Certs:** 
    - [Docker Certified Associate](https://training.mirantis.com/certification/dca-certification-exam/)
- **You should at minimum be able to:**  
    - Write Dockerfiles to containerize applications  
    - Build and run Docker containers locally  
    - Use Docker volumes for persistent storage  
    - Implement multi-stage builds to optimize image size  
    - Configure container networking basics  

### 2. Infrastructure as Code (IaC) with Terraform
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
    
### 3. CI/CD Concepts & Tools
**Key Areas:** Key skills: writing Jenkinsfiles, GitHub workflows; automating tests, builds, and artifact management.
 
- **Learn at:**
  - [GitHub Actions Docs](https://docs.github.com/en/actions)
  - [Jenkins Book](https://www.jenkins.io/doc/book/)
  - [Jekins Official website](https://www.jenkins.io/doc/tutorials/)
  - [Learn DevOps: CI/CD with Jenkins using Pipelines and Docker](https://www.udemy.com/course/learn-devops-ci-cd-with-jenkins-using-pipelines-and-docker)
  - [Github Actions](https://docs.github.com/en/actions)
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

### 4. Secrets Management
**Tools:** AWS Secrets Manager, Vault, GitHub secrets  
- Securely store/rotate secrets and inject into CI/CD
- **You should at minimum be able to:**  
    - Store secrets securely outside code repositories  
    - Inject secrets into pipelines and runtime environments securely  
    - Rotate and audit secrets regularly  

## Phase 3: More Containers & Orchestration

### 1. Kubernetes
**Key Areas:** Pods, Deployments, Services, ConfigMaps, Ingress  
- **Learn at:**
  - [Kubernetes Docs](https://kubernetes.io/docs/)
  - [Introduction to Kubernetes (LFS158)](https://training.linuxfoundation.org/training/introduction-to-kubernetes/)
- **Certs:**
  - [Certified Kubernetes Administrator (CKA)](https://training.linuxfoundation.org/certification/certified-kubernetes-administrator-cka/)
   - [Certified Kubernetes Security Specialist]()
     - Little extra, but to set you aparat
- **You should at minimum be able to:**  
    - Understand core Kubernetes architecture components  
    - Deploy applications using kubectl and YAML manifests  
    - Manage pods, deployments, and services  
    - Use ConfigMaps and Secrets for configuration management  
    - Configure Ingress controllers to expose services externally 

### 2. Helm & Observability
**Tools:** Helm, Prometheus, Grafana  
- Templating, dashboards, alerts, metrics
- **You should at minimum be able to:**  
    - Use Helm to package and deploy Kubernetes applications  
    - Install and configure Prometheus for metrics collection  
    - Create Grafana dashboards for visualizing metrics  
    - Set up alerts based on key performance indicators  
 
## Phase 4: SRE Mindset, Advanced Ops and Specialization

### 1. Monitoring & Logging
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

### 2. Advanced and Specialized Certs
**Key Areas:**   
- **Learn at:**
  - TBD
- **Certs:**
  - Google Professional Cloud Security Engineer
  - Certified Site Reliability Engineer (SRE)
  - Certified OpenShift Administrator

### 3. Advanced Infra automation, and Configuration Management
**Tools:** Ansible, Cheff, Puppet 
**Key Areas:** Configuration Management
- **Learn at:**
  - TBD
- **Certs:**
  - Puppet Certified Professional
  - Red Hat Certified Specialist in Ansible Automation

### 4. Optional/Advanced Architecture & Cloud Strategy
**Key Areas:**:
- **Learn at:**
  - TBD
- **Certs:**
  - Google Professional Cloud Architect
  - Microsoft Certified: Azure Solutions Architect Expert
  - VMware Certified Professional – Cloud Management and Automation (VCP-CMA)
  - IBM Certified Solution Architect – Cloud Pak for Automation
  - Certified Agile Service Manager (CASM) or Certified ScrumMaster (CSM)

### 5. Security & Cost Optimization
**Key Areas:** IAM, MFA, budgets, encryption, tagging  
- **Learn at:**
  - TBD
- **You should at minimum be able to:**  
    - Apply least privilege principles to IAM roles and policies  
    - Enable and enforce MFA for critical accounts  
    - Tag cloud resources for cost allocation and tracking  
    - Use encryption at rest and in transit  
    - Monitor and optimize cloud costs regularly 

### 6. Chaos Engineering
**Tools:** LitmusChaos, Gremlin  
- Learn failure injection and resiliency testing
- **Learn at:**
  - TBD
- **You should at minimum be able to:**  
    - Understand principles of failure injection and resiliency testing  
    - Use tools to simulate failures and validate system behavior  
    - Analyze results and improve system fault tolerance  


## Ongoing Practice & Interview Prep

- Practice explaining:
  - CI/CD pipeline from commit to prod
  - Docker to K8s rollout process
  - Terraform state and modules
- Mock interviews: deployment scenarios, incident response, YAML debugging
- Build a public GitHub repo: pipelines, IaC, dashboards, diagrams

---

## Why This Order?

1. **Phase 1 (Cloud + IaC)** builds the foundation. 
2. **Phase 2 (CI/CD)** connects cloud infrastructure with delivery pipelines, which you'll need to automate and troubleshoot.
3. **Phase 3 (Containers & K8s)** layers in packaging, deployment, and orchestration—this is the backbone of DevOps delivery at scale.
4. **Phase 4 (SRE Mindset)** rounds out your ops maturity—observability, cost, security, and resilience are what differentiate good from great.
