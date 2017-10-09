---
title: "aaaSync verileri (Önizleme) | Microsoft Docs"
description: "Azure SQL veri eşitleme (Önizleme) bu genel bakış sunar."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: douglasl
ms.openlocfilehash: d5b2bbd6a502ba94dba7fb309a6583d2d95cc1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sync-data-across-multiple-cloud-and-on-premises-databases-with-sql-data-sync"></a>SQL veri eşitleme ile birden çok Bulut ve şirket içi veritabanları arasında eşitleme verileri

SQL veri eşitleme hello veri birden çok SQL veritabanları ve SQL Server örnekleri arasında çift yönlü Seç eşitlemenize olanak sağlayan Azure SQL veritabanı üzerine kurulu bir hizmettir.

Veri Eşitleme eşitleme grubu hello kavramı temel alır. Bir eşitleme grubu toosynchronize istediğiniz veritabanlarının bir gruptur.

Eşitleme grubu hello aşağıdaki özelliklere sahiptir:

-   Merhaba **eşitleme şema** hangi verilerin eşitleneceğini açıklar.

-   Merhaba **eşitleme yönü** çift yönlü olabilir veya yalnızca bir yöne akabilir. Diğer bir deyişle, eşitleme yönü olabilir hello *Hub tooMember* veya *üye tooHub*, veya her ikisini de.

-   Merhaba **eşitleme aralığı** ne sıklıkla eşitleme gerçekleşir.

-   Merhaba **çakışma çözüm İlkesi** olabilir bir grubu düzeyi ilkesi *Hub WINS* veya *üye WINS*.

Veri Eşitleme bir hub ve bağlı bileşen topolojisi toosynchronize verileri kullanır. Merhaba veritabanlarından birini hello grubunda hello Hub veritabanı tanımlarsınız. üye veritabanları Hello rest hello veritabanlarının var. Eşitleme yalnızca hello Hub ve tek tek üyeleri arasında oluşur.
-   Merhaba **Hub veritabanı** bir Azure SQL veritabanı olmalıdır.
-   Merhaba **üye veritabanları** SQL veritabanları, şirket içi SQL Server veritabanları veya Azure virtual machines'de SQL Server örnekleri olabilir.
-   Merhaba **eşitleme veritabanı** veri eşitleme. hello eşitleme veritabanı toobe hello bulunan bir Azure SQL veritabanına sahip hello meta veri ve günlük içermektedir hello Hub veritabanı ile aynı bölgeye. Merhaba eşitleme veritabanı müşteri oluşturuldu ve müşteri ait olur.

> [!NOTE]
> Üzerinde bir şirket içi veritabanı kullanıyorsanız, çok sahip[bir yerel Aracısı yapılandırın.](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-sql-data-sync)

![Veritabanları arasında eşitleme verileri](media/sql-database-sync-data/sync-data-overview.png)

## <a name="when-toouse-data-sync"></a>Toouse veri eşitleme yaparken

Veri eşitleme veri birkaç Azure SQL veritabanlarını veya SQL Server veritabanları arasında toodate tutulan toobe gereken durumlarda yararlıdır. Veri eşitlemesi için hello ana kullanım örnekleri şunlardır:

-   **Karma veri eşitleme:** veri eşitleme ile şirket içi veritabanları ve Azure SQL veritabanlarını tooenable karma uygulamalar arasında eşitlenen verileri tutabilirsiniz. Bu özellik taşıma toohello bulut dikkate ve tooput istediğiniz toocustomers itiraz etmek bazı Azure uygulamalarında.

-   **Dağıtılmış uygulamalar:** çoğu durumda, yararlı tooseparate farklı iş yükleri farklı veritabanları arasında değil. Örneğin, bir üretim veritabanınız var ancak raporlama toorun ya da bu veriler üzerinde analiz iş yükü de gerekir, bu yararlı toohave bu ek iş yükü için ikinci bir veritabanı olur. Bu yaklaşım, üretim iş yükünü hello performans etkisini en aza indirir. Bu iki veritabanı eşitlenmiş veri eşitleme tookeep kullanabilirsiniz.

-   **Genel olarak dağıtılmış uygulamalar:** birçok işletme birkaç bölgeler ve hatta bazı ülkelerde span. toominimize ağ gecikmesi, verilerinizi bir bölgede kapatmak iyi toohave olan tooyou. Veri Eşitleme ile eşitlenen Merhaba Dünya bölgelerdeki veritabanlarını kolayca tutabilirsiniz.

Veri Eşitleme senaryoları aşağıdaki Merhaba öneririz yok:

-   Olağanüstü Durum Kurtarma

-   Ölçek okuma

-   ETL (OLTP tooOLAP)

-   Şirket içi SQL Server tooAzure SQL veritabanı geçiş

## <a name="how-does-data-sync-work"></a>Veri Eşitleme nasıl çalışır? 

-   **Veri değişiklikleri izleme:** veri eşitleme Ekle kullanarak değişiklikleri izler, güncelleştirme ve Tetikleyicileri silin. Merhaba değişiklikleri hello kullanıcı veritabanı taraftaki tabloda kaydedilir.

-   **Veri eşitleme:** veri eşitleme bir Hub ve bağlı bileşen modeli tasarlanmıştır. Merhaba Hub her üyesiyle ayrı ayrı eşitlenir. Merhaba Hub değişikliklerden indirilen toohello üye ve ardından değişiklikleri hello üyeden karşıya yüklenen toohello Hub.

-   **Çakışmaları giderme:** veri eşitleme çakışması çözümleme için iki seçenek sunar *Hub WINS* veya *üye WINS*.
    -   Seçerseniz *Hub WINS*, hello hub hello değişiklikleri her zaman hello üyesinde değişikliklerin üzerine yaz.
    -   Seçerseniz *üye WINS*, hello hello üye üzerine yaz değişiklikleri hello hub'ında yapılan değişiklikler. Birden fazla üye ise, hangi üye eşitlenir hello son değer bağlıdır.

## <a name="limitations-and-considerations"></a>Sınırlamalar ve ilgili önemli noktalar

### <a name="performance-impact"></a>Performans etkisi
Veri Eşitleme kullanır Ekle, Güncelleştir ve Tetikleyicileri tootrack değişiklikleri silin. Merhaba kullanıcı veritabanında değişiklik izleme yan tablolar oluşturur. Bu değişiklik izleme etkinlikleri veritabanının yükünüzü etkiler. Hizmet katmanı değerlendirmek ve gerekirse yükseltin.

### <a name="eventual-consistency"></a>Nihai tutarlılık
Veri Eşitleme tetikleyici tabanlı olduğundan, işlem tutarlılığı garanti edilmez. Microsoft, tüm değişiklikler sonunda yapılır ve veri eşitleme veri kaybına neden olmaz garanti eder.

### <a name="unsupported-data-types"></a>Desteklenmeyen veri türleri

-   FILESTREAM

-   SQL/CLR UDT

-   XMLSchemaCollection (desteklenen XML)

-   İmleç, zaman damgası, HierarchyId

### <a name="requirements"></a>Gereksinimler

-   Her tablonun birincil anahtarı olmalıdır.

-   Bir tabloda hello birincil anahtarı olmayan bir kimlik sütunu bulunamaz.

-   Nesne (veritabanları, tablolar ve sütunlar) Hello adlarını hello yazdırılabilir karakterleri nokta (.), köşeli ayraç ([]) içeremez ya da sağ kare köşeli ayraç (]).

### <a name="limitations-on-service-and-database-dimensions"></a>Hizmet ve veritabanı boyutları sınırlamalar

|                                                                 |                        |                             |
|-----------------------------------------------------------------|------------------------|-----------------------------|
| **Boyutlar**                                                      | **Sınırı**              | **Geçici çözüm**              |
| Eşitleme grubu sayısı için herhangi bir veritabanı ait olabilir.       | 5                      |                             |
| Bir tek eşitleme grubundaki uç noktaları sayısı              | 30                     | Birden çok eşitleme grupları oluşturma |
| Bir tek eşitleme grubundaki şirket içi uç noktaları sayısı üst sınırı. | 5                      | Birden çok eşitleme grupları oluşturma |
| Veritabanı, tablo, şema ve sütun adları                       | ad başına 50 karakter |                             |
| Bir eşitleme grubundaki tablolar                                          | 500                    | Birden çok eşitleme grupları oluşturma |
| Bir eşitleme grubundaki bir tablodaki sütunlar                              | 1000                   |                             |
| Bir tabloda veri satır boyutu                                        | 24 mb                  |                             |
| Minimum eşitleme aralığı                                           | 5 dakika              |                             |

## <a name="common-questions"></a>Sık sorulan sorular

### <a name="how-frequently-can-data-sync-synchronize-my-data"></a>Veri Eşitleme verilerimi ne sıklıkta eşitleyebilirsiniz? 
Merhaba en az beş dakikada sıklığıdır.

### <a name="can-i-use-data-sync-toosync-between-sql-server-on-premises-databases-only"></a>Şirket içi veritabanları yalnızca SQL Server arasında veri eşitlemeye toosync kullanabilir miyim? 
Doğrudan yönetilemez. SQL Server içi veritabanları arasında dolaylı olarak, ancak Azure Hub veritabanı oluşturma ve hello şirket içi veritabanları toohello eşitleme grubu ekleme eşitleyebilirsiniz.
   
### <a name="can-i-use-data-sync-tooseed-data-from-my-production-database-tooan-empty-database-and-then-keep-them-synchronized"></a>I veri eşitleme tooseed veri my üretim veritabanı tooan boş veritabanından ve kullanabileceğiniz bunları eşitlenmiş tut? 
Evet. Merhaba şema hello özgün komut dosyası oluşturularak hello yeni veritabanında el ile oluşturun. Merhaba şema oluşturduktan sonra hello tabloları tooa eşitleme grubu toocopy hello veri eklemek ve eşitlenen saklayın.

### <a name="why-do-i-see-tables-that-i-did-not-create"></a>Oluşturulamadı tabloları neden görüyor musunuz?  
Veri Eşitleme yan tablolar değişiklik izleme, veritabanınızdaki oluşturur. Bunları silmeyin veya veri eşitleme çalışmayı durdurur.
   
### <a name="i-got-an-error-message-that-said-cannot-insert-hello-value-null-into-hello-column-column-column-does-not-allow-nulls-what-does-this-mean-and-how-can-i-fix-hello-error"></a>Başka bir deyişle hata iletisi aldım "hello değeri NULL hello sütununa INSERT yapılamıyor \<sütun\>. Sütun null değerlere izin vermiyor." Bu ne anlama geliyor ve nasıl hello hata düzeltebilirsiniz? 
Bu hata iletisini hello iki aşağıdaki sorunlardan biriyle gösterir:
1.  Bir birincil anahtar olmayan bir tablo olabilir. toofix Bu sorun, bir birincil anahtar tooall hello tabloları eklemek eşitleniyor.
2.  CREATE INDEX deyiminde WHERE yan tümcesi olabilir. Eşitleme, bu durum işlemez. toofix bu sorunu hello WHERE yan tümcesini kaldırın veya el ile Merhaba tooall veritabanları değişiklik. 
 
### <a name="how-does-data-sync-handle-circular-references-that-is-when-hello-same-data-is-synced-in-multiple-sync-groups-and-keeps-changing-as-a-result"></a>Veri Eşitleme döngüsel başvurulara nasıl işler? Diğer bir deyişle, ne zaman hello aynı verileri birden çok eşitleme gruplarında eşitlenen ve sonuç olarak değiştirerek tutar?
Veri Eşitleme döngüsel başvurulara işleyemez. Emin tooavoid olması bunları. 

## <a name="next-steps"></a>Sonraki adımlar

SQL veri eşitleme hakkında daha fazla bilgi için bkz:

-   [SQL veri eşitleme ile çalışmaya başlama](sql-database-get-started-sql-data-sync.md)

-   Göster PowerShell örnekleri tamamlamak tooconfigure SQL veri eşitlemeyi nasıl:
    -   [Birden çok Azure SQL veritabanı arasında PowerShell toosync kullanın](scripts/sql-database-sync-data-between-sql-databases.md)
    -   [Bir Azure SQL Database ve SQL Server içi veritabanı arasında PowerShell toosync kullanın](scripts/sql-database-sync-data-between-azure-onprem.md)

-   [Merhaba tam SQL veri eşitleme teknik belgeler indirin](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)

-   [Merhaba SQL veri eşitleme REST API belgelerini indirebilirsiniz](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)

SQL veritabanı hakkında daha fazla bilgi için bkz:

-   [SQL veritabanı genel bakış](sql-database-technical-overview.md)

-   [Veritabanı yaşam döngüsü yönetimi](https://msdn.microsoft.com/library/jj907294.aspx)
