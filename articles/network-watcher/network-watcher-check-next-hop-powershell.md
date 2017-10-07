---
title: "Azure Ağ İzleyicisi sonraki atlama - PowerShell ile aaaFind sonraki atlama | Microsoft Docs"
description: "Bu makale, hangi hello sonraki atlama türü olduğunu ve IP adresini kullanarak sonraki atlama PowerShell kullanarak nasıl bulabilirsiniz anlatmaktadır."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a><span data-ttu-id="6ce91-103">Hangi hello sonraki atlama türü hello sonraki atlama yetenek PowerShell kullanarak Azure Ağ İzleyicisi içinde kullandığını bulmak</span><span class="sxs-lookup"><span data-stu-id="6ce91-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="6ce91-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="6ce91-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="6ce91-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ce91-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="6ce91-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6ce91-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="6ce91-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6ce91-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="6ce91-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="6ce91-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="6ce91-109">Sonraki atlama bir özelliği olan Ağ İzleyicisi'hello yeteneği sağlar, hello sonraki atlama türü ve belirtilen bir sanal makineye dayalı IP adresi al ' dir.</span><span class="sxs-lookup"><span data-stu-id="6ce91-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="6ce91-110">Bu özellik, bir sanal makine trafiğe bir ağ geçidi, internet veya sanal ağlar tooget tooits hedef geçiyorsa belirlemede yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="6ce91-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6ce91-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="6ce91-111">Before you begin</span></span>

<span data-ttu-id="6ce91-112">Bu senaryoda, hello Azure portal toofind hello sonraki atlama türü ve IP adresini kullanır.</span><span class="sxs-lookup"><span data-stu-id="6ce91-112">In this scenario, you will use hello Azure portal toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="6ce91-113">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="6ce91-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="6ce91-114">Merhaba senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılan toobe var olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="6ce91-114">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="6ce91-115">Senaryo</span><span class="sxs-lookup"><span data-stu-id="6ce91-115">Scenario</span></span>

<span data-ttu-id="6ce91-116">Bu makalede ele alınan hello senaryosu, sonraki atlama, bir özelliği olan Ağ İzleyicisi'hello sonraki atlama türü ve IP adresi için bir kaynak bulur kullanır.</span><span class="sxs-lookup"><span data-stu-id="6ce91-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="6ce91-117">Sonraki atlama, hakkında daha fazla toolearn ziyaret [sonraki atlama genel bakış](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6ce91-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="6ce91-118">Ağ İzleyicisi alma</span><span class="sxs-lookup"><span data-stu-id="6ce91-118">Retrieve Network Watcher</span></span>

<span data-ttu-id="6ce91-119">Merhaba ilk adımı tooretrieve hello Ağ İzleyicisi örneğidir.</span><span class="sxs-lookup"><span data-stu-id="6ce91-119">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="6ce91-120">Merhaba `$networkWatcher` değişkeni toohello sonraki atlama geçirilen cmdlet doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="6ce91-120">hello `$networkWatcher` variable is passed toohello next hop verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a><span data-ttu-id="6ce91-121">Bir sanal makine Al</span><span class="sxs-lookup"><span data-stu-id="6ce91-121">Get a virtual machine</span></span>

<span data-ttu-id="6ce91-122">Sonraki atlama hello sonraki atlama ve hello sonraki atlamanın IP adresi hello bir sanal makineden döndürür.</span><span class="sxs-lookup"><span data-stu-id="6ce91-122">Next hop returns hello next hop and hello IP address of hello next hop from a virtual machine.</span></span> <span data-ttu-id="6ce91-123">Bir sanal makine kimliği hello cmdlet'i için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="6ce91-123">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="6ce91-124">Merhaba sanal makine toouse hello Kimliğini biliyorsanız, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ce91-124">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> <span data-ttu-id="6ce91-125">Sonraki atlama hello VM kaynak toorun ayrılır gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6ce91-125">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="get-hello-network-interfaces"></a><span data-ttu-id="6ce91-126">Merhaba ağ arabirimlerini Al</span><span class="sxs-lookup"><span data-stu-id="6ce91-126">Get hello network interfaces</span></span>

<span data-ttu-id="6ce91-127">Bu örnekte, bir sanal makinede hello NIC'ler alıyoruz hello sanal makinede bir NIC Hello IP adresi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="6ce91-127">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="6ce91-128">Başlangıç IP adresini biliyorsanız tootest istediğiniz hello sanal makinede, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ce91-128">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a><span data-ttu-id="6ce91-129">Sonraki atlama Al</span><span class="sxs-lookup"><span data-stu-id="6ce91-129">Get Next Hop</span></span>

<span data-ttu-id="6ce91-130">Merhaba diyoruz artık `Get-AzureRmNetworkWatcherNextHop` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="6ce91-130">Now we call hello `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span></span> <span data-ttu-id="6ce91-131">Biz hello cmdlet hello Ağ İzleyicisi, sanal makine kimliği geçişi, kaynak IP adresi ve hedef IP adresi.</span><span class="sxs-lookup"><span data-stu-id="6ce91-131">We pass hello cmdlet hello Network Watcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="6ce91-132">Bu örnekte, başka bir sanal ağda tooa VM hello hedef IP adresi değil.</span><span class="sxs-lookup"><span data-stu-id="6ce91-132">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="6ce91-133">Merhaba iki sanal ağ arasında bir sanal ağ geçidi yok.</span><span class="sxs-lookup"><span data-stu-id="6ce91-133">There is a virtual network gateway between hello two virtual networks.</span></span>

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a><span data-ttu-id="6ce91-134">Sonuçları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="6ce91-134">Review results</span></span>

<span data-ttu-id="6ce91-135">Tamamlandığında, hello sonuçları sağlanır.</span><span class="sxs-lookup"><span data-stu-id="6ce91-135">When complete, hello results are provided.</span></span> <span data-ttu-id="6ce91-136">Merhaba sonraki atlama IP adresi bu kaynak hello türü yanı sıra döndürülür.</span><span class="sxs-lookup"><span data-stu-id="6ce91-136">hello next hop IP address is returned as well as hello type of resource it is.</span></span> <span data-ttu-id="6ce91-137">Bu senaryoda, hello hello sanal ağ geçidi genel IP adresi değil.</span><span class="sxs-lookup"><span data-stu-id="6ce91-137">In this scenario, it is hello public IP address of hello virtual network gateway.</span></span>

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

<span data-ttu-id="6ce91-138">Merhaba aşağıdaki listede hello şu anda kullanılabilir NextHopType değerleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="6ce91-138">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="6ce91-139">**Sonraki atlama türü**</span><span class="sxs-lookup"><span data-stu-id="6ce91-139">**Next Hop Type**</span></span>

* <span data-ttu-id="6ce91-140">Internet</span><span class="sxs-lookup"><span data-stu-id="6ce91-140">Internet</span></span>
* <span data-ttu-id="6ce91-141">Değerinin VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="6ce91-141">VirtualAppliance</span></span>
* <span data-ttu-id="6ce91-142">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="6ce91-142">VirtualNetworkGateway</span></span>
* <span data-ttu-id="6ce91-143">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="6ce91-143">VnetLocal</span></span>
* <span data-ttu-id="6ce91-144">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="6ce91-144">HyperNetGateway</span></span>
* <span data-ttu-id="6ce91-145">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="6ce91-145">VnetPeering</span></span>
* <span data-ttu-id="6ce91-146">None</span><span class="sxs-lookup"><span data-stu-id="6ce91-146">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ce91-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6ce91-147">Next steps</span></span>

<span data-ttu-id="6ce91-148">Bilgi nasıl tooreview ağ güvenlik grubu ayarlarınızı programlı olarak şu adresi ziyaret ederek [NSG Denetim Ağ İzleyicisi](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="6ce91-148">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

















