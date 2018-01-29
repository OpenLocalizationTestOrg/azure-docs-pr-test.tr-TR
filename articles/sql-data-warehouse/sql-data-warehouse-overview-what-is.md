---
title: Azure SQL Data Warehouse Nedir? | Microsoft Belgeleri
description: "İlişkisel ve ilişkisel olmayan petabaytlarca veriyi işleyebilen, kurumsal sınıf bir veritabanıdır. Saniyeler içinde büyütmenizi, küçültmenizi ve duraklatmanızı sağlayan, sektörün ilk bulut veri ambarıdır."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jenniehubbard
editor: 
ms.assetid: 4006c201-ec71-4982-b8ba-24bba879d7bb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 10/23/2017
ms.author: jrj
ms.openlocfilehash: 7fd17c29c413905084c6b3736018d111d3b28fea
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2017
---
# <a name="what-is-azure-sql-data-warehouse"></a>Azure SQL Data Warehouse Nedir?

SQL Veri Ambarı, petabaytlarca veri üzerinde karmaşık sorguların hızlı bir şekilde çalıştırılması için Yüksek Düzeyde Paralel İşleme (MPP) kullanan bulut tabanlı Kurumsal Veri Ambarı (EDW) çözümüdür. SQL Veri Ambarı'nı büyük veri çözümünün temel bileşenlerinden biri olarak kullanabilirsiniz. Basit PolyBase T-SQL sorguları kullanarak büyük verileri SQL Veri Ambarı'na aktarıp MPP gücünü kullanarak yüksek performanslı analizler gerçekleştirebilirsiniz. Tümleştirme ve analiz işlemleri sırasında veri ambarı, işletmenizin öngörüler için güvenebileceği tek veri sürümü haline gelir.  


## <a name="key-component-of-big-data-solution"></a>Büyük veri çözümünün önemli bileşeni
SQL Veri Ambarı, buluttaki uçtan uca veri çözümünün önemli bileşenlerinden biridir.

![Veri ambarı çözümü](media/sql-data-warehouse-overview-what-is/data-warehouse-solution.png) 

Bulut veri çözümünde veriler farklı veri kaynaklarından büyük veri depolarına alınır. Büyük veri depolarına giren veriler Hadoop, Spark ve makine öğrenimi algoritmaları tarafından hazırlanır ve eğitilir. Veriler karmaşık analiz işlemlerine hazır olduğunda SQL Veri Ambarı, PolyBase kullanarak büyük veri depolarını sorgular. PolyBase, verileri SQL Veri Ambarı'na getirmek için standart T-SQL sorgularını kullanır.
 
SQL Veri Ambarı, verileri sütunlu depolama alanındaki ilişkisel tablolara kaydeder. Bu biçim veri depolama maliyetlerini önemli ölçüde düşürürken sorgu performansını artırır. Veriler SQL Veri Ambarı'nda depolandıktan sonra büyük ölçekli analiz çalışmaları gerçekleştirebilirsiniz. Analizler geleneksel veri sistemlerine kıyasla dakikalar yerine saniyeler, günler yerine saatler içinde tamamlanır. 

Analiz sonuçları dünya çapındaki raporlama veritabanlarına veya uygulamalarına iletilebilir. Ardından iş analistleri işlerle ilgili destekli kararlar almak üzere öngörü sahibi olabilir.

## <a name="optimization-choices"></a>İyileştirme seçenekleri

SQL Veri Ambarı büyük veya küçük ölçekli veri ihtiyaçlarınızı karşılamak için gerekli esnekliği sunmak üzere tasarlanmış [performans katmanlarına](performance-tiers.md) sahiptir. Esneklik veya işlem gücü odaklı veri ambarları arasından seçim yapabilirsiniz. 

- **Esneklik için İyileştirilmiş performans katmanı**, mimari içindeki işlem ve depolama katmanlarını birbirinden ayırır. Bu seçenek kısa süreli yüksek etkinlik dönemlerini desteklemek için sık ölçeklendirme gerçekleştirerek işlem ve depolama alanı arasındaki ayrımdan faydalanan iş yükleri için idealdir. Bu işlem katmanı en düşük giriş fiyatı noktasına sahiptir ve müşteri iş yüklerinin çoğunu destekleyecek şekilde ölçeklendirilir.

- **İşlem için İyileştirilmiş performans katmanı** en güncel Azure donanımlarını kullanarak en çok erişilen verileri tam da istediğiniz yer olan CPU'ların yakınında tutmak için yeni NVMe Katı Hal Sürücü önbelleğini kullanır. Depolama alanını otomatik olarak katmanlayan bu performans katmanı, tüm giriş çıkış verileri işlem katmanında tutulduğundan karmaşık sorgular için idealdir. Ayrıca columnstore, SQL Veri Ambarınızda sınırsız miktarda veri saklayacak şekilde geliştirilmiştir. 30.000 işlem Veri Ambarı Birimine (cDWU) kadar ölçeklendirme yapmanızı sağlayan İşlem için İyileştirilmiş performans katmanı, en yüksek ölçeklendirme seviyesini sunar. Sürekli ve çok hızlı performansa ihtiyaç duyan iş yükleri için bu katmanı seçin.

## <a name="next-steps"></a>Sonraki adımlar
SQL Veri Ambarı hakkında biraz bilgi sahibi olduğunuza göre hızlıca [SQL Veri Ambarı oluşturma][create a SQL Data Warehouse] ve [örnek verileri yükleme][load sample data] hakkında bilgi edinin. Azure'da yeniyseniz yeni terimlerle karşılaşabileceğinizi için [Azure sözlüğünü][Azure glossary] yararlı bulabilirsiniz. Alternatif olarak, aşağıdaki diğer SQL Veri Ambarı Kaynakları’na göz atın.  

* [Müşteri başarı hikayeleri]
* [Bloglar]
* [Özellik istekleri]
* [Videolar]
* [Müşteri Danışma Ekibi blogları]
* [Destek bileti oluşturma]
* [MSDN forumu]
* [Stack Overflow forumu]
* [Twitter]

<!--Image references-->
[1]: ./media/sql-data-warehouse-overview-what-is/dwarchitecture.png

<!--Article references-->
[Destek bileti oluşturma]: ./sql-data-warehouse-get-started-create-support-ticket.md
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md
[Migration documentation]: ./sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[Integrated tools overview]: ./sql-data-warehouse-overview-integrate.md
[Backup and restore overview]: ./sql-data-warehouse-restore-database-overview.md
[Azure glossary]: ../azure-glossary-cloud-terminology.md

<!--MSDN references-->

<!--Other Web references-->
[Müşteri başarı hikayeleri]: https://azure.microsoft.com/case-studies/?service=sql-data-warehouse
[Bloglar]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[Müşteri Danışma Ekibi blogları]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Özellik istekleri]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[MSDN forumu]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureSQLDataWarehouse
[Stack Overflow forumu]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Videolar]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
[SLA for SQL Data Warehouse]: https://azure.microsoft.com/en-us/support/legal/sla/sql-data-warehouse/v1_0/
[Volume Licensing]: http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=37
[Service Level Agreements]: https://azure.microsoft.com/en-us/support/legal/sla/
