---
title: "Azure Search'te arama sonuçları sayfası nasıl | Microsoft Docs"
description: "Sayfa numaralandırma Azure Search'te, Microsoft Azure üzerinde barındırılan bulut arama hizmeti."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: a0a1d315-8624-4cdf-b38e-ba12569c6fcc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
ms.openlocfilehash: 1054e15a2751c53aad5dbc8054c4cec41102dee9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-page-search-results-in-azure-search"></a><span data-ttu-id="82bb6-103">Azure Arama'da arama sonuçlarını sayfalandırma</span><span class="sxs-lookup"><span data-stu-id="82bb6-103">How to page search results in Azure Search</span></span>
<span data-ttu-id="82bb6-104">Bu makale, toplam sayıları, belge alma, sıralamalar ve gezinti gibi bir arama sonuçları sayfasının standart öğeleri uygulamak için Azure Search Hizmeti REST API kullanma hakkında yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="82bb6-104">This article provides guidance on how to use the Azure Search Service REST API to implement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span></span>

<span data-ttu-id="82bb6-105">Aşağıda belirtilen her durumda, verileri veya arama sonuçları sayfasını bilgileri katkıda sayfasıyla ilgili seçenekleri aracılığıyla belirtilen [arama belge](http://msdn.microsoft.com/library/azure/dn798927.aspx) Azure arama hizmetinize gönderilen istekleri.</span><span class="sxs-lookup"><span data-stu-id="82bb6-105">In every case mentioned below, page-related options that contribute data or information to your search results page are specified through the [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent to your Azure Search Service.</span></span> <span data-ttu-id="82bb6-106">İstekleri GET komutu, yol ve ne istenen hizmet bildirmek sorgu parametreleri ile nasıl yanıt formüle içerir.</span><span class="sxs-lookup"><span data-stu-id="82bb6-106">Requests include a GET command, path, and query parameters that inform the service what is being requested, and how to formulate the response.</span></span>

> [!NOTE]
> <span data-ttu-id="82bb6-107">Geçerli bir istek bir hizmet URL'si ve yol, HTTP fiili gibi öğeleri içerir `api-version`ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="82bb6-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span></span> <span data-ttu-id="82bb6-108">Konuyu uzatmamak amacıyla, yalnızca sayfa numaralandırma için uygun olan söz dizimini vurgulamak için örnekler kırpılır.</span><span class="sxs-lookup"><span data-stu-id="82bb6-108">For brevity, we trimmed the examples to highlight just the syntax that is relevant to pagination.</span></span> <span data-ttu-id="82bb6-109">Lütfen bakın [Azure Search Hizmeti REST API'si](http://msdn.microsoft.com/library/azure/dn798935.aspx) isteği sözdizimi hakkında ayrıntılar için belgelere.</span><span class="sxs-lookup"><span data-stu-id="82bb6-109">Please see the [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span></span>
> 
> 

## <a name="total-hits-and-page-counts"></a><span data-ttu-id="82bb6-110">Toplam İsabet ve sayfa sayıları</span><span class="sxs-lookup"><span data-stu-id="82bb6-110">Total hits and Page Counts</span></span>
<span data-ttu-id="82bb6-111">Bir sorgudan döndürülen sonuç sayısı toplam gösteren ve ardından daha küçük parçalar sonuçları getireceğinden neredeyse tüm arama sayfalar için temel.</span><span class="sxs-lookup"><span data-stu-id="82bb6-111">Showing the total number of results returned from a query, and then returning those results in smaller chunks, is fundamental to virtually all search pages.</span></span>

![][1]

<span data-ttu-id="82bb6-112">Azure Search'te kullandığınız `$count`, `$top`, ve `$skip` bu değer döndürmek için parametreler.</span><span class="sxs-lookup"><span data-stu-id="82bb6-112">In Azure Search, you use the `$count`, `$top`, and `$skip` parameters to return these values.</span></span> <span data-ttu-id="82bb6-113">Aşağıdaki örnek olarak döndürülen toplam isabet sayısı için bir örnek istek gösterir `@OData.count`:</span><span class="sxs-lookup"><span data-stu-id="82bb6-113">The following example shows a sample request for total hits, returned as `@OData.count`:</span></span>

        GET /indexes/onlineCatalog/docs?$count=true

<span data-ttu-id="82bb6-114">Belge 15 gruplarındaki almak ve ayrıca ilk sayfasına başlangıç İsabetli göster:</span><span class="sxs-lookup"><span data-stu-id="82bb6-114">Retrieve documents in groups of 15, and also show the total hits, starting at the first page:</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

<span data-ttu-id="82bb6-115">Sonuçları sayfa numaralandırma, gerektiren her ikisi de `$top` ve `$skip`, burada `$top` bir toplu işlemde döndürmek için kaç tane öğelerini belirtir ve `$skip` atlamak için kaç tane öğelerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="82bb6-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items to return in a batch, and `$skip` specifies how many items to skip.</span></span> <span data-ttu-id="82bb6-116">Aşağıdaki örnekte, her sayfa sonraki 15 öğeleri gösterir artımlı atlar belirttiği `$skip` parametresi.</span><span class="sxs-lookup"><span data-stu-id="82bb6-116">In the following example, each page shows the next 15 items, indicated by the incremental jumps in the `$skip` parameter.</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a><span data-ttu-id="82bb6-117">Düzen</span><span class="sxs-lookup"><span data-stu-id="82bb6-117">Layout</span></span>
<span data-ttu-id="82bb6-118">Arama sonuçları sayfasında, bir küçük resim, alanlarının alt kümesini ve tam ürün sayfasına bir bağlantı göstermek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82bb6-118">On a search results page, you might want to show a thumbnail image, a subset of fields, and a link to a full product page.</span></span>

 ![][2]

<span data-ttu-id="82bb6-119">Azure Search'te kullanacağınız `$select` ve bu deneyimi uygulamak için bir arama komutu.</span><span class="sxs-lookup"><span data-stu-id="82bb6-119">In Azure Search, you would use `$select` and a lookup command to implement this experience.</span></span>

<span data-ttu-id="82bb6-120">Alanların döşeli düzeni için bir alt döndürmek için:</span><span class="sxs-lookup"><span data-stu-id="82bb6-120">To return a subset of fields for a tiled layout:</span></span>

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

<span data-ttu-id="82bb6-121">Görüntüleri ve medya dosyalarını doğrudan aranabilir değildir ve maliyetleri azaltmak için Azure Blob Depolama alanı gibi başka bir depolama Platform depolanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="82bb6-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, to reduce costs.</span></span> <span data-ttu-id="82bb6-122">Dizin ve belgeleri dış içeriği URL adresini depolayan bir alan tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="82bb6-122">In the index and documents, define a field that stores the URL address of the external content.</span></span> <span data-ttu-id="82bb6-123">Daha sonra alan bir görüntü başvuru olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82bb6-123">You can then use the field as an image reference.</span></span> <span data-ttu-id="82bb6-124">Resim URL'si belgede olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="82bb6-124">The URL to the image should be in the document.</span></span>

<span data-ttu-id="82bb6-125">Bir ürün açıklama sayfasına almak için bir **onClick** olay, kullanım [arama belge](http://msdn.microsoft.com/library/azure/dn798929.aspx) almak için belge anahtarında geçirmek için.</span><span class="sxs-lookup"><span data-stu-id="82bb6-125">To retrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) to pass in the key of the document to retrieve.</span></span> <span data-ttu-id="82bb6-126">Anahtarın veri türü `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="82bb6-126">The data type of the key is `Edm.String`.</span></span> <span data-ttu-id="82bb6-127">Bu örnek, *246810*.</span><span class="sxs-lookup"><span data-stu-id="82bb6-127">In this example, it is *246810*.</span></span> 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a><span data-ttu-id="82bb6-128">İlgi, derecelendirme veya fiyat göre sırala</span><span class="sxs-lookup"><span data-stu-id="82bb6-128">Sort by relevance, rating, or price</span></span>
<span data-ttu-id="82bb6-129">Genellikle ilgi için varsayılan sıralama siparişleri ancak böylece müşteriler hızla varolan sonuçları farklı bir sıralama düzeni içinde sırasını yeniden ayarlaması alternatif sıralama siparişleri kullanıma hazır olmak için yaygın bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="82bb6-129">Sort orders often default to relevance, but it's common to make alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span></span>

 ![][3]

<span data-ttu-id="82bb6-130">Azure Search'te sıralama dayanır `$orderby` olarak dizin oluşturulmuş tüm alanlar için ifade`"Sortable": true.`</span><span class="sxs-lookup"><span data-stu-id="82bb6-130">In Azure Search, sorting is based on the `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span></span>

<span data-ttu-id="82bb6-131">İlgi kesinlikle profilleri Puanlama ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="82bb6-131">Relevance is strongly associated with scoring profiles.</span></span> <span data-ttu-id="82bb6-132">Puanlama varsayılan metin analizi ve İstatistikler kullanır daha fazla veya daha güçlü eşleşme belgelerle bir arama terimi giderek daha yüksek puanları ile tüm sonuçları, sipariş derecelendirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82bb6-132">You can use the default scoring, which relies on text analysis and statistics to rank order all results, with higher scores going to documents with more or stronger matches on a search term.</span></span>

<span data-ttu-id="82bb6-133">Alternatif sıralamalar genellikle ilişkili olan **onClick** sıralama düzenini derlemeler bir yönteme geri arama olayları.</span><span class="sxs-lookup"><span data-stu-id="82bb6-133">Alternative sort orders are typically associated with **onClick** events that call back to a method that builds the sort order.</span></span> <span data-ttu-id="82bb6-134">Örneğin, bu sayfa öğesi verilen:</span><span class="sxs-lookup"><span data-stu-id="82bb6-134">For example, given this page element:</span></span>

 ![][4]

<span data-ttu-id="82bb6-135">Seçili sıralama seçeneği giriş olarak kabul eder ve sıralı bir listesi için bu seçeneği ile ilişkili ölçütler döndüren bir yöntem oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="82bb6-135">You would create a method that accepts the selected sort option as input, and returns an ordered list for the criteria associated with that option.</span></span>

 ![][5]

> [!NOTE]
> <span data-ttu-id="82bb6-136">Varsayılan Puanlama birçok senaryo için yeterli olmakla birlikte, bunun yerine özel bir Puanlama profili ilgi alma öneririz.</span><span class="sxs-lookup"><span data-stu-id="82bb6-136">While the default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span></span> <span data-ttu-id="82bb6-137">Özel bir Puanlama profili işinize daha faydalı artırma öğeleri için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="82bb6-137">A custom scoring profile gives you a way to boost items that are more beneficial to your business.</span></span> <span data-ttu-id="82bb6-138">Bkz: [Puanlama profili Ekle](http://msdn.microsoft.com/library/azure/dn798928.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="82bb6-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> 
> 
> 

## <a name="faceted-navigation"></a><span data-ttu-id="82bb6-139">Çok yönlü gezinme</span><span class="sxs-lookup"><span data-stu-id="82bb6-139">Faceted navigation</span></span>
<span data-ttu-id="82bb6-140">Arama gezinti genellikle yan veya bir sayfanın üst kısmında bulunan bir sonuçlar sayfası üzerinde yaygındır.</span><span class="sxs-lookup"><span data-stu-id="82bb6-140">Search navigation is common on a results page, often located at the side or top of a page.</span></span> <span data-ttu-id="82bb6-141">Azure Search'te modellenmiş bir gezinmede önceden tanımlanmış filtrelere göre kendi kendine yönlendirilmiş arama sağlar.</span><span class="sxs-lookup"><span data-stu-id="82bb6-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span></span> <span data-ttu-id="82bb6-142">Bkz: [Azure Search'te modellenmiş bir gezinmede](search-faceted-navigation.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="82bb6-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span></span>

## <a name="filters-at-the-page-level"></a><span data-ttu-id="82bb6-143">Sayfa düzeyinde filtreleri</span><span class="sxs-lookup"><span data-stu-id="82bb6-143">Filters at the page level</span></span>
<span data-ttu-id="82bb6-144">Çözüm tasarımınızın belirli türlerdeki içerik (örneğin, sayfanın en üstünde listelenen bölümleri olan bir çevrimiçi perakende uygulama) için ayrılmış arama sayfalar dahil, bir filtre ifadesi yanında ekleyebilirsiniz bir **onClick** olay makale bir durumda bir sayfayı açın.</span><span class="sxs-lookup"><span data-stu-id="82bb6-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at the top of the page), you can insert a filter expression alongside an **onClick** event to open a page in a prefiltered state.</span></span> 

<span data-ttu-id="82bb6-145">Bir filtre ile veya olmadan arama ifadesi gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82bb6-145">You can send a filter with or without a search expression.</span></span> <span data-ttu-id="82bb6-146">Örneğin, aşağıdaki isteği marka, eşleşen belgeleri döndüren adına filtre uygular.</span><span class="sxs-lookup"><span data-stu-id="82bb6-146">For example, the following request will filter on brand name, returning only those documents that match it.</span></span>

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

<span data-ttu-id="82bb6-147">Bkz: [Search belgeleri (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) hakkında daha fazla bilgi için `$filter` ifadeler.</span><span class="sxs-lookup"><span data-stu-id="82bb6-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="82bb6-148">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="82bb6-148">See Also</span></span>
* [<span data-ttu-id="82bb6-149">Azure Search Hizmeti REST API'si</span><span class="sxs-lookup"><span data-stu-id="82bb6-149">Azure Search Service REST API</span></span>](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [<span data-ttu-id="82bb6-150">Dizin işlemleri</span><span class="sxs-lookup"><span data-stu-id="82bb6-150">Index Operations</span></span>](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [<span data-ttu-id="82bb6-151">Belge işlemleri</span><span class="sxs-lookup"><span data-stu-id="82bb6-151">Document Operations</span></span>](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [<span data-ttu-id="82bb6-152">Video ve Azure Search öğreticileri</span><span class="sxs-lookup"><span data-stu-id="82bb6-152">Video and tutorials about Azure Search</span></span>](search-video-demo-tutorial-list.md)
* [<span data-ttu-id="82bb6-153">Azure Search'te modellenmiş bir gezinmede</span><span class="sxs-lookup"><span data-stu-id="82bb6-153">Faceted Navigation in Azure Search</span></span>](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
