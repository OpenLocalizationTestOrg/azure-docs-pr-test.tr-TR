---
title: "Azure SQL Data Warehouse işlemleri hakkında aaaLearn | Microsoft Docs"
description: "SQL Data Warehouse'un esnekliği sayesinde, bir veri ambarı birimi (DWU) kaydırıcı ölçeğini kullanarak işlem gücünü büyütebilir, küçültebilir veya duraklatabilirsiniz. Bu makalede hello veri ambarı ölçümleri ve ne tooDWUs ilişkili oldukları açıklanmaktadır. "
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: cadffa9c-589d-4db7-888a-1f202a753bc5
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 8be5ff6b14ab907e2b0a7eb55e0e2f4139aca8b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-warehouse-workload"></a>Veri ambarı iş yükü
Veri ambarı iş yükü, bir veri ambarında gerçekleşen hello işlemlerinin tooall ifade eder. Merhaba veri ambarı iş yükü hello warehouse'a veri yükleme, analiz gerçekleştirme ve raporlama hello veri ambarı üzerinde hello veri ambarındaki yönetme ve hello veri ambarındaki verileri dışarı aktarma hello tüm sürecini kapsar. Merhaba derinliği ve genişliği bu bileşenlerin genellikle hello olgunluk seviyesine hello veri ambarı ile verilmesidir.

## <a name="new-toodata-warehousing"></a>Yeni toodata depolama?
Veri ambarı birinden yüklenen veriler koleksiyonudur veya daha fazla veri kaynakları ve Raporlama ile veri analizi gibi iş zekası görevlerinin kullanılan tooperform.

Veri ambarları, büyük sayıda satırı, geniş veri aralıklarını taraması ve analiz ve raporlama hello amaçları için görece büyük sonuçlar döndürebilir sorgular tarafından belirlenir. Veri ambarları aynı zamanda görece büyük veri yüklerine karşı küçük işlem düzeyindeki eklemeler/güncelleştirmeler/silmelere göre belirlenir.

* Merhaba veri tooscan çok sayıda satırı veya geniş veri aralıklarını gereken sorguları iyileştiren bir şekilde depolandığı zaman veri ambarı en iyi şekilde gerçekleştirir. Bu tarama türü Hello veriler depolanır ve satırlar yerine sütunlara göre arama, en iyi şekilde çalışır.

> [!NOTE]
> Sütun depolamayı kullanan hello bellek içi columnstore dizini, raporlama ve analiz sorguları için geleneksel ikili ağaçlara göre too10x sıkıştırma kazancı ve 100 kata kadar sorgu performansı kazancı sağlar. Biz columnstore dizinleri hello depolamak ve veri ambarındaki büyük veri tarama standart göz önünde bulundurun.
> 
> 

* Bir veri ambarı, çevrimiçi işlem gerçekleştirme (OLTP) için iyileştirilen bir sistemden farklı gereksinimlere sahiptir. Merhaba OLTP sisteminde birçok ekleme, güncelleştirme ve silme işlemleri vardır. Bu işlemler hello tablosundaki satırları toospecific arama. Tablo aramaları hello veriler satır temelinde bir biçimde depolandığında en iyi şekilde çalışır. Merhaba veri sıralanabilir ve hızla bir ve Yönet yaklaşımı ikili ağaç veya btree araması olarak adlandırılan Yönet.

## <a name="data-loading"></a>Veri yükleme
Veri yükleme hello veri ambarı iş yükü, büyük bir parçasıdır. İşletmeler genellikle müşteriler ticari işlemler zaman oluşturduğunu hello gün boyunca değişiklikleri izleyen meşgul OLTP sistemlerine sahiptir. Düzenli aralıklarla, genellikle gece bakım penceresi sırasında hello işlemleri taşınır veya toohello veri ambarı kopyalanır. Merhaba veri hello veri ambarında eklendiğinde, analistleri çözümlemesi ve iş kararları hello verileri.

* Geleneksel olarak, yükleme hello işleme ayıklama, dönüştürme ve yükleme için ETL verilir. Verilerin genellikle toobe hello veri ambarındaki diğer verilerle tutarlı olduğundan dönüştürülmeleri gerekir. Daha önce işletmelerin adanmış ETL sunucuları tooperform hello dönüşümleri kullanılır. Artık, bu tür hızlı olan yüksek düzeyde paralel işleme sayesinde önce SQL Data Warehouse'a veri yükleme ve hello dönüştürmeleri gerçekleştirebilirsiniz. Bu işlem ayıklama, yükleme ve dönüştürme (ELT) olarak adlandırılır ve hello veri ambarı iş yükü için yeni bir standart hale gelmektedir.

> [!NOTE]
> SQL Server 2016 ile artık bir OLTP tablosunda analizleri gerçek zamanlı olarak gerçekleştirebilirsiniz. Bu olmayan bir veri ambarı toostore hello gereksinimini değiştirin ve verileri çözümlemek, ancak gerçek zamanlı bir şekilde tooperform analizi sağlar.
> 
> 

### <a name="reporting-and-analysis-queries"></a>Raporlama ve analiz sorguları
Raporlama ve analiz sorguları genellikle bir dizi ölçüte göre küçük, orta ve büyük olarak sınıflandırılır ancak sınıflandırma çoğunlukla süreye göre yapılır. Çoğu veri ambarında, hızlı çalışan ve uzun süre çalışan sorgulardan oluşan karma bir iş yükü bulunur. İsteğe bağlı olarak her durumda, önemli toodetermine olduğundan bu karıştırma ve toodetermine sıklığının (saatlik, günlük, ay sonu, üç aylık dönem bitişi vb.). Karma sorgu iş yükü, eşzamanlılık, veri ambarı için planlama sağlama tooproper kapasite ile birlikte hello önemli toounderstand olur.

* Özellikle, bir uzun bekleme süresi tooadd kapasite toohello veri ambarına gerektiğinde kapasite planlaması bir karma sorgu iş yükü için karmaşık bir görev olabilir. SQL Data Warehouse kapasite planlaması aciliyetini hello büyür ve işlem kapasitesini herhangi bir zamanda ve depolama itibaren küçültmek ve işlem kapasitesi bağımsız olarak boyutlandırıldığından ortadan kaldırır.

### <a name="data-management"></a>Veri yönetimi
Veri Yönetimi özellikle hello yakın zaman içindeki disk alanı yetersiz çalışabilir bildiğinizde önemlidir. Veri ambarları bir tabloda bölümler olarak depolanır anlamlı aralıklara genellikle hello verileri bölün. Tüm SQL Server tabanlı ürünler hello tablo ve bölümleri taşımanıza olanak tanır. Eski veri tooless pahalı depolama taşıyın ve hello son verileri çevrimiçi depolama alanında tutabilirsiniz Bu bölüm değiştirme olanağı sağlar.

* Columnstore dizinleri bölümlenmiş tabloları destekler. Columnstore dizinlerinde bölümlenmiş tablolar, veri yönetimi ve arşivleme için kullanılır. Satır temelinde depolanan tablolarda, bölümler sorgu performansında daha büyük bir role sahiptir.  
* PolyBase verilerin yönetiminde önemli bir rol oynar. Polybase'i kullanarak, hello seçeneği tooarchive eski veri tooHadoop veya Azure blob depolama alanına sahip.  Bu, Hello veriler halen çevrimiçi olduğundan çok sayıda seçenekleri sağlar.  Hadoop tooretrieve veri daha uzun sürebilir ancak alma süresinin sağladığı kazanç hello hello depolama maliyetinden üstün olabilir.

### <a name="exporting-data"></a>Verileri dışarı aktarma
Raporlar ve çözümleme için kullanılabilen tek yönlü toomake verileri rapor ve analiz çalıştırmak için adanmış hello veri ambarı tooservers toosend verilerdir. Bu sunuculara veri reyonları adı verilir. Örneğin, önceden, rapor verilerini işlemek ve hello veri ambarı toomany sunucuları Merhaba Dünya toomake verilecek, müşterilerin ve çözümleyicilerin geniş çapta kullanılabilir.

* Rapor oluşturmak için her gece salt okunur raporlama sunucularını hello günlük verilerin bir anlık görüntüsünü ile doldurabilirsiniz. Bu daha yüksek bant genişliği müşteriler için hello işlem kaynağı ihtiyaçları hello veri ambarı düşürürken sağlar. Güvenlik açısından, veri reyonlarını tooreduce hello erişim toohello veri ambarına sahip kullanıcıların sayısını sağlar.
* Analiz için ya da hello veri ambarında bir çözümleme küpü oluşturmak ve analiz hello veri ambarına karşı çalıştırabilir veya verilerini önceden işleyebilir ve ek analizler toohello analiz sunucusuna dışarı aktarma.

## <a name="next-steps"></a>Sonraki adımlar
SQL veri ambarı hakkında biraz bildiğinize göre bilgi nasıl tooquickly [SQL Data Warehouse oluşturma] [ create a SQL Data Warehouse] ve [örnek verileri yükleme][load sample data].

<!--Image references-->

<!--Article references-->
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md

<!--MSDN references-->

<!--Other web references-->
