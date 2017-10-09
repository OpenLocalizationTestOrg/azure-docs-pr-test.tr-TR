---
title: "bir Azure Resource Manager şablonu kullanarak aaaCreate Service Bus ad alanı | Microsoft Docs"
description: "Azure Resource Manager şablonu toocreate bir hizmet veri yolu ad alanı kullanın"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: dc0d6482-6344-4cef-8644-d4573639f5e4
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: fddf370affe761a734991ae9b60c1e5825e54ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a>Bir Azure Resource Manager şablonu kullanarak bir hizmet veri yolu ad alanı oluşturma

Nasıl bir hizmet veri yolu türünün ad alanını oluşturur toouse bir Azure Resource Manager şablonu bu makalede **ileti** standart/temel SKU ile. Merhaba makale ayrıca hello dağıtım hello yürütme için belirtilen başlangıç parametreleri tanımlar. Kendi dağıtımlar için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi.

Şablonları oluşturma hakkında daha fazla bilgi için lütfen bkz [Azure Resource Manager şablonları yazma][Authoring Azure Resource Manager templates].

Merhaba Hello tam şablonu için bkz [hizmet veri yolu ad alanı şablonu] [ Service Bus namespace template] github'da.

> [!NOTE]
> Azure Resource Manager şablonları aşağıdaki hello yükleme ve dağıtım için kullanılabilir. 
> 
> * [Sıra ile Service Bus ad alanı oluşturma](service-bus-resource-manager-namespace-queue.md)
> * [Hizmet veri yolu ad alanı konu ve abonelik oluşturma](service-bus-resource-manager-namespace-topic.md)
> * [Kuyruk ve yetkilendirme kuralı ile Service Bus ad alanı oluşturma](service-bus-resource-manager-namespace-auth-rule.md)
> * [Konu, abonelik ve kuralı ile Service Bus ad alanı oluşturma](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> Merhaba son şablonları için toocheck ziyaret hello [Azure hızlı başlangıç şablonlarını] [ Azure Quickstart Templates] Galerisi ve Service Bus arayın.
> 
> 

## <a name="what-will-you-deploy"></a>Ne dağıtacaksınız?
Bu şablonla, hizmet veri yolu ad alanınızla dağıtacağınız bir [temel, standart veya Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.

toorun dağıtım otomatik olarak Merhaba, düğme aşağıdaki hello tıklatın:

[![TooAzure dağıtma](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)

## <a name="parameters"></a>Parametreler
Azure Resource Manager ile tanımladığınız parametreler için değerler hello şablon dağıtıldığında toospecify istediğiniz. Merhaba şablonu adlı bir bölüm içerir `Parameters` tüm hello parametre değerlerini içerir. Dağıttığınız hello projesini temel alan veya dağıttığınız hello ortamı dayanarak değişir bu değerleri için bir parametre tanımlamanız gerekir. Her zaman kalacak değerleri aynı hello için parametreleri tanımlamayın. Her parametre değeri dağıtılan hello şablonu toodefine hello kaynaklarında kullanılır.

Bu şablon şu parametreler hello tanımlar.

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

### <a name="servicebussku"></a>serviceBusSKU
Merhaba Service Bus Hello adını [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.

```json
"serviceBusSku": { 
    "type": "string", 
    "allowedValues": [ 
        "Basic", 
        "Standard",
        "Premium" 
    ], 
    "defaultValue": "Standard", 
    "metadata": { 
        "description": "hello messaging tier for service Bus namespace" 
    } 

```

Merhaba şablonu (temel, standart veya Premium) Bu parametre için izin verilen hello değerleri tanımlar ve herhangi bir değer belirtilmezse varsayılan değer (standart) atar.

Hizmet veri yolu fiyatlandırma hakkında daha fazla bilgi için bkz: [Service fiyatlandırma ve faturalama Bus][Service Bus pricing and billing].

### <a name="servicebusapiversion"></a>serviceBusApiVersion
Hizmet veri yolu API'sini sürümü hello şablon Hello.

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by hello template" 
       } 
```

## <a name="resources-toodeploy"></a>Kaynakları toodeploy
### <a name="service-bus-namespace"></a>Hizmet veri yolu ad alanı
Standart bir hizmet veri yolu ad alanı türü oluşturur **ileti**.

```json
"resources": [
    {
        "apiVersion": "[parameters('serviceBusApiVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "properties": {
        }
    }
]
```

## <a name="commands-toorun-deployment"></a>Komutları toorun dağıtımı
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a>Azure CLI
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a>Sonraki adımlar
Oluşturulan ve Azure Resource Manager kullanarak kaynakları dağıtılan göre öğrenin nasıl toomanage bu makaleleri okuyarak bu kaynakları:

* [Service Bus PowerShell ile yönetme](service-bus-manage-with-ps.md)
* [Merhaba hizmet veri yolu Gezgini ile Service Bus kaynaklarını yönetme](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
