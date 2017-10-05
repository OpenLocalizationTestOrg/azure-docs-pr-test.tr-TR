---
title: "Etkinlik günlüğü uyarıları kullanılan Web kancası şema anlama | Microsoft Docs"
description: "Bir etkinlik günlüğü uyarı etkinleştirdiğinde, bir Web kancası URL'si gönderilen JSON şeması hakkında bilgi edinin."
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
ms.openlocfilehash: 75c71bcd16573d4f4dd3377c623aa9b414aa3906
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a>Azure etkinlik günlüğü uyarılar için Web kancaları
Bir eylem grubu tanımının bir parçası olarak, etkinlik günlüğü uyarı bildirimlerini almak için Web kancası uç noktalarını yapılandırabilirsiniz. Web kancası ile işlem sonrası ya da özel eylemler için diğer sistemlere bu bildirimler yönlendirebilirsiniz. Bu makalede, bir Web kancası için HTTP POST için yükü nasıl göründüğünü gösterir.

Etkinlik günlüğü uyarılar hakkında daha fazla bilgi için bkz: nasıl yapılır [Azure etkinlik günlüğü uyarı oluşturma](monitoring-activity-log-alerts.md).

Eylem grupları hakkında daha fazla bilgi için bkz: nasıl yapılır [Eylem grupları oluşturma](monitoring-action-groups.md).

## <a name="authenticate-the-webhook"></a>Web kancası kimlik doğrulaması
Web kancası kimlik doğrulaması için isteğe bağlı olarak belirteç tabanlı bir yetkilendirme kullanabilirsiniz. URI kaydedilir belirteci Kimliğine sahip, örneğin, Web kancası `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.

## <a name="payload-schema"></a>Yükü şeması
POST işleminde yer alan JSON yükü yükü 's data.context.activityLog.eventSource alana göre farklılık gösterir.

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

Belirli şeması hakkında ayrıntılı bilgi için diğer tüm etkinlik günlüğü uyarıları görmek [Azure etkinlik günlüğü'ne genel bakış](monitoring-overview-activity-logs.md).

| Öğe adı | Açıklama |
| --- | --- |
| durum |Ölçüm uyarılar için kullanılır. Her zaman "etkinlik günlüğü uyarıları için etkinleştirilmiş" olarak ayarlayın. |
| bağlam |Olayın bağlamı. |
| resourceProviderName |Etkilenen kaynağının kaynak sağlayıcısı. |
| Koşul türü |Her zaman "olayını." |
| ad |Uyarı kuralı adı. |
| id |Uyarının kaynak kimliği. |
| Açıklama |Uyarı açıklaması uyarı oluşturulduğunda ayarlayın. |
| subscriptionId |Azure abonelik kimliği |
| timestamp |Olay istek işlenmeden Azure hizmeti tarafından oluşturulduğu saat. |
| resourceId |Etkilenen kaynağının kaynak kimliği. |
| resourceGroupName |Etkilenen kaynak kaynak grubu adı. |
| properties |Kümesi `<Key, Value>` çiftleri (diğer bir deyişle, `Dictionary<String, String>`) olay ayrıntılarını içerir. |
| Olay |Olay hakkında meta veriler içeren öğe. |
| Yetkilendirme |Olay rol tabanlı erişim denetimi özellikleri. Bu özellikler, eylem, rolü ve kapsamı genellikle içerir. |
| category |Olay kategorisi. Yönetim, uyarı, güvenlik, ServiceHealth ve öneri desteklenen değerler içerir. |
| Arayan |İşlem, UPN Talebi veya kullanılabilirliğine göre SPN talep gerçekleştiren kullanıcı e-posta adresi. Belirli sistem çağrıları için null olabilir. |
| correlationId |Genellikle bir GUID dize biçiminde. Correlationıd değeri olaylarla aynı büyük eyleme ait ve genellikle bir correlationıd değeri paylaşın. |
| eventDescription |Olay açıklaması statik metin. |
| eventDataId |Olay için benzersiz tanımlayıcı. |
| EventSource |Azure hizmet veya olayı oluşturan altyapı adı. |
| httpRequest |İstek genellikle clientRequestId, clientIpAddress ve HTTP yöntemini içerir (örneğin, PUT). |
| düzeyi |Aşağıdaki değerlerden birini: Kritik hata, uyarı, bilgilendirici ve ayrıntılı. |
| Operationıd |Tek bir işlem için karşılık gelen olayları arasında paylaşılan genellikle bir GUID. |
| operationName |İşlemin adı. |
| properties |Olay Özellikleri. |
| durum |Dize. İşlem durumu. Ortak değerleri başlatıldı, devam eden, başarılı, başarısız, etkin ve Çözümlenmiş içerir. |
| alt durum |Genellikle, karşılık gelen REST çağrısı HTTP durum kodunu içerir. Ayrıca, bir alt durum açıklayan diğer dizeleri de içerebilir. Ortak substatus değerler Tamam (HTTP durum kodu: 200), oluşturulan (HTTP durum kodu: 201), kabul edilen (HTTP durum kodu: 202), Hayır içeriği (HTTP durum kodu: 204), hatalı istek (HTTP durum kodu: 400), bulunamadı (HTTP durum kodu: 404), çakışma (HTTP durum kodu: 409), iç sunucu hatası (HTTP durum kodu: 500), hizmet kullanılamıyor (HTTP durum kodu: 503) ve ağ geçidi zaman aşımı (HTTP durum kodu : 504). |

## <a name="next-steps"></a>Sonraki adımlar
* [Etkinlik günlüğü hakkında daha fazla bilgi](monitoring-overview-activity-logs.md).
* [Azure Otomasyon betikleri (Runbook'lar) Azure uyarılar yürütme](http://go.microsoft.com/fwlink/?LinkId=627081).
* [Twilio aracılığıyla bir SMS gelen Azure uyarı göndermek için bir mantıksal uygulama kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app). Bu örnek için ölçüm uyarıları olmakla birlikte, bir etkinlik günlüğü uyarı ile çalışmak için değiştirilebilir.
* [Bir Azure uyarıdan Slack ileti göndermek için bir mantıksal uygulama kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app). Bu örnek için ölçüm uyarıları olmakla birlikte, bir etkinlik günlüğü uyarı ile çalışmak için değiştirilebilir.
* [Bir Azure uyarıdan bir Azure kuyruğuna ileti göndermek için bir mantıksal uygulama kullanmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app). Bu örnek için ölçüm uyarıları olmakla birlikte, bir etkinlik günlüğü uyarı ile çalışmak için değiştirilebilir.
