---
title: "Azure Ağ İzleyicisi sonraki atlama - Azure portal ile aaaFind sonraki atlama | Microsoft Docs"
description: "Bu makalede nasıl hangi hello sonraki atlama türü olan ve sonraki atlama kullanarak IP adresi hello Azure portalında bulabilirsiniz açıklayın"
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
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="e4143-103">Hangi hello sonraki atlama türü hello sonraki atlama yetenek hello portalı kullanarak Azure Ağ İzleyicisi içinde kullandığını bulmak</span><span class="sxs-lookup"><span data-stu-id="e4143-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="e4143-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="e4143-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="e4143-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4143-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="e4143-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e4143-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="e4143-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e4143-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="e4143-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="e4143-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="e4143-109">Sonraki atlama bir özelliği olan Ağ İzleyicisi'hello yeteneği sağlar, hello sonraki atlama türü ve belirtilen bir sanal makineye dayalı IP adresi al ' dir.</span><span class="sxs-lookup"><span data-stu-id="e4143-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="e4143-110">Bu özellik, bir sanal makine trafiğe bir ağ geçidi, internet veya sanal ağlar tooget tooits hedef geçiyorsa belirlemede yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="e4143-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e4143-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="e4143-111">Before you begin</span></span>

<span data-ttu-id="e4143-112">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="e4143-112">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="e4143-113">Merhaba senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılan toobe var olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="e4143-113">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="e4143-114">Senaryo</span><span class="sxs-lookup"><span data-stu-id="e4143-114">Scenario</span></span>

<span data-ttu-id="e4143-115">Bu makalede ele alınan hello senaryo, bir kaynak için sonraki atlama toofind hello sonraki atlama türü ve IP adresini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e4143-115">hello scenario covered in this article uses Next hop toofind out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="e4143-116">Sonraki atlama, hakkında daha fazla toolearn ziyaret [sonraki atlama genel bakış](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e4143-116">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="e4143-117">Bu senaryoda, şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="e4143-117">In this scenario, you will:</span></span>

* <span data-ttu-id="e4143-118">Bir sanal makineden Hello sonraki atlama alın.</span><span class="sxs-lookup"><span data-stu-id="e4143-118">Retrieve hello next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="e4143-119">Sonraki atlama Al</span><span class="sxs-lookup"><span data-stu-id="e4143-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="e4143-120">1. Adım</span><span class="sxs-lookup"><span data-stu-id="e4143-120">Step 1</span></span>

<span data-ttu-id="e4143-121">Tooyour Ağ İzleyicisi kaynak hello Azure portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="e4143-121">Navigate tooyour Network Watcher resource in hello Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="e4143-122">2. Adım</span><span class="sxs-lookup"><span data-stu-id="e4143-122">Step 2</span></span>

<span data-ttu-id="e4143-123">Tıklatın **sonraki atlama** hello Gezinti bölmesinde, select hello sanal makine ve ağ arabirimi, hello kaynak ve hedef IP doldurun ve hello tıklatın **sonraki atlama** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e4143-123">Click **Next hop** in hello navigation pane, select hello virtual machine and network interface, fill out hello source and destination IP, and click hello **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="e4143-124">Sonraki atlama hello VM kaynak toorun ayrılır gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e4143-124">Next hop requires that hello VM resource is allocated toorun.</span></span>

![sonraki atlama genel bakış][1]

### <a name="step-3"></a><span data-ttu-id="e4143-126">3. Adım</span><span class="sxs-lookup"><span data-stu-id="e4143-126">Step 3</span></span>

<span data-ttu-id="e4143-127">Merhaba görev tamamlandıktan sonra hello sonuçları sağlanır.</span><span class="sxs-lookup"><span data-stu-id="e4143-127">Once hello task is complete, hello results are provided.</span></span> <span data-ttu-id="e4143-128">IP adresi ve cihaz hello sonraki atlama türü hello ise, görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e4143-128">hello IP address and type of device hello next hop is, is displayed.</span></span> <span data-ttu-id="e4143-129">Merhaba aşağıdaki tabloda hello kullanılabilir döndürülen değer hello portalda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e4143-129">hello following table shows hello available returned values in hello portal.</span></span>

<span data-ttu-id="e4143-130">**Sonraki atlama türü**</span><span class="sxs-lookup"><span data-stu-id="e4143-130">**Next Hop Type**</span></span>

* <span data-ttu-id="e4143-131">Internet</span><span class="sxs-lookup"><span data-stu-id="e4143-131">Internet</span></span>
* <span data-ttu-id="e4143-132">Değerinin VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="e4143-132">VirtualAppliance</span></span>
* <span data-ttu-id="e4143-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="e4143-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="e4143-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="e4143-134">VnetLocal</span></span>
* <span data-ttu-id="e4143-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="e4143-135">HyperNetGateway</span></span>
* <span data-ttu-id="e4143-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="e4143-136">VnetPeering</span></span>
* <span data-ttu-id="e4143-137">None</span><span class="sxs-lookup"><span data-stu-id="e4143-137">None</span></span>

<span data-ttu-id="e4143-138">Özel rota kullanılan tooroute varsa bu trafiği hello kullanıcı tanımlı yönlendirme (UDR) de hello sonuçlarıyla gösterilir.</span><span class="sxs-lookup"><span data-stu-id="e4143-138">If a custom route was used tooroute this traffic, hello User-defined route (UDR) is shown as well with hello results.</span></span>

![sonraki atlama sonuçları Al][2]

## <a name="next-steps"></a><span data-ttu-id="e4143-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e4143-140">Next steps</span></span>

<span data-ttu-id="e4143-141">Bilgi nasıl tooreview ağ güvenlik grubu ayarlarınızı programlı olarak şu adresi ziyaret ederek [NSG Denetim Ağ İzleyicisi](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="e4143-141">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














