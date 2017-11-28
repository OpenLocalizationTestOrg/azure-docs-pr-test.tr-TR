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
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a><span data-ttu-id="33966-103">Azure Data Lake Deposu'ndan veri SQL Data Warehouse'a veri yükleme</span><span class="sxs-lookup"><span data-stu-id="33966-103">Load data from Azure Data Lake Store into SQL Data Warehouse</span></span>
<span data-ttu-id="33966-104">Bu belge PolyBase kullanarak SQL Data Warehouse'a kendi verilerinizi Azure veri Gölü deposu (ADLS) gelen tooload gereken tüm adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="33966-104">This document gives you all steps you  need tooload your own data from Azure Data Lake Store (ADLS) into SQL Data Warehouse using PolyBase.</span></span>
<span data-ttu-id="33966-105">Merhaba dış tablolara kullanarak ADLS içinde depolanan hello veriler üzerinde mümkün toorun geçici sorguları olmakla birlikte, en iyi uygulama olarak hello verileri SQL Data Warehouse hello alma öneririz.</span><span class="sxs-lookup"><span data-stu-id="33966-105">While you are able toorun adhoc queries over hello data stored in ADLS using hello External Tables, as a best practice we suggest importing hello data into hello SQL Data Warehouse.</span></span>
<span data-ttu-id="33966-106">Tahmini süre: 10 dakika hello önkoşullara sahip olduğu varsayılarak toocomplete gerekir.</span><span class="sxs-lookup"><span data-stu-id="33966-106">Time Estimate: 10 minutes assuming you have hello prerequisites need toocomplete.</span></span>
<span data-ttu-id="33966-107">Bu öğreticide şunları öğreneceksiniz nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="33966-107">In this tutorial you will learn how to:</span></span>

1. <span data-ttu-id="33966-108">Dış veritabanı nesneleri tooload Azure Data Lake Deposu'ndan veri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="33966-108">Create External Database objects tooload from Azure Data Lake Store.</span></span>
2. <span data-ttu-id="33966-109">Azure Data Lake deposu dizinini tooan bağlayın.</span><span class="sxs-lookup"><span data-stu-id="33966-109">Connect tooan Azure Data Lake Store Directory.</span></span>
3. <span data-ttu-id="33966-110">Azure SQL Data Warehouse'a veri yükleme.</span><span class="sxs-lookup"><span data-stu-id="33966-110">Load data into Azure SQL Data Warehouse.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="33966-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="33966-111">Before you begin</span></span>
<span data-ttu-id="33966-112">toorun Bu öğretici, gerekir:</span><span class="sxs-lookup"><span data-stu-id="33966-112">toorun this tutorial, you need:</span></span>

* <span data-ttu-id="33966-113">Hizmetten hizmete kimlik doğrulaması için Azure Active Directory Uygulama toouse.</span><span class="sxs-lookup"><span data-stu-id="33966-113">Azure Active Directory Application toouse for Service-to-Service authentication.</span></span> <span data-ttu-id="33966-114">toocreate, izleyin [Active directory kimlik doğrulaması](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span><span class="sxs-lookup"><span data-stu-id="33966-114">toocreate, follow [Active directory authentication](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span></span>

>[!NOTE] 
> <span data-ttu-id="33966-115">Merhaba istemci kimliği, anahtar ve Active Directory Uygulama tooconnect tooyour Azure Data Lake SQL veri ambarından OAuth2.0 belirteç uç noktası değeri gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="33966-115">You need hello client ID, Key, and OAuth2.0 Token Endpoint Value of your Active Directory Application tooconnect tooyour Azure Data Lake from SQL Data Warehouse.</span></span> <span data-ttu-id="33966-116">Nasıl tooget bu bağlantıyı hello yukarıdaki değerler için Ayrıntılar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="33966-116">Details for how tooget these values are in hello link above.</span></span>
><span data-ttu-id="33966-117">Azure Active Directory Uygulama kaydı için Not hello 'Uygulama kimliği' hello istemci kimliği kullanın</span><span class="sxs-lookup"><span data-stu-id="33966-117">Note for Azure Active Directory App Registration use hello 'Application ID' as hello Client ID.</span></span>

* <span data-ttu-id="33966-118">SQL Server Management Studio veya SQL Server veri araçları, toodownload SSMS ve bakın bağlanmak [sorgu SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span><span class="sxs-lookup"><span data-stu-id="33966-118">SQL Server Management Studio or SQL Server Data Tools, toodownload SSMS and connect see [Query SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span></span>

* <span data-ttu-id="33966-119">Bir Azure SQL Data Warehouse toocreate birini izleyin: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span><span class="sxs-lookup"><span data-stu-id="33966-119">An Azure SQL Data Warehouse, toocreate one follow: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span></span>

* <span data-ttu-id="33966-120">Bir Azure Data Lake Store, ile veya olmadan şifreleme etkin.</span><span class="sxs-lookup"><span data-stu-id="33966-120">An Azure Data Lake Store, with or without encryption enabled.</span></span> <span data-ttu-id="33966-121">toocreate bir izleyin: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="33966-121">toocreate one follow: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span></span>




## <a name="configure-hello-data-source"></a><span data-ttu-id="33966-122">Merhaba veri kaynağını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="33966-122">Configure hello data source</span></span>
<span data-ttu-id="33966-123">PolyBase T-SQL dış nesneleri toodefine hello konumu ve hello dış veri özniteliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="33966-123">PolyBase uses T-SQL external objects toodefine hello location and attributes of hello external data.</span></span> <span data-ttu-id="33966-124">Merhaba dış nesneleri th harici olarak depolanan SQL veri ambarı ve başvuru hello verilerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="33966-124">hello external objects are stored in SQL Data Warehouse and reference hello data th is stored externally.</span></span>


###  <a name="create-a-credential"></a><span data-ttu-id="33966-125">Bir kimlik bilgisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="33966-125">Create a credential</span></span>
<span data-ttu-id="33966-126">Azure Data Lake tooaccess deposuna, toocreate bir veritabanı ana anahtarı tooencrypt hello sonraki adımda kullanılan kimlik bilgileri gizli anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="33966-126">tooaccess your Azure Data Lake Store, you will need toocreate a Database Master Key tooencrypt your credential secret used in hello next step.</span></span>
<span data-ttu-id="33966-127">AAD'de ayarlanan hello hizmet asıl kimlik bilgilerini depolayan bir veritabanı kapsamlı kimlik bilgisi oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="33966-127">You then create a Database scoped credential, which stores hello service principal credentials set up in AAD.</span></span> <span data-ttu-id="33966-128">PolyBase tooconnect tooWindows Azure Storage Bloblarında kullanmış, o hello kimlik bilgisi unutmayın, içeriğiyle için sözdizimi farklıdır.</span><span class="sxs-lookup"><span data-stu-id="33966-128">For those of you who have used PolyBase tooconnect tooWindows Azure Storage Blobs, note that hello credential syntax is different.</span></span>
<span data-ttu-id="33966-129">tooconnect tooAzure Data Lake Store, şunları yapmalısınız **ilk** Azure Active Directory uygulama oluşturmak, bir erişim anahtarı oluşturun ve hello uygulama erişim toohello Azure Data Lake kaynağı verin.</span><span class="sxs-lookup"><span data-stu-id="33966-129">tooconnect tooAzure Data Lake Store, you must **first** create an Azure Active Directory Application, create an access key, and grant hello application access toohello Azure Data Lake resource.</span></span> <span data-ttu-id="33966-130">Instrucitons tooperform adımları konumlandırıldığını [burada](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span><span class="sxs-lookup"><span data-stu-id="33966-130">Instrucitons tooperform these steps are located [here](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span></span>

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


### <a name="create-hello-external-data-source"></a><span data-ttu-id="33966-131">Merhaba dış veri kaynağı oluşturun</span><span class="sxs-lookup"><span data-stu-id="33966-131">Create hello external data source</span></span>
<span data-ttu-id="33966-132">Bu [dış veri kaynağı oluştur] [ CREATE EXTERNAL DATA SOURCE] komut toostore hello konumunu hello veri ve veri hello türü.</span><span class="sxs-lookup"><span data-stu-id="33966-132">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command toostore hello location of hello data, and hello type of data.</span></span>
<span data-ttu-id="33966-133">Merhaba ADL URI hello Azure portal ve www.portal.azure.com bölümünde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33966-133">You can find hello ADL URI in hello Azure portal and www.portal.azure.com.</span></span>

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



## <a name="configure-data-format"></a><span data-ttu-id="33966-134">Veri biçimini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="33966-134">Configure data format</span></span>
<span data-ttu-id="33966-135">ADLS tooimport hello verileri, toospecify hello dış dosya biçimini gerekir.</span><span class="sxs-lookup"><span data-stu-id="33966-135">tooimport hello data from ADLS, you need toospecify hello external file format.</span></span> <span data-ttu-id="33966-136">Bu komut, verilerinizi formata özgü seçenekleri toodescribe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="33966-136">This command has format-specific options toodescribe your data.</span></span>
<span data-ttu-id="33966-137">Bir kanal sınırlandırılmış metin dosyası bir sık kullanılan bir dosya biçimi örneği aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="33966-137">Below is an example of a commonly used file format that is a pipe-delimited text file.</span></span>
<span data-ttu-id="33966-138">Tam bir listesi için T-SQL belgelerimize bakın [oluşturmak dış dosya biçimi][CREATE EXTERNAL FILE FORMAT]</span><span class="sxs-lookup"><span data-stu-id="33966-138">Look at our T-SQL documentation for a complete list of [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span></span>

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

## <a name="create-hello-external-tables"></a><span data-ttu-id="33966-139">Merhaba dış tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="33966-139">Create hello external tables</span></span>
<span data-ttu-id="33966-140">Şimdi hello veri kaynağı ve dosya biçimi belirttiğiniz hazır toocreate hello dış tablolara demektir.</span><span class="sxs-lookup"><span data-stu-id="33966-140">Now that you have specified hello data source and file format, you are ready toocreate hello external tables.</span></span> <span data-ttu-id="33966-141">Dış tablolar dış veri ile nasıl etkileşim değildir.</span><span class="sxs-lookup"><span data-stu-id="33966-141">External tables are how you interact with external data.</span></span> <span data-ttu-id="33966-142">PolyBase özyinelemeli dizin geçişi tooread hello konumu parametresinde belirtilen hello dizinin tüm alt dizinler tüm dosyaları kullanır.</span><span class="sxs-lookup"><span data-stu-id="33966-142">PolyBase uses recursive directory traversal tooread all files in all subdirectories of hello directory specified in hello location parameter.</span></span> <span data-ttu-id="33966-143">Ayrıca, aşağıdaki örneğine hello nasıl toocreate hello nesne gösterir.</span><span class="sxs-lookup"><span data-stu-id="33966-143">Also, hello following example shows how toocreate hello object.</span></span> <span data-ttu-id="33966-144">Sahip olduğunuz ADLS içinde hello verilerle toocustomize hello deyimi toowork gerekir.</span><span class="sxs-lookup"><span data-stu-id="33966-144">You need toocustomize hello statement toowork with hello data you have in ADLS.</span></span>

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

## <a name="external-table-considerations"></a><span data-ttu-id="33966-145">Dış tablo konuları</span><span class="sxs-lookup"><span data-stu-id="33966-145">External Table Considerations</span></span>
<span data-ttu-id="33966-146">Bir dış tablo oluşturmak kolaydır, ancak ele alınan toobe gereken bazı küçük farklar vardır.</span><span class="sxs-lookup"><span data-stu-id="33966-146">Creating an external table is easy, but there are some nuances that need toobe discussed.</span></span>

<span data-ttu-id="33966-147">PolyBase ile veri yükleme kesin türü belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="33966-147">Loading data with PolyBase is strongly typed.</span></span> <span data-ttu-id="33966-148">Başka bir deyişle, her alınan hello veri satırının hello tablo şeması tanımı karşılaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="33966-148">This means that each row of hello data being ingested must satisfy hello table schema definition.</span></span>
<span data-ttu-id="33966-149">Belirli bir satır hello şema tanımı eşleşmiyorsa hello satır hello yük reddedilir.</span><span class="sxs-lookup"><span data-stu-id="33966-149">If a given row does not match hello schema definition, hello row is rejected from hello load.</span></span>

<span data-ttu-id="33966-150">Merhaba REJECT_TYPE ve REJECT_VALUE seçeneklerini toodefine izin kaç satırları veya hello veri yüzdesini hello son tabloda mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="33966-150">hello REJECT_TYPE and REJECT_VALUE options allow you toodefine how many rows or what percentage of hello data must be present in hello final table.</span></span>
<span data-ttu-id="33966-151">Merhaba Reddet değerine ulaşılana yüklenmesi sırasında hello yükleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="33966-151">During load, if hello reject value is reached, hello load fails.</span></span> <span data-ttu-id="33966-152">Reddedilen satır Hello en yaygın nedeni bir şema tanımı uyumsuzluğu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="33966-152">hello most common cause of rejected rows is a schema definition mismatch.</span></span>
<span data-ttu-id="33966-153">Örneğin, Hello veri hello dosyasındaki bir dize olduğunda bir sütunu yanlış hello şema int verilen her satıra tooload başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="33966-153">For example, if a column is incorrectly given hello schema of int when hello data in hello file is a string, every row will fail tooload.</span></span>

<span data-ttu-id="33966-154">Başlangıç konumu tooread verileri istediğiniz hello en üstteki dizini belirtir.</span><span class="sxs-lookup"><span data-stu-id="33966-154">hello Location specifies hello topmost directory that you want tooread data from.</span></span>
<span data-ttu-id="33966-155">Bu durumda, varsa /DimProduct/ PolyBase alt dizinler hello alt dizinleri içindeki tüm hello veri alın.</span><span class="sxs-lookup"><span data-stu-id="33966-155">In this case, if there were subdirectories under /DimProduct/ PolyBase would import all hello data within hello subdirectories.</span></span>

## <a name="load-hello-data"></a><span data-ttu-id="33966-156">Merhaba veri yükleme</span><span class="sxs-lookup"><span data-stu-id="33966-156">Load hello data</span></span>
<span data-ttu-id="33966-157">Azure Data Lake Store tooload verileri hello kullan [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] deyimi.</span><span class="sxs-lookup"><span data-stu-id="33966-157">tooload data from Azure Data Lake Store use hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="33966-158">İle CTAS yüklenirken kullanır hello oluşturduğunuz dış tablo kesin türü belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="33966-158">Loading with CTAS uses hello strongly typed external table you have created.</span></span>

<span data-ttu-id="33966-159">CTAS yeni bir tablo oluşturur ve bir select deyimi hello sonuçlarını ile doldurur.</span><span class="sxs-lookup"><span data-stu-id="33966-159">CTAS creates a new table and populates it with hello results of a select statement.</span></span> <span data-ttu-id="33966-160">CTAS tanımlar hello yeni tablo toohave hello hello sonuçlarını select deyimi gibi hello aynı sütun ve veri türleri.</span><span class="sxs-lookup"><span data-stu-id="33966-160">CTAS defines hello new table toohave hello same columns and data types as hello results of hello select statement.</span></span> <span data-ttu-id="33966-161">Bir dış tablodan tüm hello sütunları seçerseniz, hello yeni tablo hello sütunları ve veri türleri çoğaltmasını hello dış tablosunda vardır.</span><span class="sxs-lookup"><span data-stu-id="33966-161">If you select all hello columns from an external table, hello new table is a replica of hello columns and data types in hello external table.</span></span>

<span data-ttu-id="33966-162">Bu örnekte, dış tablo DimProduct_external DimProduct adlı karma bir dağıtılmış tablo oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="33966-162">In this example, we are creating a hash distributed table called DimProduct from our External Table DimProduct_external.</span></span>

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a><span data-ttu-id="33966-163">Columnstore sıkıştırma en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="33966-163">Optimize columnstore compression</span></span>
<span data-ttu-id="33966-164">Varsayılan olarak, SQL Data Warehouse kümelenmiş columnstore dizini hello tablo depolar.</span><span class="sxs-lookup"><span data-stu-id="33966-164">By default, SQL Data Warehouse stores hello table as a clustered columnstore index.</span></span> <span data-ttu-id="33966-165">Yükleme tamamlandıktan sonra bazı hello veri satır hello columnstore sıkıştırılır değil.</span><span class="sxs-lookup"><span data-stu-id="33966-165">After a load completes, some of hello data rows might not be compressed into hello columnstore.</span></span>  <span data-ttu-id="33966-166">Çeşitli nedenlerle oluşabilir neden yoktur.</span><span class="sxs-lookup"><span data-stu-id="33966-166">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="33966-167">toolearn daha, fazla [columnstore dizinleri yönetmek][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="33966-167">toolearn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="33966-168">toooptimize sorgu performansını ve columnstore sıkıştırma bir yükleme sonrasında, tüm hello satırları hello tablo tooforce hello columnstore dizini toocompress yeniden.</span><span class="sxs-lookup"><span data-stu-id="33966-168">toooptimize query performance and columnstore compression after a load, rebuild hello table tooforce hello columnstore index toocompress all hello rows.</span></span>

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

<span data-ttu-id="33966-169">Merhaba columnstore dizinleri koruma ile ilgili daha fazla bilgi için bkz: [columnstore dizinleri yönetmek] [ manage columnstore indexes] makalesi.</span><span class="sxs-lookup"><span data-stu-id="33966-169">For more information on maintaining columnstore indexes, see hello [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="optimize-statistics"></a><span data-ttu-id="33966-170">İstatistikleri en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="33966-170">Optimize statistics</span></span>
<span data-ttu-id="33966-171">Bu, bir yük hemen sonra en iyi toocreate tek sütunlu İstatistikler olur.</span><span class="sxs-lookup"><span data-stu-id="33966-171">It is best toocreate single-column statistics immediately after a load.</span></span> <span data-ttu-id="33966-172">İstatistikleri için bazı seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="33966-172">There are some choices for statistics.</span></span> <span data-ttu-id="33966-173">Örneğin, her sütunda tek sütunlu İstatistikler oluşturursanız, uzun süre toorebuild tüm hello istatistikleri alabilir.</span><span class="sxs-lookup"><span data-stu-id="33966-173">For example, if you create single-column statistics on every column it might take a long time toorebuild all hello statistics.</span></span> <span data-ttu-id="33966-174">Belirli sütunları toobe sorgu koşullarda yapmayacağınız biliyorsanız, bu sütunlarda oluşturma istatistikleri atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33966-174">If you know certain columns are not going toobe in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="33966-175">Her tablonun her sütunu toocreate tek sütunlu İstatistikler karar verirseniz, hello saklı yordam kod örneği kullanabilirsiniz `prc_sqldw_create_stats` hello içinde [istatistikleri] [ statistics] makalesi.</span><span class="sxs-lookup"><span data-stu-id="33966-175">If you decide toocreate single-column statistics on every column of every table, you can use hello stored procedure code sample `prc_sqldw_create_stats` in hello [statistics][statistics] article.</span></span>

<span data-ttu-id="33966-176">Aşağıdaki örnek hello istatistikleri oluşturmak için iyi bir başlangıç noktası ' dir.</span><span class="sxs-lookup"><span data-stu-id="33966-176">hello following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="33966-177">Her sütunda hello Boyut tablosuna ve hello olgu tabloları katılan her sütunda tek sütunlu İstatistikler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="33966-177">It creates single-column statistics on each column in hello dimension table, and on each joining column in hello fact tables.</span></span> <span data-ttu-id="33966-178">Daha sonra onları tek veya birden çok sütun istatistikleri tooother Olgu Tablosu sütunlarını ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33966-178">You can always add single or multi-column statistics tooother fact table columns later on.</span></span>


## <a name="achievement-unlocked"></a><span data-ttu-id="33966-179">Kilidi başarı!</span><span class="sxs-lookup"><span data-stu-id="33966-179">Achievement unlocked!</span></span>
<span data-ttu-id="33966-180">Azure SQL Data Warehouse'a veri başarıyla yüklemiş olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="33966-180">You have successfully loaded data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="33966-181">Harika iş!</span><span class="sxs-lookup"><span data-stu-id="33966-181">Great job!</span></span>

##<a name="next-steps"></a><span data-ttu-id="33966-182">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="33966-182">Next Steps</span></span>
<span data-ttu-id="33966-183">Veri yükleme hello ilk adım toodeveloping SQL Data Warehouse kullanarak bir veri ambarı çözüm olur.</span><span class="sxs-lookup"><span data-stu-id="33966-183">Loading data is hello first step toodeveloping a data warehouse solution using SQL Data Warehouse.</span></span> <span data-ttu-id="33966-184">Geliştirme KAYNAKLARIMIZI kontrol [tabloları](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) ve [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span><span class="sxs-lookup"><span data-stu-id="33966-184">Check out our development resources on [Tables](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) and [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span></span>


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
