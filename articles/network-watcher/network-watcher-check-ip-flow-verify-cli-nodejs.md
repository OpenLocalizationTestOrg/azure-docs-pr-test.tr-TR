---
title: "Azure Ağ İzleyicisi IP akış doğrulama - Azure CLI ile aaaVerify trafiği | Microsoft Docs"
description: "Bu makalede nasıl bir sanal makineden trafiği tooor izin verilen ya da Azure CLI kullanarak reddedildi toocheck"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c6becc5c142837b04d15490b2b3bd11124434570
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="7e137-103">Trafik izin veya tooor VM IP akış doğrulayın ile Azure Ağ İzleyicisi bileşeni reddedildi olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="7e137-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="7e137-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="7e137-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="7e137-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e137-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="7e137-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7e137-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="7e137-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7e137-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="7e137-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="7e137-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="7e137-109">IP akış doğrulayın Ağ İzleyicisinin, trafiği bir sanal makineden tooor izin verilip verilmediğini tooverify sağlayan bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="7e137-109">IP Flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="7e137-110">Bu senaryo kullanışlı tooget bir sanal makine tooan dış kaynak veya arka uç iletişim kurabilirsiniz, geçerli bir durumda olur.</span><span class="sxs-lookup"><span data-stu-id="7e137-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="7e137-111">IP akış doğrulayın olabilir kullanılan tooverify ağ güvenlik grubu (NSG) kurallarınızı düzgün şekilde yapılandırılırsa ve NSG kuralları tarafından engellenen akışları sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="7e137-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="7e137-112">IP kullanan başka bir nedeni akış durumda engellenen istediğiniz tooensure trafiği engellenmiş düzgün şekilde NSG hello tarafından doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7e137-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

<span data-ttu-id="7e137-113">Bu makalede, platformlar arası Azure CLI 1.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.</span><span class="sxs-lookup"><span data-stu-id="7e137-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7e137-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="7e137-114">Before you begin</span></span>

<span data-ttu-id="7e137-115">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturmak](network-watcher-create.md) toocreate bir Ağ İzleyicisi'ni veya mevcut bir Ağ İzleyicisi örneği.</span><span class="sxs-lookup"><span data-stu-id="7e137-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="7e137-116">Merhaba senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılan toobe var olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="7e137-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="7e137-117">Senaryo</span><span class="sxs-lookup"><span data-stu-id="7e137-117">Scenario</span></span>

<span data-ttu-id="7e137-118">Bu senaryo bir sanal makine tooa bilinen geçebildiğinden akış IP doğrulayın tooverify kullanıyorsa Bing IP adresi.</span><span class="sxs-lookup"><span data-stu-id="7e137-118">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="7e137-119">Merhaba trafik reddedilirse, bu trafiğin reddediyor hello güvenlik kuralı döndürür.</span><span class="sxs-lookup"><span data-stu-id="7e137-119">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="7e137-120">IP akış doğrulayın, hakkında daha fazla toolearn ziyaret [IP akış doğrulayın genel bakış](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7e137-120">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>


## <a name="get-a-vm"></a><span data-ttu-id="7e137-121">VM Al</span><span class="sxs-lookup"><span data-stu-id="7e137-121">Get a VM</span></span>

<span data-ttu-id="7e137-122">IP akış testleri trafiği tooor bir sanal makine tooor uzaktan bir hedef üzerinde bir IP adresinden doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7e137-122">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="7e137-123">Bir sanal makine kimliği hello cmdlet'i için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7e137-123">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="7e137-124">Merhaba sanal makine toouse hello Kimliğini biliyorsanız, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e137-124">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-hello-nics"></a><span data-ttu-id="7e137-125">Merhaba NIC alma</span><span class="sxs-lookup"><span data-stu-id="7e137-125">Get hello NICS</span></span>

<span data-ttu-id="7e137-126">Bu örnekte, bir sanal makinede hello NIC'ler alıyoruz hello sanal makinede bir NIC Hello IP adresi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7e137-126">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="7e137-127">Başlangıç IP adresini biliyorsanız tootest istediğiniz hello sanal makinede, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e137-127">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="7e137-128">Çalışma IP akış doğrulayın</span><span class="sxs-lookup"><span data-stu-id="7e137-128">Run IP flow verify</span></span>

<span data-ttu-id="7e137-129">Toorun hello cmdlet hello bilgi sahibiz, biz hello çalıştırmak `network watcher ip-flow-verify` cmdlet tootest hello trafiği.</span><span class="sxs-lookup"><span data-stu-id="7e137-129">Now that we have hello information needed toorun hello cmdlet, we run hello `network watcher ip-flow-verify` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="7e137-130">Bu örnekte, hello ilk IP adresi hello ilk NIC üzerinde kullanıyoruz</span><span class="sxs-lookup"><span data-stu-id="7e137-130">In this example, we are using hello first IP address on hello first NIC.</span></span>

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> <span data-ttu-id="7e137-131">IP akış doğrulayın gerektirir hello VM kaynak toorun ayrılır.</span><span class="sxs-lookup"><span data-stu-id="7e137-131">IP Flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="7e137-132">Sonuçları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="7e137-132">Review Results</span></span>

<span data-ttu-id="7e137-133">Çalıştırdıktan sonra `network watcher ip-flow-verify` hello sonuçlarının döndürüldüğü, hello aşağıdaki adım önceki hello döndürülen hello sonuçları bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="7e137-133">After running `network watcher ip-flow-verify` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a><span data-ttu-id="7e137-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7e137-134">Next steps</span></span>

<span data-ttu-id="7e137-135">Trafik engelleniyor ve olmamalıdır, bkz: [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tanımlanan hello ağ güvenlik grubu ve güvenlik kuralları aşağı tootrack.</span><span class="sxs-lookup"><span data-stu-id="7e137-135">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<span data-ttu-id="7e137-136">Tooaudit NSG ayarlarınızı ziyaret ederek bilgi [denetim ağ güvenlik grupları (NSG) Ağ İzleyicisi ile](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7e137-136">Learn tooaudit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
