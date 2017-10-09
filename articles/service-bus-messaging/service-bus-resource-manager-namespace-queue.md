---
title: "aaaCreate Azure Service Bus ad alanı ve Azure Resource Manager şablonu kullanarak sıraya | Microsoft Docs"
description: "Bir hizmet veri yolu ad alanı ve Azure Resource Manager şablonu kullanarak bir sıra oluşturun"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a6bfb5fd-7b98-4588-8aa1-9d5f91b599b6
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: f230878b7c557bdd80d74da0de5a85ba4ee99ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-and-a-queue-using-an-azure-resource-manager-template"></a>Bir hizmet veri yolu ad alanı ve bir Azure Resource Manager şablonu kullanarak bir sıra oluşturun

Bu makalede nasıl toouse bir Azure Resource Manager şablonunu bir hizmet veri yolu ad alanı ve bu ad alanı içindeki bir kuyruk oluşturan gösterilmektedir. Şunları öğreneceksiniz nasıl toodefine hangi kaynağın dağıtılan ve nasıl toodefine parametreler hello dağıtım zaman yürütülür belirtilmiş. Kendi dağıtımlar için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi.

Şablonları oluşturma hakkında daha fazla bilgi için lütfen bkz [Azure Resource Manager şablonları yazma][Authoring Azure Resource Manager templates].

Merhaba Hello tam şablonu için bkz [hizmet veri yolu ad alanı ve sıra şablonu] [ Service Bus namespace and queue template] github'da.

> [!NOTE]
> Azure Resource Manager şablonları aşağıdaki hello yükleme ve dağıtım için kullanılabilir.
> 
> * [Kuyruk ve yetkilendirme kuralı ile Service Bus ad alanı oluşturma](service-bus-resource-manager-namespace-auth-rule.md)
> * [Hizmet veri yolu ad alanı konu ve abonelik oluşturma](service-bus-resource-manager-namespace-topic.md)
> * [Hizmet veri yolu ad alanı oluşturma](service-bus-resource-manager-namespace.md)
> * [Konu, abonelik ve kuralı ile Service Bus ad alanı oluşturma](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> Merhaba son şablonları için toocheck ziyaret hello [Azure hızlı başlangıç şablonlarını] [ Azure Quickstart Templates] Galerisi ve "Service Bus" için arama
> 
> 

## <a name="what-will-you-deploy"></a>Ne dağıtacaksınız?

Bu şablon kullanılarak bir hizmet veri yolu ad alanı bir kuyruk dağıtır.

[Service Bus kuyruklarını](service-bus-queues-topics-subscriptions.md#queues) ilk olarak, ilk çıkar (FIFO) ileti teslim tooone veya birden çok rakip tüketiciye sunar.

toorun dağıtım otomatik olarak Merhaba, düğme aşağıdaki hello tıklatın:

[![TooAzure dağıtma](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)

## <a name="parameters"></a>Parametreler

Azure Resource Manager ile tanımladığınız parametreler için değerler hello şablon dağıtıldığında toospecify istediğiniz. Merhaba şablonu adlı bir bölüm içerir `Parameters` tüm hello parametre değerlerini içerir. Dağıttığınız hello projesini temel alan veya dağıttığınız hello ortamı dayanarak değişir bu değerleri için bir parametre tanımlamanız gerekir. Her zaman kalacak değerleri aynı hello için parametreleri tanımlamayın. Her parametre değeri dağıtılan hello şablonu toodefine hello kaynaklarında kullanılır.

Merhaba şablonu şu parametreler hello tanımlar.

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
Merhaba hizmet veri yolu ad alanı toocreate Hello adı.

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebusqueuename"></a>serviceBusQueueName
Merhaba hizmet veri yolu ad alanında oluşturulan hello sırasının Hello adı.

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
Standart bir hizmet veri yolu ad alanı türü oluşturur **ileti**, bir kuyruk.

```json
"resources ": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]",
            }
        }]
    }]
```

## <a name="commands-toorun-deployment"></a>Komutları toorun dağıtımı
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="azure-cli"></a>Azure CLI

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="next-steps"></a>Sonraki adımlar
Oluşturulan ve Azure Resource Manager kullanarak kaynakları dağıtılan göre öğrenin nasıl toomanage Bu makaleler görüntüleyerek bu kaynakları:

* [Service Bus PowerShell ile yönetme](service-bus-manage-with-ps.md)
* [Merhaba hizmet veri yolu Gezgini ile Service Bus kaynaklarını yönetme](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace and queue template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus queues]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
