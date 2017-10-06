---
title: "aaaAzure PowerShell komut dosyası örneği - bir web uygulaması dünya çapında yüksek kullanılabilirlik mimarisi ile ölçeklendirin | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - ölçek yüksek kullanılabilirlik mimarisiyle dünya çapında bir web uygulaması"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1fcda23250efe4966d63c5dfa744b76c26f3762a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="1a1ed-103">Bir web uygulaması dünya çapında yüksek kullanılabilirlik mimarisi ile ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="1a1ed-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="1a1ed-104">Bu senaryoda, bir kaynak grubu, iki uygulama hizmeti planları, iki web uygulamaları, trafik Yöneticisi profili ve iki trafik Yöneticisi uç noktaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1a1ed-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="1a1ed-105">Merhaba alıştırma tamamlandıktan sonra bir yüksek kullanılabilir olacaktır sağlayan mimari hello en düşük ağ gecikmesine bağlı, web uygulamanızın genel kullanılabilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="1a1ed-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

<span data-ttu-id="1a1ed-106">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](/powershell/azure/overview)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="1a1ed-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="1a1ed-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="1a1ed-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1a1ed-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="1a1ed-108">Clean up deployment</span></span> 

<span data-ttu-id="1a1ed-109">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, web uygulaması ve tüm ilişkili kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="1a1ed-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="1a1ed-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="1a1ed-110">Script explanation</span></span>

<span data-ttu-id="1a1ed-111">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="1a1ed-111">This script uses hello following commands.</span></span> <span data-ttu-id="1a1ed-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="1a1ed-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1a1ed-113">Komut</span><span class="sxs-lookup"><span data-stu-id="1a1ed-113">Command</span></span> | <span data-ttu-id="1a1ed-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="1a1ed-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1a1ed-115">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1a1ed-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="1a1ed-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1a1ed-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1a1ed-117">AzureRMTrafficManagerProfile yeni</span><span class="sxs-lookup"><span data-stu-id="1a1ed-117">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="1a1ed-118">Trafik Yöneticisi profili oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1a1ed-118">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="1a1ed-119">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="1a1ed-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="1a1ed-120">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1a1ed-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="1a1ed-121">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="1a1ed-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="1a1ed-122">Bir web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1a1ed-122">Creates a web app.</span></span> |
| [<span data-ttu-id="1a1ed-123">AzureRMTrafficManagerEndpoint yeni</span><span class="sxs-lookup"><span data-stu-id="1a1ed-123">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="1a1ed-124">Bir uç nokta bir Traffic Manager profilini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1a1ed-124">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1a1ed-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1a1ed-125">Next steps</span></span>

<span data-ttu-id="1a1ed-126">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1a1ed-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1a1ed-127">Azure App Service Web Apps ek Azure Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1a1ed-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
