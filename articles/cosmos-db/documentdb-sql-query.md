---
title: "SQL sorguları Azure Cosmos DB DocumentDB API'si | Microsoft Docs"
description: "Azure Cosmos DB SQL söz dizimi, veritabanı kavramlarını ve SQL sorguları hakkında bilgi edinin. SQL Azure Cosmos veritabanı bir JSON sorgu dili olarak kullanabilir."
keywords: "SQL söz dizimi, sql sorgusu, sql sorguları, json sorgu dili, veritabanı kavramlarını ve sql sorguları, toplama işlevleri"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: arramac
ms.openlocfilehash: 9b2b5668ef0552485a86f63a120b57c4623bfe35
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="fdd23-105">SQL sorguları Azure Cosmos DB DocumentDB API'si</span><span class="sxs-lookup"><span data-stu-id="fdd23-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="fdd23-106">Microsoft Azure Cosmos DB bir JSON sorgu dili SQL (yapılandırılmış sorgu dili) kullanarak belgelerin sorgulanmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="fdd23-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="fdd23-107">Cosmos DB gerçekten şemasız.</span><span class="sxs-lookup"><span data-stu-id="fdd23-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="fdd23-108">Doğrudan veritabanı altyapısının içinde JSON veri modeli için kendi taahhüt, otomatik JSON belgelerinin dizinini gerektirmeden açık şema veya ikincil dizinlerin oluşturulmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-108">By virtue of its commitment to the JSON data model directly within the database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="fdd23-109">Cosmos DB için sorgu dili tasarlarken size iki hedefleri düşünerek vardı:</span><span class="sxs-lookup"><span data-stu-id="fdd23-109">While designing the query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="fdd23-110">Yeni bir JSON sorgu dili inventing yerine biz SQL desteği istedik.</span><span class="sxs-lookup"><span data-stu-id="fdd23-110">Instead of inventing a new JSON query language, we wanted to support SQL.</span></span> <span data-ttu-id="fdd23-111">SQL en tanıdık ve popüler sorgu dilleri biridir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-111">SQL is one of the most familiar and popular query languages.</span></span> <span data-ttu-id="fdd23-112">Cosmos veritabanı SQL, JSON belgelerini zengin sorgular için resmi bir programlama modeli sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="fdd23-113">Bir JSON belgesi veritabanı doğrudan veritabanı altyapısının içinde JavaScript yürütme özellikli, biz JavaScript'in programlama modeli bizim sorgu dili için temel olarak kullanmak istedik.</span><span class="sxs-lookup"><span data-stu-id="fdd23-113">As a JSON document database capable of executing JavaScript directly in the database engine, we wanted to use JavaScript's programming model as the foundation for our query language.</span></span> <span data-ttu-id="fdd23-114">DocumentDB API SQL JavaScript'in tür sistemi, ifade değerlendirmesi ve işlev çağrısını kökü belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="fdd23-114">The DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="fdd23-115">Bu içinde dönüş JSON belgeleri, kendi kendine birleşimler, uzamsal sorguları ve kullanıcı tanımlı işlevler (UDF'ler) diğer özellikler arasında JavaScript tamamen yazılmış çalıştırılışı arasında ilişkisel projeksiyonları, hiyerarşik gezinti için doğal bir programlama modeli sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="fdd23-116">Bu özellikler uygulama ve veritabanı arasında uyuşmazlık azaltmak için anahtar ve geliştirici üretkenliği için kritik önem taşıyan inanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-116">We believe that these capabilities are key to reducing the friction between the application and the database and are crucial for developer productivity.</span></span>

<span data-ttu-id="fdd23-117">Burada Aravind Ramachandran gösterir Cosmos DB özellikleri sorgulama, aşağıdaki videoyu izlemeyi ve ziyaret tarafından Başlarken öneririz bizim [Query Playground](http://www.documentdb.com/sql/demo), burada Cosmos DB deneyin ve SQL sorguları çalıştırma bizim veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="fdd23-117">We recommend getting started by watching the following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="fdd23-118">Ardından, bu makalede, burada size bazı basit JSON belgeleri ve SQL komutları anlatan bir SQL sorgusu öğretici başlayın döndür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-118">Then, return to this article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="fdd23-119"><a id="GettingStarted"></a>Cosmos DB SQL komutları ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="fdd23-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="fdd23-120">Cosmos veritabanı SQL iş görmek için şimdi birkaç basit JSON belgeleri ile başlar ve bazı basit sorgular size yol.</span><span class="sxs-lookup"><span data-stu-id="fdd23-120">To see Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="fdd23-121">Bu iki JSON belgeleri iki ailesi hakkında göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="fdd23-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="fdd23-122">Cosmos DB ile biz herhangi bir şemaları ya da ikincil dizinlerin açıkça oluşturmak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="fdd23-122">With Cosmos DB, we do not need to create any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="fdd23-123">Biz JSON belgeleri Cosmos DB koleksiyonuna eklemek ve daha sonra sorgu yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-123">We simply need to insert the JSON documents to a Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="fdd23-124">Basit bir JSON burada sahibiz belge Andersen ailesi, üst, alt öğelerini (ve bunların Evcil Hayvanlar), adresinizi ve kayıt bilgileri.</span><span class="sxs-lookup"><span data-stu-id="fdd23-124">Here we have a simple JSON document for the Andersen family, the parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="fdd23-125">Belge dizeler, sayılar, Boole değerlerini, dizileri ve iç içe özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-125">The document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="fdd23-126">**Belge**</span><span class="sxs-lookup"><span data-stu-id="fdd23-126">**Document**</span></span>  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

<span data-ttu-id="fdd23-127">Bir fark – sahip ikinci bir belge işte `givenName` ve `familyName` yerine kullanılan `firstName` ve `lastName`.</span><span class="sxs-lookup"><span data-stu-id="fdd23-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="fdd23-128">**Belge**</span><span class="sxs-lookup"><span data-stu-id="fdd23-128">**Document**</span></span>  

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

<span data-ttu-id="fdd23-129">Şimdi DocumentDB API SQL anahtar yönlerini bazıları anlamak için bu verileri birkaç sorguları deneyelim.</span><span class="sxs-lookup"><span data-stu-id="fdd23-129">Now let's try a few queries against this data to understand some of the key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="fdd23-130">Örneğin, aşağıdaki sorguyu ID alanı eşleştiği belgeleri döndürür `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="fdd23-130">For example, the following query returns the documents where the id field matches `AndersenFamily`.</span></span> <span data-ttu-id="fdd23-131">Olduğundan bir `SELECT *`, tam JSON belgesi sorgunun çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="fdd23-131">Since it's a `SELECT *`, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="fdd23-132">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fdd23-133">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-133">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]


<span data-ttu-id="fdd23-134">Şimdi Burada farklı bir şekli JSON çıkışında yeniden biçimlendirmek için ihtiyacımız durumu göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="fdd23-134">Now consider the case where we need to reformat the JSON output in a different shape.</span></span> <span data-ttu-id="fdd23-135">Adres Şehir durumu olarak aynı ada sahip olduğunda bu sorgu adı ve şehir olmak üzere iki seçilen alan ile yeni bir JSON nesnesi projeleri.</span><span class="sxs-lookup"><span data-stu-id="fdd23-135">This query projects a new JSON object with two selected fields, Name and City, when the address' city has the same name as the state.</span></span> <span data-ttu-id="fdd23-136">Bu durumda, "NY, NY" eşleşir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="fdd23-137">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="fdd23-138">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="fdd23-139">Sonraki sorgu kimliğine eşleşen ailesinde alt tüm verilen adlarını döndürür `WakefieldFamily` ikamet ettiğiniz şehre göre sıralanmış.</span><span class="sxs-lookup"><span data-stu-id="fdd23-139">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by the city of residence.</span></span>

<span data-ttu-id="fdd23-140">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="fdd23-141">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="fdd23-142">Dikkat çekmek için birkaç önemli yönleri kadarki gördük örnekler üzerinden Cosmos DB sorgu dili isteriz:</span><span class="sxs-lookup"><span data-stu-id="fdd23-142">We would like to draw attention to a few noteworthy aspects of the Cosmos DB query language through the examples we've seen so far:</span></span>  

* <span data-ttu-id="fdd23-143">DocumentDB API SQL JSON değerler üzerinde çalışır olduğundan, satır ve sütunların yerine varlıklar şeklinde ağaç ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="fdd23-144">Bu nedenle, dil, herhangi bir rastgele derinliğe ağacını düğümlerinin gibi bakın sağlar `Node1.Node2.Node3…..Nodem`benzer şekilde iki bölümü referansı başvuran ilişkisel SQL `<table>.<column>`.</span><span class="sxs-lookup"><span data-stu-id="fdd23-144">Therefore, the language lets you refer to nodes of the tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar to relational SQL referring to the two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="fdd23-145">Yapılandırılmış sorgu dili şema daha az verilerle çalışır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-145">The structured query language works with schema-less data.</span></span> <span data-ttu-id="fdd23-146">Bu nedenle, tür sistemi dinamik olarak bağlı gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-146">Therefore, the type system needs to be bound dynamically.</span></span> <span data-ttu-id="fdd23-147">Aynı ifadeye farklı belgelere farklı türlerde üretebilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-147">The same expression could yield different types on different documents.</span></span> <span data-ttu-id="fdd23-148">Bir sorgunun sonucu, geçerli bir JSON değer, ancak bir sabit şemasına olması garanti edilmez.</span><span class="sxs-lookup"><span data-stu-id="fdd23-148">The result of a query is a valid JSON value, but is not guaranteed to be of a fixed schema.</span></span>  
* <span data-ttu-id="fdd23-149">Cosmos DB yalnızca Katı JSON belgelerini destekler.</span><span class="sxs-lookup"><span data-stu-id="fdd23-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="fdd23-150">Bu tür sistemi ve ifadeler yalnızca JSON türleri ile mücadele etmek için sınırlı olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-150">This means the type system and expressions are restricted to deal only with JSON types.</span></span> <span data-ttu-id="fdd23-151">Başvurmak [JSON belirtimi](http://www.json.org/) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="fdd23-151">Refer to the [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="fdd23-152">Cosmos DB koleksiyon JSON belgeleri, şemasız bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="fdd23-153">İlişkileri veri varlıklarında içinde ve bir koleksiyondaki belgeler arasında örtük olarak kapsama ve birincil anahtar ve yabancı anahtar ilişkileri tarafından yakalanır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-153">The relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="fdd23-154">Bu makalenin sonraki bölümlerinde ele alınan içi belge birleştirmeler etkinliğinin düzenleyicileri gösteren değer önemli bir yönü budur.</span><span class="sxs-lookup"><span data-stu-id="fdd23-154">This is an important aspect worth pointing out in light of the intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="fdd23-155"><a id="Indexing"></a>Cosmos DB dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="fdd23-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="fdd23-156">Biz DocumentDB API SQL söz dizimi ulaşmadan Cosmos DB dizin tasarımında incelenmesi yararlı olan.</span><span class="sxs-lookup"><span data-stu-id="fdd23-156">Before we get into the DocumentDB API SQL syntax, it is worth exploring the indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="fdd23-157">Veritabanı dizinlerini amacı, çeşitli formlar ve şekiller sorgularda (örneğin, CPU ve giriş/çıkış) en düşük kaynak kullanımına sahip görev iyi performans ve düşük gecikme süresi sunarken yapmaktır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-157">The purpose of database indexes is to serve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="fdd23-158">Genellikle, bir veritabanını sorgulamak için doğru dizin seçimi kadar planlama ve deneme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-158">Often, the choice of the right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="fdd23-159">Bu yaklaşım, burada veri katı bir şemaya uygun değil ve hızlı bir şekilde dönüşmesi şema daha az veritabanları için bir zorluk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fdd23-159">This approach poses a challenge for schema-less databases where the data doesn’t conform to a strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="fdd23-160">Bu nedenle, biz Cosmos DB dizin alt sistemi tasarlarken aşağıdaki hedefleri ayarlar:</span><span class="sxs-lookup"><span data-stu-id="fdd23-160">Therefore, when we designed the Cosmos DB indexing subsystem, we set the following goals:</span></span>

* <span data-ttu-id="fdd23-161">Dizin belgeleri şema gerek kalmadan: dizin oluşturma alt sistemi herhangi bir şema bilgi gerektirmez veya şeması hakkında tüm varsayımlarda belgelerin.</span><span class="sxs-lookup"><span data-stu-id="fdd23-161">Index documents without requiring schema: The indexing subsystem does not require any schema information or make any assumptions about schema of the documents.</span></span> 
* <span data-ttu-id="fdd23-162">Verimli, zengin hiyerarşik ve ilişkisel sorguları için destek: hiyerarşik ve ilişkisel tahminleri desteği dahil olmak üzere verimli bir şekilde dizin Cosmos DB sorgu dili destekler.</span><span class="sxs-lookup"><span data-stu-id="fdd23-162">Support for efficient, rich hierarchical, and relational queries: The index supports the Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="fdd23-163">Yazma sürekli bir birim in face of tutarlı sorgular için destek: tutarlı sorgularla yüksek yazma üretilen iş yükleri için dizin artımlı olarak, verimli ve çevrimiçi sürekli bir yazma hacmi karşısında güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, the index is updated incrementally, efficiently, and online in the face of a sustained volume of writes.</span></span> <span data-ttu-id="fdd23-164">Kullanıcı belge hizmeti yapılandırılan tutarlılık düzeyinde sorguları sunmak tutarlı dizin güncelleştirmesi önemlidir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-164">The consistent index update is crucial to serve the queries at the consistency level in which the user configured the document service.</span></span>
* <span data-ttu-id="fdd23-165">Çoklu kiracı için destek: ayırmaya dayalı modeli için kaynak İdaresi kiracılar arasında verildiğinde, dizin güncelleştirmeleri bütçe çoğaltma ayrılan sistem kaynaklarını (İşlemci, bellek ve saniye başına girdi/çıktı işlemleri) içinde gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-165">Support for multi-tenancy: Given the reservation-based model for resource governance across tenants, index updates are performed within the budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="fdd23-166">Depolama verimliliği: maliyet verimliliği için disk üzerinde depolama ek yükü dizin sınırlanmış ve tahmin edilebilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-166">Storage efficiency: For cost effectiveness, the on-disk storage overhead of the index is bounded and predictable.</span></span> <span data-ttu-id="fdd23-167">Cosmos DB maliyet tabanlı bileşim dizin yükü sorgu performansı ile ilgili olarak arasında yapmak Geliştirici sağladığından, bu önemlidir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-167">This is crucial because Cosmos DB allows the developer to make cost-based tradeoffs between index overhead in relation to the query performance.</span></span>  

<span data-ttu-id="fdd23-168">Başvurmak [Azure Cosmos DB örnekleri](https://github.com/Azure/azure-documentdb-net) bir koleksiyon için dizin oluşturma ilkesini yapılandırmak nasıl gösteren örnekler için MSDN'de.</span><span class="sxs-lookup"><span data-stu-id="fdd23-168">Refer to the [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how to configure the indexing policy for a collection.</span></span> <span data-ttu-id="fdd23-169">Şimdi şimdi Azure Cosmos DB SQL söz dizimi ayrıntıları alın.</span><span class="sxs-lookup"><span data-stu-id="fdd23-169">Let’s now get into the details of the Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="fdd23-170"><a id="Basics"></a>Bir Azure Cosmos DB SQL sorgusu temelleri</span><span class="sxs-lookup"><span data-stu-id="fdd23-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="fdd23-171">Her sorgu, bir SELECT yan tümcesi ve isteğe bağlı FROM oluşur ve WHERE yan tümcelerini ANSI SQL standartları başına.</span><span class="sxs-lookup"><span data-stu-id="fdd23-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="fdd23-172">Genellikle, her sorgu için kaynak FROM yan tümcesinde numaralandırılır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-172">Typically, for each query, the source in the FROM clause is enumerated.</span></span> <span data-ttu-id="fdd23-173">Ardından WHERE yan tümcesinde filtre bir alt kümesini JSON belgelerini almak için kaynak üzerinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-173">Then the filter in the WHERE clause is applied on the source to retrieve a subset of JSON documents.</span></span> <span data-ttu-id="fdd23-174">Son olarak, SELECT yan tümcesi, select listesindeki istenen JSON değerlerin proje için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-174">Finally, the SELECT clause is used to project the requested JSON values in the select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="fdd23-175"><a id="FromClause"></a>FROM yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="fdd23-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="fdd23-176">`FROM <from_specification>` Kaynak filtre veya sorguyu daha sonra öngörülen sürece yan tümcesi isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-176">The `FROM <from_specification>` clause is optional unless the source is filtered or projected later in the query.</span></span> <span data-ttu-id="fdd23-177">Bu yan tümce amacı bağlı sorgu çalışmalıdır veri kaynağı belirtmektir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-177">The purpose of this clause is to specify the data source upon which the query must operate.</span></span> <span data-ttu-id="fdd23-178">Yaygın olarak tüm koleksiyon kaynağıdır ancak bir koleksiyon kümesini yerine belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-178">Commonly the whole collection is the source, but one can specify a subset of the collection instead.</span></span> 

<span data-ttu-id="fdd23-179">Bir sorgu ister `SELECT * FROM Families` tüm aileleri koleksiyon üzerinden numaralandırmak kaynak olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-179">A query like `SELECT * FROM Families` indicates that the entire Families collection is the source over which to enumerate.</span></span> <span data-ttu-id="fdd23-180">Özel bir tanımlayıcısı kök, koleksiyon adını kullanmak yerine koleksiyonu temsil etmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-180">A special identifier ROOT can be used to represent the collection instead of using the collection name.</span></span> <span data-ttu-id="fdd23-181">Aşağıdaki listede sorgu zorlanan kurallarını içerir:</span><span class="sxs-lookup"><span data-stu-id="fdd23-181">The following list contains the rules that are enforced per query:</span></span>

* <span data-ttu-id="fdd23-182">Koleksiyon gibi diğer adı, olabilir `SELECT f.id FROM Families AS f` ya da yalnızca `SELECT f.id FROM Families f`.</span><span class="sxs-lookup"><span data-stu-id="fdd23-182">The collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="fdd23-183">Burada `f` eşdeğerdir `Families`.</span><span class="sxs-lookup"><span data-stu-id="fdd23-183">Here `f` is the equivalent of `Families`.</span></span> <span data-ttu-id="fdd23-184">`AS`diğer isteğe bağlı bir anahtar sözcüğü tanımlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-184">`AS` is an optional keyword to alias the identifier.</span></span>
* <span data-ttu-id="fdd23-185">Bir kez diğer adı, özgün kaynak bağlanamaz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-185">Once aliased, the original source cannot be bound.</span></span> <span data-ttu-id="fdd23-186">Örneğin, `SELECT Families.id FROM Families f` "Aileleri" tanımlayıcısı artık çözümlenemiyor beri sözdizimsel olarak geçersiz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since the identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="fdd23-187">Başvurulması gerekiyorsa tüm özellikleri tam olarak nitelenmiş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-187">All properties that need to be referenced must be fully qualified.</span></span> <span data-ttu-id="fdd23-188">Kesin Şema bağlılığı olmaması durumunda, bu öğeler belirsiz herhangi bağlamalar önlemek için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-188">In the absence of strict schema adherence, this is enforced to avoid any ambiguous bindings.</span></span> <span data-ttu-id="fdd23-189">Bu nedenle, `SELECT id FROM Families f` özelliği bu yana sözdizimsel olarak geçersiz `id` bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="fdd23-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since the property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="fdd23-190">Alt belgeleri</span><span class="sxs-lookup"><span data-stu-id="fdd23-190">Subdocuments</span></span>
<span data-ttu-id="fdd23-191">Kaynak, aynı zamanda daha küçük bir alt azaltılabilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-191">The source can also be reduced to a smaller subset.</span></span> <span data-ttu-id="fdd23-192">Örneğin, yalnızca bir alt ağacı her belgedeki numaralandırma için subroot sonra kaynak aşağıdaki örnekte gösterildiği gibi hale gelebilir:</span><span class="sxs-lookup"><span data-stu-id="fdd23-192">For instance, to enumerating only a subtree in each document, the subroot could then become the source, as shown in the following example:</span></span>

<span data-ttu-id="fdd23-193">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="fdd23-194">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-194">**Results**</span></span>  

    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]

<span data-ttu-id="fdd23-195">Yukarıdaki örnek kaynağı olarak bir dizi kullanılan olsa da, bir nesne de aşağıdaki örnekte gösterilen olan kaynağı olarak kullanılabilir: kaynak bulunabilir (tanımsız değil) herhangi geçerli JSON değer sorgunun sonucu eklenmek üzere olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-195">While the above example used an array as the source, an object could also be used as the source, which is what's shown in the following example: Any valid JSON value (not undefined) that can be found in the source is considered for inclusion in the result of the query.</span></span> <span data-ttu-id="fdd23-196">Bazı aileleri yoksa bir `address.state` değeri sorgu sonucu hariç tutulur.</span><span class="sxs-lookup"><span data-stu-id="fdd23-196">If some families don’t have an `address.state` value, they are excluded in the query result.</span></span>

<span data-ttu-id="fdd23-197">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="fdd23-198">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="fdd23-199"><a id="WhereClause"></a>WHERE yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="fdd23-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="fdd23-200">WHERE yan tümcesi (**`WHERE <filter_condition>`**) isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-200">The WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="fdd23-201">Sonucunu bir parçası olarak dahil edilmesi için JSON belgelerini kaynak tarafından sağlanan koşulları karşılamalıdır belirtir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-201">It specifies the condition(s) that the JSON documents provided by the source must satisfy in order to be included as part of the result.</span></span> <span data-ttu-id="fdd23-202">Herhangi bir JSON belge için sonucu olarak kabul edilmesi için "true" belirtilen koşulları değerlendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-202">Any JSON document must evaluate the specified conditions to "true" to be considered for the result.</span></span> <span data-ttu-id="fdd23-203">WHERE yan tümcesi tarafından dizini katman mutlak en küçük alt sonuç parçası olabilir kaynak belgeleri kümesini belirlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-203">The WHERE clause is used by the index layer in order to determine the absolute smallest subset of source documents that can be part of the result.</span></span> 

<span data-ttu-id="fdd23-204">Aşağıdaki sorgu, değeri olan bir ad özelliği içeren belgeleri istekleri `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="fdd23-204">The following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="fdd23-205">Name özelliği olmayan herhangi bir belge veya burada değeri eşleşmiyor `AndersenFamily` dışlandı.</span><span class="sxs-lookup"><span data-stu-id="fdd23-205">Any other document that does not have a name property, or where the value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="fdd23-206">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fdd23-207">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="fdd23-208">Önceki örnekte basit eşitlik sorgu gösterdi.</span><span class="sxs-lookup"><span data-stu-id="fdd23-208">The previous example showed a simple equality query.</span></span> <span data-ttu-id="fdd23-209">DocumentDB API SQL skaler ifadelerin çeşitli de destekler.</span><span class="sxs-lookup"><span data-stu-id="fdd23-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="fdd23-210">En yaygın kullanılan ikili ve birli ifadelerini.</span><span class="sxs-lookup"><span data-stu-id="fdd23-210">The most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="fdd23-211">Kaynak JSON nesnesi özelliği başvurularından da geçerli ifadelerini.</span><span class="sxs-lookup"><span data-stu-id="fdd23-211">Property references from the source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="fdd23-212">Aşağıdaki ikili işleçler şu anda desteklenen ve aşağıdaki örneklerde gösterildiği gibi sorgularında kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="fdd23-212">The following binary operators are currently supported and can be used in queries as shown in the following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="fdd23-213">Aritmetik</span><span class="sxs-lookup"><span data-stu-id="fdd23-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="fdd23-214">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="fdd23-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fdd23-215">Bit düzeyinde</span><span class="sxs-lookup"><span data-stu-id="fdd23-215">Bitwise</span></span></td>    
<td><span data-ttu-id="fdd23-216">|, &, ^, <<>>,, >>> (sıfır dolgu sağa kaydırma)</span><span class="sxs-lookup"><span data-stu-id="fdd23-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fdd23-217">Mantıksal</span><span class="sxs-lookup"><span data-stu-id="fdd23-217">Logical</span></span></td>
<td><span data-ttu-id="fdd23-218">VE VEYA DEĞİL</span><span class="sxs-lookup"><span data-stu-id="fdd23-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fdd23-219">Karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="fdd23-219">Comparison</span></span></td>    
<td><span data-ttu-id="fdd23-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="fdd23-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="fdd23-221">Dize</span><span class="sxs-lookup"><span data-stu-id="fdd23-221">String</span></span></td>    
<td><span data-ttu-id="fdd23-222">|| (birleştirme)</span><span class="sxs-lookup"><span data-stu-id="fdd23-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="fdd23-223">İkili işleçler kullanarak bazı sorguları bir göz atalım.</span><span class="sxs-lookup"><span data-stu-id="fdd23-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="fdd23-224">Birli işleçleri +,-, ~ değil de desteklenir ve aşağıdaki örnekte gösterildiği gibi sorgular içinde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="fdd23-224">The unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in the following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="fdd23-225">İkili ve birli işleçler ek olarak, özellik başvuruları de izin verilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-225">In addition to binary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="fdd23-226">Örneğin, `SELECT * FROM Families f WHERE f.isRegistered` içeren özellik JSON belgesini döndürür `isRegistered` özelliğin değeri olduğu için JSON eşit `true` değeri.</span><span class="sxs-lookup"><span data-stu-id="fdd23-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns the JSON document containing the property `isRegistered` where the property's value is equal to the JSON `true` value.</span></span> <span data-ttu-id="fdd23-227">Diğer tüm değerler (false, null, tanımlanmamış, `<number>`, `<string>`, `<object>`, `<array>`, vs.) sonucundan dışlanan kaynak belge için yol açar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads to the source document being excluded from the result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="fdd23-228">Eşitlik ve Karşılaştırma işleçleri</span><span class="sxs-lookup"><span data-stu-id="fdd23-228">Equality and comparison operators</span></span>
<span data-ttu-id="fdd23-229">Aşağıdaki tabloda, her iki JSON türleri arasında DocumentDB API SQL'de eşitlik karşılaştırmaları sonucunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-229">The following table shows the result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="fdd23-230">
            <strong>OP</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fdd23-231">
            <strong>Tanımlanmamış</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fdd23-232">
            <strong>Null</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fdd23-233">
            <strong>Boole değeri</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fdd23-234">
            <strong>Sayı</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fdd23-235">
            <strong>Dize</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fdd23-236">
            <strong>Nesne</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="fdd23-237">
            <strong>Dizi</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fdd23-238">
            <strong>Tanımlanmamış<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fdd23-239">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-240">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-241">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-242">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-243">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-244">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-245">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fdd23-246">
            <strong>Null<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fdd23-247">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="fdd23-248">
            <strong>TAMAM</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fdd23-249">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-250">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-251">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-252">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-253">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fdd23-254">
            <strong>Boole değeri<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fdd23-255">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-256">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="fdd23-257">
            <strong>TAMAM</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fdd23-258">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-259">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-260">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-261">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fdd23-262">
            <strong>Sayı<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fdd23-263">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-264">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-265">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="fdd23-266">
            <strong>TAMAM</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fdd23-267">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-268">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-269">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fdd23-270">
            <strong>Dize<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fdd23-271">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-272">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-273">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-274">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="fdd23-275">
            <strong>TAMAM</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fdd23-276">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-277">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fdd23-278">
            <strong>Nesne<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fdd23-279">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-280">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-281">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-282">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-283">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="fdd23-284">
            <strong>TAMAM</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fdd23-285">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="fdd23-286">
            <strong>Dizi<strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="fdd23-287">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-288">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-289">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-290">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-291">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="fdd23-292">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="fdd23-293">
            <strong>TAMAM</strong>
         </span><span class="sxs-lookup"><span data-stu-id="fdd23-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="fdd23-294">Gibi diğer Karşılaştırma işleçleri için >, > =,! =, < ve < =, aşağıdaki kurallar geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="fdd23-294">For other comparison operators such as >, >=, !=, < and <=, the following rules apply:</span></span>   

* <span data-ttu-id="fdd23-295">Karşılaştırma türü üzerinden içinde tanımlanmamış sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="fdd23-296">İki nesne veya iki arasında karşılaştırma tanımlanmamış sonuçlarında dizi.</span><span class="sxs-lookup"><span data-stu-id="fdd23-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="fdd23-297">Skaler ifade filtresi sonucu olup olmadığını tanımlanmamış "true" mantıksal olarak eşitlemek değil bu yana tanımlanmamışsa, ilgili belge sonucunda dahil edilir değil.</span><span class="sxs-lookup"><span data-stu-id="fdd23-297">If the result of the scalar expression in the filter is Undefined, the corresponding document would not be included in the result, since Undefined doesn't logically equate to "true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="fdd23-298">ARASINDA anahtar sözcüğü</span><span class="sxs-lookup"><span data-stu-id="fdd23-298">BETWEEN keyword</span></span>
<span data-ttu-id="fdd23-299">BETWEEN anahtar sözcüğü, ANSI SQL gibi değerler aralıklarına sorguları express için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-299">You can also use the BETWEEN keyword to express queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="fdd23-300">ARASINDA dizeyi veya sayı karşı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="fdd23-301">Örneğin, bu sorgu, ilk alt düzey 1-5 arasında (her ikisi de dahil) olan tüm ailesi belgeleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-301">For example, this query returns all family documents in which the first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="fdd23-302">Farklı ANSI-SQL'de de BETWEEN yan tümcesi aşağıdaki örnekteki gibi FROM yan tümcesinde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-302">Unlike in ANSI-SQL, you can also use the BETWEEN clause in the FROM clause like in the following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="fdd23-303">Tüm sayısal özellikleri/BETWEEN yan tümcesinde filtrelenen yolları karşı bir aralık dizin türünü kullanan bir dizin oluşturma ilkesi oluşturmak daha hızlı sorgu yürütme süreleri için unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fdd23-303">For faster query execution times, remember to create an indexing policy that uses a range index type against any numeric properties/paths that are filtered in the BETWEEN clause.</span></span> 

<span data-ttu-id="fdd23-304">DocumentDB API ve ANSI SQL BETWEEN kullanımı arasındaki temel fark karma türlerinin özellikleri aralığı sorguları express – Örneğin, "bir sayı (5) düzeyde" olabilir bazı belgelerde ve diğerleri ("grade4") dizelerde ' dir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-304">The main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="fdd23-305">Bu gibi durumlarda gibi JavaScript'te, iki farklı sonuçlarında "tanımsız" ve belge arasında bir karşılaştırma atlanacak.</span><span class="sxs-lookup"><span data-stu-id="fdd23-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and the document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="fdd23-306">Mantıksal (AND, OR ve NOT) işleçleri</span><span class="sxs-lookup"><span data-stu-id="fdd23-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="fdd23-307">Mantıksal işleçler Boole değerleri üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="fdd23-308">Bu işleçlere için mantıksal gerçekte tabloları aşağıdaki tablolarda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-308">The logical truth tables for these operators are shown in the following tables.</span></span>

| <span data-ttu-id="fdd23-309">OR</span><span class="sxs-lookup"><span data-stu-id="fdd23-309">OR</span></span> | <span data-ttu-id="fdd23-310">True</span><span class="sxs-lookup"><span data-stu-id="fdd23-310">True</span></span> | <span data-ttu-id="fdd23-311">False</span><span class="sxs-lookup"><span data-stu-id="fdd23-311">False</span></span> | <span data-ttu-id="fdd23-312">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fdd23-313">True</span><span class="sxs-lookup"><span data-stu-id="fdd23-313">True</span></span> |<span data-ttu-id="fdd23-314">True</span><span class="sxs-lookup"><span data-stu-id="fdd23-314">True</span></span> |<span data-ttu-id="fdd23-315">True</span><span class="sxs-lookup"><span data-stu-id="fdd23-315">True</span></span> |<span data-ttu-id="fdd23-316">True</span><span class="sxs-lookup"><span data-stu-id="fdd23-316">True</span></span> |
| <span data-ttu-id="fdd23-317">False</span><span class="sxs-lookup"><span data-stu-id="fdd23-317">False</span></span> |<span data-ttu-id="fdd23-318">True</span><span class="sxs-lookup"><span data-stu-id="fdd23-318">True</span></span> |<span data-ttu-id="fdd23-319">False</span><span class="sxs-lookup"><span data-stu-id="fdd23-319">False</span></span> |<span data-ttu-id="fdd23-320">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-320">Undefined</span></span> |
| <span data-ttu-id="fdd23-321">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-321">Undefined</span></span> |<span data-ttu-id="fdd23-322">True</span><span class="sxs-lookup"><span data-stu-id="fdd23-322">True</span></span> |<span data-ttu-id="fdd23-323">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-323">Undefined</span></span> |<span data-ttu-id="fdd23-324">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-324">Undefined</span></span> |

| <span data-ttu-id="fdd23-325">VE</span><span class="sxs-lookup"><span data-stu-id="fdd23-325">AND</span></span> | <span data-ttu-id="fdd23-326">True</span><span class="sxs-lookup"><span data-stu-id="fdd23-326">True</span></span> | <span data-ttu-id="fdd23-327">False</span><span class="sxs-lookup"><span data-stu-id="fdd23-327">False</span></span> | <span data-ttu-id="fdd23-328">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fdd23-329">True</span><span class="sxs-lookup"><span data-stu-id="fdd23-329">True</span></span> |<span data-ttu-id="fdd23-330">True</span><span class="sxs-lookup"><span data-stu-id="fdd23-330">True</span></span> |<span data-ttu-id="fdd23-331">False</span><span class="sxs-lookup"><span data-stu-id="fdd23-331">False</span></span> |<span data-ttu-id="fdd23-332">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-332">Undefined</span></span> |
| <span data-ttu-id="fdd23-333">False</span><span class="sxs-lookup"><span data-stu-id="fdd23-333">False</span></span> |<span data-ttu-id="fdd23-334">False</span><span class="sxs-lookup"><span data-stu-id="fdd23-334">False</span></span> |<span data-ttu-id="fdd23-335">False</span><span class="sxs-lookup"><span data-stu-id="fdd23-335">False</span></span> |<span data-ttu-id="fdd23-336">False</span><span class="sxs-lookup"><span data-stu-id="fdd23-336">False</span></span> |
| <span data-ttu-id="fdd23-337">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-337">Undefined</span></span> |<span data-ttu-id="fdd23-338">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-338">Undefined</span></span> |<span data-ttu-id="fdd23-339">False</span><span class="sxs-lookup"><span data-stu-id="fdd23-339">False</span></span> |<span data-ttu-id="fdd23-340">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-340">Undefined</span></span> |

| <span data-ttu-id="fdd23-341">DEĞİL</span><span class="sxs-lookup"><span data-stu-id="fdd23-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="fdd23-342">True</span><span class="sxs-lookup"><span data-stu-id="fdd23-342">True</span></span> |<span data-ttu-id="fdd23-343">False</span><span class="sxs-lookup"><span data-stu-id="fdd23-343">False</span></span> |
| <span data-ttu-id="fdd23-344">False</span><span class="sxs-lookup"><span data-stu-id="fdd23-344">False</span></span> |<span data-ttu-id="fdd23-345">True</span><span class="sxs-lookup"><span data-stu-id="fdd23-345">True</span></span> |
| <span data-ttu-id="fdd23-346">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-346">Undefined</span></span> |<span data-ttu-id="fdd23-347">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="fdd23-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="fdd23-348">Anahtar SÖZCÜĞÜ</span><span class="sxs-lookup"><span data-stu-id="fdd23-348">IN keyword</span></span>
<span data-ttu-id="fdd23-349">IN anahtar sözcüğü, belirtilen bir değeri bir listedeki herhangi bir değer eşleşip eşleşmediğini kontrol etmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-349">The IN keyword can be used to check whether a specified value matches any value in a list.</span></span> <span data-ttu-id="fdd23-350">Örneğin, bu sorgu kimliği "WakefieldFamily" veya "AndersenFamily" biri olduğu tüm ailesi belgeleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-350">For example, this query returns all family documents where the id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="fdd23-351">Bu örnek, durum belirtilen değerlerden herhangi birini olduğu tüm belgeleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-351">This example returns all documents where the state is any of the specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="fdd23-352">Üçlü (?) ve birleşim (?) işleçleri</span><span class="sxs-lookup"><span data-stu-id="fdd23-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="fdd23-353">Üçlü ve birleşim işleçleri, koşullu ifadeleri, C# ve JavaScript gibi popüler programlama dilleri benzer oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-353">The Ternary and Coalesce operators can be used to build conditional expressions, similar to popular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="fdd23-354">Üçlü (?) işleci kolay bir şekilde yeni JSON özellikleri oluşturulurken çok kullanışlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-354">The Ternary (?) operator can be very handy when constructing new JSON properties on the fly.</span></span> <span data-ttu-id="fdd23-355">Örneğin, artık, başlangıç/Orta/aşağıda gösterildiği gibi gelişmiş gibi İnsan okunabilir bir form içine sınıfı düzeyleri sınıflandırmak için sorgu yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-355">For example, now you can write queries to classify the class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="fdd23-356">Like işleci sorgu çağrıları da yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-356">You can also nest the calls to the operator like in the query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="fdd23-357">Olarak diğer sorgu işleçleri ile koşullu ifade başvurulan özelliklerinde herhangi bir belgesinde eksikse veya karşılaştırılan türleri farklıysa, sonra bu belgeleri sorgu sonuçlarında hariç tutulur.</span><span class="sxs-lookup"><span data-stu-id="fdd23-357">As with other query operators, if the referenced properties in the conditional expression are missing in any document, or if the types being compared are different, then those documents are excluded in the query results.</span></span>

<span data-ttu-id="fdd23-358">Birleşim (?) işleci verimli bir şekilde bir özellik (paketini olup olmadığını denetlemek için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="fdd23-358">The Coalesce (??) operator can be used to efficiently check for the presence of a property (a.k.a.</span></span> <span data-ttu-id="fdd23-359">tanımlanır) belgede.</span><span class="sxs-lookup"><span data-stu-id="fdd23-359">is defined) in a document.</span></span> <span data-ttu-id="fdd23-360">Yarı yapılandırılmış karşı sorgularken bu yararlıdır veya karma türlerinin veri.</span><span class="sxs-lookup"><span data-stu-id="fdd23-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="fdd23-361">Örneğin, mevcut değilse bu sorgu "Soyadı" varsa ya da "Soyadı" döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-361">For example, this query returns the "lastName" if present, or the "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="fdd23-362"><a id="EscapingReservedKeywords"></a>Tırnak işaretli özelliği erişimcisi</span><span class="sxs-lookup"><span data-stu-id="fdd23-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="fdd23-363">Özellikler tırnak işaretli özelliği işlecini kullanarak da erişebilirsiniz `[]`.</span><span class="sxs-lookup"><span data-stu-id="fdd23-363">You can also access properties using the quoted property operator `[]`.</span></span> <span data-ttu-id="fdd23-364">Örneğin, `SELECT c.grade` ve `SELECT c["grade"]` eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="fdd23-365">Bu sözdizimi, boşluk, özel karakterler içeriyor veya bir SQL anahtar sözcüğü ya da ayrılmış sözcük adıyla aynı paylaşmak için olur bir özellik atlamanız gerekir yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-365">This syntax is useful when you need to escape a property that contains spaces, special characters, or happens to share the same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="fdd23-366"><a id="SelectClause"></a>SELECT yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="fdd23-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="fdd23-367">SELECT yan tümcesi (**`SELECT <select_list>`**) zorunludur ve değerleri sorgudan tıpkı ANSI SQL'de alınır belirtir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-367">The SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from the query, just like in ANSI-SQL.</span></span> <span data-ttu-id="fdd23-368">Kaynak belgeleri üstünde filtre uygulanmış alt burada belirtilen JSON değerleri alınır ve yeni bir JSON nesnesi oluşturulur, projeksiyon aşamasında, sürüklediğinizde geçirilen her giriş için üzerine geçirilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-368">The subset that's been filtered on top of the source documents are passed onto the projection phase, where the specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="fdd23-369">Aşağıdaki örnek, tipik bir seçme sorgusu gösterir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-369">The following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="fdd23-370">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fdd23-371">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="fdd23-372">İç içe Özellikler</span><span class="sxs-lookup"><span data-stu-id="fdd23-372">Nested properties</span></span>
<span data-ttu-id="fdd23-373">Aşağıdaki örnekte, biz iki iç içe özellikler yansıtma `f.address.state` ve `f.address.city`.</span><span class="sxs-lookup"><span data-stu-id="fdd23-373">In the following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="fdd23-374">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fdd23-375">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="fdd23-376">Projeksiyon ayrıca aşağıdaki örnekte gösterildiği gibi JSON ifadeleri destekler:</span><span class="sxs-lookup"><span data-stu-id="fdd23-376">Projection also supports JSON expressions as shown in the following example:</span></span>

<span data-ttu-id="fdd23-377">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fdd23-378">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="fdd23-379">Rolü, bakalım `$1` burada.</span><span class="sxs-lookup"><span data-stu-id="fdd23-379">Let's look at the role of `$1` here.</span></span> <span data-ttu-id="fdd23-380">`SELECT` Yan tümcesi bir JSON nesnesi oluşturmak için gereksinim duyduğu ve hiçbir anahtar sağlanan beri örtük bağımsız değişken adları başlayarak kullanırız `$1`.</span><span class="sxs-lookup"><span data-stu-id="fdd23-380">The `SELECT` clause needs to create a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="fdd23-381">Örneğin, etiketli iki örtük bağımsız değişkenlerini bu sorgunun döndürdüğü `$1` ve `$2`.</span><span class="sxs-lookup"><span data-stu-id="fdd23-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="fdd23-382">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fdd23-383">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="fdd23-384">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="fdd23-384">Aliasing</span></span>
<span data-ttu-id="fdd23-385">Şimdi şimdi yukarıda değerlerin örneği açık yumuşatma ile genişletmek.</span><span class="sxs-lookup"><span data-stu-id="fdd23-385">Now let's extend the example above with explicit aliasing of values.</span></span> <span data-ttu-id="fdd23-386">Diğer ad için kullanılan anahtar sözcük olduğu gibi.</span><span class="sxs-lookup"><span data-stu-id="fdd23-386">AS is the keyword used for aliasing.</span></span> <span data-ttu-id="fdd23-387">İkinci değer olarak yansıtma sırasında gösterildiği gibi isteğe bağlı `NameInfo`.</span><span class="sxs-lookup"><span data-stu-id="fdd23-387">It's optional as shown while projecting the second value as `NameInfo`.</span></span> 

<span data-ttu-id="fdd23-388">Aynı ada sahip iki özellik bir sorgu sahip olmaması durumunda, böylece bunlar tahmini sonucunda disambiguated birini veya her ikisini özelliklerini yeniden adlandırmak için diğer ad kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-388">In case a query has two properties with the same name, aliasing must be used to rename one or both of the properties so that they are disambiguated in the projected result.</span></span>

<span data-ttu-id="fdd23-389">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fdd23-390">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="fdd23-391">Skaler ifade</span><span class="sxs-lookup"><span data-stu-id="fdd23-391">Scalar expressions</span></span>
<span data-ttu-id="fdd23-392">Özellik başvuruları yanı sıra, SELECT yan tümcesi skaler ifadeler sabitler, aritmetik ifadeler, mantıksal ifadeler, vb. gibi de destekler. Örneğin, basit bir "Hello World" sorgu aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-392">In addition to property references, the SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="fdd23-393">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="fdd23-394">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="fdd23-395">Burada, skaler bir ifade kullanır daha karmaşık bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="fdd23-396">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="fdd23-397">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="fdd23-398">Aşağıdaki örnekte, bir Boole değeri bir skaler ifade sonucudur.</span><span class="sxs-lookup"><span data-stu-id="fdd23-398">In the following example, the result of the scalar expression is a Boolean.</span></span>

<span data-ttu-id="fdd23-399">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="fdd23-400">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="fdd23-401">Nesne ve dizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="fdd23-401">Object and array creation</span></span>
<span data-ttu-id="fdd23-402">Başka bir anahtar DocumentDB API SQL dizi/nesne oluşturma özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="fdd23-403">Önceki örnekte yeni bir JSON nesnesi oluşturduğumuz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fdd23-403">In the previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="fdd23-404">Benzer şekilde, biri de diziler aşağıdaki örneklerde gösterildiği gibi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fdd23-404">Similarly, one can also construct arrays as shown in the following examples:</span></span>

<span data-ttu-id="fdd23-405">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="fdd23-406">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-406">**Results**</span></span>  

    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]

### <span data-ttu-id="fdd23-407"><a id="ValueKeyword"></a>VALUE anahtar sözcüğü</span><span class="sxs-lookup"><span data-stu-id="fdd23-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="fdd23-408">**Değeri** anahtar sözcüğü JSON değerini döndürmek için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-408">The **VALUE** keyword provides a way to return JSON value.</span></span> <span data-ttu-id="fdd23-409">Örneğin, aşağıda gösterilen sorgu skaler döndürür `"Hello World"` yerine `{$1: "Hello World"}`.</span><span class="sxs-lookup"><span data-stu-id="fdd23-409">For example, the query shown below returns the scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="fdd23-410">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="fdd23-411">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="fdd23-412">Aşağıdaki sorgu olmadan JSON değerini döndürür `"address"` sonuçları etiketi.</span><span class="sxs-lookup"><span data-stu-id="fdd23-412">The following query returns the JSON value without the `"address"` label in the results.</span></span>

<span data-ttu-id="fdd23-413">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="fdd23-414">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-414">**Results**</span></span>  

    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]

<span data-ttu-id="fdd23-415">Aşağıdaki örnekte bu dönüş JSON ilkel değerlerini (yaprak düzeyi JSON ağacının) göstermek için genişletir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-415">The following example extends this to show how to return JSON primitive values (the leaf level of the JSON tree).</span></span> 

<span data-ttu-id="fdd23-416">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="fdd23-417">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="fdd23-418">* İşleci</span><span class="sxs-lookup"><span data-stu-id="fdd23-418">* Operator</span></span>
<span data-ttu-id="fdd23-419">Özel işleci (*) belgesi olarak projeye desteklenir-değil.</span><span class="sxs-lookup"><span data-stu-id="fdd23-419">The special operator (*) is supported to project the document as-is.</span></span> <span data-ttu-id="fdd23-420">Kullanıldığında, yalnızca tahmini alan olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-420">When used, it must be the only projected field.</span></span> <span data-ttu-id="fdd23-421">While gibi bir sorgu `SELECT * FROM Families f` geçerli olduğu `SELECT VALUE * FROM Families f ` ve `SELECT *, f.id FROM Families f ` geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="fdd23-422">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="fdd23-423">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-423">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

### <span data-ttu-id="fdd23-424"><a id="TopKeyword"></a>TOP işleci</span><span class="sxs-lookup"><span data-stu-id="fdd23-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="fdd23-425">Üst anahtar sözcüğü değerleri sorgudan sayısını sınırlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-425">The TOP keyword can be used to limit the number of values from a query.</span></span> <span data-ttu-id="fdd23-426">ÜST ORDER BY yan tümcesi ile birlikte kullanıldığında, sonuç kümesi ilk N sıralı değer sayısına sınırlıdır; Aksi takdirde, tanımlanmamış bir sırada sonuçları ilk N sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-426">When TOP is used in conjunction with the ORDER BY clause, the result set is limited to the first N number of ordered values; otherwise, it returns the first N number of results in an undefined order.</span></span> <span data-ttu-id="fdd23-427">En iyi uygulama, bir SELECT deyimi içinde ORDER BY yan tümcesi her zaman üst yan tümcesiyle birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="fdd23-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with the TOP clause.</span></span> <span data-ttu-id="fdd23-428">Hangi satır üst tarafından etkilenen beklendiği belirtmek için tek yolu budur.</span><span class="sxs-lookup"><span data-stu-id="fdd23-428">This is the only way to predictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="fdd23-429">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="fdd23-430">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-430">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

<span data-ttu-id="fdd23-431">ÜST bir değişken değeri parametreli sorgular kullanmayı veya sabit bir değer (yukarıda gösterildiği gibi) ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="fdd23-432">Daha fazla ayrıntı için lütfen aşağıdaki parametreli sorgular bakın.</span><span class="sxs-lookup"><span data-stu-id="fdd23-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="fdd23-433"><a id="Aggregates"></a>Toplama işlevleri</span><span class="sxs-lookup"><span data-stu-id="fdd23-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="fdd23-434">Toplamalar de gerçekleştirebilirsiniz `SELECT` yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="fdd23-434">You can also perform aggregations in the `SELECT` clause.</span></span> <span data-ttu-id="fdd23-435">Toplama işlevleri, bir değerleri kümesi üzerinde bir hesaplama gerçekleştirmek ve tek bir değer döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="fdd23-436">Örneğin, aşağıdaki sorguyu koleksiyonundaki ailesi belge sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-436">For example, the following query returns the count of family documents within the collection.</span></span>

<span data-ttu-id="fdd23-437">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="fdd23-438">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="fdd23-439">Kullanarak toplama skaler değer döndürebilir `VALUE` anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="fdd23-439">You can also return the scalar value of the aggregate by using the `VALUE` keyword.</span></span> <span data-ttu-id="fdd23-440">Örneğin, aşağıdaki sorgu, tek bir sayı değerlerin sayısını döndürür:</span><span class="sxs-lookup"><span data-stu-id="fdd23-440">For example, the following query returns the count of values as a single number:</span></span>

<span data-ttu-id="fdd23-441">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="fdd23-442">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="fdd23-443">Filtrelerle birlikte toplamalar de gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="fdd23-444">Örneğin, aşağıdaki sorgu Washington eyaleti adresiyle belge sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-444">For example, the following query returns the count of documents with the address in the state of Washington.</span></span>

<span data-ttu-id="fdd23-445">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="fdd23-446">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="fdd23-447">Aşağıdaki tabloda, DocumentDB API desteklenen toplama işlevleri listesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-447">The following table shows the list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="fdd23-448">`SUM`ve `AVG` ise sayısal değer üzerinde gerçekleştirilen `COUNT`, `MIN`, ve `MAX` numaraları, dizeleri, Boole değerlerini ve null değerlere gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="fdd23-449">Kullanım</span><span class="sxs-lookup"><span data-stu-id="fdd23-449">Usage</span></span> | <span data-ttu-id="fdd23-450">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdd23-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="fdd23-451">SAYISI</span><span class="sxs-lookup"><span data-stu-id="fdd23-451">COUNT</span></span> | <span data-ttu-id="fdd23-452">İfade öğe sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-452">Returns the number of items in the expression.</span></span> |
| <span data-ttu-id="fdd23-453">TOPLA</span><span class="sxs-lookup"><span data-stu-id="fdd23-453">SUM</span></span>   | <span data-ttu-id="fdd23-454">İfadedeki tüm değerlerin toplamını döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-454">Returns the sum of all the values in the expression.</span></span> |
| <span data-ttu-id="fdd23-455">MIN</span><span class="sxs-lookup"><span data-stu-id="fdd23-455">MIN</span></span>   | <span data-ttu-id="fdd23-456">İfade en küçük değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-456">Returns the minimum value in the expression.</span></span> |
| <span data-ttu-id="fdd23-457">EN BÜYÜK</span><span class="sxs-lookup"><span data-stu-id="fdd23-457">MAX</span></span>   | <span data-ttu-id="fdd23-458">İfade en büyük değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-458">Returns the maximum value in the expression.</span></span> |
| <span data-ttu-id="fdd23-459">ORTALAMA</span><span class="sxs-lookup"><span data-stu-id="fdd23-459">AVG</span></span>   | <span data-ttu-id="fdd23-460">İfade değerlerin ortalamasını döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-460">Returns the average of the values in the expression.</span></span> |

<span data-ttu-id="fdd23-461">Toplamalar, bir dizi yineleme sonuçları de gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-461">Aggregates can also be performed over the results of an array iteration.</span></span> <span data-ttu-id="fdd23-462">Daha fazla bilgi için bkz: [dizi yineleme sorgularda](#Iteration).</span><span class="sxs-lookup"><span data-stu-id="fdd23-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="fdd23-463">Azure portal'ın sorgu Gezgini kullanırken, toplama sorguları sorgu sayfası kısmen toplanmış sonuçlar döndürebilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fdd23-463">When using the Azure portal's Query Explorer, note that aggregation queries may return the partially aggregated results over a query page.</span></span> <span data-ttu-id="fdd23-464">SDK'ları tüm sayfalardaki tek bir toplu değer oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fdd23-464">The SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="fdd23-465">Kod kullanarak toplama sorguları gerçekleştirmek için .NET SDK'sı 1.12.0, .NET Core SDK 1.1.0 veya Java SDK'sı 1.9.5 gerekir veya üstü.</span><span class="sxs-lookup"><span data-stu-id="fdd23-465">In order to perform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="fdd23-466"><a id="OrderByClause"></a>ORDER BY yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="fdd23-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="fdd23-467">Gibi ANSI-SQL'de, isteğe bağlı bir Order By yan tümcesi sorgularken ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="fdd23-468">Yan tümcesi sonuçlar alınması gereken sırayı belirtmek için isteğe bağlı ASC/DESC bağımsız değişken ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-468">The clause can include an optional ASC/DESC argument to specify the order in which results must be retrieved.</span></span>

<span data-ttu-id="fdd23-469">Örneğin, yerleşik Şehir kişinin adını sırasına aileleri alır bir sorgu aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-469">For example, here's a query that retrieves families in order of the resident city's name.</span></span>

<span data-ttu-id="fdd23-470">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="fdd23-471">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-471">**Results**</span></span>

    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]

<span data-ttu-id="fdd23-472">Ve aileleri dönem temsil eden bir sayı olarak depolanan oluşturma tarih sırasına göre alır bir sorgu süre, yani, 1 Ocak 1970'ten içinde bu yana geçen süre saniye burada'nın.</span><span class="sxs-lookup"><span data-stu-id="fdd23-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing the epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="fdd23-473">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="fdd23-474">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-474">**Results**</span></span>

    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]

## <span data-ttu-id="fdd23-475"><a id="Advanced"></a>Gelişmiş veritabanı kavramlarını ve SQL sorguları</span><span class="sxs-lookup"><span data-stu-id="fdd23-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="fdd23-476"><a id="Iteration"></a>Yineleme</span><span class="sxs-lookup"><span data-stu-id="fdd23-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="fdd23-477">Yeni bir yapı aracılığıyla eklendi **IN** JSON diziler yineleme için destek sağlamak için DocumentDB API SQL anahtar sözcük.</span><span class="sxs-lookup"><span data-stu-id="fdd23-477">A new construct was added via the **IN** keyword in DocumentDB API SQL to provide support for iterating over JSON arrays.</span></span> <span data-ttu-id="fdd23-478">FROM kaynak yineleme için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-478">The FROM source provides support for iteration.</span></span> <span data-ttu-id="fdd23-479">Aşağıdaki örnek ile başlayalım:</span><span class="sxs-lookup"><span data-stu-id="fdd23-479">Let's start with the following example:</span></span>

<span data-ttu-id="fdd23-480">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="fdd23-481">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-481">**Results**</span></span>  

    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]

<span data-ttu-id="fdd23-482">Şimdi koleksiyondaki çocukların üzerinden yineleme gerçekleştiren başka bir sorgu bakalım.</span><span class="sxs-lookup"><span data-stu-id="fdd23-482">Now let's look at another query that performs iteration over children in the collection.</span></span> <span data-ttu-id="fdd23-483">Çıkış dizisi fark unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fdd23-483">Note the difference in the output array.</span></span> <span data-ttu-id="fdd23-484">Bu örnek böler `children` ve tek bir dizi sonuçları düzleştirir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-484">This example splits `children` and flattens the results into a single array.</span></span>  

<span data-ttu-id="fdd23-485">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="fdd23-486">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-486">**Results**</span></span>  

    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]

<span data-ttu-id="fdd23-487">Bu daha fazla dizi her bir giriş aşağıdaki örnekte gösterildiği gibi filtrelemek için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="fdd23-487">This can be further used to filter on each individual entry of the array as shown in the following example:</span></span>

<span data-ttu-id="fdd23-488">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="fdd23-489">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="fdd23-490">Toplama dizi yineleme sonuç de gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-490">You can also perform aggregation over the result of array iteration.</span></span> <span data-ttu-id="fdd23-491">Örneğin, aşağıdaki sorgu tüm aileleri arasında alt sayısını sayar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-491">For example, the following query counts the number of children among all families.</span></span>

<span data-ttu-id="fdd23-492">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="fdd23-493">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="fdd23-494"><a id="Joins"></a>Birleşimler</span><span class="sxs-lookup"><span data-stu-id="fdd23-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="fdd23-495">İlişkisel bir veritabanında tablolar katılmak için gereken önemlidir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-495">In a relational database, the need to join across tables is important.</span></span> <span data-ttu-id="fdd23-496">Normalleştirilmiş şemaları tasarlama için mantıksal corollary olur.</span><span class="sxs-lookup"><span data-stu-id="fdd23-496">It's the logical corollary to designing normalized schemas.</span></span> <span data-ttu-id="fdd23-497">Bu aykırı DocumentDB API şemasız belgeleri Normalleştirilmemiş veri modeli ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-497">Contrary to this, DocumentDB API deals with the denormalized data model of schema-free documents.</span></span> <span data-ttu-id="fdd23-498">Bu mantıksal eşdeğerdir "Self Katıl" a.</span><span class="sxs-lookup"><span data-stu-id="fdd23-498">This is the logical equivalent of a "self-join".</span></span>

<span data-ttu-id="fdd23-499">Dilin desteklediği sözdizimi < from_source1 > JOIN < from_source2 > birleştirme ediyor... < From_sourceN > katılın.</span><span class="sxs-lookup"><span data-stu-id="fdd23-499">The syntax that the language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="fdd23-500">Genel olarak, bu bir dizi döndürür **N**- diziler (ile tanımlama grubu **N** değerleri).</span><span class="sxs-lookup"><span data-stu-id="fdd23-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="fdd23-501">Her tanımlama grubu tüm koleksiyon diğer adları kendi ilgili ayarlar yineleme tarafından üretilen değerler içeriyor.</span><span class="sxs-lookup"><span data-stu-id="fdd23-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="fdd23-502">Diğer bir deyişle, bu bir tam çapraz birleştirme katılan kümeleri ürünüdür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-502">In other words, this is a full cross product of the sets participating in the join.</span></span>

<span data-ttu-id="fdd23-503">Aşağıdaki örnekler, JOIN yan tümcesi nasıl çalıştığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-503">The following examples show how the JOIN clause works.</span></span> <span data-ttu-id="fdd23-504">Aşağıdaki örnekte, her bir belgenin kaynağından vektörel çarpımını itibaren sonucu boştur ve boş boştur.</span><span class="sxs-lookup"><span data-stu-id="fdd23-504">In the following example, the result is empty since the cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="fdd23-505">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="fdd23-506">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="fdd23-507">Aşağıdaki örnekte, birleştirme belge arasında köküdür ve `children` subroot.</span><span class="sxs-lookup"><span data-stu-id="fdd23-507">In the following example, the join is between the document root and the `children` subroot.</span></span> <span data-ttu-id="fdd23-508">Bu, iki JSON nesnesi arasındaki arası bir üründür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="fdd23-509">Biz alt öğeleri dizisi için tek bir kök çalışıyorsanız bu yana alt öğeleri olan bir dizi olgu birleştirme etkili değildir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-509">The fact that children is an array is not effective in the JOIN since we are dealing with a single root that is the children array.</span></span> <span data-ttu-id="fdd23-510">Bu nedenle tam olarak yalnızca bir belge diziye sahip her bir belgenin vektörel çarpımını üretir beri sonucu yalnızca iki sonucu içerir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-510">Hence the result contains only two results, since the cross product of each document with the array yields exactly only one document.</span></span>

<span data-ttu-id="fdd23-511">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="fdd23-512">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="fdd23-513">Aşağıdaki örnek, daha geleneksel bir birleştirme gösterir:</span><span class="sxs-lookup"><span data-stu-id="fdd23-513">The following example shows a more conventional join:</span></span>

<span data-ttu-id="fdd23-514">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="fdd23-515">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-515">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]



<span data-ttu-id="fdd23-516">Dikkat edilecek ilk şey olan `from_source` , **katılma** yan tümcesi olan yineleyici.</span><span class="sxs-lookup"><span data-stu-id="fdd23-516">The first thing to note is that the `from_source` of the **JOIN** clause is an iterator.</span></span> <span data-ttu-id="fdd23-517">Bu nedenle, akış bu durumda aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="fdd23-517">So, the flow in this case is as follows:</span></span>  

* <span data-ttu-id="fdd23-518">Her alt öğesi genişletin **c** dizideki.</span><span class="sxs-lookup"><span data-stu-id="fdd23-518">Expand each child element **c** in the array.</span></span>
* <span data-ttu-id="fdd23-519">Çapraz ürün belgenin kökü ile geçerli **f** her alt öğesi olan **c** ilk adımda düzleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="fdd23-519">Apply a cross product with the root of the document **f** with each child element **c** that was flattened in the first step.</span></span>
* <span data-ttu-id="fdd23-520">Son olarak, kök nesnesi proje **f** name özelliği bırakır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-520">Finally, project the root object **f** name property alone.</span></span> 

<span data-ttu-id="fdd23-521">İlk belgeyi (`AndersenFamily`) yalnızca bu belgeye karşılık gelen tek bir nesne sonuç kümesini içerecek şekilde yalnızca bir alt öğe içeriyor.</span><span class="sxs-lookup"><span data-stu-id="fdd23-521">The first document (`AndersenFamily`) contains only one child element, so the result set contains only a single object corresponding to this document.</span></span> <span data-ttu-id="fdd23-522">İkinci belge (`WakefieldFamily`) iki alt öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-522">The second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="fdd23-523">Bu nedenle, çapraz ürün, böylece bu belgeye karşılık gelen her bir alt için iki nesne sonuçta her bir alt için ayrı bir nesne oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fdd23-523">So, the cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding to this document.</span></span> <span data-ttu-id="fdd23-524">Bir çapraz ürün beklendiği gibi hem bu belgeleri kök alanları aynıdır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-524">The root fields in both these documents are the same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="fdd23-525">Gerçek katılma form başlıkları, aksi takdirde projeye zor olan bir şekil içinde çapraz ürünün programıdır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-525">The real utility of the JOIN is to form tuples from the cross-product in a shape that's otherwise difficult to project.</span></span> <span data-ttu-id="fdd23-526">Ayrıca, aşağıdaki örnekte, biz gördüğünüz gibi sağlar tarafından başlıklar genel memnun bir koşul kullanıcının seçtiği bir tanımlama grubu birleşimi filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-526">Furthermore, as we see in the example below, you could filter on the combination of a tuple that lets' the user chose a condition satisfied by the tuples overall.</span></span>

<span data-ttu-id="fdd23-527">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="fdd23-528">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-528">**Results**</span></span>

    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]



<span data-ttu-id="fdd23-529">Bu örnek önceki örnekte doğal bir uzantıdır ve çift birleştirme gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-529">This example is a natural extension of the preceding example, and performs a double join.</span></span> <span data-ttu-id="fdd23-530">Bu nedenle, çapraz ürün aşağıdaki sözde kodu olarak görüntülenebilir:</span><span class="sxs-lookup"><span data-stu-id="fdd23-530">So, the cross product can be viewed as the following pseudo-code:</span></span>

    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }

<span data-ttu-id="fdd23-531">`AndersenFamily`bir evcil hayvan sahip bir alt sahiptir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="fdd23-532">Bu nedenle, bir satır çapraz ürün verir (1\*1\*1) bu aile gelen.</span><span class="sxs-lookup"><span data-stu-id="fdd23-532">So, the cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="fdd23-533">WakefieldFamily ancak iki alt öğe, ancak yalnızca bir alt "Jesse" Evcil Hayvanlar içeriyor.</span><span class="sxs-lookup"><span data-stu-id="fdd23-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="fdd23-534">Jesse iki Evcil Hayvanlar yine de vardır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-534">Jesse has two pets though.</span></span> <span data-ttu-id="fdd23-535">Bu nedenle çapraz ürün 1 verir\*1\*2 = 2 Bu ailesinden satırlar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-535">Hence the cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="fdd23-536">Sonraki örnekte olduğundan bir ek filtre `pet`.</span><span class="sxs-lookup"><span data-stu-id="fdd23-536">In the next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="fdd23-537">Burada Evcil adı "Gölge" değil tüm başlıklar dışlar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-537">This excludes all the tuples where the pet name is not "Shadow".</span></span> <span data-ttu-id="fdd23-538">Biz diziler dizileri, herhangi bir tanımlama grubu öğelerinin filtre gelen derleme ve öğeleri herhangi bir bileşimini proje olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="fdd23-538">Notice that we are able to build tuples from arrays, filter on any of the elements of the tuple, and project any combination of the elements.</span></span> 

<span data-ttu-id="fdd23-539">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="fdd23-540">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="fdd23-541"><a id="JavaScriptIntegration"></a>JavaScript tümleştirme</span><span class="sxs-lookup"><span data-stu-id="fdd23-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="fdd23-542">Azure Cosmos DB JavaScript tabanlı uygulama mantığını saklı yordamları ve Tetikleyicileri bakımından koleksiyonlar üzerinde doğrudan yürütmek için bir programlama modeli sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="fdd23-543">Bu, her ikisi için sağlar:</span><span class="sxs-lookup"><span data-stu-id="fdd23-543">This allows for both:</span></span>

* <span data-ttu-id="fdd23-544">Yüksek performanslı işlem CRUD işlemleri ve belgeleri doğrudan veritabanı altyapısının içinde JavaScript çalışma zamanı derin tümleştirmesi sayesinde bir koleksiyondaki sorguları yeteneği.</span><span class="sxs-lookup"><span data-stu-id="fdd23-544">Ability to do high-performance transactional CRUD operations and queries against documents in a collection by virtue of the deep integration of JavaScript runtime directly within the database engine.</span></span> 
* <span data-ttu-id="fdd23-545">Denetim akışı, değişken kapsamı, atama ve özel durum işleme temelleri veritabanı işlemleri ile tümleştirilmesi doğal bir model.</span><span class="sxs-lookup"><span data-stu-id="fdd23-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="fdd23-546">JavaScript tümleştirme için Azure Cosmos DB desteği hakkında daha fazla ayrıntı için lütfen JavaScript sunucu tarafı programlama belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="fdd23-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer to the JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="fdd23-547"><a id="UserDefinedFunctions"></a>Kullanıcı tanımlı işlevler (UDF'ler)</span><span class="sxs-lookup"><span data-stu-id="fdd23-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="fdd23-548">Bu makalede önceden tanımlanmış türleri ile birlikte, DocumentDB API SQL kullanıcı tanımlı işlevler (UDF) için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-548">Along with the types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="fdd23-549">Özellikle, skaler UDF'ler burada geliştiriciler sıfır veya daha çok değişkenlerinde geçirmek ve geri tek bağımsız değişken sonuç desteklenir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-549">In particular, scalar UDFs are supported where the developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="fdd23-550">Bu değişkenin her biri geçerli JSON değerleri olmak için denetlenir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="fdd23-551">DocumentDB API SQL söz dizimi, bu kullanıcı tanımlı işlevler kullanılarak özel uygulama mantığını destekleyecek şekilde genişletilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-551">The DocumentDB API SQL syntax is extended to support custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="fdd23-552">UDF'ler DocumentDB API'si ile kayıtlı olması ve sonra bir SQL sorgusu bir parçası olarak başvurulan.</span><span class="sxs-lookup"><span data-stu-id="fdd23-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="fdd23-553">Aslında, UDF'ler exquisitely sorgular tarafından çağrılan için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-553">In fact, the UDFs are exquisitely designed to be invoked by queries.</span></span> <span data-ttu-id="fdd23-554">Bu seçenek için bir corollary UDF'ler diğer JavaScript türleri (saklı yordamları ve Tetikleyicileri) olan bağlam nesnesi erişiminiz yok.</span><span class="sxs-lookup"><span data-stu-id="fdd23-554">As a corollary to this choice, UDFs do not have access to the context object which the other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="fdd23-555">Salt okunur olarak sorguları yürütmek olduğundan, birincil veya ikincil çoğaltmaları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="fdd23-556">Bu nedenle, UDF'ler, diğer JavaScript türlerinin aksine ikincil çoğaltmalar üzerinde çalışmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-556">Therefore, UDFs are designed to run on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="fdd23-557">Aşağıda, özellikle bir belge koleksiyonu altında Cosmos DB veritabanı sırasında bir UDF nasıl kaydedilebilir bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-557">Below is an example of how a UDF can be registered at the Cosmos DB database, specifically under a document collection.</span></span>

       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  

<span data-ttu-id="fdd23-558">Önceki örnekte adı olan bir UDF oluşturur `REGEX_MATCH`.</span><span class="sxs-lookup"><span data-stu-id="fdd23-558">The preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="fdd23-559">İki JSON dizesi değerlerini kabul `input` ve `pattern` ve ilk eşleşme deseni ikinci belirtilmişse denetimleri kullanarak JavaScript'in string.match() işlevi.</span><span class="sxs-lookup"><span data-stu-id="fdd23-559">It accepts two JSON string values `input` and `pattern` and checks if the first matches the pattern specified in the second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="fdd23-560">Bir yansıtma sorgu Biz bu UDF artık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="fdd23-561">UDF'ler büyük küçük harfe duyarlı önekiyle "udf." nitelenmiş olmalıdır</span><span class="sxs-lookup"><span data-stu-id="fdd23-561">UDFs must be qualified with the case-sensitive prefix "udf."</span></span> <span data-ttu-id="fdd23-562">gelen sorgulara çağrıldığında.</span><span class="sxs-lookup"><span data-stu-id="fdd23-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="fdd23-563">3/17/2015 öncesinde Cosmos DB "udf." olmadan UDF çağrı desteklenir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-563">Prior to 3/17/2015, Cosmos DB supported UDF calls without the "udf."</span></span> <span data-ttu-id="fdd23-564">önek seçin REGEX_MATCH() ister.</span><span class="sxs-lookup"><span data-stu-id="fdd23-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="fdd23-565">Bu arama deseni kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="fdd23-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="fdd23-566">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="fdd23-567">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="fdd23-568">UDF de bir filtre içinde de "udf ile." tam aşağıdaki örnekte gösterildiği gibi kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="fdd23-568">The UDF can also be used inside a filter as shown in the example below, also qualified with the "udf."</span></span> <span data-ttu-id="fdd23-569">öneki:</span><span class="sxs-lookup"><span data-stu-id="fdd23-569">prefix:</span></span>

<span data-ttu-id="fdd23-570">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="fdd23-571">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="fdd23-572">Esas olarak, UDF'ler geçerli skaler ifadelerini ve tahminleri ve filtreleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="fdd23-573">UDF'ler gücüyle genişletmek için başka bir örneğe koşullu mantığı ile bakalım:</span><span class="sxs-lookup"><span data-stu-id="fdd23-573">To expand on the power of UDFs, let's look at another example with conditional logic:</span></span>

       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);


<span data-ttu-id="fdd23-574">UDF uygular örneği aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-574">Below is an example that exercises the UDF.</span></span>

<span data-ttu-id="fdd23-575">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="fdd23-576">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-576">**Results**</span></span>

     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]


<span data-ttu-id="fdd23-577">Önceki örneklerde sergiler gibi UDF'ler JavaScript dil gücünü yerleşik JavaScript çalışma zamanı yeteneklerini yardımıyla karmaşık bir yordam, koşullu mantık yapmak için zengin bir programlanabilir arabirimi sağlamak için DocumentDB API SQL ile tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="fdd23-577">As the preceding examples showcase, UDFs integrate the power of JavaScript language with the DocumentDB API SQL to provide a rich programmable interface to do complex procedural, conditional logic with the help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="fdd23-578">DocumentDB API SQL bağımsız değişkenler için UDF'ler kaynağındaki her belge için UDF işleme geçerli aşamada (WHERE yan tümcesi veya SELECT yan tümcesi) sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-578">DocumentDB API SQL provides the arguments to the UDFs for each document in the source at the current stage (WHERE clause or SELECT clause) of processing the UDF.</span></span> <span data-ttu-id="fdd23-579">Sonuç genel yürütme ardışık düzeninde sorunsuz olarak eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-579">The result is incorporated in the overall execution pipeline seamlessly.</span></span> <span data-ttu-id="fdd23-580">Özellikler başvurulan tarafından UDF parametreleri JSON değeri kullanılabilir değil, parametre olarak kabul tanımlanmamış ve bu nedenle UDF çağırma tamamen atlandı.</span><span class="sxs-lookup"><span data-stu-id="fdd23-580">If the properties referred to by the UDF parameters are not available in the JSON value, the parameter is considered as undefined and hence the UDF invocation is entirely skipped.</span></span> <span data-ttu-id="fdd23-581">Benzer şekilde UDF sonucu tanımsız ise, sonuçta bulunmaz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-581">Similarly if the result of the UDF is undefined, it's not included in the result.</span></span> 

<span data-ttu-id="fdd23-582">Özet olarak, UDF'ler karmaşık iş mantığı sorgu bir parçası olarak yapmak için harika araçlardır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-582">In summary, UDFs are great tools to do complex business logic as part of the query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="fdd23-583">İşleç değerlendirme</span><span class="sxs-lookup"><span data-stu-id="fdd23-583">Operator evaluation</span></span>
<span data-ttu-id="fdd23-584">Cosmos DB, bir JSON veritabanı olan virtue tarafından JavaScript işleçleri ve değerlendirme semantiği ile parallels çizer.</span><span class="sxs-lookup"><span data-stu-id="fdd23-584">Cosmos DB, by the virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="fdd23-585">JSON desteği bakımından JavaScript sematiğini korumak Cosmos DB çalışır, ancak bazı durumlarda işlemi değerlendirme farklıdır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-585">While Cosmos DB tries to preserve JavaScript semantics in terms of JSON support, the operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="fdd23-586">Değerleri veritabanından kadar DocumentDB API SQL'de aksine geleneksel SQL değerlerin türleri bilinmez genellikle.</span><span class="sxs-lookup"><span data-stu-id="fdd23-586">In DocumentDB API SQL, unlike in traditional SQL, the types of values are often not known until the values are retrieved from database.</span></span> <span data-ttu-id="fdd23-587">Verimli bir şekilde sorguları yürütmek için işleçleri çoğunu sıkı tür gereksinimleri vardır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-587">In order to efficiently execute queries, most of the operators have strict type requirements.</span></span> 

<span data-ttu-id="fdd23-588">DocumentDB API SQL JavaScript aksine örtük dönüşümler gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="fdd23-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="fdd23-589">Örneğin, bir sorgu ister `SELECT * FROM Person p WHERE p.Age = 21` eşleşen değeri olan 21 yaş özelliği içeren belgeleri.</span><span class="sxs-lookup"><span data-stu-id="fdd23-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="fdd23-590">"021", "21.0", "0021", "00021" dize "21", veya diğer büyük olasılıkla sonsuz Çeşitlemeler, yaş özelliği eşleşen herhangi bir belge ister, vb. eşlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="fdd23-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="fdd23-591">Bunun aksine dize değerleri nerede sayılara örtük olarak Integer JavaScript sağlamaktır (örneğin, operatöre dayanan: ==).</span><span class="sxs-lookup"><span data-stu-id="fdd23-591">This is in contrast to the JavaScript where the string values are implicitly casted to numbers (based on operator, ex: ==).</span></span> <span data-ttu-id="fdd23-592">Bu seçenek, DocumentDB API SQL'de eşleşen verimli dizin için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="fdd23-593">Parametreli SQL sorguları</span><span class="sxs-lookup"><span data-stu-id="fdd23-593">Parameterized SQL queries</span></span>
<span data-ttu-id="fdd23-594">Cosmos DB bilinen gösterimi @ ile ifade parametrelerle sorguları destekler.</span><span class="sxs-lookup"><span data-stu-id="fdd23-594">Cosmos DB supports queries with parameters expressed with the familiar @ notation.</span></span> <span data-ttu-id="fdd23-595">Parametreli SQL sağlam işleme ve kullanıcı girişi, SQL ekleme üzerinden veri yanlışlıkla açığa çıkmaya önleme, kaçış sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="fdd23-596">Örneğin, Soyadı ve adres durumu kullandığı parametreler bir sorgu yazın ve son adı ve kullanıcı girişini temel alarak adresi durumunun çeşitli değerlerin yürütün.</span><span class="sxs-lookup"><span data-stu-id="fdd23-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="fdd23-597">Bu istek sonra Cosmos DB gibi parametreli bir JSON sorgu olarak aşağıda gösterilen gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-597">This request can then be sent to Cosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="fdd23-598">İLK bağımsız değişkeni gibi parametreli sorgular kullanmayı aşağıda gösterilen ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-598">The argument to TOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="fdd23-599">Parametre değerleri geçerli bir JSON olabilir (dizeler, sayılar, Boole değerlerini, null, hatta dizileri veya JSON iç içe geçmiş).</span><span class="sxs-lookup"><span data-stu-id="fdd23-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="fdd23-600">Ayrıca parametreleri Cosmos DB Şeması daha az olduğundan, karşı herhangi bir tür doğrulanmaz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="fdd23-601"><a id="BuiltinFunctions"></a>Yerleşik işlevler</span><span class="sxs-lookup"><span data-stu-id="fdd23-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="fdd23-602">Cosmos DB yerleşik işlevleri gibi kullanıcı tanımlı işlevler (UDF'ler) sorguları içinde kullanılan ortak işlemleri için de destekler.</span><span class="sxs-lookup"><span data-stu-id="fdd23-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="fdd23-603">İşlev grubu</span><span class="sxs-lookup"><span data-stu-id="fdd23-603">Function group</span></span>          | <span data-ttu-id="fdd23-604">İşlemler</span><span class="sxs-lookup"><span data-stu-id="fdd23-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fdd23-605">Matematik işlevleri</span><span class="sxs-lookup"><span data-stu-id="fdd23-605">Mathematical functions</span></span>  | <span data-ttu-id="fdd23-606">ABS TAVAN, EXP, FLOOR, günlük, LOG10, güç, HEPSİNİ, oturum, SQRT, KARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, derece, PI, radyan, SIN ve TAN</span><span class="sxs-lookup"><span data-stu-id="fdd23-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="fdd23-607">Denetimi işlevleri yazın</span><span class="sxs-lookup"><span data-stu-id="fdd23-607">Type checking functions</span></span> | <span data-ttu-id="fdd23-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED ve IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="fdd23-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="fdd23-609">Dize işlevleri</span><span class="sxs-lookup"><span data-stu-id="fdd23-609">String functions</span></span>        | <span data-ttu-id="fdd23-610">CONCAT, içerir, ENDSWITH, INDEX_OF, sol, uzunluk, alt, LTRIM, Değiştir, çoğaltılması, geriye doğru sağ, RTRIM, STARTSWITH, SUBSTRING ve üst</span><span class="sxs-lookup"><span data-stu-id="fdd23-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="fdd23-611">Dizi işlevleri</span><span class="sxs-lookup"><span data-stu-id="fdd23-611">Array functions</span></span>         | <span data-ttu-id="fdd23-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH ve ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="fdd23-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="fdd23-613">Uzamsal işlevleri</span><span class="sxs-lookup"><span data-stu-id="fdd23-613">Spatial functions</span></span>       | <span data-ttu-id="fdd23-614">St_dıstance, ST_WITHIN, ST_INTERSECTS, ST_ISVALID ve ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="fdd23-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="fdd23-615">Şu anda yerleşik işlevi olduğu şimdi kullanılabilir bir kullanıcı tanımlı işlev (UDF) kullanıyorsanız, bunu çalıştırmak daha hızlı olacak şekilde karşılık gelen yerleşik işlevi kullanmalıdır ve daha verimli bir şekilde.</span><span class="sxs-lookup"><span data-stu-id="fdd23-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use the corresponding built-in function as it is going to be quicker to run and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="fdd23-616">Matematik işlevleri</span><span class="sxs-lookup"><span data-stu-id="fdd23-616">Mathematical functions</span></span>
<span data-ttu-id="fdd23-617">Matematik işlevleri her bağımsız değişken olarak sağlanır ve sayısal bir değeri döndürme giriş değerlerine göre bir hesaplama gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-617">The mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="fdd23-618">Burada, desteklenen yerleşik matematik işlevleri tablosu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="fdd23-619">Kullanım</span><span class="sxs-lookup"><span data-stu-id="fdd23-619">Usage</span></span> | <span data-ttu-id="fdd23-620">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdd23-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fdd23-621">[[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="fdd23-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="fdd23-622">Belirtilen sayısal ifade (pozitif) mutlak değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-622">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="fdd23-623">Üst SINIRA (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="fdd23-624">Büyüktür veya eşittir, belirtilen sayısal ifadenin en küçük tamsayı değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-624">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| [<span data-ttu-id="fdd23-625">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="fdd23-626">Belirtilen sayısal ifade küçük veya eşit en büyük tamsayıyı döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-626">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| [<span data-ttu-id="fdd23-627">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="fdd23-628">Belirtilen sayısal ifade üs döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-628">Returns the exponent of the specified numeric expression.</span></span> |
| <span data-ttu-id="fdd23-629">[Günlük (num_expr [, temel])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="fdd23-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="fdd23-630">Belirtilen sayısal ifade ya da belirtilen taban kullanarak logaritmasını doğal logaritmasını döndürür</span><span class="sxs-lookup"><span data-stu-id="fdd23-630">Returns the natural logarithm of the specified numeric expression, or the logarithm using the specified base</span></span> |
| [<span data-ttu-id="fdd23-631">Log10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="fdd23-632">Belirtilen sayısal ifade 10 tabanında Logaritmik değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-632">Returns the base-10 logarithmic value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="fdd23-633">ROUND (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="fdd23-634">En yakın tamsayı değerine yuvarlanan sayısal bir değer döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-634">Returns a numeric value, rounded to the closest integer value.</span></span> |
| [<span data-ttu-id="fdd23-635">TRUNC (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="fdd23-636">En yakın tamsayı değerine kesilmiş sayısal bir değer döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-636">Returns a numeric value, truncated to the closest integer value.</span></span> |
| [<span data-ttu-id="fdd23-637">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="fdd23-638">Belirtilen sayısal ifade kare kökünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-638">Returns the square root of the specified numeric expression.</span></span> |
| [<span data-ttu-id="fdd23-639">KARE (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="fdd23-640">Belirtilen sayısal ifade kare döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-640">Returns the square of the specified numeric expression.</span></span> |
| [<span data-ttu-id="fdd23-641">GÜÇ (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="fdd23-642">Belirtilen sayısal ifade gücünü belirtilen değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-642">Returns the power of the specified numeric expression to the value specified.</span></span> |
| [<span data-ttu-id="fdd23-643">OTURUM (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="fdd23-644">İşareti (-1, 0, 1) belirtilen sayısal ifadenin değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-644">Returns the sign value (-1, 0, 1) of the specified numeric expression.</span></span> |
| [<span data-ttu-id="fdd23-645">ACOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="fdd23-646">Açının kosinüsü belirtilen sayısal ifadesidir radyan cinsinden döndürür; arccosine olarak da bilinir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-646">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="fdd23-647">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="fdd23-648">Açının sinüsü belirtilen sayısal ifadesidir radyan cinsinden döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-648">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="fdd23-649">Bu arksinüsünü olarak da adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="fdd23-650">ATAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="fdd23-651">Açının tanjantı belirtilen sayısal ifadesidir radyan cinsinden döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-651">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="fdd23-652">Bu arktanjantını olarak da adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="fdd23-653">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="fdd23-654">Burada açıyı pozitif x ekseni ve noktasına (y, x), kaynaktan ray arasında radyan cinsinden döndürür x ve y iki belirtilen float ifadeleri değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-654">Returns the angle, in radians, between the positive x-axis and the ray from the origin to the point (y, x), where x and y are the values of the two specified float expressions.</span></span> |
| [<span data-ttu-id="fdd23-655">COS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="fdd23-656">Radyan cinsinden belirtilen ifade trigonometrik belirtilen açının kosinüsünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-656">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="fdd23-657">COT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="fdd23-658">Belirtilen açının trigonometrik kotanjantını radyan cinsinden belirtilen sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-658">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span> |
| [<span data-ttu-id="fdd23-659">DERECE (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="fdd23-660">Radyan cinsinden Açı derece cinsinden karşılık gelen açıyı döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-660">Returns the corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="fdd23-661">PI)</span><span class="sxs-lookup"><span data-stu-id="fdd23-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="fdd23-662">PI sayısının sabit değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-662">Returns the constant value of PI.</span></span> |
| [<span data-ttu-id="fdd23-663">Radyan CİNSİNDEN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="fdd23-664">Derece sayısal bir ifadenin girildiğinde radyan cinsinden döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="fdd23-665">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="fdd23-666">Radyan cinsinden belirtilen ifade trigonometrik belirtilen açının sinüsünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-666">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="fdd23-667">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="fdd23-668">Belirtilen ifade giriş ifadesi tanjantını döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-668">Returns the tangent of the input expression, in the specified expression.</span></span> |

<span data-ttu-id="fdd23-669">Örneğin, şimdi aşağıdaki gibi sorguları çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fdd23-669">For example, you can now run queries like the following:</span></span>

<span data-ttu-id="fdd23-670">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="fdd23-671">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-671">**Results**</span></span>

    [4]

<span data-ttu-id="fdd23-672">ANSI SQL karşılaştırıldığında Cosmos veritabanı işlevleri arasındaki temel fark, bunlar da şema küçüktür ve karma şema verilerle çalışmak üzere tasarlanmıştır ' dir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-672">The main difference between Cosmos DB’s functions compared to ANSI SQL is that they are designed to work well with schema-less and mixed schema data.</span></span> <span data-ttu-id="fdd23-673">Örneğin, burada Size özelliği eksik veya sahip bir belgeniz varsa "Bilinmeyen" gibi bir sayısal olmayan değer sonra belge üzerinde bir hata döndürüyor yerine atlanır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-673">For example, if you have a document where the Size property is missing, or has a non-numeric value like “unknown”, then the document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="fdd23-674">Denetimi işlevleri yazın</span><span class="sxs-lookup"><span data-stu-id="fdd23-674">Type checking functions</span></span>
<span data-ttu-id="fdd23-675">Tür denetleme işlevleri SQL sorguları içinde bir ifade türünü kontrol olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-675">The type checking functions allow you to check the type of an expression within SQL queries.</span></span> <span data-ttu-id="fdd23-676">Tür denetleme işlevleri, değişken veya bilinmeyen olduğunda kolay bir şekilde belgelerde özellikleri türünü belirlemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-676">Type checking functions can be used to determine the type of properties within documents on the fly when it is variable or unknown.</span></span> <span data-ttu-id="fdd23-677">Burada, desteklenen yerleşik tür işlevleri denetlemesini tablosu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="fdd23-678"><strong>Kullanım</strong></span><span class="sxs-lookup"><span data-stu-id="fdd23-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="fdd23-679"><strong>Açıklama</strong></span><span class="sxs-lookup"><span data-stu-id="fdd23-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fdd23-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (ifade)</a></span><span class="sxs-lookup"><span data-stu-id="fdd23-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="fdd23-681">Değerin türü bir dizi olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-681">Returns a Boolean indicating if the type of the value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fdd23-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (ifade)</a></span><span class="sxs-lookup"><span data-stu-id="fdd23-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="fdd23-683">Türde bir değer bir Boole değeri olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-683">Returns a Boolean indicating if the type of the value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fdd23-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (ifade)</a></span><span class="sxs-lookup"><span data-stu-id="fdd23-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="fdd23-685">Değerin türü null olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-685">Returns a Boolean indicating if the type of the value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fdd23-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (ifade)</a></span><span class="sxs-lookup"><span data-stu-id="fdd23-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="fdd23-687">Türde bir değer bir sayı olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-687">Returns a Boolean indicating if the type of the value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fdd23-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (ifade)</a></span><span class="sxs-lookup"><span data-stu-id="fdd23-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="fdd23-689">Değerin türü bir JSON nesnesi olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-689">Returns a Boolean indicating if the type of the value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fdd23-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (ifade)</a></span><span class="sxs-lookup"><span data-stu-id="fdd23-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="fdd23-691">Değerin türü bir dize olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-691">Returns a Boolean indicating if the type of the value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fdd23-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (ifade)</a></span><span class="sxs-lookup"><span data-stu-id="fdd23-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="fdd23-693">Özellik değeri atanmış olan gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-693">Returns a Boolean indicating if the property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fdd23-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (ifade)</a></span><span class="sxs-lookup"><span data-stu-id="fdd23-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="fdd23-695">Değerin türü bir dize, sayı, Boole veya null olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-695">Returns a Boolean indicating if the type of the value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="fdd23-696">Bu işlevler kullanılarak, şimdi aşağıdaki gibi sorguları çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fdd23-696">Using these functions, you can now run queries like the following:</span></span>

<span data-ttu-id="fdd23-697">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="fdd23-698">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="fdd23-699">Dize işlevleri</span><span class="sxs-lookup"><span data-stu-id="fdd23-699">String functions</span></span>
<span data-ttu-id="fdd23-700">Aşağıdaki skaler işlevler dize giriş değeri üzerinde bir işlemi gerçekleştirmek ve bir dize, sayısal ya da Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-700">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="fdd23-701">Yerleşik dize işlevleri tablosu aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="fdd23-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="fdd23-702">Kullanım</span><span class="sxs-lookup"><span data-stu-id="fdd23-702">Usage</span></span> | <span data-ttu-id="fdd23-703">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdd23-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="fdd23-704">UZUNLUĞU (str_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="fdd23-705">Belirtilen dize ifadesinin karakterlerin sayısını döndürür</span><span class="sxs-lookup"><span data-stu-id="fdd23-705">Returns the number of characters of the specified string expression</span></span> |
| <span data-ttu-id="fdd23-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="fdd23-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="fdd23-707">İki veya daha fazla dize değerlerini birleştirme sonucu olan bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-707">Returns a string that is the result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="fdd23-708">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="fdd23-709">Bir dize ifadesi bölümünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="fdd23-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="fdd23-711">Döndürür Boolean belirten bir ilk ifade dize olup olmadığını ve ikinci sona erer</span><span class="sxs-lookup"><span data-stu-id="fdd23-711">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="fdd23-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="fdd23-713">Döndürür Boolean belirten bir ilk ifade dize olup olmadığını ve ikinci sona erer</span><span class="sxs-lookup"><span data-stu-id="fdd23-713">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="fdd23-714">İÇERİR (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="fdd23-715">Döndüren bir Boolean belirten ikinci ilk ifade dize olup olmadığını içerir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-715">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |
| [<span data-ttu-id="fdd23-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="fdd23-717">İkinci ilk örneğinin başlangıç konumunu döndürür dizesi ifade ilk belirtilen dize ifadesi veya -1 içinde dizesi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="fdd23-717">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span> |
| [<span data-ttu-id="fdd23-718">Sol (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="fdd23-719">Sol bölümü belirtilen sayıda karakteri içeren bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-719">Returns the left part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="fdd23-720">SAĞ (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="fdd23-721">Belirtilen sayıda karakteri içeren bir dize sağ bölümünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-721">Returns the right part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="fdd23-722">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="fdd23-723">Öndeki boşlukları kaldırır sonra bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="fdd23-724">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="fdd23-725">Tüm sondaki boşlukları kesilmesi sonrasında bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="fdd23-726">Alt (str_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="fdd23-727">Büyük harf karakter verileri küçük harfe dönüştürmek sonra bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-727">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| [<span data-ttu-id="fdd23-728">ÜST (str_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="fdd23-729">Küçük harf karakter verileri büyük harfe dönüştürme sonra bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-729">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| [<span data-ttu-id="fdd23-730">REPLACE (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="fdd23-731">Belirtilen dize değeri tüm oluşumlarını başka bir dize değeri ile değiştirir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="fdd23-732">REPLICATE (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="fdd23-733">Bir dize değeri, belirtilen sayıda yineler.</span><span class="sxs-lookup"><span data-stu-id="fdd23-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="fdd23-734">Ters (str_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="fdd23-735">Ters sırada bir dize değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-735">Returns the reverse order of a string value.</span></span> |

<span data-ttu-id="fdd23-736">Bu işlevleri kullanarak, şimdi aşağıdaki gibi sorguları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-736">Using these functions, you can now run queries like the following.</span></span> <span data-ttu-id="fdd23-737">Örneğin, aile adı büyük şu şekilde döndürebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fdd23-737">For example, you can return the family name in uppercase as follows:</span></span>

<span data-ttu-id="fdd23-738">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="fdd23-739">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="fdd23-740">Veya bu örnekteki gibi dizeyi birleştirmek:</span><span class="sxs-lookup"><span data-stu-id="fdd23-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="fdd23-741">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="fdd23-742">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="fdd23-743">Dize işlevleri, WHERE yan tümcesinde aşağıdaki örnekte gibi sonuçları filtrelemek için de kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="fdd23-743">String functions can also be used in the WHERE clause to filter results, like in the following example:</span></span>

<span data-ttu-id="fdd23-744">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="fdd23-745">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="fdd23-746">Dizi işlevleri</span><span class="sxs-lookup"><span data-stu-id="fdd23-746">Array functions</span></span>
<span data-ttu-id="fdd23-747">Aşağıdaki skaler işlevler bir dizi giriş değeri ve return sayısal, Boole veya dizi değer üzerinde bir işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-747">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="fdd23-748">Yerleşik dizi işlevleri tablosu aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="fdd23-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="fdd23-749">Kullanım</span><span class="sxs-lookup"><span data-stu-id="fdd23-749">Usage</span></span> | <span data-ttu-id="fdd23-750">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdd23-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="fdd23-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="fdd23-752">Belirtilen dizi ifadesi öğe sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-752">Returns the number of elements of the specified array expression.</span></span> |
| <span data-ttu-id="fdd23-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="fdd23-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="fdd23-754">İki veya daha fazla dizi değerlerini birleştirme sonucu olan bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-754">Returns an array that is the result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="fdd23-755">[ARRAY_CONTAINS (arr_expr, ifade [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="fdd23-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="fdd23-756">Dizi belirtilen değeri içerip içermediğini gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-756">Returns a Boolean indicating whether the array contains the specified value.</span></span> <span data-ttu-id="fdd23-757">Tam veya kısmi eşleşme olup olmadığını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-757">Can specify if the match is full or partial.</span></span> |
| <span data-ttu-id="fdd23-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="fdd23-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="fdd23-759">Bir dizi ifadesi bölümünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="fdd23-760">Dizi işlevleri, JSON içinde diziler işlemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-760">Array functions can be used to manipulate arrays within JSON.</span></span> <span data-ttu-id="fdd23-761">Örneğin, bir üst "Deneme Wakefield" olduğu tüm belgeleri döndüren bir sorgu aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-761">For example, here's a query that returns all documents where one of the parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="fdd23-762">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="fdd23-763">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="fdd23-764">Dizi öğeleri eşleşen bir kısmi parça belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-764">You can specify a partial fragment for matching elements within the array.</span></span> <span data-ttu-id="fdd23-765">Aşağıdaki sorgu ile tüm üst bulur `givenName` , `Robin`.</span><span class="sxs-lookup"><span data-stu-id="fdd23-765">The following query finds all parents with the `givenName` of `Robin`.</span></span>

<span data-ttu-id="fdd23-766">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="fdd23-767">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="fdd23-768">Burada, aile başına alt sayısını almak için ARRAY_LENGTH kullanan başka bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-768">Here's another example that uses ARRAY_LENGTH to get the number of children per family.</span></span>

<span data-ttu-id="fdd23-769">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="fdd23-770">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="fdd23-771">Uzamsal işlevleri</span><span class="sxs-lookup"><span data-stu-id="fdd23-771">Spatial functions</span></span>
<span data-ttu-id="fdd23-772">Cosmos DB Jeo-uzamsal sorgulamak için aşağıdaki açık Jeo-uzamsal Konsorsiyumu (OGC) yerleşik işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="fdd23-772">Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="fdd23-773"><strong>Kullanım</strong></span><span class="sxs-lookup"><span data-stu-id="fdd23-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="fdd23-774"><strong>Açıklama</strong></span><span class="sxs-lookup"><span data-stu-id="fdd23-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fdd23-775">St_dıstance (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="fdd23-776">İki GeoJSON noktası, çokgen veya LineString ifadeleri uzaklığı döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-776">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fdd23-777">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="fdd23-778">İlk GeoJSON nesne (noktası, çokgen veya LineString) ikinci GeoJSON nesne içinde (noktası, çokgen veya LineString) olup olmadığını gösteren bir Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-778">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fdd23-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="fdd23-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="fdd23-780">İki belirtilen GeoJSON nesne (noktası, çokgen veya LineString) kesiştiği olup olmadığını gösteren bir Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-780">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fdd23-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="fdd23-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="fdd23-782">Belirtilen GeoJSON noktası, çokgen veya LineString ifade geçerli olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-782">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="fdd23-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="fdd23-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="fdd23-784">Belirtilen GeoJSON noktası, çokgen veya LineString ifade geçerli olup olmadığını ve geçersiz bir Boole değeri içeren bir JSON değeri değeri döndürür, ayrıca bir dize değeri olarak nedeni.</span><span class="sxs-lookup"><span data-stu-id="fdd23-784">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="fdd23-785">Uzamsal işlevleri uzamsal veriler yakınlaştırmalı sorguları gerçekleştirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-785">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="fdd23-786">Örneğin, içinde 30 km st_dıstance yerleşik işlevini kullanarak belirtilen konumun olan tüm ailesi belgeleri döndüren bir sorgu aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-786">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="fdd23-787">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="fdd23-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="fdd23-788">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="fdd23-789">Cosmos DB Jeo-uzamsal desteği hakkında daha fazla ayrıntı için lütfen bkz. [Azure Cosmos veritabanı Jeo-uzamsal verilerle çalışma](geospatial.md).</span><span class="sxs-lookup"><span data-stu-id="fdd23-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="fdd23-790">Cosmos DB için uzamsal işlevleri ve SQL söz dizimi, sarmalar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-790">That wraps up spatial functions, and the SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="fdd23-791">Şimdi nasıl çalışır ve sözdizimi ile nasıl etkileşim kurduğu sorgulama LINQ kadarki gördük bir bakalım.</span><span class="sxs-lookup"><span data-stu-id="fdd23-791">Now let's take a look at how LINQ querying works and how it interacts with the syntax we've seen so far.</span></span>

## <span data-ttu-id="fdd23-792"><a id="Linq"></a>LINQ-DocumentDB API SQL</span><span class="sxs-lookup"><span data-stu-id="fdd23-792"><a id="Linq"></a>LINQ to DocumentDB API SQL</span></span>
<span data-ttu-id="fdd23-793">LINQ, hesaplama nesnelerin akışları sorgular olarak ifade eder ve .NET çalışan bir programlama modelidir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="fdd23-794">Cosmos DB LINQ ile arabirim oluşturmak için bir istemci-tarafı kitaplığı, JSON ve .NET nesneleri ve bir alt kümesinden LINQ sorgularını eşleme Cosmos DB sorgulara arasında dönüştürme kolaylaştırarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-794">Cosmos DB provides a client-side library to interface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries to Cosmos DB queries.</span></span> 

<span data-ttu-id="fdd23-795">Aşağıdaki resimde Cosmos DB kullanarak LINQ sorgularını destekleme mimarisi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-795">The picture below shows the architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="fdd23-796">Cosmos DB İstemcisi'ni kullanarak geliştiriciler oluşturabilir bir **Iqueryable** doğrudan sonra Cosmos DB sorguda LINQ sorgusu çevirir Cosmos DB sorgu sağlayıcısı sorgular nesnesi.</span><span class="sxs-lookup"><span data-stu-id="fdd23-796">Using the Cosmos DB client, developers can create an **IQueryable** object that directly queries the Cosmos DB query provider, which then translates the LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="fdd23-797">Sorgu daha sonra bir JSON biçiminde sonuç kümesi almak için Cosmos DB sunucuya geçirilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-797">The query is then passed to the Cosmos DB server to retrieve a set of results in JSON format.</span></span> <span data-ttu-id="fdd23-798">Döndürülen sonuçların, istemci tarafında .NET nesnelerin bir akışa serisi.</span><span class="sxs-lookup"><span data-stu-id="fdd23-798">The returned results are deserialized into a stream of .NET objects on the client side.</span></span>

![DocumentDB API - kullanarak LINQ sorgularını SQL söz dizimi, JSON sorgu dili, veritabanı kavramlarını ve SQL sorguları destekleyen mimarisi][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="fdd23-800">.NET ve JSON eşleme</span><span class="sxs-lookup"><span data-stu-id="fdd23-800">.NET and JSON mapping</span></span>
<span data-ttu-id="fdd23-801">.NET nesneleri ve JSON belgeleri arasında eşleme doğal - her bir veri üyesi alan burada alan adı nesne "anahtarı" parçası eşlendi ve "value" bölümü nesne değer bölümünü eşlenen yinelemeli bir JSON nesnesi ile eşleştirilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-801">The mapping between .NET objects and JSON documents is natural - each data member field is mapped to a JSON object, where the field name is mapped to the "key" part of the object and the "value" part is recursively mapped to the value part of the object.</span></span> <span data-ttu-id="fdd23-802">Aşağıdaki örneği göz önünde bulundurun: oluşturulan aile nesnesi, JSON belgesi eşlendiği, aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="fdd23-802">Consider the following example: The Family object created is mapped to the JSON document as shown below.</span></span> <span data-ttu-id="fdd23-803">Ve tersi, JSON belgesini bir .NET nesnesine eşlendi.</span><span class="sxs-lookup"><span data-stu-id="fdd23-803">And vice versa, the JSON document is mapped back to a .NET object.</span></span>

<span data-ttu-id="fdd23-804">**C# sınıfı**</span><span class="sxs-lookup"><span data-stu-id="fdd23-804">**C# Class**</span></span>

    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };


<span data-ttu-id="fdd23-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="fdd23-805">**JSON**</span></span>  

    {
        "id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam", 
                "givenName": "Jesse", 
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };



### <a name="linq-to-sql-translation"></a><span data-ttu-id="fdd23-806">LINQ-SQL çevirisi</span><span class="sxs-lookup"><span data-stu-id="fdd23-806">LINQ to SQL translation</span></span>
<span data-ttu-id="fdd23-807">Cosmos DB sorgu Sağlayıcısı'nı bir en iyi çaba eşleme Cosmos DB SQL sorgusu bir LINQ Sorgu gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-807">The Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="fdd23-808">Aşağıdaki açıklamasında okuyucu temel benzerlik LINQ sahip varsayalım.</span><span class="sxs-lookup"><span data-stu-id="fdd23-808">In the following description, we assume the reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="fdd23-809">İlk olarak, tür sistemi için tüm JSON ilkel türler – sayısal türler, boolean, dize ve null destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="fdd23-809">First, for the type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="fdd23-810">Yalnızca bu JSON türleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-810">Only these JSON types are supported.</span></span> <span data-ttu-id="fdd23-811">Aşağıdaki skaler ifadelerin desteklenir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-811">The following scalar expressions are supported.</span></span>

* <span data-ttu-id="fdd23-812">Sabit değerler – bunlar sorgu değerlendirilir zaman temel veri türlerinin sabit değerleri içerir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-812">Constant values – these include constant values of the primitive data types at the time the query is evaluated.</span></span>
* <span data-ttu-id="fdd23-813">Özellik/dizi dizini ifadeleri – bu ifadeler bir nesneyi veya bir dizi öğesine özelliğine bakın.</span><span class="sxs-lookup"><span data-stu-id="fdd23-813">Property/array index expressions – these expressions refer to the property of an object or an array element.</span></span>
  
     <span data-ttu-id="fdd23-814">ailesi. Kimliği;    Family.Children[0].familyName;    Family.Children[0].grade;    Family.Children[n].grade; n bir int değişkenidir</span><span class="sxs-lookup"><span data-stu-id="fdd23-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="fdd23-815">Aritmetik ifadeler - bunlar ortak aritmetik ifadeler sayısal ve Boole değerleri içerir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="fdd23-816">Tam listesi için SQL belirtimine bakın.</span><span class="sxs-lookup"><span data-stu-id="fdd23-816">For the complete list, refer to the SQL specification.</span></span>
  
     <span data-ttu-id="fdd23-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="fdd23-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="fdd23-818">Dize karşılaştırma ifadesi - bunlar bazı sabit dize değeri bir dize değeri karşılaştırma içerir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-818">String comparison expression - these include comparing a string value to some constant string value.</span></span>  
  
     <span data-ttu-id="fdd23-819">mother.familyName == "Smith";    child.givenName s; == bir dize değişkeni s'dir</span><span class="sxs-lookup"><span data-stu-id="fdd23-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="fdd23-820">Nesne/oluşturma ifadesi - dönüş Bu deyimler bileşik değer türü veya anonim tür bir nesneyi veya bir dizi tür nesneler dizisi.</span><span class="sxs-lookup"><span data-stu-id="fdd23-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="fdd23-821">Bu değerleri iç içe.</span><span class="sxs-lookup"><span data-stu-id="fdd23-821">These values can be nested.</span></span>
  
     <span data-ttu-id="fdd23-822">Yeni üst {familyName givenName "Smith" = "Can" =}; Yeni {ilk = 1, ikincisi 2 =}; iki alan sahip anonim bir tür</span><span class="sxs-lookup"><span data-stu-id="fdd23-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="fdd23-823">Yeni int [] {3, child.grade, 5};</span><span class="sxs-lookup"><span data-stu-id="fdd23-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="fdd23-824"><a id="SupportedLinqOperators"></a>Desteklenen LINQ işleçlerin listesi</span><span class="sxs-lookup"><span data-stu-id="fdd23-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="fdd23-825">DocumentDB .NET SDK'sıyla dahil LINQ Sağlayıcısı'nda desteklenen LINQ işleçlerin bir listesi aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-825">Here is a list of supported LINQ operators in the LINQ provider included with the DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="fdd23-826">**Seçin**: tahminleri Çevir SQL nesne oluşturması dahil olmak üzere SEÇMEK için</span><span class="sxs-lookup"><span data-stu-id="fdd23-826">**Select**: Projections translate to the SQL SELECT including object construction</span></span>
* <span data-ttu-id="fdd23-827">**Burada**: filtreleri SQL WHERE için çevirin ve Destek arasında çeviri & &, || ve!</span><span class="sxs-lookup"><span data-stu-id="fdd23-827">**Where**: Filters translate to the SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="fdd23-828">SQL işleçleri</span><span class="sxs-lookup"><span data-stu-id="fdd23-828">to the SQL operators</span></span>
* <span data-ttu-id="fdd23-829">**SelectMany**: SQL JOIN yan tümcesine dizi geriye doğru izleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-829">**SelectMany**: Allows unwinding of arrays to the SQL JOIN clause.</span></span> <span data-ttu-id="fdd23-830">Dizi öğeleri filtrelemek için ifadeleri zinciri/iç içe geçirme için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="fdd23-830">Can be used to chain/nest expressions to filter on array elements</span></span>
* <span data-ttu-id="fdd23-831">**OrderBy ve OrderByDescending**: ORDER BY artan/azalan şekilde çevirir</span><span class="sxs-lookup"><span data-stu-id="fdd23-831">**OrderBy and OrderByDescending**: Translates to ORDER BY ascending/descending</span></span>
* <span data-ttu-id="fdd23-832">**Count**, **toplam**, **Min**, **Max**, ve **ortalama** toplama ve zaman uyumsuz eşdeğerlerine işleçleri **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, ve **AverageAsync**.</span><span class="sxs-lookup"><span data-stu-id="fdd23-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="fdd23-833">**CompareTo**: aralık karşılaştırmaları çevirir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-833">**CompareTo**: Translates to range comparisons.</span></span> <span data-ttu-id="fdd23-834">.NET ile karşılaştırılabilir değilseniz bu yana dizeleri için yaygın olarak kullanılan</span><span class="sxs-lookup"><span data-stu-id="fdd23-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="fdd23-835">**Ele**: bir sorgunun sonuçlarına sınırlama SQL üstüne çevirir</span><span class="sxs-lookup"><span data-stu-id="fdd23-835">**Take**: Translates to the SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="fdd23-836">**Matematik işlevleri**: çevrilmesi destekler. NET'in Abs, Acos, Asin Cos tavan Atan, Exp, Floor, günlük, Log10, Pow, hepsini, oturum, Sin, Sqrt, Bronz, eşdeğer SQL yerleşik işlevler Truncate.</span><span class="sxs-lookup"><span data-stu-id="fdd23-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="fdd23-837">**Dize işlevleri**: çevrilmesi destekler. NET'in Concat, içerir, EndsWith, IndexOf, sayısı, ToLower, TrimStart, Değiştir, geriye doğru TrimEnd, StartsWith, SubString, eşdeğer SQL yerleşik işlevlere ToUpper.</span><span class="sxs-lookup"><span data-stu-id="fdd23-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="fdd23-838">**Dizi işlevleri**: çevrilmesi destekler. NET'in Concat içerir ve eşdeğer SQL yerleşik işlevlere sayısı.</span><span class="sxs-lookup"><span data-stu-id="fdd23-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="fdd23-839">**Jeo-uzamsal uzantı işlevleri**: saplama yöntemleri IsValid ve IsValidDetailed içinde uzaklığı çevrilecek eşdeğer SQL yerleşik işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="fdd23-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="fdd23-840">**Kullanıcı tanımlı işlev uzantı işlevi**: UserDefinedFunctionProvider.Invoke saplama yönteminden çeviri karşılık gelen kullanıcı tanımlı işlev için destekler.</span><span class="sxs-lookup"><span data-stu-id="fdd23-840">**User-Defined Function Extension Function**: Supports translation from the stub method UserDefinedFunctionProvider.Invoke to the corresponding user-defined function.</span></span>
* <span data-ttu-id="fdd23-841">**Çeşitli**: koşullu işleçler ve birleşim çevrilmesi destekler.</span><span class="sxs-lookup"><span data-stu-id="fdd23-841">**Miscellaneous**: Supports translation of the coalesce and conditional operators.</span></span> <span data-ttu-id="fdd23-842">Dize İÇERİYOR, ARRAY_CONTAINS veya bağlam bağlı olarak SQL IN içerir çevirebilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-842">Can translate Contains to String CONTAINS, ARRAY_CONTAINS, or the SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="fdd23-843">SQL sorgu işleçleri</span><span class="sxs-lookup"><span data-stu-id="fdd23-843">SQL query operators</span></span>
<span data-ttu-id="fdd23-844">Aşağıda, bazı standart LINQ Sorgu işleçleri Cosmos DB sorguları aşağıya doğru nasıl dönüştürüleceğini gösteren bazı örnekler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-844">Here are some examples that illustrate how some of the standard LINQ query operators are translated down to Cosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="fdd23-845">İşleç Seç</span><span class="sxs-lookup"><span data-stu-id="fdd23-845">Select Operator</span></span>
<span data-ttu-id="fdd23-846">Sözdizimi `input.Select(x => f(x))`, burada `f` skaler bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="fdd23-846">The syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="fdd23-847">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="fdd23-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="fdd23-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fdd23-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="fdd23-849">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="fdd23-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="fdd23-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fdd23-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="fdd23-851">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="fdd23-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="fdd23-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fdd23-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="fdd23-853">SelectMany işleci</span><span class="sxs-lookup"><span data-stu-id="fdd23-853">SelectMany operator</span></span>
<span data-ttu-id="fdd23-854">Sözdizimi `input.SelectMany(x => f(x))`, burada `f` koleksiyon türü döndüren bir skaler ifade.</span><span class="sxs-lookup"><span data-stu-id="fdd23-854">The syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="fdd23-855">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="fdd23-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="fdd23-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fdd23-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="fdd23-857">Burada işleci</span><span class="sxs-lookup"><span data-stu-id="fdd23-857">Where operator</span></span>
<span data-ttu-id="fdd23-858">Sözdizimi `input.Where(x => f(x))`, burada `f` bir Boole değeri döndürür skaler bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="fdd23-858">The syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="fdd23-859">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="fdd23-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="fdd23-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fdd23-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="fdd23-861">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="fdd23-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="fdd23-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fdd23-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="fdd23-863">Bileşik SQL sorguları</span><span class="sxs-lookup"><span data-stu-id="fdd23-863">Composite SQL queries</span></span>
<span data-ttu-id="fdd23-864">Daha güçlü sorgular oluşturmak için yukarıdaki işleçleri oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-864">The above operators can be composed to form more powerful queries.</span></span> <span data-ttu-id="fdd23-865">Cosmos DB iç içe geçmiş koleksiyonları desteklediğinden, birleşim birleştirilmiş iç içe geçmiş ya da.</span><span class="sxs-lookup"><span data-stu-id="fdd23-865">Since Cosmos DB supports nested collections, the composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="fdd23-866">Birleştirme</span><span class="sxs-lookup"><span data-stu-id="fdd23-866">Concatenation</span></span>
<span data-ttu-id="fdd23-867">Sözdizimi `input(.|.SelectMany())(.Select()|.Where())*`.</span><span class="sxs-lookup"><span data-stu-id="fdd23-867">The syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="fdd23-868">Birleştirilmiş bir sorgu ile isteğe bağlı başlatabilirsiniz `SelectMany` sorgu birden fazla ardından `Select` veya `Where` işleçler.</span><span class="sxs-lookup"><span data-stu-id="fdd23-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="fdd23-869">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="fdd23-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="fdd23-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fdd23-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="fdd23-871">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="fdd23-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="fdd23-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fdd23-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="fdd23-873">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="fdd23-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="fdd23-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fdd23-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="fdd23-875">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="fdd23-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="fdd23-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fdd23-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="fdd23-877">İç içe geçme</span><span class="sxs-lookup"><span data-stu-id="fdd23-877">Nesting</span></span>
<span data-ttu-id="fdd23-878">Sözdizimi `input.SelectMany(x=>x.Q())` Q olduğu bir `Select`, `SelectMany`, veya `Where` işleci.</span><span class="sxs-lookup"><span data-stu-id="fdd23-878">The syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="fdd23-879">İç içe bir sorgu iç sorgu dış toplama her öğesine uygulanır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-879">In a nested query, the inner query is applied to each element of the outer collection.</span></span> <span data-ttu-id="fdd23-880">İç sorgu gibi dış koleksiyondaki öğelerin alanlara başvurabilir önemli özelliklerinden biri otomatik olarak birleştirir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-880">One important feature is that the inner query can refer to the fields of the elements in the outer collection like self-joins.</span></span>

<span data-ttu-id="fdd23-881">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="fdd23-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="fdd23-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fdd23-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="fdd23-883">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="fdd23-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="fdd23-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fdd23-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="fdd23-885">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="fdd23-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="fdd23-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="fdd23-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="fdd23-887"><a id="ExecutingSqlQueries"></a>SQL sorguları yürütme</span><span class="sxs-lookup"><span data-stu-id="fdd23-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="fdd23-888">Cosmos DB herhangi bir dil tarafından HTTP/HTTPS istekleri çağrılabilir bir REST API'si aracılığıyla kaynaklarını kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="fdd23-889">Ayrıca, Cosmos DB .NET, Node.js, JavaScript ve Python gibi çeşitli popüler dilde programlama kitaplıkları sunar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="fdd23-890">Tüm REST API ve çeşitli kitaplıkları SQL sorgulama destekler.</span><span class="sxs-lookup"><span data-stu-id="fdd23-890">The REST API and the various libraries all support querying through SQL.</span></span> <span data-ttu-id="fdd23-891">.NET SDK'sı SQL yanı sıra sorgulama LINQ destekler.</span><span class="sxs-lookup"><span data-stu-id="fdd23-891">The .NET SDK supports LINQ querying in addition to SQL.</span></span>

<span data-ttu-id="fdd23-892">Aşağıdaki örnekler, bir sorgu oluşturun ve Cosmos DB veritabanı hesabı karşı göndermek üzere gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-892">The following examples show how to create a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="fdd23-893"><a id="RestAPI"></a>REST API'Sİ</span><span class="sxs-lookup"><span data-stu-id="fdd23-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="fdd23-894">Cosmos DB HTTP üzerinden açık bir RESTful programlama modeli sunar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="fdd23-895">Bir Azure aboneliği kullanarak veritabanı hesaplarını sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="fdd23-896">Cosmos DB kaynak modeli kaynaklar her biri mantıksal ve kararlı bir URI kullanılarak adreslenebilir bir veritabanı hesabı altında bir dizi oluşur.</span><span class="sxs-lookup"><span data-stu-id="fdd23-896">The Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="fdd23-897">Bir kaynak kümesi için bu belgede bir akış olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-897">A set of resources is referred to as a feed in this document.</span></span> <span data-ttu-id="fdd23-898">Veritabanı hesabı her birden çok koleksiyonu kapsayan bir veritabanları kümesi oluşur belgeleri, UDF'ler ve diğer kaynak türlerini her hangi içinde dönüş içerebilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="fdd23-899">Temel etkileşim bu kaynaklarla HTTP fiilleri GET, PUT, POST ve silme ile standart kullanıcıların yorumu modelidir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-899">The basic interaction model with these resources is through the HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="fdd23-900">POST fiil yeni bir kaynak oluşturulmasını, bir saklı yordamı yürütmek veya Cosmos DB sorgu verme için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-900">The POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="fdd23-901">Sorguları her zaman salt okunur hiçbir yan etkileri olan işlemleridir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="fdd23-902">Aşağıdaki örnekler, biz kadarki geçirdikten iki örnek belgeleri içeren bir koleksiyon karşı yapılan bir DocumentDB API sorgu için bir POST gösterir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-902">The following examples show a POST for a DocumentDB API query made against a collection containing the two sample documents we've reviewed so far.</span></span> <span data-ttu-id="fdd23-903">Sorgu basit bir filtre JSON name özelliğine göre sahiptir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-903">The query has a simple filter on the JSON name property.</span></span> <span data-ttu-id="fdd23-904">Kullanımına dikkat edin `x-ms-documentdb-isquery` ve Content-Type: `application/query+json` işlemi bir sorgu olduğunu belirtmek için üstbilgiler.</span><span class="sxs-lookup"><span data-stu-id="fdd23-904">Note the use of the `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers to denote that the operation is a query.</span></span>

<span data-ttu-id="fdd23-905">**İstek**</span><span class="sxs-lookup"><span data-stu-id="fdd23-905">**Request**</span></span>

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


<span data-ttu-id="fdd23-906">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-906">**Results**</span></span>

    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }


<span data-ttu-id="fdd23-907">İkinci örnek birleştirme sonucu birden çok sonuç döndüren daha karmaşık bir sorgu gösterir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-907">The second example shows a more complex query that returns multiple results from the join.</span></span>

<span data-ttu-id="fdd23-908">**İstek**</span><span class="sxs-lookup"><span data-stu-id="fdd23-908">**Request**</span></span>

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


<span data-ttu-id="fdd23-909">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="fdd23-909">**Results**</span></span>

    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }


<span data-ttu-id="fdd23-910">Bir sorgunun sonuçları sonuçlar tek sayfalık içinde sığamıyorsa sonra REST API aracılığıyla devamlılık belirteci döndürür `x-ms-continuation-token` yanıtı üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="fdd23-910">If a query's results cannot fit within a single page of results, then the REST API returns a continuation token through the `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="fdd23-911">İstemcileri sonraki sonuçlarında üstbilgi dahil olmak üzere sonuçları sayfalara bölme.</span><span class="sxs-lookup"><span data-stu-id="fdd23-911">Clients can paginate results by including the header in subsequent results.</span></span> <span data-ttu-id="fdd23-912">Sayfa başına sonuç sayısı da aracılığıyla denetlenebilir `x-ms-max-item-count` numara üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="fdd23-912">The number of results per page can also be controlled through the `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="fdd23-913">Belirtilen sorgu gibi bir toplama işlevi varsa `COUNT`, sorgu sayfası sonuçlar sayfası kısmen toplu değer döndürebilir sonra.</span><span class="sxs-lookup"><span data-stu-id="fdd23-913">If the specified query has an aggregation function like `COUNT`, then the query page may return a partially aggregated value over the page of results.</span></span> <span data-ttu-id="fdd23-914">İstemciler, son, örneğin sonuçlar, toplam sayı bu sayıyı dönmek için tek tek sayfaları döndürülen sayıları üzerinden toplamak için bu sonuçlar ikinci düzey toplama gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-914">The clients must perform a second-level aggregation over these results to produce the final results, for example, sum over the counts returned in the individual pages to return the total count.</span></span>

<span data-ttu-id="fdd23-915">Sorguları için veri tutarlılığı ilkelerini yönetmek için `x-ms-consistency-level` tüm REST API istekleri gibi üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="fdd23-915">To manage the data consistency policy for queries, use the `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="fdd23-916">Oturum tutarlılığı için de en son echo gerekli `x-ms-session-token` sorgu istekte tanımlama bilgisi üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="fdd23-916">For session consistency, it is required to also echo the latest `x-ms-session-token` Cookie header in the query request.</span></span> <span data-ttu-id="fdd23-917">Sorgulanan koleksiyonunun dizin oluşturma ilkesini de sorgu sonuçları tutarlılığını etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-917">The queried collection's indexing policy can also influence the consistency of query results.</span></span> <span data-ttu-id="fdd23-918">İle dizin oluşturma ilkesi ayarları varsayılan olarak koleksiyonlar için dizini her zaman ile belge içeriklerini geçerli ve sorgu sonuçları için veri seçilen tutarlılık eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="fdd23-918">With the default indexing policy settings, for collections the index is always current with the document contents and query results match the consistency chosen for data.</span></span> <span data-ttu-id="fdd23-919">Lazy için dizin oluşturma ilkesini rahat, sorgular eski sonuçlar döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-919">If the indexing policy is relaxed to Lazy, then queries can return stale results.</span></span> <span data-ttu-id="fdd23-920">Daha fazla bilgi için bkz: [Azure Cosmos DB tutarlılık düzeylerini][consistency-levels].</span><span class="sxs-lookup"><span data-stu-id="fdd23-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="fdd23-921">Koleksiyon için yapılandırılan dizin oluşturma ilkesini belirtilen sorgu destekleyemiyorsa, Azure Cosmos DB sunucusu 400 "hatalı istek" döndürür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-921">If the configured indexing policy on the collection cannot support the specified query, the Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="fdd23-922">Bu karma (eşitlik) aramaları için ve dizine almasını açıkça yolları için yapılandırılmış yolları aralığı sorguları için döndürülür.</span><span class="sxs-lookup"><span data-stu-id="fdd23-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="fdd23-923">`x-ms-documentdb-query-enable-scan` Başlığı, bir dizini olmadığında bir tarama gerçekleştirmek sorgu izin vermek için belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-923">The `x-ms-documentdb-query-enable-scan` header can be specified to allow the query to perform a scan when an index is not available.</span></span>

<span data-ttu-id="fdd23-924">Ayrıntılı ölçümler ayarlayarak sorgu yürütme elde edebilirsiniz `x-ms-documentdb-populatequerymetrics` başlığına `True`.</span><span class="sxs-lookup"><span data-stu-id="fdd23-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header to `True`.</span></span> <span data-ttu-id="fdd23-925">Daha fazla bilgi için bkz: [SQL sorgu ölçümleri Azure Cosmos DB DocumentDB API'si](documentdb-sql-query-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="fdd23-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="fdd23-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span><span class="sxs-lookup"><span data-stu-id="fdd23-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="fdd23-927">LINQ ve SQL .NET SDK'yı destekleyen sorgulama.</span><span class="sxs-lookup"><span data-stu-id="fdd23-927">The .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="fdd23-928">Aşağıdaki örnek, bu belgenin önceki bölümlerinde sunulan basit filtre sorgusu gerçekleştirmeye gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-928">The following example shows how to perform the simple filter query introduced earlier in this document.</span></span>

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


<span data-ttu-id="fdd23-929">Bu örnek her belge içinde eşitlik için iki özellik karşılaştırır ve anonim tahminleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


<span data-ttu-id="fdd23-930">Sonraki örnek LINQ SelectMany ifade birleştirmeler gösterir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-930">The next sample shows joins, expressed through LINQ SelectMany.</span></span>

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



<span data-ttu-id="fdd23-931">.NET istemci otomatik olarak yukarıda gösterildiği gibi foreach blokları sorgu sonuçlarında tüm sayfaları aracılığıyla yineler.</span><span class="sxs-lookup"><span data-stu-id="fdd23-931">The .NET client automatically iterates through all the pages of query results in the foreach blocks as shown above.</span></span> <span data-ttu-id="fdd23-932">REST API bölümünde sunulan sorgu seçeneklerini de .NET SDK kullanarak kullanılabilir `FeedOptions` ve `FeedResponse` CreateDocumentQuery yöntemi sınıflarda.</span><span class="sxs-lookup"><span data-stu-id="fdd23-932">The query options introduced in the REST API section are also available in the .NET SDK using the `FeedOptions` and `FeedResponse` classes in the CreateDocumentQuery method.</span></span> <span data-ttu-id="fdd23-933">Sayfa sayısı kullanılarak denetlenebilir `MaxItemCount` ayarı.</span><span class="sxs-lookup"><span data-stu-id="fdd23-933">The number of pages can be controlled using the `MaxItemCount` setting.</span></span> 

<span data-ttu-id="fdd23-934">Disk belleği oluşturarak açıkça kontrol edebilirsiniz `IDocumentQueryable` kullanarak `IQueryable` okuyarak ardından nesne` ResponseContinuationToken` değerleri ve bunları geçirme geri olarak `RequestContinuationToken` içinde `FeedOptions`.</span><span class="sxs-lookup"><span data-stu-id="fdd23-934">You can also explicitly control paging by creating `IDocumentQueryable` using the `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="fdd23-935">`EnableScanInQuery`Sorgu yapılandırılmış bir dizin oluşturma ilkesi tarafından desteklendiğinde taramaları etkinleştirmek için ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-935">`EnableScanInQuery` can be set to enable scans when the query cannot be supported by the configured indexing policy.</span></span> <span data-ttu-id="fdd23-936">Bölümlenmiş koleksiyonlar için kullandığınız `PartitionKey` karşı tek bir sorguyu çalıştırmak için bölüm (Cosmos DB otomatik olarak bu sorgu metni ayıklayabilirsiniz rağmen), ve `EnableCrossPartitionQuery` karşı birden çok bölüm çalıştırılması gereken sorguları çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="fdd23-936">For partitioned collections, you can use `PartitionKey` to run the query against a single partition (though Cosmos DB can automatically extract this from the query text), and `EnableCrossPartitionQuery` to run queries that may need to be run against multiple partitions.</span></span> 

<span data-ttu-id="fdd23-937">Başvurmak [Azure Cosmos DB .NET örnekleri](https://github.com/Azure/azure-documentdb-net) sorguları içeren daha fazla örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="fdd23-937">Refer to [Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="fdd23-938"><a id="JavaScriptServerSideApi"></a>JavaScript sunucu tarafı API</span><span class="sxs-lookup"><span data-stu-id="fdd23-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="fdd23-939">Cosmos DB JavaScript tabanlı uygulama mantığını saklı yordamları ve Tetikleyicileri kullanarak doğrudan koleksiyonlar üzerinde yürütmek için bir programlama modeli sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdd23-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections using stored procedures and triggers.</span></span> <span data-ttu-id="fdd23-940">Bir koleksiyon düzeyinde kayıtlı JavaScript mantığı sonra verilen koleksiyon belgelerde işlemlerini veritabanı işlemlerini verebilir.</span><span class="sxs-lookup"><span data-stu-id="fdd23-940">The JavaScript logic registered at a collection level can then issue database operations on the operations on the documents of the given collection.</span></span> <span data-ttu-id="fdd23-941">Bu işlemler çevresel ACID işlemlerini sarılır.</span><span class="sxs-lookup"><span data-stu-id="fdd23-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="fdd23-942">Aşağıdaki örnek queryDocuments JavaScript Sunucusu API sorgularından yapmak için nasıl kullanılacağını gösterir iç saklı yordamları ve Tetikleyicileri.</span><span class="sxs-lookup"><span data-stu-id="fdd23-942">The following example shows how to use the queryDocuments in the JavaScript server API to make queries from inside stored procedures and triggers.</span></span>

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace the author name for all documents that satisfied the query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need to execute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <span data-ttu-id="fdd23-943"><a id="References"></a>Başvuruları</span><span class="sxs-lookup"><span data-stu-id="fdd23-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="fdd23-944">[Azure Cosmos DB giriş][introduction]</span><span class="sxs-lookup"><span data-stu-id="fdd23-944">[Introduction to Azure Cosmos DB][introduction]</span></span>
2. [<span data-ttu-id="fdd23-945">Azure Cosmos veritabanı SQL belirtimi</span><span class="sxs-lookup"><span data-stu-id="fdd23-945">Azure Cosmos DB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="fdd23-946">Azure Cosmos DB .NET örnekleri</span><span class="sxs-lookup"><span data-stu-id="fdd23-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="fdd23-947">[Azure Cosmos DB tutarlılık düzeyleri][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="fdd23-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="fdd23-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="fdd23-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="fdd23-949">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="fdd23-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="fdd23-950">JavaScript belirtimi [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="fdd23-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="fdd23-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="fdd23-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="fdd23-952">Sorgu büyük veritabanları için değerlendirme teknikleri [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="fdd23-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="fdd23-953">Sorgu 1994 paralel ilişkisel veritabanı sistemleri, IEEE bilgisayar topluluğu basın, işleme</span><span class="sxs-lookup"><span data-stu-id="fdd23-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="fdd23-954">Lu, Ooi, Bronz, sorgu 1994 paralel ilişkisel veritabanı sistemleri, IEEE bilgisayar topluluğu basın, işleme.</span><span class="sxs-lookup"><span data-stu-id="fdd23-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="fdd23-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Barış Tomkins: Pig Latin: veri işleme, SIGMOD 2008 için Not şekilde yabancı dil.</span><span class="sxs-lookup"><span data-stu-id="fdd23-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="fdd23-956">G.</span><span class="sxs-lookup"><span data-stu-id="fdd23-956">G.</span></span> <span data-ttu-id="fdd23-957">Graefe.</span><span class="sxs-lookup"><span data-stu-id="fdd23-957">Graefe.</span></span> <span data-ttu-id="fdd23-958">Sorgu iyileştirme için basamaklar çerçevesi.</span><span class="sxs-lookup"><span data-stu-id="fdd23-958">The Cascades framework for query optimization.</span></span> <span data-ttu-id="fdd23-959">IEEE veri Müh</span><span class="sxs-lookup"><span data-stu-id="fdd23-959">IEEE Data Eng.</span></span> <span data-ttu-id="fdd23-960">Bull., 18(3): 1995.</span><span class="sxs-lookup"><span data-stu-id="fdd23-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md