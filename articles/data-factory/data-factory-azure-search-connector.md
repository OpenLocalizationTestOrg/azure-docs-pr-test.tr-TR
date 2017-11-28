---
title: "Veri Fabrikası kullanarak aaaPush veri tooSearch dizini | Microsoft Docs"
description: "Hakkında bilgi edinin Azure Data Factory kullanarak toopush veri tooAzure arama dizini."
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
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="d9199-103">Azure Data Factory kullanarak veri tooan Azure Search dizini bildirme</span><span class="sxs-lookup"><span data-stu-id="d9199-103">Push data tooan Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="d9199-104">Bu makalede nasıl toouse hello kopyalama etkinliği toopush verileri bir desteklenen kaynak verilerinden tooAzure arama dizini depolamak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d9199-104">This article describes how toouse hello Copy Activity toopush data from a supported source data store tooAzure Search index.</span></span> <span data-ttu-id="d9199-105">Desteklenen kaynak veri depolarına hello Kaynak sütununda hello listelenen [desteklenen kaynakları ve havuzlarını](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="d9199-105">Supported source data stores are listed in hello Source column of hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="d9199-106">Bu makale üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) desteklenen veri deposu birleşimleri kopyalama etkinliği ile veri taşıma için genel bir bakış sunan makalesi.</span><span class="sxs-lookup"><span data-stu-id="d9199-106">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="d9199-107">Bağlantıyı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d9199-107">Enabling connectivity</span></span>
<span data-ttu-id="d9199-108">tooallow Data Factory hizmetine bağlanmak tooan şirket içi veri depolama, veri yönetimi ağ geçidi, şirket içi ortamınızda yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d9199-108">tooallow Data Factory service connect tooan on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="d9199-109">Ağ geçidi üzerinde hello kaynak verilerini barındıran aynı makine depolamak ya da hello veri kaynakları için rekabete ayrı makine tooavoid depolamak hello yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9199-109">You can install gateway on hello same machine that hosts hello source data store or on a separate machine tooavoid competing for resources with hello data store.</span></span>

<span data-ttu-id="d9199-110">Veri Yönetimi ağ geçidi şirket içi veri kaynakları toocloud Hizmetleri güvenli ve yönetilen bir şekilde birbirine bağlayan.</span><span class="sxs-lookup"><span data-stu-id="d9199-110">Data Management Gateway connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="d9199-111">Bkz: [şirket içi ve bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale veri yönetimi ağ geçidi hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="d9199-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d9199-112">Başlarken</span><span class="sxs-lookup"><span data-stu-id="d9199-112">Getting started</span></span>
<span data-ttu-id="d9199-113">Farklı araçlar/API'lerini kullanarak bir kaynak veri deposu tooAzure arama dizinden veri iter kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d9199-113">You can create a pipeline with a copy activity that pushes data from a source data store tooAzure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="d9199-114">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="d9199-114">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="d9199-115">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="d9199-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="d9199-116">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="d9199-116">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d9199-117">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="d9199-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="d9199-118">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d9199-118">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="d9199-119">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="d9199-119">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="d9199-120">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="d9199-120">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="d9199-121">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="d9199-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="d9199-122">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d9199-122">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="d9199-123">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="d9199-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="d9199-124">Kullanılan toocopy veri tooAzure arama dizini olan Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: şirket içi SQL Server tooAzure arama dizinden veri kopyalama](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="d9199-124">For a sample with JSON definitions for Data Factory entities that are used toocopy data tooAzure Search index, see [JSON example: Copy data from on-premises SQL Server tooAzure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="d9199-125">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooAzure arama dizini olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="d9199-125">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d9199-126">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="d9199-126">Linked service properties</span></span>

<span data-ttu-id="d9199-127">Aşağıdaki tablonun hello belirli toohello bağlı Azure Search Hizmeti JSON öğeleri için açıklamalar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="d9199-127">hello following table provides descriptions for JSON elements that are specific toohello Azure Search linked service.</span></span>

| <span data-ttu-id="d9199-128">Özellik</span><span class="sxs-lookup"><span data-stu-id="d9199-128">Property</span></span> | <span data-ttu-id="d9199-129">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d9199-129">Description</span></span> | <span data-ttu-id="d9199-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d9199-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="d9199-131">type</span><span class="sxs-lookup"><span data-stu-id="d9199-131">type</span></span> | <span data-ttu-id="d9199-132">Merhaba type özelliği ayarlanmalıdır: **AzureSearch**.</span><span class="sxs-lookup"><span data-stu-id="d9199-132">hello type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="d9199-133">Evet</span><span class="sxs-lookup"><span data-stu-id="d9199-133">Yes</span></span> |
| <span data-ttu-id="d9199-134">URL</span><span class="sxs-lookup"><span data-stu-id="d9199-134">url</span></span> | <span data-ttu-id="d9199-135">Hello Azure Search hizmeti için URL.</span><span class="sxs-lookup"><span data-stu-id="d9199-135">URL for hello Azure Search service.</span></span> | <span data-ttu-id="d9199-136">Evet</span><span class="sxs-lookup"><span data-stu-id="d9199-136">Yes</span></span> |
| <span data-ttu-id="d9199-137">anahtar</span><span class="sxs-lookup"><span data-stu-id="d9199-137">key</span></span> | <span data-ttu-id="d9199-138">Hello Azure Search hizmeti için yönetici anahtarı.</span><span class="sxs-lookup"><span data-stu-id="d9199-138">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="d9199-139">Evet</span><span class="sxs-lookup"><span data-stu-id="d9199-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="d9199-140">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="d9199-140">Dataset properties</span></span>

<span data-ttu-id="d9199-141">Merhaba bölümler ve veri kümelerini tanımlamak için kullanılabilir olan özellikleri tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="d9199-141">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d9199-142">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri kümesi türleri için benzerdir.</span><span class="sxs-lookup"><span data-stu-id="d9199-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="d9199-143">Merhaba **typeProperties** bölümü, her veri kümesi türü için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="d9199-143">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="d9199-144">Merhaba typeProperties bölümünde hello türü veri kümesi için **AzureSearchIndex** hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d9199-144">hello typeProperties section for a dataset of hello type **AzureSearchIndex** has hello following properties:</span></span>

| <span data-ttu-id="d9199-145">Özellik</span><span class="sxs-lookup"><span data-stu-id="d9199-145">Property</span></span> | <span data-ttu-id="d9199-146">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d9199-146">Description</span></span> | <span data-ttu-id="d9199-147">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d9199-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="d9199-148">type</span><span class="sxs-lookup"><span data-stu-id="d9199-148">type</span></span> | <span data-ttu-id="d9199-149">Merhaba type özelliği çok ayarlanmalıdır**AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="d9199-149">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="d9199-150">Evet</span><span class="sxs-lookup"><span data-stu-id="d9199-150">Yes</span></span> |
| <span data-ttu-id="d9199-151">indexName</span><span class="sxs-lookup"><span data-stu-id="d9199-151">indexName</span></span> | <span data-ttu-id="d9199-152">Hello Azure Search dizini adı.</span><span class="sxs-lookup"><span data-stu-id="d9199-152">Name of hello Azure Search index.</span></span> <span data-ttu-id="d9199-153">Veri Fabrikası hello dizin oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="d9199-153">Data Factory does not create hello index.</span></span> <span data-ttu-id="d9199-154">Başlangıç dizini, Azure Search'te mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9199-154">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="d9199-155">Evet</span><span class="sxs-lookup"><span data-stu-id="d9199-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="d9199-156">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="d9199-156">Copy activity properties</span></span>
<span data-ttu-id="d9199-157">Merhaba bölümler ve etkinlikleri tanımlamak için kullanılabilir olan özellikleri tam listesi için bkz [ardışık düzen oluşturma](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="d9199-157">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d9199-158">Ad, açıklama, giriş ve çıkış tabloları ve çeşitli ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d9199-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="d9199-159">Oysa her etkinlik türü ile Merhaba typeProperties bölümündeki özellikler değişir.</span><span class="sxs-lookup"><span data-stu-id="d9199-159">Whereas, properties available in hello typeProperties section vary with each activity type.</span></span> <span data-ttu-id="d9199-160">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="d9199-160">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="d9199-161">Kopyalama hello havuz hello türü olduğunda etkinliği için **AzureSearchIndexSink**, aşağıdaki özelliklere hello typeProperties bölümünde bulunur:</span><span class="sxs-lookup"><span data-stu-id="d9199-161">For Copy Activity, when hello sink is of hello type **AzureSearchIndexSink**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="d9199-162">Özellik</span><span class="sxs-lookup"><span data-stu-id="d9199-162">Property</span></span> | <span data-ttu-id="d9199-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d9199-163">Description</span></span> | <span data-ttu-id="d9199-164">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="d9199-164">Allowed values</span></span> | <span data-ttu-id="d9199-165">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d9199-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="d9199-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="d9199-166">WriteBehavior</span></span> | <span data-ttu-id="d9199-167">Toomerge veya Değiştir bir belgeyi açtığında hello dizinde zaten olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d9199-167">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> <span data-ttu-id="d9199-168">Merhaba bkz [WriteBehavior özelliği](#writebehavior-property).</span><span class="sxs-lookup"><span data-stu-id="d9199-168">See hello [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="d9199-169">Merge (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="d9199-169">Merge (default)</span></span><br/><span data-ttu-id="d9199-170">Karşıya Yükle</span><span class="sxs-lookup"><span data-stu-id="d9199-170">Upload</span></span>| <span data-ttu-id="d9199-171">Hayır</span><span class="sxs-lookup"><span data-stu-id="d9199-171">No</span></span> |
| <span data-ttu-id="d9199-172">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="d9199-172">WriteBatchSize</span></span> | <span data-ttu-id="d9199-173">Hello arabellek boyutu writeBatchSize ulaştığında hello Azure Search dizinine veri yükler.</span><span class="sxs-lookup"><span data-stu-id="d9199-173">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="d9199-174">Merhaba bkz [WriteBatchSize özelliği](#writebatchsize-property) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="d9199-174">See hello [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="d9199-175">1 too1, 000.</span><span class="sxs-lookup"><span data-stu-id="d9199-175">1 too1,000.</span></span> <span data-ttu-id="d9199-176">Varsayılan değer 1000'dir.</span><span class="sxs-lookup"><span data-stu-id="d9199-176">Default value is 1000.</span></span> | <span data-ttu-id="d9199-177">Hayır</span><span class="sxs-lookup"><span data-stu-id="d9199-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="d9199-178">WriteBehavior özelliği</span><span class="sxs-lookup"><span data-stu-id="d9199-178">WriteBehavior property</span></span>
<span data-ttu-id="d9199-179">Verileri yazarken AzureSearchSink upserts.</span><span class="sxs-lookup"><span data-stu-id="d9199-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="d9199-180">Diğer bir deyişle, hello belge anahtarını hello Azure Search dizini zaten varsa bir belge yazarken, Azure Search çakışma özel durum atma yerine hello var olan bir belgeyi güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="d9199-180">In other words, when writing a document, if hello document key already exists in hello Azure Search index, Azure Search updates hello existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="d9199-181">Merhaba AzureSearchSink (AzureSearch SDK kullanılarak) iki upsert davranışları aşağıdaki hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="d9199-181">hello AzureSearchSink provides hello following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="d9199-182">**Birleştirme**: hello yeni belgedeki tüm hello sütunları bir varolan hello ile birleştirin.</span><span class="sxs-lookup"><span data-stu-id="d9199-182">**Merge**: combine all hello columns in hello new document with hello existing one.</span></span> <span data-ttu-id="d9199-183">Null değer hello yeni belge bulunan sütunlar için var olan bir hello hello değeri korunur.</span><span class="sxs-lookup"><span data-stu-id="d9199-183">For columns with null value in hello new document, hello value in hello existing one is preserved.</span></span>
- <span data-ttu-id="d9199-184">**Karşıya yükleme**: hello varolan bir hello yeni belge değiştirir.</span><span class="sxs-lookup"><span data-stu-id="d9199-184">**Upload**: hello new document replaces hello existing one.</span></span> <span data-ttu-id="d9199-185">Bulunup bulunmadığını değeri null olmayan hello mevcut belgede veya hello yeni belgede belirtilmeyen sütunlar için toonull hello değer ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d9199-185">For columns not specified in hello new document, hello value is set toonull whether there is a non-null value in hello existing document or not.</span></span>

<span data-ttu-id="d9199-186">Merhaba varsayılan davranışı **birleştirme**.</span><span class="sxs-lookup"><span data-stu-id="d9199-186">hello default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="d9199-187">WriteBatchSize özelliği</span><span class="sxs-lookup"><span data-stu-id="d9199-187">WriteBatchSize Property</span></span>
<span data-ttu-id="d9199-188">Azure Search Hizmeti yazma belgeleri toplu iş olarak destekler.</span><span class="sxs-lookup"><span data-stu-id="d9199-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="d9199-189">Bir toplu 1 too1, 000 eylemler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="d9199-189">A batch can contain 1 too1,000 Actions.</span></span> <span data-ttu-id="d9199-190">Bir eylem, bir belge tooperform hello karşıya yükleme/birleştirme işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="d9199-190">An action handles one document tooperform hello upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="d9199-191">Veri türü desteği</span><span class="sxs-lookup"><span data-stu-id="d9199-191">Data type support</span></span>
<span data-ttu-id="d9199-192">Merhaba aşağıdaki tabloda bir Azure Search veri türü veya desteklenip desteklenmediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="d9199-192">hello following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="d9199-193">Azure arama veri türü</span><span class="sxs-lookup"><span data-stu-id="d9199-193">Azure Search data type</span></span> | <span data-ttu-id="d9199-194">Azure arama havuzunda desteklenir</span><span class="sxs-lookup"><span data-stu-id="d9199-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="d9199-195">Dize</span><span class="sxs-lookup"><span data-stu-id="d9199-195">String</span></span> | <span data-ttu-id="d9199-196">E</span><span class="sxs-lookup"><span data-stu-id="d9199-196">Y</span></span> |
| <span data-ttu-id="d9199-197">Int32</span><span class="sxs-lookup"><span data-stu-id="d9199-197">Int32</span></span> | <span data-ttu-id="d9199-198">E</span><span class="sxs-lookup"><span data-stu-id="d9199-198">Y</span></span> |
| <span data-ttu-id="d9199-199">Int64</span><span class="sxs-lookup"><span data-stu-id="d9199-199">Int64</span></span> | <span data-ttu-id="d9199-200">E</span><span class="sxs-lookup"><span data-stu-id="d9199-200">Y</span></span> |
| <span data-ttu-id="d9199-201">Çift</span><span class="sxs-lookup"><span data-stu-id="d9199-201">Double</span></span> | <span data-ttu-id="d9199-202">E</span><span class="sxs-lookup"><span data-stu-id="d9199-202">Y</span></span> |
| <span data-ttu-id="d9199-203">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="d9199-203">Boolean</span></span> | <span data-ttu-id="d9199-204">E</span><span class="sxs-lookup"><span data-stu-id="d9199-204">Y</span></span> |
| <span data-ttu-id="d9199-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="d9199-205">DataTimeOffset</span></span> | <span data-ttu-id="d9199-206">E</span><span class="sxs-lookup"><span data-stu-id="d9199-206">Y</span></span> |
| <span data-ttu-id="d9199-207">Dize dizisi</span><span class="sxs-lookup"><span data-stu-id="d9199-207">String Array</span></span> | <span data-ttu-id="d9199-208">N</span><span class="sxs-lookup"><span data-stu-id="d9199-208">N</span></span> |
| <span data-ttu-id="d9199-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="d9199-209">GeographyPoint</span></span> | <span data-ttu-id="d9199-210">N</span><span class="sxs-lookup"><span data-stu-id="d9199-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a><span data-ttu-id="d9199-211">JSON örnek: şirket içi SQL Server tooAzure arama dizinden veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="d9199-211">JSON example: Copy data from on-premises SQL Server tooAzure Search index</span></span>

<span data-ttu-id="d9199-212">Merhaba, aşağıdaki örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="d9199-212">hello following sample shows:</span></span>

1.  <span data-ttu-id="d9199-213">Bağlı hizmet türü [AzureSearch](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d9199-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="d9199-214">Bağlı hizmet türü [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d9199-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="d9199-215">Bir giriş [dataset](data-factory-create-datasets.md) türü [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d9199-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="d9199-216">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureSearchIndex](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d9199-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="d9199-217">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) ve [AzureSearchIndexSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d9199-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="d9199-218">Merhaba örnek time series verilerini saatlik bir şirket içi SQL Server veritabanı tooan Azure Search dizini kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d9199-218">hello sample copies time-series data from an on-premises SQL Server database tooan Azure Search index hourly.</span></span> <span data-ttu-id="d9199-219">Bu örnekte kullanılan JSON özellikleri hello hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d9199-219">hello JSON properties used in this sample are described in sections following hello samples.</span></span>

<span data-ttu-id="d9199-220">İlk adım olarak, şirket içi makinenizde hello veri yönetimi ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d9199-220">As a first step, setup hello data management gateway on your on-premises machine.</span></span> <span data-ttu-id="d9199-221">Merhaba yönergelerdir hello [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="d9199-221">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="d9199-222">**Azure arama bağlantılı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="d9199-222">**Azure Search linked service:**</span></span>

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

<span data-ttu-id="d9199-223">**SQL Server bağlantılı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="d9199-223">**SQL Server linked service**</span></span>

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

<span data-ttu-id="d9199-224">**SQL Server girdi veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="d9199-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="d9199-225">Merhaba örnek SQL Server'da bir tablo "MyTable" oluşturulur ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="d9199-225">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="d9199-226">Tek bir veri kümesi, ancak tek bir tabloyu kullanarak aynı veritabanı hello veri kümesi'nin tableName typeProperty için kullanılması gereken hello içinde birden çok tablo üzerinde sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9199-226">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="d9199-227">"Dış" ayarı: "true" bildirir Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="d9199-227">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="d9199-228">**Azure Search'te veri kümesini çıktı:**</span><span class="sxs-lookup"><span data-stu-id="d9199-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="d9199-229">Merhaba örnek kopya veri tooan Azure Search dizini adlı **ürünleri**.</span><span class="sxs-lookup"><span data-stu-id="d9199-229">hello sample copies data tooan Azure Search index named **products**.</span></span> <span data-ttu-id="d9199-230">Veri Fabrikası hello dizin oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="d9199-230">Data Factory does not create hello index.</span></span> <span data-ttu-id="d9199-231">tootest hello örnek, bu ada sahip bir dizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d9199-231">tootest hello sample, create an index with this name.</span></span> <span data-ttu-id="d9199-232">Hello Azure Search dizini oluşturma hello ile aynı sayıda sütun olduğu gibi hello girdi veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="d9199-232">Create hello Azure Search index with hello same number of columns as in hello input dataset.</span></span> <span data-ttu-id="d9199-233">Yeni girişler toohello Azure Search dizini saatte eklenir.</span><span class="sxs-lookup"><span data-stu-id="d9199-233">New entries are added toohello Azure Search index every hour.</span></span>

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

<span data-ttu-id="d9199-234">**SQL kaynak ve Azure Search dizini havuz ile ardışık düzeninde etkinlik kopyalayın:**</span><span class="sxs-lookup"><span data-stu-id="d9199-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="d9199-235">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="d9199-235">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="d9199-236">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**SqlSource** ve **havuz** türü olarak ayarlanmış çok**AzureSearchIndexSink**.</span><span class="sxs-lookup"><span data-stu-id="d9199-236">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**AzureSearchIndexSink**.</span></span> <span data-ttu-id="d9199-237">Merhaba belirtilen hello SQL sorgusu **SqlReaderQuery** özelliği saat toocopy geçmiş hello hello veri seçer.</span><span class="sxs-lookup"><span data-stu-id="d9199-237">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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

<span data-ttu-id="d9199-238">Azure Search bir bulut veri deposundan veri kopyalıyorsanız `executionLocation` özelliği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d9199-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="d9199-239">Merhaba aşağıdaki JSON parçacığı gösterir kopyalama etkinliği altında gerekli hello değişiklik `typeProperties` bir örnek olarak.</span><span class="sxs-lookup"><span data-stu-id="d9199-239">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="d9199-240">Denetleme [bulut veri depoları arasında veri kopyalama](data-factory-data-movement-activities.md#global) desteklenen değerler ve daha fazla ayrıntı için bölüm.</span><span class="sxs-lookup"><span data-stu-id="d9199-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

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


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="d9199-241">Bir bulut kaynaktan kopyalama</span><span class="sxs-lookup"><span data-stu-id="d9199-241">Copy from a cloud source</span></span>
<span data-ttu-id="d9199-242">Azure Search bir bulut veri deposundan veri kopyalıyorsanız `executionLocation` özelliği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d9199-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="d9199-243">Merhaba aşağıdaki JSON parçacığı gösterir kopyalama etkinliği altında gerekli hello değişiklik `typeProperties` bir örnek olarak.</span><span class="sxs-lookup"><span data-stu-id="d9199-243">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="d9199-244">Denetleme [bulut veri depoları arasında veri kopyalama](data-factory-data-movement-activities.md#global) desteklenen değerler ve daha fazla ayrıntı için bölüm.</span><span class="sxs-lookup"><span data-stu-id="d9199-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

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

<span data-ttu-id="d9199-245">Ayrıca, kaynak veri kümesi toocolumns hello kopyalama etkinliği tanımında havuz kümesinden sütunlarından eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9199-245">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="d9199-246">Ayrıntılar için bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="d9199-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="d9199-247">Performans ve ayar</span><span class="sxs-lookup"><span data-stu-id="d9199-247">Performance and tuning</span></span>  
<span data-ttu-id="d9199-248">Merhaba bkz [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler veri taşıma (kopyalama etkinliği), o etki performansını ve çeşitli yolları toooptimize onu.</span><span class="sxs-lookup"><span data-stu-id="d9199-248">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9199-249">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d9199-249">Next steps</span></span>
<span data-ttu-id="d9199-250">Aşağıdaki makaleleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="d9199-250">See hello following articles:</span></span>

* <span data-ttu-id="d9199-251">[Kopya etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak için adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="d9199-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
