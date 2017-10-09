---
title: "Ayrıca \"bir dizin (REST API - Azure Search) sorgu | Microsoft Docs\""
description: "Azure Search'te bir arama sorgusu oluşturun ve arama parametrelerini toofilter ve sıralama arama sonuçlarını kullanın."
services: search
documentationcenter: 
manager: jhubbard
author: ashmaka
ms.assetid: 8b3ca890-2f5f-44b6-a140-6cb676fc2c9c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/12/2017
ms.author: ashmaka
ms.openlocfilehash: 2f12238b8f4b045f536489cfc8766fb68307bbe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-rest-api"></a><span data-ttu-id="9ba88-103">Merhaba REST API kullanarak Azure Search dizininizi sorgulama</span><span class="sxs-lookup"><span data-stu-id="9ba88-103">Query your Azure Search index using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="9ba88-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="9ba88-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="9ba88-105">Portal</span><span class="sxs-lookup"><span data-stu-id="9ba88-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="9ba88-106">.NET</span><span class="sxs-lookup"><span data-stu-id="9ba88-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="9ba88-107">REST</span><span class="sxs-lookup"><span data-stu-id="9ba88-107">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="9ba88-108">Bu makalede tooquery kullanarak bir dizinin nasıl hello gösterilmektedir [Azure Search REST API'sini](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="9ba88-108">This article shows you how tooquery an index using hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

<span data-ttu-id="9ba88-109">Bu kılavuzda başlamadan önce, [Azure Search dizini oluşturmuş](search-what-is-an-index.md) ve [bunu verilerle doldurmuş](search-what-is-data-import.md) olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ba88-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span> <span data-ttu-id="9ba88-110">Arka plan bilgileri için bkz. [Azure Search'te tam metin araması nasıl çalışır](search-lucene-query-architecture.md)?</span><span class="sxs-lookup"><span data-stu-id="9ba88-110">For background information, see [How full text search works in Azure Search](search-lucene-query-architecture.md).</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="9ba88-111">Azure Search hizmet sorgunuzun api anahtarını tanımlama</span><span class="sxs-lookup"><span data-stu-id="9ba88-111">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="9ba88-112">Bir anahtar hello Azure Search REST API'sini karşı tüm arama işlemlerinin hello bileşenidir *api anahtarını* sağladığınız hello hizmeti için oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="9ba88-112">A key component of every search operation against hello Azure Search REST API is hello *api-key* that was generated for hello service you provisioned.</span></span> <span data-ttu-id="9ba88-113">Geçerli bir anahtar sahip istek başına temelinde, hello isteği gönderiliyor hello uygulama ve bunu işleyen hello hizmeti arasında güven oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9ba88-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="9ba88-114">toofind hizmetinizin api anahtarlarından, toohello kaydolabilirsiniz [Azure portalı](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="9ba88-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="9ba88-115">Tooyour Azure Search hizmet dikey penceresine gidin</span><span class="sxs-lookup"><span data-stu-id="9ba88-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="9ba88-116">Merhaba "Anahtarlar" simgesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="9ba88-116">Click hello "Keys" icon</span></span>

<span data-ttu-id="9ba88-117">Hizmetiniz, *yönetici anahtarlarına* ve *sorgu anahtarlarına* sahiptir.</span><span class="sxs-lookup"><span data-stu-id="9ba88-117">Your service has *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="9ba88-118">Birincil ve ikincil *yönetici anahtarları* tooall operations hello özelliği toomanage hello hizmeti dahil olmak üzere, tam haklar, oluşturun ve dizinler, dizin oluşturucular ve veri kaynaklarını silin.</span><span class="sxs-lookup"><span data-stu-id="9ba88-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="9ba88-119">Tooregenerate hello birincil anahtar ve tam tersini karar verirseniz toouse hello ikincil anahtar devam edebilmesi için bu iki anahtar vardır.</span><span class="sxs-lookup"><span data-stu-id="9ba88-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="9ba88-120">*Sorgu anahtarları* salt okunur erişim tooindexes ve belgeleri verin ve arama istekleri gönderen genellikle dağıtılmış tooclient uygulamalardır.</span><span class="sxs-lookup"><span data-stu-id="9ba88-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="9ba88-121">Bir dizini sorgulama hello amacıyla, sorgu anahtarlarınızdan birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ba88-121">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="9ba88-122">Yönetici anahtarlarınız da sorgular için kullanılabilir, ancak bu daha iyi hello aşağıdaki gibi uygulama kodunuzda bir sorgu anahtarı kullanmanız gerekir [en az ayrıcalık prensibi](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="9ba88-122">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="formulate-your-query"></a><span data-ttu-id="9ba88-123">Sorgunuzu düzenleme</span><span class="sxs-lookup"><span data-stu-id="9ba88-123">Formulate your query</span></span>
<span data-ttu-id="9ba88-124">İki yolu vardır çok[hello REST API kullanarak dizininizi aramanın](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="9ba88-124">There are two ways too[search your index using hello REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="9ba88-125">Bir HTTP POST isteği tooissue sorgu parametrelerinizin hello istek gövdesindeki bir JSON nesnesinde tanımlandığı yoludur.</span><span class="sxs-lookup"><span data-stu-id="9ba88-125">One way is tooissue an HTTP POST request where your query parameters are defined in a JSON object in hello request body.</span></span> <span data-ttu-id="9ba88-126">Merhaba başka bir yolla tooissue bir HTTP GET isteği burada sorgu parametrelerinizin hello istek URL'si içinde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9ba88-126">hello other way is tooissue an HTTP GET request where your query parameters are defined within hello request URL.</span></span> <span data-ttu-id="9ba88-127">POST sahip daha [esnek sınırlara](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) hello Sorgu parametrelerinin boyutu açısından get'ten üzerinde.</span><span class="sxs-lookup"><span data-stu-id="9ba88-127">POST has more [relaxed limits](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) on hello size of query parameters than GET.</span></span> <span data-ttu-id="9ba88-128">Bu nedenle, GET'i kullanmanın daha kullanışlı olduğu özel durumlar olmadığı sürece POST kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="9ba88-128">For this reason, we recommend using POST unless you have special circumstances where using GET would be more convenient.</span></span>

<span data-ttu-id="9ba88-129">POST ve GET için tooprovide gerekir, *hizmet adı*, *dizin adı*ve hello uygun *API sürümü* (Merhaba geçerli API sürümü `2016-09-01` hello zaman Bu belgenin yayımlandığı) hello istek URL'si.</span><span class="sxs-lookup"><span data-stu-id="9ba88-129">For both POST and GET, you need tooprovide your *service name*, *index name*, and hello proper *API version* (hello current API version is `2016-09-01` at hello time of publishing this document) in hello request URL.</span></span> <span data-ttu-id="9ba88-130">GET için hello *sorgu dizesi* hello hello URL hello sorgu parametreleri Burada sağladığınız sonudur.</span><span class="sxs-lookup"><span data-stu-id="9ba88-130">For GET, hello *query string* at hello end of hello URL is where you provide hello query parameters.</span></span> <span data-ttu-id="9ba88-131">Aşağıda hello URL biçimi için bkz:</span><span class="sxs-lookup"><span data-stu-id="9ba88-131">See below for hello URL format:</span></span>

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

<span data-ttu-id="9ba88-132">Merhaba olduğu POST hello için aynı, ancak yalnızca api sürümü hello sorgu dizesi parametreleri ile biçimlendirin.</span><span class="sxs-lookup"><span data-stu-id="9ba88-132">hello format for POST is hello same, but with only api-version in hello query string parameters.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="9ba88-133">Örnek Sorgular</span><span class="sxs-lookup"><span data-stu-id="9ba88-133">Example Queries</span></span>
<span data-ttu-id="9ba88-134">Burada "hotels" adlı bir dizinde birkaç örnek sorgu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9ba88-134">Here are a few example queries on an index named "hotels".</span></span> <span data-ttu-id="9ba88-135">Bu sorgular, hem GET hem de POST biçiminde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="9ba88-135">These queries are shown in both GET and POST format.</span></span>

<span data-ttu-id="9ba88-136">Merhaba tüm dizinde "budget" Merhaba dönem için arama ve yalnızca hello dönmek `hotelName` alan:</span><span class="sxs-lookup"><span data-stu-id="9ba88-136">Search hello entire index for hello term 'budget' and return only hello `hotelName` field:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

<span data-ttu-id="9ba88-137">Bir filtre toohello dizin toofind Oteller geceliği 150 gece dolardan ucuz uygulamak ve dönüş hello `hotelId` ve `description`:</span><span class="sxs-lookup"><span data-stu-id="9ba88-137">Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello `hotelId` and `description`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

<span data-ttu-id="9ba88-138">Arama hello tüm dizin, belirli bir alana göre sıralama (`lastRenovationDate`) azalan sırada hello ilk iki sonucu alın ve yalnızca Göster `hotelName` ve `lastRenovationDate`:</span><span class="sxs-lookup"><span data-stu-id="9ba88-138">Search hello entire index, order by a specific field (`lastRenovationDate`) in descending order, take hello top two results, and show only `hotelName` and `lastRenovationDate`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$top=2&$orderby=lastRenovationDate desc&$select=hotelName,lastRenovationDate&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "orderby": "lastRenovationDate desc",
    "select": "hotelName,lastRenovationDate",
    "top": 2
}
```

## <a name="submit-your-http-request"></a><span data-ttu-id="9ba88-139">HTTP isteğinizi gönderme</span><span class="sxs-lookup"><span data-stu-id="9ba88-139">Submit your HTTP request</span></span>
<span data-ttu-id="9ba88-140">Artık HTTP istek URL'nizin (GET için) veya gövdenizin (POST için) parçası olarak sorgunuzu düzenlediğinize göre, istek üst bilgilerinizi tanımlayıp sorgunuzu gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ba88-140">Now that you have formulated your query as part of your HTTP request URL (for GET) or body (for POST), you can define your request headers and submit your query.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="9ba88-141">İstek ve İstek Üst Bilgileri</span><span class="sxs-lookup"><span data-stu-id="9ba88-141">Request and Request Headers</span></span>
<span data-ttu-id="9ba88-142">GET için iki, POST için ise üç istek üst bilgisi tanımlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9ba88-142">You must define two request headers for GET, or three for POST:</span></span>

1. <span data-ttu-id="9ba88-143">Merhaba `api-key` üstbilgi bulunan adımda ı yukarıdaki toohello sorgu anahtarını ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ba88-143">hello `api-key` header must be set toohello query key you found in step I above.</span></span> <span data-ttu-id="9ba88-144">Bir yönetici anahtarı hello kullanabilirsiniz `api-key` üstbilgisi, ancak önerilir salt okunur erişim tooindexes ve belgeler özel olarak verir gibi bir sorgu anahtarı kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="9ba88-144">You can also use an admin key as hello `api-key` header, but it is recommended that you use a query key as it exclusively grants read-only access tooindexes and documents.</span></span>
2. <span data-ttu-id="9ba88-145">Merhaba `Accept` üstbilgisi çok ayarlanmalıdır`application/json`.</span><span class="sxs-lookup"><span data-stu-id="9ba88-145">hello `Accept` header must be set too`application/json`.</span></span>
3. <span data-ttu-id="9ba88-146">Yalnızca POST için hello `Content-Type` üstbilgisi çok ayarlanmalıdır`application/json`.</span><span class="sxs-lookup"><span data-stu-id="9ba88-146">For POST only, hello `Content-Type` header should also be set too`application/json`.</span></span>

<span data-ttu-id="9ba88-147">Merhaba hello "motel" terimini arayan basit bir sorgu kullanarak Azure Search REST API'sini kullanarak HTTP GET isteği toosearch hello "hotels" dizini için aşağıya bakın:</span><span class="sxs-lookup"><span data-stu-id="9ba88-147">See below for an HTTP GET request toosearch hello "hotels" index using hello Azure Search REST API, using a simple query that searches for hello term "motel":</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

<span data-ttu-id="9ba88-148">İşte aynı hello örnek sorgu, HTTP POST kullanılarak bu süre:</span><span class="sxs-lookup"><span data-stu-id="9ba88-148">Here is hello same example query, this time using HTTP POST:</span></span>

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

<span data-ttu-id="9ba88-149">Başarılı bir sorgu isteği bir durum koduna neden olacak `200 OK` ve hello arama sonuçları hello yanıt gövdesinde JSON olarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="9ba88-149">A successful query request will result in a Status Code of `200 OK` and hello search results are returned as JSON in hello response body.</span></span> <span data-ttu-id="9ba88-150">İşte hello "hotels" dizininin içinde hello örnek verilerle varsayıldığında hello sorgunun yukarıda için hangi hello sonuçları [Veri Al'ı kullanarak Azure Search REST API hello](search-import-data-rest-api.md) (JSON, daha anlaşılır olması için biçimlendirilmiş bu hello unutmayın).</span><span class="sxs-lookup"><span data-stu-id="9ba88-150">Here is what hello results for hello above query look like, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello REST API](search-import-data-rest-api.md) (note that hello JSON has been formatted for clarity).</span></span>

```JSON
{
    "value": [
        {
            "@search.score": 0.59600675,
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags":["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": {
                "type": "Point",
                "coordinates": [-122.131577, 49.678581],
                "crs": {
                    "type":"name",
                    "properties": {
                        "name": "EPSG:4326"
                    }
                }
            }
        }
    ]
}
```

<span data-ttu-id="9ba88-151">toolearn daha, lütfen şu adresi ziyaret hello "Yanıt" bölümünü [Search belgeleri](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="9ba88-151">toolearn more, please visit hello "Response" section of [Search Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="9ba88-152">Hata durumunda döndürülebilen diğer HTTP durum kodları hakkında daha fazla bilgi için bkz. [HTTP durum kodları (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="9ba88-152">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>
