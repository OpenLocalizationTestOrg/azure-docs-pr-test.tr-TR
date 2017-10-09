---
title: Azure SQL Data Warehouse'a (PolyBase) SQL Server'a aaaLoad verilerden | Microsoft Docs
description: "SQL Server tooflat dosyaları, AZCopy tooimport veri tooAzure blob depolama ve PolyBase tooingest hello veri BCP tooexport verilerini Azure SQL Data Warehouse'a kullanır."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 860c86e0-90f7-492c-9a84-1bdd3d1735cd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1346fb016e0538a44426671bf4e29358cb24f7ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a><span data-ttu-id="62870-103">SQL Data Warehouse'da PolyBase ile veri yükleme</span><span class="sxs-lookup"><span data-stu-id="62870-103">Load data with PolyBase in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="62870-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="62870-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="62870-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="62870-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="62870-106">bcp</span><span class="sxs-lookup"><span data-stu-id="62870-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="62870-107">Bu öğreticide gösterilmiştir nasıl AzCopy ve PolyBase kullanarak SQL Data Warehouse verilerini tooload.</span><span class="sxs-lookup"><span data-stu-id="62870-107">This tutorial shows how tooload data into SQL Data Warehouse by using AzCopy and PolyBase.</span></span> <span data-ttu-id="62870-108">Öğreticiyi tamamladığınızda şunları öğrenmiş olacaksınız:</span><span class="sxs-lookup"><span data-stu-id="62870-108">When finished, you will know how to:</span></span>

* <span data-ttu-id="62870-109">AzCopy toocopy veri tooAzure blob storage kullanma</span><span class="sxs-lookup"><span data-stu-id="62870-109">Use AzCopy toocopy data tooAzure blob storage</span></span>
* <span data-ttu-id="62870-110">Toodefine hello veri veritabanı nesneleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="62870-110">Create database objects toodefine hello data</span></span>
* <span data-ttu-id="62870-111">Bir T-SQL sorgusu tooload hello veri çalıştırın</span><span class="sxs-lookup"><span data-stu-id="62870-111">Run a T-SQL query tooload hello data</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="62870-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="62870-112">Prerequisites</span></span>
<span data-ttu-id="62870-113">toostep Bu öğreticide, gerekir</span><span class="sxs-lookup"><span data-stu-id="62870-113">toostep through this tutorial, you need</span></span>

* <span data-ttu-id="62870-114">SQL Data Warehouse veritabanı.</span><span class="sxs-lookup"><span data-stu-id="62870-114">A SQL Data Warehouse database.</span></span>
* <span data-ttu-id="62870-115">Standart Yerel Olarak Yedekli Depolama (Standard-LRS), Standart Coğrafi Olarak Yedekli Depolama (Standard-GRS), veya Standart Okuma Erişimli Coğrafi Olarak Yedekli Depolama (Standard-RAGRS) türünde bir Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="62870-115">An Azure storage account of type Standard Locally Redundant Storage (Standard-LRS), Standard Geo-Redundant Storage (Standard-GRS), or Standard Read-Access Geo-Redundant Storage (Standard-RAGRS).</span></span>
* <span data-ttu-id="62870-116">AzCopy Komut Satırı Yardımcı Programı</span><span class="sxs-lookup"><span data-stu-id="62870-116">AzCopy Command-Line Utility.</span></span> <span data-ttu-id="62870-117">Merhaba yükleyip [en güncel AzCopy sürümünü] [ latest version of AzCopy] hello Microsoft Azure Storage araçları ile yüklenir.</span><span class="sxs-lookup"><span data-stu-id="62870-117">Download and install hello [latest version of AzCopy][latest version of AzCopy] which is installed with hello Microsoft Azure Storage Tools.</span></span>
  
    ![Azure Storage Araçları](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a><span data-ttu-id="62870-119">1. adım: örnek veri tooAzure blob depolama ekleme</span><span class="sxs-lookup"><span data-stu-id="62870-119">Step 1: Add sample data tooAzure blob storage</span></span>
<span data-ttu-id="62870-120">Sipariş tooload verilerde tooput bazı örnek veriler Azure blob depolama alanına ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="62870-120">In order tooload data, we need tooput some sample data into an Azure blob storage.</span></span> <span data-ttu-id="62870-121">Bu adımda bir Azure Storage blobunu örnek verilerle dolduracağız.</span><span class="sxs-lookup"><span data-stu-id="62870-121">In this step we populate an Azure Storage blob with sample data.</span></span> <span data-ttu-id="62870-122">Daha sonra PolyBase tooload Bu örnek verileri SQL Data Warehouse veritabanınıza kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="62870-122">Later, we will use PolyBase tooload this sample data into your SQL Data Warehouse database.</span></span>

### <a name="a-prepare-a-sample-text-file"></a><span data-ttu-id="62870-123">A.</span><span class="sxs-lookup"><span data-stu-id="62870-123">A.</span></span> <span data-ttu-id="62870-124">Örnek metin dosyası hazırlama</span><span class="sxs-lookup"><span data-stu-id="62870-124">Prepare a sample text file</span></span>
<span data-ttu-id="62870-125">tooprepare örnek bir metin dosyası:</span><span class="sxs-lookup"><span data-stu-id="62870-125">tooprepare a sample text file:</span></span>

1. <span data-ttu-id="62870-126">Veri satırlarını yeni bir dosyaya aşağıdaki not defteri ve kopyalama hello açın.</span><span class="sxs-lookup"><span data-stu-id="62870-126">Open Notepad and copy hello following lines of data into a new file.</span></span> <span data-ttu-id="62870-127">Bu tooyour yerel geçici dizin Temp%\DimDate2.txt olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="62870-127">Save this tooyour local temp directory as %temp%\DimDate2.txt.</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="b-find-your-blob-service-endpoint"></a><span data-ttu-id="62870-128">B.</span><span class="sxs-lookup"><span data-stu-id="62870-128">B.</span></span> <span data-ttu-id="62870-129">Blob hizmeti uç noktanızı bulma</span><span class="sxs-lookup"><span data-stu-id="62870-129">Find your blob service endpoint</span></span>
<span data-ttu-id="62870-130">toofind, blob Hizmeti uç noktası:</span><span class="sxs-lookup"><span data-stu-id="62870-130">toofind your blob service endpoint:</span></span>

1. <span data-ttu-id="62870-131">Hello Azure Portalı ' seçin **Gözat** > **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="62870-131">From hello Azure Portal select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="62870-132">Toouse istediğiniz hello depolama hesabını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="62870-132">Click hello storage account you want toouse.</span></span>
3. <span data-ttu-id="62870-133">Merhaba depolama hesabı dikey penceresinde Bloblar'a tıklayın</span><span class="sxs-lookup"><span data-stu-id="62870-133">In hello Storage account blade, click Blobs</span></span>
   
    ![Bloblar'a tıklayın](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. <span data-ttu-id="62870-135">Blob hizmeti uç nokta URL'nizi daha sonra kullanmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="62870-135">Save your blob service endpoint URL for later.</span></span>
   
    ![Blob hizmeti uç noktası](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a><span data-ttu-id="62870-137">C.</span><span class="sxs-lookup"><span data-stu-id="62870-137">C.</span></span> <span data-ttu-id="62870-138">Azure depolama anahtarınızı bulma</span><span class="sxs-lookup"><span data-stu-id="62870-138">Find your Azure storage key</span></span>
<span data-ttu-id="62870-139">toofind Azure depolama anahtarınızı:</span><span class="sxs-lookup"><span data-stu-id="62870-139">toofind your Azure storage key:</span></span>

1. <span data-ttu-id="62870-140">Hello Azure Portalı ' seçin **Gözat** > **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="62870-140">From hello Azure Portal, select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="62870-141">Toouse istediğiniz hello depolama hesabına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62870-141">Click on hello storage account you want toouse.</span></span>
3. <span data-ttu-id="62870-142">**Tüm ayarlar** > **Erişim anahtarları** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="62870-142">Select **All settings** > **Access keys**.</span></span>
4. <span data-ttu-id="62870-143">Merhaba kopyalama kutusunu toocopy erişim anahtarları toohello panonuza birini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="62870-143">Click hello copy box toocopy one of your access keys toohello clipboard.</span></span>
   
    ![Azure depolama anahtarını kopyalama](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a><span data-ttu-id="62870-145">D.</span><span class="sxs-lookup"><span data-stu-id="62870-145">D.</span></span> <span data-ttu-id="62870-146">Merhaba örnek dosya tooAzure blob depolama kopyalama</span><span class="sxs-lookup"><span data-stu-id="62870-146">Copy hello sample file tooAzure blob storage</span></span>
<span data-ttu-id="62870-147">toocopy veri tooAzure blob depolama alanınızın:</span><span class="sxs-lookup"><span data-stu-id="62870-147">toocopy your data tooAzure blob storage:</span></span>

1. <span data-ttu-id="62870-148">Bir komut istemi açın ve dizinleri toohello AzCopy yükleme dizini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="62870-148">Open a command prompt, and change directories toohello AzCopy installation directory.</span></span> <span data-ttu-id="62870-149">Bu komut, bir 64-bit Windows istemcisinde varsayılan yükleme dizini toohello değiştirir.</span><span class="sxs-lookup"><span data-stu-id="62870-149">This command changes toohello default installation directory on a 64-bit Windows client.</span></span>
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. <span data-ttu-id="62870-150">Aşağıdaki komut tooupload hello dosyasına hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="62870-150">Run hello following command tooupload hello file.</span></span> <span data-ttu-id="62870-151"><blob service endpoint URL> için blob hizmeti uç nokta URL'nizi ve <azure_storage_account_key> için Azure depolama hesabı anahtarınızı belirtin.</span><span class="sxs-lookup"><span data-stu-id="62870-151">Specify your blob service endpoint URL for <blob service endpoint URL> and your Azure storage account key for <azure_storage_account_key>.</span></span>
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

<span data-ttu-id="62870-152">Ayrıca bkz. [hello AzCopy komut satırı yardımcı programı ile çalışmaya başlama][latest version of AzCopy].</span><span class="sxs-lookup"><span data-stu-id="62870-152">See also [Getting Started with hello AzCopy Command-Line Utility][latest version of AzCopy].</span></span>

### <a name="e-explore-your-blob-storage-container"></a><span data-ttu-id="62870-153">E.</span><span class="sxs-lookup"><span data-stu-id="62870-153">E.</span></span> <span data-ttu-id="62870-154">Blob depolama kapsayıcınızı araştırma</span><span class="sxs-lookup"><span data-stu-id="62870-154">Explore your blob storage container</span></span>
<span data-ttu-id="62870-155">toosee hello dosyası tooblob depolama yüklenir:</span><span class="sxs-lookup"><span data-stu-id="62870-155">toosee hello file you uploaded tooblob storage:</span></span>

1. <span data-ttu-id="62870-156">Tooyour Blob hizmeti dikey penceresine geri dönün.</span><span class="sxs-lookup"><span data-stu-id="62870-156">Go back tooyour Blob service blade.</span></span>
2. <span data-ttu-id="62870-157">Kapsayıcılar'ın altında bulunan **datacontainer** öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62870-157">Under Containers, double-click **datacontainer**.</span></span>
3. <span data-ttu-id="62870-158">tooexplore hello yolu tooyour verisi hello klasörü tıklatın **datedimension** ve karşıya yüklenen dosyanızı görürsünüz **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="62870-158">tooexplore hello path tooyour data, click hello folder **datedimension** and you will see your uploaded file **DimDate2.txt**.</span></span>
4. <span data-ttu-id="62870-159">tooview Özellikler **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="62870-159">tooview properties, click **DimDate2.txt**.</span></span>
5. <span data-ttu-id="62870-160">Merhaba Blob özellikleri dikey penceresinde yükleyebileceğiniz veya hello dosyasını silin, unutmayın.</span><span class="sxs-lookup"><span data-stu-id="62870-160">Note that in hello Blob properties blade, you can download or delete hello file.</span></span>
   
    ![Azure depolama blobunu görüntüleme](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a><span data-ttu-id="62870-162">2. adım: hello örnek veriler için bir dış tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="62870-162">Step 2: Create an external table for hello sample data</span></span>
<span data-ttu-id="62870-163">Bu bölümde hello örnek verileri tanımlayan bir dış tablo oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="62870-163">In this section we create an external table that defines hello sample data.</span></span>

<span data-ttu-id="62870-164">PolyBase, Azure blob depolama alanına dış tablolara tooaccess verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="62870-164">PolyBase uses external tables tooaccess data in Azure blob storage.</span></span> <span data-ttu-id="62870-165">Merhaba verileri SQL Data Warehouse içinde depolanmadığından PolyBase veritabanı kapsamlı bir kimlik bilgisi kullanarak kimlik doğrulaması toohello dış verileri işler.</span><span class="sxs-lookup"><span data-stu-id="62870-165">Since hello data is not stored within SQL Data Warehouse, PolyBase handles authentication toohello external data by using a database-scoped credential.</span></span>

<span data-ttu-id="62870-166">Bu adımda Hello örneği, bu Transact-SQL deyimleri toocreate bir dış tablo kullanır.</span><span class="sxs-lookup"><span data-stu-id="62870-166">hello example in this step uses these Transact-SQL statements toocreate an external table.</span></span>

* <span data-ttu-id="62870-167">[Ana anahtar (Transact-SQL) oluşturma] [ Create Master Key (Transact-SQL)] tooencrypt hello gizli veritabanı kapsamlı kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="62870-167">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] tooencrypt hello secret of your database scoped credential.</span></span>
* <span data-ttu-id="62870-168">[Database Scoped Credential (Transact-SQL) oluşturma] [ Create Database Scoped Credential (Transact-SQL)] Azure depolama hesabınızın toospecify kimlik doğrulama bilgileri.</span><span class="sxs-lookup"><span data-stu-id="62870-168">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] toospecify authentication information for your Azure storage account.</span></span>
* <span data-ttu-id="62870-169">[Dış veri kaynağı (Transact-SQL) oluşturun] [ Create External Data Source (Transact-SQL)] toospecify hello Azure blob depolama alanınızın konumunu.</span><span class="sxs-lookup"><span data-stu-id="62870-169">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] toospecify hello location of your Azure blob storage.</span></span>
* <span data-ttu-id="62870-170">[External File Format (Transact-SQL) oluşturma] [ Create External File Format (Transact-SQL)] verilerinizi toospecify hello biçimi.</span><span class="sxs-lookup"><span data-stu-id="62870-170">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] toospecify hello format of your data.</span></span>
* <span data-ttu-id="62870-171">[Dış Table (Transact-SQL) oluşturma] [ Create External Table (Transact-SQL)] toospecify hello tablo tanımı ve konumunu veri hello.</span><span class="sxs-lookup"><span data-stu-id="62870-171">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] toospecify hello table definition and location of hello data.</span></span>

<span data-ttu-id="62870-172">Bu sorguyu SQL Data Warehouse veritabanınızda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="62870-172">Run this query against your SQL Data Warehouse database.</span></span> <span data-ttu-id="62870-173">Hello Azure blob depolama alanına toohello DimDate2.txt örnek veri noktası hello dbo şemasında DimDate2External adlı bir dış tablo oluşturacak.</span><span class="sxs-lookup"><span data-stu-id="62870-173">It will create an external table named DimDate2External in hello dbo schema that points toohello DimDate2.txt sample data in hello Azure blob storage.</span></span>

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


-- D: Create an external file format
-- FORMAT_TYPE: Type of file format in Azure storage (supported: DELIMITEDTEXT, RCFILE, ORC, PARQUET).
-- FORMAT_OPTIONS: Specify field terminator, string delimiter, date format etc. for delimited text files.
-- Specify DATA_COMPRESSION method if data is compressed.

CREATE EXTERNAL FILE FORMAT TextFile
WITH (
    FORMAT_TYPE = DelimitedText,
    FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
);


-- E: Create hello external table
-- Specify column names and data types. This needs toomatch hello data in hello sample file.
-- LOCATION: Specify path toofile or directory that contains hello data (relative toohello blob container).
-- toopoint tooall files under hello blob container, use LOCATION='.'

CREATE EXTERNAL TABLE dbo.DimDate2External (
    DateId INT NOT NULL,
    CalendarQuarter TINYINT NOT NULL,
    FiscalQuarter TINYINT NOT NULL
)
WITH (
    LOCATION='/datedimension/',
    DATA_SOURCE=AzureStorage,
    FILE_FORMAT=TextFile
);


-- Run a query on hello external table

SELECT count(*) FROM dbo.DimDate2External;

```


<span data-ttu-id="62870-174">SQL Server nesne Gezgini'nde Visual Studio'da, hello dış dosya biçimini, dış veri kaynağına ve hello DimDate2External tablosunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62870-174">In SQL Server Object Explorer in Visual Studio, you can see hello external file format, external data source, and hello DimDate2External table.</span></span>

![Dış tabloyu görüntüleme](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a><span data-ttu-id="62870-176">3. Adım: SQL Data Warehouse'a veri yükleme</span><span class="sxs-lookup"><span data-stu-id="62870-176">Step 3: Load data into SQL Data Warehouse</span></span>
<span data-ttu-id="62870-177">Hello dış tablo oluşturulduktan sonra yeni bir tabloya hello verileri yüklemek veya var olan bir tabloya ekle.</span><span class="sxs-lookup"><span data-stu-id="62870-177">Once hello external table is created, you can either load hello data into a new table or insert it into an existing table.</span></span>

* <span data-ttu-id="62870-178">Merhaba çalıştıran yeni bir tabloya tooload hello veri [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] deyimi.</span><span class="sxs-lookup"><span data-stu-id="62870-178">tooload hello data into a new table, run hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="62870-179">Merhaba yeni tablo hello sorguda adlandırılan hello sütunları içerir.</span><span class="sxs-lookup"><span data-stu-id="62870-179">hello new table will have hello columns named in hello query.</span></span> <span data-ttu-id="62870-180">hello sütunların veri türlerini Hello hello dış tablo tanımındaki hello veri türleri ile eşleşir.</span><span class="sxs-lookup"><span data-stu-id="62870-180">hello data types of hello columns will match hello data types in hello external table definition.</span></span>
* <span data-ttu-id="62870-181">var olan bir tabloya tooload hello verileri kullanmak hello [Ekle... SELECT (Transact-SQL)] [ INSERT...SELECT (Transact-SQL)] deyimi.</span><span class="sxs-lookup"><span data-stu-id="62870-181">tooload hello data into an existing table, use hello [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] statement.</span></span>

```sql
-- Load hello data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="62870-182">4. Adım: Yeni yüklenmiş verilerinize ilişkin istatistikler oluşturma</span><span class="sxs-lookup"><span data-stu-id="62870-182">Step 4: Create statistics on your newly loaded data</span></span>
<span data-ttu-id="62870-183">SQL Data Warehouse, istatistikleri otomatik olarak oluşturup güncelleştirmez.</span><span class="sxs-lookup"><span data-stu-id="62870-183">SQL Data Warehouse does not auto-create or auto-update statistics.</span></span> <span data-ttu-id="62870-184">Bu nedenle, tooachieve yüksek sorgu performansı hello sonra her tablonun her sütunu toocreate istatistik ilk yük önem taşır.</span><span class="sxs-lookup"><span data-stu-id="62870-184">Therefore, tooachieve high query performance, it's important toocreate statistics on each column of each table after hello first load.</span></span> <span data-ttu-id="62870-185">Merhaba verilerdeki önemli değişiklikler yapıldıktan sonra önemli tooupdate istatistikleri de olur.</span><span class="sxs-lookup"><span data-stu-id="62870-185">It's also important tooupdate statistics after substantial changes in hello data.</span></span>

<span data-ttu-id="62870-186">Bu örnek hello yeni DimDate2 tablosunda tek sütunlu İstatistikler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="62870-186">This example creates single-column statistics on hello new DimDate2 table.</span></span>

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

<span data-ttu-id="62870-187">toolearn daha, fazla [istatistikleri][Statistics].</span><span class="sxs-lookup"><span data-stu-id="62870-187">toolearn more, see [Statistics][Statistics].</span></span>  

## <a name="next-steps"></a><span data-ttu-id="62870-188">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="62870-188">Next steps</span></span>
<span data-ttu-id="62870-189">Merhaba bkz [PolyBase Kılavuzu] [ PolyBase guide] PolyBase kullanan bir çözüm geliştirirken bilmeniz daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="62870-189">See hello [PolyBase guide][PolyBase guide] for further information you should know as you develop a solution that uses PolyBase.</span></span>

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
[latest version of AzCopy]:../storage/common/storage-use-azcopy.md

<!--External references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx


[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]:https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189450.aspx
