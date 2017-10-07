---
title: "aaaAzure Cosmos DB anahtar değeri deposu – maliyet genel bakış olarak | Microsoft Docs"
description: "Bir anahtar değeri deposu olarak Azure Cosmos DB kullanarak hello düşük maliyeti hakkında bilgi edinin."
keywords: "anahtar değeri deposu"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: 
documentationcenter: 
ms.assetid: 7f765c17-8549-4509-9475-46394fc3a218
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: mimig
ms.openlocfilehash: de7207760a8e1fca0e30f951109748835dabf4a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-as-a-key-value-store--cost-overview"></a>Anahtar değeri deposu – maliyet genel olarak Azure Cosmos DB

Azure Cosmos DB, yüksek oranda kullanılabilir, büyük ölçekli uygulamalara kolayca oluşturmaya yönelik bir genel dağıtılmış, birden çok model veritabanı hizmetidir. Varsayılan olarak, Azure Cosmos DB onu, verimli bir şekilde alır tüm hello verileri otomatik olarak dizinler. Bu, hızlı ve tutarlı sağlar [SQL](documentdb-sql-query.md) (ve [JavaScript](programming.md)) her türlü veri sorgular. 

Bu makalede Azure Cosmos DB hello maliyetini için basit yazma ve okuma işlemlerini bir anahtar/değer deposu olarak kullanıldığında. Ekler, değiştirir, siler ve belgelerin upserts işlemleri içeren yazma. % 99,99 yüksek kullanılabilirlik güvence altına almak yanı sıra Azure Cosmos DB teklifleri garanti < 10 ms Gecikmeli okumalar için ve < 15 ms gecikme (dizin) hello için yazar sırasıyla hello 99. 

## <a name="why-we-use-request-units-rus"></a>İstek birimleri (RUs) neden kullanırız

Azure Cosmos DB performans hello miktarına bağlı sağlanan [istek birimlerine](request-units.md) (RU) hello bölümü için. İkinci bazda olduğunu ve RUs/sn ile RUs/dak satın Hello sağlama ([değil saatlik faturalandırma hello ile kafası toobe](https://azure.microsoft.com/pricing/details/cosmos-db/)). RUs hello Merhaba uygulaması için gereken işleme sağlanmasını basitleştiren bir para birimi olarak düşünülmelidir. Müşterilerimizin okuma ve yazma kapasite birimler arasında ayrım yapma, toothink gerekmez. Merhaba tek para birimini RUs modelinin tooshare hello sağlanan kapasite okuma ve yazma işlemleri arasında verimliliği oluşturur. Bu sağlanan kapasite model düşük gecikme süreli ve yüksek oranda kullanılabilirlik garanti hello hizmet tooprovide tahmin edilebilir ve tutarlı bir verimlilik sağlar. Son olarak, RU toomodel verimlilik kullanırız ancak sağlanan her RU tanımlanan miktarda kaynak (bellek, çekirdek) de vardır. Saniye başına RU yalnızca IOPS değil.

Genel olarak dağıtılmış veritabanı sistem olarak Cosmos DB olduğu hello toplama toohigh kullanılabilirlik SLA gecikme süresi, performans ve tutarlılık sağlayan Azure hizmeti. sağlamanız hello işleme uygulanan tooeach Cosmos DB veritabanı hesabınızla ilişkili hello bölgelerinin ' dir. Okumalar, birden çok, iyi tanımlanmış Cosmos DB sunar [tutarlılık düzeylerini](consistency-levels.md) , toochoose için. 

Merhaba aşağıdaki tabloda gösterildiği RUs gerekli tooperform okuma sayısını hello ve 1 KB ile 100KBs belge boyutuna göre işlemleri yazma.

|Öğesi boyutu|1 okuma|1 yazma|
|-------------|------|-------|
|1 KB|1 RU|5 RUs|
|100 KB|10 RUs|50 RUs|

## <a name="cost-of-reads-and-writes"></a>Okuma ve yazma işlemleri maliyeti

1.000 RU/sn sağlarsanız, bu too3.6m RU/saat tutar ve 0,08 ABD Doları hello saati (ABD hello ve Avrupa) için maliyetlidir. Bir 1 KB boyutu belge için bu 3,6 m okuma tüketebileceği veya 0,72 m Yazar anlamına gelir (3.6mRU / 5), sağlanan işleme kullanma. Normalleştirilmiş toomillion okuma ve yazma, hello maliyet $0.022 /m okuma olacaktır (0,08 ABD Doları / 3,6) ve $0.111/ m yazar (0,08 ABD Doları / 0,72). Merhaba maliyet başına milyon hello aşağıdaki tabloda gösterildiği gibi en az olur.

|Öğesi boyutu|1m okuma|1m yazma|
|-------------|-------|--------|
|1 KB|$0.022|$0.111|
|100 KB|$0.222|$1.111|


Merhaba temel blob veya milyon okuma işlemi ve 5 milyon yazma işlem başına başına nesne depoları hizmetler ücreti $0.40 çoğunu. En iyi şekilde kullandıysanız, Cosmos DB too98% bu diğer çözümlerin (işlemlerinde 1 KB) daha ucuz olabilir.

## <a name="next-steps"></a>Sonraki adımlar

Yeni makaleler Azure Cosmos DB kaynak sağlama en iyi duruma getirmek için bizi izlemeye devam edin. Buna hello bu arada, izin ver eşitleyerek ücretsiz toouse bizim [RU hesaplayıcı](https://www.documentdb.com/capacityplanner).

