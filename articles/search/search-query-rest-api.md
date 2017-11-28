---
title: Dizin sorgulama (REST API - Azure Search) | Microsoft Docs
description: "Azure Search'te bir arama sorgusu oluşturun ve arama sonuçlarını filtrelemek ve sıralamak için arama parametrelerini kullanın."
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
ms.openlocfilehash: 49062bec233ad35cd457f9665fa94c1855343582
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="query-your-azure-search-index-using-the-rest-api"></a><span data-ttu-id="6ff57-103">REST API kullanarak Azure Search dizininizi sorgulama</span><span class="sxs-lookup"><span data-stu-id="6ff57-103">Query your Azure Search index using the REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="6ff57-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6ff57-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="6ff57-105">Portal</span><span class="sxs-lookup"><span data-stu-id="6ff57-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="6ff57-106">.NET</span><span class="sxs-lookup"><span data-stu-id="6ff57-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="6ff57-107">REST</span><span class="sxs-lookup"><span data-stu-id="6ff57-107">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="6ff57-108">Bu makale, [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/)'sini kullanarak bir dizinin nasıl sorgulanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="6ff57-108">This article shows you how to query an index using the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

<span data-ttu-id="6ff57-109">Bu kılavuzda başlamadan önce, [Azure Search dizini oluşturmuş](search-what-is-an-index.md) ve [bunu verilerle doldurmuş](search-what-is-data-import.md) olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ff57-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span> <span data-ttu-id="6ff57-110">Arka plan bilgileri için bkz. [Azure Search'te tam metin araması nasıl çalışır](search-lucene-query-architecture.md)?</span><span class="sxs-lookup"><span data-stu-id="6ff57-110">For background information, see [How full text search works in Azure Search](search-lucene-query-architecture.md).</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="6ff57-111">Azure Search hizmet sorgunuzun api anahtarını tanımlama</span><span class="sxs-lookup"><span data-stu-id="6ff57-111">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="6ff57-112">Azure Search REST API'sine karşı tüm arama işlemlerinin önemli bir bileşeni, sağladığınız hizmet için oluşturulan *api anahtarıdır*.</span><span class="sxs-lookup"><span data-stu-id="6ff57-112">A key component of every search operation against the Azure Search REST API is the *api-key* that was generated for the service you provisioned.</span></span> <span data-ttu-id="6ff57-113">İstek başına geçerli bir anahtara sahip olmak, isteği gönderen uygulama ve bunu işleyen hizmet arasında güven oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6ff57-113">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="6ff57-114">Hizmetinizin api anahtarlarını bulmak için [Azure portalında](https://portal.azure.com/) oturum açabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6ff57-114">To find your service's api-keys, you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="6ff57-115">Azure Search hizmetinizin dikey penceresine gidin</span><span class="sxs-lookup"><span data-stu-id="6ff57-115">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="6ff57-116">"Anahtarlar" simgesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="6ff57-116">Click the "Keys" icon</span></span>

<span data-ttu-id="6ff57-117">Hizmetiniz, *yönetici anahtarlarına* ve *sorgu anahtarlarına* sahiptir.</span><span class="sxs-lookup"><span data-stu-id="6ff57-117">Your service has *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="6ff57-118">Birincil ve ikincil *yönetici anahtarlarınız*; hizmeti yönetme, dizinler, dizin oluşturucular ve veri kaynakları ekleme ve silme de dahil olmak üzere her türlü işlem için tüm hakları verir.</span><span class="sxs-lookup"><span data-stu-id="6ff57-118">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="6ff57-119">Birincil anahtarı yeniden oluşturmaya karar verirseniz ikincil anahtarı kullanmaya devam edebilmeniz ve tam tersini yapabilmeniz için iki anahtar vardır.</span><span class="sxs-lookup"><span data-stu-id="6ff57-119">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="6ff57-120">*Sorgu anahtarları*, dizinler ve belgeler için salt okunur erişim verir ve genellikle, arama istekleri gönderen istemci uygulamalarına dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="6ff57-120">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="6ff57-121">Bir dizini sorgulama amacıyla, sorgu anahtarlarınızdan birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ff57-121">For the purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="6ff57-122">Yönetici anahtarlarınız da sorgular için kullanılabilir ancak uygulama kodunuzda bir sorgu anahtarı kullanmanız gerekir. Böylece [En az ayrıcalık prensibi](https://en.wikipedia.org/wiki/Principle_of_least_privilege) daha iyi takip edilmiş olur.</span><span class="sxs-lookup"><span data-stu-id="6ff57-122">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows the [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="formulate-your-query"></a><span data-ttu-id="6ff57-123">Sorgunuzu düzenleme</span><span class="sxs-lookup"><span data-stu-id="6ff57-123">Formulate your query</span></span>
<span data-ttu-id="6ff57-124">[REST API kullanarak dizininizi aramanın](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) iki yolu bulunur.</span><span class="sxs-lookup"><span data-stu-id="6ff57-124">There are two ways to [search your index using the REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="6ff57-125">Bu yollardan biri, sorgu parametrelerinizin istek gövdesindeki bir JSON nesnesinde tanımlanacağı bir HTTP POST isteği göndermektir.</span><span class="sxs-lookup"><span data-stu-id="6ff57-125">One way is to issue an HTTP POST request where your query parameters are defined in a JSON object in the request body.</span></span> <span data-ttu-id="6ff57-126">Diğer yol ise sorgu parametrelerinizin istek URL'si içinde tanımlanacağı bir HTTP GET isteği göndermektir.</span><span class="sxs-lookup"><span data-stu-id="6ff57-126">The other way is to issue an HTTP GET request where your query parameters are defined within the request URL.</span></span> <span data-ttu-id="6ff57-127">POST, sorgu parametrelerinin boyutu açısından GET'ten daha [esnek sınırlara](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="6ff57-127">POST has more [relaxed limits](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) on the size of query parameters than GET.</span></span> <span data-ttu-id="6ff57-128">Bu nedenle, GET'i kullanmanın daha kullanışlı olduğu özel durumlar olmadığı sürece POST kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="6ff57-128">For this reason, we recommend using POST unless you have special circumstances where using GET would be more convenient.</span></span>

<span data-ttu-id="6ff57-129">POST ve GET için *hizmet adınızı*, *dizin adını* ve uygun *API sürümünü* (bu belgenin yayımlandığı sırada geçerli API sürümü `2016-09-01`) istek URL'sinde sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ff57-129">For both POST and GET, you need to provide your *service name*, *index name*, and the proper *API version* (the current API version is `2016-09-01` at the time of publishing this document) in the request URL.</span></span> <span data-ttu-id="6ff57-130">GET için sorgu parametrelerini URL'nin sonundaki *sorgu dizesine* sağlarsınız.</span><span class="sxs-lookup"><span data-stu-id="6ff57-130">For GET, the *query string* at the end of the URL is where you provide the query parameters.</span></span> <span data-ttu-id="6ff57-131">URL biçimi için aşağıya bakın:</span><span class="sxs-lookup"><span data-stu-id="6ff57-131">See below for the URL format:</span></span>

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

<span data-ttu-id="6ff57-132">POST için biçim aynıdır ancak sorgu dizesi parametrelerinde yalnızca api sürümü olur.</span><span class="sxs-lookup"><span data-stu-id="6ff57-132">The format for POST is the same, but with only api-version in the query string parameters.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="6ff57-133">Örnek Sorgular</span><span class="sxs-lookup"><span data-stu-id="6ff57-133">Example Queries</span></span>
<span data-ttu-id="6ff57-134">Burada "hotels" adlı bir dizinde birkaç örnek sorgu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6ff57-134">Here are a few example queries on an index named "hotels".</span></span> <span data-ttu-id="6ff57-135">Bu sorgular, hem GET hem de POST biçiminde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="6ff57-135">These queries are shown in both GET and POST format.</span></span>

<span data-ttu-id="6ff57-136">Tüm dizinde "budget" terimi araması yapın ve yalnızca `hotelName` alanını döndürün:</span><span class="sxs-lookup"><span data-stu-id="6ff57-136">Search the entire index for the term 'budget' and return only the `hotelName` field:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

<span data-ttu-id="6ff57-137">Geceliği 150 dolardan ucuz oteller bulmak için dizinde bir filtre uygulayıp `hotelId` ve `description` sonuçlarını döndürün:</span><span class="sxs-lookup"><span data-stu-id="6ff57-137">Apply a filter to the index to find hotels cheaper than $150 per night, and return the `hotelId` and `description`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

<span data-ttu-id="6ff57-138">Tüm dizinde arama yapın, belirli bir alana göre (`lastRenovationDate`) azalan sıralamada sıralama yapın, ilk iki sonucu alın ve yalnızca `hotelName` ve `lastRenovationDate` öğesinin gösterilmesini sağlayın:</span><span class="sxs-lookup"><span data-stu-id="6ff57-138">Search the entire index, order by a specific field (`lastRenovationDate`) in descending order, take the top two results, and show only `hotelName` and `lastRenovationDate`:</span></span>

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

## <a name="submit-your-http-request"></a><span data-ttu-id="6ff57-139">HTTP isteğinizi gönderme</span><span class="sxs-lookup"><span data-stu-id="6ff57-139">Submit your HTTP request</span></span>
<span data-ttu-id="6ff57-140">Artık HTTP istek URL'nizin (GET için) veya gövdenizin (POST için) parçası olarak sorgunuzu düzenlediğinize göre, istek üst bilgilerinizi tanımlayıp sorgunuzu gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ff57-140">Now that you have formulated your query as part of your HTTP request URL (for GET) or body (for POST), you can define your request headers and submit your query.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="6ff57-141">İstek ve İstek Üst Bilgileri</span><span class="sxs-lookup"><span data-stu-id="6ff57-141">Request and Request Headers</span></span>
<span data-ttu-id="6ff57-142">GET için iki, POST için ise üç istek üst bilgisi tanımlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6ff57-142">You must define two request headers for GET, or three for POST:</span></span>

1. <span data-ttu-id="6ff57-143">`api-key` üst bilgisi, yukarıdaki 1. adımda bulduğunuz sorgu anahtarına ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6ff57-143">The `api-key` header must be set to the query key you found in step I above.</span></span> <span data-ttu-id="6ff57-144">`api-key` üst bilgisi olarak bir yönetici anahtarı da kullanabilirsiniz ancak dizinlere ve belgelere açık bir şekilde salt okunur erişimi verdiğinden, bir sorgu anahtarı kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="6ff57-144">You can also use an admin key as the `api-key` header, but it is recommended that you use a query key as it exclusively grants read-only access to indexes and documents.</span></span>
2. <span data-ttu-id="6ff57-145">`Accept` üst bilgisi `application/json` şeklinde ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6ff57-145">The `Accept` header must be set to `application/json`.</span></span>
3. <span data-ttu-id="6ff57-146">Yalnızca POST için `Content-Type` üst bilgisi `application/json` olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6ff57-146">For POST only, the `Content-Type` header should also be set to `application/json`.</span></span>

<span data-ttu-id="6ff57-147">"Motel" terimini arayan basit bir sorgu kullanarak Azure Search REST API'sini kullanıp "hotels" dizininde arama yapmaya yönelik bir HTTP GET isteği için aşağıya bakın:</span><span class="sxs-lookup"><span data-stu-id="6ff57-147">See below for an HTTP GET request to search the "hotels" index using the Azure Search REST API, using a simple query that searches for the term "motel":</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

<span data-ttu-id="6ff57-148">Aşağıda bu sefer HTTP POST kullanılmış şekilde aynı örnek sorgu verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="6ff57-148">Here is the same example query, this time using HTTP POST:</span></span>

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

<span data-ttu-id="6ff57-149">Başarılı bir sorgu isteği, `200 OK` Durum Koduna sonucunu verir ve arama sonuçları, yanıt gövdesinde JSON olarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="6ff57-149">A successful query request will result in a Status Code of `200 OK` and the search results are returned as JSON in the response body.</span></span> <span data-ttu-id="6ff57-150">Yukarıdaki sorgunun sonuçları, "hotels" dizininin [REST API kullanarak Azure Search'te Veri İçeri Aktarma](search-import-data-rest-api.md)'da verilen örnek verilerle doldurulduğu varsayıldığında şöyledir (JSON'un netlik sağlaması için biçimlendirildiğini unutmayın).</span><span class="sxs-lookup"><span data-stu-id="6ff57-150">Here is what the results for the above query look like, assuming the "hotels" index is populated with the sample data in [Data Import in Azure Search using the REST API](search-import-data-rest-api.md) (note that the JSON has been formatted for clarity).</span></span>

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

<span data-ttu-id="6ff57-151">Daha fazla bilgi edinmek için lütfen [Search Belgeleri](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)'nin "Yanıt" bölümünü ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="6ff57-151">To learn more, please visit the "Response" section of [Search Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="6ff57-152">Hata durumunda döndürülebilen diğer HTTP durum kodları hakkında daha fazla bilgi için bkz. [HTTP durum kodları (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="6ff57-152">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>
