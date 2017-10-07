---
title: "aaaCreate web API'leri & Bağlayıcılar - Azure mantıksal uygulamaları olarak REST API'leri | Microsoft Docs"
description: "Web API'leri & REST API'leri toocall API'leri, hizmetler veya sistemlerde sistem tümleştirmeleri Azure Logic Apps ile iş akışları oluşturun"
keywords: "Web API'leri, REST API'leri, bağlayıcılar, iş akışları, sistem tümleştirmeler"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: bd229179-7199-4aab-bae0-1baf072c7659
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/26/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 2792204d1d298a6f810e75211c1789ee204c2fdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-apis-as-connectors-for-logic-apps"></a>Bağlayıcılar mantıksal uygulamalar için olarak özel API oluşturma

Azure mantıksal uygulamaları sunmasına karşın [100 + yerleşik Bağlayıcılar](../connectors/apis-list.md) mantığı uygulama akışlarında kullanabilirsiniz, toocall API'leri, sistemleri, isteyebilirsiniz ve Hizmetleri, bağlayıcılar kullanıma sunulmaz. Mantıksal uygulamalar eylemleri ve Tetikleyicileri toouse sağlamak, kendi özel API'leri oluşturabilirsiniz. Neden isteyebileceğiniz toocreate kendi diğer nedenleri API'leri logic apps, bağlayıcılar olarak çok kullanın:

* Geçerli sisteminizi tümleştirme ve veri tümleştirme iş akışları genişletir.
* Müşterilerin servis toomanage professional ya da kişisel görevleri kullanmalarını sağlamak.
* Merhaba ulaşma, bulunabilirliği ve hizmetiniz için kullanım genişletin.

Temel olarak, web takılabilir arabirimleri için REST kullan API'leri bağlayıcılar olan [Swagger meta veri biçimi](http://swagger.io/specification/) belgelerine ve JSON olarak kendi veri değişimi biçimi. Bağlayıcılar HTTP uç noktaları iletişim kuran REST API'leri olduğundan, .NET, Java veya Node.js gibi herhangi bir dil bağlayıcılar oluşturmak için kullanabilirsiniz. Üzerinde Apı'lerinizi barındırabilir [Azure App Service](../app-service/app-service-value-prop-what-is.md), bir platform olarak-sağlayan hello en iyi, kolay ve en ölçeklenebilir yollarından biri, API barındırmak için sunan hizmet (PaaS). 

Logic apps ile özel API'leri toowork için API'nizi sağlayabilir [ *Eylemler* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) mantığı uygulama akışlarında belirli görevleri gerçekleştirebilir. API'nizi de olarak davranıp bir [ *tetikleyici* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) , başlayan bir mantıksal uygulama iş akışı yeni veri ya da bir olay bir belirtilen koşulu karşılıyorsa. Bu konu, Eylemler ve tetikleyicileri, API oluşturmak için takip edebilirsiniz ortak desenler açıklar, API tooprovide istediğiniz hello davranışı temelinde.

> [!TIP] 
> API olarak dağıtabilir ancak [web uygulamaları](../app-service-web/app-service-web-overview.md), Apı'lerinizi olarak dağıtmayı göz önünde bulundurun [API uygulamaları](../app-service-api/app-service-api-apps-why-best-platform.md), hangi yapabilir, işinizi daha kolay yapı, ana bilgisayar ve API'ler hello bulutta ve şirket içi kullanabilir. Herhangi bir kod Apı'leriniz toochange yok--yalnızca kod tooan API uygulamanızı dağıtın. Nasıl çok öğrenin [ASP.NET ile oluşturulan API uygulamaları derleme](../app-service-api/app-service-api-dotnet-get-started.md), [Java](../app-service-api/app-service-api-java-api-app.md), veya [Node.js](../app-service-api/app-service-api-nodejs-api-app.md). 
>
> Logic apps için yerleşik API uygulaması örnekleri için hello ziyaret [Azure Logic Apps GitHub deposunu](http://github.com/logicappsio) veya [blog](http://aka.ms/logicappsblog).

## <a name="helpful-tools"></a>Yararlı Araçlar

Merhaba API de sahip olduğunda özel bir API logic apps ile en iyi şekilde çalışır. bir [Swagger belgesinin](http://swagger.io/specification/) hello API'nin işlemlerini ve parametrelerini açıklar.
Birçok kitaplıkları, ister [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle), hello Swagger dosyası sizin için otomatik olarak oluşturur. tooannotate hello Swagger dosyası görünen adlar, özellik türleri ve benzeri için de kullanabilirsiniz [TRex](https://github.com/nihaue/TRex) böylece Swagger dosyanızın iyi logic apps ile çalışır.

<a name="actions"></a>

## <a name="action-patterns"></a>Eylem desenleri

Logic apps tooperform görevler için özel API'nizi sağlamalıdır [ *Eylemler*](./logic-apps-what-are-logic-apps.md#logic-app-concepts). Her bir işlemde API'nizi tooan eylem eşler. HTTP istekleri ve HTTP yanıtlarını döndürür kabul eden bir denetleyici buna temel bir eylemdir. Bu nedenle örneğin bir mantıksal uygulama, bir HTTP isteği tooyour web uygulaması veya API uygulaması gönderir. Uygulamanızı daha sonra bir HTTP yanıtı döndürür, uygulama mantığını hello içeriği ile birlikte işleyebilir.

Standart bir eylemi için bir HTTP istek yöntemi API'nizi yazma ve bu yöntem bir Swagger dosyasında açıklayın. Ardından, API ile doğrudan çağıran bir [HTTP eylemi](../connectors/connectors-native-http.md) veya bir [HTTP + Swagger](../connectors/connectors-native-http-swagger.md) eylem. Varsayılan olarak, yanıtları içinde hello döndürülmelidir [istek zaman aşımı sınırı](./logic-apps-limits-and-config.md). 

![Standart eylem düzeni](./media/logic-apps-create-api-app/standard-action.png)

<a name="pattern-overview"></a>bir mantıksal uygulama bekleyin, API uzun çalışan görevler tamamlarken toomake API'nizi izleyin hello [zaman uyumsuz yoklama düzeni](#async-pattern) veya hello [zaman uyumsuz Web kancası düzeni](#webhook-actions) bu konuda açıklanan. Benzetme her zaman bu desenleri farklı davranışlar görselleştirmenize yardımcı olan bir firincilik gelen özel pasta sıralama işlemi hello düşünün. Merhaba yoklama düzeni hello kek hazır olup olmadığını burada hello firincilik her 20 dakikada toocheck çağırmanız hello davranışı yansıtır. Merhaba Web kancası düzeni hello kek hazır olduğunda bunlar çağırabilirsiniz şekilde burada hello firincilik, telefon numaranızı ister hello davranışı yansıtır.

Merhaba örnekleri için ziyaret [Logic Apps GitHub deposunu](https://github.com/logicappsio). Ayrıca, daha fazla bilgi edinmek [eylemler için kullanım ölçümü](logic-apps-pricing.md).

<a name="async-pattern"></a>

### <a name="perform-long-running-tasks-with-hello-polling-action-pattern"></a>Eylem düzeni yoklama hello ile uzun süre çalışan görevleri

API'nizi hello daha uzun çalıştırabilir görevler gerçekleştirir toohave [istek zaman aşımı sınırı](./logic-apps-limits-and-config.md), hello yoklama zaman uyumsuz desen kullanabilirsiniz. Bu desen bir ayrı bir iş parçacığı, ancak Canlı etkin bağlantı toohello Logic Apps altyapının iş, API sahiptir. Bu şekilde hello mantıksal uygulama zaman aşımına desteklemez veya çalışma API'nizi tamamlanmadan önce hello hello iş akışı bir sonraki adımına devam edin.

Merhaba genel düzeni şöyledir:

1. API'nizi hello isteği kabul ve çalışmaya başladı hello altyapının bilir emin olun.
2. İş durumu için sonraki istek Hello altyapısı yaptığında, API'nizi hello görev tamamlandığında bilmeniz hello altyapısı sağlar.
3. Merhaba mantığı uygulama iş akışı devam edebilmesi için ilgili veri toohello altyapısı döndür.

<a name="bakery-polling-action"></a>Şimdi hello önceki firincilik benzerleme toohello yoklama deseni uygulamak ve firincilik ve sıra özel pasta teslim edilmek üzere çağırırsınız olduğunu düşünün. Merhaba kek sağlama hello işlem sürüyor ve hello firincilik hello kek üzerinde çalışırken hello Phone toowait istemiyorum. Hello firincilik siparişinizi onaylar ve 20 dakikada bir hello kek'ın durum çağrı sahiptir. 20 dakika geçmesi sonra hello firincilik çağrısı, ancak, pasta işiniz değil ve, başka bir programda 20 dakika çağırmalıdır bunlar size. Bu arka İleri işlemini çağırın ve siparişinizin hazır ve, pasta teslim hello firincilik size bildirir kadar devam eder. 

Bu yoklama deseni geri sağlandığından eşleyin. hello kek müşteri hello Logic Apps altyapısı temsil ederken hello firincilik özel API'nizi temsil eder. Merhaba altyapısı API'nizi isteğiyle çağırdığında API'nizi hello isteği onaylar ve hello altyapısı iş durumunu denetleyebilir, hello zaman aralığı ile yanıt verir. Merhaba altyapısı bu hello iş yapılır API'nize yanıt verene kadar iş durumu ve iş akışı devam edip döndürür veri tooyour mantığı uygulamasını denetleme devam eder. 

![Yoklama eylem düzeni](./media/logic-apps-create-api-app/custom-api-async-action-pattern.png)

Merhaba hello API'nin açısından açıklanan, API toofollow için belirli adımlar şunlardır:

1. Ne zaman API'nizi alır bir HTTP isteği toostart iş, hemen dönüş bir HTTP `202 ACCEPTED` hello yanıtıyla `location` daha sonra bu adımda anlatıldığı üstbilgi. Bu yanıt isteği, kabul edilen hello isteği Yükü (veri giriş) Logic Apps altyapısı bilmeniz API'nizi aldığınız hello hello sağlar ve şu anda işleniyor. 
   
   Merhaba `202 ACCEPTED` yanıt bu üstbilgileri içermelidir:
   
   * *Gerekli*: A `location` burada hello Logic Apps altyapısı kontrol edebilirsiniz, API'nin iş durumu hello mutlak bir yol tooa URL'yi belirtir üstbilgisi

   * *İsteğe bağlı*: A `retry-after` hello altyapısı hello saniye sayısını belirtir üstbilgi hello denetlemeden önce beklemesi gereken `location` iş durumu için URL. 

     Varsayılan olarak, her 20 saniye hello altyapısı denetler. toospecify farklı bir zaman aralığı dahil hello `retry-after` üstbilgi ve hello hello sonraki yoklama kadar saniye sayısı.

2. Hello belirtilen süreden sonra hello Logic Apps yoklamalar hello altyapısı `location` URL toocheck iş durumu. API'nizi, bu denetimleri gerçekleştirmek ve bu yanıtları döndürür:
   
   * Merhaba iş yapıldığında, bir HTTP dönmek `200 OK` hello yanıt Yükü (Merhaba sonraki adım için giriş) yanı sıra yanıt.

   * Merhaba iş hala işliyorsa, başka bir HTTP dönmek `202 ACCEPTED` yanıt, ancak hello hello özgün yanıt olarak aynı üstbilgileri.

API'nizi bu deseni izlediğinde, iş durumunu denetleme hello mantığı uygulama iş akışı tanımı toocontinue içinde herhangi bir şey toodo yok. Ne zaman hello altyapısı alır bir HTTP `202 ACCEPTED` yanıt ve geçerli bir `location` üstbilgi, hello altyapısı gizliliğinize hello zaman uyumsuz desen ve denetimleri hello `location` API'nizi 202 olmayan yanıt dönene kadar üstbilgi.

> [!TIP]
> Örnek zaman uyumsuz desen için bu gözden [zaman uyumsuz denetleyici yanıt örnek github'da](https://github.com/logicappsio/LogicAppsAsyncResponseSample).

<a name="webhook-actions"></a>

### <a name="perform-long-running-tasks-with-hello-webhook-action-pattern"></a>Merhaba Web kancası eylem desen ile uzun süre çalışan görevleri gerçekleştirme

Alternatif olarak, uzun süre çalışan görevler ve zaman uyumsuz işleme için hello Web kancası desen kullanabilirsiniz. Bu desen duraklatma ve iş akışı devam etmeden önce işleme, API toofinish ten "geri" bekleyin hello mantıksal uygulama vardır. Bir olay gerçekleştiğinde, bir ileti tooa URL gönderen bir HTTP POST aramasıdır. 

<a name="bakery-webhook-action"></a>Şimdi hello önceki firincilik benzerleme toohello Web kancası deseni uygulamak ve firincilik ve sıra özel pasta teslim edilmek üzere çağırırsınız olduğunu düşünün. Merhaba kek sağlama hello işlem sürüyor ve hello firincilik hello kek üzerinde çalışırken hello Phone toowait istemiyorum. siparişinizi Hello firincilik onaylar, ancak hello kek yapıldığında bunlar çağırabilirsiniz şekilde bu süre, telefon numaranızı vermediğiniz. Bu süre, hello firincilik zaman siparişinizi hazır ve, pasta teslim söyler.

Biz bu Web kancası deseni yeniden eşlediğinizde, hello firincilik, hello kek müşteri, temsil hello Logic Apps altyapısı yüklenirken özel API'nizi temsil eder. Merhaba altyapısı, bir istekle, API çağrılarının ve "geri çağırma" URL'sini içerir.
Merhaba işi tamamlandığında, API hello URL toonotify hello altyapısını kullanır ve iş akışı devam edip veri tooyour mantıksal uygulama döndürür. 

Bu model için iki uç nokta denetleyicinizde ayarlayın: `subscribe` ve`unsubscribe`

*  `subscribe`uç nokta: yürütme API eylemin hello iş akışında ulaştığında hello Logic Apps çağrıları hello altyapısı `subscribe` uç noktası. Bu adım, API depolayan ve ardından iş tamamlandığında, API'sinden hello geri çağırma bekleyin bir geri çağırma URL'si hello mantığı uygulama toocreate neden olur. API'nizi daha sonra geri birlikte bir HTTP POST toohello URL arar ve döndürülen içeriği ve üstbilgileri giriş toohello mantıksal uygulama geçirir.

* `unsubscribe`uç nokta: hello mantıksal uygulama çalıştırma iptal ederseniz, hello Logic Apps çağrıları hello altyapısı `unsubscribe` uç noktası. API'nizi hello geri çağırma URL'si kaydı ve gerektiği gibi tüm işlemleri durdur.

![Web kancası eylem düzeni](./media/logic-apps-create-api-app/custom-api-webhook-action-pattern.png)

> [!NOTE]
> Şu anda hello mantığı Uygulama Tasarımcısı bulan Web kancası uç noktaları Swagger yoluyla desteklemiyor. Tooadd olması için bu deseni, böylece bir [ **Web kancası** eylem](../connectors/connectors-native-webhook.md) hello URL, üstbilgiler ve isteğinizin gövdesi belirtin. Ayrıca bkz. [iş akışı eylemleri ve Tetikleyicileri](logic-apps-workflow-actions-triggers.md#api-connection-webhook-action). toopass hello geri çağırma URL'si olarak kullanabileceğiniz hello `@listCallbackUrl()` gerektiği herhangi bir hello önceki alanları iş akışı işlevi.

> [!TIP]
> Bir örnek Web kancası düzeni için bu gözden [github Web kancası tetikleyici örnek](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs).

<a name="triggers"></a>

## <a name="trigger-patterns"></a>Tetikleyici desenleri

Özel API'nizi olarak davranıp bir [ *tetikleyici* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) , başlayan bir mantıksal uygulama yeni veri ya da bir olay bir belirtilen koşulu karşılıyorsa. Bu tetikleyici ya da düzenli olarak denetleyin veya bekleyip, yeni veri ya da hizmet uç noktada olayları dinler. Yeni veri ya da bir olay karşılıyorsa belirtilen koşulu Merhaba, hello tetikleyici başlatılır ve toothat tetikleyici dinleme hello mantıksal uygulama başlatır. toostart logic apps bu şekilde, API'nizi izleyin hello [ *yoklama tetikleyici* ](#polling-triggers) veya hello [ *Web kancası tetikleyici* ](#webhook-triggers) düzeni. Bu düzenleri için benzer tootheir ortaklarınıza olan [Eylemler yoklama](#async-pattern) ve [Web kancası eylemleri](#webhook-actions). Ayrıca, daha fazla bilgi edinmek [için Tetikleyicileri kullanım ölçümü](logic-apps-pricing.md).

<a name="polling-triggers"></a>

### <a name="check-for-new-data-or-events-regularly-with-hello-polling-trigger-pattern"></a>Yeni veri ya da düzenli olarak tetikleyici düzeni yoklama hello olaylarla denetle

A *yoklama tetikleyici* çok hello gibi davranan [eylem yoklama](#async-pattern) daha önce bu konuda açıklanan. Hello Logic Apps altyapısı düzenli aralıklarla çağırır ve yeni veri ya da olaylar hello tetikleyici uç noktasının denetler. Yeni veri ya da belirtilen koşulu karşılıyor bir olay Hello altyapısı bulursa, hello tetikleyici ateşlenir. Ardından, hello altyapısı hello verileri girdi olarak işler bir mantık uygulama örneği oluşturur. 

![Tetikleyici düzeni yoklama](./media/logic-apps-create-api-app/custom-api-polling-trigger-pattern.png)

> [!NOTE]
> Her yoklama isteği bile hiçbir mantığı uygulama örneği oluşturulduğunda bir eylem yürütme olarak sayar. tooprevent işleme birden çok kez aynı veri Merhaba, zaten okuyun ve toohello mantıksal uygulama geçirilen verileri yedekleyin, tetikleyici temizlemeniz gerekir.

Merhaba API'nin açısından açıklandığı bir yoklama tetikleyici için belirli adımlar şunlardır:

| Yeni verileri veya olay bulunur?  | API yanıtını | 
| ------------------------- | ------------ |
| Bulunamadı | Bir HTTP dönmek `200 OK` hello yanıt Yükü (giriş sonraki adımınız) durumuyla. <br/>Bu yanıt, bir mantıksal uygulama örneği oluşturur ve hello iş akışı başlatır. |
| Bulunamadı | Bir HTTP dönmek `202 ACCEPTED` durumundaki bir `location` başlığı ve bir `retry-after` üstbilgi. <br/>Tetikleyiciler için hello `location` üstbilgi de içermelidir bir `triggerState` , genellikle bir "zaman damgası." sorgu parametresi Bu tanımlayıcı tootrack hello mantığı hello son zamanı API'nizi kullanabilirsiniz uygulama tetiklendi. |

Örneğin, tooperiodically denetleme hizmetiniz yeni dosyalar için bu davranışların sahip bir yoklama tetikleyici oluşturabilir:

| İstek içerir `triggerState`? | API yanıtını |
| -------------------------------- | -------------|
| Hayır | Bir HTTP dönmek `202 ACCEPTED` durum artı bir `location` üstbilgiyle `triggerState` toohello geçerli saati ayarlayın ve hello `retry-after` aralığı too15 saniye. |
| Evet | Hizmetinizin hello sonra eklenen dosyaların denetleyin `DateTime` için `triggerState`. |

| Bulunan dosyaların sayısı | API yanıtını |
| --------------------- | -------------|
| Tek dosya | Bir HTTP dönmek `200 OK` durumunu ve hello içerik yükü, güncelleştirme `triggerState` toohello `DateTime` hello dosya iade ve ayarlamak için `retry-after` aralığı too15 saniye. |
| Birden çok dosya | Bir dosyayı bir saat ve bir HTTP dönmek `200 OK` durumu, güncelleştirme `triggerState`ve kümesi hello `retry-after` aralığı too0 saniye. </br>Bu adımlar, daha fazla veri ve o hello altyapısı hemen hello hello hello URL'den istek verilerini bildiren hello altyapısı sağlayacaktır. `location` üstbilgi. |
| Dosya yok | Bir HTTP dönmek `202 ACCEPTED` durumunu, değişiklik yapmayın `triggerState`ve kümesi hello `retry-after` aralığı too15 saniye. |

> [!TIP]
> Bir örnek için bu gözden tetikleyici düzeni yoklama [yoklama tetikleyici denetleyicisi örnek github'da](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/PollTriggerController.cs).

<a name="webhook-triggers"></a>

### <a name="wait-and-listen-for-new-data-or-events-with-hello-webhook-trigger-pattern"></a>Bekleyin ve yeni veri ya da hello Web kancası tetikleyici düzendeki olayları dinler

Bir Web kancası Tetik bir *itme tetikleyici* bekler ve yeni veri ya da hizmet uç noktada olayları dinler. Yeni veri ya da bir olay karşılıyorsa hello koşul, hello tetikleyici ateşlenir belirtilen ve hello verileri girdi olarak işler bir mantıksal uygulama örneği oluşturur.
Web kancası Tetikleyicileri hello benzer hareket [Web kancası eylemleri](#webhook-actions) daha önce bu konuda açıklanan ve ile ayarlamak `subscribe` ve `unsubscribe` uç noktaları. 

* `subscribe`uç nokta: ekleme ve mantıksal uygulamanızı bir Web kancası tetikleyici kaydettiğinizde hello Logic Apps çağrıları hello altyapısı `subscribe` uç noktası. Bu adım, API depolayan bir geri çağırma URL'si hello mantığı uygulama toocreate neden olur. Yeni veri veya hello belirtilen koşulu karşılayan bir olay olduğunda API'nizi birlikte bir HTTP POST toohello URL geri çağırır. Merhaba içerik yükü ve üstbilgileri giriş toohello mantıksal uygulama geçirin.

* `unsubscribe`uç nokta: hello Web kancası tetikleyici veya tüm mantıksal uygulama silinirse, hello Logic Apps çağrıları hello altyapısı `unsubscribe` uç noktası. API'nizi hello geri çağırma URL'si kaydı ve gerektiği gibi tüm işlemleri durdur.

![Web kancası tetikleyici düzeni](./media/logic-apps-create-api-app/custom-api-webhook-trigger-pattern.png)

> [!NOTE]
> Şu anda hello mantığı Uygulama Tasarımcısı bulan Web kancası uç noktaları Swagger yoluyla desteklemiyor. Tooadd olması için bu deseni, böylece bir [ **Web kancası** tetikleyici](../connectors/connectors-native-webhook.md) hello URL, üstbilgiler ve isteğinizin gövdesi belirtin. Ayrıca bkz. [HTTPWebhook tetikleyici](logic-apps-workflow-actions-triggers.md#httpwebhook-trigger). toopass hello geri çağırma URL'si olarak kullanabileceğiniz hello `@listCallbackUrl()` gerektiği herhangi bir hello önceki alanları iş akışı işlevi.
>
> tooprevent işleme birden çok kez aynı veri Merhaba, zaten okuyun ve toohello mantıksal uygulama geçirilen verileri yedekleyin, tetikleyici temizlemeniz gerekir.

> [!TIP]
> Bir örnek Web kancası düzeni için bu gözden [github Web kancası tetikleyici denetleyicisi örnek](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs).

## <a name="deploy-call-and-secure-custom-apis"></a>Dağıtımı, arama ve özel API'leri güvenli

Güvenli bir şekilde çağırması özel Apı'lerinizi oluşturduktan sonra API dağıtımı için ayarlayın. Nasıl çok öğrenin[dağıtmak, arama ve logic apps için özel API'leri güvenli](./logic-apps-custom-hosted-api.md).

## <a name="publish-custom-apis-tooazure"></a>Özel API'leri tooAzure yayımlama

toomake genel kullanıma Azure, özel Apı'lerinizi gönderme adaylar toohello [Azure Microsoft Sertifikalı program](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/).

## <a name="get-help"></a>Yardım alın

Özel API'leri ile ilgili Yardım başvurun [ customapishelp@microsoft.com ](mailto:customapishelp@microsoft.com).

tooask sorular, soruları ve diğer Azure mantıksal uygulamaları kullanıcıların gittiğini, bkz: ziyaret hello [Azure Logic Apps Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp Logic Apps ve bağlayıcılar geliştirmek, oy veya hello fikir gönderme [Logic Apps kullanıcı geri bildirim sitesi](http://aka.ms/logicapps-wish). 

## <a name="next-steps"></a>Sonraki adımlar

* [Eylemler ve Tetikleyiciler için kullanım ölçümü](logic-apps-pricing.md)
* [İçerik türlerini işleme](./logic-apps-content-type.md)
* [Hataları ve özel durumları işleme](./logic-apps-exception-handling.md)
* [Tooyour logic apps güvenli erişim](./logic-apps-securing-a-logic-app.md)
* [Logic apps HTTP uç noktaları ile iç içe veya, tetikleyici çağırın](./logic-apps-http-endpoint.md)