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
# <a name="how-to-use-azure-table-storage-with-the-webjobs-sdk"></a>WebJobs SDK ile Azure tablo depolama kullanımı
## <a name="overview"></a>Genel Bakış
Bu kılavuz kullanarak Azure depolama tabloları okumasına ve yazmasına nasıl gösteren C# kod örnekleri sağlar [WebJobs SDK](websites-dotnet-webjobs-sdk.md) sürüm 1.x.

Bildiğiniz Kılavuzu varsayar [bağlantıyla Visual Studio'da bir Web işi projesi oluşturma, depolama hesabınıza o noktadan dizeleri](websites-dotnet-webjobs-sdk-get-started.md) veya [birden çok depolama hesabı](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

Kod parçacıkları Göster bazıları `Table` olan işlevlerde kullanılan öznitelik [el ile olarak adlandırılan](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), diğer bir deyişle, tetikleyici özniteliklerden birini kullanarak değil. 

## <a id="ingress"></a>Bir tabloya varlıklar ekleme
Bir tabloya varlıkları eklemek için kullanın `Table` ile öznitelik bir `ICollector<T>` veya `IAsyncCollector<T>` parametresi nerede `T` eklemek istediğiniz varlıklar şeması belirtir. Öznitelik oluşturucunun tablonun adını belirten bir dize parametresi alan. 

Aşağıdaki kod örneği ekler `Person` adlı bir tablo varlıklara *giriş*.

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

Genellikle türü ile kullandığınız `ICollector` türetilen `TableEntity` veya uygulayan `ITableEntity`, ancak gerekli değildir. Aşağıdakilerden birini `Person` önceki gösterilen kodu ile çalışma sınıfları `Ingress` yöntemi.

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

Ekleyebileceğiniz doğrudan Azure storage ile API çalışmak isterseniz, bir `CloudStorageAccount` yöntem imzası parametresi.

## <a id="monitor"></a>Gerçek zamanlı izleme
Veri giriş işlevleri genellikle büyük miktarda veriyi işlemek için Web işleri SDK'si Pano gerçek zamanlı izleme verileri sağlar. **Çağırma günlüğü** bölüm bildirir işlevi halen çalışmakta olup olmadığını.

![Çalışan giriş işlevi](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

**Çağırma ayrıntıları** Raporları Sayfası işlevin ilerleme durumu (yazılmış varlıkların sayısı) çalıştıran ve onu abort fırsatı sunar. 

![Çalışan giriş işlevi](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

İşlev sona erdiğinde, **çağırma ayrıntıları** Raporları Sayfası yazılmış satırların sayısı.

![Tamamlanmış Giriş işlevi](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <a id="multiple"></a>Birden çok varlık bir tablodan okumak nasıl
Bir tablo okumak için kullandığınız `Table` ile öznitelik bir `IQueryable<T>` parametresi girildiği `T` türetilen `TableEntity` veya uygulayan `ITableEntity`.

Aşağıdaki kod örneği okur ve tüm satırları günlüklerini `Ingress` tablosu:

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

### <a id="readone"></a>Tek bir varlık tablodan okumak nasıl
Var olan bir `Table` öznitelik oluşturucunun tek tablo varlığa bağlamak istediğinizde bölüm anahtarını ve satır anahtarını belirtmenize olanak sağlayan iki ek parametrelere sahip.

Aşağıdaki kod örneği için bir tablo satır okuyan bir `Person` bir kuyruk iletisi alınan bölüm anahtarını ve satır anahtarı değerleri temel varlık:  

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


`Person` Uygulamak Bu örnekte sınıfı yok `ITableEntity`.

## <a id="storageapi"></a>Bir tablo ile doğrudan çalışmak için .NET depolama API kullanma
Aynı zamanda `Table` ile öznitelik bir `CloudTable` nesne bir tablo ile çalışma daha fazla esneklik için.

Aşağıdaki kod örneği kullanan bir `CloudTable` tek bir varlık eklemek için nesne *giriş* tablo. 

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

Nasıl kullanılacağı hakkında daha fazla bilgi için `CloudTable` nesne için bkz: [.NET tablo depolamasından kullanmayı](../cosmos-db/table-storage-how-to-use-dotnet.md). 

## <a id="queues"></a>Kuyruklar nasıl yapılır makalesi tarafından kapsanan ilgili konular
Bir kuyruk iletisi tarafından tetiklenen tablo işleme nasıl ele alınacağını hakkında bilgi için veya tablo işlemeye özel olmayan Web işleri SDK'si senaryoları için bkz: [WebJobs SDK ile Azure kuyruk depolama kullanma](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Bu makalede ele alınan konular şunlardır:

* Zaman uyumsuz işlevleri
* Birden çok örneği
* Kapama
* Web işleri SDK'si öznitelikleri bir işlev gövdesine kullanın
* Kod içinde SDK bağlantı dizelerini ayarlayın
* Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama
* Tetik el ile bir işlevi
* Günlüklerini yazma

## <a id="nextsteps"></a> Sonraki adımlar
Bu kılavuz, Azure tabloları ile çalışmak için genel senaryolar nasıl ele alınacağını gösteren kod örnekleri sağlamıştır. Azure Web işleri ve WebJobs SDK nasıl kullanılacağı hakkında daha fazla bilgi için bkz: [Azure Web işleri önerilen kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).

