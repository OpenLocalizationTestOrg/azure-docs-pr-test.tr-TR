---
title: "Azure işlevleri bir işlev uygulaması aaaAutomate kaynak dağıtım | Microsoft Docs"
description: "Bilgi nasıl toobuild işlevi uygulamanızı dağıtan bir Azure Resource Manager şablonu."
services: Functions
documtationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure işlevleri, İşlevler, sunucusuz mimarisi, kod, azure kaynak yöneticisi olarak altyapısı"
ms.assetid: d20743e3-aab6-442c-a836-9bcea09bfd32
ms.server: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: b0df0d4ef9fe93213f7b1cb1d1e6b4e14f8b3a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a>Azure işlevleri işlev uygulamanız için kaynak dağıtımı otomatik hale getir

Azure Resource Manager şablonu toodeploy bir işlev uygulaması kullanabilirsiniz. Bu makalede hello gerekli kaynakları ve bunu parametrelerinin özetlenmektedir. Merhaba bağlı olarak toodeploy ek kaynaklar gerekebilecek [Tetikleyicileri ve bağlamaları](functions-triggers-bindings.md) işlevi uygulamanızda.

Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).

Örnek şablonları için bkz:
- [işlev uygulaması tüketim plan üzerinde]
- [işlev uygulaması Azure uygulama hizmeti plan üzerinde]

## <a name="required-resources"></a>Gerekli kaynakları

Bir işlev uygulaması bu kaynakları gerektirir:

* Bir [Azure Storage](../storage/index.md) hesabı
* Bir barındırma planı (tüketim planı veya uygulama hizmeti planı)
* Bir işlev uygulaması 

### <a name="storage-account"></a>Depolama hesabı

Bir Azure depolama hesabı için bir işlev uygulaması gereklidir. BLOB'lar, tablolar, kuyruklar ve dosyaları destekleyen bir genel amaçlı hesabı gerekir. Daha fazla bilgi için bkz: [Azure işlevleri depolama hesabı gereksinimleri](functions-create-function-app-portal.md#storage-account-requirements).

```json
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2015-06-15",
    "location": "[resourceGroup().location]",
    "properties": {
        "accountType": "[parameters('storageAccountType')]"
    }
}
```

Ayrıca, Özellikler hello `AzureWebJobsStorage` ve `AzureWebJobsDashboard` uygulama ayarları hello site yapılandırması olarak belirtilmelidir. Hello Azure işlevleri çalışma zamanı kullanan hello `AzureWebJobsStorage` bağlantı dizesi toocreate iç sıralar. Hello bağlantı dizesi `AzureWebJobsDashboard` kullanılan toolog, tooAzure tablo depolama ve güç hello olan **İzleyici** hello portal sekmesindedir.

Bu özellikleri hello belirtilen `appSettings` hello koleksiyonda `siteConfig` nesnesi:

```json
"appSettings": [
    {
        "name": "AzureWebJobsStorage",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    },
    {
        "name": "AzureWebJobsDashboard",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    }
```    

### <a name="hosting-plan"></a>Barındırma planı

barındırma planı hello Hello tanımı, bir tüketim veya uygulama hizmeti planı kullanmadığınıza bağlı olarak değişir. Bkz: [hello tüketim plan üzerinde bir işlev uygulaması dağıtma](#consumption) ve [hello uygulama hizmeti planı üzerinde bir işlev uygulaması dağıtma](#app-service-plan).

### <a name="function-app"></a>İşlev uygulaması

Merhaba işlevi uygulama kaynak türünde bir kaynak kullanılarak tanımlanmış **Microsoft.Web/Site** ve tür **functionapp**:

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ]
```

<a name="consumption"></a>

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a>Merhaba tüketim plan üzerinde bir işlev uygulaması dağıtma

Bir işlev uygulaması iki farklı modda çalıştırabilirsiniz: Tüketim planlama ve uygulama hizmeti planı hello hello. kodunuzu çalışıyorsa, çıkışı gerekli toohandle yükü olarak ölçeklendirir ve kod çalışmadığı zaman sonra ölçeklendirir hello tüketim planı otomatik olarak işlem gücü ayırır. Bu nedenle, boşta VM'ler için toopay yok ve önceden tooreserve kapasitesine sahip değilseniz. barındırma planları, hakkında daha fazla toolearn bkz [Azure işlevleri tüketim ve uygulama hizmeti planları](functions-scale.md).

Örnek Azure Resource Manager şablonu için bkz: [işlev uygulaması tüketim plan üzerinde].

### <a name="create-a-consumption-plan"></a>Tüketim planı oluşturma

Tüketim planı "serverfarm" kaynak özel bir türde değil. Hello kullanarak belirtin `Dynamic` hello için değer `computeMode` ve `sku` özellikleri:

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "computeMode": "Dynamic",
        "sku": "Dynamic"
    }
}
```

### <a name="create-a-function-app"></a>İşlev uygulaması oluşturma

Ayrıca, bir tüketim planı hello site yapılandırması iki ek ayarlar gerektirir: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` ve `WEBSITE_CONTENTSHARE`. Bu özellikleri hello işlevi uygulama kodu ve yapılandırma depolandığı hello depolama hesabı ve dosya yolu yapılandırın.

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ],
    "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "siteConfig": {
            "appSettings": [
                {
                    "name": "AzureWebJobsDashboard",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "AzureWebJobsStorage",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTSHARE",
                    "value": "[toLower(variables('functionAppName'))]"
                },
                {
                    "name": "FUNCTIONS_EXTENSION_VERSION",
                    "value": "~1"
                }
            ]
        }
    }
}
```                    

<a name="app-service-plan"></a> 

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a>Merhaba uygulama hizmeti planı üzerinde bir işlev uygulaması dağıtma

Hello uygulama hizmeti planı, temel, standart ve Premium SKU'ları benzer tooweb uygulamalarını özel VM'ler işlevi uygulamanızı çalışır. Merhaba hello uygulama hizmeti planı nasıl çalıştığı hakkında daha fazla bilgi için bkz [Azure App Service planlarına ayrıntılı genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Örnek Azure Resource Manager şablonu için bkz: [işlev uygulaması Azure uygulama hizmeti plan üzerinde].

### <a name="create-an-app-service-plan"></a>App Service planı oluşturma

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "sku": "[parameters('sku')]",
        "workerSize": "[parameters('workerSize')]",
        "hostingEnvironment": "",
        "numberOfWorkers": 1
    }
}
```

### <a name="create-a-function-app"></a>İşlev uygulaması oluşturma 

Ölçeklendirme seçeneği seçtikten sonra bir işlev uygulaması oluşturun. Merhaba uygulama tüm işlevlerinizi tutan hello kapsayıcıdır.

Bir işlev uygulaması, uygulama ayarları ve kaynak denetimi seçenekleri de dahil olmak üzere, dağıtımınızdaki kullanabileceğiniz birçok alt kaynaklara sahip. Tooremove hello tercih edebilirsiniz **sourcecontrols** alt kaynak ve farklı bir kullanım [dağıtım seçeneği](functions-continuous-deployment.md) yerine.

> [!IMPORTANT]
> toosuccessfully Azure Kaynak Yöneticisi'ni kullanarak uygulamanızı dağıtmak, kaynakları Azure içinde nasıl dağıtıldığını önemli toounderstand. Aşağıdaki örneğine hello kullanarak üst düzey yapılandırmaları uygulanan **siteConfig**. Çalışma zamanı ve dağıtım bilgileri toohello işlevleri altyapısı iletmek Bu yapılandırmalar bir üst düzey, önemli tooset demektir. Üst düzey bilgileri hello alt önce gerekli **sourcecontrols/web** kaynak uygulanır. Olası tooconfigure olmasına rağmen bu ayarları alt düzey hello **config/appSettings** işlevi uygulamanızı dağıtılmalıdır bazı durumlarda kaynak *önce* **config/appSettings**  uygulanır. Örneğin, kullanırken işlevleriyle [Logic Apps](../logic-apps/index.md), başka bir kaynak bağımlılığı, işlevlerdir.

```json
{
  "apiVersion": "2015-08-01",
  "name": "[parameters('appName')]",
  "type": "Microsoft.Web/sites",
  "kind": "functionapp",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Web/serverfarms', parameters('appName'))]"
  ],
  "properties": {
     "serverFarmId": "[variables('appServicePlanName')]",
     "siteConfig": {
        "alwaysOn": true,
        "appSettings": [
            { "name": "FUNCTIONS_EXTENSION_VERSION", "value": "~1" },
            { "name": "Project", "value": "src" }
        ]
     }
  },
  "resources": [
     {
        "apiVersion": "2015-08-01",
        "name": "appsettings",
        "type": "config",
        "dependsOn": [
          "[resourceId('Microsoft.Web/Sites', parameters('appName'))]",
          "[resourceId('Microsoft.Web/Sites/sourcecontrols', parameters('appName'), 'web')]",
          "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
        ],
        "properties": {
          "AzureWebJobsStorage": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]",
          "AzureWebJobsDashboard": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
        }
     },
     {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/sites/', parameters('appName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('sourceCodeRepositoryURL')]",
            "branch": "[parameters('sourceCodeBranch')]",
            "IsManualIntegration": "[parameters('sourceCodeManualIntegration')]"
          }
     }
  ]
}
```
> [!TIP]
> Bu şablon hello kullanır [proje](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) hello temel dizin hangi hello işlevleri dağıtım altyapısı (Kudu) görünüyor için dağıtılabilir kod ayarlar uygulama ayarları değeri. Bizim deposunda bizim hello bir alt klasörü işlevlerdir **src** klasör. Bu nedenle, örnek önceki hello hello uygulama ayarları değeri çok ayarlarız`src`. İşlevlerinizi deponuz hello kök dizininde ise ya da kaynak denetiminden dağıtıyorsanız değil, bu uygulama ayarları değeri kaldırabilirsiniz.

## <a name="deploy-your-template"></a>Şablonunuzu dağıtma

Aşağıdaki yolları toodeploy hello şablonunuzu kullanabilirsiniz:

* [PowerShell](../azure-resource-manager/resource-group-template-deploy.md)
* [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [REST API](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a>Dağıt tooAzure düğmesi

Değiştir ```<url-encoded-path-to-azuredeploy-json>``` ile bir [URL kodlanmış](https://www.bing.com/search?q=url+encode) hello ham yolunu sürümü, `azuredeploy.json` GitHub dosyasında.

Markdown kullanan örnek aşağıda verilmiştir:

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

HTML kullanan örnek aşağıda verilmiştir:

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a>Sonraki adımlar

Hakkında daha fazla bilgi toodevelop ve Azure işlevleri yapılandırın.

* [Azure İşlevleri geliştirici başvurusu](functions-reference.md)
* [Nasıl tooconfigure Azure işlev uygulama ayarları](functions-how-to-use-azure-function-app-settings.md)
* [İlk Azure işlevinizi oluşturma](functions-create-first-azure-function.md)

<!-- LINKS -->

[işlev uygulaması tüketim plan üzerinde]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[işlev uygulaması Azure uygulama hizmeti plan üzerinde]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
