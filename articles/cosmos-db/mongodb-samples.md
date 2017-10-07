---
title: aaaUse MongoDB API'leri toobuild Azure Cosmos DB uygulama | Microsoft Docs
description: "MongoDB için hello Azure Cosmos DB API'lerini kullanarak çevrimiçi bir veritabanı oluşturan Öğreticisi."
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
ms.openlocfilehash: 09be4362fe3aac02e0163325f958210be9598383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-azure-cosmos-db-api-for-mongodb-app-using-nodejs"></a>Bir Azure Cosmos DB yapı: Node.js kullanarak MongoDB uygulaması için API
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [MongoDB için Node.js](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
>

Bu örnekte, nasıl gösterir toobuild bir Azure Cosmos DB: Node.js kullanarak MongoDB konsol uygulaması için API.

toouse Bu örnekte, şunları yapmalısınız:

* [Oluşturma](create-mongodb-dotnet.md#create-account) bir Azure Cosmos DB: API MongoDB hesabı.
* MongoDB almak [bağlantı dizesi](connect-mongodb-account.md) bilgi.

## <a name="create-hello-app"></a>Merhaba uygulaması oluşturma

1. Oluşturma bir *app.js* dosya ve kopyalama & hello aşağıdaki kodu yapıştırın.

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
        console.log("Inserted a document into hello families collection.");
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

2. Merhaba değişkenleri aşağıdaki hello değiştirme *app.js* hesap ayarlarınızı başına dosyası (öğrenin nasıl toofind, [bağlantı dizesi](connect-mongodb-account.md)):
   
    ```nodejs
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10255/?ssl=true';
    ```
     
3. Sık kullandığınız Terminali açın, çalıştırmak **npm kaydetme mongodb--yükleme**, uygulamanızı çalıştırın **düğümü app.js**

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[MongoChef kullanmak](mongodb-mongochef.md) Azure Cosmos DB ile: API MongoDB hesabı.
