---
title: "aaaInvoke Azure Data Factory MapReduce programı"
description: "Azure Hdınsight üzerinde çalışan MapReduce programlar tarafından tooprocess veri bir Azure veri fabrikası'ndan nasıl küme öğrenin."
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
ms.openlocfilehash: 448ef93a10bd97e7ecd4be4f04f88f8a05decc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="9e82a-103">Veri Fabrikası MapReduce programlardan çağırma</span><span class="sxs-lookup"><span data-stu-id="9e82a-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="9e82a-104">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="9e82a-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="9e82a-105">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="9e82a-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="9e82a-106">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="9e82a-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="9e82a-107">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="9e82a-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="9e82a-108">Spark etkinliği</span><span class="sxs-lookup"><span data-stu-id="9e82a-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="9e82a-109">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="9e82a-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="9e82a-110">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="9e82a-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="9e82a-111">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="9e82a-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="9e82a-112">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="9e82a-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="9e82a-113">.NET özel etkinlik</span><span class="sxs-lookup"><span data-stu-id="9e82a-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="9e82a-114">Merhaba Hdınsight MapReduce etkinliği bir veri fabrikasında [ardışık düzen](data-factory-create-pipelines.md) üzerinde MapReduce programları yürütür [kendi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) veya [isteğe bağlı](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux tabanlı Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="9e82a-114">hello HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9e82a-115">Bu makale üzerinde hello derlemeler [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) makalesi, veri dönüştürme ve desteklenen hello dönüştürme etkinliklerinin genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="9e82a-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="9e82a-116">Yeni tooAzure Data Factory varsa okuyun [giriş tooAzure Data Factory](data-factory-introduction.md) ve öğretici hello: [ilk veri hattınızı yapı](data-factory-build-your-first-pipeline.md) bu makaleyi okumadan önce.</span><span class="sxs-lookup"><span data-stu-id="9e82a-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="9e82a-117">Giriş</span><span class="sxs-lookup"><span data-stu-id="9e82a-117">Introduction</span></span>
<span data-ttu-id="9e82a-118">Bir Azure data factory işlem hattı bağlantılı işlem hizmetlerini kullanarak bağlantılı depolama Hizmetleri'nde verilerini işler.</span><span class="sxs-lookup"><span data-stu-id="9e82a-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="9e82a-119">Burada her etkinlik özel işleme işlemi gerçekleştiren etkinlikler dizisini içerir.</span><span class="sxs-lookup"><span data-stu-id="9e82a-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="9e82a-120">Bu makalede, Hdınsight MapReduce etkinliği hello kullanmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="9e82a-120">This article describes using hello HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="9e82a-121">Bkz: [Pig](data-factory-pig-activity.md) ve [Hive](data-factory-hive-activity.md) Pig/Hive çalıştırma hakkında ayrıntılı bilgi için komut dosyaları Windows/Linux tabanlı Hdınsight üzerinde bir ardışık düzen tarafından Hdınsight Pig ve Hive etkinlikleri kullanarak küme.</span><span class="sxs-lookup"><span data-stu-id="9e82a-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="9e82a-122">Hdınsight MapReduce etkinliği için JSON</span><span class="sxs-lookup"><span data-stu-id="9e82a-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="9e82a-123">Merhaba hello Hdınsight etkinliği için JSON tanımı:</span><span class="sxs-lookup"><span data-stu-id="9e82a-123">In hello JSON definition for hello HDInsight Activity:</span></span> 

1. <span data-ttu-id="9e82a-124">Set hello **türü** Merhaba, **etkinlik** çok**Hdınsight**.</span><span class="sxs-lookup"><span data-stu-id="9e82a-124">Set hello **type** of hello **activity** too**HDInsight**.</span></span>
2. <span data-ttu-id="9e82a-125">Merhaba sınıfı için Hello adını belirtin **className** özelliği.</span><span class="sxs-lookup"><span data-stu-id="9e82a-125">Specify hello name of hello class for **className** property.</span></span>
3. <span data-ttu-id="9e82a-126">Merhaba dosya adı dahil olmak üzere hello yolu toohello JAR dosyasını belirtin **jarFilePath** özelliği.</span><span class="sxs-lookup"><span data-stu-id="9e82a-126">Specify hello path toohello JAR file including hello file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="9e82a-127">Toohello hello JAR dosyasını içerir Azure Blob Storage başvuruyor hello bağlantılı hizmeti belirtin **jarLinkedService** özelliği.</span><span class="sxs-lookup"><span data-stu-id="9e82a-127">Specify hello linked service that refers toohello Azure Blob Storage that contains hello JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="9e82a-128">Merhaba MapReduce program için herhangi bir bağımsız değişken hello belirtin **bağımsız değişkenleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="9e82a-128">Specify any arguments for hello MapReduce program in hello **arguments** section.</span></span> <span data-ttu-id="9e82a-129">Çalışma zamanında gördüğünüz birkaç ek bağımsız değişkenler (örneğin: mapreduce.job.tags) hello MapReduce çerçeveden.</span><span class="sxs-lookup"><span data-stu-id="9e82a-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="9e82a-130">toodifferentiate, hello MapReduce bağımsız değişkenleriyle seçeneği ve değer bağımsız değişken olarak hello aşağıdaki örnekte gösterildiği gibi kullanmayı düşünün (- s,--giriş,--çıkış vb. göre bunların değerleri hemen ardından Seçenekler belirtilmiştir).</span><span class="sxs-lookup"><span data-stu-id="9e82a-130">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix toodetermine hello similarity between 2 items",
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
                    "description": "Custom Map Reduce toogenerate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
<span data-ttu-id="9e82a-131">Merhaba Hdınsight MapReduce etkinliği toorun herhangi bir Hdınsight kümesi MapReduce jar dosyasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e82a-131">You can use hello HDInsight MapReduce Activity toorun any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="9e82a-132">Hello toorun Mahout JAR dosyasını aşağıdaki örnek JSON tanımını ardışık, Hdınsight etkinliği hello yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="9e82a-132">In hello following sample JSON definition of a pipeline, hello HDInsight Activity is configured toorun a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="9e82a-133">Github'da örnek</span><span class="sxs-lookup"><span data-stu-id="9e82a-133">Sample on GitHub</span></span>
<span data-ttu-id="9e82a-134">Merhaba Hdınsight MapReduce etkinliği kullanmak için bir örnek indirebilirsiniz gelen: [veri fabrikası örneği github'daki](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span><span class="sxs-lookup"><span data-stu-id="9e82a-134">You can download a sample for using hello HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-hello-word-count-program"></a><span data-ttu-id="9e82a-135">Merhaba sözcük sayımı programı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9e82a-135">Running hello Word Count program</span></span>
<span data-ttu-id="9e82a-136">Bu örnekte Hello ardışık hello sözcük sayımı harita/azaltın program Azure Hdınsight kümesinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="9e82a-136">hello pipeline in this example runs hello Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="9e82a-137">Bağlı hizmetler</span><span class="sxs-lookup"><span data-stu-id="9e82a-137">Linked Services</span></span>
<span data-ttu-id="9e82a-138">İlk olarak, bağlantılı hizmet toolink hello hello Azure Hdınsight küme toohello Azure veri fabrikası tarafından kullanılan Azure Storage oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e82a-138">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="9e82a-139">Kopyala/yapıştır koddan Merhaba, tooreplace unutmadığınızdan **hesap adı** ve **hesap anahtarı** hello adı ve Azure depolama alanınızı anahtarı.</span><span class="sxs-lookup"><span data-stu-id="9e82a-139">If you copy/paste hello following code, do not forget tooreplace **account name** and **account key** with hello name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="9e82a-140">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="9e82a-140">Azure Storage linked service</span></span>

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="9e82a-141">Azure Hdınsight bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="9e82a-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="9e82a-142">Ardından, Azure Hdınsight küme toohello Azure data factory'nizi bağlantılı hizmet toolink oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e82a-142">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="9e82a-143">Değiştir, kopyala/yapıştır koddan hello durumunda, **Hdınsight küme adı** Hdınsight kümesi ve değişiklik kullanıcı adı ve parola değerlerini hello adı.</span><span class="sxs-lookup"><span data-stu-id="9e82a-143">If you copy/paste hello following code, replace **HDInsight cluster name** with hello name of your HDInsight cluster, and change user name and password values.</span></span>   

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

### <a name="datasets"></a><span data-ttu-id="9e82a-144">Veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="9e82a-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="9e82a-145">Çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="9e82a-145">Output dataset</span></span>
<span data-ttu-id="9e82a-146">Bu örnekte Hello ardışık tüm girişleri almaz.</span><span class="sxs-lookup"><span data-stu-id="9e82a-146">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="9e82a-147">Merhaba Hdınsight MapReduce etkinliği için bir çıkış veri kümesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="9e82a-147">You specify an output dataset for hello HDInsight MapReduce Activity.</span></span> <span data-ttu-id="9e82a-148">Bu veri kümesi yalnızca gerekli toodrive hello ardışık düzen zamanlaması bir kukla dataset ' dir.</span><span class="sxs-lookup"><span data-stu-id="9e82a-148">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="9e82a-149">İşlem hattı</span><span class="sxs-lookup"><span data-stu-id="9e82a-149">Pipeline</span></span>
<span data-ttu-id="9e82a-150">Bu örnekte Hello ardışık türünde yalnızca bir etkinlik vardır: HDInsightMapReduce.</span><span class="sxs-lookup"><span data-stu-id="9e82a-150">hello pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="9e82a-151">Merhaba JSON içinde hello önemli özelliklerinden bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9e82a-151">Some of hello important properties in hello JSON are:</span></span> 

| <span data-ttu-id="9e82a-152">Özellik</span><span class="sxs-lookup"><span data-stu-id="9e82a-152">Property</span></span> | <span data-ttu-id="9e82a-153">Notlar</span><span class="sxs-lookup"><span data-stu-id="9e82a-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="9e82a-154">type</span><span class="sxs-lookup"><span data-stu-id="9e82a-154">type</span></span> |<span data-ttu-id="9e82a-155">Merhaba türü çok ayarlanmalıdır**HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="9e82a-155">hello type must be set too**HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="9e82a-156">className</span><span class="sxs-lookup"><span data-stu-id="9e82a-156">className</span></span> |<span data-ttu-id="9e82a-157">Merhaba sınıfı adıdır: **wordcount**</span><span class="sxs-lookup"><span data-stu-id="9e82a-157">Name of hello class is: **wordcount**</span></span> |
| <span data-ttu-id="9e82a-158">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="9e82a-158">jarFilePath</span></span> |<span data-ttu-id="9e82a-159">Merhaba sınıfı içeren yolu toohello jar dosyasını.</span><span class="sxs-lookup"><span data-stu-id="9e82a-159">Path toohello jar file containing hello class.</span></span> <span data-ttu-id="9e82a-160">Kopyala/yapıştır koddan Merhaba, toochange hello hello kümenin adını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9e82a-160">If you copy/paste hello following code, don't forget toochange hello name of hello cluster.</span></span> |
| <span data-ttu-id="9e82a-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="9e82a-161">jarLinkedService</span></span> |<span data-ttu-id="9e82a-162">Merhaba jar dosyasını içeren azure depolama bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="9e82a-162">Azure Storage linked service that contains hello jar file.</span></span> <span data-ttu-id="9e82a-163">Bu bağlı hizmetin hello Hdınsight kümesi ile ilişkili toohello depolama başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="9e82a-163">This linked service refers toohello storage that is associated with hello HDInsight cluster.</span></span> |
| <span data-ttu-id="9e82a-164">Bağımsız değişkenler</span><span class="sxs-lookup"><span data-stu-id="9e82a-164">arguments</span></span> |<span data-ttu-id="9e82a-165">Merhaba wordcount program iki bağımsız değişken, bir giriş ve çıkış alır.</span><span class="sxs-lookup"><span data-stu-id="9e82a-165">hello wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="9e82a-166">Merhaba giriş dosyası hello davinci.txt dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="9e82a-166">hello input file is hello davinci.txt file.</span></span> |
| <span data-ttu-id="9e82a-167">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="9e82a-167">frequency/interval</span></span> |<span data-ttu-id="9e82a-168">Bu özelliklerin değerlerini Hello hello çıktı veri kümesi eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="9e82a-168">hello values for these properties match hello output dataset.</span></span> |
| <span data-ttu-id="9e82a-169">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="9e82a-169">linkedServiceName</span></span> |<span data-ttu-id="9e82a-170">daha önce oluşturmuştunuz toohello Hdınsight bağlı hizmeti anlamına gelmektedir.</span><span class="sxs-lookup"><span data-stu-id="9e82a-170">refers toohello HDInsight linked service you had created earlier.</span></span> |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun hello Word Count Program",
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

## <a name="run-spark-programs"></a><span data-ttu-id="9e82a-171">Spark programları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9e82a-171">Run Spark programs</span></span>
<span data-ttu-id="9e82a-172">MapReduce etkinliği toorun Spark programları Hdınsight Spark kümesinde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e82a-172">You can use MapReduce activity toorun Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="9e82a-173">Ayrıntılar için bkz. [Azure Data Factory’den Spark programlarını çağırma](data-factory-spark.md).</span><span class="sxs-lookup"><span data-stu-id="9e82a-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="9e82a-174">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9e82a-174">See Also</span></span>
* [<span data-ttu-id="9e82a-175">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="9e82a-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="9e82a-176">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="9e82a-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="9e82a-177">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="9e82a-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="9e82a-178">Spark programlarını çağırma</span><span class="sxs-lookup"><span data-stu-id="9e82a-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="9e82a-179">R betiklerini çağırma</span><span class="sxs-lookup"><span data-stu-id="9e82a-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

