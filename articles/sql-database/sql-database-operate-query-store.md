---
title: "Azure SQL veritabanındaki Query Store aaaOperating"
description: "Nasıl toooperate hello Azure SQL veritabanındaki Query Store öğrenin"
keywords: 
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: 0cccf6bd-1327-44f7-a6f9-8eff0c210463
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: sqldb-performance
ms.workload: data-management
ms.date: 11/08/2016
ms.author: bonova
ms.openlocfilehash: ab741e49685bf6df3bceab219aaf57ea51cdb25d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="operating-hello-query-store-in-azure-sql-database"></a>İşletim hello Azure SQL veritabanındaki Query Store
Query Store Azure sürekli olarak toplayan ve tüm sorguları hakkında ayrıntılı geçmiş bilgileri sunan bir tam olarak yönetilen veritabanı özelliğidir. Query Store hakkında önemli ölçüde hem bulut için sorun giderme sorgu performansı basitleştirir ve şirket içi müşteriler benzer tooan uçak'ın uçuş veri Kaydedicisi düşünebilirsiniz. Bu makalede Azure sorgu deposunda işletim belirli yönleri açıklanmaktadır. Bu önceden toplanan verileri kullanarak, hızlı bir şekilde tanılayabilir ve performans sorunlarını gidermek ve böylece işletmelerini odaklanan daha fazla zaman ayırın. 

Query Store süredir [genel olarak kullanılabilir](https://azure.microsoft.com/updates/general-availability-azure-sql-database-query-store/) Kasım 2015 itibaren Azure SQL veritabanında. Sorgu deposudur hello temeli Performans Analizi ve ayarlama gibi özellikleri, [SQL veritabanı Danışmanı'nı ve performans Pano](https://azure.microsoft.com/updates/sqldatabaseadvisorga/). Bu makalede yayımlandığı hello şu anda Query Store, Azure, birden çok 200.000 kullanıcı veritabanlarında kesintisiz birkaç ay için sorgu ile ilgili bilgi toplama çalışıyor.

> [!IMPORTANT]
> Microsoft, tüm Azure SQL veritabanları için (mevcut ve yeni) Query Store etkinleştirme işleminin hello kullanılıyor. 
> 
> 

## <a name="optimal-query-store-configuration"></a>En iyi sorgu deposu yapılandırma
Bu bölümde tasarlanmış tooensure güvenilir işlemi hello Query Store ve bağımlı özellikler gibi olan en iyi yapılandırma varsayılanlarını açıklanmaktadır [SQL veritabanı Danışmanı'nı ve performans Pano](https://azure.microsoft.com/updates/sqldatabaseadvisorga/). Varsayılan yapılandırma kapalı/READ_ONLY durumlarda en az zamanın olan sürekli veri toplama için optimize edilmiştir.

| Yapılandırma | Açıklama | Varsayılan | Açıklama |
| --- | --- | --- | --- |
| MAX_STORAGE_SIZE_MB |Query Store z müşteri veritabanının sürebilir hello veri alanı için Hello sınırı belirtir |100 |Yeni veritabanları için zorlanan |
| İNTERVAL_LENGTH_MİNUTES DEĞERİ |İçinde sorgu planları için toplanan çalışma zamanı istatistikleri toplanır ve kalıcı zaman penceresi boyutunu tanımlar. Bu yapılandırma ile tanımlanan süre her etkin sorgu planı en çok bir satır var. |60 |Yeni veritabanları için zorlanan |
| STALE_QUERY_THRESHOLD_DAYS DEĞERİ |Merhaba saklama dönemi kalıcı çalışma zamanı istatistikleri ve etkin olmayan sorguları denetimleri zamana dayalı temizleme İlkesi |30 |Yeni veritabanları ve önceki varsayılan (367) ile veritabanları için zorlanan |
| SİZE_BASED_CLEANUP_MODE DEĞERİ |Query Store veri boyutu hello sınırı yaklaştığında otomatik veri temizleme gerçekleşir olup olmadığını belirtir |OTOMATİK |Tüm veritabanları için zorlanan |
| QUERY_CAPTURE_MODE DEĞERİ |Tüm sorgular veya yalnızca bir alt sorgu izlenen olup olmadığını belirtir |OTOMATİK |Tüm veritabanları için zorlanan |
| FLUSH_INTERVAL_SECONDS |En uzun süresi sırasında yakalanan çalışma zamanı istatistikleri bellekte toodisk temizleme önce tutulması belirtir |900 |Yeni veritabanları için zorlanan |
|  | | | |

> [!IMPORTANT]
> Bu varsayılan otomatik Query Store etkinleştirme (önceki önemli nota bakın) tüm Azure SQL veritabanı'hello son aşamasında uygulanır. Bunlar birincil iş yükünü veya hello Query Store güvenilir işlemlerini olumsuz sürece sonra bu ışık Azure SQL veritabanı müşteriler tarafından ayarladığınız yapılandırma değerlerini değiştirme olmaz.
> 
> 

Özel ayarlarınızla toostay istiyorsanız kullanın [ALTER DATABASE Query Store seçenekleriyle](https://msdn.microsoft.com/library/bb522682.aspx) toorevert yapılandırma toohello önceki durumu. Kullanıma [hello Query Store en iyi yöntemlerle](https://msdn.microsoft.com/library/mt604821.aspx) sırada toolearn nasıl üst en iyi yapılandırma parametreleri seçin.

## <a name="next-steps"></a>Sonraki adımlar
[SQL veritabanı performansı öngörüleri](sql-database-performance.md)

## <a name="additional-resources"></a>Ek kaynaklar
Daha fazla bilgi kullanıma için makaleler hello:

* [Veritabanınız için uçuş veri Kaydedicisi](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database) 
* [Merhaba Query Store performans kullanarak izleme](https://msdn.microsoft.com/library/dn817826.aspx)
* [Sorgu deposu kullanım senaryoları](https://msdn.microsoft.com/library/mt614796.aspx)
* [Merhaba Query Store performans kullanarak izleme](https://msdn.microsoft.com/library/dn817826.aspx) 

