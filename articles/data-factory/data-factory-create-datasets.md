---
title: "Azure Data Factory'de veri kümeleri oluşturma | Microsoft Docs"
description: "Uzaklık ve anchorDateTime gibi özellikleri kullanma örnekleri içeren Azure Data Factory'de veri kümeleri oluşturmayı öğrenin."
keywords: "veri kümesi, veri kümesi örnek oluşturma, örnek uzaklığı"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 6fd58edd830df8ea3f77a68e8dfcaf6de055b17c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="datasets-in-azure-data-factory"></a><span data-ttu-id="b2294-104">Azure Data Factory'deki veri kümelerini</span><span class="sxs-lookup"><span data-stu-id="b2294-104">Datasets in Azure Data Factory</span></span>
<span data-ttu-id="b2294-105">Bu makalede hangi veri kümeleri, JSON biçiminde nasıl tanımlanan açıklanmıştır ve Azure Data Factory içinde kullanılan nasıl ardışık düzenleri.</span><span class="sxs-lookup"><span data-stu-id="b2294-105">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span></span> <span data-ttu-id="b2294-106">Bu veri kümesi JSON tanımında her bölüm (örneğin, yapısı, kullanılabilirlik ve ilke) hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2294-106">It provides details about each section (for example, structure, availability, and policy) in the dataset JSON definition.</span></span> <span data-ttu-id="b2294-107">Ayrıca makale kullanmaya ilişkin örnekler verilmektedir **uzaklık**, **anchorDateTime**, ve **stili** dataset JSON tanımında özellikleri.</span><span class="sxs-lookup"><span data-stu-id="b2294-107">The article also provides examples for using the **offset**, **anchorDateTime**, and **style** properties in a dataset JSON definition.</span></span>

> [!NOTE]
> <span data-ttu-id="b2294-108">Data factory'yi yeni istiyorsanız bkz [Azure Data Factory'ye giriş](data-factory-introduction.md) bir genel bakış.</span><span class="sxs-lookup"><span data-stu-id="b2294-108">If you are new to Data Factory, see [Introduction to Azure Data Factory](data-factory-introduction.md) for an overview.</span></span> <span data-ttu-id="b2294-109">Veri fabrikaları oluşturma ile uygulamalı deneyim yoksa daha iyi okuyarak anlamak kazanmadan [veri dönüştürme öğretici](data-factory-build-your-first-pipeline.md) ve [veri taşıma Öğreticisi](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b2294-109">If you do not have hands-on experience with creating data factories, you can gain a better understanding by reading the [data transformation tutorial](data-factory-build-your-first-pipeline.md) and the [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="b2294-110">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b2294-110">Overview</span></span>
<span data-ttu-id="b2294-111">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b2294-111">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="b2294-112">A **ardışık düzen** mantıksal bir gruplandırmasıdır **etkinlikleri** görev birlikte gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="b2294-112">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="b2294-113">Ardışık etkinlikler, verilerinizde gerçekleştirilecek eylemleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b2294-113">The activities in a pipeline define actions to perform on your data.</span></span> <span data-ttu-id="b2294-114">Örneğin, bir şirket içi SQL Server'dan Azure Blob depolama alanına veri kopyalamak için kopyalama etkinliği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2294-114">For example, you might use a copy activity to copy data from an on-premises SQL Server to Azure Blob storage.</span></span> <span data-ttu-id="b2294-115">Ardından, veri işlemek için çıktı verileri üretemedi Blob depolama alanından gönderilmiş olan bir Azure Hdınsight kümesinde bir Hive betiği çalıştıran bir Hive etkinliği kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="b2294-115">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster to process data from Blob storage to produce output data.</span></span> <span data-ttu-id="b2294-116">Son olarak, çıktı verilerini Azure SQL Data Warehouse için çözümleri yerleşik raporlama hangi iş zekası üstünde (BI) kopyalamak için ikinci bir kopyalama etkinliği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2294-116">Finally, you might use a second copy activity to copy the output data to Azure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="b2294-117">Ardışık Düzen ve etkinlikleri hakkında daha fazla bilgi için bkz: [işlem hatlarının ve etkinliklerin Azure Data Factory](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="b2294-117">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md).</span></span>

<span data-ttu-id="b2294-118">Bir etkinlik sıfır veya daha fazla giriş alabilir **veri kümeleri**ve bir veya daha fazla çıkış veri kümeleri oluşturma.</span><span class="sxs-lookup"><span data-stu-id="b2294-118">An activity can take zero or more input **datasets**, and produce one or more output datasets.</span></span> <span data-ttu-id="b2294-119">Bir giriş veri kümesi işlem hattındaki bir etkinliğin girdi ve çıktı veri kümesi etkinliğinin çıkış temsil eder.</span><span class="sxs-lookup"><span data-stu-id="b2294-119">An input dataset represents the input for an activity in the pipeline, and an output dataset represents the output for the activity.</span></span> <span data-ttu-id="b2294-120">Veri kümeleri tablolar, dosyalar, klasörler ve belgeler gibi farklı veri depoları içindeki verileri tanımlamak.</span><span class="sxs-lookup"><span data-stu-id="b2294-120">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="b2294-121">Örneğin, bir Azure Blob dataset ardışık düzen veri okumalısınız Blob depolama alanına blob kapsayıcısı ve klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2294-121">For example, an Azure Blob dataset specifies the blob container and folder in Blob storage from which the pipeline should read the data.</span></span> 

<span data-ttu-id="b2294-122">Bir veri kümesi oluşturmadan önce oluşturun bir **bağlantılı hizmeti** data factory veri deponuza bağlamak için.</span><span class="sxs-lookup"><span data-stu-id="b2294-122">Before you create a dataset, create a **linked service** to link your data store to the data factory.</span></span> <span data-ttu-id="b2294-123">Bağlı hizmetler, dış kaynaklara bağlanmak için Data Factory’ye gereken bağlantı bilgilerini tanımlayan bağlantı dizelerine çok benzer.</span><span class="sxs-lookup"><span data-stu-id="b2294-123">Linked services are much like connection strings, which define the connection information needed for Data Factory to connect to external resources.</span></span> <span data-ttu-id="b2294-124">Veri kümelerini SQL tablolarının, dosyalar, klasörler ve belgeler gibi bağlantılı veri depoları içindeki verileri tanımlamak.</span><span class="sxs-lookup"><span data-stu-id="b2294-124">Datasets identify data within the linked data stores, such as SQL tables, files, folders, and documents.</span></span> <span data-ttu-id="b2294-125">Örneğin, bir Azure depolama hizmeti bağlantıları bir depolama hesabı data factory bağlantılı.</span><span class="sxs-lookup"><span data-stu-id="b2294-125">For example, an Azure Storage linked service links a storage account to the data factory.</span></span> <span data-ttu-id="b2294-126">Bir Azure Blob dataset blob kapsayıcısında ve işlenmesi için girdi BLOB'lar içeren klasörü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="b2294-126">An Azure Blob dataset represents the blob container and the folder that contains the input blobs to be processed.</span></span> 

<span data-ttu-id="b2294-127">Bir örnek senaryo aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b2294-127">Here is a sample scenario.</span></span> <span data-ttu-id="b2294-128">Blob depolama alanından bir SQL veritabanına veri kopyalamak için iki bağlı hizmet oluşturma: Azure Storage ve Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="b2294-128">To copy data from Blob storage to a SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="b2294-129">Ardından, iki veri kümesi oluşturun: (Azure Storage bağlı hizmeti ifade eder) Azure Blob veri kümesi ve (Azure SQL bağlı veritabanı hizmeti ifade eder) Azure SQL tablosu veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="b2294-129">Then, create two datasets: Azure Blob dataset (which refers to the Azure Storage linked service) and Azure SQL Table dataset (which refers to the Azure SQL Database linked service).</span></span> <span data-ttu-id="b2294-130">Azure Storage ve Azure SQL veritabanı bağlı Hizmetleri, Azure Storage ve Azure SQL Database, sırasıyla bağlanmak için çalışma zamanında Data Factory kullandığı bağlantı dizeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b2294-130">The Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime to connect to your Azure Storage and Azure SQL Database, respectively.</span></span> <span data-ttu-id="b2294-131">Azure Blob dataset blob kapsayıcısı ve Blob Depolama alanınızın giriş bloblar içeren blob klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2294-131">The Azure Blob dataset specifies the blob container and blob folder that contains the input blobs in your Blob storage.</span></span> <span data-ttu-id="b2294-132">Azure SQL tablosu veri kümesi SQL tablosu SQL veritabanınız veri ekleneceğine dair belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2294-132">The Azure SQL Table dataset specifies the SQL table in your SQL database to which the data is to be copied.</span></span>

<span data-ttu-id="b2294-133">Aşağıdaki diyagramda, veri fabrikasında ardışık düzen, etkinlik, veri kümesi ve bağlı hizmet arasındaki ilişkiler gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="b2294-133">The following diagram shows the relationships among pipeline, activity, dataset, and linked service in Data Factory:</span></span> 

![Ardışık düzen, etkinlik, veri kümesi, bağlı hizmetler arasındaki ilişki](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a><span data-ttu-id="b2294-135">JSON veri kümesi</span><span class="sxs-lookup"><span data-stu-id="b2294-135">Dataset JSON</span></span>
<span data-ttu-id="b2294-136">Veri fabrikasında bir veri kümesini JSON biçiminde şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="b2294-136">A dataset in Data Factory is defined in JSON format as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag to indicate external data. only for input datasets>,
        "linkedServiceName": "<Name of the linked service that refers to a data store.>",
        "structure": [
            {
                "name": "<Name of the column>",
                "type": "<Name of the type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies the time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies the interval within the defined frequency. For example, frequency set to 'Hour' and interval set to 1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="b2294-137">Aşağıdaki tabloda yukarıdaki JSON özelliklerinde açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="b2294-137">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="b2294-138">Özellik</span><span class="sxs-lookup"><span data-stu-id="b2294-138">Property</span></span> | <span data-ttu-id="b2294-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b2294-139">Description</span></span> | <span data-ttu-id="b2294-140">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b2294-140">Required</span></span> | <span data-ttu-id="b2294-141">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="b2294-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b2294-142">ad</span><span class="sxs-lookup"><span data-stu-id="b2294-142">name</span></span> |<span data-ttu-id="b2294-143">Veri kümesi adı.</span><span class="sxs-lookup"><span data-stu-id="b2294-143">Name of the dataset.</span></span> <span data-ttu-id="b2294-144">Bkz: [Azure Data Factory - adlandırma kuralları](data-factory-naming-rules.md) adlandırma kuralları.</span><span class="sxs-lookup"><span data-stu-id="b2294-144">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="b2294-145">Evet</span><span class="sxs-lookup"><span data-stu-id="b2294-145">Yes</span></span> |<span data-ttu-id="b2294-146">NA</span><span class="sxs-lookup"><span data-stu-id="b2294-146">NA</span></span> |
| <span data-ttu-id="b2294-147">type</span><span class="sxs-lookup"><span data-stu-id="b2294-147">type</span></span> |<span data-ttu-id="b2294-148">Veri kümesi türü.</span><span class="sxs-lookup"><span data-stu-id="b2294-148">Type of the dataset.</span></span> <span data-ttu-id="b2294-149">Data Factory ile desteklenen türlerden biri belirtin (örneğin: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="b2294-149">Specify one of the types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="b2294-150">Ayrıntılar için bkz [veri kümesi türü](#Type).</span><span class="sxs-lookup"><span data-stu-id="b2294-150">For details, see [Dataset type](#Type).</span></span> |<span data-ttu-id="b2294-151">Evet</span><span class="sxs-lookup"><span data-stu-id="b2294-151">Yes</span></span> |<span data-ttu-id="b2294-152">NA</span><span class="sxs-lookup"><span data-stu-id="b2294-152">NA</span></span> |
| <span data-ttu-id="b2294-153">yapısı</span><span class="sxs-lookup"><span data-stu-id="b2294-153">structure</span></span> |<span data-ttu-id="b2294-154">Veri kümesi şemasını.</span><span class="sxs-lookup"><span data-stu-id="b2294-154">Schema of the dataset.</span></span><br/><br/><span data-ttu-id="b2294-155">Ayrıntılar için bkz [veri kümesi yapısı](#Structure).</span><span class="sxs-lookup"><span data-stu-id="b2294-155">For details, see [Dataset structure](#Structure).</span></span> |<span data-ttu-id="b2294-156">Hayır</span><span class="sxs-lookup"><span data-stu-id="b2294-156">No</span></span> |<span data-ttu-id="b2294-157">NA</span><span class="sxs-lookup"><span data-stu-id="b2294-157">NA</span></span> |
| <span data-ttu-id="b2294-158">typeProperties</span><span class="sxs-lookup"><span data-stu-id="b2294-158">typeProperties</span></span> | <span data-ttu-id="b2294-159">Tür özellikleri her türü için farklı (örneğin: Azure Blob, Azure SQL tablosu).</span><span class="sxs-lookup"><span data-stu-id="b2294-159">The type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="b2294-160">Desteklenen türler ve özellikleri hakkında daha fazla bilgi için bkz: [veri kümesi türü](#Type).</span><span class="sxs-lookup"><span data-stu-id="b2294-160">For details on the supported types and their properties, see [Dataset type](#Type).</span></span> |<span data-ttu-id="b2294-161">Evet</span><span class="sxs-lookup"><span data-stu-id="b2294-161">Yes</span></span> |<span data-ttu-id="b2294-162">NA</span><span class="sxs-lookup"><span data-stu-id="b2294-162">NA</span></span> |
| <span data-ttu-id="b2294-163">external</span><span class="sxs-lookup"><span data-stu-id="b2294-163">external</span></span> | <span data-ttu-id="b2294-164">Bir veri kümesi açıkça data factory işlem hattı tarafından veya üretilen olup olmadığını belirlemek için mantıksal bayrak.</span><span class="sxs-lookup"><span data-stu-id="b2294-164">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> <span data-ttu-id="b2294-165">Bir etkinliğin girdi veri kümesi geçerli ardışık düzen tarafından üretilen değil, bu bayrağı true olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b2294-165">If the input dataset for an activity is not produced by the current pipeline, set this flag to true.</span></span> <span data-ttu-id="b2294-166">Bu bayrak düzenindeki ilk etkinliğin girdi veri kümesi için true olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b2294-166">Set this flag to true for the input dataset of the first activity in the pipeline.</span></span>  |<span data-ttu-id="b2294-167">Hayır</span><span class="sxs-lookup"><span data-stu-id="b2294-167">No</span></span> |<span data-ttu-id="b2294-168">False</span><span class="sxs-lookup"><span data-stu-id="b2294-168">false</span></span> |
| <span data-ttu-id="b2294-169">availability</span><span class="sxs-lookup"><span data-stu-id="b2294-169">availability</span></span> | <span data-ttu-id="b2294-170">İşleme penceresi (örneğin, saatlik veya günlük) veya veri kümesi üretim dilimleme modelini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b2294-170">Defines the processing window (for example, hourly or daily) or the slicing model for the dataset production.</span></span> <span data-ttu-id="b2294-171">Her veri birimi, tüketilen ve etkinlik çalışması tarafından üretilen veri dilimi adı verilir.</span><span class="sxs-lookup"><span data-stu-id="b2294-171">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="b2294-172">Bir çıkış veri kümesi kullanılabilirliğini (sıklığı - Day, aralığı - 1) günlük olarak ayarlanırsa, bir dilim günlük oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b2294-172">If the availability of an output dataset is set to daily (frequency - Day, interval - 1), a slice is produced daily.</span></span> <br/><br/><span data-ttu-id="b2294-173">Ayrıntılar için bkz [Dataset kullanılabilirliği](#Availability).</span><span class="sxs-lookup"><span data-stu-id="b2294-173">For details, see [Dataset availability](#Availability).</span></span> <br/><br/><span data-ttu-id="b2294-174">Model dilimleme veri kümesi hakkında daha fazla bilgi için bkz: [zamanlama ve yürütme](data-factory-scheduling-and-execution.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="b2294-174">For details on the dataset slicing model, see the [Scheduling and execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="b2294-175">Evet</span><span class="sxs-lookup"><span data-stu-id="b2294-175">Yes</span></span> |<span data-ttu-id="b2294-176">NA</span><span class="sxs-lookup"><span data-stu-id="b2294-176">NA</span></span> |
| <span data-ttu-id="b2294-177">İlke</span><span class="sxs-lookup"><span data-stu-id="b2294-177">policy</span></span> |<span data-ttu-id="b2294-178">Ölçüt ya da veri kümesi dilimler karşılamanız gerekmektedir koşulu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b2294-178">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="b2294-179">Ayrıntılar için bkz [Dataset İlkesi](#Policy) bölümü.</span><span class="sxs-lookup"><span data-stu-id="b2294-179">For details, see the [Dataset policy](#Policy) section.</span></span> |<span data-ttu-id="b2294-180">Hayır</span><span class="sxs-lookup"><span data-stu-id="b2294-180">No</span></span> |<span data-ttu-id="b2294-181">NA</span><span class="sxs-lookup"><span data-stu-id="b2294-181">NA</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="b2294-182">Veri kümesi örneği</span><span class="sxs-lookup"><span data-stu-id="b2294-182">Dataset example</span></span>
<span data-ttu-id="b2294-183">Aşağıdaki örnekte, adlı bir tablo veri kümesini temsil eden **MyTable** bir SQL veritabanında.</span><span class="sxs-lookup"><span data-stu-id="b2294-183">In the following example, the dataset represents a table named **MyTable** in a SQL database.</span></span>

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="b2294-184">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="b2294-184">Note the following points:</span></span>

* <span data-ttu-id="b2294-185">**tür** AzureSqlTable için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b2294-185">**type** is set to AzureSqlTable.</span></span>
* <span data-ttu-id="b2294-186">**tableName** type özelliği (AzureSqlTable türüne belirli) MyTable için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b2294-186">**tableName** type property (specific to AzureSqlTable type) is set to MyTable.</span></span>
* <span data-ttu-id="b2294-187">**linkedServiceName** sonraki JSON parçacığında tanımlanan AzureSqlDatabase türündeki bağlı hizmetin başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="b2294-187">**linkedServiceName** refers to a linked service of type AzureSqlDatabase, which is defined in the next JSON snippet.</span></span> 
* <span data-ttu-id="b2294-188">**Kullanılabilirlik sıklığı** gün olarak ayarlanır ve **aralığı** 1 olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b2294-188">**availability frequency** is set to Day, and **interval** is set to 1.</span></span> <span data-ttu-id="b2294-189">Bu veri kümesi dilim günlük üretilen anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b2294-189">This means that the dataset slice is produced daily.</span></span>  

<span data-ttu-id="b2294-190">**AzureSqlLinkedService** şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="b2294-190">**AzureSqlLinkedService** is defined as follows:</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

<span data-ttu-id="b2294-191">Yukarıdaki JSON parçacığında:</span><span class="sxs-lookup"><span data-stu-id="b2294-191">In the preceding JSON snippet:</span></span>

* <span data-ttu-id="b2294-192">**tür** AzureSqlDatabase için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b2294-192">**type** is set to AzureSqlDatabase.</span></span>
* <span data-ttu-id="b2294-193">**connectionString** türü özelliği, bir SQL veritabanına bağlanmak için gereken bilgileri belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2294-193">**connectionString** type property specifies information to connect to a SQL database.</span></span>  

<span data-ttu-id="b2294-194">Gördüğünüz gibi bağlantılı hizmet bir SQL veritabanına bağlanma tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b2294-194">As you can see, the linked service defines how to connect to a SQL database.</span></span> <span data-ttu-id="b2294-195">Hangi tablo girdi olarak kullanılır ve bir ardışık düzen etkinliğin çıktı veri kümesi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b2294-195">The dataset defines what table is used as an input and output for the activity in a pipeline.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="b2294-196">Bir veri kümesi ardışık düzen tarafından üretilen sürece bunu olarak işaretlenmelidir **dış**.</span><span class="sxs-lookup"><span data-stu-id="b2294-196">Unless a dataset is being produced by the pipeline, it should be marked as **external**.</span></span> <span data-ttu-id="b2294-197">Bu ayar genellikle bir ardışık düzendeki ilk etkinlik girişleri için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b2294-197">This setting generally applies to inputs of first activity in a pipeline.</span></span>   


## <span data-ttu-id="b2294-198"><a name="Type"></a>Veri kümesi türü</span><span class="sxs-lookup"><span data-stu-id="b2294-198"><a name="Type"></a> Dataset type</span></span>
<span data-ttu-id="b2294-199">Veri kümesi türü kullandığınız veri deposunda bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b2294-199">The type of the dataset depends on the data store you use.</span></span> <span data-ttu-id="b2294-200">Data Factory ile desteklenen veri depoları listesi için aşağıdaki tabloya bakın.</span><span class="sxs-lookup"><span data-stu-id="b2294-200">See the following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="b2294-201">Bağlı hizmet ve bir veri kümesi, veri deposu için nasıl oluşturulacağını öğrenmek için bir veri deposu'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b2294-201">Click a data store to learn how to create a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="b2294-202">Veri depolar ile * şirket içi olabilir veya hizmet (Iaas) olarak Azure altyapısı.</span><span class="sxs-lookup"><span data-stu-id="b2294-202">Data stores with * can be on-premises or on Azure infrastructure as a service (IaaS).</span></span> <span data-ttu-id="b2294-203">Bu veri depolarına yüklemek ihtiyaç duyduğunuz [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="b2294-203">These data stores require you to install [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="b2294-204">Önceki bölümdeki örnekte dataset türünü ayarlamak **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="b2294-204">In the example in the previous section, the type of the dataset is set to **AzureSqlTable**.</span></span> <span data-ttu-id="b2294-205">Benzer şekilde, veri kümesi türü Azure Blob veri kümesi için ayarlanmış **AzureBlob**aşağıdaki JSON gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="b2294-205">Similarly, for an Azure Blob dataset, the type of the dataset is set to **AzureBlob**, as shown in the following JSON:</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

## <span data-ttu-id="b2294-206"><a name="Structure"></a>Veri kümesi yapısı</span><span class="sxs-lookup"><span data-stu-id="b2294-206"><a name="Structure"></a>Dataset structure</span></span>
<span data-ttu-id="b2294-207">**Yapısı** bölümdür isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b2294-207">The **structure** section is optional.</span></span> <span data-ttu-id="b2294-208">Dataset şeması tarafından içeren bir koleksiyon adları ve sütunların veri türlerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b2294-208">It defines the schema of the dataset by containing a collection of names and data types of columns.</span></span> <span data-ttu-id="b2294-209">Türleri dönüştürme ve kaynaktan hedef sütunlara eşlemek için kullanılan türü bilgileri sağlamak için yapısı bölümü kullanın.</span><span class="sxs-lookup"><span data-stu-id="b2294-209">You use the structure section to provide type information that is used to convert types and map columns from the source to the destination.</span></span> <span data-ttu-id="b2294-210">Aşağıdaki örnekte, üç sütun kümesi vardır: `slicetimestamp`, `projectname`, ve `pageviews`.</span><span class="sxs-lookup"><span data-stu-id="b2294-210">In the following example, the dataset has three columns: `slicetimestamp`, `projectname`, and `pageviews`.</span></span> <span data-ttu-id="b2294-211">Bunlar dize, dize ve ondalık, sırasıyla türüdür.</span><span class="sxs-lookup"><span data-stu-id="b2294-211">They are of type String, String, and Decimal, respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="b2294-212">Her sütun yapısı içinde aşağıdaki özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="b2294-212">Each column in the structure contains the following properties:</span></span>

| <span data-ttu-id="b2294-213">Özellik</span><span class="sxs-lookup"><span data-stu-id="b2294-213">Property</span></span> | <span data-ttu-id="b2294-214">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b2294-214">Description</span></span> | <span data-ttu-id="b2294-215">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b2294-215">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b2294-216">ad</span><span class="sxs-lookup"><span data-stu-id="b2294-216">name</span></span> |<span data-ttu-id="b2294-217">Sütunun adı.</span><span class="sxs-lookup"><span data-stu-id="b2294-217">Name of the column.</span></span> |<span data-ttu-id="b2294-218">Evet</span><span class="sxs-lookup"><span data-stu-id="b2294-218">Yes</span></span> |
| <span data-ttu-id="b2294-219">type</span><span class="sxs-lookup"><span data-stu-id="b2294-219">type</span></span> |<span data-ttu-id="b2294-220">Sütunun veri türü.</span><span class="sxs-lookup"><span data-stu-id="b2294-220">Data type of the column.</span></span>  |<span data-ttu-id="b2294-221">Hayır</span><span class="sxs-lookup"><span data-stu-id="b2294-221">No</span></span> |
| <span data-ttu-id="b2294-222">Kültür</span><span class="sxs-lookup"><span data-stu-id="b2294-222">culture</span></span> |<span data-ttu-id="b2294-223">. Tür .NET türü olduğunda kullanılacak NET tabanlı kültürü: `Datetime` veya `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="b2294-223">.NET-based culture to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="b2294-224">Varsayılan değer `en-us`.</span><span class="sxs-lookup"><span data-stu-id="b2294-224">The default is `en-us`.</span></span> |<span data-ttu-id="b2294-225">Hayır</span><span class="sxs-lookup"><span data-stu-id="b2294-225">No</span></span> |
| <span data-ttu-id="b2294-226">Biçimi</span><span class="sxs-lookup"><span data-stu-id="b2294-226">format</span></span> |<span data-ttu-id="b2294-227">Biçim türü .NET türü olduğunda kullanılacak dize: `Datetime` veya `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="b2294-227">Format string to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="b2294-228">Hayır</span><span class="sxs-lookup"><span data-stu-id="b2294-228">No</span></span> |

<span data-ttu-id="b2294-229">Aşağıdaki yönergeleri yapısı bilgileri içerecek şekilde ne zaman ve ne eklenecek belirlemenize yardımcı **yapısı** bölümü.</span><span class="sxs-lookup"><span data-stu-id="b2294-229">The following guidelines help you determine when to include structure information, and what to include in the **structure** section.</span></span>

* <span data-ttu-id="b2294-230">**Yapılandırılmış veri kaynakları için**, yalnızca sütun havuz için kaynak sütunları eşlemek istediğiniz ve adlarının aynı olmayan yapısı bölüm belirtin.</span><span class="sxs-lookup"><span data-stu-id="b2294-230">**For structured data sources**, specify the structure section only if you want map source columns to sink columns, and their names are not the same.</span></span> <span data-ttu-id="b2294-231">Bu türdeki yapılandırılmış veri kaynağının veri yanı sıra veri şeması ve tür bilgileri depolar.</span><span class="sxs-lookup"><span data-stu-id="b2294-231">This kind of structured data source stores data schema and type information along with the data itself.</span></span> <span data-ttu-id="b2294-232">SQL Server, Oracle ve Azure tablo yapılandırılmış veri kaynakları örneklerindendir.</span><span class="sxs-lookup"><span data-stu-id="b2294-232">Examples of structured data sources include SQL Server, Oracle, and Azure table.</span></span> 
  
    <span data-ttu-id="b2294-233">Tür bilgileri zaten yapılandırılmış veri kaynakları için kullanılabilir olduğundan yapısı bölüm eklediğinizde türü bilgileri içermemelidir.</span><span class="sxs-lookup"><span data-stu-id="b2294-233">As type information is already available for structured data sources, you should not include type information when you do include the structure section.</span></span>
* <span data-ttu-id="b2294-234">**Şema okuma veri kaynaklarında (özellikle Blob Depolama) için**, herhangi bir şema veya türü bilgi verilerle depolamadan veri depolamayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2294-234">**For schema on read data sources (specifically Blob storage)**, you can choose to store data without storing any schema or type information with the data.</span></span> <span data-ttu-id="b2294-235">Sütunları havuz için kaynak sütunları eşleme istediğinizde bu tür veri kaynağı yapısı içerir.</span><span class="sxs-lookup"><span data-stu-id="b2294-235">For these types of data sources, include structure when you want to map source columns to sink columns.</span></span> <span data-ttu-id="b2294-236">Ayrıca yapısı kopyalama etkinliği için bir giriş veri kümesi olduğunda ve kaynak veri kümesinin veri türleri yerel türleri için havuz dönüştürülüp içerir.</span><span class="sxs-lookup"><span data-stu-id="b2294-236">Also include structure when the dataset is an input for a copy activity, and data types of source dataset should be converted to native types for the sink.</span></span> 
    
    <span data-ttu-id="b2294-237">Veri Fabrikası yapısındaki türü bilgileri sağlamak için aşağıdaki değerleri destekler: **Int16, Int32, Int64, tek, Double, Decimal, bayt [], Boolean, dize, GUID, Datetime, Datetimeoffset ve Timespan**.</span><span class="sxs-lookup"><span data-stu-id="b2294-237">Data Factory supports the following values for providing type information in structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**.</span></span> <span data-ttu-id="b2294-238">Ortak dil belirtimi (CLS) bu değerler-uyumlu. NET tabanlı türü değerleri.</span><span class="sxs-lookup"><span data-stu-id="b2294-238">These values are Common Language Specification (CLS)-compliant, .NET-based type values.</span></span>

<span data-ttu-id="b2294-239">Veri Fabrikası tür dönüşümleri veri bir havuz veri deposu için bir kaynak veri deposundan taşırken otomatik olarak gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="b2294-239">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span></span> 
  

## <a name="dataset-availability"></a><span data-ttu-id="b2294-240">DataSet kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="b2294-240">Dataset availability</span></span>
<span data-ttu-id="b2294-241">**Kullanılabilirlik** bir veri kümesi bölümünde veri kümesi için işleme penceresi (örneğin, saatlik, günlük veya haftalık) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b2294-241">The **availability** section in a dataset defines the processing window (for example, hourly, daily, or weekly) for the dataset.</span></span> <span data-ttu-id="b2294-242">Etkinlik pencereleri hakkında daha fazla bilgi için bkz: [zamanlama ve yürütme](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="b2294-242">For more information about activity windows, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>

<span data-ttu-id="b2294-243">Aşağıdaki kullanılabilirlik bölümü çıktı veri kümesi saatlik oluşturulur veya giriş veri kümesi saatlik kullanılabilir belirtir:</span><span class="sxs-lookup"><span data-stu-id="b2294-243">The following availability section specifies that the output dataset is either produced hourly, or the input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="b2294-244">Ardışık Düzen aşağıdaki başlangıç ve bitiş zamanları varsa:</span><span class="sxs-lookup"><span data-stu-id="b2294-244">If the pipeline has the following start and end times:</span></span>  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

<span data-ttu-id="b2294-245">Çıktı veri kümesi üretilen saatlik içinde ardışık düzeni başlangıç ve bitiş zamanları.</span><span class="sxs-lookup"><span data-stu-id="b2294-245">The output dataset is produced hourly within the pipeline start and end times.</span></span> <span data-ttu-id="b2294-246">Bu nedenle, bu ardışık düzen, her etkinlik penceresinin (00: 00-1 AM, 1 AM - 2 AM, 2: 00 - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM) için bir tane tarafından üretilen beş veri kümesi dilimler vardır.</span><span class="sxs-lookup"><span data-stu-id="b2294-246">Therefore, there are five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2 AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 

<span data-ttu-id="b2294-247">Aşağıdaki tabloda kullanılabilirlik bölümünde kullanabileceğiniz özellikleri açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="b2294-247">The following table describes properties you can use in the availability section:</span></span>

| <span data-ttu-id="b2294-248">Özellik</span><span class="sxs-lookup"><span data-stu-id="b2294-248">Property</span></span> | <span data-ttu-id="b2294-249">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b2294-249">Description</span></span> | <span data-ttu-id="b2294-250">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b2294-250">Required</span></span> | <span data-ttu-id="b2294-251">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="b2294-251">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b2294-252">Sıklık</span><span class="sxs-lookup"><span data-stu-id="b2294-252">frequency</span></span> |<span data-ttu-id="b2294-253">Veri kümesi dilim üretim için zaman birimini belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2294-253">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="b2294-254"><b>Sıklık desteklenen</b>: dakika, saat, gün, hafta, ay</span><span class="sxs-lookup"><span data-stu-id="b2294-254"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="b2294-255">Evet</span><span class="sxs-lookup"><span data-stu-id="b2294-255">Yes</span></span> |<span data-ttu-id="b2294-256">NA</span><span class="sxs-lookup"><span data-stu-id="b2294-256">NA</span></span> |
| <span data-ttu-id="b2294-257">aralığı</span><span class="sxs-lookup"><span data-stu-id="b2294-257">interval</span></span> |<span data-ttu-id="b2294-258">Sıklığı çarpanı belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2294-258">Specifies a multiplier for frequency.</span></span><br/><br/><span data-ttu-id="b2294-259">"X sıklığı aralığını" ne sıklıkta dilim üretilen belirler.</span><span class="sxs-lookup"><span data-stu-id="b2294-259">"Frequency x interval" determines how often the slice is produced.</span></span> <span data-ttu-id="b2294-260">Örneğin, veri kümesinin saatlik olarak başka bir dilimlenebilir gerekiyorsa, ayarladığınız <b>sıklığı</b> için <b>saat</b>, ve <b>aralığı</b> için <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="b2294-260">For example, if you need the dataset to be sliced on an hourly basis, you set <b>frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="b2294-261">Belirtirseniz unutmayın **sıklığı** olarak **Minute**, aralık en az 15 olarak ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2294-261">Note that if you specify **frequency** as **Minute**, you should set the interval to no less than 15.</span></span> |<span data-ttu-id="b2294-262">Evet</span><span class="sxs-lookup"><span data-stu-id="b2294-262">Yes</span></span> |<span data-ttu-id="b2294-263">NA</span><span class="sxs-lookup"><span data-stu-id="b2294-263">NA</span></span> |
| <span data-ttu-id="b2294-264">stili</span><span class="sxs-lookup"><span data-stu-id="b2294-264">style</span></span> |<span data-ttu-id="b2294-265">Dilim başlangıç veya Bitiş aralığı olarak üretilen belirtir.</span><span class="sxs-lookup"><span data-stu-id="b2294-265">Specifies whether the slice should be produced at the start or end of the interval.</span></span><ul><li><span data-ttu-id="b2294-266">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="b2294-266">StartOfInterval</span></span></li><li><span data-ttu-id="b2294-267">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="b2294-267">EndOfInterval</span></span></li></ul><span data-ttu-id="b2294-268">Varsa **sıklığı** ayarlanır **ay**, ve **stili** ayarlanır **EndOfInterval**, dilim ayın son gününde üretilir.</span><span class="sxs-lookup"><span data-stu-id="b2294-268">If **frequency** is set to **Month**, and **style** is set to **EndOfInterval**, the slice is produced on the last day of month.</span></span> <span data-ttu-id="b2294-269">Varsa **stili** ayarlanır **StartOfInterval**, dilim ayın ilk günü üretilir.</span><span class="sxs-lookup"><span data-stu-id="b2294-269">If **style** is set to **StartOfInterval**, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="b2294-270">Varsa **sıklığı** ayarlanır **gün**, ve **stili** ayarlanır **EndOfInterval**, dilim günün son bir saat içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b2294-270">If **frequency** is set to **Day**, and **style** is set to **EndOfInterval**, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="b2294-271">Varsa **sıklığı** ayarlanır **saat**, ve **stili** ayarlanır **EndOfInterval**, dilim saat sonunda üretilir.</span><span class="sxs-lookup"><span data-stu-id="b2294-271">If **frequency** is set to **Hour**, and **style** is set to **EndOfInterval**, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="b2294-272">Örneğin, 1 PM - 2 PM dönem için bir dilim için 2 saat dilimi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b2294-272">For example, for a slice for the 1 PM - 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="b2294-273">Hayır</span><span class="sxs-lookup"><span data-stu-id="b2294-273">No</span></span> |<span data-ttu-id="b2294-274">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="b2294-274">EndOfInterval</span></span> |
| <span data-ttu-id="b2294-275">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="b2294-275">anchorDateTime</span></span> |<span data-ttu-id="b2294-276">Veri kümesi dilim sınırlarını işlem için Zamanlayıcı tarafından kullanılan zaman içinde mutlak konum tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b2294-276">Defines the absolute position in time used by the scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="b2294-277">Bu propoerty belirtilen sıklığından daha ayrıntılı tarih kısımlarını varsa, daha ayrıntılı bölümleri göz ardı edilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b2294-277">Note that if this propoerty has date parts that are more granular than the specified frequency, the more granular parts are ignored.</span></span> <span data-ttu-id="b2294-278">Örneğin, varsa **aralığı** olan **saatlik** (sıklığı: saat ve aralığı: 1) ve **anchorDateTime** içeren **dakika ve saniyeleri**, sonra dakika ve saniyeleri bölümlerini **anchorDateTime** göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="b2294-278">For example, if the **interval** is **hourly** (frequency: hour and interval: 1), and the **anchorDateTime** contains **minutes and seconds**, then the minutes and seconds parts of **anchorDateTime** are ignored.</span></span> |<span data-ttu-id="b2294-279">Hayır</span><span class="sxs-lookup"><span data-stu-id="b2294-279">No</span></span> |<span data-ttu-id="b2294-280">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="b2294-280">01/01/0001</span></span> |
| <span data-ttu-id="b2294-281">uzaklık</span><span class="sxs-lookup"><span data-stu-id="b2294-281">offset</span></span> |<span data-ttu-id="b2294-282">Tarafından başlangıç ve bitiş tüm veri kümesi dilim gölgeye Timespan.</span><span class="sxs-lookup"><span data-stu-id="b2294-282">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="b2294-283">Her iki unutmayın **anchorDateTime** ve **uzaklık** belirtilirse, sonucudur birleşik shift.</span><span class="sxs-lookup"><span data-stu-id="b2294-283">Note that if both **anchorDateTime** and **offset** are specified, the result is the combined shift.</span></span> |<span data-ttu-id="b2294-284">Hayır</span><span class="sxs-lookup"><span data-stu-id="b2294-284">No</span></span> |<span data-ttu-id="b2294-285">NA</span><span class="sxs-lookup"><span data-stu-id="b2294-285">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="b2294-286">uzaklık örneği</span><span class="sxs-lookup"><span data-stu-id="b2294-286">offset example</span></span>
<span data-ttu-id="b2294-287">Varsayılan olarak, her gün (`"frequency": "Day", "interval": 1`) dilimler 00: 00 (gece yarısı) Eşgüdümlü Evrensel Saat (UTC) başlatın.</span><span class="sxs-lookup"><span data-stu-id="b2294-287">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM (midnight) Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="b2294-288">Başlangıç zamanı 6 AM UTC saati yerine olmasını istiyorsanız, uzaklık aşağıdaki kod parçacığında gösterildiği gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="b2294-288">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="b2294-289">anchorDateTime örneği</span><span class="sxs-lookup"><span data-stu-id="b2294-289">anchorDateTime example</span></span>
<span data-ttu-id="b2294-290">Aşağıdaki örnekte, veri kümesi 23 saatte bir kez oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b2294-290">In the following example, the dataset is produced once every 23 hours.</span></span> <span data-ttu-id="b2294-291">İlk dilim tarafından belirtilen zaman başlar **anchorDateTime**, ayarlanmış `2017-04-19T08:00:00` (UTC).</span><span class="sxs-lookup"><span data-stu-id="b2294-291">The first slice starts at the time specified by **anchorDateTime**, which is set to `2017-04-19T08:00:00` (UTC).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="b2294-292">uzaklık/stil örneği</span><span class="sxs-lookup"><span data-stu-id="b2294-292">offset/style example</span></span>
<span data-ttu-id="b2294-293">Aşağıdaki veri kümesi aylık ve 8: 00'da her ayın 3 üretilir (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="b2294-293">The following dataset is monthly, and is produced on the 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <span data-ttu-id="b2294-294"><a name="Policy"></a>Veri kümesi İlkesi</span><span class="sxs-lookup"><span data-stu-id="b2294-294"><a name="Policy"></a>Dataset policy</span></span>
<span data-ttu-id="b2294-295">**İlkesi** veri kümesi tanımı bölümünde ölçütleri veya veri kümesi dilimler karşılamanız gerekmektedir koşulu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b2294-295">The **policy** section in the dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

### <a name="validation-policies"></a><span data-ttu-id="b2294-296">Doğrulama ilkeleri</span><span class="sxs-lookup"><span data-stu-id="b2294-296">Validation policies</span></span>
| <span data-ttu-id="b2294-297">İlke adı</span><span class="sxs-lookup"><span data-stu-id="b2294-297">Policy name</span></span> | <span data-ttu-id="b2294-298">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b2294-298">Description</span></span> | <span data-ttu-id="b2294-299">Uygulanan</span><span class="sxs-lookup"><span data-stu-id="b2294-299">Applied to</span></span> | <span data-ttu-id="b2294-300">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b2294-300">Required</span></span> | <span data-ttu-id="b2294-301">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="b2294-301">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="b2294-302">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="b2294-302">minimumSizeMB</span></span> |<span data-ttu-id="b2294-303">Doğrular verilerde **Azure Blob Depolama** (megabayt cinsinden) en düşük boyut gereksinimlerini karşılıyor.</span><span class="sxs-lookup"><span data-stu-id="b2294-303">Validates that the data in **Azure Blob storage** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="b2294-304">Azure Blob depolama</span><span class="sxs-lookup"><span data-stu-id="b2294-304">Azure Blob storage</span></span> |<span data-ttu-id="b2294-305">Hayır</span><span class="sxs-lookup"><span data-stu-id="b2294-305">No</span></span> |<span data-ttu-id="b2294-306">NA</span><span class="sxs-lookup"><span data-stu-id="b2294-306">NA</span></span> |
| <span data-ttu-id="b2294-307">minimumRows</span><span class="sxs-lookup"><span data-stu-id="b2294-307">minimumRows</span></span> |<span data-ttu-id="b2294-308">Doğrular verilerde bir **Azure SQL veritabanı** veya bir **Azure tablo** en az satır sayısını içerir.</span><span class="sxs-lookup"><span data-stu-id="b2294-308">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="b2294-309">Azure SQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="b2294-309">Azure SQL database</span></span></li><li><span data-ttu-id="b2294-310">Azure tablo</span><span class="sxs-lookup"><span data-stu-id="b2294-310">Azure table</span></span></li></ul> |<span data-ttu-id="b2294-311">Hayır</span><span class="sxs-lookup"><span data-stu-id="b2294-311">No</span></span> |<span data-ttu-id="b2294-312">NA</span><span class="sxs-lookup"><span data-stu-id="b2294-312">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="b2294-313">Örnekler</span><span class="sxs-lookup"><span data-stu-id="b2294-313">Examples</span></span>
<span data-ttu-id="b2294-314">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="b2294-314">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="b2294-315">**minimumRows:**</span><span class="sxs-lookup"><span data-stu-id="b2294-315">**minimumRows:**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a><span data-ttu-id="b2294-316">Dış veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="b2294-316">External datasets</span></span>
<span data-ttu-id="b2294-317">Dış veri kümeleri veri fabrikası'nda çalışan bir ardışık düzen tarafından üretilmeyen olanlardır.</span><span class="sxs-lookup"><span data-stu-id="b2294-317">External datasets are the ones that are not produced by a running pipeline in the data factory.</span></span> <span data-ttu-id="b2294-318">Veri kümesi olarak işaretlenmişse **dış**, **ExternalData** İlkesi, veri kümesi dilim kullanılabilirlik davranışını etkilemek için tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="b2294-318">If the dataset is marked as **external**, the **ExternalData** policy may be defined to influence the behavior of the dataset slice availability.</span></span>

<span data-ttu-id="b2294-319">Bir veri kümesi Data Factory tarafından üretilen sürece bunu olarak işaretlenmelidir **dış**.</span><span class="sxs-lookup"><span data-stu-id="b2294-319">Unless a dataset is being produced by Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="b2294-320">Etkinlik veya ardışık düzen zincirleme kullanılmadığı sürece bu ayar genellikle ardışık düzendeki, ilk etkinliğin girdi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b2294-320">This setting generally applies to the inputs of first activity in a pipeline, unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="b2294-321">Ad</span><span class="sxs-lookup"><span data-stu-id="b2294-321">Name</span></span> | <span data-ttu-id="b2294-322">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b2294-322">Description</span></span> | <span data-ttu-id="b2294-323">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b2294-323">Required</span></span> | <span data-ttu-id="b2294-324">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="b2294-324">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b2294-325">dataDelay</span><span class="sxs-lookup"><span data-stu-id="b2294-325">dataDelay</span></span> |<span data-ttu-id="b2294-326">Verilen dilim için dış veri kullanılabilirliğini onay gecikme süresi.</span><span class="sxs-lookup"><span data-stu-id="b2294-326">The time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="b2294-327">Örneğin, bu ayarı kullanarak bir saatlik onay geciktirebilir.</span><span class="sxs-lookup"><span data-stu-id="b2294-327">For example, you can delay an hourly check by using this setting.</span></span><br/><br/><span data-ttu-id="b2294-328">Ayar, yalnızca mevcut süre için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b2294-328">The setting only applies to the present time.</span></span>  <span data-ttu-id="b2294-329">Örneğin, 1:00 PM şimdi ise ve bu değer 10 dakikadır doğrulama 13: 10'te başlatır.</span><span class="sxs-lookup"><span data-stu-id="b2294-329">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="b2294-330">Bu ayar geçmişte dilimler etkilemez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b2294-330">Note that this setting does not affect slices in the past.</span></span> <span data-ttu-id="b2294-331">İle dilimler **dilim bitiş saati** + **dataDelay** < **şimdi** herhangi bir gecikme işlenir.</span><span class="sxs-lookup"><span data-stu-id="b2294-331">Slices with **Slice End Time** + **dataDelay** < **Now** are processed without any delay.</span></span><br/><br/><span data-ttu-id="b2294-332">23:59 büyük saatleri saat kullanarak belirtilmelidir `day.hours:minutes:seconds` biçimi.</span><span class="sxs-lookup"><span data-stu-id="b2294-332">Times greater than 23:59 hours should be specified by using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="b2294-333">Örneğin, 24 saat belirtmek için 24:00:00 kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="b2294-333">For example, to specify 24 hours, don't use 24:00:00.</span></span> <span data-ttu-id="b2294-334">Bunun yerine, 1.00:00:00 kullanın.</span><span class="sxs-lookup"><span data-stu-id="b2294-334">Instead, use 1.00:00:00.</span></span> <span data-ttu-id="b2294-335">24:00:00 kullanırsanız, 24 gün (24.00:00:00) kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="b2294-335">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="b2294-336">1 gün ve 4 saat için 1:04:00:00 belirtin.</span><span class="sxs-lookup"><span data-stu-id="b2294-336">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="b2294-337">Hayır</span><span class="sxs-lookup"><span data-stu-id="b2294-337">No</span></span> |<span data-ttu-id="b2294-338">0</span><span class="sxs-lookup"><span data-stu-id="b2294-338">0</span></span> |
| <span data-ttu-id="b2294-339">Retryınterval</span><span class="sxs-lookup"><span data-stu-id="b2294-339">retryInterval</span></span> |<span data-ttu-id="b2294-340">Bir hata ve sonraki denemesi arasındaki bekleme süresi.</span><span class="sxs-lookup"><span data-stu-id="b2294-340">The wait time between a failure and the next attempt.</span></span> <span data-ttu-id="b2294-341">Bu ayar için mevcut zaman geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b2294-341">This setting applies to present time.</span></span> <span data-ttu-id="b2294-342">Önceki başarısız çalışırsanız, sonraki deneyin sonradır **Retryınterval** süresi.</span><span class="sxs-lookup"><span data-stu-id="b2294-342">If the previous try failed, the next try is after the **retryInterval** period.</span></span> <br/><br/><span data-ttu-id="b2294-343">1:00 PM şimdi ise, ilk denemede başlamadan.</span><span class="sxs-lookup"><span data-stu-id="b2294-343">If it is 1:00 PM right now, we begin the first try.</span></span> <span data-ttu-id="b2294-344">İlk doğrulama denetimi tamamlamak için süre 1 dakika ve işlem başarısız oldu, sonraki yeniden deneme ise 1:00 1 dak (süresi) + 1 dak (yeniden deneme aralığı) = 1:02 PM.</span><span class="sxs-lookup"><span data-stu-id="b2294-344">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="b2294-345">Geçmişte dilimler için gecikme yoktur.</span><span class="sxs-lookup"><span data-stu-id="b2294-345">For slices in the past, there is no delay.</span></span> <span data-ttu-id="b2294-346">Yeniden deneme hemen gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="b2294-346">The retry happens immediately.</span></span> |<span data-ttu-id="b2294-347">Hayır</span><span class="sxs-lookup"><span data-stu-id="b2294-347">No</span></span> |<span data-ttu-id="b2294-348">00:01:00 (1 dakika)</span><span class="sxs-lookup"><span data-stu-id="b2294-348">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="b2294-349">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="b2294-349">retryTimeout</span></span> |<span data-ttu-id="b2294-350">Yeniden deneme girişimleri için zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="b2294-350">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="b2294-351">Bu özellik 10 dakika olarak ayarlanırsa, doğrulama 10 dakika içinde tamamlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b2294-351">If this property is set to 10 minutes, the validation should be completed within 10 minutes.</span></span> <span data-ttu-id="b2294-352">Yeniden deneme doğrulamayı gerçekleştirmek için 10 dakikadan uzun sürüyorsa, zaman aşımına uğradı.</span><span class="sxs-lookup"><span data-stu-id="b2294-352">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="b2294-353">Tüm denemeleri doğrulama zaman aşımı için dilim olarak işaretlenmişse, **süresi sona erdi**.</span><span class="sxs-lookup"><span data-stu-id="b2294-353">If all attempts for the validation time out, the slice is marked as **TimedOut**.</span></span> |<span data-ttu-id="b2294-354">Hayır</span><span class="sxs-lookup"><span data-stu-id="b2294-354">No</span></span> |<span data-ttu-id="b2294-355">00:10:00 (10 dakika)</span><span class="sxs-lookup"><span data-stu-id="b2294-355">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="b2294-356">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="b2294-356">maximumRetry</span></span> |<span data-ttu-id="b2294-357">Kaç kez dış veri kullanılabilirliğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b2294-357">The number of times to check for the availability of the external data.</span></span> <span data-ttu-id="b2294-358">Değer izin verilen en fazla 10'dur.</span><span class="sxs-lookup"><span data-stu-id="b2294-358">The maximum allowed value is 10.</span></span> |<span data-ttu-id="b2294-359">Hayır</span><span class="sxs-lookup"><span data-stu-id="b2294-359">No</span></span> |<span data-ttu-id="b2294-360">3</span><span class="sxs-lookup"><span data-stu-id="b2294-360">3</span></span> |


## <a name="create-datasets"></a><span data-ttu-id="b2294-361">Veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2294-361">Create datasets</span></span>
<span data-ttu-id="b2294-362">Bu araçlar ya da SDK'ları birini kullanarak veri kümeleri oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b2294-362">You can create datasets by using one of these tools or SDKs:</span></span> 

- <span data-ttu-id="b2294-363">Kopyalama Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="b2294-363">Copy Wizard</span></span> 
- <span data-ttu-id="b2294-364">Azure portalı</span><span class="sxs-lookup"><span data-stu-id="b2294-364">Azure portal</span></span>
- <span data-ttu-id="b2294-365">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b2294-365">Visual Studio</span></span>
- <span data-ttu-id="b2294-366">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2294-366">PowerShell</span></span>
- <span data-ttu-id="b2294-367">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="b2294-367">Azure Resource Manager template</span></span>
- <span data-ttu-id="b2294-368">REST API</span><span class="sxs-lookup"><span data-stu-id="b2294-368">REST API</span></span>
- <span data-ttu-id="b2294-369">.NET API’si</span><span class="sxs-lookup"><span data-stu-id="b2294-369">.NET API</span></span>

<span data-ttu-id="b2294-370">Bu araçlar ya da SDK'ları birini kullanarak ardışık düzen ve veri kümeleri oluşturmak için aşağıdaki öğreticileri adım adım yönergeler için bkz:</span><span class="sxs-lookup"><span data-stu-id="b2294-370">See the following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs:</span></span>
 
- [<span data-ttu-id="b2294-371">Veri dönüştürme etkinliğine sahip işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2294-371">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="b2294-372">Veri taşıma etkinliği ile işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2294-372">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="b2294-373">Ardışık düzenin oluşturulan ve dağıtılan sonra yönetebilir ve Azure portal dikey penceresi veya izleme ve yönetim uygulaması kullanılarak işlem hatlarınızı izlemek.</span><span class="sxs-lookup"><span data-stu-id="b2294-373">After a pipeline is created and deployed, you can manage and monitor your pipelines by using the Azure portal blades, or the Monitoring and Management app.</span></span> <span data-ttu-id="b2294-374">Adım adım yönergeler için aşağıdaki konulara bakın:</span><span class="sxs-lookup"><span data-stu-id="b2294-374">See the following topics for step-by-step instructions:</span></span> 

- [<span data-ttu-id="b2294-375">İzleme ve Azure portal dikey penceresi kullanılarak işlem hatlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="b2294-375">Monitor and manage pipelines by using Azure portal blades</span></span>](data-factory-monitor-manage-pipelines.md)
- [<span data-ttu-id="b2294-376">İzleme ve işlem hatlarını izleme ve yönetim uygulaması kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="b2294-376">Monitor and manage pipelines by using the Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a><span data-ttu-id="b2294-377">Kapsamlı veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="b2294-377">Scoped datasets</span></span>
<span data-ttu-id="b2294-378">Kullanarak bir işlem hattı için kapsamlı veri kümeleri oluşturabilirsiniz **veri kümeleri** özelliği.</span><span class="sxs-lookup"><span data-stu-id="b2294-378">You can create datasets that are scoped to a pipeline by using the **datasets** property.</span></span> <span data-ttu-id="b2294-379">Bu veri kümeleri yalnızca kullanılabilir etkinlikler içinde bu ardışık düzen tarafından diğer ardışık etkinlikler tarafından değil.</span><span class="sxs-lookup"><span data-stu-id="b2294-379">These datasets can only be used by activities within this pipeline, not by activities in other pipelines.</span></span> <span data-ttu-id="b2294-380">Aşağıdaki örnek, iki veri kümesi (InputDataset rdc ve OutputDataset rdc) içinde ardışık düzeni kullanılacak sahip işlem hattı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b2294-380">The following example defines a pipeline with two datasets (InputDataset-rdc and OutputDataset-rdc) to be used within the pipeline.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="b2294-381">Kapsamlı veri kümeleri, yalnızca tek seferlik ardışık düzen ile desteklenir (burada **pipelineMode** ayarlanır **OneTime**).</span><span class="sxs-lookup"><span data-stu-id="b2294-381">Scoped datasets are supported only with one-time pipelines (where **pipelineMode** is set to **OneTime**).</span></span> <span data-ttu-id="b2294-382">Bkz: [Onetime ardışık düzen](data-factory-create-pipelines.md#onetime-pipeline) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="b2294-382">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details.</span></span>
>
>

```json
{
    "name": "CopyPipeline-rdc",
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
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
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
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="b2294-383">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b2294-383">Next steps</span></span>
- <span data-ttu-id="b2294-384">Ardışık Düzen hakkında daha fazla bilgi için bkz: [oluşturma ardışık düzen](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="b2294-384">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md).</span></span> 
- <span data-ttu-id="b2294-385">Ardışık Düzen nasıl zamanlanmış ve yürütülen hakkında daha fazla bilgi için bkz: [zamanlama ve yürütme Azure Data factory'de](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="b2294-385">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md).</span></span> 
