---
title: "Azure Ağ İzleyicisi IP akış ile aaaVerify trafiği doğrulama - Azure portalı | Microsoft Docs"
description: "Bu makalede nasıl bir sanal makineden trafiği tooor izin verilen veya reddedilen varsa toocheck"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="f92ba-103">Trafik izin veya tooor VM IP akış doğrulayın ile Azure Ağ İzleyicisi bileşeni reddedildi olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="f92ba-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f92ba-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="f92ba-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="f92ba-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f92ba-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="f92ba-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f92ba-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="f92ba-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f92ba-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="f92ba-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="f92ba-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="f92ba-109">IP akış doğrulayın Ağ İzleyicisinin, trafiği bir sanal makineden tooor izin verilip verilmediğini tooverify sağlayan bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="f92ba-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="f92ba-110">Merhaba doğrulama gelen veya giden trafiği için çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="f92ba-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="f92ba-111">Bu senaryo kullanışlı tooget bir sanal makine tooan dış kaynak ya da başka bir kaynak iletişim kurabilirsiniz, geçerli bir durumda olur.</span><span class="sxs-lookup"><span data-stu-id="f92ba-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or another resource.</span></span> <span data-ttu-id="f92ba-112">IP akış doğrulayın olabilir kullanılan tooverify ağ güvenlik grubu (NSG) kurallarınızı düzgün şekilde yapılandırılırsa ve NSG kuralları tarafından engellenen akışları sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="f92ba-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="f92ba-113">IP kullanan başka bir nedeni akış durumda engellenen istediğiniz tooensure trafiği engellenmiş düzgün şekilde NSG hello tarafından doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f92ba-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f92ba-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="f92ba-114">Before you begin</span></span>

<span data-ttu-id="f92ba-115">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturmak](network-watcher-create.md) toocreate bir Ağ İzleyicisi'ni veya mevcut bir Ağ İzleyicisi örneği.</span><span class="sxs-lookup"><span data-stu-id="f92ba-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="f92ba-116">Merhaba senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılan toobe var olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="f92ba-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="f92ba-117">Senaryo</span><span class="sxs-lookup"><span data-stu-id="f92ba-117">Scenario</span></span>

<span data-ttu-id="f92ba-118">Bu senaryo akış IP doğrulayın tooverify kullanıyorsa bir sanal makine tooanother makine 443 numaralı bağlantı noktası iletişim kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f92ba-118">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="f92ba-119">Merhaba trafik reddedilirse, bu trafiğin reddediyor hello güvenlik kuralı döndürür.</span><span class="sxs-lookup"><span data-stu-id="f92ba-119">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="f92ba-120">IP akış doğrulayın, hakkında daha fazla toolearn ziyaret [IP akış doğrulayın genel bakış](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f92ba-120">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="f92ba-121">Çalışma IP akış doğrulayın</span><span class="sxs-lookup"><span data-stu-id="f92ba-121">Run IP flow verify</span></span>

<span data-ttu-id="f92ba-122">Ağ İzleyicisi tooyour gidin ve tıklayın **IP akış doğrulayın**.</span><span class="sxs-lookup"><span data-stu-id="f92ba-122">Navigate tooyour Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="f92ba-123">Tooverify trafiğinden istediğiniz Hello sanal makine ve ağ arabirimi seçin.</span><span class="sxs-lookup"><span data-stu-id="f92ba-123">Select hello virtual machine and network interface you want tooverify traffic from.</span></span> <span data-ttu-id="f92ba-124">Ek filtreleme bilgileri girin ve tıklayın **denetleyin**.</span><span class="sxs-lookup"><span data-stu-id="f92ba-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="f92ba-125">Tıkladığınızda **denetleyin**, sağladığınız hello ölçütlere göre hello akışı denetlenir.</span><span class="sxs-lookup"><span data-stu-id="f92ba-125">Once you click **Check**, hello flow based on hello criteria you provided is checked.</span></span> <span data-ttu-id="f92ba-126">Merhaba sonucu olan ya da **izin verilen erişim** veya **erişim reddedildi**.</span><span class="sxs-lookup"><span data-stu-id="f92ba-126">hello result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="f92ba-127">Erişimi reddedilirse, ağ güvenlik grubu (NSG) hello ve trafiği engellemek güvenlik kuralı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f92ba-127">If access is denied, hello Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="f92ba-128">Trafik Hello reddi beklenen davranıştır, hello kuralı başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="f92ba-128">If hello denial of traffic is expected behavior, then hello rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="f92ba-129">IP akış doğrulayın gerektirir hello VM kaynak ayrılır.</span><span class="sxs-lookup"><span data-stu-id="f92ba-129">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="f92ba-130">Görüntü aşağıdaki hello görebileceğiniz gibi hello giden HTTPS trafiğine izin.</span><span class="sxs-lookup"><span data-stu-id="f92ba-130">As you can see from hello following image, hello outbound HTTPS traffic was allowed.</span></span>

![IP akış doğrulayın genel bakış][1]

<span data-ttu-id="f92ba-132">Görüntü aşağıdaki hello görülen trafiği değiştirilir tooinbound ve hello gelen bağlantı noktası değiştirilen too123.</span><span class="sxs-lookup"><span data-stu-id="f92ba-132">As seen in hello following image, traffic is changed tooinbound and hello inbound port changed too123.</span></span> <span data-ttu-id="f92ba-133">Trafik şimdi engellendi, selamlama iletisine "erişim engellendi" Merhaba trafiği reddetmeye hello ağ güvenlik grubu ve güvenlik kuralı ile birlikte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f92ba-133">Traffic is now denied, hello message "Access denied" is provided along with hello network security group and security rule that deny hello traffic.</span></span>

![IP akış sonuçları][2]

## <a name="next-steps"></a><span data-ttu-id="f92ba-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f92ba-135">Next steps</span></span>

<span data-ttu-id="f92ba-136">Trafik engelleniyor ve olmamalıdır, bkz: [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tanımlanan hello ağ güvenlik grubu ve güvenlik kuralları aşağı tootrack.</span><span class="sxs-lookup"><span data-stu-id="f92ba-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













