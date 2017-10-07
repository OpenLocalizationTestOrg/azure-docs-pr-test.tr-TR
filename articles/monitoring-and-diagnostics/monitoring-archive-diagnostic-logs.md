---
title: "aaaArchive Azure tanılama günlükleri | Microsoft Docs"
description: "Nasıl tooarchive bir depolama hesabı, uzun vadeli bekletme için Azure tanılama günlükleri öğrenin."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 3a55c73f-2ef3-45f3-8956-bcf9c0cb7e05
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: bc9edbd3a649023a728b7fe77130dba2b6e6370d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="archive-azure-diagnostic-logs"></a>Arşiv Azure tanılama günlükleri
Bu makalede, nasıl hello Azure portal, PowerShell cmdlet'leri, CLI, kullanın veya REST API tooarchive gösteriyoruz, [Azure tanılama günlüklerini](monitoring-overview-of-diagnostic-logs.md) depolama hesabındaki. Bu seçenek, Denetim, statik çözümleme veya yedekleme için bir isteğe bağlı bekletme ilkesi ile tanılama günlükleri tooretain istiyorsanız yararlıdır. Merhaba depolama hesabı hello toobe yok uygun RBAC erişim tooboth abonelikleri hello ayarı yapılandıran hello kullanıcının sahip olduğu sürece günlükleri yayma hello kaynak aynı abonelik.

## <a name="prerequisites"></a>Ön koşullar
Başlamadan önce çok ihtiyacınız[depolama hesabı oluşturma](../storage/storage-create-storage-account.md) tanılama günlüklerinize arşiv toowhich. Böylece daha iyi erişim toomonitoring veri denetimi içinde depolanmış, diğer izleme olmayan verilere sahip varolan bir depolama hesabı kullanmamanızı öneririz. Ayrıca Tanılama ölçümleri tooa depolama hesabı ve etkinlik günlüğü arşivleme, tanılama tookeep de merkezi bir konumda tüm izleme verilerini günlükleri için ancak, bu algılama toouse bu depolama hesabı kalmasına neden olabilir. kullandığınız hello depolama hesabı, genel amaçlı depolama hesabı, blob storage hesabı olması gerekir.

## <a name="diagnostic-settings"></a>Tanılama ayarları
Merhaba aşağıdaki yöntemlerden birini kullanarak, tanılama günlüklerini tooarchive, ayarladığınız bir **tanılama ayarını** belirli bir kaynak için. Kaynağın tanılama ayarını günlükleri hello kategorilerini tanımlar ve ölçüm verileri tooa hedef (depolama hesabı, olay hub'ları ad alanı veya günlük analizi) gönderilir. Ayrıca her bir günlük kategorisi ve ölçüm verileri bir depolama hesabında depolanan olayları için hello bekletme ilkesi (gün tooretain sayısı) tanımlar. Bir bekletme ilkesi toozero ayarlarsanız, bu günlüğü kategori olaylar (yani toosay, sonsuza kadar) süresiz olarak depolanır. Bir bekletme ilkesi, aksi takdirde herhangi bir sayıda gün 1 ile 2147483647 arasında olabilir. [Daha fazla bilgiyi burada tanılama ayarları hakkında](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings). Bekletme ilkeleri uygulanan gün başına, hello bitiş saati (UTC) oturum şekilde hello bekletme ilkesi sunulmuştur hello günden silinir. Bir günlük bir Bekletme İlkesi nesneniz varsa, örneğin, bugün hello günün hello başında hello hello gün dünden günlüklerinden silinecek

## <a name="archive-diagnostic-logs-using-hello-portal"></a>Merhaba portal kullanarak arşiv tanılama günlükleri
1. Merhaba portalında tooAzure İzleyici gidin ve tıklayın **tanılama ayarları**

    ![Azure İzleyicisi İzleme bölümü](media/monitoring-archive-diagnostic-logs/diagnostic-settings-blade.png)

2. İsteğe bağlı olarak kaynak grubu veya kaynak türü tarafından hello listesini filtrelemek ve tooset tanılama ayarını istediğiniz hello kaynakta'i tıklatın.

3. Hiçbir ayar seçmiş olduğunuz hello kaynakta mevcut, istendiğinde toocreate bir ayar demektir. "Tanılamayı açın."'i tıklatın

   ![Tanılama ayarını - ayar Ekle](media/monitoring-archive-diagnostic-logs/diagnostic-settings-none.png)

   Merhaba kaynakta mevcut ayarları varsa, bu kaynak üzerinde zaten yapılandırılmış ayarları listesini görürsünüz. "Tanılama ayarını Ekle" yi tıklatın.

   ![Tanılama ayarını ayarlar varolan - Ekle](media/monitoring-archive-diagnostic-logs/diagnostic-settings-multiple.png)

3. Ayarı, bir ad verin ve hello kutuyu **tooStorage hesap verme**, bir depolama hesabı seçin. İsteğe bağlı olarak, bu günlükler ayarlamak hello kullanarak birkaç gün tooretain **bekletme (gün)** kaydırıcılar. Sıfır gün bekletme hello günlükleri süresiz olarak depolar.
   
   ![Tanılama ayarını ayarlar varolan - Ekle](media/monitoring-archive-diagnostic-logs/diagnostic-settings-configure.png)
    
4. **Kaydet** düğmesine tıklayın.

Hello yeni ayar birkaç dakika sonra bu kaynak için ayarları listesi görüntülenir ve tanılama günlüklerin arşivlenmiş toothat depolama üretilen yeni olay verilerini hemen hesap.

## <a name="archive-diagnostic-logs-via-azure-powershell"></a>Azure PowerShell aracılığıyla arşiv tanılama günlükleri
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| Özellik | Gerekli | Açıklama |
| --- | --- | --- |
| ResourceId |Evet |Kaynak Kimliği hello kaynağın tanılama ayarını tooset istiyor. |
| StorageAccountId |Hayır |Kaynak Kimliğini hello depolama hesabı toowhich tanılama günlüklerini kaydedilmesi gerekir. |
| Kategoriler |Hayır |Günlük kategorileri tooenable virgülle ayrılmış listesi. |
| Etkin |Evet |Tanılama etkin veya bu kaynağa devre dışı olup olmadığını gösteren bir Boole değeri. |
| RetentionEnabled |Hayır |Bir bekletme ilkesi bu kaynakta etkin olmadığını gösteren bir Boole değeri. |
| retentionInDays |Hayır |Kendisi için olayları 1 ile 2147483647 arasında korunması gereken gün sayısı. Sıfır değeri hello günlükleri süresiz olarak depolar. |

## <a name="archive-diagnostic-logs-via-hello-cross-platform-cli"></a>Merhaba platformlar arası CLI aracılığıyla arşiv tanılama günlükleri
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| Özellik | Gerekli | Açıklama |
| --- | --- | --- |
| resourceId |Evet |Kaynak Kimliği hello kaynağın tanılama ayarını tooset istiyor. |
| storageId |Hayır |Kaynak Kimliği hello depolama hesabı toowhich tanılama günlüklerinin kaydedilmesi gerekir. |
| kategorileri |Hayır |Günlük kategorileri tooenable virgülle ayrılmış listesi. |
| Etkin |Evet |Tanılama etkin veya bu kaynağa devre dışı olup olmadığını gösteren bir Boole değeri. |

## <a name="archive-diagnostic-logs-via-hello-rest-api"></a>Merhaba REST API aracılığıyla arşiv tanılama günlükleri
[Bu belgede bakın](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) hello Azure İzleyici REST API'sini kullanarak tanılama ayarlama nasıl ayarlanacağı hakkında bilgi için.

## <a name="schema-of-diagnostic-logs-in-hello-storage-account"></a>Tanılama günlüklerini hello depolama hesabındaki şeması
Arşivleme ayarlamış olduğunuz sonra etkinleştirdiğiniz hello günlük kategorilerden birini olay oluştuktan hemen sonra bir depolama kapsayıcısı hello depolama hesabı oluşturulur. Merhaba BLOB'lar hello kapsayıcı içindeki aynı arasında tanılama günlüklerini biçimi hello ve hello etkinlik günlüğü izleyin. Bu BLOB Hello yapıdır:

> Öngörüler - günlükleri-{günlük kategori adı} / ResourceId = / ABONELİKLERİ / {abonelik kimliği} /RESOURCEGROUPS/ {kaynak grubu adı} /PROVIDERS/ {kaynak sağlayıcı adı} / {kaynak türü} / {kaynak adı} / y = {dört basamaklı sayısal year} / m = {iki basamaklı sayısal month} / d = {iki basamaklı sayısal günü} / h = {iki basamaklı 24 saatlik hour}/m=00/PT1H.json
> 
> 

Veya daha basit bir şekilde

> Öngörüler - günlükleri-{günlük kategori adı} / ResourceId = / {kaynak kimliği} / y = {dört basamaklı sayısal year} / m = {iki basamaklı sayısal month} / d = {iki basamaklı sayısal günü} / h = {iki basamaklı 24 saatlik hour}/m=00/PT1H.json
> 
> 

Örneğin, bir blob adı olabilir:

> insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json
> 
> 

Her bir PT1H.json blob hello blob URL'SİNDE belirtilen hello saat içinde gerçekleşen olayların JSON blobu içerir (örneğin, h = 12). Bunlar ortaya çıktığında hello mevcut saat sırasında eklenmiş toohello PT1H.json dosya olaylardır. Merhaba dakika değeri (m 00 =) her zaman tanılama günlük olayları tek tek bloblar saat başına ayrılmış bu yana 00.

Merhaba PT1H.json dosyası içinde her olay bu biçim aşağıdaki hello "kayıtlar" dizisinde depolanır:

```
{
    "records": [
        {
            "time": "2016-07-01T00:00:37.2040000Z",
            "systemId": "46cdbb41-cb9c-4f3d-a5b4-1d458d827ff1",
            "category": "NetworkSecurityGroupRuleCounter",
            "resourceId": "/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/TESTNSG",
            "operationName": "NetworkSecurityGroupCounters",
            "properties": {
                "vnetResourceGuid": "{12345678-9012-3456-7890-123456789012}",
                "subnetPrefix": "10.3.0.0/24",
                "macAddress": "000123456789",
                "ruleName": "/subscriptions/ s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg/securityRules/default-allow-rdp",
                "direction": "In",
                "type": "allow",
                "matchedConnections": 1988
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
| category |Merhaba olay günlüğü kategori. |
| properties |Kümesi `<Key, Value>` hello hello olay ayrıntılarını açıklayan çiftleri (yani sözlük). |

> [!NOTE]
> Merhaba özellikleri ve bu özellikleri kullanımını hello kaynak bağlı olarak değişebilir.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* [BLOB'ları çözümleme için karşıdan yükle](../storage/storage-dotnet-how-to-use-blobs.md)
* [Tooan olay hub'ları ad akış tanılama günlükleri](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Tanılama günlükleri hakkında daha fazla bilgi](monitoring-overview-of-diagnostic-logs.md)
