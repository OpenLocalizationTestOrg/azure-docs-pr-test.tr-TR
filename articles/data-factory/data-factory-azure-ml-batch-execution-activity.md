---
title: "Azure Data Factory kullanarak aaaCreate Tahmine dayalı veri ardışık | Microsoft Docs"
description: "Azure Data Factory ve Azure Machine Learning kullanarak Tahmine dayalı ardışık düzen toocreate oluşturma nasıl açıklar"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a>Azure Machine Learning ve Azure Data Factory kullanarak Tahmine dayalı ardışık düzen oluşturun

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

## <a name="introduction"></a>Giriş

### <a name="azure-machine-learning"></a>Azure Machine Learning
[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) , toobuild sınamak ve Tahmine dayalı analiz çözümlerini dağıtmak etkinleştirir. Bir üst düzey açısından bakıldığında, üç adımda gerçekleştirilir:

1. **Eğitim denemenizi oluşturma**. Bu adımı hello Azure ML Studio kullanarak yapın. Merhaba ML studio tootrain kullanın ve eğitim verileri kullanarak bir Tahmine dayalı bir analiz modeli test bir görsel işbirlikçi geliştirme ortamıdır.
2. **Tooa Tahmine dayalı denemeye Dönüştür**. Modelinizi var olan verilerle eğitilmiş ve hazır toouse olduğunuz sonra onu tooscore yeni verileri hazırlamak ve puanlama için denemenizi kolaylaştırmak.
3. **Web hizmeti olarak dağıtabilir**. Puanlama denemenizi bir Azure web hizmeti olarak yayımlayabilirsiniz. Bu web hizmeti uç noktası aracılığıyla veri tooyour modeli gönderebilir ve sonuç tahminleri hello model Excel'den alabilirsiniz.  

### <a name="azure-data-factory"></a>Azure Data Factory
Veri fabrikası, düzenleyen ve hello otomatikleştiren bir bulut tabanlı veri tümleştirme hizmetidir **taşıma** ve **dönüştürme** veri. Çeşitli veri depolarına verilerden alma, hello veri dönüştürme/işlemi ve yayımlama hello sonuç veri toohello veri depolarına Azure Data Factory kullanarak veri tümleştirme çözümleri oluşturabilirsiniz.

Data Factory Hizmeti'ne taşıyın ve veri dönüştürme toocreate veri ardışık sağlar ve belirtilen bir zamanlamayla (saatlik, günlük, haftalık, vb.) hello ardışık düzen çalıştırın. Ayrıca zengin Görselleştirmelerini toodisplay hello çizgileri ve veri işlem hatlarınızı, arasındaki bağımlılıkları sağlar ve tüm veri işlem hatlarınızı tek bir birleşik görünüm tooeasily tam olarak belirlemenizde sorunlardan izlemek ve izleme uyarıları ayarlayın.

Bkz: [giriş tooAzure Data Factory](data-factory-introduction.md) ve [ilk işlem hattınızı oluşturma](data-factory-build-your-first-pipeline.md) makaleleri tooquickly hello Azure Data Factory hizmeti ile başlayın.

### <a name="data-factory-and-machine-learning-together"></a>Veri Fabrikası ve Machine Learning birlikte
Azure Data Factory etkinleştirir, tooeasily bir yayımlanan kullanmak ardışık düzen oluşturma [Azure Machine Learning] [ azure-machine-learning] web hizmeti Tahmine dayalı analiz için. Hello kullanarak **toplu iş yürütme etkinliği** bir Azure Data Factory işlem hattı bir Azure ML web hizmeti toomake tahminleri toplu hello veriler üzerinde çağırabilirsiniz. Bkz: [çağırma Azure ML toplu iş yürütme etkinliği hello web hizmetini kullanarak](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) ayrıntıları bölümü.

Zaman içinde yeni giriş veri kümeleri kullanarak retrained toobe hello Tahmine dayalı modelleri hello Azure ML Puanlama denemeleri gerekir. Aşağıdaki adımları hello yaparak Data Factory işlem hattı Azure ML modelden yeniden eğitme:

1. Merhaba eğitim denemenizi (değil Tahmine dayalı denemeye) bir web hizmeti olarak yayımlayın. Merhaba önceki senaryoda bir web hizmeti olarak tooexpose tahmini deneme yaptığınız gibi hello Azure ML Studio bu adımda yapın.
2. Hello Azure ML toplu iş yürütme etkinliği tooinvoke hello web hizmetini hello eğitim denemenizi için kullanın. Temel olarak, web hizmeti eğitim hem web hizmeti Puanlama hello Azure ML toplu iş yürütme etkinliği tooinvoke kullanabilirsiniz.

Yeniden eğitme ile tamamladıktan sonra web hizmeti (web hizmeti olarak sunulan Tahmine dayalı denemeye) hello kullanarak hello yeni eğitilen modeli Puanlama hello güncelleştirme **Azure ML güncelleştirme kaynak etkinliği**. Bkz: [kaynak güncelleştirme etkinliği kullanarak modelleri güncelleştirme](data-factory-azure-ml-update-resource-activity.md) Ayrıntılar için makale.

## <a name="invoking-a-web-service-using-batch-execution-activity"></a>Toplu iş yürütme etkinliği kullanarak bir web hizmeti çağırma
Azure Data Factory tooorchestrate veri hareketlerini ve işleme kullanın ve sonra da toplu iş yürütme Azure Machine Learning kullanarak gerçekleştirin. Merhaba en üst düzey adımlar şunlardır:

1. Bir Azure Machine Learning bağlantılı hizmeti oluşturun. Değerleri aşağıdaki hello gerekir:

   1. **İstek URI'si** hello toplu iş yürütme API için. Merhaba tıklatarak hello istek URI'si bulabilirsiniz **toplu iş yürütme** hello web Hizmetleri sayfasında bağlantı.
   2. **API anahtarı** hello Azure Machine Learning web hizmeti yayımlanmış. Yayımladığınız hello web hizmeti tıklatarak hello API anahtarı bulabilirsiniz.
   3. Kullanım hello **AzureMLBatchExecution** etkinlik.

      ![Machine Learning Panosu](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![Toplu URI](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a>Senaryo: Web hizmeti girişleri/Azure Blob Depolama toodata başvuran çıkışları kullanarak denemelerini
Bu senaryoda, hello Azure Machine Learning Web hizmeti bir Azure blob depolama alanındaki bir dosyadan veri kullanarak tahminleri yapar ve hello tahmin sonuçlarını hello blob depolama alanında depolar. Merhaba aşağıdaki JSON Data Factory işlem hattı AzureMLBatchExecution etkinliği ile tanımlar. Merhaba etkinlik sahip hello dataset **DecisionTreeInputBlob** giriş olarak ve **DecisionTreeResultBlob** hello çıktı olarak. Merhaba **DecisionTreeInputBlob** hello kullanılarak geçirilen bir giriş toohello web hizmeti tarafından olarak **WebServiceInput etkinliğine** JSON özelliği. Merhaba **DecisionTreeResultBlob** hello kullanılarak geçirilen bir çıktı toohello Web hizmeti tarafından olarak **webServiceOutputs** JSON özelliği.  

> [!IMPORTANT]
> Merhaba web hizmeti birden fazla girdi aldığı durumlarda hello kullan **webServiceInputs** kullanmak yerine özelliği **WebServiceInput etkinliğine**. Merhaba bkz [Web hizmeti birden çok girişi gerektiren](#web-service-requires-multiple-inputs) hello webServiceInputs özelliğini kullanarak bir örnek için bölüm.
>
> Merhaba tarafından başvurulan veri kümeleri **WebServiceInput etkinliğine**/**webServiceInputs** ve **webServiceOutputs** özellikleri (içinde  **typeProperties**) de dahil hello etkinlik **girişleri** ve **çıkarır**.
>
> Azure ML denemenizde web hizmeti giriş ve çıkış bağlantı noktaları ve genel parametreleri özelleştirebileceğiniz varsayılan adları ("input1", "input2") sahip. webServiceInputs, webServiceOutputs ve globalParameters ayarları için kullandığınız hello adlarının hello denemeler hello adlarında tam olarak eşleşmelidir. Azure ML uç nokta tooverify beklenen hello eşleme için hello örnek isteği yükü hello toplu iş yürütme Yardım sayfasında görüntüleyebilirsiniz.
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> Yalnızca girişleri ve çıkışları hello AzureMLBatchExecution etkinlik parametreleri toohello Web hizmeti geçirilebilir. Örneğin, yukarıdaki JSON parçacığı hello DecisionTreeInputBlob bir giriş toohello WebServiceInput etkinliğine parametresi ile bir giriş toohello Web hizmeti geçirilen AzureMLBatchExecution etkinlik ' dir.   
>
>

### <a name="example"></a>Örnek
Bu örnek kullanan Azure depolama toohold her ikisi de hello girdi ve çıktı verilerini.

Merhaba Git öneririz [Data Factory ile ilk işlem hattınızı oluşturma] [ adf-build-1st-pipeline] Bu örnek geçmeden önce Öğreticisi. Bu örnekte Hello Data Factory Düzenleyici toocreate Data Factory yapıtlarının (bağlı hizmetler, veri kümelerini, ardışık düzen) kullanın.   

1. Oluşturma bir **bağlantılı hizmeti** için **Azure Storage**. Merhaba girdi ve çıktı dosyası farklı depolama hesapları yoksa, iki bağlı hizmet gerekir. Bir JSON örneği aşağıdadır:

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. Merhaba oluşturma **giriş** Azure Data Factory **dataset**. Bazı diğer Data Factory veri kümeleri farklı olarak, bu veri kümeleri her ikisini de içermelidir **folderPath** ve **fileName** değerleri. Her toplu iş yürütme (her veri dilimi) tooprocess bölümleme toocause kullanın veya benzersiz giriş ve çıkış dosyaları. Bazı Yukarı Akış etkinliği tootransform hello hello CSV dosya biçiminde giriş ve her dilim için hello depolama hesabındaki yerleştirin tooinclude gerekebilir. Bu durumda, hello içermeyen **dış** ve **externalData** örnek ve, DecisionTreeInputBlob hello çıkış veri kümesi farklı bir etkinliğe olacaktır aşağıdaki hello gösterilen ayarları.

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
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

    Giriş csv dosyanızda hello sütun başlık satırı olmalıdır. Merhaba kullanıyorsanız **kopyalama etkinliği** toocreate/taşıma hello csv hello blob depolama alanına hello havuz özelliği ayarlanmış olmalıdır **blobWriterAddHeader** çok**doğru**. Örneğin:

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    Merhaba csv dosyası hello başlık satırı yoksa, aşağıdaki hata hello görebilirsiniz: **etkinliğinde hata: dize okunurken hata oluştu. Beklenmeyen bir belirteç: StartObject. Yol '', satır 1, 1, konum**.
3. Merhaba oluşturma **çıkış** Azure Data Factory **dataset**. Bu örnek için her bir dilim yürütme bölümleme toocreate benzersiz çıkış yolu kullanır. Merhaba bölümleme olmadan hello etkinlik hello dosyanın üzerine.

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. Oluşturma bir **bağlantılı hizmeti** türü: **AzureMLLinkedService**, hello API anahtarı sağlayarak ve toplu yürütme URL'si model.

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. Son olarak, içeren bir ardışık düzen Yazar bir **AzureMLBatchExecution** etkinlik. Çalışma zamanında, ardışık düzen hello aşağıdaki adımları gerçekleştirir:

   1. Giriş kümeleriniz Hello hello giriş dosyasının konumunu alır.
   2. Hello Azure Machine Learning toplu iş yürütme API çağırır
   3. Kopya, çıkış veri kümesinde bulunan verilen toplu iş yürütme çıktı toohello blob hello.

      > [!NOTE]
      > AzureMLBatchExecution etkinlik sıfır veya daha fazla girişleri ve çıkışları bir veya daha fazla olabilir.
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      Her ikisi de **Başlat** ve **son** tarih/saat olmalıdır [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601). Örneğin: 2014-10-14T16:32:41Z. Merhaba **son** zaman isteğe bağlı. Hello için değer belirtmezseniz, **son** özelliği olarak hesaplanır "**start + 48 hours.**" toorun hello ardışık kalıcı olarak belirtmek **9999-09-09** hello hello değeri olarak **son** özelliği. JSON özellikleri hakkında ayrıntılı bilgi için bkz. [JSON Betik Oluşturma Başvurusu](https://msdn.microsoft.com/library/dn835050.aspx).

      > [!NOTE]
      > Merhaba AzureMLBatchExecution etkinlik için giriş belirten isteğe bağlıdır.
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a>Senaryo: Okuyucu/Yazıcı modülleri toorefer toodata içinde çeşitli depolarını kullanarak denemelerini
Azure ML denemeler oluştururken, başka bir ortak toouse okuyucu ve yazıcı modülleri senaryodur. Merhaba okuyucu modülü bir denemeyi kullanılan tooload verilerini ve hello yazıcı modülü denemelerinizi toosave verileri. Okuyucu ve yazıcı modüller hakkında daha fazla ayrıntı için bkz: [okuyucu](https://msdn.microsoft.com/library/azure/dn905997.aspx) ve [yazan](https://msdn.microsoft.com/library/azure/dn905984.aspx) MSDN Kitaplığı konularda.     

Merhaba okuyucu ve yazıcı modülleri kullanırken, iyi bir uygulama toouse bu Okuyucu/Yazıcı modüllerin her bir özellik için bir Web hizmeti parametresi var. Bu web parametreleri çalışma zamanı sırasında tooconfigure hello değerlerini etkinleştirin. Örneğin, bir Azure SQL veritabanı kullanan bir okuyucu modülü ile bir deneme oluşturabilirsiniz: XXX.database.windows.net. Merhaba web hizmeti dağıtıldıktan sonra YYY.database.windows.net adlı başka bir Azure SQL Server hello web hizmeti toospecify tooenable hello tüketicileri istiyor. Bu değer toobe yapılandırılmış bir Web hizmeti parametresi tooallow kullanabilirsiniz.

> [!NOTE]
> Web hizmeti giriş ve çıkış Web hizmeti parametrelerinden farklıdır. Merhaba ilk senaryoda, bir giriş ve çıkış için bir Azure ML Web hizmeti nasıl belirtilebilir gördünüz. Bu senaryoda, Okuyucu/Yazıcı modüllerin tooproperties karşılık gelen bir Web hizmeti parametreleri geçirin.
>
>

Web hizmeti parametreleri kullanarak bir senaryo bakalım. Azure Machine Learning tarafından desteklenen hello veri kaynakları birinden bir okuyucu modülü tooread veri kullanan bir dağıtılan Azure Machine Learning web hizmetine sahip (örneğin: Azure SQL veritabanı). Merhaba toplu yürütme işlemi yapıldıktan sonra hello sonuçları yazıcı Modülü (Azure SQL veritabanı) kullanılarak yazılır.  Hiçbir web hizmeti girişleri ve çıkışları hello denemeler tanımlanır. Bu durumda, ilgili web hizmeti parametreleri hello okuyucu ve yazıcı modüller yapılandırmanızı öneririz. Bu yapılandırma hello Okuyucu/Yazıcı hello AzureMLBatchExecution etkinlik kullanılırken modülleri toobe sağlar. Web hizmeti parametreleri hello belirttiğiniz **globalParameters** hello etkinlik JSON gibi bölüm.

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

Aynı zamanda [veri fabrikası işlevleri](data-factory-functions-variables.md) hello değerlerini hello aşağıdaki örnekte gösterildiği gibi Web hizmeti parametreleri geçirme içinde:

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> Merhaba Web hizmeti parametreleri büyük/küçük harfe duyarlıdır, bu nedenle hello etkinliğinde belirttiğiniz hello adlarıyla JSON eşleşmesini hello hello Web hizmeti tarafından sunulan olanları olun.
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a>Azure Blob içinde birden çok dosyadan bir okuyucu modülü tooread veri kullanma
Pig gibi etkinlikleri ile büyük veri ardışık düzenleri ve Hive bir oluşturabilir veya hiçbir uzantı ile daha fazla çıkış dosyaları. Dış bir Hive tablosu belirttiğinizde, örneğin, hello veri hello dış Hive tablosu için adı 000000_0 aşağıdaki hello ile Azure blob depolama alanında depolanabilir. Birden çok dosya hello okuyucu modülünde deneme tooread kullanın ve bunları tahminleri için kullanın.

Merhaba okuyucu modülü bir Azure Machine Learning deneme kullanırken, Azure Blob girdi olarak belirtebilirsiniz. hello Azure blob depolama Hello dosyalarında hello çıktı dosyaları olabilir (örnek: 000000_0) Hdınsight üzerinde çalışan bir Pig ve Hive komut dosyası tarafından üretilen. Merhaba okuyucu Modülü (hiçbir uzantılı) tooread dosyaları hello yapılandırarak sağlar **yolu toocontainer, dizin/blob**. Merhaba **yolu toocontainer** noktaları toohello kapsayıcı ve **dizin/blob** hello görüntü aşağıdaki gösterildiği gibi hello dosyalarını içeren toofolder işaret eder. Merhaba diğer bir deyişle, yıldız işareti \*) **tüm hello kapsayıcı/klasöründeki dosyaları hello belirtir (diğer bir deyişle, aggregateddata/data/yıl ay/2014-6 = /\*)** hello deneme bir parçası olarak okuyun.

![Azure Blob özellikleri](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a>Örnek
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a>Web hizmeti parametreleri ile AzureMLBatchExecution aktivitesiyle kanalı

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
              "globalParameters": {
                "Database server name": "<myserver>.database.windows.net",
                "Database name": "<database>",
                "Server user account name": "<user name>",
                "Server user account password": "<password>"
              }              
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

Yukarıdaki JSON örnek Hello:

* Merhaba dağıtılan Azure Machine Learning hizmetinin kullandığı bir okuyucu ve yazıcı modülü tooread/yazma verilerden Web / tooan Azure SQL veritabanı. Bu Web hizmetini şu dört parametreler hello sunar: veritabanı sunucu adı, veritabanı adı, sunucu kullanıcı hesabı adı ve sunucu kullanıcı hesabı parolası.  
* Her ikisi de **Başlat** ve **son** tarih/saat olmalıdır [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601). Örneğin: 2014-10-14T16:32:41Z. Merhaba **son** zaman isteğe bağlı. Hello için değer belirtmezseniz, **son** özelliği olarak hesaplanır "**start + 48 hours.**" toorun hello ardışık kalıcı olarak belirtmek **9999-09-09** hello hello değeri olarak **son** özelliği. JSON özellikleri hakkında ayrıntılı bilgi için bkz. [JSON Betik Oluşturma Başvurusu](https://msdn.microsoft.com/library/dn835050.aspx).

### <a name="other-scenarios"></a>Diğer senaryolar
#### <a name="web-service-requires-multiple-inputs"></a>Web hizmeti birden çok giriş gerektiriyor
Merhaba web hizmeti birden fazla girdi aldığı durumlarda hello kullan **webServiceInputs** kullanmak yerine özelliği **WebServiceInput etkinliğine**. Merhaba tarafından başvurulan veri kümeleri **webServiceInputs** hello etkinliği de dahil edilmesi **girişleri**.

Azure ML denemenizde web hizmeti giriş ve çıkış bağlantı noktaları ve genel parametreleri özelleştirebileceğiniz varsayılan adları ("input1", "input2") sahip. webServiceInputs, webServiceOutputs ve globalParameters ayarları için kullandığınız hello adlarının hello denemeler hello adlarında tam olarak eşleşmelidir. Azure ML uç nokta tooverify beklenen hello eşleme için hello örnek isteği yükü hello toplu iş yürütme Yardım sayfasında görüntüleyebilirsiniz.

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a>Web hizmeti bir giriş gerektirmez
Azure ML toplu iş yürütme web Hizmetleri, örnek R veya Python komut dosyaları için değil gerektirebilecek tüm girişleri kullanılan toorun herhangi bir iş akışını olabilir. Ya da hello deneme herhangi GlobalParameters kullanıma sunmuyor okuyucu modülü ile yapılandırılabilir. Bu durumda, hello AzureMLBatchExecution etkinlik şu şekilde yapılandırılması:

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a>Web hizmeti bir giriş/çıkış gerektirmez
Hello Azure ML toplu iş yürütme web hizmeti yapılandırılmış herhangi bir Web hizmeti çıktı sahip olmayabilir. Bu örnekte, Web hizmeti girişi veya çıkışı yok veya tüm GlobalParameters yapılandırılır. Hala hello faaliyete kendisini yapılandırılmış bir çıktı yoktur, ancak bir webServiceOutput verilmedi.

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a>Web hizmeti kullanan okuyucular ve yazarlar ve diğer etkinlikler yalnızca başarılı olduğunda hello etkinlik çalışması
Okuyucu ve yazıcı Hello Azure ML web hizmeti modülleri yapılandırılmış toorun ile veya olmadan herhangi GlobalParameters olabilir. Ancak, yalnızca bir Yukarı Akış işlem tamamlandığında, veri kümesi bağımlılıkları tooinvoke hello hizmetinin kullandığı bir ardışık düzende tooembed hizmetini çağırır isteyebilirsiniz. Bu yaklaşımı kullanarak Hello toplu iş yürütme tamamlandıktan sonra başka bir eylemi de tetikleyebilirsiniz. Bu durumda, etkinlik girişleri ve çıkışları, bunlardan herhangi birinin Web hizmeti girişleri veya çıkışları adlandırma olmadan kullanarak hello bağımlılıkları hızlı.

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

Merhaba **paketler** şunlardır:

* Deneme uç noktanızı bir WebServiceInput etkinliğine kullanıyorsa: blob veri kümesi tarafından temsil edilen ve hello etkinlik girişlerinde ve hello WebServiceInput etkinliğine özelliği dahil edilmiştir. Aksi takdirde hello WebServiceInput etkinliğine özelliği atlanmıştır.
* Deneme uç noktanızı webServiceOutput(s) kullanıyorsa: blob veri kümeleri tarafından temsil edilen ve hello etkinlik çıkışları ve hello webServiceOutputs özelliğinde dahil edilir. Merhaba etkinlik çıkarır ve webServiceOutputs hello deneme her bir çıkış hello adıyla eşleştirilir. Aksi takdirde hello webServiceOutputs özelliği atlanmıştır.
* GlobalParameter(s), deneme uç noktasını kullanıma sunar, bunlar hello etkinlik globalParameters özelliğinde anahtar, değer çiftleri olarak verilir. Aksi takdirde hello globalParameters özelliği atlanmıştır. Merhaba anahtarlar büyük/küçük harfe duyarlıdır. [Azure Data Factory işlevleri](data-factory-functions-variables.md) hello değerleri kullanılabilir.
* Ek veri kümeleri hello etkinlik girişleri ve çıkışları Özellikleri'nde hello etkinlik typeProperties başvurulan olmadan eklenebilir. Bu veri kümeleri dilim bağımlılıkları kullanılarak yürütme yöneten ancak hello AzureMLBatchExecution etkinlik tarafından aksi halde yoksayılır.


## <a name="updating-models-using-update-resource-activity"></a>Kaynak güncelleştirme etkinliği kullanarak modelleri güncelleştiriliyor
Yeniden eğitme ile tamamladıktan sonra web hizmeti (web hizmeti olarak sunulan Tahmine dayalı denemeye) hello kullanarak hello yeni eğitilen modeli Puanlama hello güncelleştirme **Azure ML güncelleştirme kaynak etkinliği**. Bkz: [kaynak güncelleştirme etkinliği kullanarak modelleri güncelleştirme](data-factory-azure-ml-update-resource-activity.md) Ayrıntılar için makale.

### <a name="reader-and-writer-modules"></a>Okuyucu ve yazıcı modülleri
Web hizmeti parametreleri kullanarak için yaygın bir senaryo hello Azure SQL okuyucuları ve yazıcıları kullanılır. Merhaba okuyucu modülü, veri yönetimi hizmetlerinden Azure Machine Learning Studio dışında bir deneme içine kullanılan tooload verilerdir. Merhaba yazıcı modülü denemelerinizi veri Yönetim hizmetlerine Azure Machine Learning Studio dışında toosave verilerdir.  

Azure Blob/Azure SQL Okuyucu/Yazıcı hakkında daha fazla ayrıntı için bkz: [okuyucu](https://msdn.microsoft.com/library/azure/dn905997.aspx) ve [yazan](https://msdn.microsoft.com/library/azure/dn905984.aspx) MSDN Kitaplığı konularda. Merhaba önceki bölümdeki Hello örnek hello Azure Blob okuyucu ve Azure Blob yazıcı kullanılır. Bu bölümde, Azure SQL okuyucu ve Azure SQL yazıcı kullanarak anlatılmaktadır.

## <a name="frequently-asked-questions"></a>Sık sorulan sorular
**S:** my büyük veri ardışık düzen tarafından üretilen birden çok dosya vardır. Tüm hello dosyalarda hello AzureMLBatchExecution etkinlik toowork kullanabilir miyim?

**Y:** Evet. Merhaba bkz **bir okuyucu modülü tooread verileri Azure Blob içinde birden çok dosyadan kullanarak** ayrıntıları bölümü.

## <a name="azure-ml-batch-scoring-activity"></a>Azure ML toplu iş Puanlama etkinliği
Merhaba kullanıyorsanız **AzureMLBatchScoring** etkinlik toointegrate Azure Machine Learning ile öneririz hello son kullanma **AzureMLBatchExecution** etkinlik.

Merhaba AzureMLBatchExecution etkinlik hello Ağustos 2015 sürümünde Azure PowerShell ve Azure SDK'sını sunulmuştur.

Merhaba AzureMLBatchScoring etkinliğini kullanarak toocontinue istiyorsanız, bu bölümde okuma devam edin.  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a>Giriş/çıkış için Azure Storage kullanarak azure ML toplu Puanlama etkinliği

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a>Web hizmeti parametreleri
Web hizmeti parametreleri için değerleri toospecify ekleme bir **typeProperties** bölüm toohello **AzureMLBatchScoringActivty** hello ardışık düzen hello aşağıdaki örnekte gösterildiği gibi JSON bölümünde:

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
Aynı zamanda [veri fabrikası işlevleri](data-factory-functions-variables.md) hello değerlerini hello aşağıdaki örnekte gösterildiği gibi Web hizmeti parametreleri geçirme içinde:

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> Merhaba Web hizmeti parametreleri büyük/küçük harfe duyarlıdır, bu nedenle hello etkinliğinde belirttiğiniz hello adlarıyla JSON eşleşmesini hello hello Web hizmeti tarafından sunulan olanları olun.
>
>

## <a name="see-also"></a>Ayrıca Bkz.
* [Azure blog gönderisi: Azure Machine Learning ve Azure Data Factory ile çalışmaya başlama](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
