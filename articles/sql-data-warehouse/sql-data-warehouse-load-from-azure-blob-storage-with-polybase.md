---
title: "Azure'dan yük blob Azure veri ambarına | Microsoft Docs"
description: "PolyBase verileri Azure blob depolama alanından SQL Data Warehouse'a veri yüklemek için nasıl kullanılacağını öğrenin. Birkaç tablolar Contoso perakende veri ambarı şemasına genel verileri yüklenemiyor."
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
ms.openlocfilehash: 2859c1144f72fd685af89f83024df1409902ab0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a><span data-ttu-id="6c6d6-104">Azure blob depolama alanından SQL Data Warehouse'a (PolyBase) veri yükleme</span><span class="sxs-lookup"><span data-stu-id="6c6d6-104">Load data from Azure blob storage into SQL Data Warehouse (PolyBase)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c6d6-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="6c6d6-105">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="6c6d6-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="6c6d6-106">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

<span data-ttu-id="6c6d6-107">Verileri Azure blob depolama alanından Azure SQL Data Warehouse'a veri yüklemek için PolyBase ve T-SQL komutlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-107">Use PolyBase and T-SQL commands to load data from Azure blob storage into Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="6c6d6-108">Basit tutmak için bu öğreticiyi iki tablo Contoso perakende veri ambarı şemasına ortak bir Azure Storage Blobundan yükler.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-108">To keep it simple, this tutorial loads two tables from a public Azure Storage Blob into the Contoso Retail Data Warehouse schema.</span></span> <span data-ttu-id="6c6d6-109">Tam veri kümesi yüklemek için örneği çalıştırmak [tam Contoso perakende veri ambarı yük] [ Load the full Contoso Retail Data Warehouse] Microsoft SQL Server örnekleri depodan.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-109">To load the full data set, run the example [Load the full Contoso Retail Data Warehouse][Load the full Contoso Retail Data Warehouse] from the Microsoft SQL Server Samples repository.</span></span>

<span data-ttu-id="6c6d6-110">Bu öğreticide şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="6c6d6-110">In this tutorial you will:</span></span>

1. <span data-ttu-id="6c6d6-111">Azure blob depolama alanından yüklemek için PolyBase yapılandırın</span><span class="sxs-lookup"><span data-stu-id="6c6d6-111">Configure PolyBase to load from Azure blob storage</span></span>
2. <span data-ttu-id="6c6d6-112">Veritabanınıza ortak veri yükleme</span><span class="sxs-lookup"><span data-stu-id="6c6d6-112">Load public data into your database</span></span>
3. <span data-ttu-id="6c6d6-113">Yükleme tamamlandıktan sonra en iyi duruma getirme gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-113">Perform optimizations after the load is finished.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6c6d6-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="6c6d6-114">Before you begin</span></span>
<span data-ttu-id="6c6d6-115">Bu öğretici çalıştırmak için SQL Data Warehouse veritabanı zaten bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-115">To run this tutorial, you need an Azure account that already has a SQL Data Warehouse database.</span></span> <span data-ttu-id="6c6d6-116">Zaten yoksa, bkz: [SQL Data Warehouse oluşturma][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="6c6d6-116">If you don't already have this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>

## <a name="1-configure-the-data-source"></a><span data-ttu-id="6c6d6-117">1. Veri kaynağını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6c6d6-117">1. Configure the data source</span></span>
<span data-ttu-id="6c6d6-118">PolyBase, dış veri özniteliklerini ve konumunu tanımlamak için T-SQL dış nesneleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-118">PolyBase uses T-SQL external objects to define the location and attributes of the external data.</span></span> <span data-ttu-id="6c6d6-119">Dış nesne tanımları SQL veri ambarında depolanır.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-119">The external object definitions are stored in SQL Data Warehouse.</span></span> <span data-ttu-id="6c6d6-120">Veri harici olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-120">The data itself is stored externally.</span></span>

### <a name="11-create-a-credential"></a><span data-ttu-id="6c6d6-121">1.1.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-121">1.1.</span></span> <span data-ttu-id="6c6d6-122">Bir kimlik bilgisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c6d6-122">Create a credential</span></span>
<span data-ttu-id="6c6d6-123">**Bu adımı atlayın** Contoso ortak veri yüklüyorsanız.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-123">**Skip this step** if you are loading the Contoso public data.</span></span> <span data-ttu-id="6c6d6-124">Zaten herkes için erişilebilir olduğundan ortak verilere güvenli erişim gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-124">You don't need secure access to the public data since it is already accessible to anyone.</span></span>

<span data-ttu-id="6c6d6-125">**Bu adımı atlamayın** kendi verileri yüklemek için bir şablon olarak Bu öğretici kullanıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-125">**Don't skip this step** if you are using this tutorial as a template for loading your own data.</span></span> <span data-ttu-id="6c6d6-126">Bir kimlik bilgisi verilere erişmek için veritabanı kapsamlı bir kimlik bilgisi oluşturmak için aşağıdaki komut dosyasını kullanın ve veri kaynağının konumunu tanımlarken kullanın.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-126">To access data through a credential, use the following script to create a database-scoped credential, and then use it when defining the location of the data source.</span></span>

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required to encrypt the credential secret in the next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication to Azure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide the credential created in the previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);
```

<span data-ttu-id="6c6d6-127">2. adıma atlayın.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-127">Skip to step 2.</span></span>

### <a name="12-create-the-external-data-source"></a><span data-ttu-id="6c6d6-128">1.2.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-128">1.2.</span></span> <span data-ttu-id="6c6d6-129">Dış veri kaynağı oluşturun</span><span class="sxs-lookup"><span data-stu-id="6c6d6-129">Create the external data source</span></span>
<span data-ttu-id="6c6d6-130">Bu [dış veri kaynağı oluştur] [ CREATE EXTERNAL DATA SOURCE] veri ve veri türü konumunu depolamak için komutu.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-130">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command to store the location of the data, and the type of data.</span></span> 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> <span data-ttu-id="6c6d6-131">Azure blob storage kapsayıcıları genel hale getirmek isterseniz verileri veri merkezi ayrıldığında veri sahibi olarak, veriler için çıkış ücretlerini ücretlendirilirsiniz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-131">If you choose to make your azure blob storage containers public, remember that as the data owner you will be charged for data egress charges when data leaves the data center.</span></span> 
> 
> 

## <a name="2-configure-data-format"></a><span data-ttu-id="6c6d6-132">2. Veri biçimini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="6c6d6-132">2. Configure data format</span></span>
<span data-ttu-id="6c6d6-133">Verileri Azure blob depolama alanındaki metin dosyalarında depolanır ve her bir alan sınırlayıcı ile ayrılır.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-133">The data is stored in text files in Azure blob storage, and each field is separated with a delimiter.</span></span> <span data-ttu-id="6c6d6-134">Bu [oluşturmak dış dosya BİÇİMİNİ] [ CREATE EXTERNAL FILE FORMAT] metin dosyalarında verilerin biçimini belirtmek için komut.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-134">Run this [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] command to specify the format of the data in the text files.</span></span> <span data-ttu-id="6c6d6-135">Contoso veri sıkıştırılmamış ve kanal ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-135">The Contoso data is uncompressed and pipe delimited.</span></span>

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

## <a name="3-create-the-external-tables"></a><span data-ttu-id="6c6d6-136">3. Dış tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c6d6-136">3. Create the external tables</span></span>
<span data-ttu-id="6c6d6-137">Veri kaynağı ve dosya biçimi belirttiğiniz, dış tablo oluşturmak hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-137">Now that you have specified the data source and file format, you are ready to create the external tables.</span></span> 

### <a name="31-create-a-schema-for-the-data"></a><span data-ttu-id="6c6d6-138">3.1.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-138">3.1.</span></span> <span data-ttu-id="6c6d6-139">Veriler için bir şema oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-139">Create a schema for the data.</span></span>
<span data-ttu-id="6c6d6-140">Contoso veri veritabanınızda depolamak için bir yer oluşturmak için bir şema oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-140">To create a place to store the Contoso data in your database, create a schema.</span></span>

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-the-external-tables"></a><span data-ttu-id="6c6d6-141">3.2.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-141">3.2.</span></span> <span data-ttu-id="6c6d6-142">Harici tabloları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-142">Create the external tables.</span></span>
<span data-ttu-id="6c6d6-143">DimProduct ve FactOnlineSales dış tablolar oluşturmak için bu komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-143">Run this script to create the DimProduct and FactOnlineSales external tables.</span></span> <span data-ttu-id="6c6d6-144">Tüm biz burada yapmakta olduğunuz sütun adları ve veri türleri tanımlama ve konumunu ve Azure blob depolama dosyalarının biçimi bağlama.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-144">All we are doing here is defining column names and data types, and binding them to the location and format of the Azure blob storage files.</span></span> <span data-ttu-id="6c6d6-145">Tanımı SQL veri ambarı'nda depolanır ve verileri Azure depolama Blob hala.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-145">The definition is stored in SQL Data Warehouse and the data is still in the Azure Storage Blob.</span></span>

<span data-ttu-id="6c6d6-146">**Konumu** parametresi Azure Storage Blobuna kök klasöründe bir klasördür.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-146">The  **LOCATION** parameter is the folder under the root folder in the Azure Storage Blob.</span></span> <span data-ttu-id="6c6d6-147">Her tablo farklı bir klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-147">Each table is in a different folder.</span></span>

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

## <a name="4-load-the-data"></a><span data-ttu-id="6c6d6-148">4. Verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="6c6d6-148">4. Load the data</span></span>
<span data-ttu-id="6c6d6-149">Dış verilere erişmek için farklı yollar yoktur.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-149">There's different ways to access external data.</span></span>  <span data-ttu-id="6c6d6-150">Dış tablo verileri doğrudan sorgu, yeni veritabanı tablolarına verileri yüklemek veya var olan veritabanı tablolarında dış veri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-150">You can query data directly from the external table, load the data into new database tables, or add external data to existing database tables.</span></span>  

### <a name="41-create-a-new-schema"></a><span data-ttu-id="6c6d6-151">4.1.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-151">4.1.</span></span> <span data-ttu-id="6c6d6-152">Yeni bir şema oluşturun</span><span class="sxs-lookup"><span data-stu-id="6c6d6-152">Create a new schema</span></span>
<span data-ttu-id="6c6d6-153">CTAS verileri içeren yeni bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-153">CTAS creates a new table that contains data.</span></span>  <span data-ttu-id="6c6d6-154">İlk olarak, contoso veri için bir şema oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-154">First, create a schema for the contoso data.</span></span>

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-the-data-into-new-tables"></a><span data-ttu-id="6c6d6-155">4.2.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-155">4.2.</span></span> <span data-ttu-id="6c6d6-156">Yeni tablolara veri yükleme</span><span class="sxs-lookup"><span data-stu-id="6c6d6-156">Load the data into new tables</span></span>
<span data-ttu-id="6c6d6-157">Azure blob depolama alanından verileri yüklemek ve veritabanınızın içinde bir tablodaki kaydetmek için kullanın [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] deyimi.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-157">To load data from Azure blob storage and save it in a table inside of your database, use the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="6c6d6-158">Yükleme CTAS ile oluşturduğunuz kesin türü belirtilmiş dış tablolara yararlanır. Verileri yeni tablolara yüklemek için kullanmayı [CTAS] [ CTAS] tablo başına deyimi.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-158">Loading with CTAS leverages the strongly typed external tables you have just created.To load the data into new tables, use one [CTAS][CTAS] statement per table.</span></span> 
 
<span data-ttu-id="6c6d6-159">CTAS yeni bir tablo oluşturur ve bir select deyimi sonuçları ile doldurur.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-159">CTAS creates a new table and populates it with the results of a select statement.</span></span> <span data-ttu-id="6c6d6-160">CTAS select deyimi sonuçları olarak aynı sütunları ve veri türleri için yeni tabloyu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-160">CTAS defines the new table to have the same columns and data types as the results of the select statement.</span></span> <span data-ttu-id="6c6d6-161">Dış bir tablodaki tüm sütunları seçin, yeni bir tablo sütunları ve dış tablosunda veri türlerini çoğaltmasını olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-161">If you select all the columns from an external table, the new table will be a replica of the columns and data types in the external table.</span></span>

<span data-ttu-id="6c6d6-162">Bu örnekte, boyut ve dağıtılmış tabloları karma gibi Olgu Tablosu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-162">In this example, we create both the dimension and the fact table as hash distributed tables.</span></span> 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-the-load-progress"></a><span data-ttu-id="6c6d6-163">4.3 yük ilerlemeyi</span><span class="sxs-lookup"><span data-stu-id="6c6d6-163">4.3 Track the load progress</span></span>
<span data-ttu-id="6c6d6-164">Dinamik Yönetim görünümlerini (Dmv'leri) kullanarak yük ilerlemesini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-164">You can track the progress of your load using dynamic management views (DMVs).</span></span> 

```sql
-- To see all requests
SELECT * FROM sys.dm_pdw_exec_requests;

-- To see a particular request identified by its label
SELECT * FROM sys.dm_pdw_exec_requests as r
WHERE r.[label] = 'CTAS : Load [cso].[DimProduct]             '
      OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
;

-- To track bytes and files
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

## <a name="5-optimize-columnstore-compression"></a><span data-ttu-id="6c6d6-165">5. Columnstore sıkıştırma en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="6c6d6-165">5. Optimize columnstore compression</span></span>
<span data-ttu-id="6c6d6-166">Varsayılan olarak, SQL Data Warehouse kümelenmiş columnstore dizini tablo depolar.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-166">By default, SQL Data Warehouse stores the table as a clustered columnstore index.</span></span> <span data-ttu-id="6c6d6-167">Yükleme tamamlandıktan sonra bazı veriler satır columnstore sıkıştırılır değil.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-167">After a load completes, some of the data rows might not be compressed into the columnstore.</span></span>  <span data-ttu-id="6c6d6-168">Çeşitli nedenlerle oluşabilir neden yoktur.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-168">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="6c6d6-169">Daha fazla bilgi için bkz: [columnstore dizinleri yönetmek][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="6c6d6-169">To learn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="6c6d6-170">Sorgu performansı ve yük sonra columnstore sıkıştırma iyileştirmek için tüm satırların sıkıştırılacak columnstore dizinini zorlamak için tabloyu yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-170">To optimize query performance and columnstore compression after a load, rebuild the table to force the columnstore index to compress all the rows.</span></span> 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

<span data-ttu-id="6c6d6-171">Columnstore dizinleri koruma ile ilgili daha fazla bilgi için bkz: [columnstore dizinleri yönetmek] [ manage columnstore indexes] makalesi.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-171">For more information on maintaining columnstore indexes, see the [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="6-optimize-statistics"></a><span data-ttu-id="6c6d6-172">6. İstatistikleri en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="6c6d6-172">6. Optimize statistics</span></span>
<span data-ttu-id="6c6d6-173">Bir yük hemen sonra tek sütunlu istatistikler oluşturmak en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-173">It is best to create single-column statistics immediately after a load.</span></span> <span data-ttu-id="6c6d6-174">İstatistikleri için bazı seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-174">There are some choices for statistics.</span></span> <span data-ttu-id="6c6d6-175">Örneğin, her sütunda tek sütunlu İstatistikler oluşturursanız, tüm istatistikleri yeniden oluşturmak için uzun zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-175">For example, if you create single-column statistics on every column it might take a long time to rebuild all the statistics.</span></span> <span data-ttu-id="6c6d6-176">Belirli sütunları sorgu koşullarında yapmayacağınız biliyorsanız, bu sütunlarda oluşturma istatistikleri atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-176">If you know certain columns are not going to be in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="6c6d6-177">Tek sütunlu istatistikler her tablonun her sütunu üzerinde oluşturmaya karar verirseniz, saklı yordam kod örneği kullanabilirsiniz `prc_sqldw_create_stats` içinde [istatistikleri] [ statistics] makalesi.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-177">If you decide to create single-column statistics on every column of every table, you can use the stored procedure code sample `prc_sqldw_create_stats` in the [statistics][statistics] article.</span></span>

<span data-ttu-id="6c6d6-178">Aşağıdaki istatistikler oluşturmak için iyi bir başlangıç noktası örnektir.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-178">The following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="6c6d6-179">Her sütunun Boyut tablosuna ve olgu tabloları katılan her sütunda tek sütunlu İstatistikler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-179">It creates single-column statistics on each column in the dimension table, and on each joining column in the fact tables.</span></span> <span data-ttu-id="6c6d6-180">Her zaman tek veya birden çok sütun istatistikleri diğer olgu tablo sütunları daha sonra ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-180">You can always add single or multi-column statistics to other fact table columns later on.</span></span>

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

## <a name="achievement-unlocked"></a><span data-ttu-id="6c6d6-181">Kilidi başarı!</span><span class="sxs-lookup"><span data-stu-id="6c6d6-181">Achievement unlocked!</span></span>
<span data-ttu-id="6c6d6-182">Azure SQL Data Warehouse'a ortak veri başarıyla yüklemiş olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="6c6d6-182">You have successfully loaded public data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="6c6d6-183">Harika iş!</span><span class="sxs-lookup"><span data-stu-id="6c6d6-183">Great job!</span></span>

<span data-ttu-id="6c6d6-184">Şimdi, aşağıdakiler gibi sorguları kullanarak tabloları sorgulama başlatabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6c6d6-184">You can now start querying the tables using queries like the following:</span></span>

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a><span data-ttu-id="6c6d6-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6c6d6-185">Next steps</span></span>
<span data-ttu-id="6c6d6-186">Tam Contoso perakende veri ambarı veri yüklemek için komut dosyasında daha fazla geliştirme ipuçları için bkz [SQL Data Warehouse geliştirmeye genel bakış][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="6c6d6-186">To load the full Contoso Retail Data Warehouse data, use the script in For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
[Load the full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
