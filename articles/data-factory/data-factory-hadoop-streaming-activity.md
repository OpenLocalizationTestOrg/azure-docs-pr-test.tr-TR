---
title: "Hadoop akış etkinliği - Azure kullanarak aaaTransform veri | Microsoft Docs"
description: "Üzerinde-isteğe bağlı/bilgisayarınızı kendi Hdınsight kümesi üzerinde çalışan Hadoop akış programlar bir Azure veri fabrikası tootransform verileri Hadoop akış etkinliği hello nasıl kullanabileceğinizi öğrenin."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4c3ff8f2-2c00-434e-a416-06dfca2c41ec
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: a7ddb7268f47162709a9c8136ccd69e0b7d4ad7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="8b0fe-103">Hadoop akış etkinliği Azure Data Factory kullanarak veri dönüştürme</span><span class="sxs-lookup"><span data-stu-id="8b0fe-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="8b0fe-104">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="8b0fe-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="8b0fe-105">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="8b0fe-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="8b0fe-106">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="8b0fe-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="8b0fe-107">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="8b0fe-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="8b0fe-108">Spark etkinliği</span><span class="sxs-lookup"><span data-stu-id="8b0fe-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="8b0fe-109">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="8b0fe-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="8b0fe-110">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="8b0fe-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="8b0fe-111">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="8b0fe-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="8b0fe-112">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="8b0fe-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="8b0fe-113">.NET özel etkinlik</span><span class="sxs-lookup"><span data-stu-id="8b0fe-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="8b0fe-114">Kullanabileceğiniz hello HDInsightStreamingActivity etkinliği Azure Data Factory işlem hattı Hadoop akış işten çağırma.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-114">You can use hello HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="8b0fe-115">Merhaba aşağıdaki JSON parçacığı hello HDInsightStreamingActivity bir ardışık düzen JSON dosyası kullanarak hello sözdizimi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-115">hello following JSON snippet shows hello syntax for using hello HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="8b0fe-116">Merhaba Hdınsight akış etkinliğinde Data Factory [ardışık düzen](data-factory-create-pipelines.md) üzerinde Hadoop akış programları yürütür [kendi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) veya [isteğe bağlı](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux tabanlı Hdınsight Küme.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-116">hello HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="8b0fe-117">Bu makale üzerinde hello derlemeler [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) makalesi, veri dönüştürme ve desteklenen hello dönüştürme etkinliklerinin genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="8b0fe-118">Yeni tooAzure Data Factory varsa okuyun [giriş tooAzure Data Factory](data-factory-introduction.md) ve öğretici hello: [ilk veri hattınızı yapı](data-factory-build-your-first-pipeline.md) bu makaleyi okumadan önce.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-118">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="8b0fe-119">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="8b0fe-119">JSON sample</span></span>
<span data-ttu-id="8b0fe-120">Merhaba Hdınsight kümesi örnek programlar (wc.exe ve cat.exe) ve veri (davinci.txt) ile otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-120">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="8b0fe-121">Varsayılan olarak, hello Hdınsight küme tarafından kullanılan hello kapsayıcının adını hello hello kümenin kendisi adıdır.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-121">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="8b0fe-122">Örneğin, küme adınızı myhdicluster ise, ilişkili hello blob kapsayıcısının adı myhdicluster olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-122">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span> 

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<nameofthecluster>/example/apps/wc.exe",
                        "<nameofthecluster>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "AzureStorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00Z",
        "end": "2014-01-05T00:00:00Z"
    }
}
```

<span data-ttu-id="8b0fe-123">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="8b0fe-123">Note hello following points:</span></span>

1. <span data-ttu-id="8b0fe-124">Set hello **linkedServiceName** hello toohello adını bağlantılı mapreduce akış hangi hello iş çalıştırıldığında tooyour Hdınsight kümesi işaret hizmeti.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-124">Set hello **linkedServiceName** toohello name of hello linked service that points tooyour HDInsight cluster on which hello streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="8b0fe-125">Merhaba etkinlik Hello türü çok ayarlamak**HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-125">Set hello type of hello activity too**HDInsightStreaming**.</span></span>
3. <span data-ttu-id="8b0fe-126">Hello için **Eşleyici** özelliği Eşleyici yürütülebilir hello adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-126">For hello **mapper** property, specify hello name of mapper executable.</span></span> <span data-ttu-id="8b0fe-127">Merhaba örnekte cat.exe hello Eşleyici yürütülebilir ' dir.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-127">In hello example, cat.exe is hello mapper executable.</span></span>
4. <span data-ttu-id="8b0fe-128">Hello için **reducer** özelliği reducer yürütülebilir hello adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-128">For hello **reducer** property, specify hello name of reducer executable.</span></span> <span data-ttu-id="8b0fe-129">Merhaba örnekte wc.exe hello reducer yürütülebilir ' dir.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-129">In hello example, wc.exe is hello reducer executable.</span></span>
5. <span data-ttu-id="8b0fe-130">Hello için **giriş** türü özelliği, hello Eşleştiricisi hello giriş dosyası (Merhaba konum dahil) belirtin.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-130">For hello **input** type property, specify hello input file (including hello location) for hello mapper.</span></span> <span data-ttu-id="8b0fe-131">Merhaba örnekte: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample hello blob kapsayıcısı, veri/örnek/Gutenberg hello klasördür ve davinci.txt hello blob.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-131">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span>
6. <span data-ttu-id="8b0fe-132">Hello için **çıkış** türü özelliği, hello reducer hello çıktı dosyası (Merhaba konum dahil) belirtin.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-132">For hello **output** type property, specify hello output file (including hello location) for hello reducer.</span></span> <span data-ttu-id="8b0fe-133">Merhaba çıktısı hello Hadoop akış işi, bu özelliği için belirtilen toohello konumu yazılır.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-133">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span>
7. <span data-ttu-id="8b0fe-134">Merhaba, **filePaths** bölümünde, hello Eşleyici ve reducer yürütülebilir dosyalar için hello yollarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-134">In hello **filePaths** section, specify hello paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="8b0fe-135">Merhaba örnekte: "adfsample/example/apps/wc.exe" adfsample hello blob kapsayıcısı, örnek/uygulamaları hello klasördür ve wc.exe hello çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-135">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span>
8. <span data-ttu-id="8b0fe-136">Hello için **fileLinkedService** özelliği, hello Azure temsil eden bağlı hizmet hello hello filePaths bölümünde belirtilen hello dosyaları içeren Azure depolama depolama belirtin.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-136">For hello **fileLinkedService** property, specify hello Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span>
9. <span data-ttu-id="8b0fe-137">Hello için **bağımsız değişkenleri** özelliği, iş akışı hello hello bağımsız değişkenleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-137">For hello **arguments** property, specify hello arguments for hello streaming job.</span></span>
10. <span data-ttu-id="8b0fe-138">Merhaba **Getdebugınfo** özelliği isteğe bağlı bir öğedir.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-138">hello **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="8b0fe-139">TooFailure ayarlandığında hello günlükleri yalnızca hatada indirilir.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-139">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="8b0fe-140">TooAlways ayarlandığında, günlükleri hello yürütme durumu bağımsız olarak daima yüklenir.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-140">When it is set tooAlways, logs are always downloaded irrespective of hello execution status.</span></span>

> [!NOTE]
> <span data-ttu-id="8b0fe-141">Merhaba örnekte gösterildiği gibi bir çıktı veri kümesi hello Merhaba Hadoop akış etkinliği için belirttiğiniz **çıkarır** özelliği.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-141">As shown in hello example, you specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="8b0fe-142">Bu veri kümesi yalnızca gerekli toodrive hello ardışık düzen zamanlaması bir kukla dataset ' dir.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-142">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> <span data-ttu-id="8b0fe-143">Toospecify hiçbir girdi veri kümesi hello hello etkinliğinin gerekmez **girişleri** özelliği.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-143">You do not need toospecify any input dataset for hello activity for hello **inputs** property.</span></span>  
> 
> 

## <a name="example"></a><span data-ttu-id="8b0fe-144">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b0fe-144">Example</span></span>
<span data-ttu-id="8b0fe-145">Bu kılavuzda Hello ardışık Azure Hdınsight kümesinde hello sözcük sayımı akış eşleme/azaltın programı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-145">hello pipeline in this walkthrough runs hello Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="8b0fe-146">Bağlı hizmetler</span><span class="sxs-lookup"><span data-stu-id="8b0fe-146">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="8b0fe-147">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="8b0fe-147">Azure Storage linked service</span></span>
<span data-ttu-id="8b0fe-148">İlk olarak, bağlantılı hizmet toolink hello hello Azure Hdınsight küme toohello Azure veri fabrikası tarafından kullanılan Azure Storage oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-148">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="8b0fe-149">Kopyala/yapıştır koddan Merhaba, hello adla tooreplace hesap adını ve hesap anahtarını ve Azure depolama anahtarını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-149">If you copy/paste hello following code, do not forget tooreplace account name and account key with hello name and key of your Azure Storage.</span></span> 

```JSON
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>"
        }
    }
}
```

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="8b0fe-150">Azure Hdınsight bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="8b0fe-150">Azure HDInsight linked service</span></span>
<span data-ttu-id="8b0fe-151">Ardından, Azure Hdınsight küme toohello Azure data factory'nizi bağlantılı hizmet toolink oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-151">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="8b0fe-152">Kopyala/yapıştır koddan Merhaba, Hdınsight küme adı hello Hdınsight kümenizin adıyla değiştirin ve kullanıcı adı ve parola değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-152">If you copy/paste hello following code, replace HDInsight cluster name with hello name of your HDInsight cluster, and change user name and password values.</span></span> 

```JSON
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": "https://<HDInsight cluster name>.azurehdinsight.net",
            "userName": "admin",
            "password": "**********",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

### <a name="datasets"></a><span data-ttu-id="8b0fe-153">Veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="8b0fe-153">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="8b0fe-154">Çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="8b0fe-154">Output dataset</span></span>
<span data-ttu-id="8b0fe-155">Bu örnekte Hello ardışık tüm girişleri almaz.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-155">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="8b0fe-156">Merhaba Hdınsight akış etkinliği için bir çıkış veri kümesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-156">You specify an output dataset for hello HDInsight Streaming Activity.</span></span> <span data-ttu-id="8b0fe-157">Bu veri kümesi yalnızca gerekli toodrive hello ardışık düzen zamanlaması bir kukla dataset ' dir.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-157">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> 

```JSON
{
    "name": "StreamingOutputDataset",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "adftutorial/streamingdata/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="8b0fe-158">İşlem hattı</span><span class="sxs-lookup"><span data-stu-id="8b0fe-158">Pipeline</span></span>
<span data-ttu-id="8b0fe-159">Bu örnekte Hello ardışık türünde yalnızca bir etkinlik vardır: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-159">hello pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="8b0fe-160">Merhaba Hdınsight kümesi örnek programlar (wc.exe ve cat.exe) ve veri (davinci.txt) ile otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-160">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="8b0fe-161">Varsayılan olarak, hello Hdınsight küme tarafından kullanılan hello kapsayıcının adını hello hello kümenin kendisi adıdır.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-161">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="8b0fe-162">Örneğin, küme adınızı myhdicluster ise, ilişkili hello blob kapsayıcısının adı myhdicluster olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-162">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span>  

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<blobcontainer>/example/apps/wc.exe",
                        "<blobcontainer>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "StorageLinkedService"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00Z",
        "end": "2017-01-04T00:00:00Z"
    }
}
```
## <a name="see-also"></a><span data-ttu-id="8b0fe-163">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8b0fe-163">See Also</span></span>
* [<span data-ttu-id="8b0fe-164">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="8b0fe-164">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="8b0fe-165">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="8b0fe-165">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="8b0fe-166">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="8b0fe-166">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="8b0fe-167">Spark programlarını çağırma</span><span class="sxs-lookup"><span data-stu-id="8b0fe-167">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="8b0fe-168">R betiklerini çağırma</span><span class="sxs-lookup"><span data-stu-id="8b0fe-168">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

