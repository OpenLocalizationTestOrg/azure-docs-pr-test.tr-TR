---
title: "Azure Ağ İzleyicisi sonraki atlama - Azure portal ile sonraki atlama Bul | Microsoft Docs"
description: "Bu makalede, sonraki atlama türü nedir nasıl bulabilir ve Azure portalını kullanarak sonraki atlama kullanarak IP adresi anlatmaktadır."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5434b7972346821985c459fc4620805adb88676b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-the-portal"></a><span data-ttu-id="6f585-103">Hangi bir sonraki atlama türü sonraki atlama yetenek Portalı'nı kullanarak Azure Ağ İzleyicisi içinde kullandığını bulmak</span><span class="sxs-lookup"><span data-stu-id="6f585-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using the portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="6f585-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="6f585-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="6f585-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f585-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="6f585-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6f585-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="6f585-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6f585-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="6f585-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="6f585-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="6f585-109">Sonraki atlama özelliğini get sonraki atlama türü ve belirtilen bir sanal makineye dayalı IP adresi sağlayan Ağ İzleyicisi özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="6f585-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="6f585-110">Bu özellik, bir sanal makine trafiğe bir ağ geçidi, internet veya sanal ağlar hedefine almak için geçiyorsa belirlemede yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="6f585-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6f585-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="6f585-111">Before you begin</span></span>

<span data-ttu-id="6f585-112">Bu senaryo zaten izlediğiniz adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) bir Ağ İzleyicisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="6f585-112">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="6f585-113">Senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılacak var olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="6f585-113">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="6f585-114">Senaryo</span><span class="sxs-lookup"><span data-stu-id="6f585-114">Scenario</span></span>

<span data-ttu-id="6f585-115">Bu makalede ele alınan senaryo sonraki atlama sonraki atlama türü ve kaynak IP adresini bulmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="6f585-115">The scenario covered in this article uses Next hop to find out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="6f585-116">Sonraki atlama hakkında daha fazla bilgi için [sonraki atlama genel bakış](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6f585-116">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="6f585-117">Bu senaryoda, şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="6f585-117">In this scenario, you will:</span></span>

* <span data-ttu-id="6f585-118">Sonraki atlama bir sanal makineden alın.</span><span class="sxs-lookup"><span data-stu-id="6f585-118">Retrieve the next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="6f585-119">Sonraki atlama Al</span><span class="sxs-lookup"><span data-stu-id="6f585-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="6f585-120">1. Adım</span><span class="sxs-lookup"><span data-stu-id="6f585-120">Step 1</span></span>

<span data-ttu-id="6f585-121">Ağ İzleyicisi kaynağınız Azure portalında gidin.</span><span class="sxs-lookup"><span data-stu-id="6f585-121">Navigate to your Network Watcher resource in the Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="6f585-122">2. Adım</span><span class="sxs-lookup"><span data-stu-id="6f585-122">Step 2</span></span>

<span data-ttu-id="6f585-123">Tıklatın **sonraki atlama** Gezinti bölmesinde, sanal makine ve ağ arabirimi seçin, kaynak ve hedef IP doldurun ve tıklatın **sonraki atlama** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6f585-123">Click **Next hop** in the navigation pane, select the virtual machine and network interface, fill out the source and destination IP, and click the **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="6f585-124">Sonraki atlama VM kaynak çalıştırmak için ayrılır gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6f585-124">Next hop requires that the VM resource is allocated to run.</span></span>

![sonraki atlama genel bakış][1]

### <a name="step-3"></a><span data-ttu-id="6f585-126">3. Adım</span><span class="sxs-lookup"><span data-stu-id="6f585-126">Step 3</span></span>

<span data-ttu-id="6f585-127">Görev tamamlandığında, sonuçları sağlanır.</span><span class="sxs-lookup"><span data-stu-id="6f585-127">Once the task is complete, the results are provided.</span></span> <span data-ttu-id="6f585-128">IP adresi ve sonraki atlama olan aygıt türü görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6f585-128">The IP address and type of device the next hop is, is displayed.</span></span> <span data-ttu-id="6f585-129">Aşağıdaki tabloda kullanılabilir döndürülen değer portalda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6f585-129">The following table shows the available returned values in the portal.</span></span>

<span data-ttu-id="6f585-130">**Sonraki atlama türü**</span><span class="sxs-lookup"><span data-stu-id="6f585-130">**Next Hop Type**</span></span>

* <span data-ttu-id="6f585-131">Internet</span><span class="sxs-lookup"><span data-stu-id="6f585-131">Internet</span></span>
* <span data-ttu-id="6f585-132">Değerinin VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="6f585-132">VirtualAppliance</span></span>
* <span data-ttu-id="6f585-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="6f585-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="6f585-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="6f585-134">VnetLocal</span></span>
* <span data-ttu-id="6f585-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="6f585-135">HyperNetGateway</span></span>
* <span data-ttu-id="6f585-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="6f585-136">VnetPeering</span></span>
* <span data-ttu-id="6f585-137">None</span><span class="sxs-lookup"><span data-stu-id="6f585-137">None</span></span>

<span data-ttu-id="6f585-138">Özel bir rota bu trafiği yönlendirmek için kullanıldıysa, kullanıcı tanımlı yönlendirme (UDR) de sonuçlarıyla gösterilir.</span><span class="sxs-lookup"><span data-stu-id="6f585-138">If a custom route was used to route this traffic, the User-defined route (UDR) is shown as well with the results.</span></span>

![sonraki atlama sonuçları Al][2]

## <a name="next-steps"></a><span data-ttu-id="6f585-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6f585-140">Next steps</span></span>

<span data-ttu-id="6f585-141">Ağ güvenlik grubu ayarlarınızı program aracılığıyla ziyaret ederek gözden öğrenin [NSG Denetim Ağ İzleyicisi](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="6f585-141">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














