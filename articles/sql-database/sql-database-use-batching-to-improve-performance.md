---
title: "aaaHow toouse tooimprove Azure SQL veritabanı uygulama performansı toplu işleme"
description: "Merhaba konu toplu işlemleri büyük ölçüde veritabanındaki kanıt sağlar imroves hello hızı ve Azure SQL veritabanı uygulamalarınızın ölçeklenebilirlik. Bu toplu teknikler herhangi bir SQL Server veritabanı için çalışır hello odak hello makalenin Azure üzerinde olsa da."
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a>Nasıl toouse tooimprove SQL veritabanı uygulama performansını toplu işleme
SQL veritabanı işlemleri tooAzure önemli ölçüde toplu işleme hello performans ve ölçeklenebilirlik uygulamalarınızın artırır. Sipariş toounderstand hello faydalarını sıralı ve toplu istekleri tooa SQL veritabanı karşılaştırmak bazı örnek test sonuçlarını hello ilk bölümü, bu makalenin ele alınmaktadır. Merhaba hello makalenin kalanında hello teknikleri, senaryoları ve konuları toohelp gösterir başarıyla Azure uygulamalarınızda toplu işleme toouse.

## <a name="why-is-batching-important-for-sql-database"></a>SQL veritabanı için önemli toplu işleme neden?
Toplu işlem çağrıları tooa uzak hizmet performansını ve ölçeklenebilirliğini artırmak için iyi bilinen bir stratejidir. Seri hale getirme, ağ aktarımı ve seri durumdan çıkarma gibi uzak bir hizmet ile maliyetleri tooany etkileşimleri işleme var. düzeltilmiştir. Tek bir toplu birçok ayrı işlemlere paketleme bu maliyetleri en aza indirir.

Bu yazıda, tooexamine çeşitli SQL veritabanı toplu stratejilerini ve senaryoları istiyoruz. Bu stratejileri ayrıca SQL Server kullanan şirket içi uygulamaları için önemli olsa da, SQL veritabanı için toplu işleme hello kullanım vurgulama için birkaç nedeni vardır:

* Olup olmadığını potansiyel olarak büyük ağ gecikmesi SQL veritabanına erişim özellikle dış hello SQL veritabanına erişme aynı Microsoft Azure veri merkezi.
* hello veri verimliliğini hello SQL veritabanı anlamına gelir Hello çok müşterili özelliklere erişim katmanı karşılık gelen toohello hello veritabanının genel ölçeklenebilirlik. SQL veritabanı, veritabanı kaynakları toohello zarar diğer kiracıların tekeline tek bir Kiracı/Kullanıcı engellemeniz gerekir. Önceden tanımlanmış kotaları aşan yanıt toousage içinde SQL veritabanı işleme azaltın veya özel durumlar azaltma ile yanıt verir. Toplu işleme gibi verimliliği, SQL veritabanı üzerinde daha fazla iş bu sınırları ulaşmadan önce toodo etkinleştirin. 
* Toplu işleme ayrıca birden çok veritabanı (parçalama) kullanan mimari için geçerli değildir. Her veritabanı birimi ile etkileşim Hello verimliliğini hala bir anahtar genel ölçeklenebilirlik içinde faktördür. 

SQL veritabanı kullanmanın yararları hello konak hello veritabanının toomanage hello sunucuları yok biridir. Ancak, bu yönetilen altyapı Ayrıca, farklı veritabanı en iyi duruma getirme hakkında toothink anlamına gelir. Artık, donanım veya ağ tooimprove hello veritabanı altyapısı da bakabilirsiniz. Microsoft Azure konusu ortamlara denetler. denetleyebileceğiniz hello ana uygulamanızın SQL Database ile nasıl etkileşim kurduğu alanıdır. Toplu işleme, bu en iyi duruma getirme biridir. 

Merhaba ilk bölümü hello kağıt SQL veritabanını kullan .NET uygulamaları için çeşitli toplu teknikleri inceler. Merhaba son iki bölüm toplu kılavuzları ve senaryoları kapsar.

## <a name="batching-strategies"></a>Toplu işleme stratejileri
### <a name="note-about-timing-results-in-this-topic"></a>Bu konudaki zamanlama sonuçlarıyla ilgili unutmayın
> [!NOTE]
> Sonuçları kıyaslamaları değildir ancak tooshow yöneliktir **göreli performans**. Zamanlamaları, en az 10 test çalışmaları ortalama üzerinde temel alır. Boş bir tablo ekler işlemleridir. Bu testler ölçülen öncesi V12 olan ve mutlaka hello kullanarak yeni bir V12 veritabanında karşılaşabileceğiniz toothroughput benzemez [hizmet katmanları](sql-database-service-tiers.md). Merhaba göreli teknik toplu işleme hello yararı benzer olmalıdır.
> 
> 

### <a name="transactions"></a>İşlemler
Garip toobegin işlemleri ele tarafından toplu işleme, bir gözden geçirme görünüyor. Ancak istemci-tarafı işlemleri hello kullanımını performansını artıran zarif bir toplu sunucu tarafı etkisi olmaz. Ve sıralı işlemlerinin bir hızlı yol tooimprove performansını sağlamak için yalnızca birkaç kod satırıyla, işlemleri eklenebilir.

INSERT dizisini içeren C# kod aşağıdaki hello göz önünde bulundurun ve basit bir tablo üzerinde işlem güncelleştirin.

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

ADO.NET kodu sırayla aşağıdaki hello bu işlemleri gerçekleştirir.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

Bu kodu en iyi şekilde toooptimize hello tooimplement istemci-tarafı bu çağrıları toplu işleme, bazı biçimidir. Ancak bu kod basit yol tooincrease hello performansını çağrısı hello sırası işlemde yalnızca kaydırma tarafından. İşte hello bir işlem kullandığı aynı kodu.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

İşlemleri, aslında bu örnekler ikisinde kullanılıyor. Merhaba ilk örnekte, tek tek her çağrı örtük bir işlemdir. Merhaba ikinci örnekte, açık bir işlem tüm hello çağrılarını sarmalar. Merhaba hello belgelerine başına [yazma ileriye işlem günlüğü](https://msdn.microsoft.com/library/ms186259.aspx), günlük kayıtlarını alırken temizlenmiş toohello disk hello hareketi tamamlar. Hello işlem kadar bu nedenle bir işlemde daha fazla çağrıları dahil ederek hello yazma toohello işlem günlüğü gecikmeye yol açabilir. Uygulamada hello yazma toohello sunucunun işlem günlüğü için toplu işleme olanaklı kılıyor.

Aşağıdaki tablonun hello bazı geçici test sonuçlarını gösterir. Merhaba testleri sıralı aynı olan ve olmayan işlemler ekler hello gerçekleştirilir. Daha fazla perspektif için bir Microsoft Azure dizüstü toohello veritabanında testlerin ilk Seti hello uzaktan verdi. Merhaba testlerin ikinci Seti bir bulut hizmeti ve her ikisi de hello içinde aynı belgeler, veritabanı çalışan Microsoft Azure veri merkezi (Batı ABD). Merhaba aşağıdaki tabloda hello süresi sıralı ekler ve işlemleri kullanılmadan milisaniye olarak gösterir.

**Şirket içi tooAzure**:

| İşlemler | Hiçbir işlem (ms) | İşlem (ms) |
| --- | --- | --- |
| 1 |130 |402 |
| 10 |1208 |1226 |
| 100 |12662 |10395 |
| 1000 |128852 |102917 |

**Azure tooAzure (aynı veri merkezinde)**:

| İşlemler | Hiçbir işlem (ms) | İşlem (ms) |
| --- | --- | --- |
| 1 |21 |26 |
| 10 |220 |56 |
| 100 |2145 |341 |
| 1000 |21479 |2756 |

> [!NOTE]
> Sonuçları kıyaslamaları değildir. Merhaba bkz [bu konudaki zamanlama sonuçlarıyla ilgili Not](#note-about-timing-results-in-this-topic).
> 
> 

Merhaba önceki test sonuçlarına bağlı olarak bir işlem içinde tek bir işlem kaydırma aslında performansı düşürür. Ancak, tek bir işlem içinde işlemlerinin hello sayısı arttıkça, hello performans geliştirmesi daha olarak işaretlenmiş olur. tüm işlemleri hello Microsoft Azure veri merkezi içinde olduğunda hello performans ayrıca daha belirgin farktır. Merhaba dış hello Microsoft Azure veri merkezinden SQL veritabanı kullanarak, daha yüksek gecikme süresi işlemleri kullanmanın hello performans kazancı gölgelendiren.

İşlemler Hello kullanımı performansı artırabilirsiniz ancak çok devam[işlemleri ve bağlantıları için en iyi uygulamaları gözlemlemek](https://msdn.microsoft.com/library/ms187484.aspx). Merhaba iş tamamlandıktan sonra hello işlem olası ve Kapat hello veritabanı bağlantısı olarak kısa tutun. Merhaba önceki örnekte deyimiyle hello hello izleyen kod bloğunun tamamlandığında hello bağlantı kapalı olduğundan emin olmasını sağlar.

Merhaba önceki örnekte iki satır bir yerel işlem tooany ADO.NET koduyla ekleyebileceğiniz gösterilmektedir. İşlemler tooimprove hello performans sıralı yapan kod ekleme, güncelleştirme ve silme işlemleri hızlı bir yol sunar. Ancak, hello hızlı performans için tablo değerli parametreleri gibi istemci tarafı, toplu işleme hello kod başka tootake avantajı değiştirmeyi göz önünde bulundurun.

ADO.NET işlemleri hakkında daha fazla bilgi için bkz: [ADO.NET yerel işlemlerde](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).

### <a name="table-valued-parameters"></a>Tablo değerli parametreleri
Tablo değerli parametreleri kullanıcı tanımlı tablo türü parametre olarak Transact-SQL deyimi, saklı yordamları ve işlevleri destekler. Bu istemci-tarafı toplu teknik toosend sağlayan hello tablo değerli parametre içindeki verilerin birden çok satır. toouse tablo değerli parametreleri, ilk olarak bir tablo türü tanımlayın. Transact-SQL deyimi aşağıdaki hello adlı bir tablo türü oluşturur **MyTableType**.

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


Kod içinde oluşturduğunuz bir **DataTable** hello ile aynı ad ve hello tablo türü türlerini tam. Bunu geçirmek **DataTable** metin sorgusu veya saklı yordam parametresinde çağırın. Merhaba aşağıdaki örnekte bu teknik gösterilmektedir:

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

Merhaba önceki örnekte hello **SqlCommand** nesnesi bir tablo değerli parametresinden satırları ekler  **@TestTvp** . daha önce oluşturduğunuz hello **DataTable** nesne hello toothis parametresiyle atanmış **SqlCommand.Parameters.Add** yöntemi. Bir toplu hello ekler, sıralı ekler hello performans artışları önemli ölçüde çağırın.

tooimprove hello önceki örnek ayrıca, metin tabanlı komutu yerine bir saklı yordamı kullanın. Transact-SQL komutu aşağıdaki hello oluşturur hello isteyen bir saklı yordamı **SimpleTestTableType** tablo değerli parametre.

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

Merhaba değiştirme **SqlCommand** hello önceki kod örneğinde toohello aşağıdaki bildiriminde nesne.

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

Çoğu durumda, diğer toplu teknikleri daha eşdeğer veya daha iyi performans tablo değerli parametrelere sahip. Diğer seçenekler daha esnek olduğundan tablo değerli genellikle tercih, parametreleridir. Örneğin, SQL toplu kopyalama gibi başka teknikler yalnızca yeni satır hello ekleme izin verir. Ancak tablo değerli parametreleri ile Merhaba saklı yordamı toodetermine hangi satırların güncelleştirmelerin mantığı kullanabilirsiniz ve hangi ekler. Merhaba tablo türü de değiştirilmiş toocontain hello satır eklenmesi, silinmiş veya güncelleştirilmesi belirtilen olup olmadığını gösteren bir "İşlem" sütunu olabilir.

Aşağıdaki tablonun hello geçici tablo değerli parametreleri hello kullanımı için test sonuçları milisaniye olarak gösterir.

| İşlemler | Şirket içi tooAzure (ms) | Azure aynı veri merkezinde (ms) |
| --- | --- | --- |
| 1 |124 |32 |
| 10 |131 |25 |
| 100 |338 |51 |
| 1000 |2615 |382 |
| 10000 |23830 |3586 |

> [!NOTE]
> Sonuçları kıyaslamaları değildir. Merhaba bkz [bu konudaki zamanlama sonuçlarıyla ilgili Not](#note-about-timing-results-in-this-topic).
> 
> 

Toplu işleme gelen hello performans kazancı hemen açıktır. Merhaba önceki sıralı test, 1000 işlemleri dış hello datacenter ve hello veri merkezinde bulunan 21 saniyeden 129 saniye sürdü. Ancak tablo değerli parametreleri ile 1000 işlemleri yalnızca hello veri merkezi dışında 2.6 saniye ile Merhaba veri merkezinde bulunan 0,4 saniye sürer.

Tablo değerli parametreleri hakkında daha fazla bilgi için bkz: [tablo değerli parametreleri](https://msdn.microsoft.com/library/bb510489.aspx).

### <a name="sql-bulk-copy"></a>SQL toplu kopyalama
SQL toplu kopyalama başka bir şekilde tooinsert büyük miktarlarda verinin bir hedef veritabanına ' dir. .NET uygulamaları hello kullanabileceğiniz **SqlBulkCopy** sınıfı tooperform toplu ekleme işlemleri. **SqlBulkCopy** işlevi toohello komut satırı aracı'nda benzer **Bcp.exe**, veya hello Transact-SQL deyimini **BULK INSERT**. Merhaba aşağıdaki kod örneğinde nasıl toobulk kopyalama hello hello kaynağında satırları gösterir **DataTable**, tablo, SQL Server'daki MyTable toohello hedef tablo.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

Toplu kopyalama tablo değerli parametre tercih edilen olduğu bazı durumlar vardır. Tablo değerli parametreleri karşılık toplu ekleme işlemleri hello konudaki Hello karşılaştırma tablosuna bakın [tablo değerli parametreleri](https://msdn.microsoft.com/library/bb510489.aspx).

Merhaba aşağıdaki geçici test sonuçları gösterir hello performansını ile toplu işleme **SqlBulkCopy** milisaniye cinsinden.

| İşlemler | Şirket içi tooAzure (ms) | Azure aynı veri merkezinde (ms) |
| --- | --- | --- |
| 1 |433 |57 |
| 10 |441 |32 |
| 100 |636 |53 |
| 1000 |2535 |341 |
| 10000 |21605 |2737 |

> [!NOTE]
> Sonuçları kıyaslamaları değildir. Merhaba bkz [bu konudaki zamanlama sonuçlarıyla ilgili Not](#note-about-timing-results-in-this-topic).
> 
> 

Daha küçük toplu boyutlarında hello kullan tablo değerli parametreleri outperformed hello **SqlBulkCopy** sınıfı. Ancak, **SqlBulkCopy** 12-%31 tablo değerli parametreleri daha hızlı gerçekleştirilen 1.000 ile 10.000 satırları hello testler için. Tablo değerli parametreleri gibi **SqlBulkCopy** özellikle karşılaştırıldığında toplu eklemeleri için iyi bir seçenek olan toplu olmayan işlemlerinin toohello performansını.

ADO.NET toplu kopyalama hakkında daha fazla bilgi için bkz: [SQL Server toplu kopyalama işlemleri](https://msdn.microsoft.com/library/7ek5da1a.aspx).

### <a name="multiple-row-parameterized-insert-statements"></a>Birden çok satır parametreli INSERT deyimleri
Bir küçük toplu işlemler için birden çok satır ekleyen INSERT deyimi tooconstruct büyük parametreli alternatiftir. Aşağıdaki kod örneğine Merhaba, bu tekniği gösterir.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


Bu örnek tooshow hello temel kavram amaçlanmıştır. Daha gerçekçi bir senaryo hello komut parametreleri gerekli hello varlıklar tooconstruct hello sorgu dizesi ile aynı anda döngüsü. Sınırlı tooa toplam 2100 sorgu parametreleri, böylece bu hello bu şekilde işlenebilir satırların toplam sayısını sınırlar.

Bu tür milisaniye cinsinden INSERT deyiminin geçici test sonuçları göster hello performans aşağıdaki hello.

| İşlemler | Tablo değerli parametreleri (ms) | Tek deyimli Ekle (ms) |
| --- | --- | --- |
| 1 |32 |20 |
| 10 |30 |25 |
| 100 |33 |51 |

> [!NOTE]
> Sonuçları kıyaslamaları değildir. Merhaba bkz [bu konudaki zamanlama sonuçlarıyla ilgili Not](#note-about-timing-results-in-this-topic).
> 
> 

Bu yaklaşım, 100'den az satırlar toplu işlemler için biraz daha hızlı olabilir. Merhaba geliştirme küçük olsa da, bu teknik iyi belirli uygulama senaryonuz çalışabilir başka bir seçenektir.

### <a name="dataadapter"></a>DataAdapter
Merhaba **DataAdapter** sınıfı toomodify verir bir **DataSet** nesne ve hello değişiklikleri INSERT, UPDATE ve DELETE işlemleri olarak gönderin. Merhaba kullanıyorsanız **DataAdapter** bu şekilde, çağrıları ayrı toonote her ayrı bir işlem için yapılan önemlidir. tooimprove performansı, kullanım hello **UpdateBatchSize** özelliği toohello aynı anda toplu işlem sayısı. Daha fazla bilgi için bkz: [toplu işlemleri kullanarak DataAdapters gerçekleştirme](https://msdn.microsoft.com/library/aadf8fk2.aspx).

### <a name="entity-framework"></a>Varlık çerçevesi
Toplu işleme Entity Framework şu anda desteklemiyor. Merhaba topluluğundaki farklı geliştiriciler geçersiz kılma hello gibi toodemonstrate geçici çözümler çalıştı **SaveChanges** yöntemi. Ancak hello çözümler genellikle karmaşık ve özelleştirilmiş toohello uygulama ve veri modeli. Hello Entity Framework codeplex proje şu anda bu özellik isteğinde tartışma sayfa yok. tooview bu tartışma bkz [tasarım Toplantı Notları - 2 Ağustos 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).

### <a name="xml"></a>XML
Eksiksiz olması için bir toplu stratejisi olarak XML hakkında önemli tootalk olduğunu düşündüğünüz. Ancak, XML hello kullanımını diğer yöntemleri hiçbir avantajları ve birkaç dezavantajları vardır. Merhaba yaklaşım, benzer tootable değerli parametreleri olmakla birlikte bir XML dosyası veya dize tooa depolanan yordamı kullanıcı tanımlı bir tablo yerine geçirilir. Merhaba saklı yordamı hello saklı yordamı hello komutlarda ayrıştırır.

Toothis yaklaşım birkaç dezavantajları şunlardır:

* XML ile çalışma sıkıcı olabilir ve hataya.
* Merhaba veritabanı hello XML ayrıştırma, yoğun CPU kullanımına neden olabilir.
* Çoğu durumda, bu yöntem tablo değerli parametreleri yavaştır.

Bu nedenlerle, toplu sorgular için XML hello kullanılması önerilmez.

## <a name="batching-considerations"></a>Dikkat edilecek noktalar toplu işleme
Aşağıdaki bölümlerde hello hello kullanımıyla SQL veritabanı uygulamalarında toplu işleme için daha fazla rehberlik sağlar.

### <a name="tradeoffs"></a>Bileşim
Mimarinizi bağlı olarak, toplu işleme kolaylığını performans ve dayanıklılık arasındaki içerebilir. Örneğin, burada rolünüze beklenmedik bir şekilde arıza hello senaryoyu göz önünde bulundurun. Bir veri satırı kaybederseniz, hello gönderilmeyen satırları büyük toplu kaybetme hello etkisi küçük etkisidir. Belirtilen zaman penceresi için toohello veritabanı göndermeden satırları arabellek yapıldığında büyük bir risk alınamıyor.

Bu kolaylığını nedeniyle, toplu işlemler hello türünü değerlendirin. Daha agresif toplu (büyük toplu işlemler ve daha uzun zaman pencereleri) verilerle daha az önemlidir.

### <a name="batch-size"></a>Toplu iş boyutu
Bizim testlerinde genellikle hiçbir avantajı toobreaking büyük toplu işlemleri daha küçük parçalara vardı. Aslında, bu alt bölümü genellikle tek bir büyük toplu iş gönderme daha yavaş performans ile sonuçlandı. Örneğin, tooinsert 1000 satırı istediğiniz bir senaryo düşünün. Merhaba aşağıdaki tabloda toouse tablo değerli parametreleri küçük yığınlara bölünmüş zaman tooinsert 1000 satırları süreyi gösterir.

| Toplu iş boyutu | Yineleme | Tablo değerli parametreleri (ms) |
| --- | --- | --- |
| 1000 |1 |347 |
| 500 |2 |355 |
| 100 |10 |465 |
| 50 |20 |630 |

> [!NOTE]
> Sonuçları kıyaslamaları değildir. Merhaba bkz [bu konudaki zamanlama sonuçlarıyla ilgili Not](#note-about-timing-results-in-this-topic).
> 
> 

Merhaba en iyi performans için 1000 satırı toosubmit olduğunu görebilirsiniz tümünü. (Burada gösterilmiyor) diğer testlerinde 5000 iki toplu 10000 satır toplu küçük performans kazancı toobreak vardı. Ancak hello tablo şemasını bu testler için oldukça basittir, gerçekleştirmesi gereken şekilde, belirli veri ve toplu iş boyutu tooverify bu bulgularını sınar.

Başka bir faktör tooconsider hello toplam toplu iş çok büyük olursa, SQL veritabanı azaltma ve toocommit hello toplu Reddet olmasıdır. İdeal toplu iş boyutu ise hello en iyi sonuçlar için belirli bir senaryoyu toodetermine sınayın. Merhaba toplu iş boyutu performans veya hatalar göre çalışma zamanı tooenable hızlı ayarlamalar adresindeki yapılandırılabilir olun.

Son olarak, toplu işleme ile ilişkili hello riskleri ile Merhaba toplu iş boyutu hello dengeleyin. Geçici bir hata veya hello rol başarısız olursa hello sonuçlarıyla hello işlemi yeniden denemeden veya hello toplu hello veri kaybı göz önünde bulundurun.

### <a name="parallel-processing"></a>Paralel işleme
Ne hello toplu iş boyutunu azaltma hello yaklaşım sürdü ancak çoklu iş parçacığı tooexecute hello iş kullanılan? Yeniden testlerimizde birkaç küçük birden çok iş parçacıklı toplu işlemi genellikle tek bir büyük toplu daha da kötüsü gerçekleştirdiği gösterdi. Merhaba aşağıdaki test bir veya daha fazla paralel yığınlardaki tooinsert 1000 satırı çalışır. Bu test nasıl daha fazla eşzamanlı toplu gerçekte performansı düşebilir gösterir.

| Toplu iş boyutu [yineleme] | İki iş parçacığı (ms) | Dört iş parçacığı (ms) | Altı iş parçacıkları (ms) |
| --- | --- | --- | --- |
| 1000 [1] |277 |315 |266 |
| 500 [2] |548 |278 |256 |
| 250 [4] |405 |329 |265 |
| 100 [10] |488 |439 |391 |

> [!NOTE]
> Sonuçları kıyaslamaları değildir. Merhaba bkz [bu konudaki zamanlama sonuçlarıyla ilgili Not](#note-about-timing-results-in-this-topic).
> 
> 

Performans düşüşü hello için birkaç olası nedeni vardır son tooparallelism:

* Bir yerine birden çok eşzamanlı ağ çağrıları vardır.
* Birden çok işlem tek bir tabloyu karşı Çekişme ve engelleme neden olabilir.
* İle ilişkili ek yüklerini vardır çoklu iş parçacığı kullanımı.
* birden çok bağlantı açma hello gider paralel işleme hello yararı ağır.

Farklı tablolar veya veritabanlarına hedef, bazı performans elde bu strateji ile olası toosee olur. Veritabanı parçalama veya Federasyon bir senaryo için bu yaklaşım olacaktır. Birden çok veritabanını ve yolları farklı veri tooeach veritabanı parçalama kullanır. Her küçük bir toplu iş tooa farklı veritabanı olacaksa, ardından hello paralel işlemleri daha etkili olabilir. Ancak, hello performans kazancı yeterince önemli toouse karar toouse veritabanı parçalama çözümünüzdeki hello temeli olarak değil.

Bazı tasarımları küçük toplu işlemlerin Paralel yürütme yük altında bir sistem isteklerin geliştirilmiş verimini sonuçlanabilir. Daha hızlı tooprocess tek bir büyük toplu olmasına karşın, bu durumda, birden çok toplu işlem paralel işleme daha etkili olabilir.

Paralel yürütme kullanırsanız denetleme hello en fazla çalışan iş parçacığı sayısını göz önünde bulundurun. Daha küçük bir sayı çekişmelerinin azalmasını ve daha hızlı bir yürütme süresi neden olabilir. Ayrıca, bu hello hedef veritabanı bağlantılarını ve işlemleri yerleştirir hello ek yük göz önünde bulundurun.

### <a name="related-performance-factors"></a>İlgili performans Etkenler
Toplu işleme veritabanı performansını normal yönergeler de etkiler. Örneğin, INSERT performans büyük birincil bir anahtar veya birçok kümelenmemiş dizinlerine sahip tablolar için azaltılır.

Tablo değerli parametreleri bir saklı yordam kullanırsanız, hello komutunu kullanabilirsiniz **SET NOCOUNT ON** hello başında hello yordamı. Bu bildirimi etkilenen hello satırların hello yordamdaki Merhaba sayımını hello dönüşünü gizler. Ancak, bizim testlerinde kullanımını hello **SET NOCOUNT ON** hiçbir etkisi olan ya da performansı düşebilir. Merhaba test saklı yordamı ile tek bir basit **Ekle** hello tablo değerli parametre komutu. Daha karmaşık saklı yordamlar bu deyimden yararlanabileceğini mümkündür. Ancak bu ekleme varsaymayın **SET NOCOUNT ON** tooyour depolanan yordamı, otomatik olarak performansını artırır. toounderstand Merhaba etkisi, saklı yordam ve hello kullanılmadan test **SET NOCOUNT ON** deyimi.

## <a name="batching-scenarios"></a>Toplu işleme senaryoları
Merhaba aşağıdaki bölümlerde nasıl üç uygulama senaryolarında toouse tablo değerli parametreleri. Merhaba ilk senaryoda arabelleğe alma ve yığınlama birlikte nasıl çalışabileceğini gösterir. Merhaba ikinci senaryo, bir tek bir saklı yordam çağrısında ana-ayrıntı işlemleri gerçekleştirerek performansı artırır. Merhaba son senaryo gösterilmektedir nasıl toouse tablo değerli parametre bir "UPSERT" işlemi.

### <a name="buffering"></a>Arabelleğe alma
Toplu işleme için belirgin aday olan bazı senaryolar olsa da, Gecikmeli işlemesi toplu işleme avantajı ele geçirebilir birçok senaryo vardır. Ancak, aynı zamanda Gecikmeli işleme beklenmeyen bir hata hello olayda hello veri kaybı büyük bir risk taşır. Önemli toounderstand bu riskidir ve hello sonuçlarıyla göz önünde bulundurun.

Örneğin, her kullanıcı hello Gezinti geçmişini izler bir web uygulaması göz önünde bulundurun. Her sayfa isteğinde Merhaba uygulaması bir veritabanı çağrısı toorecord hello kullanıcının sayfa görünümü hale getirebilir. Ancak daha yüksek performans ve ölçeklenebilirlik hello kullanıcıların Gezinti etkinlikleri arabelleğe alma ve ardından bu verileri toohello veritabanı toplu olarak gönderilmesi tarafından gerçekleştirilebilir. Geçen süre ve/veya arabellek boyutu tarafından hello veritabanı güncelleştirmeleri tetikleyebilir. Örneğin, bir kural hello toplu sonra 20 saniye veya hello arabellek 1000 öğeleri ulaştığında işlenmesi gerektiğini belirtebilirsiniz.

Merhaba aşağıdaki kod örneğinde [reaktif uzantılar - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess arabelleğe alınmış izleme sınıfı tarafından başlatılan olayları. Ne zaman arabellek dolgular Merhaba veya bir zaman aşımı ulaşıldığında, kullanıcı verilerini hello toplu toohello veritabanı tablo değerli bir parametre ile gönderilir.

Aşağıdaki NavHistoryData sınıfı modelleri hello kullanıcı Gezinti ayrıntılara hello. Merhaba kullanıcı tanımlayıcısı gibi temel bilgileri içeren, hello URL erişilen ve erişim zamanı hello.

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

Merhaba NavHistoryDataMonitor sınıfı hello kullanıcı Gezinti veri toohello veritabanına arabelleğe almak için sorumludur. Bir yöntemi, yükselterek yanıt RecordUserNavigationEntry içeren bir **OnAdded** olay. Merhaba aşağıdaki kod Rx toocreate kullanan hello Oluşturucu mantığı hello olaya göre bir observable koleksiyonu gösterir. Ardından toothis observable koleksiyonu hello arabellek yöntemiyle abone. Merhaba aşırı bu hello arabellek 20 dakikada veya 1000 girişleri gönderilmesi gerektiğini belirtir.

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

Merhaba işleyici arabelleğe hello öğelerin tümünü bir tablo değerli türüne dönüştürür ve ardından bu tür tooa depolanan yordamı işlemleri hello toplu geçirir. Merhaba aşağıdaki kod hello tam tanımı hello NavHistoryDataEventArgs ve hello NavHistoryDataMonitor sınıfları gösterir.

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

toouse Merhaba uygulaması arabelleğe alma Bu sınıf bir statik NavHistoryDataMonitor nesnesi oluşturur. Sayfasında, bir kullanıcının eriştiği her zaman hello uygulama hello NavHistoryDataMonitor.RecordUserNavigationEntry yöntemini çağırır. mantığı arabelleğe alma hello bu girişleri toohello veritabanı toplu olarak gönderilmesi care of tootake devam eder.

### <a name="master-detail"></a>Ana ayrıntısı
Tablo değerli parametreleri basit Ekle senaryoları için kullanışlıdır. Ancak, bir tablodaki birden çok içeren daha zorlu toobatch ekler olabilir. Merhaba "ana/ayrıntı" senaryosu iyi bir örnektir. Merhaba ana tablo hello birincil varlık tanımlar. Bir veya daha fazla ayrıntı tabloları hello varlık hakkında daha fazla veri depolar. Bu senaryoda, yabancı anahtar ilişkileri hello ilişki ayrıntıları tooa benzersiz ana varlığın uygulayın. Bir PurchaseOrder tablosu ve onun ilişkili OrderDetail tablosu basitleştirilmiş bir sürümünü göz önünde bulundurun. Merhaba Transact-SQL aşağıdaki dört sütunlarla hello PurchaseOrder tablo oluşturur: OrderID, OrderDate, CustomerID ve durum.

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

Her sipariş bir veya daha fazla ürün satın alma işlemleri içerir. Bu bilgiler hello PurchaseOrderDetail tabloda yakalanır. Transact-SQL aşağıdaki hello beş sütunlarla hello PurchaseOrderDetail tablo oluşturur: OrderID, OrderDetailID, ProductID, UnitPrice ve OrderQty.

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

Merhaba OrderID hello PurchaseOrderDetail tablo sütununda bir sipariş hello PurchaseOrder tablosundan başvurmalıdır. bir yabancı anahtar tanımını izleyen hello bu kısıtlamayı zorlar.

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

Sipariş toouse tablo değerli parametreleri, her bir hedef tablo için bir kullanıcı tanımlı tablo türü olmalıdır.

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

Ardından, bu tür tabloları kabul eden bir saklı yordam tanımlayın. Bu yordam bir uygulama toolocally toplu tek bir çağrıda bir dizi siparişleri ve Sipariş ayrıntılarını verir. Merhaba aşağıdaki Transact-SQL hello tam saklı yordam bildirimi bu satın alma siparişi örneğin sağlar.

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

Bu örnekte, yerel olarak tanımlanan hello @IdentityLink tablo hello gerçek OrderID değerleri yeni eklenen hello satırlardan depolar. Bu sipariş tanımlayıcılar hello hello geçici OrderID değerlerinden farklı @orders ve @details tablo değerli parametreleri. Bu nedenle, hello @IdentityLink tablo ardından hello hello OrderID değerleri bağlanır @orders parametresi toohello hello PurchaseOrder tablosundaki hello yeni satırlar için gerçek OrderID değerler. Bu adımdan sonra hello @IdentityLink tablo hello ekleme hello sipariş ayrıntılarla kolaylaştırmak hello yabancı anahtar kısıtlaması karşılayan gerçek OrderID.

Bu saklı yordam, kod veya diğer Transact-SQL çağrıları kullanılabilir. Kod örneği için Bu raporda Hello tablo değerli parametreleri bölümüne bakın. Transact-SQL aşağıdaki hello nasıl toocall hello sp_InsertOrdersBatch gösterir.

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

Bu çözüm, 1'den başlayan OrderID değerler kümesi her toplu toouse sağlar. Bu geçici OrderID değerleri hello toplu hello ilişkilerde açıklar ancak hello gerçek OrderID değerler hello ekleme işlemi hello aynı anda belirlenir. Merhaba önceki örnekte aynı deyimleri hello art arda çalıştırın ve hello veritabanında benzersiz siparişler oluşturmaz. Bu nedenle, bu teknik toplu işleme kullanırken yinelenen siparişleri engelleyen daha fazla kod veya veritabanı mantığı eklemeyi düşünün.

Bu örnek, tablo değerli parametreleri kullanarak ana / ayrıntı işlemleri gibi daha karmaşık veritabanı işlemleri toplu olduğunu gösterir.

### <a name="upsert"></a>UPSERT
Başka bir toplu senaryo, aynı anda var olan satır ve ekleme yeni satırlar güncelleştirilmesini gerektirir. Bu işlem bazen başvurulan tooas bir "UPSERT" (güncelleştirme + Ekle) işlem olur. Ayrı çağrıları tooINSERT ve güncelleştirme yapmak yerine, hello MERGE deyiminin en uygun toothis bir görevdir. Hello MERGE deyimi, hem INSERT işlemi ve tek bir çağrı işlemlerinde güncelleştirin.

Tablo değerli parametreleri hello MERGE deyimi tooperform güncelleştirmeleri ve eklemeleri ile kullanılabilir. Örneğin, sütunları aşağıdaki hello içeren basitleştirilmiş bir çalışan tablosunun göz önünde bulundurun: EmployeeID, FirstName, LastName, SocialSecurityNumber:

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

Bu örnekte, bu hello SocialSecurityNumber benzersiz tooperform birden fazla çalışanı BİRLEŞTİRMESİ olan hello olgu kullanabilirsiniz. İlk olarak, hello kullanıcı tanımlı tablo türü oluşturun:

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

Ardından, bir saklı yordam oluşturmak veya kullanır MERGE deyimi tooperform hello güncelleştirme hello ve Ekle kod yazma. Merhaba aşağıdaki örnek hello MERGE deyiminin bir tablo değerli parametre kullanır @employees, EmployeeTableType türünde. Merhaba Merhaba içeriğine @employees tablo aşağıda gösterilmez.

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

Daha fazla bilgi için hello belgeler ve örnekler hello MERGE deyimi için bkz. Aynı iş birden çok adım gerçekleştirilebilir hello depolanmış yordam çağrısı ayrı ekleme ve güncelleştirme işlemleri ile rağmen hello MERGE deyimi daha verimli olur. Veritabanı kod iki veritabanı çağrılarını ekleme ve güncelleştirme için gerek kalmadan doğrudan hello MERGE deyiminin kullanan Transact-SQL çağrıları de oluşturabilirsiniz.

## <a name="recommendation-summary"></a>Öneri özeti
Merhaba aşağıdaki listede bu konuda tartışılan önerileri toplu işleme hello bir özetini sunar:

* Arabelleğe alma ve tooincrease hello performansını ve ölçeklenebilirliğini SQL veritabanı uygulamaları yığınlama kullanın.
* Toplu işleme/arabelleğe alma ve dayanıklılık arasında Hello bileşim anlayın. Bir rol hata sırasında işlenmemiş bir toplu iş açısından kritik verilerin kaybı hello risk toplu işleme hello performans avantajı üstün olabilir.
* Tookeep tüm çağrıları toohello veritabanı bir tek veri merkezi tooreduce gecikme süresi içinde çalışır.
* Tek bir toplu teknik seçerseniz, tablo değerli parametreleri hello en iyi performans ve esneklik sunar.
* Merhaba hızlı performans eklemek, aşağıdaki genel yönergeleri izleyin ancak senaryonuza test:
  * < 100 satır için tek bir parametreli Ekle komutunu kullanın.
  * < 1000 satırı için tablo değerli parametreleri kullanın.
  * İçin > = 1000 satır SqlBulkCopy kullanın.
* İçin güncelleştirme ve silme işlemleri, hello doğru işlemi hello tablo parametresinde her satırda belirler saklı yordam mantığı ile tablo değerli parametreleri kullanın.
* Toplu iş boyutu yönergeleri:
  * Uygulama ve iş gereksinimleri için anlamlı hello en büyük toplu iş boyutu kullanılır.
  * Bakiye hello performans büyük toplu geçici veya geri dönülemez hataları hello riskleri ile elde edilir. Yeniden deneme hello sonucu veya hello toplu hello veri kaybı nedir? 
  * SQL veritabanı reddetmek değil, hello en büyük toplu iş boyutu tooverify sınayın.
  * Bu denetim, hello toplu iş boyutu veya hello arabelleğe alma zaman penceresi gibi toplu işleme yapılandırma ayarları oluşturur. Bu ayarları esneklik sağlar. Davranış üretim hello bulut hizmeti yeniden dağıtmadan toplu işleme hello değiştirebilirsiniz.
* Bir veritabanı tek bir tabloda çalışmayabilir toplu işlemlerin Paralel yürütme kaçının. Tek bir toplu toodivide birden fazla çalışan iş parçacıkları arasında seçerseniz, testler toodetermine hello ideal iş parçacığı sayısını çalıştırın. Belirtilmeyen bir eşik sonra daha fazla iş parçacığı performansını düşürebilir yerine onu artırın.
* Boyut ve daha fazla senaryoları için toplu işleme uygulamanın yolu sürede arabelleğe almayı düşünün.

## <a name="next-steps"></a>Sonraki adımlar
Veritabanı tasarımını ve teknikleri kodlama toobatching ilişkisini üzerine odaklanan bu makalede, uygulama performansı ve ölçeklenebilirliği artırabilir. Ancak bu yalnızca bir faktör olarak genel stratejinize. Daha fazla yol tooimprove performans ve ölçeklenebilirlik için bkz: [tek veritabanları için Azure SQL Database performans rehberi](sql-database-performance-guidance.md) ve [esnek havuzlar için fiyat ve performans konuları](sql-database-elastic-pool-guidance.md).

