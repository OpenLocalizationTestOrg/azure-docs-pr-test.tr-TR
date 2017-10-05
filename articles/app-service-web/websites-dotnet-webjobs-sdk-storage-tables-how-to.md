---
title: "WebJobs SDK ile Azure tablo depolama kullanımı"
description: "WebJobs SDK ile Azure tablo depolaması kullanmayı öğrenin. Tablolar oluşturma tablolar için varlıklar ekleyebilir ve var olan tabloları okunur."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 451432cc-c780-4310-85d3-84f44fe48afe
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 13cfc788c14d714df7022ce003d34691cf73d121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-with-the-webjobs-sdk"></a><span data-ttu-id="d3191-104">WebJobs SDK ile Azure tablo depolama kullanımı</span><span class="sxs-lookup"><span data-stu-id="d3191-104">How to use Azure table storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="d3191-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d3191-105">Overview</span></span>
<span data-ttu-id="d3191-106">Bu kılavuz kullanarak Azure depolama tabloları okumasına ve yazmasına nasıl gösteren C# kod örnekleri sağlar [WebJobs SDK](websites-dotnet-webjobs-sdk.md) sürüm 1.x.</span><span class="sxs-lookup"><span data-stu-id="d3191-106">This guide provides C# code samples that show how to read and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="d3191-107">Bildiğiniz Kılavuzu varsayar [bağlantıyla Visual Studio'da bir Web işi projesi oluşturma, depolama hesabınıza o noktadan dizeleri](websites-dotnet-webjobs-sdk-get-started.md) veya [birden çok depolama hesabı](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="d3191-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="d3191-108">Kod parçacıkları Göster bazıları `Table` olan işlevlerde kullanılan öznitelik [el ile olarak adlandırılan](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), diğer bir deyişle, tetikleyici özniteliklerden birini kullanarak değil.</span><span class="sxs-lookup"><span data-stu-id="d3191-108">Some of the code snippets show the `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of the trigger attributes.</span></span> 

## <span data-ttu-id="d3191-109"><a id="ingress"></a>Bir tabloya varlıklar ekleme</span><span class="sxs-lookup"><span data-stu-id="d3191-109"><a id="ingress"></a> How to add entities to a table</span></span>
<span data-ttu-id="d3191-110">Bir tabloya varlıkları eklemek için kullanın `Table` ile öznitelik bir `ICollector<T>` veya `IAsyncCollector<T>` parametresi nerede `T` eklemek istediğiniz varlıklar şeması belirtir.</span><span class="sxs-lookup"><span data-stu-id="d3191-110">To add entities to a table, use the `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="d3191-111">Öznitelik oluşturucunun tablonun adını belirten bir dize parametresi alan.</span><span class="sxs-lookup"><span data-stu-id="d3191-111">The attribute constructor takes a string parameter that specifies the name of the table.</span></span> 

<span data-ttu-id="d3191-112">Aşağıdaki kod örneği ekler `Person` adlı bir tablo varlıklara *giriş*.</span><span class="sxs-lookup"><span data-stu-id="d3191-112">The following code sample adds `Person` entities to a table named *Ingress*.</span></span>

        [NoAutomaticTrigger]
        public static void IngressDemo(
            [Table("Ingress")] ICollector<Person> tableBinding)
        {
            for (int i = 0; i < 100000; i++)
            {
                tableBinding.Add(
                    new Person() { 
                        PartitionKey = "Test", 
                        RowKey = i.ToString(), 
                        Name = "Name" }
                    );
            }
        }

<span data-ttu-id="d3191-113">Genellikle türü ile kullandığınız `ICollector` türetilen `TableEntity` veya uygulayan `ITableEntity`, ancak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="d3191-113">Typically the type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="d3191-114">Aşağıdakilerden birini `Person` önceki gösterilen kodu ile çalışma sınıfları `Ingress` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d3191-114">Either of the following `Person` classes work with the code shown in the preceding `Ingress` method.</span></span>

        public class Person : TableEntity
        {
            public string Name { get; set; }
        }

        public class Person
        {
            public string PartitionKey { get; set; }
            public string RowKey { get; set; }
            public string Name { get; set; }
        }

<span data-ttu-id="d3191-115">Ekleyebileceğiniz doğrudan Azure storage ile API çalışmak isterseniz, bir `CloudStorageAccount` yöntem imzası parametresi.</span><span class="sxs-lookup"><span data-stu-id="d3191-115">If you want to work directly with the Azure storage API, you can add a `CloudStorageAccount` parameter to the method signature.</span></span>

## <span data-ttu-id="d3191-116"><a id="monitor"></a>Gerçek zamanlı izleme</span><span class="sxs-lookup"><span data-stu-id="d3191-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="d3191-117">Veri giriş işlevleri genellikle büyük miktarda veriyi işlemek için Web işleri SDK'si Pano gerçek zamanlı izleme verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3191-117">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="d3191-118">**Çağırma günlüğü** bölüm bildirir işlevi halen çalışmakta olup olmadığını.</span><span class="sxs-lookup"><span data-stu-id="d3191-118">The **Invocation Log** section tells you if the function is still running.</span></span>

![Çalışan giriş işlevi](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="d3191-120">**Çağırma ayrıntıları** Raporları Sayfası işlevin ilerleme durumu (yazılmış varlıkların sayısı) çalıştıran ve onu abort fırsatı sunar.</span><span class="sxs-lookup"><span data-stu-id="d3191-120">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span> 

![Çalışan giriş işlevi](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="d3191-122">İşlev sona erdiğinde, **çağırma ayrıntıları** Raporları Sayfası yazılmış satırların sayısı.</span><span class="sxs-lookup"><span data-stu-id="d3191-122">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![Tamamlanmış Giriş işlevi](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="d3191-124"><a id="multiple"></a>Birden çok varlık bir tablodan okumak nasıl</span><span class="sxs-lookup"><span data-stu-id="d3191-124"><a id="multiple"></a> How to read multiple entities from a table</span></span>
<span data-ttu-id="d3191-125">Bir tablo okumak için kullandığınız `Table` ile öznitelik bir `IQueryable<T>` parametresi girildiği `T` türetilen `TableEntity` veya uygulayan `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="d3191-125">To read a table, use the `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="d3191-126">Aşağıdaki kod örneği okur ve tüm satırları günlüklerini `Ingress` tablosu:</span><span class="sxs-lookup"><span data-stu-id="d3191-126">The following code sample reads and logs all rows from the `Ingress` table:</span></span>

        public static void ReadTable(
            [Table("Ingress")] IQueryable<Person> tableBinding,
            TextWriter logger)
        {
            var query = from p in tableBinding select p;
            foreach (Person person in query)
            {
                logger.WriteLine("PK:{0}, RK:{1}, Name:{2}", 
                    person.PartitionKey, person.RowKey, person.Name);
            }
        }

### <span data-ttu-id="d3191-127"><a id="readone"></a>Tek bir varlık tablodan okumak nasıl</span><span class="sxs-lookup"><span data-stu-id="d3191-127"><a id="readone"></a> How to read a single entity from a table</span></span>
<span data-ttu-id="d3191-128">Var olan bir `Table` öznitelik oluşturucunun tek tablo varlığa bağlamak istediğinizde bölüm anahtarını ve satır anahtarını belirtmenize olanak sağlayan iki ek parametrelere sahip.</span><span class="sxs-lookup"><span data-stu-id="d3191-128">There is a `Table` attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="d3191-129">Aşağıdaki kod örneği için bir tablo satır okuyan bir `Person` bir kuyruk iletisi alınan bölüm anahtarını ve satır anahtarı değerleri temel varlık:</span><span class="sxs-lookup"><span data-stu-id="d3191-129">The following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

        public static void ReadTableEntity(
            [QueueTrigger("inputqueue")] Person personInQueue,
            [Table("persontable","{PartitionKey}", "{RowKey}")] Person personInTable,
            TextWriter logger)
        {
            if (personInTable == null)
            {
                logger.WriteLine("Person not found: PK:{0}, RK:{1}",
                        personInQueue.PartitionKey, personInQueue.RowKey);
            }
            else
            {
                logger.WriteLine("Person found: PK:{0}, RK:{1}, Name:{2}",
                        personInTable.PartitionKey, personInTable.RowKey, personInTable.Name);
            }
        }


<span data-ttu-id="d3191-130">`Person` Uygulamak Bu örnekte sınıfı yok `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="d3191-130">The `Person` class in this example does not have to implement `ITableEntity`.</span></span>

## <span data-ttu-id="d3191-131"><a id="storageapi"></a>Bir tablo ile doğrudan çalışmak için .NET depolama API kullanma</span><span class="sxs-lookup"><span data-stu-id="d3191-131"><a id="storageapi"></a> How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="d3191-132">Aynı zamanda `Table` ile öznitelik bir `CloudTable` nesne bir tablo ile çalışma daha fazla esneklik için.</span><span class="sxs-lookup"><span data-stu-id="d3191-132">You can also use the `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="d3191-133">Aşağıdaki kod örneği kullanan bir `CloudTable` tek bir varlık eklemek için nesne *giriş* tablo.</span><span class="sxs-lookup"><span data-stu-id="d3191-133">The following code sample uses a `CloudTable` object to add a single entity to the *Ingress* table.</span></span> 

        public static void UseStorageAPI(
            [Table("Ingress")] CloudTable tableBinding,
            TextWriter logger)
        {
            var person = new Person()
                {
                    PartitionKey = "Test",
                    RowKey = "100",
                    Name = "Name"
                };
            TableOperation insertOperation = TableOperation.Insert(person);
            tableBinding.Execute(insertOperation);
        }

<span data-ttu-id="d3191-134">Nasıl kullanılacağı hakkında daha fazla bilgi için `CloudTable` nesne için bkz: [.NET tablo depolamasından kullanmayı](../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="d3191-134">For more information about how to use the `CloudTable` object, see [How to use Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="d3191-135"><a id="queues"></a>Kuyruklar nasıl yapılır makalesi tarafından kapsanan ilgili konular</span><span class="sxs-lookup"><span data-stu-id="d3191-135"><a id="queues"></a>Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="d3191-136">Bir kuyruk iletisi tarafından tetiklenen tablo işleme nasıl ele alınacağını hakkında bilgi için veya tablo işlemeye özel olmayan Web işleri SDK'si senaryoları için bkz: [WebJobs SDK ile Azure kuyruk depolama kullanma](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="d3191-136">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="d3191-137">Bu makalede ele alınan konular şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d3191-137">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="d3191-138">Zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="d3191-138">Async functions</span></span>
* <span data-ttu-id="d3191-139">Birden çok örneği</span><span class="sxs-lookup"><span data-stu-id="d3191-139">Multiple instances</span></span>
* <span data-ttu-id="d3191-140">Kapama</span><span class="sxs-lookup"><span data-stu-id="d3191-140">Graceful shutdown</span></span>
* <span data-ttu-id="d3191-141">Web işleri SDK'si öznitelikleri bir işlev gövdesine kullanın</span><span class="sxs-lookup"><span data-stu-id="d3191-141">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="d3191-142">Kod içinde SDK bağlantı dizelerini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="d3191-142">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="d3191-143">Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama</span><span class="sxs-lookup"><span data-stu-id="d3191-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="d3191-144">Tetik el ile bir işlevi</span><span class="sxs-lookup"><span data-stu-id="d3191-144">Trigger a function manually</span></span>
* <span data-ttu-id="d3191-145">Günlüklerini yazma</span><span class="sxs-lookup"><span data-stu-id="d3191-145">Write logs</span></span>

## <span data-ttu-id="d3191-146"><a id="nextsteps"></a> Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d3191-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="d3191-147">Bu kılavuz, Azure tabloları ile çalışmak için genel senaryolar nasıl ele alınacağını gösteren kod örnekleri sağlamıştır.</span><span class="sxs-lookup"><span data-stu-id="d3191-147">This guide has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="d3191-148">Azure Web işleri ve WebJobs SDK nasıl kullanılacağı hakkında daha fazla bilgi için bkz: [Azure Web işleri önerilen kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="d3191-148">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

