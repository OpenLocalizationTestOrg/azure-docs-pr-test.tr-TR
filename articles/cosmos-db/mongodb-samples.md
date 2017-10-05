---
title: "Bir Azure Cosmos DB uygulamanızı oluşturmak için MongoDB API'leri kullanan | Microsoft Docs"
description: "MongoDB için Azure Cosmos DB API'lerini kullanarak çevrimiçi bir veritabanı oluşturan Öğreticisi."
keywords: "mongodb örnekleri"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: fb38bc53-3561-487d-9e03-20f232319a87
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: anhoh
ms.openlocfilehash: 433d2e585c884a10e7e923a0b27c179a95410d01
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="build-an-azure-cosmos-db-api-for-mongodb-app-using-nodejs"></a><span data-ttu-id="42a7f-104">Bir Azure Cosmos DB yapı: Node.js kullanarak MongoDB uygulaması için API</span><span class="sxs-lookup"><span data-stu-id="42a7f-104">Build an Azure Cosmos DB: API for MongoDB app using Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="42a7f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="42a7f-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="42a7f-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="42a7f-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="42a7f-107">Java</span><span class="sxs-lookup"><span data-stu-id="42a7f-107">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="42a7f-108">MongoDB için Node.js</span><span class="sxs-lookup"><span data-stu-id="42a7f-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="42a7f-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="42a7f-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="42a7f-110">C++</span><span class="sxs-lookup"><span data-stu-id="42a7f-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
>

<span data-ttu-id="42a7f-111">Bu örnek bir Azure Cosmos DB nasıl oluşturulacağını gösterir: Node.js kullanarak MongoDB konsol uygulaması için API.</span><span class="sxs-lookup"><span data-stu-id="42a7f-111">This example shows you how to build an Azure Cosmos DB: API for MongoDB console app using Node.js.</span></span>

<span data-ttu-id="42a7f-112">Bu örneği kullanmak için yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="42a7f-112">To use this example, you must:</span></span>

* <span data-ttu-id="42a7f-113">[Oluşturma](create-mongodb-dotnet.md#create-account) bir Azure Cosmos DB: API MongoDB hesabı.</span><span class="sxs-lookup"><span data-stu-id="42a7f-113">[Create](create-mongodb-dotnet.md#create-account) an Azure Cosmos DB: API for MongoDB account.</span></span>
* <span data-ttu-id="42a7f-114">MongoDB almak [bağlantı dizesi](connect-mongodb-account.md) bilgi.</span><span class="sxs-lookup"><span data-stu-id="42a7f-114">Retrieve your MongoDB [connection string](connect-mongodb-account.md) information.</span></span>

## <a name="create-the-app"></a><span data-ttu-id="42a7f-115">Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="42a7f-115">Create the app</span></span>

1. <span data-ttu-id="42a7f-116">Oluşturma bir *app.js* dosya ve kopyalayın ve aşağıdaki kodu yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="42a7f-116">Create a *app.js* file and copy & paste the code below.</span></span>

    ```nodejs
    var MongoClient = require('mongodb').MongoClient;
    var assert = require('assert');
    var ObjectId = require('mongodb').ObjectID;
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10255/?ssl=true';

    var insertDocument = function(db, callback) {
    db.collection('families').insertOne( {
            "id": "AndersenFamily",
            "lastName": "Andersen",
            "parents": [
                { "firstName": "Thomas" },
                { "firstName": "Mary Kay" }
            ],
            "children": [
                { "firstName": "John", "gender": "male", "grade": 7 }
            ],
            "pets": [
                { "givenName": "Fluffy" }
            ],
            "address": { "country": "USA", "state": "WA", "city": "Seattle" }
        }, function(err, result) {
        assert.equal(err, null);
        console.log("Inserted a document into the families collection.");
        callback();
    });
    };
    
    var findFamilies = function(db, callback) {
    var cursor =db.collection('families').find( );
    cursor.each(function(err, doc) {
        assert.equal(err, null);
        if (doc != null) {
            console.dir(doc);
        } else {
            callback();
        }
    });
    };
    
    var updateFamilies = function(db, callback) {
    db.collection('families').updateOne(
        { "lastName" : "Andersen" },
        {
            $set: { "pets": [
                { "givenName": "Fluffy" },
                { "givenName": "Rocky"}
            ] },
            $currentDate: { "lastModified": true }
        }, function(err, results) {
        console.log(results);
        callback();
    });
    };
    
    var removeFamilies = function(db, callback) {
    db.collection('families').deleteMany(
        { "lastName": "Andersen" },
        function(err, results) {
            console.log(results);
            callback();
        }
    );
    };
    
    MongoClient.connect(url, function(err, db) {
    assert.equal(null, err);
    insertDocument(db, function() {
        findFamilies(db, function() {
        updateFamilies(db, function() {
            removeFamilies(db, function() {
                db.close();
            });
        });
        });
    });
    });
    ```

2. <span data-ttu-id="42a7f-117">Aşağıdaki değişkenler değiştirme *app.js* hesap ayarlarınızı başına dosyası (nasıl bulacağınızı öğrenin, [bağlantı dizesi](connect-mongodb-account.md)):</span><span class="sxs-lookup"><span data-stu-id="42a7f-117">Modify the following variables in the *app.js* file per your account settings (Learn how to find your [connection string](connect-mongodb-account.md)):</span></span>
   
    ```nodejs
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10255/?ssl=true';
    ```
     
3. <span data-ttu-id="42a7f-118">Sık kullandığınız Terminali açın, çalıştırmak **npm kaydetme mongodb--yükleme**, uygulamanızı çalıştırın **düğümü app.js**</span><span class="sxs-lookup"><span data-stu-id="42a7f-118">Open your favorite terminal, run **npm install mongodb --save**, then run your app with **node app.js**</span></span>

## <a name="next-steps"></a><span data-ttu-id="42a7f-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="42a7f-119">Next steps</span></span>
* <span data-ttu-id="42a7f-120">Bilgi nasıl [MongoChef kullanmak](mongodb-mongochef.md) Azure Cosmos DB ile: API MongoDB hesabı.</span><span class="sxs-lookup"><span data-stu-id="42a7f-120">Learn how to [use MongoChef](mongodb-mongochef.md) with your Azure Cosmos DB: API for MongoDB account.</span></span>
