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
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a><span data-ttu-id="73cc1-103">Bir Azure Resource Manager şablonu kullanarak bir hizmet veri yolu ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="73cc1-103">Create a Service Bus namespace using an Azure Resource Manager template</span></span>

<span data-ttu-id="73cc1-104">Nasıl bir hizmet veri yolu türünün ad alanını oluşturur toouse bir Azure Resource Manager şablonu bu makalede **ileti** standart/temel SKU ile.</span><span class="sxs-lookup"><span data-stu-id="73cc1-104">This article describes how toouse an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard/Basic SKU.</span></span> <span data-ttu-id="73cc1-105">Merhaba makale ayrıca hello dağıtım hello yürütme için belirtilen başlangıç parametreleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="73cc1-105">hello article also defines hello parameters that are specified for hello execution of hello deployment.</span></span> <span data-ttu-id="73cc1-106">Kendi dağıtımlar için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="73cc1-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="73cc1-107">Şablonları oluşturma hakkında daha fazla bilgi için lütfen bkz [Azure Resource Manager şablonları yazma][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="73cc1-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="73cc1-108">Merhaba Hello tam şablonu için bkz [hizmet veri yolu ad alanı şablonu] [ Service Bus namespace template] github'da.</span><span class="sxs-lookup"><span data-stu-id="73cc1-108">For hello complete template, see hello [Service Bus namespace template][Service Bus namespace template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="73cc1-109">Azure Resource Manager şablonları aşağıdaki hello yükleme ve dağıtım için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="73cc1-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span> 
> 
> * [<span data-ttu-id="73cc1-110">Sıra ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="73cc1-110">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="73cc1-111">Hizmet veri yolu ad alanı konu ve abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="73cc1-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="73cc1-112">Kuyruk ve yetkilendirme kuralı ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="73cc1-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="73cc1-113">Konu, abonelik ve kuralı ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="73cc1-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="73cc1-114">Merhaba son şablonları için toocheck ziyaret hello [Azure hızlı başlangıç şablonlarını] [ Azure Quickstart Templates] Galerisi ve Service Bus arayın.</span><span class="sxs-lookup"><span data-stu-id="73cc1-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="73cc1-115">Ne dağıtacaksınız?</span><span class="sxs-lookup"><span data-stu-id="73cc1-115">What will you deploy?</span></span>
<span data-ttu-id="73cc1-116">Bu şablonla, hizmet veri yolu ad alanınızla dağıtacağınız bir [temel, standart veya Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span><span class="sxs-lookup"><span data-stu-id="73cc1-116">With this template, you will deploy a Service Bus namespace with a [Basic, Standard, or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span></span>

<span data-ttu-id="73cc1-117">toorun dağıtım otomatik olarak Merhaba, düğme aşağıdaki hello tıklatın:</span><span class="sxs-lookup"><span data-stu-id="73cc1-117">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="73cc1-118">[![TooAzure dağıtma](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="73cc1-118">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="73cc1-119">Parametreler</span><span class="sxs-lookup"><span data-stu-id="73cc1-119">Parameters</span></span>
<span data-ttu-id="73cc1-120">Azure Resource Manager ile tanımladığınız parametreler için değerler hello şablon dağıtıldığında toospecify istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="73cc1-120">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="73cc1-121">Merhaba şablonu adlı bir bölüm içerir `Parameters` tüm hello parametre değerlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="73cc1-121">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="73cc1-122">Dağıttığınız hello projesini temel alan veya dağıttığınız hello ortamı dayanarak değişir bu değerleri için bir parametre tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="73cc1-122">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="73cc1-123">Her zaman kalacak değerleri aynı hello için parametreleri tanımlamayın.</span><span class="sxs-lookup"><span data-stu-id="73cc1-123">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="73cc1-124">Her parametre değeri dağıtılan hello şablonu toodefine hello kaynaklarında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="73cc1-124">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="73cc1-125">Bu şablon şu parametreler hello tanımlar.</span><span class="sxs-lookup"><span data-stu-id="73cc1-125">This template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="73cc1-126">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="73cc1-126">serviceBusNamespaceName</span></span>
<span data-ttu-id="73cc1-127">Merhaba hizmet veri yolu ad alanı toocreate Hello adı.</span><span class="sxs-lookup"><span data-stu-id="73cc1-127">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a><span data-ttu-id="73cc1-128">serviceBusSKU</span><span class="sxs-lookup"><span data-stu-id="73cc1-128">serviceBusSKU</span></span>
<span data-ttu-id="73cc1-129">Merhaba Service Bus Hello adını [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.</span><span class="sxs-lookup"><span data-stu-id="73cc1-129">hello name of hello Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.</span></span>

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

<span data-ttu-id="73cc1-130">Merhaba şablonu (temel, standart veya Premium) Bu parametre için izin verilen hello değerleri tanımlar ve herhangi bir değer belirtilmezse varsayılan değer (standart) atar.</span><span class="sxs-lookup"><span data-stu-id="73cc1-130">hello template defines hello values that are permitted for this parameter (Basic, Standard, or Premium) and assigns a default value (Standard) if no value is specified.</span></span>

<span data-ttu-id="73cc1-131">Hizmet veri yolu fiyatlandırma hakkında daha fazla bilgi için bkz: [Service fiyatlandırma ve faturalama Bus][Service Bus pricing and billing].</span><span class="sxs-lookup"><span data-stu-id="73cc1-131">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span></span>

### <a name="servicebusapiversion"></a><span data-ttu-id="73cc1-132">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="73cc1-132">serviceBusApiVersion</span></span>
<span data-ttu-id="73cc1-133">Hizmet veri yolu API'sini sürümü hello şablon Hello.</span><span class="sxs-lookup"><span data-stu-id="73cc1-133">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by hello template" 
       } 
```

## <a name="resources-toodeploy"></a><span data-ttu-id="73cc1-134">Kaynakları toodeploy</span><span class="sxs-lookup"><span data-stu-id="73cc1-134">Resources toodeploy</span></span>
### <a name="service-bus-namespace"></a><span data-ttu-id="73cc1-135">Hizmet veri yolu ad alanı</span><span class="sxs-lookup"><span data-stu-id="73cc1-135">Service Bus namespace</span></span>
<span data-ttu-id="73cc1-136">Standart bir hizmet veri yolu ad alanı türü oluşturur **ileti**.</span><span class="sxs-lookup"><span data-stu-id="73cc1-136">Creates a standard Service Bus namespace of type **Messaging**.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="73cc1-137">Komutları toorun dağıtımı</span><span class="sxs-lookup"><span data-stu-id="73cc1-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="73cc1-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="73cc1-138">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a><span data-ttu-id="73cc1-139">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="73cc1-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a><span data-ttu-id="73cc1-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="73cc1-140">Next steps</span></span>
<span data-ttu-id="73cc1-141">Oluşturulan ve Azure Resource Manager kullanarak kaynakları dağıtılan göre öğrenin nasıl toomanage bu makaleleri okuyarak bu kaynakları:</span><span class="sxs-lookup"><span data-stu-id="73cc1-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by reading these articles:</span></span>

* [<span data-ttu-id="73cc1-142">Service Bus PowerShell ile yönetme</span><span class="sxs-lookup"><span data-stu-id="73cc1-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="73cc1-143">Merhaba hizmet veri yolu Gezgini ile Service Bus kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="73cc1-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
