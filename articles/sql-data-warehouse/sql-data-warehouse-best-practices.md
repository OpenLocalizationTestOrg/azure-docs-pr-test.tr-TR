---
title: "Azure SQL Data Warehouse için aaaBest uygulamaları | Microsoft Docs"
description: "Azure SQL Veri Ambarı için çözüm geliştirirken bilmeniz gerekenlerle ilgili öneriler ve en iyi yöntemler. Bu veriler, başarılı olmanıza yardımcı olacaktır."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 7b698cad-b152-4d33-97f5-5155dfa60f79
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 1f42908fc03e1ca52278a6853d1afe9543d648b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-sql-data-warehouse"></a>Azure SQL Veri Ambarı için en iyi yöntemler
Bu makalede, Azure SQL veri ambarı en iyi performansı tooachieve yardımcı olacak birçok en iyi yöntemler koleksiyonudur.  Bu makalede hello kavramları temel ve kolay tooexplain bazıları, diğer kavramları daha gelişmiş ve biz yalnızca hello yüzeyini bu makalede karalama.  Bu makalede Hello amacı toogive, bazı temel yönerge ve tooraise tanıma önemli alanlar toofocus yazarken, yapı, veri ambarı.  Her bölüm tooa kavram ve hangi kapak hello kavram daha kapsamlı olarak ayrıntılı toomore makaleler sonra noktası tanıtır.

Azure SQL Veri Ambarı ile çalışmaya yeni başladıysanız, bu makale gözünüzü korkutmasın.  Merhaba hello konuları çoğunlukla hello önem sırasına dizisidir.  Merhaba üzerinde ilk birkaç kavram Odaklanıldığında başlatırsanız, iyi şeklinde olacaktır.  SQL Veri Ambarı hakkında daha fazla bilgi edinip daha çok kullanmaya başladıktan sonra bu makaleye dönerek birkaç kavrama daha göz atabilirsiniz.  Bunu sürmez için her şeyi toomake algılama uzun.

## <a name="reduce-cost-with-pause-and-scale"></a>Duraklatma ve ölçeklendirme ile maliyetleri azaltın
Kullanmadığınızda bir anahtar SQL Data Warehouse hello özelliği toopause hangi işlem kaynakları hello faturalama durdurur özelliğidir.  Başka bir anahtar hello özelliği tooscale kaynakları özelliğidir.  Duraklatma ve ölçeklendirme hello Azure portal aracılığıyla veya PowerShell komutları ile yapılabilir.  Kullanımda olmadığında, veri Ambarınızı hello maliyetini büyük ölçüde azaltabilir gibi bu özellikleri hakkında bilgi sahibi olur.  Her zaman veri ambarınız erişilebilir istiyorsanız, duraklatma yerine toohello en küçük boyuta, bir DW100 ölçeklendirme tooconsider isteyebilirsiniz.

Ayrıca bkz. [İşlem kaynaklarını duraklatma][Pause compute resources], [İşlem kaynaklarını sürdürme][Resume compute resources], [İşlem kaynaklarını ölçeklendirme].

## <a name="drain-transactions-before-pausing-or-scaling"></a>Duraklatma veya ölçeklendirme öncesinde işlemleri boşaltın
Duraklattığınızda veya SQL Data Warehouse ölçeklendirebilir hello başlattığınızda sorgularınızı iptal edilir hello arka planda duraklatmak veya istek ölçeklendirin.  Basit seçme sorgusu iptal etme hızlı bir işlemdir ve toopause neredeyse hiçbir etkisi toohello süresini sahip veya örneğinizi ölçeklendirin.  Ancak, verileri veya hello yapınızı hello veri değiştirmek, işlem sorguları mümkün toostop hızla olmayabilir.  **Bir işlem sorgusunun tamamlanması veya yaptığı değişiklikleri geri alması gerekir.**  Uzun veya hatta daha uzun süre, hello özgün değişiklik hello sorgu uygulama gibi bir işlem sorgu tarafından tamamlanan hello çalışma geri alabilir.  Örneğin, satırları silme ve bir saat için bir zaten çalışan bir sorgu iptal ederseniz, bu hello sistem, silinen bir saat tooinsert geri hello satırlarını ele geçirebilir.  Duraklatma ya da işlemleri, duraklatma uçuş modunda olan ya da ölçeklendirme tootake görünebilir ölçeklendirme çalıştırıyorsanız, devam etmeden önce uzun zaman duraklatma ve ölçeklendirme hello geri alma toocomplete toowait sahip olduğundan.

Ayrıca bkz. [İşlemleri anlama][Understanding transactions], [İşlemleri iyileştirme][Optimizing transactions]

## <a name="maintain-statistics"></a>İstatistiklerin bakımını yapın
Sütunlarla ilgili istatistikleri otomatik olarak algılayıp oluşturan veya güncelleştiren SQL Server’dan farklı olarak, SQL Veri Ambarı’nda istatistiklerin bakımının kullanıcı tarafından yapılması gerekir.  Biz toochange planlarken bu hello SQL Data Warehouse planları Merhaba, istatistikleri tooensure toomaintain isteyeceksiniz artık gelecek için en iyi duruma getirilmiş.  Hello iyileştiricisi tarafından oluşturulan hello planlar yalnızca hello kullanılabilir istatistikleri kadar iyi olur.  **Her sütunda örneklenen istatistikleri oluşturma kolay bir yolu tooget istatistikleri ile başlatıldı.**  Önemli değişiklikler tooyour veri ortaya eşit oranda önemli tooupdate istatistikleri olur.  Koruyucu bir yaklaşım tooupdate, ya da her yük sonra günlük, istatistikleri olabilir.  Dengelemeler performans ve hello maliyet toocreate ve güncelleştirme istatistiklerini arasındaki her zaman vardır. Tüm, istatistik uzun toomaintain sürüyor bulursanız, hangi sütunların istatistiklerine sahip veya hangi sütunların hakkında daha fazla seçmeli tootry toobe sık sık güncelleştirilmesi gerekmeyen isteyebilirsiniz.  Örneğin, burada yeni değerleri olabilir eklenen günlük tooupdate tarih sütunlarının isteyebilirsiniz. **Sütunlarda söz konusu birleşimlerde GROUP BY yan tümcesi ve sütun bulundu hello kullanılan sütun istatistikleri sağlayarak hello çoğu avantajı elde edersiniz.**

Ayrıca bkz. [Tablo istatistiklerini yönetme][Manage table statistics], [CREATE STATISTICS][CREATE STATISTICS], [UPDATE STATISTICS][UPDATE STATISTICS]

## <a name="group-insert-statements-into-batches"></a>INSERT deyimlerini gruplayın
Bir deyim gereksinimlerinizi ister için bir kerelik yük tooa küçük bir tablo INSERT deyimi veya hatta düzenli aralıklarla yeniden bir arama, düzgün gerçekleştirebilir `INSERT INTO MyLookup VALUES (1, 'Type 1')`.  Ancak, binlerce veya milyonlarca tooload satır hello gün boyunca gerekiyorsa, singleton EKLER yalnızca yetişemiyor bulabilirsiniz.  Bunun yerine, böylece tooa dosyası yazma ve başka bir işlem düzenli aralıklarla gelen ve bu dosyayı yükler işlemlerinizi geliştirin.

Ayrıca bkz. [INSERT][INSERT]

## <a name="use-polybase-tooload-and-export-data-quickly"></a>PolyBase tooload ve dışarı aktarma verileri hızlı bir şekilde kullanma
SQL Veri Ambarı, veri yüklemek ve dışarı aktarmak için Azure Data Factory, PolyBase ve BCP gibi birçok aracı destekler.  Performansın yüksek öneme sahip olmadığı küçük miktarlardaki veriler için bu araçlardan herhangi birini kullanabilirsiniz.  Ancak, yüklenirken veya büyük miktarda veriyi dışa aktarma veya hızlı performans gerekli olduğunda PolyBase hello en iyi seçimdir.  PolyBase tasarlanmış tooleverage hello MPP (yüksek düzeyde paralel işleme) SQL veri ambarı mimarideki ve bu nedenle yük ve veri magnitudes başka bir araç daha hızlı verin.  PolyBase yükleri CTAS veya INSERT INTO ile çalıştırılabilir.  **İşlem günlüğü ve hello en hızlı yolu tooload CTAS kullanarak verilerinizi küçülür.**  Azure Data Factory, PolyBase yüklerini de destekler.  PolyBase, Gzip de dahil olmak üzere birçok dosya biçimi için destek sunar.  **gzip metin dosyaları, sonu 60 ya da daha fazla dosya toomaximize paralellik, iş yükünün kullanırken toomaximize işleme.**  Toplam hızı artırmak için verilerinizi aynı anda yükleyin.

Ayrıca bkz. [Yerel veriler][Load data], [PolyBase kullanma kılavuzu][Guide for using PolyBase], [Azure SQL Veri Ambarı yükleme modelleri ve stratejileri][Azure SQL Data Warehouse loading patterns and strategies], [Azure Data Factory ile veri yükleme][Load Data with Azure Data Factory], [Azure Data Factory ile veri taşıma][Move data with Azure Data Factory], [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT], [Create table as select (CTAS)][Create table as select (CTAS)]

## <a name="load-then-query-external-tables"></a>Dış tabloları önce yükleyip sonra sorgu çalıştırın
Polybase, dış tablo olarak da bilinen hello en hızlı yolu tooload veri olabilirler, ancak sorguları için en uygun değil. SQL Veri Ambarı Polybase tabloları şimdilik yalnızca Azure blob dosyalarını desteklemektedir. Bu dosyaları destekleyen herhangi bir işlem kaynağı yoktur.  Sonuç olarak, SQL veri ambarı bu iş boşaltma olamaz ve dosyanın tamamı hello sipariş tooread hello veri tootempdb yükleyerek bu nedenle okuması gerekir.  Bu nedenle, bu verileri Sorgulama birkaç sorgular varsa, daha iyi tooload bu kez verilerdir ve sahip sorguları hello yerel tabloyu kullanın.

Ayrıca bkz. [PolyBase kullanma kılavuzu][Guide for using PolyBase]

## <a name="hash-distribute-large-tables"></a>Büyük tabloları karma olarak dağıtın
Tablolar varsayılan olarak Hepsini Bir Kez Deneme yöntemiyle dağıtılmıştır.  Bu, kullanıcıların tooget tablolarıyla nasıl dağıtılacağı toodecide gerek kalmadan tabloları oluşturmaya başlamanızı kolaylaştırır.  Hepsini Bir Kez Deneme tabloları, belirli iş yükleri için yeterli performans sunabilir ancak birçok durumda dağıtım sütunu seçilmesi daha iyi sonuç verecektir.  iki büyük olgu tabloları katıldığında, ne zaman bir sütun tarafından dağıtılan bir tablo hepsini bir kez tablo kadar aşar hello en yaygın örnektir.  Örneğin, order_id tarafından dağıtılır, Siparişler tablosu ve siparişler tablo tooyour işlemleri tablosu üzerinde order_id katıldığında, ayrıca order_id tarafından dağıtılır, işlemleri tablo varsa, bu sorgu anlamına gelir bir doğrudan geçirilen sorgu olur Biz, veri taşıma işlemleri ortadan kaldırır.  Adım sayısı ne kadar az olursa sorgu o kadar hızlı işlenir.  Taşınan veri miktarı azaldıkça sorgunun hızı artar.  Bu açıklama yalnızca hello yüzeyini sıyırıyor. Dağıtılmış bir tablo yüklenirken bu, yükleri yavaşlatır gibi gelen verilerinizi hello dağıtım anahtarı sıralı değil olduğundan emin olun.  Merhaba aşağıdaki bağlantılar çok için nasıl dağıtım sütunun seçilmesi yanı sıra performansını hakkında daha fazla ayrıntı görmek toodefine hello WITH yan tümcesinde oluşturduğunuz TABLOLARA deyiminizde dağıtılmış bir tablo.

Ayrıca bkz. [Tabloya genel bakış][Table overview], [Tablo dağıtımı][Table distribution], [Tablo dağıtımına genel bakış][Selecting table distribution], [CREATE TABLE][CREATE TABLE], [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="do-not-over-partition"></a>Aşırı bölümleme yapmayın
Verileri bölümleme, bölüm değiştirme ile verilerinizin bakımını yapma veya bölüm eleme ile tarama iyileştirme konularında etkili olsa da, bölüm sayısının çok fazla olması sorgularınızı yavaşlatabilir.  Genelde SQL Server üzerinde iyi çalışan çok parçalı bölüm stratejisi SQL Veri Ambarı söz konusu olduğunda verimli olmayabilir.  Her bölüm 1 milyondan az satır varsa çok fazla bölümlemeye sahip olmak da kümelenmiş columnstore dizinleri hello verimliliğini azaltabilir.  Merhaba arka planda, SQL Data Warehouse verilerinizi sizin için 60 veritabanlarına bölümler olduğunu aklınızda bulundurun 100 bölümlerin bulunduğu bir tablo oluşturursanız, bu gerçekte 6000 bölümlerinde kaynaklanır.  Her iş yükü farklı olduğundan Hello en iyi ne işleminizi iş yükü için en iyi şekilde çalışır toosee bölümlendirme ile tooexperiment öneridir.  SQL Server’da kullandığınızdan daha az parça kullanmayı deneyin.  Örneğin, günlük bölümler yerine haftalık veya aylık bölümler kullanın.

Ayrıca bkz. [Tablo bölümleme][Table partitioning]

## <a name="minimize-transaction-sizes"></a>İşlem boyutları en aza indirin
Bir işlemde çalışan INSERT, UPDATE ve DELETE deyimleri başarısız olduğunda gerçekleştirilen adımların geri alınması gerekir.  toominimize hello uzun bir geri alma için olası hareket boyutları mümkün olduğunda en aza indirin.  Bunu yapmak için INSERT, UPDATE ve DELETE deyimlerini parçalara ayırabilirsiniz.  Hangi tootake 1 saat, mümkünse beklediğiniz INSERT varsa, örneğin, INSERT hello her 15 dakika içinde çalışacak 4 parçalara bölmek.  CTAS, TRUNCATE, DROP TABLE veya INSERT tooempty tabloları, tooreduce geri alma risk gibi özel en az oturum durumları yararlanın.  Başka bir şekilde tooeliminate düzeyine toouse yalnızca meta veri işlemleri bölüm için veri yönetimi değiştirme gibi olur.  Örneğin, bunun yerine hello order_date 2001 Ekim bulunduğu bir tablodaki tüm satırları silme deyimi toodelete yürütme daha verilerinizi aylık bölümleme ve başka bir tablodan boş bir bölüm için veri hello bölümüyle çıkışı geçiş (ALTER bakın Tablo örnekler).  Bölümlenmemiş tablolar için silme kullanmak yerine tookeep bir tabloda istediğiniz CTAS toowrite hello verileri kullanarak göz önünde bulundurun.  Bir CTAS varsa alır Merhaba aynı miktarda süre, çok az işlem günlüğü vardır ve hızlı bir şekilde gerekirse iptal edilebilir çok daha güvenli bir işlemi toorun olur.

Ayrıca bkz. [İşlemleri anlama][Understanding transactions], [İşlemleri iyileştirme][Optimizing transactions], [Tablo bölümleme][Table partitioning], [TRUNCATE TABLE][TRUNCATE TABLE], [ALTER TABLE][ALTER TABLE], [Create table as select (CTAS)][Create table as select (CTAS)]

## <a name="use-hello-smallest-possible-column-size"></a>Merhaba en küçük olası sütun boyutu kullanın
DDL'nizi tanımlarken, verilerinizi destekleyen hello en küçük veri türünü kullanarak sorgu performansı iyileştirir.  Bu durum özellikle CHAR ve VARCHAR sütunları için önemlidir.  Bir sütundaki en uzun değer Hello 25 karakterden oluşuyorsa, sütun VARCHAR(25) tanımlayın.  Tüm karakter sütunları tooa büyük varsayılan uzunluk tanımlamamaya özen gösterin.  Ayrıca, NVARCHAR şart değilse sütunları VARCHAR olarak tanımlayın.

Ayrıca bkz. [Tabloya genel bakış][Table overview], [Tablo veri türleri][Table data types], [CREATE TABLE][CREATE TABLE]

## <a name="use-temporary-heap-tables-for-transient-data"></a>Geçiş verileri için geçici yığın tabloları kullanın
Verileri SQL Data Warehouse geçici olarak giriş, öbek tablosunu kullanarak genel işlem daha hızlı hello yapacağı bulabilirsiniz.  Verileri yalnızca toostage hello tablo tooheap yüklenirken daha fazla dönüşümleri çalıştırmadan önce hello veri tooa yüklemekten daha hızlı olacak, yüklüyorsanız columnstore tablo kümelenmiş.  Ayrıca, veri tooa yüklenirken geçici tablo ayrıca çok tablo toopermanent depolama yüklenirken daha hızlı yükler.  Geçici tablolara Başlat "#" ile ve yalnızca sınırlı senaryolarda yalnızca çalışabilir şekilde oluşturulduğu, hello oturumu tarafından erişilebilir.   Yığın tabloları hello WITH yan tümcesinde CREATE TABLE tanımlanır.  Geçici bir tablo kullanırsanız, bu geçici tablo üzerinde toocreate istatistikleri çok unutmayın.

Ayrıca bkz. [Geçici tablolar][Temporary tables], [CREATE TABLE][CREATE TABLE], [CREATE TABLE AS SELECT][CREATE TABLE AS SELECT]

## <a name="optimize-clustered-columnstore-tables"></a>Kümelenmiş columnstore tablolarını iyileştirin
Kümelenmiş columnstore dizinleri hello en verimli şekilde Azure SQL Data Warehouse verilerinizi depolamak biridir.  SQL Veri Ambarı tabloları varsayılan ayarda Kümelenmiş ColumnStore olarak oluşturulur.  tooget hello en iyi performans iyi segment kalite olan columnstore tabloları sorgulamaları için önemlidir.  Bellek baskısı altında toocolumnstore tablolar satır yazılırken columnstore segment kalite düşebilir.  Segment kalitesi, sıkıştırılmış Satır Grubu içindeki satır sayısıyla ölçülebilir.  Merhaba bkz [zayıf columnstore nedenleri dizin kalitesi] [ Causes of poor columnstore index quality] hello içinde [tablo dizinleri] [ Table indexes] makalesi için adım adım yönergeler Algılama ve kümelenmiş columnstore tabloları için segment kaliteyi artırma.  Yüksek kaliteli columnstore kesimleri önemli olduğundan, veri yükleme için hello Orta veya büyük bir kaynak sınıfı olan bir fikir toouse kullanıcıların kimliklerini değildir.  Merhaba kullanın, daha az Dwu tooassign tooyour kullanıcı yüklenirken isteyeceksiniz hello büyük hello kaynak sınıfı.

Columnstore tabloları genellikle veri sıkıştırılmış columnstore kesimi tablo başına 1 milyondan fazla satır vardır ve her bir SQL Data Warehouse tablo altın kural, 60 tablolara bölümlenmiş kadar anında olmaz beri columnstore tabloları bir sorgu yararlı olmaz Merhaba tablo 60 milyondan fazla satır olmadıkça.  60 milyondan az satırları içeren tablo için onu herhangi algılama toohave bir columnstore dizini kalmasına neden olabilir değil.  Kullanmanın da bir zararı olmayacaktır.  Ayrıca, verilerinizi bölerseniz, her bölüm bir kümelenmiş columnstore dizinindeki toohave 1 milyon satır toobenefit gerekir tooconsider isteyeceksiniz.  Bir tablo 100 bölümler içeren sonra toohave en az 6 milyon satır toobenefit kümelenmiş sütun deposu gerekir (60 dağıtımları * 100 bölümleri * 1 milyon satır).  Tablonuz Bu örnekte 6 milyon satır yoksa bölümleri hello sayısını azaltın veya yığın tablo kullanmayı düşünün.  Daha iyi performans columnstore tablo yerine ikincil dizinler yığın tabloyla ile kazanılan varsa denemeler toosee de olabilir.  Columnstore tabloları ikincil dizinleri henüz desteklememektedir.

Yalnızca gereksinim duyduğunuz hello sütunları seçerseniz bir columnstore tablosu sorgulanırken sorguları daha hızlı çalışacaktır.  

Ayrıca bkz. [Tablo dizinleri][Table indexes], [Columnstore dizinleri kılavuzu][Columnstore indexes guide], [Columnstore dizinlerini yeniden oluşturma][Rebuilding columnstore indexes]

## <a name="use-larger-resource-class-tooimprove-query-performance"></a>Daha büyük kaynak sınıfı tooimprove sorgu performansını kullanın
SQL veri ambarı bir şekilde tooallocate bellek tooqueries kaynak gruplarını kullanır.  Merhaba kutudan çıktığında, tüm kullanıcılar, 100 MB bellek dağıtım başına veren toohello küçük kaynak sınıfı atanır.  Olduğundan her zaman en az 100 MB, sistem geniş hello toplam bellek ayırma 6,000 MB ya da yalnızca altında 6 GB olan 60 dağıtımları ve her dağıtım verilir.  Büyük birleştirmeler veya yükleri tooclustered columnstore tabloları gibi bazı sorgular büyük bellek ayırma yararlı olacaktır.  Yalnızca tarama gibi bazı sorgulara ek atama yapılmaz.  Tootake isteyeceksiniz şekilde hello Çevir tarafında büyük kaynak sınıfları kullanan eşzamanlılık, bu tüm kullanıcıların tooa büyük kaynak sınıfınızın geçmeden önce dikkate etkiler.

Ayrıca bkz. [Eşzamanlılık ve iş yükü yönetimi][Concurrency and workload management]

## <a name="use-smaller-resource-class-tooincrease-concurrency"></a>Daha küçük bir kaynak sınıfı tooIncrease eşzamanlılık kullanın
Sizin haberiniz bile, kullanıcı sorgularının toohave uzun süren bir gecikme olmadığı, bunun olabilir, kullanıcılarınızın daha büyük kaynak sınıflarda çalıştırıyorsanız ve eşzamanlılık yuva yukarı diğer sorgular tooqueue neden çok tüketen.  Kullanıcıların sorguları sıraya alınan toosee çalıştırın `SELECT * FROM sys.dm_pdw_waits` herhangi bir satır döndürülürse toosee.

Ayrıca bkz. [Eşzamanlılık ve iş yükü yönetimi][Concurrency and workload management], [sys.dm_pdw_waits][sys.dm_pdw_waits]

## <a name="use-dmvs-toomonitor-and-optimize-your-queries"></a>Dmv'leri toomonitor kullanın ve sorgularınızı en iyi duruma getirme
SQL veri ambarı kullanılan toomonitor sorgu yürütme olabilen çeşitli Dmv'leri sahiptir.  Aşağıdaki makalede izleme hello nasıl toolook hello ayrıntılarını bir yürütme sırasında sorgu üzerinde adım adım yönergeler anlatılmaktadır.  Bu Dmv'leri tooquickly Bul sorguları, sorgularınızı hello etiket seçeneği kullanılarak yardımcı olabilir.

Ayrıca bkz. [DMV’leri kullanarak iş yükünüzü izleme][Monitor your workload using DMVs], [LABEL][LABEL], [OPTION][OPTION], [sys.dm_exec_sessions][sys.dm_exec_sessions], [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests], [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps], [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], [sys.dm_pdw_dms_workers], [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN], [sys.dm_pdw_waits][sys.dm_pdw_waits]

## <a name="other-resources"></a>Diğer kaynaklar
Genel sorunlar ve çözümleri için [Sorun giderme][Troubleshooting] makalemizi de inceleyin.

Bu makalede aradığınız bulamadıysanız, hello "Arama belgeleri için" Merhaba sol tarafındaki tüm bu sayfa toosearch hello Azure SQL Data Warehouse belgelerin kullanmayı deneyin.  Merhaba [Azure SQL Data Warehouse MSDN Forumu] [ Azure SQL Data Warehouse MSDN Forum] olan bir yer olarak tooother kullanıcıları ve toohello SQL veri ambarı ürün grubu, tooask sorular için oluşturma.  Biz etkin olarak sorularınızı ya da başka bir kullanıcı ya da bize biri tarafından yanıtlanan bu Forumu tooensure izleyin.  Yığın taşması üzerine sorularınızı tooask tercih ederseniz, biz de bir [Azure SQL veri ambarı yığın taşması Forumu][Azure SQL Data Warehouse Stack Overflow Forum].

Son olarak, lütfen hello kullanın [Azure SQL veri ambarı geri bildirim] [ Azure SQL Data Warehouse Feedback] sayfasında toomake özellik istekleri.  İsteklerinizi eklemeniz veya diğer istekleri oylamanız, özellikleri önceliklendirme konusunda bize yardımcı olmaktadır.

<!--Image references-->

<!--Article references-->
[Create a support ticket]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Create table as select (CTAS)]: ./sql-data-warehouse-develop-ctas.md
[Table overview]: ./sql-data-warehouse-tables-overview.md
[Table data types]: ./sql-data-warehouse-tables-data-types.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexes]: ./sql-data-warehouse-tables-index.md
[Causes of poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuilding columnstore indexes]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Manage table statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary tables]: ./sql-data-warehouse-tables-temporary.md
[Guide for using PolyBase]: ./sql-data-warehouse-load-polybase-guide.md
[Load data]: ./sql-data-warehouse-overview-load.md
[Move data with Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[Load data with Azure Data Factory]: ./sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Monitor your workload using DMVs]: ./sql-data-warehouse-manage-monitor.md
[Pause compute resources]: ./sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Resume compute resources]: ./sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[İşlem kaynaklarını ölçeklendirme]: ./sql-data-warehouse-manage-compute-overview.md#scale-compute
[Understanding transactions]: ./sql-data-warehouse-develop-transactions.md
[Optimizing transactions]: ./sql-data-warehouse-develop-best-practices-transactions.md
[Troubleshooting]: ./sql-data-warehouse-troubleshoot.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->
[ALTER TABLE]: https://msdn.microsoft.com/library/ms190273.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[CREATE TABLE AS SELECT]: https://msdn.microsoft.com/library/mt204041.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: https://msdn.microsoft.com/library/mt204017.aspx
[INSERT]: https://msdn.microsoft.com/library/ms174335.aspx
[OPTION]: https://msdn.microsoft.com/library/ms190322.aspx
[TRUNCATE TABLE]: https://msdn.microsoft.com/library/ms177570.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx
[sys.dm_exec_sessions]: https://msdn.microsoft.com/library/ms176013.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_request_steps]: https://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: https://msdn.microsoft.com/library/mt203889.aspx
[sys.dm_pdw_dms_workers]: https://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_waits]: https://msdn.microsoft.com/library/mt203893.aspx
[Columnstore indexes guide]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
[Selecting table distribution]: https://blogs.msdn.microsoft.com/sqlcat/2015/08/11/choosing-hash-distributed-table-vs-round-robin-distributed-table-in-azure-sql-dw-service/
[Azure SQL Data Warehouse Feedback]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Azure SQL Data Warehouse MSDN Forum]: https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=AzureSQLDataWarehouse
[Azure SQL Data Warehouse Stack Overflow Forum]:  http://stackoverflow.com/questions/tagged/azure-sqldw
[Azure SQL Data Warehouse loading patterns and strategies]: https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies
