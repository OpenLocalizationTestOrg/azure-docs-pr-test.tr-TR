---
title: Azure tablo/aaaMove verileri | Microsoft Docs
description: "Bilgi nasıl/Azure Data Factory kullanarak Azure Table Storage toomove verileri."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="ec7af-103">Azure Data Factory kullanarak Azure tablodan veri tooand taşıma</span><span class="sxs-lookup"><span data-stu-id="ec7af-103">Move data tooand from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="ec7af-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri öğesine/öğesinden Azure Table Storage açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ec7af-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Table Storage.</span></span> <span data-ttu-id="ec7af-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="ec7af-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="ec7af-106">Veri depolamak tooAzure Table Storage veya Azure Table Storage desteklenen tooany havuz verileri depolamak herhangi desteklenen bir kaynaktan veri kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec7af-106">You can copy data from any supported source data store tooAzure Table Storage or from Azure Table Storage tooany supported sink data store.</span></span> <span data-ttu-id="ec7af-107">Merhaba kaynakları veya havuzlarını olarak hello kopyalama etkinliği tarafından desteklenen veri depoları listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="ec7af-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="ec7af-108">Başlarken</span><span class="sxs-lookup"><span data-stu-id="ec7af-108">Getting started</span></span>
<span data-ttu-id="ec7af-109">Farklı araçlar/API'lerini kullanarak Azure Table Storage/gruptan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ec7af-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="ec7af-110">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="ec7af-110">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="ec7af-111">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="ec7af-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="ec7af-112">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="ec7af-112">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ec7af-113">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="ec7af-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="ec7af-114">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ec7af-114">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="ec7af-115">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="ec7af-115">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="ec7af-116">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="ec7af-116">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="ec7af-117">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="ec7af-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="ec7af-118">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ec7af-118">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="ec7af-119">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ec7af-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="ec7af-120">Bir Azure Table Storage/kullanılan toocopy verileri olan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="ec7af-120">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="ec7af-121">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooAzure Table Storage olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="ec7af-121">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="ec7af-122">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="ec7af-122">Linked service properties</span></span>
<span data-ttu-id="ec7af-123">İki tür vardır bağlı hizmetler toolink Azure blob depolama tooan Azure data factory kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec7af-123">There are two types of linked services you can use toolink an Azure blob storage tooan Azure data factory.</span></span> <span data-ttu-id="ec7af-124">Bunlar: **AzureStorage** bağlantılı hizmeti ve **AzureStorageSas** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="ec7af-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="ec7af-125">Hello Azure Storage bağlı hizmeti hello data factory genel erişim toohello Azure Storage ile sağlar.</span><span class="sxs-lookup"><span data-stu-id="ec7af-125">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="ec7af-126">Hello Azure depolama SAS (paylaşılan erişim imzası) bağlı ise hello data factory ile sınırlı/zaman sınırlı erişim toohello Azure depolama hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="ec7af-126">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="ec7af-127">Bu iki bağlı hizmet arasındaki herhangi bir fark vardır.</span><span class="sxs-lookup"><span data-stu-id="ec7af-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="ec7af-128">Gereksinimlerinize uygun hello bağlı hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="ec7af-128">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="ec7af-129">Merhaba aşağıdaki bölümlerde daha fazla ayrıntı bu iki bağlı hizmet sağlar.</span><span class="sxs-lookup"><span data-stu-id="ec7af-129">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="ec7af-130">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="ec7af-130">Dataset properties</span></span>
<span data-ttu-id="ec7af-131">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ec7af-131">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="ec7af-132">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="ec7af-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="ec7af-133">Merhaba typeProperties bölümü veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ec7af-133">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="ec7af-134">Merhaba **typeProperties** hello veri kümesi için bir bölüm türü **AzureTable** hello aşağıdaki özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ec7af-134">hello **typeProperties** section for hello dataset of type **AzureTable** has hello following properties.</span></span>

| <span data-ttu-id="ec7af-135">Özellik</span><span class="sxs-lookup"><span data-stu-id="ec7af-135">Property</span></span> | <span data-ttu-id="ec7af-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ec7af-136">Description</span></span> | <span data-ttu-id="ec7af-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ec7af-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ec7af-138">tableName</span><span class="sxs-lookup"><span data-stu-id="ec7af-138">tableName</span></span> |<span data-ttu-id="ec7af-139">Bağlantılı hizmetinin hello Azure tablo veritabanı örneğinde Merhaba tablonun adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ec7af-139">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="ec7af-140">Evet.</span><span class="sxs-lookup"><span data-stu-id="ec7af-140">Yes.</span></span> <span data-ttu-id="ec7af-141">Bir tableName bir azureTableSourceQuery belirtildiğinde, tüm hello tablosundan kopyalanan toohello hedef kayıtlarıdır.</span><span class="sxs-lookup"><span data-stu-id="ec7af-141">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="ec7af-142">Bir azureTableSourceQuery de belirtilirse hello sorguyu karşılayan hello tablosundan kopyalanan toohello hedef kayıtlarıdır.</span><span class="sxs-lookup"><span data-stu-id="ec7af-142">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="ec7af-143">Şema tarafından veri fabrikası</span><span class="sxs-lookup"><span data-stu-id="ec7af-143">Schema by Data Factory</span></span>
<span data-ttu-id="ec7af-144">Azure Table gibi şemasız veri depoları için hello Data Factory hizmetinin yolları aşağıdaki hello birinde hello şema oluşturur:</span><span class="sxs-lookup"><span data-stu-id="ec7af-144">For schema-free data stores such as Azure Table, hello Data Factory service infers hello schema in one of hello following ways:</span></span>

1. <span data-ttu-id="ec7af-145">Hello kullanarak verilerin hello yapısını belirtirseniz **yapısı** hello veri kümesi tanımında hello Data Factory hizmeti özelliği bu yapısı hello şema olarak geliştirir.</span><span class="sxs-lookup"><span data-stu-id="ec7af-145">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="ec7af-146">Bu durumda, bir satır bir sütun için bir değer içermiyorsa, bir null değer için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="ec7af-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="ec7af-147">Hello kullanarak verilerin hello yapısını belirtmezseniz **yapısı** hello veri kümesi tanımı, veri fabrikası özelliğinde hello verilerde hello ilk satırını kullanarak hello şema oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ec7af-147">If you don't specify hello structure of data by using hello **structure** property in hello dataset definition, Data Factory infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="ec7af-148">Bu durumda, Hello ilk satır hello tam şema içermiyorsa, bazı sütunları hello kopyalama işlemi sonucunda eksik.</span><span class="sxs-lookup"><span data-stu-id="ec7af-148">In this case, if hello first row does not contain hello full schema, some columns are missed in hello result of copy operation.</span></span>

<span data-ttu-id="ec7af-149">Bu nedenle, şemasız veri kaynakları için hello en iyi uygulama toospecify hello hello kullanarak veri yapısıdır **yapısı** özelliği.</span><span class="sxs-lookup"><span data-stu-id="ec7af-149">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="ec7af-150">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="ec7af-150">Copy activity properties</span></span>
<span data-ttu-id="ec7af-151">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ec7af-151">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ec7af-152">Ad, açıklama, giriş ve çıkış veri kümeleri ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ec7af-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="ec7af-153">Özellikler hello hello faaliyete hello typeProperties bölümünde kullanılabilir diğer yandan farklılık ile her etkinlik türü.</span><span class="sxs-lookup"><span data-stu-id="ec7af-153">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="ec7af-154">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="ec7af-154">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="ec7af-155">**AzureTableSource** aşağıdaki özelliklere typeProperties bölümdeki hello destekler:</span><span class="sxs-lookup"><span data-stu-id="ec7af-155">**AzureTableSource** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="ec7af-156">Özellik</span><span class="sxs-lookup"><span data-stu-id="ec7af-156">Property</span></span> | <span data-ttu-id="ec7af-157">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ec7af-157">Description</span></span> | <span data-ttu-id="ec7af-158">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="ec7af-158">Allowed values</span></span> | <span data-ttu-id="ec7af-159">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ec7af-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ec7af-160">azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="ec7af-160">azureTableSourceQuery</span></span> |<span data-ttu-id="ec7af-161">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="ec7af-161">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ec7af-162">Azure tablo sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="ec7af-162">Azure table query string.</span></span> <span data-ttu-id="ec7af-163">Merhaba sonraki bölümdeki örneklere bakın.</span><span class="sxs-lookup"><span data-stu-id="ec7af-163">See examples in hello next section.</span></span> |<span data-ttu-id="ec7af-164">Hayır.</span><span class="sxs-lookup"><span data-stu-id="ec7af-164">No.</span></span> <span data-ttu-id="ec7af-165">Bir tableName bir azureTableSourceQuery belirtildiğinde, tüm hello tablosundan kopyalanan toohello hedef kayıtlarıdır.</span><span class="sxs-lookup"><span data-stu-id="ec7af-165">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="ec7af-166">Bir azureTableSourceQuery de belirtilirse hello sorguyu karşılayan hello tablosundan kopyalanan toohello hedef kayıtlarıdır.</span><span class="sxs-lookup"><span data-stu-id="ec7af-166">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="ec7af-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="ec7af-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="ec7af-168">Tablonun swallow hello özel durum var olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ec7af-168">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="ec7af-169">TRUE</span><span class="sxs-lookup"><span data-stu-id="ec7af-169">TRUE</span></span><br/><span data-ttu-id="ec7af-170">FALSE</span><span class="sxs-lookup"><span data-stu-id="ec7af-170">FALSE</span></span> |<span data-ttu-id="ec7af-171">Hayır</span><span class="sxs-lookup"><span data-stu-id="ec7af-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="ec7af-172">azureTableSourceQuery örnekleri</span><span class="sxs-lookup"><span data-stu-id="ec7af-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="ec7af-173">Azure tablo sütunu dize türü ise:</span><span class="sxs-lookup"><span data-stu-id="ec7af-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="ec7af-174">Azure tablo sütunu datetime türü ise:</span><span class="sxs-lookup"><span data-stu-id="ec7af-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="ec7af-175">**AzureTableSink** aşağıdaki özelliklere typeProperties bölümdeki hello destekler:</span><span class="sxs-lookup"><span data-stu-id="ec7af-175">**AzureTableSink** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="ec7af-176">Özellik</span><span class="sxs-lookup"><span data-stu-id="ec7af-176">Property</span></span> | <span data-ttu-id="ec7af-177">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ec7af-177">Description</span></span> | <span data-ttu-id="ec7af-178">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="ec7af-178">Allowed values</span></span> | <span data-ttu-id="ec7af-179">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ec7af-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ec7af-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="ec7af-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="ec7af-181">Merhaba havuzu tarafından kullanılan varsayılan bölüm anahtar değeri.</span><span class="sxs-lookup"><span data-stu-id="ec7af-181">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="ec7af-182">Bir dize değeri.</span><span class="sxs-lookup"><span data-stu-id="ec7af-182">A string value.</span></span> |<span data-ttu-id="ec7af-183">Hayır</span><span class="sxs-lookup"><span data-stu-id="ec7af-183">No</span></span> |
| <span data-ttu-id="ec7af-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="ec7af-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="ec7af-185">Değerleri bölüm anahtarları olarak kullanılan hello sütunun adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="ec7af-185">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="ec7af-186">Belirtilmezse, AzureTableDefaultPartitionKeyValue hello bölüm anahtarı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ec7af-186">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="ec7af-187">Sütun adı.</span><span class="sxs-lookup"><span data-stu-id="ec7af-187">A column name.</span></span> |<span data-ttu-id="ec7af-188">Hayır</span><span class="sxs-lookup"><span data-stu-id="ec7af-188">No</span></span> |
| <span data-ttu-id="ec7af-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="ec7af-189">azureTableRowKeyName</span></span> |<span data-ttu-id="ec7af-190">Sütun değerleri satır anahtarı olarak kullanılan hello sütunun adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="ec7af-190">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="ec7af-191">Belirtilmezse, her satır için bir GUID kullanın.</span><span class="sxs-lookup"><span data-stu-id="ec7af-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="ec7af-192">Sütun adı.</span><span class="sxs-lookup"><span data-stu-id="ec7af-192">A column name.</span></span> |<span data-ttu-id="ec7af-193">Hayır</span><span class="sxs-lookup"><span data-stu-id="ec7af-193">No</span></span> |
| <span data-ttu-id="ec7af-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="ec7af-194">azureTableInsertType</span></span> |<span data-ttu-id="ec7af-195">başlangıç modu tooinsert verileri Azure tablosuna.</span><span class="sxs-lookup"><span data-stu-id="ec7af-195">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="ec7af-196">Bu özellik, varolan satırlardan eşleşen bölüm ve satır anahtarlarla hello çıkış tablodaki birleştirilmiş veya değiştirilmesi değerlerine sahip olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="ec7af-196">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="ec7af-197">Bu ayarların (birleştirme ve değiştirme) nasıl çalıştığını, ilgili toolearn bkz [ekleme veya birleştirme varlık](https://msdn.microsoft.com/library/azure/hh452241.aspx) ve [ekleme veya değiştirme varlık](https://msdn.microsoft.com/library/azure/hh452242.aspx) konuları.</span><span class="sxs-lookup"><span data-stu-id="ec7af-197">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="ec7af-198">Hello satır düzeyinde, hello tablo düzeyinde değil, bu ayar uygulanır ve her iki seçenek hello giriş yok hello çıkış tablosundaki satırları siler.</span><span class="sxs-lookup"><span data-stu-id="ec7af-198">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="ec7af-199">Merge (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="ec7af-199">merge (default)</span></span><br/><span data-ttu-id="ec7af-200">Değiştir</span><span class="sxs-lookup"><span data-stu-id="ec7af-200">replace</span></span> |<span data-ttu-id="ec7af-201">Hayır</span><span class="sxs-lookup"><span data-stu-id="ec7af-201">No</span></span> |
| <span data-ttu-id="ec7af-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ec7af-202">writeBatchSize</span></span> |<span data-ttu-id="ec7af-203">Merhaba writeBatchSize veya writeBatchTimeout gelindiğinde veri hello Azure tablo ekler.</span><span class="sxs-lookup"><span data-stu-id="ec7af-203">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="ec7af-204">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="ec7af-204">Integer (number of rows)</span></span> |<span data-ttu-id="ec7af-205">Hayır (varsayılan: 10000)</span><span class="sxs-lookup"><span data-stu-id="ec7af-205">No (default: 10000)</span></span> |
| <span data-ttu-id="ec7af-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="ec7af-206">writeBatchTimeout</span></span> |<span data-ttu-id="ec7af-207">Merhaba writeBatchSize veya writeBatchTimeout gelindiğinde veri hello Azure tablo ekler.</span><span class="sxs-lookup"><span data-stu-id="ec7af-207">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="ec7af-208">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="ec7af-208">timespan</span></span><br/><br/><span data-ttu-id="ec7af-209">Örnek: "00: 20:00" (20 dakika)</span><span class="sxs-lookup"><span data-stu-id="ec7af-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="ec7af-210">Hayır (varsayılan toostorage istemci varsayılan zaman aşımı değeri 90 saniye)</span><span class="sxs-lookup"><span data-stu-id="ec7af-210">No (Default toostorage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="ec7af-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="ec7af-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="ec7af-212">Merhaba hedef sütun azureTablePartitionKeyName hello olarak kullanabilmeniz için önce hello Çeviricisi JSON özelliğini kullanarak bir kaynak sütun tooa hedef sütun eşleyin.</span><span class="sxs-lookup"><span data-stu-id="ec7af-212">Map a source column tooa destination column using hello translator JSON property before you can use hello destination column as hello azureTablePartitionKeyName.</span></span>

<span data-ttu-id="ec7af-213">Aşağıdaki örneğine hello kaynak sütunu DivisionID eşlenen toohello hedef sütundur: DivisionID.</span><span class="sxs-lookup"><span data-stu-id="ec7af-213">In hello following example, source column DivisionID is mapped toohello destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="ec7af-214">Merhaba DivisionID hello bölüm anahtarı olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="ec7af-214">hello DivisionID is specified as hello partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="ec7af-215">JSON örnekleri</span><span class="sxs-lookup"><span data-stu-id="ec7af-215">JSON examples</span></span>
<span data-ttu-id="ec7af-216">Merhaba aşağıdaki örneklerde sağlayan örnek JSON tanımları toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ec7af-216">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="ec7af-217">Bunlar Göster nasıl toocopy veri tooand Azure Table Storage ve Azure Blob veritabanı.</span><span class="sxs-lookup"><span data-stu-id="ec7af-217">They show how toocopy data tooand from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="ec7af-218">Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden hello kaynakları tooany desteklenen hello havuzlarını biri.</span><span class="sxs-lookup"><span data-stu-id="ec7af-218">However, data can be copied **directly** from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="ec7af-219">Daha fazla bilgi için hello "desteklenen veri depoları ve biçimleri" bölümüne bakın [Kopyala etkinliğini kullanarak veri taşıma](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ec7af-219">For more information, see hello section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a><span data-ttu-id="ec7af-220">Örnek: Verilerini Azure Table tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="ec7af-220">Example: Copy data from Azure Table tooAzure Blob</span></span>
<span data-ttu-id="ec7af-221">Merhaba, aşağıdaki örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="ec7af-221">hello following sample shows:</span></span>

1. <span data-ttu-id="ec7af-222">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (Tablo & blob için kullanılır).</span><span class="sxs-lookup"><span data-stu-id="ec7af-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="ec7af-223">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ec7af-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="ec7af-224">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ec7af-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="ec7af-225">Merhaba [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [AzureTableSource](#activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ec7af-225">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="ec7af-226">Merhaba örnek bir Azure Table tooa blob toohello varsayılan bölümünde saatte ait verileri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="ec7af-226">hello sample copies data belonging toohello default partition in an Azure Table tooa blob every hour.</span></span> <span data-ttu-id="ec7af-227">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ec7af-227">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="ec7af-228">**Azure depolama bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="ec7af-228">**Azure storage linked service:**</span></span>

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
<span data-ttu-id="ec7af-229">Azure Data Factory iki tür Azure Storage bağlı hizmeti destekler: **AzureStorage** ve **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="ec7af-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="ec7af-230">İçin birinci Merhaba, hello hesap anahtarı içeren hello bağlantı dizesini belirtin ve hello daha ileri bir hello paylaşılan erişim imzası (SAS) URI belirtin.</span><span class="sxs-lookup"><span data-stu-id="ec7af-230">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="ec7af-231">Bkz: [bağlı hizmetler](#linked-service-properties) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="ec7af-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="ec7af-232">**Azure Tablo girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="ec7af-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="ec7af-233">Merhaba örnek Azure tablosunda tablo "MyTable" oluşturdunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="ec7af-233">hello sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="ec7af-234">"Dış" ayarı: "true" bildirir hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="ec7af-234">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="ec7af-235">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="ec7af-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="ec7af-236">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="ec7af-236">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ec7af-237">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="ec7af-237">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="ec7af-238">Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ec7af-238">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="ec7af-239">**AzureTableSource ve BlobSink ardışık düzeninde etkinlik kopyalayın:**</span><span class="sxs-lookup"><span data-stu-id="ec7af-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="ec7af-240">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="ec7af-240">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="ec7af-241">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**AzureTableSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="ec7af-241">In hello pipeline JSON definition, hello **source** type is set too**AzureTableSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="ec7af-242">Merhaba SQL sorgusu ile belirtilen **AzureTableSourceQuery** özelliği her saat toocopy hello varsayılan bölümünden hello veri seçer.</span><span class="sxs-lookup"><span data-stu-id="ec7af-242">hello SQL query specified with **AzureTableSourceQuery** property selects hello data from hello default partition every hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },                
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
            }
         ]    
    }
}
```

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a><span data-ttu-id="ec7af-243">Örnek: Kopyalama verileri Azure Blob tooAzure tablosu</span><span class="sxs-lookup"><span data-stu-id="ec7af-243">Example: Copy data from Azure Blob tooAzure Table</span></span>
<span data-ttu-id="ec7af-244">Merhaba, aşağıdaki örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="ec7af-244">hello following sample shows:</span></span>

1. <span data-ttu-id="ec7af-245">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (Tablo & blob için kullanılır)</span><span class="sxs-lookup"><span data-stu-id="ec7af-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="ec7af-246">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ec7af-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="ec7af-247">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ec7af-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="ec7af-248">Merhaba [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) ve [AzureTableSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ec7af-248">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="ec7af-249">Merhaba örnek time series verilerini saatlik bir Azure blob tooan Azure tablosuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="ec7af-249">hello sample copies time-series data from an Azure blob tooan Azure table hourly.</span></span> <span data-ttu-id="ec7af-250">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ec7af-250">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="ec7af-251">**(İçin Azure Table & Blob) azure depolama bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="ec7af-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

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

<span data-ttu-id="ec7af-252">Azure Data Factory iki tür Azure Storage bağlı hizmeti destekler: **AzureStorage** ve **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="ec7af-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="ec7af-253">İçin birinci Merhaba, hello hesap anahtarı içeren hello bağlantı dizesini belirtin ve hello daha ileri bir hello paylaşılan erişim imzası (SAS) URI belirtin.</span><span class="sxs-lookup"><span data-stu-id="ec7af-253">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="ec7af-254">Bkz: [bağlı hizmetler](#linked-service-properties) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="ec7af-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="ec7af-255">**Azure Blob girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="ec7af-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="ec7af-256">Veri toplanma yeni blob üzerinden saatte (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="ec7af-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ec7af-257">Merhaba klasör yolu ve dosya adını hello blob dinamik olarak değerlendirilir işleniyor hello dilimin hello başlangıç zamanı temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="ec7af-257">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="ec7af-258">Merhaba klasör yolu yıl, ay ve gün kısmını hello başlangıç saati ve dosya adı hello başlangıç saati hello saat bölümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="ec7af-258">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="ec7af-259">"dış": "true" ayarı bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil hello Data Factory hizmetinin sizi bilgilendirir.</span><span class="sxs-lookup"><span data-stu-id="ec7af-259">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="ec7af-260">**Azure tablo çıkış dataset:**</span><span class="sxs-lookup"><span data-stu-id="ec7af-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="ec7af-261">Merhaba örnek Azure tablosunda "MyTable" olarak adlandırılan veri tooa tablosuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="ec7af-261">hello sample copies data tooa table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="ec7af-262">Bir Azure tablosu ile oluşturma hello Blob CSV dosyası toocontain beklediğiniz gibi hello aynı sayıda sütun.</span><span class="sxs-lookup"><span data-stu-id="ec7af-262">Create an Azure table with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="ec7af-263">Yeni satırlar toohello tablo saatte eklenir.</span><span class="sxs-lookup"><span data-stu-id="ec7af-263">New rows are added toohello table every hour.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="ec7af-264">**BlobSource ve AzureTableSink ardışık düzeninde etkinlik kopyalayın:**</span><span class="sxs-lookup"><span data-stu-id="ec7af-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="ec7af-265">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="ec7af-265">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="ec7af-266">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**BlobSource** ve **havuz** türü olarak ayarlanmış çok**AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="ec7af-266">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**AzureTableSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
          }
        },
        "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },                        
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="ec7af-267">Tür eşlemesi için Azure tablo</span><span class="sxs-lookup"><span data-stu-id="ec7af-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="ec7af-268">Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri iki aşamalı bir yaklaşım aşağıdaki hello ile.</span><span class="sxs-lookup"><span data-stu-id="ec7af-268">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="ec7af-269">Yerel kaynak türleri too.NET türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="ec7af-269">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="ec7af-270">.NET türü toonative havuz türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="ec7af-270">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="ec7af-271">Çok & Azure tablodan veri taşırken, aşağıdaki hello [Azure tablo hizmeti tarafından tanımlanan eşlemeler](https://msdn.microsoft.com/library/azure/dd179338.aspx) Azure tablo OData türlerini too.NET türünden ve kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ec7af-271">When moving data too& from Azure Table, hello following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types too.NET type and vice versa.</span></span>

| <span data-ttu-id="ec7af-272">OData veri türü</span><span class="sxs-lookup"><span data-stu-id="ec7af-272">OData Data Type</span></span> | <span data-ttu-id="ec7af-273">.NET türü</span><span class="sxs-lookup"><span data-stu-id="ec7af-273">.NET Type</span></span> | <span data-ttu-id="ec7af-274">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="ec7af-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ec7af-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="ec7af-275">Edm.Binary</span></span> |<span data-ttu-id="ec7af-276">Byte]</span><span class="sxs-lookup"><span data-stu-id="ec7af-276">byte[]</span></span> |<span data-ttu-id="ec7af-277">Too64 KB oluşturan bir bayt dizisi.</span><span class="sxs-lookup"><span data-stu-id="ec7af-277">An array of bytes up too64 KB.</span></span> |
| <span data-ttu-id="ec7af-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="ec7af-278">Edm.Boolean</span></span> |<span data-ttu-id="ec7af-279">bool</span><span class="sxs-lookup"><span data-stu-id="ec7af-279">bool</span></span> |<span data-ttu-id="ec7af-280">Bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="ec7af-280">A Boolean value.</span></span> |
| <span data-ttu-id="ec7af-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="ec7af-281">Edm.DateTime</span></span> |<span data-ttu-id="ec7af-282">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="ec7af-282">DateTime</span></span> |<span data-ttu-id="ec7af-283">Eşgüdümlü Evrensel Saat (UTC) olarak ifade edilen bir 64-bit değeri.</span><span class="sxs-lookup"><span data-stu-id="ec7af-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="ec7af-284">Aralık 1 Ocak 1601 gece 12:00 gece ' başlayan DateTime Hello desteklenir</span><span class="sxs-lookup"><span data-stu-id="ec7af-284">hello supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="ec7af-285">(C.E.) UTC.</span><span class="sxs-lookup"><span data-stu-id="ec7af-285">(C.E.), UTC.</span></span> <span data-ttu-id="ec7af-286">Merhaba Aralık 9999 31 Aralık sona erer.</span><span class="sxs-lookup"><span data-stu-id="ec7af-286">hello range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="ec7af-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="ec7af-287">Edm.Double</span></span> |<span data-ttu-id="ec7af-288">Çift</span><span class="sxs-lookup"><span data-stu-id="ec7af-288">double</span></span> |<span data-ttu-id="ec7af-289">Bir 64-bit kayan noktalı değeri.</span><span class="sxs-lookup"><span data-stu-id="ec7af-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="ec7af-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="ec7af-290">Edm.Guid</span></span> |<span data-ttu-id="ec7af-291">GUID</span><span class="sxs-lookup"><span data-stu-id="ec7af-291">Guid</span></span> |<span data-ttu-id="ec7af-292">128-bit bir genel benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="ec7af-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="ec7af-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="ec7af-293">Edm.Int32</span></span> |<span data-ttu-id="ec7af-294">Int32</span><span class="sxs-lookup"><span data-stu-id="ec7af-294">Int32</span></span> |<span data-ttu-id="ec7af-295">Bir 32 bit tamsayı.</span><span class="sxs-lookup"><span data-stu-id="ec7af-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="ec7af-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="ec7af-296">Edm.Int64</span></span> |<span data-ttu-id="ec7af-297">Int64</span><span class="sxs-lookup"><span data-stu-id="ec7af-297">Int64</span></span> |<span data-ttu-id="ec7af-298">64 bitlik bir tamsayı.</span><span class="sxs-lookup"><span data-stu-id="ec7af-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="ec7af-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="ec7af-299">Edm.String</span></span> |<span data-ttu-id="ec7af-300">Dize</span><span class="sxs-lookup"><span data-stu-id="ec7af-300">String</span></span> |<span data-ttu-id="ec7af-301">UTF-16 kodlu değer.</span><span class="sxs-lookup"><span data-stu-id="ec7af-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="ec7af-302">Dize değerlerini too64 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="ec7af-302">String values may be up too64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="ec7af-303">Tür dönüştürme örnek</span><span class="sxs-lookup"><span data-stu-id="ec7af-303">Type Conversion Sample</span></span>
<span data-ttu-id="ec7af-304">veri türü dönüşümleri ile Azure Blob tooAzure Tablo kopyalama için örnek aşağıdaki hello olur.</span><span class="sxs-lookup"><span data-stu-id="ec7af-304">hello following sample is for copying data from an Azure Blob tooAzure Table with type conversions.</span></span>

<span data-ttu-id="ec7af-305">Merhaba Blob dataset CSV biçiminde olduğunu ve üç sütun içeren varsayalım.</span><span class="sxs-lookup"><span data-stu-id="ec7af-305">Suppose hello Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="ec7af-306">Bunlardan biri, hello haftanın günü için kısaltılmış Fransızca adları kullanarak bir özel datetime biçimiyle datetime bir sütundur.</span><span class="sxs-lookup"><span data-stu-id="ec7af-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of hello week.</span></span>

<span data-ttu-id="ec7af-307">Merhaba Blob kaynağı dataset hello sütunlar için tür tanımları birlikte aşağıdaki gibi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ec7af-307">Define hello Blob Source dataset as follows along with type definitions for hello columns.</span></span>

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="ec7af-308">Merhaba türü eşlemesi Azure tablo OData türü too.NET türünden verildiğinde, şema aşağıdaki hello ile Azure tablosunda hello tablo tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="ec7af-308">Given hello type mapping from Azure Table OData type too.NET type, you would define hello table in Azure Table with hello following schema.</span></span>

<span data-ttu-id="ec7af-309">**Azure tablo şemasını:**</span><span class="sxs-lookup"><span data-stu-id="ec7af-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="ec7af-310">Sütun adı</span><span class="sxs-lookup"><span data-stu-id="ec7af-310">Column name</span></span> | <span data-ttu-id="ec7af-311">Tür</span><span class="sxs-lookup"><span data-stu-id="ec7af-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="ec7af-312">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="ec7af-312">userid</span></span> |<span data-ttu-id="ec7af-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="ec7af-313">Edm.Int64</span></span> |
| <span data-ttu-id="ec7af-314">ad</span><span class="sxs-lookup"><span data-stu-id="ec7af-314">name</span></span> |<span data-ttu-id="ec7af-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="ec7af-315">Edm.String</span></span> |
| <span data-ttu-id="ec7af-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="ec7af-316">lastlogindate</span></span> |<span data-ttu-id="ec7af-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="ec7af-317">Edm.DateTime</span></span> |

<span data-ttu-id="ec7af-318">Ardından, hello Azure Table dataset aşağıdaki gibi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ec7af-318">Next, define hello Azure Table dataset as follows.</span></span> <span data-ttu-id="ec7af-319">Veri deposu temel hello Hello türü bilgileri önceden belirtildiği toospecify "yapısı" Merhaba türü bilgileri bölümle gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ec7af-319">You do not need toospecify “structure” section with hello type information since hello type information is already specified in hello underlying data store.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="ec7af-320">Bu durumda, veri fabrikası dönüşümleri hello Datetime alan verileri Blob tooAzure tablo taşırken hello "fr-fr" kültürü kullanarak hello özel datetime biçimine de dahil olmak üzere otomatik olarak yazın.</span><span class="sxs-lookup"><span data-stu-id="ec7af-320">In this case, Data Factory automatically does type conversions including hello Datetime field with hello custom datetime format using hello "fr-fr" culture when moving data from Blob tooAzure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="ec7af-321">Kaynak veri kümesi toocolumns havuz kümesinden toomap sütunlarından bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="ec7af-321">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="ec7af-322">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="ec7af-322">Performance and Tuning</span></span>
<span data-ttu-id="ec7af-323">anahtarı hakkında toolearn Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını, bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="ec7af-323">toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
