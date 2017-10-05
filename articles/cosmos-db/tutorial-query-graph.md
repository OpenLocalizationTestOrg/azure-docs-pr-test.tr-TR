---
title: "Grafik verileri Azure Cosmos veritabanı nasıl? | Microsoft Belgeleri"
description: "Sorgu grafik verileri Azure Cosmos veritabanı hakkında bilgi edinin"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 8bde5c80-581c-4f70-acb4-9578873c92fa
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 81713c72da037f127e81239d214d7a877247dca1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-how-to-query-with-the-graph-api-preview"></a><span data-ttu-id="e4e3d-104">Azure Cosmos DB: grafik API'si (Önizleme) ile nasıl?</span><span class="sxs-lookup"><span data-stu-id="e4e3d-104">Azure Cosmos DB: How to query with the Graph API (preview)?</span></span>

<span data-ttu-id="e4e3d-105">Azure Cosmos DB [grafik API'si](graph-introduction.md) (Önizleme) destekleyen [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) sorgular.</span><span class="sxs-lookup"><span data-stu-id="e4e3d-105">The Azure Cosmos DB [Graph API](graph-introduction.md) (preview) supports [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) queries.</span></span> <span data-ttu-id="e4e3d-106">Bu makalede örnek belgelerdeki ve sorgulardaki başlamanıza yardımcı olmak için sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e4e3d-106">This article provides sample documents and queries to get you started.</span></span> <span data-ttu-id="e4e3d-107">A ayrıntılı başvuru sağlanır Gremlin [Gremlin Destek](gremlin-support.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="e4e3d-107">A detailed Gremlin reference is provided in the [Gremlin support](gremlin-support.md) article.</span></span>

<span data-ttu-id="e4e3d-108">Bu makalede aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="e4e3d-108">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="e4e3d-109">Gremlin verilerle sorgulama</span><span class="sxs-lookup"><span data-stu-id="e4e3d-109">Querying data with Gremlin</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4e3d-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e4e3d-110">Prerequisites</span></span>

<span data-ttu-id="e4e3d-111">Bu sorguları çalışmak bir Azure Cosmos DB hesabınız varsa ve grafik verileri kapsayıcısında sahip.</span><span class="sxs-lookup"><span data-stu-id="e4e3d-111">For these queries to work, you must have an Azure Cosmos DB account and have graph data in the container.</span></span> <span data-ttu-id="e4e3d-112">Bu yok?</span><span class="sxs-lookup"><span data-stu-id="e4e3d-112">Don't have any of those?</span></span> <span data-ttu-id="e4e3d-113">Tamamlamak [5 dakikalık quickstart](create-graph-dotnet.md) veya [Geliştirici öğretici](tutorial-query-graph.md) bir hesap oluşturun ve veritabanınızı doldurmak için.</span><span class="sxs-lookup"><span data-stu-id="e4e3d-113">Complete the [5-minute quickstart](create-graph-dotnet.md) or the [developer tutorial](tutorial-query-graph.md) to create an account and populate your database.</span></span> <span data-ttu-id="e4e3d-114">Kullanarak aşağıdaki sorguları çalıştırabilirsiniz [Azure Cosmos DB .NET grafik Kitaplığı](graph-sdk-dotnet.md), [Gremlin konsol](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), veya sık kullanılan Gremlin sürücünüzü.</span><span class="sxs-lookup"><span data-stu-id="e4e3d-114">You can run the following queries using the [Azure Cosmos DB .NET graph library](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span></span>

## <a name="count-vertices-in-the-graph"></a><span data-ttu-id="e4e3d-115">Grafik tepe sayısı</span><span class="sxs-lookup"><span data-stu-id="e4e3d-115">Count vertices in the graph</span></span>

<span data-ttu-id="e4e3d-116">Aşağıdaki kod parçacığında, grafik tepe sayısı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="e4e3d-116">The following snippet shows how to count the number of vertices in the graph:</span></span>

```
g.V().count()
```

## <a name="filters"></a><span data-ttu-id="e4e3d-117">Filtreler</span><span class="sxs-lookup"><span data-stu-id="e4e3d-117">Filters</span></span>

<span data-ttu-id="e4e3d-118">Gremlin'ın kullanarak filtreler gerçekleştirebilirsiniz `has` ve `hasLabel` adımları ve bunları birleştirmek kullanarak `and`, `or`, ve `not` daha karmaşık filtreler oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="e4e3d-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` to build more complex filters.</span></span> <span data-ttu-id="e4e3d-119">Azure Cosmos DB köşeleri ve derece hızlı sorgular için içindeki tüm özelliklerinin şema belirsiz dizin oluşturma sağlar:</span><span class="sxs-lookup"><span data-stu-id="e4e3d-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span></span>

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a><span data-ttu-id="e4e3d-120">Yansıtma</span><span class="sxs-lookup"><span data-stu-id="e4e3d-120">Projection</span></span>

<span data-ttu-id="e4e3d-121">Belirli özellikleri kullanarak sorgu sonuçlarındaki proje `values` . adım:</span><span class="sxs-lookup"><span data-stu-id="e4e3d-121">You can project certain properties in the query results using the `values` step:</span></span>

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a><span data-ttu-id="e4e3d-122">İlgili kenarları ve köşeleri Bul</span><span class="sxs-lookup"><span data-stu-id="e4e3d-122">Find related edges and vertices</span></span>

<span data-ttu-id="e4e3d-123">Şu ana kadar yalnızca tüm veritabanındaki iş sorgu işleçleri gördük.</span><span class="sxs-lookup"><span data-stu-id="e4e3d-123">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="e4e3d-124">İlgili kenarları ve köşeleri gitmek gerektiğinde grafikleri hızlı ve verimli çapraz geçiş işlemleri için.</span><span class="sxs-lookup"><span data-stu-id="e4e3d-124">Graphs are fast and efficient for traversal operations when you need to navigate to related edges and vertices.</span></span> <span data-ttu-id="e4e3d-125">Şimdi tüm arkadaşların Thomas bulun.</span><span class="sxs-lookup"><span data-stu-id="e4e3d-125">Let's find all friends of Thomas.</span></span> <span data-ttu-id="e4e3d-126">Biz Gremlin'ın kullanarak bunu `outE` tüm bulmak için adım Thomas silip Gremlin'ın kullanarak bu kenarlarından içinde-köşeleri için çapraz geçiş yapan dışarı kenarları `inV` . adım:</span><span class="sxs-lookup"><span data-stu-id="e4e3d-126">We do this by using Gremlin's `outE` step to find all the out-edges from Thomas, then traversing to the in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="e4e3d-127">Tüm Thomas' "arkadaş arkadaş", çağırarak bulmak için iki atlama sonraki sorgu gerçekleştirir `outE` ve `inV` iki kez.</span><span class="sxs-lookup"><span data-stu-id="e4e3d-127">The next query performs two hops to find all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="e4e3d-128">Daha karmaşık sorgular derlemek ve döngü kullanarak gerçekleştirmeden, filtre ifadeleri karıştırma dahil olmak üzere Gremlin kullanan güçlü grafik geçişi mantığı uygulamanıza `loop` adım ve uygulama koşullu Gezinti kullanarak `choose` adım.</span><span class="sxs-lookup"><span data-stu-id="e4e3d-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using the `loop` step, and implementing conditional navigation using the `choose` step.</span></span> <span data-ttu-id="e4e3d-129">İle yapabilecekleriniz hakkında daha fazla bilgi [Gremlin Destek](gremlin-support.md)!</span><span class="sxs-lookup"><span data-stu-id="e4e3d-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4e3d-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e4e3d-130">Next steps</span></span>

<span data-ttu-id="e4e3d-131">Bu öğreticide, aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="e4e3d-131">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e4e3d-132">Grafik kullanarak sorgu öğrendiniz</span><span class="sxs-lookup"><span data-stu-id="e4e3d-132">Learned how to query using Graph</span></span> 

<span data-ttu-id="e4e3d-133">Verilerinizi Genel dağıtma konusunda bilgi almak için sonraki öğretici şimdi devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4e3d-133">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e4e3d-134">Verilerinizi genel Dağıt</span><span class="sxs-lookup"><span data-stu-id="e4e3d-134">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)