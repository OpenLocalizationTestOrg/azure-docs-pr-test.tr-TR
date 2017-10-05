---
title: "İlk veri fabrikanızı derleme (Resource Manager şablonu) | Microsoft Belgeleri"
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
ms.openlocfilehash: c67169f296f2f13b9ee87180f126fb1dcf10fbea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="0d4cd-103">Öğretici: Azure Resource Manager şablonu kullanarak ilk Azure veri fabrikanızı derleme</span><span class="sxs-lookup"><span data-stu-id="0d4cd-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0d4cd-104">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="0d4cd-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="0d4cd-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="0d4cd-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="0d4cd-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0d4cd-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="0d4cd-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d4cd-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="0d4cd-108">Resource Manager Şablonu</span><span class="sxs-lookup"><span data-stu-id="0d4cd-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="0d4cd-109">REST API</span><span class="sxs-lookup"><span data-stu-id="0d4cd-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="0d4cd-110">Bu makalede Azure Resource Manager şablonu kullanarak ilk Azure veri fabrikanızı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-110">In this article, you use an Azure Resource Manager template to create your first Azure data factory.</span></span> <span data-ttu-id="0d4cd-111">Diğer araçları/SDK’ları kullanarak öğreticiyi uygulamak için açılır listedeki seçeneklerden birini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

<span data-ttu-id="0d4cd-112">Bu öğreticideki işlem hattı bir etkinlik içerir: **HDInsight Hive etkinliği**.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="0d4cd-113">Bu etkinlik, Azure HDInsight kümesi üzerinde çıkış verileri üretmek üzere giriş verilerini dönüştüren bir hive betiği çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="0d4cd-114">İşlem hattı, belirtilen başlangıç ve bitiş saatleri arasında ayda bir kez çalışacak şekilde zamanlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="0d4cd-115">Bu öğreticideki veri işlem hattı, çıkış verileri üretmek üzere giriş verilerini dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="0d4cd-116">Azure Data Factory kullanarak verileri kopyalama öğreticisi için bkz. [Öğretici: Blob Depolama’dan SQL Veritabanı’na veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="0d4cd-116">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="0d4cd-117">Bu öğreticideki işlem hattında yalnızca bir etkinlik türü vardır: HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-117">The pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="0d4cd-118">Bir işlem hattında birden fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="0d4cd-119">Bir etkinliğin çıkış veri kümesini diğer etkinliğin giriş veri kümesi olarak ayarlayarak iki etkinliği zincirleyebilir, yani bir etkinliğin diğerinden sonra çalıştırılmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-119">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="0d4cd-120">Daha fazla bilgi için bkz. [Data Factory'de zamanlama ve yürütme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="0d4cd-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0d4cd-121">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0d4cd-121">Prerequisites</span></span>
* <span data-ttu-id="0d4cd-122">[Öğreticiye Genel Bakış](data-factory-build-your-first-pipeline.md) makalesinin tamamını okuyun ve **ön koşul** adımlarını tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="0d4cd-123">Bilgisayarınıza Azure PowerShell’in en son sürümünü yüklemek için [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azure/overview) makalesindeki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-123">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="0d4cd-124">Azure Resource Manager şablonları hakkında bilgi için bkz. [Azure Resource Manager Şablonları Yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0d4cd-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="0d4cd-125">Bu öğreticide</span><span class="sxs-lookup"><span data-stu-id="0d4cd-125">In this tutorial</span></span>
| <span data-ttu-id="0d4cd-126">Varlık</span><span class="sxs-lookup"><span data-stu-id="0d4cd-126">Entity</span></span> | <span data-ttu-id="0d4cd-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0d4cd-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0d4cd-128">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="0d4cd-128">Azure Storage linked service</span></span> |<span data-ttu-id="0d4cd-129">Azure Storage hesabınızı veri fabrikasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-129">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="0d4cd-130">Azure Depolama hesabı, bu örnekteki işlem hattı için girdi ve çıktı verilerini tutar.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-130">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> |
| <span data-ttu-id="0d4cd-131">İsteğe bağlı HDInsight bağlantılı hizmeti</span><span class="sxs-lookup"><span data-stu-id="0d4cd-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="0d4cd-132">İsteğe bağlı bir HDInsight kümesini veri fabrikasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-132">Links an on-demand HDInsight cluster to the data factory.</span></span> <span data-ttu-id="0d4cd-133">Küme sizin için otomatik olarak oluşturulur ve işlem bittikten sonra silinir.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-133">The cluster is automatically created for you to process data and is deleted after the processing is done.</span></span> |
| <span data-ttu-id="0d4cd-134">Azure Blob giriş veri kümesi</span><span class="sxs-lookup"><span data-stu-id="0d4cd-134">Azure Blob input dataset</span></span> |<span data-ttu-id="0d4cd-135">Azure Storage bağlı hizmetini ifade eder.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-135">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="0d4cd-136">Bağlı hizmet bir Azure Storage hesabını belirtirken, Azure Blob veri kümesi girdi verilerini tutan depolama birimindeki kapsayıcı, klasör ve dosya adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-136">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="0d4cd-137">Azure Blob çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="0d4cd-137">Azure Blob output dataset</span></span> |<span data-ttu-id="0d4cd-138">Azure Storage bağlı hizmetini ifade eder.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-138">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="0d4cd-139">Bağlı hizmet bir Azure Storage hesabını belirtirken, Azure Blob veri kümesi çıktı verilerini tutan depolama birimindeki kapsayıcı, klasör ve dosya adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-139">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the output data.</span></span> |
| <span data-ttu-id="0d4cd-140">Veri işlem hattı</span><span class="sxs-lookup"><span data-stu-id="0d4cd-140">Data pipeline</span></span> |<span data-ttu-id="0d4cd-141">İşlem hattında girdi veri kümesini kullanan ve çıktı veri kümesini üreten HDInsightHive türünde bir etkinlik bulunur.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-141">The pipeline has one activity of type HDInsightHive, which consumes the input dataset and produces the output dataset.</span></span> |

<span data-ttu-id="0d4cd-142">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="0d4cd-143">İşlem hattında bir veya daha fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="0d4cd-144">İki tür etkinlik mevcuttur: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) ve [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="0d4cd-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="0d4cd-145">Bu öğreticide bir etkinlik (Hive etkinliği) ile işlem hattı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="0d4cd-146">Aşağıdaki bölümde, öğreticiyi hızlıca geçip şablonu test etmeniz için Data Factory varlıklarını tanımlamaya yönelik tam bir Resource Manager şablonu verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-146">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="0d4cd-147">Her bir Data Factory varlığının nasıl tanımlandığını anlamak için [Şablondaki Data Factory varlıkları](#data-factory-entities-in-the-template) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-147">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="0d4cd-148">Data Factory JSON şablonu</span><span class="sxs-lookup"><span data-stu-id="0d4cd-148">Data Factory JSON template</span></span>
<span data-ttu-id="0d4cd-149">Bir veri fabrikasını tanımlamaya yönelik en üst düzey Resource Manager şablonu şudur:</span><span class="sxs-lookup"><span data-stu-id="0d4cd-149">The top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="0d4cd-150">**C:\ADFGetStarted** klasöründe aşağıdaki içeriğe sahip **ADFTutorialARM.json** adlı bir JSON dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="0d4cd-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of the Azure storage account that contains the input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for the Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of the blob container in the Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that has the input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of the input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that will hold the transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that contains the Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of the hive query (HQL) file." } }
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
> <span data-ttu-id="0d4cd-151">Azure veri fabrikası oluşturmaya yönelik Resource Manager şablonunun başka bir örneği için bkz. [Öğretici: Azure Resource Manager şablonu kullanarak Kopyalama Etkinliği ile işlem hattı oluşturma](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="0d4cd-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="0d4cd-152">Parametreler JSON</span><span class="sxs-lookup"><span data-stu-id="0d4cd-152">Parameters JSON</span></span>
<span data-ttu-id="0d4cd-153">Azure Resource Manager şablonuna yönelik parametreleri içeren **ADFTutorialARM-Parameters.json** adlı bir JSON dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="0d4cd-154">Bu parametre dosyasında **storageAccountName** ve **storageAccountKey** parametreleri için Azure Storage hesabınızın adını ve anahtarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-154">Specify the name and key of your Azure Storage account for the **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
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
> <span data-ttu-id="0d4cd-155">Aynı Data Factory JSON şablonuyla birlikte kullanabileceğiniz geliştirme, test ve üretim ortamları için ayrı parametre JSON dosyalarına sahip olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template.</span></span> <span data-ttu-id="0d4cd-156">Bir Power Shell komut dosyası kullanarak, bu ortamlarda Data Factory varlıklarını dağıtmayı otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="0d4cd-157">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d4cd-157">Create data factory</span></span>
1. <span data-ttu-id="0d4cd-158">**Azure PowerShell**’i başlatın ve aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0d4cd-158">Start **Azure PowerShell** and run the following command:</span></span> 
   * <span data-ttu-id="0d4cd-159">Aşağıdaki komutu çalıştırın ve Azure portalda oturum açmak için kullandığınız kullanıcı adı ve parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-159">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="0d4cd-160">Bu hesapla ilgili tüm abonelikleri görmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-160">Run the following command to view all the subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="0d4cd-161">Çalışmak isteğiniz aboneliği seçmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-161">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="0d4cd-162">Bu abonelik Azure portalında kullanılanla aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-162">This subscription should be the same as the one you used in the Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="0d4cd-163">1 Adımda oluşturduğunuz Resource Manager şablonunu kullanarak Data Factory varlıklarını dağıtmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-163">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="0d4cd-164">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="0d4cd-164">Monitor pipeline</span></span>
1. <span data-ttu-id="0d4cd-165">[Azure Portal](https://portal.azure.com/)’da oturum açtıktan sonra **Gözat**’a tıklayın ve **Veri fabrikaları**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-165">After logging in to the [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="0d4cd-166">![Gözat->Veri fabrikaları](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="0d4cd-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="0d4cd-167">**Veri Fabrikaları** dikey penceresinde oluşturduğunuz veri fabrikasına (**TutorialFactoryARM**) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-167">In the **Data Factories** blade, click the data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="0d4cd-168">Veri fabrikanızın **Veri Fabrikası** dikey penceresinde **Diyagram**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-168">In the **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![Diyagram Kutucuğu](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="0d4cd-170">**Diyagram Görünümü**nde, işlem hatlarına ve bu öğreticide kullanılan veri kümelerine bir genel bakış görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-170">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>
   
   ![Diyagram Görünümü](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="0d4cd-172">Diyagram Görünümü’nde **AzureBlobOutput** veri kümesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-172">In the Diagram View, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="0d4cd-173">Dilimin işlenmekte olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-173">You see that the slice that is currently being processed.</span></span>
   
    ![Veri kümesi](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="0d4cd-175">İşlem tamamlandığında dilimi **Hazır** durumunda görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-175">When processing is done, you see the slice in **Ready** state.</span></span> <span data-ttu-id="0d4cd-176">İsteğe bağlı HDInsight kümesinin oluşturulması genellikle biraz zaman alır (yaklaşık 20 dakika).</span><span class="sxs-lookup"><span data-stu-id="0d4cd-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="0d4cd-177">Bu nedenle, işlem hattının dilimi işlemesi için **yaklaşık 30 dakika** bekleyin.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-177">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>
   
    ![Veri kümesi](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="0d4cd-179">Dilim **Hazır** durumunda olduğunda çıktı verileri için blob depolama alanınızın **adfgetstarted** kapsayıcısında **partitioneddata** klasörünü denetleyin.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-179">When the slice is in **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  

<span data-ttu-id="0d4cd-180">Bu öğreticide oluşturduğunuz işlem hattını ve veri kümelerini izlemek üzere Azure portalı dikey pencerelerinin kullanımına ilişkin yönergeler için bkz. [Veri kümelerini ve işlem hatlarını izleme](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="0d4cd-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal blades to monitor the pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="0d4cd-181">Veri işlem hatlarınızı izlemek için İzleme ve Yönetme Uygulaması’nı da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-181">You can also use Monitor and Manage App to monitor your data pipelines.</span></span> <span data-ttu-id="0d4cd-182">Uygulamanın kullanımına ilişkin ayrıntılar için bkz. [İzleme Uygulaması kullanarak Azure Data Factory işlem hatlarını izleme ve yönetme](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="0d4cd-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using the application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0d4cd-183">Dilim başarıyla işlendiğinde girdi dosyası silinir.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-183">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="0d4cd-184">Bu nedenle, dilimi yeniden çalıştırmak veya öğreticiyi yeniden uygulamak isterseniz girdi dosyasını (input.log) adfgetstarted kapsayıcısının inputdata klasörüne yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-184">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="0d4cd-185">Şablondaki Data Factory varlıkları</span><span class="sxs-lookup"><span data-stu-id="0d4cd-185">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="0d4cd-186">Veri fabrikası tanımlama</span><span class="sxs-lookup"><span data-stu-id="0d4cd-186">Define data factory</span></span>
<span data-ttu-id="0d4cd-187">Resource Manager şablonunda bir veri fabrikasını aşağıdaki örnekte gösterildiği gibi tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="0d4cd-187">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="0d4cd-188">dataFactoryName aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="0d4cd-188">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="0d4cd-189">Bu değer, kaynak grubu kimliğini temel alan benzersiz bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-189">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="0d4cd-190">Data Factory varlıklarını tanımlama</span><span class="sxs-lookup"><span data-stu-id="0d4cd-190">Defining Data Factory entities</span></span>
<span data-ttu-id="0d4cd-191">Aşağıdaki Data Factory varlıkları JSON şablonunda tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="0d4cd-191">The following Data Factory entities are defined in the JSON template:</span></span> 

* [<span data-ttu-id="0d4cd-192">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="0d4cd-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="0d4cd-193">İsteğe bağlı HDInsight bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="0d4cd-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="0d4cd-194">Azure Blob girdi veri kümesi</span><span class="sxs-lookup"><span data-stu-id="0d4cd-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="0d4cd-195">Azure Blob çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="0d4cd-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="0d4cd-196">Kopyalama etkinliği içeren bir veri işlem hattı</span><span class="sxs-lookup"><span data-stu-id="0d4cd-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="0d4cd-197">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="0d4cd-197">Azure Storage linked service</span></span>
<span data-ttu-id="0d4cd-198">Bu bölümde Azure depolama hesabınızın adını ve anahtarını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-198">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="0d4cd-199">Bir Azure Storage bağlı hizmetini tanımlamak için kullanılan JSON özelliklerine ilişkin ayrıntılar için bkz. [Azure Storage bağlı hizmeti](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="0d4cd-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

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
<span data-ttu-id="0d4cd-200">**ConnectionString**, storageAccountName ve storageAccountKey parametrelerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-200">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="0d4cd-201">Bu parametrelerin değerleri bir yapılandırma dosyası kullanılarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-201">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="0d4cd-202">Tanım ayrıca şu değişkenleri kullanır: şablonda tanımlanan azureStroageLinkedService ve dataFactoryName.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-202">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="0d4cd-203">İsteğe bağlı HDInsight bağlantılı hizmeti</span><span class="sxs-lookup"><span data-stu-id="0d4cd-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="0d4cd-204">İsteğe bağlı bir HDInsight bağlı hizmetini tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılar için [İşlem bağlı hizmetleri](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="0d4cd-205">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="0d4cd-205">Note the following points:</span></span> 

* <span data-ttu-id="0d4cd-206">Data Factory, sizin için yukarıdaki JSON ile **Linux tabanlı** bir HDInsight kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-206">The Data Factory creates a **Linux-based** HDInsight cluster for you with the above JSON.</span></span> <span data-ttu-id="0d4cd-207">Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="0d4cd-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="0d4cd-208">İsteğe bağlı HDInsight kümesi yerine **kendi HDInsight kümenizi** kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="0d4cd-209">Ayrıntılar için bkz. [HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span><span class="sxs-lookup"><span data-stu-id="0d4cd-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="0d4cd-210">HDInsight kümesi JSON’da belirttiğiniz blob depolamada (**linkedServiceName**) bir **varsayılan kapsayıcı** oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-210">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="0d4cd-211">HDInsight, küme silindiğinde bu kapsayıcıyı silmez.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-211">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="0d4cd-212">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-212">This behavior is by design.</span></span> <span data-ttu-id="0d4cd-213">İsteğe bağlı HDInsight bağlı hizmetiyle, HDInsight kümesi her oluşturulduğunda, burada mevcut canlı bir küme (**timeToLive**) olmadıkça bir dilim gerekir ve işlem bittiğinde silinir.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>
  
    <span data-ttu-id="0d4cd-214">Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="0d4cd-215">İşlerin sorunları giderilmesi için bunlara gerek yoksa, depolama maliyetini azaltmak için bunları silmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-215">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="0d4cd-216">Bu kapsayıcıların adları şu deseni izler: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="0d4cd-216">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="0d4cd-217">Azure blob depolamada kapsayıcı silmek için [Microsoft Storage Gezgini](http://storageexplorer.com/) gibi araçları kullanın.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

<span data-ttu-id="0d4cd-218">Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="0d4cd-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="0d4cd-219">Azure blob girdi veri kümesi</span><span class="sxs-lookup"><span data-stu-id="0d4cd-219">Azure blob input dataset</span></span>
<span data-ttu-id="0d4cd-220">Blob kapsayıcı, klasör ve girdi verilerini içeren dosyanın adını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-220">You specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="0d4cd-221">Bir Azure Blob veri kümesini tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılar için bkz. [Azure Blob veri kümesi özellikleri](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0d4cd-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

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
<span data-ttu-id="0d4cd-222">Bu tanım, parametre şablonunda tanımlanan şu parametreleri kullanır: blobContainer, inputBlobFolder ve inputBlobName.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-222">This definition uses the following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="0d4cd-223">Azure Blob çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="0d4cd-223">Azure Blob output dataset</span></span>
<span data-ttu-id="0d4cd-224">Blob kapsayıcının ve çıktı verilerini tutan klasörün adlarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-224">You specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="0d4cd-225">Bir Azure Blob veri kümesini tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılar için bkz. [Azure Blob veri kümesi özellikleri](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0d4cd-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="0d4cd-226">Bu tanım, parametre şablonunda tanımlanan şu parametreleri kullanır: blobContainer ve outputBlobFolder.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-226">This definition uses the following parameters defined in the parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="0d4cd-227">Veri işlem hattı</span><span class="sxs-lookup"><span data-stu-id="0d4cd-227">Data pipeline</span></span>
<span data-ttu-id="0d4cd-228">İsteğe bağlı bir Azure HDInsight kümesi üzerinde Hive komut dosyası çalıştırarak verileri dönüştüren bir işlem hattı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="0d4cd-229">Bu örnekte bir işlem hattı tanımlamak için kullanılan JSON öğelerinin açıklamaları için bkz. [İşlem Hattı JSON](data-factory-create-pipelines.md#pipeline-json).</span><span class="sxs-lookup"><span data-stu-id="0d4cd-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

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

## <a name="reuse-the-template"></a><span data-ttu-id="0d4cd-230">Şablonu yeniden kullanma</span><span class="sxs-lookup"><span data-stu-id="0d4cd-230">Reuse the template</span></span>
<span data-ttu-id="0d4cd-231">Bu öğreticide, Data Factory varlıkları tanımlamaya yönelik bir şablon ve parametrelerin değerlerini geçirmeye yönelik bir şablon oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-231">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="0d4cd-232">Data Factory varlıklarını farklı ortamlara dağıtmak üzere aynı şablonu kullanmak için, her bir ortama yönelik bir parametre dosyası oluşturur ve bu ortama dağıtırken kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-232">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="0d4cd-233">Örnek:</span><span class="sxs-lookup"><span data-stu-id="0d4cd-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="0d4cd-234">Birinci komut geliştirme ortamına, ikinci komut test ortamına ve üçüncü komut üretim ortamına yönelik parametre dosyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-234">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="0d4cd-235">Ayrıca tekrarlanan görevleri gerçekleştirmek için şablonu yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-235">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="0d4cd-236">Örneğin, aynı mantığı uygulamasına karşın her veri fabrikasının farklı Azure depolama ve Azure SQL Veritabanı hesaplarını kullandığı bir veya daha fazla işlem hattı ile çok sayıda veri fabrikası oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-236">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="0d4cd-237">Bu senaryoda, aynı şablonu veri fabrikaları oluşturmaya yönelik farklı parametre dosyaları ile aynı ortamda (geliştirme, test veya üretim) kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-237">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="0d4cd-238">Bir ağ geçidi oluşturmak için Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="0d4cd-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="0d4cd-239">Arka planda mantıksal bir ağ geçidi oluşturmaya yönelik örnek bir Resource Manager şablonu aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-239">Here is a sample Resource Manager template for creating a logical gateway in the back.</span></span> <span data-ttu-id="0d4cd-240">Şirket içi bilgisayarınıza ya da Azure IaaS sanal makinesine bir ağ geçidi yükleyin ve bu ağ geçidini bir anahtar kullanarak Data Factory hizmetine kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-240">Install a gateway on your on-premises computer or Azure IaaS VM and register the gateway with Data Factory service using a key.</span></span> <span data-ttu-id="0d4cd-241">Ayrıntılar için bkz. [Şirket içi ile bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="0d4cd-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

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
<span data-ttu-id="0d4cd-242">Bu şablon GatewayUsingArmDF adlı bir veri fabrikasını GatewayUsingARM adlı bir ağ geçidi ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="0d4cd-243">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-243">See Also</span></span>
| <span data-ttu-id="0d4cd-244">Konu</span><span class="sxs-lookup"><span data-stu-id="0d4cd-244">Topic</span></span> | <span data-ttu-id="0d4cd-245">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0d4cd-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="0d4cd-246">İşlem hatları</span><span class="sxs-lookup"><span data-stu-id="0d4cd-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="0d4cd-247">Bu makale, Azure Data Factory’de işlem hatlarının ve etkinliklerini anlamanıza ve senaryonuz ya da işletmeniz için uçtan uca veri odaklı iş akışları oluşturmak amacıyla bunları nasıl kullanacağınızı anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-247">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="0d4cd-248">Veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="0d4cd-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="0d4cd-249">Bu makale, Azure Data Factory’deki veri kümelerini anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="0d4cd-250">Zamanlama ve yürütme</span><span class="sxs-lookup"><span data-stu-id="0d4cd-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="0d4cd-251">Bu makalede Azure Data Factory uygulama modelinin zamanlama ve yürütme yönleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-251">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="0d4cd-252">İzleme Uygulaması kullanılarak işlem hatlarını izleme ve yönetme</span><span class="sxs-lookup"><span data-stu-id="0d4cd-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="0d4cd-253">Bu makalede İzleme ve Yönetim Uygulaması kullanılarak işlem hatlarını izleme, yönetme ve hatalarını ayıklama işlemleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0d4cd-253">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |

