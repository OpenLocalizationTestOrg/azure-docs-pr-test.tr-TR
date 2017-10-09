---
title: "Veri Fabrikası'nda aaaUse Resource Manager şablonları | Microsoft Docs"
description: "Bilgi nasıl toocreate ve kullanım Azure Resource Manager şablonları toocreate Data Factory varlıklarını."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: 
ms.assetid: 37724021-f55f-4e85-9206-6d4a48bda3d8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 60d5dbd29494420006aed6d5bd9a10a63c36bec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-templates-toocreate-azure-data-factory-entities"></a><span data-ttu-id="e1ebd-103">Şablonları toocreate Azure Data Factory varlıklarını kullanın</span><span class="sxs-lookup"><span data-stu-id="e1ebd-103">Use templates toocreate Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="e1ebd-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e1ebd-104">Overview</span></span>
<span data-ttu-id="e1ebd-105">Azure Data Factory veri tümleştirme ihtiyaçlarınız için kullanılırken kendinizi bulabilirsiniz yeniden hello aynı düzeni farklı ortamlar genelinde veya hello uygulama aynı art arda hello içinde aynı görev çözümü.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing hello same pattern across different environments or implementing hello same task repetitively within hello same solution.</span></span> <span data-ttu-id="e1ebd-106">Şablonları uygulamak ve bu senaryolar kolay bir şekilde yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="e1ebd-107">Azure Data Factory şablonlarında yeniden kullanılırlığı ve yineleme gerektiren senaryolar için idealdir.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="e1ebd-108">Bir kuruluş 10 üretim bitkilerin Merhaba dünya genelindeki sahip olduğu hello durumu göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-108">Consider hello situation where an organization has 10 manufacturing plants across hello world.</span></span> <span data-ttu-id="e1ebd-109">Her tesis Hello günlükleri ayrı şirket içi SQL Server veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-109">hello logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="e1ebd-110">Merhaba şirket toobuild geçici analizi için tek bir veri ambarına hello bulutta ister.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-110">hello company wants toobuild a single data warehouse in hello cloud for ad-hoc analytics.</span></span> <span data-ttu-id="e1ebd-111">Ayrıca toohave istemektedir hello aynı mantığı ancak geliştirme, test ve üretim ortamları için farklı yapılandırmaları.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-111">It also wants toohave hello same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="e1ebd-112">Bu durumda, bir görevin yinelenen toobe gereken içinde hello aynı ortam, ancak arasında farklı değerleri olan her üretim tesis için 10 veri fabrikaları hello.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-112">In this case, a task needs toobe repeated within hello same environment, but with different values across hello 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="e1ebd-113">Uygulamada **yineleme** mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="e1ebd-114">Şablon bu genel akış hello soyutlaması sağlar (diğer bir deyişle, sahip hello aynı etkinlikleri her veri fabrikasında ardışık düzenleri), ancak her üretim tesis için ayrı bir parametre dosyası kullanır.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-114">Templating allows hello abstraction of this generic flow (that is, pipelines having hello same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="e1ebd-115">Merhaba kuruluş toodeploy bu 10 veri fabrikaları birden çok kez farklı ortamlar genelinde istediği gibi Ayrıca, şablonları bu kullanabilirsiniz **yeniden kullanılırlığı** geliştirme için ayrı parametre dosyaları aynı kullanarak test, ve üretim ortamlarında.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-115">Furthermore, as hello organization wants toodeploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="e1ebd-116">Azure Resource Manager ile şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1ebd-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="e1ebd-117">[Azure Resource Manager şablonları](../azure-resource-manager/resource-group-overview.md#template-deployment) mükemmel şekilde tooachieve şablon Azure veri fabrikası'nda şunlardır.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way tooachieve templating in Azure Data Factory.</span></span> <span data-ttu-id="e1ebd-118">Resource Manager şablonları bir JSON dosyası aracılığıyla hello altyapısı ve Azure çözümünüzü yapılandırmasını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-118">Resource Manager templates define hello infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="e1ebd-119">Azure Resource Manager şablonları tüm/çoğu Azure hizmetler ile çalışmak için yaygın olarak kullanılabilir tooeasily Azure varlıklarınızın tüm kaynakları yönetin.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used tooeasily manage all resources of your Azure assets.</span></span> <span data-ttu-id="e1ebd-120">Bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md) toolearn hakkında daha fazla bilgi hello Resource Manager şablonları genel olarak.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn more about hello Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="e1ebd-121">Öğreticiler</span><span class="sxs-lookup"><span data-stu-id="e1ebd-121">Tutorials</span></span>
<span data-ttu-id="e1ebd-122">Resource Manager şablonları kullanarak öğreticileri için adım adım yönergeler toocreate Data Factory varlıklarını aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="e1ebd-122">See hello following tutorials for step-by-step instructions toocreate Data Factory entities by using Resource Manager templates:</span></span>

* [<span data-ttu-id="e1ebd-123">Öğretici: Azure Resource Manager şablonu kullanarak bir ardışık düzen toocopy veri oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1ebd-123">Tutorial: Create a pipeline toocopy data by using Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="e1ebd-124">Öğretici: Azure Resource Manager şablonu kullanarak bir ardışık düzen tooprocess veri oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1ebd-124">Tutorial: Create a pipeline tooprocess data by using Azure Resource Manager template</span></span>](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="e1ebd-125">Veri Fabrikası şablonları github'da</span><span class="sxs-lookup"><span data-stu-id="e1ebd-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="e1ebd-126">Github'da Azure hızlı başlangıç şablonları aşağıdaki hello gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="e1ebd-126">Check out hello following Azure quick start templates on GitHub:</span></span>

* [<span data-ttu-id="e1ebd-127">Veri Fabrikası toocopy verileri Azure Blob Storage tooAzure SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1ebd-127">Create a Data factory toocopy data from Azure Blob Storage tooAzure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [<span data-ttu-id="e1ebd-128">Azure Hdınsight kümesinde Hive etkinliği ile bir veri fabrikası oluşturun</span><span class="sxs-lookup"><span data-stu-id="e1ebd-128">Create a Data factory with Hive activity on Azure HDInsight cluster</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [<span data-ttu-id="e1ebd-129">Veri Fabrikası toocopy veri Salesforce tooAzure Bloblarından oluşturma</span><span class="sxs-lookup"><span data-stu-id="e1ebd-129">Create a Data factory toocopy data from Salesforce tooAzure Blobs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [<span data-ttu-id="e1ebd-130">Etkinlikler zincir bir veri fabrikası oluşturun: verileri bir FTP sunucusundan kopyalar tooAzure BLOB'ları, bir isteğe bağlı Hdınsight kümesi tootransform hello veriler üzerinde bir hive betiği çağırır ve sonucu Azure SQL veritabanına kopyalar</span><span class="sxs-lookup"><span data-stu-id="e1ebd-130">Create a Data factory that chains activities: copies data from an FTP server tooAzure Blobs, invokes a hive script on an on-demand HDInsight cluster tootransform hello data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="e1ebd-131">Azure Data Factory şablonlarınızı adresindeki boş tooshare eşitleyerek [Azure Hızlı Başlangıç](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="e1ebd-131">Feel free tooshare your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="e1ebd-132">Toohello başvuran [katkı Kılavuzu](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) bu havuzda paylaşılan şablonları geliştirme sırasında.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-132">Refer toohello [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="e1ebd-133">Aşağıdaki bölümlerde hello Veri Fabrikası Kaynakları bir Resource Manager şablonunda tanımlama hakkında ayrıntılı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-133">hello following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="e1ebd-134">Veri Fabrikası Kaynakları Tanımlama</span><span class="sxs-lookup"><span data-stu-id="e1ebd-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="e1ebd-135">Veri Fabrikası tanımlamak için üst düzey şablon hello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e1ebd-135">hello top-level template for defining a data factory is:</span></span>

```JSON
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
    { "type": "linkedservices",
        ...
    },
    {"type": "datasets",
        ...
    },
    {"type": "dataPipelines",
        ...
    }
}
```

### <a name="define-data-factory"></a><span data-ttu-id="e1ebd-136">Veri fabrikası tanımlama</span><span class="sxs-lookup"><span data-stu-id="e1ebd-136">Define data factory</span></span>
<span data-ttu-id="e1ebd-137">Hello örnek aşağıdaki gösterildiği gibi bir veri fabrikası hello Resource Manager şablonunda tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="e1ebd-137">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="e1ebd-138">Merhaba dataFactoryName "değişkenler" olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="e1ebd-138">hello dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="e1ebd-139">Bağlı hizmetler tanımlayın</span><span class="sxs-lookup"><span data-stu-id="e1ebd-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="e1ebd-140">Bkz: [depolama bağlantılı hizmeti](data-factory-azure-blob-connector.md#azure-storage-linked-service) veya [işlem bağlı Hizmetleri](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) hello belirli bağlantılı hizmet hello JSON özellikleri hakkında ayrıntılı bilgi için toodeploy istiyor.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about hello JSON properties for hello specific linked service you wish toodeploy.</span></span> <span data-ttu-id="e1ebd-141">Merhaba "dependsOn" parametresi hello karşılık gelen veri fabrikasının adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-141">hello “dependsOn” parameter specifies name of hello corresponding data factory.</span></span> <span data-ttu-id="e1ebd-142">Azure Storage için bağlı hizmet tanımlama örneği aşağıdaki JSON tanımını hello gösterilir:</span><span class="sxs-lookup"><span data-stu-id="e1ebd-142">An example of defining a linked service for Azure Storage is shown in hello following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="e1ebd-143">Veri kümelerini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="e1ebd-143">Define datasets</span></span>

```JSON
"type": "datasets",
"name": "[variables('<myDatasetName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<myDatasetLinkedServiceName>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    ...
}
```
<span data-ttu-id="e1ebd-144">Çok başvuran[desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) hello hello belirli dataset türü için JSON özellikleri hakkında ayrıntılı bilgi için toodeploy istiyor.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-144">Refer too[Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about hello JSON properties for hello specific dataset type you wish toodeploy.</span></span> <span data-ttu-id="e1ebd-145">Not hello "dependsOn" parametresi hello karşılık gelen verilerin adını belirtir Fabrika ve depolama bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-145">Note hello “dependsOn” parameter specifies name of hello corresponding data factory and storage linked service.</span></span> <span data-ttu-id="e1ebd-146">Azure blob depolama dataset türünü tanımlayan bir örnek, JSON tanımını izleyen hello gösterilir:</span><span class="sxs-lookup"><span data-stu-id="e1ebd-146">An example of defining dataset type of Azure blob storage is shown in hello following JSON definition:</span></span>

```JSON
"type": "datasets",
"name": "[variables('storageDataset')]",
"dependsOn": [
    "[variables('dataFactoryName')]",
    "[variables('storageLinkedServiceName')]"
],
"apiVersion": "2015-10-01",
"properties": {
"type": "AzureBlob",
"linkedServiceName": "[variables('storageLinkedServiceName')]",
"typeProperties": {
    "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
    "fileName": "[parameters('sourceBlobName')]",
    "format": {
        "type": "TextFormat"
    }
},
"availability": {
    "frequency": "Hour",
    "interval": 1
}
```

### <a name="define-pipelines"></a><span data-ttu-id="e1ebd-147">Ardışık Düzen tanımlayın</span><span class="sxs-lookup"><span data-stu-id="e1ebd-147">Define pipelines</span></span>

```JSON
"type": "dataPipelines",
"name": "[variables('<mypipelineName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<inputDatasetLinkedServiceName>')]",
    "[variables('<outputDatasetLinkedServiceName>')]",
    "[variables('<inputDataset>')]",
    "[variables('<outputDataset>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    activities: {
        ...
    }
}
```

<span data-ttu-id="e1ebd-148">Çok başvuran[ardışık düzen tanımlama](data-factory-create-pipelines.md#pipeline-json) belirli ardışık düzen ve etkinlikleri tanımlamak için hello JSON özellikleri hakkında ayrıntılı hello için toodeploy istiyor.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-148">Refer too[defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about hello JSON properties for defining hello specific pipeline and activities you wish toodeploy.</span></span> <span data-ttu-id="e1ebd-149">Not hello "dependsOn" parametresi hello veri fabrikasının adı ve karşılık gelen bağlı hizmetler veya veri kümeleri belirtir.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-149">Note hello “dependsOn” parameter specifies name of hello data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="e1ebd-150">JSON parçacığı aşağıdaki hello Azure Blob Storage tooAzure SQL veritabanı ' verileri kopyalayan bir işlem hattı örneği gösterilir:</span><span class="sxs-lookup"><span data-stu-id="e1ebd-150">An example of a pipeline that copies data from Azure Blob Storage tooAzure SQL Database is shown in hello following JSON snippet:</span></span>

```JSON
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
    "start": "2016-10-03T00:00:00Z",
    "end": "2016-10-04T00:00:00Z"
}
```
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="e1ebd-151">Veri Fabrikası şablon kümesini parametreleştirme</span><span class="sxs-lookup"><span data-stu-id="e1ebd-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="e1ebd-152">Kümesini parametreleştirme en iyi uygulamalar için bkz: [en iyi uygulamalar Azure Resource Manager şablonları oluşturmak için](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) makalesi.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="e1ebd-153">Özellikle değişkenleri yerine kullanılabilir genel olarak, parametre kullanımı, en aza.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="e1ebd-154">Yalnızca senaryoları aşağıdaki hello parametrelerinde sağlar:</span><span class="sxs-lookup"><span data-stu-id="e1ebd-154">Only provide parameters in hello following scenarios:</span></span>

* <span data-ttu-id="e1ebd-155">Ayarlar ortamı tarafından değişir (örnek: geliştirme, test ve üretim)</span><span class="sxs-lookup"><span data-stu-id="e1ebd-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="e1ebd-156">Gizli (parolalar gibi)</span><span class="sxs-lookup"><span data-stu-id="e1ebd-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="e1ebd-157">Gelen toopull gizli gerekiyorsa [Azure anahtar kasası](../key-vault/key-vault-get-started.md) şablonları kullanarak Azure Data Factory varlıklarını dağıtırken hello belirtin **anahtar kasası** ve **gizli anahtar adı** gösterildiği gibi Örnek hello:</span><span class="sxs-lookup"><span data-stu-id="e1ebd-157">If you need toopull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify hello **key vault** and **secret name** as shown in hello following example:</span></span>

```JSON
"parameters": {
    "storageAccountKey": {
        "reference": {
            "keyVault": {
                "id":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.KeyVault/vaults/<keyVaultName>",
             },
            "secretName": "<secretName>"
           },
       },
       ...
}
```

> [!NOTE]
> <span data-ttu-id="e1ebd-158">Mevcut veri fabrikaları şablonları verme şu anda henüz desteklenmiyor olsa da, hello çalışır durumdur.</span><span class="sxs-lookup"><span data-stu-id="e1ebd-158">While exporting templates for existing data factories is currently not yet supported, it is in hello works.</span></span>
>
>
