---
title: "Azure Data Factory'deki veri kümelerini aaaCreate | Microsoft Docs"
description: "Azure Data Factory toocreate kümelerinde gibi özellikleri kullanma örnekleri içeren nasıl uzaklığı ve anchorDateTime öğrenin."
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
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a><span data-ttu-id="2ff3d-104">Azure Data Factory'deki veri kümelerini</span><span class="sxs-lookup"><span data-stu-id="2ff3d-104">Datasets in Azure Data Factory</span></span>
<span data-ttu-id="2ff3d-105">Bu makalede hangi veri kümeleri, JSON biçiminde nasıl tanımlanan açıklanmıştır ve Azure Data Factory içinde kullanılan nasıl ardışık düzenleri.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-105">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span></span> <span data-ttu-id="2ff3d-106">Bu, hello dataset JSON tanımında her bölüm (örneğin, yapısı, kullanılabilirlik ve ilke) hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-106">It provides details about each section (for example, structure, availability, and policy) in hello dataset JSON definition.</span></span> <span data-ttu-id="2ff3d-107">Merhaba makale ayrıca hello kullanmak için örnekler **uzaklık**, **anchorDateTime**, ve **stili** dataset JSON tanımında özellikleri.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-107">hello article also provides examples for using hello **offset**, **anchorDateTime**, and **style** properties in a dataset JSON definition.</span></span>

> [!NOTE]
> <span data-ttu-id="2ff3d-108">Yeni tooData Fabrika olup olmadığını görmek [giriş tooAzure Data Factory](data-factory-introduction.md) bir genel bakış.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-108">If you are new tooData Factory, see [Introduction tooAzure Data Factory](data-factory-introduction.md) for an overview.</span></span> <span data-ttu-id="2ff3d-109">Veri fabrikaları oluşturma ile uygulamalı deneyim yoksa daha iyi anlamak okuma hello tarafından kazanmadan [veri dönüştürme öğretici](data-factory-build-your-first-pipeline.md) ve hello [veri taşıma Öğreticisi](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="2ff3d-109">If you do not have hands-on experience with creating data factories, you can gain a better understanding by reading hello [data transformation tutorial](data-factory-build-your-first-pipeline.md) and hello [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="2ff3d-110">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2ff3d-110">Overview</span></span>
<span data-ttu-id="2ff3d-111">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-111">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="2ff3d-112">A **ardışık düzen** mantıksal bir gruplandırmasıdır **etkinlikleri** görev birlikte gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-112">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="2ff3d-113">bir ardışık düzende Hello etkinlik Eylemler tooperform verilerinizde tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-113">hello activities in a pipeline define actions tooperform on your data.</span></span> <span data-ttu-id="2ff3d-114">Örneğin, bir şirket içi SQL Server tooAzure Blob depolama alanına kopyalama etkinliği toocopy verilerden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-114">For example, you might use a copy activity toocopy data from an on-premises SQL Server tooAzure Blob storage.</span></span> <span data-ttu-id="2ff3d-115">Ardından, Blob Depolama tooproduce çıktı verilerini Azure Hdınsight küme tooprocess verileri üzerinde bir Hive betiği çalıştıran bir Hive etkinliği kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-115">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster tooprocess data from Blob storage tooproduce output data.</span></span> <span data-ttu-id="2ff3d-116">Son olarak, bir ikinci kopya etkinliği toocopy hello çıkış veri tooAzure SQL Data Warehouse, çözümleri yerleşik raporlama hangi iş zekası (BI) üstünde kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-116">Finally, you might use a second copy activity toocopy hello output data tooAzure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="2ff3d-117">Ardışık Düzen ve etkinlikleri hakkında daha fazla bilgi için bkz: [işlem hatlarının ve etkinliklerin Azure Data Factory](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="2ff3d-117">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md).</span></span>

<span data-ttu-id="2ff3d-118">Bir etkinlik sıfır veya daha fazla giriş alabilir **veri kümeleri**ve bir veya daha fazla çıkış veri kümeleri oluşturma.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-118">An activity can take zero or more input **datasets**, and produce one or more output datasets.</span></span> <span data-ttu-id="2ff3d-119">Bir giriş veri kümesi hello ardışık düzeninde bir etkinliğin hello giriş ve bir çıkış veri kümesi hello çıktı hello etkinliği temsil eder.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-119">An input dataset represents hello input for an activity in hello pipeline, and an output dataset represents hello output for hello activity.</span></span> <span data-ttu-id="2ff3d-120">Veri kümeleri tablolar, dosyalar, klasörler ve belgeler gibi farklı veri depoları içindeki verileri tanımlamak.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-120">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="2ff3d-121">Örneğin, bir Azure Blob dataset hello blob kapsayıcısı ve klasör hangi hello ardışık düzen hello veri okumalısınız Blob depolama alanına belirtir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-121">For example, an Azure Blob dataset specifies hello blob container and folder in Blob storage from which hello pipeline should read hello data.</span></span> 

<span data-ttu-id="2ff3d-122">Bir veri kümesi oluşturmadan önce oluşturun bir **bağlantılı hizmeti** toolink verilerinizi depolamak toohello veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-122">Before you create a dataset, create a **linked service** toolink your data store toohello data factory.</span></span> <span data-ttu-id="2ff3d-123">Bağlı hizmetler Data Factory tooconnect tooexternal kaynakları için gerekli hello bağlantı bilgilerini tanımlayın bağlantı dizeleri çok gibidir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-123">Linked services are much like connection strings, which define hello connection information needed for Data Factory tooconnect tooexternal resources.</span></span> <span data-ttu-id="2ff3d-124">Veri kümelerini SQL tablolarının, dosyalar, klasörler ve belgeler gibi hello bağlı veri depoları içindeki verileri tanımlamak.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-124">Datasets identify data within hello linked data stores, such as SQL tables, files, folders, and documents.</span></span> <span data-ttu-id="2ff3d-125">Örneğin, bir Azure depolama hizmeti depolama hesabı toohello data factory bağlantılı.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-125">For example, an Azure Storage linked service links a storage account toohello data factory.</span></span> <span data-ttu-id="2ff3d-126">Bir Azure Blob dataset hello blob kapsayıcısı ve işlenen hello giriş BLOB'ları toobe içeren hello klasörü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-126">An Azure Blob dataset represents hello blob container and hello folder that contains hello input blobs toobe processed.</span></span> 

<span data-ttu-id="2ff3d-127">Bir örnek senaryo aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-127">Here is a sample scenario.</span></span> <span data-ttu-id="2ff3d-128">Blob Depolama tooa SQL veritabanından veri toocopy, iki bağlı hizmet oluşturma: Azure Storage ve Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-128">toocopy data from Blob storage tooa SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="2ff3d-129">Ardından, iki veri kümesi oluşturun: (toohello Azure Storage bağlı hizmeti ifade eder) Azure Blob veri kümesi ve (toohello bağlı Azure SQL veritabanı hizmetinin atıfta bulunmaktadır) Azure SQL tablosu veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-129">Then, create two datasets: Azure Blob dataset (which refers toohello Azure Storage linked service) and Azure SQL Table dataset (which refers toohello Azure SQL Database linked service).</span></span> <span data-ttu-id="2ff3d-130">Azure Storage ve Azure SQL bağlantılı Hizmetleri çalışma zamanı tooconnect tooyour Azure Storage ve Azure SQL Database, veri fabrikası sırasıyla kullandığı bağlantı dizelerini içeren veritabanı hello.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-130">hello Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime tooconnect tooyour Azure Storage and Azure SQL Database, respectively.</span></span> <span data-ttu-id="2ff3d-131">Hello Azure Blob dataset hello blob kapsayıcısı ve Blob Depolama alanınızın hello giriş blobları içeren blob klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-131">hello Azure Blob dataset specifies hello blob container and blob folder that contains hello input blobs in your Blob storage.</span></span> <span data-ttu-id="2ff3d-132">Hello Azure SQL tablosu veri kümesi, SQL veritabanı toowhich hello verilerinizi hello SQL tablosuna kopyalanan toobe belirtir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-132">hello Azure SQL Table dataset specifies hello SQL table in your SQL database toowhich hello data is toobe copied.</span></span>

<span data-ttu-id="2ff3d-133">Merhaba Aşağıdaki diyagramda hello arasındaki ilişkiler ardışık düzen, etkinlik, veri kümesi ve bağlantılı hizmet veri fabrikasında gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="2ff3d-133">hello following diagram shows hello relationships among pipeline, activity, dataset, and linked service in Data Factory:</span></span> 

![Ardışık düzen, etkinlik, veri kümesi, bağlı hizmetler arasındaki ilişki](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a><span data-ttu-id="2ff3d-135">JSON veri kümesi</span><span class="sxs-lookup"><span data-stu-id="2ff3d-135">Dataset JSON</span></span>
<span data-ttu-id="2ff3d-136">Veri fabrikasında bir veri kümesini JSON biçiminde şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="2ff3d-136">A dataset in Data Factory is defined in JSON format as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="2ff3d-137">Aşağıdaki tablonun hello JSON yukarıda hello özelliklerinde açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="2ff3d-137">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="2ff3d-138">Özellik</span><span class="sxs-lookup"><span data-stu-id="2ff3d-138">Property</span></span> | <span data-ttu-id="2ff3d-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2ff3d-139">Description</span></span> | <span data-ttu-id="2ff3d-140">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2ff3d-140">Required</span></span> | <span data-ttu-id="2ff3d-141">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="2ff3d-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2ff3d-142">ad</span><span class="sxs-lookup"><span data-stu-id="2ff3d-142">name</span></span> |<span data-ttu-id="2ff3d-143">Merhaba DataSet'in adı.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-143">Name of hello dataset.</span></span> <span data-ttu-id="2ff3d-144">Bkz: [Azure Data Factory - adlandırma kuralları](data-factory-naming-rules.md) adlandırma kuralları.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-144">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="2ff3d-145">Evet</span><span class="sxs-lookup"><span data-stu-id="2ff3d-145">Yes</span></span> |<span data-ttu-id="2ff3d-146">NA</span><span class="sxs-lookup"><span data-stu-id="2ff3d-146">NA</span></span> |
| <span data-ttu-id="2ff3d-147">type</span><span class="sxs-lookup"><span data-stu-id="2ff3d-147">type</span></span> |<span data-ttu-id="2ff3d-148">Merhaba veri kümesi türü.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-148">Type of hello dataset.</span></span> <span data-ttu-id="2ff3d-149">Data Factory ile desteklenen hello türlerinden birini belirtin (örneğin: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="2ff3d-149">Specify one of hello types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="2ff3d-150">Ayrıntılar için bkz [veri kümesi türü](#Type).</span><span class="sxs-lookup"><span data-stu-id="2ff3d-150">For details, see [Dataset type](#Type).</span></span> |<span data-ttu-id="2ff3d-151">Evet</span><span class="sxs-lookup"><span data-stu-id="2ff3d-151">Yes</span></span> |<span data-ttu-id="2ff3d-152">NA</span><span class="sxs-lookup"><span data-stu-id="2ff3d-152">NA</span></span> |
| <span data-ttu-id="2ff3d-153">yapısı</span><span class="sxs-lookup"><span data-stu-id="2ff3d-153">structure</span></span> |<span data-ttu-id="2ff3d-154">Merhaba dataset şema.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-154">Schema of hello dataset.</span></span><br/><br/><span data-ttu-id="2ff3d-155">Ayrıntılar için bkz [veri kümesi yapısı](#Structure).</span><span class="sxs-lookup"><span data-stu-id="2ff3d-155">For details, see [Dataset structure](#Structure).</span></span> |<span data-ttu-id="2ff3d-156">Hayır</span><span class="sxs-lookup"><span data-stu-id="2ff3d-156">No</span></span> |<span data-ttu-id="2ff3d-157">NA</span><span class="sxs-lookup"><span data-stu-id="2ff3d-157">NA</span></span> |
| <span data-ttu-id="2ff3d-158">typeProperties</span><span class="sxs-lookup"><span data-stu-id="2ff3d-158">typeProperties</span></span> | <span data-ttu-id="2ff3d-159">Merhaba türü özellikleri her türü için farklı (örneğin: Azure Blob, Azure SQL tablosu).</span><span class="sxs-lookup"><span data-stu-id="2ff3d-159">hello type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="2ff3d-160">Desteklenen hello türleri ve özellikleri hakkında daha fazla bilgi için bkz: [veri kümesi türü](#Type).</span><span class="sxs-lookup"><span data-stu-id="2ff3d-160">For details on hello supported types and their properties, see [Dataset type](#Type).</span></span> |<span data-ttu-id="2ff3d-161">Evet</span><span class="sxs-lookup"><span data-stu-id="2ff3d-161">Yes</span></span> |<span data-ttu-id="2ff3d-162">NA</span><span class="sxs-lookup"><span data-stu-id="2ff3d-162">NA</span></span> |
| <span data-ttu-id="2ff3d-163">external</span><span class="sxs-lookup"><span data-stu-id="2ff3d-163">external</span></span> | <span data-ttu-id="2ff3d-164">Boole veya bir veri kümesi açıkça data factory işlem hattı tarafından üretilir olup olmadığını toospecify bayrağı.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-164">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> <span data-ttu-id="2ff3d-165">Merhaba giriş veri kümesi bir etkinlik için hello geçerli ardışık düzen tarafından üretilen değil, bu bayrağı tootrue ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-165">If hello input dataset for an activity is not produced by hello current pipeline, set this flag tootrue.</span></span> <span data-ttu-id="2ff3d-166">Bu bayrak tootrue hello hello ilk etkinliğin girdi veri kümesi için hello ardışık düzeninde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-166">Set this flag tootrue for hello input dataset of hello first activity in hello pipeline.</span></span>  |<span data-ttu-id="2ff3d-167">Hayır</span><span class="sxs-lookup"><span data-stu-id="2ff3d-167">No</span></span> |<span data-ttu-id="2ff3d-168">False</span><span class="sxs-lookup"><span data-stu-id="2ff3d-168">false</span></span> |
| <span data-ttu-id="2ff3d-169">availability</span><span class="sxs-lookup"><span data-stu-id="2ff3d-169">availability</span></span> | <span data-ttu-id="2ff3d-170">(Örneğin, saatlik veya günlük) işlemi penceresini hello veya model hello dataset üretim için dilimleme hello tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-170">Defines hello processing window (for example, hourly or daily) or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="2ff3d-171">Her veri birimi, tüketilen ve etkinlik çalışması tarafından üretilen veri dilimi adı verilir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-171">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="2ff3d-172">Bir çıkış veri kümesi Hello kullanılabilirliğini kümesi toodaily (sıklığı - Day, aralığı - 1) ise, bir dilim günlük oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-172">If hello availability of an output dataset is set toodaily (frequency - Day, interval - 1), a slice is produced daily.</span></span> <br/><br/><span data-ttu-id="2ff3d-173">Ayrıntılar için bkz [Dataset kullanılabilirliği](#Availability).</span><span class="sxs-lookup"><span data-stu-id="2ff3d-173">For details, see [Dataset availability](#Availability).</span></span> <br/><br/><span data-ttu-id="2ff3d-174">Merhaba dataset hakkında ayrıntılı bilgi için modeli dilimleme bkz hello [zamanlama ve yürütme](data-factory-scheduling-and-execution.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-174">For details on hello dataset slicing model, see hello [Scheduling and execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="2ff3d-175">Evet</span><span class="sxs-lookup"><span data-stu-id="2ff3d-175">Yes</span></span> |<span data-ttu-id="2ff3d-176">NA</span><span class="sxs-lookup"><span data-stu-id="2ff3d-176">NA</span></span> |
| <span data-ttu-id="2ff3d-177">İlke</span><span class="sxs-lookup"><span data-stu-id="2ff3d-177">policy</span></span> |<span data-ttu-id="2ff3d-178">Merhaba ölçütleri veya hello dataset dilimler karşılamanız gerekmektedir hello koşulu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-178">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="2ff3d-179">Merhaba Ayrıntılar için bkz [Dataset İlkesi](#Policy) bölümü.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-179">For details, see hello [Dataset policy](#Policy) section.</span></span> |<span data-ttu-id="2ff3d-180">Hayır</span><span class="sxs-lookup"><span data-stu-id="2ff3d-180">No</span></span> |<span data-ttu-id="2ff3d-181">NA</span><span class="sxs-lookup"><span data-stu-id="2ff3d-181">NA</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="2ff3d-182">Veri kümesi örneği</span><span class="sxs-lookup"><span data-stu-id="2ff3d-182">Dataset example</span></span>
<span data-ttu-id="2ff3d-183">Aşağıdaki örneğine hello hello dataset adlı bir tablo temsil **MyTable** bir SQL veritabanında.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-183">In hello following example, hello dataset represents a table named **MyTable** in a SQL database.</span></span>

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

<span data-ttu-id="2ff3d-184">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="2ff3d-184">Note hello following points:</span></span>

* <span data-ttu-id="2ff3d-185">**tür** tooAzureSqlTable ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-185">**type** is set tooAzureSqlTable.</span></span>
* <span data-ttu-id="2ff3d-186">**tableName** type özelliği (belirli tooAzureSqlTable türü), tooMyTable ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-186">**tableName** type property (specific tooAzureSqlTable type) is set tooMyTable.</span></span>
* <span data-ttu-id="2ff3d-187">**linkedServiceName** tooa bağlantılı hizmet türü hello sonraki JSON parçacığında tanımlanan AzureSqlDatabase başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-187">**linkedServiceName** refers tooa linked service of type AzureSqlDatabase, which is defined in hello next JSON snippet.</span></span> 
* <span data-ttu-id="2ff3d-188">**Kullanılabilirlik sıklığı** tooDay, ayarlayın ve **aralığı** too1 ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-188">**availability frequency** is set tooDay, and **interval** is set too1.</span></span> <span data-ttu-id="2ff3d-189">Bu, o hello dataset dilim günlük üretilen anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-189">This means that hello dataset slice is produced daily.</span></span>  

<span data-ttu-id="2ff3d-190">**AzureSqlLinkedService** şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="2ff3d-190">**AzureSqlLinkedService** is defined as follows:</span></span>

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

<span data-ttu-id="2ff3d-191">JSON parçacığı önceki hello:</span><span class="sxs-lookup"><span data-stu-id="2ff3d-191">In hello preceding JSON snippet:</span></span>

* <span data-ttu-id="2ff3d-192">**tür** tooAzureSqlDatabase ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-192">**type** is set tooAzureSqlDatabase.</span></span>
* <span data-ttu-id="2ff3d-193">**connectionString** type özelliği bilgi tooconnect tooa SQL veritabanını belirtir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-193">**connectionString** type property specifies information tooconnect tooa SQL database.</span></span>  

<span data-ttu-id="2ff3d-194">Gördüğünüz gibi hello bağlantılı hizmet tanımlar nasıl tooconnect tooa SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-194">As you can see, hello linked service defines how tooconnect tooa SQL database.</span></span> <span data-ttu-id="2ff3d-195">Merhaba dataset hangi tablo girdi olarak kullanılır ve ardışık düzeninde hello etkinliğinin çıkış tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-195">hello dataset defines what table is used as an input and output for hello activity in a pipeline.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="2ff3d-196">Bir veri kümesi hello ardışık düzen tarafından üretilen sürece bunu olarak işaretlenmelidir **dış**.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-196">Unless a dataset is being produced by hello pipeline, it should be marked as **external**.</span></span> <span data-ttu-id="2ff3d-197">Bu ayar genellikle bir ardışık düzendeki ilk etkinliğin tooinputs uygulanır.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-197">This setting generally applies tooinputs of first activity in a pipeline.</span></span>   


## <span data-ttu-id="2ff3d-198"><a name="Type"></a>Veri kümesi türü</span><span class="sxs-lookup"><span data-stu-id="2ff3d-198"><a name="Type"></a> Dataset type</span></span>
<span data-ttu-id="2ff3d-199">kullandığınız hello veri deposunda hello dataset Hello türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-199">hello type of hello dataset depends on hello data store you use.</span></span> <span data-ttu-id="2ff3d-200">Merhaba aşağıdaki tablonun Data Factory ile desteklenen veri depoları listesi için bkz.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-200">See hello following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="2ff3d-201">Bir veri deposu toolearn tıklatın nasıl toocreate bağlı hizmet ve bu veriler için bir veri kümesi depolar.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-201">Click a data store toolearn how toocreate a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="2ff3d-202">Veri depolar ile * şirket içi olabilir veya hizmet (Iaas) olarak Azure altyapısı.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-202">Data stores with * can be on-premises or on Azure infrastructure as a service (IaaS).</span></span> <span data-ttu-id="2ff3d-203">Bu veri depolarına tooinstall gerektiren [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="2ff3d-203">These data stores require you tooinstall [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="2ff3d-204">Merhaba önceki bölümdeki Hello örnekte hello dataset hello türü çok ayarlanır**AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-204">In hello example in hello previous section, hello type of hello dataset is set too**AzureSqlTable**.</span></span> <span data-ttu-id="2ff3d-205">Benzer şekilde, Azure Blob veri kümesi için hello türü hello veri kümesi çok ayarlıdır**AzureBlob**hello JSON aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="2ff3d-205">Similarly, for an Azure Blob dataset, hello type of hello dataset is set too**AzureBlob**, as shown in hello following JSON:</span></span>

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

## <span data-ttu-id="2ff3d-206"><a name="Structure"></a>Veri kümesi yapısı</span><span class="sxs-lookup"><span data-stu-id="2ff3d-206"><a name="Structure"></a>Dataset structure</span></span>
<span data-ttu-id="2ff3d-207">Merhaba **yapısı** bölümdür isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-207">hello **structure** section is optional.</span></span> <span data-ttu-id="2ff3d-208">Merhaba kümesinin hello şema, tarafından içeren bir koleksiyon adları ve sütunların veri türlerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-208">It defines hello schema of hello dataset by containing a collection of names and data types of columns.</span></span> <span data-ttu-id="2ff3d-209">Kullanılan tooconvert türleri ve hello kaynak toohello hedef harita sütunlarından hello yapısı bölüm tooprovide türü bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-209">You use hello structure section tooprovide type information that is used tooconvert types and map columns from hello source toohello destination.</span></span> <span data-ttu-id="2ff3d-210">Aşağıdaki örneğine hello hello dataset üç sütun vardır: `slicetimestamp`, `projectname`, ve `pageviews`.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-210">In hello following example, hello dataset has three columns: `slicetimestamp`, `projectname`, and `pageviews`.</span></span> <span data-ttu-id="2ff3d-211">Bunlar dize, dize ve ondalık, sırasıyla türüdür.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-211">They are of type String, String, and Decimal, respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="2ff3d-212">Her sütun hello yapısında aşağıdaki özelliklere hello içerir:</span><span class="sxs-lookup"><span data-stu-id="2ff3d-212">Each column in hello structure contains hello following properties:</span></span>

| <span data-ttu-id="2ff3d-213">Özellik</span><span class="sxs-lookup"><span data-stu-id="2ff3d-213">Property</span></span> | <span data-ttu-id="2ff3d-214">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2ff3d-214">Description</span></span> | <span data-ttu-id="2ff3d-215">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2ff3d-215">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ff3d-216">ad</span><span class="sxs-lookup"><span data-stu-id="2ff3d-216">name</span></span> |<span data-ttu-id="2ff3d-217">Merhaba sütunun adı.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-217">Name of hello column.</span></span> |<span data-ttu-id="2ff3d-218">Evet</span><span class="sxs-lookup"><span data-stu-id="2ff3d-218">Yes</span></span> |
| <span data-ttu-id="2ff3d-219">type</span><span class="sxs-lookup"><span data-stu-id="2ff3d-219">type</span></span> |<span data-ttu-id="2ff3d-220">Merhaba sütununun veri türü.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-220">Data type of hello column.</span></span>  |<span data-ttu-id="2ff3d-221">Hayır</span><span class="sxs-lookup"><span data-stu-id="2ff3d-221">No</span></span> |
| <span data-ttu-id="2ff3d-222">Kültür</span><span class="sxs-lookup"><span data-stu-id="2ff3d-222">culture</span></span> |<span data-ttu-id="2ff3d-223">. Merhaba türü .NET türü olduğunda kullanılan NET tabanlı kültürü toobe: `Datetime` veya `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-223">.NET-based culture toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="2ff3d-224">Merhaba varsayılan `en-us`.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-224">hello default is `en-us`.</span></span> |<span data-ttu-id="2ff3d-225">Hayır</span><span class="sxs-lookup"><span data-stu-id="2ff3d-225">No</span></span> |
| <span data-ttu-id="2ff3d-226">Biçimi</span><span class="sxs-lookup"><span data-stu-id="2ff3d-226">format</span></span> |<span data-ttu-id="2ff3d-227">Biçimlendirme dizesi toobe hello türü .NET türü olduğunda kullanılan: `Datetime` veya `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-227">Format string toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="2ff3d-228">Hayır</span><span class="sxs-lookup"><span data-stu-id="2ff3d-228">No</span></span> |

<span data-ttu-id="2ff3d-229">Merhaba aşağıdaki yönergeleri tooinclude yapısı bilgileri ne zaman ve hangi tooinclude hello içinde belirlemenize yardımcı **yapısı** bölümü.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-229">hello following guidelines help you determine when tooinclude structure information, and what tooinclude in hello **structure** section.</span></span>

* <span data-ttu-id="2ff3d-230">**Yapılandırılmış veri kaynakları için**, yalnızca kaynak sütunları toosink sütunları eşlemek istediğiniz ve adları olan değil hello aynı hello yapısı bölümünde belirtin.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-230">**For structured data sources**, specify hello structure section only if you want map source columns toosink columns, and their names are not hello same.</span></span> <span data-ttu-id="2ff3d-231">Bu tür bir yapılandırılmış veri kaynağı hello verilerin kendisini veri şeması ve tür bilgileri depolar.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-231">This kind of structured data source stores data schema and type information along with hello data itself.</span></span> <span data-ttu-id="2ff3d-232">SQL Server, Oracle ve Azure tablo yapılandırılmış veri kaynakları örneklerindendir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-232">Examples of structured data sources include SQL Server, Oracle, and Azure table.</span></span> 
  
    <span data-ttu-id="2ff3d-233">Tür bilgileri zaten yapılandırılmış veri kaynakları için kullanılabilir olduğu gibi hello yapısı bölüm eklediğinizde türü bilgileri içermemelidir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-233">As type information is already available for structured data sources, you should not include type information when you do include hello structure section.</span></span>
* <span data-ttu-id="2ff3d-234">**Şema okuma veri kaynaklarında (özellikle Blob Depolama) için**, herhangi bir şema veya türü bilgi hello verilerle depolamadan toostore veri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-234">**For schema on read data sources (specifically Blob storage)**, you can choose toostore data without storing any schema or type information with hello data.</span></span> <span data-ttu-id="2ff3d-235">Toomap kaynak sütunları toosink sütunları istediğinizde bu tür veri kaynağı yapısı içerir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-235">For these types of data sources, include structure when you want toomap source columns toosink columns.</span></span> <span data-ttu-id="2ff3d-236">Ayrıca yapısı hello veri kümesi kopyalama etkinliği için bir giriş, kaynak veri kümesinin veri türleri dönüştürülmüş toonative türleri hello havuz için kullanılabilir olmalı ve zaman içerir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-236">Also include structure when hello dataset is an input for a copy activity, and data types of source dataset should be converted toonative types for hello sink.</span></span> 
    
    <span data-ttu-id="2ff3d-237">Veri Fabrikası yapısındaki türü bilgileri sağlamak için değerleri aşağıdaki hello destekler: **Int16, Int32, Int64, tek, Double, Decimal, bayt [], Boolean, dize, GUID, Datetime, Datetimeoffset ve Timespan**.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-237">Data Factory supports hello following values for providing type information in structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**.</span></span> <span data-ttu-id="2ff3d-238">Ortak dil belirtimi (CLS) bu değerler-uyumlu. NET tabanlı türü değerleri.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-238">These values are Common Language Specification (CLS)-compliant, .NET-based type values.</span></span>

<span data-ttu-id="2ff3d-239">Veri Fabrikası otomatik olarak veri kaynağına veri dosyaları tooa havuz veri deposunu taşırken tür dönüşümleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-239">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span> 
  

## <a name="dataset-availability"></a><span data-ttu-id="2ff3d-240">DataSet kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="2ff3d-240">Dataset availability</span></span>
<span data-ttu-id="2ff3d-241">Merhaba **kullanılabilirlik** hello işleme penceresi (örneğin, saatlik, günlük veya haftalık) hello veri kümesi için bir veri kümesi bölümünde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-241">hello **availability** section in a dataset defines hello processing window (for example, hourly, daily, or weekly) for hello dataset.</span></span> <span data-ttu-id="2ff3d-242">Etkinlik pencereleri hakkında daha fazla bilgi için bkz: [zamanlama ve yürütme](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="2ff3d-242">For more information about activity windows, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>

<span data-ttu-id="2ff3d-243">Kullanılabilirlik bölümden hello hello çıktı veri kümesi ya da saatlik üretilen veya hello girdi veri kümesi saatlik kullanılabilir belirtir:</span><span class="sxs-lookup"><span data-stu-id="2ff3d-243">hello following availability section specifies that hello output dataset is either produced hourly, or hello input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="2ff3d-244">Merhaba ardışık düzen başlangıç ve bitiş zamanlarını aşağıdaki hello varsa:</span><span class="sxs-lookup"><span data-stu-id="2ff3d-244">If hello pipeline has hello following start and end times:</span></span>  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

<span data-ttu-id="2ff3d-245">Merhaba çıktı veri kümesi üretilen saatlik içinde hello ardışık düzeni başlangıç ve bitiş zamanları.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-245">hello output dataset is produced hourly within hello pipeline start and end times.</span></span> <span data-ttu-id="2ff3d-246">Bu nedenle, bu ardışık düzen, her etkinlik penceresinin (00: 00-1 AM, 1 AM - 2 AM, 2: 00 - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM) için bir tane tarafından üretilen beş veri kümesi dilimler vardır.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-246">Therefore, there are five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2 AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 

<span data-ttu-id="2ff3d-247">Merhaba aşağıdaki tabloda hello Kullanılabilirliği bölümünde kullanabileceğiniz özellikleri açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="2ff3d-247">hello following table describes properties you can use in hello availability section:</span></span>

| <span data-ttu-id="2ff3d-248">Özellik</span><span class="sxs-lookup"><span data-stu-id="2ff3d-248">Property</span></span> | <span data-ttu-id="2ff3d-249">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2ff3d-249">Description</span></span> | <span data-ttu-id="2ff3d-250">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2ff3d-250">Required</span></span> | <span data-ttu-id="2ff3d-251">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="2ff3d-251">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2ff3d-252">frequency</span><span class="sxs-lookup"><span data-stu-id="2ff3d-252">frequency</span></span> |<span data-ttu-id="2ff3d-253">Veri kümesi dilim üretim Hello zaman birimini belirtir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-253">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="2ff3d-254"><b>Sıklık desteklenen</b>: dakika, saat, gün, hafta, ay</span><span class="sxs-lookup"><span data-stu-id="2ff3d-254"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="2ff3d-255">Evet</span><span class="sxs-lookup"><span data-stu-id="2ff3d-255">Yes</span></span> |<span data-ttu-id="2ff3d-256">NA</span><span class="sxs-lookup"><span data-stu-id="2ff3d-256">NA</span></span> |
| <span data-ttu-id="2ff3d-257">interval</span><span class="sxs-lookup"><span data-stu-id="2ff3d-257">interval</span></span> |<span data-ttu-id="2ff3d-258">Sıklığı çarpanı belirtir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-258">Specifies a multiplier for frequency.</span></span><br/><br/><span data-ttu-id="2ff3d-259">"X sıklığı aralığını" ne sıklıkta hello dilim üretilen belirler.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-259">"Frequency x interval" determines how often hello slice is produced.</span></span> <span data-ttu-id="2ff3d-260">Örneğin, dilimlenebilir saatlik olarak başka bir veri kümesi toobe hello varsa, ayarladığınız <b>sıklığı</b> çok<b>saat</b>, ve <b>aralığı</b> çok<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-260">For example, if you need hello dataset toobe sliced on an hourly basis, you set <b>frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="2ff3d-261">Belirtirseniz unutmayın **sıklığı** olarak **Minute**, 15'den küçük hello aralığı toono ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-261">Note that if you specify **frequency** as **Minute**, you should set hello interval toono less than 15.</span></span> |<span data-ttu-id="2ff3d-262">Evet</span><span class="sxs-lookup"><span data-stu-id="2ff3d-262">Yes</span></span> |<span data-ttu-id="2ff3d-263">NA</span><span class="sxs-lookup"><span data-stu-id="2ff3d-263">NA</span></span> |
| <span data-ttu-id="2ff3d-264">stili</span><span class="sxs-lookup"><span data-stu-id="2ff3d-264">style</span></span> |<span data-ttu-id="2ff3d-265">Merhaba dilim hello başlangıç veya bitiş hello aralığının olarak üretilen belirtir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-265">Specifies whether hello slice should be produced at hello start or end of hello interval.</span></span><ul><li><span data-ttu-id="2ff3d-266">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="2ff3d-266">StartOfInterval</span></span></li><li><span data-ttu-id="2ff3d-267">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="2ff3d-267">EndOfInterval</span></span></li></ul><span data-ttu-id="2ff3d-268">Varsa **sıklığı** çok ayarlanır**ay**, ve **stili** çok ayarlanır**EndOfInterval**, hello dilim ayın son günü hello üzerinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-268">If **frequency** is set too**Month**, and **style** is set too**EndOfInterval**, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="2ff3d-269">Varsa **stili** çok ayarlanır**StartOfInterval**, hello dilim ayın ilk günü hello üzerinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-269">If **style** is set too**StartOfInterval**, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="2ff3d-270">Varsa **sıklığı** çok ayarlanır**gün**, ve **stili** çok ayarlanır**EndOfInterval**, hello dilim hello hello günün son bir saat oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-270">If **frequency** is set too**Day**, and **style** is set too**EndOfInterval**, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="2ff3d-271">Varsa **sıklığı** çok ayarlanır**saat**, ve **stili** çok ayarlanır**EndOfInterval**, hello dilim hello hello saat sonunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-271">If **frequency** is set too**Hour**, and **style** is set too**EndOfInterval**, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="2ff3d-272">Örneğin, hello 1 PM - 2 PM dönem için bir dilim için 2 saat hello dilim oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-272">For example, for a slice for hello 1 PM - 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="2ff3d-273">Hayır</span><span class="sxs-lookup"><span data-stu-id="2ff3d-273">No</span></span> |<span data-ttu-id="2ff3d-274">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="2ff3d-274">EndOfInterval</span></span> |
| <span data-ttu-id="2ff3d-275">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="2ff3d-275">anchorDateTime</span></span> |<span data-ttu-id="2ff3d-276">Merhaba Zamanlayıcı toocompute dataset dilim sınırları tarafından kullanılan süre içinde mutlak konum Hello tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-276">Defines hello absolute position in time used by hello scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="2ff3d-277">Bu propoerty hello sıklığı belirtilenden daha ayrıntılı tarih kısımlarını varsa daha ayrıntılı bölümleri hello unutmayın göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-277">Note that if this propoerty has date parts that are more granular than hello specified frequency, hello more granular parts are ignored.</span></span> <span data-ttu-id="2ff3d-278">Örneğin, hello **aralığı** olan **saatlik** (sıklığı: saat ve aralığı: 1) ve hello **anchorDateTime** içeren **dakika ve saniyeleri**, dakika ve saniyeleri bölümlerini hello **anchorDateTime** göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-278">For example, if hello **interval** is **hourly** (frequency: hour and interval: 1), and hello **anchorDateTime** contains **minutes and seconds**, then hello minutes and seconds parts of **anchorDateTime** are ignored.</span></span> |<span data-ttu-id="2ff3d-279">Hayır</span><span class="sxs-lookup"><span data-stu-id="2ff3d-279">No</span></span> |<span data-ttu-id="2ff3d-280">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="2ff3d-280">01/01/0001</span></span> |
| <span data-ttu-id="2ff3d-281">uzaklık</span><span class="sxs-lookup"><span data-stu-id="2ff3d-281">offset</span></span> |<span data-ttu-id="2ff3d-282">Tarafından hangi hello başlangıç ve bitiş tüm veri kümesi dilim gölgeye Timespan.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-282">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="2ff3d-283">Her iki unutmayın **anchorDateTime** ve **uzaklık** belirtilirse, hello sonucudur birleştirilmiş hello shift.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-283">Note that if both **anchorDateTime** and **offset** are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="2ff3d-284">Hayır</span><span class="sxs-lookup"><span data-stu-id="2ff3d-284">No</span></span> |<span data-ttu-id="2ff3d-285">NA</span><span class="sxs-lookup"><span data-stu-id="2ff3d-285">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="2ff3d-286">uzaklık örneği</span><span class="sxs-lookup"><span data-stu-id="2ff3d-286">offset example</span></span>
<span data-ttu-id="2ff3d-287">Varsayılan olarak, her gün (`"frequency": "Day", "interval": 1`) dilimler 00: 00 (gece yarısı) Eşgüdümlü Evrensel Saat (UTC) başlatın.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-287">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM (midnight) Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="2ff3d-288">Merhaba başlangıç saati toobe 6'da UTC saati bunun yerine isterseniz, hello aşağıdaki kod parçacığında gösterildiği gibi uzaklığı hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="2ff3d-288">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="2ff3d-289">anchorDateTime örneği</span><span class="sxs-lookup"><span data-stu-id="2ff3d-289">anchorDateTime example</span></span>
<span data-ttu-id="2ff3d-290">Aşağıdaki örneğine hello hello dataset 23 saatte bir kez oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-290">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="2ff3d-291">Merhaba ilk dilim tarafından belirtilen başlangıç saati başlar **anchorDateTime**, ayarlanmış çok`2017-04-19T08:00:00` (UTC).</span><span class="sxs-lookup"><span data-stu-id="2ff3d-291">hello first slice starts at hello time specified by **anchorDateTime**, which is set too`2017-04-19T08:00:00` (UTC).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="2ff3d-292">uzaklık/stil örneği</span><span class="sxs-lookup"><span data-stu-id="2ff3d-292">offset/style example</span></span>
<span data-ttu-id="2ff3d-293">Merhaba aşağıdaki veri kümesi olan aylık ve 8: 00'da her ayın 3 hello üzerinde üretilen (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="2ff3d-293">hello following dataset is monthly, and is produced on hello 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <span data-ttu-id="2ff3d-294"><a name="Policy"></a>Veri kümesi İlkesi</span><span class="sxs-lookup"><span data-stu-id="2ff3d-294"><a name="Policy"></a>Dataset policy</span></span>
<span data-ttu-id="2ff3d-295">Merhaba **İlkesi** gerekir dataset dilimler hello hello koşulu karşılayan veya hello veri kümesi tanımı bölümünde hello ölçütleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-295">hello **policy** section in hello dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

### <a name="validation-policies"></a><span data-ttu-id="2ff3d-296">Doğrulama ilkeleri</span><span class="sxs-lookup"><span data-stu-id="2ff3d-296">Validation policies</span></span>
| <span data-ttu-id="2ff3d-297">İlke adı</span><span class="sxs-lookup"><span data-stu-id="2ff3d-297">Policy name</span></span> | <span data-ttu-id="2ff3d-298">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2ff3d-298">Description</span></span> | <span data-ttu-id="2ff3d-299">Çok uygulanan</span><span class="sxs-lookup"><span data-stu-id="2ff3d-299">Applied too</span></span>| <span data-ttu-id="2ff3d-300">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2ff3d-300">Required</span></span> | <span data-ttu-id="2ff3d-301">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="2ff3d-301">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="2ff3d-302">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="2ff3d-302">minimumSizeMB</span></span> |<span data-ttu-id="2ff3d-303">Merhaba verilerin doğrular **Azure Blob Depolama** karşılıyor hello minimum boyut gereksinimlerini (megabayt cinsinden).</span><span class="sxs-lookup"><span data-stu-id="2ff3d-303">Validates that hello data in **Azure Blob storage** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="2ff3d-304">Azure Blob depolama</span><span class="sxs-lookup"><span data-stu-id="2ff3d-304">Azure Blob storage</span></span> |<span data-ttu-id="2ff3d-305">Hayır</span><span class="sxs-lookup"><span data-stu-id="2ff3d-305">No</span></span> |<span data-ttu-id="2ff3d-306">NA</span><span class="sxs-lookup"><span data-stu-id="2ff3d-306">NA</span></span> |
| <span data-ttu-id="2ff3d-307">minimumRows</span><span class="sxs-lookup"><span data-stu-id="2ff3d-307">minimumRows</span></span> |<span data-ttu-id="2ff3d-308">Merhaba verilerin doğrulayan bir **Azure SQL veritabanı** veya bir **Azure tablo** hello en az satır sayısını içerir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-308">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="2ff3d-309">Azure SQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="2ff3d-309">Azure SQL database</span></span></li><li><span data-ttu-id="2ff3d-310">Azure tablo</span><span class="sxs-lookup"><span data-stu-id="2ff3d-310">Azure table</span></span></li></ul> |<span data-ttu-id="2ff3d-311">Hayır</span><span class="sxs-lookup"><span data-stu-id="2ff3d-311">No</span></span> |<span data-ttu-id="2ff3d-312">NA</span><span class="sxs-lookup"><span data-stu-id="2ff3d-312">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="2ff3d-313">Örnekler</span><span class="sxs-lookup"><span data-stu-id="2ff3d-313">Examples</span></span>
<span data-ttu-id="2ff3d-314">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="2ff3d-314">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="2ff3d-315">**minimumRows:**</span><span class="sxs-lookup"><span data-stu-id="2ff3d-315">**minimumRows:**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a><span data-ttu-id="2ff3d-316">Dış veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="2ff3d-316">External datasets</span></span>
<span data-ttu-id="2ff3d-317">Dış veri kümeleri hello hello veri fabrikası'nda çalışan bir ardışık düzen tarafından üretilmeyen olanları ' dir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-317">External datasets are hello ones that are not produced by a running pipeline in hello data factory.</span></span> <span data-ttu-id="2ff3d-318">Merhaba veri kümesi olarak işaretlenmişse **dış**, hello **ExternalData** ilkesi tanımlı tooinfluence hello hello dataset dilim kullanılabilirlik davranışını olabilir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-318">If hello dataset is marked as **external**, hello **ExternalData** policy may be defined tooinfluence hello behavior of hello dataset slice availability.</span></span>

<span data-ttu-id="2ff3d-319">Bir veri kümesi Data Factory tarafından üretilen sürece bunu olarak işaretlenmelidir **dış**.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-319">Unless a dataset is being produced by Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="2ff3d-320">Etkinlik veya ardışık düzen zincirleme kullanılmadığı sürece bu ayar genellikle ardışık düzendeki, ilk etkinliğin toohello girişleri uygulanır.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-320">This setting generally applies toohello inputs of first activity in a pipeline, unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="2ff3d-321">Ad</span><span class="sxs-lookup"><span data-stu-id="2ff3d-321">Name</span></span> | <span data-ttu-id="2ff3d-322">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2ff3d-322">Description</span></span> | <span data-ttu-id="2ff3d-323">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2ff3d-323">Required</span></span> | <span data-ttu-id="2ff3d-324">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="2ff3d-324">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2ff3d-325">dataDelay</span><span class="sxs-lookup"><span data-stu-id="2ff3d-325">dataDelay</span></span> |<span data-ttu-id="2ff3d-326">toodelay hello denetleyin hello için dış veri hello hello kullanılabilirliğine hello saat dilimi verilir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-326">hello time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="2ff3d-327">Örneğin, bu ayarı kullanarak bir saatlik onay geciktirebilir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-327">For example, you can delay an hourly check by using this setting.</span></span><br/><br/><span data-ttu-id="2ff3d-328">Merhaba ayar, yalnızca geçerli zaman toohello uygulanır.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-328">hello setting only applies toohello present time.</span></span>  <span data-ttu-id="2ff3d-329">Örneğin, 1:00 PM şimdi ise ve bu değer 10 dakikadır hello doğrulama 13: 10'te başlatır.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-329">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="2ff3d-330">Bu ayar hello geçmiş dilimleri etkilemez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-330">Note that this setting does not affect slices in hello past.</span></span> <span data-ttu-id="2ff3d-331">İle dilimler **dilim bitiş saati** + **dataDelay** < **şimdi** herhangi bir gecikme işlenir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-331">Slices with **Slice End Time** + **dataDelay** < **Now** are processed without any delay.</span></span><br/><br/><span data-ttu-id="2ff3d-332">23:59 büyük saatleri saat hello kullanarak belirtilmelidir `day.hours:minutes:seconds` biçimi.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-332">Times greater than 23:59 hours should be specified by using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="2ff3d-333">Örneğin, toospecify 24 saat 24:00:00 kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-333">For example, toospecify 24 hours, don't use 24:00:00.</span></span> <span data-ttu-id="2ff3d-334">Bunun yerine, 1.00:00:00 kullanın.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-334">Instead, use 1.00:00:00.</span></span> <span data-ttu-id="2ff3d-335">24:00:00 kullanırsanız, 24 gün (24.00:00:00) kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-335">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="2ff3d-336">1 gün ve 4 saat için 1:04:00:00 belirtin.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-336">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="2ff3d-337">Hayır</span><span class="sxs-lookup"><span data-stu-id="2ff3d-337">No</span></span> |<span data-ttu-id="2ff3d-338">0</span><span class="sxs-lookup"><span data-stu-id="2ff3d-338">0</span></span> |
| <span data-ttu-id="2ff3d-339">Retryınterval</span><span class="sxs-lookup"><span data-stu-id="2ff3d-339">retryInterval</span></span> |<span data-ttu-id="2ff3d-340">Merhaba hatası ve hello bir sonraki denemesi arasındaki süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-340">hello wait time between a failure and hello next attempt.</span></span> <span data-ttu-id="2ff3d-341">Bu ayar toopresent zaman geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-341">This setting applies toopresent time.</span></span> <span data-ttu-id="2ff3d-342">Merhaba önceki deneme başarısız olursa hello sonraki deneyin sonra hello olan **Retryınterval** süresi.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-342">If hello previous try failed, hello next try is after hello **retryInterval** period.</span></span> <br/><br/><span data-ttu-id="2ff3d-343">1:00 PM şimdi ise, biz hello ilk denemede başlayın.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-343">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="2ff3d-344">Merhaba süresi toocomplete hello ilk doğrulama denetimi hello işlemi başarısız oldu ve 1 dakikalık hello sonraki yeniden deneme ise, 1:00 1 dak (süresi) + 1 dak (yeniden deneme aralığı) = 1:02 PM.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-344">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="2ff3d-345">Merhaba son dilim için gecikme yoktur.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-345">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="2ff3d-346">Merhaba yeniden deneme hemen gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-346">hello retry happens immediately.</span></span> |<span data-ttu-id="2ff3d-347">Hayır</span><span class="sxs-lookup"><span data-stu-id="2ff3d-347">No</span></span> |<span data-ttu-id="2ff3d-348">00:01:00 (1 dakika)</span><span class="sxs-lookup"><span data-stu-id="2ff3d-348">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="2ff3d-349">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="2ff3d-349">retryTimeout</span></span> |<span data-ttu-id="2ff3d-350">yeniden deneme girişimleri için Hello zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-350">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="2ff3d-351">Bu özellik ayarlanırsa too10 dakika hello doğrulama 10 dakika içinde tamamlanması.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-351">If this property is set too10 minutes, hello validation should be completed within 10 minutes.</span></span> <span data-ttu-id="2ff3d-352">10 dakika tooperform hello doğrulama uzun sürerse hello zaman aşımına yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-352">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="2ff3d-353">Tüm denemeleri hello doğrulama zaman aşımı için Merhaba, dilim olarak işaretlenmiş **süresi sona erdi**.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-353">If all attempts for hello validation time out, hello slice is marked as **TimedOut**.</span></span> |<span data-ttu-id="2ff3d-354">Hayır</span><span class="sxs-lookup"><span data-stu-id="2ff3d-354">No</span></span> |<span data-ttu-id="2ff3d-355">00:10:00 (10 dakika)</span><span class="sxs-lookup"><span data-stu-id="2ff3d-355">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="2ff3d-356">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="2ff3d-356">maximumRetry</span></span> |<span data-ttu-id="2ff3d-357">Merhaba sayısı toocheck hello dış veri hello kullanılabilirlik için zaman.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-357">hello number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="2ff3d-358">değer izin verilen hello en fazla 10'dur.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-358">hello maximum allowed value is 10.</span></span> |<span data-ttu-id="2ff3d-359">Hayır</span><span class="sxs-lookup"><span data-stu-id="2ff3d-359">No</span></span> |<span data-ttu-id="2ff3d-360">3</span><span class="sxs-lookup"><span data-stu-id="2ff3d-360">3</span></span> |


## <a name="create-datasets"></a><span data-ttu-id="2ff3d-361">Veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ff3d-361">Create datasets</span></span>
<span data-ttu-id="2ff3d-362">Bu araçlar ya da SDK'ları birini kullanarak veri kümeleri oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2ff3d-362">You can create datasets by using one of these tools or SDKs:</span></span> 

- <span data-ttu-id="2ff3d-363">Kopyalama Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="2ff3d-363">Copy Wizard</span></span> 
- <span data-ttu-id="2ff3d-364">Azure portalı</span><span class="sxs-lookup"><span data-stu-id="2ff3d-364">Azure portal</span></span>
- <span data-ttu-id="2ff3d-365">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2ff3d-365">Visual Studio</span></span>
- <span data-ttu-id="2ff3d-366">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ff3d-366">PowerShell</span></span>
- <span data-ttu-id="2ff3d-367">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="2ff3d-367">Azure Resource Manager template</span></span>
- <span data-ttu-id="2ff3d-368">REST API</span><span class="sxs-lookup"><span data-stu-id="2ff3d-368">REST API</span></span>
- <span data-ttu-id="2ff3d-369">.NET API’si</span><span class="sxs-lookup"><span data-stu-id="2ff3d-369">.NET API</span></span>

<span data-ttu-id="2ff3d-370">Bu araçlar ya da SDK'ları birini kullanarak ardışık düzen ve veri kümeleri oluşturmak için öğreticileri adım adım yönergeler için aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="2ff3d-370">See hello following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs:</span></span>
 
- [<span data-ttu-id="2ff3d-371">Veri dönüştürme etkinliğine sahip işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ff3d-371">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="2ff3d-372">Veri taşıma etkinliği ile işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ff3d-372">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="2ff3d-373">Ardışık düzenin oluşturulan ve dağıtılan sonra izlemek yönetmek ve Azure portal dikey penceresi veya hello izleme ve yönetim uygulaması kullanılarak işlem hatlarınızı hello.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-373">After a pipeline is created and deployed, you can manage and monitor your pipelines by using hello Azure portal blades, or hello Monitoring and Management app.</span></span> <span data-ttu-id="2ff3d-374">Merhaba aşağıdaki konularda adım adım yönergeler için bkz:</span><span class="sxs-lookup"><span data-stu-id="2ff3d-374">See hello following topics for step-by-step instructions:</span></span> 

- [<span data-ttu-id="2ff3d-375">İzleme ve Azure portal dikey penceresi kullanılarak işlem hatlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="2ff3d-375">Monitor and manage pipelines by using Azure portal blades</span></span>](data-factory-monitor-manage-pipelines.md)
- [<span data-ttu-id="2ff3d-376">İzleme ve hello izleme ve yönetim uygulaması kullanılarak işlem hatlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="2ff3d-376">Monitor and manage pipelines by using hello Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a><span data-ttu-id="2ff3d-377">Kapsamlı veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="2ff3d-377">Scoped datasets</span></span>
<span data-ttu-id="2ff3d-378">Hello kullanarak kapsamlı tooa ardışık düzen olan veri kümeleri oluşturabilirsiniz **veri kümeleri** özelliği.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-378">You can create datasets that are scoped tooa pipeline by using hello **datasets** property.</span></span> <span data-ttu-id="2ff3d-379">Bu veri kümeleri yalnızca kullanılabilir etkinlikler içinde bu ardışık düzen tarafından diğer ardışık etkinlikler tarafından değil.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-379">These datasets can only be used by activities within this pipeline, not by activities in other pipelines.</span></span> <span data-ttu-id="2ff3d-380">Aşağıdaki örneğine hello içinde hello ardışık düzeni kullanılan iki veri kümesi (InputDataset rdc ve OutputDataset rdc) toobe ile işlem hattı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-380">hello following example defines a pipeline with two datasets (InputDataset-rdc and OutputDataset-rdc) toobe used within hello pipeline.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="2ff3d-381">Kapsamlı veri kümeleri, yalnızca tek seferlik ardışık düzen ile desteklenir (burada **pipelineMode** çok ayarlanır**OneTime**).</span><span class="sxs-lookup"><span data-stu-id="2ff3d-381">Scoped datasets are supported only with one-time pipelines (where **pipelineMode** is set too**OneTime**).</span></span> <span data-ttu-id="2ff3d-382">Bkz: [Onetime ardışık düzen](data-factory-create-pipelines.md#onetime-pipeline) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="2ff3d-382">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="2ff3d-383">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2ff3d-383">Next steps</span></span>
- <span data-ttu-id="2ff3d-384">Ardışık Düzen hakkında daha fazla bilgi için bkz: [oluşturma ardışık düzen](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="2ff3d-384">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md).</span></span> 
- <span data-ttu-id="2ff3d-385">Ardışık Düzen nasıl zamanlanmış ve yürütülen hakkında daha fazla bilgi için bkz: [zamanlama ve yürütme Azure Data factory'de](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="2ff3d-385">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md).</span></span> 
