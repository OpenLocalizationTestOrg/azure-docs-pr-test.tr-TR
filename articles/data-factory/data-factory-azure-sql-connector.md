---
title: "Azure SQL veritabanı/aaaCopy verileri | Microsoft Docs"
description: "Bilgi nasıl/Azure Data Factory kullanarak Azure SQL veritabanı toocopy verileri."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="ad4ba-103">Azure SQL Azure Data Factory kullanarak veritabanından veri tooand kopyalama</span><span class="sxs-lookup"><span data-stu-id="ad4ba-103">Copy data tooand from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="ad4ba-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri tooand Azure SQL veritabanından de açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data tooand from Azure SQL Database.</span></span> <span data-ttu-id="ad4ba-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="ad4ba-106">Desteklenen senaryolar</span><span class="sxs-lookup"><span data-stu-id="ad4ba-106">Supported scenarios</span></span>
<span data-ttu-id="ad4ba-107">Veri kopyalama **Azure SQL veritabanından** veri depolarına aşağıdaki toohello:</span><span class="sxs-lookup"><span data-stu-id="ad4ba-107">You can copy data **from Azure SQL Database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="ad4ba-108">Veri depoları aşağıdaki hello verileri kopyalayabilirsiniz **tooAzure SQL veritabanı**:</span><span class="sxs-lookup"><span data-stu-id="ad4ba-108">You can copy data from hello following data stores **tooAzure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="ad4ba-109">Desteklenen kimlik doğrulama türü</span><span class="sxs-lookup"><span data-stu-id="ad4ba-109">Supported authentication type</span></span>
<span data-ttu-id="ad4ba-110">Azure SQL Veritabanı Bağlayıcısı temel kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ad4ba-111">Başlarken</span><span class="sxs-lookup"><span data-stu-id="ad4ba-111">Getting started</span></span>
<span data-ttu-id="ad4ba-112">Farklı araçlar/API'lerini kullanarak bir Azure SQL veritabanından/gelen verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="ad4ba-113">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-113">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="ad4ba-114">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="ad4ba-115">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-115">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ad4ba-116">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="ad4ba-117">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ad4ba-117">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="ad4ba-118">Oluşturma bir **veri fabrikası**.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-118">Create a **data factory**.</span></span> <span data-ttu-id="ad4ba-119">Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="ad4ba-120">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-120">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="ad4ba-121">Bir Azure blob depolama tooan Azure SQL veritabanından veri kopyalama, örneğin, iki bağlı hizmet toolink Azure depolama hesabınız ve Azure SQL veritabanı tooyour veri fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-121">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="ad4ba-122">Belirli tooAzure SQL veritabanı bağlantılı hizmet özellikler için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-122">For linked service properties that are specific tooAzure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="ad4ba-123">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="ad4ba-124">Merhaba son adımda bahsedilen hello örnekte, bir veri kümesi toospecify hello blob kapsayıcısı ve hello giriş verisi içeren klasörü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-124">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="ad4ba-125">Ve hello blob depolama biriminden kopyalanan hello verilerini tutan hello Azure SQL veritabanında başka bir veri kümesi toospecify hello SQL tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-125">And, you create another dataset toospecify hello SQL table in hello Azure SQL database  that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="ad4ba-126">Belirli tooAzure Data Lake Store dataset özellikler için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-126">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="ad4ba-127">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="ad4ba-128">Daha önce bahsedilen hello örnekte BlobSource bir kaynak ve SqlSink havuzu olarak hello kopya etkinliği için kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-128">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="ad4ba-129">Azure SQL veritabanı tooAzure Blob Depolama kopyalıyorsanız benzer şekilde, SqlSource ve BlobSink hello kopyalama etkinliği kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-129">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="ad4ba-130">Belirli tooAzure SQL veritabanını kopyalama etkinliği özellikler için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-130">For copy activity properties that are specific tooAzure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="ad4ba-131">Nasıl toouse bir veri deposu bir kaynak veya bir havuz olarak hakkında daha fazla bilgi için veri deposu hello önceki bölümdeki hello bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-131">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="ad4ba-132">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-132">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="ad4ba-133">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="ad4ba-134">Bir Azure SQL veritabanı/kullanılan toocopy verileri olan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-to-and-from-sql-database) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-134">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="ad4ba-135">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooAzure SQL veritabanı olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="ad4ba-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="ad4ba-136">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="ad4ba-136">Linked service properties</span></span>
<span data-ttu-id="ad4ba-137">Bir Azure SQL hizmeti bir Azure SQL veritabanı tooyour data factory bağlantılı.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-137">An Azure SQL linked service links an Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="ad4ba-138">Aşağıdaki tablonun hello JSON öğeleri belirli tooAzure SQL açıklamasını bağlantılı hizmetinin sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-138">hello following table provides description for JSON elements specific tooAzure SQL linked service.</span></span>

| <span data-ttu-id="ad4ba-139">Özellik</span><span class="sxs-lookup"><span data-stu-id="ad4ba-139">Property</span></span> | <span data-ttu-id="ad4ba-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ad4ba-140">Description</span></span> | <span data-ttu-id="ad4ba-141">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ad4ba-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad4ba-142">type</span><span class="sxs-lookup"><span data-stu-id="ad4ba-142">type</span></span> |<span data-ttu-id="ad4ba-143">Merhaba type özelliği ayarlanmalıdır: **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="ad4ba-143">hello type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="ad4ba-144">Evet</span><span class="sxs-lookup"><span data-stu-id="ad4ba-144">Yes</span></span> |
| <span data-ttu-id="ad4ba-145">connectionString</span><span class="sxs-lookup"><span data-stu-id="ad4ba-145">connectionString</span></span> |<span data-ttu-id="ad4ba-146">Tooconnect toohello Azure SQL veritabanı örneğinde hello connectionString özelliği için gerekli bilgiler belirtin.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-146">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> <span data-ttu-id="ad4ba-147">Yalnızca temel kimlik doğrulama desteklenir.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="ad4ba-148">Evet</span><span class="sxs-lookup"><span data-stu-id="ad4ba-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="ad4ba-149">Yapılandırma [Azure SQL veritabanı Güvenlik Duvarı](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) veritabanı sunucusu çok hello[Azure Hizmetleri tooaccess hello sunucusu izin](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="ad4ba-150">Ayrıca, dış Azure veri fabrikası ağ geçidi ile şirket içi veri kaynaklarından dahil olmak üzere veri tooAzure SQL veritabanı kopyalıyorsanız, veri tooAzure SQL veritabanı gönderme hello makine için uygun IP adresi aralığı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-150">Additionally, if you are copying data tooAzure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="ad4ba-151">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="ad4ba-151">Dataset properties</span></span>
<span data-ttu-id="ad4ba-152">toospecify dataset toorepresent giriş veya çıkış verisi bir Azure SQL veritabanında hello türü özelliği için hello kümesinin ayarlayın: **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-152">toospecify a dataset toorepresent input or output data in an Azure SQL database, you set hello type property of hello dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="ad4ba-153">Set hello **linkedServiceName** özelliği hello dataset toohello adının hello Azure SQL bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-153">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure SQL linked service.</span></span>  

<span data-ttu-id="ad4ba-154">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-154">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="ad4ba-155">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="ad4ba-156">Merhaba typeProperties bölümü veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-156">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="ad4ba-157">Merhaba **typeProperties** hello veri kümesi için bir bölüm türü **AzureSqlTable** hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="ad4ba-157">hello **typeProperties** section for hello dataset of type **AzureSqlTable** has hello following properties:</span></span>

| <span data-ttu-id="ad4ba-158">Özellik</span><span class="sxs-lookup"><span data-stu-id="ad4ba-158">Property</span></span> | <span data-ttu-id="ad4ba-159">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ad4ba-159">Description</span></span> | <span data-ttu-id="ad4ba-160">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ad4ba-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad4ba-161">tableName</span><span class="sxs-lookup"><span data-stu-id="ad4ba-161">tableName</span></span> |<span data-ttu-id="ad4ba-162">Merhaba tablo veya Görünüm hizmeti bağlı hello Azure SQL veritabanı örneğinde başvurduğu adı.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-162">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="ad4ba-163">Evet</span><span class="sxs-lookup"><span data-stu-id="ad4ba-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="ad4ba-164">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="ad4ba-164">Copy activity properties</span></span>
<span data-ttu-id="ad4ba-165">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-165">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ad4ba-166">Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="ad4ba-167">Merhaba kopyalama etkinliği yalnızca bir girdi alır ve tek bir çıktı üretir.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-167">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="ad4ba-168">Oysa hello kullanılabilen özellikleri **typeProperties** hello etkinlik bölümünü her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-168">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="ad4ba-169">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-169">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="ad4ba-170">Bir Azure SQL veritabanından veri taşıyorsanız, hello kaynak türü hello kopyalama etkinliği çok ayarladığınız**SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-170">If you are moving data from an Azure SQL database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="ad4ba-171">Veri tooan Azure SQL veritabanını taşıyorsanız, benzer şekilde, hello Havuz türü hello kopyalama etkinliği çok ayarladığınız**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-171">Similarly, if you are moving data tooan Azure SQL database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="ad4ba-172">Bu bölümde SqlSource ve SqlSink tarafından desteklenen özellikler listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="ad4ba-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="ad4ba-173">SqlSource</span></span>
<span data-ttu-id="ad4ba-174">Kopyalama etkinliğinde hello kaynak türü olduğunda **SqlSource**, aşağıdaki özelliklere hello kullanılabilir **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="ad4ba-174">In copy activity, when hello source is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="ad4ba-175">Özellik</span><span class="sxs-lookup"><span data-stu-id="ad4ba-175">Property</span></span> | <span data-ttu-id="ad4ba-176">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ad4ba-176">Description</span></span> | <span data-ttu-id="ad4ba-177">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="ad4ba-177">Allowed values</span></span> | <span data-ttu-id="ad4ba-178">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ad4ba-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ad4ba-179">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="ad4ba-179">sqlReaderQuery</span></span> |<span data-ttu-id="ad4ba-180">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-180">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ad4ba-181">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-181">SQL query string.</span></span> <span data-ttu-id="ad4ba-182">Örnek: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="ad4ba-183">Hayır</span><span class="sxs-lookup"><span data-stu-id="ad4ba-183">No</span></span> |
| <span data-ttu-id="ad4ba-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="ad4ba-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="ad4ba-185">Merhaba adını hello kaynak tablodan veri okuyan yordamı depolanır.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-185">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="ad4ba-186">Saklı yordam hello adı.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-186">Name of hello stored procedure.</span></span> <span data-ttu-id="ad4ba-187">Merhaba son SQL deyimi SELECT deyimi hello saklı yordam içinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-187">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="ad4ba-188">Hayır</span><span class="sxs-lookup"><span data-stu-id="ad4ba-188">No</span></span> |
| <span data-ttu-id="ad4ba-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ad4ba-189">storedProcedureParameters</span></span> |<span data-ttu-id="ad4ba-190">Saklı yordam hello için parametreler.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-190">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="ad4ba-191">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-191">Name/value pairs.</span></span> <span data-ttu-id="ad4ba-192">Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-192">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="ad4ba-193">Hayır</span><span class="sxs-lookup"><span data-stu-id="ad4ba-193">No</span></span> |

<span data-ttu-id="ad4ba-194">Merhaba, **sqlReaderQuery** Merhaba SqlSource, hello kopyalama etkinliği çalıştıran bu sorguyu hello Azure SQL veritabanı kaynak tooget hello verileri karşı belirtilir.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-194">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="ad4ba-195">Alternatif olarak, bir saklı yordam hello belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (Merhaba saklı yordam parametreleri alır).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-195">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="ad4ba-196">SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz, kullanılan toobuild bir sorgu hello yapısı bölümünde JSON hello kümesinin tanımlanan hello sütunlar: (`select column1, column2 from mytable`) hello Azure SQL veritabanına karşı toorun.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (`select column1, column2 from mytable`) toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="ad4ba-197">Merhaba veri kümesi tanımı hello yapısına sahip değil, tüm sütunlar hello tablosundan seçilir.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="ad4ba-198">Kullandığınızda, **sqlReaderStoredProcedureName**, hala toospecify bir değer hello için gereksinim duyduğunuz **tableName** JSON hello kümesindeki özelliği.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-198">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="ad4ba-199">Yine de bu tabloya karşı gerçekleştirilen başka doğrulama vardır.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="ad4ba-200">SqlSource örneği</span><span class="sxs-lookup"><span data-stu-id="ad4ba-200">SqlSource example</span></span>

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

<span data-ttu-id="ad4ba-201">**Merhaba saklı yordamı tanımı:**</span><span class="sxs-lookup"><span data-stu-id="ad4ba-201">**hello stored procedure definition:**</span></span>

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

### <a name="sqlsink"></a><span data-ttu-id="ad4ba-202">SqlSink</span><span class="sxs-lookup"><span data-stu-id="ad4ba-202">SqlSink</span></span>
<span data-ttu-id="ad4ba-203">**SqlSink** aşağıdaki özelliklere hello destekler:</span><span class="sxs-lookup"><span data-stu-id="ad4ba-203">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="ad4ba-204">Özellik</span><span class="sxs-lookup"><span data-stu-id="ad4ba-204">Property</span></span> | <span data-ttu-id="ad4ba-205">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ad4ba-205">Description</span></span> | <span data-ttu-id="ad4ba-206">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="ad4ba-206">Allowed values</span></span> | <span data-ttu-id="ad4ba-207">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ad4ba-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ad4ba-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="ad4ba-208">writeBatchTimeout</span></span> |<span data-ttu-id="ad4ba-209">Zaman aşımına uğramadan önce hello toplu ekleme işlemi toocomplete bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-209">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="ad4ba-210">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="ad4ba-210">timespan</span></span><br/><br/> <span data-ttu-id="ad4ba-211">Örnek: "00: 30:00" (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="ad4ba-212">Hayır</span><span class="sxs-lookup"><span data-stu-id="ad4ba-212">No</span></span> |
| <span data-ttu-id="ad4ba-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ad4ba-213">writeBatchSize</span></span> |<span data-ttu-id="ad4ba-214">Merhaba arabellek boyutu writeBatchSize ulaştığında veri hello SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-214">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="ad4ba-215">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="ad4ba-215">Integer (number of rows)</span></span> |<span data-ttu-id="ad4ba-216">Hayır (varsayılan: 10000)</span><span class="sxs-lookup"><span data-stu-id="ad4ba-216">No (default: 10000)</span></span> |
| <span data-ttu-id="ad4ba-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="ad4ba-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="ad4ba-218">Belirli bir dilimle verilerinin temizlenmesini gibi bir sorgu için kopyalama etkinliği tooexecute belirtin.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-218">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="ad4ba-219">Daha fazla bilgi için bkz: [yinelenebilir kopyalama](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="ad4ba-220">Sorgu bildirimi.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-220">A query statement.</span></span> |<span data-ttu-id="ad4ba-221">Hayır</span><span class="sxs-lookup"><span data-stu-id="ad4ba-221">No</span></span> |
| <span data-ttu-id="ad4ba-222">Sliceıdentifiercolumnname</span><span class="sxs-lookup"><span data-stu-id="ad4ba-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="ad4ba-223">Kopyalama etkinliği toofill bir sütun adı, ne zaman yeniden çalıştırılacağını belirli bir dilim verilerini kullanılan tooclean olduğu otomatik dilim tanımlayıcı ile belirtin.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-223">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="ad4ba-224">Daha fazla bilgi için bkz: [yinelenebilir kopyalama](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="ad4ba-225">Binary(32) veri türüne sahip bir sütunun sütun adı.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="ad4ba-226">Hayır</span><span class="sxs-lookup"><span data-stu-id="ad4ba-226">No</span></span> |
| <span data-ttu-id="ad4ba-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="ad4ba-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="ad4ba-228">Merhaba adını upserts (güncelleştirmeler/ekler) verileri hello hedef tabloya saklı yordamı.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-228">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="ad4ba-229">Saklı yordam hello adı.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-229">Name of hello stored procedure.</span></span> |<span data-ttu-id="ad4ba-230">Hayır</span><span class="sxs-lookup"><span data-stu-id="ad4ba-230">No</span></span> |
| <span data-ttu-id="ad4ba-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ad4ba-231">storedProcedureParameters</span></span> |<span data-ttu-id="ad4ba-232">Saklı yordam hello için parametreler.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-232">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="ad4ba-233">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-233">Name/value pairs.</span></span> <span data-ttu-id="ad4ba-234">Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-234">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="ad4ba-235">Hayır</span><span class="sxs-lookup"><span data-stu-id="ad4ba-235">No</span></span> |
| <span data-ttu-id="ad4ba-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="ad4ba-236">sqlWriterTableType</span></span> |<span data-ttu-id="ad4ba-237">Merhaba saklı yordamda kullanılan bir tablo türü adı toobe belirtin.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-237">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="ad4ba-238">Kopyalama etkinliği taşınan hello veri geçici bir tablo bu tablo türü ile kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-238">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="ad4ba-239">Saklı yordam kodu sonra varolan verilerin kopyalanmasını hello verileri birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-239">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="ad4ba-240">Bir tablo türü adı.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-240">A table type name.</span></span> |<span data-ttu-id="ad4ba-241">Hayır</span><span class="sxs-lookup"><span data-stu-id="ad4ba-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="ad4ba-242">SqlSink örneği</span><span class="sxs-lookup"><span data-stu-id="ad4ba-242">SqlSink example</span></span>

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a><span data-ttu-id="ad4ba-243">SQL veritabanından veri tooand kopyalamak için JSON örnekleri</span><span class="sxs-lookup"><span data-stu-id="ad4ba-243">JSON examples for copying data tooand from SQL Database</span></span>
<span data-ttu-id="ad4ba-244">Merhaba aşağıdaki örneklerde sağlayan örnek JSON tanımları toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-244">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="ad4ba-245">Bunlar Göster nasıl toocopy veri tooand Azure SQL Database ve Azure Blob depolama alanından.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-245">They show how toocopy data tooand from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="ad4ba-246">Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden belirtildiği hello havuzlarını, kaynakları tooany [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-246">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a><span data-ttu-id="ad4ba-247">Örnek: Verilerini Azure SQL veritabanı tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="ad4ba-247">Example: Copy data from Azure SQL Database tooAzure Blob</span></span>
<span data-ttu-id="ad4ba-248">Merhaba aynı Data Factory varlıklarını aşağıdaki hello tanımlar:</span><span class="sxs-lookup"><span data-stu-id="ad4ba-248">hello same defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="ad4ba-249">Bağlı hizmet türü [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="ad4ba-250">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ad4ba-251">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="ad4ba-252">Bir çıkış [dataset](data-factory-create-datasets.md) türü [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="ad4ba-253">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [SqlSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="ad4ba-254">Merhaba örnek time series verilerini (saatlik, günlük, vb.) Azure SQL veritabanı tooa blob tablosunda her saat kopyalar.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-254">hello sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database tooa blob every hour.</span></span> <span data-ttu-id="ad4ba-255">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-255">hello JSON properties used in these samples are described in sections following hello samples.</span></span>  

<span data-ttu-id="ad4ba-256">**Azure SQL Database hizmeti bağlı:**</span><span class="sxs-lookup"><span data-stu-id="ad4ba-256">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="ad4ba-257">Merhaba bkz [Azure SQL bağlı hizmeti](#linked-service) hello listesi için bu bağlantılı hizmet tarafından desteklenen özellikler bölümü.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-257">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="ad4ba-258">**Azure Blob storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="ad4ba-258">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="ad4ba-259">Merhaba bkz [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) bu bağlantılı hizmet tarafından desteklenen özellikler hello listesi için makale.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-259">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="ad4ba-260">**Azure SQL girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="ad4ba-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="ad4ba-261">Merhaba örnek "MyTable" Azure SQL tablosu oluşturdunuz ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-261">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="ad4ba-262">"Dış" ayarı: "true" bildirir hello Azure Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-262">Setting “external”: ”true” informs hello Azure Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

<span data-ttu-id="ad4ba-263">Merhaba bkz [Azure SQL veri kümesi türü özellikleri](#dataset) hello listesi için bu veri kümesi türü tarafından desteklenen özellikler bölümü.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-263">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="ad4ba-264">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="ad4ba-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="ad4ba-265">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-265">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ad4ba-266">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-266">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="ad4ba-267">Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-267">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
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
<span data-ttu-id="ad4ba-268">Merhaba bkz [Azure Blob veri kümesi türü özellikleri](data-factory-azure-blob-connector.md#dataset-properties) hello listesi için bu veri kümesi türü tarafından desteklenen özellikler bölümü.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-268">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="ad4ba-269">**SQL kaynak ve Blob havuz sahip işlem hattı kopyalama etkinliğinde:**</span><span class="sxs-lookup"><span data-stu-id="ad4ba-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="ad4ba-270">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-270">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="ad4ba-271">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**SqlSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-271">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="ad4ba-272">Merhaba belirtilen hello SQL sorgusu **SqlReaderQuery** özelliği saat toocopy geçmiş hello hello veri seçer.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-272">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
<span data-ttu-id="ad4ba-273">Merhaba örnekte **sqlReaderQuery** SqlSource hello için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-273">In hello example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="ad4ba-274">Merhaba kopyalama etkinliği hello Azure SQL veritabanı kaynak tooget hello verilerine karşı bu sorguyu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-274">hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="ad4ba-275">Alternatif olarak, bir saklı yordam hello belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (Merhaba saklı yordam parametreleri alır).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-275">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="ad4ba-276">SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz hello yapısı bölümünde JSON hello kümesinin tanımlanan hello sütunlar kullanılan toobuild hello Azure SQL veritabanına karşı sorgu toorun'dır.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="ad4ba-277">Örneğin: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="ad4ba-278">Merhaba veri kümesi tanımı hello yapısına sahip değil, tüm sütunlar hello tablosundan seçilir.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-278">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="ad4ba-279">Hello bkz [Sql kaynağı](#sqlsource) bölüm ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) SqlSource ve BlobSink tarafından desteklenen özellikler hello listesi.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-279">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a><span data-ttu-id="ad4ba-280">Örnek: Kopyalama verileri Azure Blob tooAzure SQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="ad4ba-280">Example: Copy data from Azure Blob tooAzure SQL Database</span></span>
<span data-ttu-id="ad4ba-281">Merhaba örnek Data Factory varlıklarını aşağıdaki hello tanımlar:</span><span class="sxs-lookup"><span data-stu-id="ad4ba-281">hello sample defines hello following Data Factory entities:</span></span>  

1. <span data-ttu-id="ad4ba-282">Bağlı hizmet türü [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="ad4ba-283">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ad4ba-284">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="ad4ba-285">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="ad4ba-286">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) ve [SqlSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="ad4ba-287">Merhaba örnek time series verilerini (saatlik, günlük, vb.) Azure blob tooa Azure SQL veritabanı tablosunda her saat kopyalar.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-287">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL database every hour.</span></span> <span data-ttu-id="ad4ba-288">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-288">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="ad4ba-289">**Azure SQL bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="ad4ba-289">**Azure SQL linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="ad4ba-290">Merhaba bkz [Azure SQL bağlı hizmeti](#linked-service) hello listesi için bu bağlantılı hizmet tarafından desteklenen özellikler bölümü.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-290">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="ad4ba-291">**Azure Blob storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="ad4ba-291">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="ad4ba-292">Merhaba bkz [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) bu bağlantılı hizmet tarafından desteklenen özellikler hello listesi için makale.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-292">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="ad4ba-293">**Azure Blob girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="ad4ba-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="ad4ba-294">Veri toplanma yeni blob üzerinden saatte (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ad4ba-295">Merhaba klasör yolu ve dosya adını hello blob dinamik olarak değerlendirilir işleniyor hello dilimin hello başlangıç zamanı temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-295">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="ad4ba-296">Merhaba klasör yolu yıl, ay ve gün kısmını hello başlangıç saati ve dosya adı hello başlangıç saati hello saat bölümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-296">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="ad4ba-297">"dış": "true" ayarı bu tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil hello Data Factory hizmetinin sizi bilgilendirir.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-297">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
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
<span data-ttu-id="ad4ba-298">Merhaba bkz [Azure Blob veri kümesi türü özellikleri](data-factory-azure-blob-connector.md#dataset-properties) hello listesi için bu veri kümesi türü tarafından desteklenen özellikler bölümü.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-298">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="ad4ba-299">**Azure SQL veritabanı veri kümesini çıktı:**</span><span class="sxs-lookup"><span data-stu-id="ad4ba-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="ad4ba-300">Merhaba örnek Azure SQL "MyTable" olarak adlandırılan veri tooa tablosuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-300">hello sample copies data tooa table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="ad4ba-301">Azure SQL ile Merhaba tablo oluşturmak hello Blob CSV dosyası toocontain beklediğiniz gibi hello aynı sayıda sütun.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-301">Create hello table in Azure SQL with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="ad4ba-302">Yeni satırlar toohello tablo saatte eklenir.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-302">New rows are added toohello table every hour.</span></span>

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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
<span data-ttu-id="ad4ba-303">Merhaba bkz [Azure SQL veri kümesi türü özellikleri](#dataset) hello listesi için bu veri kümesi türü tarafından desteklenen özellikler bölümü.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-303">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="ad4ba-304">**Blob kaynağı ve SQL havuz sahip işlem hattı kopyalama etkinliğinde:**</span><span class="sxs-lookup"><span data-stu-id="ad4ba-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="ad4ba-305">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-305">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="ad4ba-306">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**BlobSource** ve **havuz** türü olarak ayarlanmış çok**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-306">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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
<span data-ttu-id="ad4ba-307">Hello bkz [Sql havuz](#sqlsink) bölüm ve [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) SqlSink ve BlobSource tarafından desteklenen özellikler hello listesi.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-307">See hello [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="ad4ba-308">Merhaba hedef veritabanında kimlik sütunu</span><span class="sxs-lookup"><span data-stu-id="ad4ba-308">Identity columns in hello target database</span></span>
<span data-ttu-id="ad4ba-309">Bu bölümde, bir kimlik sütunu tooa hedef tabloyla bir kimlik sütunu olmayan bir kaynak tablodan veri kopyalamak için bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-309">This section provides an example for copying data from a source table without an identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="ad4ba-310">**Kaynak tablosu:**</span><span class="sxs-lookup"><span data-stu-id="ad4ba-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="ad4ba-311">**Hedef Tablo:**</span><span class="sxs-lookup"><span data-stu-id="ad4ba-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="ad4ba-312">Merhaba hedef tablosunun bir kimlik sütunu olan dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-312">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="ad4ba-313">**Kaynak veri kümesi JSON tanımı**</span><span class="sxs-lookup"><span data-stu-id="ad4ba-313">**Source dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="ad4ba-314">**Hedef veri kümesi JSON tanımı**</span><span class="sxs-lookup"><span data-stu-id="ad4ba-314">**Destination dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

<span data-ttu-id="ad4ba-315">Kaynak ve hedef tablosu farklı şema sahip dikkat edin (hedef kimliğine sahip başka bir sütuna sahip).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="ad4ba-316">Bu senaryoda, toospecify gerek **yapısı** hello kimlik sütunu içermeyen hello hedef veri kümesi tanımında özelliği.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-316">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="ad4ba-317">SQL havuz depolanan yordamı çağırma</span><span class="sxs-lookup"><span data-stu-id="ad4ba-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="ad4ba-318">Kopyalama etkinliği ardışık SQL havuzunda bir saklı yordam çağırma bir örnek için bkz: [kopyalama etkinliği SQL havuz için saklı yordam çağırma](data-factory-invoke-stored-procedure-from-copy-activity.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="ad4ba-319">Tür eşlemesi için Azure SQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="ad4ba-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="ad4ba-320">Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale kopyalama etkinliği ile 2 adımlı yaklaşımı izleyerek hello kaynak türleri toosink türlerinden otomatik tür dönüşümleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="ad4ba-320">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="ad4ba-321">Yerel kaynak türleri too.NET türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="ad4ba-321">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="ad4ba-322">.NET türü toonative havuz türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="ad4ba-322">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="ad4ba-323">Azure SQL veritabanından veri tooand taşırken, hello aşağıdaki eşlemelerini too.NET türü ve bunun tersi de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-323">When moving data tooand from Azure SQL Database, hello following mappings are used from SQL type too.NET type and vice versa.</span></span> <span data-ttu-id="ad4ba-324">Merhaba eşleme hello ADO.NET için SQL Server veri türü eşlemesi olarak aynıdır.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-324">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="ad4ba-325">SQL Server veritabanı altyapısı türü</span><span class="sxs-lookup"><span data-stu-id="ad4ba-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="ad4ba-326">.NET framework türü</span><span class="sxs-lookup"><span data-stu-id="ad4ba-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="ad4ba-327">bigint</span><span class="sxs-lookup"><span data-stu-id="ad4ba-327">bigint</span></span> |<span data-ttu-id="ad4ba-328">Int64</span><span class="sxs-lookup"><span data-stu-id="ad4ba-328">Int64</span></span> |
| <span data-ttu-id="ad4ba-329">İkili</span><span class="sxs-lookup"><span data-stu-id="ad4ba-329">binary</span></span> |<span data-ttu-id="ad4ba-330">Byte]</span><span class="sxs-lookup"><span data-stu-id="ad4ba-330">Byte[]</span></span> |
| <span data-ttu-id="ad4ba-331">bit</span><span class="sxs-lookup"><span data-stu-id="ad4ba-331">bit</span></span> |<span data-ttu-id="ad4ba-332">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="ad4ba-332">Boolean</span></span> |
| <span data-ttu-id="ad4ba-333">char</span><span class="sxs-lookup"><span data-stu-id="ad4ba-333">char</span></span> |<span data-ttu-id="ad4ba-334">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="ad4ba-334">String, Char[]</span></span> |
| <span data-ttu-id="ad4ba-335">Tarih</span><span class="sxs-lookup"><span data-stu-id="ad4ba-335">date</span></span> |<span data-ttu-id="ad4ba-336">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="ad4ba-336">DateTime</span></span> |
| <span data-ttu-id="ad4ba-337">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="ad4ba-337">Datetime</span></span> |<span data-ttu-id="ad4ba-338">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="ad4ba-338">DateTime</span></span> |
| <span data-ttu-id="ad4ba-339">datetime2</span><span class="sxs-lookup"><span data-stu-id="ad4ba-339">datetime2</span></span> |<span data-ttu-id="ad4ba-340">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="ad4ba-340">DateTime</span></span> |
| <span data-ttu-id="ad4ba-341">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="ad4ba-341">Datetimeoffset</span></span> |<span data-ttu-id="ad4ba-342">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="ad4ba-342">DateTimeOffset</span></span> |
| <span data-ttu-id="ad4ba-343">Ondalık</span><span class="sxs-lookup"><span data-stu-id="ad4ba-343">Decimal</span></span> |<span data-ttu-id="ad4ba-344">Ondalık</span><span class="sxs-lookup"><span data-stu-id="ad4ba-344">Decimal</span></span> |
| <span data-ttu-id="ad4ba-345">FILESTREAM özniteliği (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="ad4ba-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="ad4ba-346">Byte]</span><span class="sxs-lookup"><span data-stu-id="ad4ba-346">Byte[]</span></span> |
| <span data-ttu-id="ad4ba-347">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="ad4ba-347">Float</span></span> |<span data-ttu-id="ad4ba-348">Çift</span><span class="sxs-lookup"><span data-stu-id="ad4ba-348">Double</span></span> |
| <span data-ttu-id="ad4ba-349">Görüntü</span><span class="sxs-lookup"><span data-stu-id="ad4ba-349">image</span></span> |<span data-ttu-id="ad4ba-350">Byte]</span><span class="sxs-lookup"><span data-stu-id="ad4ba-350">Byte[]</span></span> |
| <span data-ttu-id="ad4ba-351">Int</span><span class="sxs-lookup"><span data-stu-id="ad4ba-351">int</span></span> |<span data-ttu-id="ad4ba-352">Int32</span><span class="sxs-lookup"><span data-stu-id="ad4ba-352">Int32</span></span> |
| <span data-ttu-id="ad4ba-353">para</span><span class="sxs-lookup"><span data-stu-id="ad4ba-353">money</span></span> |<span data-ttu-id="ad4ba-354">Ondalık</span><span class="sxs-lookup"><span data-stu-id="ad4ba-354">Decimal</span></span> |
| <span data-ttu-id="ad4ba-355">nchar</span><span class="sxs-lookup"><span data-stu-id="ad4ba-355">nchar</span></span> |<span data-ttu-id="ad4ba-356">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="ad4ba-356">String, Char[]</span></span> |
| <span data-ttu-id="ad4ba-357">ntext</span><span class="sxs-lookup"><span data-stu-id="ad4ba-357">ntext</span></span> |<span data-ttu-id="ad4ba-358">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="ad4ba-358">String, Char[]</span></span> |
| <span data-ttu-id="ad4ba-359">sayısal</span><span class="sxs-lookup"><span data-stu-id="ad4ba-359">numeric</span></span> |<span data-ttu-id="ad4ba-360">Ondalık</span><span class="sxs-lookup"><span data-stu-id="ad4ba-360">Decimal</span></span> |
| <span data-ttu-id="ad4ba-361">nvarchar</span><span class="sxs-lookup"><span data-stu-id="ad4ba-361">nvarchar</span></span> |<span data-ttu-id="ad4ba-362">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="ad4ba-362">String, Char[]</span></span> |
| <span data-ttu-id="ad4ba-363">Gerçek</span><span class="sxs-lookup"><span data-stu-id="ad4ba-363">real</span></span> |<span data-ttu-id="ad4ba-364">Tek</span><span class="sxs-lookup"><span data-stu-id="ad4ba-364">Single</span></span> |
| <span data-ttu-id="ad4ba-365">rowVersion</span><span class="sxs-lookup"><span data-stu-id="ad4ba-365">rowversion</span></span> |<span data-ttu-id="ad4ba-366">Byte]</span><span class="sxs-lookup"><span data-stu-id="ad4ba-366">Byte[]</span></span> |
| <span data-ttu-id="ad4ba-367">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="ad4ba-367">smalldatetime</span></span> |<span data-ttu-id="ad4ba-368">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="ad4ba-368">DateTime</span></span> |
| <span data-ttu-id="ad4ba-369">tamsayı</span><span class="sxs-lookup"><span data-stu-id="ad4ba-369">smallint</span></span> |<span data-ttu-id="ad4ba-370">Int16</span><span class="sxs-lookup"><span data-stu-id="ad4ba-370">Int16</span></span> |
| <span data-ttu-id="ad4ba-371">küçük para</span><span class="sxs-lookup"><span data-stu-id="ad4ba-371">smallmoney</span></span> |<span data-ttu-id="ad4ba-372">Ondalık</span><span class="sxs-lookup"><span data-stu-id="ad4ba-372">Decimal</span></span> |
| <span data-ttu-id="ad4ba-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="ad4ba-373">sql_variant</span></span> |<span data-ttu-id="ad4ba-374">Nesne *</span><span class="sxs-lookup"><span data-stu-id="ad4ba-374">Object *</span></span> |
| <span data-ttu-id="ad4ba-375">Metin</span><span class="sxs-lookup"><span data-stu-id="ad4ba-375">text</span></span> |<span data-ttu-id="ad4ba-376">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="ad4ba-376">String, Char[]</span></span> |
| <span data-ttu-id="ad4ba-377">time</span><span class="sxs-lookup"><span data-stu-id="ad4ba-377">time</span></span> |<span data-ttu-id="ad4ba-378">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="ad4ba-378">TimeSpan</span></span> |
| <span data-ttu-id="ad4ba-379">timestamp</span><span class="sxs-lookup"><span data-stu-id="ad4ba-379">timestamp</span></span> |<span data-ttu-id="ad4ba-380">Byte]</span><span class="sxs-lookup"><span data-stu-id="ad4ba-380">Byte[]</span></span> |
| <span data-ttu-id="ad4ba-381">Mini tamsayı</span><span class="sxs-lookup"><span data-stu-id="ad4ba-381">tinyint</span></span> |<span data-ttu-id="ad4ba-382">Bayt</span><span class="sxs-lookup"><span data-stu-id="ad4ba-382">Byte</span></span> |
| <span data-ttu-id="ad4ba-383">benzersiz tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="ad4ba-383">uniqueidentifier</span></span> |<span data-ttu-id="ad4ba-384">GUID</span><span class="sxs-lookup"><span data-stu-id="ad4ba-384">Guid</span></span> |
| <span data-ttu-id="ad4ba-385">varbinary</span><span class="sxs-lookup"><span data-stu-id="ad4ba-385">varbinary</span></span> |<span data-ttu-id="ad4ba-386">Byte]</span><span class="sxs-lookup"><span data-stu-id="ad4ba-386">Byte[]</span></span> |
| <span data-ttu-id="ad4ba-387">varchar</span><span class="sxs-lookup"><span data-stu-id="ad4ba-387">varchar</span></span> |<span data-ttu-id="ad4ba-388">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="ad4ba-388">String, Char[]</span></span> |
| <span data-ttu-id="ad4ba-389">xml</span><span class="sxs-lookup"><span data-stu-id="ad4ba-389">xml</span></span> |<span data-ttu-id="ad4ba-390">XML</span><span class="sxs-lookup"><span data-stu-id="ad4ba-390">Xml</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="ad4ba-391">Kaynak toosink sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="ad4ba-391">Map source toosink columns</span></span>
<span data-ttu-id="ad4ba-392">Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-392">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="ad4ba-393">Yinelenebilir kopyalama</span><span class="sxs-lookup"><span data-stu-id="ad4ba-393">Repeatable copy</span></span>
<span data-ttu-id="ad4ba-394">Veri tooSQL sunucu veritabanı kopyalama işlemi sırasında hello kopyalama etkinliği varsayılan olarak veri toohello havuz tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-394">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="ad4ba-395">Bunun yerine, tooperform bir UPSERT bkz [yinelenebilir yazma tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-395">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="ad4ba-396">İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-396">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="ad4ba-397">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="ad4ba-398">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="ad4ba-399">Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-399">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="ad4ba-400">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="ad4ba-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="ad4ba-401">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="ad4ba-401">Performance and Tuning</span></span>
<span data-ttu-id="ad4ba-402">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="ad4ba-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
