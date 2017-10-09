---
title: Azure Data Factory kullanarak aaaUpdate Machine Learning modellerini | Microsoft Docs
description: "Azure Data Factory ve Azure Machine Learning kullanarak Tahmine dayalı ardışık düzen toocreate oluşturma nasıl açıklar"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 6e5e4d2cfd245c7a9ed3bb9cdacca1f7f82b9620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a>Azure Machine Learning modellerini kaynak güncelleştirme etkinliği kullanarak güncelleştirme

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

Bu makalede hazırlandı hello ana Azure Data Factory - Azure Machine Learning tümleştirme makale: [Azure Machine Learning ve Azure Data Factory kullanarak Tahmine dayalı işlem hatlarını oluşturmak](data-factory-azure-ml-batch-execution-activity.md). Zaten yapmadıysanız, bu makalede okumadan önce hello ana makalesini gözden geçirin. 

## <a name="overview"></a>Genel Bakış
Zaman içinde yeni giriş veri kümeleri kullanarak retrained toobe hello Tahmine dayalı modelleri hello Azure ML Puanlama denemeleri gerekir. Yeniden eğitme ile tamamladıktan sonra web hizmeti ile Merhaba Puanlama tooupdate hello ML model retrained istiyor. Merhaba tooenable tipik adımları yeniden eğitme ve web Hizmetleri aracılığıyla güncelleştirme Azure ML modelleri şunlardır:

1. Bir deneme oluşturma [Azure ML Studio](https://studio.azureml.net).
2. Merhaba modeliyle memnun kaldığınızda, her iki hello Azure ML Studio toopublish web hizmetlerini kullanmak **eğitim denemenizi** ve puanlama /**Tahmine dayalı denemeye**.

Merhaba aşağıdaki tabloda bu örnekte kullanılan hello web hizmetleri açıklanmaktadır.  Bkz: [yeniden eğitme Machine Learning modellerini programlama aracılığıyla](../machine-learning/machine-learning-retrain-models-programmatically.md) Ayrıntılar için.

- **Web hizmeti eğitim** - eğitim verileri alır ve eğitilmiş modeller üretir. Merhaba yeniden eğitme hello çıktı, Azure Blob depolamada .ilearner dosyasıdır. Merhaba **endpoint varsayılan** hello eğitim yayımladığınızda, bir web hizmeti olarak denemeler için otomatik olarak oluşturulur. Daha fazla uç noktaları oluşturabilirsiniz, ancak yalnızca hello varsayılan uç nokta Merhaba örneği kullanır.
- **Web hizmeti Puanlama** - etiketlenmemiş veri örnekleri alır ve tahminleri yapar. Tahmin Hello çıktısını bir .csv dosyası veya hello deneme hello yapılandırmasına bağlı olarak bir Azure SQL veritabanında satır gibi çeşitli formlar olabilir. bir web hizmeti olarak hello Tahmine dayalı denemeye yayımladığınızda hello varsayılan uç sizin için otomatik olarak oluşturulur. 

Merhaba aşağıdaki resimde eğitim ve uç noktaları Azure ML Puanlama arasında hello ilişki gösterilmektedir.

![Web Hizmetleri](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

Merhaba çağırabileceği **web hizmeti eğitim** hello kullanarak **Azure ML toplu iş yürütme etkinliği**. Eğitim web hizmetini çağırmak için Puanlama verileri (web hizmeti Puanlama) bir Azure ML web Hizmeti'ni çağırmadan olarak aynıdır. Önceki bölümlerde kapak nasıl tooinvoke bir Azure Data Factory Azure ML web hizmetinden kanal ayrıntılı olarak hello. 

Merhaba çağırabileceği **web hizmeti Puanlama** hello kullanarak **Azure ML kaynak güncelleştirme etkinliği** tooupdate hello web hizmeti ile Merhaba yeni eğitilen model. Örnek hello bağlantılı hizmet tanımlarını sağlar: 

## <a name="scoring-web-service-is-a-classic-web-service"></a>Klasik web hizmeti olan Web hizmeti Puanlama
Web hizmeti Puanlama hello ise bir **Klasik web hizmeti**, hello ikinci oluşturma **varsayılan olmayan ve güncelleştirilebilir uç nokta** hello kullanarak [Azure portal](https://manage.windowsazure.com). Bkz [uç noktalar oluşturmak](../machine-learning/machine-learning-create-endpoint.md) adımları makalesinde bulabilirsiniz. Merhaba varsayılan olmayan güncelleştirilebilir endpoint oluşturduktan sonra aşağıdaki adımları hello:

* Tıklatın **toplu iş yürütme** tooget hello URI değeri Merhaba **mlEndpoint** JSON özelliği.
* Tıklatın **güncelleştirme kaynağı** bağlantı tooget hello URI değeri hello **updateResourceEndpoint** JSON özelliği. Merhaba API hello uç nokta sayfasının kendinde (Merhaba sağ alt köşedeki) anahtardır.

![güncelleştirilebilir uç noktası](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

Aşağıdaki örnek hello hello AzureML bağlantılı hizmeti için bir örnek JSON tanım sağlar. Merhaba bağlantılı hizmet hello apikey ile yapılan kimlik doğrulaması için kullanır.  

```json
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--scoring experiment--/jobs",
            "apiKey": "endpoint2Key",
            "updateResourceEndpoint": "https://management.azureml.net/workspaces/xxx/webservices/--scoring experiment--/endpoints/endpoint2"
        }
    }
}
```

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a>Web hizmeti Puanlama Azure Resource Manager web hizmetidir 
Merhaba web hizmeti hello yeni bir Azure Kaynak Yöneticisi uç noktasını kullanıma sunar web hizmeti türde ise, tooadd hello ikinci gerekmez **varsayılan olmayan** uç noktası. Merhaba **updateResourceEndpoint** hello bağlantılı hizmet hello biçimi şöyledir: 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

Değerleri hello URL'deki yer tutucu için hello hello web hizmeti sorgulanırken alabileceğiniz [Azure Machine Learning Web Hizmetleri portalı](https://services.azureml.net/). güncelleştirme kaynağı endpoint Hello yeni tür bir AAD (Azure Active Directory) belirteç gerekiyor. Belirtin **servicePrincipalId** ve **servicePrincipalKey**içinde AzureML bağlantılı hizmetinin. Bkz: [nasıl toocreate hizmet sorumlusu ve izinleri toomanage Azure kaynak atama](../azure-resource-manager/resource-group-create-service-principal-portal.md). Örnek AzureML bağlantılı hizmet tanımı aşağıda verilmiştir: 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "hello linked service for AML web service.",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/0000000000000000000000000000000000000/services/0000000000000000000000000000000000000/jobs?api-version=2.0",
            "apiKey": "xxxxxxxxxxxx",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRG/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "000000000-0000-0000-0000-0000000000000",
            "servicePrincipalKey": "xxxxx",
            "tenant": "mycompany.com"
        }
    }
}
```

Merhaba aşağıdaki senaryoyu daha fazla ayrıntı sağlar. Yeniden eğitme ve bir Azure Data Factory işlem hattı Azure ML modellerinden güncelleştirmek için bir örnek vardır.

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a>Senaryo: yeniden eğitme ve bir Azure ML model güncelleştiriliyor
Bu bölümde hello kullanan örnek bir işlem hattı **Azure ML toplu iş yürütme etkinliği** tooretrain bir model. Merhaba ardışık düzen de hello kullanır **Azure ML güncelleştirme kaynağı etkinlik** tooupdate hello web hizmeti Puanlama hello modelinde. bağlı hizmetler, veri kümelerini ve ardışık düzen hello örnekte tüm JSON parçacıklarını hello Hello bölüm de sağlar.

Merhaba diyagram görünümü hello örnek ardışık aşağıdadır. Gördüğünüz gibi hello Azure ML toplu iş yürütme etkinliği hello eğitim girdi alır ve eğitim çıktı (iLearner dosyası) oluşturur. Bu eğitim Çıktı Hello Azure ML kaynak güncelleştirme etkinliği alır ve web hizmeti uç noktası Puanlama hello modelinde güncelleştirmeleri hello. Merhaba kaynak güncelleştirme etkinliği herhangi bir çıktı üretmez. Merhaba placeholderBlob hello Azure Data Factory hizmeti toorun hello ardışık düzen tarafından gerekli olan yalnızca bir kukla çıktı veri kümesi ' dir.

![ardışık düzeni diyagramı](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a>Azure Blob storage bağlı hizmeti:
Hello Azure Storage veri aşağıdaki hello tutar:

* Eğitim verileri. Merhaba hello Azure ML eğitim web hizmeti için giriş verileri.  
* iLearner dosya. Merhaba Hello Azure ML eğitim web hizmetinden çıktı. Bu ayrıca hello giriş toohello güncelleştirme kaynağı etkinlik dosyasıdır.  

Merhaba örnek JSON hello bağlantılı hizmet tanımını şöyledir:

```JSON
{
    "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=name;AccountKey=key"
        }
    }
}
```

### <a name="training-input-dataset"></a>Eğitim girdi veri kümesi:
Merhaba aşağıdaki dataset hello giriş eğitim verilerini hello Azure ML eğitim web hizmeti temsil eder. Hello Azure ML toplu iş yürütme etkinliği bu veri kümesine bir girdi olarak alır.

```JSON
{
    "name": "trainingData",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "labeledexamples",
            "fileName": "labeledexamples.arff",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "policy": {          
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

### <a name="training-output-dataset"></a>Eğitim çıktı veri kümesi:
Merhaba aşağıdaki dataset hello çıktı iLearner dosya hello Azure ML eğitim web hizmetinden temsil eder. Hello Azure ML toplu iş yürütme etkinliği bu veri kümesini oluşturur. Bu veri kümesi de hello giriş toohello Azure ML güncelleştirme kaynağı etkinlik olabilir.

```JSON
{
    "name": "trainedModelBlob",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "trainingoutput",
            "fileName": "model.ilearner",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        }
    }
}
```

### <a name="linked-service-for-azure-ml-training-endpoint"></a>Azure ML eğitim uç noktası için bağlı hizmet
JSON parçacığı aşağıdaki hello hello eğitim web hizmetinin toohello varsayılan uç noktaları bir Azure Machine Learning bağlantılı hizmeti tanımlar.

```JSON
{    
    "name": "trainingEndpoint",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--training experiment--/jobs",
              "apiKey": "myKey"
        }
      }
}
```

İçinde **Azure ML Studio**, tooget değerlerini aşağıdaki hello **mlEndpoint** ve **apikey ile yapılan**:

1. Tıklatın **WEB Hizmetleri** hello sol menüdeki.
2. Merhaba tıklatın **web hizmeti eğitim** hello listesinde web hizmetleri.
3. Sonraki çok Kopyala**API anahtarı** metin kutusu. Başlangıç anahtarı hello Pano'da hello veri fabrikası JSON düzenleyicisine yapıştırın.
4. Merhaba, **Azure ML studio**, tıklatın **toplu iş yürütme** bağlantı.
5. Kopya hello **istek URI'si** hello gelen **isteği** bölümünde ve hello veri fabrikası JSON düzenleyicisine yapıştırın.   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a>Bağlantılı hizmeti Azure ML güncelleştirilebilir Puanlama uç noktası için:
JSON parçacığı aşağıdaki hello toohello varsayılan olmayan web hizmeti Puanlama hello güncelleştirilebilir uç noktaları bir Azure Machine Learning bağlantılı hizmeti tanımlar.  

```JSON
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/00000000eb0abe4d6bbb1d7886062747d7/services/00000000026734a5889e02fbb1f65cefd/jobs?api-version=2.0",
            "apiKey": "sooooooooooh3WvG1hBfKS2BNNcfwSO7hhY6dY98noLfOdqQydYDIXyf2KoIaN3JpALu/AKtflHWMOCuicm/Q==",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "fe200044-c008-4008-a005-94000000731",
            "servicePrincipalKey": "zWa0000000000Tp6FjtZOspK/WMA2tQ08c8U+gZRBlw=",
            "tenant": "mycompany.com"
        }
    }
}
```

### <a name="placeholder-output-dataset"></a>Yer tutucu çıktı veri kümesi:
Hello Azure ML güncelleştirme kaynağı etkinlik herhangi bir çıktı üretmez. Ancak, Azure Data Factory işlem hattı bir çıkış veri kümesi toodrive hello zamanlamasını gerektirir. Bu nedenle, bir kukla/yer tutucu veri kümesi bu örnekte kullanırız.  

```JSON
{
    "name": "placeholderBlob",
    "properties": {
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "any",
            "format": {
                "type": "TextFormat"
            }
        }
    }
}
```

### <a name="pipeline"></a>İşlem hattı
Merhaba işlem hattına sahip iki etkinlik: **AzureMLBatchExecution** ve **AzureMLUpdateResource**. Hello Azure ML toplu iş yürütme etkinliği hello eğitim veri giriş olarak alır ve bir iLearner dosya bir çıktı olarak üretir. Merhaba etkinlik verileri eğitim hello girişle hello eğitim web hizmeti (web hizmeti olarak sunulan eğitim denemenizi) çağırır ve hello webservice hello ilearner dosya alır. Merhaba placeholderBlob hello Azure Data Factory hizmeti toorun hello ardışık düzen tarafından gerekli olan yalnızca bir kukla çıktı veri kümesi ' dir.

![ardışık düzeni diyagramı](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "Training Exp for ADF ML [trained model]",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "outputs": [
                    {
                        "name": "placeholderBlob"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00Z",
           "end": "2016-02-14T00:00:00Z"
    }
}
```
