---
title: "Bir şablonu kullanarak Azure'da bir mantıksal uygulama oluşturma | Microsoft Docs"
description: "İş akışları tanımlamak için bir mantıksal uygulama dağıtmak için bir Azure Resource Manager şablonunu kullanın."
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 161adeacd6da2b15225c8a4ddae171e19e539967
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-logic-app-using-a-template"></a><span data-ttu-id="d7484-103">Şablon kullanarak Logic Apps uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7484-103">Create a Logic App using a template</span></span>
<span data-ttu-id="d7484-104">Şablonları, bir mantıksal uygulama içinde farklı bağlayıcılarını kullanmak için hızlı bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="d7484-104">Templates provide a quick way to use different connectors within a logic app.</span></span> <span data-ttu-id="d7484-105">Mantıksal uygulamalar iş iş akışları tanımlamak için kullanılan bir mantıksal uygulama oluşturmak için Azure Resource Manager şablonları içerir.</span><span class="sxs-lookup"><span data-stu-id="d7484-105">Logic apps includes Azure Resource Manager templates for you to create a logic app that can be used to define business workflows.</span></span> <span data-ttu-id="d7484-106">Hangi kaynağın dağıtılan ve mantıksal uygulamanızı dağıttığınızda parametrelerini tanımlamak nasıl tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7484-106">You can define which resources are deployed, and how to define parameters when you deploy your logic app.</span></span> <span data-ttu-id="d7484-107">Bu şablon için kendi iş senaryoları kullanın veya gereksinimlerinizi karşılayacak şekilde özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d7484-107">You can use this template for your own business scenarios, or customize it to meet your requirements.</span></span>

<span data-ttu-id="d7484-108">Mantıksal uygulama özellikleri hakkında daha fazla bilgi için bkz: [mantığı uygulama iş akışı yönetimi API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span><span class="sxs-lookup"><span data-stu-id="d7484-108">For more details on the Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span></span> 

<span data-ttu-id="d7484-109">Tanımı bir örnekleri için bkz: [Yazar mantıksal uygulama tanımları](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="d7484-109">For examples of the definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md).</span></span> 

<span data-ttu-id="d7484-110">Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d7484-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="d7484-111">Tam şablon için bkz: [mantıksal uygulama şablonu](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="d7484-111">For the complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span></span>

## <a name="what-you-deploy"></a><span data-ttu-id="d7484-112">Ne dağıtma</span><span class="sxs-lookup"><span data-stu-id="d7484-112">What you deploy</span></span>
<span data-ttu-id="d7484-113">Bu şablon kullanılarak bir mantıksal uygulama dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d7484-113">With this template, you deploy a logic app.</span></span>

<span data-ttu-id="d7484-114">Dağıtımı otomatik olarak çalıştırmak için aşağıdaki düğmeye seçin:</span><span class="sxs-lookup"><span data-stu-id="d7484-114">To run the deployment automatically, select the following button:</span></span>  

<span data-ttu-id="d7484-115">[![Azure’a dağıtma](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="d7484-115">[![Deploy to Azure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="d7484-116">Parametreler</span><span class="sxs-lookup"><span data-stu-id="d7484-116">Parameters</span></span>
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a><span data-ttu-id="d7484-117">testUri</span><span class="sxs-lookup"><span data-stu-id="d7484-117">testUri</span></span>
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-to-deploy"></a><span data-ttu-id="d7484-118">Dağıtılacak kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d7484-118">Resources to deploy</span></span>
### <a name="logic-app"></a><span data-ttu-id="d7484-119">Mantıksal uygulama</span><span class="sxs-lookup"><span data-stu-id="d7484-119">Logic app</span></span>
<span data-ttu-id="d7484-120">Mantıksal uygulama oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d7484-120">Creates the logic app.</span></span>

<span data-ttu-id="d7484-121">Şablonlar mantığı uygulama adı için bir parametre değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="d7484-121">The templates uses a parameter value for the logic app name.</span></span> <span data-ttu-id="d7484-122">Kaynak grubu olarak aynı konuma mantıksal uygulama konumunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d7484-122">It sets the location of the logic app to the same location as the resource group.</span></span> 

<span data-ttu-id="d7484-123">Bu belirli tanımını saatte bir kez çalıştırır ve belirttiğiniz konuma ping **testUri** parametresi.</span><span class="sxs-lookup"><span data-stu-id="d7484-123">This particular definition runs once an hour, and pings the location specified in the **testUri** parameter.</span></span> 

    {
      "type": "Microsoft.Logic/workflows",
      "apiVersion": "2016-06-01",
      "name": "[parameters('logicAppName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "LogicApp"
      },
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      }
    }


## <a name="commands-to-run-deployment"></a><span data-ttu-id="d7484-124">Dağıtımı çalıştırma komutları</span><span class="sxs-lookup"><span data-stu-id="d7484-124">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="d7484-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7484-125">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="d7484-126">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d7484-126">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



