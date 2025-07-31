---
title: "Microsoft Azure"
description: "Services et architectures Microsoft Azure"
category: "Infrastructure"
tags: ["Azure", "VM", "Storage", "Functions", "ARM"]
level: "Intermédiaire"
reading_time: "18 min"
last_updated: "31 juillet 2025"
author: "Mathéo Fauvel"
---

# 🔷 Microsoft Azure

## Vue d'ensemble

Microsoft Azure est la plateforme cloud de Microsoft, offrant une intégration native avec l'écosystème Microsoft et des services d'entreprise avancés.

## 💻 Services de Calcul

### Virtual Machines
```bash
# Azure CLI - Création VM
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

### Azure Functions
```csharp
// Fonction Azure C#
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Extensions.Logging;

public static class HttpTrigger
{
    [FunctionName("HttpTrigger")]
    public static IActionResult Run(
        [HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequest req,
        ILogger log)
    {
        log.LogInformation("C# HTTP trigger function processed a request.");
        return new OkObjectResult("Hello Azure!");
    }
}
```

## 📁 Services de Stockage

### Blob Storage
```python
# Azure Blob Storage Python
from azure.storage.blob import BlobServiceClient

blob_service_client = BlobServiceClient(
    account_url="https://mystorageaccount.blob.core.windows.net",
    credential="account_key"
)

# Upload blob
blob_client = blob_service_client.get_blob_client(
    container="mycontainer", 
    blob="myfile.txt"
)

with open("local_file.txt", "rb") as data:
    blob_client.upload_blob(data)
```

## 🌐 Réseau Azure

### Virtual Network
```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "resources": [
    {
      "type": "Microsoft.Network/virtualNetworks",
      "apiVersion": "2021-02-01",
      "name": "myVNet",
      "location": "East US",
      "properties": {
        "addressSpace": {
          "addressPrefixes": ["10.0.0.0/16"]
        },
        "subnets": [
          {
            "name": "default",
            "properties": {
              "addressPrefix": "10.0.1.0/24"
            }
          }
        ]
      }
    }
  ]
}
```

## 📊 Monitoring

### Azure Monitor
```bash
# Métriques Azure CLI
az monitor metrics list \
    --resource "/subscriptions/{subscription}/resourceGroups/{rg}/providers/Microsoft.Compute/virtualMachines/{vm}" \
    --metric "Percentage CPU"
```

### Application Insights
```javascript
// Application Insights JavaScript
import { ApplicationInsights } from '@microsoft/applicationinsights-web';

const appInsights = new ApplicationInsights({ config: {
  instrumentationKey: 'YOUR_INSTRUMENTATION_KEY'
} });
appInsights.loadAppInsights();
appInsights.trackPageView();
```

## 🔐 Sécurité

### Azure Active Directory
```powershell
# Azure AD PowerShell
Connect-AzureAD

# Création utilisateur
New-AzureADUser -DisplayName "John Doe" -UserPrincipalName "john@domain.com" -PasswordProfile $PasswordProfile

# Attribution rôle
Add-AzureADDirectoryRoleMember -ObjectId $roleId -RefObjectId $userId
```

### Key Vault
```bash
# Gestion secrets
az keyvault secret set --vault-name "MyKeyVault" --name "DatabasePassword" --value "MySecretPassword"
az keyvault secret show --vault-name "MyKeyVault" --name "DatabasePassword"
```

---

🏆 **Avantage** : Intégration transparente avec l'écosystème Microsoft (Office 365, Windows Server, .NET).