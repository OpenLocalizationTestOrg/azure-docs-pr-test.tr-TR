---
title: "Azure Resource Manager şablonu kullanarak aaaCreate Service Bus yetkilendirme kuralı | Microsoft Docs"
description: "Ad alanı ve Azure Resource Manager şablonu kullanarak sıra için bir hizmet veri yolu yetkilendirme kuralı oluştur"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f1443a0-5fa8-4d90-8637-1a977ef0b1f0
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 48df97849281d3b47e9d722d4e821c874644be59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a>Ad alanı ve bir Azure Resource Manager şablonu kullanarak sıra için bir hizmet veri yolu yetkilendirme kuralı oluştur

Bu makalede gösterilmektedir nasıl toouse bir Azure Resource Manager şablonu oluşturan bir [yetkilendirme kuralı](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) için bir hizmet veri yolu ad alanı ve sıra. Şunları öğreneceksiniz nasıl toodefine hangi kaynağın dağıtılan ve nasıl toodefine parametreler hello dağıtım zaman yürütülür belirtilmiş. Kendi dağıtımlar için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi.

Şablonları oluşturma hakkında daha fazla bilgi için lütfen bkz [Azure Resource Manager şablonları yazma][Authoring Azure Resource Manager templates].

Merhaba Hello tam şablonu için bkz [Service Bus yetkilendirme kuralı şablonunu] [ Service Bus auth rule template] github'da.

> [!NOTE]
> Azure Resource Manager şablonları aşağıdaki hello yükleme ve dağıtım için kullanılabilir.
> 
> * [Hizmet veri yolu ad alanı oluşturma](service-bus-resource-manager-namespace.md)
> * [Sıra ile Service Bus ad alanı oluşturma](service-bus-resource-manager-namespace-queue.md)
> * [Hizmet veri yolu ad alanı konu ve abonelik oluşturma](service-bus-resource-manager-namespace-topic.md)
> * [Konu, abonelik ve kuralı ile Service Bus ad alanı oluşturma](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> Merhaba son şablonları için toocheck ziyaret hello [Azure hızlı başlangıç şablonlarını] [ Azure Quickstart Templates] Galerisi ve "Service Bus" için arama
> 
> 

## <a name="what-will-you-deploy"></a>Ne dağıtacaksınız?
Bu şablon kullanılarak bir hizmet veri yolu yetkilendirme kuralı için bir ad alanı ve mesajlaşma varlığıyla (Bu durumda, bir kuyruktaki) dağıtır.

Bu şablonu kullanan [paylaşılan erişim imzası (SAS)](service-bus-sas.md) kimlik doğrulaması için. SAS uygulamaları tooauthenticate tooService hello ad alanı veya belirli hakları ilişkili olan varlık (kuyruk veya konu) Mesajlaşma hello yapılandırılmış bir erişim anahtarı kullanarak veri yolu sağlar. Daha sonra bu anahtar toogenerate istemcileri tooauthenticate tooService Bus sırayla kullanabileceğiniz bir SAS belirteci kullanabilirsiniz.

toorun dağıtım otomatik olarak Merhaba, düğme aşağıdaki hello tıklatın:

[![TooAzure dağıtma](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)

## <a name="parameters"></a>Parametreler

Azure Resource Manager ile tanımladığınız parametreler için değerler hello şablon dağıtıldığında toospecify istediğiniz. Merhaba şablonu adlı bir bölüm içerir `Parameters` tüm hello parametre değerlerini içerir. Dağıttığınız hello projesini temel alan veya dağıttığınız hello ortamı dayanarak değişir bu değerleri için bir parametre tanımlamanız gerekir. Her zaman kalacak değerleri aynı hello için parametreleri tanımlamayın. Her parametre değeri dağıtılan hello şablonu toodefine hello kaynaklarında kullanılır.

Merhaba şablonu şu parametreler hello tanımlar.

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
Merhaba hizmet veri yolu ad alanı toocreate Hello adı.

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="namespaceauthorizationrulename"></a>namespaceAuthorizationRuleName
Merhaba Yetkilendirme kuralının adını Hello hello ad alanı için.

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a>serviceBusQueueName
Merhaba Service Bus ad alanı hello sırada Hello adı.

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a>serviceBusApiVersion
Hizmet veri yolu API'sini sürümü hello şablon Hello.

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a>Kaynakları toodeploy
Standart bir hizmet veri yolu ad alanı türü oluşturur **ileti**ve ad alanı ve varlık için bir hizmet veri yolu yetkilendirme kuralı.

```json
"resources": [
        {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusNamespaceName')]",
            "type": "Microsoft.ServiceBus/namespaces",
            "location": "[variables('location')]",
            "kind": "Messaging",
            "sku": {
                "name": "StandardSku",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusQueueName')]",
                    "type": "Queues",
                    "dependsOn": [
                        "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('serviceBusQueueName')]"
                    },
                    "resources": [
                        {
                            "apiVersion": "[variables('sbVersion')]",
                            "name": "[parameters('queueAuthorizationRuleName')]",
                            "type": "authorizationRules",
                            "dependsOn": [
                                "[parameters('serviceBusQueueName')]"
                            ],
                            "properties": {
                                "Rights": ["Listen"]
                            }
                        }
                    ]
                }
            ]
        }, {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[variables('namespaceAuthRuleName')]",
            "type": "Microsoft.ServiceBus/namespaces/authorizationRules",
            "dependsOn": ["[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"],
            "location": "[resourceGroup().location]",
            "properties": {
                "Rights": ["Send"]
            }
        }
    ]
```

## <a name="commands-toorun-deployment"></a>Komutları toorun dağıtımı
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a>Azure CLI
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a>Sonraki adımlar
Oluşturulan ve Azure Resource Manager kullanarak kaynakları dağıtılan göre öğrenin nasıl toomanage Bu makaleler görüntüleyerek bu kaynakları:

* [Service Bus PowerShell ile yönetme](service-bus-powershell-how-to-provision.md)
* [Merhaba hizmet veri yolu Gezgini ile Service Bus kaynaklarını yönetme](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [Hizmet veri yolu kimlik doğrulama ve yetkilendirme](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
