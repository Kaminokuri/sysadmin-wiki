---
title: "Amazon AWS"
description: "Services et architectures Amazon Web Services"
category: "Infrastructure"
tags: ["AWS", "EC2", "S3", "Lambda", "VPC"]
level: "Intermédiaire"
reading_time: "20 min"
last_updated: "31 juillet 2025"
author: "Mathéo Fauvel"
---

# 🟠 Amazon AWS

## Vue d'ensemble

Amazon Web Services est le leader mondial du cloud computing, proposant plus de 200 services dans 31 régions géographiques avec une infrastructure robuste et évolutive.

## 🖥️ Services de Calcul

### EC2 (Elastic Compute Cloud)
```bash
# AWS CLI - Lancement instance
aws ec2 run-instances \
    --image-id ami-0abcdef1234567890 \
    --count 1 \
    --instance-type t3.micro \
    --key-name MyKeyPair \
    --security-group-ids sg-903004f8 \
    --subnet-id subnet-6e7f829e
```

### Types d'Instances
| Famille | Usage | Exemples |
|---------|--------|----------|
| General Purpose | Équilibré | t3, m5, m6 |
| Compute Optimized | CPU intensif | c5, c6 |
| Memory Optimized | RAM intensive | r5, x1 |
| Storage Optimized | I/O élevées | i3, d3 |
| Accelerated | GPU/FPGA | p3, g4 |

### Lambda (Serverless)
```python
# Fonction Lambda Python
import json

def lambda_handler(event, context):
    # Traitement de l'événement
    name = event.get('name', 'World')
    
    return {
        'statusCode': 200,
        'body': json.dumps(f'Hello {name}!')
    }
```

## 💾 Services de Stockage

### S3 (Simple Storage Service)
```bash
# Gestion buckets S3
aws s3 mb s3://my-bucket-name
aws s3 cp file.txt s3://my-bucket-name/
aws s3 sync ./local-folder s3://my-bucket-name/folder/

# Lifecycle policy
aws s3api put-bucket-lifecycle-configuration \
    --bucket my-bucket \
    --lifecycle-configuration file://lifecycle.json
```

### Classes de Stockage S3
- **Standard** : Accès fréquent
- **Standard-IA** : Accès peu fréquent  
- **Glacier** : Archivage long terme
- **Deep Archive** : Archivage très long terme

### EBS (Elastic Block Store)
```bash
# Création volume EBS
aws ec2 create-volume \
    --size 100 \
    --volume-type gp3 \
    --availability-zone us-west-2a

# Attachement à instance
aws ec2 attach-volume \
    --volume-id vol-1234567890abcdef0 \
    --instance-id i-1234567890abcdef0 \
    --device /dev/sdf
```

## 🌐 Services Réseau

### VPC (Virtual Private Cloud)
```json
{
  "VpcId": "vpc-12345678",
  "CidrBlock": "10.0.0.0/16",
  "Subnets": [
    {
      "SubnetId": "subnet-12345678",
      "CidrBlock": "10.0.1.0/24",
      "AvailabilityZone": "us-west-2a"
    }
  ]
}
```

### Security Groups
```bash
# Règles de sécurité
aws ec2 authorize-security-group-ingress \
    --group-id sg-12345678 \
    --protocol tcp \
    --port 22 \
    --cidr 203.0.113.0/24
```

### Load Balancing
- **ALB** : Application Load Balancer (Layer 7)
- **NLB** : Network Load Balancer (Layer 4)
- **CLB** : Classic Load Balancer (Legacy)

## 🗃️ Services de Base de Données

### RDS (Relational Database Service)
```bash
# Création instance RDS
aws rds create-db-instance \
    --db-instance-identifier mydbinstance \
    --db-instance-class db.t3.micro \
    --engine mysql \
    --master-username admin \
    --master-user-password mypassword \
    --allocated-storage 20
```

### DynamoDB (NoSQL)
```python
# Boto3 DynamoDB
import boto3

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('users')

# Insert item
table.put_item(
    Item={
        'userId': '123',
        'name': 'John Doe',
        'email': 'john@example.com'
    }
)

# Query item
response = table.get_item(
    Key={'userId': '123'}
)
```

## 🔧 Services de Gestion

### CloudFormation (IaC)
```yaml
# Template CloudFormation
AWSTemplateFormatVersion: '2010-09-09'
Resources:
  MyEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: ami-0abcdef1234567890
      InstanceType: t2.micro
      KeyName: !Ref KeyPairName
      SecurityGroupIds:
        - !Ref MySecurityGroup
        
  MySecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Enable SSH access
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0
```

### Systems Manager
```bash
# Exécution commandes distantes
aws ssm send-command \
    --instance-ids "i-1234567890abcdef0" \
    --document-name "AWS-RunShellScript" \
    --parameters 'commands=["sudo yum update -y"]'
```

## 📊 Monitoring et Logging

### CloudWatch
```python
# CloudWatch metrics
import boto3

cloudwatch = boto3.client('cloudwatch')

# Envoi métrique custom
cloudwatch.put_metric_data(
    Namespace='MyApp',
    MetricData=[
        {
            'MetricName': 'ProcessedItems',
            'Value': 123,
            'Unit': 'Count'
        }
    ]
)
```

### CloudTrail
```json
{
  "Trail": {
    "Name": "my-trail",
    "S3BucketName": "my-cloudtrail-bucket",
    "IncludeGlobalServiceEvents": true,
    "IsMultiRegionTrail": true,
    "EnableLogFileValidation": true
  }
}
```

## 🔐 Sécurité et Identité

### IAM (Identity and Access Management)
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::my-bucket/*"
    }
  ]
}
```

### AWS Secrets Manager
```python
# Récupération secret
import boto3
from botocore.exceptions import ClientError

def get_secret():
    secret_name = "prod/myapp/db"
    region_name = "us-west-2"
    
    session = boto3.session.Session()
    client = session.client(
        service_name='secretsmanager',
        region_name=region_name
    )
    
    try:
        get_secret_value_response = client.get_secret_value(
            SecretId=secret_name
        )
        return get_secret_value_response['SecretString']
    except ClientError as e:
        raise e
```

## 🚀 DevOps et CI/CD

### CodePipeline
```json
{
  "pipeline": {
    "name": "MyPipeline",
    "stages": [
      {
        "name": "Source",
        "actions": [
          {
            "name": "Source",
            "actionTypeId": {
              "category": "Source",
              "owner": "AWS",
              "provider": "S3"
            }
          }
        ]
      },
      {
        "name": "Build",
        "actions": [
          {
            "name": "Build",
            "actionTypeId": {
              "category": "Build",
              "owner": "AWS", 
              "provider": "CodeBuild"
            }
          }
        ]
      }
    ]
  }
}
```

### ECS (Elastic Container Service)
```yaml
# Task Definition
family: myapp
networkMode: awsvpc
requiresCompatibilities:
  - FARGATE
cpu: 256
memory: 512
containerDefinitions:
  - name: myapp-container
    image: nginx:latest
    portMappings:
      - containerPort: 80
        protocol: tcp
```

## 💰 Optimisation des Coûts

### Reserved Instances
- **Standard RI** : Jusqu'à 75% d'économie
- **Convertible RI** : Flexibilité type instance
- **Scheduled RI** : Usage prévisible

### Spot Instances
```bash
# Lancement Spot instance
aws ec2 request-spot-instances \
    --spot-price "0.05" \
    --instance-count 1 \
    --launch-specification file://specification.json
```

### Trusted Advisor
- **Cost Optimization** : Recommandations
- **Performance** : Amélioration
- **Security** : Vulnérabilités
- **Fault Tolerance** : Résilience

## 🏗️ Architecture Well-Architected

### 5 Piliers
1. **Operational Excellence** : Automatisation
2. **Security** : Protection données
3. **Reliability** : Récupération automatique
4. **Performance Efficiency** : Optimisation ressources
5. **Cost Optimization** : Éviter gaspillage

### Patterns d'Architecture
```
┌─────────────────┐    ┌─────────────────┐
│   CloudFront    │────│      ALB        │
│      (CDN)      │    │ (Load Balancer) │
└─────────────────┘    └─────────────────┘
                              │
                    ┌─────────┼─────────┐
                    │                   │
              ┌───────────┐      ┌───────────┐
              │   EC2     │      │   EC2     │
              │ AZ-1a     │      │ AZ-1b     │
              └───────────┘      └───────────┘
                    │                   │
              ┌───────────┐      ┌───────────┐
              │    RDS    │      │    RDS    │
              │ Primary   │      │ Standby   │
              └───────────┘      └───────────┘
```

---

⚡ **Pro Tip** : Utilisez AWS Cost Explorer et Trusted Advisor pour optimiser régulièrement vos coûts AWS.