---
title: "aaaBuild ilk data factory'nizi (Resource Manager şablonu) | Microsoft Docs"
description: "Bu öğreticide, bir Azure Resource Manager şablonu kullanarak örnek bir Azure Data Factory işlem hattı oluşturacaksınız."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: eb9e70b9-a13a-4a27-8256-2759496be470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fa08cd1ac3a0e5c5bf4bd4c6bd9dfa6dba9f4319
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a>Öğretici: Azure Resource Manager şablonu kullanarak ilk Azure veri fabrikanızı derleme
> [!div class="op_single_selector"]
> * [Genel bakış ve önkoşullar](data-factory-build-your-first-pipeline.md)
> * [Azure portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager Şablonu](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

Bu makalede, ilk Azure data factory'nizi Azure Resource Manager şablonu toocreate kullanın. diğer araçlar/SDK, kullanarak toodo hello öğretici seçin hello seçeneklerden birini hello aşağı açılan listeden.

Bu öğreticide Hello ardışık bir etkinlik vardır: **Hdınsight Hive etkinliği**. Bu etkinlik dönüşümler veri tooproduce çıkış veri girişi bir Azure Hdınsight kümesinde bir hive betiği çalıştırır. Başlangıç ve bitiş zamanlarını hello arasında bir ay belirtilen sonra hello ardışık düzen zamanlanmış toorun ' dir. 

> [!NOTE]
> Bu öğreticide Hello veri ardışık giriş verisi tooproduce çıktı verilerini dönüştürür. Nasıl bir öğretici için Azure Data Factory kullanarak toocopy verileri görmek [Öğreticisi: Blob Storage tooSQL veritabanı ' veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Bu öğreticide Hello ardışık türünde yalnızca bir etkinlik vardır: Hdınsighthive. Bir işlem hattında birden fazla etkinlik olabilir. Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir. Daha fazla bilgi için bkz. [Data Factory'de zamanlama ve yürütme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

## <a name="prerequisites"></a>Ön koşullar
* Okuyun [öğreticiye genel bakış](data-factory-build-your-first-pipeline.md) makale ve tam hello **önkoşul** adımları.
* ' Ndaki yönergeleri izleyin [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) makale tooinstall en son sürümü Azure PowerShell, bilgisayarınızda.
* Bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md) toolearn Azure Resource Manager şablonları hakkında. 

## <a name="in-this-tutorial"></a>Bu öğreticide
| Varlık | Açıklama |
| --- | --- |
| Azure Storage bağlı hizmeti |Azure depolama hesabı toohello veri fabrikanıza bağlar. Azure depolama hesabı bu örnekteki hello ardışık düzeni için girdi ve çıktı verilerini ayrı tutma hello hello. |
| İsteğe bağlı HDInsight bağlantılı hizmeti |Bir isteğe bağlı Hdınsight kümesi toohello data factory bağlar. Merhaba küme sizin için tooprocess verileri otomatik olarak oluşturulur ve hello işlem tamamlandıktan sonra silinir. |
| Azure Blob giriş veri kümesi |Toohello Azure Storage bağlı hizmeti anlamına gelmektedir. Merhaba bağlantılı hizmet tooan Azure depolama hesabı anlamına gelir ve hello Azure Blob dataset hello girdi verilerini tutan hello depolama hello kapsayıcı, klasör ve dosya adını belirtir. |
| Azure Blob çıktı veri kümesi |Toohello Azure Storage bağlı hizmeti anlamına gelmektedir. Merhaba bağlantılı hizmet tooan Azure depolama hesabı anlamına gelir ve hello Azure Blob dataset hello çıktı verilerini tutan hello depolama hello kapsayıcı, klasör ve dosya adını belirtir. |
| Veri işlem hattı |Merhaba ardışık düzen hello girdi veri kümesi kullanır ve hello çıktı veri kümesi oluşturur, Hdınsighthive türünde bir etkinlik vardır. |

Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir. İşlem hattında bir veya daha fazla etkinlik olabilir. İki tür etkinlik mevcuttur: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) ve [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md). Bu öğreticide bir etkinlik (Hive etkinliği) ile işlem hattı oluşturursunuz.

Merhaba aşağıdaki bölümde hello tam Resource Manager şablonu, hızlı başlangıç Öğreticisi ve test hello şablonu aracılığıyla çalıştırabilmeniz için Data Factory varlıklarını tanımlamak için sağlar. Her bir veri fabrikası varlık tanımlanan toounderstand bkz [Data Factory varlıklarını hello şablonunda](#data-factory-entities-in-the-template) bölümü.

## <a name="data-factory-json-template"></a>Data Factory JSON şablonu
Veri Fabrikası tanımlamak için hello en üst düzey Resource Manager şablonu şöyledir: 

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```
Adlı bir JSON dosyası oluşturun **C:\adfgetstarted** içinde **C:\ADFGetStarted** içeriği aşağıdaki hello klasörüyle:

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that has hello input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of hello input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that will hold hello transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that contains hello Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of hello hive query (HQL) file." } }
    },
    "variables": {
          "dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
          "azureStorageLinkedServiceName": "AzureStorageLinkedService",
          "hdInsightOnDemandLinkedServiceName": "HDInsightOnDemandLinkedService",
          "blobInputDatasetName": "AzureBlobInput",
          "blobOutputDatasetName": "AzureBlobOutput",
          "pipelineName": "HiveTransformPipeline"
    },
    "resources": [
      {
        "name": "[variables('dataFactoryName')]",
        "apiVersion": "2015-10-01",
        "type": "Microsoft.DataFactory/datafactories",
        "location": "West US",
        "resources": [
          {
            "type": "linkedservices",
            "name": "[variables('azureStorageLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureStorage",
                  "description": "Azure Storage linked service",
                  "typeProperties": {
                    "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
                  }
            }
          },
          {
            "type": "linkedservices",
            "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "HDInsightOnDemand",
                  "typeProperties": {
                    "version": "3.5",
                    "clusterSize": 1,
                    "timeToLive": "00:05:00",
                    "osType": "Linux",
                    "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
                  }
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobInputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "fileName": "[parameters('inputBlobName')]",
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  },
                  "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobOutputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  }
            }
          },
          {
            "type": "datapipelines",
            "name": "[variables('pipelineName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]",
                  "[variables('hdInsightOnDemandLinkedServiceName')]",
                  "[variables('blobInputDatasetName')]",
                  "[variables('blobOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "description": "Pipeline that transforms data using Hive script.",
                  "activities": [
                {
                      "type": "HDInsightHive",
                      "typeProperties": {
                        "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                        "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                        "defines": {
                              "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                              "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                        }
                      },
                      "inputs": [
                        {
                              "name": "[variables('blobInputDatasetName')]"
                        }
                      ],
                      "outputs": [
                        {
                              "name": "[variables('blobOutputDatasetName')]"
                        }
                      ],
                      "policy": {
                        "concurrency": 1,
                        "retry": 3
                      },
                      "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                      },
                      "name": "RunSampleHiveActivity",
                      "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
                }
                  ],
                  "start": "2017-07-01T00:00:00Z",
                  "end": "2017-07-02T00:00:00Z",
                  "isPaused": false
              }
          }
        ]
      }
    ]
}
```

> [!NOTE]
> Azure veri fabrikası oluşturmaya yönelik Resource Manager şablonunun başka bir örneği için bkz. [Öğretici: Azure Resource Manager şablonu kullanarak Kopyalama Etkinliği ile işlem hattı oluşturma](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).  
> 
> 

## <a name="parameters-json"></a>Parametreler JSON
Adlı bir JSON dosyası oluşturun **ADFTutorialARM Parameters.json** hello Azure Resource Manager şablonu parametrelerini içerir.  

> [!IMPORTANT]
> Azure depolama hesabınızın hello için anahtar ve Hello adı belirtin **storageAccountName** ve **storageAccountKey** Bu parametre dosyanın parametreleri. 
> 
> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "value": "<Name of your Azure Storage account>"
        },
        "storageAccountKey": {
            "value": "<Key of your Azure Storage account>"
        },
        "blobContainer": {
            "value": "adfgetstarted"
        },
        "inputBlobFolder": {
            "value": "inputdata"
        },
        "inputBlobName": {
            "value": "input.log"
        },
        "outputBlobFolder": {
            "value": "partitioneddata"
        },
        "hiveScriptFolder": {
              "value": "script"
        },
        "hiveScriptFile": {
              "value": "partitionweblogs.hql"
        }
    }
}
```

> [!IMPORTANT]
> Ayrı parametre JSON geliştirme, test dosyalarınız ve aynı veri fabrikası JSON şablonu ile birlikte kullanabileceğiniz üretim ortamlarında hello. Bir Power Shell komut dosyası kullanarak, bu ortamlarda Data Factory varlıklarını dağıtmayı otomatik hale getirebilirsiniz. 
> 
> 

## <a name="create-data-factory"></a>Veri fabrikası oluşturma
1. Başlat **Azure PowerShell** ve çalışma hello aşağıdaki komutu: 
   * Merhaba aşağıdaki komutu çalıştırın ve hello kullanıcı adı ve parola toosign toohello Azure portal kullanın girin.
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * Bu hesap için tüm hello abonelikleri komutu tooview aşağıdaki hello çalıştırın.
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * Çalışma hello aşağıdaki toowork ile istediğiniz tooselect hello abonelik komutu. Bu abonelik olması hello hello Azure portalında kullanılanla hello gibi aynı.
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. 1. adımda oluşturduğunuz hello Resource Manager şablonu kullanarak komut toodeploy Data Factory varlıklarını aşağıdaki hello çalıştırın. 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>İşlem hattını izleme
1. İçinde toohello oturum sonra [Azure portal](https://portal.azure.com/), tıklatın **Gözat** seçip **veri fabrikaları**.
     ![Gözat->Veri fabrikaları](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)
2. Merhaba, **veri fabrikaları** dikey penceresinde hello veri fabrikası'i tıklatın (**TutorialFactoryARM**) oluşturduğunuz.    
3. Merhaba, **Data Factory** veri fabrikanızın dikey tıklayın **diyagramı**.

     ![Diyagram Kutucuğu](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. Merhaba, **diyagram görünümü**hello ardışık düzen özetini görmek ve kullanılan veri kümelerine Bu öğretici.
   
   ![Diyagram Görünümü](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. Merhaba dataset Hello diyagram görünümü, çift **AzureBlobOutput**. İşlenmekte olan bu hello dilim bakın.
   
    ![Veri kümesi](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. İşlem bittiğinde hello dilimi bkz **hazır** durumu. İsteğe bağlı HDInsight kümesinin oluşturulması genellikle biraz zaman alır (yaklaşık 20 dakika). Bu nedenle, hello ardışık düzen tootake beklediğiniz **yaklaşık olarak 30 dakika** tooprocess hello dilim.
   
    ![Veri kümesi](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. Merhaba dilim olduğunda **hazır** durum, hello denetleyin **partitioneddata** hello klasöründe **adfgetstarted** hello için blob depolama alanınızın kapsayıcısında çıkış verileri.  

Bkz: [veri kümelerini ve ardışık düzen izleme](data-factory-monitor-manage-pipelines.md) nasıl toouse hello Azure portal dikey penceresi toomonitor hello ardışık düzen ve veri kümeleri, bu öğreticide oluşturduğunuz hakkında yönergeler için.

Veri işlem hatlarınızı izleme ve yönetme uygulaması toomonitor de kullanabilirsiniz. Bkz: [İzleyicisi ve izleme uygulaması kullanarak Azure Data Factory işlem hatlarını yönetmek](data-factory-monitor-manage-app.md) Merhaba uygulaması kullanma hakkında ayrıntılı bilgi için. 

> [!IMPORTANT]
> Merhaba dilim başarıyla işlendiğinde hello girdi dosyası silinir. Bu nedenle, toorerun hello dilim istediğiniz veya öğreticiyi yeniden Merhaba, hello adfgetstarted kapsayıcısının hello girdi dosyasını (input.log) toohello inputdata klasörüne yükleyin.
> 
> 

## <a name="data-factory-entities-in-hello-template"></a>Data Factory varlıklarını hello şablonunda
### <a name="define-data-factory"></a>Veri fabrikası tanımlama
Hello örnek aşağıdaki gösterildiği gibi bir veri fabrikası hello Resource Manager şablonunda tanımlayın:  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
Merhaba dataFactoryName olarak tanımlanır: 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
Merhaba kaynak grup kimliğine göre benzersiz bir dize değil  

### <a name="defining-data-factory-entities"></a>Data Factory varlıklarını tanımlama
Merhaba aşağıdaki Data Factory varlıklarını hello JSON şablonunda tanımlanmıştır: 

* [Azure Storage bağlı hizmeti](#azure-storage-linked-service)
* [İsteğe bağlı HDInsight bağlı hizmeti](#hdinsight-on-demand-linked-service)
* [Azure Blob girdi veri kümesi](#azure-blob-input-dataset)
* [Azure Blob çıktı veri kümesi](#azure-blob-output-dataset)
* [Kopyalama etkinliği içeren bir veri işlem hattı](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Azure Storage bağlı hizmeti
Bu bölümde hello adı ve Azure depolama hesabınızın anahtarı belirtin. Bkz: [Azure depolama bağlantılı hizmeti](data-factory-azure-blob-connector.md#azure-storage-linked-service) JSON kullanılan özellikler toodefine hakkında ayrıntılı bilgi için bir Azure Storage bağlı hizmeti. 

```json
{
    "type": "linkedservices",
    "name": "[variables('azureStorageLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureStorage",
        "description": "Azure Storage linked service",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
Merhaba **connectionString** hello storageAccountName ve storageAccountKey parametrelerini kullanır. bir yapılandırma dosyası kullanarak geçirilen bu parametrelerin değerlerini Hello. Merhaba tanımını değişkenleri de kullanır: azureStroageLinkedService ve dataFactoryName hello şablonda tanımlı. 

#### <a name="hdinsight-on-demand-linked-service"></a>İsteğe bağlı HDInsight bağlantılı hizmeti
Bkz: [işlem bağlı Hizmetleri](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) bir Hdınsight isteğe bağlı hizmet makalesi JSON kullanılan özellikler toodefine hakkında ayrıntılı bilgi için.  

```json
{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
        }
    }
}
```
Hello aşağıdaki noktaları göz önünde bulundurun: 

* Merhaba Data Factory oluşturur bir **Linux tabanlı** hello yukarıdaki JSON ile sizin için Hdınsight kümesi. Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). 
* İsteğe bağlı HDInsight kümesi yerine **kendi HDInsight kümenizi** kullanabilirsiniz. Ayrıntılar için bkz. [HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).
* Merhaba Hdınsight kümesi oluşturur bir **varsayılan kapsayıcı** hello JSON belirtilen hello blob depolamada (**linkedServiceName**). Hdınsight Hello küme silindiğinde bu kapsayıcıyı silmez. Bu davranış tasarım gereğidir. Mevcut canlı bir küme olmadıkça işlenen toobe bir dilim gerekir her zaman isteğe bağlı Hdınsight bağlı hizmetiyle, Hdınsight kümesi oluşturulur (**timeToLive**) ve hello işlem bittiğinde silinir.
  
    Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz. Bunları hello işlerin sorunları giderilmesi için ihtiyacınız yoksa, toodelete isteyebilirsiniz bunları tooreduce hello depolama maliyeti. Bu kapsayıcıların Hello adları izleyen bir desen: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Gibi araçlar kullanın [Microsoft Storage Gezgini](http://storageexplorer.com/) toodelete kapsayıcılarında Azure blob depolama.

Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).

#### <a name="azure-blob-input-dataset"></a>Azure blob girdi veri kümesi
Blob kapsayıcı, klasör ve hello giriş verisi içeren dosya hello adlarını belirtin. Bkz: [Azure Blob veri kümesi özellikleri](data-factory-azure-blob-connector.md#dataset-properties) JSON kullanılan özellikler toodefine bir Azure Blob dataset hakkında ayrıntılı bilgi için. 

```json
{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "[parameters('inputBlobName')]",
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true
    }
}
```
Şu parametreler parametre şablonda tanımlanan hello bu tanımını kullanır: blobContainer, inputBlobFolder ve inputBlobName. 

#### <a name="azure-blob-output-dataset"></a>Azure Blob çıktı veri kümesi
Blob kapsayıcısı ve hello çıktı verilerini tutan klasör hello adlarını belirtin. Bkz: [Azure Blob veri kümesi özellikleri](data-factory-azure-blob-connector.md#dataset-properties) JSON kullanılan özellikler toodefine bir Azure Blob dataset hakkında ayrıntılı bilgi için.  

```json
{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        }
    }
}
```

Şu parametreler hello parametre şablonda tanımlanan hello bu tanımını kullanır: blobContainer ve outputBlobFolder. 

#### <a name="data-pipeline"></a>Veri işlem hattı
İsteğe bağlı bir Azure HDInsight kümesi üzerinde Hive komut dosyası çalıştırarak verileri dönüştüren bir işlem hattı tanımlayın. Bkz: [ardışık düzen JSON](data-factory-create-pipelines.md#pipeline-json) JSON kullanılan öğeleri toodefine bu örnekteki işlem hattı açıklamaları için. 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]",
        "[variables('hdInsightOnDemandLinkedServiceName')]",
        "[variables('blobInputDatasetName')]",
        "[variables('blobOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "description": "Pipeline that transforms data using Hive script.",
        "activities": [
        {
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                "defines": {
                    "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                    "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                }
            },
            "inputs": [
            {
                "name": "[variables('blobInputDatasetName')]"
            }
            ],
            "outputs": [
            {
                "name": "[variables('blobOutputDatasetName')]"
            }
            ],
            "policy": {
                "concurrency": 1,
                "retry": 3
            },
            "scheduler": {
                "frequency": "Month",
                "interval": 1
            },
            "name": "RunSampleHiveActivity",
            "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
        }
        ],
        "start": "2017-07-01T00:00:00Z",
        "end": "2017-07-02T00:00:00Z",
        "isPaused": false
    }
}
```

## <a name="reuse-hello-template"></a>Merhaba şablonu yeniden
Merhaba öğreticide Data Factory varlıklarını ve parametreleri için değerleri geçirme için bir şablon tanımlamak için bir şablon oluşturdu. toouse Merhaba aynı şablon toodeploy Data Factory varlıkları toodifferent ortamları, her ortam için bir parametre dosyası oluşturabilir ve toothat ortam dağıtırken kullanabilirsiniz.     

Örnek:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
Hello ilk komut hello geliştirme ortamı için parametre dosyası kullanır, ikinci bir hello için test ortamı ve hello üretim ortamı için üçüncü bir hello dikkat edin.  

Merhaba şablonu tooperform yeniden kullanabilir yinelenen görevler. Örneğin, birçok veri fabrikaları biriyle toocreate gerekir veya aynı mantığı ancak her veri fabrikası kullanır farklı Azure depolama ve Azure SQL veritabanı hesapları uygulamak daha fazla ardışık düzen hello. Bu senaryoda, kullandığınız hello aynı şablonu hello toocreate veri fabrikaları farklı parametre ile aynı ortamda (geliştirme, test veya üretim) dosyaları. 

## <a name="resource-manager-template-for-creating-a-gateway"></a>Bir ağ geçidi oluşturmak için Resource Manager şablonu
Geri hello mantıksal bir ağ geçidi oluşturmak için bir örnek Resource Manager şablonu aşağıda verilmiştir. Şirket içi bilgisayar ya da Azure Iaas sanal bir ağ geçidi yükleyin ve bir anahtar kullanarak Data Factory hizmeti ile Merhaba ağ geçidini kaydedin. Ayrıntılar için bkz. [Şirket içi ile bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md).

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
    },
    "variables": {
        "dataFactoryName":  "GatewayUsingArmDF",
        "apiVersion": "2015-10-01",
        "singleQuote": "'"
    },
    "resources": [
        {
            "name": "[variables('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "eastus",
            "resources": [
                {
                    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', variables('dataFactoryName'))]" ],
                    "type": "gateways",
                    "apiVersion": "[variables('apiVersion')]",
                    "name": "GatewayUsingARM",
                    "properties": {
                        "description": "my gateway"
                    }
                }            
            ]
        }
    ]
}
```
Bu şablon GatewayUsingArmDF adlı bir veri fabrikasını GatewayUsingARM adlı bir ağ geçidi ile oluşturur. 

## <a name="see-also"></a>Ayrıca Bkz.
| Konu | Açıklama |
|:--- |:--- |
| [İşlem hatları](data-factory-create-pipelines.md) |Bu makalede, işlem hatlarının ve etkinliklerin Azure Data Factory anlamanıza yardımcı olur ve nasıl toouse bunları tooconstruct uçtan uca veri odaklı iş akışlarının senaryo veya iş. |
| [Veri kümeleri](data-factory-create-datasets.md) |Bu makale, Azure Data Factory’deki veri kümelerini anlamanıza yardımcı olur. |
| [Zamanlama ve yürütme](data-factory-scheduling-and-execution.md) |Bu makalede Azure Data Factory uygulama modelinin hello zamanlama ve yürütme yönleri açıklanmaktadır. |
| [İzleme Uygulaması kullanılarak işlem hatlarını izleme ve yönetme](data-factory-monitor-manage-app.md) |Bu makalede nasıl toomonitor, yönetme ve hatalarını ayıklama işlem hatlarını izleme ve yönetim uygulaması hello kullanarak. |

