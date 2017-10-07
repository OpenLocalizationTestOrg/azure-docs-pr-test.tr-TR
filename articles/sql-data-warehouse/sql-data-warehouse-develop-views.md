---
title: "Azure SQL Data Warehouse aaaUsing T-SQL görünümleri | Microsoft Docs"
description: "Çözümleri geliştirme için Azure SQL Data Warehouse'da Transact-SQL görünümlerini kullanma ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: b5208f32-8f4a-4056-8788-2adbb253d9fd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 3990b133946621691bdfa4b09523d21867470c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-sql-data-warehouse"></a>SQL veri ambarı görünümlerde
Görünümleri SQL veri ambarı'nda özellikle yararlıdır. Çözümünüzü farklı şekillerde tooimprove hello kalitesini sayısında kullanılabilir.  Bu makalede birkaç örnekleri nasıl tooenrich toobe gereksinim hello sınırlamaları yanı sıra görünümleri çözümünüzle kabul vurgular.

> [!NOTE]
> Sözdizimi `CREATE VIEW` bu makalede ele alınmamıştır. Lütfen toohello bakın [CREATE VIEW] [ CREATE VIEW] MSDN makalesinde bu başvuru bilgileri için.
> 
> 

## <a name="architectural-abstraction"></a>Mimari Özet
Yaygın bir uygulama düzeni toore olduğu-tablolar oluşturma tablo AS seçin (desen veri yükleme yaparken yeniden adlandırma nesne tarafından izlenen CTAS) kullanarak oluşturun.

Aşağıdaki örnek Hello yeni tarihi kayıtları tooa tarih boyutu ekler. Nasıl DimDate_New, yeni bir tabble ilk oluşturulduğunda ve tooreplace hello özgün sürümü Merhaba tablonun yeniden adlandırılmış unutmayın.

```sql
CREATE TABLE dbo.DimDate_New
WITH (DISTRIBUTION = ROUND_ROBIN
, CLUSTERED INDEX (DateKey ASC)
)
AS
SELECT *
FROM   dbo.DimDate  AS prod
UNION ALL
SELECT *
FROM   dbo.DimDate_stg AS stg
;

RENAME OBJECT DimDate tooDimDate_Old;
RENAME OBJECT DimDate_New tooDimDate;

```

Ancak, bu yaklaşım görünmesini ve "tablo yok" hata iletileri yanı sıra bir kullanıcının görünüm kayboluyor tabloları neden olabilir. Merhaba arka plandaki nesneleri yeniden adlandırıldıktan adımında görünümleri tutarlı sunu katmanı kullanılan tooprovide kullanıcılarla olabilir. Kullanıcılara erişim sağlayarak toohello verileri bir görünümler yoluyla anlamına gelir kullanıcılar hello temel tabloları toohave görünürlüğünü gerek yoktur. Merhaba veri ambarı tasarımcıları hello veri modeli gelişmesi ve hello veri yükleme işlemi sırasında CTAS kullanarak performansı en üst düzeye çıkarmak sağlarken tutarlı bir kullanıcı deneyimi sağlar.    

## <a name="performance-optimization"></a>Performansı iyileştirme
Görünümleri de kullanılan tooenforce en iyi duruma getirilmiş performans birleştirmeler tablolar arasında olabilir. Örneğin, bir görünüm olarak yedekli dağıtım anahtarı ölçütleri toominimize veri taşıma birleştirme hello bir parçası olarak dahil edebilirsiniz.  Bir görünüm başka bir yararı tooforce belirli bir sorgu veya birleşme ipucu olabilir. Bu şekilde görünümleri birleştirmeler kullanıcılar tooremember hello doğru yapı kendi birleştirmelerde hello gereksinimini önleme bir en iyi şekilde her zaman gerçekleştirildiğinden emin güvence altına alır.

## <a name="limitations"></a>Sınırlamalar
SQL veri ambarı görünümlerinde yalnızca meta verilerdir.  Sonuç olarak aşağıdaki seçenekleri şu hello kullanılabilir değil:

* Şema bağlama seçeneği yoktur
* Temel tabloyu hello görünüm üzerinden güncelleştirilemiyor
* Geçici tablolar üzerindeki görünüm oluşturulamıyor
* Merhaba genişletme için destek yok / NOEXPAND ipuçları
* SQL veri ambarı'nda hiç dizini oluşturulmuş görünüm yok

## <a name="next-steps"></a>Sonraki adımlar
Geliştirme ile ilgili daha fazla ipucu için bkz. [SQL Veri Ambarı’nda geliştirmeye genel bakış][SQL Data Warehouse development overview].
İçin `CREATE VIEW` sözdizimi başvurun çok[CREATE VIEW][CREATE VIEW].

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
