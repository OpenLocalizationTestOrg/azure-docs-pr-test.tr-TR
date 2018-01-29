---
title: "Azure Cosmos DB SQL API'yi için node.js Öğreticisi | Microsoft Docs"
description: "Cosmos DB SQL API ile oluşturan bir Node.js Öğreticisi."
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
ms.openlocfilehash: 3cfea11e70309c56f991f5d563649741c675c907
ms.sourcegitcommit: 5ac112c0950d406251551d5fd66806dc22a63b01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/23/2018
---
# <a name="nodejs-tutorial-use-the-sql-api-in-azure-cosmos-db-to-create-a-nodejs-console-application"></a>Node.js Öğreticisi: SQL API Azure Cosmos DB'de bir Node.js konsol uygulaması oluşturmak için kullanın.
> [!div class="op_single_selector"]
> * [.NET](sql-api-get-started.md)
> * [.NET Core](sql-api-dotnetcore-get-started.md)
> * [MongoDB için Node.js](mongodb-samples.md)
> * [Node.js](sql-api-nodejs-get-started.md)
> * [Java](sql-api-java-get-started.md)
> * [C++](sql-api-cpp-get-started.md)
>  
> 

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)]

Azure Cosmos DB Node.js SDK'sı için Node.js öğreticisine hoş geldiniz! Bu öğreticiyi uyguladıktan sonra, Azure Cosmos DB kaynaklarını oluşturan ve sorgulayan bir konsol uygulamasına sahip olacaksınız.

Şu konulara değineceğiz:

* Azure Cosmos DB hesabı oluşturma ve hesaba bağlanma
* Uygulamanızı kurma
* Düğüm veritabanı oluşturma
* Koleksiyon oluşturma
* JSON belgeleri oluşturma
* Koleksiyonu sorgulama
* Bir belgeyi değiştirme
* Bir belgeyi silme
* Düğüm veritabanını silme

Zamanınız yok mu? Endişelenmeyin! Eksiksiz çözümü [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started)'da bulabilirsiniz. Hızlı yönergeler için bkz. [Eksiksiz çözüm edinme](#GetSolution).

Node.js öğreticisini tamamladıktan sonra, bize geri bildirim sağlamak için lütfen bu sayfanın üst ve alt kısmındaki oylama düğmelerini kullanın. Doğrudan sizinle iletişim kurmamızı isterseniz yorumlarınıza e-posta adresinizi ekleyin.

Şimdi başlayalım!

## <a name="prerequisites-for-the-nodejs-tutorial"></a>Node.js öğreticisi için önkoşullar
Lütfen aşağıdakilere sahip olduğunuzdan emin olun:

* Etkin bir Azure hesabı. Bir aboneliğiniz yoksa [Ücretsiz Azure Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz. 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* [Node.js](https://nodejs.org/) v0.10.29 sürümü veya sonraki bir sürüm.

## <a name="step-1-create-an-azure-cosmos-db-account"></a>1. Adım: Azure Cosmos DB hesabı oluşturma
Bir Azure Cosmos DB hesabı oluşturalım. Kullanmak istediğiniz bir hesap zaten varsa, atlayabilirsiniz [Node.js uygulamanızı ayarlama](#SetupNode). Azure Cosmos DB öykünücüsü kullanıyorsanız, lütfen bölümündeki adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) öykünücü kurulması ve için İleri atlayabilirsiniz [Node.js uygulamanızı ayarlama](#SetupNode).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupNode"></a>2. adım: Node.js uygulamanızı ayarlama
1. Sık kullandığınız terminali açın.
2. Node.js uygulamanızı kaydetmek istediğiniz klasör veya dizini bulun.
3. Aşağıdaki komutlarla iki adet boş JavaScript dosyası oluşturun:
   * Windows:
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * Linux/OS X:
     * ```touch app.js```
     * ```touch config.js```
4. Npm aracılığıyla documentdb modülünü yükleyin. Aşağıdaki komutu kullanın:
   * ```npm install documentdb --save```

Harika! Kurulumu tamamladığınıza göre, biraz kod yazmaya başlayalım.

## <a id="Config"></a>3. Adım: Uygulamanızın yapılandırmalarını ayarlama
Sık kullandığınız metin düzenleyicisinde ```config.js``` öğesini açın.

Ardından, kopyalama ve yapıştırma aşağıdaki kod parçacığında ve özelliklerini ayarlama ```config.endpoint``` ve ```config.primaryKey``` Azure Cosmos DB uç noktası uri ve birincil anahtar. Her iki Bu yapılandırmalar bulunabilir [Azure portal](https://portal.azure.com).

![Node.js Öğreticisi - etkin hub ile bir Azure Cosmos DB hesabını gösteren Azure portal ekran görüntüsü, Azure Cosmos DB hesabı dikey ve anahtarlar dikey penceresinde URI, birincil anahtar ve ikincil anahtar değerleri vurgulanmış ANAHTARLAR düğmesi vurgulanmış- Node veritabanı][keys]

    // ADD THIS PART TO YOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

Aşağıdaki ```config.endpoint``` ve ```config.primaryKey``` özelliklerinizi ayarladığınız ```config``` nesnenize ```database id```, ```collection id``` ve ```JSON documents``` öğelerini kopyalayıp yapıştırın. Veritabanınızda depolamak istediğiniz veriler zaten varsa belge tanımları eklemek yerine Azure Cosmos DB'nin [Veri Geçiş Aracı](import-data.md)'nı kullanabilirsiniz.

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART TO YOUR CODE
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


Veritabanı, koleksiyon ve belge tanımları, Azure Cosmos DB hareket edecek ```database id```, ```collection id```ve belgelerin verileri.

Son olarak, ```app.js``` dosyasının içinde başvurabilmek için ```config``` nesnenizi dışarı aktarın.

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART TO YOUR CODE
    module.exports = config;

## <a id="Connect"></a> 4. Adım: Azure Cosmos DB hesabına bağlanma
Bir metin düzenleyicisinde boş ```app.js``` dosyanızı açın. ```documentdb``` modülünü ve yeni oluşturduğunuz ```config``` modülünü içeri aktarmak için aşağıdaki kodu kopyalayıp yapıştırın.

    // ADD THIS PART TO YOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

Yeni bir DocumentClient oluşturmak için, önceden kaydedilen ```config.endpoint``` ve ```config.primaryKey``` öğelerini kullanmak amacıyla kodu kopyalayıp yapıştırın.

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART TO YOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

Azure Cosmos DB istemcisini başlatmaya yarayacak koda sahip olduğunuza göre Azure Cosmos DB kaynaklarla çalışmak bir bakalım.

## <a name="step-5-create-a-node-database"></a>5. Adım: Düğüm veritabanı oluşturma
Not Found, database url ve collection url için HTTP durumunu ayarlamak üzere aşağıdaki kodu kopyalayıp yapıştırın. Bu URL'leri Azure Cosmos DB istemci doğru veritabanı ve koleksiyonu nasıl bulacaksınız ' dir.

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART TO YOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

Bir [veritabanı](sql-api-resources.md#databases), **DocumentClient** sınıfının [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) işlevi kullanılarak oluşturulabilir. Veritabanı, koleksiyonlar genelinde bölümlenmiş belge depolama alanının mantıksal bir kapsayıcısıdır.

```config``` nesnesinde ```id``` belirtilmiş şekilde app.js dosyasında yeni veritabanınızı oluşturmak için **getDatabase** işlevini kopyalayın ve yapıştırın. İşlev, aynı ```FamilyRegistry``` kimliğine sahip bir veritabanının zaten var olup olmadığını denetler. Varsa yeni bir veritabanı oluşturmak yerine var olan veritabanını getireceğiz.

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART TO YOUR CODE
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

Aşağıdaki kodu kopyalayın ve çıkış iletisini ve **getDatabase** işlevine çağrıyı yazdıracak **exit** yardımcı işlevini eklemek için **getDatabase** işlevini ayarladığınız yere yapıştırın.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key to exit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Terminalinizde ```app.js``` dosyanızı bulun ve şu komutu çalıştırın: ```node app.js```

Tebrikler! Başarılı bir şekilde bir Azure Cosmos DB veritabanı oluşturdunuz.

## <a id="CreateColl"></a>6. Adım: Koleksiyon oluşturma
> [!WARNING]
> **createCollection** fiyatlandırmaya sahip yeni bir koleksiyon oluşturur. Daha ayrıntılı bilgi için lütfen [fiyatlandırma sayfamızı](https://azure.microsoft.com/pricing/details/cosmos-db/) ziyaret edin.
> 
> 

Bir [koleksiyon](sql-api-resources.md#collections), **DocumentClient** sınıfının [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) işlevi kullanılarak oluşturulabilir. Koleksiyon, JSON belgelerinin ve ilişkili JavaScript uygulama mantığının bir kapsayıcısıdır.

```config``` nesnesinde belirtilmiş ```id``` ile yeni koleksiyonunuzu oluşturmak üzere **getCollection** işlevini kopyalayıp app.js dosyasındaki **getDatabase** işlevinin altına yapıştırın. Yine aynı ```FamilyCollection``` kimliğine sahip bir koleksiyonun zaten var olup olmadığını denetleyeceğiz. Varsa yeni bir koleksiyon oluşturmak yerine var olan koleksiyonu getireceğiz.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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

**getCollection** işlevini yürütmek için **getDatabase**'e yönelik çağrının altında bulunan kodu kopyalayın ve yapıştırın.

    getDatabase()

    // ADD THIS PART TO YOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Terminalinizde ```app.js``` dosyanızı bulun ve şu komutu çalıştırın: ```node app.js```

Tebrikler! Bir Azure Cosmos DB koleksiyonunu başarıyla oluşturdunuz.

## <a id="CreateDoc"></a>7. Adım: Belge oluşturma
Bir [belge](sql-api-resources.md#documents), **DocumentClient** sınıfının [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) işlevi kullanılarak oluşturulabilir. Belgeler, kullanıcı tanımlı (rastgele) JSON içeriğidir. Artık Azure Cosmos DB'ye bir belge yerleştirebilirsiniz.

```config``` nesnesinde kaydedilen JSON verilerini içeren belgeleri oluşturmak için **getFamilyDocument** işlevini **getCollection** işlevinin altına kopyalayıp yapıştırın. Yine aynı kimliğe sahip bir belgenin zaten var olup olmadığını denetleyeceğiz.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
    function getFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Getting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDocument(documentUrl, (err, result) => {
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

**getFamilyDocument** işlevini yürütmek için **getCollection** işlevine yönelik çağrının altına kodu kopyalayıp yapıştırın.

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Terminalinizde ```app.js``` dosyanızı bulun ve şu komutu çalıştırın: ```node app.js```

Tebrikler! Bir Azure Cosmos DB belgesini başarıyla oluşturdunuz.

![Node.js öğreticisi - Hesap, veritabanı, koleksiyon ve belgeler arasındaki hiyerarşik ilişkiyi gösteren diyagram - Node veritabanı](./media/sql-api-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <a id="Query"></a>8. Adım: Azure Cosmos DB kaynaklarını sorgulama
Azure Cosmos DB, her bir koleksiyonda depolanan JSON belgeleri için [zengin sorguların](sql-api-sql-query.md) gerçekleştirilmesini destekler. Aşağıdaki örnek kod, koleksiyonunuzdaki belgeler için çalıştırabileceğiniz bir sorguyu gösterir.

**queryCollection** işlevini kopyalayıp app.js dosyasındaki **getFamilyDocument** işlevinin altına yapıştırın. Azure Cosmos DB, aşağıda gösterildiği gibi SQL benzeri sorguları destekler. Karmaşık sorgular derleme hakkında daha fazla bilgi için [Query Playground](https://www.documentdb.com/sql/demo) sayfasını ve [sorgu belgelerini](sql-api-sql-query.md) inceleyin.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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


Aşağıdaki diyagramda nasıl Azure Cosmos DB SQL sorgusu söz dizimi karşı koleksiyonu çağrıldığı gösterilmektedir oluşturuldu.

![Node.js öğreticisi - Sorgunun kapsamını ve sorgunun anlamını gösteren diyagram - Node veritabanı](./media/sql-api-nodejs-get-started/node-js-tutorial-collection-documents.png)

[FROM](sql-api-sql-query.md#FromClause) Azure Cosmos DB sorguları zaten tek bir koleksiyon kapsamında olduğundan anahtar sözcüğü sorguda isteğe bağlıdır. Bu nedenle, "FROM Families f", "FROM root r" veya seçtiğiniz herhangi bir başka değişken adıyla değiştirilebilir. Azure Cosmos DB Families, root veya seçtiğiniz değişken adı olarak Infer, varsayılan olarak geçerli koleksiyonun başvuru.

**queryCollection** işlevini yürütmek için kodu kopyalayıp **getFamilyDocument**'a yönelik çağrının altına yapıştırın.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART TO YOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Terminalinizde ```app.js``` dosyanızı bulun ve şu komutu çalıştırın: ```node app.js```

Tebrikler! Başarılı bir şekilde Azure Cosmos DB belgelerini sorguladınız.

## <a id="ReplaceDocument"></a>9. Adım: Bir belgeyi değiştirme
Azure Cosmos DB, JSON belgelerini değiştirmeyi destekler.

**replaceFamilyDocument** işlevini kopyalayıp app.js dosyasındaki **queryCollection** işlevinin altına yapıştırın.

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
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

**replaceDocument** işlevini yürütmek için **queryCollection**'a çağrının altına kodu kopyalayıp yapıştırın. Ayrıca, belgenin başarılı bir şekilde değiştiğini doğrulamak üzere **queryCollection**'ı tekrar çağırmak için kodu ekleyin.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Terminalinizde ```app.js``` dosyanızı bulun ve şu komutu çalıştırın: ```node app.js```

Tebrikler! Başarılı bir şekilde bir Azure Cosmos DB belgesini değiştirdiniz.

## <a id="DeleteDocument"></a>10. Adım: Bir belgeyi silme
Azure Cosmos DB, JSON belgelerini silmeyi destekler.

**deleteFamilyDocument** işlevini **replaceFamilyDocument** işlevinin altına kopyalayıp yapıştırın.

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
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

**deleteDocument** işlevini yürütmek için ikinci **queryCollection**'a çağrının altına kodu kopyalayın ve yapıştırın.

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Terminalinizde ```app.js``` dosyanızı bulun ve şu komutu çalıştırın: ```node app.js```

Tebrikler! Başarılı bir şekilde bir Azure Cosmos DB belgesini sildiniz.

## <a id="DeleteDatabase"></a>11. Adım: Node veritabanını silme
Oluşturulan veritabanı silindiğinde, veritabanı ve tüm alt kaynaklar (koleksiyonlar, belgeler vb.) kaldırılır.

Veritabanını ve tüm alt kaynaklarını kaldırmak için **cleanup** işlevini kopyalayıp **deleteFamilyDocument** işlevinin altına yapıştırın.

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

**cleanup** işlevini yürütmek için **deleteFamilyDocument**'a çağrının altına kodu kopyalayıp yapıştırın.

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART TO YOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <a id="Run"></a>12. Adım: Node.js uygulamanızı hep birlikte çalıştırın!
İşlevlerinizi çağırma dizisinin bütünüyle şu şekilde görünmesi gerekir:

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

Terminalinizde ```app.js``` dosyanızı bulun ve şu komutu çalıştırın: ```node app.js```

Başlarken uygulamanızın çıktısını görmeniz gerekir. Çıktı aşağıdaki örnek metinle eşleşmelidir.

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
    Press any key to exit

Tebrikler! Node.js öğreticisini tamamladınız ve ilk Azure Cosmos DB konsol uygulamanızı oluşturdunuz!

## <a id="GetSolution"></a>Eksiksiz Node.js öğreticisi çözümünü edinme
Bu öğreticideki adımları tamamlama fırsatınız olmadıysa veya yalnızca kodu indirmek isterseniz [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started)'dan ulaşabilirsiniz.

Bu makaledeki tüm örnekleri içeren GetStarted çözümünü çalıştırmak için aşağıdakilere ihtiyacınız vardır:

* [Azure Cosmos DB hesabı][create-account].
* GitHub'da bulunan [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) çözümü.

Npm aracılığıyla **documentdb** modülünü yükleyin. Aşağıdaki komutu kullanın:

* ```npm install documentdb --save```

İleri ' ```config.js``` dosya, config.endpoint ve config.primaryKey değerleri açıklandığı gibi güncelleştirin [3. adım: uygulamanızın yapılandırmalarını ayarlama](#Config). 

Ardından terminalinizde ```app.js``` dosyanızı bulun ve şu komutu çalıştırın: ```node app.js```.

Hepsi bu kadar, derleyin ve devam edin! 

## <a name="next-steps"></a>Sonraki adımlar
* Daha karmaşık bir Node.js örneği ister misiniz? Bkz. [Azure Cosmos DB kullanarak bir Node.js web uygulaması oluşturma](sql-api-nodejs-application.md).
* [Azure Cosmos DB hesabını nasıl izleyebileceğinizi](monitor-accounts.md) öğrenin.
* [Query Playground](https://www.documentdb.com/sql/demo)'daki örnek veri kümelerimizde sorgular çalıştırın.

[create-account]: create-sql-api-dotnet.md#create-account
[keys]: media/sql-api-nodejs-get-started/node-js-tutorial-keys.png
