---
title: "Veri Fabrikası kullanarak aaaMove verilerden Amazon basit depolama hizmeti | Microsoft Docs"
description: "Hakkında bilgi edinin Azure Data Factory kullanarak toomove verilerden Amazon Basit Depolama Birimi Hizmeti (S3)."
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
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="e181e-103">Azure Data Factory kullanarak Amazon Basit Depolama hizmetinden veri taşıma</span><span class="sxs-lookup"><span data-stu-id="e181e-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="e181e-104">Bu makalede nasıl toouse hello kopyalama etkinliği Azure Data Factory toomove verileri Amazon Basit Depolama hizmetinden (S3) açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e181e-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="e181e-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="e181e-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="e181e-106">Verileri Amazon S3 desteklenen tooany havuz veri deposundan kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e181e-106">You can copy data from Amazon S3 tooany supported sink data store.</span></span> <span data-ttu-id="e181e-107">Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="e181e-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="e181e-108">Veri Fabrikası şu anda yalnızca taşıma verileri Amazon S3 tooother veri depolarını destekler, ancak verileri diğer veriler taşıma değil tooAmazon S3 depolar.</span><span class="sxs-lookup"><span data-stu-id="e181e-108">Data Factory currently supports only moving data from Amazon S3 tooother data stores, but not moving data from other data stores tooAmazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="e181e-109">Gerekli izinler</span><span class="sxs-lookup"><span data-stu-id="e181e-109">Required permissions</span></span>
<span data-ttu-id="e181e-110">Amazon S3 toocopy verilerden hello aşağıdaki izinleri verilmiş olan emin olun:</span><span class="sxs-lookup"><span data-stu-id="e181e-110">toocopy data from Amazon S3, make sure you have been granted hello following permissions:</span></span>

* <span data-ttu-id="e181e-111">`s3:GetObject`ve `s3:GetObjectVersion` Amazon S3 nesne işlemleri için.</span><span class="sxs-lookup"><span data-stu-id="e181e-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="e181e-112">`s3:ListBucket`Amazon S3 Demetini işlemleri için.</span><span class="sxs-lookup"><span data-stu-id="e181e-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="e181e-113">Merhaba Data Factory Kopyalama Sihirbazı, kullanıyorsanız `s3:ListAllMyBuckets` de gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e181e-113">If you are using hello Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="e181e-114">Amazon S3 izinleri hello tam listesi hakkında daha fazla ayrıntı için bkz: [belirleyen izinleri bir ilke](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span><span class="sxs-lookup"><span data-stu-id="e181e-114">For details about hello full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="e181e-115">Başlarken</span><span class="sxs-lookup"><span data-stu-id="e181e-115">Getting started</span></span>
<span data-ttu-id="e181e-116">Farklı araçlar veya API'lerini kullanarak bir Amazon S3 kaynaktan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e181e-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="e181e-117">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="e181e-117">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="e181e-118">Hızlı bir kılavuz için bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="e181e-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="e181e-119">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="e181e-119">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="e181e-120">Adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için bkz: Merhaba [kopyalama etkinliği Öğreticisi](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="e181e-120">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="e181e-121">Araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e181e-121">Whether you use tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="e181e-122">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="e181e-122">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="e181e-123">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="e181e-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="e181e-124">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="e181e-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="e181e-125">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e181e-125">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="e181e-126">Araçları veya API'ler (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="e181e-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="e181e-127">Merhaba kullanılan toocopy verileri Amazon S3 veri deposundan Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz [JSON örnek: Blob Amazon S3 tooAzure veri kopyalama](#json-example-copy-data-from-amazon-s3-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="e181e-127">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon S3 data store, see hello [JSON example: Copy data from Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="e181e-128">Kopyalama etkinliği için desteklenen dosya ve sıkıştırma biçimleri hakkında daha fazla ayrıntı için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="e181e-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="e181e-129">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooAmazon S3 JSON özellikleri hakkında ayrıntılı bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="e181e-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="e181e-130">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="e181e-130">Linked service properties</span></span>
<span data-ttu-id="e181e-131">Bağlı hizmet, bir veri deposu tooa veri fabrikası bağlar.</span><span class="sxs-lookup"><span data-stu-id="e181e-131">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="e181e-132">Bağlı hizmet türü oluşturma **AwsAccessKey** toolink Amazon S3 verilerinizi depolamak tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="e181e-132">You create a linked service of type **AwsAccessKey** toolink your Amazon S3 data store tooyour data factory.</span></span> <span data-ttu-id="e181e-133">Aşağıdaki tablonun hello bağlı açıklamasını JSON öğeleri belirli tooAmazon S3 (AwsAccessKey) hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="e181e-133">hello following table provides description for JSON elements specific tooAmazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="e181e-134">Özellik</span><span class="sxs-lookup"><span data-stu-id="e181e-134">Property</span></span> | <span data-ttu-id="e181e-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e181e-135">Description</span></span> | <span data-ttu-id="e181e-136">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="e181e-136">Allowed values</span></span> | <span data-ttu-id="e181e-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e181e-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e181e-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="e181e-138">accessKeyID</span></span> |<span data-ttu-id="e181e-139">Merhaba gizli erişim anahtarı kimliği.</span><span class="sxs-lookup"><span data-stu-id="e181e-139">ID of hello secret access key.</span></span> |<span data-ttu-id="e181e-140">Dize</span><span class="sxs-lookup"><span data-stu-id="e181e-140">string</span></span> |<span data-ttu-id="e181e-141">Evet</span><span class="sxs-lookup"><span data-stu-id="e181e-141">Yes</span></span> |
| <span data-ttu-id="e181e-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="e181e-142">secretAccessKey</span></span> |<span data-ttu-id="e181e-143">Merhaba gizli erişim anahtarı kendisi.</span><span class="sxs-lookup"><span data-stu-id="e181e-143">hello secret access key itself.</span></span> |<span data-ttu-id="e181e-144">Şifrelenmiş gizli dize</span><span class="sxs-lookup"><span data-stu-id="e181e-144">Encrypted secret string</span></span> |<span data-ttu-id="e181e-145">Evet</span><span class="sxs-lookup"><span data-stu-id="e181e-145">Yes</span></span> |

<span data-ttu-id="e181e-146">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e181e-146">Here is an example:</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="e181e-147">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="e181e-147">Dataset properties</span></span>
<span data-ttu-id="e181e-148">toospecify dataset toorepresent giriş verileri Azure Blob storage'da kümesi hello type özelliği hello kümesinin çok**AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="e181e-148">toospecify a dataset toorepresent input data in Azure Blob storage, set hello type property of hello dataset too**AmazonS3**.</span></span> <span data-ttu-id="e181e-149">Set hello **linkedServiceName** hello dataset toohello adının hello Amazon S3 özelliği bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="e181e-149">Set hello **linkedServiceName** property of hello dataset toohello name of hello Amazon S3 linked service.</span></span> <span data-ttu-id="e181e-150">Bölümleri ve veri kümelerini tanımlamak için kullanılabilen özellikleri tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="e181e-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="e181e-151">Bölümler yapısı, kullanılabilirlik ve ilke gibi tüm veri türleri (örneğin, SQL database, Azure blob ve Azure tablo) benzer.</span><span class="sxs-lookup"><span data-stu-id="e181e-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="e181e-152">Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e181e-152">hello **typeProperties** section is different for each type of dataset, and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="e181e-153">Merhaba **typeProperties** bir veri kümesi için bir bölüm türü **AmazonS3** (Merhaba Amazon S3 dataset içerir) hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="e181e-153">hello **typeProperties** section for a dataset of type **AmazonS3** (which includes hello Amazon S3 dataset) has hello following properties:</span></span>

| <span data-ttu-id="e181e-154">Özellik</span><span class="sxs-lookup"><span data-stu-id="e181e-154">Property</span></span> | <span data-ttu-id="e181e-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e181e-155">Description</span></span> | <span data-ttu-id="e181e-156">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="e181e-156">Allowed values</span></span> | <span data-ttu-id="e181e-157">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e181e-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e181e-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="e181e-158">bucketName</span></span> |<span data-ttu-id="e181e-159">Merhaba S3 demetini adı.</span><span class="sxs-lookup"><span data-stu-id="e181e-159">hello S3 bucket name.</span></span> |<span data-ttu-id="e181e-160">Dize</span><span class="sxs-lookup"><span data-stu-id="e181e-160">String</span></span> |<span data-ttu-id="e181e-161">Evet</span><span class="sxs-lookup"><span data-stu-id="e181e-161">Yes</span></span> |
| <span data-ttu-id="e181e-162">anahtar</span><span class="sxs-lookup"><span data-stu-id="e181e-162">key</span></span> |<span data-ttu-id="e181e-163">Merhaba S3 nesne anahtarı.</span><span class="sxs-lookup"><span data-stu-id="e181e-163">hello S3 object key.</span></span> |<span data-ttu-id="e181e-164">Dize</span><span class="sxs-lookup"><span data-stu-id="e181e-164">String</span></span> |<span data-ttu-id="e181e-165">Hayır</span><span class="sxs-lookup"><span data-stu-id="e181e-165">No</span></span> |
| <span data-ttu-id="e181e-166">önek</span><span class="sxs-lookup"><span data-stu-id="e181e-166">prefix</span></span> |<span data-ttu-id="e181e-167">Merhaba S3 nesne anahtarı için önek.</span><span class="sxs-lookup"><span data-stu-id="e181e-167">Prefix for hello S3 object key.</span></span> <span data-ttu-id="e181e-168">Seçilen nesneler, anahtarları Bu önek ile başlatın.</span><span class="sxs-lookup"><span data-stu-id="e181e-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="e181e-169">Yalnızca anahtar boş olduğunda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e181e-169">Applies only when key is empty.</span></span> |<span data-ttu-id="e181e-170">Dize</span><span class="sxs-lookup"><span data-stu-id="e181e-170">String</span></span> |<span data-ttu-id="e181e-171">Hayır</span><span class="sxs-lookup"><span data-stu-id="e181e-171">No</span></span> |
| <span data-ttu-id="e181e-172">Sürüm</span><span class="sxs-lookup"><span data-stu-id="e181e-172">version</span></span> |<span data-ttu-id="e181e-173">Merhaba S3 nesnesinin S3 sürüm etkinleştirilirse Hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="e181e-173">hello version of hello S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="e181e-174">Dize</span><span class="sxs-lookup"><span data-stu-id="e181e-174">String</span></span> |<span data-ttu-id="e181e-175">Hayır</span><span class="sxs-lookup"><span data-stu-id="e181e-175">No</span></span> |
| <span data-ttu-id="e181e-176">Biçimi</span><span class="sxs-lookup"><span data-stu-id="e181e-176">format</span></span> | <span data-ttu-id="e181e-177">şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="e181e-177">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="e181e-178">Set hello **türü** biçimi tooone şu değerlerden biri altında özellik.</span><span class="sxs-lookup"><span data-stu-id="e181e-178">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="e181e-179">Merhaba daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [JSON biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi ](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="e181e-179">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="e181e-180">Toocopy dosyaları olarak istiyorsanız-dosya tabanlı depolar (ikili kopya), her iki girdi ve çıktı veri kümesi tanımları Atla hello biçimi bölümünde arasındadır.</span><span class="sxs-lookup"><span data-stu-id="e181e-180">If you want toocopy files as-is between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="e181e-181">Hayır</span><span class="sxs-lookup"><span data-stu-id="e181e-181">No</span></span> | |
| <span data-ttu-id="e181e-182">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="e181e-182">compression</span></span> | <span data-ttu-id="e181e-183">Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin.</span><span class="sxs-lookup"><span data-stu-id="e181e-183">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="e181e-184">desteklenen hello türleri şunlardır: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="e181e-184">hello supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="e181e-185">desteklenen hello düzeyleri şunlardır: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="e181e-185">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="e181e-186">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="e181e-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="e181e-187">Hayır</span><span class="sxs-lookup"><span data-stu-id="e181e-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="e181e-188">**bucketName + tuşu** hello S3 nesnesinin burada demet hello S3 nesneleri için kök kapsayıcı ve anahtarıdır hello tam yol toohello S3 nesnesini hello konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="e181e-188">**bucketName + key** specifies hello location of hello S3 object, where bucket is hello root container for S3 objects, and key is hello full path toohello S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="e181e-189">Örnek veri kümesi önekiyle</span><span class="sxs-lookup"><span data-stu-id="e181e-189">Sample dataset with prefix</span></span>

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
### <a name="sample-dataset-with-version"></a><span data-ttu-id="e181e-190">Örnek veri kümesi (sürümüyle)</span><span class="sxs-lookup"><span data-stu-id="e181e-190">Sample dataset (with version)</span></span>

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

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="e181e-191">S3 için dinamik yollar</span><span class="sxs-lookup"><span data-stu-id="e181e-191">Dynamic paths for S3</span></span>
<span data-ttu-id="e181e-192">Merhaba önceki örnek sabit değerleri Merhaba kullanır **anahtar** ve **bucketName** hello Amazon S3 dataset özelliklerinde.</span><span class="sxs-lookup"><span data-stu-id="e181e-192">hello preceding sample uses fixed values for hello **key** and **bucketName** properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="e181e-193">Veri Fabrikası SliceStart gibi sistem değişkenleri kullanarak çalışma zamanında dinamik olarak bu özellikleri hesaplama olabilir.</span><span class="sxs-lookup"><span data-stu-id="e181e-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="e181e-194">Yapabileceğiniz aynı Merhaba hello **önek** bir Amazon S3 dataset özelliğinin.</span><span class="sxs-lookup"><span data-stu-id="e181e-194">You can do hello same for hello **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="e181e-195">Desteklenen işlevleri ve değişkenler listesi için bkz: [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="e181e-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="e181e-196">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="e181e-196">Copy activity properties</span></span>
<span data-ttu-id="e181e-197">Bölümleri ve etkinlikleri tanımlamak için kullanılabilen özellikleri tam listesi için bkz: [ardışık düzen oluşturma](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="e181e-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="e181e-198">Ad, açıklama, giriş ve çıkış tabloları ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e181e-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="e181e-199">Hello kullanılabilen özellikleri **typeProperties** hello etkinlik bölümünü her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="e181e-199">Properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="e181e-200">Merhaba kopya etkinliği için özellikler hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="e181e-200">For hello copy activity, properties vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="e181e-201">Merhaba kopyalama etkinliğinde bir kaynak türü olduğunda **FileSystemSource** (içeren Amazon S3), özellik aşağıdaki hello sağlanmıştır **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="e181e-201">When a source in hello copy activity is of type **FileSystemSource** (which includes Amazon S3), hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="e181e-202">Özellik</span><span class="sxs-lookup"><span data-stu-id="e181e-202">Property</span></span> | <span data-ttu-id="e181e-203">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e181e-203">Description</span></span> | <span data-ttu-id="e181e-204">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="e181e-204">Allowed values</span></span> | <span data-ttu-id="e181e-205">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e181e-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e181e-206">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="e181e-206">recursive</span></span> |<span data-ttu-id="e181e-207">Toorecursively listesi S3 hello dizini altında nesneleri olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e181e-207">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="e181e-208">true/false</span><span class="sxs-lookup"><span data-stu-id="e181e-208">true/false</span></span> |<span data-ttu-id="e181e-209">Hayır</span><span class="sxs-lookup"><span data-stu-id="e181e-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a><span data-ttu-id="e181e-210">JSON örnek: Amazon S3 tooAzure Blob Depolama veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="e181e-210">JSON example: Copy data from Amazon S3 tooAzure Blob storage</span></span>
<span data-ttu-id="e181e-211">Bu örnek göstermektedir nasıl toocopy verileri Amazon S3 tooan Azure Blob Depolama.</span><span class="sxs-lookup"><span data-stu-id="e181e-211">This sample shows how toocopy data from Amazon S3 tooan Azure Blob storage.</span></span> <span data-ttu-id="e181e-212">Ancak, verileri doğrudan çok kopyalanabilir[desteklenen hello havuzlarını hiçbirini](data-factory-data-movement-activities.md#supported-data-stores-and-formats) veri fabrikasında hello kopyalama etkinliği kullanarak.</span><span class="sxs-lookup"><span data-stu-id="e181e-212">However, data can be copied directly too[any of hello sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using hello copy activity in Data Factory.</span></span>

<span data-ttu-id="e181e-213">Merhaba örnek Data Factory varlıklarını aşağıdaki hello için JSON tanımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="e181e-213">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="e181e-214">Hello kullanarak bu tanımları toocreate Amazon S3 tooBlob depolama, ardışık düzen toocopy verilerden kullanabileceğiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), veya [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e181e-214">You can use these definitions toocreate a pipeline toocopy data from Amazon S3 tooBlob storage, by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="e181e-215">Bağlı hizmet türü [AwsAccessKey](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e181e-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="e181e-216">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e181e-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="e181e-217">Bir giriş [dataset](data-factory-create-datasets.md) türü [AmazonS3](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e181e-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="e181e-218">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e181e-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="e181e-219">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [FileSystemSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="e181e-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="e181e-220">Merhaba örnek verileri Amazon S3 tooan Azure blob ' saatte kopyalar.</span><span class="sxs-lookup"><span data-stu-id="e181e-220">hello sample copies data from Amazon S3 tooan Azure blob every hour.</span></span> <span data-ttu-id="e181e-221">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e181e-221">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="e181e-222">Amazon S3 bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="e181e-222">Amazon S3 linked service</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="e181e-223">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="e181e-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="e181e-224">Amazon S3 girdi veri kümesi</span><span class="sxs-lookup"><span data-stu-id="e181e-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="e181e-225">Ayarı **"dış": true** hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olduğunu bildirir.</span><span class="sxs-lookup"><span data-stu-id="e181e-225">Setting **"external": true** informs hello Data Factory service that hello dataset is external toohello data factory.</span></span> <span data-ttu-id="e181e-226">Bu özellik tootrue hello ardışık düzeninde bir etkinlik tarafından üretilen olmayan bir girdi veri kümesi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e181e-226">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

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


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="e181e-227">Azure Blob çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="e181e-227">Azure Blob output dataset</span></span>

<span data-ttu-id="e181e-228">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="e181e-228">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e181e-229">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="e181e-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="e181e-230">Merhaba klasör yolu hello yıl, ay, gün ve saat bölümlerini hello başlangıç saatini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e181e-230">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="e181e-231">Bir Amazon S3 kaynak ve blob havuz sahip işlem hattı kopyalama etkinliği</span><span class="sxs-lookup"><span data-stu-id="e181e-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="e181e-232">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="e181e-232">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="e181e-233">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**FileSystemSource**, ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="e181e-233">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

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
> <span data-ttu-id="e181e-234">Kaynak veri kümesi toocolumns bir havuz veri kümesinden toomap sütunlarından bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="e181e-234">toomap columns from a source dataset toocolumns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="e181e-235">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e181e-235">Next steps</span></span>
<span data-ttu-id="e181e-236">Aşağıdaki makaleleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="e181e-236">See hello following articles:</span></span>

* <span data-ttu-id="e181e-237">anahtarı hakkında toolearn Etkenler etkisi performans veri fabrikasında (kopyalama etkinliği) veri hareketlerini ve çeşitli yolları toooptimize, hello bkz [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="e181e-237">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="e181e-238">Kopyalama etkinliği ile işlem hattı oluşturmak için adım adım yönergeler için bkz: Merhaba [kopyalama etkinliği Öğreticisi](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="e181e-238">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
