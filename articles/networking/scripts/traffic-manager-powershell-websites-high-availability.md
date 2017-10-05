---
title: "Azure PowerShell Betiği örnek - uygulamaların yüksek kullanılabilirlik için trafiği yönlendirme | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - uygulamaların yüksek kullanılabilirlik için trafiği yönlendirme"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: georgewallace
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 2f0ac4fd1779661aab04bafb217e64af5d619a2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="2964a-103">Uygulamaların yüksek kullanılabilirlik için trafiği yönlendirme</span><span class="sxs-lookup"><span data-stu-id="2964a-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="2964a-104">Bu komut dosyası, bir kaynak grubu, iki uygulama hizmeti planları, iki web uygulamaları, trafik Yöneticisi profili ve iki trafik Yöneticisi uç noktaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2964a-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="2964a-105">Birincil bölge uygulamada kullanılamadığında trafik Yöneticisi bir bölgede birincil bölge olarak uygulama ve ikincil bölge trafiğini yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="2964a-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span></span> <span data-ttu-id="2964a-106">Komut yürütülmeden önce Azure arasında benzersiz değerler mywebapp şeklindedir, MyWebAppL1 ve MyWebAppL2 değerleri değiştirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="2964a-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span></span> <span data-ttu-id="2964a-107">Betiği çalıştırdıktan sonra uygulama URL'si mywebapp.trafficmanager.net ile birincil bölgede erişebilir.</span><span class="sxs-lookup"><span data-stu-id="2964a-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="2964a-108">Gerekirse, bulunan yönergeleri kullanarak Azure PowerShell'i yükleme [Azure PowerShell Kılavuzu](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)ve ardından çalıştırın `Login-AzureRmAccount` Azure ile bir bağlantı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="2964a-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2964a-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="2964a-109">Sample script</span></span>

<span data-ttu-id="2964a-110">[!code-powershell[Ana](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "yüksek kullanılabilirlik için trafiği yönlendirmek")]</span><span class="sxs-lookup"><span data-stu-id="2964a-110">[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]</span></span>


<span data-ttu-id="2964a-111">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2964a-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="2964a-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="2964a-112">Script explanation</span></span>

<span data-ttu-id="2964a-113">Bu komut, bir kaynak grubu, web uygulaması, trafik Yöneticisi profili ve tüm ilgili kaynaklar oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="2964a-113">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="2964a-114">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="2964a-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2964a-115">Komut</span><span class="sxs-lookup"><span data-stu-id="2964a-115">Command</span></span> | <span data-ttu-id="2964a-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="2964a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2964a-117">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2964a-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="2964a-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2964a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2964a-119">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="2964a-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="2964a-120">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2964a-120">Creates an App Service plan.</span></span> <span data-ttu-id="2964a-121">Bu, Azure web uygulamanız için bir sunucu grubu gibidir.</span><span class="sxs-lookup"><span data-stu-id="2964a-121">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="2964a-122">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="2964a-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="2964a-123">Uygulama hizmeti planı içinde Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2964a-123">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="2964a-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="2964a-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="2964a-125">Uygulama hizmeti planı içinde Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2964a-125">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="2964a-126">AzureRmTrafficManagerProfile yeni</span><span class="sxs-lookup"><span data-stu-id="2964a-126">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="2964a-127">Bir Azure Traffic Manager profilini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2964a-127">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="2964a-128">AzureRmTrafficManagerEndpoint yeni</span><span class="sxs-lookup"><span data-stu-id="2964a-128">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="2964a-129">Bir uç noktası için bir Azure Traffic Manager profili ekler.</span><span class="sxs-lookup"><span data-stu-id="2964a-129">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2964a-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2964a-130">Next steps</span></span>

<span data-ttu-id="2964a-131">Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2964a-131">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="2964a-132">Ek ağ PowerShell komut dosyası örnekleri bulunabilir [Azure ağ genel görünümü belgelerine](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2964a-132">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>