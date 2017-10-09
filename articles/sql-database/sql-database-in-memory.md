---
title: "aaaAzure SQL veritabanı bellek içi teknolojileri | Microsoft Docs"
description: "Azure SQL veritabanı bellek içi teknolojileri işlem hello performansını ve analytics iş yükleri büyük ölçüde artırır. Bilgi nasıl bu teknolojiler tootake yararlanabilir."
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a>SQL veritabanı'nda Bellek içi teknolojileri kullanılarak performansı en iyi duruma getirme

Azure SQL veritabanı'nda Bellek içi teknolojilerini kullanarak, performans iyileştirmeleri çeşitli iş yükleri ile elde edebilirsiniz: işlem (çevrimiçi işlem işleme (OLTP)), analytics (çevrimiçi analitik işlem (OLAP)) ve karma (karma işlem/analitik işleme (HTAP)). Nedeniyle daha verimli sorgu ve işlem Merhaba, bellek içi teknolojileri de yardımcı tooreduce maliyeti. Fiyatlandırma katmanı hello veritabanı tooachieve performans artışı, tooupgrade hello genellikle gerekmez. Bazı durumlarda, hatta yazdıramayabilirsiniz fiyatlandırma katmanı, yine de performans iyileştirmeleri bellek içi teknolojileriyle görüyorsanız sırasında hello azaltın.

Aşağıda, bellek içi OLTP performansı toosignificantly nasıl Yardım iki örnek verilmiştir:

- Bellek içi OLTP kullanarak [çekirdek işletme çözümleri % 70 Dtu'lar arttırırken, iş yükü mümkün toodouble olan](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).
    - DTU anlamına gelir *veritabanı işleme birimi*, ve kaynak tüketimi mesurement içerir.
- Merhaba aşağıdaki videoda gösteren bir örnek iş yükü kaynak tüketimi önemli geliştirme: [Azure SQL veritabanı Video, bellek içi OLTP](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).
    - Merhaba blog gönderisi daha fazla ayrıntı için bkz: [bellek içi OLTP Azure SQL veritabanı Blog gönderisine içinde](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

Bellek içi teknolojileri hello Premium katmanı, Premium esnek havuzlarını veritabanları dahil olmak üzere tüm veritabanlarında kullanılabilir.

Merhaba aşağıdaki videoda Azure SQL veritabanında bellek içi teknolojileriyle olası performans artışı açıklanmaktadır. Her zaman gördüğünüz hello performans kazancı hello niteliği hello iş yükü ve veri erişimi deseni hello veritabanının dahil olmak üzere birçok faktöre bağlıdır unutmayın ve benzeri.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

Azure SQL veritabanı bellek içi teknolojileri aşağıdaki hello sahiptir:

- *Bellek içi OLTP* verimliliğini artırır ve işlem için gecikme süresini azaltır. Bellek içi OLTP yararlanan senaryolar şunlardır: yüksek verimlilik işlem ticaret ve oyun, veri alımı olayları veya önbelleğe alma, veri yükü ve geçici bir tablo ve tablo değişkeni senaryoları IOT cihazları gibi işleme.
- *Kümelenmiş columnstore dizinleri* (yukarı too10 saatleri), depolama ayak izini azaltmak ve raporlama ve analiz sorguları performansını. Olgu tabloları ile veri reyonlarını toofit daha fazla veri veritabanınızda kullanmak ve performansı. Ayrıca, işletimsel veritabanı tooarchive geçmiş verileriyle kullanması ve too10 kez yukarı mümkün tooquery daha fazla veri olması.
- *Kümelenmemiş columnstore dizinleri* HTAP Yardım için toogain gerçek zamanlı Öngörüler işletmenize hello işletimsel sorgulama aracılığıyla doğrudan hello gerek toorun pahalı çıkartma, dönüştürme ve yükleme (ETL) işlem veritabanı ve bekleyin doldurulmuş hello veri ambarı toobe için. Kümelenmemiş columnstore dizinleri hello OLTP veritabanlarında hello işlem iş yükü hello etkisini azaltırken analitik sorguları çok hızlı yürütülmesi izin verin.
- Ayrıca, bir columnstore dizini olan bellek için iyileştirilmiş tablo hello birleşimi olabilir. Bu birleşim tooperform çok hızlı hareket işleme, sağlar ve çok*eşzamanlı olarak* çalışma analytics sorgular çok hızlı bir şekilde hello üzerinde aynı veri.

Merhaba SQL Server ürün parçası 2012 ve 2014, bu yana columnstore dizinleri ve bellek içi OLTP sırasıyla olmuştur. Azure SQL Database ve SQL Server paylaşmak hello bellek içi teknolojileri aynı uygulamasıdır. SQL Server'da yayımlanmadan önce ileride, bu teknolojiler için yeni özellikler Azure SQL veritabanı'nda ilk olarak yayımlanmıştır.

Bu konuda, belirli tooAzure SQL veritabanı olan bellek içi OLTP ve columnstore dizinleri yönlerini açıklar ve ayrıca örnekleri içerir:
- Bu teknolojiler hello etkisini depolama ve veri boyutu sınırları görürsünüz.
- Bu teknolojiler hello farklı fiyatlandırma katmanlarına arasında kullanan veritabanları hareketini toomanage hello nasıl görürsünüz.
- Azure SQL veritabanında columnstore dizinleri yanı sıra, bellek içi OLTP hello kullanımını gösteren iki örnek görürsünüz.

Daha fazla bilgi için kaynaklar aşağıdaki hello bakın.

Merhaba teknolojileri hakkında ayrıntılı bilgi:

- [Bellek içi OLTP genel bakış ve kullanım senaryoları](https://msdn.microsoft.com/library/mt774593.aspx) (başvuruları toocustomer örnek olay incelemeleri ve bilgi tooget başlatılan içerir)
- [Bellek içi OLTP için belgeler](http://msdn.microsoft.com/library/dn133186.aspx)
- [Columnstore dizinleri Kılavuzu](https://msdn.microsoft.com/library/gg492088.aspx)
- Karma işlem / (HTAP), olarak da bilinen analitik işleme [işletimsel gerçek zamanlı analiz](https://msdn.microsoft.com/library/dn817827.aspx)

Bellek içi OLTP hızlı öncü: [hızlı başlangıç 1: bellek içi OLTP teknolojileri daha hızlı T-SQL performansı](http://msdn.microsoft.com/library/mt694156.aspx) (başka bir makale toohelp başlamanıza)

Merhaba teknolojileri hakkında ayrıntılı videolar:

- [Azure SQL veritabanında bellek içi OLTP](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (performans gösterimini içeren avantaj ve tooreproduce bu sonuçları kendinize adımları)
- [Bellek içi OLTP videolar: Nedir ve ne zaman/nasıl toouse,](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [Columnstore dizini: Bellek içi Analytics videoların 2016 göz atın.](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a>Depolama ve veri boyutu

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a>Veri boyutu ve depolama cap bellek içi OLTP için

Bellek içi OLTP kullanıcı verilerini depolamak için kullanılan bellek için iyileştirilmiş tablolar içerir. Bu tablolar bellekte gerekli toofit değildir. Merhaba SQL veritabanı hizmetinin bellekte doğrudan yönetmek için biz kullanıcı verileri için bir kota hello kavramı vardır. Başvurulan tooas bu fikirdir *bellek içi OLTP depolama*.

Belirli bir miktarda bellek içi OLTP depolama fiyatlandırma katmanı ve fiyatlandırma katmanı her esnek havuz her desteklenen tek başına veritabanı içerir. Yazma Hello anda, depolama gigabayt her 125 veritabanı işlem birimleri (Dtu'lar) veya esnek veritabanı işlem birimleri (Edtu'lar) alın.

Merhaba [SQL Database hizmet katmanlarına](sql-database-service-tiers.md) makale her desteklenen tek başına veritabanı ve fiyatlandırma katmanı esnek havuz için kullanılabilir olan hello bellek içi OLTP depolama hello resmi listesi içeriyor.

öğe sayısını, bellek içi OLTP depolama cap doğru aşağıdaki hello:

- Bellek için iyileştirilmiş tablolar ve Tablo değişkenlerinin etkin kullanıcı veri satır. Eski satır sürümlerini doğru hello cap sayılmaz unutmayın.
- Bellek için iyileştirilmiş tablolardaki dizinler.
- ALTER TABLE işlemlerin işlemsel yükünü.

Merhaba cap isabet, kota hata iletisi ve artık mümkün tooinsert veya güncelleştirme veri değil. toomitigate bu hata, verileri silmek veya fiyatlandırma katmanı hello veritabanı veya havuzu hello artırın.

Bellek içi OLTP depolama alanı kullanımı izleme ve neredeyse hello cap isabet olduğunda uyarıları yapılandırma hakkında daha fazla bilgi için bkz [monitör bellek içi depolama](sql-database-in-memory-oltp-monitoring.md).

#### <a name="about-elastic-pools"></a>Esnek havuzları hakkında

Esnek havuzları ile bellek içi OLTP depolama hello hello havuzdaki tüm veritabanları arasında paylaşılır. Bu nedenle, bir veritabanında hello kullanım büyük olasılıkla diğer veritabanlarına etkileyebilir. Bu iki Azaltıcı Etkenler şunlardır:

- Bir Max-hello havuzu bir bütün olarak için hello eDTU sayısı daha düşük olan eDTU veritabanları için yapılandırın. Bu maksimum hello havuzundaki toohello eDTU sayısı karşılık gelen toohello boyutu herhangi bir veritabanında hello bellek içi OLTP depolama alanı kullanımı caps.
- 0'dan büyük bir Min-eDTU yapılandırın. Minimum bırakıldığına hello havuzundaki her veritabanı toohello karşılık gelen kullanılabilir bellek içi OLTP depolama hello miktarına sahip en az eDTU yapılandırılmış.

### <a name="data-size-and-storage-for-columnstore-indexes"></a>Veri boyutu ve columnstore dizinleri için depolama

Columnstore dizinleri bellekte gerekli toofit değil. Merhaba dizinleri hello boyutu CAP hello belgelenen hello maksimum genel veritabanı boyutu, yalnızca bu nedenle, hello [SQL Database hizmet katmanlarına](sql-database-service-tiers.md) makalesi.

Kümelenmiş columnstore dizinleri kullandığınızda, sütunlu sıkıştırma hello temel tablo depolaması için kullanılır. Bu sıkıştırma hello depolama ayak izini hello veritabanında daha fazla veri sığabilecek anlamına gelir, verilerinizin kullanıcı önemli ölçüde azaltabilir. Ve hello sıkıştırma daha fazla artırılmasını ile [sütunlu arşiv sıkıştırma](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression). Merhaba veri hello yapısını Hello elde edebilirsiniz sıkıştırma bağlıdır, ancak 10 kez hello sıkıştırma seyrek değil.

Örneğin, 1 terabayt (TB) boyut sınırı olan bir veritabanı varsa ve columnstore dizinleri kullanarak 10 kez hello sıkıştırma elde, kullanıcı verilerini 10 TB toplam hello veritabanında sığabilecek.

Kümelenmemiş columnstore dizinleri kullandığınızda, hello temel tablo hala hello geleneksel rowstore biçiminde depolanır. Bu nedenle, hello depolama tasarrufları kümelenmiş columnstore dizinleriyle kadar büyük değil. Ancak, bir tek columnstore dizini ile geleneksel kümelenmemiş dizin sayısı değiştiriyorsanız hello depolama ayak izini hello tablosu için genel bir tasarruf görebilirsiniz.

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a>Fiyatlandırma katmanı arasındaki bellek içi teknolojileri kullanan veritabanlarını taşıma

Vardır hiçbir zaman uyumsuzlukları ya da diğer sorunlar tooa standart tooPremium gibi fiyatlandırma katmanı, daha yüksek yükselttiğinizde. Merhaba kullanılabilir işlevler ve kaynakları yalnızca artırın.

Ancak, eski sürüme düşürmeyi hello fiyatlandırma katmanı veritabanınızı olumsuz yönde etkileyebilir. Veritabanı bellek içi OLTP nesneler içerdiğinde hello özellikle Premium tooStandard düşürmek olduğunda görünen veya temel etkisidir. (Bunların görünür kalmasını olsa bile) bellek için iyileştirilmiş tablolar ve columnstore dizinleri hello indirgeme sonra kullanılamaz. Merhaba fiyatlandırma katmanı, bir esnek havuzun veya bir veritabanı bellek içi teknolojilerle birlikte, standart veya temel esnek havuz taşıma hello düşürürken ilgili noktaların aynısı geçerlidir.

### <a name="in-memory-oltp"></a>Bellek içi OLTP

*TooBasic/standart eski sürüme düşürmeyi*: bellek içi OLTP hello standart veya temel katmanı veritabanlarında desteklenmez. Ayrıca, olası toomove herhangi bellek içi OLTP nesneleri toohello standart veya temel katmanı olan bir veritabanında değil.

Merhaba veritabanı tooStandard/temel düşürmek önce tüm bellek için iyileştirilmiş tablolar ve tablo türleri yanı sıra, tüm yerel koda derlenmiş T-SQL modülleri kaldırın.

Verilen bir veritabanı bellek içi OLTP destekleyip desteklemediğini programlı şekilde toounderstand yoktur. Transact-SQL sorgusu aşağıdaki hello çalıştırabilirsiniz:

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

Merhaba sorgu döndürürse **1**, bellek içi OLTP bu veritabanında desteklenir.


*Tooa alt Premium katmanı eski sürüme düşürmeyi*: bellek için iyileştirilmiş tablolardaki verileri fiyatlandırma katmanı hello veritabanının hello ile ilişkili olduğundan veya hello esnek Havuzda kullanılabilir hello bellek içi OLTP depolama içinde sığması gerekir. Fiyatlandırma katmanı toolower hello deneyin veya hello veritabanını taşırsanız bir havuza, yeterli kullanılabilir bellek içi OLTP depolama sahip değil, hello işlemi başarısız olur.

### <a name="columnstore-indexes"></a>Columnstore dizinleri

*TooBasic veya standart eski sürüme düşürmeyi*: Columnstore dizinleri yalnızca hello Premium fiyatlandırma katmanı ve değil desteklenir hello standart ya da Basic katmanları. Veritabanı tooStandard veya Basic düşürmek, columnstore dizini kullanılamaz duruma gelir. columnstore dizini Hello sistem korur ancak hiçbir zaman hello dizin yararlanır. Daha sonra geri tooPremium yükseltirseniz, columnstore dizini yeniden işlevden hemen hazır toobe ' dir.

Varsa bir **kümelenmiş** columnstore dizini hello tüm tablo olur kullanılamaz katmanı indirgeme sonra. Bu nedenle tüm bırakma öneririz *kümelenmiş* veritabanınızı hello Premium katmanı aşağıda düşürmek önce columnstore dizinini oluşturur.

*Tooa alt Premium katmanı eski sürüme düşürmeyi*: hello tüm veritabanını hello hello esnek havuzdaki kullanılabilir depolama alanı veya hello en büyük veritabanı boyutu için fiyatlandırma katmanı hello hedef içinde uyuyorsa bu indirgeme başarılı olur. Merhaba columnstore dizinlerinde öğesinden belirli üzerinde etkisi yoktur.


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a>1. Merhaba bellek içi OLTP örneği yükleme

Merhaba, birkaç tıklama ile Merhaba AdventureWorksLT örnek veritabanı oluşturmak [Azure portal](https://portal.azure.com/). Ardından, hello bu bölümdeki adımları nasıl AdventureWorksLT veritabanınızı bellek içi OLTP nesnelerle zenginleştirmek ve performans avantajı göstermek açıklanmaktadır.

Daha fazla simplistic, ancak daha görsel olarak çekici performans gösteri için bellek içi OLTP için bkz:

- Yayın: [içinde-bellek-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)
- Kaynak kodu: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)

#### <a name="installation-steps"></a>Yükleme adımları

1. Merhaba, [Azure portal](https://portal.azure.com/), bir sunucu üzerinde bir Premium veritabanı oluşturun. Set hello **kaynak** toohello AdventureWorksLT örnek veritabanı. Ayrıntılı yönergeler için bkz: [ilk Azure SQL veritabanınızı oluşturma](sql-database-get-started-portal.md).

2. SQL Server Management Studio ile toohello veritabanı bağlantı [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).

3. Kopya hello [bellek içi OLTP Transact-SQL betiği](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour Pano. Merhaba T-SQL betiği hello gerekli bellek içi nesneleri 1. adımda oluşturduğunuz hello AdventureWorksLT örnek veritabanı oluşturur.

4. SSMS Hello T-SQL betiğini yapıştırın ve hello betiğini yürütün. Merhaba `MEMORY_OPTIMIZED = ON` yan tümcesi CREATE TABLE deyimleri önemli. Örneğin:


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a>Hata 40536


Merhaba T-SQL komut dosyasını çalıştırdığınızda 40536 hata alırsanız, bellek içi hello veritabanı destekleyip desteklemediğini T-SQL komut dosyası tooverify aşağıdaki hello çalıştırın:


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


Sonucunu **0** , bellek içi desteklenmez, anlamına gelir ve **1** desteklenip desteklenmediğini gösterir. toodiagnose hello sorun hello veritabanının hello Premium Hizmet katmanını olduğundan emin olun.


#### <a name="about-hello-created-memory-optimized-items"></a>Bellek için iyileştirilmiş öğeleri oluşturulan hello hakkında

**Tablolar**: hello örnek bellek için iyileştirilmiş tablolar aşağıdaki hello içerir:

- SalesLT.Product_inmem
- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem
- Demo.DemoSalesOrderHeaderSeed
- Demo.DemoSalesOrderDetailSeed


Bellek için iyileştirilmiş tablolar hello aracılığıyla inceleyebilirsiniz **Object Explorer** SSMS içinde. Sağ **tabloları** > **filtre** > **filtre ayarları** > **bellek için iyileştirilmiş**. Başlangıç değeri 1'e eşittir.


Veya gibi hello Katalog görünümleri sorgulayabilirsiniz:


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


**Saklı yordam yerel koda derlenmiş**: SalesLT.usp_InsertSalesOrder_inmem Katalog görünümü sorgu ile inceleyebilirsiniz:


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a>Merhaba örnek OLTP iş yükü çalıştırın

iki aşağıdaki hello arasındaki tek fark hello *saklı yordamlar* olan hello ilk yordam hello tabloları bellek için iyileştirilmiş sürümlerini kullanır, hello sırasında ikinci yordam hello normal disk üzerinde tabloları kullanır:

- SalesLT**.** usp_InsertSalesOrder**_inmem**
- SalesLT**.** usp_InsertSalesOrder**_ondisk**


Bu bölümde, nasıl toouse hello kullanışlı olan gördüğünüz **ostress.exe** yardımcı programı tooexecute hello gerilimli düzeylerinde iki saklı yordamlar. Merhaba iki stres çalışır toofinish için gereken süreyi karşılaştırabilirsiniz.


Ostress.exe çalıştırdığınızda, her iki hello aşağıdaki için tasarlanmış parametre değerlerinin geçmesini öneririz:

- Çok sayıda eşzamanlı bağlantı çalıştırmak kullanarak - n100.
- Yüzlerce kez, her bağlantı döngü göre sahip kullanma - r500.


Bununla birlikte, toostart gibi - her şeyin çalıştığını n10 ve - r50 tooensure çok daha küçük değerlerle isteyebilirsiniz.


### <a name="script-for-ostressexe"></a>Ostress.exe için komut dosyası


Bu bölümde bizim ostress.exe komut satırında katıştırılmış hello T-SQL komut dosyası görüntüler. Merhaba betik hello daha önce yüklediğiniz T-SQL komut dosyası tarafından oluşturulan öğeleri kullanır.


Merhaba aşağıdaki komut dosyası bir örnek sipariş beş satır öğelerle bellek için iyileştirilmiş hello aşağıdaki ekler *tabloları*:

- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


toomake hello *_ondisk* sürümü Merhaba ostress.exe için yukarıdaki T-SQL komut dosyası, her iki hello oluşumları değiştirirsiniz *_inmem* ile alt dize *_ondisk*. Bu değişiklik, tabloları ve saklı yordamlar hello adları etkiler.


### <a name="install-rml-utilities-and-ostress"></a>RML yardımcı programları ve ostress yükleyin


İdeal olarak, Azure sanal makine (VM) toorun ostress.exe planlamanız. Oluşturacak bir [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) hello içinde AdventureWorksLT veritabanınızın bulunduğu aynı Azure coğrafi bölge. Ancak bunun yerine dizüstü bilgisayarınızda ostress.exe çalıştırabilirsiniz.


Merhaba VM veya ne olursa olsun, ana bilgisayar seçin, hello yeniden yürütme işaretleme dili (RML) yardımcı programlarını yükleyin. Merhaba yardımcı programları ostress.exe kapsar.

Daha fazla bilgi için bkz.
- Merhaba ostress.exe tartışmada [örnek veritabanı bellek içi OLTP için](http://msdn.microsoft.com/library/mt465764.aspx).
- [Örnek veritabanı için bellek içi OLTP](http://msdn.microsoft.com/library/mt465764.aspx).
- Merhaba [ostress.exe yüklemek için blog](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a>Merhaba çalıştırmak *_inmem* ilk iş yükü stres


Kullanabileceğiniz bir *RML Cmd komut istemi* penceresi toorun bizim ostress.exe komut satırı. Merhaba komut satırı parametreleri için ostress doğrudan:

- 100 bağlantılara eşzamanlı olarak çalıştırın (-n100).
- Her bağlantınız 50 kez Hello T-SQL betiği çalıştırın (-r50).


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


ostress.exe komut satırı önceki toorun hello:


1. Merhaba veritabanı veri içeriği tüm önceki çalışmalarını tarafından eklenen tüm hello veri SSMS, toodelete komutunda aşağıdaki hello çalıştırarak sıfırlama:

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. Ostress.exe komut satırı tooyour Pano önceki hello Hello metnini kopyalayın.

3. Hello yerine `<placeholders>` hello parametreleri -S - U -P -d hello için gerçek değerleri düzeltin.

4. Düzenlenen komut satırında bir RML Cmd penceresinde çalıştırın.


#### <a name="result-is-a-duration"></a>Bir süre oluşur


Ostress.exe bitirdiğinde, kendi çıktı hello RML Cmd penceresinde son satır olarak çalışma süresini hello yazar. Örneğin, daha kısa bir test çalıştırması yaklaşık 1,5 dakika devam:

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a>Sıfırlama, düzenlemek *_ondisk*, sonra yeniden çalıştırın


Merhaba hello sonucundan sonra *_inmem* çalıştırmak, şu adımları hello için hello gerçekleştirmek *_ondisk* çalıştırın:


1. Merhaba veritabanı çalıştırmak hello tarafından önceki eklenmiş tüm hello veri SSMS toodelete komutunda aşağıdaki hello çalıştırarak sıfırlama:
```
EXECUTE Demo.usp_DemoReset;
```

2. Merhaba ostress.exe komut satırı tooreplace tüm Düzenle *_inmem* ile *_ondisk*.

3. Ostress.exe hello için ikinci kez yeniden çalıştırın ve hello süresi sonuç yakalayın.

4. Yeniden (sorumlu bir şekilde ne test verilerinin büyük bir miktarını olabilir silme) hello veritabanı sıfırlayın.


#### <a name="expected-comparison-results"></a>Beklenen Karşılaştırma sonuçları

Bellek içi testlerimizde tarafından geliştirilmiş performans göstermiştir **dokuz kez** simplistic bu iş yükü için ostress ile bir Azure VM üzerinde çalışan hello aynı hello veritabanı olarak Azure bölgesi.

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a>2. Merhaba bellek içi analizi örneği yükleme


Bir columnstore dizini bir geleneksel b-ağacı dizini karşı kullanırken bu bölümde, hello GÇ ve istatistikleri sonuçlarını karşılaştırın.


Bir OLTP iş yükü için gerçek zamanlı analiz almak için genellikle en iyi toouse kümelenmemiş bir columnstore dizini olur. Ayrıntılar için bkz [Columnstore dizinleri açıklanan](http://msdn.microsoft.com/library/gg492088.aspx).



### <a name="prepare-hello-columnstore-analytics-test"></a>Merhaba columnstore analytics test hazırlama


1. Hello Azure portal toocreate hello örnek yeni bir AdventureWorksLT veritabanından kullanın.
 - Bu tam ad kullanın.
 - Tüm Premium Hizmet katmanını seçin.

2. Kopya hello [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour Pano.
 - Merhaba T-SQL betiği hello gerekli bellek içi nesneleri 1. adımda oluşturduğunuz hello AdventureWorksLT örnek veritabanı oluşturur.
 - Merhaba betiği hello Boyut tablosuna ve iki olgu tabloları oluşturur. Merhaba olgu tabloları 3.5 milyon satır her doldurulur.
 - Merhaba betik toocomplete 15 dakika sürebilir.

3. SSMS Hello T-SQL betiğini yapıştırın ve hello betiğini yürütün. Merhaba **COLUMNSTORE** hello anahtar sözcük **CREATE INDEX** açıklamadır önemli olarak:<br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. AdventureWorksLT toocompatibility düzeyi 130 ayarlayın:<br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    Düzey 130 doğrudan ilgili tooIn bellek özellikleri değil. Ancak düzeyi 130 genellikle 120'den daha hızlı sorgu performansı sağlar.


#### <a name="key-tables-and-columnstore-indexes"></a>Anahtar tablolar ve columnstore dizinleri


- dbo. FactResellerSalesXL_CCI sıkıştırma hello en gelişmiş bir kümelenmiş columnstore dizini içeren bir tablo olduğundan *veri* düzeyi.

- dbo. FactResellerSalesXL_PageCompressed yalnızca hello sıkıştırılmış bir eşdeğer normal kümelenmiş dizin içeren bir tablo olduğundan *sayfa* düzeyi.


#### <a name="key-queries-toocompare-hello-columnstore-index"></a>Anahtar sorguları toocompare hello columnstore dizini


Vardır [çalıştırabileceğiniz birkaç T-SQL sorgu türleri](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee performans iyileştirmeleri. Adım 2'de hello T-SQL betiği, sorguları dikkat toothis çifti ücret ödersiniz. Bunlar yalnızca tek bir satırda farklılık gösterir:


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


Merhaba FactResellerSalesXL kümelenmiş columnstore dizini olan\_CCI tablo.

Merhaba aşağıdaki T-SQL komut dosyası Alıntısı istatistikleri GÇ ve her tablonun hello sorgunun süresi yazdırır.


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

Merhaba P2 fiyatlandırma katmanı ile bir veritabanında hello geleneksel dizin ile karşılaştırıldığında hello kümelenmiş columnstore dizini kullanarak bu sorgu için yaklaşık dokuz kez hello performans kazancı bekleyebilirsiniz. P15 ile Merhaba columnstore dizini kullanılarak hakkında 57 kez hello performans kazancı bekleyebilirsiniz.



## <a name="next-steps"></a>Sonraki adımlar

- [1 Hızlı Başlangıç: Daha hızlı bir T-SQL performans için bellek içi OLTP teknolojileri](http://msdn.microsoft.com/library/mt694156.aspx)

- [Mevcut Azure SQL uygulamada kullanmak bellek içi OLTP](sql-database-in-memory-oltp-migration.md)

- [İzleyici bellek içi OLTP depolama](sql-database-in-memory-oltp-monitoring.md) bellek içi OLTP için


## <a name="additional-resources"></a>Ek kaynaklar

#### <a name="deeper-information"></a>Daha ayrıntılı bilgi

- [Bellek içi OLTP SQL veritabanında ile % 70 tarafından DTU düşürürken çekirdek anahtar veritabanının iş yükü nasıl Katlar öğrenin](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [Bellek içi OLTP de Azure SQL veritabanı Blog Gönderisi](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [Bellek içi OLTP hakkında bilgi edinin](http://msdn.microsoft.com/library/dn133186.aspx)

- [Columnstore dizinleri hakkında bilgi edinin](https://msdn.microsoft.com/library/gg492088.aspx)

- [Gerçek zamanlı işletimsel analytics hakkında bilgi edinin](http://msdn.microsoft.com/library/dn817827.aspx)

- Bkz: [yaygın iş yükü desenleri ve geçiş konuları](http://msdn.microsoft.com/library/dn673538.aspx) (burada bellek içi OLTP sık sağlar önemli performans artışları yükünün desenleri açıklayan)

#### <a name="application-design"></a>Uygulama tasarımı

- [Bellek içi OLTP (bellek içi iyileştirme)](http://msdn.microsoft.com/library/dn133186.aspx)

- [Mevcut Azure SQL uygulamada kullanmak bellek içi OLTP](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a>Araçlar

- [Azure portal](https://portal.azure.com/)

- [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)

- [SQL Server Veri Araçları (SSDT)](http://msdn.microsoft.com/library/mt204009.aspx)
