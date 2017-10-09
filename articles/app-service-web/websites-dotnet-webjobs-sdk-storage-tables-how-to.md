---
title: "aaaHow toouse hello WebJobs SDK ile Azure tablo depolaması"
description: "Nasıl toouse Azure tablo depolama hello WebJobs SDK ile bilgi edinin. Tabloları oluşturma, varlıkları tootables eklemek ve varolan tabloları okunur."
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
ms.openlocfilehash: 8e28c69df4a934646add9e50c6de28e76dca1636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="128e8-104">Nasıl toouse Azure tablo depolama hello WebJobs SDK ile</span><span class="sxs-lookup"><span data-stu-id="128e8-104">How toouse Azure table storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="128e8-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="128e8-105">Overview</span></span>
<span data-ttu-id="128e8-106">Bu kılavuz C# kod örnekleri nasıl tooread ve yazma Azure depolama tabloları kullanarak gösteren sağlar [WebJobs SDK](websites-dotnet-webjobs-sdk.md) sürüm 1.x.</span><span class="sxs-lookup"><span data-stu-id="128e8-106">This guide provides C# code samples that show how tooread and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="128e8-107">Merhaba Kılavuzu varsayar bildiğiniz [nasıl toocreate bağlantısı ile Visual Studio'da bir Web işi projesi bu noktası tooyour depolama hesabı dizeleri](websites-dotnet-webjobs-sdk-get-started.md) veya çok[birden çok depolama hesabı](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="128e8-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="128e8-108">Merhaba kod parçacıkları bazıları hello Göster `Table` olan işlevlerde kullanılan öznitelik [el ile olarak adlandırılan](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), diğer bir deyişle, birini kullanarak hello tetikleyici öznitelikleri değil.</span><span class="sxs-lookup"><span data-stu-id="128e8-108">Some of hello code snippets show hello `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of hello trigger attributes.</span></span> 

## <span data-ttu-id="128e8-109"><a id="ingress"></a>Nasıl tooadd varlıklar tooa tablosu</span><span class="sxs-lookup"><span data-stu-id="128e8-109"><a id="ingress"></a> How tooadd entities tooa table</span></span>
<span data-ttu-id="128e8-110">tooadd varlıklar tooa tablo, kullanım hello `Table` ile öznitelik bir `ICollector<T>` veya `IAsyncCollector<T>` parametresi nerede `T` hello şema belirtir hello varlıklarının tooadd istiyor.</span><span class="sxs-lookup"><span data-stu-id="128e8-110">tooadd entities tooa table, use hello `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="128e8-111">Merhaba öznitelik oluşturucunun hello Merhaba tablonun adını belirten bir dize parametresi alan.</span><span class="sxs-lookup"><span data-stu-id="128e8-111">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span> 

<span data-ttu-id="128e8-112">Merhaba aşağıdaki kod örneği ekler `Person` adlı varlıklar tooa tablo *giriş*.</span><span class="sxs-lookup"><span data-stu-id="128e8-112">hello following code sample adds `Person` entities tooa table named *Ingress*.</span></span>

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

<span data-ttu-id="128e8-113">Genellikle, kullandığınız ile türünün hello `ICollector` türetilen `TableEntity` veya uygulayan `ITableEntity`, ancak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="128e8-113">Typically hello type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="128e8-114">Merhaba aşağıdakilerden birini `Person` hello önceki gösterilen hello kodu ile çalışma sınıfları `Ingress` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="128e8-114">Either of hello following `Person` classes work with hello code shown in hello preceding `Ingress` method.</span></span>

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

<span data-ttu-id="128e8-115">Ekleyebileceğiniz hello Azure storage API'si ile doğrudan toowork isterseniz, bir `CloudStorageAccount` parametre toohello yöntemi imzası.</span><span class="sxs-lookup"><span data-stu-id="128e8-115">If you want toowork directly with hello Azure storage API, you can add a `CloudStorageAccount` parameter toohello method signature.</span></span>

## <span data-ttu-id="128e8-116"><a id="monitor"></a>Gerçek zamanlı izleme</span><span class="sxs-lookup"><span data-stu-id="128e8-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="128e8-117">Veri giriş işlevleri genellikle büyük miktarda veriyi işlemek için hello Web işleri SDK'si Pano gerçek zamanlı izleme verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="128e8-117">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="128e8-118">Merhaba **çağırma günlüğü** bölüm bildirir hello işlevi halen çalışmakta olup olmadığını.</span><span class="sxs-lookup"><span data-stu-id="128e8-118">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![Çalışan giriş işlevi](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="128e8-120">Merhaba **çağırma ayrıntıları** Raporları Sayfası hello işlevin ilerleme durumu (yazılmış varlıkların sayısı) çalıştıran ve bir fırsat tooabort verir ancak onu.</span><span class="sxs-lookup"><span data-stu-id="128e8-120">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span> 

![Çalışan giriş işlevi](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="128e8-122">Merhaba işlevi tamamlandığında, hello **çağırma ayrıntıları** Raporları Sayfası hello yazılmış satırların sayısı.</span><span class="sxs-lookup"><span data-stu-id="128e8-122">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![Tamamlanmış Giriş işlevi](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="128e8-124"><a id="multiple"></a>Nasıl tooread bir tablodaki birden çok varlık</span><span class="sxs-lookup"><span data-stu-id="128e8-124"><a id="multiple"></a> How tooread multiple entities from a table</span></span>
<span data-ttu-id="128e8-125">tooread bir tablo kullanmak hello `Table` ile öznitelik bir `IQueryable<T>` parametresi girildiği `T` türetilen `TableEntity` veya uygulayan `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="128e8-125">tooread a table, use hello `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="128e8-126">Merhaba aşağıdaki kod örneği okur ve tüm satırları hello günlüklerini `Ingress` tablosu:</span><span class="sxs-lookup"><span data-stu-id="128e8-126">hello following code sample reads and logs all rows from hello `Ingress` table:</span></span>

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

### <span data-ttu-id="128e8-127"><a id="readone"></a>Nasıl tooread bir tablodaki tek bir varlık</span><span class="sxs-lookup"><span data-stu-id="128e8-127"><a id="readone"></a> How tooread a single entity from a table</span></span>
<span data-ttu-id="128e8-128">Var olan bir `Table` öznitelik oluşturucunun toobind tooa tek tablo varlığı istediğinizde hello bölüm anahtarı ve satır anahtarını belirtmenize olanak sağlayan iki ek parametrelere sahip.</span><span class="sxs-lookup"><span data-stu-id="128e8-128">There is a `Table` attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="128e8-129">Merhaba aşağıdaki kod örneği okuyan bir tablo satır için bir `Person` bir kuyruk iletisi alınan bölüm anahtarını ve satır anahtarı değerleri temel varlık:</span><span class="sxs-lookup"><span data-stu-id="128e8-129">hello following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="128e8-130">Merhaba `Person` sınıfı bu örnekte tooimplement yok `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="128e8-130">hello `Person` class in this example does not have tooimplement `ITableEntity`.</span></span>

## <span data-ttu-id="128e8-131"><a id="storageapi"></a>Nasıl toouse hello .NET depolama API doğrudan toowork bir tablo ile</span><span class="sxs-lookup"><span data-stu-id="128e8-131"><a id="storageapi"></a> How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="128e8-132">Merhaba de kullanabilirsiniz `Table` ile öznitelik bir `CloudTable` nesne bir tablo ile çalışma daha fazla esneklik için.</span><span class="sxs-lookup"><span data-stu-id="128e8-132">You can also use hello `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="128e8-133">Merhaba aşağıdaki kod örneği kullanan bir `CloudTable` tooadd tek bir varlık toohello nesne *giriş* tablo.</span><span class="sxs-lookup"><span data-stu-id="128e8-133">hello following code sample uses a `CloudTable` object tooadd a single entity toohello *Ingress* table.</span></span> 

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

<span data-ttu-id="128e8-134">Hakkında daha fazla bilgi için toouse hello `CloudTable` nesne için bkz: [nasıl toouse .NET tablo depolamasından](../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="128e8-134">For more information about how toouse hello `CloudTable` object, see [How toouse Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="128e8-135"><a id="queues"></a>Merhaba sıraları nasıl-tooarticle tarafından kapsanan ilgili konular</span><span class="sxs-lookup"><span data-stu-id="128e8-135"><a id="queues"></a>Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="128e8-136">Nasıl toohandle tablo işleme bir kuyruk iletisi tarafından veya WebJobs SDK senaryoları tetiklenen değil hakkında bilgi için işleme, özel tootable bakın [nasıl toouse Azure kuyruk depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="128e8-136">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="128e8-137">Bu makalede ele alınan konular hello şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="128e8-137">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="128e8-138">Zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="128e8-138">Async functions</span></span>
* <span data-ttu-id="128e8-139">Birden çok örneği</span><span class="sxs-lookup"><span data-stu-id="128e8-139">Multiple instances</span></span>
* <span data-ttu-id="128e8-140">Kapama</span><span class="sxs-lookup"><span data-stu-id="128e8-140">Graceful shutdown</span></span>
* <span data-ttu-id="128e8-141">Web işleri SDK'si özniteliklerini işlevinin hello gövdesindeki kullanın</span><span class="sxs-lookup"><span data-stu-id="128e8-141">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="128e8-142">Kod içinde Hello SDK bağlantı dizelerini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="128e8-142">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="128e8-143">Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama</span><span class="sxs-lookup"><span data-stu-id="128e8-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="128e8-144">Tetik el ile bir işlevi</span><span class="sxs-lookup"><span data-stu-id="128e8-144">Trigger a function manually</span></span>
* <span data-ttu-id="128e8-145">Günlüklerini yazma</span><span class="sxs-lookup"><span data-stu-id="128e8-145">Write logs</span></span>

## <span data-ttu-id="128e8-146"><a id="nextsteps"></a> Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="128e8-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="128e8-147">Bu kılavuz kodu sağlamıştır gösteren nasıl örnekleri Azure tabloları ile çalışmak için genel senaryolar toohandle.</span><span class="sxs-lookup"><span data-stu-id="128e8-147">This guide has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="128e8-148">Toouse Azure Web işleri ve hello Web işleri SDK'si nasıl görürüm hakkında daha fazla bilgi için [Azure Web işleri önerilen kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="128e8-148">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

