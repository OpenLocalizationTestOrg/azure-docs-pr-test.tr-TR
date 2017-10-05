---
title: "Otomatik olarak bir Resource Manager şablonu kullanarak tanılama ayarlarını etkinleştirin | Microsoft Docs"
description: "Tanılama günlüklerinize Event hubs'a akışla aktarmak veya bir depolama hesabında depolamak sağlayacak tanılama ayarları oluşturmak için Resource Manager şablonu kullanmayı öğrenin."
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
ms.openlocfilehash: dde2435e976bbd14ca35cccc714ea21dcc5817b7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="e81a1-103">Resource Manager şablonu kullanarak kaynak oluşturma sırasında otomatik olarak tanılama ayarlarını etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="e81a1-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="e81a1-104">Bu makalede biz nasıl kullanabileceğinizi gösterir. bir [Azure Resource Manager şablonu](../azure-resource-manager/resource-group-authoring-templates.md) oluşturulduğunda bir kaynakta tanılama ayarlarını yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="e81a1-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) to configure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="e81a1-105">Bu, tanılama günlüklerini ve Event Hubs, bir depolama hesabında arşivleme veya bir kaynak oluşturulduğunda için günlük analizi göndererek ölçümlere akış otomatik olarak başlatılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e81a1-105">This enables you to automatically start streaming your Diagnostic Logs and metrics to Event Hubs, archiving them in a Storage Account, or sending them to Log Analytics when a resource is created.</span></span>

<span data-ttu-id="e81a1-106">Resource Manager şablonu kullanarak tanılama günlüklerini etkinleştirme yöntemi kaynak türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="e81a1-106">The method for enabling Diagnostic Logs using a Resource Manager template depends on the resource type.</span></span>

* <span data-ttu-id="e81a1-107">**İşlem olmayan** kaynakları (örneğin, ağ güvenlik grupları, Logic Apps Otomasyonu) kullanmak [tanılama bu makalede açıklanan ayarlarını](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="e81a1-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="e81a1-108">**İşlem** (WAD/LAD tabanlı) kaynakları kullanmak [WAD/LAD yapılandırma dosyasını bu makalede açıklanan](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="e81a1-108">**Compute** (WAD/LAD-based) resources use the [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="e81a1-109">Bu makalede her iki yöntemi kullanarak tanılama yapılandırma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e81a1-109">In this article we describe how to configure diagnostics using either method.</span></span>

<span data-ttu-id="e81a1-110">Temel adımlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="e81a1-110">The basic steps are as follows:</span></span>

1. <span data-ttu-id="e81a1-111">Bir şablonu kaynak oluşturmak ve tanılama etkinleştirmek nasıl açıklayan bir JSON dosyası olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e81a1-111">Create a template as a JSON file that describes how to create the resource and enable diagnostics.</span></span>
2. <span data-ttu-id="e81a1-112">[Herhangi bir dağıtım yöntemi kullanarak şablonu dağıtmak](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e81a1-112">[Deploy the template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="e81a1-113">Aşağıdaki işlem dışı ve işlem kaynakları için oluşturmak için gereken şablon JSON dosyası örneği sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="e81a1-113">Below we give an example of the template JSON file you need to generate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="e81a1-114">İşlem olmayan kaynak şablonu</span><span class="sxs-lookup"><span data-stu-id="e81a1-114">Non-Compute resource template</span></span>
<span data-ttu-id="e81a1-115">İşlem dışı kaynaklar için iki işlem yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e81a1-115">For non-Compute resources, you will need to do two things:</span></span>

1. <span data-ttu-id="e81a1-116">Depolama hesabı adı, hizmet veri yolu kural kimliği ve/veya OMS günlük analizi çalışma alanı kimliği (tanılama günlüklerini arşivleme Event hubs'a günlükler akış ve/veya günlükleri göndermek için günlük analizi depolama hesabında etkinleştirmek) için parametreleri blob parametreleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e81a1-116">Add parameters to the parameters blob for the storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs to Event Hubs, and/or sending logs to Log Analytics).</span></span>
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
      }
    }
    ```
2. <span data-ttu-id="e81a1-117">Tanılama günlüklerini etkinleştirmek istediğiniz kaynak kaynakları dizisinde bir kaynak türü ekleyin `[resource namespace]/providers/diagnosticSettings`.</span><span class="sxs-lookup"><span data-stu-id="e81a1-117">In the resources array of the resource for which you want to enable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
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

<span data-ttu-id="e81a1-118">Tanılama ayarını özellikleri blob izleyen [bu makalede açıklanan biçimde](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="e81a1-118">The properties blob for the Diagnostic Setting follows [the format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="e81a1-119">Ekleme `metrics` özelliği, sağlanan bu aynı çıktıları kaynak ölçümleri de göndermenizi etkinleştirecek [kaynak Azure İzleyici ölçümleri destekleyen](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="e81a1-119">Adding the `metrics` property will enable you to also send resource metrics to these same outputs, provided that [the resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="e81a1-120">Aşağıda, bir mantıksal uygulama oluşturan ve olay hub'ları ve depolama hesabındaki depolama akışı kapatır tam bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e81a1-120">Here is a full example that creates a Logic App and turns on streaming to Event Hubs and storage in a storage account.</span></span>

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
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

## <a name="compute-resource-template"></a><span data-ttu-id="e81a1-121">Kaynak şablonu işlem</span><span class="sxs-lookup"><span data-stu-id="e81a1-121">Compute resource template</span></span>
<span data-ttu-id="e81a1-122">İşlem kaynak üzerinde tanılamayı etkinleştirmek için örneğin bir sanal makine ya da Service Fabric kümesi, gerekir:</span><span class="sxs-lookup"><span data-stu-id="e81a1-122">To enable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="e81a1-123">Azure tanılama uzantısını VM kaynak tanımına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e81a1-123">Add the Azure Diagnostics extension to the VM resource definition.</span></span>
2. <span data-ttu-id="e81a1-124">Bir depolama hesabı ve/veya olay hub'ı bir parametre olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="e81a1-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="e81a1-125">WADCfg XML dosyasının içeriğini tüm XML karakterleri düzgün kaçış XMLCfg özelliği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e81a1-125">Add the contents of your WADCfg XML file into the XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="e81a1-126">Bu son adım sağ almak zor olabilir.</span><span class="sxs-lookup"><span data-stu-id="e81a1-126">This last step can be tricky to get right.</span></span> <span data-ttu-id="e81a1-127">[Bu makaleye bakın](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) tanılama yapılandırma şeması kaçışlı ve doğru biçimlendirilmiş değişkenleri böler bir örnek.</span><span class="sxs-lookup"><span data-stu-id="e81a1-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits the Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="e81a1-128">Örnekler dahil olmak üzere tüm işlem açıklanan [bu belgedeki](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e81a1-128">The entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e81a1-129">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="e81a1-129">Next Steps</span></span>
* [<span data-ttu-id="e81a1-130">Azure tanılama günlükleri hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="e81a1-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="e81a1-131">Akış olay hub'ları için Azure tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="e81a1-131">Stream Azure Diagnostic Logs to Event Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

