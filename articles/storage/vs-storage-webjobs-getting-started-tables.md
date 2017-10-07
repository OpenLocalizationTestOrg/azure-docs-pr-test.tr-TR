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
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a>Azure ile çalışmaya başlama depolama (Azure Web işi projeler)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Genel Bakış
Bu makalede gösteren C# kod örnekleri Göster nasıl toouse hello Azure WebJobs SDK sürüm sağlar 1.x hello Azure tablo depolama hizmeti ile. Merhaba kod örnekleri kullanır hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) sürüm 1.x.

Hello Azure Table depolama hizmeti toostore büyük miktarlarda yapılandırılmış veri sağlar. Merhaba, iç ve dış hello Azure bulut gelen kimliği doğrulanmış çağrıları kabul eden bir NoSQL veri deposu hizmetidir. Azure tabloları, yapılandırılmış ve ilişkisel olmayan verilerin depolanması için idealdir.  Bkz: [.NET kullanarak Azure Table storage'ı kullanmaya başlama](storage-dotnet-how-to-use-tables.md#create-a-table) daha fazla bilgi için.

Merhaba kod parçacıkları bazıları hello Göster **tablo** el ile diğer bir deyişle, hello tetikleyici özniteliklerinden biri kullanılarak değil çağrılır işlevlerde kullanılan öznitelik.

## <a name="how-tooadd-entities-tooa-table"></a>Nasıl tooadd varlıklar tooa tablosu
tooadd varlıklar tooa tablo, kullanım hello **tablo** ile öznitelik bir **ICollector<T>**  veya **IAsyncCollector<T>**  parametresi nerede **T** hello şema belirtir hello varlıklarının tooadd istiyor. Merhaba öznitelik oluşturucunun hello Merhaba tablonun adını belirten bir dize parametresi alan.

Merhaba aşağıdaki kod örneği ekler **kişi** adlı varlıklar tooa tablo *giriş*.

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

Genellikle, kullandığınız ile türünün hello **ICollector** türetilen **TableEntity** veya uygulayan **ITableEntity**, ancak gerekli değildir. Merhaba aşağıdakilerden birini **kişi** hello önceki gösterilen hello kodu ile çalışma sınıfları **giriş** yöntemi.

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

Ekleyebileceğiniz hello Azure storage API'si ile doğrudan toowork isterseniz, bir **CloudStorageAccount** parametre toohello yöntemi imzası.

## <a name="real-time-monitoring"></a>Gerçek zamanlı izleme
Veri giriş işlevleri genellikle büyük miktarda veriyi işlemek için hello Web işleri SDK'si Pano gerçek zamanlı izleme verileri sağlar. Merhaba **çağırma günlüğü** bölüm bildirir hello işlevi halen çalışmakta olup olmadığını.

![Çalışan giriş işlevi](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

Merhaba **çağırma ayrıntıları** Raporları Sayfası hello işlevin ilerleme durumu (yazılmış varlıkların sayısı) çalıştıran ve bir fırsat tooabort verir ancak onu.

![Çalışan giriş işlevi](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

Merhaba işlevi tamamlandığında, hello **çağırma ayrıntıları** Raporları Sayfası hello yazılmış satırların sayısı.

![Tamamlanmış Giriş işlevi](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a>Nasıl tooread bir tablodaki birden çok varlık
tooread bir tablo kullanmak hello **tablo** ile öznitelik bir **Iqueryable<T>**  parametresi girildiği **T** türetilen **TableEntity**veya uygulayan **ITableEntity**.

Merhaba aşağıdaki kod örneği okur ve tüm satırları hello günlüklerini **giriş** tablosu:

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

### <a name="how-tooread-a-single-entity-from-a-table"></a>Nasıl tooread bir tablodaki tek bir varlık
Var olan bir **tablo** öznitelik oluşturucunun toobind tooa tek tablo varlığı istediğinizde hello bölüm anahtarı ve satır anahtarını belirtmenize olanak sağlayan iki ek parametrelere sahip.

Merhaba aşağıdaki kod örneği okuyan bir tablo satır için bir **kişi** bir kuyruk iletisi alınan bölüm anahtarını ve satır anahtarı değerleri temel varlık:  

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


Merhaba **kişi** sınıfı bu örnekte tooimplement yok **ITableEntity**.

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a>Nasıl toouse hello .NET depolama API doğrudan toowork bir tablo ile
Merhaba de kullanabilirsiniz **tablo** ile öznitelik bir **CloudTable** nesne bir tablo ile çalışma daha fazla esneklik için.

Merhaba aşağıdaki kod örneği kullanan bir **CloudTable** tooadd tek bir varlık toohello nesne *giriş* tablo.

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

Hakkında daha fazla bilgi için toouse hello **CloudTable** nesne için bkz: [.NET kullanarak Azure Table storage'ı kullanmaya başlama](storage-dotnet-how-to-use-tables.md).

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a>Merhaba sıraları nasıl-tooarticle tarafından kapsanan ilgili konular
Nasıl toohandle tablo işleme bir kuyruk iletisi tarafından veya WebJobs SDK senaryoları tetiklenen değil hakkında bilgi için işleme, özel tootable bakın [bağlı Hizmetleri (Web işi projeleri) Azure kuyruk depolama ve Visual Studio ile çalışmaya başlama ](vs-storage-webjobs-getting-started-queues.md).

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede kod sağlamıştır gösteren nasıl örnekleri Azure tabloları ile çalışmak için genel senaryolar toohandle. Toouse Azure Web işleri ve hello Web işleri SDK'si nasıl görürüm hakkında daha fazla bilgi için [Azure Web işleri belge kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).

