---
title: "Azure PowerShell Betiği örnek - bir web uygulaması oluşturma ve kod github'dan dağıtma | Microsoft Docs"
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
ms.openlocfilehash: 1f7fc21dc12c334f5d347ae9918bd62945bede64
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-from-github"></a><span data-ttu-id="1a4fe-103">Bir web uygulaması oluşturma ve github'dan kod dağıtma</span><span class="sxs-lookup"><span data-stu-id="1a4fe-103">Create a web app and deploy code from GitHub</span></span>

<span data-ttu-id="1a4fe-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur ve web uygulama kodunuzdan (olmadan sürekli dağıtımı) genel bir GitHub depo dağıtır.</span><span class="sxs-lookup"><span data-stu-id="1a4fe-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="1a4fe-105">Sürekli dağıtım GitHub dağıtımı için bkz: [github'dan sürekli dağıtımı ile bir web uygulaması oluşturma](app-service-powershell-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="1a4fe-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span></span>

<span data-ttu-id="1a4fe-106">Gerekirse, bulunan yönergeleri kullanarak Azure PowerShell'i yükleme [Azure PowerShell Kılavuzu](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1a4fe-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="1a4fe-107">Ayrıca, web uygulama kodunu içeren GitHub deposunu bağlantısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="1a4fe-107">Also, you need a link to GitHub repository that contains the web app code.</span></span>

## <a name="sample-script"></a><span data-ttu-id="1a4fe-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="1a4fe-108">Sample script</span></span>

<span data-ttu-id="1a4fe-109">[!code-powershell[Ana](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "bir web uygulaması oluşturma ve github'dan kod dağıtma")]</span><span class="sxs-lookup"><span data-stu-id="1a4fe-109">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Create a web app and deploy code from GitHub")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="1a4fe-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="1a4fe-110">Clean up deployment</span></span> 

<span data-ttu-id="1a4fe-111">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu, web uygulaması ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1a4fe-111">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="1a4fe-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="1a4fe-112">Script explanation</span></span>

<span data-ttu-id="1a4fe-113">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="1a4fe-113">This script uses the following commands.</span></span> <span data-ttu-id="1a4fe-114">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="1a4fe-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1a4fe-115">Komut</span><span class="sxs-lookup"><span data-stu-id="1a4fe-115">Command</span></span> | <span data-ttu-id="1a4fe-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="1a4fe-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1a4fe-117">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1a4fe-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="1a4fe-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1a4fe-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1a4fe-119">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="1a4fe-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="1a4fe-120">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1a4fe-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="1a4fe-121">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="1a4fe-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="1a4fe-122">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1a4fe-122">Creates a web app.</span></span> |
| [<span data-ttu-id="1a4fe-123">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="1a4fe-123">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="1a4fe-124">Bir kaynak bir kaynak grubu olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="1a4fe-124">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1a4fe-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1a4fe-125">Next steps</span></span>

<span data-ttu-id="1a4fe-126">Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1a4fe-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1a4fe-127">Azure App Service Web Apps ek Azure Powershell örnekleri bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1a4fe-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
