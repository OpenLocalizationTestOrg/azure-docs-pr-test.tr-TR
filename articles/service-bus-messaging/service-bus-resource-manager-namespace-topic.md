---
title: "Azure Resource Manager şablonu kullanarak aaaCreate Azure Service Bus ad alanı konu aboneliği | Microsoft Docs"
description: "Konu ve abonelik Azure Resource Manager şablonu kullanarak bir hizmet veri yolu ad alanı oluşturma"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d3d55200-5c60-4b5f-822d-59974cafff0e
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 9b5f7d8710e598b73c0a7ea3daf8c300f7fa9ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a><span data-ttu-id="f2fd3-103">Konu ve abonelik bir Azure Resource Manager şablonu kullanarak bir hizmet veri yolu ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f2fd3-103">Create a Service Bus namespace with topic and subscription using an Azure Resource Manager template</span></span>

<span data-ttu-id="f2fd3-104">Bu makalede nasıl toouse bir Azure Resource Manager şablonunu bir hizmet veri yolu ad alanı ve bir konu ve abonelik bu ad alanı içindeki oluşturan gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f2fd3-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a topic and subscription within that namespace.</span></span> <span data-ttu-id="f2fd3-105">Şunları öğreneceksiniz nasıl toodefine hangi kaynağın dağıtılan ve nasıl toodefine parametreler hello dağıtım zaman yürütülür belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="f2fd3-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="f2fd3-106">Kendi dağıtımlar için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi</span><span class="sxs-lookup"><span data-stu-id="f2fd3-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="f2fd3-107">Şablonları oluşturma hakkında daha fazla bilgi için lütfen bkz [Azure Resource Manager şablonları yazma][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="f2fd3-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="f2fd3-108">Merhaba Hello tam şablonu için bkz [konu ve abonelik ile Service Bus ad alanı] [ Service Bus namespace with topic and subscription] şablonu.</span><span class="sxs-lookup"><span data-stu-id="f2fd3-108">For hello complete template, see hello [Service Bus namespace with topic and subscription][Service Bus namespace with topic and subscription] template.</span></span>

> [!NOTE]
> <span data-ttu-id="f2fd3-109">Azure Resource Manager şablonları aşağıdaki hello yükleme ve dağıtım için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f2fd3-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="f2fd3-110">Hizmet veri yolu ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f2fd3-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="f2fd3-111">Sıra ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f2fd3-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="f2fd3-112">Kuyruk ve yetkilendirme kuralı ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f2fd3-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="f2fd3-113">Konu, abonelik ve kuralı ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f2fd3-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="f2fd3-114">Merhaba son şablonları için toocheck ziyaret hello [Azure hızlı başlangıç şablonlarını] [ Azure Quickstart Templates] Galerisi ve "Service Bus" için arama</span><span class="sxs-lookup"><span data-stu-id="f2fd3-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="f2fd3-115">Ne dağıtacaksınız?</span><span class="sxs-lookup"><span data-stu-id="f2fd3-115">What will you deploy?</span></span>

<span data-ttu-id="f2fd3-116">Bu şablonla, konu ve abonelik içeren bir hizmet veri yolu ad dağıtır.</span><span class="sxs-lookup"><span data-stu-id="f2fd3-116">With this template, you will deploy a Service Bus namespace with topic and subscription.</span></span>

<span data-ttu-id="f2fd3-117">[Service Bus konuları ve abonelikleri](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) iletişim, bir çok form sağladığınız bir *Yayınla/Abone ol* düzeni.</span><span class="sxs-lookup"><span data-stu-id="f2fd3-117">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span>

<span data-ttu-id="f2fd3-118">toorun dağıtım otomatik olarak Merhaba, düğme aşağıdaki hello tıklatın:</span><span class="sxs-lookup"><span data-stu-id="f2fd3-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="f2fd3-119">[![TooAzure dağıtma](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="f2fd3-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="f2fd3-120">Parametreler</span><span class="sxs-lookup"><span data-stu-id="f2fd3-120">Parameters</span></span>

<span data-ttu-id="f2fd3-121">Azure Resource Manager ile tanımladığınız parametreler için değerler hello şablon dağıtıldığında toospecify istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="f2fd3-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="f2fd3-122">Merhaba şablonu adlı bir bölüm içerir `Parameters` tüm hello parametre değerlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="f2fd3-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="f2fd3-123">Dağıttığınız hello projesini temel alan veya dağıttığınız hello ortamı dayanarak değişir bu değerleri için bir parametre tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f2fd3-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="f2fd3-124">Her zaman kalacak değerleri aynı hello için parametreleri tanımlamayın.</span><span class="sxs-lookup"><span data-stu-id="f2fd3-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="f2fd3-125">Her parametre değeri dağıtılan hello şablonu toodefine hello kaynaklarında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f2fd3-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="f2fd3-126">Merhaba şablonu şu parametreler hello tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f2fd3-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="f2fd3-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="f2fd3-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="f2fd3-128">Merhaba hizmet veri yolu ad alanı toocreate Hello adı.</span><span class="sxs-lookup"><span data-stu-id="f2fd3-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="f2fd3-129">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="f2fd3-129">serviceBusTopicName</span></span>
<span data-ttu-id="f2fd3-130">Merhaba hizmet veri yolu ad alanında oluşturulan hello konu Hello adı.</span><span class="sxs-lookup"><span data-stu-id="f2fd3-130">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="f2fd3-131">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="f2fd3-131">serviceBusSubscriptionName</span></span>
<span data-ttu-id="f2fd3-132">Merhaba hizmet veri yolu ad alanında oluşturulan hello abonelik Hello adı.</span><span class="sxs-lookup"><span data-stu-id="f2fd3-132">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="f2fd3-133">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="f2fd3-133">serviceBusApiVersion</span></span>
<span data-ttu-id="f2fd3-134">Hizmet veri yolu API'sini sürümü hello şablon Hello.</span><span class="sxs-lookup"><span data-stu-id="f2fd3-134">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="f2fd3-135">Kaynakları toodeploy</span><span class="sxs-lookup"><span data-stu-id="f2fd3-135">Resources toodeploy</span></span>
<span data-ttu-id="f2fd3-136">Standart bir hizmet veri yolu ad alanı türü oluşturur **ileti**, konu ve abonelik ile.</span><span class="sxs-lookup"><span data-stu-id="f2fd3-136">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription.</span></span>

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
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]",
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {}
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="f2fd3-137">Komutları toorun dağıtımı</span><span class="sxs-lookup"><span data-stu-id="f2fd3-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="f2fd3-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2fd3-138">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="f2fd3-139">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f2fd3-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="f2fd3-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f2fd3-140">Next steps</span></span>
<span data-ttu-id="f2fd3-141">Oluşturulan ve Azure Resource Manager kullanarak kaynakları dağıtılan göre öğrenin nasıl toomanage Bu makaleler görüntüleyerek bu kaynakları:</span><span class="sxs-lookup"><span data-stu-id="f2fd3-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="f2fd3-142">Service Bus PowerShell ile yönetme</span><span class="sxs-lookup"><span data-stu-id="f2fd3-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="f2fd3-143">Merhaba hizmet veri yolu Gezgini ile Service Bus kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="f2fd3-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
