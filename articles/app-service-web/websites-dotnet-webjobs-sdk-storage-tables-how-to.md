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
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a>Nasıl toouse Azure tablo depolama hello WebJobs SDK ile
## <a name="overview"></a>Genel Bakış
Bu kılavuz C# kod örnekleri nasıl tooread ve yazma Azure depolama tabloları kullanarak gösteren sağlar [WebJobs SDK](websites-dotnet-webjobs-sdk.md) sürüm 1.x.

Merhaba Kılavuzu varsayar bildiğiniz [nasıl toocreate bağlantısı ile Visual Studio'da bir Web işi projesi bu noktası tooyour depolama hesabı dizeleri](websites-dotnet-webjobs-sdk-get-started.md) veya çok[birden çok depolama hesabı](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

Merhaba kod parçacıkları bazıları hello Göster `Table` olan işlevlerde kullanılan öznitelik [el ile olarak adlandırılan](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), diğer bir deyişle, birini kullanarak hello tetikleyici öznitelikleri değil. 

## <a id="ingress"></a>Nasıl tooadd varlıklar tooa tablosu
tooadd varlıklar tooa tablo, kullanım hello `Table` ile öznitelik bir `ICollector<T>` veya `IAsyncCollector<T>` parametresi nerede `T` hello şema belirtir hello varlıklarının tooadd istiyor. Merhaba öznitelik oluşturucunun hello Merhaba tablonun adını belirten bir dize parametresi alan. 

Merhaba aşağıdaki kod örneği ekler `Person` adlı varlıklar tooa tablo *giriş*.

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

Genellikle, kullandığınız ile türünün hello `ICollector` türetilen `TableEntity` veya uygulayan `ITableEntity`, ancak gerekli değildir. Merhaba aşağıdakilerden birini `Person` hello önceki gösterilen hello kodu ile çalışma sınıfları `Ingress` yöntemi.

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

Ekleyebileceğiniz hello Azure storage API'si ile doğrudan toowork isterseniz, bir `CloudStorageAccount` parametre toohello yöntemi imzası.

## <a id="monitor"></a>Gerçek zamanlı izleme
Veri giriş işlevleri genellikle büyük miktarda veriyi işlemek için hello Web işleri SDK'si Pano gerçek zamanlı izleme verileri sağlar. Merhaba **çağırma günlüğü** bölüm bildirir hello işlevi halen çalışmakta olup olmadığını.

![Çalışan giriş işlevi](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

Merhaba **çağırma ayrıntıları** Raporları Sayfası hello işlevin ilerleme durumu (yazılmış varlıkların sayısı) çalıştıran ve bir fırsat tooabort verir ancak onu. 

![Çalışan giriş işlevi](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

Merhaba işlevi tamamlandığında, hello **çağırma ayrıntıları** Raporları Sayfası hello yazılmış satırların sayısı.

![Tamamlanmış Giriş işlevi](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <a id="multiple"></a>Nasıl tooread bir tablodaki birden çok varlık
tooread bir tablo kullanmak hello `Table` ile öznitelik bir `IQueryable<T>` parametresi girildiği `T` türetilen `TableEntity` veya uygulayan `ITableEntity`.

Merhaba aşağıdaki kod örneği okur ve tüm satırları hello günlüklerini `Ingress` tablosu:

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

### <a id="readone"></a>Nasıl tooread bir tablodaki tek bir varlık
Var olan bir `Table` öznitelik oluşturucunun toobind tooa tek tablo varlığı istediğinizde hello bölüm anahtarı ve satır anahtarını belirtmenize olanak sağlayan iki ek parametrelere sahip.

Merhaba aşağıdaki kod örneği okuyan bir tablo satır için bir `Person` bir kuyruk iletisi alınan bölüm anahtarını ve satır anahtarı değerleri temel varlık:  

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


Merhaba `Person` sınıfı bu örnekte tooimplement yok `ITableEntity`.

## <a id="storageapi"></a>Nasıl toouse hello .NET depolama API doğrudan toowork bir tablo ile
Merhaba de kullanabilirsiniz `Table` ile öznitelik bir `CloudTable` nesne bir tablo ile çalışma daha fazla esneklik için.

Merhaba aşağıdaki kod örneği kullanan bir `CloudTable` tooadd tek bir varlık toohello nesne *giriş* tablo. 

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

Hakkında daha fazla bilgi için toouse hello `CloudTable` nesne için bkz: [nasıl toouse .NET tablo depolamasından](../cosmos-db/table-storage-how-to-use-dotnet.md). 

## <a id="queues"></a>Merhaba sıraları nasıl-tooarticle tarafından kapsanan ilgili konular
Nasıl toohandle tablo işleme bir kuyruk iletisi tarafından veya WebJobs SDK senaryoları tetiklenen değil hakkında bilgi için işleme, özel tootable bakın [nasıl toouse Azure kuyruk depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Bu makalede ele alınan konular hello şunları içerir:

* Zaman uyumsuz işlevleri
* Birden çok örneği
* Kapama
* Web işleri SDK'si özniteliklerini işlevinin hello gövdesindeki kullanın
* Kod içinde Hello SDK bağlantı dizelerini ayarlayın
* Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama
* Tetik el ile bir işlevi
* Günlüklerini yazma

## <a id="nextsteps"></a> Sonraki adımlar
Bu kılavuz kodu sağlamıştır gösteren nasıl örnekleri Azure tabloları ile çalışmak için genel senaryolar toohandle. Toouse Azure Web işleri ve hello Web işleri SDK'si nasıl görürüm hakkında daha fazla bilgi için [Azure Web işleri önerilen kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).

