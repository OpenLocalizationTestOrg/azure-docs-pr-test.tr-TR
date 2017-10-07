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
# <a name="azure-cosmos-db-how-tooquery-with-api-for-mongodb"></a><span data-ttu-id="6a974-104">Azure Cosmos DB: Nasıl API MongoDB için ile tooquery?</span><span class="sxs-lookup"><span data-stu-id="6a974-104">Azure Cosmos DB: How tooquery with API for MongoDB?</span></span>

<span data-ttu-id="6a974-105">Hello Azure Cosmos DB [API MongoDB için](mongodb-introduction.md) destekleyen [MongoDB Kabuk sorguları](https://docs.mongodb.com/manual/tutorial/query-documents/).</span><span class="sxs-lookup"><span data-stu-id="6a974-105">hello Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span></span> 

<span data-ttu-id="6a974-106">Bu makalede görevleri aşağıdaki hello yer almaktadır:</span><span class="sxs-lookup"><span data-stu-id="6a974-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="6a974-107">MongoDB ile verileri Sorgulama</span><span class="sxs-lookup"><span data-stu-id="6a974-107">Querying data with MongoDB</span></span>

## <a name="sample-document"></a><span data-ttu-id="6a974-108">Örnek bir belge</span><span class="sxs-lookup"><span data-stu-id="6a974-108">Sample document</span></span>

<span data-ttu-id="6a974-109">Bu makalede Hello sorguları örnek bir belge aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="6a974-109">hello queries in this article use hello following sample document.</span></span>

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
## <span data-ttu-id="6a974-110"><a id="examplequery1"></a>Örnek sorgu 1</span><span class="sxs-lookup"><span data-stu-id="6a974-110"><a id="examplequery1"></a> Example query 1</span></span> 

<span data-ttu-id="6a974-111">Merhaba örnek ailesi belge yukarıdaki verildiğinde, hello aşağıdaki hello Kimliği alanı eşleştiği döndürür hello belgeleri sorgu `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="6a974-111">Given hello sample family document above, hello following query returns hello documents where hello id field matches `WakefieldFamily`.</span></span>

<span data-ttu-id="6a974-112">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="6a974-112">**Query**</span></span>
    
    db.families.find({ id: “WakefieldFamily”})

<span data-ttu-id="6a974-113">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="6a974-113">**Results**</span></span>

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

## <span data-ttu-id="6a974-114"><a id="examplequery2"></a>Örnek Sorgu 2</span><span class="sxs-lookup"><span data-stu-id="6a974-114"><a id="examplequery2"></a>Example query 2</span></span> 

<span data-ttu-id="6a974-115">Merhaba sonraki sorgu hello ailesinde tüm hello alt öğelerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="6a974-115">hello next query returns all hello children in hello family.</span></span> 

<span data-ttu-id="6a974-116">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="6a974-116">**Query**</span></span>
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

<span data-ttu-id="6a974-117">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="6a974-117">**Results**</span></span>

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


## <span data-ttu-id="6a974-118"><a id="examplequery3"></a>Örnek sorgu 3</span><span class="sxs-lookup"><span data-stu-id="6a974-118"><a id="examplequery3"></a>Example query 3</span></span> 

<span data-ttu-id="6a974-119">Merhaba sonraki sorgu kayıtlı tüm hello aileleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="6a974-119">hello next query returns all hello families which are registered.</span></span> 

<span data-ttu-id="6a974-120">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="6a974-120">**Query**</span></span>
    
    db.families.find( { "isRegistered" : true })
<span data-ttu-id="6a974-121">**Sonuçları** hiçbir belge döndürülür.</span><span class="sxs-lookup"><span data-stu-id="6a974-121">**Results** No document will be returned.</span></span> 

## <span data-ttu-id="6a974-122"><a id="examplequery4"></a>Örnek sorgu 4</span><span class="sxs-lookup"><span data-stu-id="6a974-122"><a id="examplequery4"></a>Example query 4</span></span>

<span data-ttu-id="6a974-123">Merhaba sonraki sorgu kayıtlı değil tüm hello aileleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="6a974-123">hello next query returns all hello families which are not registered.</span></span> 

<span data-ttu-id="6a974-124">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="6a974-124">**Query**</span></span>
    
    db.families.find( { "isRegistered" : false })
<span data-ttu-id="6a974-125">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="6a974-125">**Results**</span></span>

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
<span data-ttu-id="6a974-126">}</span><span class="sxs-lookup"><span data-stu-id="6a974-126">}</span></span>

## <span data-ttu-id="6a974-127"><a id="examplequery5"></a>Örnek sorgu 5</span><span class="sxs-lookup"><span data-stu-id="6a974-127"><a id="examplequery5"></a>Example query 5</span></span>

<span data-ttu-id="6a974-128">Tüm kayıtlı değil hello aileleri ve durumudur NY Hello sonraki sorgu döndürür.</span><span class="sxs-lookup"><span data-stu-id="6a974-128">hello next query returns all hello families which are not registered and state is NY.</span></span> 

<span data-ttu-id="6a974-129">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="6a974-129">**Query**</span></span>
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

<span data-ttu-id="6a974-130">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="6a974-130">**Results**</span></span>

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
<span data-ttu-id="6a974-131">}</span><span class="sxs-lookup"><span data-stu-id="6a974-131">}</span></span>


## <span data-ttu-id="6a974-132"><a id="examplequery6"></a>Örnek sorgu 6</span><span class="sxs-lookup"><span data-stu-id="6a974-132"><a id="examplequery6"></a>Example query 6</span></span>

<span data-ttu-id="6a974-133">Merhaba sonraki sorgu alt dereceleri 8 olduğu tüm hello aileleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="6a974-133">hello next query returns all hello families where children grades are 8.</span></span>

<span data-ttu-id="6a974-134">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="6a974-134">**Query**</span></span>
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

<span data-ttu-id="6a974-135">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="6a974-135">**Results**</span></span>

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
<span data-ttu-id="6a974-136">}</span><span class="sxs-lookup"><span data-stu-id="6a974-136">}</span></span>

## <span data-ttu-id="6a974-137"><a id="examplequery7"></a>Örnek sorgu 7</span><span class="sxs-lookup"><span data-stu-id="6a974-137"><a id="examplequery7"></a>Example query 7</span></span>

<span data-ttu-id="6a974-138">Merhaba sonraki sorgu alt dizinin boyutu 3 olduğu tüm hello aileleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="6a974-138">hello next query returns all hello families where size of children array is 3.</span></span>

<span data-ttu-id="6a974-139">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="6a974-139">**Query**</span></span>
  
      db.Family.find( {children: { $size:3} } )

<span data-ttu-id="6a974-140">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="6a974-140">**Results**</span></span>

<span data-ttu-id="6a974-141">2'den fazla alt öğe yok gibi sonuç döndürülür.</span><span class="sxs-lookup"><span data-stu-id="6a974-141">No results will be returned as we do not have more than 2 children.</span></span> <span data-ttu-id="6a974-142">Yalnızca parametresi 2 olduğunda bu sorgu başarılı ve hello tam belge döndürür.</span><span class="sxs-lookup"><span data-stu-id="6a974-142">Only when parameter is 2 this query will succeed and return hello full document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a974-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6a974-143">Next steps</span></span>

<span data-ttu-id="6a974-144">Bu öğreticide, hello aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="6a974-144">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6a974-145">Nasıl öğrenilen tooquery MongoDB kullanma</span><span class="sxs-lookup"><span data-stu-id="6a974-145">Learned how tooquery using MongoDB</span></span> 

<span data-ttu-id="6a974-146">Toohello sonraki öğretici toolearn nasıl şimdi devam toodistribute verilerinizi genel.</span><span class="sxs-lookup"><span data-stu-id="6a974-146">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6a974-147">Verilerinizi genel Dağıt</span><span class="sxs-lookup"><span data-stu-id="6a974-147">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

