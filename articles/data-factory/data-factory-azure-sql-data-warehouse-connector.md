---
title: "Veri kopyalama/Azure SQL veri ambarından | Microsoft Docs"
description: "Azure Data Factory kullanarak Azure SQL Data Warehouse öğesine/öğesinden veri kopyalama öğrenin"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 8cba89e0947646b498af07aa484511bf07bf7b0e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="copy-data-to-and-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="d4e4b-103">İçin ve Azure Data Factory kullanarak Azure SQL veri ambarından veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="d4e4b-103">Copy data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="d4e4b-104">Bu makalede kopya etkinliği Azure Data Factory'de Azure SQL Data Warehouse grafikten veri taşımak için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d4e4b-105">Derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) kopyalama etkinliği ile veri taşıma için genel bir bakış sunar makalesi.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="d4e4b-106">En iyi performansı elde etmek için Azure SQL Data Warehouse'a veri yüklemek için PolyBase kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-106">To achieve best performance, use PolyBase to load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d4e4b-107">[Kullanım Azure SQL Data Warehouse'a veri yüklemek için PolyBase](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) bölümde ayrıntılar bulunur.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-107">The [Use PolyBase to load data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="d4e4b-108">Kullanım örneği ile bir anlatım için bkz: [1 TB altında 15 dakika Azure Data Factory ile Azure SQL Data Warehouse'a veri yükleme](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="d4e4b-109">Desteklenen senaryolar</span><span class="sxs-lookup"><span data-stu-id="d4e4b-109">Supported scenarios</span></span>
<span data-ttu-id="d4e4b-110">Veri kopyalama **Azure SQL veri ambarından** aşağıdaki veri depolar:</span><span class="sxs-lookup"><span data-stu-id="d4e4b-110">You can copy data **from Azure SQL Data Warehouse** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="d4e4b-111">Aşağıdaki veri depolarına verileri kopyalayabilirsiniz **Azure SQL Data Warehouse için**:</span><span class="sxs-lookup"><span data-stu-id="d4e4b-111">You can copy data from the following data stores **to Azure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="d4e4b-112">Tablo hedef deposunda mevcut değilse veri SQL Server veya Azure SQL veritabanından Azure SQL Data Warehouse için kopyalarken, veri fabrikası otomatik olarak tablo SQL veri ambarı'nda kaynak veri deposunda tablonun şeması kullanarak oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-112">When copying data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse, if the table does not exist in the destination store, Data Factory can automatically create the table in SQL Data Warehouse by using the schema of the table in the source data store.</span></span> <span data-ttu-id="d4e4b-113">Bkz: [Otomatik Tablo oluşturma](#auto-table-creation) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="d4e4b-114">Desteklenen kimlik doğrulama türü</span><span class="sxs-lookup"><span data-stu-id="d4e4b-114">Supported authentication type</span></span>
<span data-ttu-id="d4e4b-115">Azure SQL Data Warehouse Bağlayıcısı destek temel kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d4e4b-116">Başlarken</span><span class="sxs-lookup"><span data-stu-id="d4e4b-116">Getting started</span></span>
<span data-ttu-id="d4e4b-117">Verileri farklı araçlar/API'lerini kullanarak Azure SQL Data Warehouse denetleyicisinden taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="d4e4b-118">Öğesine/öğesinden Azure SQL veri ambarı verileri kopyalayan bir işlem hattı oluşturmak için en kolay yolu, veri kopyalama Sihirbazı'nı kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-118">The easiest way to create a pipeline that copies data to/from Azure SQL Data Warehouse is to use the Copy data wizard.</span></span> <span data-ttu-id="d4e4b-119">Bkz: [öğretici: Data Factory ile SQL veri ambarına veri yükleme](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) veri kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="d4e4b-120">Bir işlem hattı oluşturmak için aşağıdaki araçları kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu**, **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d4e4b-121">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="d4e4b-122">Araçlar ya da API'leri kullanıp bir havuz veri deposu için bir kaynak veri deposundan verileri taşır bir ardışık düzen oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d4e4b-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="d4e4b-123">Oluşturma bir **veri fabrikası**.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-123">Create a **data factory**.</span></span> <span data-ttu-id="d4e4b-124">Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="d4e4b-125">Oluşturma **bağlantılı Hizmetleri** girdi ve çıktı verilerini bağlamak için veri fabrikanıza depolar.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-125">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="d4e4b-126">Örneğin, verileri Azure blob depolama alanından Azure SQL veri ambarı'na kopyalıyorsanız Azure depolama hesabı ve Azure SQL veri ambarı veri fabrikanıza bağlamak için iki bağlı hizmet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-126">For example, if you are copying data from an Azure blob storage to an Azure SQL data warehouse, you create two linked services to link your Azure storage account and Azure SQL data warehouse to your data factory.</span></span> <span data-ttu-id="d4e4b-127">Azure SQL Data Warehouse için özel bağlantılı hizmet özellikleri için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-127">For linked service properties that are specific to Azure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="d4e4b-128">Oluşturma **veri kümeleri** kopyalama işlemi için girdi ve çıktı verilerini temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-128">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="d4e4b-129">Son adımda bahsedilen örnekte blob kapsayıcısı ve giriş verilerini içeren klasörü belirtmek için bir veri kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-129">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="d4e4b-130">Ve blob depolama biriminden kopyalanan verilerini tutan Azure SQL data warehouse'da tablo belirtmek için başka bir veri kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-130">And, you create another dataset to specify the table in the Azure SQL data warehouse that holds the data copied from the blob storage.</span></span> <span data-ttu-id="d4e4b-131">Azure SQL Data Warehouse için özel veri kümesi özellikleri için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-131">For dataset properties that are specific to Azure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="d4e4b-132">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="d4e4b-133">Daha önce bahsedilen örnekte BlobSource bir kaynak ve SqlDWSink havuzu olarak kopya etkinliği için kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-133">In the example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for the copy activity.</span></span> <span data-ttu-id="d4e4b-134">Azure Blob depolama alanına Azure SQL veri ambarından kopyalıyorsanız benzer şekilde, SqlDWSource ve BlobSink kopyalama etkinliği kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-134">Similarly, if you are copying from Azure SQL Data Warehouse to Azure Blob Storage, you use SqlDWSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="d4e4b-135">Azure SQL Data Warehouse için belirli kopyalama etkinliği özellikleri için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-135">For copy activity properties that are specific to Azure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="d4e4b-136">Bir veri deposu bir kaynak veya bir havuz nasıl kullanılacağı hakkında daha fazla bilgi için önceki bölümde, veri deposu için bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-136">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="d4e4b-137">Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-137">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="d4e4b-138">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, JSON biçimini kullanarak bu Data Factory varlıklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="d4e4b-139">/ Azure SQL Data Warehouse veri kopyalamak için kullanılan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-139">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="d4e4b-140">Aşağıdaki bölümler, Azure SQL Data Warehouse için Data Factory varlıklarını belirli tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="d4e4b-140">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d4e4b-141">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="d4e4b-141">Linked service properties</span></span>
<span data-ttu-id="d4e4b-142">Aşağıdaki tabloda, Azure SQL Data Warehouse bağlantılı hizmete özgü JSON öğelerini açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-142">The following table provides description for JSON elements specific to Azure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="d4e4b-143">Özellik</span><span class="sxs-lookup"><span data-stu-id="d4e4b-143">Property</span></span> | <span data-ttu-id="d4e4b-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d4e4b-144">Description</span></span> | <span data-ttu-id="d4e4b-145">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d4e4b-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4e4b-146">type</span><span class="sxs-lookup"><span data-stu-id="d4e4b-146">type</span></span> |<span data-ttu-id="d4e4b-147">Type özelliği ayarlanmalıdır: **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="d4e4b-147">The type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="d4e4b-148">Evet</span><span class="sxs-lookup"><span data-stu-id="d4e4b-148">Yes</span></span> |
| <span data-ttu-id="d4e4b-149">connectionString</span><span class="sxs-lookup"><span data-stu-id="d4e4b-149">connectionString</span></span> |<span data-ttu-id="d4e4b-150">ConnectionString özelliği için Azure SQL Data Warehouse örneğine bağlanmak için gereken bilgileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-150">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> <span data-ttu-id="d4e4b-151">Yalnızca temel kimlik doğrulama desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="d4e4b-152">Evet</span><span class="sxs-lookup"><span data-stu-id="d4e4b-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="d4e4b-153">Yapılandırma [Azure SQL veritabanı Güvenlik Duvarı](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) ve veritabanı sunucusuna [Azure hizmetlerinin sunucuya erişimine izin](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="d4e4b-154">Ayrıca, dış Azure veri fabrikası ağ geçidi ile şirket içi veri kaynaklarından dahil olmak üzere Azure SQL Data Warehouse'a veri kopyalıyorsanız, verileri Azure SQL Data Warehouse için gönderme makine için uygun IP adresi aralığı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-154">Additionally, if you are copying data to Azure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="d4e4b-155">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="d4e4b-155">Dataset properties</span></span>
<span data-ttu-id="d4e4b-156">Bölümler & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-156">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d4e4b-157">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="d4e4b-158">TypeProperties bölümü dataset her tür için farklıdır ve verilerin veri deposunda konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-158">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="d4e4b-159">**TypeProperties** veri kümesi için bir bölüm türü **AzureSqlDWTable** aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d4e4b-159">The **typeProperties** section for the dataset of type **AzureSqlDWTable** has the following properties:</span></span>

| <span data-ttu-id="d4e4b-160">Özellik</span><span class="sxs-lookup"><span data-stu-id="d4e4b-160">Property</span></span> | <span data-ttu-id="d4e4b-161">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d4e4b-161">Description</span></span> | <span data-ttu-id="d4e4b-162">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d4e4b-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4e4b-163">tableName</span><span class="sxs-lookup"><span data-stu-id="d4e4b-163">tableName</span></span> |<span data-ttu-id="d4e4b-164">Tablo veya Görünüm başvuran bağlı hizmetin Azure SQL veri ambarı veritabanındaki adı.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-164">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="d4e4b-165">Evet</span><span class="sxs-lookup"><span data-stu-id="d4e4b-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="d4e4b-166">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="d4e4b-166">Copy activity properties</span></span>
<span data-ttu-id="d4e4b-167">Bölümler & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz: [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-167">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d4e4b-168">Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="d4e4b-169">Kopyalama etkinliği yalnızca bir girdi alır ve tek bir çıktı üretir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-169">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="d4e4b-170">Oysa etkinliğin typeProperties bölümündeki özellikler her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-170">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="d4e4b-171">Kopya etkinliği için bunlar türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-171">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="d4e4b-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="d4e4b-172">SqlDWSource</span></span>
<span data-ttu-id="d4e4b-173">Kaynak türü olduğunda **SqlDWSource**, aşağıdaki özellikler mevcuttur **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="d4e4b-173">When source is of type **SqlDWSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="d4e4b-174">Özellik</span><span class="sxs-lookup"><span data-stu-id="d4e4b-174">Property</span></span> | <span data-ttu-id="d4e4b-175">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d4e4b-175">Description</span></span> | <span data-ttu-id="d4e4b-176">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="d4e4b-176">Allowed values</span></span> | <span data-ttu-id="d4e4b-177">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d4e4b-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d4e4b-178">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="d4e4b-178">sqlReaderQuery</span></span> |<span data-ttu-id="d4e4b-179">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-179">Use the custom query to read data.</span></span> |<span data-ttu-id="d4e4b-180">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-180">SQL query string.</span></span> <span data-ttu-id="d4e4b-181">Örneğin: seçin * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="d4e4b-182">Hayır</span><span class="sxs-lookup"><span data-stu-id="d4e4b-182">No</span></span> |
| <span data-ttu-id="d4e4b-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="d4e4b-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="d4e4b-184">Kaynak tablodan veri okuyan saklı yordamın adı.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-184">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="d4e4b-185">Saklı yordam adı.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-185">Name of the stored procedure.</span></span> <span data-ttu-id="d4e4b-186">Son SQL deyimi SELECT deyimi içinde saklı yordamı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-186">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="d4e4b-187">Hayır</span><span class="sxs-lookup"><span data-stu-id="d4e4b-187">No</span></span> |
| <span data-ttu-id="d4e4b-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="d4e4b-188">storedProcedureParameters</span></span> |<span data-ttu-id="d4e4b-189">Saklı yordam parametreleri.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-189">Parameters for the stored procedure.</span></span> |<span data-ttu-id="d4e4b-190">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-190">Name/value pairs.</span></span> <span data-ttu-id="d4e4b-191">Adları ve büyük/küçük harf parametrelerinin adlarını ve saklı yordam parametreleri büyük/küçük harf eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-191">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="d4e4b-192">Hayır</span><span class="sxs-lookup"><span data-stu-id="d4e4b-192">No</span></span> |

<span data-ttu-id="d4e4b-193">Varsa **sqlReaderQuery** belirtilen SqlDWSource için kopyalama etkinliği veri almak için Azure SQL Data Warehouse kaynağında bu sorguyu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-193">If the **sqlReaderQuery** is specified for the SqlDWSource, the Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>

<span data-ttu-id="d4e4b-194">Alternatif olarak, bir saklı yordam belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (saklı yordam parametreleri alıyorsa).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-194">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="d4e4b-195">SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz JSON veri kümesi yapısı bölümünde tanımlanan sütunları Azure SQL veri ambarına karşı çalıştırmak için bir sorgu oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d4e4b-196">Örnek: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="d4e4b-197">Veri kümesi tanımı yapısına sahip değilse, tüm sütunları tablodan seçilir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-197">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="d4e4b-198">SqlDWSource örneği</span><span class="sxs-lookup"><span data-stu-id="d4e4b-198">SqlDWSource example</span></span>

```JSON
"source": {
    "type": "SqlDWSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```
<span data-ttu-id="d4e4b-199">**Saklı yordam tanımı:**</span><span class="sxs-lookup"><span data-stu-id="d4e4b-199">**The stored procedure definition:**</span></span>

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqldwsink"></a><span data-ttu-id="d4e4b-200">SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="d4e4b-200">SqlDWSink</span></span>
<span data-ttu-id="d4e4b-201">**SqlDWSink** aşağıdaki özellikleri destekler:</span><span class="sxs-lookup"><span data-stu-id="d4e4b-201">**SqlDWSink** supports the following properties:</span></span>

| <span data-ttu-id="d4e4b-202">Özellik</span><span class="sxs-lookup"><span data-stu-id="d4e4b-202">Property</span></span> | <span data-ttu-id="d4e4b-203">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d4e4b-203">Description</span></span> | <span data-ttu-id="d4e4b-204">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="d4e4b-204">Allowed values</span></span> | <span data-ttu-id="d4e4b-205">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d4e4b-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d4e4b-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="d4e4b-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="d4e4b-207">Belirli bir dilimle verilerinin temizlenmesini şekilde yürütmek kopyalama etkinliği için bir sorgu belirtin.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-207">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="d4e4b-208">Ayrıntılar için bkz [Yinelenebilirlik bölüm](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="d4e4b-209">Sorgu bildirimi.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-209">A query statement.</span></span> |<span data-ttu-id="d4e4b-210">Hayır</span><span class="sxs-lookup"><span data-stu-id="d4e4b-210">No</span></span> |
| <span data-ttu-id="d4e4b-211">Bulunan'allowpolybase</span><span class="sxs-lookup"><span data-stu-id="d4e4b-211">allowPolyBase</span></span> |<span data-ttu-id="d4e4b-212">BULKINSERT mekanizması yerine PolyBase (varsa) kullanılıp kullanılmayacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-212">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="d4e4b-213">**PolyBase kullanarak SQL Data Warehouse'a veri yükleme için önerilen yoldur.**</span><span class="sxs-lookup"><span data-stu-id="d4e4b-213">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> <span data-ttu-id="d4e4b-214">Bkz [kullanım Azure SQL Data Warehouse'a veri yüklemek için PolyBase](#use-polybase-to-load-data-into-azure-sql-data-warehouse) kısıtlamaları ve ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-214">See [Use PolyBase to load data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="d4e4b-215">True</span><span class="sxs-lookup"><span data-stu-id="d4e4b-215">True</span></span> <br/><span data-ttu-id="d4e4b-216">False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="d4e4b-216">False (default)</span></span> |<span data-ttu-id="d4e4b-217">Hayır</span><span class="sxs-lookup"><span data-stu-id="d4e4b-217">No</span></span> |
| <span data-ttu-id="d4e4b-218">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="d4e4b-218">polyBaseSettings</span></span> |<span data-ttu-id="d4e4b-219">Bir grup olabilir özellik belirtilen **Bulunan'allowpolybase** özelliği ayarlanmış **doğru**.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-219">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="d4e4b-220">Hayır</span><span class="sxs-lookup"><span data-stu-id="d4e4b-220">No</span></span> |
| <span data-ttu-id="d4e4b-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="d4e4b-221">rejectValue</span></span> |<span data-ttu-id="d4e4b-222">Sayı veya yüzde değeri sorgu başarısız önce reddedilemiyor satır belirtir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-222">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="d4e4b-223">PolyBase'nın reddetme seçenekleri hakkında daha fazla bilgi **bağımsız değişkenleri** bölümünü [CREATE dış TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) konu.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-223">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="d4e4b-224">0 (varsayılan), 1, 2...</span><span class="sxs-lookup"><span data-stu-id="d4e4b-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="d4e4b-225">Hayır</span><span class="sxs-lookup"><span data-stu-id="d4e4b-225">No</span></span> |
| <span data-ttu-id="d4e4b-226">rejectType</span><span class="sxs-lookup"><span data-stu-id="d4e4b-226">rejectType</span></span> |<span data-ttu-id="d4e4b-227">RejectValue seçeneği bir hazır değer veya bir yüzde belirtilen belirtir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-227">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="d4e4b-228">Değer (varsayılan), yüzde</span><span class="sxs-lookup"><span data-stu-id="d4e4b-228">Value (default), Percentage</span></span> |<span data-ttu-id="d4e4b-229">Hayır</span><span class="sxs-lookup"><span data-stu-id="d4e4b-229">No</span></span> |
| <span data-ttu-id="d4e4b-230">Havuzu'na ilişkin</span><span class="sxs-lookup"><span data-stu-id="d4e4b-230">rejectSampleValue</span></span> |<span data-ttu-id="d4e4b-231">PolyBase reddedilen satırları yüzdesini yeniden hesaplar önce almak için satır sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-231">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="d4e4b-232">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="d4e4b-232">1, 2, …</span></span> |<span data-ttu-id="d4e4b-233">Evet, varsa **rejectType** olan **yüzdesi**</span><span class="sxs-lookup"><span data-stu-id="d4e4b-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="d4e4b-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="d4e4b-234">useTypeDefault</span></span> |<span data-ttu-id="d4e4b-235">PolyBase metin dosyasından veri aldığında sınırlandırılmış metin dosyaları eksik değerleri nasıl ele alınacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-235">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="d4e4b-236">Bağımsız değişkenler bölümünde bu özelliği hakkında daha fazla bilgi [oluşturma EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-236">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="d4e4b-237">TRUE, False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="d4e4b-237">True, False (default)</span></span> |<span data-ttu-id="d4e4b-238">Hayır</span><span class="sxs-lookup"><span data-stu-id="d4e4b-238">No</span></span> |
| <span data-ttu-id="d4e4b-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="d4e4b-239">writeBatchSize</span></span> |<span data-ttu-id="d4e4b-240">Arabellek boyutu writeBatchSize ulaştığında veri SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-240">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="d4e4b-241">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="d4e4b-241">Integer (number of rows)</span></span> |<span data-ttu-id="d4e4b-242">Hayır (varsayılan: 10000)</span><span class="sxs-lookup"><span data-stu-id="d4e4b-242">No (default: 10000)</span></span> |
| <span data-ttu-id="d4e4b-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="d4e4b-243">writeBatchTimeout</span></span> |<span data-ttu-id="d4e4b-244">Toplu ekleme işlemi zaman aşımına uğramadan önce tamamlamak bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-244">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="d4e4b-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="d4e4b-245">timespan</span></span><br/><br/> <span data-ttu-id="d4e4b-246">Örnek: "00: 30:00" (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="d4e4b-247">Hayır</span><span class="sxs-lookup"><span data-stu-id="d4e4b-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="d4e4b-248">SqlDWSink örneği</span><span class="sxs-lookup"><span data-stu-id="d4e4b-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-to-load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="d4e4b-249">Azure SQL Data Warehouse'a veri yüklemek için Polybase'i kullanın</span><span class="sxs-lookup"><span data-stu-id="d4e4b-249">Use PolyBase to load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d4e4b-250">Kullanarak  **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)**  büyük miktarda veri yüksek işleme ile Azure SQL Data Warehouse'a veri yükleme etkili bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="d4e4b-251">PolyBase yerine varsayılan BULKINSERT mekanizmasını kullanarak büyük kazanç verimliliği de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-251">You can see a large gain in the throughput by using PolyBase instead of the default BULKINSERT mechanism.</span></span> <span data-ttu-id="d4e4b-252">Bkz: [kopyalama performans başvuru numarası](data-factory-copy-activity-performance.md#performance-reference) ayrıntılı karşılaştırması ile.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="d4e4b-253">Kullanım örneği ile bir anlatım için bkz: [1 TB altında 15 dakika Azure Data Factory ile Azure SQL Data Warehouse'a veri yükleme](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="d4e4b-254">Veri kaynağınızı ise **Azure Blob veya Azure Data Lake Store**ve biçimini PolyBase ile uyumlu ise, doğrudan Azure SQL veri Polybase'i kullanarak ambarına kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and the format is compatible with PolyBase, you can directly copy to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="d4e4b-255">Bkz:  **[Polybase'i kullanarak doğrudan kopyalama](#direct-copy-using-polybase)**  ayrıntılarla.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="d4e4b-256">Kaynak veri deposu ve biçim başlangıçta desteklenmiyor, PolyBase tarafından kullanabileceğiniz  **[Polybase'i kullanarak kopyalama hazırlanan](#staged-copy-using-polybase)**  yerine özellik.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-256">If your source data store and format is not originally supported by PolyBase, you can use the **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="d4e4b-257">Ayrıca, daha iyi verim otomatik olarak veri PolyBase uyumlu biçimine dönüştürmek için kullanılan ve Azure Blob depolama alanına veri depolayarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-257">It also provides you better throughput by automatically converting the data into PolyBase-compatible format and storing the data in Azure Blob storage.</span></span> <span data-ttu-id="d4e4b-258">Ardından verileri SQL Data Warehouse'a veri yükler.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="d4e4b-259">Ayarlama `allowPolyBase` özelliğine **true** Azure SQL Data Warehouse'a veri kopyalamak için PolyBase kullanmak Azure Data Factory için aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-259">Set the `allowPolyBase` property to **true** as shown in the following example for Azure Data Factory to use PolyBase to copy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d4e4b-260">Bulunan'allowpolybase true olarak ayarladığınızda, kullanarak PolyBase belirli özelliklerini belirtebilirsiniz `polyBaseSettings` özellik grubu.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-260">When you set allowPolyBase to true, you can specify PolyBase specific properties using the `polyBaseSettings` property group.</span></span> <span data-ttu-id="d4e4b-261">bkz: [SqlDWSink](#SqlDWSink) polyBaseSettings ile kullanabileceğiniz özellikleri hakkında ayrıntılı bilgi için bölüm.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-261">see the [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="d4e4b-262">Polybase'i kullanarak doğrudan kopyalama</span><span class="sxs-lookup"><span data-stu-id="d4e4b-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="d4e4b-263">SQL veri ambarı PolyBase doğrudan desteği Azure Blob ve Azure Data Lake Store (hizmet sorumlusu kullanarak) kaynak olarak ve belirli dosya biçimi gereksinimleriyle.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="d4e4b-264">Veri kaynağınızı Bu bölümde açıklanan ölçütlerini karşılıyorsa, kaynak veri deposundan doğrudan Azure SQL veri Polybase'i kullanarak ambarına kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-264">If your source data meets the criteria described in this section, you can directly copy from source data store to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="d4e4b-265">Aksi takdirde, kullanabileceğiniz [Polybase'i kullanarak kopyalama hazırlanan](#staged-copy-using-polybase).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="d4e4b-266">Verimli bir şekilde SQL veri ambarı için verileri Data Lake Deposu'ndan veri kopyalamak için'dan daha fazla bilgi edinin [Azure Data Factory sağlar, bu, daha kolay ve Data Lake Store ile SQL veri ambarı kullanırken verilerden Öngörüler ortaya çıkarmak uygun bile](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-266">To copy data from Data Lake Store to SQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient to uncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="d4e4b-267">Gereksinimler karşılanmazsa, Azure Data Factory ayarları denetler ve veri taşıma için BULKINSERT mekanizması için otomatik olarak geri döner.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-267">If the requirements are not met, Azure Data Factory checks the settings and automatically falls back to the BULKINSERT mechanism for the data movement.</span></span>

1. <span data-ttu-id="d4e4b-268">**Kaynak bağlantılı hizmeti** türüdür: **AzureStorage** veya **AzureDataLakeStore hizmet asıl kimlik doğrulaması ile**.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="d4e4b-269">**Girdi veri kümesi** türüdür: **AzureBlob** veya **AzureDataLakeStore**ve altında yazın biçimi `type` özellikleri **OrcFormat**, veya **TextFormat** aşağıdaki yapılandırmalara sahip:</span><span class="sxs-lookup"><span data-stu-id="d4e4b-269">The **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and the format type under `type` properties is **OrcFormat**, or **TextFormat** with the following configurations:</span></span>

   1. <span data-ttu-id="d4e4b-270">`rowDelimiter`olmalıdır  **\n** .</span><span class="sxs-lookup"><span data-stu-id="d4e4b-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="d4e4b-271">`nullValue`ayarlanmış **boş dize** (""), veya `treatEmptyAsNull` ayarlanır **doğru**.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-271">`nullValue` is set to **empty string** (""), or `treatEmptyAsNull` is set to **true**.</span></span>
   3. <span data-ttu-id="d4e4b-272">`encodingName`ayarlanmış **utf-8**, olduğu **varsayılan** değeri.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-272">`encodingName` is set to **utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="d4e4b-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, ve `skipLineCount` belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="d4e4b-274">`compression`olabilir **sıkıştırma yok**, **GZip**, veya **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. <span data-ttu-id="d4e4b-275">Yoktur hiçbir `skipHeaderLineCount` altında ayarı **BlobSource** veya **AzureDataLakeStore** işlem hattının kopyalama etkinliği için.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for the Copy activity in the pipeline.</span></span>
4. <span data-ttu-id="d4e4b-276">Var olan hiçbir `sliceIdentifierColumnName` altında ayarlama **SqlDWSink** işlem hattının kopyalama etkinliği için.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for the Copy activity in the pipeline.</span></span> <span data-ttu-id="d4e4b-277">(Tüm veriler güncelleştirilir veya hiçbir şey bir tek çalıştırmada güncelleştirildiğinde PolyBase garanti eder.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="d4e4b-278">Elde etmek için **Yinelenebilirlik**, kullanabileceğinizi `sqlWriterCleanupScript`).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-278">To achieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="d4e4b-279">Yoktur hiçbir `columnMapping` ilişkili kopya kullanılan etkinlik.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-279">There is no `columnMapping` being used in the associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="d4e4b-280">Polybase'i kullanarak hazırlanmış kopyalama</span><span class="sxs-lookup"><span data-stu-id="d4e4b-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="d4e4b-281">Veri kaynağınızı önceki bölümde sunulan ölçütlere uyan değil, bir geçici hazırlama Azure Blob (Premium depolama olamaz) depolama aracılığıyla veri kopyalamayı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-281">When your source data doesn’t meet the criteria introduced in the previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="d4e4b-282">Bu durumda, Azure Data Factory otomatik olarak dönüşümleri PolyBase veri biçimi gereksinimlerini karşılamak ve ardından verileri SQL veri ambarında ve son temizlemenin yüklemek için Polybase'i kullanın veri, geçici veriler Blob depolama alanından gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-282">In this case, Azure Data Factory automatically performs transformations on the data to meet data format requirements of PolyBase, then use PolyBase to load data into SQL Data Warehouse, and at last clean-up your temp data from the Blob storage.</span></span> <span data-ttu-id="d4e4b-283">Bkz: [hazırlanan kopyalama](data-factory-copy-activity-performance.md#staged-copy) nasıl hazırlama Azure Blob üzerinden veri kopyalama genel çalıştığı hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="d4e4b-284">Ne zaman Azure SQL Data Polybase'i kullanarak Warehouse'a bir şirket içi veri kopyalama verileri depolamak ve hazırlama, veri yönetimi ağ geçidi sürümü 2.4 ise, JRE (Java Çalışma zamanı ortamı) ağ geçidi makinenizde veri kaynağınızı dönüştürmek için kullanılan gereklidir doğru biçime.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used to transform your source data into proper format.</span></span> <span data-ttu-id="d4e4b-285">Bu bağımlılık önlemek için ağ geçidinizi en son yükseltmeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-285">Suggest you upgrade your gateway to the latest to avoid such dependency.</span></span>
>

<span data-ttu-id="d4e4b-286">Bu özelliği kullanmak için oluşturma bir [Azure depolama bağlantılı hizmeti](data-factory-azure-blob-connector.md#azure-storage-linked-service) Ara blob depolama alanına sahip Azure depolama hesabı anlamına gelir, sonra belirtin `enableStaging` ve `stagingSettings` kopyalama gösterildiği gibi etkinliğin özellikleri Aşağıdaki kod:</span><span class="sxs-lookup"><span data-stu-id="d4e4b-286">To use this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers to the Azure Storage Account that has the interim blob storage, then specify the `enableStaging` and `stagingSettings` properties for the Copy Activity as shown in the following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server to SQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="d4e4b-287">PolyBase kullanırken en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="d4e4b-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="d4e4b-288">Aşağıdaki bölümlerde bölümünde belirtildiği olanlara ek en iyi yöntemleri sağlamak [en iyi uygulamalar Azure SQL Data Warehouse için](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-288">The following sections provide additional best practices to the ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="d4e4b-289">Gerekli veritabanı izni</span><span class="sxs-lookup"><span data-stu-id="d4e4b-289">Required database permission</span></span>
<span data-ttu-id="d4e4b-290">PolyBase kullanmak için SQL Data Warehouse'a veri yükleme için kullanılan kullanıcı gerektiriyor ["Denetim" izni](https://msdn.microsoft.com/library/ms191291.aspx) hedef veritabanı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-290">To use PolyBase, it requires the user being used to load data into SQL Data Warehouse has the ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on the target database.</span></span> <span data-ttu-id="d4e4b-291">Elde etmenin bir yolu, "db_owner" rolünün bir üyesi o kullanıcı eklemektir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-291">One way to achieve that is to add that user as a member of "db_owner" role.</span></span> <span data-ttu-id="d4e4b-292">Aşağıdaki kullanarak bunu öğrenin [Bu bölümde](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-292">Learn how to do that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="d4e4b-293">Satır boyutu ve verileri sınırlama yazın</span><span class="sxs-lookup"><span data-stu-id="d4e4b-293">Row size and data type limitation</span></span>
<span data-ttu-id="d4e4b-294">Polybase yükleri sınırlı yükleme satırları hem küçük **1 MB** ve VARCHR(MAX), NVARCHAR(MAX) veya VARBINARY(MAX) yüklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-294">Polybase loads are limited to loading rows both smaller than **1 MB** and cannot load to VARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="d4e4b-295">Başvurmak [burada](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-295">Refer to [here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="d4e4b-296">Kaynak verileri satır boyutu 1 MB'tan fazla ile varsa, kaynak tabloları dikey Burada bunların her biri en büyük satır boyutu sınırı aşmadığından birkaç küçük parçalara bölmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-296">If you have source data with rows of size greater than 1 MB, you may want to split the source tables vertically into several small ones where the largest row size of each of them does not exceed the limit.</span></span> <span data-ttu-id="d4e4b-297">Daha küçük tabloları sonra PolyBase kullanarak yüklenebilir ve Azure SQL Data Warehouse'da birleştirmeniz.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-297">The smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="d4e4b-298">SQL veri ambarı kaynak sınıfı</span><span class="sxs-lookup"><span data-stu-id="d4e4b-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="d4e4b-299">Olası en iyi verime ulaşmak için PolyBase aracılığıyla SQL veri ambarında verileri yüklemek için kullanılan kullanıcı büyük kaynak sınıfı atamak için göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-299">To achieve best possible throughput, consider to assign larger resource class to the user being used to load data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="d4e4b-300">Aşağıdaki kullanarak bunu öğrenin [kullanıcı kaynak sınıfı örneğini değiştirmek](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-300">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="d4e4b-301">Azure SQL Data Warehouse tableName</span><span class="sxs-lookup"><span data-stu-id="d4e4b-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d4e4b-302">Aşağıdaki tabloda belirleme konusunda örnekler **tableName** dataset JSON çeşitli şema ve tablo adı için bir özellik.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-302">The following table provides examples on how to specify the **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="d4e4b-303">DB şeması</span><span class="sxs-lookup"><span data-stu-id="d4e4b-303">DB Schema</span></span> | <span data-ttu-id="d4e4b-304">Tablo adı</span><span class="sxs-lookup"><span data-stu-id="d4e4b-304">Table name</span></span> | <span data-ttu-id="d4e4b-305">tableName JSON özelliği</span><span class="sxs-lookup"><span data-stu-id="d4e4b-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4e4b-306">dbo</span><span class="sxs-lookup"><span data-stu-id="d4e4b-306">dbo</span></span> |<span data-ttu-id="d4e4b-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="d4e4b-307">MyTable</span></span> |<span data-ttu-id="d4e4b-308">MyTable ya da dbo. MyTable ya da [dbo]. [MyTable]</span><span class="sxs-lookup"><span data-stu-id="d4e4b-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="d4e4b-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="d4e4b-309">dbo1</span></span> |<span data-ttu-id="d4e4b-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="d4e4b-310">MyTable</span></span> |<span data-ttu-id="d4e4b-311">dbo1. MyTable veya [dbo1]. [MyTable]</span><span class="sxs-lookup"><span data-stu-id="d4e4b-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="d4e4b-312">dbo</span><span class="sxs-lookup"><span data-stu-id="d4e4b-312">dbo</span></span> |<span data-ttu-id="d4e4b-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="d4e4b-313">My.Table</span></span> |<span data-ttu-id="d4e4b-314">[My.Table] veya [dbo]. [My.Table]</span><span class="sxs-lookup"><span data-stu-id="d4e4b-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="d4e4b-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="d4e4b-315">dbo1</span></span> |<span data-ttu-id="d4e4b-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="d4e4b-316">My.Table</span></span> |<span data-ttu-id="d4e4b-317">[dbo1]. [My.Table]</span><span class="sxs-lookup"><span data-stu-id="d4e4b-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="d4e4b-318">Aşağıdaki hata görürseniz, tableName özelliği için belirtilen değer ile ilgili bir sorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-318">If you see the following error, it could be an issue with the value you specified for the tableName property.</span></span> <span data-ttu-id="d4e4b-319">TableName JSON özellik değerlerini belirtmek doğru bir şekilde için tabloya bakın.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-319">See the table for the correct way to specify values for the tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="d4e4b-320">Varsayılan değerleri içeren sütun</span><span class="sxs-lookup"><span data-stu-id="d4e4b-320">Columns with default values</span></span>
<span data-ttu-id="d4e4b-321">Şu anda, veri fabrikası'nda PolyBase özelliği yalnızca aynı sayıda sütun hedef tabloda olduğu gibi kabul eder.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-321">Currently, PolyBase feature in Data Factory only accepts the same number of columns as in the target table.</span></span> <span data-ttu-id="d4e4b-322">Dört sütun içeren bir tablo varsa ve bunlardan birini varsayılan bir değerle tanımlanan söyleyin.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="d4e4b-323">Giriş verisi hala dört sütun içermelidir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-323">The input data should still contain four columns.</span></span> <span data-ttu-id="d4e4b-324">3-sütun girdi veri kümesi sağlayan aşağıdaki iletiye benzer bir hata verir:</span><span class="sxs-lookup"><span data-stu-id="d4e4b-324">Providing a 3-column input dataset would yield an error similar to the following message:</span></span>

```
All columns of the table must be specified in the INSERT BULK statement.
```
<span data-ttu-id="d4e4b-325">NULL değer, varsayılan değeri özel bir biçimidir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="d4e4b-326">Sütun null ise girdi verilerini (blob) Bu sütun için boş olabilir (giriş kümesinden eksik olamaz).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-326">If the column is nullable, the input data (in blob) for that column could be empty (cannot be missing from the input dataset).</span></span> <span data-ttu-id="d4e4b-327">PolyBase, Azure SQL Data Warehouse bunları NULL ekler.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-327">PolyBase inserts NULL for them in the Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="d4e4b-328">Otomatik Tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4e4b-328">Auto table creation</span></span>
<span data-ttu-id="d4e4b-329">Azure SQL Data Warehouse için SQL Server veya Azure SQL veritabanına veri kopyalamak için kopyalama Sihirbazı'nı kullanıyorsanız ve kaynak tablosunda karşılık gelen tablosu hedef deposunda mevcut değil, veri fabrikası otomatik olarak tablo veri ambarında u tarafından oluşturabilirsiniz Kaynak tablo şemasını kaydolur.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-329">If you are using Copy Wizard to copy data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse and the table that corresponds to the source table does not exist in the destination store, Data Factory can automatically create the table in the data warehouse by using the source table schema.</span></span>

<span data-ttu-id="d4e4b-330">Veri Fabrikası aynı tablo adı kaynak veri deposundaki ile hedef deposunda bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-330">Data Factory creates the table in the destination store with the same table name in the source data store.</span></span> <span data-ttu-id="d4e4b-331">Sütun veri türleri aşağıdaki tür eşlemesi göre seçilir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-331">The data types for columns are chosen based on the following type mapping.</span></span> <span data-ttu-id="d4e4b-332">Gerekli olursa, kaynak ve hedef depoları arasında uyumsuzlukları düzeltmek için tür dönüşümleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-332">If needed, it performs type conversions to fix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="d4e4b-333">Ayrıca, hepsini bir kez Tablo dağıtım kullanır.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="d4e4b-334">Kaynak SQL veritabanı sütun türü</span><span class="sxs-lookup"><span data-stu-id="d4e4b-334">Source SQL Database column type</span></span> | <span data-ttu-id="d4e4b-335">Hedef SQL DW sütun türü (boyutu kısıtlaması)</span><span class="sxs-lookup"><span data-stu-id="d4e4b-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="d4e4b-336">Int</span><span class="sxs-lookup"><span data-stu-id="d4e4b-336">Int</span></span> | <span data-ttu-id="d4e4b-337">Int</span><span class="sxs-lookup"><span data-stu-id="d4e4b-337">Int</span></span> |
| <span data-ttu-id="d4e4b-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="d4e4b-338">BigInt</span></span> | <span data-ttu-id="d4e4b-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="d4e4b-339">BigInt</span></span> |
| <span data-ttu-id="d4e4b-340">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="d4e4b-340">SmallInt</span></span> | <span data-ttu-id="d4e4b-341">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="d4e4b-341">SmallInt</span></span> |
| <span data-ttu-id="d4e4b-342">Mini tamsayı</span><span class="sxs-lookup"><span data-stu-id="d4e4b-342">TinyInt</span></span> | <span data-ttu-id="d4e4b-343">Mini tamsayı</span><span class="sxs-lookup"><span data-stu-id="d4e4b-343">TinyInt</span></span> |
| <span data-ttu-id="d4e4b-344">bit</span><span class="sxs-lookup"><span data-stu-id="d4e4b-344">Bit</span></span> | <span data-ttu-id="d4e4b-345">bit</span><span class="sxs-lookup"><span data-stu-id="d4e4b-345">Bit</span></span> |
| <span data-ttu-id="d4e4b-346">Ondalık</span><span class="sxs-lookup"><span data-stu-id="d4e4b-346">Decimal</span></span> | <span data-ttu-id="d4e4b-347">Ondalık</span><span class="sxs-lookup"><span data-stu-id="d4e4b-347">Decimal</span></span> |
| <span data-ttu-id="d4e4b-348">sayısal</span><span class="sxs-lookup"><span data-stu-id="d4e4b-348">Numeric</span></span> | <span data-ttu-id="d4e4b-349">Ondalık</span><span class="sxs-lookup"><span data-stu-id="d4e4b-349">Decimal</span></span> |
| <span data-ttu-id="d4e4b-350">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="d4e4b-350">Float</span></span> | <span data-ttu-id="d4e4b-351">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="d4e4b-351">Float</span></span> |
| <span data-ttu-id="d4e4b-352">para</span><span class="sxs-lookup"><span data-stu-id="d4e4b-352">Money</span></span> | <span data-ttu-id="d4e4b-353">para</span><span class="sxs-lookup"><span data-stu-id="d4e4b-353">Money</span></span> |
| <span data-ttu-id="d4e4b-354">Real</span><span class="sxs-lookup"><span data-stu-id="d4e4b-354">Real</span></span> | <span data-ttu-id="d4e4b-355">Real</span><span class="sxs-lookup"><span data-stu-id="d4e4b-355">Real</span></span> |
| <span data-ttu-id="d4e4b-356">Küçük para</span><span class="sxs-lookup"><span data-stu-id="d4e4b-356">SmallMoney</span></span> | <span data-ttu-id="d4e4b-357">Küçük para</span><span class="sxs-lookup"><span data-stu-id="d4e4b-357">SmallMoney</span></span> |
| <span data-ttu-id="d4e4b-358">İkili</span><span class="sxs-lookup"><span data-stu-id="d4e4b-358">Binary</span></span> | <span data-ttu-id="d4e4b-359">İkili</span><span class="sxs-lookup"><span data-stu-id="d4e4b-359">Binary</span></span> |
| <span data-ttu-id="d4e4b-360">varbinary</span><span class="sxs-lookup"><span data-stu-id="d4e4b-360">Varbinary</span></span> | <span data-ttu-id="d4e4b-361">Varbinary (en fazla 8000)</span><span class="sxs-lookup"><span data-stu-id="d4e4b-361">Varbinary (up to 8000)</span></span> |
| <span data-ttu-id="d4e4b-362">Tarih</span><span class="sxs-lookup"><span data-stu-id="d4e4b-362">Date</span></span> | <span data-ttu-id="d4e4b-363">Tarih</span><span class="sxs-lookup"><span data-stu-id="d4e4b-363">Date</span></span> |
| <span data-ttu-id="d4e4b-364">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="d4e4b-364">DateTime</span></span> | <span data-ttu-id="d4e4b-365">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="d4e4b-365">DateTime</span></span> |
| <span data-ttu-id="d4e4b-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="d4e4b-366">DateTime2</span></span> | <span data-ttu-id="d4e4b-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="d4e4b-367">DateTime2</span></span> |
| <span data-ttu-id="d4e4b-368">Zaman</span><span class="sxs-lookup"><span data-stu-id="d4e4b-368">Time</span></span> | <span data-ttu-id="d4e4b-369">Zaman</span><span class="sxs-lookup"><span data-stu-id="d4e4b-369">Time</span></span> |
| <span data-ttu-id="d4e4b-370">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="d4e4b-370">DateTimeOffset</span></span> | <span data-ttu-id="d4e4b-371">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="d4e4b-371">DateTimeOffset</span></span> |
| <span data-ttu-id="d4e4b-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="d4e4b-372">SmallDateTime</span></span> | <span data-ttu-id="d4e4b-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="d4e4b-373">SmallDateTime</span></span> |
| <span data-ttu-id="d4e4b-374">Metin</span><span class="sxs-lookup"><span data-stu-id="d4e4b-374">Text</span></span> | <span data-ttu-id="d4e4b-375">VARCHAR (en fazla 8000)</span><span class="sxs-lookup"><span data-stu-id="d4e4b-375">Varchar (up to 8000)</span></span> |
| <span data-ttu-id="d4e4b-376">NText</span><span class="sxs-lookup"><span data-stu-id="d4e4b-376">NText</span></span> | <span data-ttu-id="d4e4b-377">NVarChar (en fazla 4000)</span><span class="sxs-lookup"><span data-stu-id="d4e4b-377">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="d4e4b-378">Görüntü</span><span class="sxs-lookup"><span data-stu-id="d4e4b-378">Image</span></span> | <span data-ttu-id="d4e4b-379">VarBinary (en fazla 8000)</span><span class="sxs-lookup"><span data-stu-id="d4e4b-379">VarBinary (up to 8000)</span></span> |
| <span data-ttu-id="d4e4b-380">Benzersiz tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="d4e4b-380">UniqueIdentifier</span></span> | <span data-ttu-id="d4e4b-381">Benzersiz tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="d4e4b-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="d4e4b-382">char</span><span class="sxs-lookup"><span data-stu-id="d4e4b-382">Char</span></span> | <span data-ttu-id="d4e4b-383">char</span><span class="sxs-lookup"><span data-stu-id="d4e4b-383">Char</span></span> |
| <span data-ttu-id="d4e4b-384">NChar</span><span class="sxs-lookup"><span data-stu-id="d4e4b-384">NChar</span></span> | <span data-ttu-id="d4e4b-385">NChar</span><span class="sxs-lookup"><span data-stu-id="d4e4b-385">NChar</span></span> |
| <span data-ttu-id="d4e4b-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="d4e4b-386">VarChar</span></span> | <span data-ttu-id="d4e4b-387">VarChar (en fazla 8000)</span><span class="sxs-lookup"><span data-stu-id="d4e4b-387">VarChar (up to 8000)</span></span> |
| <span data-ttu-id="d4e4b-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="d4e4b-388">NVarChar</span></span> | <span data-ttu-id="d4e4b-389">NVarChar (en fazla 4000)</span><span class="sxs-lookup"><span data-stu-id="d4e4b-389">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="d4e4b-390">XML</span><span class="sxs-lookup"><span data-stu-id="d4e4b-390">Xml</span></span> | <span data-ttu-id="d4e4b-391">VARCHAR (en fazla 8000)</span><span class="sxs-lookup"><span data-stu-id="d4e4b-391">Varchar (up to 8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="d4e4b-392">Tür eşlemesi için Azure SQL veri ambarı</span><span class="sxs-lookup"><span data-stu-id="d4e4b-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d4e4b-393">Bölümünde belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopya etkinliği aşağıdaki 2 adımlı yaklaşımı türleriyle havuz için kaynak türünden otomatik tür dönüşümleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="d4e4b-393">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="d4e4b-394">Yerel kaynak türlerinden .NET türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="d4e4b-394">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="d4e4b-395">.NET türünden yerel havuz türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="d4e4b-395">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="d4e4b-396">& Azure SQL veri ambarından veri taşıma olduğunda, aşağıdaki eşlemelerini SQL türü .NET türü ve tersi yönde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-396">When moving data to & from Azure SQL Data Warehouse, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="d4e4b-397">Eşleme aynı [ADO.NET için SQL Server veri türü eşlemesi](https://msdn.microsoft.com/library/cc716729.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-397">The mapping is same as the [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="d4e4b-398">SQL Server veritabanı altyapısı türü</span><span class="sxs-lookup"><span data-stu-id="d4e4b-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="d4e4b-399">.NET framework türü</span><span class="sxs-lookup"><span data-stu-id="d4e4b-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="d4e4b-400">bigint</span><span class="sxs-lookup"><span data-stu-id="d4e4b-400">bigint</span></span> |<span data-ttu-id="d4e4b-401">Int64</span><span class="sxs-lookup"><span data-stu-id="d4e4b-401">Int64</span></span> |
| <span data-ttu-id="d4e4b-402">İkili</span><span class="sxs-lookup"><span data-stu-id="d4e4b-402">binary</span></span> |<span data-ttu-id="d4e4b-403">Byte]</span><span class="sxs-lookup"><span data-stu-id="d4e4b-403">Byte[]</span></span> |
| <span data-ttu-id="d4e4b-404">bit</span><span class="sxs-lookup"><span data-stu-id="d4e4b-404">bit</span></span> |<span data-ttu-id="d4e4b-405">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="d4e4b-405">Boolean</span></span> |
| <span data-ttu-id="d4e4b-406">char</span><span class="sxs-lookup"><span data-stu-id="d4e4b-406">char</span></span> |<span data-ttu-id="d4e4b-407">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="d4e4b-407">String, Char[]</span></span> |
| <span data-ttu-id="d4e4b-408">Tarih</span><span class="sxs-lookup"><span data-stu-id="d4e4b-408">date</span></span> |<span data-ttu-id="d4e4b-409">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="d4e4b-409">DateTime</span></span> |
| <span data-ttu-id="d4e4b-410">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="d4e4b-410">Datetime</span></span> |<span data-ttu-id="d4e4b-411">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="d4e4b-411">DateTime</span></span> |
| <span data-ttu-id="d4e4b-412">datetime2</span><span class="sxs-lookup"><span data-stu-id="d4e4b-412">datetime2</span></span> |<span data-ttu-id="d4e4b-413">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="d4e4b-413">DateTime</span></span> |
| <span data-ttu-id="d4e4b-414">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="d4e4b-414">Datetimeoffset</span></span> |<span data-ttu-id="d4e4b-415">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="d4e4b-415">DateTimeOffset</span></span> |
| <span data-ttu-id="d4e4b-416">Ondalık</span><span class="sxs-lookup"><span data-stu-id="d4e4b-416">Decimal</span></span> |<span data-ttu-id="d4e4b-417">Ondalık</span><span class="sxs-lookup"><span data-stu-id="d4e4b-417">Decimal</span></span> |
| <span data-ttu-id="d4e4b-418">FILESTREAM özniteliği (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="d4e4b-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="d4e4b-419">Byte]</span><span class="sxs-lookup"><span data-stu-id="d4e4b-419">Byte[]</span></span> |
| <span data-ttu-id="d4e4b-420">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="d4e4b-420">Float</span></span> |<span data-ttu-id="d4e4b-421">Çift</span><span class="sxs-lookup"><span data-stu-id="d4e4b-421">Double</span></span> |
| <span data-ttu-id="d4e4b-422">Görüntü</span><span class="sxs-lookup"><span data-stu-id="d4e4b-422">image</span></span> |<span data-ttu-id="d4e4b-423">Byte]</span><span class="sxs-lookup"><span data-stu-id="d4e4b-423">Byte[]</span></span> |
| <span data-ttu-id="d4e4b-424">Int</span><span class="sxs-lookup"><span data-stu-id="d4e4b-424">int</span></span> |<span data-ttu-id="d4e4b-425">Int32</span><span class="sxs-lookup"><span data-stu-id="d4e4b-425">Int32</span></span> |
| <span data-ttu-id="d4e4b-426">para</span><span class="sxs-lookup"><span data-stu-id="d4e4b-426">money</span></span> |<span data-ttu-id="d4e4b-427">Ondalık</span><span class="sxs-lookup"><span data-stu-id="d4e4b-427">Decimal</span></span> |
| <span data-ttu-id="d4e4b-428">nchar</span><span class="sxs-lookup"><span data-stu-id="d4e4b-428">nchar</span></span> |<span data-ttu-id="d4e4b-429">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="d4e4b-429">String, Char[]</span></span> |
| <span data-ttu-id="d4e4b-430">ntext</span><span class="sxs-lookup"><span data-stu-id="d4e4b-430">ntext</span></span> |<span data-ttu-id="d4e4b-431">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="d4e4b-431">String, Char[]</span></span> |
| <span data-ttu-id="d4e4b-432">sayısal</span><span class="sxs-lookup"><span data-stu-id="d4e4b-432">numeric</span></span> |<span data-ttu-id="d4e4b-433">Ondalık</span><span class="sxs-lookup"><span data-stu-id="d4e4b-433">Decimal</span></span> |
| <span data-ttu-id="d4e4b-434">nvarchar</span><span class="sxs-lookup"><span data-stu-id="d4e4b-434">nvarchar</span></span> |<span data-ttu-id="d4e4b-435">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="d4e4b-435">String, Char[]</span></span> |
| <span data-ttu-id="d4e4b-436">Gerçek</span><span class="sxs-lookup"><span data-stu-id="d4e4b-436">real</span></span> |<span data-ttu-id="d4e4b-437">Tek</span><span class="sxs-lookup"><span data-stu-id="d4e4b-437">Single</span></span> |
| <span data-ttu-id="d4e4b-438">rowVersion</span><span class="sxs-lookup"><span data-stu-id="d4e4b-438">rowversion</span></span> |<span data-ttu-id="d4e4b-439">Byte]</span><span class="sxs-lookup"><span data-stu-id="d4e4b-439">Byte[]</span></span> |
| <span data-ttu-id="d4e4b-440">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="d4e4b-440">smalldatetime</span></span> |<span data-ttu-id="d4e4b-441">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="d4e4b-441">DateTime</span></span> |
| <span data-ttu-id="d4e4b-442">tamsayı</span><span class="sxs-lookup"><span data-stu-id="d4e4b-442">smallint</span></span> |<span data-ttu-id="d4e4b-443">Int16</span><span class="sxs-lookup"><span data-stu-id="d4e4b-443">Int16</span></span> |
| <span data-ttu-id="d4e4b-444">küçük para</span><span class="sxs-lookup"><span data-stu-id="d4e4b-444">smallmoney</span></span> |<span data-ttu-id="d4e4b-445">Ondalık</span><span class="sxs-lookup"><span data-stu-id="d4e4b-445">Decimal</span></span> |
| <span data-ttu-id="d4e4b-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="d4e4b-446">sql_variant</span></span> |<span data-ttu-id="d4e4b-447">Nesne *</span><span class="sxs-lookup"><span data-stu-id="d4e4b-447">Object *</span></span> |
| <span data-ttu-id="d4e4b-448">Metin</span><span class="sxs-lookup"><span data-stu-id="d4e4b-448">text</span></span> |<span data-ttu-id="d4e4b-449">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="d4e4b-449">String, Char[]</span></span> |
| <span data-ttu-id="d4e4b-450">time</span><span class="sxs-lookup"><span data-stu-id="d4e4b-450">time</span></span> |<span data-ttu-id="d4e4b-451">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="d4e4b-451">TimeSpan</span></span> |
| <span data-ttu-id="d4e4b-452">timestamp</span><span class="sxs-lookup"><span data-stu-id="d4e4b-452">timestamp</span></span> |<span data-ttu-id="d4e4b-453">Byte]</span><span class="sxs-lookup"><span data-stu-id="d4e4b-453">Byte[]</span></span> |
| <span data-ttu-id="d4e4b-454">Mini tamsayı</span><span class="sxs-lookup"><span data-stu-id="d4e4b-454">tinyint</span></span> |<span data-ttu-id="d4e4b-455">Bayt</span><span class="sxs-lookup"><span data-stu-id="d4e4b-455">Byte</span></span> |
| <span data-ttu-id="d4e4b-456">benzersiz tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="d4e4b-456">uniqueidentifier</span></span> |<span data-ttu-id="d4e4b-457">GUID</span><span class="sxs-lookup"><span data-stu-id="d4e4b-457">Guid</span></span> |
| <span data-ttu-id="d4e4b-458">varbinary</span><span class="sxs-lookup"><span data-stu-id="d4e4b-458">varbinary</span></span> |<span data-ttu-id="d4e4b-459">Byte]</span><span class="sxs-lookup"><span data-stu-id="d4e4b-459">Byte[]</span></span> |
| <span data-ttu-id="d4e4b-460">varchar</span><span class="sxs-lookup"><span data-stu-id="d4e4b-460">varchar</span></span> |<span data-ttu-id="d4e4b-461">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="d4e4b-461">String, Char[]</span></span> |
| <span data-ttu-id="d4e4b-462">xml</span><span class="sxs-lookup"><span data-stu-id="d4e4b-462">xml</span></span> |<span data-ttu-id="d4e4b-463">XML</span><span class="sxs-lookup"><span data-stu-id="d4e4b-463">Xml</span></span> |

<span data-ttu-id="d4e4b-464">Ayrıca havuz dataset kopyalama etkinliği tanımında sütunları kaynak kümesinden sütunları eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-464">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="d4e4b-465">Ayrıntılar için bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-to-and-from-sql-data-warehouse"></a><span data-ttu-id="d4e4b-466">JSON örnekleri ve SQL veri ambarından veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="d4e4b-466">JSON examples for copying data to and from SQL Data Warehouse</span></span>
<span data-ttu-id="d4e4b-467">Aşağıdaki örnekleri kullanarak bir işlem hattı oluşturmak için kullanabileceğiniz örnek JSON tanımları sağlar [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-467">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="d4e4b-468">Bunlar ve Azure SQL Data Warehouse ve Azure Blob Storage veri kopyalamak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-468">They show how to copy data to and from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="d4e4b-469">Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden herhangi birine belirtildiği havuzlarını kaynakları [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kopya etkinliği Azure Data Factory kullanarak.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-469">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-to-azure-blob"></a><span data-ttu-id="d4e4b-470">Örnek: Verilerini Azure SQL Data Warehouse Azure Blob</span><span class="sxs-lookup"><span data-stu-id="d4e4b-470">Example: Copy data from Azure SQL Data Warehouse to Azure Blob</span></span>
<span data-ttu-id="d4e4b-471">Örnek aşağıdaki Data Factory varlıklarını tanımlar:</span><span class="sxs-lookup"><span data-stu-id="d4e4b-471">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="d4e4b-472">Bağlı hizmet türü [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="d4e4b-473">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="d4e4b-474">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="d4e4b-475">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="d4e4b-476">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [SqlDWSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d4e4b-477">Örnek zaman serisi (saatlik, günlük, vs.) verileri Azure SQL veri ambarı veritabanındaki bir tablodan bir blobu saatte kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-477">The sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database to a blob every hour.</span></span> <span data-ttu-id="d4e4b-478">Bu örnekler kullanılan JSON özellikleri örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-478">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="d4e4b-479">**Azure SQL Data Warehouse bağlantılı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="d4e4b-479">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="d4e4b-480">**Azure Blob storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="d4e4b-480">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="d4e4b-481">**Azure SQL veri ambarı veri kümesi giriş:**</span><span class="sxs-lookup"><span data-stu-id="d4e4b-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="d4e4b-482">Örnek, Azure SQL Data Warehouse'da bir tablo "MyTable" oluşturulur ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-482">The sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="d4e4b-483">"Dış" ayarı: "true" bildirir Data Factory hizmetinin veri kümesi data factory dış ve veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-483">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="d4e4b-484">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="d4e4b-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="d4e4b-485">Veri her saat yeni bir bloba yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-485">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d4e4b-486">Blob klasör yolu dinamik işlenmekte olan dilim başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-486">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="d4e4b-487">Klasör yolu yıl, ay, gün ve saat bölümleri başlangıç saatini kullanır.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-487">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="d4e4b-488">**SqlDWSource ve BlobSink ardışık düzeninde etkinlik kopyalayın:**</span><span class="sxs-lookup"><span data-stu-id="d4e4b-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="d4e4b-489">Ardışık Düzen giriş ve çıkış veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-489">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="d4e4b-490">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **SqlDWSource** ve **havuz** türü ayarlanmış **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-490">In the pipeline JSON definition, the **source** type is set to **SqlDWSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="d4e4b-491">SQL sorgusu için belirtilen **SqlReaderQuery** özelliği veri kopyalamak için son bir saat içindeki seçer.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-491">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
> [!NOTE]
> <span data-ttu-id="d4e4b-492">Örnekte, **sqlReaderQuery** SqlDWSource için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-492">In the example, **sqlReaderQuery** is specified for the SqlDWSource.</span></span> <span data-ttu-id="d4e4b-493">Kopyalama etkinliği bu sorguyu veri almak için Azure SQL Data Warehouse kaynağına karşı çalışır.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-493">The Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>
>
> <span data-ttu-id="d4e4b-494">Alternatif olarak, bir saklı yordam belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (saklı yordam parametreleri alıyorsa).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-494">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="d4e4b-495">SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz JSON veri kümesi yapısı bölümünde tanımlanan sütunları Azure SQL veri ambarına karşı çalıştırmak için bir sorgu (select column1, column2 mytable gelen) oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (select column1, column2 from mytable) to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d4e4b-496">Veri kümesi tanımı yapısına sahip değilse, tüm sütunları tablodan seçilir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-496">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-data-warehouse"></a><span data-ttu-id="d4e4b-497">Örnek: verileri Azure Blob'tan Azure SQL veri ambarı'na kopyalama</span><span class="sxs-lookup"><span data-stu-id="d4e4b-497">Example: Copy data from Azure Blob to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d4e4b-498">Örnek aşağıdaki Data Factory varlıklarını tanımlar:</span><span class="sxs-lookup"><span data-stu-id="d4e4b-498">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="d4e4b-499">Bağlı hizmet türü [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="d4e4b-500">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="d4e4b-501">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="d4e4b-502">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="d4e4b-503">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) ve [SqlDWSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="d4e4b-504">Zaman serisi Azure SQL Data Warehouse tablosuna verilerden (saatlik, günlük, vb.) Azure blob örnek kopyaları saatte veritabanı.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-504">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="d4e4b-505">Bu örnekler kullanılan JSON özellikleri örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-505">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="d4e4b-506">**Azure SQL Data Warehouse bağlantılı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="d4e4b-506">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="d4e4b-507">**Azure Blob storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="d4e4b-507">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="d4e4b-508">**Azure Blob girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="d4e4b-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="d4e4b-509">Veri toplanma yeni blob üzerinden saatte (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="d4e4b-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d4e4b-510">Blob klasör yolu ve dosya adı dinamik olarak değerlendirilir işleniyor dilim başlangıç zamanı temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-510">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="d4e4b-511">Klasör yolu yıl, ay ve gün kısmını başlangıç saati ve dosya adı başlangıç zamanı saat bölümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-511">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="d4e4b-512">"dış": "true" ayarı Bu tablo veri fabrikası dış ve veri fabrikasında bir etkinlik tarafından üretilen değil Data Factory hizmetinin sizi bilgilendirir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-512">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="d4e4b-513">**Azure SQL veri ambarı veri kümesi çıkışını:**</span><span class="sxs-lookup"><span data-stu-id="d4e4b-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="d4e4b-514">Örnek verileri Azure SQL Data Warehouse "MyTable" adlı bir tablo kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-514">The sample copies data to a table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d4e4b-515">Blob CSV dosyasında içerecek şekilde beklediğiniz gibi tablo Azure SQL Data Warehouse ile aynı sayıda sütun oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-515">Create the table in Azure SQL Data Warehouse with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="d4e4b-516">Yeni satırlar tabloya saatte eklenir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-516">New rows are added to the table every hour.</span></span>

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="d4e4b-517">**BlobSource ve SqlDWSink ardışık düzeninde etkinlik kopyalayın:**</span><span class="sxs-lookup"><span data-stu-id="d4e4b-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="d4e4b-518">Ardışık Düzen giriş ve çıkış veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-518">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="d4e4b-519">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **BlobSource** ve **havuz** türü ayarlanmış **SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-519">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlDWSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
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
<span data-ttu-id="d4e4b-520">İçin bkz: bkz [1 TB altında 15 dakika Azure Data Factory ile Azure SQL Data Warehouse'a veri yükleme](data-factory-load-sql-data-warehouse.md) ve [Azure Data Factory ile veri yükleme](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) makale Azure SQL Data Warehouse belgelerinde.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-520">For a walkthrough, see the see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in the Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="d4e4b-521">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="d4e4b-521">Performance and Tuning</span></span>
<span data-ttu-id="d4e4b-522">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve onu en iyi duruma getirmek için çeşitli yollar etkisi performansını anahtar Etkenler hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="d4e4b-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
