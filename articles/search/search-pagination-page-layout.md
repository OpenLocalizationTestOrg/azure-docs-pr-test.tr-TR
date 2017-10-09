---
title: "aaaHow toopage arama sonuçları Azure Search'te | Microsoft Docs"
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
ms.openlocfilehash: e3abc1ca4d5994b0a77955379081a4fcfa5a7fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopage-search-results-in-azure-search"></a><span data-ttu-id="d1260-103">Azure Search'te nasıl toopage arama sonuçları</span><span class="sxs-lookup"><span data-stu-id="d1260-103">How toopage search results in Azure Search</span></span>
<span data-ttu-id="d1260-104">Bu makalede, nasıl toouse hello Azure Search Hizmeti REST API'si tooimplement standart öğeleri arama sonuçları sayfası, toplam sayıları, belge alma, sıralamalar ve gezinti gibi hakkında yönergeleri sunar.</span><span class="sxs-lookup"><span data-stu-id="d1260-104">This article provides guidance on how toouse hello Azure Search Service REST API tooimplement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span></span>

<span data-ttu-id="d1260-105">Aşağıda belirtilen her durumda, verileri veya bilgi tooyour arama sonuçları sayfasını katkıda sayfasıyla ilgili seçenekleri hello belirlenmiş [arama belge](http://msdn.microsoft.com/library/azure/dn798927.aspx) gönderilen istekleri tooyour Azure Search hizmeti.</span><span class="sxs-lookup"><span data-stu-id="d1260-105">In every case mentioned below, page-related options that contribute data or information tooyour search results page are specified through hello [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent tooyour Azure Search Service.</span></span> <span data-ttu-id="d1260-106">İstekleri GET komutu, yol ve ne istenen hello hizmet bildirmek sorgu parametreleri ile nasıl tooformulate hello yanıt içerir.</span><span class="sxs-lookup"><span data-stu-id="d1260-106">Requests include a GET command, path, and query parameters that inform hello service what is being requested, and how tooformulate hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="d1260-107">Geçerli bir istek bir hizmet URL'si ve yol, HTTP fiili gibi öğeleri içerir `api-version`ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="d1260-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span></span> <span data-ttu-id="d1260-108">Konuyu uzatmamak amacıyla, ilgili toopagination olan hello örnekler toohighlight yalnızca hello sözdizimi kırpılır.</span><span class="sxs-lookup"><span data-stu-id="d1260-108">For brevity, we trimmed hello examples toohighlight just hello syntax that is relevant toopagination.</span></span> <span data-ttu-id="d1260-109">Lütfen hello bakın [Azure Search Hizmeti REST API'si](http://msdn.microsoft.com/library/azure/dn798935.aspx) isteği sözdizimi hakkında ayrıntılar için belgelere.</span><span class="sxs-lookup"><span data-stu-id="d1260-109">Please see hello [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span></span>
> 
> 

## <a name="total-hits-and-page-counts"></a><span data-ttu-id="d1260-110">Toplam İsabet ve sayfa sayıları</span><span class="sxs-lookup"><span data-stu-id="d1260-110">Total hits and Page Counts</span></span>
<span data-ttu-id="d1260-111">Merhaba bir sorgudan döndürülen sonuç sayısı ve bu döndürme daha küçük parçalar sonuçların toplam gösteren, tüm arama sayfaları temel toovirtually olur.</span><span class="sxs-lookup"><span data-stu-id="d1260-111">Showing hello total number of results returned from a query, and then returning those results in smaller chunks, is fundamental toovirtually all search pages.</span></span>

![][1]

<span data-ttu-id="d1260-112">Azure Search'te hello kullan `$count`, `$top`, ve `$skip` parametreleri tooreturn bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="d1260-112">In Azure Search, you use hello `$count`, `$top`, and `$skip` parameters tooreturn these values.</span></span> <span data-ttu-id="d1260-113">Merhaba aşağıdaki örnekte gösterilir olarak döndürülen toplam isabet sayısı için bir örnek istek `@OData.count`:</span><span class="sxs-lookup"><span data-stu-id="d1260-113">hello following example shows a sample request for total hits, returned as `@OData.count`:</span></span>

        GET /indexes/onlineCatalog/docs?$count=true

<span data-ttu-id="d1260-114">15 grupları belgelerde almak ve ayrıca hello ilk sayfasına başlangıç hello toplam isabet sayısı göster:</span><span class="sxs-lookup"><span data-stu-id="d1260-114">Retrieve documents in groups of 15, and also show hello total hits, starting at hello first page:</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

<span data-ttu-id="d1260-115">Sonuçları sayfa numaralandırma, gerektiren her ikisi de `$top` ve `$skip`, burada `$top` kaç öğeleri tooreturn bir toplu işlemde belirtir ve `$skip` kaç öğeleri tooskip belirtir.</span><span class="sxs-lookup"><span data-stu-id="d1260-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items tooreturn in a batch, and `$skip` specifies how many items tooskip.</span></span> <span data-ttu-id="d1260-116">Hello Örneğin, aşağıdaki her bir sayfa hello sonraki 15 öğeleri gösterir hello artımlı atlar hello içinde belirtildiği `$skip` parametresi.</span><span class="sxs-lookup"><span data-stu-id="d1260-116">In hello following example, each page shows hello next 15 items, indicated by hello incremental jumps in hello `$skip` parameter.</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a><span data-ttu-id="d1260-117">Düzen</span><span class="sxs-lookup"><span data-stu-id="d1260-117">Layout</span></span>
<span data-ttu-id="d1260-118">Arama sonuçları sayfasında, bir küçük resim, alanlarının alt kümesini ve bir bağlantı tooa tam ürün sayfasını tooshow isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1260-118">On a search results page, you might want tooshow a thumbnail image, a subset of fields, and a link tooa full product page.</span></span>

 ![][2]

<span data-ttu-id="d1260-119">Azure Search'te kullanacağınız `$select` ve arama bu deneyim tooimplement komutu.</span><span class="sxs-lookup"><span data-stu-id="d1260-119">In Azure Search, you would use `$select` and a lookup command tooimplement this experience.</span></span>

<span data-ttu-id="d1260-120">tooreturn bir alt alanların döşeli düzeni için:</span><span class="sxs-lookup"><span data-stu-id="d1260-120">tooreturn a subset of fields for a tiled layout:</span></span>

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

<span data-ttu-id="d1260-121">Görüntüleri ve medya dosyaları doğrudan aranabilir değildir ve tooreduce maliyetler Azure Blob Depolama alanı gibi başka bir depolama Platform depolanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1260-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, tooreduce costs.</span></span> <span data-ttu-id="d1260-122">Başlangıç dizini ve belgeleri, hello dış içeriği hello URL adresini depolayan bir alan tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="d1260-122">In hello index and documents, define a field that stores hello URL address of hello external content.</span></span> <span data-ttu-id="d1260-123">Ardından, bir resim başvurusu hello alanını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1260-123">You can then use hello field as an image reference.</span></span> <span data-ttu-id="d1260-124">Merhaba URL toohello görüntü hello belgede olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d1260-124">hello URL toohello image should be in hello document.</span></span>

<span data-ttu-id="d1260-125">Ürün açıklaması sayfa için tooretrieve bir **onClick** olay, kullanım [arama belge](http://msdn.microsoft.com/library/azure/dn798929.aspx) hello belge tooretrieve hello anahtarı toopass.</span><span class="sxs-lookup"><span data-stu-id="d1260-125">tooretrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass in hello key of hello document tooretrieve.</span></span> <span data-ttu-id="d1260-126">başlangıç anahtarı Hello veri türü `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="d1260-126">hello data type of hello key is `Edm.String`.</span></span> <span data-ttu-id="d1260-127">Bu örnek, *246810*.</span><span class="sxs-lookup"><span data-stu-id="d1260-127">In this example, it is *246810*.</span></span> 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a><span data-ttu-id="d1260-128">İlgi, derecelendirme veya fiyat göre sırala</span><span class="sxs-lookup"><span data-stu-id="d1260-128">Sort by relevance, rating, or price</span></span>
<span data-ttu-id="d1260-129">Sıralama genellikle toorelevance varsayılan ancak ortak toomake alternatif sıralamalar kullanıma hazır, böylelikle müşterilerin hızla varolan sonuçları farklı bir sıralama düzeni içinde sırasını yeniden ayarlaması sıralar.</span><span class="sxs-lookup"><span data-stu-id="d1260-129">Sort orders often default toorelevance, but it's common toomake alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span></span>

 ![][3]

<span data-ttu-id="d1260-130">Azure Search'te sıralama üzerinde hello dayanır `$orderby` olarak dizin oluşturulmuş tüm alanlar için ifade`"Sortable": true.`</span><span class="sxs-lookup"><span data-stu-id="d1260-130">In Azure Search, sorting is based on hello `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span></span>

<span data-ttu-id="d1260-131">İlgi kesinlikle profilleri Puanlama ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="d1260-131">Relevance is strongly associated with scoring profiles.</span></span> <span data-ttu-id="d1260-132">Daha fazla veya daha güçlü eşleşme ile toodocuments bir arama terimi giderek daha yüksek puanları ile tüm sonuçları metin analiz ve İstatistikler toorank siparişte kullanır hello varsayılan Puanlama, kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1260-132">You can use hello default scoring, which relies on text analysis and statistics toorank order all results, with higher scores going toodocuments with more or stronger matches on a search term.</span></span>

<span data-ttu-id="d1260-133">Alternatif sıralamalar genellikle ilişkili olan **onClick** geri tooa yöntemi, arama olayları hello sıralama düzeni oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d1260-133">Alternative sort orders are typically associated with **onClick** events that call back tooa method that builds hello sort order.</span></span> <span data-ttu-id="d1260-134">Örneğin, bu sayfa öğesi verilen:</span><span class="sxs-lookup"><span data-stu-id="d1260-134">For example, given this page element:</span></span>

 ![][4]

<span data-ttu-id="d1260-135">Seçili hello sıralama seçeneği giriş olarak kabul eder ve bu seçenek ile ilişkili hello ölçütlerine sıralı bir listesi döndüren bir yöntem oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="d1260-135">You would create a method that accepts hello selected sort option as input, and returns an ordered list for hello criteria associated with that option.</span></span>

 ![][5]

> [!NOTE]
> <span data-ttu-id="d1260-136">Varsayılan Hello Puanlama birçok senaryo için yeterli olmakla birlikte, bunun yerine özel bir Puanlama profili ilgi alma öneririz.</span><span class="sxs-lookup"><span data-stu-id="d1260-136">While hello default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span></span> <span data-ttu-id="d1260-137">Özel bir Puanlama profili daha yararlı tooyour iş bir şekilde tooboost öğeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="d1260-137">A custom scoring profile gives you a way tooboost items that are more beneficial tooyour business.</span></span> <span data-ttu-id="d1260-138">Bkz: [Puanlama profili Ekle](http://msdn.microsoft.com/library/azure/dn798928.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="d1260-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> 
> 
> 

## <a name="faceted-navigation"></a><span data-ttu-id="d1260-139">Çok yönlü gezinme</span><span class="sxs-lookup"><span data-stu-id="d1260-139">Faceted navigation</span></span>
<span data-ttu-id="d1260-140">Arama gezinti genellikle hello yan veya bir sayfanın üst kısmında bulunan bir sonuçlar sayfası üzerinde yaygındır.</span><span class="sxs-lookup"><span data-stu-id="d1260-140">Search navigation is common on a results page, often located at hello side or top of a page.</span></span> <span data-ttu-id="d1260-141">Azure Search'te modellenmiş bir gezinmede önceden tanımlanmış filtrelere göre kendi kendine yönlendirilmiş arama sağlar.</span><span class="sxs-lookup"><span data-stu-id="d1260-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span></span> <span data-ttu-id="d1260-142">Bkz: [Azure Search'te modellenmiş bir gezinmede](search-faceted-navigation.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="d1260-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span></span>

## <a name="filters-at-hello-page-level"></a><span data-ttu-id="d1260-143">Merhaba sayfa düzeyinde filtreleri</span><span class="sxs-lookup"><span data-stu-id="d1260-143">Filters at hello page level</span></span>
<span data-ttu-id="d1260-144">Çözüm tasarımınızın belirli türlerdeki içerik (örneğin, hello hello sayfanın başında listelenen bölümleri olan bir çevrimiçi perakende uygulama) için ayrılmış arama sayfalar dahil, bir filtre ifadesi yanında ekleyebilirsiniz bir **onClick** olay tooopen bir sayfa makale bir durumda.</span><span class="sxs-lookup"><span data-stu-id="d1260-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at hello top of hello page), you can insert a filter expression alongside an **onClick** event tooopen a page in a prefiltered state.</span></span> 

<span data-ttu-id="d1260-145">Bir filtre ile veya olmadan arama ifadesi gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1260-145">You can send a filter with or without a search expression.</span></span> <span data-ttu-id="d1260-146">Örneğin, hello aşağıdaki isteği marka, eşleşen belgeleri döndüren adına filtre uygular.</span><span class="sxs-lookup"><span data-stu-id="d1260-146">For example, hello following request will filter on brand name, returning only those documents that match it.</span></span>

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

<span data-ttu-id="d1260-147">Bkz: [Search belgeleri (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) hakkında daha fazla bilgi için `$filter` ifadeler.</span><span class="sxs-lookup"><span data-stu-id="d1260-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="d1260-148">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="d1260-148">See Also</span></span>
* [<span data-ttu-id="d1260-149">Azure Search Hizmeti REST API'si</span><span class="sxs-lookup"><span data-stu-id="d1260-149">Azure Search Service REST API</span></span>](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [<span data-ttu-id="d1260-150">Dizin işlemleri</span><span class="sxs-lookup"><span data-stu-id="d1260-150">Index Operations</span></span>](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [<span data-ttu-id="d1260-151">Belge işlemleri</span><span class="sxs-lookup"><span data-stu-id="d1260-151">Document Operations</span></span>](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [<span data-ttu-id="d1260-152">Video ve Azure Search öğreticileri</span><span class="sxs-lookup"><span data-stu-id="d1260-152">Video and tutorials about Azure Search</span></span>](search-video-demo-tutorial-list.md)
* [<span data-ttu-id="d1260-153">Azure Search'te modellenmiş bir gezinmede</span><span class="sxs-lookup"><span data-stu-id="d1260-153">Faceted Navigation in Azure Search</span></span>](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
