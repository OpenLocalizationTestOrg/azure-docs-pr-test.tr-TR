---
title: aaaHow toouse hello WebJobs SDK ile Azure blob storage
description: "Nasıl toouse Azure blob depolama hello WebJobs SDK ile bilgi edinin. Yeni bir blob bir kapsayıcıda görüntülendiğinde bir işlem tetikleyebilir ve 'zararlı BLOB' tanıtıcı."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.assetid: bf32f919-f7bc-4aaa-916e-461c02f2e26c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: b34ea8cffee7c0475641886150dee521130a3132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-with-hello-webjobs-sdk"></a>Nasıl toouse Azure blob depolama hello WebJobs SDK ile
## <a name="overview"></a>Genel Bakış
Bu kılavuz C# sağlar kod örnekleri gösteren nasıl tootrigger bir Azure blob oluşturulduğunda veya bir işlem. Merhaba kod örnekleri kullan [WebJobs SDK](websites-dotnet-webjobs-sdk.md) sürüm 1.x.

BLOB'nasıl toocreate gösteren kod örnekleri için bkz: [nasıl toouse Azure kuyruk depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Merhaba Kılavuzu varsayar bildiğiniz [nasıl toocreate bağlantısı ile Visual Studio'da bir Web işi projesi bu noktası tooyour depolama hesabı dizeleri](websites-dotnet-webjobs-sdk-get-started.md) veya çok[birden çok depolama hesabı](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

## <a id="trigger"></a>Nasıl tootrigger blob oluşturulduğunda veya bir işlevi
Bu bölümde gösterilmiştir nasıl toouse hello `BlobTrigger` özniteliği. 

> [!NOTE]
> Yeni veya değiştirilmiş BLOB'lar için Web işleri SDK'si taramaları günlük dosyaları toowatch hello. Bu işlem, gerçek zamanlı değildir; Merhaba blob oluşturulduktan sonra bir işlev birkaç dakika kadar veya daha uzun tetiklenen değil. Ayrıca, [depolama günlüklerine "en iyi çaba" üzerinde oluşturulan](https://msdn.microsoft.com/library/azure/hh343262.aspx) temel; tüm olayları Yakalanacak garantisi yoktur. Bazı koşullarda günlükleri eksik. Merhaba hızı ve güvenilirliği sınırlamaları blob tetikleyicileri, uygulamanız için kabul edilebilir değilse, hello yöntemi toocreate bir kuyruk iletisi hello blob oluşturun ve hello kullandığınızda önerilir [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) yerine özniteliği Merhaba `BlobTrigger` hello blob işler hello işlevi özniteliği.
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a>Blob adı uzantısı için tek bir yer tutucu
Merhaba aşağıdaki kod örneği görüntülenen metin BLOB'ları hello kopyalar *giriş* kapsayıcı toohello *çıkış* kapsayıcı:

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Merhaba öznitelik oluşturucunun hello kapsayıcı adı ve hello blob adı için bir yer tutucu belirten bir dize parametresi alan. Bu örnekte, bir blob adlandırırsanız *Blob1.txt* hello oluşturulur *giriş* kapsayıcısının hello işlev oluşturur adlı bir blob *Blob1.txt* hello içinde *çıkış*  kapsayıcı. 

Aşağıdaki kod örneği hello gösterildiği gibi hello blob adı tutucuyla adı düzeni belirtebilirsiniz:

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Bu kodu "özgün-" ile başlayan adlara sahip yalnızca BLOB'ları kopyalar. Örneğin, *özgün Blob1.txt* hello içinde *giriş* kapsayıcı çok kopyalanan*kopya Blob1.txt* hello içinde *çıkış* kapsayıcı.

Süslü ayraçlar hello sahip blob adları için toospecify adı deseni gerekiyorsa hello süslü ayraçlar çift. Merhaba toofind blobları isterseniz, örneğin, *görüntüleri* böyle adlara sahip kapsayıcı:

        {20140101}-soundfile.mp3

Bu, düzeni için kullanın:

        images/{{20140101}}-{name}

Merhaba örnekte hello *adı* yer tutucu değerini olacaktır *soundfile.mp3*. 

### <a name="separate-blob-name-and-extension-placeholders"></a>Ayrı bir blob adı ve uzantısı yer tutucuları
hello görünür BLOB'ları kopyalar hello aşağıdaki kod örnek değişikliklerini dosya uzantısı hello *giriş* kapsayıcı toohello *çıkış* kapsayıcı. Merhaba kodunu günlüğe yazar hello hello uzantısı *giriş* blob ve hello hello uzantısı ayarlar *çıkış* çok blob*.txt*.

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <a id="types"></a>Tooblobs bağlayabilirsiniz türleri
Merhaba kullanabilirsiniz `BlobTrigger` şu türlerini hello özniteliği:

* `string`
* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `IEnumerable<CloudBlockBlob>`
* `IEnumerable<CloudPageBlob>`
* Tarafından seri diğer türleri [ICloudBlobStreamBinder](#icbsb) 

Hello Azure depolama hesabı ile doğrudan toowork isterseniz, ayrıca ekleyebileceğiniz bir `CloudStorageAccount` parametre toohello yöntemi imzası.

Merhaba örnekler için bkz [blob Github.com'u hello azure webjobs sdk havuzda bağlama kodda](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).

## <a id="string"></a>Bağlama toostring tarafından metin blob içeriği alma
Metin BLOB'ları beklenir, `BlobTrigger` uygulanan tooa olabilir `string` parametresi. Merhaba aşağıdaki kod örneği bağlar metin blob tooa `string` adlı parametre `logMessage`. Merhaba işlevi hello blob toohello WebJobs SDK Pano Bu parametre toowrite hello içeriğini kullanır. 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a id="icbsb"></a>Blob içeriğinin ICloudBlobStreamBinder kullanarak serileştirilen alma
Merhaba aşağıdaki kod örneği kullanan uygulayan bir sınıf `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` toobind blob toohello özniteliği `WebImage` türü.

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK", 
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

Merhaba `WebImage` kod bağlama sağlanır bir `WebImageBinder` öğesinden türetilen sınıf `ICloudBlobStreamBinder`.

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input, 
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="getting-hello-blob-path-for-hello-triggering-blob"></a>Blob tetikleme Merhaba Hello blob yolu alınıyor
tooget hello kapsayıcı adı ve hello işlevi tetikleyen hello blobu blob adını içeren bir `blobTrigger` hello işlev imzası parametresinde dize.

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <a id="poison"></a>Nasıl toohandle poison BLOB
Zaman bir `BlobTrigger` işlevi başarısız oldu, hello SDK çağırır onu yeniden durumda hello hatası tarafından geçici bir hata neden oldu. Merhaba blob hello içeriğe göre Hello hatasına neden oldu tooprocess hello blob çalışır her zaman hello işlevi başarısız olur. Varsayılan olarak, hello SDK too5 kez bir işlev için belirli bir blob çağırır. Merhaba beşinci deneme başarısız olursa, hello SDK adlı bir ileti tooa sırası ekler *webjobs blobtrigger poison*.

Merhaba en fazla yeniden deneme sayısı yapılandırılabilir. aynı hello [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) ayarı zararlı blob işleme ve zararlı sıraya ileti işleme için kullanılır. 

Merhaba kuyruk iletisi zararlı BLOB'lar için aşağıdaki özelliklere hello içeren bir JSON nesnesi şudur:

* FunctionId (Merhaba biçiminde *{Web işi adı}*. İşlevler. *{İşlev adı}*, örneğin: WebJob1.Functions.CopyBlob)
* BlobType ("BlockBlob" veya "PageBlob")
* Kapsayıcı adı
* BlobName
* ETag (örneğin bir blob sürüm tanıtıcısını: "0x8D1DC6E70A277EF")

Merhaba aşağıdaki örnek, hello kod `CopyBlob` işlev her çağrıldığında, toofail neden olan kod bulunur. Sonra Hello SDK çağrıları, hello en fazla yeniden deneme sayısı için hello zararlı blob sırada bir ileti oluşturulur ve bu ileti hello tarafından işlenir `LogPoisonBlob` işlevi. 

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

Merhaba SDK hello JSON ileti otomatik olarak seri durumdan çıkarır. Merhaba işte `PoisonBlobMessage` sınıfı: 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a id="polling"></a>BLOB yoklama algoritması
Merhaba WebJobs SDK tarafından belirtilen tüm kapsayıcıları tarar `BlobTrigger` uygulama başlangıcında öznitelikleri. Yeni BLOB'lar bulunan önce biraz olabilir şekilde büyük depolama hesabı bu tarama biraz zaman alabilir ve `BlobTrigger` işlevleri çalıştırılır.

toodetect yeni veya değiştirilmiş BLOB'lar uygulama başlatma sonra SDK düzenli aralıklarla hello blob depolama alanından okur hello günlüğe kaydeder. Merhaba blob günlükleri arabelleğe alınmış ve yalnızca fiziksel olarak her 10 dakikada yazılan veya bu nedenle, bu nedenle önemli gecikme olabileceğini blob oluşturulmuş veya hello karşılık gelen önce güncelleştirilmiş sonra `BlobTrigger` işlevi yürütür. 

Hello kullanarak oluşturduğunuz BLOB'ları için bir özel durum var. `Blob` özniteliği. Merhaba WebJobs SDK yeni blob oluşturduğunda, hello yeni blob hemen geçtikten tooany eşleşen `BlobTrigger` işlevleri. Blob girişleri ve çıkışları zinciri varsa, bu nedenle hello SDK bunları verimli bir şekilde işleyebilir. Ancak, düşük gecikme süresi, blob işleme işlevleri için oluşturulmuş veya başka yollarla güncelleştirilmiş BLOB'ları çalıştıran istiyorsanız, kullanmanızı öneririz `QueueTrigger` yerine `BlobTrigger`.

### <a id="receipts"></a>BLOB giriş
Merhaba WebJobs SDK emin olur hiçbir `BlobTrigger` işlevi birden çok kez Merhaba aynı yeni adlı veya blob güncelleştirildi. Bunu tutarak yapar *blob giriş* verilen blob sürümü işlediğinde sipariş toodetermine içinde.

BLOB giriş adlı bir kapsayıcıda depolanır *azure Web işleri konakları* hello AzureWebJobsStorage bağlantı dizesi tarafından belirtilen hello Azure depolama hesabı. Bir blob giriş bilgisinden hello sahiptir:

* Merhaba hello blobu çağrıldı işlevi ("*{Web işi adı}*. İşlevler. *{İşlev adı}*", örneğin:"WebJob1.Functions.CopyBlob")
* Merhaba kapsayıcı adı
* Merhaba blob türü ("BlockBlob" veya "PageBlob")
* Merhaba blob adı
* Merhaba ETag (örneğin bir blob sürüm tanıtıcısını: "0x8D1DC6E70A277EF")

Tooforce bir blob yeniden işleme istiyorsanız, o blob için hello blob giriş hello el ile silebilirsiniz *azure Web işleri konakları* kapsayıcı.

## <a id="queues"></a>Merhaba sıraları makalesiyle kapsanan ilgili konular
Nasıl toohandle blob işleme bir kuyruk iletisi tarafından veya WebJobs SDK senaryoları tetiklenen değil hakkında bilgi için işleme, belirli tooblob bakın [nasıl toouse Azure kuyruk depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Bu makalede ele alınan ilgili konular hello şunları içerir:

* Zaman uyumsuz işlevleri
* Birden çok örneği
* Kapama
* Web işleri SDK'si özniteliklerini işlevinin hello gövdesindeki kullanın
* Kodda Hello SDK bağlantı dizelerini ayarlayın.
* Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama
* Yapılandırma `MaxDequeueCount` zararlı blob işleme.
* Tetik el ile bir işlevi
* Günlüklerini yazma

## <a id="nextsteps"></a> Sonraki adımlar
Bu kılavuz, nasıl Azure çalışmak için genel senaryolar toohandle BLOB gösteren kod örnekleri sağlamıştır. Toouse Azure Web işleri ve hello Web işleri SDK'si nasıl görürüm hakkında daha fazla bilgi için [Azure Web işleri önerilen kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).

