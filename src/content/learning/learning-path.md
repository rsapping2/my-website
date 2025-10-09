---
title: "[WIP] DevOps Learning Path"
pubDate: "2025-09-02"
description: "A learning path for DevOps. This is my ongoing list which I will update as I progress in this learning path."
tags: ["DevOps","learning", "path"]
---
Note: This page is an on going work in progress. I'll update the last updated tag when I update this page.

#### TODOS: Work to add to this page
- For each section
  -  add projects.
  - Add practice interview questions.

---

## Phase 1: Core Refresh & Cloud Infrastructure

### 1. Version Control (Git)
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

### 2. Learning a Programming Language
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


### 3. Operating System (Linux) and Terminal

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


### 4. Networking Fundamentals
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

### 5. Cloud Fundamentals

- Ideally you should have a good understanding of a cloud provider. It really doesn't matter between the large providers, as their market share isn't too drastic. My recommendation is AWS. 

#### A. General Cloud Infrastructure
- **Learn at:**
  - [Introduction to Cloud Infrastructure Technologies (LFS151)](https://training.linuxfoundation.org/training/introduction-to-cloud-infrastructure-technologies/)

##### B. AWS Fundamentals (Recommended)
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

### 6. CLI Practice & Scripting
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

### 7. Database Management
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

## Phase 2: Core DevOps Tools, CI/CD & Automation

### 1. Docker
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
    
### 3. Secrets Management
**Tools:** AWS Secrets Manager, Vault, GitHub secrets  
- Securely store/rotate secrets and inject into CI/CD
- **You should at minimum be able to:**  
    - Store secrets securely outside code repositories  
    - Inject secrets into pipelines and runtime environments securely  
    - Rotate and audit secrets regularly

### 4. CI/CD Concepts & Tools
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

## Phase 3: More Containers & Orchestration

### 1. Kubernetes
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

### 2. GitOps
**Key Areas:** ArgoCD, Flux, declarative deployment patterns
- **Learn at:**
  - [ArgoCD Documentation](https://argo-cd.readthedocs.io/)
  - [Flux Documentation](https://fluxcd.io/docs/)
- **You should at minimum be able to:**
  - Set up GitOps workflows with ArgoCD or Flux
  - Implement declarative deployment patterns
  - Manage application deployments through Git

### 3. Helm & Observability
**Tools:** Helm, Prometheus, Grafana  
- Templating, dashboards, alerts, metrics
- **You should at minimum be able to:**  
    - Use Helm to package and deploy Kubernetes applications  
    - Install and configure Prometheus for metrics collection  
    - Create Grafana dashboards for visualizing metrics  
    - Set up alerts based on key performance indicators  

### 4. API Management
**Key Areas:** REST/GraphQL, API gateways, rate limiting
- **Learn at:**
  - [API Design Best Practices](https://docs.microsoft.com/en-us/azure/architecture/best-practices/api-design)
- **You should at minimum be able to:**
  - Design RESTful APIs and understand GraphQL basics
  - Configure API gateways and rate limiting
  - Implement API versioning and documentation
 
## Phase 4: SRE Mindset, Advanced Ops and Specialization

### 1. Troubleshooting & Debugging
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

### 2. Documentation & Communication
**Key Areas:** Technical writing, runbooks, incident post-mortems
- **Learn at:**
  - [Google Technical Writing Course](https://developers.google.com/tech-writing)
  - [Incident Response Documentation](https://response.pagerduty.com/)
- **You should at minimum be able to:**
  - Write clear technical documentation and runbooks
  - Conduct effective incident post-mortems
  - Create system architecture diagrams
  - Communicate technical concepts to non-technical stakeholders

### 3. Monitoring & Logging
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

### 4. Advanced Infrastructure Automation and Configuration Management
**Tools:** Ansible, Chef, Puppet 
**Key Areas:** Configuration Management
- **Learn at:**
  - TBD
- **Certs:**
  - Puppet Certified Professional
  - Red Hat Certified Specialist in Ansible Automation

### 5. Service Mesh & Microservices
**Key Areas:** Istio, Linkerd, microservices communication patterns
- **Learn at:**
  - [Istio Documentation](https://istio.io/latest/docs/)
  - [Linkerd Documentation](https://linkerd.io/2.11/overview/)
- **You should at minimum be able to:**
  - Understand service mesh concepts and benefits
  - Deploy and configure Istio or Linkerd
  - Implement traffic management and security policies
  - Monitor microservices communication

### 6. Optional/Advanced Architecture & Cloud Strategy
**Key Areas:**
- **Learn at:**
  - TBD
- **Certs:**
  - Google Professional Cloud Architect
  - Microsoft Certified: Azure Solutions Architect Expert
  - VMware Certified Professional – Cloud Management and Automation (VCP-CMA)
  - IBM Certified Solution Architect – Cloud Pak for Automation
  - Certified Agile Service Manager (CASM) or Certified ScrumMaster (CSM)

### 7. Security & Cost Optimization
**Key Areas:** IAM, MFA, budgets, encryption, tagging  
- **Learn at:**
  - TBD
- **You should at minimum be able to:**  
    - Apply least privilege principles to IAM roles and policies  
    - Enable and enforce MFA for critical accounts  
    - Tag cloud resources for cost allocation and tracking  
    - Use encryption at rest and in transit  
    - Monitor and optimize cloud costs regularly 

### 8. Chaos Engineering
**Tools:** LitmusChaos, Gremlin  
- Learn failure injection and resiliency testing
- **Learn at:**
  - TBD
- **You should at minimum be able to:**  
    - Understand principles of failure injection and resiliency testing  
    - Use tools to simulate failures and validate system behavior  
    - Analyze results and improve system fault tolerance

### 9. Advanced and Specialized Certs
**Key Areas:**   
- **Learn at:**
  - TBD
- **Certs:**
  - Google Professional Cloud Security Engineer
  - Certified Site Reliability Engineer (SRE)
  - Certified OpenShift Administrator



## Ongoing Practice & Interview Prep

- Practice explaining:
  - CI/CD pipeline from commit to prod
  - Docker to K8s rollout process
  - Terraform state and modules
- Mock interviews: deployment scenarios, incident response, YAML debugging
- Build a public GitHub repo: pipelines, IaC, dashboards, diagrams

---

## Why This Order?

**Phase 1:** Programming + Linux + Cloud fundamentals create the foundation. You need these before automating anything.
**Phase 2:** Docker + IaC + CI/CD form the core DevOps workflow. Learn to package, provision, and deploy.
**Phase 3:** Kubernetes + Observability handle scale. Orchestration and monitoring are essential for production systems.
**Phase 4:** SRE practices + Advanced certs differentiate you. Focus on reliability, security, and cost optimization.
