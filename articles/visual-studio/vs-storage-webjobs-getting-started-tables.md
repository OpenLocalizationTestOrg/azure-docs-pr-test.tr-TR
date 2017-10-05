---
title: "Azure depolama ve Visual Studio ile çalışmaya başlama bağlı Hizmetleri (Web işi projeler)"
description: "Visual Studio kullanarak bir depolama hesabı bağlandıktan sonra Visual Studio'da Azure Web işleri projesinde Azure tablo depolaması ile çalışmaya başlamak nasıl bağlı Hizmetleri"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 0bf51f9113c45c747cd4fd3f76bdabd4a4c1f8e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="e25d2-103">Azure ile çalışmaya başlama depolama (Azure Web işi projeler)</span><span class="sxs-lookup"><span data-stu-id="e25d2-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="e25d2-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e25d2-104">Overview</span></span>
<span data-ttu-id="e25d2-105">Bu makalede gösteren C# kod örnekleri Göster Azure WebJobs SDK sürümü kullanmak nasıl sağlar 1.x Azure tablo depolama hizmeti ile.</span><span class="sxs-lookup"><span data-stu-id="e25d2-105">This article provides C# code samples that show show how to use the Azure WebJobs SDK version 1.x with the Azure table storage service.</span></span> <span data-ttu-id="e25d2-106">Kod örnekleri kullan [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) sürüm 1.x.</span><span class="sxs-lookup"><span data-stu-id="e25d2-106">The code samples use the [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="e25d2-107">Azure Table depolama birimi hizmeti, büyük miktarlarda yapılandırılmış verileri depolamak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e25d2-107">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="e25d2-108">Kimliği doğrulanmış çağrılarından içinden ve dışından Azure bulut kabul eden bir NoSQL veri deposu hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="e25d2-108">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="e25d2-109">Azure tabloları, yapılandırılmış ve ilişkisel olmayan verilerin depolanması için idealdir.</span><span class="sxs-lookup"><span data-stu-id="e25d2-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="e25d2-110">Bkz: [.NET kullanarak Azure Table storage'ı kullanmaya başlama](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="e25d2-110">See [Get started with Azure Table storage using .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) for more information.</span></span>

<span data-ttu-id="e25d2-111">Kod parçacıkları Göster bazıları **tablo** el ile diğer bir deyişle, tetikleyici özniteliklerinden biri kullanılarak değil çağrılır işlevlerde kullanılan öznitelik.</span><span class="sxs-lookup"><span data-stu-id="e25d2-111">Some of the code snippets show the **Table** attribute used in functions that are called manually, that is, not by using one of the trigger attributes.</span></span>

## <a name="how-to-add-entities-to-a-table"></a><span data-ttu-id="e25d2-112">Bir tabloya varlıklar ekleme</span><span class="sxs-lookup"><span data-stu-id="e25d2-112">How to add entities to a table</span></span>
<span data-ttu-id="e25d2-113">Bir tabloya varlıkları eklemek için kullanın **tablo** ile öznitelik bir **ICollector<T>**  veya **IAsyncCollector<T>**  parametresi nerede **T** eklemek istediğiniz varlıklar şeması belirtir.</span><span class="sxs-lookup"><span data-stu-id="e25d2-113">To add entities to a table, use the **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="e25d2-114">Öznitelik oluşturucunun tablonun adını belirten bir dize parametresi alan.</span><span class="sxs-lookup"><span data-stu-id="e25d2-114">The attribute constructor takes a string parameter that specifies the name of the table.</span></span>

<span data-ttu-id="e25d2-115">Aşağıdaki kod örneği ekler **kişi** adlı bir tablo varlıklara *giriş*.</span><span class="sxs-lookup"><span data-stu-id="e25d2-115">The following code sample adds **Person** entities to a table named *Ingress*.</span></span>

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

<span data-ttu-id="e25d2-116">Genellikle türü ile kullandığınız **ICollector** türetilen **TableEntity** veya uygulayan **ITableEntity**, ancak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="e25d2-116">Typically the type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="e25d2-117">Aşağıdakilerden birini **kişi** önceki gösterilen kodu ile çalışma sınıfları **giriş** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e25d2-117">Either of the following **Person** classes work with the code shown in the preceding **Ingress** method.</span></span>

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

<span data-ttu-id="e25d2-118">Ekleyebileceğiniz doğrudan Azure storage ile API çalışmak isterseniz, bir **CloudStorageAccount** yöntem imzası parametresi.</span><span class="sxs-lookup"><span data-stu-id="e25d2-118">If you want to work directly with the Azure storage API, you can add a **CloudStorageAccount** parameter to the method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="e25d2-119">Gerçek zamanlı izleme</span><span class="sxs-lookup"><span data-stu-id="e25d2-119">Real-time monitoring</span></span>
<span data-ttu-id="e25d2-120">Veri giriş işlevleri genellikle büyük miktarda veriyi işlemek için Web işleri SDK'si Pano gerçek zamanlı izleme verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="e25d2-120">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="e25d2-121">**Çağırma günlüğü** bölüm bildirir işlevi halen çalışmakta olup olmadığını.</span><span class="sxs-lookup"><span data-stu-id="e25d2-121">The **Invocation Log** section tells you if the function is still running.</span></span>

![Çalışan giriş işlevi](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="e25d2-123">**Çağırma ayrıntıları** Raporları Sayfası işlevin ilerleme durumu (yazılmış varlıkların sayısı) çalıştıran ve onu abort fırsatı sunar.</span><span class="sxs-lookup"><span data-stu-id="e25d2-123">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span>

![Çalışan giriş işlevi](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="e25d2-125">İşlev sona erdiğinde, **çağırma ayrıntıları** Raporları Sayfası yazılmış satırların sayısı.</span><span class="sxs-lookup"><span data-stu-id="e25d2-125">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![Tamamlanmış Giriş işlevi](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-to-read-multiple-entities-from-a-table"></a><span data-ttu-id="e25d2-127">Birden çok varlık bir tablodan okumak nasıl</span><span class="sxs-lookup"><span data-stu-id="e25d2-127">How to read multiple entities from a table</span></span>
<span data-ttu-id="e25d2-128">Bir tablo okumak için kullandığınız **tablo** ile öznitelik bir **Iqueryable<T>**  parametresi girildiği **T** türetilen **TableEntity** veya uygulayan **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="e25d2-128">To read a table, use the **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="e25d2-129">Aşağıdaki kod örneği okur ve tüm satırları günlüklerini **giriş** tablosu:</span><span class="sxs-lookup"><span data-stu-id="e25d2-129">The following code sample reads and logs all rows from the **Ingress** table:</span></span>

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

### <a name="how-to-read-a-single-entity-from-a-table"></a><span data-ttu-id="e25d2-130">Tek bir varlık tablodan okumak nasıl</span><span class="sxs-lookup"><span data-stu-id="e25d2-130">How to read a single entity from a table</span></span>
<span data-ttu-id="e25d2-131">Var olan bir **tablo** öznitelik oluşturucunun tek tablo varlığa bağlamak istediğinizde bölüm anahtarını ve satır anahtarını belirtmenize olanak sağlayan iki ek parametrelere sahip.</span><span class="sxs-lookup"><span data-stu-id="e25d2-131">There is a **Table** attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="e25d2-132">Aşağıdaki kod örneği için bir tablo satır okuyan bir **kişi** bir kuyruk iletisi alınan bölüm anahtarını ve satır anahtarı değerleri temel varlık:</span><span class="sxs-lookup"><span data-stu-id="e25d2-132">The following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="e25d2-133">**Kişi** uygulamak Bu örnekte sınıfı yok **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="e25d2-133">The **Person** class in this example does not have to implement **ITableEntity**.</span></span>

## <a name="how-to-use-the-net-storage-api-directly-to-work-with-a-table"></a><span data-ttu-id="e25d2-134">Bir tablo ile doğrudan çalışmak için .NET depolama API kullanma</span><span class="sxs-lookup"><span data-stu-id="e25d2-134">How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="e25d2-135">Aynı zamanda **tablo** ile öznitelik bir **CloudTable** nesne bir tablo ile çalışma daha fazla esneklik için.</span><span class="sxs-lookup"><span data-stu-id="e25d2-135">You can also use the **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="e25d2-136">Aşağıdaki kod örneği kullanan bir **CloudTable** tek bir varlık eklemek için nesne *giriş* tablo.</span><span class="sxs-lookup"><span data-stu-id="e25d2-136">The following code sample uses a **CloudTable** object to add a single entity to the *Ingress* table.</span></span>

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

<span data-ttu-id="e25d2-137">Nasıl kullanılacağı hakkında daha fazla bilgi için **CloudTable** nesne için bkz: [.NET kullanarak Azure Table storage'ı kullanmaya başlama](../storage/storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="e25d2-137">For more information about how to use the **CloudTable** object, see [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-the-queues-how-to-article"></a><span data-ttu-id="e25d2-138">Kuyruklar nasıl yapılır makalesi tarafından kapsanan ilgili konular</span><span class="sxs-lookup"><span data-stu-id="e25d2-138">Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="e25d2-139">Bir kuyruk iletisi tarafından tetiklenen tablo işleme nasıl ele alınacağını hakkında bilgi için veya tablo işlemeye özel olmayan Web işleri SDK'si senaryoları için bkz: [bağlı Hizmetleri (Web işi projeleri) Azure kuyruk depolama ve Visual Studio ile çalışmaya başlama](../storage/vs-storage-webjobs-getting-started-queues.md).</span><span class="sxs-lookup"><span data-stu-id="e25d2-139">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](../storage/vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e25d2-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e25d2-140">Next steps</span></span>
<span data-ttu-id="e25d2-141">Bu makalede Azure tabloları ile çalışmak için genel senaryolar nasıl ele alınacağını gösteren kod örnekleri sağlamıştır.</span><span class="sxs-lookup"><span data-stu-id="e25d2-141">This article has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="e25d2-142">Azure Web işleri ve WebJobs SDK nasıl kullanılacağı hakkında daha fazla bilgi için bkz: [Azure Web işleri belge kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="e25d2-142">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

