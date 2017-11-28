---
title: "PowerShell komut dosyası örneği - aaaAzure atamak bir özel etki alanı tooa web uygulaması | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - Ata bir özel etki alanı tooa web uygulaması"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 356f5af9-f62e-411c-8b24-deba05214103
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 10224e800588019626ef25cbba4a926096779920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-custom-domain-tooa-web-app"></a><span data-ttu-id="012e0-103">Bir özel etki alanı tooa web uygulaması atayın</span><span class="sxs-lookup"><span data-stu-id="012e0-103">Assign a custom domain tooa web app</span></span>

<span data-ttu-id="012e0-104">Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur ve ardından eşler `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="012e0-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span> 

<span data-ttu-id="012e0-105">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](/powershell/azure/overview)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="012e0-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="012e0-106">Ayrıca, toohave erişim tooyour etki alanı kayıt şirketinizin DNS yapılandırma sayfası gerekir.</span><span class="sxs-lookup"><span data-stu-id="012e0-106">Also, you need toohave access tooyour domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="012e0-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="012e0-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="012e0-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="012e0-108">Clean up deployment</span></span> 

<span data-ttu-id="012e0-109">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, web uygulaması ve tüm ilişkili kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="012e0-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="012e0-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="012e0-110">Script explanation</span></span>

<span data-ttu-id="012e0-111">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="012e0-111">This script uses hello following commands.</span></span> <span data-ttu-id="012e0-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="012e0-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="012e0-113">Komut</span><span class="sxs-lookup"><span data-stu-id="012e0-113">Command</span></span> | <span data-ttu-id="012e0-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="012e0-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="012e0-115">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="012e0-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="012e0-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="012e0-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="012e0-117">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="012e0-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="012e0-118">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="012e0-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="012e0-119">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="012e0-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="012e0-120">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="012e0-120">Creates a web app.</span></span> |
| [<span data-ttu-id="012e0-121">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="012e0-121">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="012e0-122">Bir uygulama hizmeti planı toochange fiyatlandırma katmanı değiştirir.</span><span class="sxs-lookup"><span data-stu-id="012e0-122">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="012e0-123">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="012e0-123">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="012e0-124">Web uygulamanızın yapılandırmasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="012e0-124">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="012e0-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="012e0-125">Next steps</span></span>

<span data-ttu-id="012e0-126">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="012e0-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="012e0-127">Azure App Service Web Apps ek Azure Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="012e0-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
