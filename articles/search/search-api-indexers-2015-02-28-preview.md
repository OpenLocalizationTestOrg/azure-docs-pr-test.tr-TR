---
title: "Dizin Oluşturucu işlemleri (Azure Search Hizmeti REST API'si: 2015-02-28-Önizleme) | Microsoft Docs"
description: "Dizin Oluşturucu işlemleri (Azure Search Hizmeti REST API'si: 2015-02-28-Önizleme)"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 42b5f85c-8304-4bc7-8e1e-a9c76b8ca25a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: eugenesh
ms.openlocfilehash: 4dd9591072b44eeabae6eac1182b4eea10fd4a22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="indexer-operations-azure-search-service-rest-api-2015-02-28-preview"></a>Dizin Oluşturucu işlemleri (Azure Search Hizmeti REST API'si: 2015-02-28-Önizleme)
> [!NOTE]
> Bu makalede hello dizin oluşturucular [2015-02-28-Önizleme REST API](search-api-2015-02-28-preview.md). Bu API sürümü Önizleme sürümleri belge ayıklama ile Azure Blob Storage dizinleyici ve Azure Table Storage dizin oluşturucu ve diğer geliştirmeler ekler. Merhaba API dizin oluşturucular dahil olmak üzere Azure SQL Database, Azure Vm'leri ve Azure Cosmos DB SQL Server'da, genel olarak kullanılabilir (GA) Dizinleyicileri de destekler.
> 
> 

## <a name="overview"></a>Genel Bakış
Azure arama, verilerinizi doğrudan bazı genel veri kaynakları ile hello gerek toowrite kod tooindex kaldırma tümleştirebilirsiniz. tooset yukarı bu up hello Azure Search API toocreate çağırın ve yönetme **dizin oluşturucular** ve **veri kaynakları**. 

Bir **dizin oluşturucu** veri kaynakları ile hedef arama dizinlerini bağlayan bir kaynaktır. Bir dizin oluşturucu yolları aşağıdaki hello kullanılır: 

* Merhaba veri toopopulate dizin tek seferlik bir kopyasını gerçekleştirin.
* Dizin hello veri kaynağında bir zamanlamaya göre değişiklikler ile eşitleyin. Merhaba zamanlaması hello dizin oluşturucu tanımının bir parçası değildir.
* İsteğe bağlı tooupdate gerektiği gibi bir dizin çağırır. 

Bir **dizin oluşturucu** düzenli güncelleştirmeler tooan dizin istediğinizde yararlıdır. Bir dizin oluşturucu tanımının bir parçası bir satır içi zamanlama ayarlamak veya çalıştırın kullanarak isteğe bağlı olarak [çalıştırmak dizin oluşturucu](#RunIndexer). 

A **veri kaynağı** hangi verilerin toobe gereken belirtir dizine, kimlik bilgileri tooaccess hello veri ve ilkeleri tooenable Azure Search tooefficiently belirleyin (gibi değiştirilmiş veya silinmiş bir veritabanı tablosundaki satırları) hello verilerde yapılan değişiklikler. Böylece birden çok dizin oluşturucu tarafından kullanılan bağımsız bir kaynak olarak tanımlanır.

şu anda aşağıdaki veri kaynaklar hello desteklenir:

* **Azure SQL veritabanı** ve **Azure Vm'lerde SQL Server**. Hedeflenen bir kılavuz için bkz: [bu makalede](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md). 
* **Azure Cosmos DB**. Hedeflenen bir kılavuz için bkz: [bu makalede](search-howto-index-documentdb.md). 
* **Azure Blob Storage**gibi hello aşağıdaki belge biçimleri: PDF, Microsoft Office (DOCX/DOC, XSLX/XLS, PPTX/PPT, MSG), HTML, XML, ZIP ve düz metin dosyaları (JSON dahil). Hedeflenen bir kılavuz için bkz: [bu makalede](search-howto-indexing-azure-blob-storage.md).
* **Azure Table Storage**. Hedeflenen bir kılavuz için bkz: [bu makalede](search-howto-indexing-azure-tables.md).

Biz hello gelecekteki ek veri kaynakları için destek ekleyen düşünüyorsunuz. Bize bu kararlar öncelik toohelp üzerinde hello bildirimlerinizi lütfen [Azure Search geri bildirim Forumunda](http://feedback.azure.com/forums/263029-azure-search).

Bkz: [hizmet sınırları](search-limits-quotas-capacity.md) ilgili tooindexer ve veri kaynağı kaynaklar maksimum sınırlar için.

## <a name="typical-usage-flow"></a>Tipik kullanım akışı
Oluşturma ve karşı Basit HTTP isteklerini (POST, GET, PUT, DELETE) aracılığıyla dizin oluşturucular ve veri kaynaklarını yönet bir verilen `data source` veya `indexer` kaynak.

Otomatik dizin oluşturmayı ayarlama genellikle dört adım bir işlemdir:

1. Dizine toobe gereken hello veri içeren hello veri kaynağını tanımlayın. Azure Search tüm hello veri türlerinin veri kaynağınızda mevcut desteklemeyebilir olduğunu aklınızda bulundurun. Bkz: [desteklenen veri türlerini](https://msdn.microsoft.com/library/azure/dn798938.aspx) hello listesi.
2. Şema veri kaynağınız ile uyumlu olan bir Azure Search dizini oluşturma.
3. Bir Azure Search veri kaynağı açıklandığı gibi oluşturmak [veri kaynağı oluştur](#CreateDataSource).
4. Bir Azure Search dizin oluşturucu açıklandığı gibi oluşturmak [oluşturma dizin oluşturucu](#CreateIndexer).

Her hedef dizinin ve veri kaynağı bileşimi için bir dizin oluşturucu oluşturma planlamanız gerekir. Birden çok dizin oluşturucu hello aynı yazma olabilir dizin ve hello yeniden aynı veri kaynağı için birden çok dizin oluşturucu. Ancak, bir dizin oluşturucu yalnızca tek bir veri kaynağı aynı anda tüketebileceği ve yalnızca tooa tek dizin yazabilirsiniz. 

Bir dizin oluşturucu oluşturduktan sonra yürütme durumunu hello kullanarak alabilirsiniz [dizin oluşturucu durumunu Al](#GetIndexerStatus) işlemi. Bir dizin oluşturucu herhangi bir zamanda çalıştırabilirsiniz (yerine veya toplama toorunning, düzenli bir zamanlamaya göre) hello kullanarak [çalıştırmak dizin oluşturucu](#RunIndexer) işlemi.

<!-- MSDN has 2 art files plus a API topic link list -->


## <a name="create-data-source"></a>Veri kaynağı oluşturun
Azure Search'te dizin oluşturucular hello bağlantı bilgilerinin anlık veya zamanlanan veri yenileme için bir hedef dizin sağlayarak ile bir veri kaynağı kullanılır. Bir HTTP POST isteği kullanarak Azure Search hizmeti içinde yeni bir veri kaynağı oluşturabilirsiniz.

    POST https://[service name].search.windows.net/datasources?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Alternatif olarak, PUT kullanın ve URI hello üzerinde hello veri kaynağı adı belirtin. Merhaba veri kaynağı mevcut değilse oluşturulur.

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]

> [!NOTE]
> Merhaba en fazla izin verilen veri kaynağı sayısını, fiyatlandırma katmanı tarafından değişir. Merhaba ücretsiz hizmet too3 veri kaynaklarını sağlar. Standart hizmeti 50 veri kaynakları sağlar. Bkz: [hizmet sınırları](search-limits-quotas-capacity.md) Ayrıntılar için.
> 
> 

**İstek**

HTTPS tüm hizmet istekleri için gereklidir. Merhaba **veri kaynağı oluştur** isteği POST veya PUT yöntemini kullanan olacak oluşturulan. POST kullanırken, bir veri kaynağı adı hello veri kaynağı tanımını birlikte hello istek gövdesindeki sağlamanız gerekir. PUT ile Merhaba adı hello URL bir parçasıdır. Merhaba veri kaynağı yoksa, oluşturulur. Zaten varsa, güncelleştirilmiş toohello yeni tanımı var. 

Merhaba veri kaynağı adı gerekir küçük olması, bir harf veya sayı ile başlamalı, hiçbir eğik çizgi veya nokta olan ve 128 karakterden kısa olmalıdır. Merhaba tire ardışık olmayan sürece hello veri kaynağı adı bir harf veya sayı ile başlattıktan sonra hello rest hello adının herhangi harf, sayı ve kısa çizgi, içerebilir. Bkz: [adlandırma kurallarını](https://msdn.microsoft.com/library/azure/dn857353.aspx) Ayrıntılar için.

Merhaba `api-version` gereklidir. Merhaba geçerli sürümü `2015-02-28`.

**İstek üstbilgileri**

liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar. 

* `Content-Type`: Gerekli. Bu çok ayarlama`application/json`
* `api-key`: Gerekli. Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil. Bu bir dize değeri, benzersiz tooyour hizmeti olur. Merhaba **veri kaynağı oluştur** isteği içermelidir bir `api-key` üstbilgi tooyour yönetici anahtarını (karşılıklı tooa sorgu anahtarı) olarak ayarlayın. 

Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir. Her iki hello hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello gelen [Azure Portal](https://portal.azure.com/). Bkz: [hello Portalı'nda arama hizmeti oluşturun](search-create-service-portal.md) sayfa gezinti Yardım.

<a name="CreateDataSourceRequestSyntax"></a>
**İstek gövdesi sözdizimi**

Merhaba gövdesi hello isteği, bir isteğe bağlı veri değişikliği algılama yanı sıra hello veri kaynağı, kimlik bilgileri tooread hello veri türü içeren bir veri kaynağı tanımını içerir ve verileri silme algılama kullanılan tooefficiently ilkeleri tanımlamak değiştirildi ya da düzenli olarak zamanlanmış bir dizin oluşturucu ile kullanıldığında hello veri kaynağındaki Silinen veriler. 

Merhaba isteği yükü yapılandırılması hello söz dizimi aşağıdaki gibidir. Örnek istek, bu konuda daha üzerinde sağlanır.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello data source",
        "description" : "Optional. Anything you want, or nothing at all",
        "type" : "Required. Must be one of 'azuresql', 'documentdb', 'azureblob', or 'azuretable'",
        "credentials" : { "connectionString" : "Required. Connection string for your data source" },
        "container" : { "name" : "Required. hello name of hello table, collection, or blob container you wish tooindex" },
        "dataChangeDetectionPolicy" : { Optional. See below for details }, 
        "dataDeletionDetectionPolicy" : { Optional. See below for details }
    }

İstek aşağıdaki özelliklere hello içerir: 

* `name`: Gerekli. Merhaba veri kaynağının Hello adı. Bir veri kaynağı adı gerekir yalnızca küçük harf, rakam veya kısa çizgi içerebilir, başlayamaz veya bitemez tireler ve sınırlı too128 karakterdir.
* `description`: İsteğe bağlı bir açıklama. 
* `type`: Gerekli. Merhaba desteklenen veri kaynağı türlerinden biri olmalıdır:
  * `azuresql`-Azure SQL veritabanı ya da Azure Vm'lerde SQL Server
  * `documentdb`-Azure Cosmos DB
  * `azureblob`-Azure Blob Depolama
  * `azuretable`-Azure tablo depolaması
* `credentials`:
  * gerekli hello `connectionString` özelliği hello hello veri kaynağına yönelik bağlantı dizesini belirtir. Merhaba bağlantı dizesinin Hello biçimi hello veri kaynağı türüne bağlıdır: 
    * Azure SQL için bu hello olağan SQL Server bağlantı dizesidir. Hello Azure portal tooretrieve hello bağlantı dizesi kullanıyorsanız hello kullanın `ADO.NET connection string` seçeneği.
    * Azure Cosmos DB hello bağlantı dizesi biçimi aşağıdaki hello olmalıdır: `"AccountEndpoint=https://[your account name].documents.azure.com;AccountKey=[your account key];Database=[your database id]"`. Merhaba değerlerin hepsi gereklidir. Hello bulabilirsiniz [Azure portal](https://portal.azure.com/).  
    * Azure Blob ve tablo depolama için hello depolama hesabı bağlantı dizesi budur. Merhaba biçimi açıklanmaktadır [burada](https://azure.microsoft.com/documentation/articles/storage-configure-connection-string/). HTTPS uç noktası protokol gereklidir.  
* `container`, gerekli: hello kullanarak hello veri tooindex belirtir `name` ve `query` özellikleri: 
  * `name`Gerekli:
    * Azure SQL: hello tablo veya Görünüm belirtir. Şema nitelenmiş adlar gibi kullanabilir `[dbo].[mytable]`.
    * DocumentDB: hello koleksiyonu belirtir. 
    * Azure Blob Storage: hello depolama kapsayıcısı belirtir.
    * Azure Table Storage: Merhaba tablonun hello adını belirtir. 
  * `query`, isteğe bağlı:
    * DocumentDB: toospecify bir rastgele JSON belge düzenini Azure Search dizin düz bir şemaya düzleştirir bir sorgu sağlar.  
    * Azure Blob Storage: toospecify hello blob kapsayıcı içindeki sanal bir klasör sağlar. Örneğin, blob yolu `mycontainer/documents/blob.pdf`, `documents` hello sanal klasörü olarak kullanılabilir.
    * Azure Table Storage: toospecify filtreleri içeri satırları toobe kümesi hello sorgu sağlar.
    * Azure SQL: Sorgu desteklenmiyor. Bu işlev gerekiyorsa, lütfen için oy [Bu öneri](https://feedback.azure.com/forums/263029-azure-search/suggestions/9893490-support-user-provided-query-in-sql-indexer)
* İsteğe bağlı Hello `dataChangeDetectionPolicy` ve `dataDeletionDetectionPolicy` özellikleri aşağıda açıklanmıştır.

<a name="DataChangeDetectionPolicies"></a>
**Veri değişikliği algılama ilkeleri**

bir veri Hello amacı değiştirme algılama İlkesi olduğunu tooefficiently tanımlamak değiştirilen veri öğeleri. Desteklenen ilkeleri hello veri kaynağı türüne göre farklılık gösterir. Aşağıdaki bölümler her ilke anlatmaktadır. 

***Üst eşik değişiklik algılama İlkesi*** 

Veri kaynağı bir sütun veya hello aşağıdaki ölçütleri karşılayan özellik içerdiğinde bu ilkeyi kullanın:

* Tüm eklemeleri hello sütun için bir değer belirtin. 
* Tüm güncelleştirmeler tooan öğesi de hello sütun hello değerini değiştirin. 
* Bu sütunun Hello değeri her değişiklikle artırır.
* Bir filtre yan tümcesi benzer toohello aşağıdakileri kullanan sorguları `WHERE [High Water Mark Column] > [Current High Water Mark Value]` verimli bir şekilde çalıştırılabilir.

Örneğin, Azure SQL veri kaynakları, bir dizinlenmiş kullanırken `rowversion` ideal bir aday hello hello yüksek su işareti İlkesi ile kullanmak için bir sütundur. 

Bu ilke şu şekilde belirtilebilir:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "[a row version or last_updated column name]" 
    } 

Azure Cosmos DB veri kaynakları kullanırken hello kullanmalısınız `_ts` Azure Cosmos DB tarafından sağlanan özelliği. 

Azure Blob veri kaynakları, Azure Search otomatik olarak kullanırken kullanan yüksek Filigran değiştirme algılama İlkesi bir blob'un son değiştirilen zaman damgasını tabanlı; Böyle bir ilke toospecify kendiniz gerekmez.   

***SQL ile tümleştirilen değişiklik algılama İlkesi***

SQL veritabanınız destekliyorsa [değişiklik izleme](https://msdn.microsoft.com/library/bb933875.aspx), SQL tümleşik değişiklik izleme ilkesi kullanmanızı öneririz. Bu ilke hello en verimli değişiklik izleme sağlar ve Azure Search tooidentify silinen satır toohave kalmadan şemanızı açık "geçici silme" sütununda verir.

Tümleşik değişiklik izleme SQL Server veritabanı sürümleri aşağıdaki hello ile başlayarak desteklenir: 

* SQL Server 2008 Azure Vm'lerinde SQL Server kullanıyorsanız, R2.
* Azure SQL veritabanı kullanıyorsanız, Azure SQL Database V12.  

Silinen satır zaman SQL tümleşik değişiklik izleme ilke kullanan bir ayrı veri silme algılama İlkesi belirlemezseniz - Bu ilkeyi tanımlamak için yerleşik destek yok. 

Bu ilke yalnızca tablolarla kullanılabilir; görünümlerle kullanılamaz. Bu ilkeyi kullanabilmek için kullanmakta olduğunuz hello tablosunda için tooenable değişiklik izleme gerekir. Bkz: [etkinleştirme ve değişiklik izlemeyi devre dışı](https://msdn.microsoft.com/library/bb964713.aspx) yönergeler için.    

Merhaba yapılandırırken **veri kaynağı oluştur** isteği, SQL tümleşik değişiklik izleme ilkesinin gibi belirtilebilir:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy" 
    }

<a name="DataDeletionDetectionPolicies"></a>
**Verileri silme algılama ilkeleri**

bir veri silme algılama İlkesi Hello amacı tooefficiently silinen veri öğeleri tanımlayın. Şu anda, yalnızca desteklenen hello hello ilkedir `Soft Delete` , silinen öğeleri hello değerine göre tanımlayan sağlayan ilkesini bir `soft delete` sütun veya hello veri kaynağı özelliği. Bu ilke şu şekilde belirtilebilir:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello column that specifies whether a row was deleted", 
        "softDeleteMarkerValue" : "hello value that identifies a row as deleted" 
    }

> [!NOTE]
> Yalnızca dize, tamsayı veya Boole değerleri sütunlarla desteklenir. Merhaba olarak kullanılan değer `softDeleteMarkerValue` hello karşılık gelen sütunun tamsayı veya Boole değerlerini tutan olsa bile bir dize olmalıdır. Örneğin, veri kaynağınızda görünen hello değeri 1 ise, kullanın `"1"` hello olarak `softDeleteMarkerValue`.    
> 
> 

<a name="CreateDataSourceRequestExamples"></a>
**İstek gövdesi örnekleri**

Toouse hello veri kaynağı bir zamanlamaya göre çalışan bir dizin oluşturucu ile düşünüyorsanız, bu örnek nasıl toospecify değiştirme ve silme gösterir algılama ilkeleri: 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy", "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }

Yalnızca toouse hello veri kaynağı için tek seferlik hello verilerin kopyasını düşünüyorsanız, hello ilkeleri atlanabilir:

    { 
        "name" : "asqldatasource",
        "description" : "anything you want, or nothing at all",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" }
    } 

**Yanıt**

Başarılı bir istek için: 201 oluşturuldu. 

<a name="UpdateDataSource"></a>

## <a name="update-data-source"></a>Veri kaynağını güncelleme
Bir HTTP PUT İsteği kullanarak varolan bir veri kaynağına güncelleştirebilirsiniz. Merhaba istek URI'SİNDEKİ hello veri kaynağı tooupdate hello adını belirtin:

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Merhaba `api-version` gereklidir. Merhaba geçerli sürümü `2015-02-28`. [Azure Search API sürümleri](https://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri hakkında daha fazla bilgi vardır.

Merhaba `api-key` bir yönetici anahtarı (karşılıklı tooa sorgu anahtarı) olması gerekir. Toohello kimlik doğrulaması bölümünde bakın [arama hizmeti REST API'si](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn anahtarları hakkında daha fazla. [Bir arama hizmeti hello Portalı'nda oluşturma](search-create-service-portal.md) tooget hello hizmet URL'si ve anahtar özellikleri hello istekte nasıl kullandığı açıklanmaktadır.

**İstek**

Merhaba istek gövdesi sözdizimi olduğu hello aynı [veri kaynağı oluştur istekleri](#CreateDataSourceRequestSyntax).

Mevcut bir veri kaynağında bazı özellikleri güncelleştirilemiyor. Örneğin, varolan bir veri kaynağını hello türünü değiştiremezsiniz.  

Varolan bir veri kaynağı için toochange hello bağlantı dizesi istemiyorsanız, hello değişmez değer belirtebilirsiniz `<unchanged>` hello bağlantı dizesi için. Bu, burada tooupdate bir veri kaynağı gerekiyor ancak güvenlik açısından duyarlı veri olduğundan uygun erişim toohello bağlantı dizesi yok durumlarda yararlıdır.

**Yanıt**

Başarılı bir istek için: yeni bir veri kaynağı varsa 201 oluşturuldu oluşturulan ve 204 Hayır varolan bir veri kaynağını güncelleştirildiyse içerik.

<a name="ListDataSource"></a>

## <a name="list-data-sources"></a>Veri kaynaklarını listele
Merhaba **liste veri kaynaklarının** işlemi, Azure Search hizmetinizin hello veri kaynaklarının listesini döndürür. 

    GET https://[service name].search.windows.net/datasources?api-version=[api-version]
    api-key: [admin key]

Merhaba `api-version` gereklidir. Merhaba geçerli sürümü `2015-02-28`. 

Merhaba `api-key` bir yönetici anahtarı (karşılıklı tooa sorgu anahtarı) olması gerekir. Toohello kimlik doğrulaması bölümünde bakın [arama hizmeti REST API'si](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn anahtarları hakkında daha fazla. [Bir arama hizmeti hello Portalı'nda oluşturma](search-create-service-portal.md) tooget hello hizmet URL'si ve anahtar özellikleri hello istekte nasıl kullandığı açıklanmaktadır.

**Yanıt**

Başarılı bir istek için: 200 Tamam.

Bir örnek yanıt gövdesi şöyledir:

    {
      "value" : [
        {
          "name": "datasource1",
          "type": "azuresql",
          ... other data source properties
        }]
    }

İlgilendiğiniz toojust hello özellikleri aşağı hello yanıt filtreleyebilirsiniz unutmayın. Örneğin, yalnızca veri kaynağı adları listesi istiyorsanız, hello OData kullanın `$select` sorgu seçeneği:

    GET /datasources?api-version=205-02-28&$select=name

Bu durumda, yukarıdaki örnek hello hello yanıttan şu şekilde görünür: 

    {
      "value" : [ { "name": "datasource1" }, ... ]
    }

Çok miktarda veri kaynaklarını arama hizmetiniz varsa yararlı yöntem toosave bant genişliği budur.

<a name="GetDataSource"></a>

## <a name="get-data-source"></a>Veri kaynağı Al
Merhaba **veri kaynağını almak** işlemi Azure aramadan hello veri kaynağı tanımını alır.

    GET https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

Merhaba `api-version` gereklidir. Merhaba geçerli sürümü `2015-02-28`. 

Merhaba `api-key` bir yönetici anahtarı (karşılıklı tooa sorgu anahtarı) olması gerekir. Toohello kimlik doğrulaması bölümünde bakın [arama hizmeti REST API'si](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn anahtarları hakkında daha fazla. [Bir arama hizmeti hello Portalı'nda oluşturma](search-create-service-portal.md) tooget hello hizmet URL'si ve anahtar özellikleri hello istekte nasıl kullandığı açıklanmaktadır.

**Yanıt**

Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.

Merhaba yanıt olan içinde benzer tooexamples [veri kaynağı oluştur örnek istekleri](#CreateDataSourceRequestExamples): 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName" : "IsDeleted", 
            "softDeleteMarkerValue" : "true" }
    }

> [!NOTE]
> Merhaba ayarlamayın `Accept` isteği üstbilgisi çok`application/json;odata.metadata=none` olduğunda Bunun yapılması olarak bu API'yi çağıran neden olacak `@odata.type` hello yanıt ve, atlanmış özniteliği toobe veri değişikliği ve verileri silme algılama arasında mümkün toodifferentiate olmayacak farklı türlerdeki ilkeleri. 
> 
> 

<a name="DeleteDataSource"></a>

## <a name="delete-data-source"></a>Veri kaynağı silinemiyor
Merhaba **veri kaynağı silme** işlemi, Azure Search hizmetiniz bir veri kaynağı kaldırır.

    DELETE https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> Tüm Dizin oluşturucuların silmekte olduğunuz hello veri kaynağına başvuran, hello silme işlemi hala devam edecek. Ancak, bu dizin oluşturucular kendi sonraki çalıştırma sırasında bir hata duruma geçer.  
> 
> 

Merhaba `api-version` gereklidir. Merhaba geçerli sürümü `2015-02-28`. 

Merhaba `api-key` bir yönetici anahtarı (karşılıklı tooa sorgu anahtarı) olması gerekir. Toohello kimlik doğrulaması bölümünde bakın [arama hizmeti REST API'si](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn anahtarları hakkında daha fazla. [Bir arama hizmeti hello Portalı'nda oluşturma](search-create-service-portal.md) tooget hello hizmet URL'si ve anahtar özellikleri hello istekte nasıl kullandığı açıklanmaktadır.

**Yanıt**

Durum kodu: 204 Hayır içerik için başarılı bir yanıt döndürülür.

<a name="CreateIndexer"></a>

## <a name="create-indexer"></a>Dizin Oluşturucu yapın
Bir HTTP POST isteği kullanarak Azure Search hizmeti içinde yeni bir dizin oluşturucu oluşturabilirsiniz.

    POST https://[service name].search.windows.net/indexers?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Alternatif olarak, PUT kullanın ve URI hello üzerinde hello veri kaynağı adı belirtin. Merhaba veri kaynağı mevcut değilse oluşturulur.

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]

> [!NOTE]
> Dizin oluşturucular izin verilen en fazla Hello fiyatlandırma katmanı tarafından değişir. Merhaba ücretsiz hizmet too3 dizin oluşturucular sağlar. Standart hizmeti 50 dizin oluşturucular sağlar. Bkz: [hizmet sınırları](search-limits-quotas-capacity.md) Ayrıntılar için.
> 
> 

Merhaba `api-version` gereklidir. Merhaba geçerli sürümü `2015-02-28`. 

Merhaba `api-key` bir yönetici anahtarı (karşılıklı tooa sorgu anahtarı) olması gerekir. Toohello kimlik doğrulaması bölümünde bakın [arama hizmeti REST API'si](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn anahtarları hakkında daha fazla. [Bir arama hizmeti hello Portalı'nda oluşturma](search-create-service-portal.md) tooget hello hizmet URL'si ve anahtar özellikleri hello istekte nasıl kullandığı açıklanmaktadır.

<a name="CreateIndexerRequestSyntax"></a>
**İstek gövdesi sözdizimi**

Merhaba hello istek gövdesi hello veri kaynağı ve dizin oluşturma, hem de isteğe bağlı dizin oluşturma zamanlama ve parametreler için hello hedef dizin belirten bir dizin oluşturucu tanımını içerir. 

Merhaba isteği yükü yapılandırılması hello söz dizimi aşağıdaki gibidir. Örnek istek, bu konuda daha üzerinde sağlanır.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello indexer",
        "description" : "Optional. Anything you want, or null",
        "dataSourceName" : "Required. hello name of an existing data source",
        "targetIndexName" : "Required. hello name of an existing index",
        "schedule" : { Optional. See Indexing Schedule below. },
        "parameters" : { Optional. See Indexing Parameters below. },
        "fieldMappings" : { Optional. See Field Mappings below. },
        "disabled" : Optional boolean value indicating whether hello indexer is disabled. False by default.  
    }

**Dizin Oluşturucu zamanlaması**

Bir dizin oluşturucu, isteğe bağlı olarak bir zamanlama belirtebilirsiniz. Bir zamanlama varsa hello dizin oluşturucu düzenli aralıklarla zamanlamaya göre çalışır. Zamanlama öznitelikleri aşağıdaki hello sahiptir:

* `interval`: Gerekli. Bir aralığı ya da dizin oluşturucu için süresi belirten bir süre değeri çalışır. en küçük Hello aralığı 5 dakika verilir; Merhaba uzun bir gündür. Bir XSD "dayTimeDuration" değeri biçimlendirilmelidir (sınırlı alt kümesi bir [ISO 8601 süre](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) değeri). Bu Hello deseni: `"P[nD][T[nH][nM]]"`. Örnekler: `PT15M` her 15 dakikada için `PT2H` için her 2 saatte bir. 
* `startTime`: Gerekli. Merhaba dizin oluşturucu çalıştıran başlattığınızda bir UTC datetime. 

**Dizin Oluşturucu parametreleri**

Bir dizin oluşturucu davranışını etkileyen çeşitli parametreler isteğe bağlı olarak belirtebilirsiniz. Tüm hello parametreleri isteğe bağlıdır.  

* `maxFailedItems`: Merhaba toobe başarısız öğe sayısı, dizin oluşturucunun çalıştırılması hata olarak kabul edilmeden önce dizini. Varsayılan 0'dır. Başarısız olan öğeler hakkında bilgi hello tarafından döndürülen [dizin oluşturucu durumunu Al](#GetIndexerStatus) işlemi. 
* `maxFailedItemsPerBatch`: Merhaba toobe başarısız öğe sayısı, dizin oluşturucunun çalıştırılması hata olarak kabul edilmeden önce her toplu işlemde dizine. Varsayılan 0'dır.
* `base64EncodeKeys`: Belge anahtarları base-64 kodlanmış olup olmadığını belirtir. Azure arama karakterlere yönelik kısıtlamalar bir belge anahtarında mevcut olabilecek getirir. Ancak, veri kaynağınızı hello değerleri geçersiz karakterler içeriyor olabilir. Gerekli tooindex gibi belge anahtarları olarak değerleri ise, bu bayrak tootrue ayarlayabilirsiniz. Varsayılan değer `false`.
* `batchSize`: Sipariş tooimprove performans tek bir toplu iş olarak hello hello veri kaynağından okumak ve dizinli öğe sayısını belirtir. Merhaba varsayılan hello veri kaynağı türüne bağlıdır: Azure SQL ve Azure Cosmos DB 1000 ve Azure Blob Storage için 10 olan.

**Alan eşlemeleri**

Alan eşlemeleri toomap bir alan adı hello veri kaynağı tooa farklı bir alan adı hello hedef dizinde kullanabilirsiniz. Örneğin, bir alan içeren bir kaynak tablo göz önünde bulundurun `_id`. Azure arama hello alan yeniden adlandırılamaz gerekir böylece bir alt çizgi ile başlayan bir alan adı izin vermez. Bu yapılabilir hello kullanarak `fieldMappings` şekilde hello dizin oluşturucu özelliği: 

    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ] 

Birden çok alan eşlemelerini belirtebilirsiniz: 

    "fieldMappings" : [ 
        { "sourceFieldName" : "_id", "targetFieldName" : "id" },
        { "sourceFieldName" : "_timestamp", "targetFieldName" : "timestamp" },
     ]

Hem kaynak hem de hedef alan adları büyük/küçük harfe duyarsızdır.

<a name="FieldMappingFunctions"></a>
***Alan eşleme işlevleri***

Alan eşlemelerini kullanılan tootransform kaynak alan değerlerini kullanarak da olabilir *işlevleri eşleme*.

Bu tür yalnızca bir işlev şu anda desteklenmemektedir: `jsonArrayToStringCollection`. Merhaba hedef dizin Collection(Edm.String) alanına bir JSON dizisi olarak biçimlendirilmiş bir dize içeren bir alanı ayrıştırır. SQL native koleksiyon veri türüne sahip olmadığından, Azure SQL Dizin Oluşturucu ile kullanılmak üzere özel olarak, yöneliktir. Aşağıdaki gibi kullanılabilir: 

    "fieldMappings" : [ { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } } ] 

Örneğin, hello kaynak alanı hello dize varsa `["red", "white", "blue"]`, sonra hello hedef alan türü `Collection(Edm.String)` hello üç değerlerle doldurulur `"red"`, `"white"` ve `"blue"`.

Bu hello Not `targetFieldName` özelliği isteğe bağlıdır; bırakılırsa hello `sourceFieldName` değeri kullanılır. 

<a name="CreateIndexerRequestExamples"></a>
**İstek gövdesi örnekleri**

Merhaba aşağıdaki örnekte oluşturur hello tarafından başvurulan hello tablosundan verileri kopyalayan bir dizin oluşturucu `ordersds` veri kaynağı toohello `orders` , 1 Ocak 2015 tarihinde da UTC başlar ve saatte çalışır bir zamanlamaya göre dizin. Her dizin oluşturucu çağrıldığında, en fazla 5 öğe her toplu iş içinde dizine toobe başarısız olursa ve en fazla 10 öğe toplam dizine toobe başarısız başarılı olur. 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }

**Yanıt**

Başarılı bir istek için 201 oluşturuldu.

<a name="UpdateIndexer"></a>

## <a name="update-indexer"></a>Dizin oluşturucusunu güncelleştirmek
Bir HTTP PUT İsteği kullanarak var olan bir dizin oluşturucu güncelleştirebilirsiniz. Merhaba istek URI'SİNDEKİ hello dizin oluşturucu tooupdate hello adını belirtin:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Merhaba `api-version` gereklidir. Merhaba geçerli sürümü `2015-02-28`. 

Merhaba `api-key` bir yönetici anahtarı (karşılıklı tooa sorgu anahtarı) olması gerekir. Toohello kimlik doğrulaması bölümünde bakın [arama hizmeti REST API'si](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn anahtarları hakkında daha fazla. [Bir arama hizmeti hello Portalı'nda oluşturma](search-create-service-portal.md) tooget hello hizmet URL'si ve anahtar özellikleri hello istekte nasıl kullandığı açıklanmaktadır.

**İstek**

Merhaba istek gövdesi sözdizimi olduğu hello aynı [oluşturma dizin oluşturucu istekleri](#CreateIndexerRequestSyntax).

**Yanıt**

Başarılı bir istek için: yeni bir dizin oluşturucu olduysa 201 oluşturuldu oluşturulan ve 204 Hayır varolan bir dizin oluşturucu güncelleştirildiyse içerik.

<a name="ListIndexers"></a>

## <a name="list-indexers"></a>Liste dizin oluşturucular
Merhaba **listesi dizin oluşturucular** işlemi Azure Search hizmetinizde dizin oluşturucular hello listesini döndürür. 

    GET https://[service name].search.windows.net/indexers?api-version=[api-version]
    api-key: [admin key]


Merhaba `api-version` gereklidir. Merhaba Önizleme sürümü `2015-02-28-Preview`. [Azure arama sürüm](https://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri hakkında daha fazla bilgi vardır.

Merhaba `api-key` bir yönetici anahtarı (karşılıklı tooa sorgu anahtarı) olması gerekir. Toohello kimlik doğrulaması bölümünde bakın [arama hizmeti REST API'si](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn anahtarları hakkında daha fazla. [Bir arama hizmeti hello Portalı'nda oluşturma](search-create-service-portal.md) tooget hello hizmet URL'si ve anahtar özellikleri hello istekte nasıl kullandığı açıklanmaktadır.

**Yanıt**

Başarılı bir istek için: 200 Tamam.

Bir örnek yanıt gövdesi şöyledir:

    {
      "value" : [
      {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        ... other indexer properties
      }]
    }

İlgilendiğiniz toojust hello özellikleri aşağı hello yanıt filtreleyebilirsiniz unutmayın. Örneğin, yalnızca dizin oluşturucu adlarının bir listesini istiyorsanız, hello OData kullanın `$select` sorgu seçeneği:

    GET /indexers?api-version=2014-10-20-Preview&$select=name

Bu durumda, yukarıdaki örnek hello hello yanıttan şu şekilde görünür: 

    {
      "value" : [ { "name": "myindexer" } ]
    }

Dizin oluşturucular çok arama hizmetiniz varsa yararlı yöntem toosave bant genişliği budur.

<a name="GetIndexer"></a>

## <a name="get-indexer"></a>Dizin Oluşturucu Al
Merhaba **alma dizin oluşturucu** işlemi Azure aramadan hello dizin oluşturucu tanımı alır.

    GET https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

Merhaba `api-version` gereklidir. Merhaba Önizleme sürümü `2015-02-28-Preview`. 

Merhaba `api-key` bir yönetici anahtarı (karşılıklı tooa sorgu anahtarı) olması gerekir. Toohello kimlik doğrulaması bölümünde bakın [arama hizmeti REST API'si](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn anahtarları hakkında daha fazla. [Bir arama hizmeti hello Portalı'nda oluşturma](search-create-service-portal.md) tooget hello hizmet URL'si ve anahtar özellikleri hello istekte nasıl kullandığı açıklanmaktadır.

**Yanıt**

Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.

Merhaba yanıt olan içinde benzer tooexamples [oluşturma dizin oluşturucu örnek istekleri](#CreateIndexerRequestExamples): 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }


<a name="DeleteIndexer"></a>

## <a name="delete-indexer"></a>Dizin Oluşturucu Sil
Merhaba **dizin oluşturucusunu silmek** işlemi bir dizin oluşturucu, Azure Search hizmetinden kaldırır.

    DELETE https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

Bir dizin oluşturucu silindiğinde, o anda devam eden hello dizin oluşturucu yürütmeleri toocompletion çalışacak, ancak başka hiçbir yürütmeleri zamanlanacak. Mevcut olmayan bir dizin oluşturucu HTTP durum kodu 404 sonuçlanır denemeleri toouse bulunamadı. 

Merhaba `api-version` gereklidir. Merhaba Önizleme sürümü `2015-02-28-Preview`. 

Merhaba `api-key` bir yönetici anahtarı (karşılıklı tooa sorgu anahtarı) olması gerekir. Toohello kimlik doğrulaması bölümünde bakın [arama hizmeti REST API'si](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn anahtarları hakkında daha fazla. [Bir arama hizmeti hello Portalı'nda oluşturma](search-create-service-portal.md) tooget hello hizmet URL'si ve anahtar özellikleri hello istekte nasıl kullandığı açıklanmaktadır.

**Yanıt**

Durum kodu: 204 Hayır içerik için başarılı bir yanıt döndürülür.

<a name="RunIndexer"></a>

## <a name="run-indexer"></a>Dizin Oluşturucu çalıştırın
Düzenli bir zamanlamaya göre ek toorunning içinde bir dizin oluşturucu hello aracılığıyla isteğe bağlı ayrıca çağrılabilir **çalıştırmak dizin oluşturucu** işlemi: 

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=[api-version]
    api-key: [admin key]

Merhaba `api-version` gereklidir. Merhaba Önizleme sürümü `2015-02-28-Preview`. 

Merhaba `api-key` bir yönetici anahtarı (karşılıklı tooa sorgu anahtarı) olması gerekir. Toohello kimlik doğrulaması bölümünde bakın [arama hizmeti REST API'si](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn anahtarları hakkında daha fazla. [Bir arama hizmeti hello Portalı'nda oluşturma](search-create-service-portal.md) tooget hello hizmet URL'si ve anahtar özellikleri hello istekte nasıl kullandığı açıklanmaktadır.

**Yanıt**

Durum kodu: 202 başarılı bir yanıt için kabul edilen döndürülür.

<a name="GetIndexerStatus"></a>

## <a name="get-indexer-status"></a>Dizin Oluşturucu durumunu Al
Merhaba **dizin oluşturucu durumunu Al** işlemi hello geçerli durumunu ve yürütme geçmişini bir dizin oluşturucu alır: 

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=[api-version]
    api-key: [admin key]


Merhaba `api-version` gereklidir. Merhaba Önizleme sürümü `2015-02-28-Preview`. 

Merhaba `api-key` bir yönetici anahtarı (karşılıklı tooa sorgu anahtarı) olması gerekir. Toohello kimlik doğrulaması bölümünde bakın [arama hizmeti REST API'si](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn anahtarları hakkında daha fazla. [Bir arama hizmeti hello Portalı'nda oluşturma](search-create-service-portal.md) tooget hello hizmet URL'si ve anahtar özellikleri hello istekte nasıl kullandığı açıklanmaktadır.

**Yanıt**

Durum kodu: 200 Tamam başarılı bir yanıt.

Merhaba yanıt gövdesi (varsa) son dizin oluşturucu çağrılarını hello geçmişini yanı sıra genel dizin oluşturucu sistem durumu, hello son dizin oluşturucu çağırma hakkında bilgiler içerir. 

Örnek yanıt gövdesi şöyle görünür: 

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

**Dizin Oluşturucu durumu**

Dizin Oluşturucu durum değerleri aşağıdaki hello biri olabilir:

* `running`Bu hello dizin oluşturucuyu normal şekilde çalışmadığını gösterir. İyi bir fikir toocheck hello olacak şekilde hello dizin oluşturucu yürütmeleri bazıları yine başarısız olabilir, Not `lastResult` özelliğini de. 
* `error`Bu hello dizin oluşturucuyu insan etkileşimi olmadan düzeltilemeyecek hatayla gösterir. Örneğin, hello veri kaynağı kimlik bilgilerinin süresi dolmuş olabilir veya hello şema hello veri kaynağının veya hello hedef dizinin sonu içinde değişti yolu. 

**Dizin Oluşturucu yürütme sonucu**

Bir dizin oluşturucu yürütme sonucu tek dizin oluşturucusu yürütme hakkında bilgiler içerir. Merhaba en son sonuç hello ortaya `lastResult` hello dizin oluşturucu durumu özelliği. Son diğer sonuçlar hello varsa, döndürülür `executionHistory` hello dizin oluşturucu durumu özelliği. 

Dizin Oluşturucu yürütme sonucu aşağıdaki özelliklere hello içerir: 

* `status`: Merhaba bir yürütme durumu. Bkz: [dizin oluşturucusu yürütme durumu](#IndexerExecutionStatus) aşağıda Ayrıntılar için. 
* `errorMessage`: başarısız yürütme için hata iletisi. 
* `startTime`: Bu yürütme başlatıldığında UTC olarak başlangıç zamanı.
* `endTime`: Bu yürütme bittikten UTC olarak başlangıç zamanı. Merhaba yürütme devam ediyor, bu değer ayarlanmaz.
* `errors`: öğe düzeyinde hataları, herhangi bir dizi. Her girişin bir belge anahtar içeriyor (`key` özelliği) ve bir hata iletisi (`errorMessage` özelliği). 
* `itemsProcessed`: Merhaba çalıştı dizin oluşturucu tooindex bu yürütme sırasında hello veri kaynağı öğesi (örneğin, tablo satırları) sayısı. 
* `itemsFailed`: Merhaba bu yürütme sırasında başarısız öğe sayısı.  
* `initialTrackingState`: her zaman `null` hello ilk dizin oluşturucusu yürütme için veya hello veri izleme ilkesi değiştirirseniz kullanılan hello veri kaynağı üzerinde etkin değil. Böyle bir ilke etkinleştirilirse, sonraki yürütmelerde içinde bu değer hello ilk (en düşük) değişiklik izleme bu yürütme tarafından işlenen değeri gösterir. 
* `finalTrackingState`: her zaman `null` hello verileri İzleme İlkesi değiştirirseniz kullanılan hello veri kaynağı üzerinde etkin değil. Aksi takdirde hello en son (yüksek) değişiklik izleme başarıyla bu yürütme tarafından işlenen değeri gösterir. 

<a name="IndexerExecutionStatus"></a>
**Dizin Oluşturucu yürütme durumu**

Dizin Oluşturucu yürütme durumu tek bir dizin oluşturucu yürütme hello durumunu yakalar. Değerleri aşağıdaki hello sahip olabilir:

* `success`Merhaba dizin oluşturucusu yürütme başarıyla tamamlanıp tamamlanmadığını gösterir.
* `inProgress`Merhaba dizin oluşturucusu yürütme devam ediyor gösterir. 
* `transientFailure`bir dizin oluşturucu yürütme başarısız olduğunu gösterir. Bkz: `errorMessage` özelliği ayrıntıları için. Merhaba hatası gerektirebilir veya İnsan eli toofix değil - bir geçici veri kaynağı kapalı kalma süresi çalışmazken örneğin hello veri kaynağı ile Merhaba hedef dizin arasındaki bir şema uyumsuzluğu düzeltme kullanıcı eylemi gerektirir. Var olan dizin oluşturucu çağrılarını zamanlama devam eder. 
* `persistentFailure`Bu hello dizin oluşturucuyu insan etkileşimi gerektiren bir şekilde başarısız oldu gösterir. Zamanlanmış dizin oluşturucu yürütmeleri durdurun. Merhaba sorunu çözdükten sonra sıfırlama dizin oluşturucu API toorestart zamanlanmış hello yürütmeleri kullanın. 
* `reset`Bu hello dizin oluşturucu çağrısı tooReset dizin oluşturucu API (aşağıda görebilirsiniz) tarafından sıfırlandı gösterir. 

<a name="ResetIndexer"></a>

## <a name="reset-indexer"></a>Dizin Oluşturucu Sıfırla
Merhaba **sıfırlama dizin oluşturucu** işlemi hello değişiklik izleme hello Dizin Oluşturucu ile ilişkili durumunu sıfırlar. Bu, tootrigger gelen-(örneğin, veri kaynağı şeması değişmişse) yeniden dizin oluşturma baştan ya da toochange hello veri değişikliği algılama İlkesi hello Dizin Oluşturucu ile ilişkili bir veri kaynağı için sağlar.   

    POST https://[service name].search.windows.net/indexers/[indexer name]/reset?api-version=[api-version]
    api-key: [admin key]

Merhaba `api-version` gereklidir. Merhaba Önizleme sürümü `2015-02-28-Preview`. 

Merhaba `api-key` bir yönetici anahtarı (karşılıklı tooa sorgu anahtarı) olması gerekir. Toohello kimlik doğrulaması bölümünde bakın [arama hizmeti REST API'si](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn anahtarları hakkında daha fazla. [Bir arama hizmeti hello Portalı'nda oluşturma](search-create-service-portal.md) tooget hello hizmet URL'si ve anahtar özellikleri hello istekte nasıl kullandığı açıklanmaktadır.

**Yanıt**

Durum kodu: 204 başarılı bir yanıt içeriği yok.

## <a name="mapping-between-sql-data-types-and-azure-search-data-types"></a>SQL veri türleri ve Azure Search'te veri türleri arasında eşleme
<table style="font-size:12">
<tr>
<td>SQL veri türü</td>    
<td>Hedef dizini izin alan türleri</td>
<td>Notlar</td>
</tr>
<tr>
<td>bit</td>
<td>Edm.Boolean, Edm.String</td>
<td></td>
</tr>
<tr>
<td>int, smallint, tinyint</td>
<td>EDM.Int32, EDM.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>bigint</td>
<td>EDM.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Gerçek, kayan nokta</td>
<td>Edm.Double, Edm.String</td>
<td></td>
</tr>
<tr>
<td>küçük para, para<br>Ondalık<br>sayısal
</td>
<td>Edm.String</td>
<td>Azure arama Bu duyarlık kaybeder çünkü Edm.Double ondalık türlerini dönüştürmeyi desteklemez
</td>
</tr>
<tr>
<td>karakter, n karakter, değişken karakter, n değişken karakter</td>
<td>Edm.String<br/>Collection(Edm.String)</td>
<td>Bkz: [alanı eşleme işlevleri](#FieldMappingFunctions) hakkında ayrıntılar için bu belgede tootransform bir Collection(Edm.String) dize sütununa</td>
</tr>
<tr>
<td>smalldatetime, datetime, datetime2, date, datetimeoffset</td>
<td>Edm.DateTimeOffset, Edm.String</td>
<td></td>
</tr>
<tr>
<td>uniqueidentifer</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>coğrafi konum</td>
<td>Edm.GeographyPoint</td>
<td>Yalnızca Coğrafya türünün örneklerini (Merhaba varsayılan değer olan) SRID 4326 NOKTASIYLA desteklenir</td>
</tr>
<tr>
<td>rowVersion</td>
<td>Yok</td>
<td>Satır sürümü sütunları hello arama dizinine depolanamaz ancak değişiklik izleme için kullanılabilir</td>
</tr>
<tr>
<td>zaman, timespan<br>ikili, değişken ikili, görüntü,<br>XML, geometri, CLR Türleri</td>
<td>Yok</td>
<td>Desteklenmiyor</td>
</tr>
</table>

## <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>JSON veri türleri ve Azure Search'te veri türleri arasında eşleme
<table style="font-size:12">
<tr>
<td>JSON veri türü</td>    
<td>Hedef dizini izin alan türleri</td>
<td>Notlar</td>
</tr>
<tr>
<td>bool</td>
<td>Edm.Boolean, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Tamsayı numaraları</td>
<td>EDM.Int32, EDM.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Kayan nokta sayıları</td>
<td>Edm.Double, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Dize</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>dizileri ilkel türleri, örneğin ["a", "b", "c"]</td>
<td>Collection(Edm.String)</td>
<td></td>
</tr>
<tr>
<td>Tarihleri gibi görünen dizeleri</td>
<td>Edm.DateTimeOffset, Edm.String</td>
<td></td>
</tr>
<tr>
<td>GeoJSON noktası nesneleri</td>
<td>Edm.GeographyPoint</td>
<td>GeoJSON noktalarıdır biçimini izleyen hello JSON nesneleri: {"tür": "Point", "coordinates": [uzun lat]} </td>
</tr>
<tr>
<td>Diğer JSON nesneleri</td>
<td>Yok</td>
<td>Desteklenmeyen; Azure arama şu anda yalnızca ilkel türler ve dize koleksiyonlarını destekler</td>
</tr>
</table>
