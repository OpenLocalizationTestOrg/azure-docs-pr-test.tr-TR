---
title: "bir şablonu kullanarak bir Azure Event Hubs ad alanı ve tüketici grubu aaaCreate | Microsoft Docs"
description: "Azure Resource Manager şablonları kullanarak bir tüketici grubu ve bir event hub ile Event Hubs ad alanı oluşturma"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 28bb4591-1fd7-444f-a327-4e67e8878798
ms.service: event-hubs
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/12/2017
ms.author: sethm;shvija
ms.openlocfilehash: 74b0d6b3fbe848705e2c20e628aa4e5269b53edb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a>Bir Azure Resource Manager şablonu kullanarak olay hub'ı ve tüketici grubu ile bir olay hub'ları ad alanı oluşturma

Bu makalede nasıl toouse bir Azure Resource Manager şablonu, bir ad alanı türü Event Hubs bir olay hub'ı tek bir tüketici grubu oluşturur ve gösterilmektedir. Merhaba gösterir makalesi nasıl toodefine hangi kaynağın dağıtılan ve nasıl olan toodefine hello dağıtım zaman yürütülür parametrelerinizi. Kendi dağıtımlar için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi

Şablon oluşturma hakkında daha fazla bilgi için bkz. [Azure Resource Manager şablonları yazma][Authoring Azure Resource Manager templates].

Merhaba Hello tam şablonu için bkz [olay hub'ı ve tüketici grubu şablonunu] [ Event Hub and consumer group template] github'da.

> [!NOTE]
> Merhaba son şablonları için toocheck ziyaret hello [Azure hızlı başlangıç şablonlarını] [ Azure Quickstart Templates] Galerisi ve Event Hubs arayın.
> 
> 

## <a name="what-will-you-deploy"></a>Ne dağıtacaksınız?
Bu şablon kullanılarak bir olay hub'ı ve bir tüketici grubu içeren bir olay hub'ları ad dağıtır.

[Olay hub'ları](event-hubs-what-is-event-hubs.md) büyük ölçekte kullanılan hizmet tooprovide olayı ve telemetri giriş tooAzure düşük gecikme süreli ve yüksek güvenilirlik işlemeyi bir olaydır.

toorun dağıtım otomatik olarak Merhaba, düğme aşağıdaki hello tıklatın:

[![TooAzure dağıtma](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)

## <a name="parameters"></a>Parametreler
Azure Resource Manager ile tanımladığınız parametreler için değerler hello şablon dağıtıldığında toospecify istediğiniz. Merhaba şablonu adlı bir bölüm içerir `Parameters` tüm hello parametre değerlerini içerir. Dağıttığınız hello projesini temel alan veya dağıttığınız hello ortamı toowhich üzerinde temel değişir bu değerleri için bir parametre tanımlamanız gerekir. Her zaman kalın değerleri aynı hello için parametreleri tanımlamayın. Her parametre değeri hello şablonunda dağıtılan hello kaynakları tanımlar.

Merhaba şablonu şu parametreler hello tanımlar:

### <a name="eventhubnamespacename"></a>eventHubNamespaceName
Merhaba olay hub'ları ad alanı toocreate Hello adı.

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a>eventHubName
Merhaba event hub'ı hello olay hub'ları ad alanında oluşturulan Hello adı.

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a>eventHubConsumerGroupName
Merhaba olay hub'ı için oluşturulan hello tüketici grubu Hello adı.

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a>apiVersion
Merhaba şablon Hello API sürümü.

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a>Kaynakları toodeploy
Tür bir ad oluşturur **EventHubs**bir olay hub'ı ve bir tüketici grubu.

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('namespaceName')]",
         "type":"Microsoft.EventHub/namespaces",
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
                  "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]"
               },
               "resources":[  
                  {  
                     "apiVersion":"[variables('ehVersion')]",
                     "name":"[parameters('consumerGroupName')]",
                     "type":"ConsumerGroups",
                     "dependsOn":[  
                        "[parameters('eventHubName')]"
                     ],
                     "properties":{  

                     }
                  }
               ]
            }
         ]
      }
   ],
```

## <a name="commands-toorun-deployment"></a>Komutları toorun dağıtımı
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a>Azure CLI
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a>Sonraki adımlar
Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:

* [Event Hubs’a genel bakış](event-hubs-what-is-event-hubs.md)
* [Olay Hub’ı oluşturma](event-hubs-create.md)
* [Event Hubs ile ilgili SSS](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
