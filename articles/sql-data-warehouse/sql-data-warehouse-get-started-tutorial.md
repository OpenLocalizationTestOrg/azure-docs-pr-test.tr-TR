---
title: "SQL veri ambarı - aaaAzure Başlarken Öğreticisi | Microsoft Docs"
description: "Bu öğretici nasıl öğretilmektedir tooprovision ve yük verileri Azure SQL veri ambarında. Ayrıca hello temelleri ölçeklendirme, duraklatma ve ayarlama hakkında bilgi edineceksiniz."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a>SQL Veri Ambarı'nı kullanmaya başlayın

Bu öğreticide gösterilmiştir nasıl tooprovision ve yük verileri Azure SQL veri ambarında. Ayrıca hello temelleri ölçeklendirme, duraklatma ve ayarlama hakkında bilgi edineceksiniz. İşlemi tamamladığınızda, hazır tooquery olması ve veri ambarınız keşfedin.

**Zaman toocomplete tahmini:** hello önkoşulları karşıladığınızı sonra yaklaşık 30 dakika toocomplete geçen örnek kod ile uçtan uca öğretici budur. 

## <a name="prerequisites"></a>Ön koşullar

Başlangıç Öğreticisi SQL veri ambarı temel kavramları hakkında bilgi sahibi olduğunu varsayar. Bir tanıtım gerekirse bkz. [SQL Veri Ambarı nedir?](sql-data-warehouse-overview-what-is.md) 

### <a name="sign-up-for-microsoft-azure"></a>Microsoft Azure’a kaydolun
Zaten bir Microsoft Azure hesabınız yoksa, bu hizmet için bir toouse toosign gerekir. Zaten bir hesabınız varsa, bu adımı geçebilirsiniz. 

1. Toohello hesabı sayfalarında gezinmek [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)
2. Ücretsiz bir Azure hesabı oluşturun veya bir hesap satın alın.
3. Merhaba yönergeleri izleyin

### <a name="install-appropriate-sql-client-drivers-and-tools"></a>Uygun SQL istemci sürücülerini ve araçlarını yükleyin

Çoğu SQL istemci araçları JDBC, ODBC veya ADO.NET kullanarak tooSQL veri ambarına bağlanabilir. Toohello çok sayıda SQL Data Warehouse destekleyen T-SQL özelliklerini, bazı istemci uygulamaları ile SQL veri ambarı tamamen uyumlu değildir.

Bir Windows işletim sistemi çalıştırıyorsanız [Visual Studio] veya [SQL Server Management Studio] kullanmanız önerilir.

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a>SQL Data Warehouse oluşturma

SQL Veri Ambarı, yüksek düzeyde paralel işleme için tasarlanmış özel bir veritabanı türüdür. Merhaba veritabanı birden çok düğümüne dağıtılmış ve paralel sorgular işler. SQL veri ambarı tüm hello düğümleri hello etkinliklerini düzenler bir denetim düğümü vardır. Merhaba düğümlerin kendilerini SQL veritabanı toomanage verilerinizi kullanın.  

> [!NOTE]
> SQL Veri Ambarı'nın oluşturulması ek hizmet ücretlerinin alınmasına neden olabilir.  Ayrıntılı bilgi için bkz. [SQL Veri Ambarı fiyatlandırması](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).
>

### <a name="create-a-data-warehouse"></a>Veri ambarı oluşturma

1. Merhaba içine oturum [Azure portal](https://portal.azure.com).
2. **Yeni** > **Veritabanları** > **SQL Veri Ambarı** öğelerine tıklayın.

    ![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)

3. Dağıtım ayrıntılarını doldurun

    **Veritabanı Adı**: İstediğiniz bir adı seçin. Birden çok veri ambarlarında varsa adları dahil hello bölge, ortam, örneğin gibi ayrıntıları önerilir *westus 1 test mydw*.

    **Abonelik**: Azure aboneliğiniz

    **Kaynak Grubu**: Bir kaynak grubu oluşturun veya mevcut bir kaynak grubunu kullanın.
    > [!NOTE]
    > Kaynak grupları, kapsam erişim denetimi ve şablonlu dağıtım gibi kaynak yönetimi için kullanışlıdır. Azure kaynak grupları ve en iyi uygulamalar hakkında daha fazla bilgiyi [burada](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) bulabilirsiniz

    **Kaynak**: Boş Veritabanı

    **Sunucu**: oluşturduğunuz Select hello sunucu [önkoşulları].

    **Harmanlama**: hello varsayılan harmanlama sql_latin1_general_cp1_cı_as bırakın.

    **Performans seçin**: hello standart 400DWU ile başlayan öneririz.

4. Seçin **PIN toodashboard** ![PIN tooDashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)

5. Arkanıza yaslanın ve, veri ambarı toodeploy için bekleyin! Birkaç dakika için bu işlemi tootake normaldir. veri ambarınız hazır toouse olduğunda hello portal size bildirir. 

## <a name="connect-toosql-data-warehouse"></a>TooSQL veri ambarına bağlanma

Bu öğretici, SQL Server Management Studio (SSMS) tooconnect toohello veri ambarı kullanır. Bu desteklenen bağlayıcılar tooSQL veri ambarına bağlanabilir: ADO.NET, JDBC, ODBC ve PHP. Microsoft tarafından desteklenmeyen araçlar için işlevselliğin sınırlı olabileceğini unutmayın.


### <a name="get-connection-information"></a>Bağlantı bilgilerini alma

tooconnect tooyour veri ambarı, gereksinim duyduğunuz hello oluşturduğunuz mantıksal SQL sunucusu üzerinden tooconnect [önkoşulları].

1. Veri ambarınız hello Pano veya kaynaklarınız için bu aramada seçin.

    ![SQL Veri Ambarı Panosu](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. Merhaba mantıksal SQL sunucusu için tam ad Hello bulun.

    ![Sunucu Adını seçin](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. SSMS açıp Nesne Gezgini tooconnect toothis sunucusu oluşturduğunuz hello server yönetici kimlik bilgileriyle kullanmak [önkoşulları]

    ![SSMS ile bağlanma](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

Tüm kalırsa doğru artık bağlı tooyour mantıksal SQL sunucusu olması gerekir. Sunucu Yöneticisi hello gibi oturum bu yana hello ana veritabanı da dahil, hello sunucu tarafından barındırılan tooany veritabanının bağlanabilir. 

Yalnızca bir sunucu yönetici hesabı ve hello herhangi bir kullanıcı çoğu ayrıcalıklarına sahiptir. Dikkatli olun değil tooallow kuruluş tooknow hello Yönetici parolanızı çok fazla kişilere. 

Bir Azure active directory yönetici hesabına da sahip olabilirsiniz. Merhaba ayrıntıları buraya sunuyoruz yok. Azure Active Directory kimlik doğrulaması kullanma hakkında daha fazla toolearn istiyorsanız, bkz: [Azure AD kimlik doğrulaması](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

Ardından, ek oturumlar ve kullanıcılar oluşturma hakkında bilgi verilir.


## <a name="create-a-database-user"></a>Veritabanı kullanıcısı oluşturma

Bu adımda, bir kullanıcı hesabı tooaccess veri ambarınız oluşturun. Ayrıca toogive o kullanıcı hello özelliği toorun büyük miktarda bellek ve CPU kaynaklarını ile nasıl sorgular gösteriyoruz.

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a>Kaynakları tooqueries ayırma için kaynak sınıfları ile ilgili notlar

- tookeep verilerinizi güvenli, üretim veritabanlarınızı hello server yönetim toorun sorguları kullanmayın. Merhaba herhangi bir kullanıcı çoğu ayrıcalıklarına sahip ve tooperform kullanarak kullanıcı verilerine operations yerleştirir verileriniz risk altında. Hello Sunucu Yöneticisi tooperform yönetim işlemlerini tasarlanmıştır olduğundan, ayrıca, dosya işlemleri bellek ve CPU kaynaklarını yalnızca küçük bir ayırma ile çalışır. 

- SQL veri ambarı adlı kaynak sınıfları, bellek, CPU kaynaklarını ve eşzamanlılık yuvaları toousers farklı miktarlarda tooallocate önceden tanımlanmış veritabanı rollerini kullanır. Her kullanıcı tooa küçük, Orta, büyük veya çok büyük bir kaynak sınıfı ait olabilir. Merhaba kullanıcının kaynak sınıfı hello kaynakları hello kullanıcının sahip toorun sorguları belirler ve yükleme işlemleri.

- En iyi veri sıkıştırma için hello kullanıcı tooload büyük veya çok büyük kaynak ayırma gerekebilir. Kaynak sınıfları hakkında daha fazla bilgiyi [burada](./sql-data-warehouse-develop-concurrency.md#resource-classes) bulabilirsiniz:

### <a name="create-an-account-that-can-control-a-database"></a>Veritabanını denetleyebilen bir hesap oluşturma

Sunucu Yöneticisi Merhaba, oturum açmış olduğunuz olduğundan izinleri toocreate oturumları ve kullanıcıları sahip.

1. SSMS veya başka bir sorgu istemcisini kullanarak **ana** için yeni bir sorgu açın.

    ![Asıl’da Yeni Sorgu](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Asıl1’de Yeni Sorgu](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. Merhaba sorgu penceresinde, bu T-SQL komut toocreate MedRCLogin adlı oturum açma ve kullanıcı LoadingUser adlı çalıştırın. Bu oturum açma toohello mantıksal SQL sunucusuna bağlanabilir.

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. Şimdi hello sorgulama *SQL Data Warehouse veritabanı*, temel bir veritabanı kullanıcısı oluşturmalıdır hello tooaccess oluşturulan oturum açma ve hello veritabanı işlemleri.

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. Merhaba veritabanı kullanıcı denetimi izinleri toohello veritabanı NYT adlı verin. 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > Veritabanı adınız kısa çizgi varsa, emin toowrap olması köşeli ayraçlar içinde! 
    >

### <a name="give-hello-user-medium-resource-allocations"></a>Merhaba kullanıcı orta kaynak ayırma verin

1. Bu T-SQL komut toomake çalıştırmak üyesi mediumrc adlı hello Orta kaynak sınıfı, bir BT. 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > Tıklatın [burada](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn eşzamanlılık ve kaynak sınıfları hakkında daha fazla! 
    >

2. Toohello mantıksal sunucu hello yeni kimlik bilgilerinizle bağlanmak

    ![Yeni Oturum Bilgileriyle oturum açın](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a>Azure blob depolamadan veri yükleme

Artık hazır tooload verileri veri ambarınıza bulunur. Bu adım nasıl ortak bir Azure depolama biriminden tooload New York şehrinde ücreti cab verileri blob gösterir. 

- SQL veri ambarı tooload verisine toofirst olan yaygın bir yolu hello veri tooAzure blob depolama taşıyın ve veri ambarına yük. toomake bunu daha kolay toounderstand nasıl tooload, New York ücreti cab veri zaten bir ortak Azure storage blobu barındırılan sunuyoruz. 

- Gelecekte başvurmak, toolearn nasıl tooget veri tooAzure blob depolama veya doğrudan kaynağınızdan SQL veri ambarında, bkz: tooload hello [yüklemeye genel bakış](sql-data-warehouse-overview-load.md).


### <a name="define-external-data"></a>Dış veri tanımlama

1. Bir ana anahtar oluşturun. Yalnızca toocreate her veritabanı için bir kez bir ana anahtar gerekir. 

    ```sql
    CREATE MASTER KEY;
    ```

2. Merhaba hello ücreti cab verileri içeren Azure blob Hello konumunu tanımlayın.  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. Merhaba dış dosya biçimleri tanımlayın

    Merhaba ```CREATE EXTERNAL FILE FORMAT``` komuttur kullanılan toospecify hello dış veri içeren dosyaları biçimi. Sınırlayıcı adlı bir veya daha fazla karakter ile ayrılmış metinler içerir. Tanıtım amacıyla hello ücreti cab verileri hem de sıkıştırılmamış veri gzip sıkıştırılmış veri olarak depolanır.

    Bunları çalıştırmak T-SQL toodefine iki farklı biçimlerde komutlar: sıkıştırılmamış ve sıkıştırılmış.

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  Dış dosya biçiminiz için bir şema oluşturun. 

    ```sql
    CREATE SCHEMA ext;
    ```
5. Merhaba dış tablolar oluşturun. Bu tablolar Azure blob depolamada saklanan verilere başvurur. T-SQL komutlarını toocreate aşağıdaki hello tüm noktası toohello Azure blob biz önceden bizim dış veri kaynağında tanımlanan birkaç dış tablolara çalıştırın.

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-hello-data-from-azure-blob-storage"></a>Merhaba verileri Azure blob depolama alanından içeri aktarın.

SQL Veri Ambarı, CREATE TABLE AS SELECT (CTAS) adlı bir anahtar deyimini destekler. Bu deyim bir select deyimi hello sonuçlarına dayalı yeni bir tablo oluşturur. Merhaba yeni tablolu hello hello sonuçlarını select deyimi gibi hello aynı sütun ve veri türleri.  Bu bir Azure blob depolama alanına SQL Data Warehouse zarif bir şekilde tooimport verilerdir.

1. Bu komut dosyası tooimport verilerinizi çalıştırın.

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. Verilerinizi yüklenirken görüntüleyin.

   Birkaç GB veri yüklüyorsunuz ve yüksek performanslı kümelenmiş columnstore dizinlerine sıkıştırıyorsunuz. Merhaba yük dinamik yönetim görünümlerini (Dmv'leri) tooshow hello durumunu kullanan sorgu aşağıdaki hello çalıştırın. SQL Data Warehouse bazı ağır lifting desteklemiyor sırada hello sorgu başlattıktan sonra bir kahve ve bir yemek alın.
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. Tüm sistem sorgularını görüntüleyin.

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. Azure SQL Veri Ambarı’nıza verilerinizin sorunsuz şekilde yüklenmesinin keyfini çıkarın.

    ![Yüklenen Verilere bakın](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a>Sorgu performansını artırma

SQL veri ambarı tooachieve hello yüksek performans tooprovide tasarlanmış ve çeşitli yolları tooimprove sorgu performansı vardır.  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a>Merhaba etkisini sorgu performansına ölçeklendirme bakın 

Tek yönlü tooimprove sorgu performansı veri ambarınız için hello DWU hizmet düzeyi değiştirerek tooscale kaynaklarını aşıyor. Her hizmet düzeyi daha fazla maliyet getirir, ancak dilediğiniz zaman kaynakların ölçeğini azaltabilir veya kaynakları duraklatabilirsiniz. 

Bu adımda, iki farklı DWU ayarında performansı karşılaştırırsınız.

İlk olarak, biz nasıl bir işlem düğümünde hakkında bir fikir sınıflandırıp DWU gerçekleştirebileceğiniz, kendi too100 aşağı hello boyutlandırma şimdi ölçeklendirin.

1. Toohello portal gidin ve SQL veri ambarı seçin.

2. Ölçek hello SQL Data Warehouse dikey penceresinde seçin. 

    ![Portaldan Ölçek DW](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. Merhaba performans too100 DWU çubuğu ölçeğini ve Kaydet'i tıklatın.

    ![Ölçek ve kayıt](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. Ölçek işlemi toofinish bekleyin.

    > [!NOTE]
    > Sorguları hello ölçek değiştirilirken çalıştırılamıyor. Ölçeklendirme, o anda çalışmakta olan sorgularınızı **sonlandırır**. Merhaba işlem sona erdiğinde bunları yeniden başlatabilirsiniz.
    >
    
5. Merhaba üst milyon girişleri tüm hello sütunlar için seçerek hello seyahat veri üzerinde bir tarama işlemi yapın. İstekli toomove hızla girdiğinizi, ücretsiz tooselect daha az sayıda satır hissedilmesini. Bu işlem toorun geçen hello süreyi not edin.

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. Veri ambarınız ölçeklendirme too400 DWU yedekleyin. Her 100 DWU başka bir işlem düğümü tooyour Azure SQL Data Warehouse eklemeyi unutmayın.

7. Merhaba sorguyu yeniden çalıştırın! Önemli bir fark dikkat göreceksiniz. 

    > [!NOTE]
    > Hello sorgu çok miktarda veri döndürdüğünden hello bant genişliği kullanılabilirliğini SSMS çalışan hello makinenin performans düşüklüğü olabilir. Bu da herhangi bir performans artışıyla karşılaşmamanıza yol açabilir.

> [!NOTE]
> SQL Veri Ambarı, yüksek düzeyde paralel işleme kullanır. Tarama veya milyonlarca satır analitik işlevleri gerçekleştirmek sorguları hello true Azure SQL Data Warehouse gücünü karşılaşırsınız.
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a>Sorgu performans istatistikleri Hello etkisini görmek

1. Birleştirmeler tarih tablosu hello seyahat tabloyla hello sorgu çalıştırma

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    Merhaba birleştirme gerçekleştirmeden önce SQL veri ambarı tooshuffle veri içerdiğinden bu sorguyu biraz uzun sürebilir. Birleştirmeler yok tooshuffle veri hello tasarlanmış toojoin verilerde olmaları durumunda aynı şekilde bu dağıtılır. Bu daha derin bir konudur. 

2. İstatistikler fark yaratır. 
3. Bu deyim toocreate istatistikleri hello birleştirme sütunu üzerinde çalıştırın.

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > SQL DW istatistikleri sizin için otomatik olarak yönetmez. İstatistikleri sorgu performansı için önemlidir ve istatistikleri oluşturmanız ve güncelleştirmeniz önemle tavsiye edilir.
    > 
    > **Çoğu avantajı sütunlarda söz konusu birleşimlerde GROUP BY yan tümcesi ve sütun bulundu hello kullanılan sütun istatistikleri sağlayarak hello kazanır.**
    >

3. Önkoşulları Hello sorguyu yeniden çalıştırın ve tüm performans farklar inceleyin. Sorgu performansı Hello farklılıkları ölçeklendirmeyi olarak olarak keskin olmaz olsa da, bir faturalamak dikkat etmelidir. 

## <a name="next-steps"></a>Sonraki adımlar

Şimdi hazır tooquery olduğunuz ve keşfedin. En iyi yöntemlerimize veya ipuçlarımıza bakın.

İşiniz bittiğinde, örneğinizi olun emin toopause hello gün için keşfetme! Üretimde muazzam tasarrufları duraklatma ve ölçeklendirme toomeet yaşayabilirsiniz iş gereksinimlerinizi.

![Duraklat](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a>Yararlı okumalar

[Eşzamanlılık ve İş Yükü Yönetimi][]

[Azure SQL Veri Ambarı için en iyi yöntemler][]

[Sorgu İzleme][]

[Büyük Ölçekli İlişkisel Veri Ambarı Oluşturmaya Yönelik En İyi 10 Yöntem][]

[Geçirme verilerini tooAzure SQL veri ambarı][]

[Eşzamanlılık ve İş Yükü Yönetimi]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Azure SQL Veri Ambarı için en iyi yöntemler]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[Sorgu İzleme]: sql-data-warehouse-manage-monitor.md
[Büyük Ölçekli İlişkisel Veri Ambarı Oluşturmaya Yönelik En İyi 10 Yöntem]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/
[Geçirme verilerini tooAzure SQL veri ambarı]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[önkoşulları]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
