---
title: "Trafik doğrulayın ile Azure Ağ İzleyicisi IP akışını doğrulamak - REST | Microsoft Docs"
description: "Bu makalede, trafik için veya bir sanal makineden izin verilen veya reddedilen denetlemek açıklar"
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
ms.openlocfilehash: 6d3ce00a7d4f9c0cd57fa8815625a1065b03b5b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="3ed6d-103">Trafik izin verilen ya da IP akışla reddedildi onay Azure Ağ İzleyicisi'nin bir bileşeni doğrulayın</span><span class="sxs-lookup"><span data-stu-id="3ed6d-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="3ed6d-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="3ed6d-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="3ed6d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ed6d-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="3ed6d-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3ed6d-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="3ed6d-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3ed6d-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="3ed6d-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="3ed6d-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="3ed6d-109">IP akış doğrulayın özelliğidir Ağ İzleyicisi, trafik için veya bir sanal makineden izin verilip verilmediğini doğrulamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="3ed6d-110">Doğrulama gelen veya giden trafiği için çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-110">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="3ed6d-111">Bu senaryo, bir sanal makine için bir dış kaynağa veya arka uç iletişim kurabilirsiniz geçerli durumunu almak yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-111">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="3ed6d-112">IP akış doğrulayın, ağ güvenlik grubu (NSG) kurallarınızı düzgün şekilde yapılandırıldığından ve NSG kuralları tarafından engellenen akışları sorun giderme doğrulamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-112">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="3ed6d-113">IP kullanan başka bir nedeni akış durumda engellenen istediğiniz trafiği engellenmiş düzgün tarafından NSG emin olmak için doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-113">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3ed6d-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="3ed6d-114">Before you begin</span></span>

<span data-ttu-id="3ed6d-115">ARMclient PowerShell kullanarak REST API'sini çağırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-115">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="3ed6d-116">ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="3ed6d-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="3ed6d-117">Bu senaryo zaten izlediğiniz adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) bir Ağ İzleyicisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-117">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="3ed6d-118">Senaryo</span><span class="sxs-lookup"><span data-stu-id="3ed6d-118">Scenario</span></span>

<span data-ttu-id="3ed6d-119">Bu senaryo, bir sanal makine bağlantı noktası 443 üzerinden başka bir makineye konuşun olmadığını doğrulamak için IP akış doğrulama kullanır.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-119">This scenario uses IP flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="3ed6d-120">Trafiği reddedilirse, bu trafiği engelleyen güvenlik kuralı döndürür.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-120">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="3ed6d-121">IP akışı doğrulama hakkında daha fazla bilgi için ziyaret [IP akış doğrulayın genel bakış](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3ed6d-121">To learn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span></span>

<span data-ttu-id="3ed6d-122">Bu senaryoda:</span><span class="sxs-lookup"><span data-stu-id="3ed6d-122">In this scenario, you:</span></span>

* <span data-ttu-id="3ed6d-123">Bir sanal makine alma</span><span class="sxs-lookup"><span data-stu-id="3ed6d-123">Retrieve a virtual machine</span></span>
* <span data-ttu-id="3ed6d-124">Çağrı IP akış doğrulayın</span><span class="sxs-lookup"><span data-stu-id="3ed6d-124">Call IP flow verify</span></span>
* <span data-ttu-id="3ed6d-125">Sonuçları doğrulayın</span><span class="sxs-lookup"><span data-stu-id="3ed6d-125">Verify results</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="3ed6d-126">Oturum ARMClient oturum</span><span class="sxs-lookup"><span data-stu-id="3ed6d-126">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="3ed6d-127">Bir sanal makine alma</span><span class="sxs-lookup"><span data-stu-id="3ed6d-127">Retrieve a virtual machine</span></span>

<span data-ttu-id="3ed6d-128">Bir sanal makine döndürmek için aşağıdaki betiği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-128">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="3ed6d-129">Aşağıdaki kod değerleri değişkenleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="3ed6d-129">The following code needs values for the variables:</span></span>

* <span data-ttu-id="3ed6d-130">**Subscriptionıd** -abonelik kimliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-130">**subscriptionId** - The subscription Id to use.</span></span>
* <span data-ttu-id="3ed6d-131">**resourceGroupName** -sanal makine içeren bir kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-131">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="3ed6d-132">Gerekli bilgileri kimliği türü'nün altında: `Microsoft.Compute/virtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-132">The information that is needed is the id under the type `Microsoft.Compute/virtualMachines`.</span></span> <span data-ttu-id="3ed6d-133">Sonuçları aşağıdaki kod örneği benzer olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="3ed6d-133">The results should be similar to the following code sample:</span></span>

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

## <a name="call-ip-flow-verify"></a><span data-ttu-id="3ed6d-134">Çağrı IP akış doğrulayın</span><span class="sxs-lookup"><span data-stu-id="3ed6d-134">Call IP flow Verify</span></span>

<span data-ttu-id="3ed6d-135">Aşağıdaki örnek belirtilen bir sanal makine için trafiği doğrulamak için bir istek oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-135">The following example creates a request to verify the traffic for a specified virtual machine.</span></span> <span data-ttu-id="3ed6d-136">Yanıt trafiğe izin verilip verilmediğini veya trafiği reddedilirse döndürür.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-136">The response returns if the traffic is allowed or if the traffic is denied.</span></span> <span data-ttu-id="3ed6d-137">Ayrıca, trafiği reddedilirse hangi kural trafiği engeller. döndürür.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-137">If traffic is denied it also returns what rule blocks the traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="3ed6d-138">IP akış doğrulayın gerektirir VM kaynak ayrılır.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-138">IP flow verify requires that the VM resource is allocated.</span></span>

<span data-ttu-id="3ed6d-139">Komut dosyası kaynak kimliği bir sanal makine ve sanal makinedeki ağ arabirim kartı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-139">The script requires the resource Id of a virtual machine and of a network interface card on the virtual machine.</span></span> <span data-ttu-id="3ed6d-140">Bu değerler önceki çıktı tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-140">These values are provided by the preceding output.</span></span>

> [!Important]
> <span data-ttu-id="3ed6d-141">Tüm Ağ İzleyicisi REST için istek URI'SİNDEKİ kaynak grubu adı çağrıdır, Ağ İzleyicisi örneği içeren bir tanılama eylemleri gerçekleştirdiğiniz kaynakları değil.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-141">For all Network Watcher REST calls the resource group name in the request URI is the one that contains the Network Watcher instance, not the resources you are performing the diagnostic actions on.</span></span>

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

## <a name="understanding-the-results"></a><span data-ttu-id="3ed6d-142">Sonuçları anlama</span><span class="sxs-lookup"><span data-stu-id="3ed6d-142">Understanding the results</span></span>

<span data-ttu-id="3ed6d-143">Geri alma yanıt trafiğe izin verilen veya reddedilen bildirir.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-143">The response you get back tells you whether the traffic is allowed or denied.</span></span> <span data-ttu-id="3ed6d-144">Yanıt aşağıdaki örneklerde biri gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="3ed6d-144">The response looks like one of the following examples:</span></span>

<span data-ttu-id="3ed6d-145">**İzin verilen**</span><span class="sxs-lookup"><span data-stu-id="3ed6d-145">**Allowed**</span></span>

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

<span data-ttu-id="3ed6d-146">**Engellendi**</span><span class="sxs-lookup"><span data-stu-id="3ed6d-146">**Denied**</span></span>

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a><span data-ttu-id="3ed6d-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3ed6d-147">Next steps</span></span>

<span data-ttu-id="3ed6d-148">Trafik engelleniyor ve olmamalıdır, bkz: [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) ağ güvenlik grupları hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="3ed6d-148">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to learn more about Network Security Groups.</span></span>












