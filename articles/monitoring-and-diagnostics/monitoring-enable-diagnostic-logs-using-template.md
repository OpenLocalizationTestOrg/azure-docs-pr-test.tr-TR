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
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a>Resource Manager şablonu kullanarak kaynak oluşturma sırasında otomatik olarak tanılama ayarlarını etkinleştirin
Bu makalede biz nasıl kullanabileceğinizi gösterir. bir [Azure Resource Manager şablonu](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure tanılama ayarlarını oluşturulduğunda kaynak üzerinde. Bu, tanılama günlüklerini ve ölçümleri tooEvent bir depolama hesabında arşivleme veya bir kaynak oluşturulduğunda tooLog Analytics göndererek hub akış tooautomatically başlangıç sağlar.

Tanılama günlüklerini Resource Manager şablonu kullanarak etkinleştirmek için hello yöntemi hello kaynak türüne bağlıdır.

* **İşlem olmayan** kaynakları (örneğin, ağ güvenlik grupları, Logic Apps Otomasyonu) kullanmak [tanılama bu makalede açıklanan ayarlarını](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).
* **İşlem** (WAD/LAD tabanlı) kaynakları hello kullan [WAD/LAD yapılandırma dosyasını bu makalede açıklanan](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).

Biz bu makalede açıklamak nasıl her iki yöntemi kullanarak tooconfigure tanılama.

Merhaba temel adımlar aşağıdaki gibidir:

1. Bir şablonu nasıl toocreate kaynak hello ve tanılamayı etkinleştirin açıklayan bir JSON dosyası olarak oluşturun.
2. [Herhangi bir dağıtım yöntemi kullanarak hello şablonu dağıtmak](../azure-resource-manager/resource-group-template-deploy.md).

Aşağıda hello şablonu toogenerate işlem dışı ve işlem kaynakları için gereksinim duyduğunuz JSON dosyası örneği sunuyoruz.

## <a name="non-compute-resource-template"></a>İşlem olmayan kaynak şablonu
İşlem olmayan kaynakları toodo iki şey gerekir:

1. Parametreleri toohello parametreleri blob hello depolama hesabı adı, hizmet veri yolu kural kimliği ve/veya OMS günlük analizi çalışma alanı kimliği (günlükleri tooEvent Hubs akış ve/veya günlükleri tooLog Analytics gönderme depolama hesabı, tanılama günlüklerini arşivleme etkinleştirmek) ekleyin.
   
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
2. Hello kaynakları dizisinde tooenable tanılama günlüklerini istediğiniz hello kaynağının, bir kaynak türü eklemek `[resource namespace]/providers/diagnosticSettings`.
   
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

Merhaba hello tanılama ayarını için özellikler blob izleyen [bu makalede açıklanan hello biçimi](https://msdn.microsoft.com/library/azure/dn931931.aspx). Ekleme hello `metrics` özelliğini etkinleştirir, aynı çıkarır, sağlanan, tooalso gönderme kaynak ölçümleri toothese [hello kaynak destekleyen Azure İzleyici ölçümleri](monitoring-supported-metrics.md).

Aşağıda, bir mantıksal uygulama oluşturan ve akış tooEvent hub'lar ve bir depolama hesabındaki depolama kapatır tam bir örnek verilmiştir.

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

## <a name="compute-resource-template"></a>Kaynak şablonu işlem
Örneğin bir sanal makine veya Service Fabric kümesi, bir işlem kaynağına tooenable tanılama şunları yapmanız gerekir:

1. Hello Azure tanılama uzantısını toohello VM kaynak tanımını ekleyin.
2. Bir depolama hesabı ve/veya olay hub'ı bir parametre olarak belirtin.
3. WADCfg XML dosyanızı Merhaba içeriğine tüm XML karakterleri düzgün kaçış hello XMLCfg özelliğinin içine ekleyin.

> [!WARNING]
> Bu son adım, hassas tooget sağ olabilir. [Bu makaleye bakın](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) bölmelerini kaçışlı ve doğru biçimlendirilmiş değişkenleri tanılama yapılandırma şeması hello bir örnek.
> 
> 

Merhaba, örnekler dahil olmak üzere tüm işlem açıklanan [bu belgedeki](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-steps"></a>Sonraki Adımlar
* [Azure tanılama günlükleri hakkında daha fazla bilgi](monitoring-overview-of-diagnostic-logs.md)
* [Akış Azure tanılama günlükleri tooEvent hub'lar](monitoring-stream-diagnostic-logs-to-event-hubs.md)

