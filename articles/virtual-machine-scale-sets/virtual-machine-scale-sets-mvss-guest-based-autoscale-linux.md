---
title: "Bir Linux ölçek kümesi şablonunda Konuk ölçümlerle Azure otomatik ölçeklendirme kullanın | Microsoft Docs"
description: "Bilgi Linux sanal makine ölçek kümesi bir şablonda Konuk ölçümleri kullanarak otomatik ölçeklendirme yapma"
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
ms.openlocfilehash: ac0bbb4dbfccca3f3fc31526aeff11afe55d44be
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a><span data-ttu-id="88951-103">Bir Linux ölçek kümesi şablonunda Konuk ölçümleri kullanarak otomatik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="88951-103">Autoscale using guest metrics in a Linux scale set template</span></span>

<span data-ttu-id="88951-104">Azure VM'lerin toplanır ve ölçek kümeleri ölçümlerini iki tür vardır: bazı VM ana bilgisayardan gelen ve diğer Konuk sanal gelir.</span><span class="sxs-lookup"><span data-stu-id="88951-104">There are two types of metrics in Azure that are gathered from VMs and scale sets: some come from the host VM and others come from the guest VM.</span></span> <span data-ttu-id="88951-105">Ana ölçümleri gerektirmez ek Kurulum VM, ana bilgisayar tarafından toplanan çünkü Konuk ölçümleri bize yüklemek gerektirdiğinde [Windows Azure tanılama uzantısını](../virtual-machines/windows/extensions-diagnostics-template.md) veya [Linux Azure tanılama uzantısını](../virtual-machines/linux/diagnostic-extension.md) VM konuk.</span><span class="sxs-lookup"><span data-stu-id="88951-105">Host metrics do not require additional setup because they are collected by the host VM, whereas guest metrics require us to install the [Windows Azure Diagnostics extension](../virtual-machines/windows/extensions-diagnostics-template.md) or the [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) in the guest VM.</span></span> <span data-ttu-id="88951-106">Konuk ölçümleri yerine ana ölçümleri kullanmak için bir ortak neden Konuk ölçümleri ölçümleri ana ölçümleri daha büyük seçimi sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="88951-106">One common reason to use guest metrics instead of host metrics is that guest metrics provide a larger selection of metrics than host metrics.</span></span> <span data-ttu-id="88951-107">Böyle bir yalnızca konuk ölçümleri kullanılabilir bellek tüketimi ölçümlerini örnektir.</span><span class="sxs-lookup"><span data-stu-id="88951-107">One such example is memory-consumption metrics, which are only available via guest metrics.</span></span> <span data-ttu-id="88951-108">Desteklenen ana ölçümleri listelenen [burada](../monitoring-and-diagnostics/monitoring-supported-metrics.md), ve yaygın olarak kullanılan Konuk ölçümleri listelenen [burada](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="88951-108">The supported host metrics are listed [here](../monitoring-and-diagnostics/monitoring-supported-metrics.md), and commonly used guest metrics are listed [here](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span> <span data-ttu-id="88951-109">Bu makalede nasıl değiştirileceğini gösterir [minimum uygun ölçek kümesi şablonu](./virtual-machine-scale-sets-mvss-start.md) Linux ölçek kümeleri için konuk ölçümleri göre otomatik ölçeklendirme kurallarını kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="88951-109">This article shows how to modify the [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) to use autoscale rules based on guest metrics for Linux scale sets.</span></span>

## <a name="change-the-template-definition"></a><span data-ttu-id="88951-110">Şablon tanımını değiştirin</span><span class="sxs-lookup"><span data-stu-id="88951-110">Change the template definition</span></span>

<span data-ttu-id="88951-111">Bizim minimum uygun ölçek kümesi şablon görülebilir [burada](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), ve Linux ölçek dağıtma ile konuk tabanlı otomatik ölçeklendirme kümesi için bizim şablon görülebilir [burada](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="88951-111">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying the Linux scale set with guest-based autoscale can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span></span> <span data-ttu-id="88951-112">Bu şablon oluşturmak için kullanılan fark inceleyelim (`git diff minimum-viable-scale-set existing-vnet`) tarafından parça parça:</span><span class="sxs-lookup"><span data-stu-id="88951-112">Let's examine the diff used to create this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="88951-113">Parametreler için ilk olarak, eklediğimiz `storageAccountName` ve `storageAccountSasToken`.</span><span class="sxs-lookup"><span data-stu-id="88951-113">First, we add parameters for `storageAccountName` and `storageAccountSasToken`.</span></span> <span data-ttu-id="88951-114">Tanılama Aracı ölçüm verileri depolayacak bir [tablo](../cosmos-db/table-storage-how-to-use-dotnet.md) bu depolama hesabında.</span><span class="sxs-lookup"><span data-stu-id="88951-114">The diagnostics agent will store metric data in a [table](../cosmos-db/table-storage-how-to-use-dotnet.md) in this storage account.</span></span> <span data-ttu-id="88951-115">Linux Tanılama Aracı sürüm 3.0 sürümünden itibaren bir depolama erişim tuşunu kullanarak artık desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="88951-115">As of the Linux Diagnostics Agent version 3.0, using a storage access key is no longer supported.</span></span> <span data-ttu-id="88951-116">Biz kullanmalısınız bir [SAS belirteci](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="88951-116">We must use a [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

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

<span data-ttu-id="88951-117">Ardından, biz ölçek kümesini değiştirme `extensionProfile` tanılama uzantısını eklenecek.</span><span class="sxs-lookup"><span data-stu-id="88951-117">Next, we modify the scale set `extensionProfile` to include the diagnostics extension.</span></span> <span data-ttu-id="88951-118">Bu yapılandırmada, ölçümleri depolamak için kullanmak üzere, ölçümleri yanı sıra depolama hesabı ve SAS belirteci toplamak için ölçek kaynak Kimliğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="88951-118">In this configuration, we specify the resource ID of the scale set to collect metrics from, as well as the storage account and SAS token to use to store the metrics.</span></span> <span data-ttu-id="88951-119">Biz de ölçümleri (Bu durumda dakikada) ne sıklıkta toplanır ve (Bu örnek yüzde kullanılan bellek) izlemek için hangi ölçümleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="88951-119">We also specify how frequently the metrics are aggregated (in this case every minute) and which metrics to track (in this case percent used memory).</span></span> <span data-ttu-id="88951-120">Bu yapılandırma hakkında daha ayrıntılı bilgi ve ölçümleri yüzde dışında kullanılan bellek için bkz: [bu belgeleri](../virtual-machines/linux/diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="88951-120">For more detailed information on this configuration and metrics other than percent used memory, see [this documentation](../virtual-machines/linux/diagnostic-extension.md).</span></span>

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

<span data-ttu-id="88951-121">Son olarak, eklediğimiz bir `autoscaleSettings` otomatik ölçeklendirme yapılandırmak için kaynak tabanlı bu ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="88951-121">Finally, we add an `autoscaleSettings` resource to configure autoscale based on these metrics.</span></span> <span data-ttu-id="88951-122">Bu kaynak bir `dependsOn` ölçek başvuran yan tümcesi ayarlanmış ölçek kümesi için otomatik ölçeklendirme, denemeden önce mevcut olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="88951-122">This resource has a `dependsOn` clause that references the scale set to ensure that the scale set exists before attempting to autoscale it.</span></span> <span data-ttu-id="88951-123">Biz otomatik ölçeklendirme için farklı bir ölçümü tercih ederseniz, biz kullanırsınız `counterSpecifier` tanılama uzantısını yapılandırmasından `metricName` otomatik ölçeklendirme yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="88951-123">If we choose a different metric to autoscale on, we would use the `counterSpecifier` from the diagnostics extension configuration as the `metricName` in the autoscale configuration.</span></span> <span data-ttu-id="88951-124">Otomatik ölçeklendirme yapılandırma hakkında daha fazla bilgi için bkz: [otomatik ölçeklendirme en iyi yöntemler](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) ve [Azure İzleyici REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="88951-124">For more information on autoscale configuration, see the [autoscale best practices](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) and the [Azure Monitor REST API reference documentation](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span></span>

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





## <a name="next-steps"></a><span data-ttu-id="88951-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="88951-125">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
