---
title: Azure SQL aaaImprove columnstore dizini performans | Microsoft Docs
description: "Bellek gereksinimlerini azaltın veya hello kullanılabilir bellek toomaximize hello her satır grubu kimliğinde bir columnstore dizini sıkıştırır satır sayısını artırın."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 6/2/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 2c5a68435aa200236a2dc8538aa4638b52a59093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a>Satır grubu kimliğinde kalitesi columnstore için en üst düzeye çıkarma

Satır grubu kimliğinde kalite hello bir satır grubu kimliğinde satır sayısı tarafından belirlenir. Bellek gereksinimlerini azaltın veya hello kullanılabilir bellek toomaximize hello her satır grubu kimliğinde bir columnstore dizini sıkıştırır satır sayısını artırın.  Bu yöntemleri tooimprove sıkıştırma oranları ve sorgu performansı columnstore dizinleri için kullanın.

## <a name="why-hello-rowgroup-size-matters"></a>Merhaba satır grubu kimliğinde boyutu neden önemlidir?
Tek tek rowgroups sütun kesimleri tarayarak bir tabloda bir columnstore dizini tarar olduğundan, her satır grubu kimliğinde satır hello sayısı en üst düzeye çıkarma sorgu performansını geliştirir. Çok sayıda satır RowGroups sahip olduğunuzda, veri sıkıştırma daha az veri tooread diskten olmadığı anlamına gelir artırır.

Rowgroups hakkında daha fazla bilgi için bkz: [Columnstore dizinleri Kılavuzu](https://msdn.microsoft.com/library/gg492088.aspx).

## <a name="target-size-for-rowgroups"></a>Rowgroups ilişkin hedef boyutu
En iyi sorgu performansını hello hedef toomaximize hello satır grubu kimliğinde bir columnstore dizininde başına satır sayısıdır. Bir satır grubu kimliğinde 1.048.576 satır en olabilir. Merhaba en fazla satır grubu başına satır sayısı, sorunsuz toonot var. Columnstore dizinleri RowGroups 100. 000'en az satır olduğunda iyi performans elde etmek.

## <a name="rowgroups-can-get-trimmed-during-compression"></a>Sıkıştırma sırasında RowGroups kırpılmış

Bir toplu yükleme veya columnstore dizini yeniden oluşturma sırasında bazen hiç tüm her satır grubu için belirtilen satır hello yeterli bellek kullanılabilir toocompress. Bellek baskısı olduğunda sıkıştırma hello columnstore içine başarılı şekilde columnstore dizinleri hello satır grubu kimliğinde boyutları kesim. 

Her satır grubu kimliğinde toocompress 10. 000'en az satırlara bellek yetersiz olduğunda, SQL Data Warehouse bir hata oluşturur.

Toplu yükleme hakkında daha fazla bilgi için bkz: [toplu yükleme kümelenmiş columnstore dizinine](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).

## <a name="how-toomonitor-rowgroup-quality"></a>Nasıl toomonitor satır grubu kimliğinde kalitesi

Kırpma rowgroups ve hello nedeni satır sayısı gibi yararlı bilgileri var. kırpma olmadığını gösteren bir DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) yoktur. Görünüm kullanışlı şekilde tooquery olarak aşağıdaki hello satır grubu kimliğinde kırpma üzerinde bu DMV tooget bilgileri oluşturabilirsiniz.

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[distribution_id]    = nt.[distribution_id]                                          
)
select *
from cte;
```

Merhaba trim_reason_desc söyler hello satır grubu kimliğinde aynı olup olmadığını (trim_reason_desc = NO_TRIM hiçbir kırpma vardı ve satır grubu en iyi kalitesini olduğu anlamına gelir). Merhaba kırpma şunlardan hello satır grubu kimliğinde erken kırpılacağını belirtin:
- BULKLOAD: hello gelen toplu satır hello yük için 1 milyondan az satır varken bu kırpma neden kullanılır. Merhaba altyapısı vardır (olarak karşılıklı tooinserting hello delta deposuna) eklenmekte 100.000 satırları büyük ancak kümeleri kırpma neden tooBULKLOAD hello sıkıştırılmış satır grupları oluşturur. Bu senaryoda, daha fazla satır, toplu iş yükü penceresi tooaccumulate artırmayı düşünün. Ayrıca, satır gruplarından bölüm sınırları yayılamaz gibi çok parçalı değil, bölümleme düzeni tooensure yeniden.
- MEMORY_LIMITATION: toocreate satır grupları 1 milyon satır, belirli bir çalışma bellek miktarı ile Merhaba altyapısı tarafından gereklidir. Oturum yüklenirken hello kullanılabilir belleğin hello bellek çalışma gerekenden daha az olduğunda, satır gruplarından erken kırpılır. Aşağıdaki bölümlerde hello nasıl tooestimate bellek gerekli ve daha fazla bellek açıklanmaktadır.
- DICTIONARY_SIZE: Kırpma bu nedenle, geniş ve/veya yüksek nicelik dizeleri içeren en az bir dize sütunu olduğundan satır grubu kimliğinde kırpma oluştuğunu gösterir. Merhaba sözlük MB bellek ve hello satır grubu bu sınıra ulaşıldığında sıkıştırılmış sınırlı too16 boyutudur. Bu durumla karşılaşırsanız hello sorunlu sütun ayrı bir tabloya izole etmeyi düşünün.

## <a name="how-tooestimate-memory-requirements"></a>Nasıl tooestimate bellek gereksinimleri

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

Merhaba maksimum gerekli bellek toocompress bir satır grubu kimliğinde yaklaşık olarak şöyledir

- 72 MB +
- \#Satır \* \#sütunları \* 8 bayt +
- \#Satır \* \#kısa dize sütunlarındaki \* 32 bayt +
- \#uzun dize sütunlarındaki \* sıkıştırma sözlüğü için 16 MB

Burada kısa dize sütunlarındaki dize veri türlerini kullanın < = 32 bayt ve > 32 bayt dizesi veri türlerini uzun dize sütunlarındaki kullanın.

Uzun dizeleri metin sıkıştırma için tasarlanmış bir sıkıştırma yöntemi ile sıkıştırılır. Bu bir sıkıştırma yöntemi kullanan bir *sözlük* toostore metin kalıplarını. bir sözlük Hello en büyük boyutu 16 MB'tır. Merhaba satır grubu kimliğinde her uzun bir dize sütunu için yalnızca bir sözlük yoktur.

Video columnstore bellek gereksinimlerini kapsamlı bir açıklama için bkz [Azure SQL Data Warehouse ölçeklendirme: yapılandırma ve Kılavuzu](https://myignite.microsoft.com/videos/14822).

## <a name="ways-tooreduce-memory-requirements"></a>Yolları tooreduce bellek gereksinimleri

Columnstore dizinleri rowgroups sıkıştırma teknikleri tooreduce hello bellek gereksinimleri aşağıdaki hello kullanın.

### <a name="use-fewer-columns"></a>Daha az sütun kullanın
Mümkünse, daha az sütun içeren hello tablo tasarlayın. Bir satır grubu kimliğinde hello columnstore sıkıştırılmış zaman hello columnstore dizini her bir sütun segmenti ayrı olarak sıkıştırır. Bu nedenle toocompress bir satır grubu kimliğinde hello sütunları artar artırın bellek gereksinimlerini hello.


### <a name="use-fewer-string-columns"></a>Daha az dize sütun kullanın
Dize veri türleri sütunlarının daha fazla bellek sayısal ve tarih veri türü gerektirir. tooreduce bellek gereksinimleri, dize sütunlarındaki olgu tablolarından kaldırarak ve daha küçük boyut tabloları koyma göz önünde bulundurun.

Dize sıkıştırma için ek bellek gereksinimleri:

- Değer başına 32 ek bayt too32 karakter dizesi veri türlerini gerektirebilir.
- Birden fazla 32 karakter dizesi veri türleriyle sözlük yöntemleri kullanarak sıkıştırılır.  Her sütunda hello satır grubu kimliğinde tooan ek 16 MB toobuild hello sözlüğünü gerektirebilir.

### <a name="avoid-over-partitioning"></a>Aşırı bölümleme kaçının

Columnstore dizinleri bölüm başına bir veya daha fazla rowgroups oluşturun. SQL veri ambarı'nda hello bölüm sayısı çünkü hello verileri dağıtılır ve her dağıtım bölümlenmiş hızlı bir şekilde artar. Merhaba tablonun çok fazla bölümleri varsa yeterli satırları toofill hello rowgroups olmayabilir. Satır Hello eksikliği sıkıştırma sırasında bellek baskısı oluşturmaz, ancak hello en iyi columnstore sorgu performansı elde etmeyin toorowgroups yol açar.

Başka bir nedenle tooavoid aşırı bölümleme bölümlenmiş bir tablodaki columnstore dizininin içine satırları yükleme için ek bellek olmasıdır. Bir yükleme sırasında her bölüm sıkıştırılmış yeterli satırları toobe olana kadar bellekte tutulan hello gelen satırlarını, birçok bölüm alabilir. Çok fazla bölümlemeye sahip olmak için ek bellek baskısı oluşturur.

### <a name="simplify-hello-load-query"></a>Merhaba yük sorguyu basitleştirin

Merhaba veritabanı hello bellek ataması hello sorgudaki tüm hello işleçleri arasında bir sorgu için paylaşır. Bir yük sorgu karmaşık sıralar ve birleşimler olduğunda, sıkıştırma hello bellek azalır.

Merhaba yük sorgu toofocus'hello sorgu yüklenirken üzerinde yalnızca tasarlayın. Merhaba veri toorun dönüşümler ihtiyacınız varsa, bunları hello yük sorgudan ayrı çalıştırın. Örneğin, bir yığın tablosunda aşama hello veri hello dönüşümleri çalıştırın ve hazırlama tablosuna hello columnstore dizinine hello yük. Ayrıca hello verileri ilk yüklemek ve hello MPP sistem tootransform hello verileri kullanın.

### <a name="adjust-maxdop"></a>MAXDOP Ayarla

Dağıtım birden çok CPU çekirdeği bulunmadığında her dağıtım rowgroups hello columnstore paralel içine sıkıştırır. Merhaba paralellik toomemory baskısı ve satır grubu kimliğinde kırpma neden olabilecek ek bellek kaynaklarının gerektirir.

tooreduce bellek baskısı, her dağıtım içinde seri modunda hello MAXDOP sorgu ipucu tooforce hello yükleme işlemi toorun kullanabilirsiniz.

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a>Yolları tooallocate daha fazla bellek

DWU boyutu ve hello kullanıcı kaynak sınıfı birlikte belirlemek için bir kullanıcı sorgu ne kadar kullanılabilir bellek yok. tooincrease hello bellek Dwu hello sayısını artırmak veya hello kaynak sınıfı artırmak için yük sorgu, verin.

- tooincrease hello Dwu, bkz: [nasıl ı ölçeklendirme performans?](sql-data-warehouse-manage-compute-overview.md#scale-compute)
- toochange hello kaynak sınıfı bir sorgu için bkz: [kullanıcı kaynak sınıfı örneğini değiştirmek](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).

Örneğin, DWU 100 üzerinde hello smallrc kaynak sınıfında bir kullanıcı her dağıtım için 100 MB bellek kullanabilir. Merhaba Ayrıntılar için bkz [eşzamanlılık SQL Data warehouse'da](sql-data-warehouse-develop-concurrency.md).

Bellek tooget yüksek kaliteli satır grubu kimliğinde boyutları 700 MB gerektiğini belirlemek varsayalım. Bu örnekler, yeterli belleğe sahip hello yük sorgu nasıl çalıştırabileceğiniz gösterir.

- DWU 1000 ve mediumrc kullanarak, 800 MB bellek ataması
- DWU 600 ve largerc kullanarak bellek ataması 800 MB'tır.


## <a name="next-steps"></a>Sonraki adımlar

toofind SQL Data Warehouse, daha fazla yol tooimprove performans bkz hello [performans genel bakış](sql-data-warehouse-overview-manage-user-queries.md).

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
