---
title: "Akış analizi için aaaJSON çıkış | Microsoft Docs"
description: "Stream Analytics Veri arşivleme ve düşük gecikme süreli sorguları yapılandırılmamış JSON verileri için JSON çıktı için Azure Cosmos DB nasıl hedefleyebilirsiniz öğrenin."
keywords: "JSON çıktısını"
documentationcenter: 
services: stream-analytics,documentdb
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 5d2a61a6-0dbf-4f1b-80af-60a80eb25dd1
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: fa717818c839ecd7a60fcee33d22011990fd5878
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="target-azure-cosmos-db-for-json-output-from-stream-analytics"></a>Hedef Azure Stream Analytics JSON çıktısını Cosmos DB
Akış analizi hedef [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) veri arşivleme ve düşük gecikme süreli sorguları yapılandırılmamış JSON verileri JSON çıktısını için etkinleştirme. Bu belgede, bu yapılandırmayı uygulamak için bazı en iyi yöntemler kapsar.

Kişiler için Cosmos DB ile iyi tanımıyorsanız, bir göz atalım [Azure Cosmos veritabanı öğrenme yolu](https://azure.microsoft.com/documentation/learning-paths/documentdb/) tooget başlatıldı. 

Not: Mongo DB API Cosmos DB dayalı koleksiyonlar şu anda desteklenmiyor. 

## <a name="basics-of-cosmos-db-as-an-output-target"></a>Cosmos DB bir çıktı hedefi olarak temelleri
Hello Stream Analytics Azure Cosmos DB çıktısında sonuçları, Cosmos DB collection(s) JSON çıkış olarak işleme akışınızı yazılmasını etkinleştirir. Akış analizi oluşturmaz koleksiyonları veritabanınızda, bunun yerine, gerektiren toocreate bunları önceden. Bu, böylelikle hello fatura maliyetleri Cosmos DB koleksiyonların saydam tooyou olan ve hello performansı ayarlamak için tutarlılık ve kapasite kullanarak doğrudan koleksiyonlarınızı hello [Cosmos DB API'leri](https://msdn.microsoft.com/library/azure/dn781481.aspx). Tek Cosmos DB iş toologically ayrı akış başına veritabanı kullanan koleksiyonunuz için bir iş akışında öneririz.

Merhaba Cosmos DB toplama seçeneklerini bazıları aşağıda açıklanmıştır.

## <a name="tune-consistency-availability-and-latency"></a>Tutarlılık, kullanılabilirlik ve gecikme süresini ayarlama
toomatch uygulama gereksinimlerinizi Cosmos DB sağlar. toofine ayarlama hello veritabanı, koleksiyonlar ve yapma dengelemeler tutarlılık, kullanılabilirlik ve gecikme süresi arasında. Hangi düzeyde okuma tutarlılığı bağlı olarak senaryo gereksinimlerinize göre okuma ve veritabanı hesabınızdaki tutarlılık düzeyi seçebilirsiniz gecikme, yazma. Ayrıca varsayılan olarak, zaman uyumlu her CRUD işlemi tooyour koleksiyonu dizin Cosmos DB sağlar. Yazma/okuma performans Cosmos DB'de başka yararlı seçeneği toocontrol hello budur. Bu konu hakkında daha fazla bilgi için hello gözden [, veritabanı ve sorgu tutarlılık düzeylerini değiştirme](../documentdb/documentdb-consistency-levels.md) makalesi.

## <a name="upserts-from-stream-analytics"></a>Stream analytics'ten Upserts
Stream Analytics tümleştirme Cosmos DB ile belirli bir belge kimliği sütununa dayalı Cosmos DB koleksiyonunuzdaki tooinsert veya güncelleştirme kayıtları sağlar. Bu aynı zamanda başvurulan tooas olup bir *Upsert*.

Akış analizi Ekle tooa belge kimliği çakışması başarısız olduğunda burada güncelleştirmeleri yalnızca yapılır bir iyimser Upsert yaklaşımı kullanır. Bu güncelleştirme kısmi güncelleştirmeler toohello belge, yani yeni özellikleri veya mevcut bir özellik artımlı olarak gerçekleştirilen değiştirme eklenmesi tanır şekilde akış analizi tarafından bir düzeltme eki gerçekleştirilir. Üzerine hello tüm dizisinde hello değerleri dizisi özellikleri JSON belgenize değişikliklerine neden, yani hello dizi olmayan birleştirilmiş dikkat edin.

## <a name="data-partitioning-in-cosmos-db"></a>Cosmos DB'de veri bölümlendirme
Cosmos DB [bölümlenmiş koleksiyonlar](../cosmos-db/partition-data.md) önerilen verilerinizi bölümleme için yaklaşımı hello şunlardır. 

Tek Cosmos DB koleksiyonlar için Stream Analytics hala verileriniz hello sorgu desenlerine hem uygulamanızın performans gereksinimlerini temel toopartition sağlar. Her (maksimum) verilerin ve şu anda too10GB yukarı hiçbir şekilde tooscale yoktur içeren (veya taşması) bir koleksiyon. Ölçeğini için akış analizi, belirli bir önek toowrite toomultiple koleksiyonlarla sağlar (aşağıda kullanım ayrıntılarını bakın). Stream Analytics kullanır hello tutarlı [karma bölüm çözümleyici](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.partitioning.hashpartitionresolver.aspx) hello kullanıcıyı temel alarak stratejisi sağlanan PartitionKey sütun toopartition çıkış kayıtlarını. Merhaba önek işin başlangıç saati akış hello sırasında verilen hello koleksiyonlarla sayısı hello çıkış bölüm sayısı toowhich hello iş tooin paralel Yazar kullanılır (Cosmos DB koleksiyonları çıkış bölümleri =). Yavaş dizin ile tek bir koleksiyon için yalnızca eklemeleri yapılması, MB/sn üretilen iş yazma 0.4 hakkında beklenebilir. Birden çok koleksiyonları kullanarak, tooachieve daha yüksek verimlilik ve daha yüksek kapasite izin verebilirsiniz.

Merhaba gelecekteki tooincrease hello bölüm sayısı düşünüyorsanız, varolan koleksiyonlarınızı yeni Koleksiyonlar ve ardından yeniden hello Stream Analytics işi yeniden bölümle hello verileri işinizi toostop gerekebilir. Örnek kod ile birlikte yeniden bölümlendirme ve PartitionResolver kullanma hakkında daha fazla bilgi dahil izleme postasına edilir. Merhaba makale [bölümleme ve Cosmos DB'de ölçeklendirme](../documentdb/documentdb-partition-data.md) de bu ayrıntıları sağlar.

## <a name="cosmos-db-settings-for-json-output"></a>JSON çıktısını cosmos DB ayarları
Stream Analytics bir çıkış olarak Cosmos DB oluşturma aşağıda görüldüğü gibi bilgileri için bir istem oluşturur. Bu bölümde hello özellikleri tanımının bir açıklama sağlar.

Bölümlenmiş koleksiyonu | Birden çok "Tek bölüm" koleksiyonları
---|---
![documentdb stream analytics çıkış ekranı](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-1.png) |  ![documentdb stream analytics çıkış ekranı](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-2.png)


  
> [!NOTE]
> Merhaba **birden çok "Tek bölüm" koleksiyonları** senaryo bölüm anahtarı gerektirir ve desteklenen bir yapılandırmadır. 

* **Diğer ad çıktı** – Bu çıktı ASA sorgunuzda bir diğer ad toorefer  
* **Hesap adı** – hello adı veya bitiş noktası hello Cosmos DB hesap URI'si.  
* **Anahtar hesap** – hello Cosmos DB hesap hello paylaşılan erişim anahtarı.  
* **Veritabanı** – hello Cosmos DB veritabanı adı.  
* **Koleksiyon adı deseni** – hello koleksiyon adı ya da kullanılan hello koleksiyonları toobe için kendi deseni. Merhaba koleksiyon adı biçimi, burada bölümlerin 0'dan başlar hello isteğe bağlı {partition} belirteci kullanılarak oluşturulabilir. Örnek geçerli girişler şunlardır:  
  1\) MyCollection – "MyCollection" adlı bir koleksiyon bulunmalıdır.  
  2\) – böyle koleksiyonları bulunmalıdır – MyCollection {partition} "MyCollection0", "MyCollection1", "MyCollection2" ve benzeri.  
* **Anahtar bölüm** – isteğe bağlıdır. Bu, yalnızca, koleksiyon adı deseni {bölümlendirmesini} belirteci kullanıyorsanız gereklidir. çıkışın koleksiyonlar üzerinde bölümlenmesine için çıktı kullanılan olayları toospecify hello anahtar hello alanında Hello adı. Tek koleksiyon çıktı için herhangi bir rastgele çıkış sütunu olabilir örneğin PartitionID kullanılır.  
* **Belge Kimliği** – isteğe bağlıdır. hangi ekleme veya güncelleştirme işlemleri dayalı toospecify hello birincil anahtar kullanılan çıkış olaylarındaki alanın hello Hello adı.  
