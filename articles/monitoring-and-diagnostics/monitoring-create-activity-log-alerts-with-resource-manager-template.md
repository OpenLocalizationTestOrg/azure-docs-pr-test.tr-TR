---
title: "Resource Manager şablonu ile bir etkinlik günlüğü uyarı aaaCreate | Microsoft Docs"
description: "Azure kaynaklarınızı oluşturduğunuzda bilgi edinin."
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
ms.date: 07/06/2017
ms.author: ancav
ms.openlocfilehash: 0fb8aa037b9dce54ce35498622770955f2341bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a>Resource Manager şablonu ile bir etkinlik günlüğü uyarı oluşturabilir.
Bu makale size nasıl gösterir toouse bir [Azure Resource Manager şablonu](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure etkinlik günlüğü uyarıları. Şablonlarını kullanarak kolayca otomatik dağıtım işleminin bir parçası belirli etkinlik günlüğü olay koşullara göre etkinleştirme çok uyarı ayarlayabilirsiniz.

Merhaba temel adımlar şunlardır:

1. Bir şablonu nasıl toocreate hello etkinliğini günlüğe uyarı tanımlayan bir JSON dosyası olarak oluşturun.

2. Kullanarak Hello şablonu dağıtma [herhangi bir dağıtım yöntemini](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).

## <a name="resource-manager-template-for-an-activity-log-alert"></a>Bir etkinlik günlüğü uyarı için Resource Manager şablonu
toocreate Resource Manager şablonu kullanarak bir etkinlik günlüğü uyarı, oluşturduğunuz hello türde bir kaynak `microsoft.insights/activityLogAlerts`. Ardından tüm ilgili özellikleri doldurur. Bir etkinlik günlüğü uyarı oluşturan bir şablonu aşağıda verilmiştir.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not hello alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for hello Action group."
      }
    }
  },
  "resources": [   
    {
      "type": "Microsoft.Insights/activityLogAlerts",
      "apiVersion": "2017-04-01",
      "name": "[parameters('activityLogAlertName')]",      
      "location": "Global",
      "properties": {
        "enabled": "[parameters('activityLogAlertEnabled')]",
        "scopes": [
            "[subscription().id]"
        ],        
        "condition": {
          "allOf": [
            {
              "field": "category",
              "equals": "Administrative"
            },
            {
              "field": "operationName",
              "equals": "Microsoft.Resources/deployments/write"
            },
            {
              "field": "resourceType",
              "equals": "Microsoft.Resources/deployments"
            }
          ] 
        },
        "actions": {
          "actionGroups": 
          [
            {
              "actionGroupId": "[parameters('actionGroupResourceId')]"
            }
          ]
        }
      }
    }
  ]
}
```

Ziyaret bizim [Azure hızlı başlama Galerisi](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) etkinlik günlüğü uyarı şablonları ile ilgili bazı örnekler.

## <a name="next-steps"></a>Sonraki adımlar
- Daha fazla bilgi edinmek [uyarıları](monitoring-overview-alerts.md).
- Bilgi nasıl tooadd [Resource Manager şablonu kullanarak eylem grupları](monitoring-create-action-group-with-resource-manager-template.md).
- Nasıl çok öğrenin[bir etkinlik günlüğü uyarı toomonitor aboneliğinizi tüm otomatik ölçeklendirme altyapısı işlemler oluşturmak](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).
- Nasıl çok öğrenin[bir etkinlik günlüğü uyarı toomonitor aboneliğinizi tüm başarısız otomatik ölçeklendirme ölçek/genişletme işlemler oluşturmak](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).
