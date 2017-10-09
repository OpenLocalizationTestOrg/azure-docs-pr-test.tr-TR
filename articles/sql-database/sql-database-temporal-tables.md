---
title: "aaaGetting zamana bağlı tablolarda Azure SQL veritabanı ile Başlarken | Microsoft Docs"
description: "Nasıl tooget zamana bağlı tablolarda Azure SQL veritabanı'nda kullanmaya öğrenin."
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: c8c0f232-0751-4a7f-a36e-67a0b29fa1b8
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 01/10/2017
ms.author: bonova
ms.openlocfilehash: 54f394b51df07aa2f9bb299f207e692171d23479
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a>Zamana bağlı tablolarda Azure SQL veritabanı ile çalışmaya başlama
Zamana bağlı tablolarda tootrack sağlayan bir Azure SQL veritabanı'nın yeni bir programlama özelliğidir ve özel kodlama için hello gerek kalmadan, verilerde yapılan değişiklikler tam geçmişini hello analiz edin. Böylece saklı bulguları yorumlanabilen zamana bağlı tablolarda veri yakından ilgili tootime bağlamı yalnızca hello belirli bir dönem içinde geçerli olarak tutun. Zamana bağlı tablolarda, bu özellik etkili zamana dayalı çözümleme ve veri evrimi alma ilişkin bilgiler sağlar.

## <a name="temporal-scenario"></a>Zamana bağlı senaryosu
Bu makalede, bir uygulama senaryosunda başlangıç adımları tooutilize zamana bağlı tablolarda gösterilmektedir. Tootrack kullanıcı etkinliği sıfırdan geliştirilen yeni bir Web sitesi ya da kullanıcı etkinliği analytics ile tooextend istediğiniz mevcut bir Web istediğinizi varsayalım. Bu basit örnekte, bir süre sırasında ziyaret ettiğiniz web sayfalarının hello sayısının yakalanan ve Azure SQL veritabanı üzerinde barındırılan hello Web sitesi veritabanında izlenen toobe gerektiren bir gösterge olduğunu varsayalım. kullanıcı etkinliği hello geçmiş çözümleme Hello amacı tooget girişleri tooredesign Web sitesidir ve hello ziyaretçiler için daha iyi deneyimi sağlamak.

Bu senaryo için Hello veritabanı modeli çok basit - kullanıcı etkinliği ölçüm bir tek tamsayı alanıyla temsil **PageVisited**ve hello kullanıcı profili temel bilgiler birlikte yakalanır. Ayrıca, temel saat analizi için her satır belirli bir kullanıcının belirli bir dönem içinde ziyaret edilen sayfalar hello sayısı temsil ettiği satırları her kullanıcı için bir dizi engelleneceği.

![Şema](./media/sql-database-temporal-tables/AzureTemporal1.png)

Neyse ki, tooput herhangi çaba, uygulama toomaintain gerekmez bu etkinliği bilgileri. Zamana bağlı tablolar ile bu işlem - Web sitesi tasarımı ve hello veri analizi kendisi hakkında daha fazla zaman toofocus sırasında tam esneklik sağlayan otomatik hale getirilmiştir. yalnızca bir şey toodo sahip tooensure Merhaba, **WebSiteInfo** tablo olarak yapılandırılmış [zamana bağlı sistem sürümlü](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0). Bu senaryoda Hello tam adımlar tooutilize zamana bağlı tablolarda aşağıda açıklanmıştır.

## <a name="step-1-configure-tables-as-temporal"></a>1. adım: tabloları zamana bağlı olarak yapılandırma
Yeni yazılım geliştirme başlangıç mı var olan uygulama yükseltme bağlı olarak, zamana bağlı tablolarda oluşturun veya var olanları zamana bağlı öznitelikleri ekleyerek değiştirin. Genel durumda senaryonuz iki bu seçeneklerin bir bileşimi olabilir. Bunlar gerçekleştirmek eylemini kullanarak [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS) [SQL Server veri Araçları](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) veya başka bir Transact-SQL geliştirme aracıdır.

> [!IMPORTANT]
> Her zaman hello kullanmanız önerilir Management Studio tooremain en son sürümünü Azure ve SQL veritabanı güncelleştirmeleri tooMicrosoft ile eşitlenir. [SQL Server Management Studio’yu güncelleyin](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

### <a name="create-new-table"></a>Yeni Tablo Oluştur
SSMS Nesne Gezgini tooopen hello sorgu Düzenleyicisi'nde bağlam menüsü öğesini "Yeni sistem sürümlü tablo" ile bir zamana bağlı tablo şablonu komut dosyası kullanın ve ardından "Değerleri için şablon parametrelerini belirt" (Ctrl + Shift + M) toopopulate hello şablonu kullanabilirsiniz:

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

SSDT içinde yeni öğeleri toohello veritabanı projesi eklerken "(sistem sürümü tutulan) zamana bağlı tablo" Şablon seçtiniz. Açık Tablo Tasarımcısı ve etkinleştirme, tooeasily belirtin Tablo düzeni hello olduğunu:

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

Ayrıca bir oluşturma zamana bağlı tablo hello Transact-SQL deyimlerini doğrudan belirterek hello aşağıdaki örnekte gösterildiği gibi erişebilirsiniz. Her zamana bağlı tabloda zorunlu öğeleri Hello hello süre tanımının ve geçmiş satır sürümleri depolayacak bir başvuru tooanother kullanıcı tablosu ile Merhaba system_versıonıng yan tümcesini olduğuna dikkat edin:

````
CREATE TABLE WebsiteUserInfo 
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED 
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL 
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
````

Sistem sürümü tutulan zamana bağlı tablo oluşturduğunuzda, geçmiş tablosu hello varsayılan yapılandırması ile birlikte gelen hello otomatik olarak oluşturulur. Merhaba varsayılan geçmiş tablosu sayfası sıkıştırma ile Merhaba dönem sütunlarında (end, start) bir kümelenmiş B-Ağacı dizini içerir. Bu yapılandırma en iyi zamana bağlı tablolarda kullanılan senaryoları hello çoğunluğu için özellikle de [verileri denetleme](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0). 

Merhaba depolama hello geçmiş tablosu için kümelenmiş columnstore dizini seçimdir şekilde bu özel durumda biz tooperform zamana dayalı eğilim analizi üzerinden uzun bir veri geçmişini ve büyük veri kümeleriyle hedefleyin. Kümelenmiş columnstore çok iyi sıkıştırma ve analitik sorguları için performans sağlar. Esneklik tooconfigure dizinleri hello geçerli ve zamana bağlı tablolarda tamamen bağımsız olarak hello zamana bağlı tablolar verin. 

> [!NOTE]
> Columnstore dizinleri yalnızca hello premium hizmet katmanında kullanılabilir.
>

komut dosyası izleyen hello varsayılan dizini geçmiş tablosu değişen toohello kümelenmiş columnstore nasıl olabilir gösterir:

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

Geçmiş tablosu bir alt düğüm olarak görüntülendiği sırada zamana bağlı tablolarda hello Nesne Gezgini daha kolay tanımlama için hello belirli simgesiyle gösterilir.

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a>Var olan tablo tootemporal alter
Şimdi hangi hello WebsiteUserInfo tablo zaten var, ancak tasarlanmış tookeep değişikliklerin geçmişini değildi hello alternatif senaryo kapsar. Bu durumda, yalnızca hello var olan tablo toobecome hello örnek aşağıdaki gösterildiği gibi zamana bağlı genişletebilirsiniz:

````
ALTER TABLE WebsiteUserInfo 
ADD 
    ValidFrom datetime2 (0) GENERATED ALWAYS AS ROW START HIDDEN  
        constraint DF_ValidFrom DEFAULT DATEADD(SECOND, -1, SYSUTCDATETIME())
    , ValidTo datetime2 (0)  GENERATED ALWAYS AS ROW END HIDDEN   
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo); 

ALTER TABLE WebsiteUserInfo  
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

## <a name="step-2-run-your-workload-regularly"></a>2. adım: İş yükünüzün düzenli olarak çalıştırma
zamana bağlı tablolarda Hello ana avantajı, değil toochange gerekir veya herhangi bir şekilde tooperform değişiklik izleme, Web sitenizi ayarlama olması. Değişiklikler, verilerinizde gerçekleştirilecek her zaman oluşturduktan sonra zamana bağlı tablolarda saydam önceki satır sürümleri kalıcı olmasını sağlar. 

Sipariş tooleverage otomatik değişiklik izleme, bu belirli bir senaryo için şirketinizdeki yalnızca sütun güncelleştirme **PagesVisited** kullanıcı hello Web sitesinde her/his oturumu sona erdiğinde her zaman:

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

Güncelleştirme sorgusu hello toonotice tooknow hello tam zaman hello gerçek işlemi oluştuğunda veya geçmiş verileri gelecekteki analize korunacak nasıl gerek duymaz önemlidir. Her iki yönlerini hello Azure SQL veritabanı tarafından otomatik olarak işlenir. Merhaba Aşağıdaki diyagramda geçmiş verileri üzerindeki her bir güncelleştirme nasıl üretiliyor gösterilmektedir.

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a>3. adım: geçmiş veri çözümlemesi gerçekleştirme
Zamana bağlı sistem sürümü oluşturma etkin olduğunda, geçmiş verileri çözümleme, uzakta yalnızca bir sorgu sunulmuştur. Bu makalede, biz ortak analiz - toolearn senaryosu birkaç örnek tüm ayrıntıları sağlayın, hello ile sunulan çeşitli seçenekleriniz keşfetme [FOR system_tıme](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) yan tümcesi.

itibariyle bir saatten önce ziyaret edilen web sayfalarını hello sayısına göre sıralanmış toosee hello ilk 10 kullanıcılar bu sorguyu çalıştırın:

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

Bu sorgu kolayca değiştirebilirsiniz tooanalyze hello sitesini ziyaret gün önce itibariyle bir ay önce veya hello geçmiş herhangi bir noktada istediğiniz.

önceki gün tooperform temel istatistiksel çözümleme hello için aşağıdaki örneğine hello kullanın:

````
DECLARE @twoDaysAgo datetime2 = DATEADD(DAY, -2, SYSUTCDATETIME());
DECLARE @aDayAgo datetime2 = DATEADD(DAY, -1, SYSUTCDATETIME());

SELECT UserID, SUM (PagesVisited) as TotalVisitedPages, AVG (PagesVisited) as AverageVisitedPages,
MAX (PagesVisited) AS MaxVisitedPages, MIN (PagesVisited) AS MinVisitedPages,
STDEV (PagesVisited) as StDevViistedPages
FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME BETWEEN @twoDaysAgo AND @aDayAgo
GROUP BY UserId
````

toosearch belirli bir kullanıcının bir süre, kullanım hello KAPSANAN yan tümcesi içindeki etkinlikler için:

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

Eğilimleri ve kullanım düzenlerini sezgisel bir yolla kolayca gösterebilirsiniz gibi grafik görselleştirme zamana bağlı sorguları için özellikle kullanışlıdır:

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a>Tablo şemasını gelişen
Genellikle, uygulama geliştirme yaparken toochange hello zamana bağlı tablo şemasını gerekir. Yalnızca normal ALTER TABLE deyimleri çalıştırın ve Azure SQL veritabanı uygun şekilde değişiklikleri toohello geçmiş tablosu yayılır. Merhaba aşağıdaki betiği izleme için ek öznitelik nasıl ekleyebileceğiniz gösterilmektedir:

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

Benzer şekilde, iş yükünüzü etkinken sütun tanımı değiştirebilirsiniz:

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

Son olarak, artık ihtiyacınız olmayan bir sütun kaldırabilirsiniz.

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

Alternatif olarak, en son kullanın [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange zamana bağlı tablo şeması bağlı toohello veritabanı (çevrimiçi mod) durumdayken veya hello veritabanı projesi (Çevrimdışı mod) bir parçası olarak.

## <a name="controlling-retention-of-historical-data"></a>Geçmiş verilerin bekletilmesini denetleme
Sistem sürümü tutulan zamana bağlı tablolarda ile Merhaba geçmiş tablosu normal tablolardaki'birden fazla hello veritabanı boyutunu artırabilir. Büyük ve sürekli büyüyen geçmiş tablosu, hem toopure depolama maliyetleri yanı sıra bir performans etkileyici son zamana bağlı sorgulama vergi bir sorun olabilir. Bu nedenle, hello geçmiş tablosundaki verileri yönetmek için bir veri bekletme ilkesi geliştirme planlama ve her zamana bağlı tablo hello yaşam döngüsü yönetiminden önemli bir özelliği olan. Azure SQL veritabanı ile yaklaşımlar hello zamana bağlı tabloda geçmiş verileri yönetmek için aşağıdaki hello vardır:

* [Tablo bölümleme](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [Özel temizleme betiğini](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a>Sonraki adımlar
Zamana bağlı tablolarda hakkında ayrıntılı bilgi için kullanıma [MSDN belgelerine](https://msdn.microsoft.com/library/dn935015.aspx).
Ziyaret kanal 9 toohear bir [gerçek müşteri zamana bağlı implemenation başarı Öykü](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) ve izleme bir [zamana bağlı tanıtım canlı](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).

