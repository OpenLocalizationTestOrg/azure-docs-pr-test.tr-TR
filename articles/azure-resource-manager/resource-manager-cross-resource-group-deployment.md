---
title: "aaaDeploy Azure kaynaklarını toomultiple kaynak grupları | Microsoft Docs"
description: "Bir Azure kaynak birden çok tootarget dağıtımı sırasında grup nasıl gösterir."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: tomfitz
ms.openlocfilehash: 93a39a26e0ca18dfcb5c6e8de95c38a64186d6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a><span data-ttu-id="7461d-103">Bir kaynak grubundan Azure kaynaklarını toomore dağıtma</span><span class="sxs-lookup"><span data-stu-id="7461d-103">Deploy Azure resources toomore than one resource group</span></span>

<span data-ttu-id="7461d-104">Genellikle, şablon tooa tek kaynak grubunuzdaki tüm hello kaynakları dağıtın.</span><span class="sxs-lookup"><span data-stu-id="7461d-104">Typically, you deploy all hello resources in your template tooa single resource group.</span></span> <span data-ttu-id="7461d-105">Ancak, burada toodeploy bir kaynak kümesi birlikte istiyor ancak farklı kaynak gruplarına yerleştirmeyi senaryo vardır.</span><span class="sxs-lookup"><span data-stu-id="7461d-105">However, there are scenarios where you want toodeploy a set of resources together but place them in different resource groups.</span></span> <span data-ttu-id="7461d-106">Örneğin, Azure Site Recovery tooa ayrı kaynak grubunu ve konumu için toodeploy hello yedekleme sanal makine isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7461d-106">For example, you may want toodeploy hello backup virtual machine for Azure Site Recovery tooa separate resource group and location.</span></span> <span data-ttu-id="7461d-107">Resource Manager iç içe geçmiş toouse şablonları tootarget farklı kaynak grupları hello üst şablonu için kullanılan hello kaynak grubundan sağlar.</span><span class="sxs-lookup"><span data-stu-id="7461d-107">Resource Manager enables you toouse nested templates tootarget different resource groups than hello resource group used for hello parent template.</span></span>

<span data-ttu-id="7461d-108">Merhaba kaynak hello yaşam döngüsü kapsayıcı Merhaba uygulaması için ve kaynağı kendi koleksiyonunu grubudur.</span><span class="sxs-lookup"><span data-stu-id="7461d-108">hello resource group is hello lifecycle container for hello application and its collection of resources.</span></span> <span data-ttu-id="7461d-109">Hello şablon dışında hello kaynak grubu oluşturun ve dağıtım sırasında hello kaynak grubu tootarget belirtin.</span><span class="sxs-lookup"><span data-stu-id="7461d-109">You create hello resource group outside of hello template, and specify hello resource group tootarget during deployment.</span></span> <span data-ttu-id="7461d-110">Bir giriş tooresource grupları için bkz: [Azure Resource Manager'a genel bakış](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7461d-110">For an introduction tooresource groups, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="example-template"></a><span data-ttu-id="7461d-111">Örnek şablon</span><span class="sxs-lookup"><span data-stu-id="7461d-111">Example template</span></span>

<span data-ttu-id="7461d-112">farklı bir kaynak tootarget, dağıtım sırasında bir iç içe ya da bağlantılı şablonu kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7461d-112">tootarget a different resource, you must use a nested or linked template during deployment.</span></span> <span data-ttu-id="7461d-113">Merhaba `Microsoft.Resources/deployments` kaynak türü sağlayan bir `resourceGroup` farklı bir kaynak grubu hello için toospecify etkinleştirir parametresi, dağıtım iç içe geçmiş.</span><span class="sxs-lookup"><span data-stu-id="7461d-113">hello `Microsoft.Resources/deployments` resource type provides a `resourceGroup` parameter that enables you toospecify a different resource group for hello nested deployment.</span></span> <span data-ttu-id="7461d-114">Tüm hello kaynak grupları hello dağıtım çalıştırmadan önce mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7461d-114">All hello resource groups must exist before running hello deployment.</span></span> <span data-ttu-id="7461d-115">Merhaba aşağıdaki örnek dağıtır - bir dağıtım sırasında belirtilen hello kaynak grubunda iki depolama hesabı ve diğeri adlı bir kaynak grubunda `crossResourceGroupDeployment`:</span><span class="sxs-lookup"><span data-stu-id="7461d-115">hello following example deploys two storage accounts - one in hello resource group specified during deployment, and one in a resource group named `crossResourceGroupDeployment`:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "StorageAccountName1": {
            "type": "string"
        },
        "StorageAccountName2": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "crossResourceGroupDeployment",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "name": "[parameters('StorageAccountName2')]",
                            "apiVersion": "2015-06-15",
                            "location": "West US",
                            "properties": {
                                "accountType": "Standard_LRS"
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('StorageAccountName1')]",
            "apiVersion": "2015-06-15",
            "location": "West US",
            "properties": {
                "accountType": "Standard_LRS"
            }
        }
    ]
}
```

<span data-ttu-id="7461d-116">Ayarlarsanız `resourceGroup` var olmayan bir kaynak grubu adını toohello, hello dağıtımı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="7461d-116">If you set `resourceGroup` toohello name of a resource group that does not exist, hello deployment fails.</span></span> <span data-ttu-id="7461d-117">İçin bir değer belirtmezseniz, `resourceGroup`, Resource Manager hello üst kaynak grubu kullanır.</span><span class="sxs-lookup"><span data-stu-id="7461d-117">If you do not provide a value for `resourceGroup`, Resource Manager uses hello parent resource group.</span></span>  

## <a name="deploy-hello-template"></a><span data-ttu-id="7461d-118">Merhaba şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="7461d-118">Deploy hello template</span></span>

<span data-ttu-id="7461d-119">toodeploy hello örnek şablon hello portalı, Azure PowerShell veya Azure CLI kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7461d-119">toodeploy hello example template, you can use hello portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="7461d-120">Azure PowerShell veya Azure CLI için May 2017 veya sonraki bir sürümü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7461d-120">For Azure PowerShell or Azure CLI, you must use a release from May 2017 or later.</span></span> <span data-ttu-id="7461d-121">Merhaba örnekler varsayar, kaydettiğiniz hello şablonu yerel olarak adlı bir dosya **crossrgdeployment.json**.</span><span class="sxs-lookup"><span data-stu-id="7461d-121">hello examples assume you have saved hello template locally as a file named **crossrgdeployment.json**.</span></span>

<span data-ttu-id="7461d-122">PowerShell için:</span><span class="sxs-lookup"><span data-stu-id="7461d-122">For PowerShell:</span></span>

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

<span data-ttu-id="7461d-123">Azure CLI için:</span><span class="sxs-lookup"><span data-stu-id="7461d-123">For Azure CLI:</span></span>

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

<span data-ttu-id="7461d-124">Dağıtım tamamlandıktan sonra iki kaynak grubu bakın.</span><span class="sxs-lookup"><span data-stu-id="7461d-124">After deployment completes, you see two resource groups.</span></span> <span data-ttu-id="7461d-125">Her kaynak grubu bir depolama hesabını içerir.</span><span class="sxs-lookup"><span data-stu-id="7461d-125">Each resource group contains a storage account.</span></span>

## <a name="use-resourcegroup-function"></a><span data-ttu-id="7461d-126">Kullanım resourceGroup() işlevi</span><span class="sxs-lookup"><span data-stu-id="7461d-126">Use resourceGroup() function</span></span>

<span data-ttu-id="7461d-127">İçin çapraz kaynak grubu dağıtımı hello [resouceGroup() işlevi](resource-group-template-functions-resource.md#resourcegroup) çözümler farklı dayalı hello iç içe geçmiş şablonu nasıl belirtin.</span><span class="sxs-lookup"><span data-stu-id="7461d-127">For cross resource group deployments, hello [resouceGroup() function](resource-group-template-functions-resource.md#resourcegroup) resolves differently based on how you specify hello nested template.</span></span> 

<span data-ttu-id="7461d-128">Başka bir şablonu içindeki bir şablon eklemek, hello iç içe geçmiş şablonunda resouceGroup() toohello üst kaynak grubu çözümler.</span><span class="sxs-lookup"><span data-stu-id="7461d-128">If you embed one template within another template, resouceGroup() in hello nested template resolves toohello parent resource group.</span></span> <span data-ttu-id="7461d-129">Katıştırılmış bir şablonu hello aşağıdaki biçimi kullanır:</span><span class="sxs-lookup"><span data-stu-id="7461d-129">An embedded template uses hello following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers tooparent resource group
    }
}
```

<span data-ttu-id="7461d-130">Tooa ayrı bir şablon bağlantı varsa, hello bağlantılı şablonunda resouceGroup() toohello iç içe kaynak grubu çözümler.</span><span class="sxs-lookup"><span data-stu-id="7461d-130">If you link tooa separate template, resouceGroup() in hello linked template resolves toohello nested resource group.</span></span> <span data-ttu-id="7461d-131">Bağlantılı bir şablon biçimini izleyen hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="7461d-131">A linked template uses hello following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers toolinked resource group
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="7461d-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7461d-132">Next steps</span></span>

* <span data-ttu-id="7461d-133">şablonunuzu toodefine parametrelerinde nasıl görürüm toounderstand [anlamak hello yapısı ve Azure Resource Manager şablonları sözdizimini](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7461d-133">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="7461d-134">Genel dağıtım hatalarını giderme ipuçları için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="7461d-134">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="7461d-135">Bir SAS belirteci gerektiren şablonu dağıtma hakkında daha fazla bilgi için bkz: [dağıtma özel şablonu SAS belirteci ile](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="7461d-135">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
