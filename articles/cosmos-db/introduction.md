---
title: aaaIntroduction tooAzure Cosmos DB | Microsoft Docs
description: "Azure Cosmos DB hakkında bilgi edinin. Bu genel olarak dağıtılan çok modelli veritabanı; düşük gecikme süresi, esnek ölçeklenebilirlik ve yüksek kullanılabilirlik için oluşturulmuştur."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: a855183f-34d4-49cc-9609-1478e465c3b7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: f2acbe99f425b2f07a62bbbb4324aa48f1037481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="welcome-tooazure-cosmos-db"></a>TooAzure Cosmos DB Hoş Geldiniz

Azure Cosmos DB, Microsoft’un genel olarak dağıtılan çok modelli veritabanıdır. Bir düğme Hello tıklatmayla Azure Cosmos DB tooelastically ve bağımsız olarak ölçek işleme ve depolama Azure'un coğrafi bölgeler arasında herhangi bir sayı sağlar. Diğer veritabanı hizmetlerinin sunamadığı kapsamlı [hizmet düzeyi sözleşmeleri](https://aka.ms/acdbsla) (SLA) ile birlikte aktarım hızı, gecikme süresi, kullanılabilirlik ve tutarlılık garantileri sunar.

![Azure Cosmos DB, Microsoft'un esnek ölçek artırma, garantili düşük gecikme süresi, beş tutarlılık modeli ve kapsamlı SLA garantisi ile genel olarak dağıtılmış veritabanı hizmetidir](./media/introduction/azure-cosmos-db.png)

## <a name="solutions-that-benefit-from-azure-cosmos-db"></a>Azure Cosmos DB'den yararlanan çözümler

Tüm [web, mobil, oyun ve IOT uygulamaları](use-cases.md) , gereksinim okuma ve yazma işlemleri oldukça büyük miktardaki toohandle üzerinde bir [genel](distribute-data-globally.md) çok çeşitli verileri Azure Cosmos DB'den 's faydalanırsınız için düşük yanıt süreleri ile ölçeklendirin [garanti](https://azure.microsoft.com/support/legal/sla/cosmos-db/) kullanılabilirlik, yüksek performans, düşük gecikme süresi ve ince ayarlanabilir tutarlılık.

## <a name="key-capabilities"></a>Temel işlevler
Genel olarak dağıtılmış veritabanı hizmet olarak Azure Cosmos DB ölçeklenebilir, yüksek oranda yanıt veren uygulamaları derleme yetenekleri toohelp aşağıdaki hello sağlar:

* **Anahtar teslimi genel dağıtım**
    * Yapabilecekleriniz [verilerinizi dağıtmak](distribute-data-globally.md) tooany sayısı [Azure bölgeleri](https://azure.microsoft.com/regions/), hello ile [bir düğmesini tıklatın](tutorial-global-distribution-documentdb.md). Bu, tooput verilerinizi burada kullanıcılarınızın hello düşük olası gecikme tooyour müşteriler sağlama olan sağlar. 
    * Azure Cosmos veritabanı kullanarak çok girişli API'leri, hello uygulama her zaman burada bölgeye en yakın hello ve istekleri toohello en yakın veri merkezinin göndereceğiniz bilir. Tüm olası hiçbir yapılandırma değişiklikleri, yazma bölgenizi ayarlamak ve istediğiniz ve hello gibi birçok salt okunur bölgeler rest sizin için gerçekleştirilir.

* **Çoklu veri modelleri ve verilere erişim ile veri sorgulamaya yönelik popüler API’ler**
    * Azure Cosmos DB yerel olarak oluşturulmuş hello atom kayıt sırası (ARS) tabanlı veri modeli, bunlarla sınırlı toodocument, grafik, anahtar-değer, tablo ve sütun veri modelleri dahil olmak üzere birden çok veri modelleri destekler.
    * Veri modelleri aşağıdaki hello API'ler, SDK'ları birden çok dilde kullanılabilir ile desteklenir:
        * [DocumentDB API'si](documentdb-introduction.md)
        * [MongoDB API’si](mongodb-introduction.md)
        * [Tablo API’si](table-introduction.md)
        * [Graph (Gremlin) API'si](graph-introduction.md)
        * Çok yakında başka veri modelleri de sağlanacaktır 

* **Aktarım hızı ve depolamayı dünyanın dört bir yanında, talep üzerine esnek bir şekilde ölçeklendirin**
    * Veritabanı aktarım hızını [saniye başına](request-units.md) ayrıntı düzeyinde kolayca ölçeklendirin ve dilediğiniz zaman değiştirin. 
    * Depolama boyutunu [saydam ve otomatik olarak](partition-data.md) toohandle boyutu gereksinimlerinizi şimdi ve sonsuza kadar.

* **Yüksek hızda yanıt veren ve görev açısından kritik uygulamalar oluşturun**
    * Azure Cosmos DB uçtan uca hello en düşük gecikme süresi 99 yüzdelik tooits müşteriler güvence altına alır. 
    * Bir tipik 1 KB öğesi için Cosmos DB okuma uçtan uca gecikme altında 10 ms garanti eder ve dizinli yazma hello 99, en altında 15 ms içinde hello aynı Azure bölgesi. Merhaba Medyan gecikme sürelerini önemli ölçüde düşebilir (5 ms altında).

* **"Her zaman açık" özelliği ile kullanılabilirlik endişeniz olmaz**
    * Tek bir bölge içinde %99,99 kullanılabilirlik.
    * Tooany sayısı dağıtmak [Azure bölgeleri](https://azure.microsoft.com/regions) yüksek kullanılabilirlik için.
    * Sıfır veri kaybı garantisi ile bir veya daha fazla bölgenin [hata benzetimini gerçekleştirin](regional-failover.md). 

* **Genel olarak dağıtılmış uygulamaların hello yazma sağ yolu**
    * Beş [tutarlılık modelleri](consistency-levels.md) modelleri tooNoSQL benzeri şekilde nihai tutarlılık ve her şey arasındaki tüm hello güçlü SQL benzeri tutarlılık yelpazesini sağlar. 
  
* **Para iadesi garantisi**
    * Verileriniz gitmesi gereken yere hızlı bir şekilde ulaşmazsa paranız iade edilir. 
    * Kullanılabilirlik, gecikme süresi, aktarım hızı ve tutarlılık için [hizmet düzeyi sözleşmeleri](https://aka.ms/acdbsla). 

* **Veritabanı şema/dizin yönetimi yok**
    * Veritabanı şema ve dizinlerinizi uygulamanızın şemasıyla eşitleme konusunda endişelenmeyi bırakın. Bizde şema yok. 
    * Azure Cosmos veritabanı veritabanı altyapısıdır tam şema belirsiz – herhangi bir şema veya dizinleri gerek kalmadan alır ve üstün hızlı sorguları hizmet tüm hello verileri otomatik olarak dizinler. 

* **Düşük sahip olma maliyeti**
    * Tooten beş [daha düşük maliyetli](https://aka.ms/cosmos-db-tco-paper) yönetilmeyen bir çözümden.
    * DynamoDB’den üç kat daha ucuz.

## <a name="capability-comparison"></a>Özellik karşılaştırması

Azure Cosmos DB ilişkisel ve ilişkisel olmayan veritabanlarının hello en iyi yetenekleri sağlar.

| Özellikler | İlişkisel veritabanları   | İlişkisel olmayan (NoSQL) veritabanları |    Azure Cosmos DB |
| --- | --- | --- | --- |
| Genel dağıtım | Hayır | Hayır | Evet, çok girişli API'lerle 30'dan fazla bölgede anahtar teslimi dağıtım|
| Yatay ölçeklendirme | Hayır | Evet | Evet, depolama ve aktarım hızını bağımsız olarak ölçeklendirebilirsiniz | 
| Gecikme süresi garantileri | Hayır | Evet | Evte, %99 oranında okumalar <10 ms ve yazmalar <15 ms | 
| Yüksek kullanılabilirlik | Hayır | Evet | Evet, Cosmos DB her zaman açıktır, PACELC dengelemeleri vardır, ayrıca otomatik ve el ile yük devretme seçenekleri sağlar|
| Veri modeli + API | İlişkisel + SQL | Çoklu model + OSS API’si | Çoklu model + SQL + OSS API’si (yakında daha fazlası sunulacak) |
| SLA’lar | Evet | Hayır | Evet, gecikme süresi, aktarım hızı, tutarlılık ve kullanılabilirlik için kapsamlı SLA’lar |


## <a name="next-steps"></a>Sonraki adımlar
Dört hızlı başlangıçtan biriyle Azure Cosmos DB kullanmaya başlayın:

* [Azure Cosmos DB'nin DocumentDB API’si ile çalışmaya başlama](create-documentdb-dotnet.md)
* [Azure Cosmos DB'nin MongoDB API’si ile çalışmaya başlama](create-mongodb-nodejs.md)
* [Azure Cosmos DB'nin Grafik API’si ile çalışmaya başlama](create-graph-dotnet.md)
* [Azure Cosmos DB'nin Tablo API’si ile çalışmaya başlama](create-table-dotnet.md)
