---
title: "aaaAzure SQL Database esnek sorgu genel bakış | Microsoft Docs"
description: "Merhaba esnek sorgu özelliğine genel bakış"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: a8bf0e2c-bc74-44d0-9b1e-bcc9a6aa2e33
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: mlandzic
ms.openlocfilehash: db17f551882cfcae0da67fdda12708baeb6db81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-elastic-query-overview-preview"></a>Azure SQL Database esnek sorgu genel bakış (Önizleme)
Merhaba esnek sorgu özelliği (Önizleme) toorun Azure SQL veritabanında birden çok veritabanı yayılan bir Transact-SQL sorgusu sağlar. Tooperform arası veritabanı sorguları tooaccess uzak tablolar ve tooconnect Microsoft ve üçüncü taraf araçları (Excel, Powerbı, Tableau, vb.) tooquery veri katmanlarıyla birden fazla veritabanı üzerinden sağlar. Bu özelliği kullanarak SQL veritabanında sorguları toolarge veri katmanlarını ölçeğini ve iş zekası (BI) raporlarında hello sonuçlarını görselleştirme.


## <a name="why-use-elastic-queries"></a>Esnek sorgular neden kullanılır?

**Azure SQL Veritabanı**

Azure SQL veritabanlarında tamamen T-SQL sorgulama. Bu, uzak veritabanlarına salt okunur sorgulamaya izin verir. Bu, üç ve dört part adları veya bağlantılı sunucu tooSQL DB kullanan SQL Server müşteriler toomigrate uygulamalar şirket içinde geçerli bir seçenek sağlar.

**Standart katmanda kullanılabilir**

Esnek sorgu toplama toohello Premium performans katmanı standart performans katmanında hello desteklenir. Daha düşük performans katmanı için performans sınırlamaları üzerinde Önizleme sınırlamaları Hello bölümüne bakın.

**Anında iletme tooremote veritabanları**

Esnek sorgular SQL parametreleri toohello uzak veritabanları yürütme için şimdi gönderebilir.

**Saklı yordam yürütme**

Uzak saklı yordam çağrıları ya da uzak işlevleri kullanarak yürütme [sp\_yürütme \_uzak](https://msdn.microsoft.com/library/mt703714).

**Esneklik**

Esnek sorgu ile dış tablolar şimdi tooremote tabloları farklı şema veya tablo adı ile başvurabilirsiniz.

## <a name="elastic-query-scenarios"></a>Esnek sorgu senaryoları

Merhaba, burada birden çok veritabanı tek bir genel sonuç satırları katkıda senaryoları sorgulama toofacilitate hedefidir. Merhaba sorgu ya da hello kullanıcı veya uygulama tarafından doğrudan birleştirilebilen ya da dolaylı olarak bağlantılı toohello veritabanı olan araçları üzerinden. Bu rapor, ticari BI veya veri tümleştirme araçları kullanarak oluştururken özellikle yararlı olacaktır — ya da değiştirilemez herhangi bir uygulama. Esnek bir sorgu ile Merhaba tanıdık SQL Server bağlantı deneyimi Excel, Powerbı, Tableau veya Cognos gibi araçları kullanarak birden fazla veritabanı üzerinden sorgulayabilirsiniz.
Esnek bir sorgu SQL Server Management Studio veya Visual Studio tarafından verilen sorguları aracılığıyla veritabanlarının tooan tüm koleksiyon kolay erişim sağlar ve veritabanları arası Entity Framework veya diğer ORM ortamları sorgulanmasını kolaylaştırır. Şekil 1, burada varolan izin ver bulut uygulaması bir senaryo gösterir (Merhaba kullanan [esnek veritabanı istemci Kitaplığı](sql-database-elastic-database-client-library.md)) derlemeleri ölçeklendirilmiş veri katmanı ve esnek sorgu veritabanları arası raporlaması için kullanılır.

**Şekil 1** ölçeklendirilmiş veri katmanını kullanılan esnek sorgu

![Ölçeklendirilen veri katmanını kullanılan esnek sorgu][1]

Müşteri senaryoları için esnek sorgu topolojileri aşağıdaki hello tarafından belirlenir:

* **Dikey bölümleme - veritabanları arası sorguları** (topoloji 1): hello veri bölümlenmiş dikey olarak bir veri katmanı bulunan veritabanlarının sayısına arasında. Genellikle, farklı veritabanlarını tabloları farklı kümesi bulunur. Bu hello şema farklı veritabanlarında farklı olduğu anlamına gelir. Örneğin, tüm hesap ilişkili tabloları ikinci bir veritabanı üzerinde çalışırken tüm tablolar için stok bir veritabanında ' dir. Bu topoloji ile ortak kullanım durumları bir tooquery arasında veya birden fazla veritabanı tablolarında üzerinden toocompile raporları gerektirir.
* **Yatay bölümleme - parçalama** (topolojisi 2): verileri yatay olarak bölümlenmiş bir genişletilmiş veri toodistribute satırlarda katmanı. Bu yaklaşımda, hello şema tüm katılan veritabanları aynıdır. Bu yaklaşım, "parçalama" olarak da adlandırılır. Parçalama gerçekleştirilebilir ve (1) hello esnek veritabanı araçları kitaplıkları veya (2) self-parçalama kullanılarak yönetilebilir. Esnek bir sorgu fazla parça kullanılan tooquery veya derleme raporlar değildir.

> [!NOTE]
> Esnek sorgu hello işleme çoğunu hello veri katmanını burada gerçekleştirilebilir zaman raporlama senaryoları için en iyi şekilde çalışır. Raporlama yoğun iş yükleri veya veri depolama senaryolarında ile daha karmaşık sorgular için de kullanmayı [Azure SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
>  

## <a name="vertical-partitioning---cross-database-queries"></a>Dikey bölümleme - veritabanları arası sorguları

kodlama, toobegin bkz [(dikey bölümleme) veritabanları arası sorgusu ile çalışmaya başlama](sql-database-elastic-query-getting-started-vertical.md).

Esnek bir sorgu, bir SQL veritabanı kullanılabilir tooother SQL veritabanlarında bulunan kullanılan toomake veriler olabilir. Bu, tüm diğer uzak SQL veritabanında bir veritabanı toorefer tootables sorgularından sağlar. Merhaba ilk toodefine her uzak veritabanı için dış veri kaynağına adımdır. Merhaba dış veri kaynağına hello yerel veritabanı hello Uzak veritabanı üzerinde bulunan toogain erişim tootables istediğiniz tanımlanır. Hiçbir değişiklik hello Uzak veritabanı üzerinde gereklidir. Farklı veritabanlarına farklı şemalar sahip olduğu dikey bölümleme için tipik senaryolar, esnek sorgular kullanılan tooimplement erişim tooreference verileri gibi ortak kullanım durumları kullanılabilir ve veritabanları arası sorgulama.

> [!IMPORTANT]
> ALTER ANY dış veri KAYNAĞINA iznine sahip olması gerekir. Bu izni hello ALTER DATABASE iznine dahil edilir. ALTER ANY dış veri kaynağı, veri kaynağı arka plandaki gerekli toorefer toohello izinlerdir.
>

**Başvuru verileri**: hello topoloji başvuru veri yönetimi için kullanılır. Merhaba aşağıdaki şekilde, başvuru verilerinde bulunan iki tabloları (T1 ve T2) adanmış bir veritabanında tutulur. Esnek bir sorgu kullanarak, artık tabloları T1 ve T2 uzaktan diğer veritabanlarından hello şekilde gösterildiği gibi erişebilirsiniz. Başvuru tabloları küçük ya da uzak sorguları başvuru tablosu varsa 1 topolojisini kullan seçmeli koşullar vardır.

**Şekil 2** dikey bölümleme - esnek sorgu tooquery başvuru verileri kullanma

![Dikey bölümleme - esnek sorgu tooquery başvuru verileri kullanma][3]

**Veritabanları arası sorgulama**: esnek sorgular birkaç SQL veritabanları arasında sorgulama gerektiren etkinleştir kullanım örnekleri. Şekil 3, dört farklı veritabanları gösterir: CRM, Envanter, İK ve ürünler. Tooone erişim hello veritabanlarından birini gerçekleştirilen sorgular ayrıca veya tüm diğer veritabanlarına hello. Esnek bir sorgu kullanarak, her bir hello dört veritabanı birkaç basit DDL deyimleri çalıştırarak bu durumda, veritabanınızı yapılandırabilirsiniz. Bu tek seferlik yapılandırma sonra erişim tooa uzak tablo T-SQL sorgularınızı veya BI araçları tooa yerel tabloya başvuran olarak kadar basittir. Merhaba uzak sorgular büyük sonuç döndürmezse bu yaklaşım önerilir.

**Şekil 3** dikey bölümleme - çeşitli veritabanları arasında esnek sorgu tooquery kullanma

![Dikey bölümleme - çeşitli veritabanları arasında esnek sorgu tooquery kullanma][4]

Merhaba aşağıdaki adımları yapılandırmak erişim tooa tabloda bulunan hello olan uzak SQL veritabanlarında aynı gerektiren dikey bölümleme senaryolar için esnek veritabanı sorguları şeması:

* [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx) mymasterkey
* [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx) mycredential
* [CREATE/DROP dış veri KAYNAĞINA](https://msdn.microsoft.com/library/dn935022.aspx) gelen veriKaynağım'a türü **RDBMS**
* [CREATE/DROP dış tablo](https://msdn.microsoft.com/library/dn935021.aspx) mytable

Merhaba DDL deyimleri çalıştırdıktan sonra dizinindeymiş gibi yerel bir tabloya hello uzak tablo "mytable" erişebilir. Azure SQL veritabanı otomatik olarak bir bağlantı toohello Uzak veritabanı açar, isteğiniz hello Uzak veritabanı üzerinde işler ve hello sonuçlar döndürür.

## <a name="horizontal-partitioning---sharding"></a>Yatay bölümleme - parçalama
Veri katmanı gerektiren esnek sorgu tooperform bir parçalı, yani, yatay olarak bölümlenmiş, raporlama görevlerini kullanarak bir [esnek veritabanı parça eşleme](sql-database-elastic-scale-shard-map-management.md) hello veri katmanı toorepresent hello veritabanları. Genellikle, yalnızca bir tek parça eşleme Bu senaryoda kullanılan ve esnek sorgu özellikleri (baş düğüm) ile ayrılmış bir veritabanı sorguları raporlama hello giriş noktası olarak görev yapar. Bu adanmış veritabanı erişimi toohello parça eşleme gerekir. Şekil 4, bu topoloji ve yapılandırmasıyla hello esnek sorgu veritabanı ve parça eşleme ile gösterilmektedir. Merhaba veritabanları hello veri katmanındaki tüm Azure SQL veritabanı sürümü veya sürümü olabilir. Merhaba esnek veritabanı istemci kitaplığı ve parça eşlemeleri oluşturma hakkında daha fazla bilgi için bkz: [parça eşleme Yönetim](sql-database-elastic-scale-shard-map-management.md).

**Şekil 4** yatay bölümleme - parçalı veriler katmanları raporlama için esnek sorgu kullanma

![Yatay bölümleme - parçalı veriler katmanları raporlama için esnek sorgu kullanma][5]

> [!NOTE]
> Esnek sorgu veritabanı (baş düğüm) ayrı veritabanı olabilir veya hello olabilir aynı ana bilgisayar hello parça eşlenen veritabanı. Seçtiğiniz herhangi bir yapılandırma emin olun, veritabanının bu hizmet ve performans katmanı yeterince toohandle beklenen hello oturum açma/sorgu isteği miktarıdır.

Merhaba aşağıdaki adımları bulunan tablo erişim tooa kümesi gerektiren yatay bölümleme senaryoları için esnek veritabanı sorgularını (genellikle) birkaç uzak SQL veritabanlarında yapılandırın:

* [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx) mymasterkey
* [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx) mycredential
* Oluşturma bir [parça eşleme](sql-database-elastic-scale-shard-map-management.md) hello esnek veritabanı istemci kitaplığı kullanılarak, veri katmanı temsil eden.   
* [CREATE/DROP dış veri KAYNAĞINA](https://msdn.microsoft.com/library/dn935022.aspx) gelen veriKaynağım'a türü **SHARD_MAP_MANAGER**
* [CREATE/DROP dış tablo](https://msdn.microsoft.com/library/dn935021.aspx) mytable

Bu adımları gerçekleştirdikten sonra dizinindeymiş gibi yerel bir tabloya hello yatay olarak bölümlenmiş tabloda "mytable" erişebilir. Azure SQL veritabanı otomatik olarak birden çok paralel bağlantıları toohello Uzak veritabanı hello tabloları fiziksel olarak nerede depolandığı açar, hello uzak veritabanlarında hello isteklerini işler ve hello sonuçlar döndürür.
Merhaba yatay bölümleme senaryo bulunabilir için gereken hello adımları hakkında daha fazla bilgi [yatay bölümleme için esnek sorgu](sql-database-elastic-query-horizontal-partitioning.md).

kodlama, toobegin bkz [yatay (parçalama) bölümleme için esnek sorgu ile çalışmaya başlama](sql-database-elastic-query-getting-started.md).

## <a name="t-sql-querying"></a>T-SQL sorgulama
Dış veri kaynakları ve dış tablolarınızı tanımladıktan sonra dış tablolara tanımlandığı normal SQL Server bağlantı dizelerini tooconnect toohello veritabanları kullanabilirsiniz. Ardından T-SQL deyimlerini dış tablolar üzerindeki bu bağlantıda özetlenen hello kısıtlamalarla çalıştırabilirsiniz. Daha fazla bilgi ve örnekler T-SQL sorgularını hello belgelerine konuları bulabilirsiniz [yatay bölümleme](sql-database-elastic-query-horizontal-partitioning.md) ve [dikey bölümleme](sql-database-elastic-query-vertical-partitioning.md).

## <a name="connectivity-for-tools"></a>Bağlantı için araçları
Uygulama ve dış tablolar BI veya veri tümleştirme araçları toodatabases normal SQL Server bağlantı dizelerini tooconnect kullanabilirsiniz. SQL Server, aracı için bir veri kaynağı olarak desteklendiğinden emin olun. Aracınızı toowith bağlanmak herhangi bir SQL Server veritabanı ile yalnızca yaptığınız gibi bağlandıktan sonra toohello esnek sorgu veritabanı ve hello dış tablolarda veritabanının bakın.

> [!IMPORTANT]
> Esnek sorgularıyla Azure Active Directory'yi kullanarak kimlik doğrulaması şu anda desteklenmiyor.
> 
> 

## <a name="cost"></a>Maliyet
Esnek sorgu Azure SQL veritabanı veritabanları hello maliyetini dahil edilir. Uzak veritabanlarınızı nerede farklı veri merkezinde esnek sorgu endpoint hello daha topolojileri desteklenir, ancak uzak veritabanlarından veri çıkışı normal ücretlendirilirsiniz Not [Azure oranları](https://azure.microsoft.com/pricing/details/data-transfers/).

## <a name="preview-limitations"></a>Önizleme sınırlamaları
* İlk esnek sorgunuzu çalıştıran alabilir tooa hello standart performans katmanı üzerinde birkaç dakika. Gerekli tooload hello esnek sorgu işlevi zamandır; Performans yüklenirken daha yüksek performans katmanlarıyla artırır.
* Dış veri kaynakları veya dış tablolara SSMS veya SSDT komut dosyası yazma henüz desteklenmiyor.
* İçeri/dışarı aktarma SQL DB için dış veri kaynakları ve dış tablolar henüz desteklemiyor. Toouse içeri/dışarı aktarma gerekiyorsa, dışarı aktarmadan önce bu nesneleri bırakın ve sonra bunları aldıktan sonra yeniden oluşturun.
* Esnek sorgu şu anda yalnızca salt okunur erişim tooexternal tabloları destekler. Ancak, T-SQL işlevlerini hello veritabanında hello dış tablo tanımlandığı kullanabilirsiniz. Bu, örn., geçici sonuçları devam ettirmek için kullanarak, örn., seçin < column_list > < local_table > ya da toodefine tooexternal tabloları başvuran hello esnek sorgu veritabanı üzerinde saklı yordamları yararlı olabilir.
* Dış tablo tanımlarında nvarchar(max) hariç LOB türleri desteklenmez. Geçici bir çözüm olarak, nvarchar(max) hello LOB türünü çevirir hello Uzak veritabanı üzerinde bir görünüm oluşturun, hello temel tablo yerine hello görünüm üzerinden, dış tablo tanımlayabilir ve ardından onu geri hello özgün LOB sorgularınızda türe.
* Sütun istatistikleri dış tablolara şu anda desteklenmemektedir. Tablo istatistikleri desteklenir, ancak el ile oluşturulan toobe gerekir.

## <a name="feedback"></a>Geri Bildirim
Lütfen deneyiminizi geribildirim esnek sorgularıyla bizimle Disqus aşağıdaki hello MSDN Forumları veya Stackoverflow paylaşın. Merhaba hizmet (kusurları, pürüzleri, özellik boşluklar) hakkındaki görüşlerinizi her türlü ilginizi duyuyoruz.

## <a name="next-steps"></a>Sonraki adımlar

* Dikey bölümleme öğretici için bkz: [(dikey bölümleme) veritabanları arası sorgusu ile çalışmaya başlama](sql-database-elastic-query-getting-started-vertical.md).
* Dikey olarak bölümlenmiş verilere ilişkin söz dizimi ve örnek sorgular için bkz: [dikey sorgulama bölümlenmiş veri)](sql-database-elastic-query-vertical-partitioning.md)
* Yatay bölümleme (parçalama) bir öğretici için bkz: [yatay (parçalama) bölümleme için esnek sorgu ile çalışmaya başlama](sql-database-elastic-query-getting-started.md).
* Yatay olarak bölümlenmiş verilere ilişkin söz dizimi ve örnek sorgular için bkz: [yatay sorgulama bölümlenmiş veri)](sql-database-elastic-query-horizontal-partitioning.md)
* Bkz: [sp\_yürütme \_uzak](https://msdn.microsoft.com/library/mt703714) tek uzaktan Azure SQL veritabanı ya da yatay bölümleme düzenindeki parça olarak hizmet veren bir veritabanları kümesi üzerinde bir Transact-SQL deyimini yürütür bir saklı yordam için.

<!--Image references-->
[1]: ./media/sql-database-elastic-query-overview/overview.png
[2]: ./media/sql-database-elastic-query-overview/topology1.png
[3]: ./media/sql-database-elastic-query-overview/vertpartrrefdata.png
[4]: ./media/sql-database-elastic-query-overview/verticalpartitioning.png
[5]: ./media/sql-database-elastic-query-overview/horizontalpartitioning.png

<!--anchors-->
