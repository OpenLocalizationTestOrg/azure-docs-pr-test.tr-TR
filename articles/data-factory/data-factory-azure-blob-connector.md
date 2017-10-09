---
title: Azure Blob Storage/aaaCopy verileri | Microsoft Docs
description: "Nasıl toocopy blob Azure Data Factory veri öğrenin. Bizim örnek kullanın: nasıl toocopy veri tooand Azure Blob Storage ve Azure SQL veritabanı."
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
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="cc3a2-105">Azure Data Factory kullanarak Azure Blob depolama alanından veri tooor kopyalama</span><span class="sxs-lookup"><span data-stu-id="cc3a2-105">Copy data tooor from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="cc3a2-106">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toocopy veri tooand Azure Blob depolama biriminden de açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-106">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data tooand from Azure Blob Storage.</span></span> <span data-ttu-id="cc3a2-107">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="cc3a2-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="cc3a2-108">Overview</span></span>
<span data-ttu-id="cc3a2-109">Veri depolamak tooAzure Blob Storage veya Azure Blob Storage desteklenen tooany havuz verileri depolamak herhangi desteklenen bir kaynaktan veri kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-109">You can copy data from any supported source data store tooAzure Blob Storage or from Azure Blob Storage tooany supported sink data store.</span></span> <span data-ttu-id="cc3a2-110">Merhaba aşağıdaki tabloda kaynakları olarak desteklenen veri depoları listesini sağlar veya tarafından hello kopyalama etkinliği iç havuzlar.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-110">hello following table provides a list of data stores supported as sources or sinks by hello copy activity.</span></span> <span data-ttu-id="cc3a2-111">Örneğin, veri taşıyabilirsiniz **gelen** bir SQL Server veritabanı veya bir Azure SQL veritabanı **için** Azure blob depolama.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="cc3a2-112">Ve veri kopyalayabilirsiniz **gelen** Azure blob depolama **için** Azure SQL Data Warehouse veya bir Azure Cosmos DB koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="cc3a2-113">Desteklenen senaryolar</span><span class="sxs-lookup"><span data-stu-id="cc3a2-113">Supported scenarios</span></span>
<span data-ttu-id="cc3a2-114">Veri kopyalama **Azure Blob depolama biriminden** veri depolarına aşağıdaki toohello:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-114">You can copy data **from Azure Blob Storage** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="cc3a2-115">Veri depoları aşağıdaki hello verileri kopyalayabilirsiniz **tooAzure Blob Storage**:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-115">You can copy data from hello following data stores **tooAzure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="cc3a2-116">Kopyalama etkinliği destekleyen kopyalama verilerden / tooboth genel amaçlı Azure depolama hesapları ve sık erişimli/seyrek erişimli Blob Depolama.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-116">Copy Activity supports copying data from/tooboth general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="cc3a2-117">Merhaba etkinlik destekler **bloğundan okuma, ekleme veya sayfa blobları**, ancak destekleyen **tooonly blok blobları yazma**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-117">hello activity supports **reading from block, append, or page blobs**, but supports **writing tooonly block blobs**.</span></span> <span data-ttu-id="cc3a2-118">Sayfa blobları tarafından yedeklenen olduğundan azure Premium depolama havuzu olarak desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="cc3a2-119">Veri başarıyla olduğundan hello toohello hedef kopyalandıktan sonra kopyalama etkinliği hello kaynaktan verileri silmez.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-119">Copy Activity does not delete data from hello source after hello data is successfully copied toohello destination.</span></span> <span data-ttu-id="cc3a2-120">Sonra başarılı bir kopyasını toodelete kaynak verilere ihtiyacınız varsa oluşturma bir [özel etkinlik](data-factory-use-custom-activities.md) toodelete hello veri ve hello ardışık düzeninde hello etkinliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-120">If you need toodelete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) toodelete hello data and use hello activity in hello pipeline.</span></span> <span data-ttu-id="cc3a2-121">Merhaba bir örnek için bkz: [Delete blob veya klasör örneği github'daki](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-121">For an example, see hello [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="cc3a2-122">başlarken</span><span class="sxs-lookup"><span data-stu-id="cc3a2-122">Get started</span></span>
<span data-ttu-id="cc3a2-123">Farklı araçlar/API'lerini kullanarak verileri Azure Blob Storage/gruptan taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="cc3a2-124">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-124">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="cc3a2-125">Bu makalede sahip bir [izlenecek](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) bir Azure Blob Depolama konumu tooanother Azure Blob depolama konumunu bir ardışık düzen toocopy verileri oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline toocopy data from an Azure Blob Storage location  tooanother Azure Blob Storage location.</span></span> <span data-ttu-id="cc3a2-126">Ardışık Düzen toocopy veri bir Azure Blob Storage tooAzure SQL veritabanı oluşturma, Öğretici için bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-126">For a tutorial on creating a pipeline toocopy data from an Azure Blob Storage tooAzure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="cc3a2-127">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-127">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="cc3a2-128">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="cc3a2-129">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-129">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="cc3a2-130">Oluşturma bir **veri fabrikası**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-130">Create a **data factory**.</span></span> <span data-ttu-id="cc3a2-131">Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="cc3a2-132">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-132">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="cc3a2-133">Bir Azure blob depolama tooan Azure SQL veritabanından veri kopyalama, örneğin, iki bağlı hizmet toolink Azure depolama hesabınız ve Azure SQL veritabanı tooyour veri fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-133">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="cc3a2-134">Belirli tooAzure Blob Storage bağlı hizmeti özellikler için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-134">For linked service properties that are specific tooAzure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="cc3a2-135">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-135">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="cc3a2-136">Merhaba son adımda bahsedilen hello örnekte, bir veri kümesi toospecify hello blob kapsayıcısı ve hello giriş verisi içeren klasörü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-136">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="cc3a2-137">Ve hello blob depolama biriminden kopyalanan hello verilerini tutan hello Azure SQL veritabanında başka bir veri kümesi toospecify hello SQL tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-137">And, you create another dataset toospecify hello SQL table in hello Azure SQL database that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="cc3a2-138">Belirli tooAzure Blob Storage veri kümesi özellikler için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-138">For dataset properties that are specific tooAzure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="cc3a2-139">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="cc3a2-140">Daha önce bahsedilen hello örnekte BlobSource bir kaynak ve SqlSink havuzu olarak hello kopya etkinliği için kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-140">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="cc3a2-141">Azure SQL veritabanı tooAzure Blob Depolama kopyalıyorsanız benzer şekilde, SqlSource ve BlobSink hello kopyalama etkinliği kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-141">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="cc3a2-142">Belirli tooAzure Blob Storage kopyalama etkinliği özellikler için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-142">For copy activity properties that are specific tooAzure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="cc3a2-143">Nasıl toouse bir veri deposu bir kaynak veya bir havuz olarak hakkında daha fazla bilgi için veri deposu hello önceki bölümdeki hello bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-143">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="cc3a2-144">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-144">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="cc3a2-145">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="cc3a2-146">Kullanılan toocopy verileri Azure Blob Storage/Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-to-and-from-blob-storage  ) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-146">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="cc3a2-147">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooAzure Blob Storage JSON özellikleri hakkında ayrıntılı bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-147">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="cc3a2-148">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="cc3a2-148">Linked service properties</span></span>
<span data-ttu-id="cc3a2-149">İki tür vardır bağlı hizmetler Azure Storage tooan Azure data factory toolink kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-149">There are two types of linked services you can use toolink an Azure Storage tooan Azure data factory.</span></span> <span data-ttu-id="cc3a2-150">Bunlar: **AzureStorage** bağlantılı hizmeti ve **AzureStorageSas** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="cc3a2-151">Hello Azure Storage bağlı hizmeti hello data factory genel erişim toohello Azure Storage ile sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-151">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="cc3a2-152">Hello Azure depolama SAS (paylaşılan erişim imzası) bağlı ise hello data factory ile sınırlı/zaman sınırlı erişim toohello Azure depolama hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-152">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="cc3a2-153">Bu iki bağlı hizmet arasındaki herhangi bir fark vardır.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="cc3a2-154">Gereksinimlerinize uygun hello bağlı hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-154">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="cc3a2-155">Merhaba aşağıdaki bölümlerde daha fazla ayrıntı bu iki bağlı hizmet sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-155">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="cc3a2-156">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="cc3a2-156">Dataset properties</span></span>
<span data-ttu-id="cc3a2-157">toospecify dataset toorepresent giriş veya çıkış verileri Azure Blob Depolama hello türü özelliği için hello kümesinin ayarlayın: **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-157">toospecify a dataset toorepresent input or output data in an Azure Blob Storage, you set hello type property of hello dataset to: **AzureBlob**.</span></span> <span data-ttu-id="cc3a2-158">Set hello **linkedServiceName** özelliği hello dataset toohello adının hello Azure Storage veya Azure depolama SAS bağlantılı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-158">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="cc3a2-159">Merhaba kümesinin Hello türü özellikleri belirtin hello **blob kapsayıcısı** ve hello **klasörü** hello blob depolama.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-159">hello type properties of hello dataset specify hello **blob container** and hello **folder** in hello blob storage.</span></span>

<span data-ttu-id="cc3a2-160">Merhaba JSON bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-160">For a full list of JSON sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="cc3a2-161">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="cc3a2-162">Veri Fabrikası yapısındaki"" şema üzerinde okuma veri kaynakları için Azure blob gibi türü bilgileri sağlamak için temel CLS uyumlu .NET türü değerleri aşağıdaki hello destekler: Int16, Int32, Int64, tek, Double, Decimal, Byte [], Bool, dize, GUID, Datetime, Datetimeoffset, Timespan.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-162">Data factory supports hello following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="cc3a2-163">Veri Fabrikası otomatik olarak veri kaynağına veri dosyaları tooa havuz veri deposunu taşırken tür dönüşümleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-163">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span>

<span data-ttu-id="cc3a2-164">Merhaba **typeProperties** bölüm bilgileri sağlar ve her veri kümesi türü için farklı hello konumu hakkında hello veri hello veri deposundaki vb., biçimlendirme.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-164">hello **typeProperties** section is different for each type of dataset and provides information about hello location, format etc., of hello data in hello data store.</span></span> <span data-ttu-id="cc3a2-165">Merhaba typeProperties bölüm türü veri kümesi için **AzureBlob** veri kümesine hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-165">hello typeProperties section for dataset of type **AzureBlob** dataset has hello following properties:</span></span>

| <span data-ttu-id="cc3a2-166">Özellik</span><span class="sxs-lookup"><span data-stu-id="cc3a2-166">Property</span></span> | <span data-ttu-id="cc3a2-167">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc3a2-167">Description</span></span> | <span data-ttu-id="cc3a2-168">Gerekli</span><span class="sxs-lookup"><span data-stu-id="cc3a2-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc3a2-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="cc3a2-169">folderPath</span></span> |<span data-ttu-id="cc3a2-170">Yol toohello kapsayıcı ve klasöre hello blob depolama.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-170">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="cc3a2-171">Örnek: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="cc3a2-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="cc3a2-172">Evet</span><span class="sxs-lookup"><span data-stu-id="cc3a2-172">Yes</span></span> |
| <span data-ttu-id="cc3a2-173">fileName</span><span class="sxs-lookup"><span data-stu-id="cc3a2-173">fileName</span></span> |<span data-ttu-id="cc3a2-174">Merhaba blob adı.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-174">Name of hello blob.</span></span> <span data-ttu-id="cc3a2-175">isteğe bağlıdır ve büyük küçük harfe duyarlı dosya adıdır.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="cc3a2-176">Üzerinde bir dosya adı, hello (kopyalama dahil) etkinlik works belirtirseniz, belirli Blob hello.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-176">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="cc3a2-177">FileName belirtilmediğinde kopyalama tüm BLOB'lar girdi veri kümesi için hello folderPath içerir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-177">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="cc3a2-178">Zaman **fileName** bir çıkış veri kümesi için belirtilmemiş ve **preserveHierarchy** belirtilmedi etkinlik havuzunda oluşturulan hello dosyasının hello adı, bu biçim aşağıdaki hello olacaktır: veri.<Guid>. txt (örneğin:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="cc3a2-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="cc3a2-179">Hayır</span><span class="sxs-lookup"><span data-stu-id="cc3a2-179">No</span></span> |
| <span data-ttu-id="cc3a2-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="cc3a2-180">partitionedBy</span></span> |<span data-ttu-id="cc3a2-181">partitionedBy isteğe bağlı bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="cc3a2-182">Bunu toospecify dinamik folderPath ve dosya adı için zaman serisi veri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-182">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="cc3a2-183">Örneğin, folderPath için verileri saatte parametreli olabilir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="cc3a2-184">Merhaba bkz [partitionedBy özellik bölümünü kullanarak](#using-partitionedBy-property) ayrıntı ve örnekler için.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-184">See hello [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="cc3a2-185">Hayır</span><span class="sxs-lookup"><span data-stu-id="cc3a2-185">No</span></span> |
| <span data-ttu-id="cc3a2-186">Biçimi</span><span class="sxs-lookup"><span data-stu-id="cc3a2-186">format</span></span> | <span data-ttu-id="cc3a2-187">şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-187">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="cc3a2-188">Set hello **türü** biçimi tooone şu değerlerden biri altında özellik.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-188">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="cc3a2-189">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="cc3a2-190">Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-190">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="cc3a2-191">Hayır</span><span class="sxs-lookup"><span data-stu-id="cc3a2-191">No</span></span> |
| <span data-ttu-id="cc3a2-192">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="cc3a2-192">compression</span></span> | <span data-ttu-id="cc3a2-193">Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-193">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="cc3a2-194">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="cc3a2-195">Desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="cc3a2-196">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="cc3a2-197">Hayır</span><span class="sxs-lookup"><span data-stu-id="cc3a2-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="cc3a2-198">PartitionedBy özelliğini kullanma</span><span class="sxs-lookup"><span data-stu-id="cc3a2-198">Using partitionedBy property</span></span>
<span data-ttu-id="cc3a2-199">Merhaba önceki bölümünde belirtildiği gibi bir dinamik folderPath ve zaman serisi verileri için dosya adı ile Merhaba belirtebilirsiniz **partitionedBy** özelliği, [Data Factory işlevler ve hello sistem değişkenleri](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-199">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="cc3a2-200">Zaman serisi veri kümeleri, zamanlama ve dilimleri hakkında daha fazla bilgi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) ve [zamanlama ve yürütme](data-factory-scheduling-and-execution.md) makaleleri.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="cc3a2-201">Örnek 1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="cc3a2-202">Bu örnekte, {dilim} belirtilen hello Data Factory sistem değişkenin değerini SliceStart hello biçiminde (YYYYMMDDHH) ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-202">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="cc3a2-203">Merhaba SliceStart hello dilim toostart süresini ifade eder.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-203">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="cc3a2-204">Merhaba folderPath her dilim için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-204">hello folderPath is different for each slice.</span></span> <span data-ttu-id="cc3a2-205">Örneğin: wikidatagateway/wikisampledataout/2014100103 veya wikidatagateway/wikisampledataout/2014100104</span><span class="sxs-lookup"><span data-stu-id="cc3a2-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="cc3a2-206">Örnek 2</span><span class="sxs-lookup"><span data-stu-id="cc3a2-206">Sample 2</span></span>

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

<span data-ttu-id="cc3a2-207">Bu örnekte, folderPath ve fileName özellikleri tarafından kullanılan ayrı değişkenleri içine yıl, ay, gün ve saat SliceStart ayıklanır.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="cc3a2-208">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="cc3a2-208">Copy activity properties</span></span>
<span data-ttu-id="cc3a2-209">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-209">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="cc3a2-210">Ad, açıklama, giriş ve çıkış veri kümeleri ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="cc3a2-211">Oysa hello kullanılabilen özellikleri **typeProperties** hello etkinlik bölümünü her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-211">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="cc3a2-212">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-212">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="cc3a2-213">Bir Azure Blob depolama alanından veri taşıyorsanız, hello kaynak türü hello kopyalama etkinliği çok ayarladığınız**BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-213">If you are moving data from an Azure Blob Storage, you set hello source type in hello copy activity too**BlobSource**.</span></span> <span data-ttu-id="cc3a2-214">Veri tooan Azure Blob Storage taşıyorsanız, benzer şekilde, hello Havuz türü hello kopyalama etkinliği çok ayarladığınız**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-214">Similarly, if you are moving data tooan Azure Blob Storage, you set hello sink type in hello copy activity too**BlobSink**.</span></span> <span data-ttu-id="cc3a2-215">Bu bölümde BlobSource ve BlobSink tarafından desteklenen özellikler listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="cc3a2-216">**BlobSource** hello özelliklerinde aşağıdaki hello destekleyen **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-216">**BlobSource** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="cc3a2-217">Özellik</span><span class="sxs-lookup"><span data-stu-id="cc3a2-217">Property</span></span> | <span data-ttu-id="cc3a2-218">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc3a2-218">Description</span></span> | <span data-ttu-id="cc3a2-219">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="cc3a2-219">Allowed values</span></span> | <span data-ttu-id="cc3a2-220">Gerekli</span><span class="sxs-lookup"><span data-stu-id="cc3a2-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cc3a2-221">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="cc3a2-221">recursive</span></span> |<span data-ttu-id="cc3a2-222">Merhaba alt klasörler veya yalnızca hello belirtilen klasör Hello veri yinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-222">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="cc3a2-223">(Varsayılan değer) false değerini true</span><span class="sxs-lookup"><span data-stu-id="cc3a2-223">True (default value), False</span></span> |<span data-ttu-id="cc3a2-224">Hayır</span><span class="sxs-lookup"><span data-stu-id="cc3a2-224">No</span></span> |

<span data-ttu-id="cc3a2-225">**BlobSink** aşağıdaki özelliklere hello destekleyen **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-225">**BlobSink** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="cc3a2-226">Özellik</span><span class="sxs-lookup"><span data-stu-id="cc3a2-226">Property</span></span> | <span data-ttu-id="cc3a2-227">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc3a2-227">Description</span></span> | <span data-ttu-id="cc3a2-228">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="cc3a2-228">Allowed values</span></span> | <span data-ttu-id="cc3a2-229">Gerekli</span><span class="sxs-lookup"><span data-stu-id="cc3a2-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cc3a2-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="cc3a2-230">copyBehavior</span></span> |<span data-ttu-id="cc3a2-231">Merhaba kaynağı BlobSource veya dosya sistemi olduğunda hello kopyalama davranışını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-231">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="cc3a2-232"><b>PreserveHierarchy</b>: korur hello hello hedef klasörü içinde dosya hiyerarşisi.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-232"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="cc3a2-233">Kaynak dosya toosource klasörünün göreli yolu Hello aynı toohello göreli hedef dosya tootarget klasör yoludur.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-233">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="cc3a2-234"><b>FlattenHierarchy</b>: hello kaynak klasördeki tüm dosyaları hello ilk hedef klasörü düzeyi.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-234"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="cc3a2-235">Merhaba hedef dosyalara otomatik adına sahip.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-235">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="cc3a2-236"><b>MergeFiles</b>: hello kaynak klasör tooone dosyasından tüm dosyaları birleştirir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-236"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="cc3a2-237">Merhaba dosya/Blob adı belirtilirse, hello birleştirilmiş dosya adı hello belirtilen adı olur; Aksi takdirde otomatik olarak oluşturulan dosya adı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-237">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="cc3a2-238">Hayır</span><span class="sxs-lookup"><span data-stu-id="cc3a2-238">No</span></span> |

<span data-ttu-id="cc3a2-239">**BlobSource** geriye dönük uyumluluk için bu iki özellik de destekler.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="cc3a2-240">**treatEmptyAsNull**: belirtir olup olmadığını tootreat null veya boş dize olarak null değer.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-240">**treatEmptyAsNull**: Specifies whether tootreat null or empty string as null value.</span></span>
* <span data-ttu-id="cc3a2-241">**skipHeaderLineCount** -kaç satır atlandı belirtir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="cc3a2-242">Yalnızca girdi veri kümesi TextFormat kullandığında geçerli olduğu.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="cc3a2-243">Benzer şekilde, **BlobSink** özelliği geriye dönük uyumluluk için aşağıdaki hello destekler.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-243">Similarly, **BlobSink** supports hello following property for backward compatibility.</span></span>

* <span data-ttu-id="cc3a2-244">**blobWriterAddHeader**: tooadd tooan yazılırken sütun tanımları üstbilgisinin veri kümesini çıktı olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-244">**blobWriterAddHeader**: Specifies whether tooadd a header of column definitions while writing tooan output dataset.</span></span>

<span data-ttu-id="cc3a2-245">Veri kümeleri şimdi destek hello aşağıdaki uygulamak özelliklere hello aynı işlevselliği: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-245">Datasets now support hello following properties that implement hello same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="cc3a2-246">Merhaba aşağıdaki tabloda bu blob kaynak/havuz özellikleri yerine hello yeni veri kümesi özellikleri kullanma hakkında yönergeler sunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-246">hello following table provides guidance on using hello new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="cc3a2-247">Kopya etkinliği özelliği</span><span class="sxs-lookup"><span data-stu-id="cc3a2-247">Copy Activity property</span></span> | <span data-ttu-id="cc3a2-248">Veri kümesi özelliği</span><span class="sxs-lookup"><span data-stu-id="cc3a2-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="cc3a2-249">BlobSource üzerinde skipHeaderLineCount</span><span class="sxs-lookup"><span data-stu-id="cc3a2-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="cc3a2-250">skipLineCount ve firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="cc3a2-251">Satırlar ilk atlanır ve hello ilk satırın üstbilgi olarak sonra okuyun.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-251">Lines are skipped first and then hello first row is read as a header.</span></span> |
| <span data-ttu-id="cc3a2-252">BlobSource üzerinde treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="cc3a2-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="cc3a2-253">girdi veri kümesi üzerinde treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="cc3a2-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="cc3a2-254">BlobSink üzerinde blobWriterAddHeader</span><span class="sxs-lookup"><span data-stu-id="cc3a2-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="cc3a2-255">Çıktı veri kümesi üzerinde firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="cc3a2-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="cc3a2-256">Bkz: [belirtme TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) bu özellikleri hakkında ayrıntılı bilgi için bölüm.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="cc3a2-257">özyinelemeli ve copyBehavior örnekleri</span><span class="sxs-lookup"><span data-stu-id="cc3a2-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="cc3a2-258">Bu bölümde hello kopyalama işlemi farklı bir özyinelemeli ve copyBehavior değerleri kombinasyonu için sonuçta elde edilen davranışını hello açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-258">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="cc3a2-259">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="cc3a2-259">recursive</span></span> | <span data-ttu-id="cc3a2-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="cc3a2-260">copyBehavior</span></span> | <span data-ttu-id="cc3a2-261">Bunun sonucunda oluşan davranışı</span><span class="sxs-lookup"><span data-stu-id="cc3a2-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc3a2-262">TRUE</span><span class="sxs-lookup"><span data-stu-id="cc3a2-262">true</span></span> |<span data-ttu-id="cc3a2-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="cc3a2-263">preserveHierarchy</span></span> |<span data-ttu-id="cc3a2-264">Bir kaynak klasörü için Klasör1 yapı izlenerek hello ile:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-264">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="cc3a2-265">Klasör1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-265">Folder1</span></span><br/><span data-ttu-id="cc3a2-266">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="cc3a2-267">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="cc3a2-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="cc3a2-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="cc3a2-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="cc3a2-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="cc3a2-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="cc3a2-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="cc3a2-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="cc3a2-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="cc3a2-272">Merhaba hedef klasör Klasör1 aynı hello kaynağı olarak yapısı hello oluşturulur</span><span class="sxs-lookup"><span data-stu-id="cc3a2-272">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="cc3a2-273">Klasör1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-273">Folder1</span></span><br/><span data-ttu-id="cc3a2-274">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="cc3a2-275">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="cc3a2-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="cc3a2-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="cc3a2-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="cc3a2-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="cc3a2-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="cc3a2-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="cc3a2-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="cc3a2-280">TRUE</span><span class="sxs-lookup"><span data-stu-id="cc3a2-280">true</span></span> |<span data-ttu-id="cc3a2-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="cc3a2-281">flattenHierarchy</span></span> |<span data-ttu-id="cc3a2-282">Bir kaynak klasörü için Klasör1 yapı izlenerek hello ile:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-282">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="cc3a2-283">Klasör1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-283">Folder1</span></span><br/><span data-ttu-id="cc3a2-284">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="cc3a2-285">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="cc3a2-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="cc3a2-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="cc3a2-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="cc3a2-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="cc3a2-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="cc3a2-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="cc3a2-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="cc3a2-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="cc3a2-290">Merhaba hedef Klasör1 yapı izlenerek hello ile oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-290">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="cc3a2-291">Klasör1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-291">Folder1</span></span><br/><span data-ttu-id="cc3a2-292">&nbsp;&nbsp;&nbsp;&nbsp;dosya1 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="cc3a2-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="cc3a2-293">&nbsp;&nbsp;&nbsp;&nbsp;dosya2 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="cc3a2-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="cc3a2-294">&nbsp;&nbsp;&nbsp;&nbsp;dosya3 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="cc3a2-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="cc3a2-295">&nbsp;&nbsp;&nbsp;&nbsp;File4 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="cc3a2-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="cc3a2-296">&nbsp;&nbsp;&nbsp;&nbsp;File5 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="cc3a2-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="cc3a2-297">TRUE</span><span class="sxs-lookup"><span data-stu-id="cc3a2-297">true</span></span> |<span data-ttu-id="cc3a2-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="cc3a2-298">mergeFiles</span></span> |<span data-ttu-id="cc3a2-299">Bir kaynak klasörü için Klasör1 yapı izlenerek hello ile:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-299">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="cc3a2-300">Klasör1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-300">Folder1</span></span><br/><span data-ttu-id="cc3a2-301">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="cc3a2-302">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="cc3a2-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="cc3a2-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="cc3a2-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="cc3a2-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="cc3a2-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="cc3a2-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="cc3a2-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="cc3a2-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="cc3a2-307">Merhaba hedef Klasör1 yapı izlenerek hello ile oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="cc3a2-308">Klasör1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-308">Folder1</span></span><br/><span data-ttu-id="cc3a2-309">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1 + dosya2 + dosya3 + File4 + 5 dosyası içeriği otomatik olarak oluşturulan dosya adında bir dosya halinde birleştirilir</span><span class="sxs-lookup"><span data-stu-id="cc3a2-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="cc3a2-310">False</span><span class="sxs-lookup"><span data-stu-id="cc3a2-310">false</span></span> |<span data-ttu-id="cc3a2-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="cc3a2-311">preserveHierarchy</span></span> |<span data-ttu-id="cc3a2-312">Bir kaynak klasörü için Klasör1 yapı izlenerek hello ile:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-312">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="cc3a2-313">Klasör1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-313">Folder1</span></span><br/><span data-ttu-id="cc3a2-314">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="cc3a2-315">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="cc3a2-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="cc3a2-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="cc3a2-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="cc3a2-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="cc3a2-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="cc3a2-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="cc3a2-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="cc3a2-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="cc3a2-320">Merhaba hedef klasör Klasör1 yapı izlenerek hello ile oluşturulur</span><span class="sxs-lookup"><span data-stu-id="cc3a2-320">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="cc3a2-321">Klasör1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-321">Folder1</span></span><br/><span data-ttu-id="cc3a2-322">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="cc3a2-323">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="cc3a2-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="cc3a2-324">Dosya3, File4 ve File5 Subfolder1 değil toplanma.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="cc3a2-325">False</span><span class="sxs-lookup"><span data-stu-id="cc3a2-325">false</span></span> |<span data-ttu-id="cc3a2-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="cc3a2-326">flattenHierarchy</span></span> |<span data-ttu-id="cc3a2-327">Bir kaynak klasörü için Klasör1 yapı izlenerek hello ile:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-327">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="cc3a2-328">Klasör1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-328">Folder1</span></span><br/><span data-ttu-id="cc3a2-329">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="cc3a2-330">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="cc3a2-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="cc3a2-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="cc3a2-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="cc3a2-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="cc3a2-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="cc3a2-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="cc3a2-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="cc3a2-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="cc3a2-335">Merhaba hedef klasör Klasör1 yapı izlenerek hello ile oluşturulur</span><span class="sxs-lookup"><span data-stu-id="cc3a2-335">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="cc3a2-336">Klasör1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-336">Folder1</span></span><br/><span data-ttu-id="cc3a2-337">&nbsp;&nbsp;&nbsp;&nbsp;dosya1 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="cc3a2-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="cc3a2-338">&nbsp;&nbsp;&nbsp;&nbsp;dosya2 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="cc3a2-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="cc3a2-339">Dosya3, File4 ve File5 Subfolder1 değil toplanma.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="cc3a2-340">False</span><span class="sxs-lookup"><span data-stu-id="cc3a2-340">false</span></span> |<span data-ttu-id="cc3a2-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="cc3a2-341">mergeFiles</span></span> |<span data-ttu-id="cc3a2-342">Bir kaynak klasörü için Klasör1 yapı izlenerek hello ile:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-342">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="cc3a2-343">Klasör1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-343">Folder1</span></span><br/><span data-ttu-id="cc3a2-344">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="cc3a2-345">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="cc3a2-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="cc3a2-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="cc3a2-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="cc3a2-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="cc3a2-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="cc3a2-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="cc3a2-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="cc3a2-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="cc3a2-350">Merhaba hedef klasör Klasör1 yapı izlenerek hello ile oluşturulur</span><span class="sxs-lookup"><span data-stu-id="cc3a2-350">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="cc3a2-351">Klasör1</span><span class="sxs-lookup"><span data-stu-id="cc3a2-351">Folder1</span></span><br/><span data-ttu-id="cc3a2-352">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1 + dosya2 içeriği otomatik olarak oluşturulan dosya adında bir dosya halinde birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="cc3a2-353">dosya1 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="cc3a2-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="cc3a2-354">Dosya3, File4 ve File5 Subfolder1 değil toplanma.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a><span data-ttu-id="cc3a2-355">İzlenecek yol: Kopyalama Sihirbazı'nı kullan toocopy veri/Blob depolama biriminden</span><span class="sxs-lookup"><span data-stu-id="cc3a2-355">Walkthrough: Use Copy Wizard toocopy data to/from Blob Storage</span></span>
<span data-ttu-id="cc3a2-356">Nasıl tooquickly kopya verileri için/Azure blob depolama konumunda bakalım.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-356">Let's look at how tooquickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="cc3a2-357">Bu kılavuzda, hem kaynak hem de hedef veri türünü depolar: Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="cc3a2-358">Merhaba ardışık düzen bu kılavuzda veri bir tooanother klasörü hello kopyalar aynı blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-358">hello pipeline in this walkthrough copies data from a folder tooanother folder in hello same blob container.</span></span> <span data-ttu-id="cc3a2-359">Bu kılavuzda kasıtlı olarak basit tooshow olan ayarları veya Blob Depolama kaynağı veya havuz olarak kullanırken özellikleri.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-359">This walkthrough is intentionally simple tooshow you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="cc3a2-360">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cc3a2-360">Prerequisites</span></span>
1. <span data-ttu-id="cc3a2-361">Bir genel amaçlı oluşturma **Azure depolama hesabı** zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="cc3a2-362">Her iki biçimde hello blob storage kullanma **kaynak** ve **hedef** verileri depolamak bu kılavuzda.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-362">You use hello blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="cc3a2-363">bir Azure depolama hesabınız yoksa, hello bkz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) adımları toocreate bir makale.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-363">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
2. <span data-ttu-id="cc3a2-364">Adlı bir blob kapsayıcı oluşturun **adfblobconnector** hello depolama hesabındaki.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-364">Create a blob container named **adfblobconnector** in hello storage account.</span></span> 
4. <span data-ttu-id="cc3a2-365">Adlı bir klasör oluşturun **giriş** hello içinde **adfblobconnector** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-365">Create a folder named **input** in hello **adfblobconnector** container.</span></span>
5. <span data-ttu-id="cc3a2-366">Adlı bir dosya oluşturun **emp.txt** aşağıdaki hello ile içerik ve toohello karşıya **giriş** gibi araçları kullanarak klasör [Azure Storage Gezgini](https://azurestorageexplorer.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="cc3a2-366">Create a file named **emp.txt** with hello following content and upload it toohello **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a><span data-ttu-id="cc3a2-367">Merhaba veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="cc3a2-367">Create hello data factory</span></span>
1. <span data-ttu-id="cc3a2-368">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-368">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cc3a2-369">Tıklatın **+ yeni** hello sol üst köşeden tıklatın **Intelligence + analiz**, tıklatıp **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-369">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="cc3a2-370">Merhaba, **yeni data factory** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-370">In hello **New data factory** blade:</span></span>   
    1. <span data-ttu-id="cc3a2-371">Girin **ADFBlobConnectorDF** hello için **adı**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-371">Enter **ADFBlobConnectorDF** for hello **name**.</span></span> <span data-ttu-id="cc3a2-372">Merhaba hello Azure veri fabrikasının adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-372">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="cc3a2-373">Merhaba hatayı alırsanız: `*Data factory name “ADFBlobConnectorDF” is not available`, hello veri fabrikası (örneğin, yournameADFBlobConnectorDF) hello adını değiştirin ve oluşturmayı yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-373">If you receive hello error: `*Data factory name “ADFBlobConnectorDF” is not available`, change hello name of hello data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="cc3a2-374">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="cc3a2-375">Azure **aboneliğinizi** seçin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="cc3a2-376">Kaynak grubu için seçin **kullanım varolan** tooselect bir var olan kaynak grubunu (veya) seçin **Yeni Oluştur** tooenter bir kaynak grubu için bir ad.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-376">For Resource Group, select **Use existing** tooselect an existing resource group (or) select **Create new** tooenter a name for a resource group.</span></span>
    4. <span data-ttu-id="cc3a2-377">Seçin bir **konumu** hello veri fabrikası için.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-377">Select a **location** for hello data factory.</span></span>
    5. <span data-ttu-id="cc3a2-378">Seçin **PIN toodashboard** hello dikey penceresinde hello altındaki onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-378">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>
    6. <span data-ttu-id="cc3a2-379">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-379">Click **Create**.</span></span>
3. <span data-ttu-id="cc3a2-380">Merhaba oluşturma işlemi tamamlandıktan sonra hello bkz **Data Factory** hello görüntü aşağıdaki gösterildiği gibi dikey: ![Data factory giriş sayfası](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="cc3a2-380">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="cc3a2-381">Kopyalama Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="cc3a2-381">Copy Wizard</span></span>
1. <span data-ttu-id="cc3a2-382">Merhaba Hello Data Factory giriş sayfasında, tıklatın **kopyalama [Önizleme] verileri** toolaunch döşeme **kopyalama veri Sihirbazı** ayrı bir sekmede.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-382">On hello Data Factory home page, click hello **Copy data [PREVIEW]** tile toolaunch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="cc3a2-383">Bu hello web tarayıcısının "Yetkilendiriliyor..." takılmış görürseniz, devre dışı bırakın/işaretini kaldırın **üçüncü taraf tanımlama bilgilerini engelleyebilir ve site verileri** ayarlama (veya) etkin ve oluşturmak için bir özel durum **login.microsoftonline.com**ve hello Sihirbazı yeniden başlatmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-383">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
2. <span data-ttu-id="cc3a2-384">Merhaba, **özellikleri** sayfa:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-384">In hello **Properties** page:</span></span>
    1. <span data-ttu-id="cc3a2-385">Girin **CopyPipeline** için **görev adı**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="cc3a2-386">Merhaba görev adı, veri fabrikasında ardışık düzeni hello hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-386">hello task name is hello name of hello pipeline in your data factory.</span></span>
    2. <span data-ttu-id="cc3a2-387">Girin bir **açıklama** hello görevin (isteğe bağlı).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-387">Enter a **description** for hello task (optional).</span></span>
    3. <span data-ttu-id="cc3a2-388">İçin **görev tempoyla veya görev zamanlama**, hello tutmak **düzenli olarak zamanında** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-388">For **Task cadence or Task schedule**, keep hello **Run regularly on schedule** option.</span></span> <span data-ttu-id="cc3a2-389">Bu görevi yalnızca bir kez yerine çalıştırmak sürekli bir zamanlamaya göre toorun istiyorsanız seçin **kez Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-389">If you want toorun this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="cc3a2-390">Öğesini seçerseniz, **kez Şimdi Çalıştır** seçeneği, bir [tek seferlik ardışık düzen](data-factory-create-pipelines.md#onetime-pipeline) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="cc3a2-391">Hello ayarlarını koruyabilirsiniz **yinelenen desen**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-391">Keep hello settings for **Recurring pattern**.</span></span> <span data-ttu-id="cc3a2-392">Her gün çalışır hello arasında başlangıç ve bitiş, bu görev hello sonraki adımda belirtin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-392">This task runs daily between hello start and end times you specify in hello next step.</span></span>
    5. <span data-ttu-id="cc3a2-393">Değişiklik hello **başlangıç tarihi ve saati** çok**21/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-393">Change hello **Start date time** too**04/21/2017**.</span></span> 
    6. <span data-ttu-id="cc3a2-394">Değişiklik hello **bitiş tarihi ve saati** çok**25/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-394">Change hello **End date time** too**04/25/2017**.</span></span> <span data-ttu-id="cc3a2-395">Merhaba takvimi aracılığıyla gözatma yerine tootype hello tarih isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-395">You may want tootype hello date instead of browsing through hello calendar.</span></span>     
    8. <span data-ttu-id="cc3a2-396">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-396">Click **Next**.</span></span>
      <span data-ttu-id="cc3a2-397">![Kopyalama aracı - Özellikler sayfası](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="cc3a2-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="cc3a2-398">Merhaba üzerinde **kaynak veri deposu** sayfasında, **Azure Blob Storage** döşeme.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-398">On hello **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="cc3a2-399">Bu sayfa toospecify hello kaynak veri deposu hello kopyalama görevi için kullanın.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-399">You use this page toospecify hello source data store for hello copy task.</span></span> <span data-ttu-id="cc3a2-400">Yeni bir veri deposu belirtmek için mevcut bir veri deposu bağlı hizmetini kullanabilirsiniz (veya) yeni bir veri deposu belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="cc3a2-401">var olan toouse bağlantılı hizmeti, seçtiğiniz **mevcut bağlı hizmetlerden** ve hello doğru bağlı hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-401">toouse an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select hello right linked service.</span></span> 
    <span data-ttu-id="cc3a2-402">![Kopyalama aracı - kaynak veri deposu sayfası](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="cc3a2-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="cc3a2-403">Merhaba üzerinde **hello Azure Blob Depolama hesabı belirtin** sayfa:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-403">On hello **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="cc3a2-404">İçin Hello otomatik olarak oluşturulan adı bırakın **bağlantı adı**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-404">Keep hello auto-generated name for **Connection name**.</span></span> <span data-ttu-id="cc3a2-405">Merhaba bağlantı adı adıdır hello hello bağlantılı hizmet türü: Azure depolama.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-405">hello connection name is hello name of hello linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="cc3a2-406">**Hesap seçme yöntemi** için **Azure aboneliklerinden** seçeneğinin belirlendiğini onaylayın.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="cc3a2-407">Azure aboneliğinizi seçin ya da koruma **Tümünü Seç** için **Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="cc3a2-408">Seçin bir **Azure depolama hesabı** hello hesaplarına Azure depolama listesi hello seçili abonelikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-408">Select an **Azure storage account** from hello list of Azure storage accounts available in hello selected subscription.</span></span> <span data-ttu-id="cc3a2-409">Ayrıca tooenter depolama hesabı ayarlarını el ile seçerek seçebilirsiniz **el ile girmeniz** hello seçeneği **hesap seçme yöntemi**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-409">You can also choose tooenter storage account settings manually by selecting **Enter manually** option for hello **Account selection method**.</span></span>
   5. <span data-ttu-id="cc3a2-410">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-410">Click **Next**.</span></span> 
      <span data-ttu-id="cc3a2-411">![Kopyalama aracı - hello Azure Blob Depolama hesabı belirtin](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="cc3a2-411">![Copy Tool - Specify hello Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="cc3a2-412">Üzerinde **Seç hello girdi dosyası veya klasörü** sayfa:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-412">On **Choose hello input file or folder** page:</span></span>
   1. <span data-ttu-id="cc3a2-413">Çift **adfblobcontainer**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="cc3a2-414">Seçin **giriş**, tıklatıp **Seç**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="cc3a2-415">Bu kılavuzda, hello giriş klasörü seçin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-415">In this walkthrough, you select hello input folder.</span></span> <span data-ttu-id="cc3a2-416">Merhaba emp.txt dosya hello klasöründe bunun yerine seçeneğini de.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-416">You could also select hello emp.txt file in hello folder instead.</span></span> 
      <span data-ttu-id="cc3a2-417">![Kopyalama aracı - hello girdi dosyası veya klasörü seçin](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="cc3a2-417">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="cc3a2-418">Merhaba üzerinde **Seç hello girdi dosyası veya klasörü** sayfa:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-418">On hello **Choose hello input file or folder** page:</span></span>
    1. <span data-ttu-id="cc3a2-419">Bu hello onaylayın **dosya veya klasör** çok ayarlanır**adfblobconnector/giriş**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-419">Confirm that hello **file or folder** is set too**adfblobconnector/input**.</span></span> <span data-ttu-id="cc3a2-420">Merhaba dosyaları alt klasörlerde, örneğin, 04/2017/01, 04/2017/02 ve vb. adfblobconnector/giriş girin / {year} / {month} / {day} dosya veya klasör için.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-420">If hello files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="cc3a2-421">Merhaba metin kutusu dışında SEKME tuşuna bastığınızda (yyyy) yıl, ay (MM) ve gün (dd) için üç açılan listeleri tooselect biçimleri bakın.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-421">When you press TAB out of hello text box, you see three drop-down lists tooselect formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="cc3a2-422">Ayarlamayın **kopyalayın dosyayı yinelemeli olarak**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="cc3a2-423">Bu seçenek toorecursively çapraz dosyaları toobe kopyalanan toohello hedefine klasörlerde seçin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-423">Select this option toorecursively traverse through folders for files toobe copied toohello destination.</span></span> 
    3. <span data-ttu-id="cc3a2-424">Değil hello **ikili kopyalama** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-424">Do not hello **binary copy** option.</span></span> <span data-ttu-id="cc3a2-425">Bu seçenek tooperform kaynak dosya toohello hedef ikili bir kopyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-425">Select this option tooperform a binary copy of source file toohello destination.</span></span> <span data-ttu-id="cc3a2-426">Daha fazla seçenek hello sonraki sayfalarda görebilmeniz için bu kılavuzda seçmeyin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-426">Do not select for this walkthrough so that you can see more options in hello next pages.</span></span> 
    4. <span data-ttu-id="cc3a2-427">Bu hello onaylayın **sıkıştırma türünü** çok ayarlanır**hiçbiri**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-427">Confirm that hello **Compression type** is set too**None**.</span></span> <span data-ttu-id="cc3a2-428">Kaynak dosyalar hello desteklenen biçimlerden birinde sıkıştırılmış bu seçenek için bir değer seçin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-428">Select a value for this option if your source files are compressed in one of hello supported formats.</span></span> 
    5. <span data-ttu-id="cc3a2-429">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-429">Click **Next**.</span></span>
    <span data-ttu-id="cc3a2-430">![Kopyalama aracı - hello girdi dosyası veya klasörü seçin](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="cc3a2-430">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="cc3a2-431">Merhaba üzerinde **dosya biçimi ayarları** sayfasında, gördüğünüz hello sınırlayıcıları ve hello dosyası ayrıştırılırken hello Sihirbazı tarafından otomatik olarak algılanır hello şema.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-431">On hello **File format settings** page, you see hello delimiters and hello schema that is auto-detected by hello wizard by parsing hello file.</span></span> 
    1. <span data-ttu-id="cc3a2-432">Seçenekler aşağıdaki hello onaylayın: bir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-432">Confirm hello following options: a.</span></span> <span data-ttu-id="cc3a2-433">Merhaba **dosya biçimi** çok ayarlanır**metin biçimi**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-433">hello **file format** is set too**Text format**.</span></span> <span data-ttu-id="cc3a2-434">Tüm desteklenen hello biçimleri hello aşağı açılan listesinde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-434">You can see all hello supported formats in hello drop-down list.</span></span> <span data-ttu-id="cc3a2-435">Örneğin: JSON, Avro, ORC, Parquet.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="cc3a2-436">b.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-436">b.</span></span> <span data-ttu-id="cc3a2-437">Merhaba **sütun sınırlayıcı** çok ayarlanır`Comma (,)`.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-437">hello **column delimiter** is set too`Comma (,)`.</span></span> <span data-ttu-id="cc3a2-438">Gördüğünüz hello aşağı açılan listesinde Data Factory ile desteklenen diğer sütun sınırlayıcıları hello.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-438">You can see hello other column delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="cc3a2-439">Özel bir sınırlayıcı de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="cc3a2-440">c.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-440">c.</span></span> <span data-ttu-id="cc3a2-441">Merhaba **satır ayırıcı** çok ayarlanır`Carriage Return + Line feed (\r\n)`.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-441">hello **row delimiter** is set too`Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="cc3a2-442">Gördüğünüz hello aşağı açılan listesinde Data Factory ile desteklenen diğer satır sınırlayıcıları hello.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-442">You can see hello other row delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="cc3a2-443">Özel bir sınırlayıcı de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="cc3a2-444">d.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-444">d.</span></span> <span data-ttu-id="cc3a2-445">Merhaba **satır sayısı atla** çok ayarlanır**0**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-445">hello **skip line count** is set too**0**.</span></span> <span data-ttu-id="cc3a2-446">Merhaba dosya hello üstünde atlandı birkaç satırları toobe istiyorsanız hello numarasını buraya girin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-446">If you want a few lines toobe skipped at hello top of hello file, enter hello number here.</span></span>
        <span data-ttu-id="cc3a2-447">e.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-447">e.</span></span>  <span data-ttu-id="cc3a2-448">Merhaba **ilk veri satırı sütun adları içeren** ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-448">hello **first data row contains column names** is not set.</span></span> <span data-ttu-id="cc3a2-449">Merhaba ilk satırı sütun adları Hello kaynak dosyaları içeriyorsa, bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-449">If hello source files contain column names in hello first row, select this option.</span></span>
        <span data-ttu-id="cc3a2-450">f.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-450">f.</span></span> <span data-ttu-id="cc3a2-451">Merhaba **boş sütun değeri null olarak davran** seçeneği ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-451">hello **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="cc3a2-452">Genişletme **Gelişmiş ayarları** toosee Gelişmiş seçeneği kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-452">Expand **Advanced settings** toosee advanced option available.</span></span>
    3. <span data-ttu-id="cc3a2-453">Merhaba sayfasının Hello altında hello bkz **Önizleme** hello emp.txt dosya verileri.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-453">At hello bottom of hello page, see hello **preview** of data from hello emp.txt file.</span></span>
    4. <span data-ttu-id="cc3a2-454">Tıklatın **şema** hello kaynak dosyasında hello veri bakarak çıkarımı yapılan bu hello Kopyalama Sihirbazı hello alt toosee hello şema sekmesi.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-454">Click **SCHEMA** tab at hello bottom toosee hello schema that hello copy wizard inferred by looking at hello data in hello source file.</span></span>
    5. <span data-ttu-id="cc3a2-455">Tıklatın **sonraki** hello sınırlayıcıları gözden geçirin ve Önizleme veri sonra.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-455">Click **Next** after you review hello delimiters and preview data.</span></span>
    <span data-ttu-id="cc3a2-456">![Kopyalama aracı - dosya biçimi ayarları](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="cc3a2-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="cc3a2-457">Merhaba üzerinde **hedef veri deposu sayfası**seçin **Azure Blob Storage**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-457">On hello **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="cc3a2-458">Her iki hello kaynak ve hedef veri depolarına bu kılavuzda olarak hello Azure Blob Storage kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-458">You are using hello Azure Blob Storage as both hello source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="cc3a2-459">![Kopyalama aracı - select hedef veri deposu](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="cc3a2-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="cc3a2-460">Üzerinde **hello Azure Blob Depolama hesabı belirtin** sayfa:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-460">On **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="cc3a2-461">Girin **AzureStorageLinkedService** hello için **bağlantı adı** alan.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-461">Enter **AzureStorageLinkedService** for hello **Connection name** field.</span></span>
   2. <span data-ttu-id="cc3a2-462">**Hesap seçme yöntemi** için **Azure aboneliklerinden** seçeneğinin belirlendiğini onaylayın.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="cc3a2-463">Azure **aboneliğinizi** seçin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="cc3a2-464">Azure depolama hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="cc3a2-465">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-465">Click **Next**.</span></span>     
10. <span data-ttu-id="cc3a2-466">Merhaba üzerinde **Seç hello çıktı dosya veya klasör** sayfa:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-466">On hello **Choose hello output file or folder** page:</span></span> 
    6. <span data-ttu-id="cc3a2-467">belirtin **klasör yolu** olarak **adfblobconnector/çıkış / {year} / {month} / {day}**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="cc3a2-468">Girin **sekmesini**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="cc3a2-469">Hello için **yıl**seçin **yyyy**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-469">For hello **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="cc3a2-470">Hello için **ay**, çok ayarlandığından emin olun**MM**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-470">For hello **month**, confirm that it is set too**MM**.</span></span>
    9. <span data-ttu-id="cc3a2-471">Hello için **gün**, çok ayarlandığından emin olun**GG**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-471">For hello **day**, confirm that it is set too**dd**.</span></span>
    10. <span data-ttu-id="cc3a2-472">Bu hello onaylayın **sıkıştırma türünü** çok ayarlanır**hiçbiri**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-472">Confirm that hello **compression type** is set too**None**.</span></span>
    11. <span data-ttu-id="cc3a2-473">Bu hello onaylayın **kopyalama davranışı** çok ayarlanır**dosyaları Birleştir**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-473">Confirm that hello **copy behavior** is set too**Merge files**.</span></span> <span data-ttu-id="cc3a2-474">Hello çıkış dosyası ile aynı adı zaten var. Merhaba, hello yeni içerik eklendi toohello hello sonunda dosya aynı olur.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-474">If hello output file with hello same name already exists, hello new content is added toohello same file at hello end.</span></span>
    12. <span data-ttu-id="cc3a2-475">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-475">Click **Next**.</span></span>
    <span data-ttu-id="cc3a2-476">![Kopyalama aracı - çıktı dosyası veya klasörü seçin](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="cc3a2-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="cc3a2-477">Merhaba üzerinde **dosya biçimi ayarları** sayfasında hello ayarlarını gözden geçirin ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-477">On hello **File format settings** page, review hello settings, and click **Next**.</span></span> <span data-ttu-id="cc3a2-478">Burada ek seçenekler hello tooadd üstbilgi toohello çıktı dosyası biridir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-478">One of hello additional options here is tooadd a header toohello output file.</span></span> <span data-ttu-id="cc3a2-479">Bu seçeneği belirlerseniz, bir başlık satırı hello kaynak hello şemadan hello sütunların adlarıyla eklenir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-479">If you select that option, a header row is added with names of hello columns from hello schema of hello source.</span></span> <span data-ttu-id="cc3a2-480">Merhaba varsayılan sütun adları hello kaynak hello şemasını görüntülerken yeniden adlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-480">You can rename hello default column names when viewing hello schema for hello source.</span></span> <span data-ttu-id="cc3a2-481">Örneğin, hello ilk sütun tooFirst adı ve ikinci sütun tooLast adını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-481">For example, you could change hello first column tooFirst Name and second column tooLast Name.</span></span> <span data-ttu-id="cc3a2-482">Ardından, hello çıktı dosyası bu adları içeren bir başlık sütun adları olarak üretilir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-482">Then, hello output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="cc3a2-483">![Kopyalama aracı - hedef için dosya biçimi ayarları](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="cc3a2-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="cc3a2-484">Merhaba üzerinde **performans ayarlarını** sayfasında, onaylayın **bulut birimleri** ve **paralel kopyaları** çok ayarlanır**otomatik**, İleri'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-484">On hello **Performance settings** page, confirm that **cloud units** and **parallel copies** are set too**Auto**, and click Next.</span></span> <span data-ttu-id="cc3a2-485">Bu ayarlar hakkında daha fazla ayrıntı için bkz: [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md#parallel-copy).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="cc3a2-486">![Kopyalama aracı - performans ayarları](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="cc3a2-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="cc3a2-487">Merhaba üzerinde **Özet** sayfasında (görev özellikleri, kaynak ve hedef ayarları ve kopya ayarlarını) tüm ayarları gözden geçirin ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-487">On hello **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="cc3a2-488">![Kopyalama aracı - Özet sayfası](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="cc3a2-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="cc3a2-489">Merhaba bilgileri gözden **Özet** sayfasında ve tıklayın **son**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-489">Review information in hello **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="cc3a2-490">Başlangıç Sihirbazı'nı (Başlangıç burada hello Kopyalama Sihirbazı'nı başlatılan) hello veri fabrikasında iki bağlı hizmet, iki veri kümesi (girdi ve çıktı) ve bir işlem hattı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-490">hello wizard creates two linked services, two datasets (input and output), and one pipeline in hello data factory (from where you launched hello Copy Wizard).</span></span>
    <span data-ttu-id="cc3a2-491">![Kopyalama aracı - dağıtım sayfası](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="cc3a2-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-hello-pipeline-copy-task"></a><span data-ttu-id="cc3a2-492">İzleyici hello ardışık düzen (kopyalama görevi)</span><span class="sxs-lookup"><span data-stu-id="cc3a2-492">Monitor hello pipeline (copy task)</span></span>

1. <span data-ttu-id="cc3a2-493">Merhaba bağlantısına tıklayın `Click here toomonitor copy pipeline` hello üzerinde **dağıtım** sayfası.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-493">Click hello link `Click here toomonitor copy pipeline` on hello **Deployment** page.</span></span> 
2. <span data-ttu-id="cc3a2-494">Merhaba görmelisiniz **izleme ve yönetme uygulaması** ayrı bir sekmede.  ![İzleme ve uygulama yönetme](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="cc3a2-494">You should see hello **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="cc3a2-495">Değişiklik hello **Başlat** hello üstünde çok zaman`04/19/2017` ve **son** çok zaman`04/27/2017`ve ardından **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-495">Change hello **start** time at hello top too`04/19/2017` and **end** time too`04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="cc3a2-496">Beş etkinlik windows hello görmelisiniz **etkinlik WINDOWS** listesi.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-496">You should see five activity windows in hello **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="cc3a2-497">Merhaba **WindowStart** kez ardışık düzen başlangıç toopipeline bitiş zamanları tüm gün kapak.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-497">hello **WindowStart** times should cover all days from pipeline start toopipeline end times.</span></span> 
5. <span data-ttu-id="cc3a2-498">Tıklatın **yenileme** hello düğmesi **etkinlik WINDOWS** birkaç kez tüm hello etkinlik windows hello durumunu görene kadar listesini tooReady ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-498">Click **Refresh** button for hello **ACTIVITY WINDOWS** list a few times until you see hello status of all hello activity windows is set tooReady.</span></span> 
6. <span data-ttu-id="cc3a2-499">Şimdi, adfblobconnector kapsayıcısının çıkış klasörüne hello oluşturulan hello çıktı dosyaları doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-499">Now, verify that hello output files are generated in hello output folder of adfblobconnector container.</span></span> <span data-ttu-id="cc3a2-500">Klasör yapısı hello çıkış klasöründe aşağıdaki hello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-500">You should see hello following folder structure in hello output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="cc3a2-501">İzleme ve veri fabrikaları yönetme hakkında ayrıntılı bilgi için bkz: [İzleyici ve Data Factory işlem hattı yönetmek](data-factory-monitor-manage-app.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="cc3a2-502">Data Factory varlıklarını</span><span class="sxs-lookup"><span data-stu-id="cc3a2-502">Data Factory entities</span></span>
<span data-ttu-id="cc3a2-503">Şimdi, hello Data Factory giriş sayfasına geri toohello sekmesiyle geçin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-503">Now, switch back toohello tab with hello Data Factory home page.</span></span> <span data-ttu-id="cc3a2-504">İki bağlı hizmet, iki veri kümesi ve bir ardışık düzeni, veri fabrikası'nda artık dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![Varlıklarla Data Factory giriş sayfası](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="cc3a2-506">Tıklatın **yazar ve dağıtma** toolaunch Data Factory Düzenleyici.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-506">Click **Author and deploy** toolaunch Data Factory Editor.</span></span> 

![Data Factory Düzenleyicisi](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="cc3a2-508">Data Factory varlıklarını, veri fabrikası'nda aşağıdaki hello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-508">You should see hello following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="cc3a2-509">İki bağlı hizmet.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-509">Two linked services.</span></span> <span data-ttu-id="cc3a2-510">Biri hello kaynak ve hello diğeri hello hedef için.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-510">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="cc3a2-511">İki bağlı hello hizmet toohello başvurmak bu kılavuzda aynı Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-511">Both hello linked services refer toohello same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="cc3a2-512">İki veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-512">Two datasets.</span></span> <span data-ttu-id="cc3a2-513">Bir giriş veri kümesi ve bir çıkış veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="cc3a2-514">Bu kılavuzda, her ikisini de hello kullanmanız aynı blob kapsayıcısı ancak toodifferent klasörleri (girdi ve çıktı) ifade eder.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-514">In this walkthrough, both use hello same blob container but refer toodifferent folders (input and output).</span></span>
 - <span data-ttu-id="cc3a2-515">Ardışık Düzen.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-515">A pipeline.</span></span> <span data-ttu-id="cc3a2-516">Merhaba ardışık düzen blob kaynağı ve Azure blob konumu tooanother Azure blob konumu blob havuz toocopy verilerden kullanan kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-516">hello pipeline contains a copy activity that uses a blob source and a blob sink toocopy data from an Azure blob location tooanother Azure blob location.</span></span> 

<span data-ttu-id="cc3a2-517">Merhaba aşağıdaki bölümler bu varlıkları hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-517">hello following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="cc3a2-518">Bağlı hizmetler</span><span class="sxs-lookup"><span data-stu-id="cc3a2-518">Linked services</span></span>
<span data-ttu-id="cc3a2-519">İki bağlı hizmet görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-519">You should see two linked services.</span></span> <span data-ttu-id="cc3a2-520">Biri hello kaynak ve hello diğeri hello hedef için.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-520">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="cc3a2-521">Bu kılavuzda, her iki tanımları görünüm hello aynı dışında hello adları.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-521">In this walkthrough, both definitions look hello same except for hello names.</span></span> <span data-ttu-id="cc3a2-522">Merhaba **türü** Merhaba bağlantılı hizmet olarak ayarlanmış çok**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-522">hello **type** of hello linked service is set too**AzureStorage**.</span></span> <span data-ttu-id="cc3a2-523">En önemli hello bağlantılı hizmet tanımı özelliğidir hello **connectionString**, veri fabrikası tooconnect tooyour çalışma zamanında Azure depolama hesabı tarafından kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-523">Most important property of hello linked service definition is hello **connectionString**, which is used by Data Factory tooconnect tooyour Azure Storage account at runtime.</span></span> <span data-ttu-id="cc3a2-524">Merhaba hubName özelliği hello tanımında yoksay.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-524">Ignore hello hubName property in hello definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="cc3a2-525">Kaynak blob storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="cc3a2-525">Source blob storage linked service</span></span>
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

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="cc3a2-526">Hedef blob depolama bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="cc3a2-526">Destination blob storage linked service</span></span>

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

<span data-ttu-id="cc3a2-527">Azure Storage bağlı hizmeti hakkında daha fazla bilgi için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="cc3a2-528">Veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="cc3a2-528">Datasets</span></span>
<span data-ttu-id="cc3a2-529">İki veri kümesi vardır: bir giriş veri kümesi ve bir çıkış veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="cc3a2-530">Merhaba dataset Hello türü çok ayarlamak**AzureBlob** her ikisi için de.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-530">hello type of hello dataset is set too**AzureBlob** for both.</span></span> 

<span data-ttu-id="cc3a2-531">Merhaba girdi veri kümesi işaret toohello **giriş** hello klasörünü **adfblobconnector** blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-531">hello input dataset points toohello **input** folder of hello **adfblobconnector** blob container.</span></span> <span data-ttu-id="cc3a2-532">Merhaba **dış** özelliği çok ayarlanmış**true** hello olarak bu veri kümesi için veri hello ardışık düzen tarafından bu veri kümesine bir girdi olarak alır hello kopyalama etkinliği ile oluşturulmuyor.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-532">hello **external** property is set too**true** for this dataset as hello data is not produced by hello pipeline with hello copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="cc3a2-533">Çıktı veri kümesi noktaları toohello hello **çıkış** hello klasörü aynı blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-533">hello output dataset points toohello **output** folder of hello same blob container.</span></span> <span data-ttu-id="cc3a2-534">Merhaba çıktı veri kümesi de hello yıl, ay ve gün Merhaba, kullanır **SliceStart** sistem değişken toodynamically hello çıktı dosyası için hello yol değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-534">hello output dataset also uses hello year, month, and day of hello **SliceStart** system variable toodynamically evaluate hello path for hello output file.</span></span> <span data-ttu-id="cc3a2-535">İşlevler ve Data Factory ile desteklenen sistem değişkenleri listesi için bkz: [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="cc3a2-536">Merhaba **dış** özelliği çok ayarlanmış**false** (varsayılan değer) bu veri kümesi hello ardışık düzen tarafından üretilen olduğundan.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-536">hello **external** property is set too**false** (default value) because this dataset is produced by hello pipeline.</span></span> 

<span data-ttu-id="cc3a2-537">Azure Blob veri kümesi tarafından desteklenen özellikler hakkında daha fazla bilgi için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="cc3a2-538">Girdi veri kümesi</span><span class="sxs-lookup"><span data-stu-id="cc3a2-538">Input dataset</span></span>

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

##### <a name="output-dataset"></a><span data-ttu-id="cc3a2-539">Çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="cc3a2-539">Output dataset</span></span>

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

#### <a name="pipeline"></a><span data-ttu-id="cc3a2-540">İşlem hattı</span><span class="sxs-lookup"><span data-stu-id="cc3a2-540">Pipeline</span></span>
<span data-ttu-id="cc3a2-541">Merhaba ardışık yalnızca bir etkinlik vardır.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-541">hello pipeline has just one activity.</span></span> <span data-ttu-id="cc3a2-542">Merhaba **türü** Merhaba, etkinlik çok ayarlanır**kopya**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-542">hello **type** of hello activity is set too**Copy**.</span></span>  <span data-ttu-id="cc3a2-543">Merhaba etkinliğinin Hello tür özellikleri kaynak ve hello başka bir havuz için iki bölümü vardır.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-543">In hello type properties for hello activity, there are two sections, one for source and hello other one for sink.</span></span> <span data-ttu-id="cc3a2-544">Merhaba kaynak türü çok ayarlamak**BlobSource** hello etkinliği bir blob depolama alanından veri kopyalama gibi.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-544">hello source type is set too**BlobSource** as hello activity is copying data from a blob storage.</span></span> <span data-ttu-id="cc3a2-545">Merhaba Havuz türü çok ayarlanmış**BlobSink** veri tooa blob depolama kopyalama hello etkinlik olarak.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-545">hello sink type is set too**BlobSink** as hello activity copying data tooa blob storage.</span></span> <span data-ttu-id="cc3a2-546">Merhaba kopyalama etkinliği InputDataset z4y hello giriş ve OutputDataset z4y hello çıktı olarak alır.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-546">hello copy activity takes InputDataset-z4y as hello input and OutputDataset-z4y as hello output.</span></span> 

<span data-ttu-id="cc3a2-547">BlobSource ve BlobSink tarafından desteklenen özellikler hakkında daha fazla bilgi için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

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

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a><span data-ttu-id="cc3a2-548">Blob depolama alanından veri tooand kopyalama için JSON örnekleri</span><span class="sxs-lookup"><span data-stu-id="cc3a2-548">JSON examples for copying data tooand from Blob Storage</span></span>  
<span data-ttu-id="cc3a2-549">Merhaba aşağıdaki örneklerde sağlayan örnek JSON tanımları toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-549">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="cc3a2-550">Bunlar Göster nasıl toocopy veri tooand Azure Blob Storage ve Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-550">They show how toocopy data tooand from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="cc3a2-551">Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden belirtildiği hello havuzlarını, kaynakları tooany [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-551">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a><span data-ttu-id="cc3a2-552">JSON örnek: Verilerini Blob Storage tooSQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="cc3a2-552">JSON Example: Copy data from Blob Storage tooSQL Database</span></span>
<span data-ttu-id="cc3a2-553">Merhaba, aşağıdaki örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-553">hello following sample shows:</span></span>

1. <span data-ttu-id="cc3a2-554">Bağlı hizmet türü [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="cc3a2-555">Bağlı hizmet türü [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="cc3a2-556">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="cc3a2-557">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="cc3a2-558">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](#copy-activity-properties) ve [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="cc3a2-559">Merhaba örnek time series verilerini saatlik bir Azure blob tooan Azure SQL tablosundan kopyalar.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-559">hello sample copies time-series data from an Azure blob tooan Azure SQL table hourly.</span></span> <span data-ttu-id="cc3a2-560">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-560">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="cc3a2-561">**Azure SQL bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="cc3a2-561">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="cc3a2-562">**Azure Storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="cc3a2-562">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="cc3a2-563">Azure Data Factory iki tür Azure Storage bağlı hizmeti destekler: **AzureStorage** ve **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="cc3a2-564">İçin birinci Merhaba, hello hesap anahtarı içeren hello bağlantı dizesini belirtin ve hello daha ileri bir hello paylaşılan erişim imzası (SAS) URI belirtin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-564">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="cc3a2-565">Bkz: [bağlı hizmetler](#linked-service-properties) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="cc3a2-566">**Azure Blob girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="cc3a2-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="cc3a2-567">Veri toplanma yeni blob üzerinden saatte (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="cc3a2-568">Merhaba klasör yolu ve dosya adını hello blob dinamik olarak değerlendirilir işleniyor hello dilimin hello başlangıç zamanı temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-568">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="cc3a2-569">Merhaba klasör yolu yıl, ay ve gün kısmını hello başlangıç saati ve dosya adı hello başlangıç saati hello saat bölümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-569">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="cc3a2-570">"dış": "true" ayarı bu hello tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil veri fabrikası sizi bilgilendirir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-570">“external”: “true” setting informs Data Factory that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="cc3a2-571">**Azure SQL çıktı veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="cc3a2-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="cc3a2-572">Merhaba örnek bir Azure SQL veritabanında "MyTable" adlı veri tooa tablosuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-572">hello sample copies data tooa table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="cc3a2-573">Azure SQL veritabanınızda Hello tablo oluşturma hello Blob CSV dosyası toocontain beklediğiniz gibi hello aynı sayıda sütun.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-573">Create hello table in your Azure SQL database with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="cc3a2-574">Yeni satırlar toohello tablo saatte eklenir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-574">New rows are added toohello table every hour.</span></span>

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
<span data-ttu-id="cc3a2-575">**Blob kaynağı ve SQL havuz sahip işlem hattı kopyalama etkinliğinde:**</span><span class="sxs-lookup"><span data-stu-id="cc3a2-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="cc3a2-576">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-576">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="cc3a2-577">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**BlobSource** ve **havuz** türü olarak ayarlanmış çok**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-577">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a><span data-ttu-id="cc3a2-578">JSON örnek: Verilerini Azure SQL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="cc3a2-578">JSON Example: Copy data from Azure SQL tooAzure Blob</span></span>
<span data-ttu-id="cc3a2-579">Merhaba, aşağıdaki örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="cc3a2-579">hello following sample shows:</span></span>

1. <span data-ttu-id="cc3a2-580">Bağlı hizmet türü [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="cc3a2-581">Bağlı hizmet türü [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="cc3a2-582">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="cc3a2-583">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="cc3a2-584">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) ve [BlobSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="cc3a2-585">Merhaba örnek time series verilerini saatlik bir Azure SQL tablosu tooan Azure blob kopyalar.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-585">hello sample copies time-series data from an Azure SQL table tooan Azure blob hourly.</span></span> <span data-ttu-id="cc3a2-586">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-586">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="cc3a2-587">**Azure SQL bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="cc3a2-587">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="cc3a2-588">**Azure Storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="cc3a2-588">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="cc3a2-589">Azure Data Factory iki tür Azure Storage bağlı hizmeti destekler: **AzureStorage** ve **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="cc3a2-590">İçin birinci Merhaba, hello hesap anahtarı içeren hello bağlantı dizesini belirtin ve hello daha ileri bir hello paylaşılan erişim imzası (SAS) URI belirtin.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-590">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="cc3a2-591">Bkz: [bağlı hizmetler](#linked-service-properties) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="cc3a2-592">**Azure SQL girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="cc3a2-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="cc3a2-593">Merhaba örnek "MyTable" Azure SQL tablosu oluşturdunuz ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-593">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="cc3a2-594">"Dış" ayarı: "true" bildirir Data Factory hizmetinin bu hello tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-594">Setting “external”: ”true” informs Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="cc3a2-595">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="cc3a2-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="cc3a2-596">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-596">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="cc3a2-597">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-597">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="cc3a2-598">Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-598">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="cc3a2-599">**SQL kaynak ve Blob havuz sahip işlem hattı kopyalama etkinliğinde:**</span><span class="sxs-lookup"><span data-stu-id="cc3a2-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="cc3a2-600">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-600">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="cc3a2-601">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**SqlSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-601">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="cc3a2-602">Merhaba belirtilen hello SQL sorgusu **SqlReaderQuery** özelliği saat toocopy geçmiş hello hello veri seçer.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-602">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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
> <span data-ttu-id="cc3a2-603">Kaynak veri kümesi toocolumns havuz kümesinden toomap sütunlarından bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="cc3a2-603">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="cc3a2-604">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="cc3a2-604">Performance and Tuning</span></span>
<span data-ttu-id="cc3a2-605">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="cc3a2-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
