---
title: "Azure Resource Manager kullanarak bir Redis önbelleği aaaProvision | Microsoft Docs"
description: "Azure Resource Manager şablonu toodeploy bir Azure Redis önbelleği kullanın."
services: app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 46e7b3b2493ac51dbe6bab0b086304802afc5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-redis-cache-using-a-template"></a>Şablon kullanarak Redis Önbelleği oluşturma
Bu konuda, bilgi toocreate bir Azure Resource Manager şablonu dağıtan nasıl bir Azure Redis önbelleği. Merhaba önbelleği bir var olan depolama hesabı tookeep Tanılama verileri ile kullanılabilir. Da bilgi nasıl toodefine hangi kaynağın dağıtılan ve nasıl toodefine parametreler hello dağıtım zaman yürütülür belirtilmiş. Kendi dağıtımlar için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi.

Şu anda tanılama ayarları için tüm önbellekleri hello paylaşılan aynı bölge için bir abonelik. Merhaba bölgede bulunan bir önbellek güncelleştirme hello bölgedeki tüm diğer önbellekleri etkiler.

Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).

Merhaba tam şablonu için bkz: [Redis önbelleği şablon](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).

> [!NOTE]
> Resource Manager şablonları hello yeni için [Premium katmanı](cache-premium-tier-intro.md) kullanılabilir. 
> 
> * [Kümeleme Premium Redis önbelleği oluşturma](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [Premium Redis önbelleği ile veri kalıcılığını oluşturma](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [VNet ve isteğe bağlı kümeleme Premium Redis önbelleği oluşturma](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> toocheck hello son şablonları için bkz: [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/) arayın ve `Redis Cache`.
> 
> 

## <a name="what-you-will-deploy"></a>Dağıtmak
Bu şablonda bir Azure Redis Tanılama verileri için mevcut bir depolama hesabını kullanan önbelleği dağıtır.

toorun dağıtım otomatik olarak Merhaba, düğme aşağıdaki hello tıklatın:

[![TooAzure dağıtma](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)

## <a name="parameters"></a>Parametreler
Azure Resource Manager ile tanımladığınız parametreler için değerler hello şablon dağıtıldığında toospecify istediğiniz. Merhaba şablonu tüm hello parametre değerlerini içeren parametreleri adlı bir bölüm içerir.
Dağıttığınız hello projesini temel alan veya dağıttığınız hello ortamı dayanarak farklılık bu değerleri için bir parametre tanımlamanız gerekir. Her zaman kalın değerleri aynı hello için parametreleri tanımlamayın. Her parametre değeri dağıtılan hello şablonu toodefine hello kaynaklarında kullanılır. 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a>redisCacheLocation
Merhaba Redis önbelleği başlangıç konumu. En iyi performans için kullanım hello aynı hello önbelleği ile kullanılan uygulama toobe hello gibi konumu.

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a>existingDiagnosticsStorageAccountName
Tanılama hello varolan depolama hesabı toouse adı Hello. 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a>EnableNonSslPort
Gösteren bir Boole değeri tooallow SSL olmayan bağlantı noktaları erişim olup olmadığını.

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a>diagnosticsStatus
Tanılama etkin olup olmadığını belirten bir değer. Kullanım açık veya kapalı.

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a>Kaynakları toodeploy
### <a name="redis-cache"></a>Redis Önbelleği
Hello Azure Redis önbelleği oluşturur.

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-toorun-deployment"></a>Komutları toorun dağıtımı
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a>Azure CLI
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


