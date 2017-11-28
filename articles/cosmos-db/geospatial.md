---
title: "Azure Cosmos veritabanı Jeo-uzamsal verilerle aaaWorking | Microsoft Docs"
description: "Nasıl toocreate, dizin ve Azure Cosmos DB uzamsal nesneleriyle sorgulamak ve DocumentDB API hello anlayın."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 82ce2898-a9f9-4acf-af4d-8ca4ba9c7b8f
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/22/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1e40b78cb4595631d845d46c21d07a30c8b972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="1b0e6-103">Jeo-uzamsal ve Azure Cosmos veritabanı GeoJSON konum verileri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="1b0e6-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="1b0e6-104">Bu makalede bir giriş toohello Jeo-uzamsal işlevindeki olan [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="1b0e6-104">This article is an introduction toohello geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="1b0e6-105">Bu okuduktan sonra aşağıdaki soruları mümkün tooanswer hello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="1b0e6-105">After reading this, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="1b0e6-106">Azure Cosmos DB'de nasıl uzamsal veri depoluyor?</span><span class="sxs-lookup"><span data-stu-id="1b0e6-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="1b0e6-107">Azure Cosmos DB'de SQL ve LINQ Jeo-uzamsal verileri nasıl sorgulama yapabilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="1b0e6-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="1b0e6-108">Nasıl etkinleştirmek veya Azure Cosmos DB'de uzamsal dizin oluşturmayı devre dışı?</span><span class="sxs-lookup"><span data-stu-id="1b0e6-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="1b0e6-109">Bu makalede nasıl toowork uzamsal verilerle ile Merhaba DocumentDB API gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-109">This article shows how toowork with spatial data with hello DocumentDB API.</span></span> <span data-ttu-id="1b0e6-110">Lütfen bu bakın [GitHub proje](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) kod örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-toospatial-data"></a><span data-ttu-id="1b0e6-111">Giriş toospatial veri</span><span class="sxs-lookup"><span data-stu-id="1b0e6-111">Introduction toospatial data</span></span>
<span data-ttu-id="1b0e6-112">Uzamsal veri hello konumu ve Şekil alanı nesnelerin açıklar.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-112">Spatial data describes hello position and shape of objects in space.</span></span> <span data-ttu-id="1b0e6-113">Çoğu uygulamada bu Merhaba Dünya, yani Jeo-uzamsal veriler üzerindeki tooobjects karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-113">In most applications, these correspond tooobjects on hello earth, i.e. geospatial data.</span></span> <span data-ttu-id="1b0e6-114">Uzamsal veriler, bir kişinin kullanılan toorepresent hello konum, ilgilendiğiniz bir yerde ya da bir şehir veya bir lake hello sınırını olabilir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-114">Spatial data can be used toorepresent hello location of a person, a place of interest, or hello boundary of a city, or a lake.</span></span> <span data-ttu-id="1b0e6-115">Ortak kullanım durumları yakınlık sorguları, örneğin, "tüm kafeterya my geçerli konumu bulmak" için sıklıkla içerir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="1b0e6-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="1b0e6-116">GeoJSON</span></span>
<span data-ttu-id="1b0e6-117">Dizin oluşturma ve hello kullanarak temsil edilen Jeo-uzamsal noktası verileri Sorgulama Azure Cosmos DB destekler [GeoJSON belirtimi](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="1b0e6-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using hello [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="1b0e6-118">Böylece depolanabilir ve herhangi bir özel araçlar veya kitaplıkları Azure Cosmos DB kullanarak sorgulanan GeoJSON veri yapıları her zaman geçerli JSON, nesneleridir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="1b0e6-119">Hello Azure Cosmos DB SDK'ları yardımcı sınıfları ve uzamsal verileri içeren kolay toowork olun yöntemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-119">hello Azure Cosmos DB SDKs provide helper classes and methods that make it easy toowork with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="1b0e6-120">Noktaları, MultiPoint ve çokgenler</span><span class="sxs-lookup"><span data-stu-id="1b0e6-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="1b0e6-121">A **noktası** alanı tek bir konumda gösterir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="1b0e6-122">Jeo-uzamsal verileri bir noktası Market, bir bilgi noktası, bir otomobil veya bir şehir sokak adresi olabilir hello tam konumunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-122">In geospatial data, a Point represents hello exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="1b0e6-123">Bir noktayı kendi koordinat kullanarak GeoJSON (ve Azure Cosmos DB) çifti veya boylam ve enlem temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="1b0e6-124">Bir noktası için JSON örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="1b0e6-125">**Azure Cosmos DB noktaları**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="1b0e6-126">Merhaba GeoJSON belirtimi belirtir boylam ilk ve enlem ikinci.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-126">hello GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="1b0e6-127">Gibi diğer eşleme uygulamalarda boylam ve enlem açıları ve derece cinsinden temsil.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="1b0e6-128">Boylam değerleri Meridyeninden hello ölçülür ve -180 ve 180.0 derece ve enlem değerleri hello ekvatora ölçülür ve-90.0 arasında olan ve 90.0 derece.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-128">Longitude values are measured from hello Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from hello equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="1b0e6-129">Azure Cosmos DB koordinatları hello WGS 84 başvuru sistemi belirtildiği şekilde yorumlar.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-129">Azure Cosmos DB interprets coordinates as represented per hello WGS-84 reference system.</span></span> <span data-ttu-id="1b0e6-130">Lütfen koordinat başvuru sistemleri hakkında daha fazla bilgi için aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="1b0e6-131">Bu bir Azure Cosmos DB belgesinde konum verileri içeren bir kullanıcı profili bu örnekte gösterildiği gibi katıştırılabilen:</span><span class="sxs-lookup"><span data-stu-id="1b0e6-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="1b0e6-132">**Azure Cosmos DB içinde depolanan konumla profilini kullan**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

```json
{
    "id":"documentdb-profile",
    "screen_name":"@CosmosDB",
    "city":"Redmond",
    "topics":[ "global", "distributed" ],
    "location":{
        "type":"Point",
        "coordinates":[ 31.9, -4.8 ]
    }
}
```

<span data-ttu-id="1b0e6-133">Ayrıca toopoints, GeoJSON MultiPoint ve çokgenler destekler.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-133">In addition toopoints, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="1b0e6-134">**MultiPoint** alanı iki veya daha fazla noktaları bir dizi temsil eder ve bunları bağlamak çizgi dilimleri hello.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-134">**LineStrings** represent a series of two or more points in space and hello line segments that connect them.</span></span> <span data-ttu-id="1b0e6-135">Jeo-uzamsal verinin, yaygın olarak kullanılan toorepresent Otoyollar veya rivers MultiPoint içindedir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-135">In geospatial data, LineStrings are commonly used toorepresent highways or rivers.</span></span> <span data-ttu-id="1b0e6-136">A **Çokgen** kapalı LineString forms bir sınırı bağlı noktalarının.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="1b0e6-137">Çokgenler Göller gibi yaygın olarak kullanılan toorepresent doğal durum oluşumlarıyla veya şehir ve durumlar gibi siyasi daireleri markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-137">Polygons are commonly used toorepresent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="1b0e6-138">Burada, Azure Cosmos veritabanı çokgenin bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="1b0e6-139">**GeoJSON'daki çokgenler**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-139">**Polygons in GeoJSON**</span></span>

```json
{
    "type":"Polygon",
    "coordinates":[
        [ 31.8, -5 ],
        [ 31.8, -4.7 ],
        [ 32, -4.7 ],
        [ 32, -5 ],
        [ 31.8, -5 ]
    ]
}
```

> [!NOTE]
> <span data-ttu-id="1b0e6-140">Merhaba geçerli çokgenler için hello sağlanan son koordinat çifti olması gerektiğini belirtilmesini gerektiriyor GeoJSON hello aynı hello ilk toocreate kapalı bir şekil.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-140">hello GeoJSON specification requires that for valid Polygons, hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span>
> 
> <span data-ttu-id="1b0e6-141">Çokgen içindeki noktaları yönünün sırayla belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="1b0e6-142">Belirtilen saat yönünde sırayla Çokgen hello bölgesinde hello tersini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-142">A Polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>
> 
> 

<span data-ttu-id="1b0e6-143">Ayrıca tooPoint, LineString ve Çokgen GeoJSON de nasıl hello gösterimi belirtir. toogroup yanı sıra birden çok Jeo-uzamsal konumları tooassociate rasgele coğrafi konuma özelliklerle bir **özelliği**.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-143">In addition tooPoint, LineString and Polygon, GeoJSON also specifies hello representation for how toogroup multiple geospatial locations, as well as how tooassociate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="1b0e6-144">Bu nesneler geçerli JSON olduğundan, bunlar tüm depolanabilir ve Azure Cosmos DB'de işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="1b0e6-145">Ancak Azure Cosmos DB yalnızca noktalarının otomatik dizin oluşturma işlemi destekler.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="1b0e6-146">Koordinat başvuru sistemleri</span><span class="sxs-lookup"><span data-stu-id="1b0e6-146">Coordinate reference systems</span></span>
<span data-ttu-id="1b0e6-147">Merhaba Dünya Hello şeklini düzensiz olduğundan Jeo-uzamsal veri koordinatlarını sistemlerindeki birçok koordinat başvurusu (CR), her biri kendi çerçeveler başvuru ve ölçü gösterilir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-147">Since hello shape of hello earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="1b0e6-148">Örneğin, "Britanya Ulusal kılavuz" Merhaba başvuru sistemi çok doğru ise hello İngiltere, ancak değil dışında.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-148">For example, hello "National Grid of Britain" is a reference system is very accurate for hello United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="1b0e6-149">Merhaba kullanımda en popüler CRS bugün hello World Geodetic sistem olan [WGS 84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="1b0e6-149">hello most popular CRS in use today is hello World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="1b0e6-150">GPS aygıtları ve Google Haritalar ve Bing haritaları API'si dahil olmak üzere birçok eşleme Hizmetleri WGS 84 kullanın.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="1b0e6-151">Azure Cosmos DB dizin oluşturma ve Jeo-uzamsal verileri yalnızca WGS 84 CRS hello kullanarak sorgulama destekler.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-151">Azure Cosmos DB supports indexing and querying of geospatial data using hello WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="1b0e6-152">Uzamsal verilerle belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="1b0e6-152">Creating documents with spatial data</span></span>
<span data-ttu-id="1b0e6-153">GeoJSON değerleri içeren belgeleri oluşturduğunuzda, bunlar otomatik olarak uygun toohello dizin oluşturma ilkesi hello koleksiyonunun uzamsal dizine sahip dizine alınır.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance toohello indexing policy of hello collection.</span></span> <span data-ttu-id="1b0e6-154">Bir Azure Cosmos DB SDK'sı ile Python veya Node.js gibi dinamik olarak yazılan bir dilde çalışıyorsanız, geçerli GeoJSON oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="1b0e6-155">**Node.js içinde Jeo-uzamsal verilerle belge oluşturma**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-155">**Create Document with Geospatial data in Node.js**</span></span>

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within hello callback
});
```

<span data-ttu-id="1b0e6-156">Merhaba DocumentDB API'leri ile çalışıyorsanız, hello kullanabilirsiniz `Point` ve `Polygon` hello sınıfları `Microsoft.Azure.Documents.Spatial` uygulama nesnelerinizi içindeki ad alanı tooembed konum bilgileri.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-156">If you're working with hello DocumentDB APIs, you can use hello `Point` and `Polygon` classes within hello `Microsoft.Azure.Documents.Spatial` namespace tooembed location information within your application objects.</span></span> <span data-ttu-id="1b0e6-157">Bu sınıfların hello seri hale getirme ve seri durumdan çıkarma uzamsal veri GeoJSON içine kolaylaştırmaya yardımcı.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-157">These classes help simplify hello serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="1b0e6-158">**.NET Jeo-uzamsal verilerle belge oluşturma**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-158">**Create Document with Geospatial data in .NET**</span></span>

```json
using Microsoft.Azure.Documents.Spatial;

public class UserProfile
{
    [JsonProperty("name")]
    public string Name { get; set; }

    [JsonProperty("location")]
    public Point Location { get; set; }

    // More properties
}

await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "profiles"), 
    new UserProfile 
    { 
        Name = "documentdb", 
        Location = new Point (-122.12, 47.66) 
    });
```

<span data-ttu-id="1b0e6-159">Merhaba enlem ve boylam bilgilere sahip değilseniz, ancak hello fiziksel adreslerini veya şehir veya ülke gibi konum adı, Bing Haritalar REST Hizmetleri gibi bir coğrafi kodlama hizmet kullanarak hello gerçek koordinatları bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-159">If you don't have hello latitude and longitude information, but have hello physical addresses or location name like city or country, you can look up hello actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="1b0e6-160">Bing Haritalar coğrafi kodlama hakkında daha fazla bilgi [burada](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b0e6-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="1b0e6-161">Uzamsal türler sorgulama</span><span class="sxs-lookup"><span data-stu-id="1b0e6-161">Querying spatial types</span></span>
<span data-ttu-id="1b0e6-162">Biz nasıl göz ayırdıktan göre tooinsert Jeo-uzamsal veriler, nasıl bir göz atalım tooquery Azure Cosmos SQL ve LINQ kullanarak DB kullanarak bu verileri.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-162">Now that we've taken a look at how tooinsert geospatial data, let's take a look at how tooquery this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="1b0e6-163">Uzamsal SQL yerleşik işlevler</span><span class="sxs-lookup"><span data-stu-id="1b0e6-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="1b0e6-164">Azure Cosmos DB Jeo-uzamsal sorgulamak için yerleşik işlevler açık Jeo-uzamsal Konsorsiyumu (OGC) aşağıdaki hello destekler.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-164">Azure Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="1b0e6-165">Merhaba eksiksiz hello SQL dil yerleşik işlevler hakkında daha fazla ayrıntı için lütfen çok başvurun[sorgu Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="1b0e6-165">For more details on hello complete set of built-in functions in hello SQL language, please refer too[Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="1b0e6-166"><strong>Kullanım</strong></span><span class="sxs-lookup"><span data-stu-id="1b0e6-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="1b0e6-167"><strong>Açıklama</strong></span><span class="sxs-lookup"><span data-stu-id="1b0e6-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="1b0e6-168">St_dıstance (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="1b0e6-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="1b0e6-169">Merhaba iki GeoJSON noktası, çokgen veya LineString ifadeleri arasında Hello uzaklığını döndürür.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-169">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="1b0e6-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="1b0e6-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="1b0e6-171">Merhaba ilk GeoJSON nesne (noktası, çokgen veya LineString) hello ikinci GeoJSON nesne içinde (noktası, çokgen veya LineString) olup olmadığını gösteren bir Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-171">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="1b0e6-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="1b0e6-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="1b0e6-173">Merhaba iki belirtilen GeoJSON nesne (noktası, çokgen veya LineString) kesiştiği olup olmadığını gösteren bir Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-173">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="1b0e6-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="1b0e6-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="1b0e6-175">Merhaba GeoJSON noktası, çokgen veya LineString ifadesi geçerli belirtilen olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-175">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="1b0e6-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="1b0e6-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="1b0e6-177">Merhaba GeoJSON noktası, çokgen veya LineString ifade belirtilmişse bir Boole değeri içeren bir JSON değeri geçerli değil ve geçersiz, ayrıca bir dize değeri olarak neden hello döndürür.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-177">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="1b0e6-178">Uzamsal işlevleri kullanılan tooperform yakınlık sorguları uzamsal veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-178">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="1b0e6-179">Örneğin, tüm ailesi hello st_dıstance yerleşik işlevi belirtilen konum içinde 30 km hello birini kullanarak belgeleri döndüren bir sorgu aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-179">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="1b0e6-180">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="1b0e6-181">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="1b0e6-182">Dizin oluşturma ilkenizi uzamsal dizin oluşturma eklerseniz, "uzaklığı sorguları" verimli bir şekilde hello dizin sunulacak.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through hello index.</span></span> <span data-ttu-id="1b0e6-183">Uzamsal dizin oluşturma hakkında daha fazla ayrıntı için lütfen hello bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-183">For more details on spatial indexing, please see hello section below.</span></span> <span data-ttu-id="1b0e6-184">Bir uzamsal yoksa dizini hello için belirtilen yol, belirterek hala uzaysal sorgular gerçekleştirebilir `x-ms-documentdb-query-enable-scan` hello değerle istek üstbilgisi çok "true" ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-184">If you don't have a spatial index for hello specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with hello value set too"true".</span></span> <span data-ttu-id="1b0e6-185">.NET içinde bu geçirme hello tarafından isteğe bağlı yapılabilir **FeedOptions** bağımsız değişkeni tooqueries ile [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) tootrue ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-185">In .NET, this can be done by passing hello optional **FeedOptions** argument tooqueries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set tootrue.</span></span> 

<span data-ttu-id="1b0e6-186">Bir noktayı Çokgen içinde yer alıyorsa ST_WITHIN kullanılan toocheck olabilir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-186">ST_WITHIN can be used toocheck if a point lies within a Polygon.</span></span> <span data-ttu-id="1b0e6-187">Yaygın olarak kullanılan toorepresent sınırları posta kodları, durumu sınırları veya doğal durum oluşumlarıyla gibi çokgenler değildir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-187">Commonly Polygons are used toorepresent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="1b0e6-188">Dizin oluşturma ilkenizi uzamsal dizin oluşturma eklerseniz, yeniden sonra "içindeki" sorguları verimli bir şekilde hello dizin sunulacak.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through hello index.</span></span> 

<span data-ttu-id="1b0e6-189">Yalnızca tek bir halka ST_WITHIN Çokgen değişkenlerinde içerebilir, yani hello çokgenler bunlara boşluklar içermemelidir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. hello Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="1b0e6-190">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="1b0e6-191">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="1b0e6-192">Benzer eşleşmeyen toohow türleri çalışmadığını Azure Cosmos DB sorgu, hatalı biçimlendirilmiş veya geçersiz bağımsız değişken sonra çok değerlendirecek hello konum değeri belirtilen**tanımsız** ve hesaplanan hello belge toobe hello atlandı Sorgu sonuçları.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-192">Similar toohow mismatched types works in Azure Cosmos DB query, if hello location value specified in either argument is malformed or invalid, then it will evaluate too**undefined** and hello evaluated document toobe skipped from hello query results.</span></span> <span data-ttu-id="1b0e6-193">Sorgunuz hiçbir sonuç döndürmezse neden hello spatail türü geçersiz ST_ISVALIDDETAILED toodebug çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-193">If your query returns no results, run ST_ISVALIDDETAILED toodebug why hello spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="1b0e6-194">Ters sorgular gerçekleştirme Azure Cosmos DB de destekler, yani, çokgenler veya Azure Cosmos DB satırlarında dizin sonra belirtilen bir nokta içermesi için hello alanlar sorgu.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for hello areas that contain a specified point.</span></span> <span data-ttu-id="1b0e6-195">Bu desen Lojistik tooidentify yaygın olarak kullanılan örneğin ne zaman bir kamyonu girer ya da belirlenen alan bırakır.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-195">This pattern is commonly used in logistics tooidentify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="1b0e6-196">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="1b0e6-197">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="1b0e6-198">Uzamsal nesne geçerli ise ST_ISVALID ve ST_ISVALIDDETAILED kullanılan toocheck olabilir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-198">ST_ISVALID and ST_ISVALIDDETAILED can be used toocheck if a spatial object is valid.</span></span> <span data-ttu-id="1b0e6-199">Örneğin, sorgu aşağıdaki hello noktasının hello geçerlilik aralığı enlem değeri (-132.8) dışı ile denetler.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-199">For example, hello following query checks hello validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="1b0e6-200">ST_ISVALID yalnızca bir Boole değeri döndürür ve Boole ve neden geçersiz değerlendirilir hello neden içeren bir dize hello ST_ISVALIDDETAILED döndürür.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns hello Boolean and a string containing hello reason why it is considered invalid.</span></span>

<span data-ttu-id="1b0e6-201">** Sorgu **</span><span class="sxs-lookup"><span data-stu-id="1b0e6-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="1b0e6-202">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="1b0e6-203">Bu işlevler de kullanılan toovalidate çokgenler olabilir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-203">These functions can also be used toovalidate Polygons.</span></span> <span data-ttu-id="1b0e6-204">Örneğin, burada ST_ISVALIDDETAILED toovalidate kapalı bir Çokgen kullanırız.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-204">For example, here we use ST_ISVALIDDETAILED toovalidate a Polygon that is not closed.</span></span> 

<span data-ttu-id="1b0e6-205">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="1b0e6-206">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a><span data-ttu-id="1b0e6-207">LINQ sorgusu hello .NET SDK içinde</span><span class="sxs-lookup"><span data-stu-id="1b0e6-207">LINQ Querying in hello .NET SDK</span></span>
<span data-ttu-id="1b0e6-208">Merhaba DocumentDB .NET SDK'sı sağlayıcıları yöntemleri de saplama `Distance()` ve `Within()` LINQ ifadeleri içinde kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-208">hello DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="1b0e6-209">Merhaba DocumentDB LINQ sağlayıcısı çevirir bu yöntem çağrıları toohello eşdeğer SQL yerleşik işlev çağrıları (st_dıstance ve ST_WITHIN sırasıyla).</span><span class="sxs-lookup"><span data-stu-id="1b0e6-209">hello DocumentDB LINQ provider translates these method calls toohello equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="1b0e6-210">"Konum" değeri 30 km Merhaba, bir RADIUS içinde belirtilen hello Azure Cosmos DB koleksiyonunda tüm belgeleri bulur bir LINQ Sorgu örneği noktası LINQ kullanarak burada ait.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-210">Here's an example of a LINQ query that finds all documents in hello Azure Cosmos DB collection whose "location" value is within a radius of 30km of hello specified point using LINQ.</span></span>

<span data-ttu-id="1b0e6-211">**LINQ sorgusu için uzaklık**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="1b0e6-212">Benzer şekilde, "Konum" Merhaba içinde olduğu tüm hello belgeleri kutusunu/Çokgen belirtilen bulmak için bir sorgu İşte.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-212">Similarly, here's a query for finding all hello documents whose "location" is within hello specified box/Polygon.</span></span> 

<span data-ttu-id="1b0e6-213">**İçinde LINQ sorgulamak için**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-213">**LINQ query for Within**</span></span>

    Polygon rectangularArea = new Polygon(
        new[]
        {
            new LinearRing(new [] {
                new Position(31.8, -5),
                new Position(32, -5),
                new Position(32, -4.7),
                new Position(31.8, -4.7),
                new Position(31.8, -5)
            })
        });

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(a => a.Location.Within(rectangularArea)))
    {
        Console.WriteLine("\t" + user);
    }


<span data-ttu-id="1b0e6-214">Biz nasıl göz ayırdıktan göre LINQ ve SQL, kullanarak tooquery belgeleri nasıl bir göz atalım uzamsal dizin oluşturma için Azure Cosmos DB tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-214">Now that we've taken a look at how tooquery documents using LINQ and SQL, let's take a look at how tooconfigure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="1b0e6-215">Dizinleme</span><span class="sxs-lookup"><span data-stu-id="1b0e6-215">Indexing</span></span>
<span data-ttu-id="1b0e6-216">Biz hello açıklandığı gibi [belirsiz şema dizin Azure Cosmos DB ile](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) kağıt, biz tasarlanmış Azure Cosmos veritabanı veritabanı altyapısı toobe gerçekten şema belirsiz ve JSON için birinci sınıf destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-216">As we described in hello [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine toobe truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="1b0e6-217">Merhaba en iyi duruma getirilmiş yazma veritabanı motoruna Azure Cosmos DB yerel olarak hello GeoJSON standardında temsil uzamsal veriler (noktaları, çokgenler ve satırları) bilir.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-217">hello write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in hello GeoJSON standard.</span></span>

<span data-ttu-id="1b0e6-218">Buna koysalar hello geometri 2B düzlemi üzerine geodetic koordinatları gelen öngörülen sonra aşamalı olarak kullanarak hücrelere bölünmüş bir **quadtree**.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-218">In a nutshell, hello geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="1b0e6-219">Bu hücreler hello hücrenin içinde hello konumuna bağlı olarak eşlenen too1D olan bir **Hilbert alanı doldurma eğri**, yerleşim yeri noktalarının korur.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-219">These cells are mapped too1D based on hello location of hello cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="1b0e6-220">Konum verileri sıralandığında ayrıca olarak bilinen bir işlemle gidiyor **Mozaik döşeme**, yani bir konum kesiştiği tüm hello hücreleri tanımlanır ve anahtarları'hello Azure Cosmos DB dizini olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all hello cells that intersect a location are identified and stored as keys in hello Azure Cosmos DB index.</span></span> <span data-ttu-id="1b0e6-221">Sorgu zaman noktaları ve çokgenler grubun Mozaik tooextract gibi bağımsız değişkenler ilgili hücre kimliği aralıkları hello sonra tooretrieve veri hello dizinden kullanılan.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-221">At query time, arguments like points and Polygons are also tessellated tooextract hello relevant cell ID ranges, then used tooretrieve data from hello index.</span></span>

<span data-ttu-id="1b0e6-222">Uzamsal dizini içeren bir dizin oluşturma ilkesini belirtirseniz / * (tüm yolları) hello koleksiyonu içinde bulunan tüm noktalarını verimli uzamsal sorguları için (ST_WITHIN ve st_dıstance) dizine sonra.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within hello collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="1b0e6-223">Uzamsal dizinler değil duyarlılık değeri vardır ve her zaman varsayılan duyarlılık değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="1b0e6-224">Azure Cosmos DB noktaları, çokgenler ve MultiPoint otomatik dizin oluşturma destekler</span><span class="sxs-lookup"><span data-stu-id="1b0e6-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="1b0e6-225">Merhaba aşağıdaki JSON parçacığı bir dizin oluşturma ilkesi etkin uzamsal dizin ile gösterir, yani uzamsal sorgulamak için belgeler içinde bulunan herhangi bir GeoJSON noktası dizini.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-225">hello following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="1b0e6-226">Hello Azure Portal kullanarak ilke dizin hello değiştiriyorsanız hello İlkesi tooenable koleksiyonunuzu üzerinde dizin uzamsal dizin oluşturma işlemi için JSON aşağıdaki belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-226">If you are modifying hello indexing policy using hello Azure Portal, you can specify hello following JSON for indexing policy tooenable spatial indexing on your collection.</span></span>

<span data-ttu-id="1b0e6-227">**Toplama dizin oluşturma ilkesi JSON noktaları ve çokgenler için etkin Spatial ile**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Range",
                   "dataType":"String",
                   "precision":-1
                },
                {
                   "kind":"Range",
                   "dataType":"Number",
                   "precision":-1
                },
                {
                   "kind":"Spatial",
                   "dataType":"Point"
                },
                {
                   "kind":"Spatial",
                   "dataType":"Polygon"
                }                
             ]
          }
       ],
       "excludedPaths":[
       ]
    }

<span data-ttu-id="1b0e6-228">Bir kod parçacığı aşağıda verilmiştir toocreate uzamsal dizin oluşturma ile bir koleksiyon nasıl noktaları içeren tüm yollar için açık gösterir .NET içinde.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-228">Here's a code snippet in .NET that shows how toocreate a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="1b0e6-229">**Uzamsal dizin oluşturma ile bir koleksiyon oluşturma**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="1b0e6-230">Burada da belgeler içinde depolanan noktaları üzerinden uzamsal dizin oluşturma Varolan koleksiyon tootake avantajı nasıl değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-230">And here's how you can modify an existing collection tootake advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="1b0e6-231">**Var olan bir koleksiyon uzamsal dizin oluşturma ile değiştirme**</span><span class="sxs-lookup"><span data-stu-id="1b0e6-231">**Modify an existing collection with spatial indexing**</span></span>

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing toocomplete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> <span data-ttu-id="1b0e6-232">Merhaba konumu GeoJSON değeri hello belge içinde hatalı biçimlendirilmiş veya geçersiz ise, ardından uzamsal sorgulamak için dizine değil.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-232">If hello location GeoJSON value within hello document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="1b0e6-233">Konum değerleri ST_ISVALID ve ST_ISVALIDDETAILED kullanarak doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="1b0e6-234">Koleksiyon tanımınızı bölüm anahtarı içeriyorsa, dönüşüm ilerleme dizin bildirilmedi.</span><span class="sxs-lookup"><span data-stu-id="1b0e6-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1b0e6-235">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1b0e6-235">Next steps</span></span>
<span data-ttu-id="1b0e6-236">Learnt göre tooget Jeo-uzamsal desteği Azure Cosmos veritabanı ile çalışmaya nasıl hakkında şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1b0e6-236">Now that you've learnt about how tooget started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="1b0e6-237">Merhaba ile kod yazmaya başlayın [Jeo-uzamsal .NET github'daki kod örnekleri](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="1b0e6-237">Start coding with hello [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="1b0e6-238">Hello Jeo-uzamsal sorgulama ile ele almak [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="1b0e6-238">Get hands on with geospatial querying at hello [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="1b0e6-239">Daha fazla bilgi edinmek [Azure Cosmos DB sorgusu](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="1b0e6-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="1b0e6-240">Daha fazla bilgi edinmek [Azure Cosmos DB dizin oluşturma ilkeleri](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="1b0e6-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

