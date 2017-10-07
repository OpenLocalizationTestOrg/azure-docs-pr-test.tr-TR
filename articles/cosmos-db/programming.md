---
title: "Azure Cosmos DB için aaaServer tarafı JavaScript programlama | Microsoft Docs"
description: "Nasıl toouse Azure Cosmos DB toowrite JavaScript yordamları, veritabanı tetikleyiciler ve kullanıcı tanımlı işlevler (UDF'ler) depolanan bilgi edinin. Veritabanı programing ipuçları ve daha fazla bilgi edinin."
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
ms.openlocfilehash: 5a011d1c4b0b5908d5de73607a1bc328ed1711d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="5aa8b-105">Azure Cosmos DB sunucu tarafı programlama: saklı yordamlar, veritabanı tetikleyiciler ve UDF'lerin</span><span class="sxs-lookup"><span data-stu-id="5aa8b-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="5aa8b-106">Azure Cosmos veritabanı dil nasıl tümleşik öğrenin, JavaScript işlem tabanlı olarak yürütülmesini sağlar yazma geliştiriciler **saklı yordamlar**, **Tetikleyicileri** ve **kullanıcı tanımlı işlevler (UDF'ler)** yerel olarak bir [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="5aa8b-107">Bu, gönderilen ve doğrudan hello veritabanı depolama bölümleri üzerinde yürütülen toowrite veritabanı program uygulama mantığı sağlar.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-107">This allows you toowrite database program application logic that can be shipped and executed directly on hello database storage partitions.</span></span> 

<span data-ttu-id="5aa8b-108">Alma burada Barış Liu kısa giriş tooCosmos DB'ın sunucu tarafı veritabanı programlama modeli sağlar aşağıdaki izledikleri hello tarafından video, başlatılan öneririz.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-108">We recommend getting started by watching hello following video, where Andrew Liu provides a brief introduction tooCosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="5aa8b-109">Ardından, toothis makale, aşağıdaki soruları hello yanıtlar toohello burada öğreneceksiniz döndürün:</span><span class="sxs-lookup"><span data-stu-id="5aa8b-109">Then, return toothis article, where you'll learn hello answers toohello following questions:</span></span>  

* <span data-ttu-id="5aa8b-110">Ne ı yazma bir saklı yordam, tetikleyici veya JavaScript kullanarak UDF?</span><span class="sxs-lookup"><span data-stu-id="5aa8b-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="5aa8b-111">Cosmos DB ACID nasıl garanti?</span><span class="sxs-lookup"><span data-stu-id="5aa8b-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="5aa8b-112">İşlemler Cosmos DB'de nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="5aa8b-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="5aa8b-113">Önceden tetikler ve sonrası tetikler nedir ve nasıl t bir yazma?</span><span class="sxs-lookup"><span data-stu-id="5aa8b-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="5aa8b-114">Nasıl kaydetmek ve HTTP kullanarak bir RESTful şekilde bir saklı yordam, tetikleyici veya UDF yürütme?</span><span class="sxs-lookup"><span data-stu-id="5aa8b-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="5aa8b-115">Ne Cosmos DB SDK'ları kullanılabilir toocreate olan ve yürütme yordamlar, tetikleyiciler ve UDF'lerin depolanan?</span><span class="sxs-lookup"><span data-stu-id="5aa8b-115">What Cosmos DB SDKs are available toocreate and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-toostored-procedure-and-udf-programming"></a><span data-ttu-id="5aa8b-116">Giriş tooStored yordamı ve UDF programlama</span><span class="sxs-lookup"><span data-stu-id="5aa8b-116">Introduction tooStored Procedure and UDF Programming</span></span>
<span data-ttu-id="5aa8b-117">Bu yaklaşım *"JavaScript T-SQL modern gün olarak"* tür sistem uyuşmazlıkları ve nesne ilişkisel eşleme teknolojileri hello karmaşıklığını uygulama geliştiricilerden boşaltır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from hello complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="5aa8b-118">Ayrıca, birkaç kullanılan toobuild zengin uygulamalar olabilir iç avantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="5aa8b-118">It also has a number of intrinsic advantages that can be utilized toobuild rich applications:</span></span>  

* <span data-ttu-id="5aa8b-119">**Yordam mantığı:** üst düzey bir programlama dili olarak JavaScript zengin ve tanıdık arabirimi tooexpress iş mantığı sağlar.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface tooexpress business logic.</span></span> <span data-ttu-id="5aa8b-120">Karmaşık işlemleri daha yakından toohello veri dizisini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-120">You can perform complex sequences of operations closer toohello data.</span></span>
* <span data-ttu-id="5aa8b-121">**Atomik işlemleri:** tek bir saklı yordam veya tetikleyici içinde gerçekleştirilen işlemler veritabanı Cosmos DB garanti atomik.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="5aa8b-122">Bu, tek bir toplu ilgili işlemlerinde bunların tümünün başarılı ya da bunların hiçbiri başarılı birleştirmek bir uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="5aa8b-123">**Performans:** JSON doğası gereği eşlenen toohello Javascript dil tür sistemi ve ayrıca hello temel Cosmos DB depolama biriminin verir iyileştirmeler JSON, yavaş materialization gibi birtakım olduğunu hello olgu hello arabellekte belgeleri Havuz ve kod yürütmek kullanılabilir İsteğe bağlı toohello yapma.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-123">**Performance:** hello fact that JSON is intrinsically mapped toohello Javascript language type system and is also hello basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in hello buffer pool and making them available on-demand toohello executing code.</span></span> <span data-ttu-id="5aa8b-124">Sevkiyat iş mantığı toohello veritabanı ile ilgili daha fazla performans avantajı vardır:</span><span class="sxs-lookup"><span data-stu-id="5aa8b-124">There are more performance benefits associated with shipping business logic toohello database:</span></span>
  
  * <span data-ttu-id="5aa8b-125">Toplu işleme – Geliştiriciler grubu ekleme gibi işlemleri ve toplu olarak gönderin.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="5aa8b-126">Merhaba ağ trafiği gecikmesi maliyet ve hello deposu genel gider toocreate ayrı işlemleri önemli ölçüde azalır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-126">hello network traffic latency cost and hello store overhead toocreate separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="5aa8b-127">Ön derleme – Cosmos DB saklı yordamlar, tetikleyiciler ve kullanıcı tanımlı işlevler (UDF'ler) tooavoid her çağırma için JavaScript derleme maliyeti işlemini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) tooavoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="5aa8b-128">Merhaba hello yordam mantığı için hello bayt kod oluşturma yükünü tooa en az değer amortized.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-128">hello overhead of building hello byte code for hello procedural logic is amortized tooa minimal value.</span></span>
  * <span data-ttu-id="5aa8b-129">Sıralama – birçok işlemleri gerek yan içeren büyük olasılıkla bir veya daha fazla ikincil depolama işlemleri yapılması etki ("tetikleyicisi").</span><span class="sxs-lookup"><span data-stu-id="5aa8b-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="5aa8b-130">Daha fazla kullanıcı budur kararlılık yanı sıra zaman toohello server'ı taşındı.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-130">Aside from atomicity, this is more performant when moved toohello server.</span></span> 
* <span data-ttu-id="5aa8b-131">**Kapsülleme:** saklı yordamlar, tek bir yerde kullanılan toogroup iş mantığı olabilir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-131">**Encapsulation:** Stored procedures can be used toogroup business logic in one place.</span></span> <span data-ttu-id="5aa8b-132">Bu iki avantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="5aa8b-132">This has two advantages:</span></span>
  * <span data-ttu-id="5aa8b-133">Veri mimarları tooevolve uygulamalarını hello veri öğesinden bağımsız olarak etkinleştirir hello ham verileri en üstünde bir soyutlama katmanı ekler.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-133">It adds an abstraction layer on top of hello raw data, which enables data architects tooevolve their applications independently from hello data.</span></span> <span data-ttu-id="5aa8b-134">Merhaba veri toodeal verilerle doğrudan varsa, hello uygulamasına baked toobe gerekebilir toohello kırılır varsayımlar şema küçüktür, bu özellikle yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-134">This is particularly advantageous when hello data is schema-less, due toohello brittle assumptions that may need toobe baked into hello application if they have toodeal with data directly.</span></span>  
  * <span data-ttu-id="5aa8b-135">Bu soyutlama kuruluşların hello komut dosyalarından hello erişimi hızlandırma tarafından verilerine güvenli kalmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-135">This abstraction lets enterprises keep their data secure by streamlining hello access from hello scripts.</span></span>  

<span data-ttu-id="5aa8b-136">Merhaba oluşturma ve yürütme veritabanı tetikleyici, saklı yordam ve özel sorgu işleçleri desteklenir hello [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), ve [istemci SDK'ları](documentdb-sdk-dotnet.md) .NET, Node.js ve JavaScript gibi birçok platformda.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-136">hello creation and execution of database triggers, stored procedure and custom query operators is supported through hello [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="5aa8b-137">Bu öğretici hello kullanır [Node.js SDK'sı ile Q öneriler](http://azure.github.io/azure-documentdb-node-q/) tooillustrate sözdizimi ve saklı yordamlar, tetikleyiciler ve UDF'lerin kullanımı.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-137">This tutorial uses hello [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) tooillustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="5aa8b-138">Saklı yordamlar</span><span class="sxs-lookup"><span data-stu-id="5aa8b-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="5aa8b-139">Örnek: basit bir saklı yordam yazma</span><span class="sxs-lookup"><span data-stu-id="5aa8b-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="5aa8b-140">"Hello World" yanıt veren basit bir saklı yordam ile başlayalım.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="5aa8b-141">Saklı yordamlar koleksiyonu başına kaydedilir ve herhangi bir belge ve ek koleksiyonda mevcut üzerinde çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="5aa8b-142">Merhaba aşağıdaki kod parçacığında nasıl tooregister hello helloWorld saklı yordamı koleksiyonu ile gösterilir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-142">hello following snippet shows how tooregister hello helloWorld stored procedure with a collection.</span></span> 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="5aa8b-143">Hello saklı yordamı kaydedildiğinde, biz hello koleksiyonu karşı yürütün ve hello sonuçları hello istemcide geri okuyun.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-143">Once hello stored procedure is registered, we can execute it against hello collection, and read hello results back at hello client.</span></span> 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="5aa8b-144">Merhaba bağlam nesnesi toohello istek ve yanıt nesnelere erişmek yanı sıra Cosmos DB depolama alanında gerçekleştirilebilir tooall işlemleri erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-144">hello context object provides access tooall operations that can be performed on Cosmos DB storage, as well as access toohello request and response objects.</span></span> <span data-ttu-id="5aa8b-145">Bu durumda, hello yanıt nesnesi tooset hello geri toohello istemci gönderilen hello yanıtın gövdesini kullandık.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-145">In this case, we used hello response object tooset hello body of hello response that was sent back toohello client.</span></span> <span data-ttu-id="5aa8b-146">Daha fazla ayrıntı için toohello başvurun [Azure Cosmos DB JavaScript server SDK Belgeleri](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="5aa8b-146">For more details, refer toohello [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="5aa8b-147">Bize göre bu örnekte genişletin ve daha fazla veritabanı ilgili işlevsellik eklemek toohello saklı yordamı.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-147">Let us expand on this example and add more database related functionality toohello stored procedure.</span></span> <span data-ttu-id="5aa8b-148">Saklı yordamlar oluşturabilir, güncelleştirme, okuma, sorgu ve belgeler ve ekleri hello koleksiyonu içinde silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-148">Stored procedures can create, update, read, query and delete documents and attachments inside hello collection.</span></span>    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a><span data-ttu-id="5aa8b-149">Örnek: bir saklı yordam toocreate bir belge yazma</span><span class="sxs-lookup"><span data-stu-id="5aa8b-149">Example: Write a stored procedure toocreate a document</span></span>
<span data-ttu-id="5aa8b-150">Merhaba sonraki parçacığı nasıl toouse hello bağlam nesnesi toointeract Cosmos DB kaynaklarla gösterir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-150">hello next snippet shows how toouse hello context object toointeract with Cosmos DB resources.</span></span>

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


<span data-ttu-id="5aa8b-151">Bu saklı yordam giriş documentToCreate, hello geçerli Koleksiyonda oluşturulmuş bir belge toobe hello gövdesini alır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-151">This stored procedure takes as input documentToCreate, hello body of a document toobe created in hello current collection.</span></span> <span data-ttu-id="5aa8b-152">Tüm işlemleri zaman uyumsuzdur ve JavaScript işlevi geri aramalar üzerinde bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="5aa8b-153">Merhaba geri çağırma işlevi hello hata nesnesi için iki parametre hello işlemi başarısız olur ve nesne hello için oluşturulan olasılığına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-153">hello callback function has two parameters, one for hello error object in case hello operation fails, and one for hello created object.</span></span> <span data-ttu-id="5aa8b-154">Merhaba geri çağırma içinde kullanıcılar hello özel durumu işlemek ya da bir hata durum.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-154">Inside hello callback, users can either handle hello exception or throw an error.</span></span> <span data-ttu-id="5aa8b-155">Bir geri çağırma değil sağlanır ve bir hata durumunda, hello Azure Cosmos DB çalışma zamanı bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-155">In case a callback is not provided and there is an error, hello Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="5aa8b-156">Merhaba işlemi başarısız olursa hello yukarıdaki örnekte, bir hata hello geri çağırma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-156">In hello example above, hello callback throws an error if hello operation failed.</span></span> <span data-ttu-id="5aa8b-157">Aksi takdirde, belge hello yanıt toohello istemci hello gövdesi olarak oluşturulan hello hello kimliğini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-157">Otherwise, it sets hello id of hello created document as hello body of hello response toohello client.</span></span> <span data-ttu-id="5aa8b-158">İşte bu saklı yordam giriş parametreleriyle nasıl yürütülür.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register hello stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure toocreate a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "hello Hitchhiker’s Guide toohello Galaxy",
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


<span data-ttu-id="5aa8b-159">Bu saklı yordamı Not değiştirilmiş tootake belge gövdeleri bir dizi girişi olarak kullanılabilir ve tüm aynı depolanan hello oluşturma yordamı yürütme birden çok ağ yerine toocreate her biri ayrı ayrı ister.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-159">Note that this stored procedure can be modified tootake an array of document bodies as input and create them all in hello same stored procedure execution instead of multiple network requests toocreate each of them individually.</span></span> <span data-ttu-id="5aa8b-160">Bu, kullanılan tooimplement Cosmos DB (Bu öğreticinin ilerleyen bölümlerinde açıklanmıştır) için bir verimli toplu alıcısı olabilir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-160">This can be used tooimplement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="5aa8b-161">nasıl toouse saklı yordamları açıklanan Merhaba örneği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-161">hello example described demonstrated how toouse stored procedures.</span></span> <span data-ttu-id="5aa8b-162">Daha sonra hello öğreticide biz tetikleyiciler ve kullanıcı tanımlı işlevler (UDF'ler) ele alınacaktır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-162">We will cover triggers and user defined functions (UDFs) later in hello tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="5aa8b-163">Veritabanı program işlemleri</span><span class="sxs-lookup"><span data-stu-id="5aa8b-163">Database program transactions</span></span>
<span data-ttu-id="5aa8b-164">Tipik bir veritabanında işlem tek bir mantıksal birim iş olarak gerçekleştirilen işlemler dizisi olarak tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="5aa8b-165">Her işlem sağlar **ACID garanti**.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="5aa8b-166">ACID dört özellikleri - kararlılık, tutarlılık, yalıtım ve dayanıklılık anlamına gelir iyi bilinen bir kısaltma ' dir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="5aa8b-167">Kısaca, bir işlem içinde yapılan tüm hello iş tek bir birim olarak davranılır kararlılık garanti burada ya da tamamını kaydedilmiş veya yok.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-167">Briefly, atomicity guarantees that all hello work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="5aa8b-168">Tutarlılık hello veri işlemleri arasında her zaman iyi bir iç durumda olduğundan emin olur.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-168">Consistency makes sure that hello data is always in a good internal state across transactions.</span></span> <span data-ttu-id="5aa8b-169">Yalıtım iki işlem birbiriyle – genellikle etkilemesine, çoğu ticari sistemleri kullanılabilir birden çok yalıtım düzeyi hello uygulama gereksinimlerine göre sağlayın güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on hello application needs.</span></span> <span data-ttu-id="5aa8b-170">Dayanıklılık hello veritabanında kaydedilen herhangi bir değişiklik her zaman mevcut olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-170">Durability ensures that any change that’s committed in hello database will always be present.</span></span>   

<span data-ttu-id="5aa8b-171">Cosmos DB'de JavaScript hello barındırılan hello veritabanı olarak aynı bellek alanı.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-171">In Cosmos DB, JavaScript is hosted in hello same memory space as hello database.</span></span> <span data-ttu-id="5aa8b-172">Bu nedenle, saklı yordamları ve Tetikleyicileri içinde yapılan istekleri hello aynı yürütme veritabanı oturumun kapsamı.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-172">Hence, requests made within stored procedures and triggers execute in hello same scope of a database session.</span></span> <span data-ttu-id="5aa8b-173">Bu, tek bir saklı yordam/tetikleyici parçası olan tüm işlemleri için Cosmos DB tooguarantee ACID sağlar.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-173">This enables Cosmos DB tooguarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="5aa8b-174">Merhaba aşağıdakileri göz önünde bulundurun saklı yordamı tanımı:</span><span class="sxs-lookup"><span data-stu-id="5aa8b-174">Consider hello following stored procedure definition:</span></span>

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

                    if (documents.length != 1) throw "Unable toofind both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable toofind both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable tooread player details, abort ";
                });

            if (!accept) throw "Unable tooread player details, abort ";

            // swap hello two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable tooupdate player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable tooupdate player 2, abort"
                            });

                        if (!accept2) throw "Unable tooupdate player 2, abort";
                    });

                if (!accept) throw "Unable tooupdate player 1, abort";
            }
        }
    }

    // register hello stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="5aa8b-175">Bu saklı yordam işlemlerini tek bir işlemde iki oyuncu arasında oyun uygulaması tootrade öğe içinde kullanır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-175">This stored procedure uses transactions within a gaming app tootrade items between two players in a single operation.</span></span> <span data-ttu-id="5aa8b-176">Merhaba yordamı denemeleri tooread iki belge karşılık gelen her toohello player kimlikleri bağımsız değişken olarak geçirilen depolanır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-176">hello stored procedure attempts tooread two documents each corresponding toohello player IDs passed in as an argument.</span></span> <span data-ttu-id="5aa8b-177">Her iki player belge bulunamazsa, hello saklı yordamı öğelerin takas tarafından hello belgeleri güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-177">If both player documents are found, then hello stored procedure updates hello documents by swapping their items.</span></span> <span data-ttu-id="5aa8b-178">Merhaba yol boyunca herhangi bir hatayla karşılaşılmazsa örtük olarak hello işlemi iptal bir JavaScript özel durumu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-178">If any errors are encountered along hello way, it throws a JavaScript exception that implicitly aborts hello transaction.</span></span>

<span data-ttu-id="5aa8b-179">Merhaba koleksiyonu hello saklı yordamı kaydedilmişse karşı tek bölümlü bir koleksiyon olduğu sonra hello kapsamlı tooall hello belgeleri hello koleksiyonundaki bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-179">If hello collection hello stored procedure is registered against is a single-partition collection, then hello transaction is scoped tooall hello documents within hello collection.</span></span> <span data-ttu-id="5aa8b-180">Merhaba koleksiyon bölümlendiğinde ise, saklı yordamlar hello işlem kapsamında tek bölüm anahtarı yürütülür.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-180">If hello collection is partitioned, then stored procedures are executed in hello transaction scope of a single partition key.</span></span> <span data-ttu-id="5aa8b-181">Her saklı yordam yürütme ardından karşılık gelen toohello kapsam hello işlem altında çalıştırmalısınız bir bölüm anahtarı değerini içermelidir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-181">Each stored procedure execution must then include a partition key value corresponding toohello scope hello transaction must run under.</span></span> <span data-ttu-id="5aa8b-182">Daha fazla ayrıntı için bkz: [Azure DB Cosmos bölümleme](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="5aa8b-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="5aa8b-183">Kaydetme ve geri alma</span><span class="sxs-lookup"><span data-stu-id="5aa8b-183">Commit and rollback</span></span>
<span data-ttu-id="5aa8b-184">İşlemleri iç ve yerel olarak Cosmos veritabanı JavaScript programlama modeline tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="5aa8b-185">JavaScript işlevinin içinde tüm işlemleri otomatik olarak tek bir işlem altında sarılır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="5aa8b-186">Merhaba JavaScript herhangi bir özel durum olmadan tamamlarsa hello operations toohello veritabanı kaydedilmiş.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-186">If hello JavaScript completes without any exception, hello operations toohello database are committed.</span></span> <span data-ttu-id="5aa8b-187">İlişkisel veritabanları hello "BEGIN TRANSACTION" ve "COMMIT TRANSACTION" deyimleri Cosmos DB'de örtük etkindir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-187">In effect, hello “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="5aa8b-188">Merhaba betikten yayılır herhangi bir özel durum ise, Cosmos veritabanı JavaScript çalışma zamanı hello tüm işlem döndürülmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-188">If there is any exception that’s propagated from hello script, Cosmos DB’s JavaScript runtime will roll back hello whole transaction.</span></span> <span data-ttu-id="5aa8b-189">Hello daha önce gösterildiği gibi bir özel durum atma, etkili bir şekilde eşdeğer tooa Cosmos DB "geri alma işlemi" örnektir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-189">As shown in hello earlier example, throwing an exception is effectively equivalent tooa “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="5aa8b-190">Veri tutarlılığı</span><span class="sxs-lookup"><span data-stu-id="5aa8b-190">Data consistency</span></span>
<span data-ttu-id="5aa8b-191">Saklı yordamları ve Tetikleyicileri hello Azure Cosmos DB kapsayıcısının hello birincil Çoğaltmada her zaman yürütülür.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-191">Stored procedures and triggers are always executed on hello primary replica of hello Azure Cosmos DB container.</span></span> <span data-ttu-id="5aa8b-192">Bu, okuma içindeki yordamları teklif güçlü tutarlılık depolanan sağlar.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="5aa8b-193">Kullanıcı tanımlı işlevler kullanarak sorguları hello birincil veya ikincil bir çoğaltma üzerinde çalıştırılabilir, ancak biz toomeet olun hello hello uygun çoğaltma seçerek tutarlılık düzeyi istendi.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-193">Queries using user defined functions can be executed on hello primary or any secondary replica, but we ensure toomeet hello requested consistency level by choosing hello appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="5aa8b-194">Sınırlanmış yürütme</span><span class="sxs-lookup"><span data-stu-id="5aa8b-194">Bounded execution</span></span>
<span data-ttu-id="5aa8b-195">Tüm Cosmos DB işlemleri hello server'ın içinde belirtilen tamamlamalısınız isteği zaman aşımı süresi.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-195">All Cosmos DB operations must complete within hello server specified request timeout duration.</span></span> <span data-ttu-id="5aa8b-196">Bu sınırlama tooJavaScript işlevleri (saklı yordamlar, tetikleyiciler ve kullanıcı tanımlı işlevler) de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-196">This constraint also applies tooJavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="5aa8b-197">Bir işlem bu zaman sınırı ile tamamlanmazsa hello işlem geri alındı.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-197">If an operation does not complete with that time limit, hello transaction is rolled back.</span></span> <span data-ttu-id="5aa8b-198">JavaScript işlevleri hello süre sınırı içinde son veya bir temel devamlılık modeli toobatch/sürdürmeden yürütme uygulamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-198">JavaScript functions must finish within hello time limit or implement a continuation based model toobatch/resume execution.</span></span>  

<span data-ttu-id="5aa8b-199">Sipariş toosimplify geliştirme saklı yordamları ve Tetikleyicileri toohandle saat sınırlarının, hello koleksiyon nesnesi (oluşturma, okuma, değiştirme ve silme belgeler ve eklerin) altında tüm işlevleri temsil eden bir Boole değeri döndürür. olup olmadığını, işlemi tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-199">In order toosimplify development of stored procedures and triggers toohandle time limits, all functions under hello collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="5aa8b-200">Bu değeri false ise, onu tooexpire hakkında hello zaman sınırı yoktur ve bu hello yordamı yürütme sarmalamanız gerekir göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-200">If this value is false, it is an indication that hello time limit is about tooexpire and that hello procedure must wrap up execution.</span></span>  <span data-ttu-id="5aa8b-201">Operations sıraya alınan önceki toohello ilk kabul edilmeyen deposu işlemi garanti edilir toocomplete hello saklı yordamı zamanında tamamlandıktan ve başka istek sıra değil.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-201">Operations queued prior toohello first unaccepted store operation are guaranteed toocomplete if hello stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="5aa8b-202">JavaScript işlevleri de kaynak tüketimine ilişkin ilişkisindeki.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="5aa8b-203">Cosmos DB işleme sağlanan hello bir veritabanı hesabı boyutuna göre koleksiyon başına ayırır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-203">Cosmos DB reserves throughput per collection based on hello provisioned size of a database account.</span></span> <span data-ttu-id="5aa8b-204">Üretilen iş CPU, bellek ve g/ç tüketim istek birimleri veya RUs adlı normalleştirilmiş bir birim cinsinden ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="5aa8b-205">JavaScript işlevleri potansiyel olarak çok sayıda RUs kısa bir süre içinde yukarı kullanabilirsiniz ve oranı hello koleksiyonunun sınırına ulaşıldığında sınırlı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if hello collection’s limit is reached.</span></span> <span data-ttu-id="5aa8b-206">Kaynak yoğunluklu saklı yordamlar, ilkel veritabanı işlemleri karantinaya alınan tooensure kullanılabilirliğini de olabilir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-206">Resource intensive stored procedures might also be quarantined tooensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="5aa8b-207">Örnek: toplu bir veritabanı programa veri alma</span><span class="sxs-lookup"><span data-stu-id="5aa8b-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="5aa8b-208">Aşağıda, bir koleksiyona toobulk alma belgeleri yazılmış bir saklı yordam örneğidir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-208">Below is an example of a stored procedure that is written toobulk-import documents into a collection.</span></span> <span data-ttu-id="5aa8b-209">Not hello Boolean denetleyerek yordam ilişkisindeki tanıtıcıları yürütme hello depolanan nasıl dönüş değeri createDocument ve ardından kullanır hello saklı yordamı tootrack ve sürdürme ilerleme her çalıştırılışı toplu eklenen belge sayısını hello.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-209">Note how hello stored procedure handles bounded execution by checking hello Boolean return value from createDocument, and then uses hello count of documents inserted in each invocation of hello stored procedure tootrack and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // hello count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("hello array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call hello create API toocreate a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) hello createDocument request was not accepted. 
        //    In this case hello callback will not be called, we just call setBody and we are done.
        // 2) hello callback was called docs.length times.
        //    In this case all documents were created and we don’t need toocall tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If hello request was accepted, callback will be called.
            // Otherwise report current count back toohello client, 
            // which will call hello script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order tooprocess hello result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment hello count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set hello response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="5aa8b-210"><a id="trigger"></a>Veritabanı Tetikleyicileri</span><span class="sxs-lookup"><span data-stu-id="5aa8b-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="5aa8b-211">Veritabanı öncesi Tetikleyicileri</span><span class="sxs-lookup"><span data-stu-id="5aa8b-211">Database pre-triggers</span></span>
<span data-ttu-id="5aa8b-212">Cosmos DB yürütülen ya da bir belge üzerinde bir işlemi tarafından tetiklenen Tetikleyiciler sağlar.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="5aa8b-213">Örneğin, ön tetikleyici belirtebilmeniz için bir belge oluşturma – hello belge oluşturulmadan önce bu ön tetikleyici çalışacak olduğunda.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before hello document is created.</span></span> <span data-ttu-id="5aa8b-214">Merhaba, ön Tetikleyiciler kullanılan toovalidate hello oluşturulmakta olan bir belgenin özelliklerini nasıl olabilir örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="5aa8b-214">hello following is an example of how pre-triggers can be used toovalidate hello properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document toobe created in hello current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update hello document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="5aa8b-215">Ve Node.js istemci tarafı kaydı kodu hello tetikleyici için karşılık gelen hello:</span><span class="sxs-lookup"><span data-stu-id="5aa8b-215">And hello corresponding Node.js client-side registration code for hello trigger:</span></span>

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


<span data-ttu-id="5aa8b-216">Giriş parametreleri öncesi tetikleyici bulunamaz.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="5aa8b-217">Merhaba istek nesnesi kullanılan toomanipulate hello istek iletisi hello işlemle ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-217">hello request object can be used toomanipulate hello request message associated with hello operation.</span></span> <span data-ttu-id="5aa8b-218">Burada, hello öncesi tetikleyici belgeyi hello oluşturma ile çalıştırın ve JSON biçiminde oluşturulan hello belge toobe hello istek ileti gövdesi içerir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-218">Here, hello pre-trigger is being run with hello creation of a document, and hello request message body contains hello document toobe created in JSON format.</span></span>   

<span data-ttu-id="5aa8b-219">Tetikleyiciler kayıtlı olduğunda, kullanıcılar ile çalıştırabilirsiniz hello operations belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-219">When triggers are registered, users can specify hello operations that it can run with.</span></span> <span data-ttu-id="5aa8b-220">Bu tetikleyici hello aşağıdaki izin anlamına gelir TriggerOperation.Create ile oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-220">This trigger was created with TriggerOperation.Create, which means hello following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="5aa8b-221">Veritabanı sonrası Tetikleyicileri</span><span class="sxs-lookup"><span data-stu-id="5aa8b-221">Database post-triggers</span></span>
<span data-ttu-id="5aa8b-222">Ön tetikleyiciler gibi sonrası Tetikleyicileri bir belge üzerinde bir işlemi ile ilişkili ve giriş parametreleri gerçekleştirin yok.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="5aa8b-223">Çalışırlar **sonra** hello işleminin tamamlandığını ve toohello istemci gönderilen erişim toohello yanıt iletisi vardır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-223">They run **after** hello operation has completed, and have access toohello response message that is sent toohello client.</span></span>   

<span data-ttu-id="5aa8b-224">Aşağıdaki örneğine hello sonrası Tetikleyicileri eylemde gösterir:</span><span class="sxs-lookup"><span data-stu-id="5aa8b-224">hello following example shows post-triggers in action:</span></span>

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
            if(!accept) throw "Unable tooupdate metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable toofind metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable tooupdate metadata, abort";
                               });
                         if(!accept) throw "Unable tooupdate metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="5aa8b-225">Merhaba tetikleyici hello örnek aşağıdaki gösterildiği gibi kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-225">hello trigger can be registered as shown in hello following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "hello Band",
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


<span data-ttu-id="5aa8b-226">Bu tetikleyici hello meta veri belgesi için sorgular ve yeni oluşturulan hello belge hakkında ayrıntılarla güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-226">This trigger queries for hello metadata document and updates it with details about hello newly created document.</span></span>  

<span data-ttu-id="5aa8b-227">Toonote hello olan önemli bir şey **işlem** Cosmos DB Tetikleyicileri yürütülmesi.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-227">One thing that is important toonote is hello **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="5aa8b-228">Bu sonrası tetikleyici hello bir parçası olarak çalışır hello oluşturma hello orijinal belgenin olarak aynı işlem.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-228">This post-trigger runs as part of hello same transaction as hello creation of hello original document.</span></span> <span data-ttu-id="5aa8b-229">Bu nedenle, biz hello sonrası tetikleyiciyle (biz oluşturulamıyor tooupdate hello meta veri belgesi varsa say) bir özel durum, hello tüm işlem başarısız olur ve geri alındı.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-229">Therefore, if we throw an exception from hello post-trigger (say if we are unable tooupdate hello metadata document), hello whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="5aa8b-230">Bir belge oluşturulur ve bir özel durum döndürdü.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="5aa8b-231"><a id="udf"></a>Kullanıcı tanımlı işlevler</span><span class="sxs-lookup"><span data-stu-id="5aa8b-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="5aa8b-232">Kullanıcı tanımlı işlevler (UDF'ler) kullanılan tooextend hello DocumentDB API SQL Sorgu Dili Dilbilgisi olan ve özel iş mantığını uygular.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-232">User-defined functions (UDFs) are used tooextend hello DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="5aa8b-233">Öğesinden yalnızca çağrılabilir sorguları içinde.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-233">They can only be called from inside queries.</span></span> <span data-ttu-id="5aa8b-234">Bunlar erişim toohello bağlam nesnesi yoktur ve yalnızca işlem JavaScript kullanılan toobe yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-234">They do not have access toohello context object and are meant toobe used as compute-only JavaScript.</span></span> <span data-ttu-id="5aa8b-235">Bu nedenle, UDF'ler hello Cosmos DB hizmet ikincil çoğaltmalar üzerinde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-235">Therefore, UDFs can be run on secondary replicas of hello Cosmos DB service.</span></span>  

<span data-ttu-id="5aa8b-236">Hello aşağıdaki örnek çeşitli gelir köşeli için hızlarını dayalı bir UDF toocalculate gelir vergi oluşturur ve ardından sorgu toofind içinde birden fazla $20.000 vergiler Ücretli tüm kişilerin kullanır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-236">hello following sample creates a UDF toocalculate income tax based on rates for various income brackets, and then uses it inside a query toofind all people who paid more than $20,000 in taxes.</span></span>

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


<span data-ttu-id="5aa8b-237">Merhaba UDF sonradan hello örnek aşağıdaki gibi sorgularında kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="5aa8b-237">hello UDF can subsequently be used in queries like in hello following sample:</span></span>

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

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="5aa8b-238">JavaScript dil ile tümleşik sorgu API</span><span class="sxs-lookup"><span data-stu-id="5aa8b-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="5aa8b-239">Ayrıca Documentdb'nin SQL dil bilgisinin kullanarak tooissuing sorguları hello sunucu tarafı SDK'sı SQL bilgisi olmadan fluent JavaScript arabirimi kullanarak en iyi duruma getirilmiş tooperform sorguları sağlar.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-239">In addition tooissuing queries using DocumentDB’s SQL grammar, hello server-side SDK allows you tooperform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="5aa8b-240">API tooprogrammatically yapı sorguları chainable işlevdeki geçirme koşul işlevleri sağlar hello JavaScript sorgu bir söz dizimi hakkında bilgi sahibi tooECMAScript5's dizi öğelerin ve lodash gibi popüler JavaScript kitaplıkları ile çağırır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-240">hello JavaScript query API allows you tooprogrammatically build queries by passing predicate functions into chainable function calls, with a syntax familiar tooECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="5aa8b-241">Sorgular tarafından hello JavaScript çalışma zamanı toobe verimli bir şekilde Azure Cosmos veritabanı dizinlerini kullanılarak yürütülen ayrıştırılır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-241">Queries are parsed by hello JavaScript runtime toobe executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="5aa8b-242">`__`(çift alt çizgi) olan bir diğer ad çok`getContext().getCollection()`.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-242">`__` (double-underscore) is an alias too`getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="5aa8b-243">Diğer bir deyişle, kullanabileceğiniz `__` veya `getContext().getCollection()` tooaccess hello JavaScript sorgu API.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-243">In other words, you can use `__` or `getContext().getCollection()` tooaccess hello JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="5aa8b-244">Desteklenen işlevler aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="5aa8b-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="5aa8b-245">
<b>... chain(). değeri ([geri çağırma] [, Seçenekleri])</b>
</span><span class="sxs-lookup"><span data-stu-id="5aa8b-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="5aa8b-246">İle bitmelidir bir zincirleme çağrısını Value()) ile başlar.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5aa8b-247">
<b>Filtre (predicateFunction [, Seçenekleri] [, geri çağırma])</b>
</span><span class="sxs-lookup"><span data-stu-id="5aa8b-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5aa8b-248">True/false sipariş toofilter giriş/çıkış giriş belgeleri hello sonuç kümesi olarak döndüren bir koşul işlevini kullanarak giriş hello filtreler.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-248">Filters hello input using a predicate function which returns true/false in order toofilter in/out input documents into hello resulting set.</span></span> <span data-ttu-id="5aa8b-249">Bu benzer tooa davranır SQL WHERE yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-249">This behaves similar tooa WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5aa8b-250">
<b>Harita (transformationFunction [, Seçenekleri] [, geri çağırma])</b>
</span><span class="sxs-lookup"><span data-stu-id="5aa8b-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5aa8b-251">Her bir giriş öğesini tooa JavaScript nesne veya değer eşleştiren bir dönüşüm işlevi verilen bir yansıtma geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-251">Applies a projection given a transformation function which maps each input item tooa JavaScript object or value.</span></span> <span data-ttu-id="5aa8b-252">Benzer tooa SELECT yan tümcesinde SQL davranır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-252">This behaves similar tooa SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5aa8b-253">
<b>pluck ([propertyName] [, Seçenekleri] [, geri çağırma])</b>
</span><span class="sxs-lookup"><span data-stu-id="5aa8b-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5aa8b-254">Her giriş öğesinden hello tek bir özellik değerini ayıklayan bir harita için bir kısayol budur.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-254">This is a shortcut for a map which extracts hello value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5aa8b-255">
<b>düzleştirmek ([isShallow] [, Seçenekleri] [, geri çağırma])</b>
</span><span class="sxs-lookup"><span data-stu-id="5aa8b-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5aa8b-256">Birleştirir ve diziler tooa tek dizisindeki her giriş öğesinden düzleştirir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-256">Combines and flattens arrays from each input item in tooa single array.</span></span> <span data-ttu-id="5aa8b-257">LINQ benzer tooSelectMany davranır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-257">This behaves similar tooSelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5aa8b-258">
<b>sortBy ([koşulu] [, Seçenekleri] [, geri çağırma])</b>
</span><span class="sxs-lookup"><span data-stu-id="5aa8b-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5aa8b-259">Yeni belgeler birtakım koşulu verilen hello kullanarak artan hello giriş belgesi akış hello belgelerde sıralayarak üretir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-259">Produce a new set of documents by sorting hello documents in hello input document stream in ascending order using hello given predicate.</span></span> <span data-ttu-id="5aa8b-260">Benzer tooa ORDER BY yan tümcesinde SQL davranır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-260">This behaves similar tooa ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="5aa8b-261">
<b>sortByDescending ([koşulu] [, Seçenekleri] [, geri çağırma])</b>
</span><span class="sxs-lookup"><span data-stu-id="5aa8b-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="5aa8b-262">Yeni belgeler birtakım koşulu verilen hello kullanarak azalan hello giriş belgesi akış hello belgelerde sıralayarak üretir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-262">Produce a new set of documents by sorting hello documents in hello input document stream in descending order using hello given predicate.</span></span> <span data-ttu-id="5aa8b-263">Benzer tooa x DESC ORDER BY yan tümcesi SQL davranır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-263">This behaves similar tooa ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="5aa8b-264">Koşul ve/veya Seçici işlevlerinin içine dahil edilirse, hello aşağıdaki JavaScript yapılarından otomatik olarak en iyi duruma getirilmiş toorun doğrudan Azure Cosmos DB dizinlerini alın:</span><span class="sxs-lookup"><span data-stu-id="5aa8b-264">When included inside predicate and/or selector functions, hello following JavaScript constructs get automatically optimized toorun directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="5aa8b-265">Basit işleçleri: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="5aa8b-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="5aa8b-266">Merhaba nesne değişmez değer de dahil olmak üzere değişmez değerler: {}</span><span class="sxs-lookup"><span data-stu-id="5aa8b-266">Literals, including hello object literal: {}</span></span>
* <span data-ttu-id="5aa8b-267">dönüş var</span><span class="sxs-lookup"><span data-stu-id="5aa8b-267">var, return</span></span>

<span data-ttu-id="5aa8b-268">şu JavaScript oluşturur hello en iyi duruma getirilmezse Azure Cosmos DB dizinler için:</span><span class="sxs-lookup"><span data-stu-id="5aa8b-268">hello following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="5aa8b-269">Denetim akışı (örn. Eğer, sırada)</span><span class="sxs-lookup"><span data-stu-id="5aa8b-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="5aa8b-270">İşlev çağrıları</span><span class="sxs-lookup"><span data-stu-id="5aa8b-270">Function calls</span></span>

<span data-ttu-id="5aa8b-271">Daha fazla bilgi için lütfen bkz bizim [sunucu tarafı JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="5aa8b-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a><span data-ttu-id="5aa8b-272">Örnek: Merhaba JavaScript sorgu API kullanarak bir saklı yordam yazma</span><span class="sxs-lookup"><span data-stu-id="5aa8b-272">Example: Write a stored procedure using hello JavaScript query API</span></span>
<span data-ttu-id="5aa8b-273">Aşağıdaki kod örneği hello hello JavaScript sorgu API hello bir saklı yordam bağlamında nasıl kullanılabileceği bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-273">hello following code sample is an example of how hello JavaScript Query API can be used in hello context of a stored procedure.</span></span> <span data-ttu-id="5aa8b-274">Merhaba saklı yordamı bir giriş parametresi tarafından verilen bir belge ekler ve hello kullanarak bir meta veri belgesi güncelleştirmeleri `__.filter()` minSize, maxSize ve hello giriş belgenin boyut özelliği dayalı totalSize yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-274">hello stored procedure inserts a document, given by an input parameter, and updates a metadata document, using hello `__.filter()` method, with minSize, maxSize, and totalSize based upon hello input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent tooour callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check hello doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get hello meta document. We keep it in hello same collection. it's hello only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed toofind hello metadata document.");

            // hello metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all hello rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace hello metadata document in hello store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read hello meta again 
              //       and update again because due tooSnapshot isolation we will read same exact version (we are in same transaction).
              //       We have tootake care of that on hello client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-toojavascript-cheat-sheet"></a><span data-ttu-id="5aa8b-275">SQL tooJavascript kopya sayfası</span><span class="sxs-lookup"><span data-stu-id="5aa8b-275">SQL tooJavascript cheat sheet</span></span>
<span data-ttu-id="5aa8b-276">Merhaba aşağıdaki tabloda çeşitli SQL sorguları ve hello karşılık gelen JavaScript sorguları gösterir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-276">hello following table presents various SQL queries and hello corresponding JavaScript queries.</span></span>

<span data-ttu-id="5aa8b-277">Özellik anahtarları içeren SQL sorguları, belge olarak (örneğin `doc.id`) büyük küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="5aa8b-278">SQL</span><span class="sxs-lookup"><span data-stu-id="5aa8b-278">SQL</span></span>| <span data-ttu-id="5aa8b-279">JavaScript sorgu API</span><span class="sxs-lookup"><span data-stu-id="5aa8b-279">JavaScript Query API</span></span>|<span data-ttu-id="5aa8b-280">Aşağıdaki açıklama</span><span class="sxs-lookup"><span data-stu-id="5aa8b-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="5aa8b-281">SEÇİN *</span><span class="sxs-lookup"><span data-stu-id="5aa8b-281">SELECT *</span></span><br><span data-ttu-id="5aa8b-282">Belgelerinden</span><span class="sxs-lookup"><span data-stu-id="5aa8b-282">FROM docs</span></span>| <span data-ttu-id="5aa8b-283">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5aa8b-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="5aa8b-284">&nbsp;&nbsp;&nbsp;&nbsp;Belge dönüş;</span><span class="sxs-lookup"><span data-stu-id="5aa8b-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="5aa8b-285">});</span><span class="sxs-lookup"><span data-stu-id="5aa8b-285">});</span></span>|<span data-ttu-id="5aa8b-286">1</span><span class="sxs-lookup"><span data-stu-id="5aa8b-286">1</span></span>|
|<span data-ttu-id="5aa8b-287">SELECT docs.id, docs.message olarak msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="5aa8b-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="5aa8b-288">Belgelerinden</span><span class="sxs-lookup"><span data-stu-id="5aa8b-288">FROM docs</span></span>|<span data-ttu-id="5aa8b-289">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5aa8b-289">__.map(function(doc) {</span></span><br><span data-ttu-id="5aa8b-290">&nbsp;&nbsp;&nbsp;&nbsp;{Döndür</span><span class="sxs-lookup"><span data-stu-id="5aa8b-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="5aa8b-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kimliği: doc.id,</span><span class="sxs-lookup"><span data-stu-id="5aa8b-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="5aa8b-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="5aa8b-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="5aa8b-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Actions:doc.Actions</span><span class="sxs-lookup"><span data-stu-id="5aa8b-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="5aa8b-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="5aa8b-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="5aa8b-295">});</span><span class="sxs-lookup"><span data-stu-id="5aa8b-295">});</span></span>|<span data-ttu-id="5aa8b-296">2</span><span class="sxs-lookup"><span data-stu-id="5aa8b-296">2</span></span>|
|<span data-ttu-id="5aa8b-297">SEÇİN *</span><span class="sxs-lookup"><span data-stu-id="5aa8b-297">SELECT *</span></span><br><span data-ttu-id="5aa8b-298">Belgelerinden</span><span class="sxs-lookup"><span data-stu-id="5aa8b-298">FROM docs</span></span><br><span data-ttu-id="5aa8b-299">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="5aa8b-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="5aa8b-300">__.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5aa8b-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="5aa8b-301">&nbsp;&nbsp;&nbsp;&nbsp;doc.id iade === "X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="5aa8b-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="5aa8b-302">});</span><span class="sxs-lookup"><span data-stu-id="5aa8b-302">});</span></span>|<span data-ttu-id="5aa8b-303">3</span><span class="sxs-lookup"><span data-stu-id="5aa8b-303">3</span></span>|
|<span data-ttu-id="5aa8b-304">SEÇİN *</span><span class="sxs-lookup"><span data-stu-id="5aa8b-304">SELECT *</span></span><br><span data-ttu-id="5aa8b-305">Belgelerinden</span><span class="sxs-lookup"><span data-stu-id="5aa8b-305">FROM docs</span></span><br><span data-ttu-id="5aa8b-306">WHERE ARRAY_CONTAINS (belgeleri. Etiketler, 123)</span><span class="sxs-lookup"><span data-stu-id="5aa8b-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="5aa8b-307">__.filter(function(x) {</span><span class="sxs-lookup"><span data-stu-id="5aa8b-307">__.filter(function(x) {</span></span><br><span data-ttu-id="5aa8b-308">&nbsp;&nbsp;&nbsp;&nbsp;x.Tags iade & & x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="5aa8b-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="5aa8b-309">});</span><span class="sxs-lookup"><span data-stu-id="5aa8b-309">});</span></span>|<span data-ttu-id="5aa8b-310">4</span><span class="sxs-lookup"><span data-stu-id="5aa8b-310">4</span></span>|
|<span data-ttu-id="5aa8b-311">SELECT docs.id, docs.message msg olarak</span><span class="sxs-lookup"><span data-stu-id="5aa8b-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="5aa8b-312">Belgelerinden</span><span class="sxs-lookup"><span data-stu-id="5aa8b-312">FROM docs</span></span><br><span data-ttu-id="5aa8b-313">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="5aa8b-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="5aa8b-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="5aa8b-314">__.chain()</span></span><br><span data-ttu-id="5aa8b-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5aa8b-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="5aa8b-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;doc.id iade === "X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="5aa8b-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="5aa8b-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="5aa8b-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="5aa8b-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5aa8b-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="5aa8b-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{Döndür</span><span class="sxs-lookup"><span data-stu-id="5aa8b-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="5aa8b-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kimliği: doc.id,</span><span class="sxs-lookup"><span data-stu-id="5aa8b-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="5aa8b-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="5aa8b-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="5aa8b-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="5aa8b-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="5aa8b-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="5aa8b-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="5aa8b-324">.Value();</span><span class="sxs-lookup"><span data-stu-id="5aa8b-324">.value();</span></span>|<span data-ttu-id="5aa8b-325">5</span><span class="sxs-lookup"><span data-stu-id="5aa8b-325">5</span></span>|
|<span data-ttu-id="5aa8b-326">DEĞER etiketi</span><span class="sxs-lookup"><span data-stu-id="5aa8b-326">SELECT VALUE tag</span></span><br><span data-ttu-id="5aa8b-327">Belgelerinden</span><span class="sxs-lookup"><span data-stu-id="5aa8b-327">FROM docs</span></span><br><span data-ttu-id="5aa8b-328">Etiket IN belgeleri katılın. Etiketleri</span><span class="sxs-lookup"><span data-stu-id="5aa8b-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="5aa8b-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="5aa8b-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="5aa8b-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="5aa8b-330">__.chain()</span></span><br><span data-ttu-id="5aa8b-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5aa8b-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="5aa8b-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Belge döndür. Etiketleri & & Array.isArray (belge. Etiketleri);</span><span class="sxs-lookup"><span data-stu-id="5aa8b-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="5aa8b-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="5aa8b-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="5aa8b-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="5aa8b-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="5aa8b-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;doc._ts döndürür;</span><span class="sxs-lookup"><span data-stu-id="5aa8b-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="5aa8b-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="5aa8b-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="5aa8b-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="5aa8b-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="5aa8b-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="5aa8b-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="5aa8b-339">&nbsp;&nbsp;&nbsp;&nbsp;.Value()</span><span class="sxs-lookup"><span data-stu-id="5aa8b-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="5aa8b-340">6</span><span class="sxs-lookup"><span data-stu-id="5aa8b-340">6</span></span>|

<span data-ttu-id="5aa8b-341">Merhaba aşağıdaki açıklamaları yukarıdaki hello tablosundaki her sorgu açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-341">hello following descriptions explain each query in hello table above.</span></span>
1. <span data-ttu-id="5aa8b-342">Sonuç tüm belgelerde (devamlılık belirteci ile anlatır) olur.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="5aa8b-343">Projeleri kimliği, ileti (diğer toomsg) ve tüm belgeleri eylemin hello.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-343">Projects hello id, message (aliased toomsg), and action from all documents.</span></span>
3. <span data-ttu-id="5aa8b-344">Merhaba koşulu belgeler için sorgular: kimlik = "X998_Y998".</span><span class="sxs-lookup"><span data-stu-id="5aa8b-344">Queries for documents with hello predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="5aa8b-345">Etiketler özelliği ve etiketleri olan belgeler için sorgular 123 hello değerini içeren bir dizi olur.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-345">Queries for documents that have a Tags property and Tags is an array containing hello value 123.</span></span>
5. <span data-ttu-id="5aa8b-346">Sorguları bir koşul ile belgeler için kimliği = "X998_Y998" ve sonra projeleri hello kimliği ve ileti (diğer toomsg).</span><span class="sxs-lookup"><span data-stu-id="5aa8b-346">Queries for documents with a predicate, id = "X998_Y998", and then projects hello id and message (aliased toomsg).</span></span>
6. <span data-ttu-id="5aa8b-347">Etiketler, bir dizi özelliği olan belgeler için filtreleri ve hello elde edilen belgeler hello _ts zaman damgası sistem özelliği tarafından sıralar ve ardından projeleri + hello etiketler dizisi düzleştirir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-347">Filters for documents which have an array property, Tags, and sorts hello resulting documents by hello _ts timestamp system property, and then projects + flattens hello Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="5aa8b-348">Çalışma zamanı desteği</span><span class="sxs-lookup"><span data-stu-id="5aa8b-348">Runtime support</span></span>
<span data-ttu-id="5aa8b-349">[DocumentDB JavaScript sunucu tarafı API](http://azure.github.io/azure-documentdb-js-server/) hello için destek sağlar hello çoğunu genel JavaScript dil özellikleri tarafından standartlaştırılmış olarak [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span><span class="sxs-lookup"><span data-stu-id="5aa8b-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for hello most of hello mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="5aa8b-350">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="5aa8b-350">Security</span></span>
<span data-ttu-id="5aa8b-351">JavaScript saklı yordamları ve Tetikleyicileri korumalı, böylece tek bir betik hello etkilerini toohello diğer hello snapshot işlem yalıtım hello veritabanı düzeyinde üzerinden geçmeden sızıntısı değil.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-351">JavaScript stored procedures and triggers are sandboxed so that hello effects of one script do not leak toohello other without going through hello snapshot transaction isolation at hello database level.</span></span> <span data-ttu-id="5aa8b-352">Merhaba çalışma zamanı ortamları havuza alınmış ancak her çalışma sonrasında Merhaba içeriğine temizlendi.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-352">hello runtime environments are pooled but cleaned of hello context after each run.</span></span> <span data-ttu-id="5aa8b-353">Toobe bu nedenle garanti birbirinden herhangi istenmeyen yan etkileri güvenli.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-353">Hence they are guaranteed toobe safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="5aa8b-354">Ön derleme</span><span class="sxs-lookup"><span data-stu-id="5aa8b-354">Pre-compilation</span></span>
<span data-ttu-id="5aa8b-355">Saklı yordamlar, tetikleyiciler ve UDF'lerin örtük olarak önceden derlenmiş toohello bayt kodu sipariş tooavoid derleme maliyet her komut dosyası çağırma hello zaman biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-355">Stored procedures, triggers and UDFs are implicitly precompiled toohello byte code format in order tooavoid compilation cost at hello time of each script invocation.</span></span> <span data-ttu-id="5aa8b-356">Bu saklı yordam çağrılarını hızlı ve az alan kaplaması sahip sağlar.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="5aa8b-357">İstemci SDK'sı desteği</span><span class="sxs-lookup"><span data-stu-id="5aa8b-357">Client SDK support</span></span>
<span data-ttu-id="5aa8b-358">İçin ek toohello DocumentDB API içinde [Node.js](documentdb-sdk-node.md) istemci, Azure Cosmos DB [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), ve [Python SDK'ları](documentdb-sdk-python.md) hello DocumentDB API için.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-358">In addition toohello DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for hello DocumentDB API.</span></span> <span data-ttu-id="5aa8b-359">Saklı yordamlar, tetikleyiciler ve UDF'lerin oluşturulabilir ve bu SDK de birini kullanarak çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="5aa8b-360">örnekte gösterildiği nasıl aşağıdaki hello toocreate ve hello .NET İstemcisi'ni kullanarak bir saklı yordamı yürütme.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-360">hello following example shows how toocreate and execute a stored procedure using hello .NET client.</span></span> <span data-ttu-id="5aa8b-361">JSON olarak saklı yordamı ve geri okuma hello .NET türleri hello nasıl geçirildiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-361">Note how hello .NET types are passed into hello stored procedure as JSON and read back.</span></span>

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


<span data-ttu-id="5aa8b-362">Bu örnek göstermektedir nasıl toouse hello [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate öncesi tetikleyici ve etkin hello tetikleyiciyle bir belge oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-362">This sample shows how toouse hello [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate a pre-trigger and create a document with hello trigger enabled.</span></span> 

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


<span data-ttu-id="5aa8b-363">Aşağıdaki örneğine hello nasıl işlev (UDF) toocreate bir kullanıcı tanımlı gösterir ve bunu kullanın ve bir [DocumentDB API SQL sorgusu](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="5aa8b-363">And hello following example shows how toocreate a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

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

## <a name="rest-api"></a><span data-ttu-id="5aa8b-364">REST API</span><span class="sxs-lookup"><span data-stu-id="5aa8b-364">REST API</span></span>
<span data-ttu-id="5aa8b-365">Tüm Azure Cosmos DB işlemleri RESTful bir şekilde gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="5aa8b-366">Saklı yordamlar, tetikleyiciler ve kullanıcı tanımlı işlevler altından bir HTTP POST kullanılarak kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="5aa8b-367">Merhaba nasıl bir örnek verilmiştir tooregister bir saklı yordam:</span><span class="sxs-lookup"><span data-stu-id="5aa8b-367">hello following is an example of how tooregister a stored procedure:</span></span>

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


<span data-ttu-id="5aa8b-368">Merhaba saklı yordam kayıtlı bir POST isteği hello URI karşı yürüterek dbs/testdb/colls/testColl/hello gövdesini içeren ile sprocs saklı yordam toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-368">hello stored procedure is registered by executing a POST request against hello URI dbs/testdb/colls/testColl/sprocs with hello body containing hello stored procedure toocreate.</span></span> <span data-ttu-id="5aa8b-369">Tetikleyiciler ve UDF'lerin benzer şekilde bir POST/tetikleyiciler ve /udfs karşı sırasıyla vererek kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="5aa8b-370">Bu yordam can depolanan sonra kaynak bağlantısını karşı bir POST isteği göndererek yürütülebilir:</span><span class="sxs-lookup"><span data-stu-id="5aa8b-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


<span data-ttu-id="5aa8b-371">Burada, hello giriş toohello depolanan yordamı hello istek gövdesinde geçirilir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-371">Here, hello input toohello stored procedure is passed in hello request body.</span></span> <span data-ttu-id="5aa8b-372">Merhaba giriş girdi parametresi bir JSON dizisi olarak geçirilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-372">Note that hello input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="5aa8b-373">Merhaba yordamı alır hello ilk giriş yanıt gövdesi bir belge olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-373">hello stored procedure takes hello first input as a document that is a response body.</span></span> <span data-ttu-id="5aa8b-374">Merhaba yanıt aldığımız aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="5aa8b-374">hello response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of hello Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="5aa8b-375">Saklı yordamlar aksine Tetikleyicileri doğrudan yürütülemez.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="5aa8b-376">Bunun yerine, bir belge üzerinde bir işlemi bir parçası olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="5aa8b-377">HTTP üst bilgilerini kullanarak bir istekle biz hello Tetikleyicileri toorun belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-377">We can specify hello triggers toorun with a request using HTTP headers.</span></span> <span data-ttu-id="5aa8b-378">Merhaba, istek toocreate bir belge aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-378">hello following is request toocreate a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “hello Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="5aa8b-379">Burada hello istekle çalıştırmak hello öncesi tetikleyici toobe hello x-ms-documentdb-pre-trigger-include üstbilgisinde belirtilir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-379">Here hello pre-trigger toobe run with hello request is specified in hello x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="5aa8b-380">Buna bağlı olarak, hiçbir sonrası tetikleyici hello x-ms-documentdb-post-trigger-include üstbilgisinde verilir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-380">Correspondingly, any post-triggers are given in hello x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="5aa8b-381">Unutmayın her ikisi de öncesi ve sonrası tetikleyicileri, belirli bir istek için belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="5aa8b-382">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="5aa8b-382">Sample code</span></span>
<span data-ttu-id="5aa8b-383">Daha fazla sunucu tarafı kodu örnekleri bulabilirsiniz (de dahil olmak üzere [toplu silme](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), ve [güncelleştirme](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) üzerinde bizim [GitHub deposunu](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="5aa8b-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="5aa8b-384">Tooshare harika, saklı yordam istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="5aa8b-384">Want tooshare your awesome stored procedure?</span></span> <span data-ttu-id="5aa8b-385">Lütfen bize bir çekme isteği gönderin!</span><span class="sxs-lookup"><span data-stu-id="5aa8b-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5aa8b-386">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5aa8b-386">Next steps</span></span>
<span data-ttu-id="5aa8b-387">Bir veya daha fazla saklı yordamlar, tetikleyiciler ve kullanıcı tanımlı işlevler oluşturulan olduktan sonra bunları yükleyin ve hello Veri Gezgini'ni kullanarak Azure portalında görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="5aa8b-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in hello Azure portal using Data Explorer.</span></span>

<span data-ttu-id="5aa8b-388">Merhaba aşağıdakileri de bulabilirsiniz başvuruları ve kaynakları Azure Cosmos dB sunucu tarafı programlama hakkında daha fazla bilgi, yol toolearn yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="5aa8b-388">You may also find hello following references and resources useful in your path toolearn more about Azure Cosmos dB server-side programming:</span></span>

* [<span data-ttu-id="5aa8b-389">Azure Cosmos DB SDK'ları</span><span class="sxs-lookup"><span data-stu-id="5aa8b-389">Azure Cosmos DB SDKs</span></span>](documentdb-sdk-dotnet.md)
* [<span data-ttu-id="5aa8b-390">DocumentDB Studio</span><span class="sxs-lookup"><span data-stu-id="5aa8b-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="5aa8b-391">JSON</span><span class="sxs-lookup"><span data-stu-id="5aa8b-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="5aa8b-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="5aa8b-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="5aa8b-393">Güvenli ve taşınabilir veritabanı genişletilebilirliği</span><span class="sxs-lookup"><span data-stu-id="5aa8b-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="5aa8b-394">Hizmet odaklı veritabanı mimarisi</span><span class="sxs-lookup"><span data-stu-id="5aa8b-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="5aa8b-395">Microsoft SQL server Hello .NET çalışma zamanı barındırma</span><span class="sxs-lookup"><span data-stu-id="5aa8b-395">Hosting hello .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

