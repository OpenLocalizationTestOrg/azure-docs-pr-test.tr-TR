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
# <a name="create-a-logic-app-using-a-template"></a>Şablon kullanarak Logic Apps uygulaması oluşturma
Şablonları, bir mantıksal uygulama içinde farklı bağlayıcıları hızlı şekilde toouse sağlar. Logic apps kullanılan toodefine iş iş akışları bir mantıksal uygulama toocreate için Azure Resource Manager şablonları içerir. Hangi kaynağın dağıtılan, tanımlamak ve nasıl mantıksal uygulamanızı dağıttığınızda toodefine parametreleri. Kendi iş senaryoları için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi.

Merhaba mantıksal uygulama özellikleri hakkında daha fazla bilgi için bkz: [mantığı uygulama iş akışı yönetimi API](https://msdn.microsoft.com/library/azure/mt643788.aspx). 

Merhaba tanımı kendisini örnekler için bkz: [Yazar mantıksal uygulama tanımları](logic-apps-author-definitions.md). 

Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).

Merhaba tam şablonu için bkz: [mantıksal uygulama şablonu](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).

## <a name="what-you-deploy"></a>Ne dağıtma
Bu şablon kullanılarak bir mantıksal uygulama dağıtın.

toorun hello dağıtım otomatik olarak düğmesi aşağıdaki hello seçin:  

[![TooAzure dağıtma](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)

## <a name="parameters"></a>Parametreler
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a>testUri
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-toodeploy"></a>Kaynakları toodeploy
### <a name="logic-app"></a>Mantıksal uygulama
Merhaba mantıksal uygulama oluşturur.

Merhaba şablonları hello mantığı uygulama adı için bir parametre değeri kullanır. Merhaba mantığı uygulama toohello hello konumunu ayarlar hello kaynak grubu olarak aynı konumu. 

Bu belirli tanımını saatte bir kez çalıştırır ve ping hello hello belirtilen konuma **testUri** parametresi. 

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


## <a name="commands-toorun-deployment"></a>Komutları toorun dağıtımı
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Azure CLI
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



