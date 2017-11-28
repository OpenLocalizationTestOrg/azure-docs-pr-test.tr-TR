---
title: Azure Search Azure Table depolama aaaIndexing | Microsoft Docs
description: "Azure Search Azure Table depolama tooindex verilerin depolanma öğrenin"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 1cc27411-d0cc-40ed-8aed-c7cb9ab402b9
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: abb01a4d807cede310246b34775d8059fceb4456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="index-azure-table-storage-with-azure-search"></a>Azure Search dizini Azure tablo depolaması
Bu makalede, Azure Table storage ' nasıl toouse Azure Search tooindex veri depolanan gösterilmektedir.

## <a name="set-up-azure-table-storage-indexing"></a>Azure Table depolama dizin oluşturmayı ayarlama

Bu kaynakları kullanarak Azure Table depolama dizin oluşturucu ayarlayabilirsiniz:

* [Azure portal](https://ms.portal.azure.com)
* Azure arama [REST API'si](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations)
* Azure arama [.NET SDK'sı](https://aka.ms/search-sdk)

Burada size hello REST API kullanarak hello akışı gösterilmektedir. 

### <a name="step-1-create-a-datasource"></a>1. adım: bir veri kaynağı oluşturma

Bir veri kaynağı hangi veri tooindex belirtir, hello kimlik bilgileri gerekli tooaccess hello veri ve Azure Search tooefficiently etkinleştirmek hello ilkeleri hello verilerde yapılan değişiklikler tanımlayın.

Tablo dizin oluşturma işlemi için hello datasource hello aşağıdaki özelliklere sahip olması gerekir:

- **ad** hello veri kaynağının arama hizmetinizi içinde hello benzersiz adıdır.
- **tür** olmalıdır `azuretable`.
- **kimlik bilgileri** parametresi hello depolama hesabı bağlantı dizesi içerir. Merhaba bkz [kimlik bilgilerini belirtmeniz](#Credentials) ayrıntıları bölümü.
- **kapsayıcı** kümeleri hello tablo adı ve isteğe bağlı bir sorgu.
    - Hello kullanarak Hello tablo adını belirtin `name` parametresi.
    - İsteğe bağlı olarak, hello kullanarak bir sorgu belirtin `query` parametresi. 

> [!IMPORTANT] 
> Mümkün olduğunda, bir filtre PartitionKey üzerinde daha iyi performans için kullanın. Herhangi bir sorgu performansın büyük tablolar için sonuçta bir tam tablo taraması yapmaz. Merhaba bkz [başarım düşünceleri](#Performance) bölümü.


toocreate bir veri kaynağı:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-table", "query" : "PartitionKey eq '123'" }
    }   

Merhaba oluşturma Datasource API'si hakkında daha fazla bilgi için bkz: [veri kaynağı oluşturma](https://docs.microsoft.com/rest/api/searchservice/create-data-source).

<a name="Credentials"></a>
#### <a name="ways-toospecify-credentials"></a>Yolları toospecify kimlik bilgileri ####

Bu yollardan biriyle Merhaba tablonun hello kimlik bilgileri sağlayabilirsiniz: 

- **Tam erişim depolama hesabı bağlantı dizesi**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>` hello Azure portal ' hello bağlantı dizesi tarafından toohello giderek elde edebilirsiniz **depolama hesabı dikey** > **ayarları**   >  **Anahtarları** (için Klasik depolama hesapları için) veya **ayarları** > **erişim anahtarları** (için Azure kaynak Yönetici depolama hesapları).
- **Depolama hesabı paylaşılan erişim imzası bağlantı dizesi**: `TableEndpoint=https://<your account>.table.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=t&sp=rl` hello paylaşılan erişim imzası listelemek ve kapsayıcıları (Bu durumda tablolar) ve nesne (tablo satırları) üzerinde okuma hello sahip olmalıdır.
-  **Tablo paylaşılan erişim imzası**: `ContainerSharedAccessUri=https://<your storage account>.table.core.windows.net/<table name>?tn=<table name>&sv=2016-05-31&sig=<hello signature>&se=<hello validity end time>&sp=r` hello paylaşılan erişim imzası hello tablosunda sorgu (okuma) izinleri olmalıdır.

Paylaşılan depolama hakkında daha fazla bilgi için erişim imzalar, bkz: [kullanarak paylaşılan erişim imzaları](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

> [!NOTE]
> Paylaşılan erişim imzası kimlik bilgileri kullanıyorsanız, tarihlerinden tooupdate hello veri kaynağı kimlik bilgilerini düzenli aralıklarla yenilenen imzaları tooprevent gerekir. Paylaşılan erişim imzası kimlik bilgilerinin süresi dolar hello dizin oluşturucu çok "Merhaba bağlantı dizesinde belirtilen kimlik bilgileri geçersiz veya süresi doldu." benzer hata iletisiyle başarısız olur  

### <a name="step-2-create-an-index"></a>2. adım: bir dizin oluşturun
Merhaba dizin hello alanları hello öznitelikleri bir belgede belirtir ve diğer Bu şekil hello arama deneyimi oluşturur.

bir dizin toocreate:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "key", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "SomeColumnInMyTable", "type": "Edm.String", "searchable": true }
          ]
    }

Dizinler oluşturma hakkında daha fazla bilgi için bkz: [Create Index](https://docs.microsoft.com/rest/api/searchservice/create-index).

### <a name="step-3-create-an-indexer"></a>3. adım: bir dizin oluşturucu yapın
Bir dizin oluşturucu hedef arama dizin ile bir veri kaynağı bağlanır ve zamanlama tooautomate hello veri yenilemesi sağlar. 

Başlangıç dizini ve veri kaynağı oluşturulduktan sonra hazır toocreate hello dizin oluşturucu olduğunuz:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "table-indexer",
      "dataSourceName" : "table-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

Bu dizin oluşturucu, her iki saatte çalışır. (Merhaba zamanlama aralığı çok Ayarla "PT2H".) bir dizin oluşturucu toorun 30 dakikada hello aralığı çok ayarlamak "PT30M". Merhaba kısa desteklenen aralığı beş dakikadır. Merhaba zamanlama isteğe bağlıdır; yalnızca zaman bir kez oluşturulduğunda atlanırsa, bir dizin oluşturucu çalışır. Ancak, dilediğiniz zaman isteğe bağlı bir dizin oluşturucu çalıştırabilirsiniz.   

Merhaba oluşturma dizin oluşturucu API'si hakkında daha fazla bilgi için bkz: [oluşturma dizin oluşturucu](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

## <a name="deal-with-different-field-names"></a>Farklı bir alan adları ile Dağıt
Bazı durumlarda, varolan dizininize hello alan adları tablonuz hello özellik adlarını farklıdır. Alan eşlemeleri toomap hello özellik adları hello tablo toohello alan adlarından search dizininizi kullanabilirsiniz. alan eşlemeleri hakkında daha fazla toolearn bkz [Azure Search dizin oluşturucu alan eşlemelerini köprü veri kaynakları ve arama dizinlerini hello farklarını](search-indexer-field-mappings.md).

## <a name="handle-document-keys"></a>Tanıtıcı belge anahtarları
Azure Search'te hello belge anahtarını bir belge benzersiz olarak tanımlar. Tüm arama dizini tam olarak bir anahtar alanı türünün olmalıdır `Edm.String`. Merhaba anahtar alanı toohello dizin eklenen her belge için gereklidir. (Hatta onun hello yalnızca alan gereklidir.)

Bileşik anahtar tablo satırları olduğu için Azure Search adlı yapay bir alan oluşturur `Key` bölüm anahtarını ve satır anahtar değerlerinin birleşimini olmasıdır. Örneğin, bir satır PartitionKey kullanıcının ise `PK1` ve RowKey `RK1`, ardından hello `Key` alanın değeri `PK1RK1`.

> [!NOTE]
> Merhaba `Key` değeri belge anahtarları, kısa çizgi gibi geçersiz karakterler içeriyor olabilir. Geçersiz karakterlerle hello kullanarak başa `base64Encode` [alan eşleme işlev](search-indexer-field-mappings.md#base64EncodeFunction). Bunu yaparsanız, API belge anahtarları geçirme gibi arama çağırdığında tooalso kullanım URL için güvenli Base64 kodlaması unutmayın.
>
>

## <a name="incremental-indexing-and-deletion-detection"></a>Artımlı dizin oluşturma ve silme algılama
Bir tablo dizin oluşturucu toorun bir zamanlamaya göre ayarladığınızda, bu satırın tarafından belirlendiği şekilde, yalnızca yeni veya güncelleştirilmiş satırları yeniden dizin oluşturur `Timestamp` değeri. Bir değişiklik algılama İlkesi toospecify yok. Artımlı dizin oluşturma sizin için otomatik olarak etkinleştirilir.

tooindicate belgeleri hello dizinden kaldırılması bu belirli, bir geçici silme stratejiyi kullanabilirsiniz. Bir satırın silinmesi yerine silinmiş ve hello veri kaynağında bir geçici silme algılama İlkesi ayarlama bir özellik tooindicate ekleyin. Örneğin, ilke aşağıdaki hello hello satır özelliğine sahipse satır silinir göz önünde bulundurur `IsDeleted` hello değerle `"true"`:

    PUT https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "table name", "query" : "<query>" },
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }   

<a name="Performance"></a>
## <a name="performance-considerations"></a>Performansla ilgili önemli noktalar

Varsayılan olarak Azure arama sorgu filtresi aşağıdaki hello kullanır: `Timestamp >= HighWaterMarkValue`. İkincil bir dizin üzerinde hello Azure tabloları olmadığından `Timestamp` alan, bu tür sorgu tam tablo taraması gerektirir ve bu nedenle büyük tablolar için yavaş sahiptir.


Burada, tablo dizin oluşturma performansı artırmak için iki olası yaklaşımlar bulunmaktadır. Bu yaklaşım her ikisi de tablo bölümlerini kullanır: 

- Verilerinizi birkaç bölüm aralığı doğal olarak bölümlenebilir varsa, bir veri kaynağı ve karşılık gelen bir dizin oluşturucu her bölüm aralığı için oluşturun. Her dizin oluşturucu, yalnızca bir belirli bir bölüm aralığı, sorgu daha iyi performans elde edilen tooprocess artık sahiptir. Dizine toobe gereken hello veri sabit bölümleri, daha iyi az sayıda varsa: her dizin oluşturucu yalnızca bir bölüm tarama yapar. Örneğin, gelen bir bölüm aralık işlemek için bir veri kaynağı toocreate anahtarları `000` çok`100`, böyle bir sorguyu kullanın: 
    ```
    "container" : { "name" : "my-table", "query" : "PartitionKey ge '000' and PartitionKey lt '100' " }
    ```

- Verilerinizi zamanına göre bölümlendiğinde ise (örneğin, her gün veya hafta yeni bir bölüm oluşturun), yaklaşımı izleyerek hello göz önünde bulundurun: 
    - Bir sorgu hello formunun kullanın: `(PartitionKey ge <TimeStamp>) and (other filters)`. 
    - Kullanarak dizin oluşturucu ilerleme durumunu izleyin [alma dizin oluşturucu durumu API](https://docs.microsoft.com/rest/api/searchservice/get-indexer-status)ve düzenli aralıklarla hello güncelleştirme `<TimeStamp>` hello son başarılı yüksek su işareti değere göre hello sorgusunun koşulu. 
    - Bu yaklaşımda, bir tam yeniden dizin oluşturmaya, tootrigger gerekiyorsa tooreset hello veri kaynağı sorgusu toplama tooresetting hello Oluşturucudaki gerekir. 


## <a name="help-us-make-azure-search-better"></a>Azure Search iyileştirmemize yardımcı olun
Özellik istekleri veya fikir geliştirmeleri için varsa, bunları gönderme sırasında bizim [UserVoice sitesinde](https://feedback.azure.com/forums/263029-azure-search/).
