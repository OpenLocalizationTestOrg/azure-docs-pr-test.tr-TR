---
title: "WebJobs SDK ile Azure Blob Storage kullanımı"
description: "WebJobs SDK ile Azure blob depolama kullanmayı öğrenin. Yeni bir blob bir kapsayıcıda görüntülendiğinde bir işlem tetikleyebilir ve 'zararlı BLOB' tanıtıcı."
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
ms.openlocfilehash: e0a792ccdf8097d5cde254d6d4690a64838378ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-blob-storage-with-the-webjobs-sdk"></a>WebJobs SDK ile Azure Blob Storage kullanımı
## <a name="overview"></a>Genel Bakış
Bu kılavuz, Azure blob oluşturulduğunda veya bir işlem tetiklemek nasıl gösteren C# kod örnekleri sağlar. Kod örnekleri kullan [WebJobs SDK](websites-dotnet-webjobs-sdk.md) sürüm 1.x.

BLOB'ları oluşturmak nasıl gösteren kod örnekleri için bkz: [WebJobs SDK ile Azure kuyruk depolama kullanma](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Bildiğiniz Kılavuzu varsayar [bağlantıyla Visual Studio'da bir Web işi projesi oluşturma, depolama hesabınıza o noktadan dizeleri](websites-dotnet-webjobs-sdk-get-started.md) veya [birden çok depolama hesabı](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

## <a id="trigger"></a>Bir blob oluşturulduğunda veya bir işlev tetikleme
Bu bölümde nasıl kullanılacağını gösterir `BlobTrigger` özniteliği. 

> [!NOTE]
> Web işleri SDK'si için yeni veya değiştirilmiş BLOB'lar izlemek için günlük dosyalarını tarar. Bu işlem, gerçek zamanlı değildir; blob oluşturulduktan sonra bir işlev birkaç dakika kadar veya daha uzun tetiklenen değil. Ayrıca, [depolama günlüklerine "en iyi çaba" üzerinde oluşturulan](https://msdn.microsoft.com/library/azure/hh343262.aspx) temel; tüm olayları Yakalanacak garantisi yoktur. Bazı koşullarda günlükleri eksik. Blob Tetikleyicileri hızı ve güvenilirliği sınırlamaları, uygulamanız için kabul edilebilir değilse, blob oluşturma ve kullanma, bir kuyruk iletisi oluşturmak için önerilen yöntem olduğu [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) yerineözniteliği`BlobTrigger` blob işler işlevi özniteliği.
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a>Blob adı uzantısı için tek bir yer tutucu
Aşağıdaki kod örneği görünen metin BLOB'ları kopyalar *giriş* kapsayıcıya *çıkış* kapsayıcı:

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Öznitelik oluşturucunun kapsayıcı adı hem de blob adı için bir yer tutucu belirten bir dize parametresi alan. Bu örnekte, bir blob adlandırırsanız *Blob1.txt* oluşturulur *giriş* kapsayıcı, işlev oluşturur adlı bir blob *Blob1.txt* içinde *çıkış* kapsayıcı. 

Aşağıdaki kod örneğinde gösterildiği gibi blob adı yer tutucu ile adı deseni belirtebilirsiniz:

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Bu kodu "özgün-" ile başlayan adlara sahip yalnızca BLOB'ları kopyalar. Örneğin, *özgün Blob1.txt* içinde *giriş* kapsayıcı kopyalanır *kopya Blob1.txt* içinde *çıkış* kapsayıcı.

Süslü ayraçlar sahip blob adları için bir ad deseni belirtmeniz gerekiyorsa, süslü ayraçlar çift. Örneğin, BLOB'ları bulmak istiyorsanız *görüntüleri* böyle adlara sahip kapsayıcı:

        {20140101}-soundfile.mp3

Bu, düzeni için kullanın:

        images/{{20140101}}-{name}

Örnekte, *adı* yer tutucu değerini olacaktır *soundfile.mp3*. 

### <a name="separate-blob-name-and-extension-placeholders"></a>Ayrı bir blob adı ve uzantısı yer tutucuları
Görünen BLOB'ları kopyalar olarak aşağıdaki kod örneği dosya uzantısını değiştiren *giriş* kapsayıcıya *çıkış* kapsayıcı. Kod uzantısını günlüklerini *giriş* blob ve genişletilmesi ayarlar *çıkış* için blob *.txt*.

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

## <a id="types"></a>BLOB'larını bağlayabilirsiniz türleri
Kullanabileceğiniz `BlobTrigger` özniteliği aşağıdaki türler:

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

Azure depolama hesabı ile doğrudan çalışmak isterseniz, ayrıca ekleyebileceğiniz bir `CloudStorageAccount` yöntem imzası parametresi.

Örnekler için bkz: [blob Github.com'u azure webjobs sdk havuzda bağlama kodda](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).

## <a id="string"></a>Dize bağlayarak metin blob içeriği alma
Metin BLOB'ları beklenir, `BlobTrigger` uygulanabilir bir `string` parametresi. Aşağıdaki kod örneği için metin blob bağlar bir `string` adlı parametre `logMessage`. İşlevi için Web işleri SDK'si Pano blob içeriğini yazmak için bu parametresini kullanır. 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a id="icbsb"></a>Blob içeriğinin ICloudBlobStreamBinder kullanarak serileştirilen alma
Aşağıdaki kod örneği uygulayan bir sınıf kullanır `ICloudBlobStreamBinder` etkinleştirmek için `BlobTrigger` bir blobu bağlamak için öznitelik `WebImage` türü.

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

`WebImage` Kod bağlama sağlanır bir `WebImageBinder` öğesinden türetilen sınıf `ICloudBlobStreamBinder`.

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

## <a name="getting-the-blob-path-for-the-triggering-blob"></a>Blob yolu için tetikleyici blob alma
İşlevi tetikleyen blob blob adını ve kapsayıcı adını almak için içeren bir `blobTrigger` işlev imzası parametresinde dize.

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <a id="poison"></a>Zararlı BLOB'ları nasıl ele alınacağını
Zaman bir `BlobTrigger` işlevi başarısız oldu, SDK çağırır onu yeniden durumunda hata geçici bir hata neden oldu. Blob içerik tarafından hatasına neden oldu blob işlemeye çalıştığında her zaman işlevi başarısız olur. Varsayılan olarak, SDK'sı bir işlev en fazla 5 kez için belirli bir blob çağırır. Beşinci başarısız çalışırsanız, SDK bir ileti adlandırılan bir kuyruğun ekler. *webjobs blobtrigger poison*.

En fazla yeniden deneme sayısı yapılandırılabilir. Aynı [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) ayarı zararlı blob işleme ve zararlı sıraya ileti işleme için kullanılır. 

Kuyruk iletisini zararlı BLOB'lar için aşağıdaki özellikleri içeren bir JSON nesnesidir:

* FunctionId (biçimde *{Web işi adı}*. İşlevler. *{İşlev adı}*, örneğin: WebJob1.Functions.CopyBlob)
* BlobType ("BlockBlob" veya "PageBlob")
* Kapsayıcı adı
* BlobName
* ETag (örneğin bir blob sürüm tanıtıcısını: "0x8D1DC6E70A277EF")

Aşağıdaki kod örneğinde, `CopyBlob` işlev her çağrıldığında başarısız olmasına neden kodu bulunur. Sonra en fazla yeniden deneme sayısı için çağırır SDK, zararlı blob sıraya bir ileti oluşturulur ve bu iletiyi tarafından işlenen `LogPoisonBlob` işlevi. 

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

SDK JSON ileti otomatik olarak seri durumdan çıkarır. Burada `PoisonBlobMessage` sınıfı: 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a id="polling"></a>BLOB yoklama algoritması
WebJobs SDK tarafından belirtilen tüm kapsayıcıları tarar `BlobTrigger` uygulama başlangıcında öznitelikleri. Yeni BLOB'lar bulunan önce biraz olabilir şekilde büyük depolama hesabı bu tarama biraz zaman alabilir ve `BlobTrigger` işlevleri çalıştırılır.

SDK'sı, uygulama başladıktan sonra yeni veya değiştirilmiş BLOB'lar algılamak için blob depolama günlüklerinden düzenli aralıklarla okur. Blob günlükleri arabelleğe alınmış ve yalnızca fiziksel olarak her 10 dakikada yazılan veya bu nedenle, bu nedenle önemli gecikme olabileceğini blob oluşturulmuş veya karşılık gelen önce güncelleştirilmiş sonra `BlobTrigger` işlevi yürütür. 

Kullanarak oluşturduğunuz BLOB'ları için bir özel durum var. `Blob` özniteliği. WebJobs SDK yeni blob oluşturduğunda, bunu yeni blob hemen eşleşen tüm geçirir `BlobTrigger` işlevleri. Blob girişleri ve çıkışları zinciri varsa, bu nedenle SDK bunları verimli bir şekilde işleyebilir. Ancak, düşük gecikme süresi, blob işleme işlevleri için oluşturulmuş veya başka yollarla güncelleştirilmiş BLOB'ları çalıştıran istiyorsanız, kullanmanızı öneririz `QueueTrigger` yerine `BlobTrigger`.

### <a id="receipts"></a>BLOB giriş
WebJobs SDK emin yapıyorsa hiçbir `BlobTrigger` işlevi için aynı yeni veya güncelleştirilmiş blob birden çok kez çağrıldığından. Bunu tutarak yapar *blob giriş* verilen blob sürümü işlenen belirlemek için.

BLOB giriş adlı bir kapsayıcıda depolanır *azure Web işleri konakları* AzureWebJobsStorage bağlantı dizesi tarafından belirtilen Azure depolama hesabı. Bir blob giriş aşağıdaki bilgileri içerir:

* İçin blob çağrıldı işlevi ("*{Web işi adı}*. İşlevler. *{İşlev adı}*", örneğin:"WebJob1.Functions.CopyBlob")
* Kapsayıcı adı
* Blob türü ("BlockBlob" veya "PageBlob")
* Blob adı
* ETag (örneğin bir blob sürüm tanıtıcısını: "0x8D1DC6E70A277EF")

Bir blob yeniden işlemeyerek zorlamak istiyorsanız, o blobundan blob giriş el ile silebilirsiniz *azure Web işleri konakları* kapsayıcı.

## <a id="queues"></a>Kuyruklar makalesiyle kapsanan ilgili konular
İşleme, senaryoları blob özgü olmayan Web işleri SDK'si veya nasıl bir kuyruk iletisi tarafından tetiklenen blob işleme yönetileceği hakkında bilgi için bkz [WebJobs SDK ile Azure kuyruk depolama kullanma](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Bu makalede ele alınan ilgili konular şunlardır:

* Zaman uyumsuz işlevleri
* Birden çok örneği
* Kapama
* Web işleri SDK'si öznitelikleri bir işlev gövdesine kullanın
* Kod içinde SDK bağlantı dizelerini ayarlayın.
* Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama
* Yapılandırma `MaxDequeueCount` zararlı blob işleme.
* Tetik el ile bir işlevi
* Günlüklerini yazma

## <a id="nextsteps"></a> Sonraki adımlar
Bu kılavuz, Azure BLOB'ları ile çalışmak için genel senaryolar nasıl ele alınacağını gösteren kod örnekleri sağlamıştır. Azure Web işleri ve WebJobs SDK nasıl kullanılacağı hakkında daha fazla bilgi için bkz: [Azure Web işleri önerilen kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).

