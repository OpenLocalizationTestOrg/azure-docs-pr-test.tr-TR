---
title: "PowerShell komut dosyası örneği - yük dengeleyici açık uygulama bağlantı noktası aaaAzure | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - açık hello Azure yük dengeleyici Service Fabric uygulaması için bir bağlantı noktası."
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
ms.openlocfilehash: 6acb28942851dce63f89f7de362b7cf1dc7b1fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="open-an-application-port-in-hello-azure-load-balancer"></a><span data-ttu-id="4328b-103">Hello Azure yük dengeleyici bir uygulama bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="4328b-103">Open an application port in hello Azure load balancer</span></span>

<span data-ttu-id="4328b-104">Azure'da çalışan Service Fabric uygulaması hello Azure yük dengeleyici bulunur.</span><span class="sxs-lookup"><span data-stu-id="4328b-104">A Service Fabric application running in Azure sits behind hello Azure load balancer.</span></span> <span data-ttu-id="4328b-105">Bu örnek betik, bir bağlantı noktası bir Azure yük dengeleyici açar, böylece Service Fabric uygulaması dış istemcilerle iletişim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="4328b-105">This sample script opens a port in an Azure load balancer so that a Service Fabric application can communicate with external clients.</span></span> <span data-ttu-id="4328b-106">Merhaba parametrelerini gerektiği gibi özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4328b-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="4328b-107">Gerekirse, hello ile Merhaba Service Fabric PowerShell modülünü yüklemek [Service Fabric SDK](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4328b-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="4328b-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="4328b-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in hello load balancer")]

## <a name="script-explanation"></a><span data-ttu-id="4328b-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="4328b-109">Script explanation</span></span>

<span data-ttu-id="4328b-110">Bu komut dosyası komutları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="4328b-110">This script uses hello following commands.</span></span> <span data-ttu-id="4328b-111">Her komut hello tablosundaki toocommand özgü belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="4328b-111">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="4328b-112">Komut</span><span class="sxs-lookup"><span data-stu-id="4328b-112">Command</span></span> | <span data-ttu-id="4328b-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="4328b-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4328b-114">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="4328b-114">Get-AzureRmResource</span></span>](/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="4328b-115">Bir Azure kaynağı alır.</span><span class="sxs-lookup"><span data-stu-id="4328b-115">Gets an Azure resource.</span></span>  |
| [<span data-ttu-id="4328b-116">Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="4328b-116">Get-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancer) | <span data-ttu-id="4328b-117">Hello Azure yük dengeleyici alır.</span><span class="sxs-lookup"><span data-stu-id="4328b-117">Gets hello Azure load balancer.</span></span> |
| [<span data-ttu-id="4328b-118">Ekleme AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="4328b-118">Add-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | <span data-ttu-id="4328b-119">Bir araştırma yapılandırma tooa yük dengeleyici ekler.</span><span class="sxs-lookup"><span data-stu-id="4328b-119">Adds a probe configuration tooa load balancer.</span></span>|
| [<span data-ttu-id="4328b-120">Get-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="4328b-120">Get-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | <span data-ttu-id="4328b-121">Bir yük dengeleyici için bir araştırma yapılandırmasını alır.</span><span class="sxs-lookup"><span data-stu-id="4328b-121">Gets a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="4328b-122">Ekleme AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="4328b-122">Add-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | <span data-ttu-id="4328b-123">Bir kural yapılandırma tooa yük dengeleyici ekler.</span><span class="sxs-lookup"><span data-stu-id="4328b-123">Adds a rule configuration tooa load balancer.</span></span> |
| [<span data-ttu-id="4328b-124">Set-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="4328b-124">Set-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/set-azurermloadbalancer) | <span data-ttu-id="4328b-125">Ayarlar, bir yük dengeleyici için hedef durumu hello.</span><span class="sxs-lookup"><span data-stu-id="4328b-125">Sets hello goal state for a load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4328b-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4328b-126">Next steps</span></span>

<span data-ttu-id="4328b-127">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4328b-127">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4328b-128">Azure Service Fabric ek Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4328b-128">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
