---
title: "PowerShell komut dosyası örneği - uygulamaların yüksek kullanılabilirlik için trafiği yönlendirme aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 11d15780403b4ed79e85d7b3495bc5d674bfdaee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="eadbb-103">Uygulamaların yüksek kullanılabilirlik için trafiği yönlendirme</span><span class="sxs-lookup"><span data-stu-id="eadbb-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="eadbb-104">Bu komut dosyası, bir kaynak grubu, iki uygulama hizmeti planları, iki web uygulamaları, trafik Yöneticisi profili ve iki trafik Yöneticisi uç noktaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eadbb-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="eadbb-105">Merhaba uygulaması hello birincil bölgede kullanılamaz duruma geldiğinde traffic Manager trafik toohello uygulamada hello birincil bölge olarak tek bir bölge ve toohello ikincil bölge yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="eadbb-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="eadbb-106">Hello betiği yürütülürken önce hello mywebapp şeklindedir, MyWebAppL1 değiştirmeniz gerekir ve Azure arasında toounique değerleri MyWebAppL2 değerleri.</span><span class="sxs-lookup"><span data-stu-id="eadbb-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="eadbb-107">Hello komut dosyasını çalıştırdıktan sonra hello birincil bölge hello URL mywebapp.trafficmanager.net ile Merhaba uygulamasında erişebilir.</span><span class="sxs-lookup"><span data-stu-id="eadbb-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="eadbb-108">Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="eadbb-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="eadbb-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="eadbb-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]


<span data-ttu-id="eadbb-110">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="eadbb-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="eadbb-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="eadbb-111">Script explanation</span></span>

<span data-ttu-id="eadbb-112">Bu komut dosyasını aşağıdaki komutları toocreate bir kaynak grubu, web uygulaması, trafik Yöneticisi profili hello kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="eadbb-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="eadbb-113">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="eadbb-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="eadbb-114">Komut</span><span class="sxs-lookup"><span data-stu-id="eadbb-114">Command</span></span> | <span data-ttu-id="eadbb-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="eadbb-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="eadbb-116">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="eadbb-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="eadbb-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eadbb-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="eadbb-118">AzureRmAppServicePlan yeni</span><span class="sxs-lookup"><span data-stu-id="eadbb-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="eadbb-119">App Service planı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eadbb-119">Creates an App Service plan.</span></span> <span data-ttu-id="eadbb-120">Bu, Azure web uygulamanız için bir sunucu grubu gibidir.</span><span class="sxs-lookup"><span data-stu-id="eadbb-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="eadbb-121">AzureRmWebApp yeni</span><span class="sxs-lookup"><span data-stu-id="eadbb-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="eadbb-122">Merhaba uygulama hizmeti planı içinde Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eadbb-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="eadbb-123">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="eadbb-123">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="eadbb-124">Merhaba uygulama hizmeti planı içinde Azure web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eadbb-124">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="eadbb-125">AzureRmTrafficManagerProfile yeni</span><span class="sxs-lookup"><span data-stu-id="eadbb-125">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="eadbb-126">Bir Azure Traffic Manager profilini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eadbb-126">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="eadbb-127">AzureRmTrafficManagerEndpoint yeni</span><span class="sxs-lookup"><span data-stu-id="eadbb-127">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="eadbb-128">Uç nokta tooan Azure trafik Yöneticisi profili ekler.</span><span class="sxs-lookup"><span data-stu-id="eadbb-128">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="eadbb-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eadbb-129">Next steps</span></span>

<span data-ttu-id="eadbb-130">Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="eadbb-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="eadbb-131">Ek ağ PowerShell komut dosyası örnekleri hello bulunabilir [Azure ağ genel görünümü belgelerine](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eadbb-131">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
