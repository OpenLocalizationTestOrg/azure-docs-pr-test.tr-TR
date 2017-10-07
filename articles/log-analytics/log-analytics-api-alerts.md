---
title: "aaaUsing OMS günlük analizi uyarı REST API'si"
description: "Merhaba günlük analizi uyarı REST API toocreate sağlar ve bu yer Operations Management Suite (OMS) günlük analizi uyarıları yönetin.  Bu makalede, farklı işlemler gerçekleştirmek için hello API ve çeşitli örnekler ayrıntıları sağlar."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a>Oluşturma ve uyarı kurallarında günlük analizi REST API ile yönetme
Merhaba günlük analizi uyarı REST API toocreate sağlar ve Uyarıları Operations Management Suite (OMS) yönetme.  Bu makalede, farklı işlemler gerçekleştirmek için hello API ve çeşitli örnekler ayrıntıları sağlar.

Merhaba günlük analizi Search REST API'sini RESTful olan ve hello Azure Resource Manager REST API'si erişilebilir. Bu belgede hello API kullanarak bir PowerShell komut satırı burada erişilen örnekler bulacaksınız [ARMClient](https://github.com/projectkudu/ARMClient), çağırma basitleştiren bir açık kaynak komut satırı aracı hello Azure Kaynak Yöneticisi API'si. Merhaba kullanımını ARMClient ve PowerShell birçok seçenekleri tooaccess hello günlük analizi arama API biridir. Bu araçların hello RESTful Azure Kaynak Yöneticisi API'si toomake çağrıları tooOMS çalışma alanları kullanma ve bunların içindeki arama komutları gerçekleştirin. Arama sonuçları tooyou toouse hello arama sonuçları birçok farklı yolla program aracılığıyla sağlayarak JSON biçiminde Hello API çıkarır.

## <a name="prerequisites"></a>Ön koşullar
Şu anda, uyarıları günlük analizi olarak kaydedilmiş bir aramayı ile yalnızca oluşturulabilir.  Toohello başvurabilir [günlük Search REST API'sini](log-analytics-log-search-api.md) daha fazla bilgi için.

## <a name="schedules"></a>Zamanlamalar
Kaydedilmiş bir aramayı bir veya daha fazla zamanlama olabilir. Merhaba zamanlama ne sıklıkta hello arama çalıştırılan tanımlar ve hello zaman aralığı içinde hangi hello ölçütleri tanımlanır.
Zamanlamaları, aşağıdaki tablonun hello hello özelliklere sahiptir.

| Özellik | Açıklama |
|:--- |:--- |
| aralığı |Ne sıklıkta hello arama çalıştırılır. Dakika cinsinden ölçülür. |
| QueryTimeSpan |hangi hello ölçütleri değerlendirildiği hello zaman aralığı. Eşit tooor aralığından daha büyük olmalıdır. Dakika cinsinden ölçülür. |
| Sürüm |Merhaba kullanılan API sürümü.  Şu anda, bu her zaman too1 olarak ayarlanmalıdır. |

Örneğin, bir olay sorgusu bir aralığı 15 dakika ve 30 dakikalık bir zaman aralığı ile göz önünde bulundurun. Bu durumda, hello sorgu 15 dakikada bir çalışır ve hello ölçütleri 30 dakikalık aralık tooresolve tootrue etseydi uyarı tetikleyen.

### <a name="retrieving-schedules"></a>Zamanlamalar alınıyor
Kullanım hello kayıtlı bir aramaya tüm zamanlamalar yöntemi tooretrieve alın.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

Kullanım hello belirli bir zamanlama için kaydedilmiş bir aramayı bir zamanlama kimliği tooretrieve yöntemiyle alın.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

Bir zamanlama için bir örnek yanıt aşağıdadır.

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a>Bir zamanlama oluşturma
Benzersiz zamanlama kimliği toocreate yeni bir zamanlama Hello Put yöntemini kullanın.  İki zamanlamaları olamaz sahip Merhaba, aynı kimliği kayıtlı aramalar farklı ile ilişkili olsa bile unutmayın.  Merhaba OMS konsolunda bir zamanlama oluşturmak, bir GUID hello zamanlama kimliği için oluşturulur

> [!NOTE]
> Tüm kayıtlı aramaları, zamanlamaları ve günlük analizi API hello ile oluşturulan eylemler için Hello adı küçük olması gerekir.

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a>Bir zamanlama düzenleme
Kimliği aynı kaydedilmiş hello için arama zamanlama toomodify mevcut bir zamanlamayı ile Merhaba Put yöntemini kullanın.  Merhaba hello istek gövdesi hello etag hello planının eklemeniz gerekir.

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a>Zamanlamalar silme
Zamanlama kimliği toodelete bir zamanlama Hello Delete yöntemini kullanın.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a>Eylemler
Bir zamanlama birden çok eylemler olabilir. Bir eylem bir posta gönderme veya bir runbook'u başlatma gibi bir veya daha fazla işlemleri tooperform tanımlayabilir veya ne zaman bir arama sonuçlarını hello bazı ölçütlere uyan belirleyen bir eşik tanımlayabilir.  Merhaba eşiğine ulaşıldığında hello işlemlerin gerçekleştirilmesi bazı eylemler her ikisi de tanımlayacaksınız.

Tüm eylemleri aşağıdaki tablonun hello hello özelliklere sahiptir.  Farklı türde bir uyarı aşağıda açıklanan farklı ek özellikler vardır.

| Özellik | Açıklama |
|:--- |:--- |
| Tür |Merhaba eylem türü.  Şu anda hello olası değerler, uyarı ve Web kancası olur. |
| Ad |Merhaba uyarı görünen adı. |
| Sürüm |Merhaba kullanılan API sürümü.  Şu anda, bu her zaman too1 olarak ayarlanmalıdır. |

### <a name="retrieving-actions"></a>Eylemler Alınıyor
Kullanım hello tüm eylemler için bir zamanlama yöntemi tooretrieve alın.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

Kullanım hello hello Eylem Kimliği tooretrieve yöntemiyle bir zamanlama için belirli bir eylemi alın.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a>Oluşturma veya Eylemler düzenleme
Benzersiz toohello zamanlama toocreate yeni bir eylem bir eylem kimliği ile Merhaba Put yöntemini kullanın.  Bir eylemin hello OMS konsolunda oluşturduğunuzda, bir GUID için hello eylem kimliğidir.

> [!NOTE]
> Tüm kayıtlı aramaları, zamanlamaları ve günlük analizi API hello ile oluşturulan eylemler için Hello adı küçük olması gerekir.

Kimliği aynı kaydedilmiş hello için arama zamanlama toomodify var olan bir eylem ile Merhaba Put yöntemini kullanın.  Merhaba hello istek gövdesi hello etag hello planının eklemeniz gerekir.

Bu örnekler aşağıdaki hello bölümler sağlanan şekilde hello istek biçimi yeni bir eylem oluşturmak için eylem türüne göre değişir.

### <a name="deleting-actions"></a>Eylemler siliniyor
Hello Eylem Kimliği toodelete eylemin Hello Delete yöntemini kullanın.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a>Uyarı eylemleri
Bir zamanlama tek bir uyarı eylemi olması gerekir.  Uyarı eylemleri, bir veya daha fazla tablo aşağıdaki hello hello bölümlerde sahip.  Her daha aşağıda ayrıntılı olarak açıklanmıştır.

| Bölüm | Açıklama |
|:--- |:--- |
| Eşik |Merhaba eylemi çalıştırıldığında ölçütlerini. |
| EmailNotification |Posta toomultiple alıcılar gönderin. |
| Düzeltme |Bir runbook'un Azure Otomasyon tooattempt tanımlanan toocorrect sorunu başlatın. |

#### <a name="thresholds"></a>Eşikleri
Bir uyarı eylem tek bir eşik olması gerekir.  Kaydedilmiş bir aramayı Hello sonuçlarını arama ile ilişkili bir eylemin hello eşiği eşleştiğinde, başka bir işlem bu uygulamada çalıştırılır.  Böylece eşikleri içermeyen diğer türleri Eylemler ile kullanılan bir eylem yalnızca bir eşik de içerebilir.

Eşikleri aşağıdaki tablonun hello hello özelliklere sahiptir.

| Özellik | Açıklama |
|:--- |:--- |
| işleci |Merhaba eşik karşılaştırma işleci. <br> gt şundan = <br> lt = küçüktür |
| Değer |Merhaba eşik değeri. |

Örneğin, bir olay sorgusu zaman aralığı 15 dakika, 30 dakikalık bir Timespan ve 10'dan büyük bir eşik ile göz önünde bulundurun. Bu durumda, hello sorgu 15 dakikada bir çalışır ve 30 dakikalık aralık oluşturulan 10 olayları döndürülen bir uyarı tetikleyen.

Aşağıdaki örnek yanıt için bir eylem yalnızca bir eşik ile ' dir.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

Merhaba Put yöntemi için bir zamanlama benzersiz Eylem Kimliği toocreate yeni bir eşik eylemi kullanın.  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

Kullanım hello var olan bir eylem kimliği toomodify yöntemiyle bir zamanlama için bir eşik eylem yerleştirin.  Merhaba hello istek gövdesi hello eylemin hello etag eklemeniz gerekir.

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a>E-posta bildirimi
Posta tooone ya da daha fazla alıcı e-posta bildirimleri gönderin.  Bunlar, aşağıdaki tablonun hello hello özellikleri içerir.

| Özellik | Açıklama |
|:--- |:--- |
| Alıcıları |Posta adresleri listesi. |
| Konu |Merhaba posta Hello konu. |
| Eki |Bu her zaman "Hiçbiri" değerine sahip şekilde ekleri şu anda, desteklenmez. |

Aşağıdaki örnek yanıt bir eşik ile bir e-posta bildirim eylemi için ' dir.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

Merhaba Put yöntemi için bir zamanlama benzersiz Eylem Kimliği toocreate yeni bir e-posta eylemi kullanın.  Hello hello kaydedilmiş arama sonuçlarını hello eşiği aştığında hello posta gönderilen şekilde hello aşağıdaki örnek bir e-posta bildirimi bir eşik ile oluşturur.

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

Merhaba Put yöntemini bir varolan eylem kimliği toomodify ile bir e-posta eylemi için bir zamanlama kullanın.  Merhaba hello istek gövdesi hello eylemin hello etag eklemeniz gerekir.

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a>Düzeltme eylemleri
Düzeltmeler, Azure automation'da hello uyarı tarafından tanımlanan toocorrect hello sorun çalışır bir runbook başlatın.  Bir düzeltme eylemi kullanılan hello runbook için bir Web kancası oluşturun ve ardından hello URI hello WebhookUri özelliği belirtmeniz gerekir.  Merhaba OMS konsolunu kullanarak bu eylemi oluşturduğunuzda, yeni bir Web kancası hello runbook için otomatik olarak oluşturulur.

Düzeltmeler, aşağıdaki tablonun hello hello özellikleri içerir.

| Özellik | Açıklama |
|:--- |:--- |
| RunbookName |Merhaba runbook adı. Bu hello Otomasyon çözümünü OMS çalışma alanınızdaki yapılandırılan hello Otomasyon hesabı yayımlanan bir runbook'ta eşleşmelidir. |
| WebhookUri |Merhaba Web kancası URI'si. |
| Süre sonu |Merhaba sona erme tarihi ve saati hello Web kancası.  Merhaba Web kancası bir sona erme yoksa, bu geçerli bir gelecek tarih olabilir. |

Aşağıdaki örnek yanıt bir eşik ile bir düzeltme eylemi için ' dir.

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

Merhaba Put yöntemini benzersiz Eylem Kimliği toocreate yeni bir düzeltme eylemi için bir zamanlama kullanın.  Merhaba hello kaydedilmiş arama sonuçlarını hello eşiği aştığında hello runbook başlatıldıktan şekilde hello aşağıdaki örnek bir düzeltme bir eşik ile oluşturur.

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

Merhaba Put yöntemini bir varolan eylem kimliği toomodify ile bir düzeltme eylemi için bir zamanlama kullanın.  Merhaba hello istek gövdesi hello eylemin hello etag eklemeniz gerekir.

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a>Örnek
Tam örnek toocreate yeni bir e-posta uyarı aşağıdadır.  Bu eşik ve e-posta içeren bir eylem birlikte yeni bir zamanlama oluşturur.

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a>Web kancası eylemleri
Web kancası eylemleri, bir URL çağırma ve isteğe bağlı olarak gönderilen bir yükü toobe sağlayan bir işlem başlatın.  Azure Otomasyon çalışma kitabı dışındaki işlemler çağırabilir Web kancası için amacı dışında benzer tooRemediation Eylemler oldukları.  Yükü teslim toobe toohello uzak bir işlem sağlayarak hello ek bir seçeneğiniz de sağlar.

Web kancası eylemleri bir eşik gerekmez ancak bunun yerine bir eşik ile uyarı bir eylemi var. tooa zamanlama eklenmelidir.  Merhaba eşiğine ulaşıldığında, tüm çalışan birden çok Web kancası eylemleri ekleyebilirsiniz.

Web kancası eylemleri aşağıdaki tablonun hello hello özellikleri içerir.

| Özellik | Açıklama |
|:--- |:--- |
| WebhookUri |Merhaba posta Hello konu. |
| CustomPayload |Özel yük toobe toohello Web kancası gönderdi.  Merhaba biçimi hangi hello Web kancası bekleniyor bağlı olacaktır. |

Web kancası eylem ve bir eşik ile ilişkili bir uyarı eylem için örnek yanıt aşağıdadır.

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a>Oluşturma veya bir Web kancası eylemi düzenleme
Merhaba Put yöntemi için bir zamanlama benzersiz Eylem Kimliği toocreate yeni bir Web kancası eylemi kullanın.  Böylece Hello hello kaydedilmiş arama sonuçlarını hello eşiği aştığında hello Web kancası tetiklenen hello aşağıdaki örnek bir Web kancası eylemi ve bir uyarı eylem bir eşik ile oluşturur.

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

Merhaba Put yöntemini bir varolan eylem kimliği toomodify ile bir Web kancası eylemi için bir zamanlama kullanın.  Merhaba hello istek gövdesi hello eylemin hello etag eklemeniz gerekir.

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a>Sonraki adımlar
* Kullanım hello [REST API tooperform günlük aramaları](log-analytics-log-search-api.md) günlük analizi içinde.

