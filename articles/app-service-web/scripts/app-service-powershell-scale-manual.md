---
title: "Azure PowerShell Betiği örnek - bir web uygulaması elle ölçeklendirme | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bir web uygulaması elle ölçeklendirme"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: de5d4285-9c7d-4735-a695-288264047375
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: e99dfc02b6ab4123cd5f95997285dca5cb686380
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="2be78-103">Bir web uygulaması elle ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="2be78-103">Scale a web app manually</span></span>

<span data-ttu-id="2be78-104">Bu senaryoda, bir kaynak grubu, uygulama hizmeti planı ve web uygulaması oluşturmak öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="2be78-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="2be78-105">Ardından, uygulama hizmeti planı tek bir örnekten birden çok örneklerine ölçeklenir.</span><span class="sxs-lookup"><span data-stu-id="2be78-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

<span data-ttu-id="2be78-106">Gerekirse, bulunan yönergeleri kullanarak Azure PowerShell'i yükleme [Azure PowerShell Kılavuzu](/powershell/azure/overview)ve ardından çalıştırın `Login-AzureRmAccount` Azure ile bir bağlantı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="2be78-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="2be78-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="2be78-107">Sample script</span></span>

<span data-ttu-id="2be78-108">[!code-powershell[Ana](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "bir web uygulaması elle ölçeklendirme")]</span><span class="sxs-lookup"><span data-stu-id="2be78-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2be78-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="2be78-109">Clean up deployment</span></span> 

<span data-ttu-id="2be78-110">Komut dosyası örneği çalıştırdıktan sonra kaynak grubu, web uygulaması ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2be78-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="2be78-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="2be78-111">Script explanation</span></span>

<span data-ttu-id="2be78-112">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="2be78-112">This script uses the following commands.</span></span> <span data-ttu-id="2be78-113">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="2be78-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2be78-114">Komut</span><span class="sxs-lookup"><span data-stu-id="2be78-114">Command</span></span> | <span data-ttu-id="2be78-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="2be78-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2be78-116">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2be78-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="2be78-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2be78-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2be78-118">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="2be78-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="2be78-119">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2be78-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="2be78-120">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="2be78-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="2be78-121">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2be78-121">Creates a web app.</span></span> |
| [<span data-ttu-id="2be78-122">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="2be78-122">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="2be78-123">Web uygulamanızın yapılandırmasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="2be78-123">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2be78-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2be78-124">Next steps</span></span>

<span data-ttu-id="2be78-125">Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2be78-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2be78-126">Azure App Service Web Apps ek Azure Powershell örnekleri bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2be78-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
