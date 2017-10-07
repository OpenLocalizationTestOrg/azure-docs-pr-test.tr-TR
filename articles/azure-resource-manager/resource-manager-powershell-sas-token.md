---
title: "aaaDeploy SAS belirteci ve PowerShell ile Azure şablonu | Microsoft Docs"
description: "Azure Resource Manager ve Azure PowerShell toodeploy kaynakları tooAzure korunan bir şablondan SAS belirteci ile kullanın."
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
ms.openlocfilehash: b95e096591d6213f8ef79235c8cd85705c4b79ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a><span data-ttu-id="ea3be-103">SAS belirteci ve Azure PowerShell ile özel Resource Manager şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="ea3be-103">Deploy private Resource Manager template with SAS token and Azure PowerShell</span></span>

<span data-ttu-id="ea3be-104">Şablonunuzu bir depolama hesabında bulunduğunda, access toohello şablonu kısıtlamak ve dağıtım sırasında bir paylaşılan erişim imzası (SAS) belirteci sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ea3be-104">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="ea3be-105">Bu konuda açıklanmaktadır nasıl toouse Azure PowerShell'i Resource Manager şablonları tooprovide dağıtımı sırasında bir SAS belirteci ile.</span><span class="sxs-lookup"><span data-stu-id="ea3be-105">This topic explains how toouse Azure PowerShell with Resource Manager templates tooprovide a SAS token during deployment.</span></span> 

## <a name="add-private-template-toostorage-account"></a><span data-ttu-id="ea3be-106">Özel şablon toostorage hesabı Ekle</span><span class="sxs-lookup"><span data-stu-id="ea3be-106">Add private template toostorage account</span></span>

<span data-ttu-id="ea3be-107">Şablonları tooa depolama hesabınızı ekleyin ve bir SAS belirteci ile dağıtım sırasında toothem bağlayın.</span><span class="sxs-lookup"><span data-stu-id="ea3be-107">You can add your templates tooa storage account and link toothem during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea3be-108">Merhaba adımları izleyerek hello şablonu içeren hello blob erişilebilir tooonly hello hesap sahibi değil.</span><span class="sxs-lookup"><span data-stu-id="ea3be-108">By following hello steps below, hello blob containing hello template is accessible tooonly hello account owner.</span></span> <span data-ttu-id="ea3be-109">Ancak, hello blob için bir SAS belirteci oluşturduğunuzda hello blob bu URI ile erişilebilir tooanyone olur.</span><span class="sxs-lookup"><span data-stu-id="ea3be-109">However, when you create a SAS token for hello blob, hello blob is accessible tooanyone with that URI.</span></span> <span data-ttu-id="ea3be-110">Başka bir kullanıcı hello URI kesişirse kullanıcı mümkün tooaccess hello şablonudur.</span><span class="sxs-lookup"><span data-stu-id="ea3be-110">If another user intercepts hello URI, that user is able tooaccess hello template.</span></span> <span data-ttu-id="ea3be-111">Bir SAS belirteci kullanarak erişim tooyour şablonları sınırlama, iyi bir yoludur ancak parolalar gibi hassas verileri doğrudan hello şablonunda içermemelidir.</span><span class="sxs-lookup"><span data-stu-id="ea3be-111">Using a SAS token is a good way of limiting access tooyour templates, but you should not include sensitive data like passwords directly in hello template.</span></span>
> 
> 

<span data-ttu-id="ea3be-112">Merhaba aşağıdaki örnekte bir özel depolama hesabı kapsayıcısının ayarlar ve bir şablon yükler:</span><span class="sxs-lookup"><span data-stu-id="ea3be-112">hello following example sets up a private storage account container and uploads a template:</span></span>
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="ea3be-113">Dağıtım sırasında SAS belirteci sağlayın</span><span class="sxs-lookup"><span data-stu-id="ea3be-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="ea3be-114">toodeploy özel bir şablon bir depolama hesabındaki bir SAS belirteci oluştur ve hello URI hello şablonunun dahil edin.</span><span class="sxs-lookup"><span data-stu-id="ea3be-114">toodeploy a private template in a storage account, generate a SAS token and include it in hello URI for hello template.</span></span> <span data-ttu-id="ea3be-115">Merhaba sona erme saati tooallow yeterli zaman toocomplete hello dağıtım ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ea3be-115">Set hello expiry time tooallow enough time toocomplete hello deployment.</span></span>
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get hello URI with hello SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

<span data-ttu-id="ea3be-116">Bir SAS belirteci ile bağlı şablonları kullanma örneği için bkz: [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ea3be-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="ea3be-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ea3be-117">Next steps</span></span>
* <span data-ttu-id="ea3be-118">Bir giriş toodeploying şablonları için bkz: [Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtmak](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ea3be-118">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="ea3be-119">Bir şablon dağıtan bir tam örnek betik için bkz: [dağıtmak Resource Manager şablonu komut dosyası](resource-manager-samples-powershell-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="ea3be-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-powershell-deploy.md)</span></span>
* <span data-ttu-id="ea3be-120">Şablon toodefine parametrelerinde bkz [şablonları yazma](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="ea3be-120">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="ea3be-121">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="ea3be-121">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

