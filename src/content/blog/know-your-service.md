---
title: "Know your Components!"
pubDate: "2025-07-10"
description: ""
tags: ["aws", "gcp", "open market", "components"]
---


<p style="text-align: center;">
  <img src="/images/components.png" alt="My garden" style="max-width: 100%; height: auto; border-radius: 8px;" />
</p>

| **Component**                       | **AWS**                          | **GCP**                                          | **Open Market / Open Source**                        |
|-------------------------------------|----------------------------------|--------------------------------------------------|------------------------------------------------------|
| **VM / Compute**                    | EC2                              | Compute Engine                                   | VirtualBox, VMware, Proxmox, Bare metal              |
| **App Server (Tomcat)**             | EC2 with Tomcat                  | Compute Engine with Tomcat                       | Apache Tomcat (self-hosted)                          |
| **Message Broker (RabbitMQ)**       | Amazon MQ (RabbitMQ engine)      | Cloud Pub/Sub\*, RabbitMQ on GCE                 | RabbitMQ (self-hosted), Apache Kafka                 |
| **Cache (Memcached)**               | ElastiCache (Memcached)          | Memorystore (Memcached)                          | Memcached (self-hosted), Redis                       |
| **Database (MySQL)**                | RDS (MySQL)                      | Cloud SQL (MySQL)                                | MySQL (self-hosted), MariaDB                         |
| **Load Balancer (Nginx)**           | Elastic Load Balancer (ELB)      | Cloud Load Balancing                             | Nginx, HAProxy, Traefik                              |
| **Auto Scaling**                    | EC2 Auto Scaling                 | Managed Instance Groups                          | Kubernetes Horizontal Pod Autoscaler, custom scripts |
| **Private DNS / Service Discovery** | Route 53 Private Hosted Zones    | Cloud DNS with private zones                     | CoreDNS, Consul, BIND                                |
