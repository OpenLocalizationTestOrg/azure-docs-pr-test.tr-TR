---
title: "Tablo API için aaaAzure Cosmos DB genel dağıtım Öğreticisi | Microsoft Docs"
description: "Nasıl toosetup Azure Cosmos DB genel dağıtım kullanarak izin ver hello tablo API öğrenin."
services: cosmos-db
keywords: "genel dağıtım, tablo"
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
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a>Nasıl toosetup Azure Cosmos DB genel dağıtım kullanarak izin ver hello tablo API

Bu makalede, nasıl toouse Azure portal toosetup Azure Cosmos DB genel dağıtım hello ve hello tablo API (Önizleme) kullanarak bağlanmak gösterir.

Bu makalede görevleri aşağıdaki hello yer almaktadır: 

> [!div class="checklist"]
> * Genel dağıtım Hello Azure portal kullanarak yapılandırma
> * Hello kullanarak genel dağıtım yapılandırma [tablo API](table-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a>Tooa tercih edilen bölge Hello tablo API kullanarak bağlanma

Sipariş tootake avantajlarından içinde [genel dağıtım](distribute-data-globally.md), istemci uygulamalarının hello sıralı kullanılan tooperform belge işlemleri bölgeleri toobe tercih listesi belirtebilirsiniz. Bu ayarı hello tarafından yapılabilir `TablePreferredLocations` hello uygulama yapılandırması hello Önizleme Azure depolama SDK'sı için yapılandırma değeri. Hello Azure Cosmos DB hesap yapılandırmasını temel alarak, geçerli bölge kullanılabilirliği ve belirtilen hello tercih listesi en iyi endpoint hello Azure depolama SDK'sı tooperform tarafından seçilir hello yazma ve okuma işlemleri.

Merhaba `TablePreferredLocations` okuma için tercih edilen (çok girişli) konumları, virgülle ayrılmış listesini içermelidir. Her istemci örneği, düşük gecikme süresi okumalar için tercih edilen hello sırayla Bu bölgeler kümesini belirtebilirsiniz. Merhaba bölgeler gerekir adlı kullanarak kendi [görünen adları](https://msdn.microsoft.com/library/azure/gg441293.aspx), örneğin, `West US`.

Tüm okuma toohello ilk kullanılabilir bölge hello gönderilecek `TablePreferredLocations` listesi. Merhaba isteği başarısız olursa, hello istemci hello listesi toohello sonraki bölgeyi başarısız ve benzeri.

Merhaba SDK yalnızca belirtilen hello bölgelerinden tooread denemesi `TablePreferredLocations`. Bu nedenle, örneğin, hello veritabanı hesabı üç bölgelerde kullanılabilir, ancak hello istemci yalnızca belirtir iki yazma olmayan bölgeleri için hello `TablePreferredLocations`, yük devretme hello durumda bile hello yazma bölgesi dışında okuma sunulacak sonra.

Merhaba SDK tüm yazma toohello geçerli yazma bölge otomatik olarak gönderir.

Merhaba, `TablePreferredLocations` özellik ayarlanmamışsa, tüm istekleri hello geçerli yazma bölgesinden sunulacak.

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
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
