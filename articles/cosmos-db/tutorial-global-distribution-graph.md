---
title: "Grafik API'si için aaaAzure Cosmos DB genel dağıtım Öğreticisi | Microsoft Docs"
description: "Nasıl toosetup Azure Cosmos DB genel dağıtım kullanarak izin ver hello grafik API'si hakkında bilgi edinin."
services: cosmos-db
keywords: "genel dağıtım, grafik, gremlin"
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a>Nasıl toosetup Azure Cosmos DB genel dağıtım kullanarak izin ver hello grafik API'si

Bu makalede, nasıl toouse Azure portal toosetup Azure Cosmos DB genel dağıtım hello ve hello grafik API'si (Önizleme) kullanarak bağlanmak gösterir.

Bu makalede görevleri aşağıdaki hello yer almaktadır: 

> [!div class="checklist"]
> * Genel dağıtım Hello Azure portal kullanarak yapılandırma
> * Hello kullanarak genel dağıtım yapılandırma [Graph API](graph-introduction.md) (Önizleme)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a>Tooa tercih edilen bölge Hello .NET SDK kullanarak hello grafik API'sini kullanarak bağlanma

Merhaba grafik API'si hello DocumentDB SDK'sı en üstünde bir uzantı kitaplığı olarak sunulur.

Sipariş tootake avantajlarından içinde [genel dağıtım](distribute-data-globally.md), istemci uygulamalarının hello sıralı kullanılan tooperform belge işlemleri bölgeleri toobe tercih listesi belirtebilirsiniz. Bu, başlangıç bağlantı İlkesi ayarlayarak yapılabilir. Hello Azure Cosmos DB hesap yapılandırmasını temel alarak, geçerli bölge kullanılabilirliği ve hello tercih listesi belirtilmezse, çoğu en iyi uç noktası hello SDK tooperform yazma tarafından seçilen ve okuma işlemlerini hello.

Bu tercih listesi hello SDK'ları kullanarak bağlantı başlatırken belirtilir. Merhaba SDK'ları isteğe bağlı bir parametre "PreferredLocations" kabul Azure bölgeleri diğer bir deyişle sıralı bir listesi.

* **Yazar**: SDK otomatik olarak tüm gönderecek hello toohello geçerli yazma bölge yazar.
* **Okur**: tüm okuma hello PreferredLocations listesinde toohello ilk kullanılabilir bölge gönderilir. Merhaba isteği başarısız olursa, hello istemci hello listesi toohello sonraki bölgeyi başarısız ve benzeri. Merhaba SDK'ları yalnızca tooread PreferredLocations içinde belirtilen hello bölgelerinden deneyecek. Bu nedenle, örneğin, hello Cosmos DB hesap üç bölgelerde kullanılabilir, ancak PreferredLocations için iki hello yazma olmayan bölgeleri yalnızca hello istemci belirtir, sonra okuma yük devretme hello durumda bile hello yazma bölgesi dışında sunulacak.

Merhaba uygulaması hello geçerli yazma uç noktası doğrulayın ve uç nokta denetimi iki özellikleri, WriteEndpoint ve ReadEndpoint, SDK sürümü 1.8 ve üzeri kullanılabilir tarafından hello SDK tarafından seçilen okuyun. Merhaba PreferredLocations özellik ayarlanmamışsa, tüm istekleri hello geçerli yazma bölgesinden sunulacak.

### <a name="using-hello-sdk"></a>Merhaba SDK kullanma

Örneğin, hello .NET SDK'sı, hello `ConnectionPolicy` parametresi hello için `DocumentClient` Oluşturucusu adlı bir özelliği vardır `PreferredLocations`. Bu özellik tooa bölge adları listesi ayarlayabilirsiniz. Merhaba görünen adları için [Azure bölgeleri] [ regions] parçası olarak belirtilen `PreferredLocations`.

> [!NOTE]
> Merhaba URL'leri hello uç noktalar için uzun süreli sabitleri düşünülmemelidir. Merhaba hizmet bunlar herhangi bir noktada güncelleştirebilir. Merhaba SDK bu değişikliği otomatik olarak yönetir.
>
>

```cs
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

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

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

