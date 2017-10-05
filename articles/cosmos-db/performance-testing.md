---
title: "Azure Cosmos DB ölçek ve performans testi | Microsoft Docs"
description: "Ölçek ve performans ile Azure Cosmos DB testi gerçekleştirmek öğrenin"
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
ms.openlocfilehash: b5a1edd08819e82437c5b22d8eb131665d7c9645
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a>Performansı ve ölçeği Azure Cosmos DB ile test etme
Performans ve ölçek testi adımdır bir anahtar uygulama geliştirme. Birçok uygulama için veritabanı katmanı genel performans ve ölçeklenebilirlik üzerinde önemli bir etkisi vardır ve bu nedenle performans testi için kritik bir bileşen. [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) amaca esnek ölçek ve tahmin edilebilir performans ve bu nedenle yüksek performanslı veritabanı katmanı gereken uygulamalar için harika bir uygun değil. 

Bu makale, kendi Cosmos DB iş yükleri için performansı test paketleri uygulamadan veya yüksek performanslı uygulama senaryoları için Cosmos DB değerlendirme geliştiriciler için bir başvurudur. Yalıtılmış performans veritabanını öncelikle sınama odaklanır, ancak aynı zamanda üretim uygulamaları için en iyi yöntemleri içerir.

Bu makaleyi okuduktan sonra aşağıdaki soruları yanıtlayın mümkün olacaktır:   

* Cosmos DB performans testi için bir örnek .NET istemci uygulaması nereden bulabilirim? 
* My istemci uygulamasından nasıl Cosmos DB ile yüksek işleme düzeyleri elde?

Kodu ile çalışmaya başlamak için lütfen projeden indirin [Azure Cosmos DB performans testi örneği](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark). 

> [!NOTE]
> Bu uygulama amacı, az sayıda istemci makineleri ile daha iyi performans Cosmos DB dışında ayıklanacağı en iyi yöntemler göstermektir. Bu genişlediğinden ölçeklendirebilirsiniz hizmet yoğun kapasitesini göstermek için yapılmadı.
> 
> 

Cosmos DB performansını artırmak istemci tarafı yapılandırma seçenekleri arıyorsanız bkz [Azure Cosmos DB performans ipuçları](performance-tips.md).

## <a name="run-the-performance-testing-application"></a>Performans uygulama testi çalıştırma
Başlamak için en hızlı derlemek ve aşağıdaki adımları açıklandığı gibi .NET örnek aşağıda çalıştırmak için yoludur. Ayrıca, kaynak kodu gözden geçirin ve benzer yapılandırmaları için kendi istemci uygulamalarını uygulamak.

**1. adım:** projesinden indirmeniz [Azure Cosmos DB performans testi örneği](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), veya GitHub depoyu çatallaştırmanız.

**2. adım:** EndpointUrl ve AuthorizationKey, CollectionThroughput ve DocumentTemplate (App.config dosyasında isteğe bağlı) ayarlarını değiştirin.

> [!NOTE]
> Yüksek verimlilik koleksiyonlarla sağlamadan önce lütfen [Fiyatlandırma sayfasında](https://azure.microsoft.com/pricing/details/cosmos-db/) koleksiyon başına maliyetleri tahmin etme. Azure Cosmos DB faturaları depolama ve işleme silerek veya test sonra Azure Cosmos DB koleksiyonlarınızı verimini azaltmayı maliyetleri kaydedebilmeniz için bağımsız olarak bir saatlik olarak.
> 
> 

**3. adım:** derleyin ve komut satırından konsol uygulamasını çalıştırın. Aşağıdakine benzer bir çıktı görmeniz gerekir:

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


**(Gerekiyorsa) 4. adım:** bildirilen üretilen işi (RU/s) aracından aynı olması gerekir ya da daha yüksek sağlanan işleme koleksiyonu. Aksi durumda, küçük artışlarla DegreeOfParallelism artırma sınırına ulaştığında yardımcı olabilir. İstemci uygulamanızı akışından plateaus, birden çok örneğini aynı veya farklı makinelerde uygulama başlatma, farklı örneklerinde sağlanan sınırına ulaştığında yardımcı olur. Bu adım yardıma gereksinim duyarsanız, Lütfen bir e-posta yazma askcosmosdb@microsoft.com veya bir destek bileti gelen dosya [Azure Portal](https://portal.azure.com).

Uygulamayı oluşturduktan sonra farklı deneyebilirsiniz [ilkeleri dizin](indexing-policies.md) ve [tutarlılık düzeylerini](consistency-levels.md) üretilen iş ve gecikmeyi üzerindeki etkilerini anlamak için. Kaynak kodu gözden geçirmek ve kendi test paketleri ya da üretim uygulamaları için benzer yapılandırmaları uygulamak.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, nasıl performansı ve ölçeği Cosmos DB bir .NET konsol uygulaması kullanarak test gerçekleştirebileceğiniz en arama. Lütfen Azure Cosmos DB ile çalışma hakkında ek bilgi için aşağıdaki bağlantılara bakın.

* [Azure Cosmos DB performans örnek testi](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [Azure Cosmos DB performansını artırmak için istemci yapılandırma seçenekleri](performance-tips.md)
* [Sunucu tarafı Azure Cosmos DB'de bölümlendirme](partition-data.md)


