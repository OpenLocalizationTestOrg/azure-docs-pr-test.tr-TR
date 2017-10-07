---
title: "aaaError & özel durum işleme - Azure Logic Apps | Microsoft Docs"
description: "Hata ve özel durum işleme Azure Logic Apps içinde desenleri"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: e50ab2f2-1fdc-4d2a-be40-995a6cc5a0d4
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 326a252310c8dfb154e583f91c9421675e448d1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a>Hataları ve Azure Logic Apps içinde özel durumları işleme

Azure mantıksal uygulamaları zengin araçlar sağlar ve desenler toohelp, tümleştirmeler sağlam ve hatalarına karşı dayanıklı olduğundan emin olun. Herhangi bir tümleştirme mimarideki emin tooappropriately tanıtıcı kapalı kalma süresi yapma hello zorluk oluşturur veya bağımlı sistemlerden verir. Logic Apps hataları işleme yapar, vermiş bir ilk sınıf deneyimi hello araçları, iş akışlarında özel durumları ve hataları tooact gerekir.

## <a name="retry-policies"></a>İlkeleri yeniden deneyin

Bir yeniden deneme ilkesi hello en temel özel durumu ve hata işleme türüdür. İlk istek zaman aşımına uğradı ya da başarısız olursa (bir 429 sonuçları herhangi bir istek veya 5xx yanıtı), bu ilkeyi hello eylem yeniden denemeniz gerekir olup olmadığını tanımlar. Varsayılan olarak, tüm eylemler 20 saniye aralıklarında 4 ek defa yeniden deneyin. Merhaba ilk istek alırsa, bunu bir `500 Internal Server Error` yanıtı hello iş akışı altyapısının duraklatır 20 saniye ve hello isteği yeniden denemeleri. Tüm yeniden denemelerden sonra hello yanıt hala bir özel durum ya da başarısız olması durumunda hello iş akışı devam eder ve işaretleri hello eylem durumu olarak `Failed`.

Yeniden deneme ilkelerini hello yapılandırabilirsiniz **girişleri** belirli bir eylem için. Örneğin, bir yeniden deneme ilkesi tootry kadar 4 kez 1 saatlik aralıklarında yapılandırabilirsiniz. Giriş özellikleri hakkında ayrıntılar için bkz: [iş akışı eylemleri ve Tetikleyicileri][retryPolicyMSDN].

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

HTTP eylem tooretry 4 kez istediğinizi ve her denemesi arasındaki 10 dakika bekleyin, tanımı aşağıdaki hello kullanırsınız:

```json
"HTTP": 
{
    "inputs": {
        "method": "GET",
        "uri": "http://myAPIendpoint/api/action",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT10M",
            "count": 4
        }
    },
    "runAfter": {},
    "type": "Http"
}
```

Merhaba desteklenen sözdizimi hakkında daha fazla bilgi için bkz: [iş akışı eylemleri ve Tetikleyicileri yeniden deneme ilkesi bölümüne][retryPolicyMSDN].

## <a name="catch-failures-with-hello-runafter-property"></a>Merhaba RunAfter özelliği hatalarıyla catch

Her mantıksal uygulama eylem hangi eylemleri, iş akışınızı hello adımları sıralama gibi hello eylem başlatılmadan önce bitmesi gereken bildirir. Merhaba eylem tanımı'nda bu sıralama hello adlandırılıyor `runAfter` özelliği. Bu özellik, hangi eylemleri ve eylem durumları yürütme hello eylemi açıklayan bir nesnedir. Varsayılan olarak, çok hello mantığı Uygulama Tasarımcısı eklenen tüm eylemleri ayarlamak`runAfter` hello önceki adımı Merhaba, önceki adımda `Succeeded`. Ancak, önceki eylem olduğunda bu değeri toofire eylemleri özelleştirebilirsiniz `Failed`, `Skipped`, veya bu değerleri olası kümesi. Bir öğe tooa tooadd istediyseniz sonra belirli bir eylemi Service Bus konu belirlenmiş `Insert_Row` başarısız olursa, aşağıdaki hello kullanabilir `runAfter` yapılandırma:

```json
"Send_message": {
    "inputs": {
        "body": {
            "ContentData": "@{encodeBase64(body('Insert_Row'))}",
            "ContentType": "{ \"content-type\" : \"application/json\" }"
        },
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/servicebus"
            },
            "connection": {
                "name": "@parameters('$connections')['servicebus']['connectionId']"
            }
        },
        "method": "post",
        "path": "/@{encodeURIComponent('failures')}/messages"
    },
    "runAfter": {
        "Insert_Row": [
            "Failed"
        ]
    }
}
```

Bildirim hello `runAfter` özellik ayarlanmışsa toofire hello `Insert_Row` eylem `Failed`. Merhaba eylem durumu ise toorun hello eylem `Succeeded`, `Failed`, veya `Skipped`, şu sözdizimini kullanın:

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> Çalıştırın ve önceki bir eylemi başarısız oldu sonra başarıyla tamamlanmış eylemler olarak işaretlenmiş `Succeeded`. Başarılı bir şekilde catch tüm hataları bir iş akışındaki hello varsa çalışmasına davranışı deyişle olarak işaretlenmiş `Succeeded`.

## <a name="scopes-and-results-tooevaluate-actions"></a>Kapsamlar ve sonuçları tooevaluate Eylemler

Sonra ayrı Eylemler çalıştırabilir benzer toohow de gruplandırabilirsiniz Eylemler birlikte içinde bir [kapsam](../logic-apps/logic-apps-loops-and-scopes.md), Eylemler mantıksal bir gruplandırması olarak davranır. Kapsamları mantıksal uygulama eylemleri düzenlemek için hem bir kapsam hello durumunu toplama değerlendirmesini gerçekleştirmek için faydalıdır. kapsamdaki tüm eylemler bitirdikten sonra hello kapsam kendisini bir durumunu alır. Merhaba kapsamı durumunu hello ile belirlenir aynı ölçüt olarak çalıştır. Merhaba son eylem bir yürütme dal ise `Failed` veya `Aborted`, hello durumu `Failed`.

kullanabileceğiniz toofire hello kapsamı içinde gerçekleşen hatalar için belirli eylemler, `runAfter` olarak işaretlenmiş bir kapsamla `Failed`. Varsa *herhangi* Eylemler hello kapsamında başarısız, kapsam sağlar başarısız olduktan sonra çalıştıran tek işlem toocatch hataları oluşturduğunuz.

### <a name="getting-hello-context-of-failures-with-results"></a>Sonuçları hatalarıyla Merhaba içeriğine alma

Bir kapsam hatalarını yakalama yararlı olsa da, bağlam toohelp tam olarak başarısız oldu, hangi eylemlerini anlama ve hatalar veya döndürüldü durum kodları isteyebilirsiniz. Merhaba `@result()` iş akışı işlevinin kapsamdaki tüm eylemlerin hello sonucu ile ilgili bağlam sağlar.

`@result()`tek bir parametre, kapsam adı alır ve tüm hello eylem sonuçlarını, kapsam içinde bir dizi döndürür. Bu eylem nesneleri aynı öznitelikleri hello hello dahil `@actions()` nesne, eylem başlangıç saati, eylem bitiş zamanı, eylem durumu, eylemi girişleri, eylem bağıntı kimlikleri ve eylem dahil olmak üzere çıkarır. bir kapsamda başarısız herhangi bir eylem bağlamında toosend, siz kolayca eşleştirin bir `@result()` ile işlev bir `runAfter`.

tooexecute bir eylem *her* kapsamdaki eylem, `Failed`, filtre hello sonuçları tooactions dizi başarısız oldu, eşleştirin `@result()` ile bir  **[filtre dizisi](../connectors/connectors-native-query.md)**  eylem ve  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  döngü. Merhaba filtrelenmiş Sonuç dizisi alabilir ve hello kullanarak her hatası için bir eylem gerçekleştirmek **ForEach** döngü. Merhaba kapsamında hello yanıt gövdesi başarısız herhangi bir eylem ile HTTP POST isteği gönderir ayrıntılı bir açıklama, ve ardından örneği `My_Scope`.

```json
"Filter_array": {
    "inputs": {
        "from": "@result('My_Scope')",
        "where": "@equals(item()['status'], 'Failed')"
    },
    "runAfter": {
        "My_Scope": [
            "Failed"
        ]
    },
    "type": "Query"
},
"For_each": {
    "actions": {
        "Log_Exception": {
            "inputs": {
                "body": "@item()['outputs']['body']",
                "method": "POST",
                "headers": {
                    "x-failed-action-name": "@item()['name']",
                    "x-failed-tracking-id": "@item()['clientTrackingId']"
                },
                "uri": "http://requestb.in/"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "foreach": "@body('Filter_array')",
    "runAfter": {
        "Filter_array": [
            "Succeeded"
        ]
    },
    "type": "Foreach"
}
```

Neler ayrıntılı kılavuz toodescribe şöyledir:

1. içinde tüm eylemler tooget hello sonucu `My_Scope`, hello **filtre dizisi** eylem filtrelerini `@result('My_Scope')`.

2. Merhaba için koşul **filtre dizisi** herhangi `@result()` çok durum eşit olan öğe`Failed`. Bu durum tüm eylem sonuçlarını hello diziyle filtreler `My_Scope` yalnızca tooan diziyle eylem sonuçlarını başarısız oldu.

3. Gerçekleştirmek bir **her** hello eylemini **filtre dizi** çıkarır. Bu adım bir eylem gerçekleştirir *her* önceden filtre eylem sonucu başarısız oldu.

    Merhaba kapsamında tek bir eylem başarısız olursa hello Eylemler hello `foreach` yalnızca bir kez çalıştırın. 
    Çok sayıda başarısız Eylemler hatası başına tek bir eylem neden olur.

4. Bir HTTP POST hello üzerinde Gönder `foreach` öğesi yanıt gövdesi veya `@item()['outputs']['body']`. Merhaba `@result()` öğesi şekli olan hello aynı hello `@actions()` şekil ve ayrıştırılabilir aynı hello yolu.

5. Hello başarısız Eylem adına sahip iki özel üstbilgi dahil `@item()['name']` ve hello başarısız oldu, izleme kimliği çalışma istemci `@item()['clientTrackingId']`.

Başvuru için tek bir örneği burada verilmiştir `@result()` hello gösteren öğesi `name`, `body`, ve `clientTrackingId` hello önceki örnekte Ayrıştırılan özellikleri. Dışında bir `foreach`, `@result()` bu nesneleri içeren bir dizi döndürür.

```json
{
    "name": "Example_Action_That_Failed",
    "inputs": {
        "uri": "https://myfailedaction.azurewebsites.net",
        "method": "POST"
    },
    "outputs": {
        "statusCode": 404,
        "headers": {
            "Date": "Thu, 11 Aug 2016 03:18:18 GMT",
            "Server": "Microsoft-IIS/8.0",
            "X-Powered-By": "ASP.NET",
            "Content-Length": "68",
            "Content-Type": "application/json"
        },
        "body": {
            "code": "ResourceNotFound",
            "message": "/docs/folder-name/resource-name does not exist"
        }
    },
    "startTime": "2016-08-11T03:18:19.7755341Z",
    "endTime": "2016-08-11T03:18:20.2598835Z",
    "trackingId": "bdd82e28-ba2c-4160-a700-e3a8f1a38e22",
    "clientTrackingId": "08587307213861835591296330354",
    "code": "NotFound",
    "status": "Failed"
}
```

tooperform farklı özel durum işleme desenleri, daha önce gösterilen hello ifadeleri kullanabilirsiniz. Tek özel durum eylemin hello tüm filtrelenmiş dizisi hataları kabul hello kapsamı dışında işleme tooexecute seçin ve hello kaldırmak `foreach`. Merhaba yararlı olan diğer özellikleri de içerebilir `@result()` daha önce gösterilen yanıt.

## <a name="azure-diagnostics-and-telemetry"></a>Azure tanılama ve telemetri

Merhaba önceki desenleri mükemmel şekilde toohandle hataları ve özel durumları çalışması içinde alır, ancak ayrıca tanımlamak ve tooerrors çalışmasına Merhaba bağımsız yanıt. 
[Azure tanılama](../logic-apps/logic-apps-monitor-your-logic-apps.md) tüm iş akışı (tüm çalışma ve eylem durumları dahil) olayları tooan Azure Storage hesabı veya bir Azure olay hub'ı basit yol toosend sağlar. tooevaluate çalıştırma durumları, hello günlüklerini ve ölçümleri izleyin veya tercih ettiğiniz izleme aracı yayımlama. Bir olası seçenektir toostream Azure Event Hub'ına aracılığıyla tüm hello olaylarını [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/). Stream Analytics içinde herhangi bir anormallikleri, ortalama veya hataları kapalı dinamik sorgular hello tanılama günlüklerini yazabilirsiniz. Akış analizi kuyruklar, konular, SQL, Azure Cosmos DB ve Power BI gibi tooother veri kaynaklarını kolayca çıkarabilirsiniz.

## <a name="next-steps"></a>Sonraki Adımlar

* [Bir müşteri hata işleme Azure Logic Apps ile nasıl derler bakın](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [Daha fazla Logic Apps örnekleri ve senaryoları Bul](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Nasıl toocreate dağıtımları mantıksal uygulamalar için otomatik öğrenin](../logic-apps/logic-apps-create-deploy-template.md)
* [Visual Studio ile mantıksal uygulamalar oluşturma ve dağıtma](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
