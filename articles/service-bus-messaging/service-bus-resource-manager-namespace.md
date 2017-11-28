---
title: "Bir Azure Resource Manager şablonu kullanarak Service Bus ad alanı oluşturma | Microsoft Docs"
description: "Bir hizmet veri yolu ad alanı oluşturmak için Azure Resource Manager şablonu kullanın"
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
ms.openlocfilehash: 8fff390919a1807995646dab322b4cbe56dd0268
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a><span data-ttu-id="8d9ec-103">Bir Azure Resource Manager şablonu kullanarak bir hizmet veri yolu ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8d9ec-103">Create a Service Bus namespace using an Azure Resource Manager template</span></span>

<span data-ttu-id="8d9ec-104">Bu makalede, bir hizmet veri yolu ad alanı türü oluşturan bir Azure Resource Manager şablonu kullanmayı açıklar **ileti** standart/temel SKU ile.</span><span class="sxs-lookup"><span data-stu-id="8d9ec-104">This article describes how to use an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard/Basic SKU.</span></span> <span data-ttu-id="8d9ec-105">Makale ayrıca dağıtım yürütme için belirtilen parametreleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8d9ec-105">The article also defines the parameters that are specified for the execution of the deployment.</span></span> <span data-ttu-id="8d9ec-106">Bu şablonu kendi dağıtımlarınız için kullanabilir veya kendi gereksinimlerinize göre özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d9ec-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="8d9ec-107">Şablonları oluşturma hakkında daha fazla bilgi için lütfen bkz [Azure Resource Manager şablonları yazma][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="8d9ec-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="8d9ec-108">Tam şablon için bkz: [hizmet veri yolu ad alanı şablonu] [ Service Bus namespace template] github'da.</span><span class="sxs-lookup"><span data-stu-id="8d9ec-108">For the complete template, see the [Service Bus namespace template][Service Bus namespace template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="8d9ec-109">Aşağıdaki Azure Resource Manager şablonları, yükleme ve dağıtım için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8d9ec-109">The following Azure Resource Manager templates are available for download and deployment.</span></span> 
> 
> * [<span data-ttu-id="8d9ec-110">Sıra ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8d9ec-110">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="8d9ec-111">Hizmet veri yolu ad alanı konu ve abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="8d9ec-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="8d9ec-112">Kuyruk ve yetkilendirme kuralı ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8d9ec-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="8d9ec-113">Konu, abonelik ve kuralı ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8d9ec-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="8d9ec-114">Son şablonları denetlemek için ziyaret edin [Azure hızlı başlangıç şablonlarını] [ Azure Quickstart Templates] Galerisi ve Service Bus arayın.</span><span class="sxs-lookup"><span data-stu-id="8d9ec-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="8d9ec-115">Ne dağıtacaksınız?</span><span class="sxs-lookup"><span data-stu-id="8d9ec-115">What will you deploy?</span></span>
<span data-ttu-id="8d9ec-116">Bu şablonla, hizmet veri yolu ad alanınızla dağıtacağınız bir [temel, standart veya Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span><span class="sxs-lookup"><span data-stu-id="8d9ec-116">With this template, you will deploy a Service Bus namespace with a [Basic, Standard, or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span></span>

<span data-ttu-id="8d9ec-117">Dağıtımı otomatik olarak çalıştırmak için aşağıdaki düğmeye tıklayın:</span><span class="sxs-lookup"><span data-stu-id="8d9ec-117">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="8d9ec-118">[![Azure’a dağıtma](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="8d9ec-118">[![Deploy to Azure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="8d9ec-119">Parametreler</span><span class="sxs-lookup"><span data-stu-id="8d9ec-119">Parameters</span></span>
<span data-ttu-id="8d9ec-120">Azure Resource Manager sayesinde, şablon dağıtıldığında belirtmek istediğiniz değerlerin parametrelerini siz tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="8d9ec-120">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="8d9ec-121">Şablon adlı bir bölüm içerir `Parameters` , tüm parametre değerlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="8d9ec-121">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="8d9ec-122">Dağıttığınız projesini temel alan veya dağıttığınız ortamı dayanarak değişir bu değerleri için bir parametre tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8d9ec-122">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="8d9ec-123">Her zaman aynı kalır değerleri parametrelerini tanımlamayın.</span><span class="sxs-lookup"><span data-stu-id="8d9ec-123">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="8d9ec-124">Her parametre değeri, dağıtılan kaynakları tanımlamak için şablonda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8d9ec-124">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="8d9ec-125">Bu şablon, aşağıdaki parametreleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8d9ec-125">This template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="8d9ec-126">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="8d9ec-126">serviceBusNamespaceName</span></span>
<span data-ttu-id="8d9ec-127">Oluşturmak için hizmet veri yolu ad alanı adı.</span><span class="sxs-lookup"><span data-stu-id="8d9ec-127">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of the Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a><span data-ttu-id="8d9ec-128">serviceBusSKU</span><span class="sxs-lookup"><span data-stu-id="8d9ec-128">serviceBusSKU</span></span>
<span data-ttu-id="8d9ec-129">Hizmet veri yolu adı [SKU](https://azure.microsoft.com/pricing/details/service-bus/) oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="8d9ec-129">The name of the Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) to create.</span></span>

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
        "description": "The messaging tier for service Bus namespace" 
    } 

```

<span data-ttu-id="8d9ec-130">Şablon (temel, standart veya Premium) Bu parametre için izin verilen değerleri tanımlar ve herhangi bir değer belirtilmezse varsayılan değer (standart) atar.</span><span class="sxs-lookup"><span data-stu-id="8d9ec-130">The template defines the values that are permitted for this parameter (Basic, Standard, or Premium) and assigns a default value (Standard) if no value is specified.</span></span>

<span data-ttu-id="8d9ec-131">Hizmet veri yolu fiyatlandırma hakkında daha fazla bilgi için bkz: [Service fiyatlandırma ve faturalama Bus][Service Bus pricing and billing].</span><span class="sxs-lookup"><span data-stu-id="8d9ec-131">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span></span>

### <a name="servicebusapiversion"></a><span data-ttu-id="8d9ec-132">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="8d9ec-132">serviceBusApiVersion</span></span>
<span data-ttu-id="8d9ec-133">Şablon hizmet veri yolu API'sini sürümü.</span><span class="sxs-lookup"><span data-stu-id="8d9ec-133">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by the template" 
       } 
```

## <a name="resources-to-deploy"></a><span data-ttu-id="8d9ec-134">Dağıtılacak kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8d9ec-134">Resources to deploy</span></span>
### <a name="service-bus-namespace"></a><span data-ttu-id="8d9ec-135">Hizmet veri yolu ad alanı</span><span class="sxs-lookup"><span data-stu-id="8d9ec-135">Service Bus namespace</span></span>
<span data-ttu-id="8d9ec-136">Standart bir hizmet veri yolu ad alanı türü oluşturur **ileti**.</span><span class="sxs-lookup"><span data-stu-id="8d9ec-136">Creates a standard Service Bus namespace of type **Messaging**.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="8d9ec-137">Dağıtımı çalıştırma komutları</span><span class="sxs-lookup"><span data-stu-id="8d9ec-137">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="8d9ec-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d9ec-138">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a><span data-ttu-id="8d9ec-139">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8d9ec-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a><span data-ttu-id="8d9ec-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8d9ec-140">Next steps</span></span>
<span data-ttu-id="8d9ec-141">Oluşturulan ve Azure Resource Manager kullanarak kaynakları dağıtılan göre bu kaynakları bu makaleleri okuyarak yönetmeyi öğrenin:</span><span class="sxs-lookup"><span data-stu-id="8d9ec-141">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by reading these articles:</span></span>

* [<span data-ttu-id="8d9ec-142">Service Bus PowerShell ile yönetme</span><span class="sxs-lookup"><span data-stu-id="8d9ec-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="8d9ec-143">Hizmet veri yolu Gezgini ile Service Bus kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="8d9ec-143">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
