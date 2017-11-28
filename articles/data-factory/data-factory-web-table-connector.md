---
title: Azure Data Factory kullanarak Web tablodan aaaMove veri | Microsoft Docs
description: "Azure Data Factory kullanarak bir Web tablosunda toomove verileri nasıl sayfa hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="c93b1-103">Azure Data Factory kullanarak bir Web tablo kaynağından veri taşıma</span><span class="sxs-lookup"><span data-stu-id="c93b1-103">Move data from a Web table source using Azure Data Factory</span></span>
<span data-ttu-id="c93b1-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove verileri bir Web sayfası tooa tabloda havuz veri deposu desteklenen özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="c93b1-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from a table in a Web page tooa supported sink data store.</span></span> <span data-ttu-id="c93b1-105">Bu makale üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale listesiyle kopyalama etkinliği ve hello kaynakları/havuzlarını desteklenen veri depoları veri taşıma genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="c93b1-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="c93b1-106">Veri Fabrikası şu anda yalnızca bir Web tablo tooother verilerden veri taşımayı depolar, ancak verileri diğer veriler taşıma değil tooa Web tablosu hedef depolar destekler.</span><span class="sxs-lookup"><span data-stu-id="c93b1-106">Data factory currently supports only moving data from a Web table tooother data stores, but not moving data from other data stores tooa Web table destination.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c93b1-107">Bu Web bağlayıcı şu anda bir HTML sayfasından yalnızca ayıklanan tablo içeriği destekler.</span><span class="sxs-lookup"><span data-stu-id="c93b1-107">This Web connector currently supports only extracting table content from an HTML page.</span></span> <span data-ttu-id="c93b1-108">bir HTTP/s uç noktası tooretrieve verileri kullan [HTTP Bağlayıcısı](data-factory-http-connector.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="c93b1-108">tooretrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c93b1-109">Başlarken</span><span class="sxs-lookup"><span data-stu-id="c93b1-109">Getting started</span></span>
<span data-ttu-id="c93b1-110">Farklı araçlar/API'lerini kullanarak bir şirket içi Cassandra veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c93b1-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="c93b1-111">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="c93b1-111">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="c93b1-112">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="c93b1-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="c93b1-113">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="c93b1-113">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c93b1-114">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="c93b1-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="c93b1-115">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c93b1-115">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="c93b1-116">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="c93b1-116">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="c93b1-117">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="c93b1-117">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="c93b1-118">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="c93b1-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="c93b1-119">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c93b1-119">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="c93b1-120">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c93b1-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="c93b1-121">Bir web tablodan kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: Web tablo tooAzure Blob veri kopyalama](#json-example-copy-data-from-web-table-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="c93b1-121">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a web table, see [JSON example: Copy data from Web table tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="c93b1-122">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooa Web tablosunun JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="c93b1-122">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c93b1-123">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="c93b1-123">Linked service properties</span></span>
<span data-ttu-id="c93b1-124">Aşağıdaki tablonun hello JSON öğeleri belirli tooWeb bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="c93b1-124">hello following table provides description for JSON elements specific tooWeb linked service.</span></span>

| <span data-ttu-id="c93b1-125">Özellik</span><span class="sxs-lookup"><span data-stu-id="c93b1-125">Property</span></span> | <span data-ttu-id="c93b1-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c93b1-126">Description</span></span> | <span data-ttu-id="c93b1-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c93b1-127">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c93b1-128">type</span><span class="sxs-lookup"><span data-stu-id="c93b1-128">type</span></span> |<span data-ttu-id="c93b1-129">Merhaba type özelliği ayarlanmalıdır: **Web**</span><span class="sxs-lookup"><span data-stu-id="c93b1-129">hello type property must be set to: **Web**</span></span> |<span data-ttu-id="c93b1-130">Evet</span><span class="sxs-lookup"><span data-stu-id="c93b1-130">Yes</span></span> |
| <span data-ttu-id="c93b1-131">Url</span><span class="sxs-lookup"><span data-stu-id="c93b1-131">Url</span></span> |<span data-ttu-id="c93b1-132">URL toohello Web kaynağı</span><span class="sxs-lookup"><span data-stu-id="c93b1-132">URL toohello Web source</span></span> |<span data-ttu-id="c93b1-133">Evet</span><span class="sxs-lookup"><span data-stu-id="c93b1-133">Yes</span></span> |
| <span data-ttu-id="c93b1-134">authenticationType</span><span class="sxs-lookup"><span data-stu-id="c93b1-134">authenticationType</span></span> |<span data-ttu-id="c93b1-135">Anonim.</span><span class="sxs-lookup"><span data-stu-id="c93b1-135">Anonymous.</span></span> |<span data-ttu-id="c93b1-136">Evet</span><span class="sxs-lookup"><span data-stu-id="c93b1-136">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="c93b1-137">Anonim kimlik doğrulamasını kullanma</span><span class="sxs-lookup"><span data-stu-id="c93b1-137">Using Anonymous authentication</span></span>

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="c93b1-138">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="c93b1-138">Dataset properties</span></span>
<span data-ttu-id="c93b1-139">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c93b1-139">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c93b1-140">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="c93b1-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="c93b1-141">Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c93b1-141">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="c93b1-142">Merhaba typeProperties bölüm türü veri kümesi için **WebTable** hello aşağıdaki özelliklere sahip</span><span class="sxs-lookup"><span data-stu-id="c93b1-142">hello typeProperties section for dataset of type **WebTable** has hello following properties</span></span>

| <span data-ttu-id="c93b1-143">Özellik</span><span class="sxs-lookup"><span data-stu-id="c93b1-143">Property</span></span> | <span data-ttu-id="c93b1-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c93b1-144">Description</span></span> | <span data-ttu-id="c93b1-145">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c93b1-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c93b1-146">type</span><span class="sxs-lookup"><span data-stu-id="c93b1-146">type</span></span> |<span data-ttu-id="c93b1-147">Merhaba veri kümesi türü.</span><span class="sxs-lookup"><span data-stu-id="c93b1-147">type of hello dataset.</span></span> <span data-ttu-id="c93b1-148">çok ayarlanmalıdır**WebTable**</span><span class="sxs-lookup"><span data-stu-id="c93b1-148">must be set too**WebTable**</span></span> |<span data-ttu-id="c93b1-149">Evet</span><span class="sxs-lookup"><span data-stu-id="c93b1-149">Yes</span></span> |
| <span data-ttu-id="c93b1-150">Yol</span><span class="sxs-lookup"><span data-stu-id="c93b1-150">path</span></span> |<span data-ttu-id="c93b1-151">Merhaba tablo içeren bir göreli URL toohello kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="c93b1-151">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="c93b1-152">Hayır.</span><span class="sxs-lookup"><span data-stu-id="c93b1-152">No.</span></span> <span data-ttu-id="c93b1-153">Yol belirtilmediğinde hello bağlantılı hizmet tanımında belirtilen yalnızca hello URL'si kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c93b1-153">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="c93b1-154">Dizin</span><span class="sxs-lookup"><span data-stu-id="c93b1-154">index</span></span> |<span data-ttu-id="c93b1-155">hello kaynak hello tabloda başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="c93b1-155">hello index of hello table in hello resource.</span></span> <span data-ttu-id="c93b1-156">Bkz: [bir HTML sayfasında tablosunun Get dizini](#get-index-of-a-table-in-an-html-page) HTML sayfası bir tablodaki adımları toogetting dizini için bölüm.</span><span class="sxs-lookup"><span data-stu-id="c93b1-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="c93b1-157">Evet</span><span class="sxs-lookup"><span data-stu-id="c93b1-157">Yes</span></span> |

<span data-ttu-id="c93b1-158">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="c93b1-158">**Example:**</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="c93b1-159">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="c93b1-159">Copy activity properties</span></span>
<span data-ttu-id="c93b1-160">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c93b1-160">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c93b1-161">Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c93b1-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="c93b1-162">Oysa hello typeProperties bölümünde hello etkinlik özellikleri her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="c93b1-162">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="c93b1-163">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="c93b1-163">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="c93b1-164">Şu anda kopyalama etkinliği hello kaynağında olduğunda türü **WebSource**, hiçbir ek özellikler desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c93b1-164">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a><span data-ttu-id="c93b1-165">JSON örnek: Web tablo tooAzure Blob veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="c93b1-165">JSON example: Copy data from Web table tooAzure Blob</span></span>
<span data-ttu-id="c93b1-166">Merhaba, aşağıdaki örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="c93b1-166">hello following sample shows:</span></span>

1. <span data-ttu-id="c93b1-167">Bağlı hizmet türü [Web](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c93b1-167">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="c93b1-168">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c93b1-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="c93b1-169">Bir giriş [dataset](data-factory-create-datasets.md) türü [WebTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c93b1-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="c93b1-170">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c93b1-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="c93b1-171">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [WebSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c93b1-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c93b1-172">Merhaba örnek verileri saatte bir Web tablo tooan Azure blob kopyalar.</span><span class="sxs-lookup"><span data-stu-id="c93b1-172">hello sample copies data from a Web table tooan Azure blob every hour.</span></span> <span data-ttu-id="c93b1-173">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c93b1-173">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="c93b1-174">Aşağıdaki örnek hello nasıl toocopy verileri bir Web tablo tooan Azure blob'tan gösterir.</span><span class="sxs-lookup"><span data-stu-id="c93b1-174">hello following sample shows how toocopy data from a Web table tooan Azure blob.</span></span> <span data-ttu-id="c93b1-175">İçinde belirtilen hello hello tooany havuzlarını doğrudan veri ancak kopyalanabilir [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) hello kopya etkinliği Azure Data Factory kullanarak makale.</span><span class="sxs-lookup"><span data-stu-id="c93b1-175">However, data can be copied directly tooany of hello sinks stated in hello [Data Movement Activities](data-factory-data-movement-activities.md) article by using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="c93b1-176">**Web hizmeti bağlı** kullanan Web hello Bu örnek anonim kimlik doğrulaması ile bağlı.</span><span class="sxs-lookup"><span data-stu-id="c93b1-176">**Web linked service** This example uses hello Web linked service with anonymous authentication.</span></span> <span data-ttu-id="c93b1-177">Bkz: [Web bağlantılı hizmeti](#linked-service-properties) bölümü için farklı tür kimlik doğrulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c93b1-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="c93b1-178">**Azure Storage bağlı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="c93b1-178">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="c93b1-179">**WebTable girdi veri kümesi** ayarı **dış** çok**true** hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello bir etkinlik tarafından üretilen değil bildirir Veri Fabrikası.</span><span class="sxs-lookup"><span data-stu-id="c93b1-179">**WebTable input dataset** Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="c93b1-180">Bkz: [bir HTML sayfasında tablosunun Get dizini](#get-index-of-a-table-in-an-html-page) HTML sayfası bir tablodaki adımları toogetting dizini için bölüm.</span><span class="sxs-lookup"><span data-stu-id="c93b1-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span>  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


<span data-ttu-id="c93b1-181">**Azure Blob dataset çıktı**</span><span class="sxs-lookup"><span data-stu-id="c93b1-181">**Azure Blob output dataset**</span></span>

<span data-ttu-id="c93b1-182">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="c93b1-182">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```



<span data-ttu-id="c93b1-183">**Kopyalama etkinliği ile kanalı**</span><span class="sxs-lookup"><span data-stu-id="c93b1-183">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="c93b1-184">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="c93b1-184">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="c93b1-185">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**WebSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c93b1-185">In hello pipeline JSON definition, hello **source** type is set too**WebSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="c93b1-186">Bkz: [WebSource türü özellikleri](#copy-activity-type-properties) hello WebSource hello tarafından desteklenen özelliklerin listesi için.</span><span class="sxs-lookup"><span data-stu-id="c93b1-186">See [WebSource type properties](#copy-activity-type-properties) for hello list of properties supported by hello WebSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
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

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="c93b1-187">Bir HTML sayfasında bir tablonun dizini alma</span><span class="sxs-lookup"><span data-stu-id="c93b1-187">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="c93b1-188">Başlatma **Excel 2016** ve toohello anahtar **veri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="c93b1-188">Launch **Excel 2016** and switch toohello **Data** tab.</span></span>  
2. <span data-ttu-id="c93b1-189">Tıklatın **yeni sorgu** hello araç çubuğunda, çok noktası**diğer kaynaklardan** tıklatıp **Web'den**.</span><span class="sxs-lookup"><span data-stu-id="c93b1-189">Click **New Query** on hello toolbar, point too**From Other Sources** and click **From Web**.</span></span>

    ![Power Query menüsü](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="c93b1-191">Merhaba, **Web'den** iletişim kutusunda, girin **URL** bağlantılı hizmeti JSON içinde kullanırsınız (örneğin: https://en.wikipedia.org/wiki/) yolu belirtin hello veri kümesi için birlikte (örneğin: AFI % 27s_100_Years... 100_Movies) tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="c93b1-191">In hello **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for hello dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![Web iletişim kutusundan](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="c93b1-193">Bu örnekte kullanılan URL: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="c93b1-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="c93b1-194">Görürseniz **erişim Web içeriği** iletişim kutusu, select hello sağ **URL**, **kimlik doğrulaması**, tıklatıp **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="c93b1-194">If you see **Access Web content** dialog box, select hello right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Web içerik iletişim kutusuna erişin](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="c93b1-196">Tıklatın bir **tablo** öğesi hello ağaç görünümü toosee içerik hello tablosundan ve ardından **Düzenle** hello altındaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c93b1-196">Click a **table** item in hello tree view toosee content from hello table and then click **Edit** button at hello bottom.</span></span>  

   ![Gezgin iletişim](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="c93b1-198">Merhaba, **sorgu Düzenleyicisi'ni** penceresinde tıklatın **Gelişmiş Düzenleyici** hello araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="c93b1-198">In hello **Query Editor** window, click **Advanced Editor** button on hello toolbar.</span></span>

    ![Gelişmiş Düzenleyici düğmesi](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="c93b1-200">Sayı Hello Gelişmiş Düzenleyicisi iletişim kutusunda hello sonraki çok "Kaynak" Merhaba dizinidir.</span><span class="sxs-lookup"><span data-stu-id="c93b1-200">In hello Advanced Editor dialog box, hello number next too"Source" is hello index.</span></span>

    ![Düzenleyicisi - Gelişmiş dizin](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="c93b1-202">Excel 2013 kullanıyorsanız, [Excel için Microsoft Power Query](https://www.microsoft.com/download/details.aspx?id=39379) tooget başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="c93b1-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget hello index.</span></span> <span data-ttu-id="c93b1-203">Bkz: [Bağlan tooa web sayfası](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="c93b1-203">See [Connect tooa web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="c93b1-204">Merhaba adımlardır kullanıyorsanız benzer [Masaüstü için Microsoft Power BI](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="c93b1-204">hello steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> <span data-ttu-id="c93b1-205">Kaynak veri kümesi toocolumns havuz kümesinden toomap sütunlarından bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c93b1-205">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c93b1-206">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="c93b1-206">Performance and Tuning</span></span>
<span data-ttu-id="c93b1-207">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="c93b1-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
