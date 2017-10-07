---
title: "aaaAutomatically tanılama Resource Manager şablonu kullanarak ayarlarını etkinleştir | Microsoft Docs"
description: "Bilgi nasıl toouse Resource Manager toostream etkinleştirecek şablonu toocreate tanılama ayarlarını, tanılama günlüklerini tooEvent hub'ları veya bir depolama hesabında depolamak."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a8a88a8c-4a48-4df6-8f7e-d90634d39c57
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/14/2017
ms.author: johnkem
ms.openlocfilehash: 8f38731107029928029c6d940da7bd076fea5d49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="fa0cf-103">Resource Manager şablonu kullanarak kaynak oluşturma sırasında otomatik olarak tanılama ayarlarını etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="fa0cf-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="fa0cf-104">Bu makalede biz nasıl kullanabileceğinizi gösterir. bir [Azure Resource Manager şablonu](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure tanılama ayarlarını oluşturulduğunda kaynak üzerinde.</span><span class="sxs-lookup"><span data-stu-id="fa0cf-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="fa0cf-105">Bu, tanılama günlüklerini ve ölçümleri tooEvent bir depolama hesabında arşivleme veya bir kaynak oluşturulduğunda tooLog Analytics göndererek hub akış tooautomatically başlangıç sağlar.</span><span class="sxs-lookup"><span data-stu-id="fa0cf-105">This enables you tooautomatically start streaming your Diagnostic Logs and metrics tooEvent Hubs, archiving them in a Storage Account, or sending them tooLog Analytics when a resource is created.</span></span>

<span data-ttu-id="fa0cf-106">Tanılama günlüklerini Resource Manager şablonu kullanarak etkinleştirmek için hello yöntemi hello kaynak türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="fa0cf-106">hello method for enabling Diagnostic Logs using a Resource Manager template depends on hello resource type.</span></span>

* <span data-ttu-id="fa0cf-107">**İşlem olmayan** kaynakları (örneğin, ağ güvenlik grupları, Logic Apps Otomasyonu) kullanmak [tanılama bu makalede açıklanan ayarlarını](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="fa0cf-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="fa0cf-108">**İşlem** (WAD/LAD tabanlı) kaynakları hello kullan [WAD/LAD yapılandırma dosyasını bu makalede açıklanan](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="fa0cf-108">**Compute** (WAD/LAD-based) resources use hello [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="fa0cf-109">Biz bu makalede açıklamak nasıl her iki yöntemi kullanarak tooconfigure tanılama.</span><span class="sxs-lookup"><span data-stu-id="fa0cf-109">In this article we describe how tooconfigure diagnostics using either method.</span></span>

<span data-ttu-id="fa0cf-110">Merhaba temel adımlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="fa0cf-110">hello basic steps are as follows:</span></span>

1. <span data-ttu-id="fa0cf-111">Bir şablonu nasıl toocreate kaynak hello ve tanılamayı etkinleştirin açıklayan bir JSON dosyası olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fa0cf-111">Create a template as a JSON file that describes how toocreate hello resource and enable diagnostics.</span></span>
2. <span data-ttu-id="fa0cf-112">[Herhangi bir dağıtım yöntemi kullanarak hello şablonu dağıtmak](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="fa0cf-112">[Deploy hello template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="fa0cf-113">Aşağıda hello şablonu toogenerate işlem dışı ve işlem kaynakları için gereksinim duyduğunuz JSON dosyası örneği sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="fa0cf-113">Below we give an example of hello template JSON file you need toogenerate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="fa0cf-114">İşlem olmayan kaynak şablonu</span><span class="sxs-lookup"><span data-stu-id="fa0cf-114">Non-Compute resource template</span></span>
<span data-ttu-id="fa0cf-115">İşlem olmayan kaynakları toodo iki şey gerekir:</span><span class="sxs-lookup"><span data-stu-id="fa0cf-115">For non-Compute resources, you will need toodo two things:</span></span>

1. <span data-ttu-id="fa0cf-116">Parametreleri toohello parametreleri blob hello depolama hesabı adı, hizmet veri yolu kural kimliği ve/veya OMS günlük analizi çalışma alanı kimliği (günlükleri tooEvent Hubs akış ve/veya günlükleri tooLog Analytics gönderme depolama hesabı, tanılama günlüklerini arşivleme etkinleştirmek) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fa0cf-116">Add parameters toohello parameters blob for hello storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs tooEvent Hubs, and/or sending logs tooLog Analytics).</span></span>
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
      }
    }
    ```
2. <span data-ttu-id="fa0cf-117">Hello kaynakları dizisinde tooenable tanılama günlüklerini istediğiniz hello kaynağının, bir kaynak türü eklemek `[resource namespace]/providers/diagnosticSettings`.</span><span class="sxs-lookup"><span data-stu-id="fa0cf-117">In hello resources array of hello resource for which you want tooenable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
    ```json
    "resources": [
      {
        "type": "providers/diagnosticSettings",
        "name": "Microsoft.Insights/service",
        "dependsOn": [
          "[/*resource Id for which Diagnostic Logs will be enabled>*/]"
        ],
        "apiVersion": "2015-07-01",
        "properties": {
          "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
          "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
          "workspaceId": "[parameters('workspaceId')]",
          "logs": [ 
            {
              "category": "/* log category name */",
              "enabled": true,
              "retentionPolicy": {
                "days": 0,
                "enabled": false
              }
            }
          ],
          "metrics": [
            {
              "timeGrain": "PT1M",
              "enabled": true,
              "retentionPolicy": {
                "enabled": false,
                "days": 0
              }
            }
          ]
        }
      }
    ]
    ```

<span data-ttu-id="fa0cf-118">Merhaba hello tanılama ayarını için özellikler blob izleyen [bu makalede açıklanan hello biçimi](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="fa0cf-118">hello properties blob for hello Diagnostic Setting follows [hello format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="fa0cf-119">Ekleme hello `metrics` özelliğini etkinleştirir, aynı çıkarır, sağlanan, tooalso gönderme kaynak ölçümleri toothese [hello kaynak destekleyen Azure İzleyici ölçümleri](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="fa0cf-119">Adding hello `metrics` property will enable you tooalso send resource metrics toothese same outputs, provided that [hello resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="fa0cf-120">Aşağıda, bir mantıksal uygulama oluşturan ve akış tooEvent hub'lar ve bir depolama hesabındaki depolama kapatır tam bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fa0cf-120">Here is a full example that creates a Logic App and turns on streaming tooEvent Hubs and storage in a storage account.</span></span>

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
      }
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Logic/workflows",
      "name": "[parameters('logicAppName')]",
      "apiVersion": "2016-06-01",
      "location": "[resourceGroup().location]",
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      },
      "resources": [
        {
          "type": "providers/diagnosticSettings",
          "name": "Microsoft.Insights/service",
          "dependsOn": [
            "[resourceId('Microsoft.Logic/workflows', parameters('logicAppName'))]"
          ],
          "apiVersion": "2015-07-01",
          "properties": {
            "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
            "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
            "workspaceId": "[parameters('workspaceId')]",
            "logs": [
              {
                "category": "WorkflowRuntime",
                "enabled": true,
                "retentionPolicy": {
                  "days": 0,
                  "enabled": false
                }
              }
            ],
            "metrics": [
              {
                "timeGrain": "PT1M",
                "enabled": true,
                "retentionPolicy": {
                  "enabled": false,
                  "days": 0
                }
              }
            ]
          }
        }
      ],
      "dependsOn": []
    }
  ]
}

```

## <a name="compute-resource-template"></a><span data-ttu-id="fa0cf-121">Kaynak şablonu işlem</span><span class="sxs-lookup"><span data-stu-id="fa0cf-121">Compute resource template</span></span>
<span data-ttu-id="fa0cf-122">Örneğin bir sanal makine veya Service Fabric kümesi, bir işlem kaynağına tooenable tanılama şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="fa0cf-122">tooenable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="fa0cf-123">Hello Azure tanılama uzantısını toohello VM kaynak tanımını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fa0cf-123">Add hello Azure Diagnostics extension toohello VM resource definition.</span></span>
2. <span data-ttu-id="fa0cf-124">Bir depolama hesabı ve/veya olay hub'ı bir parametre olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="fa0cf-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="fa0cf-125">WADCfg XML dosyanızı Merhaba içeriğine tüm XML karakterleri düzgün kaçış hello XMLCfg özelliğinin içine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fa0cf-125">Add hello contents of your WADCfg XML file into hello XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="fa0cf-126">Bu son adım, hassas tooget sağ olabilir.</span><span class="sxs-lookup"><span data-stu-id="fa0cf-126">This last step can be tricky tooget right.</span></span> <span data-ttu-id="fa0cf-127">[Bu makaleye bakın](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) bölmelerini kaçışlı ve doğru biçimlendirilmiş değişkenleri tanılama yapılandırma şeması hello bir örnek.</span><span class="sxs-lookup"><span data-stu-id="fa0cf-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits hello Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="fa0cf-128">Merhaba, örnekler dahil olmak üzere tüm işlem açıklanan [bu belgedeki](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fa0cf-128">hello entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa0cf-129">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="fa0cf-129">Next Steps</span></span>
* [<span data-ttu-id="fa0cf-130">Azure tanılama günlükleri hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="fa0cf-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="fa0cf-131">Akış Azure tanılama günlükleri tooEvent hub'lar</span><span class="sxs-lookup"><span data-stu-id="fa0cf-131">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

