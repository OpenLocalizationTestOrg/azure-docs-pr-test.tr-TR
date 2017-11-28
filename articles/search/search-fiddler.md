---
title: aaaHow toouse Fiddler tooevaluate ve Azure Search REST API'lerini test | Microsoft Docs
description: "Bir yaklaşım Kodsuz tooverifying Azure Search hizmetinin kullanılabilirliğini ve REST API'leri hello çalışırken için fiddler'ı kullanın."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: 790e5779-c6a3-4a07-9d1e-d6739e6b87d2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: 2912e1180717d7b40a1e4f7f7f00daf2cc254f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a><span data-ttu-id="b4973-103">Fiddler tooevaluate kullanın ve Azure Search REST API'lerini test etme</span><span class="sxs-lookup"><span data-stu-id="b4973-103">Use Fiddler tooevaluate and test Azure Search REST APIs</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="b4973-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b4973-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="b4973-105">Arama Gezgini</span><span class="sxs-lookup"><span data-stu-id="b4973-105">Search Explorer</span></span>](search-explorer.md)
> * [<span data-ttu-id="b4973-106">Fiddler</span><span class="sxs-lookup"><span data-stu-id="b4973-106">Fiddler</span></span>](search-fiddler.md)
> * [<span data-ttu-id="b4973-107">.NET</span><span class="sxs-lookup"><span data-stu-id="b4973-107">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="b4973-108">REST</span><span class="sxs-lookup"><span data-stu-id="b4973-108">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="b4973-109">Bu makalede açıklanır nasıl toouse Fiddler'ın, bir [telerik'ten ücretsiz indirme](http://www.telerik.com/fiddler), herhangi bir kod toowrite gerek kalmadan hello Azure Search REST API'sini kullanarak tooissue HTTP isteklerini tooand yanıtları görüntüle.</span><span class="sxs-lookup"><span data-stu-id="b4973-109">This article explains how toouse Fiddler, available as a [free download from Telerik](http://www.telerik.com/fiddler), tooissue HTTP requests tooand view responses using hello Azure Search REST API, without having toowrite any code.</span></span> <span data-ttu-id="b4973-110">Azure Search; Microsoft Azure'da barındırılan, .NET ve REST API'ler aracılığıyla kolayca programlanabilen ve tamamen yönetilen bir bulut arama hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="b4973-110">Azure Search is fully-managed, hosted cloud search service on Microsoft Azure, easily programmable through .NET and REST APIs.</span></span> <span data-ttu-id="b4973-111">Hello Azure Search Hizmeti REST API'leri açıklanmaktadır [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4973-111">hello Azure Search service REST APIs are documented on [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span></span>

<span data-ttu-id="b4973-112">Aşağıdaki adımları hello dizin oluşturma, belgeleri, sorgu hello dizini ve ardından hizmet bilgisi için sorgu hello sistemi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b4973-112">In hello following steps, you'll create an index, upload documents, query hello index, and then query hello system for service information.</span></span>

<span data-ttu-id="b4973-113">Aşağıdaki adımları toocomplete, Azure Search hizmeti gerekir ve `api-key`.</span><span class="sxs-lookup"><span data-stu-id="b4973-113">toocomplete these steps, you will need an Azure Search service and `api-key`.</span></span> <span data-ttu-id="b4973-114">Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) tooget nasıl başlatılacağını hakkında yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="b4973-114">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for instructions on how tooget started.</span></span>

## <a name="create-an-index"></a><span data-ttu-id="b4973-115">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="b4973-115">Create an index</span></span>
1. <span data-ttu-id="b4973-116">Fiddler'ı başlatın.</span><span class="sxs-lookup"><span data-stu-id="b4973-116">Start Fiddler.</span></span> <span data-ttu-id="b4973-117">Merhaba üzerinde **dosya** menüsünde kapatmak **trafiği Yakala** ilgisiz toohello geçerli görev toohide yabancı HTTP etkinliğini.</span><span class="sxs-lookup"><span data-stu-id="b4973-117">On hello **File** menu, turn off **Capture Traffic** toohide extraneous HTTP activity that is unrelated toohello current task.</span></span>
2. <span data-ttu-id="b4973-118">Merhaba üzerinde **Oluşturucu** sekmesinde, aşağıdaki ekran görüntüsü hello gibi görünen bir istek formüle.</span><span class="sxs-lookup"><span data-stu-id="b4973-118">On hello **Composer** tab, you'll formulate a request that looks like hello following screen shot.</span></span>

      ![][1]
3. <span data-ttu-id="b4973-119">**PUT**'u seçin.</span><span class="sxs-lookup"><span data-stu-id="b4973-119">Select **PUT**.</span></span>
4. <span data-ttu-id="b4973-120">Hello hizmet URL'si, istek özniteliklerini ve hello api sürümü belirten bir URL girin.</span><span class="sxs-lookup"><span data-stu-id="b4973-120">Enter a URL that specifies hello service URL, request attributes, and hello api-version.</span></span> <span data-ttu-id="b4973-121">Birkaç işaretçileri tookeep unutmayın:</span><span class="sxs-lookup"><span data-stu-id="b4973-121">A few pointers tookeep in mind:</span></span>

   * <span data-ttu-id="b4973-122">HTTPS hello önek olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="b4973-122">Use HTTPS as hello prefix.</span></span>
   * <span data-ttu-id="b4973-123">İstek özniteliği "indexes/hotels"dir.</span><span class="sxs-lookup"><span data-stu-id="b4973-123">Request attribute is "/indexes/hotels".</span></span> <span data-ttu-id="b4973-124">Bu, "Oteller" adlı bir dizin arama toocreate bildirir.</span><span class="sxs-lookup"><span data-stu-id="b4973-124">This tells Search toocreate an index named 'hotels'.</span></span>
   * <span data-ttu-id="b4973-125">API sürümü küçük harfle yazılır, "?api-version=2016-09-01" olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="b4973-125">Api-version is lowercase, specified as "?api-version=2016-09-01".</span></span> <span data-ttu-id="b4973-126">Azure Search düzenli olarak güncelleştirme dağıttığından, API sürümleri önemlidir.</span><span class="sxs-lookup"><span data-stu-id="b4973-126">API versions are important because Azure Search deploys updates regularly.</span></span> <span data-ttu-id="b4973-127">Nadir durumlarda, bir hizmet güncelleştirmesi sonu değişiklik toohello API çıkarabilir.</span><span class="sxs-lookup"><span data-stu-id="b4973-127">On rare occasions, a service update may introduce a breaking change toohello API.</span></span> <span data-ttu-id="b4973-128">Bu nedenle Azure Search, her bir istek için api sürümünü gerekli kılar. Böylece, hangisinin kullanıldığına ilişkin tam denetiminiz olur.</span><span class="sxs-lookup"><span data-stu-id="b4973-128">For this reason, Azure Search requires an api-version on each request so that you are in full control over which one is used.</span></span>

     <span data-ttu-id="b4973-129">Merhaba tam URL aşağıdaki örneğine benzer toohello görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="b4973-129">hello full URL should look similar toohello following example.</span></span>

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. <span data-ttu-id="b4973-130">Merhaba konak ve api anahtarını hizmetiniz için geçerli olan değerleri değiştirerek hello istek üstbilgisi belirtin.</span><span class="sxs-lookup"><span data-stu-id="b4973-130">Specify hello request header, replacing hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. <span data-ttu-id="b4973-131">İstek gövdesinde hello dizin tanımını oluşturan hello alanları yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b4973-131">In Request Body, paste in hello fields that make up hello index definition.</span></span>

          {
         "name": "hotels",  
         "fields": [
           {"name": "hotelId", "type": "Edm.String", "key":true, "searchable": false},
           {"name": "baseRate", "type": "Edm.Double"},
           {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
           {"name": "hotelName", "type": "Edm.String"},
           {"name": "category", "type": "Edm.String"},
           {"name": "tags", "type": "Collection(Edm.String)"},
           {"name": "parkingIncluded", "type": "Edm.Boolean"},
           {"name": "smokingAllowed", "type": "Edm.Boolean"},
           {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
           {"name": "rating", "type": "Edm.Int32"},
           {"name": "location", "type": "Edm.GeographyPoint"}
          ]
         }
7. <span data-ttu-id="b4973-132">**Yürüt**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b4973-132">Click **Execute**.</span></span>

<span data-ttu-id="b4973-133">Birkaç saniye içinde HTTP 201 yanıtını hello oturum listesinde görmeniz gerekir, belirten hello Dizin başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="b4973-133">In a few seconds, you should see an HTTP 201 response in hello session list, indicating hello index was created successfully.</span></span>

<span data-ttu-id="b4973-134">HTTP 504 yanıtı alırsanız HTTPS'yi belirten hello URL'yi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b4973-134">If you get HTTP 504, verify hello URL specifies HTTPS.</span></span> <span data-ttu-id="b4973-135">HTTP 400 veya 404 yanıtı görürseniz, onay hello istek gövdesi tooverify var. hatalar hiçbir kopyalayıp yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b4973-135">If you see HTTP 400 or 404, check hello request body tooverify there were no copy-paste errors.</span></span> <span data-ttu-id="b4973-136">HTTP 403 genelde hello api anahtarını (Geçersiz anahtar veya hello api anahtarını nasıl belirtilen bir söz dizimi sorunu) bir sorun olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="b4973-136">An HTTP 403 typically indicates a problem with hello api-key (either an invalid key or a syntax problem with how hello api-key is specified).</span></span>

## <a name="load-documents"></a><span data-ttu-id="b4973-137">Belge yükleme</span><span class="sxs-lookup"><span data-stu-id="b4973-137">Load documents</span></span>
<span data-ttu-id="b4973-138">Merhaba üzerinde **Oluşturucu** sekmesi, istek toopost belgelerinizi hello aşağıdaki gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="b4973-138">On hello **Composer** tab, your request toopost documents will look like hello following.</span></span> <span data-ttu-id="b4973-139">Merhaba hello istek gövdesi 4 otel için arama verilerini hello içerir.</span><span class="sxs-lookup"><span data-stu-id="b4973-139">hello body of hello request contains hello search data for 4 hotels.</span></span>

   ![][2]

1. <span data-ttu-id="b4973-140">**POST**'u seçin.</span><span class="sxs-lookup"><span data-stu-id="b4973-140">Select **POST**.</span></span>
2. <span data-ttu-id="b4973-141">HTTPS ile başlayan, sırasıyla hizmet URL'niz ve "/indexes/<'indexname'>/docs/index?api-version=2016-09-01" ile devam eden bir URL girin.</span><span class="sxs-lookup"><span data-stu-id="b4973-141">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span></span> <span data-ttu-id="b4973-142">Merhaba tam URL aşağıdaki örneğine benzer toohello görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="b4973-142">hello full URL should look similar toohello following example.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. <span data-ttu-id="b4973-143">İstek üstbilgisi olması hello aynı önceki gibi.</span><span class="sxs-lookup"><span data-stu-id="b4973-143">Request Header should be hello same as before.</span></span> <span data-ttu-id="b4973-144">Hizmetiniz için geçerli değerlerle hello konak ve api anahtarını yerini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b4973-144">Remember that you replaced hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="b4973-145">Merhaba iste gövde dört belgeleri toobe eklenen toohello hotels dizini içerir.</span><span class="sxs-lookup"><span data-stu-id="b4973-145">hello Request Body contains four documents toobe added toohello hotels index.</span></span>

         {
         "value": [
         {
             "@search.action": "upload",
             "hotelId": "1",
             "baseRate": 199.0,
             "description": "Best hotel in town",
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
             "@search.action": "upload",
             "hotelId": "3",
             "baseRate": 279.99,
             "description": "Surprisingly expensive",
             "hotelName": "Dew Drop Inn",
             "category": "Bed and Breakfast",
             "tags": ["charming", "quaint"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.33207, 47.60621] }
           },
           {
             "@search.action": "upload",
             "hotelId": "4",
             "baseRate": 220.00,
             "description": "This could be hello one",
             "hotelName": "A Hotel for Everyone",
             "category": "Basic hotel",
             "tags": ["pool", "wifi"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.12151, 47.67399] }
           }
          ]
         }
5. <span data-ttu-id="b4973-146">**Yürüt**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b4973-146">Click **Execute**.</span></span>

<span data-ttu-id="b4973-147">Birkaç saniye içinde bir hello oturum listesinde HTTP 200 yanıtı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4973-147">In a few seconds, you should see an HTTP 200 response in hello session list.</span></span> <span data-ttu-id="b4973-148">Bu, belgelerin başarıyla oluşturulduğunu hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="b4973-148">This indicates hello documents were created successfully.</span></span> <span data-ttu-id="b4973-149">207 yanıtı alırsanız en az bir belge tooupload başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="b4973-149">If you get a 207, at least one document failed tooupload.</span></span> <span data-ttu-id="b4973-150">404 yanıtı alırsanız, hello üstbilgi veya hello istek gövdesi bir sözdizimi hatası var.</span><span class="sxs-lookup"><span data-stu-id="b4973-150">If you get a 404, you have a syntax error in either hello header or body of hello request.</span></span>

## <a name="query-hello-index"></a><span data-ttu-id="b4973-151">Sorgu hello dizini</span><span class="sxs-lookup"><span data-stu-id="b4973-151">Query hello index</span></span>
<span data-ttu-id="b4973-152">Şimdi dizin ve belgeler karşıya yüklendiğine göre, bunlara sorgu gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4973-152">Now that an index and documents are loaded, you can issue queries against them.</span></span>  <span data-ttu-id="b4973-153">Merhaba üzerinde **Oluşturucu** sekmesinde bir **almak** hizmetinizi sorgulayan komutu aşağıdaki ekran görüntüsü benzer toohello görünür.</span><span class="sxs-lookup"><span data-stu-id="b4973-153">On hello **Composer** tab, a **GET** command that queries your service will look similar toohello following screen shot.</span></span>

   ![][3]

1. <span data-ttu-id="b4973-154">**GET**'i seçin.</span><span class="sxs-lookup"><span data-stu-id="b4973-154">Select **GET**.</span></span>
2. <span data-ttu-id="b4973-155">HTTPS ile başlayan, sırasıyla hizmet URL'niz, "/indexes/<'indexname'>/docs?" ve sorgu parametreleri ile devam eden bir URL girin.</span><span class="sxs-lookup"><span data-stu-id="b4973-155">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs?", followed by query parameters.</span></span> <span data-ttu-id="b4973-156">Örnek olarak, URL aşağıdaki, hizmetiniz için geçerli olan bir hello örnek ana bilgisayar adı yerine hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b4973-156">By way of example, use hello following URL, replacing hello sample host name with one that is valid for your service.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   <span data-ttu-id="b4973-157">Bu sorgu "motel" Merhaba terimini arar ve derecelendirmeler için model kategorileri alır.</span><span class="sxs-lookup"><span data-stu-id="b4973-157">This query searches on hello term “motel” and retrieves facet categories for ratings.</span></span>
3. <span data-ttu-id="b4973-158">İstek üstbilgisi olması hello aynı önceki gibi.</span><span class="sxs-lookup"><span data-stu-id="b4973-158">Request Header should be hello same as before.</span></span> <span data-ttu-id="b4973-159">Hizmetiniz için geçerli değerlerle hello konak ve api anahtarını yerini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b4973-159">Remember that you replaced hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

<span data-ttu-id="b4973-160">Merhaba yanıt kodu 200 olmalıdır ve hello yanıt çıkışı aşağıdaki ekran görüntüsü benzer toohello görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="b4973-160">hello response code should be 200, and hello response output should look similar toohello following screen shot.</span></span>

   ![][4]

<span data-ttu-id="b4973-161">Merhaba aşağıdaki örnek sorgu olan hello [Search dizin işlemi (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="b4973-161">hello following example query is from hello [Search Index operation (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) on MSDN.</span></span> <span data-ttu-id="b4973-162">Bu konudaki hello örnek sorguları çoğunu Fiddler'da izin verilmeyen boşluklar içerir.</span><span class="sxs-lookup"><span data-stu-id="b4973-162">Many of hello example queries in this topic include spaces, which are not allowed in Fiddler.</span></span> <span data-ttu-id="b4973-163">Her alanı ile + karakteri hello yapıştırarak sorgu önce dize hello fiddler'da sorguyu denemeden önce değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b4973-163">Replace each space with a + character before pasting in hello query string before attempting hello query in Fiddler.</span></span>

<span data-ttu-id="b4973-164">**Boşluklar değiştirilmeden önce:**</span><span class="sxs-lookup"><span data-stu-id="b4973-164">**Before spaces are replaced:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

<span data-ttu-id="b4973-165">**Boşluklar + ile değiştirildikten sonra:**</span><span class="sxs-lookup"><span data-stu-id="b4973-165">**After spaces are replaced with +:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a><span data-ttu-id="b4973-166">Sorgu hello sistemi</span><span class="sxs-lookup"><span data-stu-id="b4973-166">Query hello system</span></span>
<span data-ttu-id="b4973-167">Sayıları ve depolama hello sistem tooget belge kullanımı da sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4973-167">You can also query hello system tooget document counts and storage consumption.</span></span> <span data-ttu-id="b4973-168">Merhaba üzerinde **Oluşturucu** sekmesinde isteğiniz benzer toohello aşağıdaki görünür ve hello yanıt Merhaba, belge sayısı ve kullanılan alan için bir sayı döndürür.</span><span class="sxs-lookup"><span data-stu-id="b4973-168">On hello **Composer** tab, your request will look similar toohello following, and hello response will return a count for hello number of documents and space used.</span></span>

 ![][5]

1. <span data-ttu-id="b4973-169">**GET**'i seçin.</span><span class="sxs-lookup"><span data-stu-id="b4973-169">Select **GET**.</span></span>
2. <span data-ttu-id="b4973-170">Hizmet URL'nizi içeren ve ardından "/indexes/hotels/stats?api-version=2016-09-01" ile devam eden bir URL girin:</span><span class="sxs-lookup"><span data-stu-id="b4973-170">Enter a URL that includes your service URL, followed by "/indexes/hotels/stats?api-version=2016-09-01":</span></span>

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. <span data-ttu-id="b4973-171">Merhaba konak ve api anahtarını hizmetiniz için geçerli olan değerleri değiştirerek hello istek üstbilgisi belirtin.</span><span class="sxs-lookup"><span data-stu-id="b4973-171">Specify hello request header, replacing hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="b4973-172">Merhaba istek gövdesini boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="b4973-172">Leave hello request body empty.</span></span>
5. <span data-ttu-id="b4973-173">**Yürüt**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b4973-173">Click **Execute**.</span></span> <span data-ttu-id="b4973-174">Bir HTTP 200 durum kodu hello oturum listesinde görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4973-174">You should see an HTTP 200 status code in hello session list.</span></span> <span data-ttu-id="b4973-175">Komutunuz için gönderilen hello girişi seçin.</span><span class="sxs-lookup"><span data-stu-id="b4973-175">Select hello entry posted for your command.</span></span>
6. <span data-ttu-id="b4973-176">Merhaba tıklatın **denetçiler** sekmesini ve ardından hello **üstbilgileri** sekmesini ve ardından hello JSON biçimi.</span><span class="sxs-lookup"><span data-stu-id="b4973-176">Click hello **Inspectors** tab, click hello **Headers** tab, and then select hello JSON format.</span></span> <span data-ttu-id="b4973-177">Merhaba belge sayısını ve depolama boyutu (KB) görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4973-177">You should see hello document count and storage size (in KB).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4973-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b4973-178">Next steps</span></span>
<span data-ttu-id="b4973-179">Bkz: [azure'da Search hizmetinizi yönetme](search-manage.md) kod içermeyen bir yaklaşım toomanaging ve Azure Search kullanma.</span><span class="sxs-lookup"><span data-stu-id="b4973-179">See [Manage your Search service on Azure](search-manage.md) for a no-code approach toomanaging and using Azure Search.</span></span>

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
