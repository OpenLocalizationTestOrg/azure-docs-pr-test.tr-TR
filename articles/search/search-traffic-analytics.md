---
title: "Azure arama için trafiği analiz aaaSearch | Microsoft Docs"
description: "Azure Search, kullanıcılarınız ve verileriniz hakkında toounlock Öngörüler Microsoft Azure üzerinde barındırılan bulut arama hizmeti için arama trafiği analytics etkinleştirin."
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
ms.assetid: b31d79cf-5924-4522-9276-a1bb5d527b13
ms.service: search
ms.devlang: multiple
ms.workload: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/05/2017
ms.author: betorres
ms.openlocfilehash: 1d16aa63d05c1c3df1bbfbb4f09ac77705ed9d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-search-traffic-analytics"></a>Arama trafiği analytics nedir
Arama trafiği analytics arama hizmetiniz için bir geri döngü uygulamak için bir desen ' dir. Bu desen hello gerekli veri ve toocollect Application Insights, izleme için bir endüstri lideri kullanarak birden çok platformda hizmetleri nasıl açıklar.

Arama trafiği analytics, arama hizmetinizi görünürlük elde etmek ve kullanıcılarınızın ve davranışları hakkında Öngörüler elde edebilirsiniz sağlar. Hangi kullanıcıların seçin hakkındaki verileri sağlayarak, daha fazla arama deneyimi ve hello sonuçları ne beklenen olduğunda kapalı tooback geliştirmek olası toomake kararları olur.

Azure Search'te Azure Application Insights ve Power BI tooprovide ayrıntılı izleme ve izleme tümleşen bir telemetri çözüm sunar. Azure Search ile etkileşimi yalnızca API'leri aracılığıyla olduğundan, bu sayfadaki hello yönergeleri izleyerek arama kullanılarak hello geliştiriciler tarafından hello telemetri uygulanmalıdır.

## <a name="identify-hello-relevant-search-data"></a>Merhaba ilgili arama veri tanımlayın

toohave yararlı arama ölçümleri, bazı sinyalleri hello arama uygulaması hello kullanıcılardan gerekli toolog olur. Bu sinyalleri kullanıcılar de ilginizi çekiyor mu ve ilgili tootheir gerektiğini düşünün içerik türünü belirtir.

Arama trafiği Analytics gereken iki sinyalleri vardır:

1. Oluşturulan kullanıcı arama olayları: yalnızca bir kullanıcı tarafından başlatılan arama sorguları ilginç. Arama ve kullanılan isteklerinin toopopulate modelleri, ek içerik veya herhangi bir iç bilgi önemli değildir ve eğme ve sonuçlarınızı bias.

2. Oluşturulan kullanıcı tıklama olayları: Bu belgede tıklama tarafından size bir arama sorgusundan döndürülen belirli bir sonucun seçilmesi tooa kullanıcı bakın. Tıklama genellikle bir belge belirli arama sorgusu için ilgili bir sonuç anlamına gelir.

Arama ve tıklatın olayları bir bağıntı kimliği ile bağlayarak, uygulamanız kullanıcıların olası tooanalyze hello davranışlarını olur. Bu arama Öngörüler yalnızca arama trafiği günlükleri ile mümkün olmayan tooobtain ' dir.

## <a name="how-tooimplement-search-traffic-analytics"></a>Nasıl tooimplement arama trafiği analizi

Hello sinyalleri hello kullanıcı ile etkileşim olarak bölüm hello arama uygulamadan toplanması hello önceki belirtiliyor. Application Insights bir Genişletilebilir izleme çözümü, esnek izleme seçeneklerini ile birden çok platform için kullanılabilir olur. Application Insights kullanımını, Itanium tabanlı sistemler için Azure Search toomake hello analiz verilerinin tarafından daha kolay oluşturulan hello Power BI arama raporlar yararlanmanızı sağlar.

Merhaba, [portal](https://portal.azure.com) Azure Search hizmetinizin hello arama trafiği Analytics dikey sayfası bu telemetri deseni izleyen bir kopya sayfası içerir. Ayrıca seçin veya bir Application Insights kaynağı oluşturun ve tek bir yerde hello gerekli verileri görün.

![Arama trafiği Analytics yönergeleri][1]

### <a name="1-select-an-application-insights-resource"></a>1. Application Insights kaynağını seçin

Zaten yoksa, oluşturun veya tooselect bir Application Insights kaynağı toouse gerekir. Kullanım toolog hello özel olaylar zaten gerekli bir kaynak kullanabilirsiniz.

Yeni bir Application Insights kaynak oluştururken, tüm uygulama türleri bu senaryo için geçerlidir. Kullanmakta olduğunuz hello platform en uygun hello birini seçin.

Merhaba telemetri istemci uygulamanız için oluşturmak için hello izleme anahtarı gerekir. Merhaba Application Insights portal panosunda alın veya toouse istediğiniz hello örneğini seçerek bunu hello arama trafiği Analytics sayfasından alabilirsiniz.

### <a name="2-instrument-your-application"></a>2. Uygulamanızın izleme

Bu aşama, nerede oluşturulacağını hello adım yukarıda hello Application Insights kaynağı kullanarak kendi arama uygulamasını İzleme ' dir. Toothis işlem dört adım vardır:

**I. Bir telemetri istemcisi oluşturma** bu olayları toohello uygulama Insights kaynağı gönderdiği hello nesnesidir.

*C#*

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

*JavaScript*

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

Diğer diller ve platformlar için tam hello [listesi](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).

**II. Bağıntı için bir arama kimliği istek** toocorrelate arama istekleri tıklama ile gerekli toohave bu iki ayrı olayları ilişkili bağıntı kimliği değil. Azure arama sahip bir üstbilgi istediğinde Kimliği Ara sağlar:

*C#*

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

*JavaScript*

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

**III. Arama olayları günlüğe kaydedin**

Bir arama isteğine bir kullanıcı tarafından verilen her zaman, bir arama olay olarak şema bir Application Insights özel olayı izleyen hello oturum açmanız:

**ServiceName**: (dize) arama hizmeti adı **SearchId**: hello arama sorgusunun benzersiz tanıtıcısı (GUID) (Merhaba arama yanıtta gelir) **IndexName**: (dize) arama hizmeti dizini Sorgulanan toobe **QueryTerms**: hello kullanıcı tarafından girilen (dize) arama terimleri **ResultCount**: döndürülmedi belge (int) sayısı (Merhaba arama yanıtta gelir)  **ScoringProfile**: kullanıldığında, profili varsa Puanlama hello adı (dize)

> [!NOTE]
> İstek sayısı = true tooyour arama sorgusu $count ekleyerek oluşturulan kullanıcı sorgularının açık. Daha fazla bilgi [burada](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)
>

> [!NOTE]
> Kullanıcılar tarafından oluşturulan tooonly günlük arama sorguları unutmayın.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

*JavaScript*

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

**IV. Tıklatın oturum olayları**

Arama analiz amacıyla günlüğe bir sinyal belgesinde, bir kullanıcı, her zaman. Application Insights özel olaylar toolog şema aşağıdaki hello ile bu olayları kullanın:

**ServiceName**: (dize) arama hizmeti adı **SearchId**: hello ilgili arama sorgusunun benzersiz tanıtıcısı (GUID) **DocId**: (dize) belge tanımlayıcısı **konumu** : hello arama hello belgede (int) derecesini sonuçları sayfası

> [!NOTE]
> Konum, uygulamanızda toohello Kardinal sırası belirtir. Ücretsiz tooset sürece vardır, her zaman hello gibi aynı tooallow karşılaştırması için bu sayı var.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

*JavaScript*

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a>3. Power BI Desktop ile çözümleme

Uygulamanızı işaretlenir ve doğru bağlı tooApplication Öngörüler uygulamanız olduğunu doğruladıktan sonra Power BI desktop için Azure Search tarafından oluşturulan önceden tanımlanmış bir şablonu kullanabilirsiniz.
Bu şablon, grafik içerir ve arama performansını ve ilgi daha fazla bilgiye dayalı kararlar tooimprove yardımcı tabloları yapın.

tooinstantiate hello Power BI Masaüstü şablonu, üç parça Application Insights hakkında bilgi gerekir. Bu veri hello kaynak toouse seçtiğinizde hello arama trafiği Analytics sayfasında bulunabilir.

![Hello arama trafiği Analytics dikey Application Insights Data][2]

Merhaba Power BI Masaüstü şablonuna dahil ölçümleri:

*   Oranı (CTRL aracılığıyla) tıklatın: Toplam Arama belirli belge toohello sayısı üzerinde tıklatın kullanıcılar oranı.
*   Tıklama olmadan arar: koşulları en çok yapılan hiçbir tıklama kaydetmek sorgular
*   En belgeleri'ı tıklattınız: 7 gün ve 30 gün içinde olmak üzere son 24 saat tıklattınız hello Kimliğine göre belgelerde en.
*   Popüler belge terimi çiftleri: hello aynı belge tıklandığında, yol koşulları sıralı tarafından tıklar.
*   Zaman tooclick: tıklama kümelenmiş zamanından bu yana hello arama sorgusu tarafından

![Application Insights okuma için Power BI şablonu][3]


## <a name="next-steps"></a>Sonraki Adımlar
Arama uygulama tooget güçlü ve ayrıntılı verilerinizle ilgili arama hizmetinizi izleme.

Application Insights hakkında daha fazla bilgi bulabilirsiniz [burada](https://go.microsoft.com/fwlink/?linkid=842905). Application Insights ziyaret [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/application-insights/) toolearn kendi farklı hizmet katmanları hakkında daha fazla bilgi.

Harika raporları oluşturma hakkında daha fazla bilgi edinin. Bkz: [Power BI Desktop ile çalışmaya başlama](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) Ayrıntılar için

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
