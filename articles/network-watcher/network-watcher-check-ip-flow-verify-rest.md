---
title: "Azure Ağ İzleyicisi IP akış ile aaaVerify trafiği doğrulama - REST | Microsoft Docs"
description: "Bu makalede nasıl bir sanal makineden trafiği tooor izin verilen veya reddedilen varsa toocheck"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 956db0d326db597c6c402a9e8d4a5522c47c02d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="6eb1f-103">Trafik izin verilen ya da IP akışla reddedildi onay Azure Ağ İzleyicisi'nin bir bileşeni doğrulayın</span><span class="sxs-lookup"><span data-stu-id="6eb1f-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="6eb1f-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="6eb1f-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="6eb1f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6eb1f-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="6eb1f-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6eb1f-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="6eb1f-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6eb1f-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="6eb1f-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="6eb1f-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="6eb1f-109">IP akış doğrulayın Ağ İzleyicisinin, trafiği bir sanal makineden tooor izin verilip verilmediğini tooverify sağlayan bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="6eb1f-110">Merhaba doğrulama gelen veya giden trafiği için çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="6eb1f-111">Bu senaryo kullanışlı tooget bir sanal makine tooan dış kaynak veya arka uç iletişim kurabilirsiniz, geçerli bir durumda olur.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="6eb1f-112">IP akış doğrulayın olabilir kullanılan tooverify ağ güvenlik grubu (NSG) kurallarınızı düzgün şekilde yapılandırılırsa ve NSG kuralları tarafından engellenen akışları sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="6eb1f-113">IP kullanan başka bir nedeni akış durumda engellenen istediğiniz tooensure trafiği engellenmiş düzgün şekilde NSG hello tarafından doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6eb1f-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="6eb1f-114">Before you begin</span></span>

<span data-ttu-id="6eb1f-115">ARMclient PowerShell kullanarak kullanılan toocall hello REST API ' dir.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-115">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="6eb1f-116">ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="6eb1f-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="6eb1f-117">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-117">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="6eb1f-118">Senaryo</span><span class="sxs-lookup"><span data-stu-id="6eb1f-118">Scenario</span></span>

<span data-ttu-id="6eb1f-119">Bu senaryo IP akış doğrula tooverify kullanıyorsa bir sanal makine tooanother makine 443 numaralı bağlantı noktası iletişim kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-119">This scenario uses IP flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="6eb1f-120">Merhaba trafik reddedilirse, bu trafiğin reddediyor hello güvenlik kuralı döndürür.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-120">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="6eb1f-121">IP akış doğrulayın, hakkında daha fazla toolearn ziyaret [IP akış doğrulayın genel bakış](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="6eb1f-121">toolearn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span></span>

<span data-ttu-id="6eb1f-122">Bu senaryoda:</span><span class="sxs-lookup"><span data-stu-id="6eb1f-122">In this scenario, you:</span></span>

* <span data-ttu-id="6eb1f-123">Bir sanal makine alma</span><span class="sxs-lookup"><span data-stu-id="6eb1f-123">Retrieve a virtual machine</span></span>
* <span data-ttu-id="6eb1f-124">Çağrı IP akış doğrulayın</span><span class="sxs-lookup"><span data-stu-id="6eb1f-124">Call IP flow verify</span></span>
* <span data-ttu-id="6eb1f-125">Sonuçları doğrulayın</span><span class="sxs-lookup"><span data-stu-id="6eb1f-125">Verify results</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="6eb1f-126">Oturum ARMClient oturum</span><span class="sxs-lookup"><span data-stu-id="6eb1f-126">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="6eb1f-127">Bir sanal makine alma</span><span class="sxs-lookup"><span data-stu-id="6eb1f-127">Retrieve a virtual machine</span></span>

<span data-ttu-id="6eb1f-128">Komut dosyası tooreturn aşağıdaki hello bir sanal makine çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-128">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="6eb1f-129">Merhaba aşağıdaki kodu değerleri hello değişkenleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="6eb1f-129">hello following code needs values for hello variables:</span></span>

* <span data-ttu-id="6eb1f-130">**Subscriptionıd** -abonelik kimliği toouse hello.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-130">**subscriptionId** - hello subscription Id toouse.</span></span>
* <span data-ttu-id="6eb1f-131">**resourceGroupName** - hello sanal makine içeren bir kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-131">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="6eb1f-132">Merhaba gerekli bilgileri hello hello türü altında kimliğidir `Microsoft.Compute/virtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-132">hello information that is needed is hello id under hello type `Microsoft.Compute/virtualMachines`.</span></span> <span data-ttu-id="6eb1f-133">Merhaba sonuçları benzer toohello kodu örneği aşağıdaki gibi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="6eb1f-133">hello results should be similar toohello following code sample:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a><span data-ttu-id="6eb1f-134">Çağrı IP akış doğrulayın</span><span class="sxs-lookup"><span data-stu-id="6eb1f-134">Call IP flow Verify</span></span>

<span data-ttu-id="6eb1f-135">Merhaba aşağıdaki örnek belirtilen bir sanal makine için bir istek tooverify hello trafiği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-135">hello following example creates a request tooverify hello traffic for a specified virtual machine.</span></span> <span data-ttu-id="6eb1f-136">Merhaba trafiğine izin verilip verilmediğini veya hello trafiği reddedilirse Hello yanıtı döndürür.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-136">hello response returns if hello traffic is allowed or if hello traffic is denied.</span></span> <span data-ttu-id="6eb1f-137">Trafik reddedilirse Ayrıca hangi kural bloklarını trafiği hello döndürür.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-137">If traffic is denied it also returns what rule blocks hello traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="6eb1f-138">IP akış doğrulayın gerektirir hello VM kaynak ayrılır.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-138">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="6eb1f-139">Merhaba betik hello kaynak kimliği, bir sanal makinenin ve hello sanal makinedeki ağ arabirim kartı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-139">hello script requires hello resource Id of a virtual machine and of a network interface card on hello virtual machine.</span></span> <span data-ttu-id="6eb1f-140">Bu değerleri çıktı önceki hello tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-140">These values are provided by hello preceding output.</span></span>

> [!Important]
> <span data-ttu-id="6eb1f-141">İçin tüm Ağ İzleyicisi REST çağrılarını hello hello tanılama eylemleri gerçekleştirdiğiniz hello kaynakları değil hello Ağ İzleyicisi örneği içeren bir URI'dir hello isteğindeki kaynak grubu adı hello.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-141">For all Network Watcher REST calls hello resource group name in hello request URI is hello one that contains hello Network Watcher instance, not hello resources you are performing hello diagnostic actions on.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-hello-results"></a><span data-ttu-id="6eb1f-142">Merhaba sonuçlarını anlama</span><span class="sxs-lookup"><span data-stu-id="6eb1f-142">Understanding hello results</span></span>

<span data-ttu-id="6eb1f-143">geri alma hello yanıt hello trafiğine izin verilen veya reddedilen söyler.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-143">hello response you get back tells you whether hello traffic is allowed or denied.</span></span> <span data-ttu-id="6eb1f-144">Merhaba yanıt bir hello örnekler aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="6eb1f-144">hello response looks like one of hello following examples:</span></span>

<span data-ttu-id="6eb1f-145">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="6eb1f-145">**Allowed**</span></span>

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

<span data-ttu-id="6eb1f-146">**Engellendi**</span><span class="sxs-lookup"><span data-stu-id="6eb1f-146">**Denied**</span></span>

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a><span data-ttu-id="6eb1f-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6eb1f-147">Next steps</span></span>

<span data-ttu-id="6eb1f-148">Trafik engelleniyor ve olmamalıdır, bkz: [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn ağ güvenlik grupları hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="6eb1f-148">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn more about Network Security Groups.</span></span>












