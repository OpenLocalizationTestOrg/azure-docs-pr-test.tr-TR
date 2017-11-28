---
title: "SQL Azure Cosmos veritabanı ile aaaHow tooquery? | Microsoft Belgeleri"
description: "SQL Azure Cosmos veritabanı ile DocumentDB verilerle tooquery öğrenin"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: tutorial-develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d3dc51acf92cb78d4f4d9dbac7ec54b1382431cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a><span data-ttu-id="e698d-104">Azure Cosmos DB: Nasıl SQL kullanarak tooquery?</span><span class="sxs-lookup"><span data-stu-id="e698d-104">Azure Cosmos DB: How tooquery using SQL?</span></span>

<span data-ttu-id="e698d-105">Hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) belgeleri SQL kullanarak sorgulama destekler.</span><span class="sxs-lookup"><span data-stu-id="e698d-105">hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="e698d-106">Bu makalede, örnek bir belge ve iki örnek SQL sorguları ve sonuçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="e698d-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="e698d-107">Bu makalede görevleri aşağıdaki hello yer almaktadır:</span><span class="sxs-lookup"><span data-stu-id="e698d-107">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="e698d-108">SQL ile veri sorgulama</span><span class="sxs-lookup"><span data-stu-id="e698d-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="e698d-109">Örnek bir belge</span><span class="sxs-lookup"><span data-stu-id="e698d-109">Sample document</span></span>

<span data-ttu-id="e698d-110">Merhaba SQL sorgularını bu makaledeki örnek bir belge aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="e698d-110">hello SQL queries in this article use hello following sample document.</span></span>

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
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="e698d-111">SQL sorguları yeri çalıştırabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="e698d-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="e698d-112">Hello Veri Gezgini hello hello aracılığıyla Azure portal kullanarak sorguları çalıştırabilirsiniz [REST API ve SDK](documentdb-sdk-dotnet.md)ve hatta hello [Query playground](https://www.documentdb.com/sql/demo), var olan bir örnek veri kümesini temel sorguları çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="e698d-112">You can run queries using hello Data Explorer in hello Azure portal, via hello [REST API and SDKs](documentdb-sdk-dotnet.md), and even hello [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="e698d-113">SQL sorguları hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="e698d-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="e698d-114">SQL sorgusu ve SQL söz dizimi</span><span class="sxs-lookup"><span data-stu-id="e698d-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="e698d-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e698d-115">Prerequisites</span></span>

<span data-ttu-id="e698d-116">Bu öğretici bir Azure Cosmos DB hesap ve koleksiyon olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="e698d-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="e698d-117">Bu yok?</span><span class="sxs-lookup"><span data-stu-id="e698d-117">Don't have any of those?</span></span> <span data-ttu-id="e698d-118">Tam hello [5 dakikalık quickstart](create-mongodb-nodejs.md) veya hello [Geliştirici öğretici](tutorial-develop-mongodb.md) toocreate bir hesap ve koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="e698d-118">Complete hello [5-minute quickstart](create-mongodb-nodejs.md) or hello [developer tutorial](tutorial-develop-mongodb.md) toocreate an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="e698d-119">Örnek sorgu 1</span><span class="sxs-lookup"><span data-stu-id="e698d-119">Example query 1</span></span>

<span data-ttu-id="e698d-120">Merhaba örnek ailesi belge yukarıda verilen, SQL sorgusu aşağıdaki hello belgeleri hello Kimliği alanı eşleştiği döndürür `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="e698d-120">Given hello sample family document above, following SQL query returns hello documents where hello id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="e698d-121">Olduğundan bir `SELECT *` ifadesi, hello sorgu hello çıktısını hello tam JSON belgesi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e698d-121">Since it's a `SELECT *` statement, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="e698d-122">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="e698d-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="e698d-123">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="e698d-123">**Results**</span></span>

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

## <a name="example-query-2"></a><span data-ttu-id="e698d-124">Örnek Sorgu 2</span><span class="sxs-lookup"><span data-stu-id="e698d-124">Example query 2</span></span>

<span data-ttu-id="e698d-125">Merhaba sonraki sorgunun döndürdüğü tüm hello verilen adları alt kimliğine eşleşen hello ailesinde `WakefieldFamily` kendi sınıf tarafından sıralanan.</span><span class="sxs-lookup"><span data-stu-id="e698d-125">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="e698d-126">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="e698d-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="e698d-127">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="e698d-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="e698d-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e698d-128">Next steps</span></span>

<span data-ttu-id="e698d-129">Bu öğreticide, hello aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="e698d-129">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e698d-130">Nasıl öğrenilen SQL kullanarak tooquery</span><span class="sxs-lookup"><span data-stu-id="e698d-130">Learned how tooquery using SQL</span></span>  

<span data-ttu-id="e698d-131">Toohello sonraki öğretici toolearn nasıl şimdi devam toodistribute verilerinizi genel.</span><span class="sxs-lookup"><span data-stu-id="e698d-131">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e698d-132">Verilerinizi genel Dağıt</span><span class="sxs-lookup"><span data-stu-id="e698d-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

