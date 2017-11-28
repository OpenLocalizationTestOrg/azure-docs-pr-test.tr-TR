---
title: "Azure PowerShell Betiği örnek - yük dengeleyici açık uygulama bağlantı noktası | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - açık Azure yük dengeleyici Service Fabric uygulaması için bir bağlantı noktası."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 2958bdef0889076249918608c04c66678fa80b97
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="open-an-application-port-in-the-azure-load-balancer"></a><span data-ttu-id="cc1c8-103">Azure yük dengeleyici bir uygulama bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="cc1c8-103">Open an application port in the Azure load balancer</span></span>

<span data-ttu-id="cc1c8-104">Azure'da çalışan Service Fabric uygulaması Azure yük dengeleyici bulunur.</span><span class="sxs-lookup"><span data-stu-id="cc1c8-104">A Service Fabric application running in Azure sits behind the Azure load balancer.</span></span> <span data-ttu-id="cc1c8-105">Bu örnek betik, bir bağlantı noktası bir Azure yük dengeleyici açar, böylece Service Fabric uygulaması dış istemcilerle iletişim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="cc1c8-105">This sample script opens a port in an Azure load balancer so that a Service Fabric application can communicate with external clients.</span></span> <span data-ttu-id="cc1c8-106">Parametreleri gerektiği gibi özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="cc1c8-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="cc1c8-107">Gerekirse, ile Service Fabric PowerShell modülünü yüklemek [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cc1c8-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="cc1c8-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="cc1c8-108">Sample script</span></span>

<span data-ttu-id="cc1c8-109">[!code-powershell[Ana](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "bir bağlantı noktası yük dengeleyicide açın")]</span><span class="sxs-lookup"><span data-stu-id="cc1c8-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in the load balancer")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="cc1c8-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="cc1c8-110">Script explanation</span></span>

<span data-ttu-id="cc1c8-111">Bu komut dosyasını aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="cc1c8-111">This script uses the following commands.</span></span> <span data-ttu-id="cc1c8-112">Komut özgü belgelere Tablo bağlantıları her komut.</span><span class="sxs-lookup"><span data-stu-id="cc1c8-112">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="cc1c8-113">Komut</span><span class="sxs-lookup"><span data-stu-id="cc1c8-113">Command</span></span> | <span data-ttu-id="cc1c8-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="cc1c8-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cc1c8-115">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="cc1c8-115">Get-AzureRmResource</span></span>](/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="cc1c8-116">Bir Azure kaynağı alır.</span><span class="sxs-lookup"><span data-stu-id="cc1c8-116">Gets an Azure resource.</span></span>  |
| [<span data-ttu-id="cc1c8-117">Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="cc1c8-117">Get-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancer) | <span data-ttu-id="cc1c8-118">Azure yük dengeleyici alır.</span><span class="sxs-lookup"><span data-stu-id="cc1c8-118">Gets the Azure load balancer.</span></span> |
| [<span data-ttu-id="cc1c8-119">Ekleme AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="cc1c8-119">Add-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | <span data-ttu-id="cc1c8-120">Bir araştırma yapılandırması bir yük dengeleyiciye ekler.</span><span class="sxs-lookup"><span data-stu-id="cc1c8-120">Adds a probe configuration to a load balancer.</span></span>|
| [<span data-ttu-id="cc1c8-121">Get-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="cc1c8-121">Get-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | <span data-ttu-id="cc1c8-122">Bir yük dengeleyici için bir araştırma yapılandırmasını alır.</span><span class="sxs-lookup"><span data-stu-id="cc1c8-122">Gets a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="cc1c8-123">Ekleme AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="cc1c8-123">Add-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | <span data-ttu-id="cc1c8-124">Kural yapılandırması bir yük dengeleyiciye ekler.</span><span class="sxs-lookup"><span data-stu-id="cc1c8-124">Adds a rule configuration to a load balancer.</span></span> |
| [<span data-ttu-id="cc1c8-125">Set-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="cc1c8-125">Set-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/set-azurermloadbalancer) | <span data-ttu-id="cc1c8-126">Hedef durumu bir yük dengeleyici için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="cc1c8-126">Sets the goal state for a load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cc1c8-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cc1c8-127">Next steps</span></span>

<span data-ttu-id="cc1c8-128">Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cc1c8-128">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="cc1c8-129">Azure Service Fabric ek Powershell örnekleri bulunabilir [Azure PowerShell örnekleri](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="cc1c8-129">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
