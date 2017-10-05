---
title: "Sunucu tarafı JavaScript programlama Azure Cosmos DB için | Microsoft Docs"
description: "Saklı yordamlar, veritabanı tetikleyiciler ve kullanıcı tanımlı işlevler (UDF'ler) JavaScript'te yazmak için Azure Cosmos DB kullanmayı öğrenin. Veritabanı programing ipuçları ve daha fazla bilgi edinin."
keywords: "Veritabanı tetikleyici, saklı yordam, saklı yordamı, veritabanı programı, sproc, documentdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: 
author: aliuy
manager: jhubbard
editor: mimig
ms.assetid: 0fba7ebd-a4fc-4253-a786-97f1354fbf17
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: andrl
ms.openlocfilehash: 8cddc7a8c9aa677b9c93bee3a7e05c226cc1f655
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="53084-105">Azure Cosmos DB sunucu tarafı programlama: saklı yordamlar, veritabanı tetikleyiciler ve UDF'lerin</span><span class="sxs-lookup"><span data-stu-id="53084-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="53084-106">Azure Cosmos veritabanı dil nasıl tümleşik öğrenin, JavaScript işlem tabanlı olarak yürütülmesini sağlar yazma geliştiriciler **saklı yordamlar**, **Tetikleyicileri** ve **kullanıcı tanımlı işlevler (UDF'ler)** yerel olarak bir [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span><span class="sxs-lookup"><span data-stu-id="53084-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="53084-107">Bu, gönderilen ve veritabanı depolama bölümlere doğrudan üzerinde yürütülen veritabanı program uygulama mantığı yazmak sağlar.</span><span class="sxs-lookup"><span data-stu-id="53084-107">This allows you to write database program application logic that can be shipped and executed directly on the database storage partitions.</span></span> 

<span data-ttu-id="53084-108">Burada Barış Liu Cosmos DB'ın sunucu tarafı veritabanı programlama modeli kısa bir giriş sağlar aşağıdaki videoyu izleyerek çalışmaya başlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="53084-108">We recommend getting started by watching the following video, where Andrew Liu provides a brief introduction to Cosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="53084-109">Ardından, bu makalede, aşağıdaki soruların yanıtlarını burada öğreneceksiniz döndürün:</span><span class="sxs-lookup"><span data-stu-id="53084-109">Then, return to this article, where you'll learn the answers to the following questions:</span></span>  

* <span data-ttu-id="53084-110">Ne ı yazma bir saklı yordam, tetikleyici veya JavaScript kullanarak UDF?</span><span class="sxs-lookup"><span data-stu-id="53084-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="53084-111">Cosmos DB ACID nasıl garanti?</span><span class="sxs-lookup"><span data-stu-id="53084-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="53084-112">İşlemler Cosmos DB'de nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="53084-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="53084-113">Önceden tetikler ve sonrası tetikler nedir ve nasıl t bir yazma?</span><span class="sxs-lookup"><span data-stu-id="53084-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="53084-114">Nasıl kaydetmek ve HTTP kullanarak bir RESTful şekilde bir saklı yordam, tetikleyici veya UDF yürütme?</span><span class="sxs-lookup"><span data-stu-id="53084-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="53084-115">Depolanmış yordamlar, tetikleyiciler ve UDF'lerin ne Cosmos DB SDK'ları oluşturmak ve çalıştırmak kullanılabilir olan?</span><span class="sxs-lookup"><span data-stu-id="53084-115">What Cosmos DB SDKs are available to create and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-to-stored-procedure-and-udf-programming"></a><span data-ttu-id="53084-116">Saklı yordam ve UDF programlamaya giriş</span><span class="sxs-lookup"><span data-stu-id="53084-116">Introduction to Stored Procedure and UDF Programming</span></span>
<span data-ttu-id="53084-117">Bu yaklaşım *"JavaScript T-SQL modern gün olarak"* tür sistem uyuşmazlıkları ve nesne ilişkisel eşleme teknolojileri karmaşıklığını uygulama geliştiricilerden boşaltır.</span><span class="sxs-lookup"><span data-stu-id="53084-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from the complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="53084-118">Ayrıca, bir dizi zengin uygulamaları oluşturmak için kullanılan iç avantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="53084-118">It also has a number of intrinsic advantages that can be utilized to build rich applications:</span></span>  

* <span data-ttu-id="53084-119">**Yordam mantığı:** JavaScript üst düzey bir programlama dili olarak iş mantığı ifade etmek için zengin ve tanıdık bir arabirim sağlar.</span><span class="sxs-lookup"><span data-stu-id="53084-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface to express business logic.</span></span> <span data-ttu-id="53084-120">Karmaşık sıraları yakın veri işlemleri gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="53084-120">You can perform complex sequences of operations closer to the data.</span></span>
* <span data-ttu-id="53084-121">**Atomik işlemleri:** tek bir saklı yordam veya tetikleyici içinde gerçekleştirilen işlemler veritabanı Cosmos DB garanti atomik.</span><span class="sxs-lookup"><span data-stu-id="53084-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="53084-122">Bu, tek bir toplu ilgili işlemlerinde bunların tümünün başarılı ya da bunların hiçbiri başarılı birleştirmek bir uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="53084-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="53084-123">**Performans:** iyileştirmeler arabellek havuzunda JSON belgelerinin yavaş materialization gibi bir dizi JSON Javascript dil türü sisteme doğası gereği eşlenen ve ayrıca temel depolama Cosmos DB'de birimidir olgu sağlar ve bunları, yürütülen kod kullanılabilir İsteğe bağlı hale getirme.</span><span class="sxs-lookup"><span data-stu-id="53084-123">**Performance:** The fact that JSON is intrinsically mapped to the Javascript language type system and is also the basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in the buffer pool and making them available on-demand to the executing code.</span></span> <span data-ttu-id="53084-124">Veritabanı dağıtımı iş mantığı ile ilgili daha fazla performans avantajı vardır:</span><span class="sxs-lookup"><span data-stu-id="53084-124">There are more performance benefits associated with shipping business logic to the database:</span></span>
  
  * <span data-ttu-id="53084-125">Toplu işleme – Geliştiriciler grubu ekleme gibi işlemleri ve toplu olarak gönderin.</span><span class="sxs-lookup"><span data-stu-id="53084-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="53084-126">Maliyet ağ trafiği gecikme süresi ve ayrı hareketleri oluşturmak için depolama yükünü önemli ölçüde azalır.</span><span class="sxs-lookup"><span data-stu-id="53084-126">The network traffic latency cost and the store overhead to create separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="53084-127">Ön derleme – Cosmos DB saklı yordamlar, tetikleyiciler ve kullanıcı tanımlı işlevler (UDF'ler JavaScript derleme maliyet her çağırma için önlemek için) işlemini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="53084-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) to avoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="53084-128">Yordam mantığı bayt kod oluşturmanın ek yükü için en az bir değer amortized.</span><span class="sxs-lookup"><span data-stu-id="53084-128">The overhead of building the byte code for the procedural logic is amortized to a minimal value.</span></span>
  * <span data-ttu-id="53084-129">Sıralama – birçok işlemleri gerek yan içeren büyük olasılıkla bir veya daha fazla ikincil depolama işlemleri yapılması etki ("tetikleyicisi").</span><span class="sxs-lookup"><span data-stu-id="53084-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="53084-130">Kararlılık yanı sıra, bu sunucuya taşındıklarında daha fazla kullanıcı olur.</span><span class="sxs-lookup"><span data-stu-id="53084-130">Aside from atomicity, this is more performant when moved to the server.</span></span> 
* <span data-ttu-id="53084-131">**Kapsülleme:** saklı yordamlar, tek bir yerde iş mantığı gruplandırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="53084-131">**Encapsulation:** Stored procedures can be used to group business logic in one place.</span></span> <span data-ttu-id="53084-132">Bu iki avantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="53084-132">This has two advantages:</span></span>
  * <span data-ttu-id="53084-133">Uygulamalarını bağımsız olarak verilerden gelişmesi veri mimarları etkinleştirir ham verileri en üstünde bir soyutlama katmanı ekler.</span><span class="sxs-lookup"><span data-stu-id="53084-133">It adds an abstraction layer on top of the raw data, which enables data architects to evolve their applications independently from the data.</span></span> <span data-ttu-id="53084-134">Veri şeması az verilerle doğrudan dağıtılacak varsa uygulamasına baked gerekebilir kırılır varsayımlar nedeniyle, bu özellikle yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="53084-134">This is particularly advantageous when the data is schema-less, due to the brittle assumptions that may need to be baked into the application if they have to deal with data directly.</span></span>  
  * <span data-ttu-id="53084-135">Bu soyutlama kuruluşların betikleri erişimden hızlandırma tarafından verilerine güvenli kalmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="53084-135">This abstraction lets enterprises keep their data secure by streamlining the access from the scripts.</span></span>  

<span data-ttu-id="53084-136">Oluşturma ve yürütme veritabanı tetikleyici, saklı yordam ve özel sorgu işleçleri aracılığıyla desteklenir [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), ve [istemci SDK'ları](documentdb-sdk-dotnet.md).NET, Node.js ve JavaScript gibi birçok platformda.</span><span class="sxs-lookup"><span data-stu-id="53084-136">The creation and execution of database triggers, stored procedure and custom query operators is supported through the [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="53084-137">Bu öğretici kullanır [Node.js SDK'sı ile Q öneriler](http://azure.github.io/azure-documentdb-node-q/) sözdizimi ve saklı yordamlar, tetikleyiciler ve UDF'lerin kullanımını göstermek için.</span><span class="sxs-lookup"><span data-stu-id="53084-137">This tutorial uses the [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) to illustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="53084-138">Saklı yordamlar</span><span class="sxs-lookup"><span data-stu-id="53084-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="53084-139">Örnek: basit bir saklı yordam yazma</span><span class="sxs-lookup"><span data-stu-id="53084-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="53084-140">"Hello World" yanıt veren basit bir saklı yordam ile başlayalım.</span><span class="sxs-lookup"><span data-stu-id="53084-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="53084-141">Saklı yordamlar koleksiyonu başına kaydedilir ve herhangi bir belge ve ek koleksiyonda mevcut üzerinde çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="53084-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="53084-142">Aşağıdaki kod parçacığını bir koleksiyonla helloWorld saklı yordamın nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="53084-142">The following snippet shows how to register the helloWorld stored procedure with a collection.</span></span> 

    // register the stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="53084-143">Saklı yordam kaydedildiğinde, biz karşı koleksiyonu yürütün ve sonuçları istemcide geri okuyun.</span><span class="sxs-lookup"><span data-stu-id="53084-143">Once the stored procedure is registered, we can execute it against the collection, and read the results back at the client.</span></span> 

    // execute the stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="53084-144">Context nesnesi Cosmos DB depolama üzerinde gerçekleştirilen tüm işlemlerin erişimin yanı sıra, istek ve yanıt nesnelere erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="53084-144">The context object provides access to all operations that can be performed on Cosmos DB storage, as well as access to the request and response objects.</span></span> <span data-ttu-id="53084-145">Bu durumda, biz istemciye gönderilen yanıtın gövdesini ayarlamak için yanıt nesnesi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="53084-145">In this case, we used the response object to set the body of the response that was sent back to the client.</span></span> <span data-ttu-id="53084-146">Daha fazla ayrıntı için başvurmak [Azure Cosmos DB JavaScript server SDK Belgeleri](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="53084-146">For more details, refer to the [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="53084-147">Bize göre bu örnekte genişletin ve daha fazla saklı yordama ilgili işlevselliği veritabanı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="53084-147">Let us expand on this example and add more database related functionality to the stored procedure.</span></span> <span data-ttu-id="53084-148">Saklı yordamlar oluşturmak, güncelleştirmek, okuyabilir, sorgu ve belgeler ve koleksiyon içindeki ekleri silin.</span><span class="sxs-lookup"><span data-stu-id="53084-148">Stored procedures can create, update, read, query and delete documents and attachments inside the collection.</span></span>    

### <a name="example-write-a-stored-procedure-to-create-a-document"></a><span data-ttu-id="53084-149">Örnek: bir belge oluşturmak için bir saklı yordam yazma</span><span class="sxs-lookup"><span data-stu-id="53084-149">Example: Write a stored procedure to create a document</span></span>
<span data-ttu-id="53084-150">Sonraki kod parçacığını context nesnesi Cosmos DB kaynakları ile etkileşim kurmak için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="53084-150">The next snippet shows how to use the context object to interact with Cosmos DB resources.</span></span>

    var createDocumentStoredProc = {
        id: "createMyDocument",
        serverScript: function createMyDocument(documentToCreate) {
            var context = getContext();
            var collection = context.getCollection();

            var accepted = collection.createDocument(collection.getSelfLink(),
                  documentToCreate,
                  function (err, documentCreated) {
                      if (err) throw new Error('Error' + err.message);
                      context.getResponse().setBody(documentCreated.id)
                  });
            if (!accepted) return;
        }
    }


<span data-ttu-id="53084-151">Bu saklı yordam giriş documentToCreate, geçerli koleksiyonunda oluşturulmasına belgeye gövdesini alır.</span><span class="sxs-lookup"><span data-stu-id="53084-151">This stored procedure takes as input documentToCreate, the body of a document to be created in the current collection.</span></span> <span data-ttu-id="53084-152">Tüm işlemleri zaman uyumsuzdur ve JavaScript işlevi geri aramalar üzerinde bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="53084-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="53084-153">Geri çağırma işlevi iki parametre, işlem başarısız durumda hata nesnesi için diğeri için oluşturulan nesnesi vardır.</span><span class="sxs-lookup"><span data-stu-id="53084-153">The callback function has two parameters, one for the error object in case the operation fails, and one for the created object.</span></span> <span data-ttu-id="53084-154">Geri çağırma içinde kullanıcıların özel durumu işlemek ya da bir hata durum.</span><span class="sxs-lookup"><span data-stu-id="53084-154">Inside the callback, users can either handle the exception or throw an error.</span></span> <span data-ttu-id="53084-155">Bir geri çağırma değil sağlanır ve bir hata durumunda, Azure Cosmos DB çalışma zamanı bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="53084-155">In case a callback is not provided and there is an error, the Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="53084-156">İşlem başarısız olursa yukarıdaki örnekte, bir hata geri çağırma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="53084-156">In the example above, the callback throws an error if the operation failed.</span></span> <span data-ttu-id="53084-157">Aksi durumda, istemci yanıt gövdesi olarak oluşturulan belge kimliğini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="53084-157">Otherwise, it sets the id of the created document as the body of the response to the client.</span></span> <span data-ttu-id="53084-158">İşte bu saklı yordam giriş parametreleriyle nasıl yürütülür.</span><span class="sxs-lookup"><span data-stu-id="53084-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register the stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure to create a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "The Hitchhiker’s Guide to the Galaxy",
                author: "Douglas Adams"
            };

            return client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/createMyDocument',
                  docToCreate);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response); // "DocFromSproc"
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="53084-159">Bu saklı yordam belge gövdeleri bir dizi girişi olarak almak ve bunları tüm aynı saklı yordam yürütme bunların her birini ayrı ayrı oluşturmak için birden çok ağ isteklerini yerine oluşturmak için değiştirilebilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="53084-159">Note that this stored procedure can be modified to take an array of document bodies as input and create them all in the same stored procedure execution instead of multiple network requests to create each of them individually.</span></span> <span data-ttu-id="53084-160">Cosmos DB (Bu öğreticinin ilerleyen bölümlerinde açıklanmıştır) için verimli toplu içeri Aktarıcı uygulamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="53084-160">This can be used to implement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="53084-161">Açıklanan örnek saklı yordamları kullanma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="53084-161">The example described demonstrated how to use stored procedures.</span></span> <span data-ttu-id="53084-162">Daha sonra öğreticide biz tetikleyiciler ve kullanıcı tanımlı işlevler (UDF'ler) ele alınacaktır.</span><span class="sxs-lookup"><span data-stu-id="53084-162">We will cover triggers and user defined functions (UDFs) later in the tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="53084-163">Veritabanı program işlemleri</span><span class="sxs-lookup"><span data-stu-id="53084-163">Database program transactions</span></span>
<span data-ttu-id="53084-164">Tipik bir veritabanında işlem tek bir mantıksal birim iş olarak gerçekleştirilen işlemler dizisi olarak tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="53084-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="53084-165">Her işlem sağlar **ACID garanti**.</span><span class="sxs-lookup"><span data-stu-id="53084-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="53084-166">ACID dört özellikleri - kararlılık, tutarlılık, yalıtım ve dayanıklılık anlamına gelir iyi bilinen bir kısaltma ' dir.</span><span class="sxs-lookup"><span data-stu-id="53084-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="53084-167">Kısaca, bir işlem içinde tüm çalışmanın tek bir birim olarak davranılır kararlılık garanti burada ya da tamamını kaydedilmiş veya yok.</span><span class="sxs-lookup"><span data-stu-id="53084-167">Briefly, atomicity guarantees that all the work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="53084-168">Tutarlılık verilerin işlemleri arasında her zaman iyi bir iç durumda olduğundan emin olur.</span><span class="sxs-lookup"><span data-stu-id="53084-168">Consistency makes sure that the data is always in a good internal state across transactions.</span></span> <span data-ttu-id="53084-169">Yalıtım iki işlem birbiriyle – genellikle etkilemesine, çoğu ticari sistemleri kullanılabilir birden çok yalıtım düzeyi uygulama gereksinimlerine göre sağlayın güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="53084-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on the application needs.</span></span> <span data-ttu-id="53084-170">Dayanıklılık veritabanında kaydedilen herhangi bir değişiklik her zaman mevcut olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="53084-170">Durability ensures that any change that’s committed in the database will always be present.</span></span>   

<span data-ttu-id="53084-171">Cosmos DB'de JavaScript veritabanıyla aynı bellek alanı barındırılır.</span><span class="sxs-lookup"><span data-stu-id="53084-171">In Cosmos DB, JavaScript is hosted in the same memory space as the database.</span></span> <span data-ttu-id="53084-172">Bu nedenle, yapılan istekleri içinde saklı yordamları ve Tetikleyicileri veritabanı oturumu aynı kapsamda yürütün.</span><span class="sxs-lookup"><span data-stu-id="53084-172">Hence, requests made within stored procedures and triggers execute in the same scope of a database session.</span></span> <span data-ttu-id="53084-173">Bu, tek bir saklı yordam/tetikleyici parçası olan tüm işlemler için ACID güvence altına almak Cosmos DB sağlar.</span><span class="sxs-lookup"><span data-stu-id="53084-173">This enables Cosmos DB to guarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="53084-174">Aşağıdaki saklı yordamı tanımı göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="53084-174">Consider the following stored procedure definition:</span></span>

    // JavaScript source code
    var exchangeItemsSproc = {
        id: "exchangeItems",
        serverScript: function (playerId1, playerId2) {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            var player1Document, player2Document;

            // query for players
            var filterQuery = 'SELECT * FROM Players p where p.id  = "' + playerId1 + '"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery, {},
                function (err, documents, responseOptions) {
                    if (err) throw new Error("Error" + err.message);

                    if (documents.length != 1) throw "Unable to find both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable to find both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable to read player details, abort ";
                });

            if (!accept) throw "Unable to read player details, abort ";

            // swap the two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable to update player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable to update player 2, abort"
                            });

                        if (!accept2) throw "Unable to update player 2, abort";
                    });

                if (!accept) throw "Unable to update player 1, abort";
            }
        }
    }

    // register the stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="53084-175">Bu saklı yordam hareketleri ticari öğelere tek bir işlemde iki oyuncu arasında bir oyun uygulaması içinde kullanır.</span><span class="sxs-lookup"><span data-stu-id="53084-175">This stored procedure uses transactions within a gaming app to trade items between two players in a single operation.</span></span> <span data-ttu-id="53084-176">Saklı yordam bir bağımsız değişken olarak geçirilen her player kimlikleri karşılık gelen iki belge okumaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="53084-176">The stored procedure attempts to read two documents each corresponding to the player IDs passed in as an argument.</span></span> <span data-ttu-id="53084-177">Her iki player belge bulunamazsa, saklı yordamı öğelerin takas tarafından belgeleri güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="53084-177">If both player documents are found, then the stored procedure updates the documents by swapping their items.</span></span> <span data-ttu-id="53084-178">Yol boyunca herhangi bir hatayla karşılaşılmazsa örtük olarak hareket durdurur bir JavaScript özel durumu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="53084-178">If any errors are encountered along the way, it throws a JavaScript exception that implicitly aborts the transaction.</span></span>

<span data-ttu-id="53084-179">Saklı yordam koleksiyonu kaydedilmişse karşı tek bölümlü bir koleksiyon olduğu sonra işlem koleksiyonundaki tüm belgelerin kapsamlıdır.</span><span class="sxs-lookup"><span data-stu-id="53084-179">If the collection the stored procedure is registered against is a single-partition collection, then the transaction is scoped to all the documents within the collection.</span></span> <span data-ttu-id="53084-180">Ardından koleksiyon bölümlendiğinde ise, saklı yordamlar tek bölüm anahtarı işlem kapsamı içinde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="53084-180">If the collection is partitioned, then stored procedures are executed in the transaction scope of a single partition key.</span></span> <span data-ttu-id="53084-181">Her saklı yordam yürütme sonra işlemin altında çalıştırmalısınız kapsamına karşılık gelen bir bölüm anahtarı değerini içermelidir.</span><span class="sxs-lookup"><span data-stu-id="53084-181">Each stored procedure execution must then include a partition key value corresponding to the scope the transaction must run under.</span></span> <span data-ttu-id="53084-182">Daha fazla ayrıntı için bkz: [Azure DB Cosmos bölümleme](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="53084-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="53084-183">Kaydetme ve geri alma</span><span class="sxs-lookup"><span data-stu-id="53084-183">Commit and rollback</span></span>
<span data-ttu-id="53084-184">İşlemleri iç ve yerel olarak Cosmos veritabanı JavaScript programlama modeline tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="53084-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="53084-185">JavaScript işlevinin içinde tüm işlemleri otomatik olarak tek bir işlem altında sarılır.</span><span class="sxs-lookup"><span data-stu-id="53084-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="53084-186">JavaScript bir özel durumla tamamlarsa, veritabanı işlemleri kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="53084-186">If the JavaScript completes without any exception, the operations to the database are committed.</span></span> <span data-ttu-id="53084-187">İlişkisel veritabanları "BEGIN TRANSACTION" ve "COMMIT TRANSACTION" deyimlerinde Cosmos DB'de örtük etkindir.</span><span class="sxs-lookup"><span data-stu-id="53084-187">In effect, the “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="53084-188">Komut dosyasını yayılır herhangi bir özel durum ise, Cosmos veritabanı JavaScript çalışma zamanı tüm işlem döndürülmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="53084-188">If there is any exception that’s propagated from the script, Cosmos DB’s JavaScript runtime will roll back the whole transaction.</span></span> <span data-ttu-id="53084-189">Önceki örnekte gösterildiği gibi bir özel durum atma etkili bir şekilde bir "geri alma işlemi" Cosmos DB'de eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="53084-189">As shown in the earlier example, throwing an exception is effectively equivalent to a “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="53084-190">Veri tutarlılığı</span><span class="sxs-lookup"><span data-stu-id="53084-190">Data consistency</span></span>
<span data-ttu-id="53084-191">Saklı yordamları ve Tetikleyicileri her zaman birincil Çoğaltmada Azure Cosmos DB kapsayıcısının yürütülür.</span><span class="sxs-lookup"><span data-stu-id="53084-191">Stored procedures and triggers are always executed on the primary replica of the Azure Cosmos DB container.</span></span> <span data-ttu-id="53084-192">Bu, okuma içindeki yordamları teklif güçlü tutarlılık depolanan sağlar.</span><span class="sxs-lookup"><span data-stu-id="53084-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="53084-193">Kullanıcı tanımlı işlevler kullanarak sorguları birincil veya ikincil bir çoğaltma üzerinde çalıştırılabilir, ancak uygun çoğaltma seçerek istenen tutarlılık düzeyi karşılamak üzere biz emin olun.</span><span class="sxs-lookup"><span data-stu-id="53084-193">Queries using user defined functions can be executed on the primary or any secondary replica, but we ensure to meet the requested consistency level by choosing the appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="53084-194">Sınırlanmış yürütme</span><span class="sxs-lookup"><span data-stu-id="53084-194">Bounded execution</span></span>
<span data-ttu-id="53084-195">Belirtilen sunucu içinde tüm Cosmos DB işlemleri tamamlamalısınız isteği zaman aşımı süresi.</span><span class="sxs-lookup"><span data-stu-id="53084-195">All Cosmos DB operations must complete within the server specified request timeout duration.</span></span> <span data-ttu-id="53084-196">Bu sınırlama JavaScript işlevleri (saklı yordamlar, tetikleyiciler ve kullanıcı tanımlı işlevler) için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="53084-196">This constraint also applies to JavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="53084-197">Bir işlem bu zaman sınırı ile tamamlanmazsa, işlem geri alındı.</span><span class="sxs-lookup"><span data-stu-id="53084-197">If an operation does not complete with that time limit, the transaction is rolled back.</span></span> <span data-ttu-id="53084-198">JavaScript işlevleri süre sınırı içinde son veya toplu/sürdürmeden yürütme için temel devamlılık modeli uygulamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="53084-198">JavaScript functions must finish within the time limit or implement a continuation based model to batch/resume execution.</span></span>  

<span data-ttu-id="53084-199">Saklı yordamları ve Tetikleyicileri süre sınırlarını, tüm işlevler (için oluşturma, okuma, değiştirin ve belgeler ve ekleri silme) koleksiyon nesnesi altında işlemek için geliştirmeyi kolaylaştırmak için return bir Boole değeri bu temsil olup olmadığını bu işlemi tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="53084-199">In order to simplify development of stored procedures and triggers to handle time limits, all functions under the collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="53084-200">Bu değeri false ise, bu zaman sınırı dolmak üzere olduğunu ve yordam yürütme sarmalamanız gerekir göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="53084-200">If this value is false, it is an indication that the time limit is about to expire and that the procedure must wrap up execution.</span></span>  <span data-ttu-id="53084-201">İlk kabul edilmeyen deposu işlemi sıraya alınan öncesinde Operations saklı yordamı zamanında tamamlandıktan ve başka istek sıraya değil tamamlamak için garanti edilir.</span><span class="sxs-lookup"><span data-stu-id="53084-201">Operations queued prior to the first unaccepted store operation are guaranteed to complete if the stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="53084-202">JavaScript işlevleri de kaynak tüketimine ilişkin ilişkisindeki.</span><span class="sxs-lookup"><span data-stu-id="53084-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="53084-203">Cosmos DB veritabanı hesabı sağlanan boyutuna göre koleksiyon başına ayırır.</span><span class="sxs-lookup"><span data-stu-id="53084-203">Cosmos DB reserves throughput per collection based on the provisioned size of a database account.</span></span> <span data-ttu-id="53084-204">Üretilen iş CPU, bellek ve g/ç tüketim istek birimleri veya RUs adlı normalleştirilmiş bir birim cinsinden ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="53084-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="53084-205">JavaScript işlevleri potansiyel olarak çok sayıda RUs kısa bir süre içinde yukarı kullanabilirsiniz ve oranı koleksiyonunun sınırına ulaşıldığında sınırlı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53084-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if the collection’s limit is reached.</span></span> <span data-ttu-id="53084-206">Basit veritabanı işlemleri kullanılabilirliğini sağlamak için kaynak yoğunluklu saklı yordamları da karantinaya.</span><span class="sxs-lookup"><span data-stu-id="53084-206">Resource intensive stored procedures might also be quarantined to ensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="53084-207">Örnek: toplu bir veritabanı programa veri alma</span><span class="sxs-lookup"><span data-stu-id="53084-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="53084-208">Aşağıda, belgeler bir koleksiyona toplu içeri için yazılmış bir saklı yordam örneğidir.</span><span class="sxs-lookup"><span data-stu-id="53084-208">Below is an example of a stored procedure that is written to bulk-import documents into a collection.</span></span> <span data-ttu-id="53084-209">Saklı yordam Boolean denetleyerek sınırlanmış yürütme nasıl işlediğini Not createDocument dönüş değeri ve izlemek ve toplu işlemler arasında ilerleme sürdürmek için saklı yordam her çalıştırılışı eklenen belge sayısını kullanır.</span><span class="sxs-lookup"><span data-stu-id="53084-209">Note how the stored procedure handles bounded execution by checking the Boolean return value from createDocument, and then uses the count of documents inserted in each invocation of the stored procedure to track and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // The count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("The array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call the create API to create a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) The createDocument request was not accepted. 
        //    In this case the callback will not be called, we just call setBody and we are done.
        // 2) The callback was called docs.length times.
        //    In this case all documents were created and we don’t need to call tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If the request was accepted, callback will be called.
            // Otherwise report current count back to the client, 
            // which will call the script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order to process the result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment the count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set the response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="53084-210"><a id="trigger"></a>Veritabanı Tetikleyicileri</span><span class="sxs-lookup"><span data-stu-id="53084-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="53084-211">Veritabanı öncesi Tetikleyicileri</span><span class="sxs-lookup"><span data-stu-id="53084-211">Database pre-triggers</span></span>
<span data-ttu-id="53084-212">Cosmos DB yürütülen ya da bir belge üzerinde bir işlemi tarafından tetiklenen Tetikleyiciler sağlar.</span><span class="sxs-lookup"><span data-stu-id="53084-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="53084-213">Örneğin, ön tetikleyici belirtebilmeniz için bir belge oluşturma – bu ön tetikleyici belgeyi oluşturulmadan önce çalışacak olduğunda.</span><span class="sxs-lookup"><span data-stu-id="53084-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before the document is created.</span></span> <span data-ttu-id="53084-214">Ön Tetikleyicileri oluşturulmakta olan bir belgenin özelliklerini doğrulamak için nasıl kullanılabileceği bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="53084-214">The following is an example of how pre-triggers can be used to validate the properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document to be created in the current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update the document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="53084-215">Ve karşılık gelen Node.js istemci tarafı kaydı kodu tetikleyici için:</span><span class="sxs-lookup"><span data-stu-id="53084-215">And the corresponding Node.js client-side registration code for the trigger:</span></span>

    // register pre-trigger
    client.createTriggerAsync(collection.self, validateDocumentContentsTrigger)
        .then(function (response) {
            console.log("Created", response.resource);
            var docToCreate = {
                id: "DocWithTrigger",
                event: "Error",
                source: "Network outage"
            };

            // run trigger while creating above document 
            var options = { preTriggerInclude: "validateDocumentContents" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response.resource); // document with timestamp property added
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="53084-216">Giriş parametreleri öncesi tetikleyici bulunamaz.</span><span class="sxs-lookup"><span data-stu-id="53084-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="53084-217">İstek nesnesi, işlemle ilişkili İstek iletisini işlemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="53084-217">The request object can be used to manipulate the request message associated with the operation.</span></span> <span data-ttu-id="53084-218">Burada, ön tetikleyici belgeyi oluşturma ile çalıştırın ve JSON biçiminde oluşturulacak belge isteği ileti gövdesi içerir.</span><span class="sxs-lookup"><span data-stu-id="53084-218">Here, the pre-trigger is being run with the creation of a document, and the request message body contains the document to be created in JSON format.</span></span>   

<span data-ttu-id="53084-219">Tetikleyiciler kayıtlı olduğunda, kullanıcılar ile çalıştırabilirsiniz operations belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53084-219">When triggers are registered, users can specify the operations that it can run with.</span></span> <span data-ttu-id="53084-220">Bu tetikleyici aşağıdaki izin anlamına gelir TriggerOperation.Create ile oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="53084-220">This trigger was created with TriggerOperation.Create, which means the following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="53084-221">Veritabanı sonrası Tetikleyicileri</span><span class="sxs-lookup"><span data-stu-id="53084-221">Database post-triggers</span></span>
<span data-ttu-id="53084-222">Ön tetikleyiciler gibi sonrası Tetikleyicileri bir belge üzerinde bir işlemi ile ilişkili ve giriş parametreleri gerçekleştirin yok.</span><span class="sxs-lookup"><span data-stu-id="53084-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="53084-223">Çalışırlar **sonra** işlemi tamamlandıktan ve istemciye gönderilen yanıt iletisi erişebilir.</span><span class="sxs-lookup"><span data-stu-id="53084-223">They run **after** the operation has completed, and have access to the response message that is sent to the client.</span></span>   

<span data-ttu-id="53084-224">Aşağıdaki örnek, eylemde sonrası Tetikleyicileri gösterir:</span><span class="sxs-lookup"><span data-stu-id="53084-224">The following example shows post-triggers in action:</span></span>

    var updateMetadataTrigger = {
        id: "updateMetadata",
        serverScript: function updateMetadata() {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            // document that was created
            var createdDocument = response.getBody();

            // query for metadata document
            var filterQuery = 'SELECT * FROM root r WHERE r.id = "_metadata"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery,
                updateMetadataCallback);
            if(!accept) throw "Unable to update metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable to find metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable to update metadata, abort";
                               });
                         if(!accept) throw "Unable to update metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="53084-225">Tetikleyici, aşağıdaki örnekte gösterildiği gibi kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="53084-225">The trigger can be registered as shown in the following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "The Band",
                albums: ["Hellujah", "Rotators", "Spinning Top"]
            };

            // run trigger while creating above document 
            var options = { postTriggerInclude: "updateMetadata" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });


<span data-ttu-id="53084-226">Bu tetikleyici için meta veri belgesi sorgular ve yeni oluşturulan belge hakkında ayrıntılarla güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="53084-226">This trigger queries for the metadata document and updates it with details about the newly created document.</span></span>  

<span data-ttu-id="53084-227">Dikkat edilecek önemli bir şey **işlem** Cosmos DB Tetikleyicileri yürütülmesi.</span><span class="sxs-lookup"><span data-stu-id="53084-227">One thing that is important to note is the **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="53084-228">Aynı işlem özgün belgeye oluşturulmasını olarak bir parçası olarak bu sonrası tetikleyici çalışır.</span><span class="sxs-lookup"><span data-stu-id="53084-228">This post-trigger runs as part of the same transaction as the creation of the original document.</span></span> <span data-ttu-id="53084-229">Bu nedenle, biz sonrası tetikleyici (meta veri belgesi güncelleştirmek bağlanamıyoruz varsa say) bir özel durum, tüm işlem başarısız olur ve geri alındı.</span><span class="sxs-lookup"><span data-stu-id="53084-229">Therefore, if we throw an exception from the post-trigger (say if we are unable to update the metadata document), the whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="53084-230">Bir belge oluşturulur ve bir özel durum döndürdü.</span><span class="sxs-lookup"><span data-stu-id="53084-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="53084-231"><a id="udf"></a>Kullanıcı tanımlı işlevler</span><span class="sxs-lookup"><span data-stu-id="53084-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="53084-232">Kullanıcı tanımlı işlevler (UDF'ler), özel iş mantığı uygulamanız ve DocumentDB API SQL Sorgu Dili Dilbilgisi genişletmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="53084-232">User-defined functions (UDFs) are used to extend the DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="53084-233">Öğesinden yalnızca çağrılabilir sorguları içinde.</span><span class="sxs-lookup"><span data-stu-id="53084-233">They can only be called from inside queries.</span></span> <span data-ttu-id="53084-234">Bunlar erişim kapsamı nesnesine sahip değil ve yalnızca işlem JavaScript kullanılması amaçlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="53084-234">They do not have access to the context object and are meant to be used as compute-only JavaScript.</span></span> <span data-ttu-id="53084-235">Bu nedenle, UDF'ler Cosmos DB hizmet ikincil çoğaltmalar üzerinde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="53084-235">Therefore, UDFs can be run on secondary replicas of the Cosmos DB service.</span></span>  

<span data-ttu-id="53084-236">Aşağıdaki örnek gelir çeşitli gelir köşeli için hızlarını göre vergi hesaplamak için bir UDF oluşturur ve ardından birden fazla $20.000 vergiler Ücretli tüm kişilerin bulmak için bir sorgu içinde kullanır.</span><span class="sxs-lookup"><span data-stu-id="53084-236">The following sample creates a UDF to calculate income tax based on rates for various income brackets, and then uses it inside a query to find all people who paid more than $20,000 in taxes.</span></span>

    var taxUdf = {
        id: "tax",
        serverScript: function tax(income) {

            if(income == undefined) 
                throw 'no input';

            if (income < 1000) 
                return income * 0.1;
            else if (income < 10000) 
                return income * 0.2;
            else
                return income * 0.4;
        }
    }


<span data-ttu-id="53084-237">UDF daha sonra aşağıdaki örnekteki gibi sorgularında kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="53084-237">The UDF can subsequently be used in queries like in the following sample:</span></span>

    // register UDF
    client.createUserDefinedFunctionAsync('dbs/testdb/colls/testColl', taxUdf)
        .then(function(response) { 
            console.log("Created", response.resource);

            var query = 'SELECT * FROM TaxPayers t WHERE udf.tax(t.income) > 20000'; 
            return client.queryDocuments('dbs/testdb/colls/testColl',
                   query).toArrayAsync();
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        var documents = response.feed;
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="53084-238">JavaScript dil ile tümleşik sorgu API</span><span class="sxs-lookup"><span data-stu-id="53084-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="53084-239">Documentdb'nin SQL dil bilgisinin kullanarak sorgu göndermeye ek olarak, sunucu tarafı SDK'sı SQL bilgisi olmadan fluent JavaScript arabirimi kullanarak en iyi duruma getirilmiş sorguları gerçekleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="53084-239">In addition to issuing queries using DocumentDB’s SQL grammar, the server-side SDK allows you to perform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="53084-240">API chainable işlevdeki koşul işlevleri geçirerek sorguları programlı olarak oluşturmanıza olanak sağlayan JavaScript sorgu ECMAScript5'ın dizi öğelerin ve lodash gibi popüler JavaScript kitaplıklarını tanıdık bir sözdizimi ile çağırır.</span><span class="sxs-lookup"><span data-stu-id="53084-240">The JavaScript query API allows you to programmatically build queries by passing predicate functions into chainable function calls, with a syntax familiar to ECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="53084-241">Sorguları verimli bir şekilde Azure Cosmos veritabanı dizinlerini kullanarak çalıştırılacak JavaScript çalışma zamanı tarafından ayrıştırılır.</span><span class="sxs-lookup"><span data-stu-id="53084-241">Queries are parsed by the JavaScript runtime to be executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="53084-242">`__`(çift alt çizgi) olan bir diğer ad `getContext().getCollection()`.</span><span class="sxs-lookup"><span data-stu-id="53084-242">`__` (double-underscore) is an alias to `getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="53084-243">Diğer bir deyişle, kullanabileceğiniz `__` veya `getContext().getCollection()` JavaScript sorgu API erişmek için.</span><span class="sxs-lookup"><span data-stu-id="53084-243">In other words, you can use `__` or `getContext().getCollection()` to access the JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="53084-244">Desteklenen işlevler aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="53084-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="53084-245">
<b>... chain(). değeri ([geri çağırma] [, Seçenekleri])</b>
</span><span class="sxs-lookup"><span data-stu-id="53084-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="53084-246">İle bitmelidir bir zincirleme çağrısını Value()) ile başlar.</span><span class="sxs-lookup"><span data-stu-id="53084-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="53084-247">
<b>Filtre (predicateFunction [, Seçenekleri] [, geri çağırma])</b>
</span><span class="sxs-lookup"><span data-stu-id="53084-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="53084-248">Giriş belgeleri giriş/çıkış sonuç kümesine filtrelemek için true/false döndüren bir koşul işlevini kullanarak giriş filtreler.</span><span class="sxs-lookup"><span data-stu-id="53084-248">Filters the input using a predicate function which returns true/false in order to filter in/out input documents into the resulting set.</span></span> <span data-ttu-id="53084-249">WHERE yan tümcesi SQL benzer şekilde davranır.</span><span class="sxs-lookup"><span data-stu-id="53084-249">This behaves similar to a WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="53084-250">
<b>Harita (transformationFunction [, Seçenekleri] [, geri çağırma])</b>
</span><span class="sxs-lookup"><span data-stu-id="53084-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="53084-251">Her bir giriş öğesini bir JavaScript nesne veya değer eşleştiren bir dönüşüm işlevi verilen bir yansıtma geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="53084-251">Applies a projection given a transformation function which maps each input item to a JavaScript object or value.</span></span> <span data-ttu-id="53084-252">Bir seçim yan tümcesinde SQL benzer şekilde davranır.</span><span class="sxs-lookup"><span data-stu-id="53084-252">This behaves similar to a SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="53084-253">
<b>pluck ([propertyName] [, Seçenekleri] [, geri çağırma])</b>
</span><span class="sxs-lookup"><span data-stu-id="53084-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="53084-254">Her giriş öğesinden tek bir özellik değeri ayıklayan bir harita için bir kısayol budur.</span><span class="sxs-lookup"><span data-stu-id="53084-254">This is a shortcut for a map which extracts the value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="53084-255">
<b>düzleştirmek ([isShallow] [, Seçenekleri] [, geri çağırma])</b>
</span><span class="sxs-lookup"><span data-stu-id="53084-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="53084-256">Birleştirir ve tek bir dizi giriş her öğeden dizilerinin düzleştirir.</span><span class="sxs-lookup"><span data-stu-id="53084-256">Combines and flattens arrays from each input item in to a single array.</span></span> <span data-ttu-id="53084-257">LINQ SelectMany benzer şekilde davranır.</span><span class="sxs-lookup"><span data-stu-id="53084-257">This behaves similar to SelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="53084-258">
<b>sortBy ([koşulu] [, Seçenekleri] [, geri çağırma])</b>
</span><span class="sxs-lookup"><span data-stu-id="53084-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="53084-259">Yeni belgeler birtakım verilen koşulu kullanarak artan giriş belgesi akış belgelerde sıralayarak üretir.</span><span class="sxs-lookup"><span data-stu-id="53084-259">Produce a new set of documents by sorting the documents in the input document stream in ascending order using the given predicate.</span></span> <span data-ttu-id="53084-260">Bir ORDER BY yan tümcesi SQL benzer şekilde davranır.</span><span class="sxs-lookup"><span data-stu-id="53084-260">This behaves similar to a ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="53084-261">
<b>sortByDescending ([koşulu] [, Seçenekleri] [, geri çağırma])</b>
</span><span class="sxs-lookup"><span data-stu-id="53084-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="53084-262">Yeni belgeler birtakım verilen koşulu kullanarak azalan giriş belgesi akış belgelerde sıralayarak üretir.</span><span class="sxs-lookup"><span data-stu-id="53084-262">Produce a new set of documents by sorting the documents in the input document stream in descending order using the given predicate.</span></span> <span data-ttu-id="53084-263">Bir x DESC ORDER BY yan tümcesi SQL benzer şekilde davranır.</span><span class="sxs-lookup"><span data-stu-id="53084-263">This behaves similar to a ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="53084-264">Koşul ve/veya Seçici işlevlerinin içine dahil edilirse, aşağıdaki JavaScript yapılarından otomatik olarak doğrudan Azure Cosmos DB dizinlerini çalıştırmak için en iyi duruma getirilmiş:</span><span class="sxs-lookup"><span data-stu-id="53084-264">When included inside predicate and/or selector functions, the following JavaScript constructs get automatically optimized to run directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="53084-265">Basit işleçleri: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="53084-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="53084-266">Değişmez değer nesnesi de dahil olmak üzere değişmez değerler: {}</span><span class="sxs-lookup"><span data-stu-id="53084-266">Literals, including the object literal: {}</span></span>
* <span data-ttu-id="53084-267">dönüş var</span><span class="sxs-lookup"><span data-stu-id="53084-267">var, return</span></span>

<span data-ttu-id="53084-268">Şu JavaScript yapıları Azure Cosmos DB dizinler için en iyi duruma getirilmiş değil:</span><span class="sxs-lookup"><span data-stu-id="53084-268">The following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="53084-269">Denetim akışı (örn. Eğer, sırada)</span><span class="sxs-lookup"><span data-stu-id="53084-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="53084-270">İşlev çağrıları</span><span class="sxs-lookup"><span data-stu-id="53084-270">Function calls</span></span>

<span data-ttu-id="53084-271">Daha fazla bilgi için lütfen bkz bizim [sunucu tarafı JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="53084-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-the-javascript-query-api"></a><span data-ttu-id="53084-272">Örnek: JavaScript sorgu API kullanarak bir saklı yordam yazma</span><span class="sxs-lookup"><span data-stu-id="53084-272">Example: Write a stored procedure using the JavaScript query API</span></span>
<span data-ttu-id="53084-273">Aşağıdaki kod örneği bağlamında bir saklı yordam, JavaScript sorgu API'sı nasıl kullanılabileceği bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="53084-273">The following code sample is an example of how the JavaScript Query API can be used in the context of a stored procedure.</span></span> <span data-ttu-id="53084-274">Saklı yordam bir giriş parametresi tarafından verilen bir belge ekler ve bir meta veri güncelleştirmeleri kullanarak belge `__.filter()` minSize, maxSize ve giriş belgenin boyut özelliği dayalı totalSize yöntemi.</span><span class="sxs-lookup"><span data-stu-id="53084-274">The stored procedure inserts a document, given by an input parameter, and updates a metadata document, using the `__.filter()` method, with minSize, maxSize, and totalSize based upon the input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent to our callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check the doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get the meta document. We keep it in the same collection. it's the only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed to find the metadata document.");

            // The metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all the rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace the metadata document in the store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read the meta again 
              //       and update again because due to Snapshot isolation we will read same exact version (we are in same transaction).
              //       We have to take care of that on the client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-to-javascript-cheat-sheet"></a><span data-ttu-id="53084-275">SQL Javascript kopya sayfası</span><span class="sxs-lookup"><span data-stu-id="53084-275">SQL to Javascript cheat sheet</span></span>
<span data-ttu-id="53084-276">Aşağıdaki tabloda, çeşitli SQL sorguları ve karşılık gelen JavaScript sorguları gösterir.</span><span class="sxs-lookup"><span data-stu-id="53084-276">The following table presents various SQL queries and the corresponding JavaScript queries.</span></span>

<span data-ttu-id="53084-277">Özellik anahtarları içeren SQL sorguları, belge olarak (örneğin `doc.id`) büyük küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="53084-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="53084-278">SQL</span><span class="sxs-lookup"><span data-stu-id="53084-278">SQL</span></span>| <span data-ttu-id="53084-279">JavaScript sorgu API</span><span class="sxs-lookup"><span data-stu-id="53084-279">JavaScript Query API</span></span>|<span data-ttu-id="53084-280">Aşağıdaki açıklama</span><span class="sxs-lookup"><span data-stu-id="53084-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="53084-281">SEÇİN *</span><span class="sxs-lookup"><span data-stu-id="53084-281">SELECT *</span></span><br><span data-ttu-id="53084-282">Belgelerinden</span><span class="sxs-lookup"><span data-stu-id="53084-282">FROM docs</span></span>| <span data-ttu-id="53084-283">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="53084-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="53084-284">&nbsp;&nbsp;&nbsp;&nbsp;Belge dönüş;</span><span class="sxs-lookup"><span data-stu-id="53084-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="53084-285">});</span><span class="sxs-lookup"><span data-stu-id="53084-285">});</span></span>|<span data-ttu-id="53084-286">1</span><span class="sxs-lookup"><span data-stu-id="53084-286">1</span></span>|
|<span data-ttu-id="53084-287">SELECT docs.id, docs.message olarak msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="53084-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="53084-288">Belgelerinden</span><span class="sxs-lookup"><span data-stu-id="53084-288">FROM docs</span></span>|<span data-ttu-id="53084-289">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="53084-289">__.map(function(doc) {</span></span><br><span data-ttu-id="53084-290">&nbsp;&nbsp;&nbsp;&nbsp;{Döndür</span><span class="sxs-lookup"><span data-stu-id="53084-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="53084-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kimliği: doc.id,</span><span class="sxs-lookup"><span data-stu-id="53084-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="53084-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="53084-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="53084-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Actions:doc.Actions</span><span class="sxs-lookup"><span data-stu-id="53084-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="53084-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="53084-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="53084-295">});</span><span class="sxs-lookup"><span data-stu-id="53084-295">});</span></span>|<span data-ttu-id="53084-296">2</span><span class="sxs-lookup"><span data-stu-id="53084-296">2</span></span>|
|<span data-ttu-id="53084-297">SEÇİN *</span><span class="sxs-lookup"><span data-stu-id="53084-297">SELECT *</span></span><br><span data-ttu-id="53084-298">Belgelerinden</span><span class="sxs-lookup"><span data-stu-id="53084-298">FROM docs</span></span><br><span data-ttu-id="53084-299">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="53084-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="53084-300">__.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="53084-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="53084-301">&nbsp;&nbsp;&nbsp;&nbsp;doc.id iade === "X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="53084-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="53084-302">});</span><span class="sxs-lookup"><span data-stu-id="53084-302">});</span></span>|<span data-ttu-id="53084-303">3</span><span class="sxs-lookup"><span data-stu-id="53084-303">3</span></span>|
|<span data-ttu-id="53084-304">SEÇİN *</span><span class="sxs-lookup"><span data-stu-id="53084-304">SELECT *</span></span><br><span data-ttu-id="53084-305">Belgelerinden</span><span class="sxs-lookup"><span data-stu-id="53084-305">FROM docs</span></span><br><span data-ttu-id="53084-306">WHERE ARRAY_CONTAINS (belgeleri. Etiketler, 123)</span><span class="sxs-lookup"><span data-stu-id="53084-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="53084-307">__.filter(function(x) {</span><span class="sxs-lookup"><span data-stu-id="53084-307">__.filter(function(x) {</span></span><br><span data-ttu-id="53084-308">&nbsp;&nbsp;&nbsp;&nbsp;x.Tags iade & & x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="53084-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="53084-309">});</span><span class="sxs-lookup"><span data-stu-id="53084-309">});</span></span>|<span data-ttu-id="53084-310">4</span><span class="sxs-lookup"><span data-stu-id="53084-310">4</span></span>|
|<span data-ttu-id="53084-311">SELECT docs.id, docs.message msg olarak</span><span class="sxs-lookup"><span data-stu-id="53084-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="53084-312">Belgelerinden</span><span class="sxs-lookup"><span data-stu-id="53084-312">FROM docs</span></span><br><span data-ttu-id="53084-313">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="53084-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="53084-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="53084-314">__.chain()</span></span><br><span data-ttu-id="53084-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="53084-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="53084-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;doc.id iade === "X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="53084-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="53084-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="53084-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="53084-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="53084-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="53084-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{Döndür</span><span class="sxs-lookup"><span data-stu-id="53084-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="53084-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kimliği: doc.id,</span><span class="sxs-lookup"><span data-stu-id="53084-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="53084-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="53084-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="53084-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="53084-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="53084-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="53084-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="53084-324">.Value();</span><span class="sxs-lookup"><span data-stu-id="53084-324">.value();</span></span>|<span data-ttu-id="53084-325">5</span><span class="sxs-lookup"><span data-stu-id="53084-325">5</span></span>|
|<span data-ttu-id="53084-326">DEĞER etiketi</span><span class="sxs-lookup"><span data-stu-id="53084-326">SELECT VALUE tag</span></span><br><span data-ttu-id="53084-327">Belgelerinden</span><span class="sxs-lookup"><span data-stu-id="53084-327">FROM docs</span></span><br><span data-ttu-id="53084-328">Etiket IN belgeleri katılın. Etiketleri</span><span class="sxs-lookup"><span data-stu-id="53084-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="53084-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="53084-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="53084-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="53084-330">__.chain()</span></span><br><span data-ttu-id="53084-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="53084-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="53084-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Belge döndür. Etiketleri & & Array.isArray (belge. Etiketleri);</span><span class="sxs-lookup"><span data-stu-id="53084-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="53084-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="53084-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="53084-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="53084-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="53084-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;doc._ts döndürür;</span><span class="sxs-lookup"><span data-stu-id="53084-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="53084-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="53084-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="53084-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="53084-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="53084-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="53084-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="53084-339">&nbsp;&nbsp;&nbsp;&nbsp;.Value()</span><span class="sxs-lookup"><span data-stu-id="53084-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="53084-340">6</span><span class="sxs-lookup"><span data-stu-id="53084-340">6</span></span>|

<span data-ttu-id="53084-341">Aşağıdaki açıklamaları Yukarıdaki tablodaki her sorgu açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="53084-341">The following descriptions explain each query in the table above.</span></span>
1. <span data-ttu-id="53084-342">Sonuç tüm belgelerde (devamlılık belirteci ile anlatır) olur.</span><span class="sxs-lookup"><span data-stu-id="53084-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="53084-343">Kimliği, ileti (diğer msg için) ve tüm belgeleri eylemden projeleri.</span><span class="sxs-lookup"><span data-stu-id="53084-343">Projects the id, message (aliased to msg), and action from all documents.</span></span>
3. <span data-ttu-id="53084-344">Koşul belgeler için sorgular: kimlik = "X998_Y998".</span><span class="sxs-lookup"><span data-stu-id="53084-344">Queries for documents with the predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="53084-345">Etiketler özelliği ve etiketleri olan belgeler için sorgular 123 değerini içeren bir dizi olur.</span><span class="sxs-lookup"><span data-stu-id="53084-345">Queries for documents that have a Tags property and Tags is an array containing the value 123.</span></span>
5. <span data-ttu-id="53084-346">Sorguları bir koşul ile belgeler için kimliği = "X998_Y998" ve ileti (diğer msg için) ve kimliği projeleri.</span><span class="sxs-lookup"><span data-stu-id="53084-346">Queries for documents with a predicate, id = "X998_Y998", and then projects the id and message (aliased to msg).</span></span>
6. <span data-ttu-id="53084-347">Etiketler, bir dizi özelliği olan belgeler için filtreleri ve elde edilen belgeler _ts zaman damgası sistem özelliği, ardından projeler tarafından sıralar + etiketler dizisi düzleştirir.</span><span class="sxs-lookup"><span data-stu-id="53084-347">Filters for documents which have an array property, Tags, and sorts the resulting documents by the _ts timestamp system property, and then projects + flattens the Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="53084-348">Çalışma zamanı desteği</span><span class="sxs-lookup"><span data-stu-id="53084-348">Runtime support</span></span>
<span data-ttu-id="53084-349">[DocumentDB JavaScript sunucu tarafı API](http://azure.github.io/azure-documentdb-js-server/) tarafından standartlaştırılmış olarak temel JavaScript dil özelliklerinin çoğu için destek sağlayan [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span><span class="sxs-lookup"><span data-stu-id="53084-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for the most of the mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="53084-350">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="53084-350">Security</span></span>
<span data-ttu-id="53084-351">JavaScript saklı yordamları ve Tetikleyicileri korumalı, böylece tek bir betik etkilerini diğer veritabanı düzeyinde snapshot işlem yalıtım üzerinden geçmeden sızıntısı değil.</span><span class="sxs-lookup"><span data-stu-id="53084-351">JavaScript stored procedures and triggers are sandboxed so that the effects of one script do not leak to the other without going through the snapshot transaction isolation at the database level.</span></span> <span data-ttu-id="53084-352">Çalışma zamanı ortamları havuza alınmış ancak sonra her çalışma bağlamında temizlendi.</span><span class="sxs-lookup"><span data-stu-id="53084-352">The runtime environments are pooled but cleaned of the context after each run.</span></span> <span data-ttu-id="53084-353">Bu nedenle bunlar birbirinden herhangi istenmeyen yan etkileri güvenli olması garanti.</span><span class="sxs-lookup"><span data-stu-id="53084-353">Hence they are guaranteed to be safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="53084-354">Ön derleme</span><span class="sxs-lookup"><span data-stu-id="53084-354">Pre-compilation</span></span>
<span data-ttu-id="53084-355">Saklı yordamlar, tetikleyiciler ve UDF'lerin her komut dosyası çağırma aynı anda derleme maliyet önlemek için bayt kodu biçimine örtük olarak önceden derlenmiş.</span><span class="sxs-lookup"><span data-stu-id="53084-355">Stored procedures, triggers and UDFs are implicitly precompiled to the byte code format in order to avoid compilation cost at the time of each script invocation.</span></span> <span data-ttu-id="53084-356">Bu saklı yordam çağrılarını hızlı ve az alan kaplaması sahip sağlar.</span><span class="sxs-lookup"><span data-stu-id="53084-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="53084-357">İstemci SDK'sı desteği</span><span class="sxs-lookup"><span data-stu-id="53084-357">Client SDK support</span></span>
<span data-ttu-id="53084-358">DocumentDB API'si yanı sıra [Node.js](documentdb-sdk-node.md) istemci, Azure Cosmos DB [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), ve [Python SDK'ları](documentdb-sdk-python.md) API DocumentDB için.</span><span class="sxs-lookup"><span data-stu-id="53084-358">In addition to the DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for the DocumentDB API.</span></span> <span data-ttu-id="53084-359">Saklı yordamlar, tetikleyiciler ve UDF'lerin oluşturulabilir ve bu SDK de birini kullanarak çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="53084-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="53084-360">Aşağıdaki örnekte, oluşturma ve .NET İstemcisi'ni kullanarak bir saklı yordam yürütme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="53084-360">The following example shows how to create and execute a stored procedure using the .NET client.</span></span> <span data-ttu-id="53084-361">.NET türleri nasıl JSON olarak saklı yordam içinde geçirilen ve geri okuma unutmayın.</span><span class="sxs-lookup"><span data-stu-id="53084-361">Note how the .NET types are passed into the stored procedure as JSON and read back.</span></span>

    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    

                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }

                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };

    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;

    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "sproc"), document, 1920);


<span data-ttu-id="53084-362">Bu örnek nasıl kullanılacağını göstermektedir [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) için ön tetikleyici ve etkinleştirilmiş tetikleyici ile bir belge oluşturun.</span><span class="sxs-lookup"><span data-stu-id="53084-362">This sample shows how to use the [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) to create a pre-trigger and create a document with the trigger enabled.</span></span> 

    Trigger preTrigger = new Trigger()
    {
        Id = "CapitalizeName",
        Body = @"function() {
            var item = getContext().getRequest().getBody();
            item.id = item.id.toUpperCase();
            getContext().getRequest().setBody(item);
        }",
        TriggerOperation = TriggerOperation.Create,
        TriggerType = TriggerType.Pre
    };

    Document createdItem = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), new Document { Id = "documentdb" },
        new RequestOptions
        {
            PreTriggerInclude = new List<string> { "CapitalizeName" },
        });


<span data-ttu-id="53084-363">Ve aşağıdaki örnekte, kullanıcı tanımlı işlev (UDF) oluşturmak ve bunu kullanmak gösterilmiştir bir [DocumentDB API SQL sorgusu](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="53084-363">And the following example shows how to create a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

    UserDefinedFunction function = new UserDefinedFunction()
    {
        Id = "LOWER",
        Body = @"function(input) 
        {
            return input.toLowerCase();
        }"
    };

    foreach (Book book in client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        "SELECT * FROM Books b WHERE udf.LOWER(b.Title) = 'war and peace'"))
    {
        Console.WriteLine("Read {0} from query", book);
    }

## <a name="rest-api"></a><span data-ttu-id="53084-364">REST API</span><span class="sxs-lookup"><span data-stu-id="53084-364">REST API</span></span>
<span data-ttu-id="53084-365">Tüm Azure Cosmos DB işlemleri RESTful bir şekilde gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="53084-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="53084-366">Saklı yordamlar, tetikleyiciler ve kullanıcı tanımlı işlevler altından bir HTTP POST kullanılarak kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="53084-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="53084-367">Saklı yordam kaydetmek nasıl bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="53084-367">The following is an example of how to register a stored procedure:</span></span>

    POST https://<url>/sprocs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT


    var x = {
      "name": "createAndAddProperty",
      "body": function (docToCreate, addedPropertyName, addedPropertyValue) {
                var collectionManager = getContext().getCollection();
                collectionManager.createDocument(
                    collectionManager.getSelfLink(),
                    docToCreate,
                    function(err, docCreated) {
                      if(err) throw new Error('Error:  ' + err.message);
                      docCreated[addedPropertyName] = addedPropertyValue;
                      getContext().getResponse().setBody(docCreated);
                    });
            }
    }


<span data-ttu-id="53084-368">Saklı yordam oluşturmak için saklı yordam içeren gövde ile bir POST isteği URI dbs/testdb/colls/testColl/sprocs karşı yürüterek kayıtlı değil.</span><span class="sxs-lookup"><span data-stu-id="53084-368">The stored procedure is registered by executing a POST request against the URI dbs/testdb/colls/testColl/sprocs with the body containing the stored procedure to create.</span></span> <span data-ttu-id="53084-369">Tetikleyiciler ve UDF'lerin benzer şekilde bir POST/tetikleyiciler ve /udfs karşı sırasıyla vererek kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="53084-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="53084-370">Bu yordam can depolanan sonra kaynak bağlantısını karşı bir POST isteği göndererek yürütülebilir:</span><span class="sxs-lookup"><span data-stu-id="53084-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of the Patriarch"}, "Price", 200 ]


<span data-ttu-id="53084-371">Burada, saklı yordam giriş istek gövdesinde geçirilir.</span><span class="sxs-lookup"><span data-stu-id="53084-371">Here, the input to the stored procedure is passed in the request body.</span></span> <span data-ttu-id="53084-372">Giriş girdi parametresi bir JSON dizisi olarak geçirilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="53084-372">Note that the input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="53084-373">Saklı yordam ilk girdi yanıt gövdesi bir belge olarak alır.</span><span class="sxs-lookup"><span data-stu-id="53084-373">The stored procedure takes the first input as a document that is a response body.</span></span> <span data-ttu-id="53084-374">Aldığımız yanıt aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="53084-374">The response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of the Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="53084-375">Saklı yordamlar aksine Tetikleyicileri doğrudan yürütülemez.</span><span class="sxs-lookup"><span data-stu-id="53084-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="53084-376">Bunun yerine, bir belge üzerinde bir işlemi bir parçası olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="53084-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="53084-377">Biz HTTP üst bilgilerini kullanarak bir istekle çalıştırmak için Tetikleyiciler belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53084-377">We can specify the triggers to run with a request using HTTP headers.</span></span> <span data-ttu-id="53084-378">Bir belge oluşturma isteği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="53084-378">The following is request to create a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “The Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="53084-379">Burada istekle çalıştırılması için ön tetikleyici x-ms-documentdb-pre-trigger-include üstbilgisinde belirtilir.</span><span class="sxs-lookup"><span data-stu-id="53084-379">Here the pre-trigger to be run with the request is specified in the x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="53084-380">Buna bağlı olarak, hiçbir sonrası tetikleyici x-ms-documentdb-post-trigger-include üst bilgi verilir.</span><span class="sxs-lookup"><span data-stu-id="53084-380">Correspondingly, any post-triggers are given in the x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="53084-381">Unutmayın her ikisi de öncesi ve sonrası tetikleyicileri, belirli bir istek için belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="53084-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="53084-382">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="53084-382">Sample code</span></span>
<span data-ttu-id="53084-383">Daha fazla sunucu tarafı kodu örnekleri bulabilirsiniz (de dahil olmak üzere [toplu silme](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), ve [güncelleştirme](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) üzerinde bizim [GitHub deposunu](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="53084-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="53084-384">Harika, saklı yordam paylaşmak ister misiniz?</span><span class="sxs-lookup"><span data-stu-id="53084-384">Want to share your awesome stored procedure?</span></span> <span data-ttu-id="53084-385">Lütfen bize bir çekme isteği gönderin!</span><span class="sxs-lookup"><span data-stu-id="53084-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="53084-386">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="53084-386">Next steps</span></span>
<span data-ttu-id="53084-387">Bir veya daha fazla saklı yordamlar, tetikleyiciler ve kullanıcı tanımlı işlevler oluşturulan olduktan sonra bunları yükleyin ve Veri Gezgini'ni kullanarak Azure portalında görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="53084-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in the Azure portal using Data Explorer.</span></span>

<span data-ttu-id="53084-388">Aynı zamanda aşağıdaki başvuru ve kaynaklar Azure Cosmos dB sunucu tarafı programlama hakkında daha fazla bilgi için yolundaki yararlı olabilir:</span><span class="sxs-lookup"><span data-stu-id="53084-388">You may also find the following references and resources useful in your path to learn more about Azure Cosmos dB server-side programming:</span></span>

* [<span data-ttu-id="53084-389">Azure Cosmos DB SDK'ları</span><span class="sxs-lookup"><span data-stu-id="53084-389">Azure Cosmos DB SDKs</span></span>](documentdb-sdk-dotnet.md)
* [<span data-ttu-id="53084-390">DocumentDB Studio</span><span class="sxs-lookup"><span data-stu-id="53084-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="53084-391">JSON</span><span class="sxs-lookup"><span data-stu-id="53084-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="53084-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="53084-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="53084-393">Güvenli ve taşınabilir veritabanı genişletilebilirliği</span><span class="sxs-lookup"><span data-stu-id="53084-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="53084-394">Hizmet odaklı veritabanı mimarisi</span><span class="sxs-lookup"><span data-stu-id="53084-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="53084-395">Microsoft SQL Server'da .NET çalışma zamanı barındırma</span><span class="sxs-lookup"><span data-stu-id="53084-395">Hosting the .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

