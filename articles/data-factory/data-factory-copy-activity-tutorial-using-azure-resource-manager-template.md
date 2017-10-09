---
title: "Öğretici: Resource Manager Şablonu kullanarak bir işlem hattı oluşturma | Microsoft Belgeleri"
description: "Bu öğreticide, Azure Resource Manager şablonu kullanarak bir Azure Data Factory işlem hattı oluşturacaksınız. Bu işlem hattı verileri Azure blob depolama tooan Azure SQL veritabanından kopyalar."
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
ms.openlocfilehash: 1c7567cb0423f7ce3e0cab2d77a4d861b70eb56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-resource-manager-template-toocreate-a-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="8cbe6-104">Öğretici: Azure Kaynak Yöneticisi'ni kullanın şablonu toocreate Data Factory işlem hattı toocopy veri</span><span class="sxs-lookup"><span data-stu-id="8cbe6-104">Tutorial: Use Azure Resource Manager template toocreate a Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8cbe6-105">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="8cbe6-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="8cbe6-106">Kopyalama Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="8cbe6-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="8cbe6-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8cbe6-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="8cbe6-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8cbe6-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="8cbe6-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cbe6-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="8cbe6-110">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="8cbe6-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="8cbe6-111">REST API</span><span class="sxs-lookup"><span data-stu-id="8cbe6-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="8cbe6-112">.NET API’si</span><span class="sxs-lookup"><span data-stu-id="8cbe6-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="8cbe6-113">Bu öğretici şunların nasıl yapıldığını gösterir toouse Azure Resource Manager şablonu toocreate bir Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-113">This tutorial shows you how toouse an Azure Resource Manager template toocreate an Azure data factory.</span></span> <span data-ttu-id="8cbe6-114">Merhaba veri ardışık Bu öğreticide, bir kaynak veri deposu tooa hedef veri deposundan verileri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-114">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="8cbe6-115">Giriş verisi tooproduce çıktı verilerini dönüştürmez.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-115">It does not transform input data tooproduce output data.</span></span> <span data-ttu-id="8cbe6-116">Nasıl bir öğretici için Azure Data Factory kullanarak tootransform verileri görmek [Öğreticisi: Hadoop kümesi kullanarak bir ardışık düzen tootransform veri derleme](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="8cbe6-116">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="8cbe6-117">Bu öğreticide, içinde bir etkinlik olan işlem hattı oluşturursunuz: Kopyalama Etkinliği.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-117">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="8cbe6-118">Merhaba kopyalama etkinliği bir desteklenen veri deposu tooa desteklenen havuz veri deposundan verileri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-118">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="8cbe6-119">Kaynak ve havuz olarak desteklenen veri depolarının listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="8cbe6-119">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="8cbe6-120">Merhaba etkinlik verileri güvenli, güvenilir ve ölçeklenebilir bir şekilde çeşitli veri depolamaları arasında kopyalayabilirsiniz genel olarak kullanılabilir bir hizmet tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-120">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="8cbe6-121">Merhaba kopyalama etkinliği hakkında daha fazla bilgi için bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="8cbe6-121">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="8cbe6-122">Bir işlem hattında birden fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-122">A pipeline can have more than one activity.</span></span> <span data-ttu-id="8cbe6-123">Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-123">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="8cbe6-124">Daha fazla bilgi için bkz. [bir işlem hattında birden fazla etkinlik](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="8cbe6-124">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="8cbe6-125">Merhaba veri ardışık Bu öğreticide, bir kaynak veri deposu tooa hedef veri deposundan verileri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-125">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="8cbe6-126">Nasıl bir öğretici için Azure Data Factory kullanarak tootransform verileri görmek [Öğreticisi: Hadoop kümesi kullanarak bir ardışık düzen tootransform veri derleme](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="8cbe6-126">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8cbe6-127">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8cbe6-127">Prerequisites</span></span>
* <span data-ttu-id="8cbe6-128">Git üzerinden [öğreticiye genel bakış ve önkoşulları](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) ve tam hello **önkoşul** adımları.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-128">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="8cbe6-129">' Ndaki yönergeleri izleyin [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) makale tooinstall en son sürümü Azure PowerShell, bilgisayarınızda.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-129">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="8cbe6-130">Bu öğreticide PowerShell toodeploy Data Factory varlıklarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-130">In this tutorial, you use PowerShell toodeploy Data Factory entities.</span></span> 
* <span data-ttu-id="8cbe6-131">(isteğe bağlı) Bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md) toolearn Azure Resource Manager şablonları hakkında.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-131">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="8cbe6-132">Bu öğreticide</span><span class="sxs-lookup"><span data-stu-id="8cbe6-132">In this tutorial</span></span>
<span data-ttu-id="8cbe6-133">Bu öğreticide, Data Factory varlıklarını aşağıdaki hello ile bir veri fabrikası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="8cbe6-133">In this tutorial, you create a data factory with hello following Data Factory entities:</span></span>

| <span data-ttu-id="8cbe6-134">Varlık</span><span class="sxs-lookup"><span data-stu-id="8cbe6-134">Entity</span></span> | <span data-ttu-id="8cbe6-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cbe6-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8cbe6-136">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="8cbe6-136">Azure Storage linked service</span></span> |<span data-ttu-id="8cbe6-137">Azure depolama hesabı toohello veri fabrikanıza bağlar.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-137">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="8cbe6-138">Azure depolama hello kaynak veri deposu ve Azure SQL veritabanı hello kopyalama etkinliği için hello havuz veri deposu hello öğreticide.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-138">Azure Storage is hello source data store and Azure SQL database is hello sink data store for hello copy activity in hello tutorial.</span></span> <span data-ttu-id="8cbe6-139">Hello hello kopyalama etkinliği için giriş verileri içeren hello depolama hesabını belirtir.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-139">It specifies hello storage account that contains hello input data for hello copy activity.</span></span> |
| <span data-ttu-id="8cbe6-140">Azure SQL Veritabanı bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="8cbe6-140">Azure SQL Database linked service</span></span> |<span data-ttu-id="8cbe6-141">Azure SQL veritabanı toohello veri fabrikanıza bağlar.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-141">Links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="8cbe6-142">Merhaba kopyalama etkinliği için hello çıktı verilerini tutan hello Azure SQL veritabanı belirtir.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-142">It specifies hello Azure SQL database that holds hello output data for hello copy activity.</span></span> |
| <span data-ttu-id="8cbe6-143">Azure Blob giriş veri kümesi</span><span class="sxs-lookup"><span data-stu-id="8cbe6-143">Azure Blob input dataset</span></span> |<span data-ttu-id="8cbe6-144">Toohello Azure Storage bağlı hizmeti anlamına gelmektedir.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-144">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="8cbe6-145">Merhaba bağlantılı hizmet tooan Azure depolama hesabı anlamına gelir ve hello Azure Blob dataset hello girdi verilerini tutan hello depolama hello kapsayıcı, klasör ve dosya adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-145">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="8cbe6-146">Azure SQL çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="8cbe6-146">Azure SQL output dataset</span></span> |<span data-ttu-id="8cbe6-147">Toohello Azure SQL bağlı hizmeti anlamına gelmektedir.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-147">Refers toohello Azure SQL linked service.</span></span> <span data-ttu-id="8cbe6-148">Hello Azure SQL bağlı hizmeti tooan Azure SQL server anlamına gelir ve hello Azure SQL veri kümesi hello hello çıktı verilerini tutan Merhaba tablonun adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-148">hello Azure SQL linked service refers tooan Azure SQL server and hello Azure SQL dataset specifies hello name of hello table that holds hello output data.</span></span> |
| <span data-ttu-id="8cbe6-149">Veri işlem hattı</span><span class="sxs-lookup"><span data-stu-id="8cbe6-149">Data pipeline</span></span> |<span data-ttu-id="8cbe6-150">Merhaba ardışık düzen hello Azure blob dataset bir girdi olarak alır kopyalama yazın ve Azure SQL veri kümesi bir çıkış olarak hello bir etkinlik vardır.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-150">hello pipeline has one activity of type Copy that takes hello Azure blob dataset as an input and hello Azure SQL dataset as an output.</span></span> <span data-ttu-id="8cbe6-151">Merhaba kopyalama etkinliği hello Azure SQL veritabanındaki bir Azure blob tooa tablodan veri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-151">hello copy activity copies data from an Azure blob tooa table in hello Azure SQL database.</span></span> |

<span data-ttu-id="8cbe6-152">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-152">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="8cbe6-153">İşlem hattında bir veya daha fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-153">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="8cbe6-154">İki tür etkinlik mevcuttur: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) ve [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="8cbe6-154">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="8cbe6-155">Bu öğreticide bir etkinlik (kopyalama etkinliği) ile işlem hattı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-155">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![Azure Blob tooAzure SQL veritabanını kopyalama](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="8cbe6-157">Merhaba aşağıdaki bölümde hello tam Resource Manager şablonu, hızlı başlangıç Öğreticisi ve test hello şablonu aracılığıyla çalıştırabilmeniz için Data Factory varlıklarını tanımlamak için sağlar.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-157">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="8cbe6-158">Her bir veri fabrikası varlık tanımlanan toounderstand bkz [Data Factory varlıklarını hello şablonunda](#data-factory-entities-in-the-template) bölümü.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-158">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="8cbe6-159">Data Factory JSON şablonu</span><span class="sxs-lookup"><span data-stu-id="8cbe6-159">Data Factory JSON template</span></span>
<span data-ttu-id="8cbe6-160">Veri Fabrikası tanımlamak için hello en üst düzey Resource Manager şablonu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="8cbe6-160">hello top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="8cbe6-161">Adlı bir JSON dosyası oluşturun **ADFCopyTutorialARM.json** içinde **C:\ADFGetStarted** içeriği aşağıdaki hello klasörüyle:</span><span class="sxs-lookup"><span data-stu-id="8cbe6-161">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello data toobe copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of hello blob in hello container that has hello data toobe copied tooAzure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Server that will hold hello output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Database in hello Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of hello user that has access toohello Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for hello user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in hello Azure SQL Database that will hold hello copied data." } 
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
                  "description": "Copy data frm Azure blob tooAzure SQL",
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

## <a name="parameters-json"></a><span data-ttu-id="8cbe6-162">Parametreler JSON</span><span class="sxs-lookup"><span data-stu-id="8cbe6-162">Parameters JSON</span></span>
<span data-ttu-id="8cbe6-163">Adlı bir JSON dosyası oluşturun **ADFCopyTutorialARM Parameters.json** hello Azure Resource Manager şablonu parametrelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-163">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8cbe6-164">storageAccountName ve storageAccountKey parametreleri için Azure Depolama hesabınızın adını ve anahtarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-164">Specify name and key of your Azure Storage account for storageAccountName and storageAccountKey parameters.</span></span>  
> 
> <span data-ttu-id="8cbe6-165">sqlServerName, databaseName, sqlServerUserName ve sqlServerPassword parametreleri için Azure SQL sunucusunu, veritabanını, kullanıcıyı ve parolayı belirtin.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-165">Specify Azure SQL server, database, user, and password for sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters.</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of hello Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for hello Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of hello Azure SQL server>" },
        "databaseName": { "value": "<Name of hello Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of hello user who has access toohello Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for hello user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="8cbe6-166">Ayrı parametre JSON geliştirme, test dosyalarınız ve aynı veri fabrikası JSON şablonu ile birlikte kullanabileceğiniz üretim ortamlarında hello.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-166">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="8cbe6-167">Bir Power Shell komut dosyası kullanarak, bu ortamlarda Data Factory varlıklarını dağıtmayı otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-167">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span>  
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="8cbe6-168">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="8cbe6-168">Create data factory</span></span>
1. <span data-ttu-id="8cbe6-169">Başlat **Azure PowerShell** ve çalışma hello aşağıdaki komutu:</span><span class="sxs-lookup"><span data-stu-id="8cbe6-169">Start **Azure PowerShell** and run hello following command:</span></span>
   * <span data-ttu-id="8cbe6-170">Merhaba aşağıdaki komutu çalıştırın ve hello kullanıcı adı ve parola toosign toohello Azure portal kullanın girin.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-170">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * <span data-ttu-id="8cbe6-171">Bu hesap için tüm hello abonelikleri komutu tooview aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-171">Run hello following command tooview all hello subscriptions for this account.</span></span>
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="8cbe6-172">Çalışma hello aşağıdaki toowork ile istediğiniz tooselect hello abonelik komutu.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-172">Run hello following command tooselect hello subscription that you want toowork with.</span></span>
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="8cbe6-173">1. adımda oluşturduğunuz hello Resource Manager şablonu kullanarak komut toodeploy Data Factory varlıklarını aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-173">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="8cbe6-174">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="8cbe6-174">Monitor pipeline</span></span>

1. <span data-ttu-id="8cbe6-175">İçinde toohello oturum [Azure portal](https://portal.azure.com) Azure hesabınızı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-175">Log in toohello [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="8cbe6-176">Tıklatın **veri fabrikaları** hello sol menü (veya) tıklatın **daha fazla hizmet** tıklatıp **veri fabrikaları** altında **INTELLİGENCE + ANALİZ** Kategori.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-176">Click **Data factories** on hello left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![Veri fabrikaları menüsü](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="8cbe6-178">Merhaba, **veri fabrikaları** sayfasında, aramak ve veri fabrikanızı (AzureBlobToAzureSQLDatabaseDF) bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-178">In hello **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span></span> 
   
    ![Veri fabrikası arama](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="8cbe6-180">Azure veri fabrikanıza tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-180">Click your Azure data factory.</span></span> <span data-ttu-id="8cbe6-181">Merhaba veri fabrikası için hello giriş sayfasına bakın.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-181">You see hello home page for hello data factory.</span></span>
   
    ![Veri fabrikasının giriş sayfası](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. <span data-ttu-id="8cbe6-183">Makalesindeki yönergeleri izleyin [veri kümelerini ve ardışık düzen izleme](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello ardışık düzen ve veri kümeleri Bu öğreticide oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-183">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="8cbe6-184">Visual Studio şu anda Data Factory işlem hatlarını izlemeyi desteklememektedir.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-184">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span>
7. <span data-ttu-id="8cbe6-185">Bir dilim hello olduğunda **hazır** durum, hello veri kopyalanan toohello olduğunu doğrulayın **emp** hello Azure SQL veritabanı tablosunda.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-185">When a slice is in hello **Ready** state, verify that hello data is copied toohello **emp** table in hello Azure SQL database.</span></span>


<span data-ttu-id="8cbe6-186">Nasıl toouse Azure portal dikey penceresi toomonitor ardışık düzen ve veri kümeleri, bu öğreticide oluşturduğunuz daha fazla bilgi için bkz: [veri kümelerini ve ardışık düzen izleme](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="8cbe6-186">For more information on how toouse Azure portal blades toomonitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span></span>

<span data-ttu-id="8cbe6-187">Toouse hello İzleyici & Yönet uygulama toomonitor verilerinizi nasıl ardışık düzenleri daha fazla bilgi için bkz: [İzleyicisi ve izleme uygulaması kullanarak Azure Data Factory işlem hatlarını yönetmek](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="8cbe6-187">For more information on how toouse hello Monitor & Manage application toomonitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span></span>

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="8cbe6-188">Data Factory varlıklarını hello şablonunda</span><span class="sxs-lookup"><span data-stu-id="8cbe6-188">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="8cbe6-189">Veri fabrikası tanımlama</span><span class="sxs-lookup"><span data-stu-id="8cbe6-189">Define data factory</span></span>
<span data-ttu-id="8cbe6-190">Hello örnek aşağıdaki gösterildiği gibi bir veri fabrikası hello Resource Manager şablonunda tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="8cbe6-190">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="8cbe6-191">Merhaba dataFactoryName olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="8cbe6-191">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="8cbe6-192">Merhaba kaynak grup kimliğine göre benzersiz bir dize değil</span><span class="sxs-lookup"><span data-stu-id="8cbe6-192">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="8cbe6-193">Data Factory varlıklarını tanımlama</span><span class="sxs-lookup"><span data-stu-id="8cbe6-193">Defining Data Factory entities</span></span>
<span data-ttu-id="8cbe6-194">Merhaba aşağıdaki Data Factory varlıklarını hello JSON şablonunda tanımlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="8cbe6-194">hello following Data Factory entities are defined in hello JSON template:</span></span> 

1. [<span data-ttu-id="8cbe6-195">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="8cbe6-195">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="8cbe6-196">Azure SQL bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="8cbe6-196">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="8cbe6-197">Azure blob veri kümesi</span><span class="sxs-lookup"><span data-stu-id="8cbe6-197">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="8cbe6-198">Azure SQL veri kümesi</span><span class="sxs-lookup"><span data-stu-id="8cbe6-198">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="8cbe6-199">Kopyalama etkinliği içeren bir veri işlem hattı</span><span class="sxs-lookup"><span data-stu-id="8cbe6-199">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="8cbe6-200">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="8cbe6-200">Azure Storage linked service</span></span>
<span data-ttu-id="8cbe6-201">Merhaba AzureStorageLinkedService Azure depolama hesabı toohello veri fabrikanıza bağlar.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-201">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="8cbe6-202">Bir kapsayıcı oluşturulur ve veri toothis depolama hesabı bir parçası olarak yüklenen [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="8cbe6-202">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="8cbe6-203">Bu bölümde hello adı ve Azure depolama hesabınızın anahtarı belirtin.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-203">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="8cbe6-204">Bkz: [Azure depolama bağlantılı hizmeti](data-factory-azure-blob-connector.md#azure-storage-linked-service) JSON kullanılan özellikler toodefine hakkında ayrıntılı bilgi için bir Azure Storage bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-204">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

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

<span data-ttu-id="8cbe6-205">Merhaba connectionString hello storageAccountName ve storageAccountKey parametrelerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-205">hello connectionString uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="8cbe6-206">bir yapılandırma dosyası kullanarak geçirilen bu parametrelerin değerlerini Hello.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-206">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="8cbe6-207">Merhaba tanımını değişkenleri de kullanır: azureStroageLinkedService ve dataFactoryName hello şablonda tanımlı.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-207">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="8cbe6-208">Azure SQL Veritabanı bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="8cbe6-208">Azure SQL Database linked service</span></span>
<span data-ttu-id="8cbe6-209">AzureSqlLinkedService Azure SQL veritabanı toohello veri fabrikanıza bağlar.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-209">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="8cbe6-210">Merhaba blob depolama biriminden kopyalanan hello veriler bu veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-210">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="8cbe6-211">Bu veritabanında hello emp tablosunda bir parçası olarak oluşturulan [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="8cbe6-211">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="8cbe6-212">Bu bölümde hello Azure SQL sunucu adı, veritabanı adı, kullanıcı adı ve parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-212">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="8cbe6-213">Bkz: [Azure SQL bağlı hizmeti](data-factory-azure-sql-connector.md#linked-service-properties) JSON kullanılan özellikler toodefine hakkındaki ayrıntılar için hizmeti bir Azure SQL bağlı.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-213">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>  

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

<span data-ttu-id="8cbe6-214">Merhaba connectionString sqlsunucusuadı, databaseName, sqlServerUserName ve bir yapılandırma dosyası kullanarak değerleri geçirilen sqlServerPassword parametreleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-214">hello connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="8cbe6-215">Merhaba tanımını da hello şablondan değişkenleri aşağıdaki hello kullanır: azureSqlLinkedServiceName, dataFactoryName.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-215">hello definition also uses hello following variables from hello template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="8cbe6-216">Azure blob veri kümesi</span><span class="sxs-lookup"><span data-stu-id="8cbe6-216">Azure blob dataset</span></span>
<span data-ttu-id="8cbe6-217">Hello Azure depolama bağlı hizmeti çalışma zamanı tooconnect tooyour Azure depolama hesabı Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-217">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="8cbe6-218">Azure blob veri kümesi tanımında blob kapsayıcı, klasör ve hello giriş verisi içeren dosya adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-218">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="8cbe6-219">Bkz: [Azure Blob veri kümesi özellikleri](data-factory-azure-blob-connector.md#dataset-properties) JSON kullanılan özellikler toodefine bir Azure Blob dataset hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-219">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

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

#### <a name="azure-sql-dataset"></a><span data-ttu-id="8cbe6-220">Azure SQL veri kümesi</span><span class="sxs-lookup"><span data-stu-id="8cbe6-220">Azure SQL dataset</span></span>
<span data-ttu-id="8cbe6-221">Hello Azure Blob depolama alanından kopyalanan hello verilerini tutan hello Azure SQL veritabanında hello Merhaba tablonun adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-221">You specify hello name of hello table in hello Azure SQL database that holds hello copied data from hello Azure Blob storage.</span></span> <span data-ttu-id="8cbe6-222">Bkz: [Azure SQL veri kümesi özellikleri](data-factory-azure-sql-connector.md#dataset-properties) JSON kullanılan özellikler toodefine bir Azure SQL veri kümesini hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-222">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure SQL dataset.</span></span> 

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

#### <a name="data-pipeline"></a><span data-ttu-id="8cbe6-223">Veri işlem hattı</span><span class="sxs-lookup"><span data-stu-id="8cbe6-223">Data pipeline</span></span>
<span data-ttu-id="8cbe6-224">Hello Azure blob dataset toohello Azure SQL veri kümesinden alınan verileri kopyalayan bir işlem hattı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-224">You define a pipeline that copies data from hello Azure blob dataset toohello Azure SQL dataset.</span></span> <span data-ttu-id="8cbe6-225">Bkz: [ardışık düzen JSON](data-factory-create-pipelines.md#pipeline-json) JSON kullanılan öğeleri toodefine bu örnekteki işlem hattı açıklamaları için.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-225">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

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
              "description": "Copy data frm Azure blob tooAzure SQL",
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

## <a name="reuse-hello-template"></a><span data-ttu-id="8cbe6-226">Merhaba şablonu yeniden</span><span class="sxs-lookup"><span data-stu-id="8cbe6-226">Reuse hello template</span></span>
<span data-ttu-id="8cbe6-227">Merhaba öğreticide Data Factory varlıklarını ve parametreleri için değerleri geçirme için bir şablon tanımlamak için bir şablon oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-227">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="8cbe6-228">Merhaba ardışık düzen parametreleri aracılığıyla belirtilen Azure depolama hesabı tooan Azure SQL veritabanına veri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-228">hello pipeline copies data from an Azure Storage account tooan Azure SQL database specified via parameters.</span></span> <span data-ttu-id="8cbe6-229">toouse Merhaba aynı şablon toodeploy Data Factory varlıkları toodifferent ortamları, her ortam için bir parametre dosyası oluşturabilir ve toothat ortam dağıtırken kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-229">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="8cbe6-230">Örnek:</span><span class="sxs-lookup"><span data-stu-id="8cbe6-230">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="8cbe6-231">Hello ilk komut hello geliştirme ortamı için parametre dosyası kullanır, ikinci bir hello için test ortamı ve hello üretim ortamı için üçüncü bir hello dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-231">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="8cbe6-232">Merhaba şablonu tooperform yeniden kullanabilir yinelenen görevler.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-232">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="8cbe6-233">Örneğin, birçok veri fabrikaları biriyle toocreate gerekir veya aynı uygulamak daha fazla ardışık düzen hello mantığı ancak her veri fabrikası farklı depolama ve SQL veritabanı hesapları kullanır.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-233">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="8cbe6-234">Bu senaryoda, kullandığınız hello aynı şablonu hello toocreate veri fabrikaları farklı parametre ile aynı ortamda (geliştirme, test veya üretim) dosyaları.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-234">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="8cbe6-235">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8cbe6-235">Next steps</span></span>
<span data-ttu-id="8cbe6-236">Bu öğreticide, bir kopyalama işleminde kaynak veri deposu olarak Azure blob depolama alanını ve hedef veri deposu olarak Azure SQL veritabanını kullandınız.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-236">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="8cbe6-237">Merhaba aşağıdaki tabloda kaynakları ve hedefleri hello kopyalama etkinliği tarafından desteklenen veri depoları listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8cbe6-237">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="8cbe6-238">nasıl bir veri öğesine/öğesinden toocopy veri deposu hakkında toolearn hello veri deposu hello tablosundaki hello bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8cbe6-238">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
