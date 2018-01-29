---
title: "SQL API için Azure Cosmos DB genel dağıtım Öğreticisi | Microsoft Docs"
description: "Kurulum SQL API'yi kullanarak Azure Cosmos DB genel dağıtım öğrenin."
services: cosmos-db
keywords: "Genel dağıtım"
documentationcenter: 
author: rafats
manager: jhubbard
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 05/10/2017
ms.author: rafats
ms.custom: mvc
ms.openlocfilehash: 0cee55673c8abca29b7e389fa4fd62a48566904b
ms.sourcegitcommit: 0e4491b7fdd9ca4408d5f2d41be42a09164db775
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-sql-api"></a>Kurulum SQL API'yi kullanarak Azure Cosmos DB genel dağıtım yapma

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)]

Bu makalede, Azure portalında Azure Cosmos DB genel dağıtım kurulumu ve SQL API'yi kullanarak bağlanmak için nasıl kullanılacağını gösterir.

Bu makalede aşağıdaki görevleri içerir: 

> [!div class="checklist"]
> * Azure portalını kullanarak genel dağıtım yapılandırma
> * Genel dağıtım kullanarak yapılandırma [SQL API'leri](sql-api-introduction.md)

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-sql-api"></a>SQL API'yi kullanarak bir tercih edilen bölge bağlanma

Anlamıyla yararlanabilmek için [genel dağıtım](distribute-data-globally.md), istemci uygulamaları, belge işlemlerini gerçekleştirmek için kullanılacak bölgelerin sıralı tercih listesi belirtebilirsiniz. Bu bağlantı İlkesi ayarlayarak yapılabilir. Azure Cosmos DB hesabı yapılandırması, geçerli bölge kullanılabilirliği ve belirtilen tercih listesi bağlı olarak, en iyi endpoint yazma gerçekleştirmek ve okuma işlemleri için SQL SDK tarafından seçilir.

Bu tercih listesi SQL SDK'ları kullanarak bağlantı başlatırken belirtilir. SDK'ları isteğe bağlı bir parametre "PreferredLocations" kabul Azure bölgeleri diğer bir deyişle sıralı bir listesi.

SDK, bölge geçerli tüm yazma işlemlerini yazma otomatik olarak gönderir.

İlk kullanılabilir bölge PreferredLocations listesindeki tüm okuma gönderilir. İstek başarısız olursa, istemci listeyi sonraki bölgeyi başarısız ve benzeri.

SDK'ları yalnızca PreferredLocations içinde belirtilen bölgeler okuma dener. Bu nedenle, örneğin, veritabanı hesabı dört bölgelerde kullanılabilir, ancak istemci PreferredLocations için yalnızca iki read(non-write) bölgede belirtir, sonra okuma PreferredLocations içinde belirtilmemiş okuma bölgesi dışında sunulacak. PreferredLocations belirtilen okuma bölgeleri kullanılabilir değilse, okuma, yazma bölgesinin dışına sunulacak.

Uygulama, geçerli yazma uç noktası doğrulayın ve WriteEndpoint ve ReadEndpoint, SDK sürümü 1.8 ve üzeri kullanılabilir iki özelliklerini denetleyerek SDK tarafından seçilen endpoint okuyun.

PreferredLocations özellik ayarlanmamışsa, tüm istekleri geçerli yazma bölgesinden sunulacak.

## <a name="net-sdk"></a>.NET SDK
SDK kod değişiklikleri kullanılabilir. Bu durumda, SDK'yı otomatik olarak her iki okuma yönlendirir ve geçerli yazma bölgesine yazar.

Sürüm 1,8 ve daha sonra .NET SDK'sına, ConnectionPolicy parametresi DocumentClient oluşturucusu için Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations adlı bir özelliğe sahiptir. Bu özellik koleksiyonu türünde `<string>` ve bölge adları listesi içermelidir. Üzerinde biçimlendirilen dize değerleri bölge adı sütun başına [Azure bölgeleri] [ regions] boşluk önce veya sonra ilk sayfasında ve karakter sırasıyla en son.

Geçerli yazma ve okuma uç noktaları sırasıyla DocumentClient.WriteEndpoint ve DocumentClient.ReadEndpoint kullanılabilir.

> [!NOTE]
> Uç noktalar için URL'leri uzun süreli sabitleri düşünülmemelidir. Hizmet, bunlar herhangi bir noktada güncelleştirebilir. SDK, bu değişiklik otomatik olarak yönetir.
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

// connect to DocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a>NodeJS, JavaScript ve Python SDK'ları
SDK kod değişiklikleri kullanılabilir. Bu durumda, SDK'yı otomatik olarak okuma ve yazma geçerli bölge yazma yönlendirir.

Sürüm 1,8 ve her SDK'ın daha sonra ConnectionPolicy parametresi DocumentClient oluşturucusu için yeni bir özellik DocumentClient.ConnectionPolicy.PreferredLocations çağrılır. Bu parametre olan bölge adlarının bir listesini alan bir dizeler dizisi. Bölge adı sütununda başına biçimli adları [Azure bölgeleri] [ regions] sayfası. Önceden tanımlanmış sabitleri kolaylık nesnesinde AzureDocuments.Regions kullanabilirsiniz

Geçerli yazma ve okuma uç noktaları sırasıyla DocumentClient.getWriteEndpoint ve DocumentClient.getReadEndpoint kullanılabilir.

> [!NOTE]
> Uç noktalar için URL'leri uzun süreli sabitleri düşünülmemelidir. Hizmet, bunlar herhangi bir noktada güncelleştirebilir. SDK bu değişikliği otomatik olarak işler.
>
>

NodeJS/Javascript için bir kod örneği aşağıdadır. Python ve Java aynı düzeni izler.

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in the following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize the connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a>REST
Veritabanı hesabı birden çok bölgede kullanılabilir yapıldıktan sonra istemciler aşağıdaki URI üzerinde bir GET isteği gerçekleştirerek, kullanılabilirlik sorgulayabilir.

    https://{databaseaccount}.documents.azure.com/

Hizmet bölgeler ve bunların karşılık gelen Azure Cosmos DB uç noktası URI için çoğaltmaları listesini döndürür. Geçerli yazma bölgeyi yanıtında gösterilir. İstemci ardından aşağıdaki gibi daha fazla tüm REST API istekleri için uygun uç noktası seçebilirsiniz.

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


* Tüm PUT, POST ve DELETE isteklerini belirtilen yazma URI gitmeniz gerekir
* Tüm alır ve diğer salt okunur istekleri (örneğin sorgular) için istemcinin istediği herhangi bir uç nokta gidebilir

Yazma isteklerini salt okunur bölgelere 403 ("Yasak") HTTP hata koduyla başarısız olur.

Yazma bölge sonra istemcinin ilk bulma aşama değişirse, önceki yazma bölgeye sonraki yazma 403 ("Yasak") HTTP hata koduyla başarısız olur. İstemci, daha sonra yeniden güncelleştirilmiş yazma bölge almak için bölgelerin listesi ALMANIZ gerekir.

Bu, bu öğreticinin tamamlanan kadar. Genel olarak çoğaltılmış hesabınızı tutarlılığını okuyarak yönetmek nasıl öğrenebilirsiniz [Azure Cosmos veritabanı tutarlılık düzeylerini](consistency-levels.md). Ve Azure Cosmos DB'de nasıl genel veritabanı çoğaltma hakkında daha fazla bilgi çalıştığı için bkz: [Azure Cosmos DB genel verilerle dağıtmak](distribute-data-globally.md).

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, aşağıdakileri yaptığınızdan:

> [!div class="checklist"]
> * Azure portalını kullanarak genel dağıtım yapılandırma
> * SQL API'lerini kullanarak genel dağıtım yapılandırma

Artık Azure Cosmos DB yerel öykünücüsü kullanarak yerel olarak geliştirme konusunda bilgi almak için sonraki öğretici devam edebilirsiniz.

> [!div class="nextstepaction"]
> [Yerel olarak öykünücü ile geliştirme](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

