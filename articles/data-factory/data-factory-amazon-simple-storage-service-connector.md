---
title: "Veri Fabrikası kullanarak Amazon Basit Depolama hizmetinden veri taşıma | Microsoft Docs"
description: "Azure Data Factory kullanarak Amazon Basit Depolama hizmetinden (S3) veri taşıma hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 3e21f7dfccc3b235071344a28c7d94f65e6bf9ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="56bb8-103">Azure Data Factory kullanarak Amazon Basit Depolama hizmetinden veri taşıma</span><span class="sxs-lookup"><span data-stu-id="56bb8-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="56bb8-104">Bu makalede kopya etkinliği Azure Data Factory'de verileri Amazon Basit Depolama hizmetinden (S3) taşımak için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="56bb8-104">This article explains how to use the copy activity in Azure Data Factory to move data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="56bb8-105">Derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) kopyalama etkinliği ile veri taşıma için genel bir bakış sunar makalesi.</span><span class="sxs-lookup"><span data-stu-id="56bb8-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="56bb8-106">Verileri Amazon S3'ten herhangi desteklenen havuz veri deposuna kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56bb8-106">You can copy data from Amazon S3 to any supported sink data store.</span></span> <span data-ttu-id="56bb8-107">Veri depoları havuzlarını kopyalama etkinliği tarafından desteklenen bir listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="56bb8-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="56bb8-108">Veri Fabrikası şu anda yalnızca taşıma Amazon S3 verileri diğer veri depolarına destekler, ancak verileri diğer veriler taşıma değil Amazon S3 depolar.</span><span class="sxs-lookup"><span data-stu-id="56bb8-108">Data Factory currently supports only moving data from Amazon S3 to other data stores, but not moving data from other data stores to Amazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="56bb8-109">Gerekli izinler</span><span class="sxs-lookup"><span data-stu-id="56bb8-109">Required permissions</span></span>
<span data-ttu-id="56bb8-110">Amazon S3'ten verileri kopyalamak için aşağıdaki izinleri verilmiş olan emin olun:</span><span class="sxs-lookup"><span data-stu-id="56bb8-110">To copy data from Amazon S3, make sure you have been granted the following permissions:</span></span>

* <span data-ttu-id="56bb8-111">`s3:GetObject`ve `s3:GetObjectVersion` Amazon S3 nesne işlemleri için.</span><span class="sxs-lookup"><span data-stu-id="56bb8-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="56bb8-112">`s3:ListBucket`Amazon S3 Demetini işlemleri için.</span><span class="sxs-lookup"><span data-stu-id="56bb8-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="56bb8-113">Data Factory Kopyalama Sihirbazı'nı kullanıyorsanız `s3:ListAllMyBuckets` de gereklidir.</span><span class="sxs-lookup"><span data-stu-id="56bb8-113">If you are using the Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="56bb8-114">Amazon S3 izinlerin tam listesi hakkında daha fazla ayrıntı için bkz: [belirleyen izinleri bir ilke](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span><span class="sxs-lookup"><span data-stu-id="56bb8-114">For details about the full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="56bb8-115">Başlarken</span><span class="sxs-lookup"><span data-stu-id="56bb8-115">Getting started</span></span>
<span data-ttu-id="56bb8-116">Farklı araçlar veya API'lerini kullanarak bir Amazon S3 kaynaktan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="56bb8-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="56bb8-117">Bir işlem hattı oluşturmak için en kolay yolu kullanmaktır **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="56bb8-117">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="56bb8-118">Hızlı bir kılavuz için bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="56bb8-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="56bb8-119">Bir işlem hattı oluşturmak için aşağıdaki araçları kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu**, **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="56bb8-119">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="56bb8-120">Kopyalama etkinliği ile işlem hattı oluşturmak adım adım yönergeler için bkz: [kopyalama etkinliği Öğreticisi](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="56bb8-120">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="56bb8-121">Araçları veya API'ler kullanıp bir havuz veri deposu için bir kaynak veri deposundan verileri taşır bir ardışık düzen oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="56bb8-121">Whether you use tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="56bb8-122">Oluşturma **bağlantılı Hizmetleri** girdi ve çıktı verilerini bağlamak için veri fabrikanıza depolar.</span><span class="sxs-lookup"><span data-stu-id="56bb8-122">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="56bb8-123">Oluşturma **veri kümeleri** kopyalama işlemi için girdi ve çıktı verilerini temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="56bb8-123">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="56bb8-124">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="56bb8-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="56bb8-125">Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="56bb8-125">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="56bb8-126">Araçları veya API'ler (dışında .NET API'si) kullandığınızda, JSON biçimini kullanarak bu Data Factory varlıklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="56bb8-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="56bb8-127">Bir Amazon S3 veri deposundan verileri kopyalamak için kullanılan Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: veri kopyalama Amazon S3'ten Azure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="56bb8-127">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon S3 data store, see the [JSON example: Copy data from Amazon S3 to Azure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="56bb8-128">Kopyalama etkinliği için desteklenen dosya ve sıkıştırma biçimleri hakkında daha fazla ayrıntı için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="56bb8-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="56bb8-129">Aşağıdaki bölümler, Amazon S3 Data Factory varlıklarını belirli tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="56bb8-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="56bb8-130">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="56bb8-130">Linked service properties</span></span>
<span data-ttu-id="56bb8-131">Bağlı hizmet, veri fabrikası için bir veri deposu bağlar.</span><span class="sxs-lookup"><span data-stu-id="56bb8-131">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="56bb8-132">Bağlı hizmet türü oluşturma **AwsAccessKey** veri fabrikanıza Amazon S3 veri deponuza bağlamak için.</span><span class="sxs-lookup"><span data-stu-id="56bb8-132">You create a linked service of type **AwsAccessKey** to link your Amazon S3 data store to your data factory.</span></span> <span data-ttu-id="56bb8-133">Aşağıdaki tabloda, Amazon S3 JSON öğeleri belirli bir açıklamasını sağlar (AwsAccessKey) bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="56bb8-133">The following table provides description for JSON elements specific to Amazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="56bb8-134">Özellik</span><span class="sxs-lookup"><span data-stu-id="56bb8-134">Property</span></span> | <span data-ttu-id="56bb8-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="56bb8-135">Description</span></span> | <span data-ttu-id="56bb8-136">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="56bb8-136">Allowed values</span></span> | <span data-ttu-id="56bb8-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="56bb8-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="56bb8-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="56bb8-138">accessKeyID</span></span> |<span data-ttu-id="56bb8-139">Gizli erişim anahtarı kimliği.</span><span class="sxs-lookup"><span data-stu-id="56bb8-139">ID of the secret access key.</span></span> |<span data-ttu-id="56bb8-140">Dize</span><span class="sxs-lookup"><span data-stu-id="56bb8-140">string</span></span> |<span data-ttu-id="56bb8-141">Evet</span><span class="sxs-lookup"><span data-stu-id="56bb8-141">Yes</span></span> |
| <span data-ttu-id="56bb8-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="56bb8-142">secretAccessKey</span></span> |<span data-ttu-id="56bb8-143">Gizli erişim anahtar kendisi.</span><span class="sxs-lookup"><span data-stu-id="56bb8-143">The secret access key itself.</span></span> |<span data-ttu-id="56bb8-144">Şifrelenmiş gizli dize</span><span class="sxs-lookup"><span data-stu-id="56bb8-144">Encrypted secret string</span></span> |<span data-ttu-id="56bb8-145">Evet</span><span class="sxs-lookup"><span data-stu-id="56bb8-145">Yes</span></span> |

<span data-ttu-id="56bb8-146">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="56bb8-146">Here is an example:</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="56bb8-147">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="56bb8-147">Dataset properties</span></span>
<span data-ttu-id="56bb8-148">Girdi verileri Azure Blob Depolama alanında temsil etmek üzere bir veri kümesi belirtmek için veri kümesine tür özelliği ayarlayın **AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="56bb8-148">To specify a dataset to represent input data in Azure Blob storage, set the type property of the dataset to **AmazonS3**.</span></span> <span data-ttu-id="56bb8-149">Ayarlama **linkedServiceName** Amazon S3 adını dataset özelliğinin bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="56bb8-149">Set the **linkedServiceName** property of the dataset to the name of the Amazon S3 linked service.</span></span> <span data-ttu-id="56bb8-150">Bölümleri ve veri kümelerini tanımlamak için kullanılabilen özellikleri tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="56bb8-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="56bb8-151">Bölümler yapısı, kullanılabilirlik ve ilke gibi tüm veri türleri (örneğin, SQL database, Azure blob ve Azure tablo) benzer.</span><span class="sxs-lookup"><span data-stu-id="56bb8-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="56bb8-152">**TypeProperties** bölüm veri kümesi her tür için farklıdır ve verilerin veri deposunda konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="56bb8-152">The **typeProperties** section is different for each type of dataset, and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="56bb8-153">**TypeProperties** bir veri kümesi için bir bölüm türü **AmazonS3** (Amazon S3 dataset içerir) aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="56bb8-153">The **typeProperties** section for a dataset of type **AmazonS3** (which includes the Amazon S3 dataset) has the following properties:</span></span>

| <span data-ttu-id="56bb8-154">Özellik</span><span class="sxs-lookup"><span data-stu-id="56bb8-154">Property</span></span> | <span data-ttu-id="56bb8-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="56bb8-155">Description</span></span> | <span data-ttu-id="56bb8-156">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="56bb8-156">Allowed values</span></span> | <span data-ttu-id="56bb8-157">Gerekli</span><span class="sxs-lookup"><span data-stu-id="56bb8-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="56bb8-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="56bb8-158">bucketName</span></span> |<span data-ttu-id="56bb8-159">S3 demetini adı.</span><span class="sxs-lookup"><span data-stu-id="56bb8-159">The S3 bucket name.</span></span> |<span data-ttu-id="56bb8-160">Dize</span><span class="sxs-lookup"><span data-stu-id="56bb8-160">String</span></span> |<span data-ttu-id="56bb8-161">Evet</span><span class="sxs-lookup"><span data-stu-id="56bb8-161">Yes</span></span> |
| <span data-ttu-id="56bb8-162">anahtar</span><span class="sxs-lookup"><span data-stu-id="56bb8-162">key</span></span> |<span data-ttu-id="56bb8-163">S3 nesne anahtarı.</span><span class="sxs-lookup"><span data-stu-id="56bb8-163">The S3 object key.</span></span> |<span data-ttu-id="56bb8-164">Dize</span><span class="sxs-lookup"><span data-stu-id="56bb8-164">String</span></span> |<span data-ttu-id="56bb8-165">Hayır</span><span class="sxs-lookup"><span data-stu-id="56bb8-165">No</span></span> |
| <span data-ttu-id="56bb8-166">önek</span><span class="sxs-lookup"><span data-stu-id="56bb8-166">prefix</span></span> |<span data-ttu-id="56bb8-167">S3 nesne anahtarı için önek.</span><span class="sxs-lookup"><span data-stu-id="56bb8-167">Prefix for the S3 object key.</span></span> <span data-ttu-id="56bb8-168">Seçilen nesneler, anahtarları Bu önek ile başlatın.</span><span class="sxs-lookup"><span data-stu-id="56bb8-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="56bb8-169">Yalnızca anahtar boş olduğunda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="56bb8-169">Applies only when key is empty.</span></span> |<span data-ttu-id="56bb8-170">Dize</span><span class="sxs-lookup"><span data-stu-id="56bb8-170">String</span></span> |<span data-ttu-id="56bb8-171">Hayır</span><span class="sxs-lookup"><span data-stu-id="56bb8-171">No</span></span> |
| <span data-ttu-id="56bb8-172">Sürüm</span><span class="sxs-lookup"><span data-stu-id="56bb8-172">version</span></span> |<span data-ttu-id="56bb8-173">S3 sürüm etkinleştirilirse S3 nesne sürümü.</span><span class="sxs-lookup"><span data-stu-id="56bb8-173">The version of the S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="56bb8-174">Dize</span><span class="sxs-lookup"><span data-stu-id="56bb8-174">String</span></span> |<span data-ttu-id="56bb8-175">Hayır</span><span class="sxs-lookup"><span data-stu-id="56bb8-175">No</span></span> |
| <span data-ttu-id="56bb8-176">Biçimi</span><span class="sxs-lookup"><span data-stu-id="56bb8-176">format</span></span> | <span data-ttu-id="56bb8-177">Şu biçimi türleri desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="56bb8-177">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="56bb8-178">Ayarlama **türü** şu değerlerden biri biçimine altında özellik.</span><span class="sxs-lookup"><span data-stu-id="56bb8-178">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="56bb8-179">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [JSON biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi ](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="56bb8-179">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="56bb8-180">Dosyaları olarak kopyalamak istiyorsanız-olan dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="56bb8-180">If you want to copy files as-is between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="56bb8-181">Hayır</span><span class="sxs-lookup"><span data-stu-id="56bb8-181">No</span></span> | |
| <span data-ttu-id="56bb8-182">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="56bb8-182">compression</span></span> | <span data-ttu-id="56bb8-183">Veri sıkıştırma düzeyini ve türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="56bb8-183">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="56bb8-184">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="56bb8-184">The supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="56bb8-185">Desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="56bb8-185">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="56bb8-186">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="56bb8-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="56bb8-187">Hayır</span><span class="sxs-lookup"><span data-stu-id="56bb8-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="56bb8-188">**bucketName + tuşu** burada demet S3 nesneleri için kök kapsayıcı ve anahtarıdır S3 nesnenin tam yolunun S3 nesnenin konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="56bb8-188">**bucketName + key** specifies the location of the S3 object, where bucket is the root container for S3 objects, and key is the full path to the S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="56bb8-189">Örnek veri kümesi önekiyle</span><span class="sxs-lookup"><span data-stu-id="56bb8-189">Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a><span data-ttu-id="56bb8-190">Örnek veri kümesi (sürümüyle)</span><span class="sxs-lookup"><span data-stu-id="56bb8-190">Sample dataset (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="56bb8-191">S3 için dinamik yollar</span><span class="sxs-lookup"><span data-stu-id="56bb8-191">Dynamic paths for S3</span></span>
<span data-ttu-id="56bb8-192">Önceki örnekte sabit değerleri kullanan **anahtar** ve **bucketName** Amazon S3 dataset özelliklerinde.</span><span class="sxs-lookup"><span data-stu-id="56bb8-192">The preceding sample uses fixed values for the **key** and **bucketName** properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="56bb8-193">Veri Fabrikası SliceStart gibi sistem değişkenleri kullanarak çalışma zamanında dinamik olarak bu özellikleri hesaplama olabilir.</span><span class="sxs-lookup"><span data-stu-id="56bb8-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="56bb8-194">Aynı yapabileceğiniz **önek** bir Amazon S3 dataset özelliğinin.</span><span class="sxs-lookup"><span data-stu-id="56bb8-194">You can do the same for the **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="56bb8-195">Desteklenen işlevleri ve değişkenler listesi için bkz: [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="56bb8-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="56bb8-196">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="56bb8-196">Copy activity properties</span></span>
<span data-ttu-id="56bb8-197">Bölümleri ve etkinlikleri tanımlamak için kullanılabilen özellikleri tam listesi için bkz: [ardışık düzen oluşturma](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="56bb8-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="56bb8-198">Ad, açıklama, giriş ve çıkış tabloları ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="56bb8-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="56bb8-199">Kullanılabilir özellikler **typeProperties** bölüm etkinliğin her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="56bb8-199">Properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="56bb8-200">Kopya etkinliği için özellikler türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="56bb8-200">For the copy activity, properties vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="56bb8-201">Kopyalama etkinliği kaynağında türü olduğunda **FileSystemSource** (içeren Amazon S3), aşağıdaki özellikler kullanılabilir **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="56bb8-201">When a source in the copy activity is of type **FileSystemSource** (which includes Amazon S3), the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="56bb8-202">Özellik</span><span class="sxs-lookup"><span data-stu-id="56bb8-202">Property</span></span> | <span data-ttu-id="56bb8-203">Açıklama</span><span class="sxs-lookup"><span data-stu-id="56bb8-203">Description</span></span> | <span data-ttu-id="56bb8-204">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="56bb8-204">Allowed values</span></span> | <span data-ttu-id="56bb8-205">Gerekli</span><span class="sxs-lookup"><span data-stu-id="56bb8-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="56bb8-206">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="56bb8-206">recursive</span></span> |<span data-ttu-id="56bb8-207">Özyinelemeli S3 listesinde olup olmadığını belirtir dizini altındaki nesneleri.</span><span class="sxs-lookup"><span data-stu-id="56bb8-207">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="56bb8-208">true/false</span><span class="sxs-lookup"><span data-stu-id="56bb8-208">true/false</span></span> |<span data-ttu-id="56bb8-209">Hayır</span><span class="sxs-lookup"><span data-stu-id="56bb8-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-to-azure-blob-storage"></a><span data-ttu-id="56bb8-210">JSON örnek: veri kopyalama Amazon S3'ten Azure Blob depolama alanına</span><span class="sxs-lookup"><span data-stu-id="56bb8-210">JSON example: Copy data from Amazon S3 to Azure Blob storage</span></span>
<span data-ttu-id="56bb8-211">Bu örnek, Amazon S3'ten bir Azure Blob depolama alanına veri kopyalama gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="56bb8-211">This sample shows how to copy data from Amazon S3 to an Azure Blob storage.</span></span> <span data-ttu-id="56bb8-212">Ancak, verileri doğrudan kopyalanabilir [desteklenen havuzlarını hiçbirini](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Data Factory kopyalama etkinliği kullanarak.</span><span class="sxs-lookup"><span data-stu-id="56bb8-212">However, data can be copied directly to [any of the sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using the copy activity in Data Factory.</span></span>

<span data-ttu-id="56bb8-213">Örnek aşağıdaki Data Factory varlıkları için JSON tanımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="56bb8-213">The sample provides JSON definitions for the following Data Factory entities.</span></span> <span data-ttu-id="56bb8-214">Bu tanımları verileri Amazon S3'ten kullanarak Blob depolama alanına kopyalamak için bir işlem hattı oluşturmak için kullanabileceğiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), veya [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="56bb8-214">You can use these definitions to create a pipeline to copy data from Amazon S3 to Blob storage, by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="56bb8-215">Bağlı hizmet türü [AwsAccessKey](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="56bb8-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="56bb8-216">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="56bb8-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="56bb8-217">Bir giriş [dataset](data-factory-create-datasets.md) türü [AmazonS3](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="56bb8-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="56bb8-218">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="56bb8-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="56bb8-219">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [FileSystemSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="56bb8-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="56bb8-220">Örnek verileri Amazon S3'ten saatte bir Azure blob kopyalar.</span><span class="sxs-lookup"><span data-stu-id="56bb8-220">The sample copies data from Amazon S3 to an Azure blob every hour.</span></span> <span data-ttu-id="56bb8-221">Bu örnekler kullanılan JSON özellikleri örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="56bb8-221">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="56bb8-222">Amazon S3 bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="56bb8-222">Amazon S3 linked service</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="56bb8-223">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="56bb8-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="56bb8-224">Amazon S3 girdi veri kümesi</span><span class="sxs-lookup"><span data-stu-id="56bb8-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="56bb8-225">Ayarı **"dış": true** Data Factory hizmetinin veri kümesi data factory dış olduğunu bildirir.</span><span class="sxs-lookup"><span data-stu-id="56bb8-225">Setting **"external": true** informs the Data Factory service that the dataset is external to the data factory.</span></span> <span data-ttu-id="56bb8-226">Bu özellik, bir işlem hattında etkinlik tarafından üretilen olmayan bir giriş veri kümesi üzerinde true olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="56bb8-226">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="56bb8-227">Azure Blob çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="56bb8-227">Azure Blob output dataset</span></span>

<span data-ttu-id="56bb8-228">Veri her saat yeni bir bloba yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="56bb8-228">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="56bb8-229">Blob klasör yolu dinamik işlenmekte olan dilim başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="56bb8-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="56bb8-230">Klasör yolu yıl, ay, gün ve saatleri bölümlerini başlangıç saatini kullanır.</span><span class="sxs-lookup"><span data-stu-id="56bb8-230">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="56bb8-231">Bir Amazon S3 kaynak ve blob havuz sahip işlem hattı kopyalama etkinliği</span><span class="sxs-lookup"><span data-stu-id="56bb8-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="56bb8-232">Ardışık Düzen giriş ve çıkış veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="56bb8-232">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="56bb8-233">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **FileSystemSource**, ve **havuz** türü ayarlanmış **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="56bb8-233">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
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
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="56bb8-234">Bir havuz veri kümesinden sütunlara kaynak kümesinden sütunları eşlemek için bkz: [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="56bb8-234">To map columns from a source dataset to columns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="56bb8-235">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="56bb8-235">Next steps</span></span>
<span data-ttu-id="56bb8-236">Aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="56bb8-236">See the following articles:</span></span>

* <span data-ttu-id="56bb8-237">Bu veri fabrikası ve onu en iyi duruma getirmek için çeşitli yollar veri taşıma (kopyalama etkinliği) etkisi performansını anahtar Etkenler hakkında bilgi için bkz [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="56bb8-237">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="56bb8-238">Kopyalama etkinliği ile işlem hattı oluşturmak için adım adım yönergeler için bkz: [kopyalama etkinliği Öğreticisi](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="56bb8-238">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
