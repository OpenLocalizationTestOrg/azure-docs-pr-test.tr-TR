---
title: "Veri kopyalama/Azure SQL veritabanından | Microsoft Docs"
description: "İçin/Azure SQL veritabanından Azure Data Factory kullanarak verileri kopyalamak öğrenin."
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
ms.openlocfilehash: a64d13fa7dc5f50c259b98774be80b603dce400a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-to-and-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="ab2da-103">Veri ve Azure SQL Azure Data Factory kullanarak veritabanından kopyalamak</span><span class="sxs-lookup"><span data-stu-id="ab2da-103">Copy data to and from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="ab2da-104">Bu makalede kopya etkinliği Azure Data Factory için ve Azure SQL veritabanından veri taşımak için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ab2da-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to and from Azure SQL Database.</span></span> <span data-ttu-id="ab2da-105">Derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) kopyalama etkinliği ile veri taşıma için genel bir bakış sunar makalesi.</span><span class="sxs-lookup"><span data-stu-id="ab2da-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="ab2da-106">Desteklenen senaryolar</span><span class="sxs-lookup"><span data-stu-id="ab2da-106">Supported scenarios</span></span>
<span data-ttu-id="ab2da-107">Veri kopyalama **Azure SQL veritabanından** aşağıdaki veri depolar:</span><span class="sxs-lookup"><span data-stu-id="ab2da-107">You can copy data **from Azure SQL Database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="ab2da-108">Aşağıdaki veri depolarına verileri kopyalayabilirsiniz **Azure SQL veritabanı**:</span><span class="sxs-lookup"><span data-stu-id="ab2da-108">You can copy data from the following data stores **to Azure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="ab2da-109">Desteklenen kimlik doğrulama türü</span><span class="sxs-lookup"><span data-stu-id="ab2da-109">Supported authentication type</span></span>
<span data-ttu-id="ab2da-110">Azure SQL Veritabanı Bağlayıcısı temel kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="ab2da-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ab2da-111">Başlarken</span><span class="sxs-lookup"><span data-stu-id="ab2da-111">Getting started</span></span>
<span data-ttu-id="ab2da-112">Farklı araçlar/API'lerini kullanarak bir Azure SQL veritabanından/gelen verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ab2da-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="ab2da-113">Bir işlem hattı oluşturmak için en kolay yolu kullanmaktır **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="ab2da-113">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="ab2da-114">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) veri kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="ab2da-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="ab2da-115">Bir işlem hattı oluşturmak için aşağıdaki araçları kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu**, **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="ab2da-115">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ab2da-116">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="ab2da-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="ab2da-117">Araçlar ya da API'leri kullanıp bir havuz veri deposu için bir kaynak veri deposundan verileri taşır bir ardışık düzen oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ab2da-117">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="ab2da-118">Oluşturma bir **veri fabrikası**.</span><span class="sxs-lookup"><span data-stu-id="ab2da-118">Create a **data factory**.</span></span> <span data-ttu-id="ab2da-119">Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="ab2da-120">Oluşturma **bağlantılı Hizmetleri** girdi ve çıktı verilerini bağlamak için veri fabrikanıza depolar.</span><span class="sxs-lookup"><span data-stu-id="ab2da-120">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="ab2da-121">Örneğin, verileri Azure blob depolama alanından Azure SQL veritabanına kopyalıyorsanız Azure storage hesabını ve Azure SQL veritabanını veri fabrikanıza bağlamak için iki bağlı hizmet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ab2da-121">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="ab2da-122">Azure SQL veritabanına özel bağlantılı hizmet özellikleri için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ab2da-122">For linked service properties that are specific to Azure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="ab2da-123">Oluşturma **veri kümeleri** kopyalama işlemi için girdi ve çıktı verilerini temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="ab2da-123">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="ab2da-124">Son adımda bahsedilen örnekte blob kapsayıcısı ve giriş verilerini içeren klasörü belirtmek için bir veri kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ab2da-124">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="ab2da-125">Ve blob depolama biriminden kopyalanan verilerini tutan Azure SQL veritabanında SQL tablosu belirtmek için başka bir veri kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ab2da-125">And, you create another dataset to specify the SQL table in the Azure SQL database  that holds the data copied from the blob storage.</span></span> <span data-ttu-id="ab2da-126">Azure Data Lake Store için özel veri kümesi özellikleri için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ab2da-126">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="ab2da-127">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="ab2da-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="ab2da-128">Daha önce bahsedilen örnekte BlobSource bir kaynak ve SqlSink havuzu olarak kopya etkinliği için kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="ab2da-128">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="ab2da-129">Azure Blob depolama alanına Azure SQL veritabanından kopyalıyorsanız benzer şekilde, SqlSource ve BlobSink kopyalama etkinliği kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="ab2da-129">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="ab2da-130">Azure SQL veritabanına belirli kopyalama etkinliği özellikleri için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ab2da-130">For copy activity properties that are specific to Azure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="ab2da-131">Bir veri deposu bir kaynak veya bir havuz nasıl kullanılacağı hakkında daha fazla bilgi için önceki bölümde, veri deposu için bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ab2da-131">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="ab2da-132">Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ab2da-132">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="ab2da-133">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, JSON biçimini kullanarak bu Data Factory varlıklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ab2da-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="ab2da-134">/ Bir Azure SQL veritabanından veri kopyalamak için kullanılan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-to-and-from-sql-database) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="ab2da-134">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="ab2da-135">Aşağıdaki bölümler, Azure SQL veritabanını Data Factory varlıklarını belirli tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="ab2da-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="ab2da-136">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="ab2da-136">Linked service properties</span></span>
<span data-ttu-id="ab2da-137">Bir Azure SQL Hizmeti Bağlantıları data factory'nizi Azure SQL veritabanına bağlı.</span><span class="sxs-lookup"><span data-stu-id="ab2da-137">An Azure SQL linked service links an Azure SQL database to your data factory.</span></span> <span data-ttu-id="ab2da-138">Aşağıdaki tabloda, JSON öğeleri Azure SQL bağlı hizmeti için belirli bir açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ab2da-138">The following table provides description for JSON elements specific to Azure SQL linked service.</span></span>

| <span data-ttu-id="ab2da-139">Özellik</span><span class="sxs-lookup"><span data-stu-id="ab2da-139">Property</span></span> | <span data-ttu-id="ab2da-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ab2da-140">Description</span></span> | <span data-ttu-id="ab2da-141">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ab2da-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ab2da-142">type</span><span class="sxs-lookup"><span data-stu-id="ab2da-142">type</span></span> |<span data-ttu-id="ab2da-143">Type özelliği ayarlanmalıdır: **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="ab2da-143">The type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="ab2da-144">Evet</span><span class="sxs-lookup"><span data-stu-id="ab2da-144">Yes</span></span> |
| <span data-ttu-id="ab2da-145">connectionString</span><span class="sxs-lookup"><span data-stu-id="ab2da-145">connectionString</span></span> |<span data-ttu-id="ab2da-146">ConnectionString özelliği için Azure SQL veritabanı örneğine bağlanmak için gereken bilgileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="ab2da-146">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> <span data-ttu-id="ab2da-147">Yalnızca temel kimlik doğrulama desteklenir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="ab2da-148">Evet</span><span class="sxs-lookup"><span data-stu-id="ab2da-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="ab2da-149">Yapılandırma [Azure SQL veritabanı Güvenlik Duvarı](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) veritabanı sunucusuna [Azure hizmetlerinin sunucuya erişimine izin](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="ab2da-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="ab2da-150">Ayrıca, dış Azure veri fabrikası ağ geçidi ile şirket içi veri kaynaklarından dahil olmak üzere Azure SQL veritabanına veri kopyalıyorsanız, Azure SQL veritabanına veri gönderme makine için uygun IP adresi aralığı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ab2da-150">Additionally, if you are copying data to Azure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="ab2da-151">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="ab2da-151">Dataset properties</span></span>
<span data-ttu-id="ab2da-152">Bir Azure SQL veritabanındaki giriş veya çıkış verileri temsil etmek için bir veri kümesi belirtmek için veri kümesine tür özelliği ayarlayın: **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="ab2da-152">To specify a dataset to represent input or output data in an Azure SQL database, you set the type property of the dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="ab2da-153">Ayarlama **linkedServiceName** özellik kümesinin adı ile Azure SQL bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="ab2da-153">Set the **linkedServiceName** property of the dataset to the name of the Azure SQL linked service.</span></span>  

<span data-ttu-id="ab2da-154">Bölümler & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ab2da-154">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="ab2da-155">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="ab2da-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="ab2da-156">TypeProperties bölümü dataset her tür için farklıdır ve verilerin veri deposunda konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ab2da-156">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="ab2da-157">**TypeProperties** veri kümesi için bir bölüm türü **AzureSqlTable** aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="ab2da-157">The **typeProperties** section for the dataset of type **AzureSqlTable** has the following properties:</span></span>

| <span data-ttu-id="ab2da-158">Özellik</span><span class="sxs-lookup"><span data-stu-id="ab2da-158">Property</span></span> | <span data-ttu-id="ab2da-159">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ab2da-159">Description</span></span> | <span data-ttu-id="ab2da-160">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ab2da-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ab2da-161">tableName</span><span class="sxs-lookup"><span data-stu-id="ab2da-161">tableName</span></span> |<span data-ttu-id="ab2da-162">Tablo veya Görünüm bağlantılı hizmetinin Azure SQL veritabanı örneğinde başvurduğu adı.</span><span class="sxs-lookup"><span data-stu-id="ab2da-162">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="ab2da-163">Evet</span><span class="sxs-lookup"><span data-stu-id="ab2da-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="ab2da-164">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="ab2da-164">Copy activity properties</span></span>
<span data-ttu-id="ab2da-165">Bölümler & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz: [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ab2da-165">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ab2da-166">Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="ab2da-167">Kopyalama etkinliği yalnızca bir girdi alır ve tek bir çıktı üretir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-167">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="ab2da-168">Bulunan özellikler **typeProperties** etkinlik bölümünü her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-168">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="ab2da-169">Kopya etkinliği için bunlar türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-169">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="ab2da-170">Bir Azure SQL veritabanından veri taşıyorsanız, kaynak türü için kopyalama etkinliğinde ayarladığınız **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="ab2da-170">If you are moving data from an Azure SQL database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="ab2da-171">Bir Azure SQL veritabanına veri taşıyorsanız, benzer şekilde, Havuz türü için kopyalama etkinliğinde ayarladığınız **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="ab2da-171">Similarly, if you are moving data to an Azure SQL database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="ab2da-172">Bu bölümde SqlSource ve SqlSink tarafından desteklenen özellikler listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ab2da-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="ab2da-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="ab2da-173">SqlSource</span></span>
<span data-ttu-id="ab2da-174">Kopyalama etkinliğinde kaynak türü olduğunda **SqlSource**, aşağıdaki özellikler mevcuttur **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="ab2da-174">In copy activity, when the source is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="ab2da-175">Özellik</span><span class="sxs-lookup"><span data-stu-id="ab2da-175">Property</span></span> | <span data-ttu-id="ab2da-176">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ab2da-176">Description</span></span> | <span data-ttu-id="ab2da-177">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="ab2da-177">Allowed values</span></span> | <span data-ttu-id="ab2da-178">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ab2da-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ab2da-179">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="ab2da-179">sqlReaderQuery</span></span> |<span data-ttu-id="ab2da-180">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="ab2da-180">Use the custom query to read data.</span></span> |<span data-ttu-id="ab2da-181">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="ab2da-181">SQL query string.</span></span> <span data-ttu-id="ab2da-182">Örnek: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="ab2da-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="ab2da-183">Hayır</span><span class="sxs-lookup"><span data-stu-id="ab2da-183">No</span></span> |
| <span data-ttu-id="ab2da-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="ab2da-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="ab2da-185">Kaynak tablodan veri okuyan saklı yordamın adı.</span><span class="sxs-lookup"><span data-stu-id="ab2da-185">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="ab2da-186">Saklı yordam adı.</span><span class="sxs-lookup"><span data-stu-id="ab2da-186">Name of the stored procedure.</span></span> <span data-ttu-id="ab2da-187">Son SQL deyimi SELECT deyimi içinde saklı yordamı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-187">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="ab2da-188">Hayır</span><span class="sxs-lookup"><span data-stu-id="ab2da-188">No</span></span> |
| <span data-ttu-id="ab2da-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ab2da-189">storedProcedureParameters</span></span> |<span data-ttu-id="ab2da-190">Saklı yordam parametreleri.</span><span class="sxs-lookup"><span data-stu-id="ab2da-190">Parameters for the stored procedure.</span></span> |<span data-ttu-id="ab2da-191">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="ab2da-191">Name/value pairs.</span></span> <span data-ttu-id="ab2da-192">Adları ve büyük/küçük harf parametrelerinin adlarını ve saklı yordam parametreleri büyük/küçük harf eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-192">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="ab2da-193">Hayır</span><span class="sxs-lookup"><span data-stu-id="ab2da-193">No</span></span> |

<span data-ttu-id="ab2da-194">Varsa **sqlReaderQuery** belirtilen SqlSource için kopyalama etkinliği veri almak için Azure SQL veritabanı kaynağında bu sorguyu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="ab2da-194">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="ab2da-195">Alternatif olarak, bir saklı yordam belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (saklı yordam parametreleri alıyorsa).</span><span class="sxs-lookup"><span data-stu-id="ab2da-195">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="ab2da-196">SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz, JSON veri kümesi yapısı bölümünde tanımlanan sütunları bir sorgu oluşturmak için kullanılır (`select column1, column2 from mytable`) Azure SQL veritabanına karşı çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="ab2da-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (`select column1, column2 from mytable`) to run against the Azure SQL Database.</span></span> <span data-ttu-id="ab2da-197">Veri kümesi tanımı yapısına sahip değilse, tüm sütunları tablodan seçilir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-197">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="ab2da-198">Kullandığınızda **sqlReaderStoredProcedureName**, yine de için bir değer belirtmeniz gerekiyorsa **tableName** JSON veri kümesi bir özellik.</span><span class="sxs-lookup"><span data-stu-id="ab2da-198">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="ab2da-199">Yine de bu tabloya karşı gerçekleştirilen başka doğrulama vardır.</span><span class="sxs-lookup"><span data-stu-id="ab2da-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="ab2da-200">SqlSource örneği</span><span class="sxs-lookup"><span data-stu-id="ab2da-200">SqlSource example</span></span>

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

<span data-ttu-id="ab2da-201">**Saklı yordam tanımı:**</span><span class="sxs-lookup"><span data-stu-id="ab2da-201">**The stored procedure definition:**</span></span>

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

### <a name="sqlsink"></a><span data-ttu-id="ab2da-202">SqlSink</span><span class="sxs-lookup"><span data-stu-id="ab2da-202">SqlSink</span></span>
<span data-ttu-id="ab2da-203">**SqlSink** aşağıdaki özellikleri destekler:</span><span class="sxs-lookup"><span data-stu-id="ab2da-203">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="ab2da-204">Özellik</span><span class="sxs-lookup"><span data-stu-id="ab2da-204">Property</span></span> | <span data-ttu-id="ab2da-205">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ab2da-205">Description</span></span> | <span data-ttu-id="ab2da-206">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="ab2da-206">Allowed values</span></span> | <span data-ttu-id="ab2da-207">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ab2da-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ab2da-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="ab2da-208">writeBatchTimeout</span></span> |<span data-ttu-id="ab2da-209">Toplu ekleme işlemi zaman aşımına uğramadan önce tamamlamak bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="ab2da-209">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="ab2da-210">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="ab2da-210">timespan</span></span><br/><br/> <span data-ttu-id="ab2da-211">Örnek: "00: 30:00" (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="ab2da-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="ab2da-212">Hayır</span><span class="sxs-lookup"><span data-stu-id="ab2da-212">No</span></span> |
| <span data-ttu-id="ab2da-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ab2da-213">writeBatchSize</span></span> |<span data-ttu-id="ab2da-214">Arabellek boyutu writeBatchSize ulaştığında veri SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="ab2da-214">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="ab2da-215">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="ab2da-215">Integer (number of rows)</span></span> |<span data-ttu-id="ab2da-216">Hayır (varsayılan: 10000)</span><span class="sxs-lookup"><span data-stu-id="ab2da-216">No (default: 10000)</span></span> |
| <span data-ttu-id="ab2da-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="ab2da-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="ab2da-218">Belirli bir dilimle verilerinin temizlenmesini şekilde yürütmek kopyalama etkinliği için bir sorgu belirtin.</span><span class="sxs-lookup"><span data-stu-id="ab2da-218">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="ab2da-219">Daha fazla bilgi için bkz: [yinelenebilir kopyalama](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="ab2da-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="ab2da-220">Sorgu bildirimi.</span><span class="sxs-lookup"><span data-stu-id="ab2da-220">A query statement.</span></span> |<span data-ttu-id="ab2da-221">Hayır</span><span class="sxs-lookup"><span data-stu-id="ab2da-221">No</span></span> |
| <span data-ttu-id="ab2da-222">Sliceıdentifiercolumnname</span><span class="sxs-lookup"><span data-stu-id="ab2da-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="ab2da-223">Ne zaman yeniden çalıştırılacağını belirli bir dilim verileri temizlemek için kullanılan otomatik dilim tanımlayıcı doldurmak kopyalama etkinliği için bir sütun adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="ab2da-223">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="ab2da-224">Daha fazla bilgi için bkz: [yinelenebilir kopyalama](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="ab2da-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="ab2da-225">Binary(32) veri türüne sahip bir sütunun sütun adı.</span><span class="sxs-lookup"><span data-stu-id="ab2da-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="ab2da-226">Hayır</span><span class="sxs-lookup"><span data-stu-id="ab2da-226">No</span></span> |
| <span data-ttu-id="ab2da-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="ab2da-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="ab2da-228">Saklı yordam adı hedef tabloda bu upserts (güncelleştirmeler/ekler) verileri.</span><span class="sxs-lookup"><span data-stu-id="ab2da-228">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="ab2da-229">Saklı yordam adı.</span><span class="sxs-lookup"><span data-stu-id="ab2da-229">Name of the stored procedure.</span></span> |<span data-ttu-id="ab2da-230">Hayır</span><span class="sxs-lookup"><span data-stu-id="ab2da-230">No</span></span> |
| <span data-ttu-id="ab2da-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ab2da-231">storedProcedureParameters</span></span> |<span data-ttu-id="ab2da-232">Saklı yordam parametreleri.</span><span class="sxs-lookup"><span data-stu-id="ab2da-232">Parameters for the stored procedure.</span></span> |<span data-ttu-id="ab2da-233">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="ab2da-233">Name/value pairs.</span></span> <span data-ttu-id="ab2da-234">Adları ve büyük/küçük harf parametrelerinin adlarını ve saklı yordam parametreleri büyük/küçük harf eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-234">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="ab2da-235">Hayır</span><span class="sxs-lookup"><span data-stu-id="ab2da-235">No</span></span> |
| <span data-ttu-id="ab2da-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="ab2da-236">sqlWriterTableType</span></span> |<span data-ttu-id="ab2da-237">Saklı yordam, kullanılacak bir tablo türü adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="ab2da-237">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="ab2da-238">Kopyalama etkinliği taşınan veri geçici bir tablo bu tablo türü ile kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-238">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="ab2da-239">Saklı yordam kodu ardından var olan verilerle kopyalanan verileri birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab2da-239">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="ab2da-240">Bir tablo türü adı.</span><span class="sxs-lookup"><span data-stu-id="ab2da-240">A table type name.</span></span> |<span data-ttu-id="ab2da-241">Hayır</span><span class="sxs-lookup"><span data-stu-id="ab2da-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="ab2da-242">SqlSink örneği</span><span class="sxs-lookup"><span data-stu-id="ab2da-242">SqlSink example</span></span>

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

## <a name="json-examples-for-copying-data-to-and-from-sql-database"></a><span data-ttu-id="ab2da-243">JSON örnekleri ve SQL veritabanından veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="ab2da-243">JSON examples for copying data to and from SQL Database</span></span>
<span data-ttu-id="ab2da-244">Aşağıdaki örnekleri kullanarak bir işlem hattı oluşturmak için kullanabileceğiniz örnek JSON tanımları sağlar [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ab2da-244">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="ab2da-245">Bunlar ve Azure SQL Database ve Azure Blob depolama alanından veri kopyalamak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-245">They show how to copy data to and from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="ab2da-246">Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden herhangi birine belirtildiği havuzlarını kaynakları [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kopya etkinliği Azure Data Factory kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ab2da-246">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-to-azure-blob"></a><span data-ttu-id="ab2da-247">Örnek: verileri Azure SQL veritabanından Azure Blob kopyalama</span><span class="sxs-lookup"><span data-stu-id="ab2da-247">Example: Copy data from Azure SQL Database to Azure Blob</span></span>
<span data-ttu-id="ab2da-248">Aynı aşağıdaki Data Factory varlıklarını tanımlar:</span><span class="sxs-lookup"><span data-stu-id="ab2da-248">The same defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="ab2da-249">Bağlı hizmet türü [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ab2da-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="ab2da-250">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ab2da-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ab2da-251">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ab2da-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="ab2da-252">Bir çıkış [dataset](data-factory-create-datasets.md) türü [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ab2da-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="ab2da-253">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [SqlSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ab2da-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="ab2da-254">Örnek time series verilerini (saatlik, günlük, vb.) Azure SQL veritabanındaki bir tablo için bir blob saatte kopyalar.</span><span class="sxs-lookup"><span data-stu-id="ab2da-254">The sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database to a blob every hour.</span></span> <span data-ttu-id="ab2da-255">Bu örnekler kullanılan JSON özellikleri örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ab2da-255">The JSON properties used in these samples are described in sections following the samples.</span></span>  

<span data-ttu-id="ab2da-256">**Azure SQL Database hizmeti bağlı:**</span><span class="sxs-lookup"><span data-stu-id="ab2da-256">**Azure SQL Database linked service:**</span></span>

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
<span data-ttu-id="ab2da-257">Bkz: [Azure SQL bağlı hizmeti](#linked-service) bu bağlantılı hizmet tarafından desteklenen özelliklerin listesi için bölüm.</span><span class="sxs-lookup"><span data-stu-id="ab2da-257">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="ab2da-258">**Azure Blob storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="ab2da-258">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="ab2da-259">Bkz: [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) bu bağlantılı hizmet tarafından desteklenen özelliklerin listesi için makale.</span><span class="sxs-lookup"><span data-stu-id="ab2da-259">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="ab2da-260">**Azure SQL girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="ab2da-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="ab2da-261">Örnek, Azure SQL tablosu "MyTable" oluşturulur ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="ab2da-261">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="ab2da-262">"Dış" ayarı: "true" bildirir Azure Data Factory hizmetinin veri kümesi data factory dış ve veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="ab2da-262">Setting “external”: ”true” informs the Azure Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="ab2da-263">Bkz: [Azure SQL veri kümesi türü özellikleri](#dataset) bu dataset türü tarafından desteklenen özelliklerin listesi için bölüm.</span><span class="sxs-lookup"><span data-stu-id="ab2da-263">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="ab2da-264">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="ab2da-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="ab2da-265">Veri her saat yeni bir bloba yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="ab2da-265">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ab2da-266">Blob klasör yolu dinamik işlenmekte olan dilim başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-266">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="ab2da-267">Klasör yolu yıl, ay, gün ve saat bölümleri başlangıç saatini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ab2da-267">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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
<span data-ttu-id="ab2da-268">Bkz: [Azure Blob veri kümesi türü özellikleri](data-factory-azure-blob-connector.md#dataset-properties) bu dataset türü tarafından desteklenen özelliklerin listesi için bölüm.</span><span class="sxs-lookup"><span data-stu-id="ab2da-268">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="ab2da-269">**SQL kaynak ve Blob havuz sahip işlem hattı kopyalama etkinliğinde:**</span><span class="sxs-lookup"><span data-stu-id="ab2da-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="ab2da-270">Ardışık Düzen giriş ve çıkış veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-270">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="ab2da-271">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **SqlSource** ve **havuz** türü ayarlanmış **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="ab2da-271">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="ab2da-272">SQL sorgusu için belirtilen **SqlReaderQuery** özelliği veri kopyalamak için son bir saat içindeki seçer.</span><span class="sxs-lookup"><span data-stu-id="ab2da-272">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
<span data-ttu-id="ab2da-273">Örnekte, **sqlReaderQuery** SqlSource için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-273">In the example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="ab2da-274">Kopyalama etkinliği bu sorguyu veri almak için Azure SQL veritabanı kaynak karşı çalışır.</span><span class="sxs-lookup"><span data-stu-id="ab2da-274">The Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="ab2da-275">Alternatif olarak, bir saklı yordam belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (saklı yordam parametreleri alıyorsa).</span><span class="sxs-lookup"><span data-stu-id="ab2da-275">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="ab2da-276">SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz JSON veri kümesi yapısı bölümünde tanımlanan sütunları Azure SQL veritabanına karşı çalıştırmak için bir sorgu oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ab2da-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Database.</span></span> <span data-ttu-id="ab2da-277">Örneğin: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="ab2da-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="ab2da-278">Veri kümesi tanımı yapısına sahip değilse, tüm sütunları tablodan seçilir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-278">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="ab2da-279">Bkz: [Sql kaynağı](#sqlsource) bölüm ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) SqlSource ve BlobSink tarafından desteklenen özelliklerin listesi için.</span><span class="sxs-lookup"><span data-stu-id="ab2da-279">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-database"></a><span data-ttu-id="ab2da-280">Örnek: verileri Azure Blob'tan Azure SQL veritabanına kopyalamak</span><span class="sxs-lookup"><span data-stu-id="ab2da-280">Example: Copy data from Azure Blob to Azure SQL Database</span></span>
<span data-ttu-id="ab2da-281">Örnek aşağıdaki Data Factory varlıklarını tanımlar:</span><span class="sxs-lookup"><span data-stu-id="ab2da-281">The sample defines the following Data Factory entities:</span></span>  

1. <span data-ttu-id="ab2da-282">Bağlı hizmet türü [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ab2da-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="ab2da-283">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ab2da-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ab2da-284">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ab2da-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="ab2da-285">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ab2da-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="ab2da-286">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) ve [SqlSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ab2da-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="ab2da-287">Zaman serisi Azure SQL tablosuna (saatlik, günlük, vb.) verileri Azure blob örnek kopyaları saatte veritabanı.</span><span class="sxs-lookup"><span data-stu-id="ab2da-287">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL database every hour.</span></span> <span data-ttu-id="ab2da-288">Bu örnekler kullanılan JSON özellikleri örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ab2da-288">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="ab2da-289">**Azure SQL bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="ab2da-289">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="ab2da-290">Bkz: [Azure SQL bağlı hizmeti](#linked-service) bu bağlantılı hizmet tarafından desteklenen özelliklerin listesi için bölüm.</span><span class="sxs-lookup"><span data-stu-id="ab2da-290">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="ab2da-291">**Azure Blob storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="ab2da-291">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="ab2da-292">Bkz: [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) bu bağlantılı hizmet tarafından desteklenen özelliklerin listesi için makale.</span><span class="sxs-lookup"><span data-stu-id="ab2da-292">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="ab2da-293">**Azure Blob girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="ab2da-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="ab2da-294">Veri toplanma yeni blob üzerinden saatte (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="ab2da-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ab2da-295">Blob klasör yolu ve dosya adı dinamik olarak değerlendirilir işleniyor dilim başlangıç zamanı temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="ab2da-295">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="ab2da-296">Klasör yolu yıl, ay ve gün kısmını başlangıç saati ve dosya adı başlangıç zamanı saat bölümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="ab2da-296">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="ab2da-297">"dış": "true" ayarı Bu tablo veri fabrikası dış ve veri fabrikasında bir etkinlik tarafından üretilen değil Data Factory hizmetinin sizi bilgilendirir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-297">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="ab2da-298">Bkz: [Azure Blob veri kümesi türü özellikleri](data-factory-azure-blob-connector.md#dataset-properties) bu dataset türü tarafından desteklenen özelliklerin listesi için bölüm.</span><span class="sxs-lookup"><span data-stu-id="ab2da-298">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="ab2da-299">**Azure SQL veritabanı veri kümesini çıktı:**</span><span class="sxs-lookup"><span data-stu-id="ab2da-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="ab2da-300">Örnek verileri Azure SQL "MyTable" adlı bir tablo kopyalar.</span><span class="sxs-lookup"><span data-stu-id="ab2da-300">The sample copies data to a table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="ab2da-301">Blob CSV dosyasında içerecek şekilde beklediğiniz gibi aynı sayıda sütun ile Azure SQL tablosu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ab2da-301">Create the table in Azure SQL with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="ab2da-302">Yeni satırlar tabloya saatte eklenir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-302">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="ab2da-303">Bkz: [Azure SQL veri kümesi türü özellikleri](#dataset) bu dataset türü tarafından desteklenen özelliklerin listesi için bölüm.</span><span class="sxs-lookup"><span data-stu-id="ab2da-303">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="ab2da-304">**Blob kaynağı ve SQL havuz sahip işlem hattı kopyalama etkinliğinde:**</span><span class="sxs-lookup"><span data-stu-id="ab2da-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="ab2da-305">Ardışık Düzen giriş ve çıkış veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-305">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="ab2da-306">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **BlobSource** ve **havuz** türü ayarlanmış **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="ab2da-306">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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
<span data-ttu-id="ab2da-307">Bkz: [Sql havuz](#sqlsink) bölüm ve [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) SqlSink ve BlobSource tarafından desteklenen özelliklerin listesi için.</span><span class="sxs-lookup"><span data-stu-id="ab2da-307">See the [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="ab2da-308">Hedef veritabanında kimlik sütunu</span><span class="sxs-lookup"><span data-stu-id="ab2da-308">Identity columns in the target database</span></span>
<span data-ttu-id="ab2da-309">Bu bölüm veri kaynak tablodaki bir kimlik sütunu olmadan bir kimlik sütunu içeren bir hedef tablo kopyalamak için bir örnek verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-309">This section provides an example for copying data from a source table without an identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="ab2da-310">**Kaynak tablosu:**</span><span class="sxs-lookup"><span data-stu-id="ab2da-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="ab2da-311">**Hedef Tablo:**</span><span class="sxs-lookup"><span data-stu-id="ab2da-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="ab2da-312">Hedef tabloda bir kimlik sütunu olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="ab2da-312">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="ab2da-313">**Kaynak veri kümesi JSON tanımı**</span><span class="sxs-lookup"><span data-stu-id="ab2da-313">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="ab2da-314">**Hedef veri kümesi JSON tanımı**</span><span class="sxs-lookup"><span data-stu-id="ab2da-314">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="ab2da-315">Kaynak ve hedef tablosu farklı şema sahip dikkat edin (hedef kimliğine sahip başka bir sütuna sahip).</span><span class="sxs-lookup"><span data-stu-id="ab2da-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="ab2da-316">Bu senaryoda, belirtmeniz gerekir. **yapısı** kimlik sütunu içermeyen hedef veri kümesi tanımında özelliği.</span><span class="sxs-lookup"><span data-stu-id="ab2da-316">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="ab2da-317">SQL havuz depolanan yordamı çağırma</span><span class="sxs-lookup"><span data-stu-id="ab2da-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="ab2da-318">Kopyalama etkinliği ardışık SQL havuzunda bir saklı yordam çağırma bir örnek için bkz: [kopyalama etkinliği SQL havuz için saklı yordam çağırma](data-factory-invoke-stored-procedure-from-copy-activity.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ab2da-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="ab2da-319">Tür eşlemesi için Azure SQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="ab2da-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="ab2da-320">Bölümünde belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale kopyalama etkinliği aşağıdaki 2 adımlı yaklaşımı türleriyle havuz için kaynak türünden otomatik tür dönüşümleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="ab2da-320">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="ab2da-321">Yerel kaynak türlerinden .NET türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="ab2da-321">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="ab2da-322">.NET türünden yerel havuz türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="ab2da-322">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="ab2da-323">Veri taşımak ve Azure SQL veritabanından olduğunda, aşağıdaki eşlemelerini SQL türü .NET türü ve tersi yönde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ab2da-323">When moving data to and from Azure SQL Database, the following mappings are used from SQL type to .NET type and vice versa.</span></span> <span data-ttu-id="ab2da-324">ADO.NET için SQL Server veri türü eşlemesi aynı eşlemedir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-324">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="ab2da-325">SQL Server veritabanı altyapısı türü</span><span class="sxs-lookup"><span data-stu-id="ab2da-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="ab2da-326">.NET framework türü</span><span class="sxs-lookup"><span data-stu-id="ab2da-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="ab2da-327">bigint</span><span class="sxs-lookup"><span data-stu-id="ab2da-327">bigint</span></span> |<span data-ttu-id="ab2da-328">Int64</span><span class="sxs-lookup"><span data-stu-id="ab2da-328">Int64</span></span> |
| <span data-ttu-id="ab2da-329">İkili</span><span class="sxs-lookup"><span data-stu-id="ab2da-329">binary</span></span> |<span data-ttu-id="ab2da-330">Byte]</span><span class="sxs-lookup"><span data-stu-id="ab2da-330">Byte[]</span></span> |
| <span data-ttu-id="ab2da-331">bit</span><span class="sxs-lookup"><span data-stu-id="ab2da-331">bit</span></span> |<span data-ttu-id="ab2da-332">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="ab2da-332">Boolean</span></span> |
| <span data-ttu-id="ab2da-333">char</span><span class="sxs-lookup"><span data-stu-id="ab2da-333">char</span></span> |<span data-ttu-id="ab2da-334">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="ab2da-334">String, Char[]</span></span> |
| <span data-ttu-id="ab2da-335">Tarih</span><span class="sxs-lookup"><span data-stu-id="ab2da-335">date</span></span> |<span data-ttu-id="ab2da-336">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="ab2da-336">DateTime</span></span> |
| <span data-ttu-id="ab2da-337">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="ab2da-337">Datetime</span></span> |<span data-ttu-id="ab2da-338">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="ab2da-338">DateTime</span></span> |
| <span data-ttu-id="ab2da-339">datetime2</span><span class="sxs-lookup"><span data-stu-id="ab2da-339">datetime2</span></span> |<span data-ttu-id="ab2da-340">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="ab2da-340">DateTime</span></span> |
| <span data-ttu-id="ab2da-341">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="ab2da-341">Datetimeoffset</span></span> |<span data-ttu-id="ab2da-342">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="ab2da-342">DateTimeOffset</span></span> |
| <span data-ttu-id="ab2da-343">Ondalık</span><span class="sxs-lookup"><span data-stu-id="ab2da-343">Decimal</span></span> |<span data-ttu-id="ab2da-344">Ondalık</span><span class="sxs-lookup"><span data-stu-id="ab2da-344">Decimal</span></span> |
| <span data-ttu-id="ab2da-345">FILESTREAM özniteliği (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="ab2da-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="ab2da-346">Byte]</span><span class="sxs-lookup"><span data-stu-id="ab2da-346">Byte[]</span></span> |
| <span data-ttu-id="ab2da-347">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="ab2da-347">Float</span></span> |<span data-ttu-id="ab2da-348">Çift</span><span class="sxs-lookup"><span data-stu-id="ab2da-348">Double</span></span> |
| <span data-ttu-id="ab2da-349">Görüntü</span><span class="sxs-lookup"><span data-stu-id="ab2da-349">image</span></span> |<span data-ttu-id="ab2da-350">Byte]</span><span class="sxs-lookup"><span data-stu-id="ab2da-350">Byte[]</span></span> |
| <span data-ttu-id="ab2da-351">Int</span><span class="sxs-lookup"><span data-stu-id="ab2da-351">int</span></span> |<span data-ttu-id="ab2da-352">Int32</span><span class="sxs-lookup"><span data-stu-id="ab2da-352">Int32</span></span> |
| <span data-ttu-id="ab2da-353">para</span><span class="sxs-lookup"><span data-stu-id="ab2da-353">money</span></span> |<span data-ttu-id="ab2da-354">Ondalık</span><span class="sxs-lookup"><span data-stu-id="ab2da-354">Decimal</span></span> |
| <span data-ttu-id="ab2da-355">nchar</span><span class="sxs-lookup"><span data-stu-id="ab2da-355">nchar</span></span> |<span data-ttu-id="ab2da-356">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="ab2da-356">String, Char[]</span></span> |
| <span data-ttu-id="ab2da-357">ntext</span><span class="sxs-lookup"><span data-stu-id="ab2da-357">ntext</span></span> |<span data-ttu-id="ab2da-358">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="ab2da-358">String, Char[]</span></span> |
| <span data-ttu-id="ab2da-359">sayısal</span><span class="sxs-lookup"><span data-stu-id="ab2da-359">numeric</span></span> |<span data-ttu-id="ab2da-360">Ondalık</span><span class="sxs-lookup"><span data-stu-id="ab2da-360">Decimal</span></span> |
| <span data-ttu-id="ab2da-361">nvarchar</span><span class="sxs-lookup"><span data-stu-id="ab2da-361">nvarchar</span></span> |<span data-ttu-id="ab2da-362">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="ab2da-362">String, Char[]</span></span> |
| <span data-ttu-id="ab2da-363">Gerçek</span><span class="sxs-lookup"><span data-stu-id="ab2da-363">real</span></span> |<span data-ttu-id="ab2da-364">Tek</span><span class="sxs-lookup"><span data-stu-id="ab2da-364">Single</span></span> |
| <span data-ttu-id="ab2da-365">rowVersion</span><span class="sxs-lookup"><span data-stu-id="ab2da-365">rowversion</span></span> |<span data-ttu-id="ab2da-366">Byte]</span><span class="sxs-lookup"><span data-stu-id="ab2da-366">Byte[]</span></span> |
| <span data-ttu-id="ab2da-367">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="ab2da-367">smalldatetime</span></span> |<span data-ttu-id="ab2da-368">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="ab2da-368">DateTime</span></span> |
| <span data-ttu-id="ab2da-369">tamsayı</span><span class="sxs-lookup"><span data-stu-id="ab2da-369">smallint</span></span> |<span data-ttu-id="ab2da-370">Int16</span><span class="sxs-lookup"><span data-stu-id="ab2da-370">Int16</span></span> |
| <span data-ttu-id="ab2da-371">küçük para</span><span class="sxs-lookup"><span data-stu-id="ab2da-371">smallmoney</span></span> |<span data-ttu-id="ab2da-372">Ondalık</span><span class="sxs-lookup"><span data-stu-id="ab2da-372">Decimal</span></span> |
| <span data-ttu-id="ab2da-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="ab2da-373">sql_variant</span></span> |<span data-ttu-id="ab2da-374">Nesne *</span><span class="sxs-lookup"><span data-stu-id="ab2da-374">Object *</span></span> |
| <span data-ttu-id="ab2da-375">Metin</span><span class="sxs-lookup"><span data-stu-id="ab2da-375">text</span></span> |<span data-ttu-id="ab2da-376">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="ab2da-376">String, Char[]</span></span> |
| <span data-ttu-id="ab2da-377">time</span><span class="sxs-lookup"><span data-stu-id="ab2da-377">time</span></span> |<span data-ttu-id="ab2da-378">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="ab2da-378">TimeSpan</span></span> |
| <span data-ttu-id="ab2da-379">timestamp</span><span class="sxs-lookup"><span data-stu-id="ab2da-379">timestamp</span></span> |<span data-ttu-id="ab2da-380">Byte]</span><span class="sxs-lookup"><span data-stu-id="ab2da-380">Byte[]</span></span> |
| <span data-ttu-id="ab2da-381">Mini tamsayı</span><span class="sxs-lookup"><span data-stu-id="ab2da-381">tinyint</span></span> |<span data-ttu-id="ab2da-382">Bayt</span><span class="sxs-lookup"><span data-stu-id="ab2da-382">Byte</span></span> |
| <span data-ttu-id="ab2da-383">benzersiz tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="ab2da-383">uniqueidentifier</span></span> |<span data-ttu-id="ab2da-384">GUID</span><span class="sxs-lookup"><span data-stu-id="ab2da-384">Guid</span></span> |
| <span data-ttu-id="ab2da-385">varbinary</span><span class="sxs-lookup"><span data-stu-id="ab2da-385">varbinary</span></span> |<span data-ttu-id="ab2da-386">Byte]</span><span class="sxs-lookup"><span data-stu-id="ab2da-386">Byte[]</span></span> |
| <span data-ttu-id="ab2da-387">varchar</span><span class="sxs-lookup"><span data-stu-id="ab2da-387">varchar</span></span> |<span data-ttu-id="ab2da-388">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="ab2da-388">String, Char[]</span></span> |
| <span data-ttu-id="ab2da-389">xml</span><span class="sxs-lookup"><span data-stu-id="ab2da-389">xml</span></span> |<span data-ttu-id="ab2da-390">XML</span><span class="sxs-lookup"><span data-stu-id="ab2da-390">Xml</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="ab2da-391">Kaynak havuzu sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="ab2da-391">Map source to sink columns</span></span>
<span data-ttu-id="ab2da-392">Havuz dataset sütunlara kaynak kümesindeki eşleme sütunları hakkında bilgi edinmek için [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="ab2da-392">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="ab2da-393">Yinelenebilir kopyalama</span><span class="sxs-lookup"><span data-stu-id="ab2da-393">Repeatable copy</span></span>
<span data-ttu-id="ab2da-394">SQL Server veritabanına veri kopyalama, kopyalama etkinliği verileri varsayılan olarak havuz tabloya ekler.</span><span class="sxs-lookup"><span data-stu-id="ab2da-394">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="ab2da-395">Bunun yerine bir UPSERT gerçekleştirmek için bkz: [Repeatable yazmak için SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ab2da-395">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="ab2da-396">İlişkisel veri kopyalama verileri depoladığında, Yinelenebilirlik istenmeyen sonuçları önlemek için göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="ab2da-396">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="ab2da-397">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab2da-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="ab2da-398">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab2da-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="ab2da-399">Bir dilim iki yolla yeniden çalıştırıldığında, aynı veri dilimi çalıştırmak kaç kez geçtiğinden bağımsız okuduğunuzdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab2da-399">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="ab2da-400">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="ab2da-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="ab2da-401">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="ab2da-401">Performance and Tuning</span></span>
<span data-ttu-id="ab2da-402">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve onu en iyi duruma getirmek için çeşitli yollar etkisi performansını anahtar Etkenler hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="ab2da-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
