---
title: "Web API'leri & REST API'leri olarak bağlayıcılar - Azure mantıksal uygulamaları oluşturma | Microsoft Docs"
description: "Web API'leri & REST API'leri API'leri, hizmetler veya sistemlerde akışlarında sistem tümleştirmeleri Azure Logic Apps ile çağrısı yapmak için oluşturma"
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
ms.openlocfilehash: 4ae98804aced23c0261c1d58721cb18d8152c6f1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-custom-apis-as-connectors-for-logic-apps"></a>Bağlayıcılar mantıksal uygulamalar için olarak özel API oluşturma

Azure mantıksal uygulamaları sunmasına karşın [100 + yerleşik Bağlayıcılar](../connectors/apis-list.md) mantığı uygulama akışlarında kullanabilirsiniz, API'leri, sistemleri ve bağlayıcıları olarak kullanılabilen olmayan hizmetleri çağrısı isteyebilirsiniz. Eylemler ve logic apps içinde kullanılacak Tetikleyiciler sağlar, kendi özel API'leri oluşturabilirsiniz. Neden logic apps, bağlayıcılar olarak kullanılmak üzere kendi API oluşturmak isteyebilirsiniz diğer nedenler şunlardır:

* Geçerli sisteminizi tümleştirme ve veri tümleştirme iş akışları genişletir.
* Professional ya da kişisel görevleri yönetmek için hizmetinizi kullanmak müşterilere yardımcı olun.
* Reach, bulunabilirliği ve hizmetiniz için kullanım genişletin.

Temel olarak, web takılabilir arabirimleri için REST kullan API'leri bağlayıcılar olan [Swagger meta veri biçimi](http://swagger.io/specification/) belgelerine ve JSON olarak kendi veri değişimi biçimi. Bağlayıcılar HTTP uç noktaları iletişim kuran REST API'leri olduğundan, .NET, Java veya Node.js gibi herhangi bir dil bağlayıcılar oluşturmak için kullanabilirsiniz. Üzerinde Apı'lerinizi barındırabilir [Azure App Service](../app-service/app-service-value-prop-what-is.md), bir platform olarak-sağlayan en iyi, kolay ve en ölçeklenebilir yollarından biri, API barındırmak için sunan hizmet (PaaS). 

Logic apps ile çalışmak özel API'leri için API'nizi sağlayabilir [ *Eylemler* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) mantığı uygulama akışlarında belirli görevleri gerçekleştirebilir. API'nizi de olarak davranıp bir [ *tetikleyici* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) , başlayan bir mantıksal uygulama iş akışı yeni veri ya da bir olay bir belirtilen koşulu karşılıyorsa. Bu konu, Eylemler ve Tetikleyicileri sağlamak için API istediğiniz davranışı temelinde API'nizi oluşturmak için takip edebilirsiniz ortak desenleri açıklar.

> [!TIP] 
> API olarak dağıtabilir ancak [web uygulamaları](../app-service-web/app-service-web-overview.md), Apı'lerinizi olarak dağıtmayı göz önünde bulundurun [API uygulamaları](../app-service-api/app-service-api-apps-why-best-platform.md), hangi yapabilir, işinizi daha kolay yapı, ana bilgisayar ve API'leri bulutta ve şirket içi kullanabilir. Tüm Apı'lerinizi kodda değişiklik--yalnızca kodunuzun bir API uygulamasına dağıtmak yok. Bilgi edinmek için nasıl [ASP.NET ile oluşturulan API uygulamaları derleme](../app-service-api/app-service-api-dotnet-get-started.md), [Java](../app-service-api/app-service-api-java-api-app.md), veya [Node.js](../app-service-api/app-service-api-nodejs-api-app.md). 
>
> Logic apps için yerleşik API uygulaması örnekleri için ziyaret [Azure Logic Apps GitHub deposunu](http://github.com/logicappsio) veya [blog](http://aka.ms/logicappsblog).

## <a name="helpful-tools"></a>Yararlı Araçlar

API de sahip olduğunda özel bir API logic apps ile en iyi şekilde çalışır. bir [Swagger belgesinin](http://swagger.io/specification/) API'nin işlemlerini ve parametrelerini açıklar.
Birçok kitaplıkları, ister [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle), Swagger dosyası sizin için otomatik olarak oluşturur. Swagger dosyası görünen adlar, özellik türleri ve benzeri için ek açıklama eklemek için de kullanabilirsiniz [TRex](https://github.com/nihaue/TRex) böylece Swagger dosyanızın iyi logic apps ile çalışır.

<a name="actions"></a>

## <a name="action-patterns"></a>Eylem desenleri

Logic apps görevleri gerçekleştirmek özel API'nizi sağlamalıdır [ *Eylemler*](./logic-apps-what-are-logic-apps.md#logic-app-concepts). API'nizi her işlem için bir eylem eşler. HTTP istekleri ve HTTP yanıtlarını döndürür kabul eden bir denetleyici buna temel bir eylemdir. Bu nedenle örneğin bir mantıksal uygulama web uygulaması veya API uygulaması için bir HTTP isteği gönderir. Uygulamanız, sonra mantıksal uygulama işleyebilir içeriği ile birlikte bir HTTP yanıtı döndürür.

Standart bir eylemi için bir HTTP istek yöntemi API'nizi yazma ve bu yöntem bir Swagger dosyasında açıklayın. Ardından, API ile doğrudan çağıran bir [HTTP eylemi](../connectors/connectors-native-http.md) veya bir [HTTP + Swagger](../connectors/connectors-native-http-swagger.md) eylem. Varsayılan olarak, içinde yanıt verilmesi gereken [istek zaman aşımı sınırı](./logic-apps-limits-and-config.md). 

![Standart eylem düzeni](./media/logic-apps-create-api-app/standard-action.png)

<a name="pattern-overview"></a>API'nizi uzun çalışan görevler tamamlarken bekleyin bir mantıksal uygulama yapmak için API izleyebilirsiniz [zaman uyumsuz yoklama düzeni](#async-pattern) veya [zaman uyumsuz Web kancası düzeni](#webhook-actions) bu konuda açıklanan. Benzetme her zaman bu desenleri farklı davranışlar görselleştirmenize yardımcı olan bir firincilik gelen özel pasta sıralama işlemi düşünün. Burada, firincilik her 20 dakikada pastayı hazır olup olmadığını denetlemek için arama davranışı yoklama düzeni yansıtır. Web kancası düzeni pastayı hazır olduğunda bunlar çağırabilirsiniz şekilde nerede firincilik, telefon numaranızı ister davranışı yansıtır.

Örnekler için ziyaret [Logic Apps GitHub deposunu](https://github.com/logicappsio). Ayrıca, daha fazla bilgi edinmek [eylemler için kullanım ölçümü](logic-apps-pricing.md).

<a name="async-pattern"></a>

### <a name="perform-long-running-tasks-with-the-polling-action-pattern"></a>Yoklama eylem desen ile uzun süre çalışan görevleri gerçekleştirme

API'nizi, daha uzun süre çalışan görevler gerçekleştirmek için [istek zaman aşımı sınırı](./logic-apps-limits-and-config.md), zaman uyumsuz yoklama desen kullanabilirsiniz. Bu desen ayrı bir iş parçacığı ancak Koru Logic Apps altyapısı için etkin bir bağlantı çalışma, API sahiptir. Bu şekilde, mantıksal uygulama zaman aşımına desteklemez veya çalışma API'nizi tamamlanmadan önce iş akışı bir sonraki adımına devam edin.

Genel düzeni şöyledir:

1. Altyapı, API istek kabul ve çalışmaya başladı bilir emin olun.
2. Altyapı iş durumu için sonraki istek yaptığında, API'nizi görev tamamlandığında bilmeniz altyapısı sağlar.
3. Mantıksal uygulama iş akışı devam edebilmesi için ilgili verileri altyapısına döndür.

<a name="bakery-polling-action"></a>Şimdi yoklama düzeni önceki firincilik benzerliği uygulamak ve firincilik ve sıra özel pasta teslim edilmek üzere çağırırsınız olduğunu düşünün. Pastayı sağlama işlemi sürüyor ve firincilik pastayı üzerinde çalışırken telefonda beklemek istemiyorsanız. Firincilik siparişinizi onaylar ve 20 dakikada pastayı 's durumu için çağrı sahiptir. 20 dakika geçmesi sonra firincilik çağrısı, ancak, pasta işiniz değil ve, başka bir programda 20 dakika çağırmalıdır bunlar size. Bu arka İleri işlemini çağırın ve siparişinizin hazır ve, pasta teslim firincilik size bildirir kadar devam eder. 

Bu yoklama deseni geri sağlandığından eşleyin. Logic Apps altyapısı, pasta müşteri temsil ederken firincilik özel API'nizi temsil eder. Altyapısı API'nizi isteğiyle çağırdığında API'nizi isteği onaylar ve altyapı iş durumunu denetleyebilir, zaman aralığı ile yanıt verir. Altyapı iş yapılır API'nize yanıt verene kadar iş durumunu denetleme devam eder ve iş akışı devam eder, mantıksal uygulama için veri döndürür. 

![Yoklama eylem düzeni](./media/logic-apps-create-api-app/custom-api-async-action-pattern.png)

Takip etmek, API için belirli adımlar şunlardır API'nin açısından açıklanmaktadır:

1. API'nizi iş başlatmak için bir HTTP isteği aldığında, bir HTTP hemen geri `202 ACCEPTED` yanıtıyla `location` daha sonra bu adımda anlatıldığı üstbilgi. Bu yanıt, API isteği alındı, isteği Yükü (veri giriş) kabul bildiğinizden Logic Apps altyapısı sağlar ve şu anda işleniyor. 
   
   `202 ACCEPTED` Yanıt bu üstbilgileri içermelidir:
   
   * *Gerekli*: A `location` burada Logic Apps altyapısı kontrol edebilirsiniz, API'nin iş durumu bir URL mutlak yolu belirtir üstbilgisi

   * *İsteğe bağlı*: A `retry-after` altyapısı denetlemeden önce beklemesi gereken saniye sayısını belirtir üstbilgi `location` iş durumu için URL. 

     Varsayılan olarak, her 20 saniye altyapısı denetler. Farklı bir zaman aralığı belirtmek için dahil `retry-after` üstbilgi ve sonraki yoklama kadar saniye sayısı.

2. Belirtilen süre geçtikten sonra Logic Apps yoklamalar altyapısı `location` işi durumunu denetlemek için URL. API'nizi, bu denetimleri gerçekleştirmek ve bu yanıtları döndürür:
   
   * İş yapıldığında, bir HTTP dönmek `200 OK` yanıt Yükü (bir sonraki adım için giriş) yanı sıra yanıt.

   * İş hala işliyorsa, başka bir HTTP dönmek `202 ACCEPTED` yanıt, özgün yanıt olarak aynı üst bilgileri ile.

API'nizi bu deseni izlediğinde, iş durumunu denetleme devam etmek için mantığı uygulama iş akışı tanımı'ndaki bir şey yapmanız gerekmez. Ne zaman altyapısı alır bir HTTP `202 ACCEPTED` yanıt ve geçerli bir `location` üstbilgi, altyapısı zaman uyumsuz desen dikkate alır ve denetler `location` API'nizi 202 olmayan yanıt dönene kadar üstbilgi.

> [!TIP]
> Örnek zaman uyumsuz desen için bu gözden [zaman uyumsuz denetleyici yanıt örnek github'da](https://github.com/logicappsio/LogicAppsAsyncResponseSample).

<a name="webhook-actions"></a>

### <a name="perform-long-running-tasks-with-the-webhook-action-pattern"></a>Web kancası eylem desen ile uzun süre çalışan görevleri gerçekleştirme

Alternatif olarak, Web kancası desen uzun süre çalışan görevler ve zaman uyumsuz işleme için kullanabilirsiniz. Bu desen duraklatma ve "için bir geri çağırma" bekleyin mantıksal uygulama iş akışı devam etmeden önce işlemeyi tamamlaması, API'sinden sahiptir. Bir olay gerçekleştiğinde, bir URL için bir ileti gönderen bir HTTP POST aramasıdır. 

<a name="bakery-webhook-action"></a>Şimdi Web kancası düzeni önceki firincilik benzerliği uygulamak ve firincilik ve sıra özel pasta teslim edilmek üzere çağırırsınız olduğunu düşünün. Pastayı sağlama işlemi sürüyor ve firincilik pastayı üzerinde çalışırken telefonda beklemek istemiyorsanız. Siparişinizi firincilik onaylar, ancak pastayı yapıldığında bunlar çağırabilirsiniz şekilde bu süre, telefon numaranızı vermediğiniz. Bu süre, firincilik zaman siparişinizi hazır ve, pasta teslim söyler.

Biz bu Web kancası deseni yeniden eşlediğinizde, pasta müşteri Logic Apps altyapısı temsil ederken firincilik özel API'nizi temsil eder. Altyapısı, bir istekle, API çağrılarının ve "geri çağırma" URL'sini içerir.
İş tamamlandığında, API'nizi altyapısı bilgilendirin ve iş akışı devam eder, mantıksal uygulama için verileri döndürmek için URL'yi kullanır. 

Bu model için iki uç nokta denetleyicinizde ayarlayın: `subscribe` ve`unsubscribe`

*  `subscribe`uç nokta: yürütme API eylem iş akışı ulaştığında, Logic Apps çağrıları altyapısı `subscribe` uç noktası. Bu adım, API depolayan bir geri çağırma URL'si oluşturun ve ardından iş tamamlandığında, API'sinden geri çağırma bekleyin mantıksal uygulama neden olur. API'nizi sonra URL bir HTTP POST ile geri çağırır ve döndürülen içeriği ve üstbilgileri mantıksal uygulama giriş olarak geçirir.

* `unsubscribe`uç nokta: çalıştırmak mantıksal uygulama iptal ederseniz, Logic Apps çağrıları altyapısı `unsubscribe` uç noktası. API'nizi geri çağırma URL'si kaydı ve gerektiği gibi tüm işlemleri durdur.

![Web kancası eylem düzeni](./media/logic-apps-create-api-app/custom-api-webhook-action-pattern.png)

> [!NOTE]
> Şu anda Logic App Tasarımcısı bulan Web kancası uç noktaları Swagger yoluyla desteklemiyor. Böylece eklemek zorunda için bu deseni, bir [ **Web kancası** eylem](../connectors/connectors-native-webhook.md) ve URL, üstbilgiler ve isteğinizin gövdesi belirtin. Ayrıca bkz. [iş akışı eylemleri ve Tetikleyicileri](logic-apps-workflow-actions-triggers.md#api-connection-webhook-action). Geri çağırma URL'si geçirmek için kullanabileceğiniz `@listCallbackUrl()` iş akışı işlevinde herhangi bir önceki alanı gerekli.

> [!TIP]
> Bir örnek Web kancası düzeni için bu gözden [github Web kancası tetikleyici örnek](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs).

<a name="triggers"></a>

## <a name="trigger-patterns"></a>Tetikleyici desenleri

Özel API'nizi olarak davranıp bir [ *tetikleyici* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) , başlayan bir mantıksal uygulama yeni veri ya da bir olay bir belirtilen koşulu karşılıyorsa. Bu tetikleyici ya da düzenli olarak denetleyin veya bekleyip, yeni veri ya da hizmet uç noktada olayları dinler. Yeni veri ya da bir olay belirtilen koşulu karşılıyorsa, tetikleyici başlatılır ve bu tetikleyiciye dinleme mantıksal uygulama başlatır. Logic apps bu şekilde başlatmak için API izleyebilirsiniz [ *yoklama tetikleyici* ](#polling-triggers) veya [ *Web kancası tetikleyici* ](#webhook-triggers) düzeni. Bu düzenleri dekiler için benzer [Eylemler yoklama](#async-pattern) ve [Web kancası eylemleri](#webhook-actions). Ayrıca, daha fazla bilgi edinmek [için Tetikleyicileri kullanım ölçümü](logic-apps-pricing.md).

<a name="polling-triggers"></a>

### <a name="check-for-new-data-or-events-regularly-with-the-polling-trigger-pattern"></a>Yeni verileri veya olay yoklama tetikleyici düzendeki düzenli olarak denetleyin

A *yoklama tetikleyici* benzer davranır [eylem yoklama](#async-pattern) daha önce bu konuda açıklanan. Logic Apps altyapısı düzenli aralıklarla çağırır ve yeni veri ya da olaylar için tetikleyici uç noktaya denetler. Yeni veri ya da belirtilen koşulu karşılıyor bir olay altyapısı bulursa, tetikleyici ateşlenir. Ardından, altyapı verileri girdi olarak işler bir mantık uygulama örneği oluşturur. 

![Tetikleyici düzeni yoklama](./media/logic-apps-create-api-app/custom-api-polling-trigger-pattern.png)

> [!NOTE]
> Her yoklama isteği bile hiçbir mantığı uygulama örneği oluşturulduğunda bir eylem yürütme olarak sayar. Birden çok kez aynı veri işleme önlemek için tetikleyici zaten okuyun ve mantıksal Uygulama'ya geçirilen verileri temizlemeniz gerekir.

API açısından açıklandığı bir yoklama tetikleyici için belirli adımlar şunlardır:

| Yeni verileri veya olay bulunur?  | API yanıtını | 
| ------------------------- | ------------ |
| Bulunamadı | Bir HTTP dönmek `200 OK` yanıt Yükü (giriş sonraki adımınız) durumuyla. <br/>Bu yanıt, bir mantıksal uygulama örneği oluşturur ve iş akışı başlatır. |
| Bulunamadı | Bir HTTP dönmek `202 ACCEPTED` durumundaki bir `location` başlığı ve bir `retry-after` üstbilgi. <br/>Tetikleyici, `location` üstbilgi de içermelidir bir `triggerState` , genellikle bir "zaman damgası." sorgu parametresi API'nizi bu tanımlayıcı, mantıksal uygulama tetiklendi son zamanı izlemek için kullanabilirsiniz. |

Örneğin, düzenli aralıklarla yeni dosyalar hizmetinizin denetlemek için bu davranışların sahip bir yoklama tetikleyici oluşturabilir:

| İstek içerir `triggerState`? | API yanıtını |
| -------------------------------- | -------------|
| Hayır | Bir HTTP dönmek `202 ACCEPTED` durum artı bir `location` üstbilgiyle `triggerState` geçerli saati ayarlamak ve `retry-after` aralığı 15 saniye. |
| Evet | Hizmetinizin sonra eklenen dosyaların denetleyin `DateTime` için `triggerState`. |

| Bulunan dosyaların sayısı | API yanıtını |
| --------------------- | -------------|
| Tek dosya | Bir HTTP dönmek `200 OK` güncelleştirme durumu ve içerik yükü `triggerState` için `DateTime` döndürülen dosyası ve kümesi `retry-after` aralığı 15 saniye. |
| Birden çok dosya | Bir dosyayı bir saat ve bir HTTP dönmek `200 OK` durumu, güncelleştirme `triggerState`ve `retry-after` aralığı 0 saniye. </br>Bu adımlar, daha fazla veri kullanılabilir olduğunu ve altyapı hemen URL'den istek verilerini biliyor altyapısı sağlayacaktır. `location` üstbilgi. |
| Dosya yok | Bir HTTP dönmek `202 ACCEPTED` durumunu, değişiklik yapmayın `triggerState`ve ayarlayın `retry-after` aralığı 15 saniye. |

> [!TIP]
> Bir örnek için bu gözden tetikleyici düzeni yoklama [yoklama tetikleyici denetleyicisi örnek github'da](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/PollTriggerController.cs).

<a name="webhook-triggers"></a>

### <a name="wait-and-listen-for-new-data-or-events-with-the-webhook-trigger-pattern"></a>Bekleyin ve yeni veri ya da Web kancası tetikleyici düzendeki olayları dinler

Bir Web kancası Tetik bir *itme tetikleyici* bekler ve yeni veri ya da hizmet uç noktada olayları dinler. Yeni veri ya da bir olay belirtilen koşulu karşılıyorsa, tetikleyici başlatılır ve ardından verileri girdi olarak işler bir mantıksal uygulama örneği oluşturur.
Web kancası Tetikleyicileri benzer hareket [Web kancası eylemleri](#webhook-actions) daha önce bu konuda açıklanan ve ile ayarlamak `subscribe` ve `unsubscribe` uç noktaları. 

* `subscribe`uç nokta: ekleme ve mantıksal uygulamanızı bir Web kancası tetikleyici kaydettiğinizde Logic Apps çağrıları altyapısı `subscribe` uç noktası. Bu adım, API depolayan bir geri çağırma URL'si oluşturmak mantıksal uygulama neden olur. Yeni veri ya da belirtilen koşulu karşılayan bir olay olduğunda API'nizi geri URL bir HTTP POST ile çağırır. Üst bilgiler ve içerik yükü mantıksal uygulama giriş olarak geçirin.

* `unsubscribe`uç nokta: Web kancası tetikleyici veya tüm mantıksal uygulama silinirse, Logic Apps çağrıları altyapısı `unsubscribe` uç noktası. API'nizi geri çağırma URL'si kaydı ve gerektiği gibi tüm işlemleri durdur.

![Web kancası tetikleyici düzeni](./media/logic-apps-create-api-app/custom-api-webhook-trigger-pattern.png)

> [!NOTE]
> Şu anda Logic App Tasarımcısı bulan Web kancası uç noktaları Swagger yoluyla desteklemiyor. Böylece eklemek zorunda için bu deseni, bir [ **Web kancası** tetikleyici](../connectors/connectors-native-webhook.md) ve URL, üstbilgiler ve isteğinizin gövdesi belirtin. Ayrıca bkz. [HTTPWebhook tetikleyici](logic-apps-workflow-actions-triggers.md#httpwebhook-trigger). Geri çağırma URL'si geçirmek için kullanabileceğiniz `@listCallbackUrl()` iş akışı işlevinde herhangi bir önceki alanı gerekli.
>
> Birden çok kez aynı veri işleme önlemek için tetikleyici zaten okuyun ve mantıksal Uygulama'ya geçirilen verileri temizlemeniz gerekir.

> [!TIP]
> Bir örnek Web kancası düzeni için bu gözden [github Web kancası tetikleyici denetleyicisi örnek](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs).

## <a name="deploy-call-and-secure-custom-apis"></a>Dağıtımı, arama ve özel API'leri güvenli

Güvenli bir şekilde çağırması özel Apı'lerinizi oluşturduktan sonra API dağıtımı için ayarlayın. Bilgi edinmek için nasıl [dağıtmak, arama ve logic apps için özel API'leri güvenli](./logic-apps-custom-hosted-api.md).

## <a name="publish-custom-apis-to-azure"></a>Özel API'leri için Azure yayımlama

Özel Apı'lerinizi Azure'da genel kullanım için kullanılabilir hale getirmek için adaylar gönderme [Azure Microsoft Sertifikalı program](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/).

## <a name="get-help"></a>Yardım alın

Özel API'leri ile ilgili Yardım başvurun [ customapishelp@microsoft.com ](mailto:customapishelp@microsoft.com).

Sorular sormak, soruları yanıtlamak ve diğer Azure Logic Apps kullanıcılarının neler yaptığını görmek için [Azure Logic Apps forumunu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) ziyaret edin.

Logic Apps ve bağlayıcıları geliştirmeye yardımcı olmak için, [Logic Apps kullanıcı geri bildirim sitesinde](http://aka.ms/logicapps-wish) oy kullanın veya fikirlerinizi paylaşın. 

## <a name="next-steps"></a>Sonraki adımlar

* [Eylemler ve Tetikleyiciler için kullanım ölçümü](logic-apps-pricing.md)
* [İçerik türlerini işleme](./logic-apps-content-type.md)
* [Hataları ve özel durumları işleme](./logic-apps-exception-handling.md)
* [Mantıksal uygulamalarınızı güvenli erişim](./logic-apps-securing-a-logic-app.md)
* [Logic apps HTTP uç noktaları ile iç içe veya, tetikleyici çağırın](./logic-apps-http-endpoint.md)