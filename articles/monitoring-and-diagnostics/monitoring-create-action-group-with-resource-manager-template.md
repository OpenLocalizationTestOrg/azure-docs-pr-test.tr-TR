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
# <a name="create-an-action-group-with-a-resource-manager-template"></a><span data-ttu-id="e90f7-103">Resource Manager şablonu ile bir eylem grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="e90f7-103">Create an action group with a Resource Manager template</span></span>
<span data-ttu-id="e90f7-104">Bu makale size nasıl gösterir toouse bir [Azure Resource Manager şablonu](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure Eylem grupları.</span><span class="sxs-lookup"><span data-stu-id="e90f7-104">This article shows you how toouse an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure action groups.</span></span> <span data-ttu-id="e90f7-105">Şablonları kullanarak otomatik olarak belirli uyarı türleri içinde yeniden kullanılabilir Eylem grupları ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e90f7-105">By using templates, you can automatically set up action groups that can be reused in certain types of alerts.</span></span> <span data-ttu-id="e90f7-106">Bu eylem grupları tüm doğru bir uyarı tetiklendiğinde tarafların bildirilir hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="e90f7-106">These action groups ensure that all hello correct parties are notified when an alert is triggered.</span></span>

<span data-ttu-id="e90f7-107">Merhaba temel adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e90f7-107">hello basic steps are:</span></span>

1. <span data-ttu-id="e90f7-108">Bir şablonu nasıl toocreate hello eylem grubu tanımlayan bir JSON dosyası olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e90f7-108">Create a template as a JSON file that describes how toocreate hello action group.</span></span>

2. <span data-ttu-id="e90f7-109">Kullanarak Hello şablonu dağıtma [herhangi bir dağıtım yöntemini](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="e90f7-109">Deploy hello template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

<span data-ttu-id="e90f7-110">İlk olarak, biz açıklamak toocreate bir eylem için bir Resource Manager şablonu Grup nasıl hello eylem tanımları hello şablonu sabit kodlanmış olduğu.</span><span class="sxs-lookup"><span data-stu-id="e90f7-110">First, we describe how toocreate a Resource Manager template for an action group where hello action definitions are hard-coded in hello template.</span></span> <span data-ttu-id="e90f7-111">İkinci olarak, hello şablon dağıtıldığında nasıl toocreate hello Web kancası yapılandırma bilgilerini olarak alan şablon giriş parametreleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="e90f7-111">Second, we describe how toocreate a template that takes hello webhook configuration information as input parameters when hello template is deployed.</span></span>

## <a name="resource-manager-templates-for-an-action-group"></a><span data-ttu-id="e90f7-112">Bir eylem grubu için Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="e90f7-112">Resource Manager templates for an action group</span></span>

<span data-ttu-id="e90f7-113">Resource Manager şablonu kullanarak bir eylem grubu toocreate, oluşturduğunuz hello türde bir kaynak `Microsoft.Insights/actionGroups`.</span><span class="sxs-lookup"><span data-stu-id="e90f7-113">toocreate an action group by using a Resource Manager template, you create a resource of hello type `Microsoft.Insights/actionGroups`.</span></span> <span data-ttu-id="e90f7-114">Ardından tüm ilgili özellikleri doldurur.</span><span class="sxs-lookup"><span data-stu-id="e90f7-114">Then you fill in all related properties.</span></span> <span data-ttu-id="e90f7-115">Bir eylem grubu oluşturma iki örnek Şablonlar aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e90f7-115">Here are two sample templates that create an action group.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="e90f7-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e90f7-116">Next steps</span></span>
* <span data-ttu-id="e90f7-117">Daha fazla bilgi edinmek [Eylem grupları](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="e90f7-117">Learn more about [action groups](monitoring-action-groups.md).</span></span>
* <span data-ttu-id="e90f7-118">Daha fazla bilgi edinmek [uyarıları](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="e90f7-118">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
* <span data-ttu-id="e90f7-119">Bilgi nasıl tooadd [Resource Manager şablonu kullanarak uyarıları](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="e90f7-119">Learn how tooadd [alerts by using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
