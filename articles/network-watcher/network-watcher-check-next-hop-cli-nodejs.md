---
title: "Azure Ağ İzleyicisi sonraki atlama - Azure CLI 1.0 ile sonraki atlama Bul | Microsoft Docs"
description: "Bu makalede, sonraki atlama türü nedir nasıl bulabilir ve Azure CLI kullanarak sonraki atlama kullanarak IP adresi anlatmaktadır."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: ff88e945060ae033717ceb29db1352e112f05a3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="fd7b2-103">Hangi bir sonraki atlama türü sonraki atlama yetenek Azure CLI 1.0 kullanarak Azure Ağ İzleyicisi içinde kullandığını bulmak</span><span class="sxs-lookup"><span data-stu-id="fd7b2-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="fd7b2-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="fd7b2-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="fd7b2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd7b2-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="fd7b2-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="fd7b2-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="fd7b2-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="fd7b2-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="fd7b2-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="fd7b2-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="fd7b2-109">Sonraki atlama özelliğini get sonraki atlama türü ve belirtilen bir sanal makineye dayalı IP adresi sağlayan Ağ İzleyicisi özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="fd7b2-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="fd7b2-110">Bu özellik, bir sanal makine trafiğe bir ağ geçidi, internet veya sanal ağlar hedefine almak için geçiyorsa belirlemede yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="fd7b2-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

<span data-ttu-id="fd7b2-111">Bu makalede, platformlar arası Azure CLI 1.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.</span><span class="sxs-lookup"><span data-stu-id="fd7b2-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fd7b2-112">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="fd7b2-112">Before you begin</span></span>

<span data-ttu-id="fd7b2-113">Bu senaryoda sonraki atlama türü ve IP adresini bulmak için Azure CLI kullanır.</span><span class="sxs-lookup"><span data-stu-id="fd7b2-113">In this scenario, you will use the Azure CLI to find the next hop type and IP address.</span></span>

<span data-ttu-id="fd7b2-114">Bu senaryo zaten izlediğiniz adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) bir Ağ İzleyicisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="fd7b2-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="fd7b2-115">Senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılacak var olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="fd7b2-115">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="fd7b2-116">Senaryo</span><span class="sxs-lookup"><span data-stu-id="fd7b2-116">Scenario</span></span>

<span data-ttu-id="fd7b2-117">Bu makalede ele alınan senaryosu, sonraki atlama, sonraki atlama türü ve IP adresi için bir kaynak bulur Ağ İzleyicisi özelliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="fd7b2-117">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="fd7b2-118">Sonraki atlama hakkında daha fazla bilgi için [sonraki atlama genel bakış](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fd7b2-118">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="fd7b2-119">Sonraki atlama Al</span><span class="sxs-lookup"><span data-stu-id="fd7b2-119">Get Next Hop</span></span>

<span data-ttu-id="fd7b2-120">Diyoruz sonraki atlama almak için `azure netowrk watcher next-hop` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="fd7b2-120">To get the next hop we call the `azure netowrk watcher next-hop` cmdlet.</span></span> <span data-ttu-id="fd7b2-121">Cmdlet Ağ İzleyicisi kaynak grubu, NetworkWatcher, sanal makine kimliği, kaynak IP adresi ve hedef IP adresi geçirin.</span><span class="sxs-lookup"><span data-stu-id="fd7b2-121">We pass the cmdlet the Network Watcher resource group, the NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="fd7b2-122">Bu örnekte, başka bir sanal ağ içinde bir VM hedef IP adresi değil.</span><span class="sxs-lookup"><span data-stu-id="fd7b2-122">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="fd7b2-123">İki sanal ağ arasında bir sanal ağ geçidi yok.</span><span class="sxs-lookup"><span data-stu-id="fd7b2-123">There is a virtual network gateway between the two virtual networks.</span></span> 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
<span data-ttu-id="fd7b2-124">Birden çok NIC VM varsa ve IP iletimini herhangi NIC'ler, daha sonra NIC parametre etkinse (-ı NIC-ID) belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="fd7b2-124">If the VM has multiple NICs and IP forwarding is enabled on any of the NICs, then the NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="fd7b2-125">Aksi takdirde isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="fd7b2-125">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="fd7b2-126">Sonuçları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="fd7b2-126">Review results</span></span>

<span data-ttu-id="fd7b2-127">Tamamlandığında, sonuçları sağlanır.</span><span class="sxs-lookup"><span data-stu-id="fd7b2-127">When complete, the results are provided.</span></span> <span data-ttu-id="fd7b2-128">Sonraki atlama IP adresi bu kaynak türü yanı sıra döndürülür.</span><span class="sxs-lookup"><span data-stu-id="fd7b2-128">The next hop IP address is returned as well as the type of resource it is.</span></span>

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

<span data-ttu-id="fd7b2-129">Aşağıdaki liste, şu anda kullanılabilir NextHopType değerleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="fd7b2-129">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="fd7b2-130">**Sonraki atlama türü**</span><span class="sxs-lookup"><span data-stu-id="fd7b2-130">**Next Hop Type**</span></span>

* <span data-ttu-id="fd7b2-131">Internet</span><span class="sxs-lookup"><span data-stu-id="fd7b2-131">Internet</span></span>
* <span data-ttu-id="fd7b2-132">Değerinin VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="fd7b2-132">VirtualAppliance</span></span>
* <span data-ttu-id="fd7b2-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="fd7b2-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="fd7b2-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="fd7b2-134">VnetLocal</span></span>
* <span data-ttu-id="fd7b2-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="fd7b2-135">HyperNetGateway</span></span>
* <span data-ttu-id="fd7b2-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="fd7b2-136">VnetPeering</span></span>
* <span data-ttu-id="fd7b2-137">None</span><span class="sxs-lookup"><span data-stu-id="fd7b2-137">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd7b2-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fd7b2-138">Next steps</span></span>

<span data-ttu-id="fd7b2-139">Ağ güvenlik grubu ayarlarınızı program aracılığıyla ziyaret ederek gözden öğrenin [NSG Denetim Ağ İzleyicisi](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="fd7b2-139">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
