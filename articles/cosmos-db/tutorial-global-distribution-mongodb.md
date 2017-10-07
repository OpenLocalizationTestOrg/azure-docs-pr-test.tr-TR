---
title: "MongoDB API için aaaAzure Cosmos DB genel dağıtım Öğreticisi | Microsoft Docs"
description: "Nasıl toosetup Azure Cosmos DB genel dağıtım kullanarak izin ver hello MongoDB API öğrenin."
services: cosmos-db
keywords: "genel dağıtım, MongoDB"
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
ms.openlocfilehash: 0fc2d670bb4e21ac5f813f9586b407ba06ccf354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a>Nasıl toosetup Azure Cosmos DB genel dağıtım kullanarak izin ver hello MongoDB API

Bu makalede, nasıl toouse Azure portal toosetup Azure Cosmos DB genel dağıtım hello ve hello MongoDB API kullanarak bağlanmak gösterir.

Bu makalede görevleri aşağıdaki hello yer almaktadır: 

> [!div class="checklist"]
> * Genel dağıtım Hello Azure portal kullanarak yapılandırma
> * Hello kullanarak genel dağıtım yapılandırma [MongoDB API](mongodb-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a>Merhaba MongoDB API kullanarak bölgesel kurulumunuzu doğrulanıyor
en basit yolu MongoDB toorun hello için genel yapılandırmanızı API içinde denetleme çift Hello *isMaster()* hello Mongo kabuğunu komutunu.

Mongo kabuğunu:

   ```
      db.isMaster()
   ```
   
Örnek sonuçları:

   ```JSON
      {
         "_t": "IsMasterResponse",
         "ok": 1,
         "ismaster": true,
         "maxMessageSizeBytes": 4194304,
         "maxWriteBatchSize": 1000,
         "minWireVersion": 0,
         "maxWireVersion": 2,
         "tags": {
            "region": "South India"
         },
         "hosts": [
            "vishi-api-for-mongodb-southcentralus.documents.azure.com:10255",
            "vishi-api-for-mongodb-westeurope.documents.azure.com:10255",
            "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
         ],
         "setName": "globaldb",
         "setVersion": 1,
         "primary": "vishi-api-for-mongodb-southindia.documents.azure.com:10255",
         "me": "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
      }
   ```

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a>Tooa tercih edilen bölge Hello MongoDB API kullanarak bağlanma

Merhaba MongoDB API, toospecify genel olarak dağıtılmış bir veritabanı için okuma tercih koleksiyonunuzun sağlar. Her ikisi de düşük gecikme süresi okur ve genel yüksek kullanılabilirlik için koleksiyonunuzun okuma tercih çok ayarlamanız önerilir*yakın*. Bir okuma tercih *yakın* yapılandırılmış tooread hello en yakın bölgesinden olduğunu.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

Birincil uygulamalarla okuma/bölgeye ve bir ikincil bölge'olağanüstü durum kurtarma (DR) senaryoları yazma için koleksiyonunuzun okuma tercih çok ayarlamanız önerilir*tercih edilen ikincil*. Bir okuma tercih *tercih edilen ikincil* hello birincil bölge kullanılamıyor hello ikincil bölgesinden yapılandırılmış tooread olur.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

Son olarak, okuma, bölgeler gibi toomanually belirtirseniz. Okuma tercihinizi içinde hello bölge etiket ayarlayabilirsiniz.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
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
