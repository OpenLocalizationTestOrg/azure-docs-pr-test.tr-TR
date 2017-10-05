---
title: "SAS belirteci ve PowerShell ile Azure şablonu dağıtma | Microsoft Docs"
description: "SAS belirteci ile korunan bir şablondan kaynakları Azure'a dağıtmak için Azure Resource Manager ve Azure PowerShell kullanın."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 1e3cea027b599e2b1af1ced0fdf14e2cc8a0db82
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a><span data-ttu-id="173d5-103">SAS belirteci ve Azure PowerShell ile özel Resource Manager şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="173d5-103">Deploy private Resource Manager template with SAS token and Azure PowerShell</span></span>

<span data-ttu-id="173d5-104">Şablonunuzu bir depolama hesabında bulunduğunda, şablona erişimi kısıtlayabilir ve dağıtım sırasında bir paylaşılan erişim imzası (SAS) belirteci sağlayın.</span><span class="sxs-lookup"><span data-stu-id="173d5-104">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="173d5-105">Bu konu Azure PowerShell'i Resource Manager şablonları ile dağıtımı sırasında bir SAS belirteci sağlamak için nasıl kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="173d5-105">This topic explains how to use Azure PowerShell with Resource Manager templates to provide a SAS token during deployment.</span></span> 

## <a name="add-private-template-to-storage-account"></a><span data-ttu-id="173d5-106">Özel şablon için depolama hesabı ekleme</span><span class="sxs-lookup"><span data-stu-id="173d5-106">Add private template to storage account</span></span>

<span data-ttu-id="173d5-107">Bir depolama hesabı ve bunları bir SAS belirteci ile dağıtım sırasında bağlantı şablonlarınızı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="173d5-107">You can add your templates to a storage account and link to them during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="173d5-108">Aşağıdaki adımları izleyerek, şablonu içeren blob yalnızca hesap sahibi erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="173d5-108">By following the steps below, the blob containing the template is accessible to only the account owner.</span></span> <span data-ttu-id="173d5-109">Blob için bir SAS belirteci oluşturduğunuzda, ancak blob bu URI ile bir kişiye erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="173d5-109">However, when you create a SAS token for the blob, the blob is accessible to anyone with that URI.</span></span> <span data-ttu-id="173d5-110">Başka bir kullanıcı URI kesişirse kullanıcı şablonu erişebilir.</span><span class="sxs-lookup"><span data-stu-id="173d5-110">If another user intercepts the URI, that user is able to access the template.</span></span> <span data-ttu-id="173d5-111">Bir SAS belirteci kullanarak şablonlarınızı erişimi sınırlayan, iyi bir yoludur ancak parolalar gibi hassas verileri doğrudan şablonunda içermemelidir.</span><span class="sxs-lookup"><span data-stu-id="173d5-111">Using a SAS token is a good way of limiting access to your templates, but you should not include sensitive data like passwords directly in the template.</span></span>
> 
> 

<span data-ttu-id="173d5-112">Aşağıdaki örnek, bir özel depolama hesabı kapsayıcısının ayarlar ve bir şablon yükler:</span><span class="sxs-lookup"><span data-stu-id="173d5-112">The following example sets up a private storage account container and uploads a template:</span></span>
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="173d5-113">Dağıtım sırasında SAS belirteci sağlayın</span><span class="sxs-lookup"><span data-stu-id="173d5-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="173d5-114">Özel bir şablon bir depolama hesabında dağıtmak için bir SAS belirteci oluştur ve şablon için URI dahil edin.</span><span class="sxs-lookup"><span data-stu-id="173d5-114">To deploy a private template in a storage account, generate a SAS token and include it in the URI for the template.</span></span> <span data-ttu-id="173d5-115">Dağıtım tamamlamak için yeterli zamana olanak sona erme saati ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="173d5-115">Set the expiry time to allow enough time to complete the deployment.</span></span>
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get the URI with the SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

<span data-ttu-id="173d5-116">Bir SAS belirteci ile bağlı şablonları kullanma örneği için bkz: [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="173d5-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="173d5-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="173d5-117">Next steps</span></span>
* <span data-ttu-id="173d5-118">Şablon dağıtımı için giriş için bkz [Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtmak](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="173d5-118">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="173d5-119">Bir şablon dağıtan bir tam örnek betik için bkz: [dağıtmak Resource Manager şablonu komut dosyası](resource-manager-samples-powershell-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="173d5-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-powershell-deploy.md)</span></span>
* <span data-ttu-id="173d5-120">Şablonda parametreleri tanımlamak için bkz: [şablonları yazma](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="173d5-120">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="173d5-121">Kuruluşların abonelikleri etkili bir şekilde yönetmek için Resource Manager'ı nasıl kullanabileceği hakkında yönergeler için bkz. [Azure kurumsal iskelesi: öngörücü abonelik idaresi](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="173d5-121">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

