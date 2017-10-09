---
title: "aaaArchive hello Azure etkinlik günlüğü | Microsoft Docs"
description: "Tooarchive Azure etkinliklerinizi nasıl oturum depolama hesabındaki uzun vadeli bekletme için öğrenin."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a>Arşiv hello Azure etkinlik günlüğü
Bu makalede, biz hello Azure portal, PowerShell cmdlet'lerini veya platformlar arası CLI tooarchive nasıl kullanabileceğinizi gösterir, [ **Azure etkinlik günlüğü** ](monitoring-overview-activity-logs.md) depolama hesabındaki. Bu seçenek (ile Merhaba bekletme ilkesi üzerinde tam denetim) 90 gün boyunca daha uzun, etkinlik günlüğü, statik çözümleme denetim veya yedekleme tooretain istiyorsanız yararlıdır. Tooretain yalnızca gerekiyorsa, olayları 90 gün veya daha az, etkinlik günlüğü olaylarını arşivleme etkinleştirmeden hello Azure platformu 90 gün boyunca tutulur beri tooset arşivleme tooa depolama hesabı, gerek yoktur.

## <a name="prerequisites"></a>Ön koşullar
Başlamadan önce çok ihtiyacınız[depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) arşiv etkinlik günlüğü toowhich. Böylece daha iyi erişim toomonitoring veri denetimi içinde depolanmış, diğer izleme olmayan verilere sahip varolan bir depolama hesabı kullanmamanızı öneririz. Tanılama günlüklerini ve ölçümleri tooa depolama hesabı arşivlemeye çalışıyorsunuz, etkinlik günlüğü için de tookeep tüm izleme verilerini merkezi bir konumda ancak, bu algılama toouse bu depolama hesabı kalmasına neden olabilir. kullandığınız hello depolama hesabı, genel amaçlı depolama hesabı, blob storage hesabı olması gerekir. Merhaba depolama hesabı hello toobe yok uygun RBAC erişim tooboth abonelikleri hello ayarı yapılandıran hello kullanıcının sahip olduğu sürece günlükleri yayma hello abonelik aynı abonelik.

## <a name="log-profile"></a>Günlük profili
tooarchive hello etkinlik günlüğü hello aşağıdaki yöntemlerden birini kullanarak, ayarladığınız hello **günlük profili** aboneliği. Merhaba günlük profili hello depolanan ya da akışı olayların türünü tanımlar ve hello çıkışları — depolama hesabı ve/veya olay hub'ı. Ayrıca bir depolama hesabında depolanan olayları için hello bekletme ilkesi (gün tooretain sayısı) tanımlar. Merhaba bekletme ilkesi toozero ayarlarsanız, olaylar süresiz olarak depolanır. Aksi takdirde, bu tooany değerinin 1 ile 2147483647 arasında ayarlanabilir. Bekletme ilkeleri uygulanan gün başına, hello bitiş saati (UTC) oturum şekilde hello bekletme ilkesi sunulmuştur hello günden silinir. Bir günlük bir Bekletme İlkesi nesneniz varsa, örneğin, bugün hello günün hello başında hello hello gün dünden günlüklerinden silinecek. [Daha fazla bilgiyi hakkında günlük profilleri burada](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile). 

## <a name="archive-hello-activity-log-using-hello-portal"></a>Arşiv hello hello portal kullanarak Etkinlik günlüğü
1. Merhaba Hello Portalı'nda tıklatın **etkinlik günlüğü** hello sol taraftaki gezinti bağlantısına. Merhaba etkinlik günlüğü için bir bağlantı görmüyorsanız, hello tıklatın **daha Hizmetleri** ilk bağlantı.
   
    ![TooActivity günlük dikey gidin](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. Merhaba dikey penceresinde Hello üstünde tıklatın **verme**.
   
    ![Merhaba Dışa Aktar düğmesini tıklatın](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. Merhaba kutuyu için görünür hello dikey penceresinde, **verme tooa depolama hesabı** ve bir depolama hesabı seçin.
   
    ![Bir depolama hesabı ayarlama](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. Merhaba kaydırıcı veya metin kutusunu kullanarak, depolama hesabınızı etkinlik günlüğü olaylarını tutulmalıdır gün sayısı tanımlayın. Verilerinizi hello depolama hesabında süresiz olarak kalıcı toohave tercih ederseniz, bu sayı toozero ayarlayın.
5. **Kaydet** düğmesine tıklayın.

## <a name="archive-hello-activity-log-via-powershell"></a>Arşiv hello PowerShell aracılığıyla etkinlik günlüğü
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| Özellik | Gerekli | Açıklama |
| --- | --- | --- |
| StorageAccountId |Hayır |Kaynak Kimliğini hello depolama hesabı toowhich etkinlik günlükleri kaydedilmesi gerekir. |
| Konumlar |Evet |Toocollect etkinlik günlüğü olaylarını istediğiniz bölgeler virgülle ayrılmış listesi. Tüm bölgelerin bir listesi görüntüleyebilirsiniz [bu sayfasını ziyaret tarafından](https://azure.microsoft.com/en-us/regions) veya kullanarak [Azure Yönetimi REST API hello](https://msdn.microsoft.com/library/azure/gg441293.aspx). |
| retentionInDays |Evet |Hangi olayların tutulacağını için 1 ile 2147483647 arasında gün sayısı. Sıfır değeri hello günlükleri süresiz olarak depolar (sürekli). |
| Kategoriler |Evet |Toplanması gereken olay kategorileri virgülle ayrılmış listesi. Olası değerler şunlardır: yazma, silme ve eylem. |

## <a name="archive-hello-activity-log-via-cli"></a>Arşiv hello CLI aracılığıyla etkinlik günlüğü
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| Özellik | Gerekli | Açıklama |
| --- | --- | --- |
| ad |Evet |Günlük profilinin adı. |
| storageId |Hayır |Kaynak Kimliğini hello depolama hesabı toowhich etkinlik günlükleri kaydedilmesi gerekir. |
| Konumları |Evet |Toocollect etkinlik günlüğü olaylarını istediğiniz bölgeler virgülle ayrılmış listesi. Tüm bölgelerin bir listesi görüntüleyebilirsiniz [bu sayfasını ziyaret tarafından](https://azure.microsoft.com/en-us/regions) veya kullanarak [Azure Yönetimi REST API hello](https://msdn.microsoft.com/library/azure/gg441293.aspx). |
| retentionInDays |Evet |Hangi olayların tutulacağını için 1 ile 2147483647 arasında gün sayısı. Sıfır değeri hello günlükleri süresiz olarak depolar (sürekli). |
| kategorileri |Evet |Toplanması gereken olay kategorileri virgülle ayrılmış listesi. Olası değerler şunlardır: yazma, silme ve eylem. |

## <a name="storage-schema-of-hello-activity-log"></a>Merhaba etkinlik günlüğü depolama şeması
Arşivleme kurduktan sonra bir etkinlik günlüğü olay oluştuktan hemen sonra bir depolama kapsayıcısı hello depolama hesabı oluşturulur. Merhaba BLOB'lar hello kapsayıcı içindeki aynı hello etkinlik günlüğü ve tanılama günlüklerini arasında biçimi hello izleyin. Bu BLOB Hello yapıdır:

> Öngörüler-işletimsel-günlükleri/name = varsayılan/ResourceId/ABONELİKLERİ = / {abonelik kimliği} / y = {dört basamaklı sayısal year} / m = {iki basamaklı sayısal ay} / d = {iki basamaklı sayısal günü} / h {iki basamaklı 24 saatlik hour}/m=00/PT1H.json =
> 
> 

Örneğin, bir blob adı olabilir:

> insights-Operational-Logs/Name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.JSON
> 
> 

Her bir PT1H.json blob hello blob URL'SİNDE belirtilen hello saat içinde gerçekleşen olayların JSON blobu içerir (örneğin h = 12). Bunlar ortaya çıktığında hello mevcut saat sırasında eklenmiş toohello PT1H.json dosya olaylardır. Merhaba dakika değeri (m 00 =) her zaman etkinlik günlüğü olaylarını tek tek bloblar saat başına ayrılmış bu yana 00.

Merhaba PT1H.json dosyası içinde her olay bu biçim aşağıdaki hello "kayıtlar" dizisinde depolanır:

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
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
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
            }
        }
    ]
}
```


| Öğe adı | Açıklama |
| --- | --- |
| time |Merhaba olay hello Azure hizmetini işleme hello tarafından oluşturulan zaman damgası karşılık gelen hello olay isteği. |
| resourceId |Kaynak Kimliğini hello kaynak etkilenmiş. |
| operationName |Merhaba işlemin adı. |
| category |Merhaba eylem kategorisi örn. Yazma, okuma, eylem. |
| resultType |Merhaba Hello türü neden, örn. Başarılı, başarısız, Başlat |
| resultSignature |Merhaba kaynak türüne bağlıdır. |
| durationMs |Milisaniye cinsinden hello işlemi süresi |
| callerIpAddress |Merhaba işlemi, UPN Talebi veya kullanılabilirliğine göre SPN talep yürüttü hello kullanıcının IP adresi. |
| correlationId |Genellikle bir GUID hello dize biçiminde. Bir correlationıd değeri paylaşan olayları ait toohello aynı uber eylemi. |
| identity |JSON blob Hello yetkilendirme ve talep açıklayan. |
| Yetkilendirme |BLOB hello olay RBAC özelliklerinin. Genellikle hello "eylem", "rol" ve "scope" özellikleri içerir. |
| düzeyi |Merhaba olay düzeyi. Değerleri aşağıdaki hello birini: "Kritik", "Error"Uyarı",", "Bilgi" ve "Ayrıntılı" |
| location |Bölge hangi hello konumda oluştu (veya genel). |
| properties |Kümesi `<Key, Value>` hello hello olay ayrıntılarını açıklayan çiftleri (yani sözlük). |

> [!NOTE]
> Merhaba özellikleri ve bu özellikleri kullanımını hello kaynak bağlı olarak değişebilir.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* [BLOB'ları çözümleme için karşıdan yükle](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [Merhaba etkinlik günlüğü tooEvent hub akışı](monitoring-stream-activity-logs-event-hubs.md)
* [Merhaba etkinlik günlüğü hakkında daha fazla bilgi](monitoring-overview-activity-logs.md)

