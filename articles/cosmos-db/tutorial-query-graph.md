---
title: "aaaHow tooquery grafik verileri Azure Cosmos veritabanı? | Microsoft Belgeleri"
description: "Tooquery grafik verileri Azure Cosmos veritabanı öğrenin"
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
ms.openlocfilehash: fdde881edd6c488e2fea51e5c9665e1d736009fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a><span data-ttu-id="0e8b9-104">Azure Cosmos DB: Nasıl tooquery ile Merhaba grafik API'si (Önizleme)?</span><span class="sxs-lookup"><span data-stu-id="0e8b9-104">Azure Cosmos DB: How tooquery with hello Graph API (preview)?</span></span>

<span data-ttu-id="0e8b9-105">Hello Azure Cosmos DB [grafik API'si](graph-introduction.md) (Önizleme) destekleyen [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) sorgular.</span><span class="sxs-lookup"><span data-stu-id="0e8b9-105">hello Azure Cosmos DB [Graph API](graph-introduction.md) (preview) supports [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) queries.</span></span> <span data-ttu-id="0e8b9-106">Bu makalede örnek belgeler sağlar ve başlattığınız tooget sorgular.</span><span class="sxs-lookup"><span data-stu-id="0e8b9-106">This article provides sample documents and queries tooget you started.</span></span> <span data-ttu-id="0e8b9-107">Ayrıntılı Gremlin başvuru hello sağlanan [Gremlin Destek](gremlin-support.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="0e8b9-107">A detailed Gremlin reference is provided in hello [Gremlin support](gremlin-support.md) article.</span></span>

<span data-ttu-id="0e8b9-108">Bu makalede görevleri aşağıdaki hello yer almaktadır:</span><span class="sxs-lookup"><span data-stu-id="0e8b9-108">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="0e8b9-109">Gremlin verilerle sorgulama</span><span class="sxs-lookup"><span data-stu-id="0e8b9-109">Querying data with Gremlin</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e8b9-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0e8b9-110">Prerequisites</span></span>

<span data-ttu-id="0e8b9-111">Bu sorguları toowork için bir Azure Cosmos DB hesabınız varsa ve grafik verileri hello kapsayıcısında sahip.</span><span class="sxs-lookup"><span data-stu-id="0e8b9-111">For these queries toowork, you must have an Azure Cosmos DB account and have graph data in hello container.</span></span> <span data-ttu-id="0e8b9-112">Bu yok?</span><span class="sxs-lookup"><span data-stu-id="0e8b9-112">Don't have any of those?</span></span> <span data-ttu-id="0e8b9-113">Tam hello [5 dakikalık quickstart](create-graph-dotnet.md) veya hello [Geliştirici öğretici](tutorial-query-graph.md) toocreate bir hesap ve veritabanınızı doldurmak.</span><span class="sxs-lookup"><span data-stu-id="0e8b9-113">Complete hello [5-minute quickstart](create-graph-dotnet.md) or hello [developer tutorial](tutorial-query-graph.md) toocreate an account and populate your database.</span></span> <span data-ttu-id="0e8b9-114">Hello kullanarak sorguları aşağıdaki hello çalıştırabilirsiniz [Azure Cosmos DB .NET grafik Kitaplığı](graph-sdk-dotnet.md), [Gremlin konsol](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), veya sık kullanılan Gremlin sürücünüzü.</span><span class="sxs-lookup"><span data-stu-id="0e8b9-114">You can run hello following queries using hello [Azure Cosmos DB .NET graph library](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span></span>

## <a name="count-vertices-in-hello-graph"></a><span data-ttu-id="0e8b9-115">Merhaba grafik tepe sayısı</span><span class="sxs-lookup"><span data-stu-id="0e8b9-115">Count vertices in hello graph</span></span>

<span data-ttu-id="0e8b9-116">Aşağıdaki kod parçacığında hello nasıl toocount hello hello grafik tepe sayısı gösterir:</span><span class="sxs-lookup"><span data-stu-id="0e8b9-116">hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```
g.V().count()
```

## <a name="filters"></a><span data-ttu-id="0e8b9-117">Filtreler</span><span class="sxs-lookup"><span data-stu-id="0e8b9-117">Filters</span></span>

<span data-ttu-id="0e8b9-118">Gremlin'ın kullanarak filtreler gerçekleştirebilirsiniz `has` ve `hasLabel` adımları ve bunları birleştirmek kullanarak `and`, `or`, ve `not` toobuild daha karmaşık filtreler.</span><span class="sxs-lookup"><span data-stu-id="0e8b9-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters.</span></span> <span data-ttu-id="0e8b9-119">Azure Cosmos DB köşeleri ve derece hızlı sorgular için içindeki tüm özelliklerinin şema belirsiz dizin oluşturma sağlar:</span><span class="sxs-lookup"><span data-stu-id="0e8b9-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span></span>

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a><span data-ttu-id="0e8b9-120">Yansıtma</span><span class="sxs-lookup"><span data-stu-id="0e8b9-120">Projection</span></span>

<span data-ttu-id="0e8b9-121">Belirli özellikler hello sorgu sonuçlarındaki hello kullanarak proje `values` . adım:</span><span class="sxs-lookup"><span data-stu-id="0e8b9-121">You can project certain properties in hello query results using hello `values` step:</span></span>

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a><span data-ttu-id="0e8b9-122">İlgili kenarları ve köşeleri Bul</span><span class="sxs-lookup"><span data-stu-id="0e8b9-122">Find related edges and vertices</span></span>

<span data-ttu-id="0e8b9-123">Şu ana kadar yalnızca tüm veritabanındaki iş sorgu işleçleri gördük.</span><span class="sxs-lookup"><span data-stu-id="0e8b9-123">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="0e8b9-124">Toonavigate toorelated kenarları ve köşeleri gerektiğinde grafikleri hızlı ve verimli çapraz geçiş işlemleri için.</span><span class="sxs-lookup"><span data-stu-id="0e8b9-124">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="0e8b9-125">Şimdi tüm arkadaşların Thomas bulun.</span><span class="sxs-lookup"><span data-stu-id="0e8b9-125">Let's find all friends of Thomas.</span></span> <span data-ttu-id="0e8b9-126">Biz Gremlin'ın kullanarak bunu `outE` tüm hello dışarı Thomas kenarları toofind adım sonra içinde köşe için toohello Gremlin'ın kullanarak bu kenarlarından çapraz geçiş yapan `inV` . adım:</span><span class="sxs-lookup"><span data-stu-id="0e8b9-126">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="0e8b9-127">Merhaba sonraki sorgu gerçekleştirir iki atlama toofind tüm "çağırarak Thomas arkadaş arkadaş", `outE` ve `inV` iki kez.</span><span class="sxs-lookup"><span data-stu-id="0e8b9-127">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="0e8b9-128">Daha karmaşık sorgular derlemek ve Gremlin, kullanarak döngü gerçekleştirme ifadeleri hello dahil olmak üzere karıştırma filtre kullanan güçlü grafik geçişi mantığı uygulamanıza `loop` adım ve hello kullanarak uygulama koşullu Gezinti `choose` adım.</span><span class="sxs-lookup"><span data-stu-id="0e8b9-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="0e8b9-129">İle yapabilecekleriniz hakkında daha fazla bilgi [Gremlin Destek](gremlin-support.md)!</span><span class="sxs-lookup"><span data-stu-id="0e8b9-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e8b9-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0e8b9-130">Next steps</span></span>

<span data-ttu-id="0e8b9-131">Bu öğreticide, hello aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="0e8b9-131">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0e8b9-132">Nasıl öğrenilen grafiğini kullanarak tooquery</span><span class="sxs-lookup"><span data-stu-id="0e8b9-132">Learned how tooquery using Graph</span></span> 

<span data-ttu-id="0e8b9-133">Toohello sonraki öğretici toolearn nasıl şimdi devam toodistribute verilerinizi genel.</span><span class="sxs-lookup"><span data-stu-id="0e8b9-133">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0e8b9-134">Verilerinizi genel Dağıt</span><span class="sxs-lookup"><span data-stu-id="0e8b9-134">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)