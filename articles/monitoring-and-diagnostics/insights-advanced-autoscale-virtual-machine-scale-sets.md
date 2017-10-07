---
title: "Azure sanal makineleri kullanarak otomatik ölçeklendirme aaaAdvanced | Microsoft Docs"
description: "Birden çok kural ve e-posta göndermek ve ölçek eylemleri ile Web kancası URL'leri çağrı profillerinin Resource Manager ve VM ölçek kümesi kullanır."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 7e3576e2-4a2b-4736-b5ae-98c4689cdd2b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2016
ms.author: ancav
ms.openlocfilehash: ecb01e3094f715837b75ef07a7dbecdf0f2e78f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a>VM ölçek kümesi için Resource Manager şablonları kullanarak gelişmiş otomatik ölçeklendirme yapılandırma
Ölçek ve sanal makine ölçek kümeleri yinelenen bir zamanlamaya göre veya belirli bir tarihe göre performans ölçüm eşiklere dayanarak genişleme kullanabilirsiniz. Ölçeklendirme eylemi için e-posta ve Web kancası bildirimleri de yapılandırabilirsiniz. Bu kılavuz, bir VM ölçek kümesi üzerinde bir Resource Manager şablonu kullanarak bu nesneleri yapılandırma örneği gösterilir.

> [!NOTE]
> Bu kılavuz, VM ölçek kümesi için hello adımlar açıklanmaktadır, ancak hello aynı bilgiler tooautoscaling geçerlidir [bulut Hizmetleri](https://azure.microsoft.com/services/cloud-services/), ve [uygulama hizmeti - Web Apps](https://azure.microsoft.com/services/app-service/web/).
> Bir basit performans ölçümü CPU gibi basit bir ölçek giriş/çıkış VM ölçek kümesi ayarda dayalı için toohello başvuran [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) ve [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) belgeleri
>
>

## <a name="walkthrough"></a>Kılavuz
Bu kılavuzda, kullandığımız [Azure kaynak Gezgini](https://resources.azure.com/) tooconfigure ve güncelleştirme hello otomatik ölçeklendirme ayarının ölçek kümesi için. Azure kaynak Gezgini kolay bir yolu toomanage olan Resource Manager şablonları aracılığıyla Azure kaynakları. Yeni tooAzure kaynak Gezgini aracı varsa, okuma [bu giriş](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).

1. Bir temel otomatik ölçeklendirme ayarı ile yeni bir ölçek dağıtın. Bu makalede hello sahip bir Windows Azure hızlı başlama Galerisi gelen hello kullanan ölçek kümesi temel otomatik ölçeklendirme şablonla. Linux ölçek ayarlar çalışma hello aynı şekilde.
2. Merhaba ölçek kümesi oluşturulduktan sonra Azure kaynak Gezgini toohello ölçek kümesi kaynaktan gidin. Merhaba aşağıdaki Microsoft.ınsights düğümü altında bakın.

    ![Azure Gezgini](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    Hello şablon yürütme hello ada sahip varsayılan bir otomatik ölçeklendirme ayarı oluşturdu **'autoscalewad'**. Merhaba sağ tarafta, bu otomatik ölçeklendirme ayarı tam tanımını hello görüntüleyebilirsiniz. Bu durumda, hello varsayılan otomatik ölçeklendirme ayarında bir CPU tabanlı % genişleme ve ölçek bileşenini kuralı ile birlikte gelir.  

3. Artık daha fazla profilleri ve hello zamanlama veya özel gereksinimler dayalı kurallar ekleyebilirsiniz. Üç profil ile bir otomatik ölçeklendirme ayarı oluşturuyoruz. toounderstand profilleri ve otomatik ölçeklendirme, kuralları gözden [otomatik ölçeklendirme en iyi yöntemler](insights-autoscale-best-practices.md).  

    | Profilleri & kuralları | Açıklama |
    |--- | --- |
    | **Profili** |**Performans/ölçü dayalı** |
    | Kural |Hizmet veri yolu kuyruğu ileti sayısı > x |
    | Kural |Hizmet veri yolu kuyruğu ileti sayısı < y |
    | Kural |CPU % > n |
    | Kural |CPU % < p |
    | **Profili** |**Hafta içi gün sabah saat (kuralları yok)** |
    | **Profili** |**Ürün başlatma gün (kuralları yok)** |

4. Bu kılavuz için kullandığımız kuramsal bir ölçeklendirme senaryo aşağıda verilmiştir.

    * **Temel yük** -tooscale veya my ölçek set.* üzerinde barındırılan Uygulamam hello yüküne göre istiyorum
    * **Sıra boyutu ileti** -ı Merhaba gelen iletileri toomy uygulaması için bir hizmet veri yolu kuyruğu kullanın. Merhaba sıranın ileti sayısı ve CPU % kullanın ve ileti sayısı veya CPU isabet threshold.* hello bir varsayılan profili tootrigger bir ölçek eylemi yapılandırın
    * **Haftanın günü ve saat** -'Hafta içi gün sabah saat' adlı bir haftalık yinelenen 'zaman hello günün' temel profil istiyor. Geçmiş verilerini temel alarak VM sayısı toohandle my uygulamanın yükleme sırasında bu sağlar.* örnekleri belirli daha iyi toohave olduğunu bilmeniz
    * **Özel tarih** -'Ürün başlatma Day' profili eklendi. Böylece Uygulamam hazır toohandle hello yük pazarlama duyuruları nedeniyle ve biz hello uygulamasında yeni bir ürün zaman put t belirli tarihler için İleriyi
    * *Son iki Hello profilleri diğer performans ölçüm tabanlı içinde kurallar bunları da sahip olabilirsiniz. Bu durumda değil toohave bir karar ve bunun yerine toorely üzerinde hello varsayılan performans ölçüm kuralları dayalı. Kuralları hello yinelenen ve tarih temelli profilleri için isteğe bağlıdır.*

    Otomatik ölçeklendirme altyapısının önceliği hello profilleri ve kuralları hello ayrıca yakalanan [otomatik ölçeklendirmeyi en iyi yöntemler](insights-autoscale-best-practices.md) makalesi.
    Otomatik ölçeklendirme için ortak ölçümleri listesi için bkz [otomatik ölçeklendirme için ortak ölçümleri](insights-autoscale-common-metrics.md)

5. Merhaba üzerinde olduğundan emin olun **okuma/yazma** kaynak Gezgininde modu

    ![Autoscalewad, varsayılan otomatik ölçeklendirme ayarı](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. Düzenle'yi tıklatın. **Değiştir** hello 'profilleri' öğesinde yapılandırma aşağıdaki hello otomatik ölçeklendirme ayarı:

    ![Profilleri](./media/insights-advanced-autoscale-vmss/profiles.png)

    ```
    {
            "name": "Perf_Based_Scale",
            "capacity": {
              "minimum": "2",
              "maximum": "12",
              "default": "2"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 10
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 3
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 85
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          },
          {
            "name": "Weekday_Morning_Hours_Scale",
            "capacity": {
              "minimum": "4",
              "maximum": "12",
              "default": "4"
            },
            "rules": [],
            "recurrence": {
              "frequency": "Week",
              "schedule": {
                "timeZone": "Pacific Standard Time",
                "days": [
                  "Monday",
                  "Tuesday",
                  "Wednesday",
                  "Thursday",
                  "Friday"
                ],
                "hours": [
                  6
                ],
                "minutes": [
                  0
                ]
              }
            }
          },
          {
            "name": "Product_Launch_Day",
            "capacity": {
              "minimum": "6",
              "maximum": "20",
              "default": "6"
            },
            "rules": [],
            "fixedDate": {
              "timeZone": "Pacific Standard Time",
              "start": "2016-06-20T00:06:00Z",
              "end": "2016-06-21T23:59:00Z"
            }
          }
    ```
    Desteklenen alanlar ve bunların değerleri için bkz: [otomatik ölçeklendirme REST API belgeleri](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx). Şimdi, otomatik ölçeklendirme ayarında daha önce açıklanan hello üç profil içerir.

7. Son olarak, otomatik ölçeklendirme hello Ara **bildirim** bölümü. Otomatik ölçeklendirme bildirimleri toodo üç şey bir genişletme zaman izin verin veya eylemi başarıyla tetiklendi.
   - Hello Yöneticisi ve ortak yöneticileri aboneliğinizin bildir
   - Kullanıcı e-posta
   - Bir Web kancası çağrı tetikler. Harekete, bu Web kancası hello otomatik ölçeklendirmeyi koşul hakkındaki meta verileri gönderir ve kaynak hello ölçek kümesi. otomatik ölçeklendirme Web kancası hello yükünü hakkında daha fazla toolearn bkz [yapılandırma Web kancası & otomatik ölçeklendirme için e-posta bildirimleri](insights-autoscale-to-webhook-email.md).

   Toohello otomatik ölçeklendirme ayarı değiştirerek aşağıdaki hello eklemek, **bildirim** öğesi değeri null

   ```
   "notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": true,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]

   ```

   İsabet **Put** kaynak Gezgini tooupdate hello otomatik ölçeklendirme ayarında düğmesi.

Bir otomatik ölçeklendirme VM ölçek kümesi tooinclude üzerinde birden fazla ölçek profilleri ayarı güncelleştirdiniz ve bildirimleri ölçeklendirin.

## <a name="next-steps"></a>Sonraki Adımlar
Otomatik ölçeklendirme hakkında daha fazla bu bağlantılar toolearn kullanın.

[Otomatik ölçeklendirme sanal makine ölçek kümeleri ile ilgili sorunları giderme](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[Otomatik ölçeklendirme için ortak ölçümleri](insights-autoscale-common-metrics.md)

[Azure otomatik ölçeklendirme için en iyi yöntemler](insights-autoscale-best-practices.md)

[Otomatik ölçeklendirme PowerShell kullanarak yönetme](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[Otomatik ölçeklendirme CLI kullanarak yönetme](insights-cli-samples.md#autoscale)

[Web kancası & otomatik ölçeklendirme için e-posta bildirimleri yapılandırma](insights-autoscale-to-webhook-email.md)
