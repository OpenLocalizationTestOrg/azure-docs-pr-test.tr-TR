---
title: Veri kopyalama/Azure Blob depolama biriminden | Microsoft Docs
description: "Azure Data Factory'de BLOB verileri kopyalamak öğrenin. Bizim örnek kullanın: ve Azure Blob Storage ve Azure SQL veritabanına veri kopyalamak nasıl."
keywords: BLOB verilerini, azure blob kopyalama
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 2cf955b52010869a4e753c441e17bdd32fd2e63d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="copy-data-to-or-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="64fa7-105">Veri ya da Azure Data Factory kullanarak Azure Blob depolama biriminden kopyalayın</span><span class="sxs-lookup"><span data-stu-id="64fa7-105">Copy data to or from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="64fa7-106">Bu makalede kopya etkinliği Azure Data Factory'de ve Azure Blob depolama biriminden veri kopyalamak için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-106">This article explains how to use the Copy Activity in Azure Data Factory to copy data to and from Azure Blob Storage.</span></span> <span data-ttu-id="64fa7-107">Derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) kopyalama etkinliği ile veri taşıma için genel bir bakış sunar makalesi.</span><span class="sxs-lookup"><span data-stu-id="64fa7-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="64fa7-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="64fa7-108">Overview</span></span>
<span data-ttu-id="64fa7-109">Verileri Azure Blob Storage için tüm desteklenen kaynak veri deposundan veya Azure Blob Storage tüm desteklenen havuz veri deposuna kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64fa7-109">You can copy data from any supported source data store to Azure Blob Storage or from Azure Blob Storage to any supported sink data store.</span></span> <span data-ttu-id="64fa7-110">Aşağıdaki tabloda tarafından kopyalama etkinliği iç havuzlar veya kaynakları olarak desteklenen veri depoları listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="64fa7-110">The following table provides a list of data stores supported as sources or sinks by the copy activity.</span></span> <span data-ttu-id="64fa7-111">Örneğin, veri taşıyabilirsiniz **gelen** bir SQL Server veritabanı veya bir Azure SQL veritabanı **için** Azure blob depolama.</span><span class="sxs-lookup"><span data-stu-id="64fa7-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="64fa7-112">Ve veri kopyalayabilirsiniz **gelen** Azure blob depolama **için** Azure SQL Data Warehouse veya bir Azure Cosmos DB koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="64fa7-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="64fa7-113">Desteklenen senaryolar</span><span class="sxs-lookup"><span data-stu-id="64fa7-113">Supported scenarios</span></span>
<span data-ttu-id="64fa7-114">Veri kopyalama **Azure Blob depolama biriminden** aşağıdaki veri depolar:</span><span class="sxs-lookup"><span data-stu-id="64fa7-114">You can copy data **from Azure Blob Storage** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="64fa7-115">Aşağıdaki veri depolarına verileri kopyalayabilirsiniz **Azure Blob depolama alanına**:</span><span class="sxs-lookup"><span data-stu-id="64fa7-115">You can copy data from the following data stores **to Azure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="64fa7-116">Kopyalama etkinliği başlangıç/bitiş hem genel amaçlı Azure depolama hesapları hem de etkin/Cool Blob Depolama veri kopyalamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="64fa7-116">Copy Activity supports copying data from/to both general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="64fa7-117">Etkinlik destekler **bloğundan okuma, ekleme veya sayfa blobları**, ancak destekleyen **yalnızca blok yazma**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-117">The activity supports **reading from block, append, or page blobs**, but supports **writing to only block blobs**.</span></span> <span data-ttu-id="64fa7-118">Sayfa blobları tarafından yedeklenen olduğundan azure Premium depolama havuzu olarak desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="64fa7-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="64fa7-119">Verileri başarıyla hedefe kopyalandıktan sonra kopyalama etkinliği kaynaktan verileri silmez.</span><span class="sxs-lookup"><span data-stu-id="64fa7-119">Copy Activity does not delete data from the source after the data is successfully copied to the destination.</span></span> <span data-ttu-id="64fa7-120">Sonra başarılı bir kopyasını kaynak verilerini silmek ihtiyacınız varsa oluşturma bir [özel etkinlik](data-factory-use-custom-activities.md) verileri silmek ve ardışık düzeninde etkinlik kullanın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-120">If you need to delete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) to delete the data and use the activity in the pipeline.</span></span> <span data-ttu-id="64fa7-121">Bir örnek için bkz: [Delete blob veya klasör örneği github'daki](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span><span class="sxs-lookup"><span data-stu-id="64fa7-121">For an example, see the [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="64fa7-122">başlarken</span><span class="sxs-lookup"><span data-stu-id="64fa7-122">Get started</span></span>
<span data-ttu-id="64fa7-123">Farklı araçlar/API'lerini kullanarak verileri Azure Blob Storage/gruptan taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="64fa7-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="64fa7-124">Bir işlem hattı oluşturmak için en kolay yolu kullanmaktır **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-124">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="64fa7-125">Bu makalede sahip bir [izlenecek](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) verileri bir Azure Blob Depolama Birimi konumundan başka bir Azure Blob depolama konumuna kopyalamak için bir işlem hattı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="64fa7-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline to copy data from an Azure Blob Storage location  to another Azure Blob Storage location.</span></span> <span data-ttu-id="64fa7-126">Verileri Azure Blob depolama alanından Azure SQL veritabanına kopyalamak için bir işlem hattı oluşturma bir öğretici için bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="64fa7-126">For a tutorial on creating a pipeline to copy data from an Azure Blob Storage to Azure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="64fa7-127">Bir işlem hattı oluşturmak için aşağıdaki araçları kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu**, **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-127">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="64fa7-128">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="64fa7-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="64fa7-129">Araçlar ya da API'leri kullanıp bir havuz veri deposu için bir kaynak veri deposundan verileri taşır bir ardışık düzen oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="64fa7-129">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="64fa7-130">Oluşturma bir **veri fabrikası**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-130">Create a **data factory**.</span></span> <span data-ttu-id="64fa7-131">Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="64fa7-132">Oluşturma **bağlantılı Hizmetleri** girdi ve çıktı verilerini bağlamak için veri fabrikanıza depolar.</span><span class="sxs-lookup"><span data-stu-id="64fa7-132">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="64fa7-133">Örneğin, verileri Azure blob depolama alanından Azure SQL veritabanına kopyalıyorsanız Azure storage hesabını ve Azure SQL veritabanını veri fabrikanıza bağlamak için iki bağlı hizmet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="64fa7-133">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="64fa7-134">Azure Blob depolama alanına özel bağlantılı hizmet özellikleri için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="64fa7-134">For linked service properties that are specific to Azure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="64fa7-135">Oluşturma **veri kümeleri** kopyalama işlemi için girdi ve çıktı verilerini temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="64fa7-135">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="64fa7-136">Son adımda bahsedilen örnekte blob kapsayıcısı ve giriş verilerini içeren klasörü belirtmek için bir veri kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="64fa7-136">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="64fa7-137">Ve blob depolama biriminden kopyalanan verilerini tutan Azure SQL veritabanında SQL tablosu belirtmek için başka bir veri kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="64fa7-137">And, you create another dataset to specify the SQL table in the Azure SQL database that holds the data copied from the blob storage.</span></span> <span data-ttu-id="64fa7-138">Azure Blob depolama alanına özel veri kümesi özellikleri için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="64fa7-138">For dataset properties that are specific to Azure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="64fa7-139">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="64fa7-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="64fa7-140">Daha önce bahsedilen örnekte BlobSource bir kaynak ve SqlSink havuzu olarak kopya etkinliği için kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="64fa7-140">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="64fa7-141">Azure Blob depolama alanına Azure SQL veritabanından kopyalıyorsanız benzer şekilde, SqlSource ve BlobSink kopyalama etkinliği kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="64fa7-141">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="64fa7-142">Azure Blob depolama alanına belirli kopyalama etkinliği özellikleri için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="64fa7-142">For copy activity properties that are specific to Azure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="64fa7-143">Bir veri deposu bir kaynak veya bir havuz nasıl kullanılacağı hakkında daha fazla bilgi için önceki bölümde, veri deposu için bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-143">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>  

<span data-ttu-id="64fa7-144">Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="64fa7-144">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="64fa7-145">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, JSON biçimini kullanarak bu Data Factory varlıklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="64fa7-146">/ Azure Blob depolama biriminden veri kopyalamak için kullanılan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-to-and-from-blob-storage  ) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-146">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="64fa7-147">Aşağıdaki bölümler, Azure Blob depolama alanına Data Factory varlıklarını belirli tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="64fa7-147">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="64fa7-148">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="64fa7-148">Linked service properties</span></span>
<span data-ttu-id="64fa7-149">Bağlı hizmetler Azure Storage bir Azure data factory'ye bağlamak için kullanabileceğiniz iki tür vardır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-149">There are two types of linked services you can use to link an Azure Storage to an Azure data factory.</span></span> <span data-ttu-id="64fa7-150">Bunlar: **AzureStorage** bağlantılı hizmeti ve **AzureStorageSas** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="64fa7-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="64fa7-151">Azure Storage bağlı hizmeti Azure Storage data factory ile genel erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="64fa7-151">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="64fa7-152">Azure depolama SAS (paylaşılan erişim imzası) bağlı ise hizmeti Azure Storage veri fabrikası kısıtlanmış/zaman sınırlı erişimi olan sağlar.</span><span class="sxs-lookup"><span data-stu-id="64fa7-152">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="64fa7-153">Bu iki bağlı hizmet arasındaki herhangi bir fark vardır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="64fa7-154">Gereksinimlerinize uygun bağlı hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-154">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="64fa7-155">Aşağıdaki bölümler bu iki bağlı hizmet üzerinde daha fazla ayrıntı sağlar.</span><span class="sxs-lookup"><span data-stu-id="64fa7-155">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="64fa7-156">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="64fa7-156">Dataset properties</span></span>
<span data-ttu-id="64fa7-157">Giriş veya çıkış verileri Azure Blob Depolama göstermek için bir veri kümesi belirtmek için veri kümesine tür özelliği ayarlayın: **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-157">To specify a dataset to represent input or output data in an Azure Blob Storage, you set the type property of the dataset to: **AzureBlob**.</span></span> <span data-ttu-id="64fa7-158">Ayarlama **linkedServiceName** bağlı hizmeti Azure Storage veya Azure depolama SAS adını kümesinin özellik.</span><span class="sxs-lookup"><span data-stu-id="64fa7-158">Set the **linkedServiceName** property of the dataset to the name of the Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="64fa7-159">Veri kümesi türü özelliklerini belirtin **blob kapsayıcısı** ve **klasörü** blob depolamada.</span><span class="sxs-lookup"><span data-stu-id="64fa7-159">The type properties of the dataset specify the **blob container** and the **folder** in the blob storage.</span></span>

<span data-ttu-id="64fa7-160">JSON bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="64fa7-160">For a full list of JSON sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="64fa7-161">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="64fa7-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="64fa7-162">Veri Fabrikası yapısındaki"" şema üzerinde okuma veri kaynakları için Azure blob gibi tür bilgilerini sağlamaktan aşağıdaki temel CLS uyumlu .NET türü değerleri destekler: Int16, Int32, Int64, tek, Double, Decimal, Byte [], Bool, dize, GUID, Datetime, Datetimeoffset, Timespan.</span><span class="sxs-lookup"><span data-stu-id="64fa7-162">Data factory supports the following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="64fa7-163">Veri Fabrikası tür dönüşümleri veri bir havuz veri deposu için bir kaynak veri deposundan taşırken otomatik olarak gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-163">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span></span>

<span data-ttu-id="64fa7-164">**TypeProperties** bölüm bilgileri sağlar ve her veri kümesi türü için farklı konumu hakkında vb., verilerin veri deposundaki biçimlendirin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-164">The **typeProperties** section is different for each type of dataset and provides information about the location, format etc., of the data in the data store.</span></span> <span data-ttu-id="64fa7-165">TypeProperties bölüm türü veri kümesi için **AzureBlob** veri kümesine aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="64fa7-165">The typeProperties section for dataset of type **AzureBlob** dataset has the following properties:</span></span>

| <span data-ttu-id="64fa7-166">Özellik</span><span class="sxs-lookup"><span data-stu-id="64fa7-166">Property</span></span> | <span data-ttu-id="64fa7-167">Açıklama</span><span class="sxs-lookup"><span data-stu-id="64fa7-167">Description</span></span> | <span data-ttu-id="64fa7-168">Gerekli</span><span class="sxs-lookup"><span data-stu-id="64fa7-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="64fa7-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="64fa7-169">folderPath</span></span> |<span data-ttu-id="64fa7-170">Kapsayıcı ve klasöre blob depolamada yolu.</span><span class="sxs-lookup"><span data-stu-id="64fa7-170">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="64fa7-171">Örnek: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="64fa7-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="64fa7-172">Evet</span><span class="sxs-lookup"><span data-stu-id="64fa7-172">Yes</span></span> |
| <span data-ttu-id="64fa7-173">fileName</span><span class="sxs-lookup"><span data-stu-id="64fa7-173">fileName</span></span> |<span data-ttu-id="64fa7-174">Blob adı.</span><span class="sxs-lookup"><span data-stu-id="64fa7-174">Name of the blob.</span></span> <span data-ttu-id="64fa7-175">isteğe bağlıdır ve büyük küçük harfe duyarlı dosya adıdır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="64fa7-176">Bir dosya adı belirtirseniz, (kopyalama dahil) etkinlik belirli Blob üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-176">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="64fa7-177">Dosya adı belirtilmediğinde kopyalama tüm BLOB'lar girdi veri kümesi için folderPath içerir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-177">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="64fa7-178">Zaman **fileName** bir çıkış veri kümesi için belirtilmemiş ve **preserveHierarchy** belirtilmedi etkinlik havuzunda oluşturulmuş dosya adı aşağıdaki olacaktır Bu biçim: veri.<Guid>. txt (örneğin:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="64fa7-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="64fa7-179">Hayır</span><span class="sxs-lookup"><span data-stu-id="64fa7-179">No</span></span> |
| <span data-ttu-id="64fa7-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="64fa7-180">partitionedBy</span></span> |<span data-ttu-id="64fa7-181">partitionedBy isteğe bağlı bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="64fa7-182">Bir dinamik folderPath ve zaman serisi verileri için dosya adı belirtmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64fa7-182">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="64fa7-183">Örneğin, folderPath için verileri saatte parametreli olabilir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="64fa7-184">Bkz: [partitionedBy özellik bölümünü kullanarak](#using-partitionedBy-property) ayrıntı ve örnekler için.</span><span class="sxs-lookup"><span data-stu-id="64fa7-184">See the [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="64fa7-185">Hayır</span><span class="sxs-lookup"><span data-stu-id="64fa7-185">No</span></span> |
| <span data-ttu-id="64fa7-186">Biçimi</span><span class="sxs-lookup"><span data-stu-id="64fa7-186">format</span></span> | <span data-ttu-id="64fa7-187">Şu biçimi türleri desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-187">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="64fa7-188">Ayarlama **türü** şu değerlerden biri biçimine altında özellik.</span><span class="sxs-lookup"><span data-stu-id="64fa7-188">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="64fa7-189">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="64fa7-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="64fa7-190">İsterseniz **olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-190">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="64fa7-191">Hayır</span><span class="sxs-lookup"><span data-stu-id="64fa7-191">No</span></span> |
| <span data-ttu-id="64fa7-192">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="64fa7-192">compression</span></span> | <span data-ttu-id="64fa7-193">Veri sıkıştırma düzeyini ve türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-193">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="64fa7-194">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="64fa7-195">Desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="64fa7-196">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="64fa7-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="64fa7-197">Hayır</span><span class="sxs-lookup"><span data-stu-id="64fa7-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="64fa7-198">PartitionedBy özelliğini kullanma</span><span class="sxs-lookup"><span data-stu-id="64fa7-198">Using partitionedBy property</span></span>
<span data-ttu-id="64fa7-199">Önceki bölümde belirtildiği gibi bir dinamik folderPath ve zaman serisi verilerle dosya adını belirtebilirsiniz **partitionedBy** özelliği, [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="64fa7-199">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="64fa7-200">Zaman serisi veri kümeleri, zamanlama ve dilimleri hakkında daha fazla bilgi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) ve [zamanlama ve yürütme](data-factory-scheduling-and-execution.md) makaleleri.</span><span class="sxs-lookup"><span data-stu-id="64fa7-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="64fa7-201">Örnek 1</span><span class="sxs-lookup"><span data-stu-id="64fa7-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="64fa7-202">Bu örnekte, {dilim} belirtilen veri fabrikası sistem değişkenin değerini SliceStart (YYYYMMDDHH) biçiminde ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-202">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="64fa7-203">Dilimin başlangıç SliceStart başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="64fa7-203">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="64fa7-204">FolderPath her dilim için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-204">The folderPath is different for each slice.</span></span> <span data-ttu-id="64fa7-205">Örneğin: wikidatagateway/wikisampledataout/2014100103 veya wikidatagateway/wikisampledataout/2014100104</span><span class="sxs-lookup"><span data-stu-id="64fa7-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="64fa7-206">Örnek 2</span><span class="sxs-lookup"><span data-stu-id="64fa7-206">Sample 2</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

<span data-ttu-id="64fa7-207">Bu örnekte, folderPath ve fileName özellikleri tarafından kullanılan ayrı değişkenleri içine yıl, ay, gün ve saat SliceStart ayıklanır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="64fa7-208">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="64fa7-208">Copy activity properties</span></span>
<span data-ttu-id="64fa7-209">Bölümler & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz: [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="64fa7-209">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="64fa7-210">Ad, açıklama, giriş ve çıkış veri kümeleri ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="64fa7-211">Bulunan özellikler **typeProperties** etkinlik bölümünü her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-211">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="64fa7-212">Kopya etkinliği için bunlar türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-212">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="64fa7-213">Bir Azure Blob depolama alanından veri taşıyorsanız, kaynak türü için kopyalama etkinliğinde ayarladığınız **BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-213">If you are moving data from an Azure Blob Storage, you set the source type in the copy activity to **BlobSource**.</span></span> <span data-ttu-id="64fa7-214">Bir Azure Blob depolama alanına veri taşıyorsanız, benzer şekilde, Havuz türü için kopyalama etkinliğinde ayarladığınız **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-214">Similarly, if you are moving data to an Azure Blob Storage, you set the sink type in the copy activity to **BlobSink**.</span></span> <span data-ttu-id="64fa7-215">Bu bölümde BlobSource ve BlobSink tarafından desteklenen özellikler listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="64fa7-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="64fa7-216">**BlobSource** aşağıdaki özellikleri destekler **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="64fa7-216">**BlobSource** supports the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="64fa7-217">Özellik</span><span class="sxs-lookup"><span data-stu-id="64fa7-217">Property</span></span> | <span data-ttu-id="64fa7-218">Açıklama</span><span class="sxs-lookup"><span data-stu-id="64fa7-218">Description</span></span> | <span data-ttu-id="64fa7-219">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="64fa7-219">Allowed values</span></span> | <span data-ttu-id="64fa7-220">Gerekli</span><span class="sxs-lookup"><span data-stu-id="64fa7-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="64fa7-221">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="64fa7-221">recursive</span></span> |<span data-ttu-id="64fa7-222">Belirtilen klasörün alt klasörleri ya da yalnızca verileri özyinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-222">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="64fa7-223">(Varsayılan değer) false değerini true</span><span class="sxs-lookup"><span data-stu-id="64fa7-223">True (default value), False</span></span> |<span data-ttu-id="64fa7-224">Hayır</span><span class="sxs-lookup"><span data-stu-id="64fa7-224">No</span></span> |

<span data-ttu-id="64fa7-225">**BlobSink** aşağıdaki özellikleri destekler **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="64fa7-225">**BlobSink** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="64fa7-226">Özellik</span><span class="sxs-lookup"><span data-stu-id="64fa7-226">Property</span></span> | <span data-ttu-id="64fa7-227">Açıklama</span><span class="sxs-lookup"><span data-stu-id="64fa7-227">Description</span></span> | <span data-ttu-id="64fa7-228">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="64fa7-228">Allowed values</span></span> | <span data-ttu-id="64fa7-229">Gerekli</span><span class="sxs-lookup"><span data-stu-id="64fa7-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="64fa7-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="64fa7-230">copyBehavior</span></span> |<span data-ttu-id="64fa7-231">Kaynak BlobSource veya dosya sistemi olduğunda kopyalama davranışını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="64fa7-231">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="64fa7-232"><b>PreserveHierarchy</b>: Dosya hiyerarşisi hedef klasördeki korur.</span><span class="sxs-lookup"><span data-stu-id="64fa7-232"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="64fa7-233">Kaynak dosyanın kaynak klasöre göreli yol, hedef dosya hedef klasöre göreli yolunu aynıdır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-233">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="64fa7-234"><b>FlattenHierarchy</b>: tüm kaynak klasörü hedef klasör ilk düzeyi dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-234"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="64fa7-235">Hedef dosyalar otomatik adına sahip.</span><span class="sxs-lookup"><span data-stu-id="64fa7-235">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="64fa7-236"><b>MergeFiles</b>: bir dosya için kaynak klasöründeki tüm dosyaları birleştirir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-236"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="64fa7-237">Birleştirilmiş Dosya adı, dosya/Blob adı belirtilirse, belirtilen ad olur; Aksi takdirde otomatik olarak oluşturulan dosya adı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-237">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="64fa7-238">Hayır</span><span class="sxs-lookup"><span data-stu-id="64fa7-238">No</span></span> |

<span data-ttu-id="64fa7-239">**BlobSource** geriye dönük uyumluluk için bu iki özellik de destekler.</span><span class="sxs-lookup"><span data-stu-id="64fa7-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="64fa7-240">**treatEmptyAsNull**: null veya boş dize null değeri olarak kabul edilip edilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-240">**treatEmptyAsNull**: Specifies whether to treat null or empty string as null value.</span></span>
* <span data-ttu-id="64fa7-241">**skipHeaderLineCount** -kaç satır atlandı belirtir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="64fa7-242">Yalnızca girdi veri kümesi TextFormat kullandığında geçerli olduğu.</span><span class="sxs-lookup"><span data-stu-id="64fa7-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="64fa7-243">Benzer şekilde, **BlobSink** geriye dönük uyumluluk için aşağıdaki özelliği destekler.</span><span class="sxs-lookup"><span data-stu-id="64fa7-243">Similarly, **BlobSink** supports the following property for backward compatibility.</span></span>

* <span data-ttu-id="64fa7-244">**blobWriterAddHeader**: bir çıkış veri kümesi yazılırken sütun tanımları üstbilgisinin eklenip eklenmeyeceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="64fa7-244">**blobWriterAddHeader**: Specifies whether to add a header of column definitions while writing to an output dataset.</span></span>

<span data-ttu-id="64fa7-245">Veri kümeleri artık aynı işlevselliği uygulamak aşağıdaki özellikleri destekler: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-245">Datasets now support the following properties that implement the same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="64fa7-246">Aşağıdaki tabloda, bu blob kaynak/havuz özellikleri yerine yeni veri kümesi özellikleri kullanma hakkında yönergeler sunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-246">The following table provides guidance on using the new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="64fa7-247">Kopya etkinliği özelliği</span><span class="sxs-lookup"><span data-stu-id="64fa7-247">Copy Activity property</span></span> | <span data-ttu-id="64fa7-248">Veri kümesi özelliği</span><span class="sxs-lookup"><span data-stu-id="64fa7-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="64fa7-249">BlobSource üzerinde skipHeaderLineCount</span><span class="sxs-lookup"><span data-stu-id="64fa7-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="64fa7-250">skipLineCount ve firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="64fa7-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="64fa7-251">Satırlar ilk atlanır ve ilk satırın üstbilgi olarak sonra okuyun.</span><span class="sxs-lookup"><span data-stu-id="64fa7-251">Lines are skipped first and then the first row is read as a header.</span></span> |
| <span data-ttu-id="64fa7-252">BlobSource üzerinde treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="64fa7-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="64fa7-253">girdi veri kümesi üzerinde treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="64fa7-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="64fa7-254">BlobSink üzerinde blobWriterAddHeader</span><span class="sxs-lookup"><span data-stu-id="64fa7-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="64fa7-255">Çıktı veri kümesi üzerinde firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="64fa7-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="64fa7-256">Bkz: [belirtme TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) bu özellikleri hakkında ayrıntılı bilgi için bölüm.</span><span class="sxs-lookup"><span data-stu-id="64fa7-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="64fa7-257">özyinelemeli ve copyBehavior örnekleri</span><span class="sxs-lookup"><span data-stu-id="64fa7-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="64fa7-258">Bu bölümde, sonuçta elde edilen davranışını özyinelemeli ve copyBehavior değerleri farklı birleşimlerini kopyalama işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-258">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="64fa7-259">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="64fa7-259">recursive</span></span> | <span data-ttu-id="64fa7-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="64fa7-260">copyBehavior</span></span> | <span data-ttu-id="64fa7-261">Bunun sonucunda oluşan davranışı</span><span class="sxs-lookup"><span data-stu-id="64fa7-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="64fa7-262">TRUE</span><span class="sxs-lookup"><span data-stu-id="64fa7-262">true</span></span> |<span data-ttu-id="64fa7-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="64fa7-263">preserveHierarchy</span></span> |<span data-ttu-id="64fa7-264">Bir kaynak klasörü için Klasör1 şu yapıda:</span><span class="sxs-lookup"><span data-stu-id="64fa7-264">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="64fa7-265">Klasör1</span><span class="sxs-lookup"><span data-stu-id="64fa7-265">Folder1</span></span><br/><span data-ttu-id="64fa7-266">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="64fa7-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="64fa7-267">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="64fa7-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="64fa7-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="64fa7-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="64fa7-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="64fa7-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="64fa7-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="64fa7-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="64fa7-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="64fa7-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="64fa7-272">Hedef klasör Klasör1 kaynak aynı yapısını oluşturulur</span><span class="sxs-lookup"><span data-stu-id="64fa7-272">the target folder Folder1 is created with the same structure as the source</span></span><br/><br/><span data-ttu-id="64fa7-273">Klasör1</span><span class="sxs-lookup"><span data-stu-id="64fa7-273">Folder1</span></span><br/><span data-ttu-id="64fa7-274">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="64fa7-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="64fa7-275">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="64fa7-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="64fa7-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="64fa7-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="64fa7-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="64fa7-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="64fa7-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="64fa7-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="64fa7-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="64fa7-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="64fa7-280">TRUE</span><span class="sxs-lookup"><span data-stu-id="64fa7-280">true</span></span> |<span data-ttu-id="64fa7-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="64fa7-281">flattenHierarchy</span></span> |<span data-ttu-id="64fa7-282">Bir kaynak klasörü için Klasör1 şu yapıda:</span><span class="sxs-lookup"><span data-stu-id="64fa7-282">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="64fa7-283">Klasör1</span><span class="sxs-lookup"><span data-stu-id="64fa7-283">Folder1</span></span><br/><span data-ttu-id="64fa7-284">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="64fa7-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="64fa7-285">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="64fa7-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="64fa7-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="64fa7-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="64fa7-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="64fa7-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="64fa7-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="64fa7-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="64fa7-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="64fa7-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="64fa7-290">Hedef Klasör1 aşağıdaki yapısıyla oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="64fa7-290">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="64fa7-291">Klasör1</span><span class="sxs-lookup"><span data-stu-id="64fa7-291">Folder1</span></span><br/><span data-ttu-id="64fa7-292">&nbsp;&nbsp;&nbsp;&nbsp;dosya1 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="64fa7-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="64fa7-293">&nbsp;&nbsp;&nbsp;&nbsp;dosya2 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="64fa7-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="64fa7-294">&nbsp;&nbsp;&nbsp;&nbsp;dosya3 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="64fa7-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="64fa7-295">&nbsp;&nbsp;&nbsp;&nbsp;File4 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="64fa7-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="64fa7-296">&nbsp;&nbsp;&nbsp;&nbsp;File5 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="64fa7-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="64fa7-297">TRUE</span><span class="sxs-lookup"><span data-stu-id="64fa7-297">true</span></span> |<span data-ttu-id="64fa7-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="64fa7-298">mergeFiles</span></span> |<span data-ttu-id="64fa7-299">Bir kaynak klasörü için Klasör1 şu yapıda:</span><span class="sxs-lookup"><span data-stu-id="64fa7-299">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="64fa7-300">Klasör1</span><span class="sxs-lookup"><span data-stu-id="64fa7-300">Folder1</span></span><br/><span data-ttu-id="64fa7-301">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="64fa7-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="64fa7-302">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="64fa7-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="64fa7-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="64fa7-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="64fa7-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="64fa7-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="64fa7-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="64fa7-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="64fa7-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="64fa7-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="64fa7-307">Hedef Klasör1 aşağıdaki yapısıyla oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="64fa7-307">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="64fa7-308">Klasör1</span><span class="sxs-lookup"><span data-stu-id="64fa7-308">Folder1</span></span><br/><span data-ttu-id="64fa7-309">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1 + dosya2 + dosya3 + File4 + 5 dosyası içeriği otomatik olarak oluşturulan dosya adında bir dosya halinde birleştirilir</span><span class="sxs-lookup"><span data-stu-id="64fa7-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="64fa7-310">False</span><span class="sxs-lookup"><span data-stu-id="64fa7-310">false</span></span> |<span data-ttu-id="64fa7-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="64fa7-311">preserveHierarchy</span></span> |<span data-ttu-id="64fa7-312">Bir kaynak klasörü için Klasör1 şu yapıda:</span><span class="sxs-lookup"><span data-stu-id="64fa7-312">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="64fa7-313">Klasör1</span><span class="sxs-lookup"><span data-stu-id="64fa7-313">Folder1</span></span><br/><span data-ttu-id="64fa7-314">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="64fa7-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="64fa7-315">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="64fa7-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="64fa7-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="64fa7-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="64fa7-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="64fa7-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="64fa7-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="64fa7-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="64fa7-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="64fa7-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="64fa7-320">Hedef klasör Klasör1 aşağıdaki yapısıyla oluşturulur</span><span class="sxs-lookup"><span data-stu-id="64fa7-320">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="64fa7-321">Klasör1</span><span class="sxs-lookup"><span data-stu-id="64fa7-321">Folder1</span></span><br/><span data-ttu-id="64fa7-322">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="64fa7-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="64fa7-323">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="64fa7-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="64fa7-324">Dosya3, File4 ve File5 Subfolder1 değil toplanma.</span><span class="sxs-lookup"><span data-stu-id="64fa7-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="64fa7-325">False</span><span class="sxs-lookup"><span data-stu-id="64fa7-325">false</span></span> |<span data-ttu-id="64fa7-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="64fa7-326">flattenHierarchy</span></span> |<span data-ttu-id="64fa7-327">Bir kaynak klasörü için Klasör1 şu yapıda:</span><span class="sxs-lookup"><span data-stu-id="64fa7-327">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="64fa7-328">Klasör1</span><span class="sxs-lookup"><span data-stu-id="64fa7-328">Folder1</span></span><br/><span data-ttu-id="64fa7-329">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="64fa7-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="64fa7-330">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="64fa7-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="64fa7-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="64fa7-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="64fa7-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="64fa7-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="64fa7-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="64fa7-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="64fa7-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="64fa7-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="64fa7-335">Hedef klasör Klasör1 aşağıdaki yapısıyla oluşturulur</span><span class="sxs-lookup"><span data-stu-id="64fa7-335">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="64fa7-336">Klasör1</span><span class="sxs-lookup"><span data-stu-id="64fa7-336">Folder1</span></span><br/><span data-ttu-id="64fa7-337">&nbsp;&nbsp;&nbsp;&nbsp;dosya1 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="64fa7-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="64fa7-338">&nbsp;&nbsp;&nbsp;&nbsp;dosya2 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="64fa7-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="64fa7-339">Dosya3, File4 ve File5 Subfolder1 değil toplanma.</span><span class="sxs-lookup"><span data-stu-id="64fa7-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="64fa7-340">False</span><span class="sxs-lookup"><span data-stu-id="64fa7-340">false</span></span> |<span data-ttu-id="64fa7-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="64fa7-341">mergeFiles</span></span> |<span data-ttu-id="64fa7-342">Bir kaynak klasörü için Klasör1 şu yapıda:</span><span class="sxs-lookup"><span data-stu-id="64fa7-342">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="64fa7-343">Klasör1</span><span class="sxs-lookup"><span data-stu-id="64fa7-343">Folder1</span></span><br/><span data-ttu-id="64fa7-344">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="64fa7-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="64fa7-345">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="64fa7-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="64fa7-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="64fa7-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="64fa7-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="64fa7-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="64fa7-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="64fa7-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="64fa7-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="64fa7-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="64fa7-350">Hedef klasör Klasör1 aşağıdaki yapısıyla oluşturulur</span><span class="sxs-lookup"><span data-stu-id="64fa7-350">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="64fa7-351">Klasör1</span><span class="sxs-lookup"><span data-stu-id="64fa7-351">Folder1</span></span><br/><span data-ttu-id="64fa7-352">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1 + dosya2 içeriği otomatik olarak oluşturulan dosya adında bir dosya halinde birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="64fa7-353">dosya1 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="64fa7-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="64fa7-354">Dosya3, File4 ve File5 Subfolder1 değil toplanma.</span><span class="sxs-lookup"><span data-stu-id="64fa7-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage"></a><span data-ttu-id="64fa7-355">İzlenecek yol: Kullanım Kopyalama Sihirbazı ' / Blob depolama biriminden verileri kopyalamak için</span><span class="sxs-lookup"><span data-stu-id="64fa7-355">Walkthrough: Use Copy Wizard to copy data to/from Blob Storage</span></span>
<span data-ttu-id="64fa7-356">Hızlı bir şekilde grafikten bir Azure blob depolama veri kopyalamak nasıl bakalım.</span><span class="sxs-lookup"><span data-stu-id="64fa7-356">Let's look at how to quickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="64fa7-357">Bu kılavuzda, hem kaynak hem de hedef veri türünü depolar: Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="64fa7-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="64fa7-358">Bu kılavuzda ardışık düzen veri bir klasörden aynı blob kapsayıcısında başka bir klasöre kopyalar.</span><span class="sxs-lookup"><span data-stu-id="64fa7-358">The pipeline in this walkthrough copies data from a folder to another folder in the same blob container.</span></span> <span data-ttu-id="64fa7-359">Bu kılavuz, Blob Depolama kaynağı veya havuz olarak kullanırken ayarları veya özellikleri göstermek kasıtlı olarak basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-359">This walkthrough is intentionally simple to show you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="64fa7-360">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="64fa7-360">Prerequisites</span></span>
1. <span data-ttu-id="64fa7-361">Bir genel amaçlı oluşturma **Azure depolama hesabı** zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="64fa7-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="64fa7-362">Her iki biçimde blob storage kullanma **kaynak** ve **hedef** verileri depolamak bu kılavuzda.</span><span class="sxs-lookup"><span data-stu-id="64fa7-362">You use the blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="64fa7-363">bir Azure depolama hesabınız yoksa bkz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) makale oluşturmak adımlar.</span><span class="sxs-lookup"><span data-stu-id="64fa7-363">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
2. <span data-ttu-id="64fa7-364">Adlı bir blob kapsayıcı oluşturun **adfblobconnector** depolama hesabındaki.</span><span class="sxs-lookup"><span data-stu-id="64fa7-364">Create a blob container named **adfblobconnector** in the storage account.</span></span> 
4. <span data-ttu-id="64fa7-365">Adlı bir klasör oluşturun **giriş** içinde **adfblobconnector** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="64fa7-365">Create a folder named **input** in the **adfblobconnector** container.</span></span>
5. <span data-ttu-id="64fa7-366">Adlı bir dosya oluşturun **emp.txt** ile aşağıdaki içerik ve kendisine karşıya **giriş** gibi araçları kullanarak klasör [Azure Storage Gezgini](https://azurestorageexplorer.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="64fa7-366">Create a file named **emp.txt** with the following content and upload it to the **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-the-data-factory"></a><span data-ttu-id="64fa7-367">Veri Fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="64fa7-367">Create the data factory</span></span>
1. <span data-ttu-id="64fa7-368">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-368">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="64fa7-369">Tıklatın **+ yeni** sol üst köşeden tıklatın **Intelligence + analiz**, tıklatıp **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-369">Click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="64fa7-370">**Yeni data factory** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="64fa7-370">In the **New data factory** blade:</span></span>   
    1. <span data-ttu-id="64fa7-371">Girin **ADFBlobConnectorDF** için **adı**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-371">Enter **ADFBlobConnectorDF** for the **name**.</span></span> <span data-ttu-id="64fa7-372">Azure veri fabrikasının adı genel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-372">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="64fa7-373">Hatayı alırsanız: `*Data factory name “ADFBlobConnectorDF” is not available`, veri fabrikası (örneğin, yournameADFBlobConnectorDF) adını değiştirin ve oluşturmayı yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-373">If you receive the error: `*Data factory name “ADFBlobConnectorDF” is not available`, change the name of the data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="64fa7-374">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="64fa7-375">Azure **aboneliğinizi** seçin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="64fa7-376">Kaynak grubu için seçin **kullanım varolan** varolan bir kaynak grubu seçin (veya) seçmek için **Yeni Oluştur** bir kaynak grubu için bir ad girmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="64fa7-376">For Resource Group, select **Use existing** to select an existing resource group (or) select **Create new** to enter a name for a resource group.</span></span>
    4. <span data-ttu-id="64fa7-377">Veri fabrikası için bir **konum** seçin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-377">Select a **location** for the data factory.</span></span>
    5. <span data-ttu-id="64fa7-378">Dikey pencerenin alt kısmındaki **Panoya sabitle** onay kutusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-378">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>
    6. <span data-ttu-id="64fa7-379">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-379">Click **Create**.</span></span>
3. <span data-ttu-id="64fa7-380">Oluşturma işlemi tamamlandıktan sonra gördüğünüz **Data Factory** dikey penceresini aşağıdaki görüntüde gösterildiği gibi: ![Data factory giriş sayfası](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="64fa7-380">After the creation is complete, you see the **Data Factory** blade as shown in the following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="64fa7-381">Kopyalama Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="64fa7-381">Copy Wizard</span></span>
1. <span data-ttu-id="64fa7-382">Data Factory giriş sayfasında, tıklatın **kopyalama [Önizleme] verileri** başlatmak için döşeme **kopyalama veri Sihirbazı** ayrı bir sekmede.</span><span class="sxs-lookup"><span data-stu-id="64fa7-382">On the Data Factory home page, click the **Copy data [PREVIEW]** tile to launch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="64fa7-383">Web tarayıcısının "Yetkilendiriliyor..." durumunda takıldığını görürseniz, devre dışı bırakın/işaretini **üçüncü taraf tanımlama bilgilerini engelleyebilir ve site verileri** ayarlama (veya) etkin ve oluşturmak için bir özel durum **login.microsoftonline.com** ve ardından Sihirbazı yeniden başlatmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-383">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
2. <span data-ttu-id="64fa7-384">**Özellikler** sayfasında:</span><span class="sxs-lookup"><span data-stu-id="64fa7-384">In the **Properties** page:</span></span>
    1. <span data-ttu-id="64fa7-385">Girin **CopyPipeline** için **görev adı**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="64fa7-386">Görev adı, veri fabrikasında ardışık düzeni adıdır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-386">The task name is the name of the pipeline in your data factory.</span></span>
    2. <span data-ttu-id="64fa7-387">Girin bir **açıklama** görevin (isteğe bağlı).</span><span class="sxs-lookup"><span data-stu-id="64fa7-387">Enter a **description** for the task (optional).</span></span>
    3. <span data-ttu-id="64fa7-388">İçin **görev tempoyla veya görev zamanlama**, tutmak **düzenli olarak zamanında** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="64fa7-388">For **Task cadence or Task schedule**, keep the **Run regularly on schedule** option.</span></span> <span data-ttu-id="64fa7-389">Bu görevi yalnızca bir kez art arda bir zamanlamaya göre çalıştır yerine çalıştırmak isteyip istemediğinizi seçin **kez Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-389">If you want to run this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="64fa7-390">Öğesini seçerseniz, **kez Şimdi Çalıştır** seçeneği, bir [tek seferlik ardışık düzen](data-factory-create-pipelines.md#onetime-pipeline) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="64fa7-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="64fa7-391">Ayarlarını koruyabilirsiniz **yinelenen desen**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-391">Keep the settings for **Recurring pattern**.</span></span> <span data-ttu-id="64fa7-392">Bu görev, sonraki adımda belirttiğiniz her gün başlangıç ve bitiş zamanları arasında çalışır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-392">This task runs daily between the start and end times you specify in the next step.</span></span>
    5. <span data-ttu-id="64fa7-393">Değişiklik **başlangıç tarihi ve saati** için **21/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-393">Change the **Start date time** to **04/21/2017**.</span></span> 
    6. <span data-ttu-id="64fa7-394">Değişiklik **bitiş tarihi ve saati** için **25/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-394">Change the **End date time** to **04/25/2017**.</span></span> <span data-ttu-id="64fa7-395">Takvim gözatma yerine tarihi yazın isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64fa7-395">You may want to type the date instead of browsing through the calendar.</span></span>     
    8. <span data-ttu-id="64fa7-396">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-396">Click **Next**.</span></span>
      <span data-ttu-id="64fa7-397">![Kopyalama aracı - Özellikler sayfası](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="64fa7-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="64fa7-398">**Kaynak veri deposu** sayfasında **Azure Blob Storage** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-398">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="64fa7-399">Kopyalama görevine yönelik kaynak veri deposunu belirtmek için bu sayfayı kullanın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-399">You use this page to specify the source data store for the copy task.</span></span> <span data-ttu-id="64fa7-400">Yeni bir veri deposu belirtmek için mevcut bir veri deposu bağlı hizmetini kullanabilirsiniz (veya) yeni bir veri deposu belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64fa7-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="64fa7-401">Mevcut bir bağlı hizmeti kullanmak için seçeceğiniz **mevcut bağlı hizmetlerden** ve doğru bağlı hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-401">To use an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select the right linked service.</span></span> 
    <span data-ttu-id="64fa7-402">![Kopyalama aracı - kaynak veri deposu sayfası](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="64fa7-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="64fa7-403">**Azure Blob depolama hesabı belirtin** sayfasında:</span><span class="sxs-lookup"><span data-stu-id="64fa7-403">On the **Specify the Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="64fa7-404">İçin otomatik olarak oluşturulan adı bırakın **bağlantı adı**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-404">Keep the auto-generated name for **Connection name**.</span></span> <span data-ttu-id="64fa7-405">Bağlantı adı türündeki bağlı hizmetin adıdır: Azure depolama.</span><span class="sxs-lookup"><span data-stu-id="64fa7-405">The connection name is the name of the linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="64fa7-406">**Hesap seçme yöntemi** için **Azure aboneliklerinden** seçeneğinin belirlendiğini onaylayın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="64fa7-407">Azure aboneliğinizi seçin ya da koruma **Tümünü Seç** için **Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="64fa7-408">Seçili abonelikte bulunan Azure depolama hesapları listesinden bir **Azure depolama hesabı** seçin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-408">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="64fa7-409">Ayrıca depolama hesabı ayarlarını el ile girmeyi seçebilirsiniz **el ile girmeniz** seçenek için **hesap seçme yöntemi**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-409">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**.</span></span>
   5. <span data-ttu-id="64fa7-410">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-410">Click **Next**.</span></span> 
      <span data-ttu-id="64fa7-411">![Kopyalama aracı - Azure Blob Depolama hesabı belirtin](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="64fa7-411">![Copy Tool - Specify the Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="64fa7-412">**Girdi dosyası veya klasörü seçin** sayfasında:</span><span class="sxs-lookup"><span data-stu-id="64fa7-412">On **Choose the input file or folder** page:</span></span>
   1. <span data-ttu-id="64fa7-413">Çift **adfblobcontainer**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="64fa7-414">Seçin **giriş**, tıklatıp **Seç**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="64fa7-415">Bu kılavuzda, giriş klasörü seçin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-415">In this walkthrough, you select the input folder.</span></span> <span data-ttu-id="64fa7-416">Ayrıca emp.txt dosya klasöründe yerine seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64fa7-416">You could also select the emp.txt file in the folder instead.</span></span> 
      <span data-ttu-id="64fa7-417">![Kopyalama aracı - girdi dosyası veya klasörü seçin](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="64fa7-417">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="64fa7-418">Üzerinde **girdi dosyası veya klasörü seçin** sayfa:</span><span class="sxs-lookup"><span data-stu-id="64fa7-418">On the **Choose the input file or folder** page:</span></span>
    1. <span data-ttu-id="64fa7-419">Onaylayın **dosya veya klasör** ayarlanır **adfblobconnector/giriş**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-419">Confirm that the **file or folder** is set to **adfblobconnector/input**.</span></span> <span data-ttu-id="64fa7-420">Dosyaları alt klasörlerde, örneğin, 04/2017/01, 04/2017/02 ve vb. adfblobconnector/giriş girin / {year} / {month} / {day} dosya veya klasör için.</span><span class="sxs-lookup"><span data-stu-id="64fa7-420">If the files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="64fa7-421">Metin kutusu dışında SEKME tuşuna bastığınızda biçimlerini (yyyy) yıl, ay (MM) ve gün (dd) seçmek için üç açılan listeleri bakın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-421">When you press TAB out of the text box, you see three drop-down lists to select formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="64fa7-422">Ayarlamayın **kopyalayın dosyayı yinelemeli olarak**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="64fa7-423">Hedefe kopyalanacak dosyaları yinelemeli olarak çapraz klasörlerde için bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-423">Select this option to recursively traverse through folders for files to be copied to the destination.</span></span> 
    3. <span data-ttu-id="64fa7-424">Sağlamadığı **ikili kopyalama** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="64fa7-424">Do not the **binary copy** option.</span></span> <span data-ttu-id="64fa7-425">Hedef kaynak dosyaya ikili bir kopyasını gerçekleştirmek için bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-425">Select this option to perform a binary copy of source file to the destination.</span></span> <span data-ttu-id="64fa7-426">Daha fazla seçenek sonraki sayfalarda görebilmeniz için bu kılavuzda seçmeyin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-426">Do not select for this walkthrough so that you can see more options in the next pages.</span></span> 
    4. <span data-ttu-id="64fa7-427">Onaylayın **sıkıştırma türünü** ayarlanır **hiçbiri**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-427">Confirm that the **Compression type** is set to **None**.</span></span> <span data-ttu-id="64fa7-428">Kaynak dosyalar desteklenen biçimlerden birinde sıkıştırılmış bu seçenek için bir değer seçin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-428">Select a value for this option if your source files are compressed in one of the supported formats.</span></span> 
    5. <span data-ttu-id="64fa7-429">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-429">Click **Next**.</span></span>
    <span data-ttu-id="64fa7-430">![Kopyalama aracı - girdi dosyası veya klasörü seçin](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="64fa7-430">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="64fa7-431">**Dosya biçimi ayarları** sayfasında sınırlayıcıları ve sihirbaz tarafından dosya ayrıştırılarak otomatik olarak algılanan düzeni görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="64fa7-431">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> 
    1. <span data-ttu-id="64fa7-432">Aşağıdaki seçenekler onaylayın: bir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-432">Confirm the following options: a.</span></span> <span data-ttu-id="64fa7-433">**Dosya biçimi** ayarlanır **metin biçimi**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-433">The **file format** is set to **Text format**.</span></span> <span data-ttu-id="64fa7-434">Aşağı açılan listesinde tüm desteklenen biçimler görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64fa7-434">You can see all the supported formats in the drop-down list.</span></span> <span data-ttu-id="64fa7-435">Örneğin: JSON, Avro, ORC, Parquet.</span><span class="sxs-lookup"><span data-stu-id="64fa7-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="64fa7-436">b.</span><span class="sxs-lookup"><span data-stu-id="64fa7-436">b.</span></span> <span data-ttu-id="64fa7-437">**Sütun sınırlayıcı** ayarlanır `Comma (,)`.</span><span class="sxs-lookup"><span data-stu-id="64fa7-437">The **column delimiter** is set to `Comma (,)`.</span></span> <span data-ttu-id="64fa7-438">Aşağı açılan listesinde Data Factory ile desteklenen diğer sütun sınırlayıcıları görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64fa7-438">You can see the other column delimiters supported by Data Factory in the drop-down list.</span></span> <span data-ttu-id="64fa7-439">Özel bir sınırlayıcı de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64fa7-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="64fa7-440">c.</span><span class="sxs-lookup"><span data-stu-id="64fa7-440">c.</span></span> <span data-ttu-id="64fa7-441">**Satır ayırıcı** ayarlanır `Carriage Return + Line feed (\r\n)`.</span><span class="sxs-lookup"><span data-stu-id="64fa7-441">The **row delimiter** is set to `Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="64fa7-442">Aşağı açılan listesinde Data Factory ile desteklenen diğer satır sınırlayıcıları görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64fa7-442">You can see the other row delimiters supported by Data Factory in the drop-down list.</span></span> <span data-ttu-id="64fa7-443">Özel bir sınırlayıcı de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64fa7-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="64fa7-444">d.</span><span class="sxs-lookup"><span data-stu-id="64fa7-444">d.</span></span> <span data-ttu-id="64fa7-445">**Satır sayısı atla** ayarlanır **0**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-445">The **skip line count** is set to **0**.</span></span> <span data-ttu-id="64fa7-446">Dosyanın üst kısmında atlanacak birkaç satır numarasını buraya girin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-446">If you want a few lines to be skipped at the top of the file, enter the number here.</span></span>
        <span data-ttu-id="64fa7-447">e.</span><span class="sxs-lookup"><span data-stu-id="64fa7-447">e.</span></span>  <span data-ttu-id="64fa7-448">**İlk veri satırı sütun adları içeren** ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="64fa7-448">The **first data row contains column names** is not set.</span></span> <span data-ttu-id="64fa7-449">İlk satırı sütun adları kaynak dosyaları içeriyorsa, bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-449">If the source files contain column names in the first row, select this option.</span></span>
        <span data-ttu-id="64fa7-450">f.</span><span class="sxs-lookup"><span data-stu-id="64fa7-450">f.</span></span> <span data-ttu-id="64fa7-451">**Boş sütun değeri null olarak davran** seçeneği ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="64fa7-451">The **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="64fa7-452">Genişletme **Gelişmiş ayarları** Gelişmiş seçeneği kullanılabilir görmek için.</span><span class="sxs-lookup"><span data-stu-id="64fa7-452">Expand **Advanced settings** to see advanced option available.</span></span>
    3. <span data-ttu-id="64fa7-453">Sayfanın alt kısmındaki bkz **Önizleme** emp.txt dosya verileri.</span><span class="sxs-lookup"><span data-stu-id="64fa7-453">At the bottom of the page, see the **preview** of data from the emp.txt file.</span></span>
    4. <span data-ttu-id="64fa7-454">Tıklatın **şema** kaynak dosyasında veri bakarak Kopyalama Sihirbazı'nı çıkarımı yapılan şema görmek için alt sekmesi.</span><span class="sxs-lookup"><span data-stu-id="64fa7-454">Click **SCHEMA** tab at the bottom to see the schema that the copy wizard inferred by looking at the data in the source file.</span></span>
    5. <span data-ttu-id="64fa7-455">Sınırlayıcıları gözden geçirin verilerin önizlemesini gördükten sonra **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-455">Click **Next** after you review the delimiters and preview data.</span></span>
    <span data-ttu-id="64fa7-456">![Kopyalama aracı - dosya biçimi ayarları](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="64fa7-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="64fa7-457">Üzerinde **hedef veri deposu sayfası**seçin **Azure Blob Storage**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-457">On the **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="64fa7-458">Kaynak ve hedef veri depolarına bu kılavuzda olarak Azure Blob Storage kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="64fa7-458">You are using the Azure Blob Storage as both the source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="64fa7-459">![Kopyalama aracı - select hedef veri deposu](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="64fa7-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="64fa7-460">Üzerinde **Azure Blob Depolama hesabı belirtin** sayfa:</span><span class="sxs-lookup"><span data-stu-id="64fa7-460">On **Specify the Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="64fa7-461">Girin **AzureStorageLinkedService** için **bağlantı adı** alan.</span><span class="sxs-lookup"><span data-stu-id="64fa7-461">Enter **AzureStorageLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="64fa7-462">**Hesap seçme yöntemi** için **Azure aboneliklerinden** seçeneğinin belirlendiğini onaylayın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="64fa7-463">Azure **aboneliğinizi** seçin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="64fa7-464">Azure depolama hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="64fa7-465">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-465">Click **Next**.</span></span>     
10. <span data-ttu-id="64fa7-466">Üzerinde **çıktı dosyası veya klasörü seçin** sayfa:</span><span class="sxs-lookup"><span data-stu-id="64fa7-466">On the **Choose the output file or folder** page:</span></span> 
    6. <span data-ttu-id="64fa7-467">belirtin **klasör yolu** olarak **adfblobconnector/çıkış / {year} / {month} / {day}**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="64fa7-468">Girin **sekmesini**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="64fa7-469">İçin **yıl**seçin **yyyy**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-469">For the **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="64fa7-470">İçin **ay**, kümesine olduğunu onaylayın **MM**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-470">For the **month**, confirm that it is set to **MM**.</span></span>
    9. <span data-ttu-id="64fa7-471">İçin **gün**, kümesine olduğunu onaylayın **GG**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-471">For the **day**, confirm that it is set to **dd**.</span></span>
    10. <span data-ttu-id="64fa7-472">Onaylayın **sıkıştırma türünü** ayarlanır **hiçbiri**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-472">Confirm that the **compression type** is set to **None**.</span></span>
    11. <span data-ttu-id="64fa7-473">Onaylayın **kopyalama davranışı** ayarlanır **dosyaları Birleştir**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-473">Confirm that the **copy behavior** is set to **Merge files**.</span></span> <span data-ttu-id="64fa7-474">Aynı ada sahip çıktı dosyası zaten varsa, yeni içerik aynı dosyanın sonuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-474">If the output file with the same name already exists, the new content is added to the same file at the end.</span></span>
    12. <span data-ttu-id="64fa7-475">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-475">Click **Next**.</span></span>
    <span data-ttu-id="64fa7-476">![Kopyalama aracı - çıktı dosyası veya klasörü seçin](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="64fa7-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="64fa7-477">Üzerinde **dosya biçimi ayarları** sayfasında, ayarları gözden geçirin ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-477">On the **File format settings** page, review the settings, and click **Next**.</span></span> <span data-ttu-id="64fa7-478">Ek seçenekler burada ve çıktı dosyası için bir başlık eklemek için biridir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-478">One of the additional options here is to add a header to the output file.</span></span> <span data-ttu-id="64fa7-479">Bu seçeneği belirlerseniz, bir başlık satırı sütunlarının adlarını kaynak şemadan eklenir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-479">If you select that option, a header row is added with names of the columns from the schema of the source.</span></span> <span data-ttu-id="64fa7-480">Varsayılan sütun adları kaynağı için şema görüntülerken yeniden adlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64fa7-480">You can rename the default column names when viewing the schema for the source.</span></span> <span data-ttu-id="64fa7-481">Örneğin, ad ve Soyadı ikinci sütuna ilk sütun değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-481">For example, you could change the first column to First Name and second column to Last Name.</span></span> <span data-ttu-id="64fa7-482">Ardından, çıktı dosyası bu adları içeren bir başlık sütun adları olarak üretilir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-482">Then, the output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="64fa7-483">![Kopyalama aracı - hedef için dosya biçimi ayarları](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="64fa7-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="64fa7-484">Üzerinde **performans ayarlarını** sayfasında, onaylayın **bulut birimleri** ve **paralel kopyaları** ayarlanır **otomatik**, İleri'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-484">On the **Performance settings** page, confirm that **cloud units** and **parallel copies** are set to **Auto**, and click Next.</span></span> <span data-ttu-id="64fa7-485">Bu ayarlar hakkında daha fazla ayrıntı için bkz: [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md#parallel-copy).</span><span class="sxs-lookup"><span data-stu-id="64fa7-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="64fa7-486">![Kopyalama aracı - performans ayarları](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="64fa7-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="64fa7-487">Üzerinde **Özet** sayfasında (görev özellikleri, kaynak ve hedef ayarları ve kopya ayarlarını) tüm ayarları gözden geçirin ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-487">On the **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="64fa7-488">![Kopyalama aracı - Özet sayfası](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="64fa7-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="64fa7-489">**Özet** sayfasındaki bilgileri gözden geçirin ve **Son**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-489">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="64fa7-490">Sihirbaz, veri fabrikasında (Kopyalama Sihirbazı’nı başlattığınız yer) iki bağlı hizmet, iki veri kümesi (girdi ve çıktı) ve bir işlem hattı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="64fa7-490">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span>
    <span data-ttu-id="64fa7-491">![Kopyalama aracı - dağıtım sayfası](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="64fa7-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-the-pipeline-copy-task"></a><span data-ttu-id="64fa7-492">(Kopyalama görevi) işlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="64fa7-492">Monitor the pipeline (copy task)</span></span>

1. <span data-ttu-id="64fa7-493">Bağlantıya tıklayın `Click here to monitor copy pipeline` üzerinde **dağıtım** sayfası.</span><span class="sxs-lookup"><span data-stu-id="64fa7-493">Click the link `Click here to monitor copy pipeline` on the **Deployment** page.</span></span> 
2. <span data-ttu-id="64fa7-494">Görmeniz gerekir **izleme ve yönetme uygulaması** ayrı bir sekmede.  ![İzleme ve uygulama yönetme](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="64fa7-494">You should see the **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="64fa7-495">Değişiklik **Başlat** en üstte zaman `04/19/2017` ve **son** için zaman `04/27/2017`ve ardından **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-495">Change the **start** time at the top to `04/19/2017` and **end** time to `04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="64fa7-496">Beş etkinlik Windows'da görmelisiniz **etkinlik WINDOWS** listesi.</span><span class="sxs-lookup"><span data-stu-id="64fa7-496">You should see five activity windows in the **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="64fa7-497">**WindowStart** kez ardışık düzen baştan bitiş zamanları kanal tüm günler kapak.</span><span class="sxs-lookup"><span data-stu-id="64fa7-497">The **WindowStart** times should cover all days from pipeline start to pipeline end times.</span></span> 
5. <span data-ttu-id="64fa7-498">Tıklatın **yenileme** için düğmesini **etkinlik WINDOWS** birkaç kez tüm etkinlik windows durumunu görene kadar listesini hazır ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-498">Click **Refresh** button for the **ACTIVITY WINDOWS** list a few times until you see the status of all the activity windows is set to Ready.</span></span> 
6. <span data-ttu-id="64fa7-499">Şimdi, çıktı dosyaları adfblobconnector kapsayıcı çıkış klasöründe oluşturulan doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-499">Now, verify that the output files are generated in the output folder of adfblobconnector container.</span></span> <span data-ttu-id="64fa7-500">Çıkış klasöründe aşağıdaki klasör yapısını görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="64fa7-500">You should see the following folder structure in the output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="64fa7-501">İzleme ve veri fabrikaları yönetme hakkında ayrıntılı bilgi için bkz: [İzleyici ve Data Factory işlem hattı yönetmek](data-factory-monitor-manage-app.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="64fa7-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="64fa7-502">Data Factory varlıklarını</span><span class="sxs-lookup"><span data-stu-id="64fa7-502">Data Factory entities</span></span>
<span data-ttu-id="64fa7-503">Data Factory giriş sayfası sekmesi için şimdi dönün.</span><span class="sxs-lookup"><span data-stu-id="64fa7-503">Now, switch back to the tab with the Data Factory home page.</span></span> <span data-ttu-id="64fa7-504">İki bağlı hizmet, iki veri kümesi ve bir ardışık düzeni, veri fabrikası'nda artık dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![Varlıklarla Data Factory giriş sayfası](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="64fa7-506">Tıklatın **yazar ve dağıtma** Data Factory Düzenleyici başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="64fa7-506">Click **Author and deploy** to launch Data Factory Editor.</span></span> 

![Data Factory Düzenleyicisi](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="64fa7-508">Veri fabrikanızın aşağıdaki Data Factory varlıklarını görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="64fa7-508">You should see the following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="64fa7-509">İki bağlı hizmet.</span><span class="sxs-lookup"><span data-stu-id="64fa7-509">Two linked services.</span></span> <span data-ttu-id="64fa7-510">Bir kaynak ve hedef için başka bir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-510">One for the source and the other one for the destination.</span></span> <span data-ttu-id="64fa7-511">Bu kılavuzda aynı Azure depolama hesabı her iki bağlı hizmet bakın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-511">Both the linked services refer to the same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="64fa7-512">İki veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="64fa7-512">Two datasets.</span></span> <span data-ttu-id="64fa7-513">Bir giriş veri kümesi ve bir çıkış veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="64fa7-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="64fa7-514">Bu kılavuzda, her ikisi de aynı blob kapsayıcısı kullanır ancak farklı klasörlere (girdi ve çıktı) bakın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-514">In this walkthrough, both use the same blob container but refer to different folders (input and output).</span></span>
 - <span data-ttu-id="64fa7-515">Ardışık Düzen.</span><span class="sxs-lookup"><span data-stu-id="64fa7-515">A pipeline.</span></span> <span data-ttu-id="64fa7-516">Ardışık düzen, verileri bir Azure blob konumundan başka bir Azure blob konumuna kopyalamak için bir blob kaynağı ve blob havuz kullanan kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-516">The pipeline contains a copy activity that uses a blob source and a blob sink to copy data from an Azure blob location to another Azure blob location.</span></span> 

<span data-ttu-id="64fa7-517">Aşağıdaki bölümler bu varlıkları hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="64fa7-517">The following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="64fa7-518">Bağlı hizmetler</span><span class="sxs-lookup"><span data-stu-id="64fa7-518">Linked services</span></span>
<span data-ttu-id="64fa7-519">İki bağlı hizmet görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-519">You should see two linked services.</span></span> <span data-ttu-id="64fa7-520">Bir kaynak ve hedef için başka bir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-520">One for the source and the other one for the destination.</span></span> <span data-ttu-id="64fa7-521">Bu kılavuzda, her iki tanımları aynı adları dışında arayın.</span><span class="sxs-lookup"><span data-stu-id="64fa7-521">In this walkthrough, both definitions look the same except for the names.</span></span> <span data-ttu-id="64fa7-522">**Türü** bağlı hizmetin adı ayarlamak **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-522">The **type** of the linked service is set to **AzureStorage**.</span></span> <span data-ttu-id="64fa7-523">Bağlantılı hizmet tanımını en önemli özelliği **connectionString**, hangi veri fabrikası tarafından çalışma zamanında Azure Storage hesabınıza bağlanmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-523">Most important property of the linked service definition is the **connectionString**, which is used by Data Factory to connect to your Azure Storage account at runtime.</span></span> <span data-ttu-id="64fa7-524">HubName özelliği tanımı'ndaki yoksay.</span><span class="sxs-lookup"><span data-stu-id="64fa7-524">Ignore the hubName property in the definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="64fa7-525">Kaynak blob storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="64fa7-525">Source blob storage linked service</span></span>
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="64fa7-526">Hedef blob depolama bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="64fa7-526">Destination blob storage linked service</span></span>

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

<span data-ttu-id="64fa7-527">Azure Storage bağlı hizmeti hakkında daha fazla bilgi için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="64fa7-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="64fa7-528">Veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="64fa7-528">Datasets</span></span>
<span data-ttu-id="64fa7-529">İki veri kümesi vardır: bir giriş veri kümesi ve bir çıkış veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="64fa7-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="64fa7-530">Veri kümesi türü kümesine **AzureBlob** her ikisi için de.</span><span class="sxs-lookup"><span data-stu-id="64fa7-530">The type of the dataset is set to **AzureBlob** for both.</span></span> 

<span data-ttu-id="64fa7-531">Girdi veri kümesi işaret **giriş** klasöründe **adfblobconnector** blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="64fa7-531">The input dataset points to the **input** folder of the **adfblobconnector** blob container.</span></span> <span data-ttu-id="64fa7-532">**Dış** özelliği ayarlanmış **true** bu veri kümesi için verileri bu veri kümesine bir girdi olarak alır kopyalama etkinliği ile ardışık düzen tarafından üretilen değil olarak.</span><span class="sxs-lookup"><span data-stu-id="64fa7-532">The **external** property is set to **true** for this dataset as the data is not produced by the pipeline with the copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="64fa7-533">Çıktı veri kümesi işaret **çıkış** aynı blob kapsayıcısının klasör.</span><span class="sxs-lookup"><span data-stu-id="64fa7-533">The output dataset points to the **output** folder of the same blob container.</span></span> <span data-ttu-id="64fa7-534">Çıktı veri kümesi yıl, ay ve günün kullanan **SliceStart** çıktı dosyası yolu dinamik olarak değerlendirilecek sistem değişkeni.</span><span class="sxs-lookup"><span data-stu-id="64fa7-534">The output dataset also uses the year, month, and day of the **SliceStart** system variable to dynamically evaluate the path for the output file.</span></span> <span data-ttu-id="64fa7-535">İşlevler ve Data Factory ile desteklenen sistem değişkenleri listesi için bkz: [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="64fa7-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="64fa7-536">**Dış** özelliği ayarlanmış **false** (varsayılan değer) bu veri kümesi ardışık düzen tarafından üretilen olduğundan.</span><span class="sxs-lookup"><span data-stu-id="64fa7-536">The **external** property is set to **false** (default value) because this dataset is produced by the pipeline.</span></span> 

<span data-ttu-id="64fa7-537">Azure Blob veri kümesi tarafından desteklenen özellikler hakkında daha fazla bilgi için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="64fa7-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="64fa7-538">Girdi veri kümesi</span><span class="sxs-lookup"><span data-stu-id="64fa7-538">Input dataset</span></span>

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a><span data-ttu-id="64fa7-539">Çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="64fa7-539">Output dataset</span></span>

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a><span data-ttu-id="64fa7-540">İşlem hattı</span><span class="sxs-lookup"><span data-stu-id="64fa7-540">Pipeline</span></span>
<span data-ttu-id="64fa7-541">Ardışık Düzen yalnızca bir etkinlik vardır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-541">The pipeline has just one activity.</span></span> <span data-ttu-id="64fa7-542">**Türü** etkinliğini kümesine **kopya**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-542">The **type** of the activity is set to **Copy**.</span></span>  <span data-ttu-id="64fa7-543">Etkinlik türü özelliklerini iki bölümü, kaynak için bir ve havuz için başka bir vardır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-543">In the type properties for the activity, there are two sections, one for source and the other one for sink.</span></span> <span data-ttu-id="64fa7-544">Kaynak türü kümesine **BlobSource** etkinlik bir blob depolama alanından veri kopyalama gibi.</span><span class="sxs-lookup"><span data-stu-id="64fa7-544">The source type is set to **BlobSource** as the activity is copying data from a blob storage.</span></span> <span data-ttu-id="64fa7-545">Havuz türü kümesine **BlobSink** bir blob depolama alanına veri kopyalama etkinlik olarak.</span><span class="sxs-lookup"><span data-stu-id="64fa7-545">The sink type is set to **BlobSink** as the activity copying data to a blob storage.</span></span> <span data-ttu-id="64fa7-546">Kopya etkinliği InputDataset z4y giriş olarak alır ve çıktı olarak OutputDataset z4y.</span><span class="sxs-lookup"><span data-stu-id="64fa7-546">The copy activity takes InputDataset-z4y as the input and OutputDataset-z4y as the output.</span></span> 

<span data-ttu-id="64fa7-547">BlobSource ve BlobSink tarafından desteklenen özellikler hakkında daha fazla bilgi için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="64fa7-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-to-and-from-blob-storage"></a><span data-ttu-id="64fa7-548">Depolamaya ve Blob depolamadan veri kopyalamak için JSON örnekleri</span><span class="sxs-lookup"><span data-stu-id="64fa7-548">JSON examples for copying data to and from Blob Storage</span></span>  
<span data-ttu-id="64fa7-549">Aşağıdaki örnekleri kullanarak bir işlem hattı oluşturmak için kullanabileceğiniz örnek JSON tanımları sağlar [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="64fa7-549">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="64fa7-550">Bunlar ve Azure Blob Storage ve Azure SQL veritabanına veri kopyalamak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-550">They show how to copy data to and from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="64fa7-551">Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden herhangi birine belirtildiği havuzlarını kaynakları [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kopya etkinliği Azure Data Factory kullanarak.</span><span class="sxs-lookup"><span data-stu-id="64fa7-551">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-to-sql-database"></a><span data-ttu-id="64fa7-552">JSON örnek: verileri Blob depolama alanından SQL veritabanına kopyalamak</span><span class="sxs-lookup"><span data-stu-id="64fa7-552">JSON Example: Copy data from Blob Storage to SQL Database</span></span>
<span data-ttu-id="64fa7-553">Aşağıdaki örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="64fa7-553">The following sample shows:</span></span>

1. <span data-ttu-id="64fa7-554">Bağlı hizmet türü [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="64fa7-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="64fa7-555">Bağlı hizmet türü [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="64fa7-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="64fa7-556">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="64fa7-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="64fa7-557">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="64fa7-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="64fa7-558">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](#copy-activity-properties) ve [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="64fa7-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="64fa7-559">Zaman serisi bir Azure SQL verileri Azure blob örnek kopyaları saatlik tablo.</span><span class="sxs-lookup"><span data-stu-id="64fa7-559">The sample copies time-series data from an Azure blob to an Azure SQL table hourly.</span></span> <span data-ttu-id="64fa7-560">Bu örnekler kullanılan JSON özellikleri örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-560">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="64fa7-561">**Azure SQL bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="64fa7-561">**Azure SQL linked service:**</span></span>

```json
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
<span data-ttu-id="64fa7-562">**Azure Storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="64fa7-562">**Azure Storage linked service:**</span></span>

```json
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
<span data-ttu-id="64fa7-563">Azure Data Factory iki tür Azure Storage bağlı hizmeti destekler: **AzureStorage** ve **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="64fa7-564">İlk biri için hesap anahtarı içeren bağlantı dizesini belirtin ve daha sonra biri için paylaşılan erişim imzası (SAS) URI'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-564">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="64fa7-565">Bkz: [bağlı hizmetler](#linked-service-properties) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="64fa7-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="64fa7-566">**Azure Blob girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="64fa7-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="64fa7-567">Veri toplanma yeni blob üzerinden saatte (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="64fa7-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="64fa7-568">Blob klasör yolu ve dosya adı dinamik olarak değerlendirilir işleniyor dilim başlangıç zamanı temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="64fa7-568">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="64fa7-569">Klasör yolu yıl, ay ve gün kısmını başlangıç saati ve dosya adı başlangıç zamanı saat bölümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-569">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="64fa7-570">"dış": "true" ayarı bildirir Data Factory tablosu data factory dış ve veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="64fa7-570">“external”: “true” setting informs Data Factory that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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
<span data-ttu-id="64fa7-571">**Azure SQL çıktı veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="64fa7-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="64fa7-572">Kopya veri örneklemek için bir tablo bir Azure SQL veritabanında "MyTable" adlı.</span><span class="sxs-lookup"><span data-stu-id="64fa7-572">The sample copies data to a table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="64fa7-573">Blob CSV dosyasında içerecek şekilde beklediğiniz gibi Azure SQL veritabanınızda aynı sayıda sütuna sahip tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="64fa7-573">Create the table in your Azure SQL database with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="64fa7-574">Yeni satırlar tabloya saatte eklenir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-574">New rows are added to the table every hour.</span></span>

```json
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
<span data-ttu-id="64fa7-575">**Blob kaynağı ve SQL havuz sahip işlem hattı kopyalama etkinliğinde:**</span><span class="sxs-lookup"><span data-stu-id="64fa7-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="64fa7-576">Ardışık Düzen giriş ve çıkış veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-576">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="64fa7-577">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **BlobSource** ve **havuz** türü ayarlanmış **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-577">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
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
            "type": "BlobSource"
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
### <a name="json-example-copy-data-from-azure-sql-to-azure-blob"></a><span data-ttu-id="64fa7-578">JSON örnek: Verilerini Azure SQL Azure Blob</span><span class="sxs-lookup"><span data-stu-id="64fa7-578">JSON Example: Copy data from Azure SQL to Azure Blob</span></span>
<span data-ttu-id="64fa7-579">Aşağıdaki örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="64fa7-579">The following sample shows:</span></span>

1. <span data-ttu-id="64fa7-580">Bağlı hizmet türü [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="64fa7-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="64fa7-581">Bağlı hizmet türü [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="64fa7-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="64fa7-582">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="64fa7-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="64fa7-583">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="64fa7-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="64fa7-584">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) ve [BlobSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="64fa7-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="64fa7-585">Örnek zaman serisi veri bir Azure SQL tablosundan bir Azure blob saatlik kopyalar.</span><span class="sxs-lookup"><span data-stu-id="64fa7-585">The sample copies time-series data from an Azure SQL table to an Azure blob hourly.</span></span> <span data-ttu-id="64fa7-586">Bu örnekler kullanılan JSON özellikleri örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-586">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="64fa7-587">**Azure SQL bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="64fa7-587">**Azure SQL linked service:**</span></span>

```json
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
<span data-ttu-id="64fa7-588">**Azure Storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="64fa7-588">**Azure Storage linked service:**</span></span>

```json
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
<span data-ttu-id="64fa7-589">Azure Data Factory iki tür Azure Storage bağlı hizmeti destekler: **AzureStorage** ve **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="64fa7-590">İlk biri için hesap anahtarı içeren bağlantı dizesini belirtin ve daha sonra biri için paylaşılan erişim imzası (SAS) URI'sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="64fa7-590">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="64fa7-591">Bkz: [bağlı hizmetler](#linked-service-properties) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="64fa7-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="64fa7-592">**Azure SQL girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="64fa7-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="64fa7-593">Örnek, Azure SQL tablosu "MyTable" oluşturulur ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="64fa7-593">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="64fa7-594">"Dış" ayarı: "true" bildirir Data Factory hizmetinin tablo data factory dış ve veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="64fa7-594">Setting “external”: ”true” informs Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
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

<span data-ttu-id="64fa7-595">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="64fa7-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="64fa7-596">Veri her saat yeni bir bloba yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="64fa7-596">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="64fa7-597">Blob klasör yolu dinamik işlenmekte olan dilim başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-597">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="64fa7-598">Klasör yolu yıl, ay, gün ve saat bölümleri başlangıç saatini kullanır.</span><span class="sxs-lookup"><span data-stu-id="64fa7-598">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
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
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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

<span data-ttu-id="64fa7-599">**SQL kaynak ve Blob havuz sahip işlem hattı kopyalama etkinliğinde:**</span><span class="sxs-lookup"><span data-stu-id="64fa7-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="64fa7-600">Ardışık Düzen giriş ve çıkış veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="64fa7-600">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="64fa7-601">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **SqlSource** ve **havuz** türü ayarlanmış **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="64fa7-601">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="64fa7-602">SQL sorgusu için belirtilen **SqlReaderQuery** özelliği veri kopyalamak için son bir saat içindeki seçer.</span><span class="sxs-lookup"><span data-stu-id="64fa7-602">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```json
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

> [!NOTE]
> <span data-ttu-id="64fa7-603">Kaynak veri kümesi sütunlarından havuz kümesinden sütunlara eşlemek için bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="64fa7-603">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="64fa7-604">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="64fa7-604">Performance and Tuning</span></span>
<span data-ttu-id="64fa7-605">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve onu en iyi duruma getirmek için çeşitli yollar etkisi performansını anahtar Etkenler hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="64fa7-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
