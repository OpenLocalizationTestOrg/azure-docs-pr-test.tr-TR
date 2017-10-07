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
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="ad6d1-103">Öğretici: Azure Resource Manager şablonu kullanarak ilk Azure veri fabrikanızı derleme</span><span class="sxs-lookup"><span data-stu-id="ad6d1-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ad6d1-104">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ad6d1-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="ad6d1-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="ad6d1-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="ad6d1-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ad6d1-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="ad6d1-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad6d1-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="ad6d1-108">Resource Manager Şablonu</span><span class="sxs-lookup"><span data-stu-id="ad6d1-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="ad6d1-109">REST API</span><span class="sxs-lookup"><span data-stu-id="ad6d1-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="ad6d1-110">Bu makalede, ilk Azure data factory'nizi Azure Resource Manager şablonu toocreate kullanın.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-110">In this article, you use an Azure Resource Manager template toocreate your first Azure data factory.</span></span> <span data-ttu-id="ad6d1-111">diğer araçlar/SDK, kullanarak toodo hello öğretici seçin hello seçeneklerden birini hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="ad6d1-112">Bu öğreticide Hello ardışık bir etkinlik vardır: **Hdınsight Hive etkinliği**.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="ad6d1-113">Bu etkinlik dönüşümler veri tooproduce çıkış veri girişi bir Azure Hdınsight kümesinde bir hive betiği çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="ad6d1-114">Başlangıç ve bitiş zamanlarını hello arasında bir ay belirtilen sonra hello ardışık düzen zamanlanmış toorun ' dir.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="ad6d1-115">Bu öğreticide Hello veri ardışık giriş verisi tooproduce çıktı verilerini dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="ad6d1-116">Nasıl bir öğretici için Azure Data Factory kullanarak toocopy verileri görmek [Öğreticisi: Blob Storage tooSQL veritabanı ' veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="ad6d1-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="ad6d1-117">Bu öğreticide Hello ardışık türünde yalnızca bir etkinlik vardır: Hdınsighthive.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-117">hello pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="ad6d1-118">Bir işlem hattında birden fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="ad6d1-119">Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="ad6d1-120">Daha fazla bilgi için bkz. [Data Factory'de zamanlama ve yürütme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="ad6d1-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ad6d1-121">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ad6d1-121">Prerequisites</span></span>
* <span data-ttu-id="ad6d1-122">Okuyun [öğreticiye genel bakış](data-factory-build-your-first-pipeline.md) makale ve tam hello **önkoşul** adımları.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="ad6d1-123">' Ndaki yönergeleri izleyin [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) makale tooinstall en son sürümü Azure PowerShell, bilgisayarınızda.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="ad6d1-124">Bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md) toolearn Azure Resource Manager şablonları hakkında.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="ad6d1-125">Bu öğreticide</span><span class="sxs-lookup"><span data-stu-id="ad6d1-125">In this tutorial</span></span>
| <span data-ttu-id="ad6d1-126">Varlık</span><span class="sxs-lookup"><span data-stu-id="ad6d1-126">Entity</span></span> | <span data-ttu-id="ad6d1-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ad6d1-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ad6d1-128">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="ad6d1-128">Azure Storage linked service</span></span> |<span data-ttu-id="ad6d1-129">Azure depolama hesabı toohello veri fabrikanıza bağlar.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-129">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="ad6d1-130">Azure depolama hesabı bu örnekteki hello ardışık düzeni için girdi ve çıktı verilerini ayrı tutma hello hello.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-130">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> |
| <span data-ttu-id="ad6d1-131">İsteğe bağlı HDInsight bağlantılı hizmeti</span><span class="sxs-lookup"><span data-stu-id="ad6d1-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="ad6d1-132">Bir isteğe bağlı Hdınsight kümesi toohello data factory bağlar.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-132">Links an on-demand HDInsight cluster toohello data factory.</span></span> <span data-ttu-id="ad6d1-133">Merhaba küme sizin için tooprocess verileri otomatik olarak oluşturulur ve hello işlem tamamlandıktan sonra silinir.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-133">hello cluster is automatically created for you tooprocess data and is deleted after hello processing is done.</span></span> |
| <span data-ttu-id="ad6d1-134">Azure Blob giriş veri kümesi</span><span class="sxs-lookup"><span data-stu-id="ad6d1-134">Azure Blob input dataset</span></span> |<span data-ttu-id="ad6d1-135">Toohello Azure Storage bağlı hizmeti anlamına gelmektedir.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-135">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="ad6d1-136">Merhaba bağlantılı hizmet tooan Azure depolama hesabı anlamına gelir ve hello Azure Blob dataset hello girdi verilerini tutan hello depolama hello kapsayıcı, klasör ve dosya adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-136">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="ad6d1-137">Azure Blob çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="ad6d1-137">Azure Blob output dataset</span></span> |<span data-ttu-id="ad6d1-138">Toohello Azure Storage bağlı hizmeti anlamına gelmektedir.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-138">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="ad6d1-139">Merhaba bağlantılı hizmet tooan Azure depolama hesabı anlamına gelir ve hello Azure Blob dataset hello çıktı verilerini tutan hello depolama hello kapsayıcı, klasör ve dosya adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-139">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello output data.</span></span> |
| <span data-ttu-id="ad6d1-140">Veri işlem hattı</span><span class="sxs-lookup"><span data-stu-id="ad6d1-140">Data pipeline</span></span> |<span data-ttu-id="ad6d1-141">Merhaba ardışık düzen hello girdi veri kümesi kullanır ve hello çıktı veri kümesi oluşturur, Hdınsighthive türünde bir etkinlik vardır.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-141">hello pipeline has one activity of type HDInsightHive, which consumes hello input dataset and produces hello output dataset.</span></span> |

<span data-ttu-id="ad6d1-142">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="ad6d1-143">İşlem hattında bir veya daha fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="ad6d1-144">İki tür etkinlik mevcuttur: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) ve [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ad6d1-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="ad6d1-145">Bu öğreticide bir etkinlik (Hive etkinliği) ile işlem hattı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="ad6d1-146">Merhaba aşağıdaki bölümde hello tam Resource Manager şablonu, hızlı başlangıç Öğreticisi ve test hello şablonu aracılığıyla çalıştırabilmeniz için Data Factory varlıklarını tanımlamak için sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-146">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="ad6d1-147">Her bir veri fabrikası varlık tanımlanan toounderstand bkz [Data Factory varlıklarını hello şablonunda](#data-factory-entities-in-the-template) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-147">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="ad6d1-148">Data Factory JSON şablonu</span><span class="sxs-lookup"><span data-stu-id="ad6d1-148">Data Factory JSON template</span></span>
<span data-ttu-id="ad6d1-149">Veri Fabrikası tanımlamak için hello en üst düzey Resource Manager şablonu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ad6d1-149">hello top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="ad6d1-150">Adlı bir JSON dosyası oluşturun **C:\adfgetstarted** içinde **C:\ADFGetStarted** içeriği aşağıdaki hello klasörüyle:</span><span class="sxs-lookup"><span data-stu-id="ad6d1-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

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
> <span data-ttu-id="ad6d1-151">Azure veri fabrikası oluşturmaya yönelik Resource Manager şablonunun başka bir örneği için bkz. [Öğretici: Azure Resource Manager şablonu kullanarak Kopyalama Etkinliği ile işlem hattı oluşturma](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="ad6d1-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="ad6d1-152">Parametreler JSON</span><span class="sxs-lookup"><span data-stu-id="ad6d1-152">Parameters JSON</span></span>
<span data-ttu-id="ad6d1-153">Adlı bir JSON dosyası oluşturun **ADFTutorialARM Parameters.json** hello Azure Resource Manager şablonu parametrelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="ad6d1-154">Azure depolama hesabınızın hello için anahtar ve Hello adı belirtin **storageAccountName** ve **storageAccountKey** Bu parametre dosyanın parametreleri.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-154">Specify hello name and key of your Azure Storage account for hello **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
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
> <span data-ttu-id="ad6d1-155">Ayrı parametre JSON geliştirme, test dosyalarınız ve aynı veri fabrikası JSON şablonu ile birlikte kullanabileceğiniz üretim ortamlarında hello.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="ad6d1-156">Bir Power Shell komut dosyası kullanarak, bu ortamlarda Data Factory varlıklarını dağıtmayı otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="ad6d1-157">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad6d1-157">Create data factory</span></span>
1. <span data-ttu-id="ad6d1-158">Başlat **Azure PowerShell** ve çalışma hello aşağıdaki komutu:</span><span class="sxs-lookup"><span data-stu-id="ad6d1-158">Start **Azure PowerShell** and run hello following command:</span></span> 
   * <span data-ttu-id="ad6d1-159">Merhaba aşağıdaki komutu çalıştırın ve hello kullanıcı adı ve parola toosign toohello Azure portal kullanın girin.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-159">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="ad6d1-160">Bu hesap için tüm hello abonelikleri komutu tooview aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-160">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="ad6d1-161">Çalışma hello aşağıdaki toowork ile istediğiniz tooselect hello abonelik komutu.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-161">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="ad6d1-162">Bu abonelik olması hello hello Azure portalında kullanılanla hello gibi aynı.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-162">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="ad6d1-163">1. adımda oluşturduğunuz hello Resource Manager şablonu kullanarak komut toodeploy Data Factory varlıklarını aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-163">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="ad6d1-164">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="ad6d1-164">Monitor pipeline</span></span>
1. <span data-ttu-id="ad6d1-165">İçinde toohello oturum sonra [Azure portal](https://portal.azure.com/), tıklatın **Gözat** seçip **veri fabrikaları**.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-165">After logging in toohello [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="ad6d1-166">![Gözat->Veri fabrikaları](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="ad6d1-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="ad6d1-167">Merhaba, **veri fabrikaları** dikey penceresinde hello veri fabrikası'i tıklatın (**TutorialFactoryARM**) oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-167">In hello **Data Factories** blade, click hello data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="ad6d1-168">Merhaba, **Data Factory** veri fabrikanızın dikey tıklayın **diyagramı**.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-168">In hello **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![Diyagram Kutucuğu](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="ad6d1-170">Merhaba, **diyagram görünümü**hello ardışık düzen özetini görmek ve kullanılan veri kümelerine Bu öğretici.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-170">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>
   
   ![Diyagram Görünümü](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="ad6d1-172">Merhaba dataset Hello diyagram görünümü, çift **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-172">In hello Diagram View, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="ad6d1-173">İşlenmekte olan bu hello dilim bakın.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-173">You see that hello slice that is currently being processed.</span></span>
   
    ![Veri kümesi](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="ad6d1-175">İşlem bittiğinde hello dilimi bkz **hazır** durumu.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-175">When processing is done, you see hello slice in **Ready** state.</span></span> <span data-ttu-id="ad6d1-176">İsteğe bağlı HDInsight kümesinin oluşturulması genellikle biraz zaman alır (yaklaşık 20 dakika).</span><span class="sxs-lookup"><span data-stu-id="ad6d1-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="ad6d1-177">Bu nedenle, hello ardışık düzen tootake beklediğiniz **yaklaşık olarak 30 dakika** tooprocess hello dilim.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-177">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
   
    ![Veri kümesi](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="ad6d1-179">Merhaba dilim olduğunda **hazır** durum, hello denetleyin **partitioneddata** hello klasöründe **adfgetstarted** hello için blob depolama alanınızın kapsayıcısında çıkış verileri.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-179">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

<span data-ttu-id="ad6d1-180">Bkz: [veri kümelerini ve ardışık düzen izleme](data-factory-monitor-manage-pipelines.md) nasıl toouse hello Azure portal dikey penceresi toomonitor hello ardışık düzen ve veri kümeleri, bu öğreticide oluşturduğunuz hakkında yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how toouse hello Azure portal blades toomonitor hello pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="ad6d1-181">Veri işlem hatlarınızı izleme ve yönetme uygulaması toomonitor de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-181">You can also use Monitor and Manage App toomonitor your data pipelines.</span></span> <span data-ttu-id="ad6d1-182">Bkz: [İzleyicisi ve izleme uygulaması kullanarak Azure Data Factory işlem hatlarını yönetmek](data-factory-monitor-manage-app.md) Merhaba uygulaması kullanma hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using hello application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ad6d1-183">Merhaba dilim başarıyla işlendiğinde hello girdi dosyası silinir.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-183">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="ad6d1-184">Bu nedenle, toorerun hello dilim istediğiniz veya öğreticiyi yeniden Merhaba, hello adfgetstarted kapsayıcısının hello girdi dosyasını (input.log) toohello inputdata klasörüne yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-184">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="ad6d1-185">Data Factory varlıklarını hello şablonunda</span><span class="sxs-lookup"><span data-stu-id="ad6d1-185">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="ad6d1-186">Veri fabrikası tanımlama</span><span class="sxs-lookup"><span data-stu-id="ad6d1-186">Define data factory</span></span>
<span data-ttu-id="ad6d1-187">Hello örnek aşağıdaki gösterildiği gibi bir veri fabrikası hello Resource Manager şablonunda tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="ad6d1-187">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="ad6d1-188">Merhaba dataFactoryName olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="ad6d1-188">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="ad6d1-189">Merhaba kaynak grup kimliğine göre benzersiz bir dize değil</span><span class="sxs-lookup"><span data-stu-id="ad6d1-189">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="ad6d1-190">Data Factory varlıklarını tanımlama</span><span class="sxs-lookup"><span data-stu-id="ad6d1-190">Defining Data Factory entities</span></span>
<span data-ttu-id="ad6d1-191">Merhaba aşağıdaki Data Factory varlıklarını hello JSON şablonunda tanımlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="ad6d1-191">hello following Data Factory entities are defined in hello JSON template:</span></span> 

* [<span data-ttu-id="ad6d1-192">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="ad6d1-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="ad6d1-193">İsteğe bağlı HDInsight bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="ad6d1-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="ad6d1-194">Azure Blob girdi veri kümesi</span><span class="sxs-lookup"><span data-stu-id="ad6d1-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="ad6d1-195">Azure Blob çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="ad6d1-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="ad6d1-196">Kopyalama etkinliği içeren bir veri işlem hattı</span><span class="sxs-lookup"><span data-stu-id="ad6d1-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="ad6d1-197">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="ad6d1-197">Azure Storage linked service</span></span>
<span data-ttu-id="ad6d1-198">Bu bölümde hello adı ve Azure depolama hesabınızın anahtarı belirtin.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-198">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="ad6d1-199">Bkz: [Azure depolama bağlantılı hizmeti](data-factory-azure-blob-connector.md#azure-storage-linked-service) JSON kullanılan özellikler toodefine hakkında ayrıntılı bilgi için bir Azure Storage bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

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
<span data-ttu-id="ad6d1-200">Merhaba **connectionString** hello storageAccountName ve storageAccountKey parametrelerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-200">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="ad6d1-201">bir yapılandırma dosyası kullanarak geçirilen bu parametrelerin değerlerini Hello.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-201">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="ad6d1-202">Merhaba tanımını değişkenleri de kullanır: azureStroageLinkedService ve dataFactoryName hello şablonda tanımlı.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-202">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="ad6d1-203">İsteğe bağlı HDInsight bağlantılı hizmeti</span><span class="sxs-lookup"><span data-stu-id="ad6d1-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="ad6d1-204">Bkz: [işlem bağlı Hizmetleri](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) bir Hdınsight isteğe bağlı hizmet makalesi JSON kullanılan özellikler toodefine hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="ad6d1-205">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="ad6d1-205">Note hello following points:</span></span> 

* <span data-ttu-id="ad6d1-206">Merhaba Data Factory oluşturur bir **Linux tabanlı** hello yukarıdaki JSON ile sizin için Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-206">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="ad6d1-207">Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="ad6d1-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="ad6d1-208">İsteğe bağlı HDInsight kümesi yerine **kendi HDInsight kümenizi** kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="ad6d1-209">Ayrıntılar için bkz. [HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span><span class="sxs-lookup"><span data-stu-id="ad6d1-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="ad6d1-210">Merhaba Hdınsight kümesi oluşturur bir **varsayılan kapsayıcı** hello JSON belirtilen hello blob depolamada (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="ad6d1-210">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="ad6d1-211">Hdınsight Hello küme silindiğinde bu kapsayıcıyı silmez.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-211">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="ad6d1-212">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-212">This behavior is by design.</span></span> <span data-ttu-id="ad6d1-213">Mevcut canlı bir küme olmadıkça işlenen toobe bir dilim gerekir her zaman isteğe bağlı Hdınsight bağlı hizmetiyle, Hdınsight kümesi oluşturulur (**timeToLive**) ve hello işlem bittiğinde silinir.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>
  
    <span data-ttu-id="ad6d1-214">Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="ad6d1-215">Bunları hello işlerin sorunları giderilmesi için ihtiyacınız yoksa, toodelete isteyebilirsiniz bunları tooreduce hello depolama maliyeti.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-215">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="ad6d1-216">Bu kapsayıcıların Hello adları izleyen bir desen: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="ad6d1-216">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="ad6d1-217">Gibi araçlar kullanın [Microsoft Storage Gezgini](http://storageexplorer.com/) toodelete kapsayıcılarında Azure blob depolama.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="ad6d1-218">Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="ad6d1-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="ad6d1-219">Azure blob girdi veri kümesi</span><span class="sxs-lookup"><span data-stu-id="ad6d1-219">Azure blob input dataset</span></span>
<span data-ttu-id="ad6d1-220">Blob kapsayıcı, klasör ve hello giriş verisi içeren dosya hello adlarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-220">You specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="ad6d1-221">Bkz: [Azure Blob veri kümesi özellikleri](data-factory-azure-blob-connector.md#dataset-properties) JSON kullanılan özellikler toodefine bir Azure Blob dataset hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

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
<span data-ttu-id="ad6d1-222">Şu parametreler parametre şablonda tanımlanan hello bu tanımını kullanır: blobContainer, inputBlobFolder ve inputBlobName.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-222">This definition uses hello following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="ad6d1-223">Azure Blob çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="ad6d1-223">Azure Blob output dataset</span></span>
<span data-ttu-id="ad6d1-224">Blob kapsayıcısı ve hello çıktı verilerini tutan klasör hello adlarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-224">You specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="ad6d1-225">Bkz: [Azure Blob veri kümesi özellikleri](data-factory-azure-blob-connector.md#dataset-properties) JSON kullanılan özellikler toodefine bir Azure Blob dataset hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="ad6d1-226">Şu parametreler hello parametre şablonda tanımlanan hello bu tanımını kullanır: blobContainer ve outputBlobFolder.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-226">This definition uses hello following parameters defined in hello parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="ad6d1-227">Veri işlem hattı</span><span class="sxs-lookup"><span data-stu-id="ad6d1-227">Data pipeline</span></span>
<span data-ttu-id="ad6d1-228">İsteğe bağlı bir Azure HDInsight kümesi üzerinde Hive komut dosyası çalıştırarak verileri dönüştüren bir işlem hattı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="ad6d1-229">Bkz: [ardışık düzen JSON](data-factory-create-pipelines.md#pipeline-json) JSON kullanılan öğeleri toodefine bu örnekteki işlem hattı açıklamaları için.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

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

## <a name="reuse-hello-template"></a><span data-ttu-id="ad6d1-230">Merhaba şablonu yeniden</span><span class="sxs-lookup"><span data-stu-id="ad6d1-230">Reuse hello template</span></span>
<span data-ttu-id="ad6d1-231">Merhaba öğreticide Data Factory varlıklarını ve parametreleri için değerleri geçirme için bir şablon tanımlamak için bir şablon oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-231">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="ad6d1-232">toouse Merhaba aynı şablon toodeploy Data Factory varlıkları toodifferent ortamları, her ortam için bir parametre dosyası oluşturabilir ve toothat ortam dağıtırken kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-232">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="ad6d1-233">Örnek:</span><span class="sxs-lookup"><span data-stu-id="ad6d1-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="ad6d1-234">Hello ilk komut hello geliştirme ortamı için parametre dosyası kullanır, ikinci bir hello için test ortamı ve hello üretim ortamı için üçüncü bir hello dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-234">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="ad6d1-235">Merhaba şablonu tooperform yeniden kullanabilir yinelenen görevler.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-235">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="ad6d1-236">Örneğin, birçok veri fabrikaları biriyle toocreate gerekir veya aynı mantığı ancak her veri fabrikası kullanır farklı Azure depolama ve Azure SQL veritabanı hesapları uygulamak daha fazla ardışık düzen hello.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-236">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="ad6d1-237">Bu senaryoda, kullandığınız hello aynı şablonu hello toocreate veri fabrikaları farklı parametre ile aynı ortamda (geliştirme, test veya üretim) dosyaları.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-237">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="ad6d1-238">Bir ağ geçidi oluşturmak için Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="ad6d1-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="ad6d1-239">Geri hello mantıksal bir ağ geçidi oluşturmak için bir örnek Resource Manager şablonu aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-239">Here is a sample Resource Manager template for creating a logical gateway in hello back.</span></span> <span data-ttu-id="ad6d1-240">Şirket içi bilgisayar ya da Azure Iaas sanal bir ağ geçidi yükleyin ve bir anahtar kullanarak Data Factory hizmeti ile Merhaba ağ geçidini kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-240">Install a gateway on your on-premises computer or Azure IaaS VM and register hello gateway with Data Factory service using a key.</span></span> <span data-ttu-id="ad6d1-241">Ayrıntılar için bkz. [Şirket içi ile bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="ad6d1-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

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
<span data-ttu-id="ad6d1-242">Bu şablon GatewayUsingArmDF adlı bir veri fabrikasını GatewayUsingARM adlı bir ağ geçidi ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="ad6d1-243">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-243">See Also</span></span>
| <span data-ttu-id="ad6d1-244">Konu</span><span class="sxs-lookup"><span data-stu-id="ad6d1-244">Topic</span></span> | <span data-ttu-id="ad6d1-245">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ad6d1-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="ad6d1-246">İşlem hatları</span><span class="sxs-lookup"><span data-stu-id="ad6d1-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="ad6d1-247">Bu makalede, işlem hatlarının ve etkinliklerin Azure Data Factory anlamanıza yardımcı olur ve nasıl toouse bunları tooconstruct uçtan uca veri odaklı iş akışlarının senaryo veya iş.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-247">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="ad6d1-248">Veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="ad6d1-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="ad6d1-249">Bu makale, Azure Data Factory’deki veri kümelerini anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="ad6d1-250">Zamanlama ve yürütme</span><span class="sxs-lookup"><span data-stu-id="ad6d1-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="ad6d1-251">Bu makalede Azure Data Factory uygulama modelinin hello zamanlama ve yürütme yönleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-251">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="ad6d1-252">İzleme Uygulaması kullanılarak işlem hatlarını izleme ve yönetme</span><span class="sxs-lookup"><span data-stu-id="ad6d1-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="ad6d1-253">Bu makalede nasıl toomonitor, yönetme ve hatalarını ayıklama işlem hatlarını izleme ve yönetim uygulaması hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ad6d1-253">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |

