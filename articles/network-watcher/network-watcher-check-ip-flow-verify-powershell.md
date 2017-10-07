---
title: "Azure Ağ İzleyicisi IP akış ile aaaverify trafiği doğrulama - PowerShell | Microsoft Docs"
description: "Bu makalede nasıl bir sanal makineden trafiği tooor izin verilen veya PowerShell kullanarak reddedildi toocheck"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e1dad757-8c5d-467f-812e-7cc751143207
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 924da1de1bd554e15816886f8e51d7f170f0e7ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="b88c7-103">Trafik izin verilen ya da bir VM'den IP akış ile tooor reddedildi onay Azure Ağ İzleyicisi'nin bir bileşeni doğrulayın</span><span class="sxs-lookup"><span data-stu-id="b88c7-103">Check if traffic is allowed or denied tooor from a VM with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="b88c7-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="b88c7-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="b88c7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b88c7-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="b88c7-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b88c7-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="b88c7-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b88c7-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="b88c7-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="b88c7-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="b88c7-109">IP akış doğrulayın Ağ İzleyicisinin, trafiği bir sanal makineden tooor izin verilip verilmediğini tooverify sağlayan bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="b88c7-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="b88c7-110">Bu senaryo kullanışlı tooget bir sanal makine tooan dış kaynak veya arka uç iletişim kurabilirsiniz, geçerli bir durumda olur.</span><span class="sxs-lookup"><span data-stu-id="b88c7-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="b88c7-111">IP akış doğrulayın olabilir kullanılan tooverify ağ güvenlik grubu (NSG) kurallarınızı düzgün şekilde yapılandırılırsa ve NSG kuralları tarafından engellenen akışları sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="b88c7-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="b88c7-112">IP kullanan başka bir nedeni akış durumda engellenen istediğiniz tooensure trafiği engellenmiş düzgün şekilde NSG hello tarafından doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b88c7-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b88c7-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="b88c7-113">Before you begin</span></span>

<span data-ttu-id="b88c7-114">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturmak](network-watcher-create.md) toocreate bir Ağ İzleyicisi'ni veya mevcut bir Ağ İzleyicisi örneği.</span><span class="sxs-lookup"><span data-stu-id="b88c7-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="b88c7-115">Merhaba senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılan toobe var olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="b88c7-115">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="b88c7-116">Senaryo</span><span class="sxs-lookup"><span data-stu-id="b88c7-116">Scenario</span></span>

<span data-ttu-id="b88c7-117">Bu senaryo kullanan IP akışını denetlemek için bir sanal makine tooa bilinen geçebildiğinden if tooverify Bing IP adresi.</span><span class="sxs-lookup"><span data-stu-id="b88c7-117">This scenario uses IP flow verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="b88c7-118">Merhaba trafik reddedilirse, bu trafiğin reddediyor hello güvenlik kuralı döndürür.</span><span class="sxs-lookup"><span data-stu-id="b88c7-118">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="b88c7-119">IP akışı hakkında daha fazla doğrulama, toolearn ziyaret [IP akış doğrulayın genel bakış](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b88c7-119">toolearn more about IP flow verify, visit [IP flow verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="b88c7-120">Ağ İzleyicisi alma</span><span class="sxs-lookup"><span data-stu-id="b88c7-120">Retrieve Network Watcher</span></span>

<span data-ttu-id="b88c7-121">Merhaba ilk adımı tooretrieve hello Ağ İzleyicisi örneğidir.</span><span class="sxs-lookup"><span data-stu-id="b88c7-121">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="b88c7-122">Merhaba `$networkWatcher` değişkeni toohello IP geçirilen akış cmdlet doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b88c7-122">hello `$networkWatcher` variable is passed toohello IP flow verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="b88c7-123">VM Al</span><span class="sxs-lookup"><span data-stu-id="b88c7-123">Get a VM</span></span>

<span data-ttu-id="b88c7-124">IP akış testleri trafiği tooor bir sanal makine tooor uzaktan bir hedef üzerinde bir IP adresinden doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b88c7-124">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="b88c7-125">Bir sanal makine kimliği hello cmdlet'i için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b88c7-125">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="b88c7-126">Merhaba sanal makine toouse hello Kimliğini biliyorsanız, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b88c7-126">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-hello-nics"></a><span data-ttu-id="b88c7-127">Merhaba NIC alma</span><span class="sxs-lookup"><span data-stu-id="b88c7-127">Get hello NICS</span></span>

<span data-ttu-id="b88c7-128">Bu örnekte, bir sanal makinede hello NIC'ler alıyoruz hello sanal makinede bir NIC Hello IP adresi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b88c7-128">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="b88c7-129">Başlangıç IP adresini biliyorsanız tootest istediğiniz hello sanal makinede, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b88c7-129">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="b88c7-130">Çalışma IP akış doğrulayın</span><span class="sxs-lookup"><span data-stu-id="b88c7-130">Run IP flow verify</span></span>

<span data-ttu-id="b88c7-131">Toorun hello cmdlet hello bilgi sahibiz, biz hello çalıştırmak `Test-AzureRmNetworkWatcherIPFlow` cmdlet tootest hello trafiği.</span><span class="sxs-lookup"><span data-stu-id="b88c7-131">Now that we have hello information needed toorun hello cmdlet, we run hello `Test-AzureRmNetworkWatcherIPFlow` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="b88c7-132">Bu örnekte, hello ilk IP adresi hello ilk NIC üzerinde kullanıyoruz</span><span class="sxs-lookup"><span data-stu-id="b88c7-132">In this example, we are using hello first IP address on hello first NIC.</span></span>

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> <span data-ttu-id="b88c7-133">IP akış doğrulayın gerektirir hello VM kaynak toorun ayrılır.</span><span class="sxs-lookup"><span data-stu-id="b88c7-133">IP flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="b88c7-134">Sonuçları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="b88c7-134">Review Results</span></span>

<span data-ttu-id="b88c7-135">Çalıştırdıktan sonra `Test-AzureRmNetworkWatcherIPFlow` hello sonuçlarının döndürüldüğü, hello aşağıdaki adım önceki hello döndürülen hello sonuçları bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="b88c7-135">After running `Test-AzureRmNetworkWatcherIPFlow` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a><span data-ttu-id="b88c7-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b88c7-136">Next steps</span></span>

<span data-ttu-id="b88c7-137">Trafik engelleniyor ve olmamalıdır, bkz: [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tanımlanan hello ağ güvenlik grubu ve güvenlik kuralları aşağı tootrack.</span><span class="sxs-lookup"><span data-stu-id="b88c7-137">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













