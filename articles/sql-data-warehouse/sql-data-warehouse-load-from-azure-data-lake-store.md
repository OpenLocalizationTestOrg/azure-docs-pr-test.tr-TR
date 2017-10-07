---
title: "aaaLoad - Azure Data Lake Store tooSQL veri ambarı | Microsoft Docs"
description: "Toouse PolyBase dış Azure Data Lake Store tooload verileri Azure SQL Data Warehouse'a nasıl tabloları hakkında bilgi edinin."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 01/25/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 50ef23b3eba5f58bc9974095f84140dc5c11fa4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a>Azure Data Lake Deposu'ndan veri SQL Data Warehouse'a veri yükleme
Bu belge PolyBase kullanarak SQL Data Warehouse'a kendi verilerinizi Azure veri Gölü deposu (ADLS) gelen tooload gereken tüm adımları sağlar.
Merhaba dış tablolara kullanarak ADLS içinde depolanan hello veriler üzerinde mümkün toorun geçici sorguları olmakla birlikte, en iyi uygulama olarak hello verileri SQL Data Warehouse hello alma öneririz.
Tahmini süre: 10 dakika hello önkoşullara sahip olduğu varsayılarak toocomplete gerekir.
Bu öğreticide şunları öğreneceksiniz nasıl yapılır:

1. Dış veritabanı nesneleri tooload Azure Data Lake Deposu'ndan veri oluşturun.
2. Azure Data Lake deposu dizinini tooan bağlayın.
3. Azure SQL Data Warehouse'a veri yükleme.

## <a name="before-you-begin"></a>Başlamadan önce
toorun Bu öğretici, gerekir:

* Hizmetten hizmete kimlik doğrulaması için Azure Active Directory Uygulama toouse. toocreate, izleyin [Active directory kimlik doğrulaması](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)

>[!NOTE] 
> Merhaba istemci kimliği, anahtar ve Active Directory Uygulama tooconnect tooyour Azure Data Lake SQL veri ambarından OAuth2.0 belirteç uç noktası değeri gerekiyor. Nasıl tooget bu bağlantıyı hello yukarıdaki değerler için Ayrıntılar'ı tıklatın.
>Azure Active Directory Uygulama kaydı için Not hello 'Uygulama kimliği' hello istemci kimliği kullanın

* SQL Server Management Studio veya SQL Server veri araçları, toodownload SSMS ve bakın bağlanmak [sorgu SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)

* Bir Azure SQL Data Warehouse toocreate birini izleyin: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision

* Bir Azure Data Lake Store, ile veya olmadan şifreleme etkin. toocreate bir izleyin: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal




## <a name="configure-hello-data-source"></a>Merhaba veri kaynağını yapılandırma
PolyBase T-SQL dış nesneleri toodefine hello konumu ve hello dış veri özniteliklerini kullanır. Merhaba dış nesneleri th harici olarak depolanan SQL veri ambarı ve başvuru hello verilerinde depolanır.


###  <a name="create-a-credential"></a>Bir kimlik bilgisi oluşturma
Azure Data Lake tooaccess deposuna, toocreate bir veritabanı ana anahtarı tooencrypt hello sonraki adımda kullanılan kimlik bilgileri gizli anahtarı gerekir.
AAD'de ayarlanan hello hizmet asıl kimlik bilgilerini depolayan bir veritabanı kapsamlı kimlik bilgisi oluşturursunuz. PolyBase tooconnect tooWindows Azure Storage Bloblarında kullanmış, o hello kimlik bilgisi unutmayın, içeriğiyle için sözdizimi farklıdır.
tooconnect tooAzure Data Lake Store, şunları yapmalısınız **ilk** Azure Active Directory uygulama oluşturmak, bir erişim anahtarı oluşturun ve hello uygulama erişim toohello Azure Data Lake kaynağı verin. Instrucitons tooperform adımları konumlandırıldığını [burada](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass hello client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
-- SECRET: Provide your AAD Application Service Principal key.
-- For more information on Create Database Scoped Credential: https://msdn.microsoft.com/en-us/library/mt270260.aspx

CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '<client_id>@<OAuth_2.0_Token_EndPoint>',
    SECRET = '<key>'
;

-- It should look something like this:
CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '536540b4-4239-45fe-b9a3-629f97591c0c@https://login.microsoftonline.com/42f988bf-85f1-41af-91ab-2d2cd011da47/oauth2/token',
    SECRET = 'BjdIlmtKp4Fpyh9hIvr8HJlUida/seM5kQ3EpLAmeDI='
;
```


### <a name="create-hello-external-data-source"></a>Merhaba dış veri kaynağı oluşturun
Bu [dış veri kaynağı oluştur] [ CREATE EXTERNAL DATA SOURCE] komut toostore hello konumunu hello veri ve veri hello türü.
Merhaba ADL URI hello Azure portal ve www.portal.azure.com bölümünde bulabilirsiniz.

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a>Veri biçimini yapılandırın
ADLS tooimport hello verileri, toospecify hello dış dosya biçimini gerekir. Bu komut, verilerinizi formata özgü seçenekleri toodescribe sahiptir.
Bir kanal sınırlandırılmış metin dosyası bir sık kullanılan bir dosya biçimi örneği aşağıdadır.
Tam bir listesi için T-SQL belgelerimize bakın [oluşturmak dış dosya biçimi][CREATE EXTERNAL FILE FORMAT]

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks hello end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies hello field terminator for data of type string in hello text-delimited file.
-- DATE_FORMAT: Specifies a custom format for all date and time data that might appear in a delimited text file.
-- Use_Type_Default: Store all Missing values as NULL

CREATE EXTERNAL FILE FORMAT TextFileFormat
WITH
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE
                    )
);
```

## <a name="create-hello-external-tables"></a>Merhaba dış tabloları oluşturma
Şimdi hello veri kaynağı ve dosya biçimi belirttiğiniz hazır toocreate hello dış tablolara demektir. Dış tablolar dış veri ile nasıl etkileşim değildir. PolyBase özyinelemeli dizin geçişi tooread hello konumu parametresinde belirtilen hello dizinin tüm alt dizinler tüm dosyaları kullanır. Ayrıca, aşağıdaki örneğine hello nasıl toocreate hello nesne gösterir. Sahip olduğunuz ADLS içinde hello verilerle toocustomize hello deyimi toowork gerekir.

```sql
-- D: Create an External Table
-- LOCATION: Folder under hello ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object toouse.
-- FILE_FORMAT: Specifies which File Format Object toouse
-- REJECT_TYPE: Specifies how you want toodeal with rejected rows. Either Value or percentage of hello total
-- REJECT_VALUE: Sets hello Reject value based on hello reject type.

-- DimProduct
CREATE EXTERNAL TABLE [dbo].[DimProduct_external] (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL
)
WITH
(
    LOCATION='/DimProduct/'
,   DATA_SOURCE = AzureDataLakeStore
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

```

## <a name="external-table-considerations"></a>Dış tablo konuları
Bir dış tablo oluşturmak kolaydır, ancak ele alınan toobe gereken bazı küçük farklar vardır.

PolyBase ile veri yükleme kesin türü belirtilmiş. Başka bir deyişle, her alınan hello veri satırının hello tablo şeması tanımı karşılaması gerekir.
Belirli bir satır hello şema tanımı eşleşmiyorsa hello satır hello yük reddedilir.

Merhaba REJECT_TYPE ve REJECT_VALUE seçeneklerini toodefine izin kaç satırları veya hello veri yüzdesini hello son tabloda mevcut olması gerekir.
Merhaba Reddet değerine ulaşılana yüklenmesi sırasında hello yükleme başarısız olur. Reddedilen satır Hello en yaygın nedeni bir şema tanımı uyumsuzluğu oluşturur.
Örneğin, Hello veri hello dosyasındaki bir dize olduğunda bir sütunu yanlış hello şema int verilen her satıra tooload başarısız olur.

Başlangıç konumu tooread verileri istediğiniz hello en üstteki dizini belirtir.
Bu durumda, varsa /DimProduct/ PolyBase alt dizinler hello alt dizinleri içindeki tüm hello veri alın.

## <a name="load-hello-data"></a>Merhaba veri yükleme
Azure Data Lake Store tooload verileri hello kullan [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] deyimi. İle CTAS yüklenirken kullanır hello oluşturduğunuz dış tablo kesin türü belirtilmiş.

CTAS yeni bir tablo oluşturur ve bir select deyimi hello sonuçlarını ile doldurur. CTAS tanımlar hello yeni tablo toohave hello hello sonuçlarını select deyimi gibi hello aynı sütun ve veri türleri. Bir dış tablodan tüm hello sütunları seçerseniz, hello yeni tablo hello sütunları ve veri türleri çoğaltmasını hello dış tablosunda vardır.

Bu örnekte, dış tablo DimProduct_external DimProduct adlı karma bir dağıtılmış tablo oluşturuyoruz.

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a>Columnstore sıkıştırma en iyi duruma getirme
Varsayılan olarak, SQL Data Warehouse kümelenmiş columnstore dizini hello tablo depolar. Yükleme tamamlandıktan sonra bazı hello veri satır hello columnstore sıkıştırılır değil.  Çeşitli nedenlerle oluşabilir neden yoktur. toolearn daha, fazla [columnstore dizinleri yönetmek][manage columnstore indexes].

toooptimize sorgu performansını ve columnstore sıkıştırma bir yükleme sonrasında, tüm hello satırları hello tablo tooforce hello columnstore dizini toocompress yeniden.

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

Merhaba columnstore dizinleri koruma ile ilgili daha fazla bilgi için bkz: [columnstore dizinleri yönetmek] [ manage columnstore indexes] makalesi.

## <a name="optimize-statistics"></a>İstatistikleri en iyi duruma getirme
Bu, bir yük hemen sonra en iyi toocreate tek sütunlu İstatistikler olur. İstatistikleri için bazı seçeneğiniz vardır. Örneğin, her sütunda tek sütunlu İstatistikler oluşturursanız, uzun süre toorebuild tüm hello istatistikleri alabilir. Belirli sütunları toobe sorgu koşullarda yapmayacağınız biliyorsanız, bu sütunlarda oluşturma istatistikleri atlayabilirsiniz.

Her tablonun her sütunu toocreate tek sütunlu İstatistikler karar verirseniz, hello saklı yordam kod örneği kullanabilirsiniz `prc_sqldw_create_stats` hello içinde [istatistikleri] [ statistics] makalesi.

Aşağıdaki örnek hello istatistikleri oluşturmak için iyi bir başlangıç noktası ' dir. Her sütunda hello Boyut tablosuna ve hello olgu tabloları katılan her sütunda tek sütunlu İstatistikler oluşturur. Daha sonra onları tek veya birden çok sütun istatistikleri tooother Olgu Tablosu sütunlarını ekleyebilirsiniz.


## <a name="achievement-unlocked"></a>Kilidi başarı!
Azure SQL Data Warehouse'a veri başarıyla yüklemiş olduğunuz. Harika iş!

##<a name="next-steps"></a>Sonraki Adımlar
Veri yükleme hello ilk adım toodeveloping SQL Data Warehouse kullanarak bir veri ambarı çözüm olur. Geliştirme KAYNAKLARIMIZI kontrol [tabloları](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) ve [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).


<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Load data into SQL Data Warehouse]: sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[manage columnstore indexes]: sql-data-warehouse-tables-index.md
[Statistics]: sql-data-warehouse-tables-statistics.md
[CTAS]: sql-data-warehouse-develop-ctas.md
[label]: sql-data-warehouse-develop-label.md

<!--MSDN references-->
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
