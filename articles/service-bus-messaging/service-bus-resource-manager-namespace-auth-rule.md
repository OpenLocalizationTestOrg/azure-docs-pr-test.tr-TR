---
title: "Azure Resource Manager şablonu kullanarak Service Bus yetkilendirme kuralını | Microsoft Docs"
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
ms.openlocfilehash: fbd2372829a1aefa2c080c0a8a72b9ff4375b16f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="fc63d-103">Ad alanı ve bir Azure Resource Manager şablonu kullanarak sıra için bir hizmet veri yolu yetkilendirme kuralı oluştur</span><span class="sxs-lookup"><span data-stu-id="fc63d-103">Create a Service Bus authorization rule for namespace and queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="fc63d-104">Bu makalede oluşturan bir Azure Resource Manager şablonu kullanmayı gösterir bir [yetkilendirme kuralı](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) için bir hizmet veri yolu ad alanı ve sıra.</span><span class="sxs-lookup"><span data-stu-id="fc63d-104">This article shows how to use an Azure Resource Manager template that creates an [authorization rule](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) for a Service Bus namespace and queue.</span></span> <span data-ttu-id="fc63d-105">Nasıl tanımlamak için hangi kaynağın dağıtılan ve ne zaman dağıtım yürütülen parametreler tanımlamak nasıl belirtilen öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="fc63d-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="fc63d-106">Bu şablonu kendi dağıtımlarınız için kullanabilir veya kendi gereksinimlerinize göre özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc63d-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="fc63d-107">Şablonları oluşturma hakkında daha fazla bilgi için lütfen bkz [Azure Resource Manager şablonları yazma][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="fc63d-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="fc63d-108">Tam şablon için bkz: [Service Bus yetkilendirme kuralı şablonunu] [ Service Bus auth rule template] github'da.</span><span class="sxs-lookup"><span data-stu-id="fc63d-108">For the complete template, see the [Service Bus authorization rule template][Service Bus auth rule template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="fc63d-109">Aşağıdaki Azure Resource Manager şablonları, yükleme ve dağıtım için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fc63d-109">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="fc63d-110">Hizmet veri yolu ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc63d-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="fc63d-111">Sıra ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc63d-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="fc63d-112">Hizmet veri yolu ad alanı konu ve abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc63d-112">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="fc63d-113">Konu, abonelik ve kuralı ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc63d-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="fc63d-114">Son şablonları denetlemek için ziyaret edin [Azure hızlı başlangıç şablonlarını] [ Azure Quickstart Templates] Galerisi ve "Service Bus" için arama</span><span class="sxs-lookup"><span data-stu-id="fc63d-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="fc63d-115">Ne dağıtacaksınız?</span><span class="sxs-lookup"><span data-stu-id="fc63d-115">What will you deploy?</span></span>
<span data-ttu-id="fc63d-116">Bu şablon kullanılarak bir hizmet veri yolu yetkilendirme kuralı için bir ad alanı ve mesajlaşma varlığıyla (Bu durumda, bir kuyruktaki) dağıtır.</span><span class="sxs-lookup"><span data-stu-id="fc63d-116">With this template, you will deploy a Service Bus authorization rule for a namespace and messaging entity (in this case, a queue).</span></span>

<span data-ttu-id="fc63d-117">Bu şablonu kullanan [paylaşılan erişim imzası (SAS)](service-bus-sas.md) kimlik doğrulaması için.</span><span class="sxs-lookup"><span data-stu-id="fc63d-117">This template uses [Shared Access Signature (SAS)](service-bus-sas.md) for authentication.</span></span> <span data-ttu-id="fc63d-118">SAS hizmet veri yolu ad alanı veya belirli haklar ilişkili Mesajlaşma varlığıyla (kuyruk veya konu) yapılandırılmış bir erişim anahtarı kullanarak kimlik doğrulaması uygulamaları etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="fc63d-118">SAS enables applications to authenticate to Service Bus using an access key configured on the namespace, or on the messaging entity (queue or topic) with which specific rights are associated.</span></span> <span data-ttu-id="fc63d-119">Bu anahtar ardından istemcilerin sırayla Service Bus kimlik doğrulaması yapmak için kullanabileceği bir SAS belirteci oluşturmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc63d-119">You can then use this key to generate a SAS token that clients can in turn use to authenticate to Service Bus.</span></span>

<span data-ttu-id="fc63d-120">Dağıtımı otomatik olarak çalıştırmak için aşağıdaki düğmeye tıklayın:</span><span class="sxs-lookup"><span data-stu-id="fc63d-120">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="fc63d-121">[![Azure’a dağıtma](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="fc63d-121">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="fc63d-122">Parametreler</span><span class="sxs-lookup"><span data-stu-id="fc63d-122">Parameters</span></span>

<span data-ttu-id="fc63d-123">Azure Resource Manager sayesinde, şablon dağıtıldığında belirtmek istediğiniz değerlerin parametrelerini siz tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="fc63d-123">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="fc63d-124">Şablon adlı bir bölüm içerir `Parameters` , tüm parametre değerlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="fc63d-124">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="fc63d-125">Dağıttığınız projesini temel alan veya dağıttığınız ortamı dayanarak değişir bu değerleri için bir parametre tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc63d-125">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="fc63d-126">Her zaman aynı kalır değerleri parametrelerini tanımlamayın.</span><span class="sxs-lookup"><span data-stu-id="fc63d-126">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="fc63d-127">Her parametre değeri, dağıtılan kaynakları tanımlamak için şablonda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fc63d-127">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="fc63d-128">Şablon aşağıdaki parametreleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="fc63d-128">The template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="fc63d-129">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="fc63d-129">serviceBusNamespaceName</span></span>
<span data-ttu-id="fc63d-130">Oluşturmak için hizmet veri yolu ad alanı adı.</span><span class="sxs-lookup"><span data-stu-id="fc63d-130">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="namespaceauthorizationrulename"></a><span data-ttu-id="fc63d-131">namespaceAuthorizationRuleName</span><span class="sxs-lookup"><span data-stu-id="fc63d-131">namespaceAuthorizationRuleName</span></span>
<span data-ttu-id="fc63d-132">Yetkilendirme kuralı adı ad.</span><span class="sxs-lookup"><span data-stu-id="fc63d-132">The name of the authorization rule for the namespace.</span></span>

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="fc63d-133">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="fc63d-133">serviceBusQueueName</span></span>
<span data-ttu-id="fc63d-134">Hizmet veri yolu ad alanında kuyruk adı.</span><span class="sxs-lookup"><span data-stu-id="fc63d-134">The name of the queue in the Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="fc63d-135">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="fc63d-135">serviceBusApiVersion</span></span>
<span data-ttu-id="fc63d-136">Şablon hizmet veri yolu API'sini sürümü.</span><span class="sxs-lookup"><span data-stu-id="fc63d-136">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="fc63d-137">Dağıtılacak kaynaklar</span><span class="sxs-lookup"><span data-stu-id="fc63d-137">Resources to deploy</span></span>
<span data-ttu-id="fc63d-138">Standart bir hizmet veri yolu ad alanı türü oluşturur **ileti**ve ad alanı ve varlık için bir hizmet veri yolu yetkilendirme kuralı.</span><span class="sxs-lookup"><span data-stu-id="fc63d-138">Creates a standard Service Bus namespace of type **Messaging**, and a Service Bus authorization rule for namespace and entity.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="fc63d-139">Dağıtımı çalıştırma komutları</span><span class="sxs-lookup"><span data-stu-id="fc63d-139">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="fc63d-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc63d-140">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="fc63d-141">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fc63d-141">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="fc63d-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fc63d-142">Next steps</span></span>
<span data-ttu-id="fc63d-143">Oluşturulan ve Azure Resource Manager kullanarak kaynakları dağıtılan göre bu kaynakları Bu makaleler görüntüleyerek yönetmeyi öğrenin:</span><span class="sxs-lookup"><span data-stu-id="fc63d-143">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="fc63d-144">Service Bus PowerShell ile yönetme</span><span class="sxs-lookup"><span data-stu-id="fc63d-144">Manage Service Bus with PowerShell</span></span>](service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="fc63d-145">Hizmet veri yolu Gezgini ile Service Bus kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="fc63d-145">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [<span data-ttu-id="fc63d-146">Hizmet veri yolu kimlik doğrulama ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="fc63d-146">Service Bus authentication and authorization</span></span>](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
