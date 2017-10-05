---
title: "Azure Data Factory kullanarak Web tablodan veri taşıma | Microsoft Docs"
description: "Azure Data Factory kullanarak bir Web sayfası bir tablodaki veri taşıma hakkında bilgi edinin."
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
ms.openlocfilehash: 9e006bc7289fa0239f1650ac6ad43dd159e3c7e0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="818ad-103">Azure Data Factory kullanarak bir Web tablo kaynağından veri taşıma</span><span class="sxs-lookup"><span data-stu-id="818ad-103">Move data from a Web table source using Azure Data Factory</span></span>
<span data-ttu-id="818ad-104">Bu makalede kopya etkinliği Azure Data Factory'de bir desteklenen havuz veri deposuna bir Web sayfasında bir tablodan veri taşımak için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="818ad-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from a table in a Web page to a supported sink data store.</span></span> <span data-ttu-id="818ad-105">Bu makalede derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale kopyalama etkinliği ve kaynakları/havuzlarını desteklenen veri depoları listesi ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="818ad-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="818ad-106">Veri Fabrikası şu anda yalnızca veri taşımayı Web tablodan diğer veri depolarına destekler, ancak verileri diğer veriler taşıma olmayan bir Web tablo hedefine depolar.</span><span class="sxs-lookup"><span data-stu-id="818ad-106">Data factory currently supports only moving data from a Web table to other data stores, but not moving data from other data stores to a Web table destination.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="818ad-107">Bu Web bağlayıcı şu anda bir HTML sayfasından yalnızca ayıklanan tablo içeriği destekler.</span><span class="sxs-lookup"><span data-stu-id="818ad-107">This Web connector currently supports only extracting table content from an HTML page.</span></span> <span data-ttu-id="818ad-108">Bir HTTP/s uç noktasından verileri almak için kullanmak [HTTP Bağlayıcısı](data-factory-http-connector.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="818ad-108">To retrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span></span>

## <a name="getting-started"></a><span data-ttu-id="818ad-109">Başlarken</span><span class="sxs-lookup"><span data-stu-id="818ad-109">Getting started</span></span>
<span data-ttu-id="818ad-110">Farklı araçlar/API'lerini kullanarak bir şirket içi Cassandra veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="818ad-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="818ad-111">Bir işlem hattı oluşturmak için en kolay yolu kullanmaktır **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="818ad-111">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="818ad-112">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) veri kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="818ad-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="818ad-113">Bir işlem hattı oluşturmak için aşağıdaki araçları kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu**, **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="818ad-113">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="818ad-114">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="818ad-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="818ad-115">Araçlar ya da API'leri kullanıp bir havuz veri deposu için bir kaynak veri deposundan verileri taşır bir ardışık düzen oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="818ad-115">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="818ad-116">Oluşturma **bağlantılı Hizmetleri** girdi ve çıktı verilerini bağlamak için veri fabrikanıza depolar.</span><span class="sxs-lookup"><span data-stu-id="818ad-116">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="818ad-117">Oluşturma **veri kümeleri** kopyalama işlemi için girdi ve çıktı verilerini temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="818ad-117">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="818ad-118">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="818ad-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="818ad-119">Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="818ad-119">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="818ad-120">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, JSON biçimini kullanarak bu Data Factory varlıklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="818ad-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="818ad-121">Bir web tablodan veri kopyalamak için kullanılan Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: veri kopyalama Web tablosundan Azure Blob](#json-example-copy-data-from-web-table-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="818ad-121">For a sample with JSON definitions for Data Factory entities that are used to copy data from a web table, see [JSON example: Copy data from Web table to Azure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="818ad-122">Aşağıdaki bölümler, Data Factory varlıklarını belirli bir Web tabloya tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="818ad-122">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="818ad-123">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="818ad-123">Linked service properties</span></span>
<span data-ttu-id="818ad-124">Aşağıdaki tabloda, JSON öğeleri Web bağlantılı hizmeti için belirli bir açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="818ad-124">The following table provides description for JSON elements specific to Web linked service.</span></span>

| <span data-ttu-id="818ad-125">Özellik</span><span class="sxs-lookup"><span data-stu-id="818ad-125">Property</span></span> | <span data-ttu-id="818ad-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="818ad-126">Description</span></span> | <span data-ttu-id="818ad-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="818ad-127">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="818ad-128">type</span><span class="sxs-lookup"><span data-stu-id="818ad-128">type</span></span> |<span data-ttu-id="818ad-129">Type özelliği ayarlanmalıdır: **Web**</span><span class="sxs-lookup"><span data-stu-id="818ad-129">The type property must be set to: **Web**</span></span> |<span data-ttu-id="818ad-130">Evet</span><span class="sxs-lookup"><span data-stu-id="818ad-130">Yes</span></span> |
| <span data-ttu-id="818ad-131">Url</span><span class="sxs-lookup"><span data-stu-id="818ad-131">Url</span></span> |<span data-ttu-id="818ad-132">Web kaynağı URL'si</span><span class="sxs-lookup"><span data-stu-id="818ad-132">URL to the Web source</span></span> |<span data-ttu-id="818ad-133">Evet</span><span class="sxs-lookup"><span data-stu-id="818ad-133">Yes</span></span> |
| <span data-ttu-id="818ad-134">authenticationType</span><span class="sxs-lookup"><span data-stu-id="818ad-134">authenticationType</span></span> |<span data-ttu-id="818ad-135">Anonim.</span><span class="sxs-lookup"><span data-stu-id="818ad-135">Anonymous.</span></span> |<span data-ttu-id="818ad-136">Evet</span><span class="sxs-lookup"><span data-stu-id="818ad-136">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="818ad-137">Anonim kimlik doğrulamasını kullanma</span><span class="sxs-lookup"><span data-stu-id="818ad-137">Using Anonymous authentication</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="818ad-138">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="818ad-138">Dataset properties</span></span>
<span data-ttu-id="818ad-139">Bölümler & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="818ad-139">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="818ad-140">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="818ad-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="818ad-141">**TypeProperties** bölüm veri kümesi her tür için farklıdır ve verilerin veri deposunda konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="818ad-141">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="818ad-142">TypeProperties bölüm türü veri kümesi için **WebTable** aşağıdaki özelliklere sahip</span><span class="sxs-lookup"><span data-stu-id="818ad-142">The typeProperties section for dataset of type **WebTable** has the following properties</span></span>

| <span data-ttu-id="818ad-143">Özellik</span><span class="sxs-lookup"><span data-stu-id="818ad-143">Property</span></span> | <span data-ttu-id="818ad-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="818ad-144">Description</span></span> | <span data-ttu-id="818ad-145">Gerekli</span><span class="sxs-lookup"><span data-stu-id="818ad-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="818ad-146">type</span><span class="sxs-lookup"><span data-stu-id="818ad-146">type</span></span> |<span data-ttu-id="818ad-147">Veri kümesi türü.</span><span class="sxs-lookup"><span data-stu-id="818ad-147">type of the dataset.</span></span> <span data-ttu-id="818ad-148">ayarlanmalıdır **WebTable**</span><span class="sxs-lookup"><span data-stu-id="818ad-148">must be set to **WebTable**</span></span> |<span data-ttu-id="818ad-149">Evet</span><span class="sxs-lookup"><span data-stu-id="818ad-149">Yes</span></span> |
| <span data-ttu-id="818ad-150">Yol</span><span class="sxs-lookup"><span data-stu-id="818ad-150">path</span></span> |<span data-ttu-id="818ad-151">Tabloyu içeren kaynak için göreli bir URL.</span><span class="sxs-lookup"><span data-stu-id="818ad-151">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="818ad-152">Hayır.</span><span class="sxs-lookup"><span data-stu-id="818ad-152">No.</span></span> <span data-ttu-id="818ad-153">Bağlantılı hizmet tanımında belirtilen URL yolu belirtilmediğinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="818ad-153">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="818ad-154">Dizin</span><span class="sxs-lookup"><span data-stu-id="818ad-154">index</span></span> |<span data-ttu-id="818ad-155">Tablo kaynak dizini.</span><span class="sxs-lookup"><span data-stu-id="818ad-155">The index of the table in the resource.</span></span> <span data-ttu-id="818ad-156">Bkz: [bir HTML sayfasında tablosunun Get dizini](#get-index-of-a-table-in-an-html-page) bir HTML sayfasında bir tablo dizininin alma adımları için bölüm.</span><span class="sxs-lookup"><span data-stu-id="818ad-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="818ad-157">Evet</span><span class="sxs-lookup"><span data-stu-id="818ad-157">Yes</span></span> |

<span data-ttu-id="818ad-158">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="818ad-158">**Example:**</span></span>

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

## <a name="copy-activity-properties"></a><span data-ttu-id="818ad-159">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="818ad-159">Copy activity properties</span></span>
<span data-ttu-id="818ad-160">Bölümler & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz: [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="818ad-160">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="818ad-161">Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="818ad-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="818ad-162">Oysa etkinliğin typeProperties bölümündeki özellikler her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="818ad-162">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="818ad-163">Kopya etkinliği için bunlar türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="818ad-163">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="818ad-164">Şu anda kopyalama etkinliği kaynağında olduğunda türü **WebSource**, hiçbir ek özellikler desteklenir.</span><span class="sxs-lookup"><span data-stu-id="818ad-164">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-to-azure-blob"></a><span data-ttu-id="818ad-165">JSON örnek: veri kopyalama Web tablosundan Azure Blob</span><span class="sxs-lookup"><span data-stu-id="818ad-165">JSON example: Copy data from Web table to Azure Blob</span></span>
<span data-ttu-id="818ad-166">Aşağıdaki örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="818ad-166">The following sample shows:</span></span>

1. <span data-ttu-id="818ad-167">Bağlı hizmet türü [Web](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="818ad-167">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="818ad-168">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="818ad-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="818ad-169">Bir giriş [dataset](data-factory-create-datasets.md) türü [WebTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="818ad-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="818ad-170">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="818ad-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="818ad-171">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [WebSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="818ad-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="818ad-172">Örnek verileri saatte bir Azure blob Web tablosundan kopyalar.</span><span class="sxs-lookup"><span data-stu-id="818ad-172">The sample copies data from a Web table to an Azure blob every hour.</span></span> <span data-ttu-id="818ad-173">Bu örnekler kullanılan JSON özellikleri örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="818ad-173">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="818ad-174">Aşağıdaki örnek, bir Azure blob Web tablodan veri kopyalama gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="818ad-174">The following sample shows how to copy data from a Web table to an Azure blob.</span></span> <span data-ttu-id="818ad-175">Ancak, verileri doğrudan belirtilen havuzlarını hiçbirini kopyalanabilir [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) kopya etkinliği Azure Data Factory kullanarak makale.</span><span class="sxs-lookup"><span data-stu-id="818ad-175">However, data can be copied directly to any of the sinks stated in the [Data Movement Activities](data-factory-data-movement-activities.md) article by using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="818ad-176">**Web hizmeti bağlı** Bu örnek anonim kimlik doğrulaması ile bağlantılı Web hizmetini kullanır.</span><span class="sxs-lookup"><span data-stu-id="818ad-176">**Web linked service** This example uses the Web linked service with anonymous authentication.</span></span> <span data-ttu-id="818ad-177">Bkz: [Web bağlantılı hizmeti](#linked-service-properties) bölümü için farklı tür kimlik doğrulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="818ad-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="818ad-178">**Azure Storage bağlı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="818ad-178">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="818ad-179">**WebTable girdi veri kümesi** ayarı **dış** için **true** Data Factory hizmetinin veri kümesi data factory dış ve verileri bir etkinlik tarafından üretilen değil bildirir üreteci.</span><span class="sxs-lookup"><span data-stu-id="818ad-179">**WebTable input dataset** Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="818ad-180">Bkz: [bir HTML sayfasında tablosunun Get dizini](#get-index-of-a-table-in-an-html-page) bir HTML sayfasında bir tablo dizininin alma adımları için bölüm.</span><span class="sxs-lookup"><span data-stu-id="818ad-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span>  
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


<span data-ttu-id="818ad-181">**Azure Blob dataset çıktı**</span><span class="sxs-lookup"><span data-stu-id="818ad-181">**Azure Blob output dataset**</span></span>

<span data-ttu-id="818ad-182">Veri her saat yeni bir bloba yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="818ad-182">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

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



<span data-ttu-id="818ad-183">**Kopyalama etkinliği ile kanalı**</span><span class="sxs-lookup"><span data-stu-id="818ad-183">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="818ad-184">Ardışık Düzen giriş ve çıkış veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="818ad-184">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="818ad-185">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **WebSource** ve **havuz** türü ayarlanmış **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="818ad-185">In the pipeline JSON definition, the **source** type is set to **WebSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="818ad-186">Bkz: [WebSource türü özellikleri](#copy-activity-type-properties) WebSource tarafından desteklenen özelliklerin listesi için.</span><span class="sxs-lookup"><span data-stu-id="818ad-186">See [WebSource type properties](#copy-activity-type-properties) for the list of properties supported by the WebSource.</span></span>

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
        "description": "Copy from a Web table to an Azure blob",
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

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="818ad-187">Bir HTML sayfasında bir tablonun dizini alma</span><span class="sxs-lookup"><span data-stu-id="818ad-187">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="818ad-188">Başlatma **Excel 2016** ve geçiş **veri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="818ad-188">Launch **Excel 2016** and switch to the **Data** tab.</span></span>  
2. <span data-ttu-id="818ad-189">Tıklatın **yeni sorgu** araç çubuğunda işaret **diğer kaynaklardan** tıklatıp **Web'den**.</span><span class="sxs-lookup"><span data-stu-id="818ad-189">Click **New Query** on the toolbar, point to **From Other Sources** and click **From Web**.</span></span>

    ![Power Query menüsü](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="818ad-191">İçinde **Web'den** iletişim kutusunda, girin **URL** bağlantılı hizmeti JSON içinde kullanırsınız (örneğin: https://en.wikipedia.org/wiki/) yolu belirtin veri kümesi için birlikte (örneğin: AFI % 27s_ 100_Years... 100_Movies) tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="818ad-191">In the **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for the dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![Web iletişim kutusundan](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="818ad-193">Bu örnekte kullanılan URL: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="818ad-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="818ad-194">Görürseniz **erişim Web içeriği** iletişim kutusunda, sağa seçin **URL**, **kimlik doğrulaması**, tıklatıp **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="818ad-194">If you see **Access Web content** dialog box, select the right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Web içerik iletişim kutusuna erişin](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="818ad-196">Tıklatın bir **tablo** öğesi tablosundan içeriğine bakın ve ardından ağaç görünümünde **Düzenle** altındaki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="818ad-196">Click a **table** item in the tree view to see content from the table and then click **Edit** button at the bottom.</span></span>  

   ![Gezgin iletişim](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="818ad-198">İçinde **sorgu Düzenleyicisi'ni** penceresinde tıklatın **Gelişmiş Düzenleyici** araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="818ad-198">In the **Query Editor** window, click **Advanced Editor** button on the toolbar.</span></span>

    ![Gelişmiş Düzenleyici düğmesi](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="818ad-200">Gelişmiş Düzenleyici iletişim kutusunda "Kaynak" yanındaki dizin numarasıdır.</span><span class="sxs-lookup"><span data-stu-id="818ad-200">In the Advanced Editor dialog box, the number next to "Source" is the index.</span></span>

    ![Düzenleyicisi - Gelişmiş dizin](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="818ad-202">Excel 2013 kullanıyorsanız, [Excel için Microsoft Power Query](https://www.microsoft.com/download/details.aspx?id=39379) dizini alınamadı.</span><span class="sxs-lookup"><span data-stu-id="818ad-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) to get the index.</span></span> <span data-ttu-id="818ad-203">Bkz: [bir web sayfası Bağlan](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="818ad-203">See [Connect to a web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="818ad-204">Adımlar kullanıyorsanız benzer [Masaüstü için Microsoft Power BI](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="818ad-204">The steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> <span data-ttu-id="818ad-205">Kaynak veri kümesi sütunlarından havuz kümesinden sütunlara eşlemek için bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="818ad-205">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="818ad-206">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="818ad-206">Performance and Tuning</span></span>
<span data-ttu-id="818ad-207">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve onu en iyi duruma getirmek için çeşitli yollar etkisi performansını anahtar Etkenler hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="818ad-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
