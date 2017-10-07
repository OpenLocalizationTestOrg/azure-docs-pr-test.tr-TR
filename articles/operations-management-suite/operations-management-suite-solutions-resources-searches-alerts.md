---
title: "aaaSaved arar ve uyarılar OMS çözümleri | Microsoft Docs"
description: "OMS çözümlerinde genellikle Kaydedilmiş aramaları hello çözümü tarafından toplanan günlük analizi tooanalyze verileri de içerir.  Aynı zamanda uyarılar toonotify hello kullanıcı tanımlar olabilir veya otomatik olarak yanıt tooa kritik sorunu eylemi gerçekleştirin.  Bu makalede, yönetim çözümlerine dahil şekilde nasıl toodefine günlük analizi arar ve Uyarıları bir ARM şablonu kaydedileceği açıklanmaktadır."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a>Günlük analizi ekleme arar ve Uyarıları tooOMS kaydedilen yönetim çözümü (Önizleme)

> [!NOTE]
> Bu, şu anda önizlemede OMS yönetim çözümleri oluşturmak için başlangıç belgesidir. Aşağıda açıklanan herhangi bir şema konu toochange ' dir.   


[OMS yönetim çözümlerine](operations-management-suite-solutions.md) genellikle içerecektir [kayıtlı aramalar](../log-analytics/log-analytics-log-searches.md) hello çözümü tarafından toplanan günlük analizi tooanalyze veri.  Ayrıca tanımlayabilir [uyarıları](../log-analytics/log-analytics-alerts.md) toonotify hello kullanıcı ya da otomatik olarak yanıt tooa kritik sorunu eylemi gerçekleştirin.  Günlük analizi toodefine arar ve uyarılar kaydedilme bu makalede bir [kaynak yönetimi şablonu](../resource-manager-template-walkthrough.md) içinde eklenebilir şekilde [yönetim çözümleri](operations-management-suite-solutions-creating.md).

> [!NOTE]
> Merhaba bu makaledeki örnekler parametreleri ve ya da gerekli veya ortak toomanagement çözümleri ve açıklanan değişkenleri kullanma [Operations Management Suite (OMS) yönetimi çözümleri oluşturma](operations-management-suite-solutions-creating.md)  

## <a name="prerequisites"></a>Ön koşullar
Bu makale, zaten çok konusunda bilgi sahibi olduğunuzu varsayar[bir yönetim çözümü oluşturma](operations-management-suite-solutions-creating.md) ve hello yapısını bir [ARM şablonu](../resource-group-authoring-templates.md) ve çözüm dosya.


## <a name="log-analytics-workspace"></a>Günlük analizi çalışma alanı
Günlük analizi tüm kaynaklarında bulunan bir [çalışma](../log-analytics/log-analytics-manage-access.md).  Bölümünde açıklandığı gibi [OMS çalışma ve Automation hesabı](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello çalışma hello Yönetimi çözümünde dahil değildir ancak hello çözüm yüklenmeden önce mevcut olması gerekir.  Kullanılabilir değilse, hello çözüm yükleme başarısız olur.

Merhaba hello çalışma her günlük analizi kaynak hello adlarında adıdır.  Bu hello ile Merhaba çözümde yapılır **çalışma** savedsearch kaynak örneği aşağıdaki hello olduğu gibi parametre.

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a>Kaydedilen aramalar
Dahil [kayıtlı aramalar](../log-analytics/log-analytics-log-searches.md) çözümünüz tarafından toplanan çözüm tooallow kullanıcılar tooquery veri.  Kaydedilmiş aramaları altında görünür **Sık Kullanılanlar** hello OMS portalında ve **kayıtlı aramaları** hello Azure Portalı'nda.  Kaydedilmiş bir aramayı de her uyarı için gereklidir.   

[Günlük analizi kaydedilen arama](../log-analytics/log-analytics-log-searches.md) kaynaklarınız türü `Microsoft.OperationalInsights/workspaces/savedSearches` ve yapı izlenerek hello sahiptir.  Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir. 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



Her bir kayıtlı arama hello özelliklerinin aşağıdaki tablonun hello açıklanmıştır. 

| Özellik | Açıklama |
|:--- |:--- |
| category | Merhaba kayıtlı arama Hello kategorisi.  Merhaba konsolunda birlikte gruplanır şekilde herhangi aynı çözüm genellikle paylaşacak hello tek bir kategori kayıtlı aramalar. |
| görünen adı | Merhaba adı toodisplay hello Portalı'nda arama kaydedildi. |
| sorgu | Sorgu toorun. |

> [!NOTE]
> JSON olarak yorumlanabilecek karakterler içeriyorsa toouse kaçış karakterleri hello sorgusunda gerekebilir.  Örneğin, sorgu, **türü: AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, hello Çözüm dosyasındaki yazılmalıdır **türü: AzureActivity işlemadı:\" Microsoft.Compute/virtualMachines/write\"**.

## <a name="alerts"></a>Uyarılar
[Analytics uyarıları oturum](../log-analytics/log-analytics-alerts.md) düzenli aralıklarla kaydedilmiş bir aramayı çalıştırma uyarı kuralları tarafından oluşturulur.  Merhaba hello sorgunun sonuçlarını belirtilen ölçütlere uyan varsa bir uyarı kaydı oluşturulur ve bir veya daha fazla eylem çalıştırın.  

Bir yönetim çözümüne uyarı kuralları üç farklı kaynaklar aşağıdaki hello yapılır.

- **Kayıtlı arama.**  Çalıştırılacak hello günlük arama tanımlar.  Birden çok uyarı kurallarını, tek bir kayıtlı arama paylaşabilirsiniz.
- **Zamanlama.**  Ne sıklıkta hello günlük arama çalıştırılacak tanımlar.  Her uyarı kuralı tek bir zamanlama sahip olur.
- **Uyarı eylem.**  Her uyarı kuralı bir eylem kaynak türüne sahip olacaktır **uyarı** hello hello ölçütlerini ne zaman bir uyarı kaydı oluşturulur ve uyarının önem derecesi hello gibi hello uyarı ayrıntılarını tanımlar.  Merhaba eylem kaynak isteğe bağlı olarak bir posta ve runbook yanıt tanımlayacaksınız.
- **Web kancası eylem (isteğe bağlı).**  Merhaba uyarı kuralı, bir Web kancası çağıracaktır sonra başka bir işlem kaynak türüne sahip gerektirir **Web kancası**.    

Kaynaklar, yukarıda açıklanan arama kaydedildi.  Merhaba kaynaklar aşağıda açıklanmıştır.


### <a name="schedule-resource"></a>Zamanlama kaynak

Kaydedilmiş bir aramayı her zamanlamayı ayrı bir uyarı kuralı temsil eden ile bir veya daha fazla zamanlama olabilir. Merhaba zamanlama ne sıklıkta hello arama çalıştırılır ve zaman aralığı içinde hangi hello veriler alınır hello tanımlar.  Zamanlama kaynaklarınız türü `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` ve yapı izlenerek hello sahiptir. Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir. 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



Aşağıdaki tablonun hello zamanlama kaynakların Hello özellikleri açıklanmaktadır.

| Öğe adı | Gerekli | Açıklama |
|:--|:--|:--|
| Etkin       | Evet | Merhaba uyarı oluşturulduğunda etkinleştirilip etkinleştirilmeyeceğini belirtir. |
| interval      | Evet | Ne sıklıkta hello sorgu dakika içinde çalışır. |
| QueryTimeSpan | Evet | Hangi tooevaluate sonuçları üzerinden dakika cinsinden süre uzunluğu. |

Merhaba zamanlama kaynak hello zamanlama önce oluşturulan kaydedilmiş aramayı hello bağlı.


### <a name="actions"></a>Eylemler
Merhaba tarafından belirtilen eylemi kaynak iki tür vardır **türü** özelliği.  Bir zamanlama gerektiren **uyarı** hello uyarı kuralı ve bir uyarı oluşturulduğunda, hangi eylemleri alınır hello ayrıntılarını tanımlayan eylem.  Ayrıca içerebilir bir **Web kancası** eylem bir Web kancası hello uyarıdan çağrılmalıdır.  

Eylem kaynaklarınız türü `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.  

#### <a name="alert-actions"></a>Uyarı eylemleri

Her biri zaman çizelgeleri **uyarı** eylem.  Merhaba ayrıntılarını hello uyarı ve isteğe bağlı olarak bildirim ve düzeltme eylemleri tanımlar.  Bir e-posta tooone bir bildirim gönderir veya daha fazla adresleri.  Bir düzeltme Azure Otomasyonu tooattempt tooremediate algılanan hello sayısındaki bir runbook başlatır.

Uyarı eylemleri yapı izlenerek hello vardır.  Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir. 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

Uyarı eylemi kaynakların Hello özellikleri tabloları aşağıdaki hello açıklanmaktadır.

| Öğe adı | Gerekli | Açıklama |
|:--|:--|:--|
| Tür | Evet | Merhaba eylem türü.  Bu **uyarı** uyarı eylemleri için. |
| Ad | Evet | Merhaba uyarı görünen adı.  Bu hello uyarı kuralı için başlangıç konsolunda görüntülenen hello adıdır. |
| Açıklama | Hayır | Merhaba uyarı isteğe bağlı bir açıklama. |
| Önem Derecesi | Evet | Önem derecesi değerlerini aşağıdaki hello uyarı kaydından hello:<br><br> **Kritik**<br>**Uyarı**<br>**Bilgilendirme** |


##### <a name="threshold"></a>Eşik
Bu bölüm gereklidir.  Merhaba uyarı eşiği hello özelliklerini tanımlar.

| Öğe adı | Gerekli | Açıklama |
|:--|:--|:--|
| işleci | Evet | Değerleri aşağıdaki hello hello karşılaştırmadan işleci:<br><br>**gt büyük =<br>lt = küçüktür** |
| Değer | Evet | Merhaba değeri toocompare hello sonuçları. |


##### <a name="metricstrigger"></a>MetricsTrigger
Bu bölümde isteğe bağlıdır.  Bir ölçüm ölçüm uyarı içerir.

> [!NOTE]
> Ölçüm ölçüm uyarılar şu anda genel önizlemede. 

| Öğe adı | Gerekli | Açıklama |
|:--|:--|:--|
| TriggerCondition | Evet | Merhaba Eşik ihlallerini veya değerleri aşağıdaki hello gelen ardışık ihlallerini toplam sayısını olup olmadığını belirtir:<br><br>**Toplam<br>ardışık** |
| işleci | Evet | Değerleri aşağıdaki hello hello karşılaştırmadan işleci:<br><br>**gt büyük =<br>lt = küçüktür** |
| Değer | Evet | Hello ölçütleri kez hello sayısı ölç tootrigger hello uyarı olmalıdır. |

##### <a name="throttling"></a>Azaltma
Bu bölümde isteğe bağlıdır.  Toosuppress uyarılardan aynı bazı süreyi bir uyarı oluşturulduktan sonra için kural hello istiyorsanız bu bölümü ekleyin.

| Öğe adı | Gerekli | Açıklama |
|:--|:--|:--|
| Dakika Cinsiden Süre | Dahil edilen öğesi azaltma, Evet | Aynı uyarı kuralı oluşturulan dakika toosuppress uyarıların hello birinden sonra sayısı. |

##### <a name="emailnotification"></a>EmailNotification
 Bu bölüm, bunu istiyorsanız hello uyarı toosend posta tooone ya da daha fazla alıcı isteğe bağlı dahil değildir.

| Öğe adı | Gerekli | Açıklama |
|:--|:--|:--|
| Alıcıları | Evet | Bir uyarı gibi aşağıdaki örneğine hello oluşturulduğunda e-posta virgülle ayrılmış listesini toosend bildirim giderir.<br><br>**[ "recipient1@contoso.com", "recipient2@contoso.com" ]** |
| Konu | Evet | Merhaba posta konu satırı. |
| Eki | Hayır | Ekleri şu anda desteklenmemektedir.  Bu öğe dahil ise olmalıdır **hiçbiri**. |


##### <a name="remediation"></a>Düzeltme
Bu bölümde isteğe bağlı bir runbook toostart yanıt toohello uyarısında istiyorsanız ekleyin. |

| Öğe adı | Gerekli | Açıklama |
|:--|:--|:--|
| RunbookName | Evet | Merhaba runbook toostart adı. |
| WebhookUri | Evet | Merhaba Web kancası hello runbook için URI. |
| Süre sonu | Hayır | Tarih ve saat düzeltme hello süresi dolar. |

#### <a name="webhook-actions"></a>Web kancası eylemleri

Web kancası eylemleri, bir URL çağırma ve isteğe bağlı olarak gönderilen bir yükü toobe sağlayan bir işlem başlatın. Azure Otomasyon çalışma kitabı dışındaki işlemler çağırabilir Web kancası için amacı dışında benzer tooRemediation Eylemler oldukları. Yükü teslim toobe toohello uzak bir işlem sağlayarak hello ek bir seçeneğiniz de sağlar.

Uyarınız bir Web kancası çağırır sonra bir eylem kaynak türüne sahip gerekir **Web kancası** toplama toohello içinde **uyarı** eylem kaynak.  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

Web kancası eylem kaynakların Hello özellikleri tabloları aşağıdaki hello açıklanmaktadır.

| Öğe adı | Gerekli | Açıklama |
|:--|:--|:--|
| type | Evet | Merhaba eylem türü.  Bu **Web kancası** Web kancası eylemleri için. |
| ad | Evet | Merhaba eylem görünen adı.  Bu hello konsolunda görüntülenmez. |
| wehookUri | Evet | Merhaba Web kancası için URI. |
| CustomPayload | Hayır | Özel yük toobe toohello Web kancası gönderdi. Merhaba biçimi hangi hello Web kancası bekleniyor bağlı olacaktır. |




## <a name="sample"></a>Örnek

Aşağıdaki kaynakları izleyerek hello içeren içeren bir çözüm örneğidir:

- Kayıtlı arama
- Zamanlama
- Uyarı eylemi
- Web kancası eylemi

Merhaba örnek kullanır [standart çözüm parametreleri](operations-management-suite-solutions-solution-file.md#parameters) bir çözüm olarak, yaygın olarak kullanılacak değişkenleri toohardcoding değerleri hello kaynak tanımlarında değil.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for hello email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


Aşağıdaki parametre dosyasına hello örnekleri değerleri için bu çözümü sağlar.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a>Sonraki adımlar
* [Görünümler ekleme](operations-management-suite-solutions-resources-views.md) tooyour yönetim çözümü.
* [Otomasyon runbook'ları ve diğer kaynakları eklemek](operations-management-suite-solutions-resources-automation.md) tooyour yönetim çözümü.

