---
title: "aaaAzure PowerShell komut dosyası örneği - bir web uygulaması oluşturma ve kod github'dan dağıtma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bir web uygulaması oluşturma ve github'dan kod dağıtma"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 9a28f9cb01b71c86fa0a3f1d0a6761fc3d45d43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-github"></a><span data-ttu-id="7ba2e-103">Bir web uygulaması oluşturma ve github'dan kod dağıtma</span><span class="sxs-lookup"><span data-stu-id="7ba2e-103">Create a web app and deploy code from GitHub</span></span>

<span data-ttu-id="7ba2e-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur ve web uygulama kodunuzdan (olmadan sürekli dağıtımı) genel bir GitHub depo dağıtır.</span><span class="sxs-lookup"><span data-stu-id="7ba2e-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="7ba2e-105">Sürekli dağıtım GitHub dağıtımı için bkz: [github'dan sürekli dağıtımı ile bir web uygulaması oluşturma](app-service-powershell-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="7ba2e-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span></span>

<span data-ttu-id="7ba2e-106">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7ba2e-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="7ba2e-107">Ayrıca, hello web uygulama kodu içeren bir bağlantı tooGitHub deposu gerekir.</span><span class="sxs-lookup"><span data-stu-id="7ba2e-107">Also, you need a link tooGitHub repository that contains hello web app code.</span></span>

## <a name="sample-script"></a><span data-ttu-id="7ba2e-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="7ba2e-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Create a web app and deploy code from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7ba2e-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="7ba2e-109">Clean up deployment</span></span> 

<span data-ttu-id="7ba2e-110">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, web uygulaması ve tüm ilişkili kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="7ba2e-110">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="7ba2e-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="7ba2e-111">Script explanation</span></span>

<span data-ttu-id="7ba2e-112">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="7ba2e-112">This script uses hello following commands.</span></span> <span data-ttu-id="7ba2e-113">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="7ba2e-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7ba2e-114">Komut</span><span class="sxs-lookup"><span data-stu-id="7ba2e-114">Command</span></span> | <span data-ttu-id="7ba2e-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="7ba2e-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7ba2e-116">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7ba2e-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="7ba2e-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7ba2e-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7ba2e-118">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="7ba2e-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="7ba2e-119">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7ba2e-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="7ba2e-120">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="7ba2e-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="7ba2e-121">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7ba2e-121">Creates a web app.</span></span> |
| [<span data-ttu-id="7ba2e-122">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="7ba2e-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="7ba2e-123">Bir kaynak bir kaynak grubu olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="7ba2e-123">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7ba2e-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7ba2e-124">Next steps</span></span>

<span data-ttu-id="7ba2e-125">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7ba2e-125">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7ba2e-126">Azure App Service Web Apps ek Azure Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7ba2e-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
