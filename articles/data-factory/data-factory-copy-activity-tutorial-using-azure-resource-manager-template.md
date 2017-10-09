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
# <a name="tutorial-use-azure-resource-manager-template-toocreate-a-data-factory-pipeline-toocopy-data"></a>Öğretici: Azure Kaynak Yöneticisi'ni kullanın şablonu toocreate Data Factory işlem hattı toocopy veri 
> [!div class="op_single_selector"]
> * [Genel bakış ve önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Kopyalama Sihirbazı](data-factory-copy-data-wizard-tutorial.md)
> * [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager şablonu](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API’si](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

Bu öğretici şunların nasıl yapıldığını gösterir toouse Azure Resource Manager şablonu toocreate bir Azure data factory. Merhaba veri ardışık Bu öğreticide, bir kaynak veri deposu tooa hedef veri deposundan verileri kopyalar. Giriş verisi tooproduce çıktı verilerini dönüştürmez. Nasıl bir öğretici için Azure Data Factory kullanarak tootransform verileri görmek [Öğreticisi: Hadoop kümesi kullanarak bir ardışık düzen tootransform veri derleme](data-factory-build-your-first-pipeline.md).

Bu öğreticide, içinde bir etkinlik olan işlem hattı oluşturursunuz: Kopyalama Etkinliği. Merhaba kopyalama etkinliği bir desteklenen veri deposu tooa desteklenen havuz veri deposundan verileri kopyalar. Kaynak ve havuz olarak desteklenen veri depolarının listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Merhaba etkinlik verileri güvenli, güvenilir ve ölçeklenebilir bir şekilde çeşitli veri depolamaları arasında kopyalayabilirsiniz genel olarak kullanılabilir bir hizmet tarafından desteklenir. Merhaba kopyalama etkinliği hakkında daha fazla bilgi için bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).

Bir işlem hattında birden fazla etkinlik olabilir. Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir. Daha fazla bilgi için bkz. [bir işlem hattında birden fazla etkinlik](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> Merhaba veri ardışık Bu öğreticide, bir kaynak veri deposu tooa hedef veri deposundan verileri kopyalar. Nasıl bir öğretici için Azure Data Factory kullanarak tootransform verileri görmek [Öğreticisi: Hadoop kümesi kullanarak bir ardışık düzen tootransform veri derleme](data-factory-build-your-first-pipeline.md). 

## <a name="prerequisites"></a>Ön koşullar
* Git üzerinden [öğreticiye genel bakış ve önkoşulları](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) ve tam hello **önkoşul** adımları.
* ' Ndaki yönergeleri izleyin [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) makale tooinstall en son sürümü Azure PowerShell, bilgisayarınızda. Bu öğreticide PowerShell toodeploy Data Factory varlıklarını kullanın. 
* (isteğe bağlı) Bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md) toolearn Azure Resource Manager şablonları hakkında.

## <a name="in-this-tutorial"></a>Bu öğreticide
Bu öğreticide, Data Factory varlıklarını aşağıdaki hello ile bir veri fabrikası oluşturun:

| Varlık | Açıklama |
| --- | --- |
| Azure Storage bağlı hizmeti |Azure depolama hesabı toohello veri fabrikanıza bağlar. Azure depolama hello kaynak veri deposu ve Azure SQL veritabanı hello kopyalama etkinliği için hello havuz veri deposu hello öğreticide. Hello hello kopyalama etkinliği için giriş verileri içeren hello depolama hesabını belirtir. |
| Azure SQL Veritabanı bağlı hizmeti |Azure SQL veritabanı toohello veri fabrikanıza bağlar. Merhaba kopyalama etkinliği için hello çıktı verilerini tutan hello Azure SQL veritabanı belirtir. |
| Azure Blob giriş veri kümesi |Toohello Azure Storage bağlı hizmeti anlamına gelmektedir. Merhaba bağlantılı hizmet tooan Azure depolama hesabı anlamına gelir ve hello Azure Blob dataset hello girdi verilerini tutan hello depolama hello kapsayıcı, klasör ve dosya adını belirtir. |
| Azure SQL çıktı veri kümesi |Toohello Azure SQL bağlı hizmeti anlamına gelmektedir. Hello Azure SQL bağlı hizmeti tooan Azure SQL server anlamına gelir ve hello Azure SQL veri kümesi hello hello çıktı verilerini tutan Merhaba tablonun adını belirtir. |
| Veri işlem hattı |Merhaba ardışık düzen hello Azure blob dataset bir girdi olarak alır kopyalama yazın ve Azure SQL veri kümesi bir çıkış olarak hello bir etkinlik vardır. Merhaba kopyalama etkinliği hello Azure SQL veritabanındaki bir Azure blob tooa tablodan veri kopyalar. |

Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir. İşlem hattında bir veya daha fazla etkinlik olabilir. İki tür etkinlik mevcuttur: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) ve [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md). Bu öğreticide bir etkinlik (kopyalama etkinliği) ile işlem hattı oluşturursunuz.

![Azure Blob tooAzure SQL veritabanını kopyalama](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

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
Adlı bir JSON dosyası oluşturun **ADFCopyTutorialARM.json** içinde **C:\ADFGetStarted** içeriği aşağıdaki hello klasörüyle:

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

## <a name="parameters-json"></a>Parametreler JSON
Adlı bir JSON dosyası oluşturun **ADFCopyTutorialARM Parameters.json** hello Azure Resource Manager şablonu parametrelerini içerir. 

> [!IMPORTANT]
> storageAccountName ve storageAccountKey parametreleri için Azure Depolama hesabınızın adını ve anahtarını belirtin.  
> 
> sqlServerName, databaseName, sqlServerUserName ve sqlServerPassword parametreleri için Azure SQL sunucusunu, veritabanını, kullanıcıyı ve parolayı belirtin.  

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
   * Çalışma hello aşağıdaki toowork ile istediğiniz tooselect hello abonelik komutu.
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. 1. adımda oluşturduğunuz hello Resource Manager şablonu kullanarak komut toodeploy Data Factory varlıklarını aşağıdaki hello çalıştırın.

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>İşlem hattını izleme

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) Azure hesabınızı kullanarak.
2. Tıklatın **veri fabrikaları** hello sol menü (veya) tıklatın **daha fazla hizmet** tıklatıp **veri fabrikaları** altında **INTELLİGENCE + ANALİZ** Kategori.
   
    ![Veri fabrikaları menüsü](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. Merhaba, **veri fabrikaları** sayfasında, aramak ve veri fabrikanızı (AzureBlobToAzureSQLDatabaseDF) bulabilirsiniz. 
   
    ![Veri fabrikası arama](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. Azure veri fabrikanıza tıklayın. Merhaba veri fabrikası için hello giriş sayfasına bakın.
   
    ![Veri fabrikasının giriş sayfası](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. Makalesindeki yönergeleri izleyin [veri kümelerini ve ardışık düzen izleme](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello ardışık düzen ve veri kümeleri Bu öğreticide oluşturdunuz. Visual Studio şu anda Data Factory işlem hatlarını izlemeyi desteklememektedir.
7. Bir dilim hello olduğunda **hazır** durum, hello veri kopyalanan toohello olduğunu doğrulayın **emp** hello Azure SQL veritabanı tablosunda.


Nasıl toouse Azure portal dikey penceresi toomonitor ardışık düzen ve veri kümeleri, bu öğreticide oluşturduğunuz daha fazla bilgi için bkz: [veri kümelerini ve ardışık düzen izleme](data-factory-monitor-manage-pipelines.md) .

Toouse hello İzleyici & Yönet uygulama toomonitor verilerinizi nasıl ardışık düzenleri daha fazla bilgi için bkz: [İzleyicisi ve izleme uygulaması kullanarak Azure Data Factory işlem hatlarını yönetmek](data-factory-monitor-manage-app.md).

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
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

Merhaba kaynak grup kimliğine göre benzersiz bir dize değil  

### <a name="defining-data-factory-entities"></a>Data Factory varlıklarını tanımlama
Merhaba aşağıdaki Data Factory varlıklarını hello JSON şablonunda tanımlanmıştır: 

1. [Azure Storage bağlı hizmeti](#azure-storage-linked-service)
2. [Azure SQL bağlı hizmeti](#azure-sql-database-linked-service)
3. [Azure blob veri kümesi](#azure-blob-dataset)
4. [Azure SQL veri kümesi](#azure-sql-dataset)
5. [Kopyalama etkinliği içeren bir veri işlem hattı](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Azure Storage bağlı hizmeti
Merhaba AzureStorageLinkedService Azure depolama hesabı toohello veri fabrikanıza bağlar. Bir kapsayıcı oluşturulur ve veri toothis depolama hesabı bir parçası olarak yüklenen [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). Bu bölümde hello adı ve Azure depolama hesabınızın anahtarı belirtin. Bkz: [Azure depolama bağlantılı hizmeti](data-factory-azure-blob-connector.md#azure-storage-linked-service) JSON kullanılan özellikler toodefine hakkında ayrıntılı bilgi için bir Azure Storage bağlı hizmeti. 

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

Merhaba connectionString hello storageAccountName ve storageAccountKey parametrelerini kullanır. bir yapılandırma dosyası kullanarak geçirilen bu parametrelerin değerlerini Hello. Merhaba tanımını değişkenleri de kullanır: azureStroageLinkedService ve dataFactoryName hello şablonda tanımlı. 

#### <a name="azure-sql-database-linked-service"></a>Azure SQL Veritabanı bağlı hizmeti
AzureSqlLinkedService Azure SQL veritabanı toohello veri fabrikanıza bağlar. Merhaba blob depolama biriminden kopyalanan hello veriler bu veritabanında depolanır. Bu veritabanında hello emp tablosunda bir parçası olarak oluşturulan [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). Bu bölümde hello Azure SQL sunucu adı, veritabanı adı, kullanıcı adı ve parola belirtin. Bkz: [Azure SQL bağlı hizmeti](data-factory-azure-sql-connector.md#linked-service-properties) JSON kullanılan özellikler toodefine hakkındaki ayrıntılar için hizmeti bir Azure SQL bağlı.  

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

Merhaba connectionString sqlsunucusuadı, databaseName, sqlServerUserName ve bir yapılandırma dosyası kullanarak değerleri geçirilen sqlServerPassword parametreleri kullanır. Merhaba tanımını da hello şablondan değişkenleri aşağıdaki hello kullanır: azureSqlLinkedServiceName, dataFactoryName.

#### <a name="azure-blob-dataset"></a>Azure blob veri kümesi
Hello Azure depolama bağlı hizmeti çalışma zamanı tooconnect tooyour Azure depolama hesabı Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir. Azure blob veri kümesi tanımında blob kapsayıcı, klasör ve hello giriş verisi içeren dosya adını belirtin. Bkz: [Azure Blob veri kümesi özellikleri](data-factory-azure-blob-connector.md#dataset-properties) JSON kullanılan özellikler toodefine bir Azure Blob dataset hakkında ayrıntılı bilgi için. 

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

#### <a name="azure-sql-dataset"></a>Azure SQL veri kümesi
Hello Azure Blob depolama alanından kopyalanan hello verilerini tutan hello Azure SQL veritabanında hello Merhaba tablonun adını belirtin. Bkz: [Azure SQL veri kümesi özellikleri](data-factory-azure-sql-connector.md#dataset-properties) JSON kullanılan özellikler toodefine bir Azure SQL veri kümesini hakkında ayrıntılı bilgi için. 

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

#### <a name="data-pipeline"></a>Veri işlem hattı
Hello Azure blob dataset toohello Azure SQL veri kümesinden alınan verileri kopyalayan bir işlem hattı tanımlayın. Bkz: [ardışık düzen JSON](data-factory-create-pipelines.md#pipeline-json) JSON kullanılan öğeleri toodefine bu örnekteki işlem hattı açıklamaları için. 

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

## <a name="reuse-hello-template"></a>Merhaba şablonu yeniden
Merhaba öğreticide Data Factory varlıklarını ve parametreleri için değerleri geçirme için bir şablon tanımlamak için bir şablon oluşturdu. Merhaba ardışık düzen parametreleri aracılığıyla belirtilen Azure depolama hesabı tooan Azure SQL veritabanına veri kopyalar. toouse Merhaba aynı şablon toodeploy Data Factory varlıkları toodifferent ortamları, her ortam için bir parametre dosyası oluşturabilir ve toothat ortam dağıtırken kullanabilirsiniz.     

Örnek:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

Hello ilk komut hello geliştirme ortamı için parametre dosyası kullanır, ikinci bir hello için test ortamı ve hello üretim ortamı için üçüncü bir hello dikkat edin.  

Merhaba şablonu tooperform yeniden kullanabilir yinelenen görevler. Örneğin, birçok veri fabrikaları biriyle toocreate gerekir veya aynı uygulamak daha fazla ardışık düzen hello mantığı ancak her veri fabrikası farklı depolama ve SQL veritabanı hesapları kullanır. Bu senaryoda, kullandığınız hello aynı şablonu hello toocreate veri fabrikaları farklı parametre ile aynı ortamda (geliştirme, test veya üretim) dosyaları.   

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, bir kopyalama işleminde kaynak veri deposu olarak Azure blob depolama alanını ve hedef veri deposu olarak Azure SQL veritabanını kullandınız. Merhaba aşağıdaki tabloda kaynakları ve hedefleri hello kopyalama etkinliği tarafından desteklenen veri depoları listesi verilmiştir: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

nasıl bir veri öğesine/öğesinden toocopy veri deposu hakkında toolearn hello veri deposu hello tablosundaki hello bağlantısını tıklatın.
