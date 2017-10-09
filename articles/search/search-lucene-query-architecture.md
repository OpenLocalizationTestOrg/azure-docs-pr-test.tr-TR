---
title: Azure Search'te aaaFull metin arama motoru (Lucene) mimarisi | Microsoft Docs
description: "Açıklama Lucene sorgu işleme ve belge alma kavramları için tam metin araması, ilgili tooAzure arama olarak."
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
ms.openlocfilehash: c6d1bea8d40154fd9237b9e44584cdfcd193cbd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-full-text-search-works-in-azure-search"></a><span data-ttu-id="0dea0-103">Azure Search'te nasıl tam metin araması çalışır</span><span class="sxs-lookup"><span data-stu-id="0dea0-103">How full text search works in Azure Search</span></span>

<span data-ttu-id="0dea0-104">Bu makale, Azure Search'te Lucene tam metin araması nasıl çalıştığını daha derin bir anlayış isteyen geliştiriciler için yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="0dea0-104">This article is for developers who need a deeper understanding of how Lucene full text search works in Azure Search.</span></span> <span data-ttu-id="0dea0-105">Metin sorguları için sorunsuz bir şekilde beklenen sonuçları Azure Search Çoğu senaryoda teslim eder, ancak bazen "kapalı" şekilde görünen bir sonuç almak.</span><span class="sxs-lookup"><span data-stu-id="0dea0-105">For text queries, Azure Search will seamlessly deliver expected results in most scenarios, but occasionally you might get a result that seems "off" somehow.</span></span> <span data-ttu-id="0dea0-106">Bu durumlarda Lucene sorgu yürütme dört aşamaları hello bir arka plana sahip (ayrıştırma, sözcük analiz sorgusu, belge eşleşen, Puanlama) belirli değişiklikleri tooquery parametrelerini tanımlamak veya dizin hello dağıtılacak yapılandırma yardımcı olur İstenen sonuca.</span><span class="sxs-lookup"><span data-stu-id="0dea0-106">In these situations, having a background in hello four stages of Lucene query execution (query parsing, lexical analysis, document matching, scoring) can help you identify specific changes tooquery parameters or index configuration that will deliver hello desired outcome.</span></span> 

> [!Note] 
> <span data-ttu-id="0dea0-107">Azure arama için tam metin araması Lucene kullanır, ancak Lucene tümleştirme geniş kapsamlı değildir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-107">Azure Search uses Lucene for full text search, but Lucene integration is not exhaustive.</span></span> <span data-ttu-id="0dea0-108">Biz seçmeli olarak kullanıma sunmak ve Lucene işlevselliği tooenable hello senaryoları önemli tooAzure arama genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dea0-108">We selectively expose and extend Lucene functionality tooenable hello scenarios important tooAzure Search.</span></span> 

## <a name="architecture-overview-and-diagram"></a><span data-ttu-id="0dea0-109">Mimarisine genel bakış ve diyagramı</span><span class="sxs-lookup"><span data-stu-id="0dea0-109">Architecture overview and diagram</span></span>

<span data-ttu-id="0dea0-110">Bir tam metin arama sorgusu işlemeye başlıyor hello sorgu metni tooextract arama terimleri ayrıştırma ile.</span><span class="sxs-lookup"><span data-stu-id="0dea0-110">Processing a full text search query starts with parsing hello query text tooextract search terms.</span></span> <span data-ttu-id="0dea0-111">Merhaba arama motoru tooretrieve belgelerin dizinini eşleşen şartlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="0dea0-111">hello search engine uses an index tooretrieve documents with matching terms.</span></span> <span data-ttu-id="0dea0-112">Tek tek sorgu terimleri bazen ayrılmıştır ve ne olası bir eşleşme olarak kabul edilebilir üzerinde daha geniş bir net yeni forms toocast reconstituted.</span><span class="sxs-lookup"><span data-stu-id="0dea0-112">Individual query terms are sometimes broken down and reconstituted into new forms toocast a broader net over what could be considered as a potential match.</span></span> <span data-ttu-id="0dea0-113">Bir sonuç kümesi sonra bir ilgi puan atanan tooeach eşleşen belgenin tarafından sıralanır.</span><span class="sxs-lookup"><span data-stu-id="0dea0-113">A result set is then sorted by a relevance score assigned tooeach individual matching document.</span></span> <span data-ttu-id="0dea0-114">Bu liste derece hello hello üstündeki toohello çağıran uygulama döndürülür.</span><span class="sxs-lookup"><span data-stu-id="0dea0-114">Those at hello top of hello ranked list are returned toohello calling application.</span></span>

<span data-ttu-id="0dea0-115">Sorgu yürütme açıklandı, dört aşamadan oluşur:</span><span class="sxs-lookup"><span data-stu-id="0dea0-115">Restated, query execution has four stages:</span></span> 

1. <span data-ttu-id="0dea0-116">Sorgu ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="0dea0-116">Query parsing</span></span> 
2. <span data-ttu-id="0dea0-117">Sözcük çözümleme</span><span class="sxs-lookup"><span data-stu-id="0dea0-117">Lexical analysis</span></span> 
3. <span data-ttu-id="0dea0-118">Belge alma</span><span class="sxs-lookup"><span data-stu-id="0dea0-118">Document retrieval</span></span> 
4. <span data-ttu-id="0dea0-119">Puanlama</span><span class="sxs-lookup"><span data-stu-id="0dea0-119">Scoring</span></span> 

<span data-ttu-id="0dea0-120">Merhaba diyagramda hello kullanılan bileşenler tooprocess bir arama isteğine gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-120">hello diagram below illustrates hello components used tooprocess a search request.</span></span> 

 ![Azure Search'te Lucene sorgu mimarisi diyagramı][1]


| <span data-ttu-id="0dea0-122">Başlıca bileşenler</span><span class="sxs-lookup"><span data-stu-id="0dea0-122">Key components</span></span> | <span data-ttu-id="0dea0-123">İşlev açıklaması</span><span class="sxs-lookup"><span data-stu-id="0dea0-123">Functional description</span></span> | 
|----------------|------------------------|
|<span data-ttu-id="0dea0-124">**Sorgu ayrıştırıcıları**</span><span class="sxs-lookup"><span data-stu-id="0dea0-124">**Query parsers**</span></span> | <span data-ttu-id="0dea0-125">Sorgu işleçleri sorgu terimlerinin ayırın ve hello sorgu yapısını (sorgu ağacı) gönderilen toobe toohello arama motoru oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0dea0-125">Separate query terms from query operators and create hello query structure (a query tree) toobe sent toohello search engine.</span></span> |
|<span data-ttu-id="0dea0-126">**Çözümleyiciler**</span><span class="sxs-lookup"><span data-stu-id="0dea0-126">**Analyzers**</span></span> | <span data-ttu-id="0dea0-127">Sözcük analiz sorgu terimlerinin üzerinde gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0dea0-127">Perform lexical analysis on query terms.</span></span> <span data-ttu-id="0dea0-128">Bu işlem, dönüştürme, kaldırma veya sorgu koşullarını genişletme içerebilir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-128">This process can involve transforming, removing, or expanding of query terms.</span></span> |
|<span data-ttu-id="0dea0-129">**Dizin**</span><span class="sxs-lookup"><span data-stu-id="0dea0-129">**Index**</span></span> | <span data-ttu-id="0dea0-130">Verimli veri yapısı toostore kullanılan ve dizinli belgelerden ayıklanan aranabilir koşullarını düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dea0-130">An efficient data structure used toostore and organize searchable terms extracted from indexed documents.</span></span> |
|<span data-ttu-id="0dea0-131">**Arama motoru**</span><span class="sxs-lookup"><span data-stu-id="0dea0-131">**Search engine**</span></span> | <span data-ttu-id="0dea0-132">Alır ve eşleşen hello Merhaba içeriğine göre belgelerin puanlarını dizin tersine.</span><span class="sxs-lookup"><span data-stu-id="0dea0-132">Retrieves and scores matching documents based on hello contents of hello inverted index.</span></span> |

## <a name="anatomy-of-a-search-request"></a><span data-ttu-id="0dea0-133">Bir arama isteğine anatomisi</span><span class="sxs-lookup"><span data-stu-id="0dea0-133">Anatomy of a search request</span></span>

<span data-ttu-id="0dea0-134">Bir arama isteğine bir sonuç kümesi döndürdü, tam bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-134">A search request is a complete specification of what should be returned in a result set.</span></span> <span data-ttu-id="0dea0-135">Basit haliyle, hiçbir ölçüt içermeyen boş bir sorgu değil.</span><span class="sxs-lookup"><span data-stu-id="0dea0-135">In simplest form, it is an empty query with no criteria of any kind.</span></span> <span data-ttu-id="0dea0-136">Birkaç koşulları, belki de kapsamlı toocertain alanlarla büyük olasılıkla bir filtre ifadesi ve kuralları sipariş sorgu parametreleri daha gerçekçi bir örnek içerir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-136">A more realistic example includes parameters, several query terms, perhaps scoped toocertain fields, with possibly a filter expression and ordering rules.</span></span>  

<span data-ttu-id="0dea0-137">Merhaba aşağıdaki örnekte olduğu tooAzure arama Gönder bir arama isteğine hello kullanarak [REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span><span class="sxs-lookup"><span data-stu-id="0dea0-137">hello following example is a search request you might send tooAzure Search using hello [REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span></span>  

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

<span data-ttu-id="0dea0-138">Bu istek için aşağıdaki hello arama motoru hello:</span><span class="sxs-lookup"><span data-stu-id="0dea0-138">For this request, hello search engine does hello following:</span></span>

1. <span data-ttu-id="0dea0-139">Giden belgeleri hello fiyat en az 60 ve değerinden 300 olduğu filtreler.</span><span class="sxs-lookup"><span data-stu-id="0dea0-139">Filters out documents where hello price is at least $60 and less than $300.</span></span>
2. <span data-ttu-id="0dea0-140">Merhaba sorgusunu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="0dea0-140">Executes hello query.</span></span> <span data-ttu-id="0dea0-141">Bu örnekte, hello arama sorgusu tümcecikleri ve şartları oluşur: `"Spacious, air-condition* +\"Ocean view\""` (kullanıcılar genellikle noktalama girin yoktur, ancak hello örnekte dahil olmak üzere verir bize tooexplain nasıl çözümleyiciler tanıtıcı).</span><span class="sxs-lookup"><span data-stu-id="0dea0-141">In this example, hello search query consists of phrases and terms: `"Spacious, air-condition* +\"Ocean view\""` (users typically don't enter punctuation, but including it in hello example allows us tooexplain how analyzers handle it).</span></span> <span data-ttu-id="0dea0-142">Bu sorgu için hello arama motoru hello açıklama tarar ve belirtilen başlık alanları `searchFields` "Okyanusu Görünüm" içeren belgeleri ve ayrıca "spacious" Merhaba terim veya hello önekiyle başlayan koşulları "air-condition".</span><span class="sxs-lookup"><span data-stu-id="0dea0-142">For this query, hello search engine scans hello description and title fields specified in `searchFields` for documents that contain "Ocean view", and additionally on hello term "spacious", or on terms that start with hello prefix "air-condition".</span></span> <span data-ttu-id="0dea0-143">Merhaba `searchMode` parametredir kullanılan toomatch herhangi terim (varsayılan) veya bir terim olduğu kesinlikle gerekli durumlarda bunların tümünün (`+`).</span><span class="sxs-lookup"><span data-stu-id="0dea0-143">hello `searchMode` parameter is used toomatch on any term (default) or all of them, for cases where a term is not explicitly required (`+`).</span></span>
3. <span data-ttu-id="0dea0-144">Siparişleri Oteller sonuç kümesini Coğrafya konumu verilen ve toohello çağıran uygulama döndürülen yakınlık tooa tarafından hello.</span><span class="sxs-lookup"><span data-stu-id="0dea0-144">Orders hello resulting set of hotels by proximity tooa given geography location, and then returned toohello calling application.</span></span> 

<span data-ttu-id="0dea0-145">Merhaba, bu makalenin çoğunluğu hello hakkında işlemesidir *arama sorgusu*: `"Spacious, air-condition* +\"Ocean view\""`.</span><span class="sxs-lookup"><span data-stu-id="0dea0-145">hello majority of this article is about processing of hello *search query*: `"Spacious, air-condition* +\"Ocean view\""`.</span></span> <span data-ttu-id="0dea0-146">Filtreleme ve Sıralama kapsamının dışına markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="0dea0-146">Filtering and ordering are out of scope.</span></span> <span data-ttu-id="0dea0-147">Daha fazla bilgi için bkz: Merhaba [arama API başvuru belgeleri](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span><span class="sxs-lookup"><span data-stu-id="0dea0-147">For more information, see hello [Search API reference documentation](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span></span>

<a name="stage1"></a>
## <a name="stage-1-query-parsing"></a><span data-ttu-id="0dea0-148">1. Aşama: ayrıştırma sorgu</span><span class="sxs-lookup"><span data-stu-id="0dea0-148">Stage 1: Query parsing</span></span> 

<span data-ttu-id="0dea0-149">Belirtildiği gibi hello sorgu dizesi hello ilk satır hello isteğinin şöyledir:</span><span class="sxs-lookup"><span data-stu-id="0dea0-149">As noted, hello query string is hello first line of hello request:</span></span> 

~~~~
 "search": "Spacious, air-condition* +\"Ocean view\"", 
~~~~

<span data-ttu-id="0dea0-150">Merhaba sorgu ayrıştırıcı ayıran işleçleri (gibi `*` ve `+` hello örnekte) arama koşulları ve hello arama sorgusu içine deconstructs *alt sorgulara* desteklenen bir türde:</span><span class="sxs-lookup"><span data-stu-id="0dea0-150">hello query parser separates operators (such as `*` and `+` in hello example) from search terms, and deconstructs hello search query into *subqueries* of a supported type:</span></span> 

+ <span data-ttu-id="0dea0-151">*Terim sorgu* (gibi spacious) tek başına koşulları için</span><span class="sxs-lookup"><span data-stu-id="0dea0-151">*term query* for standalone terms (like spacious)</span></span>
+ <span data-ttu-id="0dea0-152">*Tümcecik sorgusu* tırnak işaretli şartlarının (gibi Okyanusu görünümü)</span><span class="sxs-lookup"><span data-stu-id="0dea0-152">*phrase query* for quoted terms (like ocean view)</span></span>
+ <span data-ttu-id="0dea0-153">*önek sorgu* önek işleci tarafından izlenen koşulları için `*` (air-condition gibi)</span><span class="sxs-lookup"><span data-stu-id="0dea0-153">*prefix query* for terms followed by a prefix operator `*` (like air-condition)</span></span>

<span data-ttu-id="0dea0-154">Desteklenen sorgu türlerinin tam listesi için bkz: [Lucene sorgu sytnax](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)</span><span class="sxs-lookup"><span data-stu-id="0dea0-154">For a full list of supported query types see [Lucene query sytnax](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)</span></span>

<span data-ttu-id="0dea0-155">Bir alt sorgu ile ilişkili işleçleri belirlemek hello sorgu "olmalıdır" veya "olmalıdır" bir belge için sırayla memnun toobe kabul bir eşleşme.</span><span class="sxs-lookup"><span data-stu-id="0dea0-155">Operators associated with a subquery determine whether hello query "must be" or "should be" satisfied in order for a document toobe considered a match.</span></span> <span data-ttu-id="0dea0-156">Örneğin, `+"Ocean view"` "ayarlanmalıdır" son toohello `+` işleci.</span><span class="sxs-lookup"><span data-stu-id="0dea0-156">For example, `+"Ocean view"` is "must" due toohello `+` operator.</span></span> 

<span data-ttu-id="0dea0-157">Merhaba sorgu ayrıştırıcı yeniden yapılandırır hello alt sorgulara içine bir *sorgu ağaç* isteğe bağlı olarak (Merhaba sorgu temsil eden bir iç yapısı) toohello arama motorunda geçirir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-157">hello query parser restructures hello subqueries into a *query tree* (an internal structure representing hello query) it passes on toohello search engine.</span></span> <span data-ttu-id="0dea0-158">Merhaba ilk aşamasında ayrıştırma sorgu hello sorgu ağaç şöyle görünür.</span><span class="sxs-lookup"><span data-stu-id="0dea0-158">In hello first stage of query parsing, hello query tree looks like this.</span></span>  

 ![Boolean sorgu searchmode herhangi][2]

### <a name="supported-parsers-simple-and-full-lucene"></a><span data-ttu-id="0dea0-160">Ayrıştırıcıları desteklenen: Basit ve tam Lucene</span><span class="sxs-lookup"><span data-stu-id="0dea0-160">Supported parsers: Simple and Full Lucene</span></span> 

 <span data-ttu-id="0dea0-161">Azure arama gösteren iki farklı sorgu dili, `simple` (varsayılan) ve `full`.</span><span class="sxs-lookup"><span data-stu-id="0dea0-161">Azure Search exposes two different query languages, `simple` (default) and `full`.</span></span> <span data-ttu-id="0dea0-162">Merhaba ayarı tarafından `queryType` arama isteğinizi parametresi, size hello sorgu ayrıştırıcı bunu bilen sorgu dili, toointerpret nasıl hello işleçleri ve sözdizimi seçin.</span><span class="sxs-lookup"><span data-stu-id="0dea0-162">By setting hello `queryType` parameter with your search request, you tell hello query parser which query language you choose so that it knows how toointerpret hello operators and syntax.</span></span> <span data-ttu-id="0dea0-163">Merhaba [basit sorgu dili](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) sezgisel ve sağlam, genellikle uygun toointerpret kullanıcı girişi olarak-istemci tarafı işleme olmadan.</span><span class="sxs-lookup"><span data-stu-id="0dea0-163">hello [Simple query langauge](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) is intuitive and robust, often suitable toointerpret user input as-is without client-side processing.</span></span> <span data-ttu-id="0dea0-164">Sorgu işleçleri web arama motorlarından tanıdık destekler.</span><span class="sxs-lookup"><span data-stu-id="0dea0-164">It supports query operators familiar from web search engines.</span></span> <span data-ttu-id="0dea0-165">Merhaba [tam Lucene sorgu dili](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), hangi ayarlayarak alma `queryType=full`, daha fazla işleçler ve joker karakter, benzer gibi sorgu türleri, regex ve alan kapsamlı sorgular için destek ekleyerek hello varsayılan Basit Sorgu Dili genişletir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-165">hello [Full Lucene query language](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), which you get by setting `queryType=full`, extends hello default Simple query language by adding support for more operators and query types like wildcard, fuzzy, regex, and field-scoped queries.</span></span> <span data-ttu-id="0dea0-166">Örneğin, Basit Sorgu söz dizimi gönderilen bir normal ifade bir sorgu dizesi ve bir ifade yorumlanır.</span><span class="sxs-lookup"><span data-stu-id="0dea0-166">For example, a regular expression sent in Simple query syntax would be interpreted as a query string and not an expression.</span></span> <span data-ttu-id="0dea0-167">Bu makalede Hello örnek istek hello tam Lucene sorgu dilini kullanır.</span><span class="sxs-lookup"><span data-stu-id="0dea0-167">hello example request in this article uses hello Full Lucene query language.</span></span>

### <a name="impact-of-searchmode-on-hello-parser"></a><span data-ttu-id="0dea0-168">SearchMode hello ayrıştırıcı üzerindeki etkisi</span><span class="sxs-lookup"><span data-stu-id="0dea0-168">Impact of searchMode on hello parser</span></span> 

<span data-ttu-id="0dea0-169">Ayrıştırma etkileyen başka bir arama isteği hello parametredir `searchMode` parametresi.</span><span class="sxs-lookup"><span data-stu-id="0dea0-169">Another search request parameter that affects parsing is hello `searchMode` parameter.</span></span> <span data-ttu-id="0dea0-170">Boole sorgular için varsayılan işleç hello denetler: herhangi bir (varsayılan) veya tüm.</span><span class="sxs-lookup"><span data-stu-id="0dea0-170">It controls hello default operator for Boolean queries: any (default) or all.</span></span>  

<span data-ttu-id="0dea0-171">Zaman `searchMode=any`, hello varsayılan, hello alanı bölücüyü spacious ve air-condition veya (`||`), hello örnek sorgu metni eşdeğer yapma:</span><span class="sxs-lookup"><span data-stu-id="0dea0-171">When `searchMode=any`, which is hello default, hello space delimiter between spacious and air-condition is OR (`||`), making hello sample query text equivalent to:</span></span> 

~~~~
Spacious,||air-condition*+"Ocean view" 
~~~~

<span data-ttu-id="0dea0-172">Açık işleçleri gibi `+` içinde `+"Ocean view"`, boolean sorgu yapısında anlaşılır olan (Merhaba terim *gerekir* eşleşen).</span><span class="sxs-lookup"><span data-stu-id="0dea0-172">Explicit operators, such as `+` in `+"Ocean view"`, are unambiguous in boolean query construction (hello term *must* match).</span></span> <span data-ttu-id="0dea0-173">Kalan toointerpret hello nasıl koşulları daha az açıktır: spacious ve air-condition.</span><span class="sxs-lookup"><span data-stu-id="0dea0-173">Less obvious is how toointerpret hello remaining terms: spacious and air-condition.</span></span> <span data-ttu-id="0dea0-174">Merhaba arama motoru Okyanusu görünümünde eşleşen bulmalısınız *ve* spacious *ve* air-condition?</span><span class="sxs-lookup"><span data-stu-id="0dea0-174">Should hello search engine find matches on ocean view *and* spacious *and* air-condition?</span></span> <span data-ttu-id="0dea0-175">Veya Okyanusu görünüm bulmalısınız artı *herhangi birini* koşulları kalan Merhaba?</span><span class="sxs-lookup"><span data-stu-id="0dea0-175">Or should it find ocean view plus *either one* of hello remaining terms?</span></span> 

<span data-ttu-id="0dea0-176">Varsayılan olarak (`searchMode=any`), hello arama motoru hello daha geniş yorumlama varsayar.</span><span class="sxs-lookup"><span data-stu-id="0dea0-176">By default (`searchMode=any`), hello search engine assumes hello broader interpretation.</span></span> <span data-ttu-id="0dea0-177">Her iki alan *gereken* eşleştirilmesi, yansıtma "veya" semantiği.</span><span class="sxs-lookup"><span data-stu-id="0dea0-177">Either field *should* be matched, reflecting "or" semantics.</span></span> <span data-ttu-id="0dea0-178">Hello ilk sorgu ağaç daha önce iki işlem, "gerekir" gösterir hello varsayılan hello ile gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-178">hello initial query tree illustrated previously, with hello two "should" operations, shows hello default.</span></span>  

<span data-ttu-id="0dea0-179">Şimdi ayarlarız varsayalım `searchMode=all`.</span><span class="sxs-lookup"><span data-stu-id="0dea0-179">Suppose that we now set `searchMode=all`.</span></span> <span data-ttu-id="0dea0-180">Bu durumda, hello alanı "ve" bir işlem olarak yorumlanır.</span><span class="sxs-lookup"><span data-stu-id="0dea0-180">In this case, hello space is interpreted as an "and" operation.</span></span> <span data-ttu-id="0dea0-181">Her hello kalan terimlerin her ikisi de bir eşleşme olarak hello belge tooqualify mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-181">Each of hello remaining terms must both be present in hello document tooqualify as a match.</span></span> <span data-ttu-id="0dea0-182">Merhaba sonuçta elde edilen örnek sorgu şu şekilde yorumlanacağını:</span><span class="sxs-lookup"><span data-stu-id="0dea0-182">hello resulting sample query would be interpreted as follows:</span></span> 

~~~~
+Spacious,+air-condition*+"Ocean view"  
~~~~

<span data-ttu-id="0dea0-183">Bu sorgu için değiştirilmiş sorgu ağacı eşleşen belgenin tüm üç alt sorgulara hello kesişimi olduğu aşağıdaki gibi olur:</span><span class="sxs-lookup"><span data-stu-id="0dea0-183">A modified query tree for this query would be as follows, where a matching document is hello intersection of all three subqueries:</span></span> 

 ![Boole Sorgusu searchmode tüm][3]

> [!Note] 
> <span data-ttu-id="0dea0-185">Seçme `searchMode=any` üzerinden `searchMode=all` en iyi kararı temsilcisi sorguları çalıştırarak gelen değil.</span><span class="sxs-lookup"><span data-stu-id="0dea0-185">Choosing `searchMode=any` over `searchMode=all` is a decision best arrived at by running representative queries.</span></span> <span data-ttu-id="0dea0-186">Büyük olasılıkla tooinclude işleçleri (arama belge depoladığında ortak) olan kullanıcıların sonuçlarını daha sezgisel, bulabileceğiniz `searchMode=all` boolean sorgu yapıları bildirir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-186">Users who are likely tooinclude operators (common when searching document stores) might find results more intuitive if `searchMode=all` informs boolean query constructs.</span></span> <span data-ttu-id="0dea0-187">Merhaba Interplay arasında hakkında daha fazla bilgi için `searchMode` ve işleçleri [Basit Sorgu söz dizimi](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).</span><span class="sxs-lookup"><span data-stu-id="0dea0-187">For more about hello interplay between `searchMode` and operators, see [Simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).</span></span>

<a name="stage2"></a>
## <a name="stage-2-lexical-analysis"></a><span data-ttu-id="0dea0-188">2. Aşama: Sözcük çözümleme</span><span class="sxs-lookup"><span data-stu-id="0dea0-188">Stage 2: Lexical analysis</span></span> 

<span data-ttu-id="0dea0-189">Sözcük çözümleyiciler işlem *terim sorguları* ve *tümcecik sorguları* hello sorgu ağaç yapılandırılmış sonra.</span><span class="sxs-lookup"><span data-stu-id="0dea0-189">Lexical analyzers process *term queries* and *phrase queries* after hello query tree is structured.</span></span> <span data-ttu-id="0dea0-190">Bir Çözümleyicisi metin girişleri verilen tooit hello ayrıştırıcı tarafından Merhaba, işlemleri metin hello ve sonra geri simgeleştirilmiş gönderir koşulları içine toobe birleştirilmiş sorgu ağaç hello kabul eder.</span><span class="sxs-lookup"><span data-stu-id="0dea0-190">An analyzer accepts hello text inputs given tooit by hello parser, processes hello text, and then sends back tokenized terms toobe incorporated into hello query tree.</span></span> 

<span data-ttu-id="0dea0-191">Merhaba en sık kullanılan sözcük analiz biçimidir *dil analiz* kuralları belirli tooa dil verilen üzerinde temel sorgu terimlerinin dönüştürür:</span><span class="sxs-lookup"><span data-stu-id="0dea0-191">hello most common form of lexical analysis is *linguistic analysis* which transforms query terms based on rules specific tooa given language:</span></span> 

* <span data-ttu-id="0dea0-192">Bir sorgu Terime toohello kök formu bir word'ün azaltma</span><span class="sxs-lookup"><span data-stu-id="0dea0-192">Reducing a query term toohello root form of a word</span></span> 
* <span data-ttu-id="0dea0-193">Gerekli olmayan sözcükler kaldırma ("" gibi bir Durma sözcükleri veya "ve" İngilizce)</span><span class="sxs-lookup"><span data-stu-id="0dea0-193">Removing non-essential words (stopwords, such as "the" or "and" in English)</span></span> 
* <span data-ttu-id="0dea0-194">Bileşen parçalara bileşik bir sözcük bölme</span><span class="sxs-lookup"><span data-stu-id="0dea0-194">Breaking a composite word into component parts</span></span> 
* <span data-ttu-id="0dea0-195">Küçük büyük harf word büyük/küçük harfleri</span><span class="sxs-lookup"><span data-stu-id="0dea0-195">Lower casing an upper case word</span></span> 

<span data-ttu-id="0dea0-196">Bu işlemlerin tümü hello dizininde depolanan hello kullanıcı ve hello koşulları tarafından sağlanan hello metin girişi tooerase farklarını eğilimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-196">All of these operations tend tooerase differences between hello text input provided by hello user and hello terms stored in hello index.</span></span> <span data-ttu-id="0dea0-197">Bu tür işlemler metin işleme ötesine gidin ve hello dilinin kendisini kapsamlı bilgi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-197">Such operations go beyond text processing and require in-depth knowledge of hello language itself.</span></span> <span data-ttu-id="0dea0-198">tooadd dil tanıma, Azure Search bu katmanını destekler uzun bir listesi [dil Çözümleyicileri](https://docs.microsoft.com/rest/api/searchservice/language-support) Lucene ve Microsoft tarafından.</span><span class="sxs-lookup"><span data-stu-id="0dea0-198">tooadd this layer of linguistic awareness, Azure Search supports a long list of [language analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support) from both Lucene and Microsoft.</span></span>

> [!Note]
> <span data-ttu-id="0dea0-199">Analiz gereksinimleri en az tooelaborate senaryonuza bağlı olarak değişebilir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-199">Analysis requirements can range from minimal tooelaborate depending on your scenario.</span></span> <span data-ttu-id="0dea0-200">Önceden tanımlanmış hello çözümleyiciler birini seçerek hello veya kendi oluşturarak sözcük analiz karmaşıklığını denetleyebilirsiniz [özel Çözümleyicisi](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="0dea0-200">You can control complexity of lexical analysis by hello selecting one of hello predefined analyzers or by creating your own [custom analyzer](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search).</span></span> <span data-ttu-id="0dea0-201">Çözümleyiciler kapsamlı toosearchable alanlar ve alan tanımının bir parçası belirtilir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-201">Analyzers are scoped toosearchable fields and are specified as part of a field definition.</span></span> <span data-ttu-id="0dea0-202">Bu, toovary sözcük analiz bir alan başına temelinde sağlar.</span><span class="sxs-lookup"><span data-stu-id="0dea0-202">This allows you toovary lexical analysis on a per-field basis.</span></span> <span data-ttu-id="0dea0-203">Belirtilmezse, hello *standart* Lucene Çözümleyicisi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0dea0-203">Unspecified, hello *standard* Lucene analyzer is used.</span></span>

<span data-ttu-id="0dea0-204">Örneğimizde, önceki tooanalysis hello ilk sorgu ağacı hello terimi "bir büyük harf"S"ile" Spacious sahiptir ve sorgu ayrıştırıcı hello virgül (virgül bir sorgu dili işleci sayılmaz) hello sorgu Terime bir parçası olarak yorumlar.</span><span class="sxs-lookup"><span data-stu-id="0dea0-204">In our example, prior tooanalysis, hello initial query tree has hello term "Spacious," with an uppercase "S" and a comma that hello query parser interprets as a part of hello query term (a comma is not considered a query language operator).</span></span>  

<span data-ttu-id="0dea0-205">Merhaba varsayılan Çözümleyicisi hello terim işlediğinde, bu "Okyanusu Görünüm" ve "spacious" küçük harf ve hello virgül karakterini kaldırma.</span><span class="sxs-lookup"><span data-stu-id="0dea0-205">When hello default analyzer processes hello term, it will lowercase "ocean view" and "spacious", and remove hello comma character.</span></span> <span data-ttu-id="0dea0-206">Merhaba değiştirilmiş sorgu ağacında aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="0dea0-206">hello modified query tree will look as follows:</span></span> 

 ![Çözümlenen koşullarla Boole Sorgusu][4]

### <a name="testing-analyzer-behaviors"></a><span data-ttu-id="0dea0-208">Test Çözümleyicisi davranışları</span><span class="sxs-lookup"><span data-stu-id="0dea0-208">Testing analyzer behaviors</span></span> 

<span data-ttu-id="0dea0-209">bir Çözümleyicisi Hello davranışını hello kullanarak test edilmiş [analiz API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer).</span><span class="sxs-lookup"><span data-stu-id="0dea0-209">hello behavior of an analyzer can be tested using hello [Analyze API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer).</span></span> <span data-ttu-id="0dea0-210">Merhaba metin tooanalyze toosee Çözümleyicisi verilen hangi koşulları oluşturacak istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="0dea0-210">Provide hello text you want tooanalyze toosee what terms given analyzer will generate.</span></span> <span data-ttu-id="0dea0-211">Örneğin, hello standart Çözümleyicisi işleminin nasıl toosee hello "metni air-condition", istek aşağıdaki hello gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0dea0-211">For example, toosee how hello standard analyzer would process hello text "air-condition", you can issue hello following request:</span></span>

~~~~
{ 
    "text": "air-condition",
    "analyzer": "standard"
}
~~~~

<span data-ttu-id="0dea0-212">Merhaba standart Çözümleyicisi iki belirteçleri, bunları konumlarını (tümcecik eşleştirmek için kullanılır) yanı sıra başlangıç ve bitiş kaydırmalar (isabet vurgulama için kullanılan) gibi özniteliklerle yorumlama aşağıdaki hello içine hello giriş metni keser:</span><span class="sxs-lookup"><span data-stu-id="0dea0-212">hello standard analyzer breaks hello input text into hello following two tokens, annotating them with attributes like start and end offsets (used for hit highlighting) as well as their position (used for phrase matching):</span></span>

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

### <a name="exceptions-toolexical-analysis"></a><span data-ttu-id="0dea0-213">Özel durumlar toolexical çözümleme</span><span class="sxs-lookup"><span data-stu-id="0dea0-213">Exceptions toolexical analysis</span></span> 

<span data-ttu-id="0dea0-214">Sözcük analiz tüm koşullar – bir terim sorgu veya tümcecik sorgusu gerektiren tooquery türleri geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-214">Lexical analysis applies only tooquery types that require complete terms – either a term query or a phrase query.</span></span> <span data-ttu-id="0dea0-215">Tamamlanmamış koşulları – önek sorgu, joker karakter sorgu, regex sorgu – veya tooa benzer sorgu tooquery türleriyle uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="0dea0-215">It doesn’t apply tooquery types with incomplete terms – prefix query, wildcard query, regex query – or tooa fuzzy query.</span></span> <span data-ttu-id="0dea0-216">Bu terim hello önek sorguyla dahil olmak üzere türü, sorgu *air-condition\**  Bizim örneğimizde, doğrudan hello analysis aşaması atlayarak toohello sorgu ağaç eklenir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-216">Those query types, including hello prefix query with term *air-condition\** in our example, are added directly toohello query tree, bypassing hello analysis stage.</span></span> <span data-ttu-id="0dea0-217">Merhaba yalnızca bu türlerde sorgu koşullarını gerçekleştirilen dönüştürmeyi lowercasing.</span><span class="sxs-lookup"><span data-stu-id="0dea0-217">hello only transformation performed on query terms of those types is lowercasing.</span></span>

<a name="stage3"></a>
## <a name="stage-3-document-retrieval"></a><span data-ttu-id="0dea0-218">3. Aşama: Belge alma</span><span class="sxs-lookup"><span data-stu-id="0dea0-218">Stage 3: Document retrieval</span></span> 

<span data-ttu-id="0dea0-219">Belge alma hello dizindeki eşleşen terimleri toofinding belgelerle başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="0dea0-219">Document retrieval refers toofinding documents with matching terms in hello index.</span></span> <span data-ttu-id="0dea0-220">Bu aşama örneği arasında en iyi anlaşılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0dea0-220">This stage is understood best through an example.</span></span> <span data-ttu-id="0dea0-221">Basit şema aşağıdaki hello sahip Oteller diziniyle başlayalım:</span><span class="sxs-lookup"><span data-stu-id="0dea0-221">Let's start with a hotels index having hello following simple schema:</span></span> 

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

<span data-ttu-id="0dea0-222">Daha fazla bu dizini dört belge aşağıdaki hello içeren varsayın:</span><span class="sxs-lookup"><span data-stu-id="0dea0-222">Further assume that this index contains hello following four documents:</span></span> 

~~~~
{ 
    "value": [
        {         
            "id": "1",         
            "title": "Hotel Atman",         
            "description": "Spacious rooms, ocean view, walking distance toohello beach."   
        },       
        {         
            "id": "2",         
            "title": "Beach Resort",        
            "description": "Located on hello north shore of hello island of Kauaʻi. Ocean view."     
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

<span data-ttu-id="0dea0-223">**Koşulları nasıl dizini**</span><span class="sxs-lookup"><span data-stu-id="0dea0-223">**How terms are indexed**</span></span>

<span data-ttu-id="0dea0-224">toounderstand alma tooknow yardımcı dizin oluşturma hakkındaki bazı temel bilgileri.</span><span class="sxs-lookup"><span data-stu-id="0dea0-224">toounderstand retrieval, it helps tooknow a few basics about indexing.</span></span> <span data-ttu-id="0dea0-225">Merhaba depolama ters dizin, aranabilir her alan için bir tane birimidir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-225">hello unit of storage is an inverted index, one for each searchable field.</span></span> <span data-ttu-id="0dea0-226">Ters dizin tüm belgelerden tüm koşulları sıralanmış bir listesidir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-226">Within an inverted index is a sorted list of all terms from all documents.</span></span> <span data-ttu-id="0dea0-227">Her terim bunu, aşağıdaki hello örnekte korumalı oluştuğu belgelerin toohello listesini eşler.</span><span class="sxs-lookup"><span data-stu-id="0dea0-227">Each term maps toohello list of documents in which it occurs, as evident in hello example below.</span></span>

<span data-ttu-id="0dea0-228">tooproduce hello koşulları ters bir dizinde hello arama motoru sözcük analizi belgeleri hello içerik üzerinde benzer toowhat sorgu işleme sırasında olur gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-228">tooproduce hello terms in an inverted index, hello search engine performs lexical analysis over hello content of documents, similar toowhat happens during query processing.</span></span> <span data-ttu-id="0dea0-229">Metin girişleri tooan analyzer, alt ortası noktalama işaretleri ve hello Çözümleyicisi yapılandırmasına bağlı olarak belirli bir benzeri atılmış geçirilir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-229">Text inputs are passed tooan analyzer, lower-cased, stripped of punctuation, and so forth, depending on hello analyzer configuration.</span></span> <span data-ttu-id="0dea0-230">Ortak, ancak gerekli değildir, toouse hello arama ve böylece sorgu terimlerinin hello dizini içinde koşulları gibi daha fazla ara işlemleri dizin oluşturma için aynı Çözümleyicileri.</span><span class="sxs-lookup"><span data-stu-id="0dea0-230">It's common, but not required, toouse hello same analyzers for search and indexing operations so that query terms look more like terms inside hello index.</span></span>

> [!Note]
> <span data-ttu-id="0dea0-231">Azure arama sağlar, dizin oluşturma için farklı çözümleyiciler belirtin ve arama aracılığıyla ek `indexAnalyzer` ve `searchAnalyzer` alan parametreleri.</span><span class="sxs-lookup"><span data-stu-id="0dea0-231">Azure Search lets you specify different analyzers for indexing and search via additional `indexAnalyzer` and `searchAnalyzer` field parameters.</span></span> <span data-ttu-id="0dea0-232">Belirtilmezse, hello ile ayarlamak Çözümleyicisi hello `analyzer` özelliği, hem dizin oluşturma ve arama için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0dea0-232">If unspecified, hello analyzer set with hello `analyzer` property is used for both indexing and searching.</span></span>  

<span data-ttu-id="0dea0-233">**Örnek belgeler için ters dizin**</span><span class="sxs-lookup"><span data-stu-id="0dea0-233">**Inverted index for example documents**</span></span>

<span data-ttu-id="0dea0-234">Tooour örneğin hello döndürme **başlık** alanı, ters çevrilmiş hello dizini şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="0dea0-234">Returning tooour example, for hello **title** field, hello inverted index looks like this:</span></span>

| <span data-ttu-id="0dea0-235">Sözleşme Dönemi</span><span class="sxs-lookup"><span data-stu-id="0dea0-235">Term</span></span> | <span data-ttu-id="0dea0-236">Belge listesi</span><span class="sxs-lookup"><span data-stu-id="0dea0-236">Document list</span></span> |
|------|---------------|
| <span data-ttu-id="0dea0-237">atman</span><span class="sxs-lookup"><span data-stu-id="0dea0-237">atman</span></span> | <span data-ttu-id="0dea0-238">1</span><span class="sxs-lookup"><span data-stu-id="0dea0-238">1</span></span> |
| <span data-ttu-id="0dea0-239">Plaj</span><span class="sxs-lookup"><span data-stu-id="0dea0-239">beach</span></span> | <span data-ttu-id="0dea0-240">2</span><span class="sxs-lookup"><span data-stu-id="0dea0-240">2</span></span> |
| <span data-ttu-id="0dea0-241">Otel</span><span class="sxs-lookup"><span data-stu-id="0dea0-241">hotel</span></span> | <span data-ttu-id="0dea0-242">1, 3</span><span class="sxs-lookup"><span data-stu-id="0dea0-242">1, 3</span></span> |
| <span data-ttu-id="0dea0-243">Okyanusu</span><span class="sxs-lookup"><span data-stu-id="0dea0-243">ocean</span></span> | <span data-ttu-id="0dea0-244">4</span><span class="sxs-lookup"><span data-stu-id="0dea0-244">4</span></span>  |
| <span data-ttu-id="0dea0-245">playa</span><span class="sxs-lookup"><span data-stu-id="0dea0-245">playa</span></span> | <span data-ttu-id="0dea0-246">3</span><span class="sxs-lookup"><span data-stu-id="0dea0-246">3</span></span> |
| <span data-ttu-id="0dea0-247">çare</span><span class="sxs-lookup"><span data-stu-id="0dea0-247">resort</span></span> | <span data-ttu-id="0dea0-248">3</span><span class="sxs-lookup"><span data-stu-id="0dea0-248">3</span></span> |
| <span data-ttu-id="0dea0-249">Retreat</span><span class="sxs-lookup"><span data-stu-id="0dea0-249">retreat</span></span> | <span data-ttu-id="0dea0-250">4</span><span class="sxs-lookup"><span data-stu-id="0dea0-250">4</span></span> |

<span data-ttu-id="0dea0-251">Merhaba başlığı alanında, yalnızca *otel* iki belgelerde görüntülenir: 1, 3.</span><span class="sxs-lookup"><span data-stu-id="0dea0-251">In hello title field, only *hotel* shows up in two documents: 1, 3.</span></span>

<span data-ttu-id="0dea0-252">Hello için **açıklama** alanı, başlangıç dizini aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="0dea0-252">For hello **description** field, hello index is as follows:</span></span>

| <span data-ttu-id="0dea0-253">Sözleşme Dönemi</span><span class="sxs-lookup"><span data-stu-id="0dea0-253">Term</span></span> | <span data-ttu-id="0dea0-254">Belge listesi</span><span class="sxs-lookup"><span data-stu-id="0dea0-254">Document list</span></span> |
|------|---------------|
| <span data-ttu-id="0dea0-255">Hava</span><span class="sxs-lookup"><span data-stu-id="0dea0-255">air</span></span> | <span data-ttu-id="0dea0-256">3</span><span class="sxs-lookup"><span data-stu-id="0dea0-256">3</span></span>
| <span data-ttu-id="0dea0-257">ve</span><span class="sxs-lookup"><span data-stu-id="0dea0-257">and</span></span> | <span data-ttu-id="0dea0-258">4</span><span class="sxs-lookup"><span data-stu-id="0dea0-258">4</span></span>
| <span data-ttu-id="0dea0-259">Plaj</span><span class="sxs-lookup"><span data-stu-id="0dea0-259">beach</span></span> | <span data-ttu-id="0dea0-260">1</span><span class="sxs-lookup"><span data-stu-id="0dea0-260">1</span></span>
| <span data-ttu-id="0dea0-261">söylediğinizde</span><span class="sxs-lookup"><span data-stu-id="0dea0-261">conditioned</span></span> | <span data-ttu-id="0dea0-262">3</span><span class="sxs-lookup"><span data-stu-id="0dea0-262">3</span></span>
| <span data-ttu-id="0dea0-263">rahat</span><span class="sxs-lookup"><span data-stu-id="0dea0-263">comfortable</span></span> | <span data-ttu-id="0dea0-264">3</span><span class="sxs-lookup"><span data-stu-id="0dea0-264">3</span></span>
| <span data-ttu-id="0dea0-265">uzaklık</span><span class="sxs-lookup"><span data-stu-id="0dea0-265">distance</span></span> | <span data-ttu-id="0dea0-266">1</span><span class="sxs-lookup"><span data-stu-id="0dea0-266">1</span></span>
| <span data-ttu-id="0dea0-267">Adası</span><span class="sxs-lookup"><span data-stu-id="0dea0-267">island</span></span> | <span data-ttu-id="0dea0-268">2</span><span class="sxs-lookup"><span data-stu-id="0dea0-268">2</span></span>
| <span data-ttu-id="0dea0-269">kauaʻi</span><span class="sxs-lookup"><span data-stu-id="0dea0-269">kauaʻi</span></span> | <span data-ttu-id="0dea0-270">2</span><span class="sxs-lookup"><span data-stu-id="0dea0-270">2</span></span>
| <span data-ttu-id="0dea0-271">bulunan</span><span class="sxs-lookup"><span data-stu-id="0dea0-271">located</span></span> | <span data-ttu-id="0dea0-272">2</span><span class="sxs-lookup"><span data-stu-id="0dea0-272">2</span></span>
| <span data-ttu-id="0dea0-273">Kuzey</span><span class="sxs-lookup"><span data-stu-id="0dea0-273">north</span></span> | <span data-ttu-id="0dea0-274">2</span><span class="sxs-lookup"><span data-stu-id="0dea0-274">2</span></span>
| <span data-ttu-id="0dea0-275">Okyanusu</span><span class="sxs-lookup"><span data-stu-id="0dea0-275">ocean</span></span> | <span data-ttu-id="0dea0-276">1, 2, 3</span><span class="sxs-lookup"><span data-stu-id="0dea0-276">1, 2, 3</span></span>
| <span data-ttu-id="0dea0-277">/</span><span class="sxs-lookup"><span data-stu-id="0dea0-277">of</span></span> | <span data-ttu-id="0dea0-278">2</span><span class="sxs-lookup"><span data-stu-id="0dea0-278">2</span></span>
| <span data-ttu-id="0dea0-279">üzerinde</span><span class="sxs-lookup"><span data-stu-id="0dea0-279">on</span></span> |<span data-ttu-id="0dea0-280">2</span><span class="sxs-lookup"><span data-stu-id="0dea0-280">2</span></span>
| <span data-ttu-id="0dea0-281">Sessiz</span><span class="sxs-lookup"><span data-stu-id="0dea0-281">quiet</span></span> | <span data-ttu-id="0dea0-282">4</span><span class="sxs-lookup"><span data-stu-id="0dea0-282">4</span></span>
| <span data-ttu-id="0dea0-283">odaları</span><span class="sxs-lookup"><span data-stu-id="0dea0-283">rooms</span></span>  | <span data-ttu-id="0dea0-284">1, 3</span><span class="sxs-lookup"><span data-stu-id="0dea0-284">1, 3</span></span>
| <span data-ttu-id="0dea0-285">secluded</span><span class="sxs-lookup"><span data-stu-id="0dea0-285">secluded</span></span> | <span data-ttu-id="0dea0-286">4</span><span class="sxs-lookup"><span data-stu-id="0dea0-286">4</span></span>
| <span data-ttu-id="0dea0-287">Deniz Kıyısı</span><span class="sxs-lookup"><span data-stu-id="0dea0-287">shore</span></span> | <span data-ttu-id="0dea0-288">2</span><span class="sxs-lookup"><span data-stu-id="0dea0-288">2</span></span>
| <span data-ttu-id="0dea0-289">spacious</span><span class="sxs-lookup"><span data-stu-id="0dea0-289">spacious</span></span> | <span data-ttu-id="0dea0-290">1</span><span class="sxs-lookup"><span data-stu-id="0dea0-290">1</span></span>
| <span data-ttu-id="0dea0-291">Merhaba</span><span class="sxs-lookup"><span data-stu-id="0dea0-291">hello</span></span> | <span data-ttu-id="0dea0-292">1, 2</span><span class="sxs-lookup"><span data-stu-id="0dea0-292">1, 2</span></span>
| <span data-ttu-id="0dea0-293">çok</span><span class="sxs-lookup"><span data-stu-id="0dea0-293">too</span></span>| <span data-ttu-id="0dea0-294">1</span><span class="sxs-lookup"><span data-stu-id="0dea0-294">1</span></span>
| <span data-ttu-id="0dea0-295">görünüm</span><span class="sxs-lookup"><span data-stu-id="0dea0-295">view</span></span> | <span data-ttu-id="0dea0-296">1, 2, 3</span><span class="sxs-lookup"><span data-stu-id="0dea0-296">1, 2, 3</span></span>
| <span data-ttu-id="0dea0-297">taramasını</span><span class="sxs-lookup"><span data-stu-id="0dea0-297">walking</span></span> | <span data-ttu-id="0dea0-298">1</span><span class="sxs-lookup"><span data-stu-id="0dea0-298">1</span></span>
| <span data-ttu-id="0dea0-299">İle</span><span class="sxs-lookup"><span data-stu-id="0dea0-299">with</span></span> | <span data-ttu-id="0dea0-300">3</span><span class="sxs-lookup"><span data-stu-id="0dea0-300">3</span></span>


<span data-ttu-id="0dea0-301">**Dizinli koşulları karşı sorgu terimlerinin eşleştirme**</span><span class="sxs-lookup"><span data-stu-id="0dea0-301">**Matching query terms against indexed terms**</span></span>

<span data-ttu-id="0dea0-302">Şimdi dönmek toohello örnek sorgu ters hello dizinlerini yukarıdaki verildiğinde ve nasıl eşleşen belgeleri görmek için bizim örnek sorgu bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="0dea0-302">Given hello inverted indices above, let’s return toohello sample query and see how matching documents are found for our example query.</span></span> <span data-ttu-id="0dea0-303">Geri çağırma hello son sorgu ağacı şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="0dea0-303">Recall that hello final query tree looks like this:</span></span> 

 ![Çözümlenen koşullarla Boole Sorgusu][4]

<span data-ttu-id="0dea0-305">Sorgu yürütme sırasında tek tek sorguları hello aranabilir alanlara karşı bağımsız olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="0dea0-305">During query execution, individual queries are executed against hello searchable fields independently.</span></span> 

+ <span data-ttu-id="0dea0-306">Merhaba TermQuery "spacious" eşleşen 1 (otel Atman) belgesi.</span><span class="sxs-lookup"><span data-stu-id="0dea0-306">hello TermQuery, "spacious", matches document 1 (Hotel Atman).</span></span> 

+ <span data-ttu-id="0dea0-307">Merhaba PrefixQuery, "air-condition *", herhangi bir belgeniz eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="0dea0-307">hello PrefixQuery, "air-condition*", doesn't match any documents.</span></span> 

  <span data-ttu-id="0dea0-308">Bazen geliştiriciler kafasını karıştırabilirler bir davranış budur.</span><span class="sxs-lookup"><span data-stu-id="0dea0-308">This is a behavior that sometimes confuses developers.</span></span> <span data-ttu-id="0dea0-309">Merhaba terim Air-conditioned hello belgede var ancak iki terimleri hello varsayılan Çözümleyicisi tarafından ayrılır.</span><span class="sxs-lookup"><span data-stu-id="0dea0-309">Although hello term air-conditioned exists in hello document, it is split into two terms by hello default analyzer.</span></span> <span data-ttu-id="0dea0-310">Kısmi terimleri içeren, önek sorguları çözümlenmediğini geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="0dea0-310">Recall that prefix queries, which contain partial terms, are not analyzed.</span></span> <span data-ttu-id="0dea0-311">Bu nedenle "air-condition" hello aranır önek şartlarını dizin ters ve bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="0dea0-311">Therefore terms with prefix "air-condition" are looked up in hello inverted index and not found.</span></span>

+ <span data-ttu-id="0dea0-312">Merhaba PhraseQuery "Okyanusu Görünüm" Merhaba koşulları "Okyanusu" ve "Görünüm" arar ve hello yakınlık hello özgün belgede koşulları denetler.</span><span class="sxs-lookup"><span data-stu-id="0dea0-312">hello PhraseQuery, "ocean view", looks up hello terms "ocean" and "view" and checks hello proximity of terms in hello original document.</span></span> <span data-ttu-id="0dea0-313">Belgeleri 1, 2 ve 3 Bu sorguyu hello açıklama alanı eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="0dea0-313">Documents 1, 2 and 3 match this query in hello description field.</span></span> <span data-ttu-id="0dea0-314">Bildirim belgesi 4 hello terim Okyanusu hello başlığında olsa da hello "Okyanusu Görünüm" tümceciği için tek sözcük yerine bekliyoruz gibi bir eşleşme olarak kabul değil.</span><span class="sxs-lookup"><span data-stu-id="0dea0-314">Notice document 4 has hello term ocean in hello title but isn’t considered a match, as we're looking for hello "ocean view" phrase rather than individual words.</span></span> 

> [!Note]
> <span data-ttu-id="0dea0-315">Bir arama sorgusu bağımsız olarak Azure arama dizini hello alanlar ile Merhaba kümesine sınırlamak sürece hello tüm aranabilir alanları karşı yürütülebilir `searchFields` hello örnek arama isteğinde gösterildiği gibi parametre.</span><span class="sxs-lookup"><span data-stu-id="0dea0-315">A search query is executed independently against all searchable fields in hello Azure Search index unless you limit hello fields set with hello `searchFields` parameter, as illustrated in hello example search request.</span></span> <span data-ttu-id="0dea0-316">Seçili hello alanların hiçbirini eşleşen belgeleri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="0dea0-316">Documents that match in any of hello selected fields are returned.</span></span> 

<span data-ttu-id="0dea0-317">Söz konusu hello sorgu için tüm Hello üzerinde eşleşen hello belgelerdir 1, 2, 3.</span><span class="sxs-lookup"><span data-stu-id="0dea0-317">On hello whole, for hello query in question, hello documents that match are 1, 2, 3.</span></span> 

## <a name="stage-4-scoring"></a><span data-ttu-id="0dea0-318">4. Aşama: Puanlama</span><span class="sxs-lookup"><span data-stu-id="0dea0-318">Stage 4: Scoring</span></span>  

<span data-ttu-id="0dea0-319">Her belge arama sonuç kümesinde bir ilgi puan atanır.</span><span class="sxs-lookup"><span data-stu-id="0dea0-319">Every document in a search result set is assigned a relevance score.</span></span> <span data-ttu-id="0dea0-320">Merhaba hello ilgi puanının toorank hello arama sorgusu ifade edilen en iyi bir kullanıcı yanıt bu belgeleri soru daha yüksek işlevdir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-320">hello function of hello relevance score is toorank higher those documents that best answer a user question as expressed by hello search query.</span></span> <span data-ttu-id="0dea0-321">Merhaba puan eşleşen koşulları istatistiksel özelliklerini göre hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="0dea0-321">hello score is computed based on statistical properties of terms that matched.</span></span> <span data-ttu-id="0dea0-322">Formül Puanlama hello çekirdek Hello olan [TF/IDF (terim sıklığı ters belge sıklığı)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).</span><span class="sxs-lookup"><span data-stu-id="0dea0-322">At hello core of hello scoring formula is [TF/IDF (term frequency-inverse document frequency)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).</span></span> <span data-ttu-id="0dea0-323">Nadir ve sık kullanılan terimleri içeren sorgularda TF/IDF hello nadir terimi içeren sonuçları yükseltir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-323">In queries containing rare and common terms, TF/IDF promotes results containing hello rare term.</span></span> <span data-ttu-id="0dea0-324">Örneğin, tüm Wikipedia makalelerde kuramsal bir dizinde eşleşen hello sorgu belgelerini *hello Başkanı*, üzerinde eşleşen belgeler *Başkanı* daha ilgili olarak kabul edilir üzerinde eşleşen belgeler **.</span><span class="sxs-lookup"><span data-stu-id="0dea0-324">For example, in a hypothetical index with all Wikipedia articles, from documents that matched hello query *hello president*, documents matching on *president* are considered more relevant than documents matching on *the*.</span></span>


### <a name="scoring-example"></a><span data-ttu-id="0dea0-325">Puanlama örneği</span><span class="sxs-lookup"><span data-stu-id="0dea0-325">Scoring example</span></span>

<span data-ttu-id="0dea0-326">Geri çağırma hello bizim örnek sorgu eşleşen üç belgeler:</span><span class="sxs-lookup"><span data-stu-id="0dea0-326">Recall hello three documents that matched our example query:</span></span>
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
      "description": "Spacious rooms, ocean view, walking distance toohello beach."
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
      "description": "Located on a cliff on hello north shore of hello island of Kauai. Ocean view."
    }
  ]
}
~~~~

<span data-ttu-id="0dea0-327">Her ikisi de hello çünkü 1 eşleşen hello sorgu en iyi belge terim *spacious* ve hello gerekli deyimi *Okyanusu Görünüm* hello Açıklama alanına oluşur.</span><span class="sxs-lookup"><span data-stu-id="0dea0-327">Document 1 matched hello query best because both hello term *spacious* and hello required phrase *ocean view* occur in hello description field.</span></span> <span data-ttu-id="0dea0-328">Merhaba sonraki iki belgeleri yalnızca hello tümcecik eşleşen *Okyanusu Görünüm*.</span><span class="sxs-lookup"><span data-stu-id="0dea0-328">hello next two documents match only hello phrase *ocean view*.</span></span> <span data-ttu-id="0dea0-329">Merhaba hello sorguda eşleşen olsa bile belge 2 ve 3 farklı olduğu için o hello ilgi puan önler aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="0dea0-329">It might be surprising that hello relevance score for document 2 and 3 is different even though they matched hello query in hello same way.</span></span> <span data-ttu-id="0dea0-330">Formül Puanlama hello yalnızca TF/IDF'den daha fazla bileşenlere sahip olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="0dea0-330">It's because hello scoring formula has more components than just TF/IDF.</span></span> <span data-ttu-id="0dea0-331">Bu durumda, belge 3 açıklamasını kısa olduğundan biraz daha yüksek bir puan atanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0dea0-331">In this case, document 3 was assigned a slightly higher score because its description is shorter.</span></span> <span data-ttu-id="0dea0-332">Hakkında bilgi edinin [Lucene'nın pratik Puanlama formülü](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) alan uzunluğu ve diğer etkenlere bağlı nasıl etkileyeceğini toounderstand hello ilgi puanı.</span><span class="sxs-lookup"><span data-stu-id="0dea0-332">Learn about [Lucene's Practical Scoring Formula](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) toounderstand how field length and other factors can influence hello relevance score.</span></span>

<span data-ttu-id="0dea0-333">Bazı sorgu türü (joker karakter öneki, regex) her zaman sabit bir puan katkıda toohello genel belge puanı.</span><span class="sxs-lookup"><span data-stu-id="0dea0-333">Some query types (wildcard, prefix, regex) always contribute a constant score toohello overall document score.</span></span> <span data-ttu-id="0dea0-334">Bu sorgu genişletme toobe hello sonuçlarında ancak hello derecelendirme etkilemeden dahil aracılığıyla bulunan eşleşmeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="0dea0-334">This allows matches found through query expansion toobe included in hello results, but without affecting hello ranking.</span></span> 

<span data-ttu-id="0dea0-335">Bu önemli neden bir örnek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-335">An example illustrates why this matters.</span></span> <span data-ttu-id="0dea0-336">Merhaba giriş olası eşleşmeleri ile kısmi dize çok fazla sayıda farklı koşulları üzerinde olduğundan önek aramaları da dahil olmak üzere, joker karakter aramaları tanımına göre belirsiz (girişi "tur *", "tur üzerinde", "tourettes" bulunan eşleşmeler göz önünde bulundurun, ve " tourmaline").</span><span class="sxs-lookup"><span data-stu-id="0dea0-336">Wildcard searches, including prefix searches, are ambiguous by definition because hello input is a partial string with potential matches on a very large number of disparate terms (consider an input of "tour*", with matches found on “tours”, “tourettes”, and “tourmaline”).</span></span> <span data-ttu-id="0dea0-337">Bu sonuçları Hello yapısını verildiğinde, hangi koşulları diğerlerinden daha değerli tooreasonably Infer yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="0dea0-337">Given hello nature of these results, there is no way tooreasonably infer which terms are more valuable than others.</span></span> <span data-ttu-id="0dea0-338">Bu nedenle, biz terim sıklıklarını sonuçları türleri joker karakter, önek ve regex sorgularda Puanlama zaman yoksay.</span><span class="sxs-lookup"><span data-stu-id="0dea0-338">For this reason, we ignore term frequencies when scoring results in queries of types wildcard, prefix and regex.</span></span> <span data-ttu-id="0dea0-339">Bir sabit ile birleştirilmiş kısmi ve tam koşulları içeren bir çok parçalı arama isteğinde hello kısmi giriş sonuçlarından puan tooavoid sapması büyük olasılıkla beklenmeyen eşleşmeleri bulunun.</span><span class="sxs-lookup"><span data-stu-id="0dea0-339">In a multi-part search request that includes partial and complete terms, results from hello partial input are incorporated with a constant score tooavoid bias towards potentially unexpected matches.</span></span>

### <a name="score-tuning"></a><span data-ttu-id="0dea0-340">Puan ayarlama</span><span class="sxs-lookup"><span data-stu-id="0dea0-340">Score tuning</span></span>

<span data-ttu-id="0dea0-341">Azure Search'te tootune ilgi puanları iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="0dea0-341">There are two ways tootune relevance scores in Azure Search:</span></span>

1. <span data-ttu-id="0dea0-342">**Profilleri Puanlama** bir dizi kurala göre sonuçları derece hello listesi belgelerde Yükselt.</span><span class="sxs-lookup"><span data-stu-id="0dea0-342">**Scoring profiles** promote documents in hello ranked list of results based on a set of rules.</span></span> <span data-ttu-id="0dea0-343">Bizim örneğimizde, biz hello başlığı alanında hello Açıklama alanına eşleşen belgeleri daha ilgili eşleşen belgeleri düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dea0-343">In our example, we could consider documents that matched in hello title field more relevant than documents that matched in hello description field.</span></span> <span data-ttu-id="0dea0-344">Ayrıca, dizinimizi her otel için bir fiyat alan olsaydı, biz alt fiyat belgelerle yükseltmek.</span><span class="sxs-lookup"><span data-stu-id="0dea0-344">Additionally, if our index had a price field for each hotel, we could promote documents with lower price.</span></span> <span data-ttu-id="0dea0-345">Daha fazla bilgi edinin nasıl çok[Puanlama profilleri tooa arama dizini ekleyin.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)</span><span class="sxs-lookup"><span data-stu-id="0dea0-345">Learn more how too[add Scoring Profiles tooa search index.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)</span></span>
2. <span data-ttu-id="0dea0-346">**Terim** (yalnızca kullanılabilir hello tam Lucene sorgu söz dizimi) artırma işleci sağlar `^` , olabilir uygulanan tooany hello sorgu ağacının bir parçası.</span><span class="sxs-lookup"><span data-stu-id="0dea0-346">**Term boosting** (available only in hello Full Lucene query syntax) provides a boosting operator `^` that can be applied tooany part of hello query tree.</span></span> <span data-ttu-id="0dea0-347">Merhaba ön ekini temel arama yerine örneğimizde *air-condition*\*, bir ya da hello tam dönem için arama *air-condition* veya hello önek ancak hello tam eşleşen belgeleri Terim derece yüksek artırma toohello terim sorgu uygulayarak: *hava durumu ^ 2 || Air-Condition**.</span><span class="sxs-lookup"><span data-stu-id="0dea0-347">In our example, instead of searching on hello prefix *air-condition*\*, one could search for either hello exact term *air-condition* or hello prefix, but documents that match on hello exact term are ranked higher by applying boost toohello term query: *air-condition^2||air-condition**.</span></span> <span data-ttu-id="0dea0-348">Daha fazla bilgi edinmek [terim](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).</span><span class="sxs-lookup"><span data-stu-id="0dea0-348">Learn more about [term boosting](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).</span></span>


### <a name="scoring-in-a-distributed-index"></a><span data-ttu-id="0dea0-349">Dağıtılmış bir dizinde Puanlama</span><span class="sxs-lookup"><span data-stu-id="0dea0-349">Scoring in a distributed index</span></span>

<span data-ttu-id="0dea0-350">Azure Search'te tüm dizinleri otomatik olarak olan birden fazla parça bölme, birden çok arasında hello dizin dağıtmak bize tooquickly izin vererek düğümleri hizmet ölçek sırasında yukarı veya ölçeklendirmeyi azaltın.</span><span class="sxs-lookup"><span data-stu-id="0dea0-350">All indexes in Azure Search are automatically split into multiple shards, allowing us tooquickly distribute hello index among multiple nodes during service scale up or scale down.</span></span> <span data-ttu-id="0dea0-351">Bir arama isteğine verildiğinde, her parça karşı bağımsız olarak verilir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-351">When a search request is issued, it’s issued against each shard independently.</span></span> <span data-ttu-id="0dea0-352">Merhaba her parça sonuçlarından ardından birleştirilmiş ve (diğer sıralamaya tanımlanmışsa) puana göre sıralanmış.</span><span class="sxs-lookup"><span data-stu-id="0dea0-352">hello results from each shard are then merged and ordered by score (if no other ordering is defined).</span></span> <span data-ttu-id="0dea0-353">Puanlama işlevi ağırlıkları sorgu Terime sıklığı hello parça, tüm belgelerde ters belge sıklığının karşı değil tüm parça hello önemli tooknow kadar!</span><span class="sxs-lookup"><span data-stu-id="0dea0-353">It is important tooknow that hello scoring function weights query term frequency against its inverse document frequency in all documents within hello shard, not across all shards!</span></span>

<span data-ttu-id="0dea0-354">Bu bir ilgi puan anlamına gelir *verebilir* üzerinde farklı parça bulunuyorsa aynı belgeler için farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-354">This means a relevance score *could* be different for identical documents if they reside on different shards.</span></span> <span data-ttu-id="0dea0-355">Neyse ki, bu farklara toomore bile terim dağıtım hello dizin belgelerde Hello sayısı arttıkça toodisappear eğilimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-355">Fortunately, such differences tend toodisappear as hello number of documents in hello index grows due toomore even term distribution.</span></span> <span data-ttu-id="0dea0-356">Belirli bir belge üzerinde hangi parça yerleştirilecek olası tooassume değil.</span><span class="sxs-lookup"><span data-stu-id="0dea0-356">It’s not possible tooassume on which shard any given document will be placed.</span></span> <span data-ttu-id="0dea0-357">Ancak, bir belge anahtarı değiştirmez varsayıldığında, bu her zaman toohello atanacak aynı parça.</span><span class="sxs-lookup"><span data-stu-id="0dea0-357">However, assuming a document key doesn't change, it will always be assigned toohello same shard.</span></span>

<span data-ttu-id="0dea0-358">Genel olarak, belge puan hello sipariş kararlılık önemliyse belgeleri sıralama için en iyi öznitelik değil.</span><span class="sxs-lookup"><span data-stu-id="0dea0-358">In general, document score is not hello best attribute for ordering documents if order stability is important.</span></span> <span data-ttu-id="0dea0-359">Örneğin, iki belgeyle aynı puan verildiğinde, hangisinin görünür hello sonraki çalıştırmalarında ilk garantisi yoktur aynı sorgu.</span><span class="sxs-lookup"><span data-stu-id="0dea0-359">For example, given two document with an identical score, there is no guarantee which one appears first in subsequent runs of hello same query.</span></span> <span data-ttu-id="0dea0-360">Belge puan yalnızca belge ilgi genel bir fikir göreli tooother belgeleri hello sonuç kümesinde vermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-360">Document score should only give a general sense of document relevance relative tooother documents in hello results set.</span></span>

## <a name="conclusion"></a><span data-ttu-id="0dea0-361">Sonuç</span><span class="sxs-lookup"><span data-stu-id="0dea0-361">Conclusion</span></span>

<span data-ttu-id="0dea0-362">Internet arama motorları Hello başarısını tam metin araması için beklentiler özel veriler üzerinde yükseltilmiş.</span><span class="sxs-lookup"><span data-stu-id="0dea0-362">hello success of internet search engines has raised expectations for full text search over private data.</span></span> <span data-ttu-id="0dea0-363">Arama deneyimi neredeyse her türlü için şimdi hello altyapısı toounderstand bizim amacı dahi koşulları yanlış veya tamamlanmamış bekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="0dea0-363">For almost any kind of search experience, we now expect hello engine toounderstand our intent, even when terms are misspelled or incomplete.</span></span> <span data-ttu-id="0dea0-364">Hatta eşdeğer terimler veya hiçbir zaman gerçekte belirtilen eş anlamlıları dayalı eşleşmeler bekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="0dea0-364">We might even expect matches based on near equivalent terms or synonyms that we never actually specified.</span></span>

<span data-ttu-id="0dea0-365">Teknik açıdan, tam metin araması Gelişmiş bir dil analiz ve sistematik bir yaklaşım tooprocessing biçimlendirebilir, genişletin ve sorgu koşulları toodeliver ilgili bir sonuç dönüştürme şekillerde gerektiren yüksek oranda karmaşık bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="0dea0-365">From a technical standpoint, full text search is highly complex, requiring sophisticated linguistic analysis and a systematic approach tooprocessing in ways that distill, expand, and transform query terms toodeliver a relevant result.</span></span> <span data-ttu-id="0dea0-366">Hello devralınmış karmaşıklık göz önüne alındığında, bir sorgu sonucunu hello etkileyen faktörler çok vardır.</span><span class="sxs-lookup"><span data-stu-id="0dea0-366">Given hello inherent complexities, there are a lot of factors that can affect hello outcome of a query.</span></span> <span data-ttu-id="0dea0-367">Bu nedenle, başlangıç saati toounderstand hello tam metin araması mekanikleri yatırım, beklenmeyen sonuçlara aracılığıyla toowork çalışırken somut avantajları sunar.</span><span class="sxs-lookup"><span data-stu-id="0dea0-367">For this reason, investing hello time toounderstand hello mechanics of full text search offers tangible benefits when trying toowork through unexpected results.</span></span>  

<span data-ttu-id="0dea0-368">Bu makalede, Azure Search'ün hello bağlamında tam metin araması incelediniz.</span><span class="sxs-lookup"><span data-stu-id="0dea0-368">This article explored full text search in hello context of Azure Search.</span></span> <span data-ttu-id="0dea0-369">Bu, yeterli arka plan toorecognize olası nedenleri ve çözümlemeleri ortak sorgu sorunları ele almak için sağlar umuyoruz.</span><span class="sxs-lookup"><span data-stu-id="0dea0-369">We hope it gives you sufficient background toorecognize potential causes and resolutions for addressing common query problems.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0dea0-370">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0dea0-370">Next steps</span></span>

+ <span data-ttu-id="0dea0-371">Merhaba örnek dizini oluşturun, farklı sorguları deneyin ve sonuçları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="0dea0-371">Build hello sample index, try out different queries and review results.</span></span> <span data-ttu-id="0dea0-372">Yönergeler için bkz: [oluşturmak ve hello Portalı'nda bir dizin sorgu](search-get-started-portal.md#query-index).</span><span class="sxs-lookup"><span data-stu-id="0dea0-372">For instructions, see [Build and query an index in hello portal](search-get-started-portal.md#query-index).</span></span>

+ <span data-ttu-id="0dea0-373">Merhaba ek sorgu sözdiziminde deneyin [Search belgeleri](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) örnek bölümüne veya [Basit Sorgu söz dizimi](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) hello Portalı'nda arama Gezgini'nde.</span><span class="sxs-lookup"><span data-stu-id="0dea0-373">Try additional query syntax from hello [Search Documents](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) example section or from [Simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) in Search explorer in hello portal.</span></span>

+ <span data-ttu-id="0dea0-374">Gözden geçirme [profilleri Puanlama](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) arama uygulamanızda sıralaması tootune istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="0dea0-374">Review [scoring profiles](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) if you want tootune ranking in your search application.</span></span>

+ <span data-ttu-id="0dea0-375">Bilgi nasıl tooapply [dile özgü sözcük çözümleyiciler](https://docs.microsoft.com/rest/api/searchservice/language-support).</span><span class="sxs-lookup"><span data-stu-id="0dea0-375">Learn how tooapply [language-specific lexical analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support).</span></span>

+ <span data-ttu-id="0dea0-376">[Özel çözümleyiciler yapılandırma](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) en az işleme veya belirli alanları üzerindeki özel işleme için.</span><span class="sxs-lookup"><span data-stu-id="0dea0-376">[Configure custom analyzers](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) for either minimal processing or specialized processing on specific fields.</span></span>

+ <span data-ttu-id="0dea0-377">[Standart ve İngilizce çözümleyiciler karşılaştırmak](http://alice.unearth.ai/)) yana birimi bu demo web sitesinde.</span><span class="sxs-lookup"><span data-stu-id="0dea0-377">[Compare standard and English analyzers](http://alice.unearth.ai/)) side-by-side on this demo web site.</span></span> 

## <a name="see-also"></a><span data-ttu-id="0dea0-378">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="0dea0-378">See also</span></span>

[<span data-ttu-id="0dea0-379">REST API belgelerde arama</span><span class="sxs-lookup"><span data-stu-id="0dea0-379">Search Documents REST API</span></span>](https://docs.microsoft.com/rest/api/searchservice/search-documents)

[<span data-ttu-id="0dea0-380">Basit sorgu söz dizimi</span><span class="sxs-lookup"><span data-stu-id="0dea0-380">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)

[<span data-ttu-id="0dea0-381">Tam Lucene sorgu söz dizimi</span><span class="sxs-lookup"><span data-stu-id="0dea0-381">Full Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

[<span data-ttu-id="0dea0-382">Arama sonuçlarını işleme</span><span class="sxs-lookup"><span data-stu-id="0dea0-382">Handle search results</span></span>](https://docs.microsoft.com/azure/search/search-pagination-page-layout)

<!--Image references-->
[1]: ./media/search-lucene-query-architecture/architecture-diagram2.png
[2]: ./media/search-lucene-query-architecture/azSearch-queryparsing-should2.png
[3]: ./media/search-lucene-query-architecture/azSearch-queryparsing-must2.png
[4]: ./media/search-lucene-query-architecture/azSearch-queryparsing-spacious2.png
