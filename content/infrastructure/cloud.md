---
title: "Cloud Computing"
description: "Stratégies et technologies cloud : AWS, Azure, GCP et cloud hybride"
category: "Infrastructure"
tags: ["Cloud", "AWS", "Azure", "GCP", "Multi-cloud"]
level: "Intermédiaire"
reading_time: "25 min"
last_updated: "31 juillet 2025"
author: "Mathéo Fauvel"
---

# ☁️ Cloud Computing

## Vue d'ensemble

Le cloud computing révolutionne l'infrastructure IT en offrant des ressources informatiques à la demande, avec une scalabilité, une flexibilité et une optimisation des coûts sans précédent.

## 🏗️ Modèles de Service

### IaaS (Infrastructure as a Service)
- **Compute** : Virtual machines, containers
- **Storage** : Object, block, file storage  
- **Network** : VPC, load balancers, CDN
- **Exemples** : AWS EC2, Azure VMs, GCP Compute Engine

### PaaS (Platform as a Service)
- **Application platforms** : App Engine, Lambda
- **Databases** : RDS, CosmosDB, Cloud SQL
- **Development tools** : CI/CD pipelines
- **Middleware** : Message queues, APIs

### SaaS (Software as a Service)
- **Business applications** : Office 365, Salesforce
- **Productivity tools** : Google Workspace
- **Specialized software** : CRM, ERP, BI

## 🏢 Modèles de Déploiement

### Public Cloud
- **Ressources partagées** multi-tenant
- **Coût optimisé** pay-as-you-use
- **Scalabilité maximale**
- **Maintenance assurée** par le provider

### Private Cloud
- **Ressources dédiées** single-tenant
- **Contrôle total** de la sécurité
- **Compliance** réglementaire
- **Coûts fixes** plus élevés

### Hybrid Cloud
- **Combinaison** public + private
- **Workload distribution** optimisée
- **Data sovereignty** respectée
- **Flexibilité maximale**

### Multi-Cloud
- **Plusieurs providers** simultaneously
- **Éviter vendor lock-in**
- **Best-of-breed** services
- **Complexité de gestion**

## 🚀 Avantages du Cloud

### Économiques
- **CAPEX vers OPEX** : Transformation des coûts
- **Pay-as-you-use** : Optimisation budgétaire
- **Économies d'échelle** : Mutualisation
- **ROI rapide** : Time-to-market

### Techniques
- **Scalabilité automatique** : Auto-scaling
- **Haute disponibilité** : Multi-AZ/region
- **Performance** : Global infrastructure
- **Innovation** : Services managés

### Opérationnels
- **Agilité** : Provisioning rapide
- **Focus métier** : Moins d'ops
- **Mobilité** : Accès anywhere
- **Collaboration** : Outils partagés

## 🛡️ Sécurité Cloud

### Modèle de Responsabilité Partagée
```
Provider Responsibility:
├── Physical infrastructure
├── Network controls
├── Host OS patching
└── Hypervisor

Customer Responsibility:
├── Data encryption
├── Network traffic protection
├── OS/application patching
├── Identity & access management
└── Application-level controls
```

### Bonnes Pratiques Sécurité
- **Identity & Access Management** : Principe moindre privilège
- **Network Security** : VPC, security groups
- **Data Encryption** : At rest + in transit
- **Monitoring** : CloudTrail, logs, SIEM
- **Compliance** : SOC2, PCI-DSS, GDPR

## 📊 FinOps et Optimisation Coûts

### Stratégies d'Optimisation
- **Right-sizing** : Dimensionnement optimal
- **Reserved Instances** : Engagements long terme
- **Spot Instances** : Workloads interruptibles
- **Auto-scaling** : Ajustement automatique

### Outils de Monitoring
- **AWS Cost Explorer** : Analyse détaillée
- **Azure Cost Management** : Budgets & alerts
- **GCP Cloud Billing** : Reporting avancé
- **Third-party** : CloudHealth, Cloudability

### Gouvernance Financière
```yaml
# Budget Alert Template
Budget:
  Name: "Production-Monthly"
  BudgetLimit: 10000
  TimeUnit: MONTHLY
  CostFilters:
    Service: ["EC2-Instance", "RDS"]
  BudgetType: COST
  AlertThresholds:
    - Type: ACTUAL
      Threshold: 80
    - Type: FORECASTED  
      Threshold: 100
```

## 🔄 Migration vers le Cloud

### Stratégies des 6 R
1. **Rehost** (Lift & Shift) : Migration directe
2. **Replatform** : Optimisations mineures
3. **Repurchase** : Passage au SaaS
4. **Refactor** : Réécriture cloud-native
5. **Retire** : Décommissioning
6. **Retain** : Maintien on-premise

### Framework de Migration
```
Assessment → Planning → Migration → Optimization
     ↓           ↓         ↓           ↓
  Discovery   Wave Plan  Execute   Continuous
  Portfolio   Design    Migrate   Improvement
  Dependencies Teams    Validate  Cost Opt
```

### Outils de Migration
- **AWS Migration Hub** : Orchestration
- **Azure Migrate** : Assessment & migration
- **GCP Migrate** : VM migration
- **CloudEndure** : Continuous replication

## 🏗️ Architectures Cloud-Native

### Microservices
```yaml
# Kubernetes microservice example
apiVersion: apps/v1
kind: Deployment
metadata:
  name: user-service
spec:
  replicas: 3
  selector:
    matchLabels:
      app: user-service
  template:
    metadata:
      labels:
        app: user-service
    spec:
      containers:
      - name: user-service
        image: myregistry/user-service:v1.0
        ports:
        - containerPort: 8080
```

### Serverless Computing
- **Functions** : Event-driven execution
- **API Gateway** : RESTful APIs
- **Event sourcing** : Asynchronous processing
- **Cold start** : Performance consideration

### Container Orchestration
- **Kubernetes** : Industry standard
- **Docker Swarm** : Simple orchestration
- **Managed services** : EKS, AKS, GKE
- **Service mesh** : Istio, Linkerd

## 📈 Monitoring et Observabilité

### Pilliers de l'Observabilité
1. **Metrics** : Performance indicators
2. **Logs** : Event records
3. **Traces** : Request flow

### Outils Cloud-Native
- **Prometheus + Grafana** : Metrics & visualization
- **ELK Stack** : Logs aggregation
- **Jaeger** : Distributed tracing
- **Cloud providers** : Native monitoring

### SLI/SLO/SLA Framework
```yaml
# Service Level Objectives
SLO:
  availability: "99.9%"
  latency_p99: "<100ms"
  error_rate: "<0.1%"
  
SLI:
  availability: "successful_requests / total_requests"
  latency: "histogram_quantile(0.99, request_duration)"
```

## 🌍 Multi-Cloud Strategy

### Avantages Multi-Cloud
- **Vendor neutrality** : Éviter lock-in
- **Best-of-breed** : Meilleurs services
- **Risk mitigation** : Diversification
- **Regulatory compliance** : Data residency

### Défis Multi-Cloud
- **Complexity** : Gestion multiple
- **Skills gap** : Expertise diverse
- **Network latency** : Inter-cloud
- **Data consistency** : Synchronization

### Outils Multi-Cloud
- **Terraform** : Infrastructure as Code
- **Kubernetes** : Portable orchestration
- **Istio** : Service mesh
- **Anthos/Arc** : Hybrid management

## 🔮 Tendances Futures

### Edge Computing
- **IoT integration** : Device connectivity
- **Low latency** : Real-time processing
- **Bandwidth optimization** : Local processing
- **5G enablement** : Network evolution

### AI/ML as a Service
- **Pre-trained models** : Ready-to-use AI
- **AutoML** : Democratized ML
- **MLOps** : ML lifecycle management
- **Edge AI** : Inference at edge

### Sustainability
- **Carbon neutrality** : Green cloud
- **Renewable energy** : Clean power
- **Efficiency optimization** : Resource usage
- **Circular economy** : Hardware reuse

---

🎯 **Success Factor** : Une stratégie cloud réussie aligne les objectifs business avec les capacités techniques et la gouvernance.