---
title: "aaaDesign verimli listesi sorguları - Azure Batch | Microsoft Docs"
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
ms.openlocfilehash: b7e554119ec9d0e9e8007ccfb1ca80fe142a5e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-queries-toolist-batch-resources-efficiently"></a><span data-ttu-id="992bf-103">Sorgular toolist Batch kaynaklarını verimli bir şekilde oluşturun</span><span class="sxs-lookup"><span data-stu-id="992bf-103">Create queries toolist Batch resources efficiently</span></span>

<span data-ttu-id="992bf-104">Burada tooincrease hello işleri sorguladığınızda hello hizmet tarafından döndürülen veri miktarını azaltarak Azure Batch uygulamanızın performansını nasıl görevler ve işlem düğümlerini hello ile öğreneceksiniz [Batch .NET] [ api_net] kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="992bf-104">Here you'll learn how tooincrease your Azure Batch application's performance by reducing hello amount of data that is returned by hello service when you query jobs, tasks, and compute nodes with hello [Batch .NET][api_net] library.</span></span>

<span data-ttu-id="992bf-105">Neredeyse tüm Batch uygulamaları tooperform hello Batch hizmeti düzenli aralıklarla genellikle sorgular izleme ya da başka işlem bazı türü gerekir.</span><span class="sxs-lookup"><span data-stu-id="992bf-105">Nearly all Batch applications need tooperform some type of monitoring or other operation that queries hello Batch service, often at regular intervals.</span></span> <span data-ttu-id="992bf-106">Örneğin, toodetermine bir işi kalan tüm kuyruğa alınmış görevlerin olsanız da, hello işteki her görevde veri almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="992bf-106">For example, toodetermine whether there are any queued tasks remaining in a job, you must get data on every task in hello job.</span></span> <span data-ttu-id="992bf-107">havuzunuzdaki düğümler toodetermine hello durumu, hello havuzdaki her düğümde veri almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="992bf-107">toodetermine hello status of nodes in your pool, you must get data on every node in hello pool.</span></span> <span data-ttu-id="992bf-108">Bu makalede, nasıl tooexecute gibi hello sorgular açıklanmaktadır en verimli şekilde.</span><span class="sxs-lookup"><span data-stu-id="992bf-108">This article explains how tooexecute such queries in hello most efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="992bf-109">Merhaba toplu işlem hizmetinin işteki görevler sayım hello yaygın bir senaryo için özel API desteği sağlar.</span><span class="sxs-lookup"><span data-stu-id="992bf-109">hello Batch service provides special API support for hello common scenario of counting tasks in a job.</span></span> <span data-ttu-id="992bf-110">Bir liste sorgusu için kullanmak yerine, hello çağırabilirsiniz [alma görev sayar] [ rest_get_task_counts] işlemi.</span><span class="sxs-lookup"><span data-stu-id="992bf-110">Instead of using a list query for these, you can call hello [Get Task Counts][rest_get_task_counts] operation.</span></span> <span data-ttu-id="992bf-111">Get görev sayıları kaç görevleri bekleyen, çalışan veya tamamlamak ve kaç tane görevlerin başarılı veya başarısız olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="992bf-111">Get Task Counts indicates how many tasks are pending, running or complete, and how many tasks have succeeded or failed.</span></span> <span data-ttu-id="992bf-112">Görev Get sayar, liste sorgusu daha etkilidir.</span><span class="sxs-lookup"><span data-stu-id="992bf-112">Get Task Counts is more efficient than a list query.</span></span> <span data-ttu-id="992bf-113">Daha fazla bilgi için bkz: [saymak durumuna (Önizleme) göre bir iş için görevleri](batch-get-task-counts.md).</span><span class="sxs-lookup"><span data-stu-id="992bf-113">For more information, see [Count tasks for a job by state (Preview)](batch-get-task-counts.md).</span></span> 
>
> <span data-ttu-id="992bf-114">Merhaba görev sayar alma işlemi 2017 06 01.5.1'den önceki toplu işlem hizmeti sürümlerinde kullanılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="992bf-114">hello Get Task Counts operation is not available in Batch service versions earlier than 2017-06-01.5.1.</span></span> <span data-ttu-id="992bf-115">Merhaba hizmeti daha eski bir sürümü kullanıyorsanız, ardından bir liste sorgu toocount görevleri bir işi kullanın.</span><span class="sxs-lookup"><span data-stu-id="992bf-115">If you are using an older version of hello service, then use a list query toocount tasks in a job instead.</span></span>
>
> 

## <a name="meet-hello-detaillevel"></a><span data-ttu-id="992bf-116">Karşılayan hello DetailLevel</span><span class="sxs-lookup"><span data-stu-id="992bf-116">Meet hello DetailLevel</span></span>
<span data-ttu-id="992bf-117">Bir üretim toplu uygulama, işler, görevler ve işlem düğümü gibi varlıkları hello binlerce sayı.</span><span class="sxs-lookup"><span data-stu-id="992bf-117">In a production Batch application, entities like jobs, tasks, and compute nodes can number in hello thousands.</span></span> <span data-ttu-id="992bf-118">Bu kaynaklar hakkında bilgi istediklerinde, potansiyel olarak büyük miktarda veri "Merhaba kablo hello Batch hizmeti tooyour uygulamadan her sorguda geçmelidir".</span><span class="sxs-lookup"><span data-stu-id="992bf-118">When you request information on these resources, a potentially large amount of data must "cross hello wire" from hello Batch service tooyour application on each query.</span></span> <span data-ttu-id="992bf-119">Öğe Hello sayısı ve türü bir sorgu tarafından döndürülen bilgilerin kısıtlayarak, sorgularınızı hello hızını artırmak ve bu nedenle, uygulamanızın performansını hello.</span><span class="sxs-lookup"><span data-stu-id="992bf-119">By limiting hello number of items and type of information that is returned by a query, you can increase hello speed of your queries, and therefore hello performance of your application.</span></span>

<span data-ttu-id="992bf-120">Bu [Batch .NET] [ api_net] API kod parçacığını listeleri *her* ile birlikte bir işlemle ilişkili görev *tüm* her hello özellikleri Görev:</span><span class="sxs-lookup"><span data-stu-id="992bf-120">This [Batch .NET][api_net] API code snippet lists *every* task that is associated with a job, along with *all* of hello properties of each task:</span></span>

```csharp
// Get a collection of all of hello tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

<span data-ttu-id="992bf-121">Ancak, bir "ayrıntı düzeyi" tooyour sorgu uygulayarak çok daha verimli bir liste sorgusu gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="992bf-121">You can perform a much more efficient list query, however, by applying a "detail level" tooyour query.</span></span> <span data-ttu-id="992bf-122">Sağlayarak bunu bir [ODATADetailLevel] [ odata] toohello nesne [JobOperations.ListTasks] [ net_list_tasks] yöntemi.</span><span class="sxs-lookup"><span data-stu-id="992bf-122">You do this by supplying an [ODATADetailLevel][odata] object toohello [JobOperations.ListTasks][net_list_tasks] method.</span></span> <span data-ttu-id="992bf-123">Bu kod parçacığında, yalnızca hello kimliği, komut satırı ve işlem düğümü bilgi tamamlanan görevler özelliklerini döndürür:</span><span class="sxs-lookup"><span data-stu-id="992bf-123">This snippet returns only hello ID, command line, and compute node information properties of completed tasks:</span></span>

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties tooreturn
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply hello ODATADetailLevel toohello ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

<span data-ttu-id="992bf-124">Bu örnek senaryoda hello işteki görevleri binlerce varsa hello ikinci sorgudan hello sonuçlar genellikle olacaktır hello çok hızlı ilk döndürdü.</span><span class="sxs-lookup"><span data-stu-id="992bf-124">In this example scenario, if there are thousands of tasks in hello job, hello results from hello second query will typically be returned much quicker than hello first.</span></span> <span data-ttu-id="992bf-125">Merhaba Batch .NET API'si öğeleriyle listelediğinizde ODATADetailLevel kullanma hakkında daha fazla bilgi bulunmaktadır [aşağıda](#efficient-querying-in-batch-net).</span><span class="sxs-lookup"><span data-stu-id="992bf-125">More information about using ODATADetailLevel when you list items with hello Batch .NET API is included [below](#efficient-querying-in-batch-net).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="992bf-126">Yüksek oranda öneririz, *her zaman* bir ODATADetailLevel nesne tooyour .NET API listesi çağırır tooensure en yüksek verimlilik ve uygulamanızın performansını sağlar.</span><span class="sxs-lookup"><span data-stu-id="992bf-126">We highly recommend that you *always* supply an ODATADetailLevel object tooyour .NET API list calls tooensure maximum efficiency and performance of your application.</span></span> <span data-ttu-id="992bf-127">Ayrıntı düzeyi belirterek, hizmet yanıt sürelerini toplu işlem, ağ kullanımı iyileştirirsiniz ve istemci uygulamaları tarafından bellek kullanımını en aza indirmek toolower yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="992bf-127">By specifying a detail level, you can help toolower Batch service response times, improve network utilization, and minimize memory usage by client applications.</span></span>
> 
> 

## <a name="filter-select-and-expand"></a><span data-ttu-id="992bf-128">Filtre, seçin ve genişletin</span><span class="sxs-lookup"><span data-stu-id="992bf-128">Filter, select, and expand</span></span>
<span data-ttu-id="992bf-129">Merhaba [Batch .NET] [ api_net] ve [Batch REST] [ api_rest] API'leri hem bir listede, döndürülen öğe hello sayısı hello özelliği tooreduce sağlayın aynı zamanda her biri için döndürülen bilgi tutarını hello.</span><span class="sxs-lookup"><span data-stu-id="992bf-129">hello [Batch .NET][api_net] and [Batch REST][api_rest] APIs provide hello ability tooreduce both hello number of items that are returned in a list, as well as hello amount of information that is returned for each.</span></span> <span data-ttu-id="992bf-130">Belirterek bunu **filtre**, **seçin**, ve **dizeleri genişletin** listesi sorguları gerçekleştirirken.</span><span class="sxs-lookup"><span data-stu-id="992bf-130">You do so by specifying **filter**, **select**, and **expand strings** when performing list queries.</span></span>

### <a name="filter"></a><span data-ttu-id="992bf-131">Filtre</span><span class="sxs-lookup"><span data-stu-id="992bf-131">Filter</span></span>
<span data-ttu-id="992bf-132">Merhaba filtre dizesi hello döndürülen öğe sayısını azaltan bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="992bf-132">hello filter string is an expression that reduces hello number of items that are returned.</span></span> <span data-ttu-id="992bf-133">Çalışan görevlerin bir iş ya da hazır toorun görevler listesi tek işlem düğümleri için örneğin, liste yalnızca hello.</span><span class="sxs-lookup"><span data-stu-id="992bf-133">For example, list only hello running tasks for a job, or list only compute nodes that are ready toorun tasks.</span></span>

* <span data-ttu-id="992bf-134">Merhaba filtre dizesi olan bir veya daha fazla ifade, bir özellik adı, işleç ve değer oluşan bir ifade oluşur.</span><span class="sxs-lookup"><span data-stu-id="992bf-134">hello filter string consists of one or more expressions, with an expression that consists of a property name, operator, and value.</span></span> <span data-ttu-id="992bf-135">Her bir özellik için desteklenen hello işleçleri olarak belirtilebilecek Merhaba, sorgu, belirli tooeach varlık türü özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="992bf-135">hello properties that can be specified are specific tooeach entity type that you query, as are hello operators that are supported for each property.</span></span>
* <span data-ttu-id="992bf-136">Merhaba mantıksal işleçler kullanarak birden çok ifadeleri birleştirilebilir `and` ve `or`.</span><span class="sxs-lookup"><span data-stu-id="992bf-136">Multiple expressions can be combined by using hello logical operators `and` and `or`.</span></span>
* <span data-ttu-id="992bf-137">Bu örnek filtre dizesi listelerini görevleri çalıştıran hello "işleme yalnızca": `(state eq 'running') and startswith(id, 'renderTask')`.</span><span class="sxs-lookup"><span data-stu-id="992bf-137">This example filter string lists only hello running "render" tasks: `(state eq 'running') and startswith(id, 'renderTask')`.</span></span>

### <a name="select"></a><span data-ttu-id="992bf-138">Şunu seçin:</span><span class="sxs-lookup"><span data-stu-id="992bf-138">Select</span></span>
<span data-ttu-id="992bf-139">Merhaba select dize her öğe için döndürülen hello özellik değerlerini sınırlar.</span><span class="sxs-lookup"><span data-stu-id="992bf-139">hello select string limits hello property values that are returned for each item.</span></span> <span data-ttu-id="992bf-140">Özellik adlarının bir listesini belirtin ve yalnızca bu özellik değerlerini hello sorgu sonuçlarındaki hello öğeleri için döndürülür.</span><span class="sxs-lookup"><span data-stu-id="992bf-140">You specify a list of property names, and only those property values are returned for hello items in hello query results.</span></span>

* <span data-ttu-id="992bf-141">Merhaba select dize virgülle ayrılmış listesini özellik adlarının oluşur.</span><span class="sxs-lookup"><span data-stu-id="992bf-141">hello select string consists of a comma-separated list of property names.</span></span> <span data-ttu-id="992bf-142">Merhaba varlık türü, sorgulama için hello özelliklerinden herhangi birini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="992bf-142">You can specify any of hello properties for hello entity type you are querying.</span></span>
* <span data-ttu-id="992bf-143">Bu örnek Seç dize her görev için yalnızca üç özellik değerlerini döndürülmelidir belirtir: `id, state, stateTransitionTime`.</span><span class="sxs-lookup"><span data-stu-id="992bf-143">This example select string specifies that only three property values should be returned for each task: `id, state, stateTransitionTime`.</span></span>

### <a name="expand"></a><span data-ttu-id="992bf-144">Genişlet</span><span class="sxs-lookup"><span data-stu-id="992bf-144">Expand</span></span>
<span data-ttu-id="992bf-145">Merhaba genişletin dize belirli bilgileri hello gerekli tooobtain olan API çağrıları azaltır.</span><span class="sxs-lookup"><span data-stu-id="992bf-145">hello expand string reduces hello number of API calls that are required tooobtain certain information.</span></span> <span data-ttu-id="992bf-146">Genişletme dizisi kullandığınızda, her öğe hakkında daha fazla bilgi alınabilir tek bir API çağrısı ile.</span><span class="sxs-lookup"><span data-stu-id="992bf-146">When you use an expand string, more information about each item can be obtained with a single API call.</span></span> <span data-ttu-id="992bf-147">İlk alma hello listesi varlıklar sonra hello listesindeki her bir öğe için bilgi isteyen yerine, genişletilecek dize kullanın tooobtain hello tek bir API çağrısı aynı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="992bf-147">Rather than first obtaining hello list of entities, then requesting information for each item in hello list, you use an expand string tooobtain hello same information in a single API call.</span></span> <span data-ttu-id="992bf-148">Daha az API çağrıları daha iyi performans anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="992bf-148">Less API calls means better performance.</span></span>

* <span data-ttu-id="992bf-149">Benzer toohello select dize, hello genişletin dize denetimleri belirli veri listesi sorgu sonuçlarında dahil olup olmayacağını.</span><span class="sxs-lookup"><span data-stu-id="992bf-149">Similar toohello select string, hello expand string controls whether certain data is included in list query results.</span></span>
* <span data-ttu-id="992bf-150">Merhaba genişletin dize işleri, iş zamanlamalarını, görevler ve havuzları liste kullanıldığında, yalnızca desteklenir.</span><span class="sxs-lookup"><span data-stu-id="992bf-150">hello expand string is only supported when it is used in listing jobs, job schedules, tasks, and pools.</span></span> <span data-ttu-id="992bf-151">Şu anda, istatistik bilgileri yalnızca destekler.</span><span class="sxs-lookup"><span data-stu-id="992bf-151">Currently, it only supports statistics information.</span></span>
* <span data-ttu-id="992bf-152">Tüm özellikleri gereklidir ve belirtilen bir select dize, dize genişletin hello *gerekir* kullanılan tooget istatistik bilgileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="992bf-152">When all properties are required and no select string is specified, hello expand string *must* be used tooget statistics information.</span></span> <span data-ttu-id="992bf-153">Select dize kullanılan tooobtain özelliklerinin bir alt sonra olup olmadığını `stats` hello select dizesinde belirtilen ve hello genişletin dize belirtilen toobe gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="992bf-153">If a select string is used tooobtain a subset of properties, then `stats` can be specified in hello select string, and hello expand string does not need toobe specified.</span></span>
* <span data-ttu-id="992bf-154">Bu örnek genişletin dize istatistik bilgileri hello listesindeki her bir öğe için döndürülmelidir belirtir: `stats`.</span><span class="sxs-lookup"><span data-stu-id="992bf-154">This example expand string specifies that statistics information should be returned for each item in hello list: `stats`.</span></span>

> [!NOTE]
> <span data-ttu-id="992bf-155">Merhaba hiçbirini oluşturulurken üç sorgu dize türleri (filtre, seçin ve genişletin) hello özellik adları ve çalışması, REST API öğesi dekiler eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="992bf-155">When constructing any of hello three query string types (filter, select, and expand), you must ensure that hello property names and case match that of their REST API element counterparts.</span></span> <span data-ttu-id="992bf-156">Örneğin, .NET ile çalışırken hello [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) sınıfı, belirtmelisiniz **durumu** yerine **durumu**, hello .NET özelliği olsa bile [ CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span><span class="sxs-lookup"><span data-stu-id="992bf-156">For example, when working with hello .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) class, you must specify **state** instead of **State**, even though hello .NET property is [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span></span> <span data-ttu-id="992bf-157">Merhaba .NET ve REST API'lerinin arasında özellik eşlemeleri için aşağıdaki Hello tablolara bakın.</span><span class="sxs-lookup"><span data-stu-id="992bf-157">See hello tables below for property mappings between hello .NET and REST APIs.</span></span>
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a><span data-ttu-id="992bf-158">Filtre için kuralları seçin ve dizeleri genişletin</span><span class="sxs-lookup"><span data-stu-id="992bf-158">Rules for filter, select, and expand strings</span></span>
* <span data-ttu-id="992bf-159">Filtre, Özellikler adlarında seçin ve dizeleri genişletin hello yaptıkları gibi görünmelidir [Batch REST] [ api_rest] kullandığınızda da API-- [Batch .NET] [ api_net] veya diğer toplu SDK hello biri.</span><span class="sxs-lookup"><span data-stu-id="992bf-159">Properties names in filter, select, and expand strings should appear as they do in hello [Batch REST][api_rest] API--even when you use [Batch .NET][api_net] or one of hello other Batch SDKs.</span></span>
* <span data-ttu-id="992bf-160">Tüm özellik adları büyük/küçük harfe duyarlıdır, ancak özellik değerleri büyük küçük harfe duyarlı.</span><span class="sxs-lookup"><span data-stu-id="992bf-160">All property names are case-sensitive, but property values are case insensitive.</span></span>
* <span data-ttu-id="992bf-161">Tarih/saat dizeleri iki biçimlerden birinde olabilir ve ile gelmelidir `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="992bf-161">Date/time strings can be one of two formats, and must be preceded with `DateTime`.</span></span>
  
  * <span data-ttu-id="992bf-162">W3C DTF biçimi örneği:`creationTime gt DateTime'2011-05-08T08:49:37Z'`</span><span class="sxs-lookup"><span data-stu-id="992bf-162">W3C-DTF format example: `creationTime gt DateTime'2011-05-08T08:49:37Z'`</span></span>
  * <span data-ttu-id="992bf-163">RFC 1123 biçimi örneği:`creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span><span class="sxs-lookup"><span data-stu-id="992bf-163">RFC 1123 format example: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span></span>
* <span data-ttu-id="992bf-164">Boole dizelerdir ya da `true` veya `false`.</span><span class="sxs-lookup"><span data-stu-id="992bf-164">Boolean strings are either `true` or `false`.</span></span>
* <span data-ttu-id="992bf-165">Bir geçersiz özellik ya da operatör belirtilirse, bir `400 (Bad Request)` hata neden olur.</span><span class="sxs-lookup"><span data-stu-id="992bf-165">If an invalid property or operator is specified, a `400 (Bad Request)` error will result.</span></span>

## <a name="efficient-querying-in-batch-net"></a><span data-ttu-id="992bf-166">Verimli Batch .NET içinde sorgulama</span><span class="sxs-lookup"><span data-stu-id="992bf-166">Efficient querying in Batch .NET</span></span>
<span data-ttu-id="992bf-167">Merhaba içinde [Batch .NET] [ api_net] API, hello [ODATADetailLevel] [ odata] sınıfı, filtre sağlama için kullanılır, seçin ve dizeleri genişletin toolist işlemleri.</span><span class="sxs-lookup"><span data-stu-id="992bf-167">Within hello [Batch .NET][api_net] API, hello [ODATADetailLevel][odata] class is used for supplying filter, select, and expand strings toolist operations.</span></span> <span data-ttu-id="992bf-168">Merhaba ODataDetailLevel sınıfı hello oluşturucuda belirtilen veya doğrudan hello nesnesinde ayarlanan üç genel dize özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="992bf-168">hello ODataDetailLevel class has three public string properties that can be specified in hello constructor, or set directly on hello object.</span></span> <span data-ttu-id="992bf-169">Ardından hello ODataDetailLevel nesnesi parametresi toohello çeşitli listeleme işlemleri gibi geçirdiğiniz [ListPools][net_list_pools], [ListJobs][net_list_jobs], ve [ListTasks][net_list_tasks].</span><span class="sxs-lookup"><span data-stu-id="992bf-169">You then pass hello ODataDetailLevel object as a parameter toohello various list operations such as [ListPools][net_list_pools], [ListJobs][net_list_jobs], and [ListTasks][net_list_tasks].</span></span>

* <span data-ttu-id="992bf-170">[ODATADetailLevel][odata].[ FilterClause][odata_filter]: hello döndürülen öğe sayısını sınırla.</span><span class="sxs-lookup"><span data-stu-id="992bf-170">[ODATADetailLevel][odata].[FilterClause][odata_filter]: Limit hello number of items that are returned.</span></span>
* <span data-ttu-id="992bf-171">[ODATADetailLevel][odata].[ SelectClause][odata_select]: hangi özellik değerlerini her bir öğeyle döndürülür belirtin.</span><span class="sxs-lookup"><span data-stu-id="992bf-171">[ODATADetailLevel][odata].[SelectClause][odata_select]: Specify which property values are returned with each item.</span></span>
* <span data-ttu-id="992bf-172">[ODATADetailLevel][odata].[ ExpandClause][odata_expand]: tek bir API tüm öğeleri için verileri almak yerine ayrı çağrıları her öğe için çağırın.</span><span class="sxs-lookup"><span data-stu-id="992bf-172">[ODATADetailLevel][odata].[ExpandClause][odata_expand]: Retrieve data for all items in a single API call instead of separate calls for each item.</span></span>

<span data-ttu-id="992bf-173">Merhaba aşağıdaki kod parçacığını hello Batch .NET API'si tooefficiently sorgu hello Batch hizmeti havuzları belirli bir dizi hello istatistiklerini için kullanır.</span><span class="sxs-lookup"><span data-stu-id="992bf-173">hello following code snippet uses hello Batch .NET API tooefficiently query hello Batch service for hello statistics of a specific set of pools.</span></span> <span data-ttu-id="992bf-174">Bu senaryoda, test ve Üretim havuzları hello toplu kullanıcı sahiptir.</span><span class="sxs-lookup"><span data-stu-id="992bf-174">In this scenario, hello Batch user has both test and production pools.</span></span> <span data-ttu-id="992bf-175">Merhaba test havuzu kimlikleri "ile bir test" öneki ve hello üretim havuzu kimlikleri "ile üretim" öneki.</span><span class="sxs-lookup"><span data-stu-id="992bf-175">hello test pool IDs are prefixed with "test", and hello production pool IDs are prefixed with "prod".</span></span> <span data-ttu-id="992bf-176">Merhaba parçacığında bulunan *myBatchClient* hello düzgün başlatılmadı örneğidir [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="992bf-176">In hello snippet, *myBatchClient* is a properly initialized instance of hello [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) class.</span></span>

```csharp
// First we need an ODATADetailLevel instance on which tooset hello filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want toopull only hello "test" pools, so we limit hello number of items returned
// by using a FilterClause and specifying that hello pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// toofurther limit hello data that crosses hello wire, configure hello SelectClause to
// limit hello properties that are returned on each CloudPool object tooonly
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify hello ExpandClause so that hello .NET API pulls hello statistics for the
// CloudPools in a single underlying REST API call. Note that we use hello pool's
// REST API element name "stats" here as opposed too"Statistics" as it appears in
// hello .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing hello amount of data that is returned
// by specifying hello detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> <span data-ttu-id="992bf-177">Örneği [ODATADetailLevel] [ odata] seçin ile yapılandırılmış ve genişletme yan tümceleri de geçirilebilir tooappropriate Get yöntemleri gibi [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx) , toolimit hello döndürülen veri miktarı.</span><span class="sxs-lookup"><span data-stu-id="992bf-177">An instance of [ODATADetailLevel][odata] that is configured with Select and Expand clauses can also be passed tooappropriate Get methods, such as [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), toolimit hello amount of data that is returned.</span></span>
> 
> 

## <a name="batch-rest-toonet-api-mappings"></a><span data-ttu-id="992bf-178">Toplu işlem REST too.NET API eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="992bf-178">Batch REST too.NET API mappings</span></span>
<span data-ttu-id="992bf-179">Filtre, özellik adlarını seçin ve dizeleri genişletin *gerekir* REST API'dekiler, hem adı ve durum yansıtır.</span><span class="sxs-lookup"><span data-stu-id="992bf-179">Property names in filter, select, and expand strings *must* reflect their REST API counterparts, both in name and case.</span></span> <span data-ttu-id="992bf-180">Merhaba tablolar aşağıdaki hello .NET ve REST API ortaklarınıza arasındaki eşlemeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="992bf-180">hello tables below provide mappings between hello .NET and REST API counterparts.</span></span>

### <a name="mappings-for-filter-strings"></a><span data-ttu-id="992bf-181">Filtre dizeleri eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="992bf-181">Mappings for filter strings</span></span>
* <span data-ttu-id="992bf-182">**.NET listesi yöntemleri**: Bu sütunda hello .NET API yöntemlerin her biri kabul eden bir [ODATADetailLevel] [ odata] nesnesini parametre olarak.</span><span class="sxs-lookup"><span data-stu-id="992bf-182">**.NET list methods**: Each of hello .NET API methods in this column accepts an [ODATADetailLevel][odata] object as a parameter.</span></span>
* <span data-ttu-id="992bf-183">**REST listesi istekleri**: her REST API sayfasında izin bu sütunu içeren hello özelliklerini ve işlemlerini belirten bir tablo bağlantılı tooin *filtre* dizeleri.</span><span class="sxs-lookup"><span data-stu-id="992bf-183">**REST list requests**: Each REST API page linked tooin this column contains a table that specifies hello properties and operations that are allowed in *filter* strings.</span></span> <span data-ttu-id="992bf-184">Oluşturmak, bu özellik adları ve işlemleri için kullanacağı bir [ODATADetailLevel.FilterClause] [ odata_filter] dize.</span><span class="sxs-lookup"><span data-stu-id="992bf-184">You will use these property names and operations when you construct an [ODATADetailLevel.FilterClause][odata_filter] string.</span></span>

| <span data-ttu-id="992bf-185">.NET listesi yöntemleri</span><span class="sxs-lookup"><span data-stu-id="992bf-185">.NET list methods</span></span> | <span data-ttu-id="992bf-186">REST listesi istekleri</span><span class="sxs-lookup"><span data-stu-id="992bf-186">REST list requests</span></span> |
| --- | --- |
| <span data-ttu-id="992bf-187">[CertificateOperations.ListCertificates][net_list_certs]</span><span class="sxs-lookup"><span data-stu-id="992bf-187">[CertificateOperations.ListCertificates][net_list_certs]</span></span> |<span data-ttu-id="992bf-188">[Bir hesap hello sertifikalarını listele][rest_list_certs]</span><span class="sxs-lookup"><span data-stu-id="992bf-188">[List hello certificates in an account][rest_list_certs]</span></span> |
| <span data-ttu-id="992bf-189">[CloudTask.ListNodeFiles][net_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="992bf-189">[CloudTask.ListNodeFiles][net_list_task_files]</span></span> |<span data-ttu-id="992bf-190">[Bir görev ile ilişkili hello dosyaları listeleme][rest_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="992bf-190">[List hello files associated with a task][rest_list_task_files]</span></span> |
| <span data-ttu-id="992bf-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="992bf-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span></span> |<span data-ttu-id="992bf-192">[Merhaba iş hazırlama ve iş sürüm görevleri bir iş için Hello durumu listesi][rest_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="992bf-192">[List hello status of hello job preparation and job release tasks for a job][rest_list_jobprep_status]</span></span> |
| <span data-ttu-id="992bf-193">[JobOperations.ListJobs][net_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="992bf-193">[JobOperations.ListJobs][net_list_jobs]</span></span> |<span data-ttu-id="992bf-194">[Bir hesap listesi hello işleri][rest_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="992bf-194">[List hello jobs in an account][rest_list_jobs]</span></span> |
| <span data-ttu-id="992bf-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="992bf-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span></span> |<span data-ttu-id="992bf-196">[Bir düğümde hello dosyaları listeleme][rest_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="992bf-196">[List hello files on a node][rest_list_nodefiles]</span></span> |
| <span data-ttu-id="992bf-197">[JobOperations.ListTasks][net_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="992bf-197">[JobOperations.ListTasks][net_list_tasks]</span></span> |<span data-ttu-id="992bf-198">[Bir işle ilişkili listesi hello görevleri][rest_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="992bf-198">[List hello tasks associated with a job][rest_list_tasks]</span></span> |
| <span data-ttu-id="992bf-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="992bf-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span></span> |<span data-ttu-id="992bf-200">[Bir hesap listesi hello iş zamanlamaları][rest_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="992bf-200">[List hello job schedules in an account][rest_list_job_schedules]</span></span> |
| <span data-ttu-id="992bf-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="992bf-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span></span> |<span data-ttu-id="992bf-202">[Bir iş zamanlaması ile ilişkili listesi hello işleri][rest_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="992bf-202">[List hello jobs associated with a job schedule][rest_list_schedule_jobs]</span></span> |
| <span data-ttu-id="992bf-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="992bf-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span></span> |<span data-ttu-id="992bf-204">[Liste hello işlem düğümleri havuzunda][rest_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="992bf-204">[List hello compute nodes in a pool][rest_list_compute_nodes]</span></span> |
| <span data-ttu-id="992bf-205">[PoolOperations.ListPools][net_list_pools]</span><span class="sxs-lookup"><span data-stu-id="992bf-205">[PoolOperations.ListPools][net_list_pools]</span></span> |<span data-ttu-id="992bf-206">[Bir hesap listesi hello havuzları][rest_list_pools]</span><span class="sxs-lookup"><span data-stu-id="992bf-206">[List hello pools in an account][rest_list_pools]</span></span> |

### <a name="mappings-for-select-strings"></a><span data-ttu-id="992bf-207">Select dizeleri eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="992bf-207">Mappings for select strings</span></span>
* <span data-ttu-id="992bf-208">**Batch .NET türleri**: Batch .NET API'si türleri.</span><span class="sxs-lookup"><span data-stu-id="992bf-208">**Batch .NET types**: Batch .NET API types.</span></span>
* <span data-ttu-id="992bf-209">**REST API varlıklar**: hello REST API özellik adları hello türünün listesinde bir veya daha fazla tablo bu sütundaki her bir sayfa içerir.</span><span class="sxs-lookup"><span data-stu-id="992bf-209">**REST API entities**: Each page in this column contains one or more tables that list hello REST API property names for hello type.</span></span> <span data-ttu-id="992bf-210">Bu özellik adları, yapısı oluştururken kullanılan *seçin* dizeleri.</span><span class="sxs-lookup"><span data-stu-id="992bf-210">These property names are used when you construct *select* strings.</span></span> <span data-ttu-id="992bf-211">Oluşturmak, bu aynı özellik adları için kullanacağı bir [ODATADetailLevel.SelectClause] [ odata_select] dize.</span><span class="sxs-lookup"><span data-stu-id="992bf-211">You will use these same property names when you construct an [ODATADetailLevel.SelectClause][odata_select] string.</span></span>

| <span data-ttu-id="992bf-212">Batch .NET türleri</span><span class="sxs-lookup"><span data-stu-id="992bf-212">Batch .NET types</span></span> | <span data-ttu-id="992bf-213">REST API varlıklar</span><span class="sxs-lookup"><span data-stu-id="992bf-213">REST API entities</span></span> |
| --- | --- |
| <span data-ttu-id="992bf-214">[Sertifika][net_cert]</span><span class="sxs-lookup"><span data-stu-id="992bf-214">[Certificate][net_cert]</span></span> |<span data-ttu-id="992bf-215">[Bir sertifika hakkında bilgi edinin][rest_get_cert]</span><span class="sxs-lookup"><span data-stu-id="992bf-215">[Get information about a certificate][rest_get_cert]</span></span> |
| <span data-ttu-id="992bf-216">[CloudJob][net_job]</span><span class="sxs-lookup"><span data-stu-id="992bf-216">[CloudJob][net_job]</span></span> |<span data-ttu-id="992bf-217">[Bir iş hakkında bilgi edinin][rest_get_job]</span><span class="sxs-lookup"><span data-stu-id="992bf-217">[Get information about a job][rest_get_job]</span></span> |
| <span data-ttu-id="992bf-218">[CloudJobSchedule][net_schedule]</span><span class="sxs-lookup"><span data-stu-id="992bf-218">[CloudJobSchedule][net_schedule]</span></span> |<span data-ttu-id="992bf-219">[Bir iş zamanlaması hakkında bilgi edinin][rest_get_schedule]</span><span class="sxs-lookup"><span data-stu-id="992bf-219">[Get information about a job schedule][rest_get_schedule]</span></span> |
| <span data-ttu-id="992bf-220">[ComputeNode][net_node]</span><span class="sxs-lookup"><span data-stu-id="992bf-220">[ComputeNode][net_node]</span></span> |<span data-ttu-id="992bf-221">[Bir düğüm hakkında bilgi edinin][rest_get_node]</span><span class="sxs-lookup"><span data-stu-id="992bf-221">[Get information about a node][rest_get_node]</span></span> |
| <span data-ttu-id="992bf-222">[CloudPool][net_pool]</span><span class="sxs-lookup"><span data-stu-id="992bf-222">[CloudPool][net_pool]</span></span> |<span data-ttu-id="992bf-223">[Bir havuzu hakkında bilgi edinin][rest_get_pool]</span><span class="sxs-lookup"><span data-stu-id="992bf-223">[Get information about a pool][rest_get_pool]</span></span> |
| <span data-ttu-id="992bf-224">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="992bf-224">[CloudTask][net_task]</span></span> |<span data-ttu-id="992bf-225">[Bir görev hakkında bilgi edinin][rest_get_task]</span><span class="sxs-lookup"><span data-stu-id="992bf-225">[Get information about a task][rest_get_task]</span></span> |

## <a name="example-construct-a-filter-string"></a><span data-ttu-id="992bf-226">Örnek: bir filtre dizesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="992bf-226">Example: construct a filter string</span></span>
<span data-ttu-id="992bf-227">Bir filtre dizesi oluşturmak zaman [ODATADetailLevel.FilterClause][odata_filter], karşılık gelen "Eşlemeleri filtre dizeleri için" toofind hello REST API belge sayfasının altında Merhaba tablonun üzerinde başvurun toohello liste işlemi tooperform istiyor.</span><span class="sxs-lookup"><span data-stu-id="992bf-227">When you construct a filter string for [ODATADetailLevel.FilterClause][odata_filter], consult hello table above under "Mappings for filter strings" toofind hello REST API documentation page that corresponds toohello list operation that you wish tooperform.</span></span> <span data-ttu-id="992bf-228">Merhaba ilk tablodaki çok satırlı o sayfadaki hello filtrelenebilir özellikleri ve bunların desteklenen işleçleri bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="992bf-228">You will find hello filterable properties and their supported operators in hello first multirow table on that page.</span></span> <span data-ttu-id="992bf-229">Çıkış kodu sıfır olmayan tüm görevler tooretrieve isterseniz, örneğin, bu satırın üzerinde [listesinde bir işlemle ilişkili hello görevleri] [ rest_list_tasks] hello geçerli özellik dizesi ve izin verilen işleçleri belirtir:</span><span class="sxs-lookup"><span data-stu-id="992bf-229">If you wish tooretrieve all tasks whose exit code was nonzero, for example, this row on [List hello tasks associated with a job][rest_list_tasks] specifies hello applicable property string and allowable operators:</span></span>

| <span data-ttu-id="992bf-230">Özellik</span><span class="sxs-lookup"><span data-stu-id="992bf-230">Property</span></span> | <span data-ttu-id="992bf-231">İzin verilen işlemler</span><span class="sxs-lookup"><span data-stu-id="992bf-231">Operations allowed</span></span> | <span data-ttu-id="992bf-232">Tür</span><span class="sxs-lookup"><span data-stu-id="992bf-232">Type</span></span> |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

<span data-ttu-id="992bf-233">Bu nedenle, sıfır olmayan çıkış kodu ile tüm görevleri listeleme için filtre dizesini hello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="992bf-233">Thus, hello filter string for listing all tasks with a nonzero exit code would be:</span></span>

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a><span data-ttu-id="992bf-234">Örnek: select dizesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="992bf-234">Example: construct a select string</span></span>
<span data-ttu-id="992bf-235">tooconstruct [ODATADetailLevel.SelectClause][odata_select], "Select dizeleri eşlemeleri" altında Merhaba tablonun üzerinde başvurun ve karşılık gelen varlık toohello türü toohello REST API sayfasına gidin, listeliyorsanız.</span><span class="sxs-lookup"><span data-stu-id="992bf-235">tooconstruct [ODATADetailLevel.SelectClause][odata_select], consult hello table above under "Mappings for select strings" and navigate toohello REST API page that corresponds toohello type of entity that you are listing.</span></span> <span data-ttu-id="992bf-236">Merhaba ilk tablodaki çok satırlı o sayfadaki hello seçilebilir özellikleri ve bunların desteklenen işleçleri bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="992bf-236">You will find hello selectable properties and their supported operators in hello first multirow table on that page.</span></span> <span data-ttu-id="992bf-237">Bir listede tooretrieve yalnızca hello kimliği ve her görev için komut satırı isterseniz, örneğin, bu satırı hello geçerli tabloda üzerinde bulacaksınız [bir görev hakkında bilgi alma][rest_get_task]:</span><span class="sxs-lookup"><span data-stu-id="992bf-237">If you wish tooretrieve only hello ID and command line for each task in a list, for example, you will find these rows in hello applicable table on [Get information about a task][rest_get_task]:</span></span>

| <span data-ttu-id="992bf-238">Özellik</span><span class="sxs-lookup"><span data-stu-id="992bf-238">Property</span></span> | <span data-ttu-id="992bf-239">Tür</span><span class="sxs-lookup"><span data-stu-id="992bf-239">Type</span></span> | <span data-ttu-id="992bf-240">Notlar</span><span class="sxs-lookup"><span data-stu-id="992bf-240">Notes</span></span> |
|:--- |:--- |:--- |
| `id` |`String` |`hello ID of hello task.` |
| `commandLine` |`String` |`hello command line of hello task.` |

<span data-ttu-id="992bf-241">yalnızca hello kimliği ve listelenen her görev komut satırıyla dahil etmek için hello select dizesi sonra aşağıdaki gibi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="992bf-241">hello select string for including only hello ID and command line with each listed task would then be:</span></span>

`id, commandLine`

## <a name="code-samples"></a><span data-ttu-id="992bf-242">Kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="992bf-242">Code samples</span></span>
### <a name="efficient-list-queries-code-sample"></a><span data-ttu-id="992bf-243">Verimli listesi sorguları kod örneği</span><span class="sxs-lookup"><span data-stu-id="992bf-243">Efficient list queries code sample</span></span>
<span data-ttu-id="992bf-244">Merhaba denetleyin [EfficientListQueries] [ efficient_query_sample] GitHub toosee nasıl verimli üzerinde örnek proje listesi sorgulama uygulama performansını etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="992bf-244">Check out hello [EfficientListQueries][efficient_query_sample] sample project on GitHub toosee how efficient list querying can affect performance in an application.</span></span> <span data-ttu-id="992bf-245">Bu C# konsol uygulaması oluşturur ve çok sayıda görevleri tooa iş ekler.</span><span class="sxs-lookup"><span data-stu-id="992bf-245">This C# console application creates and adds a large number of tasks tooa job.</span></span> <span data-ttu-id="992bf-246">Sonra birden çok çağrıları toohello yapar [JobOperations.ListTasks] [ net_list_tasks] yöntemi ve geçişleri [ODATADetailLevel] [ odata] nesneleri farklı özellik değerleri toovary hello miktarını döndürülen veri toobe ile yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="992bf-246">Then, it makes multiple calls toohello [JobOperations.ListTasks][net_list_tasks] method and passes [ODATADetailLevel][odata] objects that are configured with different property values toovary hello amount of data toobe returned.</span></span> <span data-ttu-id="992bf-247">Toohello aşağıdaki benzer bir çıktı üretir:</span><span class="sxs-lookup"><span data-stu-id="992bf-247">It produces output similar toohello following:</span></span>

```
Adding 5000 tasks toojob jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER tooquery tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER toocontinue...
```

<span data-ttu-id="992bf-248">Merhaba geçen kez gösterildiği gibi hello özellikleri ve hello döndürülen öğe sayısını sınırlayarak sorgusu yanıt sürelerini önemli ölçüde düşürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="992bf-248">As shown in hello elapsed times, you can greatly lower query response times by limiting hello properties and hello number of items that are returned.</span></span> <span data-ttu-id="992bf-249">Bu ve diğer örnek projelerine hello bulabilirsiniz [azure-batch-samples] [ github_samples] github'daki.</span><span class="sxs-lookup"><span data-stu-id="992bf-249">You can find this and other sample projects in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span>

### <a name="batchmetrics-library-and-code-sample"></a><span data-ttu-id="992bf-250">BatchMetrics kitaplığı ve kod örneği</span><span class="sxs-lookup"><span data-stu-id="992bf-250">BatchMetrics library and code sample</span></span>
<span data-ttu-id="992bf-251">Ayrıca toohello EfficientListQueries kod örneği yukarıdaki, hello bulabileceğiniz [BatchMetrics] [ batch_metrics] hello bir projede [azure-batch-samples] [ github_samples] GitHub depo.</span><span class="sxs-lookup"><span data-stu-id="992bf-251">In addition toohello EfficientListQueries code sample above, you can find hello [BatchMetrics][batch_metrics] project in hello [azure-batch-samples][github_samples] GitHub repository.</span></span> <span data-ttu-id="992bf-252">Merhaba BatchMetrics örnek proje nasıl tooefficiently izlemek hello Batch API'sini kullanarak Azure Batch iş ilerleme durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="992bf-252">hello BatchMetrics sample project demonstrates how tooefficiently monitor Azure Batch job progress using hello Batch API.</span></span>

<span data-ttu-id="992bf-253">Merhaba [BatchMetrics] [ batch_metrics] örnek içeren, kendi projeleri ve basit bir komut satırı dahil edebilirsiniz .NET sınıf kitaplığı proje program tooexercise ve hello hello kullanımını gösterir Kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="992bf-253">hello [BatchMetrics][batch_metrics] sample includes a .NET class library project which you can incorporate into your own projects, and a simple command-line program tooexercise and demonstrate hello use of hello library.</span></span>

<span data-ttu-id="992bf-254">Merhaba örnek uygulaması hello proje içindeki operations aşağıdaki hello gösterir:</span><span class="sxs-lookup"><span data-stu-id="992bf-254">hello sample application within hello project demonstrates hello following operations:</span></span>

1. <span data-ttu-id="992bf-255">Özel öznitelikler sipariş toodownload yalnızca hello özelliklerinde seçerek gerekir</span><span class="sxs-lookup"><span data-stu-id="992bf-255">Selecting specific attributes in order toodownload only hello properties you need</span></span>
2. <span data-ttu-id="992bf-256">Durum geçişi kez sipariş toodownload süzme yalnızca bu yana hello son sorgu değiştirir</span><span class="sxs-lookup"><span data-stu-id="992bf-256">Filtering on state transition times in order toodownload only changes since hello last query</span></span>

<span data-ttu-id="992bf-257">Örneğin, yöntem aşağıdaki hello hello BatchMetrics kitaplığı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="992bf-257">For example, hello following method appears in hello BatchMetrics library.</span></span> <span data-ttu-id="992bf-258">Bu yalnızca hello belirten bir ODATADetailLevel döndürür `id` ve `state` özellikleri sorgulanır hello varlıklar için elde.</span><span class="sxs-lookup"><span data-stu-id="992bf-258">It returns an ODATADetailLevel that specifies that only hello `id` and `state` properties should be obtained for hello entities that are queried.</span></span> <span data-ttu-id="992bf-259">Ayrıca, belirtir, durumu, belirtilen hello bu yana değişti yalnızca varlıklar `DateTime` parametresi döndürülmesi.</span><span class="sxs-lookup"><span data-stu-id="992bf-259">It also specifies that only entities whose state has changed since hello specified `DateTime` parameter should be returned.</span></span>

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a><span data-ttu-id="992bf-260">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="992bf-260">Next steps</span></span>
### <a name="parallel-node-tasks"></a><span data-ttu-id="992bf-261">Paralel düğüm görevleri</span><span class="sxs-lookup"><span data-stu-id="992bf-261">Parallel node tasks</span></span>
<span data-ttu-id="992bf-262">[Eşzamanlı düğüm görevleri ile Azure toplu işlem kaynak kullanımını en üst düzeye](batch-parallel-node-tasks.md) başka bir makale ilgili tooBatch uygulama performansı.</span><span class="sxs-lookup"><span data-stu-id="992bf-262">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) is another article related tooBatch application performance.</span></span> <span data-ttu-id="992bf-263">İş yüklerinin bazı türleri üzerinde Paralel Görevler yürütülürken yararlanabilir büyük--ancak daha az--işlem düğümlerini.</span><span class="sxs-lookup"><span data-stu-id="992bf-263">Some types of workloads can benefit from executing parallel tasks on larger--but fewer--compute nodes.</span></span> <span data-ttu-id="992bf-264">Merhaba denetleyin [Örnek senaryo](batch-parallel-node-tasks.md#example-scenario) hello makalede böyle bir senaryo hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="992bf-264">Check out hello [example scenario](batch-parallel-node-tasks.md#example-scenario) in hello article for details on such a scenario.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="992bf-265">Toplu işlem Forumu</span><span class="sxs-lookup"><span data-stu-id="992bf-265">Batch Forum</span></span>
<span data-ttu-id="992bf-266">Merhaba [Azure toplu işlem Forumu] [ forum] MSDN'de mükemmel toodiscuss toplu yerleştirin ve hello hizmeti hakkında soru sorun olduğunu.</span><span class="sxs-lookup"><span data-stu-id="992bf-266">hello [Azure Batch Forum][forum] on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="992bf-267">HEAD üzerinde üzerinden faydalı "Yapışkan" gönderiler için ve Batch çözümlerinizi derleme sırasında çıktıkları anda sorularınızı gönderin.</span><span class="sxs-lookup"><span data-stu-id="992bf-267">Head on over for helpful "sticky" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

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