---
title: "Bir Linux ölçek kümesi şablonunda Konuk ölçümlerle Azure otomatik ölçeklendirme kullanın | Microsoft Docs"
description: "Bilgi nasıl Linux sanal makine ölçek kümesi bir şablonda Konuk ölçümleri kullanarak tooautoscale"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: na
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: negat
ms.openlocfilehash: 7afbef943a5f15c7a72dcf7114f46d521c504424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a><span data-ttu-id="fb92d-103">Bir Linux ölçek kümesi şablonunda Konuk ölçümleri kullanarak otomatik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="fb92d-103">Autoscale using guest metrics in a Linux scale set template</span></span>

<span data-ttu-id="fb92d-104">Azure VM'lerin toplanır ve ölçek kümeleri ölçümlerini iki tür vardır: bazı gelen hello VM ana bilgisayar ve diğerleri hello Konuk sanal gelir.</span><span class="sxs-lookup"><span data-stu-id="fb92d-104">There are two types of metrics in Azure that are gathered from VMs and scale sets: some come from hello host VM and others come from hello guest VM.</span></span> <span data-ttu-id="fb92d-105">Ana ölçümleri gerektirmez ek kurulum hello ana bilgisayar VM tarafından toplanan çünkü Konuk ölçümleri bize tooinstall hello gerektirdiğinde [Windows Azure tanılama uzantısını](../virtual-machines/windows/extensions-diagnostics-template.md) veya hello [Linux Azure tanılama Uzantı](../virtual-machines/linux/diagnostic-extension.md) hello VM konuk.</span><span class="sxs-lookup"><span data-stu-id="fb92d-105">Host metrics do not require additional setup because they are collected by hello host VM, whereas guest metrics require us tooinstall hello [Windows Azure Diagnostics extension](../virtual-machines/windows/extensions-diagnostics-template.md) or hello [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) in hello guest VM.</span></span> <span data-ttu-id="fb92d-106">Bir ortak neden toouse Konuk ölçümleri ana ölçümleri yerine Konuk ölçümleri ölçümleri ana ölçümleri daha büyük seçimi sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="fb92d-106">One common reason toouse guest metrics instead of host metrics is that guest metrics provide a larger selection of metrics than host metrics.</span></span> <span data-ttu-id="fb92d-107">Böyle bir yalnızca konuk ölçümleri kullanılabilir bellek tüketimi ölçümlerini örnektir.</span><span class="sxs-lookup"><span data-stu-id="fb92d-107">One such example is memory-consumption metrics, which are only available via guest metrics.</span></span> <span data-ttu-id="fb92d-108">desteklenen hello ana ölçümleri listelenen [burada](../monitoring-and-diagnostics/monitoring-supported-metrics.md), ve yaygın olarak kullanılan Konuk ölçümleri listelenen [burada](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="fb92d-108">hello supported host metrics are listed [here](../monitoring-and-diagnostics/monitoring-supported-metrics.md), and commonly used guest metrics are listed [here](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span> <span data-ttu-id="fb92d-109">Bu makalede gösterilmektedir nasıl toomodify hello [minimum uygun ölçek kümesi şablonu](./virtual-machine-scale-sets-mvss-start.md) toouse otomatik ölçeklendirme kurallarını temel alarak Linux ölçek kümeleri için konuk ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="fb92d-109">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toouse autoscale rules based on guest metrics for Linux scale sets.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="fb92d-110">Merhaba şablon tanımını değiştirin</span><span class="sxs-lookup"><span data-stu-id="fb92d-110">Change hello template definition</span></span>

<span data-ttu-id="fb92d-111">Bizim minimum uygun ölçek kümesi şablon görülebilir [burada](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), ve hello Linux ölçeği konuk tabanlı otomatik ölçeklendirme ile Ayarla dağıtmak için bizim şablon görülebilir [burada](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="fb92d-111">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello Linux scale set with guest-based autoscale can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span></span> <span data-ttu-id="fb92d-112">Merhaba kullanılan fark toocreate bu şablonu inceleyelim (`git diff minimum-viable-scale-set existing-vnet`) tarafından parça parça:</span><span class="sxs-lookup"><span data-stu-id="fb92d-112">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="fb92d-113">Parametreler için ilk olarak, eklediğimiz `storageAccountName` ve `storageAccountSasToken`.</span><span class="sxs-lookup"><span data-stu-id="fb92d-113">First, we add parameters for `storageAccountName` and `storageAccountSasToken`.</span></span> <span data-ttu-id="fb92d-114">Merhaba Tanılama Aracı ölçüm verileri depolar bir [tablo](../cosmos-db/table-storage-how-to-use-dotnet.md) bu depolama hesabında.</span><span class="sxs-lookup"><span data-stu-id="fb92d-114">hello diagnostics agent will store metric data in a [table](../cosmos-db/table-storage-how-to-use-dotnet.md) in this storage account.</span></span> <span data-ttu-id="fb92d-115">Hello Linux Tanılama Aracı sürüm 3.0 sürümünden itibaren bir depolama erişim tuşunu kullanarak artık desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="fb92d-115">As of hello Linux Diagnostics Agent version 3.0, using a storage access key is no longer supported.</span></span> <span data-ttu-id="fb92d-116">Biz kullanmalısınız bir [SAS belirteci](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="fb92d-116">We must use a [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "storageAccountName": {
+      "type": "string"
+    },
+    "storageAccountSasToken": {
+      "type": "securestring"
     }
   },
```

<span data-ttu-id="fb92d-117">Ardından, biz hello ölçek kümesini değiştirme `extensionProfile` tooinclude hello tanılama uzantısını.</span><span class="sxs-lookup"><span data-stu-id="fb92d-117">Next, we modify hello scale set `extensionProfile` tooinclude hello diagnostics extension.</span></span> <span data-ttu-id="fb92d-118">Bu yapılandırmada, biz toocollect ölçümleri kimliği hello ölçek kümesi hello kaynağı belirtin, aynı zamanda depolama hesabı ve SAS belirteci toouse toostore hello ölçümleri hello.</span><span class="sxs-lookup"><span data-stu-id="fb92d-118">In this configuration, we specify hello resource ID of hello scale set toocollect metrics from, as well as hello storage account and SAS token toouse toostore hello metrics.</span></span> <span data-ttu-id="fb92d-119">Biz de hello ölçümleri (Bu durumda dakikada) ne sıklıkta toplanır ve hangi ölçümleri tootrack (bellekte bu servis talebi yüzde kullanılan) belirtin.</span><span class="sxs-lookup"><span data-stu-id="fb92d-119">We also specify how frequently hello metrics are aggregated (in this case every minute) and which metrics tootrack (in this case percent used memory).</span></span> <span data-ttu-id="fb92d-120">Bu yapılandırma hakkında daha ayrıntılı bilgi ve ölçümleri yüzde dışında kullanılan bellek için bkz: [bu belgeleri](../virtual-machines/linux/diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="fb92d-120">For more detailed information on this configuration and metrics other than percent used memory, see [this documentation](../virtual-machines/linux/diagnostic-extension.md).</span></span>

```diff
                 }
               }
             ]
+          },
+          "extensionProfile": {
+            "extensions": [
+              {
+                "name": "LinuxDiagnosticExtension",
+                "properties": {
+                  "publisher": "Microsoft.Azure.Diagnostics",
+                  "type": "LinuxDiagnostic",
+                  "typeHandlerVersion": "3.0",
+                  "settings": {
+                    "StorageAccount": "[parameters('storageAccountName')]",
+                    "ladCfg": {
+                      "diagnosticMonitorConfiguration": {
+                        "performanceCounters": {
+                          "sinks": "WADMetricJsonBlob",
+                          "performanceCounterConfiguration": [
+                            {
+                              "unit": "percent",
+                              "type": "builtin",
+                              "class": "memory",
+                              "counter": "percentUsedMemory",
+                              "counterSpecifier": "/builtin/memory/percentUsedMemory",
+                              "condition": "IsAggregate=TRUE"
+                            }
+                          ]
+                        },
+                        "metrics": {
+                          "metricAggregation": [
+                            {
+                              "scheduledTransferPeriod": "PT1M"
+                            }
+                          ],
+                          "resourceId": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]"
+                        }
+                      }
+                    }
+                  },
+                  "protectedSettings": {
+                    "storageAccountName": "[parameters('storageAccountName')]",
+                    "storageAccountSasToken": "[parameters('storageAccountSasToken')]",
+                    "sinksConfig": {
+                      "sink": [
+                        {
+                          "name": "WADMetricJsonBlob",
+                          "type": "JsonBlob"
+                        }
+                      ]
+                    }
+                  }
+                }
+              }
+            ]
           }
         }
       }
```

<span data-ttu-id="fb92d-121">Son olarak, eklediğimiz bir `autoscaleSettings` kaynak tooconfigure otomatik ölçeklendirme dayalı bu ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="fb92d-121">Finally, we add an `autoscaleSettings` resource tooconfigure autoscale based on these metrics.</span></span> <span data-ttu-id="fb92d-122">Bu kaynak bir `dependsOn` hello ölçek başvuran yan tümcesi hello ölçek kümesini tooautoscale denemeden önce mevcut tooensure ayarlamak.</span><span class="sxs-lookup"><span data-stu-id="fb92d-122">This resource has a `dependsOn` clause that references hello scale set tooensure that hello scale set exists before attempting tooautoscale it.</span></span> <span data-ttu-id="fb92d-123">Biz üzerinde farklı ölçüm tooautoscale seçerseniz, hello kullanmanız `counterSpecifier` hello tanılama uzantısını yapılandırmadan hello olarak `metricName` hello otomatik ölçeklendirme yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="fb92d-123">If we choose a different metric tooautoscale on, we would use hello `counterSpecifier` from hello diagnostics extension configuration as hello `metricName` in hello autoscale configuration.</span></span> <span data-ttu-id="fb92d-124">Merhaba otomatik ölçeklendirme yapılandırma hakkında daha fazla bilgi için bkz: [otomatik ölçeklendirme en iyi yöntemler](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) ve hello [Azure İzleyici REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="fb92d-124">For more information on autoscale configuration, see hello [autoscale best practices](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) and hello [Azure Monitor REST API reference documentation](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span></span>

```diff
+    },
+    {
+      "type": "Microsoft.Insights/autoscaleSettings",
+      "apiVersion": "2015-04-01",
+      "name": "guestMetricsAutoscale",
+      "location": "[resourceGroup().location]",
+      "dependsOn": [
+        "Microsoft.Compute/virtualMachineScaleSets/myScaleSet"
+      ],
+      "properties": {
+        "name": "guestMetricsAutoscale",
+        "targetResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+        "enabled": true,
+        "profiles": [
+          {
+            "name": "Profile1",
+            "capacity": {
+              "minimum": "1",
+              "maximum": "10",
+              "default": "3"
+            },
+            "rules": [
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "GreaterThan",
+                  "threshold": 60
+                },
+                "scaleAction": {
+                  "direction": "Increase",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              },
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "LessThan",
+                  "threshold": 30
+                },
+                "scaleAction": {
+                  "direction": "Decrease",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              }
+            ]
+          }
+        ]
+      }
     }
   ]
 }
```





## <a name="next-steps"></a><span data-ttu-id="fb92d-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fb92d-125">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
