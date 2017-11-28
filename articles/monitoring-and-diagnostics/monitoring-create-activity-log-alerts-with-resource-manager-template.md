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
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a><span data-ttu-id="874fb-103">Resource Manager şablonu ile bir etkinlik günlüğü uyarı oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="874fb-103">Create an activity log alert with a Resource Manager template</span></span>
<span data-ttu-id="874fb-104">Bu makale size nasıl gösterir toouse bir [Azure Resource Manager şablonu](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure etkinlik günlüğü uyarıları.</span><span class="sxs-lookup"><span data-stu-id="874fb-104">This article shows you how toouse an [Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure activity log alerts.</span></span> <span data-ttu-id="874fb-105">Şablonlarını kullanarak kolayca otomatik dağıtım işleminin bir parçası belirli etkinlik günlüğü olay koşullara göre etkinleştirme çok uyarı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="874fb-105">By using templates, you can easily set up many alerts that activate based on specific activity log event conditions as part of your automated deployment process.</span></span>

<span data-ttu-id="874fb-106">Merhaba temel adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="874fb-106">hello basic steps are:</span></span>

1. <span data-ttu-id="874fb-107">Bir şablonu nasıl toocreate hello etkinliğini günlüğe uyarı tanımlayan bir JSON dosyası olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="874fb-107">Create a template as a JSON file that describes how toocreate hello activity log alert.</span></span>

2. <span data-ttu-id="874fb-108">Kullanarak Hello şablonu dağıtma [herhangi bir dağıtım yöntemini](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="874fb-108">Deploy hello template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

## <a name="resource-manager-template-for-an-activity-log-alert"></a><span data-ttu-id="874fb-109">Bir etkinlik günlüğü uyarı için Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="874fb-109">Resource Manager template for an activity log alert</span></span>
<span data-ttu-id="874fb-110">toocreate Resource Manager şablonu kullanarak bir etkinlik günlüğü uyarı, oluşturduğunuz hello türde bir kaynak `microsoft.insights/activityLogAlerts`.</span><span class="sxs-lookup"><span data-stu-id="874fb-110">toocreate an activity log alert by using a Resource Manager template, you create a resource of hello type `microsoft.insights/activityLogAlerts`.</span></span> <span data-ttu-id="874fb-111">Ardından tüm ilgili özellikleri doldurur.</span><span class="sxs-lookup"><span data-stu-id="874fb-111">Then you fill in all related properties.</span></span> <span data-ttu-id="874fb-112">Bir etkinlik günlüğü uyarı oluşturan bir şablonu aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="874fb-112">Here's a template that creates an activity log alert.</span></span>

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

<span data-ttu-id="874fb-113">Ziyaret bizim [Azure hızlı başlama Galerisi](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) etkinlik günlüğü uyarı şablonları ile ilgili bazı örnekler.</span><span class="sxs-lookup"><span data-stu-id="874fb-113">Visit our [Azure Quickstart gallery](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) for some examples of activity log alert templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="874fb-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="874fb-114">Next steps</span></span>
- <span data-ttu-id="874fb-115">Daha fazla bilgi edinmek [uyarıları](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="874fb-115">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="874fb-116">Bilgi nasıl tooadd [Resource Manager şablonu kullanarak eylem grupları](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="874fb-116">Learn how tooadd [action groups by using a Resource Manager template](monitoring-create-action-group-with-resource-manager-template.md).</span></span>
- <span data-ttu-id="874fb-117">Nasıl çok öğrenin[bir etkinlik günlüğü uyarı toomonitor aboneliğinizi tüm otomatik ölçeklendirme altyapısı işlemler oluşturmak](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="874fb-117">Learn how too[create an activity log alert toomonitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="874fb-118">Nasıl çok öğrenin[bir etkinlik günlüğü uyarı toomonitor aboneliğinizi tüm başarısız otomatik ölçeklendirme ölçek/genişletme işlemler oluşturmak](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="874fb-118">Learn how too[create an activity log alert toomonitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
