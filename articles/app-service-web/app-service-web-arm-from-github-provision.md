---
title: "Bir GitHub deposuna bağlı bir web uygulaması dağıtma | Microsoft Docs"
description: "Github'da depodan bir proje içeren bir web uygulaması dağıtmak için bir Azure Resource Manager şablonunu kullanın."
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
ms.openlocfilehash: 77064802814296d0c21f004534e4264d2f97252e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-web-app-linked-to-a-github-repository"></a>Bir GitHub deposuna bağlı bir web uygulaması dağıtma
Bu konuda, GitHub deposunda bir projeye bağlı bir web uygulaması dağıtan bir Azure Resource Manager şablonunun nasıl oluşturulacağını öğreneceksiniz. Nasıl tanımlamak için hangi kaynağın dağıtılan ve ne zaman dağıtım yürütülen parametreler tanımlamak nasıl belirtilen öğreneceksiniz. Bu şablonu kendi dağıtımlarınız için kullanabilir veya kendi gereksinimlerinize göre özelleştirebilirsiniz.

Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).

Tam şablon için bkz: [Web uygulaması bağlantılı GitHub şablonuna](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a>Dağıtmak
Bu şablon kullanılarak GitHub projesinde kodu içeren bir web uygulamasına dağıtır.

Dağıtımı otomatik olarak çalıştırmak için aşağıdaki düğmeye tıklayın:

[![Azure’a dağıtma](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)

## <a name="parameters"></a>Parametreler
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a>repoURL
Dağıtmak için projeyi içeren GitHub deposunu URL'si. Bu parametre bir varsayılan değer içeriyor, ancak bu değer yalnızca URL için depo sağlama göstermek için tasarlanmıştır. Bu değer şablon sınarken kullanabilirsiniz ancak şablonla çalışırken kendi deposu URL'sini sağlamanız isteyeceksiniz.

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a>Dal
Uygulama dağıtımı sırasında kullanılacak olan deponun dalı. Varsayılan değer ana, ancak herhangi bir dal dağıtım yapmak istediğiniz depo adını sağlayabilirsiniz.

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-to-deploy"></a>Dağıtılacak kaynaklar
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a>Web uygulaması
GitHub'nde projeye bağlantılı web uygulamasını oluşturur. 

Web uygulaması adı belirtin **siteName** parametre ve web uygulaması konumunu **siteLocation** parametresi. İçinde **dependsOn** öğe, şablonu tanımlar web uygulaması barındırma planı hizmet bağlı olarak. Barındırma planı üzerinde bağımlı olduğundan, barındırma planı oluşturuluyor tamamlanana kadar web uygulaması oluşturulamadı. **DependsOn** öğesi dağıtım sırası belirtmek için yalnızca kullanılır. Barındırma planı bağlı olarak web uygulaması işaretlemezseniz, Azure Kaynak Yöneticisi aynı anda hem kaynakları oluşturmayı dener ve barındırma planı önce web uygulaması oluşturduysanız, bir hata alabilirsiniz.

Web uygulaması da içinde tanımlanan bir alt kaynak sahip **kaynakları** bölümüne bakın. Bu alt kaynak web uygulaması ile dağıtılan projesi için kaynak denetimi tanımlar. Bu şablonda kaynak denetimi belirli bir GitHub deposuna bağlıdır. GitHub deposuna koduyla tanımlanan **"RepoUrl": "https://github.com/davidebbo-test/Mvc52Application.git"** sürekli olarak tek bir dağıtan bir şablon oluşturmak istediğinizde depo URL'si sabit kodlu olabilir minimum parametre sayısını gerektiren sırasında projesi.
Depo URL'si kodlamak yerine, bir parametre depo URL'si ekleyin ve bu değeri kullanın **RepoUrl** özelliği.

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

## <a name="commands-to-run-deployment"></a>Dağıtımı çalıştırma komutları
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Azure CLI

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a>Azure CLI 2.0

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> Parametreleri JSON dosyasının içeriğine bakın [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).
>
>

