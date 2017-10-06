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
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a>Bir web bağlantılı uygulama tooa GitHub deposunu dağıtma
Bu konuda, nasıl toocreate, bir web uygulamasını dağıtan bir Azure Resource Manager şablonu GitHub deposunu tooa projesinde bağlı öğreneceksiniz. Şunları öğreneceksiniz nasıl toodefine hangi kaynağın dağıtılan ve nasıl toodefine parametreler hello dağıtım zaman yürütülür belirtilmiş. Kendi dağıtımlar için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi.

Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).

Merhaba tam şablonu için bkz: [Web uygulaması bağlantılı tooGitHub şablon](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a>Dağıtmak
Bu şablon kullanılarak, github'da bir projeden hello kodu içeren bir web uygulaması dağıtır.

toorun dağıtım otomatik olarak Merhaba, düğme aşağıdaki hello tıklatın:

[![TooAzure dağıtma](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)

## <a name="parameters"></a>Parametreler
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a>repoURL
Merhaba proje toodeploy içeren GitHub deposunu Hello URL'si. Bu parametre bir varsayılan değer içeriyor ancak bu değer yalnızca hedeflenen tooshow, nasıl tooprovide hello URL için depo. Merhaba şablon ancak test tooprovide hello URL kendi depo hello şablonla çalışırken istediğinizde, bu değeri kullanabilirsiniz.

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a>Dal
Merhaba Uygulama dağıtırken hello depo toouse dalı Hello. Merhaba varsayılan değer ana ancak toodeploy istediğiniz herhangi bir dal hello deposundaki hello adını sağlayabilirsiniz.

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a>Kaynakları toodeploy
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a>Web uygulaması
Github'da bağlantılı toohello projedir hello web uygulamasını oluşturur. 

Merhaba aracılığıyla hello web uygulamasının hello adı belirtin **siteName** parametre ve hello web uygulaması hello aracılığıyla hello konumunu **siteLocation** parametresi. Merhaba, **dependsOn** öğesi hello şablonu tanımlar hello web uygulaması hello service barındırma planı bağlı olarak. Barındırma planı hello üzerinde bağımlı olduğundan, oluşturulmakta hello barındırma planı tamamlanana kadar hello web uygulaması oluşturulamadı. Merhaba **dependsOn** yalnızca kullanılan toospecify dağıtım sırası bir öğedir. Merhaba web uygulaması hello barındırma planı bağlı olarak işaretlemezseniz, Azure kaynak yöneticisi her iki kaynağın toocreate deneyecek hello web uygulaması barındırma planı hello önce oluşturulduysa hello aynı saat ve bir hata iletisi alabilirsiniz.

Hello web uygulaması da içinde tanımlanan bir alt kaynak sahip **kaynakları** bölümüne bakın. Bu alt kaynak hello web uygulaması ile dağıtılan hello projesi için kaynak denetimi tanımlar. Bu şablonda hello kaynak denetimi bağlantılı tooa belirli GitHub depodur. Merhaba GitHub deposunu hello koduyla tanımlanan **"RepoUrl": "https://github.com/davidebbo-test/Mvc52Application.git"** toocreate art arda dağıtan bir şablon istediğinizde sabit kodlu hello depo URL'si olabilir bir tek bir projede hello minimum parametre sayısını gerektiren oluştu.
Depo URL'si hello yerine sabit kodlama, hello depo URL'si için bir parametre eklemek ve bu değer için hello kullanın **RepoUrl** özelliği.

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

## <a name="commands-toorun-deployment"></a>Komutları toorun dağıtımı
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Azure CLI

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a>Azure CLI 2.0

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> Merhaba parametreleri JSON dosyasının içeriğine bakın [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).
>
>

