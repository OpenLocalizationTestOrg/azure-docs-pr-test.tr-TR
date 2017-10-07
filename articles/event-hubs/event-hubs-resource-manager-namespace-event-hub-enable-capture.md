---
title: "bir Azure Event Hubs ad alanı ve etkinleştir yakalama bir şablon kullanarak aaaCreate | Microsoft Docs"
description: "Bir olay hub'ı ile bir Azure Event Hubs ad alanı oluşturma ve Azure Resource Manager şablonu kullanarak Yakalamayı etkinleştirme"
services: event-hubs
documentationcenter: .net
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 8bdda6a2-5ff1-45e3-b696-c553768f1090
ms.service: event-hubs
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: a43b4e8d690ae825047e8a9d609bfda89cf2a06f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-enable-capture-using-an-azure-resource-manager-template"></a>Bir olay hub'ı ile bir Event Hubs ad alanı oluşturma ve Azure Resource Manager şablonu kullanarak Yakalamayı etkinleştirme

Bu makalede nasıl toouse bir Azure Resource Manager şablonu, bir olay hub'ları ad alanı, bir olay hub'ı örneği etkinleştirir hello da oluşturur ve gösterilmektedir [yakalama özelliği](event-hubs-capture-overview.md) hello olay hub'ındaki. Merhaba makalede nasıl toodefine hangi kaynağın dağıtılan ve nasıl olan toodefine hello dağıtım zaman yürütülür parametrelerinizi. Kendi dağıtımlar için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi.

Bu makale ayrıca nasıl olayları Azure Storage Bloblarında veya bir Azure Data Lake Store yakalanır toospecify üzerinde hello gösterir, seçtiğiniz hedef.

Şablon oluşturma hakkında daha fazla bilgi için bkz. [Azure Resource Manager şablonları yazma][Authoring Azure Resource Manager templates].

Azure Kaynakları adlandırma kurallarına ilişkin uygulama ve yapılar için bkz. [Azure Kaynakları Adlandırma Kuralları][Azure Resources naming conventions].

Merhaba tam şablonları için GitHub bağlantılar aşağıdaki hello tıklatın:

- [Olay hub'ı ve etkinleştir yakalama tooStorage şablonu][Event Hub and enable Capture tooStorage template] 
- [Olay hub'ı ve etkinleştir yakalama tooAzure Data Lake Store şablonu][Event Hub and enable Capture tooAzure Data Lake Store template]

> [!NOTE]
> Merhaba son şablonları için toocheck ziyaret hello [Azure hızlı başlangıç şablonlarını] [ Azure Quickstart Templates] Galerisi ve Event Hubs arayın.
> 
> 

## <a name="what-will-you-deploy"></a>Ne dağıtacaksınız?

Bu şablonu kullanarak bir olay hub’ı ile Event Hubs ad alanı dağıtır ve aynı zamanda [Event Hubs Yakalama](event-hubs-capture-overview.md) özelliğini etkinleştirirsiniz.

[Olay hub'ları](event-hubs-what-is-event-hubs.md) büyük ölçekte kullanılan hizmet tooprovide olayı ve telemetri giriş tooAzure düşük gecikme süreli ve yüksek güvenilirlik işlemeyi bir olaydır. Tooautomatically teslim olay hub'ları tooAzure Blob Depolama birimindeki verileri veya Azure Data Lake Store, belirtilen zaman veya seçtiğiniz boyutu aralığı içinde akış hello olay hub'ları yakalama etkinleştirir.

Azure depolama alanına düğmesi tooenable olay hub'ları yakalama aşağıdaki hello tıklatın:

[![TooAzure dağıtma](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)

Azure Data Lake Store düğmesi tooenable olay hub'ları yakalama aşağıdaki hello tıklatın:

[![TooAzure dağıtma](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)

## <a name="parameters"></a>Parametreler

Azure Resource Manager ile tanımladığınız parametreler için değerler hello şablon dağıtıldığında toospecify istediğiniz. Merhaba şablonu adlı bir bölüm içerir `Parameters` tüm hello parametre değerlerini içerir. Dağıttığınız hello projesini temel alan veya dağıttığınız hello ortamı dayanarak farklılık bu değerleri için bir parametre tanımlamanız gerekir. Her zaman kalın değerleri aynı hello için parametreleri tanımlamayın. Her parametre değeri dağıtılan hello şablonu toodefine hello kaynaklarında kullanılır.

Merhaba şablonu şu parametreler hello tanımlar.

### <a name="eventhubnamespacename"></a>eventHubNamespaceName

Merhaba Hello adını [olay hub'ları ad alanı](event-hubs-create.md) toocreate.

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of hello EventHub namespace"
      }
}
```

### <a name="eventhubname"></a>eventHubName

Merhaba event hub'ı hello oluşturulan Hello adını [olay hub'ları ad alanı](event-hubs-create.md).

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of hello event hub"
    }
}
```

### <a name="messageretentionindays"></a>messageRetentionInDays

gün tooretain hello iletilerinin hello event hub'ındaki Hello sayısı. 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long tooretain hello data in event hub"
     }
 }
```

### <a name="partitioncount"></a>partitionCount

Merhaba event hub'ındaki bölümleri toocreate Hello sayısı.

```json
"partitionCount":{
    "type":"int",
    "defaultValue":2,
    "minValue":2,
    "maxValue":32,
    "metadata":{
        "description":"Number of partitions chosen"
    }
 }
```

### <a name="captureenabled"></a>captureEnabled

Yakalama hello olay hub'ına etkinleştirin.

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable hello Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a>captureEncodingFormat

Merhaba kodlama biçimi tooserialize hello olay verileri belirtin.

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"hello encoding format in which Capture serializes hello EventData"
    }
}
```

### <a name="capturetime"></a>captureTime

Merhaba zaman aralığı içinde olay hub'ları yakalama hello veri yakalamayı başlatır.

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"hello time window in seconds for hello capture"
    }
}
```

### <a name="capturesize"></a>captureSize
Başlangıç boyutu aralığı aktarılma hello veri yakalamayı yakalama başlatır.

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"hello size window in bytes for capture"
    }
}
```

###<a name="capturenameformat"></a>captureNameFormat

Olay hub'ları yakalama toowrite hello Avro dosyalarının kullandığı hello adı biçimi. Yakalama adı biçimi `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}` ve `{Second}` alanlarını içermelidir. Bu, herhangi bir sırada olabilir, sınırlayıcılar tercihe bağlıdır.
 
```json
"captureNameFormat": {
      "type": "string",
      "defaultValue": "{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}",
      "metadata": {
        "description": "A Capture Name Format must contain {Namespace}, {EventHub}, {PartitionId}, {Year}, {Month}, {Day}, {Hour}, {Minute} and {Second} fields. These can be arranged in any order with or without delimeters. E.g.  Prod_{EventHub}/{Namespace}\\{PartitionId}_{Year}_{Month}/{Day}/{Hour}/{Minute}/{Second}"
      }
    }
  }
```

### <a name="apiversion"></a>apiVersion

Merhaba şablon Hello API sürümü.

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2015-08-01",
    "metadata":{  
        "description":"ApiVersion used by hello template"
    }
 }
```

Hedef olarak Azure Storage'ı seçerseniz şu parametreler hello kullanın.

### <a name="destinationstorageaccountresourceid"></a>destinationStorageAccountResourceId

Yakalama tooyour yakalama bir Azure depolama hesabı kaynak kimliği tooenable istenen depolama hesabı gerektirir.

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want hello blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a>blobContainerName

hangi toocapture BLOB kapsayıcısında olay verilerinizi hello.

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want hello blobs captured"
    }
}
```

Azure Data Lake Store, hedef olarak seçerseniz, şu parametreler hello kullanın. TooCapture hello olay istediğiniz, Data Lake Store yolunuza bağlı izinlerini ayarlamanız gerekir. bkz: tooset izinleri [bu makalede](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).

###<a name="subscriptionid"></a>subscriptionId

Merhaba olay hub'ları ad alanı ve Azure Data Lake Store için abonelik kimliği. Her iki bu kaynakları hello altında olmalıdır aynı abonelik kimliği

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription Id of both Azure Data Lake Store and Event Hub namespace"
     }
 }
```

###<a name="datalakeaccountname"></a>dataLakeAccountName

Hello Azure Data Lake Store adı hello için olayları yakalandı.

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

###<a name="datalakefolderpath"></a>dataLakeFolderPath

Merhaba hedef klasör yolu hello için olayları yakalandı.

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination archive folder path"
    }
}
```

## <a name="resources-toodeploy-for-azure-storage-as-destination-toocaptured-events"></a>Azure depolama için kaynakları toodeploy de hedef toocaptured olayları

Türü bir ad oluşturur **EventHubs**bir olay hub'ı ve etkinleştirir tooAzure Blob Storage yakalayın.

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('eventHubNamespaceName')]",
         "type":"Microsoft.EventHub/Namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]",
                  "MessageRetentionInDays":"[parameters('messageRetentionInDays')]",
                  "PartitionCount":"[parameters('partitionCount')]",
                  "CaptureDescription":{
                        "enabled":"[parameters('captureEnabled')]",
                        "encoding":"[parameters('captureEncodingFormat')]",
                        "intervalInSeconds":"[parameters('captureTime')]",
                        "sizeLimitInBytes":"[parameters('captureSize')]",
                        "destination":{
                            "name":"EventHubCapture.AzureBlockBlob",
                            "properties":{
                                "StorageAccountResourceId":"[parameters('destinationStorageAccountResourceId')]",
                                "BlobContainer":"[parameters('blobContainerName')]"
                            }
                        } 
                  }

               }

            }
         ]
      }
   ]
```

## <a name="resources-toodeploy-for-azure-data-lake-store-as-destination"></a>Hedef olarak Azure Data Lake Store için kaynakları toodeploy

Tür bir ad oluşturur **EventHubs**bir olay hub'ı ve yakalama tooAzure Data Lake Store etkinleştirir.

```json
 "resources": [
        {
            "apiVersion": "2015-08-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "2015-08-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('eventHubName')]",
                        "ArchiveDescription": {
                            "enabled": "true",
                            "encoding": "[parameters('archiveEncodingFormat')]",
                            "intervalInSeconds": "[parameters('archiveTime')]",
                            "sizeLimitInBytes": "[parameters('archiveSize')]",
                            "destination": {
                                "name": "EventHubArchive.AzureDataLake",
                                "properties": {
                                    "DataLakeSubscriptionId": "[parameters('subscriptionId')]",
                                    "DataLakeAccountName": "[parameters('dataLakeAccountName')]",
                                    "DataLakeFolderPath": "[parameters('dataLakeFolderPath')]",
                                    "ArchiveNameFormat": "[parameters('archiveNameFormat')]"
                                }
                            }
                        }
                    }
                }
            ]
        }
    ]
```

## <a name="commands-toorun-deployment"></a>Komutları toorun dağıtımı

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell

Azure depolama alanına, şablon tooenable olay hub'ları yakalama dağıtın:
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

Azure Data Lake Store, şablon tooenable olay hub'ları yakalama dağıtın:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a>Azure CLI

Hedef olarak Azure Blob Depolamayı seçme:

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

Hedef olarak Azure Data Lake Store’u seçme:

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a>Sonraki adımlar

Ayrıca olay hub'ları yakalama hello yapılandırabilirsiniz [Azure portal](https://portal.azure.com). Daha fazla bilgi için bkz: [etkinleştirmek olay hub'ları yakalama kullanarak hello Azure portal](event-hubs-capture-enable-through-portal.md).

Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:

* [Event Hubs’a genel bakış](event-hubs-what-is-event-hubs.md)
* [Olay Hub’ı oluşturma](event-hubs-create.md)
* [Event Hubs ile ilgili SSS](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture tooStorage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture tooAzure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls
