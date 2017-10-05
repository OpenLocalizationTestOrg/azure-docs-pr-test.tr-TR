---
title: "Verimli listesi sorguları - Azure Batch tasarlama | Microsoft Docs"
description: "Havuzlar, işler, görevler gibi Batch kaynaklarını hakkında bilgi isterken sorgularınızı filtreleyerek performansını artırmak ve işlem düğümleri."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 031fefeb-248e-4d5a-9bc2-f07e46ddd30d
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 08/02/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a80b207f591bd888d4749287527013c5e554fb6e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-queries-to-list-batch-resources-efficiently"></a><span data-ttu-id="1d9a3-103">Sorguları listesi Batch kaynaklarını verimli bir şekilde oluşturun</span><span class="sxs-lookup"><span data-stu-id="1d9a3-103">Create queries to list Batch resources efficiently</span></span>

<span data-ttu-id="1d9a3-104">Burada, sorgu işler, görevler ve işlem düğümleri ile hizmet tarafından döndürülen veri miktarını azaltarak Azure Batch uygulamanızın performansını artırmak öğreneceksiniz [Batch .NET] [ api_net]kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-104">Here you'll learn how to increase your Azure Batch application's performance by reducing the amount of data that is returned by the service when you query jobs, tasks, and compute nodes with the [Batch .NET][api_net] library.</span></span>

<span data-ttu-id="1d9a3-105">Neredeyse tüm Batch uygulamaları bazı türden bir Batch hizmeti düzenli aralıklarla genellikle sorgular izleme ya da başka işlem yapmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-105">Nearly all Batch applications need to perform some type of monitoring or other operation that queries the Batch service, often at regular intervals.</span></span> <span data-ttu-id="1d9a3-106">Örneğin, bir işin kalan tüm kuyruğa alınmış görevlerin olup olmadığını belirlemek için işteki her görevde veri almalısınız.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-106">For example, to determine whether there are any queued tasks remaining in a job, you must get data on every task in the job.</span></span> <span data-ttu-id="1d9a3-107">Havuzunuzdaki düğümler durumunu belirlemek için verileri havuzdaki her düğümde edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-107">To determine the status of nodes in your pool, you must get data on every node in the pool.</span></span> <span data-ttu-id="1d9a3-108">Bu makale, en verimli şekilde sorgularını yürütmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-108">This article explains how to execute such queries in the most efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="1d9a3-109">Toplu işlem hizmetinin işteki görevler sayım yaygın bir senaryo için özel API desteği sağlar.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-109">The Batch service provides special API support for the common scenario of counting tasks in a job.</span></span> <span data-ttu-id="1d9a3-110">Bir liste sorgusu için kullanmak yerine, çağırabilirsiniz [alma görev sayar] [ rest_get_task_counts] işlemi.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-110">Instead of using a list query for these, you can call the [Get Task Counts][rest_get_task_counts] operation.</span></span> <span data-ttu-id="1d9a3-111">Get görev sayıları kaç görevleri bekleyen, çalışan veya tamamlamak ve kaç tane görevlerin başarılı veya başarısız olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-111">Get Task Counts indicates how many tasks are pending, running or complete, and how many tasks have succeeded or failed.</span></span> <span data-ttu-id="1d9a3-112">Görev Get sayar, liste sorgusu daha etkilidir.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-112">Get Task Counts is more efficient than a list query.</span></span> <span data-ttu-id="1d9a3-113">Daha fazla bilgi için bkz: [saymak durumuna (Önizleme) göre bir iş için görevleri](batch-get-task-counts.md).</span><span class="sxs-lookup"><span data-stu-id="1d9a3-113">For more information, see [Count tasks for a job by state (Preview)](batch-get-task-counts.md).</span></span> 
>
> <span data-ttu-id="1d9a3-114">Görev sayar alma işlemi 2017 06 01.5.1'den önceki toplu işlem hizmeti sürümlerinde kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-114">The Get Task Counts operation is not available in Batch service versions earlier than 2017-06-01.5.1.</span></span> <span data-ttu-id="1d9a3-115">Hizmeti daha eski bir sürümü kullanıyorsanız, bir liste sorgusu işteki görevler yerine saymak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-115">If you are using an older version of the service, then use a list query to count tasks in a job instead.</span></span>
>
> 

## <a name="meet-the-detaillevel"></a><span data-ttu-id="1d9a3-116">DetailLevel karşılayan</span><span class="sxs-lookup"><span data-stu-id="1d9a3-116">Meet the DetailLevel</span></span>
<span data-ttu-id="1d9a3-117">Bir üretimde toplu uygulama varlıkları işler, görevler ve işlem düğümü gibi binlerce sayı.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-117">In a production Batch application, entities like jobs, tasks, and compute nodes can number in the thousands.</span></span> <span data-ttu-id="1d9a3-118">Bu kaynaklar hakkında bilgi istediklerinde, potansiyel olarak büyük miktarda veri "kablo toplu hizmetinden uygulamanıza her sorguda geçmelidir".</span><span class="sxs-lookup"><span data-stu-id="1d9a3-118">When you request information on these resources, a potentially large amount of data must "cross the wire" from the Batch service to your application on each query.</span></span> <span data-ttu-id="1d9a3-119">Öğe sayısı ve türü bir sorgu tarafından döndürülen bilgilerin kısıtlayarak, sorgularınızı hızına ve bu nedenle, uygulamanızın performansını artırabilir.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-119">By limiting the number of items and type of information that is returned by a query, you can increase the speed of your queries, and therefore the performance of your application.</span></span>

<span data-ttu-id="1d9a3-120">Bu [Batch .NET] [ api_net] API kod parçacığını listeleri *her* ile birlikte bir işlemle ilişkili görev *tüm* her görev özellikleri:</span><span class="sxs-lookup"><span data-stu-id="1d9a3-120">This [Batch .NET][api_net] API code snippet lists *every* task that is associated with a job, along with *all* of the properties of each task:</span></span>

```csharp
// Get a collection of all of the tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

<span data-ttu-id="1d9a3-121">Ancak, sorgunuza "ayrıntı düzeyi" uygulayarak çok daha verimli bir liste sorgusu gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-121">You can perform a much more efficient list query, however, by applying a "detail level" to your query.</span></span> <span data-ttu-id="1d9a3-122">Sağlayarak bunu bir [ODATADetailLevel] [ odata] nesnesini [JobOperations.ListTasks] [ net_list_tasks] yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-122">You do this by supplying an [ODATADetailLevel][odata] object to the [JobOperations.ListTasks][net_list_tasks] method.</span></span> <span data-ttu-id="1d9a3-123">Bu kod parçacığında, yalnızca kimliği, komut satırı ve işlem düğümü bilgi tamamlanan görevler özelliklerini döndürür:</span><span class="sxs-lookup"><span data-stu-id="1d9a3-123">This snippet returns only the ID, command line, and compute node information properties of completed tasks:</span></span>

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties to return
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply the ODATADetailLevel to the ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

<span data-ttu-id="1d9a3-124">İşteki görevler binlerce varsa bu örnek senaryoda, ikinci sorgusundan gelen sonuçları genellikle çok döndürülecek ilk hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-124">In this example scenario, if there are thousands of tasks in the job, the results from the second query will typically be returned much quicker than the first.</span></span> <span data-ttu-id="1d9a3-125">Batch .NET API'si öğeleriyle listelediğinizde ODATADetailLevel kullanma hakkında daha fazla bilgi bulunmaktadır [aşağıda](#efficient-querying-in-batch-net).</span><span class="sxs-lookup"><span data-stu-id="1d9a3-125">More information about using ODATADetailLevel when you list items with the Batch .NET API is included [below](#efficient-querying-in-batch-net).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d9a3-126">Yüksek oranda öneririz, *her zaman* ODATADetailLevel nesneye en yüksek verimlilik ve uygulamanızın performansını sağlamak için .NET API listesi çağrılarınızı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-126">We highly recommend that you *always* supply an ODATADetailLevel object to your .NET API list calls to ensure maximum efficiency and performance of your application.</span></span> <span data-ttu-id="1d9a3-127">Ayrıntı düzeyi belirterek, Batch hizmeti yanıt sürelerini alt ağ kullanımı iyileştirirsiniz ve istemci uygulamaları tarafından bellek kullanımını en aza indirmek için yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-127">By specifying a detail level, you can help to lower Batch service response times, improve network utilization, and minimize memory usage by client applications.</span></span>
> 
> 

## <a name="filter-select-and-expand"></a><span data-ttu-id="1d9a3-128">Filtre, seçin ve genişletin</span><span class="sxs-lookup"><span data-stu-id="1d9a3-128">Filter, select, and expand</span></span>
<span data-ttu-id="1d9a3-129">[Batch .NET] [ api_net] ve [Batch REST] [ api_rest] API'leri hem bir listede, döndürülen öğe sayısını düşürmek için olanağı sağlar yanı her biri için döndürülen bilgi tutarını.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-129">The [Batch .NET][api_net] and [Batch REST][api_rest] APIs provide the ability to reduce both the number of items that are returned in a list, as well as the amount of information that is returned for each.</span></span> <span data-ttu-id="1d9a3-130">Belirterek bunu **filtre**, **seçin**, ve **dizeleri genişletin** listesi sorguları gerçekleştirirken.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-130">You do so by specifying **filter**, **select**, and **expand strings** when performing list queries.</span></span>

### <a name="filter"></a><span data-ttu-id="1d9a3-131">Filtre</span><span class="sxs-lookup"><span data-stu-id="1d9a3-131">Filter</span></span>
<span data-ttu-id="1d9a3-132">Filtre dizesi döndürülen öğe sayısını azaltan bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-132">The filter string is an expression that reduces the number of items that are returned.</span></span> <span data-ttu-id="1d9a3-133">Örneğin, bir iş için yalnızca çalışan görevleri listesinde ya da görevleri çalıştırmak hazır olan işlem düğümleri listeleyin.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-133">For example, list only the running tasks for a job, or list only compute nodes that are ready to run tasks.</span></span>

* <span data-ttu-id="1d9a3-134">Filtre dizesi olan bir veya daha fazla ifade, bir özellik adı, işleç ve değer oluşan bir ifade oluşur.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-134">The filter string consists of one or more expressions, with an expression that consists of a property name, operator, and value.</span></span> <span data-ttu-id="1d9a3-135">Her bir özellik için desteklenen işleçleri olarak belirtilebilir özellikler, sorgu, her bir varlık türü özgüdür.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-135">The properties that can be specified are specific to each entity type that you query, as are the operators that are supported for each property.</span></span>
* <span data-ttu-id="1d9a3-136">Mantıksal işleçler kullanarak birden çok ifadeleri birleştirilebilir `and` ve `or`.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-136">Multiple expressions can be combined by using the logical operators `and` and `or`.</span></span>
* <span data-ttu-id="1d9a3-137">Bu örnek filtre dizesi listelerini çalışmasını "işleme yalnızca" görevler: `(state eq 'running') and startswith(id, 'renderTask')`.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-137">This example filter string lists only the running "render" tasks: `(state eq 'running') and startswith(id, 'renderTask')`.</span></span>

### <a name="select"></a><span data-ttu-id="1d9a3-138">Şunu seçin:</span><span class="sxs-lookup"><span data-stu-id="1d9a3-138">Select</span></span>
<span data-ttu-id="1d9a3-139">Select dize her öğe için döndürülen özellik değerlerini sınırlar.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-139">The select string limits the property values that are returned for each item.</span></span> <span data-ttu-id="1d9a3-140">Özellik adlarının bir listesini belirtin ve yalnızca bu özellik değerlerini sorgu sonuçlarında öğeleri için döndürülür.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-140">You specify a list of property names, and only those property values are returned for the items in the query results.</span></span>

* <span data-ttu-id="1d9a3-141">Select dize virgülle ayrılmış listesini özellik adlarının oluşur.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-141">The select string consists of a comma-separated list of property names.</span></span> <span data-ttu-id="1d9a3-142">Sorgulama varlık türü için özelliklerinden herhangi birini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-142">You can specify any of the properties for the entity type you are querying.</span></span>
* <span data-ttu-id="1d9a3-143">Bu örnek Seç dize her görev için yalnızca üç özellik değerlerini döndürülmelidir belirtir: `id, state, stateTransitionTime`.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-143">This example select string specifies that only three property values should be returned for each task: `id, state, stateTransitionTime`.</span></span>

### <a name="expand"></a><span data-ttu-id="1d9a3-144">Genişlet</span><span class="sxs-lookup"><span data-stu-id="1d9a3-144">Expand</span></span>
<span data-ttu-id="1d9a3-145">Genişletilecek dize belirli bilgileri elde etmek için gereken API çağrılarının sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-145">The expand string reduces the number of API calls that are required to obtain certain information.</span></span> <span data-ttu-id="1d9a3-146">Genişletme dizisi kullandığınızda, her öğe hakkında daha fazla bilgi alınabilir tek bir API çağrısı ile.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-146">When you use an expand string, more information about each item can be obtained with a single API call.</span></span> <span data-ttu-id="1d9a3-147">İlk listesinde, her bir öğe için bilgi isteyen varlıkların listesi alma yerine bir genişletme dize tek bir API çağrısı aynı bilgileri almak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-147">Rather than first obtaining the list of entities, then requesting information for each item in the list, you use an expand string to obtain the same information in a single API call.</span></span> <span data-ttu-id="1d9a3-148">Daha az API çağrıları daha iyi performans anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-148">Less API calls means better performance.</span></span>

* <span data-ttu-id="1d9a3-149">Select dizeye benzer, genişletilecek dize, bazı verileri listesi sorgu sonuçlarında dahil edilip edilmeyeceğini denetler.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-149">Similar to the select string, the expand string controls whether certain data is included in list query results.</span></span>
* <span data-ttu-id="1d9a3-150">İşlerini, iş zamanlamalarını, görevler ve havuzları liste kullanıldığında genişletme dize yalnızca desteklenir.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-150">The expand string is only supported when it is used in listing jobs, job schedules, tasks, and pools.</span></span> <span data-ttu-id="1d9a3-151">Şu anda, istatistik bilgileri yalnızca destekler.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-151">Currently, it only supports statistics information.</span></span>
* <span data-ttu-id="1d9a3-152">Tüm özellikleri gereklidir ve select dize belirtilirse, genişletilecek dize *gerekir* istatistik bilgileri almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-152">When all properties are required and no select string is specified, the expand string *must* be used to get statistics information.</span></span> <span data-ttu-id="1d9a3-153">Select dize özelliklerinin bir alt ardından elde etmek için kullanılır, `stats` select dizesinde belirtilen ve Genişletilecek dize belirtilmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-153">If a select string is used to obtain a subset of properties, then `stats` can be specified in the select string, and the expand string does not need to be specified.</span></span>
* <span data-ttu-id="1d9a3-154">Bu örnek genişletin dize istatistik bilgileri, listedeki her bir öğe için döndürülmelidir belirtir: `stats`.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-154">This example expand string specifies that statistics information should be returned for each item in the list: `stats`.</span></span>

> [!NOTE]
> <span data-ttu-id="1d9a3-155">Üç sorgu dizesi türlerinden herhangi birini oluşturulurken (filtre, seçin ve genişletin), özellik adları ve çalışması, REST API öğesi dekiler eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-155">When constructing any of the three query string types (filter, select, and expand), you must ensure that the property names and case match that of their REST API element counterparts.</span></span> <span data-ttu-id="1d9a3-156">Örneğin, .NET ile çalışırken [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) sınıfı belirtmeniz gerekir **durumu** yerine **durumu**, .NET özelliğini olsa bile [ CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span><span class="sxs-lookup"><span data-stu-id="1d9a3-156">For example, when working with the .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) class, you must specify **state** instead of **State**, even though the .NET property is [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span></span> <span data-ttu-id="1d9a3-157">.NET ve REST API'leri arasında özellik eşlemeleri için aşağıdaki tablolara bakın.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-157">See the tables below for property mappings between the .NET and REST APIs.</span></span>
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a><span data-ttu-id="1d9a3-158">Filtre için kuralları seçin ve dizeleri genişletin</span><span class="sxs-lookup"><span data-stu-id="1d9a3-158">Rules for filter, select, and expand strings</span></span>
* <span data-ttu-id="1d9a3-159">Filtre, Özellikler adlarında seçin ve dizeleri genişletin yaptıkları gibi görünmelidir [Batch REST] [ api_rest] kullandığınızda da API-- [Batch .NET] [ api_net]veya diğer toplu Sdk'lardan birini.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-159">Properties names in filter, select, and expand strings should appear as they do in the [Batch REST][api_rest] API--even when you use [Batch .NET][api_net] or one of the other Batch SDKs.</span></span>
* <span data-ttu-id="1d9a3-160">Tüm özellik adları büyük/küçük harfe duyarlıdır, ancak özellik değerleri büyük küçük harfe duyarlı.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-160">All property names are case-sensitive, but property values are case insensitive.</span></span>
* <span data-ttu-id="1d9a3-161">Tarih/saat dizeleri iki biçimlerden birinde olabilir ve ile gelmelidir `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-161">Date/time strings can be one of two formats, and must be preceded with `DateTime`.</span></span>
  
  * <span data-ttu-id="1d9a3-162">W3C DTF biçimi örneği:`creationTime gt DateTime'2011-05-08T08:49:37Z'`</span><span class="sxs-lookup"><span data-stu-id="1d9a3-162">W3C-DTF format example: `creationTime gt DateTime'2011-05-08T08:49:37Z'`</span></span>
  * <span data-ttu-id="1d9a3-163">RFC 1123 biçimi örneği:`creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span><span class="sxs-lookup"><span data-stu-id="1d9a3-163">RFC 1123 format example: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span></span>
* <span data-ttu-id="1d9a3-164">Boole dizelerdir ya da `true` veya `false`.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-164">Boolean strings are either `true` or `false`.</span></span>
* <span data-ttu-id="1d9a3-165">Bir geçersiz özellik ya da operatör belirtilirse, bir `400 (Bad Request)` hata neden olur.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-165">If an invalid property or operator is specified, a `400 (Bad Request)` error will result.</span></span>

## <a name="efficient-querying-in-batch-net"></a><span data-ttu-id="1d9a3-166">Verimli Batch .NET içinde sorgulama</span><span class="sxs-lookup"><span data-stu-id="1d9a3-166">Efficient querying in Batch .NET</span></span>
<span data-ttu-id="1d9a3-167">İçinde [Batch .NET] [ api_net] API, [ODATADetailLevel] [ odata] sınıfı, filtre sağlama için kullanılır, seçin ve listeye dizeleri genişletin işlemler.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-167">Within the [Batch .NET][api_net] API, the [ODATADetailLevel][odata] class is used for supplying filter, select, and expand strings to list operations.</span></span> <span data-ttu-id="1d9a3-168">ODataDetailLevel sınıfı oluşturucuda belirtilen veya doğrudan nesnesinde ayarlanan üç genel dize özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-168">The ODataDetailLevel class has three public string properties that can be specified in the constructor, or set directly on the object.</span></span> <span data-ttu-id="1d9a3-169">Ardından ODataDetailLevel nesnesini parametre olarak çeşitli listeleme işlemleri gibi geçirdiğiniz [ListPools][net_list_pools], [ListJobs][net_list_jobs], ve [ListTasks][net_list_tasks].</span><span class="sxs-lookup"><span data-stu-id="1d9a3-169">You then pass the ODataDetailLevel object as a parameter to the various list operations such as [ListPools][net_list_pools], [ListJobs][net_list_jobs], and [ListTasks][net_list_tasks].</span></span>

* <span data-ttu-id="1d9a3-170">[ODATADetailLevel][odata].[ FilterClause][odata_filter]: döndürülen öğe sayısını sınırla.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-170">[ODATADetailLevel][odata].[FilterClause][odata_filter]: Limit the number of items that are returned.</span></span>
* <span data-ttu-id="1d9a3-171">[ODATADetailLevel][odata].[ SelectClause][odata_select]: hangi özellik değerlerini her bir öğeyle döndürülür belirtin.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-171">[ODATADetailLevel][odata].[SelectClause][odata_select]: Specify which property values are returned with each item.</span></span>
* <span data-ttu-id="1d9a3-172">[ODATADetailLevel][odata].[ ExpandClause][odata_expand]: tek bir API tüm öğeleri için verileri almak yerine ayrı çağrıları her öğe için çağırın.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-172">[ODATADetailLevel][odata].[ExpandClause][odata_expand]: Retrieve data for all items in a single API call instead of separate calls for each item.</span></span>

<span data-ttu-id="1d9a3-173">Aşağıdaki kod parçacığını Batch .NET API'si havuzları belirli bir dizi istatistiklerini Batch hizmeti verimli bir şekilde sorgulamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-173">The following code snippet uses the Batch .NET API to efficiently query the Batch service for the statistics of a specific set of pools.</span></span> <span data-ttu-id="1d9a3-174">Bu senaryoda, test ve Üretim havuzları toplu kullanıcı sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-174">In this scenario, the Batch user has both test and production pools.</span></span> <span data-ttu-id="1d9a3-175">Test havuzu kimlikleri "ile bir test" öneki ve üretim havuzu kimlikleri "ile üretim" öneki.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-175">The test pool IDs are prefixed with "test", and the production pool IDs are prefixed with "prod".</span></span> <span data-ttu-id="1d9a3-176">Parçacığında bulunan *myBatchClient* düzgün başlatılmadı örneğidir [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-176">In the snippet, *myBatchClient* is a properly initialized instance of the [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) class.</span></span>

```csharp
// First we need an ODATADetailLevel instance on which to set the filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want to pull only the "test" pools, so we limit the number of items returned
// by using a FilterClause and specifying that the pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// To further limit the data that crosses the wire, configure the SelectClause to
// limit the properties that are returned on each CloudPool object to only
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify the ExpandClause so that the .NET API pulls the statistics for the
// CloudPools in a single underlying REST API call. Note that we use the pool's
// REST API element name "stats" here as opposed to "Statistics" as it appears in
// the .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing the amount of data that is returned
// by specifying the detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> <span data-ttu-id="1d9a3-177">Örneği [ODATADetailLevel] [ odata] seçin ile yapılandırılmış ve genişletme yan tümceleri de geçirilebilir uygun Get yöntemleri gibi [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), döndürülen veri miktarını sınırlamak için.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-177">An instance of [ODATADetailLevel][odata] that is configured with Select and Expand clauses can also be passed to appropriate Get methods, such as [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), to limit the amount of data that is returned.</span></span>
> 
> 

## <a name="batch-rest-to-net-api-mappings"></a><span data-ttu-id="1d9a3-178">Batch REST .NET API eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="1d9a3-178">Batch REST to .NET API mappings</span></span>
<span data-ttu-id="1d9a3-179">Filtre, özellik adlarını seçin ve dizeleri genişletin *gerekir* REST API'dekiler, hem adı ve durum yansıtır.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-179">Property names in filter, select, and expand strings *must* reflect their REST API counterparts, both in name and case.</span></span> <span data-ttu-id="1d9a3-180">Aşağıdaki tablolarda, .NET ve REST API ortaklarınıza arasındaki eşlemeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-180">The tables below provide mappings between the .NET and REST API counterparts.</span></span>

### <a name="mappings-for-filter-strings"></a><span data-ttu-id="1d9a3-181">Filtre dizeleri eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="1d9a3-181">Mappings for filter strings</span></span>
* <span data-ttu-id="1d9a3-182">**.NET listesi yöntemleri**: Bu sütunda .NET API yöntemlerin her biri kabul eden bir [ODATADetailLevel] [ odata] nesnesini parametre olarak.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-182">**.NET list methods**: Each of the .NET API methods in this column accepts an [ODATADetailLevel][odata] object as a parameter.</span></span>
* <span data-ttu-id="1d9a3-183">**REST listesi istekleri**: Bu sütuna bağlı her REST API sayfa izin işlemleri ve özellikleri belirten bir tablo içeriyor *filtre* dizeleri.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-183">**REST list requests**: Each REST API page linked to in this column contains a table that specifies the properties and operations that are allowed in *filter* strings.</span></span> <span data-ttu-id="1d9a3-184">Oluşturmak, bu özellik adları ve işlemleri için kullanacağı bir [ODATADetailLevel.FilterClause] [ odata_filter] dize.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-184">You will use these property names and operations when you construct an [ODATADetailLevel.FilterClause][odata_filter] string.</span></span>

| <span data-ttu-id="1d9a3-185">.NET listesi yöntemleri</span><span class="sxs-lookup"><span data-stu-id="1d9a3-185">.NET list methods</span></span> | <span data-ttu-id="1d9a3-186">REST listesi istekleri</span><span class="sxs-lookup"><span data-stu-id="1d9a3-186">REST list requests</span></span> |
| --- | --- |
| <span data-ttu-id="1d9a3-187">[CertificateOperations.ListCertificates][net_list_certs]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-187">[CertificateOperations.ListCertificates][net_list_certs]</span></span> |<span data-ttu-id="1d9a3-188">[Bir hesap sertifikaları listesi][rest_list_certs]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-188">[List the certificates in an account][rest_list_certs]</span></span> |
| <span data-ttu-id="1d9a3-189">[CloudTask.ListNodeFiles][net_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-189">[CloudTask.ListNodeFiles][net_list_task_files]</span></span> |<span data-ttu-id="1d9a3-190">[Bir görev ile ilişkili dosyaları listesi][rest_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-190">[List the files associated with a task][rest_list_task_files]</span></span> |
| <span data-ttu-id="1d9a3-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span></span> |<span data-ttu-id="1d9a3-192">[İş hazırlama ve iş sürüm görevleri bir iş için durumu listesi][rest_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-192">[List the status of the job preparation and job release tasks for a job][rest_list_jobprep_status]</span></span> |
| <span data-ttu-id="1d9a3-193">[JobOperations.ListJobs][net_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-193">[JobOperations.ListJobs][net_list_jobs]</span></span> |<span data-ttu-id="1d9a3-194">[Bir hesap işleri listesi][rest_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-194">[List the jobs in an account][rest_list_jobs]</span></span> |
| <span data-ttu-id="1d9a3-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span></span> |<span data-ttu-id="1d9a3-196">[Bir düğümdeki dosya listesi][rest_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-196">[List the files on a node][rest_list_nodefiles]</span></span> |
| <span data-ttu-id="1d9a3-197">[JobOperations.ListTasks][net_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-197">[JobOperations.ListTasks][net_list_tasks]</span></span> |<span data-ttu-id="1d9a3-198">[Bir işi ile ilişkili görevleri listeler][rest_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-198">[List the tasks associated with a job][rest_list_tasks]</span></span> |
| <span data-ttu-id="1d9a3-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span></span> |<span data-ttu-id="1d9a3-200">[Bir hesaptaki iş zamanlamalarını listesi][rest_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-200">[List the job schedules in an account][rest_list_job_schedules]</span></span> |
| <span data-ttu-id="1d9a3-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span></span> |<span data-ttu-id="1d9a3-202">[Bir iş zamanlaması ile ilişkili işleri listesi][rest_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-202">[List the jobs associated with a job schedule][rest_list_schedule_jobs]</span></span> |
| <span data-ttu-id="1d9a3-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span></span> |<span data-ttu-id="1d9a3-204">[Bir havuzdaki işlem düğümleri listesi][rest_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-204">[List the compute nodes in a pool][rest_list_compute_nodes]</span></span> |
| <span data-ttu-id="1d9a3-205">[PoolOperations.ListPools][net_list_pools]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-205">[PoolOperations.ListPools][net_list_pools]</span></span> |<span data-ttu-id="1d9a3-206">[Bir hesap havuzlarını Listele][rest_list_pools]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-206">[List the pools in an account][rest_list_pools]</span></span> |

### <a name="mappings-for-select-strings"></a><span data-ttu-id="1d9a3-207">Select dizeleri eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="1d9a3-207">Mappings for select strings</span></span>
* <span data-ttu-id="1d9a3-208">**Batch .NET türleri**: Batch .NET API'si türleri.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-208">**Batch .NET types**: Batch .NET API types.</span></span>
* <span data-ttu-id="1d9a3-209">**REST API varlıklar**: Bu sütundaki her bir sayfa türü için REST API özellik adları listesinde bir veya daha fazla tablo içeriyor.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-209">**REST API entities**: Each page in this column contains one or more tables that list the REST API property names for the type.</span></span> <span data-ttu-id="1d9a3-210">Bu özellik adları, yapısı oluştururken kullanılan *seçin* dizeleri.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-210">These property names are used when you construct *select* strings.</span></span> <span data-ttu-id="1d9a3-211">Oluşturmak, bu aynı özellik adları için kullanacağı bir [ODATADetailLevel.SelectClause] [ odata_select] dize.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-211">You will use these same property names when you construct an [ODATADetailLevel.SelectClause][odata_select] string.</span></span>

| <span data-ttu-id="1d9a3-212">Batch .NET türleri</span><span class="sxs-lookup"><span data-stu-id="1d9a3-212">Batch .NET types</span></span> | <span data-ttu-id="1d9a3-213">REST API varlıklar</span><span class="sxs-lookup"><span data-stu-id="1d9a3-213">REST API entities</span></span> |
| --- | --- |
| <span data-ttu-id="1d9a3-214">[Sertifika][net_cert]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-214">[Certificate][net_cert]</span></span> |<span data-ttu-id="1d9a3-215">[Bir sertifika hakkında bilgi edinin][rest_get_cert]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-215">[Get information about a certificate][rest_get_cert]</span></span> |
| <span data-ttu-id="1d9a3-216">[CloudJob][net_job]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-216">[CloudJob][net_job]</span></span> |<span data-ttu-id="1d9a3-217">[Bir iş hakkında bilgi edinin][rest_get_job]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-217">[Get information about a job][rest_get_job]</span></span> |
| <span data-ttu-id="1d9a3-218">[CloudJobSchedule][net_schedule]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-218">[CloudJobSchedule][net_schedule]</span></span> |<span data-ttu-id="1d9a3-219">[Bir iş zamanlaması hakkında bilgi edinin][rest_get_schedule]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-219">[Get information about a job schedule][rest_get_schedule]</span></span> |
| <span data-ttu-id="1d9a3-220">[ComputeNode][net_node]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-220">[ComputeNode][net_node]</span></span> |<span data-ttu-id="1d9a3-221">[Bir düğüm hakkında bilgi edinin][rest_get_node]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-221">[Get information about a node][rest_get_node]</span></span> |
| <span data-ttu-id="1d9a3-222">[CloudPool][net_pool]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-222">[CloudPool][net_pool]</span></span> |<span data-ttu-id="1d9a3-223">[Bir havuzu hakkında bilgi edinin][rest_get_pool]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-223">[Get information about a pool][rest_get_pool]</span></span> |
| <span data-ttu-id="1d9a3-224">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-224">[CloudTask][net_task]</span></span> |<span data-ttu-id="1d9a3-225">[Bir görev hakkında bilgi edinin][rest_get_task]</span><span class="sxs-lookup"><span data-stu-id="1d9a3-225">[Get information about a task][rest_get_task]</span></span> |

## <a name="example-construct-a-filter-string"></a><span data-ttu-id="1d9a3-226">Örnek: bir filtre dizesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="1d9a3-226">Example: construct a filter string</span></span>
<span data-ttu-id="1d9a3-227">Bir filtre dizesi oluşturmak zaman [ODATADetailLevel.FilterClause][odata_filter], yukarıdaki tabloda "Eşlemeleri filtre dizeleri için" altında karşılık gelen Bul REST API belgelerine sayfasına bakın gerçekleştirmek istediğiniz işlem listesi.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-227">When you construct a filter string for [ODATADetailLevel.FilterClause][odata_filter], consult the table above under "Mappings for filter strings" to find the REST API documentation page that corresponds to the list operation that you wish to perform.</span></span> <span data-ttu-id="1d9a3-228">Bu sayfada ilk çok satırlı tablodaki filtrelenebilir özellikleri ve bunların desteklenen işleçleri bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-228">You will find the filterable properties and their supported operators in the first multirow table on that page.</span></span> <span data-ttu-id="1d9a3-229">Çıkış kodu sıfır olmayan tüm görevler almak isterseniz, örneğin, bu satırın üzerinde [bir işlemle ilişkili görevleri listesinde] [ rest_list_tasks] geçerli özellik dizesi ve izin verilen işleçleri belirtir:</span><span class="sxs-lookup"><span data-stu-id="1d9a3-229">If you wish to retrieve all tasks whose exit code was nonzero, for example, this row on [List the tasks associated with a job][rest_list_tasks] specifies the applicable property string and allowable operators:</span></span>

| <span data-ttu-id="1d9a3-230">Özellik</span><span class="sxs-lookup"><span data-stu-id="1d9a3-230">Property</span></span> | <span data-ttu-id="1d9a3-231">İzin verilen işlemler</span><span class="sxs-lookup"><span data-stu-id="1d9a3-231">Operations allowed</span></span> | <span data-ttu-id="1d9a3-232">Tür</span><span class="sxs-lookup"><span data-stu-id="1d9a3-232">Type</span></span> |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

<span data-ttu-id="1d9a3-233">Bu nedenle, sıfır olmayan çıkış kodu ile tüm görevleri listeleme için filtre dizesini olacaktır:</span><span class="sxs-lookup"><span data-stu-id="1d9a3-233">Thus, the filter string for listing all tasks with a nonzero exit code would be:</span></span>

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a><span data-ttu-id="1d9a3-234">Örnek: select dizesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="1d9a3-234">Example: construct a select string</span></span>
<span data-ttu-id="1d9a3-235">Oluşturmak için [ODATADetailLevel.SelectClause][odata_select], yukarıdaki tabloda "Select dizeleri eşlemeleri" altında başvurun ve listeleme varlık türüne karşılık gelen REST API sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-235">To construct [ODATADetailLevel.SelectClause][odata_select], consult the table above under "Mappings for select strings" and navigate to the REST API page that corresponds to the type of entity that you are listing.</span></span> <span data-ttu-id="1d9a3-236">Bu sayfada ilk çok satırlı tablodaki seçilebilir özellikleri ve bunların desteklenen işleçleri bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-236">You will find the selectable properties and their supported operators in the first multirow table on that page.</span></span> <span data-ttu-id="1d9a3-237">Yalnızca kimliği ve listedeki her görev için komut satırı almak isterseniz, örneğin, bu satırlar geçerli tabloda üzerinde bulacaksınız [bir görev hakkında bilgi alma][rest_get_task]:</span><span class="sxs-lookup"><span data-stu-id="1d9a3-237">If you wish to retrieve only the ID and command line for each task in a list, for example, you will find these rows in the applicable table on [Get information about a task][rest_get_task]:</span></span>

| <span data-ttu-id="1d9a3-238">Özellik</span><span class="sxs-lookup"><span data-stu-id="1d9a3-238">Property</span></span> | <span data-ttu-id="1d9a3-239">Tür</span><span class="sxs-lookup"><span data-stu-id="1d9a3-239">Type</span></span> | <span data-ttu-id="1d9a3-240">Notlar</span><span class="sxs-lookup"><span data-stu-id="1d9a3-240">Notes</span></span> |
|:--- |:--- |:--- |
| `id` |`String` |`The ID of the task.` |
| `commandLine` |`String` |`The command line of the task.` |

<span data-ttu-id="1d9a3-241">Yalnızca kimliği ve listelenen her görev komut satırıyla dahil etmek için seçim dizesi sonra aşağıdaki gibi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="1d9a3-241">The select string for including only the ID and command line with each listed task would then be:</span></span>

`id, commandLine`

## <a name="code-samples"></a><span data-ttu-id="1d9a3-242">Kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="1d9a3-242">Code samples</span></span>
### <a name="efficient-list-queries-code-sample"></a><span data-ttu-id="1d9a3-243">Verimli listesi sorguları kod örneği</span><span class="sxs-lookup"><span data-stu-id="1d9a3-243">Efficient list queries code sample</span></span>
<span data-ttu-id="1d9a3-244">Kullanıma [EfficientListQueries] [ efficient_query_sample] örnek proje nasıl verimli sorgulama listesini görmek için GitHub üzerindeki bir uygulama performansını etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-244">Check out the [EfficientListQueries][efficient_query_sample] sample project on GitHub to see how efficient list querying can affect performance in an application.</span></span> <span data-ttu-id="1d9a3-245">Bu C# konsol uygulaması oluşturur ve çok sayıda görevler bir projeye ekler.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-245">This C# console application creates and adds a large number of tasks to a job.</span></span> <span data-ttu-id="1d9a3-246">Ardından, birden çok çağrıları yapan [JobOperations.ListTasks] [ net_list_tasks] yöntemi ve geçişleri [ODATADetailLevel] [ odata] nesneleri döndürülecek veri miktarı değiştirmek için farklı özellik değerleri ile yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-246">Then, it makes multiple calls to the [JobOperations.ListTasks][net_list_tasks] method and passes [ODATADetailLevel][odata] objects that are configured with different property values to vary the amount of data to be returned.</span></span> <span data-ttu-id="1d9a3-247">Aşağıdakine benzer bir çıktı üretir:</span><span class="sxs-lookup"><span data-stu-id="1d9a3-247">It produces output similar to the following:</span></span>

```
Adding 5000 tasks to job jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER to query tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER to continue...
```

<span data-ttu-id="1d9a3-248">Geçen kez gösterildiği gibi özellikleri ve döndürülen öğe sayısını sınırlayarak sorgusu yanıt sürelerini önemli ölçüde düşürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-248">As shown in the elapsed times, you can greatly lower query response times by limiting the properties and the number of items that are returned.</span></span> <span data-ttu-id="1d9a3-249">Bu ve diğer örnek projelerinde bulabilirsiniz [azure-batch-samples] [ github_samples] github'daki.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-249">You can find this and other sample projects in the [azure-batch-samples][github_samples] repository on GitHub.</span></span>

### <a name="batchmetrics-library-and-code-sample"></a><span data-ttu-id="1d9a3-250">BatchMetrics kitaplığı ve kod örneği</span><span class="sxs-lookup"><span data-stu-id="1d9a3-250">BatchMetrics library and code sample</span></span>
<span data-ttu-id="1d9a3-251">EfficientListQueries kod örneği yanı sıra yukarıdaki, bulduğunuz [BatchMetrics] [ batch_metrics] proje [azure-batch-samples] [ github_samples]GitHub depo.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-251">In addition to the EfficientListQueries code sample above, you can find the [BatchMetrics][batch_metrics] project in the [azure-batch-samples][github_samples] GitHub repository.</span></span> <span data-ttu-id="1d9a3-252">BatchMetrics örnek proje verimli bir şekilde Batch API'sini kullanarak Azure Batch iş ilerleme durumunu izlemek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-252">The BatchMetrics sample project demonstrates how to efficiently monitor Azure Batch job progress using the Batch API.</span></span>

<span data-ttu-id="1d9a3-253">[BatchMetrics] [ batch_metrics] örnek, kendi projeleri ve çalışma ve kitaplık kullanımı tanıtmak için basit bir komut satırı program dahil edebilirsiniz .NET sınıf kitaplığı proje içerir.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-253">The [BatchMetrics][batch_metrics] sample includes a .NET class library project which you can incorporate into your own projects, and a simple command-line program to exercise and demonstrate the use of the library.</span></span>

<span data-ttu-id="1d9a3-254">Proje içinde örnek uygulama aşağıdaki işlemleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="1d9a3-254">The sample application within the project demonstrates the following operations:</span></span>

1. <span data-ttu-id="1d9a3-255">Özel öznitelikler yalnızca gereksinim duyduğunuz özellikleri indirmek için seçme</span><span class="sxs-lookup"><span data-stu-id="1d9a3-255">Selecting specific attributes in order to download only the properties you need</span></span>
2. <span data-ttu-id="1d9a3-256">Değişiklikler yalnızca son sorgu itibaren indirmek için durum geçiş süreleri filtreleme</span><span class="sxs-lookup"><span data-stu-id="1d9a3-256">Filtering on state transition times in order to download only changes since the last query</span></span>

<span data-ttu-id="1d9a3-257">Örneğin, aşağıdaki yöntemi BatchMetrics Kitaplığı'nda görünür.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-257">For example, the following method appears in the BatchMetrics library.</span></span> <span data-ttu-id="1d9a3-258">Yalnızca belirleyen bir ODATADetailLevel döndürür `id` ve `state` özellikleri için sorgulanır varlıklar elde.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-258">It returns an ODATADetailLevel that specifies that only the `id` and `state` properties should be obtained for the entities that are queried.</span></span> <span data-ttu-id="1d9a3-259">Ayrıca, belirtir, durumu belirtilen bu yana değişti varlıklar `DateTime` parametresi döndürülmesi.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-259">It also specifies that only entities whose state has changed since the specified `DateTime` parameter should be returned.</span></span>

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a><span data-ttu-id="1d9a3-260">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1d9a3-260">Next steps</span></span>
### <a name="parallel-node-tasks"></a><span data-ttu-id="1d9a3-261">Paralel düğüm görevleri</span><span class="sxs-lookup"><span data-stu-id="1d9a3-261">Parallel node tasks</span></span>
<span data-ttu-id="1d9a3-262">[Eşzamanlı düğüm görevleri ile Azure toplu işlem kaynak kullanımını en üst düzeye](batch-parallel-node-tasks.md) başka bir makaleye toplu uygulama performansı ile ilgili.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-262">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) is another article related to Batch application performance.</span></span> <span data-ttu-id="1d9a3-263">İş yüklerinin bazı türleri üzerinde Paralel Görevler yürütülürken yararlanabilir büyük--ancak daha az--işlem düğümlerini.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-263">Some types of workloads can benefit from executing parallel tasks on larger--but fewer--compute nodes.</span></span> <span data-ttu-id="1d9a3-264">Kullanıma [Örnek senaryo](batch-parallel-node-tasks.md#example-scenario) makalede böyle bir senaryo hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-264">Check out the [example scenario](batch-parallel-node-tasks.md#example-scenario) in the article for details on such a scenario.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="1d9a3-265">Toplu işlem Forumu</span><span class="sxs-lookup"><span data-stu-id="1d9a3-265">Batch Forum</span></span>
<span data-ttu-id="1d9a3-266">[Azure toplu işlem Forumu] [ forum] MSDN'de toplu ele almaktadır ve hizmet hakkında sorular sormak için iyi bir yerdir.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-266">The [Azure Batch Forum][forum] on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="1d9a3-267">HEAD üzerinde üzerinden faydalı "Yapışkan" gönderiler için ve Batch çözümlerinizi derleme sırasında çıktıkları anda sorularınızı gönderin.</span><span class="sxs-lookup"><span data-stu-id="1d9a3-267">Head on over for helpful "sticky" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_metrics]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchMetrics
[efficient_query_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/EfficientListQueries
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_samples]: https://github.com/Azure/azure-batch-samples
[odata]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[odata_ctor]: https://msdn.microsoft.com/library/azure/dn866178.aspx
[odata_expand]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.expandclause.aspx
[odata_filter]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.filterclause.aspx
[odata_select]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.selectclause.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[rest_list_certs]: https://msdn.microsoft.com/library/azure/dn820154.aspx
[rest_list_compute_nodes]: https://msdn.microsoft.com/library/azure/dn820159.aspx
[rest_list_job_schedules]: https://msdn.microsoft.com/library/azure/mt282174.aspx
[rest_list_jobprep_status]: https://msdn.microsoft.com/library/azure/mt282170.aspx
[rest_list_jobs]: https://msdn.microsoft.com/library/azure/dn820117.aspx
[rest_list_nodefiles]: https://msdn.microsoft.com/library/azure/dn820151.aspx
[rest_list_pools]: https://msdn.microsoft.com/library/azure/dn820101.aspx
[rest_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/mt282169.aspx
[rest_list_task_files]: https://msdn.microsoft.com/library/azure/dn820142.aspx
[rest_list_tasks]: https://msdn.microsoft.com/library/azure/dn820187.aspx

[rest_get_cert]: https://msdn.microsoft.com/library/azure/dn820176.aspx
[rest_get_job]: https://msdn.microsoft.com/library/azure/dn820106.aspx
[rest_get_node]: https://msdn.microsoft.com/library/azure/dn820168.aspx
[rest_get_pool]: https://msdn.microsoft.com/library/azure/dn820165.aspx
[rest_get_schedule]: https://msdn.microsoft.com/library/azure/mt282171.aspx
[rest_get_task]: https://msdn.microsoft.com/library/azure/dn820133.aspx

[net_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificate.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_schedule]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjobschedule.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx

[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job