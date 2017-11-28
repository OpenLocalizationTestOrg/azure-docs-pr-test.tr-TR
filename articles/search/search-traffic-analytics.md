---
title: "Azure arama için arama trafiği analizi | Microsoft Docs"
description: "Azure Search, kullanıcılarınız ve verilerinizi hakkında Öngörüler kilidini açmak için Microsoft Azure üzerinde barındırılan bulut arama hizmeti için arama trafiği analytics etkinleştirin."
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
ms.openlocfilehash: 303ca5c820f573dc0b58f1910f258403c3baad2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="37035-103">Arama trafiği analytics nedir</span><span class="sxs-lookup"><span data-stu-id="37035-103">What is search traffic analytics</span></span>
<span data-ttu-id="37035-104">Arama trafiği analytics arama hizmetiniz için bir geri döngü uygulamak için bir desen ' dir.</span><span class="sxs-lookup"><span data-stu-id="37035-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="37035-105">Bu deseni gerekli veri ve Application Insights, birden çok platform hizmetlerinde izleme için bir endüstri lideri kullanarak Topla açıklar.</span><span class="sxs-lookup"><span data-stu-id="37035-105">This pattern describes the necessary data and how to collect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="37035-106">Arama trafiği analytics, arama hizmetinizi görünürlük elde etmek ve kullanıcılarınızın ve davranışları hakkında Öngörüler elde edebilirsiniz sağlar.</span><span class="sxs-lookup"><span data-stu-id="37035-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="37035-107">Hangi kullanıcıların seçin hakkındaki verileri sağlayarak, daha fazla arama deneyiminizi geliştirmeye kararları ve sonuçları ne beklenen olduğunda kapatmak için mümkündür.</span><span class="sxs-lookup"><span data-stu-id="37035-107">By having data about what your users choose, it's possible to make decisions that further improve your search experience, and to back off when the results are not what expected.</span></span>

<span data-ttu-id="37035-108">Azure arama ayrıntılı izleme ve izleme sağlamak için Azure Application Insights ve Power BI'ı tümleştiren bir telemetri çözüm sunar.</span><span class="sxs-lookup"><span data-stu-id="37035-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI to provide in-depth monitoring and tracking.</span></span> <span data-ttu-id="37035-109">Azure Search ile etkileşimi yalnızca API'leri aracılığıyla olduğundan, telemetriyi bu sayfasındaki yönergeleri izleyerek arama kullanan geliştiriciler tarafından uygulanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="37035-109">Because interaction with Azure Search is only through APIs, the telemetry must be implemented by the developers using search, following the instructions in this page.</span></span>

## <a name="identify-the-relevant-search-data"></a><span data-ttu-id="37035-110">İlgili arama verilerini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="37035-110">Identify the relevant search data</span></span>

<span data-ttu-id="37035-111">Yararlı arama ölçümleri sağlamak için arama uygulaması kullanıcılardan bazı sinyalleri oturum gereklidir.</span><span class="sxs-lookup"><span data-stu-id="37035-111">To have useful search metrics, it's necessary to log some signals from the users of the search application.</span></span> <span data-ttu-id="37035-112">Bu sinyalleri kullanıcılar de ilginizi çekiyor mu içerik ve kendi gereksinimlerine göre uygun düşünün türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="37035-112">These signals signify content that users are interested in and that they consider relevant to their needs.</span></span>

<span data-ttu-id="37035-113">Arama trafiği Analytics gereken iki sinyalleri vardır:</span><span class="sxs-lookup"><span data-stu-id="37035-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="37035-114">Oluşturulan kullanıcı arama olayları: yalnızca bir kullanıcı tarafından başlatılan arama sorguları ilginç.</span><span class="sxs-lookup"><span data-stu-id="37035-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="37035-115">Arama istekleri modelleri, ek içerik veya herhangi bir iç bilgi doldurmak için kullanılan önemli değildir ve eğme ve sonuçlarınızı bias.</span><span class="sxs-lookup"><span data-stu-id="37035-115">Search requests used to populate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="37035-116">Oluşturulan kullanıcı tıklama olayları: Bu belgede tıklama tarafından size bir arama sorgusundan döndürülen belirli bir sonucun seçilmesi kullanıcı bakın.</span><span class="sxs-lookup"><span data-stu-id="37035-116">User generated click events: By clicks in this document, we refer to a user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="37035-117">Tıklama genellikle bir belge belirli arama sorgusu için ilgili bir sonuç anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="37035-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="37035-118">Arama ve tıklatın olayları bir bağıntı kimliği ile bağlayarak, uygulamanızın kullanıcı davranışlarını analiz etmek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="37035-118">By linking search and click events with a correlation id, it's possible to analyze the behaviors of users on your application.</span></span> <span data-ttu-id="37035-119">Bu arama Öngörüler yalnızca arama trafiği günlükleri ile elde etmek mümkün.</span><span class="sxs-lookup"><span data-stu-id="37035-119">These search insights are impossible to obtain with only search traffic logs.</span></span>

## <a name="how-to-implement-search-traffic-analytics"></a><span data-ttu-id="37035-120">Arama trafiği analiz gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="37035-120">How to implement search traffic analytics</span></span>

<span data-ttu-id="37035-121">Kullanıcı ile etkileşim gibi önceki bölümde belirtildiği sinyalleri arama uygulamadan toplanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="37035-121">The signals mentioned in the preceding section must be gathered from the search application as the user interacts with it.</span></span> <span data-ttu-id="37035-122">Application Insights bir Genişletilebilir izleme çözümü, esnek izleme seçeneklerini ile birden çok platform için kullanılabilir olur.</span><span class="sxs-lookup"><span data-stu-id="37035-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="37035-123">Application Insights kullanımını veri analizini kolaylaştırmak için Azure Search'tarafından oluşturulan Power BI arama raporlar yararlanmak olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="37035-123">Usage of Application Insights lets you take advantage of the Power BI search reports created by Azure Search to make the analysis of data easier.</span></span>

<span data-ttu-id="37035-124">İçinde [portal](https://portal.azure.com) Azure Search hizmet, arama trafiği Analytics dikey için sayfası bu telemetri deseni izleyen bir kopya sayfası içerir.</span><span class="sxs-lookup"><span data-stu-id="37035-124">In the [portal](https://portal.azure.com) page for your Azure Search service, the Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="37035-125">Ayrıca seçin veya bir Application Insights kaynağı oluşturun ve gerekli verileri tek bir yerde görün.</span><span class="sxs-lookup"><span data-stu-id="37035-125">You can also select or create an Application Insights resource, and see the necessary data, all in one place.</span></span>

![Arama trafiği Analytics yönergeleri][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="37035-127">1. Application Insights kaynağını seçin</span><span class="sxs-lookup"><span data-stu-id="37035-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="37035-128">Kullanın veya zaten yoksa, oluşturmak için Application Insights kaynağını seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="37035-128">You need to select an Application Insights resource to use or create one if you don't have one already.</span></span> <span data-ttu-id="37035-129">Gerekli özel olayları günlüğe kullanımda olduğundan bir kaynak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37035-129">You can use a resource that's already in use to log the required custom events.</span></span>

<span data-ttu-id="37035-130">Yeni bir Application Insights kaynak oluştururken, tüm uygulama türleri bu senaryo için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="37035-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="37035-131">Kullanmakta olduğunuz platform için en uygun olanı seçin.</span><span class="sxs-lookup"><span data-stu-id="37035-131">Select the one that best fits the platform you are using.</span></span>

<span data-ttu-id="37035-132">Uygulamanız için telemetri istemci oluşturmak için izleme anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="37035-132">You need the instrumentation key for creating the telemetry client for your application.</span></span> <span data-ttu-id="37035-133">Application Insights portal panosunda alın veya kullanmak istediğiniz örneği seçildiğinde, arama trafiği Analytics sayfasından alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37035-133">You can get it from the Application Insights portal dashboard, or you can get it from the Search Traffic Analytics page, selecting the instance you want to use.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="37035-134">2. Uygulamanızın izleme</span><span class="sxs-lookup"><span data-stu-id="37035-134">2. Instrument your application</span></span>

<span data-ttu-id="37035-135">Burada Application Insights kaynağı Yukarıdaki adımda, oluşturulan kullanan kendi arama uygulamasını izleme bu aşamasıdır.</span><span class="sxs-lookup"><span data-stu-id="37035-135">This phase is where you instrument your own search application, using the Application Insights resource your created in the step above.</span></span> <span data-ttu-id="37035-136">Bu işlem için dört adım vardır:</span><span class="sxs-lookup"><span data-stu-id="37035-136">There are four steps to this process:</span></span>

<span data-ttu-id="37035-137">**I. Bir telemetri istemcisi oluşturma** bu olayları uygulama Öngörüler kaynağa gönderdiği nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="37035-137">**I. Create a telemetry client** This is the object that sends events to the Application Insights Resource.</span></span>

<span data-ttu-id="37035-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="37035-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="37035-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="37035-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="37035-140">Diğer diller ve platformlar için tam bkz [listesi](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span><span class="sxs-lookup"><span data-stu-id="37035-140">For other languages and platforms, see the complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="37035-141">**II. Bağıntı için bir arama kimliği istek** arama istekleri tıklama ile ilişkilendirmek için bu iki ayrı olayları ilişkili bağıntı kimliği sağlamak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="37035-141">**II. Request a Search ID for correlation** To correlate search requests with clicks, it's necessary to have a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="37035-142">Azure arama sahip bir üstbilgi istediğinde Kimliği Ara sağlar:</span><span class="sxs-lookup"><span data-stu-id="37035-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="37035-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="37035-143">*C#*</span></span>

    // This sample uses the Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="37035-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="37035-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="37035-145">**III. Arama olayları günlüğe kaydedin**</span><span class="sxs-lookup"><span data-stu-id="37035-145">**III. Log Search events**</span></span>

<span data-ttu-id="37035-146">Bir arama isteğine bir kullanıcı tarafından verilen her zaman, olarak arama olay Application Insights özel olay aşağıdaki şema ile oturum açmanız:</span><span class="sxs-lookup"><span data-stu-id="37035-146">Every time that a search request is issued by a user, you should log that as a search event with the following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="37035-147">**ServiceName**: (dize) arama hizmeti adı **SearchId**: arama sorgusunun benzersiz tanıtıcısı (GUID) (arama yanıtta gelir) **IndexName**: olmasını (dize) arama hizmeti dizini Sorgulanan **QueryTerms**: (dize) arama terimleri kullanıcı tarafından girilen **ResultCount**: döndürülmedi belge (int) sayısı (arama yanıtta gelir)  **ScoringProfile**: varsa, kullanılan Puanlama profili adı (dize)</span><span class="sxs-lookup"><span data-stu-id="37035-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of the search query (comes in the search response) **IndexName**: (string) search service index to be queried **QueryTerms**: (string) search terms entered by the user **ResultCount**: (int) number of documents that were returned (comes in the search response) **ScoringProfile**: (string) name of the scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="37035-148">İstek sayısı = true, arama sorgusu $count ekleyerek oluşturulan kullanıcı sorgularının açık.</span><span class="sxs-lookup"><span data-stu-id="37035-148">Request count on user generated queries by adding $count=true to your search query.</span></span> <span data-ttu-id="37035-149">Daha fazla bilgi [burada](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span><span class="sxs-lookup"><span data-stu-id="37035-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="37035-150">Yalnızca kullanıcılar tarafından oluşturulan arama sorguları oturum unutmayın.</span><span class="sxs-lookup"><span data-stu-id="37035-150">Remember to only log search queries that are generated by users.</span></span>
>

<span data-ttu-id="37035-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="37035-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="37035-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="37035-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="37035-153">**IV. Tıklatın oturum olayları**</span><span class="sxs-lookup"><span data-stu-id="37035-153">**IV. Log Click events**</span></span>

<span data-ttu-id="37035-154">Arama analiz amacıyla günlüğe bir sinyal belgesinde, bir kullanıcı, her zaman.</span><span class="sxs-lookup"><span data-stu-id="37035-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="37035-155">Bu olaylar aşağıdaki şema ile oturum için Application Insights özel olaylar kullanın:</span><span class="sxs-lookup"><span data-stu-id="37035-155">Use Application Insights custom events to log these events with the following schema:</span></span>

<span data-ttu-id="37035-156">**ServiceName**: (dize) arama hizmeti adı **SearchId**: ilgili arama sorgusunun benzersiz tanıtıcısı (GUID) **DocId**: (dize) belge tanımlayıcısı **konumu** : (int) derecesini belgenin arama sonuçları sayfası</span><span class="sxs-lookup"><span data-stu-id="37035-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of the related search query **DocId**: (string) document identifier **Position**: (int) rank of the document in the search results page</span></span>

> [!NOTE]
> <span data-ttu-id="37035-157">Konum, uygulamanızın Kardinal sırayla ifade eder.</span><span class="sxs-lookup"><span data-stu-id="37035-157">Position refers to the cardinal order in your application.</span></span> <span data-ttu-id="37035-158">Bu her zaman aynı karşılaştırma için izin vermek için olduğu sürece bu numarayı ayarlayabilirler.</span><span class="sxs-lookup"><span data-stu-id="37035-158">You are free to set this number, as long as it's always the same, to allow for comparison.</span></span>
>

<span data-ttu-id="37035-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="37035-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="37035-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="37035-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="37035-161">3. Power BI Desktop ile çözümleme</span><span class="sxs-lookup"><span data-stu-id="37035-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="37035-162">Uygulamanızı işaretlenir ve uygulamanız için Application Insights doğru bir şekilde bağlandığından doğruladıktan sonra Power BI desktop için Azure Search tarafından oluşturulan önceden tanımlanmış bir şablonu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37035-162">After you have instrumented your app and verified your application is correctly connected to Application Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="37035-163">Bu şablon, grafik içerir ve yardımcı tabloları uygunluğu ve arama performansını artırmak için daha fazla bilgiye dayalı kararlar.</span><span class="sxs-lookup"><span data-stu-id="37035-163">This template contains charts and tables that help you make more informed decisions to improve your search performance and relevance.</span></span>

<span data-ttu-id="37035-164">Power BI Masaüstü şablonu oluşturmak için üç parça Application Insights hakkında bilgi gerekir.</span><span class="sxs-lookup"><span data-stu-id="37035-164">To instantiate the Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="37035-165">Bu veri kullanmak için kaynak seçtiğinizde arama trafiği Analytics sayfasında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="37035-165">This data can be found in the Search Traffic Analytics page, when you select the resource to use</span></span>

![Arama trafiği Analytics dikey Application Insights Data][2]

<span data-ttu-id="37035-167">Power BI Masaüstü şablona dahil ölçümleri:</span><span class="sxs-lookup"><span data-stu-id="37035-167">Metrics included in the Power BI desktop template:</span></span>

*   <span data-ttu-id="37035-168">Oranı (CTRL aracılığıyla) tıklatın: toplam arama sayısı için belirli bir belge tıklayın kullanıcılar oranı.</span><span class="sxs-lookup"><span data-stu-id="37035-168">Click through Rate (CTR): ratio of users who click on a specific document to the number of total searches.</span></span>
*   <span data-ttu-id="37035-169">Tıklama olmadan arar: koşulları en çok yapılan hiçbir tıklama kaydetmek sorgular</span><span class="sxs-lookup"><span data-stu-id="37035-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="37035-170">En belgeleri'ı tıklattınız: Son 24 saat içinde 7 gün ve 30 gün tıklattınız Kimliğine göre belge en.</span><span class="sxs-lookup"><span data-stu-id="37035-170">Most clicked documents: most clicked documents by ID in the last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="37035-171">Popüler belge terimi çiftleri: tıklandığında, belgede neden koşulları tıklama tarafından sıralanan.</span><span class="sxs-lookup"><span data-stu-id="37035-171">Popular term-document pairs: terms that result in the same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="37035-172">Saat'ı tıklatın: tıklama kümelenmiş zamanından bu yana arama sorgusu tarafından</span><span class="sxs-lookup"><span data-stu-id="37035-172">Time to click: clicks bucketed by time since the search query</span></span>

![Application Insights okuma için Power BI şablonu][3]


## <a name="next-steps"></a><span data-ttu-id="37035-174">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="37035-174">Next Steps</span></span>
<span data-ttu-id="37035-175">Arama hizmetinize ilişkin güçlü ve ayrıntılı veri almak için arama uygulamasını izleme.</span><span class="sxs-lookup"><span data-stu-id="37035-175">Instrument your search application to get powerful and insightful data about your search service.</span></span>

<span data-ttu-id="37035-176">Application Insights hakkında daha fazla bilgi bulabilirsiniz [burada](https://go.microsoft.com/fwlink/?linkid=842905).</span><span class="sxs-lookup"><span data-stu-id="37035-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="37035-177">Application Insights ziyaret [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/application-insights/) kendi farklı hizmet katmanları hakkında daha fazla bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="37035-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) to learn more about their different service tiers.</span></span>

<span data-ttu-id="37035-178">Harika raporları oluşturma hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="37035-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="37035-179">Bkz: [Power BI Desktop ile çalışmaya başlama](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) Ayrıntılar için</span><span class="sxs-lookup"><span data-stu-id="37035-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
