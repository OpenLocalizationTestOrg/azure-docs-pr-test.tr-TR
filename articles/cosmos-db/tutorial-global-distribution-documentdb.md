---
title: "DocumentDB API için aaaAzure Cosmos DB genel dağıtım Öğreticisi | Microsoft Docs"
description: "Nasıl toosetup Azure Cosmos DB genel dağıtım kullanarak izin ver hello DocumentDB API öğrenin."
services: cosmos-db
keywords: "genel dağıtım, documentdb"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: a1d5f01faa62407fbbc9c078ef4a9589a1a29219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a>Nasıl toosetup Azure Cosmos DB genel dağıtım kullanarak izin ver hello DocumentDB API

Bu makalede, nasıl toouse Azure portal toosetup Azure Cosmos DB genel dağıtım hello ve hello DocumentDB API kullanarak bağlanmak gösterir.

Bu makalede görevleri aşağıdaki hello yer almaktadır: 

> [!div class="checklist"]
> * Genel dağıtım Hello Azure portal kullanarak yapılandırma
> * Hello kullanarak genel dağıtım yapılandırma [DocumentDB API'leri](documentdb-introduction.md)

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a>Tooa tercih edilen bölge Hello DocumentDB API kullanarak bağlanma

Sipariş tootake avantajlarından içinde [genel dağıtım](distribute-data-globally.md), istemci uygulamalarının hello sıralı kullanılan tooperform belge işlemleri bölgeleri toobe tercih listesi belirtebilirsiniz. Bu, başlangıç bağlantı İlkesi ayarlayarak yapılabilir. Hello Azure Cosmos DB hesap yapılandırmasını temel alarak, geçerli bölge kullanılabilirliği ve hello tercih listesi, belirtilen hello çoğu en iyi bitiş noktası tarafından DocumentDB SDK'sı tooperform yazma ve okuma işlemlerini hello seçilir.

Bu tercih listesi hello DocumentDB SDK'ları kullanarak bağlantı başlatırken belirtilir. Merhaba SDK'ları isteğe bağlı bir parametre "PreferredLocations" kabul Azure bölgeleri diğer bir deyişle sıralı bir listesi.

Merhaba SDK tüm yazma toohello geçerli yazma bölge otomatik olarak gönderir.

Tüm okuma toohello ilk kullanılabilir bölge hello PreferredLocations listesinde gönderilir. Merhaba isteği başarısız olursa, hello istemci hello listesi toohello sonraki bölgeyi başarısız ve benzeri.

Merhaba SDK'ları yalnızca tooread PreferredLocations içinde belirtilen hello bölgelerinden deneyecek. Bu nedenle, örneğin, hello veritabanı hesabı üç bölgelerde kullanılabilir, ancak PreferredLocations için iki hello yazma olmayan bölgeleri yalnızca hello istemci belirtir, sonra okuma yük devretme hello durumda bile hello yazma bölgesi dışında sunulacak.

Merhaba uygulaması hello geçerli yazma uç noktası doğrulayın ve uç nokta denetimi iki özellikleri, WriteEndpoint ve ReadEndpoint, SDK sürümü 1.8 ve üzeri kullanılabilir tarafından hello SDK tarafından seçilen okuyun.

Merhaba PreferredLocations özellik ayarlanmamışsa, tüm istekleri hello geçerli yazma bölgesinden sunulacak.

## <a name="net-sdk"></a>.NET SDK
Merhaba SDK kod değişiklikleri kullanılabilir. Bu durumda, hello SDK otomatik olarak her iki okuma yönlendirir ve toohello geçerli yazma bölge yazar.

Sürüm 1,8 ve sonraki hello .NET SDK'sı, hello ConnectionPolicy parametresi hello DocumentClient oluşturucusu için Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations adlı bir özelliğe sahiptir. Bu özellik koleksiyonu türünde `<string>` ve bölge adları listesi içermelidir. Merhaba hello bölge adı sütunu başına biçimlendirilen Hello dize değerleri [Azure bölgeleri] [ regions] , boşluk önce veya sonra hello ilk sayfa ve karakter sırasıyla en son.

Merhaba geçerli yazma ve okuma uç noktaları sırasıyla DocumentClient.WriteEndpoint ve DocumentClient.ReadEndpoint kullanılabilir.

> [!NOTE]
> Merhaba URL'leri hello uç noktalar için uzun süreli sabitleri düşünülmemelidir. Merhaba hizmet bunlar herhangi bir noktada güncelleştirebilir. Merhaba SDK bu değişikliği otomatik olarak yönetir.
>
>

```csharp
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;
  
ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooDocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a>NodeJS, JavaScript ve Python SDK'ları
Merhaba SDK kod değişiklikleri kullanılabilir. Bu durumda, SDK otomatik olarak doğrudan hello hem okur ve toohello geçerli yazma bölge yazar.

Sürüm 1,8 ve daha sonra her SDK'sının hello ConnectionPolicy parametre hello DocumentClient Oluşturucusu DocumentClient.ConnectionPolicy.PreferredLocations adlı yeni bir özellik için. Bu parametre olan bölge adlarının bir listesini alan bir dizeler dizisi. Merhaba bölge adı hello sütununda başına biçimli Hello adları [Azure bölgeleri] [ regions] sayfası. Önceden tanımlanmış hello sabitleri hello kolaylık nesne AzureDocuments.Regions kullanabilirsiniz

Merhaba geçerli yazma ve okuma uç noktaları sırasıyla DocumentClient.getWriteEndpoint ve DocumentClient.getReadEndpoint kullanılabilir.

> [!NOTE]
> Merhaba URL'leri hello uç noktalar için uzun süreli sabitleri düşünülmemelidir. Merhaba hizmet bunlar herhangi bir noktada güncelleştirebilir. Merhaba SDK bu değişikliği otomatik olarak işler.
>
>

NodeJS/Javascript için bir kod örneği aşağıdadır. Python ve Java hello izleyecek aynı düzeni.

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in hello following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize hello connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a>REST
Veritabanı hesabı birden çok bölgede kullanılabilir yapıldıktan sonra istemciler kendi kullanılabilirlik URI aşağıdaki hello üzerinde bir GET isteği gerçekleştirerek sorgulayabilir.

    https://{databaseaccount}.documents.azure.com/

Merhaba hizmet bölgeler ve bunların karşılık gelen Azure Cosmos DB uç noktası URI için hello çoğaltmaları listesini döndürür. Merhaba geçerli yazma bölge hello yanıt olarak belirtilir. Merhaba istemci hello uygun uç noktası daha fazla tüm REST API istekleri için daha sonra şu şekilde seçebilirsiniz.

Örnek yanıt

    {
        "_dbs": "//dbs/",
        "media": "//media/",
        "writableLocations": [
            {
                "Name": "West US",
                "DatabaseAccountEndpoint": "https://globaldbexample-westus.documents.azure.com:443/"
            }
        ],
        "readableLocations": [
            {
                "Name": "East US",
                "DatabaseAccountEndpoint": "https://globaldbexample-eastus.documents.azure.com:443/"
            }
        ],
        "MaxMediaStorageUsageInMB": 2048,
        "MediaStorageUsageInMB": 0,
        "ConsistencyPolicy": {
            "defaultConsistencyLevel": "Session",
            "maxStalenessPrefix": 100,
            "maxIntervalInSeconds": 5
        },
        "addresses": "//addresses/",
        "id": "globaldbexample",
        "_rid": "globaldbexample.documents.azure.com",
        "_self": "",
        "_ts": 0,
        "_etag": null
    }


* Tüm PUT, POST ve DELETE isteklerini gitmelidir belirtilen toohello URI yazma
* Tüm alır ve diğer salt okunur istekleri (örneğin sorgular) tooany endpoint hello istemcinin tercih gidebilir

Yazma isteklerini yalnızca tooread bölgeler 403 ("Yasak") HTTP hata koduyla başarısız olur.

Merhaba yazma bölge sonra değişirse hello istemcinin ilk bulma aşaması, sonraki toohello önceki yazma bölge 403 ("Yasak") HTTP hata koduyla başarısız olur yazar. Merhaba istemci sonra hello bölgelerin listesi yeniden tooget hello güncelleştirilmiş yazma bölge ALMANIZ gerekir.

Bu, bu öğreticinin tamamlanan kadar. Nasıl toomanage hello genel çoğaltılmış hesabınızı tutarlılığını okuyarak öğrenebilirsiniz [Azure Cosmos veritabanı tutarlılık düzeylerini](consistency-levels.md). Ve Azure Cosmos DB'de nasıl genel veritabanı çoğaltma hakkında daha fazla bilgi çalıştığı için bkz: [Azure Cosmos DB genel verilerle dağıtmak](distribute-data-globally.md).

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, hello aşağıdakileri yaptığınızdan:

> [!div class="checklist"]
> * Genel dağıtım Hello Azure portal kullanarak yapılandırma
> * Merhaba DocumentDB API'leri kullanılarak genel dağıtım yapılandırma

Toohello sonraki öğretici toolearn şimdi devam etmek için nasıl Azure Cosmos DB yerel öykünücüsü kullanarak yerel olarak toodevelop hello.

> [!div class="nextstepaction"]
> [Yerel olarak hello öykünücü ile geliştirme](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

