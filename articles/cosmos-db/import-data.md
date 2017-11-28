---
title: "Azure Cosmos DB aaaDatabase geçiş aracını | Microsoft Docs"
description: "Toouse hello açılma şeklini kaynak Azure Cosmos DB veri geçiş araçları tooimport veri tooAzure Cosmos DB MongoDB, SQL Server, tablo depolama, Amazon DynamoDB, CSV ve JSON dosyaları dahil olmak üzere çeşitli kaynaklardan bilgi edinin. CSV tooJSON dönüştürme."
keywords: "CSV toojson, veritabanı Geçiş Araçları, csv toojson Dönüştür"
services: cosmos-db
author: andrewhoh
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: d173581d-782a-445c-98d9-5e3c49b00e25
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 997648a31602d854db75bb6ce4e2ecff36fc1069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a><span data-ttu-id="aa7e7-105">Nasıl tooimport verileri için Azure Cosmos DB DocumentDB API hello?</span><span class="sxs-lookup"><span data-stu-id="aa7e7-105">How tooimport data into Azure Cosmos DB for hello DocumentDB API?</span></span>

<span data-ttu-id="aa7e7-106">Bu öğretici Azure Cosmos DB hello kullanma yönergeleri sağlar: JSON dosyaları dahil olmak üzere çeşitli kaynaklardan veri aktarabilirsiniz DocumentDB API veri geçiş aracı CSV dosyaları, SQL, MongoDB, Azure Table storage, Amazon DynamoDB ve Azure Cosmos DB DocumentDB Koleksiyonlar için API koleksiyonlara Azure Cosmos DB ve hello DocumentDB API kullanın.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-106">This tutorial provides instructions on using hello Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and hello DocumentDB API.</span></span> <span data-ttu-id="aa7e7-107">Merhaba veri geçiş aracı, hello DocumentDB API için tek bölüm koleksiyonu tooa çok bölüm koleksiyondan geçirirken kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-107">hello Data Migration tool can also be used when migrating from a single partition collection tooa multi-partition collection for hello DocumentDB API.</span></span>

<span data-ttu-id="aa7e7-108">Merhaba veri geçiş aracı, yalnızca Azure Cosmos DB için içeri aktarma verileri hello DocumentDB API ile kullandığınızda çalışır.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-108">hello Data Migration tool only works when importing data into Azure Cosmos DB for use with hello DocumentDB API.</span></span> <span data-ttu-id="aa7e7-109">Hello tablo API veya grafik API'si ile kullanmak için veri içe aktarımı şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-109">Importing data for use with hello Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="aa7e7-110">Merhaba MongoDB API ile kullanmak için tooimport verileri görmek [Azure Cosmos DB: toomigrate verileri MongoDB API nasıl hello?](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="aa7e7-110">tooimport data for use with hello MongoDB API, see [Azure Cosmos DB: How toomigrate data for hello MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="aa7e7-111">Bu öğretici hello aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-111">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aa7e7-112">Merhaba veri geçiş aracı yükleme</span><span class="sxs-lookup"><span data-stu-id="aa7e7-112">Installing hello Data Migration tool</span></span>
> * <span data-ttu-id="aa7e7-113">Farklı veri kaynaklarından veri alma</span><span class="sxs-lookup"><span data-stu-id="aa7e7-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="aa7e7-114">Azure Cosmos DB tooJSON ' dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="aa7e7-114">Exporting from Azure Cosmos DB tooJSON</span></span>

## <span data-ttu-id="aa7e7-115"><a id="Prerequisites"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="aa7e7-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="aa7e7-116">Bu makaledeki Hello yönergeleri izlemeden önce hello aşağıdaki yüklü olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-116">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="aa7e7-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="aa7e7-118"><a id="Overviewl"></a>Merhaba veri geçiş aracı genel bakış</span><span class="sxs-lookup"><span data-stu-id="aa7e7-118"><a id="Overviewl"></a>Overview of hello Data Migration tool</span></span>
<span data-ttu-id="aa7e7-119">Merhaba veri geçiş aracı veri tooAzure Cosmos DB bir çeşitli kaynaklardan dahil olmak üzere, içe aktaran bir açık kaynak çözümü olmasıdır:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-119">hello Data Migration tool is an open source solution that imports data tooAzure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="aa7e7-120">JSON dosyaları</span><span class="sxs-lookup"><span data-stu-id="aa7e7-120">JSON files</span></span>
* <span data-ttu-id="aa7e7-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="aa7e7-121">MongoDB</span></span>
* <span data-ttu-id="aa7e7-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="aa7e7-122">SQL Server</span></span>
* <span data-ttu-id="aa7e7-123">CSV dosyaları</span><span class="sxs-lookup"><span data-stu-id="aa7e7-123">CSV files</span></span>
* <span data-ttu-id="aa7e7-124">Azure Tablo depolama</span><span class="sxs-lookup"><span data-stu-id="aa7e7-124">Azure Table storage</span></span>
* <span data-ttu-id="aa7e7-125">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="aa7e7-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="aa7e7-126">HBase</span><span class="sxs-lookup"><span data-stu-id="aa7e7-126">HBase</span></span>
* <span data-ttu-id="aa7e7-127">Azure Cosmos DB koleksiyonları</span><span class="sxs-lookup"><span data-stu-id="aa7e7-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="aa7e7-128">Bir grafik kullanıcı arabirimi (dtui.exe) Hello alma aracı içerir, ancak bunu da hello komut satırından (dt.exe) bulunarak belirlenebilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-128">While hello import tool includes a graphical user interface (dtui.exe), it can also be driven from hello command line (dt.exe).</span></span> <span data-ttu-id="aa7e7-129">Aslında, hello UI ile alma kurduktan sonra bir seçenek toooutput ilişkili hello komutu yoktur.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-129">In fact, there is an option toooutput hello associated command after setting up an import through hello UI.</span></span> <span data-ttu-id="aa7e7-130">Hiyerarşik ilişkileri (alt) içeri aktarma sırasında oluşturulabilir, tablo kaynak verileri (örn. SQL Server ya da CSV dosyaları) dönüştürülebilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="aa7e7-131">Toolearn kaynak seçenekleri, her kaynaktan örnek komut satırları tooimport hakkında daha fazla okuma tutmak, hedef seçenekleri ve görüntüleme sonuçları alın.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-131">Keep reading toolearn more about source options, sample command lines tooimport from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="aa7e7-132"><a id="Install"></a>Merhaba Veri Taşıma aracını yükle</span><span class="sxs-lookup"><span data-stu-id="aa7e7-132"><a id="Install"></a>Install hello Data Migration tool</span></span>
<span data-ttu-id="aa7e7-133">Github'da üzerinde Hello geçiş aracı kaynak kodu kullanılabilir [bu havuzda](https://github.com/azure/azure-documentdb-datamigrationtool) ve derlenmiş bir sürüm kullanılabilir [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span><span class="sxs-lookup"><span data-stu-id="aa7e7-133">hello migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="aa7e7-134">Merhaba çözümü derleme veya yalnızca karşıdan yükleyip hello derlenmiş sürüm tooa directory tercih ettiğiniz ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-134">You may either compile hello solution or simply download and extract hello compiled version tooa directory of your choice.</span></span> <span data-ttu-id="aa7e7-135">Ardından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-135">Then run either:</span></span>

* <span data-ttu-id="aa7e7-136">**Dtui.exe**: grafik arabirim hello aracı sürümü</span><span class="sxs-lookup"><span data-stu-id="aa7e7-136">**Dtui.exe**: Graphical interface version of hello tool</span></span>
* <span data-ttu-id="aa7e7-137">**Dt.exe**: hello aracı komut satırı sürümü</span><span class="sxs-lookup"><span data-stu-id="aa7e7-137">**Dt.exe**: Command-line version of hello tool</span></span>

## <a name="import-data"></a><span data-ttu-id="aa7e7-138">Veri içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="aa7e7-138">Import data</span></span>

<span data-ttu-id="aa7e7-139">Merhaba aracı yükledikten sonra saat tooimport olan verilerinizi.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-139">Once you've installed hello tool, it's time tooimport your data.</span></span> <span data-ttu-id="aa7e7-140">Ne tür veriler tooimport istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="aa7e7-140">What kind of data do you want tooimport?</span></span>

* [<span data-ttu-id="aa7e7-141">JSON dosyaları</span><span class="sxs-lookup"><span data-stu-id="aa7e7-141">JSON files</span></span>](#JSON)
* [<span data-ttu-id="aa7e7-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="aa7e7-142">MongoDB</span></span>](#MongoDB)
* [<span data-ttu-id="aa7e7-143">MongoDB dışarı aktarma dosyaları</span><span class="sxs-lookup"><span data-stu-id="aa7e7-143">MongoDB Export files</span></span>](#MongoDBExport)
* [<span data-ttu-id="aa7e7-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="aa7e7-144">SQL Server</span></span>](#SQL)
* [<span data-ttu-id="aa7e7-145">CSV dosyaları</span><span class="sxs-lookup"><span data-stu-id="aa7e7-145">CSV files</span></span>](#CSV)
* [<span data-ttu-id="aa7e7-146">Azure Tablo Depolama</span><span class="sxs-lookup"><span data-stu-id="aa7e7-146">Azure Table storage</span></span>](#AzureTableSource)
* [<span data-ttu-id="aa7e7-147">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="aa7e7-147">Amazon DynamoDB</span></span>](#DynamoDBSource)
* [<span data-ttu-id="aa7e7-148">BLOB</span><span class="sxs-lookup"><span data-stu-id="aa7e7-148">Blob</span></span>](#BlobImport)
* [<span data-ttu-id="aa7e7-149">Azure Cosmos DB koleksiyonları</span><span class="sxs-lookup"><span data-stu-id="aa7e7-149">Azure Cosmos DB collections</span></span>](#DocumentDBSource)
* [<span data-ttu-id="aa7e7-150">HBase</span><span class="sxs-lookup"><span data-stu-id="aa7e7-150">HBase</span></span>](#HBaseSource)
* [<span data-ttu-id="aa7e7-151">Azure Cosmos DB toplu içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="aa7e7-151">Azure Cosmos DB bulk import</span></span>](#DocumentDBBulkImport)
* [<span data-ttu-id="aa7e7-152">Azure Cosmos DB sıralı kayıt alma</span><span class="sxs-lookup"><span data-stu-id="aa7e7-152">Azure Cosmos DB sequential record import</span></span>](#DocumentDSeqTarget)


## <span data-ttu-id="aa7e7-153"><a id="JSON"></a>tooimport JSON dosyaları</span><span class="sxs-lookup"><span data-stu-id="aa7e7-153"><a id="JSON"></a>tooimport JSON files</span></span>
<span data-ttu-id="aa7e7-154">Merhaba JSON dosyasını kaynak alma seçeneği tooimport bir veya daha fazla tek bir belge JSON veya her bir dizi JSON belgelerini içeren JSON dosyaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-154">hello JSON file source importer option allows you tooimport one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="aa7e7-155">JSON dosyaları tooimport içeren klasörleri eklerken, alt klasörler dosyaları aranıyor yinelemeli hello seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-155">When adding folders that contain JSON files tooimport, you have hello option of recursively searching for files in subfolders.</span></span>

![Ekran görüntüsü, JSON dosyası kaynak seçenekleri - veritabanı Geçiş Araçları](./media/import-data/jsonsource.png)

<span data-ttu-id="aa7e7-157">Bazı komut satırı örnekleri tooimport JSON dosyaları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-157">Here are some command line samples tooimport JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition hello data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <span data-ttu-id="aa7e7-158"><a id="MongoDB"></a>MongoDB gelen tooimport</span><span class="sxs-lookup"><span data-stu-id="aa7e7-158"><a id="MongoDB"></a>tooimport from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aa7e7-159">MongoDB için destek tooan Azure Cosmos DB hesabıyla alıyorsanız, aşağıdaki adımları [yönergeleri](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="aa7e7-159">If you are importing tooan Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="aa7e7-160">Merhaba MongoDB kaynak alma seçeneği tek bir MongoDB koleksiyonundan tooimport sağlar ve isteğe bağlı olarak bir sorgu kullanarak belgelere filtre ve/veya hello belge yapısı bir yansıtma kullanarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-160">hello MongoDB source importer option allows you tooimport from an individual MongoDB collection and optionally filter documents using a query and/or modify hello document structure by using a projection.</span></span>  

![Ekran görüntüsü, MongoDB kaynak seçenekleri](./media/import-data/mongodbsource.png)

<span data-ttu-id="aa7e7-162">Merhaba bağlantı dizesi hello standart MongoDB biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-162">hello connection string is in hello standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="aa7e7-163">Merhaba bağlantı dizesi alanına belirtilen MongoDB örneği hello kullan hello doğrula komutu tooensure erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-163">Use hello Verify command tooensure that hello MongoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="aa7e7-164">Veri içeri aktarılacak hello koleksiyonunun Hello adı girin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-164">Enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="aa7e7-165">İsteğe bağlı olarak belirttiğinizde veya bir sorgu için bir dosya belirtin (örneğin {pop: {$gt: 5000}}) ve/veya yansıtma (örneğin {loc:0}) içeri tooboth filtresi ve Şekil hello veri toobe.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) tooboth filter and shape hello data toobe imported.</span></span>

<span data-ttu-id="aa7e7-166">Bazı komut satırı örnekleri tooimport MongoDB gelen şunlardır:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-166">Here are some command line samples tooimport from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="aa7e7-167"><a id="MongoDBExport"></a>tooimport MongoDB dışarı aktarma dosyaları</span><span class="sxs-lookup"><span data-stu-id="aa7e7-167"><a id="MongoDBExport"></a>tooimport MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aa7e7-168">MongoDB için destek tooan Azure Cosmos DB hesabıyla alıyorsanız, aşağıdaki adımları [yönergeleri](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="aa7e7-168">If you are importing tooan Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="aa7e7-169">Daha fazla JSON dosyaları hello mongoexport yardımcı programını üretilen veya Hello MongoDB verme JSON dosyasını kaynak alma seçeneği tooimport bir sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-169">hello MongoDB export JSON file source importer option allows you tooimport one or more JSON files produced from hello mongoexport utility.</span></span>  

![Ekran görüntüsü, MongoDB dışa aktarma kaynak seçenekleri](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="aa7e7-171">Alma için MongoDB verme JSON dosyaları içeren klasörleri eklerken, alt klasörler dosyaları aranıyor yinelemeli hello seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-171">When adding folders that contain MongoDB export JSON files for import, you have hello option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="aa7e7-172">JSON dosyaları bir komut satırı örnek tooimport MongoDB dışarı aktarma işleminden şöyledir:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-172">Here is a command line sample tooimport from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="aa7e7-173"><a id="SQL"></a>SQL Server'dan tooimport</span><span class="sxs-lookup"><span data-stu-id="aa7e7-173"><a id="SQL"></a>tooimport from SQL Server</span></span>
<span data-ttu-id="aa7e7-174">Hello SQL kaynak alma seçeneği tek bir SQL Server veritabanından tooimport sağlar ve isteğe bağlı olarak bir sorgu kullanarak içeri hello kayıtları toobe filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-174">hello SQL source importer option allows you tooimport from an individual SQL Server database and optionally filter hello records toobe imported using a query.</span></span> <span data-ttu-id="aa7e7-175">Ayrıca, bir iç içe geçmiş ayırıcı (daha ayrıntılı bir dakika içinde) belirterek hello belge yapısını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-175">In addition, you can modify hello document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![Ekran görüntüsü, SQL kaynak seçenekleri - veritabanı Geçiş Araçları](./media/import-data/sqlexportsource.png)

<span data-ttu-id="aa7e7-177">Merhaba hello bağlantı dizesi hello standart SQL bağlantı dizesi biçimi biçimidir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-177">hello format of hello connection string is hello standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="aa7e7-178">Merhaba bağlantı dizesi alanında belirtilen SQL Server örneği hello kullan hello doğrula komutu tooensure erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-178">Use hello Verify command tooensure that hello SQL Server instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="aa7e7-179">ayırıcı özelliği iç içe geçme hello içeri aktarma sırasında kullanılan toocreate hiyerarşik ilişkileri (alt belgeler) olur.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-179">hello nesting separator property is used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="aa7e7-180">SQL sorgusu aşağıdaki hello göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-180">Consider hello following SQL query:</span></span>

<span data-ttu-id="aa7e7-181">*Kimliği, ad, [Address.AddressType] olarak AddressType, AddressLine1 [Address.AddressLine1] olarak, [Address.Location.City] olarak Şehir, StateProvinceName [Address.Location.StateProvinceName] olarak, PostalCode [olarak dönüştürme (BusinessEntityID AS varchar) seçin Address.PostalCode], [Address.CountryRegionName] olarak CountryRegionName Sales.vStoreWithAddresses gelen nerede AddressType 'Ana ofis' =*</span><span class="sxs-lookup"><span data-stu-id="aa7e7-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="aa7e7-182">Hangi (kısmi) sonuçları aşağıdaki hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-182">Which returns hello following (partial) results:</span></span>

![Ekran görüntüsü, SQL sorgu sonuçları](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="aa7e7-184">Address.AddressType ve Address.Location.StateProvinceName gibi Hello diğer adlar unutmayın.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-184">Note hello aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="aa7e7-185">İç içe geçmiş bir ayırıcı olarak belirterek '.', hello alma aracı adresi oluşturur ve Address.Location alt hello sırasında içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-185">By specifying a nesting separator of ‘.’, hello import tool creates Address and Address.Location subdocuments during hello import.</span></span> <span data-ttu-id="aa7e7-186">Azure Cosmos DB ortaya çıkan bir belgede bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="aa7e7-187">*{"ID": "956", "Name": "Yüksekse satış ve"Adres"hizmet": {"AddressType": "Ana ofis", "AddressLine1": "#500 75 O'Connor Sokak", "Konum": {"Şehir": "Ottawa", "StateProvinceName": "Ontario"}, "PostalCode": "K4B 1S2", "CountryRegionName": " Kanada"}}*</span><span class="sxs-lookup"><span data-stu-id="aa7e7-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="aa7e7-188">Bazı komut satırı örnekleri tooimport SQL Server'dan şunlardır:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-188">Here are some command line samples tooimport from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="aa7e7-189"><a id="CSV"></a>tooimport CSV dosyaları ve dönüştürme CSV tooJSON</span><span class="sxs-lookup"><span data-stu-id="aa7e7-189"><a id="CSV"></a>tooimport CSV files and convert CSV tooJSON</span></span>
<span data-ttu-id="aa7e7-190">Merhaba CSV dosyası kaynak alma seçeneği, tooimport bir veya daha fazla CSV dosyaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-190">hello CSV file source importer option enables you tooimport one or more CSV files.</span></span> <span data-ttu-id="aa7e7-191">İçeri aktarma için CSV dosyaları içeren klasörleri eklerken, alt klasörler dosyaları aranıyor yinelemeli hello seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-191">When adding folders that contain CSV files for import, you have hello option of recursively searching for files in subfolders.</span></span>

![Ekran görüntüsü, CSV kaynak seçenekleri - CSV tooJSON](media/import-data/csvsource.png)

<span data-ttu-id="aa7e7-193">Benzer toohello SQL kaynağı, ayırıcı özelliği iç içe geçme hello içeri aktarma sırasında kullanılan toocreate hiyerarşik ilişkileri (alt belgeler) olabilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-193">Similar toohello SQL source, hello nesting separator property may be used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="aa7e7-194">CSV üstbilgisi satır ve veri satırına aşağıdaki hello göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-194">Consider hello following CSV header row and data rows:</span></span>

![Ekran görüntüsü, CSV örnek kayıtlarını - CSV tooJSON](./media/import-data/csvsample.png)

<span data-ttu-id="aa7e7-196">DomainInfo.Domain_Name ve RedirectInfo.Redirecting gibi Hello diğer adlar unutmayın.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-196">Note hello aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="aa7e7-197">İç içe geçmiş bir ayırıcı olarak belirterek '.', hello içeri aktarma aracını DomainInfo oluşturur ve RedirectInfo alt hello sırasında içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-197">By specifying a nesting separator of ‘.’, hello import tool will create DomainInfo and RedirectInfo subdocuments during hello import.</span></span> <span data-ttu-id="aa7e7-198">Azure Cosmos DB ortaya çıkan bir belgede bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="aa7e7-199">*{"DomainInfo": {"Etki_alanı_adı": "ACUS.GOV", "Domain_Name_Address": "http://www. ACUS.GOV"},"Federal Teşkilatı":"Merhaba Amerika Birleşik Devletleri yönetim konferans","RedirectInfo": {"Yeniden yönlendirme":"0","Redirect_Destination":" "},"id":"9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d"}*</span><span class="sxs-lookup"><span data-stu-id="aa7e7-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of hello United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="aa7e7-200">Merhaba içeri aktarma aracını CSV dosyalarında tırnak işareti olmayan değerler için tooinfer türü bilgileri (tırnak içine alınmış değerler her zaman dize olarak kabul edilir) dener.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-200">hello import tool will attempt tooinfer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="aa7e7-201">Türleri sırasının hello tanımlanır: sayı, datetime, Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-201">Types are identified in hello following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="aa7e7-202">CSV Import hakkında diğer iki şey toonote vardır:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-202">There are two other things toonote about CSV import:</span></span>

1. <span data-ttu-id="aa7e7-203">Tırnak içine alınmış değerler olarak korunur sırasında varsayılan olarak, tırnak işareti olmayan değerler her zaman sekmeler ve alanları için atılır-değil.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="aa7e7-204">Bu davranış kırpma değerleri onay kutusunu veya hello /s.TrimQuoted komut satırı seçeneği tırnak içine alınmış hello ile geçersiz kılınabilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-204">This behavior can be overridden with hello Trim quoted values checkbox or hello /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="aa7e7-205">Varsayılan olarak, tırnak işareti olmayan bir null, null değeri olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="aa7e7-206">Bu davranışı geçersiz kılınabilir (yani tırnak işareti olmayan bir null "null" dize olarak işle) hello NULL dize onay kutusunu veya hello /s.NoUnquotedNulls komut satırı seçeneği olarak tırnak işareti olmayan kabul ile.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with hello Treat unquoted NULL as string checkbox or hello /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="aa7e7-207">CSV içeri aktarma için bir komut satırı örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="aa7e7-208"><a id="AzureTableSource"></a>Azure Table depolama biriminden tooimport</span><span class="sxs-lookup"><span data-stu-id="aa7e7-208"><a id="AzureTableSource"></a>tooimport from Azure Table storage</span></span>
<span data-ttu-id="aa7e7-209">Hello Azure Table depolama kaynağı alma seçeneği tek bir Azure Table depolama tablosundan tooimport sağlar ve isteğe bağlı olarak içeri hello tablo varlıkları toobe filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-209">hello Azure Table storage source importer option allows you tooimport from an individual Azure Table storage table and optionally filter hello table entities toobe imported.</span></span> <span data-ttu-id="aa7e7-210">Hello veri geçiş aracı tooimport Azure Table depolama veri Azure Cosmos Veritabanına hello tablo API ile kullanılmak üzere kullanamayacağınızı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-210">Note that you cannot use hello Data Migration tool tooimport Azure Table storage data into Azure Cosmos DB for use with hello Table API.</span></span> <span data-ttu-id="aa7e7-211">Yalnızca tooAzure Cosmos DB hello DocumentDB API ile kullanmak için içeri aktarma şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-211">Only importing tooAzure Cosmos DB for use with hello DocumentDB API is supported at this time.</span></span>

![Azure tablo ekran depolama kaynağı seçenekleri](./media/import-data/azuretablesource.png)

<span data-ttu-id="aa7e7-213">hello Azure Table depolama bağlantı dizesi Hello biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-213">hello format of hello Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="aa7e7-214">Azure Table depolama örneği hello bağlantı dizesi alanında belirtilen hello kullan hello doğrula komutu tooensure erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-214">Use hello Verify command tooensure that hello Azure Table storage instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="aa7e7-215">Hello Azure Hello adını girin, veri içeri aktarılacak tablo.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-215">Enter hello name of hello Azure table from which data will be imported.</span></span> <span data-ttu-id="aa7e7-216">İsteğe bağlı olarak belirtebilir bir [filtre](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa7e7-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="aa7e7-217">ek seçenekler aşağıdaki hello Hello Azure Table depolama kaynağı alma seçeneği vardır:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-217">hello Azure Table storage source importer option has hello following additional options:</span></span>

1. <span data-ttu-id="aa7e7-218">İç alanlar</span><span class="sxs-lookup"><span data-stu-id="aa7e7-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="aa7e7-219">Tüm - dahil tüm iç alanlar (PartitionKey, RowKey ve zaman damgası)</span><span class="sxs-lookup"><span data-stu-id="aa7e7-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="aa7e7-220">Hiçbiri - hariç tüm iç alanları</span><span class="sxs-lookup"><span data-stu-id="aa7e7-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="aa7e7-221">RowKey - yalnızca hello RowKey alan dahil et</span><span class="sxs-lookup"><span data-stu-id="aa7e7-221">RowKey - Only include hello RowKey field</span></span>
2. <span data-ttu-id="aa7e7-222">Sütunları seçin</span><span class="sxs-lookup"><span data-stu-id="aa7e7-222">Select Columns</span></span>
   1. <span data-ttu-id="aa7e7-223">Azure tablo depolama filtrelerini tahminleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="aa7e7-224">Tooonly alma belirli Azure tablo varlık özellikleri istiyorsanız, bunları toohello Sütunları Seç listeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-224">If you want tooonly import specific Azure Table entity properties, add them toohello Select Columns list.</span></span> <span data-ttu-id="aa7e7-225">Diğer tüm varlık özellikleri yoksayılacak.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="aa7e7-226">Bir komut satırı örnek tooimport Azure Table depolama biriminden şöyledir:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-226">Here is a command line sample tooimport from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="aa7e7-227"><a id="DynamoDBSource"></a>Amazon DynamoDB gelen tooimport</span><span class="sxs-lookup"><span data-stu-id="aa7e7-227"><a id="DynamoDBSource"></a>tooimport from Amazon DynamoDB</span></span>
<span data-ttu-id="aa7e7-228">Hello Amazon DynamoDB kaynak alma seçeneği tek bir Amazon DynamoDB tablosundan tooimport sağlar ve isteğe bağlı olarak içeri hello varlıklar toobe filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-228">hello Amazon DynamoDB source importer option allows you tooimport from an individual Amazon DynamoDB table and optionally filter hello entities toobe imported.</span></span> <span data-ttu-id="aa7e7-229">Alma ayarı kadar kolay böylece çeşitli şablonlar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Amazon DynamoDB ekran kaynak seçenekleri - veritabanı Geçiş Araçları](./media/import-data/dynamodbsource1.png)

![Amazon DynamoDB ekran kaynak seçenekleri - veritabanı Geçiş Araçları](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="aa7e7-232">Merhaba Amazon DynamoDB bağlantı dizesi Hello biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-232">hello format of hello Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="aa7e7-233">Merhaba bağlantı dizesi alanına belirtilen Amazon DynamoDB örneği hello kullan hello doğrula komutu tooensure erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-233">Use hello Verify command tooensure that hello Amazon DynamoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="aa7e7-234">Bir komut satırı örnek tooimport Amazon DynamoDB gelen şöyledir:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-234">Here is a command line sample tooimport from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="aa7e7-235"><a id="BlobImport"></a>Azure Blob depolama biriminden tooimport dosyaları</span><span class="sxs-lookup"><span data-stu-id="aa7e7-235"><a id="BlobImport"></a>tooimport files from Azure Blob storage</span></span>
<span data-ttu-id="aa7e7-236">Merhaba JSON dosyası, MongoDB dışarı aktarma dosyası ve CSV dosyası kaynağı içeri Aktarıcı seçenekleri tooimport izin Azure Blob depolama biriminden bir veya daha fazla.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-236">hello JSON file, MongoDB export file, and CSV file source importer options allow you tooimport one or more files from Azure Blob storage.</span></span> <span data-ttu-id="aa7e7-237">Bir Blob kapsayıcı URL'si ve hesap anahtarı belirttikten sonra bir normal ifade tooselect hello dosyaları tooimport belirtmeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-237">After specifying a Blob container URL and Account Key, simply provide a regular expression tooselect hello file(s) tooimport.</span></span>

![Ekran görüntüsü, Blob dosya kaynağı seçenekleri](./media/import-data/blobsource.png)

<span data-ttu-id="aa7e7-239">Komut satırı örnek tooimport JSON dosyaları Azure Blob depolama biriminden şöyledir:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-239">Here is command line sample tooimport JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="aa7e7-240"><a id="DocumentDBSource"></a>bir Azure Cosmos DB DocumentDB API koleksiyonundan tooimport</span><span class="sxs-lookup"><span data-stu-id="aa7e7-240"><a id="DocumentDBSource"></a>tooimport from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="aa7e7-241">Hello Azure Cosmos DB kaynak alma seçeneği ve isteğe bağlı olarak bir sorgu kullanarak belgelere filtre bir veya daha fazla Azure Cosmos DB koleksiyonundan tooimport verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-241">hello Azure Cosmos DB source importer option allows you tooimport data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Azure Cosmos DB ekran kaynak seçenekleri](./media/import-data/documentdbsource.png)

<span data-ttu-id="aa7e7-243">hello Azure Cosmos DB bağlantı dizesi Hello biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-243">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="aa7e7-244">Hello Azure Cosmos DB hesabı bağlantı dizesi açıklandığı gibi hello Azure portal, hello anahtarlar dikey penceresinden alınabilir [nasıl toomanage bir Azure Cosmos DB hesap](manage-account.md), ancak eklenmiş toobe toohello hello veritabanının hello adı gerekiyor bağlantı dizesi biçimi aşağıdaki hello olarak:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-244">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="aa7e7-245">Merhaba bağlantı dizesi alanına belirtilen Azure Cosmos DB örneği hello kullan hello doğrula komutu tooensure erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-245">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="aa7e7-246">tek bir Azure Cosmos DB koleksiyonundan tooimport hello veri içeri aktarılacak hello koleksiyonun adını girin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-246">tooimport from a single Azure Cosmos DB collection, enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="aa7e7-247">birden çok Azure Cosmos DB koleksiyonlardan tooimport bir veya daha fazla koleksiyon adları bir normal ifade toomatch sağlayın (örneğin collection01 | collection02 | collection03).</span><span class="sxs-lookup"><span data-stu-id="aa7e7-247">tooimport from multiple Azure Cosmos DB collections, provide a regular expression toomatch one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="aa7e7-248">İsteğe bağlı olarak belirtin, veya bir dosya için bir sorgu tooboth filtresi sağlamak ve olabilirsiniz içeri hello veri toobe şekil.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-248">You may optionally specify, or provide a file for, a query tooboth filter and shape hello data toobe imported.</span></span>

> [!NOTE]
> <span data-ttu-id="aa7e7-249">Adında normal ifade karakterler içeren tek bir koleksiyondan alıyorsanız, normal ifadeler hello koleksiyonu alan kabul olduğundan, ardından bu karakterleri uygun şekilde kaçış uygulanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-249">Since hello collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="aa7e7-250">Hello Azure Cosmos DB kaynak alma seçeneği hello aşağıdaki gelişmiş seçenekler vardır:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-250">hello Azure Cosmos DB source importer option has hello following advanced options:</span></span>

1. <span data-ttu-id="aa7e7-251">Dahili alanlar şunlardır: tooinclude Azure Cosmos DB belge Sistem Özellikleri'nde hello (örneğin _rid, _ts) verme olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-251">Include Internal Fields: Specifies whether or not tooinclude Azure Cosmos DB document system properties in hello export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="aa7e7-252">Hata yeniden deneme sayısı: hello kaç kez tooretry hello geçici hataları (örneğin ağ bağlantı kesintisi) olması durumunda bağlantı tooAzure Cosmos DB belirtir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-252">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="aa7e7-253">Yeniden deneme aralığı: geçici hataları (örneğin ağ bağlantı kesintisi) durumunda hello bağlantı tooAzure Cosmos DB yeniden deneniyor arasında ne kadar süreyle toowait belirtir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-253">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="aa7e7-254">Bağlantı modu: Azure Cosmos DB ile Merhaba bağlantı modu toouse belirtir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-254">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="aa7e7-255">Merhaba kullanılabilir DirectTcp, DirectHttps ve ağ geçidi seçimlerdir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-255">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="aa7e7-256">yalnızca 443 numaralı bağlantı noktasını kullanır gibi hello ağ geçidi modu daha fazla güvenlik duvarı kolay ederken hello doğrudan bağlantı modları, daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-256">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Gelişmiş Seçenekleri Azure Cosmos DB ekran kaynağı](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="aa7e7-258">Merhaba aracı Varsayılanları tooconnection modu DirectTcp içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-258">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="aa7e7-259">Güvenlik Duvarı sorunlarla karşılaşırsanız, yalnızca bağlantı noktası 443 gerektirdiğinden tooconnection modu ağ geçidi geçin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-259">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="aa7e7-260">Bazı komut satırı örnekleri tooimport Azure Cosmos DB'den şunlardır:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-260">Here are some command line samples tooimport from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="aa7e7-261">Hello Azure Cosmos DB verileri içe aktarma aracını da destekler hello verilerini alma [Azure Cosmos DB öykünücüsü](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="aa7e7-261">hello Azure Cosmos DB Data Import Tool also supports import of data from hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="aa7e7-262">Yerel bir öykünücüsünden verilerini içeri aktarırken hello son nokta çok ayarlanmış`https://localhost:<port>`.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-262">When importing data from a local emulator, set hello endpoint too`https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="aa7e7-263"><a id="HBaseSource"></a>HBase gelen tooimport</span><span class="sxs-lookup"><span data-stu-id="aa7e7-263"><a id="HBaseSource"></a>tooimport from HBase</span></span>
<span data-ttu-id="aa7e7-264">Merhaba HBase kaynak alma seçeneği bir HBase tablosu tooimport verileri sağlar ve isteğe bağlı olarak hello verileri filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-264">hello HBase source importer option allows you tooimport data from an HBase table and optionally filter hello data.</span></span> <span data-ttu-id="aa7e7-265">Alma ayarı kadar kolay böylece çeşitli şablonlar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Ekran görüntüsü, HBase kaynak seçenekleri](./media/import-data/hbasesource1.png)

![Ekran görüntüsü, HBase kaynak seçenekleri](./media/import-data/hbasesource2.png)

<span data-ttu-id="aa7e7-268">Merhaba HBase Stargate bağlantı dizesi Hello biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-268">hello format of hello HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="aa7e7-269">Merhaba bağlantı dizesi alanına belirtilen HBase örneği hello kullan hello doğrula komutu tooensure erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-269">Use hello Verify command tooensure that hello HBase instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="aa7e7-270">Bir komut satırı örnek tooimport HBase gelen şöyledir:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-270">Here is a command line sample tooimport from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="aa7e7-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API (Toplu içe aktarma)</span><span class="sxs-lookup"><span data-stu-id="aa7e7-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="aa7e7-272">Hello Azure Cosmos DB toplu içeri Aktarıcı tooimport herhangi bir Azure Cosmos DB saklı yordamı için verimliliğini kullanarak hello kullanılabilir kaynak seçeneklerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-272">hello Azure Cosmos DB Bulk importer allows you tooimport from any of hello available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="aa7e7-273">Merhaba aracı yapabildiği verileri birden çok tek bölümlenmiş Azure Cosmos DB koleksiyonlar genelinde bölümlenmiş parçalı alma yanı sıra, içeri aktarma tooone tek bölümlenmiş Azure Cosmos DB koleksiyonu destekler.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-273">hello tool supports import tooone single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="aa7e7-274">Veri bölümlendirme hakkında daha fazla bilgi için bkz: [bölümleme ve Azure Cosmos DB'de ölçeklendirme](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="aa7e7-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="aa7e7-275">Merhaba aracı oluşturmak, çalıştırmak ve hello saklı yordamı hello hedef collection(s) silin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-275">hello tool will create, execute, and then delete hello stored procedure from hello target collection(s).</span></span>  

![Azure Cosmos DB ekran toplu seçenekleri](./media/import-data/documentdbbulk.png)

<span data-ttu-id="aa7e7-277">hello Azure Cosmos DB bağlantı dizesi Hello biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-277">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="aa7e7-278">Hello Azure Cosmos DB hesabı bağlantı dizesi açıklandığı gibi hello Azure portal, hello anahtarlar dikey penceresinden alınabilir [nasıl toomanage bir Azure Cosmos DB hesap](manage-account.md), ancak eklenmiş toobe toohello hello veritabanının hello adı gerekiyor bağlantı dizesi biçimi aşağıdaki hello olarak:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-278">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="aa7e7-279">Merhaba bağlantı dizesi alanına belirtilen Azure Cosmos DB örneği hello kullan hello doğrula komutu tooensure erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-279">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="aa7e7-280">tooimport tooa tek bir koleksiyon, verileri içeri aktarılır ve hello Ekle düğmesini tıklatın hello koleksiyonu toowhich hello adını girin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-280">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="aa7e7-281">tooimport toomultiple koleksiyonları, tek tek her koleksiyon adını girin veya birden çok koleksiyon sözdizimi toospecify aşağıdaki hello kullanın: *collection_prefix*[Başlangıç dizini - bitiş dizini].</span><span class="sxs-lookup"><span data-stu-id="aa7e7-281">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="aa7e7-282">Merhaba daha önce bahsedilen söz dizimi aracılığıyla birden çok koleksiyon belirtirken, hello aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-282">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="aa7e7-283">Yalnızca tamsayı aralığı adı desenleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="aa7e7-284">Koleksiyonunu [0-3] belirten hello koleksiyonlar aşağıdaki gibi oluşturur: Koleksiyon0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-284">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="aa7e7-285">Kısaltılmış sözdizimi kullanabilirsiniz: Koleksiyon [3], 1. adımda bahsedilen koleksiyonları aynı kümesini yayma.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="aa7e7-286">Birden fazla değiştirme sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-286">More than one substitution can be provided.</span></span> <span data-ttu-id="aa7e7-287">Örneğin, [0-1] [0-9] koleksiyonuna baştaki sıfırlarla 20 koleksiyon adları oluşturur (collection01,.. 02... 03).</span><span class="sxs-lookup"><span data-stu-id="aa7e7-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="aa7e7-288">Merhaba koleksiyon adı belirtilmiş sonra hello istenen hello collection(s) (400 RUs too10, 000 RUs) verimini seçin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-288">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too10,000 RUs).</span></span> <span data-ttu-id="aa7e7-289">En iyi alma performans için daha fazla üretilen işi seçin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="aa7e7-290">Performans düzeyleri hakkında daha fazla bilgi için bkz: [Azure Cosmos veritabanı performans düzeyleri](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="aa7e7-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="aa7e7-291">Merhaba performans verimlilik ayarı yalnızca toocollection oluşturma geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-291">hello performance throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="aa7e7-292">Merhaba koleksiyon zaten var. belirtilmişse, üretilen iş değiştirilmeyecek.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-292">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="aa7e7-293">Toomultiple koleksiyonları içeri aktarırken hello içeri aktarma aracını tabanlı karma parçalama destekler.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-293">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="aa7e7-294">Bu senaryoda, istediğiniz toouse bölüm anahtarı hello gibi hello belge özelliği belirtin (bölüm anahtarı boş bırakılırsa, belgeleri rastgele hello hedef koleksiyonlarındaki parçalı olacaktır).</span><span class="sxs-lookup"><span data-stu-id="aa7e7-294">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="aa7e7-295">İsteğe bağlı olarak, hangi hello alma kaynağı alanında hello alma (belgeleri bu özellik içermiyorsa, ardından hello içeri aktarma aracını GUID hello kimliği özellik değeri olarak oluşturacağını unutmayın) sırasında Azure Cosmos DB belge kimliği özelliği hello kullanılması gereken belirtebilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-295">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="aa7e7-296">İçeri aktarma sırasında birkaç Gelişmiş Seçenekler yok.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="aa7e7-297">İlk olarak, hello aracı içerir ancak varsayılan toplu alma saklı yordam (BulkInsert.js), kendi depolanan içeri aktarma yordamı toospecify tercih edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-297">First, while hello tool includes a default bulk import stored procedure (BulkInsert.js), you may choose toospecify your own import stored procedure:</span></span>

 ![Azure Cosmos DB ekran bulk INSERT sproc seçeneği](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="aa7e7-299">Ayrıca, tarih türleri (örn. SQL Server veya MongoDB) alırken, üç alma seçenekler arasından seçim yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Azure Cosmos DB ekran tarih saat içeri aktarma seçenekleri](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="aa7e7-301">Dize: bir dize değeri olarak sürdürülemedi</span><span class="sxs-lookup"><span data-stu-id="aa7e7-301">String: Persist as a string value</span></span>
* <span data-ttu-id="aa7e7-302">Dönem: bir dönem sayı değeri kalır</span><span class="sxs-lookup"><span data-stu-id="aa7e7-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="aa7e7-303">Her ikisi: hem dize hem de dönem sayı değerlerini kalıcı olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="aa7e7-304">Bu seçenek bir alt örneğin oluşturur: "date_joined": {"Value": "2013-10-21T21:17:25.2410000Z", "dönem": 1382390245}</span><span class="sxs-lookup"><span data-stu-id="aa7e7-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="aa7e7-305">Hello Azure Cosmos DB toplu içeri Aktarıcı hello aşağıdaki ek gelişmiş seçenekler vardır:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-305">hello Azure Cosmos DB Bulk importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="aa7e7-306">Toplu iş boyutu: hello aracı Varsayılanları tooa toplu iş boyutu 50.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-306">Batch Size: hello tool defaults tooa batch size of 50.</span></span>  <span data-ttu-id="aa7e7-307">Alınan hello belgeleri toobe büyükse hello toplu iş boyutunu azaltmayı göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-307">If hello documents toobe imported are large, consider lowering hello batch size.</span></span> <span data-ttu-id="aa7e7-308">Alınan hello belgeleri toobe küçükse, buna karşılık, hello toplu iş boyutu yükseltme göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-308">Conversely, if hello documents toobe imported are small, consider raising hello batch size.</span></span>
2. <span data-ttu-id="aa7e7-309">En fazla komut dosyası boyutu (bayt): hello aracı Varsayılanları tooa en fazla betik boyutu 512KB</span><span class="sxs-lookup"><span data-stu-id="aa7e7-309">Max Script Size (bytes): hello tool defaults tooa max script size of 512KB</span></span>
3. <span data-ttu-id="aa7e7-310">Otomatik kimliği oluşturma devre dışı bırak: içeri aktarılan her belge toobe kimlik alanı içeriyorsa, bu seçeneğin belirlenmesi performansını artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-310">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="aa7e7-311">Benzersiz kimliği alanı eksik belgeleri içeri aktarılmayacak.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="aa7e7-312">Güncelleştirme mevcut belgeler: varolan belgeleri kimliği çakışmaları ile değiştirerek hello aracı Varsayılanları toonot.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-312">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="aa7e7-313">Bu seçeneğin kimlikleriyle eşleşen ile varolan belgeleri üzerine izin verir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="aa7e7-314">Bu özellik, varolan belgeleri güncelleştirme zamanlanan veri geçişler için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="aa7e7-315">Hata yeniden deneme sayısı: hello kaç kez tooretry hello geçici hataları (örneğin ağ bağlantı kesintisi) olması durumunda bağlantı tooAzure Cosmos DB belirtir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-315">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="aa7e7-316">Yeniden deneme aralığı: geçici hataları (örneğin ağ bağlantı kesintisi) durumunda hello bağlantı tooAzure Cosmos DB yeniden deneniyor arasında ne kadar süreyle toowait belirtir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-316">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="aa7e7-317">Bağlantı modu: Azure Cosmos DB ile Merhaba bağlantı modu toouse belirtir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-317">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="aa7e7-318">Merhaba kullanılabilir DirectTcp, DirectHttps ve ağ geçidi seçimlerdir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-318">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="aa7e7-319">yalnızca 443 numaralı bağlantı noktasını kullanır gibi hello ağ geçidi modu daha fazla güvenlik duvarı kolay ederken hello doğrudan bağlantı modları, daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-319">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Gelişmiş Seçenekleri Azure Cosmos DB ekran toplu içeri aktarma](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="aa7e7-321">Merhaba aracı Varsayılanları tooconnection modu DirectTcp içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-321">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="aa7e7-322">Güvenlik Duvarı sorunlarla karşılaşırsanız, yalnızca bağlantı noktası 443 gerektirdiğinden tooconnection modu ağ geçidi geçin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-322">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="aa7e7-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API (sıralı kayıt içe aktarma)</span><span class="sxs-lookup"><span data-stu-id="aa7e7-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="aa7e7-324">Hello Azure Cosmos DB sıralı kayıt alma tooimport herhangi bir kayıt kayıt temelinde hello kullanılabilir kaynak seçenekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-324">hello Azure Cosmos DB sequential record importer allows you tooimport from any of hello available source options on a record by record basis.</span></span> <span data-ttu-id="aa7e7-325">Saklı yordamlar kotasına ulaştı olan bir koleksiyon tooan alıyorsanız bu seçeneği belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-325">You might choose this option if you’re importing tooan existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="aa7e7-326">Merhaba aracı destekler alma tooa tek parçalı içeri aktarma verileri birden çok tek bölümlü ve/veya birden çok bölüm Azure Cosmos DB koleksiyonlar genelinde yapabildiği bölümlenmiş yanı sıra (tek bölüm ve birden çok bölüm) Azure Cosmos DB koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-326">hello tool supports import tooa single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="aa7e7-327">Veri bölümlendirme hakkında daha fazla bilgi için bkz: [bölümleme ve Azure Cosmos DB'de ölçeklendirme](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="aa7e7-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Azure Cosmos DB ekran sıralı kayıt içeri aktarma seçenekleri](./media/import-data/documentdbsequential.png)

<span data-ttu-id="aa7e7-329">hello Azure Cosmos DB bağlantı dizesi Hello biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-329">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="aa7e7-330">Hello Azure Cosmos DB hesabı bağlantı dizesi açıklandığı gibi hello Azure portal, hello anahtarlar dikey penceresinden alınabilir [nasıl toomanage bir Azure Cosmos DB hesap](manage-account.md), ancak eklenmiş toobe toohello hello veritabanının hello adı gerekiyor bağlantı dizesi biçimi aşağıdaki hello olarak:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-330">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="aa7e7-331">Merhaba bağlantı dizesi alanına belirtilen Azure Cosmos DB örneği hello kullan hello doğrula komutu tooensure erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-331">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="aa7e7-332">tooimport tooa tek bir koleksiyon, verileri içeri aktarılır ve hello Ekle düğmesini tıklatın hello koleksiyonu toowhich hello adını girin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-332">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="aa7e7-333">tooimport toomultiple koleksiyonları, tek tek her koleksiyon adını girin veya birden çok koleksiyon sözdizimi toospecify aşağıdaki hello kullanın: *collection_prefix*[Başlangıç dizini - bitiş dizini].</span><span class="sxs-lookup"><span data-stu-id="aa7e7-333">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="aa7e7-334">Merhaba daha önce bahsedilen söz dizimi aracılığıyla birden çok koleksiyon belirtirken, hello aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-334">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="aa7e7-335">Yalnızca tamsayı aralığı adı desenleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="aa7e7-336">Koleksiyonunu [0-3] belirten hello koleksiyonlar aşağıdaki gibi oluşturur: Koleksiyon0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-336">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="aa7e7-337">Kısaltılmış sözdizimi kullanabilirsiniz: Koleksiyon [3], 1. adımda bahsedilen koleksiyonları aynı kümesini yayma.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="aa7e7-338">Birden fazla değiştirme sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-338">More than one substitution can be provided.</span></span> <span data-ttu-id="aa7e7-339">Örneğin, [0-1] [0-9] koleksiyonuna baştaki sıfırlarla 20 koleksiyon adları oluşturur (collection01,.. 02... 03).</span><span class="sxs-lookup"><span data-stu-id="aa7e7-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="aa7e7-340">Merhaba koleksiyon adı belirtilmiş sonra hello istenen hello collection(s) (400 RUs too250, 000 RUs) verimini seçin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-340">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too250,000 RUs).</span></span> <span data-ttu-id="aa7e7-341">En iyi alma performans için daha fazla üretilen işi seçin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="aa7e7-342">Performans düzeyleri hakkında daha fazla bilgi için bkz: [Azure Cosmos veritabanı performans düzeyleri](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="aa7e7-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="aa7e7-343">Üretilen iş ile toocollections verebilirsiniz > 10.000 RUs bölüm anahtarı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-343">Any import toocollections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="aa7e7-344">Birden fazla 250.000 RUs toohave seçerseniz, hesabınızın artan bir istekte hello portal toohave toofile gerekir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-344">If you choose toohave more than 250,000 RUs, you will need toofile a request in hello portal toohave your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="aa7e7-345">Merhaba verimlilik ayarı yalnızca toocollection oluşturma geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-345">hello throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="aa7e7-346">Merhaba koleksiyon zaten var. belirtilmişse, üretilen iş değiştirilmeyecek.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-346">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="aa7e7-347">Toomultiple koleksiyonları içeri aktarırken hello içeri aktarma aracını tabanlı karma parçalama destekler.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-347">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="aa7e7-348">Bu senaryoda, istediğiniz toouse bölüm anahtarı hello gibi hello belge özelliği belirtin (bölüm anahtarı boş bırakılırsa, belgeleri rastgele hello hedef koleksiyonlarındaki parçalı olacaktır).</span><span class="sxs-lookup"><span data-stu-id="aa7e7-348">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="aa7e7-349">İsteğe bağlı olarak, hangi hello alma kaynağı alanında hello alma (belgeleri bu özellik içermiyorsa, ardından hello içeri aktarma aracını GUID hello kimliği özellik değeri olarak oluşturacağını unutmayın) sırasında Azure Cosmos DB belge kimliği özelliği hello kullanılması gereken belirtebilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-349">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="aa7e7-350">İçeri aktarma sırasında birkaç Gelişmiş Seçenekler yok.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="aa7e7-351">İlk olarak, tarih türleri (örn. SQL Server veya MongoDB) alırken, üç alma seçenekler arasından seçim yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Azure Cosmos DB ekran tarih saat içeri aktarma seçenekleri](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="aa7e7-353">Dize: bir dize değeri olarak sürdürülemedi</span><span class="sxs-lookup"><span data-stu-id="aa7e7-353">String: Persist as a string value</span></span>
* <span data-ttu-id="aa7e7-354">Dönem: bir dönem sayı değeri kalır</span><span class="sxs-lookup"><span data-stu-id="aa7e7-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="aa7e7-355">Her ikisi: hem dize hem de dönem sayı değerlerini kalıcı olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="aa7e7-356">Bu seçenek bir alt örneğin oluşturur: "date_joined": {"Value": "2013-10-21T21:17:25.2410000Z", "dönem": 1382390245}</span><span class="sxs-lookup"><span data-stu-id="aa7e7-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="aa7e7-357">Hello Azure Cosmos DB - sıralı kayıt içeri Aktarıcı hello aşağıdaki ek gelişmiş seçenekler vardır:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-357">hello Azure Cosmos DB - Sequential record importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="aa7e7-358">Paralel istek sayısı: hello aracı Varsayılanları too2 paralel istekler.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-358">Number of Parallel Requests: hello tool defaults too2 parallel requests.</span></span> <span data-ttu-id="aa7e7-359">Alınan hello belgeleri toobe küçükse, paralel istek hello sayısı oluşturma göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-359">If hello documents toobe imported are small, consider raising hello number of parallel requests.</span></span> <span data-ttu-id="aa7e7-360">Bu sayı çok fazla tetiklenir alma hello açtıysanız, azaltma karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-360">Note that if this number is raised too much, hello import may experience throttling.</span></span>
2. <span data-ttu-id="aa7e7-361">Otomatik kimliği oluşturma devre dışı bırak: içeri aktarılan her belge toobe kimlik alanı içeriyorsa, bu seçeneğin belirlenmesi performansını artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-361">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="aa7e7-362">Benzersiz kimliği alanı eksik belgeleri içeri aktarılmayacak.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="aa7e7-363">Güncelleştirme mevcut belgeler: varolan belgeleri kimliği çakışmaları ile değiştirerek hello aracı Varsayılanları toonot.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-363">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="aa7e7-364">Bu seçeneğin kimlikleriyle eşleşen ile varolan belgeleri üzerine izin verir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="aa7e7-365">Bu özellik, varolan belgeleri güncelleştirme zamanlanan veri geçişler için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="aa7e7-366">Hata yeniden deneme sayısı: hello kaç kez tooretry hello geçici hataları (örneğin ağ bağlantı kesintisi) olması durumunda bağlantı tooAzure Cosmos DB belirtir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-366">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="aa7e7-367">Yeniden deneme aralığı: geçici hataları (örneğin ağ bağlantı kesintisi) durumunda hello bağlantı tooAzure Cosmos DB yeniden deneniyor arasında ne kadar süreyle toowait belirtir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-367">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="aa7e7-368">Bağlantı modu: Azure Cosmos DB ile Merhaba bağlantı modu toouse belirtir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-368">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="aa7e7-369">Merhaba kullanılabilir DirectTcp, DirectHttps ve ağ geçidi seçimlerdir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-369">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="aa7e7-370">yalnızca 443 numaralı bağlantı noktasını kullanır gibi hello ağ geçidi modu daha fazla güvenlik duvarı kolay ederken hello doğrudan bağlantı modları, daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-370">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Gelişmiş Seçenekleri Azure Cosmos DB ekran sıralı kayıt alma](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="aa7e7-372">Merhaba aracı Varsayılanları tooconnection modu DirectTcp içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-372">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="aa7e7-373">Güvenlik Duvarı sorunlarla karşılaşırsanız, yalnızca bağlantı noktası 443 gerektirdiğinden tooconnection modu ağ geçidi geçin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-373">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="aa7e7-374"><a id="IndexingPolicy"></a>Azure Cosmos DB koleksiyonları oluştururken bir dizin oluşturma ilkesini belirtin</span><span class="sxs-lookup"><span data-stu-id="aa7e7-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="aa7e7-375">Merhaba geçiş aracı toocreate koleksiyonları içeri aktarma sırasında izin verdiğinizde, hello koleksiyonların hello dizin oluşturma ilkesini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-375">When you allow hello migration tool toocreate collections during import, you can specify hello indexing policy of hello collections.</span></span> <span data-ttu-id="aa7e7-376">Gelişmiş Seçenekler bölümünde hello Azure Cosmos DB toplu alma ve Azure Cosmos DB sıralı kaydını seçenekleri hello toohello dizin oluşturma ilkesi bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-376">In hello advanced options section of hello Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate toohello Indexing Policy section.</span></span>

![Ekran Azure Cosmos DB dizin Gelişmiş Seçenekler ilke](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="aa7e7-378">Hello İlkesi Gelişmiş dizin oluşturma seçeneğini kullanarak, bir dizin oluşturma ilke dosyası seçin, el ile bir dizin oluşturma ilkesi girin veya (varsayılan şablonları kümesinden sağ hello İlkesi textbox dizin tıklayarak) seçin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-378">Using hello Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in hello indexing policy textbox).</span></span>

<span data-ttu-id="aa7e7-379">Merhaba aracı sağlar hello ilkesi şablonları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-379">hello policy templates hello tool provides are:</span></span>

* <span data-ttu-id="aa7e7-380">Varsayılan.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-380">Default.</span></span> <span data-ttu-id="aa7e7-381">Dizeleri eşitlik sorguları gerçekleştirme ve sıralama, aralık ve eşitlik sorguları için numaraları kullanarak bu en iyi bir ilkedir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="aa7e7-382">Bu ilkeyi daha az dizin depolama yükü aralığından daha vardır.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="aa7e7-383">Aralık.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-383">Range.</span></span> <span data-ttu-id="aa7e7-384">Bu ilke hem sayılara hem de dizeleri sıralama, aralık ve eşitlik sorguları kullanmakta olduğunuz en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="aa7e7-385">Bu ilke varsayılan veya karma daha yüksek bir dizin depolama yükü var.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Ekran Azure Cosmos DB dizin Gelişmiş Seçenekler ilke](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="aa7e7-387">Bir dizin oluşturma ilkesi belirtmezseniz hello varsayılan ilke uygulanır.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-387">If you do not specify an indexing policy, then hello default policy will be applied.</span></span> <span data-ttu-id="aa7e7-388">Dizin oluşturma ilkeleri hakkında daha fazla bilgi için bkz: [Azure Cosmos ilkeleri dizin DB](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="aa7e7-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-toojson-file"></a><span data-ttu-id="aa7e7-389">Dışarı aktarma tooJSON dosyası</span><span class="sxs-lookup"><span data-stu-id="aa7e7-389">Export tooJSON file</span></span>
<span data-ttu-id="aa7e7-390">Hello Azure Cosmos DB JSON verici tooexport verir herhangi birini içeren bir dizi JSON belgelerini hello kullanılabilir kaynak seçenekleri tooa JSON dosyası.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-390">hello Azure Cosmos DB JSON exporter allows you tooexport any of hello available source options tooa JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="aa7e7-391">Merhaba aracı hello verme sizin için işler veya tooview hello ortaya çıkan geçiş komut seçin ve kendiniz hello komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-391">hello tool will handle hello export for you, or you can choose tooview hello resulting migration command and run hello command yourself.</span></span> <span data-ttu-id="aa7e7-392">Merhaba sonuçta elde edilen JSON dosyasını yerel olarak veya Azure Blob Depolama alanında depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-392">hello resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Ekran Azure Cosmos DB JSON yerel dosya dışa aktarma seçeneği](./media/import-data/jsontarget.png)

![Azure Cosmos DB JSON Azure Blob'ın ekran depolama dışa aktarma seçeneği](./media/import-data/jsontarget2.png)

<span data-ttu-id="aa7e7-395">İsteğe bağlı olarak hello yaparak daha fazla okunabilir içeriği sırada hello elde edilen belgenin hello boyutu artıran JSON kaynaklanan tooprettify hello seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-395">You may optionally choose tooprettify hello resulting JSON, which will increase hello size of hello resulting document while making hello contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places toosee in Paris"}]}]

    Prettified JSON export
    [
     {
    "id": "Sample",
    "Title": "About Paris",
    "Language": {
      "Name": "English"
    },
    "Author": {
      "Name": "Don",
      "Location": {
        "City": "Paris",
        "Country": "France"
      }
    },
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places toosee in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a><span data-ttu-id="aa7e7-396">Gelişmiş yapılandırma</span><span class="sxs-lookup"><span data-stu-id="aa7e7-396">Advanced configuration</span></span>
<span data-ttu-id="aa7e7-397">Merhaba Gelişmiş yapılandırma ekranında yazılmış hataları istediğiniz hello günlük dosyası toowhich hello konumunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-397">In hello Advanced configuration screen, specify hello location of hello log file toowhich you would like any errors written.</span></span> <span data-ttu-id="aa7e7-398">Kuralları aşağıdaki hello toothis sayfayı uygulayın:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-398">hello following rules apply toothis page:</span></span>

1. <span data-ttu-id="aa7e7-399">Bir dosya adı sağlanmazsa, tüm hataları hello sonuçları sayfasında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-399">If a file name is not provided, then all errors will be returned on hello Results page.</span></span>
2. <span data-ttu-id="aa7e7-400">Bir dosya adı olmadan bir dizin sağlanırsa, ardından hello dosya oluşturulan (üzerine hello geçerli ortam dizinde veya).</span><span class="sxs-lookup"><span data-stu-id="aa7e7-400">If a file name is provided without a directory, then hello file will be created (or overwritten) in hello current environment directory.</span></span>
3. <span data-ttu-id="aa7e7-401">Var olan belirlerseniz dosyası sonra hello dosyasının üzerine yazılır, ek bir seçenek yoktur.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-401">If you select an existing file, then hello file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="aa7e7-402">Ardından, olup olmadığını toolog tüm kritik veya herhangi bir hata iletisi.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-402">Then, choose whether toolog all, critical, or no error messages.</span></span> <span data-ttu-id="aa7e7-403">Son olarak, ne sıklıkta Merhaba ekranında aktarımı iletideki ilerlemesini ile güncelleştirilecek karar verin.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-403">Finally, decide how frequently hello on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="aa7e7-404">Ayarları içeri aktarma ve görünüm komut satırında onaylayın</span><span class="sxs-lookup"><span data-stu-id="aa7e7-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="aa7e7-405">Kaynak bilgileri, hedef bilgileri ve Gelişmiş Yapılandırma belirtme sonra hello geçiş özeti gözden geçirin ve isteğe bağlı olarak, görünüm/kopyalama (kopyalama hello komutu yararlı tooautomate alma işlemleri) geçiş komutu kaynaklanan hello:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-405">After specifying source information, target information, and advanced configuration, review hello migration summary and, optionally, view/copy hello resulting migration command (copying hello command is useful tooautomate import operations):</span></span>
   
    ![Özet ekranının ekran görüntüsü](./media/import-data/summary.png)
   
    ![Özet ekranının ekran görüntüsü](./media/import-data/summarycommand.png)
2. <span data-ttu-id="aa7e7-408">Kaynak ve hedef seçeneklerle memnun kaldıktan sonra tıklatın **alma**.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="aa7e7-409">Merhaba alma işleminde olduğu gibi hello geçen süre, aktarılan sayısı ve (Merhaba Gelişmiş Yapılandırma bir dosya adı kaydetmedi sağlarsanız) hata bilgileri güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-409">hello elapsed time, transferred count, and failure information (if you didn't provide a file name in hello Advanced configuration) will update as hello import is in process.</span></span> <span data-ttu-id="aa7e7-410">Tamamlandıktan sonra hello sonuçları (örneğin toodeal alma hataları ile) dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-410">Once complete, you can export hello results (e.g. toodeal with any import failures).</span></span>
   
    ![Ekran Azure Cosmos DB JSON dışa aktarma seçeneği](./media/import-data/viewresults.png)
3. <span data-ttu-id="aa7e7-412">Yeni bir içeri aktarma hello var olan ayarları (ör. bağlantı dizesi bilgilerini, kaynak ve hedef seçimi, vb.) tutma ya da tüm değerleri sıfırlama da başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-412">You may also start a new import, either keeping hello existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Ekran Azure Cosmos DB JSON dışa aktarma seçeneği](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="aa7e7-414">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aa7e7-414">Next steps</span></span>

<span data-ttu-id="aa7e7-415">Bu öğreticide, hello aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="aa7e7-415">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aa7e7-416">Merhaba veri geçiş aracı yüklü</span><span class="sxs-lookup"><span data-stu-id="aa7e7-416">Installed hello Data Migration tool</span></span>
> * <span data-ttu-id="aa7e7-417">Farklı veri kaynaklarından alınan verileri</span><span class="sxs-lookup"><span data-stu-id="aa7e7-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="aa7e7-418">Azure Cosmos DB tooJSON dışarı</span><span class="sxs-lookup"><span data-stu-id="aa7e7-418">Exported from Azure Cosmos DB tooJSON</span></span>

<span data-ttu-id="aa7e7-419">Şimdi toohello sonraki öğretici devam ve öğrenin nasıl Azure Cosmos DB kullanarak tooquery verileri.</span><span class="sxs-lookup"><span data-stu-id="aa7e7-419">You can now proceed toohello next tutorial and learn how tooquery data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="aa7e7-420">Nasıl tooquery veri?</span><span class="sxs-lookup"><span data-stu-id="aa7e7-420">How tooquery data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
