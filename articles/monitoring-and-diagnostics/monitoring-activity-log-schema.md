---
title: "Etkinlik günlüğü olay şeması aaaAzure | Microsoft Docs"
description: "Etkinlik günlüğü hello yayılan veriler için Hello olay şeması anlama"
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a>Azure etkinlik günlüğü olay şeması
Merhaba **Azure etkinlik günlüğü** Azure'da oluşan herhangi bir abonelik düzeyi olayı bir anlayış sağlar günlüktür. Bu makalede hello olay şema veri kategorisi başına açıklanmaktadır.

## <a name="administrative"></a>Yönetim
Bu kategorideki tüm hello kayıt içeren oluşturma, güncelleştirme, silme ve eylem işlemlerine Resource Manager aracılığıyla gerçekleştirilir. Bu kategorideki görür olay türleri dahil hello örnekleri "sanal makine oluşturma" ve "ağ güvenlik grubu bir kullanıcı tarafından gerçekleştirilen her eylem delete" veya Kaynak Yöneticisi'ni kullanarak uygulama belirli bir kaynak türü üzerinde bir işlemi olarak modellenir. Merhaba işlem türü ise yazma, silme veya eylem hello kayıtlarını hello başlangıç ve başarı veya işlemi hello yönetim kategorisinde kaydedilir başarısız. Merhaba yönetim kategorisi, ayrıca bir abonelikte herhangi bir değişiklik toorole tabanlı erişim denetimi içerir.

### <a name="sample-event"></a>Örnek olayı
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a>Özellik açıklamaları
| Öğe adı | Açıklama |
| --- | --- |
| Yetkilendirme |BLOB hello olay RBAC özelliklerinin. Genellikle hello "eylem", "rol" ve "scope" özellikleri içerir. |
| Arayan |Merhaba işlemi, UPN Talebi veya kullanılabilirliğine göre SPN talep yürüttü hello kullanıcının e-posta adresi. |
| Kanalları |Değerleri aşağıdaki hello birini: "Yönetici", "İşlem" |
| Talepleri |Merhaba JWT belirteci Kaynak Yöneticisi'nde bu işlem Active Directory tooauthenticate hello kullanıcı veya uygulama tooperform tarafından kullanılır. |
| correlationId |Genellikle bir GUID hello dize biçiminde. Bir correlationıd değeri paylaşan olayları ait toohello aynı uber eylemi. |
| Açıklama |Olay açıklaması statik metin. |
| eventDataId |Bir olay benzersiz tanımlayıcısı. |
| httpRequest |BLOB açıklayan hello Http isteği. Merhaba "clientRequestId", "clientIpAddress" ve "yöntem" (HTTP yöntemi. genellikle içerir For example, PUT). |
| düzeyi |Merhaba olay düzeyi. Değerleri aşağıdaki hello birini: "Kritik", "Error"Uyarı",", "Bilgi" ve "Ayrıntılı" |
| resourceGroupName |Merhaba hello kaynak grubunun adı, kaynak etkilenmiş. |
| resourceProviderName |Kaynak hello kaynak sağlayıcısının adını hello için etkilenen |
| resourceId |Kaynak kimliğini hello kaynak etkilenmiş. |
| Operationıd |Tooa tek bir işlem karşılık gelen hello olayları arasında paylaşılan bir GUID. |
| operationName |Merhaba işlemin adı. |
| properties |Kümesi `<Key, Value>` hello hello olay ayrıntılarını açıklayan çiftleri (diğer bir deyişle, bir sözlük). |
| durum |Merhaba hello işlemi durumunu açıklayan dize. Bazı genel değerler şunlardır:, ilerleme, başarılı, başarısız, etkin, çözümlenmiş başlatıldı. |
| alt durum |Genellikle hello REST çağrısı karşılık gelen HTTP durum kodunu Merhaba, ancak bu ortak değerleri gibi bir alt durum açıklayan diğer dizeleri de içerir: Tamam (HTTP durum kodu: 200), oluşturulan (HTTP durum kodu: 201), kabul edilen (HTTP durum kodu: 202), içerik yok (HTTP Durum kodu: 204), hatalı istek (HTTP durum kodu: 400), bulunamadı (HTTP durum kodu: 404), çakışma (HTTP durum kodu: 409), iç sunucu hatası (HTTP durum kodu: 500), hizmet kullanılamıyor (HTTP durum kodu: 503), ağ geçidi zaman aşımı (HTTP durum kodu: 504). |
| eventTimestamp |Merhaba olay hello Azure hizmetini işleme hello tarafından oluşturulan zaman damgası karşılık gelen hello olay isteği. |
| submissionTimestamp |Merhaba olay sorgulama için kullanılabilir duruma zaman damgası. |
| subscriptionId |Azure abonelik kimliği |

## <a name="service-health"></a>Hizmet durumu
Bu kategori, Azure'da oluşan herhangi bir hizmet durumu olay hello kaydını içerir. Bu kategorideki görür olay hello türü "SQL Azure Doğu ABD kesinti yaşanıyor." örneğidir Hizmet sistem durumu olayları beş çeşit olarak gelir: eylem gerekli, Destekli kurtarma, olay, bakım, bilgi veya güvenlik ve hello olay tarafından etkilenen hello Abonelikteki bir kaynağınız varsa yalnızca görünür.

### <a name="sample-event"></a>Örnek olayı
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a>Özellik açıklamaları
Öğe adı | Açıklama
-------- | -----------
Kanalları | Değerleri aşağıdaki hello biridir: "Yönetici", "İşlem"
correlationId | Genellikle bir hello dize biçimindeki GUID'dir. Olaylar, ile ait aynı uber eylemi genellikle paylaşmak toohello hello aynı correlationıd değeri.
Açıklama | Merhaba Olay açıklaması.
eventDataId | bir olayın Hello benzersiz tanımlayıcısı.
EventName | Merhaba olay Hello başlığı.
düzeyi | Merhaba olay düzeyi. Değerleri aşağıdaki hello birini: "Kritik", "Error"Uyarı",", "Bilgi" ve "Ayrıntılı"
resourceProviderName | Merhaba kaynak sağlayıcısının adını hello için kaynak etkilenmiş. Bilinmiyor, bu boş olacaktır.
Kaynak türü| Merhaba, kaynak Hello türü kaynak etkilenmiş. Bilinmiyor, bu boş olacaktır.
alt durum | Genellikle hizmet sistem durumu olayları için null.
eventTimestamp | Merhaba günlük olay oluşturuldu ve toohello etkinlik günlüğü gönderilen zaman damgası.
submissionTimestamp |   Merhaba olay hello etkinlik günlüğü kullanılabilen zaman damgası.
subscriptionId | Bu olayın günlüğe yazıldığı Azure aboneliği hello.
durum | Merhaba hello işlemi durumunu açıklayan dize. Bazı genel değerler şunlardır: etkin, çözüldü.
operationName | Merhaba işlemin adı. Genellikle Microsoft.ServiceHealth/incident/action.
category | "ServiceHealth"
resourceId | Kaynak kimliğini hello kaynağı biliniyorsa etkilenmiş. Abonelik kimliği aksi sağlanır.
Properties.Title | Bu iletişim için yerelleştirilmiş hello başlığı. İngilizce hello varsayılan dildir.
Properties.Communication | Merhaba, HTML biçimlendirmesi ile Merhaba iletişim ayrıntılarını yerelleştirilmiş. İngilizce hello varsayılandır.
Properties.incidentType | Olası değerler: AssistedRecovery, ActionRequired, bilgi, olay, bakım, güvenlik
Properties.trackingId | Bu olay ile ilişkilendirilmiş hello olay tanımlar. Bu toocorrelate hello olayları ilgili tooan olayı kullanın.
Properties.impactedServices | Merhaba Hizmetleri ve hello olaydan etkilenen bölgeler açıklar bir kaçış karakterli JSON blobu. Her biri bir ServiceName ve her biri bir RegionName sahip ImpactedRegions listesini sahip hizmetlerin listesini.
Properties.defaultLanguageTitle | İngilizce Hello iletişimi
Properties.defaultLanguageContent | html biçimlendirmesi veya düz metin olarak İngilizce Hello iletişimi
Properties.Stage | AssistedRecovery, ActionRequired, bilgi, olay, güvenlik için olası değerler: etkin, olan çözümlendi. Bakım için oldukları: etkin, planlanmış, devam ediyor, iptal edildi, Rescheduled, çözümlenmiş, tamamlandı
Properties.communicationId | Bu olay Hello iletişimi ilişkilidir.

## <a name="alert"></a>Uyarı
Bu kategorideki tüm etkinleştirmeleri Azure uyarıların hello kaydını içerir. Bu kategorideki görür olay hello türü "myVM CPU % son 5 dakika boyunca hello 80 bırakıldı." örneğidir Azure sistemleri çeşitli sahip bir uyarı verme kavramı--bir kural çeşit tanımlayabilir ve bu kural için koşullara uyan bir bildirim alıyorsunuz. Her bir desteklenen Azure uyarı türü 'etkinleştirir,' veya hello koşullar sağlanmadığı toogenerate bir bildirim, hello etkinleştirme kaydını da hello etkinlik günlüğü toothis kategorisini gönderilir.

### <a name="sample-event"></a>Örnek olayı

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a>Özellik açıklamaları
| Öğe adı | Açıklama |
| --- | --- |
| Arayan | Her zaman Microsoft.Insights/alertRules |
| Kanalları | Her zaman "Yönetici, işlemi" |
| Talepleri | JSON blob hello uyarı altyapısı hello SPN (hizmet asıl adı) ya da kaynak türüne sahip. |
| correlationId | Merhaba dize biçiminde bir GUID. |
| Açıklama |Merhaba uyarı Olay açıklaması statik metin. |
| eventDataId |Merhaba uyarı olay benzersiz tanımlayıcısı. |
| düzeyi |Merhaba olay düzeyi. Değerleri aşağıdaki hello birini: "Kritik", "Error"Uyarı",", "Bilgi" ve "Ayrıntılı" |
| resourceGroupName |Ölçüm uyarı ise hello hello kaynak grubunun adı kaynak etkilenmiş. Diğer uyarı türleri için bu hello hello uyarı kendisini içeren hello kaynak grubunun adıdır. |
| resourceProviderName |Ölçüm uyarı ise hello kaynak sağlayıcısının adını hello için kaynak etkilenmiş. Diğer uyarı türleri için bu hello hello kaynak sağlayıcısı hello uyarı kendisi için adıdır. |
| resourceId | Ölçüm uyarı ise hello hello kaynak kimliği adını kaynak etkilenmiş. Diğer uyarı türleri için uyarı kaynağın hello kendisini hello kaynak kimliği budur. |
| Operationıd |Tooa tek bir işlem karşılık gelen hello olayları arasında paylaşılan bir GUID. |
| operationName |Merhaba işlemin adı. |
| properties |Kümesi `<Key, Value>` hello hello olay ayrıntılarını açıklayan çiftleri (diğer bir deyişle, bir sözlük). |
| durum |Merhaba hello işlemi durumunu açıklayan dize. Bazı genel değerler şunlardır:, ilerleme, başarılı, başarısız, etkin, çözümlenmiş başlatıldı. |
| alt durum | Genellikle uyarılar için null. |
| eventTimestamp |Merhaba olay hello Azure hizmetini işleme hello tarafından oluşturulan zaman damgası karşılık gelen hello olay isteği. |
| submissionTimestamp |Merhaba olay sorgulama için kullanılabilir duruma zaman damgası. |
| subscriptionId |Azure abonelik kimliği |

### <a name="properties-field-per-alert-type"></a>Uyarı türü başına özellikleri alanı
Merhaba özellikleri alanı hello uyarı olayının hello kaynağı bağlı olarak farklı değerler içerir. İki ortak uyarı Olay Etkinlik günlüğü uyarıları ve ölçüm uyarıları sağlayıcılarıdır.

#### <a name="properties-for-activity-log-alerts"></a>Etkinlik günlüğü uyarıların özellikleri
| Öğe adı | Açıklama |
| --- | --- |
| properties.subscriptionId | etkinleştirilen bu etkinlik günlüğü uyarı kuralı toobe neden hello etkinlik günlüğü olayı Hello abonelik kimliği. |
| properties.eventDataId | Merhaba olay verileri Kimliğinden etkinleştirilen bu etkinlik günlüğü uyarı kuralı toobe neden hello etkinlik günlüğü olayı. |
| properties.resourceGroup | Kaynak grubundan etkinleştirilen bu etkinlik günlüğü uyarı kuralı toobe neden hello etkinlik günlüğü olayı Hello. |
| properties.resourceId | etkinleştirilen bu etkinlik günlüğü uyarı kuralı toobe neden hello etkinlik günlüğü olayı Hello kaynak kimliği. |
| properties.eventTimestamp | etkinleştirilen bu etkinlik günlüğü uyarı kuralı toobe neden hello etkinlik günlüğü olay Hello olay zaman damgası. |
| properties.operationName | etkinleştirilen bu etkinlik günlüğü uyarı kuralı toobe neden hello etkinlik günlüğü olayı Hello işlemi adı. |
| Properties.Status | etkinleştirilen bu etkinlik günlüğü uyarı kuralı toobe neden hello etkinlik günlüğü olayı durumundan Hello.|

#### <a name="properties-for-metric-alerts"></a>Ölçüm uyarıların özellikleri
| Öğe adı | Açıklama |
| --- | --- |
| Özellikler. RuleUri | Merhaba ölçüm uyarı kuralı kendisini kaynak kimliği. |
| Özellikler. RuleName | Merhaba ölçüm uyarı kuralı Hello adı. |
| Özellikler. RuleDescription | Merhaba ölçüm uyarı kuralı (Merhaba uyarı kuralı tanımlanan) Hello açıklaması. |
| Özellikler. Eşik | Merhaba ölçüm uyarı kuralı Hello hesaplanmasında kullanılan hello eşik değeri. |
| Özellikler. WindowSizeInMinutes | Merhaba ölçüm uyarı kuralı Hello hesaplanmasında kullanılan hello pencere boyutu. |
| Özellikler. Toplama | Merhaba ölçüm uyarı kuralda tanımlanan hello toplama türü. |
| Özellikler. İşleci | Merhaba ölçüm uyarı kuralı Hello hesaplanmasında kullanılan hello koşullu işleç. |
| Özellikler. MetricName | Merhaba hello ölçüm uyarı kuralı hello hesaplanmasında kullanılan hello ölçüsünün ölçüm adı. |
| Özellikler. MetricUnit | ölçü birimi hello ölçüm uyarı kuralı hello hesaplanmasında kullanılan hello ölçümünü Hello. |

## <a name="autoscale"></a>Otomatik Ölçeklendirme
Bu kategori, aboneliğinizde tanımladığınız herhangi bir otomatik ölçeklendirme ayarı göre hello otomatik ölçeklendirme altyapısının herhangi bir olayları ilgili toohello işlem hello kaydını içerir. Bu kategorideki görür olay hello türü "Otomatik ölçeklendirme ölçek büyütme eylemi başarısız oldu." örneğidir Otomatik ölçeklendirme'ni kullanarak, otomatik olarak ölçeğini veya ölçeklendirmek hello desteklenen kaynak türü örneği sayısı dayalı bir otomatik ölçeklendirme ayarı kullanarak gün ve/veya yük (ölçüm) verileri zamanında. Hello koşullar karşılandığında tooscale yukarı veya aşağı başlangıç hello ve başarılı veya başarısız olayları bu kategorideki kaydedilmez.

### <a name="sample-event"></a>Örnek olayı
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a>Özellik açıklamaları
| Öğe adı | Açıklama |
| --- | --- |
| Arayan | Her zaman Microsoft.Insights/autoscaleSettings |
| Kanalları | Her zaman "Yönetici, işlemi" |
| Talepleri | JSON blob hello hello otomatik ölçeklendirme altyapısı SPN (hizmet asıl adı) ya da kaynak türüne sahip. |
| correlationId | Merhaba dize biçiminde bir GUID. |
| Açıklama |Merhaba otomatik ölçeklendirme Olay açıklaması statik metin. |
| eventDataId |Merhaba otomatik ölçeklendirme olay benzersiz tanımlayıcısı. |
| düzeyi |Merhaba olay düzeyi. Değerleri aşağıdaki hello birini: "Kritik", "Error"Uyarı",", "Bilgi" ve "Ayrıntılı" |
| resourceGroupName |Merhaba otomatik ölçeklendirme ayarı hello kaynak grubunun adı. |
| resourceProviderName |Merhaba otomatik ölçeklendirme ayarı hello kaynak sağlayıcısı adı. |
| resourceId |Merhaba otomatik ölçeklendirme ayarı kaynak kimliği. |
| Operationıd |Tooa tek bir işlem karşılık gelen hello olayları arasında paylaşılan bir GUID. |
| operationName |Merhaba işlemin adı. |
| properties |Kümesi `<Key, Value>` hello hello olay ayrıntılarını açıklayan çiftleri (diğer bir deyişle, bir sözlük). |
| Özellikler. Açıklama | Hangi hello otomatik ölçeklendirme altyapısı yapmakta olduğu ayrıntılı açıklaması. |
| Özellikler. ResourceName | Kaynak Kimliğini hello etkilenen kaynak (üzerinde hangi hello ölçek eylemi gerçekleştirilir kaynak hello) |
| Özellikler. OldInstancesCount | Merhaba hello otomatik ölçeklendirme eylemi önce örneklerinin sayısını etkisi sürdü. |
| Özellikler. NewInstancesCount | Merhaba hello otomatik ölçeklendirme eylemin etkisi sonra örneği sayısı. |
| Özellikler. LastScaleActionTime | Merhaba otomatik ölçeklendirme eylemi gerçekleştiği, hello zaman damgası. |
| durum |Merhaba hello işlemi durumunu açıklayan dize. Bazı genel değerler şunlardır:, ilerleme, başarılı, başarısız, etkin, çözümlenmiş başlatıldı. |
| alt durum | Genellikle otomatik ölçeklendirme için null. |
| eventTimestamp |Merhaba olay hello Azure hizmetini işleme hello tarafından oluşturulan zaman damgası karşılık gelen hello olay isteği. |
| submissionTimestamp |Merhaba olay sorgulama için kullanılabilir duruma zaman damgası. |
| subscriptionId |Azure abonelik kimliği |

## <a name="next-steps"></a>Sonraki adımlar
* [Merhaba etkinlik günlüğü (önceki adıyla denetim günlüklerini) hakkında daha fazla bilgi edinin](monitoring-overview-activity-logs.md)
* [Hello Azure etkinlik günlüğü tooEvent hub akışı](monitoring-stream-activity-logs-event-hubs.md)
