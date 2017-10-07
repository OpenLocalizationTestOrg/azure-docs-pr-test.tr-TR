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
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a><span data-ttu-id="c3ce7-103">Azure Resource Manager’ı Kullanarak Machine Learning Çalışma Alanını Dağıtma</span><span class="sxs-lookup"><span data-stu-id="c3ce7-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span></span>
## <a name="introduction"></a><span data-ttu-id="c3ce7-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="c3ce7-104">Introduction</span></span>
<span data-ttu-id="c3ce7-105">Bir Azure Resource Manager dağıtım şablonu kaydeder kullanarak ölçeklenebilir şekilde toodeploy vererek, zaman bileşenleri ile bir doğrulama ve yeniden deneme mekanizması birbirlerine bağlı.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way toodeploy interconnected components with a validation and retry mechanism.</span></span> <span data-ttu-id="c3ce7-106">tooset Azure Machine Learning çalışma alanlarını oluşturan, örneğin, gereksinim duyduğunuz toofirst bir Azure depolama hesabı yapılandırın ve sonra çalışma alanınızda dağıtın.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-106">tooset up Azure Machine Learning Workspaces, for example, you need toofirst configure an Azure storage account and then deploy your workspace.</span></span> <span data-ttu-id="c3ce7-107">El ile çalışma alanları yüzlerce için bunu düşünün.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-107">Imagine doing this manually for hundreds of workspaces.</span></span> <span data-ttu-id="c3ce7-108">Bir daha kolay toouse Azure Resource Manager şablonu toodeploy bir Azure Machine Learning çalışma alanı ve tüm bağımlılıklarını alternatiftir.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-108">An easier alternative is toouse an Azure Resource Manager template toodeploy an Azure Machine Learning Workspace and all its dependencies.</span></span> <span data-ttu-id="c3ce7-109">Bu makalede bu işlemi adım adım alır.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-109">This article takes you through this process step-by-step.</span></span> <span data-ttu-id="c3ce7-110">Bir harika Azure Kaynak Yöneticisi'nin için bkz: genel bakış [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c3ce7-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="step-by-step-create-a-machine-learning-workspace"></a><span data-ttu-id="c3ce7-111">Adım adım: bir Machine Learning çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c3ce7-111">Step-by-step: create a Machine Learning Workspace</span></span>
<span data-ttu-id="c3ce7-112">Biz bir Azure kaynak grubu oluşturun ve ardından yeni bir Azure depolama hesabı ve yeni bir Azure Machine Learning Resource Manager şablonu kullanarak çalışma alanı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span></span> <span data-ttu-id="c3ce7-113">Merhaba dağıtım tamamlandıktan sonra biz (Merhaba birincil anahtar, hello Workspaceıd ve hello URL toohello çalışma) oluşturulmuş hello çalışma alanları hakkında önemli bilgiler yazdırır.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-113">Once hello deployment is complete, we will print out important information about hello workspaces that were created (hello primary key, hello workspaceID, and hello URL toohello workspace).</span></span>

### <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="c3ce7-114">Bir Azure Resource Manager şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c3ce7-114">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="c3ce7-115">Bir Machine Learning çalışma alanı, bir Azure depolama hesabı toostore hello bağlantılı veri kümesi tooit gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-115">A Machine Learning Workspace requires an Azure storage account toostore hello dataset linked tooit.</span></span>
<span data-ttu-id="c3ce7-116">Merhaba aşağıdaki şablonu hello kaynak grubu toogenerate hello depolama hesabı adı ve hello çalışma alanı adı hello adını kullanır.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-116">hello following template uses hello name of hello resource group toogenerate hello storage account name and hello workspace name.</span></span>  <span data-ttu-id="c3ce7-117">Ayrıca hello depolama hesabı adı bir özellik olarak hello çalışma oluştururken kullanır.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-117">It also uses hello storage account name as a property when creating hello workspace.</span></span>

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
<span data-ttu-id="c3ce7-118">Bu şablon, c:\temp\ altında mlworkspace.json dosyası olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-118">Save this template as mlworkspace.json file under c:\temp\.</span></span>

### <a name="deploy-hello-resource-group-based-on-hello-template"></a><span data-ttu-id="c3ce7-119">Merhaba şablona dayalı hello kaynak grubu dağıtma</span><span class="sxs-lookup"><span data-stu-id="c3ce7-119">Deploy hello resource group, based on hello template</span></span>
* <span data-ttu-id="c3ce7-120">PowerShell'i açın</span><span class="sxs-lookup"><span data-stu-id="c3ce7-120">Open PowerShell</span></span>
* <span data-ttu-id="c3ce7-121">Azure Resource Manager ve Azure hizmet yönetimi için modüllerini yükleyin</span><span class="sxs-lookup"><span data-stu-id="c3ce7-121">Install modules for Azure Resource Manager and Azure Service Management</span></span>  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   <span data-ttu-id="c3ce7-122">Bu adımları yükleyip hello modülleri gerekli toocomplete hello kalan adımları.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-122">These steps download and install hello modules necessary toocomplete hello remaining steps.</span></span> <span data-ttu-id="c3ce7-123">Bu yalnızca bir kez burada hello PowerShell komutlarını çalıştırma hello ortamında yapılır toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-123">This only needs toobe done once in hello environment where you are executing hello PowerShell commands.</span></span>   

* <span data-ttu-id="c3ce7-124">TooAzure kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="c3ce7-124">Authenticate tooAzure</span></span>  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
<span data-ttu-id="c3ce7-125">Bu adımı her oturum için yinelenen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-125">This step needs toobe repeated for each session.</span></span> <span data-ttu-id="c3ce7-126">Kimliği doğrulanmış sonra abonelik bilgilerinizi görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-126">Once authenticated, your subscription information should be displayed.</span></span>

![Azure hesabı][1]

<span data-ttu-id="c3ce7-128">Biz erişim tooAzure sahip olduğunuza göre biz hello kaynak grubu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-128">Now that we have access tooAzure, we can create hello resource group.</span></span>

* <span data-ttu-id="c3ce7-129">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c3ce7-129">Create a resource group</span></span>

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

<span data-ttu-id="c3ce7-130">Merhaba kaynak grubunun doğru biçimde sağlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-130">Verify that hello resource group is correctly provisioned.</span></span> <span data-ttu-id="c3ce7-131">**ProvisioningState** "Başarılı."</span><span class="sxs-lookup"><span data-stu-id="c3ce7-131">**ProvisioningState** should be “Succeeded.”</span></span>
<span data-ttu-id="c3ce7-132">Merhaba kaynak grubu adı hello şablonu toogenerate hello depolama hesabı adı tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-132">hello resource group name is used by hello template toogenerate hello storage account name.</span></span> <span data-ttu-id="c3ce7-133">Merhaba depolama hesabı adı 3 ile 24 karakter uzunluğunda olmalıdır ve rakamlar ve yalnızca küçük harfler kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-133">hello storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

![Kaynak Grubu][2]

* <span data-ttu-id="c3ce7-135">Merhaba kaynak grubu dağıtım kullanarak, yeni bir Machine Learning çalışma alanı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-135">Using hello resource group deployment, deploy a new Machine Learning Workspace.</span></span>

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

<span data-ttu-id="c3ce7-136">Merhaba dağıtım tamamlandıktan sonra basit tooaccess özellikleri, dağıtılan hello çalışma alanının var.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-136">Once hello deployment is completed, it is straightforward tooaccess properties of hello workspace you deployed.</span></span> <span data-ttu-id="c3ce7-137">Örneğin, birincil anahtar belirteci hello erişebilir.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-137">For example, you can access hello Primary Key Token.</span></span>

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

<span data-ttu-id="c3ce7-138">Varolan çalışma alanının başka bir şekilde tooretrieve belirteçleri toouse hello Invoke-AzureRmResourceAction komutu olur.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-138">Another way tooretrieve tokens of existing workspace is toouse hello Invoke-AzureRmResourceAction command.</span></span> <span data-ttu-id="c3ce7-139">Örneğin, tüm çalışma alanları hello birincil ve ikincil belirteçleri listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3ce7-139">For example, you can list hello primary and secondary tokens of all workspaces.</span></span>

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
<span data-ttu-id="c3ce7-140">Merhaba çalışma alanı sağlandıktan sonra hello kullanarak birçok Azure Machine Learning Studio görevleri de otomatik hale getirebilirsiniz [Azure Machine Learning için PowerShell Modülü](http://aka.ms/amlps).</span><span class="sxs-lookup"><span data-stu-id="c3ce7-140">After hello workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using hello [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3ce7-141">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c3ce7-141">Next Steps</span></span>
* <span data-ttu-id="c3ce7-142">Daha fazla bilgi edinmek [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c3ce7-142">Learn more about [authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="c3ce7-143">Merhaba bakın [Azure hızlı başlangıç şablonlarını deposuna](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="c3ce7-143">Have a look at hello [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span></span> 
* <span data-ttu-id="c3ce7-144">İlgili bu videoyu izleyin [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span><span class="sxs-lookup"><span data-stu-id="c3ce7-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span></span> 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
