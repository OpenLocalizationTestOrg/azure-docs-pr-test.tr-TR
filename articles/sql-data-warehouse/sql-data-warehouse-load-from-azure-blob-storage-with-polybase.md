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
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a><span data-ttu-id="64555-104">Azure blob depolama alanından SQL Data Warehouse'a (PolyBase) veri yükleme</span><span class="sxs-lookup"><span data-stu-id="64555-104">Load data from Azure blob storage into SQL Data Warehouse (PolyBase)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="64555-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="64555-105">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="64555-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="64555-106">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

<span data-ttu-id="64555-107">PolyBase ve T-SQL komutlarını tooload verileri Azure blob depolama alanından Azure SQL Data Warehouse'a kullanın.</span><span class="sxs-lookup"><span data-stu-id="64555-107">Use PolyBase and T-SQL commands tooload data from Azure blob storage into Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="64555-108">tookeep basit, Bu öğretici iki tablo ortak bir Azure Storage Blobundan hello Contoso perakende veri ambarı şemasına yükler.</span><span class="sxs-lookup"><span data-stu-id="64555-108">tookeep it simple, this tutorial loads two tables from a public Azure Storage Blob into hello Contoso Retail Data Warehouse schema.</span></span> <span data-ttu-id="64555-109">tooload hello tam veri hello örneği çalıştırmak kümesi [yük hello tam Contoso perakende veri ambarı] [ Load hello full Contoso Retail Data Warehouse] hello Microsoft SQL Server örnekleri depodan.</span><span class="sxs-lookup"><span data-stu-id="64555-109">tooload hello full data set, run hello example [Load hello full Contoso Retail Data Warehouse][Load hello full Contoso Retail Data Warehouse] from hello Microsoft SQL Server Samples repository.</span></span>

<span data-ttu-id="64555-110">Bu öğreticide şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="64555-110">In this tutorial you will:</span></span>

1. <span data-ttu-id="64555-111">PolyBase tooload Azure blob depolama biriminden yapılandırma</span><span class="sxs-lookup"><span data-stu-id="64555-111">Configure PolyBase tooload from Azure blob storage</span></span>
2. <span data-ttu-id="64555-112">Veritabanınıza ortak veri yükleme</span><span class="sxs-lookup"><span data-stu-id="64555-112">Load public data into your database</span></span>
3. <span data-ttu-id="64555-113">Merhaba yükleme tamamlandıktan sonra en iyi duruma getirme gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="64555-113">Perform optimizations after hello load is finished.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="64555-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="64555-114">Before you begin</span></span>
<span data-ttu-id="64555-115">toorun Bu öğreticide, bir SQL Data Warehouse veritabanı zaten olan bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="64555-115">toorun this tutorial, you need an Azure account that already has a SQL Data Warehouse database.</span></span> <span data-ttu-id="64555-116">Zaten yoksa, bkz: [SQL Data Warehouse oluşturma][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="64555-116">If you don't already have this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>

## <a name="1-configure-hello-data-source"></a><span data-ttu-id="64555-117">1. Merhaba veri kaynağını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="64555-117">1. Configure hello data source</span></span>
<span data-ttu-id="64555-118">PolyBase T-SQL dış nesneleri toodefine hello konumu ve hello dış veri özniteliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="64555-118">PolyBase uses T-SQL external objects toodefine hello location and attributes of hello external data.</span></span> <span data-ttu-id="64555-119">Merhaba dış nesne tanımları SQL veri ambarında depolanır.</span><span class="sxs-lookup"><span data-stu-id="64555-119">hello external object definitions are stored in SQL Data Warehouse.</span></span> <span data-ttu-id="64555-120">Merhaba verilerin kendisini harici olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="64555-120">hello data itself is stored externally.</span></span>

### <a name="11-create-a-credential"></a><span data-ttu-id="64555-121">1.1.</span><span class="sxs-lookup"><span data-stu-id="64555-121">1.1.</span></span> <span data-ttu-id="64555-122">Bir kimlik bilgisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="64555-122">Create a credential</span></span>
<span data-ttu-id="64555-123">**Bu adımı atlayın** hello Contoso ortak veri yüklüyorsanız.</span><span class="sxs-lookup"><span data-stu-id="64555-123">**Skip this step** if you are loading hello Contoso public data.</span></span> <span data-ttu-id="64555-124">Erişilebilir tooanyone olduğundan güvenli erişim toohello ortak veri gerekmez.</span><span class="sxs-lookup"><span data-stu-id="64555-124">You don't need secure access toohello public data since it is already accessible tooanyone.</span></span>

<span data-ttu-id="64555-125">**Bu adımı atlamayın** kendi verileri yüklemek için bir şablon olarak Bu öğretici kullanıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="64555-125">**Don't skip this step** if you are using this tutorial as a template for loading your own data.</span></span> <span data-ttu-id="64555-126">kimlik bilgileri, aşağıdaki kullanım hello tooaccess verilerine toocreate veritabanı kapsamlı kimlik bilgisi komut dosyası ve hello hello veri kaynağının konumunu tanımlarken kullanın.</span><span class="sxs-lookup"><span data-stu-id="64555-126">tooaccess data through a credential, use hello following script toocreate a database-scoped credential, and then use it when defining hello location of hello data source.</span></span>

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

<span data-ttu-id="64555-127">Toostep 2 atlayın.</span><span class="sxs-lookup"><span data-stu-id="64555-127">Skip toostep 2.</span></span>

### <a name="12-create-hello-external-data-source"></a><span data-ttu-id="64555-128">1.2.</span><span class="sxs-lookup"><span data-stu-id="64555-128">1.2.</span></span> <span data-ttu-id="64555-129">Merhaba dış veri kaynağı oluşturun</span><span class="sxs-lookup"><span data-stu-id="64555-129">Create hello external data source</span></span>
<span data-ttu-id="64555-130">Bu [dış veri kaynağı oluştur] [ CREATE EXTERNAL DATA SOURCE] komut toostore hello konumunu hello veri ve veri hello türü.</span><span class="sxs-lookup"><span data-stu-id="64555-130">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command toostore hello location of hello data, and hello type of data.</span></span> 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> <span data-ttu-id="64555-131">Azure blob depolama kapsayıcıları ortak toomake seçerseniz, veri hello veri merkezi ayrıldığında hello veri sahibi olarak, veriler için çıkış ücretlerini ücretlendirilirsiniz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="64555-131">If you choose toomake your azure blob storage containers public, remember that as hello data owner you will be charged for data egress charges when data leaves hello data center.</span></span> 
> 
> 

## <a name="2-configure-data-format"></a><span data-ttu-id="64555-132">2. Veri biçimini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="64555-132">2. Configure data format</span></span>
<span data-ttu-id="64555-133">Merhaba veriler Azure blob depolama alanındaki metin dosyalarında depolanır ve her bir alan sınırlayıcı ile ayrılır.</span><span class="sxs-lookup"><span data-stu-id="64555-133">hello data is stored in text files in Azure blob storage, and each field is separated with a delimiter.</span></span> <span data-ttu-id="64555-134">Bu [oluşturmak dış dosya BİÇİMİNİ] [ CREATE EXTERNAL FILE FORMAT] hello verilerin hello metin dosyalarında komutu toospecify hello biçimi.</span><span class="sxs-lookup"><span data-stu-id="64555-134">Run this [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] command toospecify hello format of hello data in hello text files.</span></span> <span data-ttu-id="64555-135">Merhaba Contoso veri sıkıştırılmamış ve kanal ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="64555-135">hello Contoso data is uncompressed and pipe delimited.</span></span>

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

## <a name="3-create-hello-external-tables"></a><span data-ttu-id="64555-136">3. Merhaba dış tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="64555-136">3. Create hello external tables</span></span>
<span data-ttu-id="64555-137">Şimdi hello veri kaynağı ve dosya biçimi belirttiğiniz hazır toocreate hello dış tablolara demektir.</span><span class="sxs-lookup"><span data-stu-id="64555-137">Now that you have specified hello data source and file format, you are ready toocreate hello external tables.</span></span> 

### <a name="31-create-a-schema-for-hello-data"></a><span data-ttu-id="64555-138">3.1.</span><span class="sxs-lookup"><span data-stu-id="64555-138">3.1.</span></span> <span data-ttu-id="64555-139">Merhaba veri için bir şema oluşturun.</span><span class="sxs-lookup"><span data-stu-id="64555-139">Create a schema for hello data.</span></span>
<span data-ttu-id="64555-140">toocreate yer toostore hello Contoso verileri, veritabanında bir şema oluşturun.</span><span class="sxs-lookup"><span data-stu-id="64555-140">toocreate a place toostore hello Contoso data in your database, create a schema.</span></span>

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-hello-external-tables"></a><span data-ttu-id="64555-141">3.2.</span><span class="sxs-lookup"><span data-stu-id="64555-141">3.2.</span></span> <span data-ttu-id="64555-142">Merhaba dış tablolar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="64555-142">Create hello external tables.</span></span>
<span data-ttu-id="64555-143">Bu komut dosyası toocreate hello DimProduct ve FactOnlineSales dış tablolara çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="64555-143">Run this script toocreate hello DimProduct and FactOnlineSales external tables.</span></span> <span data-ttu-id="64555-144">Tüm biz burada yapmakta olduğunuz sütun adları ve veri türleri tanımlama ve toohello konumu ve hello Azure blob depolama dosyalarının biçimi bağlama.</span><span class="sxs-lookup"><span data-stu-id="64555-144">All we are doing here is defining column names and data types, and binding them toohello location and format of hello Azure blob storage files.</span></span> <span data-ttu-id="64555-145">Merhaba tanımı SQL veri ambarı'nda depolanır ve hello veri hala hello Azure Storage Blobuna.</span><span class="sxs-lookup"><span data-stu-id="64555-145">hello definition is stored in SQL Data Warehouse and hello data is still in hello Azure Storage Blob.</span></span>

<span data-ttu-id="64555-146">Merhaba **konumu** hello klasörü hello Azure Storage Blobuna hello kök klasöründe bir parametredir.</span><span class="sxs-lookup"><span data-stu-id="64555-146">hello  **LOCATION** parameter is hello folder under hello root folder in hello Azure Storage Blob.</span></span> <span data-ttu-id="64555-147">Her tablo farklı bir klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="64555-147">Each table is in a different folder.</span></span>

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

## <a name="4-load-hello-data"></a><span data-ttu-id="64555-148">4. Merhaba veri yükleme</span><span class="sxs-lookup"><span data-stu-id="64555-148">4. Load hello data</span></span>
<span data-ttu-id="64555-149">Farklı şekillerde tooaccess dış veri yoktur.</span><span class="sxs-lookup"><span data-stu-id="64555-149">There's different ways tooaccess external data.</span></span>  <span data-ttu-id="64555-150">Merhaba dış tablo verileri doğrudan sorgu, yeni veritabanı tablolarına hello verileri yüklemek veya dış veri tooexisting veritabanı tabloları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="64555-150">You can query data directly from hello external table, load hello data into new database tables, or add external data tooexisting database tables.</span></span>  

### <a name="41-create-a-new-schema"></a><span data-ttu-id="64555-151">4.1.</span><span class="sxs-lookup"><span data-stu-id="64555-151">4.1.</span></span> <span data-ttu-id="64555-152">Yeni bir şema oluşturun</span><span class="sxs-lookup"><span data-stu-id="64555-152">Create a new schema</span></span>
<span data-ttu-id="64555-153">CTAS verileri içeren yeni bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="64555-153">CTAS creates a new table that contains data.</span></span>  <span data-ttu-id="64555-154">İlk olarak hello contoso veri için bir şema oluşturun.</span><span class="sxs-lookup"><span data-stu-id="64555-154">First, create a schema for hello contoso data.</span></span>

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-hello-data-into-new-tables"></a><span data-ttu-id="64555-155">4.2.</span><span class="sxs-lookup"><span data-stu-id="64555-155">4.2.</span></span> <span data-ttu-id="64555-156">Yeni tablolara hello veri yükleme</span><span class="sxs-lookup"><span data-stu-id="64555-156">Load hello data into new tables</span></span>
<span data-ttu-id="64555-157">tooload verileri Azure blob depolama ve veritabanınızı içinde bir tabloda, hello kullanmak [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] deyimi.</span><span class="sxs-lookup"><span data-stu-id="64555-157">tooload data from Azure blob storage and save it in a table inside of your database, use hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="64555-158">İle CTAS yüklenirken yararlanır hello kesinlikle yalnızca created.tooload hello yeni tablolar verisine sahip dış tablolara yazılan, kullanmayı [CTAS] [ CTAS] tablo başına deyimi.</span><span class="sxs-lookup"><span data-stu-id="64555-158">Loading with CTAS leverages hello strongly typed external tables you have just created.tooload hello data into new tables, use one [CTAS][CTAS] statement per table.</span></span> 
 
<span data-ttu-id="64555-159">CTAS yeni bir tablo oluşturur ve bir select deyimi hello sonuçlarını ile doldurur.</span><span class="sxs-lookup"><span data-stu-id="64555-159">CTAS creates a new table and populates it with hello results of a select statement.</span></span> <span data-ttu-id="64555-160">CTAS tanımlar hello yeni tablo toohave hello hello sonuçlarını select deyimi gibi hello aynı sütun ve veri türleri.</span><span class="sxs-lookup"><span data-stu-id="64555-160">CTAS defines hello new table toohave hello same columns and data types as hello results of hello select statement.</span></span> <span data-ttu-id="64555-161">Bir dış tablodan tüm hello sütunları seçerseniz, hello yeni tablo hello dış tabloda hello sütunları ve veri türleri çoğaltmasını olacaktır.</span><span class="sxs-lookup"><span data-stu-id="64555-161">If you select all hello columns from an external table, hello new table will be a replica of hello columns and data types in hello external table.</span></span>

<span data-ttu-id="64555-162">Bu örnekte, hello boyut ve dağıtılmış tabloları karma gibi hello Olgu Tablosu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="64555-162">In this example, we create both hello dimension and hello fact table as hash distributed tables.</span></span> 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-hello-load-progress"></a><span data-ttu-id="64555-163">4.3 izleme hello yükleme ilerlemesi</span><span class="sxs-lookup"><span data-stu-id="64555-163">4.3 Track hello load progress</span></span>
<span data-ttu-id="64555-164">Dinamik Yönetim görünümlerini (Dmv'leri) kullanarak yük hello ilerlemesini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64555-164">You can track hello progress of your load using dynamic management views (DMVs).</span></span> 

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

## <a name="5-optimize-columnstore-compression"></a><span data-ttu-id="64555-165">5. Columnstore sıkıştırma en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="64555-165">5. Optimize columnstore compression</span></span>
<span data-ttu-id="64555-166">Varsayılan olarak, SQL Data Warehouse kümelenmiş columnstore dizini hello tablo depolar.</span><span class="sxs-lookup"><span data-stu-id="64555-166">By default, SQL Data Warehouse stores hello table as a clustered columnstore index.</span></span> <span data-ttu-id="64555-167">Yükleme tamamlandıktan sonra bazı hello veri satır hello columnstore sıkıştırılır değil.</span><span class="sxs-lookup"><span data-stu-id="64555-167">After a load completes, some of hello data rows might not be compressed into hello columnstore.</span></span>  <span data-ttu-id="64555-168">Çeşitli nedenlerle oluşabilir neden yoktur.</span><span class="sxs-lookup"><span data-stu-id="64555-168">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="64555-169">toolearn daha, fazla [columnstore dizinleri yönetmek][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="64555-169">toolearn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="64555-170">toooptimize sorgu performansını ve columnstore sıkıştırma bir yükleme sonrasında, tüm hello satırları hello tablo tooforce hello columnstore dizini toocompress yeniden.</span><span class="sxs-lookup"><span data-stu-id="64555-170">toooptimize query performance and columnstore compression after a load, rebuild hello table tooforce hello columnstore index toocompress all hello rows.</span></span> 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

<span data-ttu-id="64555-171">Merhaba columnstore dizinleri koruma ile ilgili daha fazla bilgi için bkz: [columnstore dizinleri yönetmek] [ manage columnstore indexes] makalesi.</span><span class="sxs-lookup"><span data-stu-id="64555-171">For more information on maintaining columnstore indexes, see hello [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="6-optimize-statistics"></a><span data-ttu-id="64555-172">6. İstatistikleri en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="64555-172">6. Optimize statistics</span></span>
<span data-ttu-id="64555-173">Bu, bir yük hemen sonra en iyi toocreate tek sütunlu İstatistikler olur.</span><span class="sxs-lookup"><span data-stu-id="64555-173">It is best toocreate single-column statistics immediately after a load.</span></span> <span data-ttu-id="64555-174">İstatistikleri için bazı seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="64555-174">There are some choices for statistics.</span></span> <span data-ttu-id="64555-175">Örneğin, her sütunda tek sütunlu İstatistikler oluşturursanız, uzun süre toorebuild tüm hello istatistikleri alabilir.</span><span class="sxs-lookup"><span data-stu-id="64555-175">For example, if you create single-column statistics on every column it might take a long time toorebuild all hello statistics.</span></span> <span data-ttu-id="64555-176">Belirli sütunları toobe sorgu koşullarda yapmayacağınız biliyorsanız, bu sütunlarda oluşturma istatistikleri atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64555-176">If you know certain columns are not going toobe in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="64555-177">Her tablonun her sütunu toocreate tek sütunlu İstatistikler karar verirseniz, hello saklı yordam kod örneği kullanabilirsiniz `prc_sqldw_create_stats` hello içinde [istatistikleri] [ statistics] makalesi.</span><span class="sxs-lookup"><span data-stu-id="64555-177">If you decide toocreate single-column statistics on every column of every table, you can use hello stored procedure code sample `prc_sqldw_create_stats` in hello [statistics][statistics] article.</span></span>

<span data-ttu-id="64555-178">Aşağıdaki örnek hello istatistikleri oluşturmak için iyi bir başlangıç noktası ' dir.</span><span class="sxs-lookup"><span data-stu-id="64555-178">hello following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="64555-179">Her sütunda hello Boyut tablosuna ve hello olgu tabloları katılan her sütunda tek sütunlu İstatistikler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="64555-179">It creates single-column statistics on each column in hello dimension table, and on each joining column in hello fact tables.</span></span> <span data-ttu-id="64555-180">Daha sonra onları tek veya birden çok sütun istatistikleri tooother Olgu Tablosu sütunlarını ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64555-180">You can always add single or multi-column statistics tooother fact table columns later on.</span></span>

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

## <a name="achievement-unlocked"></a><span data-ttu-id="64555-181">Kilidi başarı!</span><span class="sxs-lookup"><span data-stu-id="64555-181">Achievement unlocked!</span></span>
<span data-ttu-id="64555-182">Azure SQL Data Warehouse'a ortak veri başarıyla yüklemiş olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="64555-182">You have successfully loaded public data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="64555-183">Harika iş!</span><span class="sxs-lookup"><span data-stu-id="64555-183">Great job!</span></span>

<span data-ttu-id="64555-184">Şimdi hello aşağıdaki gibi sorguları kullanarak hello tabloları sorgulama başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="64555-184">You can now start querying hello tables using queries like hello following:</span></span>

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a><span data-ttu-id="64555-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="64555-185">Next steps</span></span>
<span data-ttu-id="64555-186">tooload hello tam Contoso perakende veri ambarı veri, hello komut dosyasında daha fazla geliştirme ipuçları için bkz [SQL Data Warehouse geliştirmeye genel bakış][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="64555-186">tooload hello full Contoso Retail Data Warehouse data, use hello script in For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
