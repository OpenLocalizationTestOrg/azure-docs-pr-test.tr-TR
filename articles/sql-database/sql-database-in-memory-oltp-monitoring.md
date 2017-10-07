---
title: "aaaMonitor XTP bellek içi depolama | Microsoft Docs"
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
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a>Bellek içi OLTP Depolama Alanını izleme
Kullanırken [bellek içi OLTP](sql-database-in-memory.md), bellek için iyileştirilmiş tablolar ve Tablo değişkenlerinin verileri bellek içi OLTP depolamada yer alıyor. Her Premium Hizmet katmanını hello belgelenen en fazla bir bellek içi OLTP depolama boyutuna sahip [SQL Database hizmet katmanları makale](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels). Bu sınır aşılırsa sonra ekleme ve güncelleştirme işlemleri (hatası 41823 ile) başarısız olan başlayabilir. Bu noktada tooeither delete veri tooreclaim belleğe ihtiyacınız veya hello performans katmanı veritabanınızın yükseltin.

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a>Veri hello bellek içi depolama cap içinde uygun olup olmadığını belirleme
Merhaba depolama cap belirlemek: hello başvurun [SQL Database hizmet katmanları makale](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) hello depolama caps hello farklı Premium hizmet katmanı için.

Bellek için iyileştirilmiş bir tablo çalışır için gereksinimleri aynı hello bellek tahmin şekilde SQL Server için Azure SQL veritabanı'nda yapar. Birkaç dakika tooreview bu konuda ele [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).

Merhaba tablosu ve tablo değişkeni satırları yanı sıra, dizinler, hello en fazla kullanıcı veri boyutu doğru saymak unutmayın. Ayrıca, ALTER TABLE yeterli yer toocreate hello tüm tablo ve dizinlerini yeni bir sürümü gerekiyor.

## <a name="monitoring-and-alerting"></a>İzleme ve uyarı
Bellek içi depolama kullanımı hello yüzdesi olarak izleyebilirsiniz [depolama cap performans katmanı için](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) hello Azure'nın [portal](https://portal.azure.com/): 

* Merhaba veritabanı dikey penceresinde hello kaynak kullanımı kutusunu bulun ve Düzenle'yi tıklatın.
* Merhaba ölçümü seçebilmeniz `In-Memory OLTP Storage percentage`.
* tooadd bir uyarı hello kaynak kullanımı kutusunu tooopen hello ölçüm dikey penceresinde'ı tıklatın, sonra Ekle uyarıya tıklayın.

Veya sorgu tooshow hello bellek içi depolama kullanımını izleyen hello kullanın:

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a>Bellek durum - hata 41823 düzeltin
Bellek sonuçlarını 41823 hata iletisiyle başarısız INSERT, UPDATE ve oluşturma işlemleri çalışıyor.

Hata iletisi 41823 hello bellek için iyileştirilmiş tablolar ve Tablo değişkenlerinin hello sınırını aştınız gösterir.

tooresolve bu hata ya da:

* Veri hello bellek için iyileştirilmiş tablolar, potansiyel olarak yük boşaltma hello veri tootraditional, disk tabanlı tabloları silin; veya,
* Merhaba hizmet katmanı tooone yükseltme hello verileri için yeterli bellek içi depolama ile bellek için iyileştirilmiş tablolardaki tookeep gerekir.

## <a name="next-steps"></a>Sonraki adımlar
Kılavuzu izleme için bkz: [Azure SQL Dinamik Yönetim görünümlerini kullanarak veritabanı izleme](sql-database-monitoring-with-dmvs.md).
