---
title: "aaaMigrate, veri ambarı çözüm tooSQL | Microsoft Docs"
description: "Çözüm tooAzure SQL Data Warehouse platformunuz getiren Geçiş Kılavuzu."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a>SQL Data Warehouse, çözüm tooAzure geçirme
Ne var olan bir veritabanı çözümü tooAzure SQL veri ambarı geçiş konusuysa bakın. 

## <a name="profile-your-workload"></a>İş yükünüzün profil
Geçirmeden önce SQL Data Warehouse hello doğru iş yükü çözümdür belirli toobe istiyor. SQL veri ambarı büyük veri tasarlanmış Dağıtılmış Sistem tooperform analytics ' dir.  Geçirme tooSQL veri ambarı çok sabit toounderstand değildir ancak bazı zaman tooimplement sürebilir bazı tasarım değişiklikleri gerektirir. Bir kurumsal sınıf veri ambarı, İşletmenizde hello avantajları hello çabalara demektir. Ancak, SQL Data Warehouse hello gücünü gerek duymuyorsanız, daha fazla uygun maliyetli toouse SQL Server veya Azure SQL veritabanı değil.

SQL veri ambarı kullanmayı olduğunda:
- Bir veya daha fazla terabayt veri sahip
- Büyük miktarlarda verinin toorun analytics planlama
- Merhaba özelliği tooscale işlem ve depolama gerekir 
- Bunları gerekmediğinde duraklatma tarafından toosave maliyetleri işlem kaynaklarını istiyor.

SQL veri ambarı sahip işlem (gerçekleştirme OLTP) iş yükleri için kullanmayın:
- Yüksek yoğunlukta okuma ve yazma işlemleri
- Singleton çok sayıda seçer
- Yüksek hacimli tek bir satır ekler
- Satır satır işleme tarafından gerekiyor
- Uyumsuz biçimleri (JSON, XML)


## <a name="plan-hello-migration"></a>Merhaba geçişi planlama

Var olan bir çözümü tooSQL veri ambarı toomigrate karar verdikten sonra başlarken önce önemli tooplan hello geçiş değil. 

Planlama tek amacı, tablo şemalarını verilerinizi tooensure olduğunu ve kodunuzu SQL Data Warehouse ile uyumludur. Bazı uyumluluk farklar toowork geçici geçerli sistem ve SQL Data Warehouse arasında vardır. Ayrıca, büyük miktarlarda veri tooAzure alır süresini geçirme. Dikkatli planlama veri tooAzure alma hızlandırır. 

Planlama, başka bir hedef çözümünüzü SQL veri ambarı hello yüksek sorgu performansı yararlanır ayarlamalar tooensure tooprovide tasarlanmış toomake tasarımdır. Veri ambarları ölçek tasarlama farklı tasarım desenleri tanıtır ve bu nedenle geleneksel yaklaşım her zaman hello en iyi değil. Geçişten sonra bazı tasarım ayarlamalar yapabilmenize rağmen daha erken hello işleminde değişiklik daha sonra zaman kaydeder.

tooperform başarılı bir geçiş, gereksinim duyduğunuz toomigrate, tablo şemalarını, kodunuz ve verileriniz. Bu geçiş konuları hakkında yönergeler için bkz:

-  [Şemalar geçirme](sql-data-warehouse-migrate-schema.md)
-  [Kodunuzu geçirme](sql-data-warehouse-migrate-code.md)
-  [Verilerinizi geçirme](sql-data-warehouse-migrate-data.md). 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a>Sonraki adımlar
Hello kat (Müşteri danışma ekibi) blog yayımlama bazı harika SQL Data Warehouse yönergeler de vardır.  Kendi makale bakalım [uygulamada geçiş veri tooAzure SQL Data Warehouse] [ Migrating data tooAzure SQL Data Warehouse in practice] geçiş hakkında ek yönergeler için.

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
