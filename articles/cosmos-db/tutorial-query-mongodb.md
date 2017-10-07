---
title: "Azure Cosmos DB: Nasıl tooquery kullanarak hello DocumentDB API? | Microsoft Belgeleri"
description: Azure Cosmos DB tooquery hello DocumentDB API ile bilgi edinin
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: e3e5a49f7510942bcfb15330e5f86c5dd8b1e5d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-api-for-mongodb"></a>Azure Cosmos DB: Nasıl API MongoDB için ile tooquery?

Hello Azure Cosmos DB [API MongoDB için](mongodb-introduction.md) destekleyen [MongoDB Kabuk sorguları](https://docs.mongodb.com/manual/tutorial/query-documents/). 

Bu makalede görevleri aşağıdaki hello yer almaktadır: 

> [!div class="checklist"]
> * MongoDB ile verileri Sorgulama

## <a name="sample-document"></a>Örnek bir belge

Bu makalede Hello sorguları örnek bir belge aşağıdaki hello kullanın.

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
## <a id="examplequery1"></a>Örnek sorgu 1 

Merhaba örnek ailesi belge yukarıdaki verildiğinde, hello aşağıdaki hello Kimliği alanı eşleştiği döndürür hello belgeleri sorgu `WakefieldFamily`.

**Sorgu**
    
    db.families.find({ id: “WakefieldFamily”})

**Sonuçları**

    {
    "_id": "ObjectId(\"58f65e1198f3a12c7090e68c\")",
    "id": "WakefieldFamily",
    "parents": [
      {
        "familyName": "Wakefield",
        "givenName": "Robin"
      },
      {
        "familyName": "Miller",
        "givenName": "Ben"
      }
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
    "address": {
      "state": "NY",
      "county": "Manhattan",
      "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
    }

## <a id="examplequery2"></a>Örnek Sorgu 2 

Merhaba sonraki sorgu hello ailesinde tüm hello alt öğelerini döndürür. 

**Sorgu**
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

**Sonuçları**

    {
    "_id": "ObjectId("58f65e1198f3a12c7090e68c")",
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
    ]
    }


## <a id="examplequery3"></a>Örnek sorgu 3 

Merhaba sonraki sorgu kayıtlı tüm hello aileleri döndürür. 

**Sorgu**
    
    db.families.find( { "isRegistered" : true })
**Sonuçları** hiçbir belge döndürülür. 

## <a id="examplequery4"></a>Örnek sorgu 4

Merhaba sonraki sorgu kayıtlı değil tüm hello aileleri döndürür. 

**Sorgu**
    
    db.families.find( { "isRegistered" : false })
**Sonuçları**

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
}

## <a id="examplequery5"></a>Örnek sorgu 5

Tüm kayıtlı değil hello aileleri ve durumudur NY Hello sonraki sorgu döndürür. 

**Sorgu**
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

**Sonuçları**

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
}


## <a id="examplequery6"></a>Örnek sorgu 6

Merhaba sonraki sorgu alt dereceleri 8 olduğu tüm hello aileleri döndürür.

**Sorgu**
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

**Sonuçları**

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
}

## <a id="examplequery7"></a>Örnek sorgu 7

Merhaba sonraki sorgu alt dizinin boyutu 3 olduğu tüm hello aileleri döndürür.

**Sorgu**
  
      db.Family.find( {children: { $size:3} } )

**Sonuçları**

2'den fazla alt öğe yok gibi sonuç döndürülür. Yalnızca parametresi 2 olduğunda bu sorgu başarılı ve hello tam belge döndürür.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, hello aşağıdakileri yaptığınızdan:

> [!div class="checklist"]
> * Nasıl öğrenilen tooquery MongoDB kullanma 

Toohello sonraki öğretici toolearn nasıl şimdi devam toodistribute verilerinizi genel.

> [!div class="nextstepaction"]
> [Verilerinizi genel Dağıt](tutorial-global-distribution-documentdb.md)

