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
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="73c92-103">Arama trafiği analytics nedir</span><span class="sxs-lookup"><span data-stu-id="73c92-103">What is search traffic analytics</span></span>
<span data-ttu-id="73c92-104">Arama trafiği analytics arama hizmetiniz için bir geri döngü uygulamak için bir desen ' dir.</span><span class="sxs-lookup"><span data-stu-id="73c92-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="73c92-105">Bu desen hello gerekli veri ve toocollect Application Insights, izleme için bir endüstri lideri kullanarak birden çok platformda hizmetleri nasıl açıklar.</span><span class="sxs-lookup"><span data-stu-id="73c92-105">This pattern describes hello necessary data and how toocollect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="73c92-106">Arama trafiği analytics, arama hizmetinizi görünürlük elde etmek ve kullanıcılarınızın ve davranışları hakkında Öngörüler elde edebilirsiniz sağlar.</span><span class="sxs-lookup"><span data-stu-id="73c92-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="73c92-107">Hangi kullanıcıların seçin hakkındaki verileri sağlayarak, daha fazla arama deneyimi ve hello sonuçları ne beklenen olduğunda kapalı tooback geliştirmek olası toomake kararları olur.</span><span class="sxs-lookup"><span data-stu-id="73c92-107">By having data about what your users choose, it's possible toomake decisions that further improve your search experience, and tooback off when hello results are not what expected.</span></span>

<span data-ttu-id="73c92-108">Azure Search'te Azure Application Insights ve Power BI tooprovide ayrıntılı izleme ve izleme tümleşen bir telemetri çözüm sunar.</span><span class="sxs-lookup"><span data-stu-id="73c92-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI tooprovide in-depth monitoring and tracking.</span></span> <span data-ttu-id="73c92-109">Azure Search ile etkileşimi yalnızca API'leri aracılığıyla olduğundan, bu sayfadaki hello yönergeleri izleyerek arama kullanılarak hello geliştiriciler tarafından hello telemetri uygulanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="73c92-109">Because interaction with Azure Search is only through APIs, hello telemetry must be implemented by hello developers using search, following hello instructions in this page.</span></span>

## <a name="identify-hello-relevant-search-data"></a><span data-ttu-id="73c92-110">Merhaba ilgili arama veri tanımlayın</span><span class="sxs-lookup"><span data-stu-id="73c92-110">Identify hello relevant search data</span></span>

<span data-ttu-id="73c92-111">toohave yararlı arama ölçümleri, bazı sinyalleri hello arama uygulaması hello kullanıcılardan gerekli toolog olur.</span><span class="sxs-lookup"><span data-stu-id="73c92-111">toohave useful search metrics, it's necessary toolog some signals from hello users of hello search application.</span></span> <span data-ttu-id="73c92-112">Bu sinyalleri kullanıcılar de ilginizi çekiyor mu ve ilgili tootheir gerektiğini düşünün içerik türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="73c92-112">These signals signify content that users are interested in and that they consider relevant tootheir needs.</span></span>

<span data-ttu-id="73c92-113">Arama trafiği Analytics gereken iki sinyalleri vardır:</span><span class="sxs-lookup"><span data-stu-id="73c92-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="73c92-114">Oluşturulan kullanıcı arama olayları: yalnızca bir kullanıcı tarafından başlatılan arama sorguları ilginç.</span><span class="sxs-lookup"><span data-stu-id="73c92-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="73c92-115">Arama ve kullanılan isteklerinin toopopulate modelleri, ek içerik veya herhangi bir iç bilgi önemli değildir ve eğme ve sonuçlarınızı bias.</span><span class="sxs-lookup"><span data-stu-id="73c92-115">Search requests used toopopulate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="73c92-116">Oluşturulan kullanıcı tıklama olayları: Bu belgede tıklama tarafından size bir arama sorgusundan döndürülen belirli bir sonucun seçilmesi tooa kullanıcı bakın.</span><span class="sxs-lookup"><span data-stu-id="73c92-116">User generated click events: By clicks in this document, we refer tooa user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="73c92-117">Tıklama genellikle bir belge belirli arama sorgusu için ilgili bir sonuç anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="73c92-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="73c92-118">Arama ve tıklatın olayları bir bağıntı kimliği ile bağlayarak, uygulamanız kullanıcıların olası tooanalyze hello davranışlarını olur.</span><span class="sxs-lookup"><span data-stu-id="73c92-118">By linking search and click events with a correlation id, it's possible tooanalyze hello behaviors of users on your application.</span></span> <span data-ttu-id="73c92-119">Bu arama Öngörüler yalnızca arama trafiği günlükleri ile mümkün olmayan tooobtain ' dir.</span><span class="sxs-lookup"><span data-stu-id="73c92-119">These search insights are impossible tooobtain with only search traffic logs.</span></span>

## <a name="how-tooimplement-search-traffic-analytics"></a><span data-ttu-id="73c92-120">Nasıl tooimplement arama trafiği analizi</span><span class="sxs-lookup"><span data-stu-id="73c92-120">How tooimplement search traffic analytics</span></span>

<span data-ttu-id="73c92-121">Hello sinyalleri hello kullanıcı ile etkileşim olarak bölüm hello arama uygulamadan toplanması hello önceki belirtiliyor.</span><span class="sxs-lookup"><span data-stu-id="73c92-121">hello signals mentioned in hello preceding section must be gathered from hello search application as hello user interacts with it.</span></span> <span data-ttu-id="73c92-122">Application Insights bir Genişletilebilir izleme çözümü, esnek izleme seçeneklerini ile birden çok platform için kullanılabilir olur.</span><span class="sxs-lookup"><span data-stu-id="73c92-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="73c92-123">Application Insights kullanımını, Itanium tabanlı sistemler için Azure Search toomake hello analiz verilerinin tarafından daha kolay oluşturulan hello Power BI arama raporlar yararlanmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="73c92-123">Usage of Application Insights lets you take advantage of hello Power BI search reports created by Azure Search toomake hello analysis of data easier.</span></span>

<span data-ttu-id="73c92-124">Merhaba, [portal](https://portal.azure.com) Azure Search hizmetinizin hello arama trafiği Analytics dikey sayfası bu telemetri deseni izleyen bir kopya sayfası içerir.</span><span class="sxs-lookup"><span data-stu-id="73c92-124">In hello [portal](https://portal.azure.com) page for your Azure Search service, hello Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="73c92-125">Ayrıca seçin veya bir Application Insights kaynağı oluşturun ve tek bir yerde hello gerekli verileri görün.</span><span class="sxs-lookup"><span data-stu-id="73c92-125">You can also select or create an Application Insights resource, and see hello necessary data, all in one place.</span></span>

![Arama trafiği Analytics yönergeleri][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="73c92-127">1. Application Insights kaynağını seçin</span><span class="sxs-lookup"><span data-stu-id="73c92-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="73c92-128">Zaten yoksa, oluşturun veya tooselect bir Application Insights kaynağı toouse gerekir.</span><span class="sxs-lookup"><span data-stu-id="73c92-128">You need tooselect an Application Insights resource toouse or create one if you don't have one already.</span></span> <span data-ttu-id="73c92-129">Kullanım toolog hello özel olaylar zaten gerekli bir kaynak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73c92-129">You can use a resource that's already in use toolog hello required custom events.</span></span>

<span data-ttu-id="73c92-130">Yeni bir Application Insights kaynak oluştururken, tüm uygulama türleri bu senaryo için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="73c92-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="73c92-131">Kullanmakta olduğunuz hello platform en uygun hello birini seçin.</span><span class="sxs-lookup"><span data-stu-id="73c92-131">Select hello one that best fits hello platform you are using.</span></span>

<span data-ttu-id="73c92-132">Merhaba telemetri istemci uygulamanız için oluşturmak için hello izleme anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="73c92-132">You need hello instrumentation key for creating hello telemetry client for your application.</span></span> <span data-ttu-id="73c92-133">Merhaba Application Insights portal panosunda alın veya toouse istediğiniz hello örneğini seçerek bunu hello arama trafiği Analytics sayfasından alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73c92-133">You can get it from hello Application Insights portal dashboard, or you can get it from hello Search Traffic Analytics page, selecting hello instance you want toouse.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="73c92-134">2. Uygulamanızın izleme</span><span class="sxs-lookup"><span data-stu-id="73c92-134">2. Instrument your application</span></span>

<span data-ttu-id="73c92-135">Bu aşama, nerede oluşturulacağını hello adım yukarıda hello Application Insights kaynağı kullanarak kendi arama uygulamasını İzleme ' dir.</span><span class="sxs-lookup"><span data-stu-id="73c92-135">This phase is where you instrument your own search application, using hello Application Insights resource your created in hello step above.</span></span> <span data-ttu-id="73c92-136">Toothis işlem dört adım vardır:</span><span class="sxs-lookup"><span data-stu-id="73c92-136">There are four steps toothis process:</span></span>

<span data-ttu-id="73c92-137">**I. Bir telemetri istemcisi oluşturma** bu olayları toohello uygulama Insights kaynağı gönderdiği hello nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="73c92-137">**I. Create a telemetry client** This is hello object that sends events toohello Application Insights Resource.</span></span>

<span data-ttu-id="73c92-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="73c92-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="73c92-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="73c92-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="73c92-140">Diğer diller ve platformlar için tam hello [listesi](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span><span class="sxs-lookup"><span data-stu-id="73c92-140">For other languages and platforms, see hello complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="73c92-141">**II. Bağıntı için bir arama kimliği istek** toocorrelate arama istekleri tıklama ile gerekli toohave bu iki ayrı olayları ilişkili bağıntı kimliği değil.</span><span class="sxs-lookup"><span data-stu-id="73c92-141">**II. Request a Search ID for correlation** toocorrelate search requests with clicks, it's necessary toohave a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="73c92-142">Azure arama sahip bir üstbilgi istediğinde Kimliği Ara sağlar:</span><span class="sxs-lookup"><span data-stu-id="73c92-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="73c92-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="73c92-143">*C#*</span></span>

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="73c92-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="73c92-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="73c92-145">**III. Arama olayları günlüğe kaydedin**</span><span class="sxs-lookup"><span data-stu-id="73c92-145">**III. Log Search events**</span></span>

<span data-ttu-id="73c92-146">Bir arama isteğine bir kullanıcı tarafından verilen her zaman, bir arama olay olarak şema bir Application Insights özel olayı izleyen hello oturum açmanız:</span><span class="sxs-lookup"><span data-stu-id="73c92-146">Every time that a search request is issued by a user, you should log that as a search event with hello following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="73c92-147">**ServiceName**: (dize) arama hizmeti adı **SearchId**: hello arama sorgusunun benzersiz tanıtıcısı (GUID) (Merhaba arama yanıtta gelir) **IndexName**: (dize) arama hizmeti dizini Sorgulanan toobe **QueryTerms**: hello kullanıcı tarafından girilen (dize) arama terimleri **ResultCount**: döndürülmedi belge (int) sayısı (Merhaba arama yanıtta gelir)  **ScoringProfile**: kullanıldığında, profili varsa Puanlama hello adı (dize)</span><span class="sxs-lookup"><span data-stu-id="73c92-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello search query (comes in hello search response) **IndexName**: (string) search service index toobe queried **QueryTerms**: (string) search terms entered by hello user **ResultCount**: (int) number of documents that were returned (comes in hello search response) **ScoringProfile**: (string) name of hello scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="73c92-148">İstek sayısı = true tooyour arama sorgusu $count ekleyerek oluşturulan kullanıcı sorgularının açık.</span><span class="sxs-lookup"><span data-stu-id="73c92-148">Request count on user generated queries by adding $count=true tooyour search query.</span></span> <span data-ttu-id="73c92-149">Daha fazla bilgi [burada](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span><span class="sxs-lookup"><span data-stu-id="73c92-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="73c92-150">Kullanıcılar tarafından oluşturulan tooonly günlük arama sorguları unutmayın.</span><span class="sxs-lookup"><span data-stu-id="73c92-150">Remember tooonly log search queries that are generated by users.</span></span>
>

<span data-ttu-id="73c92-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="73c92-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="73c92-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="73c92-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="73c92-153">**IV. Tıklatın oturum olayları**</span><span class="sxs-lookup"><span data-stu-id="73c92-153">**IV. Log Click events**</span></span>

<span data-ttu-id="73c92-154">Arama analiz amacıyla günlüğe bir sinyal belgesinde, bir kullanıcı, her zaman.</span><span class="sxs-lookup"><span data-stu-id="73c92-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="73c92-155">Application Insights özel olaylar toolog şema aşağıdaki hello ile bu olayları kullanın:</span><span class="sxs-lookup"><span data-stu-id="73c92-155">Use Application Insights custom events toolog these events with hello following schema:</span></span>

<span data-ttu-id="73c92-156">**ServiceName**: (dize) arama hizmeti adı **SearchId**: hello ilgili arama sorgusunun benzersiz tanıtıcısı (GUID) **DocId**: (dize) belge tanımlayıcısı **konumu** : hello arama hello belgede (int) derecesini sonuçları sayfası</span><span class="sxs-lookup"><span data-stu-id="73c92-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello related search query **DocId**: (string) document identifier **Position**: (int) rank of hello document in hello search results page</span></span>

> [!NOTE]
> <span data-ttu-id="73c92-157">Konum, uygulamanızda toohello Kardinal sırası belirtir.</span><span class="sxs-lookup"><span data-stu-id="73c92-157">Position refers toohello cardinal order in your application.</span></span> <span data-ttu-id="73c92-158">Ücretsiz tooset sürece vardır, her zaman hello gibi aynı tooallow karşılaştırması için bu sayı var.</span><span class="sxs-lookup"><span data-stu-id="73c92-158">You are free tooset this number, as long as it's always hello same, tooallow for comparison.</span></span>
>

<span data-ttu-id="73c92-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="73c92-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="73c92-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="73c92-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="73c92-161">3. Power BI Desktop ile çözümleme</span><span class="sxs-lookup"><span data-stu-id="73c92-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="73c92-162">Uygulamanızı işaretlenir ve doğru bağlı tooApplication Öngörüler uygulamanız olduğunu doğruladıktan sonra Power BI desktop için Azure Search tarafından oluşturulan önceden tanımlanmış bir şablonu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73c92-162">After you have instrumented your app and verified your application is correctly connected tooApplication Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="73c92-163">Bu şablon, grafik içerir ve arama performansını ve ilgi daha fazla bilgiye dayalı kararlar tooimprove yardımcı tabloları yapın.</span><span class="sxs-lookup"><span data-stu-id="73c92-163">This template contains charts and tables that help you make more informed decisions tooimprove your search performance and relevance.</span></span>

<span data-ttu-id="73c92-164">tooinstantiate hello Power BI Masaüstü şablonu, üç parça Application Insights hakkında bilgi gerekir.</span><span class="sxs-lookup"><span data-stu-id="73c92-164">tooinstantiate hello Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="73c92-165">Bu veri hello kaynak toouse seçtiğinizde hello arama trafiği Analytics sayfasında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="73c92-165">This data can be found in hello Search Traffic Analytics page, when you select hello resource toouse</span></span>

![Hello arama trafiği Analytics dikey Application Insights Data][2]

<span data-ttu-id="73c92-167">Merhaba Power BI Masaüstü şablonuna dahil ölçümleri:</span><span class="sxs-lookup"><span data-stu-id="73c92-167">Metrics included in hello Power BI desktop template:</span></span>

*   <span data-ttu-id="73c92-168">Oranı (CTRL aracılığıyla) tıklatın: Toplam Arama belirli belge toohello sayısı üzerinde tıklatın kullanıcılar oranı.</span><span class="sxs-lookup"><span data-stu-id="73c92-168">Click through Rate (CTR): ratio of users who click on a specific document toohello number of total searches.</span></span>
*   <span data-ttu-id="73c92-169">Tıklama olmadan arar: koşulları en çok yapılan hiçbir tıklama kaydetmek sorgular</span><span class="sxs-lookup"><span data-stu-id="73c92-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="73c92-170">En belgeleri'ı tıklattınız: 7 gün ve 30 gün içinde olmak üzere son 24 saat tıklattınız hello Kimliğine göre belgelerde en.</span><span class="sxs-lookup"><span data-stu-id="73c92-170">Most clicked documents: most clicked documents by ID in hello last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="73c92-171">Popüler belge terimi çiftleri: hello aynı belge tıklandığında, yol koşulları sıralı tarafından tıklar.</span><span class="sxs-lookup"><span data-stu-id="73c92-171">Popular term-document pairs: terms that result in hello same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="73c92-172">Zaman tooclick: tıklama kümelenmiş zamanından bu yana hello arama sorgusu tarafından</span><span class="sxs-lookup"><span data-stu-id="73c92-172">Time tooclick: clicks bucketed by time since hello search query</span></span>

![Application Insights okuma için Power BI şablonu][3]


## <a name="next-steps"></a><span data-ttu-id="73c92-174">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="73c92-174">Next Steps</span></span>
<span data-ttu-id="73c92-175">Arama uygulama tooget güçlü ve ayrıntılı verilerinizle ilgili arama hizmetinizi izleme.</span><span class="sxs-lookup"><span data-stu-id="73c92-175">Instrument your search application tooget powerful and insightful data about your search service.</span></span>

<span data-ttu-id="73c92-176">Application Insights hakkında daha fazla bilgi bulabilirsiniz [burada](https://go.microsoft.com/fwlink/?linkid=842905).</span><span class="sxs-lookup"><span data-stu-id="73c92-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="73c92-177">Application Insights ziyaret [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/application-insights/) toolearn kendi farklı hizmet katmanları hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="73c92-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) toolearn more about their different service tiers.</span></span>

<span data-ttu-id="73c92-178">Harika raporları oluşturma hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="73c92-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="73c92-179">Bkz: [Power BI Desktop ile çalışmaya başlama](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) Ayrıntılar için</span><span class="sxs-lookup"><span data-stu-id="73c92-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
