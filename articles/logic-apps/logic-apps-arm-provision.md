---
title: "bir şablonu kullanarak Azure'da bir mantıksal uygulama aaaCreate | Microsoft Docs"
description: "Azure Resource Manager şablonu toodeploy bir mantıksal uygulama iş akışları tanımlamak için kullanın."
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
ms.openlocfilehash: efbacb534fc7f11e9b593aae4383480ce3a1752f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-logic-app-using-a-template"></a><span data-ttu-id="60983-103">Şablon kullanarak Logic Apps uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="60983-103">Create a Logic App using a template</span></span>
<span data-ttu-id="60983-104">Şablonları, bir mantıksal uygulama içinde farklı bağlayıcıları hızlı şekilde toouse sağlar.</span><span class="sxs-lookup"><span data-stu-id="60983-104">Templates provide a quick way toouse different connectors within a logic app.</span></span> <span data-ttu-id="60983-105">Logic apps kullanılan toodefine iş iş akışları bir mantıksal uygulama toocreate için Azure Resource Manager şablonları içerir.</span><span class="sxs-lookup"><span data-stu-id="60983-105">Logic apps includes Azure Resource Manager templates for you toocreate a logic app that can be used toodefine business workflows.</span></span> <span data-ttu-id="60983-106">Hangi kaynağın dağıtılan, tanımlamak ve nasıl mantıksal uygulamanızı dağıttığınızda toodefine parametreleri.</span><span class="sxs-lookup"><span data-stu-id="60983-106">You can define which resources are deployed, and how toodefine parameters when you deploy your logic app.</span></span> <span data-ttu-id="60983-107">Kendi iş senaryoları için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="60983-107">You can use this template for your own business scenarios, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="60983-108">Merhaba mantıksal uygulama özellikleri hakkında daha fazla bilgi için bkz: [mantığı uygulama iş akışı yönetimi API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span><span class="sxs-lookup"><span data-stu-id="60983-108">For more details on hello Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span></span> 

<span data-ttu-id="60983-109">Merhaba tanımı kendisini örnekler için bkz: [Yazar mantıksal uygulama tanımları](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="60983-109">For examples of hello definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md).</span></span> 

<span data-ttu-id="60983-110">Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="60983-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="60983-111">Merhaba tam şablonu için bkz: [mantıksal uygulama şablonu](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="60983-111">For hello complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span></span>

## <a name="what-you-deploy"></a><span data-ttu-id="60983-112">Ne dağıtma</span><span class="sxs-lookup"><span data-stu-id="60983-112">What you deploy</span></span>
<span data-ttu-id="60983-113">Bu şablon kullanılarak bir mantıksal uygulama dağıtın.</span><span class="sxs-lookup"><span data-stu-id="60983-113">With this template, you deploy a logic app.</span></span>

<span data-ttu-id="60983-114">toorun hello dağıtım otomatik olarak düğmesi aşağıdaki hello seçin:</span><span class="sxs-lookup"><span data-stu-id="60983-114">toorun hello deployment automatically, select hello following button:</span></span>  

<span data-ttu-id="60983-115">[![TooAzure dağıtma](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="60983-115">[![Deploy tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="60983-116">Parametreler</span><span class="sxs-lookup"><span data-stu-id="60983-116">Parameters</span></span>
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a><span data-ttu-id="60983-117">testUri</span><span class="sxs-lookup"><span data-stu-id="60983-117">testUri</span></span>
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-toodeploy"></a><span data-ttu-id="60983-118">Kaynakları toodeploy</span><span class="sxs-lookup"><span data-stu-id="60983-118">Resources toodeploy</span></span>
### <a name="logic-app"></a><span data-ttu-id="60983-119">Mantıksal uygulama</span><span class="sxs-lookup"><span data-stu-id="60983-119">Logic app</span></span>
<span data-ttu-id="60983-120">Merhaba mantıksal uygulama oluşturur.</span><span class="sxs-lookup"><span data-stu-id="60983-120">Creates hello logic app.</span></span>

<span data-ttu-id="60983-121">Merhaba şablonları hello mantığı uygulama adı için bir parametre değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="60983-121">hello templates uses a parameter value for hello logic app name.</span></span> <span data-ttu-id="60983-122">Merhaba mantığı uygulama toohello hello konumunu ayarlar hello kaynak grubu olarak aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="60983-122">It sets hello location of hello logic app toohello same location as hello resource group.</span></span> 

<span data-ttu-id="60983-123">Bu belirli tanımını saatte bir kez çalıştırır ve ping hello hello belirtilen konuma **testUri** parametresi.</span><span class="sxs-lookup"><span data-stu-id="60983-123">This particular definition runs once an hour, and pings hello location specified in hello **testUri** parameter.</span></span> 

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


## <a name="commands-toorun-deployment"></a><span data-ttu-id="60983-124">Komutları toorun dağıtımı</span><span class="sxs-lookup"><span data-stu-id="60983-124">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="60983-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="60983-125">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="60983-126">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="60983-126">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



