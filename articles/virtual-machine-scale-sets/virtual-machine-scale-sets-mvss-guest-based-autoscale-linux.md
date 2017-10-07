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
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a>Bir Linux ölçek kümesi şablonunda Konuk ölçümleri kullanarak otomatik ölçeklendirme

Azure VM'lerin toplanır ve ölçek kümeleri ölçümlerini iki tür vardır: bazı gelen hello VM ana bilgisayar ve diğerleri hello Konuk sanal gelir. Ana ölçümleri gerektirmez ek kurulum hello ana bilgisayar VM tarafından toplanan çünkü Konuk ölçümleri bize tooinstall hello gerektirdiğinde [Windows Azure tanılama uzantısını](../virtual-machines/windows/extensions-diagnostics-template.md) veya hello [Linux Azure tanılama Uzantı](../virtual-machines/linux/diagnostic-extension.md) hello VM konuk. Bir ortak neden toouse Konuk ölçümleri ana ölçümleri yerine Konuk ölçümleri ölçümleri ana ölçümleri daha büyük seçimi sağlamaktır. Böyle bir yalnızca konuk ölçümleri kullanılabilir bellek tüketimi ölçümlerini örnektir. desteklenen hello ana ölçümleri listelenen [burada](../monitoring-and-diagnostics/monitoring-supported-metrics.md), ve yaygın olarak kullanılan Konuk ölçümleri listelenen [burada](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md). Bu makalede gösterilmektedir nasıl toomodify hello [minimum uygun ölçek kümesi şablonu](./virtual-machine-scale-sets-mvss-start.md) toouse otomatik ölçeklendirme kurallarını temel alarak Linux ölçek kümeleri için konuk ölçümleri.

## <a name="change-hello-template-definition"></a>Merhaba şablon tanımını değiştirin

Bizim minimum uygun ölçek kümesi şablon görülebilir [burada](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), ve hello Linux ölçeği konuk tabanlı otomatik ölçeklendirme ile Ayarla dağıtmak için bizim şablon görülebilir [burada](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json). Merhaba kullanılan fark toocreate bu şablonu inceleyelim (`git diff minimum-viable-scale-set existing-vnet`) tarafından parça parça:

Parametreler için ilk olarak, eklediğimiz `storageAccountName` ve `storageAccountSasToken`. Merhaba Tanılama Aracı ölçüm verileri depolar bir [tablo](../cosmos-db/table-storage-how-to-use-dotnet.md) bu depolama hesabında. Hello Linux Tanılama Aracı sürüm 3.0 sürümünden itibaren bir depolama erişim tuşunu kullanarak artık desteklenmemektedir. Biz kullanmalısınız bir [SAS belirteci](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

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

Ardından, biz hello ölçek kümesini değiştirme `extensionProfile` tooinclude hello tanılama uzantısını. Bu yapılandırmada, biz toocollect ölçümleri kimliği hello ölçek kümesi hello kaynağı belirtin, aynı zamanda depolama hesabı ve SAS belirteci toouse toostore hello ölçümleri hello. Biz de hello ölçümleri (Bu durumda dakikada) ne sıklıkta toplanır ve hangi ölçümleri tootrack (bellekte bu servis talebi yüzde kullanılan) belirtin. Bu yapılandırma hakkında daha ayrıntılı bilgi ve ölçümleri yüzde dışında kullanılan bellek için bkz: [bu belgeleri](../virtual-machines/linux/diagnostic-extension.md).

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

Son olarak, eklediğimiz bir `autoscaleSettings` kaynak tooconfigure otomatik ölçeklendirme dayalı bu ölçümleri. Bu kaynak bir `dependsOn` hello ölçek başvuran yan tümcesi hello ölçek kümesini tooautoscale denemeden önce mevcut tooensure ayarlamak. Biz üzerinde farklı ölçüm tooautoscale seçerseniz, hello kullanmanız `counterSpecifier` hello tanılama uzantısını yapılandırmadan hello olarak `metricName` hello otomatik ölçeklendirme yapılandırması. Merhaba otomatik ölçeklendirme yapılandırma hakkında daha fazla bilgi için bkz: [otomatik ölçeklendirme en iyi yöntemler](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) ve hello [Azure İzleyici REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/dn931928.aspx).

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





## <a name="next-steps"></a>Sonraki adımlar

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
