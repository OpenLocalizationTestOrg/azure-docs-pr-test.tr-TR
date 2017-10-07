---
title: aaaHow toouse hello WebJobs SDK ile Azure kuyruk depolama
description: "Nasıl toouse Azure kuyruk depolama hello WebJobs SDK ile bilgi edinin. Oluşturma ve kuyrukları silin; Ekle, Gözat, Al ve iletileri kuyruğa ve daha fazlasını silin."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: dbfac5d9-f4a0-4e3e-9ecc-af3d7bf80463
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 49f844436b0453489800b2762a5c7dc30b9db805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-queue-storage-with-hello-webjobs-sdk"></a>Nasıl toouse Azure kuyruk depolama hello WebJobs SDK ile
## <a name="overview"></a>Genel Bakış
Bu kılavuz, nasıl toouse hello Azure WebJobs SDK sürüm gösteren C# kod örnekleri sağlar 1.x hello Azure kuyruk depolama hizmeti ile.

Merhaba Kılavuzu varsayar bildiğiniz [nasıl toocreate bağlantısı ile Visual Studio'da bir Web işi projesi bu noktası tooyour depolama hesabı dizeleri](websites-dotnet-webjobs-sdk-get-started.md) veya çok[birden çok depolama hesabı](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

Merhaba kod parçacıkları çoğunu İşlevler, yalnızca Göster hello oluşturan kodunu hello değil `JobHost` nesne bu örnekte olduğu gibi:

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

Aşağıdaki konularda hello Hello kılavuz içerir:

* [Nasıl tootrigger bir kuyruk iletisi alındığında işlevi](#trigger)
  * Dize iletileri
  * POCO iletileri
  * Zaman uyumsuz işlevleri
  * Türleri hello QueueTrigger özniteliği birlikte çalışır.
  * Yoklama algoritması
  * Birden çok örneği
  * Paralel yürütme
  * Sıra veya sıra ileti meta verileri alma
  * Kapama
* [Toocreate bir kuyruk iletisi nasıl bir kuyruk iletisi işlenirken](#createqueue)
  * Dize iletileri
  * POCO iletileri
  * Birden çok iletileri oluşturmak veya zaman uyumsuz işlevleri
  * Türleri hello sıra özniteliği birlikte çalışır.
  * Web işleri SDK'si özniteliklerini işlevinin hello gövdesindeki kullanın
* [Tooread ve yazma BLOB nasıl bir kuyruk iletisi işlenirken](#blobs)
  * Dize iletileri
  * POCO iletileri
  * Türleri hello Blob özniteliği birlikte çalışır.
* [Nasıl toohandle zehirli ileti](#poison)
  * Otomatik zehirli ileti işleme
  * El ile zehirli ileti işleme
* [Nasıl tooset yapılandırma seçenekleri](#config)
  * Kod içinde SDK bağlantı dizelerini ayarlayın
  * QueueTrigger ayarlarını yapılandırma
  * Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama
* [Nasıl tootrigger bir işlev el ile](#manual)
* [Toowrite nasıl kaydeder](#logs)
* [Nasıl toohandle hataları ve zaman aşımları yapılandırın](#errors)
* [Sonraki adımlar](#nextsteps)

## <a id="trigger"></a>Nasıl tootrigger bir kuyruk iletisi alındığında işlevi
toowrite Web işleri SDK'si hello işlevi çağıran bir kuyruk iletisi alındığında, hello kullan `QueueTrigger` özniteliği. Hello özniteliği Oluşturucusu hello sıra toopoll hello adını belirten bir dize parametresi alan. Ayrıca [hello sıra adı dinamik olarak ayarlamak](#config).

### <a name="string-queue-messages"></a>Dize iletileri
Bir dize ileti hello sıra aşağıdaki örneğine hello, bu nedenle içeren `QueueTrigger` adlı uygulanan tooa dize parametresi `logMessage` hello kuyruk iletisi Merhaba içeriğine içerir. Merhaba işlevi [bir günlük iletisi toohello Pano Yazar](#logs).

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

Yanında `string`, hello parametresi bir bayt dizisi olabilir bir `CloudQueueMessage` nesne ya da tanımladığınız bir POCO.

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) kuyruk iletileri
Aşağıdaki örneğine hello, JSON hello kuyruk iletisi içeren bir `BlobInformation` içeren nesne bir `BlobName` özelliği. Merhaba SDK otomatik olarak hello nesne seri durumdan çıkarır.

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Merhaba SDK kullanan hello [Newtonsoft.Json NuGet paketi](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize ve iletileri seri durumdan. Merhaba WebJobs SDK kullanmayan bir programda iletileri kuyruğa oluşturursanız, SDK ayrıştıramıyor bu hello hello örnek toocreate bir POCO kuyruk iletisi aşağıdaki gibi kod yazabilirsiniz.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a>Zaman uyumsuz işlevleri
Async işlevi aşağıdaki hello [günlük toohello Pano Yazar](#logs).

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

Zaman uyumsuz işlevleri sürebilir bir [iptal belirteci](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken)hello blob kopyaladığı örnek aşağıdaki gösterildiği gibi. (Merhaba açıklaması için `queueTrigger` yer tutucu hello bkz [BLOB'lar](#blobs) bölüm.)

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <a id="qtattributetypes"></a>Türleri hello QueueTrigger özniteliği birlikte çalışır.
Kullanabileceğiniz `QueueTrigger` şu türlerini hello ile:

* `string`
* JSON olarak serileştirilen bir POCO türü
* `byte[]`
* `CloudQueueMessage`

### <a id="polling"></a>Yoklama algoritması
Merhaba SDK boşta kuyruk depolama işlem maliyetleri yoklama rasgele üstel geri alma algoritması tooreduce hello etkisini uygular.  Bir ileti bulunduğunda, hello SDK iki saniye bekler ve ardından başka bir ileti için denetler; bir ileti bulunduğunda yeniden denemeden önce yaklaşık dört saniye bekler. Merhaba maksimum bekleme süresi, ulaşana kadar sonraki başarısız denemeler tooget bir kuyruk iletisi sonra hello bekleme süresi tooincrease devam eder. hangi Varsayılanları tooone minute. [Merhaba maksimum bekleme süresi yapılandırılabilir](#config).

### <a id="instances"></a>Birden çok örneği
Web uygulamanız birden çok örneği üzerinde çalışıyorsa, bir sürekli Webjob'un her makinede çalışır ve her makine için Tetikleyicileri bekleyin ve toorun işlevlerini deneyin. Merhaba WebJobs SDK sıra tetikleyici otomatik olarak bir işlev bir kuyruk iletisi birden çok kez önlediği; İşlevler toobe ıdempotent yazılmış toobe gerekmez. Ancak, tooensure istiyorsanız bile hello ana web uygulamanızın birden fazla örneği bulunduğunda bir işlevi yalnızca bir örneğini çalıştıran, hello kullanabilirsiniz `Singleton` özniteliği.

### <a id="parallel"></a>Paralel yürütme
Birden çok işlevler farklı sıralarda dinleme varsa, iletileri aynı anda alındığında hello SDK bunları paralel olarak çağırın.

tek bir kuyruk için birden fazla ileti alındığında hello aynı durum geçerlidir. Varsayılan olarak, hello SDK 16 iletileri kuyruğa toplu bir zaman alır ve paralel olarak işler hello işlevi yürütür. [Merhaba toplu iş boyutu Dur yapılandırılabilir](#config). İşlenmekte olan hello numarası hello toplu iş boyutu toohalf aldığında hello SDK başka bir toplu iş alır ve bu iletileri işleme başlatır. Bu nedenle hello en fazla eş zamanlı ileti işlevi işlenen sayısı bir ve yarı kez bir hello toplu iş boyutu dur. Bu sınır olan tooeach işlev ayrı ayrı uygular bir `QueueTrigger` özniteliği.

Paralel yürütme üzerinde bir Sıraya alınan iletileri istemiyorsanız hello toplu iş boyutu too1 ayarlayabilirsiniz. Ayrıca bkz. **sırası işleme üzerinde daha fazla denetim** içinde [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).

### <a id="queuemetadata"></a>Sıra veya sıra ileti meta verileri alma
Aşağıdaki ileti özelliklere parametreleri toohello yöntemi imza ekleyerek hello alabilirsiniz:

* `DateTimeOffset`expirationTime
* `DateTimeOffset`insertionTime
* `DateTimeOffset`nextVisibleTime
* `string`queueTrigger (ileti metni içerir)
* `string`Kimliği
* `string`popReceipt
* `int`dequeueCount

Hello Azure storage API'si ile doğrudan toowork isterseniz, ayrıca ekleyebileceğiniz bir `CloudStorageAccount` parametresi.

Merhaba aşağıdaki örnekte tüm bu meta verileri tooan bilgisi uygulama günlüğüne yazar. Merhaba örnekte hello kuyruk iletisi Merhaba içeriğine logMessage ve queueTrigger içerir.

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

Merhaba örnek kodu ile yazılmış bir örnek günlük şöyledir:

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <a id="graceful"></a>Kapama
Sürekli bir WebJob içinde çalışan bir işlevinin kabul edebileceği bir `CancellationToken` hello işletim sistemi toonotify hello işlevi hello zaman sağlayan Web işi parametredir hakkında toobe sonlandırıldı. Bu bildirim toomake hello beklenmedik bir şekilde veri tutarsız bir durumda bırakır şekilde sonlandırma işlevi değil emin kullanabilirsiniz.

örnekte gösterildiği nasıl aşağıdaki hello toocheck bir işlevdeki yaklaşan WebJob sonlandırma için.

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

**Not:** hello Pano hello durumunu ve çıkışını kapatılmışsa işlevlerin doğru şekilde göstermeyebilir.

Daha fazla bilgi için bkz: [Web işleri normal şekilde kapatılmasını](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).   

## <a id="createqueue"></a>Toocreate bir kuyruk iletisi nasıl bir kuyruk iletisi işlenirken
Yeni bir kuyruk iletisi kullanım hello oluşturan bir işlev toowrite `Queue` özniteliği. Gibi `QueueTrigger`, hello kuyruk adı bir dize olarak geçirin veya yapabilecekleriniz [hello sıra adı dinamik olarak ayarlamak](#config).

### <a name="string-queue-messages"></a>Dize iletileri
zaman uyumsuz olmayan kodu örneği aşağıdaki hello hello kuyruk iletisi olarak içerik aynı "inputqueue" adlı hello sıraya alınan hello hello sırasındaki "outputqueue" adlı yeni bir kuyruk iletisi oluşturur. (İşlevler için async kullanma `IAsyncCollector<T>` daha sonra bu bölümde gösterilen.)

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) kuyruk iletileri
toocreate geçişi hello POCO bir dize yerine bir POCO içeren bir kuyruk iletisi türü bir çıkış parametresi toohello `Queue` özniteliği Oluşturucusu.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

Merhaba SDK hello nesne tooJSON otomatik olarak serileştirir. Merhaba nesnesi boş olsa bile bir kuyruk iletisi her zaman oluşturulur.

### <a name="create-multiple-messages-or-in-async-functions"></a>Birden çok iletileri oluşturmak veya zaman uyumsuz işlevleri
toocreate birden fazla ileti olun hello çıkış sırası için hello parametre türü `ICollector<T>` veya `IAsyncCollector<T>`hello aşağıdaki örnekte gösterildiği gibi.

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Her kuyruk iletisi hemen hello oluşturulduğunda `Add` yöntemi çağrılır.

### <a name="types-that-hello-queue-attribute-works-with"></a>Türleri bu hello sıra özniteliği birlikte çalışır.
Merhaba kullanabilirsiniz `Queue` parametre türleri şu hello özniteliği:

* `out string`(Merhaba işlevi sona erdiğinde parametre değeri null olmayan ise kuyruk iletisi oluşturur)
* `out byte[]`(gibi çalışır `string`)
* `out CloudQueueMessage`(gibi çalışır `string`)
* `out POCO`(serializable bir tür oluşturduğu bir ileti null bir nesne ile Merhaba işlevi sona erdiğinde hello parametre null ise)
* `ICollector`
* `IAsyncCollector`
* `CloudQueue`(el ile hello Azure Storage API'sini kullanarak doğrudan iletileri oluşturmak için)

### <a id="ibinder"></a>Web işleri SDK'si özniteliklerini işlevinin hello gövdesindeki kullanın
Toodo ihtiyacınız varsa bazı, işlevinde bir Web işleri SDK'si öznitelik gibi kullanmadan önce iş `Queue`, `Blob`, veya `Table`, hello kullanabilirsiniz `IBinder` arabirimi.

Aşağıdaki örneğine hello bir giriş sırası iletisi sürer ve aynı bir çıkış sırasının içerik hello ile yeni bir ileti oluşturur. Merhaba çıkış sırası adı hello işlevi hello gövdesinde kodu tarafından ayarlanır.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

Merhaba `IBinder` arabirimi hello ile de kullanılabilir `Table` ve `Blob` öznitelikleri.

## <a id="blobs"></a>Nasıl tooread ve yazma BLOB ve bir sıraya ileti işlenirken tabloları
Merhaba `Blob` ve `Table` öznitelikleri tooread etkinleştirmek ve blobları ve tabloları yazma. Bu bölümdeki Hello örnekler tooblobs uygulayın. BLOB'ları oluşturulduğunda veya güncelleştirilmiş tootrigger nasıl işlediği gösteren kod örnekleri için bkz: [nasıl toouse Azure blob depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)ve okuma ve yazma tabloları kod örnekleri için bkz: [nasıl toouse Azure tablo Depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).

### <a name="string-queue-messages-triggering-blob-operations"></a>Dize iletileri kuyruğa blobu işlemleri tetikleme
Bir dizeyi içeren bir kuyruk iletisi için `queueTrigger` hello kullanabileceğiniz bir yer tutucudur `Blob` özniteliğin `blobPath` selamlama iletisine Merhaba içeriğine içeren parametre.

Merhaba aşağıdaki örnek kullanır `Stream` tooread ve yazma BLOB'lar nesneleri. Merhaba kuyruk iletisi hello textblobs kapsayıcıda bulunan bir blob hello adıdır. Merhaba blob ile bir kopyasını "-Yeni" eklenmiş toohello adı oluşturulduğu hello aynı kapsayıcı.

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Merhaba `Blob` özniteliği Oluşturucusu alır bir `blobPath` hello kapsayıcı ve blob adı belirten parametre. Bu yer tutucu hakkında daha fazla bilgi için bkz: [nasıl toouse Azure blob depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),

Ne zaman hello öznitelik süsler bir `Stream` nesnesi, başka bir oluşturucu parametresini belirtir hello `FileAccess` modu okuma, yazma veya okuma/yazma olarak.

Merhaba aşağıdaki örnek kullanan bir `CloudBlockBlob` toodelete blob nesnesi. Merhaba kuyruk iletisi hello blob hello adıdır.

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a id="pocoblobs"></a>POCO [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) kuyruk iletileri
JSON olarak hello kuyruk iletisi içinde depolanan bir POCO için hello hello nesnesinde özelliklerini adı yer tutucuları kullanabilirsiniz `Queue` özniteliğin `blobPath` parametresi. Aynı zamanda [sıra meta veri özellik adları](#queuemetadata) yer tutucu olarak.

Merhaba aşağıdaki örnek bir blob tooa yeni blob farklı bir uzantı kopyalar. Merhaba kuyruk iletisi bir `BlobInformation` içeren nesnesinin `BlobName` ve `BlobNameWithoutExtension` özellikleri. Merhaba özellik adları olarak kullanılan hello blob yolu yer tutucuları Merhaba `Blob` öznitelikleri.

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Merhaba SDK kullanan hello [Newtonsoft.Json NuGet paketi](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize ve iletileri seri durumdan. Merhaba WebJobs SDK kullanmayan bir programda iletileri kuyruğa oluşturursanız, SDK ayrıştıramıyor bu hello hello örnek toocreate bir POCO kuyruk iletisi aşağıdaki gibi kod yazabilirsiniz.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

Bazı iş toodo, bir blob tooan nesnesi bağlama önce işlevinde gerekiyorsa hello işlevi hello gövdesinde hello özniteliğini kullanabilirsiniz [hello sıra özniteliği için daha önce gösterildiği gibi](#ibinder).

### <a id="blobattributetypes"></a>Merhaba kullanabileceğiniz türü özniteliğiyle Blob
Merhaba `Blob` özniteliği şu türlerini hello ile kullanılabilir:

* `Stream`(okuma veya yazma, hello FileAccess Oluşturucu parametresi kullanılarak belirtilen)
* `TextReader`
* `TextWriter`
* `string`(okuma)
* `out string`(yazma; hello işlevi döndüğünde yalnızca hello dizesi parametresi null olmayan ise bir blob oluşturur)
* POCO (okuma)
* POCO out (yazma; her zaman bir blob oluşturur, hello işlevi döndüğünde POCO parametre null ise null nesnesi olarak oluşturur)
* `CloudBlobStream`(yazma)
* `ICloudBlob`(okuma veya yazma)
* `CloudBlockBlob`(okuma veya yazma)
* `CloudPageBlob`(okuma veya yazma)

## <a id="poison"></a>Nasıl toohandle zehirli ileti
İçerikleri işlevi toofail neden olan iletileri çağrılır *zehirli ileti*. Merhaba işlevi başarısız olduğunda, hello kuyruk iletisi silinmez ve sonunda yeniden neden hello döngüsü toobe yinelenen kayıt. otomatik olarak hello döngüsü Hello SDK sınırlı sayıda yineleme sonra kesintiye uğratabilir veya el ile yapabilirsiniz.

### <a name="automatic-poison-message-handling"></a>Otomatik zehirli ileti işleme
Merhaba SDK too5 kez tooprocess bir kuyruk iletisi yukarı işlevi çağırır. Merhaba beşinci deneme başarısız olursa, selamlama iletisine taşınan tooa zararlı sıradır. [Merhaba en fazla yeniden deneme sayısı yapılandırılabilir](#config).

Merhaba zararlı sıra adlandırılan *{originalqueuename}*-zararlı. Bir işlev tooprocess iletileri hello zararlı sıradan günlüğe yazma veya el ile ilgilenilmesi gereken bir bildirim göndererek yazabilirsiniz.

Aşağıdaki örnek hello hello içinde `CopyBlob` bir kuyruk iletisi mevcut olmayan bir blob hello adını içerdiğinde işlevi başarısız olur. Bu durum oluştuğunda selamlama iletisine hello copyblobqueue sıra toohello copyblobqueue poison sıradan taşınır. Merhaba `ProcessPoisonMessage` zehir iletisi günlükleri hello sonra.

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed toocopy blob, name=" + blobName);
        }

zararlı bir ileti işlendiğinde hello aşağıda bu işlevler konsol çıktısı gösterilmektedir.

![Zehirli ileti işleme için konsol çıkışı](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a>El ile zehirli ileti işleme
Hello sayısı bir ileti toplanma işleme ekleyerek alabileceğiniz bir `int` adlı parametre `dequeueCount` tooyour işlevi. Bundan sonra onay hello işlev kodu sayıma dequeue ve hello sayısı hello aşağıdaki örnekte gösterildiği gibi bir eşiği aştığında kendi zehirli ileti işleme gerçekleştirmek kullanabilirsiniz.

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed toocopy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a id="config"></a>Nasıl tooset yapılandırma seçenekleri
Merhaba kullanabilirsiniz `JobHostConfiguration` yapılandırma seçenekleri aşağıdaki türü tooset hello:

* Kodda Hello SDK bağlantı dizelerini ayarlayın.
* Yapılandırma `QueueTrigger` maksimum gibi ayarları dequeue sayısı.
* Sıra adları yapılandırmasından alın.

### <a id="setconnstr"></a>Kod içinde SDK bağlantı dizelerini ayarlayın
Kodda Hello SDK bağlantı dizelerini ayarlama, toouse kendi bağlantı dizesi adlarında yapılandırma dosyalarının veya ortam değişkenleri hello aşağıdaki örnekte gösterildiği gibi sağlar.

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a id="configqueue"></a>QueueTrigger ayarlarını yapılandırma
Toohello sıraya ileti işleme uygulanan ayarları aşağıdaki hello yapılandırabilirsiniz:

* Merhaba en fazla eşzamanlı olarak paralel olarak yürütülen toobe yukarı çekilen sıraya ileti sayısı (varsayılan olarak 16).
* bir kuyruk iletisi tooa zararlı sıra gönderilmeden önce yeniden deneme sayısı Hello (varsayılan olarak 5).
* bir sıranın boş olduğunda yeniden yoklama önce hello maksimum bekleme süresi (varsayılan değer 1 dakika).

örnekte gösterildiği nasıl aşağıdaki hello tooconfigure bu ayarları:

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a id="setnamesincode"></a>Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama
Kuyruk adı, bir blob adı veya kapsayıcı toospecify bazen istediğiniz veya bir tablo adı kod sabit kodlu yerine onu. Örneğin, toospecify hello sıra adı için isteyebilirsiniz `QueueTrigger` bir yapılandırma dosyası veya ortam değişkeninde.

Bunu geçirerek yapabilirsiniz bir `NameResolver` toohello nesne `JobHostConfiguration` türü. Web işleri SDK'si özniteliği Oluşturucusu parametrelerinde yüzde (%) işareti tarafından çevrelenen özel yer tutucular içerir ve `NameResolver` kod bu yer tutucular yerine kullanılan hello gerçek değerler toobe belirtir.

Örneğin, toouse istediğinizi düşünelim bir sıra hello test ortamında logqueuetest ve üretimde bir adlandırılmış logqueueprod adlı. Sabit kodlanmış kuyruk adı yerine bir girişe hello toospecify hello adı istediğiniz `appSettings` hello gerçek sıra adı olurdu koleksiyonu. Merhaba, `appSettings` anahtarı logqueue, işlevinizi aşağıdaki örneğine hello gibi görünebilir.

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

`NameResolver` Sınıfını hello sıra adından sonra almak `appSettings` hello aşağıdaki örnekte gösterildiği gibi:

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

Merhaba geçirdiğiniz `NameResolver` toohello sınıfında `JobHost` nesne hello aşağıdaki örnekte gösterildiği gibi.

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

**Not:** kuyruk, tablo ve blob adları çözümlenmiş her zaman bir işlev çağrılır, ancak blob kapsayıcı adları yalnızca Merhaba uygulaması başladığında çözümlenir. Merhaba iş çalışırken blob kapsayıcı adı değiştirilemiyor.

## <a id="manual"></a>Nasıl tootrigger bir işlev el ile
tootrigger işlevi el ile Merhaba kullanmak `Call` veya `CallAsync` hello yöntemi `JobHost` nesne ve hello `NoAutomaticTrigger` hello aşağıdaki örnekte gösterildiği gibi hello işlevi üzerinde özniteliği.

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <a id="logs"></a>Toowrite nasıl kaydeder
Başlangıç Panosu iki yerde günlükleri gösterir: hello sayfası hello Web işi için ve belirli bir Web işi çağırma için hello sayfası.

![Web işi sayfasındaki günlükleri](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![İşlev çağırma sayfasındaki günlükleri](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

Bir işlev veya hello çağıran konsol yöntemlerini çıkışı `Main()` yöntemi görünür hello Web işi için hello Pano sayfası, belirli yöntem çağırma için hello sayfasındaki değil. Çıktı yöntemi imzanız bir parametresinden alma hello TextWriter nesneden bir yöntem çağırma için hello Pano sayfası görünür.

Konsol çıktısı, bağlantılı tooa belirli yöntemi çağırma olamaz, hello konsol birçok iş işlevlerinin hello çalışmıyor olabilir tek iş parçacıklı, olduğu için aynı anda. İşte bu nedenle hello SDK her işlev çağrısını kendi benzersiz günlük yazıcı nesnesi ile sağlar.

toowrite [uygulama izleme günlükleri](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), kullanın `Console.Out` (bilgisi olarak işaretlenmiş günlükleri oluşturur) ve `Console.Error` (hata olarak işaretlenmiş günlükleri oluşturur). Toouse alternatiftir [izleme veya TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), uyarı, ayrıntı sağlar ve kritik düzeyleri toplama tooInfo ve hata. Azure web uygulamanızı nasıl yapılandırdığınıza bağlı olarak Azure BLOB veya uygulama izleme günlükleri hello web uygulama günlük dosyalarında Azure tabloları görünür. Tüm konsol çıktısı doğru olduğu gibi hello en son 100 uygulama günlüklerini da hello Web işi, olmayan bir işlev çağrısını hello sayfasını için hello Pano sayfası görünür.

Merhaba hello programı yerel olarak çalışmıyorsa hello program bir Azure WebJob içinde yalnızca çalışıyorsa, Pano veya başka bir ortamında konsol çıktısı görüntülenir.

Yüksek verimlilik senaryolar için panoyu günlüğü devre dışı bırakın. Varsayılan olarak, günlükler toostorage hello SDK yazar ve birçok iletilerini işlerken bu etkinliği performansının düşmesine neden. Günlük, toodisable hello aşağıdaki örnekte gösterildiği gibi hello Pano bağlantı dizesi toonull ayarlayın.

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

Merhaba aşağıdaki örnekte çeşitli yollar gösterir toowrite günlükleri:

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

Hello WebJobs SDK Pano, hello hello çıktısını `TextWriter` toohello sayfa belirli bir zaman gittiğiniz yukarı gösterir işlev çağırma ve tıklatın nesnesi **geçiş çıktı**:

![İşlev çağırma bağlantısına tıklayın](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![İşlev çağırma sayfasındaki günlükleri](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

Merhaba WebJob (değil hello işlev çağrısını) için toohello sayfasına gidin ve'ı tıklattığınızda hello WebJobs SDK Pano, konsolunun hello en son 100 satırları göster yukarı çıktı **geçiş çıktı**.

![Çıkışı Aç/Kapat'ı tıklatın](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

Bir sürekli Webjob'un uygulama günlüklerini/data/işleri/sürekli/içinde gösterilmesi*{webjobname}*hello web uygulama dosya sisteminde /job_log.txt.

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

Azure blob hello uygulamada günlükleri şuna benzeyebilir: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Merhaba Dünya!, 2014-09-26T21:01:13, hata, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.Error - Merhaba Dünya!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Merhaba Dünya!,

Ve Azure tablo hello `Console.Out` ve `Console.Error` günlükleri şuna benzeyebilir:

![Tablo bilgi günlüğüne](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Hata günlüğü tablosundaki](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

Kendi Günlükçü tooplug istiyorsanız, bkz: [Bu örnek](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).

## <a id="errors"></a>Nasıl toohandle hataları ve zaman aşımları yapılandırın
Merhaba WebJobs SDK de içeren bir [zaman aşımı](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) işlevi toobe iptal varsa toocause kullanabileceğiniz öznitelik belirtilen sürede tamamlamak değil. Belirtilen bir süre içinde çok fazla hata oluştuğunda tooraise bir uyarı istiyorsanız, hello kullanabileceğiniz `ErrorTrigger` özniteliği. Burada bir [ErrorTrigger örnek](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    too= "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors toohello Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

Ayrıca dinamik olarak devre dışı bırakın ve bunlar, bir uygulama ayarı veya ortam değişkeni adı olabilir bir yapılandırma anahtarı kullanarak tetiklenebilir olup olmadığını işlevleri toocontrol etkinleştirin. Merhaba örnek kod için bkz: `Disable` özniteliğini [hello Web işleri SDK'si örnekleri depo](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).

## <a id="nextsteps"></a> Sonraki adımlar
Bu kılavuz kodu sağlamıştır gösteren nasıl örnekleri Azure kuyruklarla çalışmaya yönelik yaygın senaryolar toohandle. Toouse Azure Web işleri ve hello Web işleri SDK'si nasıl görürüm hakkında daha fazla bilgi için [Azure Web işleri önerilen kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).
