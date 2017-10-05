---
title: "SQL Azure Cosmos veritabanı ile nasıl? | Microsoft Belgeleri"
description: "SQL Azure Cosmos veritabanı ile DocumentDB verilerle sorgu öğrenin"
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
ms.openlocfilehash: a2a562c06c6302b9548e758b4c6754ec13b6001d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-using-sql"></a><span data-ttu-id="65c14-104">Azure Cosmos DB: SQL kullanarak nasıl?</span><span class="sxs-lookup"><span data-stu-id="65c14-104">Azure Cosmos DB: How to query using SQL?</span></span>

<span data-ttu-id="65c14-105">Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) belgeleri SQL kullanarak sorgulama destekler.</span><span class="sxs-lookup"><span data-stu-id="65c14-105">The Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="65c14-106">Bu makalede, örnek bir belge ve iki örnek SQL sorguları ve sonuçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="65c14-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="65c14-107">Bu makalede aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="65c14-107">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="65c14-108">SQL ile veri sorgulama</span><span class="sxs-lookup"><span data-stu-id="65c14-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="65c14-109">Örnek bir belge</span><span class="sxs-lookup"><span data-stu-id="65c14-109">Sample document</span></span>

<span data-ttu-id="65c14-110">Bu makalede SQL sorguları aşağıdaki örnek belge kullanın.</span><span class="sxs-lookup"><span data-stu-id="65c14-110">The SQL queries in this article use the following sample document.</span></span>

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
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="65c14-111">SQL sorguları yeri çalıştırabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="65c14-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="65c14-112">Aracılığıyla Azure portalında Veri Gezgini'ni kullanarak sorguları çalıştırabilirsiniz [REST API ve SDK](documentdb-sdk-dotnet.md)ve hatta [Query playground](https://www.documentdb.com/sql/demo), var olan bir örnek veri kümesini temel sorguları çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="65c14-112">You can run queries using the Data Explorer in the Azure portal, via the [REST API and SDKs](documentdb-sdk-dotnet.md), and even the [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="65c14-113">SQL sorguları hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="65c14-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="65c14-114">SQL sorgusu ve SQL söz dizimi</span><span class="sxs-lookup"><span data-stu-id="65c14-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="65c14-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="65c14-115">Prerequisites</span></span>

<span data-ttu-id="65c14-116">Bu öğretici bir Azure Cosmos DB hesap ve koleksiyon olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="65c14-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="65c14-117">Bu yok?</span><span class="sxs-lookup"><span data-stu-id="65c14-117">Don't have any of those?</span></span> <span data-ttu-id="65c14-118">Tamamlamak [5 dakikalık quickstart](create-mongodb-nodejs.md) veya [Geliştirici öğretici](tutorial-develop-mongodb.md) bir hesap ve koleksiyonu oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="65c14-118">Complete the [5-minute quickstart](create-mongodb-nodejs.md) or the [developer tutorial](tutorial-develop-mongodb.md) to create an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="65c14-119">Örnek sorgu 1</span><span class="sxs-lookup"><span data-stu-id="65c14-119">Example query 1</span></span>

<span data-ttu-id="65c14-120">Yukarıdaki örnek ailesi belge verilen, SQL sorgusu aşağıdaki belgeleri ID alanı eşleştiği döndürür `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="65c14-120">Given the sample family document above, following SQL query returns the documents where the id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="65c14-121">Olduğundan bir `SELECT *` ifadesi, sorgu çıktısı tam JSON belgesi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="65c14-121">Since it's a `SELECT *` statement, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="65c14-122">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="65c14-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="65c14-123">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="65c14-123">**Results**</span></span>

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

## <a name="example-query-2"></a><span data-ttu-id="65c14-124">Örnek Sorgu 2</span><span class="sxs-lookup"><span data-stu-id="65c14-124">Example query 2</span></span>

<span data-ttu-id="65c14-125">Sonraki sorgu kimliğine eşleşen ailesinde alt tüm verilen adlarını döndürür `WakefieldFamily` kendi sınıf tarafından sıralanan.</span><span class="sxs-lookup"><span data-stu-id="65c14-125">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="65c14-126">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="65c14-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="65c14-127">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="65c14-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="65c14-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="65c14-128">Next steps</span></span>

<span data-ttu-id="65c14-129">Bu öğreticide, aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="65c14-129">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="65c14-130">SQL kullanarak sorgulamak öğrendiniz</span><span class="sxs-lookup"><span data-stu-id="65c14-130">Learned how to query using SQL</span></span>  

<span data-ttu-id="65c14-131">Verilerinizi Genel dağıtma konusunda bilgi almak için sonraki öğretici şimdi devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65c14-131">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="65c14-132">Verilerinizi genel Dağıt</span><span class="sxs-lookup"><span data-stu-id="65c14-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

