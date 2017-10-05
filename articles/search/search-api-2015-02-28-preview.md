---
title: "Azure Search Hizmeti REST API sürümü 2015-02-28-Önizleme | Microsoft Docs"
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
ms.openlocfilehash: e6ad5c964bfa8421be2706cb4015980e01a271b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="57071-103">Azure Search Hizmeti REST API'si: Sürüm 2015-02-28-Önizleme</span><span class="sxs-lookup"><span data-stu-id="57071-103">Azure Search Service REST API: Version 2015-02-28-Preview</span></span>
<span data-ttu-id="57071-104">Bu makale için başvuru belgesidir `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="57071-104">This article is the reference documentation for `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="57071-105">Bu önizleme geçerli genel olarak kullanılabilir sürüm genişletir [api-version = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), aşağıdaki Deneysel özellikleri sağlayarak:</span><span class="sxs-lookup"><span data-stu-id="57071-105">This preview extends the current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing the following experimental features:</span></span>

* <span data-ttu-id="57071-106">`moreLikeThis`sorgu parametresi olarak [Search belgeleri](#SearchDocs) API.</span><span class="sxs-lookup"><span data-stu-id="57071-106">`moreLikeThis` query parameter in the [Search Documents](#SearchDocs) API.</span></span> <span data-ttu-id="57071-107">Başka bir özel belge için uygun olan diğer belgeleri bulur.</span><span class="sxs-lookup"><span data-stu-id="57071-107">It finds other documents that are relevant to another specific document.</span></span>

<span data-ttu-id="57071-108">Birkaç ek bölümlerini `2015-02-28-Preview` REST API ayrı olarak belgelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="57071-108">A few additional parts of the `2015-02-28-Preview` REST API are documented separately.</span></span> <span data-ttu-id="57071-109">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="57071-109">These include:</span></span>

* [<span data-ttu-id="57071-110">Puanlama profili</span><span class="sxs-lookup"><span data-stu-id="57071-110">Scoring Profiles</span></span>](search-api-scoring-profiles-2015-02-28-preview.md)
* [<span data-ttu-id="57071-111">Dizin Oluşturucular</span><span class="sxs-lookup"><span data-stu-id="57071-111">Indexers</span></span>](search-api-indexers-2015-02-28-preview.md)

<span data-ttu-id="57071-112">Azure Search hizmeti birden çok sürümlerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="57071-112">Azure Search service is available in multiple versions.</span></span> <span data-ttu-id="57071-113">Lütfen [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="57071-113">Please refer to [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span></span>

## <a name="apis-in-this-document"></a><span data-ttu-id="57071-114">Bu belgedeki API'leri</span><span class="sxs-lookup"><span data-stu-id="57071-114">APIs in this document</span></span>
<span data-ttu-id="57071-115">Azure Search Hizmeti API'si API işlemleri için iki URL sözdizimleri destekler: Basit ve OData (bkz [OData (Azure Search API) için destek](http://msdn.microsoft.com/library/azure/dn798932.aspx) Ayrıntılar için).</span><span class="sxs-lookup"><span data-stu-id="57071-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span></span> <span data-ttu-id="57071-116">Aşağıdaki listede basit sözdizimi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="57071-116">The following list shows the simple syntax.</span></span>

[<span data-ttu-id="57071-117">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="57071-117">Create Index</span></span>](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="57071-118">Dizini Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="57071-118">Update Index</span></span>](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="57071-119">Dizin Al</span><span class="sxs-lookup"><span data-stu-id="57071-119">Get Index</span></span>](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="57071-120">Dizinleri listeleme</span><span class="sxs-lookup"><span data-stu-id="57071-120">Listing Indexes</span></span>](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="57071-121">Dizin istatistikleri Al</span><span class="sxs-lookup"><span data-stu-id="57071-121">Get Index Statistics</span></span>](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[<span data-ttu-id="57071-122">Testi Çözümleyicisi</span><span class="sxs-lookup"><span data-stu-id="57071-122">Test Analyzer</span></span>](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[<span data-ttu-id="57071-123">Dizin silme</span><span class="sxs-lookup"><span data-stu-id="57071-123">Delete an Index</span></span>](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="57071-124">Ekleme, silme ve dizin içindeki verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="57071-124">Add, Delete, and Update Data within an Index</span></span>](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[<span data-ttu-id="57071-125">Belge ara</span><span class="sxs-lookup"><span data-stu-id="57071-125">Search Documents</span></span>](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[<span data-ttu-id="57071-126">Arama belge</span><span class="sxs-lookup"><span data-stu-id="57071-126">Lookup Document</span></span>](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[<span data-ttu-id="57071-127">Count belgeleri</span><span class="sxs-lookup"><span data-stu-id="57071-127">Count Documents</span></span>](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[<span data-ttu-id="57071-128">Öneriler</span><span class="sxs-lookup"><span data-stu-id="57071-128">Suggestions</span></span>](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a><span data-ttu-id="57071-129">Dizin işlemleri</span><span class="sxs-lookup"><span data-stu-id="57071-129">Index Operations</span></span>
<span data-ttu-id="57071-130">Oluşturun ve Azure Search hizmeti belirtilen dizin kaynak basit HTTP isteklerini (POST, GET, PUT, DELETE) aracılığıyla dizinlerde yönetin.</span><span class="sxs-lookup"><span data-stu-id="57071-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span></span> <span data-ttu-id="57071-131">Dizin oluşturmak için önce dizin şemasını tanımlayan bir JSON belgesi gönderin.</span><span class="sxs-lookup"><span data-stu-id="57071-131">To create an index, you first POST a JSON document that describes the index schema.</span></span> <span data-ttu-id="57071-132">Şema dizini, kendi veri türleri ve nasıl (örneğin, tam metin araması, filtre, sıralama veya olduğunu) kullanılabilmesi için alan tanımlar.</span><span class="sxs-lookup"><span data-stu-id="57071-132">The schema defines the fields of the index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span></span> <span data-ttu-id="57071-133">Ayrıca dizin davranışını yapılandırmak için Puanlama profilleri, ilgili ve diğer öznitelikleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="57071-133">It also defines scoring profiles, suggesters and other attributes to configure the behavior of the index.</span></span>

<span data-ttu-id="57071-134">Aşağıdaki örnek, bir çizimi iki dillerde tanımlanan açıklama alanı ile otel bilgi aramak için kullanılan bir şema sağlar.</span><span class="sxs-lookup"><span data-stu-id="57071-134">The following example provides an illustration of a schema used for searching on hotel information with the Description field defined in two languages.</span></span> <span data-ttu-id="57071-135">Öznitelikler alanın nasıl kullanılacağına nasıl kontrol dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="57071-135">Notice how attributes control how the field is used.</span></span> <span data-ttu-id="57071-136">Örneğin `hotelId` belge anahtarı olarak kullanılan (`"key": true`) ve tam metin aramalardan dışlandı (`"searchable": false`).</span><span class="sxs-lookup"><span data-stu-id="57071-136">For example the `hotelId` is used as the document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span></span>

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

<span data-ttu-id="57071-137">Dizin oluşturulduktan sonra dizinini doldurmak belgeleri yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="57071-137">After the index is created, you'll upload documents that populate the index.</span></span> <span data-ttu-id="57071-138">Bkz: [ekleme veya güncelleştirme belgeler](#AddOrUpdateDocuments) bu sonraki adım için.</span><span class="sxs-lookup"><span data-stu-id="57071-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span></span>

<span data-ttu-id="57071-139">Azure Search'te dizin oluşturma için video giriş için bkz [kanal 9 bulut kapak bölüm Azure Search üzerinde](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span><span class="sxs-lookup"><span data-stu-id="57071-139">For a video introduction to indexing in Azure Search, see the [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span></span>

<a name="CreateIndex"></a>

## <a name="create-index"></a><span data-ttu-id="57071-140">Dizin Oluşturma</span><span class="sxs-lookup"><span data-stu-id="57071-140">Create Index</span></span>
<span data-ttu-id="57071-141">Bir dizin, düzenleme ve belgeler Azure arama, bir tablo veritabanındaki kayıtları nasıl düzenler için benzer arama birincil yoludur.</span><span class="sxs-lookup"><span data-stu-id="57071-141">An index is the primary means of organizing and searching documents in Azure Search, similar to how a table organizes records in a database.</span></span> <span data-ttu-id="57071-142">Her dizin tüm (alan adları, veri türleri ve özellikleri) dizin şemasıyla uyumlu, ancak dizinler de diğer arama davranışları tanımlamak ek yapıları (ilgili, Puanlama profilleri ve CORS seçenekleri) belirtmeniz belgeleri koleksiyonu vardır.</span><span class="sxs-lookup"><span data-stu-id="57071-142">Each index has a collection of documents that all conform to the index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span></span>

<span data-ttu-id="57071-143">Bir HTTP POST veya PUT İsteği kullanarak Azure Search hizmeti içinde yeni bir dizin oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57071-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span></span> <span data-ttu-id="57071-144">İstek gövdesine dizin ve yapılandırma bilgileri belirten bir JSON Şeması ' dir.</span><span class="sxs-lookup"><span data-stu-id="57071-144">The body of the request is a JSON schema that specifies the index and configuration information.</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="57071-145">Alternatif olarak, PUT kullanın ve URI üzerinde dizin adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="57071-145">Alternatively, you can use PUT and specify the index name on the URI.</span></span> <span data-ttu-id="57071-146">Dizin yoksa, oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="57071-146">If the index does not exist, it will be created.</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

<span data-ttu-id="57071-147">Dizin oluşturma depolanır ve arama işlemlerinin kullanılan belgelerinin yapısını belirler.</span><span class="sxs-lookup"><span data-stu-id="57071-147">Creating an index determines the structure of the documents stored and used in search operations.</span></span> <span data-ttu-id="57071-148">Dizin doldurma ayrı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="57071-148">Populating the index is a separate operation.</span></span> <span data-ttu-id="57071-149">Bu adım için kullanabileceğiniz bir [dizin oluşturucu](https://msdn.microsoft.com/library/azure/mt183328.aspx) (desteklenen veri kaynakları için kullanılabilir) veya bir [Ekle, güncelleştirme veya silme belgeleri](https://msdn.microsoft.com/library/azure/dn798930.aspx) işlemi.</span><span class="sxs-lookup"><span data-stu-id="57071-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span></span> <span data-ttu-id="57071-150">Belgeleri gönderilen ters dizin oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="57071-150">The inverted index is generated when the documents are posted.</span></span>

<span data-ttu-id="57071-151">**Not**: fiyatlandırma katmanı tarafından dizinleri izin verilen maksimum sayısı değişir.</span><span class="sxs-lookup"><span data-stu-id="57071-151">**Note**: The maximum number of indexes allowed varies by pricing tier.</span></span> <span data-ttu-id="57071-152">Ücretsiz hizmeti 3 adede kadar dizinler sağlar.</span><span class="sxs-lookup"><span data-stu-id="57071-152">The free service allows up to 3 indexes.</span></span> <span data-ttu-id="57071-153">Standart hizmeti arama hizmeti başına 50 dizinleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="57071-153">Standard service allows 50 indexes per Search service.</span></span> <span data-ttu-id="57071-154">Bkz: [sınırları ve kısıtlamaları](http://msdn.microsoft.com/library/azure/dn798934.aspx) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="57071-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span></span>

<span data-ttu-id="57071-155">**İstek**</span><span class="sxs-lookup"><span data-stu-id="57071-155">**Request**</span></span>

<span data-ttu-id="57071-156">HTTPS tüm hizmet istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="57071-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="57071-157">**Create Index** isteği POST veya PUT yöntemini kullanan olacak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="57071-157">The **Create Index** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="57071-158">POST kullanırken, dizin şeması tanımı birlikte istek gövdesinde bir dizin adı sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-158">When using POST, you must provide an index name in the request body along with the index schema definition.</span></span> <span data-ttu-id="57071-159">PUT ile dizin adı URL bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-159">With PUT, the index name is part of the URL.</span></span> <span data-ttu-id="57071-160">Dizin yoksa, oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="57071-160">If the index doesn't exist, it is created.</span></span> <span data-ttu-id="57071-161">Zaten varsa, yeni tanımına güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="57071-161">If it already exists, it is updated to the new definition.</span></span>

<span data-ttu-id="57071-162">Dizin adı gerekir küçük olması, bir harf veya sayı ile başlamalı, hiçbir eğik çizgi veya nokta olan ve 128 karakterden kısa olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-162">The index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="57071-163">Tireler ardışık olmayan sürece dizin adı bir harf veya sayı ile başlattıktan sonra kalan adının herhangi harf, sayı ve kısa çizgi, içerebilir.</span><span class="sxs-lookup"><span data-stu-id="57071-163">After starting the index name with a letter or number, the rest of the name can include any letter, number and dashes, as long as the dashes are not consecutive.</span></span>

<span data-ttu-id="57071-164">`api-version` Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="57071-164">The `api-version` is required.</span></span> <span data-ttu-id="57071-165">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) kullanılabilir sürümlerin listesi için.</span><span class="sxs-lookup"><span data-stu-id="57071-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span></span>

<span data-ttu-id="57071-166">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="57071-166">**Request Headers**</span></span>

<span data-ttu-id="57071-167">Aşağıdaki listede gerekli ve isteğe bağlı İstek üstbilgilerinin açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="57071-167">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="57071-168">`Content-Type`: Gerekli.</span><span class="sxs-lookup"><span data-stu-id="57071-168">`Content-Type`: Required.</span></span> <span data-ttu-id="57071-169">Bu ayar`application/json`</span><span class="sxs-lookup"><span data-stu-id="57071-169">Set this to `application/json`</span></span>
* <span data-ttu-id="57071-170">`api-key`: Gerekli.</span><span class="sxs-lookup"><span data-stu-id="57071-170">`api-key`: Required.</span></span> <span data-ttu-id="57071-171">`api-key` İçin kullanılır</span><span class="sxs-lookup"><span data-stu-id="57071-171">The `api-key` is used to</span></span>
* <span data-ttu-id="57071-172">isteğin arama hizmetiniz için kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="57071-172">authenticate the request to your Search service.</span></span> <span data-ttu-id="57071-173">Hizmetinize benzersiz bir dize değeri değil.</span><span class="sxs-lookup"><span data-stu-id="57071-173">It is a string value, unique to your service.</span></span> <span data-ttu-id="57071-174">**Create Index** isteği içermelidir bir `api-key` üstbilgi yönetici anahtarınızı (aksine, bir sorgu anahtarı) ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="57071-174">The **Create Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="57071-175">İstek URL'si oluşturmak için hizmet adı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-175">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="57071-176">Her iki hizmet adını alabilir ve `api-key` Azure Portalı'nda, hizmet panosundan.</span><span class="sxs-lookup"><span data-stu-id="57071-176">You can get both the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="57071-177">Bkz: [portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="57071-177">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="57071-178"><a name="RequestData"></a>
**İstek gövdesi sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="57071-178"><a name="RequestData"></a>
**Request Body Syntax**</span></span>

<span data-ttu-id="57071-179">Bu dizin, veri türleri, öznitelikler yanı sıra isteğe bağlı bir sorgu zamanında eşleşen belgeleri Puanlama amacıyla kullanılan profilleri Puanlama listesi içine beslenecek belgeleri içindeki veri alanlarını listesini içeren bir şema tanımı istek gövdesi içeriyor .</span><span class="sxs-lookup"><span data-stu-id="57071-179">The body of the request contains a schema definition, which includes the list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used to score matching documents at query time.</span></span>

<span data-ttu-id="57071-180">Bir POST isteği için dizin adı istek gövdesinde belirtmeniz gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="57071-180">Note that for a POST request, you must specify the index name in the request body.</span></span>

<span data-ttu-id="57071-181">Yalnızca olabilir bir anahtar alanı dizinde.</span><span class="sxs-lookup"><span data-stu-id="57071-181">There can only be one key field in the index.</span></span> <span data-ttu-id="57071-182">Bu bir dize alanı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-182">It has to be a string field.</span></span> <span data-ttu-id="57071-183">Bu alan dizini içinde depolanan her belge için benzersiz tanımlayıcıyı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="57071-183">This field represents the unique identifier for each document stored within the index.</span></span>

<span data-ttu-id="57071-184">Bir dizinin ana bölümleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="57071-184">The main parts of an index include the following:</span></span>

* `name`
* <span data-ttu-id="57071-185">`fields`Bu ad, veri türü ve bu alan izin verilen eylemleri tanımlayan özellikleri dahil olmak üzere bu dizinine beslenecek.</span><span class="sxs-lookup"><span data-stu-id="57071-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span></span>
* <span data-ttu-id="57071-186">`suggesters`otomatik tamamlamayı veya yazarken tamamlanan sorgular için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-186">`suggesters` used for auto-complete or type-ahead queries.</span></span>
* <span data-ttu-id="57071-187">`scoringProfiles`Derecelendirme özel arama puanı için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-187">`scoringProfiles` used for custom search score ranking.</span></span> <span data-ttu-id="57071-188">Bkz: [Puanlama profili Ekle](https://msdn.microsoft.com/library/azure/dn798928.aspx) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="57071-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span></span>
* <span data-ttu-id="57071-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` belgeler/sorgularınızı dizine ve arama yapılabilir belirteçlere nasıl ayrılır tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used to define how your documents/queries are broken into indexable/searchable tokens.</span></span> <span data-ttu-id="57071-190">Bkz: [analiz Azure Search'te](https://aka.ms//azsanalysis) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="57071-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span></span>
* <span data-ttu-id="57071-191">`defaultScoringProfile`davranışları Puanlama varsayılan üzerine yazmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-191">`defaultScoringProfile` used to overwrite the default scoring behaviors.</span></span>
* <span data-ttu-id="57071-192">`corsOptions`dizininizi çıkış noktaları arası sorguları izin vermek için.</span><span class="sxs-lookup"><span data-stu-id="57071-192">`corsOptions` to allow cross-origin queries against your index.</span></span>

<span data-ttu-id="57071-193">İstek yükünde yapılandırılması söz dizimi aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="57071-193">The syntax for structuring the request payload is as follows.</span></span> <span data-ttu-id="57071-194">Örnek istek, bu konuda daha üzerinde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="57071-194">A sample request is provided further on in this topic.</span></span>

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
          "analyzer": "name of the analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of the search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of the indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in the future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies to searchable fields) {
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
                "boostingDuration": "..." (value representing timespan leading to now over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter to be passed in queries to use as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (the distance in kilometers from the reference location where the boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter to be passed in queries to specify list of tags to compare against target field, see "scoringParameter" for syntax details)
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

<span data-ttu-id="57071-195">**Dizin öznitelikleri**</span><span class="sxs-lookup"><span data-stu-id="57071-195">**Index Attributes**</span></span>

<span data-ttu-id="57071-196">Aşağıdaki öznitelikler, dizin oluşturma sırasında ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="57071-196">The following attributes can be set when creating an index.</span></span> <span data-ttu-id="57071-197">Puanlama ve puanlama profilleri hakkında daha fazla bilgi için bkz [eklemek profilleri Puanlama](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="57071-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span>

<span data-ttu-id="57071-198">`name`-Alanın adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="57071-198">`name` - Sets the name of the field.</span></span>

<span data-ttu-id="57071-199">`type`-Alanın veri türünü ayarlar.</span><span class="sxs-lookup"><span data-stu-id="57071-199">`type` - Sets the data type for the field.</span></span>

<span data-ttu-id="57071-200">`searchable`-Alan tam metin arama yapabilir işaretler.</span><span class="sxs-lookup"><span data-stu-id="57071-200">`searchable` - Marks the field as full-text search-able.</span></span> <span data-ttu-id="57071-201">Başka bir deyişle, dizin oluşturma sırasında sözcük bölme gibi analiz yapılacaktır.</span><span class="sxs-lookup"><span data-stu-id="57071-201">This means it will undergo analysis such as word-breaking during indexing.</span></span> <span data-ttu-id="57071-202">Ayarlarsanız bir `searchable` "güneşli gün", dahili olarak bu gibi bir değer alanına bölme tek tek belirteçlere "güneşli" ve "gün".</span><span class="sxs-lookup"><span data-stu-id="57071-202">If you set a `searchable` field to a value like "sunny day", internally it will be split into the individual tokens "sunny" and "day".</span></span> <span data-ttu-id="57071-203">Bu, bu koşulları için tam metin araması sağlar.</span><span class="sxs-lookup"><span data-stu-id="57071-203">This enables full-text searches for these terms.</span></span> <span data-ttu-id="57071-204">Türünde alanlar `Edm.String` veya `Collection(Edm.String)` olan `searchable` varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="57071-204">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span></span> <span data-ttu-id="57071-205">Diğer türleri alanlarının olamaz `searchable`.</span><span class="sxs-lookup"><span data-stu-id="57071-205">Fields of other types cannot be `searchable`.</span></span>

* <span data-ttu-id="57071-206">**Not**: `searchable` alanları Azure Search tam metin araması için alan değeri ek parçalanmış sürümünü depolayacak beri dizininizdeki ek boşluk kullanma.</span><span class="sxs-lookup"><span data-stu-id="57071-206">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of the field value for full-text searches.</span></span> <span data-ttu-id="57071-207">Dizininizde alanı kaydetmek istediğiniz ve arama dahil edilecek bir alan olması gerekmez, ayarlamak `searchable` için `false`.</span><span class="sxs-lookup"><span data-stu-id="57071-207">If you want to save space in your index and you don't need a field to be included in searches, set `searchable` to `false`.</span></span>

<span data-ttu-id="57071-208">`filterable`-İçinde başvurulacak alan verir `$filter` sorgular.</span><span class="sxs-lookup"><span data-stu-id="57071-208">`filterable` - Allows the field to be referenced in `$filter` queries.</span></span> <span data-ttu-id="57071-209">`filterable`farklı `searchable` dizeleri işlenme içinde.</span><span class="sxs-lookup"><span data-stu-id="57071-209">`filterable` differs from `searchable` in how strings are handled.</span></span> <span data-ttu-id="57071-210">Türünde alanlar `Edm.String` veya `Collection(Edm.String)` olan `filterable` yalnızca tam eşleşme için karşılaştırmaları; bu nedenle Sözcük bölünmesi, uygulanabilecek değil.</span><span class="sxs-lookup"><span data-stu-id="57071-210">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span></span> <span data-ttu-id="57071-211">Örneğin, böyle bir alan ayarlarsanız `f` "güneşli Day" `$filter=f eq 'sunny'` herhangi bir eşleşme bulur ancak `$filter=f eq 'sunny day'` olur.</span><span class="sxs-lookup"><span data-stu-id="57071-211">For example, if you set such a field `f` to "sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span></span> <span data-ttu-id="57071-212">Tüm alanlar `filterable` varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="57071-212">All fields are `filterable` by default.</span></span>

<span data-ttu-id="57071-213">`sortable`-Varsayılan sistem sonuçları puana göre sıralar, ancak birçok deneyimlerinde kullanıcıların belgeleri alanlara göre sıralamayı isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="57071-213">`sortable` - By default the system sorts results by score, but in many experiences users will want to sort by fields in the documents.</span></span> <span data-ttu-id="57071-214">Türünde alanlar `Collection(Edm.String)` olamaz `sortable`.</span><span class="sxs-lookup"><span data-stu-id="57071-214">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span></span> <span data-ttu-id="57071-215">Diğer tüm alanlar `sortable` varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="57071-215">All other fields are `sortable` by default.</span></span>

<span data-ttu-id="57071-216">`facetable`-Genellikle kategorisini (örneğin, dijital kamera ve bakın isabet marka tarafından megapiksel tarafından fiyat, vb. göre arayın.) tarafından isabet sayısı içeren sunu arama sonuçlarının kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-216">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span></span> <span data-ttu-id="57071-217">Bu seçenek türü alanlarla kullanılamaz `Edm.GeographyPoint`.</span><span class="sxs-lookup"><span data-stu-id="57071-217">This option cannot be used with fields of type `Edm.GeographyPoint`.</span></span> <span data-ttu-id="57071-218">Diğer tüm alanlar `facetable` varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="57071-218">All other fields are `facetable` by default.</span></span>

* <span data-ttu-id="57071-219">**Not**: türünde alanlar `Edm.String` olan `filterable`, `sortable`, veya `facetable` 32 KB cinsinden uzunluğu en fazla olabilir.</span><span class="sxs-lookup"><span data-stu-id="57071-219">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span></span> <span data-ttu-id="57071-220">Bu tür alanları tek arama terimi olarak kabul edilir ve Azure Search'te bir terim uzunluğu en fazla 32 KB olduğundan budur.</span><span class="sxs-lookup"><span data-stu-id="57071-220">This is because such fields are treated as a single search term, and the maximum length of a term in Azure Search is 32KB.</span></span> <span data-ttu-id="57071-221">Tek bir dize alanında bu daha fazla metni depolamak gerekiyorsa, açık bir şekilde ayarlamanız gerekir `filterable`, `sortable`, ve `facetable` için `false` , dizin tanımında.</span><span class="sxs-lookup"><span data-stu-id="57071-221">If you need to store more text than this in a single string field, you will need to explicitly set `filterable`, `sortable`, and `facetable` to `false` in your index definition.</span></span>
* <span data-ttu-id="57071-222">**Not**: bir alan ayarlamak yukarıdaki öznitelikleri hiçbiri varsa `true` (`searchable`, `filterable`, `sortable`, veya`facetable`) alan etkili bir şekilde ters dizinden çıkarılır.</span><span class="sxs-lookup"><span data-stu-id="57071-222">**Note**: If a field has none of the above attributes set to `true` (`searchable`, `filterable`, `sortable`,  or`facetable`) the field is effectively excluded from the inverted index.</span></span> <span data-ttu-id="57071-223">Bu seçenek, sorgularda kullanılmaz, ancak arama sonuçlarında gerekli alanlar için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-223">This option is useful for fields that are not used in queries, but are needed in search results.</span></span> <span data-ttu-id="57071-224">Bu tür alanları dizinden hariç performansı artırır.</span><span class="sxs-lookup"><span data-stu-id="57071-224">Excluding such fields from the index improves performance.</span></span>

<span data-ttu-id="57071-225">`key`-Alanın dizini içinde belgeleri için benzersiz tanımlayıcı içeren olarak işaretler.</span><span class="sxs-lookup"><span data-stu-id="57071-225">`key` - Marks the field as containing unique identifiers for documents within the index.</span></span> <span data-ttu-id="57071-226">Yalnızca bir alanın seçilen, olarak `key` alanı ve türü olması gerektiği `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="57071-226">Exactly one field must be chosen as the `key` field and it must be of type `Edm.String`.</span></span> <span data-ttu-id="57071-227">Anahtar alanları için doğrudan aracılığıyla belgeleri aramak için kullanılabilir [arama API](#LookupAPI).</span><span class="sxs-lookup"><span data-stu-id="57071-227">Key fields can be used to look up documents directly via the [Lookup API](#LookupAPI).</span></span>

<span data-ttu-id="57071-228">`retrievable`-Alan bir arama sonucunda döndürülebilecek olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="57071-228">`retrievable` - Sets whether the field can be returned in a search result.</span></span>  <span data-ttu-id="57071-229">Alanı (örneğin, kenar boşluğu) kullanmak bir filtre olarak sıralama veya mekanizması Puanlama istediğiniz, ancak son kullanıcı için görünür olacak alanı istemediğiniz durumlarda kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-229">This is useful when you want to use a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want the field to be visible to the end user.</span></span> <span data-ttu-id="57071-230">Bu öznitelik olmalıdır `true` için `key` alanları.</span><span class="sxs-lookup"><span data-stu-id="57071-230">This attribute must be `true` for `key` fields.</span></span>

<span data-ttu-id="57071-231">`analyzer`-Arama süresini ve dizin oluşturma zamanında alan için kullanılacak çözümleyici adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="57071-231">`analyzer` - Sets the name of the analyzer to use for the field at search time and indexing time.</span></span> <span data-ttu-id="57071-232">İzin verilen değerler için bkz [çözümleyiciler](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="57071-232">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="57071-233">Bu seçenek yalnızca kullanılabilir `searchable` alanları ve ayarlanamaz birlikte ya da `searchAnalyzer` veya `indexAnalyzer`.</span><span class="sxs-lookup"><span data-stu-id="57071-233">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span></span>  <span data-ttu-id="57071-234">Çözümleyicisi seçildikten sonra alan için değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="57071-234">Once the analyzer is chosen, it cannot be changed for the field.</span></span>

<span data-ttu-id="57071-235">`searchAnalyzer`-Arama zaman alan için kullanılan Çözümleyicisi adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="57071-235">`searchAnalyzer` - Sets the name of the analyzer used at search time for the field.</span></span> <span data-ttu-id="57071-236">İzin verilen değerler için bkz [çözümleyiciler](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="57071-236">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="57071-237">Bu seçenek yalnızca kullanılabilir `searchable` alanları.</span><span class="sxs-lookup"><span data-stu-id="57071-237">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="57071-238">İle birlikte ayarlanmalıdır `indexAnalyzer` ve ile birlikte ayarlanamaz `analyzer` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="57071-238">It must be set together with `indexAnalyzer` and it cannot be set together with the `analyzer` option.</span></span> <span data-ttu-id="57071-239">Bu çözümleyici varolan alan güncelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="57071-239">This analyzer can be updated on an existing field.</span></span>

<span data-ttu-id="57071-240">`indexAnalyzer`-Alan için dizin oluşturma zamanında kullanılan Çözümleyicisi adını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="57071-240">`indexAnalyzer` - Sets the name of the analyzer used at indexing time for the field.</span></span> <span data-ttu-id="57071-241">İzin verilen değerler için bkz [çözümleyiciler](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="57071-241">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="57071-242">Bu seçenek yalnızca kullanılabilir `searchable` alanları.</span><span class="sxs-lookup"><span data-stu-id="57071-242">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="57071-243">İle birlikte ayarlanmalıdır `searchAnalyzer` ve ile birlikte ayarlanamaz `analyzer` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="57071-243">It must be set together with `searchAnalyzer` and it cannot be set together with the `analyzer` option.</span></span> <span data-ttu-id="57071-244">Çözümleyicisi seçildikten sonra alan için değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="57071-244">Once the analyzer is chosen, it cannot be changed for the field.</span></span>

<span data-ttu-id="57071-245">`suggesters`-Arama modu ve öneriler için içerik kaynağı olan alanları ayarlar.</span><span class="sxs-lookup"><span data-stu-id="57071-245">`suggesters` - Sets the search mode and fields that are the source of the content for suggestions.</span></span> <span data-ttu-id="57071-246">Bkz: [ilgili](#Suggesters) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="57071-246">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="57071-247">`scoringProfiles`-Hangi öğelerin arama sonuçlarında daha yüksek görünür etkilemek sağlayan özel Puanlama davranışları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="57071-247">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span></span> <span data-ttu-id="57071-248">Puanlama profili, alan ağırlığı ve işlevleri yapılır.</span><span class="sxs-lookup"><span data-stu-id="57071-248">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="57071-249">Bkz: [eklemek profilleri Puanlama](https://msdn.microsoft.com/library/azure/dn798928.aspx) Puanlama profili kullanılan öznitelikler hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="57071-249">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about the attributes used in a scoring profile.</span></span>

<span data-ttu-id="57071-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Dil desteği**</span><span class="sxs-lookup"><span data-stu-id="57071-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span></span>

<span data-ttu-id="57071-251">Aranabilir alanlara analiz uygulanabilecek en sık Sözcük bölünmesi, metin normalleştirme ve koşulları filtreleme ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="57071-251">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span></span> <span data-ttu-id="57071-252">Varsayılan olarak Azure arama aranabilir alanlara sahip analiz [Apache Lucene standart Çözümleyicisi](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) aşağıdaki elemanlara metni keser["Unicode metin kesimleme"](http://unicode.org/reports/tr29/) kuralları.</span><span class="sxs-lookup"><span data-stu-id="57071-252">By default, searchable fields in Azure Search are analyzed with the [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span></span> <span data-ttu-id="57071-253">Ayrıca, standart Çözümleyicisi tüm karakterleri küçük harfe formlarına dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="57071-253">Additionally, the standard analyzer converts all characters to their lower case form.</span></span> <span data-ttu-id="57071-254">Dizinlenmiş belgeleri ve arama terimlerini analiz dizin oluşturma ve sorgu işleme sırasında gidin.</span><span class="sxs-lookup"><span data-stu-id="57071-254">Both indexed documents and search terms go through the analysis during indexing and query processing.</span></span>

<span data-ttu-id="57071-255">Azure arama, çeşitli dillerde destekler.</span><span class="sxs-lookup"><span data-stu-id="57071-255">Azure Search supports a variety of languages.</span></span> <span data-ttu-id="57071-256">Her dil için belirli bir dil özellikleri hesapları bir standart metin Çözümleyicisi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="57071-256">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span></span> <span data-ttu-id="57071-257">Azure arama çözümleyiciler iki tür sunar:</span><span class="sxs-lookup"><span data-stu-id="57071-257">Azure Search offers two types of analyzers:</span></span>

* <span data-ttu-id="57071-258">35 çözümleyiciler Lucene tarafından yedeklenir.</span><span class="sxs-lookup"><span data-stu-id="57071-258">35 analyzers backed by Lucene.</span></span>
* <span data-ttu-id="57071-259">Office ve Bing kullanılan teknoloji işleme özel Microsoft doğal dil desteğiyle 50 Çözümleyicileri.</span><span class="sxs-lookup"><span data-stu-id="57071-259">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span></span>

<span data-ttu-id="57071-260">Bazı geliştiriciler Lucene daha tanıdık, basit, açık kaynak çözümü tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57071-260">Some developers might prefer the more familiar, simple, open-source solution of Lucene.</span></span> <span data-ttu-id="57071-261">Lucene çözümleyiciler hızlıdır, ancak Microsoft çözümleyiciler Gelişmiş lemmatization, word (dillerde Almanca, Danca, Felemenkçe, İsveççe, Norveççe, Estonca, bitiş, Macarca, Slovakça gibi) decompounding ve varlık tanıma (URL'ler gibi özellikleri e-postalar, tarihler, sayılar).</span><span class="sxs-lookup"><span data-stu-id="57071-261">Lucene analyzers are faster, but the Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span></span> <span data-ttu-id="57071-262">Mümkünse, hangisinin daha iyi uygun olduğuna karar vermek için hem Microsoft hem de Lucene çözümleyiciler karşılaştırmaları çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-262">If possible, you should run comparisons of both the Microsoft and Lucene analyzers to decide which one is a better fit.</span></span>

<span data-ttu-id="57071-263">***Nasıl Karşılaştır***</span><span class="sxs-lookup"><span data-stu-id="57071-263">***How they compare***</span></span>

<span data-ttu-id="57071-264">İngilizce için Lucene Çözümleyicisi standart Çözümleyicisi genişletir.</span><span class="sxs-lookup"><span data-stu-id="57071-264">The Lucene analyzer for English extends the standard analyzer.</span></span> <span data-ttu-id="57071-265">('S sondaki) iyelik sözcükleri kaldırır, göre kaynaklanan geçerlidir [bağlantısı kaynaklanan algoritması](http://tartarus.org/~martin/PorterStemmer/)ve İngilizce kaldırır [durdurma sözcükleri](http://en.wikipedia.org/wiki/Stop_words).</span><span class="sxs-lookup"><span data-stu-id="57071-265">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span></span>

<span data-ttu-id="57071-266">Buna karşılık, Microsoft analyzer kaynaklanan yerine lemmatization gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="57071-266">In comparison, the Microsoft analyzer performs lemmatization instead of stemming.</span></span> <span data-ttu-id="57071-267">Bunu işleyebilir bükümlü ve düzensiz sözcük formlarını daha iyi ne daha ilgili arama sonuçlarında sonuçları anlamına gelir (izleme modülünü 7 [Azure arama MVA sunu](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) daha fazla ayrıntı için).</span><span class="sxs-lookup"><span data-stu-id="57071-267">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span></span>

<span data-ttu-id="57071-268">İle Microsoft çözümleyiciler dizin ortalama iki ila üç kat daha yavaş Lucene eşdeğerlerine dil bağlı olarak daha açıktır.</span><span class="sxs-lookup"><span data-stu-id="57071-268">Indexing with Microsoft analyzers is on average two to three times slower than their Lucene equivalents, depending on the language.</span></span> <span data-ttu-id="57071-269">Arama performansını önemli ölçüde ortalama boyutu sorgularında etkilenmemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-269">Search performance should not be significantly affected for average size queries.</span></span>

<span data-ttu-id="57071-270">***Yapılandırma***</span><span class="sxs-lookup"><span data-stu-id="57071-270">***Configuration***</span></span>

<span data-ttu-id="57071-271">Dizin tanımı'ndaki her bir alan için ayarladığınız `analyzer` hangi dil ve satıcı belirten Çözümleyicisi adına özelliği.</span><span class="sxs-lookup"><span data-stu-id="57071-271">For each field in the index definition, you can set the `analyzer` property to an analyzer name that specifies which language and vendor.</span></span> <span data-ttu-id="57071-272">Aynı Çözümleyicisi dizin oluşturma ve bu alan için arama uygulanır.</span><span class="sxs-lookup"><span data-stu-id="57071-272">The same analyzer will be applied when indexing and searching for that field.</span></span>
<span data-ttu-id="57071-273">Örneğin, yana birimi aynı dizinde mevcut İngilizce, Fransızca ve İspanyolca otel açıklamaları için ayrı alanları olabilir.</span><span class="sxs-lookup"><span data-stu-id="57071-273">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in the same index.</span></span> <span data-ttu-id="57071-274">Kullanım ['searchFields' sorgu parametresi](#SearchQueryParameters) karşı sorgularınızda aramak için hangi dile özgü alanı belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="57071-274">Use the ['searchFields' query parameter](#SearchQueryParameters) to specify which language-specific field to search against in your queries.</span></span> <span data-ttu-id="57071-275">Dahil sorgu örnekler gözden geçirebilirsiniz `analyzer` özelliğinde [Search belgeleri](#SearchDocs).</span><span class="sxs-lookup"><span data-stu-id="57071-275">You can review query examples that include the `analyzer` property in [Search Documents](#SearchDocs).</span></span> 

<span data-ttu-id="57071-276">***Çözümleyici listesi***</span><span class="sxs-lookup"><span data-stu-id="57071-276">***Analyzer list***</span></span>

<span data-ttu-id="57071-277">Lucene ve Microsoft Çözümleyicisi adları ile birlikte desteklenen dillerin listesi aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="57071-277">Below is the list of supported languages together with Lucene and Microsoft analyzer names.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="57071-278">Dil</span><span class="sxs-lookup"><span data-stu-id="57071-278">Language</span></span></th>
        <th><span data-ttu-id="57071-279">Microsoft Çözümleyicisi adı</span><span class="sxs-lookup"><span data-stu-id="57071-279">Microsoft analyzer name</span></span></th>
        <th><span data-ttu-id="57071-280">Lucene Çözümleyicisi adı</span><span class="sxs-lookup"><span data-stu-id="57071-280">Lucene analyzer name</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-281">Arapça</span><span class="sxs-lookup"><span data-stu-id="57071-281">Arabic</span></span></td>
        <td><span data-ttu-id="57071-282">ar.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-282">ar.microsoft</span></span></td>
        <td><span data-ttu-id="57071-283">ar.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-283">ar.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="57071-284">Ermenice</span><span class="sxs-lookup"><span data-stu-id="57071-284">Armenian</span></span></td>
        <td></td>
        <td><span data-ttu-id="57071-285">hy.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-285">hy.lucene</span></span></td>
      </tr>
    <tr>
        <td><span data-ttu-id="57071-286">Bangla</span><span class="sxs-lookup"><span data-stu-id="57071-286">Bangla</span></span></td>
        <td><span data-ttu-id="57071-287">Bn.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-287">bn.microsoft</span></span></td>
        <td></td>
    </tr>
      <tr>
        <td><span data-ttu-id="57071-288">Bask dili</span><span class="sxs-lookup"><span data-stu-id="57071-288">Basque</span></span></td>
        <td></td>
        <td><span data-ttu-id="57071-289">EU.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-289">eu.lucene</span></span></td>
    </tr>
      <tr>
         <td><span data-ttu-id="57071-290">Bulgarca</span><span class="sxs-lookup"><span data-stu-id="57071-290">Bulgarian</span></span></td>
        <td><span data-ttu-id="57071-291">BG.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-291">bg.microsoft</span></span></td>
        <td><span data-ttu-id="57071-292">BG.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-292">bg.lucene</span></span></td>
      </tr>
      <tr>
        <td><span data-ttu-id="57071-293">Katalanca</span><span class="sxs-lookup"><span data-stu-id="57071-293">Catalan</span></span></td>
        <td><span data-ttu-id="57071-294">CA.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-294">ca.microsoft</span></span></td>
        <td><span data-ttu-id="57071-295">CA.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-295">ca.lucene</span></span></td>          
      </tr>
    <tr>
        <td><span data-ttu-id="57071-296">Basitleştirilmiş Çince</span><span class="sxs-lookup"><span data-stu-id="57071-296">Chinese Simplified</span></span></td>
        <td><span data-ttu-id="57071-297">zh-Hans.microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-297">zh-Hans.microsoft</span></span></td>
        <td><span data-ttu-id="57071-298">zh-Hans.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-298">zh-Hans.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="57071-299">Geleneksel Çince</span><span class="sxs-lookup"><span data-stu-id="57071-299">Chinese Traditional</span></span></td>
        <td><span data-ttu-id="57071-300">zh-Hant.microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-300">zh-Hant.microsoft</span></span></td>
        <td><span data-ttu-id="57071-301">zh-Hant.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-301">zh-Hant.lucene</span></span></td>        
    <tr>
    <tr>
        <td><span data-ttu-id="57071-302">Hırvatça</span><span class="sxs-lookup"><span data-stu-id="57071-302">Croatian</span></span></td>
        <td><span data-ttu-id="57071-303">hr.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-303">hr.microsoft</span></span></td>
        <td/></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-304">Çekçe</span><span class="sxs-lookup"><span data-stu-id="57071-304">Czech</span></span></td>
        <td><span data-ttu-id="57071-305">cs.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-305">cs.microsoft</span></span></td>
        <td><span data-ttu-id="57071-306">cs.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-306">cs.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="57071-307">Danca</span><span class="sxs-lookup"><span data-stu-id="57071-307">Danish</span></span></td>
        <td><span data-ttu-id="57071-308">da.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-308">da.microsoft</span></span></td>
        <td><span data-ttu-id="57071-309">da.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-309">da.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="57071-310">Hollanda dili</span><span class="sxs-lookup"><span data-stu-id="57071-310">Dutch</span></span></td>
        <td><span data-ttu-id="57071-311">NL.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-311">nl.microsoft</span></span></td>
        <td><span data-ttu-id="57071-312">NL.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-312">nl.lucene</span></span></td>    
    </tr>    
    <tr>
        <td><span data-ttu-id="57071-313">Türkçe</span><span class="sxs-lookup"><span data-stu-id="57071-313">English</span></span></td>        
        <td><span data-ttu-id="57071-314">en.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-314">en.microsoft</span></span></td>
        <td><span data-ttu-id="57071-315">en.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-315">en.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="57071-316">Estonca</span><span class="sxs-lookup"><span data-stu-id="57071-316">Estonian</span></span></td>
        <td><span data-ttu-id="57071-317">et.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-317">et.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-318">Fince</span><span class="sxs-lookup"><span data-stu-id="57071-318">Finnish</span></span></td>
        <td><span data-ttu-id="57071-319">Fi.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-319">fi.microsoft</span></span></td>
        <td><span data-ttu-id="57071-320">Fi.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-320">fi.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="57071-321">Fransızca</span><span class="sxs-lookup"><span data-stu-id="57071-321">French</span></span></td>
        <td><span data-ttu-id="57071-322">fr.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-322">fr.microsoft</span></span></td>
        <td><span data-ttu-id="57071-323">fr.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-323">fr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="57071-324">Galiçya lehçesi</span><span class="sxs-lookup"><span data-stu-id="57071-324">Galician</span></span></td>
        <td></td>
        <td><span data-ttu-id="57071-325">GL.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-325">gl.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="57071-326">Almanca</span><span class="sxs-lookup"><span data-stu-id="57071-326">German</span></span></td>
        <td><span data-ttu-id="57071-327">de.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-327">de.microsoft</span></span></td>
        <td><span data-ttu-id="57071-328">de.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-328">de.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="57071-329">Yunanca</span><span class="sxs-lookup"><span data-stu-id="57071-329">Greek</span></span></td>
        <td><span data-ttu-id="57071-330">el.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-330">el.microsoft</span></span></td>
        <td><span data-ttu-id="57071-331">el.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-331">el.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="57071-332">Gucerat dili</span><span class="sxs-lookup"><span data-stu-id="57071-332">Gujarati</span></span></td>
        <td><span data-ttu-id="57071-333">gu.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-333">gu.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-334">İbranice</span><span class="sxs-lookup"><span data-stu-id="57071-334">Hebrew</span></span></td>
        <td><span data-ttu-id="57071-335">He.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-335">he.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-336">Hintçe</span><span class="sxs-lookup"><span data-stu-id="57071-336">Hindi</span></span></td>
        <td><span data-ttu-id="57071-337">Hi.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-337">hi.microsoft</span></span></td>
        <td><span data-ttu-id="57071-338">Hi.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-338">hi.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="57071-339">Macarca</span><span class="sxs-lookup"><span data-stu-id="57071-339">Hungarian</span></span></td>        
        <td><span data-ttu-id="57071-340">hu.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-340">hu.microsoft</span></span></td>
        <td><span data-ttu-id="57071-341">hu.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-341">hu.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-342">İzlanda dili</span><span class="sxs-lookup"><span data-stu-id="57071-342">Icelandic</span></span></td>
        <td><span data-ttu-id="57071-343">is.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-343">is.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-344">Endonezya dili (Bahasa)</span><span class="sxs-lookup"><span data-stu-id="57071-344">Indonesian (Bahasa)</span></span></td>
        <td><span data-ttu-id="57071-345">id.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-345">id.microsoft</span></span></td>
        <td><span data-ttu-id="57071-346">id.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-346">id.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="57071-347">İrlanda dili</span><span class="sxs-lookup"><span data-stu-id="57071-347">Irish</span></span></td>
        <td></td>
          <td><span data-ttu-id="57071-348">GA.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-348">ga.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-349">İtalyanca</span><span class="sxs-lookup"><span data-stu-id="57071-349">Italian</span></span></td>
        <td><span data-ttu-id="57071-350">it.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-350">it.microsoft</span></span></td>
        <td><span data-ttu-id="57071-351">it.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-351">it.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="57071-352">Japonca</span><span class="sxs-lookup"><span data-stu-id="57071-352">Japanese</span></span></td>
        <td><span data-ttu-id="57071-353">ja.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-353">ja.microsoft</span></span></td>
        <td><span data-ttu-id="57071-354">ja.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-354">ja.lucene</span></span></td>

    </tr>
    <tr>
        <td><span data-ttu-id="57071-355">Kannada dili</span><span class="sxs-lookup"><span data-stu-id="57071-355">Kannada</span></span></td>
        <td><span data-ttu-id="57071-356">Ka.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-356">ka.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-357">Kore dili</span><span class="sxs-lookup"><span data-stu-id="57071-357">Korean</span></span></td>
        <td><span data-ttu-id="57071-358">Ko.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-358">ko.microsoft</span></span></td>
        <td><span data-ttu-id="57071-359">Ko.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-359">ko.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-360">Letonca</span><span class="sxs-lookup"><span data-stu-id="57071-360">Latvian</span></span></td>        
        <td><span data-ttu-id="57071-361">LV.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-361">lv.microsoft</span></span></td>
        <td><span data-ttu-id="57071-362">LV.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-362">lv.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="57071-363">Litvanca</span><span class="sxs-lookup"><span data-stu-id="57071-363">Lithuanian</span></span></td>
        <td><span data-ttu-id="57071-364">lt.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-364">lt.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-365">Malayalam dili</span><span class="sxs-lookup"><span data-stu-id="57071-365">Malayalam</span></span></td>
        <td><span data-ttu-id="57071-366">ML.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-366">ml.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-367">Malay (Latin)</span><span class="sxs-lookup"><span data-stu-id="57071-367">Malay (Latin)</span></span></td>
        <td><span data-ttu-id="57071-368">MS.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-368">ms.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-369">Marathi</span><span class="sxs-lookup"><span data-stu-id="57071-369">Marathi</span></span></td>
        <td><span data-ttu-id="57071-370">Mr.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-370">mr.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-371">Norveççe</span><span class="sxs-lookup"><span data-stu-id="57071-371">Norwegian</span></span></td>
        <td><span data-ttu-id="57071-372">NB.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-372">nb.microsoft</span></span></td>
        <td><span data-ttu-id="57071-373">No.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-373">no.lucene</span></span></td>        
    </tr>
      <tr>
        <td><span data-ttu-id="57071-374">Farsça</span><span class="sxs-lookup"><span data-stu-id="57071-374">Persian</span></span></td>
        <td></td>
        <td><span data-ttu-id="57071-375">FA.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-375">fa.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="57071-376">Lehçe</span><span class="sxs-lookup"><span data-stu-id="57071-376">Polish</span></span></td>
        <td><span data-ttu-id="57071-377">PL.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-377">pl.microsoft</span></span></td>
        <td><span data-ttu-id="57071-378">PL.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-378">pl.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="57071-379">Portekizce (Brezilya)</span><span class="sxs-lookup"><span data-stu-id="57071-379">Portuguese (Brazil)</span></span></td>
        <td><span data-ttu-id="57071-380">PT Br.microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-380">pt-Br.microsoft</span></span></td>
        <td><span data-ttu-id="57071-381">PT Br.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-381">pt-Br.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="57071-382">Portekizce (Portekiz)</span><span class="sxs-lookup"><span data-stu-id="57071-382">Portuguese (Portugal)</span></span></td>
        <td><span data-ttu-id="57071-383">PT Pt.microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-383">pt-Pt.microsoft</span></span></td>        
        <td><span data-ttu-id="57071-384">PT Pt.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-384">pt-Pt.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-385">Pencap dili</span><span class="sxs-lookup"><span data-stu-id="57071-385">Punjabi</span></span></td>
        <td><span data-ttu-id="57071-386">Pa.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-386">pa.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-387">Rumence</span><span class="sxs-lookup"><span data-stu-id="57071-387">Romanian</span></span></td>
        <td><span data-ttu-id="57071-388">Ro.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-388">ro.microsoft</span></span></td>
        <td><span data-ttu-id="57071-389">Ro.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-389">ro.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-390">Rusça</span><span class="sxs-lookup"><span data-stu-id="57071-390">Russian</span></span></td>
        <td><span data-ttu-id="57071-391">RU.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-391">ru.microsoft</span></span></td>
        <td><span data-ttu-id="57071-392">RU.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-392">ru.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="57071-393">Sırpça (Kiril)</span><span class="sxs-lookup"><span data-stu-id="57071-393">Serbian (Cyrillic)</span></span></td>
        <td><span data-ttu-id="57071-394">SR-cyrillic.microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-394">sr-cyrillic.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-395">Sırpça (Latin)</span><span class="sxs-lookup"><span data-stu-id="57071-395">Serbian (Latin)</span></span></td>
        <td><span data-ttu-id="57071-396">SR-latin.microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-396">sr-latin.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-397">Slovakça</span><span class="sxs-lookup"><span data-stu-id="57071-397">Slovak</span></span></td>
        <td><span data-ttu-id="57071-398">SK.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-398">sk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-399">Slovence</span><span class="sxs-lookup"><span data-stu-id="57071-399">Slovenian</span></span></td>
        <td><span data-ttu-id="57071-400">SL.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-400">sl.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-401">İspanyolca</span><span class="sxs-lookup"><span data-stu-id="57071-401">Spanish</span></span></td>
        <td><span data-ttu-id="57071-402">Es.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-402">es.microsoft</span></span></td>
        <td><span data-ttu-id="57071-403">Es.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-403">es.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-404">İsveç dili</span><span class="sxs-lookup"><span data-stu-id="57071-404">Swedish</span></span></td>
        <td><span data-ttu-id="57071-405">sv.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-405">sv.microsoft</span></span></td>
        <td><span data-ttu-id="57071-406">sv.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-406">sv.lucene</span></span></td>
    </tr>

    <tr>
        <td><span data-ttu-id="57071-407">Tamil dili</span><span class="sxs-lookup"><span data-stu-id="57071-407">Tamil</span></span></td>
        <td><span data-ttu-id="57071-408">ta.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-408">ta.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-409">Telugu dili</span><span class="sxs-lookup"><span data-stu-id="57071-409">Telugu</span></span></td>
        <td><span data-ttu-id="57071-410">te.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-410">te.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-411">Tay dili</span><span class="sxs-lookup"><span data-stu-id="57071-411">Thai</span></span></td>
        <td><span data-ttu-id="57071-412">TH.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-412">th.microsoft</span></span></td>
        <td><span data-ttu-id="57071-413">TH.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-413">th.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-414">Türkçe</span><span class="sxs-lookup"><span data-stu-id="57071-414">Turkish</span></span></td>
        <td><span data-ttu-id="57071-415">tr.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-415">tr.microsoft</span></span></td>
        <td><span data-ttu-id="57071-416">tr.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-416">tr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="57071-417">Ukrayna dili</span><span class="sxs-lookup"><span data-stu-id="57071-417">Ukrainian</span></span></td>
        <td><span data-ttu-id="57071-418">UK.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-418">uk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-419">Urduca</span><span class="sxs-lookup"><span data-stu-id="57071-419">Urdu</span></span></td>
        <td><span data-ttu-id="57071-420">Your.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-420">ur.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-421">Vietnam dili</span><span class="sxs-lookup"><span data-stu-id="57071-421">Vietnamese</span></span></td>
        <td><span data-ttu-id="57071-422">vi.Microsoft</span><span class="sxs-lookup"><span data-stu-id="57071-422">vi.microsoft</span></span></td>
        <td></td>
    </tr>
    <td colspan="3"><span data-ttu-id="57071-423">Ayrıca Azure Search dilden bağımsız çözümleyicisi yapılandırmalarını sağlar</span><span class="sxs-lookup"><span data-stu-id="57071-423">Additionally Azure Search provides language-agnostic analyzer configurations</span></span></td>
    <tr>
        <td><span data-ttu-id="57071-424">Standart ASCII Katlama</span><span class="sxs-lookup"><span data-stu-id="57071-424">Standard ASCII Folding</span></span></td>
        <td><span data-ttu-id="57071-425">standardasciifolding.lucene</span><span class="sxs-lookup"><span data-stu-id="57071-425">standardasciifolding.lucene</span></span></td>
        <td>
        <ul>
            <li><span data-ttu-id="57071-426">Unicode metin kesimleme (standart belirteç Oluşturucu)</span><span class="sxs-lookup"><span data-stu-id="57071-426">Unicode text segmentation (Standard Tokenizer)</span></span></li>
            <li><span data-ttu-id="57071-427">ASCII kırılma filtresi - ilk 127 ASCII karakter kümesi ASCII eşdeğerlerine ait olmayan Unicode karakterler dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="57071-427">ASCII folding filter - converts Unicode characters that don't belong to the set of first 127 ASCII characters into their ASCII equivalents.</span></span> <span data-ttu-id="57071-428">Bu, Aksan kaldırmak için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-428">This is useful for removing diacritics.</span></span></li>
        </ul>
        </td>
    </tr>
</table>

<span data-ttu-id="57071-429">İle ek açıklama adları olan tüm çözümleyiciler <i>lucene</i> tarafından sağlanmıştır [Apache Lucene'nın dil Çözümleyicileri](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span><span class="sxs-lookup"><span data-stu-id="57071-429">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span></span> <span data-ttu-id="57071-430">Filtre Katlama ASCII hakkında daha fazla bilgi bulunabilir [burada](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span><span class="sxs-lookup"><span data-stu-id="57071-430">More information about the ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span></span>

<span data-ttu-id="57071-431">**Öneri araçları**</span><span class="sxs-lookup"><span data-stu-id="57071-431">**Suggesters**</span></span>

<span data-ttu-id="57071-432">A `suggester` hangi alanların bir dizin aramaları otomatik tamamlama desteklemek için kullanılacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="57071-432">A `suggester` defines which fields in an index are used to support auto-complete in searches.</span></span> <span data-ttu-id="57071-433">Kısmi arama dizelerini genellikle gönderilir [önerileri API](#Suggestions) kullanıcı bir arama sorgusu yazıyor ve API önerilen tümcecikleri kümesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="57071-433">Typically partial search strings are sent to the [Suggestions API](#Suggestions) while the user is typing a search query, and the API returns a set of suggested phrases.</span></span> <span data-ttu-id="57071-434">Hangi alanların yazarken tamamlanan arama terimleri oluşturmak için kullanılan dizinde tanımladığınız bir öneri aracı belirler.</span><span class="sxs-lookup"><span data-stu-id="57071-434">A suggester that you define in the index determines which fields are used to build the type-ahead search terms.</span></span> <span data-ttu-id="57071-435">Bkz: [ilgili](#Suggesters) yapılandırma ayrıntıları için.</span><span class="sxs-lookup"><span data-stu-id="57071-435">See [Suggesters](#Suggesters) for configuration details.</span></span>

<span data-ttu-id="57071-436">**Puanlama modelleri**</span><span class="sxs-lookup"><span data-stu-id="57071-436">**Scoring profiles**</span></span>

<span data-ttu-id="57071-437">A `scoringProfile` hangi öğelerin arama sonuçlarında daha yüksek görünür etkilemek sağlayan özel Puanlama davranışları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="57071-437">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in the search results.</span></span> <span data-ttu-id="57071-438">Puanlama profili, alan ağırlığı ve işlevleri yapılır.</span><span class="sxs-lookup"><span data-stu-id="57071-438">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="57071-439">Bunları kullanmak için sorgu dizesi adına göre bir profili belirtin.</span><span class="sxs-lookup"><span data-stu-id="57071-439">To use them, you specify a profile by name on the query string.</span></span>

<span data-ttu-id="57071-440">Arka planda bir sonuç kümesi bulunan her öğe için bir arama puanı hesaplamak için bir varsayılan profili Puanlama çalışır.</span><span class="sxs-lookup"><span data-stu-id="57071-440">A default scoring profile operates behind the scenes to compute a search score for every item in a result set.</span></span> <span data-ttu-id="57071-441">İç, Puanlama profili adlandırılmamış kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57071-441">You can use the internal, unnamed scoring profile.</span></span> <span data-ttu-id="57071-442">Alternatif olarak, kümesinin `defaultScoringProfile` özel bir profil varsayılan olarak kullanmak üzere özel bir profil sorgu dizesinde belirtilmediğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="57071-442">Alternatively, set `defaultScoringProfile` to use a custom profile as the default, invoked whenever a custom profile is not specified on the query string.</span></span>

<span data-ttu-id="57071-443">Bkz: [arama dizini (Azure Search Hizmeti REST API'si) Puanlama profili Ekle](search-api-scoring-profiles-2015-02-28-preview.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="57071-443">See [Add scoring profiles to a search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span></span>

<span data-ttu-id="57071-444">**CORS seçenekleri**</span><span class="sxs-lookup"><span data-stu-id="57071-444">**CORS Options**</span></span>

<span data-ttu-id="57071-445">Tarayıcı tüm çıkış noktaları arası istekleri engeller istemci tarafı Javascript herhangi API'leri varsayılan olarak çağrılamaz.</span><span class="sxs-lookup"><span data-stu-id="57071-445">Client-side Javascript cannot call any APIs by default since the browser will prevent all cross-origin requests.</span></span> <span data-ttu-id="57071-446">CORS (çıkış noktaları arası kaynak paylaşımı) ayarlayarak etkinleştir `corsOptions` dizininizi çıkış noktaları arası sorgularına izin vermek için öznitelik.</span><span class="sxs-lookup"><span data-stu-id="57071-446">Enable CORS (Cross-Origin Resource Sharing) by setting the `corsOptions` attribute to allow cross-origin queries to your index.</span></span> <span data-ttu-id="57071-447">Yalnızca bu sorguyu güvenlik nedeniyle CORS desteğini API'leri unutmayın.</span><span class="sxs-lookup"><span data-stu-id="57071-447">Note that only query APIs support CORS for security reasons.</span></span> <span data-ttu-id="57071-448">CORS için aşağıdaki seçenekler ayarlanabilir:</span><span class="sxs-lookup"><span data-stu-id="57071-448">The following options can be set for CORS:</span></span>

* <span data-ttu-id="57071-449">`allowedOrigins`(gerekli): Bu bir dizininize erişim izni verilecek çıkış noktaları listesidir.</span><span class="sxs-lookup"><span data-stu-id="57071-449">`allowedOrigins` (required): This is a list of origins that will be granted access to your index.</span></span> <span data-ttu-id="57071-450">Bu çıkış noktalarından sunulacak tüm Javascript kodlarının bu anlamına gelir (doğru API anahtarını verdiği varsayılarak) dizininizi sorgulama izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="57071-450">This means that any Javascript code served from those origins will be allowed to query your index (assuming it provides the correct API key).</span></span> <span data-ttu-id="57071-451">Her kaynak kod biçimidir genellikle `protocol://fully-qualified-domain-name:port` ancak bağlantı noktası çoğunlukla yazılmaz.</span><span class="sxs-lookup"><span data-stu-id="57071-451">Each origin is typically of the form `protocol://fully-qualified-domain-name:port` although the port is often omitted.</span></span> <span data-ttu-id="57071-452">Bkz: [bu makalede](http://go.microsoft.com/fwlink/?LinkId=330822) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="57071-452">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span></span>
  * <span data-ttu-id="57071-453">Tüm kaynaklara erişmesine izin vermek istiyorsanız, dahil `*` tek bir öğe olarak `allowedOrigins` dizi.</span><span class="sxs-lookup"><span data-stu-id="57071-453">If you want to allow access to all origins, include `*` as a single item in the `allowedOrigins` array.</span></span> <span data-ttu-id="57071-454">Unutmayın **bu yöntem üretim arama hizmetleri için önerilmez.**</span><span class="sxs-lookup"><span data-stu-id="57071-454">Note that **this is not recommended practice for production search services.**</span></span> <span data-ttu-id="57071-455">Ancak, geliştirme veya hata ayıklama için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="57071-455">However, it may be useful for development or debugging purposes.</span></span>
* <span data-ttu-id="57071-456">`maxAgeInSeconds`(isteğe bağlı): tarayıcılar bu değer önbellek CORS denetim öncesi yanıtlarını süresi (saniye) belirlemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="57071-456">`maxAgeInSeconds` (optional): Browsers use this value to determine the duration (in seconds) to cache CORS preflight responses.</span></span> <span data-ttu-id="57071-457">Bu, negatif olmayan bir tamsayı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-457">This must be a non-negative integer.</span></span> <span data-ttu-id="57071-458">Bu değer büyük, daha iyi performans olur ancak CORS İlkesi değişikliklerinin etkili olması alacaktır uzun.</span><span class="sxs-lookup"><span data-stu-id="57071-458">The larger this value is, the better performance will be, but the longer it will take for CORS policy changes to take effect.</span></span> <span data-ttu-id="57071-459">Ayarlanmazsa, varsayılan süre olan 5 dakika kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-459">If it is not set, a default duration of 5 minutes will be used.</span></span>

<span data-ttu-id="57071-460"><a name="CreateUpdateIndexExample"></a>
**İstek gövdesi örneği**</span><span class="sxs-lookup"><span data-stu-id="57071-460"><a name="CreateUpdateIndexExample"></a>
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

<span data-ttu-id="57071-461">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="57071-461">**Response**</span></span>

<span data-ttu-id="57071-462">Başarılı bir istek için: "201 oluşturuldu".</span><span class="sxs-lookup"><span data-stu-id="57071-462">For a successful request: "201 Created".</span></span>

<span data-ttu-id="57071-463">Varsayılan olarak yanıt gövdesi JSON için oluşturulan dizin tanımını içerir.</span><span class="sxs-lookup"><span data-stu-id="57071-463">By default the response body will contain the JSON for the index definition that was created.</span></span> <span data-ttu-id="57071-464">Varsa `Prefer` istek üstbilgisi olarak ayarlanmış `return=minimal`, yanıt gövdesi boş olur ve başarı durumunu kodu olacaktır "204 İçerik yok" yerine "201 oluşturuldu".</span><span class="sxs-lookup"><span data-stu-id="57071-464">If the `Prefer` request header is set to `return=minimal`, the response body will be empty and the success status code will be "204 No Content" instead of "201 Created".</span></span> <span data-ttu-id="57071-465">Bu, olup PUT veya POST dizini oluşturmak için kullanılan bağımsız olarak geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="57071-465">This is true regardless of whether PUT or POST was used to create the index.</span></span>

<span data-ttu-id="57071-466">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="57071-466">**Remarks**</span></span>

<span data-ttu-id="57071-467">Şu anda, sınırlı dizin şeması güncelleştirmelerini desteği yoktur.</span><span class="sxs-lookup"><span data-stu-id="57071-467">Currently, there is limited support for index schema updates.</span></span> <span data-ttu-id="57071-468">Alan türlerinin değiştirilmesi gibi yeniden dizinlemeyi gerektiren hiçbir şema güncelleştirmesi şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="57071-468">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span></span> <span data-ttu-id="57071-469">Var olan alanları değiştirilmiş veya silinemez ancak herhangi bir zamanda mevcut bir dizine yeni alanlar eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="57071-469">Although existing fields cannot be changed or deleted, new fields can be added to an existing index at any time.</span></span> <span data-ttu-id="57071-470">Yeni bir alan eklediğinizde, dizindeki tüm mevcut belgeleri otomatik olarak bu alan için bir null değer sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="57071-470">When a new field is added, all existing documents in the index will automatically have a null value for that field.</span></span> <span data-ttu-id="57071-471">Yeni belgeler dizin için eklenene kadar hiçbir ek depolama alanı tüketilebilir.</span><span class="sxs-lookup"><span data-stu-id="57071-471">No additional storage space will be consumed until new documents are added to the index.</span></span>

<a name="Suggesters"></a>

## <a name="suggesters"></a><span data-ttu-id="57071-472">Öneri Araçları</span><span class="sxs-lookup"><span data-stu-id="57071-472">Suggesters</span></span>
<span data-ttu-id="57071-473">Arama kutusuna girilen kısmi dize girişleri yanıta olası arama terimlerini listesini sağlayan yazarken tamamlanan veya otomatik tamamlama sorgusu özelliği, Azure Search'te önerileri özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="57071-473">The suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response to partial string inputs entered into a search box.</span></span> <span data-ttu-id="57071-474">Büyük olasılıkla Sorgu önerileri ticari web arama motorları kullanılırken fark: Bing içinde ".NET" yazarak üreten koşulları listesini ".NET 4.5", ".NET Framework 3,5", vb..</span><span class="sxs-lookup"><span data-stu-id="57071-474">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span></span> <span data-ttu-id="57071-475">Arama hizmeti REST API kullanırken, özel bir Azure Search uygulamada önerileri uygulamak için şunlar gerekir:</span><span class="sxs-lookup"><span data-stu-id="57071-475">When using the Search service REST API, implementing suggestions in a custom Azure Search application requires the following:</span></span>

* <span data-ttu-id="57071-476">Ekleyerek önerilerini etkinleştirmek bir **öneri aracı** adı, arama modu ve alanların listesi için yazarken tamamlanan vermiş dizininizdeki yapım çağrılır.</span><span class="sxs-lookup"><span data-stu-id="57071-476">Enable suggestions by adding a **suggester** construction in your index, giving the name, search mode, and a list of fields for which type-ahead is invoked.</span></span> <span data-ttu-id="57071-477">Kısmi arama dizesi "Sea" yazarak bir kaynak alanı olarak "ŞehirAdı" belirtirseniz, örneğin, "Seattle", "Sahil" ve "(üçü gerçek Şehir adlardır) Seatac Sorgu önerileri kullanıcıya sunulan" neden olur.</span><span class="sxs-lookup"><span data-stu-id="57071-477">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions to the user.</span></span>
* <span data-ttu-id="57071-478">Öneriler çağırarak çağırma [önerileri API](#Suggestions) , uygulama kodunuzda.</span><span class="sxs-lookup"><span data-stu-id="57071-478">Invoke suggestions by calling the [Suggestions API](#Suggestions) in your application code.</span></span> <span data-ttu-id="57071-479">Genellikle kısmi arama dizelerini kullanıcı bir arama sorgusu yazıyor ve bu API önerilen tümcecikleri kümesini döndürür hizmetine gönderilir.</span><span class="sxs-lookup"><span data-stu-id="57071-479">Typically partial search strings are sent to the service while the user is typing a search query, and this API returns a set of suggested phrases.</span></span>

<span data-ttu-id="57071-480">Bu makalede nasıl yapılandırılacağı açıklanmaktadır bir **öneri aracı**.</span><span class="sxs-lookup"><span data-stu-id="57071-480">This article explains how to configure a **suggester**.</span></span> <span data-ttu-id="57071-481">Da gözden geçirmelisiniz [önerileri API](#Suggestions) bir öneri Aracı nasıl kullanıldığı hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="57071-481">You should also review the [Suggestions API](#Suggestions) for details on how a suggester is used.</span></span>

<span data-ttu-id="57071-482">**Kullanım**</span><span class="sxs-lookup"><span data-stu-id="57071-482">**Usage**</span></span>

<span data-ttu-id="57071-483">`Suggesters`Dizin ve iş veya belirli belgeleri yerine gevşek koşulları tümce önermek üzere kullanıldığında en iyi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="57071-483">`Suggesters` are created in the index and work best when used to suggest specific documents rather than loose terms or phrases.</span></span> <span data-ttu-id="57071-484">En iyi adayı başlıklar, adları ve bir öğe tanımlayabilir diğer görece kısa tümceleri alanlardır.</span><span class="sxs-lookup"><span data-stu-id="57071-484">The best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span></span> <span data-ttu-id="57071-485">Kategoriler ve etiketler gibi yinelenen alanları veya çok uzun alanları açıklamaları veya açıklamalar alanları gibi daha az etkili olur.</span><span class="sxs-lookup"><span data-stu-id="57071-485">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span></span>

<span data-ttu-id="57071-486">Dizin tanımı bir parçası olarak, tek bir öneri aracı için ekleyebilirsiniz `suggesters` koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="57071-486">As part of the index definition, you can add a single suggester to the `suggesters` collection.</span></span> <span data-ttu-id="57071-487">Bir öneri aracı tanımlayan özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="57071-487">Properties that define a suggester include the following:</span></span>

* <span data-ttu-id="57071-488">`name`: Öneri aracı adı.</span><span class="sxs-lookup"><span data-stu-id="57071-488">`name`: The name of the suggester.</span></span> <span data-ttu-id="57071-489">Öneri aracı adını çağrılırken kullanmak `suggest` API.</span><span class="sxs-lookup"><span data-stu-id="57071-489">You use the name of the suggester when calling the `suggest` API.</span></span>
* <span data-ttu-id="57071-490">`searchMode`: Aday tümcecikleri aramak için kullanılan stratejisi.</span><span class="sxs-lookup"><span data-stu-id="57071-490">`searchMode`: The strategy used to search for candidate phrases.</span></span> <span data-ttu-id="57071-491">Şu anda desteklenen tek mod `analyzingInfixMatching`, başında veya ortasında cümleleri esnek eşleştirilmesini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="57071-491">The only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at the beginning or in the middle of sentences.</span></span>
* <span data-ttu-id="57071-492">`sourceFields`: Öneriler için içerik kaynağı olan bir veya daha fazla alanları bir listesi.</span><span class="sxs-lookup"><span data-stu-id="57071-492">`sourceFields`: A list of one or more fields that are the source of the content for suggestions.</span></span> <span data-ttu-id="57071-493">Yalnızca türünde alanlar `Edm.String` ve `Collection(Edm.String)` kaynakları önerileri için olabilir.</span><span class="sxs-lookup"><span data-stu-id="57071-493">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span></span> <span data-ttu-id="57071-494">Ayarlama özel bir dil Çözümleyicisi sahip olmayan alanlar kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="57071-494">Only fields that don't have a custom language analyzer set can be used.</span></span>

<span data-ttu-id="57071-495">**Öneri aracı örneği**</span><span class="sxs-lookup"><span data-stu-id="57071-495">**Suggester Example**</span></span>

<span data-ttu-id="57071-496">Bir öneri aracı dizini bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-496">A suggester is part of the index.</span></span> <span data-ttu-id="57071-497">Yalnızca bir öneri aracı varolabilir `suggesters` alanlar koleksiyonu yanında geçerli sürümü koleksiyonunda ve `scoringProfiles`.</span><span class="sxs-lookup"><span data-stu-id="57071-497">Only one suggester can exist in the `suggesters` collection in the current version, alongside the fields collection and `scoringProfiles`.</span></span>

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
> <span data-ttu-id="57071-498">Azure Search, genel Önizleme sürümü kullandıysanız `suggesters` daha eski bir boolean özelliği değiştirir (`"suggestions": false`), yalnızca desteklenen önek önerileri için kısa dizeleri (3-25 karakter).</span><span class="sxs-lookup"><span data-stu-id="57071-498">If you used the public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span></span> <span data-ttu-id="57071-499">Kendi değiştirme `suggesters`, destekler infix başında veya ortasında alan içeriği, bir arama dizelerini hatalar için daha iyi tolerans ile eşleşen terimleri bulduğu eşleşen.</span><span class="sxs-lookup"><span data-stu-id="57071-499">Its replacement, `suggesters`, supports infix matching that finds matching terms at the beginning or in the middle of field content, with better tolerance for mistakes in search strings.</span></span> <span data-ttu-id="57071-500">Genel olarak kullanılabilir sürümünden başlayarak, bu artık yalnızca API önerileri uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-500">Starting with the generally available release, this is now the only implementation of the suggestions API.</span></span> <span data-ttu-id="57071-501">Eski `suggestions` sunulmuştur özelliği `api-version=2014-07-31-Preview` bu sürümde çalışmaya devam eder, ancak içinde çalışmıyor `2015-02-28` veya Azure Search'ın sonraki sürümleri.</span><span class="sxs-lookup"><span data-stu-id="57071-501">The older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues to work in that version, but is not operational in the `2015-02-28` or later versions of Azure Search.</span></span>
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a><span data-ttu-id="57071-502">Dizini Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="57071-502">Update Index</span></span>
<span data-ttu-id="57071-503">Bir HTTP PUT İsteği kullanarak Azure Search'te içinde varolan bir dizin güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57071-503">You can update an existing index within Azure Search using an HTTP PUT request.</span></span> <span data-ttu-id="57071-504">Güncelleştirmeler için varolan şema yeni alanlar ekleyerek, CORS seçenekleri değiştirme ve puanlama profilleri değiştirme içerebilir.</span><span class="sxs-lookup"><span data-stu-id="57071-504">Updates can include adding new fields to the existing schema, modifying CORS options, and modifying scoring profiles.</span></span> <span data-ttu-id="57071-505">Bkz: [eklemek profilleri Puanlama](https://msdn.microsoft.com/library/azure/dn798928.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="57071-505">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> <span data-ttu-id="57071-506">İstek URI'si güncelleştirmek için dizin adını belirtin:</span><span class="sxs-lookup"><span data-stu-id="57071-506">You specify the name of the index to update on the request URI:</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="57071-507">**Önemli:** arama dizinini yeniden oluşturmayı gerektirmeyen işlemleri için dizin şeması güncelleştirmeler için destek sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-507">**Important:** Support for index schema updates is limited to operations that don't require rebuilding the search index.</span></span> <span data-ttu-id="57071-508">Alan türlerinin değiştirilmesi gibi yeniden dizinlemeyi gerektiren hiçbir şema güncelleştirmesi şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="57071-508">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span></span> <span data-ttu-id="57071-509">Var olan alanları değiştirilmiş veya silinemez ancak herhangi bir zamanda yeni alanlar eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="57071-509">New fields can be added at any time, although existing fields cannot be changed or deleted.</span></span> <span data-ttu-id="57071-510">Aynı durum geçerlidir `suggesters`.</span><span class="sxs-lookup"><span data-stu-id="57071-510">The same applies to `suggesters`.</span></span> <span data-ttu-id="57071-511">Yeni alanlar eklenebilir bir öneri aracı zaman alanları eklenir, ancak alanları öğesinden kaldırılamaz `suggesters` ve var olan alanları eklenemez `suggesters`.</span><span class="sxs-lookup"><span data-stu-id="57071-511">New fields may be added to a suggester at the time the fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added to `suggesters`.</span></span>

<span data-ttu-id="57071-512">Yeni bir alan için bir dizin eklerken, dizindeki tüm mevcut belgeleri otomatik olarak bu alan için bir null değer sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="57071-512">When adding a new field to an index, all existing documents in the index will automatically have a null value for that field.</span></span> <span data-ttu-id="57071-513">Yeni belgeler dizin için eklenene kadar hiçbir ek depolama alanı tüketilebilir.</span><span class="sxs-lookup"><span data-stu-id="57071-513">No additional storage space will be consumed until new documents are added to the index.</span></span>

<span data-ttu-id="57071-514">**İstek**</span><span class="sxs-lookup"><span data-stu-id="57071-514">**Request**</span></span>

<span data-ttu-id="57071-515">HTTPS tüm hizmet istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="57071-515">HTTPS is required for all service requests.</span></span> <span data-ttu-id="57071-516">**Güncelleştirme dizin** isteği HTTP PUT kullanarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="57071-516">The **Update Index** request is constructed using HTTP PUT.</span></span> <span data-ttu-id="57071-517">PUT ile dizin adı URL bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-517">With PUT, the index name is part of the URL.</span></span> <span data-ttu-id="57071-518">Dizin yoksa, oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="57071-518">If the index doesn't exist, it is created.</span></span> <span data-ttu-id="57071-519">Dizini zaten varsa, yeni tanımına güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="57071-519">If the index already exists, it is updated to the new definition.</span></span>

<span data-ttu-id="57071-520">Dizin adı gerekir küçük olması, bir harf veya sayı ile başlamalı, hiçbir eğik çizgi veya nokta olan ve 128 karakterden kısa olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-520">The index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="57071-521">Tireler ardışık olmayan sürece dizin adı bir harf veya sayı ile başlattıktan sonra kalan adının herhangi harf, sayı ve kısa çizgi, içerebilir.</span><span class="sxs-lookup"><span data-stu-id="57071-521">After starting the index name with a letter or number, the rest of the name can include any letter, number and dashes, as long as the dashes are not consecutive.</span></span>

<span data-ttu-id="57071-522">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="57071-522">`api-version=[string]` (required).</span></span> <span data-ttu-id="57071-523">Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="57071-523">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="57071-524">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="57071-524">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="57071-525">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="57071-525">**Request Headers**</span></span>

<span data-ttu-id="57071-526">Aşağıdaki listede gerekli ve isteğe bağlı İstek üstbilgilerinin açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="57071-526">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="57071-527">`Content-Type`: Gerekli.</span><span class="sxs-lookup"><span data-stu-id="57071-527">`Content-Type`: Required.</span></span> <span data-ttu-id="57071-528">Bu ayar`application/json`</span><span class="sxs-lookup"><span data-stu-id="57071-528">Set this to `application/json`</span></span>
* <span data-ttu-id="57071-529">`api-key`: Gerekli.</span><span class="sxs-lookup"><span data-stu-id="57071-529">`api-key`: Required.</span></span> <span data-ttu-id="57071-530">`api-key` İsteğin arama hizmetiniz için kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-530">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="57071-531">Hizmetinize benzersiz bir dize değeri değil.</span><span class="sxs-lookup"><span data-stu-id="57071-531">It is a string value, unique to your service.</span></span> <span data-ttu-id="57071-532">**Güncelleştirme dizin** isteği içermelidir bir `api-key` üstbilgi yönetici anahtarınızı (aksine, bir sorgu anahtarı) ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="57071-532">The **Update Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="57071-533">İstek URL'si oluşturmak için hizmet adı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-533">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="57071-534">Hizmet adını alabilir ve `api-key` Azure Portalı'nda, hizmet panosundan.</span><span class="sxs-lookup"><span data-stu-id="57071-534">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="57071-535">Bkz: [portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="57071-535">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="57071-536">**İstek gövdesi sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="57071-536">**Request Body Syntax**</span></span>

<span data-ttu-id="57071-537">Varolan bir dizini güncelleştirirken gövdesi özgün şema tanımı artı eklediğiniz yeni alanlar yanı sıra, ilgili ve CORS seçenekleri değiştirilmiş Puanlama profilini varsa eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-537">When updating an existing index, the body must include the original schema definition, plus the new fields you are adding, as well as the modified scoring profiles, suggesters and CORS options, if any.</span></span> <span data-ttu-id="57071-538">Puanlama profili ve CORS seçenekleri değiştirme değil, dizin oluşturulduğu gelen özgün eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-538">If you are not modifying the scoring profiles and CORS options, you must include the originals from when the index was created.</span></span> <span data-ttu-id="57071-539">Genel güncelleştirmeleri için kullanılacak en iyi düzeni olan bir GET ile dizin tanımı almak için değiştirin, ardından PUT ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="57071-539">In general the best pattern to use for updates is to retrieve the index definition with a GET, modify it, then update it with PUT.</span></span>

<span data-ttu-id="57071-540">Dizin oluşturmak için kullanılan şema sözdizimi burada kolaylık olması için yeniden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="57071-540">The schema syntax used to create an index is reproduced here for convenience.</span></span> <span data-ttu-id="57071-541">Bkz: [Create Index](#CreateIndex) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="57071-541">See [Create Index](#CreateIndex) for more details.</span></span>

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
          "analyzer": "name of the analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of the search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of the indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in the future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies to searchable fields) {
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
                "boostingDuration": "..." (value representing timespan leading to now over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter to be passed in queries to use as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (the distance in kilometers from the reference location where the boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter to be passed in queries to specify list of tags to compare against target field, see "scoringParameter" for syntax details)
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


<span data-ttu-id="57071-542">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="57071-542">**Response**</span></span>

<span data-ttu-id="57071-543">Başarılı bir istek için: "204 İçerik yok".</span><span class="sxs-lookup"><span data-stu-id="57071-543">For a successful request: "204 No Content".</span></span>

<span data-ttu-id="57071-544">Varsayılan olarak yanıt gövdesi boş olur.</span><span class="sxs-lookup"><span data-stu-id="57071-544">By default the response body will be empty.</span></span> <span data-ttu-id="57071-545">Ancak, varsa `Prefer` istek üstbilgisi olarak ayarlanmış `return=representation`, yanıt gövdesi güncelleştirildi dizin tanımı JSON içerir.</span><span class="sxs-lookup"><span data-stu-id="57071-545">However, if the `Prefer` request header is set to `return=representation`, the response body will contain the JSON for the index definition that was updated.</span></span> <span data-ttu-id="57071-546">Bu durumda, başarı durum kodu olacak "200 Tamam".</span><span class="sxs-lookup"><span data-stu-id="57071-546">In this case, the success status code will be "200 OK".</span></span>

<span data-ttu-id="57071-547">**Dizin tanımı ile özel çözümleyiciler güncelleştiriliyor**</span><span class="sxs-lookup"><span data-stu-id="57071-547">**Updating index definition with custom analyzers**</span></span>

<span data-ttu-id="57071-548">Bir analyzer, bir belirteç Oluşturucu, bir belirteç filtre veya char filtre tanımlandıktan sonra değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="57071-548">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span></span> <span data-ttu-id="57071-549">Yeni bir tane varsa, yalnızca mevcut bir dizine eklenebilir `allowIndexDowntime` bayrağı ayarlanmış dizin güncelleştirme isteğinde doğru:</span><span class="sxs-lookup"><span data-stu-id="57071-549">New ones can be added to an existing index only if the `allowIndexDowntime` flag is set to true in the index update request:</span></span> 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

<span data-ttu-id="57071-550">Bu işlem, dizini çevrimdışı, dizin oluşturma neden en az birkaç saniye ve sorgu isteği başarısız sokar unutmayın.</span><span class="sxs-lookup"><span data-stu-id="57071-550">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests to fail.</span></span> <span data-ttu-id="57071-551">Performans ve yazma kullanılabilirlik dizininin dizin güncelleştirildikten sonra birkaç dakika engelli ya da çok büyük dizinler için daha uzun olabilir.</span><span class="sxs-lookup"><span data-stu-id="57071-551">Performance and write availability of the index can be impaired for several minutes after the index is updated, or longer for very large indexes.</span></span>

<a name="ListIndexes"></a>

## <a name="list-indexes"></a><span data-ttu-id="57071-552">Liste dizinler</span><span class="sxs-lookup"><span data-stu-id="57071-552">List Indexes</span></span>
<span data-ttu-id="57071-553">**Listesi dizinleri** işlemi listesi döndürülür dizinleri şu anda Azure Search hizmetinizin.</span><span class="sxs-lookup"><span data-stu-id="57071-553">The **List Indexes** operation returns a list of the indexes currently in your Azure Search service.</span></span>

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="57071-554">**İstek**</span><span class="sxs-lookup"><span data-stu-id="57071-554">**Request**</span></span>

<span data-ttu-id="57071-555">HTTPS tüm hizmet istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="57071-555">HTTPS is required for all service requests.</span></span> <span data-ttu-id="57071-556">**Listesi dizinleri** isteği GET yöntemini kullanan olacak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="57071-556">The **List Indexes** request can be constructed using the GET method.</span></span>

<span data-ttu-id="57071-557">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="57071-557">`api-version=[string]` (required).</span></span> <span data-ttu-id="57071-558">Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="57071-558">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="57071-559">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="57071-559">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="57071-560">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="57071-560">**Request Headers**</span></span>

<span data-ttu-id="57071-561">Aşağıdaki listede gerekli ve isteğe bağlı İstek üstbilgilerinin açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="57071-561">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="57071-562">`api-key`: Gerekli.</span><span class="sxs-lookup"><span data-stu-id="57071-562">`api-key`: Required.</span></span> <span data-ttu-id="57071-563">`api-key` İsteğin arama hizmetiniz için kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-563">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="57071-564">Hizmetinize benzersiz bir dize değeri değil.</span><span class="sxs-lookup"><span data-stu-id="57071-564">It is a string value, unique to your service.</span></span> <span data-ttu-id="57071-565">**Listesi dizinler** isteği içermelidir bir `api-key` bir yönetici anahtarı (aksine, bir sorgu anahtarı) ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="57071-565">The **List Indexes** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="57071-566">İstek URL'si oluşturmak için hizmet adı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-566">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="57071-567">Hizmet adını alabilir ve `api-key` Azure Portalı'nda, hizmet panosundan.</span><span class="sxs-lookup"><span data-stu-id="57071-567">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="57071-568">Bkz: [portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="57071-568">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="57071-569">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="57071-569">**Request Body**</span></span>

<span data-ttu-id="57071-570">yok.</span><span class="sxs-lookup"><span data-stu-id="57071-570">None.</span></span>

<span data-ttu-id="57071-571">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="57071-571">**Response**</span></span>

<span data-ttu-id="57071-572">Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.</span><span class="sxs-lookup"><span data-stu-id="57071-572">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="57071-573">Bir örnek yanıt gövdesi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="57071-573">Here is an example response body:</span></span>

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

<span data-ttu-id="57071-574">Yalnızca ilgilendiğiniz özellikleri aşağıya doğru yanıt filtreleyebilirsiniz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="57071-574">Note that you can filter the response down to just the properties you're interested in.</span></span> <span data-ttu-id="57071-575">Örneğin, yalnızca dizin adlarının bir listesini istiyorsanız, OData kullanın `$select` sorgu seçeneği:</span><span class="sxs-lookup"><span data-stu-id="57071-575">For example, if you want only a list of index names, use the OData `$select` query option:</span></span>

    GET /indexes?api-version=2015-02-28-Preview&$select=name

<span data-ttu-id="57071-576">Bu durumda, yukarıdaki örnek yanıttan şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="57071-576">In this case, the response from the above example would appear as follows:</span></span>

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

<span data-ttu-id="57071-577">Bu, dizinleri çok arama hizmetiniz varsa, bant genişliğinden tasarruf için yararlı bir tekniktir.</span><span class="sxs-lookup"><span data-stu-id="57071-577">This is a useful technique to save bandwidth if you have a lot of indexes in your Search service.</span></span>

<a name="GetIndex"></a>

## <a name="get-index"></a><span data-ttu-id="57071-578">Dizin Al</span><span class="sxs-lookup"><span data-stu-id="57071-578">Get Index</span></span>
<span data-ttu-id="57071-579">**Alma dizin** işlemi Azure aramadan dizin tanımını alır.</span><span class="sxs-lookup"><span data-stu-id="57071-579">The **Get Index** operation gets the index definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="57071-580">**İstek**</span><span class="sxs-lookup"><span data-stu-id="57071-580">**Request**</span></span>

<span data-ttu-id="57071-581">HTTPS istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="57071-581">HTTPS is required for service requests.</span></span> <span data-ttu-id="57071-582">**Alma dizin** isteği GET yöntemini kullanan olacak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="57071-582">The **Get Index** request can be constructed using the GET method.</span></span>

<span data-ttu-id="57071-583">İstek URI'SİNDEKİ [dizin adı] dizinleri koleksiyondan döndürmek için hangi dizinini belirtir.</span><span class="sxs-lookup"><span data-stu-id="57071-583">The [index name] in the request URI specifies which index to return from the indexes collection.</span></span>

<span data-ttu-id="57071-584">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="57071-584">`api-version=[string]` (required).</span></span> <span data-ttu-id="57071-585">Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="57071-585">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="57071-586">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="57071-586">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="57071-587">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="57071-587">**Request Headers**</span></span>

<span data-ttu-id="57071-588">Aşağıdaki listede gerekli ve isteğe bağlı İstek üstbilgilerinin açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="57071-588">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="57071-589">`api-key``api-key` İsteğin arama hizmetiniz için kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-589">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="57071-590">Hizmetinize benzersiz bir dize değeri değil.</span><span class="sxs-lookup"><span data-stu-id="57071-590">It is a string value, unique to your service.</span></span> <span data-ttu-id="57071-591">**Alma dizin** isteği içermelidir bir `api-key` bir yönetici anahtarı (aksine, bir sorgu anahtarı) ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="57071-591">The **Get Index** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="57071-592">İstek URL'si oluşturmak için hizmet adı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-592">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="57071-593">Hizmet adını alabilir ve `api-key` Azure Portalı'nda, hizmet panosundan.</span><span class="sxs-lookup"><span data-stu-id="57071-593">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="57071-594">Bkz: [portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="57071-594">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="57071-595">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="57071-595">**Request Body**</span></span>

<span data-ttu-id="57071-596">yok.</span><span class="sxs-lookup"><span data-stu-id="57071-596">None.</span></span>

<span data-ttu-id="57071-597">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="57071-597">**Response**</span></span>

<span data-ttu-id="57071-598">Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.</span><span class="sxs-lookup"><span data-stu-id="57071-598">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="57071-599">Örnek JSON içinde [oluşturma ve bir dizin güncelleştirme](#CreateUpdateIndexExample) yanıt yükü ilişkin bir örnek.</span><span class="sxs-lookup"><span data-stu-id="57071-599">See the example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of the response payload.</span></span>

<a name="DeleteIndex"></a>

## <a name="delete-index"></a><span data-ttu-id="57071-600">Dizin Sil</span><span class="sxs-lookup"><span data-stu-id="57071-600">Delete Index</span></span>
<span data-ttu-id="57071-601">**Silmek dizin** işlemi, Azure Search hizmetinizin dizin ve ilişkili belgeleri kaldırır.</span><span class="sxs-lookup"><span data-stu-id="57071-601">The **Delete Index** operation removes an index and associated documents from your Azure Search service.</span></span> <span data-ttu-id="57071-602">Dizin adı Azure portalında hizmet panosundan veya API'sinden elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57071-602">You can get the index name from the service dashboard in the Azure portal, or from the API.</span></span> <span data-ttu-id="57071-603">Bkz: [listesi dizinleri](#ListIndexes) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="57071-603">See [List Indexes](#ListIndexes) for details.</span></span>

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="57071-604">**İstek**</span><span class="sxs-lookup"><span data-stu-id="57071-604">**Request**</span></span>

<span data-ttu-id="57071-605">HTTPS istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="57071-605">HTTPS is required for service requests.</span></span> <span data-ttu-id="57071-606">**Silmek dizin** isteği DELETE yöntemini kullanan olacak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="57071-606">The **Delete Index** request can be constructed using the DELETE method.</span></span>

<span data-ttu-id="57071-607">İstek URI'SİNDEKİ [dizin adı] dizinleri koleksiyonundan silmek için hangi dizinini belirtir.</span><span class="sxs-lookup"><span data-stu-id="57071-607">The [index name] in the request URI specifies which index to delete from the indexes collection.</span></span>

<span data-ttu-id="57071-608">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="57071-608">`api-version=[string]` (required).</span></span> <span data-ttu-id="57071-609">Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="57071-609">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="57071-610">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="57071-610">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="57071-611">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="57071-611">**Request Headers**</span></span>

<span data-ttu-id="57071-612">Aşağıdaki listede gerekli ve isteğe bağlı İstek üstbilgilerinin açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="57071-612">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="57071-613">`api-key`: Gerekli.</span><span class="sxs-lookup"><span data-stu-id="57071-613">`api-key`: Required.</span></span> <span data-ttu-id="57071-614">`api-key` İsteğin arama hizmetiniz için kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-614">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="57071-615">Hizmet URL'nizi benzersiz bir dize değeri değil.</span><span class="sxs-lookup"><span data-stu-id="57071-615">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="57071-616">**Silmek dizin** isteği içermelidir bir `api-key` üstbilgi yönetici anahtarınızı (aksine, bir sorgu anahtarı) ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="57071-616">The **Delete Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="57071-617">İstek URL'si oluşturmak için hizmet adı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-617">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="57071-618">Hizmet adını alabilir ve `api-key` Azure Portalı'nda, hizmet panosundan.</span><span class="sxs-lookup"><span data-stu-id="57071-618">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="57071-619">Bkz: [portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="57071-619">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="57071-620">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="57071-620">**Request Body**</span></span>

<span data-ttu-id="57071-621">yok.</span><span class="sxs-lookup"><span data-stu-id="57071-621">None.</span></span>

<span data-ttu-id="57071-622">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="57071-622">**Response**</span></span>

<span data-ttu-id="57071-623">Durum kodu: 204 Hayır içerik için başarılı bir yanıt döndürülür.</span><span class="sxs-lookup"><span data-stu-id="57071-623">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a><span data-ttu-id="57071-624">Dizin istatistikleri Al</span><span class="sxs-lookup"><span data-stu-id="57071-624">Get Index Statistics</span></span>
<span data-ttu-id="57071-625">**Dizin istatistikleri almak** işlemi, geçerli dizin ek depolama alanı kullanımı için bir belge sayısı Azure aramadan döndürür.</span><span class="sxs-lookup"><span data-stu-id="57071-625">The **Get Index Statistics** operation returns from Azure Search a document count for the current index, plus storage usage.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="57071-626">Belge sayısını ve depolama boyutunu istatistiklerle değil gerçek zamanlı olarak birkaç dakikada toplanır.</span><span class="sxs-lookup"><span data-stu-id="57071-626">Statistics on document count and storage size are collected every few minutes, not in real time.</span></span> <span data-ttu-id="57071-627">Bu nedenle, bu API tarafından döndürülen istatistikleri son dizin oluşturma işlemleri tarafından yapılan değişiklikler neden yansıtmayabilir.</span><span class="sxs-lookup"><span data-stu-id="57071-627">Therefore, the statistics returned by this API may not reflect changes caused by recent indexing operations.</span></span>
> 
> 

<span data-ttu-id="57071-628">**İstek**</span><span class="sxs-lookup"><span data-stu-id="57071-628">**Request**</span></span>

<span data-ttu-id="57071-629">HTTPS tüm hizmetleri istekler için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="57071-629">HTTPS is required for all services requests.</span></span> <span data-ttu-id="57071-630">**Dizin istatistikleri almak** isteği GET yöntemini kullanan olacak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="57071-630">The **Get Index Statistics** request can be constructed using the GET method.</span></span>

<span data-ttu-id="57071-631">İstek URI'SİNDEKİ [dizin adı] belirtilen dizin için dizin istatistiği hizmete bildirir.</span><span class="sxs-lookup"><span data-stu-id="57071-631">The [index name] in the request URI tells the service to return index statistics for the specified index.</span></span>

<span data-ttu-id="57071-632">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="57071-632">`api-version=[string]` (required).</span></span> <span data-ttu-id="57071-633">Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="57071-633">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="57071-634">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="57071-634">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="57071-635">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="57071-635">**Request Headers**</span></span>

<span data-ttu-id="57071-636">Aşağıdaki listede gerekli ve isteğe bağlı İstek üstbilgilerinin açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="57071-636">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="57071-637">`api-key``api-key` İsteğin arama hizmetiniz için kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-637">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="57071-638">Hizmetinize benzersiz bir dize değeri değil.</span><span class="sxs-lookup"><span data-stu-id="57071-638">It is a string value, unique to your service.</span></span> <span data-ttu-id="57071-639">**Dizin istatistikleri almak** isteği içermelidir bir `api-key` bir yönetici anahtarı (aksine, bir sorgu anahtarı) ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="57071-639">The **Get Index Statistics** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="57071-640">İstek URL'si oluşturmak için hizmet adı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-640">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="57071-641">Hizmet adını alabilir ve `api-key` Azure Portalı'nda, hizmet panosundan.</span><span class="sxs-lookup"><span data-stu-id="57071-641">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="57071-642">Bkz: [portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="57071-642">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="57071-643">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="57071-643">**Request Body**</span></span>

<span data-ttu-id="57071-644">yok.</span><span class="sxs-lookup"><span data-stu-id="57071-644">None.</span></span>

<span data-ttu-id="57071-645">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="57071-645">**Response**</span></span>

<span data-ttu-id="57071-646">Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.</span><span class="sxs-lookup"><span data-stu-id="57071-646">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="57071-647">Yanıt gövdesi aşağıdaki biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="57071-647">The response body is in the following format:</span></span>

    {
      "documentCount": number,
      "storageSize": number (size of the index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a><span data-ttu-id="57071-648">Testi Çözümleyicisi</span><span class="sxs-lookup"><span data-stu-id="57071-648">Test Analyzer</span></span>
<span data-ttu-id="57071-649">**Analiz API** nasıl bir Çözümleyicisi belirteçlere metni keser. gösterir.</span><span class="sxs-lookup"><span data-stu-id="57071-649">The **Analyze API** shows how an analyzer breaks text into tokens.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="57071-650">**İstek**</span><span class="sxs-lookup"><span data-stu-id="57071-650">**Request**</span></span>

<span data-ttu-id="57071-651">HTTPS tüm hizmetleri istekler için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="57071-651">HTTPS is required for all services requests.</span></span> <span data-ttu-id="57071-652">**Analiz API** isteği POST yöntemini kullanan olacak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="57071-652">The **Analyze API** request can be constructed using the POST method.</span></span>

<span data-ttu-id="57071-653">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="57071-653">`api-version=[string]` (required).</span></span> <span data-ttu-id="57071-654">Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="57071-654">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="57071-655">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="57071-655">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="57071-656">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="57071-656">**Request Headers**</span></span>

<span data-ttu-id="57071-657">Aşağıdaki listede gerekli ve isteğe bağlı İstek üstbilgilerinin açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="57071-657">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="57071-658">`api-key``api-key` İsteğin arama hizmetiniz için kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-658">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="57071-659">Hizmetinize benzersiz bir dize değeri değil.</span><span class="sxs-lookup"><span data-stu-id="57071-659">It is a string value, unique to your service.</span></span> <span data-ttu-id="57071-660">**Analiz API** isteği içermelidir bir `api-key` bir yönetici anahtarı (aksine, bir sorgu anahtarı) ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="57071-660">The **Analyze API** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="57071-661">Dizin adı ve istek URL'si oluşturmak için hizmet adı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-661">You will also need the index name and the service name to construct the request URL.</span></span> <span data-ttu-id="57071-662">Hizmet adını alabilir ve `api-key` Azure Portalı'nda, hizmet panosundan.</span><span class="sxs-lookup"><span data-stu-id="57071-662">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="57071-663">Bkz: [portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="57071-663">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="57071-664">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="57071-664">**Request Body**</span></span>

    {
      "text": "Text to analyze",
      "analyzer": "analyzer_name"
    }

<span data-ttu-id="57071-665">or</span><span class="sxs-lookup"><span data-stu-id="57071-665">or</span></span>

    {
      "text": "Text to analyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

<span data-ttu-id="57071-666">`analyzer_name`, `tokenizer_name`, `token_filter_name` Ve `char_filter_name` önceden tanımlanmış veya özel çözümleyiciler, tokenizers, belirteç filtreleri ve char filtreleri dizini için geçerli adlar olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-666">The `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need to be valid names of predefined or custom analyzers, tokenizers, token filters and char filters for the index.</span></span> <span data-ttu-id="57071-667">Sözcük çözümleme işlemi hakkında daha fazla bilgi için [analiz Azure Search'te](https://aka.ms/azsanalysis).</span><span class="sxs-lookup"><span data-stu-id="57071-667">To learn more about the process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span></span>

<span data-ttu-id="57071-668">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="57071-668">**Response**</span></span>

<span data-ttu-id="57071-669">Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.</span><span class="sxs-lookup"><span data-stu-id="57071-669">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="57071-670">Yanıt gövdesi aşağıdaki biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="57071-670">The response body is in the following format:</span></span>

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of the first character of the token),
          "endOffset": number (index of the last character of the token),
          "position": number (position of the token in the input text)
        },
        ...
      ]
    }

<span data-ttu-id="57071-671">**API örnek Çözümle**</span><span class="sxs-lookup"><span data-stu-id="57071-671">**Analyze API example**</span></span>

<span data-ttu-id="57071-672">**İstek**</span><span class="sxs-lookup"><span data-stu-id="57071-672">**Request**</span></span>

    {
      "text": "Text to analyze",
      "analyzer": "standard"
    }

<span data-ttu-id="57071-673">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="57071-673">**Response**</span></span>

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

## <a name="document-operations"></a><span data-ttu-id="57071-674">Belge işlemleri</span><span class="sxs-lookup"><span data-stu-id="57071-674">Document Operations</span></span>
<span data-ttu-id="57071-675">Azure Search'te bir dizine bulutta depolanan ve hizmete karşıya JSON belgelerini kullanarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="57071-675">In Azure Search, an index is stored in the cloud and populated using JSON documents that you upload to the service.</span></span> <span data-ttu-id="57071-676">Karşıya yüklediğiniz tüm belgeleri arama verilerinizi gövde kapsar.</span><span class="sxs-lookup"><span data-stu-id="57071-676">All the documents that you upload comprise the corpus of your search data.</span></span> <span data-ttu-id="57071-677">Belgeleri karşıya gibi bazıları arama terimleri simgeleştirilmiş alanlar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="57071-677">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span></span> <span data-ttu-id="57071-678">`/docs` Azure Search API URL kesimi dizini belgelerde koleksiyonunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="57071-678">The `/docs` URL segment in the Azure Search API represents the collection of documents in an index.</span></span> <span data-ttu-id="57071-679">Karşıya yükleme gibi koleksiyon üzerinde gerçekleştirilen tüm işlemler birleştirme, silme veya belgeleri Al sorgulama yerleştirin bağlamında tek bir dizin, bu nedenle URL'leri bu işlemlerin her zaman ile başlar için `/indexes/[index name]/docs` için belirtilen dizin adı.</span><span class="sxs-lookup"><span data-stu-id="57071-679">All operations performed on the collection such as uploading, merging, deleting, or querying documents take place in the context of a single index, so the URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span></span>

<span data-ttu-id="57071-680">Uygulama kodunuz için Azure Search karşıya yüklemek için JSON belgeleri ya da oluşturmanız gerekir veya kullanabileceğiniz bir [dizin oluşturucu](https://msdn.microsoft.com/library/dn946891.aspx) veri kaynağı Azure SQL Database veya Azure Cosmos DB ise belgeleri yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="57071-680">Your application code must either generate JSON documents to upload to Azure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) to load documents if the data source is either Azure SQL Database or Azure Cosmos DB.</span></span> <span data-ttu-id="57071-681">Genellikle, dizinleri sağlayan bir tek veri kümesinden doldurulur.</span><span class="sxs-lookup"><span data-stu-id="57071-681">Typically, indexes are populated from a single dataset that you provide.</span></span>

<span data-ttu-id="57071-682">Arama yapmak istediğiniz her bir öğe için bir belge sahip planlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-682">You should plan on having one document for each item that you want to search.</span></span> <span data-ttu-id="57071-683">Film kiralama uygulamasının film başına tek bir belgenin olabilir, bir mağaza uygulaması SKU başına tek bir belgenin olabilir, bir çevrimiçi eğitim malzemesi uygulamasının indirmelere başına tek bir belgenin olabilir, araştırma kesin bir belgeyi her akademik kağıt olabilir kendi Depo ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="57071-683">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span></span>

<span data-ttu-id="57071-684">Belgeler bir veya daha fazla alan oluşur.</span><span class="sxs-lookup"><span data-stu-id="57071-684">Documents consist of one or more fields.</span></span> <span data-ttu-id="57071-685">Alanları Azure Search tarafından arama terimleri simgeleştirilmiş yanı sıra dışı simgeleştirilmiş metin veya filtreleri veya Puanlama profilleri kullanılabilir metin dışı değerleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="57071-685">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span></span> <span data-ttu-id="57071-686">Adları, veri türleri ve her bir alan için desteklenen arama özellikleri, dizin şemasına göre belirlenir.</span><span class="sxs-lookup"><span data-stu-id="57071-686">The names, data types, and search features supported for each field are determined by the index schema.</span></span> <span data-ttu-id="57071-687">Her dizin şemasında alanlardan biri bir kimliği olarak işaretlenmesi gerekir ve her bir belgenin bu belge dizini içinde benzersiz olarak tanıtan ID alanı için bir değer olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-687">One of the fields in each index schema must be designated as an ID, and each document must have a value for the ID field that uniquely identifies that document in the index.</span></span> <span data-ttu-id="57071-688">Diğer tüm belge alanlarını isteğe bağlıdır ve sol belirtilmezse bir null değeri varsayılan olarak alır.</span><span class="sxs-lookup"><span data-stu-id="57071-688">All other document fields are optional and will default to a null value if left unspecified.</span></span> <span data-ttu-id="57071-689">Null değerler arama dizini yer almayan unutmayın.</span><span class="sxs-lookup"><span data-stu-id="57071-689">Note that null values do not take up space in the search index.</span></span>

<span data-ttu-id="57071-690">Belgeleri yüklemeden önce dizin hizmeti oluşturmuş olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="57071-690">Before you can upload documents, you must have already created the index on the service.</span></span> <span data-ttu-id="57071-691">Bkz: [Create Index](#CreateIndex) birinci adım hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="57071-691">See [Create Index](#CreateIndex) for details about this first step.</span></span>

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a><span data-ttu-id="57071-692">Ekleme, güncelleştirme, belgeleri veya silme</span><span class="sxs-lookup"><span data-stu-id="57071-692">Add, Update, or Delete Documents</span></span>
<span data-ttu-id="57071-693">Karşıya yüklediğiniz, HTTP POST kullanılarak belirtilen bir dizinden birleştirme, birleştirme veya karşıya yükleme veya delete belgeleri.</span><span class="sxs-lookup"><span data-stu-id="57071-693">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span> <span data-ttu-id="57071-694">Güncelleştirmeler için çok sayıda (toplu iş başına 1000 belge) veya toplu iş başına yaklaşık 16 MB kadar belgelerin toplu işleme önerilir.</span><span class="sxs-lookup"><span data-stu-id="57071-694">For large numbers of updates, batching of documents (up to 1000 documents per batch or about 16 MB per batch) is recommended.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="57071-695">**İstek**</span><span class="sxs-lookup"><span data-stu-id="57071-695">**Request**</span></span>

<span data-ttu-id="57071-696">HTTPS tüm hizmet istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="57071-696">HTTPS is required for all service requests.</span></span> <span data-ttu-id="57071-697">Karşıya yüklediğiniz, HTTP POST kullanılarak belirtilen bir dizinden birleştirme, birleştirme veya karşıya yükleme veya delete belgeleri.</span><span class="sxs-lookup"><span data-stu-id="57071-697">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span>

<span data-ttu-id="57071-698">İstek URI'si [dizin adı] içeren belgeleri gönderme hangi dizin belirtme.</span><span class="sxs-lookup"><span data-stu-id="57071-698">The request URI includes [index name], specifying which index to post documents.</span></span> <span data-ttu-id="57071-699">Bu gibi durumlarda, bir dizin belgelere yalnızca aynı anda nakledebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57071-699">You can only post documents to one index at a time.</span></span>

<span data-ttu-id="57071-700">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="57071-700">`api-version=[string]` (required).</span></span> <span data-ttu-id="57071-701">Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="57071-701">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="57071-702">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="57071-702">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="57071-703">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="57071-703">**Request Headers**</span></span>

<span data-ttu-id="57071-704">Aşağıdaki listede gerekli ve isteğe bağlı İstek üstbilgilerinin açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="57071-704">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="57071-705">`Content-Type`: Gerekli.</span><span class="sxs-lookup"><span data-stu-id="57071-705">`Content-Type`: Required.</span></span> <span data-ttu-id="57071-706">Bu ayar`application/json`</span><span class="sxs-lookup"><span data-stu-id="57071-706">Set this to `application/json`</span></span>
* <span data-ttu-id="57071-707">`api-key`: Gerekli.</span><span class="sxs-lookup"><span data-stu-id="57071-707">`api-key`: Required.</span></span> <span data-ttu-id="57071-708">`api-key` İsteğin arama hizmetiniz için kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-708">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="57071-709">Hizmetinize benzersiz bir dize değeri değil.</span><span class="sxs-lookup"><span data-stu-id="57071-709">It is a string value, unique to your service.</span></span> <span data-ttu-id="57071-710">**Ekleme belgeleri** isteği içermelidir bir `api-key` üstbilgi yönetici anahtarınızı (aksine, bir sorgu anahtarı) ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="57071-710">The **Add Documents** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="57071-711">İstek URL'si oluşturmak için hizmet adı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-711">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="57071-712">Hizmet adını alabilir ve `api-key` Azure Portalı'nda, hizmet panosundan.</span><span class="sxs-lookup"><span data-stu-id="57071-712">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="57071-713">Bkz: [portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="57071-713">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="57071-714">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="57071-714">**Request Body**</span></span>

<span data-ttu-id="57071-715">İstek gövdesini dizine alınacak bir veya daha fazla belgeler içerir.</span><span class="sxs-lookup"><span data-stu-id="57071-715">The body of the request contains one or more documents to be indexed.</span></span> <span data-ttu-id="57071-716">Belgeler, benzersiz bir anahtar tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="57071-716">Documents are identified by a unique key.</span></span> <span data-ttu-id="57071-717">Her bir eylem ile ilişkili bir belgedir: karşıya yükleme, birleştirme, mergeOrUpload veya Sil.</span><span class="sxs-lookup"><span data-stu-id="57071-717">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span></span> <span data-ttu-id="57071-718">Karşıya yükleme istekleri belge verileri anahtar/değer çiftleri kümesi olarak eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-718">Upload requests must include the document data as a set of key/value pairs.</span></span>

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
> <span data-ttu-id="57071-719">Belge anahtarları yalnızca harf, sayı, kısa çizgi içerebilir ("-"), alt çizgi ("_") ve eşittir işareti ("=").</span><span class="sxs-lookup"><span data-stu-id="57071-719">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span></span> <span data-ttu-id="57071-720">Daha fazla ayrıntı için bkz: [adlandırma kurallarını](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span><span class="sxs-lookup"><span data-stu-id="57071-720">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span></span>
> 
> 

<span data-ttu-id="57071-721">**Belge eylemleri**</span><span class="sxs-lookup"><span data-stu-id="57071-721">**Document Actions**</span></span>

* <span data-ttu-id="57071-722">`upload`: Bir karşıya yükleme eylem varsa, yeni ve güncelleştirilmiş/değiştirileceği ise belge ekleneceği bir "upsert" benzer.</span><span class="sxs-lookup"><span data-stu-id="57071-722">`upload`: An upload action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> <span data-ttu-id="57071-723">Tüm alanları güncelleştirme durumda yerini aldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="57071-723">Note that all fields are replaced in the update case.</span></span>
* <span data-ttu-id="57071-724">`merge`: Birleştirme var olan bir belgeyi belirtilen alanlarla güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="57071-724">`merge`: Merge updates an existing document with the specified fields.</span></span> <span data-ttu-id="57071-725">Belge mevcut değilse birleştirme işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="57071-725">If the document doesn't exist, the merge will fail.</span></span> <span data-ttu-id="57071-726">Birleştirmede belirttiğiniz herhangi bir alan belgede var olan alanın yerini alır.</span><span class="sxs-lookup"><span data-stu-id="57071-726">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="57071-727">Buna `Collection(Edm.String)` türünde alanlar dahildir.</span><span class="sxs-lookup"><span data-stu-id="57071-727">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="57071-728">Örneğin, belgeyi bir alan değeri olan "etiketler" içeriyorsa `["budget"]` ve değeriyle bir birleştirme yürütme `["economy", "pool"]` "etiketleri", "etiketler" alanının son değeri olacaktır `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="57071-728">For example, if the document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", the final value of the "tags" field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="57071-729">İçinde **değil** olması `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="57071-729">It will **not** be `["budget", "economy", "pool"]`.</span></span>
* <span data-ttu-id="57071-730">`mergeOrUpload`: gibi davranır `merge` belirtilen anahtara sahip bir belge dizinde zaten mevcutsa.</span><span class="sxs-lookup"><span data-stu-id="57071-730">`mergeOrUpload`: behaves like `merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="57071-731">Belge mevcut değilse gibi davranır `upload` yeni bir belgeyle.</span><span class="sxs-lookup"><span data-stu-id="57071-731">If the document does not exist it behaves like `upload` with a new document.</span></span>
* <span data-ttu-id="57071-732">`delete`: Delete belirtilen belgeyi dizinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="57071-732">`delete`: Delete removes the specified document from the index.</span></span> <span data-ttu-id="57071-733">Belirttiğiniz tüm alanlar içinde olduğunu unutmayın bir `delete` işlemi anahtar alanı dışında yok sayılacak.</span><span class="sxs-lookup"><span data-stu-id="57071-733">Note that any fields you specify in a `delete` operation other than the key field will be ignored.</span></span> <span data-ttu-id="57071-734">Bir belgeden tek bir alanı kaldırmak istiyorsanız, kullanmak `merge` yeterlidir ve bunun yerine alanını açıkça ayarlayın `null`.</span><span class="sxs-lookup"><span data-stu-id="57071-734">If you want to remove an individual field from a document, use `merge` instead and simply set the field explicitly to `null`.</span></span>

<span data-ttu-id="57071-735">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="57071-735">**Response**</span></span>

<span data-ttu-id="57071-736">Durum kodu 200 (Tamam) tüm öğeleri başarıyla eklenmemiş anlamı başarılı bir yanıt için döndürülür.</span><span class="sxs-lookup"><span data-stu-id="57071-736">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span></span> <span data-ttu-id="57071-737">Bu belirtilir `status` özelliği ayarlanıyor tüm öğeleri de için true olarak `statusCode` 201 (için yeni yüklenen belgeleri için) veya 200 (için birleştirilmiş veya Silinen Belge) ayarlanan özelliği:</span><span class="sxs-lookup"><span data-stu-id="57071-737">This is indicated by the `status` property being set to true for all items, as well as the `statusCode` property being set to either 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span></span>

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

<span data-ttu-id="57071-738">En az bir öğenin dizine alınması başarısız olduğunda 207 (çok durumu) durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="57071-738">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="57071-739">Dizine öğeleriniz `status` alanını false olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="57071-739">Items that have not been indexed have the `status` field set to false.</span></span> <span data-ttu-id="57071-740">`errorMessage` Ve `statusCode` özellikleri dizin hatanın nedenini gösterir:</span><span class="sxs-lookup"><span data-stu-id="57071-740">The `errorMessage` and `statusCode` properties will indicate the reason for the indexing error:</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "The search service is too busy to process this document. Please try again later.",
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
          "errorMessage": "Index is temporarily unavailable because it was updated with the 'allowIndexDowntime' flag set to 'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

<span data-ttu-id="57071-741">Aşağıdaki tabloda yanıtta döndürülen çeşitli belge başına durum kodları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="57071-741">The following table explains the various per-document status codes that can be returned in the response.</span></span> <span data-ttu-id="57071-742">Başkalarının geçici hata koşulları belirtmek karşın bazı sorunları isteği kendisi ile olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="57071-742">Note that some indicate problems with the request itself, while others indicate temporary error conditions.</span></span> <span data-ttu-id="57071-743">İkinci bir gecikmeden sonra yeniden denemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-743">The latter you should retry after a delay.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="57071-744">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="57071-744">Status code</span></span></th>
        <th><span data-ttu-id="57071-745">Anlamı</span><span class="sxs-lookup"><span data-stu-id="57071-745">Meaning</span></span></th>
        <th><span data-ttu-id="57071-746">Yeniden denenebilir</span><span class="sxs-lookup"><span data-stu-id="57071-746">Retryable</span></span></th>
        <th><span data-ttu-id="57071-747">Notlar</span><span class="sxs-lookup"><span data-stu-id="57071-747">Notes</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-748">200</span><span class="sxs-lookup"><span data-stu-id="57071-748">200</span></span></td>
        <td><span data-ttu-id="57071-749">Belge başarıyla değiştirilmiş veya silinmiş.</span><span class="sxs-lookup"><span data-stu-id="57071-749">Document was successfully modified or deleted.</span></span></td>
        <td><span data-ttu-id="57071-750">yok</span><span class="sxs-lookup"><span data-stu-id="57071-750">n/a</span></span></td>
        <td><span data-ttu-id="57071-751">Silme işlemlerine olan <a href="https://en.wikipedia.org/wiki/Idempotence">ıdempotent</a>.</span><span class="sxs-lookup"><span data-stu-id="57071-751">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span> <span data-ttu-id="57071-752">Diğer bir deyişle, bir belge anahtarı dizinde mevcut değilse, bu anahtara sahip bir silme işlemini denemeden 200 durum koduna neden olur.</span><span class="sxs-lookup"><span data-stu-id="57071-752">That is, even if a document key does not exist in the index, attempting a delete operation with that key will result in a 200 status code.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-753">201</span><span class="sxs-lookup"><span data-stu-id="57071-753">201</span></span></td>
        <td><span data-ttu-id="57071-754">Belge başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="57071-754">Document was successfully created.</span></span></td>
        <td><span data-ttu-id="57071-755">yok</span><span class="sxs-lookup"><span data-stu-id="57071-755">n/a</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-756">400</span><span class="sxs-lookup"><span data-stu-id="57071-756">400</span></span></td>
        <td><span data-ttu-id="57071-757">Belgedeki dizine alınmasını engelleyen bir hata vardı.</span><span class="sxs-lookup"><span data-stu-id="57071-757">There was an error in the document that prevented it from being indexed.</span></span></td>
        <td><span data-ttu-id="57071-758">Hayır</span><span class="sxs-lookup"><span data-stu-id="57071-758">No</span></span></td>
        <td><span data-ttu-id="57071-759">Yanıt hata iletisinde belgeyle nerede olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="57071-759">The error message in the response will indicate what is wrong with the document.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-760">404</span><span class="sxs-lookup"><span data-stu-id="57071-760">404</span></span></td>
        <td><span data-ttu-id="57071-761">Verilen anahtar dizininde mevcut olmadığından belge birleştirilemeyen.</span><span class="sxs-lookup"><span data-stu-id="57071-761">The document could not be merged because the given key doesn't exist in the index.</span></span></td>
        <td><span data-ttu-id="57071-762">Hayır</span><span class="sxs-lookup"><span data-stu-id="57071-762">No</span></span></td>
        <td><span data-ttu-id="57071-763">Bu hata yüklemeler için yeni belgeler oluşturma ve olduklarından silme işlemi için oluşmaz oluşmaz <a href="https://en.wikipedia.org/wiki/Idempotence">ıdempotent</a>.</span><span class="sxs-lookup"><span data-stu-id="57071-763">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-764">409</span><span class="sxs-lookup"><span data-stu-id="57071-764">409</span></span></td>
        <td><span data-ttu-id="57071-765">Bir belge dizin çalışılırken bir sürüm çakışması algılandı.</span><span class="sxs-lookup"><span data-stu-id="57071-765">A version conflict was detected when attempting to index a document.</span></span></td>
        <td><span data-ttu-id="57071-766">Evet</span><span class="sxs-lookup"><span data-stu-id="57071-766">Yes</span></span></td>
        <td><span data-ttu-id="57071-767">Bu durum, birden çok kez aynı anda aynı belge dizini oluşturmak çalıştığınız ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="57071-767">This can happen when you're trying to index the same document more than once concurrently.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-768">422</span><span class="sxs-lookup"><span data-stu-id="57071-768">422</span></span></td>
        <td><span data-ttu-id="57071-769">'AllowIndexDowntime' bayrağı 'true' olarak ayarlanmış güncelleştirilmediğinden dizin geçici olarak kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="57071-769">The index is temporarily unavailable because it was updated with the 'allowIndexDowntime' flag set to 'true'.</span></span></td>
        <td><span data-ttu-id="57071-770">Evet</span><span class="sxs-lookup"><span data-stu-id="57071-770">Yes</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="57071-771">503</span><span class="sxs-lookup"><span data-stu-id="57071-771">503</span></span></td>
        <td><span data-ttu-id="57071-772">Arama hizmetinizi büyük olasılıkla ağır yük nedeniyle geçici olarak kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="57071-772">Your search service is temporarily unavailable, possibly due to heavy load.</span></span></td>
        <td><span data-ttu-id="57071-773">Evet</span><span class="sxs-lookup"><span data-stu-id="57071-773">Yes</span></span></td>
        <td><span data-ttu-id="57071-774">Kodunuzu bu durumda yeniden denemeden önce beklemesi gereken veya hizmet olmadığından uzatma risk.</span><span class="sxs-lookup"><span data-stu-id="57071-774">Your code should wait before retrying in this case or you risk prolonging the service unavailability.</span></span></td>
    </tr>
</table> 

<span data-ttu-id="57071-775">**Not**: istemci kodunuzun sık 207 yanıtı karşılaşırsa, olası bir nedeni sistem yük altında olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-775">**Note**: If your client code frequently encounters a 207 response, one possible reason is that the system is under load.</span></span> <span data-ttu-id="57071-776">Bu denetleyerek doğrulayabilirsiniz `statusCode` 503 özelliği.</span><span class="sxs-lookup"><span data-stu-id="57071-776">You can confirm this by checking the `statusCode` property for 503.</span></span> <span data-ttu-id="57071-777">Bu durumda olup olmadığını, öneririz ***dizin oluşturma isteklerinin azaltma***.</span><span class="sxs-lookup"><span data-stu-id="57071-777">If this is the case, we recommend ***throttling indexing requests***.</span></span> <span data-ttu-id="57071-778">Aksi durumda, trafik dizin subside değil, sistem 503 hataları olan tüm istekleri reddetme başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57071-778">Otherwise, if indexing traffic doesn't subside, the system could start rejecting all requests with 503 errors.</span></span>

<span data-ttu-id="57071-779">Durum kodu 429 dizin başına belge sayısı Kotanızı aştınız gösterir.</span><span class="sxs-lookup"><span data-stu-id="57071-779">Status code 429 indicates that you have exceeded your quota on the number of documents per index.</span></span> <span data-ttu-id="57071-780">Yeni bir dizin oluşturabilir veya için daha yüksek kapasite limitlerini yükseltin.</span><span class="sxs-lookup"><span data-stu-id="57071-780">You must either create a new index or upgrade for higher capacity limits.</span></span>

<span data-ttu-id="57071-781">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="57071-781">**Example:**</span></span>

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

## <a name="search-documents"></a><span data-ttu-id="57071-782">Belge ara</span><span class="sxs-lookup"><span data-stu-id="57071-782">Search Documents</span></span>
<span data-ttu-id="57071-783">A **arama** işlemi bir GET veya POST talebi olarak verilir ve eşleşen belgeleri seçmek için ölçüt vermek parametreleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="57071-783">A **Search** operation is issued as a GET or POST request and specifies parameters that give the criteria for selecting matching documents.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="57071-784">**POST yerine GET kullanma zamanı**</span><span class="sxs-lookup"><span data-stu-id="57071-784">**When to use POST instead of GET**</span></span>

<span data-ttu-id="57071-785">Kullandığınızda, HTTP GET çağırmak için **arama** API, gereken isteği URL uzunluğu 8 KB'yi aşamaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="57071-785">When you use HTTP GET to call the **Search** API, you need to be aware that the length of the request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="57071-786">Çoğu uygulama için yeterince genellikle budur.</span><span class="sxs-lookup"><span data-stu-id="57071-786">This is usually enough for most applications.</span></span> <span data-ttu-id="57071-787">Ancak, bazı uygulamalar çok büyük sorgular veya OData filtre ifadeleri üretir.</span><span class="sxs-lookup"><span data-stu-id="57071-787">However, some applications produce very large queries or OData filter expressions.</span></span> <span data-ttu-id="57071-788">Daha büyük filtreleri ve sorguları get'ten sağladığından bu uygulamalar için HTTP POST kullanılarak daha iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="57071-788">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span></span> <span data-ttu-id="57071-789">POST ile koşulları veya bir sorgu yan tümcelerinde sayısını sınırlama, POST isteği boyut sınırını yaklaşık 16 MB olduğundan ham sorgu boyutu faktördür.</span><span class="sxs-lookup"><span data-stu-id="57071-789">With POST, the number of terms or clauses in a query is the limiting factor, not the size of the raw query since the request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-790">POST isteği boyut sınırı çok büyük olsa bile arama sorguları ve filtre ifadeleri rasgele karmaşık olamaz.</span><span class="sxs-lookup"><span data-stu-id="57071-790">Even though the POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="57071-791">Bkz: [Lucene sorgu söz dizimi](https://msdn.microsoft.com/library/mt589323.aspx) ve [OData ifade sözdizimini](https://msdn.microsoft.com/library/dn798921.aspx) arama sorgusu ve filtre karmaşıklık sınırlamalar hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="57071-791">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="57071-792">**İstek**</span><span class="sxs-lookup"><span data-stu-id="57071-792">**Request**</span></span>

<span data-ttu-id="57071-793">HTTPS istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="57071-793">HTTPS is required for service requests.</span></span> <span data-ttu-id="57071-794">**Arama** isteği GET veya POST yöntemleri kullanılarak olacak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="57071-794">The **Search** request can be constructed using the GET or POST methods.</span></span>

<span data-ttu-id="57071-795">İsteğin URI sorgu parametreleri eşleşen tüm belgeler için hangi dizine belirtir.</span><span class="sxs-lookup"><span data-stu-id="57071-795">The request URI specifies which index to query, for all documents that match the parameters.</span></span> <span data-ttu-id="57071-796">Parametreleri GET istekleri durumunda sorgu dizesinde belirtilen ve gövde POST söz konusu olduğunda istek ister.</span><span class="sxs-lookup"><span data-stu-id="57071-796">Parameters are specified on the query string in the case of GET requests, and in the request body in the case of POST requests.</span></span>

<span data-ttu-id="57071-797">GET isteklerini oluştururken en iyi uygulama, unutmayın [URL kodlama](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) REST API doğrudan çağrılırken belirli sorgu parametreleri.</span><span class="sxs-lookup"><span data-stu-id="57071-797">As a best practice when creating GET requests, remember to [URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling the REST API directly.</span></span> <span data-ttu-id="57071-798">İçin **arama** bu işlemleri içerir:</span><span class="sxs-lookup"><span data-stu-id="57071-798">For **Search** operations, this includes:</span></span>

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

<span data-ttu-id="57071-799">URL kodlaması yalnızca yukarıdaki sorgu parametreleri önerilir.</span><span class="sxs-lookup"><span data-stu-id="57071-799">URL encoding is only recommended on the above query parameters.</span></span> <span data-ttu-id="57071-800">Varsa, yanlışlıkla URL kodlama tüm sorgu dizesi (sonra her şeyi?), istekleri bozar.</span><span class="sxs-lookup"><span data-stu-id="57071-800">If you inadvertently URL-encode the entire query string (everything after the ?), requests will break.</span></span>

<span data-ttu-id="57071-801">Ayrıca, URL kodlaması yalnızca GET kullanarak doğrudan REST API çağrılırken gereklidir.</span><span class="sxs-lookup"><span data-stu-id="57071-801">Also, URL encoding is only necessary when calling the REST API directly using GET.</span></span> <span data-ttu-id="57071-802">Hiçbir URL kodlaması çağrılırken gereklidir **arama** POST, kullanma ya da kullanırken [.NET istemci kitaplığını](https://msdn.microsoft.com/library/dn951165.aspx), sizin için URL kodlaması işler.</span><span class="sxs-lookup"><span data-stu-id="57071-802">No URL encoding is necessary when calling **Search** using POST, or when using the [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="57071-803"><a name="SearchQueryParameters"></a>
**Sorgu parametreleri**</span><span class="sxs-lookup"><span data-stu-id="57071-803"><a name="SearchQueryParameters"></a>
**Query Parameters**</span></span>

<span data-ttu-id="57071-804">**Arama** sorgu ölçütlerini sağlayan ve ayrıca arama davranışını belirtin birkaç parametre kabul eder.</span><span class="sxs-lookup"><span data-stu-id="57071-804">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="57071-805">Bu parametreler URL'deki sorgu dizesi çağrılırken sağladığınız **arama** GET aracılığıyla ve çağrılırken istek gövdesinde JSON özellikleri olarak **arama** POST ile.</span><span class="sxs-lookup"><span data-stu-id="57071-805">You provide these parameters in the URL query string when calling **Search** via GET, and as JSON properties in the request body when calling **Search** via POST.</span></span> <span data-ttu-id="57071-806">Bazı parametreler sözdizimi GET ve POST arasında biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-806">The syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="57071-807">Bu farklılıklar, geçerli aşağıda belirtilmiştir:</span><span class="sxs-lookup"><span data-stu-id="57071-807">These differences are noted as applicable below:</span></span>

<span data-ttu-id="57071-808">`search=[string]`(isteğe bağlı) - Aranacak metin.</span><span class="sxs-lookup"><span data-stu-id="57071-808">`search=[string]` (optional) - The text to search for.</span></span> <span data-ttu-id="57071-809">Tüm `searchable` sürece alanları varsayılan olarak aranır `searchFields` belirtilir.</span><span class="sxs-lookup"><span data-stu-id="57071-809">All `searchable` fields are searched by default unless `searchFields` is specified.</span></span> <span data-ttu-id="57071-810">Arama yaparken `searchable` alanları, arama metni simgeleştirilmiş, birden çok koşulları boşluk ile ayrılabilir şekilde (örneğin: `search=hello world`).</span><span class="sxs-lookup"><span data-stu-id="57071-810">When searching `searchable` fields, the search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span></span> <span data-ttu-id="57071-811">Her terim eşleştirmek için kullanın `*` (Boole filtresi sorgular için yararlı olabilir).</span><span class="sxs-lookup"><span data-stu-id="57071-811">To match any term, use `*` (this can be useful for boolean filter queries).</span></span> <span data-ttu-id="57071-812">Bu parametrenin atlanması ayarı aynı etkiye sahip `*`.</span><span class="sxs-lookup"><span data-stu-id="57071-812">Omitting this parameter has the same effect as setting it to `*`.</span></span> <span data-ttu-id="57071-813">Bkz: [Basit Sorgu söz dizimi](https://msdn.microsoft.com/library/dn798920.aspx) arama söz dizimi üzerinde özellikleri için.</span><span class="sxs-lookup"><span data-stu-id="57071-813">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on the search syntax.</span></span>

* <span data-ttu-id="57071-814">**Not**: sonuçları bazen üzerinden sorgulanırken şaşırtıcı olabilir `searchable` alanları.</span><span class="sxs-lookup"><span data-stu-id="57071-814">**Note**: The results can sometimes be surprising when querying over `searchable` fields.</span></span> <span data-ttu-id="57071-815">Belirteç Oluşturucu İngilizce metin kesme, virgüller numaraları, vb. gibi ortak durumlarında mantığı içerir. Örneğin, `search=123,456` virgül İngilizce büyük sayılar için bin ayırıcı olarak kullanıldığından 123 ve 456, tek tek terimleri yerine tek bir terim 123,456 ile eşleşir.</span><span class="sxs-lookup"><span data-stu-id="57071-815">The tokenizer includes logic to handle cases common to English text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than the individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span></span> <span data-ttu-id="57071-816">Bu nedenle, koşullarını ayırmak için noktalama yerine boşluk kullanılmasını öneririz `search` parametresi.</span><span class="sxs-lookup"><span data-stu-id="57071-816">For this reason, we recommend using white space rather than punctuation to separate terms in the `search` parameter.</span></span>

<span data-ttu-id="57071-817">`searchMode=any|all`(isteğe bağlı, varsayılan olarak `any`) - arama terimleri bir bölümünü veya tamamını belgeyi bir eşleşme olarak saymak için eşleşmesi gereken olup olmadığını.</span><span class="sxs-lookup"><span data-stu-id="57071-817">`searchMode=any|all` (optional, defaults to `any`) - whether any or all of the search terms must be matched in order to count the document as a match.</span></span>

<span data-ttu-id="57071-818">`searchFields=[string]`(isteğe bağlı) - Belirtilen metni aramak için virgülle ayrılmış bir alan adları listesi.</span><span class="sxs-lookup"><span data-stu-id="57071-818">`searchFields=[string]` (optional) - The list of comma-separated field names to search for the specified text.</span></span> <span data-ttu-id="57071-819">Hedef alan işaretli, olarak `searchable`.</span><span class="sxs-lookup"><span data-stu-id="57071-819">Target fields must be marked as `searchable`.</span></span>

<span data-ttu-id="57071-820">`queryType=simple|full`(isteğe bağlı, varsayılan olarak `simple`) - simgelerini gibi sağlayan bir basit sorgu dilini kullanma "Basit" arama metni kümesine değerlendirdiğinde +, * ve "".</span><span class="sxs-lookup"><span data-stu-id="57071-820">`queryType=simple|full` (optional, defaults to `simple`) - when set to "simple" search text is interpreted using a simple query language that allows for symbols such as +, * and "".</span></span> <span data-ttu-id="57071-821">Sorguları, tüm aranabilir alanları değerlendirilir (veya alanlarını belirtilen `searchFields`) varsayılan olarak her belgedeki.</span><span class="sxs-lookup"><span data-stu-id="57071-821">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span></span> <span data-ttu-id="57071-822">Sorgu türü ayarlandığında `full` arama metni alana özgü ve ağırlıklı aramaları sağlayan Lucene sorgu dili kullanarak yorumlanır.</span><span class="sxs-lookup"><span data-stu-id="57071-822">When the query type is set to `full` search text is interpreted using the Lucene query language which allows field-specific and weighted searches.</span></span> <span data-ttu-id="57071-823">Bkz: [Basit Sorgu söz dizimi](https://msdn.microsoft.com/library/dn798920.aspx) ve [Lucene sorgu söz dizimi](https://msdn.microsoft.com/library/mt589323.aspx) arama sözdizimleri üzerinde özellikleri için.</span><span class="sxs-lookup"><span data-stu-id="57071-823">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on the search syntaxes.</span></span> 

> [!NOTE]
> <span data-ttu-id="57071-824">Sorgu dili benzer işlevselliği sunan $filter lehinde desteklenmiyor Lucene aramada aralığı.</span><span class="sxs-lookup"><span data-stu-id="57071-824">Range search in the Lucene query language is not supported in favor of $filter which offers similar functionality.</span></span>
> 
> 

<span data-ttu-id="57071-825">`moreLikeThis=[key]`(isteğe bağlı) **Önemli:** bu özellik yalnızca kullanılabilir `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="57071-825">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span></span> <span data-ttu-id="57071-826">Bu seçenek metin arama parametre içeren bir sorguda kullanılamaz `search=[string]`.</span><span class="sxs-lookup"><span data-stu-id="57071-826">This option cannot be used in a query that contains the text search parameter, `search=[string]`.</span></span> <span data-ttu-id="57071-827">`moreLikeThis` Parametresi belge anahtarı tarafından belirtilen belge benzer belgeleri bulur.</span><span class="sxs-lookup"><span data-stu-id="57071-827">The `moreLikeThis` parameter finds documents that are similar to the document specified by the document key.</span></span> <span data-ttu-id="57071-828">Ne zaman bir arama isteği yapıldığında ile `moreLikeThis`, arama terimleri listesi sıklığı ve kaynak belgedeki terimlerin rarity temel alınarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="57071-828">When a search request is made with `moreLikeThis`, a list of search terms is generated based on the frequency and rarity of terms in the source document.</span></span> <span data-ttu-id="57071-829">Bu koşullar, daha sonra isteği yapmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-829">Those terms are then used to make the request.</span></span> <span data-ttu-id="57071-830">Varsayılan olarak, tüm içeriğini `searchable` sürece alanlar olarak kabul `searchFields` hangi alanların aranacağını kısıtlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-830">By default, the contents of all `searchable` fields are considered unless `searchFields` is used to restrict which fields are searched.</span></span>  

<span data-ttu-id="57071-831">`$skip=#`(isteğe bağlı) - atlamak için; arama sonuçları sayısı 100. 000 ' büyük olamaz.</span><span class="sxs-lookup"><span data-stu-id="57071-831">`$skip=#` (optional) - the number of search results to skip; Cannot be greater than 100,000.</span></span> <span data-ttu-id="57071-832">Belgeleri sırayla taraması gereken ancak kullanamazsınız `$skip` bu sınırlama nedeniyle kullanmayı `$orderby` tamamen sıralı anahtar ve `$filter` bir aralık sorgu yerine.</span><span class="sxs-lookup"><span data-stu-id="57071-832">If you need to scan documents in sequence but cannot use `$skip` due to this limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-833">Çağrılırken **arama** POST kullanarak, bu parametre adlı `skip` yerine `$skip`.</span><span class="sxs-lookup"><span data-stu-id="57071-833">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span></span>
> 
> 

<span data-ttu-id="57071-834">`$top=#`(isteğe bağlı) - almak için arama sonuçları sayısı.</span><span class="sxs-lookup"><span data-stu-id="57071-834">`$top=#` (optional) - the number of search results to retrieve.</span></span> <span data-ttu-id="57071-835">Bu ile birlikte kullanılabilir `$skip` arama sonuçlarının istemci-tarafı Sayfalaması uygulamak üzere.</span><span class="sxs-lookup"><span data-stu-id="57071-835">This can be used in conjunction with `$skip` to implement client-side paging of search results.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-836">Çağrılırken **arama** POST kullanarak, bu parametre adlı `top` yerine `$top`.</span><span class="sxs-lookup"><span data-stu-id="57071-836">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="57071-837">`$count=true|false`(isteğe bağlı, varsayılan olarak `false`)-sonuçları toplam hata sayısı fetch belirtir.</span><span class="sxs-lookup"><span data-stu-id="57071-837">`$count=true|false` (optional, defaults to `false`) - Specifies whether to fetch the total count of results.</span></span> <span data-ttu-id="57071-838">Eşleşen tüm belgeleri sayısıdır `search` ve `$filter` yoksayılıyor parametreleri `$top` ve `$skip`.</span><span class="sxs-lookup"><span data-stu-id="57071-838">This is the count of all documents that match the `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span></span> <span data-ttu-id="57071-839">Bu değeri ayarlamak `true` bir performans etkisi olabilir.</span><span class="sxs-lookup"><span data-stu-id="57071-839">Setting this value to `true` may have a performance impact.</span></span> <span data-ttu-id="57071-840">Döndürülen sayısı yaklaşık olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="57071-840">Note that the count returned is an approximation.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-841">Çağrılırken **arama** POST kullanarak, bu parametre adlı `count` yerine `$count`.</span><span class="sxs-lookup"><span data-stu-id="57071-841">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span></span>
> 
> 

<span data-ttu-id="57071-842">`$orderby=[string]`(isteğe bağlı) - sonuçlarına göre sıralamak için ifadeleri virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="57071-842">`$orderby=[string]` (optional) - A list of comma-separated expressions to sort the results by.</span></span> <span data-ttu-id="57071-843">Her bir ifadenin bir alan adı veya yapılan bir çağrı olabilir `geo.distance()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="57071-843">Each expression can be either a field name or a call to the `geo.distance()` function.</span></span> <span data-ttu-id="57071-844">Her deyim tarafından izlenebilir `asc` belirtildiği için artan ve `desc` azalan belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="57071-844">Each expression can be followed by `asc` to indicated ascending, and `desc` to indicate descending.</span></span> <span data-ttu-id="57071-845">Varsayılan, artan.</span><span class="sxs-lookup"><span data-stu-id="57071-845">The default is ascending order.</span></span> <span data-ttu-id="57071-846">TIES belgeleri eşleşmiyor puan tarafından ayrılmış olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="57071-846">Ties will be broken by the match scores of documents.</span></span> <span data-ttu-id="57071-847">Öyle değilse `$orderby` belirtilmemişse, varsayılan sıralama düzeni belge eşleşmiyor puan göre azalan.</span><span class="sxs-lookup"><span data-stu-id="57071-847">If no `$orderby` is specified, the default sort order is descending by document match score.</span></span> <span data-ttu-id="57071-848">Bir sınır için 32 yan `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="57071-848">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-849">Çağrılırken **arama** POST kullanarak, bu parametre adlı `orderby` yerine `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="57071-849">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="57071-850">`$select=[string]`(isteğe bağlı) - almak için bir alanlar virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="57071-850">`$select=[string]` (optional) - A list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="57071-851">Belirtilmezse, şema olarak alınabilir işaretlenmiş tüm alanlar dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="57071-851">If unspecified, all fields marked as retrievable in the schema are included.</span></span> <span data-ttu-id="57071-852">Bu parametre ayarlayarak tüm alanları açıkça isteyebilir `*`.</span><span class="sxs-lookup"><span data-stu-id="57071-852">You can also explicitly request all fields by setting this parameter to `*`.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-853">Çağrılırken **arama** POST kullanarak, bu parametre adlı `select` yerine `$select`.</span><span class="sxs-lookup"><span data-stu-id="57071-853">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="57071-854">`facet=[string]`(sıfır veya daha fazla) - modeli tarafından bir alan.</span><span class="sxs-lookup"><span data-stu-id="57071-854">`facet=[string]` (zero or more) - A field to facet by.</span></span> <span data-ttu-id="57071-855">Dize virgülle ayrılmış olarak ifade edilen olduğunu özelleştirmek için parametreler isteğe bağlı olarak içerebilir `name:value` çiftleri.</span><span class="sxs-lookup"><span data-stu-id="57071-855">Optionally the string may contain parameters to customize the faceting expressed as comma-separated `name:value` pairs.</span></span> <span data-ttu-id="57071-856">Geçerli Parametreler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="57071-856">Valid parameters are:</span></span>

* <span data-ttu-id="57071-857">`count`(en fazla sayıda modeli şartı; varsayılan değer 10).</span><span class="sxs-lookup"><span data-stu-id="57071-857">`count` (max number of facet terms; default is 10).</span></span> <span data-ttu-id="57071-858">Maksimum yok yoktur, ancak özellikle çok sayıda benzersiz koşulları modellenmiş alan içeriyorsa, daha yüksek değerleri karşılık gelen bir performans cezasına sebep.</span><span class="sxs-lookup"><span data-stu-id="57071-858">There is no maximum, but higher values incur a corresponding performance penalty, especially if the faceted field contains a large number of unique terms.</span></span>
  * <span data-ttu-id="57071-859">Örneğin: `facet=category,count:5` modeli sonuçlarında ilk beş kategorileri alır.</span><span class="sxs-lookup"><span data-stu-id="57071-859">For example: `facet=category,count:5` gets the top five categories in facet results.</span></span>  
  * <span data-ttu-id="57071-860">**Not**: varsa `count` parametre benzersiz koşulları sayısından daha az ve sonuçları doğru olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="57071-860">**Note**: If the `count` parameter is less than the number of unique terms, the results may not be accurate.</span></span> <span data-ttu-id="57071-861">Olduğunu sorgular parça dağıtılan şekilde nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="57071-861">This is due to the way faceting queries are distributed across shards.</span></span> <span data-ttu-id="57071-862">Artan `count` genellikle terim sayıları, ancak performans maliyeti doğruluğu artırır.</span><span class="sxs-lookup"><span data-stu-id="57071-862">Increasing `count` generally increases the accuracy of the term counts, but at a performance cost.</span></span>
* <span data-ttu-id="57071-863">`sort`(birini `count` sıralamak için *azalan* sayıma göre `-count` sıralamak için *artan* sayıma göre `value` sıralamak için *artan* değeri ya da `-value` sıralamak için *azalan* değeriyle)</span><span class="sxs-lookup"><span data-stu-id="57071-863">`sort` (one of `count` to sort *descending* by count, `-count` to sort *ascending* by count, `value` to sort *ascending* by value, or `-value` to sort *descending* by value)</span></span>
  * <span data-ttu-id="57071-864">Örneğin: `facet=category,count:3,sort:count` her şehir adı belgelerle sayısına göre azalan sırada modeli sonuçlarında ilk üç kategorileri alır.</span><span class="sxs-lookup"><span data-stu-id="57071-864">For example: `facet=category,count:3,sort:count` gets the top three categories in facet results in descending order by the number of documents with each city name.</span></span> <span data-ttu-id="57071-865">Örneğin, en iyi üç kategorileri şunlardır: Bütçe, Motel ve lüks ve bütçe 5 isabet varsa, 6 Motel sahip ve 4 lüks sahip, ardından demet sırayla olacaktır Motel, bütçe, lüks.</span><span class="sxs-lookup"><span data-stu-id="57071-865">For example, if the top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then the buckets will be in the order Motel, Budget, Luxury.</span></span>
  * <span data-ttu-id="57071-866">Örneğin: `facet=rating,sort:-value` değerine göre azalan sırada tüm olası derecelendirmeler aralıklarını üretir.</span><span class="sxs-lookup"><span data-stu-id="57071-866">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span></span> <span data-ttu-id="57071-867">Derecelendirmeleri 1'den 5'e, örneğin, demet sıralanır 5, 4, 3, 2, kaç tane belgeleri her derecelendirme eşleşen yedeklemiş 1.</span><span class="sxs-lookup"><span data-stu-id="57071-867">For example, if the ratings are from 1 to 5, the buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span></span>
* <span data-ttu-id="57071-868">`values`(kanal ayrılmış sayısal veya `Edm.DateTimeOffset` değerleri model girdi değerleri dinamik bir dizi belirtme)</span><span class="sxs-lookup"><span data-stu-id="57071-868">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span></span>
  * <span data-ttu-id="57071-869">Örneğin: `facet=baseRate,values:10|20` üç demet oluşturur: biri kadar temel oranı 0 ancak 10, 10 için bir tane kadar dahil değildir, ancak 20 dahil değil, diğeri 20 veya daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="57071-869">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up to but not including 10, one for 10 up to but not including 20, and one for 20 or higher.</span></span>
  * <span data-ttu-id="57071-870">Örneğin: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` iki demet oluşturur: biri Şubat 2010'dan önce renovated Oteller ve Otel için bir renovated Şubat 2010 veya üzeri 1.</span><span class="sxs-lookup"><span data-stu-id="57071-870">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span></span>
* <span data-ttu-id="57071-871">`interval`(sayı, 0'dan büyük tamsayı aralığı veya `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` tarih saat değerleri için)</span><span class="sxs-lookup"><span data-stu-id="57071-871">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span></span>
  * <span data-ttu-id="57071-872">Örneğin: `facet=baseRate,interval:100` demet boyutu 100 temel oranı aralıklarını temel alarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="57071-872">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span></span> <span data-ttu-id="57071-873">Örneğin, temel oranları tüm $60 ve $600 arasında varsa, olacaktır 0-100, 100-200, 200-300, 400 300, 400-500 ve 500-600 aralıklarını.</span><span class="sxs-lookup"><span data-stu-id="57071-873">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span></span>
  * <span data-ttu-id="57071-874">Örneğin: `facet=lastRenovationDate,interval:year` bir demet zaman Oteller renovated her yıl üretir.</span><span class="sxs-lookup"><span data-stu-id="57071-874">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span></span>
* <span data-ttu-id="57071-875">`timeoffset`([+-] hh: mm, [+-] ssdd, veya [+-] hh) `timeoffset` isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span></span> <span data-ttu-id="57071-876">İle yalnızca birleştirilebilir `interval` seçeneği ve yalnızca türünde bir alan uygulandığında `Edm.DateTimeOffset`.</span><span class="sxs-lookup"><span data-stu-id="57071-876">It can only be combined with the `interval` option, and only when applied to a field of type `Edm.DateTimeOffset`.</span></span> <span data-ttu-id="57071-877">Değeri, zaman sınırları ayarı hesabına UTC saat konumu belirtir.</span><span class="sxs-lookup"><span data-stu-id="57071-877">The value specifies the UTC time offset to account for in setting time boundaries.</span></span>
  * <span data-ttu-id="57071-878">Örneğin: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` 01:00:00 UTC (hedef saat diliminde gece yarısı) konumunda başlayan günlük sınır kullanır</span><span class="sxs-lookup"><span data-stu-id="57071-878">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses the day boundary that starts at 01:00:00 UTC (midnight in the target time zone)</span></span>
* <span data-ttu-id="57071-879">**Not**: `count` ve `sort` aynı modeli belirtiminde birleştirilebilir, ancak ile birleştirilemez `interval` veya `values`, ve `interval` ve `values` birlikte birleştirilemez.</span><span class="sxs-lookup"><span data-stu-id="57071-879">**Note**: `count` and `sort` can be combined in the same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span></span>
* <span data-ttu-id="57071-880">**Not**: tarih saat aralığı nedeni modellerinin hesaplanan UTC saat tabanlı `timeoffset` belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="57071-880">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span></span> <span data-ttu-id="57071-881">Örneğin: için `facet=lastRenovationDate,interval:day`, günlük sınır 00:00:00 UTC başlatır.</span><span class="sxs-lookup"><span data-stu-id="57071-881">For example: for `facet=lastRenovationDate,interval:day`, the day boundary starts at 00:00:00 UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="57071-882">Çağrılırken **arama** POST kullanarak, bu parametre adlı `facets` yerine `facet`.</span><span class="sxs-lookup"><span data-stu-id="57071-882">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span></span> <span data-ttu-id="57071-883">Ayrıca, bunu burada her ayrı modeli ifade dizesidir dizeleri bir JSON dizisi olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="57071-883">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span></span>
> 
> 

<span data-ttu-id="57071-884">`$filter=[string]`(isteğe bağlı) - standart OData sözdiziminde yapılandırılmış arama ifadesi.</span><span class="sxs-lookup"><span data-stu-id="57071-884">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-885">Çağrılırken **arama** POST kullanarak, bu parametre adlı `filter` yerine `$filter`.</span><span class="sxs-lookup"><span data-stu-id="57071-885">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="57071-886">`highlight=[string]`(isteğe bağlı) - virgülle ayrılmış bir alan adları isabet için kullanılan bir dizi vurgular.</span><span class="sxs-lookup"><span data-stu-id="57071-886">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span></span> <span data-ttu-id="57071-887">Yalnızca `searchable` alanları isabet vurgulama için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="57071-887">Only `searchable` fields can be used for hit highlighting.</span></span>

<span data-ttu-id="57071-888">`highlightPreTag=[string]`(isteğe bağlı, varsayılan olarak `<em>`) - bir dize vurgular isabet başına etiketi.</span><span class="sxs-lookup"><span data-stu-id="57071-888">`highlightPreTag=[string]` (optional, defaults to `<em>`) - A string tag that prepends to hit highlights.</span></span> <span data-ttu-id="57071-889">İle ayarlanmalıdır `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="57071-889">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-890">Çağrılırken **arama** GET kullanarak, URL'deki ayrılmış karakterler (örneğin, % &#23; yerine) yüzde olarak kodlanmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-890">When calling **Search** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="57071-891">`highlightPostTag=[string]`(isteğe bağlı, varsayılan olarak `</em>`)-vurgular isabet ekler bir dize etiketi.</span><span class="sxs-lookup"><span data-stu-id="57071-891">`highlightPostTag=[string]` (optional, defaults to `</em>`) - a string tag that appends to hit highlights.</span></span> <span data-ttu-id="57071-892">İle ayarlanmalıdır `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="57071-892">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-893">Çağrılırken **arama** GET kullanarak, URL'deki ayrılmış karakterler (örneğin, % &#23; yerine) yüzde olarak kodlanmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-893">When calling **Search** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="57071-894">`scoringProfile=[string]`(isteğe bağlı) - değerlendirmek için bir Puanlama profili adıyla aynı sonuçları sıralamak için eşleşen belgelerin puanlarını.</span><span class="sxs-lookup"><span data-stu-id="57071-894">`scoringProfile=[string]` (optional) - The name of a scoring profile to evaluate match scores for matching documents in order to sort the results.</span></span>

<span data-ttu-id="57071-895">`scoringParameter=[string]`(sıfır veya daha fazla) - bir Puanlama işlevi tanımlanan her parametre için değerler belirtir (örneğin, `referencePointParameter`) biçimini kullanarak `name-value1,value2,...`.</span><span class="sxs-lookup"><span data-stu-id="57071-895">`scoringParameter=[string]` (zero or more) - Indicates the values for each parameter defined in a scoring function (for example, `referencePointParameter`) using the format `name-value1,value2,...`.</span></span>

* <span data-ttu-id="57071-896">Örneğin, Puanlama profili "mylocation" adlı bir parametre ile bir işlev tanımlıyorsa sorgu dizesi seçeneği olması `&scoringParameter=mylocation--122.2,44.8`.</span><span class="sxs-lookup"><span data-stu-id="57071-896">For example, if the scoring profile defines a function with a parameter called "mylocation" the query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span></span> <span data-ttu-id="57071-897">İkinci tire ilk değer (Bu örnekte boylam) bir parçası olsa da ilk tire değer listesinden adını ayırır.</span><span class="sxs-lookup"><span data-stu-id="57071-897">The first dash separates the name from the value list, while the second dash is part of the first value (longitude in this example).</span></span>
* <span data-ttu-id="57071-898">Puanlama parametrelerini etiketi, artırmanın virgüller, içerebilir gibi böyle bir değer tek tırnak kullanılarak listesinde kaçış.</span><span class="sxs-lookup"><span data-stu-id="57071-898">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in the list using single quotes.</span></span> <span data-ttu-id="57071-899">Değer kendilerini tek tırnak içermiyorsa, katlama tarafından kaçış</span><span class="sxs-lookup"><span data-stu-id="57071-899">If the values themselves contain single quotes, you can escape them by doubling.</span></span>
  * <span data-ttu-id="57071-900">Örneğin, "Hello, O'Brien" ve "Smith", sorgu "mytag" adlı bir parametreye artırmanın bir etiketi olması ve etiket artırmak istiyorsanız değerleri dize seçenek olacaktır `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span><span class="sxs-lookup"><span data-stu-id="57071-900">For example, if you have a tag boosting parameter called "mytag" and you want to boost on the tag values "Hello, O'Brien" and "Smith", the query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span></span> <span data-ttu-id="57071-901">Tırnak işaretleri yalnızca olduğuna dikkat edin virgül içeren değerler için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="57071-901">Note that quotes are only required for values that contain commas.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-902">Çağrılırken **arama** POST kullanarak, bu parametre adlı `scoringParameters` yerine `scoringParameter`.</span><span class="sxs-lookup"><span data-stu-id="57071-902">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span></span> <span data-ttu-id="57071-903">Bir JSON dizisini ayrı bir olduğu her bir dize belirttiğiniz ayrıca `name-values` çifti.</span><span class="sxs-lookup"><span data-stu-id="57071-903">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span></span>
> 
> 

<span data-ttu-id="57071-904">`minimumCoverage`(isteğe bağlı, 100 varsayılanlara)-0 ile 100 sırada başarılı bildirilecek sorgu için bir arama sorgusu tarafından ele alınması gereken dizin yüzdesini gösteren arasında bir sayı.</span><span class="sxs-lookup"><span data-stu-id="57071-904">`minimumCoverage` (optional, defaults to 100) - a number between 0 and 100 indicating the percentage of the index that must be covered by a search query in order for the query to be reported as a success.</span></span> <span data-ttu-id="57071-905">Varsayılan olarak, tüm dizini kullanılabilir olmalıdır veya `Search` 503 HTTP durum kodunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="57071-905">By default, the entire index must be available or `Search` will return HTTP status code 503.</span></span> <span data-ttu-id="57071-906">Ayarlarsanız `minimumCoverage` ve `Search` başarılı, HTTP 200 dönün ve içeren bir `@search.coverage` sorguda eklenmiştir dizin yüzdesini gösteren yanıt değeri.</span><span class="sxs-lookup"><span data-stu-id="57071-906">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in the response indicating the percentage of the index that was included in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-907">Bu parametre için bir değer 100'den daha düşük ayarı yalnızca bir çoğaltma hizmetleriyle için bile arama kullanılabilirlik sağlamak için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="57071-907">Setting this parameter to a value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="57071-908">Ancak, tüm eşleşen belgeleri arama sonuçlarında mevcut olması garanti.</span><span class="sxs-lookup"><span data-stu-id="57071-908">However, not all matching documents are guaranteed to be present in the search results.</span></span> <span data-ttu-id="57071-909">Arama geri çağırma önemlidir kullanılabilirlik uygulamanızı daha sonra çıkmak en iyisidir `minimumCoverage` zaman, varsayılan değer 100.</span><span class="sxs-lookup"><span data-stu-id="57071-909">If search recall is more important to your application than availability, then it's best to leave `minimumCoverage` at its default value of 100.</span></span>
> 
> 

<span data-ttu-id="57071-910">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="57071-910">`api-version=[string]` (required).</span></span> <span data-ttu-id="57071-911">Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="57071-911">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="57071-912">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="57071-912">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="57071-913">Not: Bu işlem için `api-version` olup, çağrı bağımsız olarak URL'deki sorgu parametresi olarak belirtilen **arama** GET veya POST ile.</span><span class="sxs-lookup"><span data-stu-id="57071-913">Note: For this operation, the `api-version` is specified as a query parameter in the URL regardless of whether you call **Search** with GET or POST.</span></span>

<span data-ttu-id="57071-914">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="57071-914">**Request Headers**</span></span>

<span data-ttu-id="57071-915">Aşağıdaki listede gerekli ve isteğe bağlı İstek üstbilgilerinin açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="57071-915">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="57071-916">`api-key``api-key` İsteğin arama hizmetiniz için kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-916">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="57071-917">Hizmet URL'nizi benzersiz bir dize değeri değil.</span><span class="sxs-lookup"><span data-stu-id="57071-917">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="57071-918">**Arama** isteği, bir yönetici anahtarını veya sorgu anahtarı belirtebilirsiniz `api-key`.</span><span class="sxs-lookup"><span data-stu-id="57071-918">The **Search** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="57071-919">İstek URL'si oluşturmak için hizmet adı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-919">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="57071-920">Hizmet adını alabilir ve `api-key` Azure Portalı'nda, hizmet panosundan.</span><span class="sxs-lookup"><span data-stu-id="57071-920">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="57071-921">Bkz: [portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="57071-921">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="57071-922">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="57071-922">**Request Body**</span></span>

<span data-ttu-id="57071-923">GET için: yok.</span><span class="sxs-lookup"><span data-stu-id="57071-923">For GET: None.</span></span>

<span data-ttu-id="57071-924">POST için:</span><span class="sxs-lookup"><span data-stu-id="57071-924">For POST:</span></span>

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered to declare query successful; default 100),
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

<span data-ttu-id="57071-925">**Kısmi arama yanıtları devamlılığı**</span><span class="sxs-lookup"><span data-stu-id="57071-925">**Continuation of Partial Search Responses**</span></span>

<span data-ttu-id="57071-926">Bazen Azure Search tüm istenen sonuçları tek bir arama yanıtta döndüremez.</span><span class="sxs-lookup"><span data-stu-id="57071-926">Sometimes Azure Search can't return all the requested results in a single Search response.</span></span> <span data-ttu-id="57071-927">Bu sorgu çok fazla belgeleri değil belirterek isteğinde bulunduğunda gibi farklı nedenlerle oluşabilir `$top` veya için bir değer belirterek `$top` , çok büyük.</span><span class="sxs-lookup"><span data-stu-id="57071-927">This can happen for different reasons, such as when the query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span></span> <span data-ttu-id="57071-928">Böyle durumlarda, Azure Search içerecektir `@odata.nextLink` yanıt gövdesi içinde ek açıklama ve ayrıca `@search.nextPageParameters` bir POST isteği ise.</span><span class="sxs-lookup"><span data-stu-id="57071-928">In such cases, Azure Search will include the `@odata.nextLink` annotation in the response body, and also `@search.nextPageParameters` if it was a POST request.</span></span> <span data-ttu-id="57071-929">Bu ek açıklamalar değerlerini arama yanıtı sonraki bölümü almak için başka bir arama isteğine formüle için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57071-929">You can use the values of these annotations to formulate another Search request to get the next part of the search response.</span></span> <span data-ttu-id="57071-930">Bu adlı bir ***devamlılık*** özgün araması genellikle istek ve ek açıklamalar denir ***devamlılık belirteçleri***.</span><span class="sxs-lookup"><span data-stu-id="57071-930">This is called a ***continuation*** of the original Search request, and the annotations are generally called ***continuation tokens***.</span></span> <span data-ttu-id="57071-931">Bkz: [örnek](#SearchResponse) bu açıklamalarının ve yanıt gövdesi içinde nerede göründüklerinden sözdizimi hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="57071-931">See [the example below](#SearchResponse) for details on the syntax of these annotations and where they appear in the response body.</span></span> 

<span data-ttu-id="57071-932">Azure Search devamlılık belirteçleri neden döndürebilir nedeniyle uygulama özgü ve değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="57071-932">The reasons why Azure Search might return continuation tokens are implementation-specific and subject to change.</span></span> <span data-ttu-id="57071-933">Sağlam istemcileri her zaman durumlarda beklenenden daha az belgeler döndürülür ve belgeleri alınırken devam etmek için devamlılık belirteci eklenmiştir işlemeye hazır olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-933">Robust clients should always be ready to handle cases where fewer documents than expected are returned and a continuation token is included to continue retrieving documents.</span></span> <span data-ttu-id="57071-934">Ayrıca, aynı HTTP yöntemi özgün istek devam edebilmeniz için kullanmanız gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="57071-934">Also note that you must use the same HTTP method as the original request in order to continue.</span></span> <span data-ttu-id="57071-935">Bir GET isteği gönderirse, örneğin, gönderdiğiniz herhangi bir devamlılık isteğini de GET kullanmanız gerekir (ve sonrası için benzer şekilde).</span><span class="sxs-lookup"><span data-stu-id="57071-935">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span></span>

<span data-ttu-id="57071-936"><a name="SearchResponse"></a>
**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="57071-936"><a name="SearchResponse"></a>
**Response**</span></span>

<span data-ttu-id="57071-937">Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.</span><span class="sxs-lookup"><span data-stu-id="57071-937">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@odata.count": # (if $count=true was provided in the query),
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "@search.facets": { (if faceting was specified in the query)
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
      "@search.nextPageParameters": { (request body to fetch the next page of results if not all results could be returned in this response and Search was called with POST)
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
      "@odata.nextLink": (URL to fetch the next page of results if not all results could be returned in this response; Applies to both GET and POST)
    }

<span data-ttu-id="57071-938">**Örnekler:**</span><span class="sxs-lookup"><span data-stu-id="57071-938">**Examples:**</span></span>

<span data-ttu-id="57071-939">Ek örnekler bulabilirsiniz [OData ifade sözdizimini Azure arama için](https://msdn.microsoft.com/library/azure/dn798921.aspx) sayfası.</span><span class="sxs-lookup"><span data-stu-id="57071-939">You can find additional examples on the [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span></span>

1)    <span data-ttu-id="57071-940">Arama dizini tarihe göre azalan sırada sıralanır.</span><span class="sxs-lookup"><span data-stu-id="57071-940">Search the Index sorted descending by date.</span></span>

    <span data-ttu-id="57071-941">GET /indexes/hotels/docs? arama = * & $orderby lastRenovationDate desc & api-version = 2015-02-28-Önizleme =</span><span class="sxs-lookup"><span data-stu-id="57071-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="57071-942">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "*", "orderby": "lastRenovationDate desc"}</span><span class="sxs-lookup"><span data-stu-id="57071-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span></span>

2)    <span data-ttu-id="57071-943">Modellenmiş bir arama dizinini aramak ve modelleri için kategoriler, derecelendirme, etiketleri yanı sıra belirli aralıklara baseRate öğeleriyle almak:</span><span class="sxs-lookup"><span data-stu-id="57071-943">In a faceted search, search the index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span></span>

    <span data-ttu-id="57071-944">GET /indexes/hotels/docs? arama = test & modeli = kategori & modeli = derecelendirme & modeli etiketleri & modeli = baseRate, değerleri: 80 = | 150 | 220 & API sürümü 2015-02-28-Önizleme =</span><span class="sxs-lookup"><span data-stu-id="57071-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="57071-945">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "test", "modelleri": ["kategorisi", "Derecelendirme", "etiketler", "baseRate, değerleri: 80 | 150 | 220"]}</span><span class="sxs-lookup"><span data-stu-id="57071-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span></span>

3)    <span data-ttu-id="57071-946">Bir filtre kullanarak daraltmak önceki modellenmiş sorgu sonuçları üzerinde kullanıcı tıklattıktan sonra 3 ve kategori "Motel" derecelendirme:</span><span class="sxs-lookup"><span data-stu-id="57071-946">Using a filter, narrow down the previous faceted query results after the user clicks on rating 3 and category "Motel":</span></span>

    <span data-ttu-id="57071-947">GET /indexes/hotels/docs? arama = test & modeli etiketleri & modeli = baseRate, değerleri: 80 = | 150 | 220 & $filter & derecelendirme eq 3 ve kategori eq 'Motel' api-version = 2015-02-28-Önizleme =</span><span class="sxs-lookup"><span data-stu-id="57071-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="57071-948">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "test", "modelleri": ["etiketleri", "baseRate, değerleri: 80 | 150 | 220"], "filtre": "Derecelendirme eq 3 ve kategori eq 'Motel'"}</span><span class="sxs-lookup"><span data-stu-id="57071-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span></span>

4) <span data-ttu-id="57071-949">Modellenmiş bir aramada bir sorgudan döndürülen benzersiz koşulları bir üst sınır ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="57071-949">In a faceted search, set an upper limit on unique terms returned in a query.</span></span> <span data-ttu-id="57071-950">Varsayılan değer 10'dur, ancak artırabilir ya da bu değeri kullanılarak azaltmak `count` parametresini `facet` özniteliği:</span><span class="sxs-lookup"><span data-stu-id="57071-950">The default is 10, but you can increase or decrease this value using the `count` parameter on the `facet` attribute:</span></span>

    <span data-ttu-id="57071-951">GET /indexes/hotels/docs? arama = test & modeli Şehir, sayısı: 5 & api-version = 2015-02-28-Önizleme =</span><span class="sxs-lookup"><span data-stu-id="57071-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="57071-952">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "test", "modelleri": ["Şehir, sayısı: 5"]}</span><span class="sxs-lookup"><span data-stu-id="57071-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span></span>

5)    <span data-ttu-id="57071-953">Belirli alanları dizin arama; Dile özgü alanı:</span><span class="sxs-lookup"><span data-stu-id="57071-953">Search the Index within specific fields; For example, a language-specific field:</span></span>

    <span data-ttu-id="57071-954">GET /indexes/hotels/docs? arama hôtel & searchFields = description_fr & api-version = 2015-02-28-Önizleme =</span><span class="sxs-lookup"><span data-stu-id="57071-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="57071-955">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "hôtel", "searchFields": "description_fr"}</span><span class="sxs-lookup"><span data-stu-id="57071-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span></span>

6) <span data-ttu-id="57071-956">Dizin arasında birden çok alan arayın.</span><span class="sxs-lookup"><span data-stu-id="57071-956">Search the Index across multiple fields.</span></span> <span data-ttu-id="57071-957">Örneğin, depolamak ve tüm aynı dizin içinde birden çok dilde aranabilir alanlara sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57071-957">For example, you can store and query searchable fields in multiple languages, all within the same index.</span></span>  <span data-ttu-id="57071-958">İngilizce ve Fransızca açıklamaları aynı belgede birlikte bulunması durumunda veya tamamını sorgu sonuçlarında döndürebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="57071-958">If English and French descriptions co-exist in the same document, you can return any or all in the query results:</span></span>

    <span data-ttu-id="57071-959">GET /indexes/hotels/docs? arama otel & searchFields = açıklama, description_fr & api-version = 2015-02-28-Önizleme =</span><span class="sxs-lookup"><span data-stu-id="57071-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="57071-960">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "otel", "searchFields": "açıklama, description_fr"}</span><span class="sxs-lookup"><span data-stu-id="57071-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span></span>

<span data-ttu-id="57071-961">Aynı anda yalnızca bir dizin sorgulanabilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="57071-961">Note that you can only query one index at a time.</span></span> <span data-ttu-id="57071-962">Bir seferde bir sorgu planlamıyorsanız her dil için birden çok dizin oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="57071-962">Do not create multiple indexes for each language unless you plan to query one at a time.</span></span>

7)    <span data-ttu-id="57071-963">Disk belleği - Get öğe 1 sayfasının (sayfa boyutu Dur 10):</span><span class="sxs-lookup"><span data-stu-id="57071-963">Paging - Get the 1st page of items (page size is 10):</span></span>

    <span data-ttu-id="57071-964">GET /indexes/hotels/docs? arama = * & $skip = 0 & $top = 10 & api-version = 2015-02-28-Önizleme</span><span class="sxs-lookup"><span data-stu-id="57071-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="57071-965">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "*", "Atla": 0, "üst": 10}</span><span class="sxs-lookup"><span data-stu-id="57071-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span></span>

8)    <span data-ttu-id="57071-966">Disk belleği - Get öğe 2 sayfasının (sayfa boyutu Dur 10):</span><span class="sxs-lookup"><span data-stu-id="57071-966">Paging - Get the 2nd page of items (page size is 10):</span></span>

    <span data-ttu-id="57071-967">GET /indexes/hotels/docs? arama = * & $skip = 10 & $top = 10 & api-version = 2015-02-28-Önizleme</span><span class="sxs-lookup"><span data-stu-id="57071-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="57071-968">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "*", "Atla": "üst" 10: 10}</span><span class="sxs-lookup"><span data-stu-id="57071-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span></span>

9)    <span data-ttu-id="57071-969">Belirli bir alan kümesi Al:</span><span class="sxs-lookup"><span data-stu-id="57071-969">Retrieve a specific set of fields:</span></span>

    <span data-ttu-id="57071-970">GET /indexes/hotels/docs? arama = * & $select hotelName, açıklama ve api-version = 2015-02-28-Önizleme =</span><span class="sxs-lookup"><span data-stu-id="57071-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="57071-971">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "*", "Seç": "hotelName, açıklaması"}</span><span class="sxs-lookup"><span data-stu-id="57071-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span></span>

10)  <span data-ttu-id="57071-972">Bir özel filtre ifadesi eşleşen belgeler Al:</span><span class="sxs-lookup"><span data-stu-id="57071-972">Retrieve documents matching a specific filter expression:</span></span>

    <span data-ttu-id="57071-973">GET /indexes/hotels/docs? $filter = (baseRate ge 60 ve baseRate lt 300) veya hotelName eq 'Süslü kalmak' & api-version = 2015-02-28-Önizleme</span><span class="sxs-lookup"><span data-stu-id="57071-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="57071-974">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"filtre": "(baseRate ge 60 ve baseRate lt 300) veya hotelName eq 'Süslü Kal'"}</span><span class="sxs-lookup"><span data-stu-id="57071-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span></span>

11) <span data-ttu-id="57071-975">İsabet vurgular dizin ve return parçaları arama</span><span class="sxs-lookup"><span data-stu-id="57071-975">Search the index and return fragments with hit highlights</span></span>

    <span data-ttu-id="57071-976">GET /indexes/hotels/docs? arama bir şey = & vurgulayın açıklama & api-version = 2015-02-28-Önizleme =</span><span class="sxs-lookup"><span data-stu-id="57071-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="57071-977">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "bir şey", "highlight": "Açıklama"}</span><span class="sxs-lookup"><span data-stu-id="57071-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span></span>

12) <span data-ttu-id="57071-978">Dizin arama ve yakın bir başvuru çıktığınızda uzağına konumdan sıralanmış belgeleri döndürür</span><span class="sxs-lookup"><span data-stu-id="57071-978">Search the index and return documents sorted from closer to farther away from a reference location</span></span>

    <span data-ttu-id="57071-979">GET /indexes/hotels/docs? arama bir şey = & $orderby=geo.distance (konum, geography'POINT(-122.12315 47.88121)') & api-version = 2015-02-28-Önizleme</span><span class="sxs-lookup"><span data-stu-id="57071-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="57071-980">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "bir şey", "orderby": "geo.distance (konum, geography'POINT(-122.12315 47.88121)')"}</span><span class="sxs-lookup"><span data-stu-id="57071-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span></span>

13) <span data-ttu-id="57071-981">"Coğrafi" adlı bir Puanlama profili olduğunu varsayarak dizininde iki uzaklık Puanlama işlevleri ile arama, "currentLocation" ve "lastLocation" adlı bir parametreyi tanımlayan bir adı verilen bir parametre tanımlama</span><span class="sxs-lookup"><span data-stu-id="57071-981">Search the index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span></span>

    <span data-ttu-id="57071-982">GET /indexes/hotels/docs? arama bir şey = & scoringProfile = coğrafi & scoringParameter currentLocation--122.123,44.77233 & scoringParameter = lastLocation--121.499,44.2113 & api-version = 2015-02-28-Önizleme =</span><span class="sxs-lookup"><span data-stu-id="57071-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="57071-983">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "bir şey", "scoringProfile": "coğrafi", "scoringParameters": ["currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113"]}</span><span class="sxs-lookup"><span data-stu-id="57071-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span></span>

14) <span data-ttu-id="57071-984">Dizini kullanarak bulmanın [Basit Sorgu söz dizimi](https://msdn.microsoft.com/library/dn798920.aspx).</span><span class="sxs-lookup"><span data-stu-id="57071-984">Find documents in the index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span></span> <span data-ttu-id="57071-985">Bu sorgu burada koşulları "rahatlık" ve "Konum" ancak değil "motel" aranabilir alanları içeren Oteller döndürür:</span><span class="sxs-lookup"><span data-stu-id="57071-985">This query returns hotels where searchable fields contain the terms "comfort" and "location" but not "motel":</span></span>

    <span data-ttu-id="57071-986">GET /indexes/hotels/docs? arama = rahatlık + konumu-motel & searchMode = all & api-version = 2015-02-28-Önizleme</span><span class="sxs-lookup"><span data-stu-id="57071-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="57071-987">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "rahatlık + konumu-motel", "searchMode": "tümü"}</span><span class="sxs-lookup"><span data-stu-id="57071-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span></span>

<span data-ttu-id="57071-988">Kullanımına dikkat edin `searchMode=all` üstünde.</span><span class="sxs-lookup"><span data-stu-id="57071-988">Note the use of `searchMode=all` above.</span></span> <span data-ttu-id="57071-989">Bu parametreyi dahil olmak üzere varsayılan değerini geçersiz kılar `searchMode=any`, sağlama, `-motel` "Ve değil" yerine "Veya değil" anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="57071-989">Including this parameter overrides the default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span></span> <span data-ttu-id="57071-990">Olmadan `searchMode=all`"Veya, arama sonuçları kısıtlayan yerine genişletir değil" alın ve bu, bazı kullanıcılara counter-intuitive olabilir.</span><span class="sxs-lookup"><span data-stu-id="57071-990">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive to some users.</span></span>

15) <span data-ttu-id="57071-991">Dizini kullanarak bulmanın [lucene sorgu söz dizimi](https://msdn.microsoft.com/library/mt589323.aspx).</span><span class="sxs-lookup"><span data-stu-id="57071-991">Find documents in the index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span></span> <span data-ttu-id="57071-992">Bu sorgu hotels "Bütçe" terimi kategori alanı, içerdiği ve "son renovated" ifadesini içeren tüm aranabilir alanları döndürür.</span><span class="sxs-lookup"><span data-stu-id="57071-992">This query returns hotels where the category field contains the term "budget" and all searchable fields containing the phrase "recently renovated".</span></span> <span data-ttu-id="57071-993">"En son renovated" ifadesini içeren belgeleri yüksek terim artırma değeri (3) sonucunda derecelendirilir.</span><span class="sxs-lookup"><span data-stu-id="57071-993">Documents containing the phrase "recently renovated" are ranked higher as a result of the term boost value (3)</span></span>

    <span data-ttu-id="57071-994">GET /indexes/hotels/docs? arama Kategori: Bütçe = ve \"son renovated\"^ 3 & searchMode = all & api-version = 2015-02-28-Önizleme & querytype tam =</span><span class="sxs-lookup"><span data-stu-id="57071-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span></span>

    <span data-ttu-id="57071-995">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "Kategori: Bütçe ve \"son renovated\"^ 3", "queryType": "tam", "searchMode": "tümü"}</span><span class="sxs-lookup"><span data-stu-id="57071-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span></span>

<a name="LookupAPI"></a>

## <a name="lookup-document"></a><span data-ttu-id="57071-996">Arama belge</span><span class="sxs-lookup"><span data-stu-id="57071-996">Lookup Document</span></span>
<span data-ttu-id="57071-997">**Arama belge** işlemi Azure aramadan belge alır.</span><span class="sxs-lookup"><span data-stu-id="57071-997">The **Lookup Document** operation retrieves a document from Azure Search.</span></span> <span data-ttu-id="57071-998">Bu, belirli arama sonucu kullanıcı ve bu belge hakkında belirli diğer ayrıntıları aramak istediğinizde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-998">This is useful when a user clicks on a specific search result, and you want to look up specific details about that document.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

<span data-ttu-id="57071-999">**İstek**</span><span class="sxs-lookup"><span data-stu-id="57071-999">**Request**</span></span>

<span data-ttu-id="57071-1000">HTTPS istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="57071-1000">HTTPS is required for service requests.</span></span> <span data-ttu-id="57071-1001">**Arama belge** isteği oluşturulmasını gibi.</span><span class="sxs-lookup"><span data-stu-id="57071-1001">The **Lookup Document** request can be constructed as follows.</span></span>

    GET /indexes/[index name]/docs/key?[query parameters]

<span data-ttu-id="57071-1002">Alternatif olarak, anahtar arama için geleneksel OData sözdizimini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="57071-1002">Alternatively, you can use the traditional OData syntax for key lookup:</span></span>

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

<span data-ttu-id="57071-1003">İstek URI'si [dizin adı] içerir ve [Temel], hangi dizinden almak için hangi belge belirtme.</span><span class="sxs-lookup"><span data-stu-id="57071-1003">The request URI includes an [index name] and [key], specifying which document to retrieve from which index.</span></span> <span data-ttu-id="57071-1004">Ayrıca, aynı anda yalnızca bir belge alabilir.</span><span class="sxs-lookup"><span data-stu-id="57071-1004">You can only get one document at a time.</span></span> <span data-ttu-id="57071-1005">Kullanım **arama** tek bir istekte birden çok belge alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="57071-1005">Use **Search** to get multiple documents in a single request.</span></span>

<span data-ttu-id="57071-1006">**Sorgu parametreleri**</span><span class="sxs-lookup"><span data-stu-id="57071-1006">**Query Parameters**</span></span>

<span data-ttu-id="57071-1007">`$select=[string]`(isteğe bağlı) - almak için bir alanlar virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="57071-1007">`$select=[string]` (optional) - a list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="57071-1008">Belirtilmemiş veya kümesine `*`, şemada alınabilir olarak işaretlenmiş tüm alanlar projeksiyon dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="57071-1008">If unspecified or set to `*`, all fields marked as retrievable in the schema are included in the projection.</span></span>

<span data-ttu-id="57071-1009">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="57071-1009">`api-version=[string]` (required).</span></span> <span data-ttu-id="57071-1010">Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="57071-1010">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="57071-1011">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="57071-1011">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="57071-1012">Not: Bu işlem için `api-version` sorgu parametresi olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="57071-1012">Note: For this operation, the `api-version` is specified as a query parameter.</span></span>

<span data-ttu-id="57071-1013">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="57071-1013">**Request Headers**</span></span>

<span data-ttu-id="57071-1014">Aşağıdaki listede gerekli ve isteğe bağlı İstek üstbilgilerinin açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="57071-1014">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="57071-1015">`api-key``api-key` İsteğin arama hizmetiniz için kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-1015">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="57071-1016">Hizmet URL'nizi benzersiz bir dize değeri değil.</span><span class="sxs-lookup"><span data-stu-id="57071-1016">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="57071-1017">**Arama belge** isteği, bir yönetici anahtarını veya sorgu anahtarı belirtebilirsiniz `api-key`.</span><span class="sxs-lookup"><span data-stu-id="57071-1017">The **Lookup Document** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="57071-1018">İstek URL'si oluşturmak için hizmet adı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-1018">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="57071-1019">Hizmet adını alabilir ve `api-key` Azure Portalı'nda, hizmet panosundan.</span><span class="sxs-lookup"><span data-stu-id="57071-1019">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="57071-1020">Bkz: [portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="57071-1020">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="57071-1021">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="57071-1021">**Request Body**</span></span>

<span data-ttu-id="57071-1022">yok.</span><span class="sxs-lookup"><span data-stu-id="57071-1022">None.</span></span>

<span data-ttu-id="57071-1023">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="57071-1023">**Response**</span></span>

<span data-ttu-id="57071-1024">Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.</span><span class="sxs-lookup"><span data-stu-id="57071-1024">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      field_name: field_value (fields matching the default or specified projection)
    }

<span data-ttu-id="57071-1025">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="57071-1025">**Example**</span></span>

<span data-ttu-id="57071-1026">Arama anahtarı '2' olan belge</span><span class="sxs-lookup"><span data-stu-id="57071-1026">Lookup the document that has key '2'</span></span>

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

<span data-ttu-id="57071-1027">Arama 'OData sözdizimini kullanarak 3' anahtarına sahip belge:</span><span class="sxs-lookup"><span data-stu-id="57071-1027">Lookup the document that has key '3' using OData syntax:</span></span>

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a><span data-ttu-id="57071-1028">Count belgeleri</span><span class="sxs-lookup"><span data-stu-id="57071-1028">Count Documents</span></span>
<span data-ttu-id="57071-1029">**Sayısı belgeleri** işlemi arama dizini belgelerde sayısını alır.</span><span class="sxs-lookup"><span data-stu-id="57071-1029">The **Count Documents** operation retrieves a count of the number of documents in a search index.</span></span> <span data-ttu-id="57071-1030">`$count` Sözdizimi OData protokolü bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-1030">The `$count` syntax is part of the OData protocol.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

<span data-ttu-id="57071-1031">**İstek**</span><span class="sxs-lookup"><span data-stu-id="57071-1031">**Request**</span></span>

<span data-ttu-id="57071-1032">HTTPS istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="57071-1032">HTTPS is required for service requests.</span></span> <span data-ttu-id="57071-1033">**Sayısı belgeleri** isteği GET yöntemini kullanan olacak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="57071-1033">The **Count Documents** request can be constructed using the GET method.</span></span>

<span data-ttu-id="57071-1034">İstek URI'SİNDEKİ [dizin adı] belirtilen dizin belgeleri koleksiyonundaki tüm öğelerin sayısını döndürülecek hizmetin söyler.</span><span class="sxs-lookup"><span data-stu-id="57071-1034">The [index name] in the request URI tells the service to return a count of all items in the docs collection of the specified index.</span></span>

<span data-ttu-id="57071-1035">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="57071-1035">`api-version=[string]` (required).</span></span> <span data-ttu-id="57071-1036">Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="57071-1036">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="57071-1037">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="57071-1037">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="57071-1038">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="57071-1038">**Request Headers**</span></span>

<span data-ttu-id="57071-1039">Aşağıdaki listede gerekli ve isteğe bağlı İstek üstbilgilerinin açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="57071-1039">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="57071-1040">`Accept`: Bu değer ayarlamak `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="57071-1040">`Accept`: This value must be set to `text/plain`.</span></span>
* <span data-ttu-id="57071-1041">`api-key``api-key` İsteğin arama hizmetiniz için kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-1041">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="57071-1042">Hizmet URL'nizi benzersiz bir dize değeri değil.</span><span class="sxs-lookup"><span data-stu-id="57071-1042">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="57071-1043">**Sayısı belgeleri** isteği, bir yönetici anahtarını veya sorgu anahtarı belirtebilirsiniz `api-key`.</span><span class="sxs-lookup"><span data-stu-id="57071-1043">The **Count Documents** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="57071-1044">İstek URL'si oluşturmak için hizmet adı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-1044">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="57071-1045">Hizmet adını alabilir ve `api-key` Azure Portalı'nda, hizmet panosundan.</span><span class="sxs-lookup"><span data-stu-id="57071-1045">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="57071-1046">Bkz: [portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="57071-1046">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="57071-1047">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="57071-1047">**Request Body**</span></span>

<span data-ttu-id="57071-1048">yok.</span><span class="sxs-lookup"><span data-stu-id="57071-1048">None.</span></span>

<span data-ttu-id="57071-1049">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="57071-1049">**Response**</span></span>

<span data-ttu-id="57071-1050">Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.</span><span class="sxs-lookup"><span data-stu-id="57071-1050">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="57071-1051">Yanıt gövdesi, düz metin olarak biçimlendirilmiş bir tamsayı olarak sayısı değeri içerir.</span><span class="sxs-lookup"><span data-stu-id="57071-1051">The response body contains the count value as an integer formatted in plain text.</span></span>

<a name="Suggestions"></a>

## <a name="suggestions"></a><span data-ttu-id="57071-1052">Öneriler</span><span class="sxs-lookup"><span data-stu-id="57071-1052">Suggestions</span></span>
<span data-ttu-id="57071-1053">**Önerileri** işlemi kısmi arama girişinize göre önerileri alır.</span><span class="sxs-lookup"><span data-stu-id="57071-1053">The **Suggestions** operation retrieves suggestions based on partial search input.</span></span> <span data-ttu-id="57071-1054">Bu genellikle, arama kutularında kullanıcılar arama terimi girerek yazarken tamamlanan öneriler sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-1054">It's typically used in search boxes to provide type-ahead suggestions as users are entering search terms.</span></span>

<span data-ttu-id="57071-1055">Öneri istekleri hedef belgeler, birden çok adayı belge giriş aynı arama eşleşiyorsa önerilen metin yinelenebilir şekilde öneren adresindeki hedefleyin.</span><span class="sxs-lookup"><span data-stu-id="57071-1055">Suggestion requests aim at suggesting target documents, so the suggested text may be repeated if multiple candidate documents match the same search input.</span></span> <span data-ttu-id="57071-1056">Kullanabileceğiniz `$select` , her bir öneri kaynağı belgedir yapıp yapmadığını (belge anahtar dahil) diğer belge alanları alınamadı.</span><span class="sxs-lookup"><span data-stu-id="57071-1056">You can use `$select` to retrieve other document fields (including the document key) so that you can tell which document is the source for each suggestion.</span></span>

<span data-ttu-id="57071-1057">A **önerileri** işlem bir GET veya POST isteği verildi.</span><span class="sxs-lookup"><span data-stu-id="57071-1057">A **Suggestions** operation is issued as a GET or POST request.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="57071-1058">**POST yerine GET kullanma zamanı**</span><span class="sxs-lookup"><span data-stu-id="57071-1058">**When to use POST instead of GET**</span></span>

<span data-ttu-id="57071-1059">Kullandığınızda, HTTP GET çağırmak için **önerileri** API, gereken isteği URL uzunluğu 8 KB'yi aşamaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="57071-1059">When you use HTTP GET to call the **Suggestions** API, you need to be aware that the length of the request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="57071-1060">Çoğu uygulama için yeterince genellikle budur.</span><span class="sxs-lookup"><span data-stu-id="57071-1060">This is usually enough for most applications.</span></span> <span data-ttu-id="57071-1061">Ancak, bazı uygulamalar çok büyük sorgular, özellikle OData filtre ifadeleri üretir.</span><span class="sxs-lookup"><span data-stu-id="57071-1061">However, some applications produce very large queries, specifically OData filter expressions.</span></span> <span data-ttu-id="57071-1062">GET daha büyük filtreleri sağladığından bu uygulamalar için HTTP POST kullanılarak daha iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="57071-1062">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span></span> <span data-ttu-id="57071-1063">POST ile bir filtre yan tümcelerinde POST isteği boyut sınırını yaklaşık 16 MB olduğundan ham filtre dizesi boyutu sınırlama faktörü sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-1063">With POST, the number of clauses in a filter is the limiting factor, not the size of the raw filter string since the request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-1064">POST isteği boyut sınırı çok büyük olsa da, filtre ifadeleri rasgele karmaşık olamaz.</span><span class="sxs-lookup"><span data-stu-id="57071-1064">Even though the POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="57071-1065">Bkz: [OData ifade sözdizimini](https://msdn.microsoft.com/library/dn798921.aspx) filtre karmaşıklık sınırlamalar hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="57071-1065">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="57071-1066">**İstek**</span><span class="sxs-lookup"><span data-stu-id="57071-1066">**Request**</span></span>

<span data-ttu-id="57071-1067">HTTPS istekleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="57071-1067">HTTPS is required for service requests.</span></span> <span data-ttu-id="57071-1068">**Önerileri** isteği GET veya POST yöntemleri kullanılarak olacak oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="57071-1068">The **Suggestions** request can be constructed using the GET or POST methods.</span></span>

<span data-ttu-id="57071-1069">İsteğin URI sorgu için dizin adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="57071-1069">The request URI specifies the name of the index to query.</span></span> <span data-ttu-id="57071-1070">Kısmen giriş arama terimi gibi parametreleri GET istekleri durumunda sorgu dizesinde belirtilen ve gövde POST söz konusu olduğunda istek ister.</span><span class="sxs-lookup"><span data-stu-id="57071-1070">Parameters, such as the partially input search term, are specified on the query string in the case of GET requests, and in the request body in the case of POST requests.</span></span>

<span data-ttu-id="57071-1071">GET isteklerini oluştururken en iyi uygulama, unutmayın [URL kodlama](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) REST API doğrudan çağrılırken belirli sorgu parametreleri.</span><span class="sxs-lookup"><span data-stu-id="57071-1071">As a best practice when creating GET requests, remember to [URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling the REST API directly.</span></span> <span data-ttu-id="57071-1072">İçin **önerileri** bu işlemleri içerir:</span><span class="sxs-lookup"><span data-stu-id="57071-1072">For **Suggestions** operations, this includes:</span></span>

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

<span data-ttu-id="57071-1073">URL kodlaması yalnızca yukarıdaki sorgu parametreleri önerilir.</span><span class="sxs-lookup"><span data-stu-id="57071-1073">URL encoding is only recommended on the above query parameters.</span></span> <span data-ttu-id="57071-1074">Varsa, yanlışlıkla URL kodlama tüm sorgu dizesi (sonra her şeyi?), istekleri bozar.</span><span class="sxs-lookup"><span data-stu-id="57071-1074">If you inadvertently URL-encode the entire query string (everything after the ?), requests will break.</span></span>

<span data-ttu-id="57071-1075">Ayrıca, URL kodlaması yalnızca GET kullanarak doğrudan REST API çağrılırken gereklidir.</span><span class="sxs-lookup"><span data-stu-id="57071-1075">Also, URL encoding is only necessary when calling the REST API directly using GET.</span></span> <span data-ttu-id="57071-1076">Hiçbir URL kodlaması çağrılırken gereklidir **önerileri** POST, kullanma ya da kullanırken [.NET istemci kitaplığını](https://msdn.microsoft.com/library/dn951165.aspx), sizin için URL kodlaması işler.</span><span class="sxs-lookup"><span data-stu-id="57071-1076">No URL encoding is necessary when calling **Suggestions** using POST, or when using the [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="57071-1077">**Sorgu parametreleri**</span><span class="sxs-lookup"><span data-stu-id="57071-1077">**Query Parameters**</span></span>

<span data-ttu-id="57071-1078">**Öneriler** sorgu ölçütlerini sağlayan ve ayrıca arama davranışını belirtin birkaç parametre kabul eder.</span><span class="sxs-lookup"><span data-stu-id="57071-1078">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="57071-1079">Bu parametreler URL'deki sorgu dizesi çağrılırken sağladığınız **önerileri** GET aracılığıyla ve çağrılırken istek gövdesinde JSON özellikleri olarak **önerileri** POST ile.</span><span class="sxs-lookup"><span data-stu-id="57071-1079">You provide these parameters in the URL query string when calling **Suggestions** via GET, and as JSON properties in the request body when calling **Suggestions** via POST.</span></span> <span data-ttu-id="57071-1080">Bazı parametreler sözdizimi GET ve POST arasında biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-1080">The syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="57071-1081">Bu farklılıklar, geçerli aşağıda belirtilmiştir:</span><span class="sxs-lookup"><span data-stu-id="57071-1081">These differences are noted as applicable below:</span></span>

<span data-ttu-id="57071-1082">`search=[string]`-sorguları önermek üzere kullanmak için arama metni.</span><span class="sxs-lookup"><span data-stu-id="57071-1082">`search=[string]` - the search text to use to suggest queries.</span></span> <span data-ttu-id="57071-1083">En az 1 karakter ve en fazla 100 karakter olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-1083">Must be at least 1 character, and no more than 100 characters.</span></span>

<span data-ttu-id="57071-1084">`highlightPreTag=[string]`(isteğe bağlı) - bir dize etiketi, isabet aramak için başına.</span><span class="sxs-lookup"><span data-stu-id="57071-1084">`highlightPreTag=[string]` (optional) - a string tag that prepends to search hits.</span></span> <span data-ttu-id="57071-1085">İle ayarlanmalıdır `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="57071-1085">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-1086">Çağrılırken **önerileri** GET kullanarak, URL'deki ayrılmış karakterler (örneğin, % &#23; yerine) yüzde olarak kodlanmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-1086">When calling **Suggestions** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="57071-1087">`highlightPostTag=[string]`(isteğe bağlı) - bir dize etiketi, isabet aramak için ekler.</span><span class="sxs-lookup"><span data-stu-id="57071-1087">`highlightPostTag=[string]` (optional) - a string tag that appends to search hits.</span></span> <span data-ttu-id="57071-1088">İle ayarlanmalıdır `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="57071-1088">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-1089">Çağrılırken **önerileri** GET kullanarak, URL'deki ayrılmış karakterler (örneğin, % &#23; yerine) yüzde olarak kodlanmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-1089">When calling **Suggestions** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="57071-1090">`suggesterName=[string]`-belirtildiği gibi öneri aracı adını `suggesters` dizin tanımı parçası olan koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="57071-1090">`suggesterName=[string]` - the name of the suggester as specified in the `suggesters` collection that's part of the index definition.</span></span> <span data-ttu-id="57071-1091">A `suggester` hangi alanlar için önerilen sorgu terimlerinin taranır belirler.</span><span class="sxs-lookup"><span data-stu-id="57071-1091">A `suggester` determines which fields are scanned for suggested query terms.</span></span> <span data-ttu-id="57071-1092">Bkz: [ilgili](#Suggesters) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="57071-1092">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="57071-1093">`fuzzy=[boolean]`(isteğe bağlı, varsayılan = false)-olsa bile bir yedek veya eksik karakter arama metni olarak ayarlandığında bu API true olarak öneriler bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="57071-1093">`fuzzy=[boolean]` (optional, default = false) - when set to true this API will find suggestions even if there's a substituted or missing character in the search text.</span></span> <span data-ttu-id="57071-1094">Bu bazı senaryolarda daha iyi bir deneyim sağlarken benzer bir öneri aramalar daha yavaş ve daha fazla kaynak tüketmesine maliyeti performanslarının gelir.</span><span class="sxs-lookup"><span data-stu-id="57071-1094">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span></span>

<span data-ttu-id="57071-1095">`searchFields=[string]`(isteğe bağlı): Belirtilen arama metni aramak için virgülle ayrılmış bir alan adları listesi.</span><span class="sxs-lookup"><span data-stu-id="57071-1095">`searchFields=[string]` (optional) - the list of comma-separated field names to search for the specified search text.</span></span> <span data-ttu-id="57071-1096">Hedef alan önerileri için etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-1096">Target fields must be enabled for suggestions.</span></span>

<span data-ttu-id="57071-1097">`$top=#`(isteğe bağlı, varsayılan = 5)-almak için öneriler sayısı.</span><span class="sxs-lookup"><span data-stu-id="57071-1097">`$top=#` (optional, default = 5) - the number of suggestions to retrieve.</span></span> <span data-ttu-id="57071-1098">1 ile 100 arasında bir sayı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="57071-1098">Must be a number between 1 and 100.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-1099">Çağrılırken **önerileri** POST kullanarak, bu parametre adlı `top` yerine `$top`.</span><span class="sxs-lookup"><span data-stu-id="57071-1099">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="57071-1100">`$filter=[string]`(isteğe bağlı) - belgeleri filtreleyen bir ifade için öneriler kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="57071-1100">`$filter=[string]` (optional) - an expression that filters the documents considered for suggestions.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-1101">Çağrılırken **önerileri** POST kullanarak, bu parametre adlı `filter` yerine `$filter`.</span><span class="sxs-lookup"><span data-stu-id="57071-1101">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="57071-1102">`$orderby=[string]`(isteğe bağlı) - sonuçlarına göre sıralamak için ifadeleri virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="57071-1102">`$orderby=[string]` (optional) - a list of comma-separated expressions to sort the results by.</span></span> <span data-ttu-id="57071-1103">Her bir ifadenin bir alan adı veya yapılan bir çağrı olabilir `geo.distance()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="57071-1103">Each expression can be either a field name or a call to the `geo.distance()` function.</span></span> <span data-ttu-id="57071-1104">Her deyim tarafından izlenebilir `asc` belirtildiği için artan ve `desc` azalan belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="57071-1104">Each expression can be followed by `asc` to indicated ascending, and `desc` to indicate descending.</span></span> <span data-ttu-id="57071-1105">Varsayılan, artan.</span><span class="sxs-lookup"><span data-stu-id="57071-1105">The default is ascending order.</span></span> <span data-ttu-id="57071-1106">Bir sınır için 32 yan `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="57071-1106">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-1107">Çağrılırken **önerileri** POST kullanarak, bu parametre adlı `orderby` yerine `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="57071-1107">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="57071-1108">`$select=[string]`(isteğe bağlı) - almak için bir alanlar virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="57071-1108">`$select=[string]` (optional) - a list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="57071-1109">Belirtilmezse, yalnızca belge anahtarını ve öneri metni döndürülür.</span><span class="sxs-lookup"><span data-stu-id="57071-1109">If unspecified, only the document key and suggestion text is returned.</span></span> <span data-ttu-id="57071-1110">Bu parametre ayarlayarak tüm alanları açıkça isteyebilir `*`.</span><span class="sxs-lookup"><span data-stu-id="57071-1110">You can explicitly request all fields by setting this parameter to `*`.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-1111">Çağrılırken **önerileri** POST kullanarak, bu parametre adlı `select` yerine `$select`.</span><span class="sxs-lookup"><span data-stu-id="57071-1111">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="57071-1112">`minimumCoverage`(isteğe bağlı, varsayılan olarak 80)-0 ve öneriler sorgu başarılı bildirilecek sorgu için sırasıyla tarafından ele alınması gereken dizin yüzdesini gösteren 100 arasında bir sayı.</span><span class="sxs-lookup"><span data-stu-id="57071-1112">`minimumCoverage` (optional, defaults to 80) - a number between 0 and 100 indicating the percentage of the index that must be covered by a suggestions query in order for the query to be reported as a success.</span></span> <span data-ttu-id="57071-1113">Varsayılan olarak, dizin % 80'en az kullanılabilir olmalıdır veya `Suggest` 503 HTTP durum kodunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="57071-1113">By default, at least 80% of the index must be available or `Suggest` will return HTTP status code 503.</span></span> <span data-ttu-id="57071-1114">Ayarlarsanız `minimumCoverage` ve `Suggest` başarılı, HTTP 200 dönün ve içeren bir `@search.coverage` sorguda eklenmiştir dizin yüzdesini gösteren yanıt değeri.</span><span class="sxs-lookup"><span data-stu-id="57071-1114">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in the response indicating the percentage of the index that was included in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="57071-1115">Bu parametre için bir değer 100'den daha düşük ayarı yalnızca bir çoğaltma hizmetleriyle için bile arama kullanılabilirlik sağlamak için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="57071-1115">Setting this parameter to a value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="57071-1116">Ancak, tüm eşleşen öneri sonuçlarında mevcut olması garanti.</span><span class="sxs-lookup"><span data-stu-id="57071-1116">However, not all matching suggestions are guaranteed to be present in the results.</span></span> <span data-ttu-id="57071-1117">Geri çağırma önemlidir kullanılabilirlik uygulamanızı daha sonra değil düşürmek en iyisidir `minimumCoverage` varsayılan değerini 80 aşağıda.</span><span class="sxs-lookup"><span data-stu-id="57071-1117">If recall is more important to your application than availability, then it's best not to lower `minimumCoverage` below its default value of 80.</span></span>
> 
> 

<span data-ttu-id="57071-1118">`api-version=[string]`(gerekli).</span><span class="sxs-lookup"><span data-stu-id="57071-1118">`api-version=[string]` (required).</span></span> <span data-ttu-id="57071-1119">Önizleme sürümü `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="57071-1119">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="57071-1120">Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.</span><span class="sxs-lookup"><span data-stu-id="57071-1120">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="57071-1121">Not: Bu işlem için `api-version` olup, çağrı bağımsız olarak URL'deki sorgu parametresi olarak belirtilen **önerileri** GET veya POST ile.</span><span class="sxs-lookup"><span data-stu-id="57071-1121">Note: For this operation, the `api-version` is specified as a query parameter in the URL regardless of whether you call **Suggestions** with GET or POST.</span></span>

<span data-ttu-id="57071-1122">**İstek üstbilgileri**</span><span class="sxs-lookup"><span data-stu-id="57071-1122">**Request Headers**</span></span>

<span data-ttu-id="57071-1123">Gerekli ve isteğe bağlı İstek üstbilgilerinin aşağıdaki listede açıklanmaktadır</span><span class="sxs-lookup"><span data-stu-id="57071-1123">The following list describes the required and optional request headers</span></span>

* <span data-ttu-id="57071-1124">`api-key``api-key` İsteğin arama hizmetiniz için kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57071-1124">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="57071-1125">Hizmet URL'nizi benzersiz bir dize değeri değil.</span><span class="sxs-lookup"><span data-stu-id="57071-1125">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="57071-1126">**Önerileri** isteği, bir yönetici anahtarını veya sorgu anahtarı olarak belirtebilirsiniz `api-key`.</span><span class="sxs-lookup"><span data-stu-id="57071-1126">The **Suggestions** request can specify either an admin key or query key as the `api-key`.</span></span>

<span data-ttu-id="57071-1127">İstek URL'si oluşturmak için hizmet adı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="57071-1127">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="57071-1128">Hizmet adını alabilir ve `api-key` Azure Portalı'nda, hizmet panosundan.</span><span class="sxs-lookup"><span data-stu-id="57071-1128">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="57071-1129">Bkz: [portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.</span><span class="sxs-lookup"><span data-stu-id="57071-1129">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="57071-1130">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="57071-1130">**Request Body**</span></span>

<span data-ttu-id="57071-1131">GET için: yok.</span><span class="sxs-lookup"><span data-stu-id="57071-1131">For GET: None.</span></span>

<span data-ttu-id="57071-1132">POST için:</span><span class="sxs-lookup"><span data-stu-id="57071-1132">For POST:</span></span>

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered to declare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

<span data-ttu-id="57071-1133">**Yanıt**</span><span class="sxs-lookup"><span data-stu-id="57071-1133">**Response**</span></span>

<span data-ttu-id="57071-1134">Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.</span><span class="sxs-lookup"><span data-stu-id="57071-1134">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

<span data-ttu-id="57071-1135">Dizinin her bir öğesinde bulunan alanları almak için yansıtma seçeneği kullandıysanız:</span><span class="sxs-lookup"><span data-stu-id="57071-1135">If the projection option is used to retrieve fields they are included in each element of the array:</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

<span data-ttu-id="57071-1136">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="57071-1136">**Example**</span></span>

<span data-ttu-id="57071-1137">Kısmi arama giriş 'lux' olduğu 5 önerileri Al</span><span class="sxs-lookup"><span data-stu-id="57071-1137">Retrieve 5 suggestions where the partial search input is 'lux'</span></span>

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
