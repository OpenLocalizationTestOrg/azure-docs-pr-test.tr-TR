---
title: Azure Search ile Azure Blob Storage aaaIndexing
description: "Azure Search ile nasıl tooindex Azure Blob Depolama ve ayıklama metinden belgeleri öğrenin"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 2a5968f4-6768-4e16-84d0-8b995592f36a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/22/2017
ms.author: eugenesh
ms.openlocfilehash: 1bdd34e66a4a9192ed88cacbc7b8456d0dcdfeb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-documents-in-azure-blob-storage-with-azure-search"></a>Azure arama ile Azure Blob Storage belgelerde dizin oluşturma
Bu makalede gösterilmektedir nasıl toouse Azure Search tooindex belgeleri (PDF gibi Microsoft Office belgelerini ve diğer birçok ortak biçimleri) Azure Blob depolama alanına depolanır. İlk olarak, ayarlama ve blob dizin oluşturucu yapılandırma hello temellerini açıklar. Ardından, derin keşif davranışları ve büyük olasılıkla tooencounter olduğunuz senaryolar sunar.

## <a name="supported-document-formats"></a>Desteklenen Belge biçimleri
Merhaba blob dizin oluşturucu metin Belge biçimleri aşağıdaki hello ayıklayabilirsiniz:

* PDF
* Microsoft Office biçimleri: DOCX/DOC, XLSX/XLS, PPTX/PPT, MSG (Outlook e-postalar)  
* HTML
* XML
* ZIP
* EML
* RTF
* Düz metin dosyaları (Ayrıca bkz. [dizin düz metin](#IndexingPlainText))
* JSON (bkz [dizin JSON BLOB'ların](search-howto-index-json-blobs.md))
* CSV (bkz [dizin oluşturma CSV BLOB'ların](search-howto-index-csv-blobs.md) önizleme özelliği)

> [!IMPORTANT]
> CSV ve JSON dizileri desteği şu anda önizlemede değil. Bu biçim yalnızca sürüm kullanılarak kullanılabilir **2016-09-01-Önizleme** hello REST API veya sürüm 2.x Önizleme hello .NET SDK'sı, biri. Lütfen unutmayın, Önizleme API'leri sınama ve değerlendirme için tasarlanmıştır ve üretim ortamlarında kullanılmamalıdır.
>
>

## <a name="setting-up-blob-indexing"></a>BLOB dizin oluşturmayı ayarlama
Azure Blob Storage bir kullanarak dizin oluşturucu ayarlayabilirsiniz:

* [Azure portal](https://ms.portal.azure.com)
* Azure arama [REST API'si](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations)
* Azure arama [.NET SDK'sı](https://aka.ms/search-sdk)

> [!NOTE]
> Bazı özellikler (örneğin, alan eşlemelerini) henüz hello Portalı'nda kullanılabilir değil ve program aracılığıyla kullanılan toobe sahip.
>
>

Burada, hello REST API kullanarak hello akışı gösterilmektedir.

### <a name="step-1-create-a-data-source"></a>1. adım: bir veri kaynağı oluşturma
Hangi veri tooindex, gerekli kimlik bilgilerini tooaccess hello veriler ve ilkeleri tooefficiently (yeni, değiştirilen veya silinen satır) hello verilerde yapılan değişiklikler tanımlamak bir veri kaynağını belirtir. Bir veri kaynağı kullanılabilir aynı arama hizmeti hello birden çok dizin oluşturucular tarafından.

BLOB dizin oluşturma işlemi için gerekli özellikler aşağıdaki hello hello veri kaynağı olması gerekir:

* **ad** arama hizmetinizi içinde hello veri kaynağının hello benzersiz adıdır.
* **tür** olmalıdır `azureblob`.
* **kimlik bilgileri** hello depolama hesabı bağlantı dizesi hello olarak sağlar `credentials.connectionString` parametresi. Bkz: [nasıl toospecify kimlik bilgileri](#Credentials) aşağıda Ayrıntılar için.
* **kapsayıcı** depolama hesabınızdaki bir kapsayıcı belirtir. Varsayılan olarak, hello kapsayıcıdaki tüm blob'lara alınabilir. Yalnızca belirli bir sanal dizin tooindex blobları istiyorsanız, isteğe bağlı hello kullanarak bu dizini belirtebilirsiniz **sorgu** parametresi.

toocreate bir veri kaynağı:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional-virtual-directory-name>" }
    }   

Merhaba oluşturma Datasource API'si hakkında daha fazla bilgi için bkz: [veri kaynağı oluşturma](https://docs.microsoft.com/rest/api/searchservice/create-data-source).

<a name="Credentials"></a>
#### <a name="how-toospecify-credentials"></a>Nasıl toospecify kimlik bilgileri ####

Şu yöntemlerden birini kullanarak hello blob kapsayıcısında hello kimlik bilgilerini sağlayabilir:

- **Tam erişim depolama hesabı bağlantı dizesi**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>`. Toohello depolama hesabı dikey giderek hello bağlantı dizesi hello Azure portal ' edinebilirsiniz > Ayarlar > tuşları (Klasik depolama hesapları) ya da ayarlar > erişim tuşları (Azure Resource Manager depolama hesapları).
- **Depolama hesabı paylaşılan erişim imzası** (SAS) bağlantı dizesi: `BlobEndpoint=https://<your account>.blob.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=b&sp=rl` hello SAS listelemek ve kapsayıcıları ve nesneleri üzerinde okuma hello sahip olması gerekir (Bu durumda BLOB ').
-  **Kapsayıcı paylaşılan erişim imzası**: `ContainerSharedAccessUri=https://<your storage account>.blob.core.windows.net/<container name>?sv=2016-05-31&sr=c&sig=<hello signature>&se=<hello validity end time>&sp=rl` hello SAS listelemek ve hello kapsayıcısı üzerinde okuma hello sahip olmalıdır.

Paylaşılan depolama hakkında daha fazla bilgi için erişim imzalar, bkz: [kullanarak paylaşılan erişim imzaları](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

> [!NOTE]
> SAS kimlik bilgileri kullanıyorsanız tarihlerinden yenilenen imzaları tooprevent ile düzenli aralıklarla tooupdate hello veri kaynağı kimlik bilgileri gerekir. SAS kimlik bilgilerinin süresi dolar, benzer bir hata iletisi ile çok hello dizin oluşturucu başarısız olur`Credentials provided in hello connection string are invalid or have expired.`.  

### <a name="step-2-create-an-index"></a>2. adım: bir dizin oluşturun
Hello dizin öznitelikleri bir belgede hello alanları belirtir ve diğer Bu şekil hello arama deneyimi oluşturur.

İşte nasıl toocreate dizin ile bir aranabilir `content` alan bloblarından ayıklanan toostore hello metin:   

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "id", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "content", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": false, "facetable": false }
          ]
    }

Dizin oluşturma hakkında daha fazla bilgi için bkz: [Create Index](https://docs.microsoft.com/rest/api/searchservice/create-index)

### <a name="step-3-create-an-indexer"></a>3. adım: bir dizin oluşturucu yapın
Bir dizin oluşturucu hedef arama dizin ile bir veri kaynağına bağlanır ve zamanlama tooautomate hello veri yenilemesi sağlar.

Başlangıç dizini ve veri kaynağı oluşturulduktan sonra hazır toocreate hello dizin oluşturucu olduğunuz:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "blob-indexer",
      "dataSourceName" : "blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

Bu dizin oluşturucu iki saatte bir çalışır (zamanlama aralığı çok Ayarla "PT2H"). bir dizin oluşturucu toorun 30 dakikada hello aralığı çok ayarlamak "PT30M". Merhaba kısa desteklenen aralığı 5 dakikadır. Merhaba zamanlama atlanırsa, isteğe bağlı -, yalnızca zaman bir kez oluşturulduktan sonra bir dizin oluşturucu çalıştırır. Ancak, bir dizin oluşturucu isteğe bağlı herhangi bir zamanda çalıştırabilirsiniz.   

Merhaba dizin oluşturucu API oluşturma hakkında daha fazla ayrıntı için kullanıma [oluşturma dizin oluşturucu](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

## <a name="how-azure-search-indexes-blobs"></a>Azure Search BLOB'ları nasıl dizinler

Merhaba bağlı olarak [dizin oluşturucu yapılandırma](#PartsOfBlobToIndex), hello blob dizin oluşturucu yalnızca depolama meta veri dizini (yararlı meta verileri hello ve tooindex gerekmeyen hakkında yalnızca çok değer verdiğiniz hello BLOB içeriği), depolama ve içerik meta veri ya da her ikisini de meta verileri ve metin içeriği. Varsayılan olarak, hello dizin oluşturucu meta verilerini ve içeriği ayıklar.

> [!NOTE]
> Varsayılan olarak, BLOB'lar ile yapılandırılmış bir içerik JSON veya CSV gibi tek bir metin öbek dizine alınır. Yapılandırılmış bir biçimde tooindex JSON ve CSV BLOB'lar istiyorsanız bkz [dizin JSON BLOB '](search-howto-index-json-blobs.md) ve [dizin oluşturma CSV BLOB'ların](search-howto-index-csv-blobs.md) Önizleme özellikleri.
>
> Bileşik veya katıştırılmış bir belge (örneğin, ZIP arşivini veya ekleri içeren katıştırılmış Outlook e-posta içeren bir Word belgesini) de tek bir belge dizine alınır.

* Merhaba belgesinin Hello metinsel içeriği adlı bir dize alanı ayıklanan `content`.

> [!NOTE]
> Azure arama sınırlar fiyatlandırma katmanı hello bağlı olarak ayıklar ne kadar metin: 32.000 karakter ücretsiz katmanı, Basic 64.000 ve standart, standart S2 ve standart S3 katmanları için 4 milyon. Bir uyarı hello dizin oluşturucu durumu yanıt kesilmiş belgeler için dahil edilmiştir.  

* Kullanıcı tanımlı meta veri özelliklerini hello blob üzerindeki mevcut varsa, aynen ayıklanır.
* Standart blob meta veri özelliklerini alanları izleyen hello ayıklanır:

  * **meta veri\_depolama\_adı** (Edm.String) - hello blob hello dosya adı. Örneğin, bir blob /my-container/my-folder/subfolder/resume.pdf varsa, hello bu alanın değeri `resume.pdf`.
  * **meta veri\_depolama\_yolu** (Edm.String) - hello BLOB hello depolama hesabı dahil olmak üzere, tam URI hello. Örneğin, `https://myaccount.blob.core.windows.net/my-container/my-folder/subfolder/resume.pdf`
  * **meta veri\_depolama\_içerik\_türü** (Edm.String) - hello kod tarafından belirtildiği gibi içerik türü tooupload hello blobu kullanılır. Örneğin, `application/octet-stream`.
  * **meta veri\_depolama\_son\_değiştiren** (Edm.DateTimeOffset) - son değiştirilme hello blob için zaman damgası. Azure arama, bu zaman damgası değiştirilen tooidentify BLOB'lar, her şeyi hello ilk dizin oluşturma sonrasında yeniden dizin oluşturmaya tooavoid kullanır.
  * **meta veri\_depolama\_boyutu** (EDM.Int64) - blob bayt cinsinden boyutu.
  * **meta veri\_depolama\_içerik\_md5** (Edm.String) - hello blob içeriğinin, kullanılabilir durumdaysa, MD5 karma değeri.
* Meta veri özelliklerini belirli tooeach belge biçimi listelenen hello alanlarına ayıklanan [burada](#ContentSpecificMetadata).

Tüm hello yukarıdaki özellikleri için arama dizininizdeki toodefine alanları gerekmez - yalnızca uygulamanız için gereksinim hello özellikleri yakalayın.

> [!NOTE]
> Genellikle, hello alan adları varolan dizininize belge ayıklama sırasında oluşturulan hello alan adları farklı olacaktır. Kullanabileceğiniz **alan eşlemelerini** search dizininizi Azure Search toohello alan adlarının tarafından sağlanan toomap hello özellik adları. Alan eşlemeleri aşağıda kullanacağınız örneği görürsünüz.
>
>

<a name="DocumentKeys"></a>
### <a name="defining-document-keys-and-field-mappings"></a>Belge anahtarları ve alan eşlemelerini tanımlama
Azure Search'te hello belge anahtarını bir belge benzersiz olarak tanımlar. Tüm arama dizini türü Edm.String tam olarak bir anahtar alanı olması gerekir. Merhaba anahtar alanı (bunu gerçekten hello yalnızca gerekli bir alandır) toohello dizin eklenen her belge için gereklidir.  

Ayıklanan alanı toohello anahtar alanı dizininiz için eşlemelisiniz dikkatlice düşünün. Merhaba adaylar:

* **meta veri\_depolama\_adı** - bu kullanışlı bir aday olarak, ancak, BLOB'lar ile aynı adı farklı klasörlerde hello yaptığınız gibi 1) hello adları benzersiz olabileceğine dikkat edin ve 2) hello adı karakterleri içerebilir, kısa çizgi gibi belge anahtarlarında geçersizdir. Geçersiz karakterlerle hello kullanarak başa `base64Encode` [alan eşleme işlev](search-indexer-field-mappings.md#base64EncodeFunction) - bunu yaptığınızda, API geçirme gibi arama çağırdığında tooencode belge anahtarları unutmayın. (Örneğin, .NET hello kullanabileceğiniz [UrlTokenEncode yöntemi](https://msdn.microsoft.com/library/system.web.httpserverutility.urltokenencode.aspx) bu amaç için).
* **meta veri\_depolama\_yolu** - hello tam yolunu kullanarak benzersizlik sağlar, ancak hello yolu kesinlikle içeriyor `/` olan karakterleri [geçersiz bir belge anahtarında](https://docs.microsoft.com/rest/api/searchservice/naming-rules).  Yukarıdaki, hello anahtarlarını hello kullanarak kodlama hello seçeneğiniz `base64Encode` [işlevi](search-indexer-field-mappings.md#base64EncodeFunction).
* Yukarıdaki hello seçenekleri hiçbiri sizin için çalışıyorsanız, özel meta veri özellik toohello BLOB'lar ekleyebilirsiniz. Bu seçenek ancak blob karşıya yükleme işlemi tooadd bu meta veri özellik tooall BLOB'ları gerektirir. Başlangıç anahtarı gerekli bir özellik olduğundan, bu özelliğe sahip olmayan tüm BLOB'lar dizine toobe başarısız olur.

> [!IMPORTANT]
> Merhaba dizindeki hello anahtar alanı için açık bir eşleme varsa, Azure Search otomatik olarak kullanan `metadata_storage_path` hello anahtarı ve base-64 anahtar değerleri (Merhaba ikinci seçeneği yukarıdaki) kodlar gibi.
>
>

Bu örnekte, şimdi hello çekme `metadata_storage_name` hello belge anahtarı olarak alan. Ayrıca, dizini adlı bir anahtar alanı var varsayalım `key` alanı `fileSize` hello belge boyutu depolamak için. istediğiniz toowire işlemleri oluştururken veya güncelleştirirken oluşturucunuz alan eşlemelerini aşağıdaki hello belirtin:

    "fieldMappings" : [
      { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
      { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
    ]

toobring nasıl ekleyebileceğiniz alan eşlemelerini ve var olan bir dizin oluşturucu için anahtarların etkinleştir 64 tabanlı kodlama tüm birlikte buradan 's:

    PUT https://[service name].search.windows.net/indexers/blob-indexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "dataSourceName" : " blob-datasource ",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "fieldMappings" : [
        { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
        { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
      ]
    }

> [!NOTE]
> alan eşlemeleri hakkında daha fazla toolearn bkz [bu makalede](search-indexer-field-mappings.md).
>
>

<a name="WhichBlobsAreIndexed"></a>
## <a name="controlling-which-blobs-are-indexed"></a>Hangi BLOB'lar dizine denetleme
Hangi BLOB'lar dizine ve hangi atlanır kontrol edebilirsiniz.

### <a name="index-only-hello-blobs-with-specific-file-extensions"></a>Yalnızca hello BLOB'lar belirli dosya uzantılarına sahip dizini
Yalnızca hello BLOB'lar hello kullanarak belirtirseniz hello dosya adı uzantıları ile dizin `indexedFileNameExtensions` dizin oluşturucu yapılandırma parametresi. Merhaba, dosya uzantıları (ile başında nokta), virgülle ayrılmış listesini içeren bir dize değeridir. Örneğin, tooindex yalnızca hello. PDF ve. DOCX BLOB'lar, bunu yapın:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "indexedFileNameExtensions" : ".pdf,.docx" } }
    }

### <a name="exclude-blobs-with-specific-file-extensions"></a>BLOB'lar ile belirli dosya uzantılarını dışarıda
Hello kullanarak dizin BLOB'lar belirli dosya adı uzantıları ile dışlayabilirsiniz `excludedFileNameExtensions` yapılandırma parametresi. Merhaba, dosya uzantıları (ile başında nokta), virgülle ayrılmış listesini içeren bir dize değeridir. Örneğin, hello olanlar dışındaki tüm tooindex blobları. PNG ve. JPEG uzantılar, bunu yapın:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "excludedFileNameExtensions" : ".png,.jpeg" } }
    }

Her iki `indexedFileNameExtensions` ve `excludedFileNameExtensions` parametreleri, ilk Azure Search bakar adresindeki `indexedFileNameExtensions`, sonra en `excludedFileNameExtensions`. Bu, hello aynı dosya uzantısını hem listelerinde varsa, bu dizine almasını dışlanıp olduğunu anlamına gelir.

### <a name="dealing-with-unsupported-content-types"></a>Desteklenmeyen içerik türleriyle ele alma

Varsayılan olarak, bir blob desteklenmeyen bir içerik türüyle (örneğin, bir görüntü) karşılaştığında hemen hello blob dizin oluşturucu durdurur. Elbette hello kullanabilirsiniz `excludedFileNameExtensions` tooskip parametresi belirli içerik türlerini. Ancak, tüm hello olası içerik türleri önceden bilmeden tooindex BLOB'lar gerekebilir. Desteklenmeyen içerik türü karşılaşıldığında, dizin oluşturma toocontinue ayarlamak hello `failOnUnsupportedContentType` yapılandırma parametresi çok`false`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "failOnUnsupportedContentType" : false } }
    }

### <a name="ignoring-parsing-errors"></a>Ayrıştırma hataları yoksayma

Azure arama belge ayıklama mantığı kusursuz değildir ve desteklenen bir içerik türüne tooparse belgelerinin gibi bazen başarısız olur. DOCX veya. PDF. Bu gibi durumlarda dizin toointerrupt hello istemiyorsanız hello ayarlamak `maxFailedItems` ve `maxFailedItemsPerBatch` yapılandırma parametreleri toosome makul değerleri. Örneğin:

    {
      ... other parts of indexer definition
      "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 10 }
    }

<a name="PartsOfBlobToIndex"></a>
## <a name="controlling-which-parts-of-hello-blob-are-indexed"></a>Merhaba blob hangi kısımlarının dizine denetleme

Merhaba BLOB'lar hangi kısımlarının hello kullanarak dizinlenir denetleyebilirsiniz `dataToExtract` yapılandırma parametresi. Değerleri aşağıdaki hello alabilir:

* `storageMetadata`-yalnızca o hello belirtir [standart blob özellikleri ve kullanıcı tanımlı meta veriler](../storage/blobs/storage-properties-metadata.md) dizinlenir.
* `allMetadata`-Depolama meta verilerin belirtir ve hello [içerik türü belirli meta veriler](#ContentSpecificMetadata) ayıklanan hello blobundan içerik dizin haline getirilir.
* `contentAndMetadata`-tüm meta veri ve hello blobundan ayıklanan metinsel içerik dizinlenir belirtir. Merhaba varsayılan değer budur.

Örneğin, tooindex yalnızca hello depolama meta verileri, kullanın:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "dataToExtract" : "storageMetadata" } }
    }

### <a name="using-blob-metadata-toocontrol-how-blobs-are-indexed"></a>BLOB'ları nasıl dizine blob meta verileri toocontrol kullanma

Yukarıda açıklanan hello yapılandırma parametreleri tooall BLOB'lar uygulayın. Bazen, toocontrol nasıl isteyebilirsiniz *tek tek bloblar* dizinlenir. Bunu hello aşağıdakileri ekleyerek yapabilirsiniz blob meta veri özellikleri ve değerleri:

| Özellik adı | Özellik değeri | Açıklama |
| --- | --- | --- |
| AzureSearch_Skip |"true" |Merhaba blob dizin oluşturucu toocompletely Atla hello blob bildirir. Meta veri ne içerik ayıklama denenir. Bu, belirli bir blob art arda başarısız olur ve hello dizin oluşturma işlemi kesintiye uğratır durumunda faydalı olur. |
| AzureSearch_SkipContent |"true" |Bu, eşdeğerdir `"dataToExtract" : "allMetadata"` açıklanan ayarı [yukarıda](#PartsOfBlobToIndex) kapsamlı tooa belirli blob. |

## <a name="incremental-indexing-and-deletion-detection"></a>Artımlı dizin oluşturma ve silme algılama
Bir zamanlamaya göre bir blob dizin oluşturucu toorun ayarladığınızda, yalnızca hello blob'un tarafından belirlendiği şekilde hello BLOB'lar, değiştirilen onu yeniden dizinler `LastModified` zaman damgası.

> [!NOTE]
> Bir değişiklik algılama İlkesi toospecify yok – Artımlı dizin oluşturma sizin için otomatik olarak etkinleştirilir.

toosupport silme belgeler, "yumuşak Sil" yaklaşımı kullanın. Merhaba BLOB'lar depolayabileceği silerseniz, karşılık gelen belgeler hello arama dizinden kaldırılmaz. Bunun yerine, hello aşağıdaki adımları kullanın:  

1. Bir özel meta veri özellik toohello blob tooindicate tooAzure mantıksal olarak silinip silinmediğini arama ekleyin
2. Merhaba veri kaynağında bir geçici silme algılama ilkesi yapılandırma
3. Merhaba dizin oluşturucu (Merhaba dizin oluşturucu durumu API tarafından gösterildiği gibi) hello blob işlediğinde, fiziksel olarak hello blob silebilirsiniz

Örneğin, bir meta veri özelliği varsa, silinen bir blob toobe ilke aşağıdaki hello göz önünde bulundurur `IsDeleted` hello değerle `true`:

    PUT https://[service name].search.windows.net/datasources/blob-datasource?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" },
        "dataDeletionDetectionPolicy" : {
            "@odata.type" :"#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",     
            "softDeleteColumnName" : "IsDeleted",
            "softDeleteMarkerValue" : "true"
        }
    }   

## <a name="indexing-large-datasets"></a>Dizin oluşturma büyük veri kümeleri

BLOB'ları dizin oluşturma zaman alan bir işlem olabilir. BLOB'ları tooindex milyonlarca sahip olduğu durumlarda, verilerinizi bölümlendirme ve paralel olarak birden çok dizin oluşturucular tooprocess hello veri kullanarak dizin oluşturmayı hızlandırabilir. İşte nasıl bu ayarlayabilirsiniz:

- Verilerinizin birden çok blob kapsayıcıları ya da sanal klasörler bölüm
- Çok sayıda Azure Search veri kaynağı, bir kapsayıcı veya klasör başına ayarlayın. toopoint tooa blob klasörü, kullanım hello `query` parametre:

    ```
    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" }
    }
    ```

- Her veri kaynağı için karşılık gelen bir dizin oluşturucu yapın. Tüm Dizin oluşturucuların can noktası toohello hello aynı hedef arama dizini.  

- Bir arama birimi hizmetinizde bir dizin oluşturucu herhangi bir zamanda çalıştırabilirsiniz. Yukarıda açıklandığı gibi birden çok dizin oluşturucu oluşturma yalnızca gerçekten paralel olarak çalıştırırsanız yararlı olur. toorun paralel olarak birden çok dizin oluşturucu ölçeklendirme arama hizmetinizi uygun sayıda bölümler ve çoğaltmalar oluşturarak. Arama hizmetinizi 6 arama birimi (örneğin, 2 bölüm x 3 yineleme) varsa, örneğin, daha sonra 6 dizin oluşturucular, hello dizin oluşturma performansı six-fold bir artış sonuçta çalıştırabilirsiniz. ölçekleme ve kapasite planlaması hakkında daha fazla toolearn bkz [ölçeklendirme sorgu ve iş yüklerini Azure Search'te dizin oluşturma için kaynak düzeylerini](search-capacity-planning.md).

## <a name="indexing-documents-along-with-related-data"></a>İlgili verileri birlikte belgelere dizin

Çok "belgeleri dizininize birden çok kaynaktan toplayın" isteyebilirsiniz. Örneğin, Cosmos DB içinde depolanan diğer meta verilerle BLOB'lar toomerge metinden isteyebilirsiniz. Anında iletme dizin oluşturma API çeşitli dizin oluşturucular birlikte çok oluşturmak birden fazla bölümü arama belgelerden hello bile kullanabilirsiniz. 

Bu toowork için tüm dizin oluşturucuların ve diğer bileşenleri tooagree hello belge anahtarı gerekir. Dış makalede ayrıntılı bir kılavuz için bkz: [Azure Search'te diğer verilerle belgeleri birleştirmeniz ](http://blog.lytzen.name/2017/01/combine-documents-with-other-data-in.html).

<a name="IndexingPlainText"></a>
## <a name="indexing-plain-text"></a>Dizin oluşturma düz metin 

Tüm bloblarınızın içeren düz metin olarak aynı kodlama Merhaba, önemli ölçüde dizin oluşturma performansı kullanarak artırabilirsiniz **modu ayrıştırma metin**. modu, kümesi hello ayrıştırma toouse metin `parsingMode` Yapılandırma özelliği çok`text`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text" } }
    }

Varsayılan olarak, hello `UTF-8` kodlama varsayılır. farklı bir kodlama, toospecify kullanmak hello `encoding` Yapılandırma özelliği: 

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text", "encoding" : "windows-1252" } }
    }


<a name="ContentSpecificMetadata"></a>
## <a name="content-type-specific-metadata-properties"></a>İçerik türe özgü meta veriler özellikleri
Merhaba aşağıdaki tabloda her belge biçimi için yapılan işleme özetler ve Azure Search tarafından ayıklanan hello meta veri özelliklerini açıklar.

| Belge biçimi / içerik türü | İçerik türü belirli meta veriler özellikleri | İşlem ayrıntıları |
| --- | --- | --- |
| HTML (`text/html`) |`metadata_content_encoding`<br/>`metadata_content_type`<br/>`metadata_language`<br/>`metadata_description`<br/>`metadata_keywords`<br/>`metadata_title` |Şerit HTML İşaretleme ve ayıklama metin |
| PDF (`application/pdf`) |`metadata_content_type`<br/>`metadata_language`<br/>`metadata_author`<br/>`metadata_title` |Embedded belgeler (görüntüleri hariç) dahil olmak üzere bir metin Ayıkla |
| DOCX (application/vnd.openxmlformats-officedocument.wordprocessingml.document) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |Embedded belgeler dahil olmak üzere bir metin Ayıkla |
| DOC (uygulama/msword) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |Embedded belgeler dahil olmak üzere bir metin Ayıkla |
| XLSX (application/vnd.openxmlformats-officedocument.spreadsheetml.sheet) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |Embedded belgeler dahil olmak üzere bir metin Ayıkla |
| XLS (uygulama/vnd.ms-excel) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |Embedded belgeler dahil olmak üzere bir metin Ayıkla |
| PPTX (application/vnd.openxmlformats-officedocument.presentationml.presentation) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |Embedded belgeler dahil olmak üzere bir metin Ayıkla |
| PPT (uygulama/vnd.ms-powerpoint) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |Embedded belgeler dahil olmak üzere bir metin Ayıkla |
| MSG (uygulama/vnd.ms-outlook) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_message_bcc`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_subject` |Metni ekler dahil olmak üzere, ayıklayın |
| ZIP (uygulama/posta) |`metadata_content_type` |Merhaba arşiv tüm belgelerde metin Al |
| XML (uygulama/xml) |`metadata_content_type`</br>`metadata_content_encoding`</br> |Şerit XML biçimlendirme ve ayıklama metni |
| JSON (uygulama/json) |`metadata_content_type`</br>`metadata_content_encoding` |Metni ayıklayın<br/>Not: birden çok belge alanları JSON blobundan tooextract gerekiyorsa, bkz. [dizin JSON BLOB'ların](search-howto-index-json-blobs.md) Ayrıntılar için |
| EML (ileti/rfc822) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_creation_date`<br/>`metadata_subject` |Metni ekler dahil olmak üzere, ayıklayın |
| RTF (uygulama/rtf) |`metadata_content_type`</br>`metadata_author`</br>`metadata_character_count`</br>`metadata_creation_date`</br>`metadata_page_count`</br>`metadata_word_count`</br> | Metni ayıklayın|
| Düz metin (metin/düz) |`metadata_content_type`</br>`metadata_content_encoding`</br> | Metni ayıklayın|


## <a name="help-us-make-azure-search-better"></a>Azure Search iyileştirmemize yardımcı olun
Özellik istekleri veya fikir geliştirmeleri için varsa, bize bilmeniz bizim [UserVoice sitesinde](https://feedback.azure.com/forums/263029-azure-search/).
