---
title: "aaaGet, bağlı hizmetler (Web işi projeleri) blob depolama ve Visual Studio ile çalışmaya | Microsoft Docs"
description: "Visual Studio kullanarak Azure depolama tooan bağlandıktan sonra bir Web işi projesinin Blob storage kullanarak tooget nasıl başlatılacağını Hizmetleri bağlı."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 29f2d5e19426d37d815cdf9a1e00abfb1e07ccf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a>Azure Blob ile çalışmaya başlama depolama ve Visual Studio bağlı Hizmetleri (Web işi projeler)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Genel Bakış
Bu makalede, C# sağlanmaktadır kod örnekleri gösteren nasıl tootrigger bir Azure blob oluşturulduğunda veya bir işlem. Merhaba kod örnekleri kullanır hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) sürüm 1.x. Merhaba Visual Studio kullanarak bir depolama hesabı tooa Web işi projesinin eklediğinizde **bağlı Hizmetleri Ekle** iletişim kutusunda, hello uygun Azure depolama NuGet paketi yüklenir, hello uygun .NET başvuruları eklenen toohello Proje ve hello depolama hesabı için bağlantı dizelerini hello App.config dosyasında güncelleştirilir.

## <a name="how-tootrigger-a-function-when-a-blob-is-created-or-updated"></a>Nasıl tootrigger blob oluşturulduğunda veya bir işlevi
Bu bölümde gösterilmiştir nasıl toouse hello **BlobTrigger** özniteliği.

 **Not:** WebJobs SDK taramaları günlük dosyaları toowatch yeni veya değiştirilmiş BLOB'lar için hello. Bu işlem, doğası gereği yavaş; Merhaba blob oluşturulduktan sonra bir işlev birkaç dakika kadar veya daha uzun tetiklenen değil.  Uygulamanızı tooprocess BLOB'ları hemen gerekirse, hello yöntemi toocreate bir kuyruk iletisi hello blob oluşturun ve hello kullandığınızda önerilir [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) özniteliği hello yerine **BlobTrigger** hello blob işler hello işlevi özniteliği.

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

## <a name="types-that-you-can-bind-tooblobs"></a>Tooblobs bağlayabilirsiniz türleri
Merhaba kullanabilirsiniz **BlobTrigger** şu türlerini hello özniteliği:

* **dize**
* **TextReader**
* **Akış**
* **ICloudBlob**
* **CloudBlockBlob**
* **CloudPageBlob**
* Tarafından seri diğer türleri [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)

Hello Azure depolama hesabı ile doğrudan toowork isterseniz, ayrıca ekleyebileceğiniz bir **CloudStorageAccount** parametre toohello yöntemi imzası.

## <a name="getting-text-blob-content-by-binding-toostring"></a>Bağlama toostring tarafından metin blob içeriği alma
Metin BLOB'ları beklenir, **BlobTrigger** uygulanan tooa olabilir **dize** parametresi. Merhaba aşağıdaki kod örneği bağlar metin blob tooa **dize** adlı parametre **logMessage**. Merhaba işlevi hello blob toohello WebJobs SDK Pano Bu parametre toowrite hello içeriğini kullanır.

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a>Blob içeriğinin ICloudBlobStreamBinder kullanarak serileştirilen alma
Merhaba aşağıdaki kod örneği kullanan uygulayan bir sınıf **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** toobind blob toohello özniteliği **WebImage** türü.

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

Merhaba **WebImage** kod bağlama sağlanır bir **WebImageBinder** öğesinden türetilen sınıf **ICloudBlobStreamBinder**.

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

## <a name="how-toohandle-poison-blobs"></a>Nasıl toohandle poison BLOB
Zaman bir **BlobTrigger** işlevi başarısız oldu, hello SDK çağırır onu yeniden durumda hello hatası tarafından geçici bir hata neden oldu. Merhaba blob hello içeriğe göre Hello hatasına neden oldu tooprocess hello blob çalışır her zaman hello işlevi başarısız olur. Varsayılan olarak, hello SDK too5 kez bir işlev için belirli bir blob çağırır. Merhaba beşinci deneme başarısız olursa, hello SDK adlı bir ileti tooa sırası ekler *webjobs blobtrigger poison*.

Merhaba en fazla yeniden deneme sayısı yapılandırılabilir. aynı hello [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) ayarı zararlı blob işleme ve zararlı sıraya ileti işleme için kullanılır.

Merhaba kuyruk iletisi zararlı BLOB'lar için aşağıdaki özelliklere hello içeren bir JSON nesnesi şudur:

* FunctionId (Merhaba biçiminde *{Web işi adı}*. İşlevler. *{İşlev adı}*, örneğin: WebJob1.Functions.CopyBlob)
* BlobType ("BlockBlob" veya "PageBlob")
* Kapsayıcı adı
* BlobName
* ETag (örneğin bir blob sürüm tanıtıcısını: "0x8D1DC6E70A277EF")

Merhaba aşağıdaki örnek, hello kod **CopyBlob** işlev her çağrıldığında, toofail neden olan kod bulunur. Sonra Hello SDK çağrıları, hello en fazla yeniden deneme sayısı için hello zararlı blob sırada bir ileti oluşturulur ve bu ileti hello tarafından işlenir **LogPoisonBlob** işlevi.

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

Merhaba SDK hello JSON ileti otomatik olarak seri durumdan çıkarır. Merhaba işte **PoisonBlobMessage** sınıfı:

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a>BLOB yoklama algoritması
Merhaba WebJobs SDK tarafından belirtilen tüm kapsayıcıları tarar **BlobTrigger** uygulama başlangıcında öznitelikleri. Yeni BLOB'lar bulunan önce biraz olabilir şekilde büyük depolama hesabı bu tarama biraz zaman alabilir ve **BlobTrigger** işlevleri çalıştırılır.

toodetect yeni veya değiştirilmiş BLOB'lar uygulama başlatma sonra SDK düzenli aralıklarla hello blob depolama alanından okur hello günlüğe kaydeder. Merhaba blob günlükleri arabelleğe alınmış ve yalnızca fiziksel olarak her 10 dakikada yazılan veya bu nedenle, bu nedenle önemli gecikme olabileceğini blob oluşturulmuş veya hello karşılık gelen önce güncelleştirilmiş sonra **BlobTrigger** işlevi yürütür.

Hello kullanarak oluşturduğunuz BLOB'ları için bir özel durum var. **Blob** özniteliği. Merhaba WebJobs SDK yeni blob oluşturduğunda, hello yeni blob hemen geçtikten tooany eşleşen **BlobTrigger** işlevleri. Blob girişleri ve çıkışları zinciri varsa, bu nedenle hello SDK bunları verimli bir şekilde işleyebilir. Ancak, düşük gecikme süresi, blob işleme işlevleri için oluşturulmuş veya başka yollarla güncelleştirilmiş BLOB'ları çalıştıran istiyorsanız, kullanmanızı öneririz **QueueTrigger** yerine **BlobTrigger**.

### <a name="blob-receipts"></a>BLOB giriş
Merhaba WebJobs SDK emin olur hiçbir **BlobTrigger** işlevi birden çok kez Merhaba aynı yeni adlı veya blob güncelleştirildi. Bunu tutarak yapar *blob giriş* verilen blob sürümü işlediğinde sipariş toodetermine içinde.

BLOB giriş adlı bir kapsayıcıda depolanır *azure Web işleri konakları* hello AzureWebJobsStorage bağlantı dizesi tarafından belirtilen hello Azure depolama hesabı. Bir blob giriş bilgisinden hello sahiptir:

* Merhaba hello blobu çağrıldı işlevi ("*{Web işi adı}*. İşlevler. *{İşlev adı}*", örneğin:"WebJob1.Functions.CopyBlob")
* Merhaba kapsayıcı adı
* Merhaba blob türü ("BlockBlob" veya "PageBlob")
* Merhaba blob adı
* Merhaba ETag (örneğin bir blob sürüm tanıtıcısını: "0x8D1DC6E70A277EF")

Tooforce bir blob yeniden işleme istiyorsanız, o blob için hello blob giriş hello el ile silebilirsiniz *azure Web işleri konakları* kapsayıcı.

## <a name="related-topics-covered-by-hello-queues-article"></a>Merhaba sıraları makalesiyle kapsanan ilgili konular
Nasıl toohandle blob işleme bir kuyruk iletisi tarafından veya WebJobs SDK senaryoları tetiklenen değil hakkında bilgi için işleme, belirli tooblob bakın [nasıl toouse Azure kuyruk depolama hello WebJobs SDK ile](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).

Bu makalede ele alınan ilgili konular hello şunları içerir:

* Zaman uyumsuz işlevleri
* Birden çok örneği
* Kapama
* Web işleri SDK'si özniteliklerini işlevinin hello gövdesindeki kullanın
* Kodda Hello SDK bağlantı dizelerini ayarlayın.
* Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama
* Yapılandırma **MaxDequeueCount** zararlı blob işleme.
* Tetik el ile bir işlevi
* Günlüklerini yazma

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, nasıl Azure çalışmak için genel senaryolar toohandle BLOB gösteren kod örnekleri sağlamıştır. Toouse Azure Web işleri ve hello Web işleri SDK'si nasıl görürüm hakkında daha fazla bilgi için [Azure Web işleri belge kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).

