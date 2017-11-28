---
title: / Azure Cosmos DB aaaMove verileri | Microsoft Docs
description: "Bilgi nasıl veri taşıma/Azure Data Factory kullanarak Azure Cosmos DB koleksiyonundan"
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="59193-103">Azure Cosmos Azure Data Factory kullanarak Veritabanından veri tooand Taşı</span><span class="sxs-lookup"><span data-stu-id="59193-103">Move data tooand from Azure Cosmos DB using Azure Data Factory</span></span>
<span data-ttu-id="59193-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri öğesine/öğesinden Azure Cosmos DB (DocumentDB API) açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="59193-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Cosmos DB (DocumentDB API).</span></span> <span data-ttu-id="59193-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="59193-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="59193-106">Veri tooAzure Cosmos DB depolamak veya Azure Cosmos DB desteklenen tooany havuz verileri depolamak istediğiniz desteklenen kaynağından veri kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59193-106">You can copy data from any supported source data store tooAzure Cosmos DB or from Azure Cosmos DB tooany supported sink data store.</span></span> <span data-ttu-id="59193-107">Merhaba kaynakları veya havuzlarını olarak hello kopyalama etkinliği tarafından desteklenen veri depoları listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="59193-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="59193-108">Azure Cosmos DB Bağlayıcısı yalnızca DocumentDB API destekler.</span><span class="sxs-lookup"><span data-stu-id="59193-108">Azure Cosmos DB connector only support DocumentDB API.</span></span>

<span data-ttu-id="59193-109">toocopy verileri olarak-olduğu için/JSON dosyalarında veya başka bir Cosmos DB koleksiyonu bkz [içeri/dışarı aktarma JSON belgeleri](#importexport-json-documents).</span><span class="sxs-lookup"><span data-stu-id="59193-109">toocopy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="59193-110">Başlarken</span><span class="sxs-lookup"><span data-stu-id="59193-110">Getting started</span></span>
<span data-ttu-id="59193-111">Farklı araçlar/API'lerini kullanarak verileri öğesine/öğesinden Azure Cosmos DB taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="59193-111">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="59193-112">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="59193-112">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="59193-113">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="59193-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="59193-114">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="59193-114">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="59193-115">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="59193-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="59193-116">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="59193-116">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="59193-117">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="59193-117">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="59193-118">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="59193-118">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="59193-119">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="59193-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="59193-120">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="59193-120">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="59193-121">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="59193-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="59193-122">/ Cosmos DB kullanılan toocopy verileri olan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="59193-122">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="59193-123">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooCosmos DB olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="59193-123">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooCosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="59193-124">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="59193-124">Linked service properties</span></span>
<span data-ttu-id="59193-125">Aşağıdaki tablonun hello JSON öğeleri belirli tooAzure Cosmos DB bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="59193-125">hello following table provides description for JSON elements specific tooAzure Cosmos DB linked service.</span></span>

| <span data-ttu-id="59193-126">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="59193-126">**Property**</span></span> | <span data-ttu-id="59193-127">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="59193-127">**Description**</span></span> | <span data-ttu-id="59193-128">**Gerekli**</span><span class="sxs-lookup"><span data-stu-id="59193-128">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="59193-129">type</span><span class="sxs-lookup"><span data-stu-id="59193-129">type</span></span> |<span data-ttu-id="59193-130">Merhaba type özelliği ayarlanmalıdır: **DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="59193-130">hello type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="59193-131">Evet</span><span class="sxs-lookup"><span data-stu-id="59193-131">Yes</span></span> |
| <span data-ttu-id="59193-132">connectionString</span><span class="sxs-lookup"><span data-stu-id="59193-132">connectionString</span></span> |<span data-ttu-id="59193-133">Gerekli bilgiler tooconnect tooAzure Cosmos DB veritabanı belirtin.</span><span class="sxs-lookup"><span data-stu-id="59193-133">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="59193-134">Evet</span><span class="sxs-lookup"><span data-stu-id="59193-134">Yes</span></span> |

<span data-ttu-id="59193-135">Örnek:</span><span class="sxs-lookup"><span data-stu-id="59193-135">Example:</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="59193-136">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="59193-136">Dataset properties</span></span>
<span data-ttu-id="59193-137">Bölümler & özellikleri veri kümeleri tanımlamak için kullanılabilir tam bir listesi için lütfen toohello bakın [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="59193-137">For a full list of sections & properties available for defining datasets please refer toohello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="59193-138">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="59193-138">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="59193-139">Merhaba typeProperties bölümü veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="59193-139">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="59193-140">Merhaba typeProperties bölüm türü hello veri kümesi için **DocumentDbCollection** hello aşağıdaki özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="59193-140">hello typeProperties section for hello dataset of type **DocumentDbCollection** has hello following properties.</span></span>

| <span data-ttu-id="59193-141">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="59193-141">**Property**</span></span> | <span data-ttu-id="59193-142">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="59193-142">**Description**</span></span> | <span data-ttu-id="59193-143">**Gerekli**</span><span class="sxs-lookup"><span data-stu-id="59193-143">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="59193-144">collectionName</span><span class="sxs-lookup"><span data-stu-id="59193-144">collectionName</span></span> |<span data-ttu-id="59193-145">Merhaba Cosmos DB belge koleksiyonu adı.</span><span class="sxs-lookup"><span data-stu-id="59193-145">Name of hello Cosmos DB document collection.</span></span> |<span data-ttu-id="59193-146">Evet</span><span class="sxs-lookup"><span data-stu-id="59193-146">Yes</span></span> |

<span data-ttu-id="59193-147">Örnek:</span><span class="sxs-lookup"><span data-stu-id="59193-147">Example:</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a><span data-ttu-id="59193-148">Şema tarafından veri fabrikası</span><span class="sxs-lookup"><span data-stu-id="59193-148">Schema by Data Factory</span></span>
<span data-ttu-id="59193-149">Azure Cosmos DB gibi şemasız veri depoları için hello Data Factory hizmetinin yolları aşağıdaki hello birinde hello şema oluşturur:</span><span class="sxs-lookup"><span data-stu-id="59193-149">For schema-free data stores such as Azure Cosmos DB, hello Data Factory service infers hello schema in one of hello following ways:</span></span>  

1. <span data-ttu-id="59193-150">Hello kullanarak verilerin hello yapısını belirtirseniz **yapısı** hello veri kümesi tanımında hello Data Factory hizmeti özelliği bu yapısı hello şema olarak geliştirir.</span><span class="sxs-lookup"><span data-stu-id="59193-150">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="59193-151">Bir satır bir sütun için bir değer içermiyorsa, bu durumda, boş bir değer için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="59193-151">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="59193-152">Hello kullanarak verilerin hello yapısını belirtmezseniz, **yapısı** hello veri kümesi tanımında hello Data Factory hizmeti özellik hello verilerde hello ilk satırını kullanarak hello şema oluşturur.</span><span class="sxs-lookup"><span data-stu-id="59193-152">If you do not specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="59193-153">Merhaba ilk satır hello tam şema içermiyorsa, bu durumda, bazı sütunları hello kopyalama işlemi sonucunda eksilir.</span><span class="sxs-lookup"><span data-stu-id="59193-153">In this case, if hello first row does not contain hello full schema, some columns will be missing in hello result of copy operation.</span></span>

<span data-ttu-id="59193-154">Bu nedenle, şemasız veri kaynakları için hello en iyi uygulama toospecify hello hello kullanarak veri yapısıdır **yapısı** özelliği.</span><span class="sxs-lookup"><span data-stu-id="59193-154">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="59193-155">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="59193-155">Copy activity properties</span></span>
<span data-ttu-id="59193-156">Bölümler & özellikleri etkinlikleri tanımlamak için kullanılabilir tam bir listesi için lütfen toohello bakın [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="59193-156">For a full list of sections & properties available for defining activities please refer toohello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="59193-157">Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="59193-157">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="59193-158">Merhaba kopyalama etkinliği yalnızca bir girdi alır ve tek bir çıktı üretir.</span><span class="sxs-lookup"><span data-stu-id="59193-158">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="59193-159">Özellikler hello hello faaliyete hello typeProperties bölümünde kullanılabilir diğer yandan farklılık hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık kopyalama etkinliği durumunda her etkinlik türü ile.</span><span class="sxs-lookup"><span data-stu-id="59193-159">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type and in case of Copy activity they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="59193-160">Kaynak türü olduğunda kopyalama etkinliği durumunda **DocumentDbCollectionSource** aşağıdaki özelliklere hello kullanılabilir **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="59193-160">In case of Copy activity when source is of type **DocumentDbCollectionSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="59193-161">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="59193-161">**Property**</span></span> | <span data-ttu-id="59193-162">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="59193-162">**Description**</span></span> | <span data-ttu-id="59193-163">**İzin verilen değerler**</span><span class="sxs-lookup"><span data-stu-id="59193-163">**Allowed values**</span></span> | <span data-ttu-id="59193-164">**Gerekli**</span><span class="sxs-lookup"><span data-stu-id="59193-164">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="59193-165">sorgu</span><span class="sxs-lookup"><span data-stu-id="59193-165">query</span></span> |<span data-ttu-id="59193-166">Merhaba sorgu tooread verileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="59193-166">Specify hello query tooread data.</span></span> |<span data-ttu-id="59193-167">Sorgu dizesindeki Azure Cosmos DB tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="59193-167">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="59193-168">Örnek:`SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="59193-168">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="59193-169">Hayır</span><span class="sxs-lookup"><span data-stu-id="59193-169">No</span></span> <br/><br/><span data-ttu-id="59193-170">Belirtilmezse, yürütülen SQL deyimini hello:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="59193-170">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="59193-171">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="59193-171">nestingSeparator</span></span> |<span data-ttu-id="59193-172">Belge hello özel karakter tooindicate iç içe geçmiş</span><span class="sxs-lookup"><span data-stu-id="59193-172">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="59193-173">Herhangi bir karakter.</span><span class="sxs-lookup"><span data-stu-id="59193-173">Any character.</span></span> <br/><br/><span data-ttu-id="59193-174">Azure Cosmos DB iç içe geçmiş yapılar burada izin verilen bir NoSQL JSON belgeleri için deposudur.</span><span class="sxs-lookup"><span data-stu-id="59193-174">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="59193-175">Azure Data Factory sağlayan kullanıcı toodenote hiyerarşisi olan nestingSeparator aracılığıyla "."</span><span class="sxs-lookup"><span data-stu-id="59193-175">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="59193-176">Yukarıdaki örneklerde Hello.</span><span class="sxs-lookup"><span data-stu-id="59193-176">in hello above examples.</span></span> <span data-ttu-id="59193-177">Merhaba ayırıcı ile üç alt öğeleri olan hello "Ad" nesne hello kopyalama etkinliği oluşturacaktır ilk, Orta ve son, according too"Name.First", "Name.Middle" ve "Name.Last" hello, tablo tanımı.</span><span class="sxs-lookup"><span data-stu-id="59193-177">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="59193-178">Hayır</span><span class="sxs-lookup"><span data-stu-id="59193-178">No</span></span> |

<span data-ttu-id="59193-179">**DocumentDbCollectionSink** aşağıdaki özelliklere hello destekler:</span><span class="sxs-lookup"><span data-stu-id="59193-179">**DocumentDbCollectionSink** supports hello following properties:</span></span>

| <span data-ttu-id="59193-180">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="59193-180">**Property**</span></span> | <span data-ttu-id="59193-181">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="59193-181">**Description**</span></span> | <span data-ttu-id="59193-182">**İzin verilen değerler**</span><span class="sxs-lookup"><span data-stu-id="59193-182">**Allowed values**</span></span> | <span data-ttu-id="59193-183">**Gerekli**</span><span class="sxs-lookup"><span data-stu-id="59193-183">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="59193-184">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="59193-184">nestingSeparator</span></span> |<span data-ttu-id="59193-185">Bir özel karakter belge iç içe geçmiş hello kaynak sütun adı tooindicate gereklidir.</span><span class="sxs-lookup"><span data-stu-id="59193-185">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="59193-186">Örneğin yukarıdaki: `Name.First` hello çıktısında JSON yapısındaki hello Cosmos DB belgede aşağıdaki hello tablo oluşturur:</span><span class="sxs-lookup"><span data-stu-id="59193-186">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="59193-187">"Name": {</span><span class="sxs-lookup"><span data-stu-id="59193-187">"Name": {</span></span><br/>    <span data-ttu-id="59193-188">"İlk": "John"</span><span class="sxs-lookup"><span data-stu-id="59193-188">"First": "John"</span></span><br/><span data-ttu-id="59193-189">},</span><span class="sxs-lookup"><span data-stu-id="59193-189">},</span></span> |<span data-ttu-id="59193-190">Kullanılan tooseparate iç içe geçme düzeyi karakter.</span><span class="sxs-lookup"><span data-stu-id="59193-190">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="59193-191">Varsayılan değer `.` (nokta).</span><span class="sxs-lookup"><span data-stu-id="59193-191">Default value is `.` (dot).</span></span> |<span data-ttu-id="59193-192">Kullanılan tooseparate iç içe geçme düzeyi karakter.</span><span class="sxs-lookup"><span data-stu-id="59193-192">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="59193-193">Varsayılan değer `.` (nokta).</span><span class="sxs-lookup"><span data-stu-id="59193-193">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="59193-194">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="59193-194">writeBatchSize</span></span> |<span data-ttu-id="59193-195">TooAzure Cosmos DB hizmet toocreate belgeleri istekleri paralel sayısı.</span><span class="sxs-lookup"><span data-stu-id="59193-195">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="59193-196">Bu özelliği kullanarak verileri için/Cosmos DB kopyalama işlemi sırasında hello performans ince ayar yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59193-196">You can fine-tune hello performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="59193-197">Daha fazla paralel istekler tooCosmos DB gönderildiğinden writeBatchSize artırdığınızda daha iyi bir performans düşüklüğü görebilir.</span><span class="sxs-lookup"><span data-stu-id="59193-197">You can expect a better performance when you increase writeBatchSize because more parallel requests tooCosmos DB are sent.</span></span> <span data-ttu-id="59193-198">Ancak, azaltma tooavoid gerekir hello hata iletisi atabilirsiniz: "oranıdır büyük istek".</span><span class="sxs-lookup"><span data-stu-id="59193-198">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="59193-199">Azaltmayı bir dizi etkene, belgeler, belgeleri koşullarını sayısı boyutunu dahil olmak üzere, hedef koleksiyon, vb. İlkesi dizin tarafından belirlenir. Kopyalama işlemleri için daha iyi bir koleksiyon (ör S3) toohave hello çoğu üretilen iş kullanabilirsiniz (2.500 istek birimleri/saniye).</span><span class="sxs-lookup"><span data-stu-id="59193-199">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="59193-200">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="59193-200">Integer</span></span> |<span data-ttu-id="59193-201">Hayır (varsayılan: 5)</span><span class="sxs-lookup"><span data-stu-id="59193-201">No (default: 5)</span></span> |
| <span data-ttu-id="59193-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="59193-202">writeBatchTimeout</span></span> |<span data-ttu-id="59193-203">Zaman aşımına uğramadan önce hello işlemi toocomplete bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="59193-203">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="59193-204">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="59193-204">timespan</span></span><br/><br/> <span data-ttu-id="59193-205">Örnek: "00: 30:00" (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="59193-205">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="59193-206">Hayır</span><span class="sxs-lookup"><span data-stu-id="59193-206">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="59193-207">İçeri/dışarı aktarma JSON belgeleri</span><span class="sxs-lookup"><span data-stu-id="59193-207">Import/Export JSON documents</span></span>
<span data-ttu-id="59193-208">Bu Cosmos DB Bağlayıcısı'nı kullanarak kolayca yapabilecekleriniz</span><span class="sxs-lookup"><span data-stu-id="59193-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="59193-209">JSON belgeleri Cosmos DB, Azure Blob, Azure Data Lake, şirket içi dosya sistemi veya Azure Data Factory ile desteklenen diğer dosya tabanlı depoları gibi çeşitli kaynaklardan aktarın.</span><span class="sxs-lookup"><span data-stu-id="59193-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="59193-210">JSON belgeleri Cosmos DB collecton çeşitli dosya tabanlı depoları verin.</span><span class="sxs-lookup"><span data-stu-id="59193-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="59193-211">İki Cosmos DB koleksiyon olarak arasında veri geçirme-değil.</span><span class="sxs-lookup"><span data-stu-id="59193-211">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="59193-212">Bu tür şema belirsiz tooachieve kopyalama</span><span class="sxs-lookup"><span data-stu-id="59193-212">tooachieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="59193-213">Kopyalama Sihirbazı'nı kullanırken hello denetleyin **"dışa-tooJSON dosyaları ya da Cosmos DB koleksiyonu"** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="59193-213">When using copy wizard, check hello **"Export as-is tooJSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="59193-214">Ne zaman, JSON düzenleme kullanarak belirlemezseniz hello "yapısı" bölümü Cosmos DB veri kümeleri içinde ya da "nestingSeparator" özelliği Cosmos DB kaynak/havuz kopyalama etkinliği.</span><span class="sxs-lookup"><span data-stu-id="59193-214">When using JSON editing, do not specify hello "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="59193-215">gelen tooimport / tooJSON dosyaları dışarı aktarma, hello dosya depolama kümesinde "JsonFormat", yapılandırma "filePattern" biçim türünü belirtin ve hello rest biçim ayarlarını Atla bkz [JSON biçimine](data-factory-supported-file-and-compression-formats.md#json-format) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="59193-215">tooimport from/export tooJSON files, in hello file store dataset specify format type as "JsonFormat", config "filePattern" and skip hello rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="59193-216">JSON örnekleri</span><span class="sxs-lookup"><span data-stu-id="59193-216">JSON examples</span></span>
<span data-ttu-id="59193-217">Merhaba aşağıdaki örneklerde sağlayan örnek JSON tanımları toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="59193-217">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="59193-218">Bunlar Göster nasıl toocopy veri tooand Azure Cosmos DB ve Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="59193-218">They show how toocopy data tooand from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="59193-219">Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden hello kaynakları tooany belirtildiği hello havuzlarını, [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="59193-219">However, data can be copied **directly** from any of hello sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a><span data-ttu-id="59193-220">Örnek: Verilerini Azure Cosmos DB tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="59193-220">Example: Copy data from Azure Cosmos DB tooAzure Blob</span></span>
<span data-ttu-id="59193-221">Aşağıdaki Hello örneği gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="59193-221">hello sample below shows:</span></span>

1. <span data-ttu-id="59193-222">Bağlı hizmet türü [DocumentDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="59193-222">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="59193-223">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="59193-223">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="59193-224">Bir giriş [dataset](data-factory-create-datasets.md) türü [DocumentDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="59193-224">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="59193-225">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="59193-225">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="59193-226">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [DocumentDbCollectionSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="59193-226">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="59193-227">Merhaba örnek verileri Azure Cosmos DB tooAzure Blob kopyalar.</span><span class="sxs-lookup"><span data-stu-id="59193-227">hello sample copies data in Azure Cosmos DB tooAzure Blob.</span></span> <span data-ttu-id="59193-228">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="59193-228">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="59193-229">**Azure Cosmos bağlı DB hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="59193-229">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="59193-230">**Azure Blob storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="59193-230">**Azure Blob storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="59193-231">**Azure belge DB girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="59193-231">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="59193-232">Merhaba örnek varsayar adlı bir koleksiyon sahip **kişi** Azure Cosmos DB veritabanında.</span><span class="sxs-lookup"><span data-stu-id="59193-232">hello sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="59193-233">"Dış" ayarı: "true" ve externalData belirtme hello Azure Data Factory hizmeti hello tablosunun ilkesi bilgileri dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="59193-233">Setting “external”: ”true” and specifying externalData policy information hello Azure Data Factory service that hello table is external toohello data factory and not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="59193-234">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="59193-234">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="59193-235">Kopyalanan tooa yeni blob hello yoluyla her saat için saat ayrıntı hello belirli datetime yansıtma hello blob verilerdir.</span><span class="sxs-lookup"><span data-stu-id="59193-235">Data is copied tooa new blob every hour with hello path for hello blob reflecting hello specific datetime with hour granularity.</span></span>

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="59193-236">JSON belgesinde hello Cosmos DB veritabanı kişi koleksiyonunda örnek:</span><span class="sxs-lookup"><span data-stu-id="59193-236">Sample JSON document in hello Person collection in a Cosmos DB database:</span></span>

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
<span data-ttu-id="59193-237">Cosmos DB SQL söz dizimi gibi hiyerarşik JSON belgelerini kullanarak belgelerin sorgulanmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="59193-237">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="59193-238">Örnek:</span><span class="sxs-lookup"><span data-stu-id="59193-238">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="59193-239">Merhaba aşağıdaki hello hello Azure Cosmos DB veritabanı tooan Azure blob kişi koleksiyonunda kopya veri kanalı.</span><span class="sxs-lookup"><span data-stu-id="59193-239">hello following pipeline copies data from hello Person collection in hello Azure Cosmos DB database tooan Azure blob.</span></span> <span data-ttu-id="59193-240">Merhaba kopyalama etkinliği hello bir parçası olarak giriş ve çıkış veri kümeleri belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="59193-240">As part of hello copy activity hello input and output datasets have been specified.</span></span>  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a><span data-ttu-id="59193-241">Örnek: Kopyalama verileri Azure Blob tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="59193-241">Example: Copy data from Azure Blob tooAzure Cosmos DB</span></span> 
<span data-ttu-id="59193-242">Aşağıdaki Hello örneği gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="59193-242">hello sample below shows:</span></span>

1. <span data-ttu-id="59193-243">Bağlı hizmet türü [DocumentDb](#azure-documentdb-linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="59193-243">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="59193-244">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="59193-244">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="59193-245">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="59193-245">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="59193-246">Bir çıkış [dataset](data-factory-create-datasets.md) türü [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span><span class="sxs-lookup"><span data-stu-id="59193-246">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="59193-247">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) ve [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="59193-247">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="59193-248">Merhaba örnek verileri Azure blob tooAzure Cosmos DB kopyalar.</span><span class="sxs-lookup"><span data-stu-id="59193-248">hello sample copies data from Azure blob tooAzure Cosmos DB.</span></span> <span data-ttu-id="59193-249">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="59193-249">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="59193-250">**Azure Blob storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="59193-250">**Azure Blob storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="59193-251">**Azure Cosmos bağlı DB hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="59193-251">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="59193-252">**Azure Blob girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="59193-252">**Azure Blob input dataset:**</span></span>

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="59193-253">**Azure Cosmos DB çıkış dataset:**</span><span class="sxs-lookup"><span data-stu-id="59193-253">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="59193-254">Merhaba örnek "Kişi" adlı veri tooa koleksiyon kopyalar.</span><span class="sxs-lookup"><span data-stu-id="59193-254">hello sample copies data tooa collection named “Person”.</span></span>

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="59193-255">Merhaba aşağıdaki kopya verileri Azure Blob toohello kişi hello Cosmos DB koleksiyonunda kanalı.</span><span class="sxs-lookup"><span data-stu-id="59193-255">hello following pipeline copies data from Azure Blob toohello Person collection in hello Cosmos DB.</span></span> <span data-ttu-id="59193-256">Merhaba kopyalama etkinliği hello bir parçası olarak giriş ve çıkış veri kümeleri belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="59193-256">As part of hello copy activity hello input and output datasets have been specified.</span></span>

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
<span data-ttu-id="59193-257">Merhaba örnek blob giriş olarak ise</span><span class="sxs-lookup"><span data-stu-id="59193-257">If hello sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="59193-258">Ardından hello çıktı Cosmos DB'de JSON olarak olacaktır:</span><span class="sxs-lookup"><span data-stu-id="59193-258">Then hello output JSON in Cosmos DB will be as:</span></span>

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
<span data-ttu-id="59193-259">Azure Cosmos DB iç içe geçmiş yapılar burada izin verilen bir NoSQL JSON belgeleri için deposudur.</span><span class="sxs-lookup"><span data-stu-id="59193-259">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="59193-260">Azure Data Factory sağlayan kullanıcı toodenote hiyerarşisi aracılığıyla **nestingSeparator**, olduğu "."</span><span class="sxs-lookup"><span data-stu-id="59193-260">Azure Data Factory enables user toodenote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="59193-261">Bu örnekte.</span><span class="sxs-lookup"><span data-stu-id="59193-261">in this example.</span></span> <span data-ttu-id="59193-262">Merhaba ayırıcı ile üç alt öğeleri olan hello "Ad" nesne hello kopyalama etkinliği oluşturacaktır ilk, Orta ve son, according too"Name.First", "Name.Middle" ve "Name.Last" hello, tablo tanımı.</span><span class="sxs-lookup"><span data-stu-id="59193-262">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="59193-263">Ek</span><span class="sxs-lookup"><span data-stu-id="59193-263">Appendix</span></span>
1. <span data-ttu-id="59193-264">**Soru:** kopyalama etkinliği desteği güncelleştirmesi mevcut kayıtların hello?</span><span class="sxs-lookup"><span data-stu-id="59193-264">**Question:** Does hello Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="59193-265">**Yanıt:** No</span><span class="sxs-lookup"><span data-stu-id="59193-265">**Answer:** No.</span></span>
2. <span data-ttu-id="59193-266">**Soru:** kayıtları kopyalanan nasıl bir kopya tooAzure Cosmos DB anlaşma ile yeniden denemek zaten mu?</span><span class="sxs-lookup"><span data-stu-id="59193-266">**Question:** How does a retry of a copy tooAzure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="59193-267">**Yanıt:** kayıtları "ID" alanına sahipseniz ve hello kopyalama işlemi çalışırsa tooinsert hello bir kayıtla aynı kimliği, başlangıç kopyalama işlemi bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="59193-267">**Answer:** If records have an "ID" field and hello copy operation tries tooinsert a record with hello same ID, hello copy operation throws an error.</span></span>  
3. <span data-ttu-id="59193-268">**Soru:** Data Factory desteklemiyor [aralığı veya karma tabanlı veri bölümlendirme](../documentdb/documentdb-partition-data.md)?</span><span class="sxs-lookup"><span data-stu-id="59193-268">**Question:** Does Data Factory support [range or hash-based data partitioning](../documentdb/documentdb-partition-data.md)?</span></span>

    <span data-ttu-id="59193-269">**Yanıt:** No</span><span class="sxs-lookup"><span data-stu-id="59193-269">**Answer:** No.</span></span>
4. <span data-ttu-id="59193-270">**Soru:** bir tablo için birden fazla Azure Cosmos DB koleksiyonu belirtin?</span><span class="sxs-lookup"><span data-stu-id="59193-270">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="59193-271">**Yanıt:** No</span><span class="sxs-lookup"><span data-stu-id="59193-271">**Answer:** No.</span></span> <span data-ttu-id="59193-272">Şu anda yalnızca bir koleksiyon belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="59193-272">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="59193-273">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="59193-273">Performance and Tuning</span></span>
<span data-ttu-id="59193-274">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="59193-274">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
