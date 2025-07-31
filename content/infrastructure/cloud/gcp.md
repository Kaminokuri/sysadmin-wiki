---
title: "Google Cloud Platform"
description: "Services et architectures Google Cloud Platform"
category: "Infrastructure"
tags: ["GCP", "Compute Engine", "BigQuery", "Kubernetes"]
level: "Intermédiaire"
reading_time: "16 min"
last_updated: "31 juillet 2025"
author: "Mathéo Fauvel"
---

# 🟢 Google Cloud Platform

## Vue d'ensemble

Google Cloud Platform (GCP) est la plateforme cloud de Google, spécialisée dans l'analytique, l'intelligence artificielle et les technologies conteneurisées.

## 💻 Services de Calcul

### Compute Engine
```bash
# gcloud CLI - Création VM
gcloud compute instances create my-instance \
    --zone=us-central1-a \
    --machine-type=e2-medium \
    --image-family=ubuntu-2004-lts \
    --image-project=ubuntu-os-cloud
```

### Cloud Functions
```python
# Cloud Function Python
def hello_world(request):
    """HTTP Cloud Function.
    Args:
        request (flask.Request): The request object.
    Returns:
        The response text, or any set of values that can be turned into a
        Response object using `make_response`.
    """
    return 'Hello, World!'
```

### Google Kubernetes Engine (GKE)
```bash
# Création cluster GKE
gcloud container clusters create my-cluster \
    --zone=us-central1-a \
    --num-nodes=3 \
    --enable-autoscaling \
    --min-nodes=1 \
    --max-nodes=10
```

## 📁 Stockage et Bases de Données

### Cloud Storage
```python
# Cloud Storage Python
from google.cloud import storage

client = storage.Client()
bucket = client.bucket('my-bucket')
blob = bucket.blob('my-file.txt')

# Upload
with open('local-file.txt', 'rb') as f:
    blob.upload_from_file(f)
```

### BigQuery
```sql
-- BigQuery SQL
SELECT 
  country,
  COUNT(*) as total_users
FROM `project.dataset.users`
WHERE created_at >= '2025-01-01'
GROUP BY country
ORDER BY total_users DESC
LIMIT 10
```

## 🤖 Intelligence Artificielle

### AI Platform
```python
# AI Platform prediction
from googleapiclient import discovery

service = discovery.build('ml', 'v1')
name = 'projects/{}/models/{}'.format(project, model)

response = service.projects().predict(
    name=name,
    body={'instances': [instance]}
).execute()
```

### Vision API
```python
# Vision API
from google.cloud import vision

client = vision.ImageAnnotatorClient()

with open('image.jpg', 'rb') as image_file:
    content = image_file.read()

image = vision.Image(content=content)
response = client.text_detection(image=image)
```

## 🔐 Sécurité

### Identity and Access Management
```bash
# IAM gcloud
gcloud projects add-iam-policy-binding PROJECT_ID \
    --member="user:jane@example.com" \
    --role="roles/viewer"
```

### Secret Manager
```python
# Secret Manager
from google.cloud import secretmanager

client = secretmanager.SecretManagerServiceClient()
name = f"projects/{project_id}/secrets/{secret_id}/versions/latest"
response = client.access_secret_version(request={"name": name})
secret_value = response.payload.data.decode("UTF-8")
```

---

🎆 **Excellence** : Leader en IA/ML et analytics avec BigQuery, TensorFlow et infrastructure Kubernetes native.