---
title: "Azure Cosmos veritabanı Jeo-uzamsal verilerle çalışma | Microsoft Docs"
description: "Oluşturma, dizin ve Azure Cosmos DB ve DocumentDB API uzamsal nesneleriyle sorgu anlayın."
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
ms.openlocfilehash: d5785c81fb597e7d30eb7d3a880e7194d8358ed5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="7d8fa-103">Jeo-uzamsal ve Azure Cosmos veritabanı GeoJSON konum verileri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="7d8fa-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="7d8fa-104">Bu makalede Jeo-uzamsal işlevine bir giriş olduğunu [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="7d8fa-104">This article is an introduction to the geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="7d8fa-105">Bu okuduktan sonra aşağıdaki soruları yanıtlayın mümkün olacaktır:</span><span class="sxs-lookup"><span data-stu-id="7d8fa-105">After reading this, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="7d8fa-106">Azure Cosmos DB'de nasıl uzamsal veri depoluyor?</span><span class="sxs-lookup"><span data-stu-id="7d8fa-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="7d8fa-107">Azure Cosmos DB'de SQL ve LINQ Jeo-uzamsal verileri nasıl sorgulama yapabilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="7d8fa-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="7d8fa-108">Nasıl etkinleştirmek veya Azure Cosmos DB'de uzamsal dizin oluşturmayı devre dışı?</span><span class="sxs-lookup"><span data-stu-id="7d8fa-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="7d8fa-109">Bu makalede, DocumentDB API uzamsal verilerle çalışmak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-109">This article shows how to work with spatial data with the DocumentDB API.</span></span> <span data-ttu-id="7d8fa-110">Lütfen bu bakın [GitHub proje](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) kod örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-to-spatial-data"></a><span data-ttu-id="7d8fa-111">Uzamsal veri giriş</span><span class="sxs-lookup"><span data-stu-id="7d8fa-111">Introduction to spatial data</span></span>
<span data-ttu-id="7d8fa-112">Uzamsal veri konumu ve Şekil alanı nesnelerin açıklar.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-112">Spatial data describes the position and shape of objects in space.</span></span> <span data-ttu-id="7d8fa-113">Çoğu uygulamada bu dünya, yani Jeo-uzamsal veri nesnelerinde karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-113">In most applications, these correspond to objects on the earth, i.e. geospatial data.</span></span> <span data-ttu-id="7d8fa-114">Uzamsal veriler, bir kişi, ilgilendiğiniz bir yerde veya bir şehir veya bir lake sınırını konumunu temsil etmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-114">Spatial data can be used to represent the location of a person, a place of interest, or the boundary of a city, or a lake.</span></span> <span data-ttu-id="7d8fa-115">Ortak kullanım durumları yakınlık sorguları, örneğin, "tüm kafeterya my geçerli konumu bulmak" için sıklıkla içerir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="7d8fa-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="7d8fa-116">GeoJSON</span></span>
<span data-ttu-id="7d8fa-117">Dizin oluşturma ve kullanma temsil Jeo-uzamsal noktası verileri Sorgulama Azure Cosmos DB destekler [GeoJSON belirtimi](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="7d8fa-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using the [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="7d8fa-118">Böylece depolanabilir ve herhangi bir özel araçlar veya kitaplıkları Azure Cosmos DB kullanarak sorgulanan GeoJSON veri yapıları her zaman geçerli JSON, nesneleridir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="7d8fa-119">Azure Cosmos DB SDK'ları yardımcı sınıfları ve kolaylaştıran uzamsal verilerle çalışmak yöntemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-119">The Azure Cosmos DB SDKs provide helper classes and methods that make it easy to work with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="7d8fa-120">Noktaları, MultiPoint ve çokgenler</span><span class="sxs-lookup"><span data-stu-id="7d8fa-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="7d8fa-121">A **noktası** alanı tek bir konumda gösterir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="7d8fa-122">Jeo-uzamsal verileri bir noktayı Market, bir bilgi noktası, bir otomobil veya bir şehir sokak adresi olabilir tam konumu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-122">In geospatial data, a Point represents the exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="7d8fa-123">Bir noktayı kendi koordinat kullanarak GeoJSON (ve Azure Cosmos DB) çifti veya boylam ve enlem temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="7d8fa-124">Bir noktası için JSON örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="7d8fa-125">**Azure Cosmos DB noktaları**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="7d8fa-126">GeoJSON belirtimi boylam belirtir ilk ve enlem ikinci.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-126">The GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="7d8fa-127">Gibi diğer eşleme uygulamalarda boylam ve enlem açıları ve derece cinsinden temsil.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="7d8fa-128">Boylam değerleri Meridyeninden ölçülür ve -180 ve 180.0 derece ve enlem değerleri ekvatora ölçülür ve-90.0 arasında olan ve 90.0 derece.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-128">Longitude values are measured from the Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from the equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="7d8fa-129">Azure Cosmos DB 84 WGS başvuru sistemi belirtildiği şekilde koordinatları yorumlama.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-129">Azure Cosmos DB interprets coordinates as represented per the WGS-84 reference system.</span></span> <span data-ttu-id="7d8fa-130">Lütfen koordinat başvuru sistemleri hakkında daha fazla bilgi için aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="7d8fa-131">Bu bir Azure Cosmos DB belgesinde konum verileri içeren bir kullanıcı profili bu örnekte gösterildiği gibi katıştırılabilen:</span><span class="sxs-lookup"><span data-stu-id="7d8fa-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="7d8fa-132">**Azure Cosmos DB içinde depolanan konumla profilini kullan**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

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

<span data-ttu-id="7d8fa-133">Noktalarına ek olarak, GeoJSON MultiPoint ve çokgenler destekler.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-133">In addition to points, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="7d8fa-134">**MultiPoint** iki veya daha çok puan alan ve bunları bağlamak çizgi dilimleri bir dizi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-134">**LineStrings** represent a series of two or more points in space and the line segments that connect them.</span></span> <span data-ttu-id="7d8fa-135">Jeo-uzamsal verileri MultiPoint Otoyollar veya rivers göstermek için yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-135">In geospatial data, LineStrings are commonly used to represent highways or rivers.</span></span> <span data-ttu-id="7d8fa-136">A **Çokgen** kapalı LineString forms bir sınırı bağlı noktalarının.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="7d8fa-137">Çokgenler yaygın olarak Göller gibi doğal durum oluşumlarıyla veya siyasi daireleri şehirler ve durumlar gibi göstermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-137">Polygons are commonly used to represent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="7d8fa-138">Burada, Azure Cosmos veritabanı çokgenin bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="7d8fa-139">**GeoJSON'daki çokgenler**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-139">**Polygons in GeoJSON**</span></span>

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
> <span data-ttu-id="7d8fa-140">Geçerli çokgenler için sağlanan son koordinat çifti kapalı bir şekil oluşturmak için birinci ile aynı olması gerektiğini GeoJSON belirtilmesini gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-140">The GeoJSON specification requires that for valid Polygons, the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span>
> 
> <span data-ttu-id="7d8fa-141">Çokgen içindeki noktaları yönünün sırayla belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="7d8fa-142">Belirtilen saat yönünde sırayla Çokgen bölge içindeki tersini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-142">A Polygon specified in clockwise order represents the inverse of the region within it.</span></span>
> 
> 

<span data-ttu-id="7d8fa-143">GeoJSON Point, LineString ve Çokgen ek olarak, ayrıca isteğe bağlı özellikler coğrafi konum ilişkilendirmek nasıl yanı sıra birden çok Jeo-uzamsal konumları grubuna nasıl için gösterimi belirtir. bir **özelliği**.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-143">In addition to Point, LineString and Polygon, GeoJSON also specifies the representation for how to group multiple geospatial locations, as well as how to associate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="7d8fa-144">Bu nesneler geçerli JSON olduğundan, bunlar tüm depolanabilir ve Azure Cosmos DB'de işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="7d8fa-145">Ancak Azure Cosmos DB yalnızca noktalarının otomatik dizin oluşturma işlemi destekler.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="7d8fa-146">Koordinat başvuru sistemleri</span><span class="sxs-lookup"><span data-stu-id="7d8fa-146">Coordinate reference systems</span></span>
<span data-ttu-id="7d8fa-147">Dünya şeklini düzensiz olduğundan, Jeo-uzamsal veri koordinatlarını sistemlerindeki birçok koordinat başvurusu (CR), her biri kendi çerçeveler başvuru ve ölçü gösterilir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-147">Since the shape of the earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="7d8fa-148">Örneğin, "ulusal kılavuz, Britanya" başvuru sistemi çok doğru ise İngiltere, ancak değil dışında.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-148">For example, the "National Grid of Britain" is a reference system is very accurate for the United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="7d8fa-149">En popüler CRS kullanımda bugün dünya Geodetic sistemidir [WGS 84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="7d8fa-149">The most popular CRS in use today is the World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="7d8fa-150">GPS aygıtları ve Google Haritalar ve Bing haritaları API'si dahil olmak üzere birçok eşleme Hizmetleri WGS 84 kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="7d8fa-151">Azure Cosmos DB dizin oluşturma ve Jeo-uzamsal verileri yalnızca WGS 84 CRS kullanarak sorgulama destekler.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-151">Azure Cosmos DB supports indexing and querying of geospatial data using the WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="7d8fa-152">Uzamsal verilerle belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d8fa-152">Creating documents with spatial data</span></span>
<span data-ttu-id="7d8fa-153">GeoJSON değerleri içeren belgeleri oluşturduğunuzda, uzamsal dizin ile dizin oluşturma ilkesini koleksiyonunun uygun otomatik olarak dizini oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance to the indexing policy of the collection.</span></span> <span data-ttu-id="7d8fa-154">Bir Azure Cosmos DB SDK'sı ile Python veya Node.js gibi dinamik olarak yazılan bir dilde çalışıyorsanız, geçerli GeoJSON oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="7d8fa-155">**Node.js içinde Jeo-uzamsal verilerle belge oluşturma**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-155">**Create Document with Geospatial data in Node.js**</span></span>

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within the callback
});
```

<span data-ttu-id="7d8fa-156">DocumentDB API'leri ile çalışıyorsanız, kullanabileceğiniz `Point` ve `Polygon` içinde sınıfları `Microsoft.Azure.Documents.Spatial` uygulama nesnelerinizi içindeki konum bilgileri katıştırmak için ad alanı.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-156">If you're working with the DocumentDB APIs, you can use the `Point` and `Polygon` classes within the `Microsoft.Azure.Documents.Spatial` namespace to embed location information within your application objects.</span></span> <span data-ttu-id="7d8fa-157">Bu sınıfların seri hale getirme ve seri durumdan çıkarma uzamsal veri GeoJSON içine kolaylaştırmaya yardımcı.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-157">These classes help simplify the serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="7d8fa-158">**.NET Jeo-uzamsal verilerle belge oluşturma**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-158">**Create Document with Geospatial data in .NET**</span></span>

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

<span data-ttu-id="7d8fa-159">Enlem ve boylam bilgilere sahip değilseniz, ancak fiziksel adreslerini veya şehir veya ülke gibi konum adı, Bing Haritalar REST Hizmetleri gibi bir coğrafi kodlama hizmet kullanarak gerçek koordinatları bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-159">If you don't have the latitude and longitude information, but have the physical addresses or location name like city or country, you can look up the actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="7d8fa-160">Bing Haritalar coğrafi kodlama hakkında daha fazla bilgi [burada](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d8fa-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="7d8fa-161">Uzamsal türler sorgulama</span><span class="sxs-lookup"><span data-stu-id="7d8fa-161">Querying spatial types</span></span>
<span data-ttu-id="7d8fa-162">Biz Jeo-uzamsal veri eklemek nasıl göz ayırdıktan, SQL ve LINQ kullanarak Azure Cosmos DB kullanarak bu verileri sorgulamak nasıl bir göz atalım.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-162">Now that we've taken a look at how to insert geospatial data, let's take a look at how to query this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="7d8fa-163">Uzamsal SQL yerleşik işlevler</span><span class="sxs-lookup"><span data-stu-id="7d8fa-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="7d8fa-164">Azure Cosmos DB Jeo-uzamsal sorgulamak için aşağıdaki açık Jeo-uzamsal Konsorsiyumu (OGC) yerleşik işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-164">Azure Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="7d8fa-165">Tamamını SQL dilinde yerleşik işlevler hakkında daha fazla ayrıntı için lütfen [sorgu Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="7d8fa-165">For more details on the complete set of built-in functions in the SQL language, please refer to [Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="7d8fa-166"><strong>Kullanım</strong></span><span class="sxs-lookup"><span data-stu-id="7d8fa-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="7d8fa-167"><strong>Açıklama</strong></span><span class="sxs-lookup"><span data-stu-id="7d8fa-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="7d8fa-168">St_dıstance (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="7d8fa-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="7d8fa-169">İki GeoJSON noktası, çokgen veya LineString ifadeleri uzaklığı döndürür.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-169">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="7d8fa-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="7d8fa-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="7d8fa-171">İlk GeoJSON nesne (noktası, çokgen veya LineString) ikinci GeoJSON nesne içinde (noktası, çokgen veya LineString) olup olmadığını gösteren bir Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-171">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="7d8fa-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="7d8fa-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="7d8fa-173">İki belirtilen GeoJSON nesne (noktası, çokgen veya LineString) kesiştiği olup olmadığını gösteren bir Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-173">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="7d8fa-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="7d8fa-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="7d8fa-175">Belirtilen GeoJSON noktası, çokgen veya LineString ifade geçerli olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-175">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="7d8fa-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="7d8fa-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="7d8fa-177">Belirtilen GeoJSON noktası, çokgen veya LineString ifade geçerli olup olmadığını ve geçersiz bir Boole değeri içeren bir JSON değeri değeri döndürür, ayrıca bir dize değeri olarak nedeni.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-177">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="7d8fa-178">Uzamsal işlevleri uzamsal veriler yakınlaştırmalı sorguları gerçekleştirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-178">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="7d8fa-179">Örneğin, içinde 30 km st_dıstance yerleşik işlevini kullanarak belirtilen konumun olan tüm ailesi belgeleri döndüren bir sorgu aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-179">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="7d8fa-180">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="7d8fa-181">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="7d8fa-182">Dizin oluşturma ilkenizi uzamsal dizin oluşturma eklerseniz, "uzaklığı sorguları" verimli bir şekilde dizin sunulacak.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through the index.</span></span> <span data-ttu-id="7d8fa-183">Uzamsal dizin oluşturma hakkında daha fazla ayrıntı için lütfen aşağıdaki bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-183">For more details on spatial indexing, please see the section below.</span></span> <span data-ttu-id="7d8fa-184">Belirtilen yol için bir uzamsal dizin yoksa, hala uzamsal sorguları belirterek gerçekleştirebileceğiniz `x-ms-documentdb-query-enable-scan` "true" değerini kümesiyle istek üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-184">If you don't have a spatial index for the specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with the value set to "true".</span></span> <span data-ttu-id="7d8fa-185">.NET içinde bu isteğe bağlı geçirerek yapılabilir **FeedOptions** sorgularıyla bağımsız değişkeni [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) true olarak ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-185">In .NET, this can be done by passing the optional **FeedOptions** argument to queries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set to true.</span></span> 

<span data-ttu-id="7d8fa-186">ST_WITHIN bir noktası içinde Çokgen arasındadır varsa denetlemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-186">ST_WITHIN can be used to check if a point lies within a Polygon.</span></span> <span data-ttu-id="7d8fa-187">Yaygın olarak çokgenler sınırları posta kodları, durumu sınırları veya doğal durum oluşumlarıyla gibi göstermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-187">Commonly Polygons are used to represent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="7d8fa-188">Dizin oluşturma ilkenizi uzamsal dizin oluşturma dahil ederseniz, tekrar sonra "içindeki" sorguları verimli bir şekilde dizin sunulacak.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through the index.</span></span> 

<span data-ttu-id="7d8fa-189">Yalnızca tek bir halka ST_WITHIN Çokgen değişkenlerinde içerebilir, yani çokgenler bunlara boşluklar içermemelidir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. the Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="7d8fa-190">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="7d8fa-191">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="7d8fa-192">Hatalı biçimlendirilmiş veya geçersiz bağımsız değişken sonra olarak değerlendirilecek konum değeri belirtilen varsa Azure Cosmos DB sorgusunda nasıl eşleşmeyen türler works benzer **tanımsız** ve değerlendirilen belgenin sorgu sonuçlarından atlanır.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-192">Similar to how mismatched types works in Azure Cosmos DB query, if the location value specified in either argument is malformed or invalid, then it will evaluate to **undefined** and the evaluated document to be skipped from the query results.</span></span> <span data-ttu-id="7d8fa-193">Sorgunuz hiçbir sonuç döndürürse, ST_ISVALIDDETAILED için hata ayıklama neden spatail türü geçersiz çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-193">If your query returns no results, run ST_ISVALIDDETAILED To debug why the spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="7d8fa-194">Ters sorgular gerçekleştirme Azure Cosmos DB de destekler, yani, çokgenler veya Azure Cosmos DB satırlarında dizin sonra için belirtilen bir nokta içeren alanlar sorgu.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for the areas that contain a specified point.</span></span> <span data-ttu-id="7d8fa-195">Bu deseni örneğin ne zaman bir kamyonu girer veya belirlenen alanı terk tanımlamak için Lojistik yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-195">This pattern is commonly used in logistics to identify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="7d8fa-196">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="7d8fa-197">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="7d8fa-198">ST_ISVALID ve ST_ISVALIDDETAILED uzamsal nesne geçerli olup olmadığını denetlemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-198">ST_ISVALID and ST_ISVALIDDETAILED can be used to check if a spatial object is valid.</span></span> <span data-ttu-id="7d8fa-199">Örneğin, aşağıdaki sorguyu bir noktası geçerlilik aralığı enlem değeri (-132.8) dışı ile denetler.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-199">For example, the following query checks the validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="7d8fa-200">ST_ISVALID yalnızca bir Boole değeri döndürür ve ST_ISVALIDDETAILED Boole ve neden geçersiz değerlendirilir neden içeren bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns the Boolean and a string containing the reason why it is considered invalid.</span></span>

<span data-ttu-id="7d8fa-201">** Sorgu **</span><span class="sxs-lookup"><span data-stu-id="7d8fa-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="7d8fa-202">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="7d8fa-203">Bu işlevler çokgenler doğrulamak için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-203">These functions can also be used to validate Polygons.</span></span> <span data-ttu-id="7d8fa-204">Örneğin, burada ST_ISVALIDDETAILED kapalı bir Çokgen doğrulamak için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-204">For example, here we use ST_ISVALIDDETAILED to validate a Polygon that is not closed.</span></span> 

<span data-ttu-id="7d8fa-205">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="7d8fa-206">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a Polygon must have the same start and end points." 
          }
    }]

### <a name="linq-querying-in-the-net-sdk"></a><span data-ttu-id="7d8fa-207">.NET SDK'ın sorgulama LINQ</span><span class="sxs-lookup"><span data-stu-id="7d8fa-207">LINQ Querying in the .NET SDK</span></span>
<span data-ttu-id="7d8fa-208">DocumentDB .NET SDK'sı sağlayıcıları yöntemleri de saplama `Distance()` ve `Within()` LINQ ifadeleri içinde kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-208">The DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="7d8fa-209">Bu yöntem çağrıları eşdeğer SQL yerleşik işlev çağrıları için DocumentDB LINQ sağlayıcısı çevirir (st_dıstance ve ST_WITHIN sırasıyla).</span><span class="sxs-lookup"><span data-stu-id="7d8fa-209">The DocumentDB LINQ provider translates these method calls to the equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="7d8fa-210">"Konum" değeri 30 km belirtilen bir RADIUS içinde noktasındaki LINQ kullanarak Azure Cosmos DB koleksiyonunda tüm belgeleri bulur bir LINQ Sorgu bir örneği burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-210">Here's an example of a LINQ query that finds all documents in the Azure Cosmos DB collection whose "location" value is within a radius of 30km of the specified point using LINQ.</span></span>

<span data-ttu-id="7d8fa-211">**LINQ sorgusu için uzaklık**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="7d8fa-212">Benzer şekilde, belirtilen kutusunu/Çokgen içinde "Konum" olan tüm belgeleri bulmak için bir sorgu İşte.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-212">Similarly, here's a query for finding all the documents whose "location" is within the specified box/Polygon.</span></span> 

<span data-ttu-id="7d8fa-213">**İçinde LINQ sorgulamak için**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-213">**LINQ query for Within**</span></span>

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


<span data-ttu-id="7d8fa-214">LINQ ve SQL kullanarak belgeleri nasıl göz yapılan, uzamsal dizin oluşturma işlemi için Azure Cosmos DB yapılandırmak nasıl bir göz atalım.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-214">Now that we've taken a look at how to query documents using LINQ and SQL, let's take a look at how to configure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="7d8fa-215">Dizinleme</span><span class="sxs-lookup"><span data-stu-id="7d8fa-215">Indexing</span></span>
<span data-ttu-id="7d8fa-216">Bölümünde açıklanan [belirsiz şema dizin Azure Cosmos DB ile](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) kağıt, biz tasarlanmış olmasını Azure Cosmos veritabanı veritabanı altyapısı gerçekten şema belirsiz ve JSON için birinci sınıf destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-216">As we described in the [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine to be truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="7d8fa-217">Azure Cosmos DB yazma en iyi duruma getirilmiş veritabanı motoruna yerel GeoJSON standart gösterilen uzamsal veriler (noktaları, çokgenler ve satırları) bilir.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-217">The write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in the GeoJSON standard.</span></span>

<span data-ttu-id="7d8fa-218">Buna koysalar geometri 2B düzlemi üzerine geodetic koordinatları gelen öngörülen sonra aşamalı olarak kullanarak hücrelere bölünmüş bir **quadtree**.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-218">In a nutshell, the geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="7d8fa-219">Bu hücreler 1 hücrede konumuna bağlı olarak D eşlendiği bir **Hilbert alanı doldurma eğri**, yerleşim yeri noktalarının korur.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-219">These cells are mapped to 1D based on the location of the cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="7d8fa-220">Konum verileri sıralandığında ayrıca olarak bilinen bir işlemle gidiyor **Mozaik döşeme**, bir konum kesiştiği yani tüm hücreleri tanımlanır ve Azure Cosmos DB dizin anahtar olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all the cells that intersect a location are identified and stored as keys in the Azure Cosmos DB index.</span></span> <span data-ttu-id="7d8fa-221">Sorgu zamanında noktaları ve çokgenler gibi bağımsız değişkenler de ilgili hücre kimliği aralıkları ayıklamak için grubun Mozaik, sonra verileri dizinden almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-221">At query time, arguments like points and Polygons are also tessellated to extract the relevant cell ID ranges, then used to retrieve data from the index.</span></span>

<span data-ttu-id="7d8fa-222">Uzamsal dizini içeren bir dizin oluşturma ilkesini belirtirseniz / * (tüm yolları), koleksiyon içinde bulunan tüm noktalarını verimli uzamsal sorguları için (ST_WITHIN ve st_dıstance) dizine sonra.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within the collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="7d8fa-223">Uzamsal dizinler değil duyarlılık değeri vardır ve her zaman varsayılan duyarlılık değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="7d8fa-224">Azure Cosmos DB noktaları, çokgenler ve MultiPoint otomatik dizin oluşturma destekler</span><span class="sxs-lookup"><span data-stu-id="7d8fa-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="7d8fa-225">Etkin uzamsal dizin ile bir dizin oluşturma ilkesini aşağıdaki JSON parçacığı gösterir, yani uzamsal sorgulamak için belgeler içinde bulunan herhangi bir GeoJSON noktası dizini.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-225">The following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="7d8fa-226">Azure Portalı'nı kullanarak dizin oluşturma ilkesini değiştiriyorsanız, koleksiyonunuzu üzerinde dizin uzamsal etkinleştirmek için dizin oluşturma ilkesi için aşağıdaki JSON belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-226">If you are modifying the indexing policy using the Azure Portal, you can specify the following JSON for indexing policy to enable spatial indexing on your collection.</span></span>

<span data-ttu-id="7d8fa-227">**Toplama dizin oluşturma ilkesi JSON noktaları ve çokgenler için etkin Spatial ile**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

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

<span data-ttu-id="7d8fa-228">Bir kod parçacığı aşağıda verilmiştir noktaları içeren tüm yollar için açık uzamsal dizin ile bir koleksiyon oluşturmayı gösteren .NET içinde.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-228">Here's a code snippet in .NET that shows how to create a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="7d8fa-229">**Uzamsal dizin oluşturma ile bir koleksiyon oluşturma**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override to turn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="7d8fa-230">Burada da var olan bir koleksiyon içindeki belgelerde depolanır noktaları üzerinden uzamsal dizin oluşturma avantajından yararlanmak için nasıl değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-230">And here's how you can modify an existing collection to take advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="7d8fa-231">**Var olan bir koleksiyon uzamsal dizin oluşturma ile değiştirme**</span><span class="sxs-lookup"><span data-stu-id="7d8fa-231">**Modify an existing collection with spatial indexing**</span></span>

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing to complete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> <span data-ttu-id="7d8fa-232">GeoJSON değeri belge içindeki konum hatalı biçimlendirilmiş veya geçersiz ise, ardından uzamsal sorgulamak için dizine değil.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-232">If the location GeoJSON value within the document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="7d8fa-233">Konum değerleri ST_ISVALID ve ST_ISVALIDDETAILED kullanarak doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="7d8fa-234">Koleksiyon tanımınızı bölüm anahtarı içeriyorsa, dönüşüm ilerleme dizin bildirilmedi.</span><span class="sxs-lookup"><span data-stu-id="7d8fa-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7d8fa-235">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7d8fa-235">Next steps</span></span>
<span data-ttu-id="7d8fa-236">Azure Cosmos DB Jeo-uzamsal desteği ile çalışmaya nasıl başlayacağınız hakkında learnt, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7d8fa-236">Now that you've learnt about how to get started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="7d8fa-237">İle kod yazmaya başlayın [Jeo-uzamsal .NET github'daki kod örnekleri](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="7d8fa-237">Start coding with the [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="7d8fa-238">Konumundaki Jeo-uzamsal sorgulama ile ele almak [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="7d8fa-238">Get hands on with geospatial querying at the [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="7d8fa-239">Daha fazla bilgi edinmek [Azure Cosmos DB sorgusu](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="7d8fa-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="7d8fa-240">Daha fazla bilgi edinmek [Azure Cosmos DB dizin oluşturma ilkeleri](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="7d8fa-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

