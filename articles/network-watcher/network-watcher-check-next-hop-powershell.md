---
title: "Azure Ağ İzleyicisi sonraki atlama - PowerShell ile sonraki atlama Bul | Microsoft Docs"
description: "Bu makalede, sonraki atlama türü nedir nasıl bulabilir ve PowerShell kullanarak sonraki atlama kullanarak IP adresi anlatmaktadır."
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
ms.openlocfilehash: 00161e7c6fb4becdb7d8eab266fa27128e50f8ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-powershell"></a><span data-ttu-id="f379b-103">Hangi bir sonraki atlama türü sonraki atlama yetenek PowerShell kullanarak Azure Ağ İzleyicisi içinde kullandığını bulmak</span><span class="sxs-lookup"><span data-stu-id="f379b-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f379b-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="f379b-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="f379b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f379b-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="f379b-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f379b-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="f379b-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f379b-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="f379b-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="f379b-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="f379b-109">Sonraki atlama özelliğini get sonraki atlama türü ve belirtilen bir sanal makineye dayalı IP adresi sağlayan Ağ İzleyicisi özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="f379b-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="f379b-110">Bu özellik, bir sanal makine trafiğe bir ağ geçidi, internet veya sanal ağlar hedefine almak için geçiyorsa belirlemede yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="f379b-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f379b-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="f379b-111">Before you begin</span></span>

<span data-ttu-id="f379b-112">Bu senaryoda sonraki atlama türü ve IP adresini bulmak için Azure portalını kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="f379b-112">In this scenario, you will use the Azure portal to find the next hop type and IP address.</span></span>

<span data-ttu-id="f379b-113">Bu senaryo zaten izlediğiniz adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) bir Ağ İzleyicisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="f379b-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="f379b-114">Senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılacak var olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="f379b-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="f379b-115">Senaryo</span><span class="sxs-lookup"><span data-stu-id="f379b-115">Scenario</span></span>

<span data-ttu-id="f379b-116">Bu makalede ele alınan senaryosu, sonraki atlama, sonraki atlama türü ve IP adresi için bir kaynak bulur Ağ İzleyicisi özelliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="f379b-116">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="f379b-117">Sonraki atlama hakkında daha fazla bilgi için [sonraki atlama genel bakış](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f379b-117">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="f379b-118">Ağ İzleyicisi alma</span><span class="sxs-lookup"><span data-stu-id="f379b-118">Retrieve Network Watcher</span></span>

<span data-ttu-id="f379b-119">Ağ İzleyicisi örneği almak için ilk adımdır bakın.</span><span class="sxs-lookup"><span data-stu-id="f379b-119">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="f379b-120">`$networkWatcher` Değişkeni sonraki atlama geçirilen cmdlet doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f379b-120">The `$networkWatcher` variable is passed to the next hop verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a><span data-ttu-id="f379b-121">Bir sanal makine Al</span><span class="sxs-lookup"><span data-stu-id="f379b-121">Get a virtual machine</span></span>

<span data-ttu-id="f379b-122">Sonraki atlama, bir sanal makineden sonraki atlama ve sonraki atlama IP adresini döndürür.</span><span class="sxs-lookup"><span data-stu-id="f379b-122">Next hop returns the next hop and the IP address of the next hop from a virtual machine.</span></span> <span data-ttu-id="f379b-123">Bir sanal makine kimliği cmdlet'i için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f379b-123">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="f379b-124">Kullanmak için sanal makine Kimliğini biliyorsanız, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f379b-124">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> <span data-ttu-id="f379b-125">Sonraki atlama VM kaynak çalıştırmak için ayrılır gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f379b-125">Next hop requires that the VM resource is allocated to run.</span></span>

## <a name="get-the-network-interfaces"></a><span data-ttu-id="f379b-126">Ağ arabirimlerini Al</span><span class="sxs-lookup"><span data-stu-id="f379b-126">Get the network interfaces</span></span>

<span data-ttu-id="f379b-127">Bu örnekte, bir sanal makinede NIC alıyoruz sanal makinede bir NIC IP adresi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f379b-127">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="f379b-128">Sanal makinede test etmek istediğiniz IP adresi zaten biliyorsanız, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f379b-128">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a><span data-ttu-id="f379b-129">Sonraki atlama Al</span><span class="sxs-lookup"><span data-stu-id="f379b-129">Get Next Hop</span></span>

<span data-ttu-id="f379b-130">Diyoruz artık `Get-AzureRmNetworkWatcherNextHop` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="f379b-130">Now we call the `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span></span> <span data-ttu-id="f379b-131">Cmdlet Ağ İzleyicisi, sanal makine kimliği, kaynak IP adresi ve hedef IP adresi geçirin.</span><span class="sxs-lookup"><span data-stu-id="f379b-131">We pass the cmdlet the Network Watcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="f379b-132">Bu örnekte, başka bir sanal ağ içinde bir VM hedef IP adresi değil.</span><span class="sxs-lookup"><span data-stu-id="f379b-132">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="f379b-133">İki sanal ağ arasında bir sanal ağ geçidi yok.</span><span class="sxs-lookup"><span data-stu-id="f379b-133">There is a virtual network gateway between the two virtual networks.</span></span>

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a><span data-ttu-id="f379b-134">Sonuçları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="f379b-134">Review results</span></span>

<span data-ttu-id="f379b-135">Tamamlandığında, sonuçları sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f379b-135">When complete, the results are provided.</span></span> <span data-ttu-id="f379b-136">Sonraki atlama IP adresi bu kaynak türü yanı sıra döndürülür.</span><span class="sxs-lookup"><span data-stu-id="f379b-136">The next hop IP address is returned as well as the type of resource it is.</span></span> <span data-ttu-id="f379b-137">Bu senaryoda, sanal ağ geçidinin genel IP adresi değil.</span><span class="sxs-lookup"><span data-stu-id="f379b-137">In this scenario, it is the public IP address of the virtual network gateway.</span></span>

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

<span data-ttu-id="f379b-138">Aşağıdaki liste, şu anda kullanılabilir NextHopType değerleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="f379b-138">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="f379b-139">**Sonraki atlama türü**</span><span class="sxs-lookup"><span data-stu-id="f379b-139">**Next Hop Type**</span></span>

* <span data-ttu-id="f379b-140">Internet</span><span class="sxs-lookup"><span data-stu-id="f379b-140">Internet</span></span>
* <span data-ttu-id="f379b-141">Değerinin VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="f379b-141">VirtualAppliance</span></span>
* <span data-ttu-id="f379b-142">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="f379b-142">VirtualNetworkGateway</span></span>
* <span data-ttu-id="f379b-143">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="f379b-143">VnetLocal</span></span>
* <span data-ttu-id="f379b-144">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="f379b-144">HyperNetGateway</span></span>
* <span data-ttu-id="f379b-145">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="f379b-145">VnetPeering</span></span>
* <span data-ttu-id="f379b-146">None</span><span class="sxs-lookup"><span data-stu-id="f379b-146">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="f379b-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f379b-147">Next steps</span></span>

<span data-ttu-id="f379b-148">Ağ güvenlik grubu ayarlarınızı program aracılığıyla ziyaret ederek gözden öğrenin [NSG Denetim Ağ İzleyicisi](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="f379b-148">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

















