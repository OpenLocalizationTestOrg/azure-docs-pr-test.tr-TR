---
title: "Azure Cosmos DB DocumentDB API aaaSQL sorgularında | Microsoft Docs"
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
ms.openlocfilehash: f4db95b87f5796c4e4299aaf016435cb6301bbfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="8b908-105">SQL sorguları Azure Cosmos DB DocumentDB API'si</span><span class="sxs-lookup"><span data-stu-id="8b908-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="8b908-106">Microsoft Azure Cosmos DB bir JSON sorgu dili SQL (yapılandırılmış sorgu dili) kullanarak belgelerin sorgulanmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="8b908-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="8b908-107">Cosmos DB gerçekten şemasız.</span><span class="sxs-lookup"><span data-stu-id="8b908-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="8b908-108">Kendi taahhüt toohello JSON veri modeli, doğrudan hello veritabanı altyapısı içinde otomatik JSON belgelerinin dizinini gerektirmeden açık şema veya ikincil dizinlerin oluşturulmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b908-108">By virtue of its commitment toohello JSON data model directly within hello database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="8b908-109">Cosmos DB Hello sorgu dili tasarlarken size iki hedefleri düşünerek vardı:</span><span class="sxs-lookup"><span data-stu-id="8b908-109">While designing hello query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="8b908-110">Yeni bir JSON sorgu dili inventing yerine, biz toosupport SQL istedik.</span><span class="sxs-lookup"><span data-stu-id="8b908-110">Instead of inventing a new JSON query language, we wanted toosupport SQL.</span></span> <span data-ttu-id="8b908-111">SQL hello en tanıdık ve popüler sorgu dilleri biridir.</span><span class="sxs-lookup"><span data-stu-id="8b908-111">SQL is one of hello most familiar and popular query languages.</span></span> <span data-ttu-id="8b908-112">Cosmos veritabanı SQL, JSON belgelerini zengin sorgular için resmi bir programlama modeli sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b908-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="8b908-113">Bir JSON belgesi veritabanı JavaScript doğrudan hello Veritabanı Altyapısı'nda yürütülebilir, biz toouse JavaScript'in programlama modeli hello temel olarak bizim sorgu dili için istedik.</span><span class="sxs-lookup"><span data-stu-id="8b908-113">As a JSON document database capable of executing JavaScript directly in hello database engine, we wanted toouse JavaScript's programming model as hello foundation for our query language.</span></span> <span data-ttu-id="8b908-114">Merhaba DocumentDB API SQL JavaScript'in tür sistemi, ifade değerlendirmesi ve işlev çağrısını kökü belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="8b908-114">hello DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="8b908-115">Bu içinde dönüş JSON belgeleri, kendi kendine birleşimler, uzamsal sorguları ve kullanıcı tanımlı işlevler (UDF'ler) diğer özellikler arasında JavaScript tamamen yazılmış çalıştırılışı arasında ilişkisel projeksiyonları, hiyerarşik gezinti için doğal bir programlama modeli sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b908-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="8b908-116">Bu özellikler anahtar tooreducing hello uyuşmazlık Merhaba uygulaması ile Merhaba veritabanı arasında ve geliştirici üretkenliği için önemli olduğundan inanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="8b908-116">We believe that these capabilities are key tooreducing hello friction between hello application and hello database and are crucial for developer productivity.</span></span>

<span data-ttu-id="8b908-117">Burada Aravind Ramachandran Cosmos veritabanı sorgulama özelliklerini gösterir, video, aşağıdaki hello izlemeye ve ziyaret tarafından Başlarken öneririz bizim [Query Playground](http://www.documentdb.com/sql/demo), burada Cosmos DB deneyin ve SQL sorguları çalıştırma Veri kümemizde.</span><span class="sxs-lookup"><span data-stu-id="8b908-117">We recommend getting started by watching hello following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="8b908-118">Ardından, burada size bazı basit JSON belgeleri ve SQL komutları anlatan bir SQL sorgusu öğretici başlayın toothis makale döndür.</span><span class="sxs-lookup"><span data-stu-id="8b908-118">Then, return toothis article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="8b908-119"><a id="GettingStarted"></a>Cosmos DB SQL komutları ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="8b908-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="8b908-120">toosee Cosmos DB SQL adresindeki iş, şimdi birkaç basit JSON belgeleri ile başlar ve bazı basit sorgular size yol.</span><span class="sxs-lookup"><span data-stu-id="8b908-120">toosee Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="8b908-121">Bu iki JSON belgeleri iki ailesi hakkında göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="8b908-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="8b908-122">Cosmos DB ile biz toocreate herhangi bir şemaları ya da ikincil dizinlerin açıkça gerekmez.</span><span class="sxs-lookup"><span data-stu-id="8b908-122">With Cosmos DB, we do not need toocreate any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="8b908-123">Biz tooinsert hello JSON belgeleri tooa Cosmos DB koleksiyonu yeterlidir ve daha sonra sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b908-123">We simply need tooinsert hello JSON documents tooa Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="8b908-124">Basit bir JSON burada sahibiz belge hello Andersen ailesi, hello üst, alt öğelerini (ve bunların Evcil Hayvanlar), adresinizi ve kayıt bilgileri.</span><span class="sxs-lookup"><span data-stu-id="8b908-124">Here we have a simple JSON document for hello Andersen family, hello parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="8b908-125">Merhaba belge dizeler, sayılar, Boole değerlerini, dizileri ve iç içe özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="8b908-125">hello document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="8b908-126">**Belge**</span><span class="sxs-lookup"><span data-stu-id="8b908-126">**Document**</span></span>  

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

<span data-ttu-id="8b908-127">Bir fark – sahip ikinci bir belge işte `givenName` ve `familyName` yerine kullanılan `firstName` ve `lastName`.</span><span class="sxs-lookup"><span data-stu-id="8b908-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="8b908-128">**Belge**</span><span class="sxs-lookup"><span data-stu-id="8b908-128">**Document**</span></span>  

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

<span data-ttu-id="8b908-129">Şimdi birkaç sorgu deneyelim bu veri toounderstand karşı hello bazıları DocumentDB API SQL yönlerini anahtar.</span><span class="sxs-lookup"><span data-stu-id="8b908-129">Now let's try a few queries against this data toounderstand some of hello key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="8b908-130">Örneğin, hello aşağıdaki hello Kimliği alanı eşleştiği döndürür hello belgeleri sorgu `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="8b908-130">For example, hello following query returns hello documents where hello id field matches `AndersenFamily`.</span></span> <span data-ttu-id="8b908-131">Olduğundan bir `SELECT *`, hello hello sorgu çıkışıdır hello tam JSON belgesi:</span><span class="sxs-lookup"><span data-stu-id="8b908-131">Since it's a `SELECT *`, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="8b908-132">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="8b908-133">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-133">**Results**</span></span>

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


<span data-ttu-id="8b908-134">Şimdi tooreformat hello farklı bir şekli JSON çıkışında burada ihtiyacımız hello durumu göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="8b908-134">Now consider hello case where we need tooreformat hello JSON output in a different shape.</span></span> <span data-ttu-id="8b908-135">Bu sorgu Hello Adres Şehir hello durumu olarak aynı ad hello olduğunda iki seçili alanları ile adı ve şehir projeleri yeni bir JSON nesnesi.</span><span class="sxs-lookup"><span data-stu-id="8b908-135">This query projects a new JSON object with two selected fields, Name and City, when hello address' city has hello same name as hello state.</span></span> <span data-ttu-id="8b908-136">Bu durumda, "NY, NY" eşleşir.</span><span class="sxs-lookup"><span data-stu-id="8b908-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="8b908-137">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="8b908-138">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="8b908-139">Merhaba sonraki sorgunun döndürdüğü tüm hello verilen adları alt kimliğine eşleşen hello ailesinde `WakefieldFamily` hello Şehir ikamet ettiğiniz sıralanan.</span><span class="sxs-lookup"><span data-stu-id="8b908-139">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by hello city of residence.</span></span>

<span data-ttu-id="8b908-140">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="8b908-141">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="8b908-142">Merhaba Cosmos DB birkaç önemli yönleri sorgu dili kadarki gördük hello örnekler üzerinden toodraw dikkat tooa isteriz:</span><span class="sxs-lookup"><span data-stu-id="8b908-142">We would like toodraw attention tooa few noteworthy aspects of hello Cosmos DB query language through hello examples we've seen so far:</span></span>  

* <span data-ttu-id="8b908-143">DocumentDB API SQL JSON değerler üzerinde çalışır olduğundan, satır ve sütunların yerine varlıklar şeklinde ağaç ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="8b908-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="8b908-144">Bu nedenle, hello dili, herhangi bir rastgele derinliğe hello ağacını toonodes gibi bakın sağlar `Node1.Node2.Node3…..Nodem`, benzer toorelational SQL başvuran toohello iki bölümü başvurusu `<table>.<column>`.</span><span class="sxs-lookup"><span data-stu-id="8b908-144">Therefore, hello language lets you refer toonodes of hello tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar toorelational SQL referring toohello two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="8b908-145">Merhaba sorgu dili works şema daha az veri ile yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="8b908-145">hello structured query language works with schema-less data.</span></span> <span data-ttu-id="8b908-146">Bu nedenle, hello türü sistem gereksinimlerini toobe bağlı dinamik olarak.</span><span class="sxs-lookup"><span data-stu-id="8b908-146">Therefore, hello type system needs toobe bound dynamically.</span></span> <span data-ttu-id="8b908-147">Merhaba aynı ifade farklı belgelere farklı türlerde üretebilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-147">hello same expression could yield different types on different documents.</span></span> <span data-ttu-id="8b908-148">bir sorgunun sonucu Hello geçerli bir JSON değer olmakla birlikte, sabit bir şema toobe garanti edilmez.</span><span class="sxs-lookup"><span data-stu-id="8b908-148">hello result of a query is a valid JSON value, but is not guaranteed toobe of a fixed schema.</span></span>  
* <span data-ttu-id="8b908-149">Cosmos DB yalnızca Katı JSON belgelerini destekler.</span><span class="sxs-lookup"><span data-stu-id="8b908-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="8b908-150">Bu, yalnızca JSON türleriyle sınırlı toodeal hello tür sistemi ve ifadeler olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8b908-150">This means hello type system and expressions are restricted toodeal only with JSON types.</span></span> <span data-ttu-id="8b908-151">Toohello başvuran [JSON belirtimi](http://www.json.org/) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="8b908-151">Refer toohello [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="8b908-152">Cosmos DB koleksiyon JSON belgeleri, şemasız bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="8b908-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="8b908-153">Merhaba ilişkileri veri varlıklarında içinde ve bir koleksiyondaki belgeler arasında örtük olarak kapsama ve birincil anahtar ve yabancı anahtar ilişkileri tarafından yakalanır.</span><span class="sxs-lookup"><span data-stu-id="8b908-153">hello relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="8b908-154">Bu makalenin sonraki bölümlerinde ele alınan hello içi belge birleştirmeler etkinliğinin düzenleyicileri gösteren değer önemli bir yönü budur.</span><span class="sxs-lookup"><span data-stu-id="8b908-154">This is an important aspect worth pointing out in light of hello intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="8b908-155"><a id="Indexing"></a>Cosmos DB dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="8b908-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="8b908-156">Biz DocumentDB API SQL söz dizimi hello ulaşmadan Cosmos DB tasarımında dizin hello incelenmesi yararlı olan.</span><span class="sxs-lookup"><span data-stu-id="8b908-156">Before we get into hello DocumentDB API SQL syntax, it is worth exploring hello indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="8b908-157">Veritabanı dizinlerini Hello amacı, iyi performans ve düşük gecikme süresi sağlarken kendi çeşitli formlar ve şekiller (örneğin, CPU ve giriş/çıkış) en düşük kaynak kullanımına sahip tooserve sorguları budur.</span><span class="sxs-lookup"><span data-stu-id="8b908-157">hello purpose of database indexes is tooserve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="8b908-158">Genellikle, bir veritabanını sorgulamak için doğru dizin hello hello seçimine kadar planlama ve deneme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8b908-158">Often, hello choice of hello right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="8b908-159">Bu yaklaşım, burada hello veri tooa kesin şema uygun değil ve hızlı bir şekilde dönüşmesi şema daha az veritabanları için bir zorluk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8b908-159">This approach poses a challenge for schema-less databases where hello data doesn’t conform tooa strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="8b908-160">Bu nedenle, biz hello Cosmos DB dizin alt sistemi tasarlarken, biz hedeflerini izleyerek hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="8b908-160">Therefore, when we designed hello Cosmos DB indexing subsystem, we set hello following goals:</span></span>

* <span data-ttu-id="8b908-161">Dizin belgeleri şema gerek kalmadan: alt dizin hello herhangi bir şema bilgi gerektirmez veya şeması hakkında tüm varsayımlarda hello belgelerin.</span><span class="sxs-lookup"><span data-stu-id="8b908-161">Index documents without requiring schema: hello indexing subsystem does not require any schema information or make any assumptions about schema of hello documents.</span></span> 
* <span data-ttu-id="8b908-162">Verimli, zengin hiyerarşik ve ilişkisel sorguları için destek: hello dizinini destekleyen hello Cosmos DB sorgu dili verimli bir şekilde, hiyerarşik ve ilişkisel tahminleri desteği dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="8b908-162">Support for efficient, rich hierarchical, and relational queries: hello index supports hello Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="8b908-163">Yazma sürekli bir birim in face of tutarlı sorgular için destek: yüksek yazma işleme iş yükleri için tutarlı sorgularla hello dizin artımlı olarak, verimli ve çevrimiçi yazma sürekli bir birimin hello karşılaştıkları güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, hello index is updated incrementally, efficiently, and online in hello face of a sustained volume of writes.</span></span> <span data-ttu-id="8b908-164">önemli tooserve hello sorguları hangi hello yapılandırılan kullanıcı hello belge hizmetindeki hello tutarlılık düzeyinde Hello tutarlı dizin güncelleştirmesidir.</span><span class="sxs-lookup"><span data-stu-id="8b908-164">hello consistent index update is crucial tooserve hello queries at hello consistency level in which hello user configured hello document service.</span></span>
* <span data-ttu-id="8b908-165">Çoklu kiracı için destek: hello ayırmaya dayalı modeli için kaynak İdaresi kiracılar arasında verildiğinde, dizin güncelleştirmeleri hello bütçe çoğaltma ayrılan sistem kaynaklarını (İşlemci, bellek ve saniye başına girdi/çıktı işlemleri) içinde gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-165">Support for multi-tenancy: Given hello reservation-based model for resource governance across tenants, index updates are performed within hello budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="8b908-166">Depolama verimliliği: maliyet verimliliği için hello disk üzerinde depolama ek yükü hello dizinin sınırlanmış ve tahmin edilebilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-166">Storage efficiency: For cost effectiveness, hello on-disk storage overhead of hello index is bounded and predictable.</span></span> <span data-ttu-id="8b908-167">Cosmos DB maliyet tabanlı Geliştirici toomake bileşim dizin yükü ilişkisi toohello sorgu performansı arasında hello sağladığından, bu önemlidir.</span><span class="sxs-lookup"><span data-stu-id="8b908-167">This is crucial because Cosmos DB allows hello developer toomake cost-based tradeoffs between index overhead in relation toohello query performance.</span></span>  

<span data-ttu-id="8b908-168">Toohello başvuran [Azure Cosmos DB örnekleri](https://github.com/Azure/azure-documentdb-net) nasıl tooconfigure hello bir koleksiyon için dizin oluşturma ilkesini gösteren örnekler için MSDN'de.</span><span class="sxs-lookup"><span data-stu-id="8b908-168">Refer toohello [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how tooconfigure hello indexing policy for a collection.</span></span> <span data-ttu-id="8b908-169">Şimdi şimdi hello Azure Cosmos DB SQL söz dizimi hello ayrıntılarını alın.</span><span class="sxs-lookup"><span data-stu-id="8b908-169">Let’s now get into hello details of hello Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="8b908-170"><a id="Basics"></a>Bir Azure Cosmos DB SQL sorgusu temelleri</span><span class="sxs-lookup"><span data-stu-id="8b908-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="8b908-171">Her sorgu, bir SELECT yan tümcesi ve isteğe bağlı FROM oluşur ve WHERE yan tümcelerini ANSI SQL standartları başına.</span><span class="sxs-lookup"><span data-stu-id="8b908-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="8b908-172">Genellikle, her sorgu için hello kaynak hello FROM yan tümcesinde numaralandırılır.</span><span class="sxs-lookup"><span data-stu-id="8b908-172">Typically, for each query, hello source in hello FROM clause is enumerated.</span></span> <span data-ttu-id="8b908-173">Daha sonra hello filtre hello WHERE yan tümcesi hello kaynak tooretrieve üzerinde uygulanır, JSON belgelerini bir kısmı.</span><span class="sxs-lookup"><span data-stu-id="8b908-173">Then hello filter in hello WHERE clause is applied on hello source tooretrieve a subset of JSON documents.</span></span> <span data-ttu-id="8b908-174">Son olarak, hello SELECT yan tümcesinde kullanılan tooproject hello istenen hello JSON değerleri listesi seçin.</span><span class="sxs-lookup"><span data-stu-id="8b908-174">Finally, hello SELECT clause is used tooproject hello requested JSON values in hello select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="8b908-175"><a id="FromClause"></a>FROM yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="8b908-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="8b908-176">Merhaba `FROM <from_specification>` hello kaynak filtre ya da daha sonra hello sorguda öngörülen sürece yan tümcesi isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8b908-176">hello `FROM <from_specification>` clause is optional unless hello source is filtered or projected later in hello query.</span></span> <span data-ttu-id="8b908-177">Bu yan tümce Hello amacı hangi hello sorgu çalışmalıdır toospecify hello veri kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="8b908-177">hello purpose of this clause is toospecify hello data source upon which hello query must operate.</span></span> <span data-ttu-id="8b908-178">Yaygın olarak hello tüm koleksiyon hello kaynağıdır, ancak bir hello koleksiyonunun bir alt bunun yerine belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b908-178">Commonly hello whole collection is hello source, but one can specify a subset of hello collection instead.</span></span> 

<span data-ttu-id="8b908-179">Bir sorgu ister `SELECT * FROM Families` hello tüm aileleri koleksiyon hangi tooenumerate hello kaynak olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="8b908-179">A query like `SELECT * FROM Families` indicates that hello entire Families collection is hello source over which tooenumerate.</span></span> <span data-ttu-id="8b908-180">Özel bir tanımlayıcısı kök hello koleksiyon adı kullanmak yerine kullanılan toorepresent hello koleksiyonu olabilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-180">A special identifier ROOT can be used toorepresent hello collection instead of using hello collection name.</span></span> <span data-ttu-id="8b908-181">Merhaba aşağıdaki listede sorgu zorlanan hello kurallarını içerir:</span><span class="sxs-lookup"><span data-stu-id="8b908-181">hello following list contains hello rules that are enforced per query:</span></span>

* <span data-ttu-id="8b908-182">Merhaba koleksiyonu olabilir, diğer gibi `SELECT f.id FROM Families AS f` ya da yalnızca `SELECT f.id FROM Families f`.</span><span class="sxs-lookup"><span data-stu-id="8b908-182">hello collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="8b908-183">Burada `f` hello eşdeğerdir `Families`.</span><span class="sxs-lookup"><span data-stu-id="8b908-183">Here `f` is hello equivalent of `Families`.</span></span> <span data-ttu-id="8b908-184">`AS`optional anahtar sözcüğü tooalias hello tanımlayıcısı değil.</span><span class="sxs-lookup"><span data-stu-id="8b908-184">`AS` is an optional keyword tooalias hello identifier.</span></span>
* <span data-ttu-id="8b908-185">Bir kez diğer hello özgün kaynak bağlanamaz.</span><span class="sxs-lookup"><span data-stu-id="8b908-185">Once aliased, hello original source cannot be bound.</span></span> <span data-ttu-id="8b908-186">Örneğin, `SELECT Families.id FROM Families f` hello tanımlayıcı "Aileleri" artık çözümlenemiyor beri sözdizimsel olarak geçersiz.</span><span class="sxs-lookup"><span data-stu-id="8b908-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since hello identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="8b908-187">Başvurulan toobe gereken tüm özellikleri tam olarak nitelenmiş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b908-187">All properties that need toobe referenced must be fully qualified.</span></span> <span data-ttu-id="8b908-188">Merhaba kesin şema bağlılığı durumunda, bu zorlanan tooavoid bildirilmesidir belirsiz hiçbir bağlama.</span><span class="sxs-lookup"><span data-stu-id="8b908-188">In hello absence of strict schema adherence, this is enforced tooavoid any ambiguous bindings.</span></span> <span data-ttu-id="8b908-189">Bu nedenle, `SELECT id FROM Families f` hello özelliği bu yana sözdizimsel olarak geçersiz `id` bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="8b908-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since hello property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="8b908-190">Alt belgeleri</span><span class="sxs-lookup"><span data-stu-id="8b908-190">Subdocuments</span></span>
<span data-ttu-id="8b908-191">Merhaba kaynağı azaltılmış tooa daha küçük alt de olabilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-191">hello source can also be reduced tooa smaller subset.</span></span> <span data-ttu-id="8b908-192">Örneği için yalnızca bir alt ağacı her belgedeki tooenumerating hello subroot sonra hello kaynak hello aşağıdaki örnekte gösterildiği gibi hale gelebilir:</span><span class="sxs-lookup"><span data-stu-id="8b908-192">For instance, tooenumerating only a subtree in each document, hello subroot could then become hello source, as shown in hello following example:</span></span>

<span data-ttu-id="8b908-193">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="8b908-194">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-194">**Results**</span></span>  

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

<span data-ttu-id="8b908-195">Yukarıdaki örnek Hello hello kaynağı olarak bir dizi kullanılan olsa da, bir nesne de aşağıdaki örneğine hello gösterilen olduğu hello kaynağı olarak kullanılabilir: hello kaynağında bulunan (tanımsız değil) tüm geçerli JSON değer hello sonucunu eklenmek üzere olarak kabul edilir Merhaba sorgu.</span><span class="sxs-lookup"><span data-stu-id="8b908-195">While hello above example used an array as hello source, an object could also be used as hello source, which is what's shown in hello following example: Any valid JSON value (not undefined) that can be found in hello source is considered for inclusion in hello result of hello query.</span></span> <span data-ttu-id="8b908-196">Bazı aileleri yoksa bir `address.state` değeri hello sorgu sonucu hariç tutulur.</span><span class="sxs-lookup"><span data-stu-id="8b908-196">If some families don’t have an `address.state` value, they are excluded in hello query result.</span></span>

<span data-ttu-id="8b908-197">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="8b908-198">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="8b908-199"><a id="WhereClause"></a>WHERE yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="8b908-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="8b908-200">WHERE yan tümcesi hello (**`WHERE <filter_condition>`**) isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8b908-200">hello WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="8b908-201">Merhaba hello kaynağı tarafından sağlanan hello JSON belgelerini hello sonuç bir parçası olarak dahil edilen sipariş toobe getirmelidir koşulları belirtir.</span><span class="sxs-lookup"><span data-stu-id="8b908-201">It specifies hello condition(s) that hello JSON documents provided by hello source must satisfy in order toobe included as part of hello result.</span></span> <span data-ttu-id="8b908-202">Herhangi bir JSON belge değerlendirilmelidir hello belirtilen koşullar çok "true" Merhaba sonucu olarak kabul toobe.</span><span class="sxs-lookup"><span data-stu-id="8b908-202">Any JSON document must evaluate hello specified conditions too"true" toobe considered for hello result.</span></span> <span data-ttu-id="8b908-203">Merhaba yan tümcesi hello dizin katmanı sipariş toodetermine hello mutlak en küçük alt kümesini hello sonuç parçası olabilir kaynak belgeleri'tarafından kullanıldığı.</span><span class="sxs-lookup"><span data-stu-id="8b908-203">hello WHERE clause is used by hello index layer in order toodetermine hello absolute smallest subset of source documents that can be part of hello result.</span></span> 

<span data-ttu-id="8b908-204">Merhaba aşağıdaki sorguyu istekleri, değeri olan bir ad özelliği içeren belgeleri `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="8b908-204">hello following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="8b908-205">Name özelliği olmayan herhangi bir belge veya burada hello değeri eşleşmiyor `AndersenFamily` dışlandı.</span><span class="sxs-lookup"><span data-stu-id="8b908-205">Any other document that does not have a name property, or where hello value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="8b908-206">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="8b908-207">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="8b908-208">Merhaba önceki örnekte basit eşitlik sorgu gösterdi.</span><span class="sxs-lookup"><span data-stu-id="8b908-208">hello previous example showed a simple equality query.</span></span> <span data-ttu-id="8b908-209">DocumentDB API SQL skaler ifadelerin çeşitli de destekler.</span><span class="sxs-lookup"><span data-stu-id="8b908-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="8b908-210">İkili ve birli ifadeleri en yaygın olarak kullanılan hello var.</span><span class="sxs-lookup"><span data-stu-id="8b908-210">hello most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="8b908-211">Özellik başvuruları hello kaynak JSON nesnesinden de geçerli ifadeler oluyor.</span><span class="sxs-lookup"><span data-stu-id="8b908-211">Property references from hello source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="8b908-212">ikili işleçler aşağıdaki hello şu anda desteklenen ve örnek hello gösterildiği gibi sorgularında kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="8b908-212">hello following binary operators are currently supported and can be used in queries as shown in hello following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="8b908-213">Aritmetik</span><span class="sxs-lookup"><span data-stu-id="8b908-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="8b908-214">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="8b908-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8b908-215">Bit düzeyinde</span><span class="sxs-lookup"><span data-stu-id="8b908-215">Bitwise</span></span></td>    
<td><span data-ttu-id="8b908-216">|, &, ^, <<>>,, >>> (sıfır dolgu sağa kaydırma)</span><span class="sxs-lookup"><span data-stu-id="8b908-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8b908-217">Mantıksal</span><span class="sxs-lookup"><span data-stu-id="8b908-217">Logical</span></span></td>
<td><span data-ttu-id="8b908-218">VE VEYA DEĞİL</span><span class="sxs-lookup"><span data-stu-id="8b908-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8b908-219">Karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="8b908-219">Comparison</span></span></td>    
<td><span data-ttu-id="8b908-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="8b908-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8b908-221">Dize</span><span class="sxs-lookup"><span data-stu-id="8b908-221">String</span></span></td>    
<td><span data-ttu-id="8b908-222">|| (birleştirme)</span><span class="sxs-lookup"><span data-stu-id="8b908-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="8b908-223">İkili işleçler kullanarak bazı sorguları bir göz atalım.</span><span class="sxs-lookup"><span data-stu-id="8b908-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="8b908-224">birli işleçleri hello +,-, ~ değil de desteklenir ve sorgular içinde hello aşağıdaki örnekte gösterildiği gibi kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="8b908-224">hello unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in hello following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="8b908-225">Ayrıca toobinary ve birli işleçleri özelliği başvuruları de izin verilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-225">In addition toobinary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="8b908-226">Örneğin, `SELECT * FROM Families f WHERE f.isRegistered` döndürür hello hello özelliği içeren JSON belgesi `isRegistered` hello özellik değerine eşit toohello JSON olduğu `true` değeri.</span><span class="sxs-lookup"><span data-stu-id="8b908-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns hello JSON document containing hello property `isRegistered` where hello property's value is equal toohello JSON `true` value.</span></span> <span data-ttu-id="8b908-227">Diğer tüm değerler (false, null, tanımlanmamış, `<number>`, `<string>`, `<object>`, `<array>`, vs.) toohello kaynak belge hello sonucundan dışlanan yol açar.</span><span class="sxs-lookup"><span data-stu-id="8b908-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads toohello source document being excluded from hello result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="8b908-228">Eşitlik ve Karşılaştırma işleçleri</span><span class="sxs-lookup"><span data-stu-id="8b908-228">Equality and comparison operators</span></span>
<span data-ttu-id="8b908-229">Merhaba aşağıdaki tabloda eşitlik karşılaştırmaları hello sonucunu DocumentDB API SQL'de herhangi iki JSON türleri arasında gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8b908-229">hello following table shows hello result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="8b908-230">
            <strong>OP</strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="8b908-231">
            <strong>Tanımlanmamış</strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="8b908-232">
            <strong>Null</strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="8b908-233">
            <strong>Boole değeri</strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="8b908-234">
            <strong>Sayı</strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="8b908-235">
            <strong>Dize</strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="8b908-236">
            <strong>Nesne</strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="8b908-237">
            <strong>Dizi</strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="8b908-238">
            <strong>Tanımlanmamış<strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="8b908-239">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-240">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-241">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-242">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-243">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-244">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-245">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="8b908-246">
            <strong>Null<strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="8b908-247">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="8b908-248">
            <strong>TAMAM</strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="8b908-249">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-250">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-251">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-252">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-253">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="8b908-254">
            <strong>Boole değeri<strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="8b908-255">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-256">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="8b908-257">
            <strong>TAMAM</strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="8b908-258">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-259">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-260">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-261">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="8b908-262">
            <strong>Sayı<strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="8b908-263">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-264">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-265">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="8b908-266">
            <strong>TAMAM</strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="8b908-267">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-268">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-269">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="8b908-270">
            <strong>Dize<strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="8b908-271">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-272">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-273">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-274">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="8b908-275">
            <strong>TAMAM</strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="8b908-276">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-277">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="8b908-278">
            <strong>Nesne<strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="8b908-279">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-280">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-281">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-282">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-283">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="8b908-284">
            <strong>TAMAM</strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="8b908-285">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="8b908-286">
            <strong>Dizi<strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="8b908-287">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-288">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-289">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-290">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-291">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="8b908-292">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="8b908-293">
            <strong>TAMAM</strong>
         </span><span class="sxs-lookup"><span data-stu-id="8b908-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="8b908-294">Gibi diğer Karşılaştırma işleçleri için >, > =,! =, < ve <, hello = aşağıdaki kurallar geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="8b908-294">For other comparison operators such as >, >=, !=, < and <=, hello following rules apply:</span></span>   

* <span data-ttu-id="8b908-295">Karşılaştırma türü üzerinden içinde tanımlanmamış sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="8b908-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="8b908-296">İki nesne veya iki arasında karşılaştırma tanımlanmamış sonuçlarında dizi.</span><span class="sxs-lookup"><span data-stu-id="8b908-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="8b908-297">Merhaba skaler ifade hello filtresi Hello sonucu olup olmadığını tanımlanmamış mantıksal olarak çok "true" eşitlemek değil bu yana tanımlanmamışsa, hello karşılık gelen belge hello sonucunda dahil edilir değil.</span><span class="sxs-lookup"><span data-stu-id="8b908-297">If hello result of hello scalar expression in hello filter is Undefined, hello corresponding document would not be included in hello result, since Undefined doesn't logically equate too"true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="8b908-298">ARASINDA anahtar sözcüğü</span><span class="sxs-lookup"><span data-stu-id="8b908-298">BETWEEN keyword</span></span>
<span data-ttu-id="8b908-299">ANSI SQL hello BETWEEN anahtar sözcüğü tooexpress sorguları aralıkları gibi değerlerin de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b908-299">You can also use hello BETWEEN keyword tooexpress queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="8b908-300">ARASINDA dizeyi veya sayı karşı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="8b908-301">Örneğin, bu sorgu hangi hello ilk alt düzey 1-5 arasında (her ikisi de dahil) olan tüm ailesi belgeleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-301">For example, this query returns all family documents in which hello first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="8b908-302">Farklı ANSI-SQL'de de hello BETWEEN yan tümcesi gibi hello FROM yan tümcesinde aşağıdaki örneğine hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b908-302">Unlike in ANSI-SQL, you can also use hello BETWEEN clause in hello FROM clause like in hello following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="8b908-303">Daha hızlı sorgu yürütme süreleri için toocreate tüm sayısal özellikleri/hello BETWEEN yan tümcesinde filtrelenen yolları karşı bir aralık dizin türünü kullanan bir dizin oluşturma ilkesi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8b908-303">For faster query execution times, remember toocreate an indexing policy that uses a range index type against any numeric properties/paths that are filtered in hello BETWEEN clause.</span></span> 

<span data-ttu-id="8b908-304">BETWEEN DocumentDB API ve ANSI SQL kullanarak arasında hello ana karma türlerinin özellikleri aralığı sorguları express – Örneğin, "bir sayı (5) düzeyde" olabilir bazı belgelerde ve diğerleri ("grade4") dizelerde farktır.</span><span class="sxs-lookup"><span data-stu-id="8b908-304">hello main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="8b908-305">Bu gibi durumlarda gibi JavaScript'te, iki farklı sonuçlarında "tanımsız" ve hello belge arasında bir karşılaştırma atlanacak.</span><span class="sxs-lookup"><span data-stu-id="8b908-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and hello document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="8b908-306">Mantıksal (AND, OR ve NOT) işleçleri</span><span class="sxs-lookup"><span data-stu-id="8b908-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="8b908-307">Mantıksal işleçler Boole değerleri üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="8b908-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="8b908-308">Bu işleçleri için mantıksal gerçekte tabloları Hello tabloları aşağıdaki hello gösterilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-308">hello logical truth tables for these operators are shown in hello following tables.</span></span>

| <span data-ttu-id="8b908-309">OR</span><span class="sxs-lookup"><span data-stu-id="8b908-309">OR</span></span> | <span data-ttu-id="8b908-310">True</span><span class="sxs-lookup"><span data-stu-id="8b908-310">True</span></span> | <span data-ttu-id="8b908-311">False</span><span class="sxs-lookup"><span data-stu-id="8b908-311">False</span></span> | <span data-ttu-id="8b908-312">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b908-313">True</span><span class="sxs-lookup"><span data-stu-id="8b908-313">True</span></span> |<span data-ttu-id="8b908-314">True</span><span class="sxs-lookup"><span data-stu-id="8b908-314">True</span></span> |<span data-ttu-id="8b908-315">True</span><span class="sxs-lookup"><span data-stu-id="8b908-315">True</span></span> |<span data-ttu-id="8b908-316">True</span><span class="sxs-lookup"><span data-stu-id="8b908-316">True</span></span> |
| <span data-ttu-id="8b908-317">False</span><span class="sxs-lookup"><span data-stu-id="8b908-317">False</span></span> |<span data-ttu-id="8b908-318">True</span><span class="sxs-lookup"><span data-stu-id="8b908-318">True</span></span> |<span data-ttu-id="8b908-319">False</span><span class="sxs-lookup"><span data-stu-id="8b908-319">False</span></span> |<span data-ttu-id="8b908-320">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-320">Undefined</span></span> |
| <span data-ttu-id="8b908-321">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-321">Undefined</span></span> |<span data-ttu-id="8b908-322">True</span><span class="sxs-lookup"><span data-stu-id="8b908-322">True</span></span> |<span data-ttu-id="8b908-323">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-323">Undefined</span></span> |<span data-ttu-id="8b908-324">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-324">Undefined</span></span> |

| <span data-ttu-id="8b908-325">VE</span><span class="sxs-lookup"><span data-stu-id="8b908-325">AND</span></span> | <span data-ttu-id="8b908-326">True</span><span class="sxs-lookup"><span data-stu-id="8b908-326">True</span></span> | <span data-ttu-id="8b908-327">False</span><span class="sxs-lookup"><span data-stu-id="8b908-327">False</span></span> | <span data-ttu-id="8b908-328">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b908-329">True</span><span class="sxs-lookup"><span data-stu-id="8b908-329">True</span></span> |<span data-ttu-id="8b908-330">True</span><span class="sxs-lookup"><span data-stu-id="8b908-330">True</span></span> |<span data-ttu-id="8b908-331">False</span><span class="sxs-lookup"><span data-stu-id="8b908-331">False</span></span> |<span data-ttu-id="8b908-332">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-332">Undefined</span></span> |
| <span data-ttu-id="8b908-333">False</span><span class="sxs-lookup"><span data-stu-id="8b908-333">False</span></span> |<span data-ttu-id="8b908-334">False</span><span class="sxs-lookup"><span data-stu-id="8b908-334">False</span></span> |<span data-ttu-id="8b908-335">False</span><span class="sxs-lookup"><span data-stu-id="8b908-335">False</span></span> |<span data-ttu-id="8b908-336">False</span><span class="sxs-lookup"><span data-stu-id="8b908-336">False</span></span> |
| <span data-ttu-id="8b908-337">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-337">Undefined</span></span> |<span data-ttu-id="8b908-338">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-338">Undefined</span></span> |<span data-ttu-id="8b908-339">False</span><span class="sxs-lookup"><span data-stu-id="8b908-339">False</span></span> |<span data-ttu-id="8b908-340">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-340">Undefined</span></span> |

| <span data-ttu-id="8b908-341">DEĞİL</span><span class="sxs-lookup"><span data-stu-id="8b908-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="8b908-342">True</span><span class="sxs-lookup"><span data-stu-id="8b908-342">True</span></span> |<span data-ttu-id="8b908-343">False</span><span class="sxs-lookup"><span data-stu-id="8b908-343">False</span></span> |
| <span data-ttu-id="8b908-344">False</span><span class="sxs-lookup"><span data-stu-id="8b908-344">False</span></span> |<span data-ttu-id="8b908-345">True</span><span class="sxs-lookup"><span data-stu-id="8b908-345">True</span></span> |
| <span data-ttu-id="8b908-346">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-346">Undefined</span></span> |<span data-ttu-id="8b908-347">Tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="8b908-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="8b908-348">Anahtar SÖZCÜĞÜ</span><span class="sxs-lookup"><span data-stu-id="8b908-348">IN keyword</span></span>
<span data-ttu-id="8b908-349">Belirtilen bir değeri bir listedeki herhangi bir değer ile eşleşip eşleşmediğini hello IN anahtar sözcüğü kullanılan toocheck olabilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-349">hello IN keyword can be used toocheck whether a specified value matches any value in a list.</span></span> <span data-ttu-id="8b908-350">Örneğin, bu sorgu, hello kimliği "WakefieldFamily" veya "AndersenFamily" biri olduğu tüm ailesi belgeleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-350">For example, this query returns all family documents where hello id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="8b908-351">Bu örnek hello durumu belirtilen hello hiçbirini olduğu tüm belgeleri döndüren değerleri.</span><span class="sxs-lookup"><span data-stu-id="8b908-351">This example returns all documents where hello state is any of hello specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="8b908-352">Üçlü (?) ve birleşim (?) işleçleri</span><span class="sxs-lookup"><span data-stu-id="8b908-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="8b908-353">Merhaba Üçlü ve birleşim işleçleri kullanılan toobuild koşullu ifadeler, C# ve JavaScript gibi programlama dillerinde benzer toopopular olabilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-353">hello Ternary and Coalesce operators can be used toobuild conditional expressions, similar toopopular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="8b908-354">Merhaba oluşturma yeni JSON özellikleri uçarak hello Üçlü (?) işleci çok kullanışlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-354">hello Ternary (?) operator can be very handy when constructing new JSON properties on hello fly.</span></span> <span data-ttu-id="8b908-355">Örneğin, artık, sorguları tooclassify hello sınıfı düzeyleri başlangıç/Orta/aşağıda gösterildiği gibi gelişmiş gibi İnsan okunabilir bir form içine yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b908-355">For example, now you can write queries tooclassify hello class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="8b908-356">Itanium tabanlı sistemler için hello çağrıları toohello operatör gibi aşağıdaki hello sorgusunda iç içe.</span><span class="sxs-lookup"><span data-stu-id="8b908-356">You can also nest hello calls toohello operator like in hello query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="8b908-357">Olarak diğer sorgu işleçleri ile Merhaba hello koşullu ifade başvurulan özelliklerinde herhangi bir belgesinde eksikse veya karşılaştırılan hello türleri farklıysa, sonra bu belgeleri hello sorgu sonuçlarında hariç tutulur.</span><span class="sxs-lookup"><span data-stu-id="8b908-357">As with other query operators, if hello referenced properties in hello conditional expression are missing in any document, or if hello types being compared are different, then those documents are excluded in hello query results.</span></span>

<span data-ttu-id="8b908-358">Merhaba birleşim (?) işleci olabilir tooefficiently onay hello bir özellik varlığını (paketini kullanılan</span><span class="sxs-lookup"><span data-stu-id="8b908-358">hello Coalesce (??) operator can be used tooefficiently check for hello presence of a property (a.k.a.</span></span> <span data-ttu-id="8b908-359">tanımlanır) belgede.</span><span class="sxs-lookup"><span data-stu-id="8b908-359">is defined) in a document.</span></span> <span data-ttu-id="8b908-360">Yarı yapılandırılmış karşı sorgularken bu yararlıdır veya karma türlerinin veri.</span><span class="sxs-lookup"><span data-stu-id="8b908-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="8b908-361">Örneğin, mevcut değilse bu sorguyu hello "Soyadı" varsa veya hello "Soyadı" döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-361">For example, this query returns hello "lastName" if present, or hello "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="8b908-362"><a id="EscapingReservedKeywords"></a>Tırnak işaretli özelliği erişimcisi</span><span class="sxs-lookup"><span data-stu-id="8b908-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="8b908-363">Özellikler hello tırnak işaretli özelliği işlecini kullanarak da erişebilirsiniz `[]`.</span><span class="sxs-lookup"><span data-stu-id="8b908-363">You can also access properties using hello quoted property operator `[]`.</span></span> <span data-ttu-id="8b908-364">Örneğin, `SELECT c.grade` ve `SELECT c["grade"]` eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="8b908-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="8b908-365">Bu sözdiziminin tooescape alanları, özel karakterler içeriyor veya bir SQL anahtar sözcüğü ya da ayrılmış sözcük olarak aynı ad tooshare hello olur bir özellik gerektiğinde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="8b908-365">This syntax is useful when you need tooescape a property that contains spaces, special characters, or happens tooshare hello same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="8b908-366"><a id="SelectClause"></a>SELECT yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="8b908-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="8b908-367">Merhaba SELECT yan tümcesi (**`SELECT <select_list>`**) zorunludur ve hangi değerlerin hello sorgudan tıpkı ANSI SQL'de alınır belirtir.</span><span class="sxs-lookup"><span data-stu-id="8b908-367">hello SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from hello query, just like in ANSI-SQL.</span></span> <span data-ttu-id="8b908-368">Merhaba kaynak belgeleri üstünde filtre uygulanmış hello alt geçirilir hello projeksiyon aşaması hello JSON değerleri alınır ve yeni bir JSON nesnesi, bunun geçirilen her giriş için oluşturulan burada belirtilen.</span><span class="sxs-lookup"><span data-stu-id="8b908-368">hello subset that's been filtered on top of hello source documents are passed onto hello projection phase, where hello specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="8b908-369">Aşağıdaki örnek hello tipik seçme sorgusu gösterir.</span><span class="sxs-lookup"><span data-stu-id="8b908-369">hello following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="8b908-370">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="8b908-371">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="8b908-372">İç içe Özellikler</span><span class="sxs-lookup"><span data-stu-id="8b908-372">Nested properties</span></span>
<span data-ttu-id="8b908-373">Aşağıdaki örneğine hello biz iki iç içe özellikler yansıtma `f.address.state` ve `f.address.city`.</span><span class="sxs-lookup"><span data-stu-id="8b908-373">In hello following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="8b908-374">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="8b908-375">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="8b908-376">Projeksiyon hello aşağıdaki örnekte gösterildiği gibi JSON ifadeler de destekler:</span><span class="sxs-lookup"><span data-stu-id="8b908-376">Projection also supports JSON expressions as shown in hello following example:</span></span>

<span data-ttu-id="8b908-377">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="8b908-378">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="8b908-379">Merhaba role daha bakalım `$1` burada.</span><span class="sxs-lookup"><span data-stu-id="8b908-379">Let's look at hello role of `$1` here.</span></span> <span data-ttu-id="8b908-380">Merhaba `SELECT` yan tümcesi toocreate bir JSON nesnesi gerekiyor ve hiçbir anahtar sağlanan beri örtük bağımsız değişken adları başlayarak kullanırız `$1`.</span><span class="sxs-lookup"><span data-stu-id="8b908-380">hello `SELECT` clause needs toocreate a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="8b908-381">Örneğin, etiketli iki örtük bağımsız değişkenlerini bu sorgunun döndürdüğü `$1` ve `$2`.</span><span class="sxs-lookup"><span data-stu-id="8b908-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="8b908-382">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="8b908-383">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="8b908-384">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="8b908-384">Aliasing</span></span>
<span data-ttu-id="8b908-385">Şimdi şimdi hello Yukarıdaki örnek açık yumuşatma ile değerlerin genişletme.</span><span class="sxs-lookup"><span data-stu-id="8b908-385">Now let's extend hello example above with explicit aliasing of values.</span></span> <span data-ttu-id="8b908-386">Diğer ad için kullanılan anahtar sözcük hello olduğu gibi.</span><span class="sxs-lookup"><span data-stu-id="8b908-386">AS is hello keyword used for aliasing.</span></span> <span data-ttu-id="8b908-387">Planlanması hello ikinci değer çalışırken gösterildiği gibi isteğe bağlı `NameInfo`.</span><span class="sxs-lookup"><span data-stu-id="8b908-387">It's optional as shown while projecting hello second value as `NameInfo`.</span></span> 

<span data-ttu-id="8b908-388">Bir sorgu hello sahip iki özellik gerekmesi durumunda aynı adı yumuşatma birini veya her ikisini böylece bunlar öngörülen hello disambiguated özellikleri hello kullanılan toorename olmalı sonucu.</span><span class="sxs-lookup"><span data-stu-id="8b908-388">In case a query has two properties with hello same name, aliasing must be used toorename one or both of hello properties so that they are disambiguated in hello projected result.</span></span>

<span data-ttu-id="8b908-389">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="8b908-390">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="8b908-391">Skaler ifade</span><span class="sxs-lookup"><span data-stu-id="8b908-391">Scalar expressions</span></span>
<span data-ttu-id="8b908-392">Ayrıca tooproperty başvuruyor, skaler ifadeler sabitler, aritmetik ifadeler, mantıksal ifadeler, vb. gibi hello SELECT yan tümcesi de destekler. Örneğin, basit bir "Hello World" sorgu aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="8b908-392">In addition tooproperty references, hello SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="8b908-393">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="8b908-394">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="8b908-395">Burada, skaler bir ifade kullanır daha karmaşık bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8b908-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="8b908-396">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="8b908-397">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="8b908-398">Aşağıdaki örneğine hello hello hello skaler ifade Boolean sonucudur.</span><span class="sxs-lookup"><span data-stu-id="8b908-398">In hello following example, hello result of hello scalar expression is a Boolean.</span></span>

<span data-ttu-id="8b908-399">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="8b908-400">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="8b908-401">Nesne ve dizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="8b908-401">Object and array creation</span></span>
<span data-ttu-id="8b908-402">Başka bir anahtar DocumentDB API SQL dizi/nesne oluşturma özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="8b908-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="8b908-403">Merhaba önceki örnekte yeni bir JSON nesnesi oluşturduğumuz dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="8b908-403">In hello previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="8b908-404">Benzer şekilde, bir de diziler hello örnekleri aşağıdaki gösterildiği gibi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8b908-404">Similarly, one can also construct arrays as shown in hello following examples:</span></span>

<span data-ttu-id="8b908-405">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="8b908-406">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-406">**Results**</span></span>  

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

### <span data-ttu-id="8b908-407"><a id="ValueKeyword"></a>VALUE anahtar sözcüğü</span><span class="sxs-lookup"><span data-stu-id="8b908-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="8b908-408">Merhaba **değeri** anahtar sözcüğü bir şekilde tooreturn JSON değer sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b908-408">hello **VALUE** keyword provides a way tooreturn JSON value.</span></span> <span data-ttu-id="8b908-409">Örneğin, döndürür hello skaler gösterilen hello sorgu `"Hello World"` yerine `{$1: "Hello World"}`.</span><span class="sxs-lookup"><span data-stu-id="8b908-409">For example, hello query shown below returns hello scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="8b908-410">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="8b908-411">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="8b908-412">Merhaba aşağıdaki sorgunun döndürdüğü hello JSON değeri hello olmadan `"address"` hello sonuçlarında etiketi.</span><span class="sxs-lookup"><span data-stu-id="8b908-412">hello following query returns hello JSON value without hello `"address"` label in hello results.</span></span>

<span data-ttu-id="8b908-413">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="8b908-414">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-414">**Results**</span></span>  

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

<span data-ttu-id="8b908-415">Merhaba aşağıdaki örnekte bu tooshow nasıl genişlettiğini tooreturn JSON ilkel değerlerini (yaprak düzeyi hello JSON ağaç hello).</span><span class="sxs-lookup"><span data-stu-id="8b908-415">hello following example extends this tooshow how tooreturn JSON primitive values (hello leaf level of hello JSON tree).</span></span> 

<span data-ttu-id="8b908-416">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="8b908-417">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="8b908-418">* İşleci</span><span class="sxs-lookup"><span data-stu-id="8b908-418">* Operator</span></span>
<span data-ttu-id="8b908-419">Merhaba özel işleci (*) desteklenen tooproject hello olarak belgedir-değil.</span><span class="sxs-lookup"><span data-stu-id="8b908-419">hello special operator (*) is supported tooproject hello document as-is.</span></span> <span data-ttu-id="8b908-420">Kullanıldığında, hello yalnızca alan öngörülen olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b908-420">When used, it must be hello only projected field.</span></span> <span data-ttu-id="8b908-421">While gibi bir sorgu `SELECT * FROM Families f` geçerli olduğu `SELECT VALUE * FROM Families f ` ve `SELECT *, f.id FROM Families f ` geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="8b908-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="8b908-422">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="8b908-423">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-423">**Results**</span></span>

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

### <span data-ttu-id="8b908-424"><a id="TopKeyword"></a>TOP işleci</span><span class="sxs-lookup"><span data-stu-id="8b908-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="8b908-425">Merhaba üst anahtar sözcüğü olabilir toolimit hello değerleri sorgudan sayısı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8b908-425">hello TOP keyword can be used toolimit hello number of values from a query.</span></span> <span data-ttu-id="8b908-426">ÜST hello ORDER BY yan tümcesi ile birlikte kullanıldığında, hello sonuç kümesi sınırlı toohello ilk N sıralı değerler sayısıdır; Aksi takdirde, tanımlanmamış bir sırada hello ilk N sonuç sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-426">When TOP is used in conjunction with hello ORDER BY clause, hello result set is limited toohello first N number of ordered values; otherwise, it returns hello first N number of results in an undefined order.</span></span> <span data-ttu-id="8b908-427">En iyi uygulama, bir SELECT deyimi içinde ORDER BY yan tümcesi her zaman hello üst yan tümcesiyle birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="8b908-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with hello TOP clause.</span></span> <span data-ttu-id="8b908-428">Bu toopredictably belirtmek hangi satırların üst tarafından etkilenen hello tek yoludur.</span><span class="sxs-lookup"><span data-stu-id="8b908-428">This is hello only way toopredictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="8b908-429">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="8b908-430">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-430">**Results**</span></span>

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

<span data-ttu-id="8b908-431">ÜST bir değişken değeri parametreli sorgular kullanmayı veya sabit bir değer (yukarıda gösterildiği gibi) ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="8b908-432">Daha fazla ayrıntı için lütfen aşağıdaki parametreli sorgular bakın.</span><span class="sxs-lookup"><span data-stu-id="8b908-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="8b908-433"><a id="Aggregates"></a>Toplama işlevleri</span><span class="sxs-lookup"><span data-stu-id="8b908-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="8b908-434">Toplamalar hello gerçekleştirebilirsiniz `SELECT` yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="8b908-434">You can also perform aggregations in hello `SELECT` clause.</span></span> <span data-ttu-id="8b908-435">Toplama işlevleri, bir değerleri kümesi üzerinde bir hesaplama gerçekleştirmek ve tek bir değer döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="8b908-436">Örneğin, hello aşağıdaki sorguyu hello koleksiyonundaki ailesi belge hello sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-436">For example, hello following query returns hello count of family documents within hello collection.</span></span>

<span data-ttu-id="8b908-437">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="8b908-438">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="8b908-439">Ayrıca hello skaler hello değerini toplama hello kullanarak dönebilirsiniz `VALUE` anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="8b908-439">You can also return hello scalar value of hello aggregate by using hello `VALUE` keyword.</span></span> <span data-ttu-id="8b908-440">Örneğin, hello aşağıdaki sorguyu Merhaba sayımını değerleri tek bir sayı döndürür:</span><span class="sxs-lookup"><span data-stu-id="8b908-440">For example, hello following query returns hello count of values as a single number:</span></span>

<span data-ttu-id="8b908-441">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="8b908-442">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="8b908-443">Filtrelerle birlikte toplamalar de gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b908-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="8b908-444">Örneğin, hello aşağıdaki sorguyu Merhaba sayımını hello adresi belgelerle hello Washington eyaleti yasalarına içinde döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-444">For example, hello following query returns hello count of documents with hello address in hello state of Washington.</span></span>

<span data-ttu-id="8b908-445">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="8b908-446">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="8b908-447">Merhaba aşağıdaki tabloda hello listesini desteklenen toplama işlevleri DocumentDB API gösterir.</span><span class="sxs-lookup"><span data-stu-id="8b908-447">hello following table shows hello list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="8b908-448">`SUM`ve `AVG` ise sayısal değer üzerinde gerçekleştirilen `COUNT`, `MIN`, ve `MAX` numaraları, dizeleri, Boole değerlerini ve null değerlere gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="8b908-449">Kullanım</span><span class="sxs-lookup"><span data-stu-id="8b908-449">Usage</span></span> | <span data-ttu-id="8b908-450">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b908-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="8b908-451">SAYISI</span><span class="sxs-lookup"><span data-stu-id="8b908-451">COUNT</span></span> | <span data-ttu-id="8b908-452">Merhaba ifadesinde öğe sayısını döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="8b908-452">Returns hello number of items in hello expression.</span></span> |
| <span data-ttu-id="8b908-453">TOPLA</span><span class="sxs-lookup"><span data-stu-id="8b908-453">SUM</span></span>   | <span data-ttu-id="8b908-454">Merhaba ifadedeki tüm hello değerlerinin toplamını döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="8b908-454">Returns hello sum of all hello values in hello expression.</span></span> |
| <span data-ttu-id="8b908-455">MIN</span><span class="sxs-lookup"><span data-stu-id="8b908-455">MIN</span></span>   | <span data-ttu-id="8b908-456">Döndürür hello ifadedeki en küçük değer hello.</span><span class="sxs-lookup"><span data-stu-id="8b908-456">Returns hello minimum value in hello expression.</span></span> |
| <span data-ttu-id="8b908-457">EN BÜYÜK</span><span class="sxs-lookup"><span data-stu-id="8b908-457">MAX</span></span>   | <span data-ttu-id="8b908-458">Hello ifadedeki en büyük değeri döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="8b908-458">Returns hello maximum value in hello expression.</span></span> |
| <span data-ttu-id="8b908-459">ORTALAMA</span><span class="sxs-lookup"><span data-stu-id="8b908-459">AVG</span></span>   | <span data-ttu-id="8b908-460">Merhaba ifadesinde hello değerlerin ortalamasını döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="8b908-460">Returns hello average of hello values in hello expression.</span></span> |

<span data-ttu-id="8b908-461">Toplamalar, bir dizi yineleme hello sonuçlarını de gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-461">Aggregates can also be performed over hello results of an array iteration.</span></span> <span data-ttu-id="8b908-462">Daha fazla bilgi için bkz: [dizi yineleme sorgularda](#Iteration).</span><span class="sxs-lookup"><span data-stu-id="8b908-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="8b908-463">Azure portal'ın sorgu Gezgini kullanarak hello zaman toplama sorguları sorgu sayfası kısmen toplanmış sonuçlar hello döndürebilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8b908-463">When using hello Azure portal's Query Explorer, note that aggregation queries may return hello partially aggregated results over a query page.</span></span> <span data-ttu-id="8b908-464">Hello SDK'ları, tek bir toplu değer tüm sayfalardaki üretir.</span><span class="sxs-lookup"><span data-stu-id="8b908-464">hello SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="8b908-465">Kod kullanarak tooperform toplama sorguları ihtiyacınız .NET SDK'sı 1.12.0, .NET Core SDK 1.1.0 veya Java SDK'sı 1.9.5 da sipariş veya üstü.</span><span class="sxs-lookup"><span data-stu-id="8b908-465">In order tooperform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="8b908-466"><a id="OrderByClause"></a>ORDER BY yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="8b908-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="8b908-467">Gibi ANSI-SQL'de, isteğe bağlı bir Order By yan tümcesi sorgularken ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b908-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="8b908-468">Merhaba yan tümcesi sonuçlar alınması gereken isteğe bağlı ASC/DESC bağımsız değişkeni toospecify hello sipariş içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-468">hello clause can include an optional ASC/DESC argument toospecify hello order in which results must be retrieved.</span></span>

<span data-ttu-id="8b908-469">Örneğin, işte sorguda aileleri sırasına hello yerleşik Şehir kişinin adını alır.</span><span class="sxs-lookup"><span data-stu-id="8b908-469">For example, here's a query that retrieves families in order of hello resident city's name.</span></span>

<span data-ttu-id="8b908-470">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="8b908-471">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-471">**Results**</span></span>

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

<span data-ttu-id="8b908-472">Burada da sorguda aileleri sayı temsil eden bir hello gibi dönem zamanı, yani, geçen süre 1 Ocak 1970'ten itibaren saniye cinsinden, depolanan oluşturma tarih sırasına göre alır.</span><span class="sxs-lookup"><span data-stu-id="8b908-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing hello epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="8b908-473">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="8b908-474">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-474">**Results**</span></span>

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

## <span data-ttu-id="8b908-475"><a id="Advanced"></a>Gelişmiş veritabanı kavramlarını ve SQL sorguları</span><span class="sxs-lookup"><span data-stu-id="8b908-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="8b908-476"><a id="Iteration"></a>Yineleme</span><span class="sxs-lookup"><span data-stu-id="8b908-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="8b908-477">Yeni bir yapı hello eklenen **IN** DocumentDB API SQL tooprovide desteği, JSON diziler yineleme anahtar sözcük.</span><span class="sxs-lookup"><span data-stu-id="8b908-477">A new construct was added via hello **IN** keyword in DocumentDB API SQL tooprovide support for iterating over JSON arrays.</span></span> <span data-ttu-id="8b908-478">Merhaba FROM kaynak yineleme için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b908-478">hello FROM source provides support for iteration.</span></span> <span data-ttu-id="8b908-479">Aşağıdaki örneğine hello ile başlayalım:</span><span class="sxs-lookup"><span data-stu-id="8b908-479">Let's start with hello following example:</span></span>

<span data-ttu-id="8b908-480">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="8b908-481">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-481">**Results**</span></span>  

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

<span data-ttu-id="8b908-482">Şimdi hello koleksiyonundaki alt öğe üzerinden yineleme gerçekleştiren başka bir sorgu bakalım.</span><span class="sxs-lookup"><span data-stu-id="8b908-482">Now let's look at another query that performs iteration over children in hello collection.</span></span> <span data-ttu-id="8b908-483">Merhaba çıkış dizisi Hello fark unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8b908-483">Note hello difference in hello output array.</span></span> <span data-ttu-id="8b908-484">Bu örnek böler `children` ve tek bir dizi hello sonuçları düzleştirir.</span><span class="sxs-lookup"><span data-stu-id="8b908-484">This example splits `children` and flattens hello results into a single array.</span></span>  

<span data-ttu-id="8b908-485">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="8b908-486">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-486">**Results**</span></span>  

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

<span data-ttu-id="8b908-487">Bu, daha fazla hello aşağıdaki örnekte gösterildiği gibi hello dizinin her bir giriş üzerinde kullanılan toofilter olabilir:</span><span class="sxs-lookup"><span data-stu-id="8b908-487">This can be further used toofilter on each individual entry of hello array as shown in hello following example:</span></span>

<span data-ttu-id="8b908-488">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="8b908-489">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="8b908-490">Dizi yineleme hello sonucunun üzerinde toplama de gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b908-490">You can also perform aggregation over hello result of array iteration.</span></span> <span data-ttu-id="8b908-491">Örneğin, hello aşağıdaki sorguyu hello tüm aileleri arasında alt sayar.</span><span class="sxs-lookup"><span data-stu-id="8b908-491">For example, hello following query counts hello number of children among all families.</span></span>

<span data-ttu-id="8b908-492">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="8b908-493">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="8b908-494"><a id="Joins"></a>Birleşimler</span><span class="sxs-lookup"><span data-stu-id="8b908-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="8b908-495">İlişkisel bir veritabanında tablolar arasında hello gerek toojoin önemlidir.</span><span class="sxs-lookup"><span data-stu-id="8b908-495">In a relational database, hello need toojoin across tables is important.</span></span> <span data-ttu-id="8b908-496">Merhaba normalleştirilmiş mantıksal corollary toodesigning şemaları kullanıcının.</span><span class="sxs-lookup"><span data-stu-id="8b908-496">It's hello logical corollary toodesigning normalized schemas.</span></span> <span data-ttu-id="8b908-497">Bulmadýðýný toothis, DocumentDB API şemasız belgelerin hello Normalleştirilmemiş veri modeli ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="8b908-497">Contrary toothis, DocumentDB API deals with hello denormalized data model of schema-free documents.</span></span> <span data-ttu-id="8b908-498">Bu hello mantıksal eşdeğerdir "Self Katıl" a.</span><span class="sxs-lookup"><span data-stu-id="8b908-498">This is hello logical equivalent of a "self-join".</span></span>

<span data-ttu-id="8b908-499">Merhaba dili destekleyen hello sözdizimi < from_source1 > JOIN < from_source2 > birleştirme ediyor... < From_sourceN > katılın.</span><span class="sxs-lookup"><span data-stu-id="8b908-499">hello syntax that hello language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="8b908-500">Genel olarak, bu bir dizi döndürür **N**- diziler (ile tanımlama grubu **N** değerleri).</span><span class="sxs-lookup"><span data-stu-id="8b908-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="8b908-501">Her tanımlama grubu tüm koleksiyon diğer adları kendi ilgili ayarlar yineleme tarafından üretilen değerler içeriyor.</span><span class="sxs-lookup"><span data-stu-id="8b908-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="8b908-502">Diğer bir deyişle, tam bir çapraz ürün hello birleştirme katılan hello kümelerinin budur.</span><span class="sxs-lookup"><span data-stu-id="8b908-502">In other words, this is a full cross product of hello sets participating in hello join.</span></span>

<span data-ttu-id="8b908-503">Merhaba aşağıdaki örneklerde hello JOIN yan tümcesi nasıl çalıştığı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8b908-503">hello following examples show how hello JOIN clause works.</span></span> <span data-ttu-id="8b908-504">Hello çapraz ürün kaynak ve boş her belge boş olduğundan aşağıdaki örneğine hello hello sonuç boş kalır.</span><span class="sxs-lookup"><span data-stu-id="8b908-504">In hello following example, hello result is empty since hello cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="8b908-505">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="8b908-506">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="8b908-507">Aşağıdaki örneğine hello hello birleştirme hello belge kökü hello arasında ise `children` subroot.</span><span class="sxs-lookup"><span data-stu-id="8b908-507">In hello following example, hello join is between hello document root and hello `children` subroot.</span></span> <span data-ttu-id="8b908-508">Bu, iki JSON nesnesi arasındaki arası bir üründür.</span><span class="sxs-lookup"><span data-stu-id="8b908-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="8b908-509">alt öğeleri olan bir dizi hello olgu biz hello alt öğeleri dizisi için tek bir kök çalışıyorsanız hello birleşim etkin değil.</span><span class="sxs-lookup"><span data-stu-id="8b908-509">hello fact that children is an array is not effective in hello JOIN since we are dealing with a single root that is hello children array.</span></span> <span data-ttu-id="8b908-510">Bu nedenle Hello hello diziye sahip her bir belgenin vektörel çarpımını üretir tam olarak yalnızca bir belge beri hello sonucu yalnızca iki sonucu içerir.</span><span class="sxs-lookup"><span data-stu-id="8b908-510">Hence hello result contains only two results, since hello cross product of each document with hello array yields exactly only one document.</span></span>

<span data-ttu-id="8b908-511">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="8b908-512">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="8b908-513">Aşağıdaki örnek hello daha geleneksel bir birleştirme gösterir:</span><span class="sxs-lookup"><span data-stu-id="8b908-513">hello following example shows a more conventional join:</span></span>

<span data-ttu-id="8b908-514">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="8b908-515">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-515">**Results**</span></span>

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



<span data-ttu-id="8b908-516">Merhaba ilk şey toonote bu hello olan `from_source` Merhaba, **katılma** yan tümcesi olan yineleyici.</span><span class="sxs-lookup"><span data-stu-id="8b908-516">hello first thing toonote is that hello `from_source` of hello **JOIN** clause is an iterator.</span></span> <span data-ttu-id="8b908-517">Bu nedenle, hello akışı bu durumda şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="8b908-517">So, hello flow in this case is as follows:</span></span>  

* <span data-ttu-id="8b908-518">Her alt öğesi genişletin **c** hello dizisindeki.</span><span class="sxs-lookup"><span data-stu-id="8b908-518">Expand each child element **c** in hello array.</span></span>
* <span data-ttu-id="8b908-519">Çapraz ürün hello belge hello kökü ile geçerli **f** her alt öğesi olan **c** hello ilk adımda düzleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="8b908-519">Apply a cross product with hello root of hello document **f** with each child element **c** that was flattened in hello first step.</span></span>
* <span data-ttu-id="8b908-520">Son olarak, hello kök nesnesi proje **f** name özelliği bırakır.</span><span class="sxs-lookup"><span data-stu-id="8b908-520">Finally, project hello root object **f** name property alone.</span></span> 

<span data-ttu-id="8b908-521">Merhaba ilk belge (`AndersenFamily`) yalnızca tek bir nesnede karşılık gelen toothis belgesini hello sonuç kümesini içerecek şekilde yalnızca bir alt öğe içeriyor.</span><span class="sxs-lookup"><span data-stu-id="8b908-521">hello first document (`AndersenFamily`) contains only one child element, so hello result set contains only a single object corresponding toothis document.</span></span> <span data-ttu-id="8b908-522">Merhaba ikinci belge (`WakefieldFamily`) iki alt öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="8b908-522">hello second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="8b908-523">Bu nedenle, hello çapraz ürün ayrı bir nesne için böylece her alt karşılık gelen toothis belge için iki nesne sonuçta her bir alt üretir.</span><span class="sxs-lookup"><span data-stu-id="8b908-523">So, hello cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding toothis document.</span></span> <span data-ttu-id="8b908-524">Her iki bu belgedeki alanlar hello kök hello aynı bir çapraz ürün beklendiği gibi.</span><span class="sxs-lookup"><span data-stu-id="8b908-524">hello root fields in both these documents are hello same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="8b908-525">Hello hello birleştirme gerçek yardımcı programı olan başka bir şekil hello cross-ürünün tooform diziler zor tooproject.</span><span class="sxs-lookup"><span data-stu-id="8b908-525">hello real utility of hello JOIN is tooform tuples from hello cross-product in a shape that's otherwise difficult tooproject.</span></span> <span data-ttu-id="8b908-526">Biz hello aşağıdaki örnekte gördüğünüz gibi Ayrıca, bir tanımlama grubu hello birleşimi olanak tanıyan hello filtre kullanıcı tarafından hello diziler genel memnun bir koşul seçti.</span><span class="sxs-lookup"><span data-stu-id="8b908-526">Furthermore, as we see in hello example below, you could filter on hello combination of a tuple that lets' hello user chose a condition satisfied by hello tuples overall.</span></span>

<span data-ttu-id="8b908-527">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="8b908-528">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-528">**Results**</span></span>

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



<span data-ttu-id="8b908-529">Bu örnek, örnek önceki hello doğal bir uzantıdır ve çift birleştirme gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="8b908-529">This example is a natural extension of hello preceding example, and performs a double join.</span></span> <span data-ttu-id="8b908-530">Bu nedenle, hello çapraz ürün sözde koddan hello görüntülenebilir:</span><span class="sxs-lookup"><span data-stu-id="8b908-530">So, hello cross product can be viewed as hello following pseudo-code:</span></span>

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

<span data-ttu-id="8b908-531">`AndersenFamily`bir evcil hayvan sahip bir alt sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8b908-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="8b908-532">Bu nedenle, hello çapraz ürün bir satır verir (1\*1\*1) bu aile gelen.</span><span class="sxs-lookup"><span data-stu-id="8b908-532">So, hello cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="8b908-533">WakefieldFamily ancak iki alt öğe, ancak yalnızca bir alt "Jesse" Evcil Hayvanlar içeriyor.</span><span class="sxs-lookup"><span data-stu-id="8b908-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="8b908-534">Jesse iki Evcil Hayvanlar yine de vardır.</span><span class="sxs-lookup"><span data-stu-id="8b908-534">Jesse has two pets though.</span></span> <span data-ttu-id="8b908-535">Bu nedenle hello çapraz ürün 1 verir\*1\*2 = 2 Bu ailesinden satırlar.</span><span class="sxs-lookup"><span data-stu-id="8b908-535">Hence hello cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="8b908-536">Merhaba sonraki örnekte olduğundan bir ek filtre `pet`.</span><span class="sxs-lookup"><span data-stu-id="8b908-536">In hello next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="8b908-537">Merhaba Evcil adı "Gölge" olduğu tüm hello diziler dışlar.</span><span class="sxs-lookup"><span data-stu-id="8b908-537">This excludes all hello tuples where hello pet name is not "Shadow".</span></span> <span data-ttu-id="8b908-538">Biz mümkün toobuild diziler dizileri, herhangi bir hello tuple hello öğelerinin filtre gelen olan ve herhangi bir bileşimini hello öğeleri proje dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="8b908-538">Notice that we are able toobuild tuples from arrays, filter on any of hello elements of hello tuple, and project any combination of hello elements.</span></span> 

<span data-ttu-id="8b908-539">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="8b908-540">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="8b908-541"><a id="JavaScriptIntegration"></a>JavaScript tümleştirme</span><span class="sxs-lookup"><span data-stu-id="8b908-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="8b908-542">Azure Cosmos DB JavaScript tabanlı uygulama mantığını saklı yordamları ve Tetikleyicileri bakımından hello koleksiyonlar üzerinde doğrudan yürütmek için bir programlama modeli sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b908-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="8b908-543">Bu, her ikisi için sağlar:</span><span class="sxs-lookup"><span data-stu-id="8b908-543">This allows for both:</span></span>

* <span data-ttu-id="8b908-544">Özelliği toodo yüksek performanslı işlem CRUD işlemleri ve belgeleri hello doğrudan hello veritabanı altyapısının içinde JavaScript çalışma zamanı için derin tümleştirme, bir koleksiyondaki sorguları.</span><span class="sxs-lookup"><span data-stu-id="8b908-544">Ability toodo high-performance transactional CRUD operations and queries against documents in a collection by virtue of hello deep integration of JavaScript runtime directly within hello database engine.</span></span> 
* <span data-ttu-id="8b908-545">Denetim akışı, değişken kapsamı, atama ve özel durum işleme temelleri veritabanı işlemleri ile tümleştirilmesi doğal bir model.</span><span class="sxs-lookup"><span data-stu-id="8b908-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="8b908-546">JavaScript tümleştirme için Azure Cosmos DB desteği hakkında daha fazla ayrıntı için lütfen toohello JavaScript sunucu tarafı programlama belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="8b908-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer toohello JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="8b908-547"><a id="UserDefinedFunctions"></a>Kullanıcı tanımlı işlevler (UDF'ler)</span><span class="sxs-lookup"><span data-stu-id="8b908-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="8b908-548">Bu makalede önceden tanımlanmış hello türleri ile birlikte DocumentDB API SQL kullanıcı tanımlı işlevler (UDF) için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b908-548">Along with hello types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="8b908-549">Özellikle, skaler UDF'ler burada hello geliştiriciler sıfır veya daha çok değişkenlerinde geçirmek ve geri tek bağımsız değişken sonuç desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8b908-549">In particular, scalar UDFs are supported where hello developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="8b908-550">Bu değişkenin her biri geçerli JSON değerleri olmak için denetlenir.</span><span class="sxs-lookup"><span data-stu-id="8b908-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="8b908-551">Merhaba DocumentDB API SQL söz dizimi, bu kullanıcı tanımlı işlevler kullanılarak toosupport özel uygulama mantığını genişletilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-551">hello DocumentDB API SQL syntax is extended toosupport custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="8b908-552">UDF'ler DocumentDB API'si ile kayıtlı olması ve sonra bir SQL sorgusu bir parçası olarak başvurulan.</span><span class="sxs-lookup"><span data-stu-id="8b908-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="8b908-553">Aslında, UDF'ler exquisitely olan hello sorgular tarafından çağrılan toobe tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8b908-553">In fact, hello UDFs are exquisitely designed toobe invoked by queries.</span></span> <span data-ttu-id="8b908-554">Corollary toothis seçenek olarak, UDF'ler erişim toohello bağlam nesnesi, diğer JavaScript hello yoktur türleri (saklı yordamları ve Tetikleyicileri) sahip.</span><span class="sxs-lookup"><span data-stu-id="8b908-554">As a corollary toothis choice, UDFs do not have access toohello context object which hello other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="8b908-555">Salt okunur olarak sorguları yürütmek olduğundan, birincil veya ikincil çoğaltmaları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b908-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="8b908-556">Bu nedenle, UDF'ler diğer JavaScript türlerinin aksine ikincil çoğaltmalar üzerinde tasarlanmış toorun altındadır.</span><span class="sxs-lookup"><span data-stu-id="8b908-556">Therefore, UDFs are designed toorun on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="8b908-557">Aşağıda, özellikle bir belge koleksiyonu altında hello Cosmos DB veritabanı sırasında bir UDF nasıl kaydedilebilir bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="8b908-557">Below is an example of how a UDF can be registered at hello Cosmos DB database, specifically under a document collection.</span></span>

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

<span data-ttu-id="8b908-558">Merhaba önceki örnekte oluşturur adı olan bir UDF `REGEX_MATCH`.</span><span class="sxs-lookup"><span data-stu-id="8b908-558">hello preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="8b908-559">İki JSON dizesi değerlerini kabul `input` ve `pattern` ve JavaScript'in string.match() işlevi kullanarak hello ilk eşleşmeleri hello düzeni belirtilen ikinci hello gerekmediğini denetler.</span><span class="sxs-lookup"><span data-stu-id="8b908-559">It accepts two JSON string values `input` and `pattern` and checks if hello first matches hello pattern specified in hello second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="8b908-560">Bir yansıtma sorgu Biz bu UDF artık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b908-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="8b908-561">UDF'ler hello büyük küçük harfe duyarlı önekiyle "udf." nitelenmiş olmalıdır</span><span class="sxs-lookup"><span data-stu-id="8b908-561">UDFs must be qualified with hello case-sensitive prefix "udf."</span></span> <span data-ttu-id="8b908-562">gelen sorgulara çağrıldığında.</span><span class="sxs-lookup"><span data-stu-id="8b908-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="8b908-563">Önceki too3/17/2015, Cosmos DB hello "udf." olmadan UDF çağrı desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8b908-563">Prior too3/17/2015, Cosmos DB supported UDF calls without hello "udf."</span></span> <span data-ttu-id="8b908-564">önek seçin REGEX_MATCH() ister.</span><span class="sxs-lookup"><span data-stu-id="8b908-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="8b908-565">Bu arama deseni kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="8b908-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="8b908-566">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="8b908-567">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="8b908-568">Merhaba UDF de bir filtre içinde de hello "udf ile." tam hello aşağıdaki örnekte, gösterildiği gibi kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="8b908-568">hello UDF can also be used inside a filter as shown in hello example below, also qualified with hello "udf."</span></span> <span data-ttu-id="8b908-569">öneki:</span><span class="sxs-lookup"><span data-stu-id="8b908-569">prefix:</span></span>

<span data-ttu-id="8b908-570">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="8b908-571">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="8b908-572">Esas olarak, UDF'ler geçerli skaler ifadelerini ve tahminleri ve filtreleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="8b908-573">tooexpand UDF'ler hello gücüyle başka bir örneğe koşullu mantığı ile bakalım:</span><span class="sxs-lookup"><span data-stu-id="8b908-573">tooexpand on hello power of UDFs, let's look at another example with conditional logic:</span></span>

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


<span data-ttu-id="8b908-574">Alıştırmaları UDF hello bir örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8b908-574">Below is an example that exercises hello UDF.</span></span>

<span data-ttu-id="8b908-575">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="8b908-576">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-576">**Results**</span></span>

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


<span data-ttu-id="8b908-577">Önceki örnekler gösterimi hello gibi UDF'ler JavaScript dil hello gücünü hello DocumentDB API SQL tooprovide ile bir zengin programlanabilir arabirimi toodo karmaşık yordam, koşullu mantık hello Yardım yerleşik JavaScript çalışma zamanı ile tümleştirme yetenekleri.</span><span class="sxs-lookup"><span data-stu-id="8b908-577">As hello preceding examples showcase, UDFs integrate hello power of JavaScript language with hello DocumentDB API SQL tooprovide a rich programmable interface toodo complex procedural, conditional logic with hello help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="8b908-578">DocumentDB API SQL hello bağımsız değişkenleri toohello UDF'ler hello kaynağındaki her belge için hello geçerli aşamasında işleme hello UDF (WHERE yan tümcesi veya SELECT yan tümcesi) sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b908-578">DocumentDB API SQL provides hello arguments toohello UDFs for each document in hello source at hello current stage (WHERE clause or SELECT clause) of processing hello UDF.</span></span> <span data-ttu-id="8b908-579">Merhaba sonucu olarak dahil edilmiş genel yürütme ardışık düzeni sorunsuz bir şekilde hello.</span><span class="sxs-lookup"><span data-stu-id="8b908-579">hello result is incorporated in hello overall execution pipeline seamlessly.</span></span> <span data-ttu-id="8b908-580">Başvurulan tooby hello UDF parametreleri hello parametre olarak kabul hello JSON değeri, kullanılabilir değil hello Özellikleri tanımlanmamış ve bu nedenle hello UDF çağırma tamamen atlanır.</span><span class="sxs-lookup"><span data-stu-id="8b908-580">If hello properties referred tooby hello UDF parameters are not available in hello JSON value, hello parameter is considered as undefined and hence hello UDF invocation is entirely skipped.</span></span> <span data-ttu-id="8b908-581">Benzer şekilde hello UDF Hello sonucu tanımsız ise hello sonucunda bulunmaz.</span><span class="sxs-lookup"><span data-stu-id="8b908-581">Similarly if hello result of hello UDF is undefined, it's not included in hello result.</span></span> 

<span data-ttu-id="8b908-582">Özet olarak, UDF'ler harika Araçlar toodo karmaşık iş mantığı hello sorgu kapsamında ' dir.</span><span class="sxs-lookup"><span data-stu-id="8b908-582">In summary, UDFs are great tools toodo complex business logic as part of hello query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="8b908-583">İşleç değerlendirme</span><span class="sxs-lookup"><span data-stu-id="8b908-583">Operator evaluation</span></span>
<span data-ttu-id="8b908-584">Cosmos DB, bir JSON veritabanı olma hello virtue tarafından JavaScript işleçleri ve değerlendirme semantiği ile parallels çizer.</span><span class="sxs-lookup"><span data-stu-id="8b908-584">Cosmos DB, by hello virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="8b908-585">Cosmos DB toopreserve JavaScript semantiği JSON desteği bakımından çalışır, ancak bazı durumlarda hello işlemi değerlendirme farklıdır.</span><span class="sxs-lookup"><span data-stu-id="8b908-585">While Cosmos DB tries toopreserve JavaScript semantics in terms of JSON support, hello operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="8b908-586">Merhaba değerleri veritabanından kadar DocumentDB API SQL'de aksine geleneksel SQL değerlerin hello türleri bilinmez genellikle.</span><span class="sxs-lookup"><span data-stu-id="8b908-586">In DocumentDB API SQL, unlike in traditional SQL, hello types of values are often not known until hello values are retrieved from database.</span></span> <span data-ttu-id="8b908-587">Sipariş tooefficiently sorguları yürütün, hello işleçleri çoğunu sıkı tür gereksinimleri vardır.</span><span class="sxs-lookup"><span data-stu-id="8b908-587">In order tooefficiently execute queries, most of hello operators have strict type requirements.</span></span> 

<span data-ttu-id="8b908-588">DocumentDB API SQL JavaScript aksine örtük dönüşümler gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="8b908-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="8b908-589">Örneğin, bir sorgu ister `SELECT * FROM Person p WHERE p.Age = 21` eşleşen değeri olan 21 yaş özelliği içeren belgeleri.</span><span class="sxs-lookup"><span data-stu-id="8b908-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="8b908-590">"021", "21.0", "0021", "00021" dize "21", veya diğer büyük olasılıkla sonsuz Çeşitlemeler, yaş özelliği eşleşen herhangi bir belge ister, vb. eşlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="8b908-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="8b908-591">Buna karşılık toohello hello dize değerlerini örtük olarak Integer toonumbers nerede JavaScript budur (örneğin, operatöre dayanan: ==).</span><span class="sxs-lookup"><span data-stu-id="8b908-591">This is in contrast toohello JavaScript where hello string values are implicitly casted toonumbers (based on operator, ex: ==).</span></span> <span data-ttu-id="8b908-592">Bu seçenek, DocumentDB API SQL'de eşleşen verimli dizin için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="8b908-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="8b908-593">Parametreli SQL sorguları</span><span class="sxs-lookup"><span data-stu-id="8b908-593">Parameterized SQL queries</span></span>
<span data-ttu-id="8b908-594">Cosmos DB hello @ gösterimi tanıdık ile ifade parametrelerle sorguları destekler.</span><span class="sxs-lookup"><span data-stu-id="8b908-594">Cosmos DB supports queries with parameters expressed with hello familiar @ notation.</span></span> <span data-ttu-id="8b908-595">Parametreli SQL sağlam işleme ve kullanıcı girişi, SQL ekleme üzerinden veri yanlışlıkla açığa çıkmaya önleme, kaçış sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b908-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="8b908-596">Örneğin, Soyadı ve adres durumu kullandığı parametreler bir sorgu yazın ve son adı ve kullanıcı girişini temel alarak adresi durumunun çeşitli değerlerin yürütün.</span><span class="sxs-lookup"><span data-stu-id="8b908-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="8b908-597">Bu istek ardından aşağıda gösterildiği gibi tooCosmos DB parametreli bir JSON sorgu olarak gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-597">This request can then be sent tooCosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="8b908-598">Merhaba bağımsız değişkeni tooTOP gibi parametreli sorgular kullanmayı aşağıda gösterilen ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-598">hello argument tooTOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="8b908-599">Parametre değerleri geçerli bir JSON olabilir (dizeler, sayılar, Boole değerlerini, null, hatta dizileri veya JSON iç içe geçmiş).</span><span class="sxs-lookup"><span data-stu-id="8b908-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="8b908-600">Ayrıca parametreleri Cosmos DB Şeması daha az olduğundan, karşı herhangi bir tür doğrulanmaz.</span><span class="sxs-lookup"><span data-stu-id="8b908-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="8b908-601"><a id="BuiltinFunctions"></a>Yerleşik işlevler</span><span class="sxs-lookup"><span data-stu-id="8b908-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="8b908-602">Cosmos DB yerleşik işlevleri gibi kullanıcı tanımlı işlevler (UDF'ler) sorguları içinde kullanılan ortak işlemleri için de destekler.</span><span class="sxs-lookup"><span data-stu-id="8b908-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="8b908-603">İşlev grubu</span><span class="sxs-lookup"><span data-stu-id="8b908-603">Function group</span></span>          | <span data-ttu-id="8b908-604">İşlemler</span><span class="sxs-lookup"><span data-stu-id="8b908-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8b908-605">Matematik işlevleri</span><span class="sxs-lookup"><span data-stu-id="8b908-605">Mathematical functions</span></span>  | <span data-ttu-id="8b908-606">ABS TAVAN, EXP, FLOOR, günlük, LOG10, güç, HEPSİNİ, oturum, SQRT, KARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, derece, PI, radyan, SIN ve TAN</span><span class="sxs-lookup"><span data-stu-id="8b908-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="8b908-607">Denetimi işlevleri yazın</span><span class="sxs-lookup"><span data-stu-id="8b908-607">Type checking functions</span></span> | <span data-ttu-id="8b908-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED ve IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="8b908-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="8b908-609">Dize işlevleri</span><span class="sxs-lookup"><span data-stu-id="8b908-609">String functions</span></span>        | <span data-ttu-id="8b908-610">CONCAT, içerir, ENDSWITH, INDEX_OF, sol, uzunluk, alt, LTRIM, Değiştir, çoğaltılması, geriye doğru sağ, RTRIM, STARTSWITH, SUBSTRING ve üst</span><span class="sxs-lookup"><span data-stu-id="8b908-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="8b908-611">Dizi işlevleri</span><span class="sxs-lookup"><span data-stu-id="8b908-611">Array functions</span></span>         | <span data-ttu-id="8b908-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH ve ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="8b908-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="8b908-613">Uzamsal işlevleri</span><span class="sxs-lookup"><span data-stu-id="8b908-613">Spatial functions</span></span>       | <span data-ttu-id="8b908-614">St_dıstance, ST_WITHIN, ST_INTERSECTS, ST_ISVALID ve ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="8b908-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="8b908-615">Şu anda yerleşik işlevi olduğu şimdi kullanılabilir bir kullanıcı tanımlı işlev (UDF) kullanıyorsanız, toobe daha hızlı toorun ve daha fazlasını geçiyor gibi hello karşılık gelen yerleşik işlevi kullanmalıdır verimli bir şekilde.</span><span class="sxs-lookup"><span data-stu-id="8b908-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use hello corresponding built-in function as it is going toobe quicker toorun and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="8b908-616">Matematik işlevleri</span><span class="sxs-lookup"><span data-stu-id="8b908-616">Mathematical functions</span></span>
<span data-ttu-id="8b908-617">Merhaba matematik işlevleri her bağımsız değişken olarak sağlanır ve sayısal bir değeri döndürme giriş değerlerine göre bir hesaplama gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="8b908-617">hello mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="8b908-618">Burada, desteklenen yerleşik matematik işlevleri tablosu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8b908-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="8b908-619">Kullanım</span><span class="sxs-lookup"><span data-stu-id="8b908-619">Usage</span></span> | <span data-ttu-id="8b908-620">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b908-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8b908-621">[[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="8b908-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="8b908-622">Sayısal ifade döndürür hello mutlak (pozitif) değerini hello belirtildi.</span><span class="sxs-lookup"><span data-stu-id="8b908-622">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="8b908-623">Üst SINIRA (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="8b908-624">En küçük tamsayı değeri büyük hello veya belirtilen sayısal ifade hello eşit verir.</span><span class="sxs-lookup"><span data-stu-id="8b908-624">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| [<span data-ttu-id="8b908-625">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="8b908-626">Daha az Hello en büyük tamsayıyı döndürür veya bu değere eşit toohello sayısal ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="8b908-626">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| [<span data-ttu-id="8b908-627">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="8b908-628">Merhaba, döndürür hello üs sayısal ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="8b908-628">Returns hello exponent of hello specified numeric expression.</span></span> |
| <span data-ttu-id="8b908-629">[Günlük (num_expr [, temel])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="8b908-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="8b908-630">Sayısal ifade hello hello doğal logaritmasını döndürür belirtilen veya hello kullanarak hello logaritmanın tabanı belirtilen</span><span class="sxs-lookup"><span data-stu-id="8b908-630">Returns hello natural logarithm of hello specified numeric expression, or hello logarithm using hello specified base</span></span> |
| [<span data-ttu-id="8b908-631">Log10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="8b908-632">Merhaba, döndürür hello 10 tabanında Logaritmik değer sayısal ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="8b908-632">Returns hello base-10 logarithmic value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="8b908-633">ROUND (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="8b908-634">Yuvarlak toohello en yakın tamsayı değeri sayısal bir değer döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-634">Returns a numeric value, rounded toohello closest integer value.</span></span> |
| [<span data-ttu-id="8b908-635">TRUNC (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="8b908-636">Kesilmiş toohello en yakın tamsayı değeri sayısal bir değer döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-636">Returns a numeric value, truncated toohello closest integer value.</span></span> |
| [<span data-ttu-id="8b908-637">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="8b908-638">Merhaba hello kare kökünü döndürür sayısal ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="8b908-638">Returns hello square root of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="8b908-639">KARE (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="8b908-640">Merhaba kare döndürür hello sayısal ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="8b908-640">Returns hello square of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="8b908-641">GÜÇ (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="8b908-642">Sayısal ifade toohello değeri belirtilen döndürür hello hello gücünü belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="8b908-642">Returns hello power of hello specified numeric expression toohello value specified.</span></span> |
| [<span data-ttu-id="8b908-643">OTURUM (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="8b908-644">Döndürür hello oturum değerini (-1, 0, 1) hello sayısal ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="8b908-644">Returns hello sign value (-1, 0, 1) of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="8b908-645">ACOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="8b908-646">Kosinüsü belirtilen sayısal ifade hello radyan cinsinden döndürür hello açı; arccosine olarak da bilinir.</span><span class="sxs-lookup"><span data-stu-id="8b908-646">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="8b908-647">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="8b908-648">Döndürür hello açının sinüsü hello olduğundan, sayısal ifade radyan cinsinden.</span><span class="sxs-lookup"><span data-stu-id="8b908-648">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="8b908-649">Bu arksinüsünü olarak da adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="8b908-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="8b908-650">ATAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="8b908-651">Döndürür hello açının tanjantı hello olduğundan, sayısal ifade radyan cinsinden.</span><span class="sxs-lookup"><span data-stu-id="8b908-651">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="8b908-652">Bu arktanjantını olarak da adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="8b908-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="8b908-653">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="8b908-654">Döndürür hello hello pozitif x ekseni ve hello ray hello kaynak toohello noktasından (y, x) arasında radyan cinsinden açı burada x ve y hello hello iki belirtilen float ifadeleri değerleri.</span><span class="sxs-lookup"><span data-stu-id="8b908-654">Returns hello angle, in radians, between hello positive x-axis and hello ray from hello origin toohello point (y, x), where x and y are hello values of hello two specified float expressions.</span></span> |
| [<span data-ttu-id="8b908-655">COS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="8b908-656">Döndürür hello trigonometrik kosinüsünü hello radyan cinsinden açı, hello ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="8b908-656">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="8b908-657">COT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="8b908-658">Döndürür hello trigonometrik kotanjantını hello radyan cinsinden açı, hello sayısal ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="8b908-658">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span> |
| [<span data-ttu-id="8b908-659">DERECE (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="8b908-660">Karşılık gelen açıyı radyan cinsinden açı için derece cinsinden döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="8b908-660">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="8b908-661">PI)</span><span class="sxs-lookup"><span data-stu-id="8b908-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="8b908-662">PI sayısının sabit bir değer döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="8b908-662">Returns hello constant value of PI.</span></span> |
| [<span data-ttu-id="8b908-663">Radyan CİNSİNDEN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="8b908-664">Derece sayısal bir ifadenin girildiğinde radyan cinsinden döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="8b908-665">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="8b908-666">Döndürür hello trigonometrik sinüsünü hello radyan cinsinden açı, hello ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="8b908-666">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="8b908-667">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="8b908-668">Merhaba içinde hello giriş ifadesi döndürür hello tanjantını ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="8b908-668">Returns hello tangent of hello input expression, in hello specified expression.</span></span> |

<span data-ttu-id="8b908-669">Örneğin, şimdi sorguları hello aşağıdaki gibi çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8b908-669">For example, you can now run queries like hello following:</span></span>

<span data-ttu-id="8b908-670">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="8b908-671">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-671">**Results**</span></span>

    [4]

<span data-ttu-id="8b908-672">Cosmos veritabanı işlevleri karşılaştırıldığında tooANSI SQL arasındaki temel fark Hello bunlar iyi şema küçüktür ve karma şema verilerle tasarlanmış toowork olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="8b908-672">hello main difference between Cosmos DB’s functions compared tooANSI SQL is that they are designed toowork well with schema-less and mixed schema data.</span></span> <span data-ttu-id="8b908-673">Örneğin, burada hello boyut özelliği eksik veya sahip bir belgeniz varsa "bilinmiyor" gibi bir sayısal olmayan değer sonra hello belge üzerinde bir hata döndürüyor yerine atlanır.</span><span class="sxs-lookup"><span data-stu-id="8b908-673">For example, if you have a document where hello Size property is missing, or has a non-numeric value like “unknown”, then hello document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="8b908-674">Denetimi işlevleri yazın</span><span class="sxs-lookup"><span data-stu-id="8b908-674">Type checking functions</span></span>
<span data-ttu-id="8b908-675">Merhaba tür denetimi işlevleri içinde SQL sorguları ifade toocheck hello türü izin verin.</span><span class="sxs-lookup"><span data-stu-id="8b908-675">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span> <span data-ttu-id="8b908-676">Denetimi işlevleri olabilir türü değişken veya bilinmeyen olduğunda toodetermine hello türü belgelerde özelliklerinin hello anında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8b908-676">Type checking functions can be used toodetermine hello type of properties within documents on hello fly when it is variable or unknown.</span></span> <span data-ttu-id="8b908-677">Burada, desteklenen yerleşik tür işlevleri denetlemesini tablosu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8b908-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="8b908-678"><strong>Kullanım</strong></span><span class="sxs-lookup"><span data-stu-id="8b908-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="8b908-679"><strong>Açıklama</strong></span><span class="sxs-lookup"><span data-stu-id="8b908-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8b908-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (ifade)</a></span><span class="sxs-lookup"><span data-stu-id="8b908-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="8b908-681">Merhaba değerin Hello türü bir dizi olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-681">Returns a Boolean indicating if hello type of hello value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8b908-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (ifade)</a></span><span class="sxs-lookup"><span data-stu-id="8b908-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="8b908-683">Hello türde bir hello değer bir Boole değeri olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-683">Returns a Boolean indicating if hello type of hello value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8b908-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (ifade)</a></span><span class="sxs-lookup"><span data-stu-id="8b908-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="8b908-685">Merhaba değerin Hello türü null olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-685">Returns a Boolean indicating if hello type of hello value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8b908-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (ifade)</a></span><span class="sxs-lookup"><span data-stu-id="8b908-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="8b908-687">Hello türde bir hello değer bir sayı olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-687">Returns a Boolean indicating if hello type of hello value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8b908-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (ifade)</a></span><span class="sxs-lookup"><span data-stu-id="8b908-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="8b908-689">Merhaba değerin Hello türü bir JSON nesnesi olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-689">Returns a Boolean indicating if hello type of hello value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8b908-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (ifade)</a></span><span class="sxs-lookup"><span data-stu-id="8b908-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="8b908-691">Merhaba değerin Hello türü bir dize olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-691">Returns a Boolean indicating if hello type of hello value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8b908-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (ifade)</a></span><span class="sxs-lookup"><span data-stu-id="8b908-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="8b908-693">Başlangıç özellik değeri atanmış olan gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-693">Returns a Boolean indicating if hello property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8b908-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (ifade)</a></span><span class="sxs-lookup"><span data-stu-id="8b908-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="8b908-695">Merhaba değerin Hello türü bir dize, sayı, Boole veya null olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-695">Returns a Boolean indicating if hello type of hello value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="8b908-696">Bu işlevler kullanılarak, şimdi sorguları hello aşağıdaki gibi çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8b908-696">Using these functions, you can now run queries like hello following:</span></span>

<span data-ttu-id="8b908-697">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="8b908-698">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="8b908-699">Dize işlevleri</span><span class="sxs-lookup"><span data-stu-id="8b908-699">String functions</span></span>
<span data-ttu-id="8b908-700">Merhaba aşağıdaki skaler işlevler dize giriş değeri üzerinde bir işlemi gerçekleştirmek ve bir dize, sayısal ya da Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-700">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="8b908-701">Yerleşik dize işlevleri tablosu aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="8b908-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="8b908-702">Kullanım</span><span class="sxs-lookup"><span data-stu-id="8b908-702">Usage</span></span> | <span data-ttu-id="8b908-703">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b908-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="8b908-704">UZUNLUĞU (str_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="8b908-705">Dize ifadesi döndürür hello hello karakter sayısı belirtilen</span><span class="sxs-lookup"><span data-stu-id="8b908-705">Returns hello number of characters of hello specified string expression</span></span> |
| <span data-ttu-id="8b908-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="8b908-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="8b908-707">İki veya daha fazla dize değerlerini birleştirme hello sonucu olan bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-707">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="8b908-708">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="8b908-709">Bir dize ifadesi bölümünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="8b908-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="8b908-711">Merhaba ilk dize ifadesi ile Merhaba ikinci bitip olup olmadığını gösteren bir Boole değeri döndürür</span><span class="sxs-lookup"><span data-stu-id="8b908-711">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="8b908-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="8b908-713">Merhaba ilk dize ifadesi ile Merhaba ikinci bitip olup olmadığını gösteren bir Boole değeri döndürür</span><span class="sxs-lookup"><span data-stu-id="8b908-713">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="8b908-714">İÇERİR (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="8b908-715">Merhaba ilk dize ifadesi hello ikinci içerip içermediğini gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-715">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |
| [<span data-ttu-id="8b908-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="8b908-717">Merhaba dize bulunmazsa hello ikinci dize ifadesi hello ilk belirtilen dize ifadesi veya -1 içinde hello ilk oluşum konumunu başlangıç hello döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-717">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span> |
| [<span data-ttu-id="8b908-718">Sol (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="8b908-719">Döndürür hello sol bölümü bir dizenin belirtilen hello ile karakter sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b908-719">Returns hello left part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="8b908-720">SAĞ (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="8b908-721">Karakter sayısını döndürür hello dizesi sağ parçası hello ile belirtilen.</span><span class="sxs-lookup"><span data-stu-id="8b908-721">Returns hello right part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="8b908-722">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="8b908-723">Öndeki boşlukları kaldırır sonra bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="8b908-724">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="8b908-725">Tüm sondaki boşlukları kesilmesi sonrasında bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="8b908-726">Alt (str_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="8b908-727">Büyük harf karakter veri toolowercase dönüştürmeden sonra bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-727">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| [<span data-ttu-id="8b908-728">ÜST (str_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="8b908-729">Küçük harf karakter veri toouppercase dönüştürmeden sonra bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-729">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| [<span data-ttu-id="8b908-730">REPLACE (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="8b908-731">Belirtilen dize değeri tüm oluşumlarını başka bir dize değeri ile değiştirir.</span><span class="sxs-lookup"><span data-stu-id="8b908-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="8b908-732">REPLICATE (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="8b908-733">Bir dize değeri, belirtilen sayıda yineler.</span><span class="sxs-lookup"><span data-stu-id="8b908-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="8b908-734">Ters (str_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="8b908-735">Merhaba ters sırada bir dize değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-735">Returns hello reverse order of a string value.</span></span> |

<span data-ttu-id="8b908-736">Bu işlevleri kullanarak, artık hello aşağıdaki gibi sorguları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b908-736">Using these functions, you can now run queries like hello following.</span></span> <span data-ttu-id="8b908-737">Örneğin, size hello aile adı büyük şu şekilde döndürebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8b908-737">For example, you can return hello family name in uppercase as follows:</span></span>

<span data-ttu-id="8b908-738">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="8b908-739">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="8b908-740">Veya bu örnekteki gibi dizeyi birleştirmek:</span><span class="sxs-lookup"><span data-stu-id="8b908-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="8b908-741">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="8b908-742">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="8b908-743">Dize işlevleri, hello yan tümcesi toofilter sonuçları, aşağıdaki örneğine hello oluşturulacağı yeri de kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="8b908-743">String functions can also be used in hello WHERE clause toofilter results, like in hello following example:</span></span>

<span data-ttu-id="8b908-744">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="8b908-745">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="8b908-746">Dizi işlevleri</span><span class="sxs-lookup"><span data-stu-id="8b908-746">Array functions</span></span>
<span data-ttu-id="8b908-747">skaler işlevler aşağıdaki hello bir dizi giriş değeri ve return sayısal, Boole veya dizi değer üzerinde bir işlemi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="8b908-747">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="8b908-748">Yerleşik dizi işlevleri tablosu aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="8b908-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="8b908-749">Kullanım</span><span class="sxs-lookup"><span data-stu-id="8b908-749">Usage</span></span> | <span data-ttu-id="8b908-750">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8b908-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="8b908-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="8b908-752">Dizi ifadesi belirtilen döndürür hello hello öğelerinin sayısı.</span><span class="sxs-lookup"><span data-stu-id="8b908-752">Returns hello number of elements of hello specified array expression.</span></span> |
| <span data-ttu-id="8b908-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="8b908-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="8b908-754">İki veya daha fazla dizi değerlerini birleştirme hello sonucu olan bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-754">Returns an array that is hello result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="8b908-755">[ARRAY_CONTAINS (arr_expr, ifade [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="8b908-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="8b908-756">Belirtilen değer hello dizi hello içerip içermediğini gösteren Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-756">Returns a Boolean indicating whether hello array contains hello specified value.</span></span> <span data-ttu-id="8b908-757">Merhaba eşleşme tam veya kısmi olup olmadığını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b908-757">Can specify if hello match is full or partial.</span></span> |
| <span data-ttu-id="8b908-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="8b908-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="8b908-759">Bir dizi ifadesi bölümünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="8b908-760">Dizi işlevleri JSON içinde kullanılan toomanipulate diziler olabilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-760">Array functions can be used toomanipulate arrays within JSON.</span></span> <span data-ttu-id="8b908-761">Örneğin, "Deneme Wakefield" olduğu bir hello üst tüm belgeleri döndüren bir sorgu aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="8b908-761">For example, here's a query that returns all documents where one of hello parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="8b908-762">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="8b908-763">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="8b908-764">Merhaba dizi eşleşen öğeleri için kısmi bir parça belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b908-764">You can specify a partial fragment for matching elements within hello array.</span></span> <span data-ttu-id="8b908-765">Merhaba aşağıdaki sorgu bulur hello ile tüm üst `givenName` , `Robin`.</span><span class="sxs-lookup"><span data-stu-id="8b908-765">hello following query finds all parents with hello `givenName` of `Robin`.</span></span>

<span data-ttu-id="8b908-766">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="8b908-767">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="8b908-768">Burada, ARRAY_LENGTH tooget hello ailesi başına alt sayısını kullanan başka bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8b908-768">Here's another example that uses ARRAY_LENGTH tooget hello number of children per family.</span></span>

<span data-ttu-id="8b908-769">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="8b908-770">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="8b908-771">Uzamsal işlevleri</span><span class="sxs-lookup"><span data-stu-id="8b908-771">Spatial functions</span></span>
<span data-ttu-id="8b908-772">Cosmos DB Jeo-uzamsal sorgulamak için yerleşik işlevler açık Jeo-uzamsal Konsorsiyumu (OGC) aşağıdaki hello destekler.</span><span class="sxs-lookup"><span data-stu-id="8b908-772">Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="8b908-773"><strong>Kullanım</strong></span><span class="sxs-lookup"><span data-stu-id="8b908-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="8b908-774"><strong>Açıklama</strong></span><span class="sxs-lookup"><span data-stu-id="8b908-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8b908-775">St_dıstance (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="8b908-776">Merhaba iki GeoJSON noktası, çokgen veya LineString ifadeleri arasında Hello uzaklığını döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-776">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8b908-777">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="8b908-778">Merhaba ilk GeoJSON nesne (noktası, çokgen veya LineString) hello ikinci GeoJSON nesne içinde (noktası, çokgen veya LineString) olup olmadığını gösteren bir Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-778">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8b908-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="8b908-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="8b908-780">Merhaba iki belirtilen GeoJSON nesne (noktası, çokgen veya LineString) kesiştiği olup olmadığını gösteren bir Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-780">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8b908-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="8b908-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="8b908-782">Merhaba GeoJSON noktası, çokgen veya LineString ifadesi geçerli belirtilen olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-782">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8b908-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="8b908-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="8b908-784">Merhaba GeoJSON noktası, çokgen veya LineString ifade belirtilmişse bir Boole değeri içeren bir JSON değeri geçerli değil ve geçersiz, ayrıca bir dize değeri olarak neden hello döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-784">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="8b908-785">Uzamsal işlevleri kullanılan tooperform yakınlık sorguları uzamsal veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-785">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="8b908-786">Örneğin, tüm ailesi hello st_dıstance yerleşik işlevi belirtilen konum içinde 30 km hello birini kullanarak belgeleri döndüren bir sorgu aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="8b908-786">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="8b908-787">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="8b908-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="8b908-788">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="8b908-789">Cosmos DB Jeo-uzamsal desteği hakkında daha fazla ayrıntı için lütfen bkz. [Azure Cosmos veritabanı Jeo-uzamsal verilerle çalışma](geospatial.md).</span><span class="sxs-lookup"><span data-stu-id="8b908-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="8b908-790">Cosmos DB için uzamsal işlevleri ve hello SQL söz dizimi, sarmalar.</span><span class="sxs-lookup"><span data-stu-id="8b908-790">That wraps up spatial functions, and hello SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="8b908-791">Şimdi nasıl çalışır ve hello sözdizimi ile nasıl etkileşim kurduğu sorgulama LINQ kadarki gördük bir bakalım.</span><span class="sxs-lookup"><span data-stu-id="8b908-791">Now let's take a look at how LINQ querying works and how it interacts with hello syntax we've seen so far.</span></span>

## <span data-ttu-id="8b908-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span><span class="sxs-lookup"><span data-stu-id="8b908-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span></span>
<span data-ttu-id="8b908-793">LINQ, hesaplama nesnelerin akışları sorgular olarak ifade eder ve .NET çalışan bir programlama modelidir.</span><span class="sxs-lookup"><span data-stu-id="8b908-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="8b908-794">JSON ve .NET nesneleri arasında dönüştürme kolaylaştırarak LINQ ile bir istemci-tarafı kitaplığı toointerface cosmos DB sağlar ve bir alt kümesini LINQ eşlemesinden tooCosmos DB sorguları.</span><span class="sxs-lookup"><span data-stu-id="8b908-794">Cosmos DB provides a client-side library toointerface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries tooCosmos DB queries.</span></span> 

<span data-ttu-id="8b908-795">Merhaba resimde Cosmos DB kullanarak LINQ sorgularını destekleme hello mimari gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8b908-795">hello picture below shows hello architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="8b908-796">Merhaba Cosmos DB İstemcisi'ni kullanarak geliştiriciler oluşturabilir bir **Iqueryable** Cosmos DB sorgu sağlayıcısı sorguları hello doğrudan o hello LINQ sorgusu Cosmos DB sorguda çevirir, nesne.</span><span class="sxs-lookup"><span data-stu-id="8b908-796">Using hello Cosmos DB client, developers can create an **IQueryable** object that directly queries hello Cosmos DB query provider, which then translates hello LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="8b908-797">Merhaba sorgu daha sonra JSON biçiminde toohello Cosmos DB sunucusu tooretrieve sonuç kümesi geçirilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-797">hello query is then passed toohello Cosmos DB server tooretrieve a set of results in JSON format.</span></span> <span data-ttu-id="8b908-798">Merhaba, sonuçları hello istemci tarafında .NET nesnelerin bir akışa seri durumdan çıkarılmış döndürdü.</span><span class="sxs-lookup"><span data-stu-id="8b908-798">hello returned results are deserialized into a stream of .NET objects on hello client side.</span></span>

![DocumentDB API - kullanarak LINQ sorgularını SQL söz dizimi, JSON sorgu dili, veritabanı kavramlarını ve SQL sorguları destekleyen mimarisi][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="8b908-800">.NET ve JSON eşleme</span><span class="sxs-lookup"><span data-stu-id="8b908-800">.NET and JSON mapping</span></span>
<span data-ttu-id="8b908-801">.NET nesneleri ve JSON belgeleri arasında Hello eşleme doğal - her bir veri üyesi alanına eşlenen hello alan adı olduğu tooa JSON nesnesi eşlenen toohello "anahtarı" Merhaba nesnesinin bir parçası ve Başlangıç "değeri" parçasıdır eşlenen yinelemeli olarak toohello değeri hello nesnesinin bir parçası.</span><span class="sxs-lookup"><span data-stu-id="8b908-801">hello mapping between .NET objects and JSON documents is natural - each data member field is mapped tooa JSON object, where hello field name is mapped toohello "key" part of hello object and hello "value" part is recursively mapped toohello value part of hello object.</span></span> <span data-ttu-id="8b908-802">Aşağıdaki örnek hello göz önünde bulundurun: oluşturulan hello ailesi nesnesidir eşlenen toohello JSON belgesi aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="8b908-802">Consider hello following example: hello Family object created is mapped toohello JSON document as shown below.</span></span> <span data-ttu-id="8b908-803">Ve tersi yönde hello JSON belgesi eşlenen geri tooa .NET nesnedir.</span><span class="sxs-lookup"><span data-stu-id="8b908-803">And vice versa, hello JSON document is mapped back tooa .NET object.</span></span>

<span data-ttu-id="8b908-804">**C# sınıfı**</span><span class="sxs-lookup"><span data-stu-id="8b908-804">**C# Class**</span></span>

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


<span data-ttu-id="8b908-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="8b908-805">**JSON**</span></span>  

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



### <a name="linq-toosql-translation"></a><span data-ttu-id="8b908-806">LINQ tooSQL çevirisi</span><span class="sxs-lookup"><span data-stu-id="8b908-806">LINQ tooSQL translation</span></span>
<span data-ttu-id="8b908-807">Merhaba Cosmos DB sorgu sağlayıcısı en iyi çaba eşleme Cosmos DB SQL sorgusu bir LINQ Sorgu gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="8b908-807">hello Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="8b908-808">Açıklama aşağıdaki hello hello okuyucu LINQ temel bilgisi içeriyor varsayalım.</span><span class="sxs-lookup"><span data-stu-id="8b908-808">In hello following description, we assume hello reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="8b908-809">İlk olarak, hello tür sistemi için tüm JSON ilkel türler – sayısal türler, boolean, dize ve null destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="8b908-809">First, for hello type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="8b908-810">Yalnızca bu JSON türleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8b908-810">Only these JSON types are supported.</span></span> <span data-ttu-id="8b908-811">skaler ifadelerin aşağıdaki hello desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8b908-811">hello following scalar expressions are supported.</span></span>

* <span data-ttu-id="8b908-812">Sabit değerler – bunlar hello sorgu değerlendirilir hello zamanında hello temel veri türlerinin sabit değerleri içerir.</span><span class="sxs-lookup"><span data-stu-id="8b908-812">Constant values – these include constant values of hello primitive data types at hello time hello query is evaluated.</span></span>
* <span data-ttu-id="8b908-813">Özellik/dizi dizini ifadeleri – bu ifadeler toohello özelliğinin bir nesneyi veya bir dizi öğesine bakın.</span><span class="sxs-lookup"><span data-stu-id="8b908-813">Property/array index expressions – these expressions refer toohello property of an object or an array element.</span></span>
  
     <span data-ttu-id="8b908-814">ailesi. Kimliği;    Family.Children[0].familyName;    Family.Children[0].grade;    Family.Children[n].grade; n bir int değişkenidir</span><span class="sxs-lookup"><span data-stu-id="8b908-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="8b908-815">Aritmetik ifadeler - bunlar ortak aritmetik ifadeler sayısal ve Boole değerleri içerir.</span><span class="sxs-lookup"><span data-stu-id="8b908-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="8b908-816">Merhaba tam listesi için toohello SQL belirtimine bakın.</span><span class="sxs-lookup"><span data-stu-id="8b908-816">For hello complete list, refer toohello SQL specification.</span></span>
  
     <span data-ttu-id="8b908-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="8b908-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="8b908-818">Dize karşılaştırma ifadesi - bunlar bir dize değeri toosome sabit dize değeri karşılaştırma içerir.</span><span class="sxs-lookup"><span data-stu-id="8b908-818">String comparison expression - these include comparing a string value toosome constant string value.</span></span>  
  
     <span data-ttu-id="8b908-819">mother.familyName == "Smith";    child.givenName s; == bir dize değişkeni s'dir</span><span class="sxs-lookup"><span data-stu-id="8b908-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="8b908-820">Nesne/oluşturma ifadesi - dönüş Bu deyimler bileşik değer türü veya anonim tür bir nesneyi veya bir dizi tür nesneler dizisi.</span><span class="sxs-lookup"><span data-stu-id="8b908-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="8b908-821">Bu değerleri iç içe.</span><span class="sxs-lookup"><span data-stu-id="8b908-821">These values can be nested.</span></span>
  
     <span data-ttu-id="8b908-822">Yeni üst {familyName givenName "Smith" = "Can" =}; Yeni {ilk = 1, ikincisi 2 =}; iki alan sahip anonim bir tür</span><span class="sxs-lookup"><span data-stu-id="8b908-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="8b908-823">Yeni int [] {3, child.grade, 5};</span><span class="sxs-lookup"><span data-stu-id="8b908-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="8b908-824"><a id="SupportedLinqOperators"></a>Desteklenen LINQ işleçlerin listesi</span><span class="sxs-lookup"><span data-stu-id="8b908-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="8b908-825">Merhaba LINQ sağlayıcısında hello DocumentDB .NET SDK'sı ile dahil desteklenen LINQ işleçlerin bir listesi aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8b908-825">Here is a list of supported LINQ operators in hello LINQ provider included with hello DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="8b908-826">**Seçin**: tahminleri Çevir toohello SQL nesne oluşturması dahil olmak üzere seçin</span><span class="sxs-lookup"><span data-stu-id="8b908-826">**Select**: Projections translate toohello SQL SELECT including object construction</span></span>
* <span data-ttu-id="8b908-827">**Burada**: filtreleri SQL WHERE toohello çevirin ve Destek arasında çeviri & &, || ve!</span><span class="sxs-lookup"><span data-stu-id="8b908-827">**Where**: Filters translate toohello SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="8b908-828">toohello SQL işleçleri</span><span class="sxs-lookup"><span data-stu-id="8b908-828">toohello SQL operators</span></span>
* <span data-ttu-id="8b908-829">**SelectMany**: diziler toohello SQL JOIN yan tümcesinde geriye doğru izleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b908-829">**SelectMany**: Allows unwinding of arrays toohello SQL JOIN clause.</span></span> <span data-ttu-id="8b908-830">Dizi öğeleri üzerinde kullanılan toochain/nest ifadeleri toofilter olabilir</span><span class="sxs-lookup"><span data-stu-id="8b908-830">Can be used toochain/nest expressions toofilter on array elements</span></span>
* <span data-ttu-id="8b908-831">**OrderBy ve OrderByDescending**: tooORDER BY artan/azalan çevirir</span><span class="sxs-lookup"><span data-stu-id="8b908-831">**OrderBy and OrderByDescending**: Translates tooORDER BY ascending/descending</span></span>
* <span data-ttu-id="8b908-832">**Count**, **toplam**, **Min**, **Max**, ve **ortalama** toplama ve zaman uyumsuz eşdeğerlerine işleçleri **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, ve **AverageAsync**.</span><span class="sxs-lookup"><span data-stu-id="8b908-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="8b908-833">**CompareTo**: toorange karşılaştırmaları çevirir.</span><span class="sxs-lookup"><span data-stu-id="8b908-833">**CompareTo**: Translates toorange comparisons.</span></span> <span data-ttu-id="8b908-834">.NET ile karşılaştırılabilir değilseniz bu yana dizeleri için yaygın olarak kullanılan</span><span class="sxs-lookup"><span data-stu-id="8b908-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="8b908-835">**Ele**: toohello SQL üst bir sorgunun sonuçlarına sınırlamak için çevirir.</span><span class="sxs-lookup"><span data-stu-id="8b908-835">**Take**: Translates toohello SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="8b908-836">**Matematik işlevleri**: çevrilmesi destekler. NET'in Abs, Acos, Asin Cos tavan Atan Exp, Floor, günlük, Log10, Pow, hepsini, oturum, Sin, Sqrt, Tan, Truncate toohello eşdeğer SQL yerleşik işlevleri.</span><span class="sxs-lookup"><span data-stu-id="8b908-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="8b908-837">**Dize işlevleri**: çevrilmesi destekler. NET'in Concat, içerir, EndsWith, IndexOf, Count, ToLower, TrimStart, Değiştir, tersine, TrimEnd, StartsWith, SubString, ToUpper toohello eşdeğer SQL yerleşik işlevler.</span><span class="sxs-lookup"><span data-stu-id="8b908-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="8b908-838">**Dizi işlevleri**: çevrilmesi destekler. NET'in Concat, içerir ve sayısı toohello eşdeğer SQL yerleşik işlevler.</span><span class="sxs-lookup"><span data-stu-id="8b908-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="8b908-839">**Jeo-uzamsal uzantı işlevleri**: saplama yöntemlerden içinde IsValid, uzaklığı çeviri destekler ve IsValidDetailed toohello eşdeğer SQL yerleşik işlevleri.</span><span class="sxs-lookup"><span data-stu-id="8b908-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="8b908-840">**Kullanıcı tanımlı işlev uzantı işlevi**: hello destekler çevrilmesi saplama yöntemi UserDefinedFunctionProvider.Invoke toohello karşılık gelen kullanıcı tanımlı işlev.</span><span class="sxs-lookup"><span data-stu-id="8b908-840">**User-Defined Function Extension Function**: Supports translation from hello stub method UserDefinedFunctionProvider.Invoke toohello corresponding user-defined function.</span></span>
* <span data-ttu-id="8b908-841">**Çeşitli**: koşullu işleçler ve hello çevrilmesi birleşim destekler.</span><span class="sxs-lookup"><span data-stu-id="8b908-841">**Miscellaneous**: Supports translation of hello coalesce and conditional operators.</span></span> <span data-ttu-id="8b908-842">CONTAINS tooString çevirebilir içerir, ARRAY_CONTAINS veya hello SQL IN bağlamı bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="8b908-842">Can translate Contains tooString CONTAINS, ARRAY_CONTAINS, or hello SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="8b908-843">SQL sorgu işleçleri</span><span class="sxs-lookup"><span data-stu-id="8b908-843">SQL query operators</span></span>
<span data-ttu-id="8b908-844">Aşağıda, bazı hello standart LINQ Sorgu işleçleri tooCosmos DB sorguları nasıl dönüştürüleceğini gösteren bazı örnekler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8b908-844">Here are some examples that illustrate how some of hello standard LINQ query operators are translated down tooCosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="8b908-845">İşleç Seç</span><span class="sxs-lookup"><span data-stu-id="8b908-845">Select Operator</span></span>
<span data-ttu-id="8b908-846">Merhaba sözdizimi `input.Select(x => f(x))`, burada `f` skaler bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="8b908-846">hello syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="8b908-847">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="8b908-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="8b908-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="8b908-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="8b908-849">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="8b908-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="8b908-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="8b908-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="8b908-851">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="8b908-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="8b908-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="8b908-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="8b908-853">SelectMany işleci</span><span class="sxs-lookup"><span data-stu-id="8b908-853">SelectMany operator</span></span>
<span data-ttu-id="8b908-854">Merhaba sözdizimi `input.SelectMany(x => f(x))`, burada `f` koleksiyon türü döndüren bir skaler ifade.</span><span class="sxs-lookup"><span data-stu-id="8b908-854">hello syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="8b908-855">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="8b908-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="8b908-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="8b908-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="8b908-857">Burada işleci</span><span class="sxs-lookup"><span data-stu-id="8b908-857">Where operator</span></span>
<span data-ttu-id="8b908-858">Merhaba sözdizimi `input.Where(x => f(x))`, burada `f` bir Boole değeri döndürür skaler bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="8b908-858">hello syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="8b908-859">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="8b908-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="8b908-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="8b908-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="8b908-861">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="8b908-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="8b908-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="8b908-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="8b908-863">Bileşik SQL sorguları</span><span class="sxs-lookup"><span data-stu-id="8b908-863">Composite SQL queries</span></span>
<span data-ttu-id="8b908-864">Hello işleçleri yukarıda oluşturulan tooform daha güçlü sorgular olabilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-864">hello above operators can be composed tooform more powerful queries.</span></span> <span data-ttu-id="8b908-865">Cosmos DB iç içe geçmiş koleksiyonları desteklediğinden hello birleşim birleştirilmiş iç içe geçmiş ya da.</span><span class="sxs-lookup"><span data-stu-id="8b908-865">Since Cosmos DB supports nested collections, hello composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="8b908-866">Birleştirme</span><span class="sxs-lookup"><span data-stu-id="8b908-866">Concatenation</span></span>
<span data-ttu-id="8b908-867">Merhaba sözdizimi `input(.|.SelectMany())(.Select()|.Where())*`.</span><span class="sxs-lookup"><span data-stu-id="8b908-867">hello syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="8b908-868">Birleştirilmiş bir sorgu ile isteğe bağlı başlatabilirsiniz `SelectMany` sorgu birden fazla ardından `Select` veya `Where` işleçler.</span><span class="sxs-lookup"><span data-stu-id="8b908-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="8b908-869">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="8b908-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="8b908-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="8b908-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="8b908-871">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="8b908-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="8b908-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="8b908-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="8b908-873">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="8b908-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="8b908-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="8b908-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="8b908-875">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="8b908-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="8b908-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="8b908-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="8b908-877">İç içe geçme</span><span class="sxs-lookup"><span data-stu-id="8b908-877">Nesting</span></span>
<span data-ttu-id="8b908-878">Merhaba sözdizimi `input.SelectMany(x=>x.Q())` Q olduğu bir `Select`, `SelectMany`, veya `Where` işleci.</span><span class="sxs-lookup"><span data-stu-id="8b908-878">hello syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="8b908-879">İç içe bir sorgu hello iç sorgu uygulanan tooeach hello dış toplama öğesidir.</span><span class="sxs-lookup"><span data-stu-id="8b908-879">In a nested query, hello inner query is applied tooeach element of hello outer collection.</span></span> <span data-ttu-id="8b908-880">Bir önemli özelliği hello iç sorgu toohello alanları gibi hello dış koleksiyonundaki hello öğelerinin başvuruda bulunabilir kendi kendine birleştirir.</span><span class="sxs-lookup"><span data-stu-id="8b908-880">One important feature is that hello inner query can refer toohello fields of hello elements in hello outer collection like self-joins.</span></span>

<span data-ttu-id="8b908-881">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="8b908-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="8b908-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="8b908-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="8b908-883">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="8b908-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="8b908-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="8b908-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="8b908-885">**LINQ lambda ifadesi**</span><span class="sxs-lookup"><span data-stu-id="8b908-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="8b908-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="8b908-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="8b908-887"><a id="ExecutingSqlQueries"></a>SQL sorguları yürütme</span><span class="sxs-lookup"><span data-stu-id="8b908-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="8b908-888">Cosmos DB herhangi bir dil tarafından HTTP/HTTPS istekleri çağrılabilir bir REST API'si aracılığıyla kaynaklarını kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="8b908-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="8b908-889">Ayrıca, Cosmos DB .NET, Node.js, JavaScript ve Python gibi çeşitli popüler dilde programlama kitaplıkları sunar.</span><span class="sxs-lookup"><span data-stu-id="8b908-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="8b908-890">Merhaba REST API ve hello tüm çeşitli kitaplıkları SQL sorgulama destekler.</span><span class="sxs-lookup"><span data-stu-id="8b908-890">hello REST API and hello various libraries all support querying through SQL.</span></span> <span data-ttu-id="8b908-891">Merhaba .NET SDK ayrıca tooSQL sorgulama LINQ destekler.</span><span class="sxs-lookup"><span data-stu-id="8b908-891">hello .NET SDK supports LINQ querying in addition tooSQL.</span></span>

<span data-ttu-id="8b908-892">örneklerde nasıl aşağıdaki hello toocreate bir sorgu ve Cosmos DB veritabanı hesabı karşı gönderin.</span><span class="sxs-lookup"><span data-stu-id="8b908-892">hello following examples show how toocreate a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="8b908-893"><a id="RestAPI"></a>REST API'Sİ</span><span class="sxs-lookup"><span data-stu-id="8b908-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="8b908-894">Cosmos DB HTTP üzerinden açık bir RESTful programlama modeli sunar.</span><span class="sxs-lookup"><span data-stu-id="8b908-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="8b908-895">Bir Azure aboneliği kullanarak veritabanı hesaplarını sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="8b908-896">Merhaba Cosmos DB kaynak modeli kaynaklar her biri mantıksal ve kararlı bir URI kullanılarak adreslenebilir bir veritabanı hesabı altında bir dizi oluşur.</span><span class="sxs-lookup"><span data-stu-id="8b908-896">hello Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="8b908-897">Başvurulan tooas bu belgede bir akış kaynakları kümesidir.</span><span class="sxs-lookup"><span data-stu-id="8b908-897">A set of resources is referred tooas a feed in this document.</span></span> <span data-ttu-id="8b908-898">Veritabanı hesabı her birden çok koleksiyonu kapsayan bir veritabanları kümesi oluşur belgeleri, UDF'ler ve diğer kaynak türlerini her hangi içinde dönüş içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="8b908-899">Hello temel etkileşim bu kaynaklarla hello HTTP fiilleri GET, PUT, POST ve silme ile standart kullanıcıların yorumu modelidir.</span><span class="sxs-lookup"><span data-stu-id="8b908-899">hello basic interaction model with these resources is through hello HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="8b908-900">Merhaba POST fiil yeni bir kaynak oluşturulmasını, bir saklı yordamı yürütmek veya Cosmos DB sorgu verme için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8b908-900">hello POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="8b908-901">Sorguları her zaman salt okunur hiçbir yan etkileri olan işlemleridir.</span><span class="sxs-lookup"><span data-stu-id="8b908-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="8b908-902">Merhaba Aşağıdaki örnekler biz kadarki geçirdikten hello iki örnek belgeleri içeren bir koleksiyon karşı yapılan bir DocumentDB API sorgu için bir POST gösterir.</span><span class="sxs-lookup"><span data-stu-id="8b908-902">hello following examples show a POST for a DocumentDB API query made against a collection containing hello two sample documents we've reviewed so far.</span></span> <span data-ttu-id="8b908-903">Merhaba sorgu hello JSON name özelliğine göre basit bir filtre yok.</span><span class="sxs-lookup"><span data-stu-id="8b908-903">hello query has a simple filter on hello JSON name property.</span></span> <span data-ttu-id="8b908-904">Not hello hello `x-ms-documentdb-isquery` ve Content-Type: `application/query+json` işlemi hello üstbilgileri toodenote olan bir sorgu.</span><span class="sxs-lookup"><span data-stu-id="8b908-904">Note hello use of hello `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers toodenote that hello operation is a query.</span></span>

<span data-ttu-id="8b908-905">**İstek**</span><span class="sxs-lookup"><span data-stu-id="8b908-905">**Request**</span></span>

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


<span data-ttu-id="8b908-906">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-906">**Results**</span></span>

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


<span data-ttu-id="8b908-907">Merhaba ikinci örneği birden çok sonuç hello birleştirme sonucu döndürür daha karmaşık bir sorgu gösterir.</span><span class="sxs-lookup"><span data-stu-id="8b908-907">hello second example shows a more complex query that returns multiple results from hello join.</span></span>

<span data-ttu-id="8b908-908">**İstek**</span><span class="sxs-lookup"><span data-stu-id="8b908-908">**Request**</span></span>

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


<span data-ttu-id="8b908-909">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="8b908-909">**Results**</span></span>

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


<span data-ttu-id="8b908-910">Bir sorgunun sonuçları sonuçlar tek sayfalık içinde sığamıyorsa sonra hello REST API aracılığıyla hello devamlılık belirteci döndürür `x-ms-continuation-token` yanıtı üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="8b908-910">If a query's results cannot fit within a single page of results, then hello REST API returns a continuation token through hello `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="8b908-911">İstemcileri sonraki sonuçlarında hello üstbilgi dahil olmak üzere sonuçları sayfalara bölme.</span><span class="sxs-lookup"><span data-stu-id="8b908-911">Clients can paginate results by including hello header in subsequent results.</span></span> <span data-ttu-id="8b908-912">Sayfa başına sonuç Hello sayısı hello da denetlenebilir `x-ms-max-item-count` numara üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="8b908-912">hello number of results per page can also be controlled through hello `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="8b908-913">Belirtilen sorgu Hello gibi bir toplama işlevi varsa `COUNT`, hello sorgu sayfası kısmen toplu değer sonuç hello sayfasını döndürebilir sonra.</span><span class="sxs-lookup"><span data-stu-id="8b908-913">If hello specified query has an aggregation function like `COUNT`, then hello query page may return a partially aggregated value over hello page of results.</span></span> <span data-ttu-id="8b908-914">Merhaba istemcileri, bu sonuçları tooproduce hello son sonuçları, örneğin üzerinden ikinci düzey toplama gerçekleştirmek, hello tek tek sayfaları tooreturn hello toplam sayısı döndürülen hello sayıları üzerinden toplayın.</span><span class="sxs-lookup"><span data-stu-id="8b908-914">hello clients must perform a second-level aggregation over these results tooproduce hello final results, for example, sum over hello counts returned in hello individual pages tooreturn hello total count.</span></span>

<span data-ttu-id="8b908-915">sorguları, kullanım hello için toomanage hello veri tutarlılığı İlkesi `x-ms-consistency-level` tüm REST API istekleri gibi üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="8b908-915">toomanage hello data consistency policy for queries, use hello `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="8b908-916">Oturum tutarlılığı için gerekli tooalso echo hello son olmasından `x-ms-session-token` hello sorgu isteği, tanımlama bilgisi üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="8b908-916">For session consistency, it is required tooalso echo hello latest `x-ms-session-token` Cookie header in hello query request.</span></span> <span data-ttu-id="8b908-917">Merhaba sorgulanan koleksiyonunun dizin oluşturma ilkesini de sorgu sonuçları hello tutarlılığını etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-917">hello queried collection's indexing policy can also influence hello consistency of query results.</span></span> <span data-ttu-id="8b908-918">Merhaba varsayılan dizin oluşturma ilkesi ayarları, koleksiyonlar için hello her zaman geçerli hello belge içeriklerini ve sorgu sonuçları için veri seçilen hello tutarlılık eşleşen dizinidir.</span><span class="sxs-lookup"><span data-stu-id="8b908-918">With hello default indexing policy settings, for collections hello index is always current with hello document contents and query results match hello consistency chosen for data.</span></span> <span data-ttu-id="8b908-919">Dizin oluşturma ilkesi hello gevşek tooLazy ise, sorgular eski sonuçlar döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-919">If hello indexing policy is relaxed tooLazy, then queries can return stale results.</span></span> <span data-ttu-id="8b908-920">Daha fazla bilgi için bkz: [Azure Cosmos DB tutarlılık düzeylerini][consistency-levels].</span><span class="sxs-lookup"><span data-stu-id="8b908-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="8b908-921">Yapılandırılmış hello dizin oluşturma ilkesini hello koleksiyonunda hello belirtilen sorgu destekleyemiyorsa, 400 "hatalı istek" Merhaba Azure Cosmos DB sunucusu döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b908-921">If hello configured indexing policy on hello collection cannot support hello specified query, hello Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="8b908-922">Bu karma (eşitlik) aramaları için ve dizine almasını açıkça yolları için yapılandırılmış yolları aralığı sorguları için döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8b908-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="8b908-923">Merhaba `x-ms-documentdb-query-enable-scan` bir dizini olmadığında belirtilen tooallow hello sorgu tooperform bir tarama üstbilgisi olabilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-923">hello `x-ms-documentdb-query-enable-scan` header can be specified tooallow hello query tooperform a scan when an index is not available.</span></span>

<span data-ttu-id="8b908-924">Ayrıntılı ölçümler ayarlayarak sorgu yürütme elde edebilirsiniz `x-ms-documentdb-populatequerymetrics` üstbilgisi çok`True`.</span><span class="sxs-lookup"><span data-stu-id="8b908-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header too`True`.</span></span> <span data-ttu-id="8b908-925">Daha fazla bilgi için bkz: [SQL sorgu ölçümleri Azure Cosmos DB DocumentDB API'si](documentdb-sql-query-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="8b908-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="8b908-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span><span class="sxs-lookup"><span data-stu-id="8b908-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="8b908-927">LINQ ve SQL Hello .NET SDK'yı destekleyen sorgulama.</span><span class="sxs-lookup"><span data-stu-id="8b908-927">hello .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="8b908-928">Merhaba aşağıdaki örnekte nasıl tooperform hello basit filtre sorgusu bu belgenin önceki bölümlerinde sunulan gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8b908-928">hello following example shows how tooperform hello simple filter query introduced earlier in this document.</span></span>

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


<span data-ttu-id="8b908-929">Bu örnek her belge içinde eşitlik için iki özellik karşılaştırır ve anonim tahminleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="8b908-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

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


<span data-ttu-id="8b908-930">Merhaba sonraki örnek LINQ SelectMany ifade birleştirmeler gösterir.</span><span class="sxs-lookup"><span data-stu-id="8b908-930">hello next sample shows joins, expressed through LINQ SelectMany.</span></span>

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



<span data-ttu-id="8b908-931">Merhaba .NET istemci otomatik olarak yukarıda gösterildiği gibi hello foreach blokları sorgu sonuçlarında tüm hello sayfalarında dolaşır.</span><span class="sxs-lookup"><span data-stu-id="8b908-931">hello .NET client automatically iterates through all hello pages of query results in hello foreach blocks as shown above.</span></span> <span data-ttu-id="8b908-932">Merhaba REST API bölümünde sunulan seçenekleri kullanılabilir ayrıca hello sorgu hello hello kullanarak .NET SDK'SININ `FeedOptions` ve `FeedResponse` hello CreateDocumentQuery yöntemi sınıflarda.</span><span class="sxs-lookup"><span data-stu-id="8b908-932">hello query options introduced in hello REST API section are also available in hello .NET SDK using hello `FeedOptions` and `FeedResponse` classes in hello CreateDocumentQuery method.</span></span> <span data-ttu-id="8b908-933">Sayfa sayısı Hello hello kullanılarak denetlenebilir `MaxItemCount` ayarı.</span><span class="sxs-lookup"><span data-stu-id="8b908-933">hello number of pages can be controlled using hello `MaxItemCount` setting.</span></span> 

<span data-ttu-id="8b908-934">Disk belleği oluşturarak açıkça kontrol edebilirsiniz `IDocumentQueryable` hello kullanarak `IQueryable` okuyarak ardından nesne` ResponseContinuationToken` değerleri ve bunları geçirme geri olarak `RequestContinuationToken` içinde `FeedOptions`.</span><span class="sxs-lookup"><span data-stu-id="8b908-934">You can also explicitly control paging by creating `IDocumentQueryable` using hello `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="8b908-935">`EnableScanInQuery`Merhaba sorgu yapılandırılmış hello dizin oluşturma ilkesi tarafından desteklendiğinde kümesi tooenable taramaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-935">`EnableScanInQuery` can be set tooenable scans when hello query cannot be supported by hello configured indexing policy.</span></span> <span data-ttu-id="8b908-936">Bölümlenmiş koleksiyonlar için kullandığınız `PartitionKey` toorun hello sorgusu tek bir bölüm (Cosmos DB otomatik olarak bu hello sorgu metinden ayıklayabilirsiniz rağmen), ve `EnableCrossPartitionQuery` toobe gerekebilir toorun sorgularını kullanarak birden çok bölüm karşı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b908-936">For partitioned collections, you can use `PartitionKey` toorun hello query against a single partition (though Cosmos DB can automatically extract this from hello query text), and `EnableCrossPartitionQuery` toorun queries that may need toobe run against multiple partitions.</span></span> 

<span data-ttu-id="8b908-937">Çok başvuran[Azure Cosmos DB .NET örnekleri](https://github.com/Azure/azure-documentdb-net) sorguları içeren daha fazla örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="8b908-937">Refer too[Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="8b908-938"><a id="JavaScriptServerSideApi"></a>JavaScript sunucu tarafı API</span><span class="sxs-lookup"><span data-stu-id="8b908-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="8b908-939">Cosmos DB doğrudan saklı yordamları ve Tetikleyicileri kullanarak hello koleksiyonlar üzerinde temel JavaScript uygulama mantığının yürütmek için bir programlama modeli sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b908-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections using stored procedures and triggers.</span></span> <span data-ttu-id="8b908-940">bir koleksiyon düzeyinde kayıtlı hello JavaScript mantığı, ardından koleksiyonu verilen hello hello işlemlerini hello belgelerde veritabanı işlemlerini verebilir.</span><span class="sxs-lookup"><span data-stu-id="8b908-940">hello JavaScript logic registered at a collection level can then issue database operations on hello operations on hello documents of hello given collection.</span></span> <span data-ttu-id="8b908-941">Bu işlemler çevresel ACID işlemlerini sarılır.</span><span class="sxs-lookup"><span data-stu-id="8b908-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="8b908-942">Merhaba aşağıdaki örnek alanından toouse hello queryDocuments hello JavaScript sunucu API'sini toomake içinde nasıl sorgular gösterir iç saklı yordamları ve Tetikleyicileri.</span><span class="sxs-lookup"><span data-stu-id="8b908-942">hello following example shows how toouse hello queryDocuments in hello JavaScript server API toomake queries from inside stored procedures and triggers.</span></span>

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

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <span data-ttu-id="8b908-943"><a id="References"></a>Başvuruları</span><span class="sxs-lookup"><span data-stu-id="8b908-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="8b908-944">[Giriş tooAzure Cosmos DB][introduction]</span><span class="sxs-lookup"><span data-stu-id="8b908-944">[Introduction tooAzure Cosmos DB][introduction]</span></span>
2. [<span data-ttu-id="8b908-945">Azure Cosmos veritabanı SQL belirtimi</span><span class="sxs-lookup"><span data-stu-id="8b908-945">Azure Cosmos DB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="8b908-946">Azure Cosmos DB .NET örnekleri</span><span class="sxs-lookup"><span data-stu-id="8b908-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="8b908-947">[Azure Cosmos DB tutarlılık düzeyleri][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="8b908-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="8b908-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="8b908-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="8b908-949">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="8b908-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="8b908-950">JavaScript belirtimi [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="8b908-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="8b908-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="8b908-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="8b908-952">Sorgu büyük veritabanları için değerlendirme teknikleri [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="8b908-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="8b908-953">Sorgu 1994 paralel ilişkisel veritabanı sistemleri, IEEE bilgisayar topluluğu basın, işleme</span><span class="sxs-lookup"><span data-stu-id="8b908-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="8b908-954">Lu, Ooi, Bronz, sorgu 1994 paralel ilişkisel veritabanı sistemleri, IEEE bilgisayar topluluğu basın, işleme.</span><span class="sxs-lookup"><span data-stu-id="8b908-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="8b908-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Barış Tomkins: Pig Latin: veri işleme, SIGMOD 2008 için Not şekilde yabancı dil.</span><span class="sxs-lookup"><span data-stu-id="8b908-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="8b908-956">G.</span><span class="sxs-lookup"><span data-stu-id="8b908-956">G.</span></span> <span data-ttu-id="8b908-957">Graefe.</span><span class="sxs-lookup"><span data-stu-id="8b908-957">Graefe.</span></span> <span data-ttu-id="8b908-958">sorgu iyileştirme için Hello basamaklar çerçevesi.</span><span class="sxs-lookup"><span data-stu-id="8b908-958">hello Cascades framework for query optimization.</span></span> <span data-ttu-id="8b908-959">IEEE veri Müh</span><span class="sxs-lookup"><span data-stu-id="8b908-959">IEEE Data Eng.</span></span> <span data-ttu-id="8b908-960">Bull., 18(3): 1995.</span><span class="sxs-lookup"><span data-stu-id="8b908-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md