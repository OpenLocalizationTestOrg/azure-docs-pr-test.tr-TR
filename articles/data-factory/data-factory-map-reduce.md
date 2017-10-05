---
title: "Azure Data Factory MapReduce programdan çağırma"
description: "MapReduce programlar bir Azure Hdınsight kümesinde bir Azure veri fabrikası'ndan çalıştırılarak verileri işlemek öğrenin."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c34db93f-570a-44f1-a7d6-00390f4dc0fa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 55fc2196cb4ba50eced4a463914ae188217d0fed
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="e2e16-103">Veri Fabrikası MapReduce programlardan çağırma</span><span class="sxs-lookup"><span data-stu-id="e2e16-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="e2e16-104">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="e2e16-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="e2e16-105">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="e2e16-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="e2e16-106">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="e2e16-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="e2e16-107">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="e2e16-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="e2e16-108">Spark etkinliği</span><span class="sxs-lookup"><span data-stu-id="e2e16-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="e2e16-109">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="e2e16-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="e2e16-110">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="e2e16-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="e2e16-111">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="e2e16-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="e2e16-112">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="e2e16-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="e2e16-113">.NET özel etkinlik</span><span class="sxs-lookup"><span data-stu-id="e2e16-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="e2e16-114">Veri Fabrikası'nda Hdınsight MapReduce etkinliği [ardışık düzen](data-factory-create-pipelines.md) üzerinde MapReduce programları yürütür [kendi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) veya [isteğe bağlı](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux tabanlı Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="e2e16-114">The HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="e2e16-115">Bu makalede derlemeler [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) makalesi, veri dönüştürme ve desteklenen dönüştürme etkinliklerinin genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="e2e16-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="e2e16-116">Azure Data Factory yeniyseniz okuyun [Azure Data Factory'ye giriş](data-factory-introduction.md) ve öğretici: [ilk veri hattınızı yapı](data-factory-build-your-first-pipeline.md) bu makaleyi okumadan önce.</span><span class="sxs-lookup"><span data-stu-id="e2e16-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="e2e16-117">Giriş</span><span class="sxs-lookup"><span data-stu-id="e2e16-117">Introduction</span></span>
<span data-ttu-id="e2e16-118">Bir Azure data factory işlem hattı bağlantılı işlem hizmetlerini kullanarak bağlantılı depolama Hizmetleri'nde verilerini işler.</span><span class="sxs-lookup"><span data-stu-id="e2e16-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="e2e16-119">Burada her etkinlik özel işleme işlemi gerçekleştiren etkinlikler dizisini içerir.</span><span class="sxs-lookup"><span data-stu-id="e2e16-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="e2e16-120">Bu makalede, Hdınsight MapReduce etkinliği kullanmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="e2e16-120">This article describes using the HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="e2e16-121">Bkz: [Pig](data-factory-pig-activity.md) ve [Hive](data-factory-hive-activity.md) Pig/Hive çalıştırma hakkında ayrıntılı bilgi için komut dosyaları Windows/Linux tabanlı Hdınsight üzerinde bir ardışık düzen tarafından Hdınsight Pig ve Hive etkinlikleri kullanarak küme.</span><span class="sxs-lookup"><span data-stu-id="e2e16-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="e2e16-122">Hdınsight MapReduce etkinliği için JSON</span><span class="sxs-lookup"><span data-stu-id="e2e16-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="e2e16-123">Hdınsight etkinliği JSON tanımında:</span><span class="sxs-lookup"><span data-stu-id="e2e16-123">In the JSON definition for the HDInsight Activity:</span></span> 

1. <span data-ttu-id="e2e16-124">Ayarlama **türü** , **etkinlik** için **Hdınsight**.</span><span class="sxs-lookup"><span data-stu-id="e2e16-124">Set the **type** of the **activity** to **HDInsight**.</span></span>
2. <span data-ttu-id="e2e16-125">Sınıfı için adını belirtin **className** özelliği.</span><span class="sxs-lookup"><span data-stu-id="e2e16-125">Specify the name of the class for **className** property.</span></span>
3. <span data-ttu-id="e2e16-126">Dosya adı dahil olmak üzere JAR dosyasının yolunu belirtin **jarFilePath** özelliği.</span><span class="sxs-lookup"><span data-stu-id="e2e16-126">Specify the path to the JAR file including the file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="e2e16-127">Azure Blob Storage için JAR dosyasını içeren başvurduğu bağlantılı hizmet belirtin **jarLinkedService** özelliği.</span><span class="sxs-lookup"><span data-stu-id="e2e16-127">Specify the linked service that refers to the Azure Blob Storage that contains the JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="e2e16-128">MapReduce program için herhangi bir bağımsız değişken belirtin **bağımsız değişkenleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="e2e16-128">Specify any arguments for the MapReduce program in the **arguments** section.</span></span> <span data-ttu-id="e2e16-129">Çalışma zamanında gördüğünüz birkaç ek bağımsız değişkenler (örneğin: mapreduce.job.tags) MapReduce çerçeveden.</span><span class="sxs-lookup"><span data-stu-id="e2e16-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="e2e16-130">MapReduce bağımsız değişkenleriyle ayırt etmek için seçeneği ve değer bağımsız değişken olarak aşağıdaki örnekte gösterildiği gibi kullanmayı düşünün (- s,--giriş,--çıkış vb. göre bunların değerleri hemen ardından Seçenekler belirtilmiştir).</span><span class="sxs-lookup"><span data-stu-id="e2e16-130">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix to determine the similarity between 2 items",
            "activities": [
                {
                    "type": "HDInsightMapReduce",
                    "typeProperties": {
                        "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                        "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                        "jarLinkedService": "StorageLinkedService",
                        "arguments": [
                            "-s",
                            "SIMILARITY_LOGLIKELIHOOD",
                            "--input",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input",
                            "--output",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/",
                            "--maxSimilaritiesPerItem",
                            "500",
                            "--tempDir",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"
                        ]
                    },
                    "inputs": [
                        {
                            "name": "MahoutInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "MahoutOutput"
                        }
                    ],
                    "policy": {
                        "timeout": "01:00:00",
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "MahoutActivity",
                    "description": "Custom Map Reduce to generate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
<span data-ttu-id="e2e16-131">Hdınsight MapReduce etkinliği Hdınsight kümesinde herhangi MapReduce jar dosyasını çalıştırmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2e16-131">You can use the HDInsight MapReduce Activity to run any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="e2e16-132">Aşağıdaki örnek JSON tanımında bir ardışık düzen, Hdınsight etkinliği Mahout JAR dosyasını çalıştırmak için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="e2e16-132">In the following sample JSON definition of a pipeline, the HDInsight Activity is configured to run a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="e2e16-133">Github'da örnek</span><span class="sxs-lookup"><span data-stu-id="e2e16-133">Sample on GitHub</span></span>
<span data-ttu-id="e2e16-134">Hdınsight MapReduce etkinliğinden kullanmak için bir örnek indirebilirsiniz: [veri fabrikası örneği github'daki](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span><span class="sxs-lookup"><span data-stu-id="e2e16-134">You can download a sample for using the HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-the-word-count-program"></a><span data-ttu-id="e2e16-135">Sözcük sayısını programı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e2e16-135">Running the Word Count program</span></span>
<span data-ttu-id="e2e16-136">Ardışık Düzen Bu örnekte, Azure Hdınsight kümesinde sözcük sayımı harita/azaltın programı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="e2e16-136">The pipeline in this example runs the Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="e2e16-137">Bağlı hizmetler</span><span class="sxs-lookup"><span data-stu-id="e2e16-137">Linked Services</span></span>
<span data-ttu-id="e2e16-138">İlk olarak, Azure data factory Azure Hdınsight küme tarafından kullanılan Azure Storage bağlamak için bağlı hizmet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e2e16-138">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="e2e16-139">Kopyala/yapıştır aşağıdaki kod, değiştirmek unutmadığınızdan **hesap adı** ve **hesap anahtarı** adı ile Azure depolama alanınızı anahtarı.</span><span class="sxs-lookup"><span data-stu-id="e2e16-139">If you copy/paste the following code, do not forget to replace **account name** and **account key** with the name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="e2e16-140">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="e2e16-140">Azure Storage linked service</span></span>

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="e2e16-141">Azure Hdınsight bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="e2e16-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="e2e16-142">Ardından, Azure Hdınsight kümenizi Azure data factory'ye bağlamak için bağlı hizmet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e2e16-142">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="e2e16-143">Kopyala/yapıştır aşağıdaki kod, yerini **Hdınsight küme adı** Hdınsight kümesi ve kullanıcı adı ve parola değerleri değiştirme ada sahip.</span><span class="sxs-lookup"><span data-stu-id="e2e16-143">If you copy/paste the following code, replace **HDInsight cluster name** with the name of your HDInsight cluster, and change user name and password values.</span></span>   

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

### <a name="datasets"></a><span data-ttu-id="e2e16-144">Veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="e2e16-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="e2e16-145">Çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="e2e16-145">Output dataset</span></span>
<span data-ttu-id="e2e16-146">Ardışık Düzen Bu örnekte, tüm girişleri almaz.</span><span class="sxs-lookup"><span data-stu-id="e2e16-146">The pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="e2e16-147">Hdınsight MapReduce etkinliği için bir çıkış veri kümesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="e2e16-147">You specify an output dataset for the HDInsight MapReduce Activity.</span></span> <span data-ttu-id="e2e16-148">Bu veri kümesi yalnızca ardışık düzen zamanlama sürücü için gereken bir kukla dataset ' dir.</span><span class="sxs-lookup"><span data-stu-id="e2e16-148">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span>  

```JSON
{
    "name": "MROutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "WordCountOutput1.txt",
            "folderPath": "example/data/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="e2e16-149">İşlem hattı</span><span class="sxs-lookup"><span data-stu-id="e2e16-149">Pipeline</span></span>
<span data-ttu-id="e2e16-150">Bu örnekte ardışık türünde yalnızca bir etkinlik vardır: HDInsightMapReduce.</span><span class="sxs-lookup"><span data-stu-id="e2e16-150">The pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="e2e16-151">JSON önemli özelliklerin bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e2e16-151">Some of the important properties in the JSON are:</span></span> 

| <span data-ttu-id="e2e16-152">Özellik</span><span class="sxs-lookup"><span data-stu-id="e2e16-152">Property</span></span> | <span data-ttu-id="e2e16-153">Notlar</span><span class="sxs-lookup"><span data-stu-id="e2e16-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="e2e16-154">type</span><span class="sxs-lookup"><span data-stu-id="e2e16-154">type</span></span> |<span data-ttu-id="e2e16-155">Türü ayarlamak **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="e2e16-155">The type must be set to **HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="e2e16-156">className</span><span class="sxs-lookup"><span data-stu-id="e2e16-156">className</span></span> |<span data-ttu-id="e2e16-157">Sınıf adıdır: **wordcount**</span><span class="sxs-lookup"><span data-stu-id="e2e16-157">Name of the class is: **wordcount**</span></span> |
| <span data-ttu-id="e2e16-158">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="e2e16-158">jarFilePath</span></span> |<span data-ttu-id="e2e16-159">Sınıf içeren jar dosyasının yolu.</span><span class="sxs-lookup"><span data-stu-id="e2e16-159">Path to the jar file containing the class.</span></span> <span data-ttu-id="e2e16-160">Kopyala/yapıştır aşağıdaki kod, kümenin adını değiştirmeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e2e16-160">If you copy/paste the following code, don't forget to change the name of the cluster.</span></span> |
| <span data-ttu-id="e2e16-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="e2e16-161">jarLinkedService</span></span> |<span data-ttu-id="e2e16-162">Jar dosyasını içeren azure depolama bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="e2e16-162">Azure Storage linked service that contains the jar file.</span></span> <span data-ttu-id="e2e16-163">Bu bağlı hizmetin Hdınsight kümesi ile ilişkili depolama ifade eder.</span><span class="sxs-lookup"><span data-stu-id="e2e16-163">This linked service refers to the storage that is associated with the HDInsight cluster.</span></span> |
| <span data-ttu-id="e2e16-164">Bağımsız değişkenler</span><span class="sxs-lookup"><span data-stu-id="e2e16-164">arguments</span></span> |<span data-ttu-id="e2e16-165">Wordcount program iki bağımsız değişken, bir giriş ve çıkış alır.</span><span class="sxs-lookup"><span data-stu-id="e2e16-165">The wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="e2e16-166">Giriş dosyası davinci.txt dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="e2e16-166">The input file is the davinci.txt file.</span></span> |
| <span data-ttu-id="e2e16-167">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="e2e16-167">frequency/interval</span></span> |<span data-ttu-id="e2e16-168">Bu özelliklerin değerlerini çıktı veri kümesi eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="e2e16-168">The values for these properties match the output dataset.</span></span> |
| <span data-ttu-id="e2e16-169">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="e2e16-169">linkedServiceName</span></span> |<span data-ttu-id="e2e16-170">daha önce oluşturmuştunuz Hdınsight bağlı hizmeti anlamına gelmektedir.</span><span class="sxs-lookup"><span data-stu-id="e2e16-170">refers to the HDInsight linked service you had created earlier.</span></span> |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run the Word Count Program",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "wordcount",
                    "jarFilePath": "<HDInsight cluster name>/example/jars/hadoop-examples.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": [
                        "/example/data/gutenberg/davinci.txt",
                        "/example/data/WordCountOutput1"
                    ]
                },
                "outputs": [
                    {
                        "name": "MROutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "MRActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-03T00:00:00Z",
        "end": "2014-01-04T00:00:00Z"
    }
}
```

## <a name="run-spark-programs"></a><span data-ttu-id="e2e16-171">Spark programları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e2e16-171">Run Spark programs</span></span>
<span data-ttu-id="e2e16-172">MapReduce etkinliğini kullanarak HDInsight Spark kümenizde Spark programları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2e16-172">You can use MapReduce activity to run Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="e2e16-173">Ayrıntılar için bkz. [Azure Data Factory’den Spark programlarını çağırma](data-factory-spark.md).</span><span class="sxs-lookup"><span data-stu-id="e2e16-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="e2e16-174">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="e2e16-174">See Also</span></span>
* [<span data-ttu-id="e2e16-175">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="e2e16-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="e2e16-176">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="e2e16-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="e2e16-177">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="e2e16-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="e2e16-178">Spark programlarını çağırma</span><span class="sxs-lookup"><span data-stu-id="e2e16-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="e2e16-179">R betiklerini çağırma</span><span class="sxs-lookup"><span data-stu-id="e2e16-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

