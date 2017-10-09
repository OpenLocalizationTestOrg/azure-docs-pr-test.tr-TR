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
# <a name="use-templates-toocreate-azure-data-factory-entities"></a>Şablonları toocreate Azure Data Factory varlıklarını kullanın
## <a name="overview"></a>Genel Bakış
Azure Data Factory veri tümleştirme ihtiyaçlarınız için kullanılırken kendinizi bulabilirsiniz yeniden hello aynı düzeni farklı ortamlar genelinde veya hello uygulama aynı art arda hello içinde aynı görev çözümü. Şablonları uygulamak ve bu senaryolar kolay bir şekilde yönetmenize yardımcı olur. Azure Data Factory şablonlarında yeniden kullanılırlığı ve yineleme gerektiren senaryolar için idealdir.

Bir kuruluş 10 üretim bitkilerin Merhaba dünya genelindeki sahip olduğu hello durumu göz önünde bulundurun. Her tesis Hello günlükleri ayrı şirket içi SQL Server veritabanında depolanır. Merhaba şirket toobuild geçici analizi için tek bir veri ambarına hello bulutta ister. Ayrıca toohave istemektedir hello aynı mantığı ancak geliştirme, test ve üretim ortamları için farklı yapılandırmaları.

Bu durumda, bir görevin yinelenen toobe gereken içinde hello aynı ortam, ancak arasında farklı değerleri olan her üretim tesis için 10 veri fabrikaları hello. Uygulamada **yineleme** mevcuttur. Şablon bu genel akış hello soyutlaması sağlar (diğer bir deyişle, sahip hello aynı etkinlikleri her veri fabrikasında ardışık düzenleri), ancak her üretim tesis için ayrı bir parametre dosyası kullanır.

Merhaba kuruluş toodeploy bu 10 veri fabrikaları birden çok kez farklı ortamlar genelinde istediği gibi Ayrıca, şablonları bu kullanabilirsiniz **yeniden kullanılırlığı** geliştirme için ayrı parametre dosyaları aynı kullanarak test, ve üretim ortamlarında.

## <a name="templating-with-azure-resource-manager"></a>Azure Resource Manager ile şablonu oluşturma
[Azure Resource Manager şablonları](../azure-resource-manager/resource-group-overview.md#template-deployment) mükemmel şekilde tooachieve şablon Azure veri fabrikası'nda şunlardır. Resource Manager şablonları bir JSON dosyası aracılığıyla hello altyapısı ve Azure çözümünüzü yapılandırmasını tanımlayın. Azure Resource Manager şablonları tüm/çoğu Azure hizmetler ile çalışmak için yaygın olarak kullanılabilir tooeasily Azure varlıklarınızın tüm kaynakları yönetin. Bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md) toolearn hakkında daha fazla bilgi hello Resource Manager şablonları genel olarak.

## <a name="tutorials"></a>Öğreticiler
Resource Manager şablonları kullanarak öğreticileri için adım adım yönergeler toocreate Data Factory varlıklarını aşağıdaki hello bakın:

* [Öğretici: Azure Resource Manager şablonu kullanarak bir ardışık düzen toocopy veri oluşturma](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [Öğretici: Azure Resource Manager şablonu kullanarak bir ardışık düzen tooprocess veri oluşturma](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a>Veri Fabrikası şablonları github'da
Github'da Azure hızlı başlangıç şablonları aşağıdaki hello gözden geçirin:

* [Veri Fabrikası toocopy verileri Azure Blob Storage tooAzure SQL veritabanı oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [Azure Hdınsight kümesinde Hive etkinliği ile bir veri fabrikası oluşturun](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [Veri Fabrikası toocopy veri Salesforce tooAzure Bloblarından oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [Etkinlikler zincir bir veri fabrikası oluşturun: verileri bir FTP sunucusundan kopyalar tooAzure BLOB'ları, bir isteğe bağlı Hdınsight kümesi tootransform hello veriler üzerinde bir hive betiği çağırır ve sonucu Azure SQL veritabanına kopyalar](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

Azure Data Factory şablonlarınızı adresindeki boş tooshare eşitleyerek [Azure Hızlı Başlangıç](https://azure.microsoft.com/documentation/templates/). Toohello başvuran [katkı Kılavuzu](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) bu havuzda paylaşılan şablonları geliştirme sırasında.

Aşağıdaki bölümlerde hello Veri Fabrikası Kaynakları bir Resource Manager şablonunda tanımlama hakkında ayrıntılı bilgi sağlar.

## <a name="defining-data-factory-resources-in-templates"></a>Veri Fabrikası Kaynakları Tanımlama
Veri Fabrikası tanımlamak için üst düzey şablon hello şöyledir:

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

### <a name="define-data-factory"></a>Veri fabrikası tanımlama
Hello örnek aşağıdaki gösterildiği gibi bir veri fabrikası hello Resource Manager şablonunda tanımlayın:

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
Merhaba dataFactoryName "değişkenler" olarak tanımlanır:

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a>Bağlı hizmetler tanımlayın

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

Bkz: [depolama bağlantılı hizmeti](data-factory-azure-blob-connector.md#azure-storage-linked-service) veya [işlem bağlı Hizmetleri](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) hello belirli bağlantılı hizmet hello JSON özellikleri hakkında ayrıntılı bilgi için toodeploy istiyor. Merhaba "dependsOn" parametresi hello karşılık gelen veri fabrikasının adını belirtir. Azure Storage için bağlı hizmet tanımlama örneği aşağıdaki JSON tanımını hello gösterilir:

### <a name="define-datasets"></a>Veri kümelerini tanımlayın

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
Çok başvuran[desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) hello hello belirli dataset türü için JSON özellikleri hakkında ayrıntılı bilgi için toodeploy istiyor. Not hello "dependsOn" parametresi hello karşılık gelen verilerin adını belirtir Fabrika ve depolama bağlı hizmeti. Azure blob depolama dataset türünü tanımlayan bir örnek, JSON tanımını izleyen hello gösterilir:

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

### <a name="define-pipelines"></a>Ardışık Düzen tanımlayın

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

Çok başvuran[ardışık düzen tanımlama](data-factory-create-pipelines.md#pipeline-json) belirli ardışık düzen ve etkinlikleri tanımlamak için hello JSON özellikleri hakkında ayrıntılı hello için toodeploy istiyor. Not hello "dependsOn" parametresi hello veri fabrikasının adı ve karşılık gelen bağlı hizmetler veya veri kümeleri belirtir. JSON parçacığı aşağıdaki hello Azure Blob Storage tooAzure SQL veritabanı ' verileri kopyalayan bir işlem hattı örneği gösterilir:

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
## <a name="parameterizing-data-factory-template"></a>Veri Fabrikası şablon kümesini parametreleştirme
Kümesini parametreleştirme en iyi uygulamalar için bkz: [en iyi uygulamalar Azure Resource Manager şablonları oluşturmak için](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) makalesi. Özellikle değişkenleri yerine kullanılabilir genel olarak, parametre kullanımı, en aza. Yalnızca senaryoları aşağıdaki hello parametrelerinde sağlar:

* Ayarlar ortamı tarafından değişir (örnek: geliştirme, test ve üretim)
* Gizli (parolalar gibi)

Gelen toopull gizli gerekiyorsa [Azure anahtar kasası](../key-vault/key-vault-get-started.md) şablonları kullanarak Azure Data Factory varlıklarını dağıtırken hello belirtin **anahtar kasası** ve **gizli anahtar adı** gösterildiği gibi Örnek hello:

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
> Mevcut veri fabrikaları şablonları verme şu anda henüz desteklenmiyor olsa da, hello çalışır durumdur.
>
>
