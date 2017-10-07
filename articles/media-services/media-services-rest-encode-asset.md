---
title: "aaaHow tooencode medya Kodlayıcı standart kullanarak bir Azure varlığını | Microsoft Docs"
description: "Azure Media Services toouse Medya Kodlayıcısı standart tooencode medya nasıl içerik öğrenin. Kod örnekleri, REST API kullanın."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a>Nasıl tooencode medya Kodlayıcı standart kullanarak bir varlık
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [REST](media-services-rest-encode-asset.md)
> * [Portal](media-services-portal-encode.md)
>
>

## <a name="overview"></a>Genel Bakış
toodeliver hello Internet üzerinden dijital video, hello medyayı sıkıştırmanız gerekir. Dijital video dosyaları büyük ve çok büyük toodeliver düzgün şekilde hello Internet üzerinden veya müşterilerinizin aygıtları toodisplay olabilir. Kodlama müşterilerinizin medyanızı görüntüleyebilmeniz için video ve ses sıkıştırma hello işlemidir.

Kodlama işleri hello en yaygın işlemleri Azure Media Services biridir. Bir kodlama tooanother kodlama işleri tooconvert medya dosyaları oluşturun. Kodlarken, hello Media Services yerleşik Kodlayıcı (Medya Kodlayıcısı standart) kullanabilirsiniz. Bir Media Services iş ortağı tarafından sağlanan bir kodlayıcı de kullanabilirsiniz. Üçüncü taraf kodlayıcılar hello Azure Market kullanılabilir. Kodlayıcı için tanımlanan Önayar dizeleri veya önceden belirlenmiş yapılandırma dosyalarını kullanarak kodlama görevlerine hello ayrıntılarını belirtebilirsiniz. kullanılabilir hazır toosee hello türlerini görmek [Medya Kodlayıcısı standart için görev hazır](http://msdn.microsoft.com/library/mt269960).

Her iş sahip olabilir veya tooaccomplish, işleme hello türüne bağlı olarak daha fazla görev istiyor. Hello REST API, işler ve bunların ilgili görevleri aşağıdaki iki yöntemden biriyle oluşturabilirsiniz:

* Görevler, satır içi olarak tanımlanan iş varlıkları hello görevleri gezinti özelliği aracılığıyla gerçekleştirilebilir.
* OData toplu işleme kullanın.

Her zaman Kaynak dosyalarınız Uyarlamalı bit hızlı MP4 kümesi kodlamak ve ardından kullanarak hello kümesi toohello istenen biçimine dönüştürmek öneririz [dinamik paketleme](media-services-dynamic-packaging-overview.md).

Çıkış varlığına depolama şifrelenmiş ise, hello varlık teslim ilkesini yapılandırmanız gerekir. Daha fazla bilgi için bkz: [varlık teslim ilkesini yapılandırma](media-services-rest-configure-asset-delivery-policy.md).

## <a name="considerations"></a>Dikkat edilmesi gerekenler

Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir. Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).

Medya işlemcileri başvuran başlamadan önce yüklü hello olduğunu doğru medya işlemci kimliğini doğrulayın Daha fazla bilgi için bkz: [alma medya işlemcileri](media-services-rest-get-media-processor.md).

## <a name="connect-toomedia-services"></a>TooMedia Hizmetleri'ne Bağlama

Nasıl tooconnect toohello AMS API, bkz. bilgi [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız. Sonraki çağrılar toohello yapmanız gereken yeni bir URI.

## <a name="create-a-job-with-a-single-encoding-task"></a>Bir işi ile tek bir kodlama görev oluşturma
> [!NOTE]
> Media Services REST API hello ile çalışırken, hello aşağıdaki maddeler geçerlidir:
>
> Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir. Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).
>
> Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız. Sonraki çağrılar toohello yapmanız gereken yeni bir URI. Nasıl tooconnect toohello AMS API, bkz. bilgi [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md).
>
> JSON kullanarak ve toouse hello belirterek **__metadata** hello isteğinde hello ayarlamanız gerekir (örneğin, tooreferences bağlantılı nesne), anahtar sözcüğü **kabul** üstbilgisi çok[JSON Verbose biçimi ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Kabul: uygulama/json; odata = verbose.
>
>

Aşağıdaki örneğine hello nasıl toocreate ve sonrası bir görev bir işle tooencode bir video belirli çözümleme ve kalite ayarlama gösterir. Medya Kodlayıcısı standart ile kodlamak, belirtilen görev yapılandırması hazır kullanabilirsiniz [burada](http://msdn.microsoft.com/library/mt269960).

İsteği:

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

Yanıtı:

    HTTP/1.1 201 Created

    . . .

### <a name="set-hello-output-assets-name"></a>Merhaba çıkış varlığın adı ayarlama
Aşağıdaki örnek hello nasıl tooset hello assetName özniteliği gösterir:

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a>Dikkat edilmesi gerekenler
* TaskBody özellikleri değişmez değer XML toodefine hello sayısı giriş veya başlangıç görevi tarafından kullanılan çıkış varlıklar kullanmanız gerekir. Merhaba görev konu hello XML Merhaba XML şema tanımı içerir.
* Her iç Hello TaskBody tanımı, değer <inputAsset> ve <outputAsset> JobInputAsset(value) veya JobOutputAsset(value) ayarlanması gerekir.
* Bir görev, birden fazla çıkış varlığına sahip olabilir. Bir JobOutputAsset(x) yalnızca bir kez bir görevin bir İşte bir çıkış olarak kullanılabilir.
* Bir görev bir giriş varlık JobInputAsset veya JobOutputAsset belirtebilirsiniz.
* Görevler bir döngü oluşturmuyor gerekir.
* tooJobInputAsset veya JobOutputAsset geçirmek hello değer parametresi bir varlık için hello dizin değerini temsil eder. Merhaba gerçek varlıklar hello InputMediaAssets ve OutputMediaAssets Gezinti özellikleri hello işi varlık açıklamasında tanımlanır.
* Media Services üzerinde OData v3 oluşturulduğundan, tek tek varlıkları hello InputMediaAssets hello ve OutputMediaAssets gezinti özelliği koleksiyonlar aracılığıyla başvurulan bir "__metadata: URI" ad-değer çifti.
* InputMediaAssets tooone veya Media Services ile oluşturulan daha fazla varlıklar eşler. OutputMediaAssets hello sistem tarafından oluşturulur. Bunlar, var olan bir varlık başvurusu yok.
* Merhaba assetName özniteliğini kullanarak OutputMediaAssets adlandırılabilir. Bu öznitelik yok sonra hello hello OutputMediaAsset adıdır hello ne olursa olsun hello iç metin değeri <outputAsset> öğesidir hello iş adı değeri veya hello iş kimliği değeri (durumda hello Name özelliği tanımlanmadı burada hello) soneki. AssetName için bir değer ayarlarsanız, örneğin, çok "Örnek" sonra hello OutputMediaAsset özelliği ayarlanmış adı çok "Sample." AssetName için bir değer ayarlamadınız ancak hello iş adı ayarlama ancak, çok "NewJob" sonra hello OutputMediaAsset adı "JobOutputAsset (değer) _NewJob." olacaktır

## <a name="create-a-job-with-chained-tasks"></a>Bir iş ile zincirleme görevler oluşturma
Birçok uygulama senaryolarında geliştiriciler toocreate bir dizi görevleri işleme istiyor. Media Services'de zincirleme görevleri bir dizi oluşturabilirsiniz. Her görev, farklı işleme adımları gerçekleştirir ve farklı medya işlemcileri kullanabilir. Zincirleme hello görevleri bir varlık hello varlık üzerinde doğrusal bir görev dizisini gerçekleştiren bir görev tooanother el. Ancak, bir işi gerçekleştirilen hello görevler bir sırayla gerekli toobe değildir. Zincirleme bir görev oluşturduğunuzda, hello zincirleme **ITask** nesneler, tek bir oluşturulur **IJob** nesnesi.

> [!NOTE]
> Şu anda iş başına 30 görevlerin bir sınırı yoktur. 30'dan fazla görevleri toochain ihtiyacınız varsa, birden fazla iş toocontain hello Görevler oluşturun.
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a>Dikkat edilmesi gerekenler
tooenable görev zincirleme:

* Bir işi, en az iki görev olması gerekir.
* En az bir görev girişi hello hello işteki başka bir görev çıkışıdır olması gerekir.

## <a name="use-odata-batch-processing"></a>OData toplu işleme
Aşağıdaki örnek hello nasıl toouse OData toplu işleme toocreate bir işi ve görevleri gösterir. Toplu işleme hakkında daha fazla bilgi için bkz: [açık veri Protokolü (OData) toplu işleme](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a>Bir JobTemplate kullanarak bir iş oluşturma
Ne zaman birden çok varlığı görevler, bir JobTemplate toospecify hello varsayılan görev hazır ayarları kullanın veya görevlerin tooset hello sırası ortak bir dizi kullanarak işleyin.

Aşağıdaki örnek hello nasıl satır içi toocreate JobTemplate olan bir TaskTemplate ile tanımlanan gösterir. Merhaba TaskTemplate hello Medya Kodlayıcısı standart hello MediaProcessor tooencode hello varlık dosyası olarak kullanır. Ancak, diğer MediaProcessors de kullanılabilir.

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> Diğer Media Services varlıklar farklı olarak, her TaskTemplate için yeni bir GUID tanımlayıcısı tanımlayın ve istek gövdesinde hello taskTemplateId ve ID özelliği yerleştirin. Merhaba içerik tanımlama düzeni tanımlamak Azure Media Services varlıklarda tanımlanan hello düzenini izlemeniz gerekir. Ayrıca, JobTemplates güncelleştirilemiyor. Bunun yerine, güncelleştirilmiş değişikliklerinizi içeren yeni bir tane oluşturmanız gerekir.
>
>

Başarılı olursa, yanıt aşağıdaki hello verilir:

    HTTP/1.1 201 Created

    . . .


örnekte gösterildiği nasıl aşağıdaki hello toocreate JobTemplate kimliği başvuran bir iş:

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


Başarılı olursa, yanıt aşağıdaki hello verilir:

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Sonraki adımlar
Varlık, bir iş tooencode toocreate nasıl görürüm bildiğinize göre [nasıl toocheck iş ilerleme Media Services ile](media-services-rest-check-job-progress.md).

## <a name="see-also"></a>Ayrıca bkz.
[Medya işlemcileri Al](media-services-rest-get-media-processor.md)
