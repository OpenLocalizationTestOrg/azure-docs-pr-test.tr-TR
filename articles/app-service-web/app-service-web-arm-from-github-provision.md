---
title: "aaaDeploy, bir web uygulamasını tooa GitHub deposunu bağlı | Microsoft Docs"
description: "Azure Resource Manager şablonu toodeploy Github'da depodan bir proje içeren bir web uygulaması kullanın."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 32739607-85fe-43c8-a4dc-1feb46d93a4d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: 8b23416c4c06a60991517e6ee4cd82bebc5a9d73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a><span data-ttu-id="fcede-103">Bir web bağlantılı uygulama tooa GitHub deposunu dağıtma</span><span class="sxs-lookup"><span data-stu-id="fcede-103">Deploy a web app linked tooa GitHub repository</span></span>
<span data-ttu-id="fcede-104">Bu konuda, nasıl toocreate, bir web uygulamasını dağıtan bir Azure Resource Manager şablonu GitHub deposunu tooa projesinde bağlı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="fcede-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys a web app that is linked tooa project in a GitHub repository.</span></span> <span data-ttu-id="fcede-105">Şunları öğreneceksiniz nasıl toodefine hangi kaynağın dağıtılan ve nasıl toodefine parametreler hello dağıtım zaman yürütülür belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="fcede-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="fcede-106">Kendi dağıtımlar için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="fcede-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="fcede-107">Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fcede-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="fcede-108">Merhaba tam şablonu için bkz: [Web uygulaması bağlantılı tooGitHub şablon](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="fcede-108">For hello complete template, see [Web App Linked tooGitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="fcede-109">Dağıtmak</span><span class="sxs-lookup"><span data-stu-id="fcede-109">What you will deploy</span></span>
<span data-ttu-id="fcede-110">Bu şablon kullanılarak, github'da bir projeden hello kodu içeren bir web uygulaması dağıtır.</span><span class="sxs-lookup"><span data-stu-id="fcede-110">With this template, you will deploy a web app that contains hello code from a project in GitHub.</span></span>

<span data-ttu-id="fcede-111">toorun dağıtım otomatik olarak Merhaba, düğme aşağıdaki hello tıklatın:</span><span class="sxs-lookup"><span data-stu-id="fcede-111">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="fcede-112">[![TooAzure dağıtma](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="fcede-112">[![Deploy tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="fcede-113">Parametreler</span><span class="sxs-lookup"><span data-stu-id="fcede-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="fcede-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="fcede-114">repoURL</span></span>
<span data-ttu-id="fcede-115">Merhaba proje toodeploy içeren GitHub deposunu Hello URL'si.</span><span class="sxs-lookup"><span data-stu-id="fcede-115">hello URL for GitHub repository that contains hello project toodeploy.</span></span> <span data-ttu-id="fcede-116">Bu parametre bir varsayılan değer içeriyor ancak bu değer yalnızca hedeflenen tooshow, nasıl tooprovide hello URL için depo.</span><span class="sxs-lookup"><span data-stu-id="fcede-116">This parameter contains a default value but this value is only intended tooshow you how tooprovide hello URL for repository.</span></span> <span data-ttu-id="fcede-117">Merhaba şablon ancak test tooprovide hello URL kendi depo hello şablonla çalışırken istediğinizde, bu değeri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcede-117">You can use this value when testing hello template but you will want tooprovide hello URL your own repository when working with hello template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="fcede-118">Dal</span><span class="sxs-lookup"><span data-stu-id="fcede-118">branch</span></span>
<span data-ttu-id="fcede-119">Merhaba Uygulama dağıtırken hello depo toouse dalı Hello.</span><span class="sxs-lookup"><span data-stu-id="fcede-119">hello branch of hello repository toouse when deploying hello application.</span></span> <span data-ttu-id="fcede-120">Merhaba varsayılan değer ana ancak toodeploy istediğiniz herhangi bir dal hello deposundaki hello adını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcede-120">hello default value is master, but you can provide hello name of any branch in hello repository that you wish toodeploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="fcede-121">Kaynakları toodeploy</span><span class="sxs-lookup"><span data-stu-id="fcede-121">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="fcede-122">Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="fcede-122">Web app</span></span>
<span data-ttu-id="fcede-123">Github'da bağlantılı toohello projedir hello web uygulamasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fcede-123">Creates hello web app that is linked toohello project in GitHub.</span></span> 

<span data-ttu-id="fcede-124">Merhaba aracılığıyla hello web uygulamasının hello adı belirtin **siteName** parametre ve hello web uygulaması hello aracılığıyla hello konumunu **siteLocation** parametresi.</span><span class="sxs-lookup"><span data-stu-id="fcede-124">You specify hello name of hello web app through hello **siteName** parameter, and hello location of hello web app through hello **siteLocation** parameter.</span></span> <span data-ttu-id="fcede-125">Merhaba, **dependsOn** öğesi hello şablonu tanımlar hello web uygulaması hello service barındırma planı bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="fcede-125">In hello **dependsOn** element, hello template defines hello web app as dependent on hello service hosting plan.</span></span> <span data-ttu-id="fcede-126">Barındırma planı hello üzerinde bağımlı olduğundan, oluşturulmakta hello barındırma planı tamamlanana kadar hello web uygulaması oluşturulamadı.</span><span class="sxs-lookup"><span data-stu-id="fcede-126">Because it is dependent on hello hosting plan, hello web app is not created until hello hosting plan has finished being created.</span></span> <span data-ttu-id="fcede-127">Merhaba **dependsOn** yalnızca kullanılan toospecify dağıtım sırası bir öğedir.</span><span class="sxs-lookup"><span data-stu-id="fcede-127">hello **dependsOn** element is only used toospecify deployment order.</span></span> <span data-ttu-id="fcede-128">Merhaba web uygulaması hello barındırma planı bağlı olarak işaretlemezseniz, Azure kaynak yöneticisi her iki kaynağın toocreate deneyecek hello web uygulaması barındırma planı hello önce oluşturulduysa hello aynı saat ve bir hata iletisi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcede-128">If you do not mark hello web app as dependent on hello hosting plan, Azure Resource Mananger will attempt toocreate both resources at hello same time and you may receive an error if hello web app is created before hello hosting plan.</span></span>

<span data-ttu-id="fcede-129">Hello web uygulaması da içinde tanımlanan bir alt kaynak sahip **kaynakları** bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="fcede-129">hello web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="fcede-130">Bu alt kaynak hello web uygulaması ile dağıtılan hello projesi için kaynak denetimi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="fcede-130">This child resource defines source control for hello project deployed with hello web app.</span></span> <span data-ttu-id="fcede-131">Bu şablonda hello kaynak denetimi bağlantılı tooa belirli GitHub depodur.</span><span class="sxs-lookup"><span data-stu-id="fcede-131">In this template, hello source control is linked tooa particular GitHub repository.</span></span> <span data-ttu-id="fcede-132">Merhaba GitHub deposunu hello koduyla tanımlanan **"RepoUrl": "https://github.com/davidebbo-test/Mvc52Application.git"** toocreate art arda dağıtan bir şablon istediğinizde sabit kodlu hello depo URL'si olabilir bir tek bir projede hello minimum parametre sayısını gerektiren oluştu.</span><span class="sxs-lookup"><span data-stu-id="fcede-132">hello GitHub repository is defined with hello code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code hello repository URL when you want toocreate a template that repeatedly deploys a single project while requiring hello minimum number of parameters.</span></span>
<span data-ttu-id="fcede-133">Depo URL'si hello yerine sabit kodlama, hello depo URL'si için bir parametre eklemek ve bu değer için hello kullanın **RepoUrl** özelliği.</span><span class="sxs-lookup"><span data-stu-id="fcede-133">Instead of hard-coding hello repository URL, you can add a parameter for hello repository URL and use that value for hello **RepoUrl** property.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[parameters('hostingPlanName')]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/Sites', parameters('siteName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('repoURL')]",
            "branch": "[parameters('branch')]",
            "IsManualIntegration": true
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a><span data-ttu-id="fcede-134">Komutları toorun dağıtımı</span><span class="sxs-lookup"><span data-stu-id="fcede-134">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="fcede-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fcede-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="fcede-136">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fcede-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="fcede-137">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="fcede-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="fcede-138">Merhaba parametreleri JSON dosyasının içeriğine bakın [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="fcede-138">For content of hello parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

