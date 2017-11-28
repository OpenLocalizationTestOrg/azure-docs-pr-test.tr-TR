---
title: "Verileri karşıya yükleme (REST API - Azure Search) | Microsoft Docs"
description: "REST API kullanarak Azure Search'te bir dizine nasıl veri yükleneceğini öğrenin."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: 8d0749fb-6e08-4a17-8cd3-1a215138abc6
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: f22a33ed86fbfc46dfa732239263a49f34c4afee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="upload-data-to-azure-search-using-the-rest-api"></a><span data-ttu-id="552b0-103">REST API kullanarak Azure Search'e veri yükleme</span><span class="sxs-lookup"><span data-stu-id="552b0-103">Upload data to Azure Search using the REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="552b0-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="552b0-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="552b0-105">.NET</span><span class="sxs-lookup"><span data-stu-id="552b0-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="552b0-106">REST</span><span class="sxs-lookup"><span data-stu-id="552b0-106">REST</span></span>](search-import-data-rest-api.md)
>
>

<span data-ttu-id="552b0-107">Bu makalede, bir Azure Search dizinine veri aktarmak için [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/)'sinin nasıl kullanılacağı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="552b0-107">This article will show you how to use the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) to import data into an Azure Search index.</span></span>

<span data-ttu-id="552b0-108">Bu kılavuza başlamadan önce bir [Azure Search dizini oluşturmuş](search-what-is-an-index.md) olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="552b0-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span>

<span data-ttu-id="552b0-109">REST API kullanarak dizininize belgeleri göndermek için dizininizin URL uç noktasına bir HTTP POST isteği gönderirsiniz.</span><span class="sxs-lookup"><span data-stu-id="552b0-109">In order to push documents into your index using the REST API, you will issue an HTTP POST request to your index's URL endpoint.</span></span> <span data-ttu-id="552b0-110">HTTP isteğinin gövdesi eklenecek, değiştirilecek veya silinecek belgeleri içeren bir JSON nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="552b0-110">The body of the HTTP request body is a JSON object containing the documents to be added, modified, or deleted.</span></span>

## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="552b0-111">Azure Search hizmet yöneticinizin api anahtarını tanımlama</span><span class="sxs-lookup"><span data-stu-id="552b0-111">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="552b0-112">REST API kullanarak hizmetinize karşı HTTP istekleri gönderirken, *her bir* API isteğinin sağladığınız Search hizmeti için oluşturulmuş api anahtarını içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="552b0-112">When issuing HTTP requests against your service using the REST API, *each* API request must include the api-key that was generated for the Search service you provisioned.</span></span> <span data-ttu-id="552b0-113">İstek başına geçerli bir anahtara sahip olmak, isteği gönderen uygulama ve bunu işleyen hizmet arasında güven oluşturur.</span><span class="sxs-lookup"><span data-stu-id="552b0-113">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="552b0-114">Hizmetinizin api anahtarlarını bulmak için [Azure portalında](https://portal.azure.com/) oturum açabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="552b0-114">To find your service's api-keys, you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="552b0-115">Azure Search hizmetinizin dikey penceresine gidin</span><span class="sxs-lookup"><span data-stu-id="552b0-115">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="552b0-116">"Anahtarlar" simgesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="552b0-116">Click on the "Keys" icon</span></span>

<span data-ttu-id="552b0-117">Hizmetiniz, *yönetici anahtarlarına* ve *sorgu anahtarlarına* sahiptir.</span><span class="sxs-lookup"><span data-stu-id="552b0-117">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="552b0-118">Birincil ve ikincil *yönetici anahtarlarınız*; hizmeti yönetme, dizinler, dizin oluşturucular ve veri kaynakları ekleme ve silme de dahil olmak üzere her türlü işlem için tüm hakları verir.</span><span class="sxs-lookup"><span data-stu-id="552b0-118">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="552b0-119">Birincil anahtarı yeniden oluşturmaya karar verirseniz ikincil anahtarı kullanmaya devam edebilmeniz ve tam tersini yapabilmeniz için iki anahtar vardır.</span><span class="sxs-lookup"><span data-stu-id="552b0-119">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="552b0-120">*Sorgu anahtarları*, dizinler ve belgeler için salt okunur erişim verir ve genellikle, arama istekleri gönderen istemci uygulamalarına dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="552b0-120">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="552b0-121">Bir dizine veri aktarma amacıyla birincil ya da ikincil yönetici anahtarınızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="552b0-121">For the purposes of importing data into an index, you can use either your primary or secondary admin key.</span></span>

## <a name="decide-which-indexing-action-to-use"></a><span data-ttu-id="552b0-122">Hangi dizin oluşturma eyleminin kullanılacağına karar verme</span><span class="sxs-lookup"><span data-stu-id="552b0-122">Decide which indexing action to use</span></span>
<span data-ttu-id="552b0-123">REST API kullanırken, Azure Search dizininizin uç nokta URL'sine JSON istek gövdelerine sahip HTTP POST istekleri gönderirsiniz.</span><span class="sxs-lookup"><span data-stu-id="552b0-123">When using the REST API, you will issue HTTP POST requests with JSON request bodies to your Azure Search index's endpoint URL.</span></span> <span data-ttu-id="552b0-124">HTTP istek gövdenizdeki JSON nesnesi, dizininize eklemek, güncelleştirmek veya silmek istediğiniz belgeleri temsil eden JSON nesnelerini içeren "value" adlı tek bir JSON dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="552b0-124">The JSON object in your HTTP request body will contain a single JSON array named "value" containing JSON objects representing documents you would like to add to your index, update, or delete.</span></span>

<span data-ttu-id="552b0-125">"value" dizisindeki her bir JSON nesnesi, dizine alınacak bir belgeyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="552b0-125">Each JSON object in the "value" array represents a document to be indexed.</span></span> <span data-ttu-id="552b0-126">Bu nesnelerin her biri belgenin anahtarını içerir ve istenen dizin oluşturma eylemini (karşıya yükleme, birleştirme, silme, vb.) belirtir.</span><span class="sxs-lookup"><span data-stu-id="552b0-126">Each of these objects contains the document's key and specifies the desired indexing action (upload, merge, delete, etc).</span></span> <span data-ttu-id="552b0-127">Yukarıdaki eylemlerden hangisini seçtiğinize bağlı olarak, her bir belgeye yalnızca belirli alanlar dahil edilmelidir:</span><span class="sxs-lookup"><span data-stu-id="552b0-127">Depending on which of the below actions you choose, only certain fields must be included for each document:</span></span>

| @search.action | <span data-ttu-id="552b0-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="552b0-128">Description</span></span> | <span data-ttu-id="552b0-129">Her bir belge için gerekli alanlar</span><span class="sxs-lookup"><span data-stu-id="552b0-129">Necessary fields for each document</span></span> | <span data-ttu-id="552b0-130">Notlar</span><span class="sxs-lookup"><span data-stu-id="552b0-130">Notes</span></span> |
| --- | --- | --- | --- |
| `upload` |<span data-ttu-id="552b0-131">Bir `upload` eylemi, belgenin yeni olması durumunda ekleneceği ve var olması durumunda güncelleştirileceği/değiştirileceği bir "upsert" ile benzerlik gösterir.</span><span class="sxs-lookup"><span data-stu-id="552b0-131">An `upload` action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="552b0-132">anahtar ve tanımlamak istediğiniz diğer alanlar</span><span class="sxs-lookup"><span data-stu-id="552b0-132">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="552b0-133">Var olan bir belgeyi güncelleştirirken/değiştirirken istekte belirtilmeyen herhangi bir alan `null` olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="552b0-133">When updating/replacing an existing document, any field that is not specified in the request will have its field set to `null`.</span></span> <span data-ttu-id="552b0-134">Bu durum, alan daha önce değersiz olmayan bir değere ayarlanmış olsa dahi gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="552b0-134">This occurs even when the field was previously set to a non-null value.</span></span> |
| `merge` |<span data-ttu-id="552b0-135">Var olan belgeyi belirtilen alanlarla güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="552b0-135">Updates an existing document with the specified fields.</span></span> <span data-ttu-id="552b0-136">Belge dizinde mevcut değilse birleştirme işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="552b0-136">If the document does not exist in the index, the merge will fail.</span></span> |<span data-ttu-id="552b0-137">anahtar ve tanımlamak istediğiniz diğer alanlar</span><span class="sxs-lookup"><span data-stu-id="552b0-137">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="552b0-138">Birleştirmede belirttiğiniz herhangi bir alan belgede var olan alanın yerini alır.</span><span class="sxs-lookup"><span data-stu-id="552b0-138">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="552b0-139">Buna `Collection(Edm.String)` türünde alanlar dahildir.</span><span class="sxs-lookup"><span data-stu-id="552b0-139">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="552b0-140">Örneğin, belge `["budget"]` değerine sahip bir `tags` alanını içeriyorsa ve `tags` için `["economy", "pool"]` değeriyle bir birleştirme yürütürseniz `tags` alanının son değeri `["economy", "pool"]` olur.</span><span class="sxs-lookup"><span data-stu-id="552b0-140">For example, if the document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, the final value of the `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="552b0-141">`["budget", "economy", "pool"]` olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="552b0-141">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `mergeOrUpload` |<span data-ttu-id="552b0-142">Belirtilen anahtara sahip bir belge dizinde zaten mevcutsa bu eylem `merge` gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="552b0-142">This action behaves like `merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="552b0-143">Belge mevcut değilse yeni bir belgeyle `upload` gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="552b0-143">If the document does not exist, it behaves like `upload` with a new document.</span></span> |<span data-ttu-id="552b0-144">anahtar ve tanımlamak istediğiniz diğer alanlar</span><span class="sxs-lookup"><span data-stu-id="552b0-144">key, plus any other fields you wish to define</span></span> |- |
| `delete` |<span data-ttu-id="552b0-145">Belirtilen belgeyi dizinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="552b0-145">Removes the specified document from the index.</span></span> |<span data-ttu-id="552b0-146">yalnızca anahtar</span><span class="sxs-lookup"><span data-stu-id="552b0-146">key only</span></span> |<span data-ttu-id="552b0-147">Anahtar alanı dışında belirttiğiniz tüm alanlar yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="552b0-147">Any fields you specify other than the key field will be ignored.</span></span> <span data-ttu-id="552b0-148">Bir belgeden tek bir alanı kaldırmak istiyorsanız bunun yerine `merge` kullanıp alanı açık bir şekilde null olarak ayarlamanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="552b0-148">If you want to remove an individual field from a document, use `merge` instead and simply set the field explicitly to null.</span></span> |

## <a name="construct-your-http-request-and-request-body"></a><span data-ttu-id="552b0-149">HTTP isteğinizi ve istek gövdenizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="552b0-149">Construct your HTTP request and request body</span></span>
<span data-ttu-id="552b0-150">Artık dizin eylemleriniz için gerekli alan değerlerini topladığınıza göre, verilerinizi içeri aktarmak için asıl HTTP isteğini ve JSON istek gövdesini oluşturmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="552b0-150">Now that you have gathered the necessary field values for your index actions, you are ready to construct the actual HTTP request and JSON request body to import your data.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="552b0-151">İstek ve İstek Üst Bilgileri</span><span class="sxs-lookup"><span data-stu-id="552b0-151">Request and Request Headers</span></span>
<span data-ttu-id="552b0-152">URL'de hizmet adınızın ve dizin adının (bu durumda "hotels") yanı sıra düzgün API sürümünü (bu belgenin yayımlandığı sırada geçerli API sürümü `2016-09-01`) de sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="552b0-152">In the URL, you will need to provide your service name, index name ("hotels" in this case), as well as the proper API version (the current API version is `2016-09-01` at the time of publishing this document).</span></span> <span data-ttu-id="552b0-153">`Content-Type` ve `api-key` istek üst bilgilerini tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="552b0-153">You will need to define the `Content-Type` and `api-key` request headers.</span></span> <span data-ttu-id="552b0-154">İkincisi için hizmetinizin yönetici anahtarlarından birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="552b0-154">For the latter, use one of your service's admin keys.</span></span>

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a><span data-ttu-id="552b0-155">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="552b0-155">Request Body</span></span>
```JSON
{
    "value": [
        {
            "@search.action": "upload",
            "hotelId": "1",
            "baseRate": 199.0,
            "description": "Best hotel in town",
            "description_fr": "Meilleur hôtel en ville",
            "hotelName": "Fancy Stay",
            "category": "Luxury",
            "tags": ["pool", "view", "wifi", "concierge"],
            "parkingIncluded": false,
            "smokingAllowed": false,
            "lastRenovationDate": "2010-06-27T00:00:00Z",
            "rating": 5,
            "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
            "@search.action": "upload",
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags": ["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
            "@search.action": "mergeOrUpload",
            "hotelId": "3",
            "baseRate": 129.99,
            "description": "Close to town hall and the river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

<span data-ttu-id="552b0-156">Bu durumda arama eylemlerimiz olarak `upload`, `mergeOrUpload` ve `delete` kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="552b0-156">In this case, we are using `upload`, `mergeOrUpload`, and `delete` as our search actions.</span></span>

<span data-ttu-id="552b0-157">Bu "hotels" dizini örneğinin, birçok belgeyle önceden doldurulduğunu varsayın.</span><span class="sxs-lookup"><span data-stu-id="552b0-157">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="552b0-158">`mergeOrUpload` kullanırken olası tüm belge alanlarını belirtmek zorunda kalmadığımıza ve `delete` kullanırken yalnızca belge anahtarını (`hotelId`) belirttiğimize dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="552b0-158">Note how we did not have to specify all the possible document fields when using `mergeOrUpload` and how we only specified the document key (`hotelId`) when using `delete`.</span></span>

<span data-ttu-id="552b0-159">Ayrıca, tek bir dizin oluşturma isteğine yalnızca en fazla 1000 belge (veya 16 MB) dahil edebileceğinizi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="552b0-159">Also, note that you can only include up to 1000 documents (or 16 MB) in a single indexing request.</span></span>

## <a name="understand-your-http-response-code"></a><span data-ttu-id="552b0-160">HTTP yanıt kodunuzu anlama</span><span class="sxs-lookup"><span data-stu-id="552b0-160">Understand your HTTP response code</span></span>
#### <a name="200"></a><span data-ttu-id="552b0-161">200</span><span class="sxs-lookup"><span data-stu-id="552b0-161">200</span></span>
<span data-ttu-id="552b0-162">Başarılı bir dizin oluşturma isteği gönderdikten sonra `200 OK` durum koduna sahip bir HTTP yanıtı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="552b0-162">After submitting a successful indexing request you will receive an HTTP response with status code of `200 OK`.</span></span> <span data-ttu-id="552b0-163">HTTP yanıtının JSON gövdesi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="552b0-163">The JSON body of the HTTP response will be as follows:</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": true,
            "errorMessage": null
        },
        ...
    ]
}
```

#### <a name="207"></a><span data-ttu-id="552b0-164">207</span><span class="sxs-lookup"><span data-stu-id="552b0-164">207</span></span>
<span data-ttu-id="552b0-165">En az bir öğenin dizine alınması başarısız olduğunda `207` durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="552b0-165">A status code of `207` will be returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="552b0-166">HTTP yanıtının JSON gövdesi, başarısız belge/belgeler hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="552b0-166">The JSON body of the HTTP response will contain information about the unsuccessful document(s).</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "The search service is too busy to process this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> <span data-ttu-id="552b0-167">Bu durum genellikle, arama hizmetinizdeki yükün, dizin oluşturma isteklerinin `503` yanıtları döndürmeye başlayacağı bir noktaya eriştiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="552b0-167">This often means that the load on your search service is reaching a point where indexing requests will begin to return `503` responses.</span></span> <span data-ttu-id="552b0-168">Bu durumda, istemci kodunuzun geri alınmasını ve yeniden denemeden önce beklenmesini kesinlikle öneririz.</span><span class="sxs-lookup"><span data-stu-id="552b0-168">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="552b0-169">Böylece kurtulması için sisteme biraz zaman tanınmış ve gelecekteki isteklerin başarılı olma şansı artırılmış olur.</span><span class="sxs-lookup"><span data-stu-id="552b0-169">This will give the system some time to recover, increasing the chances that future requests will succeed.</span></span> <span data-ttu-id="552b0-170">İsteklerinizi hızla yeniden denemeniz bu durumu yalnızca uzatır.</span><span class="sxs-lookup"><span data-stu-id="552b0-170">Rapidly retrying your requests will only prolong the situation.</span></span>
>
>

#### <a name="429"></a><span data-ttu-id="552b0-171">429</span><span class="sxs-lookup"><span data-stu-id="552b0-171">429</span></span>
<span data-ttu-id="552b0-172">Dizin başına belge sayısı kotanızı aştığınızda `429` durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="552b0-172">A status code of `429` will be returned when you have exceeded your quota on the number of documents per index.</span></span>

#### <a name="503"></a><span data-ttu-id="552b0-173">503</span><span class="sxs-lookup"><span data-stu-id="552b0-173">503</span></span>
<span data-ttu-id="552b0-174">İstekteki öğelerin hiçbiri başarılı bir şekilde dizine alınamazsa `503` durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="552b0-174">A status code of `503` will be returned if none of the items in the request were successfully indexed.</span></span> <span data-ttu-id="552b0-175">Bu hata, sistemin aşırı yüklü olduğu ve isteğinizin şu anda işlenemediği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="552b0-175">This error means that the system is under heavy load and your request can't be processed at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="552b0-176">Bu durumda, istemci kodunuzun geri alınmasını ve yeniden denemeden önce beklenmesini kesinlikle öneririz.</span><span class="sxs-lookup"><span data-stu-id="552b0-176">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="552b0-177">Böylece kurtulması için sisteme biraz zaman tanınmış ve gelecekteki isteklerin başarılı olma şansı artırılmış olur.</span><span class="sxs-lookup"><span data-stu-id="552b0-177">This will give the system some time to recover, increasing the chances that future requests will succeed.</span></span> <span data-ttu-id="552b0-178">İsteklerinizi hızla yeniden denemeniz bu durumu yalnızca uzatır.</span><span class="sxs-lookup"><span data-stu-id="552b0-178">Rapidly retrying your requests will only prolong the situation.</span></span>
>
>

<span data-ttu-id="552b0-179">Belge eylemleri ve başarı/hata yanıtları hakkında daha fazla bilgi için lütfen bkz. [Belge Ekleme, Güncelleştirme veya Silme](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span><span class="sxs-lookup"><span data-stu-id="552b0-179">For more information on document actions and success/error responses, please see [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span></span> <span data-ttu-id="552b0-180">Hata durumunda döndürülebilen diğer HTTP durum kodları hakkında daha fazla bilgi için bkz. [HTTP durum kodları (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="552b0-180">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="552b0-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="552b0-181">Next steps</span></span>
<span data-ttu-id="552b0-182">Azure Search dizininizi doldurduktan sonra, belgeleri aramak için sorgu göndermeye başlamaya hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="552b0-182">After populating your Azure Search index, you will be ready to start issuing queries to search for documents.</span></span> <span data-ttu-id="552b0-183">Ayrıntılı bilgi için bkz. [Azure Search Dizininizi Sorgulama](search-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="552b0-183">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>
