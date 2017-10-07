---
title: Azure SQL Data Warehouse/aaaCopy verileri | Microsoft Docs
description: "Bilgi nasıl/Azure Data Factory kullanarak Azure SQL Data Warehouse toocopy verileri"
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
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="bd702-103">Azure Data Factory kullanarak Azure SQL veri ambarından veri tooand Kopyala</span><span class="sxs-lookup"><span data-stu-id="bd702-103">Copy data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="bd702-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri öğesine/öğesinden Azure SQL Data Warehouse açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="bd702-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="bd702-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="bd702-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="bd702-106">tooachieve en iyi performans için Azure SQL Data Warehouse'a PolyBase tooload verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd702-106">tooachieve best performance, use PolyBase tooload data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="bd702-107">Merhaba [kullanım PolyBase tooload verilerin Azure SQL veri ambarında](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) bölümde ayrıntılar bulunur.</span><span class="sxs-lookup"><span data-stu-id="bd702-107">hello [Use PolyBase tooload data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="bd702-108">Kullanım örneği ile bir anlatım için bkz: [1 TB altında 15 dakika Azure Data Factory ile Azure SQL Data Warehouse'a veri yükleme](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="bd702-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="bd702-109">Desteklenen senaryolar</span><span class="sxs-lookup"><span data-stu-id="bd702-109">Supported scenarios</span></span>
<span data-ttu-id="bd702-110">Veri kopyalama **Azure SQL veri ambarından** veri depolarına aşağıdaki toohello:</span><span class="sxs-lookup"><span data-stu-id="bd702-110">You can copy data **from Azure SQL Data Warehouse** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="bd702-111">Veri depoları aşağıdaki hello verileri kopyalayabilirsiniz **tooAzure SQL Data Warehouse**:</span><span class="sxs-lookup"><span data-stu-id="bd702-111">You can copy data from hello following data stores **tooAzure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="bd702-112">SQL Server veya Azure SQL Database tooAzure veri kopyalama işlemi sırasında SQL Data Warehouse hello tablo hello hedef depo, veri fabrikası yoksa, otomatik olarak hello tablo SQL veri ambarı'nda hello kaynağında Merhaba tablonun hello şeması kullanarak oluşturabilirsiniz veri deposu.</span><span class="sxs-lookup"><span data-stu-id="bd702-112">When copying data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse, if hello table does not exist in hello destination store, Data Factory can automatically create hello table in SQL Data Warehouse by using hello schema of hello table in hello source data store.</span></span> <span data-ttu-id="bd702-113">Bkz: [Otomatik Tablo oluşturma](#auto-table-creation) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="bd702-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="bd702-114">Desteklenen kimlik doğrulama türü</span><span class="sxs-lookup"><span data-stu-id="bd702-114">Supported authentication type</span></span>
<span data-ttu-id="bd702-115">Azure SQL Data Warehouse Bağlayıcısı destek temel kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="bd702-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="bd702-116">Başlarken</span><span class="sxs-lookup"><span data-stu-id="bd702-116">Getting started</span></span>
<span data-ttu-id="bd702-117">Verileri farklı araçlar/API'lerini kullanarak Azure SQL Data Warehouse denetleyicisinden taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bd702-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="bd702-118">Merhaba en kolay yolu toocreate öğesine/öğesinden Azure SQL veri ambarı verileri kopyalayan bir işlem hattı toouse hello kopya veri sihirbazıdır.</span><span class="sxs-lookup"><span data-stu-id="bd702-118">hello easiest way toocreate a pipeline that copies data to/from Azure SQL Data Warehouse is toouse hello Copy data wizard.</span></span> <span data-ttu-id="bd702-119">Bkz: [öğretici: Data Factory ile SQL veri ambarına veri yükleme](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="bd702-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="bd702-120">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="bd702-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="bd702-121">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="bd702-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="bd702-122">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bd702-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="bd702-123">Oluşturma bir **veri fabrikası**.</span><span class="sxs-lookup"><span data-stu-id="bd702-123">Create a **data factory**.</span></span> <span data-ttu-id="bd702-124">Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir.</span><span class="sxs-lookup"><span data-stu-id="bd702-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="bd702-125">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="bd702-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="bd702-126">Bir Azure blob depolama tooan Azure SQL veri ambarından veri kopyalama, örneğin, iki bağlı hizmet toolink Azure depolama hesabınız ve Azure SQL veri ambarı tooyour veri fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bd702-126">For example, if you are copying data from an Azure blob storage tooan Azure SQL data warehouse, you create two linked services toolink your Azure storage account and Azure SQL data warehouse tooyour data factory.</span></span> <span data-ttu-id="bd702-127">Belirli tooAzure SQL Data Warehouse bağlantılı hizmet özellikler için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="bd702-127">For linked service properties that are specific tooAzure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="bd702-128">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="bd702-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="bd702-129">Merhaba son adımda bahsedilen hello örnekte, bir veri kümesi toospecify hello blob kapsayıcısı ve hello giriş verisi içeren klasörü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bd702-129">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="bd702-130">Ve hello blob depolama biriminden kopyalanan hello verilerini tutan Azure SQL veri ambarı hello başka bir veri kümesi toospecify hello tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bd702-130">And, you create another dataset toospecify hello table in hello Azure SQL data warehouse that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="bd702-131">Belirli tooAzure SQL veri ambarı veri kümesi özellikler için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="bd702-131">For dataset properties that are specific tooAzure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="bd702-132">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="bd702-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="bd702-133">Daha önce bahsedilen hello örnekte BlobSource bir kaynak ve SqlDWSink havuzu olarak hello kopya etkinliği için kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="bd702-133">In hello example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for hello copy activity.</span></span> <span data-ttu-id="bd702-134">Azure SQL Data Warehouse tooAzure Blob Depolama kopyalıyorsanız benzer şekilde, SqlDWSource ve BlobSink hello kopyalama etkinliği kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="bd702-134">Similarly, if you are copying from Azure SQL Data Warehouse tooAzure Blob Storage, you use SqlDWSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="bd702-135">Belirli tooAzure SQL Data Warehouse kopyalama etkinliği özellikler için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="bd702-135">For copy activity properties that are specific tooAzure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="bd702-136">Nasıl toouse bir veri deposu bir kaynak veya bir havuz olarak hakkında daha fazla bilgi için veri deposu hello önceki bölümdeki hello bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd702-136">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="bd702-137">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bd702-137">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="bd702-138">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="bd702-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="bd702-139">Azure SQL Data Warehouse/kullanılan toocopy verileri olan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="bd702-139">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="bd702-140">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooAzure SQL veri ambarı olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="bd702-140">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="bd702-141">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="bd702-141">Linked service properties</span></span>
<span data-ttu-id="bd702-142">Aşağıdaki tablonun hello JSON öğeleri belirli tooAzure SQL veri ambarı bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="bd702-142">hello following table provides description for JSON elements specific tooAzure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="bd702-143">Özellik</span><span class="sxs-lookup"><span data-stu-id="bd702-143">Property</span></span> | <span data-ttu-id="bd702-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bd702-144">Description</span></span> | <span data-ttu-id="bd702-145">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bd702-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd702-146">type</span><span class="sxs-lookup"><span data-stu-id="bd702-146">type</span></span> |<span data-ttu-id="bd702-147">Merhaba type özelliği ayarlanmalıdır: **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="bd702-147">hello type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="bd702-148">Evet</span><span class="sxs-lookup"><span data-stu-id="bd702-148">Yes</span></span> |
| <span data-ttu-id="bd702-149">connectionString</span><span class="sxs-lookup"><span data-stu-id="bd702-149">connectionString</span></span> |<span data-ttu-id="bd702-150">Tooconnect toohello Azure SQL Data Warehouse örneğine hello connectionString özelliği için gerekli bilgiler belirtin.</span><span class="sxs-lookup"><span data-stu-id="bd702-150">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> <span data-ttu-id="bd702-151">Yalnızca temel kimlik doğrulama desteklenir.</span><span class="sxs-lookup"><span data-stu-id="bd702-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="bd702-152">Evet</span><span class="sxs-lookup"><span data-stu-id="bd702-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="bd702-153">Yapılandırma [Azure SQL veritabanı Güvenlik Duvarı](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) ve veritabanı sunucusu çok hello[Azure Hizmetleri tooaccess hello sunucusu izin](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="bd702-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="bd702-154">Ayrıca, dış Azure veri fabrikası ağ geçidi ile şirket içi veri kaynaklarından dahil olmak üzere veri tooAzure SQL Data Warehouse kopyalıyorsanız, veri tooAzure SQL Data Warehouse gönderme hello makine için uygun IP adresi aralığı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bd702-154">Additionally, if you are copying data tooAzure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="bd702-155">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="bd702-155">Dataset properties</span></span>
<span data-ttu-id="bd702-156">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="bd702-156">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="bd702-157">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="bd702-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="bd702-158">Merhaba typeProperties bölümü veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="bd702-158">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="bd702-159">Merhaba **typeProperties** hello veri kümesi için bir bölüm türü **AzureSqlDWTable** hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="bd702-159">hello **typeProperties** section for hello dataset of type **AzureSqlDWTable** has hello following properties:</span></span>

| <span data-ttu-id="bd702-160">Özellik</span><span class="sxs-lookup"><span data-stu-id="bd702-160">Property</span></span> | <span data-ttu-id="bd702-161">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bd702-161">Description</span></span> | <span data-ttu-id="bd702-162">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bd702-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd702-163">tableName</span><span class="sxs-lookup"><span data-stu-id="bd702-163">tableName</span></span> |<span data-ttu-id="bd702-164">Merhaba tablonun veya bağlantılı hizmet hello hello Azure SQL Data Warehouse Veritabanı görünümünde adı ifade eder.</span><span class="sxs-lookup"><span data-stu-id="bd702-164">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="bd702-165">Evet</span><span class="sxs-lookup"><span data-stu-id="bd702-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="bd702-166">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="bd702-166">Copy activity properties</span></span>
<span data-ttu-id="bd702-167">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="bd702-167">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="bd702-168">Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bd702-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="bd702-169">Merhaba kopyalama etkinliği yalnızca bir girdi alır ve tek bir çıktı üretir.</span><span class="sxs-lookup"><span data-stu-id="bd702-169">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="bd702-170">Oysa hello typeProperties bölümünde hello etkinlik özellikleri her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="bd702-170">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="bd702-171">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="bd702-171">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="bd702-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="bd702-172">SqlDWSource</span></span>
<span data-ttu-id="bd702-173">Kaynak türü olduğunda **SqlDWSource**, aşağıdaki özelliklere hello kullanılabilir **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="bd702-173">When source is of type **SqlDWSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="bd702-174">Özellik</span><span class="sxs-lookup"><span data-stu-id="bd702-174">Property</span></span> | <span data-ttu-id="bd702-175">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bd702-175">Description</span></span> | <span data-ttu-id="bd702-176">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="bd702-176">Allowed values</span></span> | <span data-ttu-id="bd702-177">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bd702-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bd702-178">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="bd702-178">sqlReaderQuery</span></span> |<span data-ttu-id="bd702-179">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd702-179">Use hello custom query tooread data.</span></span> |<span data-ttu-id="bd702-180">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="bd702-180">SQL query string.</span></span> <span data-ttu-id="bd702-181">Örneğin: seçin * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="bd702-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="bd702-182">Hayır</span><span class="sxs-lookup"><span data-stu-id="bd702-182">No</span></span> |
| <span data-ttu-id="bd702-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="bd702-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="bd702-184">Merhaba adını hello kaynak tablodan veri okuyan yordamı depolanır.</span><span class="sxs-lookup"><span data-stu-id="bd702-184">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="bd702-185">Saklı yordam hello adı.</span><span class="sxs-lookup"><span data-stu-id="bd702-185">Name of hello stored procedure.</span></span> <span data-ttu-id="bd702-186">Merhaba son SQL deyimi SELECT deyimi hello saklı yordam içinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bd702-186">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="bd702-187">Hayır</span><span class="sxs-lookup"><span data-stu-id="bd702-187">No</span></span> |
| <span data-ttu-id="bd702-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="bd702-188">storedProcedureParameters</span></span> |<span data-ttu-id="bd702-189">Saklı yordam hello için parametreler.</span><span class="sxs-lookup"><span data-stu-id="bd702-189">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="bd702-190">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="bd702-190">Name/value pairs.</span></span> <span data-ttu-id="bd702-191">Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="bd702-191">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="bd702-192">Hayır</span><span class="sxs-lookup"><span data-stu-id="bd702-192">No</span></span> |

<span data-ttu-id="bd702-193">Merhaba, **sqlReaderQuery** Merhaba SqlDWSource, hello kopyalama etkinliği çalıştıran bu sorguyu hello Azure SQL Data Warehouse kaynak tooget hello verileri karşı belirtilir.</span><span class="sxs-lookup"><span data-stu-id="bd702-193">If hello **sqlReaderQuery** is specified for hello SqlDWSource, hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>

<span data-ttu-id="bd702-194">Alternatif olarak, bir saklı yordam hello belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (Merhaba saklı yordam parametreleri alır).</span><span class="sxs-lookup"><span data-stu-id="bd702-194">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="bd702-195">SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz hello yapısı bölümünde JSON hello kümesinin tanımlanan hello sütunlar kullanılan toobuild hello Azure SQL veri ambarına karşı sorgu toorun'dır.</span><span class="sxs-lookup"><span data-stu-id="bd702-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="bd702-196">Örnek: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="bd702-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="bd702-197">Merhaba veri kümesi tanımı hello yapısına sahip değil, tüm sütunlar hello tablosundan seçilir.</span><span class="sxs-lookup"><span data-stu-id="bd702-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="bd702-198">SqlDWSource örneği</span><span class="sxs-lookup"><span data-stu-id="bd702-198">SqlDWSource example</span></span>

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
<span data-ttu-id="bd702-199">**Merhaba saklı yordamı tanımı:**</span><span class="sxs-lookup"><span data-stu-id="bd702-199">**hello stored procedure definition:**</span></span>

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

### <a name="sqldwsink"></a><span data-ttu-id="bd702-200">SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="bd702-200">SqlDWSink</span></span>
<span data-ttu-id="bd702-201">**SqlDWSink** aşağıdaki özelliklere hello destekler:</span><span class="sxs-lookup"><span data-stu-id="bd702-201">**SqlDWSink** supports hello following properties:</span></span>

| <span data-ttu-id="bd702-202">Özellik</span><span class="sxs-lookup"><span data-stu-id="bd702-202">Property</span></span> | <span data-ttu-id="bd702-203">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bd702-203">Description</span></span> | <span data-ttu-id="bd702-204">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="bd702-204">Allowed values</span></span> | <span data-ttu-id="bd702-205">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bd702-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bd702-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="bd702-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="bd702-207">Belirli bir dilimle verilerinin temizlenmesini gibi bir sorgu için kopyalama etkinliği tooexecute belirtin.</span><span class="sxs-lookup"><span data-stu-id="bd702-207">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="bd702-208">Ayrıntılar için bkz [Yinelenebilirlik bölüm](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="bd702-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="bd702-209">Sorgu bildirimi.</span><span class="sxs-lookup"><span data-stu-id="bd702-209">A query statement.</span></span> |<span data-ttu-id="bd702-210">Hayır</span><span class="sxs-lookup"><span data-stu-id="bd702-210">No</span></span> |
| <span data-ttu-id="bd702-211">Bulunan'allowpolybase</span><span class="sxs-lookup"><span data-stu-id="bd702-211">allowPolyBase</span></span> |<span data-ttu-id="bd702-212">Gösterir olup olmadığını BULKINSERT mekanizması yerine toouse PolyBase (varsa).</span><span class="sxs-lookup"><span data-stu-id="bd702-212">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="bd702-213">**PolyBase kullanarak SQL Data Warehouse'a veri yolu tooload veri önerilen hello değildir.**</span><span class="sxs-lookup"><span data-stu-id="bd702-213">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> <span data-ttu-id="bd702-214">Bkz: [kullanım PolyBase tooload verilerin Azure SQL veri ambarında](#use-polybase-to-load-data-into-azure-sql-data-warehouse) kısıtlamaları ve ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="bd702-214">See [Use PolyBase tooload data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="bd702-215">True</span><span class="sxs-lookup"><span data-stu-id="bd702-215">True</span></span> <br/><span data-ttu-id="bd702-216">False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="bd702-216">False (default)</span></span> |<span data-ttu-id="bd702-217">Hayır</span><span class="sxs-lookup"><span data-stu-id="bd702-217">No</span></span> |
| <span data-ttu-id="bd702-218">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="bd702-218">polyBaseSettings</span></span> |<span data-ttu-id="bd702-219">Bir grup hello belirtilebilir özellik **Bulunan'allowpolybase** özelliği çok ayarlanmış**doğru**.</span><span class="sxs-lookup"><span data-stu-id="bd702-219">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="bd702-220">Hayır</span><span class="sxs-lookup"><span data-stu-id="bd702-220">No</span></span> |
| <span data-ttu-id="bd702-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="bd702-221">rejectValue</span></span> |<span data-ttu-id="bd702-222">Merhaba numarası veya hello sorgu başarısız olmadan önce reddedilemiyor satırları yüzdesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="bd702-222">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="bd702-223">Merhaba seçeneklerinde Reddet hello PolyBase'nın hakkında daha fazla bilgi edinin **bağımsız değişkenleri** bölümünü [CREATE dış TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) konu.</span><span class="sxs-lookup"><span data-stu-id="bd702-223">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="bd702-224">0 (varsayılan), 1, 2...</span><span class="sxs-lookup"><span data-stu-id="bd702-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="bd702-225">Hayır</span><span class="sxs-lookup"><span data-stu-id="bd702-225">No</span></span> |
| <span data-ttu-id="bd702-226">rejectType</span><span class="sxs-lookup"><span data-stu-id="bd702-226">rejectType</span></span> |<span data-ttu-id="bd702-227">Merhaba rejectValue seçeneği bir hazır değer veya bir yüzde belirtilen belirtir.</span><span class="sxs-lookup"><span data-stu-id="bd702-227">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="bd702-228">Değer (varsayılan), yüzde</span><span class="sxs-lookup"><span data-stu-id="bd702-228">Value (default), Percentage</span></span> |<span data-ttu-id="bd702-229">Hayır</span><span class="sxs-lookup"><span data-stu-id="bd702-229">No</span></span> |
| <span data-ttu-id="bd702-230">Havuzu'na ilişkin</span><span class="sxs-lookup"><span data-stu-id="bd702-230">rejectSampleValue</span></span> |<span data-ttu-id="bd702-231">Merhaba PolyBase reddedilen satırları hello yüzdesini yeniden hesaplar önce satırları tooretrieve hello sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="bd702-231">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="bd702-232">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="bd702-232">1, 2, …</span></span> |<span data-ttu-id="bd702-233">Evet, varsa **rejectType** olan **yüzdesi**</span><span class="sxs-lookup"><span data-stu-id="bd702-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="bd702-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="bd702-234">useTypeDefault</span></span> |<span data-ttu-id="bd702-235">PolyBase hello metin dosyasından veri aldığında değerlerde eksik toohandle metin dosyaları nasıl ayrılmış belirtir.</span><span class="sxs-lookup"><span data-stu-id="bd702-235">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="bd702-236">Merhaba bağımsız değişkenler bölümünde bu özelliği hakkında daha fazla bilgi [oluşturma EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="bd702-236">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="bd702-237">TRUE, False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="bd702-237">True, False (default)</span></span> |<span data-ttu-id="bd702-238">Hayır</span><span class="sxs-lookup"><span data-stu-id="bd702-238">No</span></span> |
| <span data-ttu-id="bd702-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="bd702-239">writeBatchSize</span></span> |<span data-ttu-id="bd702-240">Merhaba arabellek boyutu writeBatchSize ulaştığında veri hello SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="bd702-240">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="bd702-241">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="bd702-241">Integer (number of rows)</span></span> |<span data-ttu-id="bd702-242">Hayır (varsayılan: 10000)</span><span class="sxs-lookup"><span data-stu-id="bd702-242">No (default: 10000)</span></span> |
| <span data-ttu-id="bd702-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="bd702-243">writeBatchTimeout</span></span> |<span data-ttu-id="bd702-244">Zaman aşımına uğramadan önce hello toplu ekleme işlemi toocomplete bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="bd702-244">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="bd702-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="bd702-245">timespan</span></span><br/><br/> <span data-ttu-id="bd702-246">Örnek: "00: 30:00" (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="bd702-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="bd702-247">Hayır</span><span class="sxs-lookup"><span data-stu-id="bd702-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="bd702-248">SqlDWSink örneği</span><span class="sxs-lookup"><span data-stu-id="bd702-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="bd702-249">Azure SQL Data Warehouse'a PolyBase tooload verileri kullanma</span><span class="sxs-lookup"><span data-stu-id="bd702-249">Use PolyBase tooload data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="bd702-250">Kullanarak  **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)**  büyük miktarda veri yüksek işleme ile Azure SQL Data Warehouse'a veri yükleme etkili bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="bd702-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="bd702-251">Merhaba varsayılan BULKINSERT mekanizmasını yerine PolyBase kullanarak büyük kazanç hello verimliliği de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd702-251">You can see a large gain in hello throughput by using PolyBase instead of hello default BULKINSERT mechanism.</span></span> <span data-ttu-id="bd702-252">Bkz: [kopyalama performans başvuru numarası](data-factory-copy-activity-performance.md#performance-reference) ayrıntılı karşılaştırması ile.</span><span class="sxs-lookup"><span data-stu-id="bd702-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="bd702-253">Kullanım örneği ile bir anlatım için bkz: [1 TB altında 15 dakika Azure Data Factory ile Azure SQL Data Warehouse'a veri yükleme](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="bd702-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="bd702-254">Veri kaynağınızı ise **Azure Blob veya Azure Data Lake Store**ve hello biçimi PolyBase ile uyumlu ise, SQL Data Warehouse Polybase'i kullanarak tooAzure doğrudan kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd702-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and hello format is compatible with PolyBase, you can directly copy tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="bd702-255">Bkz:  **[Polybase'i kullanarak doğrudan kopyalama](#direct-copy-using-polybase)**  ayrıntılarla.</span><span class="sxs-lookup"><span data-stu-id="bd702-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="bd702-256">Kaynak veri deposu ve biçim başlangıçta desteklenmiyor, PolyBase tarafından hello kullanabilirsiniz  **[Polybase'i kullanarak kopyalama hazırlanan](#staged-copy-using-polybase)**  yerine özelliği.</span><span class="sxs-lookup"><span data-stu-id="bd702-256">If your source data store and format is not originally supported by PolyBase, you can use hello **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="bd702-257">Ayrıca, daha iyi verim otomatik olarak hello veri PolyBase uyumlu biçimine dönüştürmek için kullanılan ve hello verileri Azure Blob storage'da depolamak sağlar.</span><span class="sxs-lookup"><span data-stu-id="bd702-257">It also provides you better throughput by automatically converting hello data into PolyBase-compatible format and storing hello data in Azure Blob storage.</span></span> <span data-ttu-id="bd702-258">Ardından verileri SQL Data Warehouse'a veri yükler.</span><span class="sxs-lookup"><span data-stu-id="bd702-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="bd702-259">Set hello `allowPolyBase` özelliği çok**true** hello Azure SQL Data Warehouse'a örnek Azure Data Factory toouse PolyBase toocopy veri için aşağıdaki gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="bd702-259">Set hello `allowPolyBase` property too**true** as shown in hello following example for Azure Data Factory toouse PolyBase toocopy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="bd702-260">Bulunan'allowpolybase tootrue ayarladığınızda hello kullanarak PolyBase belirli özelliklerini belirtebilirsiniz `polyBaseSettings` özellik grubu.</span><span class="sxs-lookup"><span data-stu-id="bd702-260">When you set allowPolyBase tootrue, you can specify PolyBase specific properties using hello `polyBaseSettings` property group.</span></span> <span data-ttu-id="bd702-261">Merhaba bkz [SqlDWSink](#SqlDWSink) polyBaseSettings ile kullanabileceğiniz özellikleri hakkında ayrıntılı bilgi için bölüm.</span><span class="sxs-lookup"><span data-stu-id="bd702-261">see hello [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

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

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="bd702-262">Polybase'i kullanarak doğrudan kopyalama</span><span class="sxs-lookup"><span data-stu-id="bd702-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="bd702-263">SQL veri ambarı PolyBase doğrudan desteği Azure Blob ve Azure Data Lake Store (hizmet sorumlusu kullanarak) kaynak olarak ve belirli dosya biçimi gereksinimleriyle.</span><span class="sxs-lookup"><span data-stu-id="bd702-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="bd702-264">Veri kaynağınızı Bu bölümde açıklanan hello ölçütlerini karşılıyorsa, kaynak veri deposu tooAzure PolyBase kullanarak SQL Data Warehouse doğrudan kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd702-264">If your source data meets hello criteria described in this section, you can directly copy from source data store tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="bd702-265">Aksi takdirde, kullanabileceğiniz [Polybase'i kullanarak kopyalama hazırlanan](#staged-copy-using-polybase).</span><span class="sxs-lookup"><span data-stu-id="bd702-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="bd702-266">Data Lake Store tooSQL veri ambarı toocopy verilerden verimli bir şekilde daha fazla bilgi gelen [verilerden daha kolay ve rahat toouncover Öngörüler Data Lake Store ile SQL veri ambarı kullanırken bile Azure Data Factory kılar](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="bd702-266">toocopy data from Data Lake Store tooSQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient toouncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="bd702-267">Hello gereksinimleri karşılanmadı, Azure Data Factory hello ayarlarını denetler ve otomatik olarak toohello BULKINSERT mekanizması hello veri taşıma için geri döner.</span><span class="sxs-lookup"><span data-stu-id="bd702-267">If hello requirements are not met, Azure Data Factory checks hello settings and automatically falls back toohello BULKINSERT mechanism for hello data movement.</span></span>

1. <span data-ttu-id="bd702-268">**Kaynak bağlantılı hizmeti** türüdür: **AzureStorage** veya **AzureDataLakeStore hizmet asıl kimlik doğrulaması ile**.</span><span class="sxs-lookup"><span data-stu-id="bd702-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="bd702-269">Merhaba **girdi veri kümesi** türüdür: **AzureBlob** veya **AzureDataLakeStore**, ve hello biçim türü'nün altında `type` özellikleri **OrcFormat** , veya **TextFormat** yapılandırmaları aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="bd702-269">hello **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and hello format type under `type` properties is **OrcFormat**, or **TextFormat** with hello following configurations:</span></span>

   1. <span data-ttu-id="bd702-270">`rowDelimiter`olmalıdır  **\n** .</span><span class="sxs-lookup"><span data-stu-id="bd702-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="bd702-271">`nullValue`çok ayarlanır**boş dize** (""), veya `treatEmptyAsNull` çok ayarlanır**doğru**.</span><span class="sxs-lookup"><span data-stu-id="bd702-271">`nullValue` is set too**empty string** (""), or `treatEmptyAsNull` is set too**true**.</span></span>
   3. <span data-ttu-id="bd702-272">`encodingName`çok ayarlanır**utf-8**, olduğu **varsayılan** değeri.</span><span class="sxs-lookup"><span data-stu-id="bd702-272">`encodingName` is set too**utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="bd702-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, ve `skipLineCount` belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="bd702-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="bd702-274">`compression`olabilir **sıkıştırma yok**, **GZip**, veya **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="bd702-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

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

3. <span data-ttu-id="bd702-275">Yoktur hiçbir `skipHeaderLineCount` altında ayarı **BlobSource** veya **AzureDataLakeStore** hello hello ardışık düzeninde kopyalama etkinliği için.</span><span class="sxs-lookup"><span data-stu-id="bd702-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for hello Copy activity in hello pipeline.</span></span>
4. <span data-ttu-id="bd702-276">Yoktur hiçbir `sliceIdentifierColumnName` altında ayarı **SqlDWSink** hello hello ardışık düzeninde kopyalama etkinliği için.</span><span class="sxs-lookup"><span data-stu-id="bd702-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for hello Copy activity in hello pipeline.</span></span> <span data-ttu-id="bd702-277">(Tüm veriler güncelleştirilir veya hiçbir şey bir tek çalıştırmada güncelleştirildiğinde PolyBase garanti eder.</span><span class="sxs-lookup"><span data-stu-id="bd702-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="bd702-278">tooachieve **Yinelenebilirlik**, kullanabileceğinizi `sqlWriterCleanupScript`).</span><span class="sxs-lookup"><span data-stu-id="bd702-278">tooachieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="bd702-279">Var olan hiçbir `columnMapping` kopyalama etkinliği ilişkili hello kullanılmakta.</span><span class="sxs-lookup"><span data-stu-id="bd702-279">There is no `columnMapping` being used in hello associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="bd702-280">Polybase'i kullanarak hazırlanmış kopyalama</span><span class="sxs-lookup"><span data-stu-id="bd702-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="bd702-281">Veri kaynağınızı hello önceki bölümde sunulan hello ölçütlerle eşleşmeyen, bir geçici hazırlama Azure Blob (Premium depolama olamaz) depolama aracılığıyla veri kopyalamayı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd702-281">When your source data doesn’t meet hello criteria introduced in hello previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="bd702-282">Bu durumda, Azure Data Factory otomatik olarak hello veri toomeet veri biçimi gereksinimleri PolyBase, daha sonra kullanmak PolyBase tooload verileri SQL Data Warehouse dönüşümleri gerçekleştirir ve en sonunda temp verilerinizi hello Blob depolama biriminden temizleyin.</span><span class="sxs-lookup"><span data-stu-id="bd702-282">In this case, Azure Data Factory automatically performs transformations on hello data toomeet data format requirements of PolyBase, then use PolyBase tooload data into SQL Data Warehouse, and at last clean-up your temp data from hello Blob storage.</span></span> <span data-ttu-id="bd702-283">Bkz: [hazırlanan kopyalama](data-factory-copy-activity-performance.md#staged-copy) nasıl hazırlama Azure Blob üzerinden veri kopyalama genel çalıştığı hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="bd702-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="bd702-284">Bir şirket içi veri kopyalama verileri Azure SQL Data Polybase'i kullanarak Warehouse'a veri depolamak ve hazırlama, veri yönetimi ağ geçidi sürümü 2.4 ise, JRE (Java Çalışma zamanı ortamı) ağ geçidiniz gerekli olduğunda, makine kullanılan tootransform veri kaynağınızı olduğu doğru biçime.</span><span class="sxs-lookup"><span data-stu-id="bd702-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used tootransform your source data into proper format.</span></span> <span data-ttu-id="bd702-285">Bu bağımlılık ağ geçidi toohello son tooavoid yükseltme önerir.</span><span class="sxs-lookup"><span data-stu-id="bd702-285">Suggest you upgrade your gateway toohello latest tooavoid such dependency.</span></span>
>

<span data-ttu-id="bd702-286">toouse bu özelliği, oluşturma bir [Azure depolama bağlantılı hizmeti](data-factory-azure-blob-connector.md#azure-storage-linked-service) toohello hello geçici blob depolama alanına sahip bir Azure depolama hesabı anlamına gelir, sonra hello belirtin `enableStaging` ve `stagingSettings` hello kopyalama etkinliği özellikleri hello kod aşağıdaki gösterildiği gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="bd702-286">toouse this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers toohello Azure Storage Account that has hello interim blob storage, then specify hello `enableStaging` and `stagingSettings` properties for hello Copy Activity as shown in hello following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
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

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="bd702-287">PolyBase kullanırken en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="bd702-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="bd702-288">Merhaba aşağıdaki bölümlerde ek en iyi yöntemler toohello bölümünde belirtildiği olanları sağlamak [en iyi uygulamalar Azure SQL Data Warehouse için](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="bd702-288">hello following sections provide additional best practices toohello ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="bd702-289">Gerekli veritabanı izni</span><span class="sxs-lookup"><span data-stu-id="bd702-289">Required database permission</span></span>
<span data-ttu-id="bd702-290">toouse PolyBase, gerektirdiği SQL Data Warehouse kullanılan tooload verisine sahip hello kullanıcı hello olan ["Denetim" izni](https://msdn.microsoft.com/library/ms191291.aspx) hello hedef veritabanı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="bd702-290">toouse PolyBase, it requires hello user being used tooload data into SQL Data Warehouse has hello ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on hello target database.</span></span> <span data-ttu-id="bd702-291">Tooadd olan tek yönlü tooachieve "db_owner" rolünün bir üyesi olarak o kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="bd702-291">One way tooachieve that is tooadd that user as a member of "db_owner" role.</span></span> <span data-ttu-id="bd702-292">Bilgi nasıl toodo, izleyerek [Bu bölümde](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span><span class="sxs-lookup"><span data-stu-id="bd702-292">Learn how toodo that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="bd702-293">Satır boyutu ve verileri sınırlama yazın</span><span class="sxs-lookup"><span data-stu-id="bd702-293">Row size and data type limitation</span></span>
<span data-ttu-id="bd702-294">Polybase yükleri sınırlı tooloading satırları hem küçük **1 MB** ve tooVARCHR(MAX), yüklenemiyor NVARCHAR(MAX) veya VARBINARY(MAX).</span><span class="sxs-lookup"><span data-stu-id="bd702-294">Polybase loads are limited tooloading rows both smaller than **1 MB** and cannot load tooVARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="bd702-295">Çok başvuran[burada](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span><span class="sxs-lookup"><span data-stu-id="bd702-295">Refer too[here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="bd702-296">Satır boyutu 1 MB'tan fazla kaynak verilerle varsa, burada her biri en büyük satır boyutu hello hello sınırını aşmayacak birkaç küçük parçalara toosplit hello kaynak tabloları dikey isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd702-296">If you have source data with rows of size greater than 1 MB, you may want toosplit hello source tables vertically into several small ones where hello largest row size of each of them does not exceed hello limit.</span></span> <span data-ttu-id="bd702-297">Merhaba küçük tabloları sonra PolyBase kullanarak ve Azure SQL Data Warehouse'da birleştirmeniz yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="bd702-297">hello smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="bd702-298">SQL veri ambarı kaynak sınıfı</span><span class="sxs-lookup"><span data-stu-id="bd702-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="bd702-299">tooachieve en iyi olası üretilen işi tooassign büyük kaynak sınıfı toohello kullanıcı olan göz önünde bulundurun PolyBase aracılığıyla SQL veri ambarında kullanılan tooload veri.</span><span class="sxs-lookup"><span data-stu-id="bd702-299">tooachieve best possible throughput, consider tooassign larger resource class toohello user being used tooload data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="bd702-300">Bilgi nasıl toodo, izleyerek [kullanıcı kaynak sınıfı örneğini değiştirmek](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="bd702-300">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="bd702-301">Azure SQL Data Warehouse tableName</span><span class="sxs-lookup"><span data-stu-id="bd702-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="bd702-302">Merhaba aşağıdaki tabloda örnekler hakkında yönergeler verilmektedir toospecify hello **tableName** dataset JSON çeşitli şema ve tablo adı için bir özellik.</span><span class="sxs-lookup"><span data-stu-id="bd702-302">hello following table provides examples on how toospecify hello **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="bd702-303">DB şeması</span><span class="sxs-lookup"><span data-stu-id="bd702-303">DB Schema</span></span> | <span data-ttu-id="bd702-304">Tablo adı</span><span class="sxs-lookup"><span data-stu-id="bd702-304">Table name</span></span> | <span data-ttu-id="bd702-305">tableName JSON özelliği</span><span class="sxs-lookup"><span data-stu-id="bd702-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd702-306">dbo</span><span class="sxs-lookup"><span data-stu-id="bd702-306">dbo</span></span> |<span data-ttu-id="bd702-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="bd702-307">MyTable</span></span> |<span data-ttu-id="bd702-308">MyTable ya da dbo. MyTable ya da [dbo]. [MyTable]</span><span class="sxs-lookup"><span data-stu-id="bd702-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="bd702-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="bd702-309">dbo1</span></span> |<span data-ttu-id="bd702-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="bd702-310">MyTable</span></span> |<span data-ttu-id="bd702-311">dbo1. MyTable veya [dbo1]. [MyTable]</span><span class="sxs-lookup"><span data-stu-id="bd702-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="bd702-312">dbo</span><span class="sxs-lookup"><span data-stu-id="bd702-312">dbo</span></span> |<span data-ttu-id="bd702-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="bd702-313">My.Table</span></span> |<span data-ttu-id="bd702-314">[My.Table] veya [dbo]. [My.Table]</span><span class="sxs-lookup"><span data-stu-id="bd702-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="bd702-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="bd702-315">dbo1</span></span> |<span data-ttu-id="bd702-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="bd702-316">My.Table</span></span> |<span data-ttu-id="bd702-317">[dbo1]. [My.Table]</span><span class="sxs-lookup"><span data-stu-id="bd702-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="bd702-318">Aşağıdaki hata hello görürseniz, hello tableName özelliği için belirtilen başlangıç değeri ile ilgili bir sorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="bd702-318">If you see hello following error, it could be an issue with hello value you specified for hello tableName property.</span></span> <span data-ttu-id="bd702-319">Merhaba tableName JSON özellik için hello doğru bir şekilde toospecify değerler için Hello tabloya bakın.</span><span class="sxs-lookup"><span data-stu-id="bd702-319">See hello table for hello correct way toospecify values for hello tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="bd702-320">Varsayılan değerleri içeren sütun</span><span class="sxs-lookup"><span data-stu-id="bd702-320">Columns with default values</span></span>
<span data-ttu-id="bd702-321">Şu anda aynı sayıda sütun hello hedef tabloda olduğu gibi hello PolyBase özelliği veri fabrikasında yalnızca kabul eder.</span><span class="sxs-lookup"><span data-stu-id="bd702-321">Currently, PolyBase feature in Data Factory only accepts hello same number of columns as in hello target table.</span></span> <span data-ttu-id="bd702-322">Dört sütun içeren bir tablo varsa ve bunlardan birini varsayılan bir değerle tanımlanan söyleyin.</span><span class="sxs-lookup"><span data-stu-id="bd702-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="bd702-323">Merhaba giriş verisi hala dört sütun içermelidir.</span><span class="sxs-lookup"><span data-stu-id="bd702-323">hello input data should still contain four columns.</span></span> <span data-ttu-id="bd702-324">3-sütun girdi veri kümesi sağlayan bir hata benzer toohello iletiden verir:</span><span class="sxs-lookup"><span data-stu-id="bd702-324">Providing a 3-column input dataset would yield an error similar toohello following message:</span></span>

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
<span data-ttu-id="bd702-325">NULL değer, varsayılan değeri özel bir biçimidir.</span><span class="sxs-lookup"><span data-stu-id="bd702-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="bd702-326">Merhaba sütunu null atanabilir ise, hello giriş verilerini (blob) Bu sütun için boş olabilir (Merhaba giriş kümesinden eksik olamaz).</span><span class="sxs-lookup"><span data-stu-id="bd702-326">If hello column is nullable, hello input data (in blob) for that column could be empty (cannot be missing from hello input dataset).</span></span> <span data-ttu-id="bd702-327">PolyBase, bunlar için NULL hello Azure SQL Data Warehouse ekler.</span><span class="sxs-lookup"><span data-stu-id="bd702-327">PolyBase inserts NULL for them in hello Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="bd702-328">Otomatik Tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd702-328">Auto table creation</span></span>
<span data-ttu-id="bd702-329">Toohello kaynak tablosunda karşılık gelen Azure SQL veritabanı tooAzure SQL veri ambarı ve hello tablosu hello hedef deposunda mevcut değil veya kopyalama Sihirbazı'nı toocopy verileri SQL Server kullanıyorsanız, veri fabrikası otomatik olarak hello tablo hello oluşturabilirsiniz Merhaba kaynak tablo şemasını kullanarak veri ambarı'nı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bd702-329">If you are using Copy Wizard toocopy data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse and hello table that corresponds toohello source table does not exist in hello destination store, Data Factory can automatically create hello table in hello data warehouse by using hello source table schema.</span></span>

<span data-ttu-id="bd702-330">Veri Fabrikası hello hedef deposunda hello tablo oluşturur hello ile aynı tablo hello kaynak veri deposundaki adı.</span><span class="sxs-lookup"><span data-stu-id="bd702-330">Data Factory creates hello table in hello destination store with hello same table name in hello source data store.</span></span> <span data-ttu-id="bd702-331">Merhaba veri türlerinde sütun türü eşlemesi aşağıdaki hello göre seçilir.</span><span class="sxs-lookup"><span data-stu-id="bd702-331">hello data types for columns are chosen based on hello following type mapping.</span></span> <span data-ttu-id="bd702-332">Gerekli olursa, kaynak ve hedef depoları arasında uyumsuzlukları türü dönüşümleri toofix gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="bd702-332">If needed, it performs type conversions toofix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="bd702-333">Ayrıca, hepsini bir kez Tablo dağıtım kullanır.</span><span class="sxs-lookup"><span data-stu-id="bd702-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="bd702-334">Kaynak SQL veritabanı sütun türü</span><span class="sxs-lookup"><span data-stu-id="bd702-334">Source SQL Database column type</span></span> | <span data-ttu-id="bd702-335">Hedef SQL DW sütun türü (boyutu kısıtlaması)</span><span class="sxs-lookup"><span data-stu-id="bd702-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="bd702-336">Int</span><span class="sxs-lookup"><span data-stu-id="bd702-336">Int</span></span> | <span data-ttu-id="bd702-337">Int</span><span class="sxs-lookup"><span data-stu-id="bd702-337">Int</span></span> |
| <span data-ttu-id="bd702-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="bd702-338">BigInt</span></span> | <span data-ttu-id="bd702-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="bd702-339">BigInt</span></span> |
| <span data-ttu-id="bd702-340">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="bd702-340">SmallInt</span></span> | <span data-ttu-id="bd702-341">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="bd702-341">SmallInt</span></span> |
| <span data-ttu-id="bd702-342">Mini tamsayı</span><span class="sxs-lookup"><span data-stu-id="bd702-342">TinyInt</span></span> | <span data-ttu-id="bd702-343">Mini tamsayı</span><span class="sxs-lookup"><span data-stu-id="bd702-343">TinyInt</span></span> |
| <span data-ttu-id="bd702-344">bit</span><span class="sxs-lookup"><span data-stu-id="bd702-344">Bit</span></span> | <span data-ttu-id="bd702-345">bit</span><span class="sxs-lookup"><span data-stu-id="bd702-345">Bit</span></span> |
| <span data-ttu-id="bd702-346">Ondalık</span><span class="sxs-lookup"><span data-stu-id="bd702-346">Decimal</span></span> | <span data-ttu-id="bd702-347">Ondalık</span><span class="sxs-lookup"><span data-stu-id="bd702-347">Decimal</span></span> |
| <span data-ttu-id="bd702-348">sayısal</span><span class="sxs-lookup"><span data-stu-id="bd702-348">Numeric</span></span> | <span data-ttu-id="bd702-349">Ondalık</span><span class="sxs-lookup"><span data-stu-id="bd702-349">Decimal</span></span> |
| <span data-ttu-id="bd702-350">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="bd702-350">Float</span></span> | <span data-ttu-id="bd702-351">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="bd702-351">Float</span></span> |
| <span data-ttu-id="bd702-352">para</span><span class="sxs-lookup"><span data-stu-id="bd702-352">Money</span></span> | <span data-ttu-id="bd702-353">para</span><span class="sxs-lookup"><span data-stu-id="bd702-353">Money</span></span> |
| <span data-ttu-id="bd702-354">Real</span><span class="sxs-lookup"><span data-stu-id="bd702-354">Real</span></span> | <span data-ttu-id="bd702-355">Real</span><span class="sxs-lookup"><span data-stu-id="bd702-355">Real</span></span> |
| <span data-ttu-id="bd702-356">Küçük para</span><span class="sxs-lookup"><span data-stu-id="bd702-356">SmallMoney</span></span> | <span data-ttu-id="bd702-357">Küçük para</span><span class="sxs-lookup"><span data-stu-id="bd702-357">SmallMoney</span></span> |
| <span data-ttu-id="bd702-358">İkili</span><span class="sxs-lookup"><span data-stu-id="bd702-358">Binary</span></span> | <span data-ttu-id="bd702-359">İkili</span><span class="sxs-lookup"><span data-stu-id="bd702-359">Binary</span></span> |
| <span data-ttu-id="bd702-360">varbinary</span><span class="sxs-lookup"><span data-stu-id="bd702-360">Varbinary</span></span> | <span data-ttu-id="bd702-361">Varbinary (yukarı too8000)</span><span class="sxs-lookup"><span data-stu-id="bd702-361">Varbinary (up too8000)</span></span> |
| <span data-ttu-id="bd702-362">Tarih</span><span class="sxs-lookup"><span data-stu-id="bd702-362">Date</span></span> | <span data-ttu-id="bd702-363">Tarih</span><span class="sxs-lookup"><span data-stu-id="bd702-363">Date</span></span> |
| <span data-ttu-id="bd702-364">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="bd702-364">DateTime</span></span> | <span data-ttu-id="bd702-365">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="bd702-365">DateTime</span></span> |
| <span data-ttu-id="bd702-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="bd702-366">DateTime2</span></span> | <span data-ttu-id="bd702-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="bd702-367">DateTime2</span></span> |
| <span data-ttu-id="bd702-368">Zaman</span><span class="sxs-lookup"><span data-stu-id="bd702-368">Time</span></span> | <span data-ttu-id="bd702-369">Zaman</span><span class="sxs-lookup"><span data-stu-id="bd702-369">Time</span></span> |
| <span data-ttu-id="bd702-370">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="bd702-370">DateTimeOffset</span></span> | <span data-ttu-id="bd702-371">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="bd702-371">DateTimeOffset</span></span> |
| <span data-ttu-id="bd702-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="bd702-372">SmallDateTime</span></span> | <span data-ttu-id="bd702-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="bd702-373">SmallDateTime</span></span> |
| <span data-ttu-id="bd702-374">Metin</span><span class="sxs-lookup"><span data-stu-id="bd702-374">Text</span></span> | <span data-ttu-id="bd702-375">VARCHAR (yukarı too8000)</span><span class="sxs-lookup"><span data-stu-id="bd702-375">Varchar (up too8000)</span></span> |
| <span data-ttu-id="bd702-376">NText</span><span class="sxs-lookup"><span data-stu-id="bd702-376">NText</span></span> | <span data-ttu-id="bd702-377">NVarChar (yukarı too4000)</span><span class="sxs-lookup"><span data-stu-id="bd702-377">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="bd702-378">Görüntü</span><span class="sxs-lookup"><span data-stu-id="bd702-378">Image</span></span> | <span data-ttu-id="bd702-379">VarBinary (yukarı too8000)</span><span class="sxs-lookup"><span data-stu-id="bd702-379">VarBinary (up too8000)</span></span> |
| <span data-ttu-id="bd702-380">Benzersiz tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="bd702-380">UniqueIdentifier</span></span> | <span data-ttu-id="bd702-381">Benzersiz tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="bd702-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="bd702-382">char</span><span class="sxs-lookup"><span data-stu-id="bd702-382">Char</span></span> | <span data-ttu-id="bd702-383">char</span><span class="sxs-lookup"><span data-stu-id="bd702-383">Char</span></span> |
| <span data-ttu-id="bd702-384">NChar</span><span class="sxs-lookup"><span data-stu-id="bd702-384">NChar</span></span> | <span data-ttu-id="bd702-385">NChar</span><span class="sxs-lookup"><span data-stu-id="bd702-385">NChar</span></span> |
| <span data-ttu-id="bd702-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="bd702-386">VarChar</span></span> | <span data-ttu-id="bd702-387">VarChar (yukarı too8000)</span><span class="sxs-lookup"><span data-stu-id="bd702-387">VarChar (up too8000)</span></span> |
| <span data-ttu-id="bd702-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="bd702-388">NVarChar</span></span> | <span data-ttu-id="bd702-389">NVarChar (yukarı too4000)</span><span class="sxs-lookup"><span data-stu-id="bd702-389">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="bd702-390">XML</span><span class="sxs-lookup"><span data-stu-id="bd702-390">Xml</span></span> | <span data-ttu-id="bd702-391">VARCHAR (yukarı too8000)</span><span class="sxs-lookup"><span data-stu-id="bd702-391">Varchar (up too8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="bd702-392">Tür eşlemesi için Azure SQL veri ambarı</span><span class="sxs-lookup"><span data-stu-id="bd702-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="bd702-393">Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri 2 adımlı yaklaşımı izleyerek hello ile:</span><span class="sxs-lookup"><span data-stu-id="bd702-393">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="bd702-394">Yerel kaynak türleri too.NET türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="bd702-394">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="bd702-395">.NET türü toonative havuz türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="bd702-395">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="bd702-396">Çok & Azure SQL veri ambarından veri taşırken, hello aşağıdaki eşlemelerini too.NET türü ve bunun tersi de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bd702-396">When moving data too& from Azure SQL Data Warehouse, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="bd702-397">Merhaba eşleme hello aynı [ADO.NET için SQL Server veri türü eşlemesi](https://msdn.microsoft.com/library/cc716729.aspx).</span><span class="sxs-lookup"><span data-stu-id="bd702-397">hello mapping is same as hello [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="bd702-398">SQL Server veritabanı altyapısı türü</span><span class="sxs-lookup"><span data-stu-id="bd702-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="bd702-399">.NET framework türü</span><span class="sxs-lookup"><span data-stu-id="bd702-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="bd702-400">bigint</span><span class="sxs-lookup"><span data-stu-id="bd702-400">bigint</span></span> |<span data-ttu-id="bd702-401">Int64</span><span class="sxs-lookup"><span data-stu-id="bd702-401">Int64</span></span> |
| <span data-ttu-id="bd702-402">İkili</span><span class="sxs-lookup"><span data-stu-id="bd702-402">binary</span></span> |<span data-ttu-id="bd702-403">Byte]</span><span class="sxs-lookup"><span data-stu-id="bd702-403">Byte[]</span></span> |
| <span data-ttu-id="bd702-404">bit</span><span class="sxs-lookup"><span data-stu-id="bd702-404">bit</span></span> |<span data-ttu-id="bd702-405">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="bd702-405">Boolean</span></span> |
| <span data-ttu-id="bd702-406">char</span><span class="sxs-lookup"><span data-stu-id="bd702-406">char</span></span> |<span data-ttu-id="bd702-407">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="bd702-407">String, Char[]</span></span> |
| <span data-ttu-id="bd702-408">Tarih</span><span class="sxs-lookup"><span data-stu-id="bd702-408">date</span></span> |<span data-ttu-id="bd702-409">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="bd702-409">DateTime</span></span> |
| <span data-ttu-id="bd702-410">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="bd702-410">Datetime</span></span> |<span data-ttu-id="bd702-411">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="bd702-411">DateTime</span></span> |
| <span data-ttu-id="bd702-412">datetime2</span><span class="sxs-lookup"><span data-stu-id="bd702-412">datetime2</span></span> |<span data-ttu-id="bd702-413">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="bd702-413">DateTime</span></span> |
| <span data-ttu-id="bd702-414">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="bd702-414">Datetimeoffset</span></span> |<span data-ttu-id="bd702-415">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="bd702-415">DateTimeOffset</span></span> |
| <span data-ttu-id="bd702-416">Ondalık</span><span class="sxs-lookup"><span data-stu-id="bd702-416">Decimal</span></span> |<span data-ttu-id="bd702-417">Ondalık</span><span class="sxs-lookup"><span data-stu-id="bd702-417">Decimal</span></span> |
| <span data-ttu-id="bd702-418">FILESTREAM özniteliği (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="bd702-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="bd702-419">Byte]</span><span class="sxs-lookup"><span data-stu-id="bd702-419">Byte[]</span></span> |
| <span data-ttu-id="bd702-420">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="bd702-420">Float</span></span> |<span data-ttu-id="bd702-421">Çift</span><span class="sxs-lookup"><span data-stu-id="bd702-421">Double</span></span> |
| <span data-ttu-id="bd702-422">Görüntü</span><span class="sxs-lookup"><span data-stu-id="bd702-422">image</span></span> |<span data-ttu-id="bd702-423">Byte]</span><span class="sxs-lookup"><span data-stu-id="bd702-423">Byte[]</span></span> |
| <span data-ttu-id="bd702-424">Int</span><span class="sxs-lookup"><span data-stu-id="bd702-424">int</span></span> |<span data-ttu-id="bd702-425">Int32</span><span class="sxs-lookup"><span data-stu-id="bd702-425">Int32</span></span> |
| <span data-ttu-id="bd702-426">para</span><span class="sxs-lookup"><span data-stu-id="bd702-426">money</span></span> |<span data-ttu-id="bd702-427">Ondalık</span><span class="sxs-lookup"><span data-stu-id="bd702-427">Decimal</span></span> |
| <span data-ttu-id="bd702-428">nchar</span><span class="sxs-lookup"><span data-stu-id="bd702-428">nchar</span></span> |<span data-ttu-id="bd702-429">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="bd702-429">String, Char[]</span></span> |
| <span data-ttu-id="bd702-430">ntext</span><span class="sxs-lookup"><span data-stu-id="bd702-430">ntext</span></span> |<span data-ttu-id="bd702-431">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="bd702-431">String, Char[]</span></span> |
| <span data-ttu-id="bd702-432">sayısal</span><span class="sxs-lookup"><span data-stu-id="bd702-432">numeric</span></span> |<span data-ttu-id="bd702-433">Ondalık</span><span class="sxs-lookup"><span data-stu-id="bd702-433">Decimal</span></span> |
| <span data-ttu-id="bd702-434">nvarchar</span><span class="sxs-lookup"><span data-stu-id="bd702-434">nvarchar</span></span> |<span data-ttu-id="bd702-435">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="bd702-435">String, Char[]</span></span> |
| <span data-ttu-id="bd702-436">Gerçek</span><span class="sxs-lookup"><span data-stu-id="bd702-436">real</span></span> |<span data-ttu-id="bd702-437">Tek</span><span class="sxs-lookup"><span data-stu-id="bd702-437">Single</span></span> |
| <span data-ttu-id="bd702-438">rowVersion</span><span class="sxs-lookup"><span data-stu-id="bd702-438">rowversion</span></span> |<span data-ttu-id="bd702-439">Byte]</span><span class="sxs-lookup"><span data-stu-id="bd702-439">Byte[]</span></span> |
| <span data-ttu-id="bd702-440">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="bd702-440">smalldatetime</span></span> |<span data-ttu-id="bd702-441">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="bd702-441">DateTime</span></span> |
| <span data-ttu-id="bd702-442">tamsayı</span><span class="sxs-lookup"><span data-stu-id="bd702-442">smallint</span></span> |<span data-ttu-id="bd702-443">Int16</span><span class="sxs-lookup"><span data-stu-id="bd702-443">Int16</span></span> |
| <span data-ttu-id="bd702-444">küçük para</span><span class="sxs-lookup"><span data-stu-id="bd702-444">smallmoney</span></span> |<span data-ttu-id="bd702-445">Ondalık</span><span class="sxs-lookup"><span data-stu-id="bd702-445">Decimal</span></span> |
| <span data-ttu-id="bd702-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="bd702-446">sql_variant</span></span> |<span data-ttu-id="bd702-447">Nesne *</span><span class="sxs-lookup"><span data-stu-id="bd702-447">Object *</span></span> |
| <span data-ttu-id="bd702-448">Metin</span><span class="sxs-lookup"><span data-stu-id="bd702-448">text</span></span> |<span data-ttu-id="bd702-449">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="bd702-449">String, Char[]</span></span> |
| <span data-ttu-id="bd702-450">time</span><span class="sxs-lookup"><span data-stu-id="bd702-450">time</span></span> |<span data-ttu-id="bd702-451">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="bd702-451">TimeSpan</span></span> |
| <span data-ttu-id="bd702-452">timestamp</span><span class="sxs-lookup"><span data-stu-id="bd702-452">timestamp</span></span> |<span data-ttu-id="bd702-453">Byte]</span><span class="sxs-lookup"><span data-stu-id="bd702-453">Byte[]</span></span> |
| <span data-ttu-id="bd702-454">Mini tamsayı</span><span class="sxs-lookup"><span data-stu-id="bd702-454">tinyint</span></span> |<span data-ttu-id="bd702-455">Bayt</span><span class="sxs-lookup"><span data-stu-id="bd702-455">Byte</span></span> |
| <span data-ttu-id="bd702-456">benzersiz tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="bd702-456">uniqueidentifier</span></span> |<span data-ttu-id="bd702-457">GUID</span><span class="sxs-lookup"><span data-stu-id="bd702-457">Guid</span></span> |
| <span data-ttu-id="bd702-458">varbinary</span><span class="sxs-lookup"><span data-stu-id="bd702-458">varbinary</span></span> |<span data-ttu-id="bd702-459">Byte]</span><span class="sxs-lookup"><span data-stu-id="bd702-459">Byte[]</span></span> |
| <span data-ttu-id="bd702-460">varchar</span><span class="sxs-lookup"><span data-stu-id="bd702-460">varchar</span></span> |<span data-ttu-id="bd702-461">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="bd702-461">String, Char[]</span></span> |
| <span data-ttu-id="bd702-462">xml</span><span class="sxs-lookup"><span data-stu-id="bd702-462">xml</span></span> |<span data-ttu-id="bd702-463">XML</span><span class="sxs-lookup"><span data-stu-id="bd702-463">Xml</span></span> |

<span data-ttu-id="bd702-464">Ayrıca, kaynak veri kümesi toocolumns hello kopyalama etkinliği tanımında havuz kümesinden sütunlarından eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd702-464">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="bd702-465">Ayrıntılar için bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="bd702-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a><span data-ttu-id="bd702-466">SQL veri ambarından veri tooand kopyalama için JSON örnekleri</span><span class="sxs-lookup"><span data-stu-id="bd702-466">JSON examples for copying data tooand from SQL Data Warehouse</span></span>
<span data-ttu-id="bd702-467">Merhaba aşağıdaki örneklerde sağlayan örnek JSON tanımları toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bd702-467">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="bd702-468">Bunlar Göster nasıl toocopy veri tooand Azure SQL Data Warehouse ve Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="bd702-468">They show how toocopy data tooand from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="bd702-469">Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden belirtildiği hello havuzlarını, kaynakları tooany [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="bd702-469">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a><span data-ttu-id="bd702-470">Örnek: Verilerini Azure SQL Data Warehouse tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="bd702-470">Example: Copy data from Azure SQL Data Warehouse tooAzure Blob</span></span>
<span data-ttu-id="bd702-471">Merhaba örnek Data Factory varlıklarını aşağıdaki hello tanımlar:</span><span class="sxs-lookup"><span data-stu-id="bd702-471">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="bd702-472">Bağlı hizmet türü [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bd702-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="bd702-473">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bd702-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="bd702-474">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bd702-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="bd702-475">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bd702-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="bd702-476">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [SqlDWSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="bd702-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="bd702-477">Merhaba örnek zaman serisi (saatlik, günlük, vs.) verileri Azure SQL Data Warehouse veritabanı tooa blob tablosunda her saat kopyalar.</span><span class="sxs-lookup"><span data-stu-id="bd702-477">hello sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database tooa blob every hour.</span></span> <span data-ttu-id="bd702-478">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="bd702-478">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="bd702-479">**Azure SQL Data Warehouse bağlantılı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="bd702-479">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="bd702-480">**Azure Blob storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="bd702-480">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="bd702-481">**Azure SQL veri ambarı veri kümesi giriş:**</span><span class="sxs-lookup"><span data-stu-id="bd702-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="bd702-482">Azure SQL Data Warehouse'da bir tablo "MyTable" oluşturulur ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği Hello örnek varsayar.</span><span class="sxs-lookup"><span data-stu-id="bd702-482">hello sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="bd702-483">"Dış" ayarı: "true" bildirir hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="bd702-483">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="bd702-484">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="bd702-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="bd702-485">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="bd702-485">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="bd702-486">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="bd702-486">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="bd702-487">Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="bd702-487">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="bd702-488">**SqlDWSource ve BlobSink ardışık düzeninde etkinlik kopyalayın:**</span><span class="sxs-lookup"><span data-stu-id="bd702-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="bd702-489">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="bd702-489">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="bd702-490">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**SqlDWSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="bd702-490">In hello pipeline JSON definition, hello **source** type is set too**SqlDWSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="bd702-491">Merhaba belirtilen hello SQL sorgusu **SqlReaderQuery** özelliği saat toocopy geçmiş hello hello veri seçer.</span><span class="sxs-lookup"><span data-stu-id="bd702-491">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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
> <span data-ttu-id="bd702-492">Merhaba örnekte **sqlReaderQuery** SqlDWSource hello için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="bd702-492">In hello example, **sqlReaderQuery** is specified for hello SqlDWSource.</span></span> <span data-ttu-id="bd702-493">Merhaba kopyalama etkinliği hello Azure SQL Data Warehouse kaynak tooget hello verileri karşı bu sorguyu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="bd702-493">hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>
>
> <span data-ttu-id="bd702-494">Alternatif olarak, bir saklı yordam hello belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (Merhaba saklı yordam parametreleri alır).</span><span class="sxs-lookup"><span data-stu-id="bd702-494">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="bd702-495">SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz, kullanılan toobuild bir sorgu (select column1, column2 mytable gelen) hello yapısı bölümünde JSON hello kümesinin tanımlanan hello sütunlar: hello Azure SQL Data Warehouse karşı toorun.</span><span class="sxs-lookup"><span data-stu-id="bd702-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (select column1, column2 from mytable) toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="bd702-496">Merhaba veri kümesi tanımı hello yapısına sahip değil, tüm sütunlar hello tablosundan seçilir.</span><span class="sxs-lookup"><span data-stu-id="bd702-496">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a><span data-ttu-id="bd702-497">Örnek: Kopyalama verileri Azure Blob tooAzure SQL veri ambarı</span><span class="sxs-lookup"><span data-stu-id="bd702-497">Example: Copy data from Azure Blob tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="bd702-498">Merhaba örnek Data Factory varlıklarını aşağıdaki hello tanımlar:</span><span class="sxs-lookup"><span data-stu-id="bd702-498">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="bd702-499">Bağlı hizmet türü [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bd702-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="bd702-500">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bd702-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="bd702-501">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bd702-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="bd702-502">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bd702-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="bd702-503">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) ve [SqlDWSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="bd702-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="bd702-504">Merhaba örnek time series verilerini (saatlik, günlük, vb.) Azure blob tooa Azure SQL Data Warehouse veritabanı tablosunda her saat kopyalar.</span><span class="sxs-lookup"><span data-stu-id="bd702-504">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="bd702-505">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="bd702-505">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="bd702-506">**Azure SQL Data Warehouse bağlantılı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="bd702-506">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="bd702-507">**Azure Blob storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="bd702-507">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="bd702-508">**Azure Blob girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="bd702-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="bd702-509">Veri toplanma yeni blob üzerinden saatte (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="bd702-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="bd702-510">Merhaba klasör yolu ve dosya adını hello blob dinamik olarak değerlendirilir işleniyor hello dilimin hello başlangıç zamanı temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="bd702-510">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="bd702-511">Merhaba klasör yolu yıl, ay ve gün kısmını hello başlangıç saati ve dosya adı hello başlangıç saati hello saat bölümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="bd702-511">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="bd702-512">"dış": "true" ayarı bu tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil hello Data Factory hizmetinin sizi bilgilendirir.</span><span class="sxs-lookup"><span data-stu-id="bd702-512">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="bd702-513">**Azure SQL veri ambarı veri kümesi çıkışını:**</span><span class="sxs-lookup"><span data-stu-id="bd702-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="bd702-514">Merhaba örnek Azure SQL Data Warehouse "MyTable" adlı veri tooa tablosuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="bd702-514">hello sample copies data tooa table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="bd702-515">Azure SQL Data Warehouse ile Merhaba tablosunu oluşturan hello Blob CSV dosyası toocontain beklediğiniz gibi hello aynı sayıda sütun.</span><span class="sxs-lookup"><span data-stu-id="bd702-515">Create hello table in Azure SQL Data Warehouse with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="bd702-516">Yeni satırlar toohello tablo saatte eklenir.</span><span class="sxs-lookup"><span data-stu-id="bd702-516">New rows are added toohello table every hour.</span></span>

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
<span data-ttu-id="bd702-517">**BlobSource ve SqlDWSink ardışık düzeninde etkinlik kopyalayın:**</span><span class="sxs-lookup"><span data-stu-id="bd702-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="bd702-518">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="bd702-518">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="bd702-519">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**BlobSource** ve **havuz** türü olarak ayarlanmış çok**SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="bd702-519">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlDWSink**.</span></span>

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
<span data-ttu-id="bd702-520">İçin bkz: hello bkz [1 TB altında 15 dakika Azure Data Factory ile Azure SQL Data Warehouse'a veri yükleme](data-factory-load-sql-data-warehouse.md) ve [Azure Data Factory ile veri yükleme](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) hello Azure SQL Data Warehouse makalesinde belgeler.</span><span class="sxs-lookup"><span data-stu-id="bd702-520">For a walkthrough, see hello see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in hello Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="bd702-521">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="bd702-521">Performance and Tuning</span></span>
<span data-ttu-id="bd702-522">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="bd702-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
