---
title: "aaaAzure Cosmos DB ölçek ve performans testi | Microsoft Docs"
description: "Nasıl tooperform ölçekleme ve performans Azure Cosmos DB ile test etme öğrenin"
keywords: Performans testi
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a>Performansı ve ölçeği Azure Cosmos DB ile test etme
Performans ve ölçek testi adımdır bir anahtar uygulama geliştirme. Birçok uygulama için hello veritabanı katmanı önemli bir etkisi vardır genel performans ve ölçeklenebilirlik hello ve bu nedenle önemli bir bileşeni performansını sınamak. [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) amaca esnek ölçek ve tahmin edilebilir performans ve bu nedenle yüksek performanslı veritabanı katmanı gereken uygulamalar için harika bir uygun değil. 

Bu makale, kendi Cosmos DB iş yükleri için performansı test paketleri uygulamadan veya yüksek performanslı uygulama senaryoları için Cosmos DB değerlendirme geliştiriciler için bir başvurudur. Yalıtılmış performans hello veritabanını öncelikle sınama odaklanır, ancak aynı zamanda üretim uygulamaları için en iyi yöntemleri içerir.

Bu makaleyi okuduktan sonra aşağıdaki soruları mümkün tooanswer hello olacaktır:   

* Cosmos DB performans testi için bir örnek .NET istemci uygulaması nereden bulabilirim? 
* My istemci uygulamasından nasıl Cosmos DB ile yüksek işleme düzeyleri elde?

tooget kodu ile başlatıldı, lütfen hello projeden indirin [Azure Cosmos DB performans testi örneği](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark). 

> [!NOTE]
> Merhaba, bu uygulamanın istemci makineleri az sayıda ile daha iyi performans Cosmos DB dışında ayıklanacağı toodemonstrate en iyi yöntemler hedeftir. Bu toodemonstrate hello yoğun genişlediğinden ölçeklendirebilirsiniz hello hizmet kapasitesini yapılmadı.
> 
> 

İstemci tarafı yapılandırma seçenekleri tooimprove Cosmos DB performans arıyorsanız bkz [Azure Cosmos DB performans ipuçları](performance-tips.md).

## <a name="run-hello-performance-testing-application"></a>Merhaba performans uygulama testi çalıştırma
hızlı şekilde tooget hello başlatılan toocompile çalışma hello .NET örnek aşağıda hello aşağıdaki adımlarda açıklandığı gibi ise. Ayrıca, hello kaynak kodu gözden geçirin ve benzer yapılandırmaları tooyour kendi istemci uygulamalarını uygulamak.

**1. adım:** indirme hello projeden [Azure Cosmos DB performans testi örneği](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), veya çatalı hello GitHub depo.

**2. adım:** EndpointUrl ve AuthorizationKey, CollectionThroughput ve DocumentTemplate (App.config dosyasında isteğe bağlı) hello ayarlarını değiştirin.

> [!NOTE]
> Yüksek verimlilik koleksiyonlarla sağlamadan önce lütfen toohello bakın [Fiyatlandırma sayfasında](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate hello maliyetleri koleksiyon başına. Azure Cosmos DB faturaları depolama ve işleme silerek veya test sonra Azure Cosmos DB koleksiyonlarınızı hello verimini azaltmayı maliyetleri kaydedebilmeniz için bağımsız olarak bir saatlik olarak.
> 
> 

**3. adım:** derleyip hello komut satırından hello konsol uygulamasını çalıştırın. Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


**(Gerekiyorsa) 4. adım:** bildirilen hello işleme (RU/s) hello aracından hello aynı ya da hello sağlanan işleme hello koleksiyonunun daha yüksek olmalıdır. Aksi durumda, artan hello DegreeOfParallelism küçük artışlarla hello sınırına ulaştığında yardımcı olabilir. İstemci uygulamanızı Hello akışından plateaus, üzerinde birden çok örneğini hello uygulama başlatma aynı hello veya farklı makinelerde sağlanan hello sınırı farklı örnekleri arasında hello ulaşmak yardımcı olur. Bu adım yardıma gereksinim duyarsanız, Lütfen bir e-posta yazma tooaskcosmosdb@microsoft.com veya bir destek bileti hello gelen dosya [Azure Portal](https://portal.azure.com).

Çalışan hello uygulama olduktan sonra farklı deneyebilirsiniz [ilkeleri dizin](indexing-policies.md) ve [tutarlılık düzeylerini](consistency-levels.md) toounderstand üretilen iş ve gecikmeyi üzerindeki etkilerini. Ayrıca hello kaynak kodu gözden geçirin ve benzer yapılandırmaları tooyour kendi test paketleri ya da üretim uygulamaları uygulayın.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, nasıl performansı ve ölçeği Cosmos DB bir .NET konsol uygulaması kullanarak test gerçekleştirebileceğiniz en arama. Azure Cosmos DB ile çalışma hakkında ek bilgi için lütfen aşağıdaki toohello bağlantılara bakın.

* [Azure Cosmos DB performans örnek testi](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [İstemci yapılandırma seçenekleri tooimprove Azure Cosmos DB performansı](performance-tips.md)
* [Sunucu tarafı Azure Cosmos DB'de bölümlendirme](partition-data.md)


