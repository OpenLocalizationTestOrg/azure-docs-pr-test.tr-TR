---
title: "Etkinlik günlüğü uyarıları kullanılan aaaUnderstand hello Web kancası şema | Microsoft Docs"
description: "Merhaba etkinlik günlüğü uyarı etkinleştirdiğinde tooa Web kancası URL'si gönderilen JSON Hello şeması hakkında bilgi edinin."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: 75562e0589222d3e392ea73eacfd7414a422d115
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a>Azure etkinlik günlüğü uyarılar için Web kancaları
Bir eylem grubu hello tanımının bir parçası olarak, Web kancası uç noktaları tooreceive etkinlik günlüğü uyarı bildirimleri yapılandırabilirsiniz. Web kancası ile bu bildirimleri tooother sistemleri işlem sonrası ya da özel eylemler için yönlendirebilirsiniz. Bu makalede hello HTTP POST tooa gibi görünüyor Web kancası için hangi hello yükü gösterilmektedir.

Etkinlik günlüğü uyarılar hakkında daha fazla bilgi için bkz. nasıl çok[Azure etkinlik günlüğü uyarı oluşturma](monitoring-activity-log-alerts.md).

Eylem grupları hakkında daha fazla bilgi için bkz. nasıl çok[Eylem grupları oluşturma](monitoring-action-groups.md).

## <a name="authenticate-hello-webhook"></a>Merhaba Web kancası kimlik doğrulaması
Merhaba Web kancası kimlik doğrulaması için isteğe bağlı olarak belirteç tabanlı bir yetkilendirme kullanabilirsiniz. URI kaydedilir belirteci Kimliğine sahip, örneğin, Web kancası hello `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.

## <a name="payload-schema"></a>Yükü şeması
Merhaba POST işlemine bulunan hello JSON yükü hello yükü'nın data.context.activityLog.eventSource alanında bulunan göre farklılık gösterir.

###<a name="common"></a>Ortak
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
###<a name="administrative"></a>Yönetim
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
###<a name="servicehealth"></a>ServiceHealth
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                }
            }
        },
        "properties": {}
    }
}
```

Belirli şeması hakkında ayrıntılı bilgi için hizmet sistem durumu bildirimi etkinlik günlüğü uyarıları görmek [hizmet durumu bildirimlerine](monitoring-service-notifications.md).

Belirli şeması hakkında ayrıntılı bilgi için diğer tüm etkinlik günlüğü uyarıları görmek [hello Azure etkinlik günlüğü'ne genel bakış](monitoring-overview-activity-logs.md).

| Öğe adı | Açıklama |
| --- | --- |
| durum |Ölçüm uyarılar için kullanılır. Her zaman "çok etkinlik günlüğü uyarıları için etkinleştirilmiş" ayarlayın. |
| bağlam |Merhaba olay bağlamı. |
| resourceProviderName |Merhaba Hello kaynak sağlayıcısı kaynak etkilenmiş. |
| Koşul türü |Her zaman "olayını." |
| ad |Merhaba uyarı kuralının adı. |
| id |Merhaba uyarı kaynak kimliği. |
| açıklama |Uyarı açıklaması Hello uyarı oluşturulduğunda ayarlayın. |
| subscriptionId |Azure abonelik kimliği |
| timestamp |Hangi hello olay hello hello istek işlenmeden Azure hizmeti tarafından oluşturulan saat. |
| resourceId |Kaynak Kimliğini hello kaynak etkilenmiş. |
| resourceGroupName |Merhaba hello kaynak grubunun adı, kaynak etkilenmiş. |
| properties |Kümesi `<Key, Value>` çiftleri (diğer bir deyişle, `Dictionary<String, String>`) hello olay ayrıntılarını içerir. |
| Olay |Merhaba olay hakkında meta veriler içeren öğe. |
| Yetkilendirme |Merhaba olay Hello rol tabanlı erişim denetimi özellikleri. Bu özellikler genellikle hello eylem, hello rolü ve hello kapsamı içerir. |
| category |Merhaba olay kategorisi. Yönetim, uyarı, güvenlik, ServiceHealth ve öneri desteklenen değerler içerir. |
| Arayan |Merhaba işlemi, UPN Talebi veya kullanılabilirliğine göre SPN talep gerçekleştiren hello kullanıcının e-posta adresi. Belirli sistem çağrıları için null olabilir. |
| correlationId |Genellikle bir GUID dize biçiminde. Correlationıd değeri olaylarla ait toohello aynı büyük eylemi ve genellikle bir correlationıd değeri paylaşın. |
| eventDescription |Merhaba Olay açıklaması statik metin. |
| eventDataId |Merhaba olay için benzersiz tanımlayıcı. |
| EventSource |Hello Azure hizmetine veya altyapı oluşturulan hello olayın adı. |
| httpRequest |Merhaba istek genellikle hello clientRequestId, clientIpAddress ve HTTP yöntemini içerir (örneğin, PUT). |
| düzeyi |Değerleri aşağıdaki hello birini: Kritik hata, uyarı, bilgilendirici ve ayrıntılı. |
| Operationıd |Toosingle işlemi karşılık gelen hello olaylar arasında paylaşılan genellikle bir GUID. |
| operationName |Merhaba işlemin adı. |
| properties |Merhaba olay özellikleri. |
| durum |Dize. Merhaba işlem durumu. Ortak değerleri başlatıldı, devam eden, başarılı, başarısız, etkin ve Çözümlenmiş içerir. |
| alt durum |Genellikle hello karşılık gelen REST çağrısı hello HTTP durum kodunu içerir. Ayrıca, bir alt durum açıklayan diğer dizeleri de içerebilir. Ortak substatus değerler Tamam (HTTP durum kodu: 200), oluşturulan (HTTP durum kodu: 201), kabul edilen (HTTP durum kodu: 202), Hayır içeriği (HTTP durum kodu: 204), hatalı istek (HTTP durum kodu: 400), bulunamadı (HTTP durum kodu: 404), çakışma (HTTP durum kodu: 409), iç sunucu hatası (HTTP durum kodu: 500), hizmet kullanılamıyor (HTTP durum kodu: 503) ve ağ geçidi zaman aşımı (HTTP durum kodu : 504). |

## <a name="next-steps"></a>Sonraki adımlar
* [Merhaba etkinlik günlüğü hakkında daha fazla bilgi](monitoring-overview-activity-logs.md).
* [Azure Otomasyon betikleri (Runbook'lar) Azure uyarılar yürütme](http://go.microsoft.com/fwlink/?LinkId=627081).
* [Bir Azure uyarıdan mantığı uygulama toosend Twilio aracılığıyla bir SMS kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app). Bu örnekte ölçüm uyarıları, ancak bir etkinlik günlüğü uyarı ile değiştirilmiş toowork olabilir.
* [Bir mantıksal uygulama toosend Azure uyarı Slack iletiden kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app). Bu örnekte ölçüm uyarıları, ancak bir etkinlik günlüğü uyarı ile değiştirilmiş toowork olabilir.
* [İleti tooan Azure kuyruk Azure bir uyarıdan mantığı uygulama toosend kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app). Bu örnekte ölçüm uyarıları, ancak bir etkinlik günlüğü uyarı ile değiştirilmiş toowork olabilir.
