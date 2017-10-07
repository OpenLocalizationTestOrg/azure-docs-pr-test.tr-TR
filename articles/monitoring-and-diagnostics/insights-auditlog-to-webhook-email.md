---
title: "aaaCall bir Web kancası Azure etkinlik günlüğü uyarılar hakkında | Microsoft Docs"
description: "Etkinlik günlüğü olaylarını tooother Hizmetleri özel eylemler için rota. Örneğin SMS gönder, hatalar oturum veya sohbet ve mesajlaşma hizmeti üzerinden bir takım bildirin."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 9017ff3e5165857ec7084a8f07f4123552e55f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a>Bir Web kancası Azure etkinlik günlüğü uyarılar çağırın
Web kancası tooroute Azure izin uyarı bildirim tooother sistemleri işlem sonrası ya da özel eylemler için. Bir uyarı tooroute üzerinde bir Web kancası kullanabilirsiniz, SMS gönder tooservices oturum hatalar, sohbet ve mesajlaşma Servisleri üzerinden takım bildirmek veya herhangi bir sayıda diğer eylemleri yapın. Bu makalede nasıl tooset bir Web kancası toobe Azure etkinlik günlüğü uyarı ateşlenir çağrılır açıklanmaktadır. Ayrıca, hangi hello yükü hello HTTP POST tooa Web kancası gibi görünüyor gösterir. Merhaba kurulumu ve bir Azure ölçüm uyarı şeması hakkında bilgiler için [bunun yerine bu sayfaya bakın](insights-webhooks-alerts.md). Etkinleştirildiğinde bir etkinlik günlüğü uyarı toosend e-posta de ayarlayabilirsiniz.

> [!NOTE]
> Bu özellik şu anda önizlemede değil ve gelecekteki hello belirli bir noktada kaldırılacak.
>
>

Hello kullanarak bir etkinlik günlüğü alarm kurabilirsiniz [Azure PowerShell cmdlet'leri](insights-powershell-samples.md#create-metric-alerts), [platformlar arası CLI](insights-cli-samples.md#work-with-alerts), veya [Azure İzleyici REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx). Şu anda bir hello Azure portal kullanarak ayarlanamıyor.

## <a name="authenticating-hello-webhook"></a>Merhaba Web kancası kimlik doğrulaması
Merhaba Web kancası bu yöntemlerden birini kullanarak doğrulayabilir:

1. **Belirteç tabanlı bir yetkilendirme** -URI kaydedilir belirteci Kimliğine sahip, örneğin, Web kancası hello`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`
2. **Temel yetkilendirme** -URI kaydedilir bir kullanıcı adı ve parola, örneğin, Web kancası hello`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`

## <a name="payload-schema"></a>Yükü şeması
Merhaba POST işlemine JSON yükü ve etkinlik günlüğü tabanlı tüm uyarılar için şema aşağıdaki hello içerir. Bu şemayı bir ölçüm tabanlı uyarılar tarafından kullanılan benzer toohello ' dir.

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| Öğe adı | Açıklama |
| --- | --- |
| durum |Ölçüm uyarılar için kullanılır. Her zaman "çok etkinlik günlüğü uyarılar için etkinleştirilmiş" ayarlayın. |
| bağlam |Merhaba olay bağlamı. |
| resourceProviderName |Merhaba Hello kaynak sağlayıcısı kaynak etkilenmiş. |
| Koşul türü |Her zaman "olayını." |
| ad |Merhaba uyarı kuralının adı. |
| id |Merhaba uyarı kaynak kimliği. |
| açıklama |Merhaba uyarı oluşturulması sırasında uyarı açıklaması olarak ayarla. |
| subscriptionId |Azure abonelik kimliği |
| timestamp |Hangi hello olay hello hello istek işlenmeden Azure hizmeti tarafından oluşturulan saat. |
| resourceId |Kaynak Kimliğini hello kaynak etkilenmiş. |
| resourceGroupName |Kaynak hello kaynak grubunun adını hello için etkilenen |
| properties |Kümesi `<Key, Value>` çiftleri (yani `Dictionary<String, String>`) hello olay ayrıntılarını içerir. |
| Olay |Merhaba olayla ilgili meta verileri içeren öğe. |
| Yetkilendirme |Merhaba olay Hello RBAC özellikleri. Bunlar genellikle hello "eylem" ve "rol" hello "scope." içerir |
| category |Merhaba olay kategorisi. Desteklenen değerler: yönetici, uyarı, güvenlik, ServiceHealth, öneri. |
| Arayan |Merhaba işlemi, UPN Talebi veya kullanılabilirliğine göre SPN talep gerçekleştiren hello kullanıcının e-posta adresi. Belirli sistem çağrıları için null olabilir. |
| correlationId |Genellikle bir GUID dize biçiminde. Correlationıd değeri olaylarla ait toohello aynı büyük eylemi ve genellikle bir correlationıd değeri paylaşın. |
| eventDescription |Merhaba Olay açıklaması statik metin. |
| eventDataId |Merhaba olay için benzersiz tanımlayıcı. |
| EventSource |Hello Azure hizmetine veya altyapı oluşturulan hello olayın adı. |
| httpRequest |Genellikle hello "clientRequestId", "clientIpAddress" ve "yöntem" içerir (örneğin PUT HTTP yöntemi). |
| düzeyi |Değerleri aşağıdaki hello birini: "Kritik", "Error"Uyarı",", "Bilgi" ve "Ayrıntılı." |
| Operationıd |Toosingle işlemi karşılık gelen hello olaylar arasında paylaşılan genellikle bir GUID. |
| operationName |Merhaba işlemin adı. |
| properties |Merhaba olay özellikleri. |
| durum |Dize. Merhaba işlem durumu. Genel değerler şunlardır: "Başlatıldı", "Sürüyor", "Başarılı", "Başarısız", "Active", "Çözülmüş". |
| alt durum |Genellikle hello karşılık gelen REST çağrısı hello HTTP durum kodunu içerir. Ayrıca, bir alt durum açıklayan diğer dizeleri de içerebilir. Ortak alt durum değerleri şunları içerir: Tamam (HTTP durum kodu: 200), oluşturulan (HTTP durum kodu: 201), kabul edilen (HTTP durum kodu: 202), Hayır içeriği (HTTP durum kodu: 204), hatalı istek (HTTP durum kodu: 400), bulunamadı (HTTP durum kodu: 404), çakışma (HTTP durum kodu: 409), iç sunucu hatası (HTTP durum kodu: 500), hizmet kullanılamıyor (HTTP durum kodu: 503), ağ geçidi zaman aşımı (HTTP durum kodu: 504) |

## <a name="next-steps"></a>Sonraki adımlar
* [Merhaba etkinlik günlüğü hakkında daha fazla bilgi edinin](monitoring-overview-activity-logs.md)
* [Azure Otomasyonu komut dosyaları (Runbook'lar) Azure uyarılar yürütme](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Bir Azure uyarıdan mantıksal uygulama toosend Twilio aracılığıyla bir SMS kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app). Bu örnek için ölçüm uyarılar, ancak bir etkinlik günlüğü uyarı ile değiştirilmiş toowork olabilir.
* [Mantıksal uygulama toosend Azure uyarı Slack iletiden kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app). Bu örnek için ölçüm uyarılar, ancak bir etkinlik günlüğü uyarı ile değiştirilmiş toowork olabilir.
* [Mantıksal uygulama toosend Azure bir uyarıdan ileti tooan Azure kuyruk kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app). Bu örnek için ölçüm uyarılar, ancak bir etkinlik günlüğü uyarı ile değiştirilmiş toowork olabilir.
