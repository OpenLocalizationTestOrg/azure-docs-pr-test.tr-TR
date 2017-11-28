---
title: "Hadoop akış etkinliği - Azure kullanarak veri dönüştürme | Microsoft Docs"
description: "Hadoop akış etkinliği bir Azure data factory üzerinde-isteğe bağlı/bilgisayarınızı kendi Hdınsight kümesi üzerinde çalışan Hadoop akış programlar verileri dönüştürmek için nasıl kullanabileceğinizi öğrenin."
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
ms.openlocfilehash: bfe62aa60f5a0ff339e1d495d22a5fdfac10d5dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="935a2-103">Hadoop akış etkinliği Azure Data Factory kullanarak veri dönüştürme</span><span class="sxs-lookup"><span data-stu-id="935a2-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="935a2-104">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="935a2-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="935a2-105">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="935a2-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="935a2-106">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="935a2-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="935a2-107">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="935a2-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="935a2-108">Spark etkinliği</span><span class="sxs-lookup"><span data-stu-id="935a2-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="935a2-109">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="935a2-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="935a2-110">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="935a2-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="935a2-111">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="935a2-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="935a2-112">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="935a2-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="935a2-113">.NET özel etkinlik</span><span class="sxs-lookup"><span data-stu-id="935a2-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="935a2-114">HDInsightStreamingActivity etkinlik kullanabileceğiniz bir Azure Data Factory işlem hattı Hadoop akış işten çağırma.</span><span class="sxs-lookup"><span data-stu-id="935a2-114">You can use the HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="935a2-115">Aşağıdaki JSON parçacığı HDInsightStreamingActivity bir ardışık düzen JSON dosyası kullanarak sözdizimi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="935a2-115">The following JSON snippet shows the syntax for using the HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="935a2-116">Hdınsight akış etkinliğinde Data Factory [ardışık düzen](data-factory-create-pipelines.md) üzerinde Hadoop akış programları yürütür [kendi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) veya [isteğe bağlı](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux tabanlı Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="935a2-116">The HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="935a2-117">Bu makalede derlemeler [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) makalesi, veri dönüştürme ve desteklenen dönüştürme etkinliklerinin genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="935a2-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="935a2-118">Azure Data Factory yeniyseniz okuyun [Azure Data Factory'ye giriş](data-factory-introduction.md) ve öğretici: [ilk veri hattınızı yapı](data-factory-build-your-first-pipeline.md) bu makaleyi okumadan önce.</span><span class="sxs-lookup"><span data-stu-id="935a2-118">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="935a2-119">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="935a2-119">JSON sample</span></span>
<span data-ttu-id="935a2-120">Hdınsight kümesi örnek programlar (wc.exe ve cat.exe) ve veri (davinci.txt) ile otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="935a2-120">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="935a2-121">Varsayılan olarak, Hdınsight kümesi tarafından kullanılan kapsayıcının adını küme adıdır.</span><span class="sxs-lookup"><span data-stu-id="935a2-121">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span></span> <span data-ttu-id="935a2-122">Örneğin, küme adınızı myhdicluster ise, ilişkili blob kapsayıcısının adı myhdicluster olacaktır.</span><span class="sxs-lookup"><span data-stu-id="935a2-122">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span></span> 

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

<span data-ttu-id="935a2-123">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="935a2-123">Note the following points:</span></span>

1. <span data-ttu-id="935a2-124">Ayarlama **linkedServiceName** mapreduce iş akışında çalıştırıldığı, Hdınsight işaret bağlı hizmetin adı küme.</span><span class="sxs-lookup"><span data-stu-id="935a2-124">Set the **linkedServiceName** to the name of the linked service that points to your HDInsight cluster on which the streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="935a2-125">Etkinlik türünü ayarlayın **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="935a2-125">Set the type of the activity to **HDInsightStreaming**.</span></span>
3. <span data-ttu-id="935a2-126">İçin **Eşleyici** özelliği Eşleyici yürütülebilir adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="935a2-126">For the **mapper** property, specify the name of mapper executable.</span></span> <span data-ttu-id="935a2-127">Örnekte, cat.exe yürütülebilir Eşleyici ' dir.</span><span class="sxs-lookup"><span data-stu-id="935a2-127">In the example, cat.exe is the mapper executable.</span></span>
4. <span data-ttu-id="935a2-128">İçin **reducer** özelliği reducer yürütülebilir adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="935a2-128">For the **reducer** property, specify the name of reducer executable.</span></span> <span data-ttu-id="935a2-129">Örnekte, wc.exe yürütülebilir reducer ' dir.</span><span class="sxs-lookup"><span data-stu-id="935a2-129">In the example, wc.exe is the reducer executable.</span></span>
5. <span data-ttu-id="935a2-130">İçin **giriş** türü özelliği, Eşleştiricisi (konum dahil) giriş dosyası belirtin.</span><span class="sxs-lookup"><span data-stu-id="935a2-130">For the **input** type property, specify the input file (including the location) for the mapper.</span></span> <span data-ttu-id="935a2-131">Örnekte: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample blob kapsayıcısı, veri/örnek/Gutenberg klasördür ve davinci.txt blob.</span><span class="sxs-lookup"><span data-stu-id="935a2-131">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span>
6. <span data-ttu-id="935a2-132">İçin **çıkış** türü özelliği, çıktı dosyası (konum dahil) için reducer belirtin.</span><span class="sxs-lookup"><span data-stu-id="935a2-132">For the **output** type property, specify the output file (including the location) for the reducer.</span></span> <span data-ttu-id="935a2-133">Hadoop akış işi çıkışı, bu özellik için belirtilen konuma yazılır.</span><span class="sxs-lookup"><span data-stu-id="935a2-133">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span>
7. <span data-ttu-id="935a2-134">İçinde **filePaths** bölümünde, Eşleyici ve reducer yürütülebilir dosyalar için yollarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="935a2-134">In the **filePaths** section, specify the paths for the mapper and reducer executables.</span></span> <span data-ttu-id="935a2-135">Örnekte: "adfsample/example/apps/wc.exe" adfsample blob kapsayıcısı, örnek/uygulamaları klasördür ve wc.exe çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="935a2-135">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span>
8. <span data-ttu-id="935a2-136">İçin **fileLinkedService** özelliği filePaths bölümünde belirtilen dosyaları içeren Azure depolama temsil eden Azure Storage bağlı hizmeti belirtin.</span><span class="sxs-lookup"><span data-stu-id="935a2-136">For the **fileLinkedService** property, specify the Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span>
9. <span data-ttu-id="935a2-137">İçin **bağımsız değişkenleri** özelliği, iş akışında bağımsız değişkenleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="935a2-137">For the **arguments** property, specify the arguments for the streaming job.</span></span>
10. <span data-ttu-id="935a2-138">**Getdebugınfo** özelliği isteğe bağlı bir öğedir.</span><span class="sxs-lookup"><span data-stu-id="935a2-138">The **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="935a2-139">Hata için ayarlandığında, günlükleri yalnızca hatada indirilir.</span><span class="sxs-lookup"><span data-stu-id="935a2-139">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="935a2-140">Her zaman olarak ayarlandığında, günlükleri yürütme durumu bağımsız olarak daima yüklenir.</span><span class="sxs-lookup"><span data-stu-id="935a2-140">When it is set to Always, logs are always downloaded irrespective of the execution status.</span></span>

> [!NOTE]
> <span data-ttu-id="935a2-141">Örnekte gösterildiği gibi bir çıktı veri kümesi için Hadoop akış etkinliği için belirlediğiniz **çıkarır** özelliği.</span><span class="sxs-lookup"><span data-stu-id="935a2-141">As shown in the example, you specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="935a2-142">Bu veri kümesi yalnızca ardışık düzen zamanlama sürücü için gereken bir kukla dataset ' dir.</span><span class="sxs-lookup"><span data-stu-id="935a2-142">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span> <span data-ttu-id="935a2-143">Hiçbir girdi veri kümesi için etkinliği belirtmek gerekmez **girişleri** özelliği.</span><span class="sxs-lookup"><span data-stu-id="935a2-143">You do not need to specify any input dataset for the activity for the **inputs** property.</span></span>  
> 
> 

## <a name="example"></a><span data-ttu-id="935a2-144">Örnek</span><span class="sxs-lookup"><span data-stu-id="935a2-144">Example</span></span>
<span data-ttu-id="935a2-145">Ardışık Düzen bu kılavuzda, Azure Hdınsight kümesinde sözcük sayımı akış Haritası/azaltın programı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="935a2-145">The pipeline in this walkthrough runs the Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="935a2-146">Bağlı hizmetler</span><span class="sxs-lookup"><span data-stu-id="935a2-146">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="935a2-147">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="935a2-147">Azure Storage linked service</span></span>
<span data-ttu-id="935a2-148">İlk olarak, Azure data factory Azure Hdınsight küme tarafından kullanılan Azure Storage bağlamak için bağlı hizmet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="935a2-148">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="935a2-149">Hesap adı ve hesap anahtarı adı ve Azure depolama alanınızı anahtarı ile değiştirmek, kopyala/yapıştır aşağıdaki kod, unutmayın.</span><span class="sxs-lookup"><span data-stu-id="935a2-149">If you copy/paste the following code, do not forget to replace account name and account key with the name and key of your Azure Storage.</span></span> 

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="935a2-150">Azure Hdınsight bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="935a2-150">Azure HDInsight linked service</span></span>
<span data-ttu-id="935a2-151">Ardından, Azure Hdınsight kümenizi Azure data factory'ye bağlamak için bağlı hizmet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="935a2-151">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="935a2-152">Kopyala/yapıştır aşağıdaki kod, Hdınsight küme adı Hdınsight kümenizin adıyla değiştirin ve kullanıcı adı ve parola değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="935a2-152">If you copy/paste the following code, replace HDInsight cluster name with the name of your HDInsight cluster, and change user name and password values.</span></span> 

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

### <a name="datasets"></a><span data-ttu-id="935a2-153">Veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="935a2-153">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="935a2-154">Çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="935a2-154">Output dataset</span></span>
<span data-ttu-id="935a2-155">Ardışık Düzen Bu örnekte, tüm girişleri almaz.</span><span class="sxs-lookup"><span data-stu-id="935a2-155">The pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="935a2-156">Hdınsight akış etkinliği için bir çıkış veri kümesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="935a2-156">You specify an output dataset for the HDInsight Streaming Activity.</span></span> <span data-ttu-id="935a2-157">Bu veri kümesi yalnızca ardışık düzen zamanlama sürücü için gereken bir kukla dataset ' dir.</span><span class="sxs-lookup"><span data-stu-id="935a2-157">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span> 

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

### <a name="pipeline"></a><span data-ttu-id="935a2-158">İşlem hattı</span><span class="sxs-lookup"><span data-stu-id="935a2-158">Pipeline</span></span>
<span data-ttu-id="935a2-159">Bu örnekte ardışık türünde yalnızca bir etkinlik vardır: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="935a2-159">The pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="935a2-160">Hdınsight kümesi örnek programlar (wc.exe ve cat.exe) ve veri (davinci.txt) ile otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="935a2-160">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="935a2-161">Varsayılan olarak, Hdınsight kümesi tarafından kullanılan kapsayıcının adını küme adıdır.</span><span class="sxs-lookup"><span data-stu-id="935a2-161">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span></span> <span data-ttu-id="935a2-162">Örneğin, küme adınızı myhdicluster ise, ilişkili blob kapsayıcısının adı myhdicluster olacaktır.</span><span class="sxs-lookup"><span data-stu-id="935a2-162">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span></span>  

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
## <a name="see-also"></a><span data-ttu-id="935a2-163">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="935a2-163">See Also</span></span>
* [<span data-ttu-id="935a2-164">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="935a2-164">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="935a2-165">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="935a2-165">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="935a2-166">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="935a2-166">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="935a2-167">Spark programlarını çağırma</span><span class="sxs-lookup"><span data-stu-id="935a2-167">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="935a2-168">R betiklerini çağırma</span><span class="sxs-lookup"><span data-stu-id="935a2-168">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

