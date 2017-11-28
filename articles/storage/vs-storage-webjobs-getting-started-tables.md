---
title: "Azure depolama ve Visual Studio ile başlatıldı aaaGetting Hizmetleri (Web işi projeleri) bağlı"
description: "Nasıl tooget Visual Studio kullanarak tooa depolama hesabı bağlanma Hizmetleri bağlandıktan sonra Azure Table depolama Visual Studio'daki Azure Web işleri projesinde kullanmaya"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 448dee3369207062ee85c6636c84bcb4e26a2085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="2b94c-103">Azure ile çalışmaya başlama depolama (Azure Web işi projeler)</span><span class="sxs-lookup"><span data-stu-id="2b94c-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="2b94c-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2b94c-104">Overview</span></span>
<span data-ttu-id="2b94c-105">Bu makalede gösteren C# kod örnekleri Göster nasıl toouse hello Azure WebJobs SDK sürüm sağlar 1.x hello Azure tablo depolama hizmeti ile.</span><span class="sxs-lookup"><span data-stu-id="2b94c-105">This article provides C# code samples that show show how toouse hello Azure WebJobs SDK version 1.x with hello Azure table storage service.</span></span> <span data-ttu-id="2b94c-106">Merhaba kod örnekleri kullanır hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) sürüm 1.x.</span><span class="sxs-lookup"><span data-stu-id="2b94c-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="2b94c-107">Hello Azure Table depolama hizmeti toostore büyük miktarlarda yapılandırılmış veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="2b94c-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="2b94c-108">Merhaba, iç ve dış hello Azure bulut gelen kimliği doğrulanmış çağrıları kabul eden bir NoSQL veri deposu hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="2b94c-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="2b94c-109">Azure tabloları, yapılandırılmış ve ilişkisel olmayan verilerin depolanması için idealdir.</span><span class="sxs-lookup"><span data-stu-id="2b94c-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="2b94c-110">Bkz: [.NET kullanarak Azure Table storage'ı kullanmaya başlama](storage-dotnet-how-to-use-tables.md#create-a-table) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="2b94c-110">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md#create-a-table) for more information.</span></span>

<span data-ttu-id="2b94c-111">Merhaba kod parçacıkları bazıları hello Göster **tablo** el ile diğer bir deyişle, hello tetikleyici özniteliklerinden biri kullanılarak değil çağrılır işlevlerde kullanılan öznitelik.</span><span class="sxs-lookup"><span data-stu-id="2b94c-111">Some of hello code snippets show hello **Table** attribute used in functions that are called manually, that is, not by using one of hello trigger attributes.</span></span>

## <a name="how-tooadd-entities-tooa-table"></a><span data-ttu-id="2b94c-112">Nasıl tooadd varlıklar tooa tablosu</span><span class="sxs-lookup"><span data-stu-id="2b94c-112">How tooadd entities tooa table</span></span>
<span data-ttu-id="2b94c-113">tooadd varlıklar tooa tablo, kullanım hello **tablo** ile öznitelik bir **ICollector<T>**  veya **IAsyncCollector<T>**  parametresi nerede **T** hello şema belirtir hello varlıklarının tooadd istiyor.</span><span class="sxs-lookup"><span data-stu-id="2b94c-113">tooadd entities tooa table, use hello **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="2b94c-114">Merhaba öznitelik oluşturucunun hello Merhaba tablonun adını belirten bir dize parametresi alan.</span><span class="sxs-lookup"><span data-stu-id="2b94c-114">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span>

<span data-ttu-id="2b94c-115">Merhaba aşağıdaki kod örneği ekler **kişi** adlı varlıklar tooa tablo *giriş*.</span><span class="sxs-lookup"><span data-stu-id="2b94c-115">hello following code sample adds **Person** entities tooa table named *Ingress*.</span></span>

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

<span data-ttu-id="2b94c-116">Genellikle, kullandığınız ile türünün hello **ICollector** türetilen **TableEntity** veya uygulayan **ITableEntity**, ancak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="2b94c-116">Typically hello type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="2b94c-117">Merhaba aşağıdakilerden birini **kişi** hello önceki gösterilen hello kodu ile çalışma sınıfları **giriş** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="2b94c-117">Either of hello following **Person** classes work with hello code shown in hello preceding **Ingress** method.</span></span>

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

<span data-ttu-id="2b94c-118">Ekleyebileceğiniz hello Azure storage API'si ile doğrudan toowork isterseniz, bir **CloudStorageAccount** parametre toohello yöntemi imzası.</span><span class="sxs-lookup"><span data-stu-id="2b94c-118">If you want toowork directly with hello Azure storage API, you can add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="2b94c-119">Gerçek zamanlı izleme</span><span class="sxs-lookup"><span data-stu-id="2b94c-119">Real-time monitoring</span></span>
<span data-ttu-id="2b94c-120">Veri giriş işlevleri genellikle büyük miktarda veriyi işlemek için hello Web işleri SDK'si Pano gerçek zamanlı izleme verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="2b94c-120">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="2b94c-121">Merhaba **çağırma günlüğü** bölüm bildirir hello işlevi halen çalışmakta olup olmadığını.</span><span class="sxs-lookup"><span data-stu-id="2b94c-121">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![Çalışan giriş işlevi](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="2b94c-123">Merhaba **çağırma ayrıntıları** Raporları Sayfası hello işlevin ilerleme durumu (yazılmış varlıkların sayısı) çalıştıran ve bir fırsat tooabort verir ancak onu.</span><span class="sxs-lookup"><span data-stu-id="2b94c-123">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span>

![Çalışan giriş işlevi](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="2b94c-125">Merhaba işlevi tamamlandığında, hello **çağırma ayrıntıları** Raporları Sayfası hello yazılmış satırların sayısı.</span><span class="sxs-lookup"><span data-stu-id="2b94c-125">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![Tamamlanmış Giriş işlevi](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a><span data-ttu-id="2b94c-127">Nasıl tooread bir tablodaki birden çok varlık</span><span class="sxs-lookup"><span data-stu-id="2b94c-127">How tooread multiple entities from a table</span></span>
<span data-ttu-id="2b94c-128">tooread bir tablo kullanmak hello **tablo** ile öznitelik bir **Iqueryable<T>**  parametresi girildiği **T** türetilen **TableEntity**veya uygulayan **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="2b94c-128">tooread a table, use hello **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="2b94c-129">Merhaba aşağıdaki kod örneği okur ve tüm satırları hello günlüklerini **giriş** tablosu:</span><span class="sxs-lookup"><span data-stu-id="2b94c-129">hello following code sample reads and logs all rows from hello **Ingress** table:</span></span>

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

### <a name="how-tooread-a-single-entity-from-a-table"></a><span data-ttu-id="2b94c-130">Nasıl tooread bir tablodaki tek bir varlık</span><span class="sxs-lookup"><span data-stu-id="2b94c-130">How tooread a single entity from a table</span></span>
<span data-ttu-id="2b94c-131">Var olan bir **tablo** öznitelik oluşturucunun toobind tooa tek tablo varlığı istediğinizde hello bölüm anahtarı ve satır anahtarını belirtmenize olanak sağlayan iki ek parametrelere sahip.</span><span class="sxs-lookup"><span data-stu-id="2b94c-131">There is a **Table** attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="2b94c-132">Merhaba aşağıdaki kod örneği okuyan bir tablo satır için bir **kişi** bir kuyruk iletisi alınan bölüm anahtarını ve satır anahtarı değerleri temel varlık:</span><span class="sxs-lookup"><span data-stu-id="2b94c-132">hello following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="2b94c-133">Merhaba **kişi** sınıfı bu örnekte tooimplement yok **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="2b94c-133">hello **Person** class in this example does not have tooimplement **ITableEntity**.</span></span>

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a><span data-ttu-id="2b94c-134">Nasıl toouse hello .NET depolama API doğrudan toowork bir tablo ile</span><span class="sxs-lookup"><span data-stu-id="2b94c-134">How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="2b94c-135">Merhaba de kullanabilirsiniz **tablo** ile öznitelik bir **CloudTable** nesne bir tablo ile çalışma daha fazla esneklik için.</span><span class="sxs-lookup"><span data-stu-id="2b94c-135">You can also use hello **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="2b94c-136">Merhaba aşağıdaki kod örneği kullanan bir **CloudTable** tooadd tek bir varlık toohello nesne *giriş* tablo.</span><span class="sxs-lookup"><span data-stu-id="2b94c-136">hello following code sample uses a **CloudTable** object tooadd a single entity toohello *Ingress* table.</span></span>

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

<span data-ttu-id="2b94c-137">Hakkında daha fazla bilgi için toouse hello **CloudTable** nesne için bkz: [.NET kullanarak Azure Table storage'ı kullanmaya başlama](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="2b94c-137">For more information about how toouse hello **CloudTable** object, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a><span data-ttu-id="2b94c-138">Merhaba sıraları nasıl-tooarticle tarafından kapsanan ilgili konular</span><span class="sxs-lookup"><span data-stu-id="2b94c-138">Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="2b94c-139">Nasıl toohandle tablo işleme bir kuyruk iletisi tarafından veya WebJobs SDK senaryoları tetiklenen değil hakkında bilgi için işleme, özel tootable bakın [bağlı Hizmetleri (Web işi projeleri) Azure kuyruk depolama ve Visual Studio ile çalışmaya başlama ](vs-storage-webjobs-getting-started-queues.md).</span><span class="sxs-lookup"><span data-stu-id="2b94c-139">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b94c-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2b94c-140">Next steps</span></span>
<span data-ttu-id="2b94c-141">Bu makalede kod sağlamıştır gösteren nasıl örnekleri Azure tabloları ile çalışmak için genel senaryolar toohandle.</span><span class="sxs-lookup"><span data-stu-id="2b94c-141">This article has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="2b94c-142">Toouse Azure Web işleri ve hello Web işleri SDK'si nasıl görürüm hakkında daha fazla bilgi için [Azure Web işleri belge kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="2b94c-142">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

