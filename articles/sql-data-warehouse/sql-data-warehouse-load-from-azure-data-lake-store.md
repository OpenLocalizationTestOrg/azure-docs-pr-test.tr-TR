---
title: "Yük - SQL veri ambarı için Azure Data Lake Store | Microsoft Docs"
description: "Azure Data Lake Deposu'ndan veri Azure SQL Data Warehouse'a veri yüklemek için PolyBase dış tablolara kullanmayı öğrenin."
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
ms.openlocfilehash: ab951c30aae0d4afdd931e245f25d4645bba1681
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a><span data-ttu-id="b8efe-103">Azure Data Lake Deposu'ndan veri SQL Data Warehouse'a veri yükleme</span><span class="sxs-lookup"><span data-stu-id="b8efe-103">Load data from Azure Data Lake Store into SQL Data Warehouse</span></span>
<span data-ttu-id="b8efe-104">Bu belge Polybase'i kullanarak kendi verilerinizi Azure veri Gölü deposu (ADLS) SQL Data Warehouse'a veri yüklemek için gereken tüm adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="b8efe-104">This document gives you all steps you  need to load your own data from Azure Data Lake Store (ADLS) into SQL Data Warehouse using PolyBase.</span></span>
<span data-ttu-id="b8efe-105">Geçici sorguları dış tablolara kullanarak ADLS içinde depolanan veriler üzerinde çalıştırmak mümkün olmakla birlikte, en iyi uygulama olarak SQL Data Warehouse'a veri aktarma öneririz.</span><span class="sxs-lookup"><span data-stu-id="b8efe-105">While you are able to run adhoc queries over the data stored in ADLS using the External Tables, as a best practice we suggest importing the data into the SQL Data Warehouse.</span></span>
<span data-ttu-id="b8efe-106">Tahmini süre: 10 ön koşullara sahip olduğu varsayılarak dakika tamamlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b8efe-106">Time Estimate: 10 minutes assuming you have the prerequisites need to complete.</span></span>
<span data-ttu-id="b8efe-107">Bu öğreticide şunları öğreneceksiniz nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="b8efe-107">In this tutorial you will learn how to:</span></span>

1. <span data-ttu-id="b8efe-108">Azure Data Lake Deposu'ndan veri yüklemek için dış veritabanı nesneleri oluşturma.</span><span class="sxs-lookup"><span data-stu-id="b8efe-108">Create External Database objects to load from Azure Data Lake Store.</span></span>
2. <span data-ttu-id="b8efe-109">Bir Azure Data Lake Store dizinine bağlanır.</span><span class="sxs-lookup"><span data-stu-id="b8efe-109">Connect to an Azure Data Lake Store Directory.</span></span>
3. <span data-ttu-id="b8efe-110">Azure SQL Data Warehouse'a veri yükleme.</span><span class="sxs-lookup"><span data-stu-id="b8efe-110">Load data into Azure SQL Data Warehouse.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b8efe-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="b8efe-111">Before you begin</span></span>
<span data-ttu-id="b8efe-112">Bu öğretici çalıştırmak için gerekir:</span><span class="sxs-lookup"><span data-stu-id="b8efe-112">To run this tutorial, you need:</span></span>

* <span data-ttu-id="b8efe-113">Azure Active Directory Hizmeti için kimlik doğrulaması için kullanılacak uygulama.</span><span class="sxs-lookup"><span data-stu-id="b8efe-113">Azure Active Directory Application to use for Service-to-Service authentication.</span></span> <span data-ttu-id="b8efe-114">Oluşturmak için izlemeniz [Active directory kimlik doğrulaması](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span><span class="sxs-lookup"><span data-stu-id="b8efe-114">To create, follow [Active directory authentication](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span></span>

>[!NOTE] 
> <span data-ttu-id="b8efe-115">İstemci kimliği, anahtar ve OAuth2.0 belirteç uç noktası değeri, uygulamanızın Active Directory, Azure Data Lake SQL veri ambarından bağlanmak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="b8efe-115">You need the client ID, Key, and OAuth2.0 Token Endpoint Value of your Active Directory Application to connect to your Azure Data Lake from SQL Data Warehouse.</span></span> <span data-ttu-id="b8efe-116">Bu değerleri alma ayrıntılarını yukarıdaki bağlantıyı ' dir.</span><span class="sxs-lookup"><span data-stu-id="b8efe-116">Details for how to get these values are in the link above.</span></span>
><span data-ttu-id="b8efe-117">Not Azure Active Directory Uygulama kaydı için istemci kimliği olarak 'Uygulama kimliği' kullanın</span><span class="sxs-lookup"><span data-stu-id="b8efe-117">Note for Azure Active Directory App Registration use the 'Application ID' as the Client ID.</span></span>

* <span data-ttu-id="b8efe-118">SQL Server Management Studio veya SQL Server veri araçları, SSMS karşıdan yüklemek ve bağlamak için bkz: [sorgu SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span><span class="sxs-lookup"><span data-stu-id="b8efe-118">SQL Server Management Studio or SQL Server Data Tools, to download SSMS and connect see [Query SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span></span>

* <span data-ttu-id="b8efe-119">Bir Azure SQL veri oluşturmak için bir izleyin deposu: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span><span class="sxs-lookup"><span data-stu-id="b8efe-119">An Azure SQL Data Warehouse, to create one follow: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span></span>

* <span data-ttu-id="b8efe-120">Bir Azure Data Lake Store, ile veya olmadan şifreleme etkin.</span><span class="sxs-lookup"><span data-stu-id="b8efe-120">An Azure Data Lake Store, with or without encryption enabled.</span></span> <span data-ttu-id="b8efe-121">Bir izleme oluşturmak için: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="b8efe-121">To create one follow: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span></span>




## <a name="configure-the-data-source"></a><span data-ttu-id="b8efe-122">Veri kaynağını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b8efe-122">Configure the data source</span></span>
<span data-ttu-id="b8efe-123">PolyBase, dış veri özniteliklerini ve konumunu tanımlamak için T-SQL dış nesneleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="b8efe-123">PolyBase uses T-SQL external objects to define the location and attributes of the external data.</span></span> <span data-ttu-id="b8efe-124">Dış nesneleri SQL veri ambarı'nda depolanır ve th harici olarak depolanan veriler başvuru.</span><span class="sxs-lookup"><span data-stu-id="b8efe-124">The external objects are stored in SQL Data Warehouse and reference the data th is stored externally.</span></span>


###  <a name="create-a-credential"></a><span data-ttu-id="b8efe-125">Bir kimlik bilgisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b8efe-125">Create a credential</span></span>
<span data-ttu-id="b8efe-126">Azure Data Lake Store erişmek için sonraki adımda kullanılan kimlik bilgileri gizli anahtarı şifrelemek için bir veritabanı ana anahtarı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b8efe-126">To access your Azure Data Lake Store, you will need to create a Database Master Key to encrypt your credential secret used in the next step.</span></span>
<span data-ttu-id="b8efe-127">AAD'de ayarlanmış hizmet asıl kimlik bilgilerini depolayan bir veritabanı kapsamlı kimlik bilgisi oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="b8efe-127">You then create a Database scoped credential, which stores the service principal credentials set up in AAD.</span></span> <span data-ttu-id="b8efe-128">Bu Windows Azure depolama BLOB'larını bağlamak için PolyBase kullanmış olduğunuz CREDENTIAL sözdizimi farklı olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b8efe-128">For those of you who have used PolyBase to connect to Windows Azure Storage Blobs, note that the credential syntax is different.</span></span>
<span data-ttu-id="b8efe-129">Azure Data Lake Store'a bağlanmak için yapmanız gerekir **ilk** Azure Active Directory uygulama oluşturmak, bir erişim anahtarı oluşturun ve Azure Data Lake kaynak uygulama erişimi verin.</span><span class="sxs-lookup"><span data-stu-id="b8efe-129">To connect to Azure Data Lake Store, you must **first** create an Azure Active Directory Application, create an access key, and grant the application access to the Azure Data Lake resource.</span></span> <span data-ttu-id="b8efe-130">Bu adımları gerçekleştirmek için Instrucitons konumlandırıldığını [burada](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span><span class="sxs-lookup"><span data-stu-id="b8efe-130">Instrucitons to perform these steps are located [here](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span></span>

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required to encrypt the credential secret in the next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass the client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
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


### <a name="create-the-external-data-source"></a><span data-ttu-id="b8efe-131">Dış veri kaynağı oluşturun</span><span class="sxs-lookup"><span data-stu-id="b8efe-131">Create the external data source</span></span>
<span data-ttu-id="b8efe-132">Bu [dış veri kaynağı oluştur] [ CREATE EXTERNAL DATA SOURCE] veri ve veri türü konumunu depolamak için komutu.</span><span class="sxs-lookup"><span data-stu-id="b8efe-132">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command to store the location of the data, and the type of data.</span></span>
<span data-ttu-id="b8efe-133">Azure portalı ve www.portal.azure.com ADL URI bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8efe-133">You can find the ADL URI in the Azure portal and www.portal.azure.com.</span></span>

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide the credential created in the previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a><span data-ttu-id="b8efe-134">Veri biçimini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="b8efe-134">Configure data format</span></span>
<span data-ttu-id="b8efe-135">ADLS veri almak için dış dosya biçimini belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b8efe-135">To import the data from ADLS, you need to specify the external file format.</span></span> <span data-ttu-id="b8efe-136">Bu komut, verilerinizi tanımlamak için biçim özgü seçenek vardır.</span><span class="sxs-lookup"><span data-stu-id="b8efe-136">This command has format-specific options to describe your data.</span></span>
<span data-ttu-id="b8efe-137">Bir kanal sınırlandırılmış metin dosyası bir sık kullanılan bir dosya biçimi örneği aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="b8efe-137">Below is an example of a commonly used file format that is a pipe-delimited text file.</span></span>
<span data-ttu-id="b8efe-138">Tam bir listesi için T-SQL belgelerimize bakın [oluşturmak dış dosya biçimi][CREATE EXTERNAL FILE FORMAT]</span><span class="sxs-lookup"><span data-stu-id="b8efe-138">Look at our T-SQL documentation for a complete list of [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span></span>

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks the end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies the field terminator for data of type string in the text-delimited file.
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

## <a name="create-the-external-tables"></a><span data-ttu-id="b8efe-139">Dış tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="b8efe-139">Create the external tables</span></span>
<span data-ttu-id="b8efe-140">Veri kaynağı ve dosya biçimi belirttiğiniz, dış tablo oluşturmak hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="b8efe-140">Now that you have specified the data source and file format, you are ready to create the external tables.</span></span> <span data-ttu-id="b8efe-141">Dış tablolar dış veri ile nasıl etkileşim değildir.</span><span class="sxs-lookup"><span data-stu-id="b8efe-141">External tables are how you interact with external data.</span></span> <span data-ttu-id="b8efe-142">PolyBase özyinelemeli dizin geçişi konumu parametresinde belirtilen dizinin tüm alt dizinler tüm dosyaları okumak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="b8efe-142">PolyBase uses recursive directory traversal to read all files in all subdirectories of the directory specified in the location parameter.</span></span> <span data-ttu-id="b8efe-143">Ayrıca, aşağıdaki örnekte nesnesinin nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b8efe-143">Also, the following example shows how to create the object.</span></span> <span data-ttu-id="b8efe-144">Sahip olduğunuz ADLS içinde verilerle çalışmak için bildirimini özelleştirerek gerekir.</span><span class="sxs-lookup"><span data-stu-id="b8efe-144">You need to customize the statement to work with the data you have in ADLS.</span></span>

```sql
-- D: Create an External Table
-- LOCATION: Folder under the ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object to use.
-- FILE_FORMAT: Specifies which File Format Object to use
-- REJECT_TYPE: Specifies how you want to deal with rejected rows. Either Value or percentage of the total
-- REJECT_VALUE: Sets the Reject value based on the reject type.

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

## <a name="external-table-considerations"></a><span data-ttu-id="b8efe-145">Dış tablo konuları</span><span class="sxs-lookup"><span data-stu-id="b8efe-145">External Table Considerations</span></span>
<span data-ttu-id="b8efe-146">Bir dış tablo oluşturmak kolaydır, ancak ele alınması gereken bazı küçük farklar vardır.</span><span class="sxs-lookup"><span data-stu-id="b8efe-146">Creating an external table is easy, but there are some nuances that need to be discussed.</span></span>

<span data-ttu-id="b8efe-147">PolyBase ile veri yükleme kesin türü belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="b8efe-147">Loading data with PolyBase is strongly typed.</span></span> <span data-ttu-id="b8efe-148">Başka bir deyişle, her alınan veri satırının tablo şeması tanımı karşılaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b8efe-148">This means that each row of the data being ingested must satisfy the table schema definition.</span></span>
<span data-ttu-id="b8efe-149">Belirli bir satır şema tanımı eşleşmiyorsa, satır yüklerinin reddedilir.</span><span class="sxs-lookup"><span data-stu-id="b8efe-149">If a given row does not match the schema definition, the row is rejected from the load.</span></span>

<span data-ttu-id="b8efe-150">REJECT_TYPE ve REJECT_VALUE seçenekleri, satır sayısını veya veri yüzdesini son tablosunda bulunmalıdır tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="b8efe-150">The REJECT_TYPE and REJECT_VALUE options allow you to define how many rows or what percentage of the data must be present in the final table.</span></span>
<span data-ttu-id="b8efe-151">Reddetme değerine ulaşılana yüklenmesi sırasında yükleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="b8efe-151">During load, if the reject value is reached, the load fails.</span></span> <span data-ttu-id="b8efe-152">Reddedilen satır en yaygın nedeni bir şema tanımı eşleşmemesidir.</span><span class="sxs-lookup"><span data-stu-id="b8efe-152">The most common cause of rejected rows is a schema definition mismatch.</span></span>
<span data-ttu-id="b8efe-153">Örneğin, veri dosyasındaki bir dize olduğunda bir sütunu int şeması yanlış verilirse, her satıra yüklemek başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="b8efe-153">For example, if a column is incorrectly given the schema of int when the data in the file is a string, every row will fail to load.</span></span>

<span data-ttu-id="b8efe-154">Konum verileri okumak istediğiniz en üstteki dizini belirtir.</span><span class="sxs-lookup"><span data-stu-id="b8efe-154">The Location specifies the topmost directory that you want to read data from.</span></span>
<span data-ttu-id="b8efe-155">Bu durumda, varsa /DimProduct/ PolyBase alt dizinler alt dizinleri içindeki tüm veri alın.</span><span class="sxs-lookup"><span data-stu-id="b8efe-155">In this case, if there were subdirectories under /DimProduct/ PolyBase would import all the data within the subdirectories.</span></span>

## <a name="load-the-data"></a><span data-ttu-id="b8efe-156">Verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="b8efe-156">Load the data</span></span>
<span data-ttu-id="b8efe-157">Azure Data Lake Store kullanımdan veri yüklemek için [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] deyimi.</span><span class="sxs-lookup"><span data-stu-id="b8efe-157">To load data from Azure Data Lake Store use the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="b8efe-158">Yükleme CTAS ile oluşturduğunuz kesin türü belirtilmiş dış tablo kullanır.</span><span class="sxs-lookup"><span data-stu-id="b8efe-158">Loading with CTAS uses the strongly typed external table you have created.</span></span>

<span data-ttu-id="b8efe-159">CTAS yeni bir tablo oluşturur ve bir select deyimi sonuçları ile doldurur.</span><span class="sxs-lookup"><span data-stu-id="b8efe-159">CTAS creates a new table and populates it with the results of a select statement.</span></span> <span data-ttu-id="b8efe-160">CTAS select deyimi sonuçları olarak aynı sütunları ve veri türleri için yeni tabloyu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b8efe-160">CTAS defines the new table to have the same columns and data types as the results of the select statement.</span></span> <span data-ttu-id="b8efe-161">Dış bir tablodaki tüm sütunları seçin, yeni bir tablo sütunları ve dış tablosunda veri türlerini çoğaltmasını olur.</span><span class="sxs-lookup"><span data-stu-id="b8efe-161">If you select all the columns from an external table, the new table is a replica of the columns and data types in the external table.</span></span>

<span data-ttu-id="b8efe-162">Bu örnekte, dış tablo DimProduct_external DimProduct adlı karma bir dağıtılmış tablo oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="b8efe-162">In this example, we are creating a hash distributed table called DimProduct from our External Table DimProduct_external.</span></span>

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a><span data-ttu-id="b8efe-163">Columnstore sıkıştırma en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="b8efe-163">Optimize columnstore compression</span></span>
<span data-ttu-id="b8efe-164">Varsayılan olarak, SQL Data Warehouse kümelenmiş columnstore dizini tablo depolar.</span><span class="sxs-lookup"><span data-stu-id="b8efe-164">By default, SQL Data Warehouse stores the table as a clustered columnstore index.</span></span> <span data-ttu-id="b8efe-165">Yükleme tamamlandıktan sonra bazı veriler satır columnstore sıkıştırılır değil.</span><span class="sxs-lookup"><span data-stu-id="b8efe-165">After a load completes, some of the data rows might not be compressed into the columnstore.</span></span>  <span data-ttu-id="b8efe-166">Çeşitli nedenlerle oluşabilir neden yoktur.</span><span class="sxs-lookup"><span data-stu-id="b8efe-166">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="b8efe-167">Daha fazla bilgi için bkz: [columnstore dizinleri yönetmek][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="b8efe-167">To learn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="b8efe-168">Sorgu performansı ve yük sonra columnstore sıkıştırma iyileştirmek için tüm satırların sıkıştırılacak columnstore dizinini zorlamak için tabloyu yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b8efe-168">To optimize query performance and columnstore compression after a load, rebuild the table to force the columnstore index to compress all the rows.</span></span>

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

<span data-ttu-id="b8efe-169">Columnstore dizinleri koruma ile ilgili daha fazla bilgi için bkz: [columnstore dizinleri yönetmek] [ manage columnstore indexes] makalesi.</span><span class="sxs-lookup"><span data-stu-id="b8efe-169">For more information on maintaining columnstore indexes, see the [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="optimize-statistics"></a><span data-ttu-id="b8efe-170">İstatistikleri en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="b8efe-170">Optimize statistics</span></span>
<span data-ttu-id="b8efe-171">Bir yük hemen sonra tek sütunlu istatistikler oluşturmak en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="b8efe-171">It is best to create single-column statistics immediately after a load.</span></span> <span data-ttu-id="b8efe-172">İstatistikleri için bazı seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="b8efe-172">There are some choices for statistics.</span></span> <span data-ttu-id="b8efe-173">Örneğin, her sütunda tek sütunlu İstatistikler oluşturursanız, tüm istatistikleri yeniden oluşturmak için uzun zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="b8efe-173">For example, if you create single-column statistics on every column it might take a long time to rebuild all the statistics.</span></span> <span data-ttu-id="b8efe-174">Belirli sütunları sorgu koşullarında yapmayacağınız biliyorsanız, bu sütunlarda oluşturma istatistikleri atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8efe-174">If you know certain columns are not going to be in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="b8efe-175">Tek sütunlu istatistikler her tablonun her sütunu üzerinde oluşturmaya karar verirseniz, saklı yordam kod örneği kullanabilirsiniz `prc_sqldw_create_stats` içinde [istatistikleri] [ statistics] makalesi.</span><span class="sxs-lookup"><span data-stu-id="b8efe-175">If you decide to create single-column statistics on every column of every table, you can use the stored procedure code sample `prc_sqldw_create_stats` in the [statistics][statistics] article.</span></span>

<span data-ttu-id="b8efe-176">Aşağıdaki istatistikler oluşturmak için iyi bir başlangıç noktası örnektir.</span><span class="sxs-lookup"><span data-stu-id="b8efe-176">The following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="b8efe-177">Her sütunun Boyut tablosuna ve olgu tabloları katılan her sütunda tek sütunlu İstatistikler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b8efe-177">It creates single-column statistics on each column in the dimension table, and on each joining column in the fact tables.</span></span> <span data-ttu-id="b8efe-178">Her zaman tek veya birden çok sütun istatistikleri diğer olgu tablo sütunları daha sonra ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8efe-178">You can always add single or multi-column statistics to other fact table columns later on.</span></span>


## <a name="achievement-unlocked"></a><span data-ttu-id="b8efe-179">Kilidi başarı!</span><span class="sxs-lookup"><span data-stu-id="b8efe-179">Achievement unlocked!</span></span>
<span data-ttu-id="b8efe-180">Azure SQL Data Warehouse'a veri başarıyla yüklemiş olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="b8efe-180">You have successfully loaded data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="b8efe-181">Harika iş!</span><span class="sxs-lookup"><span data-stu-id="b8efe-181">Great job!</span></span>

##<a name="next-steps"></a><span data-ttu-id="b8efe-182">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="b8efe-182">Next Steps</span></span>
<span data-ttu-id="b8efe-183">Veri yükleme SQL Data Warehouse kullanarak bir veri ambarı çözüm geliştirmek için ilk adımdır.</span><span class="sxs-lookup"><span data-stu-id="b8efe-183">Loading data is the first step to developing a data warehouse solution using SQL Data Warehouse.</span></span> <span data-ttu-id="b8efe-184">Geliştirme KAYNAKLARIMIZI kontrol [tabloları](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) ve [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span><span class="sxs-lookup"><span data-stu-id="b8efe-184">Check out our development resources on [Tables](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) and [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span></span>


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
[Load the full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
