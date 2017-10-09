---
title: "aaaResolving T-SQL farkları geçiş Azure SQL veritabanı | Microsoft Docs"
description: "Azure SQL Veritabanında tam olarak desteklenmeyen Transact-SQL deyimleri"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: c05abd9e-28a7-4c97-9bdf-bc60d08fc92e
ms.service: sql-database
ms.custom: load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 03/17/2017
ms.author: rickbyh
ms.openlocfilehash: 3852013338bfdc6c7da9d1d879c54781682bc635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resolving-transact-sql-differences-during-migration-toosql-database"></a>Geçiş tooSQL veritabanı sırasında Transact-SQL farkları çözme   
Zaman [veritabanınızı geçirme](sql-database-cloud-migrate.md) SQL Server tooAzure ' SQL Server, veritabanınızın bazı SQL Server geçiş yapabilir hello önce yeniden mühendislik gerektirdiğini fark edebilirsiniz. Bu konuda, hem bu yeniden mühendislik gerçekleştirme ve nedenleri neden temel hello anlama yeniden mühendislik hello Kılavuzu tooassist gereklidir sağlar. toodetect uyumsuzlukları kullanmak hello [veri geçiş Yardımcısı (DMA)](https://www.microsoft.com/download/details.aspx?id=53595).

## <a name="overview"></a>Genel Bakış
Uygulamaları kullanan çoğu Transact-SQL özelliklerini hem Microsoft SQL Server hem de Azure SQL veritabanı tam olarak desteklenir. Örneğin, veri türleri, işleçler, dize, aritmetik, mantıksal ve imleci İşlevler, SQL Server ve SQL veritabanını aynı çalışma gibi çekirdek SQL bileşenleri hello. Ancak bazı T-SQL farklılıklar vardır DDL (veri tanımlama dili) ve T-SQL deyimlerini ve yalnızca kısmen desteklenen sorgu DML (veri işleme dili) öğeleri (, bu konunun ilerleyen bölümlerinde aşağıdakiler ele).

Ayrıca, bazı özellikler vardır ve Azure SQL veritabanı olduğundan hiç desteklenmeyen söz dizimi hello ana veritabanı ve hello işletim sistemi bağımlılıkları tooisolate özelliklerinden tasarlanmıştır. Bu nedenle, sunucu düzeyi etkinliklerin çoğu SQL veritabanı için uygun. Sunucu düzeyinde seçeneklerini, işletim sistemi bileşenleri yapılandırmak veya dosya sistemi yapılandırması belirtin T-SQL deyimlerini ve seçenekler kullanılamaz. Aşağıdakiler gibi özelliklerinden gerekli olduğunda, uygun bir alternatif genellikle diğer herhangi bir yolla kullanılabilir SQL veritabanı veya başka bir Azure özellik veya hizmet. 

Örneğin, yüksek kullanılabilirlik (tooconfigure etkin coğrafi çoğaltma için bir olağanüstü durum hello olayı içinde daha hızlı kurtarma istediğiniz ancak) her zaman açık yapılandırma gerekli değildir, Azure'da oluşturulmuştur. Bu nedenle, T-SQL deyimlerini tooavailability grupların SQL veritabanı tarafından desteklenmiyor ve hello dinamik yönetim görünümlerini ilgili tooAlways üzerinde de desteklenmez ilgili.

Desteklenen ve desteklenmeyen SQL veritabanı tarafından hello özelliklerin listesi için bkz: [Azure SQL veritabanı özellik karşılaştırması](sql-database-features.md). Bu sayfada Hello liste, bu yönergeleri ve özellikleri bölümüne ek niteliğindedir ve Transact-SQL deyimlerini temel odaklanır.

## <a name="transact-sql-syntax-statements-with-partial-differences"></a>Kısmi farklarla birlikte Transact-SQL söz dizimi deyimleri
Merhaba çekirdek (veri tanımlama dili) DDL deyimleri kullanılabilir, ancak bazı DDL deyimleri uzantıları ilgili toodisk yerleştirme ve desteklenmeyen özelliklere sahip. 

- OLUŞTURMA ve ALTER DATABASE deyimleri üzerinde üç düzine seçeneğiniz vardır. Merhaba deyimleri dosya yerleştirme, FILESTREAM ve yalnızca tooSQL sunucu geçerli hizmet Aracısı seçenekleri içerir. Geçiş, ancak veritabanları oluşturuyorsa T-SQL kodunu geçiriyorsanız karşılaştırmanız gerekir önce veritabanları oluşturursanız, bu önemli değil [CREATE DATABASE (Azure SQL veritabanı)](https://msdn.microsoft.com/library/dn268335.aspx) hello SQL Server sözdizimine sahip [oluştur Veritabanı (SQL Server Transact-SQL)](https://msdn.microsoft.com/library/ms176061.aspx) toomake emin kullandığınız tüm hello seçenek desteklenmez. Azure SQL veritabanı için veritabanı oluşturma, ayrıca hizmet hedefi ve yalnızca tooSQL veritabanı geçerli esnek ölçeklendirme seçenekleri sahiptir.
- Merhaba oluşturma ve ALTER TABLE deyimleri FILESTREAM desteklenmediği için SQL veritabanında kullanılamaz FileTable seçeneğiniz vardır.
- CREATE ve ALTER oturum açma ifadeleri desteklenir, ancak SQL veritabanı tüm hello seçeneklerini sunmaz. Veritabanınızı daha taşınabilir SQL veritabanı kullanarak teşvik eden toomake oturumları mümkün olduğunda yerine veritabanı kullanıcıları içeriyor. Daha fazla bilgi için bkz: [CREATE/ALTER oturum açma](https://msdn.microsoft.com/library/ms189828.aspx) ve [denetleme ve veritabanı erişimi verme](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins).

## <a name="transact-sql-syntax-not-supported-in-sql-database"></a>SQL Veritabanında desteklenmeyen Transact-SQL söz dizimleri   
Ayrıca tooTransact SQL deyimleri ilgili toohello desteklenmeyen özelliklere açıklanan [Azure SQL veritabanı özellik karşılaştırması](sql-database-features.md), hello deyimleri ve deyimleri grupları, desteklenmez. Veritabanı toobe geçirdiyseniz, bu nedenle hello aşağıdakilerden herhangi birini kullanan özellikler, T-SQL tooeliminate yeniden mühendislik bu T-SQL özelliklerini ve deyimleri.

- Harmanlanmış sistem nesneleri
- Bağlantıyla ilişkili: Uç nokta deyimleri, `ORIGINAL_DB_NAME`. SQL veritabanı Windows kimlik doğrulamasını desteklemez, ancak hello benzer Azure Active Directory kimlik doğrulamasını destekler. Bazı kimlik doğrulama türleri hello SSMS en son sürümünü gerektirir. Daha fazla bilgi için bkz: [bağlanıyor tooSQL veritabanı veya SQL veri ambarı tarafından kullanarak Azure Active Directory kimlik doğrulaması](sql-database-aad-authentication.md).
- Üç veya dört bölüm adı kullanan veritabanları arası sorgular. (Salt okunur veritabanları arası sorgular [elastik veritabanı sorgusu](sql-database-elastic-query-overview.md) kullanılarak desteklenir.)
- Veritabanları arası sahiplik zinciri, `TRUSTWORTHY` ayarı
- `DATABASEPROPERTY` Bunun yerine `DATABASEPROPERTYEX` kullanın.
- `EXECUTE AS LOGIN` Bunun yerine "EXECUTE AS USER" kullanın.
- Genişletilebilir anahtar yönetimi haricinde şifreleme desteklenir
- Olay: Olaylar, olay bildirimleri, sorgu bildirimleri
- Dosya yerleştirme: sözdizimi ilgili toodatabase dosya yerleştirme, boyutu ve Microsoft Azure tarafından otomatik olarak yönetilir veritabanı dosyaları.
- Yüksek Kullanılabilirlik: sözdizimi ilgili Microsoft Azure hesabınız üzerinden yönetilen toohigh kullanılabilirlik. Buna yedekleme, geri yükleme, Her Zaman Açık, veritabanı yansıtması, günlük aktarma ve kurtarma modları için söz dizimleri dahildir.
- Günlük Okuyucusu: SQL veritabanı üzerinde kullanılabilir değil hello günlük okuyucu üzerine dayanır sözdizimi: itme çoğaltma, değişiklik verilerini yakalama. SQL Veritabanı gönderme temelli çoğaltma gönderisinin abonesi olabilir.
- İşlevler: `fn_get_sql`, `fn_virtualfilestats`, `fn_virtualservernodes`
- Genel geçici tablolar
- Donanım: Sözdizimi ilgili toohardware ilgili sunucu ayarları: bellek, çalışan iş parçacığı, CPU benzeşimi gibi izleme bayrakları. Bunun yerine hizmet düzeylerini kullanın.
- `HAS_DBACCESS`
- `KILL STATS JOB`
- `OPENQUERY`, `OPENROWSET`, `OPENDATASOURCE`ve dört bölümden oluşan adları
- .NET framework: SQL Server CLR tümleştirme
- Anlamsal arama
- Sunucu kimlik bilgileri: kullanım [veritabanı kapsamlı kimlik bilgileri](https://msdn.microsoft.com/library/mt270260.aspx) yerine.
- Sunucu düzeyi öğeler: Sunucu rolleri, `IS_SRVROLEMEMBER`, `sys.login_token`. `GRANT`, `REVOKE` ve `DENY` sunucu düzeyi izinler kullanılamaz ancak bazıları veritabanı düzeyi izinlerle değiştirilmiştir. Sunucu düzeyi kullanışlı DMV'lerden bazıları, eşdeğer veritabanı düzeyi DMV'lerine sahiptir.
- `SET REMOTE_PROC_TRANSACTIONS`
- `SHUTDOWN`
- `sp_addmessage`
- `sp_configure` seçenekleri ve `RECONFIGURE`. Bazı seçenekler [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx) ile kullanılabilir.
- `sp_helpuser`
- `sp_migrate_user_to_contained`
- SQL Server Agent: hello SQL Server Agent ya da hello MSDB veritabanı güvenen söz dizimi: uyarıları, işleçler, merkezi yönetim sunucuları. Bunun yerine Azure PowerShell gibi betik uygulamaları kullanın.
- SQL Server audit: SQL veritabanını kullan yerine denetleme.
- SQL Server izleme
- İzleme bayrakları: toocompatibility modları öğeleri olmuştur bazı izleme bayrağı taşındı.
- Transact-SQL hata ayıklama
- Tetikleyiciler: Sunucu kapsamlı veya oturum açma tetikleyicileri
- `USE`deyimi: toochange hello veritabanı bağlamı tooa farklı veritabanı, yeni bir bağlantı toohello yeni veritabanı olmalısınız.

## <a name="full-transact-sql-reference"></a>Tam Transact-SQL başvurusu
Transact-SQL dil bilgisi, kullanımı ve örnekleri için SQL Server Çevrimiçi Kitapları sayfasında [Transact-SQL Başvurusu (Veritabanı Altyapısı)](https://msdn.microsoft.com/library/bb510741.aspx) bölümüne bakın. 

### <a name="about-hello-applies-to-tags"></a>Merhaba "uygulandığı" etiketler hakkında
Merhaba Transact-SQL başvuru konuları ilgili tooSQL Server sürümleri 2008 toohello mevcut içerir. Merhaba konu başlığı bir simge çubuğu, listeleme hello dört SQL sunucu platformları ve belirten Uygulanabilirlik yoktur. Örneğin kullanılabilirlik grupları SQL Server 2012'de tanıtılmıştır. [AVAILABILTY grubu oluşturma](https://msdn.microsoft.com/library/ff878399.aspx) konu gösterir hello deyim için geçerli olduğunu **SQL Server'ın (2012'den başlayarak)**. Merhaba deyimi tooSQL Server 2008, SQL Server 2008 R2, Azure SQL Database, Azure SQL Data Warehouse veya paralel veri ambarı geçerli değildir.

Bazı durumlarda, konunun hello genel konu bir üründe kullanılabilir, ancak ürünleri arasında küçük farklar vardır. Hello farklılıklar uygun şekilde hello konudaki Orta noktalar sırasında belirtilir. Bazı durumlarda, konunun hello genel konu bir üründe kullanılabilir, ancak ürünleri arasında küçük farklar vardır. Hello farklılıklar uygun şekilde hello konudaki Orta noktalar sırasında belirtilir. Örneğin hello CREATE TRIGGER konu SQL veritabanında kullanılabilir. Ancak hello **tüm sunucu** seçeneği için sunucu düzeyi tetikleyiciler, sunucu düzeyi Tetikleyiciler SQL veritabanında kullanılamaz olduğunu gösterir. Bunun yerine veritabanı düzeyi tetikleyicilerin kullanın.

## <a name="next-steps"></a>Sonraki adımlar

Desteklenen ve desteklenmeyen SQL veritabanı tarafından hello özelliklerin listesi için bkz: [Azure SQL veritabanı özellik karşılaştırması](sql-database-features.md). Bu sayfada Hello liste, bu yönergeleri ve özellikleri bölümüne ek niteliğindedir ve Transact-SQL deyimlerini temel odaklanır.

