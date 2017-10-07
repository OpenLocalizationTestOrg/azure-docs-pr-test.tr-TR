---
title: "aaaSQL hata kodları - veritabanı bağlantı hatası | Microsoft Docs"
description: "Ortak veritabanı bağlantı hataları, veritabanı kopyalama sorunlarını ve genel hataları gibi SQL Database istemci uygulamaları için SQL hata kodları hakkında bilgi edinin. "
keywords: "SQL hata kodu, erişim sql, veritabanı bağlantı hatası, sql hata kodları"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 2a23e4ca-ea93-4990-855a-1f9f05548202
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 683a7d72c935742f3f9f9a0c683e5d8161167d6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-error-codes-for-sql-database-client-applications-database-connection-error-and-other-issues"></a>SQL Database istemci uygulamaları için SQL hata kodları: veritabanı bağlantı hatası ve diğer sorunlar
<!--
Old Title on MSDN:  Error Messages (Azure SQL Database)
ShortId on MSDN:  ff394106.aspx
Dx 4cff491e-9359-4454-bd7c-fb72c4c452ca
-->


Bu makalede SQL veritabanı, veritabanı bağlantı hataları, geçici hataları (geçici hataları olarak da bilinir), kaynak İdaresi hataları, veritabanı kopyalama sorunlarını, esnek havuz ve başka hatalar da dahil olmak üzere istemci uygulamaları için SQL hata kodları listelenmektedir. Çoğu kategorileri, belirli tooAzure SQL veritabanı olan ve SQL Server tooMicrosoft geçerli değildir.

## <a name="database-connection-errors-transient-errors-and-other-temporary-errors"></a>Veritabanı bağlantı hataları, geçici hataları ve diğer geçici hataları
Merhaba aşağıdaki tabloda bağlantı kaybı hataları ve uygulamanızı tooaccess SQL veritabanı çalıştığında karşılaşabileceğiniz diğer geçici hataları için hello SQL hata kodları yer almaktadır. Başlarken eğitimleri hakkında yönergeler için bkz tooconnect tooAzure SQL Database, [tooAzure SQL veritabanına bağlanma](sql-database-libraries.md).

### <a name="most-common-database-connection-errors-and-transient-fault-errors"></a>En yaygın veritabanı bağlantı hataları ve geçici hata hataları
Hello Azure altyapı yoğun iş yükleri hello SQL veritabanı hizmetinin ortaya zaman sunucularını yeniden hello özelliği toodynamically sahiptir.  Bu dinamik davranış istemciniz program toolose neden olabilir, bağlantı tooSQL veritabanı. Bu tür bir hata durumu olarak adlandırılan bir *geçici hata*.

Böylece hello geçici hata zaman toocorrect kendisini vermiş sonra bağlantı yeniden, istemci programınızı yeniden deneme mantığına sahiptir önerilir.  İlk, yeniden denemeden önce 5 saniye gecikme öneririz. 5 saniyeden daha kısa bir gecikme sonrasında yeniden deneniyor zorlamayı hello bulut hizmeti risklerini. Sonraki denemeler hello gecikme katlanarak, tooa 60 saniye olarak en fazla büyümesini.

Geçici hata hatalar genellikle, istemci programlardan hata iletileri aşağıdaki hello biri olarak bildirimi:

* Veritabanı &lt;db_name&gt; sunucuda &lt;Azure_instance&gt; şu anda kullanılamıyor. Lütfen hello bağlantıyı daha sonra yeniden deneyin. Merhaba sorun devam ederse müşteri desteğine başvurun ve hello oturum izleme Kimliğini verin &lt;session_id&gt;
* Veritabanı &lt;db_name&gt; sunucuda &lt;Azure_instance&gt; şu anda kullanılamıyor. Lütfen hello bağlantıyı daha sonra yeniden deneyin. Merhaba sorun devam ederse müşteri desteğine başvurun ve hello oturum izleme Kimliğini verin &lt;session_id&gt;. (Microsoft SQL Server, hata: 40613)
* Varolan bir bağlantıyı zorla hello uzak ana bilgisayar tarafından kapatıldı.
* System.Data.Entity.Core.EntityCommandExecutionException: Hello komut tanımı yürütülürken bir hata oluştu. Merhaba, Ayrıntılar için iç özel duruma bakın. System.Data.SqlClient.SqlException--->: sonuçları hello sunucudan alırken bir aktarım düzeyi hatası oluştu. (sağlayıcısı: oturum sağlayıcısı, hata: 19 - fiziksel bağlantı değil kullanılabilir)
* Bir bağlantı girişimi tooa ikincil veritabanı reconfguration hello işleminde hello veritabanıdır ve hello birincil veritabanında yeni sayfalarında hello ortasını etkin bir işlem sırasında uygulama meşgul olduğundan başarısız oldu. 

Yeniden deneme mantığı kod örnekleri için bkz:

* [SQL Database ve SQL Server için bağlantı kitaplıkları](sql-database-libraries.md) 
* [Eylemler toofix bağlantı hataları ve SQL veritabanında geçici hataları](sql-database-connectivity-issues.md)

Merhaba tartışması *engelleme süresi* ADO.NET kullanan istemciler için kullanılabilir [SQL Server bağlantı havuzu (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).

### <a name="transient-fault-error-codes"></a>Geçici hata hata kodları
Merhaba aşağıdaki hataları geçici ve uygulama mantığını yeniden denenmesi gerekiyor 

| Hata kodu | Önem Derecesi | Açıklama |
| ---:| ---:|:--- |
| 4060 |16 |Veritabanı açılamıyor. "%. & #x2a; ls" Merhaba oturum açma tarafından istenen. Merhaba oturum açma başarısız oldu. |
| 40197 |17 |Merhaba hizmet isteğinizi işlerken bir hatayla karşılaştı. Lütfen yeniden deneyin. Hata kodu %d.<br/><br/>Merhaba hizmet aşağı toosoftware veya donanım yükseltmeleri, donanım hataları veya başka bir yük devretme sorunları olduğunda bu hatayı alırsınız. Katıştırılmış hata 40197 Hello iletisi içinde hello hata kodu (%d) hello tür hata veya oluştu yük devretme hakkında ek bilgi sağlar. Bazı hello hata kodları hata 40197 selamlama iletisine içinde katıştırılmış 40020, 40143, 40166 ve 40540 gösterilebilir.<br/><br/>Yeniden bağlanan tooyour SQL veritabanı sunucusu tooa sağlıklı veritabanınızın kopyasını otomatik olarak bağlanır. Uygulamanız hata 40197, günlük katıştırılmış hello hata kodu (%d) sorun giderme için selamlama iletisine içinde yakalamak ve tooSQL veritabanı hello kaynakların kullanılabilir ve, bağlantı yeniden kurulana kadar yeniden bağlanmayı deneyin. |
| 40501 |20 |Merhaba Hizmet şu anda meşgul. Merhaba isteği 10 saniye sonra yeniden deneyin. Olay Kimliği: %ls. Kodu: %d.<br/><br/>*Not:* daha fazla bilgi için bkz:<br/>• [Azure SQL veritabanı kaynak sınırları](sql-database-resource-limits.md). |
| 40613 |17 |Veritabanı '%. & #x2a; ls' sunucusundaki '%. & #x2a; ls' şu anda kullanılamıyor. Lütfen hello bağlantıyı daha sonra yeniden deneyin. Merhaba sorun devam ederse müşteri desteğine başvurun ve hello oturum izleme Kimliğini verin '%. & #x2a; ls'. |
| 49918 |16 |İsteği işleyemiyor. Yeterli kaynaklara tooprocess isteyin.<br/><br/>Merhaba Hizmet şu anda meşgul. Lütfen hello isteği daha sonra yeniden deneyin. |
| 49919 |16 |İşlem oluşturulamıyor veya istek güncelleştirilemiyor. Çok sayıda oluşturma veya güncelleştirme devam eden işlemleri aboneliği için "% ld".<br/><br/>Merhaba Hizmet meşgul birden çok işleme oluştur veya güncelleştir abonelik veya sunucu için istekleri. İstek şu anda kaynak iyileştirme için engellenir. Sorgu [sys.dm_operation_status](https://msdn.microsoft.com/library/dn270022.aspx) için bekleyen işlemler. Kasa Oluştur bekleyin veya güncelleştirme isteklerinin tamamlandığı veya bekleyen istekler birini silin ve isteğinizi daha sonra yeniden deneyin. |
| 49920 |16 |İsteği işleyemiyor. Devam eden çok fazla işlemleri aboneliği için "% ld".<br/><br/>Bu abonelik için birden çok istek işleme Hello Hizmet meşgul. İstek şu anda kaynak iyileştirme için engellenir. Sorgu [sys.dm_operation_status](https://msdn.microsoft.com/library/dn270022.aspx) işlem durumu. Bekleyen istekler kadar bekleyin, tam veya bekleyen istekler birini silin ve isteğinizi daha sonra yeniden deneyin. |
| 4221 |16 |Oturum açma tooread-ikincil 'HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING' toolong bekleme nedeniyle başarısız oldu. hello çoğaltma satır sürümleri hello çoğaltma dönüştürüldü yükleyen yürütülen işlemler için eksik olduğundan oturum açma için kullanılabilir değil. geri alma veya hello etkin işlem hello birincil çoğaltmadaki yürüten Hello sorun çözülebilir. Bu koşul oluşumlarını hello birincil uzun yazma hareketleri kaçınarak en aza indirgenebilir. |

## <a name="database-copy-errors"></a>Veritabanı kopyalama hataları
Aşağıdaki hatalar hello Azure SQL veritabanında bir veritabanı kopyalanırken karşılaşılabilir. Daha fazla bilgi için bkz. [Azure SQL Veritabanını kopyalama](sql-database-copy.md).

| Hata kodu | Önem Derecesi | Açıklama |
| ---:| ---:|:--- |
| 40635 |16 |İstemci IP adresi '%. & #x2a; ls' geçici olarak devre dışıdır. |
| 40637 |16 |Oluşturma veritabanı kopyalama şu anda devre dışı. |
| 40561 |16 |Veritabanı kopyalama başarısız oldu. Her iki hello kaynak veya hedef veritabanı yok. |
| 40562 |16 |Veritabanı kopyalama başarısız oldu. Merhaba kaynak veritabanı bırakılmış. |
| 40563 |16 |Veritabanı kopyalama başarısız oldu. Merhaba hedef veritabanı bırakılmış. |
| 40564 |16 |Veritabanı kopyasını tooan iç hata başarısız oldu. Lütfen hedef veritabanını bırakın ve yeniden deneyin. |
| 40565 |16 |Veritabanı kopyalama başarısız oldu. Aynı kaynak izin hello kopyadan 1'den fazla eşzamanlı veritabanı. Lütfen hedef veritabanını bırakın ve daha sonra yeniden deneyin. |
| 40566 |16 |Veritabanı kopyasını tooan iç hata başarısız oldu. Lütfen hedef veritabanını bırakın ve yeniden deneyin. |
| 40567 |16 |Veritabanı kopyasını tooan iç hata başarısız oldu. Lütfen hedef veritabanını bırakın ve yeniden deneyin. |
| 40568 |16 |Veritabanı kopyalama başarısız oldu. Kaynak veritabanı kullanılamıyor. Lütfen hedef veritabanını bırakın ve yeniden deneyin. |
| 40569 |16 |Veritabanı kopyalama başarısız oldu. Hedef veritabanı kullanılamıyor. Lütfen hedef veritabanını bırakın ve yeniden deneyin. |
| 40570 |16 |Veritabanı kopyasını tooan iç hata başarısız oldu. Lütfen hedef veritabanını bırakın ve daha sonra yeniden deneyin. |
| 40571 |16 |Veritabanı kopyasını tooan iç hata başarısız oldu. Lütfen hedef veritabanını bırakın ve daha sonra yeniden deneyin. |

## <a name="resource-governance-errors"></a>Kaynak İdaresi hataları
Aşağıdaki hatalar hello Azure SQL Database ile çalışırken aşırı kaynaklarının kullanımını nedeni değildir. Örneğin:

* Bir işlem için çok uzun süredir.
* Bir işlem çok fazla sayıda kilit tutuyor.
* Bir uygulama çok fazla bellek tükettikten.
* Bir uygulama çok tüketen `TempDb` alanı.

İlgili Konular:

* Daha ayrıntılı bilgi sağlanmıştır burada: [Azure SQL veritabanı kaynak sınırları](sql-database-resource-limits.md)

| Hata kodu | Önem Derecesi | Açıklama |
| ---:| ---:|:--- |
| 10928 |20 |Kaynak Kimliği: %d. Merhaba %s sınırı hello veritabanı için %d ve üst sınırına ulaşıldı. Daha fazla bilgi için bkz: [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637).<br/><br/>Merhaba kaynak kimliği hello sınırına hello kaynak gösterir. Çalışan iş parçacığı için kaynak kimliği hello = 1. Kaynak Kimliği oturumları için hello = 2.<br/><br/>*Not:* bu hata hakkında daha fazla bilgi ve nasıl tooresolve, bkz:<br/>• [Azure SQL veritabanı kaynak sınırları](sql-database-resource-limits.md). |
| 10929 |20 |Kaynak Kimliği: %d. Merhaba %s en az garantisi %d, üst sınır: %d ve hello hello veritabanı için geçerli kullanımı %d. Ancak, hello şu anda çok meşgul toosupport istekleri %d Bu veritabanı için büyük sunucusudur. Daha fazla bilgi için bkz: [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637). Aksi halde, lütfen daha sonra yeniden deneyin.<br/><br/>Merhaba kaynak kimliği hello sınırına hello kaynak gösterir. Çalışan iş parçacığı için kaynak kimliği hello = 1. Kaynak Kimliği oturumları için hello = 2.<br/><br/>*Not:* bu hata hakkında daha fazla bilgi ve nasıl tooresolve, bkz:<br/>• [Azure SQL veritabanı kaynak sınırları](sql-database-resource-limits.md). |
| 40544 |20 |Merhaba veritabanı boyut kotasına ulaştı. Verileri bölün veya silin, dizinleri bırakın veya olası çözümler için hello belgelerine başvurun. |
| 40549 |16 |Uzun süre çalışan işlem olduğundan oturum sonlandırıldı. İşleminiz kısaltmayı deneyin. |
| 40550 |16 |Bu çok fazla sayıda kilit aldığından hello oturum sonlandırıldı. Try okuma veya tek bir işlemde daha az sayıda satır değiştirme. |
| 40551 |16 |Merhaba oturum sonlandırıldı nedeniyle aşırı `TEMPDB` kullanımı. Sorgu tooreduce hello geçici tablo alanı kullanımını değiştirmeyi deneyin.<br/><br/>*İpucu:* geçici nesneler kullanıyorsanız, hello alandan tasarruf etmek `TEMPDB` artık hello oturumu tarafından gerekli sonra geçici nesneler bırakarak tarafından veritabanı. |
| 40552 |16 |Merhaba oturum aşırı işlem günlüğü alanı kullanımı nedeniyle sonlandırıldı. Tek bir işlemde daha az sayıda satır değiştirmeyi deneyin.<br/><br/>*İpucu:* hello kullanarak toplu eklemeler gerçekleştirirseniz `bcp.exe` yardımcı programı veya hello `System.Data.SqlClient.SqlBulkCopy` sınıfı, hello kullanmayı deneyin `-b batchsize` veya `BatchSize` seçenekleri toolimit hello satır sayısı her işlemde toohello sunucu kopyalanır. Merhaba ile bir dizini yeniden oluşturma, `ALTER INDEX` deyimi, hello kullanmayı deneyin `REBUILD WITH ONLINE = ON` seçeneği. |
| 40553 |16 |aşırı bellek kullanımı nedeniyle Hello oturum sonlandırıldı. Sorgu tooprocess değiştirmeyi daha az sayıda satır deneyin.<br/><br/>*İpucu:* hello sayısının azaltılması `ORDER BY` ve `GROUP BY` Transact-SQL kodunuzu işlemlerinde sorgunuzu hello bellek gereksinimlerini azaltır. |

## <a name="elastic-pool-errors"></a>Esnek Havuz Hataları
Aşağıdaki hatalar hello ilgili toocreating ve Elastics havuzlarını kullanarak ' dir.

| HataNumarası | ErrorSeverity | ErrorFormat | ErrorInserts | ErrorCause | ErrorCorrectiveAction |
|:--- |:--- |:--- |:--- |:--- |:--- |
| 1132 |EX_RESOURCE |Merhaba esnek havuz, depolama sınırına ulaştı. Merhaba depolama kullanımı hello esnek havuz için (%d) MB aşamaz. |MB cinsinden esnek havuz alanı sınırı. |Hello esnek havuz depolama sınırını Hello erişildiğinde toowrite veri tooa veritabanı çalışıyor. |Lütfen, depolama sınırına hello esnek havuzda mümkünse sipariş tooincrease artan hello Dtu göz önünde bulundurun, hello esnek havuz içindeki tek veritabanlarını tarafından kullanılan hello depolama azaltın veya hello esnek havuzdan veritabanı kaldırma. |
| 10929 |EX_USER |Merhaba %s en az garantisi %d, üst sınır: %d ve hello hello veritabanı için geçerli kullanımı %d. Ancak, hello şu anda çok meşgul toosupport istekleri %d Bu veritabanı için büyük sunucusudur. Bkz: [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637) Yardım için. Aksi halde, lütfen daha sonra yeniden deneyin. |Veritabanı başına minimum DTU; Veritabanı başına maksimum DTU |Merhaba esnek havuz denenen tooexceed hello havuz sınırı tüm veritabanları arasında eşzamanlı çalışan (istek) toplam sayısı hello. |Lütfen çalışan sınırına hello hello esnek havuzda mümkünse sipariş tooincrease Dtu'lar artırmayı deneyin veya veritabanlarını hello esnek havuzdan kaldırın. |
| 40844 |EX_USER |'%Ls' sunucusundaki '%ls' veritabanını bir esnek havuzdaki '%ls' sürümü veritabanıdır ve sürekli kopyalama ilişkisine sahip olamaz. |Veritabanı adı, veritabanı sürümü, sunucu adı |Esnek havuzdaki premium olmayan db için StartDatabaseCopy komutu verildi. |Çok yakında |
| 40857 |EX_USER |Esnek havuz için sunucusu bulunamadı: '%ls', esnek havuz adı: '%ls'. |Sunucu adı; Esnek havuz adı |Belirtilen esnek havuz hello belirtilen Server'da yok. |Lütfen geçerli esnek havuz adını belirtin. |
| 40858 |EX_USER |'%Ls' esnek havuzu zaten şu sunucuda: '%ls' |Esnek havuz adı, sunucu adı |Belirtilen esnek havuz hello belirtilen mantıksal sunucu zaten var. |Yeni bir esnek havuz adını belirtin. |
| 40859 |EX_USER |Esnek havuz hizmet Katmanı '%ls' desteklemez. |Esnek havuz hizmet katmanı |Belirtilen hizmet katmanı, esnek havuz sağlamak için desteklenmiyor. |Merhaba doğru sürümü belirtin ya da hizmet katmanı boş toouse hello varsayılan hizmet katmanı bırakın. |
| 40860 |EX_USER |Esnek havuz '%ls' ve hizmet hedefi '%ls' birleşimi geçersiz. |Esnek havuz adı; Hizmet düzeyi hedef adı |Esnek havuzu ve hizmet hedefi belirtilebilir birlikte yalnızca hizmet hedefi 'ElasticPool' belirtilmişse. |Lütfen doğru birleşimini esnek havuz ve hizmet hedefi belirtin. |
| 40861 |EX_USER |Merhaba veritabanı sürümü ' %. *ls olan hello esnek havuz katmanından farklı olamaz ' %.* ls'. |veritabanı sürümü, esnek havuz hizmet katmanı |Merhaba veritabanı sürümü hello esnek havuz katmanından farklı. |Lütfen hello esnek havuz katmanından farklı olan bir veritabanı sürümü belirtmeyin.  Bu hello veritabanı sürümü belirtilen toobe gerekmez unutmayın. |
| 40862 |EX_USER |Esnek havuz adının belirtilmesi gerekir hello esnek havuz hizmeti hedefi belirtildiyse smbiosguid'sinin. |None |Esnek havuz hizmeti hedefi bir esnek havuz benzersiz olarak tanımlamıyor. |Lütfen hello esnek havuz hizmeti hedefi kullanıyorsanız hello esnek havuz adı belirtin. |
| 40864 |EX_USER |Merhaba esnek havuz için Dtu'lar Hello en az olmalıdır (%d) Dtu'lar hizmet katmanı için ' %. * ls'. |Esnek havuz için Dtu'lar; Esnek havuz hizmet katmanı. |Merhaba alt sınırı aşağıda hello esnek havuz için Dtu'lar tooset hello çalışıyor. |Lütfen hello esnek havuz tooat hello Dtu'lar ayarı yeniden deneme en az hello alt sınırı. |
| 40865 |EX_USER |Merhaba esnek havuz için Dtu'lar Hello (%d) Dtu'lar hizmet katmanı için aşamaz ' %. * ls'. |Esnek havuz için Dtu'lar; Esnek havuz hizmet katmanı. |Merhaba sınırı üstünde hello esnek havuz için Dtu'lar tooset hello çalışıyor. |Lütfen hello esnek havuz toono hello Dtu'lar hello üst sınır değerinden ayarı yeniden deneyin. |
| 40867 |EX_USER |Merhaba veritabanı başına maksimum DTU olması gerekir en az (%d) hizmet katmanı için ' %. * ls'. |Veritabanı başına maksimum DTU; Esnek havuz hizmet katmanı |Tooset hello hello aşağıda veritabanı başına maksimum DTU çalışırken sınırı desteklenir. |Lütfen istenen hello ayarını destekler hello esnek havuz hizmet katmanı kullanmayı düşünün. |
| 40868 |EX_USER |Merhaba veritabanı başına maksimum DTU (%d) aşamaz hizmet katmanı için ' %. * ls'. |Veritabanı başına maksimum DTU; Esnek havuz hizmet katmanı. |Tooset hello hello ötesinde veritabanı başına maksimum DTU çalışırken sınırı desteklenir. |Lütfen istenen hello ayarını destekler hello esnek havuz hizmet katmanı kullanmayı düşünün. |
| 40870 |EX_USER |Merhaba veritabanı başına minimum DTU (%d) aşamaz hizmet katmanı için ' %. * ls'. |Veritabanı başına minimum DTU; Esnek havuz hizmet katmanı. |Merhaba ötesinde veritabanı başına minimum tooset hello DTU çalışırken sınırı desteklenir. |Lütfen istenen hello ayarını destekler hello esnek havuz hizmet katmanı kullanmayı düşünün. |
| 40873 |EX_USER |Merhaba veritabanı sayısı (%d) ve (%d) veritabanı başına minimum DTU hello Dtu'lar hello esnek havuzun (%d) aşamaz. |Esnek havuzdaki veritabanları sayı; Veritabanı başına minimum DTU; Esnek havuz Dtu. |Toospecify hello hello esnek havuz Dtu aşan hello esnek havuzdaki veritabanları için minimum DTU çalışılıyor. |Lütfen hello hello esnek havuzun Dtu'lar artırmayı veya hello veritabanı başına minimum DTU azaltın veya hello esnek havuzdaki veritabanları hello sayısını azaltın. |
| 40877 |EX_USER |Tüm veritabanları içermediği sürece bir esnek havuz silinemez. |None |Merhaba esnek havuzu bir veya daha fazla veritabanı içerir ve bu nedenle silinemez. |Lütfen Kaldır havuzundan hello esnek sipariş toodelete bu veritabanları. |
| 40881 |EX_USER |Merhaba esnek havuzu ' %. * ls, veritabanı sayısı sınırına ulaşıldı.  Merhaba esnek havuz için Hello veritabanı sayısı sınırına (%d) Dtu'ya sahip bir esnek havuz için (%d) aşamaz. |Esnek havuz adı; Esnek havuz veritabanı sayısı sınırını; kaynak havuzu için Dtu'lar e. |Toocreate çalışırken veya hello esnek havuzun hello veritabanı sayısı sınırına ulaşıldığında veritabanı tooelastic havuzu ekleyin. |Lütfen hello hello esnek havuzda mümkünse sipariş tooincrease Dtu'lar veritabanı sınırına artırmayı deneyin veya veritabanlarını hello esnek havuzdan kaldırın. |
| 40889 |EX_USER |Merhaba Dtu'lar veya hello esnek havuz depolama sınırı ' %. * ls olamaz azaltılabilir, yeterli depolama alanına veritabanları için sağlamayacağından. |Esnek havuz adı. |Toodecrease hello depolama sınırını hello esnek havuz depolama kullanım altında çalışıyor. |Lütfen hello depolama hello esnek havuzdaki tek tek veritabanlarının kullanımını azaltmayı deneyin veya Kaldır veritabanları sipariş tooreduce hello havuzundan kendi Dtu'lar ve depolama sınırı. |
| 40891 |EX_USER |Merhaba (%d) veritabanı başına minimum DTU hello Katmanı için maksimum veritabanı (%d) dtu'yu aşamaz. |Veritabanı başına minimum DTU; Veritabanı başına maksimum DTU. |Merhaba veritabanı başına maksimum DTU daha yüksek olan veritabanı başına minimum tooset hello DTU çalışılıyor. |Lütfen veritabanı başına minimum DTU hello hello veritabanı başına maksimum DTU aşmadığından emin olun. |
| TBD |EX_USER |Esnek havuzdaki tek bir veritabanının Hello depolama boyutu tarafından izin verilen en büyük boyut hello aşamaz ' %. * ls hizmet katmanı esnek havuz. |Esnek havuz hizmet katmanı |Merhaba veritabanı için en büyük boyutu Hello hello esnek havuz hizmet katmanı tarafından izin hello en fazla boyutu aşıyor. |Lütfen hello max hello esnek havuz hizmet katmanı tarafından izin verilen en büyük boyut hello hello sınırları içinde hello veritabanı boyutunu ayarlayın. |

İlgili Konular:

* [Bir esnek havuz (C#) oluşturma](sql-database-elastic-pool-manage-csharp.md) 
* [Bir esnek havuz (C#) yönetme](sql-database-elastic-pool-manage-csharp.md). 
* [Bir esnek havuz (PowerShell) oluşturma](sql-database-elastic-pool-manage-powershell.md) 
* [İzleme ve yönetme bir esnek havuz (PowerShell)](sql-database-elastic-pool-manage-powershell.md).

## <a name="general-errors"></a>Genel hataları
Aşağıdaki hatalar hello herhangi önceki kategorilere ayrılır değil.

| Hata kodu | Önem Derecesi | Açıklama |
| ---:| ---:|:--- |
| 15006 |16 |<AdministratorLogin>geçersiz karakterler içerdiğinden geçerli bir ad değil. |
| 18452 |14 |Oturum açma başarısız oldu. Merhaba oturum açma güvenilmeyen bir etki alanından ve Windows authentication.%. & #x2a; ile kullanılamaz ls (Windows oturumu açma desteklenmez SQL Server'ın bu sürümünde.) |
| 18456 |14 |Kullanıcı için oturum açma başarısız ' %. #x2a;ls'.%. & #x2a ls %. & #x2a; ls (Merhaba oturum açma kullanıcısı için başarısız oldu "%. & #x2a; ls". Merhaba parola değiştirme başarısız oldu. Oturum açma sırasında parola değiştirme bu SQL Server sürümünde desteklenmiyor.) |
| 18470 |14 |Kullanıcı için oturum açma başarısız '%. & #x2a; ls'. Neden: Merhaba disabled.%. & #x2a; hesabıdır ls |
| 40014 |16 |Birden çok veritabanı hello kullanılamaz aynı işlem. |
| 40054 |16 |Kümelenmiş dizini olmayan tablolar, SQL Server'ın bu sürümünde desteklenmez. Kümelenmiş bir dizin oluşturun ve yeniden deneyin. |
| 40133 |15 |Bu işlem, SQL Server'ın bu sürümünde desteklenmiyor. |
| 40506 |16 |Belirtilen SID bu SQL Server sürümü için geçersiz. |
| 40507 |16 |' %. & #x2a; ls'SQL Server'ın bu sürümünde parametrelerle çağrılacak olamaz. |
| 40508 |16 |USE deyiminin desteklenen tooswitch veritabanları arasında değil. Yeni bir bağlantı tooconnect tooa farklı veritabanı kullanın. |
| 40510 |16 |Deyimi '%. & #x2a; ls' SQL Server'ın bu sürümünde desteklenmiyor |
| 40511 |16 |Yerleşik işlevi '%. & #x2a; ls' SQL Server'ın bu sürümünde desteklenmiyor. |
| 40512 |16 |Kullanım dışı özelliği '%ls' SQL Server'ın bu sürümünde desteklenmiyor. |
| 40513 |16 |Sunucu değişkeni '%. & #x2a; ls' SQL Server'ın bu sürümünde desteklenmiyor. |
| 40514 |16 |'%ls' SQL Server'ın bu sürümünde desteklenmiyor. |
| 40515 |16 |Başvuru toodatabase ve/veya sunucu adı içinde '%. & #x2a; ls' SQL Server'ın bu sürümünde desteklenmiyor. |
| 40516 |16 |Genel geçici nesneler bu SQL Server sürümünde desteklenmiyor. |
| 40517 |16 |Anahtar sözcüğü veya deyim seçeneği '%. & #x2a; ls' SQL Server'ın bu sürümünde desteklenmiyor. |
| 40518 |16 |DBCC komutu '%. & #x2a; ls' SQL Server'ın bu sürümünde desteklenmiyor. |
| 40520 |16 |Güvenliği sağlanabilir sınıfı '% S_MSG' SQL Server'ın bu sürümünde desteklenmiyor. |
| 40521 |16 |Güvenliği sağlanabilir sınıfı '% S_MSG' hello sunucu kapsamındaki SQL Server'ın bu sürümünde desteklenmiyor. |
| 40522 |16 |Veritabanı asıl '%. & #x2a; ls' türü SQL Server'ın bu sürümünde desteklenmiyor. |
| 40523 |16 |'%. & #X2a; ls' örtük kullanıcı oluşturma, SQL Server'ın bu sürümünde desteklenmiyor. Açıkça hello kullanıcı kullanmadan önce oluşturun. |
| 40524 |16 |Veri türü '%. & #x2a; ls' SQL Server'ın bu sürümünde desteklenmiyor. |
| 40525 |16 |'%.Ls' ile SQL Server'ın bu sürümünde desteklenmiyor. |
| 40526 |16 |' %. & #x2a; ls satır kümesi sağlayıcısı bu SQL Server sürümünde desteklenmiyor. |
| 40527 |16 |Bağlantılı sunucular, SQL Server'ın bu sürümünde desteklenmez. |
| 40528 |16 |Kullanıcılar eşlenmiş toocertificates, asimetrik anahtarlar veya SQL Server'ın bu sürümünde Windows oturumları olamaz. |
| 40529 |16 |Yerleşik işlevi '%. & #x2a; ls' kimliğe bürünme bağlam, SQL Server'ın bu sürümünde desteklenmiyor. |
| 40532 |11 |Sunucu açamıyor "%. & #x2a; ls" Merhaba oturum açma tarafından istenen. Merhaba oturum açma başarısız oldu. |
| 40553 |16 |aşırı bellek kullanımı nedeniyle Hello oturum sonlandırıldı. Sorgu tooprocess değiştirmeyi daha az sayıda satır deneyin.<br/><br/>*Not:* hello sayısının azaltılması `ORDER BY` ve `GROUP BY` Transact-SQL kodunuzu işlemlerinde yardımcı sorgunuzu hello bellek gereksinimlerini azaltın. |
| 40604 |16 |Merhaba kota hello sunucusunun aşacağından CREATE/ALTER DATABASE verebilir. |
| 40606 |16 |Veritabanları ekleme SQL Server'ın bu sürümünde desteklenmiyor. |
| 40607 |16 |Windows oturum açma bilgileri, SQL Server'ın bu sürümünde desteklenmez. |
| 40611 |16 |Sunucuları tanımlanan en fazla 128 güvenlik duvarı kuralları olabilir. |
| 40614 |16 |Güvenlik duvarı kuralının başlangıç IP adresi bitiş IP adresini aşamaz. |
| 40615 |16 |Sunucu '{0}' hello oturum açma tarafından istenen açamıyor. İstemci IP adresiyle '{1}' tooaccess hello sunucu izin verilmiyor.  tooenable erişim hello SQL veritabanı Portal kullanın veya hello ana veritabanı toocreate bu IP adresi veya adres aralığı için bir güvenlik duvarı kuralı üzerinde sp_set_firewall_rule.  Yukarı bu değişikliğin tootake toofive dakika sürebilir. |
| 40617 |16 |ile başlayan güvenlik duvarı kuralı adı hello <rule name> çok uzun. En fazla uzunluk 128'dir. |
| 40618 |16 |Merhaba güvenlik duvarı kuralı adı boş olamaz. |
| 40620 |16 |Merhaba oturum açma kullanıcısı için başarısız oldu "%. & #x2a; ls". Merhaba parola değiştirme başarısız oldu. Oturum açma sırasında parola değiştirme bu SQL Server sürümünde desteklenmiyor. |
| 40627 |20 |Sunucu '{0}' ve veritabanı '{1}' işlemi devam ediyor. Yeniden denemeden önce birkaç dakika bekleyin. |
| 40630 |16 |Parola doğrulama başarısız oldu. Merhaba parola çok kısa olduğundan ilke gereksinimlerini karşılamıyor. |
| 40631 |16 |Belirttiğiniz hello parola çok uzun. Merhaba parola en fazla 128 karakter olmalıdır. |
| 40632 |16 |Parola doğrulama başarısız oldu. Merhaba parola yeterince karmaşık olmadığı için ilke gereksinimlerini karşılamıyor. |
| 40636 |16 |Ayrılmış veritabanı adı kullanamazsınız '%. & #x2a; ls' Bu işlemde. |
| 40638 |16 |Geçersiz abonelik kimliği < subscrıptıon-ID >. Abonelik yok. |
| 40639 |16 |İstek tooschema uymuyor: <schema error>. |
| 40640 |20 |Merhaba sunucu beklenmeyen bir özel durumla karşılaştı. |
| 40641 |16 |Merhaba belirtilen konum geçersiz. |
| 40642 |17 |Merhaba sunucu şu anda çok meşgul. Lütfen daha sonra tekrar deneyin. |
| 40643 |16 |Merhaba belirtilen x-ms-version üstbilgi değeri geçersiz. |
| 40644 |14 |Başarısız tooauthorize erişim toohello abonelik belirtilmiş. |
| 40645 |16 |ServerName <servername> boş veya null olamaz. Bunu yalnızca küçük harfler yapılabilir 'a'-'z', hello numaraları 0-9 ve hello tire. Merhaba tire değil sağlama veya hello adlarında izi. |
| 40646 |16 |Abonelik kimliği boş olamaz. |
| 40647 |16 |Abonelik < server SunucuAdı abonelik kimliği yok. |
| 40648 |17 |Çok fazla istek gerçekleştirildi. Lütfen daha sonra yeniden deneyin. |
| 40649 |16 |Geçersiz içerik türü belirtildi. Yalnızca application/xml desteklenir. |
| 40650 |16 |< Subscrıptıon-ID > abonelik yok veya hello işlem için hazır değil. |
| 40651 |16 |Merhaba abonelik < subscrıptıon-ID > devre dışı bırakıldığından toocreate server başarısız oldu. |
| 40652 |16 |Taşınamıyor veya sunucu oluşturulamıyor. Abonelik < subscrıptıon-ID > sunucu kotası aşılacak. |
| 40671 |17 |Merhaba ağ geçidi ve hello yönetim hizmeti arasındaki iletişim hatası. Lütfen daha sonra yeniden deneyin. |
| 40852 |16 |Veritabanı açılamıyor. ' %. *ls sunucusundaki ' %.* ls'hello oturum açma tarafından istenen. Access toohello veritabanını yalnızca güvenliği etkinleştirilmiş bağlantı dizesi kullanarak izin verilir. tooaccess bu veritabanı, bağlantı dizeleri toocontain Değiştir 'güvenli' hello Server FQDN - 'sunucu adı'.database.windows .net değiştirilmiş too'server adı da olmalıdır '.database. `secure`. windows.net. |
| 45168 |16 |Merhaba SQL Azure sistem yük altında ve bir üst sınır, tek bir sunucu için eş zamanlı DB CRUD işlemleri yerleştirerek (örn., veritabanı oluşturma). Merhaba hata iletisinde belirtilen hello sunucusu hello en fazla eşzamanlı bağlantı sayısını aştı. Daha sonra yeniden deneyin. |
| 45169 |16 |Merhaba SQL azure sistem yük altında ve bir eş zamanlı sunucu CRUD işlemleri için tek bir abonelik hello sayısının üst sınırını yerleştirme (örneğin, sunucu oluşturma). Merhaba abonelik hello hatada belirtilen ileti hello en fazla eşzamanlı bağlantı sayısını aştı ve hello istek reddedildi. Daha sonra yeniden deneyin. |

## <a name="related-links"></a>İlgili bağlantılar
* [Azure SQL veritabanı özellikleri](sql-database-features.md)
* [Azure SQL veritabanı kaynak sınırları](sql-database-resource-limits.md)

