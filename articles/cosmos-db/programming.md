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
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a>Azure Cosmos DB sunucu tarafı programlama: saklı yordamlar, veritabanı tetikleyiciler ve UDF'lerin
Azure Cosmos veritabanı dil nasıl tümleşik öğrenin, JavaScript işlem tabanlı olarak yürütülmesini sağlar yazma geliştiriciler **saklı yordamlar**, **Tetikleyicileri** ve **kullanıcı tanımlı işlevler (UDF'ler)** yerel olarak bir [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript. Bu, gönderilen ve doğrudan hello veritabanı depolama bölümleri üzerinde yürütülen toowrite veritabanı program uygulama mantığı sağlar. 

Alma burada Barış Liu kısa giriş tooCosmos DB'ın sunucu tarafı veritabanı programlama modeli sağlar aşağıdaki izledikleri hello tarafından video, başlatılan öneririz. 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

Ardından, toothis makale, aşağıdaki soruları hello yanıtlar toohello burada öğreneceksiniz döndürün:  

* Ne ı yazma bir saklı yordam, tetikleyici veya JavaScript kullanarak UDF?
* Cosmos DB ACID nasıl garanti?
* İşlemler Cosmos DB'de nasıl çalışır?
* Önceden tetikler ve sonrası tetikler nedir ve nasıl t bir yazma?
* Nasıl kaydetmek ve HTTP kullanarak bir RESTful şekilde bir saklı yordam, tetikleyici veya UDF yürütme?
* Ne Cosmos DB SDK'ları kullanılabilir toocreate olan ve yürütme yordamlar, tetikleyiciler ve UDF'lerin depolanan?

## <a name="introduction-toostored-procedure-and-udf-programming"></a>Giriş tooStored yordamı ve UDF programlama
Bu yaklaşım *"JavaScript T-SQL modern gün olarak"* tür sistem uyuşmazlıkları ve nesne ilişkisel eşleme teknolojileri hello karmaşıklığını uygulama geliştiricilerden boşaltır. Ayrıca, birkaç kullanılan toobuild zengin uygulamalar olabilir iç avantajları vardır:  

* **Yordam mantığı:** üst düzey bir programlama dili olarak JavaScript zengin ve tanıdık arabirimi tooexpress iş mantığı sağlar. Karmaşık işlemleri daha yakından toohello veri dizisini gerçekleştirebilirsiniz.
* **Atomik işlemleri:** tek bir saklı yordam veya tetikleyici içinde gerçekleştirilen işlemler veritabanı Cosmos DB garanti atomik. Bu, tek bir toplu ilgili işlemlerinde bunların tümünün başarılı ya da bunların hiçbiri başarılı birleştirmek bir uygulama sağlar. 
* **Performans:** JSON doğası gereği eşlenen toohello Javascript dil tür sistemi ve ayrıca hello temel Cosmos DB depolama biriminin verir iyileştirmeler JSON, yavaş materialization gibi birtakım olduğunu hello olgu hello arabellekte belgeleri Havuz ve kod yürütmek kullanılabilir İsteğe bağlı toohello yapma. Sevkiyat iş mantığı toohello veritabanı ile ilgili daha fazla performans avantajı vardır:
  
  * Toplu işleme – Geliştiriciler grubu ekleme gibi işlemleri ve toplu olarak gönderin. Merhaba ağ trafiği gecikmesi maliyet ve hello deposu genel gider toocreate ayrı işlemleri önemli ölçüde azalır. 
  * Ön derleme – Cosmos DB saklı yordamlar, tetikleyiciler ve kullanıcı tanımlı işlevler (UDF'ler) tooavoid her çağırma için JavaScript derleme maliyeti işlemini gerçekleştirir. Merhaba hello yordam mantığı için hello bayt kod oluşturma yükünü tooa en az değer amortized.
  * Sıralama – birçok işlemleri gerek yan içeren büyük olasılıkla bir veya daha fazla ikincil depolama işlemleri yapılması etki ("tetikleyicisi"). Daha fazla kullanıcı budur kararlılık yanı sıra zaman toohello server'ı taşındı. 
* **Kapsülleme:** saklı yordamlar, tek bir yerde kullanılan toogroup iş mantığı olabilir. Bu iki avantajları vardır:
  * Veri mimarları tooevolve uygulamalarını hello veri öğesinden bağımsız olarak etkinleştirir hello ham verileri en üstünde bir soyutlama katmanı ekler. Merhaba veri toodeal verilerle doğrudan varsa, hello uygulamasına baked toobe gerekebilir toohello kırılır varsayımlar şema küçüktür, bu özellikle yararlı olur.  
  * Bu soyutlama kuruluşların hello komut dosyalarından hello erişimi hızlandırma tarafından verilerine güvenli kalmasına izin verir.  

Merhaba oluşturma ve yürütme veritabanı tetikleyici, saklı yordam ve özel sorgu işleçleri desteklenir hello [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), ve [istemci SDK'ları](documentdb-sdk-dotnet.md) .NET, Node.js ve JavaScript gibi birçok platformda.

Bu öğretici hello kullanır [Node.js SDK'sı ile Q öneriler](http://azure.github.io/azure-documentdb-node-q/) tooillustrate sözdizimi ve saklı yordamlar, tetikleyiciler ve UDF'lerin kullanımı.   

## <a name="stored-procedures"></a>Saklı yordamlar
### <a name="example-write-a-simple-stored-procedure"></a>Örnek: basit bir saklı yordam yazma
"Hello World" yanıt veren basit bir saklı yordam ile başlayalım.

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


Saklı yordamlar koleksiyonu başına kaydedilir ve herhangi bir belge ve ek koleksiyonda mevcut üzerinde çalışabilir. Merhaba aşağıdaki kod parçacığında nasıl tooregister hello helloWorld saklı yordamı koleksiyonu ile gösterilir. 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


Hello saklı yordamı kaydedildiğinde, biz hello koleksiyonu karşı yürütün ve hello sonuçları hello istemcide geri okuyun. 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


Merhaba bağlam nesnesi toohello istek ve yanıt nesnelere erişmek yanı sıra Cosmos DB depolama alanında gerçekleştirilebilir tooall işlemleri erişim sağlar. Bu durumda, hello yanıt nesnesi tooset hello geri toohello istemci gönderilen hello yanıtın gövdesini kullandık. Daha fazla ayrıntı için toohello başvurun [Azure Cosmos DB JavaScript server SDK Belgeleri](http://azure.github.io/azure-documentdb-js-server/).  

Bize göre bu örnekte genişletin ve daha fazla veritabanı ilgili işlevsellik eklemek toohello saklı yordamı. Saklı yordamlar oluşturabilir, güncelleştirme, okuma, sorgu ve belgeler ve ekleri hello koleksiyonu içinde silebilirsiniz.    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a>Örnek: bir saklı yordam toocreate bir belge yazma
Merhaba sonraki parçacığı nasıl toouse hello bağlam nesnesi toointeract Cosmos DB kaynaklarla gösterir.

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


Bu saklı yordam giriş documentToCreate, hello geçerli Koleksiyonda oluşturulmuş bir belge toobe hello gövdesini alır. Tüm işlemleri zaman uyumsuzdur ve JavaScript işlevi geri aramalar üzerinde bağlıdır. Merhaba geri çağırma işlevi hello hata nesnesi için iki parametre hello işlemi başarısız olur ve nesne hello için oluşturulan olasılığına sahiptir. Merhaba geri çağırma içinde kullanıcılar hello özel durumu işlemek ya da bir hata durum. Bir geri çağırma değil sağlanır ve bir hata durumunda, hello Azure Cosmos DB çalışma zamanı bir hata oluşturur.   

Merhaba işlemi başarısız olursa hello yukarıdaki örnekte, bir hata hello geri çağırma oluşturur. Aksi takdirde, belge hello yanıt toohello istemci hello gövdesi olarak oluşturulan hello hello kimliğini ayarlar. İşte bu saklı yordam giriş parametreleriyle nasıl yürütülür.

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


Bu saklı yordamı Not değiştirilmiş tootake belge gövdeleri bir dizi girişi olarak kullanılabilir ve tüm aynı depolanan hello oluşturma yordamı yürütme birden çok ağ yerine toocreate her biri ayrı ayrı ister. Bu, kullanılan tooimplement Cosmos DB (Bu öğreticinin ilerleyen bölümlerinde açıklanmıştır) için bir verimli toplu alıcısı olabilir.   

nasıl toouse saklı yordamları açıklanan Merhaba örneği gösterilmektedir. Daha sonra hello öğreticide biz tetikleyiciler ve kullanıcı tanımlı işlevler (UDF'ler) ele alınacaktır.

## <a name="database-program-transactions"></a>Veritabanı program işlemleri
Tipik bir veritabanında işlem tek bir mantıksal birim iş olarak gerçekleştirilen işlemler dizisi olarak tanımlanabilir. Her işlem sağlar **ACID garanti**. ACID dört özellikleri - kararlılık, tutarlılık, yalıtım ve dayanıklılık anlamına gelir iyi bilinen bir kısaltma ' dir.  

Kısaca, bir işlem içinde yapılan tüm hello iş tek bir birim olarak davranılır kararlılık garanti burada ya da tamamını kaydedilmiş veya yok. Tutarlılık hello veri işlemleri arasında her zaman iyi bir iç durumda olduğundan emin olur. Yalıtım iki işlem birbiriyle – genellikle etkilemesine, çoğu ticari sistemleri kullanılabilir birden çok yalıtım düzeyi hello uygulama gereksinimlerine göre sağlayın güvence altına alır. Dayanıklılık hello veritabanında kaydedilen herhangi bir değişiklik her zaman mevcut olmasını sağlar.   

Cosmos DB'de JavaScript hello barındırılan hello veritabanı olarak aynı bellek alanı. Bu nedenle, saklı yordamları ve Tetikleyicileri içinde yapılan istekleri hello aynı yürütme veritabanı oturumun kapsamı. Bu, tek bir saklı yordam/tetikleyici parçası olan tüm işlemleri için Cosmos DB tooguarantee ACID sağlar. Merhaba aşağıdakileri göz önünde bulundurun saklı yordamı tanımı:

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

Bu saklı yordam işlemlerini tek bir işlemde iki oyuncu arasında oyun uygulaması tootrade öğe içinde kullanır. Merhaba yordamı denemeleri tooread iki belge karşılık gelen her toohello player kimlikleri bağımsız değişken olarak geçirilen depolanır. Her iki player belge bulunamazsa, hello saklı yordamı öğelerin takas tarafından hello belgeleri güncelleştirir. Merhaba yol boyunca herhangi bir hatayla karşılaşılmazsa örtük olarak hello işlemi iptal bir JavaScript özel durumu oluşturur.

Merhaba koleksiyonu hello saklı yordamı kaydedilmişse karşı tek bölümlü bir koleksiyon olduğu sonra hello kapsamlı tooall hello belgeleri hello koleksiyonundaki bir işlemdir. Merhaba koleksiyon bölümlendiğinde ise, saklı yordamlar hello işlem kapsamında tek bölüm anahtarı yürütülür. Her saklı yordam yürütme ardından karşılık gelen toohello kapsam hello işlem altında çalıştırmalısınız bir bölüm anahtarı değerini içermelidir. Daha fazla ayrıntı için bkz: [Azure DB Cosmos bölümleme](partition-data.md).

### <a name="commit-and-rollback"></a>Kaydetme ve geri alma
İşlemleri iç ve yerel olarak Cosmos veritabanı JavaScript programlama modeline tümleşiktir. JavaScript işlevinin içinde tüm işlemleri otomatik olarak tek bir işlem altında sarılır. Merhaba JavaScript herhangi bir özel durum olmadan tamamlarsa hello operations toohello veritabanı kaydedilmiş. İlişkisel veritabanları hello "BEGIN TRANSACTION" ve "COMMIT TRANSACTION" deyimleri Cosmos DB'de örtük etkindir.  

Merhaba betikten yayılır herhangi bir özel durum ise, Cosmos veritabanı JavaScript çalışma zamanı hello tüm işlem döndürülmesine neden olur. Hello daha önce gösterildiği gibi bir özel durum atma, etkili bir şekilde eşdeğer tooa Cosmos DB "geri alma işlemi" örnektir.

### <a name="data-consistency"></a>Veri tutarlılığı
Saklı yordamları ve Tetikleyicileri hello Azure Cosmos DB kapsayıcısının hello birincil Çoğaltmada her zaman yürütülür. Bu, okuma içindeki yordamları teklif güçlü tutarlılık depolanan sağlar. Kullanıcı tanımlı işlevler kullanarak sorguları hello birincil veya ikincil bir çoğaltma üzerinde çalıştırılabilir, ancak biz toomeet olun hello hello uygun çoğaltma seçerek tutarlılık düzeyi istendi.

## <a name="bounded-execution"></a>Sınırlanmış yürütme
Tüm Cosmos DB işlemleri hello server'ın içinde belirtilen tamamlamalısınız isteği zaman aşımı süresi. Bu sınırlama tooJavaScript işlevleri (saklı yordamlar, tetikleyiciler ve kullanıcı tanımlı işlevler) de geçerlidir. Bir işlem bu zaman sınırı ile tamamlanmazsa hello işlem geri alındı. JavaScript işlevleri hello süre sınırı içinde son veya bir temel devamlılık modeli toobatch/sürdürmeden yürütme uygulamak gerekir.  

Sipariş toosimplify geliştirme saklı yordamları ve Tetikleyicileri toohandle saat sınırlarının, hello koleksiyon nesnesi (oluşturma, okuma, değiştirme ve silme belgeler ve eklerin) altında tüm işlevleri temsil eden bir Boole değeri döndürür. olup olmadığını, işlemi tamamlanır. Bu değeri false ise, onu tooexpire hakkında hello zaman sınırı yoktur ve bu hello yordamı yürütme sarmalamanız gerekir göstergesidir.  Operations sıraya alınan önceki toohello ilk kabul edilmeyen deposu işlemi garanti edilir toocomplete hello saklı yordamı zamanında tamamlandıktan ve başka istek sıra değil.  

JavaScript işlevleri de kaynak tüketimine ilişkin ilişkisindeki. Cosmos DB işleme sağlanan hello bir veritabanı hesabı boyutuna göre koleksiyon başına ayırır. Üretilen iş CPU, bellek ve g/ç tüketim istek birimleri veya RUs adlı normalleştirilmiş bir birim cinsinden ifade edilir. JavaScript işlevleri potansiyel olarak çok sayıda RUs kısa bir süre içinde yukarı kullanabilirsiniz ve oranı hello koleksiyonunun sınırına ulaşıldığında sınırlı alabilirsiniz. Kaynak yoğunluklu saklı yordamlar, ilkel veritabanı işlemleri karantinaya alınan tooensure kullanılabilirliğini de olabilir.  

### <a name="example-bulk-importing-data-into-a-database-program"></a>Örnek: toplu bir veritabanı programa veri alma
Aşağıda, bir koleksiyona toobulk alma belgeleri yazılmış bir saklı yordam örneğidir. Not hello Boolean denetleyerek yordam ilişkisindeki tanıtıcıları yürütme hello depolanan nasıl dönüş değeri createDocument ve ardından kullanır hello saklı yordamı tootrack ve sürdürme ilerleme her çalıştırılışı toplu eklenen belge sayısını hello.

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

## <a id="trigger"></a>Veritabanı Tetikleyicileri
### <a name="database-pre-triggers"></a>Veritabanı öncesi Tetikleyicileri
Cosmos DB yürütülen ya da bir belge üzerinde bir işlemi tarafından tetiklenen Tetikleyiciler sağlar. Örneğin, ön tetikleyici belirtebilmeniz için bir belge oluşturma – hello belge oluşturulmadan önce bu ön tetikleyici çalışacak olduğunda. Merhaba, ön Tetikleyiciler kullanılan toovalidate hello oluşturulmakta olan bir belgenin özelliklerini nasıl olabilir örneği aşağıdadır:

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


Ve Node.js istemci tarafı kaydı kodu hello tetikleyici için karşılık gelen hello:

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


Giriş parametreleri öncesi tetikleyici bulunamaz. Merhaba istek nesnesi kullanılan toomanipulate hello istek iletisi hello işlemle ilişkili olabilir. Burada, hello öncesi tetikleyici belgeyi hello oluşturma ile çalıştırın ve JSON biçiminde oluşturulan hello belge toobe hello istek ileti gövdesi içerir.   

Tetikleyiciler kayıtlı olduğunda, kullanıcılar ile çalıştırabilirsiniz hello operations belirtebilirsiniz. Bu tetikleyici hello aşağıdaki izin anlamına gelir TriggerOperation.Create ile oluşturuldu.

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a>Veritabanı sonrası Tetikleyicileri
Ön tetikleyiciler gibi sonrası Tetikleyicileri bir belge üzerinde bir işlemi ile ilişkili ve giriş parametreleri gerçekleştirin yok. Çalışırlar **sonra** hello işleminin tamamlandığını ve toohello istemci gönderilen erişim toohello yanıt iletisi vardır.   

Aşağıdaki örneğine hello sonrası Tetikleyicileri eylemde gösterir:

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


Merhaba tetikleyici hello örnek aşağıdaki gösterildiği gibi kaydedilebilir.

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


Bu tetikleyici hello meta veri belgesi için sorgular ve yeni oluşturulan hello belge hakkında ayrıntılarla güncelleştirir.  

Toonote hello olan önemli bir şey **işlem** Cosmos DB Tetikleyicileri yürütülmesi. Bu sonrası tetikleyici hello bir parçası olarak çalışır hello oluşturma hello orijinal belgenin olarak aynı işlem. Bu nedenle, biz hello sonrası tetikleyiciyle (biz oluşturulamıyor tooupdate hello meta veri belgesi varsa say) bir özel durum, hello tüm işlem başarısız olur ve geri alındı. Bir belge oluşturulur ve bir özel durum döndürdü.  

## <a id="udf"></a>Kullanıcı tanımlı işlevler
Kullanıcı tanımlı işlevler (UDF'ler) kullanılan tooextend hello DocumentDB API SQL Sorgu Dili Dilbilgisi olan ve özel iş mantığını uygular. Öğesinden yalnızca çağrılabilir sorguları içinde. Bunlar erişim toohello bağlam nesnesi yoktur ve yalnızca işlem JavaScript kullanılan toobe yöneliktir. Bu nedenle, UDF'ler hello Cosmos DB hizmet ikincil çoğaltmalar üzerinde çalıştırılabilir.  

Hello aşağıdaki örnek çeşitli gelir köşeli için hızlarını dayalı bir UDF toocalculate gelir vergi oluşturur ve ardından sorgu toofind içinde birden fazla $20.000 vergiler Ücretli tüm kişilerin kullanır.

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


Merhaba UDF sonradan hello örnek aşağıdaki gibi sorgularında kullanılabilir:

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

## <a name="javascript-language-integrated-query-api"></a>JavaScript dil ile tümleşik sorgu API
Ayrıca Documentdb'nin SQL dil bilgisinin kullanarak tooissuing sorguları hello sunucu tarafı SDK'sı SQL bilgisi olmadan fluent JavaScript arabirimi kullanarak en iyi duruma getirilmiş tooperform sorguları sağlar. API tooprogrammatically yapı sorguları chainable işlevdeki geçirme koşul işlevleri sağlar hello JavaScript sorgu bir söz dizimi hakkında bilgi sahibi tooECMAScript5's dizi öğelerin ve lodash gibi popüler JavaScript kitaplıkları ile çağırır. Sorgular tarafından hello JavaScript çalışma zamanı toobe verimli bir şekilde Azure Cosmos veritabanı dizinlerini kullanılarak yürütülen ayrıştırılır.

> [!NOTE]
> `__`(çift alt çizgi) olan bir diğer ad çok`getContext().getCollection()`.
> <br/>
> Diğer bir deyişle, kullanabileceğiniz `__` veya `getContext().getCollection()` tooaccess hello JavaScript sorgu API.
> 
> 

Desteklenen işlevler aşağıdakileri içerir:

<ul>
<li>
<b>... chain(). değeri ([geri çağırma] [, Seçenekleri])</b>
<ul>
<li>
İle bitmelidir bir zincirleme çağrısını Value()) ile başlar.
</li>
</ul>
</li>
<li>
<b>Filtre (predicateFunction [, Seçenekleri] [, geri çağırma])</b>
<ul>
<li>
True/false sipariş toofilter giriş/çıkış giriş belgeleri hello sonuç kümesi olarak döndüren bir koşul işlevini kullanarak giriş hello filtreler. Bu benzer tooa davranır SQL WHERE yan tümcesi.
</li>
</ul>
</li>
<li>
<b>Harita (transformationFunction [, Seçenekleri] [, geri çağırma])</b>
<ul>
<li>
Her bir giriş öğesini tooa JavaScript nesne veya değer eşleştiren bir dönüşüm işlevi verilen bir yansıtma geçerlidir. Benzer tooa SELECT yan tümcesinde SQL davranır.
</li>
</ul>
</li>
<li>
<b>pluck ([propertyName] [, Seçenekleri] [, geri çağırma])</b>
<ul>
<li>
Her giriş öğesinden hello tek bir özellik değerini ayıklayan bir harita için bir kısayol budur.
</li>
</ul>
</li>
<li>
<b>düzleştirmek ([isShallow] [, Seçenekleri] [, geri çağırma])</b>
<ul>
<li>
Birleştirir ve diziler tooa tek dizisindeki her giriş öğesinden düzleştirir. LINQ benzer tooSelectMany davranır.
</li>
</ul>
</li>
<li>
<b>sortBy ([koşulu] [, Seçenekleri] [, geri çağırma])</b>
<ul>
<li>
Yeni belgeler birtakım koşulu verilen hello kullanarak artan hello giriş belgesi akış hello belgelerde sıralayarak üretir. Benzer tooa ORDER BY yan tümcesinde SQL davranır.
</li>
</ul>
</li>
<li>
<b>sortByDescending ([koşulu] [, Seçenekleri] [, geri çağırma])</b>
<ul>
<li>
Yeni belgeler birtakım koşulu verilen hello kullanarak azalan hello giriş belgesi akış hello belgelerde sıralayarak üretir. Benzer tooa x DESC ORDER BY yan tümcesi SQL davranır.
</li>
</ul>
</li>
</ul>


Koşul ve/veya Seçici işlevlerinin içine dahil edilirse, hello aşağıdaki JavaScript yapılarından otomatik olarak en iyi duruma getirilmiş toorun doğrudan Azure Cosmos DB dizinlerini alın:

* Basit işleçleri: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;! ~
* Merhaba nesne değişmez değer de dahil olmak üzere değişmez değerler: {}
* dönüş var

şu JavaScript oluşturur hello en iyi duruma getirilmezse Azure Cosmos DB dizinler için:

* Denetim akışı (örn. Eğer, sırada)
* İşlev çağrıları

Daha fazla bilgi için lütfen bkz bizim [sunucu tarafı JSDocs](http://azure.github.io/azure-documentdb-js-server/).

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a>Örnek: Merhaba JavaScript sorgu API kullanarak bir saklı yordam yazma
Aşağıdaki kod örneği hello hello JavaScript sorgu API hello bir saklı yordam bağlamında nasıl kullanılabileceği bir örnektir. Merhaba saklı yordamı bir giriş parametresi tarafından verilen bir belge ekler ve hello kullanarak bir meta veri belgesi güncelleştirmeleri `__.filter()` minSize, maxSize ve hello giriş belgenin boyut özelliği dayalı totalSize yöntemi.

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

## <a name="sql-toojavascript-cheat-sheet"></a>SQL tooJavascript kopya sayfası
Merhaba aşağıdaki tabloda çeşitli SQL sorguları ve hello karşılık gelen JavaScript sorguları gösterir.

Özellik anahtarları içeren SQL sorguları, belge olarak (örneğin `doc.id`) büyük küçük harfe duyarlıdır.

|SQL| JavaScript sorgu API|Aşağıdaki açıklama|
|---|---|---|
|SEÇİN *<br>Belgelerinden| __.map(function(doc) { <br>&nbsp;&nbsp;&nbsp;&nbsp;Belge dönüş;<br>});|1|
|SELECT docs.id, docs.message olarak msg, docs.actions <br>Belgelerinden|__.map(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;{Döndür<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kimliği: doc.id,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Msg: doc.message,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Actions:doc.Actions<br>&nbsp;&nbsp;&nbsp;&nbsp;};<br>});|2|
|SEÇİN *<br>Belgelerinden<br>WHERE docs.id="X998_Y998"|__.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;doc.id iade === "X998_Y998";<br>});|3|
|SEÇİN *<br>Belgelerinden<br>WHERE ARRAY_CONTAINS (belgeleri. Etiketler, 123)|__.filter(function(x) {<br>&nbsp;&nbsp;&nbsp;&nbsp;x.Tags iade & & x.Tags.indexOf(123) > -1;<br>});|4|
|SELECT docs.id, docs.message msg olarak<br>Belgelerinden<br>WHERE docs.id="X998_Y998"|__.chain()<br>&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;doc.id iade === "X998_Y998";<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{Döndür<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kimliği: doc.id,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Msg: doc.message<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>.Value();|5|
|DEĞER etiketi<br>Belgelerinden<br>Etiket IN belgeleri katılın. Etiketleri<br>ORDER BY docs._ts|__.chain()<br>&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Belge döndür. Etiketleri & & Array.isArray (belge. Etiketleri);<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;doc._ts döndürür;<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")<br>&nbsp;&nbsp;&nbsp;&nbsp;.flatten()<br>&nbsp;&nbsp;&nbsp;&nbsp;.Value()|6|

Merhaba aşağıdaki açıklamaları yukarıdaki hello tablosundaki her sorgu açıklanmaktadır.
1. Sonuç tüm belgelerde (devamlılık belirteci ile anlatır) olur.
2. Projeleri kimliği, ileti (diğer toomsg) ve tüm belgeleri eylemin hello.
3. Merhaba koşulu belgeler için sorgular: kimlik = "X998_Y998".
4. Etiketler özelliği ve etiketleri olan belgeler için sorgular 123 hello değerini içeren bir dizi olur.
5. Sorguları bir koşul ile belgeler için kimliği = "X998_Y998" ve sonra projeleri hello kimliği ve ileti (diğer toomsg).
6. Etiketler, bir dizi özelliği olan belgeler için filtreleri ve hello elde edilen belgeler hello _ts zaman damgası sistem özelliği tarafından sıralar ve ardından projeleri + hello etiketler dizisi düzleştirir.


## <a name="runtime-support"></a>Çalışma zamanı desteği
[DocumentDB JavaScript sunucu tarafı API](http://azure.github.io/azure-documentdb-js-server/) hello için destek sağlar hello çoğunu genel JavaScript dil özellikleri tarafından standartlaştırılmış olarak [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).

### <a name="security"></a>Güvenlik
JavaScript saklı yordamları ve Tetikleyicileri korumalı, böylece tek bir betik hello etkilerini toohello diğer hello snapshot işlem yalıtım hello veritabanı düzeyinde üzerinden geçmeden sızıntısı değil. Merhaba çalışma zamanı ortamları havuza alınmış ancak her çalışma sonrasında Merhaba içeriğine temizlendi. Toobe bu nedenle garanti birbirinden herhangi istenmeyen yan etkileri güvenli.

### <a name="pre-compilation"></a>Ön derleme
Saklı yordamlar, tetikleyiciler ve UDF'lerin örtük olarak önceden derlenmiş toohello bayt kodu sipariş tooavoid derleme maliyet her komut dosyası çağırma hello zaman biçimindedir. Bu saklı yordam çağrılarını hızlı ve az alan kaplaması sahip sağlar.

## <a name="client-sdk-support"></a>İstemci SDK'sı desteği
İçin ek toohello DocumentDB API içinde [Node.js](documentdb-sdk-node.md) istemci, Azure Cosmos DB [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), ve [Python SDK'ları](documentdb-sdk-python.md) hello DocumentDB API için. Saklı yordamlar, tetikleyiciler ve UDF'lerin oluşturulabilir ve bu SDK de birini kullanarak çalıştırılabilir. örnekte gösterildiği nasıl aşağıdaki hello toocreate ve hello .NET İstemcisi'ni kullanarak bir saklı yordamı yürütme. JSON olarak saklı yordamı ve geri okuma hello .NET türleri hello nasıl geçirildiğini unutmayın.

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


Bu örnek göstermektedir nasıl toouse hello [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate öncesi tetikleyici ve etkin hello tetikleyiciyle bir belge oluşturun. 

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


Aşağıdaki örneğine hello nasıl işlev (UDF) toocreate bir kullanıcı tanımlı gösterir ve bunu kullanın ve bir [DocumentDB API SQL sorgusu](documentdb-sql-query.md).

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

## <a name="rest-api"></a>REST API
Tüm Azure Cosmos DB işlemleri RESTful bir şekilde gerçekleştirilebilir. Saklı yordamlar, tetikleyiciler ve kullanıcı tanımlı işlevler altından bir HTTP POST kullanılarak kaydedilebilir. Merhaba nasıl bir örnek verilmiştir tooregister bir saklı yordam:

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


Merhaba saklı yordam kayıtlı bir POST isteği hello URI karşı yürüterek dbs/testdb/colls/testColl/hello gövdesini içeren ile sprocs saklı yordam toocreate hello. Tetikleyiciler ve UDF'lerin benzer şekilde bir POST/tetikleyiciler ve /udfs karşı sırasıyla vererek kaydedilebilir.
Bu yordam can depolanan sonra kaynak bağlantısını karşı bir POST isteği göndererek yürütülebilir:

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


Burada, hello giriş toohello depolanan yordamı hello istek gövdesinde geçirilir. Merhaba giriş girdi parametresi bir JSON dizisi olarak geçirilir unutmayın. Merhaba yordamı alır hello ilk giriş yanıt gövdesi bir belge olarak depolanır. Merhaba yanıt aldığımız aşağıdaki gibidir:

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


Saklı yordamlar aksine Tetikleyicileri doğrudan yürütülemez. Bunun yerine, bir belge üzerinde bir işlemi bir parçası olarak yürütülür. HTTP üst bilgilerini kullanarak bir istekle biz hello Tetikleyicileri toorun belirtebilirsiniz. Merhaba, istek toocreate bir belge aşağıdadır.

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


Burada hello istekle çalıştırmak hello öncesi tetikleyici toobe hello x-ms-documentdb-pre-trigger-include üstbilgisinde belirtilir. Buna bağlı olarak, hiçbir sonrası tetikleyici hello x-ms-documentdb-post-trigger-include üstbilgisinde verilir. Unutmayın her ikisi de öncesi ve sonrası tetikleyicileri, belirli bir istek için belirtilebilir.

## <a name="sample-code"></a>Örnek kod
Daha fazla sunucu tarafı kodu örnekleri bulabilirsiniz (de dahil olmak üzere [toplu silme](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), ve [güncelleştirme](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) üzerinde bizim [GitHub deposunu](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).

Tooshare harika, saklı yordam istiyorsunuz? Lütfen bize bir çekme isteği gönderin! 

## <a name="next-steps"></a>Sonraki adımlar
Bir veya daha fazla saklı yordamlar, tetikleyiciler ve kullanıcı tanımlı işlevler oluşturulan olduktan sonra bunları yükleyin ve hello Veri Gezgini'ni kullanarak Azure portalında görüntüleyin.

Merhaba aşağıdakileri de bulabilirsiniz başvuruları ve kaynakları Azure Cosmos dB sunucu tarafı programlama hakkında daha fazla bilgi, yol toolearn yararlıdır:

* [Azure Cosmos DB SDK'ları](documentdb-sdk-dotnet.md)
* [DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases)
* [JSON](http://www.json.org/) 
* [JavaScript ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [Güvenli ve taşınabilir veritabanı genişletilebilirliği](http://dl.acm.org/citation.cfm?id=276339) 
* [Hizmet odaklı veritabanı mimarisi](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [Microsoft SQL server Hello .NET çalışma zamanı barındırma](http://dl.acm.org/citation.cfm?id=1007669)

