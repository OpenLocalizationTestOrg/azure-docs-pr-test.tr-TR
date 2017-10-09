---
title: "Azure blob tooAzure veri ambarından aaaLoad | Microsoft Docs"
description: "Toouse PolyBase tooload verileri Azure depolama SQL Data Warehouse'a nasıl blob öğrenin. Birkaç tablolar hello Contoso perakende veri ambarı şemasına genel verileri yüklenemiyor."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: faca0fe7-62e7-4e1f-a86f-032b4ffcb06e
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 4b4978ccefa4d55ff5c89fba84c5e705422ddbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a>Azure blob depolama alanından SQL Data Warehouse'a (PolyBase) veri yükleme
> [!div class="op_single_selector"]
> * [Data Factory](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [PolyBase](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

PolyBase ve T-SQL komutlarını tooload verileri Azure blob depolama alanından Azure SQL Data Warehouse'a kullanın. 

tookeep basit, Bu öğretici iki tablo ortak bir Azure Storage Blobundan hello Contoso perakende veri ambarı şemasına yükler. tooload hello tam veri hello örneği çalıştırmak kümesi [yük hello tam Contoso perakende veri ambarı] [ Load hello full Contoso Retail Data Warehouse] hello Microsoft SQL Server örnekleri depodan.

Bu öğreticide şunları yapacaksınız:

1. PolyBase tooload Azure blob depolama biriminden yapılandırma
2. Veritabanınıza ortak veri yükleme
3. Merhaba yükleme tamamlandıktan sonra en iyi duruma getirme gerçekleştirin.

## <a name="before-you-begin"></a>Başlamadan önce
toorun Bu öğreticide, bir SQL Data Warehouse veritabanı zaten olan bir Azure hesabınızın olması gerekir. Zaten yoksa, bkz: [SQL Data Warehouse oluşturma][Create a SQL Data Warehouse].

## <a name="1-configure-hello-data-source"></a>1. Merhaba veri kaynağını yapılandırma
PolyBase T-SQL dış nesneleri toodefine hello konumu ve hello dış veri özniteliklerini kullanır. Merhaba dış nesne tanımları SQL veri ambarında depolanır. Merhaba verilerin kendisini harici olarak depolanır.

### <a name="11-create-a-credential"></a>1.1. Bir kimlik bilgisi oluşturma
**Bu adımı atlayın** hello Contoso ortak veri yüklüyorsanız. Erişilebilir tooanyone olduğundan güvenli erişim toohello ortak veri gerekmez.

**Bu adımı atlamayın** kendi verileri yüklemek için bir şablon olarak Bu öğretici kullanıyorsanız. kimlik bilgileri, aşağıdaki kullanım hello tooaccess verilerine toocreate veritabanı kapsamlı kimlik bilgisi komut dosyası ve hello hello veri kaynağının konumunu tanımlarken kullanın.

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication tooAzure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);
```

Toostep 2 atlayın.

### <a name="12-create-hello-external-data-source"></a>1.2. Merhaba dış veri kaynağı oluşturun
Bu [dış veri kaynağı oluştur] [ CREATE EXTERNAL DATA SOURCE] komut toostore hello konumunu hello veri ve veri hello türü. 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> Azure blob depolama kapsayıcıları ortak toomake seçerseniz, veri hello veri merkezi ayrıldığında hello veri sahibi olarak, veriler için çıkış ücretlerini ücretlendirilirsiniz olduğunu unutmayın. 
> 
> 

## <a name="2-configure-data-format"></a>2. Veri biçimini yapılandırın
Merhaba veriler Azure blob depolama alanındaki metin dosyalarında depolanır ve her bir alan sınırlayıcı ile ayrılır. Bu [oluşturmak dış dosya BİÇİMİNİ] [ CREATE EXTERNAL FILE FORMAT] hello verilerin hello metin dosyalarında komutu toospecify hello biçimi. Merhaba Contoso veri sıkıştırılmamış ve kanal ayrılmış.

```sql
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

## <a name="3-create-hello-external-tables"></a>3. Merhaba dış tabloları oluşturma
Şimdi hello veri kaynağı ve dosya biçimi belirttiğiniz hazır toocreate hello dış tablolara demektir. 

### <a name="31-create-a-schema-for-hello-data"></a>3.1. Merhaba veri için bir şema oluşturun.
toocreate yer toostore hello Contoso verileri, veritabanında bir şema oluşturun.

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-hello-external-tables"></a>3.2. Merhaba dış tablolar oluşturun.
Bu komut dosyası toocreate hello DimProduct ve FactOnlineSales dış tablolara çalıştırın. Tüm biz burada yapmakta olduğunuz sütun adları ve veri türleri tanımlama ve toohello konumu ve hello Azure blob depolama dosyalarının biçimi bağlama. Merhaba tanımı SQL veri ambarı'nda depolanır ve hello veri hala hello Azure Storage Blobuna.

Merhaba **konumu** hello klasörü hello Azure Storage Blobuna hello kök klasöründe bir parametredir. Her tablo farklı bir klasöründe bulunur.

```sql

--DimProduct
CREATE EXTERNAL TABLE [asb].DimProduct (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL,
    [ProductDescription] [nvarchar](400) NULL,
    [ProductSubcategoryKey] [int] NULL,
    [Manufacturer] [nvarchar](50) NULL,
    [BrandName] [nvarchar](50) NULL,
    [ClassID] [nvarchar](10) NULL,
    [ClassName] [nvarchar](20) NULL,
    [StyleID] [nvarchar](10) NULL,
    [StyleName] [nvarchar](20) NULL,
    [ColorID] [nvarchar](10) NULL,
    [ColorName] [nvarchar](20) NOT NULL,
    [Size] [nvarchar](50) NULL,
    [SizeRange] [nvarchar](50) NULL,
    [SizeUnitMeasureID] [nvarchar](20) NULL,
    [Weight] [float] NULL,
    [WeightUnitMeasureID] [nvarchar](20) NULL,
    [UnitOfMeasureID] [nvarchar](10) NULL,
    [UnitOfMeasureName] [nvarchar](40) NULL,
    [StockTypeID] [nvarchar](10) NULL,
    [StockTypeName] [nvarchar](40) NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [AvailableForSaleDate] [datetime] NULL,
    [StopSaleDate] [datetime] NULL,
    [Status] [nvarchar](7) NULL,
    [ImageURL] [nvarchar](150) NULL,
    [ProductURL] [nvarchar](150) NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/DimProduct/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

--FactOnlineSales
CREATE EXTERNAL TABLE [asb].FactOnlineSales 
(
    [OnlineSalesKey] [int]  NOT NULL,
    [DateKey] [datetime] NOT NULL,
    [StoreKey] [int] NOT NULL,
    [ProductKey] [int] NOT NULL,
    [PromotionKey] [int] NOT NULL,
    [CurrencyKey] [int] NOT NULL,
    [CustomerKey] [int] NOT NULL,
    [SalesOrderNumber] [nvarchar](20) NOT NULL,
    [SalesOrderLineNumber] [int] NULL,
    [SalesQuantity] [int] NOT NULL,
    [SalesAmount] [money] NOT NULL,
    [ReturnQuantity] [int] NOT NULL,
    [ReturnAmount] [money] NULL,
    [DiscountQuantity] [int] NULL,
    [DiscountAmount] [money] NULL,
    [TotalCost] [money] NOT NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/FactOnlineSales/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;
```

## <a name="4-load-hello-data"></a>4. Merhaba veri yükleme
Farklı şekillerde tooaccess dış veri yoktur.  Merhaba dış tablo verileri doğrudan sorgu, yeni veritabanı tablolarına hello verileri yüklemek veya dış veri tooexisting veritabanı tabloları ekleyin.  

### <a name="41-create-a-new-schema"></a>4.1. Yeni bir şema oluşturun
CTAS verileri içeren yeni bir tablo oluşturur.  İlk olarak hello contoso veri için bir şema oluşturun.

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-hello-data-into-new-tables"></a>4.2. Yeni tablolara hello veri yükleme
tooload verileri Azure blob depolama ve veritabanınızı içinde bir tabloda, hello kullanmak [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] deyimi. İle CTAS yüklenirken yararlanır hello kesinlikle yalnızca created.tooload hello yeni tablolar verisine sahip dış tablolara yazılan, kullanmayı [CTAS] [ CTAS] tablo başına deyimi. 
 
CTAS yeni bir tablo oluşturur ve bir select deyimi hello sonuçlarını ile doldurur. CTAS tanımlar hello yeni tablo toohave hello hello sonuçlarını select deyimi gibi hello aynı sütun ve veri türleri. Bir dış tablodan tüm hello sütunları seçerseniz, hello yeni tablo hello dış tabloda hello sütunları ve veri türleri çoğaltmasını olacaktır.

Bu örnekte, hello boyut ve dağıtılmış tabloları karma gibi hello Olgu Tablosu oluşturun. 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-hello-load-progress"></a>4.3 izleme hello yükleme ilerlemesi
Dinamik Yönetim görünümlerini (Dmv'leri) kullanarak yük hello ilerlemesini izleyebilirsiniz. 

```sql
-- toosee all requests
SELECT * FROM sys.dm_pdw_exec_requests;

-- toosee a particular request identified by its label
SELECT * FROM sys.dm_pdw_exec_requests as r
WHERE r.[label] = 'CTAS : Load [cso].[DimProduct]             '
      OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
;

-- tootrack bytes and files
SELECT
    r.command,
    s.request_id,
    r.status,
    count(distinct input_name) as nbr_files, 
    sum(s.bytes_processed)/1024/1024/1024 as gb_processed
FROM
    sys.dm_pdw_exec_requests r
    inner join sys.dm_pdw_dms_external_work s
        on r.request_id = s.request_id
WHERE 
    r.[label] = 'CTAS : Load [cso].[DimProduct]             '
    OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
GROUP BY
    r.command,
    s.request_id,
    r.status
ORDER BY
    nbr_files desc,
    gb_processed desc;
```

## <a name="5-optimize-columnstore-compression"></a>5. Columnstore sıkıştırma en iyi duruma getirme
Varsayılan olarak, SQL Data Warehouse kümelenmiş columnstore dizini hello tablo depolar. Yükleme tamamlandıktan sonra bazı hello veri satır hello columnstore sıkıştırılır değil.  Çeşitli nedenlerle oluşabilir neden yoktur. toolearn daha, fazla [columnstore dizinleri yönetmek][manage columnstore indexes].

toooptimize sorgu performansını ve columnstore sıkıştırma bir yükleme sonrasında, tüm hello satırları hello tablo tooforce hello columnstore dizini toocompress yeniden. 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

Merhaba columnstore dizinleri koruma ile ilgili daha fazla bilgi için bkz: [columnstore dizinleri yönetmek] [ manage columnstore indexes] makalesi.

## <a name="6-optimize-statistics"></a>6. İstatistikleri en iyi duruma getirme
Bu, bir yük hemen sonra en iyi toocreate tek sütunlu İstatistikler olur. İstatistikleri için bazı seçeneğiniz vardır. Örneğin, her sütunda tek sütunlu İstatistikler oluşturursanız, uzun süre toorebuild tüm hello istatistikleri alabilir. Belirli sütunları toobe sorgu koşullarda yapmayacağınız biliyorsanız, bu sütunlarda oluşturma istatistikleri atlayabilirsiniz.

Her tablonun her sütunu toocreate tek sütunlu İstatistikler karar verirseniz, hello saklı yordam kod örneği kullanabilirsiniz `prc_sqldw_create_stats` hello içinde [istatistikleri] [ statistics] makalesi.

Aşağıdaki örnek hello istatistikleri oluşturmak için iyi bir başlangıç noktası ' dir. Her sütunda hello Boyut tablosuna ve hello olgu tabloları katılan her sütunda tek sütunlu İstatistikler oluşturur. Daha sonra onları tek veya birden çok sütun istatistikleri tooother Olgu Tablosu sütunlarını ekleyebilirsiniz.

```sql
CREATE STATISTICS [stat_cso_DimProduct_AvailableForSaleDate] ON [cso].[DimProduct]([AvailableForSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_BrandName] ON [cso].[DimProduct]([BrandName]);
CREATE STATISTICS [stat_cso_DimProduct_ClassID] ON [cso].[DimProduct]([ClassID]);
CREATE STATISTICS [stat_cso_DimProduct_ClassName] ON [cso].[DimProduct]([ClassName]);
CREATE STATISTICS [stat_cso_DimProduct_ColorID] ON [cso].[DimProduct]([ColorID]);
CREATE STATISTICS [stat_cso_DimProduct_ColorName] ON [cso].[DimProduct]([ColorName]);
CREATE STATISTICS [stat_cso_DimProduct_ETLLoadID] ON [cso].[DimProduct]([ETLLoadID]);
CREATE STATISTICS [stat_cso_DimProduct_ImageURL] ON [cso].[DimProduct]([ImageURL]);
CREATE STATISTICS [stat_cso_DimProduct_LoadDate] ON [cso].[DimProduct]([LoadDate]);
CREATE STATISTICS [stat_cso_DimProduct_Manufacturer] ON [cso].[DimProduct]([Manufacturer]);
CREATE STATISTICS [stat_cso_DimProduct_ProductDescription] ON [cso].[DimProduct]([ProductDescription]);
CREATE STATISTICS [stat_cso_DimProduct_ProductKey] ON [cso].[DimProduct]([ProductKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductLabel] ON [cso].[DimProduct]([ProductLabel]);
CREATE STATISTICS [stat_cso_DimProduct_ProductName] ON [cso].[DimProduct]([ProductName]);
CREATE STATISTICS [stat_cso_DimProduct_ProductSubcategoryKey] ON [cso].[DimProduct]([ProductSubcategoryKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductURL] ON [cso].[DimProduct]([ProductURL]);
CREATE STATISTICS [stat_cso_DimProduct_Size] ON [cso].[DimProduct]([Size]);
CREATE STATISTICS [stat_cso_DimProduct_SizeRange] ON [cso].[DimProduct]([SizeRange]);
CREATE STATISTICS [stat_cso_DimProduct_SizeUnitMeasureID] ON [cso].[DimProduct]([SizeUnitMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_Status] ON [cso].[DimProduct]([Status]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeID] ON [cso].[DimProduct]([StockTypeID]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeName] ON [cso].[DimProduct]([StockTypeName]);
CREATE STATISTICS [stat_cso_DimProduct_StopSaleDate] ON [cso].[DimProduct]([StopSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_StyleID] ON [cso].[DimProduct]([StyleID]);
CREATE STATISTICS [stat_cso_DimProduct_StyleName] ON [cso].[DimProduct]([StyleName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitCost] ON [cso].[DimProduct]([UnitCost]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureID] ON [cso].[DimProduct]([UnitOfMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureName] ON [cso].[DimProduct]([UnitOfMeasureName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitPrice] ON [cso].[DimProduct]([UnitPrice]);
CREATE STATISTICS [stat_cso_DimProduct_UpdateDate] ON [cso].[DimProduct]([UpdateDate]);
CREATE STATISTICS [stat_cso_DimProduct_Weight] ON [cso].[DimProduct]([Weight]);
CREATE STATISTICS [stat_cso_DimProduct_WeightUnitMeasureID] ON [cso].[DimProduct]([WeightUnitMeasureID]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CurrencyKey] ON [cso].[FactOnlineSales]([CurrencyKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CustomerKey] ON [cso].[FactOnlineSales]([CustomerKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_DateKey] ON [cso].[FactOnlineSales]([DateKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_OnlineSalesKey] ON [cso].[FactOnlineSales]([OnlineSalesKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_ProductKey] ON [cso].[FactOnlineSales]([ProductKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_PromotionKey] ON [cso].[FactOnlineSales]([PromotionKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_StoreKey] ON [cso].[FactOnlineSales]([StoreKey]);
```

## <a name="achievement-unlocked"></a>Kilidi başarı!
Azure SQL Data Warehouse'a ortak veri başarıyla yüklemiş olduğunuz. Harika iş!

Şimdi hello aşağıdaki gibi sorguları kullanarak hello tabloları sorgulama başlatabilirsiniz:

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a>Sonraki adımlar
tooload hello tam Contoso perakende veri ambarı veri, hello komut dosyasında daha fazla geliştirme ipuçları için bkz [SQL Data Warehouse geliştirmeye genel bakış][SQL Data Warehouse development overview].

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
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/en-us/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/en-us/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
