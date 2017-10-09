---
title: "aaa \"verileri (REST API - Azure Search) yükleme | Microsoft Docs\""
description: "REST API kullanarak Azure Search tooupload veri tooan dizini hello nasıl öğrenin."
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
ms.openlocfilehash: 6ba1336012d1f0f6d6d6c933e16aa879afb9b824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a><span data-ttu-id="1d653-103">Karşıya veri tooAzure arama'yı kullanarak hello REST API'si</span><span class="sxs-lookup"><span data-stu-id="1d653-103">Upload data tooAzure Search using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="1d653-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="1d653-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="1d653-105">.NET</span><span class="sxs-lookup"><span data-stu-id="1d653-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="1d653-106">REST</span><span class="sxs-lookup"><span data-stu-id="1d653-106">REST</span></span>](search-import-data-rest-api.md)
>
>

<span data-ttu-id="1d653-107">Bu makale size nasıl gösterir toouse hello [Azure Search REST API'sini](https://docs.microsoft.com/rest/api/searchservice/) tooimport verileri Azure Search dizini.</span><span class="sxs-lookup"><span data-stu-id="1d653-107">This article will show you how toouse hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="1d653-108">Bu kılavuza başlamadan önce bir [Azure Search dizini oluşturmuş](search-what-is-an-index.md) olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d653-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span>

<span data-ttu-id="1d653-109">Sipariş toopush belgelerde hello REST API kullanarak dizininizi içine bir HTTP POST isteği tooyour dizinin URL uç gönderirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d653-109">In order toopush documents into your index using hello REST API, you will issue an HTTP POST request tooyour index's URL endpoint.</span></span> <span data-ttu-id="1d653-110">Merhaba gövdesi hello HTTP istek gövdesi toobe eklenen, değiştirilen veya silinen hello belgeleri içeren bir JSON nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="1d653-110">hello body of hello HTTP request body is a JSON object containing hello documents toobe added, modified, or deleted.</span></span>

## <a name="identify-your-azure-search-services-admin-api-key"></a><span data-ttu-id="1d653-111">Azure Search hizmet yöneticinizin api anahtarını tanımlama</span><span class="sxs-lookup"><span data-stu-id="1d653-111">Identify your Azure Search service's admin api-key</span></span>
<span data-ttu-id="1d653-112">Merhaba REST API kullanarak hizmetinize karşı HTTP istekleri gönderirken *her* API isteğinin sağladığınız Search Hizmeti hello için oluşturulan hello API-anahtarını içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d653-112">When issuing HTTP requests against your service using hello REST API, *each* API request must include hello api-key that was generated for hello Search service you provisioned.</span></span> <span data-ttu-id="1d653-113">Geçerli bir anahtar sahip istek başına temelinde, hello isteği gönderiliyor hello uygulama ve bunu işleyen hello hizmeti arasında güven oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1d653-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="1d653-114">toofind hizmetinizin api anahtarlarından, toohello kaydolabilirsiniz [Azure portalı](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="1d653-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="1d653-115">Tooyour Azure Search hizmet dikey penceresine gidin</span><span class="sxs-lookup"><span data-stu-id="1d653-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="1d653-116">Merhaba üzerinde "Anahtarlar" simgesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="1d653-116">Click on hello "Keys" icon</span></span>

<span data-ttu-id="1d653-117">Hizmetiniz, *yönetici anahtarlarına* ve *sorgu anahtarlarına* sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1d653-117">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="1d653-118">Birincil ve ikincil *yönetici anahtarları* tooall operations hello özelliği toomanage hello hizmeti dahil olmak üzere, tam haklar, oluşturun ve dizinler, dizin oluşturucular ve veri kaynaklarını silin.</span><span class="sxs-lookup"><span data-stu-id="1d653-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="1d653-119">Tooregenerate hello birincil anahtar ve tam tersini karar verirseniz toouse hello ikincil anahtar devam edebilmesi için bu iki anahtar vardır.</span><span class="sxs-lookup"><span data-stu-id="1d653-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="1d653-120">*Sorgu anahtarları* salt okunur erişim tooindexes ve belgeleri verin ve arama istekleri gönderen genellikle dağıtılmış tooclient uygulamalardır.</span><span class="sxs-lookup"><span data-stu-id="1d653-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="1d653-121">Merhaba amacıyla bir dizine veri alma ya da kullanabilirsiniz, birincil veya ikincil yönetici anahtarınızı.</span><span class="sxs-lookup"><span data-stu-id="1d653-121">For hello purposes of importing data into an index, you can use either your primary or secondary admin key.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="1d653-122">Hangi dizin oluşturma eylemini toouse karar verin</span><span class="sxs-lookup"><span data-stu-id="1d653-122">Decide which indexing action toouse</span></span>
<span data-ttu-id="1d653-123">Merhaba REST API kullanırken, JSON istek gövdesi tooyour Azure Search dizinine ait uç nokta URL'si ile HTTP POST istekleri gönderirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d653-123">When using hello REST API, you will issue HTTP POST requests with JSON request bodies tooyour Azure Search index's endpoint URL.</span></span> <span data-ttu-id="1d653-124">HTTP isteği gövdesinin Hello JSON nesnesinde, tek bir JSON dizisi içerecek "tooadd tooyour dizin istediğiniz belgeleri temsil eden JSON nesnelerini içeren değer" adlı, güncelleştirme veya silme.</span><span class="sxs-lookup"><span data-stu-id="1d653-124">hello JSON object in your HTTP request body will contain a single JSON array named "value" containing JSON objects representing documents you would like tooadd tooyour index, update, or delete.</span></span>

<span data-ttu-id="1d653-125">Merhaba "value" dizisindeki her bir JSON nesnesi, dizine bir belge toobe temsil eder.</span><span class="sxs-lookup"><span data-stu-id="1d653-125">Each JSON object in hello "value" array represents a document toobe indexed.</span></span> <span data-ttu-id="1d653-126">Bu nesnelerin her biri hello belgenin anahtarını içerir ve istenen hello dizin oluşturma eylemini (karşıya yükleme, birleştirme, silme, vb.) belirtir.</span><span class="sxs-lookup"><span data-stu-id="1d653-126">Each of these objects contains hello document's key and specifies hello desired indexing action (upload, merge, delete, etc).</span></span> <span data-ttu-id="1d653-127">Seçtiğiniz Eylemler aşağıda hello bağlı olarak, yalnızca belirli alanlar her belge için dahil edilmelidir:</span><span class="sxs-lookup"><span data-stu-id="1d653-127">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| @search.action | <span data-ttu-id="1d653-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1d653-128">Description</span></span> | <span data-ttu-id="1d653-129">Her bir belge için gerekli alanlar</span><span class="sxs-lookup"><span data-stu-id="1d653-129">Necessary fields for each document</span></span> | <span data-ttu-id="1d653-130">Notlar</span><span class="sxs-lookup"><span data-stu-id="1d653-130">Notes</span></span> |
| --- | --- | --- | --- |
| `upload` |<span data-ttu-id="1d653-131">Bir `upload` benzer tooan "upsert" nerede hello belgenin yeni olması durumunda ekleneceği ve olması mevcut durumunda güncelleştirileceği/değiştirileceği bir eylemdir.</span><span class="sxs-lookup"><span data-stu-id="1d653-131">An `upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="1d653-132">anahtar ve toodefine istediğiniz diğer alanlar</span><span class="sxs-lookup"><span data-stu-id="1d653-132">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="1d653-133">Güncelleştirme/var olan bir belgeyi değiştirirken, hello istekte belirtilen olmayan herhangi bir alan kendi alan çok kümesini sahip`null`.</span><span class="sxs-lookup"><span data-stu-id="1d653-133">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="1d653-134">Bu durum, hatta hello alan tooa null olmayan değer önceden ayarlandı oluşur.</span><span class="sxs-lookup"><span data-stu-id="1d653-134">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `merge` |<span data-ttu-id="1d653-135">Varolan bir belge ile Merhaba güncelleştirmeleri alanları belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="1d653-135">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="1d653-136">Merhaba belge hello dizininde mevcut değilse hello birleştirme işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="1d653-136">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="1d653-137">anahtar ve toodefine istediğiniz diğer alanlar</span><span class="sxs-lookup"><span data-stu-id="1d653-137">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="1d653-138">Birleştirmede belirttiğiniz herhangi bir alan varolan bir alana hello hello belgedeki yerini alır.</span><span class="sxs-lookup"><span data-stu-id="1d653-138">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="1d653-139">Buna `Collection(Edm.String)` türünde alanlar dahildir.</span><span class="sxs-lookup"><span data-stu-id="1d653-139">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="1d653-140">Örneğin, hello belge bir alanı varsa, `tags` değerle `["budget"]` ve değeriyle bir birleştirme yürütme `["economy", "pool"]` için `tags`, hello hello son değerini `tags` alan `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="1d653-140">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="1d653-141">`["budget", "economy", "pool"]` olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="1d653-141">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `mergeOrUpload` |<span data-ttu-id="1d653-142">Bu eylem gibi davranır `merge` anahtar zaten verilen hello belgeyle hello dizinde varsa.</span><span class="sxs-lookup"><span data-stu-id="1d653-142">This action behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="1d653-143">Merhaba belge mevcut değilse gibi davranır `upload` yeni bir belgeyle.</span><span class="sxs-lookup"><span data-stu-id="1d653-143">If hello document does not exist, it behaves like `upload` with a new document.</span></span> |<span data-ttu-id="1d653-144">anahtar ve toodefine istediğiniz diğer alanlar</span><span class="sxs-lookup"><span data-stu-id="1d653-144">key, plus any other fields you wish toodefine</span></span> |- |
| `delete` |<span data-ttu-id="1d653-145">Merhaba belirtilen belge hello dizinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1d653-145">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="1d653-146">yalnızca anahtar</span><span class="sxs-lookup"><span data-stu-id="1d653-146">key only</span></span> |<span data-ttu-id="1d653-147">Merhaba anahtar alanı yoksayılacak dışında belirttiğiniz tüm alanlar.</span><span class="sxs-lookup"><span data-stu-id="1d653-147">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="1d653-148">Bir belgeden tek bir alanı tooremove istiyorsanız kullanın `merge` yerine ve basit şekilde hello alan açık olarak ayarlanıp toonull.</span><span class="sxs-lookup"><span data-stu-id="1d653-148">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly toonull.</span></span> |

## <a name="construct-your-http-request-and-request-body"></a><span data-ttu-id="1d653-149">HTTP isteğinizi ve istek gövdenizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1d653-149">Construct your HTTP request and request body</span></span>
<span data-ttu-id="1d653-150">Dizin eylemleriniz için hello gerekli alan değerlerini topladıktan, hazır tooconstruct hello asıl HTTP isteğini olan ve JSON istek gövdesi tooimport verilerinizi.</span><span class="sxs-lookup"><span data-stu-id="1d653-150">Now that you have gathered hello necessary field values for your index actions, you are ready tooconstruct hello actual HTTP request and JSON request body tooimport your data.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="1d653-151">İstek ve İstek Üst Bilgileri</span><span class="sxs-lookup"><span data-stu-id="1d653-151">Request and Request Headers</span></span>
<span data-ttu-id="1d653-152">Merhaba URL'de tooprovide, hizmet adı, dizin adı (Bu durumda "hotels") yanı sıra düzgün API sürümünü hello gerekir (Merhaba geçerli API sürümü `2016-09-01` bu belgenin yayımlandığı hello zaman).</span><span class="sxs-lookup"><span data-stu-id="1d653-152">In hello URL, you will need tooprovide your service name, index name ("hotels" in this case), as well as hello proper API version (hello current API version is `2016-09-01` at hello time of publishing this document).</span></span> <span data-ttu-id="1d653-153">Toodefine hello gerekir `Content-Type` ve `api-key` istek üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="1d653-153">You will need toodefine hello `Content-Type` and `api-key` request headers.</span></span> <span data-ttu-id="1d653-154">İkinci Hello için hizmetinizin yönetici anahtarlarından birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1d653-154">For hello latter, use one of your service's admin keys.</span></span>

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a><span data-ttu-id="1d653-155">İstek Gövdesi</span><span class="sxs-lookup"><span data-stu-id="1d653-155">Request Body</span></span>
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
            "description": "Close tootown hall and hello river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

<span data-ttu-id="1d653-156">Bu durumda arama eylemlerimiz olarak `upload`, `mergeOrUpload` ve `delete` kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="1d653-156">In this case, we are using `upload`, `mergeOrUpload`, and `delete` as our search actions.</span></span>

<span data-ttu-id="1d653-157">Bu "hotels" dizini örneğinin, birçok belgeyle önceden doldurulduğunu varsayın.</span><span class="sxs-lookup"><span data-stu-id="1d653-157">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="1d653-158">Nasıl biz toospecify tüm hello olası belge alanlarını kullanırken sahip değildi Not `mergeOrUpload` ve yalnızca hello belge anahtarını belirttiğimize (`hotelId`) kullanırken `delete`.</span><span class="sxs-lookup"><span data-stu-id="1d653-158">Note how we did not have toospecify all hello possible document fields when using `mergeOrUpload` and how we only specified hello document key (`hotelId`) when using `delete`.</span></span>

<span data-ttu-id="1d653-159">Ayrıca, yalnızca too1000 belgeleri (veya 16 MB) tek bir dizin oluşturma isteğine dahil edebileceğinizi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1d653-159">Also, note that you can only include up too1000 documents (or 16 MB) in a single indexing request.</span></span>

## <a name="understand-your-http-response-code"></a><span data-ttu-id="1d653-160">HTTP yanıt kodunuzu anlama</span><span class="sxs-lookup"><span data-stu-id="1d653-160">Understand your HTTP response code</span></span>
#### <a name="200"></a><span data-ttu-id="1d653-161">200</span><span class="sxs-lookup"><span data-stu-id="1d653-161">200</span></span>
<span data-ttu-id="1d653-162">Başarılı bir dizin oluşturma isteği gönderdikten sonra `200 OK` durum koduna sahip bir HTTP yanıtı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="1d653-162">After submitting a successful indexing request you will receive an HTTP response with status code of `200 OK`.</span></span> <span data-ttu-id="1d653-163">Merhaba hello HTTP yanıtının JSON gövdesi aşağıdaki gibi olur:</span><span class="sxs-lookup"><span data-stu-id="1d653-163">hello JSON body of hello HTTP response will be as follows:</span></span>

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

#### <a name="207"></a><span data-ttu-id="1d653-164">207</span><span class="sxs-lookup"><span data-stu-id="1d653-164">207</span></span>
<span data-ttu-id="1d653-165">En az bir öğenin dizine alınması başarısız olduğunda `207` durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1d653-165">A status code of `207` will be returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="1d653-166">Merhaba hello HTTP yanıtının JSON gövdesi hello başarısız belgeler hakkındaki bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="1d653-166">hello JSON body of hello HTTP response will contain information about hello unsuccessful document(s).</span></span>

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "hello search service is too busy tooprocess this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> <span data-ttu-id="1d653-167">Bu genellikle hello yük gelir aramanızı hizmet burada dizin oluşturma isteklerinin başlayacak tooreturn bir noktaya eriştiği `503` yanıtlar.</span><span class="sxs-lookup"><span data-stu-id="1d653-167">This often means that hello load on your search service is reaching a point where indexing requests will begin tooreturn `503` responses.</span></span> <span data-ttu-id="1d653-168">Bu durumda, istemci kodunuzun geri alınmasını ve yeniden denemeden önce beklenmesini kesinlikle öneririz.</span><span class="sxs-lookup"><span data-stu-id="1d653-168">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="1d653-169">Gelecekteki isteklerin başarılı olma hello şansı artırılmış bazı zaman toorecover hello sistem verir.</span><span class="sxs-lookup"><span data-stu-id="1d653-169">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="1d653-170">İsteklerinizi hızla yeniden hello durumu yalnızca uzatır.</span><span class="sxs-lookup"><span data-stu-id="1d653-170">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

#### <a name="429"></a><span data-ttu-id="1d653-171">429</span><span class="sxs-lookup"><span data-stu-id="1d653-171">429</span></span>
<span data-ttu-id="1d653-172">Durum kodu `429` hello dizin başına belge sayısı kotanızı aştığınızda döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1d653-172">A status code of `429` will be returned when you have exceeded your quota on hello number of documents per index.</span></span>

#### <a name="503"></a><span data-ttu-id="1d653-173">503</span><span class="sxs-lookup"><span data-stu-id="1d653-173">503</span></span>
<span data-ttu-id="1d653-174">Durum kodu `503` hello isteği hello öğelerde hiçbiri başarılı bir şekilde dizine alınamazsa döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1d653-174">A status code of `503` will be returned if none of hello items in hello request were successfully indexed.</span></span> <span data-ttu-id="1d653-175">Bu hata, ağır yük altında hello sistemidir ve isteğiniz şu anda işlenemiyor anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1d653-175">This error means that hello system is under heavy load and your request can't be processed at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="1d653-176">Bu durumda, istemci kodunuzun geri alınmasını ve yeniden denemeden önce beklenmesini kesinlikle öneririz.</span><span class="sxs-lookup"><span data-stu-id="1d653-176">In this case, we highly recommend that your client code back off and wait before retrying.</span></span> <span data-ttu-id="1d653-177">Gelecekteki isteklerin başarılı olma hello şansı artırılmış bazı zaman toorecover hello sistem verir.</span><span class="sxs-lookup"><span data-stu-id="1d653-177">This will give hello system some time toorecover, increasing hello chances that future requests will succeed.</span></span> <span data-ttu-id="1d653-178">İsteklerinizi hızla yeniden hello durumu yalnızca uzatır.</span><span class="sxs-lookup"><span data-stu-id="1d653-178">Rapidly retrying your requests will only prolong hello situation.</span></span>
>
>

<span data-ttu-id="1d653-179">Belge eylemleri ve başarı/hata yanıtları hakkında daha fazla bilgi için lütfen bkz. [Belge Ekleme, Güncelleştirme veya Silme](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span><span class="sxs-lookup"><span data-stu-id="1d653-179">For more information on document actions and success/error responses, please see [Add, Update, or Delete Documents](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents).</span></span> <span data-ttu-id="1d653-180">Hata durumunda döndürülebilen diğer HTTP durum kodları hakkında daha fazla bilgi için bkz. [HTTP durum kodları (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="1d653-180">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d653-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1d653-181">Next steps</span></span>
<span data-ttu-id="1d653-182">Azure Search dizininizi doldurduktan sonra belgeler için sorguları toosearch veren hazır toostart olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1d653-182">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="1d653-183">Ayrıntılı bilgi için bkz. [Azure Search Dizininizi Sorgulama](search-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d653-183">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>
