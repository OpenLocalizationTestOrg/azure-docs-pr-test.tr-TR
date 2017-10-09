---
title: "Arama hizmeti REST API sürümü 2015-02-28-Önizleme aaaAzure | Microsoft Docs"
description: "Azure Search Hizmeti REST API sürümü 2015-02-28-Önizleme doğal dil Çözümleyicileri ve moreLikeThis aramaları gibi Deneysel özellikler içerir."
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="86e86-103">Azure Search Hizmeti REST API'si: Sürüm 2015-02-28-Önizleme</span><span class="sxs-lookup"><span data-stu-id="86e86-103">Azure Search Service REST API: Version 2015-02-28-Preview</span></span>
<span data-ttu-id="86e86-104">Bu makalede hello başvurusu için belgesidir `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="86e86-104">This article is hello reference documentation for `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="86e86-105">Bu önizleme hello geçerli genel olarak kullanılabilir sürümü, genişletir [api-version = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), Deneysel özellikleri aşağıdaki hello sağlayarak:</span><span class="sxs-lookup"><span data-stu-id="86e86-105">This preview extends hello current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing hello following experimental features:</span></span>

* <span data-ttu-id="86e86-106">`moreLikeThis`sorgu parametresi hello içinde [Search belgeleri](#SearchDocs) API.</span><span class="sxs-lookup"><span data-stu-id="86e86-106">`moreLikeThis` query parameter in hello [Search Documents](#SearchDocs) API.</span></span> <span data-ttu-id="86e86-107">İlgili tooanother belirli belge olan diğer belgeleri bulur.</span><span class="sxs-lookup"><span data-stu-id="86e86-107">It finds other documents that are relevant tooanother specific document.</span></span>

<span data-ttu-id="86e86-108">Merhaba birkaç ek bölümlerini `2015-02-28-Preview` REST API ayrı olarak belgelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="86e86-108">A few additional parts of hello `2015-02-28-Preview` REST API are documented separately.</span></span> <span data-ttu-id="86e86-109">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="86e86-109">These include:</span></span>

* [<span data-ttu-id="86e86-110">Puanlama profili</span><span class="sxs-lookup"><span data-stu-id="86e86-110">Scoring Profiles</span></span>](search-api-scoring-profiles-2015-02-28-preview.md)
* [<span data-ttu-id="86e86-111">Dizin Oluşturucular</span><span class="sxs-lookup"><span data-stu-id="86e86-111">Indexers</span></span>](search-api-indexers-2015-02-28-preview.md)

<span data-ttu-id="86e86-112">Azure Search hizmeti birden çok sürümlerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-112">Azure Search service is available in multiple versions.</span></span> <span data-ttu-id="86e86-113">Lütfen çok başvurun[arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="86e86-113">Please refer too[Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span></span>

## <a name="apis-in-this-document"></a><span data-ttu-id="86e86-114">Bu belgedeki API'leri</span><span class="sxs-lookup"><span data-stu-id="86e86-114">APIs in this document</span></span>
<span data-ttu-id="86e86-115">Azure Search Hizmeti API'si API işlemleri için iki URL sözdizimleri destekler: Basit ve OData (bkz [OData (Azure Search API) için destek](http://msdn.microsoft.com/library/azure/dn798932.aspx) Ayrıntılar için).</span><span class="sxs-lookup"><span data-stu-id="86e86-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span></span> <span data-ttu-id="86e86-116">Merhaba aşağıdaki listede hello basit sözdizimi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="86e86-116">hello following list shows hello simple syntax.</span></span>

[<span data-ttu-id="86e86-117">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="86e86-117">Create Index</span></span>](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="86e86-118">Dizini Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="86e86-118">Update Index</span></span>](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="86e86-119">Dizin Al</span><span class="sxs-lookup"><span data-stu-id="86e86-119">Get Index</span></span>](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="86e86-120">Dizinleri listeleme</span><span class="sxs-lookup"><span data-stu-id="86e86-120">Listing Indexes</span></span>](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="86e86-121">Dizin istatistikleri Al</span><span class="sxs-lookup"><span data-stu-id="86e86-121">Get Index Statistics</span></span>](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[<span data-ttu-id="86e86-122">Testi Çözümleyicisi</span><span class="sxs-lookup"><span data-stu-id="86e86-122">Test Analyzer</span></span>](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[<span data-ttu-id="86e86-123">Dizin silme</span><span class="sxs-lookup"><span data-stu-id="86e86-123">Delete an Index</span></span>](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="86e86-124">Ekleme, silme ve dizin içindeki verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="86e86-124">Add, Delete, and Update Data within an Index</span></span>](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[<span data-ttu-id="86e86-125">Belge ara</span><span class="sxs-lookup"><span data-stu-id="86e86-125">Search Documents</span></span>](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[<span data-ttu-id="86e86-126">Arama belge</span><span class="sxs-lookup"><span data-stu-id="86e86-126">Lookup Document</span></span>](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[<span data-ttu-id="86e86-127">Count belgeleri</span><span class="sxs-lookup"><span data-stu-id="86e86-127">Count Documents</span></span>](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[<span data-ttu-id="86e86-128">Öneriler</span><span class="sxs-lookup"><span data-stu-id="86e86-128">Suggestions</span></span>](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a><span data-ttu-id="86e86-129">Dizin işlemleri</span><span class="sxs-lookup"><span data-stu-id="86e86-129">Index Operations</span></span>
<span data-ttu-id="86e86-130">Oluşturun ve Azure Search hizmeti belirtilen dizin kaynak basit HTTP isteklerini (POST, GET, PUT, DELETE) aracılığıyla dizinlerde yönetin.</span><span class="sxs-lookup"><span data-stu-id="86e86-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span></span> <span data-ttu-id="86e86-131">toocreate dizini bir ilk hello dizin şemasını tanımlayan bir JSON belgesi gönderin.</span><span class="sxs-lookup"><span data-stu-id="86e86-131">toocreate an index, you first POST a JSON document that describes hello index schema.</span></span> <span data-ttu-id="86e86-132">Merhaba şema başlangıç dizini, kendi veri türleri ve nasıl (örneğin, tam metin araması, filtre, sıralama veya olduğunu) kullanılabilmesi için hello alanları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="86e86-132">hello schema defines hello fields of hello index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span></span> <span data-ttu-id="86e86-133">Ayrıca, Puanlama profilleri, ilgili ve hello dizin diğer öznitelikleri tooconfigure hello davranışını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="86e86-133">It also defines scoring profiles, suggesters and other attributes tooconfigure hello behavior of hello index.</span></span>

<span data-ttu-id="86e86-134">Merhaba aşağıdaki örnekte iki dillerde tanımlanan hello açıklama alanı ile otel bilgi aramak için kullanılan bir şema bir çizimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="86e86-134">hello following example provides an illustration of a schema used for searching on hotel information with hello Description field defined in two languages.</span></span> <span data-ttu-id="86e86-135">Nasıl öznitelikleri hello alanın nasıl kullanıldığını kontrol dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="86e86-135">Notice how attributes control how hello field is used.</span></span> <span data-ttu-id="86e86-136">Örneğin hello `hotelId` hello belge anahtarı olarak kullanılan (`"key": true`) ve tam metin aramalardan dışlandı (`"searchable": false`).</span><span class="sxs-lookup"><span data-stu-id="86e86-136">For example hello `hotelId` is used as hello document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span></span>

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

<span data-ttu-id="86e86-137">Merhaba dizin oluşturulduktan sonra başlangıç dizinini doldurmak belgeleri yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="86e86-137">After hello index is created, you'll upload documents that populate hello index.</span></span> <span data-ttu-id="86e86-138">Bkz: [ekleme veya güncelleştirme belgeler](#AddOrUpdateDocuments) bu sonraki adım için.</span><span class="sxs-lookup"><span data-stu-id="86e86-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span></span>

<span data-ttu-id="86e86-139">Azure Search'te bir video girişi tooindexing için hello bkz [kanal 9 bulut kapak bölüm Azure Search üzerinde](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span><span class="sxs-lookup"><span data-stu-id="86e86-139">For a video introduction tooindexing in Azure Search, see hello [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span></span>

<a name="CreateIndex"></a>

## <a name="create-index"></a><span data-ttu-id="86e86-140">Dizin Oluşturma</span><span class="sxs-lookup"><span data-stu-id="86e86-140">Create Index</span></span>
<span data-ttu-id="86e86-141">Bir dizin düzenleme ve belgeler Azure Search'te arama hello birincil anlamına gelir, veritabanındaki kayıtları benzer toohow tablo düzenler.</span><span class="sxs-lookup"><span data-stu-id="86e86-141">An index is hello primary means of organizing and searching documents in Azure Search, similar toohow a table organizes records in a database.</span></span> <span data-ttu-id="86e86-142">Her dizin tüm toohello dizin şemasını (alan adları, veri türleri ve özellikleri) uygun ancak dizinler de diğer arama davranışları tanımlamak ek yapıları (ilgili, Puanlama profilleri ve CORS seçenekleri) belirtmeniz belgeleri koleksiyonu vardır.</span><span class="sxs-lookup"><span data-stu-id="86e86-142">Each index has a collection of documents that all conform toohello index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span></span>

<span data-ttu-id="86e86-143">Bir HTTP POST veya PUT İsteği kullanarak Azure Search hizmeti içinde yeni bir dizin oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86e86-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span></span> <span data-ttu-id="86e86-144">Merhaba hello istek gövdesi başlangıç dizini ve yapılandırma bilgileri belirten bir JSON Şeması ' dir.</span><span class="sxs-lookup"><span data-stu-id="86e86-144">hello body of hello request is a JSON schema that specifies hello index and configuration information.</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="86e86-145">Alternatif olarak, PUT kullanın ve URI hello üzerinde hello dizin adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="86e86-145">Alternatively, you can use PUT and specify hello index name on hello URI.</span></span> <span data-ttu-id="86e86-146">Merhaba dizin yoksa, oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="86e86-146">If hello index does not exist, it will be created.</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

<span data-ttu-id="86e86-147">Dizin oluşturma depolanır ve arama işlemlerinin kullanılan hello belgelerinin hello yapısını belirler.</span><span class="sxs-lookup"><span data-stu-id="86e86-147">Creating an index determines hello structure of hello documents stored and used in search operations.</span></span> <span data-ttu-id="86e86-148">Doldurma hello dizin ayrı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="86e86-148">Populating hello index is a separate operation.</span></span> <span data-ttu-id="86e86-149">Bu adım için kullanabileceğiniz bir [dizin oluşturucu](https://msdn.microsoft.com/library/azure/mt183328.aspx) (desteklenen veri kaynakları için kullanılabilir) veya bir [Ekle, güncelleştirme veya silme belgeleri](https://msdn.microsoft.com/library/azure/dn798930.aspx) işlemi.</span><span class="sxs-lookup"><span data-stu-id="86e86-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span></span> <span data-ttu-id="86e86-150">Merhaba belgeleri gönderilen ters hello dizin oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="86e86-150">hello inverted index is generated when hello documents are posted.</span></span>

<span data-ttu-id="86e86-151">**Not**: hello dizinleri izin verilen maksimum sayısı değişir fiyatlandırma katmanı tarafından.</span><span class="sxs-lookup"><span data-stu-id="86e86-151">**Note**: hello maximum number of indexes allowed varies by pricing tier.</span></span> <span data-ttu-id="86e86-152">Merhaba ücretsiz hizmet too3 dizinlerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="86e86-152">hello free service allows up too3 indexes.</span></span> <span data-ttu-id="86e86-153">Standart hizmeti arama hizmeti başına 50 dizinleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="86e86-153">Standard service allows 50 indexes per Search service.</span></span> <span data-ttu-id="86e86-154">Bkz: [sınırları ve kısıtlamaları](http://msdn.microsoft.com/library/azure/dn798934.aspx) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="86e86-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span></span>

<span data-ttu-id="86e86-155">**İstek**</span><span class="sxs-lookup"><span data-stu-id="86e86-155">**Request**</span></span>

<span data-ttu-id="86e86-156">HTTPS tüm hizmet istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="86e86-157">Merhaba **Create Index** isteği POST veya PUT yöntemini kullanan olacak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="86e86-157">hello **Create Index** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="86e86-158">POST kullanırken hello dizin şeması tanımı birlikte hello istek gövdesinde bir dizin adı sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-158">When using POST, you must provide an index name in hello request body along with hello index schema definition.</span></span> <span data-ttu-id="86e86-159">PUT ile Merhaba dizin adı hello URL bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-159">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="86e86-160">Merhaba dizin yoksa, oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="86e86-160">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="86e86-161">Zaten varsa, güncelleştirilmiş toohello yeni tanımı var.</span><span class="sxs-lookup"><span data-stu-id="86e86-161">If it already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="86e86-162">Merhaba dizin adı gerekir küçük olması, bir harf veya sayı ile başlamalı, hiçbir eğik çizgi veya nokta olan ve 128 karakterden kısa olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-162">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="86e86-163">Merhaba tire ardışık olmayan sürece hello dizin adı bir harf veya sayı ile başlattıktan sonra hello rest hello adının herhangi harf, sayı ve kısa çizgi, içerebilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-163">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="86e86-164">Merhaba `api-version` gereklidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-164">hello `api-version` is required.</span></span> <span data-ttu-id="86e86-165">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) kullanılabilir sürümlerin listesi için.</span><span class="sxs-lookup"><span data-stu-id="86e86-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span></span>

<span data-ttu-id="86e86-166">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="86e86-166">**Request Headers**</span></span>

<span data-ttu-id="86e86-167">liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.</span><span class="sxs-lookup"><span data-stu-id="86e86-167">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="86e86-168">`Content-Type`: Gerekli.</span><span class="sxs-lookup"><span data-stu-id="86e86-168">`Content-Type`: Required.</span></span> <span data-ttu-id="86e86-169">Bu çok ayarlama`application/json`</span><span class="sxs-lookup"><span data-stu-id="86e86-169">Set this too`application/json`</span></span>
* <span data-ttu-id="86e86-170">`api-key`: Gerekli.</span><span class="sxs-lookup"><span data-stu-id="86e86-170">`api-key`: Required.</span></span> <span data-ttu-id="86e86-171">Merhaba `api-key` için kullanılır</span><span class="sxs-lookup"><span data-stu-id="86e86-171">hello `api-key` is used to</span></span>
* <span data-ttu-id="86e86-172">Merhaba isteği tooyour arama hizmeti kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="86e86-172">authenticate hello request tooyour Search service.</span></span> <span data-ttu-id="86e86-173">Bu bir dize değeri, benzersiz tooyour hizmeti olur.</span><span class="sxs-lookup"><span data-stu-id="86e86-173">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="86e86-174">Merhaba **Create Index** isteği içermelidir bir `api-key` üstbilgi tooyour yönetici anahtarını (karşılıklı tooa sorgu anahtarı) olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="86e86-174">hello **Create Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="86e86-175">Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-175">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="86e86-176">Her iki hello hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan.</span><span class="sxs-lookup"><span data-stu-id="86e86-176">You can get both hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="86e86-177">Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="86e86-177">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="86e86-178"><a name="RequestData"></a>
**İstek gövdesi sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="86e86-178"><a name="RequestData"></a>
**Request Body Syntax**</span></span>

<span data-ttu-id="86e86-179">veri türleri, öznitelikler yanı sıra, isteğe bağlı bir profilleri Puanlama listesi bu dizine beslenecek belgeleri içindeki veri alanlarını hello listesini içeren bir şema tanımı Hello hello istek gövdesini içeren, belgeleri eşleşen kullanılan tooscore Sorgu saati.</span><span class="sxs-lookup"><span data-stu-id="86e86-179">hello body of hello request contains a schema definition, which includes hello list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used tooscore matching documents at query time.</span></span>

<span data-ttu-id="86e86-180">Bir POST isteği unutmayın, hello istek gövdesinde hello dizin adı belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-180">Note that for a POST request, you must specify hello index name in hello request body.</span></span>

<span data-ttu-id="86e86-181">Yalnızca olabilir bir anahtar alanı hello dizininde.</span><span class="sxs-lookup"><span data-stu-id="86e86-181">There can only be one key field in hello index.</span></span> <span data-ttu-id="86e86-182">Bir dize alanı toobe içeriyor.</span><span class="sxs-lookup"><span data-stu-id="86e86-182">It has toobe a string field.</span></span> <span data-ttu-id="86e86-183">Bu alan hello dizini içinde depolanan her belge için benzersiz tanımlayıcı hello temsil eder.</span><span class="sxs-lookup"><span data-stu-id="86e86-183">This field represents hello unique identifier for each document stored within hello index.</span></span>

<span data-ttu-id="86e86-184">Merhaba ana dizin bölümlerini hello şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="86e86-184">hello main parts of an index include hello following:</span></span>

* `name`
* <span data-ttu-id="86e86-185">`fields`Bu ad, veri türü ve bu alan izin verilen eylemleri tanımlayan özellikleri dahil olmak üzere bu dizinine beslenecek.</span><span class="sxs-lookup"><span data-stu-id="86e86-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span></span>
* <span data-ttu-id="86e86-186">`suggesters`otomatik tamamlamayı veya yazarken tamamlanan sorgular için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="86e86-186">`suggesters` used for auto-complete or type-ahead queries.</span></span>
* <span data-ttu-id="86e86-187">`scoringProfiles`Derecelendirme özel arama puanı için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="86e86-187">`scoringProfiles` used for custom search score ranking.</span></span> <span data-ttu-id="86e86-188">Bkz: [Puanlama profili Ekle](https://msdn.microsoft.com/library/azure/dn798928.aspx) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="86e86-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span></span>
* <span data-ttu-id="86e86-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` nasıl belgeleri/sorgularınızı bozuk dizine ve arama yapılabilir belirteçlere toodefine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="86e86-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used toodefine how your documents/queries are broken into indexable/searchable tokens.</span></span> <span data-ttu-id="86e86-190">Bkz: [analiz Azure Search'te](https://aka.ms//azsanalysis) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="86e86-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span></span>
* <span data-ttu-id="86e86-191">`defaultScoringProfile`toooverwrite hello varsayılan davranışlar Puanlama kullanılır.</span><span class="sxs-lookup"><span data-stu-id="86e86-191">`defaultScoringProfile` used toooverwrite hello default scoring behaviors.</span></span>
* <span data-ttu-id="86e86-192">`corsOptions`dizininizi tooallow çıkış noktaları arası sorguları.</span><span class="sxs-lookup"><span data-stu-id="86e86-192">`corsOptions` tooallow cross-origin queries against your index.</span></span>

<span data-ttu-id="86e86-193">Merhaba isteği yükü yapılandırılması hello söz dizimi aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-193">hello syntax for structuring hello request payload is as follows.</span></span> <span data-ttu-id="86e86-194">Örnek istek, bu konuda daha üzerinde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="86e86-194">A sample request is provided further on in this topic.</span></span>

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

<span data-ttu-id="86e86-195">**Dizin öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="86e86-195">**Index Attributes**</span></span>

<span data-ttu-id="86e86-196">Merhaba aşağıdaki öznitelikleri dizin oluşturulurken ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-196">hello following attributes can be set when creating an index.</span></span> <span data-ttu-id="86e86-197">Puanlama ve puanlama profilleri hakkında daha fazla bilgi için bkz [eklemek profilleri Puanlama](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="86e86-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span>

<span data-ttu-id="86e86-198">`name`-Ayarlar hello alanın adını hello.</span><span class="sxs-lookup"><span data-stu-id="86e86-198">`name` - Sets hello name of hello field.</span></span>

<span data-ttu-id="86e86-199">`type`-Ayarlar hello alanın veri türünü hello.</span><span class="sxs-lookup"><span data-stu-id="86e86-199">`type` - Sets hello data type for hello field.</span></span>

<span data-ttu-id="86e86-200">`searchable`-Hello alan tam metin arama yapabilir işaretler.</span><span class="sxs-lookup"><span data-stu-id="86e86-200">`searchable` - Marks hello field as full-text search-able.</span></span> <span data-ttu-id="86e86-201">Başka bir deyişle, dizin oluşturma sırasında sözcük bölme gibi analiz yapılacaktır.</span><span class="sxs-lookup"><span data-stu-id="86e86-201">This means it will undergo analysis such as word-breaking during indexing.</span></span> <span data-ttu-id="86e86-202">Ayarlarsanız bir `searchable` alan tooa değeri "güneşli gün" gibi dahili olarak "güneşli" ve "gün" Merhaba tek tek belirteçlere bölme.</span><span class="sxs-lookup"><span data-stu-id="86e86-202">If you set a `searchable` field tooa value like "sunny day", internally it will be split into hello individual tokens "sunny" and "day".</span></span> <span data-ttu-id="86e86-203">Bu, bu koşulları için tam metin araması sağlar.</span><span class="sxs-lookup"><span data-stu-id="86e86-203">This enables full-text searches for these terms.</span></span> <span data-ttu-id="86e86-204">Türünde alanlar `Edm.String` veya `Collection(Edm.String)` olan `searchable` varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="86e86-204">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span></span> <span data-ttu-id="86e86-205">Diğer türleri alanlarının olamaz `searchable`.</span><span class="sxs-lookup"><span data-stu-id="86e86-205">Fields of other types cannot be `searchable`.</span></span>

* <span data-ttu-id="86e86-206">**Not**: `searchable` alanları Azure arama için tam metin araması hello alan değeri ek parçalanmış sürümünü depolayacak beri dizininizdeki ek boşluk kullanma.</span><span class="sxs-lookup"><span data-stu-id="86e86-206">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of hello field value for full-text searches.</span></span> <span data-ttu-id="86e86-207">Toosave alanı istiyorsanız dizininizi ve aramaların içinde yer alan toobe gerekmez, Ayarla `searchable` çok`false`.</span><span class="sxs-lookup"><span data-stu-id="86e86-207">If you want toosave space in your index and you don't need a field toobe included in searches, set `searchable` too`false`.</span></span>

<span data-ttu-id="86e86-208">`filterable`-Başvurulan hello alan toobe sağlayan `$filter` sorgular.</span><span class="sxs-lookup"><span data-stu-id="86e86-208">`filterable` - Allows hello field toobe referenced in `$filter` queries.</span></span> <span data-ttu-id="86e86-209">`filterable`farklı `searchable` dizeleri işlenme içinde.</span><span class="sxs-lookup"><span data-stu-id="86e86-209">`filterable` differs from `searchable` in how strings are handled.</span></span> <span data-ttu-id="86e86-210">Türünde alanlar `Edm.String` veya `Collection(Edm.String)` olan `filterable` yalnızca tam eşleşme için karşılaştırmaları; bu nedenle Sözcük bölünmesi, uygulanabilecek değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-210">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span></span> <span data-ttu-id="86e86-211">Örneğin, böyle bir alan ayarlarsanız `f` çok "güneşli gün", `$filter=f eq 'sunny'` herhangi bir eşleşme bulur ancak `$filter=f eq 'sunny day'` olur.</span><span class="sxs-lookup"><span data-stu-id="86e86-211">For example, if you set such a field `f` too"sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span></span> <span data-ttu-id="86e86-212">Tüm alanlar `filterable` varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="86e86-212">All fields are `filterable` by default.</span></span>

<span data-ttu-id="86e86-213">`sortable`-Varsayılan olarak hello sistem sonuçları puana göre sıralar, ancak birçok deneyimlerinde toosort hello belgelerde alanlara göre kullanıcılar isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="86e86-213">`sortable` - By default hello system sorts results by score, but in many experiences users will want toosort by fields in hello documents.</span></span> <span data-ttu-id="86e86-214">Türünde alanlar `Collection(Edm.String)` olamaz `sortable`.</span><span class="sxs-lookup"><span data-stu-id="86e86-214">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span></span> <span data-ttu-id="86e86-215">Diğer tüm alanlar `sortable` varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="86e86-215">All other fields are `sortable` by default.</span></span>

<span data-ttu-id="86e86-216">`facetable`-Genellikle kategorisini (örneğin, dijital kamera ve bakın isabet marka tarafından megapiksel tarafından fiyat, vb. göre arayın.) tarafından isabet sayısı içeren sunu arama sonuçlarının kullanılır.</span><span class="sxs-lookup"><span data-stu-id="86e86-216">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span></span> <span data-ttu-id="86e86-217">Bu seçenek türü alanlarla kullanılamaz `Edm.GeographyPoint`.</span><span class="sxs-lookup"><span data-stu-id="86e86-217">This option cannot be used with fields of type `Edm.GeographyPoint`.</span></span> <span data-ttu-id="86e86-218">Diğer tüm alanlar `facetable` varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="86e86-218">All other fields are `facetable` by default.</span></span>

* <span data-ttu-id="86e86-219">**Not**: türünde alanlar `Edm.String` olan `filterable`, `sortable`, veya `facetable` 32 KB cinsinden uzunluğu en fazla olabilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-219">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span></span> <span data-ttu-id="86e86-220">Bu tür alanları tek arama terimi olarak kabul edilir ve Azure Search'te bir terim hello en fazla 32 KB olduğundan budur.</span><span class="sxs-lookup"><span data-stu-id="86e86-220">This is because such fields are treated as a single search term, and hello maximum length of a term in Azure Search is 32KB.</span></span> <span data-ttu-id="86e86-221">Bu tek bir dize alanda daha fazla metni toostore gerekiyorsa, tooexplicitly gerekir ayarlamak `filterable`, `sortable`, ve `facetable` çok`false` , dizin tanımında.</span><span class="sxs-lookup"><span data-stu-id="86e86-221">If you need toostore more text than this in a single string field, you will need tooexplicitly set `filterable`, `sortable`, and `facetable` too`false` in your index definition.</span></span>
* <span data-ttu-id="86e86-222">**Not**: alan hello yukarıdaki hiçbiri sahipse özniteliklerini çok Ayarla`true` (`searchable`, `filterable`, `sortable`, veya`facetable`) hello alan ters hello dizinden etkili bir şekilde dışlandı.</span><span class="sxs-lookup"><span data-stu-id="86e86-222">**Note**: If a field has none of hello above attributes set too`true` (`searchable`, `filterable`, `sortable`,  or`facetable`) hello field is effectively excluded from hello inverted index.</span></span> <span data-ttu-id="86e86-223">Bu seçenek, sorgularda kullanılmaz, ancak arama sonuçlarında gerekli alanlar için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-223">This option is useful for fields that are not used in queries, but are needed in search results.</span></span> <span data-ttu-id="86e86-224">Bu tür alanları hello dizinden hariç performansı artırır.</span><span class="sxs-lookup"><span data-stu-id="86e86-224">Excluding such fields from hello index improves performance.</span></span>

<span data-ttu-id="86e86-225">`key`-İşaretleri hello dizini içinde belgeleri için benzersiz tanımlayıcı içeren olarak alan hello.</span><span class="sxs-lookup"><span data-stu-id="86e86-225">`key` - Marks hello field as containing unique identifiers for documents within hello index.</span></span> <span data-ttu-id="86e86-226">Hello yalnızca bir alanın seçilen `key` alanı ve türü olması gerektiği `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="86e86-226">Exactly one field must be chosen as hello `key` field and it must be of type `Edm.String`.</span></span> <span data-ttu-id="86e86-227">Anahtar alanları için kullanılan toolook belgeleri doğrudan hello aracılığıyla yukarı olabilir [arama API](#LookupAPI).</span><span class="sxs-lookup"><span data-stu-id="86e86-227">Key fields can be used toolook up documents directly via hello [Lookup API](#LookupAPI).</span></span>

<span data-ttu-id="86e86-228">`retrievable`-Hello alan bir arama sonucunda döndürülebilecek olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="86e86-228">`retrievable` - Sets whether hello field can be returned in a search result.</span></span>  <span data-ttu-id="86e86-229">Sıralama veya mekanizması Puanlama toouse alan (örneğin, kenar boşluğu) bir filtre olarak istiyor ancak hello alan toobe görünür toohello son kullanıcı istemiyorsanız bu yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-229">This is useful when you want toouse a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want hello field toobe visible toohello end user.</span></span> <span data-ttu-id="86e86-230">Bu öznitelik olmalıdır `true` için `key` alanları.</span><span class="sxs-lookup"><span data-stu-id="86e86-230">This attribute must be `true` for `key` fields.</span></span>

<span data-ttu-id="86e86-231">`analyzer`-Ayarlar hello Çözümleyicisi toouse adını hello alan için arama süresini ve dizin oluşturma zamanında hello.</span><span class="sxs-lookup"><span data-stu-id="86e86-231">`analyzer` - Sets hello name of hello analyzer toouse for hello field at search time and indexing time.</span></span> <span data-ttu-id="86e86-232">Değer kümesi izin Merhaba bkz [çözümleyiciler](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="86e86-232">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="86e86-233">Bu seçenek yalnızca kullanılabilir `searchable` alanları ve ayarlanamaz birlikte ya da `searchAnalyzer` veya `indexAnalyzer`.</span><span class="sxs-lookup"><span data-stu-id="86e86-233">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span></span>  <span data-ttu-id="86e86-234">Merhaba Çözümleyicisi seçilen sonra hello alanı değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="86e86-234">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="86e86-235">`searchAnalyzer`-Ayarlar hello Çözümleyicisi hello alan için arama zamanında kullanılan adını hello.</span><span class="sxs-lookup"><span data-stu-id="86e86-235">`searchAnalyzer` - Sets hello name of hello analyzer used at search time for hello field.</span></span> <span data-ttu-id="86e86-236">Değer kümesi izin Merhaba bkz [çözümleyiciler](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="86e86-236">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="86e86-237">Bu seçenek yalnızca kullanılabilir `searchable` alanları.</span><span class="sxs-lookup"><span data-stu-id="86e86-237">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="86e86-238">İle birlikte ayarlanmalıdır `indexAnalyzer` ve hello birlikte ayarlanamaz `analyzer` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="86e86-238">It must be set together with `indexAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="86e86-239">Bu çözümleyici varolan alan güncelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-239">This analyzer can be updated on an existing field.</span></span>

<span data-ttu-id="86e86-240">`indexAnalyzer`-Ayarlar hello Çözümleyicisi hello alan için dizin oluşturma zamanında kullanılan adını hello.</span><span class="sxs-lookup"><span data-stu-id="86e86-240">`indexAnalyzer` - Sets hello name of hello analyzer used at indexing time for hello field.</span></span> <span data-ttu-id="86e86-241">Değer kümesi izin Merhaba bkz [çözümleyiciler](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="86e86-241">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="86e86-242">Bu seçenek yalnızca kullanılabilir `searchable` alanları.</span><span class="sxs-lookup"><span data-stu-id="86e86-242">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="86e86-243">İle birlikte ayarlanmalıdır `searchAnalyzer` ve hello birlikte ayarlanamaz `analyzer` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="86e86-243">It must be set together with `searchAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="86e86-244">Merhaba Çözümleyicisi seçilen sonra hello alanı değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="86e86-244">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="86e86-245">`suggesters`-Ayarlar arama modu ve öneriler için Merhaba içeriğine hello kaynak alanlar hello.</span><span class="sxs-lookup"><span data-stu-id="86e86-245">`suggesters` - Sets hello search mode and fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="86e86-246">Bkz: [ilgili](#Suggesters) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="86e86-246">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="86e86-247">`scoringProfiles`-Hangi öğelerin arama sonuçlarında daha yüksek görünür etkilemek sağlayan özel Puanlama davranışları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="86e86-247">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span></span> <span data-ttu-id="86e86-248">Puanlama profili, alan ağırlığı ve işlevleri yapılır.</span><span class="sxs-lookup"><span data-stu-id="86e86-248">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="86e86-249">Bkz: [eklemek profilleri Puanlama](https://msdn.microsoft.com/library/azure/dn798928.aspx) Puanlama profilinde kullanılan hello öznitelikleri hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="86e86-249">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about hello attributes used in a scoring profile.</span></span>

<span data-ttu-id="86e86-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Dil desteği**</span><span class="sxs-lookup"><span data-stu-id="86e86-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span></span>

<span data-ttu-id="86e86-251">Aranabilir alanlara analiz uygulanabilecek en sık Sözcük bölünmesi, metin normalleştirme ve koşulları filtreleme ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-251">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span></span> <span data-ttu-id="86e86-252">Varsayılan olarak, Azure Search aranabilir alanlara hello analiz edilen [Apache Lucene standart Çözümleyicisi](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) aşağıdaki elemanlara metni keser["Unicode metin kesimleme"](http://unicode.org/reports/tr29/) kuralları.</span><span class="sxs-lookup"><span data-stu-id="86e86-252">By default, searchable fields in Azure Search are analyzed with hello [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span></span> <span data-ttu-id="86e86-253">Ayrıca, tüm karakterleri tootheir küçük form hello standart Çözümleyicisi dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="86e86-253">Additionally, hello standard analyzer converts all characters tootheir lower case form.</span></span> <span data-ttu-id="86e86-254">Dizinlenmiş belgeleri ve arama terimlerini hello analiz dizin oluşturma ve sorgu işleme sırasında gidin.</span><span class="sxs-lookup"><span data-stu-id="86e86-254">Both indexed documents and search terms go through hello analysis during indexing and query processing.</span></span>

<span data-ttu-id="86e86-255">Azure arama, çeşitli dillerde destekler.</span><span class="sxs-lookup"><span data-stu-id="86e86-255">Azure Search supports a variety of languages.</span></span> <span data-ttu-id="86e86-256">Her dil için belirli bir dil özellikleri hesapları bir standart metin Çözümleyicisi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="86e86-256">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span></span> <span data-ttu-id="86e86-257">Azure arama çözümleyiciler iki tür sunar:</span><span class="sxs-lookup"><span data-stu-id="86e86-257">Azure Search offers two types of analyzers:</span></span>

* <span data-ttu-id="86e86-258">35 çözümleyiciler Lucene tarafından yedeklenir.</span><span class="sxs-lookup"><span data-stu-id="86e86-258">35 analyzers backed by Lucene.</span></span>
* <span data-ttu-id="86e86-259">Office ve Bing kullanılan teknoloji işleme özel Microsoft doğal dil desteğiyle 50 Çözümleyicileri.</span><span class="sxs-lookup"><span data-stu-id="86e86-259">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span></span>

<span data-ttu-id="86e86-260">Bazı geliştiriciler tercih edebilirsiniz hello Lucene daha tanıdık, basit, açık kaynaklı çözüm.</span><span class="sxs-lookup"><span data-stu-id="86e86-260">Some developers might prefer hello more familiar, simple, open-source solution of Lucene.</span></span> <span data-ttu-id="86e86-261">Lucene çözümleyiciler hızlıdır, ancak hello Microsoft çözümleyiciler Gelişmiş lemmatization gibi özellikleri vardır, word (dillerde Almanca, Danca, Felemenkçe, İsveççe, Norveççe, Estonca, bitiş, Macarca, Slovakça gibi) decompounding ve varlık tanıma (URL'leri e-postalar, tarihler, sayılar).</span><span class="sxs-lookup"><span data-stu-id="86e86-261">Lucene analyzers are faster, but hello Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span></span> <span data-ttu-id="86e86-262">Mümkünse, hangisinin daha iyi bir uyum olan iki hello Microsoft ve Lucene çözümleyiciler toodecide karşılaştırmaları çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-262">If possible, you should run comparisons of both hello Microsoft and Lucene analyzers toodecide which one is a better fit.</span></span>

<span data-ttu-id="86e86-263">***Nasıl Karşılaştır***</span><span class="sxs-lookup"><span data-stu-id="86e86-263">***How they compare***</span></span>

<span data-ttu-id="86e86-264">İngilizce için Hello Lucene Çözümleyicisi hello standart Çözümleyicisi genişletir.</span><span class="sxs-lookup"><span data-stu-id="86e86-264">hello Lucene analyzer for English extends hello standard analyzer.</span></span> <span data-ttu-id="86e86-265">('S sondaki) iyelik sözcükleri kaldırır, göre kaynaklanan geçerlidir [bağlantısı kaynaklanan algoritması](http://tartarus.org/~martin/PorterStemmer/)ve İngilizce kaldırır [durdurma sözcükleri](http://en.wikipedia.org/wiki/Stop_words).</span><span class="sxs-lookup"><span data-stu-id="86e86-265">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span></span>

<span data-ttu-id="86e86-266">Buna karşılık, hello Microsoft Çözümleyicisi kaynaklanan yerine lemmatization gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="86e86-266">In comparison, hello Microsoft analyzer performs lemmatization instead of stemming.</span></span> <span data-ttu-id="86e86-267">Bunu işleyebilir bükümlü ve düzensiz sözcük formlarını daha iyi ne daha ilgili arama sonuçlarında sonuçları anlamına gelir (izleme modülünü 7 [Azure arama MVA sunu](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) daha fazla ayrıntı için).</span><span class="sxs-lookup"><span data-stu-id="86e86-267">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span></span>

<span data-ttu-id="86e86-268">İle Microsoft çözümleyiciler dizin ortalama iki toothree Lucene eşdeğerlerine hello dil bağlı olarak daha yavaş katıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-268">Indexing with Microsoft analyzers is on average two toothree times slower than their Lucene equivalents, depending on hello language.</span></span> <span data-ttu-id="86e86-269">Arama performansını önemli ölçüde ortalama boyutu sorgularında etkilenmemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-269">Search performance should not be significantly affected for average size queries.</span></span>

<span data-ttu-id="86e86-270">***Yapılandırma***</span><span class="sxs-lookup"><span data-stu-id="86e86-270">***Configuration***</span></span>

<span data-ttu-id="86e86-271">Merhaba dizin tanımı'ndaki her bir alan için hello ayarlayabilirsiniz `analyzer` hangi dil ve satıcı belirtir özellik tooan Çözümleyicisi adı.</span><span class="sxs-lookup"><span data-stu-id="86e86-271">For each field in hello index definition, you can set hello `analyzer` property tooan analyzer name that specifies which language and vendor.</span></span> <span data-ttu-id="86e86-272">Merhaba aynı Çözümleyicisi dizin oluşturma ve bu alan için arama uygulanır.</span><span class="sxs-lookup"><span data-stu-id="86e86-272">hello same analyzer will be applied when indexing and searching for that field.</span></span>
<span data-ttu-id="86e86-273">Örneğin, yana birimi hello içinde mevcut İngilizce, Fransızca ve İspanyolca otel açıklamaları için ayrı alanları olabilir aynı dizin.</span><span class="sxs-lookup"><span data-stu-id="86e86-273">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in hello same index.</span></span> <span data-ttu-id="86e86-274">Kullanım hello ['searchFields' sorgu parametresi](#SearchQueryParameters) toospecify hangi dile özgü alan toosearch karşı sorgularınızı.</span><span class="sxs-lookup"><span data-stu-id="86e86-274">Use hello ['searchFields' query parameter](#SearchQueryParameters) toospecify which language-specific field toosearch against in your queries.</span></span> <span data-ttu-id="86e86-275">Merhaba dahil sorgu örnekler gözden geçirebilirsiniz `analyzer` özelliğinde [Search belgeleri](#SearchDocs).</span><span class="sxs-lookup"><span data-stu-id="86e86-275">You can review query examples that include hello `analyzer` property in [Search Documents](#SearchDocs).</span></span> 

<span data-ttu-id="86e86-276">***Çözümleyici listesi***</span><span class="sxs-lookup"><span data-stu-id="86e86-276">***Analyzer list***</span></span>

<span data-ttu-id="86e86-277">Merhaba Lucene ve Microsoft Çözümleyicisi adları ile birlikte desteklenen dillerin listesi aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="86e86-277">Below is hello list of supported languages together with Lucene and Microsoft analyzer names.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="86e86-278">Dil</span><span class="sxs-lookup"><span data-stu-id="86e86-278">Language</span></span></th>
        <th><span data-ttu-id="86e86-279">Microsoft Çözümleyicisi adı</span><span class="sxs-lookup"><span data-stu-id="86e86-279">Microsoft analyzer name</span></span></th>
        <th><span data-ttu-id="86e86-280">Lucene Çözümleyicisi adı</span><span class="sxs-lookup"><span data-stu-id="86e86-280">Lucene analyzer name</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-281">Arapça</span><span class="sxs-lookup"><span data-stu-id="86e86-281">Arabic</span></span></td>
        <td><span data-ttu-id="86e86-282">ar.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-282">ar.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-283">ar.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-283">ar.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-284">Ermenice</span><span class="sxs-lookup"><span data-stu-id="86e86-284">Armenian</span></span></td>
        <td></td>
        <td><span data-ttu-id="86e86-285">hy.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-285">hy.lucene</span></span></td>
      </tr>
    <tr>
        <td><span data-ttu-id="86e86-286">Bangla</span><span class="sxs-lookup"><span data-stu-id="86e86-286">Bangla</span></span></td>
        <td><span data-ttu-id="86e86-287">Bn.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-287">bn.microsoft</span></span></td>
        <td></td>
    </tr>
      <tr>
        <td><span data-ttu-id="86e86-288">Bask dili</span><span class="sxs-lookup"><span data-stu-id="86e86-288">Basque</span></span></td>
        <td></td>
        <td><span data-ttu-id="86e86-289">EU.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-289">eu.lucene</span></span></td>
    </tr>
      <tr>
         <td><span data-ttu-id="86e86-290">Bulgarca</span><span class="sxs-lookup"><span data-stu-id="86e86-290">Bulgarian</span></span></td>
        <td><span data-ttu-id="86e86-291">BG.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-291">bg.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-292">BG.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-292">bg.lucene</span></span></td>
      </tr>
      <tr>
        <td><span data-ttu-id="86e86-293">Katalanca</span><span class="sxs-lookup"><span data-stu-id="86e86-293">Catalan</span></span></td>
        <td><span data-ttu-id="86e86-294">CA.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-294">ca.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-295">CA.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-295">ca.lucene</span></span></td>          
      </tr>
    <tr>
        <td><span data-ttu-id="86e86-296">Basitleştirilmiş Çince</span><span class="sxs-lookup"><span data-stu-id="86e86-296">Chinese Simplified</span></span></td>
        <td><span data-ttu-id="86e86-297">zh-Hans.microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-297">zh-Hans.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-298">zh-Hans.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-298">zh-Hans.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-299">Geleneksel Çince</span><span class="sxs-lookup"><span data-stu-id="86e86-299">Chinese Traditional</span></span></td>
        <td><span data-ttu-id="86e86-300">zh-Hant.microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-300">zh-Hant.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-301">zh-Hant.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-301">zh-Hant.lucene</span></span></td>        
    <tr>
    <tr>
        <td><span data-ttu-id="86e86-302">Hırvatça</span><span class="sxs-lookup"><span data-stu-id="86e86-302">Croatian</span></span></td>
        <td><span data-ttu-id="86e86-303">hr.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-303">hr.microsoft</span></span></td>
        <td/></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-304">Çekçe</span><span class="sxs-lookup"><span data-stu-id="86e86-304">Czech</span></span></td>
        <td><span data-ttu-id="86e86-305">cs.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-305">cs.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-306">cs.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-306">cs.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="86e86-307">Danca</span><span class="sxs-lookup"><span data-stu-id="86e86-307">Danish</span></span></td>
        <td><span data-ttu-id="86e86-308">da.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-308">da.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-309">da.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-309">da.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="86e86-310">Hollanda dili</span><span class="sxs-lookup"><span data-stu-id="86e86-310">Dutch</span></span></td>
        <td><span data-ttu-id="86e86-311">NL.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-311">nl.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-312">NL.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-312">nl.lucene</span></span></td>    
    </tr>    
    <tr>
        <td><span data-ttu-id="86e86-313">Türkçe</span><span class="sxs-lookup"><span data-stu-id="86e86-313">English</span></span></td>        
        <td><span data-ttu-id="86e86-314">en.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-314">en.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-315">en.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-315">en.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-316">Estonca</span><span class="sxs-lookup"><span data-stu-id="86e86-316">Estonian</span></span></td>
        <td><span data-ttu-id="86e86-317">et.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-317">et.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-318">Fince</span><span class="sxs-lookup"><span data-stu-id="86e86-318">Finnish</span></span></td>
        <td><span data-ttu-id="86e86-319">Fi.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-319">fi.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-320">Fi.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-320">fi.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="86e86-321">Fransızca</span><span class="sxs-lookup"><span data-stu-id="86e86-321">French</span></span></td>
        <td><span data-ttu-id="86e86-322">fr.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-322">fr.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-323">fr.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-323">fr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-324">Galiçya lehçesi</span><span class="sxs-lookup"><span data-stu-id="86e86-324">Galician</span></span></td>
        <td></td>
        <td><span data-ttu-id="86e86-325">GL.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-325">gl.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="86e86-326">Almanca</span><span class="sxs-lookup"><span data-stu-id="86e86-326">German</span></span></td>
        <td><span data-ttu-id="86e86-327">de.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-327">de.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-328">de.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-328">de.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-329">Yunanca</span><span class="sxs-lookup"><span data-stu-id="86e86-329">Greek</span></span></td>
        <td><span data-ttu-id="86e86-330">el.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-330">el.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-331">el.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-331">el.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-332">Gucerat dili</span><span class="sxs-lookup"><span data-stu-id="86e86-332">Gujarati</span></span></td>
        <td><span data-ttu-id="86e86-333">gu.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-333">gu.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-334">İbranice</span><span class="sxs-lookup"><span data-stu-id="86e86-334">Hebrew</span></span></td>
        <td><span data-ttu-id="86e86-335">He.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-335">he.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-336">Hintçe</span><span class="sxs-lookup"><span data-stu-id="86e86-336">Hindi</span></span></td>
        <td><span data-ttu-id="86e86-337">Hi.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-337">hi.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-338">Hi.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-338">hi.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-339">Macarca</span><span class="sxs-lookup"><span data-stu-id="86e86-339">Hungarian</span></span></td>        
        <td><span data-ttu-id="86e86-340">hu.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-340">hu.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-341">hu.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-341">hu.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-342">İzlanda dili</span><span class="sxs-lookup"><span data-stu-id="86e86-342">Icelandic</span></span></td>
        <td><span data-ttu-id="86e86-343">is.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-343">is.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-344">Endonezya dili (Bahasa)</span><span class="sxs-lookup"><span data-stu-id="86e86-344">Indonesian (Bahasa)</span></span></td>
        <td><span data-ttu-id="86e86-345">id.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-345">id.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-346">id.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-346">id.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-347">İrlanda dili</span><span class="sxs-lookup"><span data-stu-id="86e86-347">Irish</span></span></td>
        <td></td>
          <td><span data-ttu-id="86e86-348">GA.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-348">ga.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-349">İtalyanca</span><span class="sxs-lookup"><span data-stu-id="86e86-349">Italian</span></span></td>
        <td><span data-ttu-id="86e86-350">it.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-350">it.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-351">it.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-351">it.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-352">Japonca</span><span class="sxs-lookup"><span data-stu-id="86e86-352">Japanese</span></span></td>
        <td><span data-ttu-id="86e86-353">ja.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-353">ja.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-354">ja.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-354">ja.lucene</span></span></td>

    </tr>
    <tr>
        <td><span data-ttu-id="86e86-355">Kannada dili</span><span class="sxs-lookup"><span data-stu-id="86e86-355">Kannada</span></span></td>
        <td><span data-ttu-id="86e86-356">Ka.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-356">ka.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-357">Kore dili</span><span class="sxs-lookup"><span data-stu-id="86e86-357">Korean</span></span></td>
        <td><span data-ttu-id="86e86-358">Ko.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-358">ko.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-359">Ko.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-359">ko.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-360">Letonca</span><span class="sxs-lookup"><span data-stu-id="86e86-360">Latvian</span></span></td>        
        <td><span data-ttu-id="86e86-361">LV.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-361">lv.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-362">LV.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-362">lv.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-363">Litvanca</span><span class="sxs-lookup"><span data-stu-id="86e86-363">Lithuanian</span></span></td>
        <td><span data-ttu-id="86e86-364">lt.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-364">lt.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-365">Malayalam dili</span><span class="sxs-lookup"><span data-stu-id="86e86-365">Malayalam</span></span></td>
        <td><span data-ttu-id="86e86-366">ML.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-366">ml.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-367">Malay (Latin)</span><span class="sxs-lookup"><span data-stu-id="86e86-367">Malay (Latin)</span></span></td>
        <td><span data-ttu-id="86e86-368">MS.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-368">ms.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-369">Marathi</span><span class="sxs-lookup"><span data-stu-id="86e86-369">Marathi</span></span></td>
        <td><span data-ttu-id="86e86-370">Mr.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-370">mr.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-371">Norveççe</span><span class="sxs-lookup"><span data-stu-id="86e86-371">Norwegian</span></span></td>
        <td><span data-ttu-id="86e86-372">NB.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-372">nb.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-373">No.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-373">no.lucene</span></span></td>        
    </tr>
      <tr>
        <td><span data-ttu-id="86e86-374">Farsça</span><span class="sxs-lookup"><span data-stu-id="86e86-374">Persian</span></span></td>
        <td></td>
        <td><span data-ttu-id="86e86-375">FA.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-375">fa.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="86e86-376">Lehçe</span><span class="sxs-lookup"><span data-stu-id="86e86-376">Polish</span></span></td>
        <td><span data-ttu-id="86e86-377">PL.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-377">pl.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-378">PL.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-378">pl.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-379">Portekizce (Brezilya)</span><span class="sxs-lookup"><span data-stu-id="86e86-379">Portuguese (Brazil)</span></span></td>
        <td><span data-ttu-id="86e86-380">PT Br.microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-380">pt-Br.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-381">PT Br.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-381">pt-Br.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-382">Portekizce (Portekiz)</span><span class="sxs-lookup"><span data-stu-id="86e86-382">Portuguese (Portugal)</span></span></td>
        <td><span data-ttu-id="86e86-383">PT Pt.microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-383">pt-Pt.microsoft</span></span></td>        
        <td><span data-ttu-id="86e86-384">PT Pt.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-384">pt-Pt.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-385">Pencap dili</span><span class="sxs-lookup"><span data-stu-id="86e86-385">Punjabi</span></span></td>
        <td><span data-ttu-id="86e86-386">Pa.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-386">pa.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-387">Rumence</span><span class="sxs-lookup"><span data-stu-id="86e86-387">Romanian</span></span></td>
        <td><span data-ttu-id="86e86-388">Ro.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-388">ro.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-389">Ro.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-389">ro.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-390">Rusça</span><span class="sxs-lookup"><span data-stu-id="86e86-390">Russian</span></span></td>
        <td><span data-ttu-id="86e86-391">RU.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-391">ru.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-392">RU.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-392">ru.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-393">Sırpça (Kiril)</span><span class="sxs-lookup"><span data-stu-id="86e86-393">Serbian (Cyrillic)</span></span></td>
        <td><span data-ttu-id="86e86-394">SR-cyrillic.microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-394">sr-cyrillic.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-395">Sırpça (Latin)</span><span class="sxs-lookup"><span data-stu-id="86e86-395">Serbian (Latin)</span></span></td>
        <td><span data-ttu-id="86e86-396">SR-latin.microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-396">sr-latin.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-397">Slovakça</span><span class="sxs-lookup"><span data-stu-id="86e86-397">Slovak</span></span></td>
        <td><span data-ttu-id="86e86-398">SK.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-398">sk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-399">Slovence</span><span class="sxs-lookup"><span data-stu-id="86e86-399">Slovenian</span></span></td>
        <td><span data-ttu-id="86e86-400">SL.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-400">sl.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-401">İspanyolca</span><span class="sxs-lookup"><span data-stu-id="86e86-401">Spanish</span></span></td>
        <td><span data-ttu-id="86e86-402">Es.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-402">es.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-403">Es.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-403">es.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-404">İsveç dili</span><span class="sxs-lookup"><span data-stu-id="86e86-404">Swedish</span></span></td>
        <td><span data-ttu-id="86e86-405">sv.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-405">sv.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-406">sv.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-406">sv.lucene</span></span></td>
    </tr>

    <tr>
        <td><span data-ttu-id="86e86-407">Tamil dili</span><span class="sxs-lookup"><span data-stu-id="86e86-407">Tamil</span></span></td>
        <td><span data-ttu-id="86e86-408">ta.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-408">ta.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-409">Telugu dili</span><span class="sxs-lookup"><span data-stu-id="86e86-409">Telugu</span></span></td>
        <td><span data-ttu-id="86e86-410">te.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-410">te.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-411">Tay dili</span><span class="sxs-lookup"><span data-stu-id="86e86-411">Thai</span></span></td>
        <td><span data-ttu-id="86e86-412">TH.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-412">th.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-413">TH.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-413">th.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-414">Türkçe</span><span class="sxs-lookup"><span data-stu-id="86e86-414">Turkish</span></span></td>
        <td><span data-ttu-id="86e86-415">tr.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-415">tr.microsoft</span></span></td>
        <td><span data-ttu-id="86e86-416">tr.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-416">tr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-417">Ukrayna dili</span><span class="sxs-lookup"><span data-stu-id="86e86-417">Ukrainian</span></span></td>
        <td><span data-ttu-id="86e86-418">UK.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-418">uk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-419">Urduca</span><span class="sxs-lookup"><span data-stu-id="86e86-419">Urdu</span></span></td>
        <td><span data-ttu-id="86e86-420">Your.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-420">ur.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-421">Vietnam dili</span><span class="sxs-lookup"><span data-stu-id="86e86-421">Vietnamese</span></span></td>
        <td><span data-ttu-id="86e86-422">vi.Microsoft</span><span class="sxs-lookup"><span data-stu-id="86e86-422">vi.microsoft</span></span></td>
        <td></td>
    </tr>
    <td colspan="3"><span data-ttu-id="86e86-423">Ayrıca Azure Search dilden bağımsız çözümleyicisi yapılandırmalarını sağlar</span><span class="sxs-lookup"><span data-stu-id="86e86-423">Additionally Azure Search provides language-agnostic analyzer configurations</span></span></td>
    <tr>
        <td><span data-ttu-id="86e86-424">Standart ASCII Katlama</span><span class="sxs-lookup"><span data-stu-id="86e86-424">Standard ASCII Folding</span></span></td>
        <td><span data-ttu-id="86e86-425">standardasciifolding.lucene</span><span class="sxs-lookup"><span data-stu-id="86e86-425">standardasciifolding.lucene</span></span></td>
        <td>
        <ul>
            <li><span data-ttu-id="86e86-426">Unicode metin kesimleme (standart belirteç Oluşturucu)</span><span class="sxs-lookup"><span data-stu-id="86e86-426">Unicode text segmentation (Standard Tokenizer)</span></span></li>
            <li><span data-ttu-id="86e86-427">ASCII kırılma filtresi - toohello ilk 127 ASCII karakter kümesi ASCII eşdeğerlerine ait olmayan Unicode karakterler dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="86e86-427">ASCII folding filter - converts Unicode characters that don't belong toohello set of first 127 ASCII characters into their ASCII equivalents.</span></span> <span data-ttu-id="86e86-428">Bu, Aksan kaldırmak için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-428">This is useful for removing diacritics.</span></span></li>
        </ul>
        </td>
    </tr>
</table>

<span data-ttu-id="86e86-429">İle ek açıklama adları olan tüm çözümleyiciler <i>lucene</i> tarafından sağlanmıştır [Apache Lucene'nın dil Çözümleyicileri](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span><span class="sxs-lookup"><span data-stu-id="86e86-429">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span></span> <span data-ttu-id="86e86-430">Filtre Katlama hello ASCII hakkında daha fazla bilgi bulunabilir [burada](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span><span class="sxs-lookup"><span data-stu-id="86e86-430">More information about hello ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span></span>

<span data-ttu-id="86e86-431">**Öneri araçları**</span><span class="sxs-lookup"><span data-stu-id="86e86-431">**Suggesters**</span></span>

<span data-ttu-id="86e86-432">A `suggester` bir dizindeki hangi alanların kullanılan toosupport aramalarda otomatik tamamlama olduğunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="86e86-432">A `suggester` defines which fields in an index are used toosupport auto-complete in searches.</span></span> <span data-ttu-id="86e86-433">Kısmi arama dizelerini toohello genellikle gönderilen [önerileri API](#Suggestions) hello kullanıcı bir arama sorgusu yazarak ve hello API önerilen tümcecikleri bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="86e86-433">Typically partial search strings are sent toohello [Suggestions API](#Suggestions) while hello user is typing a search query, and hello API returns a set of suggested phrases.</span></span> <span data-ttu-id="86e86-434">Merhaba dizinde tanımladığınız bir öneri aracı hangi alanların kullanılan toobuild hello yazarken tamamlanan arama terimleri olduğunu belirler.</span><span class="sxs-lookup"><span data-stu-id="86e86-434">A suggester that you define in hello index determines which fields are used toobuild hello type-ahead search terms.</span></span> <span data-ttu-id="86e86-435">Bkz: [ilgili](#Suggesters) yapılandırma ayrıntıları için.</span><span class="sxs-lookup"><span data-stu-id="86e86-435">See [Suggesters](#Suggesters) for configuration details.</span></span>

<span data-ttu-id="86e86-436">**Puanlama modelleri**</span><span class="sxs-lookup"><span data-stu-id="86e86-436">**Scoring profiles**</span></span>

<span data-ttu-id="86e86-437">A `scoringProfile` hangi öğelerin görünür hello arama sonuçlarında daha yüksek etkilemek sağlayan özel Puanlama davranışları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="86e86-437">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in hello search results.</span></span> <span data-ttu-id="86e86-438">Puanlama profili, alan ağırlığı ve işlevleri yapılır.</span><span class="sxs-lookup"><span data-stu-id="86e86-438">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="86e86-439">toouse bunları, hello sorgu dizesi adına göre bir profili belirttiğiniz.</span><span class="sxs-lookup"><span data-stu-id="86e86-439">toouse them, you specify a profile by name on hello query string.</span></span>

<span data-ttu-id="86e86-440">Puanlama profili varsayılan sonuç kümesinde her öğe için bir arama puanı hello planda toocompute çalışır.</span><span class="sxs-lookup"><span data-stu-id="86e86-440">A default scoring profile operates behind hello scenes toocompute a search score for every item in a result set.</span></span> <span data-ttu-id="86e86-441">Merhaba iç, adlandırılmamış Puanlama profili kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86e86-441">You can use hello internal, unnamed scoring profile.</span></span> <span data-ttu-id="86e86-442">Alternatif olarak, kümesinin `defaultScoringProfile` toouse özel bir profil hello varsayılan olarak özel bir profil hello sorgu dizesinde belirtilmediğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="86e86-442">Alternatively, set `defaultScoringProfile` toouse a custom profile as hello default, invoked whenever a custom profile is not specified on hello query string.</span></span>

<span data-ttu-id="86e86-443">Bkz: [Ekle Puanlama profilleri tooa arama dizini (Azure Search Hizmeti REST API'si)](search-api-scoring-profiles-2015-02-28-preview.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="86e86-443">See [Add scoring profiles tooa search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span></span>

<span data-ttu-id="86e86-444">**CORS seçenekleri**</span><span class="sxs-lookup"><span data-stu-id="86e86-444">**CORS Options**</span></span>

<span data-ttu-id="86e86-445">Merhaba tarayıcı tüm çıkış noktaları arası istekleri engeller istemci tarafı Javascript herhangi API'leri varsayılan olarak çağrılamaz.</span><span class="sxs-lookup"><span data-stu-id="86e86-445">Client-side Javascript cannot call any APIs by default since hello browser will prevent all cross-origin requests.</span></span> <span data-ttu-id="86e86-446">CORS (çıkış noktaları arası kaynak paylaşımı) ayarı hello tarafından etkinleştirmek `corsOptions` öznitelik tooallow çıkış noktaları arası sorguları tooyour dizini.</span><span class="sxs-lookup"><span data-stu-id="86e86-446">Enable CORS (Cross-Origin Resource Sharing) by setting hello `corsOptions` attribute tooallow cross-origin queries tooyour index.</span></span> <span data-ttu-id="86e86-447">Yalnızca bu sorguyu güvenlik nedeniyle CORS desteğini API'leri unutmayın.</span><span class="sxs-lookup"><span data-stu-id="86e86-447">Note that only query APIs support CORS for security reasons.</span></span> <span data-ttu-id="86e86-448">Seçenekler aşağıdaki hello için CORS ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="86e86-448">hello following options can be set for CORS:</span></span>

* <span data-ttu-id="86e86-449">`allowedOrigins`(gerekli): Bu bir erişim tooyour dizin verilecek çıkış noktaları listesidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-449">`allowedOrigins` (required): This is a list of origins that will be granted access tooyour index.</span></span> <span data-ttu-id="86e86-450">Bu, bu çıkış noktalarından sunulacak tüm Javascript kodlarının olacaktır anlamına gelir izin tooquery dizininizi (Merhaba doğru API anahtarını verdiği varsayılarak).</span><span class="sxs-lookup"><span data-stu-id="86e86-450">This means that any Javascript code served from those origins will be allowed tooquery your index (assuming it provides hello correct API key).</span></span> <span data-ttu-id="86e86-451">Her bir çıkış noktası genellikle hello biçimidir `protocol://fully-qualified-domain-name:port` ancak başlangıç bağlantı noktası çoğunlukla yazılmaz.</span><span class="sxs-lookup"><span data-stu-id="86e86-451">Each origin is typically of hello form `protocol://fully-qualified-domain-name:port` although hello port is often omitted.</span></span> <span data-ttu-id="86e86-452">Bkz: [bu makalede](http://go.microsoft.com/fwlink/?LinkId=330822) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="86e86-452">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span></span>
  * <span data-ttu-id="86e86-453">Tooallow erişim tooall çıkış istiyorsanız ekleyin `*` hello içinde tek bir öğe olarak `allowedOrigins` dizi.</span><span class="sxs-lookup"><span data-stu-id="86e86-453">If you want tooallow access tooall origins, include `*` as a single item in hello `allowedOrigins` array.</span></span> <span data-ttu-id="86e86-454">Unutmayın **bu yöntem üretim arama hizmetleri için önerilmez.**</span><span class="sxs-lookup"><span data-stu-id="86e86-454">Note that **this is not recommended practice for production search services.**</span></span> <span data-ttu-id="86e86-455">Ancak, geliştirme veya hata ayıklama için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-455">However, it may be useful for development or debugging purposes.</span></span>
* <span data-ttu-id="86e86-456">`maxAgeInSeconds`(isteğe bağlı): tarayıcılar bu değeri toodetermine hello süresi (saniye) toocache CORS denetim öncesi yanıtlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="86e86-456">`maxAgeInSeconds` (optional): Browsers use this value toodetermine hello duration (in seconds) toocache CORS preflight responses.</span></span> <span data-ttu-id="86e86-457">Bu, negatif olmayan bir tamsayı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-457">This must be a non-negative integer.</span></span> <span data-ttu-id="86e86-458">Merhaba büyük hello daha iyi performans bu değer olur, ancak hello uzun CORS İlkesi değişiklikleri tootake için etkili.</span><span class="sxs-lookup"><span data-stu-id="86e86-458">hello larger this value is, hello better performance will be, but hello longer it will take for CORS policy changes tootake effect.</span></span> <span data-ttu-id="86e86-459">Ayarlanmazsa, varsayılan süre olan 5 dakika kullanılır.</span><span class="sxs-lookup"><span data-stu-id="86e86-459">If it is not set, a default duration of 5 minutes will be used.</span></span>

<span data-ttu-id="86e86-460"><a name="CreateUpdateIndexExample"></a>
**İstek gövdesi örneği**</span><span class="sxs-lookup"><span data-stu-id="86e86-460"><a name="CreateUpdateIndexExample"></a>
**Request Body Example**</span></span>

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

<span data-ttu-id="86e86-461">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="86e86-461">**Response**</span></span>

<span data-ttu-id="86e86-462">Başarılı bir istek için: "201 oluşturuldu".</span><span class="sxs-lookup"><span data-stu-id="86e86-462">For a successful request: "201 Created".</span></span>

<span data-ttu-id="86e86-463">Varsayılan olarak oluşturulan hello dizin tanımı için JSON hello hello yanıt gövdesi içerir.</span><span class="sxs-lookup"><span data-stu-id="86e86-463">By default hello response body will contain hello JSON for hello index definition that was created.</span></span> <span data-ttu-id="86e86-464">Merhaba, `Prefer` istek üstbilgisi çok ayarlamak`return=minimal`hello yanıt gövdesi boş olacaktır ve hello başarı durum kodu olacaktır "204 İçerik" yerine "201 oluşturuldu".</span><span class="sxs-lookup"><span data-stu-id="86e86-464">If hello `Prefer` request header is set too`return=minimal`, hello response body will be empty and hello success status code will be "204 No Content" instead of "201 Created".</span></span> <span data-ttu-id="86e86-465">Bu, PUT veya POST kullanılan toocreate hello dizin olmasına bakılmaksızın geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-465">This is true regardless of whether PUT or POST was used toocreate hello index.</span></span>

<span data-ttu-id="86e86-466">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="86e86-466">**Remarks**</span></span>

<span data-ttu-id="86e86-467">Şu anda, sınırlı dizin şeması güncelleştirmelerini desteği yoktur.</span><span class="sxs-lookup"><span data-stu-id="86e86-467">Currently, there is limited support for index schema updates.</span></span> <span data-ttu-id="86e86-468">Alan türlerinin değiştirilmesi gibi yeniden dizinlemeyi gerektiren hiçbir şema güncelleştirmesi şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="86e86-468">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span></span> <span data-ttu-id="86e86-469">Var olan alanları silinmiş veya değiştirilemez rağmen yeni alanlar herhangi bir zamanda tooan varolan bir dizini eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-469">Although existing fields cannot be changed or deleted, new fields can be added tooan existing index at any time.</span></span> <span data-ttu-id="86e86-470">Yeni bir alan eklediğinizde hello dizindeki tüm mevcut belgeleri otomatik olarak bu alan için bir null değer sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="86e86-470">When a new field is added, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="86e86-471">Yeni belgeler toohello dizin ekleninceye kadar hiçbir ek depolama alanı tüketilebilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-471">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<a name="Suggesters"></a>

## <a name="suggesters"></a><span data-ttu-id="86e86-472">Öneri Araçları</span><span class="sxs-lookup"><span data-stu-id="86e86-472">Suggesters</span></span>
<span data-ttu-id="86e86-473">Merhaba önerileri özellik Azure Search, arama kutusuna girilen yanıt toopartial dize girdileri olası arama terimlerini listesini sağlayan yazarken tamamlanan veya otomatik tamamlama sorgusu yetenektir.</span><span class="sxs-lookup"><span data-stu-id="86e86-473">hello suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response toopartial string inputs entered into a search box.</span></span> <span data-ttu-id="86e86-474">Büyük olasılıkla Sorgu önerileri ticari web arama motorları kullanılırken fark: Bing içinde ".NET" yazarak üreten koşulları listesini ".NET 4.5", ".NET Framework 3,5", vb..</span><span class="sxs-lookup"><span data-stu-id="86e86-474">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span></span> <span data-ttu-id="86e86-475">Merhaba arama hizmeti REST API kullanırken, özel bir Azure Search uygulamada önerileri uygulama hello aşağıdakileri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="86e86-475">When using hello Search service REST API, implementing suggestions in a custom Azure Search application requires hello following:</span></span>

* <span data-ttu-id="86e86-476">Ekleyerek önerilerini etkinleştirmek bir **öneri aracı** hello adı, arama modu ve alanların listesi için yazarken tamamlanan vermiş dizininizdeki yapım çağrılır.</span><span class="sxs-lookup"><span data-stu-id="86e86-476">Enable suggestions by adding a **suggester** construction in your index, giving hello name, search mode, and a list of fields for which type-ahead is invoked.</span></span> <span data-ttu-id="86e86-477">Kısmi arama dizesi "Sea" yazarak bir kaynak alanı olarak "ŞehirAdı" "Seattle" sonuçlanır belirtirseniz, örneğin, "Sahil" ve "Seatac" (üçü gerçek Şehir adları) Sorgu önerileri toohello kullanıcı olarak sunulan.</span><span class="sxs-lookup"><span data-stu-id="86e86-477">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions toohello user.</span></span>
* <span data-ttu-id="86e86-478">Öneriler tarafından arama hello çağırma [önerileri API](#Suggestions) , uygulama kodunuzda.</span><span class="sxs-lookup"><span data-stu-id="86e86-478">Invoke suggestions by calling hello [Suggestions API](#Suggestions) in your application code.</span></span> <span data-ttu-id="86e86-479">Genellikle kısmi arama dizelerini hello kullanıcı bir arama sorgusu yazıyor ve bu API önerilen tümcecikleri kümesini döndürür toohello hizmet gönderilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-479">Typically partial search strings are sent toohello service while hello user is typing a search query, and this API returns a set of suggested phrases.</span></span>

<span data-ttu-id="86e86-480">Bu makalede açıklanır nasıl tooconfigure bir **öneri aracı**.</span><span class="sxs-lookup"><span data-stu-id="86e86-480">This article explains how tooconfigure a **suggester**.</span></span> <span data-ttu-id="86e86-481">Merhaba da gözden geçirmelisiniz [önerileri API](#Suggestions) bir öneri Aracı nasıl kullanıldığı hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="86e86-481">You should also review hello [Suggestions API](#Suggestions) for details on how a suggester is used.</span></span>

<span data-ttu-id="86e86-482">**Kullanım**</span><span class="sxs-lookup"><span data-stu-id="86e86-482">**Usage**</span></span>

<span data-ttu-id="86e86-483">`Suggesters`Merhaba dizinde oluşturulur ve kullanıldığında en iyi şekilde çalışır toosuggest özel belgeler gevşek terimleri veya tümcecikleri yerine.</span><span class="sxs-lookup"><span data-stu-id="86e86-483">`Suggesters` are created in hello index and work best when used toosuggest specific documents rather than loose terms or phrases.</span></span> <span data-ttu-id="86e86-484">Merhaba en iyi adayı başlıklar, adları ve bir öğe tanımlayabilir diğer görece kısa tümceleri alanlardır.</span><span class="sxs-lookup"><span data-stu-id="86e86-484">hello best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span></span> <span data-ttu-id="86e86-485">Kategoriler ve etiketler gibi yinelenen alanları veya çok uzun alanları açıklamaları veya açıklamalar alanları gibi daha az etkili olur.</span><span class="sxs-lookup"><span data-stu-id="86e86-485">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span></span>

<span data-ttu-id="86e86-486">Merhaba dizin tanımının bir parçası olarak, bir tek öneri aracı toohello ekleyebilirsiniz `suggesters` koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="86e86-486">As part of hello index definition, you can add a single suggester toohello `suggesters` collection.</span></span> <span data-ttu-id="86e86-487">Bir öneri aracı tanımlayan özellikleri hello şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="86e86-487">Properties that define a suggester include hello following:</span></span>

* <span data-ttu-id="86e86-488">`name`: hello hello öneri aracı adını.</span><span class="sxs-lookup"><span data-stu-id="86e86-488">`name`: hello name of hello suggester.</span></span> <span data-ttu-id="86e86-489">Merhaba çağırırken hello hello öneri aracı adını kullanmak `suggest` API.</span><span class="sxs-lookup"><span data-stu-id="86e86-489">You use hello name of hello suggester when calling hello `suggest` API.</span></span>
* <span data-ttu-id="86e86-490">`searchMode`: aday tümcecikleri için kullanılan strateji toosearch hello.</span><span class="sxs-lookup"><span data-stu-id="86e86-490">`searchMode`: hello strategy used toosearch for candidate phrases.</span></span> <span data-ttu-id="86e86-491">Merhaba şu anda desteklenen tek mod olan `analyzingInfixMatching`, hello başında veya tümcelerin hello ortasında esnek eşleştirilmesini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="86e86-491">hello only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at hello beginning or in hello middle of sentences.</span></span>
* <span data-ttu-id="86e86-492">`sourceFields`: Merhaba kaynak önerileri için Merhaba içeriğine bir veya daha fazla alanlar bir listesi.</span><span class="sxs-lookup"><span data-stu-id="86e86-492">`sourceFields`: A list of one or more fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="86e86-493">Yalnızca türünde alanlar `Edm.String` ve `Collection(Edm.String)` kaynakları önerileri için olabilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-493">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span></span> <span data-ttu-id="86e86-494">Ayarlama özel bir dil Çözümleyicisi sahip olmayan alanlar kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-494">Only fields that don't have a custom language analyzer set can be used.</span></span>

<span data-ttu-id="86e86-495">**Öneri aracı örneği**</span><span class="sxs-lookup"><span data-stu-id="86e86-495">**Suggester Example**</span></span>

<span data-ttu-id="86e86-496">Bir öneri aracı hello dizini bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-496">A suggester is part of hello index.</span></span> <span data-ttu-id="86e86-497">Yalnızca bir öneri aracı hello mevcut `suggesters` hello yanında hello geçerli sürümü koleksiyonda koleksiyon alanları ve `scoringProfiles`.</span><span class="sxs-lookup"><span data-stu-id="86e86-497">Only one suggester can exist in hello `suggesters` collection in hello current version, alongside hello fields collection and `scoringProfiles`.</span></span>

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> <span data-ttu-id="86e86-498">Azure Search hello genel Önizleme sürümü kullandıysanız `suggesters` daha eski bir boolean özelliği değiştirir (`"suggestions": false`), yalnızca desteklenen önek önerileri için kısa dizeleri (3-25 karakter).</span><span class="sxs-lookup"><span data-stu-id="86e86-498">If you used hello public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span></span> <span data-ttu-id="86e86-499">Kendi değiştirme `suggesters`, destekler infix hello başında veya hello ortasında yer alan içeriği, bir arama dizelerini hatalar için daha iyi tolerans ile eşleşen terimleri bulan eşleşen.</span><span class="sxs-lookup"><span data-stu-id="86e86-499">Its replacement, `suggesters`, supports infix matching that finds matching terms at hello beginning or in hello middle of field content, with better tolerance for mistakes in search strings.</span></span> <span data-ttu-id="86e86-500">Merhaba genel olarak kullanılabilir sürümünden başlayarak, bunu şimdi hello yalnızca hello önerileri API uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-500">Starting with hello generally available release, this is now hello only implementation of hello suggestions API.</span></span> <span data-ttu-id="86e86-501">Merhaba eski `suggestions` sunulmuştur özelliği `api-version=2014-07-31-Preview` toowork bu sürümde devam eder, ancak hello işlemsel değil `2015-02-28` veya Azure Search'ın sonraki sürümleri.</span><span class="sxs-lookup"><span data-stu-id="86e86-501">hello older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues toowork in that version, but is not operational in hello `2015-02-28` or later versions of Azure Search.</span></span>
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a><span data-ttu-id="86e86-502">Dizini Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="86e86-502">Update Index</span></span>
<span data-ttu-id="86e86-503">Bir HTTP PUT İsteği kullanarak Azure Search'te içinde varolan bir dizin güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86e86-503">You can update an existing index within Azure Search using an HTTP PUT request.</span></span> <span data-ttu-id="86e86-504">Güncelleştirmeler CORS seçenekleri değiştirme ve puanlama profilleri değiştirme yeni alanları toohello varolan şema, ekleme içerebilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-504">Updates can include adding new fields toohello existing schema, modifying CORS options, and modifying scoring profiles.</span></span> <span data-ttu-id="86e86-505">Bkz: [eklemek profilleri Puanlama](https://msdn.microsoft.com/library/azure/dn798928.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="86e86-505">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> <span data-ttu-id="86e86-506">Merhaba istek URI'SİNDEKİ hello dizin tooupdate hello adını belirtin:</span><span class="sxs-lookup"><span data-stu-id="86e86-506">You specify hello name of hello index tooupdate on hello request URI:</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="86e86-507">**Önemli:** dizin şeması güncelleştirmelerini desteğidir hello arama dizinini yeniden oluşturmayı gerektirmeyen sınırlı toooperations.</span><span class="sxs-lookup"><span data-stu-id="86e86-507">**Important:** Support for index schema updates is limited toooperations that don't require rebuilding hello search index.</span></span> <span data-ttu-id="86e86-508">Alan türlerinin değiştirilmesi gibi yeniden dizinlemeyi gerektiren hiçbir şema güncelleştirmesi şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="86e86-508">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span></span> <span data-ttu-id="86e86-509">Var olan alanları değiştirilmiş veya silinemez ancak herhangi bir zamanda yeni alanlar eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-509">New fields can be added at any time, although existing fields cannot be changed or deleted.</span></span> <span data-ttu-id="86e86-510">Merhaba aynı çok geçerlidir`suggesters`.</span><span class="sxs-lookup"><span data-stu-id="86e86-510">hello same applies too`suggesters`.</span></span> <span data-ttu-id="86e86-511">Yeni alanlar eklenebilir, başlangıç saati hello alanlarındaki tooa öneri aracı eklenir, ancak alanları öğesinden kaldırılamaz `suggesters` ve var olan alanları çok eklenemez`suggesters`.</span><span class="sxs-lookup"><span data-stu-id="86e86-511">New fields may be added tooa suggester at hello time hello fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added too`suggesters`.</span></span>

<span data-ttu-id="86e86-512">Yeni bir alan tooan dizin eklerken hello dizindeki tüm mevcut belgeleri otomatik olarak bu alan için bir null değer sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="86e86-512">When adding a new field tooan index, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="86e86-513">Yeni belgeler toohello dizin ekleninceye kadar hiçbir ek depolama alanı tüketilebilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-513">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<span data-ttu-id="86e86-514">**İstek**</span><span class="sxs-lookup"><span data-stu-id="86e86-514">**Request**</span></span>

<span data-ttu-id="86e86-515">HTTPS tüm hizmet istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-515">HTTPS is required for all service requests.</span></span> <span data-ttu-id="86e86-516">Merhaba **güncelleştirme dizin** isteği HTTP PUT kullanarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="86e86-516">hello **Update Index** request is constructed using HTTP PUT.</span></span> <span data-ttu-id="86e86-517">PUT ile Merhaba dizin adı hello URL bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-517">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="86e86-518">Merhaba dizin yoksa, oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="86e86-518">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="86e86-519">Merhaba dizini zaten varsa, güncelleştirilmiş toohello yeni tanımı var.</span><span class="sxs-lookup"><span data-stu-id="86e86-519">If hello index already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="86e86-520">Merhaba dizin adı gerekir küçük olması, bir harf veya sayı ile başlamalı, hiçbir eğik çizgi veya nokta olan ve 128 karakterden kısa olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-520">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="86e86-521">Merhaba tire ardışık olmayan sürece hello dizin adı bir harf veya sayı ile başlattıktan sonra hello rest hello adının herhangi harf, sayı ve kısa çizgi, içerebilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-521">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="86e86-522">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="86e86-522">`api-version=[string]` (required).</span></span> <span data-ttu-id="86e86-523">Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="86e86-523">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="86e86-524">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="86e86-524">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="86e86-525">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="86e86-525">**Request Headers**</span></span>

<span data-ttu-id="86e86-526">liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.</span><span class="sxs-lookup"><span data-stu-id="86e86-526">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="86e86-527">`Content-Type`: Gerekli.</span><span class="sxs-lookup"><span data-stu-id="86e86-527">`Content-Type`: Required.</span></span> <span data-ttu-id="86e86-528">Bu çok ayarlama`application/json`</span><span class="sxs-lookup"><span data-stu-id="86e86-528">Set this too`application/json`</span></span>
* <span data-ttu-id="86e86-529">`api-key`: Gerekli.</span><span class="sxs-lookup"><span data-stu-id="86e86-529">`api-key`: Required.</span></span> <span data-ttu-id="86e86-530">Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-530">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="86e86-531">Bu bir dize değeri, benzersiz tooyour hizmeti olur.</span><span class="sxs-lookup"><span data-stu-id="86e86-531">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="86e86-532">Merhaba **güncelleştirme dizin** isteği içermelidir bir `api-key` üstbilgi tooyour yönetici anahtarını (karşılıklı tooa sorgu anahtarı) olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="86e86-532">hello **Update Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="86e86-533">Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-533">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="86e86-534">Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan.</span><span class="sxs-lookup"><span data-stu-id="86e86-534">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="86e86-535">Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="86e86-535">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="86e86-536">**İstek gövdesi sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="86e86-536">**Request Body Syntax**</span></span>

<span data-ttu-id="86e86-537">Varolan bir dizini güncelleştirirken hello gövde hello özgün şema tanımı içermelidir artı hello yanı sıra, eklemekte olduğunuz hello yeni alanlar varsa Puanlama profilleri, ilgili ve CORS seçenekleri değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="86e86-537">When updating an existing index, hello body must include hello original schema definition, plus hello new fields you are adding, as well as hello modified scoring profiles, suggesters and CORS options, if any.</span></span> <span data-ttu-id="86e86-538">Merhaba Puanlama profilleri ve CORS seçenekleri değiştirme değil, başlangıç dizini oluşturulduğu gelen hello orijinal eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-538">If you are not modifying hello scoring profiles and CORS options, you must include hello originals from when hello index was created.</span></span> <span data-ttu-id="86e86-539">Genel güncelleştirmeleri için en iyi düzeni toouse hello tooretrieve hello dizini GET tanımıdır, değiştirin ve sonra PUT ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="86e86-539">In general hello best pattern toouse for updates is tooretrieve hello index definition with a GET, modify it, then update it with PUT.</span></span>

<span data-ttu-id="86e86-540">Merhaba şema sözdizimi dizin burada çoğaltılamaz toocreate kolaylık sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="86e86-540">hello schema syntax used toocreate an index is reproduced here for convenience.</span></span> <span data-ttu-id="86e86-541">Bkz: [Create Index](#CreateIndex) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="86e86-541">See [Create Index](#CreateIndex) for more details.</span></span>

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


<span data-ttu-id="86e86-542">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="86e86-542">**Response**</span></span>

<span data-ttu-id="86e86-543">Başarılı bir istek için: "204 İçerik yok".</span><span class="sxs-lookup"><span data-stu-id="86e86-543">For a successful request: "204 No Content".</span></span>

<span data-ttu-id="86e86-544">Varsayılan olarak hello yanıt gövdesi boş olur.</span><span class="sxs-lookup"><span data-stu-id="86e86-544">By default hello response body will be empty.</span></span> <span data-ttu-id="86e86-545">Ancak, hello `Prefer` istek üstbilgisi çok ayarlamak`return=representation`, hello yanıt gövdesi Merhaba JSON güncelleştirildi hello dizin tanımını içerir.</span><span class="sxs-lookup"><span data-stu-id="86e86-545">However, if hello `Prefer` request header is set too`return=representation`, hello response body will contain hello JSON for hello index definition that was updated.</span></span> <span data-ttu-id="86e86-546">Bu durumda, hello başarı durum kodu olacak "200 Tamam".</span><span class="sxs-lookup"><span data-stu-id="86e86-546">In this case, hello success status code will be "200 OK".</span></span>

<span data-ttu-id="86e86-547">**Dizin tanımı ile özel çözümleyiciler güncelleştiriliyor**</span><span class="sxs-lookup"><span data-stu-id="86e86-547">**Updating index definition with custom analyzers**</span></span>

<span data-ttu-id="86e86-548">Bir analyzer, bir belirteç Oluşturucu, bir belirteç filtre veya char filtre tanımlandıktan sonra değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="86e86-548">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span></span> <span data-ttu-id="86e86-549">Yenilerini yalnızca hello varsa tooan varolan bir dizini eklenebilir `allowIndexDowntime` bayrağı hello dizin güncelleştirme isteğinde tootrue ayarlanır:</span><span class="sxs-lookup"><span data-stu-id="86e86-549">New ones can be added tooan existing index only if hello `allowIndexDowntime` flag is set tootrue in hello index update request:</span></span> 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

<span data-ttu-id="86e86-550">Bu işlem en az birkaç saniye olarak, dizin oluşturma neden ve sorgu dizininizi çevrimdışı sokar Not toofail ister.</span><span class="sxs-lookup"><span data-stu-id="86e86-550">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests toofail.</span></span> <span data-ttu-id="86e86-551">Merhaba dizin performans ve yazma kullanılabilirliğini hello dizin güncelleştirildikten sonra birkaç dakika engelli ya da çok büyük dizinler için daha uzun olabilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-551">Performance and write availability of hello index can be impaired for several minutes after hello index is updated, or longer for very large indexes.</span></span>

<a name="ListIndexes"></a>

## <a name="list-indexes"></a><span data-ttu-id="86e86-552">Liste dizinler</span><span class="sxs-lookup"><span data-stu-id="86e86-552">List Indexes</span></span>
<span data-ttu-id="86e86-553">Merhaba **listesi dizinleri** işlemi listesi döndürülür hello dizinleri şu anda Azure Search hizmetinizin.</span><span class="sxs-lookup"><span data-stu-id="86e86-553">hello **List Indexes** operation returns a list of hello indexes currently in your Azure Search service.</span></span>

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="86e86-554">**İstek**</span><span class="sxs-lookup"><span data-stu-id="86e86-554">**Request**</span></span>

<span data-ttu-id="86e86-555">HTTPS tüm hizmet istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-555">HTTPS is required for all service requests.</span></span> <span data-ttu-id="86e86-556">Merhaba **listesi dizinleri** isteği hello GET yöntemini kullanan olacak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="86e86-556">hello **List Indexes** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="86e86-557">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="86e86-557">`api-version=[string]` (required).</span></span> <span data-ttu-id="86e86-558">Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="86e86-558">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="86e86-559">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="86e86-559">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="86e86-560">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="86e86-560">**Request Headers**</span></span>

<span data-ttu-id="86e86-561">liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.</span><span class="sxs-lookup"><span data-stu-id="86e86-561">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="86e86-562">`api-key`: Gerekli.</span><span class="sxs-lookup"><span data-stu-id="86e86-562">`api-key`: Required.</span></span> <span data-ttu-id="86e86-563">Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-563">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="86e86-564">Bu bir dize değeri, benzersiz tooyour hizmeti olur.</span><span class="sxs-lookup"><span data-stu-id="86e86-564">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="86e86-565">Merhaba **listesi dizinler** isteği içermelidir bir `api-key` kümesi tooan yönetici anahtarı (karşılıklı tooa sorgu anahtarı).</span><span class="sxs-lookup"><span data-stu-id="86e86-565">hello **List Indexes** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="86e86-566">Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-566">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="86e86-567">Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan.</span><span class="sxs-lookup"><span data-stu-id="86e86-567">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="86e86-568">Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="86e86-568">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="86e86-569">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="86e86-569">**Request Body**</span></span>

<span data-ttu-id="86e86-570">yok.</span><span class="sxs-lookup"><span data-stu-id="86e86-570">None.</span></span>

<span data-ttu-id="86e86-571">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="86e86-571">**Response**</span></span>

<span data-ttu-id="86e86-572">Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.</span><span class="sxs-lookup"><span data-stu-id="86e86-572">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="86e86-573">Bir örnek yanıt gövdesi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="86e86-573">Here is an example response body:</span></span>

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

<span data-ttu-id="86e86-574">İlgilendiğiniz toojust hello özellikleri aşağı hello yanıt filtreleyebilirsiniz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="86e86-574">Note that you can filter hello response down toojust hello properties you're interested in.</span></span> <span data-ttu-id="86e86-575">Örneğin, yalnızca dizin adlarının bir listesini istiyorsanız, hello OData kullanın `$select` sorgu seçeneği:</span><span class="sxs-lookup"><span data-stu-id="86e86-575">For example, if you want only a list of index names, use hello OData `$select` query option:</span></span>

    GET /indexes?api-version=2015-02-28-Preview&$select=name

<span data-ttu-id="86e86-576">Bu durumda, yukarıdaki örnek hello hello yanıttan şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="86e86-576">In this case, hello response from hello above example would appear as follows:</span></span>

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

<span data-ttu-id="86e86-577">Dizinleri çok arama hizmetiniz varsa yararlı yöntem toosave bant genişliği budur.</span><span class="sxs-lookup"><span data-stu-id="86e86-577">This is a useful technique toosave bandwidth if you have a lot of indexes in your Search service.</span></span>

<a name="GetIndex"></a>

## <a name="get-index"></a><span data-ttu-id="86e86-578">Dizin Al</span><span class="sxs-lookup"><span data-stu-id="86e86-578">Get Index</span></span>
<span data-ttu-id="86e86-579">Merhaba **alma dizin** işlemi Azure aramadan hello dizin tanımını alır.</span><span class="sxs-lookup"><span data-stu-id="86e86-579">hello **Get Index** operation gets hello index definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="86e86-580">**İstek**</span><span class="sxs-lookup"><span data-stu-id="86e86-580">**Request**</span></span>

<span data-ttu-id="86e86-581">HTTPS istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-581">HTTPS is required for service requests.</span></span> <span data-ttu-id="86e86-582">Merhaba **alma dizin** isteği hello GET yöntemini kullanan olacak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="86e86-582">hello **Get Index** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="86e86-583">Merhaba [dizin adı] hello istek URI'SİNDEKİ hangi dizin tooreturn hello dizinleri koleksiyonundan belirtir.</span><span class="sxs-lookup"><span data-stu-id="86e86-583">hello [index name] in hello request URI specifies which index tooreturn from hello indexes collection.</span></span>

<span data-ttu-id="86e86-584">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="86e86-584">`api-version=[string]` (required).</span></span> <span data-ttu-id="86e86-585">Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="86e86-585">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="86e86-586">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="86e86-586">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="86e86-587">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="86e86-587">**Request Headers**</span></span>

<span data-ttu-id="86e86-588">liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.</span><span class="sxs-lookup"><span data-stu-id="86e86-588">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="86e86-589">`api-key`: Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-589">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="86e86-590">Bu bir dize değeri, benzersiz tooyour hizmeti olur.</span><span class="sxs-lookup"><span data-stu-id="86e86-590">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="86e86-591">Merhaba **alma dizin** isteği içermelidir bir `api-key` kümesi tooan yönetici anahtarı (karşılıklı tooa sorgu anahtarı).</span><span class="sxs-lookup"><span data-stu-id="86e86-591">hello **Get Index** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="86e86-592">Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-592">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="86e86-593">Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan.</span><span class="sxs-lookup"><span data-stu-id="86e86-593">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="86e86-594">Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="86e86-594">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="86e86-595">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="86e86-595">**Request Body**</span></span>

<span data-ttu-id="86e86-596">yok.</span><span class="sxs-lookup"><span data-stu-id="86e86-596">None.</span></span>

<span data-ttu-id="86e86-597">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="86e86-597">**Response**</span></span>

<span data-ttu-id="86e86-598">Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.</span><span class="sxs-lookup"><span data-stu-id="86e86-598">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="86e86-599">Merhaba örnek JSON içinde [oluşturma ve bir dizin güncelleştirme](#CreateUpdateIndexExample) hello yanıt yükü ilişkin bir örnek.</span><span class="sxs-lookup"><span data-stu-id="86e86-599">See hello example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of hello response payload.</span></span>

<a name="DeleteIndex"></a>

## <a name="delete-index"></a><span data-ttu-id="86e86-600">Dizin Sil</span><span class="sxs-lookup"><span data-stu-id="86e86-600">Delete Index</span></span>
<span data-ttu-id="86e86-601">Merhaba **silmek dizin** işlemi, Azure Search hizmetinizin dizin ve ilişkili belgeleri kaldırır.</span><span class="sxs-lookup"><span data-stu-id="86e86-601">hello **Delete Index** operation removes an index and associated documents from your Azure Search service.</span></span> <span data-ttu-id="86e86-602">Merhaba dizin adı hello hizmet hello Azure portal panosunda veya hello API alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86e86-602">You can get hello index name from hello service dashboard in hello Azure portal, or from hello API.</span></span> <span data-ttu-id="86e86-603">Bkz: [listesi dizinleri](#ListIndexes) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="86e86-603">See [List Indexes](#ListIndexes) for details.</span></span>

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="86e86-604">**İstek**</span><span class="sxs-lookup"><span data-stu-id="86e86-604">**Request**</span></span>

<span data-ttu-id="86e86-605">HTTPS istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-605">HTTPS is required for service requests.</span></span> <span data-ttu-id="86e86-606">Merhaba **silmek dizin** isteği hello DELETE yöntemini kullanan olacak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="86e86-606">hello **Delete Index** request can be constructed using hello DELETE method.</span></span>

<span data-ttu-id="86e86-607">Merhaba [dizin adı] hello istek URI'SİNDEKİ hangi dizin toodelete hello dizinleri koleksiyonundan belirtir.</span><span class="sxs-lookup"><span data-stu-id="86e86-607">hello [index name] in hello request URI specifies which index toodelete from hello indexes collection.</span></span>

<span data-ttu-id="86e86-608">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="86e86-608">`api-version=[string]` (required).</span></span> <span data-ttu-id="86e86-609">Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="86e86-609">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="86e86-610">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="86e86-610">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="86e86-611">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="86e86-611">**Request Headers**</span></span>

<span data-ttu-id="86e86-612">liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.</span><span class="sxs-lookup"><span data-stu-id="86e86-612">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="86e86-613">`api-key`: Gerekli.</span><span class="sxs-lookup"><span data-stu-id="86e86-613">`api-key`: Required.</span></span> <span data-ttu-id="86e86-614">Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-614">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="86e86-615">Bir dize değeri, benzersiz tooyour hizmeti URL'si değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-615">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="86e86-616">Merhaba **silmek dizin** isteği içermelidir bir `api-key` üstbilgi tooyour yönetici anahtarını (karşılıklı tooa sorgu anahtarı) olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="86e86-616">hello **Delete Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="86e86-617">Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-617">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="86e86-618">Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan.</span><span class="sxs-lookup"><span data-stu-id="86e86-618">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="86e86-619">Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="86e86-619">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="86e86-620">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="86e86-620">**Request Body**</span></span>

<span data-ttu-id="86e86-621">yok.</span><span class="sxs-lookup"><span data-stu-id="86e86-621">None.</span></span>

<span data-ttu-id="86e86-622">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="86e86-622">**Response**</span></span>

<span data-ttu-id="86e86-623">Durum kodu: 204 Hayır içerik için başarılı bir yanıt döndürülür.</span><span class="sxs-lookup"><span data-stu-id="86e86-623">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a><span data-ttu-id="86e86-624">Dizin istatistikleri Al</span><span class="sxs-lookup"><span data-stu-id="86e86-624">Get Index Statistics</span></span>
<span data-ttu-id="86e86-625">Merhaba **dizin istatistikleri almak** işlemi hello geçerli dizin yanı sıra, depolama alanı kullanımı için bir belge sayısı Azure aramadan döndürür.</span><span class="sxs-lookup"><span data-stu-id="86e86-625">hello **Get Index Statistics** operation returns from Azure Search a document count for hello current index, plus storage usage.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="86e86-626">Belge sayısını ve depolama boyutunu istatistiklerle değil gerçek zamanlı olarak birkaç dakikada toplanır.</span><span class="sxs-lookup"><span data-stu-id="86e86-626">Statistics on document count and storage size are collected every few minutes, not in real time.</span></span> <span data-ttu-id="86e86-627">Bu nedenle, bu API tarafından döndürülen hello istatistikleri son dizin oluşturma işlemleri tarafından yapılan değişiklikler neden yansıtmayabilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-627">Therefore, hello statistics returned by this API may not reflect changes caused by recent indexing operations.</span></span>
> 
> 

<span data-ttu-id="86e86-628">**İstek**</span><span class="sxs-lookup"><span data-stu-id="86e86-628">**Request**</span></span>

<span data-ttu-id="86e86-629">HTTPS tüm hizmetleri istekler için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-629">HTTPS is required for all services requests.</span></span> <span data-ttu-id="86e86-630">Merhaba **dizin istatistikleri almak** isteği hello GET yöntemini kullanan olacak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="86e86-630">hello **Get Index Statistics** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="86e86-631">Merhaba [dizin adı] hello istek URI'SİNDEKİ hello hizmet tooreturn dizin istatistikleri hello belirtilen dizin için söyler.</span><span class="sxs-lookup"><span data-stu-id="86e86-631">hello [index name] in hello request URI tells hello service tooreturn index statistics for hello specified index.</span></span>

<span data-ttu-id="86e86-632">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="86e86-632">`api-version=[string]` (required).</span></span> <span data-ttu-id="86e86-633">Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="86e86-633">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="86e86-634">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="86e86-634">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="86e86-635">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="86e86-635">**Request Headers**</span></span>

<span data-ttu-id="86e86-636">liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.</span><span class="sxs-lookup"><span data-stu-id="86e86-636">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="86e86-637">`api-key`: Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-637">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="86e86-638">Bu bir dize değeri, benzersiz tooyour hizmeti olur.</span><span class="sxs-lookup"><span data-stu-id="86e86-638">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="86e86-639">Merhaba **dizin istatistikleri almak** isteği içermelidir bir `api-key` kümesi tooan yönetici anahtarı (karşılıklı tooa sorgu anahtarı).</span><span class="sxs-lookup"><span data-stu-id="86e86-639">hello **Get Index Statistics** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="86e86-640">Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-640">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="86e86-641">Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan.</span><span class="sxs-lookup"><span data-stu-id="86e86-641">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="86e86-642">Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="86e86-642">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="86e86-643">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="86e86-643">**Request Body**</span></span>

<span data-ttu-id="86e86-644">yok.</span><span class="sxs-lookup"><span data-stu-id="86e86-644">None.</span></span>

<span data-ttu-id="86e86-645">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="86e86-645">**Response**</span></span>

<span data-ttu-id="86e86-646">Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.</span><span class="sxs-lookup"><span data-stu-id="86e86-646">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="86e86-647">Merhaba yanıt gövdesi hello biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="86e86-647">hello response body is in hello following format:</span></span>

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a><span data-ttu-id="86e86-648">Testi Çözümleyicisi</span><span class="sxs-lookup"><span data-stu-id="86e86-648">Test Analyzer</span></span>
<span data-ttu-id="86e86-649">Merhaba **analiz API** nasıl bir Çözümleyicisi belirteçlere metni keser. gösterir.</span><span class="sxs-lookup"><span data-stu-id="86e86-649">hello **Analyze API** shows how an analyzer breaks text into tokens.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="86e86-650">**İstek**</span><span class="sxs-lookup"><span data-stu-id="86e86-650">**Request**</span></span>

<span data-ttu-id="86e86-651">HTTPS tüm hizmetleri istekler için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-651">HTTPS is required for all services requests.</span></span> <span data-ttu-id="86e86-652">Merhaba **analiz API** isteği hello POST yöntemini kullanan olacak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="86e86-652">hello **Analyze API** request can be constructed using hello POST method.</span></span>

<span data-ttu-id="86e86-653">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="86e86-653">`api-version=[string]` (required).</span></span> <span data-ttu-id="86e86-654">Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="86e86-654">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="86e86-655">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="86e86-655">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="86e86-656">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="86e86-656">**Request Headers**</span></span>

<span data-ttu-id="86e86-657">liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.</span><span class="sxs-lookup"><span data-stu-id="86e86-657">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="86e86-658">`api-key`: Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-658">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="86e86-659">Bu bir dize değeri, benzersiz tooyour hizmeti olur.</span><span class="sxs-lookup"><span data-stu-id="86e86-659">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="86e86-660">Merhaba **analiz API** isteği içermelidir bir `api-key` kümesi tooan yönetici anahtarı (karşılıklı tooa sorgu anahtarı).</span><span class="sxs-lookup"><span data-stu-id="86e86-660">hello **Analyze API** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="86e86-661">Merhaba dizin adı ve hello hizmet adı tooconstruct hello istek URL'si de gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-661">You will also need hello index name and hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="86e86-662">Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan.</span><span class="sxs-lookup"><span data-stu-id="86e86-662">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="86e86-663">Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="86e86-663">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="86e86-664">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="86e86-664">**Request Body**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

<span data-ttu-id="86e86-665">or</span><span class="sxs-lookup"><span data-stu-id="86e86-665">or</span></span>

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

<span data-ttu-id="86e86-666">Merhaba `analyzer_name`, `tokenizer_name`, `token_filter_name` ve `char_filter_name` hello dizini için önceden tanımlanmış veya özel çözümleyiciler, tokenizers, belirteç filtreleri ve char filtreleri geçerli adlarını toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-666">hello `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need toobe valid names of predefined or custom analyzers, tokenizers, token filters and char filters for hello index.</span></span> <span data-ttu-id="86e86-667">sözcük analiz hello işlemi hakkında daha fazla toolearn [analiz Azure Search'te](https://aka.ms/azsanalysis).</span><span class="sxs-lookup"><span data-stu-id="86e86-667">toolearn more about hello process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span></span>

<span data-ttu-id="86e86-668">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="86e86-668">**Response**</span></span>

<span data-ttu-id="86e86-669">Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.</span><span class="sxs-lookup"><span data-stu-id="86e86-669">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="86e86-670">Merhaba yanıt gövdesi hello biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="86e86-670">hello response body is in hello following format:</span></span>

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

<span data-ttu-id="86e86-671">**API örnek Çözümle**</span><span class="sxs-lookup"><span data-stu-id="86e86-671">**Analyze API example**</span></span>

<span data-ttu-id="86e86-672">**İstek**</span><span class="sxs-lookup"><span data-stu-id="86e86-672">**Request**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

<span data-ttu-id="86e86-673">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="86e86-673">**Response**</span></span>

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a><span data-ttu-id="86e86-674">Belge işlemleri</span><span class="sxs-lookup"><span data-stu-id="86e86-674">Document Operations</span></span>
<span data-ttu-id="86e86-675">Azure Search'te bir dizine hello bulutta depolanan ve toohello hizmet karşıya JSON belgelerini kullanarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="86e86-675">In Azure Search, an index is stored in hello cloud and populated using JSON documents that you upload toohello service.</span></span> <span data-ttu-id="86e86-676">Karşıya yüklediğiniz tüm hello belgeleri hello gövde arama verilerinizin kapsar.</span><span class="sxs-lookup"><span data-stu-id="86e86-676">All hello documents that you upload comprise hello corpus of your search data.</span></span> <span data-ttu-id="86e86-677">Belgeleri karşıya gibi bazıları arama terimleri simgeleştirilmiş alanlar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-677">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span></span> <span data-ttu-id="86e86-678">Merhaba `/docs` hello Azure Search API URL kesimi dizin belgelerde hello koleksiyonunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="86e86-678">hello `/docs` URL segment in hello Azure Search API represents hello collection of documents in an index.</span></span> <span data-ttu-id="86e86-679">Karşıya yükleme gibi hello koleksiyon üzerinde gerçekleştirilen tüm işlemleri, birleştirme, silme veya belgeleri sorgulama sürer bunu hello URL'leri tek bir dizin Merhaba içeriğine yerinde bu işlemlerin her zaman ile başlar için `/indexes/[index name]/docs` için belirtilen dizin adı.</span><span class="sxs-lookup"><span data-stu-id="86e86-679">All operations performed on hello collection such as uploading, merging, deleting, or querying documents take place in hello context of a single index, so hello URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span></span>

<span data-ttu-id="86e86-680">Uygulama kodunuz JSON belgeleri tooupload tooAzure arama ya da oluşturmanız gerekir veya kullanabileceğiniz bir [dizin oluşturucu](https://msdn.microsoft.com/library/dn946891.aspx) tooload belgeleri hello veri kaynağı Azure SQL Database veya Azure Cosmos DB ise.</span><span class="sxs-lookup"><span data-stu-id="86e86-680">Your application code must either generate JSON documents tooupload tooAzure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) tooload documents if hello data source is either Azure SQL Database or Azure Cosmos DB.</span></span> <span data-ttu-id="86e86-681">Genellikle, dizinleri sağlayan bir tek veri kümesinden doldurulur.</span><span class="sxs-lookup"><span data-stu-id="86e86-681">Typically, indexes are populated from a single dataset that you provide.</span></span>

<span data-ttu-id="86e86-682">Toosearch istediğiniz her bir öğe için bir belge sahip planlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-682">You should plan on having one document for each item that you want toosearch.</span></span> <span data-ttu-id="86e86-683">Film kiralama uygulamasının film başına tek bir belgenin olabilir, bir mağaza uygulaması SKU başına tek bir belgenin olabilir, bir çevrimiçi eğitim malzemesi uygulamasının indirmelere başına tek bir belgenin olabilir, araştırma kesin bir belgeyi her akademik kağıt olabilir kendi Depo ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="86e86-683">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span></span>

<span data-ttu-id="86e86-684">Belgeler bir veya daha fazla alan oluşur.</span><span class="sxs-lookup"><span data-stu-id="86e86-684">Documents consist of one or more fields.</span></span> <span data-ttu-id="86e86-685">Alanları Azure Search tarafından arama terimleri simgeleştirilmiş yanı sıra dışı simgeleştirilmiş metin veya filtreleri veya Puanlama profilleri kullanılabilir metin dışı değerleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-685">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span></span> <span data-ttu-id="86e86-686">Merhaba adları, veri türleri ve her bir alan için desteklenen arama özellikleri hello dizin şemasına göre belirlenir.</span><span class="sxs-lookup"><span data-stu-id="86e86-686">hello names, data types, and search features supported for each field are determined by hello index schema.</span></span> <span data-ttu-id="86e86-687">Her dizin şemasında hello alanlardan biri bir kimliği olarak işaretlenmesi gerekir ve her bir belgenin bu belgede hello dizini benzersiz olarak tanıtan hello Kimliği alanı için bir değer olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-687">One of hello fields in each index schema must be designated as an ID, and each document must have a value for hello ID field that uniquely identifies that document in hello index.</span></span> <span data-ttu-id="86e86-688">Diğer tüm belge alanlarını isteğe bağlıdır ve sol belirtilmezse varsayılan tooa null değer kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="86e86-688">All other document fields are optional and will default tooa null value if left unspecified.</span></span> <span data-ttu-id="86e86-689">Null değerler hello arama dizini yer almayan unutmayın.</span><span class="sxs-lookup"><span data-stu-id="86e86-689">Note that null values do not take up space in hello search index.</span></span>

<span data-ttu-id="86e86-690">Belgeleri yüklemeden önce başlangıç dizini hello hizmette oluşturmuş olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="86e86-690">Before you can upload documents, you must have already created hello index on hello service.</span></span> <span data-ttu-id="86e86-691">Bkz: [Create Index](#CreateIndex) birinci adım hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="86e86-691">See [Create Index](#CreateIndex) for details about this first step.</span></span>

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a><span data-ttu-id="86e86-692">Ekleme, güncelleştirme, belgeleri veya silme</span><span class="sxs-lookup"><span data-stu-id="86e86-692">Add, Update, or Delete Documents</span></span>
<span data-ttu-id="86e86-693">Karşıya yüklediğiniz, HTTP POST kullanılarak belirtilen bir dizinden birleştirme, birleştirme veya karşıya yükleme veya delete belgeleri.</span><span class="sxs-lookup"><span data-stu-id="86e86-693">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span> <span data-ttu-id="86e86-694">Güncelleştirmeler için çok sayıda (too1000 belgeleri toplu iş başına) veya toplu iş başına yaklaşık 16 MB belgelerin toplu işleme önerilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-694">For large numbers of updates, batching of documents (up too1000 documents per batch or about 16 MB per batch) is recommended.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="86e86-695">**İstek**</span><span class="sxs-lookup"><span data-stu-id="86e86-695">**Request**</span></span>

<span data-ttu-id="86e86-696">HTTPS tüm hizmet istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-696">HTTPS is required for all service requests.</span></span> <span data-ttu-id="86e86-697">Karşıya yüklediğiniz, HTTP POST kullanılarak belirtilen bir dizinden birleştirme, birleştirme veya karşıya yükleme veya delete belgeleri.</span><span class="sxs-lookup"><span data-stu-id="86e86-697">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span>

<span data-ttu-id="86e86-698">URI içerir [dizin adı] hello isteği hangi dizin toopost belgeler belirtme.</span><span class="sxs-lookup"><span data-stu-id="86e86-698">hello request URI includes [index name], specifying which index toopost documents.</span></span> <span data-ttu-id="86e86-699">Bu gibi durumlarda, belgeleri tooone dizin yalnızca aynı anda nakledebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86e86-699">You can only post documents tooone index at a time.</span></span>

<span data-ttu-id="86e86-700">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="86e86-700">`api-version=[string]` (required).</span></span> <span data-ttu-id="86e86-701">Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="86e86-701">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="86e86-702">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="86e86-702">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="86e86-703">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="86e86-703">**Request Headers**</span></span>

<span data-ttu-id="86e86-704">liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.</span><span class="sxs-lookup"><span data-stu-id="86e86-704">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="86e86-705">`Content-Type`: Gerekli.</span><span class="sxs-lookup"><span data-stu-id="86e86-705">`Content-Type`: Required.</span></span> <span data-ttu-id="86e86-706">Bu çok ayarlama`application/json`</span><span class="sxs-lookup"><span data-stu-id="86e86-706">Set this too`application/json`</span></span>
* <span data-ttu-id="86e86-707">`api-key`: Gerekli.</span><span class="sxs-lookup"><span data-stu-id="86e86-707">`api-key`: Required.</span></span> <span data-ttu-id="86e86-708">Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-708">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="86e86-709">Bu bir dize değeri, benzersiz tooyour hizmeti olur.</span><span class="sxs-lookup"><span data-stu-id="86e86-709">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="86e86-710">Merhaba **ekleme belgeleri** isteği içermelidir bir `api-key` üstbilgi tooyour yönetici anahtarını (karşılıklı tooa sorgu anahtarı) olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="86e86-710">hello **Add Documents** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="86e86-711">Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-711">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="86e86-712">Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan.</span><span class="sxs-lookup"><span data-stu-id="86e86-712">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="86e86-713">Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="86e86-713">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="86e86-714">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="86e86-714">**Request Body**</span></span>

<span data-ttu-id="86e86-715">Daha fazla belgeleri toobe Hello hello istek gövdesi içeriyor veya dizini.</span><span class="sxs-lookup"><span data-stu-id="86e86-715">hello body of hello request contains one or more documents toobe indexed.</span></span> <span data-ttu-id="86e86-716">Belgeler, benzersiz bir anahtar tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="86e86-716">Documents are identified by a unique key.</span></span> <span data-ttu-id="86e86-717">Her bir eylem ile ilişkili bir belgedir: karşıya yükleme, birleştirme, mergeOrUpload veya Sil.</span><span class="sxs-lookup"><span data-stu-id="86e86-717">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span></span> <span data-ttu-id="86e86-718">Karşıya yükleme istekleri hello belge verileri içeren bir anahtar/değer çiftleri kümesi olarak olarak gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-718">Upload requests must include hello document data as a set of key/value pairs.</span></span>

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> <span data-ttu-id="86e86-719">Belge anahtarları yalnızca harf, sayı, kısa çizgi içerebilir ("-"), alt çizgi ("_") ve eşittir işareti ("=").</span><span class="sxs-lookup"><span data-stu-id="86e86-719">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span></span> <span data-ttu-id="86e86-720">Daha fazla ayrıntı için bkz: [adlandırma kurallarını](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span><span class="sxs-lookup"><span data-stu-id="86e86-720">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span></span>
> 
> 

<span data-ttu-id="86e86-721">**Belge eylemleri**</span><span class="sxs-lookup"><span data-stu-id="86e86-721">**Document Actions**</span></span>

* <span data-ttu-id="86e86-722">`upload`: Bir karşıya yükleme benzer tooan "upsert" nerede hello belgenin yeni olması durumunda ekleneceği ve olması mevcut durumunda güncelleştirileceği/değiştirileceği bir eylemdir.</span><span class="sxs-lookup"><span data-stu-id="86e86-722">`upload`: An upload action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> <span data-ttu-id="86e86-723">Tüm alanlar hello güncelleştirme durumda yerini aldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="86e86-723">Note that all fields are replaced in hello update case.</span></span>
* <span data-ttu-id="86e86-724">`merge`: Varolan bir belge ile hello birleştirme güncelleştirmeleri alanları belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="86e86-724">`merge`: Merge updates an existing document with hello specified fields.</span></span> <span data-ttu-id="86e86-725">Merhaba belge yoksa, hello birleştirme işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="86e86-725">If hello document doesn't exist, hello merge will fail.</span></span> <span data-ttu-id="86e86-726">Birleştirmede belirttiğiniz herhangi bir alan varolan bir alana hello hello belgedeki yerini alır.</span><span class="sxs-lookup"><span data-stu-id="86e86-726">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="86e86-727">Buna `Collection(Edm.String)` türünde alanlar dahildir.</span><span class="sxs-lookup"><span data-stu-id="86e86-727">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="86e86-728">Örneğin, hello belge "etiketler" değerine sahip bir alan varsa, `["budget"]` ve değeriyle bir birleştirme yürütme `["economy", "pool"]` "etiketleri için" Merhaba "etiketler" alanının son değeri hello olacaktır `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="86e86-728">For example, if hello document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", hello final value of hello "tags" field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="86e86-729">İçinde **değil** olması `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="86e86-729">It will **not** be `["budget", "economy", "pool"]`.</span></span>
* <span data-ttu-id="86e86-730">`mergeOrUpload`: gibi davranır `merge` anahtar zaten verilen hello belgeyle hello dizinde varsa.</span><span class="sxs-lookup"><span data-stu-id="86e86-730">`mergeOrUpload`: behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="86e86-731">Merhaba belge mevcut değilse gibi davranır `upload` yeni bir belgeyle.</span><span class="sxs-lookup"><span data-stu-id="86e86-731">If hello document does not exist it behaves like `upload` with a new document.</span></span>
* <span data-ttu-id="86e86-732">`delete`: Delete hello belirtilen belge hello dizinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="86e86-732">`delete`: Delete removes hello specified document from hello index.</span></span> <span data-ttu-id="86e86-733">Belirttiğiniz tüm alanlar içinde olduğunu unutmayın bir `delete` işlemi hello anahtar alanı dışında yok sayılacak.</span><span class="sxs-lookup"><span data-stu-id="86e86-733">Note that any fields you specify in a `delete` operation other than hello key field will be ignored.</span></span> <span data-ttu-id="86e86-734">Bir belgeden tek bir alanı tooremove istiyorsanız kullanın `merge` yerine ve basit şekilde hello alan açıkça çok kümesi`null`.</span><span class="sxs-lookup"><span data-stu-id="86e86-734">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly too`null`.</span></span>

<span data-ttu-id="86e86-735">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="86e86-735">**Response**</span></span>

<span data-ttu-id="86e86-736">Durum kodu 200 (Tamam) tüm öğeleri başarıyla eklenmemiş anlamı başarılı bir yanıt için döndürülür.</span><span class="sxs-lookup"><span data-stu-id="86e86-736">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span></span> <span data-ttu-id="86e86-737">Bu hello tarafından belirtilir `status` tootrue tüm öğeleri yanı sıra hello için ayarlanan özelliği `statusCode` tooeither 201 (için yeni yüklenen belgeleri için) veya 200 (için birleştirilmiş veya Silinen Belge) ayarlanan özelliği:</span><span class="sxs-lookup"><span data-stu-id="86e86-737">This is indicated by hello `status` property being set tootrue for all items, as well as hello `statusCode` property being set tooeither 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

<span data-ttu-id="86e86-738">En az bir öğenin dizine alınması başarısız olduğunda 207 (çok durumu) durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="86e86-738">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="86e86-739">Dizine öğeleri sahip hello `status` alanını toofalse ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="86e86-739">Items that have not been indexed have hello `status` field set toofalse.</span></span> <span data-ttu-id="86e86-740">Merhaba `errorMessage` ve `statusCode` özellikleri hata dizin hello hello nedeni gösterir:</span><span class="sxs-lookup"><span data-stu-id="86e86-740">hello `errorMessage` and `statusCode` properties will indicate hello reason for hello indexing error:</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

<span data-ttu-id="86e86-741">Aşağıdaki tablonun hello çeşitli hello yanıtta döndürülen durum kodları belge başına hello açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="86e86-741">hello following table explains hello various per-document status codes that can be returned in hello response.</span></span> <span data-ttu-id="86e86-742">Başkalarının geçici hata koşulları belirtmek karşın bazı sorunları hello isteği kendisi ile olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="86e86-742">Note that some indicate problems with hello request itself, while others indicate temporary error conditions.</span></span> <span data-ttu-id="86e86-743">Merhaba ikinci bir gecikmeden sonra yeniden denemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-743">hello latter you should retry after a delay.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="86e86-744">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="86e86-744">Status code</span></span></th>
        <th><span data-ttu-id="86e86-745">Anlamı</span><span class="sxs-lookup"><span data-stu-id="86e86-745">Meaning</span></span></th>
        <th><span data-ttu-id="86e86-746">Yeniden denenebilir</span><span class="sxs-lookup"><span data-stu-id="86e86-746">Retryable</span></span></th>
        <th><span data-ttu-id="86e86-747">Notlar</span><span class="sxs-lookup"><span data-stu-id="86e86-747">Notes</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-748">200</span><span class="sxs-lookup"><span data-stu-id="86e86-748">200</span></span></td>
        <td><span data-ttu-id="86e86-749">Belge başarıyla değiştirilmiş veya silinmiş.</span><span class="sxs-lookup"><span data-stu-id="86e86-749">Document was successfully modified or deleted.</span></span></td>
        <td><span data-ttu-id="86e86-750">yok</span><span class="sxs-lookup"><span data-stu-id="86e86-750">n/a</span></span></td>
        <td><span data-ttu-id="86e86-751">Silme işlemlerine olan <a href="https://en.wikipedia.org/wiki/Idempotence">ıdempotent</a>.</span><span class="sxs-lookup"><span data-stu-id="86e86-751">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span> <span data-ttu-id="86e86-752">Diğer bir deyişle, bir belge anahtarı hello dizininde mevcut değilse, bu anahtara sahip bir silme işlemini denemeden 200 durum koduna neden olur.</span><span class="sxs-lookup"><span data-stu-id="86e86-752">That is, even if a document key does not exist in hello index, attempting a delete operation with that key will result in a 200 status code.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-753">201</span><span class="sxs-lookup"><span data-stu-id="86e86-753">201</span></span></td>
        <td><span data-ttu-id="86e86-754">Belge başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="86e86-754">Document was successfully created.</span></span></td>
        <td><span data-ttu-id="86e86-755">yok</span><span class="sxs-lookup"><span data-stu-id="86e86-755">n/a</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-756">400</span><span class="sxs-lookup"><span data-stu-id="86e86-756">400</span></span></td>
        <td><span data-ttu-id="86e86-757">Merhaba belgedeki dizine alınmasını engelleyen bir hata vardı.</span><span class="sxs-lookup"><span data-stu-id="86e86-757">There was an error in hello document that prevented it from being indexed.</span></span></td>
        <td><span data-ttu-id="86e86-758">Hayır</span><span class="sxs-lookup"><span data-stu-id="86e86-758">No</span></span></td>
        <td><span data-ttu-id="86e86-759">Merhaba hata iletisi hello yanıt hello belgeyle nerede olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="86e86-759">hello error message in hello response will indicate what is wrong with hello document.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-760">404</span><span class="sxs-lookup"><span data-stu-id="86e86-760">404</span></span></td>
        <td><span data-ttu-id="86e86-761">anahtarı verilen hello hello dizininde mevcut olmadığından hello belge birleştirilemeyen.</span><span class="sxs-lookup"><span data-stu-id="86e86-761">hello document could not be merged because hello given key doesn't exist in hello index.</span></span></td>
        <td><span data-ttu-id="86e86-762">Hayır</span><span class="sxs-lookup"><span data-stu-id="86e86-762">No</span></span></td>
        <td><span data-ttu-id="86e86-763">Bu hata yüklemeler için yeni belgeler oluşturma ve olduklarından silme işlemi için oluşmaz oluşmaz <a href="https://en.wikipedia.org/wiki/Idempotence">ıdempotent</a>.</span><span class="sxs-lookup"><span data-stu-id="86e86-763">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-764">409</span><span class="sxs-lookup"><span data-stu-id="86e86-764">409</span></span></td>
        <td><span data-ttu-id="86e86-765">Sürüm çakışması tooindex bir belge çalışırken algılandı.</span><span class="sxs-lookup"><span data-stu-id="86e86-765">A version conflict was detected when attempting tooindex a document.</span></span></td>
        <td><span data-ttu-id="86e86-766">Evet</span><span class="sxs-lookup"><span data-stu-id="86e86-766">Yes</span></span></td>
        <td><span data-ttu-id="86e86-767">Bu durum, aynı anda birden fazla kez belge tooindex hello çalıştığınız ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="86e86-767">This can happen when you're trying tooindex hello same document more than once concurrently.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-768">422</span><span class="sxs-lookup"><span data-stu-id="86e86-768">422</span></span></td>
        <td><span data-ttu-id="86e86-769">Merhaba 'allowIndexDowntime' bayrak kümesi too'true ile güncellendiğinden Merhaba dizin geçici olarak devre dışı '.</span><span class="sxs-lookup"><span data-stu-id="86e86-769">hello index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'.</span></span></td>
        <td><span data-ttu-id="86e86-770">Evet</span><span class="sxs-lookup"><span data-stu-id="86e86-770">Yes</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="86e86-771">503</span><span class="sxs-lookup"><span data-stu-id="86e86-771">503</span></span></td>
        <td><span data-ttu-id="86e86-772">Arama hizmetinizi büyük olasılıkla tooheavy yük geçici olarak kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="86e86-772">Your search service is temporarily unavailable, possibly due tooheavy load.</span></span></td>
        <td><span data-ttu-id="86e86-773">Evet</span><span class="sxs-lookup"><span data-stu-id="86e86-773">Yes</span></span></td>
        <td><span data-ttu-id="86e86-774">Kodunuzu bu durumda yeniden denemeden önce beklemesi gereken veya hello hizmet kullanılamazlık uzatma risk.</span><span class="sxs-lookup"><span data-stu-id="86e86-774">Your code should wait before retrying in this case or you risk prolonging hello service unavailability.</span></span></td>
    </tr>
</table> 

<span data-ttu-id="86e86-775">**Not**: istemci kodunuzun sık 207 yanıtı karşılaşırsa, olası bir nedeni hello sistem yük altında olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-775">**Note**: If your client code frequently encounters a 207 response, one possible reason is that hello system is under load.</span></span> <span data-ttu-id="86e86-776">Bu hello denetleyerek doğrulayabilirsiniz `statusCode` 503 özelliği.</span><span class="sxs-lookup"><span data-stu-id="86e86-776">You can confirm this by checking hello `statusCode` property for 503.</span></span> <span data-ttu-id="86e86-777">Öneririz bu hello durumda olup olmadığını, ***dizin oluşturma isteklerinin azaltma***.</span><span class="sxs-lookup"><span data-stu-id="86e86-777">If this is hello case, we recommend ***throttling indexing requests***.</span></span> <span data-ttu-id="86e86-778">Aksi takdirde, dizin oluşturma trafiği subside değil, hello sistem 503 hataları olan tüm istekleri reddetme başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86e86-778">Otherwise, if indexing traffic doesn't subside, hello system could start rejecting all requests with 503 errors.</span></span>

<span data-ttu-id="86e86-779">Durum kodu 429 hello dizin başına belge sayısı Kotanızı aştınız gösterir.</span><span class="sxs-lookup"><span data-stu-id="86e86-779">Status code 429 indicates that you have exceeded your quota on hello number of documents per index.</span></span> <span data-ttu-id="86e86-780">Yeni bir dizin oluşturabilir veya için daha yüksek kapasite limitlerini yükseltin.</span><span class="sxs-lookup"><span data-stu-id="86e86-780">You must either create a new index or upgrade for higher capacity limits.</span></span>

<span data-ttu-id="86e86-781">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="86e86-781">**Example:**</span></span>

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
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a><span data-ttu-id="86e86-782">Belge ara</span><span class="sxs-lookup"><span data-stu-id="86e86-782">Search Documents</span></span>
<span data-ttu-id="86e86-783">A **arama** işlemi bir GET veya POST talebi olarak verilir ve eşleşen belgeleri seçmek için hello ölçütleri vermek parametreleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="86e86-783">A **Search** operation is issued as a GET or POST request and specifies parameters that give hello criteria for selecting matching documents.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="86e86-784">**Toouse yerine duyurduğumuzda Al**</span><span class="sxs-lookup"><span data-stu-id="86e86-784">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="86e86-785">HTTP GET toocall hello kullandığınızda **arama** API, toobe hello istek URL'si hello uzunluğu 8 KB'yi aşamaz kullanan gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-785">When you use HTTP GET toocall hello **Search** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="86e86-786">Çoğu uygulama için yeterince genellikle budur.</span><span class="sxs-lookup"><span data-stu-id="86e86-786">This is usually enough for most applications.</span></span> <span data-ttu-id="86e86-787">Ancak, bazı uygulamalar çok büyük sorgular veya OData filtre ifadeleri üretir.</span><span class="sxs-lookup"><span data-stu-id="86e86-787">However, some applications produce very large queries or OData filter expressions.</span></span> <span data-ttu-id="86e86-788">Daha büyük filtreleri ve sorguları get'ten sağladığından bu uygulamalar için HTTP POST kullanılarak daha iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="86e86-788">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span></span> <span data-ttu-id="86e86-789">POST, koşulları veya bir sorgu yan tümcelerinde hello sayısı ile hello faktörü, değil hello istek boyutu sınırını POST için yaklaşık 16 MB olduğundan hello ham sorgu hello boyutu sınırlama değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-789">With POST, hello number of terms or clauses in a query is hello limiting factor, not hello size of hello raw query since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-790">Merhaba POST isteği boyut sınırı çok büyük olsa bile arama sorguları ve filtre ifadeleri rasgele karmaşık olamaz.</span><span class="sxs-lookup"><span data-stu-id="86e86-790">Even though hello POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="86e86-791">Bkz: [Lucene sorgu söz dizimi](https://msdn.microsoft.com/library/mt589323.aspx) ve [OData ifade sözdizimini](https://msdn.microsoft.com/library/dn798921.aspx) arama sorgusu ve filtre karmaşıklık sınırlamalar hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="86e86-791">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="86e86-792">**İstek**</span><span class="sxs-lookup"><span data-stu-id="86e86-792">**Request**</span></span>

<span data-ttu-id="86e86-793">HTTPS istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-793">HTTPS is required for service requests.</span></span> <span data-ttu-id="86e86-794">Merhaba **arama** isteği hello GET veya POST yöntemleri kullanarak olacak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="86e86-794">hello **Search** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="86e86-795">Merhaba isteğin URI hello parametreleriyle eşleşen tüm belgeler için hangi dizin tooquery belirtir.</span><span class="sxs-lookup"><span data-stu-id="86e86-795">hello request URI specifies which index tooquery, for all documents that match hello parameters.</span></span> <span data-ttu-id="86e86-796">Parametreleri hello sorgu dizesinde GET isteklerinin hello durumda belirtilir ve hello istekte hello durumunun POST gövdesinde ister.</span><span class="sxs-lookup"><span data-stu-id="86e86-796">Parameters are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="86e86-797">GET isteklerini oluştururken en iyi uygulama, çok unutmayın[URL kodlama](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) çağrılırken parametreleri hello REST API doğrudan belirli sorgu.</span><span class="sxs-lookup"><span data-stu-id="86e86-797">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="86e86-798">İçin **arama** bu işlemleri içerir:</span><span class="sxs-lookup"><span data-stu-id="86e86-798">For **Search** operations, this includes:</span></span>

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

<span data-ttu-id="86e86-799">URL kodlaması sorgu parametreleri yukarıda hello üzerinde yalnızca önerilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-799">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="86e86-800">Tüm sorgu dizesi (her şeyi hello sonra?), yanlışlıkla URL kodlama Merhaba, istekleri çalışmamasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="86e86-800">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="86e86-801">Ayrıca, URL kodlaması yalnızca REST API kullanarak doğrudan alma hello çağrılırken gereklidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-801">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="86e86-802">Hiçbir URL kodlaması çağrılırken gereklidir **arama** POST, kullanma ya da hello kullanırken [.NET istemci kitaplığını](https://msdn.microsoft.com/library/dn951165.aspx), sizin için URL kodlaması işler.</span><span class="sxs-lookup"><span data-stu-id="86e86-802">No URL encoding is necessary when calling **Search** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="86e86-803"><a name="SearchQueryParameters"></a>
**Sorgu parametreleri**</span><span class="sxs-lookup"><span data-stu-id="86e86-803"><a name="SearchQueryParameters"></a>
**Query Parameters**</span></span>

<span data-ttu-id="86e86-804">**Arama** sorgu ölçütlerini sağlayan ve ayrıca arama davranışını belirtin birkaç parametre kabul eder.</span><span class="sxs-lookup"><span data-stu-id="86e86-804">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="86e86-805">Bu parametreler hello URL'deki sorgu dizesi çağrılırken sağladığınız **arama** GET aracılığıyla ve JSON özellikleri çağrılırken hello istek gövdesi olarak **arama** POST ile.</span><span class="sxs-lookup"><span data-stu-id="86e86-805">You provide these parameters in hello URL query string when calling **Search** via GET, and as JSON properties in hello request body when calling **Search** via POST.</span></span> <span data-ttu-id="86e86-806">bazı parametreler için Hello sözdizimi GET ve POST arasında biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-806">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="86e86-807">Bu farklılıklar, geçerli aşağıda belirtilmiştir:</span><span class="sxs-lookup"><span data-stu-id="86e86-807">These differences are noted as applicable below:</span></span>

<span data-ttu-id="86e86-808">`search=[string]`(isteğe bağlı) - metin toosearch hello.</span><span class="sxs-lookup"><span data-stu-id="86e86-808">`search=[string]` (optional) - hello text toosearch for.</span></span> <span data-ttu-id="86e86-809">Tüm `searchable` sürece alanları varsayılan olarak aranır `searchFields` belirtilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-809">All `searchable` fields are searched by default unless `searchFields` is specified.</span></span> <span data-ttu-id="86e86-810">Arama yaparken `searchable` alanları, hello arama metni kendisini simgeleştirilmiş, birden çok koşulları boşluk ile ayrılabilir şekilde (örneğin: `search=hello world`).</span><span class="sxs-lookup"><span data-stu-id="86e86-810">When searching `searchable` fields, hello search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span></span> <span data-ttu-id="86e86-811">Her terim toomatch kullanmak `*` (Boole filtresi sorgular için yararlı olabilir).</span><span class="sxs-lookup"><span data-stu-id="86e86-811">toomatch any term, use `*` (this can be useful for boolean filter queries).</span></span> <span data-ttu-id="86e86-812">Bu parametrenin atlanması sahip aynı efekt çok ayarı olarak hello`*`.</span><span class="sxs-lookup"><span data-stu-id="86e86-812">Omitting this parameter has hello same effect as setting it too`*`.</span></span> <span data-ttu-id="86e86-813">Bkz: [Basit Sorgu söz dizimi](https://msdn.microsoft.com/library/dn798920.aspx) hello arama söz dizimi üzerinde özellikleri için.</span><span class="sxs-lookup"><span data-stu-id="86e86-813">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on hello search syntax.</span></span>

* <span data-ttu-id="86e86-814">**Not**: hello sonuçları bazen olabilir şaşırtıcı üzerinden sorgulanırken `searchable` alanları.</span><span class="sxs-lookup"><span data-stu-id="86e86-814">**Note**: hello results can sometimes be surprising when querying over `searchable` fields.</span></span> <span data-ttu-id="86e86-815">Merhaba belirteç Oluşturucu mantığı toohandle durumlarda ortak tooEnglish metin kesme, virgül gibi sayılar, vb. içerir. Örneğin, `search=123,456` virgül İngilizce büyük sayılar için bin ayırıcı olarak kullanıldığından hello tek tek 123 ve terimleri 456, yerine tek bir terim 123,456 ile eşleşir.</span><span class="sxs-lookup"><span data-stu-id="86e86-815">hello tokenizer includes logic toohandle cases common tooEnglish text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than hello individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span></span> <span data-ttu-id="86e86-816">Bu nedenle, noktalama tooseparate koşullarını yerine boşluk hello kullanılmasını öneririz `search` parametresi.</span><span class="sxs-lookup"><span data-stu-id="86e86-816">For this reason, we recommend using white space rather than punctuation tooseparate terms in hello `search` parameter.</span></span>

<span data-ttu-id="86e86-817">`searchMode=any|all`(isteğe bağlı, çok varsayılanları`any`) - olup hello arama terimleri bir bölümünü veya tamamını sipariş toocount hello belgede bir eşleşme olarak eşlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-817">`searchMode=any|all` (optional, defaults too`any`) - whether any or all of hello search terms must be matched in order toocount hello document as a match.</span></span>

<span data-ttu-id="86e86-818">`searchFields=[string]`(isteğe bağlı) - hello için virgülle ayrılmış bir alan adları toosearch hello listesini Belirtilen metni.</span><span class="sxs-lookup"><span data-stu-id="86e86-818">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified text.</span></span> <span data-ttu-id="86e86-819">Hedef alan işaretli, olarak `searchable`.</span><span class="sxs-lookup"><span data-stu-id="86e86-819">Target fields must be marked as `searchable`.</span></span>

<span data-ttu-id="86e86-820">`queryType=simple|full`(isteğe bağlı, çok varsayılanları`simple`) - kümesi "Basit" çok arama metni simgelerini gibi sağlayan bir basit sorgu dili kullanarak değerlendirdiğinde +, * ve "".</span><span class="sxs-lookup"><span data-stu-id="86e86-820">`queryType=simple|full` (optional, defaults too`simple`) - when set too"simple" search text is interpreted using a simple query language that allows for symbols such as +, * and "".</span></span> <span data-ttu-id="86e86-821">Sorguları, tüm aranabilir alanları değerlendirilir (veya alanlarını belirtilen `searchFields`) varsayılan olarak her belgedeki.</span><span class="sxs-lookup"><span data-stu-id="86e86-821">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span></span> <span data-ttu-id="86e86-822">Merhaba sorgu türü ayarlandığında çok`full` arama metni alana özgü ve ağırlıklı aramaları sağlayan hello Lucene sorgu dili kullanarak yorumlanır.</span><span class="sxs-lookup"><span data-stu-id="86e86-822">When hello query type is set too`full` search text is interpreted using hello Lucene query language which allows field-specific and weighted searches.</span></span> <span data-ttu-id="86e86-823">Bkz: [Basit Sorgu söz dizimi](https://msdn.microsoft.com/library/dn798920.aspx) ve [Lucene sorgu söz dizimi](https://msdn.microsoft.com/library/mt589323.aspx) hello arama sözdizimleri üzerinde özellikleri için.</span><span class="sxs-lookup"><span data-stu-id="86e86-823">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on hello search syntaxes.</span></span> 

> [!NOTE]
> <span data-ttu-id="86e86-824">Merhaba Lucene sorgu dili benzer işlevselliği sunan $filter lehinde desteklenmiyor aramada aralığı.</span><span class="sxs-lookup"><span data-stu-id="86e86-824">Range search in hello Lucene query language is not supported in favor of $filter which offers similar functionality.</span></span>
> 
> 

<span data-ttu-id="86e86-825">`moreLikeThis=[key]`(isteğe bağlı) **Önemli:** bu özellik yalnızca kullanılabilir `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="86e86-825">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span></span> <span data-ttu-id="86e86-826">Bu seçenek hello metin arama parametre içeren bir sorguda kullanılamaz `search=[string]`.</span><span class="sxs-lookup"><span data-stu-id="86e86-826">This option cannot be used in a query that contains hello text search parameter, `search=[string]`.</span></span> <span data-ttu-id="86e86-827">Merhaba `moreLikeThis` parametresi hello belge anahtarı ile belirtilen benzer toohello belge olan belgeleri bulur.</span><span class="sxs-lookup"><span data-stu-id="86e86-827">hello `moreLikeThis` parameter finds documents that are similar toohello document specified by hello document key.</span></span> <span data-ttu-id="86e86-828">Ne zaman bir arama isteği yapıldığında ile `moreLikeThis`, arama terimleri listesini hello sıklığı ve rarity hello kaynak belgedeki koşulları temel alınarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="86e86-828">When a search request is made with `moreLikeThis`, a list of search terms is generated based on hello frequency and rarity of terms in hello source document.</span></span> <span data-ttu-id="86e86-829">Kullanılan toomake hello sonra isteği bu terimler.</span><span class="sxs-lookup"><span data-stu-id="86e86-829">Those terms are then used toomake hello request.</span></span> <span data-ttu-id="86e86-830">Varsayılan olarak, tüm içeriğini hello `searchable` sürece alanlar olarak kabul `searchFields` hangi alanları aranır kullanılan toorestrict değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-830">By default, hello contents of all `searchable` fields are considered unless `searchFields` is used toorestrict which fields are searched.</span></span>  

<span data-ttu-id="86e86-831">`$skip=#`(isteğe bağlı) - hello sayısı arama sonuçları tooskip; 100. 000 ' büyük olamaz.</span><span class="sxs-lookup"><span data-stu-id="86e86-831">`$skip=#` (optional) - hello number of search results tooskip; Cannot be greater than 100,000.</span></span> <span data-ttu-id="86e86-832">Dizisi tooscan belgelerde gerekiyor ancak kullanamazsınız `$skip` toothis sınırlaması nedeniyle kullanmayı `$orderby` tamamen sıralı anahtar ve `$filter` bir aralık sorgu yerine.</span><span class="sxs-lookup"><span data-stu-id="86e86-832">If you need tooscan documents in sequence but cannot use `$skip` due toothis limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-833">Çağrılırken **arama** POST kullanarak, bu parametre adlı `skip` yerine `$skip`.</span><span class="sxs-lookup"><span data-stu-id="86e86-833">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span></span>
> 
> 

<span data-ttu-id="86e86-834">`$top=#`(isteğe bağlı) - arama hello sayısı tooretrieve sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="86e86-834">`$top=#` (optional) - hello number of search results tooretrieve.</span></span> <span data-ttu-id="86e86-835">Bu ile birlikte kullanılabilir `$skip` tooimplement istemci-tarafı sayfalama arama sonuçları.</span><span class="sxs-lookup"><span data-stu-id="86e86-835">This can be used in conjunction with `$skip` tooimplement client-side paging of search results.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-836">Çağrılırken **arama** POST kullanarak, bu parametre adlı `top` yerine `$top`.</span><span class="sxs-lookup"><span data-stu-id="86e86-836">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="86e86-837">`$count=true|false`(isteğe bağlı, çok varsayılanları`false`)-toofetch sonuçları toplam hata sayısı hello olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="86e86-837">`$count=true|false` (optional, defaults too`false`) - Specifies whether toofetch hello total count of results.</span></span> <span data-ttu-id="86e86-838">Bu hello eşleşen tüm belgelerin hello sayısıdır `search` ve `$filter` yoksayılıyor parametreleri `$top` ve `$skip`.</span><span class="sxs-lookup"><span data-stu-id="86e86-838">This is hello count of all documents that match hello `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span></span> <span data-ttu-id="86e86-839">Bu değeri çok ayarı`true` bir performans etkisi olabilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-839">Setting this value too`true` may have a performance impact.</span></span> <span data-ttu-id="86e86-840">Döndürülen hello sayısı yaklaşık olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="86e86-840">Note that hello count returned is an approximation.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-841">Çağrılırken **arama** POST kullanarak, bu parametre adlı `count` yerine `$count`.</span><span class="sxs-lookup"><span data-stu-id="86e86-841">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span></span>
> 
> 

<span data-ttu-id="86e86-842">`$orderby=[string]`(isteğe bağlı) - virgülle ayrılmış ifadeler toosort hello sonuçlarına göre listesi.</span><span class="sxs-lookup"><span data-stu-id="86e86-842">`$orderby=[string]` (optional) - A list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="86e86-843">Her bir ifadenin bir alan adı veya bir çağrı toohello olabilir `geo.distance()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="86e86-843">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="86e86-844">Her deyim tarafından izlenebilir `asc` artan, tooindicated ve `desc` azalan tooindicate.</span><span class="sxs-lookup"><span data-stu-id="86e86-844">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="86e86-845">Merhaba varsayılan, artan.</span><span class="sxs-lookup"><span data-stu-id="86e86-845">hello default is ascending order.</span></span> <span data-ttu-id="86e86-846">TIES tarafından belgelerin hello eşleşmiyor puan ayrılmış olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-846">Ties will be broken by hello match scores of documents.</span></span> <span data-ttu-id="86e86-847">Öyle değilse `$orderby` belirtilirse, belge eşleşmiyor puan göre azalan hello varsayılan sıralama düzeni.</span><span class="sxs-lookup"><span data-stu-id="86e86-847">If no `$orderby` is specified, hello default sort order is descending by document match score.</span></span> <span data-ttu-id="86e86-848">Bir sınır için 32 yan `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="86e86-848">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-849">Çağrılırken **arama** POST kullanarak, bu parametre adlı `orderby` yerine `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="86e86-849">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="86e86-850">`$select=[string]`(isteğe bağlı) - virgülle ayrılmış alanlar tooretrieve listesi.</span><span class="sxs-lookup"><span data-stu-id="86e86-850">`$select=[string]` (optional) - A list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="86e86-851">Belirtilmezse, hello şemasında alınabilir olarak işaretlenmiş tüm alanlar dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-851">If unspecified, all fields marked as retrievable in hello schema are included.</span></span> <span data-ttu-id="86e86-852">Bu parametre çok ayarlayarak da açıkça tüm alanlar isteyebilir`*`.</span><span class="sxs-lookup"><span data-stu-id="86e86-852">You can also explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-853">Çağrılırken **arama** POST kullanarak, bu parametre adlı `select` yerine `$select`.</span><span class="sxs-lookup"><span data-stu-id="86e86-853">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="86e86-854">`facet=[string]`(sıfır veya daha fazla) - bir alan toofacet tarafından.</span><span class="sxs-lookup"><span data-stu-id="86e86-854">`facet=[string]` (zero or more) - A field toofacet by.</span></span> <span data-ttu-id="86e86-855">Merhaba dizesi parametreleri toocustomize hello olduğunu virgülle ayrılmış olarak ifade edilen isteğe bağlı olarak içerebilir `name:value` çiftleri.</span><span class="sxs-lookup"><span data-stu-id="86e86-855">Optionally hello string may contain parameters toocustomize hello faceting expressed as comma-separated `name:value` pairs.</span></span> <span data-ttu-id="86e86-856">Geçerli Parametreler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="86e86-856">Valid parameters are:</span></span>

* <span data-ttu-id="86e86-857">`count`(en fazla sayıda modeli şartı; varsayılan değer 10).</span><span class="sxs-lookup"><span data-stu-id="86e86-857">`count` (max number of facet terms; default is 10).</span></span> <span data-ttu-id="86e86-858">Maksimum yok yoktur, ancak özellikle çok sayıda benzersiz koşulları hello modellenmiş alan içeriyorsa, daha yüksek değerleri karşılık gelen bir performans cezasına sebep.</span><span class="sxs-lookup"><span data-stu-id="86e86-858">There is no maximum, but higher values incur a corresponding performance penalty, especially if hello faceted field contains a large number of unique terms.</span></span>
  * <span data-ttu-id="86e86-859">Örneğin: `facet=category,count:5` hello modeli sonuçlarında iyi beş kategorileri alır.</span><span class="sxs-lookup"><span data-stu-id="86e86-859">For example: `facet=category,count:5` gets hello top five categories in facet results.</span></span>  
  * <span data-ttu-id="86e86-860">**Not**: hello varsa `count` parametre benzersiz koşulları hello sayısından daha az ve hello sonuçları doğru olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-860">**Note**: If hello `count` parameter is less than hello number of unique terms, hello results may not be accurate.</span></span> <span data-ttu-id="86e86-861">Son olduğunu sorgular parça dağıtılan toohello yolu budur.</span><span class="sxs-lookup"><span data-stu-id="86e86-861">This is due toohello way faceting queries are distributed across shards.</span></span> <span data-ttu-id="86e86-862">Artan `count` genellikle artar doğruluğu hello terim sayıları, ancak performans maliyeti hello.</span><span class="sxs-lookup"><span data-stu-id="86e86-862">Increasing `count` generally increases hello accuracy of hello term counts, but at a performance cost.</span></span>
* <span data-ttu-id="86e86-863">`sort`(birini `count` toosort *azalan* sayıma göre `-count` toosort *artan* sayıma göre `value` toosort *artan* değer veya `-value` toosort *azalan* değeriyle)</span><span class="sxs-lookup"><span data-stu-id="86e86-863">`sort` (one of `count` toosort *descending* by count, `-count` toosort *ascending* by count, `value` toosort *ascending* by value, or `-value` toosort *descending* by value)</span></span>
  * <span data-ttu-id="86e86-864">Örneğin: `facet=category,count:3,sort:count` alır, her şehir adı belgelerle hello sayısına göre azalan sırada modeli sonuçlarında üst üç kategoride hello.</span><span class="sxs-lookup"><span data-stu-id="86e86-864">For example: `facet=category,count:3,sort:count` gets hello top three categories in facet results in descending order by hello number of documents with each city name.</span></span> <span data-ttu-id="86e86-865">Örneğin, bütçe, Motel ve lüks, hello üst üç kategorileri şunlardır ve bütçe 5 isabet, 6 Motel sahip ve lüks 4 varsa, ardından hello demet hello sırayla olacaktır Motel, bütçe, lüks.</span><span class="sxs-lookup"><span data-stu-id="86e86-865">For example, if hello top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then hello buckets will be in hello order Motel, Budget, Luxury.</span></span>
  * <span data-ttu-id="86e86-866">Örneğin: `facet=rating,sort:-value` değerine göre azalan sırada tüm olası derecelendirmeler aralıklarını üretir.</span><span class="sxs-lookup"><span data-stu-id="86e86-866">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span></span> <span data-ttu-id="86e86-867">Merhaba derecelendirmeleri 1 too5 varsa, örneğin, hello demet sıralanır 5, 4, 3, 2, kaç tane belgeleri her derecelendirme eşleşen yedeklemiş 1.</span><span class="sxs-lookup"><span data-stu-id="86e86-867">For example, if hello ratings are from 1 too5, hello buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span></span>
* <span data-ttu-id="86e86-868">`values`(kanal ayrılmış sayısal veya `Edm.DateTimeOffset` değerleri model girdi değerleri dinamik bir dizi belirtme)</span><span class="sxs-lookup"><span data-stu-id="86e86-868">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span></span>
  * <span data-ttu-id="86e86-869">Örneğin: `facet=baseRate,values:10|20` üç demet oluşturur: biri temel oranını 0 toobut 10, 10 toobut 20 ve 20 veya daha yüksek bir dahil değil yedeklemek için bir tane dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="86e86-869">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up toobut not including 10, one for 10 up toobut not including 20, and one for 20 or higher.</span></span>
  * <span data-ttu-id="86e86-870">Örneğin: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` iki demet oluşturur: biri Şubat 2010'dan önce renovated Oteller ve Otel için bir renovated Şubat 2010 veya üzeri 1.</span><span class="sxs-lookup"><span data-stu-id="86e86-870">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span></span>
* <span data-ttu-id="86e86-871">`interval`(sayı, 0'dan büyük tamsayı aralığı veya `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` tarih saat değerleri için)</span><span class="sxs-lookup"><span data-stu-id="86e86-871">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span></span>
  * <span data-ttu-id="86e86-872">Örneğin: `facet=baseRate,interval:100` demet boyutu 100 temel oranı aralıklarını temel alarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="86e86-872">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span></span> <span data-ttu-id="86e86-873">Örneğin, temel oranları tüm $60 ve $600 arasında varsa, olacaktır 0-100, 100-200, 200-300, 400 300, 400-500 ve 500-600 aralıklarını.</span><span class="sxs-lookup"><span data-stu-id="86e86-873">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span></span>
  * <span data-ttu-id="86e86-874">Örneğin: `facet=lastRenovationDate,interval:year` bir demet zaman Oteller renovated her yıl üretir.</span><span class="sxs-lookup"><span data-stu-id="86e86-874">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span></span>
* <span data-ttu-id="86e86-875">`timeoffset`([+-] hh: mm, [+-] ssdd, veya [+-] hh) `timeoffset` isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span></span> <span data-ttu-id="86e86-876">Yalnızca hello ile birleştirilebilir `interval` seçeneği ve yalnızca türünde uygulanan tooa alan `Edm.DateTimeOffset`.</span><span class="sxs-lookup"><span data-stu-id="86e86-876">It can only be combined with hello `interval` option, and only when applied tooa field of type `Edm.DateTimeOffset`.</span></span> <span data-ttu-id="86e86-877">Merhaba değeri, zaman sınırları ayarı hello UTC saati için uzaklık tooaccount belirtir.</span><span class="sxs-lookup"><span data-stu-id="86e86-877">hello value specifies hello UTC time offset tooaccount for in setting time boundaries.</span></span>
  * <span data-ttu-id="86e86-878">Örneğin: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` kullandığı hello 01:00:00 UTC (Merhaba hedef saat diliminde gece yarısı) başlar günlük sınır</span><span class="sxs-lookup"><span data-stu-id="86e86-878">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses hello day boundary that starts at 01:00:00 UTC (midnight in hello target time zone)</span></span>
* <span data-ttu-id="86e86-879">**Not**: `count` ve `sort` hello aynı birleştirilebilir ile modeli belirtimi, ancak bunlar ilişkilendirilemez `interval` veya `values`, ve `interval` ve `values` birlikte birleştirilemez.</span><span class="sxs-lookup"><span data-stu-id="86e86-879">**Note**: `count` and `sort` can be combined in hello same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span></span>
* <span data-ttu-id="86e86-880">**Not**: tarih saat aralığı nedeni modellerinin hesaplanan UTC saat tabanlı `timeoffset` belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="86e86-880">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span></span> <span data-ttu-id="86e86-881">Örneğin: için `facet=lastRenovationDate,interval:day`, hello günlük sınır 00:00:00 UTC başlatır.</span><span class="sxs-lookup"><span data-stu-id="86e86-881">For example: for `facet=lastRenovationDate,interval:day`, hello day boundary starts at 00:00:00 UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="86e86-882">Çağrılırken **arama** POST kullanarak, bu parametre adlı `facets` yerine `facet`.</span><span class="sxs-lookup"><span data-stu-id="86e86-882">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span></span> <span data-ttu-id="86e86-883">Ayrıca, bunu burada her ayrı modeli ifade dizesidir dizeleri bir JSON dizisi olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="86e86-883">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span></span>
> 
> 

<span data-ttu-id="86e86-884">`$filter=[string]`(isteğe bağlı) - standart OData sözdiziminde yapılandırılmış arama ifadesi.</span><span class="sxs-lookup"><span data-stu-id="86e86-884">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-885">Çağrılırken **arama** POST kullanarak, bu parametre adlı `filter` yerine `$filter`.</span><span class="sxs-lookup"><span data-stu-id="86e86-885">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="86e86-886">`highlight=[string]`(isteğe bağlı) - virgülle ayrılmış bir alan adları isabet için kullanılan bir dizi vurgular.</span><span class="sxs-lookup"><span data-stu-id="86e86-886">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span></span> <span data-ttu-id="86e86-887">Yalnızca `searchable` alanları isabet vurgulama için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-887">Only `searchable` fields can be used for hit highlighting.</span></span>

<span data-ttu-id="86e86-888">`highlightPreTag=[string]`(isteğe bağlı, çok varsayılanları`<em>`) - bir dize toohit vurgular başına etiketi.</span><span class="sxs-lookup"><span data-stu-id="86e86-888">`highlightPreTag=[string]` (optional, defaults too`<em>`) - A string tag that prepends toohit highlights.</span></span> <span data-ttu-id="86e86-889">İle ayarlanmalıdır `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="86e86-889">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-890">Çağrılırken **arama** GET kullanarak, ayrılmış karakter hello URL (örneğin, % &#23; yerine) yüzde olarak kodlanmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-890">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="86e86-891">`highlightPostTag=[string]`(isteğe bağlı, çok varsayılanları`</em>`)-toohit vurgular ekler bir dize etiketi.</span><span class="sxs-lookup"><span data-stu-id="86e86-891">`highlightPostTag=[string]` (optional, defaults too`</em>`) - a string tag that appends toohit highlights.</span></span> <span data-ttu-id="86e86-892">İle ayarlanmalıdır `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="86e86-892">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-893">Çağrılırken **arama** GET kullanarak, ayrılmış karakter hello URL (örneğin, % &#23; yerine) yüzde olarak kodlanmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-893">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="86e86-894">`scoringProfile=[string]`(isteğe bağlı) - hello Puanlama profili tooevaluate adıyla aynı düzeni toosort hello sonuçları eşleşen belgelerde puanlarını.</span><span class="sxs-lookup"><span data-stu-id="86e86-894">`scoringProfile=[string]` (optional) - hello name of a scoring profile tooevaluate match scores for matching documents in order toosort hello results.</span></span>

<span data-ttu-id="86e86-895">`scoringParameter=[string]`(sıfır veya daha fazla) - bir Puanlama işlevi tanımlanan her parametre için hello değerleri gösterir (örneğin, `referencePointParameter`) hello biçimini kullanarak `name-value1,value2,...`.</span><span class="sxs-lookup"><span data-stu-id="86e86-895">`scoringParameter=[string]` (zero or more) - Indicates hello values for each parameter defined in a scoring function (for example, `referencePointParameter`) using hello format `name-value1,value2,...`.</span></span>

* <span data-ttu-id="86e86-896">Örneğin, hello profil Puanlama işlevi ile tanımlıyorsa "mylocation" Merhaba sorgu dizesi seçeneği adlı bir parametre olması `&scoringParameter=mylocation--122.2,44.8`.</span><span class="sxs-lookup"><span data-stu-id="86e86-896">For example, if hello scoring profile defines a function with a parameter called "mylocation" hello query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span></span> <span data-ttu-id="86e86-897">Merhaba ikinci tire hello ilk değer (Bu örnekte boylam) bir parçası olsa hello ilk tire hello adını hello değer listesinden ayırır.</span><span class="sxs-lookup"><span data-stu-id="86e86-897">hello first dash separates hello name from hello value list, while hello second dash is part of hello first value (longitude in this example).</span></span>
* <span data-ttu-id="86e86-898">Puanlama parametrelerini etiketi, artırmanın virgüller, içerebilir gibi tek tırnak kullanılarak hello listedeki tür değerleri kaçış.</span><span class="sxs-lookup"><span data-stu-id="86e86-898">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in hello list using single quotes.</span></span> <span data-ttu-id="86e86-899">Merhaba değer kendilerini tek tırnak içermiyorsa, katlama tarafından kaçış</span><span class="sxs-lookup"><span data-stu-id="86e86-899">If hello values themselves contain single quotes, you can escape them by doubling.</span></span>
  * <span data-ttu-id="86e86-900">Örneğin, "Hello, O'Brien" ve "Smith", hello sorgu "mytag" adlı bir parametreye artırmanın bir etiketi varsa ve hello etiketinde tooboost istediğiniz değerleri dize seçenek olacaktır `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span><span class="sxs-lookup"><span data-stu-id="86e86-900">For example, if you have a tag boosting parameter called "mytag" and you want tooboost on hello tag values "Hello, O'Brien" and "Smith", hello query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span></span> <span data-ttu-id="86e86-901">Tırnak işaretleri yalnızca olduğuna dikkat edin virgül içeren değerler için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-901">Note that quotes are only required for values that contain commas.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-902">Çağrılırken **arama** POST kullanarak, bu parametre adlı `scoringParameters` yerine `scoringParameter`.</span><span class="sxs-lookup"><span data-stu-id="86e86-902">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span></span> <span data-ttu-id="86e86-903">Bir JSON dizisini ayrı bir olduğu her bir dize belirttiğiniz ayrıca `name-values` çifti.</span><span class="sxs-lookup"><span data-stu-id="86e86-903">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span></span>
> 
> 

<span data-ttu-id="86e86-904">`minimumCoverage`(isteğe bağlı, varsayılan olarak too100) - 0 ile Merhaba sorgu toobe sırada bir arama sorgusu tarafından ele alınması gereken hello dizin hello yüzdesini gösteren 100 arasında bir sayı başarı bildirdi.</span><span class="sxs-lookup"><span data-stu-id="86e86-904">`minimumCoverage` (optional, defaults too100) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a search query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="86e86-905">Varsayılan olarak, tüm dizin hello kullanılabilir olmalıdır veya `Search` 503 HTTP durum kodunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="86e86-905">By default, hello entire index must be available or `Search` will return HTTP status code 503.</span></span> <span data-ttu-id="86e86-906">Ayarlarsanız `minimumCoverage` ve `Search` başarılı, HTTP 200 dönün ve içeren bir `@search.coverage` hello yanıt hello sorguda eklenmiştir hello dizin hello yüzdesini belirten değer.</span><span class="sxs-lookup"><span data-stu-id="86e86-906">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-907">Bu parametre tooa değerin 100 Hizmetleri ile yalnızca bir çoğaltma için bile arama kullanılabilirlik sağlamak için yararlı olabilir. daha düşük ayarlanması.</span><span class="sxs-lookup"><span data-stu-id="86e86-907">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="86e86-908">Ancak, tüm eşleşen belgeleri toobe hello arama sonuçlarında mevcut sağlanır.</span><span class="sxs-lookup"><span data-stu-id="86e86-908">However, not all matching documents are guaranteed toobe present in hello search results.</span></span> <span data-ttu-id="86e86-909">Arama geri çağırma olduğu daha önemli tooyour uygulamadan kullanılabilirlik daha sonra en iyi tooleave olan `minimumCoverage` zaman, varsayılan değer 100.</span><span class="sxs-lookup"><span data-stu-id="86e86-909">If search recall is more important tooyour application than availability, then it's best tooleave `minimumCoverage` at its default value of 100.</span></span>
> 
> 

<span data-ttu-id="86e86-910">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="86e86-910">`api-version=[string]` (required).</span></span> <span data-ttu-id="86e86-911">Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="86e86-911">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="86e86-912">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="86e86-912">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="86e86-913">Not: Bu işlem için hello `api-version` olup, çağrı bağımsız olarak hello URL'deki sorgu parametresi olarak belirtilen **arama** GET veya POST ile.</span><span class="sxs-lookup"><span data-stu-id="86e86-913">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Search** with GET or POST.</span></span>

<span data-ttu-id="86e86-914">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="86e86-914">**Request Headers**</span></span>

<span data-ttu-id="86e86-915">liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.</span><span class="sxs-lookup"><span data-stu-id="86e86-915">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="86e86-916">`api-key`: Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-916">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="86e86-917">Bir dize değeri, benzersiz tooyour hizmeti URL'si değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-917">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="86e86-918">Merhaba **arama** isteği, bir yönetici anahtarını veya sorgu anahtarı belirtebilirsiniz `api-key`.</span><span class="sxs-lookup"><span data-stu-id="86e86-918">hello **Search** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="86e86-919">Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-919">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="86e86-920">Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan.</span><span class="sxs-lookup"><span data-stu-id="86e86-920">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="86e86-921">Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="86e86-921">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="86e86-922">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="86e86-922">**Request Body**</span></span>

<span data-ttu-id="86e86-923">GET için: yok.</span><span class="sxs-lookup"><span data-stu-id="86e86-923">For GET: None.</span></span>

<span data-ttu-id="86e86-924">POST için:</span><span class="sxs-lookup"><span data-stu-id="86e86-924">For POST:</span></span>

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

<span data-ttu-id="86e86-925">**Kısmi arama yanıtları devamlılığı**</span><span class="sxs-lookup"><span data-stu-id="86e86-925">**Continuation of Partial Search Responses**</span></span>

<span data-ttu-id="86e86-926">Bazen Azure Search tüm tek bir arama yanıt istenen sonuçları hello döndüremez.</span><span class="sxs-lookup"><span data-stu-id="86e86-926">Sometimes Azure Search can't return all hello requested results in a single Search response.</span></span> <span data-ttu-id="86e86-927">Bu durum hello sorgu çok fazla belgeleri değil belirterek isteğinde bulunduğunda gibi farklı nedenlerle oluşabilir `$top` veya için bir değer belirterek `$top` , çok büyük.</span><span class="sxs-lookup"><span data-stu-id="86e86-927">This can happen for different reasons, such as when hello query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span></span> <span data-ttu-id="86e86-928">Böyle durumlarda, Azure Search hello içerecektir `@odata.nextLink` hello yanıt gövdesi içinde ek açıklama ve ayrıca `@search.nextPageParameters` bir POST isteği ise.</span><span class="sxs-lookup"><span data-stu-id="86e86-928">In such cases, Azure Search will include hello `@odata.nextLink` annotation in hello response body, and also `@search.nextPageParameters` if it was a POST request.</span></span> <span data-ttu-id="86e86-929">Bu ek açıklamaları tooformulate hello değerlerini başka bir arama isteği tooget hello sonraki bölümü hello arama yanıtı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86e86-929">You can use hello values of these annotations tooformulate another Search request tooget hello next part of hello search response.</span></span> <span data-ttu-id="86e86-930">Bu adlı bir ***devamlılık*** hello özgün arama isteği ve hello ek açıklamaları genellikle denir ***devamlılık belirteçleri***.</span><span class="sxs-lookup"><span data-stu-id="86e86-930">This is called a ***continuation*** of hello original Search request, and hello annotations are generally called ***continuation tokens***.</span></span> <span data-ttu-id="86e86-931">Bkz: [aşağıdaki hello örnek](#SearchResponse) hello sözdizimi, bu ek açıklamaların ve hello yanıt gövdesi içinde nerede göründüklerinden hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="86e86-931">See [hello example below](#SearchResponse) for details on hello syntax of these annotations and where they appear in hello response body.</span></span> 

<span data-ttu-id="86e86-932">Azure Search devamlılık belirteçleri neden döndürebilir hello uygulamaya özel ve konu toochange nedenleridir.</span><span class="sxs-lookup"><span data-stu-id="86e86-932">hello reasons why Azure Search might return continuation tokens are implementation-specific and subject toochange.</span></span> <span data-ttu-id="86e86-933">Sağlam istemcileri her zaman burada beklenenden daha az belgeler döndürülür ve devamlılık belirteci belgelerini almak dahil toocontinue hazır toohandle durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-933">Robust clients should always be ready toohandle cases where fewer documents than expected are returned and a continuation token is included toocontinue retrieving documents.</span></span> <span data-ttu-id="86e86-934">Ayrıca aynı HTTP yöntemi sipariş toocontinue özgün isteğinde hello olarak hello kullanmanız gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="86e86-934">Also note that you must use hello same HTTP method as hello original request in order toocontinue.</span></span> <span data-ttu-id="86e86-935">Bir GET isteği gönderirse, örneğin, gönderdiğiniz herhangi bir devamlılık isteğini de GET kullanmanız gerekir (ve sonrası için benzer şekilde).</span><span class="sxs-lookup"><span data-stu-id="86e86-935">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span></span>

<span data-ttu-id="86e86-936"><a name="SearchResponse"></a>
**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="86e86-936"><a name="SearchResponse"></a>
**Response**</span></span>

<span data-ttu-id="86e86-937">Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.</span><span class="sxs-lookup"><span data-stu-id="86e86-937">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

<span data-ttu-id="86e86-938">**Örnekler:**</span><span class="sxs-lookup"><span data-stu-id="86e86-938">**Examples:**</span></span>

<span data-ttu-id="86e86-939">Ek örnekler üzerinde hello bulabilirsiniz [OData ifade sözdizimini Azure arama için](https://msdn.microsoft.com/library/azure/dn798921.aspx) sayfası.</span><span class="sxs-lookup"><span data-stu-id="86e86-939">You can find additional examples on hello [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span></span>

1)    <span data-ttu-id="86e86-940">Arama hello dizin tarihe göre azalan sırada sıralanır.</span><span class="sxs-lookup"><span data-stu-id="86e86-940">Search hello Index sorted descending by date.</span></span>

    <span data-ttu-id="86e86-941">GET /indexes/hotels/docs? arama = * & $orderby lastRenovationDate desc & api-version = 2015-02-28-Önizleme =</span><span class="sxs-lookup"><span data-stu-id="86e86-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="86e86-942">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "*", "orderby": "lastRenovationDate desc"}</span><span class="sxs-lookup"><span data-stu-id="86e86-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span></span>

2)    <span data-ttu-id="86e86-943">Modellenmiş bir arama hello dizinini aramak ve modelleri için kategoriler, derecelendirme, etiketleri yanı sıra belirli aralıklara baseRate öğeleriyle almak:</span><span class="sxs-lookup"><span data-stu-id="86e86-943">In a faceted search, search hello index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span></span>

    <span data-ttu-id="86e86-944">GET /indexes/hotels/docs? arama = test & modeli = kategori & modeli = derecelendirme & modeli etiketleri & modeli = baseRate, değerleri: 80 = | 150 | 220 & API sürümü 2015-02-28-Önizleme =</span><span class="sxs-lookup"><span data-stu-id="86e86-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="86e86-945">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "test", "modelleri": ["kategorisi", "Derecelendirme", "etiketler", "baseRate, değerleri: 80 | 150 | 220"]}</span><span class="sxs-lookup"><span data-stu-id="86e86-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span></span>

3)    <span data-ttu-id="86e86-946">Bir filtre kullanarak daraltmak hello önceki modellenmiş sorgu sonuçları üzerinde hello kullanıcı tıklattıktan sonra 3 ve kategori "Motel" derecelendirme:</span><span class="sxs-lookup"><span data-stu-id="86e86-946">Using a filter, narrow down hello previous faceted query results after hello user clicks on rating 3 and category "Motel":</span></span>

    <span data-ttu-id="86e86-947">GET /indexes/hotels/docs? arama = test & modeli etiketleri & modeli = baseRate, değerleri: 80 = | 150 | 220 & $filter & derecelendirme eq 3 ve kategori eq 'Motel' api-version = 2015-02-28-Önizleme =</span><span class="sxs-lookup"><span data-stu-id="86e86-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="86e86-948">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "test", "modelleri": ["etiketleri", "baseRate, değerleri: 80 | 150 | 220"], "filtre": "Derecelendirme eq 3 ve kategori eq 'Motel'"}</span><span class="sxs-lookup"><span data-stu-id="86e86-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span></span>

4) <span data-ttu-id="86e86-949">Modellenmiş bir aramada bir sorgudan döndürülen benzersiz koşulları bir üst sınır ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="86e86-949">In a faceted search, set an upper limit on unique terms returned in a query.</span></span> <span data-ttu-id="86e86-950">Merhaba varsayılan değer 10 ancak artırabilir ya da hello kullanarak bu değeri azaltmak `count` hello parametresini `facet` özniteliği:</span><span class="sxs-lookup"><span data-stu-id="86e86-950">hello default is 10, but you can increase or decrease this value using hello `count` parameter on hello `facet` attribute:</span></span>

    <span data-ttu-id="86e86-951">GET /indexes/hotels/docs? arama = test & modeli Şehir, sayısı: 5 & api-version = 2015-02-28-Önizleme =</span><span class="sxs-lookup"><span data-stu-id="86e86-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="86e86-952">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "test", "modelleri": ["Şehir, sayısı: 5"]}</span><span class="sxs-lookup"><span data-stu-id="86e86-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span></span>

5)    <span data-ttu-id="86e86-953">Belirli alanları içinde arama hello dizin; Dile özgü alanı:</span><span class="sxs-lookup"><span data-stu-id="86e86-953">Search hello Index within specific fields; For example, a language-specific field:</span></span>

    <span data-ttu-id="86e86-954">GET /indexes/hotels/docs? arama hôtel & searchFields = description_fr & api-version = 2015-02-28-Önizleme =</span><span class="sxs-lookup"><span data-stu-id="86e86-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="86e86-955">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "hôtel", "searchFields": "description_fr"}</span><span class="sxs-lookup"><span data-stu-id="86e86-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span></span>

6) <span data-ttu-id="86e86-956">Birden çok alan arasında arama başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="86e86-956">Search hello Index across multiple fields.</span></span> <span data-ttu-id="86e86-957">Örneğin, depolayabileceğiniz ve tüm içinde birden fazla dilde sorgu aranabilir alanları aynı dizin hello.</span><span class="sxs-lookup"><span data-stu-id="86e86-957">For example, you can store and query searchable fields in multiple languages, all within hello same index.</span></span>  <span data-ttu-id="86e86-958">İngilizce ve Fransızca açıklamaları hello aynı birlikte varsa belge, sorgu sonuçları tüm içinde hello döndürebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="86e86-958">If English and French descriptions co-exist in hello same document, you can return any or all in hello query results:</span></span>

    <span data-ttu-id="86e86-959">GET /indexes/hotels/docs? arama otel & searchFields = açıklama, description_fr & api-version = 2015-02-28-Önizleme =</span><span class="sxs-lookup"><span data-stu-id="86e86-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="86e86-960">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "otel", "searchFields": "açıklama, description_fr"}</span><span class="sxs-lookup"><span data-stu-id="86e86-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span></span>

<span data-ttu-id="86e86-961">Aynı anda yalnızca bir dizin sorgulanabilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="86e86-961">Note that you can only query one index at a time.</span></span> <span data-ttu-id="86e86-962">Aynı anda tooquery bir planlamıyorsanız her dil için birden çok dizin oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="86e86-962">Do not create multiple indexes for each language unless you plan tooquery one at a time.</span></span>

7)    <span data-ttu-id="86e86-963">Disk belleği - Get hello 1 öğe sayfasının (sayfa boyutu Dur 10):</span><span class="sxs-lookup"><span data-stu-id="86e86-963">Paging - Get hello 1st page of items (page size is 10):</span></span>

    <span data-ttu-id="86e86-964">GET /indexes/hotels/docs? arama = * & $skip = 0 & $top = 10 & api-version = 2015-02-28-Önizleme</span><span class="sxs-lookup"><span data-stu-id="86e86-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="86e86-965">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "*", "Atla": 0, "üst": 10}</span><span class="sxs-lookup"><span data-stu-id="86e86-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span></span>

8)    <span data-ttu-id="86e86-966">Disk belleği - Get hello 2 öğe sayfasının (sayfa boyutu Dur 10):</span><span class="sxs-lookup"><span data-stu-id="86e86-966">Paging - Get hello 2nd page of items (page size is 10):</span></span>

    <span data-ttu-id="86e86-967">GET /indexes/hotels/docs? arama = * & $skip = 10 & $top = 10 & api-version = 2015-02-28-Önizleme</span><span class="sxs-lookup"><span data-stu-id="86e86-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="86e86-968">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "*", "Atla": "üst" 10: 10}</span><span class="sxs-lookup"><span data-stu-id="86e86-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span></span>

9)    <span data-ttu-id="86e86-969">Belirli bir alan kümesi Al:</span><span class="sxs-lookup"><span data-stu-id="86e86-969">Retrieve a specific set of fields:</span></span>

    <span data-ttu-id="86e86-970">GET /indexes/hotels/docs? arama = * & $select hotelName, açıklama ve api-version = 2015-02-28-Önizleme =</span><span class="sxs-lookup"><span data-stu-id="86e86-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="86e86-971">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "*", "Seç": "hotelName, açıklaması"}</span><span class="sxs-lookup"><span data-stu-id="86e86-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span></span>

10)  <span data-ttu-id="86e86-972">Bir özel filtre ifadesi eşleşen belgeler Al:</span><span class="sxs-lookup"><span data-stu-id="86e86-972">Retrieve documents matching a specific filter expression:</span></span>

    <span data-ttu-id="86e86-973">GET /indexes/hotels/docs? $filter = (baseRate ge 60 ve baseRate lt 300) veya hotelName eq 'Süslü kalmak' & api-version = 2015-02-28-Önizleme</span><span class="sxs-lookup"><span data-stu-id="86e86-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="86e86-974">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"filtre": "(baseRate ge 60 ve baseRate lt 300) veya hotelName eq 'Süslü Kal'"}</span><span class="sxs-lookup"><span data-stu-id="86e86-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span></span>

11) <span data-ttu-id="86e86-975">Arama başlangıç dizini ve isabet vurgular dönüş parçaları</span><span class="sxs-lookup"><span data-stu-id="86e86-975">Search hello index and return fragments with hit highlights</span></span>

    <span data-ttu-id="86e86-976">GET /indexes/hotels/docs? arama bir şey = & vurgulayın açıklama & api-version = 2015-02-28-Önizleme =</span><span class="sxs-lookup"><span data-stu-id="86e86-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="86e86-977">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "bir şey", "highlight": "Açıklama"}</span><span class="sxs-lookup"><span data-stu-id="86e86-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span></span>

12) <span data-ttu-id="86e86-978">Arama başlangıç dizini ve bir başvuru konumu çıktığınızda daha yakından toofarther gelen sıralanmış dönüş belgeleri</span><span class="sxs-lookup"><span data-stu-id="86e86-978">Search hello index and return documents sorted from closer toofarther away from a reference location</span></span>

    <span data-ttu-id="86e86-979">GET /indexes/hotels/docs? arama bir şey = & $orderby=geo.distance (konum, geography'POINT(-122.12315 47.88121)') & api-version = 2015-02-28-Önizleme</span><span class="sxs-lookup"><span data-stu-id="86e86-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="86e86-980">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "bir şey", "orderby": "geo.distance (konum, geography'POINT(-122.12315 47.88121)')"}</span><span class="sxs-lookup"><span data-stu-id="86e86-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span></span>

13) <span data-ttu-id="86e86-981">Dizin hello arama olmadığı varsayılarak "coğrafi" adlı bir Puanlama profili ile iki uzaklık Puanlama işlevleri, bir parametre tanımlama "currentLocation" ve "lastLocation" adlı bir parametreyi tanımlayan bir adlı</span><span class="sxs-lookup"><span data-stu-id="86e86-981">Search hello index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span></span>

    <span data-ttu-id="86e86-982">GET /indexes/hotels/docs? arama bir şey = & scoringProfile = coğrafi & scoringParameter currentLocation--122.123,44.77233 & scoringParameter = lastLocation--121.499,44.2113 & api-version = 2015-02-28-Önizleme =</span><span class="sxs-lookup"><span data-stu-id="86e86-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="86e86-983">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "bir şey", "scoringProfile": "coğrafi", "scoringParameters": ["currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113"]}</span><span class="sxs-lookup"><span data-stu-id="86e86-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span></span>

14) <span data-ttu-id="86e86-984">Dizin hello kullanarak bulmanın [Basit Sorgu söz dizimi](https://msdn.microsoft.com/library/dn798920.aspx).</span><span class="sxs-lookup"><span data-stu-id="86e86-984">Find documents in hello index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span></span> <span data-ttu-id="86e86-985">Bu sorgu burada hello koşulları "rahatlık" ve "Konum" ancak değil "motel" aranabilir alanları içeren Oteller döndürür:</span><span class="sxs-lookup"><span data-stu-id="86e86-985">This query returns hotels where searchable fields contain hello terms "comfort" and "location" but not "motel":</span></span>

    <span data-ttu-id="86e86-986">GET /indexes/hotels/docs? arama = rahatlık + konumu-motel & searchMode = all & api-version = 2015-02-28-Önizleme</span><span class="sxs-lookup"><span data-stu-id="86e86-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="86e86-987">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "rahatlık + konumu-motel", "searchMode": "tümü"}</span><span class="sxs-lookup"><span data-stu-id="86e86-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span></span>

<span data-ttu-id="86e86-988">Not hello `searchMode=all` üstünde.</span><span class="sxs-lookup"><span data-stu-id="86e86-988">Note hello use of `searchMode=all` above.</span></span> <span data-ttu-id="86e86-989">Bu parametreyi dahil olmak üzere hello varsayılan değerini geçersiz kılar `searchMode=any`, sağlama, `-motel` "Ve değil" yerine "Veya değil" anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="86e86-989">Including this parameter overrides hello default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span></span> <span data-ttu-id="86e86-990">Olmadan `searchMode=all`"Veya, arama sonuçları kısıtlayan yerine genişletir değil" alın ve bu counter-intuitive toosome kullanıcılar olabilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-990">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive toosome users.</span></span>

15) <span data-ttu-id="86e86-991">Dizin hello kullanarak bulmanın [lucene sorgu söz dizimi](https://msdn.microsoft.com/library/mt589323.aspx).</span><span class="sxs-lookup"><span data-stu-id="86e86-991">Find documents in hello index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span></span> <span data-ttu-id="86e86-992">Bu sorgu hello terimi "Bütçe" ve "son renovated" Merhaba ifadesini içeren tüm aranabilir alanları hello kategori alanı, içerdiği Oteller döndürür.</span><span class="sxs-lookup"><span data-stu-id="86e86-992">This query returns hotels where hello category field contains hello term "budget" and all searchable fields containing hello phrase "recently renovated".</span></span> <span data-ttu-id="86e86-993">"En son renovated" Merhaba tümcecik içeren belgeleri yüksek hello terim artırma değeri (3) sonucunda derecelendirilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-993">Documents containing hello phrase "recently renovated" are ranked higher as a result of hello term boost value (3)</span></span>

    <span data-ttu-id="86e86-994">GET /indexes/hotels/docs? arama Kategori: Bütçe = ve \"son renovated\"^ 3 & searchMode = all & api-version = 2015-02-28-Önizleme & querytype tam =</span><span class="sxs-lookup"><span data-stu-id="86e86-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span></span>

    <span data-ttu-id="86e86-995">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "Kategori: Bütçe ve \"son renovated\"^ 3", "queryType": "tam", "searchMode": "tümü"}</span><span class="sxs-lookup"><span data-stu-id="86e86-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span></span>

<a name="LookupAPI"></a>

## <a name="lookup-document"></a><span data-ttu-id="86e86-996">Arama belge</span><span class="sxs-lookup"><span data-stu-id="86e86-996">Lookup Document</span></span>
<span data-ttu-id="86e86-997">Merhaba **arama belge** işlemi Azure aramadan belge alır.</span><span class="sxs-lookup"><span data-stu-id="86e86-997">hello **Lookup Document** operation retrieves a document from Azure Search.</span></span> <span data-ttu-id="86e86-998">Bu, bir kullanıcı belirli arama sonucu tıklar ve bu belge hakkında belirli ayrıntıları toolook istediğinizde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-998">This is useful when a user clicks on a specific search result, and you want toolook up specific details about that document.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

<span data-ttu-id="86e86-999">**İstek**</span><span class="sxs-lookup"><span data-stu-id="86e86-999">**Request**</span></span>

<span data-ttu-id="86e86-1000">HTTPS istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1000">HTTPS is required for service requests.</span></span> <span data-ttu-id="86e86-1001">Merhaba **arama belge** isteği oluşturulmasını gibi.</span><span class="sxs-lookup"><span data-stu-id="86e86-1001">hello **Lookup Document** request can be constructed as follows.</span></span>

    GET /indexes/[index name]/docs/key?[query parameters]

<span data-ttu-id="86e86-1002">Alternatif olarak, anahtar aramasını hello geleneksel OData sözdizimini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="86e86-1002">Alternatively, you can use hello traditional OData syntax for key lookup:</span></span>

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

<span data-ttu-id="86e86-1003">Merhaba istek URI içeren bir [dizin adı] ve [Temel], hangi belge tooretrieve hangi dizinden belirtme.</span><span class="sxs-lookup"><span data-stu-id="86e86-1003">hello request URI includes an [index name] and [key], specifying which document tooretrieve from which index.</span></span> <span data-ttu-id="86e86-1004">Ayrıca, aynı anda yalnızca bir belge alabilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1004">You can only get one document at a time.</span></span> <span data-ttu-id="86e86-1005">Kullanım **arama** tooget tek bir istekte birden çok belge.</span><span class="sxs-lookup"><span data-stu-id="86e86-1005">Use **Search** tooget multiple documents in a single request.</span></span>

<span data-ttu-id="86e86-1006">**Sorgu parametreleri**</span><span class="sxs-lookup"><span data-stu-id="86e86-1006">**Query Parameters**</span></span>

<span data-ttu-id="86e86-1007">`$select=[string]`(isteğe bağlı) - virgülle ayrılmış alanlar tooretrieve listesi.</span><span class="sxs-lookup"><span data-stu-id="86e86-1007">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="86e86-1008">Belirtilmemiş veya çok ayarlarsanız`*`, hello şemada alınabilir olarak işaretlenmiş tüm alanlar hello projeksiyon dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1008">If unspecified or set too`*`, all fields marked as retrievable in hello schema are included in hello projection.</span></span>

<span data-ttu-id="86e86-1009">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="86e86-1009">`api-version=[string]` (required).</span></span> <span data-ttu-id="86e86-1010">Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="86e86-1010">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="86e86-1011">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="86e86-1011">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="86e86-1012">Not: Bu işlem için hello `api-version` sorgu parametresi olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1012">Note: For this operation, hello `api-version` is specified as a query parameter.</span></span>

<span data-ttu-id="86e86-1013">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="86e86-1013">**Request Headers**</span></span>

<span data-ttu-id="86e86-1014">liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.</span><span class="sxs-lookup"><span data-stu-id="86e86-1014">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="86e86-1015">`api-key`: Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-1015">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="86e86-1016">Bir dize değeri, benzersiz tooyour hizmeti URL'si değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-1016">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="86e86-1017">Merhaba **arama belge** isteği, bir yönetici anahtarını veya sorgu anahtarı belirtebilirsiniz `api-key`.</span><span class="sxs-lookup"><span data-stu-id="86e86-1017">hello **Lookup Document** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="86e86-1018">Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1018">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="86e86-1019">Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan.</span><span class="sxs-lookup"><span data-stu-id="86e86-1019">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="86e86-1020">Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="86e86-1020">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="86e86-1021">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="86e86-1021">**Request Body**</span></span>

<span data-ttu-id="86e86-1022">yok.</span><span class="sxs-lookup"><span data-stu-id="86e86-1022">None.</span></span>

<span data-ttu-id="86e86-1023">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="86e86-1023">**Response**</span></span>

<span data-ttu-id="86e86-1024">Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.</span><span class="sxs-lookup"><span data-stu-id="86e86-1024">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

<span data-ttu-id="86e86-1025">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="86e86-1025">**Example**</span></span>

<span data-ttu-id="86e86-1026">'2' anahtar içeriyor arama hello belge</span><span class="sxs-lookup"><span data-stu-id="86e86-1026">Lookup hello document that has key '2'</span></span>

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

<span data-ttu-id="86e86-1027">'OData sözdizimini kullanarak 3' anahtarına sahip arama hello belge:</span><span class="sxs-lookup"><span data-stu-id="86e86-1027">Lookup hello document that has key '3' using OData syntax:</span></span>

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a><span data-ttu-id="86e86-1028">Count belgeleri</span><span class="sxs-lookup"><span data-stu-id="86e86-1028">Count Documents</span></span>
<span data-ttu-id="86e86-1029">Merhaba **sayısı belgeleri** işlemi arama dizini belgelerde hello sayısı sayısını alır.</span><span class="sxs-lookup"><span data-stu-id="86e86-1029">hello **Count Documents** operation retrieves a count of hello number of documents in a search index.</span></span> <span data-ttu-id="86e86-1030">Merhaba `$count` sözdizimi hello OData protokolü bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-1030">hello `$count` syntax is part of hello OData protocol.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

<span data-ttu-id="86e86-1031">**İstek**</span><span class="sxs-lookup"><span data-stu-id="86e86-1031">**Request**</span></span>

<span data-ttu-id="86e86-1032">HTTPS istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1032">HTTPS is required for service requests.</span></span> <span data-ttu-id="86e86-1033">Merhaba **sayısı belgeleri** isteği hello GET yöntemini kullanan olacak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="86e86-1033">hello **Count Documents** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="86e86-1034">Merhaba [dizin adı] hello istek URI'SİNDEKİ hello hizmet tooreturn tüm öğelerin sayısını hello belgeleri koleksiyonundaki hello belirtilen dizin söyler.</span><span class="sxs-lookup"><span data-stu-id="86e86-1034">hello [index name] in hello request URI tells hello service tooreturn a count of all items in hello docs collection of hello specified index.</span></span>

<span data-ttu-id="86e86-1035">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="86e86-1035">`api-version=[string]` (required).</span></span> <span data-ttu-id="86e86-1036">Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="86e86-1036">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="86e86-1037">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="86e86-1037">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="86e86-1038">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="86e86-1038">**Request Headers**</span></span>

<span data-ttu-id="86e86-1039">liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.</span><span class="sxs-lookup"><span data-stu-id="86e86-1039">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="86e86-1040">`Accept`: Bu değeri çok ayarlanmalıdır`text/plain`.</span><span class="sxs-lookup"><span data-stu-id="86e86-1040">`Accept`: This value must be set too`text/plain`.</span></span>
* <span data-ttu-id="86e86-1041">`api-key`: Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-1041">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="86e86-1042">Bir dize değeri, benzersiz tooyour hizmeti URL'si değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-1042">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="86e86-1043">Merhaba **sayısı belgeleri** isteği, bir yönetici anahtarını veya sorgu anahtarı belirtebilirsiniz `api-key`.</span><span class="sxs-lookup"><span data-stu-id="86e86-1043">hello **Count Documents** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="86e86-1044">Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1044">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="86e86-1045">Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan.</span><span class="sxs-lookup"><span data-stu-id="86e86-1045">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="86e86-1046">Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="86e86-1046">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="86e86-1047">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="86e86-1047">**Request Body**</span></span>

<span data-ttu-id="86e86-1048">yok.</span><span class="sxs-lookup"><span data-stu-id="86e86-1048">None.</span></span>

<span data-ttu-id="86e86-1049">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="86e86-1049">**Response**</span></span>

<span data-ttu-id="86e86-1050">Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.</span><span class="sxs-lookup"><span data-stu-id="86e86-1050">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="86e86-1051">Merhaba yanıt gövdesi, düz metin olarak biçimlendirilmiş bir tamsayı olarak hello sayısı değeri içerir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1051">hello response body contains hello count value as an integer formatted in plain text.</span></span>

<a name="Suggestions"></a>

## <a name="suggestions"></a><span data-ttu-id="86e86-1052">Öneriler</span><span class="sxs-lookup"><span data-stu-id="86e86-1052">Suggestions</span></span>
<span data-ttu-id="86e86-1053">Merhaba **önerileri** işlemi kısmi arama girişinize göre önerileri alır.</span><span class="sxs-lookup"><span data-stu-id="86e86-1053">hello **Suggestions** operation retrieves suggestions based on partial search input.</span></span> <span data-ttu-id="86e86-1054">Kullanıcıların arama terimi girerek gibi genellikle arama kutuları tooprovide yazarken tamamlanan önerilerine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="86e86-1054">It's typically used in search boxes tooprovide type-ahead suggestions as users are entering search terms.</span></span>

<span data-ttu-id="86e86-1055">Öneri istekleri hedef belgeler öneren adresindeki hedeflenir, birden çok adayı belgeleri hello eşleşiyorsa metin yinelenebilir hello önerilen şekilde aynı giriş arayın.</span><span class="sxs-lookup"><span data-stu-id="86e86-1055">Suggestion requests aim at suggesting target documents, so hello suggested text may be repeated if multiple candidate documents match hello same search input.</span></span> <span data-ttu-id="86e86-1056">Kullanabileceğiniz `$select` tooretrieve diğer belge (Merhaba belge anahtar dahil) alanları böylece hangi belge hello her öneri kaynağıdır anlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86e86-1056">You can use `$select` tooretrieve other document fields (including hello document key) so that you can tell which document is hello source for each suggestion.</span></span>

<span data-ttu-id="86e86-1057">A **önerileri** işlem bir GET veya POST isteği verildi.</span><span class="sxs-lookup"><span data-stu-id="86e86-1057">A **Suggestions** operation is issued as a GET or POST request.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="86e86-1058">**Toouse yerine duyurduğumuzda Al**</span><span class="sxs-lookup"><span data-stu-id="86e86-1058">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="86e86-1059">HTTP GET toocall hello kullandığınızda **önerileri** API, toobe hello istek URL'si hello uzunluğu 8 KB'yi aşamaz kullanan gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1059">When you use HTTP GET toocall hello **Suggestions** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="86e86-1060">Çoğu uygulama için yeterince genellikle budur.</span><span class="sxs-lookup"><span data-stu-id="86e86-1060">This is usually enough for most applications.</span></span> <span data-ttu-id="86e86-1061">Ancak, bazı uygulamalar çok büyük sorgular, özellikle OData filtre ifadeleri üretir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1061">However, some applications produce very large queries, specifically OData filter expressions.</span></span> <span data-ttu-id="86e86-1062">GET daha büyük filtreleri sağladığından bu uygulamalar için HTTP POST kullanılarak daha iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1062">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span></span> <span data-ttu-id="86e86-1063">POST, ile birlikte bir filtre yan tümcelerinde hello sayısı hello sınırlama faktörü, POST için hello isteği boyut sınırı yaklaşık 16 MB olduğundan hello ham filtre dizesi boyutunu hello değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-1063">With POST, hello number of clauses in a filter is hello limiting factor, not hello size of hello raw filter string since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-1064">Merhaba POST isteği boyut sınırı çok büyük olsa da, filtre ifadeleri rasgele karmaşık olamaz.</span><span class="sxs-lookup"><span data-stu-id="86e86-1064">Even though hello POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="86e86-1065">Bkz: [OData ifade sözdizimini](https://msdn.microsoft.com/library/dn798921.aspx) filtre karmaşıklık sınırlamalar hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="86e86-1065">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="86e86-1066">**İstek**</span><span class="sxs-lookup"><span data-stu-id="86e86-1066">**Request**</span></span>

<span data-ttu-id="86e86-1067">HTTPS istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1067">HTTPS is required for service requests.</span></span> <span data-ttu-id="86e86-1068">Merhaba **önerileri** isteği hello GET veya POST yöntemleri kullanarak olacak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="86e86-1068">hello **Suggestions** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="86e86-1069">Merhaba isteğin URI hello dizin tooquery hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1069">hello request URI specifies hello name of hello index tooquery.</span></span> <span data-ttu-id="86e86-1070">Merhaba kısmen giriş arama terimi gibi parametreleri hello sorgu dizesinde GET isteklerinin hello durumda belirtilir ve hello istekte hello durumunun POST gövdesinde ister.</span><span class="sxs-lookup"><span data-stu-id="86e86-1070">Parameters, such as hello partially input search term, are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="86e86-1071">GET isteklerini oluştururken en iyi uygulama, çok unutmayın[URL kodlama](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) çağrılırken parametreleri hello REST API doğrudan belirli sorgu.</span><span class="sxs-lookup"><span data-stu-id="86e86-1071">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="86e86-1072">İçin **önerileri** bu işlemleri içerir:</span><span class="sxs-lookup"><span data-stu-id="86e86-1072">For **Suggestions** operations, this includes:</span></span>

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

<span data-ttu-id="86e86-1073">URL kodlaması sorgu parametreleri yukarıda hello üzerinde yalnızca önerilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1073">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="86e86-1074">Tüm sorgu dizesi (her şeyi hello sonra?), yanlışlıkla URL kodlama Merhaba, istekleri çalışmamasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="86e86-1074">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="86e86-1075">Ayrıca, URL kodlaması yalnızca REST API kullanarak doğrudan alma hello çağrılırken gereklidir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1075">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="86e86-1076">Hiçbir URL kodlaması çağrılırken gereklidir **önerileri** POST, kullanma ya da hello kullanırken [.NET istemci kitaplığını](https://msdn.microsoft.com/library/dn951165.aspx), sizin için URL kodlaması işler.</span><span class="sxs-lookup"><span data-stu-id="86e86-1076">No URL encoding is necessary when calling **Suggestions** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="86e86-1077">**Sorgu parametreleri**</span><span class="sxs-lookup"><span data-stu-id="86e86-1077">**Query Parameters**</span></span>

<span data-ttu-id="86e86-1078">**Öneriler** sorgu ölçütlerini sağlayan ve ayrıca arama davranışını belirtin birkaç parametre kabul eder.</span><span class="sxs-lookup"><span data-stu-id="86e86-1078">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="86e86-1079">Bu parametreler hello URL'deki sorgu dizesi çağrılırken sağladığınız **önerileri** GET aracılığıyla ve JSON özellikleri çağrılırken hello istek gövdesi olarak **önerileri** POST ile.</span><span class="sxs-lookup"><span data-stu-id="86e86-1079">You provide these parameters in hello URL query string when calling **Suggestions** via GET, and as JSON properties in hello request body when calling **Suggestions** via POST.</span></span> <span data-ttu-id="86e86-1080">bazı parametreler için Hello sözdizimi GET ve POST arasında biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-1080">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="86e86-1081">Bu farklılıklar, geçerli aşağıda belirtilmiştir:</span><span class="sxs-lookup"><span data-stu-id="86e86-1081">These differences are noted as applicable below:</span></span>

<span data-ttu-id="86e86-1082">`search=[string]`-arama metni toouse toosuggest sorguları hello.</span><span class="sxs-lookup"><span data-stu-id="86e86-1082">`search=[string]` - hello search text toouse toosuggest queries.</span></span> <span data-ttu-id="86e86-1083">En az 1 karakter ve en fazla 100 karakter olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-1083">Must be at least 1 character, and no more than 100 characters.</span></span>

<span data-ttu-id="86e86-1084">`highlightPreTag=[string]`(isteğe bağlı) - toosearch isabet başına bir dize etiketi.</span><span class="sxs-lookup"><span data-stu-id="86e86-1084">`highlightPreTag=[string]` (optional) - a string tag that prepends toosearch hits.</span></span> <span data-ttu-id="86e86-1085">İle ayarlanmalıdır `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="86e86-1085">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-1086">Çağrılırken **önerileri** GET kullanarak, ayrılmış karakter hello URL (örneğin, % &#23; yerine) yüzde olarak kodlanmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-1086">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="86e86-1087">`highlightPostTag=[string]`(isteğe bağlı) - toosearch isabet ekler bir dize etiketi.</span><span class="sxs-lookup"><span data-stu-id="86e86-1087">`highlightPostTag=[string]` (optional) - a string tag that appends toosearch hits.</span></span> <span data-ttu-id="86e86-1088">İle ayarlanmalıdır `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="86e86-1088">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-1089">Çağrılırken **önerileri** GET kullanarak, ayrılmış karakter hello URL (örneğin, % &#23; yerine) yüzde olarak kodlanmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-1089">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="86e86-1090">`suggesterName=[string]`-Belirtilen hello olarak hello öneri aracı adını hello `suggesters` hello dizin tanımının bir parçası olan koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="86e86-1090">`suggesterName=[string]` - hello name of hello suggester as specified in hello `suggesters` collection that's part of hello index definition.</span></span> <span data-ttu-id="86e86-1091">A `suggester` hangi alanlar için önerilen sorgu terimlerinin taranır belirler.</span><span class="sxs-lookup"><span data-stu-id="86e86-1091">A `suggester` determines which fields are scanned for suggested query terms.</span></span> <span data-ttu-id="86e86-1092">Bkz: [ilgili](#Suggesters) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="86e86-1092">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="86e86-1093">`fuzzy=[boolean]`(isteğe bağlı, varsayılan = false)-tootrue bu ayarlandığında olsa bile bir yedek veya eksik karakter hello arama metnini API öneriler bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="86e86-1093">`fuzzy=[boolean]` (optional, default = false) - when set tootrue this API will find suggestions even if there's a substituted or missing character in hello search text.</span></span> <span data-ttu-id="86e86-1094">Bu bazı senaryolarda daha iyi bir deneyim sağlarken benzer bir öneri aramalar daha yavaş ve daha fazla kaynak tüketmesine maliyeti performanslarının gelir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1094">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span></span>

<span data-ttu-id="86e86-1095">`searchFields=[string]`(isteğe bağlı) - hello için virgülle ayrılmış bir alan adları toosearch hello listesi belirtilen arama metni.</span><span class="sxs-lookup"><span data-stu-id="86e86-1095">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified search text.</span></span> <span data-ttu-id="86e86-1096">Hedef alan önerileri için etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1096">Target fields must be enabled for suggestions.</span></span>

<span data-ttu-id="86e86-1097">`$top=#`(isteğe bağlı, varsayılan = 5)-hello önerileri tooretrieve sayısı.</span><span class="sxs-lookup"><span data-stu-id="86e86-1097">`$top=#` (optional, default = 5) - hello number of suggestions tooretrieve.</span></span> <span data-ttu-id="86e86-1098">1 ile 100 arasında bir sayı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86e86-1098">Must be a number between 1 and 100.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-1099">Çağrılırken **önerileri** POST kullanarak, bu parametre adlı `top` yerine `$top`.</span><span class="sxs-lookup"><span data-stu-id="86e86-1099">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="86e86-1100">`$filter=[string]`(isteğe bağlı) - hello belgeleri filtreleyen bir ifade için öneriler kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1100">`$filter=[string]` (optional) - an expression that filters hello documents considered for suggestions.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-1101">Çağrılırken **önerileri** POST kullanarak, bu parametre adlı `filter` yerine `$filter`.</span><span class="sxs-lookup"><span data-stu-id="86e86-1101">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="86e86-1102">`$orderby=[string]`(isteğe bağlı) - virgülle ayrılmış ifadeler toosort hello sonuçlarına göre listesi.</span><span class="sxs-lookup"><span data-stu-id="86e86-1102">`$orderby=[string]` (optional) - a list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="86e86-1103">Her bir ifadenin bir alan adı veya bir çağrı toohello olabilir `geo.distance()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="86e86-1103">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="86e86-1104">Her deyim tarafından izlenebilir `asc` artan, tooindicated ve `desc` azalan tooindicate.</span><span class="sxs-lookup"><span data-stu-id="86e86-1104">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="86e86-1105">Merhaba varsayılan, artan.</span><span class="sxs-lookup"><span data-stu-id="86e86-1105">hello default is ascending order.</span></span> <span data-ttu-id="86e86-1106">Bir sınır için 32 yan `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="86e86-1106">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-1107">Çağrılırken **önerileri** POST kullanarak, bu parametre adlı `orderby` yerine `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="86e86-1107">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="86e86-1108">`$select=[string]`(isteğe bağlı) - virgülle ayrılmış alanlar tooretrieve listesi.</span><span class="sxs-lookup"><span data-stu-id="86e86-1108">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="86e86-1109">Belirtilmezse, yalnızca belge anahtarını hello ve öneri metni döndürülür.</span><span class="sxs-lookup"><span data-stu-id="86e86-1109">If unspecified, only hello document key and suggestion text is returned.</span></span> <span data-ttu-id="86e86-1110">Bu parametre çok ayarlayarak tüm alanları açıkça isteyebilir`*`.</span><span class="sxs-lookup"><span data-stu-id="86e86-1110">You can explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-1111">Çağrılırken **önerileri** POST kullanarak, bu parametre adlı `select` yerine `$select`.</span><span class="sxs-lookup"><span data-stu-id="86e86-1111">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="86e86-1112">`minimumCoverage`(isteğe bağlı, varsayılan olarak too80) - 0 ve öneriler sorgu hello sorgu toobe sırada tarafından ele alınması gereken hello dizin hello yüzdesini gösteren 100 arasında bir sayı başarı bildirdi.</span><span class="sxs-lookup"><span data-stu-id="86e86-1112">`minimumCoverage` (optional, defaults too80) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a suggestions query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="86e86-1113">Varsayılan olarak, en az % 80 hello dizini kullanılabilir olmalıdır veya `Suggest` 503 HTTP durum kodunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="86e86-1113">By default, at least 80% of hello index must be available or `Suggest` will return HTTP status code 503.</span></span> <span data-ttu-id="86e86-1114">Ayarlarsanız `minimumCoverage` ve `Suggest` başarılı, HTTP 200 dönün ve içeren bir `@search.coverage` hello yanıt hello sorguda eklenmiştir hello dizin hello yüzdesini belirten değer.</span><span class="sxs-lookup"><span data-stu-id="86e86-1114">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="86e86-1115">Bu parametre tooa değerin 100 Hizmetleri ile yalnızca bir çoğaltma için bile arama kullanılabilirlik sağlamak için yararlı olabilir. daha düşük ayarlanması.</span><span class="sxs-lookup"><span data-stu-id="86e86-1115">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="86e86-1116">Ancak, tüm eşleşen öneri toobe hello sonuçlarında mevcut sağlanır.</span><span class="sxs-lookup"><span data-stu-id="86e86-1116">However, not all matching suggestions are guaranteed toobe present in hello results.</span></span> <span data-ttu-id="86e86-1117">Geri çağırma kullanılabilirlik sonra onun değil toolower en iyi daha fazla önemli tooyour uygulama ise `minimumCoverage` varsayılan değerini 80 aşağıda.</span><span class="sxs-lookup"><span data-stu-id="86e86-1117">If recall is more important tooyour application than availability, then it's best not toolower `minimumCoverage` below its default value of 80.</span></span>
> 
> 

<span data-ttu-id="86e86-1118">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="86e86-1118">`api-version=[string]` (required).</span></span> <span data-ttu-id="86e86-1119">Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="86e86-1119">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="86e86-1120">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="86e86-1120">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="86e86-1121">Not: Bu işlem için hello `api-version` olup, çağrı bağımsız olarak hello URL'deki sorgu parametresi olarak belirtilen **önerileri** GET veya POST ile.</span><span class="sxs-lookup"><span data-stu-id="86e86-1121">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Suggestions** with GET or POST.</span></span>

<span data-ttu-id="86e86-1122">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="86e86-1122">**Request Headers**</span></span>

<span data-ttu-id="86e86-1123">liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar</span><span class="sxs-lookup"><span data-stu-id="86e86-1123">hello following list describes hello required and optional request headers</span></span>

* <span data-ttu-id="86e86-1124">`api-key`: Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-1124">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="86e86-1125">Bir dize değeri, benzersiz tooyour hizmeti URL'si değil.</span><span class="sxs-lookup"><span data-stu-id="86e86-1125">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="86e86-1126">Merhaba **önerileri** isteği hello bir yönetici anahtarını veya sorgu anahtarını belirtebilirsiniz `api-key`.</span><span class="sxs-lookup"><span data-stu-id="86e86-1126">hello **Suggestions** request can specify either an admin key or query key as hello `api-key`.</span></span>

<span data-ttu-id="86e86-1127">Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir.</span><span class="sxs-lookup"><span data-stu-id="86e86-1127">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="86e86-1128">Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan.</span><span class="sxs-lookup"><span data-stu-id="86e86-1128">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="86e86-1129">Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="86e86-1129">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="86e86-1130">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="86e86-1130">**Request Body**</span></span>

<span data-ttu-id="86e86-1131">GET için: yok.</span><span class="sxs-lookup"><span data-stu-id="86e86-1131">For GET: None.</span></span>

<span data-ttu-id="86e86-1132">POST için:</span><span class="sxs-lookup"><span data-stu-id="86e86-1132">For POST:</span></span>

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

<span data-ttu-id="86e86-1133">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="86e86-1133">**Response**</span></span>

<span data-ttu-id="86e86-1134">Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.</span><span class="sxs-lookup"><span data-stu-id="86e86-1134">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

<span data-ttu-id="86e86-1135">Merhaba projeksiyon seçeneği hello dizinin her bir öğesinde bulunan kullanılan tooretrieve alanları ise:</span><span class="sxs-lookup"><span data-stu-id="86e86-1135">If hello projection option is used tooretrieve fields they are included in each element of hello array:</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

<span data-ttu-id="86e86-1136">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="86e86-1136">**Example**</span></span>

<span data-ttu-id="86e86-1137">Merhaba kısmi arama giriş 'lux' olduğu 5 önerileri Al</span><span class="sxs-lookup"><span data-stu-id="86e86-1137">Retrieve 5 suggestions where hello partial search input is 'lux'</span></span>

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
