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
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="3958e-103">Hizmet veri yolu ad alanı konu, aboneliği ve Azure Resource Manager şablonu kullanarak kural oluşturma</span><span class="sxs-lookup"><span data-stu-id="3958e-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="3958e-104">Bu makalede nasıl toouse bir Azure Resource Manager şablonu, bir hizmet veri yolu ad alanı bir konu, abonelik kural (Filtresi) oluşturur ve gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3958e-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="3958e-105">Hakkında bilgi edineceksiniz nasıl toodefine hangi kaynağın dağıtılan ve nasıl toodefine parametreler hello dağıtım zaman yürütülür belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="3958e-105">You learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="3958e-106">Kendi dağıtımlar için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi</span><span class="sxs-lookup"><span data-stu-id="3958e-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="3958e-107">Şablon oluşturma hakkında daha fazla bilgi için bkz. [Azure Resource Manager şablonları yazma][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="3958e-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="3958e-108">Adlandırma kuralları Azure kaynaklarını uygulama ve desenleri hakkında daha fazla bilgi için bkz: [Azure kaynakları için adlandırma kurallarını önerilen][Recommended naming conventions for Azure resources].</span><span class="sxs-lookup"><span data-stu-id="3958e-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="3958e-109">Merhaba Hello tam şablonu için bkz [konu, abonelik ve kuralı ile Service Bus ad alanı] [ Service Bus namespace with topic, subscription, and rule] şablonu.</span><span class="sxs-lookup"><span data-stu-id="3958e-109">For hello complete template, see hello [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="3958e-110">Azure Resource Manager şablonları aşağıdaki hello yükleme ve dağıtım için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3958e-110">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="3958e-111">Kuyruk ve yetkilendirme kuralı ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3958e-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="3958e-112">Sıra ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3958e-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="3958e-113">Hizmet veri yolu ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3958e-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="3958e-114">Hizmet veri yolu ad alanı konu ve abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="3958e-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="3958e-115">Merhaba son şablonları için toocheck ziyaret hello [Azure hızlı başlangıç şablonlarını] [ Azure Quickstart Templates] Galerisi ve Service Bus arayın.</span><span class="sxs-lookup"><span data-stu-id="3958e-115">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="3958e-116">Ne dağıtacaksınız?</span><span class="sxs-lookup"><span data-stu-id="3958e-116">What will you deploy?</span></span>

<span data-ttu-id="3958e-117">Bu şablon kullanılarak konu, abonelik ve kural (Filtresi) içeren bir hizmet veri yolu ad dağıtın.</span><span class="sxs-lookup"><span data-stu-id="3958e-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="3958e-118">[Service Bus konuları ve abonelikleri](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) iletişim, bir çok form sağladığınız bir *Yayınla/Abone ol* düzeni.</span><span class="sxs-lookup"><span data-stu-id="3958e-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="3958e-119">Bunun yerine konular ve abonelikler, dağıtılmış uygulamanın bileşenleri birbirleriyle doğrudan, iletişim kurmazlar kullanıldığında bir aracı gibi davranan bir konu aracılığıyla iletileri değiş. Bir abonelik tooa konu toohello konu gönderilen iletilerin kopyalarını alan sanal kuyruğa benzer.</span><span class="sxs-lookup"><span data-stu-id="3958e-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription tooa topic resembles a virtual queue that receives copies of messages that were sent toohello topic.</span></span> <span data-ttu-id="3958e-120">Abonelik filtre tooa konu içinde belirli konu aboneliği görünmelidir hangi iletilerin gönderilen toospecify sağlar.</span><span class="sxs-lookup"><span data-stu-id="3958e-120">A filter on subscription enables you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="3958e-121">Kuralları (filtreleri) nelerdir?</span><span class="sxs-lookup"><span data-stu-id="3958e-121">What are rules (filters)?</span></span>

<span data-ttu-id="3958e-122">Birçok senaryoda belirli özelliklere sahip iletileri farklı şekillerde işlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="3958e-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="3958e-123">tooenable Bu, belirli özellikleri ve değişiklikleri toothose özellikleri gerçekleştirmek abonelikleri toofind iletileri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3958e-123">tooenable this, you can configure subscriptions toofind messages that have specific properties and then perform modifications toothose properties.</span></span> <span data-ttu-id="3958e-124">Service Bus abonelikleri toohello konu gönderilen tüm iletiler görmenize rağmen yalnızca bir alt kümesini bu iletileri toohello sanal abonelik sırası kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3958e-124">Although Service Bus subscriptions see all messages sent toohello topic, you can only copy a subset of those messages toohello virtual subscription queue.</span></span> <span data-ttu-id="3958e-125">Bu, abonelik filtreleri kullanılarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3958e-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="3958e-126">toolearn kuralları (filtreleri) hakkında daha fazla bilgi görmek [kurallar ve Eylemler](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span><span class="sxs-lookup"><span data-stu-id="3958e-126">toolearn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="3958e-127">toorun dağıtım otomatik olarak Merhaba, düğme aşağıdaki hello tıklatın:</span><span class="sxs-lookup"><span data-stu-id="3958e-127">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="3958e-128">[![TooAzure dağıtma](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="3958e-128">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="3958e-129">Parametreler</span><span class="sxs-lookup"><span data-stu-id="3958e-129">Parameters</span></span>

<span data-ttu-id="3958e-130">Azure Resource Manager ile parametreleri tanımlamanız gerekir değerlerini hello şablon dağıtıldığında toospecify istiyor.</span><span class="sxs-lookup"><span data-stu-id="3958e-130">With Azure Resource Manager, you should define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="3958e-131">Merhaba şablonu adlı bir bölüm içerir `Parameters` tüm hello parametre değerlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="3958e-131">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="3958e-132">Dağıttığınız hello projesini temel alan veya dağıttığınız hello ortamı dayanarak farklılık bu değerleri için bir parametre tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3958e-132">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="3958e-133">Her zaman kalın değerleri aynı hello için parametreleri tanımlamayın.</span><span class="sxs-lookup"><span data-stu-id="3958e-133">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="3958e-134">Her parametre değeri dağıtılan hello şablonu toodefine hello kaynaklarında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3958e-134">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="3958e-135">Merhaba şablonu şu parametreler hello tanımlar:</span><span class="sxs-lookup"><span data-stu-id="3958e-135">hello template defines hello following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="3958e-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="3958e-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="3958e-137">Merhaba hizmet veri yolu ad alanı toocreate Hello adı.</span><span class="sxs-lookup"><span data-stu-id="3958e-137">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="3958e-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="3958e-138">serviceBusTopicName</span></span>
<span data-ttu-id="3958e-139">Merhaba hizmet veri yolu ad alanında oluşturulan hello konu Hello adı.</span><span class="sxs-lookup"><span data-stu-id="3958e-139">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="3958e-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="3958e-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="3958e-141">Merhaba hizmet veri yolu ad alanında oluşturulan hello abonelik Hello adı.</span><span class="sxs-lookup"><span data-stu-id="3958e-141">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="3958e-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="3958e-142">serviceBusRuleName</span></span>
<span data-ttu-id="3958e-143">Merhaba hizmet veri yolu ad alanında oluşturulan hello rule(filter) Hello adı.</span><span class="sxs-lookup"><span data-stu-id="3958e-143">hello name of hello rule(filter) created in hello Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="3958e-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="3958e-144">serviceBusApiVersion</span></span>
<span data-ttu-id="3958e-145">Hizmet veri yolu API'sini sürümü hello şablon Hello.</span><span class="sxs-lookup"><span data-stu-id="3958e-145">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="3958e-146">Kaynakları toodeploy</span><span class="sxs-lookup"><span data-stu-id="3958e-146">Resources toodeploy</span></span>
<span data-ttu-id="3958e-147">Standart bir hizmet veri yolu ad alanı türü oluşturur **ileti**, konu ve abonelik ve kuralları ile.</span><span class="sxs-lookup"><span data-stu-id="3958e-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="3958e-148">Komutları toorun dağıtımı</span><span class="sxs-lookup"><span data-stu-id="3958e-148">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="3958e-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3958e-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="3958e-150">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3958e-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="3958e-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3958e-151">Next steps</span></span>
<span data-ttu-id="3958e-152">Oluşturulan ve Azure Resource Manager kullanarak kaynakları dağıtılan göre öğrenin nasıl toomanage Bu makaleler görüntüleyerek bu kaynakları:</span><span class="sxs-lookup"><span data-stu-id="3958e-152">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="3958e-153">Azure hizmet veri yolu yönetme</span><span class="sxs-lookup"><span data-stu-id="3958e-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="3958e-154">Service Bus PowerShell ile yönetme</span><span class="sxs-lookup"><span data-stu-id="3958e-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="3958e-155">Merhaba hizmet veri yolu Gezgini ile Service Bus kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="3958e-155">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

