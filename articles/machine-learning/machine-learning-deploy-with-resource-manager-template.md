---
title: "bir Machine Learning çalışma alanı Azure Resource Manager ile aaaDeploy | Microsoft Docs"
description: "Nasıl toodeploy Azure Machine Learning Azure Resource Manager şablonu kullanarak bir çalışma alanı"
services: machine-learning
documentationcenter: 
author: ahgyger
manager: haining
editor: garye
ms.assetid: 4955ac4d-ff99-4908-aa27-69b6bfcc8e85
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/15/2017
ms.author: ahgyger
ms.openlocfilehash: 308959825bcbd670f6ce9b6dc381be767f172357
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a>Azure Resource Manager’ı Kullanarak Machine Learning Çalışma Alanını Dağıtma
## <a name="introduction"></a>Giriş
Bir Azure Resource Manager dağıtım şablonu kaydeder kullanarak ölçeklenebilir şekilde toodeploy vererek, zaman bileşenleri ile bir doğrulama ve yeniden deneme mekanizması birbirlerine bağlı. tooset Azure Machine Learning çalışma alanlarını oluşturan, örneğin, gereksinim duyduğunuz toofirst bir Azure depolama hesabı yapılandırın ve sonra çalışma alanınızda dağıtın. El ile çalışma alanları yüzlerce için bunu düşünün. Bir daha kolay toouse Azure Resource Manager şablonu toodeploy bir Azure Machine Learning çalışma alanı ve tüm bağımlılıklarını alternatiftir. Bu makalede bu işlemi adım adım alır. Bir harika Azure Kaynak Yöneticisi'nin için bkz: genel bakış [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).

## <a name="step-by-step-create-a-machine-learning-workspace"></a>Adım adım: bir Machine Learning çalışma alanı oluşturma
Biz bir Azure kaynak grubu oluşturun ve ardından yeni bir Azure depolama hesabı ve yeni bir Azure Machine Learning Resource Manager şablonu kullanarak çalışma alanı dağıtın. Merhaba dağıtım tamamlandıktan sonra biz (Merhaba birincil anahtar, hello Workspaceıd ve hello URL toohello çalışma) oluşturulmuş hello çalışma alanları hakkında önemli bilgiler yazdırır.

### <a name="create-an-azure-resource-manager-template"></a>Bir Azure Resource Manager şablonu oluşturma
Bir Machine Learning çalışma alanı, bir Azure depolama hesabı toostore hello bağlantılı veri kümesi tooit gerektirir.
Merhaba aşağıdaki şablonu hello kaynak grubu toogenerate hello depolama hesabı adı ve hello çalışma alanı adı hello adını kullanır.  Ayrıca hello depolama hesabı adı bir özellik olarak hello çalışma oluştururken kullanır.

```
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "variables": {
        "namePrefix": "[resourceGroup().name]",
        "location": "[resourceGroup().location]",
        "mlVersion": "2016-04-01",
        "stgVersion": "2015-06-15",
        "storageAccountName": "[concat(variables('namePrefix'),'stg')]",
        "mlWorkspaceName": "[concat(variables('namePrefix'),'mlwk')]",
        "mlResourceId": "[resourceId('Microsoft.MachineLearning/workspaces', variables('mlWorkspaceName'))]",
        "stgResourceId": "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
        "storageAccountType": "Standard_LRS"
    },
    "resources": [
        {
            "apiVersion": "[variables('stgVersion')]",
            "name": "[variables('storageAccountName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "location": "[variables('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "apiVersion": "[variables('mlVersion')]",
            "type": "Microsoft.MachineLearning/workspaces",
            "name": "[variables('mlWorkspaceName')]",
            "location": "[variables('location')]",
            "dependsOn": ["[variables('stgResourceId')]"],
            "properties": {
                "UserStorageAccountId": "[variables('stgResourceId')]"
            }
        }
    ],
    "outputs": {
        "mlWorkspaceObject": {"type": "object", "value": "[reference(variables('mlResourceId'), variables('mlVersion'))]"},
        "mlWorkspaceToken": {"type": "string", "value": "[listWorkspaceKeys(variables('mlResourceId'), variables('mlVersion')).primaryToken]"},
        "mlWorkspaceWorkspaceID": {"type": "string", "value": "[reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId]"},
        "mlWorkspaceWorkspaceLink": {"type": "string", "value": "[concat('https://studio.azureml.net/Home/ViewWorkspace/', reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId)]"}
    }
}

```
Bu şablon, c:\temp\ altında mlworkspace.json dosyası olarak kaydedin.

### <a name="deploy-hello-resource-group-based-on-hello-template"></a>Merhaba şablona dayalı hello kaynak grubu dağıtma
* PowerShell'i açın
* Azure Resource Manager ve Azure hizmet yönetimi için modüllerini yükleyin  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   Bu adımları yükleyip hello modülleri gerekli toocomplete hello kalan adımları. Bu yalnızca bir kez burada hello PowerShell komutlarını çalıştırma hello ortamında yapılır toobe gerekir.   

* TooAzure kimlik doğrulaması  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
Bu adımı her oturum için yinelenen toobe gerekir. Kimliği doğrulanmış sonra abonelik bilgilerinizi görüntülenmesi gerekir.

![Azure hesabı][1]

Biz erişim tooAzure sahip olduğunuza göre biz hello kaynak grubu oluşturabilirsiniz.

* Kaynak grubu oluşturma

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

Merhaba kaynak grubunun doğru biçimde sağlandığından emin olun. **ProvisioningState** "Başarılı."
Merhaba kaynak grubu adı hello şablonu toogenerate hello depolama hesabı adı tarafından kullanılır. Merhaba depolama hesabı adı 3 ile 24 karakter uzunluğunda olmalıdır ve rakamlar ve yalnızca küçük harfler kullanmanız gerekir.

![Kaynak Grubu][2]

* Merhaba kaynak grubu dağıtım kullanarak, yeni bir Machine Learning çalışma alanı dağıtın.

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

Merhaba dağıtım tamamlandıktan sonra basit tooaccess özellikleri, dağıtılan hello çalışma alanının var. Örneğin, birincil anahtar belirteci hello erişebilir.

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

Varolan çalışma alanının başka bir şekilde tooretrieve belirteçleri toouse hello Invoke-AzureRmResourceAction komutu olur. Örneğin, tüm çalışma alanları hello birincil ve ikincil belirteçleri listeleyebilirsiniz.

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
Merhaba çalışma alanı sağlandıktan sonra hello kullanarak birçok Azure Machine Learning Studio görevleri de otomatik hale getirebilirsiniz [Azure Machine Learning için PowerShell Modülü](http://aka.ms/amlps).

## <a name="next-steps"></a>Sonraki Adımlar
* Daha fazla bilgi edinmek [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md). 
* Merhaba bakın [Azure hızlı başlangıç şablonlarını deposuna](https://github.com/Azure/azure-quickstart-templates). 
* İlgili bu videoyu izleyin [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39). 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
