---
title: "aaaIntroduction tooAzure Cosmos veritabanı tablo API | Microsoft Docs"
description: "Düşük gecikme süresi kullanarak anahtar-değer veri yoğun birimleri sorgu popüler OSS MongoDB API'leri hello ve Azure Cosmos DB toostore nasıl kullanacağınızı öğrenin."
services: cosmos-db
author: bhanupr
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/25/2017
ms.author: arramac
ms.openlocfilehash: 4c5678898a772808f4bcd1465a23d436b0f8fc0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-table-api"></a>Giriş tooAzure Cosmos DB: Tablo API

[Azure Cosmos DB](introduction.md), Microsoft'un görev açısından kritik uygulamalar için genel olarak dağıtılmış çok modelli veritabanı hizmetidir. Azure Cosmos DB sağlar [anahtar teslim genel dağıtım](distribute-data-globally.md), [üretilen iş ve depolama esnek ölçeklendirme](partition-data.md) dünya, tek basamaklı milisaniyelik gecikme hello 99, adresindeki [beş iyi tanımlanmış tutarlılık düzeylerini](consistency-levels.md), yüksek oranda kullanılabilirlik, tarafından yedeklenen tüm garanti [endüstri lideri SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure Cosmos DB [verileri otomatik olarak dizinler](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) toodeal şema ve dizin yönetimi ile gerektirmeden. Çok modelli olan bu hizmet belge, anahtar-değer, grafik ve sütunlu veri modellerini destekler. 

![Azure Tablo depolama API’si ve Azure Cosmos DB](./media/table-introduction/premium-tables.png) 

Azure Cosmos DB hello tablo API (Önizleme) bir anahtar-değer deposu esnek şema, tahmin edilebilir performans, genel dağıtım ve yüksek verimlilik ile gereken uygulamalar için sağlar. Merhaba tablo API sağlar hello Azure Table storage aynı işlevselliği ancak hello Azure Cosmos veritabanı altyapısı hello avantajlarından yararlanır. 

Toouse Azure Table storage yüksek depolama ve daha düşük işleme gereksinimlerine sahip tablolar için devam edebilirsiniz. Azure Cosmos DB gelecekteki bir güncelleştirme depolama için iyileştirilmiş tablolar için destek getirir ve var olan ve yeni Azure depolama hesapları tablo tooAzure Cosmos DB yükseltilecektir.

## <a name="premium-and-standard-table-apis"></a>Premium ve standart Tablo API’leri
Şu anda Azure Table depolama kullanırsanız, tooAzure Cosmos veritabanı "premium tablo" Önizleme taşıyarak avantajları aşağıdaki hello elde:

|  | Azure Table Storage | Azure Cosmos DB: Tablo depolama (önizleme) |
| --- | --- | --- |
| Gecikme süresi | Hızlıdır, ancak gecikme süresi için üst sınır yoktur | Tek basamaklı milisaniyelik gecikme süresi için okuma ve yazma işlemleri, yedeklenen ile < 10 ms Gecikmeli okur ve < 15 ms gecikme Yazar hello 99, hello world başka bir yerindeki herhangi bir ölçekte adresindeki |
| Aktarım hızı | Yüksek düzeyde ölçeklenebilir, ancak adanmış aktarım hızı modeli değildir. Tabloların 20.000 işlem/sn’lik bir ölçeklenebilirlik sınırı vardır | SLA’lar ile desteklenen [tablo başına adanmış, ayrılmış aktarım hızı](request-units.md) ile yüksek düzeyde ölçeklenebilir. Hesapların aktarım hızı açısından üst sınırı yoktur ve tablo başına saniyede 10 milyondan fazla işlem desteklenir |
| Genel Dağıtım | Yüksek kullanılabilirlik için isteğe bağlı okunabilir bir ikincil okuma bölgesi olan tek bölge. Yük devretme başlatamazsınız | [Anahtar teslim genel dağıtım](distribute-data-globally.md) bir too30 + bölgelerden, desteği [otomatik ve el ile yük devretme](regional-failover.md) Merhaba Dünya başka bir yerindeki herhangi bir anda |
| Dizinleme | Yalnızca PartitionKey ve RowKey’de birincil dizin. İkincil dizin yok | Tüm özelliklerde otomatik ve eksiksiz dizin oluşturma, dizin yönetimi yok |
| Sorgu | Sorgu yürütme birincil anahtar için dizini kullanır, aksi durumda tarar. | Sorgular, hızlı sorgu süreleri için özelliklerde otomatik dizin oluşturma avantajından yararlanabilir. Azure Cosmos DB’nin veritabanı altyapısı, toplamaları, jeo-uzamsal aramayı ve sıralamayı destekleme özelliğine sahiptir. |
| Tutarlılık | Birincil bölgede Güçlü, ikincil bölgede Nihai | [Beş iyi tanımlanmış tutarlılık düzeylerini](consistency-levels.md) tootrade kapatma kullanılabilirlik, gecikme süresi, üretilen iş ve tutarlılık tabanlı uygulama gereksinimlerinize göre |
| Fiyatlandırma | Depolama açısından iyileştirilmiş  | Aktarım hızı açısından iyileştirilmiş |
| SLA’lar | %99,9 kullanılabilirlik | tek bir bölge ve yeteneği tooadd daha fazla içinde % 99,99 kullanılabilirlik yüksek kullanılabilirlik için bölgeler. Genel kullanılabilirlik aşamasında [sektör lideri kapsamlı SLA’lar](https://azure.microsoft.com/support/legal/sla/cosmos-db/) |

## <a name="how-tooget-started"></a>Tooget nasıl başlatılacağını

Hello Azure Cosmos DB hesap oluşturmak [Azure portal](https://portal.azure.com)ve kullanmaya başlama bizim [tablo .NET kullanarak API için Hızlı Başlangıç](create-table-dotnet.md). 

## <a name="next-steps"></a>Sonraki adımlar

Başlattığınız birkaç işaretçileri tooget şunlardır:
* [Merhaba tablo API kullanarak bir .NET uygulaması oluşturma](create-table-dotnet.md)
* [Merhaba .NET tablo API ile geliştirme](tutorial-develop-table-dotnet.md)
* [Tablo verisi hello tablo API kullanarak sorgulama](tutorial-query-table.md)
* [Nasıl toosetup Azure Cosmos DB genel dağıtım kullanarak izin ver hello tablo API](tutorial-global-distribution-table.md)
* [.NET için Azure Cosmos DB Tablo API SDK’si](table-sdk-dotnet.md)
