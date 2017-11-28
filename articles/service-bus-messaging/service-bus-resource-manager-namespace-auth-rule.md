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
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="4a828-103">Ad alanı ve bir Azure Resource Manager şablonu kullanarak sıra için bir hizmet veri yolu yetkilendirme kuralı oluştur</span><span class="sxs-lookup"><span data-stu-id="4a828-103">Create a Service Bus authorization rule for namespace and queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="4a828-104">Bu makalede gösterilmektedir nasıl toouse bir Azure Resource Manager şablonu oluşturan bir [yetkilendirme kuralı](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) için bir hizmet veri yolu ad alanı ve sıra.</span><span class="sxs-lookup"><span data-stu-id="4a828-104">This article shows how toouse an Azure Resource Manager template that creates an [authorization rule](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) for a Service Bus namespace and queue.</span></span> <span data-ttu-id="4a828-105">Şunları öğreneceksiniz nasıl toodefine hangi kaynağın dağıtılan ve nasıl toodefine parametreler hello dağıtım zaman yürütülür belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="4a828-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="4a828-106">Kendi dağıtımlar için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="4a828-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="4a828-107">Şablonları oluşturma hakkında daha fazla bilgi için lütfen bkz [Azure Resource Manager şablonları yazma][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="4a828-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="4a828-108">Merhaba Hello tam şablonu için bkz [Service Bus yetkilendirme kuralı şablonunu] [ Service Bus auth rule template] github'da.</span><span class="sxs-lookup"><span data-stu-id="4a828-108">For hello complete template, see hello [Service Bus authorization rule template][Service Bus auth rule template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="4a828-109">Azure Resource Manager şablonları aşağıdaki hello yükleme ve dağıtım için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4a828-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="4a828-110">Hizmet veri yolu ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4a828-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="4a828-111">Sıra ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4a828-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="4a828-112">Hizmet veri yolu ad alanı konu ve abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="4a828-112">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="4a828-113">Konu, abonelik ve kuralı ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4a828-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="4a828-114">Merhaba son şablonları için toocheck ziyaret hello [Azure hızlı başlangıç şablonlarını] [ Azure Quickstart Templates] Galerisi ve "Service Bus" için arama</span><span class="sxs-lookup"><span data-stu-id="4a828-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="4a828-115">Ne dağıtacaksınız?</span><span class="sxs-lookup"><span data-stu-id="4a828-115">What will you deploy?</span></span>
<span data-ttu-id="4a828-116">Bu şablon kullanılarak bir hizmet veri yolu yetkilendirme kuralı için bir ad alanı ve mesajlaşma varlığıyla (Bu durumda, bir kuyruktaki) dağıtır.</span><span class="sxs-lookup"><span data-stu-id="4a828-116">With this template, you will deploy a Service Bus authorization rule for a namespace and messaging entity (in this case, a queue).</span></span>

<span data-ttu-id="4a828-117">Bu şablonu kullanan [paylaşılan erişim imzası (SAS)](service-bus-sas.md) kimlik doğrulaması için.</span><span class="sxs-lookup"><span data-stu-id="4a828-117">This template uses [Shared Access Signature (SAS)](service-bus-sas.md) for authentication.</span></span> <span data-ttu-id="4a828-118">SAS uygulamaları tooauthenticate tooService hello ad alanı veya belirli hakları ilişkili olan varlık (kuyruk veya konu) Mesajlaşma hello yapılandırılmış bir erişim anahtarı kullanarak veri yolu sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a828-118">SAS enables applications tooauthenticate tooService Bus using an access key configured on hello namespace, or on hello messaging entity (queue or topic) with which specific rights are associated.</span></span> <span data-ttu-id="4a828-119">Daha sonra bu anahtar toogenerate istemcileri tooauthenticate tooService Bus sırayla kullanabileceğiniz bir SAS belirteci kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a828-119">You can then use this key toogenerate a SAS token that clients can in turn use tooauthenticate tooService Bus.</span></span>

<span data-ttu-id="4a828-120">toorun dağıtım otomatik olarak Merhaba, düğme aşağıdaki hello tıklatın:</span><span class="sxs-lookup"><span data-stu-id="4a828-120">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="4a828-121">[![TooAzure dağıtma](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="4a828-121">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="4a828-122">Parametreler</span><span class="sxs-lookup"><span data-stu-id="4a828-122">Parameters</span></span>

<span data-ttu-id="4a828-123">Azure Resource Manager ile tanımladığınız parametreler için değerler hello şablon dağıtıldığında toospecify istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="4a828-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="4a828-124">Merhaba şablonu adlı bir bölüm içerir `Parameters` tüm hello parametre değerlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="4a828-124">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="4a828-125">Dağıttığınız hello projesini temel alan veya dağıttığınız hello ortamı dayanarak değişir bu değerleri için bir parametre tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4a828-125">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="4a828-126">Her zaman kalacak değerleri aynı hello için parametreleri tanımlamayın.</span><span class="sxs-lookup"><span data-stu-id="4a828-126">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="4a828-127">Her parametre değeri dağıtılan hello şablonu toodefine hello kaynaklarında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4a828-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="4a828-128">Merhaba şablonu şu parametreler hello tanımlar.</span><span class="sxs-lookup"><span data-stu-id="4a828-128">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="4a828-129">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="4a828-129">serviceBusNamespaceName</span></span>
<span data-ttu-id="4a828-130">Merhaba hizmet veri yolu ad alanı toocreate Hello adı.</span><span class="sxs-lookup"><span data-stu-id="4a828-130">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="namespaceauthorizationrulename"></a><span data-ttu-id="4a828-131">namespaceAuthorizationRuleName</span><span class="sxs-lookup"><span data-stu-id="4a828-131">namespaceAuthorizationRuleName</span></span>
<span data-ttu-id="4a828-132">Merhaba Yetkilendirme kuralının adını Hello hello ad alanı için.</span><span class="sxs-lookup"><span data-stu-id="4a828-132">hello name of hello authorization rule for hello namespace.</span></span>

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="4a828-133">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="4a828-133">serviceBusQueueName</span></span>
<span data-ttu-id="4a828-134">Merhaba Service Bus ad alanı hello sırada Hello adı.</span><span class="sxs-lookup"><span data-stu-id="4a828-134">hello name of hello queue in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="4a828-135">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="4a828-135">serviceBusApiVersion</span></span>
<span data-ttu-id="4a828-136">Hizmet veri yolu API'sini sürümü hello şablon Hello.</span><span class="sxs-lookup"><span data-stu-id="4a828-136">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="4a828-137">Kaynakları toodeploy</span><span class="sxs-lookup"><span data-stu-id="4a828-137">Resources toodeploy</span></span>
<span data-ttu-id="4a828-138">Standart bir hizmet veri yolu ad alanı türü oluşturur **ileti**ve ad alanı ve varlık için bir hizmet veri yolu yetkilendirme kuralı.</span><span class="sxs-lookup"><span data-stu-id="4a828-138">Creates a standard Service Bus namespace of type **Messaging**, and a Service Bus authorization rule for namespace and entity.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="4a828-139">Komutları toorun dağıtımı</span><span class="sxs-lookup"><span data-stu-id="4a828-139">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="4a828-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a828-140">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="4a828-141">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4a828-141">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="4a828-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4a828-142">Next steps</span></span>
<span data-ttu-id="4a828-143">Oluşturulan ve Azure Resource Manager kullanarak kaynakları dağıtılan göre öğrenin nasıl toomanage Bu makaleler görüntüleyerek bu kaynakları:</span><span class="sxs-lookup"><span data-stu-id="4a828-143">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="4a828-144">Service Bus PowerShell ile yönetme</span><span class="sxs-lookup"><span data-stu-id="4a828-144">Manage Service Bus with PowerShell</span></span>](service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="4a828-145">Merhaba hizmet veri yolu Gezgini ile Service Bus kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="4a828-145">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [<span data-ttu-id="4a828-146">Hizmet veri yolu kimlik doğrulama ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="4a828-146">Service Bus authentication and authorization</span></span>](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
