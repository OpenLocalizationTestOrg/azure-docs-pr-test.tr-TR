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
# <a name="create-a-service-bus-namespace-and-a-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="73a37-103">Bir hizmet veri yolu ad alanı ve bir Azure Resource Manager şablonu kullanarak bir sıra oluşturun</span><span class="sxs-lookup"><span data-stu-id="73a37-103">Create a Service Bus namespace and a queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="73a37-104">Bu makalede nasıl toouse bir Azure Resource Manager şablonunu bir hizmet veri yolu ad alanı ve bu ad alanı içindeki bir kuyruk oluşturan gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="73a37-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a queue within that namespace.</span></span> <span data-ttu-id="73a37-105">Şunları öğreneceksiniz nasıl toodefine hangi kaynağın dağıtılan ve nasıl toodefine parametreler hello dağıtım zaman yürütülür belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="73a37-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="73a37-106">Kendi dağıtımlar için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="73a37-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="73a37-107">Şablonları oluşturma hakkında daha fazla bilgi için lütfen bkz [Azure Resource Manager şablonları yazma][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="73a37-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="73a37-108">Merhaba Hello tam şablonu için bkz [hizmet veri yolu ad alanı ve sıra şablonu] [ Service Bus namespace and queue template] github'da.</span><span class="sxs-lookup"><span data-stu-id="73a37-108">For hello complete template, see hello [Service Bus namespace and queue template][Service Bus namespace and queue template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="73a37-109">Azure Resource Manager şablonları aşağıdaki hello yükleme ve dağıtım için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="73a37-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="73a37-110">Kuyruk ve yetkilendirme kuralı ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="73a37-110">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="73a37-111">Hizmet veri yolu ad alanı konu ve abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="73a37-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="73a37-112">Hizmet veri yolu ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="73a37-112">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="73a37-113">Konu, abonelik ve kuralı ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="73a37-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="73a37-114">Merhaba son şablonları için toocheck ziyaret hello [Azure hızlı başlangıç şablonlarını] [ Azure Quickstart Templates] Galerisi ve "Service Bus" için arama</span><span class="sxs-lookup"><span data-stu-id="73a37-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="73a37-115">Ne dağıtacaksınız?</span><span class="sxs-lookup"><span data-stu-id="73a37-115">What will you deploy?</span></span>

<span data-ttu-id="73a37-116">Bu şablon kullanılarak bir hizmet veri yolu ad alanı bir kuyruk dağıtır.</span><span class="sxs-lookup"><span data-stu-id="73a37-116">With this template, you will deploy a Service Bus namespace with a queue.</span></span>

<span data-ttu-id="73a37-117">[Service Bus kuyruklarını](service-bus-queues-topics-subscriptions.md#queues) ilk olarak, ilk çıkar (FIFO) ileti teslim tooone veya birden çok rakip tüketiciye sunar.</span><span class="sxs-lookup"><span data-stu-id="73a37-117">[Service Bus queues](service-bus-queues-topics-subscriptions.md#queues) offer First In, First Out (FIFO) message delivery tooone or more competing consumers.</span></span>

<span data-ttu-id="73a37-118">toorun dağıtım otomatik olarak Merhaba, düğme aşağıdaki hello tıklatın:</span><span class="sxs-lookup"><span data-stu-id="73a37-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="73a37-119">[![TooAzure dağıtma](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="73a37-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="73a37-120">Parametreler</span><span class="sxs-lookup"><span data-stu-id="73a37-120">Parameters</span></span>

<span data-ttu-id="73a37-121">Azure Resource Manager ile tanımladığınız parametreler için değerler hello şablon dağıtıldığında toospecify istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="73a37-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="73a37-122">Merhaba şablonu adlı bir bölüm içerir `Parameters` tüm hello parametre değerlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="73a37-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="73a37-123">Dağıttığınız hello projesini temel alan veya dağıttığınız hello ortamı dayanarak değişir bu değerleri için bir parametre tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="73a37-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="73a37-124">Her zaman kalacak değerleri aynı hello için parametreleri tanımlamayın.</span><span class="sxs-lookup"><span data-stu-id="73a37-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="73a37-125">Her parametre değeri dağıtılan hello şablonu toodefine hello kaynaklarında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="73a37-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="73a37-126">Merhaba şablonu şu parametreler hello tanımlar.</span><span class="sxs-lookup"><span data-stu-id="73a37-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="73a37-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="73a37-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="73a37-128">Merhaba hizmet veri yolu ad alanı toocreate Hello adı.</span><span class="sxs-lookup"><span data-stu-id="73a37-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="73a37-129">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="73a37-129">serviceBusQueueName</span></span>
<span data-ttu-id="73a37-130">Merhaba hizmet veri yolu ad alanında oluşturulan hello sırasının Hello adı.</span><span class="sxs-lookup"><span data-stu-id="73a37-130">hello name of hello queue created in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="73a37-131">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="73a37-131">serviceBusApiVersion</span></span>
<span data-ttu-id="73a37-132">Hizmet veri yolu API'sini sürümü hello şablon Hello.</span><span class="sxs-lookup"><span data-stu-id="73a37-132">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="73a37-133">Kaynakları toodeploy</span><span class="sxs-lookup"><span data-stu-id="73a37-133">Resources toodeploy</span></span>
<span data-ttu-id="73a37-134">Standart bir hizmet veri yolu ad alanı türü oluşturur **ileti**, bir kuyruk.</span><span class="sxs-lookup"><span data-stu-id="73a37-134">Creates a standard Service Bus namespace of type **Messaging**, with a queue.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="73a37-135">Komutları toorun dağıtımı</span><span class="sxs-lookup"><span data-stu-id="73a37-135">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="73a37-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="73a37-136">PowerShell</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="73a37-137">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="73a37-137">Azure CLI</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="73a37-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="73a37-138">Next steps</span></span>
<span data-ttu-id="73a37-139">Oluşturulan ve Azure Resource Manager kullanarak kaynakları dağıtılan göre öğrenin nasıl toomanage Bu makaleler görüntüleyerek bu kaynakları:</span><span class="sxs-lookup"><span data-stu-id="73a37-139">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="73a37-140">Service Bus PowerShell ile yönetme</span><span class="sxs-lookup"><span data-stu-id="73a37-140">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="73a37-141">Merhaba hizmet veri yolu Gezgini ile Service Bus kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="73a37-141">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace and queue template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus queues]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
