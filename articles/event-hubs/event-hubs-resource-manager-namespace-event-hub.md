---
title: "bir şablonu kullanarak bir Azure Event Hubs ad alanı ve tüketici grubu aaaCreate | Microsoft Docs"
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
ms.openlocfilehash: 74b0d6b3fbe848705e2c20e628aa4e5269b53edb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="93d7e-103">Bir Azure Resource Manager şablonu kullanarak olay hub'ı ve tüketici grubu ile bir olay hub'ları ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="93d7e-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="93d7e-104">Bu makalede nasıl toouse bir Azure Resource Manager şablonu, bir ad alanı türü Event Hubs bir olay hub'ı tek bir tüketici grubu oluşturur ve gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="93d7e-104">This article shows how toouse an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="93d7e-105">Merhaba gösterir makalesi nasıl toodefine hangi kaynağın dağıtılan ve nasıl olan toodefine hello dağıtım zaman yürütülür parametrelerinizi.</span><span class="sxs-lookup"><span data-stu-id="93d7e-105">hello article shows how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="93d7e-106">Kendi dağıtımlar için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi</span><span class="sxs-lookup"><span data-stu-id="93d7e-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="93d7e-107">Şablon oluşturma hakkında daha fazla bilgi için bkz. [Azure Resource Manager şablonları yazma][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="93d7e-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="93d7e-108">Merhaba Hello tam şablonu için bkz [olay hub'ı ve tüketici grubu şablonunu] [ Event Hub and consumer group template] github'da.</span><span class="sxs-lookup"><span data-stu-id="93d7e-108">For hello complete template, see hello [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="93d7e-109">Merhaba son şablonları için toocheck ziyaret hello [Azure hızlı başlangıç şablonlarını] [ Azure Quickstart Templates] Galerisi ve Event Hubs arayın.</span><span class="sxs-lookup"><span data-stu-id="93d7e-109">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="93d7e-110">Ne dağıtacaksınız?</span><span class="sxs-lookup"><span data-stu-id="93d7e-110">What will you deploy?</span></span>
<span data-ttu-id="93d7e-111">Bu şablon kullanılarak bir olay hub'ı ve bir tüketici grubu içeren bir olay hub'ları ad dağıtır.</span><span class="sxs-lookup"><span data-stu-id="93d7e-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="93d7e-112">[Olay hub'ları](event-hubs-what-is-event-hubs.md) büyük ölçekte kullanılan hizmet tooprovide olayı ve telemetri giriş tooAzure düşük gecikme süreli ve yüksek güvenilirlik işlemeyi bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="93d7e-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="93d7e-113">toorun dağıtım otomatik olarak Merhaba, düğme aşağıdaki hello tıklatın:</span><span class="sxs-lookup"><span data-stu-id="93d7e-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="93d7e-114">[![TooAzure dağıtma](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="93d7e-114">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="93d7e-115">Parametreler</span><span class="sxs-lookup"><span data-stu-id="93d7e-115">Parameters</span></span>
<span data-ttu-id="93d7e-116">Azure Resource Manager ile tanımladığınız parametreler için değerler hello şablon dağıtıldığında toospecify istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="93d7e-116">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="93d7e-117">Merhaba şablonu adlı bir bölüm içerir `Parameters` tüm hello parametre değerlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="93d7e-117">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="93d7e-118">Dağıttığınız hello projesini temel alan veya dağıttığınız hello ortamı toowhich üzerinde temel değişir bu değerleri için bir parametre tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="93d7e-118">You should define a parameter for those values that will vary, based on hello project you are deploying or based on hello environment toowhich you are deploying.</span></span> <span data-ttu-id="93d7e-119">Her zaman kalın değerleri aynı hello için parametreleri tanımlamayın.</span><span class="sxs-lookup"><span data-stu-id="93d7e-119">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="93d7e-120">Her parametre değeri hello şablonunda dağıtılan hello kaynakları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="93d7e-120">Each parameter value in hello template defines hello resources that are deployed.</span></span>

<span data-ttu-id="93d7e-121">Merhaba şablonu şu parametreler hello tanımlar:</span><span class="sxs-lookup"><span data-stu-id="93d7e-121">hello template defines hello following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="93d7e-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="93d7e-122">eventHubNamespaceName</span></span>
<span data-ttu-id="93d7e-123">Merhaba olay hub'ları ad alanı toocreate Hello adı.</span><span class="sxs-lookup"><span data-stu-id="93d7e-123">hello name of hello Event Hubs namespace toocreate.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="93d7e-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="93d7e-124">eventHubName</span></span>
<span data-ttu-id="93d7e-125">Merhaba event hub'ı hello olay hub'ları ad alanında oluşturulan Hello adı.</span><span class="sxs-lookup"><span data-stu-id="93d7e-125">hello name of hello event hub created in hello Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="93d7e-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="93d7e-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="93d7e-127">Merhaba olay hub'ı için oluşturulan hello tüketici grubu Hello adı.</span><span class="sxs-lookup"><span data-stu-id="93d7e-127">hello name of hello consumer group created for hello event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="93d7e-128">apiVersion</span><span class="sxs-lookup"><span data-stu-id="93d7e-128">apiVersion</span></span>
<span data-ttu-id="93d7e-129">Merhaba şablon Hello API sürümü.</span><span class="sxs-lookup"><span data-stu-id="93d7e-129">hello API version of hello template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="93d7e-130">Kaynakları toodeploy</span><span class="sxs-lookup"><span data-stu-id="93d7e-130">Resources toodeploy</span></span>
<span data-ttu-id="93d7e-131">Tür bir ad oluşturur **EventHubs**bir olay hub'ı ve bir tüketici grubu.</span><span class="sxs-lookup"><span data-stu-id="93d7e-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="93d7e-132">Komutları toorun dağıtımı</span><span class="sxs-lookup"><span data-stu-id="93d7e-132">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="93d7e-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="93d7e-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="93d7e-134">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="93d7e-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="93d7e-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="93d7e-135">Next steps</span></span>
<span data-ttu-id="93d7e-136">Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="93d7e-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="93d7e-137">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="93d7e-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="93d7e-138">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="93d7e-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="93d7e-139">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="93d7e-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
