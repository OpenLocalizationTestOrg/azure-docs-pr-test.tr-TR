---
title: "İş akışı eylemleri ve Tetikleyicileri - Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: bd3f1d225b974ebde889738bb435825658d1e1e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a>İş akışı eylemleri ve Azure Logic Apps için Tetikleyiciler

Logic apps tetikleyiciler ve Eylemler oluşur. Tetikleyiciler altı tür vardır. Her tür farklı arabirimi ve farklı bir davranışı vardır. Ayrıntılarını bakarak ilgili diğer ayrıntıları öğrenebilirsiniz [iş akışı tanımlama dili](logic-apps-workflow-definition-language.md).  
  
İçin okumaya tetikleyiciler ve Eylemler ve iş süreçlerini ve iş akışları geliştirmek için mantığı uygulamalar oluşturmak için bunları nasıl kullanacağınızı hakkında daha fazla bilgi edinin.  
  
### <a name="triggers"></a>Tetikleyiciler  

Tetikleyicinin mantığını uygulama akışınızın bir farklı çalıştır başlatabilirsiniz çağrıları belirtir. İş akışınızı yürütülmesi başlatmak için iki farklı şekilde şunlardır:  
  
-   Yoklama tetikleyici  

-   Çağırarak itme tetikleyici - [iş akışı hizmeti REST API'si](https://docs.microsoft.com/rest/api/logic/workflows)  
  
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
    "splitOn" : "<property to create runs for>",
    "operationOptions": "<operation options on the trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a>Tetikleyici türlerini ve bunların girişleri  

Bu tür tetikleyici sunucusu kullanabilirsiniz:
  
-   **İstek** \- mantıksal uygulamayı çağırmak size bir uç nokta yapar  
  
-   **Yineleme** \- ateşlenir dayalı tanımlanmış bir zamanlamaya göre  
  
-   **HTTP** \- bir HTTP web uç noktası yoklar. HTTP uç noktası için belirli bir tetikleme sözleşme uymalıdır \- bir 202 kullanarak ya da\-zaman uyumsuz desen veya bir dizi döndürerek  
  
-   **ApiConnection** \- HTTP gibi yoklamalar tetikleyin, ancak bunu yararlanan [Microsoft tarafından yönetilen API'ler](https://docs.microsoft.com/azure/connectors/apis-list)  
  
-   **HTTPWebhook** \- uç noktası, el ile tetikleyici, Bununla birlikte, benzer bir açılır de çağırır kaydedin ve kaydı için belirtilen URL  
  
-   **ApiConnectionWebhook** \- Operates Microsoft tarafından yönetilen API'ları yararlanarak HTTPWebhook tetikleyici gibi       
    Farklı bir kümesini her tetikleyici türünde **girişleri** davranışını tanımlar.  
  
## <a name="request-trigger"></a>Tetikleyici isteği  

Bu tetikleyici bir uç nokta mantıksal uygulamanızı çağırmak için bir HTTP isteği çağıran işlevi görür. Bir istek tetikleyici aşağıdaki gibi görünür:  
  
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
|Şema|Hayır|JSON şeması gelen isteği doğrular. Sonraki iş akışı adımları başvurmak için hangi özelliklerin bilmeniz yardımcı olmak için kullanışlıdır.|

Bu uç noktaya çağrılacak çağırması gerekir *listCallbackUrl* API. Bkz: [iş akışı hizmeti REST API'si](https://docs.microsoft.com/rest/api/logic/workflows).  
  
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

Gördüğünüz gibi bir iş akışını çalıştırmak için basit bir yoludur.  
  
|Öğe adı|Gerekli|Açıklama|  
|----------------|------------|---------------|  
|Sıklık|Evet|Ne sıklıkta tetikleyici yürütür. Bu değerlerden yalnızca birini kullanın: saniye, dakika, saat, gün, hafta, ay veya yıl|  
|aralığı|Evet|Verilen sıklığı aralığını yineleme için|  
|startTime|Hayır|Bir startTime UTC uzaklığı sağlanırsa, bu saat dilimi kullanılır.|  
|saat dilimi|Yok|Bir startTime UTC uzaklığı sağlanırsa, bu saat dilimi kullanılır.|  
  
Ayrıca, belirli bir noktada gelecekte çalıştırmaya başlamak için bir tetikleyici zamanlayabilirsiniz. Örneğin, haftalık bir rapor her Pazartesi başlatmak istiyorsanız aşağıdaki tetikleyici oluşturarak her Pazartesi başlatmak için mantıksal uygulama zamanlayabilirsiniz:  

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

HTTP Tetikleyicileri belirtilen uç nokta yoklamak ve iş akışı yürütülüp yürütülmeyeceğini belirlemek için yanıtı denetleyin. Giriş nesnesi bir HTTP çağrısıyla oluşturmak için gerekli parametreleri kümesini alır:  
  
|Öğe adı|Gerekli|Açıklama|Tür|  
|----------------|------------|---------------|--------|  
|Yöntemi|Evet|Aşağıdaki HTTP yöntemlerden biri olabilir: GET, POST, PUT, DELETE, düzeltme eki veya HEAD|Dize|  
|URI|Evet|Çağrılan http veya https uç noktası. 2 kilobayt sayısı.|Dize|  
|Sorguları|Hayır|URL'ye eklemek için sorgu parametreleri temsil eden bir nesne. Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` URL.|Nesne|  
|Üstbilgileri|Hayır|Her isteği gönderilen üstbilgilerini temsil eden bir nesne. Örneğin, dilini ayarlamak ve bir istek yazmak için şunu yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|Nesne|  
|Gövde|Hayır|Uç noktasına gönderilen yükünü temsil eden bir nesne.|Nesne|  
|retryPolicy|Hayır|4xx veya 5xx hataları yeniden deneme davranışı özelleştirmenize olanak sağlayan bir nesne.|Nesne|  
|Kimlik doğrulaması|Hayır|İsteğin kimliği olduğunu yöntemi temsil eder. Bu nesne üzerinde daha fazla bilgi için bkz [Scheduler giden bağlantı kimlik doğrulaması](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Zamanlayıcı daha desteklenen bir özellik yok: `authority` varsayılan olarak, bu değer `https://login.windows.net` belirtilmediğinde, ancak gibi farklı bir kitleye kullanabilirsiniz`https://login.windows\-ppe.net`|Nesne|  
  
HTTP tetikleyicisini iyi mantığı uygulamanızın üzerinde çalışmak için belirli bir desendeki uygun olması HTTP API gerektiriyor. Aşağıdaki alanları gerektirir:  
  
|Yanıt|Açıklama|  
|------------|---------------|  
|Durum kodu|Durum kodu 200 \(Tamam\) Çalıştır neden olacak. Diğer bir durum kodu bir Farklı Çalıştır neden olmaz.|  
|Yeniden deneme\-üstbilgi sonra|Mantıksal uygulama uç nokta yeniden yoklar kadar saniye sayısı.|  
|Konum üstbilgisi|Sonraki yoklama aralığını üzerinde çağrısı için URL. Belirtilmezse, özgün URL'si kullanılır.|  
  
İstekleri farklı türleri için farklı davranışlar bazı örnekleri şunlardır:  
  
|Yanıt kodu|Yeniden deneme\-sonra|Davranışı|  
|-----------------|----------------|------------|  
|200|\(yok\)|Değil geçerli tetikleyici yeniden deneme\-sonra gereklidir veya başka altyapısı sonraki istek için hiçbir zaman yoklar.|  
|202|60|İş akışı tetiklemez. Sonraki girişiminde bir dakika içinde gerçekleşir.|  
|200|10|İş akışını çalıştırmak ve daha fazla içerik için 10 saniye içinde yeniden kontrol edin.|  
|400|\(yok\)|Hatalı istek, iş akışı çalıştırmayın. Varsa hiçbir **yeniden deneme ilkesi** tanımlanan varsayılan ilke kullanılır. Yeniden deneme sayısı üst sınırına ulaşıldı sonra tetikleyici artık geçerli değil.|  
|500|\(yok\)|Sunucu hatası, iş akışı çalıştırmayın.  Varsa hiçbir **yeniden deneme ilkesi** tanımlanan varsayılan ilke kullanılır. Yeniden deneme sayısı üst sınırına ulaşıldı sonra tetikleyici artık geçerli değil.|  
  
Bir HTTP tetikleyicisi çıkışları aşağıdaki gibi görünür:  
  
|Öğe adı|Açıklama|Tür|  
|----------------|---------------|--------|  
|Üstbilgileri|Http yanıtı üstbilgileri.|Nesne|  
|Gövde|Http yanıt gövdesi.|Nesne|  
  
## <a name="api-connection-trigger"></a>API bağlantı tetikleyici  

API bağlantı tetikleyici temel işlevselliğini HTTP tetikleyicinin benzer. Bununla birlikte, eylem tanımlamak için farklı parametreleridir. Örnek aşağıda verilmiştir:  
  
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
|ana bilgisayar|Evet||Ağ geçidi ve kimliği ApiApp barındırılan.|  
|Yöntemi|Evet|Dize|Aşağıdaki HTTP yöntemlerden biri olabilir: **almak**, **POST**, **PUT**, **silmek**, **düzeltme eki**, veya  **HEAD**|  
|Sorguları|Hayır|Nesne|URL'ye eklenecek sorgu parametreleri temsil eder. Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` URL.|  
|Üstbilgileri|Hayır|Nesne|Her isteği gönderilen üstbilgilerinin temsil eder. Örneğin, dilini ayarlamak ve bir istek yazmak için şunu yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Gövde|Hayır|Nesne|Uç noktasına gönderilen yükünü temsil eder.|  
|retryPolicy|Hayır|Nesne|4xx veya 5xx hataları yeniden deneme davranışını özelleştirmenizi sağlar.|  
|Kimlik doğrulaması|Hayır|Nesne|İsteğin kimliği olduğunu yöntemi temsil eder. Bu nesne üzerinde daha fazla bilgi için bkz [Scheduler giden bağlantı kimlik doğrulaması](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)|  
  
Konak özellikleri şunlardır:  
  
|Öğe adı|Gerekli|Açıklama|  
|----------------|------------|---------------|  
|API runtimeUrl|Evet|Yönetilen API uç noktası.|  
|Bağlantı adı||Adlı bir parametre için bir başvurusu olmalıdır `$connection` ve iş akışının kullandığı yönetilen API bağlantı adıdır.|
  
Bir API bağlantı tetikleyicisi çıkışları şunlardır:
  
|Öğe adı|Tür|Açıklama|  
|----------------|--------|---------------|  
|Üstbilgileri|Nesne|Http yanıtı üstbilgileri.|  
|Gövde|Nesne|Http yanıt gövdesi.|  
  
## <a name="httpwebhook-trigger"></a>HTTPWebhook tetikleyici  

Bir uç nokta, el ile tetikleyiciye benzer HTTPWebhook tetikleyici açar ancak HTTPWebhook tetikleyici de kaydetme ve kaydını kaldırmak için belirtilen URL çağırır. Bir HTTPWebhook tetikleyicisi aşağıdaki gibi görünmelidir örneği şöyledir:  

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

Bu bölümler çoğunu isteğe bağlıdır ve Web kancası davranışını hangi bölümlerinin sağlanan atlanmış veya bağlıdır.  
Bir Web kancası özelliklerini aşağıdaki gibidir:  
  
|Öğe adı|Gerekli|Açıklama|  
|----------------|------------|---------------|  
|abone olma|Hayır|Tetikleyici oluşturulduğunda ve ilk kaydı gerçekleştiren çağrılan giden istek.|  
|Aboneliği Kaldır|Hayır|Tetikleyici silindiğinde giden istek.|  
  
-   **Abone** olaylarını dinleme başlatmak için yaptığı giden çağrıdır. Bu çağrı normal HTTP eylemleri gerçekleştirebilirsiniz parametreleri aynı kümesiyle başlatır. Bu giden çağrı herhangi bir iş akışı herhangi bir şekilde, örneğin, kimlik bilgileri alınır veya tetikleyici giriş parametreleri değiştirmek her değiştiğinde yapılır.
  
    Bu çağrı desteklemek için bir yeni işlevi yoktur: `@listCallbackUrl()`. Bu işlev, bu iş akışındaki belirli Bu tetikleyici için benzersiz bir URL döndürür. Bu hizmet REST kullanan uç noktaları için benzersiz tanımlayıcıyı temsil eder.  
  
-   **Aboneliği** bir işlem Bu tetikleyici geçersiz dahil olmak üzere işler olduğunda çağrılır:  
  
    -   Silme veya tetikleyici devre dışı bırakma  
  
    -   Silme veya iş akışını devre dışı bırakma  
  
    -   Silme veya abonelik devre dışı bırakma  
  
    Mantıksal uygulama otomatik olarak abonelikten eylemini çağırır. Bu işlev parametreleri HTTP tetikleyicisini ile aynıdır.  
  
    Gelen istek içeriği HTTPWebhook tetikleyici çıkışları şunlardır:  
  
|Öğe adı|Tür|Açıklama|  
|-----------------|--------|---------------|  
|Üstbilgileri|Nesne|Http isteği üstbilgileri.|  
|Gövde|Nesne|Http istek gövdesi.|  

Bir Web kancası eylemi sınırları, aynı şekilde belirtilebilir [HTTP zaman uyumsuz sınırları](#asynchronous-limits).
  

## <a name="conditions"></a>Koşullar  

Herhangi bir tetikleyici için iş akışı veya çalıştırılması gerekip gerekmediğini belirlemek için bir veya daha fazla koşulları kullanabilirsiniz. Örneğin:  

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

Bu durumda, rapor yalnızca Tetikleyicileri iş akışı çalışırken `sendReports` parametrenin ayarlanmış true. Son olarak, koşullar tetikleyici durum kodunu başvurabilir. Örneğin, yalnızca Web sitenizin bir durum kodu 500, aşağıdaki gibi geri döndüğünde devre dışı bir iş akışı kazandırın:
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> Herhangi bir ifade tetikleyici durum kodunu başvurduğunda \(herhangi bir şekilde\), varsayılan davranışı \(200 yalnızca Tetikle \(Tamam\) \) değiştirilir. Durum kodu 200 hem 201 durum kodunu tetiklemek istiyorsanız, örneğin, dahil etmek zorunda: `@or(equals(triggers().code, 200),equals(triggers().code,201))` koşulunuz olarak.  
  
## <a name="start-multiple-runs-for-a-request"></a>Bir istek için birden çok çalışmalarını Başlat

Tek bir istek için birden çok çalıştırır kapalı kazandırın için `splitOn` yoklama aralıkları arasında birden çok yeni öğeleri olan bir uç nokta yoklamak istediğinizde, örneğin, yararlıdır.
  
İle `splitOn`, her biri tetikleyicinin çalıştırmasını başlatmak için kullanmak istediğiniz öğeleri dizisi içeren yanıt yükünün özelliğini belirtin. Örneğin, aşağıdaki yanıtı döndüren bir API olduğunu düşünün:  
  
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
  
Bu örnek gibi tetikleyici gerçekleştirebilmesi için mantıksal uygulamanızı yalnızca satır içerik gerekir:  
  
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
  
Daha sonra iş akışı tanımında `@triggerBody().name` döndürür `mycoolrow` ilk çalıştırma için ve `another row` ikinci çalıştırma için. Bu örnek tetikleyici çıkışları görünümlü:  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

Kullanırsanız, bunu `SplitOn`, bu durumda, dizi dışında olan özellikler alınamıyor `Status` alan.  
  
> [!NOTE]  
> Bu örnekte, kullandığımız `?` bir hata durumunda kaçınabilirsiniz işleci `Rows` özelliği mevcut değil. 
  
## <a name="single-run-instance"></a>Tek çalışma örneği

Tüm etkin metinler tamamladıysanız, yalnızca tetiklenecek yinelenme özelliğine sahip Tetikleyicileri yapılandırabilirsiniz. Bir çalıştırma sürüyor olsa zamanlanmış bir yinelenme meydana gelirse, tetikleyici atlar ve yeniden denetlemek için bir sonraki zamanlanmış yinelenme aralığı kadar bekler.

Bu ayar işlemi seçeneklerle yapılandırabilirsiniz:

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
  
-   **ApiConnection** \- Bu eylem HTTP eylemi gibi davranır, ancak Microsoft tarafından yönetilen API'lerini kullanır.  
  
-   **ApiConnectionWebhook** \- gibi HTTPWebhook, ancak Microsoft tarafından yönetilen API'lerini kullanır.  
  
-   **Yanıt** \- gelen bir arama için bir yanıt bu eylemi tanımlar.  
  
-   **Bekleyin** \- bu basit işlem sabit bir tutar saat veya belirli bir süre kadar bekler.  
  
-   **İş akışı** \- Bu eylem bir iç içe geçmiş iş akışını temsil eder.  

-   **İşlev** \- Bu eylem bir Azure işlevi temsil eder.

### <a name="collection-actions"></a>Koleksiyon Eylemler

-   **Kapsam** \- bu eylemi diğer Eylemler, mantıksal bir gruplandırmasıdır.

-   **Koşul** \- Bu eylem bir ifadeyi değerlendirir ve karşılık gelen sonuç dal yürütür.

-   **ForEach** \- döngü Bu eylem bir dizisini yineler ve her öğe için iç eylemleri gerçekleştirir.

-   **Kadar** \- bir koşul true olarak sonuçları kadar bu döngü eylem iç Eylemler yürütür.
  
Her eylem farklı bir dizi türü **girişleri** bir eylemin davranışını tanımlayın.  
  
## <a name="http-action"></a>HTTP eylemi  

HTTP Eylemler belirtilen uç noktasını çağırmak ve iş akışı çalıştırılması gerekip gerekmediğini belirlemek için yanıtı denetleyin. **Girişleri** nesnesini HTTP çağrısıyla oluşturmak için gerekli parametreleri kümesini alır:  
  
|Öğe adı|Gerekli|Tür|Açıklama|  
|----------------|------------|--------|---------------|  
|Yöntemi|Evet|Dize|Aşağıdaki HTTP yöntemlerden biri olabilir: **almak**, **POST**, **PUT**, **silmek**, **düzeltme eki**, veya  **HEAD**|  
|URI|Evet|Dize|Çağrılan http veya https uç noktası. En fazla uzunluğu 2 kilobayttır.|  
|Sorguları|Hayır|Nesne|URL'ye eklemek için sorgu parametreleri temsil eder. Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` URL.|  
|Üstbilgileri|Hayır|Nesne|Her isteği gönderilen üstbilgilerinin temsil eder. Örneğin, dilini ayarlamak ve bir istek yazmak için şunu yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Gövde|Hayır|Nesne|Uç noktasına gönderilen yükünü temsil eder.|  
|retryPolicy|Hayır|Nesne|4xx veya 5xx hataları yeniden deneme davranışını özelleştirmenizi sağlar.|  
|operationsOptions|Hayır|Dize|Geçersiz kılmak için özel davranışları kümesini tanımlar.|  
|Kimlik doğrulaması|Hayır|Nesne|İsteğin kimliği olduğunu yöntemi temsil eder. Bu nesne üzerinde daha fazla bilgi için bkz [Scheduler giden bağlantı kimlik doğrulaması](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Zamanlayıcı daha desteklenen bir özellik yok: `authority`. Varsayılan olarak, `https://login.windows.net` belirtilmediğinde, ancak gibi farklı bir kitleye kullanabilirsiniz`https://login.windows\-ppe.net`|  
  
HTTP Eylemler \(ve API bağlantısı\) Eylemler destek ilkeleri yeniden deneyin. 408, 429 ve tüm bağlantı özel durumları yanı sıra 5xx aralıklı hatalar, HTTP durum kodları işlemleri için bir yeniden deneme ilkesi uygulanır. Bu ilke kullanılarak tanımlanır *retryPolicy* aşağıda gösterildiği gibi tanımlanan nesnesi:
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
Yeniden deneme aralığını ISO 8601 biçiminde belirtilir. En büyük değer bir saat olsa da bu aralığı 20 saniye varsayılan ve en az değerine sahip. Varsayılan ve en fazla yeniden deneme sayısı dört saattir. Yeniden deneme ilkesi tanımı belirtilmezse, bir `fixed` stratejisi varsayılan yeniden deneme sayısı ve aralığı değerlerle kullanılır. Yeniden deneme ilkesi devre dışı bırakmak için türünü ayarlamak `None`.  
  
Her denemesi arasındaki 30 saniyelik gecikmeyle üç yürütmeleri toplam aralıklı hatalar varsa en son haberleri iki kez getiriliyor. Örneğin, aşağıdaki eylem yeniden deneme sayısı:  
  
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

Varsayılan olarak, tüm HTTP tabanlı eylemleri standart zaman uyumsuz işlem düzenini destekler. Uzak sunucu isteği bir 202 işleme için kabul edilir olduğunu gösteriyorsa, bunu \(kabul edilen\) yanıt, Logic Apps altyapısı tutar yoklama terminaldurumunaulaşmasınıkadaryanıtınkonumuüstbilgisindebelirtilenURL\(olmayan bir\-202 yanıt\).  
  
Daha önce açıklanan zaman uyumsuz davranışı devre dışı bırakmak için ayarlanmış bir `DisableAsyncPattern` eylem girişleri seçeneği. Bu durumda, eylemin çıkış sunucusundan ilk 202 yanıt temel alır.  
  
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

Zaman uyumsuz desen süresinin belirli bir zaman aralığı için sınırlı olabilir.  Terminal durumuna erişmeden zaman aralığını aşılırsa, eylemin durumunu işaretlenecek `Cancelled` koduyla `ActionTimedOut`.  Sınır zaman aşımı ISO 8601 biçiminde belirtilir.  Sınırları, aşağıdaki sözdizimi ile belirtilebilir:

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
Bu eylem geçerli bir bağlantı ve API ve gerekli parametreleri hakkında bilgi için bir başvuru gerektirir.

|Öğe adı|Gerekli|Tür|Açıklama|  
|----------------|------------|--------|---------------|  
|ana bilgisayar|Evet|Nesne|Bağlantı nesnesine başvuru ve runtimeUrl gibi bağlayıcı bilgileri temsil eder|
|Yöntemi|Evet|Dize|Aşağıdaki HTTP yöntemlerden biri olabilir: **almak**, **POST**, **PUT**, **silmek**, **düzeltme eki**, veya  **HEAD**|  
|Yol|Evet|Dize|API işlemi yolu.|  
|Sorguları|Hayır|Nesne|URL'ye eklemek için sorgu parametreleri temsil eder. Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` URL.|  
|Üstbilgileri|Hayır|Nesne|Her isteği gönderilen üstbilgilerinin temsil eder. Örneğin, dilini ayarlamak ve bir istek yazmak için şunu yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Gövde|Hayır|Nesne|Uç noktasına gönderilen yükünü temsil eder.|  
|retryPolicy|Hayır|Nesne|4xx veya 5xx hataları yeniden deneme davranışını özelleştirmenizi sağlar.|  
|operationsOptions|Hayır|Dize|Geçersiz kılmak için özel davranışları kümesini tanımlar.|  

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

Bir Web kancası eylemi sınırları, aynı şekilde belirtilebilir [HTTP zaman uyumsuz sınırları](#asynchronous-limits).
  
## <a name="response-action"></a>Yanıt eylemi  

Bu eylem türü bir HTTP isteği tüm yanıt yükü içerir ve bir statusCode, metnini ve üst bilgileri içerir:  
  
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
  
Yanıt eylemi diğer eylemler için uygulama özel sınırlamalar vardır. Bu avantajlar şunlardır:  
  
-   Gelen istek belirleyici yanıt gerektiğinden yanıt eylemlerinizi bir tanım paralel olamaz.  
  
-   Gelen istek yanıt aldıktan sonra bir yanıt eylemi ulaştıysanız, eylem olarak kabul başarısız \(çakışma\), ve sonuç olarak, çalışma `Failed`.  
  
-   Yanıt eylemleri içeren bir iş akışının olamaz `splitOn` , tetikleyici içinde birçok çalışır bir çağrı neden olduğundan. Sonuç olarak, akış PUT ve nedeni hatalı istek olduğunda bu doğrulanmalıdır.  
  
## <a name="wait-action"></a>Eylem bekleyin  

`wait` Eylem iş akışı yürütme belirtilen zaman aralığı için askıya alır. Örneğin, 15 dakika beklemek için bu parçacığı kullanabilirsiniz:  
  
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
  
Alternatif olarak, zaman içinde belirli bir süre kadar beklemek için bu örnek kullanabilirsiniz:  
  
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
> Bekleme süresi kullanılarak da belirtilebilir **aralığı** nesne veya **kadar** nesnesi, ancak ikisini birden değil.  
  
|Ad|Gerekli|Tür|Açıklama|  
|--------|------------|--------|---------------|  
|aralığı|Hayır|Nesne|Zaman miktarına bağlı bekleme süresi.|  
|aralığı birimi|Evet|Dize|Bu aralıklar birini: saniye, dakika, saat, gün, hafta, ay, yıl.|  
|Aralık sayısı|Evet|Dize|Verilen iç birimine dayalı süresi.|  
|kadar|Hayır|Nesne|Bekleme süresi bir noktasında zaman dayanır.|  
|zaman damgası kadar|Evet|Dize|Dize &#124; Bekleme süresi dolduğunda UTC zaman içinde nokta.|  

## <a name="query-action"></a>Sorgu eylemi

`query` Eylemi bir koşula göre bir dizi filtre olanak sağlar. Örneğin, 2'den büyük sayılar seçmek için kullanabilirsiniz:

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

Çıktısını `query` koşulu karşılıyor giriş dizisi öğelerinden sahip bir dizi eylemdir.

> [!NOTE]
> Hiçbir değer belirtecini karşılıyorsa `where` sonucu durumudur boş bir dizi.

|Ad|Gerekli|Tür|Açıklama|
|--------|------------|--------|---------------|
|Kaynak|Evet|Dizi|Kaynak dizi.|
|Burada|Evet|Dize|Kaynak dizinin her öğeye uygulamak için koşulu.|

## <a name="select-action"></a>Bir eylem seçin

`select` Eylemi yeni bir değer dizideki her öğe proje olanak sağlar.
Örneğin, bir dizi sayının nesnelerinin bir dizisi dönüştürmek için kullanabilirsiniz:

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

Çıktısını `select` giriş dizisi olarak aynı kardinalite tarafından tanımlandığı şekilde dönüştürülmüş her öğeye sahip olan bir dizi eylemdir `select` özelliği. Girdi boş bir dizi çıkışı da boş bir dizi ise.

|Ad|Gerekli|Tür|Açıklama|
|--------|------------|--------|---------------|
|Kaynak|Evet|Dizi|Kaynak dizi.|
|seçin|Evet|Herhangi biri|Kaynak dizinin her öğeye uygulamak için yansıtma.|

## <a name="terminate-action"></a>Sonlandırma eylemi

Sonlandırma eyleminin yürütülen tüm eylemler durduruluyor ve kalan herhangi bir eylem atlanıyor iş akışı çalışmanın yürütülmesi durdurur. Örneğin, bir çalışma durumuna sahip sonlandırmak için **başarısız**, aşağıdaki kod parçacığında kullanabilirsiniz:

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
> Zaten tamamlanmış Eylemler Sonlandır eylemi tarafından etkilenmez.

|Ad|Gerekli|Tür|Açıklama|
|--------|------------|--------|---------------|
|runStatus|Evet|Dize|Hedef durumu çalıştırma. Her iki **başarısız** veya **iptal**.|
|runError|Hayır|Nesne|Hata ayrıntıları. Ne zaman desteklenen yalnızca **runStatus** ayarlanır **başarısız**.|
|runError kodu|Hayır|Dize|Çalışma hata kodu.|
|runError iletisi|Hayır|Dize|Çalışma hata iletisi.|

## <a name="compose-action"></a>Eylem oluşturma

Oluşturma eylem rastgele bir nesne oluşturmak olanak sağlar. Oluşturma eylem çıktısını girdilerinden değerlendirme sonucudur. Örneğin, birden çok eylem çıkışları birleştirmek için oluşturma eylemini kullanabilirsiniz:

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
> **Oluşturma** eylem nesneleri, dizileri ve yerel olarak XML ve ikili gibi mantıksal uygulamalar tarafından desteklenen herhangi bir türü de dahil olmak üzere herhangi bir çıktı oluşturmak için kullanılabilir.

## <a name="table-action"></a>Tablo eylemi

`table` Öğeleri dizisi dönüştürmenize olanak sağlayan bir **CSV** veya **HTML** tablo.

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

Ve olarak tanımladığı eylem izin verin

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

Yukarıdaki oluşturur

<table><thead><tr><th>id</th><th>ad</th></tr></thead><tbody><tr><td>0</td><td>elmalar</td></tr><tr><td>1</td><td>portakallar</td></tr></tbody></table>"

Tablo özelleştirmek için sütunları açıkça belirtebilirsiniz. Örneğin:

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

Yukarıdaki oluşturur

<table><thead><tr><th>kimliği oluşturmak</th><th>Açıklama</th></tr></thead><tbody><tr><td>0</td><td>Yeni elmalar</td></tr><tr><td>1</td><td>Yeni portakallar</td></tr></tbody></table>"

Varsa `from` özellik değeri boş bir dizi, çıktı boş bir tablo.

|Ad|Gerekli|Tür|Açıklama|
|--------|------------|--------|---------------|
|Kaynak|Evet|Dizi|Kaynak dizi.|
|Biçimi|Evet|Dize|Biçim ya da **CSV** veya **HTML**.|
|sütunları|Hayır|Dizi|Sütunlar. Tablonun varsayılan Şekil geçersiz kılmasını sağlar.|
|sütun başlığı|Hayır|Dize|Sütun başlığı.|
|Sütun değeri|Evet|Dize|Sütun değeri.|

## <a name="workflow-action"></a>İş akışı eylemi   

|Ad|Gerekli|Tür|Açıklama|  
|--------|------------|--------|---------------|  
|ana bilgisayar kimliği|Evet|Dize|Aramak istediğiniz iş akışı kaynak kimliği.|  
|ana bilgisayar tetikleyiciadı|Evet|Dize|Çağrılacak istediğiniz Tetikleyici adı.|  
|Sorguları|Hayır|Nesne|URL'ye eklemek için sorgu parametreleri temsil eder. Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` URL.|  
|Üstbilgileri|Hayır|Nesne|Her isteği gönderilen üstbilgilerinin temsil eder. Örneğin, dilini ayarlamak ve bir istek yazmak için şunu yazın:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|Gövde|Hayır|Nesne|Uç noktasına gönderilen yükünü temsil eder.|  
  
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
  
Bir erişim denetimi akışında yapılan \(daha belirgin olarak tetikleyici\), iş akışı erişmesi gereken anlamına gelir.  
  
Çıkışlarından `workflow` eylem ne tanımlanan üzerinde dayalı `response` alt iş akışı eylemi. Herhangi bir tanımlamadığınız varsa `response` eylemi ve ardından çıkışları boş.  

## <a name="function-action"></a>İşlev eylemi   

|Ad|Gerekli|Tür|Açıklama|  
|--------|------------|--------|---------------|  
|İşlev kimliği|Evet|Dize|Çağırmak için istediğiniz işlev kaynak kimliği.|  
|Yöntemi|Hayır|Dize|İşlevi çağırmak için kullanılan HTTP yöntemi. Varsayılan olarak, olmasından `POST` belirtilmemiş olduğunda.|  
|Sorguları|Hayır|Nesne|URL'ye eklemek için sorgu parametreleri temsil eder. Örneğin, `"queries" : { "api-version": "2015-02-01" }` ekler `?api-version=2015-02-01` URL.|  
|Üstbilgileri|Hayır|Nesne|Her isteği gönderilen üstbilgilerinin temsil eder. Örneğin, bir isteği dil ve türünü ayarlamak için: `"headers" : { "Accept-Language": "en-us" }`.|  
|Gövde|Hayır|Nesne|Uç noktasına gönderilen yükünü temsil eder.|  

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

Mantıksal uygulama kaydettiğinizde, biz başvurulan işlev üzerinde bazı denetimler gerçekleştirin:
-   İşlev erişiminizin olması gerekir.
-   Yalnızca standart HTTP tetikleyicisi veya genel JSON Web kancası tetikleyici izin verilir.
-   Tanımlı yol olmamalıdır.
-   Yalnızca "işlev" ve "anonim" yetki düzeyini izin verilmez.

Tetikleme URL'si alınan, önbelleğe alınmış ve çalışma zamanında kullanılır. Herhangi bir işlem önbelleğe alınmış URL'sini geçersiz kılar, dolayısıyla eylemi çalışma zamanında başarısız olur. Bu sorunu çözmek için almak ve tetikleme URL'si tekrar önbelleğe mantıksal uygulama neden olacak mantıksal uygulama yeniden kaydedin.

## <a name="collection-actions-scopes-and-loops"></a>Koleksiyon eylemleri (kapsamlar ve döngüler)

Bazı eylem türleri kendilerini içinde eylemler içerebilir. Bir koleksiyon içinde başvurusu Eylemler doğrudan dışında koleksiyonu başvurulabilir. Tanımladıysanız `http` bir kapsamda `@body('http')` herhangi bir iş akışında hala geçerlidir. Bir koleksiyon içinde eylemler olabilir `runAfter` yalnızca aynı koleksiyondaki diğer eylemler.

## <a name="scope-action"></a>Kapsam eylemi

`scope` Eylem sağlar, mantıksal olarak bir iş akışında Grup eylemler.

|Ad|Gerekli|Tür|Açıklama|  
|--------|------------|--------|---------------|  
|Eylemler|Evet|Nesne|Kapsam içinde yürütmek için iç Eylemler|

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

Bu döngü eylem bir dizisini yineler ve her öğe için iç eylemleri gerçekleştirir. Varsayılan olarak, (20 yürütmeleri paralel birer birer) paralel foreach döngüsü yürütür. Yürütme kurallarını kullanarak ayarlayabilirsiniz `operationOptions` parametresi.

|Ad|Gerekli|Tür|Açıklama|  
|--------|------------|--------|---------------|  
|Eylemler|Evet|Nesne|Döngü içinde yürütmek için iç Eylemler|
|foreach|Evet|Dize|Dizi üzerinden yineleme|
|operationOptions|Yok|Dize|İşlemi için herhangi bir seçenek davranışı. Şu anda yalnızca destekler `sequential` yineleme sırayla yürütmek için (varsayılan davranıştır paralel)|

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

Bir koşul true olarak sonuçları kadar bu döngü eylem iç Eylemler yürütür.

|Ad|Gerekli|Tür|Açıklama|  
|--------|------------|--------|---------------|  
|Eylemler|Evet|Nesne|Döngü içinde yürütmek için iç Eylemler|
|ifade|Evet|Dize|Her yinelemeden sonra değerlendirilecek ifade|
|Sınırı|Evet|Nesne|Döngü - en az bir sınır sınırlarını tanımlanmış olması gerekir|
|Sayısı|Yok|Int|Gerçekleştirilebilir yineleme sayısını sınırla|
|Zaman aşımı|Yok|Dize|Ne kadar süreyle döndürmelidir için zaman aşımı.  ISO 8601 biçim|


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

`If` Eylem, bir koşulu değerlendirmek ve olup olmadığını ifade değerlendiren üzerinde dayalı bir dal yürütme sağlar `true`.

|Ad|Gerekli|Tür|Açıklama|  
|--------|------------|--------|---------------|  
|Eylemler|Evet|Nesne|İfade olarak değerlendirildiğinde yürütmek için iç Eylemler`true`|
|ifade|Evet|Dize|Değerlendirilecek ifade|
|else|Yok|Nesne|İfade olarak değerlendirildiğinde yürütmek için iç Eylemler`false`|
  
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
  
Aşağıdaki tabloda koşullar bir eylemi ifade nasıl kullanabileceğiniz örnekler gösterilmektedir:  
  
|JSON değeri|Sonuç|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|True olarak değerlendirecek herhangi bir değer geçirmek bu koşul neden olur. Yalnızca Boole ifadeleri desteklenir. Diğer türleri Boolean değerine dönüştürmek için işlevlerini kullanın `empty`, `equals`.|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|Karşılaştırma işlevleri desteklenir. Act1 çıktısı eşik değerinden yüksek olduğunda örnek için eylem yalnızca yürütür.|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|Mantığı işlevleri iç içe geçmiş Boole ifadeleri oluşturmak için de desteklenir. Bu durumda, act1 çıktısını eşiğin üstünde veya altında 100 olduğunda eylemi yürütür.|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|Dizi işlevleri, bir dizinin tüm öğeleri olup olmadığını denetlemek için kullanabilirsiniz. Bu durumda, hataları dizi boş olduğunda eylemi yürütür.| 
|`"expression": "parameters('hasSpecialAction')"`|Hata - geçerli bir @ için gerekli olduğundan koşul koşulları.|  
  
Bir koşul başarıyla değerlendirilirse koşul olarak işaretlenmiş `Succeeded`. Ya da içinde eylemler `actions` veya `else` nesneleri değerlendirmek için `Succeeded` yürütülen ve başarılı oldu, `Failed` yürütülen ve başarısız olduğunda veya `Skipped` zaman o şubedeki yürütülmez.

## <a name="next-steps"></a>Sonraki adımlar

[İş akışı hizmeti REST API'si](https://docs.microsoft.com/rest/api/logic/workflows)
