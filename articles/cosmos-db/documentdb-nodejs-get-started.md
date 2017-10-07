---
title: "hello Azure Cosmos DB için DocumentDB API için aaaNode.js Öğreticisi | Microsoft Docs"
description: "Cosmos DB hello DocumentDB API ile oluşturan bir Node.js Öğreticisi."
keywords: "node.js öğreticisi, düğüm veritabanı"
services: cosmos-db
documentationcenter: node.js
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: 14d52110-1dce-4ac0-9dd9-f936afccd550
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: node
ms.topic: article
ms.date: 08/14/2017
ms.author: anhoh
ms.openlocfilehash: fce244c6a5f321608e82ca51a2c987e84b98bffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a>Node.js Öğreticisi: DocumentDB API kullanımı hello Azure Cosmos DB toocreate bir Node.js konsol uygulaması
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [MongoDB için Node.js](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Hello Azure Cosmos DB Node.js SDK'sı için toohello Node.js Öğreticisi Hoş Geldiniz! Bu öğreticiyi uyguladıktan sonra, Azure Cosmos DB kaynaklarını oluşturan ve sorgulayan bir konsol uygulamasına sahip olacaksınız.

Şu konulara değineceğiz:

* Oluşturma ve tooan Azure Cosmos DB hesabına bağlanma
* Uygulamanızı kurma
* Düğüm veritabanı oluşturma
* Koleksiyon oluşturma
* JSON belgeleri oluşturma
* Merhaba koleksiyonu sorgulama
* Bir belgeyi değiştirme
* Bir belgeyi silme
* Merhaba node veritabanı silme

Zamanınız yok mu? Endişelenmeyin! Merhaba eksiksiz bir çözüm edinilebilir [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started). Bkz: [alma hello eksiksiz bir çözüm](#GetSolution) hızlı yönergeler için.

Merhaba Node.js öğreticisini tamamladıktan sonra lütfen hello kullan oylama hello üst ve alt bu sayfa toogive bize geri bildirim düğmeler. Bize istiyorsanız toocontact doğrudan düşündüğünüz e-posta adresi serbest tooinclude yorumlarınızı içinde.

Şimdi başlayalım!

## <a name="prerequisites-for-hello-nodejs-tutorial"></a>Merhaba Node.js öğreticisi için Önkoşullar
Merhaba aşağıdaki sahip olduğunuzdan emin olun:

* Etkin bir Azure hesabı. Bir aboneliğiniz yoksa [Ücretsiz Azure Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.
    * Alternatif olarak, hello kullanabilirsiniz [Azure Cosmos DB öykünücüsü](local-emulator.md) Bu öğretici için.
* [Node.js](https://nodejs.org/) v0.10.29 sürümü veya sonraki bir sürüm.

## <a name="step-1-create-an-azure-cosmos-db-account"></a>1. Adım: Azure Cosmos DB hesabı oluşturma
Bir Azure Cosmos DB hesabı oluşturalım. Toouse istediğiniz bir hesap zaten varsa, şimdi çok atlayabilirsiniz[Node.js uygulamanızı ayarlama](#SetupNode). Hello Azure Cosmos DB öykünücüsü kullanıyorsanız, lütfen hello adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) toosetup öykünücüsü hello ve İleri çok atlayabilirsiniz[Node.js uygulamanızı ayarlama](#SetupNode).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupNode"></a>2. adım: Node.js uygulamanızı ayarlama
1. Sık kullandığınız terminali açın.
2. Merhaba klasör veya toosave oluşturulacağı yeri dizin Node.js uygulamanızı bulun.
3. Aşağıdaki komutları hello ile iki boş JavaScript dosyası oluşturun:
   * Windows:
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * Linux/OS X:
     * ```touch app.js```
     * ```touch config.js```
4. Merhaba npm aracılığıyla documentdb modülünü yükleyin. Merhaba aşağıdaki komutu kullanın:
   * ```npm install documentdb --save```

Harika! Kurulumu tamamladığınıza göre, biraz kod yazmaya başlayalım.

## <a id="Config"></a>3. Adım: Uygulamanızın yapılandırmalarını ayarlama
Sık kullandığınız metin düzenleyicisinde ```config.js``` öğesini açın.

Ardından, kopyalama ve yapıştırma hello aşağıdaki kod parçacığında ve özelliklerini ayarlama ```config.endpoint``` ve ```config.primaryKey``` tooyour Azure Cosmos DB uç noktası URI ve birincil anahtar. Her iki Bu yapılandırmalar hello bulunabilir [Azure portal](https://portal.azure.com).

![Node.js Öğreticisi - hello hello etkin hub ile bir Azure Cosmos DB hesabını gösteren Azure portal ekran görüntüsü vurgulanmış, üzerinde hello vurgulanmış hello Azure Cosmos DB hesabı dikey ve hello URI, birincil anahtar ve ikincil anahtar değerleri vurgulanmış hello ANAHTARLAR düğmesi Anahtarlar dikey penceresi - Node veritabanı][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

Kopyalama ve yapıştırma hello ```database id```, ```collection id```, ve ```JSON documents``` tooyour ```config``` ayarladığınız alttaki nesne, ```config.endpoint``` ve ```config.authKey``` özellikleri. İstediğiniz toostore veritabanınızda veriler zaten varsa, Azure Cosmos veritabanı kullanabilirsiniz [veri geçiş aracı](import-data.md) hello belge tanımları eklemek yerine.

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART tooYOUR CODE
    config.database = {
        "id": "FamilyDB"
    };

    config.collection = {
        "id": "FamilyColl"
    };

    config.documents = {
        "Andersen": {
            "id": "Anderson.1",
            "lastName": "Andersen",
            "parents": [{
                "firstName": "Thomas"
            }, {
                    "firstName": "Mary Kay"
                }],
            "children": [{
                "firstName": "Henriette Thaulow",
                "gender": "female",
                "grade": 5,
                "pets": [{
                    "givenName": "Fluffy"
                }]
            }],
            "address": {
                "state": "WA",
                "county": "King",
                "city": "Seattle"
            }
        },
        "Wakefield": {
            "id": "Wakefield.7",
            "parents": [{
                "familyName": "Wakefield",
                "firstName": "Robin"
            }, {
                    "familyName": "Miller",
                    "firstName": "Ben"
                }],
            "children": [{
                "familyName": "Merriam",
                "firstName": "Jesse",
                "gender": "female",
                "grade": 8,
                "pets": [{
                    "givenName": "Goofy"
                }, {
                        "givenName": "Shadow"
                    }]
            }, {
                    "familyName": "Miller",
                    "firstName": "Lisa",
                    "gender": "female",
                    "grade": 1
                }],
            "address": {
                "state": "NY",
                "county": "Manhattan",
                "city": "NY"
            },
            "isRegistered": false
        }
    };


Merhaba veritabanı, koleksiyon ve belge tanımları, Azure Cosmos DB hareket edecek ```database id```, ```collection id```ve belgelerin verileri.

Son olarak, dışarı aktarma, ```config``` nesne hello içinde başvurabilmek ```app.js``` dosya.

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <a id="Connect"></a>4. adım: tooan Azure Cosmos DB hesap bağlanma
Boş açmak ```app.js``` hello metin düzenleyicisinde. Tooimport hello aşağıda hello kodu kopyalayıp yapıştırın ```documentdb``` modülü ve yeni oluşturduğunuz ```config``` modülü.

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

Daha önce kaydettiğiniz hello kod toouse hello kopyalayıp ```config.endpoint``` ve ```config.primaryKey``` toocreate yeni bir DocumentClient.

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

Merhaba kod tooinitialize hello Azure Cosmos DB istemci sahip olduğunuza göre Azure Cosmos DB kaynaklarla çalışmak bir bakalım.

## <a name="step-5-create-a-node-database"></a>5. Adım: Düğüm veritabanı oluşturma
Merhaba kodu kopyalayıp tooset hello HTTP durumu aşağıda bulunamadı, hello veritabanı url ve hello koleksiyonu URL'si yapıştırın. Bu URL'leri hello Azure Cosmos DB istemci hello doğru veritabanı ve koleksiyonu nasıl bulacaksınız ' dir.

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

A [veritabanı](documentdb-resources.md#databases) hello kullanarak oluşturulan [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) hello işlevinin **DocumentClient** sınıfı. Veritabanı hello mantıksal koleksiyonlar genelinde bölümlenmiş belge depolama alanının bir kapsayıcısıdır.

Kopyalama ve yapıştırma hello **getDatabase** hello ile Merhaba app.js dosyasında yeni veritabanınızı oluşturmak için işlevi ```id``` hello belirtilen ```config``` nesnesi. Merhaba hello ile aynı veritabanı hello işlevi denetler ```FamilyRegistry``` kimliği zaten mevcut değil. Varsa yeni bir veritabanı oluşturmak yerine var olan veritabanını getireceğiz.

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART tooYOUR CODE
    function getDatabase() {
        console.log(`Getting database:\n${config.database.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDatabase(databaseUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDatabase(config.database, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

Merhaba ayarladığınız hello aşağıdaki kodu yapıştırın **getDatabase** işlev tooadd hello yardımcı işlevini **çıkmak** yazdıracak hello çıkış iletisini ve hello çağrı çok**getDatabase** işlevi.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key tooexit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Terminalinizde bulun, ```app.js``` dosya ve hello komutu çalıştırın:```node app.js```

Tebrikler! Başarılı bir şekilde bir Azure Cosmos DB veritabanı oluşturdunuz.

## <a id="CreateColl"></a>6. Adım: Koleksiyon oluşturma
> [!WARNING]
> **CreateDocumentCollectionAsync**, fiyatlandırmaya yönelik etkilere sahip yeni bir koleksiyon oluşturur. Daha ayrıntılı bilgi için lütfen [fiyatlandırma sayfamızı](https://azure.microsoft.com/pricing/details/cosmos-db/) ziyaret edin.
> 
> 

A [koleksiyonu](documentdb-resources.md#collections) hello kullanarak oluşturulan [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) hello işlevinin **DocumentClient** sınıfı. Koleksiyon, JSON belgelerinin ve ilişkili JavaScript uygulama mantığının bir kapsayıcısıdır.

Kopyalama ve yapıştırma hello **Getfamilydocument** hello altında işlevi **getDatabase** hello ile yeni koleksiyonunuzu hello app.js dosya toocreate işlev ```id``` hello belirtilen```config```nesnesi. Biz toomake yeniden kontrol edeceğiz emin ile bir koleksiyon hello aynı ```FamilyCollection``` kimliği zaten mevcut değil. Varsa yeni bir koleksiyon oluşturmak yerine var olan koleksiyonu getireceğiz.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getCollection() {
        console.log(`Getting collection:\n${config.collection.id}\n`);

        return new Promise((resolve, reject) => {
            client.readCollection(collectionUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

Merhaba çağrısı hello kodu çok kopyalayıp**getDatabase** tooexecute hello **Getfamilydocument** işlevi.

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Terminalinizde bulun, ```app.js``` dosya ve hello komutu çalıştırın:```node app.js```

Tebrikler! Bir Azure Cosmos DB koleksiyonunu başarıyla oluşturdunuz.

## <a id="CreateDoc"></a>7. Adım: Belge oluşturma
A [belge](documentdb-resources.md#documents) hello kullanarak oluşturulan [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) hello işlevinin **DocumentClient** sınıfı. Belgeler, kullanıcı tanımlı (rastgele) JSON içeriğidir. Artık Azure Cosmos DB'ye bir belge yerleştirebilirsiniz.

Kopyalama ve yapıştırma hello **getFamilyDocument** hello altında işlevi **Getfamilydocument** hello kaydedilmiş hello JSON verilerini içeren hello belgeleri oluşturmak için işlevi ```config``` nesnesi. Yeniden, biz toomake emin kontrol edeceğiz bir belgeyle hello aynı kimliği zaten mevcut değil.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Getting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDocument(documentUrl, { partitionKey: document.district }, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDocument(collectionUrl, document, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    };

Merhaba çağrısı hello kodu çok kopyalayıp**Getfamilydocument** tooexecute hello **getFamilyDocument** işlevi.

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Terminalinizde bulun, ```app.js``` dosya ve hello komutu çalıştırın:```node app.js```

Tebrikler! Bir Azure Cosmos DB belgesini başarıyla oluşturdunuz.

![Node.js Öğreticisi - hello hello hesabı, hello veritabanı, hello koleksiyonu ve hello belgeler arasındaki hiyerarşik ilişkiyi gösteren diyagram - Node veritabanı](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <a id="Query"></a>8. Adım: Azure Cosmos DB kaynaklarını sorgulama
Azure Cosmos DB, her bir koleksiyonda depolanan JSON belgeleri için [zengin sorguların](documentdb-sql-query.md) gerçekleştirilmesini destekler. Merhaba aşağıdaki örnek kod koleksiyonunuzda hello belgeleri karşı çalıştırabileceğiniz bir sorguyu gösterir.

Kopyalama ve yapıştırma hello **queryCollection** hello altında işlevi **getFamilyDocument** hello app.js dosyasında işlevi. Azure Cosmos DB, aşağıda gösterildiği gibi SQL benzeri sorguları destekler. Karmaşık sorgular derleme hakkında daha fazla bilgi için hello denetleyin [Query Playground](https://www.documentdb.com/sql/demo) ve hello [sorgu belgelerini](documentdb-sql-query.md).

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function queryCollection() {
        console.log(`Querying collection through index:\n${config.collection.id}`);

        return new Promise((resolve, reject) => {
            client.queryDocuments(
                collectionUrl,
                'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
            ).toArray((err, results) => {
                if (err) reject(err)
                else {
                    for (var queryResult of results) {
                        let resultString = JSON.stringify(queryResult);
                        console.log(`\tQuery returned ${resultString}`);
                    }
                    console.log();
                    resolve(results);
                }
            });
        });
    };


Aşağıdaki diyagramda hello nasıl hello Azure Cosmos DB SQL sorgusu söz dizimi karşı hello koleksiyonu olarak adlandırılır, oluşturduğunuz gösterilmektedir.

![Node.js Öğreticisi - hello kapsamını ve hello sorgunun anlamını diyagram - Node veritabanı](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

Merhaba [FROM](documentdb-sql-query.md#FromClause) Azure Cosmos DB sorguları kapsamlı tooa tek koleksiyon zaten olduğu için anahtar sözcüğü hello sorguda isteğe bağlıdır. Bu nedenle, "FROM Families f", "FROM root r" veya seçtiğiniz herhangi bir başka değişken adıyla değiştirilebilir. Azure Cosmos DB aileleri, kök veya hello değişken adı, seçtiğiniz, başvuru hello geçerli koleksiyonu varsayılan olarak Infer.

Merhaba çağrısı hello kodu çok kopyalayıp**getFamilyDocument** tooexecute hello **queryCollection** işlevi.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Terminalinizde bulun, ```app.js``` dosya ve hello komutu çalıştırın:```node app.js```

Tebrikler! Başarılı bir şekilde Azure Cosmos DB belgelerini sorguladınız.

## <a id="ReplaceDocument"></a>9. Adım: Bir belgeyi değiştirme
Azure Cosmos DB, JSON belgelerini değiştirmeyi destekler.

Kopyalama ve yapıştırma hello **replaceFamilyDocument** hello altında işlevi **queryCollection** hello app.js dosyasında işlevi.

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function replaceFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Replacing document:\n${document.id}\n`);
        document.children[0].grade = 6;

        return new Promise((resolve, reject) => {
            client.replaceDocument(documentUrl, document, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

Merhaba çağrısı hello kodu çok kopyalayıp**queryCollection** tooexecute hello **replaceDocument** işlevi. Ayrıca, hello kod toocall ekleme **queryCollection** yeniden tooverify hello Belge başarıyla değiştirildi.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Terminalinizde bulun, ```app.js``` dosya ve hello komutu çalıştırın:```node app.js```

Tebrikler! Başarılı bir şekilde bir Azure Cosmos DB belgesini değiştirdiniz.

## <a id="DeleteDocument"></a>10. Adım: Bir belgeyi silme
Azure Cosmos DB, JSON belgelerini silmeyi destekler.

Kopyalama ve yapıştırma hello **deleteFamilyDocument** hello altında işlevi **replaceFamilyDocument** işlevi.

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function deleteFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Deleting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.deleteDocument(documentUrl, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

Merhaba çağrısı toohello hello kodu ikinci kopyalayıp **queryCollection** tooexecute hello **deleteDocument** işlevi.

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Terminalinizde bulun, ```app.js``` dosya ve hello komutu çalıştırın:```node app.js```

Tebrikler! Başarılı bir şekilde bir Azure Cosmos DB belgesini sildiniz.

## <a id="DeleteDatabase"></a>11. adım: hello Node veritabanını silme
Veritabanı oluşturulan silme hello hello veritabanı ve tüm alt kaynaklar (koleksiyonlar, belgeler, vb.) kaldırır.

Kopyalama ve yapıştırma hello **Temizleme** hello altında işlevi **deleteFamilyDocument** tooremove hello veritabanı ve tüm hello alt kaynaklarını işlevi.

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

Merhaba çağrısı hello kodu çok kopyalayıp**deleteFamilyDocument** tooexecute hello **Temizleme** işlevi.

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <a id="Run"></a>12. Adım: Node.js uygulamanızı hep birlikte çalıştırın!
Tamamen işlevlerinizi çağırma hello dizisi aşağıdaki gibi görünmelidir:

    getDatabase()
    .then(() => getCollection())
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    .then(() => cleanup())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Terminalinizde bulun, ```app.js``` dosya ve hello komutu çalıştırın:```node app.js```

Merhaba Başlarken uygulamanızın çıktısını görmeniz gerekir. Merhaba çıktı hello örnek metinle eşleşmelidir.

    Getting database:
    FamilyDB

    Getting collection:
    FamilyColl

    Getting document:
    Anderson.1

    Getting document:
    Wakefield.7

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":5,"pets":[{"givenName":"Fluffy"}]}]

    Replacing document:
    Anderson.1

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":6,"pets":[{"givenName":"Fluffy"}]}]

    Deleting document:
    Anderson.1

    Cleaning up by deleting database FamilyDB
    Completed successfully
    Press any key tooexit

Tebrikler! Oluşturduğunuz hello Node.js öğreticisini tamamladınız ve İlk Azure Cosmos DB konsol uygulamanız sahip!

## <a id="GetSolution"></a>Merhaba eksiksiz Node.js Öğreticisi çözümünü edinme
Bu öğreticide adımları hello ya da yalnızca toodownload hello kod istediğiniz zaman toocomplete varsa alamadık, buradan edinebilirsiniz [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).

Bu makaledeki tüm hello örnekleri içeren toorun hello GetStarted çözümünü hello aşağıdaki gerekir:

* [Azure Cosmos DB hesabı][create-account].
* Merhaba [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) çözüm Github'da kullanılabilir.

Merhaba yüklemek **documentdb** npm aracılığıyla modülü. Merhaba aşağıdaki komutu kullanın:

* ```npm install documentdb --save```

Merhaba sonraki ```config.js``` dosya, güncelleştirme hello config.endpoint ve config.authKey değerlerini açıklandığı gibi [3. adım: uygulamanızın yapılandırmalarını ayarlama](#Config). 

Terminalinizde bulun, ```app.js``` dosya ve hello komutu çalıştırın: ```node app.js```.

Hepsi bu kadar, derleyin ve devam edin! 

## <a name="next-steps"></a>Sonraki adımlar
* Daha karmaşık bir Node.js örneği ister misiniz? Bkz. [Azure Cosmos DB kullanarak bir Node.js web uygulaması oluşturma](documentdb-nodejs-application.md).
* Nasıl çok öğrenin[Azure Cosmos DB hesabını izleme](monitor-accounts.md).
* Merhaba, örnek veri kümelerimizde sorgular çalıştırın [Query Playground](https://www.documentdb.com/sql/demo).
* Merhaba hello hello geliştirme bölümünde programlama modelleri hakkında daha fazla bilgi edinin [Azure Cosmos DB belge sayfasının](https://azure.microsoft.com/documentation/services/documentdb/).

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
