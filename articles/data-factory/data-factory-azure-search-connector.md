---
title: "Data Factory kullanarak Search dizinine veri gönderme | Microsoft Docs"
description: "Azure Data Factory kullanarak Azure Search dizinine veri gönderme hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5c617c7a2f2eb4da2164ce5f802354a64dfd1fa1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="push-data-to-an-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="64a77-103">Azure Data Factory kullanarak Azure Search dizini veri göndermek</span><span class="sxs-lookup"><span data-stu-id="64a77-103">Push data to an Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="64a77-104">Bu makalede, Azure Search dizini için desteklenen kaynak veri deposundan veri göndermek için kopyalama etkinliği kullanmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="64a77-104">This article describes how to use the Copy Activity to push data from a supported source data store to Azure Search index.</span></span> <span data-ttu-id="64a77-105">Desteklenen kaynak veri depoları, kaynağı sütununda listelenen [desteklenen kaynakları ve havuzlarını](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="64a77-105">Supported source data stores are listed in the Source column of the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="64a77-106">Bu makalede derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) desteklenen veri deposu birleşimleri kopyalama etkinliği ile veri taşıma için genel bir bakış sunan makalesi.</span><span class="sxs-lookup"><span data-stu-id="64a77-106">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="64a77-107">Bağlantıyı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="64a77-107">Enabling connectivity</span></span>
<span data-ttu-id="64a77-108">Veri Fabrikası hizmetine bağlanın bir şirket içi veri deposuna izin vermek için şirket içi ortamınızda veri yönetimi ağ geçidi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="64a77-108">To allow Data Factory service connect to an on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="64a77-109">Ağ geçidi ana bilgisayar veri kaynağını depolamak aynı makine üzerindeki veya veri depolama alanı kaynakları için rekabete önlemek için ayrı bir makine yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64a77-109">You can install gateway on the same machine that hosts the source data store or on a separate machine to avoid competing for resources with the data store.</span></span>

<span data-ttu-id="64a77-110">Veri Yönetimi ağ geçidi şirket içi veri kaynaklarına güvenli ve yönetilen bir şekilde bulut hizmetlerine bağlar.</span><span class="sxs-lookup"><span data-stu-id="64a77-110">Data Management Gateway connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="64a77-111">Bkz: [şirket içi ve bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale veri yönetimi ağ geçidi hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="64a77-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="64a77-112">Başlarken</span><span class="sxs-lookup"><span data-stu-id="64a77-112">Getting started</span></span>
<span data-ttu-id="64a77-113">Veri kaynağı veri deposundan farklı araçlar/API'lerini kullanarak Azure Search dizinine iter kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="64a77-113">You can create a pipeline with a copy activity that pushes data from a source data store to Azure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="64a77-114">Bir işlem hattı oluşturmak için en kolay yolu kullanmaktır **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="64a77-114">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="64a77-115">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) veri kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="64a77-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="64a77-116">Bir işlem hattı oluşturmak için aşağıdaki araçları kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu**, **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="64a77-116">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="64a77-117">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="64a77-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="64a77-118">Araçlar ya da API'leri kullanıp bir havuz veri deposu için bir kaynak veri deposundan verileri taşır bir ardışık düzen oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="64a77-118">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="64a77-119">Oluşturma **bağlantılı Hizmetleri** girdi ve çıktı verilerini bağlamak için veri fabrikanıza depolar.</span><span class="sxs-lookup"><span data-stu-id="64a77-119">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="64a77-120">Oluşturma **veri kümeleri** kopyalama işlemi için girdi ve çıktı verilerini temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="64a77-120">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="64a77-121">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="64a77-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="64a77-122">Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="64a77-122">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="64a77-123">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, JSON biçimini kullanarak bu Data Factory varlıklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="64a77-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="64a77-124">Azure Search dizinine veri kopyalamak için kullanılan Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: veri kopyalama şirket içi SQL Server'dan Azure Search dizinine](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="64a77-124">For a sample with JSON definitions for Data Factory entities that are used to copy data to Azure Search index, see [JSON example: Copy data from on-premises SQL Server to Azure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="64a77-125">Aşağıdaki bölümler, Azure Search dizinine Data Factory varlıklarını belirli tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="64a77-125">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="64a77-126">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="64a77-126">Linked service properties</span></span>

<span data-ttu-id="64a77-127">Aşağıdaki tabloda Azure Search bağlantılı hizmete özgü JSON öğeleri için açıklamalar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="64a77-127">The following table provides descriptions for JSON elements that are specific to the Azure Search linked service.</span></span>

| <span data-ttu-id="64a77-128">Özellik</span><span class="sxs-lookup"><span data-stu-id="64a77-128">Property</span></span> | <span data-ttu-id="64a77-129">Açıklama</span><span class="sxs-lookup"><span data-stu-id="64a77-129">Description</span></span> | <span data-ttu-id="64a77-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="64a77-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="64a77-131">type</span><span class="sxs-lookup"><span data-stu-id="64a77-131">type</span></span> | <span data-ttu-id="64a77-132">Type özelliği ayarlanmalıdır: **AzureSearch**.</span><span class="sxs-lookup"><span data-stu-id="64a77-132">The type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="64a77-133">Evet</span><span class="sxs-lookup"><span data-stu-id="64a77-133">Yes</span></span> |
| <span data-ttu-id="64a77-134">URL</span><span class="sxs-lookup"><span data-stu-id="64a77-134">url</span></span> | <span data-ttu-id="64a77-135">Azure Search hizmeti için URL.</span><span class="sxs-lookup"><span data-stu-id="64a77-135">URL for the Azure Search service.</span></span> | <span data-ttu-id="64a77-136">Evet</span><span class="sxs-lookup"><span data-stu-id="64a77-136">Yes</span></span> |
| <span data-ttu-id="64a77-137">anahtar</span><span class="sxs-lookup"><span data-stu-id="64a77-137">key</span></span> | <span data-ttu-id="64a77-138">Azure Search hizmeti için yönetici anahtarı.</span><span class="sxs-lookup"><span data-stu-id="64a77-138">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="64a77-139">Evet</span><span class="sxs-lookup"><span data-stu-id="64a77-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="64a77-140">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="64a77-140">Dataset properties</span></span>

<span data-ttu-id="64a77-141">Bölümleri ve veri kümelerini tanımlamak için kullanılabilir olan özellikleri tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="64a77-141">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="64a77-142">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri kümesi türleri için benzerdir.</span><span class="sxs-lookup"><span data-stu-id="64a77-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="64a77-143">**TypeProperties** bölümü, her veri kümesi türü için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="64a77-143">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="64a77-144">TypeProperties bölüm türü veri kümesi için **AzureSearchIndex** aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="64a77-144">The typeProperties section for a dataset of the type **AzureSearchIndex** has the following properties:</span></span>

| <span data-ttu-id="64a77-145">Özellik</span><span class="sxs-lookup"><span data-stu-id="64a77-145">Property</span></span> | <span data-ttu-id="64a77-146">Açıklama</span><span class="sxs-lookup"><span data-stu-id="64a77-146">Description</span></span> | <span data-ttu-id="64a77-147">Gerekli</span><span class="sxs-lookup"><span data-stu-id="64a77-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="64a77-148">type</span><span class="sxs-lookup"><span data-stu-id="64a77-148">type</span></span> | <span data-ttu-id="64a77-149">Type özelliği ayarlamak **AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="64a77-149">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="64a77-150">Evet</span><span class="sxs-lookup"><span data-stu-id="64a77-150">Yes</span></span> |
| <span data-ttu-id="64a77-151">indexName</span><span class="sxs-lookup"><span data-stu-id="64a77-151">indexName</span></span> | <span data-ttu-id="64a77-152">Azure Search dizini adı.</span><span class="sxs-lookup"><span data-stu-id="64a77-152">Name of the Azure Search index.</span></span> <span data-ttu-id="64a77-153">Veri Fabrikası dizinini oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="64a77-153">Data Factory does not create the index.</span></span> <span data-ttu-id="64a77-154">Azure Search'te dizin mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="64a77-154">The index must exist in Azure Search.</span></span> | <span data-ttu-id="64a77-155">Evet</span><span class="sxs-lookup"><span data-stu-id="64a77-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="64a77-156">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="64a77-156">Copy activity properties</span></span>
<span data-ttu-id="64a77-157">Bölümleri ve etkinlikleri tanımlamak için kullanılabilir olan özellikleri tam listesi için bkz: [ardışık düzen oluşturma](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="64a77-157">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="64a77-158">Ad, açıklama, giriş ve çıkış tabloları ve çeşitli ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="64a77-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="64a77-159">Oysa typeProperties bölümündeki özellikler her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="64a77-159">Whereas, properties available in the typeProperties section vary with each activity type.</span></span> <span data-ttu-id="64a77-160">Kopya etkinliği için bunlar türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="64a77-160">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="64a77-161">Kopyalama Havuz türü olduğunda etkinliği için **AzureSearchIndexSink**, typeProperties bölümünde aşağıdaki özellikler kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="64a77-161">For Copy Activity, when the sink is of the type **AzureSearchIndexSink**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="64a77-162">Özellik</span><span class="sxs-lookup"><span data-stu-id="64a77-162">Property</span></span> | <span data-ttu-id="64a77-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="64a77-163">Description</span></span> | <span data-ttu-id="64a77-164">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="64a77-164">Allowed values</span></span> | <span data-ttu-id="64a77-165">Gerekli</span><span class="sxs-lookup"><span data-stu-id="64a77-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="64a77-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="64a77-166">WriteBehavior</span></span> | <span data-ttu-id="64a77-167">Birleştir veya bir belge dizinde zaten mevcut olduğunda Değiştir belirtir.</span><span class="sxs-lookup"><span data-stu-id="64a77-167">Specifies whether to merge or replace when a document already exists in the index.</span></span> <span data-ttu-id="64a77-168">Bkz: [WriteBehavior özelliği](#writebehavior-property).</span><span class="sxs-lookup"><span data-stu-id="64a77-168">See the [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="64a77-169">Merge (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="64a77-169">Merge (default)</span></span><br/><span data-ttu-id="64a77-170">Karşıya Yükle</span><span class="sxs-lookup"><span data-stu-id="64a77-170">Upload</span></span>| <span data-ttu-id="64a77-171">Hayır</span><span class="sxs-lookup"><span data-stu-id="64a77-171">No</span></span> |
| <span data-ttu-id="64a77-172">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="64a77-172">WriteBatchSize</span></span> | <span data-ttu-id="64a77-173">Arabellek boyutu writeBatchSize ulaştığında Azure Search dizinine veri yükler.</span><span class="sxs-lookup"><span data-stu-id="64a77-173">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="64a77-174">Bkz: [WriteBatchSize özelliği](#writebatchsize-property) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="64a77-174">See the [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="64a77-175">1 için 1.000.</span><span class="sxs-lookup"><span data-stu-id="64a77-175">1 to 1,000.</span></span> <span data-ttu-id="64a77-176">Varsayılan değer 1000'dir.</span><span class="sxs-lookup"><span data-stu-id="64a77-176">Default value is 1000.</span></span> | <span data-ttu-id="64a77-177">Hayır</span><span class="sxs-lookup"><span data-stu-id="64a77-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="64a77-178">WriteBehavior özelliği</span><span class="sxs-lookup"><span data-stu-id="64a77-178">WriteBehavior property</span></span>
<span data-ttu-id="64a77-179">Verileri yazarken AzureSearchSink upserts.</span><span class="sxs-lookup"><span data-stu-id="64a77-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="64a77-180">Diğer bir deyişle, belge anahtarı Azure arama dizini zaten varsa bir belge yazarken, Azure Search çakışma özel durum atma yerine varolan bir belgeyi güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="64a77-180">In other words, when writing a document, if the document key already exists in the Azure Search index, Azure Search updates the existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="64a77-181">AzureSearchSink (AzureSearch SDK kullanılarak) aşağıdaki iki upsert davranışlar sağlar:</span><span class="sxs-lookup"><span data-stu-id="64a77-181">The AzureSearchSink provides the following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="64a77-182">**Birleştirme**: yeni belgedeki tüm sütunları mevcut birleştirin.</span><span class="sxs-lookup"><span data-stu-id="64a77-182">**Merge**: combine all the columns in the new document with the existing one.</span></span> <span data-ttu-id="64a77-183">Yeni belge null değere sahip sütunlar için mevcut değeri korunur.</span><span class="sxs-lookup"><span data-stu-id="64a77-183">For columns with null value in the new document, the value in the existing one is preserved.</span></span>
- <span data-ttu-id="64a77-184">**Karşıya yükleme**: varolan bir yeni belge değiştirir.</span><span class="sxs-lookup"><span data-stu-id="64a77-184">**Upload**: The new document replaces the existing one.</span></span> <span data-ttu-id="64a77-185">Yeni belge içinde belirtilmeyen sütunlar için değer olup olmadığını değeri null olmayan mevcut belgede veya null olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="64a77-185">For columns not specified in the new document, the value is set to null whether there is a non-null value in the existing document or not.</span></span>

<span data-ttu-id="64a77-186">Varsayılan davranış **birleştirme**.</span><span class="sxs-lookup"><span data-stu-id="64a77-186">The default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="64a77-187">WriteBatchSize özelliği</span><span class="sxs-lookup"><span data-stu-id="64a77-187">WriteBatchSize Property</span></span>
<span data-ttu-id="64a77-188">Azure Search Hizmeti yazma belgeleri toplu iş olarak destekler.</span><span class="sxs-lookup"><span data-stu-id="64a77-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="64a77-189">Bir toplu iş için 1 1.000 eylemler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="64a77-189">A batch can contain 1 to 1,000 Actions.</span></span> <span data-ttu-id="64a77-190">Bir eylem karşıya yükleme/birleştirme işlemi gerçekleştirmek için bir belge işler.</span><span class="sxs-lookup"><span data-stu-id="64a77-190">An action handles one document to perform the upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="64a77-191">Veri türü desteği</span><span class="sxs-lookup"><span data-stu-id="64a77-191">Data type support</span></span>
<span data-ttu-id="64a77-192">Aşağıdaki tabloda, bir Azure Search veri türü veya desteklenip desteklenmediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="64a77-192">The following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="64a77-193">Azure arama veri türü</span><span class="sxs-lookup"><span data-stu-id="64a77-193">Azure Search data type</span></span> | <span data-ttu-id="64a77-194">Azure arama havuzunda desteklenir</span><span class="sxs-lookup"><span data-stu-id="64a77-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="64a77-195">Dize</span><span class="sxs-lookup"><span data-stu-id="64a77-195">String</span></span> | <span data-ttu-id="64a77-196">E</span><span class="sxs-lookup"><span data-stu-id="64a77-196">Y</span></span> |
| <span data-ttu-id="64a77-197">Int32</span><span class="sxs-lookup"><span data-stu-id="64a77-197">Int32</span></span> | <span data-ttu-id="64a77-198">E</span><span class="sxs-lookup"><span data-stu-id="64a77-198">Y</span></span> |
| <span data-ttu-id="64a77-199">Int64</span><span class="sxs-lookup"><span data-stu-id="64a77-199">Int64</span></span> | <span data-ttu-id="64a77-200">E</span><span class="sxs-lookup"><span data-stu-id="64a77-200">Y</span></span> |
| <span data-ttu-id="64a77-201">Çift</span><span class="sxs-lookup"><span data-stu-id="64a77-201">Double</span></span> | <span data-ttu-id="64a77-202">E</span><span class="sxs-lookup"><span data-stu-id="64a77-202">Y</span></span> |
| <span data-ttu-id="64a77-203">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="64a77-203">Boolean</span></span> | <span data-ttu-id="64a77-204">E</span><span class="sxs-lookup"><span data-stu-id="64a77-204">Y</span></span> |
| <span data-ttu-id="64a77-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="64a77-205">DataTimeOffset</span></span> | <span data-ttu-id="64a77-206">E</span><span class="sxs-lookup"><span data-stu-id="64a77-206">Y</span></span> |
| <span data-ttu-id="64a77-207">Dize dizisi</span><span class="sxs-lookup"><span data-stu-id="64a77-207">String Array</span></span> | <span data-ttu-id="64a77-208">N</span><span class="sxs-lookup"><span data-stu-id="64a77-208">N</span></span> |
| <span data-ttu-id="64a77-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="64a77-209">GeographyPoint</span></span> | <span data-ttu-id="64a77-210">N</span><span class="sxs-lookup"><span data-stu-id="64a77-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-to-azure-search-index"></a><span data-ttu-id="64a77-211">JSON örnek: veri kopyalama şirket içi SQL Server'dan Azure Search dizini</span><span class="sxs-lookup"><span data-stu-id="64a77-211">JSON example: Copy data from on-premises SQL Server to Azure Search index</span></span>

<span data-ttu-id="64a77-212">Aşağıdaki örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="64a77-212">The following sample shows:</span></span>

1.  <span data-ttu-id="64a77-213">Bağlı hizmet türü [AzureSearch](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="64a77-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="64a77-214">Bağlı hizmet türü [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="64a77-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="64a77-215">Bir giriş [dataset](data-factory-create-datasets.md) türü [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="64a77-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="64a77-216">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureSearchIndex](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="64a77-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="64a77-217">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) ve [AzureSearchIndexSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="64a77-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="64a77-218">Örnek zaman serisi veri bir şirket içi SQL Server veritabanından bir Azure Search dizini saatlik kopyalar.</span><span class="sxs-lookup"><span data-stu-id="64a77-218">The sample copies time-series data from an on-premises SQL Server database to an Azure Search index hourly.</span></span> <span data-ttu-id="64a77-219">Bu örnekte kullanılan JSON özellikleri örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="64a77-219">The JSON properties used in this sample are described in sections following the samples.</span></span>

<span data-ttu-id="64a77-220">İlk adım olarak, veri yönetimi ağ geçidi, şirket içi makinenizde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="64a77-220">As a first step, setup the data management gateway on your on-premises machine.</span></span> <span data-ttu-id="64a77-221">Yönergeler bulunan [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="64a77-221">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="64a77-222">**Azure arama bağlantılı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="64a77-222">**Azure Search linked service:**</span></span>

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="64a77-223">**SQL Server bağlantılı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="64a77-223">**SQL Server linked service**</span></span>

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

<span data-ttu-id="64a77-224">**SQL Server girdi veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="64a77-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="64a77-225">Örnek SQL Server'da bir tablo "MyTable" oluşturulur ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="64a77-225">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="64a77-226">Tek bir veri kümesini kullanarak aynı veritabanı içinde birden çok tablo üzerinde sorgulayabilir, ancak tek bir tablo için veri kümesi'nin tableName typeProperty kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="64a77-226">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="64a77-227">"Dış" ayarı: "true" bildirir Data Factory hizmetinin veri kümesi data factory dış ve veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="64a77-227">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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

<span data-ttu-id="64a77-228">**Azure Search'te veri kümesini çıktı:**</span><span class="sxs-lookup"><span data-stu-id="64a77-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="64a77-229">Örnek verileri adlı bir Azure Search dizini kopyalar **ürünleri**.</span><span class="sxs-lookup"><span data-stu-id="64a77-229">The sample copies data to an Azure Search index named **products**.</span></span> <span data-ttu-id="64a77-230">Veri Fabrikası dizinini oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="64a77-230">Data Factory does not create the index.</span></span> <span data-ttu-id="64a77-231">Örnek test etmek için bu ada sahip bir dizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="64a77-231">To test the sample, create an index with this name.</span></span> <span data-ttu-id="64a77-232">İle aynı sayıda sütun girdi veri kümesi olduğu gibi Azure Search dizini oluşturma.</span><span class="sxs-lookup"><span data-stu-id="64a77-232">Create the Azure Search index with the same number of columns as in the input dataset.</span></span> <span data-ttu-id="64a77-233">Yeni girişler için Azure Search dizini saatte eklenir.</span><span class="sxs-lookup"><span data-stu-id="64a77-233">New entries are added to the Azure Search index every hour.</span></span>

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

<span data-ttu-id="64a77-234">**SQL kaynak ve Azure Search dizini havuz ile ardışık düzeninde etkinlik kopyalayın:**</span><span class="sxs-lookup"><span data-stu-id="64a77-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="64a77-235">Ardışık Düzen giriş ve çıkış veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="64a77-235">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="64a77-236">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **SqlSource** ve **havuz** türü ayarlanmış **AzureSearchIndexSink**.</span><span class="sxs-lookup"><span data-stu-id="64a77-236">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **AzureSearchIndexSink**.</span></span> <span data-ttu-id="64a77-237">SQL sorgusu için belirtilen **SqlReaderQuery** özelliği veri kopyalamak için son bir saat içindeki seçer.</span><span class="sxs-lookup"><span data-stu-id="64a77-237">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
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

<span data-ttu-id="64a77-238">Azure Search bir bulut veri deposundan veri kopyalıyorsanız `executionLocation` özelliği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="64a77-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="64a77-239">Kopyalama etkinliği altında gerekli değişiklik aşağıdaki JSON parçacığı gösterir `typeProperties` bir örnek olarak.</span><span class="sxs-lookup"><span data-stu-id="64a77-239">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="64a77-240">Denetleme [bulut veri depoları arasında veri kopyalama](data-factory-data-movement-activities.md#global) desteklenen değerler ve daha fazla ayrıntı için bölüm.</span><span class="sxs-lookup"><span data-stu-id="64a77-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="64a77-241">Bir bulut kaynaktan kopyalama</span><span class="sxs-lookup"><span data-stu-id="64a77-241">Copy from a cloud source</span></span>
<span data-ttu-id="64a77-242">Azure Search bir bulut veri deposundan veri kopyalıyorsanız `executionLocation` özelliği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="64a77-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="64a77-243">Kopyalama etkinliği altında gerekli değişiklik aşağıdaki JSON parçacığı gösterir `typeProperties` bir örnek olarak.</span><span class="sxs-lookup"><span data-stu-id="64a77-243">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="64a77-244">Denetleme [bulut veri depoları arasında veri kopyalama](data-factory-data-movement-activities.md#global) desteklenen değerler ve daha fazla ayrıntı için bölüm.</span><span class="sxs-lookup"><span data-stu-id="64a77-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

<span data-ttu-id="64a77-245">Ayrıca havuz dataset kopyalama etkinliği tanımında sütunları kaynak kümesinden sütunları eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64a77-245">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="64a77-246">Ayrıntılar için bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="64a77-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="64a77-247">Performans ve ayar</span><span class="sxs-lookup"><span data-stu-id="64a77-247">Performance and tuning</span></span>  
<span data-ttu-id="64a77-248">Bkz: [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md) etkisi performans veri hareketlerini (kopyalama etkinliği) ve bunu iyileştirmek için çeşitli yollar hakkında önemli faktör öğrenin.</span><span class="sxs-lookup"><span data-stu-id="64a77-248">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64a77-249">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="64a77-249">Next steps</span></span>
<span data-ttu-id="64a77-250">Aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="64a77-250">See the following articles:</span></span>

* <span data-ttu-id="64a77-251">[Kopya etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak için adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="64a77-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
