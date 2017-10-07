---
title: "Resource Manager şablonları ile aaaCreate Eylem grupları | Microsoft Docs"
description: "Bir eylem toocreate Grup bir Azure Resource Manager şablonu kullanılarak nasıl öğrenin."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 9902b33cad99bd99b3deda0cf6f4ff12278c89c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-action-group-with-a-resource-manager-template"></a>Resource Manager şablonu ile bir eylem grubu oluştur
Bu makale size nasıl gösterir toouse bir [Azure Resource Manager şablonu](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure Eylem grupları. Şablonları kullanarak otomatik olarak belirli uyarı türleri içinde yeniden kullanılabilir Eylem grupları ayarlayabilirsiniz. Bu eylem grupları tüm doğru bir uyarı tetiklendiğinde tarafların bildirilir hello emin olun.

Merhaba temel adımlar şunlardır:

1. Bir şablonu nasıl toocreate hello eylem grubu tanımlayan bir JSON dosyası olarak oluşturun.

2. Kullanarak Hello şablonu dağıtma [herhangi bir dağıtım yöntemini](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).

İlk olarak, biz açıklamak toocreate bir eylem için bir Resource Manager şablonu Grup nasıl hello eylem tanımları hello şablonu sabit kodlanmış olduğu. İkinci olarak, hello şablon dağıtıldığında nasıl toocreate hello Web kancası yapılandırma bilgilerini olarak alan şablon giriş parametreleri açıklar.

## <a name="resource-manager-templates-for-an-action-group"></a>Bir eylem grubu için Resource Manager şablonları

Resource Manager şablonu kullanarak bir eylem grubu toocreate, oluşturduğunuz hello türde bir kaynak `Microsoft.Insights/actionGroups`. Ardından tüm ilgili özellikleri doldurur. Bir eylem grubu oluşturma iki örnek Şablonlar aşağıda verilmiştir.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
      }
    }
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
          {
            "name": "contosoSMS",
            "countryCode": "1",
            "phoneNumber": "5555551212"
          },
          {
            "name": "contosoSMS2",
            "countryCode": "1",
            "phoneNumber": "5555552121"
          }
        ],
        "emailReceivers": [
          {
            "name": "contosoEmail",
            "emailAddress": "devops@contoso.com"
          },
          {
            "name": "contosoEmail2",
            "emailAddress": "devops2@contoso.com"
          }
        ],
        "webhookReceivers": [
          {
            "name": "contosoHook",
            "serviceUri": "http://requestb.in/1bq62iu1"
          },
          {
            "name": "contosoHook2",
            "serviceUri": "http://requestb.in/1bq62iu2"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
      }
    },
    "webhookReceiverName": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    },    
    "webhookServiceUri": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    }    
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
        ],
        "emailReceivers": [
        ],
        "webhookReceivers": [
          {
            "name": "[parameters('webhookReceiverName')]",
            "serviceUri": "[parameters('webhookServiceUri')]"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupResourceId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```


## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [Eylem grupları](monitoring-action-groups.md).
* Daha fazla bilgi edinmek [uyarıları](monitoring-overview-alerts.md).
* Bilgi nasıl tooadd [Resource Manager şablonu kullanarak uyarıları](monitoring-create-activity-log-alerts-with-resource-manager-template.md).
