---
title: Azure SQL Data Warehouse aaaWhat mi? | Microsoft Belgeleri
description: "İlişkisel ve ilişkisel olmayan petabaytlarca veriyi işleyebilen, kurumsal sınıf bir veritabanıdır. Merhaba sektörün ilk bulut veri ambarıdır büyütmenizi., küçülen ve saniye cinsinden."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: bjhubbard
editor: 
ms.assetid: 4006c201-ec71-4982-b8ba-24bba879d7bb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 2/28/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 5fefe40879230f123c2e4a90b9c20a35779cf711
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-sql-data-warehouse"></a>Azure SQL Data Warehouse Nedir?
Azure SQL Veri Ambarı, çok geniş hacimlerdeki verileri işleyebilen, bulut tabanlı, ölçeklenebilen, ilişkisel bir yüksek düzeyde paralel işleme (MPP) veritabanıdır. 

SQL Data Warehouse:

* Merhaba SQL Server ilişkisel veritabanıyla Azure bulut genişletme işlevlerini birleştirir. 
* Depolamayı işlemden ayırır.
* İşlemi artırma, azaltma, duraklatma ve sürdürme olanağı sağlar. 
* Azure platformu Hello arasında tümleştirir.
* SQL Server Transact-SQL (T-SQL) ve araçları kullanır.
* SOC ve ISO gibi çeşitli yasal gereksinimler ve iş güvenliği gereksinimleriyle uyumludur.

Bu makalede SQL Data Warehouse hello anahtar özelliklerini açıklar.

## <a name="massively-parallel-processing-architecture"></a>Yüksek düzeyde paralel işleme mimarisi
SQL Veri Ambarı, yüksek düzeyde paralel işleme (MPP) ile dağıtılmış bir veritabanı sistemidir. Merhaba arka planda, SQL Data Warehouse verilerinizi birçok hiçbir şey paylaşılmayan depolama ve işleme birimleri arasında yayar. Merhaba veri hangi üstünde dinamik olarak bağlı işlem düğümleri sorguları yürütmek Premium yerel olarak yedekli depolama katmanı içinde depolanır. SQL veri ambarı alır bir "Böl ve Yönet" yaklaşımını toorunning yükler ve karmaşık sorgular. İstekler, dağıtım için en iyi duruma getirilmiş ve ardından tooCompute düğümleri toodo çalışmalarını paralel olarak geçirilen bir denetim düğümü tarafından alınır.

Ayrılmış depolama ve işlem ile SQL Veri Ambarı şunları yapabilir:

* İşlemden bağımsız olarak depolama boyutunu büyütür veya küçültür.
* Verileri taşımadan işlem gücünü büyütür veya küçültür.
* Verileri olduğu gibi bırakıp işlem kapasitesini duraklatır ve yalnızca depolama için ödeme yapılır.
* Çalışma saatleri içinde işlem kapasitesini sürdürür.

Merhaba Aşağıdaki diyagramda hello mimari daha ayrıntılı olarak gösterilmiştir.

![SQL Data Warehouse Mimarisi][1]

**Denetim düğümü:** hello denetim düğümü yönetir ve sorguları en iyi duruma getirir. Tüm uygulamalarla ve bağlantılarla etkileşim kuran hello ön uç değil. SQL Data Warehouse, hello kontrol düğümü SQL Database ile güçlendirilmiştir ve tooit bağlanma arar ve hissi aynı hello. Merhaba yüzeyini altında hello kontrol düğümü tüm hello veri hareketlerini ve hesaplamaları gereken koordinatları toorun üzerinde dağıtılmış verilerinizde paralel sorgular. T-SQL sorgusu tooSQL veri ambarı gönderdiğinizde hello kontrol düğümü, her paralel işlem düğümünde çalışacak ayrı sorgulara dönüştürür.

**İşlem düğümleri:** hello işlem düğümleri hello SQL veri ambarı'nın arkasındaki güç olarak hizmet verir. Bunlar verilerinizi depolayan ve sorgunuzu işleyen SQL Veritabanlarıdır. Veri eklediğiniz zaman SQL veri ambarı hello satırları tooyour işlem düğümleri dağıtır. Merhaba işlem düğümleri verilerinizde hello paralel sorgular çalıştırmak hello çalışanlardır. İşlemeden sonra hello sonuçları geri toohello kontrol düğümü geçirirler. toofinish hello sorgu hello kontrol düğümü hello sonuçları toplar ve son sonucu döndürür hello.

**Depolama:** Verileriniz Azure Blob depolama alanına depolanır. İşlem düğümleri verilerinizle etkileşim kurduklarında, yazma ve doğrudan tooand blob depolama alanından okuyun. Azure depolama saydam ve böylelikle genişletir olduğundan, SQL Data Warehouse yapabilirsiniz aynı hello. İşlem ve depolama bağımsız olduğundan, SQL Data Warehouse işlemi ölçeklendirmeden ayrı olarak depolamayı otomatik şekilde ölçeklendirebilir ve tam tersini yapabilir. Azure Blob Depolama aynı zamanda hatalara tamamen dayanıklıdır ve ölçeklendirerek hello yedekleme ve geri yükleme işlemi.

**Veri Taşıma hizmeti:** veri taşıma hizmeti (DMS) hello düğümler arasında verileri taşır. DMS hello işlem düğümleri erişim toodata birleşimler ve Toplamalar için ihtiyaç duydukları sağlar. DMS bir Azure hizmeti değildir. Tüm hello düğümlerde SQL Database'in yanında çalışan bir Windows hizmetidir. DMS doğrudan etkileşim kurulamayan bir arka plan işlemidir. Ancak, bakabilirsiniz sorgu planları toosee veri taşıma gerekli toorun olduğundan DMS işlemlerini meydana geldiğinde her paralel sorguda.

## <a name="optimized-for-data-warehouse-workloads"></a>Data warehouse iş yükleri için en iyi duruma getirilmiştir
Merhaba MPP yaklaşımı dahil olmak üzere belirli bir performans iyileştirmeleriyle birkaç veri tarafından destekli:

* Tüm verileri kapsayan karmaşık istatistikler kümesi ve bir dağıtılmış sorgu iyileştiricisi. Veri boyutu ve dağıtım bilgileri kullanarak, hello mümkün toooptimize sorguları hello belirli dağıtılmış sorgu işlemlerinin maliyetini değerlendirerek hizmetidir.
* Gelişmiş algoritmalar ve teknikler hello verisine gerekli tooperform hello sorgu olarak bilgi işlem kaynakları arasında taşıma işlemi tooefficiently taşıma veri tümleşiktir. Bu veri taşıma işlemleri yerleşiktir ve tüm en iyi duruma getirme toohello veri taşıma hizmeti otomatik olarak gerçekleşir.
* Varsayılan olarak kümelenmiş **columnstore** dizinleri. SQL veri ambarı, sütun tabanlı depolamayı kullanarak geleneksel satır yönelimli depolamaya üzerinden ve too10x yukarı ortalama 5 kat sıkıştırma kazancı ya da daha fazla sorgu performansı kazancı alır. Tooscan gereken analitik sorguları çok sayıda satır columnstore dizinleri ile daha iyi çalışır.


## <a name="predictable-and-scalable-performance-with-data-warehouse-units"></a>Veri Ambarı Birimleri ile tahmin edilebilir ve ölçeklenebilir performans
SQL Veri Ambarı SQL Veritabanı ile benzer teknolojiler kullanılarak oluşturulmuştur, bu da kullanıcıların analitik sorgular için tutarlı ve öngörülebilir performans elde etmesini sağlar. Kullanıcıları ekleme veya çıkarma işlem düğümleri olarak toosee performans ölçek doğrusal olarak beklemelisiniz. SQL Data Warehouse kaynakları tooyour ayrılması Data Warehouse birimlerinde (Dwu) ölçülür. Dwu'lar CPU, bellek, tooyour SQL veri ambarı ayrılmış IOPS, temel alınan kaynakların bir ölçü var. Merhaba Dwu sayısı artırıldığında kaynaklar ve performansı artırır. DWU’lar özellikle aşağıdakilere yardımcı olur:

* Merhaba temel alınan donanım veya yazılım hakkında endişelenmeden, veri ambarı mümkün tooscale var.
* Merhaba işlem, veri ambarının değiştirmeden önce bir DWU düzeyindeki performans artışını tahmin edebilirsiniz.
* Merhaba temel alınan donanım veya yazılım örneğinizi değiştirebilir veya iş yükü performansınızı etkilemeden taşınır.
* Microsoft hello İş yükünüzün performansını etkilemeden hello hizmetin mimarisi temel hello artırabilir.
* Microsoft SQL veri ambarı performans ölçeklenebilir bir şekilde hızlı bir şekilde artırabilir ve eşit etkileri sistem hello.

Veri Ambarı Birimleri, veri ambarı iş yükü performansı ile son derece bağıntılı olan üç ölçüm sağlar. Merhaba aşağıdaki iş yükü ölçümleri ölçek hello dwu'larla doğrusal olarak anahtarı.

**Tarama/Toplama:** Çok sayıda satırı tarayan ve ardından karmaşık bir toplama işlemi gerçekleştiren standart bir veri ambarı sorgusu. Bu, G/Ç ve CPU yoğunluklu bir işlemdir.

**Yük:** özelliği tooingest veri hello hizmetinde hello. Yükler, Azure Depolama Blobları veya Azure Data Lake PolyBase ile en iyi şekilde gerçekleştirilir. Bu, tasarlanmış toostress ağ ve CPU yönlerine hello hizmet ölçümüdür.

**Create Table As Select (CTAS):** CTAS bir tabloyu hello özelliği toocopy ölçer. Bu, verilerin tüm hello Gereci hello düğümlerine dağıtılmasını ve toostorage yeniden yazma depolama alanından okunmasını içerir. CPU, G/Ç ve ağ yoğunluklu bir işlemdir.

## <a name="built-on-sql-server"></a>Yerleşik SQL Server
SQL veri ambarı hello SQL Server ilişkisel veritabanı altyapısını temel alır ve bir kurumsal veri ambarından beklediğiniz hello özelliklerinin çoğunu içerir. T-SQL zaten biliyorsanız, kolay tootransfer olduğundan, Bilgi Bankası tooSQL veri ambarı. Olup ileri düzeyde veya kullanmaya yeni başlıyor, hello örnekler hello belge boyunca başlamak yardımcı olur. Genel olarak, biz SQL Data Warehouse hello dil öğelerini şu şekilde oluşturulan olduğunu hello şekilde oluşturduğumuzu kabul:

* SQL Veri Ambarı birçok işlem için T-SQL söz dizimini kullanır. Ayrıca depolanan yordamlar, kullanıcı tanımlı işlevler, tablo bölümleme, dizinler ve harmanlamalar gibi çok sayıda geleneksel SQL yapısını destekler.
* SQL Veri Ambarı kümelenmiş **columnstore** dizinleri, PolyBase tümleştirme ve veri denetimi (tehdit değerlendirmesi içerir) dahil olmak üzere daha yeni SQL Server özelliklerini de içerir.
* Veri ambarı iş yükleri için daha az yaygın olan ya da daha yeni tooSQL sunucusu olan bazı T-SQL dil öğeleri şu anda kullanılamayabilir. Daha fazla bilgi için bkz: Merhaba [geçiş belgeleri][Migration documentation].

Merhaba Transact-SQL ve SQL Server, SQL Data Warehouse, SQL Database ve analiz platformu sistemi arasında ortaklık özelliği, veri ihtiyaçlarınıza uygun bir çözümü geliştirebilirsiniz. Karar verebilirsiniz nerede tookeep, verilerinizi temel performans, güvenlik ve ölçeklendirme gereksinimlerine ve sonra aktarımı verileri farklı sistemler arasında gereken şekilde.

## <a name="data-protection"></a>Veri koruma
SQL Veri Ambarı tüm verileri Azure Premium yerel olarak yedekli depolama alanında depolar. Merhaba yerel veri merkezi tooguarantee saydam veri koruma yerelleştirilmiş hatalarına karşı hello verileri birden çok zaman uyumlu kopyası saklanır. Ayrıca, SQL Veri Ambarı Azure Depolama Anlık Görüntüleri kullanarak etkin (duraklatılmamış) veritabanlarınızı otomatik olarak yedekler. hakkında daha fazla yedekleme ve çalışır, toolearn bkz hello [yedekleme ve geri yüklemeye genel bakış][Backup and restore overview].

## <a name="integrated-with-microsoft-tools"></a>Microsoft araçları ile tümleşiktir
SQL veri ambarı, SQL Server kullanıcıların tanıyor olabileceği çok hello aracını ayrıca ile tümleştirir. Bu araçlar şunları içerir:

**Geleneksel SQL Server araçları:** SQL Veri Ambarı SQL Server Analysis Services, Integration Services ve Reporting Services ile tam olarak tümleşiktir.

**Bulut tabanlı araçlar:** SQL Veri Ambarı; Data Factory, Stream Analytics, Machine Learning ve Power BI dahil olmak üzere Azure’daki çeşitli hizmetler ile tümleştirilebilir. Daha kapsamlı bir liste için bkz. [Tümleşik araçlara genel bakış][Integrated tools overview].

**Üçüncü taraf araçları:** Çok sayıda üçüncü taraf aracı sağlayıcısına ait araç, SQL Veri Ambarı ile sertifikalı tümleştirmeye sahiptir. Tam bir liste için bkz. [SQL Veri Ambarı çözüm ortakları][SQL Data Warehouse solution partners].

## <a name="hybrid-data-sources-scenarios"></a>Karma veri kaynakları senaryoları
Polybase tooleverage verir tanıdık T-SQL komutlarını kullanarak farklı kaynaklardaki verilerinizi. Polybase, normal bir tablo gibi sorgulamanıza Azure Blob depolamada tutulan ilişkisel olmayan verileri tooquery sağlar. Polybase tooquery ilişkisel olmayan verileri veya tooimport ilişkisel olmayan verileri SQL Data Warehouse'a kullanın.

* PolyBase, dış tablolara tooaccess ilişkisel olmayan verileri kullanır. Merhaba tablo tanımları SQL veri ambarı'nda depolanır ve normal ilişkisel verilere erişirken araçlarla ve SQL kullanarak erişebilirsiniz.
* Polybase, tümleştirme sırasında bağımsız şekilde hareket eder. Bunu çıkarır hello aynı özellikleri ve destekliyorsa işlevselliği tooall hello kaynakları. Polybase tarafından okunan hello veriler, sınırlandırılmış dosyalar veya ORC dosyaları dahil olmak üzere çeşitli biçimlerde olabilir.
* PolyBase, ayrıca bir Hdınsight kümesi için depolama alanı olarak kullanılıyor kullanılan tooaccess blob depolama olabilir. Toohello bu erişmenizi ilişkisel ve ilişkisel olmayan araçlarla aynı verilere.

## <a name="sla"></a>SLA
SQL Veri Ambarı, Microsoft Online Services SLA’nın parçası olarak ürün düzeyinde hizmet düzeyi sözleşmesi (SLA) sağlar. Daha fazla bilgi için [SQL Veri Ambarı için SLA][SLA for SQL Data Warehouse] bölümünü ziyaret edin. Tüm diğer ürünlerle ilgili SLA bilgileri için hello ziyaret edebilirsiniz [hizmet düzeyi sözleşmeleri] Azure sayfa veya üzerinde hello indirme [Toplu Lisanslama] [ Volume Licensing] sayfası. 

## <a name="next-steps"></a>Sonraki adımlar
SQL veri ambarı hakkında biraz bildiğinize göre bilgi nasıl tooquickly [SQL Data Warehouse oluşturma] [ create a SQL Data Warehouse] ve [örnek verileri yükleme][load sample data]. Yeni tooAzure varsa, hello bulabilirsiniz [Azure sözlüğünü] [ Azure glossary] yeni terimlerle karşılaşabileceğinizi yararlıdır. Alternatif olarak, aşağıdaki diğer SQL Veri Ambarı Kaynakları’na göz atın.  

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
[hizmet düzeyi sözleşmeleri]: https://azure.microsoft.com/en-us/support/legal/sla/
