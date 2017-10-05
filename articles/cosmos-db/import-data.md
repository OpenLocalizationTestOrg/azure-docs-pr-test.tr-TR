---
title: "Azure Cosmos DB veritabanı geçiş aracını | Microsoft Docs"
description: "Açık kaynak Azure Cosmos DB veri geçiş araçları Azure Cosmos DB MongoDB, SQL Server, tablo depolama, Amazon DynamoDB, CSV ve JSON dosyaları dahil olmak üzere çeşitli kaynaklardan veri almak için nasıl kullanılacağını öğrenin. CSV JSON dönüştürme."
keywords: "json, veritabanı Geçiş Araçları, CSV'ye Dönüştür csv için json"
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
ms.openlocfilehash: 23a4a82dbdb611f4da90562af936fca28da9b24d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-data-into-azure-cosmos-db-for-the-documentdb-api"></a><span data-ttu-id="e3cbd-105">DocumentDB API için Azure Cosmos Veritabanına veri almak nasıl?</span><span class="sxs-lookup"><span data-stu-id="e3cbd-105">How to import data into Azure Cosmos DB for the DocumentDB API?</span></span>

<span data-ttu-id="e3cbd-106">Bu öğretici Azure Cosmos DB kullanma hakkında yönergeler sağlar: JSON dosyaları dahil olmak üzere çeşitli kaynaklardan veri aktarabilirsiniz DocumentDB API veri geçiş aracı CSV dosyaları, SQL, MongoDB, Azure Table storage, Amazon DynamoDB ve Azure Cosmos DB DocumentDB API'si Azure Cosmos DB ve DocumentDB API ile kullanılmak üzere koleksiyonlara koleksiyonları.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-106">This tutorial provides instructions on using the Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and the DocumentDB API.</span></span> <span data-ttu-id="e3cbd-107">Veri Geçiş Aracı, tek bir bölüm koleksiyondan DocumentDB API için çok bölümlü bir koleksiyon için geçirirken kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-107">The Data Migration tool can also be used when migrating from a single partition collection to a multi-partition collection for the DocumentDB API.</span></span>

<span data-ttu-id="e3cbd-108">Veri Geçiş Aracı, yalnızca Azure Cosmos DB için içeri aktarma verileri DocumentDB API'si ile kullandığınızda çalışır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-108">The Data Migration tool only works when importing data into Azure Cosmos DB for use with the DocumentDB API.</span></span> <span data-ttu-id="e3cbd-109">Tablo API veya grafik API'si ile kullanmak için veri içe aktarımı şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-109">Importing data for use with the Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="e3cbd-110">MongoDB API ile kullanmak için veri almak için bkz: [Azure Cosmos DB: MongoDB API'si veri geçirmek nasıl?](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="e3cbd-110">To import data for use with the MongoDB API, see [Azure Cosmos DB: How to migrate data for the MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="e3cbd-111">Bu öğretici, aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-111">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e3cbd-112">Veri geçiş aracı yükleme</span><span class="sxs-lookup"><span data-stu-id="e3cbd-112">Installing the Data Migration tool</span></span>
> * <span data-ttu-id="e3cbd-113">Farklı veri kaynaklarından veri alma</span><span class="sxs-lookup"><span data-stu-id="e3cbd-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="e3cbd-114">Azure Cosmos DB JSON olarak dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="e3cbd-114">Exporting from Azure Cosmos DB to JSON</span></span>

## <span data-ttu-id="e3cbd-115"><a id="Prerequisites"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e3cbd-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="e3cbd-116">Bu makaledeki yönergeleri izlemeden önce aşağıdakilerin yüklü olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-116">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="e3cbd-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="e3cbd-118"><a id="Overviewl"></a>Veri Geçiş Aracı genel bakış</span><span class="sxs-lookup"><span data-stu-id="e3cbd-118"><a id="Overviewl"></a>Overview of the Data Migration tool</span></span>
<span data-ttu-id="e3cbd-119">Veri Geçiş Aracı, verileri Azure Cosmos DB bir çeşitli kaynaklardan dahil olmak üzere, içe aktaran bir açık kaynak çözümü olmasıdır:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-119">The Data Migration tool is an open source solution that imports data to Azure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="e3cbd-120">JSON dosyaları</span><span class="sxs-lookup"><span data-stu-id="e3cbd-120">JSON files</span></span>
* <span data-ttu-id="e3cbd-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="e3cbd-121">MongoDB</span></span>
* <span data-ttu-id="e3cbd-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="e3cbd-122">SQL Server</span></span>
* <span data-ttu-id="e3cbd-123">CSV dosyaları</span><span class="sxs-lookup"><span data-stu-id="e3cbd-123">CSV files</span></span>
* <span data-ttu-id="e3cbd-124">Azure Tablo depolama</span><span class="sxs-lookup"><span data-stu-id="e3cbd-124">Azure Table storage</span></span>
* <span data-ttu-id="e3cbd-125">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="e3cbd-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="e3cbd-126">HBase</span><span class="sxs-lookup"><span data-stu-id="e3cbd-126">HBase</span></span>
* <span data-ttu-id="e3cbd-127">Azure Cosmos DB koleksiyonları</span><span class="sxs-lookup"><span data-stu-id="e3cbd-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="e3cbd-128">Bir grafik kullanıcı arabirimi (dtui.exe) alma aracı içerir, ancak bunu da komut satırından (dt.exe) bulunarak belirlenebilir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-128">While the import tool includes a graphical user interface (dtui.exe), it can also be driven from the command line (dt.exe).</span></span> <span data-ttu-id="e3cbd-129">Aslında, kullanıcı Arabirimi aracılığıyla içe kurduktan sonra ilişkili komut çıktısı için bir seçenek yoktur.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-129">In fact, there is an option to output the associated command after setting up an import through the UI.</span></span> <span data-ttu-id="e3cbd-130">Hiyerarşik ilişkileri (alt) içeri aktarma sırasında oluşturulabilir, tablo kaynak verileri (örn. SQL Server ya da CSV dosyaları) dönüştürülebilir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="e3cbd-131">Kaynak seçenekleri hakkında daha fazla bilgi için her bir kaynak, hedef seçenekleri ve görüntüleme içeri aktarma sonuçları almak için komut satırları örnek okuma tutun.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-131">Keep reading to learn more about source options, sample command lines to import from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="e3cbd-132"><a id="Install"></a>Veri Taşıma aracını yükle</span><span class="sxs-lookup"><span data-stu-id="e3cbd-132"><a id="Install"></a>Install the Data Migration tool</span></span>
<span data-ttu-id="e3cbd-133">Geçiş Aracı kaynak kodu Github'da üzerinde kullanılabilir [bu havuzda](https://github.com/azure/azure-documentdb-datamigrationtool) ve derlenmiş bir sürüm kullanılabilir [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span><span class="sxs-lookup"><span data-stu-id="e3cbd-133">The migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="e3cbd-134">Çözümü derlemek veya yalnızca karşıdan yükleyip derlenmiş sürümünü tercih ettiğiniz bir dizine ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-134">You may either compile the solution or simply download and extract the compiled version to a directory of your choice.</span></span> <span data-ttu-id="e3cbd-135">Ardından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-135">Then run either:</span></span>

* <span data-ttu-id="e3cbd-136">**Dtui.exe**: grafik arabirim aracı sürümü</span><span class="sxs-lookup"><span data-stu-id="e3cbd-136">**Dtui.exe**: Graphical interface version of the tool</span></span>
* <span data-ttu-id="e3cbd-137">**Dt.exe**: komut satırı aracı sürümü</span><span class="sxs-lookup"><span data-stu-id="e3cbd-137">**Dt.exe**: Command-line version of the tool</span></span>

## <a name="import-data"></a><span data-ttu-id="e3cbd-138">Veri içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="e3cbd-138">Import data</span></span>

<span data-ttu-id="e3cbd-139">Aracı yükledikten sonra verilerinizi almak için zaman yapılır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-139">Once you've installed the tool, it's time to import your data.</span></span> <span data-ttu-id="e3cbd-140">Ne tür verileri içeri aktarmak istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="e3cbd-140">What kind of data do you want to import?</span></span>

* [<span data-ttu-id="e3cbd-141">JSON dosyaları</span><span class="sxs-lookup"><span data-stu-id="e3cbd-141">JSON files</span></span>](#JSON)
* [<span data-ttu-id="e3cbd-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="e3cbd-142">MongoDB</span></span>](#MongoDB)
* [<span data-ttu-id="e3cbd-143">MongoDB dışarı aktarma dosyaları</span><span class="sxs-lookup"><span data-stu-id="e3cbd-143">MongoDB Export files</span></span>](#MongoDBExport)
* [<span data-ttu-id="e3cbd-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="e3cbd-144">SQL Server</span></span>](#SQL)
* [<span data-ttu-id="e3cbd-145">CSV dosyaları</span><span class="sxs-lookup"><span data-stu-id="e3cbd-145">CSV files</span></span>](#CSV)
* [<span data-ttu-id="e3cbd-146">Azure Tablo Depolama</span><span class="sxs-lookup"><span data-stu-id="e3cbd-146">Azure Table storage</span></span>](#AzureTableSource)
* [<span data-ttu-id="e3cbd-147">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="e3cbd-147">Amazon DynamoDB</span></span>](#DynamoDBSource)
* [<span data-ttu-id="e3cbd-148">BLOB</span><span class="sxs-lookup"><span data-stu-id="e3cbd-148">Blob</span></span>](#BlobImport)
* [<span data-ttu-id="e3cbd-149">Azure Cosmos DB koleksiyonları</span><span class="sxs-lookup"><span data-stu-id="e3cbd-149">Azure Cosmos DB collections</span></span>](#DocumentDBSource)
* [<span data-ttu-id="e3cbd-150">HBase</span><span class="sxs-lookup"><span data-stu-id="e3cbd-150">HBase</span></span>](#HBaseSource)
* [<span data-ttu-id="e3cbd-151">Azure Cosmos DB toplu içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="e3cbd-151">Azure Cosmos DB bulk import</span></span>](#DocumentDBBulkImport)
* [<span data-ttu-id="e3cbd-152">Azure Cosmos DB sıralı kayıt alma</span><span class="sxs-lookup"><span data-stu-id="e3cbd-152">Azure Cosmos DB sequential record import</span></span>](#DocumentDSeqTarget)


## <span data-ttu-id="e3cbd-153"><a id="JSON"></a>JSON dosyalarını içeri aktarmak için</span><span class="sxs-lookup"><span data-stu-id="e3cbd-153"><a id="JSON"></a>To import JSON files</span></span>
<span data-ttu-id="e3cbd-154">JSON dosyası kaynak alma seçeneği alma bir veya daha fazla tek bir belge JSON dosyaları veya JSON dosyaları her bir dizi JSON belgelerini içeren sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-154">The JSON file source importer option allows you to import one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="e3cbd-155">İçeri aktarmak için JSON dosyaları içeren klasörleri eklerken, alt klasörler dosyaları aranıyor yinelemeli seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-155">When adding folders that contain JSON files to import, you have the option of recursively searching for files in subfolders.</span></span>

![Ekran görüntüsü, JSON dosyası kaynak seçenekleri - veritabanı Geçiş Araçları](./media/import-data/jsonsource.png)

<span data-ttu-id="e3cbd-157">JSON dosyalarını içeri aktarmak için bazı komut satırı örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-157">Here are some command line samples to import JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition the data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <span data-ttu-id="e3cbd-158"><a id="MongoDB"></a>Adresinden içeri aktarmak için</span><span class="sxs-lookup"><span data-stu-id="e3cbd-158"><a id="MongoDB"></a>To import from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3cbd-159">MongoDB için desteği olan bir Azure Cosmos DB hesap alıyorsanız, aşağıdaki adımları [yönergeleri](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="e3cbd-159">If you are importing to an Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="e3cbd-160">MongoDB kaynak içeri Aktarıcı seçenek, tek bir MongoDB koleksiyonundan almak ve isteğe bağlı olarak bir sorgu kullanarak belgelere filtre ve/veya bir yansıtma kullanarak belge yapısı değiştirme olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-160">The MongoDB source importer option allows you to import from an individual MongoDB collection and optionally filter documents using a query and/or modify the document structure by using a projection.</span></span>  

![Ekran görüntüsü, MongoDB kaynak seçenekleri](./media/import-data/mongodbsource.png)

<span data-ttu-id="e3cbd-162">Bağlantı dizesi standart MongoDB biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-162">The connection string is in the standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="e3cbd-163">Bağlantı dizesi alanına belirtilen MongoDB örneği erişilebildiğinden emin olmak için Doğrula komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-163">Use the Verify command to ensure that the MongoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="e3cbd-164">Veri içeri aktarılacak koleksiyonun adını girin.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-164">Enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="e3cbd-165">İsteğe bağlı olarak belirttiğinizde veya bir sorgu için bir dosya belirtin (örneğin {pop: {$gt: 5000}}) ve/veya yansıtma (örneğin {loc:0}) hem filtre ve içeri aktarılacak veri şekli.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) to both filter and shape the data to be imported.</span></span>

<span data-ttu-id="e3cbd-166">Adresinden almak için bazı komut satırı örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-166">Here are some command line samples to import from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match the query and exclude the loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="e3cbd-167"><a id="MongoDBExport"></a>MongoDB verme dosyalarını içeri aktarmak için</span><span class="sxs-lookup"><span data-stu-id="e3cbd-167"><a id="MongoDBExport"></a>To import MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3cbd-168">MongoDB için desteği olan bir Azure Cosmos DB hesap alıyorsanız, aşağıdaki adımları [yönergeleri](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="e3cbd-168">If you are importing to an Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="e3cbd-169">MongoDB verme JSON dosyasını kaynak alma seçeneği mongoexport yardımcı programını üretilen bir veya daha fazla JSON dosyalarını içeri aktarmak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-169">The MongoDB export JSON file source importer option allows you to import one or more JSON files produced from the mongoexport utility.</span></span>  

![Ekran görüntüsü, MongoDB dışa aktarma kaynak seçenekleri](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="e3cbd-171">Alma için MongoDB verme JSON dosyaları içeren klasörleri eklerken, alt klasörler dosyaları aranıyor yinelemeli seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-171">When adding folders that contain MongoDB export JSON files for import, you have the option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="e3cbd-172">MongoDB verme JSON dosyalarından içeri aktarma için bir komut satırı örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-172">Here is a command line sample to import from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="e3cbd-173"><a id="SQL"></a>SQL Server'dan içeri aktarmak için</span><span class="sxs-lookup"><span data-stu-id="e3cbd-173"><a id="SQL"></a>To import from SQL Server</span></span>
<span data-ttu-id="e3cbd-174">SQL kaynak alma seçeneği, tek bir SQL Server veritabanından içeri aktarın ve isteğe bağlı olarak bir sorgu kullanarak içeri aktarılacak kayıtlarını filtrelemek sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-174">The SQL source importer option allows you to import from an individual SQL Server database and optionally filter the records to be imported using a query.</span></span> <span data-ttu-id="e3cbd-175">Ayrıca, bir iç içe geçmiş ayırıcı (daha ayrıntılı bir dakika içinde) belirterek, belge yapısı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-175">In addition, you can modify the document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![Ekran görüntüsü, SQL kaynak seçenekleri - veritabanı Geçiş Araçları](./media/import-data/sqlexportsource.png)

<span data-ttu-id="e3cbd-177">Bağlantı dizesi standart SQL bağlantı dizesi biçimi biçimidir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-177">The format of the connection string is the standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="e3cbd-178">Bağlantı dizesi alanında belirtilen SQL Server örneği erişilebildiğinden emin olmak için Doğrula komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-178">Use the Verify command to ensure that the SQL Server instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="e3cbd-179">İç içe geçmiş ayırıcı özellik alma sırasında hiyerarşik ilişkileri (alt belgeler) oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-179">The nesting separator property is used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="e3cbd-180">Aşağıdaki SQL sorgusunu göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-180">Consider the following SQL query:</span></span>

<span data-ttu-id="e3cbd-181">*Kimliği, ad, [Address.AddressType] olarak AddressType, AddressLine1 [Address.AddressLine1] olarak, [Address.Location.City] olarak Şehir, StateProvinceName [Address.Location.StateProvinceName] olarak, PostalCode [olarak dönüştürme (BusinessEntityID AS varchar) seçin Address.PostalCode], [Address.CountryRegionName] olarak CountryRegionName Sales.vStoreWithAddresses gelen nerede AddressType 'Ana ofis' =*</span><span class="sxs-lookup"><span data-stu-id="e3cbd-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="e3cbd-182">Aşağıdaki (kısmi) sonuçları döndüren:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-182">Which returns the following (partial) results:</span></span>

![Ekran görüntüsü, SQL sorgu sonuçları](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="e3cbd-184">Diğer adlar Address.AddressType ve Address.Location.StateProvinceName gibi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-184">Note the aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="e3cbd-185">İç içe geçmiş bir ayırıcı olarak belirterek '.', içeri aktarma aracını içeri aktarma sırasında adresi ve Address.Location belgeler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-185">By specifying a nesting separator of ‘.’, the import tool creates Address and Address.Location subdocuments during the import.</span></span> <span data-ttu-id="e3cbd-186">Azure Cosmos DB ortaya çıkan bir belgede bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="e3cbd-187">*{"ID": "956", "Name": "Yüksekse satış ve"Adres"hizmet": {"AddressType": "Ana ofis", "AddressLine1": "#500 75 O'Connor Sokak", "Konum": {"Şehir": "Ottawa", "StateProvinceName": "Ontario"}, "PostalCode": "K4B 1S2", "CountryRegionName": " Kanada"}}*</span><span class="sxs-lookup"><span data-stu-id="e3cbd-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="e3cbd-188">SQL Server'dan almak için bazı komut satırı örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-188">Here are some command line samples to import from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="e3cbd-189"><a id="CSV"></a>CSV dosyaları alıp CSV JSON biçimine Dönüştür</span><span class="sxs-lookup"><span data-stu-id="e3cbd-189"><a id="CSV"></a>To import CSV files and convert CSV to JSON</span></span>
<span data-ttu-id="e3cbd-190">CSV dosya kaynak içeri Aktarıcı seçeneği, bir veya daha fazla CSV dosyalarını içeri aktarmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-190">The CSV file source importer option enables you to import one or more CSV files.</span></span> <span data-ttu-id="e3cbd-191">İçeri aktarma için CSV dosyaları içeren klasörleri eklerken, alt klasörler dosyaları aranıyor yinelemeli seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-191">When adding folders that contain CSV files for import, you have the option of recursively searching for files in subfolders.</span></span>

![Ekran görüntüsü, CSV kaynak seçenekleri - JSON CSV'ye](media/import-data/csvsource.png)

<span data-ttu-id="e3cbd-193">SQL kaynağına benzer, iç içe geçmiş ayırıcı özellik alma sırasında hiyerarşik ilişkileri (alt belgeler) oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-193">Similar to the SQL source, the nesting separator property may be used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="e3cbd-194">Aşağıdaki CSV üstbilgisi satır ve veri satırı göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-194">Consider the following CSV header row and data rows:</span></span>

![Ekran görüntüsü, CSV örnek kayıtlarını - JSON CSV'ye](./media/import-data/csvsample.png)

<span data-ttu-id="e3cbd-196">Diğer adlar DomainInfo.Domain_Name ve RedirectInfo.Redirecting gibi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-196">Note the aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="e3cbd-197">İç içe geçmiş bir ayırıcı olarak belirterek '.', içeri aktarma aracını içeri aktarma sırasında DomainInfo ve RedirectInfo belgeler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-197">By specifying a nesting separator of ‘.’, the import tool will create DomainInfo and RedirectInfo subdocuments during the import.</span></span> <span data-ttu-id="e3cbd-198">Azure Cosmos DB ortaya çıkan bir belgede bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="e3cbd-199">*{"DomainInfo": {"Etki_alanı_adı": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV"}, "Federal Teşkilatı": "Yönetimsel konferans, Amerika Birleşik Devletleri", "RedirectInfo": {"Yeniden yönlendirme": "0", "Redirect_Destination": ""}, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d"}*</span><span class="sxs-lookup"><span data-stu-id="e3cbd-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="e3cbd-200">İçeri aktarma aracını (tırnak içine alınmış değerler her zaman dize olarak kabul edilir) türü bilgileri CSV dosyaları tırnak işareti olmayan değerleri Infer dener.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-200">The import tool will attempt to infer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="e3cbd-201">Türleri, aşağıdaki sırayla tanımlanır: sayı, datetime, Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-201">Types are identified in the following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="e3cbd-202">CSV Import hakkında dikkat edilecek iki noktalar vardır:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-202">There are two other things to note about CSV import:</span></span>

1. <span data-ttu-id="e3cbd-203">Tırnak içine alınmış değerler olarak korunur sırasında varsayılan olarak, tırnak işareti olmayan değerler her zaman sekmeler ve alanları için atılır-değil.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="e3cbd-204">Bu davranış kırpma tırnak içine alınmış değerler onay kutusunu veya /s.TrimQuoted komut satırı seçeneği ile geçersiz kılınabilir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-204">This behavior can be overridden with the Trim quoted values checkbox or the /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="e3cbd-205">Varsayılan olarak, tırnak işareti olmayan bir null, null değeri olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="e3cbd-206">Bu davranışı geçersiz kılınabilir (yani tırnak işareti olmayan bir null "null" dize olarak işle) ile kabul NULL dize onay kutusunu veya /s.NoUnquotedNulls komut satırı seçeneği olarak tırnak işareti olmayan.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with the Treat unquoted NULL as string checkbox or the /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="e3cbd-207">CSV içeri aktarma için bir komut satırı örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="e3cbd-208"><a id="AzureTableSource"></a>Azure tablo depolamasından içeri aktarmak için</span><span class="sxs-lookup"><span data-stu-id="e3cbd-208"><a id="AzureTableSource"></a>To import from Azure Table storage</span></span>
<span data-ttu-id="e3cbd-209">Azure Table depolama kaynağı alma seçeneği, tek bir Azure Table depolama tablosundan almak ve isteğe bağlı olarak içeri aktarılacak tablo varlıkları filtrelemek sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-209">The Azure Table storage source importer option allows you to import from an individual Azure Table storage table and optionally filter the table entities to be imported.</span></span> <span data-ttu-id="e3cbd-210">Tablo API ile kullanmak için Azure Cosmos Veritabanına Azure Table depolama veri almak için veri geçiş aracı kullanamayacağınızı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-210">Note that you cannot use the Data Migration tool to import Azure Table storage data into Azure Cosmos DB for use with the Table API.</span></span> <span data-ttu-id="e3cbd-211">Yalnızca Azure Cosmos DB DocumentDB API ile kullanmak için içeri aktarma şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-211">Only importing to Azure Cosmos DB for use with the DocumentDB API is supported at this time.</span></span>

![Azure tablo ekran depolama kaynağı seçenekleri](./media/import-data/azuretablesource.png)

<span data-ttu-id="e3cbd-213">Azure Table depolama bağlantı dizesi biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-213">The format of the Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="e3cbd-214">Bağlantı dizesi alanına belirtilen Azure Table depolama örneği erişilebildiğinden emin olmak için Doğrula komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-214">Use the Verify command to ensure that the Azure Table storage instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="e3cbd-215">Veri içeri aktarılacak Azure tablo adını girin.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-215">Enter the name of the Azure table from which data will be imported.</span></span> <span data-ttu-id="e3cbd-216">İsteğe bağlı olarak belirtebilir bir [filtre](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3cbd-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="e3cbd-217">Azure Table depolama kaynağı alma seçeneği aşağıdaki ek seçenekler vardır:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-217">The Azure Table storage source importer option has the following additional options:</span></span>

1. <span data-ttu-id="e3cbd-218">İç alanlar</span><span class="sxs-lookup"><span data-stu-id="e3cbd-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="e3cbd-219">Tüm - dahil tüm iç alanlar (PartitionKey, RowKey ve zaman damgası)</span><span class="sxs-lookup"><span data-stu-id="e3cbd-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="e3cbd-220">Hiçbiri - hariç tüm iç alanları</span><span class="sxs-lookup"><span data-stu-id="e3cbd-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="e3cbd-221">RowKey - yalnızca RowKey alan dahil et</span><span class="sxs-lookup"><span data-stu-id="e3cbd-221">RowKey - Only include the RowKey field</span></span>
2. <span data-ttu-id="e3cbd-222">Sütunları seçin</span><span class="sxs-lookup"><span data-stu-id="e3cbd-222">Select Columns</span></span>
   1. <span data-ttu-id="e3cbd-223">Azure tablo depolama filtrelerini tahminleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="e3cbd-224">Yalnızca belirli Azure tablo varlık özellikleri almak istiyorsanız, bunları seçin sütunlar listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-224">If you want to only import specific Azure Table entity properties, add them to the Select Columns list.</span></span> <span data-ttu-id="e3cbd-225">Diğer tüm varlık özellikleri yoksayılacak.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="e3cbd-226">Azure tablo depolamasından içeri aktarmak için bir komut satırı örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-226">Here is a command line sample to import from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="e3cbd-227"><a id="DynamoDBSource"></a>Amazon DynamoDB içeri aktarmak için</span><span class="sxs-lookup"><span data-stu-id="e3cbd-227"><a id="DynamoDBSource"></a>To import from Amazon DynamoDB</span></span>
<span data-ttu-id="e3cbd-228">Amazon DynamoDB kaynağı içeri Aktarıcı seçenek, tek tek bir Amazon DynamoDB tablosundan alma ve isteğe bağlı olarak içeri aktarılacak varlıklara filtre olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-228">The Amazon DynamoDB source importer option allows you to import from an individual Amazon DynamoDB table and optionally filter the entities to be imported.</span></span> <span data-ttu-id="e3cbd-229">Alma ayarı kadar kolay böylece çeşitli şablonlar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Amazon DynamoDB ekran kaynak seçenekleri - veritabanı Geçiş Araçları](./media/import-data/dynamodbsource1.png)

![Amazon DynamoDB ekran kaynak seçenekleri - veritabanı Geçiş Araçları](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="e3cbd-232">Amazon DynamoDB bağlantı dizesinin biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-232">The format of the Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="e3cbd-233">Bağlantı dizesi alanına belirtilen Amazon DynamoDB örneği erişilebildiğinden emin olmak için Doğrula komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-233">Use the Verify command to ensure that the Amazon DynamoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="e3cbd-234">Amazon DynamoDB içeri aktarmak için bir komut satırı örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-234">Here is a command line sample to import from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="e3cbd-235"><a id="BlobImport"></a>Azure Blob depolama alanından dosyalarını içeri aktarmak için</span><span class="sxs-lookup"><span data-stu-id="e3cbd-235"><a id="BlobImport"></a>To import files from Azure Blob storage</span></span>
<span data-ttu-id="e3cbd-236">JSON dosyasını, MongoDB dışarı aktarma dosyası ve CSV dosyası kaynak alma seçenekleri, bir veya daha fazla Azure Blob depolama alanından içeri aktarmanıza olanak verin.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-236">The JSON file, MongoDB export file, and CSV file source importer options allow you to import one or more files from Azure Blob storage.</span></span> <span data-ttu-id="e3cbd-237">Bir Blob kapsayıcı URL'si ve hesap anahtarı belirttikten sonra içeri aktarmak üzere dosyaları seçmek için normal bir ifade belirtmeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-237">After specifying a Blob container URL and Account Key, simply provide a regular expression to select the file(s) to import.</span></span>

![Ekran görüntüsü, Blob dosya kaynağı seçenekleri](./media/import-data/blobsource.png)

<span data-ttu-id="e3cbd-239">Azure Blob depolama alanından JSON dosyaları almak için komut satırı örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-239">Here is command line sample to import JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="e3cbd-240"><a id="DocumentDBSource"></a>Bir Azure Cosmos DB DocumentDB API koleksiyonundan içeri aktarmak için</span><span class="sxs-lookup"><span data-stu-id="e3cbd-240"><a id="DocumentDBSource"></a>To import from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="e3cbd-241">Azure Cosmos DB kaynak içeri Aktarıcı seçenek, bir veya daha fazla Azure Cosmos DB koleksiyonlarından verileri alır ve isteğe bağlı olarak bir sorgu kullanarak belgelere filtre olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-241">The Azure Cosmos DB source importer option allows you to import data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Azure Cosmos DB ekran kaynak seçenekleri](./media/import-data/documentdbsource.png)

<span data-ttu-id="e3cbd-243">Azure Cosmos DB bağlantı dizesi biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-243">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="e3cbd-244">Bölümünde açıklandığı gibi Azure portal'ın anahtarlar dikey penceresinden Azure Cosmos DB hesabı bağlantı dizesi alınabilir [Azure Cosmos DB hesabın nasıl yönetileceği](manage-account.md), veritabanının adını bağlantısı eklenmesi gerekiyor ancak dizesi şu biçimde:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-244">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="e3cbd-245">Bağlantı dizesi alanına belirtilen Azure Cosmos DB örneği erişilebildiğinden emin olmak için Doğrula komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-245">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="e3cbd-246">Tek bir Azure Cosmos DB koleksiyonundan almak için verileri içeri aktarılacak koleksiyonun adını girin.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-246">To import from a single Azure Cosmos DB collection, enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="e3cbd-247">Birden çok Azure Cosmos DB koleksiyonları içeri aktarmak için bir veya daha fazla koleksiyon adlarını eşleştirmek için normal bir ifade girin (örneğin collection01 | collection02 | collection03).</span><span class="sxs-lookup"><span data-stu-id="e3cbd-247">To import from multiple Azure Cosmos DB collections, provide a regular expression to match one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="e3cbd-248">İsteğe bağlı olarak belirtin veya bir dosya filtresi ve Şekil alınacak veri için bir sorgu için sağlayın.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-248">You may optionally specify, or provide a file for, a query to both filter and shape the data to be imported.</span></span>

> [!NOTE]
> <span data-ttu-id="e3cbd-249">Adında normal ifade karakterler içeren tek bir koleksiyondan alıyorsanız, normal ifadeler, koleksiyon alanın kabul olduğundan, ardından bu karakterleri uygun şekilde kaçış uygulanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-249">Since the collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="e3cbd-250">Aşağıdaki gelişmiş seçenekleri Azure Cosmos DB kaynak alma seçeneği vardır:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-250">The Azure Cosmos DB source importer option has the following advanced options:</span></span>

1. <span data-ttu-id="e3cbd-251">Dahili alanlar şunlardır: Azure Cosmos DB belge sistem özelliklerini dışa aktarma (örneğin, _rid, _ts) dahil gerekip gerekmediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-251">Include Internal Fields: Specifies whether or not to include Azure Cosmos DB document system properties in the export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="e3cbd-252">Hata yeniden deneme sayısı: Azure Cosmos DB bağlantısı geçici hataları (örneğin ağ bağlantı kesintisi) durumunda yeniden deneme sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-252">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="e3cbd-253">Yeniden deneme aralığı: nasıl geçici hataları (örneğin ağ bağlantı kesintisi) durumunda Azure Cosmos DB bağlantısı yeniden deneniyor arasında bekleneceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-253">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="e3cbd-254">Bağlantı modu: Azure Cosmos DB ile kullanmak için bağlantı modunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-254">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="e3cbd-255">Kullanılabilir seçenekler DirectTcp, DirectHttps ve ağ geçidi ' dir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-255">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="e3cbd-256">Doğrudan bağlantı modu yalnızca 443 numaralı bağlantı noktasını kullanır gibi ağ geçidi modu daha fazla güvenlik duvarı kolay olsa da, daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-256">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Gelişmiş Seçenekleri Azure Cosmos DB ekran kaynağı](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="e3cbd-258">İçeri aktarma aracını bağlantı modu DirectTcp varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-258">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="e3cbd-259">Güvenlik Duvarı sorunlarla karşılaşırsanız, yalnızca bir bağlantı noktası 443 gerektirdiği ağ geçidi bağlantı moduna geçer.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-259">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="e3cbd-260">Azure Cosmos DB'den almak için bazı komut satırı örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-260">Here are some command line samples to import from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection to another Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections to a single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection to a JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="e3cbd-261">Azure Cosmos DB verileri içe aktarma aracını ayrıca verilerini alma destekler [Azure Cosmos DB öykünücüsü](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="e3cbd-261">The Azure Cosmos DB Data Import Tool also supports import of data from the [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="e3cbd-262">Yerel bir öykünücüsünden verilerini içeri aktarırken, uç nokta kümesine `https://localhost:<port>`.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-262">When importing data from a local emulator, set the endpoint to `https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="e3cbd-263"><a id="HBaseSource"></a>HBase içeri aktarmak için</span><span class="sxs-lookup"><span data-stu-id="e3cbd-263"><a id="HBaseSource"></a>To import from HBase</span></span>
<span data-ttu-id="e3cbd-264">HBase kaynak alma seçeneği, bir HBase tablodan veri içeri aktarın ve isteğe bağlı olarak verileri filtrelemek sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-264">The HBase source importer option allows you to import data from an HBase table and optionally filter the data.</span></span> <span data-ttu-id="e3cbd-265">Alma ayarı kadar kolay böylece çeşitli şablonlar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Ekran görüntüsü, HBase kaynak seçenekleri](./media/import-data/hbasesource1.png)

![Ekran görüntüsü, HBase kaynak seçenekleri](./media/import-data/hbasesource2.png)

<span data-ttu-id="e3cbd-268">HBase Stargate bağlantı dizesinin biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-268">The format of the HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="e3cbd-269">Bağlantı dizesi alanına belirtilen HBase örneği erişilebildiğinden emin olmak için Doğrula komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-269">Use the Verify command to ensure that the HBase instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="e3cbd-270">HBase içeri aktarmak için bir komut satırı örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-270">Here is a command line sample to import from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="e3cbd-271"><a id="DocumentDBBulkTarget"></a>DocumentDB API'sine (toplu içeri aktarın) almak için</span><span class="sxs-lookup"><span data-stu-id="e3cbd-271"><a id="DocumentDBBulkTarget"></a>To import to the DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="e3cbd-272">Azure Cosmos DB toplu içeri Aktarıcı herhangi verimlilik için bir Azure Cosmos DB saklı yordamı kullanarak kullanılabilir kaynak seçeneklerinin almanıza izin verir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-272">The Azure Cosmos DB Bulk importer allows you to import from any of the available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="e3cbd-273">Aracı, tek tek bölümlenmiş Azure Cosmos DB koleksiyonuna alma yanı sıra, yapabildiği verileri birden çok tek bölümlenmiş Azure Cosmos DB koleksiyonlar genelinde bölümlenmiş parçalı alma destekler.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-273">The tool supports import to one single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="e3cbd-274">Veri bölümlendirme hakkında daha fazla bilgi için bkz: [bölümleme ve Azure Cosmos DB'de ölçeklendirme](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="e3cbd-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="e3cbd-275">Aracı oluşturmak, çalıştırmak ve saklı yordam hedef collection(s) silin.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-275">The tool will create, execute, and then delete the stored procedure from the target collection(s).</span></span>  

![Azure Cosmos DB ekran toplu seçenekleri](./media/import-data/documentdbbulk.png)

<span data-ttu-id="e3cbd-277">Azure Cosmos DB bağlantı dizesi biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-277">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="e3cbd-278">Bölümünde açıklandığı gibi Azure portal'ın anahtarlar dikey penceresinden Azure Cosmos DB hesabı bağlantı dizesi alınabilir [Azure Cosmos DB hesabın nasıl yönetileceği](manage-account.md), veritabanının adını bağlantısı eklenmesi gerekiyor ancak dizesi şu biçimde:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-278">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="e3cbd-279">Bağlantı dizesi alanına belirtilen Azure Cosmos DB örneği erişilebildiğinden emin olmak için Doğrula komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-279">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="e3cbd-280">Tek bir koleksiyon almak için verileri içeri aktarılır ve Ekle düğmesine basın koleksiyonun adını girin.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-280">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="e3cbd-281">Birden çok koleksiyonları içeri aktarmak için ayrı ayrı her koleksiyon adını girin veya birden çok koleksiyon belirtmek için aşağıdaki sözdizimini kullanın: *collection_prefix*[Başlangıç dizini - bitiş dizini].</span><span class="sxs-lookup"><span data-stu-id="e3cbd-281">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="e3cbd-282">Daha önce bahsedilen söz dizimi aracılığıyla birden çok koleksiyon belirtirken, aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-282">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="e3cbd-283">Yalnızca tamsayı aralığı adı desenleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="e3cbd-284">Toplama [0-3] belirtme aşağıdaki koleksiyonları örneğin oluşturur: Koleksiyon0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-284">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="e3cbd-285">Kısaltılmış sözdizimi kullanabilirsiniz: Koleksiyon [3], 1. adımda bahsedilen koleksiyonları aynı kümesini yayma.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="e3cbd-286">Birden fazla değiştirme sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-286">More than one substitution can be provided.</span></span> <span data-ttu-id="e3cbd-287">Örneğin, [0-1] [0-9] koleksiyonuna baştaki sıfırlarla 20 koleksiyon adları oluşturur (collection01,.. 02... 03).</span><span class="sxs-lookup"><span data-stu-id="e3cbd-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="e3cbd-288">Koleksiyon adları belirledikten sonra istenen üretimini collection(s) (10. 000'rus için 400 RUs) seçin.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-288">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 10,000 RUs).</span></span> <span data-ttu-id="e3cbd-289">En iyi alma performans için daha fazla üretilen işi seçin.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="e3cbd-290">Performans düzeyleri hakkında daha fazla bilgi için bkz: [Azure Cosmos veritabanı performans düzeyleri](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="e3cbd-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e3cbd-291">Performans verimlilik ayar yalnızca koleksiyon oluşturma için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-291">The performance throughput setting only applies to collection creation.</span></span> <span data-ttu-id="e3cbd-292">Belirtilen koleksiyon zaten varsa, üretilen iş değiştirilmeyecek.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-292">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="e3cbd-293">Birden çok koleksiyonuna içe aktarırken, içe aktarma aracını destekler karma parçalama temel.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-293">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="e3cbd-294">Bu senaryoda, bölüm anahtarı olarak kullanmak istediğiniz belgeyi özelliği belirtin (bölüm anahtarı boş bırakılırsa, belgeleri rastgele hedef koleksiyonlarındaki parçalı olacaktır).</span><span class="sxs-lookup"><span data-stu-id="e3cbd-294">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="e3cbd-295">İsteğe bağlı olarak, hangi alma kaynağı alanında (belgeleri bu özellik içermiyorsa, ardından içe aktarma aracını GUID kimliği özellik değeri olarak oluşturacağını unutmayın) alma sırasında Azure Cosmos DB belge kimliği özelliği olarak kullanılması gereken belirtebilir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-295">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="e3cbd-296">İçeri aktarma sırasında birkaç Gelişmiş Seçenekler yok.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="e3cbd-297">İlk olarak, Aracı'nı içerir ancak varsayılan toplu alma saklı yordam (BulkInsert.js), kendi depolanan içeri aktarma yordamı belirtmeyi seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-297">First, while the tool includes a default bulk import stored procedure (BulkInsert.js), you may choose to specify your own import stored procedure:</span></span>

 ![Azure Cosmos DB ekran bulk INSERT sproc seçeneği](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="e3cbd-299">Ayrıca, tarih türleri (örn. SQL Server veya MongoDB) alırken, üç alma seçenekler arasından seçim yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Azure Cosmos DB ekran tarih saat içeri aktarma seçenekleri](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="e3cbd-301">Dize: bir dize değeri olarak sürdürülemedi</span><span class="sxs-lookup"><span data-stu-id="e3cbd-301">String: Persist as a string value</span></span>
* <span data-ttu-id="e3cbd-302">Dönem: bir dönem sayı değeri kalır</span><span class="sxs-lookup"><span data-stu-id="e3cbd-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="e3cbd-303">Her ikisi: hem dize hem de dönem sayı değerlerini kalıcı olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="e3cbd-304">Bu seçenek bir alt örneğin oluşturur: "date_joined": {"Value": "2013-10-21T21:17:25.2410000Z", "dönem": 1382390245}</span><span class="sxs-lookup"><span data-stu-id="e3cbd-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="e3cbd-305">Azure Cosmos DB toplu içeri Aktarıcı Gelişmiş Seçenekler aşağıdaki ek sahiptir:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-305">The Azure Cosmos DB Bulk importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="e3cbd-306">Toplu iş boyutu: Aracı varsayılan olarak bir toplu iş boyutu 50.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-306">Batch Size: The tool defaults to a batch size of 50.</span></span>  <span data-ttu-id="e3cbd-307">İçeri aktarılacak belgeleri büyük toplu iş boyutunu azaltmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-307">If the documents to be imported are large, consider lowering the batch size.</span></span> <span data-ttu-id="e3cbd-308">İçeri aktarılacak belgeleri küçükse, buna karşılık, toplu iş boyutu yükseltme göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-308">Conversely, if the documents to be imported are small, consider raising the batch size.</span></span>
2. <span data-ttu-id="e3cbd-309">En fazla komut dosyası boyutu (bayt): aracı en fazla komut dosyası boyutunu 512 KB için varsayılanları</span><span class="sxs-lookup"><span data-stu-id="e3cbd-309">Max Script Size (bytes): The tool defaults to a max script size of 512KB</span></span>
3. <span data-ttu-id="e3cbd-310">Otomatik kimliği oluşturma devre dışı bırak: içeri aktarılacak her belgenin bir kimlik alanı içeriyorsa, bu seçeneğin belirlenmesi performansını artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-310">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="e3cbd-311">Benzersiz kimliği alanı eksik belgeleri içeri aktarılmayacak.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="e3cbd-312">Güncelleştirme mevcut belgeler: varolan belgeleri kimliği çakışmaları ile değiştirerek değil aracı varsayılanlarını.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-312">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="e3cbd-313">Bu seçeneğin kimlikleriyle eşleşen ile varolan belgeleri üzerine izin verir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="e3cbd-314">Bu özellik, varolan belgeleri güncelleştirme zamanlanan veri geçişler için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="e3cbd-315">Hata yeniden deneme sayısı: Azure Cosmos DB bağlantısı geçici hataları (örneğin ağ bağlantı kesintisi) durumunda yeniden deneme sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-315">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="e3cbd-316">Yeniden deneme aralığı: nasıl geçici hataları (örneğin ağ bağlantı kesintisi) durumunda Azure Cosmos DB bağlantısı yeniden deneniyor arasında bekleneceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-316">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="e3cbd-317">Bağlantı modu: Azure Cosmos DB ile kullanmak için bağlantı modunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-317">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="e3cbd-318">Kullanılabilir seçenekler DirectTcp, DirectHttps ve ağ geçidi ' dir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-318">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="e3cbd-319">Doğrudan bağlantı modu yalnızca 443 numaralı bağlantı noktasını kullanır gibi ağ geçidi modu daha fazla güvenlik duvarı kolay olsa da, daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-319">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Gelişmiş Seçenekleri Azure Cosmos DB ekran toplu içeri aktarma](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="e3cbd-321">İçeri aktarma aracını bağlantı modu DirectTcp varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-321">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="e3cbd-322">Güvenlik Duvarı sorunlarla karşılaşırsanız, yalnızca bir bağlantı noktası 443 gerektirdiği ağ geçidi bağlantı moduna geçer.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-322">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="e3cbd-323"><a id="DocumentDBSeqTarget"></a>DocumentDB API'sine (sıralı kayıt Al) almak için</span><span class="sxs-lookup"><span data-stu-id="e3cbd-323"><a id="DocumentDBSeqTarget"></a>To import to the DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="e3cbd-324">Azure Cosmos DB sıralı kayıt alma, kayıt kayıt temelinde kullanılabilir kaynak seçeneklerinden herhangi birini alınacak olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-324">The Azure Cosmos DB sequential record importer allows you to import from any of the available source options on a record by record basis.</span></span> <span data-ttu-id="e3cbd-325">Saklı yordamlar kotasına ulaştı varolan bir koleksiyona alıyorsanız bu seçeneği belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-325">You might choose this option if you’re importing to an existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="e3cbd-326">Aracı, verileri birden çok tek bölümlü ve/veya birden çok bölüm Azure Cosmos DB koleksiyonlar genelinde yapabildiği bölümlenmiş parçalı alma yanı sıra tek (tek bölüm ve birden çok bölüm) Azure Cosmos DB koleksiyona Al destekler.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-326">The tool supports import to a single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="e3cbd-327">Veri bölümlendirme hakkında daha fazla bilgi için bkz: [bölümleme ve Azure Cosmos DB'de ölçeklendirme](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="e3cbd-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Azure Cosmos DB ekran sıralı kayıt içeri aktarma seçenekleri](./media/import-data/documentdbsequential.png)

<span data-ttu-id="e3cbd-329">Azure Cosmos DB bağlantı dizesi biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-329">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="e3cbd-330">Bölümünde açıklandığı gibi Azure portal'ın anahtarlar dikey penceresinden Azure Cosmos DB hesabı bağlantı dizesi alınabilir [Azure Cosmos DB hesabın nasıl yönetileceği](manage-account.md), veritabanının adını bağlantısı eklenmesi gerekiyor ancak dizesi şu biçimde:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-330">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="e3cbd-331">Bağlantı dizesi alanına belirtilen Azure Cosmos DB örneği erişilebildiğinden emin olmak için Doğrula komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-331">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="e3cbd-332">Tek bir koleksiyon almak için verileri içeri aktarılır ve Ekle düğmesine basın koleksiyonun adını girin.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-332">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="e3cbd-333">Birden çok koleksiyonları içeri aktarmak için ayrı ayrı her koleksiyon adını girin veya birden çok koleksiyon belirtmek için aşağıdaki sözdizimini kullanın: *collection_prefix*[Başlangıç dizini - bitiş dizini].</span><span class="sxs-lookup"><span data-stu-id="e3cbd-333">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="e3cbd-334">Daha önce bahsedilen söz dizimi aracılığıyla birden çok koleksiyon belirtirken, aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-334">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="e3cbd-335">Yalnızca tamsayı aralığı adı desenleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="e3cbd-336">Toplama [0-3] belirtme aşağıdaki koleksiyonları örneğin oluşturur: Koleksiyon0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-336">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="e3cbd-337">Kısaltılmış sözdizimi kullanabilirsiniz: Koleksiyon [3], 1. adımda bahsedilen koleksiyonları aynı kümesini yayma.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="e3cbd-338">Birden fazla değiştirme sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-338">More than one substitution can be provided.</span></span> <span data-ttu-id="e3cbd-339">Örneğin, [0-1] [0-9] koleksiyonuna baştaki sıfırlarla 20 koleksiyon adları oluşturur (collection01,.. 02... 03).</span><span class="sxs-lookup"><span data-stu-id="e3cbd-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="e3cbd-340">Koleksiyon adları belirledikten sonra istenen üretimini collection(s) (250.000 RUs için 400 RUs) seçin.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-340">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 250,000 RUs).</span></span> <span data-ttu-id="e3cbd-341">En iyi alma performans için daha fazla üretilen işi seçin.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="e3cbd-342">Performans düzeyleri hakkında daha fazla bilgi için bkz: [Azure Cosmos veritabanı performans düzeyleri](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="e3cbd-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="e3cbd-343">Tüm alma işleme sahip koleksiyonları > 10.000 RUs bölüm anahtarı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-343">Any import to collections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="e3cbd-344">Birden fazla 250.000 RUs tercih ediyorsanız, artan, hesabınızın olması için portalında bir istek dosya gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-344">If you choose to have more than 250,000 RUs, you will need to file a request in the portal to have your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="e3cbd-345">Üretilen iş ayar yalnızca koleksiyon oluşturma için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-345">The throughput setting only applies to collection creation.</span></span> <span data-ttu-id="e3cbd-346">Belirtilen koleksiyon zaten varsa, üretilen iş değiştirilmeyecek.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-346">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="e3cbd-347">Birden çok koleksiyonuna içe aktarırken, içe aktarma aracını destekler karma parçalama temel.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-347">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="e3cbd-348">Bu senaryoda, bölüm anahtarı olarak kullanmak istediğiniz belgeyi özelliği belirtin (bölüm anahtarı boş bırakılırsa, belgeleri rastgele hedef koleksiyonlarındaki parçalı olacaktır).</span><span class="sxs-lookup"><span data-stu-id="e3cbd-348">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="e3cbd-349">İsteğe bağlı olarak, hangi alma kaynağı alanında (belgeleri bu özellik içermiyorsa, ardından içe aktarma aracını GUID kimliği özellik değeri olarak oluşturacağını unutmayın) alma sırasında Azure Cosmos DB belge kimliği özelliği olarak kullanılması gereken belirtebilir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-349">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="e3cbd-350">İçeri aktarma sırasında birkaç Gelişmiş Seçenekler yok.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="e3cbd-351">İlk olarak, tarih türleri (örn. SQL Server veya MongoDB) alırken, üç alma seçenekler arasından seçim yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Azure Cosmos DB ekran tarih saat içeri aktarma seçenekleri](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="e3cbd-353">Dize: bir dize değeri olarak sürdürülemedi</span><span class="sxs-lookup"><span data-stu-id="e3cbd-353">String: Persist as a string value</span></span>
* <span data-ttu-id="e3cbd-354">Dönem: bir dönem sayı değeri kalır</span><span class="sxs-lookup"><span data-stu-id="e3cbd-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="e3cbd-355">Her ikisi: hem dize hem de dönem sayı değerlerini kalıcı olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="e3cbd-356">Bu seçenek bir alt örneğin oluşturur: "date_joined": {"Value": "2013-10-21T21:17:25.2410000Z", "dönem": 1382390245}</span><span class="sxs-lookup"><span data-stu-id="e3cbd-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="e3cbd-357">Azure DB - Cosmos sıralı kayıt içeri Aktarıcı aşağıdaki ek gelişmiş seçenekler vardır:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-357">The Azure Cosmos DB - Sequential record importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="e3cbd-358">Paralel istek sayısı: aracı 2 paralel istekler için varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-358">Number of Parallel Requests: The tool defaults to 2 parallel requests.</span></span> <span data-ttu-id="e3cbd-359">İçeri aktarılacak belgeleri küçükse, paralel istek sayısı oluşturma göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-359">If the documents to be imported are small, consider raising the number of parallel requests.</span></span> <span data-ttu-id="e3cbd-360">Bu sayı çok fazla oluşursa alma azaltma karşılaşabilirsiniz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-360">Note that if this number is raised too much, the import may experience throttling.</span></span>
2. <span data-ttu-id="e3cbd-361">Otomatik kimliği oluşturma devre dışı bırak: içeri aktarılacak her belgenin bir kimlik alanı içeriyorsa, bu seçeneğin belirlenmesi performansını artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-361">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="e3cbd-362">Benzersiz kimliği alanı eksik belgeleri içeri aktarılmayacak.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="e3cbd-363">Güncelleştirme mevcut belgeler: varolan belgeleri kimliği çakışmaları ile değiştirerek değil aracı varsayılanlarını.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-363">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="e3cbd-364">Bu seçeneğin kimlikleriyle eşleşen ile varolan belgeleri üzerine izin verir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="e3cbd-365">Bu özellik, varolan belgeleri güncelleştirme zamanlanan veri geçişler için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="e3cbd-366">Hata yeniden deneme sayısı: Azure Cosmos DB bağlantısı geçici hataları (örneğin ağ bağlantı kesintisi) durumunda yeniden deneme sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-366">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="e3cbd-367">Yeniden deneme aralığı: nasıl geçici hataları (örneğin ağ bağlantı kesintisi) durumunda Azure Cosmos DB bağlantısı yeniden deneniyor arasında bekleneceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-367">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="e3cbd-368">Bağlantı modu: Azure Cosmos DB ile kullanmak için bağlantı modunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-368">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="e3cbd-369">Kullanılabilir seçenekler DirectTcp, DirectHttps ve ağ geçidi ' dir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-369">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="e3cbd-370">Doğrudan bağlantı modu yalnızca 443 numaralı bağlantı noktasını kullanır gibi ağ geçidi modu daha fazla güvenlik duvarı kolay olsa da, daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-370">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Gelişmiş Seçenekleri Azure Cosmos DB ekran sıralı kayıt alma](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="e3cbd-372">İçeri aktarma aracını bağlantı modu DirectTcp varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-372">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="e3cbd-373">Güvenlik Duvarı sorunlarla karşılaşırsanız, yalnızca bir bağlantı noktası 443 gerektirdiği ağ geçidi bağlantı moduna geçer.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-373">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="e3cbd-374"><a id="IndexingPolicy"></a>Azure Cosmos DB koleksiyonları oluştururken bir dizin oluşturma ilkesini belirtin</span><span class="sxs-lookup"><span data-stu-id="e3cbd-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="e3cbd-375">Koleksiyonları içeri aktarma sırasında oluşturmak geçiş aracı izin verdiğinizde, koleksiyon dizin oluşturma ilkesini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-375">When you allow the migration tool to create collections during import, you can specify the indexing policy of the collections.</span></span> <span data-ttu-id="e3cbd-376">Gelişmiş Seçenekler bölümünde Azure Cosmos DB sıralı kayıt seçenekleri ve Azure Cosmos DB toplu içeri dizin oluşturma ilkesi bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-376">In the advanced options section of the Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate to the Indexing Policy section.</span></span>

![Ekran Azure Cosmos DB dizin Gelişmiş Seçenekler ilke](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="e3cbd-378">Seçenek Gelişmiş dizin oluşturma İlkesi'ni kullanarak, bir dizin oluşturma ilke dosyası seçin, el ile bir dizin oluşturma ilkesi girin veya (varsayılan şablonları kümesinden sağ dizin oluşturma ilkesi metin kutusuna tıklayarak) seçin.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-378">Using the Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in the indexing policy textbox).</span></span>

<span data-ttu-id="e3cbd-379">Aracı sağlar ilke şablonları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-379">The policy templates the tool provides are:</span></span>

* <span data-ttu-id="e3cbd-380">Varsayılan.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-380">Default.</span></span> <span data-ttu-id="e3cbd-381">Dizeleri eşitlik sorguları gerçekleştirme ve sıralama, aralık ve eşitlik sorguları için numaraları kullanarak bu en iyi bir ilkedir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="e3cbd-382">Bu ilkeyi daha az dizin depolama yükü aralığından daha vardır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="e3cbd-383">Aralık.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-383">Range.</span></span> <span data-ttu-id="e3cbd-384">Bu ilke hem sayılara hem de dizeleri sıralama, aralık ve eşitlik sorguları kullanmakta olduğunuz en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="e3cbd-385">Bu ilke varsayılan veya karma daha yüksek bir dizin depolama yükü var.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Ekran Azure Cosmos DB dizin Gelişmiş Seçenekler ilke](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="e3cbd-387">Bir dizin oluşturma ilkesi belirtmezseniz, varsayılan ilke uygulanır.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-387">If you do not specify an indexing policy, then the default policy will be applied.</span></span> <span data-ttu-id="e3cbd-388">Dizin oluşturma ilkeleri hakkında daha fazla bilgi için bkz: [Azure Cosmos ilkeleri dizin DB](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="e3cbd-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-to-json-file"></a><span data-ttu-id="e3cbd-389">JSON dosyasına dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="e3cbd-389">Export to JSON file</span></span>
<span data-ttu-id="e3cbd-390">Azure Cosmos DB JSON dışarı aktarma, kullanılabilir kaynak seçeneklerinden herhangi birini bir dizi JSON belgeleri içeren bir JSON dosyası vermenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-390">The Azure Cosmos DB JSON exporter allows you to export any of the available source options to a JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="e3cbd-391">Aracı, verme işleyecek veya ortaya çıkan geçiş komut görüntülemek ve kendiniz komutu çalıştırmak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-391">The tool will handle the export for you, or you can choose to view the resulting migration command and run the command yourself.</span></span> <span data-ttu-id="e3cbd-392">Sonuçta elde edilen JSON dosyasını yerel olarak veya Azure Blob Depolama alanında depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-392">The resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Ekran Azure Cosmos DB JSON yerel dosya dışa aktarma seçeneği](./media/import-data/jsontarget.png)

![Azure Cosmos DB JSON Azure Blob'ın ekran depolama dışa aktarma seçeneği](./media/import-data/jsontarget2.png)

<span data-ttu-id="e3cbd-395">İsteğe bağlı olarak daha fazla içeriği yaparken sonuç belgesi boyutunu artıracaktır elde edilen JSON prettify seçebileceği okunabilir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-395">You may optionally choose to prettify the resulting JSON, which will increase the size of the resulting document while making the contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places to see in Paris"}]}]

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
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places to see in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a><span data-ttu-id="e3cbd-396">Gelişmiş yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e3cbd-396">Advanced configuration</span></span>
<span data-ttu-id="e3cbd-397">Gelişmiş yapılandırma ekranında yazılmış hataları istediğiniz günlük dosyasının konumunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-397">In the Advanced configuration screen, specify the location of the log file to which you would like any errors written.</span></span> <span data-ttu-id="e3cbd-398">Bu sayfa aşağıdaki kurallar geçerli olur:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-398">The following rules apply to this page:</span></span>

1. <span data-ttu-id="e3cbd-399">Bir dosya adı sağlanmazsa, tüm hataları sonuçları sayfasında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-399">If a file name is not provided, then all errors will be returned on the Results page.</span></span>
2. <span data-ttu-id="e3cbd-400">Bir dosya adı olmadan bir dizin sağlanırsa, ardından dosyayı oluşturulan (üzerine geçerli ortam dizinde veya).</span><span class="sxs-lookup"><span data-stu-id="e3cbd-400">If a file name is provided without a directory, then the file will be created (or overwritten) in the current environment directory.</span></span>
3. <span data-ttu-id="e3cbd-401">Var olan belirlerseniz dosyası sonra dosyanın üzerine yazılır, ek bir seçenek yoktur.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-401">If you select an existing file, then the file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="e3cbd-402">Ardından, tüm, günlük isteyip istemediğinizi seçin kritik veya herhangi bir hata iletisi.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-402">Then, choose whether to log all, critical, or no error messages.</span></span> <span data-ttu-id="e3cbd-403">Son olarak, ne sıklıkta üzerinde ekran aktarımı ileti ile ilerleme durumunu güncelleştirilecek karar verin.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-403">Finally, decide how frequently the on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="e3cbd-404">Ayarları içeri aktarma ve görünüm komut satırında onaylayın</span><span class="sxs-lookup"><span data-stu-id="e3cbd-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="e3cbd-405">Kaynak bilgileri, hedef bilgileri ve Gelişmiş Yapılandırma belirtme sonra geçiş özeti gözden geçirin ve isteğe bağlı olarak, görünüm/kopyalama ortaya çıkan geçiş komut (komutu kopyalama, içeri aktarma işlemlerini otomatikleştirmek yararlıdır):</span><span class="sxs-lookup"><span data-stu-id="e3cbd-405">After specifying source information, target information, and advanced configuration, review the migration summary and, optionally, view/copy the resulting migration command (copying the command is useful to automate import operations):</span></span>
   
    ![Özet ekranının ekran görüntüsü](./media/import-data/summary.png)
   
    ![Özet ekranının ekran görüntüsü](./media/import-data/summarycommand.png)
2. <span data-ttu-id="e3cbd-408">Kaynak ve hedef seçeneklerle memnun kaldıktan sonra tıklatın **alma**.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="e3cbd-409">İçeri aktarma sürecinde olduğundan geçen süre, aktarılan sayısını ve (Gelişmiş Yapılandırma bir dosya adı kaydetmedi sağlarsanız) hata bilgileri güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-409">The elapsed time, transferred count, and failure information (if you didn't provide a file name in the Advanced configuration) will update as the import is in process.</span></span> <span data-ttu-id="e3cbd-410">Tamamlandıktan sonra sonuçları verebilirsiniz (örneğin tüm alma hataları ile mücadele etmek için).</span><span class="sxs-lookup"><span data-stu-id="e3cbd-410">Once complete, you can export the results (e.g. to deal with any import failures).</span></span>
   
    ![Ekran Azure Cosmos DB JSON dışa aktarma seçeneği](./media/import-data/viewresults.png)
3. <span data-ttu-id="e3cbd-412">Yeni bir içeri aktarma (ör. bağlantı dizesi bilgilerini, kaynak ve hedef seçimi, vb.) var olan ayarları tutma ya da tüm değerleri sıfırlama da başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-412">You may also start a new import, either keeping the existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Ekran Azure Cosmos DB JSON dışa aktarma seçeneği](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="e3cbd-414">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e3cbd-414">Next steps</span></span>

<span data-ttu-id="e3cbd-415">Bu öğreticide, aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="e3cbd-415">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e3cbd-416">Veri Geçiş Aracı yüklü</span><span class="sxs-lookup"><span data-stu-id="e3cbd-416">Installed the Data Migration tool</span></span>
> * <span data-ttu-id="e3cbd-417">Farklı veri kaynaklarından alınan verileri</span><span class="sxs-lookup"><span data-stu-id="e3cbd-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="e3cbd-418">JSON olarak Azure Cosmos DB dışarı</span><span class="sxs-lookup"><span data-stu-id="e3cbd-418">Exported from Azure Cosmos DB to JSON</span></span>

<span data-ttu-id="e3cbd-419">Şimdi, sonraki öğretici devam etmek ve Azure Cosmos DB kullanarak verileri sorgulamak öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e3cbd-419">You can now proceed to the next tutorial and learn how to query data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="e3cbd-420">Sorgu verileri nasıl?</span><span class="sxs-lookup"><span data-stu-id="e3cbd-420">How to query data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
