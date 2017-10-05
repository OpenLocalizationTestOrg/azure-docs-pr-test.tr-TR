---
title: Tam metin arama motoru (Lucene) mimarisi Azure Search'te | Microsoft Docs
description: "Lucene sorgu işleme ve belge alma kavramları açıklaması olarak Azure arama ile ilgili tam metin araması için."
services: search
manager: jhubbard
author: yahnoosh
documentationcenter: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/06/2017
ms.author: jlembicz
ms.openlocfilehash: 9b7adf78271407963ed1d4b34a7760d707b5fc3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-full-text-search-works-in-azure-search"></a><span data-ttu-id="fda50-103">Azure Search'te nasıl tam metin araması çalışır</span><span class="sxs-lookup"><span data-stu-id="fda50-103">How full text search works in Azure Search</span></span>

<span data-ttu-id="fda50-104">Bu makale, Azure Search'te Lucene tam metin araması nasıl çalıştığını daha derin bir anlayış isteyen geliştiriciler için yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="fda50-104">This article is for developers who need a deeper understanding of how Lucene full text search works in Azure Search.</span></span> <span data-ttu-id="fda50-105">Metin sorguları için sorunsuz bir şekilde beklenen sonuçları Azure Search Çoğu senaryoda teslim eder, ancak bazen "kapalı" şekilde görünen bir sonuç almak.</span><span class="sxs-lookup"><span data-stu-id="fda50-105">For text queries, Azure Search will seamlessly deliver expected results in most scenarios, but occasionally you might get a result that seems "off" somehow.</span></span> <span data-ttu-id="fda50-106">Bu durumda, bir arka plan Lucene sorgu yürütme dört aşamalarında sahip (ayrıştırma, sözcük analiz sorgusu, belge eşleşen, Puanlama), sorgu parametreleri ya da istenen sonuca teslim eder dizini yapılandırmasını belirli değişiklikleri belirlemenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="fda50-106">In these situations, having a background in the four stages of Lucene query execution (query parsing, lexical analysis, document matching, scoring) can help you identify specific changes to query parameters or index configuration that will deliver the desired outcome.</span></span> 

> [!Note] 
> <span data-ttu-id="fda50-107">Azure arama için tam metin araması Lucene kullanır, ancak Lucene tümleştirme geniş kapsamlı değildir.</span><span class="sxs-lookup"><span data-stu-id="fda50-107">Azure Search uses Lucene for full text search, but Lucene integration is not exhaustive.</span></span> <span data-ttu-id="fda50-108">Biz seçmeli olarak kullanıma sunmak ve Azure Search önemli senaryoları etkinleştirmek için Lucene işlevselliğini genişleten.</span><span class="sxs-lookup"><span data-stu-id="fda50-108">We selectively expose and extend Lucene functionality to enable the scenarios important to Azure Search.</span></span> 

## <a name="architecture-overview-and-diagram"></a><span data-ttu-id="fda50-109">Mimarisine genel bakış ve diyagramı</span><span class="sxs-lookup"><span data-stu-id="fda50-109">Architecture overview and diagram</span></span>

<span data-ttu-id="fda50-110">Bir tam metin arama sorgusu işlemeye başlıyor arama terimleri ayıklamak için sorgu metni ayrıştırma ile.</span><span class="sxs-lookup"><span data-stu-id="fda50-110">Processing a full text search query starts with parsing the query text to extract search terms.</span></span> <span data-ttu-id="fda50-111">Arama motoru dizin eşleşen terimleri içeren belgeleri almak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="fda50-111">The search engine uses an index to retrieve documents with matching terms.</span></span> <span data-ttu-id="fda50-112">Tek tek sorgu terimleri bazen ayrıntılarıyla ve ne olası bir eşleşme olarak kabul edilebilir üzerinde daha geniş bir net dönüştürmek için yeni formları içine reconstituted.</span><span class="sxs-lookup"><span data-stu-id="fda50-112">Individual query terms are sometimes broken down and reconstituted into new forms to cast a broader net over what could be considered as a potential match.</span></span> <span data-ttu-id="fda50-113">Bir sonuç kümesi sonra her bir eşleşen belgeyi atanmış bir ilgi puana göre sıralanır.</span><span class="sxs-lookup"><span data-stu-id="fda50-113">A result set is then sorted by a relevance score assigned to each individual matching document.</span></span> <span data-ttu-id="fda50-114">Bu dereceli listenin çağrı yapan uygulamaya döndürülür.</span><span class="sxs-lookup"><span data-stu-id="fda50-114">Those at the top of the ranked list are returned to the calling application.</span></span>

<span data-ttu-id="fda50-115">Sorgu yürütme açıklandı, dört aşamadan oluşur:</span><span class="sxs-lookup"><span data-stu-id="fda50-115">Restated, query execution has four stages:</span></span> 

1. <span data-ttu-id="fda50-116">Sorgu ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="fda50-116">Query parsing</span></span> 
2. <span data-ttu-id="fda50-117">Sözcük çözümleme</span><span class="sxs-lookup"><span data-stu-id="fda50-117">Lexical analysis</span></span> 
3. <span data-ttu-id="fda50-118">Belge alma</span><span class="sxs-lookup"><span data-stu-id="fda50-118">Document retrieval</span></span> 
4. <span data-ttu-id="fda50-119">Puanlama</span><span class="sxs-lookup"><span data-stu-id="fda50-119">Scoring</span></span> 

<span data-ttu-id="fda50-120">Aşağıdaki diyagramda bir arama isteği işlemek için kullanılan bileşenleri göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="fda50-120">The diagram below illustrates the components used to process a search request.</span></span> 

 ![Azure Search'te Lucene sorgu mimarisi diyagramı][1]


| <span data-ttu-id="fda50-122">Başlıca bileşenler</span><span class="sxs-lookup"><span data-stu-id="fda50-122">Key components</span></span> | <span data-ttu-id="fda50-123">İşlev açıklaması</span><span class="sxs-lookup"><span data-stu-id="fda50-123">Functional description</span></span> | 
|----------------|------------------------|
|<span data-ttu-id="fda50-124">**Sorgu ayrıştırıcıları**</span><span class="sxs-lookup"><span data-stu-id="fda50-124">**Query parsers**</span></span> | <span data-ttu-id="fda50-125">Sorgu işleçleri sorgu terimlerinin ayırın ve arama motoru gönderilmek üzere sorgu yapısını (sorgu ağacı) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fda50-125">Separate query terms from query operators and create the query structure (a query tree) to be sent to the search engine.</span></span> |
|<span data-ttu-id="fda50-126">**Çözümleyiciler**</span><span class="sxs-lookup"><span data-stu-id="fda50-126">**Analyzers**</span></span> | <span data-ttu-id="fda50-127">Sözcük analiz sorgu terimlerinin üzerinde gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="fda50-127">Perform lexical analysis on query terms.</span></span> <span data-ttu-id="fda50-128">Bu işlem, dönüştürme, kaldırma veya sorgu koşullarını genişletme içerebilir.</span><span class="sxs-lookup"><span data-stu-id="fda50-128">This process can involve transforming, removing, or expanding of query terms.</span></span> |
|<span data-ttu-id="fda50-129">**Dizin**</span><span class="sxs-lookup"><span data-stu-id="fda50-129">**Index**</span></span> | <span data-ttu-id="fda50-130">Depolamak ve dizinli belgelerden ayıklanan aranabilir koşulları düzenlemek için kullanılan bir verimli veri yapısı.</span><span class="sxs-lookup"><span data-stu-id="fda50-130">An efficient data structure used to store and organize searchable terms extracted from indexed documents.</span></span> |
|<span data-ttu-id="fda50-131">**Arama motoru**</span><span class="sxs-lookup"><span data-stu-id="fda50-131">**Search engine**</span></span> | <span data-ttu-id="fda50-132">Alır ve ters dizin içeriğine göre eşleşen belgeleri puanlar.</span><span class="sxs-lookup"><span data-stu-id="fda50-132">Retrieves and scores matching documents based on the contents of the inverted index.</span></span> |

## <a name="anatomy-of-a-search-request"></a><span data-ttu-id="fda50-133">Bir arama isteğine anatomisi</span><span class="sxs-lookup"><span data-stu-id="fda50-133">Anatomy of a search request</span></span>

<span data-ttu-id="fda50-134">Bir arama isteğine bir sonuç kümesi döndürdü, tam bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="fda50-134">A search request is a complete specification of what should be returned in a result set.</span></span> <span data-ttu-id="fda50-135">Basit haliyle, hiçbir ölçüt içermeyen boş bir sorgu değil.</span><span class="sxs-lookup"><span data-stu-id="fda50-135">In simplest form, it is an empty query with no criteria of any kind.</span></span> <span data-ttu-id="fda50-136">Daha gerçekçi bir örnek, belki de büyük olasılıkla bir filtre ifadesi ve kuralları sıralama ile bazı alanlar için kapsamlı, birkaç sorgu terimlerinin parametrelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="fda50-136">A more realistic example includes parameters, several query terms, perhaps scoped to certain fields, with possibly a filter expression and ordering rules.</span></span>  

<span data-ttu-id="fda50-137">Aşağıdaki örnek Gönder Azure Search kullanmaya arama istektir [REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span><span class="sxs-lookup"><span data-stu-id="fda50-137">The following example is a search request you might send to Azure Search using the [REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span></span>  

~~~~
POST /indexes/hotels/docs/search?api-version=2016-09-01 
{  
    "search": "Spacious, air-condition* +\"Ocean view\"",  
    "searchFields": "description, title",  
    "searchMode": "any",
    "filter": "price ge 60 and price lt 300",  
    "orderby": "geo.distance(location, geography'POINT(-159.476235 22.227659)')", 
    "queryType": "full" 
 } 
~~~~

<span data-ttu-id="fda50-138">Bu istek için arama motoru şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="fda50-138">For this request, the search engine does the following:</span></span>

1. <span data-ttu-id="fda50-139">Fiyat en az 60 ve değerinden 300 olduğu giden belgeleri filtreler.</span><span class="sxs-lookup"><span data-stu-id="fda50-139">Filters out documents where the price is at least $60 and less than $300.</span></span>
2. <span data-ttu-id="fda50-140">Sorguyu yürütür.</span><span class="sxs-lookup"><span data-stu-id="fda50-140">Executes the query.</span></span> <span data-ttu-id="fda50-141">Bu örnekte, arama sorgusu tümcecikleri ve şartları oluşur: `"Spacious, air-condition* +\"Ocean view\""` (kullanıcılar genellikle noktalama girin yoktur, ancak örnekte dahil olmak üzere, verir bize nasıl çözümleyiciler ele açıklamak).</span><span class="sxs-lookup"><span data-stu-id="fda50-141">In this example, the search query consists of phrases and terms: `"Spacious, air-condition* +\"Ocean view\""` (users typically don't enter punctuation, but including it in the example allows us to explain how analyzers handle it).</span></span> <span data-ttu-id="fda50-142">Bu sorgu için arama motoru açıklama tarar ve belirtilen başlık alanları `searchFields` "Okyanusu Görünüm" içeren belgeleri ve ayrıca "spacious" terimini veya önek ile başlayan koşullarınızda "air-condition".</span><span class="sxs-lookup"><span data-stu-id="fda50-142">For this query, the search engine scans the description and title fields specified in `searchFields` for documents that contain "Ocean view", and additionally on the term "spacious", or on terms that start with the prefix "air-condition".</span></span> <span data-ttu-id="fda50-143">`searchMode` Parametresi herhangi terim (varsayılan) veya bir terim olduğu kesinlikle gerekli durumlarda bunların tümünün eşleştirmek için kullanılır (`+`).</span><span class="sxs-lookup"><span data-stu-id="fda50-143">The `searchMode` parameter is used to match on any term (default) or all of them, for cases where a term is not explicitly required (`+`).</span></span>
3. <span data-ttu-id="fda50-144">Yakınlık verilen Coğrafya konuma göre Oteller ayarlayın ve çağıran uygulamada döndürülen sonuç sıralar.</span><span class="sxs-lookup"><span data-stu-id="fda50-144">Orders the resulting set of hotels by proximity to a given geography location, and then returned to the calling application.</span></span> 

<span data-ttu-id="fda50-145">Bu makalede çoğunluğu hakkında işlemesidir *arama sorgusu*: `"Spacious, air-condition* +\"Ocean view\""`.</span><span class="sxs-lookup"><span data-stu-id="fda50-145">The majority of this article is about processing of the *search query*: `"Spacious, air-condition* +\"Ocean view\""`.</span></span> <span data-ttu-id="fda50-146">Filtreleme ve Sıralama kapsamının dışına markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="fda50-146">Filtering and ordering are out of scope.</span></span> <span data-ttu-id="fda50-147">Daha fazla bilgi için bkz: [arama API başvuru belgeleri](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span><span class="sxs-lookup"><span data-stu-id="fda50-147">For more information, see the [Search API reference documentation](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span></span>

<a name="stage1"></a>
## <a name="stage-1-query-parsing"></a><span data-ttu-id="fda50-148">1. Aşama: ayrıştırma sorgu</span><span class="sxs-lookup"><span data-stu-id="fda50-148">Stage 1: Query parsing</span></span> 

<span data-ttu-id="fda50-149">Belirtildiği gibi sorgu dizesi isteğin ilk satır şöyledir:</span><span class="sxs-lookup"><span data-stu-id="fda50-149">As noted, the query string is the first line of the request:</span></span> 

~~~~
 "search": "Spacious, air-condition* +\"Ocean view\"", 
~~~~

<span data-ttu-id="fda50-150">Sorgu ayrıştırıcı işleçleri ayıran (gibi `*` ve `+` örnekte) arama koşulları ve arama sorguyu deconstructs *alt sorgulara* desteklenen bir türde:</span><span class="sxs-lookup"><span data-stu-id="fda50-150">The query parser separates operators (such as `*` and `+` in the example) from search terms, and deconstructs the search query into *subqueries* of a supported type:</span></span> 

+ <span data-ttu-id="fda50-151">*Terim sorgu* (gibi spacious) tek başına koşulları için</span><span class="sxs-lookup"><span data-stu-id="fda50-151">*term query* for standalone terms (like spacious)</span></span>
+ <span data-ttu-id="fda50-152">*Tümcecik sorgusu* tırnak işaretli şartlarının (gibi Okyanusu görünümü)</span><span class="sxs-lookup"><span data-stu-id="fda50-152">*phrase query* for quoted terms (like ocean view)</span></span>
+ <span data-ttu-id="fda50-153">*önek sorgu* önek işleci tarafından izlenen koşulları için `*` (air-condition gibi)</span><span class="sxs-lookup"><span data-stu-id="fda50-153">*prefix query* for terms followed by a prefix operator `*` (like air-condition)</span></span>

<span data-ttu-id="fda50-154">Desteklenen sorgu türlerinin tam listesi için bkz: [Lucene sorgu sytnax](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)</span><span class="sxs-lookup"><span data-stu-id="fda50-154">For a full list of supported query types see [Lucene query sytnax](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)</span></span>

<span data-ttu-id="fda50-155">Bir alt sorgu ile ilişkili işleçleri belirlemek sorgu "olmalıdır" veya "olmalıdır" belge bir eşleşme olarak kabul edilmesi sırayla memnun.</span><span class="sxs-lookup"><span data-stu-id="fda50-155">Operators associated with a subquery determine whether the query "must be" or "should be" satisfied in order for a document to be considered a match.</span></span> <span data-ttu-id="fda50-156">Örneğin, `+"Ocean view"` "" nedeniyle gerekliliktir `+` işleci.</span><span class="sxs-lookup"><span data-stu-id="fda50-156">For example, `+"Ocean view"` is "must" due to the `+` operator.</span></span> 

<span data-ttu-id="fda50-157">Alt sorgular içine sorgu ayrıştırıcı yeniden yapılandırır bir *sorgu ağaç* arama motoru, (sorgu temsil eden bir iç yapısı) geçirir.</span><span class="sxs-lookup"><span data-stu-id="fda50-157">The query parser restructures the subqueries into a *query tree* (an internal structure representing the query) it passes on to the search engine.</span></span> <span data-ttu-id="fda50-158">Sorgu ayrıştırma, ilk aşamada, sorgu ağaç şöyle görünür.</span><span class="sxs-lookup"><span data-stu-id="fda50-158">In the first stage of query parsing, the query tree looks like this.</span></span>  

 ![Boolean sorgu searchmode herhangi][2]

### <a name="supported-parsers-simple-and-full-lucene"></a><span data-ttu-id="fda50-160">Ayrıştırıcıları desteklenen: Basit ve tam Lucene</span><span class="sxs-lookup"><span data-stu-id="fda50-160">Supported parsers: Simple and Full Lucene</span></span> 

 <span data-ttu-id="fda50-161">Azure arama gösteren iki farklı sorgu dili, `simple` (varsayılan) ve `full`.</span><span class="sxs-lookup"><span data-stu-id="fda50-161">Azure Search exposes two different query languages, `simple` (default) and `full`.</span></span> <span data-ttu-id="fda50-162">Ayarlayarak `queryType` arama isteğinizi parametresi, size sorgu ayrıştırıcı sorgu dili böylece bunu bilen işleçler ve sözdizimi yorumlama seçin.</span><span class="sxs-lookup"><span data-stu-id="fda50-162">By setting the `queryType` parameter with your search request, you tell the query parser which query language you choose so that it knows how to interpret the operators and syntax.</span></span> <span data-ttu-id="fda50-163">[Basit sorgu dili](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) olan sezgisel ve güçlü, kullanıcı giriş olarak yorumlamak genellikle uygun-istemci tarafı işleme olmadan.</span><span class="sxs-lookup"><span data-stu-id="fda50-163">The [Simple query langauge](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) is intuitive and robust, often suitable to interpret user input as-is without client-side processing.</span></span> <span data-ttu-id="fda50-164">Sorgu işleçleri web arama motorlarından tanıdık destekler.</span><span class="sxs-lookup"><span data-stu-id="fda50-164">It supports query operators familiar from web search engines.</span></span> <span data-ttu-id="fda50-165">[Tam Lucene sorgu dili](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), hangi ayarlayarak alma `queryType=full`, daha fazla işleçler ve joker karakter, benzer gibi sorgu türleri, regex ve alan kapsamlı sorgular için destek ekleyerek varsayılan Basit Sorgu Dili genişletir.</span><span class="sxs-lookup"><span data-stu-id="fda50-165">The [Full Lucene query language](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), which you get by setting `queryType=full`, extends the default Simple query language by adding support for more operators and query types like wildcard, fuzzy, regex, and field-scoped queries.</span></span> <span data-ttu-id="fda50-166">Örneğin, Basit Sorgu söz dizimi gönderilen bir normal ifade bir sorgu dizesi ve bir ifade yorumlanır.</span><span class="sxs-lookup"><span data-stu-id="fda50-166">For example, a regular expression sent in Simple query syntax would be interpreted as a query string and not an expression.</span></span> <span data-ttu-id="fda50-167">Bu makaledeki örnek istek tam Lucene sorgu dilini kullanır.</span><span class="sxs-lookup"><span data-stu-id="fda50-167">The example request in this article uses the Full Lucene query language.</span></span>

### <a name="impact-of-searchmode-on-the-parser"></a><span data-ttu-id="fda50-168">Ayrıştırıcının üzerinde searchMode etkisi</span><span class="sxs-lookup"><span data-stu-id="fda50-168">Impact of searchMode on the parser</span></span> 

<span data-ttu-id="fda50-169">Ayrıştırma etkiler başka bir arama istek parametresi `searchMode` parametresi.</span><span class="sxs-lookup"><span data-stu-id="fda50-169">Another search request parameter that affects parsing is the `searchMode` parameter.</span></span> <span data-ttu-id="fda50-170">Boole sorgular için varsayılan işleç denetler: herhangi bir (varsayılan) veya tüm.</span><span class="sxs-lookup"><span data-stu-id="fda50-170">It controls the default operator for Boolean queries: any (default) or all.</span></span>  

<span data-ttu-id="fda50-171">Zaman `searchMode=any`, varsayılan, spacious alanı bölücüyü ve air-condition veya (`||`), örnek sorgu metnini eşdeğer yapma:</span><span class="sxs-lookup"><span data-stu-id="fda50-171">When `searchMode=any`, which is the default, the space delimiter between spacious and air-condition is OR (`||`), making the sample query text equivalent to:</span></span> 

~~~~
Spacious,||air-condition*+"Ocean view" 
~~~~

<span data-ttu-id="fda50-172">Açık işleçleri gibi `+` içinde `+"Ocean view"`, boolean sorgu yapısında anlaşılır olan (terimi *gerekir* eşleşen).</span><span class="sxs-lookup"><span data-stu-id="fda50-172">Explicit operators, such as `+` in `+"Ocean view"`, are unambiguous in boolean query construction (the term *must* match).</span></span> <span data-ttu-id="fda50-173">Kalan koşulları yorumlama daha az açıktır: spacious ve air-condition.</span><span class="sxs-lookup"><span data-stu-id="fda50-173">Less obvious is how to interpret the remaining terms: spacious and air-condition.</span></span> <span data-ttu-id="fda50-174">Arama motoru Okyanusu görünümünde eşleşen bulmalısınız *ve* spacious *ve* air-condition?</span><span class="sxs-lookup"><span data-stu-id="fda50-174">Should the search engine find matches on ocean view *and* spacious *and* air-condition?</span></span> <span data-ttu-id="fda50-175">Veya Okyanusu görünüm bulmalısınız artı *herhangi birini* kalan koşullarını?</span><span class="sxs-lookup"><span data-stu-id="fda50-175">Or should it find ocean view plus *either one* of the remaining terms?</span></span> 

<span data-ttu-id="fda50-176">Varsayılan olarak (`searchMode=any`), arama motoru daha geniş yorumlama varsayar.</span><span class="sxs-lookup"><span data-stu-id="fda50-176">By default (`searchMode=any`), the search engine assumes the broader interpretation.</span></span> <span data-ttu-id="fda50-177">Her iki alan *gereken* eşleştirilmesi, yansıtma "veya" semantiği.</span><span class="sxs-lookup"><span data-stu-id="fda50-177">Either field *should* be matched, reflecting "or" semantics.</span></span> <span data-ttu-id="fda50-178">İlk sorguyu ağaç daha önce gösterilen ile iki "gereken işlemleri", varsayılan gösterir.</span><span class="sxs-lookup"><span data-stu-id="fda50-178">The initial query tree illustrated previously, with the two "should" operations, shows the default.</span></span>  

<span data-ttu-id="fda50-179">Şimdi ayarlarız varsayalım `searchMode=all`.</span><span class="sxs-lookup"><span data-stu-id="fda50-179">Suppose that we now set `searchMode=all`.</span></span> <span data-ttu-id="fda50-180">Bu durumda, alan bir "ve" işlem olarak yorumlanır.</span><span class="sxs-lookup"><span data-stu-id="fda50-180">In this case, the space is interpreted as an "and" operation.</span></span> <span data-ttu-id="fda50-181">Her kalan koşullarını hem de bir eşleşme olarak nitelemek için belgedeki bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fda50-181">Each of the remaining terms must both be present in the document to qualify as a match.</span></span> <span data-ttu-id="fda50-182">Sonuçta elde edilen örnek sorgu şu şekilde yorumlanacağını:</span><span class="sxs-lookup"><span data-stu-id="fda50-182">The resulting sample query would be interpreted as follows:</span></span> 

~~~~
+Spacious,+air-condition*+"Ocean view"  
~~~~

<span data-ttu-id="fda50-183">Bu sorgu için değiştirilmiş sorgu ağacı eşleşen belgenin tüm üç alt sorgulara kesişimi olduğu aşağıdaki gibi olur:</span><span class="sxs-lookup"><span data-stu-id="fda50-183">A modified query tree for this query would be as follows, where a matching document is the intersection of all three subqueries:</span></span> 

 ![Boole Sorgusu searchmode tüm][3]

> [!Note] 
> <span data-ttu-id="fda50-185">Seçme `searchMode=any` üzerinden `searchMode=all` en iyi kararı temsilcisi sorguları çalıştırarak gelen değil.</span><span class="sxs-lookup"><span data-stu-id="fda50-185">Choosing `searchMode=any` over `searchMode=all` is a decision best arrived at by running representative queries.</span></span> <span data-ttu-id="fda50-186">İşleçler (arama belge depoladığında ortak) dahil olasılığı olan kullanıcıların sonuçları daha sezgisel, bulabileceğiniz `searchMode=all` boolean sorgu yapıları bildirir.</span><span class="sxs-lookup"><span data-stu-id="fda50-186">Users who are likely to include operators (common when searching document stores) might find results more intuitive if `searchMode=all` informs boolean query constructs.</span></span> <span data-ttu-id="fda50-187">Arasında Interplay hakkında daha fazla bilgi için `searchMode` ve işleçleri [Basit Sorgu söz dizimi](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).</span><span class="sxs-lookup"><span data-stu-id="fda50-187">For more about the interplay between `searchMode` and operators, see [Simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).</span></span>

<a name="stage2"></a>
## <a name="stage-2-lexical-analysis"></a><span data-ttu-id="fda50-188">2. Aşama: Sözcük çözümleme</span><span class="sxs-lookup"><span data-stu-id="fda50-188">Stage 2: Lexical analysis</span></span> 

<span data-ttu-id="fda50-189">Sözcük çözümleyiciler işlem *terim sorguları* ve *tümcecik sorguları* sorgu ağaç yapılandırılmış sonra.</span><span class="sxs-lookup"><span data-stu-id="fda50-189">Lexical analyzers process *term queries* and *phrase queries* after the query tree is structured.</span></span> <span data-ttu-id="fda50-190">Bir Çözümleyicisi için ayrıştırıcı tarafından verilen metin girişleri kabul eder, metin ve ardından geri simgeleştirilmiş gönderir koşulları sorgu ağacına yapılması işler.</span><span class="sxs-lookup"><span data-stu-id="fda50-190">An analyzer accepts the text inputs given to it by the parser, processes the text, and then sends back tokenized terms to be incorporated into the query tree.</span></span> 

<span data-ttu-id="fda50-191">En sık kullanılan sözcük analiz biçimidir *dil analiz* hangi dönüşümler sorgulamak için belirli bir dile özel kurallar temel alınarak koşulları:</span><span class="sxs-lookup"><span data-stu-id="fda50-191">The most common form of lexical analysis is *linguistic analysis* which transforms query terms based on rules specific to a given language:</span></span> 

* <span data-ttu-id="fda50-192">Bir sorgu Terime bir sözcük kökü forma azaltma</span><span class="sxs-lookup"><span data-stu-id="fda50-192">Reducing a query term to the root form of a word</span></span> 
* <span data-ttu-id="fda50-193">Gerekli olmayan sözcükler kaldırma ("" gibi bir Durma sözcükleri veya "ve" İngilizce)</span><span class="sxs-lookup"><span data-stu-id="fda50-193">Removing non-essential words (stopwords, such as "the" or "and" in English)</span></span> 
* <span data-ttu-id="fda50-194">Bileşen parçalara bileşik bir sözcük bölme</span><span class="sxs-lookup"><span data-stu-id="fda50-194">Breaking a composite word into component parts</span></span> 
* <span data-ttu-id="fda50-195">Küçük büyük harf word büyük/küçük harfleri</span><span class="sxs-lookup"><span data-stu-id="fda50-195">Lower casing an upper case word</span></span> 

<span data-ttu-id="fda50-196">Bu işlemlerin tümü, kullanıcı tarafından sağlanan metin giriş dizininde depolanan koşulları arasındaki farklar silinecek eğilimlidir.</span><span class="sxs-lookup"><span data-stu-id="fda50-196">All of these operations tend to erase differences between the text input provided by the user and the terms stored in the index.</span></span> <span data-ttu-id="fda50-197">Bu tür işlemler metin işleme ötesine gidin ve dilinin kapsamlı bilgi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fda50-197">Such operations go beyond text processing and require in-depth knowledge of the language itself.</span></span> <span data-ttu-id="fda50-198">Bu dil tanıma katmanı eklemek için uzun bir listesi Azure Search destekler [dil Çözümleyicileri](https://docs.microsoft.com/rest/api/searchservice/language-support) Lucene ve Microsoft tarafından.</span><span class="sxs-lookup"><span data-stu-id="fda50-198">To add this layer of linguistic awareness, Azure Search supports a long list of [language analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support) from both Lucene and Microsoft.</span></span>

> [!Note]
> <span data-ttu-id="fda50-199">Analiz gereksinimleri en az karmaşık üzerinde senaryonuza bağlı olarak için değişebilir.</span><span class="sxs-lookup"><span data-stu-id="fda50-199">Analysis requirements can range from minimal to elaborate depending on your scenario.</span></span> <span data-ttu-id="fda50-200">Önceden tanımlanmış çözümleyiciler seçme birini veya kendi oluşturarak sözcük analiz karmaşıklığını denetleyebilirsiniz [özel Çözümleyicisi](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="fda50-200">You can control complexity of lexical analysis by the selecting one of the predefined analyzers or by creating your own [custom analyzer](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search).</span></span> <span data-ttu-id="fda50-201">Çözümleyiciler aranabilir alanlara kapsamlı ve alan tanımının bir parçası belirtilir.</span><span class="sxs-lookup"><span data-stu-id="fda50-201">Analyzers are scoped to searchable fields and are specified as part of a field definition.</span></span> <span data-ttu-id="fda50-202">Bu, alan başına temelinde sözcük analiz değiştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="fda50-202">This allows you to vary lexical analysis on a per-field basis.</span></span> <span data-ttu-id="fda50-203">Belirtilmezse, *standart* Lucene Çözümleyicisi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fda50-203">Unspecified, the *standard* Lucene analyzer is used.</span></span>

<span data-ttu-id="fda50-204">Örneğimizde, analiz önce ilk sorgu ağacı terimi "bir büyük harf"S"ve sorgu ayrıştırıcı (virgül bir sorgu dili işleci sayılmaz) sorgu Terime bir parçası olarak yorumlar virgül ile" Spacious sahiptir.</span><span class="sxs-lookup"><span data-stu-id="fda50-204">In our example, prior to analysis, the initial query tree has the term "Spacious," with an uppercase "S" and a comma that the query parser interprets as a part of the query term (a comma is not considered a query language operator).</span></span>  

<span data-ttu-id="fda50-205">Varsayılan çözümleyici terimi işlediğinde, bunu "Okyanusu Görünüm" ve "spacious" küçük harf ve virgül karakteri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="fda50-205">When the default analyzer processes the term, it will lowercase "ocean view" and "spacious", and remove the comma character.</span></span> <span data-ttu-id="fda50-206">Değiştirilen sorgu ağacında aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="fda50-206">The modified query tree will look as follows:</span></span> 

 ![Çözümlenen koşullarla Boole Sorgusu][4]

### <a name="testing-analyzer-behaviors"></a><span data-ttu-id="fda50-208">Test Çözümleyicisi davranışları</span><span class="sxs-lookup"><span data-stu-id="fda50-208">Testing analyzer behaviors</span></span> 

<span data-ttu-id="fda50-209">Bir Çözümleyicisi davranışını kullanılarak sınanabilir [analiz API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer).</span><span class="sxs-lookup"><span data-stu-id="fda50-209">The behavior of an analyzer can be tested using the [Analyze API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer).</span></span> <span data-ttu-id="fda50-210">Ne Çözümleyicisi verilen koşulları oluşturacak görmek için analiz etmek istediğiniz metni girin.</span><span class="sxs-lookup"><span data-stu-id="fda50-210">Provide the text you want to analyze to see what terms given analyzer will generate.</span></span> <span data-ttu-id="fda50-211">Örneğin, standart Çözümleyicisi metin "air-condition" işleminin nasıl görmek için aşağıdaki isteği verebilir:</span><span class="sxs-lookup"><span data-stu-id="fda50-211">For example, to see how the standard analyzer would process the text "air-condition", you can issue the following request:</span></span>

~~~~
{ 
    "text": "air-condition",
    "analyzer": "standard"
}
~~~~

<span data-ttu-id="fda50-212">Standart Çözümleyicisi bunları konumlarını (tümcecik eşleştirmek için kullanılır) yanı sıra başlangıç ve bitiş kaydırmalar (isabet vurgulama için kullanılan) gibi özniteliklerle yorumlama aşağıdaki iki belirteçler içine giriş metni keser:</span><span class="sxs-lookup"><span data-stu-id="fda50-212">The standard analyzer breaks the input text into the following two tokens, annotating them with attributes like start and end offsets (used for hit highlighting) as well as their position (used for phrase matching):</span></span>

~~~~
{  
  "tokens": [
    {
      "token": "air",
      "startOffset": 0,
      "endOffset": 3,
      "position": 0
    },
    {
      "token": "condition",
      "startOffset": 4,
      "endOffset": 13,
      "position": 1
    }
  ]
}
~~~~

### <a name="exceptions-to-lexical-analysis"></a><span data-ttu-id="fda50-213">Sözcük analiz için özel durumlar</span><span class="sxs-lookup"><span data-stu-id="fda50-213">Exceptions to lexical analysis</span></span> 

<span data-ttu-id="fda50-214">Sözcük analiz tüm koşullar – bir terim sorgu veya tümcecik sorgusu gerektiren sorgu türleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="fda50-214">Lexical analysis applies only to query types that require complete terms – either a term query or a phrase query.</span></span> <span data-ttu-id="fda50-215">Sorgu türleri – önek sorgu, joker karakter sorgu, regex sorgu – tamamlanmamış koşullarla veya benzer bir sorgu için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="fda50-215">It doesn’t apply to query types with incomplete terms – prefix query, wildcard query, regex query – or to a fuzzy query.</span></span> <span data-ttu-id="fda50-216">Bu terim önek sorguyla dahil olmak üzere türü, sorgu *air-condition\**  Bizim örneğimizde, analiz aşaması atlayarak doğrudan sorgu ağacında için eklenir.</span><span class="sxs-lookup"><span data-stu-id="fda50-216">Those query types, including the prefix query with term *air-condition\** in our example, are added directly to the query tree, bypassing the analysis stage.</span></span> <span data-ttu-id="fda50-217">Bu türlerde sorgu koşullarını gerçekleştirilen yalnızca dönüştürmeyi lowercasing.</span><span class="sxs-lookup"><span data-stu-id="fda50-217">The only transformation performed on query terms of those types is lowercasing.</span></span>

<a name="stage3"></a>
## <a name="stage-3-document-retrieval"></a><span data-ttu-id="fda50-218">3. Aşama: Belge alma</span><span class="sxs-lookup"><span data-stu-id="fda50-218">Stage 3: Document retrieval</span></span> 

<span data-ttu-id="fda50-219">Belge alma dizini terimleriyle eşleşen belgeleri bulmak için ifade eder.</span><span class="sxs-lookup"><span data-stu-id="fda50-219">Document retrieval refers to finding documents with matching terms in the index.</span></span> <span data-ttu-id="fda50-220">Bu aşama örneği arasında en iyi anlaşılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fda50-220">This stage is understood best through an example.</span></span> <span data-ttu-id="fda50-221">Aşağıdaki basit şemasına sahip Oteller diziniyle başlayalım:</span><span class="sxs-lookup"><span data-stu-id="fda50-221">Let's start with a hotels index having the following simple schema:</span></span> 

~~~~
{   
    "name": "hotels",     
    "fields": [     
        { "name": "id", "type": "Edm.String", "key": true, "searchable": false },     
        { "name": "title", "type": "Edm.String", "searchable": true },     
        { "name": "description", "type": "Edm.String", "searchable": true }
    ] 
} 
~~~~

<span data-ttu-id="fda50-222">Daha fazla bu dizini aşağıdaki dört belge içerir varsayın:</span><span class="sxs-lookup"><span data-stu-id="fda50-222">Further assume that this index contains the following four documents:</span></span> 

~~~~
{ 
    "value": [
        {         
            "id": "1",         
            "title": "Hotel Atman",         
            "description": "Spacious rooms, ocean view, walking distance to the beach."   
        },       
        {         
            "id": "2",         
            "title": "Beach Resort",        
            "description": "Located on the north shore of the island of Kauaʻi. Ocean view."     
        },       
        {         
            "id": "3",         
            "title": "Playa Hotel",         
            "description": "Comfortable, air-conditioned rooms with ocean view."
        },       
        {         
            "id": "4",         
            "title": "Ocean Retreat",         
            "description": "Quiet and secluded"
        }    
    ]
}
~~~~

<span data-ttu-id="fda50-223">**Koşulları nasıl dizini**</span><span class="sxs-lookup"><span data-stu-id="fda50-223">**How terms are indexed**</span></span>

<span data-ttu-id="fda50-224">Alma anlamak için dizin oluşturma hakkındaki birkaç temel kavramları biliyorsanız yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="fda50-224">To understand retrieval, it helps to know a few basics about indexing.</span></span> <span data-ttu-id="fda50-225">Depolama Birimi ters, aranabilir her alan için bir tane dizinidir.</span><span class="sxs-lookup"><span data-stu-id="fda50-225">The unit of storage is an inverted index, one for each searchable field.</span></span> <span data-ttu-id="fda50-226">Ters dizin tüm belgelerden tüm koşulları sıralanmış bir listesidir.</span><span class="sxs-lookup"><span data-stu-id="fda50-226">Within an inverted index is a sorted list of all terms from all documents.</span></span> <span data-ttu-id="fda50-227">Bunu, aşağıdaki örnekte güvenli oluştuğu belgelerin listesini her terim eşler.</span><span class="sxs-lookup"><span data-stu-id="fda50-227">Each term maps to the list of documents in which it occurs, as evident in the example below.</span></span>

<span data-ttu-id="fda50-228">Ters dizin koşullarını üretmek için belgeler, sorgu işleme sırasında neler için benzer içerik üzerinde sözcük analiz arama motoru gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="fda50-228">To produce the terms in an inverted index, the search engine performs lexical analysis over the content of documents, similar to what happens during query processing.</span></span> <span data-ttu-id="fda50-229">Metin girişleri noktalama işaretleri ve Çözümleyicisi yapılandırmasına bağlı olarak belirli bir benzeri atılmış bir Çözümleyicisi için alt ortası geçirilir.</span><span class="sxs-lookup"><span data-stu-id="fda50-229">Text inputs are passed to an analyzer, lower-cased, stripped of punctuation, and so forth, depending on the analyzer configuration.</span></span> <span data-ttu-id="fda50-230">Ortak, ancak gerekli değildir, aynı çözümleyiciler arama ve böylece sorgu terimlerinin dizini içinde koşulları gibi daha fazla ara işlemleri dizin oluşturma için kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="fda50-230">It's common, but not required, to use the same analyzers for search and indexing operations so that query terms look more like terms inside the index.</span></span>

> [!Note]
> <span data-ttu-id="fda50-231">Azure arama sağlar, dizin oluşturma için farklı çözümleyiciler belirtin ve arama aracılığıyla ek `indexAnalyzer` ve `searchAnalyzer` alan parametreleri.</span><span class="sxs-lookup"><span data-stu-id="fda50-231">Azure Search lets you specify different analyzers for indexing and search via additional `indexAnalyzer` and `searchAnalyzer` field parameters.</span></span> <span data-ttu-id="fda50-232">Belirtilmezse, Çözümleyicisi kümesiyle `analyzer` özelliği, hem dizin oluşturma ve arama için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fda50-232">If unspecified, the analyzer set with the `analyzer` property is used for both indexing and searching.</span></span>  

<span data-ttu-id="fda50-233">**Örnek belgeler için ters dizin**</span><span class="sxs-lookup"><span data-stu-id="fda50-233">**Inverted index for example documents**</span></span>

<span data-ttu-id="fda50-234">Bizim örneğimizde için için döndürme **başlık** alanı, ters dizini şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="fda50-234">Returning to our example, for the **title** field, the inverted index looks like this:</span></span>

| <span data-ttu-id="fda50-235">Sözleşme Dönemi</span><span class="sxs-lookup"><span data-stu-id="fda50-235">Term</span></span> | <span data-ttu-id="fda50-236">Belge listesi</span><span class="sxs-lookup"><span data-stu-id="fda50-236">Document list</span></span> |
|------|---------------|
| <span data-ttu-id="fda50-237">atman</span><span class="sxs-lookup"><span data-stu-id="fda50-237">atman</span></span> | <span data-ttu-id="fda50-238">1</span><span class="sxs-lookup"><span data-stu-id="fda50-238">1</span></span> |
| <span data-ttu-id="fda50-239">Plaj</span><span class="sxs-lookup"><span data-stu-id="fda50-239">beach</span></span> | <span data-ttu-id="fda50-240">2</span><span class="sxs-lookup"><span data-stu-id="fda50-240">2</span></span> |
| <span data-ttu-id="fda50-241">Otel</span><span class="sxs-lookup"><span data-stu-id="fda50-241">hotel</span></span> | <span data-ttu-id="fda50-242">1, 3</span><span class="sxs-lookup"><span data-stu-id="fda50-242">1, 3</span></span> |
| <span data-ttu-id="fda50-243">Okyanusu</span><span class="sxs-lookup"><span data-stu-id="fda50-243">ocean</span></span> | <span data-ttu-id="fda50-244">4</span><span class="sxs-lookup"><span data-stu-id="fda50-244">4</span></span>  |
| <span data-ttu-id="fda50-245">playa</span><span class="sxs-lookup"><span data-stu-id="fda50-245">playa</span></span> | <span data-ttu-id="fda50-246">3</span><span class="sxs-lookup"><span data-stu-id="fda50-246">3</span></span> |
| <span data-ttu-id="fda50-247">çare</span><span class="sxs-lookup"><span data-stu-id="fda50-247">resort</span></span> | <span data-ttu-id="fda50-248">3</span><span class="sxs-lookup"><span data-stu-id="fda50-248">3</span></span> |
| <span data-ttu-id="fda50-249">Retreat</span><span class="sxs-lookup"><span data-stu-id="fda50-249">retreat</span></span> | <span data-ttu-id="fda50-250">4</span><span class="sxs-lookup"><span data-stu-id="fda50-250">4</span></span> |

<span data-ttu-id="fda50-251">Başlık alanında, yalnızca *otel* iki belgelerde görüntülenir: 1, 3.</span><span class="sxs-lookup"><span data-stu-id="fda50-251">In the title field, only *hotel* shows up in two documents: 1, 3.</span></span>

<span data-ttu-id="fda50-252">İçin **açıklama** alan, dizinde aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="fda50-252">For the **description** field, the index is as follows:</span></span>

| <span data-ttu-id="fda50-253">Sözleşme Dönemi</span><span class="sxs-lookup"><span data-stu-id="fda50-253">Term</span></span> | <span data-ttu-id="fda50-254">Belge listesi</span><span class="sxs-lookup"><span data-stu-id="fda50-254">Document list</span></span> |
|------|---------------|
| <span data-ttu-id="fda50-255">Hava</span><span class="sxs-lookup"><span data-stu-id="fda50-255">air</span></span> | <span data-ttu-id="fda50-256">3</span><span class="sxs-lookup"><span data-stu-id="fda50-256">3</span></span>
| <span data-ttu-id="fda50-257">ve</span><span class="sxs-lookup"><span data-stu-id="fda50-257">and</span></span> | <span data-ttu-id="fda50-258">4</span><span class="sxs-lookup"><span data-stu-id="fda50-258">4</span></span>
| <span data-ttu-id="fda50-259">Plaj</span><span class="sxs-lookup"><span data-stu-id="fda50-259">beach</span></span> | <span data-ttu-id="fda50-260">1</span><span class="sxs-lookup"><span data-stu-id="fda50-260">1</span></span>
| <span data-ttu-id="fda50-261">söylediğinizde</span><span class="sxs-lookup"><span data-stu-id="fda50-261">conditioned</span></span> | <span data-ttu-id="fda50-262">3</span><span class="sxs-lookup"><span data-stu-id="fda50-262">3</span></span>
| <span data-ttu-id="fda50-263">rahat</span><span class="sxs-lookup"><span data-stu-id="fda50-263">comfortable</span></span> | <span data-ttu-id="fda50-264">3</span><span class="sxs-lookup"><span data-stu-id="fda50-264">3</span></span>
| <span data-ttu-id="fda50-265">uzaklık</span><span class="sxs-lookup"><span data-stu-id="fda50-265">distance</span></span> | <span data-ttu-id="fda50-266">1</span><span class="sxs-lookup"><span data-stu-id="fda50-266">1</span></span>
| <span data-ttu-id="fda50-267">Adası</span><span class="sxs-lookup"><span data-stu-id="fda50-267">island</span></span> | <span data-ttu-id="fda50-268">2</span><span class="sxs-lookup"><span data-stu-id="fda50-268">2</span></span>
| <span data-ttu-id="fda50-269">kauaʻi</span><span class="sxs-lookup"><span data-stu-id="fda50-269">kauaʻi</span></span> | <span data-ttu-id="fda50-270">2</span><span class="sxs-lookup"><span data-stu-id="fda50-270">2</span></span>
| <span data-ttu-id="fda50-271">bulunan</span><span class="sxs-lookup"><span data-stu-id="fda50-271">located</span></span> | <span data-ttu-id="fda50-272">2</span><span class="sxs-lookup"><span data-stu-id="fda50-272">2</span></span>
| <span data-ttu-id="fda50-273">Kuzey</span><span class="sxs-lookup"><span data-stu-id="fda50-273">north</span></span> | <span data-ttu-id="fda50-274">2</span><span class="sxs-lookup"><span data-stu-id="fda50-274">2</span></span>
| <span data-ttu-id="fda50-275">Okyanusu</span><span class="sxs-lookup"><span data-stu-id="fda50-275">ocean</span></span> | <span data-ttu-id="fda50-276">1, 2, 3</span><span class="sxs-lookup"><span data-stu-id="fda50-276">1, 2, 3</span></span>
| <span data-ttu-id="fda50-277">/</span><span class="sxs-lookup"><span data-stu-id="fda50-277">of</span></span> | <span data-ttu-id="fda50-278">2</span><span class="sxs-lookup"><span data-stu-id="fda50-278">2</span></span>
| <span data-ttu-id="fda50-279">üzerinde</span><span class="sxs-lookup"><span data-stu-id="fda50-279">on</span></span> |<span data-ttu-id="fda50-280">2</span><span class="sxs-lookup"><span data-stu-id="fda50-280">2</span></span>
| <span data-ttu-id="fda50-281">Sessiz</span><span class="sxs-lookup"><span data-stu-id="fda50-281">quiet</span></span> | <span data-ttu-id="fda50-282">4</span><span class="sxs-lookup"><span data-stu-id="fda50-282">4</span></span>
| <span data-ttu-id="fda50-283">odaları</span><span class="sxs-lookup"><span data-stu-id="fda50-283">rooms</span></span>  | <span data-ttu-id="fda50-284">1, 3</span><span class="sxs-lookup"><span data-stu-id="fda50-284">1, 3</span></span>
| <span data-ttu-id="fda50-285">secluded</span><span class="sxs-lookup"><span data-stu-id="fda50-285">secluded</span></span> | <span data-ttu-id="fda50-286">4</span><span class="sxs-lookup"><span data-stu-id="fda50-286">4</span></span>
| <span data-ttu-id="fda50-287">Deniz Kıyısı</span><span class="sxs-lookup"><span data-stu-id="fda50-287">shore</span></span> | <span data-ttu-id="fda50-288">2</span><span class="sxs-lookup"><span data-stu-id="fda50-288">2</span></span>
| <span data-ttu-id="fda50-289">spacious</span><span class="sxs-lookup"><span data-stu-id="fda50-289">spacious</span></span> | <span data-ttu-id="fda50-290">1</span><span class="sxs-lookup"><span data-stu-id="fda50-290">1</span></span>
| <span data-ttu-id="fda50-291">,</span><span class="sxs-lookup"><span data-stu-id="fda50-291">the</span></span> | <span data-ttu-id="fda50-292">1, 2</span><span class="sxs-lookup"><span data-stu-id="fda50-292">1, 2</span></span>
| <span data-ttu-id="fda50-293">-</span><span class="sxs-lookup"><span data-stu-id="fda50-293">to</span></span> | <span data-ttu-id="fda50-294">1</span><span class="sxs-lookup"><span data-stu-id="fda50-294">1</span></span>
| <span data-ttu-id="fda50-295">görünüm</span><span class="sxs-lookup"><span data-stu-id="fda50-295">view</span></span> | <span data-ttu-id="fda50-296">1, 2, 3</span><span class="sxs-lookup"><span data-stu-id="fda50-296">1, 2, 3</span></span>
| <span data-ttu-id="fda50-297">taramasını</span><span class="sxs-lookup"><span data-stu-id="fda50-297">walking</span></span> | <span data-ttu-id="fda50-298">1</span><span class="sxs-lookup"><span data-stu-id="fda50-298">1</span></span>
| <span data-ttu-id="fda50-299">İle</span><span class="sxs-lookup"><span data-stu-id="fda50-299">with</span></span> | <span data-ttu-id="fda50-300">3</span><span class="sxs-lookup"><span data-stu-id="fda50-300">3</span></span>


<span data-ttu-id="fda50-301">**Dizinli koşulları karşı sorgu terimlerinin eşleştirme**</span><span class="sxs-lookup"><span data-stu-id="fda50-301">**Matching query terms against indexed terms**</span></span>

<span data-ttu-id="fda50-302">Şimdi örnek sorgu döndürme yukarıdaki ters dizinlerini verildiğinde ve nasıl eşleşen belgeleri görmek için bizim örnek sorgu bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="fda50-302">Given the inverted indices above, let’s return to the sample query and see how matching documents are found for our example query.</span></span> <span data-ttu-id="fda50-303">Son sorgu ağaç şöyle geri çağırma:</span><span class="sxs-lookup"><span data-stu-id="fda50-303">Recall that the final query tree looks like this:</span></span> 

 ![Çözümlenen koşullarla Boole Sorgusu][4]

<span data-ttu-id="fda50-305">Sorgu yürütme sırasında tek tek sorguları karşı aranabilir alanlara bağımsız olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="fda50-305">During query execution, individual queries are executed against the searchable fields independently.</span></span> 

+ <span data-ttu-id="fda50-306">TermQuery, "spacious" eşleşmeleri 1 (otel Atman) belgesi.</span><span class="sxs-lookup"><span data-stu-id="fda50-306">The TermQuery, "spacious", matches document 1 (Hotel Atman).</span></span> 

+ <span data-ttu-id="fda50-307">PrefixQuery "air-condition *", herhangi bir belgeniz eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="fda50-307">The PrefixQuery, "air-condition*", doesn't match any documents.</span></span> 

  <span data-ttu-id="fda50-308">Bazen geliştiriciler kafasını karıştırabilirler bir davranış budur.</span><span class="sxs-lookup"><span data-stu-id="fda50-308">This is a behavior that sometimes confuses developers.</span></span> <span data-ttu-id="fda50-309">Belgede Air-conditioned terim var ancak iki terimleri varsayılan Çözümleyicisi tarafından ayrılır.</span><span class="sxs-lookup"><span data-stu-id="fda50-309">Although the term air-conditioned exists in the document, it is split into two terms by the default analyzer.</span></span> <span data-ttu-id="fda50-310">Kısmi terimleri içeren, önek sorguları çözümlenmediğini geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="fda50-310">Recall that prefix queries, which contain partial terms, are not analyzed.</span></span> <span data-ttu-id="fda50-311">Bu nedenle önek "air-condition" ile koşulları ters dizinde arama ve bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="fda50-311">Therefore terms with prefix "air-condition" are looked up in the inverted index and not found.</span></span>

+ <span data-ttu-id="fda50-312">"Okyanusu Görünüm" PhraseQuery koşulları "Okyanusu" ve "görüntüle" arar ve özgün belgede terimlerin yakınlık denetler.</span><span class="sxs-lookup"><span data-stu-id="fda50-312">The PhraseQuery, "ocean view", looks up the terms "ocean" and "view" and checks the proximity of terms in the original document.</span></span> <span data-ttu-id="fda50-313">Belgeleri 1, 2 ve 3 Bu sorguyu Açıklama alanına eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="fda50-313">Documents 1, 2 and 3 match this query in the description field.</span></span> <span data-ttu-id="fda50-314">"Okyanusu Görünüm" tümceciği için yerine tek tek sözcükleri bekliyoruz gibi belge 4 başlığında terim Okyanusu sahiptir, ancak bir eşleşme olarak değil dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="fda50-314">Notice document 4 has the term ocean in the title but isn’t considered a match, as we're looking for the "ocean view" phrase rather than individual words.</span></span> 

> [!Note]
> <span data-ttu-id="fda50-315">İle ayarlanan alanların sınırlamak sürece bir arama sorgusu bağımsız olarak Azure arama dizini içindeki tüm aranabilir alanları karşı yürütülür `searchFields` örnek arama isteğinde gösterildiği gibi parametre.</span><span class="sxs-lookup"><span data-stu-id="fda50-315">A search query is executed independently against all searchable fields in the Azure Search index unless you limit the fields set with the `searchFields` parameter, as illustrated in the example search request.</span></span> <span data-ttu-id="fda50-316">Seçilen alanlar hiçbirinde eşleşen belgeleri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="fda50-316">Documents that match in any of the selected fields are returned.</span></span> 

<span data-ttu-id="fda50-317">Tüm, söz konusu sorgu eşleşen belgelerdir 1, 2, 3.</span><span class="sxs-lookup"><span data-stu-id="fda50-317">On the whole, for the query in question, the documents that match are 1, 2, 3.</span></span> 

## <a name="stage-4-scoring"></a><span data-ttu-id="fda50-318">4. Aşama: Puanlama</span><span class="sxs-lookup"><span data-stu-id="fda50-318">Stage 4: Scoring</span></span>  

<span data-ttu-id="fda50-319">Her belge arama sonuç kümesinde bir ilgi puan atanır.</span><span class="sxs-lookup"><span data-stu-id="fda50-319">Every document in a search result set is assigned a relevance score.</span></span> <span data-ttu-id="fda50-320">İlgi puanının derece yüksek en iyi bir kullanıcı tarafından arama sorgusu ifade edilen sorunuzu bu belgeleri işlevdir.</span><span class="sxs-lookup"><span data-stu-id="fda50-320">The function of the relevance score is to rank higher those documents that best answer a user question as expressed by the search query.</span></span> <span data-ttu-id="fda50-321">Puan eşleşen koşulları istatistiksel özelliklerini göre hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="fda50-321">The score is computed based on statistical properties of terms that matched.</span></span> <span data-ttu-id="fda50-322">Puanlama formülü çekirdeği [TF/IDF (terim sıklığı ters belge sıklığı)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).</span><span class="sxs-lookup"><span data-stu-id="fda50-322">At the core of the scoring formula is [TF/IDF (term frequency-inverse document frequency)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).</span></span> <span data-ttu-id="fda50-323">Nadir ve sık kullanılan terimleri içeren sorgularda TF/IDF nadir terimi içeren sonuçları yükseltir.</span><span class="sxs-lookup"><span data-stu-id="fda50-323">In queries containing rare and common terms, TF/IDF promotes results containing the rare term.</span></span> <span data-ttu-id="fda50-324">Örneğin, tüm Wikipedia makalelerde kuramsal bir dizinde belgelerden sorguyla eşleşen *Başkanı*, üzerinde eşleşen belgeler *Başkanı* üzerinde eşleşen belgeler daha fazla ilgili kabul edilip edilmediğini **.</span><span class="sxs-lookup"><span data-stu-id="fda50-324">For example, in a hypothetical index with all Wikipedia articles, from documents that matched the query *the president*, documents matching on *president* are considered more relevant than documents matching on *the*.</span></span>


### <a name="scoring-example"></a><span data-ttu-id="fda50-325">Puanlama örneği</span><span class="sxs-lookup"><span data-stu-id="fda50-325">Scoring example</span></span>

<span data-ttu-id="fda50-326">Bizim örnek sorgu eşleşen üç belgeleri geri çağırma:</span><span class="sxs-lookup"><span data-stu-id="fda50-326">Recall the three documents that matched our example query:</span></span>
~~~~
search=Spacious, air-condition* +"Ocean view"  
~~~~
~~~~
{  
  "value": [
    {
      "@search.score": 0.25610128,
      "id": "1",
      "title": "Hotel Atman",
      "description": "Spacious rooms, ocean view, walking distance to the beach."
    },
    {
      "@search.score": 0.08951007,
      "id": "3",
      "title": "Playa Hotel",
      "description": "Comfortable, air-conditioned rooms with ocean view."
    },
    {
      "@search.score": 0.05967338,
      "id": "2",
      "title": "Ocean Resort",
      "description": "Located on a cliff on the north shore of the island of Kauai. Ocean view."
    }
  ]
}
~~~~

<span data-ttu-id="fda50-327">Çünkü belge 1 sorgu en iyi eşleşen. her iki terim *spacious* ve gerekli deyimi *Okyanusu Görünüm* Açıklama alanına oluşur.</span><span class="sxs-lookup"><span data-stu-id="fda50-327">Document 1 matched the query best because both the term *spacious* and the required phrase *ocean view* occur in the description field.</span></span> <span data-ttu-id="fda50-328">Sonraki iki belgeleri yalnızca tümcecik eşleşen *Okyanusu Görünüm*.</span><span class="sxs-lookup"><span data-stu-id="fda50-328">The next two documents match only the phrase *ocean view*.</span></span> <span data-ttu-id="fda50-329">Bunlar aynı şekilde sorguyla eşleşen olsa bile belge 2 ve 3 ilgi puanını farklıdır şaşırtıcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="fda50-329">It might be surprising that the relevance score for document 2 and 3 is different even though they matched the query in the same way.</span></span> <span data-ttu-id="fda50-330">Puanlama formülü yalnızca TF/IDF'den daha fazla bileşenlere sahip olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="fda50-330">It's because the scoring formula has more components than just TF/IDF.</span></span> <span data-ttu-id="fda50-331">Bu durumda, belge 3 açıklamasını kısa olduğundan biraz daha yüksek bir puan atanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fda50-331">In this case, document 3 was assigned a slightly higher score because its description is shorter.</span></span> <span data-ttu-id="fda50-332">Hakkında bilgi edinin [Lucene'nın pratik Puanlama formülü](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) ilgi puan alan uzunluğu ve diğer etkenlere bağlı nasıl etkileyebilir anlamak için.</span><span class="sxs-lookup"><span data-stu-id="fda50-332">Learn about [Lucene's Practical Scoring Formula](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) to understand how field length and other factors can influence the relevance score.</span></span>

<span data-ttu-id="fda50-333">Bazı sorgu türü (joker karakter öneki, regex) her zaman genel belge puan için sabit bir puan katkıda bulunun.</span><span class="sxs-lookup"><span data-stu-id="fda50-333">Some query types (wildcard, prefix, regex) always contribute a constant score to the overall document score.</span></span> <span data-ttu-id="fda50-334">Bu sorgu genişletme bulunan eşleşmeler sonuçlarında dahil edilecek sağlar ancak derecelendirme etkilemeden.</span><span class="sxs-lookup"><span data-stu-id="fda50-334">This allows matches found through query expansion to be included in the results, but without affecting the ranking.</span></span> 

<span data-ttu-id="fda50-335">Bu önemli neden bir örnek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fda50-335">An example illustrates why this matters.</span></span> <span data-ttu-id="fda50-336">Giriş farklı koşullarını ("tur", "tourettes" ve "tourmaline" bulunan eşleşmeleri ile girişi "tur *" düşünebilirsiniz) çok sayıda olası eşleşmeleri ile kısmi dize olduğundan önek aramaları da dahil olmak üzere, joker karakter aramaları tanımına göre belirsiz.</span><span class="sxs-lookup"><span data-stu-id="fda50-336">Wildcard searches, including prefix searches, are ambiguous by definition because the input is a partial string with potential matches on a very large number of disparate terms (consider an input of "tour*", with matches found on “tours”, “tourettes”, and “tourmaline”).</span></span> <span data-ttu-id="fda50-337">Bu sonuçları yapısını verildiğinde, hangi koşulları diğerlerinden daha değerli makul çıkarsamak için bir yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="fda50-337">Given the nature of these results, there is no way to reasonably infer which terms are more valuable than others.</span></span> <span data-ttu-id="fda50-338">Bu nedenle, biz terim sıklıklarını sonuçları türleri joker karakter, önek ve regex sorgularda Puanlama zaman yoksay.</span><span class="sxs-lookup"><span data-stu-id="fda50-338">For this reason, we ignore term frequencies when scoring results in queries of types wildcard, prefix and regex.</span></span> <span data-ttu-id="fda50-339">Kısmi ve tam koşulları içeren bir çok parçalı arama isteğinde kısmi giriş sonuçlarından büyük olasılıkla beklenmeyen eşleşen doğru sapması önlemek için sabit bir puan ile birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="fda50-339">In a multi-part search request that includes partial and complete terms, results from the partial input are incorporated with a constant score to avoid bias towards potentially unexpected matches.</span></span>

### <a name="score-tuning"></a><span data-ttu-id="fda50-340">Puan ayarlama</span><span class="sxs-lookup"><span data-stu-id="fda50-340">Score tuning</span></span>

<span data-ttu-id="fda50-341">Azure Search'te ilgi puanları ayarlamak için iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="fda50-341">There are two ways to tune relevance scores in Azure Search:</span></span>

1. <span data-ttu-id="fda50-342">**Profilleri Puanlama** bir dizi kurala göre sonuçları dereceli listesi belgelerde Yükselt.</span><span class="sxs-lookup"><span data-stu-id="fda50-342">**Scoring profiles** promote documents in the ranked list of results based on a set of rules.</span></span> <span data-ttu-id="fda50-343">Bizim örneğimizde, biz Açıklama alanına eşleşen belgeleri daha ilgili Başlık alanında eşleşen belgeleri düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fda50-343">In our example, we could consider documents that matched in the title field more relevant than documents that matched in the description field.</span></span> <span data-ttu-id="fda50-344">Ayrıca, dizinimizi her otel için bir fiyat alan olsaydı, biz alt fiyat belgelerle yükseltmek.</span><span class="sxs-lookup"><span data-stu-id="fda50-344">Additionally, if our index had a price field for each hotel, we could promote documents with lower price.</span></span> <span data-ttu-id="fda50-345">Daha fazla öğrenmek için [Puanlama profilleri arama dizinine ekleyin.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)</span><span class="sxs-lookup"><span data-stu-id="fda50-345">Learn more how to [add Scoring Profiles to a search index.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)</span></span>
2. <span data-ttu-id="fda50-346">**Terim** (yalnızca kullanılabilir tam Lucene sorgu söz dizimi) artırma işleci sağlar `^` sorgu ağaç herhangi bir kısmını uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="fda50-346">**Term boosting** (available only in the Full Lucene query syntax) provides a boosting operator `^` that can be applied to any part of the query tree.</span></span> <span data-ttu-id="fda50-347">Önek arama yerine örneğimizde *air-condition*\*, bir arama için tam terimi *air-condition* veya önek, ancak tam terimini eşleşen belgeleri derece yüksek terim sorguya artırma uygulayarak: *hava durumu ^ 2 || Air-Condition**.</span><span class="sxs-lookup"><span data-stu-id="fda50-347">In our example, instead of searching on the prefix *air-condition*\*, one could search for either the exact term *air-condition* or the prefix, but documents that match on the exact term are ranked higher by applying boost to the term query: *air-condition^2||air-condition**.</span></span> <span data-ttu-id="fda50-348">Daha fazla bilgi edinmek [terim](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).</span><span class="sxs-lookup"><span data-stu-id="fda50-348">Learn more about [term boosting](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).</span></span>


### <a name="scoring-in-a-distributed-index"></a><span data-ttu-id="fda50-349">Dağıtılmış bir dizinde Puanlama</span><span class="sxs-lookup"><span data-stu-id="fda50-349">Scoring in a distributed index</span></span>

<span data-ttu-id="fda50-350">Azure Search'te tüm dizinleri otomatik olarak birden çok parça bölünür bize birden çok düğüm arasında dizin hizmeti ölçek sırasında hızlı bir şekilde dağıtmak veren yukarı veya ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="fda50-350">All indexes in Azure Search are automatically split into multiple shards, allowing us to quickly distribute the index among multiple nodes during service scale up or scale down.</span></span> <span data-ttu-id="fda50-351">Bir arama isteğine verildiğinde, her parça karşı bağımsız olarak verilir.</span><span class="sxs-lookup"><span data-stu-id="fda50-351">When a search request is issued, it’s issued against each shard independently.</span></span> <span data-ttu-id="fda50-352">Her parça sonuçlarından ardından birleştirilmiş ve (diğer sıralamaya tanımlanmışsa) puana göre sıralanmış.</span><span class="sxs-lookup"><span data-stu-id="fda50-352">The results from each shard are then merged and ordered by score (if no other ordering is defined).</span></span> <span data-ttu-id="fda50-353">Puanlama işlevi ağırlıkları değil tüm parça terim sıklığı parça tüm belgelerde ters belge sıklığının karşı sorgu bilmeniz önemlidir!</span><span class="sxs-lookup"><span data-stu-id="fda50-353">It is important to know that the scoring function weights query term frequency against its inverse document frequency in all documents within the shard, not across all shards!</span></span>

<span data-ttu-id="fda50-354">Bu bir ilgi puan anlamına gelir *verebilir* üzerinde farklı parça bulunuyorsa aynı belgeler için farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="fda50-354">This means a relevance score *could* be different for identical documents if they reside on different shards.</span></span> <span data-ttu-id="fda50-355">Neyse ki, bu farklara belge dizinde sayısı daha fazla bile terim dağıtım nedeniyle büyüdükçe kayboluyor eğilimindedir.</span><span class="sxs-lookup"><span data-stu-id="fda50-355">Fortunately, such differences tend to disappear as the number of documents in the index grows due to more even term distribution.</span></span> <span data-ttu-id="fda50-356">Varsaymak mümkün değildir üzerinde hangi parça herhangi belirli bir belgeye yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="fda50-356">It’s not possible to assume on which shard any given document will be placed.</span></span> <span data-ttu-id="fda50-357">Ancak, bir belge anahtarı değiştirmez varsayıldığında, bu her zaman aynı parça atanır.</span><span class="sxs-lookup"><span data-stu-id="fda50-357">However, assuming a document key doesn't change, it will always be assigned to the same shard.</span></span>

<span data-ttu-id="fda50-358">Genel olarak, belge puan sipariş kararlılık önemliyse belgeleri sıralama için en iyi öznitelik değil.</span><span class="sxs-lookup"><span data-stu-id="fda50-358">In general, document score is not the best attribute for ordering documents if order stability is important.</span></span> <span data-ttu-id="fda50-359">Örneğin, iki belgeyle aynı puan verildiğinde, hangisinin aynı sorgu sonraki çalıştırmalarında ilk olarak görünür garantisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="fda50-359">For example, given two document with an identical score, there is no guarantee which one appears first in subsequent runs of the same query.</span></span> <span data-ttu-id="fda50-360">Belge puan sonuçları kümesindeki diğer belgeleri göre belge ilgi genel bir fikir yalnızca vermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="fda50-360">Document score should only give a general sense of document relevance relative to other documents in the results set.</span></span>

## <a name="conclusion"></a><span data-ttu-id="fda50-361">Sonuç</span><span class="sxs-lookup"><span data-stu-id="fda50-361">Conclusion</span></span>

<span data-ttu-id="fda50-362">Internet arama motorları başarısını tam metin araması için beklentiler özel veriler üzerinde yükseltilmiş.</span><span class="sxs-lookup"><span data-stu-id="fda50-362">The success of internet search engines has raised expectations for full text search over private data.</span></span> <span data-ttu-id="fda50-363">Arama deneyimi neredeyse her türlü için şimdi koşulları yanlış yazılmış veya eksik olduğunda bile bizim hedefi anlamak için altyapısı bekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="fda50-363">For almost any kind of search experience, we now expect the engine to understand our intent, even when terms are misspelled or incomplete.</span></span> <span data-ttu-id="fda50-364">Hatta eşdeğer terimler veya hiçbir zaman gerçekte belirtilen eş anlamlıları dayalı eşleşmeler bekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="fda50-364">We might even expect matches based on near equivalent terms or synonyms that we never actually specified.</span></span>

<span data-ttu-id="fda50-365">Teknik açıdan, tam metin araması Gelişmiş bir dil analiz ve biçimlendirebilir, genişletin ve ilgili bir sonuç sunmak için sorgu terimlerinin dönüştürme şekilde işlemeye sistematik bir yaklaşım gerektiren yüksek oranda karmaşık bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="fda50-365">From a technical standpoint, full text search is highly complex, requiring sophisticated linguistic analysis and a systematic approach to processing in ways that distill, expand, and transform query terms to deliver a relevant result.</span></span> <span data-ttu-id="fda50-366">Devralınan karmaşıklık göz önüne alındığında, bir sorgu sonucunu etkileyen faktörler çok vardır.</span><span class="sxs-lookup"><span data-stu-id="fda50-366">Given the inherent complexities, there are a lot of factors that can affect the outcome of a query.</span></span> <span data-ttu-id="fda50-367">Bu nedenle, tam metin araması mekanikleri anlamak için zaman yatırım, beklenmeyen sonuçlara çalışmaya çalışırken somut avantajları sunar.</span><span class="sxs-lookup"><span data-stu-id="fda50-367">For this reason, investing the time to understand the mechanics of full text search offers tangible benefits when trying to work through unexpected results.</span></span>  

<span data-ttu-id="fda50-368">Bu makalede, Azure Search bağlamında tam metin araması incelediniz.</span><span class="sxs-lookup"><span data-stu-id="fda50-368">This article explored full text search in the context of Azure Search.</span></span> <span data-ttu-id="fda50-369">Olası nedenleri ve çözümlemeleri sorgu karşılaşılan adresleme tanımak için yeterli arka plan verir umuyoruz.</span><span class="sxs-lookup"><span data-stu-id="fda50-369">We hope it gives you sufficient background to recognize potential causes and resolutions for addressing common query problems.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fda50-370">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fda50-370">Next steps</span></span>

+ <span data-ttu-id="fda50-371">Örnek dizini oluşturun, farklı sorguları deneyin ve sonuçları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="fda50-371">Build the sample index, try out different queries and review results.</span></span> <span data-ttu-id="fda50-372">Yönergeler için bkz: [oluşturmak ve Portalı'nda bir dizin sorgu](search-get-started-portal.md#query-index).</span><span class="sxs-lookup"><span data-stu-id="fda50-372">For instructions, see [Build and query an index in the portal](search-get-started-portal.md#query-index).</span></span>

+ <span data-ttu-id="fda50-373">Ek sorgu sözdiziminde deneyin [Search belgeleri](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) örnek bölümüne veya [Basit Sorgu söz dizimi](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) Portalı'nda arama Gezgini'nde.</span><span class="sxs-lookup"><span data-stu-id="fda50-373">Try additional query syntax from the [Search Documents](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) example section or from [Simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) in Search explorer in the portal.</span></span>

+ <span data-ttu-id="fda50-374">Gözden geçirme [profilleri Puanlama](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) sıralama, arama uygulamanızda ayarlamak istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="fda50-374">Review [scoring profiles](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) if you want to tune ranking in your search application.</span></span>

+ <span data-ttu-id="fda50-375">Uygulamayı öğrenin [dile özgü sözcük çözümleyiciler](https://docs.microsoft.com/rest/api/searchservice/language-support).</span><span class="sxs-lookup"><span data-stu-id="fda50-375">Learn how to apply [language-specific lexical analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support).</span></span>

+ <span data-ttu-id="fda50-376">[Özel çözümleyiciler yapılandırma](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) en az işleme veya belirli alanları üzerindeki özel işleme için.</span><span class="sxs-lookup"><span data-stu-id="fda50-376">[Configure custom analyzers](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) for either minimal processing or specialized processing on specific fields.</span></span>

+ <span data-ttu-id="fda50-377">[Standart ve İngilizce çözümleyiciler karşılaştırmak](http://alice.unearth.ai/)) yana birimi bu demo web sitesinde.</span><span class="sxs-lookup"><span data-stu-id="fda50-377">[Compare standard and English analyzers](http://alice.unearth.ai/)) side-by-side on this demo web site.</span></span> 

## <a name="see-also"></a><span data-ttu-id="fda50-378">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="fda50-378">See also</span></span>

[<span data-ttu-id="fda50-379">REST API belgelerde arama</span><span class="sxs-lookup"><span data-stu-id="fda50-379">Search Documents REST API</span></span>](https://docs.microsoft.com/rest/api/searchservice/search-documents)

[<span data-ttu-id="fda50-380">Basit sorgu söz dizimi</span><span class="sxs-lookup"><span data-stu-id="fda50-380">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)

[<span data-ttu-id="fda50-381">Tam Lucene sorgu söz dizimi</span><span class="sxs-lookup"><span data-stu-id="fda50-381">Full Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

[<span data-ttu-id="fda50-382">Arama sonuçlarını işleme</span><span class="sxs-lookup"><span data-stu-id="fda50-382">Handle search results</span></span>](https://docs.microsoft.com/azure/search/search-pagination-page-layout)

<!--Image references-->
[1]: ./media/search-lucene-query-architecture/architecture-diagram2.png
[2]: ./media/search-lucene-query-architecture/azSearch-queryparsing-should2.png
[3]: ./media/search-lucene-query-architecture/azSearch-queryparsing-must2.png
[4]: ./media/search-lucene-query-architecture/azSearch-queryparsing-spacious2.png
