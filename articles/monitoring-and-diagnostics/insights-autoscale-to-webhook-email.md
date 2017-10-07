---
title: "aaaUse otomatik ölçeklendirme eylemleri toosend e-posta ve Web kancası uyarı bildirimleri. | Microsoft Belgeleri"
description: "Nasıl toouse otomatik ölçeklendirme eylemleri toocall URL'leri web veya Azure İzleyicisi'nde e-posta bildirimleri gönderin konusuna bakın. "
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: eb9a4c98-0894-488c-8ee8-5df0065d094f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: ancav
ms.openlocfilehash: f611a18f5a808412fbdd0c89e3addb36437064c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a>Otomatik ölçeklendirme eylemleri toosend e-posta ve Web kancası uyarı bildirimleri Azure İzleyicisi'nde kullanın
Bu makalede, böylece belirli web URL'leri çağrısı veya Azure otomatik ölçeklendirme eylemleri göre e-postalar göndermek Tetikleyicileri nasıl ayarlama gösterilir.  

## <a name="webhooks"></a>Web kancaları
Web kancası tooroute hello Azure uyarı bildirimleri tooother sistemleri işlem sonrası veya özel bildirimleri için izin verir. Örneğin, bir gelen web isteği toosend SMS günlük hataları işleyebileceği yönlendirme hello uyarı tooservices Sohbeti kullanarak veya hizmetleri Mesajlaşma takım bildir, vb. hello Web kancası URI geçerli bir HTTP veya HTTPS uç noktası olmalıdır.

## <a name="email"></a>E-posta
Tooany geçerli e-posta adresine e-posta gönderilebilir. Yöneticiler ve hello kural çalıştığı hello aboneliğin ortak yöneticileri aynı zamanda bildirilecek.

## <a name="cloud-services-and-web-apps"></a>Bulut Hizmetleri ve Web uygulamaları
Azure portal hello bulut Hizmetleri ve sunucu grupları (Web uygulamaları) için katılımı.

* Merhaba seçin **göre ölçeklendirmeniz** ölçüm.

![tarafından ölçeklendirme](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a>Sanal makine ölçekleme kümeleri
Yeni Kaynak Yöneticisi (sanal makine ölçek kümeleri) ile oluşturulan sanal makineler için bunu REST API, Resource Manager şablonları, PowerShell ve CLI kullanarak yapılandırabilirsiniz. Bir portal arabirimi henüz kullanılabilir değil.
Hello REST API veya Resource Manager şablonunu kullandığınızda, aşağıdaki seçenekleri şu hello ile Merhaba bildirimleri öğesi ekleyin.

```
"notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": false,
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
| Alan | Zorunlu? | Açıklama |
| --- | --- | --- |
| işlemi |Evet |değerin "Ölçek" olması gerekir |
| sendToSubscriptionAdministrator |Evet |değer "true" veya "false" olmalıdır |
| sendToSubscriptionCoAdministrators |Evet |değer "true" veya "false" olmalıdır |
| customEmails |Evet |değer null [] veya e-postaların dize dizisi olabilir |
| Web kancaları |Evet |değer null veya geçerli URI olabilir |
| serviceUri |Evet |Geçerli bir https URI |
| properties |Evet |Değer boş {} olması gerekir veya anahtar-değer çiftleri içerebilir |

## <a name="authentication-in-webhooks"></a>Web kancası kimlik doğrulaması
Merhaba Web kancası hello Web kancası URI sorgu parametresi olarak bir belirteç kimliği ile kaydettiğiniz belirteç tabanlı kimlik doğrulamasını kullanarak kimlik doğrulaması yapabilir. Örneğin, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue

## <a name="autoscale-notification-webhook-payload-schema"></a>Otomatik ölçeklendirme bildirim Web kancası yükü şeması
Merhaba otomatik ölçeklendirme bildirim oluşturulduğunda hello aşağıdaki meta verileri hello Web kancası yükünde eklenmiştir:

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' toocapacity '2'",
                "subscriptionId": "s1",
                "resourceGroupName": "rg1",
                "resourceName": "MyCSRole",
                "resourceType": "microsoft.classiccompute/domainnames/slots/roles",
                "resourceId": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService/slots/Production/roles/MyCSRole",
                "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService",
                "oldCapacity": "3",
                "newCapacity": "2"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```


| Alan | Zorunlu? | Açıklama |
| --- | --- | --- |
| durum |Evet |otomatik ölçeklendirme eylemi oluşturulan gösterir hello durumu |
| işlemi |Evet |Artışı örnekleri için "Ölçeği Genişlet" olur ve bir düşüş için örnekleri, "Ölçek içinde" olacaktır |
| bağlam |Evet |Merhaba otomatik ölçeklendirme eylem bağlamı |
| timestamp |Evet |Merhaba otomatik ölçeklendirme eylemi tetiklendiğinde zaman damgası |
| id |Evet |Resource Manager Kimliğini hello otomatik ölçeklendirme ayarı |
| ad |Evet |Hello hello otomatik ölçeklendirme ayarı adı |
| Ayrıntıları |Evet |Otomatik ölçeklendirme hizmet hello hello eylem açıklaması sürdü ve hello değiştirmek hello örnek sayısı |
| subscriptionId |Evet |Abonelik kimliği ölçeklendirilir hello hedef kaynak |
| resourceGroupName |Evet |Genişletilmiş hello hedef kaynak kaynak grubu adı |
| resourceName |Evet |Genişletilmiş hello hedef kaynağın adı |
| Kaynak türü |Evet |Merhaba üç desteklenen değerler: "microsoft.classiccompute/domainnames/slots/roles" - bulut hizmeti rolleri, "microsoft.compute/virtualmachinescalesets" - sanal makine ölçek kümeleri ve "Microsoft.Web/serverfarms" - Web uygulaması |
| resourceId |Evet |Genişletilmiş hello hedef kaynak Resource Manager kimliği |
| portalLink |Evet |Azure portal bağlantısı toohello Özet sayfasında hello hedef kaynak |
| oldCapacity |Evet |bir ölçek eylemi otomatik ölçeklendirme geçen zaman hello geçerli (eski) örnek sayısı |
| newCapacity |Evet |otomatik ölçeklendirme hello kaynak çok ölçeklendirilmiş hello yeni örnek sayısı|
| Özellikler |Hayır |İsteğe bağlı. < Anahtar, değer > kümesi çiftleri (örneğin, sözlük < dize, dize >). Merhaba özellikleri alan isteğe bağlıdır. Özel kullanıcı arabirimi veya mantığı tabanlı uygulama iş akışı, anahtarlar ve hello yükü kullanılarak geçirilebilir değerler girebilirsiniz. Toouse hello Web kancası URI kendisini (gibi sorgu parametrelerini) toopass özel özellikler toohello giden Web kancası çağrı başa alternatif bir yoludur. |
