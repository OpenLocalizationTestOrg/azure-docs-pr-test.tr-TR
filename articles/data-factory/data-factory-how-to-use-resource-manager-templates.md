---
title: "Veri Fabrikası'nda kullanmak Resource Manager şablonları | Microsoft Docs"
description: "Oluşturma ve Data Factory varlıklarını oluşturmak için Azure Resource Manager şablonlarını kullanma hakkında bilgi edinin."
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
ms.openlocfilehash: c3ea2c047434b5b5495f0ce85be9376a502e4962
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-templates-to-create-azure-data-factory-entities"></a><span data-ttu-id="226e0-103">Azure Data Factory varlıklarını oluşturmak için şablon kullanın</span><span class="sxs-lookup"><span data-stu-id="226e0-103">Use templates to create Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="226e0-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="226e0-104">Overview</span></span>
<span data-ttu-id="226e0-105">Kendinizi bulabilirsiniz veri tümleştirme ihtiyaçlarınız için Azure Data Factory kullanırken farklı ortamlar veya aynı çözüm içinde art arda aynı görevi uygulama arasında aynı düzeni yeniden kullanma.</span><span class="sxs-lookup"><span data-stu-id="226e0-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing the same pattern across different environments or implementing the same task repetitively within the same solution.</span></span> <span data-ttu-id="226e0-106">Şablonları uygulamak ve bu senaryolar kolay bir şekilde yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="226e0-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="226e0-107">Azure Data Factory şablonlarında yeniden kullanılırlığı ve yineleme gerektiren senaryolar için idealdir.</span><span class="sxs-lookup"><span data-stu-id="226e0-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="226e0-108">Bir kuruluş dünya genelindeki 10 üretim bitkilerin sahip olduğu durum göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="226e0-108">Consider the situation where an organization has 10 manufacturing plants across the world.</span></span> <span data-ttu-id="226e0-109">Her tesis günlüklerinden ayrı şirket içi SQL Server veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="226e0-109">The logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="226e0-110">Tek bir veri ambarına geçici analiz için bulutta oluşturmak şirket ister.</span><span class="sxs-lookup"><span data-stu-id="226e0-110">The company wants to build a single data warehouse in the cloud for ad-hoc analytics.</span></span> <span data-ttu-id="226e0-111">Ayrıca aynı mantığı ancak geliştirme, test ve üretim ortamları için farklı yapılandırmalara sahip olmasını istiyor.</span><span class="sxs-lookup"><span data-stu-id="226e0-111">It also wants to have the same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="226e0-112">Bu durumda, bir görev aynı ortamda ancak farklı değerleri olan her üretim tesis için 10 veri fabrikaları arasında yinelenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="226e0-112">In this case, a task needs to be repeated within the same environment, but with different values across the 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="226e0-113">Uygulamada **yineleme** mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="226e0-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="226e0-114">Şablon bu genel akış (diğer bir deyişle, her veri fabrikası aynı etkinlikleri sahip ardışık) soyutlaması sağlar, ancak her üretim tesis için ayrı bir parametre dosyası kullanır.</span><span class="sxs-lookup"><span data-stu-id="226e0-114">Templating allows the abstraction of this generic flow (that is, pipelines having the same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="226e0-115">Bu 10 veri fabrikaları farklı ortamlar genelinde birden çok kez dağıtmak kuruluş istediği gibi Ayrıca, şablonları bu kullanabilirsiniz **yeniden kullanılırlığı** geliştirme, test ve üretim ortamları için ayrı parametre dosyaları aynı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="226e0-115">Furthermore, as the organization wants to deploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="226e0-116">Azure Resource Manager ile şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="226e0-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="226e0-117">[Azure Resource Manager şablonları](../azure-resource-manager/resource-group-overview.md#template-deployment) Azure veri fabrikası'nda şablon elde etmek için kullanışlı bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="226e0-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way to achieve templating in Azure Data Factory.</span></span> <span data-ttu-id="226e0-118">Resource Manager şablonları bir JSON dosyası aracılığıyla altyapısı ve Azure çözümünüzü yapılandırmasını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="226e0-118">Resource Manager templates define the infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="226e0-119">Azure Resource Manager şablonları tüm/çoğu Azure hizmetler ile çalışmak için bu yaygın olarak kolayca Azure varlıklarınızın tüm kaynakları yönetmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="226e0-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used to easily manage all resources of your Azure assets.</span></span> <span data-ttu-id="226e0-120">Bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md) Resource Manager şablonları hakkında daha fazla genel bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="226e0-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn more about the Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="226e0-121">Öğreticiler</span><span class="sxs-lookup"><span data-stu-id="226e0-121">Tutorials</span></span>
<span data-ttu-id="226e0-122">Aşağıdaki öğreticileri Resource Manager şablonları kullanarak Data Factory varlıklarını oluşturmak adım adım yönergeler için bkz:</span><span class="sxs-lookup"><span data-stu-id="226e0-122">See the following tutorials for step-by-step instructions to create Data Factory entities by using Resource Manager templates:</span></span>

* [<span data-ttu-id="226e0-123">Öğretici: Azure Resource Manager şablonu kullanarak veri kopyalamak için bir işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="226e0-123">Tutorial: Create a pipeline to copy data by using Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="226e0-124">Öğretici: Azure Resource Manager şablonu kullanarak verileri işlemek için bir işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="226e0-124">Tutorial: Create a pipeline to process data by using Azure Resource Manager template</span></span>](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="226e0-125">Veri Fabrikası şablonları github'da</span><span class="sxs-lookup"><span data-stu-id="226e0-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="226e0-126">Github'da aşağıdaki Azure hızlı başlangıç şablonlarını gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="226e0-126">Check out the following Azure quick start templates on GitHub:</span></span>

* [<span data-ttu-id="226e0-127">Verileri Azure Blob depolama alanından Azure SQL veritabanına kopyalamak için bir veri fabrikası oluşturun</span><span class="sxs-lookup"><span data-stu-id="226e0-127">Create a Data factory to copy data from Azure Blob Storage to Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [<span data-ttu-id="226e0-128">Azure Hdınsight kümesinde Hive etkinliği ile bir veri fabrikası oluşturun</span><span class="sxs-lookup"><span data-stu-id="226e0-128">Create a Data factory with Hive activity on Azure HDInsight cluster</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [<span data-ttu-id="226e0-129">Azure BLOB'larını Salesforce verileri kopyalamak için bir veri fabrikası oluşturun</span><span class="sxs-lookup"><span data-stu-id="226e0-129">Create a Data factory to copy data from Salesforce to Azure Blobs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [<span data-ttu-id="226e0-130">Etkinlikler zincir bir veri fabrikası oluşturun: verileri Azure BLOB'larını bir FTP sunucusundan kopyalar, verileri dönüştürmek için isteğe bağlı Hdınsight kümesinde bir hive betiği çağırır ve sonucu Azure SQL veritabanına kopyalar</span><span class="sxs-lookup"><span data-stu-id="226e0-130">Create a Data factory that chains activities: copies data from an FTP server to Azure Blobs, invokes a hive script on an on-demand HDInsight cluster to transform the data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="226e0-131">Azure Data Factory şablonlarınızı paylaşmak çekinmeyin [Azure Hızlı Başlangıç](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="226e0-131">Feel free to share your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="226e0-132">Başvurmak [katkı Kılavuzu](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) bu havuzda paylaşılan şablonları geliştirme sırasında.</span><span class="sxs-lookup"><span data-stu-id="226e0-132">Refer to the [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="226e0-133">Aşağıdaki bölümler, Veri Fabrikası Kaynakları bir Resource Manager şablonunda tanımlama hakkında ayrıntılı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="226e0-133">The following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="226e0-134">Veri Fabrikası Kaynakları Tanımlama</span><span class="sxs-lookup"><span data-stu-id="226e0-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="226e0-135">Veri Fabrikası tanımlamak için üst düzey şablon şöyledir:</span><span class="sxs-lookup"><span data-stu-id="226e0-135">The top-level template for defining a data factory is:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="226e0-136">Veri fabrikası tanımlama</span><span class="sxs-lookup"><span data-stu-id="226e0-136">Define data factory</span></span>
<span data-ttu-id="226e0-137">Resource Manager şablonunda bir veri fabrikasını aşağıdaki örnekte gösterildiği gibi tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="226e0-137">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="226e0-138">DataFactoryName "değişkenler" olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="226e0-138">The dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="226e0-139">Bağlı hizmetler tanımlayın</span><span class="sxs-lookup"><span data-stu-id="226e0-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="226e0-140">Bkz: [depolama bağlantılı hizmeti](data-factory-azure-blob-connector.md#azure-storage-linked-service) veya [işlem bağlı Hizmetleri](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) dağıtmak istediğiniz belirli bağlantılı hizmeti için JSON özellikleri hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="226e0-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about the JSON properties for the specific linked service you wish to deploy.</span></span> <span data-ttu-id="226e0-141">"DependsOn" parametresi karşılık gelen veri fabrikasının adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="226e0-141">The “dependsOn” parameter specifies name of the corresponding data factory.</span></span> <span data-ttu-id="226e0-142">Azure Storage için bağlı hizmet tanımlama örneği aşağıdaki JSON tanımında gösterilir:</span><span class="sxs-lookup"><span data-stu-id="226e0-142">An example of defining a linked service for Azure Storage is shown in the following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="226e0-143">Veri kümelerini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="226e0-143">Define datasets</span></span>

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
<span data-ttu-id="226e0-144">Başvurmak [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) dağıtmak istediğiniz belirli dataset türü için JSON özellikleri hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="226e0-144">Refer to [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about the JSON properties for the specific dataset type you wish to deploy.</span></span> <span data-ttu-id="226e0-145">Bağlantılı hizmetinin Not "dependsOn" parametresi depolama alanını ve karşılık gelen veri fabrikası adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="226e0-145">Note the “dependsOn” parameter specifies name of the corresponding data factory and storage linked service.</span></span> <span data-ttu-id="226e0-146">Azure blob depolama dataset türünü tanımlayan bir örneği aşağıdaki JSON tanımında gösterilir:</span><span class="sxs-lookup"><span data-stu-id="226e0-146">An example of defining dataset type of Azure blob storage is shown in the following JSON definition:</span></span>

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

### <a name="define-pipelines"></a><span data-ttu-id="226e0-147">Ardışık Düzen tanımlayın</span><span class="sxs-lookup"><span data-stu-id="226e0-147">Define pipelines</span></span>

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

<span data-ttu-id="226e0-148">Başvurmak [ardışık düzen tanımlama](data-factory-create-pipelines.md#pipeline-json) belirli ardışık düzen ve dağıtmak istediğiniz etkinlikleri tanımlamak için JSON özellikleri hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="226e0-148">Refer to [defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about the JSON properties for defining the specific pipeline and activities you wish to deploy.</span></span> <span data-ttu-id="226e0-149">Veri Fabrikası adı "dependsOn" parametresi belirtir ve ilgili tüm hizmetleri veya veri kümeleri bağlı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="226e0-149">Note the “dependsOn” parameter specifies name of the data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="226e0-150">Azure Blob depolama alanından Azure SQL veritabanına verileri kopyalayan bir işlem hattı örneği aşağıdaki JSON parçacığında gösterilir:</span><span class="sxs-lookup"><span data-stu-id="226e0-150">An example of a pipeline that copies data from Azure Blob Storage to Azure SQL Database is shown in the following JSON snippet:</span></span>

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
    "start": "2016-10-03T00:00:00Z",
    "end": "2016-10-04T00:00:00Z"
}
```
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="226e0-151">Veri Fabrikası şablon kümesini parametreleştirme</span><span class="sxs-lookup"><span data-stu-id="226e0-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="226e0-152">Kümesini parametreleştirme en iyi uygulamalar için bkz: [en iyi uygulamalar Azure Resource Manager şablonları oluşturmak için](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) makalesi.</span><span class="sxs-lookup"><span data-stu-id="226e0-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="226e0-153">Özellikle değişkenleri yerine kullanılabilir genel olarak, parametre kullanımı, en aza.</span><span class="sxs-lookup"><span data-stu-id="226e0-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="226e0-154">Yalnızca aşağıdaki senaryolarda parametreler sağlar:</span><span class="sxs-lookup"><span data-stu-id="226e0-154">Only provide parameters in the following scenarios:</span></span>

* <span data-ttu-id="226e0-155">Ayarlar ortamı tarafından değişir (örnek: geliştirme, test ve üretim)</span><span class="sxs-lookup"><span data-stu-id="226e0-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="226e0-156">Gizli (parolalar gibi)</span><span class="sxs-lookup"><span data-stu-id="226e0-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="226e0-157">Gizli gelen çekme gerekiyorsa [Azure anahtar kasası](../key-vault/key-vault-get-started.md) şablonları kullanarak Azure Data Factory varlıklarını dağıtırken belirtin **anahtar kasası** ve **gizli anahtar adı** aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="226e0-157">If you need to pull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify the **key vault** and **secret name** as shown in the following example:</span></span>

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
> <span data-ttu-id="226e0-158">Mevcut veri fabrikaları şablonları verme şu anda henüz desteklenmiyor olsa da, çalışır durumdur.</span><span class="sxs-lookup"><span data-stu-id="226e0-158">While exporting templates for existing data factories is currently not yet supported, it is in the works.</span></span>
>
>
