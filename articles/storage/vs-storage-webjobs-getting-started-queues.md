---
title: "aaaGetting, bağlı hizmetler (Web işi projeleri) kuyruk depolama ve Visual Studio ile çalışmaya | Microsoft Docs"
description: "Visual Studio kullanarak tooa depolama hesabı bağlanma Hizmetleri bağlandıktan sonra bir Web işi projesinin Azure kuyruk depolama kullanarak nasıl tooget başlatıldı."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 720e96fda734c31e1b1d68d4f95aa9531a20a3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a>Azure kuyruk depolama ve Visual Studio ile çalışmaya başlama bağlı Hizmetleri (Web işi projeler)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Genel Bakış
Bu makalede nereden Azure kuyruk kullanmaya oluşturduğunuz veya Azure storage hesabı kullanarak başvurulan sonra Visual Studio Azure WebJob projesinde depolama hello Visual Studio **bağlı Hizmetleri Ekle** iletişim kutusu. Merhaba Visual Studio kullanarak bir depolama hesabı tooa Web işi projesinin eklediğinizde **bağlı Hizmetleri Ekle** iletişim kutusunda, hello uygun Azure depolama NuGet paketleri yüklenir, hello uygun .NET başvuruları eklenen toohello Proje ve hello depolama hesabı için bağlantı dizelerini hello App.config dosyasında güncelleştirilir.  

Bu makalede nasıl toouse hello Azure WebJobs SDK sürüm gösteren C# kod örnekleri sağlar 1.x hello Azure kuyruk depolama hizmeti ile.

Azure kuyruk depolama alanından herhangi bir yere Merhaba Dünya HTTP veya HTTPS kullanarak kimlik doğrulaması yapılmış çağrılar aracılığıyla erişilebilen iletileri çok sayıda depolamak için bir hizmettir. Tek bir kuyruk iletisinin boyutu too64 KB yukarı olabilir ve bir kuyruk iletileri, bir depolama hesabı toohello toplam kapasite sınırına milyonlarca içerebilir. Bkz: [.NET kullanarak Azure kuyruk depolama ile çalışmaya başlama](storage-dotnet-how-to-use-queues.md) daha fazla bilgi için. ASP.NET hakkında daha fazla bilgi için bkz: [ASP.NET](http://www.asp.net).

## <a name="how-tootrigger-a-function-when-a-queue-message-is-received"></a>Nasıl tootrigger bir kuyruk iletisi alındığında işlevi
toowrite Web işleri SDK'si hello işlevi çağıran bir kuyruk iletisi alındığında, hello kullan **QueueTrigger** özniteliği. Hello özniteliği Oluşturucusu hello sıra toopoll hello adını belirten bir dize parametresi alan. toosee tooset hello nasıl sıra adı dinamik olarak kullanıma [nasıl tooset yapılandırma seçenekleri](#how-to-set-configuration-options).

### <a name="string-queue-messages"></a>Dize iletileri
Bir dize ileti hello sıra aşağıdaki örneğine hello, bu nedenle içeren **QueueTrigger** adlı uygulanan tooa dize parametresi **logMessage** hello kuyruk iletisi Merhaba içeriğine içerir. Merhaba işlevi [bir günlük iletisi toohello Pano Yazar](#how-to-write-logs).

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

Yanında **dize**, hello parametresi bir bayt dizisi olabilir bir **CloudQueueMessage** nesne ya da tanımladığınız bir POCO.

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) kuyruk iletileri
Aşağıdaki örneğine hello, JSON hello kuyruk iletisi içeren bir **BlobInformation** içeren nesne bir **BlobName** özelliği. Merhaba SDK otomatik olarak hello nesne seri durumdan çıkarır.

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Merhaba SDK kullanan hello [Newtonsoft.Json NuGet paketi](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize ve iletileri seri durumdan. Merhaba WebJobs SDK kullanmayan bir programda iletileri kuyruğa oluşturursanız, SDK ayrıştıramıyor bu hello hello örnek toocreate bir POCO kuyruk iletisi aşağıdaki gibi kod yazabilirsiniz.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a>Zaman uyumsuz işlevleri
Async işlevi aşağıdaki hello [günlük toohello Pano Yazar](#how-to-write-logs).

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

Zaman uyumsuz işlevleri sürebilir bir [iptal belirteci](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken)hello blob kopyaladığı örnek aşağıdaki gösterildiği gibi. (Merhaba açıklaması için **queueTrigger** yer tutucu hello bkz [BLOB'lar](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) bölüm.)

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-hello-queuetrigger-attribute-works-with"></a>Türleri hello QueueTrigger özniteliği birlikte çalışır.
Kullanabileceğiniz **QueueTrigger** şu türlerini hello ile:

* **dize**
* JSON olarak serileştirilen bir POCO türü
* **byte]**
* **CloudQueueMessage**

## <a name="polling-algorithm"></a>Yoklama algoritması
Merhaba SDK boşta kuyruk depolama işlem maliyetleri yoklama rasgele üstel geri alma algoritması tooreduce hello etkisini uygular.  Bir ileti bulunduğunda, hello SDK iki saniye bekler ve ardından başka bir ileti için denetler; bir ileti bulunduğunda yeniden denemeden önce yaklaşık dört saniye bekler. Merhaba maksimum bekleme süresi, ulaşana kadar sonraki başarısız denemeler tooget bir kuyruk iletisi sonra hello bekleme süresi tooincrease devam eder. hangi Varsayılanları tooone minute. [Merhaba maksimum bekleme süresi yapılandırılabilir](#how-to-set-configuration-options).

## <a name="multiple-instances"></a>Birden çok örneği
Web uygulamanız birden çok örneklerinde çalıştırıyorsa, her makineye sürekli Webjob'lar çalışır ve her makine için Tetikleyicileri bekleyin ve toorun işlevlerini deneyin. Bu yol açabilir bazı senaryolarda işleme toosome işlevleri aynı veri nedenle işlevleri (bunları sürekli olarak aynı giriş verisi oluşturmuyor hello ile arama sonuçları çoğaltmak için yazılmış) ıdempotent olmalıdır, iki kez hello.  

## <a name="parallel-execution"></a>Paralel yürütme
Birden çok işlevler farklı sıralarda dinleme varsa, iletileri aynı anda alındığında hello SDK bunları paralel olarak çağırın.

tek bir kuyruk için birden fazla ileti alındığında hello aynı durum geçerlidir. Varsayılan olarak, hello SDK 16 iletileri kuyruğa toplu bir zaman alır ve paralel olarak işler hello işlevi yürütür. [Merhaba toplu iş boyutu Dur yapılandırılabilir](#how-to-set-configuration-options). İşlenmekte olan hello numarası hello toplu iş boyutu toohalf aldığında hello SDK başka bir toplu iş alır ve bu iletileri işleme başlatır. Bu nedenle hello en fazla eş zamanlı ileti işlevi işlenen sayısı bir ve yarı kez bir hello toplu iş boyutu dur. Bu sınır olan tooeach işlev ayrı ayrı uygular bir **QueueTrigger** özniteliği. Paralel yürütme üzerinde bir Sıraya alınan iletileri istemiyorsanız hello toplu iş boyutu too1 ayarlayın.

## <a name="get-queue-or-queue-message-metadata"></a>Sıra veya sıra ileti meta verileri alma
Aşağıdaki ileti özelliklere parametreleri toohello yöntemi imza ekleyerek hello alabilirsiniz:

* **DateTimeOffset** expirationTime
* **DateTimeOffset** insertionTime
* **DateTimeOffset** nextVisibleTime
* **dize** queueTrigger (ileti metni içerir)
* **dize** kimliği
* **dize** popReceipt
* **int** dequeueCount

Hello Azure storage API'si ile doğrudan toowork isterseniz, ayrıca ekleyebileceğiniz bir **CloudStorageAccount** parametresi.

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

## <a name="graceful-shutdown"></a>Kapama
Sürekli bir WebJob içinde çalışan bir işlevinin kabul edebileceği bir **CancellationToken** hello işletim sistemi toonotify hello işlevi hello zaman sağlayan Web işi parametredir hakkında toobe sonlandırıldı. Bu bildirim toomake hello beklenmedik bir şekilde veri tutarsız bir durumda bırakır şekilde sonlandırma işlevi değil emin kullanabilirsiniz.

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

## <a name="how-toocreate-a-queue-message-while-processing-a-queue-message"></a>Toocreate bir kuyruk iletisi nasıl bir kuyruk iletisi işlenirken
Yeni bir kuyruk iletisi kullanım hello oluşturan bir işlev toowrite **sıra** özniteliği. Gibi **QueueTrigger**, hello kuyruk adı bir dize olarak geçirin veya yapabilecekleriniz [hello sıra adı dinamik olarak ayarlamak](#how-to-set-configuration-options).

### <a name="string-queue-messages"></a>Dize iletileri
zaman uyumsuz olmayan kodu örneği aşağıdaki hello hello kuyruk iletisi olarak içerik aynı "inputqueue" adlı hello sıraya alınan hello hello sırasındaki "outputqueue" adlı yeni bir kuyruk iletisi oluşturur. (İşlevler için async kullanma **IAsyncCollector<T>**  daha sonra bu bölümde gösterilen.)

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) kuyruk iletileri
toocreate geçişi hello POCO bir dize yerine bir POCO içeren bir kuyruk iletisi türü bir çıkış parametresi toohello **sıra** özniteliği Oluşturucusu.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

Merhaba SDK hello nesne tooJSON otomatik olarak serileştirir. Merhaba nesnesi boş olsa bile bir kuyruk iletisi her zaman oluşturulur.

### <a name="create-multiple-messages-or-in-async-functions"></a>Birden çok iletileri oluşturmak veya zaman uyumsuz işlevleri
toocreate birden fazla ileti olun hello çıkış sırası için hello parametre türü **ICollector<T>**  veya **IAsyncCollector<T>**hello aşağıdaki örnekte gösterildiği gibi.

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Her kuyruk iletisi hemen hello oluşturulduğunda **Ekle** yöntemi çağrılır.

### <a name="types-that-hello-queue-attribute-works-with"></a>Türleri bu hello sıra özniteliği birlikte çalışır.
Merhaba kullanabilirsiniz **sıra** parametre türleri şu hello özniteliği:

* **dize çıkışı** (Merhaba işlevi sona erdiğinde parametre değeri null olmayan ise kuyruk iletisi oluşturur)
* **byte [] çıkışı** (gibi çalışır **dize**)
* **CloudQueueMessage çıkışı** (gibi çalışır **dize**)
* **POCO çıkışı** (serializable bir tür oluşturduğu bir ileti null bir nesne ile Merhaba işlevi sona erdiğinde hello parametre null ise)
* **ICollector**
* **IAsyncCollector**
* **CloudQueue** (iletileri el ile oluşturmak için kullanarak hello Azure Storage API'sini doğrudan)

### <a name="use-webjobs-sdk-attributes-in-hello-body-of-a-function"></a>Web işleri SDK'si özniteliklerini işlevinin hello gövdesindeki kullanın
Toodo ihtiyacınız varsa bazı, işlevinde bir Web işleri SDK'si öznitelik gibi kullanmadan önce iş **sıra**, **Blob**, veya **tablo**, hello kullanabilirsiniz **IBinder** arabirimi.

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

Merhaba **IBinder** arabirimi hello ile de kullanılabilir **tablo** ve **Blob** öznitelikleri.

## <a name="how-tooread-and-write-blobs-and-tables-while-processing-a-queue-message"></a>Nasıl tooread ve yazma BLOB ve bir sıraya ileti işlenirken tabloları
Merhaba **Blob** ve **tablo** öznitelikleri tooread etkinleştirmek ve blobları ve tabloları yazma. Bu bölümdeki Hello örnekler tooblobs uygulayın. BLOB'ları oluşturulduğunda veya güncelleştirilmiş tootrigger nasıl işlediği gösteren kod örnekleri için bkz: [nasıl toouse Azure blob depolama hello WebJobs SDK ile](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)ve okuma ve yazma tabloları kod örnekleri için bkz: [nasıl toouse Azure tablo Depolama hello WebJobs SDK ile](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).

### <a name="string-queue-messages-triggering-blob-operations"></a>Dize iletileri kuyruğa blobu işlemleri tetikleme
Bir dizeyi içeren bir kuyruk iletisi için **queueTrigger** hello kullanabileceğiniz bir yer tutucudur **Blob** özniteliğin **blobPath** Merhaba içeriğine içeren parametresi Başlangıç iletisi.

Merhaba aşağıdaki örnek kullanır **akış** tooread ve yazma BLOB'lar nesneleri. Merhaba kuyruk iletisi hello textblobs kapsayıcıda bulunan bir blob hello adıdır. Merhaba blob ile bir kopyasını "-Yeni" eklenmiş toohello adı oluşturulduğu hello aynı kapsayıcı.

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Merhaba **Blob** özniteliği Oluşturucusu alır bir **blobPath** hello kapsayıcı ve blob adı belirten parametre. Bu yer tutucu hakkında daha fazla bilgi için bkz: [nasıl toouse Azure blob depolama hello WebJobs SDK ile](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).

Ne zaman hello öznitelik süsler bir **akış** nesnesi, başka bir oluşturucu parametresini belirtir hello **FileAccess** modu okuma, yazma veya okuma/yazma olarak.

Merhaba aşağıdaki örnek kullanan bir **CloudBlockBlob** toodelete blob nesnesi. Merhaba kuyruk iletisi hello blob hello adıdır.

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) kuyruk iletileri
JSON olarak hello kuyruk iletisi içinde depolanan bir POCO için hello hello nesnesinde özelliklerini adı yer tutucuları kullanabilirsiniz **sıra** özniteliğin **blobPath** parametresi. Bu gibi durumlarda, sıra meta veri özellik adları da yer tutucu olarak kullanabilirsiniz. Bkz: [sıra veya sıra ileti meta verileri alma](#get-queue-or-queue-message-metadata).

Merhaba aşağıdaki örnek bir blob tooa yeni blob farklı bir uzantı kopyalar. Merhaba kuyruk iletisi bir **BlobInformation** içeren nesnesinin **BlobName** ve **BlobNameWithoutExtension** özellikleri. Merhaba özellik adları olarak kullanılan hello blob yolu yer tutucuları Merhaba **Blob** öznitelikleri.

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

Bir blob tooan nesnesi bağlama önce işlevinde bazı iş toodo gerekiyorsa, gösterildiği gibi hello işlevinin hello gövdesi hello özniteliğinde kullanabilirsiniz [hello gövdesi bir işlev kullanmak Web işleri SDK'si öznitelikleri](#use-webjobs-sdk-attributes-in-the-body-of-a-function).

### <a name="types-you-can-use-hello-blob-attribute-with"></a>Merhaba kullanabileceğiniz türü özniteliğiyle Blob
Merhaba **Blob** özniteliği şu türlerini hello ile kullanılabilir:

* **Akış** (okuma veya yazma, hello FileAccess Oluşturucu parametresi kullanılarak belirtilen)
* **TextReader**
* **TextWriter**
* **dize** (okuma)
* **dize çıkışı** (yazma; hello işlevi döndüğünde yalnızca hello dizesi parametresi null olmayan ise bir blob oluşturur)
* POCO (okuma)
* POCO out (yazma; her zaman bir blob oluşturur, hello işlevi döndüğünde POCO parametre null ise null nesnesi olarak oluşturur)
* **CloudBlobStream** (yazma)
* **ICloudBlob** (okuma veya yazma)
* **CloudBlockBlob** (okuma veya yazma)
* **CloudPageBlob** (okuma veya yazma)

## <a name="how-toohandle-poison-messages"></a>Nasıl toohandle zehirli ileti
İçerikleri işlevi toofail neden olan iletileri çağrılır *zehirli ileti*. Merhaba işlevi başarısız olduğunda, hello kuyruk iletisi silinmez ve sonunda yeniden neden hello döngüsü toobe yinelenen kayıt. otomatik olarak hello döngüsü Hello SDK sınırlı sayıda yineleme sonra kesintiye uğratabilir veya el ile yapabilirsiniz.

### <a name="automatic-poison-message-handling"></a>Otomatik zehirli ileti işleme
Merhaba SDK too5 kez tooprocess bir kuyruk iletisi yukarı işlevi çağırır. Merhaba beşinci deneme başarısız olursa, selamlama iletisine taşınan tooa zararlı sıradır. Nasıl tooconfigure Merhaba yeniden deneme sayısı görebilirsiniz [nasıl tooset yapılandırma seçenekleri](#how-to-set-configuration-options).

Merhaba zararlı sıra adlandırılan *{originalqueuename}*-zararlı. Bir işlev tooprocess iletileri hello zararlı sıradan günlüğe yazma veya el ile ilgilenilmesi gereken bir bildirim göndererek yazabilirsiniz.

Aşağıdaki örnek hello hello içinde **CopyBlob** bir kuyruk iletisi mevcut olmayan bir blob hello adını içerdiğinde işlevi başarısız olur. Bu durum oluştuğunda selamlama iletisine hello copyblobqueue sıra toohello copyblobqueue poison sıradan taşınır. Merhaba **ProcessPoisonMessage** zehir iletisi günlükleri hello sonra.

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

![Zehirli ileti işleme için konsol çıkışı](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a>El ile zehirli ileti işleme
Hello sayısı bir ileti toplanma işleme ekleyerek alabileceğiniz bir **int** adlı parametre **dequeueCount** tooyour işlevi. Bundan sonra onay hello işlev kodu sayıma dequeue ve hello sayısı hello aşağıdaki örnekte gösterildiği gibi bir eşiği aştığında kendi zehirli ileti işleme gerçekleştirmek kullanabilirsiniz.

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

## <a name="how-tooset-configuration-options"></a>Nasıl tooset yapılandırma seçenekleri
Merhaba kullanabilirsiniz **JobHostConfiguration** yapılandırma seçenekleri aşağıdaki türü tooset hello:

* Kodda Hello SDK bağlantı dizelerini ayarlayın.
* Yapılandırma **QueueTrigger** maksimum gibi ayarları dequeue sayısı.
* Sıra adları yapılandırmasından alın.

### <a name="set-sdk-connection-strings-in-code"></a>Kod içinde SDK bağlantı dizelerini ayarlayın
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

### <a name="configure-queuetrigger--settings"></a>QueueTrigger ayarlarını yapılandırma
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

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a>Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama
Kuyruk adı, bir blob adı veya kapsayıcı toospecify bazen istediğiniz veya bir tablo adı kod sabit kodlu yerine onu. Örneğin, toospecify hello sıra adı için isteyebilirsiniz **QueueTrigger** bir yapılandırma dosyası veya ortam değişkeninde.

Bunu geçirerek yapabilirsiniz bir **NameResolver** toohello nesne **JobHostConfiguration** türü. Web işleri SDK'si özniteliği Oluşturucusu parametrelerinde yüzde (%) işareti tarafından çevrelenen özel yer tutucular içerir ve **NameResolver** kod bu yer tutucular yerine kullanılan hello gerçek değerler toobe belirtir.

Örneğin, toouse istediğinizi düşünelim bir sıra hello test ortamında logqueuetest ve üretimde bir adlandırılmış logqueueprod adlı. Sabit kodlanmış kuyruk adı yerine bir girişe hello toospecify hello adı istediğiniz **appSettings** hello gerçek sıra adı olurdu koleksiyonu. Merhaba, **appSettings** anahtar logqueue, işlevinizi aşağıdaki örneğine hello gibi görünebilir.

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

**NameResolver** sınıfını hello sıra adından sonra almak **appSettings** hello aşağıdaki örnekte gösterildiği gibi:

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

Merhaba geçirdiğiniz **NameResolver** toohello sınıfında **JobHost** nesne hello aşağıdaki örnekte gösterildiği gibi.

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

**Not:** kuyruk, tablo ve blob adları çözümlenmiş her zaman bir işlev çağrılır, ancak blob kapsayıcı adları yalnızca Merhaba uygulaması başladığında çözümlenir. Merhaba iş çalışırken blob kapsayıcı adı değiştirilemiyor.

## <a name="how-tootrigger-a-function-manually"></a>Nasıl tootrigger bir işlev el ile
tootrigger işlevi el ile Merhaba kullanmak **çağrısı** veya **CallAsync** hello yöntemi **JobHost** nesne ve hello **NoAutomaticTrigger** hello aşağıdaki örnekte gösterildiği gibi hello işlevi özniteliği.

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

## <a name="how-toowrite-logs"></a>Toowrite nasıl kaydeder
Başlangıç Panosu iki yerde günlükleri gösterir: hello sayfası hello Web işi için ve belirli bir Web işi çağırma için hello sayfası.

![Web işi sayfasındaki günlükleri](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![İşlev çağırma sayfasındaki günlükleri](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

Bir işlev veya hello çağıran konsol yöntemlerini çıkışı **Main()** yöntemi görünür hello Web işi için hello Pano sayfası, belirli yöntem çağırma için hello sayfasındaki değil. Çıktı yöntemi imzanız bir parametresinden alma hello TextWriter nesneden bir yöntem çağırma için hello Pano sayfası görünür.

Konsol çıktısı, bağlantılı tooa belirli yöntemi çağırma olamaz, hello konsol birçok iş işlevlerinin hello çalışmıyor olabilir tek iş parçacıklı, olduğu için aynı anda. İşte bu nedenle hello SDK her işlev çağrısını kendi benzersiz günlük yazıcı nesnesi ile sağlar.

toowrite [uygulama izleme günlükleri](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), kullanın **Console.Out** (bilgisi olarak işaretlenmiş günlükleri oluşturur) ve **Console.Error** (hata olarak işaretlenmiş günlükleri oluşturur). Toouse alternatiftir [izleme veya TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), uyarı, ayrıntı sağlar ve kritik düzeyleri toplama tooInfo ve hata. Azure web uygulamanızı nasıl yapılandırdığınıza bağlı olarak Azure BLOB veya uygulama izleme günlükleri hello web uygulama günlük dosyalarında Azure tabloları görünür. Tüm konsol çıktısı doğru olduğu gibi hello en son 100 uygulama günlüklerini da hello Web işi, olmayan bir işlev çağrısını hello sayfasını için hello Pano sayfası görünür.

Merhaba hello programı yerel olarak çalışmıyorsa hello program bir Azure WebJob içinde yalnızca çalışıyorsa, Pano veya başka bir ortamında konsol çıktısı görüntülenir.

Merhaba Pano bağlantı dizesi toonull ayarlayarak günlüğü devre dışı bırakabilirsiniz. Daha fazla bilgi için bkz: [nasıl tooset yapılandırma seçenekleri](#how-to-set-configuration-options).

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

Hello WebJobs SDK Pano, hello hello çıktısını **TextWriter** toohello sayfa belirli bir zaman gittiğiniz yukarı gösterir işlev çağırma ve seçin nesnesi **geçiş çıktı**:

![Çağırma bağlantı](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![İşlev çağırma sayfasındaki günlükleri](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

Merhaba WebJob (değil hello işlev çağrısını) için toohello sayfasına gidin ve seçin hello WebJobs SDK Pano, konsol hello en son 100 satırları göster yukarı çıktı **geçiş çıktı**.

![Çıkışı Aç/Kapat](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

Bir sürekli Webjob'un uygulama günlüklerini/data/işleri/sürekli/içinde gösterilmesi*{webjobname}*hello web uygulama dosya sisteminde /job_log.txt.

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

Azure blob hello uygulamada günlükleri şuna benzeyebilir: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Merhaba Dünya!, 2014-09-26T21:01:13, hata, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.Error - Merhaba Dünya!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Merhaba Dünya!,

Ve Azure tablo hello **Console.Out** ve **Console.Error** günlükleri şuna benzeyebilir:

![Tablo bilgi günlüğüne](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Hata günlüğü tablosundaki](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede kod sağlamıştır gösteren nasıl örnekleri Azure kuyruklarla çalışmaya yönelik yaygın senaryolar toohandle. Toouse Azure Web işleri ve hello Web işleri SDK'si nasıl görürüm hakkında daha fazla bilgi için [Azure Web işleri belge kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).

