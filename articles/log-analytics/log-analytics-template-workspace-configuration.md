---
title: "aaaUse Azure Resource Manager şablonları tooCreate ve günlük analizi çalışma alanı yapılandırma | Microsoft Docs"
description: "Azure Resource Manager şablonları toocreate kullanın ve günlük analizi çalışma alanları yapılandırın."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: d21ca1b0-847d-4716-bb30-2a8c02a606aa
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: json
ms.topic: article
ms.date: 06/01/2017
ms.author: richrund
ms.openlocfilehash: c8f413e982f5eeed73f463524ff6f239f26c9127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-log-analytics-using-azure-resource-manager-templates"></a><span data-ttu-id="b762b-103">Günlük analizi Azure Resource Manager şablonları kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="b762b-103">Manage Log Analytics using Azure Resource Manager templates</span></span>
<span data-ttu-id="b762b-104">Kullanabileceğiniz [Azure Resource Manager şablonları](../azure-resource-manager/resource-group-authoring-templates.md) toocreate ve günlük analizi çalışma alanları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b762b-104">You can use [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) toocreate and configure Log Analytics workspaces.</span></span> <span data-ttu-id="b762b-105">Şablonları ile gerçekleştirebileceğiniz hello görevler örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b762b-105">Examples of hello tasks you can perform with templates include:</span></span>

* <span data-ttu-id="b762b-106">Çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b762b-106">Create a workspace</span></span>
* <span data-ttu-id="b762b-107">Bir çözüm Ekle</span><span class="sxs-lookup"><span data-stu-id="b762b-107">Add a solution</span></span>
* <span data-ttu-id="b762b-108">Kaydedilen Aramalar oluşturun</span><span class="sxs-lookup"><span data-stu-id="b762b-108">Create saved searches</span></span>
* <span data-ttu-id="b762b-109">Bir bilgisayar grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="b762b-109">Create a computer group</span></span>
* <span data-ttu-id="b762b-110">Merhaba Windows aracısının yüklü olduğu IIS günlüklerinin bilgisayarlardan toplamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="b762b-110">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
* <span data-ttu-id="b762b-111">Linux ve Windows bilgisayarlarından performans sayaçlarını Topla</span><span class="sxs-lookup"><span data-stu-id="b762b-111">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="b762b-112">Linux bilgisayarlarda syslog olaylarını Topla</span><span class="sxs-lookup"><span data-stu-id="b762b-112">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="b762b-113">Windows olay günlüklerini olaylarını Topla</span><span class="sxs-lookup"><span data-stu-id="b762b-113">Collect events from Windows event logs</span></span>
* <span data-ttu-id="b762b-114">Özel olay günlüklerini toplayın</span><span class="sxs-lookup"><span data-stu-id="b762b-114">Collect custom event logs</span></span>
* <span data-ttu-id="b762b-115">Merhaba günlük analizi aracı tooan Azure sanal makine ekleyin</span><span class="sxs-lookup"><span data-stu-id="b762b-115">Add hello log analytics agent tooan Azure virtual machine</span></span>
* <span data-ttu-id="b762b-116">Günlük analizi tooindex verileri Azure Tanılama'yı kullanarak toplanan yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b762b-116">Configure log analytics tooindex data collected using Azure diagnostics</span></span>

<span data-ttu-id="b762b-117">Bu makalede bir şablon bazı şablonlardan gerçekleştirebilirsiniz hello yapılandırmasının göstermek örnekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b762b-117">This article provides a template samples that illustrate some of hello configuration that you can perform from templates.</span></span>

## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="b762b-118">Oluşturma ve yapılandırma günlük analizi çalışma alanı</span><span class="sxs-lookup"><span data-stu-id="b762b-118">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="b762b-119">Merhaba aşağıdaki şablon örneği gösterilmektedir nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="b762b-119">hello following template sample illustrates how to:</span></span>

1. <span data-ttu-id="b762b-120">Ayar veri saklama dahil olmak üzere bir çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b762b-120">Create a workspace, including setting data retention</span></span>
2. <span data-ttu-id="b762b-121">Çözümleri toohello çalışma Ekle</span><span class="sxs-lookup"><span data-stu-id="b762b-121">Add solutions toohello workspace</span></span>
3. <span data-ttu-id="b762b-122">Kaydedilen Aramalar oluşturun</span><span class="sxs-lookup"><span data-stu-id="b762b-122">Create saved searches</span></span>
4. <span data-ttu-id="b762b-123">Bir bilgisayar grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="b762b-123">Create a computer group</span></span>
5. <span data-ttu-id="b762b-124">Merhaba Windows aracısının yüklü olduğu IIS günlüklerinin bilgisayarlardan toplamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="b762b-124">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
6. <span data-ttu-id="b762b-125">Mantıksal Disk performans sayaçlarını Linux bilgisayarından toplar (% kullanılan Inode; Boş megabayt; % Kullanılan alan; Disk aktarımı/sn; Disk Okuma/sn; Disk Yazma/sn)</span><span class="sxs-lookup"><span data-stu-id="b762b-125">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
7. <span data-ttu-id="b762b-126">Linux bilgisayarlardan Syslog olaylarını Topla</span><span class="sxs-lookup"><span data-stu-id="b762b-126">Collect syslog events from Linux computers</span></span>
8. <span data-ttu-id="b762b-127">Merhaba uygulama olay günlüğüne Windows bilgisayarlardan hata ve uyarı olayları toplar</span><span class="sxs-lookup"><span data-stu-id="b762b-127">Collect Error and Warning events from hello Application Event Log from Windows computers</span></span>
9. <span data-ttu-id="b762b-128">Windows bilgisayarlardan bellek kullanılabilir MBayt performans sayacı Topla</span><span class="sxs-lookup"><span data-stu-id="b762b-128">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
10. <span data-ttu-id="b762b-129">Özel günlük Topla</span><span class="sxs-lookup"><span data-stu-id="b762b-129">Collect a custom log</span></span> 
11. <span data-ttu-id="b762b-130">IIS ve Windows olay günlükleri Azure tanılama tooa depolama hesabı tarafından yazılmış Topla</span><span class="sxs-lookup"><span data-stu-id="b762b-130">Collect IIS logs and Windows Event logs written by Azure diagnostics tooa storage account</span></span>

```
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "workspaceName": {
      "type": "string",
      "metadata": {
        "description": "workspaceName"
      }
    },
    "serviceTier": {
      "type": "string",
      "allowedValues": [
        "Free",
        "Standalone",
        "PerNode"
      ],
      "metadata": {
        "description": "Service Tier: Free, Standalone, or PerNode"
    }
      },
    "dataRetention": {
      "type": "int",
      "defaultValue": 30,
      "minValue": 7,
      "maxValue": 730,
      "metadata": {
        "description": "Number of days of retention. Free plans can only have 7 days, Standalone and OMS plans include 30 days for free"
      }
    },
    "location": {
      "type": "string",
      "allowedValues": [
        "East US",
        "West Europe",
        "Southeast Asia",
        "Australia Southeast"
      ]
    },
    "applicationDiagnosticsStorageAccountName": {
        "type": "string",
        "metadata": {
          "description": "Name of hello storage account with Azure diagnostics output"
        }
    },
    "applicationDiagnosticsStorageAccountResourceGroup": {
        "type": "string",
        "metadata": {
          "description": "hello resource group name containing hello storage account with Azure diagnostics output"
        }
    }
  },
  "variables": {
    "Updates": {
      "Name": "[Concat('Updates', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "Updates"
    },
    "AntiMalware": {
      "Name": "[concat('AntiMalware', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "AntiMalware"
    },
    "SQLAssessment": {
      "Name": "[Concat('SQLAssessment', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "SQLAssessment"
    },
    "diagnosticsStorageAccount": "[resourceId(parameters('applicationDiagnosticsStorageAccountResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName'))]"
  },
  "resources": [
    {
      "apiVersion": "2015-11-01-preview",
      "type": "Microsoft.OperationalInsights/workspaces",
      "name": "[parameters('workspaceName')]",
      "location": "[parameters('location')]",
      "properties": {
        "sku": {
          "Name": "[parameters('serviceTier')]"
        },
    "retention": "[parameters('dataRetention')]"
      },
      "resources": [
        {
          "apiVersion": "2015-11-01-preview",
          "name": "VMSS Queries2",
          "type": "savedSearches",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "Category": "VMSS",
            "ETag": "*",
            "DisplayName": "VMSS Instance Count",
            "Query": "Type:Event Source=ServiceFabricNodeBootstrapAgent | dedup Computer | measure count () by Computer",
            "Version": 1
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleWindowsEvent1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "WindowsEvent",
          "properties": {
            "eventLogName": "Application",
            "eventTypes": [
              {
                "eventType": "Error"
              },
              {
                "eventType": "Warning"
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleWindowsPerfCounter1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "WindowsPerformanceCounter",
          "properties": {
            "objectName": "Memory",
            "instanceName": "*",
            "intervalSeconds": 10,
            "counterName": "Available MBytes"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleIISLog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "IISLogs",
          "properties": {
            "state": "OnPremiseEnabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleSyslog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxSyslog",
          "properties": {
            "syslogName": "kern",
            "syslogSeverities": [
              {
                "severity": "emerg"
              },
              {
                "severity": "alert"
              },
              {
                "severity": "crit"
              },
              {
                "severity": "err"
              },
              {
                "severity": "warning"
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleSyslogCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxSyslogCollection",
          "properties": {
            "state": "Enabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleLinuxPerf1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxPerformanceObject",
          "properties": {
            "performanceCounters": [
              {
                "counterName": "% Used Inodes"
              },
              {
                "counterName": "Free Megabytes"
              },
              {
                "counterName": "% Used Space"
              },
              {
                "counterName": "Disk Transfers/sec"
              },
              {
                "counterName": "Disk Reads/sec"
              },
              {
                "counterName": "Disk Writes/sec"
              }
            ],
            "objectName": "Logical Disk",
            "instanceName": "*",
            "intervalSeconds": 10
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleLinuxPerfCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxPerformanceCollection",
          "properties": {
            "state": "Enabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleCustomLog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "CustomLog",
          "properties": {
            "customLogName": "sampleCustomLog1",
            "description": "test custom log datasources",
            "inputs": [
              {
                "location": {
                  "fileSystemLocations": {
                    "windowsFileTypeLogPaths": [ "e:\\iis5\\*.log" ],
                    "linuxFileTypeLogPaths": [ "/var/logs" ]
                  }
                },
                "recordDelimiter": {
                  "regexDelimiter": {
                    "pattern": "\\n",
                    "matchIndex": 0,
                    "matchIndexSpecified": true,
                    "numberedGroup": null
                  }
                }
              }
            ],
            "extractions": [
              {
                "extractionName": "TimeGenerated",
                "extractionType": "DateTime",
                "extractionProperties": {
                  "dateTimeExtraction": {
                    "regex": null,
                    "joinStringRegex": null
                  }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleCustomLogCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "CustomLogCollection",
          "properties": {
            "state": "LinuxLogsEnabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "name": "[concat(parameters('applicationDiagnosticsStorageAccountName'),parameters('workspaceName'))]",
          "type": "storageinsightconfigs",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "containers": [ 
              "wad-iis-logfiles" 
            ],
            "tables": [
              "WADWindowsEventLogsTable"
            ],
            "storageAccount": {
              "id": "[variables('diagnosticsStorageAccount')]",
              "key": "[listKeys(variables('diagnosticsStorageAccount'),'2015-06-15').key1]"
            }
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('Updates').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('Updates').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('Updates').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('Updates').GalleryName)]",
            "promotionCode": ""
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('AntiMalware').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('AntiMalware').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('AntiMalware').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('AntiMalware').GalleryName)]",
            "promotionCode": ""
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('SQLAssessment').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('SQLAssessment').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('SQLAssessment').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('SQLAssessment').GalleryName)]",
            "promotionCode": ""
          }
        }
      ]
    }
  ],
  "outputs": {
    "workspaceOutput": {
      "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-11-01-preview')]",
      "type": "object"
    }
  }
}

```
### <a name="deploying-hello-sample-template"></a><span data-ttu-id="b762b-131">Merhaba örnek şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="b762b-131">Deploying hello sample template</span></span>
<span data-ttu-id="b762b-132">toodeploy hello örnek şablonu:</span><span class="sxs-lookup"><span data-stu-id="b762b-132">toodeploy hello sample template:</span></span>

1. <span data-ttu-id="b762b-133">Örneğin bir dosyada Hello ekli örnek kaydedin`azuredeploy.json`</span><span class="sxs-lookup"><span data-stu-id="b762b-133">Save hello attached sample in a file, for example `azuredeploy.json`</span></span> 
2. <span data-ttu-id="b762b-134">İstediğiniz hello şablonu toohave hello yapılandırmasını düzenle</span><span class="sxs-lookup"><span data-stu-id="b762b-134">Edit hello template toohave hello configuration you want</span></span>
3. <span data-ttu-id="b762b-135">PowerShell veya hello komut satırı toodeploy hello şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="b762b-135">Use PowerShell or hello command line toodeploy hello template</span></span>

#### <a name="powershell"></a><span data-ttu-id="b762b-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b762b-136">PowerShell</span></span>
`New-AzureRmResourceGroupDeployment -Name <deployment-name> -ResourceGroupName <resource-group-name> -TemplateFile azuredeploy.json`

#### <a name="command-line"></a><span data-ttu-id="b762b-137">Komut satırı</span><span class="sxs-lookup"><span data-stu-id="b762b-137">Command line</span></span>
```
azure config mode arm
azure group deployment create <my-resource-group> <my-deployment-name> --TemplateFile azuredeploy.json
```


## <a name="example-resource-manager-templates"></a><span data-ttu-id="b762b-138">Örnek Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="b762b-138">Example Resource Manager templates</span></span>
<span data-ttu-id="b762b-139">Hello Azure hızlı başlangıç Şablon Galerisi dahil olmak üzere günlük analizi için çeşitli şablonlar içerir:</span><span class="sxs-lookup"><span data-stu-id="b762b-139">hello Azure quickstart template gallery includes several templates for Log Analytics, including:</span></span>

* [<span data-ttu-id="b762b-140">Windows hello günlük analizi VM uzantısı ile çalışan bir sanal makine dağıtma</span><span class="sxs-lookup"><span data-stu-id="b762b-140">Deploy a virtual machine running Windows with hello Log Analytics VM extension</span></span>](https://azure.microsoft.com/documentation/templates/201-oms-extension-windows-vm/)
* [<span data-ttu-id="b762b-141">Günlük analizi VM uzantısı hello ile Linux çalıştıran bir sanal makine dağıtma</span><span class="sxs-lookup"><span data-stu-id="b762b-141">Deploy a virtual machine running Linux with hello Log Analytics VM extension</span></span>](https://azure.microsoft.com/documentation/templates/201-oms-extension-ubuntu-vm/)
* [<span data-ttu-id="b762b-142">Azure Site Recovery varolan bir günlük analizi çalışma alanını kullanarak izleme</span><span class="sxs-lookup"><span data-stu-id="b762b-142">Monitor Azure Site Recovery using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/asr-oms-monitoring/)
* [<span data-ttu-id="b762b-143">Varolan bir günlük analizi çalışma alanını kullanarak Azure Web uygulamaları İzle</span><span class="sxs-lookup"><span data-stu-id="b762b-143">Monitor Azure Web Apps using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/101-webappazure-oms-monitoring/)
* [<span data-ttu-id="b762b-144">SQL Azure varolan bir günlük analizi çalışma alanını kullanarak izleme</span><span class="sxs-lookup"><span data-stu-id="b762b-144">Monitor SQL Azure using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/101-sqlazure-oms-monitoring/)
* [<span data-ttu-id="b762b-145">Service Fabric kümesi dağıtma ve var olan bir günlük analizi çalışma ile izleme</span><span class="sxs-lookup"><span data-stu-id="b762b-145">Deploy a Service Fabric cluster and monitor it with an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/service-fabric-oms/)
* [<span data-ttu-id="b762b-146">Service Fabric kümesi dağıtma ve günlük analizi çalışma alanı toomonitor oluşturun,</span><span class="sxs-lookup"><span data-stu-id="b762b-146">Deploy a Service Fabric cluster and create a Log Analytics workspace toomonitor it</span></span>](https://azure.microsoft.com/documentation/templates/service-fabric-vmss-oms/)

## <a name="next-steps"></a><span data-ttu-id="b762b-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b762b-147">Next steps</span></span>
* [<span data-ttu-id="b762b-148">Azure Resource Manager şablonları kullanarak VM'ler aracılar dağıtma</span><span class="sxs-lookup"><span data-stu-id="b762b-148">Deploy agents into Azure VMs using Resource Manager templates</span></span>](log-analytics-azure-vm-extension.md)

