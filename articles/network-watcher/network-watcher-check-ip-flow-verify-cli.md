---
title: "Trafik Azure Ağ İzleyicisi IP akış ile - Azure CLI doğrulayın | Microsoft Docs"
description: "Bu makalede denetlemek için veya bir sanal makineden trafiğin izin verilen veya Azure CLI kullanarak reddedildi varsa açıklar"
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
ms.openlocfilehash: 0b52257a6c38a4392573672b7190d2269c2f145a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="48056-103">Trafiği olup veya izin verilen IP akış doğrulayın ile bir VM'den/VM'ye Azure Ağ İzleyicisi'nin bir bileşeni reddedildi denetleyin</span><span class="sxs-lookup"><span data-stu-id="48056-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="48056-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="48056-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="48056-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="48056-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="48056-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="48056-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="48056-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="48056-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="48056-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="48056-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="48056-109">IP akış doğrulayın özelliğidir Ağ İzleyicisi, trafik için veya bir sanal makineden izin verilip verilmediğini doğrulamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="48056-109">IP Flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="48056-110">Bu senaryo, bir sanal makine için bir dış kaynağa veya arka uç iletişim kurabilirsiniz geçerli durumunu almak yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="48056-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="48056-111">IP akış doğrulayın, ağ güvenlik grubu (NSG) kurallarınızı düzgün şekilde yapılandırıldığından ve NSG kuralları tarafından engellenen akışları sorun giderme doğrulamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="48056-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="48056-112">IP kullanan başka bir nedeni akış durumda engellenen istediğiniz trafiği engellenmiş düzgün tarafından NSG emin olmak için doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="48056-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

<span data-ttu-id="48056-113">Bu makalede, Windows, Mac ve Linux için kullanılabilir olduğu, kaynak yönetimi için dağıtım modelini, Azure CLI 2.0 bizim nesil CLI kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="48056-113">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="48056-114">Bu makaledeki adımları gerçekleştirmek için gerek [Mac, Linux ve Windows (Azure CLI) için Azure komut satırı arabirimini yükleyin](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="48056-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="48056-115">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="48056-115">Before you begin</span></span>

<span data-ttu-id="48056-116">Bu senaryo zaten izlediğiniz adımlarda varsayar [bir Ağ İzleyicisi oluşturmak](network-watcher-create.md) Ağ İzleyicisi mevcut bir örneği olması veya bir Ağ İzleyicisi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="48056-116">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="48056-117">Senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılacak var olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="48056-117">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="48056-118">Senaryo</span><span class="sxs-lookup"><span data-stu-id="48056-118">Scenario</span></span>

<span data-ttu-id="48056-119">Bu senaryo, bir sanal makine bilinen bir Bing IP adresine iletişim kurabilirsiniz doğrulamak için akış IP doğrulayın kullanır.</span><span class="sxs-lookup"><span data-stu-id="48056-119">This scenario uses IP Flow Verify to verify if a virtual machine can talk to a known Bing IP address.</span></span> <span data-ttu-id="48056-120">Trafiği reddedilirse, bu trafiği engelleyen güvenlik kuralı döndürür.</span><span class="sxs-lookup"><span data-stu-id="48056-120">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="48056-121">Akış IP doğrulama hakkında daha fazla bilgi için [IP akış doğrulayın genel bakış](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="48056-121">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="48056-122">VM Al</span><span class="sxs-lookup"><span data-stu-id="48056-122">Get a VM</span></span>

<span data-ttu-id="48056-123">IP akış testleri trafiği için veya bir IP adresi için bir sanal makinede veya uzaktan bir hedef doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="48056-123">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span></span> <span data-ttu-id="48056-124">Bir sanal makine kimliği cmdlet'i için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="48056-124">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="48056-125">Kullanmak için sanal makine Kimliğini biliyorsanız, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48056-125">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-the-nics"></a><span data-ttu-id="48056-126">NIC alma</span><span class="sxs-lookup"><span data-stu-id="48056-126">Get the NICS</span></span>

<span data-ttu-id="48056-127">Bu örnekte, bir sanal makinede NIC alıyoruz sanal makinede bir NIC IP adresi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="48056-127">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="48056-128">Sanal makinede test etmek istediğiniz IP adresi zaten biliyorsanız, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48056-128">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="48056-129">Çalışma IP akış doğrulayın</span><span class="sxs-lookup"><span data-stu-id="48056-129">Run IP flow verify</span></span>

<span data-ttu-id="48056-130">Biz cmdlet'i biz çalıştırmak çalıştırmak için gereken bilgileri sahip olduğunuza `az network watcher test-ip-flow` trafiği test etmek için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="48056-130">Now that we have the information needed to run the cmdlet, we run the `az network watcher test-ip-flow` cmdlet to test the traffic.</span></span> <span data-ttu-id="48056-131">Bu örnekte, ilk IP adresi ilk NIC üzerinde kullanıyoruz</span><span class="sxs-lookup"><span data-stu-id="48056-131">In this example, we are using the first IP address on the first NIC.</span></span>

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> <span data-ttu-id="48056-132">IP akış doğrulayın gerektirir VM kaynak çalıştırmak için ayrılır.</span><span class="sxs-lookup"><span data-stu-id="48056-132">IP Flow verify requires that the VM resource is allocated to run.</span></span>

## <a name="review-results"></a><span data-ttu-id="48056-133">Sonuçları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="48056-133">Review Results</span></span>

<span data-ttu-id="48056-134">Çalıştırdıktan sonra `az network watcher test-ip-flow` sonuçların döndürülmesini, aşağıdaki örnek önceki adımdan döndürülen sonuç.</span><span class="sxs-lookup"><span data-stu-id="48056-134">After running `az network watcher test-ip-flow` the results are returned, the following example is the results returned from the preceding step.</span></span>

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a><span data-ttu-id="48056-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="48056-135">Next steps</span></span>

<span data-ttu-id="48056-136">Trafik engelleniyor ve olmamalıdır, bkz: [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tanımlanan ağ güvenlik grubu ve güvenlik kuralları izlemek için.</span><span class="sxs-lookup"><span data-stu-id="48056-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

<span data-ttu-id="48056-137">NSG ayarlarınızı ziyaret ederek denetim öğrenin [denetim ağ güvenlik grupları (NSG) Ağ İzleyicisi ile](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="48056-137">Learn to audit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
