---
title: aaaWorkflow eylemleri ve Tetikleyicileri - Azure Logic Apps | Microsoft Docs
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a>İş akışı eylemleri ve Azure Logic Apps için Tetikleyiciler

Logic apps tetikleyiciler ve Eylemler oluşur. Tetikleyiciler altı tür vardır. Her tür farklı arabirimi ve farklı bir davranışı vardır. Merhaba hello ayrıntılarını bakarak ilgili diğer ayrıntıları öğrenebilirsiniz [iş akışı tanımlama dili](logic-apps-workflow-definition-language.md).  
  
Toolearn tetikleyiciler ve Eylemler ve nasıl bunları toobuild logic apps tooimprove kullanabilir hakkında daha fazla iş süreçlerini ve iş akışları okumaya devam edin.  
  
### <a name="triggers"></a>Tetikleyiciler  

Tetikleyicinin mantığını uygulama akışınızın bir farklı çalıştır başlatabilirsiniz hello çağrıları belirtir. Merhaba iki farklı şekilde tooinitiate, iş akışınızın bir farklı çalıştır şunlardır:  
  
-   Yoklama tetikleyici  

-   Anında iletme tetikleyici - arama hello tarafından [iş akışı hizmeti REST API'si](https://docs.microsoft.com/rest/api/logic/workflows)  
  
Tüm Tetikleyicileri bu üst düzey öğeleri içerir:  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a>Tetikleyici türlerini ve bunların girişleri  

Bu tür tetikleyici sunucusu kullanabilirsiniz:
  
-   **İstek** \- hello mantıksal uygulama, toocall için bir uç nokta yapar  
  
-   **Yineleme** \- ateşlenir dayalı tanımlanmış bir zamanlamaya göre  
  
-   **HTTP** \- bir HTTP web uç noktası yoklar. Merhaba HTTP uç noktası tooa belirli tetikleme sözleşme uygun olmalıdır \- bir 202 kullanarak ya da\-zaman uyumsuz desen veya bir dizi döndürerek  
  
-   **ApiConnection** \- hello HTTP gibi yoklamalar tetikleyin, ancak bunu hello yararlanan [Microsoft tarafından yönetilen API'ler](https://docs.microsoft.com/azure/connectors/apis-list)  
  
-   **HTTPWebhook** \- açılır uç noktası, benzer toohello el ile tetikleyici, ancak, bir de çağırır tooa URL tooregister belirtilen ve kaldırılamadı  
  
-   **ApiConnectionWebhook** \- hello Microsoft tarafından yönetilen API yararlanarak HTTPWebhook tetikleyici hello gibi çalışır       
    Farklı bir kümesini her tetikleyici türünde **girişleri** davranışını tanımlar.  
  
## <a name="request-trigger"></a>Tetikleyici isteği  

Bu tetikleyici bir uç noktası olarak bir HTTP isteği tooinvoke mantıksal uygulamanızı çağıran işlevi görür. Bir istek tetikleyici aşağıdaki gibi görünür:  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

Ayrıca adlı isteğe bağlı bir özellik olan **şema**:  
  
|Öğe adı|Gerekli|Açıklama|  
|----------------|------------|---------------|  
|Şema|Hayır|JSON şeması hello gelen isteği doğrular. Sonraki iş akışı adımları hangi özellikleri tooreference bilmeniz yardımcı olmak için kullanışlıdır.|

tooinvoke Bu uç noktaya toocall hello gereksinim *listCallbackUrl* API. Bkz: [iş akışı hizmeti REST API'si](https://docs.microsoft.com/rest/api/logic/workflows).  
  
## <a name="recurrence-trigger"></a>Yineleme tetikleyici  

Bir yineleme tetikleyici tanımlanmış bir zamanlamaya göre çalıştırır biridir. Bu tür bir tetikleyici, aşağıdaki örnekte olduğu gibi görünebilir:  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

Gördüğünüz gibi bir basit yol toorun bir iş akışı gereklidir.  
  
|Öğe adı|Gerekli|Açıklama|  
|----------------|------------|---------------|  
|frequency|Evet|Ne sıklıkta hello tetikleyici yürütür. Bu değerlerden yalnızca birini kullanın: saniye, dakika, saat, gün, hafta, ay veya yıl|  
|interval|Evet|Merhaba yinelemesi sıklığı verilen hello aralığı|  
|startTime|Hayır|Bir startTime UTC uzaklığı sağlanırsa, bu saat dilimi kullanılır.|  
|saat dilimi|Yok|Bir startTime UTC uzaklığı sağlanırsa, bu saat dilimi kullanılır.|  
  
Ayrıca, bir tetikleyici toostart hello gelecekteki belirli bir noktada yürütme zamanlayabilirsiniz. Haftalık rapor her Pazartesi toostart isterseniz, örneğin, hello mantığı uygulama toostart her Pazartesi tetikleyici aşağıdaki hello oluşturarak zamanlayabilirsiniz:  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a>HTTP tetikleyicisi  

HTTP Tetikleyicileri belirtilen uç nokta yoklamak ve hello yanıt toodetermine hello iş akışı yürütülmesi gereken olup olmadığını denetleyin. Merhaba girişleri nesne parametreleri gerekli tooconstruct bir HTTP çağrısıyla hello kümesini alır:  
  
|Öğe adı|Gerekli|Açıklama|Tür|  
|----------------|------------|---------------|--------|  
|Yöntemi|Evet|HTTP yöntemleri aşağıdaki hello biri olabilir: GET, POST, PUT, DELETE, düzeltme eki veya HEAD|Dize|  
|URI|Evet|çağrılan hello http veya https uç noktası. 2 kilobayt sayısı.|Dize|  
|Sorguları|Hayır|Merhaba sorgu parametreleri tooadd toohello URL'yi temsil eden bir nesne. Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` toohello URL.|Nesne|  
|Üstbilgileri|Hayır|Her toohello isteği gönderilir hello üstbilgilerinin temsil eden bir nesne. Örneğin, tooset hello dil ve istek üzerine yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|Nesne|  
|Gövde|Hayır|Toohello endpoint gönderilen hello yükünü temsil eden bir nesne.|Nesne|  
|retryPolicy|Hayır|Merhaba yeniden deneme davranışı 4xx veya 5xx hataları özelleştirmenize olanak sağlayan bir nesne.|Nesne|  
|Kimlik doğrulaması|Hayır|İstek hello temsil hello yöntemi kimlik doğrulaması. Bu nesne üzerinde daha fazla bilgi için bkz [Scheduler giden bağlantı kimlik doğrulaması](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Zamanlayıcı daha desteklenen bir özellik yok: `authority` varsayılan olarak, bu değer `https://login.windows.net` belirtilmediğinde, ancak gibi farklı bir kitleye kullanabilirsiniz`https://login.windows\-ppe.net`|Nesne|  
  
Merhaba HTTP tetikleyicisini hello HTTP API tooconform belirli bir desene toowork mantıksal uygulamanızı ile iyi ile gerektirir. Alanları aşağıdaki hello gerektirir:  
  
|Yanıt|Açıklama|  
|------------|---------------|  
|Durum kodu|Durum kodu 200 \(Tamam\) toocause Çalıştır. Diğer bir durum kodu bir Farklı Çalıştır neden olmaz.|  
|Yeniden deneme\-üstbilgi sonra|Merhaba mantıksal uygulama hello uç nokta yeniden yoklar kadar saniye sayısı.|  
|Konum üstbilgisi|Merhaba URL toocall hello sonraki yoklama aralığı. Belirtilmezse, hello özgün URL'si kullanılır.|  
  
İstekleri farklı türleri için farklı davranışlar bazı örnekleri şunlardır:  
  
|Yanıt kodu|Yeniden deneme\-sonra|Davranışı|  
|-----------------|----------------|------------|  
|200|\(yok\)|Değil geçerli tetikleyici yeniden deneme\-sonra gerekli ya da başka hello hiçbir zaman hello sonraki istek için yoklamaları altyapısıdır.|  
|202|60|Merhaba iş akışı tetiklemez. Merhaba sonraki girişiminde bir dakika içinde gerçekleşir.|  
|200|10|Merhaba iş akışını çalıştırma ve daha fazla içerik için 10 saniye içinde yeniden kontrol edin.|  
|400|\(yok\)|Hatalı istek, hello iş akışı çalıştırmayın. Varsa hiçbir **yeniden deneme ilkesi** tanımlanan hello varsayılan ilke kullanılır. Merhaba yeniden deneme sayısı üst sınırına ulaşıldı sonra hello tetikleyici artık geçerli değil.|  
|500|\(yok\)|Sunucu hatası, hello iş akışı çalıştırmayın.  Varsa hiçbir **yeniden deneme ilkesi** tanımlanan hello varsayılan ilke kullanılır. Merhaba yeniden deneme sayısı üst sınırına ulaşıldı sonra hello tetikleyici artık geçerli değil.|  
  
bir HTTP tetikleyicisi Hello çıkışları aşağıdaki gibi görünür:  
  
|Öğe adı|Açıklama|Tür|  
|----------------|---------------|--------|  
|Üstbilgileri|Merhaba http yanıtının Hello üstbilgileri.|Nesne|  
|Gövde|Merhaba hello http yanıt gövdesi.|Nesne|  
  
## <a name="api-connection-trigger"></a>API bağlantı tetikleyici  

Merhaba API bağlantı tetikleyici temel işlevselliği de benzer toohello HTTP tetikleyici ' dir. Ancak, hello eylem tanımlamak için başlangıç parametreleri farklıdır. Örnek aşağıda verilmiştir:  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|Öğe adı|Gerekli|Tür|Açıklama|  
|----------------|------------|--------|---------------|  
|ana bilgisayar|Evet||Merhaba ApiApp ağ geçidi ve kimliği barındırılan.|  
|Yöntemi|Evet|Dize|HTTP yöntemleri aşağıdaki hello biri olabilir: **almak**, **POST**, **PUT**, **silmek**, **düzeltme eki**, veya  **HEAD**|  
|Sorguları|Hayır|Nesne|Temsil hello sorgu parametreleri toobe toohello URL eklendi. Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` toohello URL.|  
|Üstbilgileri|Hayır|Nesne|Her toohello isteği gönderilir hello üstbilgilerinin temsil eder. Örneğin, tooset hello dil ve istek üzerine yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Gövde|Hayır|Nesne|Toohello endpoint gönderilen hello yükünü temsil eder.|  
|retryPolicy|Hayır|Nesne|Toocustomize hello yeniden deneme davranışı 4xx veya 5xx hataları sağlar.|  
|Kimlik doğrulaması|Hayır|Nesne|İstek hello temsil hello yöntemi kimlik doğrulaması. Bu nesne üzerinde daha fazla bilgi için bkz [Scheduler giden bağlantı kimlik doğrulaması](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)|  
  
ana bilgisayar için Hello özellikleri şunlardır:  
  
|Öğe adı|Gerekli|Açıklama|  
|----------------|------------|---------------|  
|API runtimeUrl|Evet|Merhaba Hello uç noktasını API yönetilen.|  
|Bağlantı adı||Bir başvuru tooa parametre çağrılmalıdır `$connection` ve iş akışı kullanır hello yönetilen hello API bağlantı hello adıdır.|
  
bir API bağlantı tetikleyicisi Hello çıkışları şunlardır:
  
|Öğe adı|Tür|Açıklama|  
|----------------|--------|---------------|  
|Üstbilgileri|Nesne|Merhaba http yanıtının Hello üstbilgileri.|  
|Gövde|Nesne|Merhaba hello http yanıt gövdesi.|  
  
## <a name="httpwebhook-trigger"></a>HTTPWebhook tetikleyici  

bir uç nokta, benzer toohello el ile tetikleyici, ancak hello HTTPWebhook tetikleyici de tooa çağırır hello HTTPWebhook tetikleyici açar URL tooregister belirtilen ve kaydını silin. Bir HTTPWebhook tetikleyicisi aşağıdaki gibi görünmelidir örneği şöyledir:  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

Bu bölümler çoğunu isteğe bağlıdır ve hello Web kancası hello davranışını hangi bölümlerinin sağlanan atlanmış veya bağlıdır.  
bir Web kancası Hello özelliklerini aşağıdaki gibidir:  
  
|Öğe adı|Gerekli|Açıklama|  
|----------------|------------|---------------|  
|abone olma|Hayır|Merhaba Hello tetikleyici oluşturulduğunda ve hello ilk kaydı gerçekleştiren çağrılan isteği giden.|  
|Aboneliği Kaldır|Hayır|Merhaba Hello tetikleyici silindiğinde isteği giden.|  
  
-   **Abone** olan hello giden toostart dinleme tooevents yaptı çağrısı. Bu çağrı aynı normal HTTP Eylemler hello parametre kümesine yapmak hello ile başlar. Bu giden çağrı hiçbir zaman hello yapılan herhangi bir şekilde değişiklikler iş akışı, örneğin, her hello kimlik yapılır ya da hello tetikleyici parametreleri değişiklik girdisini.
  
    toosupport bu çağrı, yeni bir işlev yok: `@listCallbackUrl()`. Bu işlev, bu iş akışındaki belirli Bu tetikleyici için benzersiz bir URL döndürür. Merhaba hizmet REST kullanan hello uç noktaları için benzersiz tanımlayıcı hello temsil eder.  
  
-   **Aboneliği** bir işlem Bu tetikleyici geçersiz dahil olmak üzere işler olduğunda çağrılır:  
  
    -   Silme veya hello tetikleyici devre dışı bırakma  
  
    -   Silme veya hello iş akışını devre dışı bırakma  
  
    -   Silme veya hello abonelik devre dışı bırakma  
  
    Merhaba mantıksal uygulama otomatik olarak hello çağıran eylem aboneliği. toothis işlevini hello parametreleri aynı hello HTTP tetikleyici olarak hello.  
  
    Merhaba hello HTTPWebhook tetikleyici çıkışları hello gelen istek Merhaba içeriğine şunlardır:  
  
|Öğe adı|Tür|Açıklama|  
|-----------------|--------|---------------|  
|Üstbilgileri|Nesne|Merhaba http istek üstbilgilerinin Hello.|  
|Gövde|Nesne|Merhaba hello http istek gövdesi.|  

Bir Web kancası eylemi sınırları hello belirtilebilir aynı şekilde [HTTP zaman uyumsuz sınırları](#asynchronous-limits).
  

## <a name="conditions"></a>Koşullar  

Merhaba iş akışı çalışıp çalışmayacağını olup olmadığını, herhangi bir tetikleyici için bir veya daha fazla koşullar toodetermine kullanabilirsiniz. Örneğin:  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

Bu durumda, rapor yalnızca Tetikleyicileri hello iş akışı çalışırken hello `sendReports` parametresini tootrue ayarlayın. Son olarak, koşullar hello tetikleyici hello durum kodunu başvurabilir. Örneğin, yalnızca Web sitenizin bir durum kodu 500, aşağıdaki gibi geri döndüğünde devre dışı bir iş akışı kazandırın:
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> Herhangi bir ifade hello tetikleyici hello durum kodunu başvurduğunda \(herhangi bir şekilde\), hello varsayılan davranışı \(200 yalnızca Tetikle \(Tamam\) \) değiştirilir. Örneğin, durum kodu 200 ve 201 durum kodunu tootrigger isterseniz, tooinclude gerekir: `@or(equals(triggers().code, 200),equals(triggers().code,201))` koşulunuz olarak.  
  
## <a name="start-multiple-runs-for-a-request"></a>Bir istek için birden çok çalışmalarını Başlat

tek bir istek için birden çok çalıştırır kapalı tookick `splitOn` toopoll yoklama aralıkları arasında birden çok yeni öğeleri olan bir uç nokta istediğinizde, örneğin, yararlıdır.
  
İle `splitOn`, her biri istediğiniz öğeleri hello dizisi içerir hello yanıt yükünün hello özelliği belirtin toouse toostart hello tetikleyici yürütülmesi. Örneğin, yanıt aşağıdaki hello döndüren bir API olduğunu düşünün:  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
Bu örnek gibi tetikleyici gerçekleştirebilmesi için mantıksal uygulamanızı hello satırları içeriği, yalnızca gerekir:  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
Daha sonra hello iş akışı tanımında `@triggerBody().name` döndürür `mycoolrow` ilk çalıştırma hello için ve `another row` hello ikinci çalıştırma için. Bu örnek gibi Hello tetikleyici çıkışları bakın:  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

Kullanırsanız, bunu `SplitOn`, hello dizi dışında bu durumda, hello hello özellikler alınamıyor `Status` alan.  
  
> [!NOTE]  
> Bu örnekte, kullandığımız hello `?` işleci toobe mümkün tooavoid hello durumunda bir hata `Rows` özelliği mevcut değil. 
  
## <a name="single-run-instance"></a>Tek çalışma örneği

Tüm etkin metinler tamamladıysanız, yineleme özelliği tooonly yangın sahip Tetikleyicileri yapılandırabilirsiniz. Bir çalıştırma sürüyor olsa zamanlanmış bir yinelenme meydana gelirse, hello tetikleyici atlar ve hello sonraki zamanlanmış yineleme aralığı toocheck kadar yeniden bekler.

Bu ayar hello işlemi seçeneklerle yapılandırabilirsiniz:

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a>Türleri ve girişleri  

Eylemler, her benzersiz davranışına sahip birçok tür vardır. Koleksiyon Eylemler kendisini içinde birçok diğer eylemler içerebilir.

### <a name="standard-actions"></a>Standart Eylemler  

-   **HTTP** bir HTTP web uç noktası bu eylemi çağırır.  
  
-   **ApiConnection** \- Bu eylem HTTP eylemi hello gibi davranır, ancak kullanır hello Microsoft tarafından yönetilen API'ler.  
  
-   **ApiConnectionWebhook** \- gibi HTTPWebhook ancak kullanır hello Microsoft tarafından yönetilen API'ler.  
  
-   **Yanıt** \- gelen bir arama için bir yanıt bu eylemi tanımlar.  
  
-   **Bekleyin** \- bu basit işlem sabit bir tutar saat veya belirli bir süre kadar bekler.  
  
-   **İş akışı** \- Bu eylem bir iç içe geçmiş iş akışını temsil eder.  

-   **İşlev** \- Bu eylem bir Azure işlevi temsil eder.

### <a name="collection-actions"></a>Koleksiyon Eylemler

-   **Kapsam** \- bu eylemi diğer Eylemler, mantıksal bir gruplandırmasıdır.

-   **Koşul** \- Bu eylem bir ifadeyi değerlendirir ve hello karşılık gelen sonuç dal yürütür.

-   **ForEach** \- döngü Bu eylem bir dizisini yineler ve her öğe için iç eylemleri gerçekleştirir.

-   **Kadar** \- tootrue bir koşul sonuçları kadar bu döngü eylem iç Eylemler yürütür.
  
Her eylem farklı bir dizi türü **girişleri** bir eylemin davranışını tanımlayın.  
  
## <a name="http-action"></a>HTTP eylemi  

HTTP Eylemler belirtilen uç noktasını çağırmak ve hello yanıt toodetermine hello iş akışının çalışması gerektiğini olup olmadığını denetleyin. Merhaba **girişleri** nesnesini parametreleri gerekli tooconstruct hello HTTP çağrısı hello kümesini alır:  
  
|Öğe adı|Gerekli|Tür|Açıklama|  
|----------------|------------|--------|---------------|  
|Yöntemi|Evet|Dize|HTTP yöntemleri aşağıdaki hello biri olabilir: **almak**, **POST**, **PUT**, **silmek**, **düzeltme eki**, veya  **HEAD**|  
|URI|Evet|Dize|çağrılan hello http veya https uç noktası. En fazla uzunluğu 2 kilobayttır.|  
|Sorguları|Hayır|Nesne|Merhaba sorgu parametreleri tooadd toohello URL'yi temsil eder. Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` toohello URL.|  
|Üstbilgileri|Hayır|Nesne|Her toohello isteği gönderilir hello üstbilgilerinin temsil eder. Örneğin, tooset hello dil ve istek üzerine yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Gövde|Hayır|Nesne|Toohello endpoint gönderilen hello yükünü temsil eder.|  
|retryPolicy|Hayır|Nesne|Merhaba yeniden deneme davranışı 4xx veya 5xx hataları özelleştirmenizi sağlar.|  
|operationsOptions|Hayır|Dize|Özel davranışlar toooverride Hello kümesini tanımlar.|  
|Kimlik doğrulaması|Hayır|Nesne|İstek hello temsil hello yöntemi kimlik doğrulaması. Bu nesne üzerinde daha fazla bilgi için bkz [Scheduler giden bağlantı kimlik doğrulaması](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Zamanlayıcı daha desteklenen bir özellik yok: `authority`. Varsayılan olarak, `https://login.windows.net` belirtilmediğinde, ancak gibi farklı bir kitleye kullanabilirsiniz`https://login.windows\-ppe.net`|  
  
HTTP Eylemler \(ve API bağlantısı\) Eylemler destek ilkeleri yeniden deneyin. Bir yeniden deneme ilkesi toointermittent hataları, HTTP durum işlemleri uygular kodları 408, 429 ve ayrıca tooany bağlantı özel durumlarda 5xx. Bu ilke hello kullanarak açıklanan *retryPolicy* aşağıda gösterildiği gibi tanımlanan nesnesi:
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
Merhaba yeniden deneme aralığı hello ISO 8601 biçiminde belirtilir. Hello en büyük değer bir saat olsa da bu aralık varsayılan ve 20 saniye, en küçük değerini sahiptir. Merhaba varsayılan ve en fazla yeniden deneme sayısı dört saattir. Merhaba yeniden deneme ilkesi tanımı belirtilmezse, bir `fixed` stratejisi varsayılan yeniden deneme sayısı ve aralığı değerlerle kullanılır. toodisable hello yeniden deneme İlkesi ayarlamak türü çok`None`.  
  
Her denemesi arasındaki 30 saniyelik gecikmeyle üç yürütmeleri toplam aralıklı hatalar varsa örneğin, hello aşağıdaki eylemi getirilirken hello en son haberleri iki kez yeniden dener:  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a>Zaman uyumsuz desenleri

Varsayılan olarak, tüm HTTP tabanlı eylemleri hello standart zaman uyumsuz işlem düzenini destekler. Merhaba uzak sunucu bu hello istek gösterirse bir 202 işleme için kabul edilir şekilde \(kabul edilen\) yanıtı hello Logic Apps altyapısı tutar yoklama terminal ulaşmasını kadar hello yanıtın konumu üstbilgisinde belirtilen hello URL'si durumu \(olmayan bir\-202 yanıt\).  
  
toodisable hello zaman uyumsuz davranışı, daha önce açıklandığı gibi ayarlanmış bir `DisableAsyncPattern` hello eylem girişleri seçeneği. Bu durumda, hello eylemin hello çıktı hello ilk 202 yanıt hello sunucusundan temel alır.  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a>Zaman uyumsuz sınırları

Zaman uyumsuz desen kendi süresi tooa belirli bir zaman aralığı içinde sınırlı olabilir.  Terminal durumuna erişmeden Hello zaman aralığı sona erdiğinde, hello eylemin hello durumunu işaretlenecek `Cancelled` koduyla `ActionTimedOut`.  ISO 8601 biçiminde Hello sınırı zaman aşımı belirtildi.  Sınırları sözdizimi aşağıdaki hello ile belirtilebilir:

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a>API bağlantısı  

API bağlantı Microsoft tarafından yönetilen bir bağlayıcı başvuruda bulunan bir eylemdir.
Bu eylem, bir başvuru tooa geçerli bağlantı ve hello API ve gerekli parametreleri hakkında bilgi gerektirir.

|Öğe adı|Gerekli|Tür|Açıklama|  
|----------------|------------|--------|---------------|  
|ana bilgisayar|Evet|Nesne|Merhaba runtimeUrl ve başvuru toohello bağlantı nesnesi gibi Hello bağlayıcı bilgileri temsil eder|
|Yöntemi|Evet|Dize|HTTP yöntemleri aşağıdaki hello biri olabilir: **almak**, **POST**, **PUT**, **silmek**, **düzeltme eki**, veya  **HEAD**|  
|Yol|Evet|Dize|Merhaba API işlemi Hello yolu.|  
|Sorguları|Hayır|Nesne|Merhaba sorgu parametreleri tooadd toohello URL'yi temsil eder. Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` toohello URL.|  
|Üstbilgileri|Hayır|Nesne|Her toohello isteği gönderilir hello üstbilgilerinin temsil eder. Örneğin, tooset hello dil ve istek üzerine yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Gövde|Hayır|Nesne|Toohello endpoint gönderilen hello yükünü temsil eder.|  
|retryPolicy|Hayır|Nesne|Merhaba yeniden deneme davranışı 4xx veya 5xx hataları özelleştirmenizi sağlar.|  
|operationsOptions|Hayır|Dize|Özel davranışlar toooverride Hello kümesini tanımlar.|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a>API bağlantısı Web kancası eylemi

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

Bir Web kancası eylemi sınırları hello belirtilebilir aynı şekilde [HTTP zaman uyumsuz sınırları](#asynchronous-limits).
  
## <a name="response-action"></a>Yanıt eylemi  

Bu eylem türü bir HTTP isteğinden hello tüm yanıt yükü içerir ve bir statusCode, metnini ve üst bilgileri içerir:  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
Merhaba yanıt eylem tooother Eylemler uygulanmaz özel sınırlamalar vardır. Bu avantajlar şunlardır:  
  
-   Belirleyici yanıt toohello gelen isteği gerektiğinden yanıt eylemlerinizi bir tanım paralel olamaz.  
  
-   Merhaba gelen istek yanıt aldıktan sonra bir yanıt eylemi ulaştıysanız, hello eylem olarak kabul başarısız \(çakışma\), ve bunun sonucunda çalıştırmak hello `Failed`.  
  
-   Yanıt eylemleri içeren bir iş akışının olamaz `splitOn` , tetikleyici içinde birçok çalışır bir çağrı neden olduğundan. Sonuç olarak, Hello akış PUT ve nedeni hatalı istek olduğunda bu doğrulanmalıdır.  
  
## <a name="wait-action"></a>Eylem bekleyin  

Merhaba `wait` eylemin hello belirtilen zaman aralığı için iş akışı yürütme askıya alır. Örneğin, toowait 15 dakika, bu kod parçacığında kullanabilirsiniz:  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
Alternatif olarak, toowait zaman belirli bir süre kadar bu örnek kullanabilirsiniz:  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> Merhaba bekleme süresini ya da hello kullanılarak belirtilebilir **aralığı** nesne veya hello **kadar** nesnesi, ancak ikisini birden değil.  
  
|Ad|Gerekli|Tür|Açıklama|  
|--------|------------|--------|---------------|  
|interval|Hayır|Nesne|Merhaba zaman miktarına göre süre bekleyin.|  
|aralığı birimi|Evet|Dize|Bu aralıklar birini: saniye, dakika, saat, gün, hafta, ay, yıl.|  
|Aralık sayısı|Evet|Dize|İç birim verilen hello üzerinde temel süresi.|  
|kadar|Hayır|Nesne|Merhaba zamandaki bir noktasında temel süre bekleyin.|  
|zaman damgası kadar|Evet|Dize|Dize &#124; hello bekleme süresi dolduğunda UTC zamanı başlangıç noktası.|  

## <a name="query-action"></a>Sorgu eylemi

Merhaba `query` eylemi bir koşula göre bir dizi filtre olanak sağlar. Örneğin, 2'den büyük tooselect sayılar, kullanabilirsiniz:

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

Merhaba hello çıktısını `query` hello koşulu karşılıyor hello Giriş dizisinin öğelerinden sahip bir dizi eylemdir.

> [!NOTE]
> Hiçbir değer hello belirtecini karşılıyorsa `where` koşul, hello boş bir dizi sonucudur.

|Ad|Gerekli|Tür|Açıklama|
|--------|------------|--------|---------------|
|Kaynak|Evet|Dizi|Merhaba kaynak dizi.|
|Burada|Evet|Dize|Merhaba kaynak dizinin Hello koşulu tooapply tooeach öğesi.|

## <a name="select-action"></a>Bir eylem seçin

Merhaba `select` eylem yeni bir değer dizideki her öğe proje olanak sağlar.
Örneğin, bir dizi sayılara nesnelerinin dizisi tooconvert kullanabilirsiniz:

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

Merhaba hello çıktısını `select` aynı kardinalite olarak dönüştürülen her bir öğesiyle Giriş dizisinin hello olarak tanımlanan hello hello tarafından sahip bir dizi eylemdir `select` özelliği. Merhaba giriş boş bir dizi hello çıktı da boş bir dizi ise.

|Ad|Gerekli|Tür|Açıklama|
|--------|------------|--------|---------------|
|Kaynak|Evet|Dizi|Merhaba kaynak dizi.|
|seçin|Evet|Herhangi biri|Merhaba kaynak dizinin Hello projeksiyon tooapply tooeach öğesi.|

## <a name="terminate-action"></a>Sonlandırma eylemi

Merhaba sonlandırma eyleminin yürütülen tüm eylemler durduruluyor ve kalan herhangi bir eylem atlanıyor Çalıştır hello iş akışının yürütülmesini durdurur. Örneğin, tooterminate durumuna sahip bir Farklı Çalıştır **başarısız**, aşağıdaki kod parçacığında hello kullanabilirsiniz:

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> Zaten tamamlanmış eylemler tarafından hello etkilenmez sonlandırma eylemi.

|Ad|Gerekli|Tür|Açıklama|
|--------|------------|--------|---------------|
|runStatus|Evet|Dize|Merhaba hedef durumu çalıştırın. Her iki **başarısız** veya **iptal**.|
|runError|Hayır|Nesne|Merhaba hata ayrıntıları. Ne zaman desteklenen yalnızca **runStatus** çok ayarlanır**başarısız**.|
|runError kodu|Hayır|Dize|Merhaba hata kodu çalıştırma.|
|runError iletisi|Hayır|Dize|Merhaba, hata iletisi çalıştırın.|

## <a name="compose-action"></a>Eylem oluşturma

Merhaba Oluştur eylemi, rastgele bir nesne oluşturmak olanak tanır. Merhaba Hello çıktısını oluşturan eylem girdilerinden değerlendirme hello sonucudur. Örneğin, hello kullanabilirsiniz birden çok eylem eylem toomerge çıkışları oluşturun:

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> Merhaba **oluşturma** eylem kullanılan tooconstruct nesneleri, dizileri ve yerel olarak XML ve ikili gibi mantıksal uygulamalar tarafından desteklenen herhangi bir türü de dahil olmak üzere herhangi bir çıktı olabilir.

## <a name="table-action"></a>Tablo eylemi

Merhaba `table` öğeleri dizisi bir tooconvert sağlayan bir **CSV** veya **HTML** tablo.

Varsayalım @triggerBody() değil

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

Ve hello eylem olarak tanımlanması izin verin

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

Yukarıdaki Hello oluşturur

<table><thead><tr><th>id</th><th>ad</th></tr></thead><tbody><tr><td>0</td><td>elmalar</td></tr><tr><td>1</td><td>portakallar</td></tr></tbody></table>"

Sipariş toocustomize hello tabloda hello sütunları açıkça belirtebilirsiniz. Örneğin:

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

Yukarıdaki Hello oluşturur

<table><thead><tr><th>kimliği oluşturmak</th><th>Açıklama</th></tr></thead><tbody><tr><td>0</td><td>Yeni elmalar</td></tr><tr><td>1</td><td>Yeni portakallar</td></tr></tbody></table>"

Merhaba, `from` özellik değeri boş bir dizi, hello çıkış boş bir tablo.

|Ad|Gerekli|Tür|Açıklama|
|--------|------------|--------|---------------|
|Kaynak|Evet|Dizi|Merhaba kaynak dizi.|
|Biçimi|Evet|Dize|Biçim, ya da hello **CSV** veya **HTML**.|
|sütunları|Hayır|Dizi|Merhaba sütun. Merhaba tablonun toooverride hello varsayılan şekil sağlar.|
|sütun başlığı|Hayır|Dize|Merhaba sütunun başlığını Hello.|
|Sütun değeri|Evet|Dize|Merhaba sütunun Hello değeri.|

## <a name="workflow-action"></a>İş akışı eylemi   

|Ad|Gerekli|Tür|Açıklama|  
|--------|------------|--------|---------------|  
|ana bilgisayar kimliği|Evet|Dize|Merhaba iş akışı toocall istediğiniz Hello kaynak kimliği.|  
|ana bilgisayar tetikleyiciadı|Evet|Dize|tooinvoke istediğiniz hello tetikleyici Hello adı.|  
|Sorguları|Hayır|Nesne|Merhaba sorgu parametreleri tooadd toohello URL'yi temsil eder. Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` toohello URL.|  
|Üstbilgileri|Hayır|Nesne|Her toohello isteği gönderilir hello üstbilgilerinin temsil eder. Örneğin, tooset hello dil ve istek üzerine yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Gövde|Hayır|Nesne|Toohello endpoint gönderilen hello yükünü temsil eder.|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
Bir erişim denetimi hello iş akışında yapılan \(daha belirgin olarak hello tetikleyici\), başka bir deyişle toohello iş akışı erişim.  
  
Merhaba çıkarır hello `workflow` eylemin hello tanımlanan dayalı `response` hello alt iş akışı eylemi. Herhangi bir tanımlamadığınız varsa `response` eylemi ve ardından hello çıkışları boş.  

## <a name="function-action"></a>İşlev eylemi   

|Ad|Gerekli|Tür|Açıklama|  
|--------|------------|--------|---------------|  
|İşlev kimliği|Evet|Dize|tooinvoke istediğiniz hello işlevini Hello kaynak kimliği.|  
|Yöntemi|Hayır|Dize|Merhaba HTTP yöntemini tooinvoke hello işlevi kullanılır. Varsayılan olarak, olmasından `POST` belirtilmemiş olduğunda.|  
|Sorguları|Hayır|Nesne|Merhaba sorgu parametreleri tooadd toohello URL'yi temsil eder. Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` toohello URL.|  
|Üstbilgileri|Hayır|Nesne|Her toohello isteği gönderilir hello üstbilgilerinin temsil eder. Örneğin, tooset başlangıç dili ve istek üzerine türü: `"headers" : { "Accept-Language": "en-us" }`.|  
|Gövde|Hayır|Nesne|Toohello endpoint gönderilen hello yükünü temsil eder.|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

Merhaba mantıksal uygulama kaydettiğinizde, biz başvurulan hello işlevi üzerinde bazı denetimler gerçekleştirin:
-   Toohave erişim toohello işlevi gerekir.
-   Yalnızca standart HTTP tetikleyicisi veya genel JSON Web kancası tetikleyici izin verilir.
-   Tanımlı yol olmamalıdır.
-   Yalnızca "işlev" ve "anonim" yetki düzeyini izin verilmez.

Merhaba tetikleme URL'si alınan, önbelleğe alınan ve çalışma zamanında kullanılan. Herhangi bir işlem önbelleğe hello URL geçersiz kılar, dolayısıyla hello eylem çalışma zamanında başarısız olur. Bu, geçici toowork mantığı uygulama tooretrieve neden ve hello tetikleme URL'si tekrar önbelleğe hello mantıksal uygulama yeniden kaydedin.

## <a name="collection-actions-scopes-and-loops"></a>Koleksiyon eylemleri (kapsamlar ve döngüler)

Bazı eylem türleri kendilerini içinde eylemler içerebilir. Bir koleksiyon içinde başvurusu Eylemler doğrudan hello koleksiyonu dışında başvurulabilir. Tanımladıysanız `http` bir kapsamda `@body('http')` herhangi bir iş akışında hala geçerlidir. Bir koleksiyon içinde eylemler için `runAfter` içindeki diğer eylemleri hello aynı koleksiyonu.

## <a name="scope-action"></a>Kapsam eylemi

Merhaba `scope` eylem sağlar, mantıksal olarak bir iş akışında Grup eylemler.

|Ad|Gerekli|Tür|Açıklama|  
|--------|------------|--------|---------------|  
|Eylemler|Evet|Nesne|İç Eylemler tooexecute hello kapsam içinde|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a>ForEach eylemi

Bu döngü eylem bir dizisini yineler ve her öğe için iç eylemleri gerçekleştirir. Varsayılan olarak, paralel (20 yürütmeleri paralel birer birer) hello foreach döngüsü yürütür. Hello kullanarak yürütme kurallarını ayarlayabilmeniz için `operationOptions` parametresi.

|Ad|Gerekli|Tür|Açıklama|  
|--------|------------|--------|---------------|  
|Eylemler|Evet|Nesne|İç Eylemler tooexecute hello döngü içinde|
|foreach|Evet|Dize|Merhaba dizi tooiterate üzerinden|
|operationOptions|Yok|Dize|İşlemi için herhangi bir seçenek davranışı. Şu anda yalnızca destekler `sequential` tooexecute yineleme sırayla (varsayılan davranıştır paralel)|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a>Eylem kadar

Bir koşul tootrue sonuçları kadar bu döngü eylem iç Eylemler yürütür.

|Ad|Gerekli|Tür|Açıklama|  
|--------|------------|--------|---------------|  
|Eylemler|Evet|Nesne|İç Eylemler tooexecute hello döngü içinde|
|ifade|Evet|Dize|Her yinelemeden sonra Hello ifade tooevaluate|
|Sınırı|Evet|Nesne|Merhaba sınırları hello döngü - en az bir sınır için tanımlanmış olması gerekir|
|Sayısı|Yok|Int|Merhaba sınırı toohello gerçekleştirilebilir yineleme sayısı|
|Zaman aşımı|Yok|Dize|ne kadar süreyle döndürmelidir için hello zaman aşımı.  ISO 8601 biçim|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a>-Varsa koşulları eylemi

Merhaba `If` eylem, bir koşulu değerlendirmek ve olup hello ifadeyi çok hesaplar üzerinde dayalı bir dal yürütme sağlar`true`.

|Ad|Gerekli|Tür|Açıklama|  
|--------|------------|--------|---------------|  
|Eylemler|Evet|Nesne|İfade çok değerlendirirken, iç Eylemler tooexecute`true`|
|ifade|Evet|Dize|Merhaba ifade tooevaluate|
|else|Yok|Nesne|İfade çok değerlendirirken, iç Eylemler tooexecute`false`|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
Merhaba aşağıdaki tabloda koşullar bir eylemi ifade nasıl kullanabileceğiniz örnekler gösterilmektedir:  
  
|JSON değeri|Sonuç|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|Tootrue değerlendirecek herhangi bir değer bu koşul toopass neden olur. Yalnızca Boole ifadeleri desteklenir. tooconvert diğer türleri tooBoolean, kullanım işlevleri `empty`, `equals`.|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|Karşılaştırma işlevleri desteklenir. Act1 Hello çıktısını hello eşik değerinden yüksek olduğunda burada hello örneğin hello eylem yalnızca yürütür.|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|Mantığı da desteklenen toocreate Boolean ifadeleri iç içe işlevlerdir. Bu durumda, act1 Hello çıktısını hello eşiğin üstünde veya altında 100 olduğunda hello eylem yürütür.|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|Bir dizinin tüm öğeleri varsa, dizi işlevleri toocheck kullanabilirsiniz. Bu durumda, Hello hataları dizi boş olduğunda hello eylem yürütür.| 
|`"expression": "parameters('hasSpecialAction')"`|Hata - geçerli bir @ için gerekli olduğundan koşul koşulları.|  
  
Bir koşul başarıyla değerlendirilirse hello koşulu olarak işaretlenmiş `Succeeded`. Ya da hello içinde eylemler `actions` veya `else` nesneleri değerlendirmek çok`Succeeded` yürütülen ve başarılı oldu, `Failed` yürütülen ve başarısız olduğunda veya `Skipped` zaman o şubedeki yürütülmez.

## <a name="next-steps"></a>Sonraki adımlar

[İş akışı hizmeti REST API'si](https://docs.microsoft.com/rest/api/logic/workflows)
