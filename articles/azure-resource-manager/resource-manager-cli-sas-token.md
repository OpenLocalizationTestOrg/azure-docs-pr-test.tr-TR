---
title: "aaaDeploy SAS belirteci ve Azure CLI ile Azure şablonu | Microsoft Docs"
description: "Azure Resource Manager ve Azure CLI toodeploy kaynakları tooAzure korunan bir şablondan SAS belirteci ile kullanın."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 59c64616d6e1f5e456d88a72854d0ed99e1bdc0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a><span data-ttu-id="2173f-103">SAS belirteci ve Azure CLI ile özel Resource Manager şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="2173f-103">Deploy private Resource Manager template with SAS token and Azure CLI</span></span>

<span data-ttu-id="2173f-104">Şablonunuzu bir depolama hesabında bulunduğunda, access toohello şablonu kısıtlamak ve dağıtım sırasında bir paylaşılan erişim imzası (SAS) belirteci sağlayın.</span><span class="sxs-lookup"><span data-stu-id="2173f-104">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span> <span data-ttu-id="2173f-105">Bu konuda açıklanmaktadır nasıl toouse Azure PowerShell'i Resource Manager şablonları tooprovide dağıtımı sırasında bir SAS belirteci ile.</span><span class="sxs-lookup"><span data-stu-id="2173f-105">This topic explains how toouse Azure PowerShell with Resource Manager templates tooprovide a SAS token during deployment.</span></span> 

## <a name="add-private-template-toostorage-account"></a><span data-ttu-id="2173f-106">Özel şablon toostorage hesabı Ekle</span><span class="sxs-lookup"><span data-stu-id="2173f-106">Add private template toostorage account</span></span>

<span data-ttu-id="2173f-107">Şablonları tooa depolama hesabınızı ekleyin ve bir SAS belirteci ile dağıtım sırasında toothem bağlayın.</span><span class="sxs-lookup"><span data-stu-id="2173f-107">You can add your templates tooa storage account and link toothem during deployment with a SAS token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2173f-108">Merhaba adımları izleyerek hello şablonu içeren hello blob erişilebilir tooonly hello hesap sahibi değil.</span><span class="sxs-lookup"><span data-stu-id="2173f-108">By following hello steps below, hello blob containing hello template is accessible tooonly hello account owner.</span></span> <span data-ttu-id="2173f-109">Ancak, hello blob için bir SAS belirteci oluşturduğunuzda hello blob bu URI ile erişilebilir tooanyone olur.</span><span class="sxs-lookup"><span data-stu-id="2173f-109">However, when you create a SAS token for hello blob, hello blob is accessible tooanyone with that URI.</span></span> <span data-ttu-id="2173f-110">Başka bir kullanıcı hello URI kesişirse kullanıcı mümkün tooaccess hello şablonudur.</span><span class="sxs-lookup"><span data-stu-id="2173f-110">If another user intercepts hello URI, that user is able tooaccess hello template.</span></span> <span data-ttu-id="2173f-111">Bir SAS belirteci kullanarak erişim tooyour şablonları sınırlama, iyi bir yoludur ancak parolalar gibi hassas verileri doğrudan hello şablonunda içermemelidir.</span><span class="sxs-lookup"><span data-stu-id="2173f-111">Using a SAS token is a good way of limiting access tooyour templates, but you should not include sensitive data like passwords directly in hello template.</span></span>
> 
> 

<span data-ttu-id="2173f-112">Merhaba aşağıdaki örnekte bir özel depolama hesabı kapsayıcısının ayarlar ve bir şablon yükler:</span><span class="sxs-lookup"><span data-stu-id="2173f-112">hello following example sets up a private storage account container and uploads a template:</span></span>
   
```azurecli
az group create --name "ManageGroup" --location "South Central US"
az storage account create \
    --resource-group ManageGroup \
    --location "South Central US" \
    --sku Standard_LRS \
    --kind Storage \
    --name {your-unique-name}
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
az storage container create \
    --name templates \
    --public-access Off \
    --connection-string $connection
az storage blob upload \
    --container-name templates \
    --file vmlinux.json \
    --name vmlinux.json \
    --connection-string $connection
```

### <a name="provide-sas-token-during-deployment"></a><span data-ttu-id="2173f-113">Dağıtım sırasında SAS belirteci sağlayın</span><span class="sxs-lookup"><span data-stu-id="2173f-113">Provide SAS token during deployment</span></span>
<span data-ttu-id="2173f-114">toodeploy özel bir şablon bir depolama hesabındaki bir SAS belirteci oluştur ve hello URI hello şablonunun dahil edin.</span><span class="sxs-lookup"><span data-stu-id="2173f-114">toodeploy a private template in a storage account, generate a SAS token and include it in hello URI for hello template.</span></span> <span data-ttu-id="2173f-115">Merhaba sona erme saati tooallow yeterli zaman toocomplete hello dağıtım ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2173f-115">Set hello expiry time tooallow enough time toocomplete hello deployment.</span></span>
   
```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
token=$(az storage blob generate-sas \
    --container-name templates \
    --name vmlinux.json \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name vmlinux.json \
    --output tsv \
    --connection-string $connection)
az group deployment create --resource-group ExampleGroup --template-uri $url?$token
```

<span data-ttu-id="2173f-116">Bir SAS belirteci ile bağlı şablonları kullanma örneği için bkz: [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2173f-116">For an example of using a SAS token with linked templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2173f-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2173f-117">Next steps</span></span>
* <span data-ttu-id="2173f-118">Bir giriş toodeploying şablonları için bkz: [Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtmak](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2173f-118">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy-cli.md).</span></span>
* <span data-ttu-id="2173f-119">Bir şablon dağıtan bir tam örnek betik için bkz: [dağıtmak Resource Manager şablonu komut dosyası](resource-manager-samples-cli-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="2173f-119">For a complete sample script that deploys a template, see [Deploy Resource Manager template script](resource-manager-samples-cli-deploy.md)</span></span>
* <span data-ttu-id="2173f-120">Şablon toodefine parametrelerinde bkz [şablonları yazma](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="2173f-120">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="2173f-121">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="2173f-121">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
