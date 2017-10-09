---
title: "SQL veri ambarı aaaIndexing tablolarda | Microsoft Azure"
description: "Azure SQL Data Warehouse'da dizin tablo ile çalışmaya başlama."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 3e617674-7b62-43ab-9ca2-3f40c41d5a88
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2016
ms.author: shigu;barbkess
ms.openlocfilehash: e614d63c8fb871f2ba388f14576cf9f282d4b818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-tables-in-sql-data-warehouse"></a>SQL veri ambarı tablolarda dizin oluşturma
> [!div class="op_single_selector"]
> * [Genel bakış][Overview]
> * [Veri türleri][Data Types]
> * [Dağıt][Distribute]
> * [Dizin][Index]
> * [Bölüm][Partition]
> * [İstatistikleri][Statistics]
> * [Geçici][Temporary]
> 
> 

SQL Data Warehouse dahil olmak üzere çeşitli dizin oluşturma seçenekleri sunar [kümelenmiş columnstore dizinleri][clustered columnstore indexes], [Kümelenmiş dizinler ve kümelenmemiş dizinler][clustered indexes and nonclustered indexes].  Ayrıca, aynı zamanda herhangi bir dizin seçeneği olarak da bilinen sağlar [yığın][heap].  Bu makalede her dizin türünü hello yararları kapsayan yanı sıra toogetting hello dizinlerinizi dışında çoğu performans ipuçları. Bkz: [table söz dizimi oluşturma] [ create table syntax] konusunda daha fazla ayrıntı için toocreate SQL Data warehouse'da bir tablo.

## <a name="clustered-columnstore-indexes"></a>Kümelenmiş columnstore dizinleri
Bir tablo üzerinde hiçbir dizin seçeneği belirtildiğinde varsayılan olarak, SQL Data Warehouse kümelenmiş columnstore dizini oluşturur. Kümelenmiş columnstore tabloları hem hello en yüksek düzeyde veri sıkıştırma ve bunun yanı sıra hello en iyi genel sorgu performansı sunar.  Kümelenmiş columnstore tabloları kümelenmiş dizin veya yığın tabloları genellikle aşar ve genellikle hello en büyük tablolar için bir seçimdir.  Nasıl emin değilseniz bu nedenlerle, kümelenmiş columnstore hello en iyi yeri toostart olduğunda tooindex tablonuz.  

toocreate bir kümelenmiş columnstore tablo yalnızca hello WITH yan tümcesinde kümelenmiş COLUMNSTORE dizini belirtin veya hello WITH yan tümcesi devre dışı bırakın:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );
```

Burada kümelenmiş columnstore iyi bir seçenek olmayabilir birkaç senaryo vardır:

* Columnstore tabloları, varchar(max), nvarchar(max) ve varbinary(max) desteklemez.  Yığın veya kümelenmiş dizin yerine göz önünde bulundurun.
* Columnstore tablolar için geçici verileri daha az verimli olabilir.  Yığın ve hatta belki de geçici tabloları göz önünde bulundurun.
* 100 milyondan az satır içeren küçük tabloları silin.  Yığın tabloları göz önünde bulundurun.

## <a name="heap-tables"></a>Yığın tabloları
Verileri SQL Data Warehouse geçici olarak giriş, öbek tablosunu kullanarak genel işlem daha hızlı hello yapacağı bulabilirsiniz.  Bu yükleri tooheaps tooindex tabloları hızlıdır ve bazı durumlarda hello sonraki okuma önbelleğinden yapılabilir kaynaklanır.  Verileri yalnızca toostage hello tablo tooheap yüklenirken daha fazla dönüşümleri çalıştırmadan önce hello veri tooa yüklemekten daha hızlı olacak, yüklüyorsanız columnstore tablo kümelenmiş. Ayrıca, veri tooa yüklenirken [geçici tablo] [ Temporary] de çok tablo toopermanent depolama yüklenirken daha hızlı yükler.  

100 milyondan az satır küçük arama tabloları için genellikle yığın tabloları anlamlı.  100 milyondan fazla satır olduğunda küme columnstore tabloları tooachieve en iyi sıkıştırma başlayın.

toocreate bir öbek tablo hello WITH yan tümcesinde yalnızca yığın belirtin:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( HEAP );
```

## <a name="clustered-and-nonclustered-indexes"></a>Kümelenmiş ve kümelenmemiş dizinleri
Tek bir satır hızla alınan toobe gerektiğinde Kümelenmiş dizinler kümelenmiş columnstore tabloları daha iyi performans gösterir.  Tek veya çok az sayıda satır arama aşırı hız gerekli tooperformance olduğu sorgular için küme dizini ya da ikincil kümelenmemiş dizin göz önünde bulundurun.  Merhaba dezavantajı toousing kümelenmiş bir dizin hello kümelenmiş dizin sütunu üzerinde yüksek oranda seçmeli bir filtre kullanan sorgular faydalanırsınız ' dir.  kümelenmemiş bir dizin olabilir diğer sütunlardaki tooimprove filtre tooother sütunları eklenir.  Ancak, tooa tablo eklenen her dizin alanı ve zaman tooloads işleme ekleyeceksiniz.

toocreate bir kümelenmiş dizin tablo hello WITH yan tümcesinde yalnızca kümelenmiş dizini belirtin:

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED INDEX (id) );
```

bir tabloda kümelenmemiş bir dizin tooadd yalnızca sözdizimi aşağıdaki hello kullanın:

```SQL
CREATE INDEX zipCodeIndex ON t1 (zipCode);
```

## <a name="optimizing-clustered-columnstore-indexes"></a>Kümelenmiş columnstore dizinleri en iyi duruma getirme
Kümelenmiş columnstore tabloları veri kesimler halinde düzenlenir.  Yüksek segment kalite sahip bir columnstore tabloda kritik tooachieving en iyi sorgu performansını istenir.  Segment kalite hello sıkıştırılmış satır grubu satır sayısı tarafından ölçülebilir.  En az 100 sıkıştırılmış satır başına satır grup ve performans olan hello başına satır sayısı satır grubu yaklaşım 1.048.576 satır, satır grubu içerebilir çoğu satırları hello olarak geçirmesine K bulunduğu segment kalite en uygundur.

Görünüm aşağıda Hello oluşturulan ve kullanılan sistem toocompute hello satır başına ortalama satır grup ve tüm iyinin küme columnstore dizinleri belirleyin.  Bu görünüm Hello son sütunda kullanılan toorebuild olabilen SQL deyimini dizinlerinizi oluşturur.

```sql
CREATE VIEW dbo.vColumnstoreDensity
AS
SELECT
        GETDATE()                                                               AS [execution_date]
,       DB_Name()                                                               AS [database_name]
,       s.name                                                                  AS [schema_name]
,       t.name                                                                  AS [table_name]
,    COUNT(DISTINCT rg.[partition_number])                    AS [table_partition_count]
,       SUM(rg.[total_rows])                                                    AS [row_count_total]
,       SUM(rg.[total_rows])/COUNT(DISTINCT rg.[distribution_id])               AS [row_count_per_distribution_MAX]
,    CEILING    ((SUM(rg.[total_rows])*1.0/COUNT(DISTINCT rg.[distribution_id]))/1048576) AS [rowgroup_per_distribution_MAX]
,       SUM(CASE WHEN rg.[State] = 0 THEN 1                   ELSE 0    END)    AS [INVISIBLE_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE 0    END)    AS [INVISIBLE_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 1 THEN 1                   ELSE 0    END)    AS [OPEN_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE 0    END)    AS [OPEN_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 2 THEN 1                   ELSE 0    END)    AS [CLOSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE 0    END)    AS [CLOSED_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 3 THEN 1                   ELSE 0    END)    AS [COMPRESSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE 0    END)    AS [COMPRESSED_rowgroup_rows]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[deleted_rows]   ELSE 0    END)    AS [COMPRESSED_rowgroup_rows_DELETED]
,       MIN(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_AVG]
,       'ALTER INDEX ALL ON ' + s.name + '.' + t.NAME + ' REBUILD;'             AS [Rebuild_Index_SQL]
FROM    sys.[pdw_nodes_column_store_row_groups] rg
JOIN    sys.[pdw_nodes_tables] nt                   ON  rg.[object_id]          = nt.[object_id]
                                                    AND rg.[pdw_node_id]        = nt.[pdw_node_id]
                                                    AND rg.[distribution_id]    = nt.[distribution_id]
JOIN    sys.[pdw_table_mappings] mp                 ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[tables] t                              ON  mp.[object_id]          = t.[object_id]
JOIN    sys.[schemas] s                             ON t.[schema_id]            = s.[schema_id]
GROUP BY
        s.[name]
,       t.[name]
;
```

Merhaba görünüm oluşturduğunuza göre bu sorgu tooidentify tablolar satır grupları 100 K satırları değerinden ile çalıştırın.  Elbette, daha fazla en iyi segment kalitesini arıyorsanız tooincrease hello Eşiği 100 k isteyebilirsiniz. 

```sql
SELECT    *
FROM    [dbo].[vColumnstoreDensity]
WHERE    COMPRESSED_rowgroup_rows_AVG < 100000
        OR INVISIBLE_rowgroup_rows_AVG < 100000
```

Merhaba sorgu çalıştırdıktan sonra hello veri toolook başlamak ve sonuçlarınızı analiz edin. Bu tabloda, satır grubu analizi için hangi toolook açıklanmaktadır.

| Sütun | Nasıl toouse bu verileri |
| --- | --- |
| [table_partition_count] |Merhaba tablo bölümlenmişse toosee daha yüksek açık satır grubu sayılarını beklediğiniz. Her bölüm hello dağıtımındaki teorik olarak kendisiyle ilişkili bir açık satır grubu olabilir. Çözümleme öğeli. Bölümlenmiş küçük bir tablo, bu sıkıştırma arttıkça değerlerinin bölümleme hello kaldırarak iyileştirilmiş. |
| [row_count_total] |Merhaba tablonun toplam satır sayısı. Örneğin, bu değer toocalculate yüzde satır sıkıştırılmış hello durumda kullanabilirsiniz. |
| [row_count_per_distribution_MAX] |Tüm satırları olacak şekilde eşit dağıtılır, bu değer hello hedef dağıtım başına satır sayısı olacaktır. Merhaba compressed_rowgroup_count bu değerle karşılaştırın. |
| [COMPRESSED_rowgroup_rows] |Columnstore biçiminde hello tablosu için satırların toplam sayısı. |
| [COMPRESSED_rowgroup_rows_AVG] |Hello ortalama satır sayısını önemli ölçüde ise satır grubu için satır değerinden hello maksimum # CTAS kullanarak göz önünde bulundurun veya ALTER INDEX REBUILD toorecompress veri hello |
| [COMPRESSED_rowgroup_count] |Satır gruplarını columnstore biçiminde sayısı. Bu sayı ilişkisi toohello tabloda çok yüksekse, hello columnstore yoğunluğu düşük bir göstergesidir. |
| [COMPRESSED_rowgroup_rows_DELETED] |Satır columnstore biçiminde mantıksal olarak silinir. Merhaba numarası yüksek göreli tootable boyutu ise, hello bölümünü yeniden oluşturmak veya bu bunları fiziksel olarak kaldırır hello dizinini yeniden oluşturmayı düşünün. |
| [COMPRESSED_rowgroup_rows_MIN] |Bu hello ortalama ve en fazla sütun toounderstand hello değerleri aralığı ile birlikte, columnstore hello satır grupları için kullanın. En iyi duruma getirme hello veri yükleme kullanılabilir hello yükleme eşiği (hizalı bölüm dağıtım başına 102,400) üzerinden düşük bir sayı önerir |
| [COMPRESSED_rowgroup_rows_MAX] |Yukarıdaki gibi |
| [OPEN_rowgroup_count] |Açık satır grupları normal. Bir tablo dağıtım (60) başına bir açık satır grubu makul beklenir. Aşırı numaraları veri bölümler yükleme önerin. Çift onay hello stratejisi toomake ses olduğundan emin bölümlendirme |
| [OPEN_rowgroup_rows] |Her satır grubu 1.048.576 satır en fazla olabilir. Bu değer toosee nasıl tam kullanmak hello açık satır grupları olan şu anda |
| [OPEN_rowgroup_rows_MIN] |Gruplar'ı açın, veri akışla yükleniyor hello tabloya ya da bu satır grubu kalan satırlara üzerinden geçmiş önceki yük hello olduğunu gösterir. Kullanım hello MIN, MAX, AVG sütunları toosee ne kadar veri açık satır grupları sat. Küçük tablolar için tüm hello verilerin % 100 olabilir! Bu durumda ALTER INDEX REBUILD tooforce veri toocolumnstore hello. |
| [OPEN_rowgroup_rows_MAX] |Yukarıdaki gibi |
| [OPEN_rowgroup_rows_AVG] |Yukarıdaki gibi |
| [CLOSED_rowgroup_rows] |Kapalı hello satır grubu satırları sağlamlık denetimi olarak arayın. |
| [CLOSED_rowgroup_count] |Kapalı satır grupları Hello sayısı herhangi hiç görülüyorsa düşük olmalıdır. Kapalı satır grupları hello ALTER INDEX kullanarak dönüştürülen toocompressed rowg roups olabilir... Komut yeniden düzenleme. Ancak, bu normalde gerekli değildir. Merhaba arka plan "tanımlama grubu taşıyıcısı" işlemi tarafından otomatik olarak dönüştürülen toocolumnstore satır grupları kapalı gruplarıdır. |
| [CLOSED_rowgroup_rows_MIN] |Kapalı satır grupları çok yüksek dolgu oranı olması gerekir. Merhaba dolgu oranı kapalı satır grubu için düşükse çözümlemeler hello columnstore gereklidir. |
| [CLOSED_rowgroup_rows_MAX] |Yukarıdaki gibi |
| [CLOSED_rowgroup_rows_AVG] |Yukarıdaki gibi |
| [Rebuild_Index_SQL] |SQL toorebuild columnstore dizini bir tablo için |

## <a name="causes-of-poor-columnstore-index-quality"></a>Zayıf columnstore dizini kalite nedenleri
Zayıf segment kalitesiyle tabloları tanımladıysanız tooidentify hello kök nedeni isteyeceksiniz.  Bazı diğer yaygın nedenlerini zayıf segment quaility aşağıda verilmiştir:

1. Dizin yapılandırıldığında bellek baskısı
2. Yüksek hacimli DML işlemleri
3. Küçük veya yük işlemleri trickle
4. Çok fazla bölümleri

Bu etkenler bir columnstore dizini toohave önemli ölçüde daha az satır grubu başına en iyi 1 milyon satır hello neden olabilir.  Ayrıca satırları toogo toohello delta satır grubu yerine bir sıkıştırılmış satır grubuna neden olabilir. 

### <a name="memory-pressure-when-index-was-built"></a>Dizin yapılandırıldığında bellek baskısı
Merhaba satır doğrudan ilgili toohello genişliğini olan ve kullanılabilir tooprocess satır grubu hello bellek miktarını hello sıkıştırılmış satır grubu başına satır Hello sayısıdır.  Bellek baskısı altında toocolumnstore tablolar satır yazılırken columnstore segment kalite düşebilir.  Bu nedenle, tooyour columnstore dizini tabloları tooas mümkün olduğunca fazla bellek erişim yazma toogive hello oturumu hello en iyi yoldur.  Bellek ve eşzamanlılık arasında bir denge olduğundan hello bellek ayırma hello verileri DWU hello miktarı, tablodaki her satır, bağımlı tooyour sistem tahsis ve eşzamanlılık hello miktarını yuvası sağ hello yönergeler toohello verebilirsiniz Veri tooyour tablosu yazma oturumu.  En iyi uygulama, DW1000 kullanıyorsanız ve yukarıdaki DW400 tooDW600 ve mediumrc kullanıyorsanız, DW300 kullanıyorsanız xlargerc veya daha az, largerc başlangıç öneririz.

### <a name="high-volume-of-dml-operations"></a>Yüksek hacimli DML işlemleri
Güncelleştirme ve satırları silme DML işlemleri yüksek hacimli Etkisizliği hello columnstore ortaya çıkarabilir. Bir satır gruptaki hello satırlar Hello çoğunluğu değiştirildiğinde durumlarda özellikle geçerlidir.

* Sıkıştırılmış satır grubundan yalnızca mantıksal olarak bir satırın silinmesi hello satır silindi olarak işaretler. Merhaba bölüm veya tablo yapılana kadar hello satır hello sıkıştırılmış satır grubunda kalır.
* Satır ekleme, bir delta satır grubu adlı hello satır tootooan iç rowstore tablo ekler. Merhaba delta satır grubu dolu olduğunda ve kapatıldı olarak işaretlenen kadar eklenen hello satır dönüştürülmüş toocolumnstore değildir. Merhaba maksimum kapasite 1.048.576 satır ulaştığınızda satır grupları kapatılır. 
* Columnstore biçiminde bir satırı güncelleştirmek, mantıksal bir silme ve ardından bir ekleme işlenir. eklenen hello satır hello delta deposunda depolanabilir.

Toplu güncelleştirme ve toohello columnstore biçimlendirmek doğrudan hizalanmış dağıtım yazılır bölüm başına 102,400 satır hello toplu eşiğini aşan işlemlere ekleyin. Ancak, bir bile dağıtım varsayıldığında, bu toooccur için tek bir işlemde birden fazla 6.144 milyon satır değiştirme toobe'nı gerekir. Belli bir bölüm için satır sayısını Hello dağıtım hizalı hello satırları toohello delta deposu geçer ve yeterli satırları eklenen veya değiştirilen tooclose hello satır grubunun veya hello dizini yeniden kadar orada kalacak değerinden 102,400 ise.

### <a name="small-or-trickle-load-operations"></a>Küçük veya yük işlemleri trickle
Küçük SQL Data Warehouse akışına bazen bilinir olduğunu yükleri trickle olarak yükler. Bunlar genellikle hello sistem tarafından alınan bir veri yakın sabit akışı temsil eder. Ancak, bu akış yakın olduğundan satır sürekli hello birim özellikle büyük değil. Daha sık fazla hello veri önemli ölçüde için doğrudan yük toocolumnstore biçimi gerekli hello eşiğin altında değil.

Bu durumlarda, bu genellikle daha iyi tooland hello veri ilk Azure blob depolama alanına ve önceki tooloading birikmesini çalışmasına izin. Bu teknik genellikle olarak bilinen *mikro toplu işleme*.

### <a name="too-many-partitions"></a>Çok fazla bölümleri
Başka bir şey tooconsider kümelenmiş columnstore tabloları üzerinde bölümleme hello etkisi olur.  Bölümleme önce SQL veri ambarı zaten verilerinizi 60 veritabanlarına olarak böler.  Bölümlendirme, verilerinizi daha fazla böler.  Verilerinizi bölüm sonra tooconsider istersiniz, **her** bölüm toohave en az 1 milyon satır toobenefit kümelenmiş columnstore dizinindeki gerekir.  Tablonuz 100 bölümlere bölüm sonra tablonuz toohave en az 6 milyon satır toobenefit kümelenmiş columnstore dizinindeki gerekir (60 dağıtımları * 100 bölümleri * 1 milyon satır). 100 bölüm tablonuz 6 milyon satır yoksa bölümleri hello sayısını azaltın veya yığın tablo kullanmayı düşünün.

Tablolarınızı bazı verilerle birlikte yüklenmiş sonra hello adımları tooidentify aşağıda izleyin ve tabloları iyinin küme columnstore dizinleri ile yeniden oluşturun.

## <a name="rebuilding-indexes-tooimprove-segment-quality"></a>Dizinleri tooimprove segment kalite yeniden oluşturma
### <a name="step-1-identify-or-create-user-which-uses-hello-right-resource-class"></a>1. adım: Tanımlamak veya hello doğru kaynak sınıfı kullanan kullanıcı oluştur
Tooimmediately segment kalitesini geliştirmek bir hızlı toorebuild hello dizin yoludur.  Merhaba SQL görünümü yukarıda hello tarafından döndürülen kullanılan toorebuild olabilen bir ALTER INDEX REBUILD deyimi dizinleri döndürür.  Dizinleri yeniden oluştururken dizininizi oluşturacak yeterli bellek toohello oturum ayırdığınızdan emin olun.  toodo Bu tablo toohello önerilen minimum izinleri toorebuild hello dizini olan bir kullanıcı bu, artış hello kaynak sınıfı.  bir kullanıcı hello sistemde oluşturmadıysanız toodo için öncelikle gerekir hello kaynak sınıfı hello veritabanı sahibi kullanıcının değiştirilemez.  DW1000 kullanıyorsanız ve yukarıdaki DW400 tooDW600 ve mediumrc kullanıyorsanız, öneririz hello xlargerc DW300 kullanıyorsanız veya daha az, largerc gereksinimdir.

Nasıl bir örneği aşağıdadır tooallocate kendi kaynak sınıfı artırarak daha fazla bellek tooa kullanıcı.  Kaynak sınıfları ve hello nasıl toocreate yeni bir kullanıcı bulunabilir hakkında daha fazla bilgi için [eşzamanlılık ve iş yükü yönetimi] [ Concurrency] makalesi.

```sql
EXEC sp_addrolemember 'xlargerc', 'LoadUser'
```

### <a name="step-2-rebuild-clustered-columnstore-indexes-with-higher-resource-class-user"></a>2. adım: yüksek kaynak sınıfı kullanıcıyla kümelenmiş columnstore dizinleri yeniden oluştur
Şimdi daha yüksek bir kaynak sınıfı kullanarak ve hello ALTER INDEX deyimlerini hello kullanıcı adım 1 (örneğin LoadUser) olarak oturum açın.  Bu kullanıcı hello dizin burada yeniden oluşturuluyorsa ALTER izni toohello tabloları olduğundan emin olun.  Bu örnekler toorebuild hello nasıl tüm columnstore dizini veya nasıl toorebuild tek bir bölüm. Tek bir bölüm aynı anda daha pratik toorebuild dizinleri olduğu büyük tablolar üzerinde.

Alternatif olarak, hello dizinini yeniden oluşturmayı yerine hello tablo tooa tablo kullanarak yeni kopyaladığınız [CTAS][CTAS].  Hangi yolla en iyisidir? Büyük veri, birimleri için [CTAS] [ CTAS] genellikle hızlıdır [ALTER INDEX][ALTER INDEX]. Veri, daha küçük birimler için [ALTER INDEX] [ ALTER INDEX] daha kolay toouse ise ve tooswap hello tablo çıkışı gerektiren olmaz.  Bkz: **CTAS ve bölüm değiştirme dizinleri yeniden oluşturma** aşağıda nasıl toorebuild ile CTAS dizinler hakkında daha fazla bilgi.

```sql
-- Rebuild hello entire clustered index
ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD
```

```sql
-- Rebuild a single partition
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5
```

```sql
-- Rebuild a single partition with archival compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE)
```

```sql
-- Rebuild a single partition with columnstore compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE)
```

SQL Data warehouse'da bir dizini yeniden oluşturma çevrimdışı bir işlemdir.  ALTER INDEX yeniden bölümünde hello dizinleri yeniden oluşturma hakkında daha fazla bilgi için bkz: [Columnstore dizinleri birleştirme] [ Columnstore Indexes Defragmentation] ve hello söz dizimi konusuna [ALTER INDEX] [ALTER INDEX].

### <a name="step-3-verify-clustered-columnstore-segment-quality-has-improved"></a>3. adım: Kümelenmiş columnstore segment kalite geliştirilmiştir doğrulayın
Tablo ile düşük tanımlanan hello sorguyu yeniden çalıştır kalite segment ve segment kalite geliştirilmiştir doğrulayın.  Segment kalitesini artırmak değil, tablonuz hello satır çok geniş olabilir.  Dizinleri yeniden oluştururken daha yüksek kaynak sınıfı veya DWU kullanmayı düşünün.

## <a name="rebuilding-indexes-with-ctas-and-partition-switching"></a>CTAS ve bölüm değiştirme dizinleri yeniden oluşturma
Bu örnekte [CTAS] [ CTAS] ve bölüm toorebuild bir tabloda bölüm değiştirme. 

```sql
-- Step 1: Select hello partition of data and write it out tooa new table using CTAS
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

-- Step 2: Create a SWITCH out table
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE   1=2 -- Note this table will be empty

-- Step 3: Switch OUT hello data 
ALTER TABLE [dbo].[FactInternetSales] SWITCH PARTITION 2 too [dbo].[FactInternetSales_20000101] PARTITION 2;

-- Step 4: Switch IN hello rebuilt data
ALTER TABLE [dbo].[FactInternetSales_20000101_20010101] SWITCH PARTITION 2 too [dbo].[FactInternetSales] PARTITION 2;
```

Kullanarak bölümleri yeniden oluşturma hakkında daha fazla ayrıntı için `CTAS`, hello bkz [bölüm] [ Partition] makalesi.

## <a name="next-steps"></a>Sonraki adımlar
toolearn daha hello makalelere bakın üzerinde [tablo genel bakışı][Overview], [tablo veri türleri][Data Types], [bir tablodağıtma] [ Distribute], [Bir tablo bölümleme][Partition], [tablo istatistikleri koruma] [ Statistics] ve [ Geçici tablolara][Temporary].  en iyi uygulamalar hakkında daha fazla toolearn bkz [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[ALTER INDEX]: https://msdn.microsoft.com/library/ms188388.aspx
[heap]: https://msdn.microsoft.com/library/hh213609.aspx
[clustered indexes and nonclustered indexes]: https://msdn.microsoft.com/library/ms190457.aspx
[create table syntax]: https://msdn.microsoft.com/library/mt203953.aspx
[Columnstore Indexes Defragmentation]: https://msdn.microsoft.com/library/dn935013.aspx#Anchor_1
[clustered columnstore indexes]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
