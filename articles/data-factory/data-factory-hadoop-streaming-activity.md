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
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a>Hadoop akış etkinliği Azure Data Factory kullanarak veri dönüştürme
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

Kullanabileceğiniz hello HDInsightStreamingActivity etkinliği Azure Data Factory işlem hattı Hadoop akış işten çağırma. Merhaba aşağıdaki JSON parçacığı hello HDInsightStreamingActivity bir ardışık düzen JSON dosyası kullanarak hello sözdizimi gösterilmektedir. 

Merhaba Hdınsight akış etkinliğinde Data Factory [ardışık düzen](data-factory-create-pipelines.md) üzerinde Hadoop akış programları yürütür [kendi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) veya [isteğe bağlı](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux tabanlı Hdınsight Küme. Bu makale üzerinde hello derlemeler [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) makalesi, veri dönüştürme ve desteklenen hello dönüştürme etkinliklerinin genel bir bakış sunar.

> [!NOTE] 
> Yeni tooAzure Data Factory varsa okuyun [giriş tooAzure Data Factory](data-factory-introduction.md) ve öğretici hello: [ilk veri hattınızı yapı](data-factory-build-your-first-pipeline.md) bu makaleyi okumadan önce. 

## <a name="json-sample"></a>JSON örneği
Merhaba Hdınsight kümesi örnek programlar (wc.exe ve cat.exe) ve veri (davinci.txt) ile otomatik olarak doldurulur. Varsayılan olarak, hello Hdınsight küme tarafından kullanılan hello kapsayıcının adını hello hello kümenin kendisi adıdır. Örneğin, küme adınızı myhdicluster ise, ilişkili hello blob kapsayıcısının adı myhdicluster olacaktır. 

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

Hello aşağıdaki noktaları göz önünde bulundurun:

1. Set hello **linkedServiceName** hello toohello adını bağlantılı mapreduce akış hangi hello iş çalıştırıldığında tooyour Hdınsight kümesi işaret hizmeti.
2. Merhaba etkinlik Hello türü çok ayarlamak**HDInsightStreaming**.
3. Hello için **Eşleyici** özelliği Eşleyici yürütülebilir hello adını belirtin. Merhaba örnekte cat.exe hello Eşleyici yürütülebilir ' dir.
4. Hello için **reducer** özelliği reducer yürütülebilir hello adını belirtin. Merhaba örnekte wc.exe hello reducer yürütülebilir ' dir.
5. Hello için **giriş** türü özelliği, hello Eşleştiricisi hello giriş dosyası (Merhaba konum dahil) belirtin. Merhaba örnekte: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample hello blob kapsayıcısı, veri/örnek/Gutenberg hello klasördür ve davinci.txt hello blob.
6. Hello için **çıkış** türü özelliği, hello reducer hello çıktı dosyası (Merhaba konum dahil) belirtin. Merhaba çıktısı hello Hadoop akış işi, bu özelliği için belirtilen toohello konumu yazılır.
7. Merhaba, **filePaths** bölümünde, hello Eşleyici ve reducer yürütülebilir dosyalar için hello yollarını belirtin. Merhaba örnekte: "adfsample/example/apps/wc.exe" adfsample hello blob kapsayıcısı, örnek/uygulamaları hello klasördür ve wc.exe hello çalıştırılabilir.
8. Hello için **fileLinkedService** özelliği, hello Azure temsil eden bağlı hizmet hello hello filePaths bölümünde belirtilen hello dosyaları içeren Azure depolama depolama belirtin.
9. Hello için **bağımsız değişkenleri** özelliği, iş akışı hello hello bağımsız değişkenleri belirtin.
10. Merhaba **Getdebugınfo** özelliği isteğe bağlı bir öğedir. TooFailure ayarlandığında hello günlükleri yalnızca hatada indirilir. TooAlways ayarlandığında, günlükleri hello yürütme durumu bağımsız olarak daima yüklenir.

> [!NOTE]
> Merhaba örnekte gösterildiği gibi bir çıktı veri kümesi hello Merhaba Hadoop akış etkinliği için belirttiğiniz **çıkarır** özelliği. Bu veri kümesi yalnızca gerekli toodrive hello ardışık düzen zamanlaması bir kukla dataset ' dir. Toospecify hiçbir girdi veri kümesi hello hello etkinliğinin gerekmez **girişleri** özelliği.  
> 
> 

## <a name="example"></a>Örnek
Bu kılavuzda Hello ardışık Azure Hdınsight kümesinde hello sözcük sayımı akış eşleme/azaltın programı çalıştırır. 

### <a name="linked-services"></a>Bağlı hizmetler
#### <a name="azure-storage-linked-service"></a>Azure Storage bağlı hizmeti
İlk olarak, bağlantılı hizmet toolink hello hello Azure Hdınsight küme toohello Azure veri fabrikası tarafından kullanılan Azure Storage oluşturun. Kopyala/yapıştır koddan Merhaba, hello adla tooreplace hesap adını ve hesap anahtarını ve Azure depolama anahtarını unutmayın. 

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
Ardından, Azure Hdınsight küme toohello Azure data factory'nizi bağlantılı hizmet toolink oluşturun. Kopyala/yapıştır koddan Merhaba, Hdınsight küme adı hello Hdınsight kümenizin adıyla değiştirin ve kullanıcı adı ve parola değerlerini değiştirin. 

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
Bu örnekte Hello ardışık tüm girişleri almaz. Merhaba Hdınsight akış etkinliği için bir çıkış veri kümesi belirtin. Bu veri kümesi yalnızca gerekli toodrive hello ardışık düzen zamanlaması bir kukla dataset ' dir. 

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

### <a name="pipeline"></a>İşlem hattı
Bu örnekte Hello ardışık türünde yalnızca bir etkinlik vardır: **HDInsightStreaming**. 

Merhaba Hdınsight kümesi örnek programlar (wc.exe ve cat.exe) ve veri (davinci.txt) ile otomatik olarak doldurulur. Varsayılan olarak, hello Hdınsight küme tarafından kullanılan hello kapsayıcının adını hello hello kümenin kendisi adıdır. Örneğin, küme adınızı myhdicluster ise, ilişkili hello blob kapsayıcısının adı myhdicluster olacaktır.  

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
## <a name="see-also"></a>Ayrıca Bkz.
* [Hive etkinliği](data-factory-hive-activity.md)
* [Pig etkinliği](data-factory-pig-activity.md)
* [MapReduce etkinliği](data-factory-map-reduce.md)
* [Spark programlarını çağırma](data-factory-spark.md)
* [R betiklerini çağırma](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

