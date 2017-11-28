---
title: "Öğretici: Resource Manager Şablonu kullanarak bir işlem hattı oluşturma | Microsoft Belgeleri"
description: "Bu öğreticide, Azure Resource Manager şablonu kullanarak bir Azure Data Factory işlem hattı oluşturacaksınız. İşlem hattı, verileri Azure blob depolama alanlarından Azure SQL veritabanlarına kopyalar."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1274e11a-e004-4df5-af07-850b2de7c15e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 8a155213ed17e516a5c46abbe3d8a2bcc52268ed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-use-azure-resource-manager-template-to-create-a-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="6f3af-104">Öğretici: Verileri kopyalamak üzere bir Data Factory işlem hattı oluşturmak için Azure Resource Manager şablonunu kullanma</span><span class="sxs-lookup"><span data-stu-id="6f3af-104">Tutorial: Use Azure Resource Manager template to create a Data Factory pipeline to copy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6f3af-105">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="6f3af-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="6f3af-106">Kopyalama Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="6f3af-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="6f3af-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6f3af-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="6f3af-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6f3af-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="6f3af-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f3af-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="6f3af-110">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="6f3af-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="6f3af-111">REST API</span><span class="sxs-lookup"><span data-stu-id="6f3af-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="6f3af-112">.NET API’si</span><span class="sxs-lookup"><span data-stu-id="6f3af-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="6f3af-113">Bu öğreticide, Azure Resource Manager şablonu kullanarak bir Azure veri fabrikasını nasıl oluşturacağınız ve izleyeceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6f3af-113">This tutorial shows you how to use an Azure Resource Manager template to create an Azure data factory.</span></span> <span data-ttu-id="6f3af-114">Bu öğreticideki veri işlem hattı, bir kaynak veri deposundaki verileri hedef veri deposuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="6f3af-114">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="6f3af-115">Çıkış verileri üretmek için giriş verilerini dönüştürmez.</span><span class="sxs-lookup"><span data-stu-id="6f3af-115">It does not transform input data to produce output data.</span></span> <span data-ttu-id="6f3af-116">Azure Data Factory kullanarak verileri dönüştürme hakkında bir öğretici için bkz. [Öğretici: Hadoop kümesi kullanarak verileri dönüştürmek için işlem hattı oluşturma](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="6f3af-116">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="6f3af-117">Bu öğreticide, içinde yalnızca şu etkinlik olan bir işlem hattı oluşturacaksınız: Kopyalama Etkinliği.</span><span class="sxs-lookup"><span data-stu-id="6f3af-117">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="6f3af-118">Kopyalama etkinliği, verileri, desteklenen bir veri deposundan desteklenen bir havuz veri deposuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="6f3af-118">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="6f3af-119">Kaynak ve havuz olarak desteklenen veri depolarının listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="6f3af-119">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="6f3af-120">Etkinlik, çeşitli veri depolama alanları arasında güvenli, güvenilir ve ölçeklenebilir bir yolla veri kopyalayabilen genel olarak kullanılabilir bir hizmet tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="6f3af-120">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="6f3af-121">Kopyalama Etkinliği hakkında daha fazla bilgi için bkz. [Veri Taşıma Etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6f3af-121">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="6f3af-122">Bir işlem hattında birden fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="6f3af-122">A pipeline can have more than one activity.</span></span> <span data-ttu-id="6f3af-123">Bir etkinliğin çıkış veri kümesini diğer etkinliğin giriş veri kümesi olarak ayarlayarak iki etkinliği zincirleyebilir, yani bir etkinliğin diğerinden sonra çalıştırılmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6f3af-123">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="6f3af-124">Daha fazla bilgi için bkz. [bir işlem hattında birden fazla etkinlik](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="6f3af-124">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="6f3af-125">Bu öğreticideki veri işlem hattı, bir kaynak veri deposundaki verileri hedef veri deposuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="6f3af-125">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="6f3af-126">Azure Data Factory kullanarak verileri dönüştürme hakkında bir öğretici için bkz. [Öğretici: Hadoop kümesi kullanarak verileri dönüştürmek için işlem hattı oluşturma](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="6f3af-126">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6f3af-127">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6f3af-127">Prerequisites</span></span>
* <span data-ttu-id="6f3af-128">[Öğreticiye Genel Bakış ve Ön Koşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) bölümünü inceleyin ve **ön koşul** adımlarını tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="6f3af-128">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="6f3af-129">Bilgisayarınıza Azure PowerShell’in en son sürümünü yüklemek için [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azure/overview) makalesindeki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="6f3af-129">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="6f3af-130">Bu öğreticide PowerShell’i kullanarak Data Factory varlıklarını dağıtırsınız.</span><span class="sxs-lookup"><span data-stu-id="6f3af-130">In this tutorial, you use PowerShell to deploy Data Factory entities.</span></span> 
* <span data-ttu-id="6f3af-131">(isteğe bağlı) Azure Resource Manager şablonları hakkında bilgi için bkz. [Azure Resource Manager Şablonları Yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6f3af-131">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="6f3af-132">Bu öğreticide</span><span class="sxs-lookup"><span data-stu-id="6f3af-132">In this tutorial</span></span>
<span data-ttu-id="6f3af-133">Bu öğreticide, aşağıdaki Data Factory varlıklarıyla bir veri fabrikası oluşturursunuz:</span><span class="sxs-lookup"><span data-stu-id="6f3af-133">In this tutorial, you create a data factory with the following Data Factory entities:</span></span>

| <span data-ttu-id="6f3af-134">Varlık</span><span class="sxs-lookup"><span data-stu-id="6f3af-134">Entity</span></span> | <span data-ttu-id="6f3af-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6f3af-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6f3af-136">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="6f3af-136">Azure Storage linked service</span></span> |<span data-ttu-id="6f3af-137">Azure Storage hesabınızı veri fabrikasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="6f3af-137">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="6f3af-138">Öğreticideki kopyalama etkinliği için Azure Storage kaynak veri deposu, Azure SQL veritabanı ise havuz veri deposudur.</span><span class="sxs-lookup"><span data-stu-id="6f3af-138">Azure Storage is the source data store and Azure SQL database is the sink data store for the copy activity in the tutorial.</span></span> <span data-ttu-id="6f3af-139">Kopyalama etkinliği için giriş verilerini içeren depolama hesabını belirtir.</span><span class="sxs-lookup"><span data-stu-id="6f3af-139">It specifies the storage account that contains the input data for the copy activity.</span></span> |
| <span data-ttu-id="6f3af-140">Azure SQL Veritabanı bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="6f3af-140">Azure SQL Database linked service</span></span> |<span data-ttu-id="6f3af-141">Azure SQL veritabanınızı veri fabrikasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="6f3af-141">Links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="6f3af-142">Kopyalama etkinliği için çıktı verilerini tutan Azure SQL veritabanını belirtir.</span><span class="sxs-lookup"><span data-stu-id="6f3af-142">It specifies the Azure SQL database that holds the output data for the copy activity.</span></span> |
| <span data-ttu-id="6f3af-143">Azure Blob giriş veri kümesi</span><span class="sxs-lookup"><span data-stu-id="6f3af-143">Azure Blob input dataset</span></span> |<span data-ttu-id="6f3af-144">Azure Storage bağlı hizmetini ifade eder.</span><span class="sxs-lookup"><span data-stu-id="6f3af-144">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="6f3af-145">Bağlı hizmet bir Azure Storage hesabını belirtirken, Azure Blob veri kümesi girdi verilerini tutan depolama birimindeki kapsayıcı, klasör ve dosya adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="6f3af-145">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="6f3af-146">Azure SQL çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="6f3af-146">Azure SQL output dataset</span></span> |<span data-ttu-id="6f3af-147">Azure SQL bağlı hizmetini ifade eder.</span><span class="sxs-lookup"><span data-stu-id="6f3af-147">Refers to the Azure SQL linked service.</span></span> <span data-ttu-id="6f3af-148">Azure SQL bağlı hizmeti bir Azure SQL sunucusunu, Azure SQL veri kümesi ise çıktı verilerini tutan tablonun adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="6f3af-148">The Azure SQL linked service refers to an Azure SQL server and the Azure SQL dataset specifies the name of the table that holds the output data.</span></span> |
| <span data-ttu-id="6f3af-149">Veri işlem hattı</span><span class="sxs-lookup"><span data-stu-id="6f3af-149">Data pipeline</span></span> |<span data-ttu-id="6f3af-150">İşlem hattı, Azure blob veri kümesini girdi, Azure SQL veri kümesini ise çıktı olarak alan Kopyalama türünde bir etkinliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="6f3af-150">The pipeline has one activity of type Copy that takes the Azure blob dataset as an input and the Azure SQL dataset as an output.</span></span> <span data-ttu-id="6f3af-151">Kopyalama etkinliği, verileri bir Azure blob’undan Azure SQL veritabanındaki tabloya kopyalar.</span><span class="sxs-lookup"><span data-stu-id="6f3af-151">The copy activity copies data from an Azure blob to a table in the Azure SQL database.</span></span> |

<span data-ttu-id="6f3af-152">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="6f3af-152">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="6f3af-153">İşlem hattında bir veya daha fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="6f3af-153">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="6f3af-154">İki tür etkinlik mevcuttur: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) ve [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6f3af-154">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="6f3af-155">Bu öğreticide bir etkinlik (kopyalama etkinliği) ile işlem hattı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="6f3af-155">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![Azure Blob’u Azure SQL Veritabanına kopyalama](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="6f3af-157">Aşağıdaki bölümde, öğreticiyi hızlıca geçip şablonu test etmeniz için Data Factory varlıklarını tanımlamaya yönelik tam bir Resource Manager şablonu verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6f3af-157">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="6f3af-158">Her bir Data Factory varlığının nasıl tanımlandığını anlamak için [Şablondaki Data Factory varlıkları](#data-factory-entities-in-the-template) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="6f3af-158">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="6f3af-159">Data Factory JSON şablonu</span><span class="sxs-lookup"><span data-stu-id="6f3af-159">Data Factory JSON template</span></span>
<span data-ttu-id="6f3af-160">Bir veri fabrikasını tanımlamaya yönelik en üst düzey Resource Manager şablonu şudur:</span><span class="sxs-lookup"><span data-stu-id="6f3af-160">The top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="6f3af-161">**C:\ADFGetStarted** klasöründe aşağıdaki içeriklerle birlikte **ADFCopyTutorialARM.json** adlı bir JSON dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="6f3af-161">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of the Azure storage account that contains the data to be copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for the Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of the blob container in the Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of the blob in the container that has the data to be copied to Azure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of the Azure SQL Server that will hold the output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of the Azure SQL Database in the Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of the user that has access to the Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for the user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in the Azure SQL Database that will hold the copied data." } 
      } 
    },
    "variables": {
      "dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]",
      "azureSqlLinkedServiceName": "AzureSqlLinkedService",
      "azureStorageLinkedServiceName": "AzureStorageLinkedService",
      "blobInputDatasetName": "BlobInputDataset",
      "sqlOutputDatasetName": "SQLOutputDataset",
      "pipelineName": "Blob2SQLPipeline"
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
            "name": "[variables('azureSqlLinkedServiceName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlDatabase",
              "description": "Azure SQL linked service",
              "typeProperties": {
                "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
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
              "structure": [
                {
                  "name": "Column0",
                  "type": "String"
                },
                {
                  "name": "Column1",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
                "fileName": "[parameters('sourceBlobName')]",
                "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
                }
              },
              "availability": {
                "frequency": "Hour",
                "interval": 1
              },
              "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('sqlOutputDatasetName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureSqlLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlTable",
              "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
              "structure": [
                {
                  "name": "FirstName",
                  "type": "String"
                },
                {
                  "name": "LastName",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "tableName": "[parameters('targetSQLTable')]"
              },
              "availability": {
                "frequency": "Hour",
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
              "[variables('azureSqlLinkedServiceName')]",
              "[variables('blobInputDatasetName')]",
              "[variables('sqlOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "activities": [
                {
                  "name": "CopyFromAzureBlobToAzureSQL",
                  "description": "Copy data frm Azure blob to Azure SQL",
                  "type": "Copy",
                  "inputs": [
                    {
                      "name": "[variables('blobInputDatasetName')]"
                    }
                  ],
                  "outputs": [
                    {
                      "name": "[variables('sqlOutputDatasetName')]"
                    }
                  ],
                  "typeProperties": {
                    "source": {
                      "type": "BlobSource"
                    },
                    "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                    },
                    "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                    }
                  },
                  "Policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 3,
                    "timeout": "01:00:00"
                  }
                }
              ],
              "start": "2017-05-11T00:00:00Z",
              "end": "2017-05-12T00:00:00Z"
            }
          }
        ]
      }
    ]
  }
```

## <a name="parameters-json"></a><span data-ttu-id="6f3af-162">Parametreler JSON</span><span class="sxs-lookup"><span data-stu-id="6f3af-162">Parameters JSON</span></span>
<span data-ttu-id="6f3af-163">Azure Resource Manager şablonuna yönelik parametreleri içeren **ADFCopyTutorialARM-Parameters.json** adlı bir JSON dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6f3af-163">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6f3af-164">storageAccountName ve storageAccountKey parametreleri için Azure Depolama hesabınızın adını ve anahtarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="6f3af-164">Specify name and key of your Azure Storage account for storageAccountName and storageAccountKey parameters.</span></span>  
> 
> <span data-ttu-id="6f3af-165">sqlServerName, databaseName, sqlServerUserName ve sqlServerPassword parametreleri için Azure SQL sunucusunu, veritabanını, kullanıcıyı ve parolayı belirtin.</span><span class="sxs-lookup"><span data-stu-id="6f3af-165">Specify Azure SQL server, database, user, and password for sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters.</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of the Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for the Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of the Azure SQL server>" },
        "databaseName": { "value": "<Name of the Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of the user who has access to the Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for the user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="6f3af-166">Aynı Data Factory JSON şablonuyla birlikte kullanabileceğiniz geliştirme, test ve üretim ortamları için ayrı parametre JSON dosyalarına sahip olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6f3af-166">You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template.</span></span> <span data-ttu-id="6f3af-167">Bir Power Shell komut dosyası kullanarak, bu ortamlarda Data Factory varlıklarını dağıtmayı otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6f3af-167">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span>  
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="6f3af-168">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="6f3af-168">Create data factory</span></span>
1. <span data-ttu-id="6f3af-169">**Azure PowerShell**’i başlatın ve aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6f3af-169">Start **Azure PowerShell** and run the following command:</span></span>
   * <span data-ttu-id="6f3af-170">Aşağıdaki komutu çalıştırın ve Azure portalda oturum açmak için kullandığınız kullanıcı adı ve parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="6f3af-170">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * <span data-ttu-id="6f3af-171">Bu hesapla ilgili tüm abonelikleri görmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6f3af-171">Run the following command to view all the subscriptions for this account.</span></span>
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="6f3af-172">Çalışmak isteğiniz aboneliği seçmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6f3af-172">Run the following command to select the subscription that you want to work with.</span></span>
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="6f3af-173">1 Adımda oluşturduğunuz Resource Manager şablonunu kullanarak Data Factory varlıklarını dağıtmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6f3af-173">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="6f3af-174">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="6f3af-174">Monitor pipeline</span></span>

1. <span data-ttu-id="6f3af-175">Azure hesabınızı kullanarak [Azure portalında](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6f3af-175">Log in to the [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="6f3af-176">Sol menüdeki **Veri fabrikaları**’na tıklayın (veya) **INTELLIGENCE + ANALYTICS** kategorisi altındaki **Diğer hizmetler** ve **Veri fabrikaları** öğelerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6f3af-176">Click **Data factories** on the left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![Veri fabrikaları menüsü](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="6f3af-178">**Veri fabrikaları** sayfasında veri fabrikanızı (AzureBlobToAzureSQLDatabaseDF) bulun.</span><span class="sxs-lookup"><span data-stu-id="6f3af-178">In the **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span></span> 
   
    ![Veri fabrikası arama](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="6f3af-180">Azure veri fabrikanıza tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6f3af-180">Click your Azure data factory.</span></span> <span data-ttu-id="6f3af-181">Veri fabrikasının giriş sayfasını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6f3af-181">You see the home page for the data factory.</span></span>
   
    ![Veri fabrikasının giriş sayfası](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. <span data-ttu-id="6f3af-183">Bu öğreticide oluşturduğunuz işlem hattını ve veri kümelerini izlemek için [Veri kümelerini ve işlem hatlarını izleme](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) makalesindeki yönergeleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="6f3af-183">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) to monitor the pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="6f3af-184">Visual Studio şu anda Data Factory işlem hatlarını izlemeyi desteklememektedir.</span><span class="sxs-lookup"><span data-stu-id="6f3af-184">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span>
7. <span data-ttu-id="6f3af-185">Bir dilim **Hazır** durumundayken verilerin Azure SQL veritabanındaki **emp** tablosuna kopyalandığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="6f3af-185">When a slice is in the **Ready** state, verify that the data is copied to the **emp** table in the Azure SQL database.</span></span>


<span data-ttu-id="6f3af-186">Bu öğreticide oluşturduğunuz işlem hattını ve veri kümelerini izlemek üzere Azure portalı dikey pencerelerinin kullanımına ilişkin daha fazla bilgi için bkz. [Veri kümelerini ve işlem hatlarını izleme](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="6f3af-186">For more information on how to use Azure portal blades to monitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span></span>

<span data-ttu-id="6f3af-187">Veri işlem hatlarınızı izlemek üzere İzleme ve Yönetme uygulamasının kullanımına ilişkin daha fazla bilgi için bkz. [İzleme Uygulamasını kullanarak Azure Data Factory işlem hatlarını izleme ve yönetme](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="6f3af-187">For more information on how to use the Monitor & Manage application to monitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span></span>

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="6f3af-188">Şablondaki Data Factory varlıkları</span><span class="sxs-lookup"><span data-stu-id="6f3af-188">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="6f3af-189">Veri fabrikası tanımlama</span><span class="sxs-lookup"><span data-stu-id="6f3af-189">Define data factory</span></span>
<span data-ttu-id="6f3af-190">Resource Manager şablonunda bir veri fabrikasını aşağıdaki örnekte gösterildiği gibi tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="6f3af-190">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="6f3af-191">dataFactoryName aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="6f3af-191">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="6f3af-192">Bu değer, kaynak grubu kimliğini temel alan benzersiz bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="6f3af-192">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="6f3af-193">Data Factory varlıklarını tanımlama</span><span class="sxs-lookup"><span data-stu-id="6f3af-193">Defining Data Factory entities</span></span>
<span data-ttu-id="6f3af-194">Aşağıdaki Data Factory varlıkları JSON şablonunda tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="6f3af-194">The following Data Factory entities are defined in the JSON template:</span></span> 

1. [<span data-ttu-id="6f3af-195">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="6f3af-195">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="6f3af-196">Azure SQL bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="6f3af-196">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="6f3af-197">Azure blob veri kümesi</span><span class="sxs-lookup"><span data-stu-id="6f3af-197">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="6f3af-198">Azure SQL veri kümesi</span><span class="sxs-lookup"><span data-stu-id="6f3af-198">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="6f3af-199">Kopyalama etkinliği içeren bir veri işlem hattı</span><span class="sxs-lookup"><span data-stu-id="6f3af-199">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="6f3af-200">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="6f3af-200">Azure Storage linked service</span></span>
<span data-ttu-id="6f3af-201">AzureStorageLinkedService, Azure depolama hesabınızı veri fabrikasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="6f3af-201">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="6f3af-202">Bir kapsayıcı oluşturup verileri [önkoşulların](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) parçası olarak bu depolama hesabına yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="6f3af-202">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="6f3af-203">Bu bölümde Azure depolama hesabınızın adını ve anahtarını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6f3af-203">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="6f3af-204">Bir Azure Storage bağlı hizmetini tanımlamak için kullanılan JSON özelliklerine ilişkin ayrıntılar için bkz. [Azure Storage bağlı hizmeti](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="6f3af-204">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

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

<span data-ttu-id="6f3af-205">ConnectionString, storageAccountName ve storageAccountKey parametrelerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="6f3af-205">The connectionString uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="6f3af-206">Bu parametrelerin değerleri bir yapılandırma dosyası kullanılarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="6f3af-206">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="6f3af-207">Tanım ayrıca şu değişkenleri kullanır: şablonda tanımlanan azureStroageLinkedService ve dataFactoryName.</span><span class="sxs-lookup"><span data-stu-id="6f3af-207">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="6f3af-208">Azure SQL Veritabanı bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="6f3af-208">Azure SQL Database linked service</span></span>
<span data-ttu-id="6f3af-209">AzureSqlLinkedService, Azure SQL veritabanınızı veri fabrikasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="6f3af-209">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="6f3af-210">Blob depolama alanından kopyalanan veriler bu veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="6f3af-210">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="6f3af-211">Bu veritabanındaki emp tablosunu, [önkoşulların](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) parçası olarak oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="6f3af-211">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="6f3af-212">Bu bölümde Azure SQL sunucu adı, veritabanı adı, kullanıcı adı ve kullanıcı parolasını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6f3af-212">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="6f3af-213">Bir Azure SQL bağlı hizmetini tanımlamak için kullanılan JSON özelliklerine ilişkin ayrıntılar için bkz. [Azure SQL bağlı hizmeti](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6f3af-213">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span></span>  

```json
{
    "type": "linkedservices",
    "name": "[variables('azureSqlLinkedServiceName')]",
    "dependsOn": [
      "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlDatabase",
          "description": "Azure SQL linked service",
          "typeProperties": {
            "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
          }
    }
}
```

<span data-ttu-id="6f3af-214">connectionString; değerleri bir yapılandırma dosyası kullanılarak geçirilen sqlServerName, databaseName, sqlServerUserName ve sqlServerPassword parametrelerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="6f3af-214">The connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="6f3af-215">Tanımda ayrıca şablondaki şu değişkenler kullanılır: azureSqlLinkedServiceName, dataFactoryName.</span><span class="sxs-lookup"><span data-stu-id="6f3af-215">The definition also uses the following variables from the template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="6f3af-216">Azure blob veri kümesi</span><span class="sxs-lookup"><span data-stu-id="6f3af-216">Azure blob dataset</span></span>
<span data-ttu-id="6f3af-217">Azure Depolama bağlı hizmeti, Data Factory hizmetinin Azure depolama hesabınıza bağlanmak için çalışma zamanında kullandığı bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="6f3af-217">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="6f3af-218">Azure blob veri kümesi tanımında blob kapsayıcısını, klasörü ve giriş verilerini içeren dosyanın adını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6f3af-218">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="6f3af-219">Bir Azure Blob veri kümesini tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılar için bkz. [Azure Blob veri kümesi özellikleri](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6f3af-219">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

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
        "structure": [
        {
              "name": "Column0",
              "type": "String"
        },
        {
              "name": "Column1",
              "type": "String"
        }
          ],
          "typeProperties": {
            "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
            "fileName": "[parameters('sourceBlobName')]",
            "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
            }
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          },
          "external": true
    }
}
```

#### <a name="azure-sql-dataset"></a><span data-ttu-id="6f3af-220">Azure SQL veri kümesi</span><span class="sxs-lookup"><span data-stu-id="6f3af-220">Azure SQL dataset</span></span>
<span data-ttu-id="6f3af-221">Azure SQL veritabanında Azure Blob depolama biriminden kopyalanan verileri tutan tablonun adını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6f3af-221">You specify the name of the table in the Azure SQL database that holds the copied data from the Azure Blob storage.</span></span> <span data-ttu-id="6f3af-222">Bir Azure SQL veri kümesini tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılar için bkz. [Azure SQL veri kümesi özellikleri](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6f3af-222">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used to define an Azure SQL dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('sqlOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureSqlLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlTable",
          "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
          "structure": [
        {
              "name": "FirstName",
              "type": "String"
        },
        {
              "name": "LastName",
              "type": "String"
        }
          ],
          "typeProperties": {
            "tableName": "[parameters('targetSQLTable')]"
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          }
    }
}
```

#### <a name="data-pipeline"></a><span data-ttu-id="6f3af-223">Veri işlem hattı</span><span class="sxs-lookup"><span data-stu-id="6f3af-223">Data pipeline</span></span>
<span data-ttu-id="6f3af-224">Verileri Azure blob veri kümesinden Azure SQL veri kümesine kopyalayan bir işlem hattı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="6f3af-224">You define a pipeline that copies data from the Azure blob dataset to the Azure SQL dataset.</span></span> <span data-ttu-id="6f3af-225">Bu örnekte bir işlem hattı tanımlamak için kullanılan JSON öğelerinin açıklamaları için bkz. [İşlem Hattı JSON](data-factory-create-pipelines.md#pipeline-json).</span><span class="sxs-lookup"><span data-stu-id="6f3af-225">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureStorageLinkedServiceName')]",
          "[variables('azureSqlLinkedServiceName')]",
          "[variables('blobInputDatasetName')]",
          "[variables('sqlOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "activities": [
        {
              "name": "CopyFromAzureBlobToAzureSQL",
              "description": "Copy data frm Azure blob to Azure SQL",
              "type": "Copy",
              "inputs": [
            {
                  "name": "[variables('blobInputDatasetName')]"
            }
              ],
              "outputs": [
            {
                  "name": "[variables('sqlOutputDatasetName')]"
            }
              ],
              "typeProperties": {
                "source": {
                      "type": "BlobSource"
                },
                "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                },
                "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                }
              },
              "Policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 3,
                "timeout": "01:00:00"
              }
        }
          ],
          "start": "2017-05-11T00:00:00Z",
          "end": "2017-05-12T00:00:00Z"
    }
}
```

## <a name="reuse-the-template"></a><span data-ttu-id="6f3af-226">Şablonu yeniden kullanma</span><span class="sxs-lookup"><span data-stu-id="6f3af-226">Reuse the template</span></span>
<span data-ttu-id="6f3af-227">Bu öğreticide, Data Factory varlıkları tanımlamaya yönelik bir şablon ve parametrelerin değerlerini geçirmeye yönelik bir şablon oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="6f3af-227">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="6f3af-228">İşlem hattı, verileri bir Azure Storage hesabından parametreler aracılığıyla belirtilen bir Azure SQL veritabanına kopyalar.</span><span class="sxs-lookup"><span data-stu-id="6f3af-228">The pipeline copies data from an Azure Storage account to an Azure SQL database specified via parameters.</span></span> <span data-ttu-id="6f3af-229">Data Factory varlıklarını farklı ortamlara dağıtmak üzere aynı şablonu kullanmak için, her bir ortama yönelik bir parametre dosyası oluşturur ve bu ortama dağıtırken kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="6f3af-229">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="6f3af-230">Örnek:</span><span class="sxs-lookup"><span data-stu-id="6f3af-230">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="6f3af-231">Birinci komut geliştirme ortamına, ikinci komut test ortamına ve üçüncü komut üretim ortamına yönelik parametre dosyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="6f3af-231">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="6f3af-232">Ayrıca tekrarlanan görevleri gerçekleştirmek için şablonu yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6f3af-232">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="6f3af-233">Örneğin, aynı mantığı uygulamasına karşın her veri fabrikasının farklı Depolama ve SQL Veritabanı hesaplarını kullandığı bir veya daha fazla işlem hattı ile çok sayıda veri fabrikası oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f3af-233">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="6f3af-234">Bu senaryoda, aynı şablonu veri fabrikaları oluşturmaya yönelik farklı parametre dosyaları ile aynı ortamda (geliştirme, test veya üretim) kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="6f3af-234">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="6f3af-235">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6f3af-235">Next steps</span></span>
<span data-ttu-id="6f3af-236">Bu öğreticide, bir kopyalama işleminde kaynak veri deposu olarak Azure blob depolama alanını ve hedef veri deposu olarak Azure SQL veritabanını kullandınız.</span><span class="sxs-lookup"><span data-stu-id="6f3af-236">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="6f3af-237">Aşağıdaki tabloda, kopyalama etkinliği tarafından kaynak ve hedef olarak desteklenen veri depolarının listesi sağlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="6f3af-237">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="6f3af-238">Veri deposundan/veri deposuna veri kopyalama hakkında bilgi edinmek için tablodaki veri deposunun bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6f3af-238">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>
