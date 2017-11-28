---
title: "SQL Server'dan Azure SQL Veri Ambarı'na (PolyBase) veri yükleme | Microsoft Belgeleri"
description: "SQL Server'dan düz dosyalara veri aktarmak için bcp'yi, Azure blob depolama alanına veri aktarmak için AZCopy'yi ve verileri Azure SQL Data Warehouse'a almak için PolyBase'i kullanın."
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
ms.openlocfilehash: 966100094f98bae41bf90df500d005fa78b31ec3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a><span data-ttu-id="d06dd-103">SQL Data Warehouse'da PolyBase ile veri yükleme</span><span class="sxs-lookup"><span data-stu-id="d06dd-103">Load data with PolyBase in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d06dd-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="d06dd-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="d06dd-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="d06dd-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="d06dd-106">bcp</span><span class="sxs-lookup"><span data-stu-id="d06dd-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="d06dd-107">Bu öğreticide, AzCopy ve PolyBase kullanarak SQL Data Warehouse'a nasıl veri yükleyeceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d06dd-107">This tutorial shows how to load data into SQL Data Warehouse by using AzCopy and PolyBase.</span></span> <span data-ttu-id="d06dd-108">Öğreticiyi tamamladığınızda şunları öğrenmiş olacaksınız:</span><span class="sxs-lookup"><span data-stu-id="d06dd-108">When finished, you will know how to:</span></span>

* <span data-ttu-id="d06dd-109">AzCopy kullanarak Azure blob depolama alanına veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="d06dd-109">Use AzCopy to copy data to Azure blob storage</span></span>
* <span data-ttu-id="d06dd-110">Verileri tanımlamak için veritabanı nesneleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="d06dd-110">Create database objects to define the data</span></span>
* <span data-ttu-id="d06dd-111">T-SQL sorgusu çalıştırarak veri yükleme</span><span class="sxs-lookup"><span data-stu-id="d06dd-111">Run a T-SQL query to load the data</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d06dd-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d06dd-112">Prerequisites</span></span>
<span data-ttu-id="d06dd-113">Bu öğreticide ilerleyebilmeniz için, şunlar gereklidir:</span><span class="sxs-lookup"><span data-stu-id="d06dd-113">To step through this tutorial, you need</span></span>

* <span data-ttu-id="d06dd-114">SQL Data Warehouse veritabanı.</span><span class="sxs-lookup"><span data-stu-id="d06dd-114">A SQL Data Warehouse database.</span></span>
* <span data-ttu-id="d06dd-115">Standart Yerel Olarak Yedekli Depolama (Standard-LRS), Standart Coğrafi Olarak Yedekli Depolama (Standard-GRS), veya Standart Okuma Erişimli Coğrafi Olarak Yedekli Depolama (Standard-RAGRS) türünde bir Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="d06dd-115">An Azure storage account of type Standard Locally Redundant Storage (Standard-LRS), Standard Geo-Redundant Storage (Standard-GRS), or Standard Read-Access Geo-Redundant Storage (Standard-RAGRS).</span></span>
* <span data-ttu-id="d06dd-116">AzCopy Komut Satırı Yardımcı Programı</span><span class="sxs-lookup"><span data-stu-id="d06dd-116">AzCopy Command-Line Utility.</span></span> <span data-ttu-id="d06dd-117">Microsoft Azure Depolama Araçları ile birlikte yüklenen [en güncel AzCopy sürümünü][latest version of AzCopy] indirip yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d06dd-117">Download and install the [latest version of AzCopy][latest version of AzCopy] which is installed with the Microsoft Azure Storage Tools.</span></span>
  
    ![Azure Storage Araçları](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-to-azure-blob-storage"></a><span data-ttu-id="d06dd-119">1. Adım: Azure blob depolama alanına örnek veri ekleme</span><span class="sxs-lookup"><span data-stu-id="d06dd-119">Step 1: Add sample data to Azure blob storage</span></span>
<span data-ttu-id="d06dd-120">Veri yüklemek için Azure blob depolama alanına birkaç örnek veri eklememiz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d06dd-120">In order to load data, we need to put some sample data into an Azure blob storage.</span></span> <span data-ttu-id="d06dd-121">Bu adımda bir Azure Storage blobunu örnek verilerle dolduracağız.</span><span class="sxs-lookup"><span data-stu-id="d06dd-121">In this step we populate an Azure Storage blob with sample data.</span></span> <span data-ttu-id="d06dd-122">Daha sonra PolyBase kullanarak bu örnek verileri SQL Data Warehouse veritabanınıza yükleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="d06dd-122">Later, we will use PolyBase to load this sample data into your SQL Data Warehouse database.</span></span>

### <a name="a-prepare-a-sample-text-file"></a><span data-ttu-id="d06dd-123">A.</span><span class="sxs-lookup"><span data-stu-id="d06dd-123">A.</span></span> <span data-ttu-id="d06dd-124">Örnek metin dosyası hazırlama</span><span class="sxs-lookup"><span data-stu-id="d06dd-124">Prepare a sample text file</span></span>
<span data-ttu-id="d06dd-125">Örnek metin dosyası hazırlamak için şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="d06dd-125">To prepare a sample text file:</span></span>

1. <span data-ttu-id="d06dd-126">Not Defteri'ni açın ve aşağıdaki veri satırlarını yeni bir dosyaya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d06dd-126">Open Notepad and copy the following lines of data into a new file.</span></span> <span data-ttu-id="d06dd-127">Bu dosyayı yerel geçici dizininize %temp%\DimDate2.txt olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d06dd-127">Save this to your local temp directory as %temp%\DimDate2.txt.</span></span>

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

### <a name="b-find-your-blob-service-endpoint"></a><span data-ttu-id="d06dd-128">B.</span><span class="sxs-lookup"><span data-stu-id="d06dd-128">B.</span></span> <span data-ttu-id="d06dd-129">Blob hizmeti uç noktanızı bulma</span><span class="sxs-lookup"><span data-stu-id="d06dd-129">Find your blob service endpoint</span></span>
<span data-ttu-id="d06dd-130">Blob hizmeti uç noktanızı bulmak için şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="d06dd-130">To find your blob service endpoint:</span></span>

1. <span data-ttu-id="d06dd-131">Azure Portal'dan **Gözat** > **Storage Hesapları**'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="d06dd-131">From the Azure Portal select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="d06dd-132">Kullanmak istediğiniz depolama hesabına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d06dd-132">Click the storage account you want to use.</span></span>
3. <span data-ttu-id="d06dd-133">Depolama hesabı dikey penceresinde Bloblar'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d06dd-133">In the Storage account blade, click Blobs</span></span>
   
    ![Bloblar'a tıklayın](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. <span data-ttu-id="d06dd-135">Blob hizmeti uç nokta URL'nizi daha sonra kullanmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d06dd-135">Save your blob service endpoint URL for later.</span></span>
   
    ![Blob hizmeti uç noktası](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a><span data-ttu-id="d06dd-137">C.</span><span class="sxs-lookup"><span data-stu-id="d06dd-137">C.</span></span> <span data-ttu-id="d06dd-138">Azure depolama anahtarınızı bulma</span><span class="sxs-lookup"><span data-stu-id="d06dd-138">Find your Azure storage key</span></span>
<span data-ttu-id="d06dd-139">Azure depolama anahtarınızı bulmak için şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="d06dd-139">To find your Azure storage key:</span></span>

1. <span data-ttu-id="d06dd-140">Azure Portal'dan, **Gözat** > **Storage Hesapları**'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="d06dd-140">From the Azure Portal, select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="d06dd-141">Kullanmak istediğiniz depolama hesabına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d06dd-141">Click on the storage account you want to use.</span></span>
3. <span data-ttu-id="d06dd-142">**Tüm ayarlar** > **Erişim anahtarları** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d06dd-142">Select **All settings** > **Access keys**.</span></span>
4. <span data-ttu-id="d06dd-143">Erişim anahtarlarınızdan birini panoya kopyalamak için kopyalama kutusuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d06dd-143">Click the copy box to copy one of your access keys to the clipboard.</span></span>
   
    ![Azure depolama anahtarını kopyalama](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-the-sample-file-to-azure-blob-storage"></a><span data-ttu-id="d06dd-145">D.</span><span class="sxs-lookup"><span data-stu-id="d06dd-145">D.</span></span> <span data-ttu-id="d06dd-146">Örnek dosyayı Azure blob depolama alanına kopyalama</span><span class="sxs-lookup"><span data-stu-id="d06dd-146">Copy the sample file to Azure blob storage</span></span>
<span data-ttu-id="d06dd-147">Verilerinizi Azure blob depolama alanına kopyalamak için şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="d06dd-147">To copy your data to Azure blob storage:</span></span>

1. <span data-ttu-id="d06dd-148">Bir komut istemi açın ve dizinleri AzCopy yükleme dizini olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d06dd-148">Open a command prompt, and change directories to the AzCopy installation directory.</span></span> <span data-ttu-id="d06dd-149">Bu komut, 64 bit Windows istemcisinde varsayılan yükleme dizinine değiştirme işlemini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="d06dd-149">This command changes to the default installation directory on a 64-bit Windows client.</span></span>
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. <span data-ttu-id="d06dd-150">Dosyayı karşıya yüklemek için aşağıdaki şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d06dd-150">Run the following command to upload the file.</span></span> <span data-ttu-id="d06dd-151"><blob service endpoint URL> için blob hizmeti uç nokta URL'nizi ve <azure_storage_account_key> için Azure depolama hesabı anahtarınızı belirtin.</span><span class="sxs-lookup"><span data-stu-id="d06dd-151">Specify your blob service endpoint URL for <blob service endpoint URL> and your Azure storage account key for <azure_storage_account_key>.</span></span>
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

<span data-ttu-id="d06dd-152">Ayrıca bkz. [AzCopy Komut Satırı Yardımcı Programı ile Çalışmaya Başlama][latest version of AzCopy].</span><span class="sxs-lookup"><span data-stu-id="d06dd-152">See also [Getting Started with the AzCopy Command-Line Utility][latest version of AzCopy].</span></span>

### <a name="e-explore-your-blob-storage-container"></a><span data-ttu-id="d06dd-153">E.</span><span class="sxs-lookup"><span data-stu-id="d06dd-153">E.</span></span> <span data-ttu-id="d06dd-154">Blob depolama kapsayıcınızı araştırma</span><span class="sxs-lookup"><span data-stu-id="d06dd-154">Explore your blob storage container</span></span>
<span data-ttu-id="d06dd-155">Blob depolama alanına yüklediğiniz dosyayı görmek için şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="d06dd-155">To see the file you uploaded to blob storage:</span></span>

1. <span data-ttu-id="d06dd-156">Blob hizmeti dikey pencerenize geri dönün.</span><span class="sxs-lookup"><span data-stu-id="d06dd-156">Go back to your Blob service blade.</span></span>
2. <span data-ttu-id="d06dd-157">Kapsayıcılar'ın altında bulunan **datacontainer** öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d06dd-157">Under Containers, double-click **datacontainer**.</span></span>
3. <span data-ttu-id="d06dd-158">Verilerinizin yolunu keşfetmek için **datedimension** klasörüne tıkladığınızda karşıya yüklediğiniz **DimDate2.txt** dosyasıyla karşılaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="d06dd-158">To explore the path to your data, click the folder **datedimension** and you will see your uploaded file **DimDate2.txt**.</span></span>
4. <span data-ttu-id="d06dd-159">Özellikleri görüntülemek için **DimDate2.txt** dosyasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d06dd-159">To view properties, click **DimDate2.txt**.</span></span>
5. <span data-ttu-id="d06dd-160">Blob özellikleri dikey penceresinde dosya indirme ve dosya silme işlemlerini gerçekleştirebileceğinizi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d06dd-160">Note that in the Blob properties blade, you can download or delete the file.</span></span>
   
    ![Azure depolama blobunu görüntüleme](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-the-sample-data"></a><span data-ttu-id="d06dd-162">2. Adım: Örnek veriler için dış tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="d06dd-162">Step 2: Create an external table for the sample data</span></span>
<span data-ttu-id="d06dd-163">Bu bölümde örnek verileri tanımlayan bir dış tablo oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="d06dd-163">In this section we create an external table that defines the sample data.</span></span>

<span data-ttu-id="d06dd-164">PolyBase, Azure blob depolama alanındaki verilere erişmek için dış tabloları kullanır.</span><span class="sxs-lookup"><span data-stu-id="d06dd-164">PolyBase uses external tables to access data in Azure blob storage.</span></span> <span data-ttu-id="d06dd-165">Veriler SQL Data Warehouse'da depolanmadığı için PolyBase, dış veriler için kimlik doğrulaması gerçekleştirirken veritabanı kapsamlı bir kimlik bilgisi kullanır.</span><span class="sxs-lookup"><span data-stu-id="d06dd-165">Since the data is not stored within SQL Data Warehouse, PolyBase handles authentication to the external data by using a database-scoped credential.</span></span>

<span data-ttu-id="d06dd-166">Bu adımdaki örnekte, bir dış tablo oluşturmak için aşağıdaki Transact-SQL deyimleri kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d06dd-166">The example in this step uses these Transact-SQL statements to create an external table.</span></span>

* <span data-ttu-id="d06dd-167">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)]: Veritabanı kapsamlı kimlik bilgileri anahtarınızı şifrelemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d06dd-167">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] to encrypt the secret of your database scoped credential.</span></span>
* <span data-ttu-id="d06dd-168">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)]: Azure depolama hesabınız için kimlik doğrulama bilgilerinin belirtilmesi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d06dd-168">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] to specify authentication information for your Azure storage account.</span></span>
* <span data-ttu-id="d06dd-169">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)]: Azure blob depolama alanınızın konumunu belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d06dd-169">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] to specify the location of your Azure blob storage.</span></span>
* <span data-ttu-id="d06dd-170">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)]: Verilerinizin biçimini belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d06dd-170">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] to specify the format of your data.</span></span>
* <span data-ttu-id="d06dd-171">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)]: Tablo tanımını ve verilerin konumunu belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d06dd-171">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] to specify the table definition and location of the data.</span></span>

<span data-ttu-id="d06dd-172">Bu sorguyu SQL Data Warehouse veritabanınızda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d06dd-172">Run this query against your SQL Data Warehouse database.</span></span> <span data-ttu-id="d06dd-173">Bu sorgu, Azure blob depolama alanındaki DimDate2.txt örnek verilerini gösteren dbo şemasında DimDate2External adlı bir dış tablo oluşturacak.</span><span class="sxs-lookup"><span data-stu-id="d06dd-173">It will create an external table named DimDate2External in the dbo schema that points to the DimDate2.txt sample data in the Azure blob storage.</span></span>

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


-- D: Create an external file format
-- FORMAT_TYPE: Type of file format in Azure storage (supported: DELIMITEDTEXT, RCFILE, ORC, PARQUET).
-- FORMAT_OPTIONS: Specify field terminator, string delimiter, date format etc. for delimited text files.
-- Specify DATA_COMPRESSION method if data is compressed.

CREATE EXTERNAL FILE FORMAT TextFile
WITH (
    FORMAT_TYPE = DelimitedText,
    FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
);


-- E: Create the external table
-- Specify column names and data types. This needs to match the data in the sample file.
-- LOCATION: Specify path to file or directory that contains the data (relative to the blob container).
-- To point to all files under the blob container, use LOCATION='.'

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


-- Run a query on the external table

SELECT count(*) FROM dbo.DimDate2External;

```


<span data-ttu-id="d06dd-174">Visual Studio'da bulunan SQL Server Nesne Gezgini'nde dış dosya biçimini, dış veri kaynağını ve DimDate2External tablosunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d06dd-174">In SQL Server Object Explorer in Visual Studio, you can see the external file format, external data source, and the DimDate2External table.</span></span>

![Dış tabloyu görüntüleme](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a><span data-ttu-id="d06dd-176">3. Adım: SQL Data Warehouse'a veri yükleme</span><span class="sxs-lookup"><span data-stu-id="d06dd-176">Step 3: Load data into SQL Data Warehouse</span></span>
<span data-ttu-id="d06dd-177">Dış tablo oluşturulduktan sonra verileri yeni bir tabloya yükleyebilir veya var olan bir tabloya ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d06dd-177">Once the external table is created, you can either load the data into a new table or insert it into an existing table.</span></span>

* <span data-ttu-id="d06dd-178">Verileri yeni bir tabloya yüklemek için [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] deyimini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d06dd-178">To load the data into a new table, run the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="d06dd-179">Yeni tablo, sorguda adlandırılan sütunları içerir.</span><span class="sxs-lookup"><span data-stu-id="d06dd-179">The new table will have the columns named in the query.</span></span> <span data-ttu-id="d06dd-180">Sütunların veri türleri, dış tablo tanımındaki veri türleriyle eşleşir.</span><span class="sxs-lookup"><span data-stu-id="d06dd-180">The data types of the columns will match the data types in the external table definition.</span></span>
* <span data-ttu-id="d06dd-181">Verileri, var olan bir tabloya yüklemek için [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] deyimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d06dd-181">To load the data into an existing table, use the [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] statement.</span></span>

```sql
-- Load the data from Azure blob storage to SQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="d06dd-182">4. Adım: Yeni yüklenmiş verilerinize ilişkin istatistikler oluşturma</span><span class="sxs-lookup"><span data-stu-id="d06dd-182">Step 4: Create statistics on your newly loaded data</span></span>
<span data-ttu-id="d06dd-183">SQL Data Warehouse, istatistikleri otomatik olarak oluşturup güncelleştirmez.</span><span class="sxs-lookup"><span data-stu-id="d06dd-183">SQL Data Warehouse does not auto-create or auto-update statistics.</span></span> <span data-ttu-id="d06dd-184">Bu nedenle yüksek sorgu performansı elde etmek için ilk yükleme işleminden sonra her tablonun her sütunu için istatistik oluşturulması önemlidir.</span><span class="sxs-lookup"><span data-stu-id="d06dd-184">Therefore, to achieve high query performance, it's important to create statistics on each column of each table after the first load.</span></span> <span data-ttu-id="d06dd-185">Ayrıca veriler üzerinde önemli değişiklikler yapıldıktan sonra istatistiklerin güncelleştirilmesi de önemlidir.</span><span class="sxs-lookup"><span data-stu-id="d06dd-185">It's also important to update statistics after substantial changes in the data.</span></span>

<span data-ttu-id="d06dd-186">Bu örnekte, yeni DimDate2 tablosuna ilişkin tek sütunlu istatistikler oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="d06dd-186">This example creates single-column statistics on the new DimDate2 table.</span></span>

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

<span data-ttu-id="d06dd-187">Daha fazla bilgi edinmek için bkz. [İstatistikler][Statistics].</span><span class="sxs-lookup"><span data-stu-id="d06dd-187">To learn more, see [Statistics][Statistics].</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d06dd-188">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d06dd-188">Next steps</span></span>
<span data-ttu-id="d06dd-189">PolyBase kullanan bir çözüm geliştirirken bilmeniz gereken daha fazla bilgi için bkz. [PolyBase kılavuzu][PolyBase guide].</span><span class="sxs-lookup"><span data-stu-id="d06dd-189">See the [PolyBase guide][PolyBase guide] for further information you should know as you develop a solution that uses PolyBase.</span></span>

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
