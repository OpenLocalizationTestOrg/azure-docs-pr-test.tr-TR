---
title: Amazon Data Factory kullanarak Redshift aaaMove verilerden | Microsoft Docs
description: "Hakkında bilgi edinin Amazon Azure Data Factory kullanarak Redshift toomove verileri."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 01d15078-58dc-455c-9d9d-98fbdf4ea51e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 2a097320734ebdd57282d250f7fdba35741777f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="36250-103">Veri öğesinden Amazon, Redshift Azure Data Factory kullanarak Taşı</span><span class="sxs-lookup"><span data-stu-id="36250-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="36250-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove verileri Amazon Redshift de açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="36250-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from Amazon Redshift.</span></span> <span data-ttu-id="36250-105">Merhaba makale üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="36250-105">hello article builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="36250-106">Verileri Amazon Redshift desteklenen tooany havuz veri deposundan kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36250-106">You can copy data from Amazon Redshift tooany supported sink data store.</span></span> <span data-ttu-id="36250-107">Veri depoları havuzlarını hello kopyalama etkinliği tarafından desteklenen bir listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="36250-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="36250-108">Veri Fabrikası şu anda Amazon Redshift tooother veri depoları, ancak diğer veri depoları tooAmazon Redshift veri taşıma değil veri taşımayı destekler.</span><span class="sxs-lookup"><span data-stu-id="36250-108">Data factory currently supports moving data from Amazon Redshift tooother data stores, but not for moving data from other data stores tooAmazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36250-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="36250-109">Prerequisites</span></span>
* <span data-ttu-id="36250-110">Veri tooan şirket içi veri deposu taşıyorsanız, yükleme [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) , şirket içi makinede.</span><span class="sxs-lookup"><span data-stu-id="36250-110">If you are moving data tooan on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="36250-111">Ardından, Grant veri yönetimi ağ geçidi (hello makinenin IP adresini kullan) hello erişim tooAmazon Redshift kümesi.</span><span class="sxs-lookup"><span data-stu-id="36250-111">Then, Grant Data Management Gateway (use IP address of hello machine) hello access tooAmazon Redshift cluster.</span></span> <span data-ttu-id="36250-112">Bkz: [yetkilendirme access toohello küme](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="36250-112">See [Authorize access toohello cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="36250-113">Veri tooan Azure veri deposu taşıyorsanız bkz [Azure veri merkezi IP aralıkları](https://www.microsoft.com/download/details.aspx?id=41653) hello işlem IP adresi ve hello Azure veri merkezleri tarafından kullanılan SQL aralıkları.</span><span class="sxs-lookup"><span data-stu-id="36250-113">If you are moving data tooan Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for hello Compute IP address and SQL ranges used by hello Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="36250-114">Başlarken</span><span class="sxs-lookup"><span data-stu-id="36250-114">Getting started</span></span>
<span data-ttu-id="36250-115">Farklı araçlar/API'lerini kullanarak bir Amazon Redshift kaynaktan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="36250-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="36250-116">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="36250-116">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="36250-117">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="36250-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="36250-118">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="36250-118">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="36250-119">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="36250-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="36250-120">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="36250-120">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="36250-121">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="36250-121">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="36250-122">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="36250-122">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="36250-123">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="36250-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="36250-124">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="36250-124">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="36250-125">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="36250-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="36250-126">Bir Amazon Redshift veri deposundaki kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: Blob Amazon Redshift tooAzure veri kopyalama](#json-example-copy-data-from-amazon-redshift-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="36250-126">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="36250-127">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooAmazon Redshift olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="36250-127">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="36250-128">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="36250-128">Linked service properties</span></span>
<span data-ttu-id="36250-129">Aşağıdaki tablonun hello JSON öğeleri belirli tooAmazon Redshift bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="36250-129">hello following table provides description for JSON elements specific tooAmazon Redshift linked service.</span></span>

| <span data-ttu-id="36250-130">Özellik</span><span class="sxs-lookup"><span data-stu-id="36250-130">Property</span></span> | <span data-ttu-id="36250-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36250-131">Description</span></span> | <span data-ttu-id="36250-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="36250-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36250-133">type</span><span class="sxs-lookup"><span data-stu-id="36250-133">type</span></span> |<span data-ttu-id="36250-134">Merhaba type özelliği ayarlanmalıdır: **AmazonRedshift**.</span><span class="sxs-lookup"><span data-stu-id="36250-134">hello type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="36250-135">Evet</span><span class="sxs-lookup"><span data-stu-id="36250-135">Yes</span></span> |
| <span data-ttu-id="36250-136">sunucu</span><span class="sxs-lookup"><span data-stu-id="36250-136">server</span></span> |<span data-ttu-id="36250-137">IP adresi veya ana bilgisayar hello Amazon Redshift sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="36250-137">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="36250-138">Evet</span><span class="sxs-lookup"><span data-stu-id="36250-138">Yes</span></span> |
| <span data-ttu-id="36250-139">port</span><span class="sxs-lookup"><span data-stu-id="36250-139">port</span></span> |<span data-ttu-id="36250-140">Amazon Redshift sunucu hello hello TCP bağlantı noktası sayısı Hello toolisten istemci bağlantıları için kullanır.</span><span class="sxs-lookup"><span data-stu-id="36250-140">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="36250-141">Hayır, varsayılan değer: 5439</span><span class="sxs-lookup"><span data-stu-id="36250-141">No, default value: 5439</span></span> |
| <span data-ttu-id="36250-142">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="36250-142">database</span></span> |<span data-ttu-id="36250-143">Merhaba Amazon Redshift veritabanının adı.</span><span class="sxs-lookup"><span data-stu-id="36250-143">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="36250-144">Evet</span><span class="sxs-lookup"><span data-stu-id="36250-144">Yes</span></span> |
| <span data-ttu-id="36250-145">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="36250-145">username</span></span> |<span data-ttu-id="36250-146">Erişim toohello veritabanı olan kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="36250-146">Name of user who has access toohello database.</span></span> |<span data-ttu-id="36250-147">Evet</span><span class="sxs-lookup"><span data-stu-id="36250-147">Yes</span></span> |
| <span data-ttu-id="36250-148">password</span><span class="sxs-lookup"><span data-stu-id="36250-148">password</span></span> |<span data-ttu-id="36250-149">Merhaba kullanıcı hesabının parolası.</span><span class="sxs-lookup"><span data-stu-id="36250-149">Password for hello user account.</span></span> |<span data-ttu-id="36250-150">Evet</span><span class="sxs-lookup"><span data-stu-id="36250-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="36250-151">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="36250-151">Dataset properties</span></span>
<span data-ttu-id="36250-152">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="36250-152">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="36250-153">Bölümler yapısı, kullanılabilirlik ve ilke gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="36250-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="36250-154">Merhaba **typeProperties** bölümü, her veri kümesi türü için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="36250-154">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="36250-155">Merhaba veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="36250-155">It provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="36250-156">Merhaba typeProperties bölüm türü veri kümesi için **RelationalTable** hello aşağıdaki özelliklere sahip (Amazon Redshift dataset içerir)</span><span class="sxs-lookup"><span data-stu-id="36250-156">hello typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has hello following properties</span></span>

| <span data-ttu-id="36250-157">Özellik</span><span class="sxs-lookup"><span data-stu-id="36250-157">Property</span></span> | <span data-ttu-id="36250-158">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36250-158">Description</span></span> | <span data-ttu-id="36250-159">Gerekli</span><span class="sxs-lookup"><span data-stu-id="36250-159">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36250-160">tableName</span><span class="sxs-lookup"><span data-stu-id="36250-160">tableName</span></span> |<span data-ttu-id="36250-161">Bağlantılı hizmetinin hello Amazon Redshift veritabanında Merhaba tablonun adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="36250-161">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="36250-162">Hayır (varsa **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="36250-162">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="36250-163">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="36250-163">Copy activity properties</span></span>
<span data-ttu-id="36250-164">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="36250-164">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="36250-165">Ad, açıklama, giriş ve çıkış tabloları ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="36250-165">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="36250-166">Oysa hello kullanılabilen özellikleri **typeProperties** hello etkinlik bölümünü her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="36250-166">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="36250-167">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="36250-167">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="36250-168">Kopyalama etkinliği kaynağının türü olduğunda **RelationalSource** (içeren Amazon Redshift), aşağıdaki özelliklere hello typeProperties bölümünde bulunur:</span><span class="sxs-lookup"><span data-stu-id="36250-168">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="36250-169">Özellik</span><span class="sxs-lookup"><span data-stu-id="36250-169">Property</span></span> | <span data-ttu-id="36250-170">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36250-170">Description</span></span> | <span data-ttu-id="36250-171">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="36250-171">Allowed values</span></span> | <span data-ttu-id="36250-172">Gerekli</span><span class="sxs-lookup"><span data-stu-id="36250-172">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="36250-173">sorgu</span><span class="sxs-lookup"><span data-stu-id="36250-173">query</span></span> |<span data-ttu-id="36250-174">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="36250-174">Use hello custom query tooread data.</span></span> |<span data-ttu-id="36250-175">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="36250-175">SQL query string.</span></span> <span data-ttu-id="36250-176">Örneğin: seçin * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="36250-176">For example: select * from MyTable.</span></span> |<span data-ttu-id="36250-177">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="36250-177">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-tooazure-blob"></a><span data-ttu-id="36250-178">JSON örnek: Blob Amazon Redshift tooAzure veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="36250-178">JSON example: Copy data from Amazon Redshift tooAzure Blob</span></span>
<span data-ttu-id="36250-179">Bu örnekte, nasıl bir Amazon Redshift toocopy verileri Azure Blob Storage tooan veritabanı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="36250-179">This sample shows how toocopy data from an Amazon Redshift database tooan Azure Blob Storage.</span></span> <span data-ttu-id="36250-180">Ancak, veriler kopyalanabilir **doğrudan** belirtildiği hello havuzlarını tooany [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="36250-180">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="36250-181">Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="36250-181">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="36250-182">Bağlı hizmet türü [AmazonRedshift](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="36250-182">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="36250-183">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="36250-183">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="36250-184">Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="36250-184">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="36250-185">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="36250-185">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="36250-186">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="36250-186">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="36250-187">Merhaba örnek verileri Amazon Redshift tooa blob bir sorgu sonucunda her saat kopyalar.</span><span class="sxs-lookup"><span data-stu-id="36250-187">hello sample copies data from a query result in Amazon Redshift tooa blob every hour.</span></span> <span data-ttu-id="36250-188">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="36250-188">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="36250-189">**Amazon bağlı Redshift hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="36250-189">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< hello IP address or host name of hello Amazon Redshift server >",
            "port": <hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.>,
            "database": "<hello database name of hello Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="36250-190">**Azure Storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="36250-190">**Azure Storage linked service:**</span></span>

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="36250-191">**Amazon Redshift girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="36250-191">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="36250-192">Ayarı `"external": true` hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.</span><span class="sxs-lookup"><span data-stu-id="36250-192">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="36250-193">Bu özellik tootrue hello ardışık düzeninde bir etkinlik tarafından üretilen olmayan bir girdi veri kümesi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="36250-193">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="36250-194">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="36250-194">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="36250-195">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="36250-195">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="36250-196">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="36250-196">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="36250-197">Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="36250-197">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazonredshift/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="36250-198">**Azure Redshift kaynak (RelationalSource) ve Blob havuz ile ardışık düzeninde etkinlik kopyalayın:**</span><span class="sxs-lookup"><span data-stu-id="36250-198">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="36250-199">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="36250-199">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="36250-200">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**RelationalSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="36250-200">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="36250-201">Merhaba belirtilen hello SQL sorgusu **sorgu** özelliği saat toocopy geçmiş hello hello veri seçer.</span><span class="sxs-lookup"><span data-stu-id="36250-201">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonRedshiftInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonRedshiftToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="36250-202">Tür eşlemesi için Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="36250-202">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="36250-203">Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri iki aşamalı bir yaklaşım aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="36250-203">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="36250-204">Yerel kaynak türleri too.NET türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="36250-204">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="36250-205">.NET türü toonative havuz türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="36250-205">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="36250-206">Veri tooAmazon Redshift taşırken eşlemeleri aşağıdaki hello Amazon Redshift türleri too.NET türlerinden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="36250-206">When moving data tooAmazon Redshift, hello following mappings are used from Amazon Redshift types too.NET types.</span></span>

| <span data-ttu-id="36250-207">Amazon Redshift türü</span><span class="sxs-lookup"><span data-stu-id="36250-207">Amazon Redshift Type</span></span> | <span data-ttu-id="36250-208">.NET türü temelinde</span><span class="sxs-lookup"><span data-stu-id="36250-208">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="36250-209">TAMSAYI</span><span class="sxs-lookup"><span data-stu-id="36250-209">SMALLINT</span></span> |<span data-ttu-id="36250-210">Int16</span><span class="sxs-lookup"><span data-stu-id="36250-210">Int16</span></span> |
| <span data-ttu-id="36250-211">TAMSAYI</span><span class="sxs-lookup"><span data-stu-id="36250-211">INTEGER</span></span> |<span data-ttu-id="36250-212">Int32</span><span class="sxs-lookup"><span data-stu-id="36250-212">Int32</span></span> |
| <span data-ttu-id="36250-213">BIGINT</span><span class="sxs-lookup"><span data-stu-id="36250-213">BIGINT</span></span> |<span data-ttu-id="36250-214">Int64</span><span class="sxs-lookup"><span data-stu-id="36250-214">Int64</span></span> |
| <span data-ttu-id="36250-215">ONDALIK</span><span class="sxs-lookup"><span data-stu-id="36250-215">DECIMAL</span></span> |<span data-ttu-id="36250-216">Ondalık</span><span class="sxs-lookup"><span data-stu-id="36250-216">Decimal</span></span> |
| <span data-ttu-id="36250-217">GERÇEK</span><span class="sxs-lookup"><span data-stu-id="36250-217">REAL</span></span> |<span data-ttu-id="36250-218">Tek</span><span class="sxs-lookup"><span data-stu-id="36250-218">Single</span></span> |
| <span data-ttu-id="36250-219">ÇİFT DUYARLIKLI</span><span class="sxs-lookup"><span data-stu-id="36250-219">DOUBLE PRECISION</span></span> |<span data-ttu-id="36250-220">Çift</span><span class="sxs-lookup"><span data-stu-id="36250-220">Double</span></span> |
| <span data-ttu-id="36250-221">BOOLE DEĞERİ</span><span class="sxs-lookup"><span data-stu-id="36250-221">BOOLEAN</span></span> |<span data-ttu-id="36250-222">Dize</span><span class="sxs-lookup"><span data-stu-id="36250-222">String</span></span> |
| <span data-ttu-id="36250-223">CHAR</span><span class="sxs-lookup"><span data-stu-id="36250-223">CHAR</span></span> |<span data-ttu-id="36250-224">Dize</span><span class="sxs-lookup"><span data-stu-id="36250-224">String</span></span> |
| <span data-ttu-id="36250-225">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="36250-225">VARCHAR</span></span> |<span data-ttu-id="36250-226">Dize</span><span class="sxs-lookup"><span data-stu-id="36250-226">String</span></span> |
| <span data-ttu-id="36250-227">TARİH</span><span class="sxs-lookup"><span data-stu-id="36250-227">DATE</span></span> |<span data-ttu-id="36250-228">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="36250-228">DateTime</span></span> |
| <span data-ttu-id="36250-229">ZAMAN DAMGASI</span><span class="sxs-lookup"><span data-stu-id="36250-229">TIMESTAMP</span></span> |<span data-ttu-id="36250-230">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="36250-230">DateTime</span></span> |
| <span data-ttu-id="36250-231">METİN</span><span class="sxs-lookup"><span data-stu-id="36250-231">TEXT</span></span> |<span data-ttu-id="36250-232">Dize</span><span class="sxs-lookup"><span data-stu-id="36250-232">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="36250-233">Kaynak toosink sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="36250-233">Map source toosink columns</span></span>
<span data-ttu-id="36250-234">Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="36250-234">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="36250-235">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="36250-235">Repeatable read from relational sources</span></span>
<span data-ttu-id="36250-236">İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="36250-236">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="36250-237">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36250-237">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="36250-238">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36250-238">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="36250-239">Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="36250-239">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="36250-240">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="36250-240">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="36250-241">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="36250-241">Performance and Tuning</span></span>
<span data-ttu-id="36250-242">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="36250-242">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36250-243">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="36250-243">Next Steps</span></span>
<span data-ttu-id="36250-244">Aşağıdaki makaleleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="36250-244">See hello following articles:</span></span>

* <span data-ttu-id="36250-245">[Kopya etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak için adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="36250-245">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
