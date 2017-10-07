---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Ön belgeleri hello Azure Search REST API'sini sunulan hello anlamlıları (Önizleme) özelliği için."
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 2695139d2b298fa2e7c1814715fdf96729f594ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="synonyms-in-azure-search-preview"></a><span data-ttu-id="a1d19-102">Eş anlamlıları Azure Search'te (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="a1d19-102">Synonyms in Azure Search (preview)</span></span>

<span data-ttu-id="a1d19-103">Arama motorları eş anlamlı örtük olarak bir sorgu hello kapsamını hello terim sağlamak tooactually sahip hello kullanıcı genişletin eşdeğer terimler ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="a1d19-103">Synonyms in search engines associate equivalent terms that implicitly expand hello scope of a query, without hello user having tooactually provide hello term.</span></span> <span data-ttu-id="a1d19-104">Örneğin, belirli hello terimi "köpek" ve "köpek" ve "köpek yavrusu", "köpek", "köpek" veya "köpek yavrusu" içeren tüm belgeleri eş ilişkilendirmelerini hello hello sorgu kapsamında döner.</span><span class="sxs-lookup"><span data-stu-id="a1d19-104">For example, given hello term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within hello scope of hello query.</span></span>

<span data-ttu-id="a1d19-105">Azure Search'te sorgu zamanında eş genişletme yapılır.</span><span class="sxs-lookup"><span data-stu-id="a1d19-105">In Azure Search, synonym expansion is done at query time.</span></span> <span data-ttu-id="a1d19-106">Eş anlamlı eşlemeleri tooa hiç kesintiye tooexisting işlemleri hizmetiyle ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d19-106">You can add synonym maps tooa service with no disruption tooexisting operations.</span></span> <span data-ttu-id="a1d19-107">Ekleyebileceğiniz bir **synonymMaps** toorebuild hello dizin kalmadan özellik tooa alan tanımı.</span><span class="sxs-lookup"><span data-stu-id="a1d19-107">You can add a  **synonymMaps** property tooa field definition without having toorebuild hello index.</span></span> <span data-ttu-id="a1d19-108">Daha fazla bilgi için bkz: [güncelleştirme dizin](https://docs.microsoft.com/rest/api/searchservice/update-index).</span><span class="sxs-lookup"><span data-stu-id="a1d19-108">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

## <a name="feature-availability"></a><span data-ttu-id="a1d19-109">Özellik kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="a1d19-109">Feature availability</span></span>

<span data-ttu-id="a1d19-110">Merhaba anlamlıları özelliği şu anda, Önizleme ve desteklenen yalnızca en son Önizleme api sürümü hello (API sürümü 2016-09-01-Önizleme =).</span><span class="sxs-lookup"><span data-stu-id="a1d19-110">hello synonyms feature is currently in preview and only supported in hello latest preview api-version (api-version=2016-09-01-Preview).</span></span> <span data-ttu-id="a1d19-111">Şu anda Azure portalı desteği yoktur.</span><span class="sxs-lookup"><span data-stu-id="a1d19-111">There is no Azure portal support at this time.</span></span> <span data-ttu-id="a1d19-112">Olası toocombine genel olarak kullanılabilir (GA) ve hello API'leri önizlemede Hello API sürümü hello istek belirtilmediğinden olmasından aynı uygulama.</span><span class="sxs-lookup"><span data-stu-id="a1d19-112">Because hello API version is specified on hello request, it's possible toocombine generally available (GA) and preview APIs in hello same app.</span></span> <span data-ttu-id="a1d19-113">Üretim uygulamalarında kullanma önermiyoruz şekilde ancak API SLA ve Özellikler altında olmayan Önizleme, değişebilir.</span><span class="sxs-lookup"><span data-stu-id="a1d19-113">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span></span>

## <a name="how-toouse-synonyms-in-azure-search"></a><span data-ttu-id="a1d19-114">Azure toouse eş anlamlı nasıl arama</span><span class="sxs-lookup"><span data-stu-id="a1d19-114">How toouse synonyms in Azure search</span></span>

<span data-ttu-id="a1d19-115">Azure Search'te eş anlamlı destek tanımlamak ve tooyour hizmet karşıya eş eşlemeleri temel alır.</span><span class="sxs-lookup"><span data-stu-id="a1d19-115">In Azure Search, synonym support is based on synonym maps that you define and upload tooyour service.</span></span> <span data-ttu-id="a1d19-116">Bu eşlemeleri bağımsız bir kaynak (örneğin, veri kaynaklarını veya dizin) oluşturur ve herhangi bir dizinde arama hizmetinizi aranabilir herhangi bir alana tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a1d19-116">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span></span>

<span data-ttu-id="a1d19-117">Eş anlamlı eşler ve dizinleri bağımsız olarak korunur.</span><span class="sxs-lookup"><span data-stu-id="a1d19-117">Synonym maps and indexes are maintained independently.</span></span> <span data-ttu-id="a1d19-118">Bir eş anlamlı harita tanımlayın ve tooyour hizmet karşıya sonra adlı yeni bir özellik ekleyerek bir alan hello eş özelliğini etkinleştirebilirsiniz **synonymMaps** hello alan tanımında.</span><span class="sxs-lookup"><span data-stu-id="a1d19-118">Once you define a synonym map and upload it tooyour service, you can enable hello synonym feature on a field by adding a new property called **synonymMaps** in hello field definition.</span></span> <span data-ttu-id="a1d19-119">Oluşturma, güncelleştirme ve bir eş anlamlı harita her zaman emin oluşturulamıyor, yani bir bütün belge işlemi siliyor güncelleştirmek veya hello eş harita bölümlerini artımlı olarak silin.</span><span class="sxs-lookup"><span data-stu-id="a1d19-119">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of hello synonym map incrementally.</span></span> <span data-ttu-id="a1d19-120">Tek giriş güncelleştirme, bir yeniden yükleme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a1d19-120">Updating even a single entry requires a reload.</span></span>

<span data-ttu-id="a1d19-121">Eş anlamlıları arama uygulamanıza ekleme iki adımlı bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="a1d19-121">Incorporating synonyms into your search application is a two-step process:</span></span>

1.  <span data-ttu-id="a1d19-122">Bir eş anlamlı harita tooyour arama hizmeti hello aşağıdaki API'leri aracılığıyla ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a1d19-122">Add a synonym map tooyour search service through hello APIs below.</span></span>  

2.  <span data-ttu-id="a1d19-123">Aranabilir alan toouse hello eş eşleştirme hello dizin tanımında yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a1d19-123">Configure a searchable field toouse hello synonym map in hello index definition.</span></span>

### <a name="synonymmaps-resource-apis"></a><span data-ttu-id="a1d19-124">SynonymMaps kaynak API'leri</span><span class="sxs-lookup"><span data-stu-id="a1d19-124">SynonymMaps Resource APIs</span></span>

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a><span data-ttu-id="a1d19-125">Eklemek veya bir eş anlamlı harita hizmetinizin altında güncelleştirmek, kullanarak gönderdiğiniz ya da yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="a1d19-125">Add or update a synonym map under your service, using POST or PUT.</span></span>

<span data-ttu-id="a1d19-126">Eş anlamlı eşlemeleri yüklenir POST veya PUT aracılığıyla toohello hizmet.</span><span class="sxs-lookup"><span data-stu-id="a1d19-126">Synonym maps are uploaded toohello service via POST or PUT.</span></span> <span data-ttu-id="a1d19-127">Her kural hello yeni satır karakteri ('\n') ayrılmış gerekir.</span><span class="sxs-lookup"><span data-stu-id="a1d19-127">Each rule must be delimited by hello new line character ('\n').</span></span> <span data-ttu-id="a1d19-128">Too5, ücretsiz bir hizmettir eş eşlemesinde başına 000 kuralları ve diğer tüm SKU 10.000 kurallarında tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d19-128">You can define up too5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span></span> <span data-ttu-id="a1d19-129">Her kural too20 uzantılarına sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="a1d19-129">Each rule can have up too20 expansions.</span></span>

<span data-ttu-id="a1d19-130">Bu Önizleme'de, eş anlamlı eşlemeleri, aşağıda açıklandığı hello Apache Solr biçiminde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a1d19-130">In this preview, synonym maps must be in hello Apache Solr format which is explained below.</span></span> <span data-ttu-id="a1d19-131">Var olan bir eş anlamlı sözlük farklı bir biçime sahip ve toouse istiyorsanız bunu doğrudan, lütfen bize bildirin üzerinde [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="a1d19-131">If you have an existing synonym dictionary in a different format and want toouse it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="a1d19-132">HTTP POST aşağıdaki örneğine hello olduğu gibi kullanarak yeni bir eş anlamlı eşlemesi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a1d19-132">You can create a new synonym map using HTTP POST, as in hello following example:</span></span>

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

<span data-ttu-id="a1d19-133">Alternatif olarak, PUT kullanın ve URI hello üzerinde hello eş eşleme adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="a1d19-133">Alternatively, you can use PUT and specify hello synonym map name on hello URI.</span></span> <span data-ttu-id="a1d19-134">Merhaba eş eşlemesi yoksa, oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a1d19-134">If hello synonym map does not exist, it will be created.</span></span>

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a><span data-ttu-id="a1d19-135">Apache Solr eş biçimi</span><span class="sxs-lookup"><span data-stu-id="a1d19-135">Apache Solr synonym format</span></span>

<span data-ttu-id="a1d19-136">Merhaba Solr biçimi eşdeğer ve açık eş eşlemeleri destekler.</span><span class="sxs-lookup"><span data-stu-id="a1d19-136">hello Solr format supports equivalent and explicit synonym mappings.</span></span> <span data-ttu-id="a1d19-137">Eşleştirme kurallarına toohello açık kaynak eş filtre Apache Solr, bu belgede açıklanan belirtimi: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span><span class="sxs-lookup"><span data-stu-id="a1d19-137">Mapping rules adhere toohello open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span></span> <span data-ttu-id="a1d19-138">Aşağıda bir örnek için eşdeğer eş anlamlıları kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="a1d19-138">Below is a sample rule for equivalent synonyms.</span></span>
```
              USA, United States, United States of America
```

<span data-ttu-id="a1d19-139">Yukarıdaki Hello kuralı ile bir arama sorgusu "ABD" çok genişletecek "ABD" veya "ABD" veya "Amerika Birleşik Devletleri".</span><span class="sxs-lookup"><span data-stu-id="a1d19-139">With hello rule above, a search query "USA" will expand too"USA" OR "United States" OR "United States of America".</span></span>

<span data-ttu-id="a1d19-140">Açık eşleme bir okla gösterilen "= >".</span><span class="sxs-lookup"><span data-stu-id="a1d19-140">Explicit mapping is denoted by an arrow "=>".</span></span> <span data-ttu-id="a1d19-141">Belirtildiğinde, hello sol tarafındaki eşleşen bir arama sorgu Terime bir dizi "= >" hello alternatifleri hello sağ taraftaki üzerinde ile değiştirilecek.</span><span class="sxs-lookup"><span data-stu-id="a1d19-141">When specified, a term sequence of a search query that matches hello left hand side of "=>" will be replaced with hello alternatives on hello right hand side.</span></span> <span data-ttu-id="a1d19-142">Aşağıdaki Hello kural verildiğinde, arama sorgularını "Washington", "Wash."</span><span class="sxs-lookup"><span data-stu-id="a1d19-142">Given hello rule below, search queries "Washington", "Wash."</span></span> <span data-ttu-id="a1d19-143">veya "WA" tüm yeniden yazılmıştır çok "WA".</span><span class="sxs-lookup"><span data-stu-id="a1d19-143">or "WA" will all be rewritten too"WA".</span></span> <span data-ttu-id="a1d19-144">Belirtilen hello yönde uygular ve hello sorgu "WA" çok yeniden değil yalnızca açık eşleme bu durumda "Washington".</span><span class="sxs-lookup"><span data-stu-id="a1d19-144">Explicit mapping only applies in hello direction specified and does not rewrite hello query "WA" too"Washington" in this case.</span></span>
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a><span data-ttu-id="a1d19-145">Liste eş hizmetinizi altında eşler.</span><span class="sxs-lookup"><span data-stu-id="a1d19-145">List synonym maps under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a><span data-ttu-id="a1d19-146">Bir eş anlamlı harita hizmetinizin altında alın.</span><span class="sxs-lookup"><span data-stu-id="a1d19-146">Get a synonym map under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a><span data-ttu-id="a1d19-147">Eş anlamlıları harita hizmetinizin altında silin.</span><span class="sxs-lookup"><span data-stu-id="a1d19-147">Delete a synonyms map under your service.</span></span>

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a><span data-ttu-id="a1d19-148">Aranabilir alan toouse hello eş eşleştirme hello dizin tanımında yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a1d19-148">Configure a searchable field toouse hello synonym map in hello index definition.</span></span>

<span data-ttu-id="a1d19-149">Yeni bir alan özelliği **synonymMaps** kullanılan toospecify aranabilir bir alan için eş anlamlı harita toouse olabilir.</span><span class="sxs-lookup"><span data-stu-id="a1d19-149">A new field property **synonymMaps** can be used toospecify a synonym map toouse for a searchable field.</span></span> <span data-ttu-id="a1d19-150">Eş anlamlı eşlemeleri hizmet düzeyi kaynaklar ve herhangi bir alan hello hizmeti altında bir dizinin başvurduğu.</span><span class="sxs-lookup"><span data-stu-id="a1d19-150">Synonym maps are service level resources and can be referenced by any field of an index under hello service.</span></span>

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

<span data-ttu-id="a1d19-151">**synonymMaps** hello türü 'Edm.String' veya 'Collection(Edm.String)' aranabilir alanları için belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="a1d19-151">**synonymMaps** can be specified for searchable fields of hello type 'Edm.String' or 'Collection(Edm.String)'.</span></span>

> [!NOTE]
> <span data-ttu-id="a1d19-152">Bu Önizleme'de, yalnızca her alan eşleme bir eş anlamlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a1d19-152">In this preview, you can only have one synonym map per field.</span></span> <span data-ttu-id="a1d19-153">Birden çok eş eşlemesi toouse istiyorsanız, lütfen bize bilmeniz [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="a1d19-153">If you want toouse multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

## <a name="impact-of-synonyms-on-other-search-features"></a><span data-ttu-id="a1d19-154">Eş anlamlıları diğer arama özellikleri üzerinde etkisi</span><span class="sxs-lookup"><span data-stu-id="a1d19-154">Impact of synonyms on other search features</span></span>

<span data-ttu-id="a1d19-155">Merhaba eş anlamlıları özelliği hello özgün sorgu hello OR işleci ile anlamlıları ile yeniden yazar.</span><span class="sxs-lookup"><span data-stu-id="a1d19-155">hello synonyms feature rewrites hello original query with synonyms with hello OR operator.</span></span> <span data-ttu-id="a1d19-156">Bu nedenle, isabet vurgulama ve profilleri Puanlama hello özgün terim ve eş anlamlıları eşdeğer olarak kabul eder.</span><span class="sxs-lookup"><span data-stu-id="a1d19-156">For this reason, hit highlighting and scoring profiles treat hello original term and synonyms as equivalent.</span></span>

<span data-ttu-id="a1d19-157">Eş anlamlı özellik toosearch sorguları uygular ve toofilters veya modelleri geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="a1d19-157">Synonym feature applies toosearch queries and does not apply toofilters or facets.</span></span> <span data-ttu-id="a1d19-158">Benzer şekilde, öneriler yalnızca hello özgün terimini temel alır; Eş anlamlı sözcük eşleşmeleri hello yanıt olarak görünmez.</span><span class="sxs-lookup"><span data-stu-id="a1d19-158">Similarly, suggestions are based only on hello original term; synonym matches do not appear in hello response.</span></span>

<span data-ttu-id="a1d19-159">Eş anlamlı genişletmeleri toowildcard arama terimi geçerli değildir; önek, benzer ve regex koşulları genişletilmiş değil.</span><span class="sxs-lookup"><span data-stu-id="a1d19-159">Synonym expansions do not apply toowildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span></span>

## <a name="tips-for-building-a-synonym-map"></a><span data-ttu-id="a1d19-160">Bir eş anlamlı eşlemesi oluşturmak için ipuçları</span><span class="sxs-lookup"><span data-stu-id="a1d19-160">Tips for building a synonym map</span></span>

- <span data-ttu-id="a1d19-161">Kısa, iyi tasarlanmış eş harita olası eşleşmeler kapsamlı bir liste daha verimli olur.</span><span class="sxs-lookup"><span data-stu-id="a1d19-161">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span></span> <span data-ttu-id="a1d19-162">Aşırı büyük veya karmaşık sözlükler uzun tooparse alın ve toomany anlamlıları hello sorgu genişletir, hello sorgu gecikmesi etkiler.</span><span class="sxs-lookup"><span data-stu-id="a1d19-162">Excessively large or complex dictionaries take longer tooparse and affect hello query latency if hello query expands toomany synonyms.</span></span> <span data-ttu-id="a1d19-163">Hangi koşulları kullanılabilir tahmin yerine hello gerçek koşulları aracılığıyla elde edebilirsiniz bir [arama trafiği analiz raporu](search-traffic-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="a1d19-163">Rather than guess at which terms might be used, you can get hello actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span></span>

- <span data-ttu-id="a1d19-164">Hem Başlangıç hem de doğrulama alıştırma olarak etkinleştirin ve sonra bu raporu tooprecisely hangi koşulları belirlemek yararlı bir eş anlamlı eşleşmeden ve toouse devam olarak eş haritanızı daha iyi sonuç üretme olduğunu doğrulama.</span><span class="sxs-lookup"><span data-stu-id="a1d19-164">As both a preliminary and validation exercise, enable and then use this report tooprecisely determine which terms will benefit from a synonym match, and then continue toouse it as validation that your synonym map is producing a better outcome.</span></span> <span data-ttu-id="a1d19-165">Önceden tanımlanmış hello raporunda, "en yaygın arama sorguları" Merhaba yerleştirir ve "sıfır sonuç arama sorguları" verir hello gerekli bilgileri.</span><span class="sxs-lookup"><span data-stu-id="a1d19-165">In hello predefined report, hello tiles "Most common search queries" and "Zero-result search queries" will give you hello necessary information.</span></span>

- <span data-ttu-id="a1d19-166">Arama uygulamanız için birden çok eş eşlemeleri (çok dilli müşteri tabanı uygulamanız destekliyorsa, örneğin, dil tarafından) oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d19-166">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span></span> <span data-ttu-id="a1d19-167">Şu anda bir alana yalnızca bunlardan birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d19-167">Currently, a field can only use one of them.</span></span> <span data-ttu-id="a1d19-168">Herhangi bir anda bir alanın synonymMaps özelliği güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d19-168">You can update a field's synonymMaps property at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1d19-169">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="a1d19-169">Next Steps</span></span>

- <span data-ttu-id="a1d19-170">Varolan bir dizini geliştirme (üretim olmayan) ortamında varsa, eş anlamlıları hello eklenmesi profilleri Puanlama isabet vurgulama ve öneriler etkisini de dahil olmak üzere hello arama deneyimi nasıl değiştiğini küçük sözlük toosee ile deneyin.</span><span class="sxs-lookup"><span data-stu-id="a1d19-170">If you have an existing index in a development (non-production) environment, experiment with a small dictionary toosee how hello addition of synonyms changes hello search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span></span>

- <span data-ttu-id="a1d19-171">[Arama trafiği analytics etkinleştirmek](search-traffic-analytics.md) ve kullanım hello önceden tanımlanmış Power BI raporu hangi koşulları kullanılır toolearn hello çoğu ve hangi olanları dönüş sıfır belgeleri.</span><span class="sxs-lookup"><span data-stu-id="a1d19-171">[Enable search traffic analytics](search-traffic-analytics.md) and use hello predefined Power BI report toolearn which terms are used hello most, and which ones return zero documents.</span></span> <span data-ttu-id="a1d19-172">Bu ınsights ile sayesinde hello sözlük tooinclude için eş anlamlı sözcükleri dizininizdeki toodocuments çözme üretken sorguları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="a1d19-172">Armed with these insights, revise hello dictionary tooinclude synonyms for unproductive queries that should be resolving toodocuments in your index.</span></span>
