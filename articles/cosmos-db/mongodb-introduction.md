---
title: "Giriş tooAzure Cosmos DB: API MongoDB için | Microsoft Docs"
description: "Sorgu büyük birimleri düşük gecikme süresi kullanarak JSON belgelerinin popüler OSS MongoDB API'leri hello ve Azure Cosmos DB toostore nasıl kullanacağınızı öğrenin."
keywords: MongoDB nedir
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 4afaf40d-c560-42e0-83b4-a64d94671f0a
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: anhoh
ms.openlocfilehash: 1eb88014cc4809332e3f5c109a44a55814194934
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-api-for-mongodb"></a>Giriş tooAzure Cosmos DB: API MongoDB için

[Azure Cosmos DB](../cosmos-db/introduction.md), Microsoft'un görev açısından kritik uygulamalar için genel olarak dağıtılmış çok modelli veritabanı hizmetidir. Azure Cosmos DB sağlar [anahtar teslim genel dağıtım](distribute-data-globally.md), [üretilen iş ve depolama esnek ölçeklendirme](partition-data.md) dünya, tek basamaklı milisaniyelik gecikme hello 99, adresindeki [beş iyi tanımlanmış tutarlılık düzeylerini](consistency-levels.md), yüksek oranda kullanılabilirlik, tarafından yedeklenen tüm garanti [endüstri lideri SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure Cosmos DB [verileri otomatik olarak dizinler](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) toodeal şema ve dizin yönetimi ile gerektirmeden. Çok modelli olan bu hizmet belge, anahtar-değer, grafik ve sütunlu veri modellerini destekler. 

![Azure Cosmos DB: MongoDB API](./media/mongodb-introduction/cosmosdb-mongodb.png) 

Cosmos DB veritabanları için yazılmış uygulamalar için hello veri deposu olarak kullanılabilir [MongoDB](https://docs.mongodb.com/manual/introduction/). Varolan kullanarak buna [sürücüleri](https://docs.mongodb.org/ecosystem/drivers/), uygulamanızın MongoDB, şimdi Cosmos DB ile iletişim kurmak ve Cosmos DB veritabanları MongoDB veritabanı yerine kullanmak için yazılmış. Çoğu durumda, sadece bir bağlantı dizesi değiştirilerek MongoDB tooCosmos DB kullanarak geçiş yapabilirsiniz. Bu işlevini kullanarak, kolayca oluşturabilir ve hello Azure çalışma MongoDB veritabanı uygulamalarında bulut ile Azure Cosmos veritabanı genel dağıtım ve [kapsamlı endüstri lideri SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db), toouse tanıdık devam ederken becerileri ve araçları MongoDB için.


## <a name="what-is-hello-benefit-of-using-azure-cosmos-db-for-mongodb-applications"></a>MongoDB uygulamaları için Azure Cosmos DB kullanarak hello avantajı nedir?

**Esnek bir şekilde ölçeklenebilir işleme ve Depolama:** kolayca yukarı veya, MongoDB veritabanı toomeet uygulamanız gerekir. Verileriniz düşük tahmin edilebilirliğe sahip gecikme süreleri sağlamak için katı hal disklerinde (SSD) depolanır. Cosmos DB destekleyen toovirtually ölçeklendirebilirsiniz MongoDB koleksiyonları sınırsız depolama boyutlarına ve sağlanan işleme. Uygulamanız büyüdükçe, Özellikler esnek Cosmos DB tahmin edilebilir performansla sorunsuz bir şekilde ölçeklendirebilirsiniz. 

**Bölgeli çoğaltma:** Cosmos DB saydam çoğaltır, veri tooall bölgeleri ilgili MongoDB hesabınızla arasında bileşim sağlarken genel erişim toodata gerektiren toodevelop uygulamalar etkinleştirme tutarlılık, kullanılabilirlik ve performans, tüm ilgili garanti ile. Cosmos DB saydam bölgesel yük devretmesi çok girişli API'leri ve hello özelliği tooelastically ölçek işleme ve depolama ile Merhaba Dünya çapında sağlar. Daha fazla bilgi edinin [verilerini genel dağıtmak](distribute-data-globally.md).

**MongoDB Uyumluluk**: Varolan MongoDB uzmanlık, uygulama kodu ve araçları kullanabilirsiniz. MongoDB kullanarak uygulamaları geliştirmek ve bunları tooproduction dağıtma hello tam olarak kullanarak yönetilen Genel dağıtılmış Cosmos DB hizmeti.

**Hiçbir Sunucu Yönetimi**: yoksa toomanage ve MongoDB veritabanlarınızı ölçeklendirin. Cosmos DB, toomanage herhangi bir altyapı ya da sanal makineleri kendiniz gerekmediği anlamına gelir tam olarak yönetilen bir hizmettir. Cosmos DB kullanılabilir 30 + [Azure bölgeleri](https://azure.microsoft.com/regions/services/).

**İnce ayarlanabilir tutarlılık düzeyleri:** iyi tanımlanmış tutarlılık düzeyleri tooachieve tutarlılık ve performans arasında en iyi dengeyi beş seçin. Sorgular ve okuma işlemleri için Cosmos DB beş farklı tutarlılık düzeyi sunar: güçlü, sınırlanmış eskime durumu, oturum, tutarlı öneki ve son. Bu ayrıntılı ve iyi tanımlanmış tutarlılık düzeyleri toomake ses dengelemeler tutarlılık, kullanılabilirlik ve gecikme süresi arasında izin verin. Daha fazla bilgi edinin [toomaximize kullanılabilirlik ve performans düzeyleri tutarlılık kullanarak](consistency-levels.md).

**Otomatik dizin oluşturma**: varsayılan olarak, Cosmos DB otomatik olarak tüm hello özellikleri, MongoDB veritabanı belgelerde içinde dizinler ve beklediğiniz veya herhangi bir şemayı ya da ikincil dizinlerin oluşturulmasını gerektirir.

**Kurumsal düzeyde** -Azure Cosmos DB yerel ve bölgesel hatalar hello karşılaştıkları birden çok yerel yinelemeler toodeliver % 99,99 kullanılabilirlik ve veri korumasını destekler. Azure Cosmos DB sahip kurumsal düzeyde [uyumluluk sertifikalarından](https://www.microsoft.com/trustcenter) ve güvenlik özellikleri. 

Bu Azure Cuma Scott Hanselman ve Azure Cosmos DB sorumlu mühendislik Yöneticisi, Kirill Gavrylyuk ile video edinin.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Introducing-Azure-Cosmos-DB/player]
> 

## <a name="how-tooget-started"></a>Tooget nasıl başlatılacağını

Merhaba MongoDB quickstarts toocreate Cosmos DB hesap izleyin ve, varolan Mongo DB uygulama toouse Cosmos DB geçirmek veya yeni bir tane oluşturun:

* [Var olan bir Node.js MongoDB web uygulamaya geçirmek](create-mongodb-nodejs.md).
* [.NET ve hello Azure portal ile bir MongoDB API web uygulaması oluşturma](create-mongodb-dotnet.md)
* [Java ve hello Azure portal ile bir API MongoDB konsol uygulaması oluşturma](create-mongodb-java.md)

## <a name="next-steps"></a>Sonraki adımlar

Azure Cosmos veritabanı MongoDB API'si hakkında bilgi genel Azure Cosmos DB belgelerine hello tümleştirilmiştir, ancak başlattığınız birkaç işaretçileri tooget şunlardır:

* Merhaba izleyin [tooa MongoDB hesabını bağlaması](connect-mongodb-account.md) öğretici toolearn nasıl tooget hesabı bağlantı dizesi bilgilerinizi.
* Merhaba izleyin [Azure Cosmos DB ile kullanım MongoChef](mongodb-mongochef.md) öğretici toolearn nasıl toocreate Azure Cosmos DB veritabanı MongoChef MongoDB uygulamada arasında bir bağlantı.
* Merhaba izleyin [MongoDB için protokol desteği ile veri tooAzure Cosmos DB geçirmek](mongodb-migrate.md) öğretici tooimport veri tooan API MongoDB veritabanı için.
* Tooan API MongoDB hesabı kullanarak bağlanmak [Robomongo](mongodb-robomongo.md).
* Kaç tane RUs işletim ile hello kullanarak bilgi [GetLastRequestStatistics komut ve Azure portal ölçümleri hello](request-units.md#GetLastRequestStatistics).
* Nasıl çok öğrenin[Genel dağıtılmış uygulamalar için okuma tercihleri yapılandırmak](../cosmos-db/tutorial-global-distribution-mongodb.md).
