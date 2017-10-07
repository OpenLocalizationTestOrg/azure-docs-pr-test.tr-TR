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
# <a name="invoke-mapreduce-programs-from-data-factory"></a>Veri Fabrikası MapReduce programlardan çağırma
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive etkinliği](data-factory-hive-activity.md) 
> * [Pig etkinliği](data-factory-pig-activity.md)
> * [MapReduce etkinliği](data-factory-map-reduce.md)
> * [Hadoop akış etkinliği](data-factory-hadoop-streaming-activity.md)
> * [Spark etkinliği](data-factory-spark.md)
> * [Machine Learning Batch Yürütme Etkinliği](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning Kaynak Güncelleştirme Etkinliği](data-factory-azure-ml-update-resource-activity.md)
> * [Saklı Yordam Etkinliği](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL Etkinliği](data-factory-usql-activity.md)
> * [.NET özel etkinlik](data-factory-use-custom-activities.md)

Merhaba Hdınsight MapReduce etkinliği bir veri fabrikasında [ardışık düzen](data-factory-create-pipelines.md) üzerinde MapReduce programları yürütür [kendi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) veya [isteğe bağlı](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux tabanlı Hdınsight kümesi. Bu makale üzerinde hello derlemeler [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) makalesi, veri dönüştürme ve desteklenen hello dönüştürme etkinliklerinin genel bir bakış sunar.

> [!NOTE] 
> Yeni tooAzure Data Factory varsa okuyun [giriş tooAzure Data Factory](data-factory-introduction.md) ve öğretici hello: [ilk veri hattınızı yapı](data-factory-build-your-first-pipeline.md) bu makaleyi okumadan önce.  

## <a name="introduction"></a>Giriş
Bir Azure data factory işlem hattı bağlantılı işlem hizmetlerini kullanarak bağlantılı depolama Hizmetleri'nde verilerini işler. Burada her etkinlik özel işleme işlemi gerçekleştiren etkinlikler dizisini içerir. Bu makalede, Hdınsight MapReduce etkinliği hello kullanmayı açıklar.

Bkz: [Pig](data-factory-pig-activity.md) ve [Hive](data-factory-hive-activity.md) Pig/Hive çalıştırma hakkında ayrıntılı bilgi için komut dosyaları Windows/Linux tabanlı Hdınsight üzerinde bir ardışık düzen tarafından Hdınsight Pig ve Hive etkinlikleri kullanarak küme. 

## <a name="json-for-hdinsight-mapreduce-activity"></a>Hdınsight MapReduce etkinliği için JSON
Merhaba hello Hdınsight etkinliği için JSON tanımı: 

1. Set hello **türü** Merhaba, **etkinlik** çok**Hdınsight**.
2. Merhaba sınıfı için Hello adını belirtin **className** özelliği.
3. Merhaba dosya adı dahil olmak üzere hello yolu toohello JAR dosyasını belirtin **jarFilePath** özelliği.
4. Toohello hello JAR dosyasını içerir Azure Blob Storage başvuruyor hello bağlantılı hizmeti belirtin **jarLinkedService** özelliği.   
5. Merhaba MapReduce program için herhangi bir bağımsız değişken hello belirtin **bağımsız değişkenleri** bölümü. Çalışma zamanında gördüğünüz birkaç ek bağımsız değişkenler (örneğin: mapreduce.job.tags) hello MapReduce çerçeveden. toodifferentiate, hello MapReduce bağımsız değişkenleriyle seçeneği ve değer bağımsız değişken olarak hello aşağıdaki örnekte gösterildiği gibi kullanmayı düşünün (- s,--giriş,--çıkış vb. göre bunların değerleri hemen ardından Seçenekler belirtilmiştir).

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
Merhaba Hdınsight MapReduce etkinliği toorun herhangi bir Hdınsight kümesi MapReduce jar dosyasını kullanabilirsiniz. Hello toorun Mahout JAR dosyasını aşağıdaki örnek JSON tanımını ardışık, Hdınsight etkinliği hello yapılandırılmış.

## <a name="sample-on-github"></a>Github'da örnek
Merhaba Hdınsight MapReduce etkinliği kullanmak için bir örnek indirebilirsiniz gelen: [veri fabrikası örneği github'daki](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).  

## <a name="running-hello-word-count-program"></a>Merhaba sözcük sayımı programı çalıştırma
Bu örnekte Hello ardışık hello sözcük sayımı harita/azaltın program Azure Hdınsight kümesinde çalışır.   

### <a name="linked-services"></a>Bağlı hizmetler
İlk olarak, bağlantılı hizmet toolink hello hello Azure Hdınsight küme toohello Azure veri fabrikası tarafından kullanılan Azure Storage oluşturun. Kopyala/yapıştır koddan Merhaba, tooreplace unutmadığınızdan **hesap adı** ve **hesap anahtarı** hello adı ve Azure depolama alanınızı anahtarı. 

#### <a name="azure-storage-linked-service"></a>Azure Storage bağlı hizmeti

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

#### <a name="azure-hdinsight-linked-service"></a>Azure Hdınsight bağlı hizmeti
Ardından, Azure Hdınsight küme toohello Azure data factory'nizi bağlantılı hizmet toolink oluşturun. Değiştir, kopyala/yapıştır koddan hello durumunda, **Hdınsight küme adı** Hdınsight kümesi ve değişiklik kullanıcı adı ve parola değerlerini hello adı.   

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

### <a name="datasets"></a>Veri kümeleri
#### <a name="output-dataset"></a>Çıktı veri kümesi
Bu örnekte Hello ardışık tüm girişleri almaz. Merhaba Hdınsight MapReduce etkinliği için bir çıkış veri kümesi belirtin. Bu veri kümesi yalnızca gerekli toodrive hello ardışık düzen zamanlaması bir kukla dataset ' dir.  

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

### <a name="pipeline"></a>İşlem hattı
Bu örnekte Hello ardışık türünde yalnızca bir etkinlik vardır: HDInsightMapReduce. Merhaba JSON içinde hello önemli özelliklerinden bazıları şunlardır: 

| Özellik | Notlar |
|:--- |:--- |
| type |Merhaba türü çok ayarlanmalıdır**HDInsightMapReduce**. |
| className |Merhaba sınıfı adıdır: **wordcount** |
| jarFilePath |Merhaba sınıfı içeren yolu toohello jar dosyasını. Kopyala/yapıştır koddan Merhaba, toochange hello hello kümenin adını unutmayın. |
| jarLinkedService |Merhaba jar dosyasını içeren azure depolama bağlı hizmeti. Bu bağlı hizmetin hello Hdınsight kümesi ile ilişkili toohello depolama başvuruyor. |
| Bağımsız değişkenler |Merhaba wordcount program iki bağımsız değişken, bir giriş ve çıkış alır. Merhaba giriş dosyası hello davinci.txt dosyasıdır. |
| frequency/interval |Bu özelliklerin değerlerini Hello hello çıktı veri kümesi eşleşmesi. |
| linkedServiceName |daha önce oluşturmuştunuz toohello Hdınsight bağlı hizmeti anlamına gelmektedir. |

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

## <a name="run-spark-programs"></a>Spark programları çalıştırma
MapReduce etkinliği toorun Spark programları Hdınsight Spark kümesinde kullanabilirsiniz. Ayrıntılar için bkz. [Azure Data Factory’den Spark programlarını çağırma](data-factory-spark.md).  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a>Ayrıca Bkz.
* [Hive etkinliği](data-factory-hive-activity.md)
* [Pig etkinliği](data-factory-pig-activity.md)
* [Hadoop akış etkinliği](data-factory-hadoop-streaming-activity.md)
* [Spark programlarını çağırma](data-factory-spark.md)
* [R betiklerini çağırma](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

