---
title: "aaaCreate Azure Service Bus konu aboneliği ve Azure Resource Manager şablonu kullanarak kural | Microsoft Docs"
description: "Hizmet veri yolu ad alanı konu, aboneliği ve Azure Resource Manager şablonu kullanarak kural oluşturma"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9e0aaf58-0214-4bca-bd00-d29c08f9b1bc
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: dbc46da8491aee4d0c73bd4db90c696008920df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a>Hizmet veri yolu ad alanı konu, aboneliği ve Azure Resource Manager şablonu kullanarak kural oluşturma

Bu makalede nasıl toouse bir Azure Resource Manager şablonu, bir hizmet veri yolu ad alanı bir konu, abonelik kural (Filtresi) oluşturur ve gösterilmektedir. Hakkında bilgi edineceksiniz nasıl toodefine hangi kaynağın dağıtılan ve nasıl toodefine parametreler hello dağıtım zaman yürütülür belirtilmiş. Kendi dağıtımlar için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi

Şablon oluşturma hakkında daha fazla bilgi için bkz. [Azure Resource Manager şablonları yazma][Authoring Azure Resource Manager templates].

Adlandırma kuralları Azure kaynaklarını uygulama ve desenleri hakkında daha fazla bilgi için bkz: [Azure kaynakları için adlandırma kurallarını önerilen][Recommended naming conventions for Azure resources].

Merhaba Hello tam şablonu için bkz [konu, abonelik ve kuralı ile Service Bus ad alanı] [ Service Bus namespace with topic, subscription, and rule] şablonu.

> [!NOTE]
> Azure Resource Manager şablonları aşağıdaki hello yükleme ve dağıtım için kullanılabilir.
> 
> * [Kuyruk ve yetkilendirme kuralı ile Service Bus ad alanı oluşturma](service-bus-resource-manager-namespace-auth-rule.md)
> * [Sıra ile Service Bus ad alanı oluşturma](service-bus-resource-manager-namespace-queue.md)
> * [Hizmet veri yolu ad alanı oluşturma](service-bus-resource-manager-namespace.md)
> * [Hizmet veri yolu ad alanı konu ve abonelik oluşturma](service-bus-resource-manager-namespace-topic.md)
> 
> Merhaba son şablonları için toocheck ziyaret hello [Azure hızlı başlangıç şablonlarını] [ Azure Quickstart Templates] Galerisi ve Service Bus arayın.
> 
> 

## <a name="what-will-you-deploy"></a>Ne dağıtacaksınız?

Bu şablon kullanılarak konu, abonelik ve kural (Filtresi) içeren bir hizmet veri yolu ad dağıtın.

[Service Bus konuları ve abonelikleri](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) iletişim, bir çok form sağladığınız bir *Yayınla/Abone ol* düzeni. Bunun yerine konular ve abonelikler, dağıtılmış uygulamanın bileşenleri birbirleriyle doğrudan, iletişim kurmazlar kullanıldığında bir aracı gibi davranan bir konu aracılığıyla iletileri değiş. Bir abonelik tooa konu toohello konu gönderilen iletilerin kopyalarını alan sanal kuyruğa benzer. Abonelik filtre tooa konu içinde belirli konu aboneliği görünmelidir hangi iletilerin gönderilen toospecify sağlar.

## <a name="what-are-rules-filters"></a>Kuralları (filtreleri) nelerdir?

Birçok senaryoda belirli özelliklere sahip iletileri farklı şekillerde işlenmelidir. tooenable Bu, belirli özellikleri ve değişiklikleri toothose özellikleri gerçekleştirmek abonelikleri toofind iletileri yapılandırabilirsiniz. Service Bus abonelikleri toohello konu gönderilen tüm iletiler görmenize rağmen yalnızca bir alt kümesini bu iletileri toohello sanal abonelik sırası kopyalayabilirsiniz. Bu, abonelik filtreleri kullanılarak gerçekleştirilir. toolearn kuralları (filtreleri) hakkında daha fazla bilgi görmek [kurallar ve Eylemler](service-bus-queues-topics-subscriptions.md#rules-and-actions).

toorun dağıtım otomatik olarak Merhaba, düğme aşağıdaki hello tıklatın:

[![TooAzure dağıtma](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)

## <a name="parameters"></a>Parametreler

Azure Resource Manager ile parametreleri tanımlamanız gerekir değerlerini hello şablon dağıtıldığında toospecify istiyor. Merhaba şablonu adlı bir bölüm içerir `Parameters` tüm hello parametre değerlerini içerir. Dağıttığınız hello projesini temel alan veya dağıttığınız hello ortamı dayanarak farklılık bu değerleri için bir parametre tanımlamanız gerekir. Her zaman kalın değerleri aynı hello için parametreleri tanımlamayın. Her parametre değeri dağıtılan hello şablonu toodefine hello kaynaklarında kullanılır.

Merhaba şablonu şu parametreler hello tanımlar:

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
Merhaba hizmet veri yolu ad alanı toocreate Hello adı.

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a>serviceBusTopicName
Merhaba hizmet veri yolu ad alanında oluşturulan hello konu Hello adı.

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a>serviceBusSubscriptionName
Merhaba hizmet veri yolu ad alanında oluşturulan hello abonelik Hello adı.

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a>serviceBusRuleName
Merhaba hizmet veri yolu ad alanında oluşturulan hello rule(filter) Hello adı.

```json
   "serviceBusRuleName": {
   "type": "string",
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
Standart bir hizmet veri yolu ad alanı türü oluşturur **ileti**, konu ve abonelik ve kuralları ile.

```json
 "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "sku": {
            "name": "Standard",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]"
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {},
                "resources": [{
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusRuleName')]",
                    "type": "Rules",
                    "dependsOn": [
                        "[parameters('serviceBusSubscriptionName')]"
                    ],
                    "properties": {
                        "filter": {
                            "sqlExpression": "StoreName = 'Store1'"
                        },
                        "action": {
                            "sqlExpression": "set FilterTag = 'true'"
                        }
                    }
                }]
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a>Komutları toorun dağıtımı
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a>Azure CLI
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a>Sonraki adımlar
Oluşturulan ve Azure Resource Manager kullanarak kaynakları dağıtılan göre öğrenin nasıl toomanage Bu makaleler görüntüleyerek bu kaynakları:

* [Azure hizmet veri yolu yönetme](service-bus-management-libraries.md)
* [Service Bus PowerShell ile yönetme](service-bus-manage-with-ps.md)
* [Merhaba hizmet veri yolu Gezgini ile Service Bus kaynaklarını yönetme](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

