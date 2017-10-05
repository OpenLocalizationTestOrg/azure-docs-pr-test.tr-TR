---
title: "İzleme XTP bellek içi depolama | Microsoft Docs"
description: "Tahmin ve İzleyici XTP bellek içi depolama, kapasite kullanın; Kapasite hatayı 41823"
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: 5afb2209f18b1ba2aa0a916a439509b01afd80da
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-in-memory-oltp-storage"></a>Bellek içi OLTP Depolama Alanını izleme
Kullanırken [bellek içi OLTP](sql-database-in-memory.md), bellek için iyileştirilmiş tablolar ve Tablo değişkenlerinin verileri bellek içi OLTP depolamada yer alıyor. Her Premium Hizmet katmanını belgelenen en fazla bir bellek içi OLTP depolama boyutuna sahip [SQL Database hizmet katmanları makale](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels). Bu sınır aşılırsa sonra ekleme ve güncelleştirme işlemleri (hatası 41823 ile) başarısız olan başlayabilir. Bu noktada, ya da belleği geri almasını verileri silmek veya veritabanınızın performans katmanı yükseltin.

## <a name="determine-whether-data-will-fit-within-the-in-memory-storage-cap"></a>Veri içinde bellek içi depolama ucun uygun olup olmadığını belirleme
Depolama ucun belirlemek: başvurun [SQL Database hizmet katmanları makale](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) farklı Premium hizmet katmanları, depolama caps için.

Bellek için iyileştirilmiş tablo works onu aynı şekilde SQL Server için Azure SQL veritabanı'nda mu bellek gereksinimlerini tahmin etme. Bu konuda üzerinde gözden geçirmek için birkaç dakika sürebilir [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).

Tablosu ve tablo değişkeni satırları yanı dizinler, en fazla kullanıcı veri boyutu doğru saymak unutmayın. Buna ek olarak, ALTER TABLE tablonun tamamını ve dizinlerini yeni bir sürümünü oluşturmak için yeterli alan gerekir.

## <a name="monitoring-and-alerting"></a>İzleme ve uyarı
Bellek içi depolama kullanımı yüzdesi olarak izleyebilirsiniz [depolama cap performans katmanı için](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) azure'da [portal](https://portal.azure.com/): 

* Veritabanı dikey penceresinde kaynak kullanımı kutusunu bulun ve Düzenle'yi tıklatın.
* Ölçümü seçin `In-Memory OLTP Storage percentage`.
* Bir uyarı eklemek için ölçüm dikey penceresi açmak için kaynak kullanımı kutusuna tıklayın, sonra Ekle uyarıya tıklayın.

Veya bellek içi depolama kullanımını göstermek için aşağıdaki sorguyu kullanın:

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a>Bellek durum - hata 41823 düzeltin
Bellek sonuçlarını 41823 hata iletisiyle başarısız INSERT, UPDATE ve oluşturma işlemleri çalışıyor.

Hata iletisi 41823 bellek için iyileştirilmiş tablolar ve Tablo değişkenlerinin boyutu üst sınırı aştınız gösterir.

Ya da bu hatayı gidermek için:

* Potansiyel olarak Geleneksel, disk tabanlı tablolara veri boşaltma bellek için iyileştirilmiş tablolardaki verileri silmek; veya,
* Bellek için iyileştirilmiş tablolarda tutmak için gereken verileri için yeterli bellek içi depolama sahip bir hizmet katmanına yükseltin.

## <a name="next-steps"></a>Sonraki adımlar
Kılavuzu izleme için bkz: [Azure SQL Dinamik Yönetim görünümlerini kullanarak veritabanı izleme](sql-database-monitoring-with-dmvs.md).
