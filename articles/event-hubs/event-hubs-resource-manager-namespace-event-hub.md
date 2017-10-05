---
title: "Bir şablonu kullanarak bir Azure Event Hubs ad alanı ve tüketici grubu oluşturun | Microsoft Docs"
description: "Azure Resource Manager şablonları kullanarak bir tüketici grubu ve bir event hub ile Event Hubs ad alanı oluşturma"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 28bb4591-1fd7-444f-a327-4e67e8878798
ms.service: event-hubs
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/12/2017
ms.author: sethm;shvija
ms.openlocfilehash: eb9a80eec0326aaa605cb8b21aecbaeec94ff212
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="a0f51-103">Bir Azure Resource Manager şablonu kullanarak olay hub'ı ve tüketici grubu ile bir olay hub'ları ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a0f51-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="a0f51-104">Bu makalede bir olay hub ile Event Hubs türünde bir ad ve bir tüketici grubu oluşturur bir Azure Resource Manager şablonu kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="a0f51-104">This article shows how to use an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="a0f51-105">Makaleyi nasıl tanımlamak için hangi kaynağın dağıtılan ve ne zaman dağıtım yürütülen parametreler tanımlamak nasıl belirtilen gösterir.</span><span class="sxs-lookup"><span data-stu-id="a0f51-105">The article shows how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="a0f51-106">Bu şablonu kendi dağıtımlarınız için kullanabilir veya kendi gereksinimlerinize göre özelleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a0f51-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="a0f51-107">Şablon oluşturma hakkında daha fazla bilgi için bkz. [Azure Resource Manager şablonları yazma][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="a0f51-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="a0f51-108">Tam şablon için bkz: [olay hub'ı ve tüketici grubu şablonunu] [ Event Hub and consumer group template] github'da.</span><span class="sxs-lookup"><span data-stu-id="a0f51-108">For the complete template, see the [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="a0f51-109">En yeni şablonları denetlemek için [Azure Hızlı Başlangıç Şablonları][Azure Quickstart Templates] galerisini ziyaret edin ve Event Hubs araması yapın.</span><span class="sxs-lookup"><span data-stu-id="a0f51-109">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="a0f51-110">Ne dağıtacaksınız?</span><span class="sxs-lookup"><span data-stu-id="a0f51-110">What will you deploy?</span></span>
<span data-ttu-id="a0f51-111">Bu şablon kullanılarak bir olay hub'ı ve bir tüketici grubu içeren bir olay hub'ları ad dağıtır.</span><span class="sxs-lookup"><span data-stu-id="a0f51-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="a0f51-112">[Event Hubs](event-hubs-what-is-event-hubs.md), düşük gecikme süresi ve yüksek güvenilirlikle Azure’a büyük ölçekte olay ve telemetri girişi sağlayan bir olay işleme hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="a0f51-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used to provide event and telemetry ingress to Azure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="a0f51-113">Dağıtımı otomatik olarak çalıştırmak için aşağıdaki düğmeye tıklayın:</span><span class="sxs-lookup"><span data-stu-id="a0f51-113">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="a0f51-114">[![Azure’a dağıtma](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="a0f51-114">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="a0f51-115">Parametreler</span><span class="sxs-lookup"><span data-stu-id="a0f51-115">Parameters</span></span>
<span data-ttu-id="a0f51-116">Azure Resource Manager sayesinde, şablon dağıtıldığında belirtmek istediğiniz değerlerin parametrelerini siz tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="a0f51-116">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="a0f51-117">Şablon, tüm parametre değerlerini içeren `Parameters` adlı bir bölüm içerir.</span><span class="sxs-lookup"><span data-stu-id="a0f51-117">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="a0f51-118">Dağıttığınız projesini temel alan veya dağıtmakta olduğunuz ortamına bağlı olarak değişir bu değerleri için bir parametre tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a0f51-118">You should define a parameter for those values that will vary, based on the project you are deploying or based on the environment to which you are deploying.</span></span> <span data-ttu-id="a0f51-119">Her zaman aynı kalan değerler için parametre tanımlamayın.</span><span class="sxs-lookup"><span data-stu-id="a0f51-119">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="a0f51-120">Her parametre değeri şablondaki dağıtılan kaynakları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a0f51-120">Each parameter value in the template defines the resources that are deployed.</span></span>

<span data-ttu-id="a0f51-121">Şablon aşağıdaki parametreleri tanımlar:</span><span class="sxs-lookup"><span data-stu-id="a0f51-121">The template defines the following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="a0f51-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="a0f51-122">eventHubNamespaceName</span></span>
<span data-ttu-id="a0f51-123">Oluşturulacak Event Hubs ad alanının adı.</span><span class="sxs-lookup"><span data-stu-id="a0f51-123">The name of the Event Hubs namespace to create.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="a0f51-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="a0f51-124">eventHubName</span></span>
<span data-ttu-id="a0f51-125">Event Hubs ad alanında oluşturulan olay hub’ının adı.</span><span class="sxs-lookup"><span data-stu-id="a0f51-125">The name of the event hub created in the Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="a0f51-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="a0f51-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="a0f51-127">Olay hub'ı için oluşturulan tüketici grubu adı.</span><span class="sxs-lookup"><span data-stu-id="a0f51-127">The name of the consumer group created for the event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="a0f51-128">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a0f51-128">apiVersion</span></span>
<span data-ttu-id="a0f51-129">Şablonun API sürümü.</span><span class="sxs-lookup"><span data-stu-id="a0f51-129">The API version of the template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="a0f51-130">Dağıtılacak kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a0f51-130">Resources to deploy</span></span>
<span data-ttu-id="a0f51-131">Tür bir ad oluşturur **EventHubs**bir olay hub'ı ve bir tüketici grubu.</span><span class="sxs-lookup"><span data-stu-id="a0f51-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('namespaceName')]",
         "type":"Microsoft.EventHub/namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]"
               },
               "resources":[  
                  {  
                     "apiVersion":"[variables('ehVersion')]",
                     "name":"[parameters('consumerGroupName')]",
                     "type":"ConsumerGroups",
                     "dependsOn":[  
                        "[parameters('eventHubName')]"
                     ],
                     "properties":{  

                     }
                  }
               ]
            }
         ]
      }
   ],
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="a0f51-132">Dağıtımı çalıştırma komutları</span><span class="sxs-lookup"><span data-stu-id="a0f51-132">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="a0f51-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0f51-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="a0f51-134">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a0f51-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="a0f51-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a0f51-135">Next steps</span></span>
<span data-ttu-id="a0f51-136">Aşağıdaki bağlantıları inceleyerek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a0f51-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="a0f51-137">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="a0f51-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="a0f51-138">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a0f51-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="a0f51-139">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="a0f51-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
