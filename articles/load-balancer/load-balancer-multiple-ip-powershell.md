---
title: "Azure içinde birden fazla IP yapılandırması dengelemesini | Microsoft Docs"
description: "Birincil ve ikincil IP yapılandırmaları yükdengeleme"
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: annahar
ms.openlocfilehash: a8550519f094ca7afcd868a14b313337627f97d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a><span data-ttu-id="d5eef-103">PowerShell kullanarak birden fazla IP yapılandırması üzerinde yükdengeleme</span><span class="sxs-lookup"><span data-stu-id="d5eef-103">Load balancing on multiple IP configurations using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d5eef-104">Portal</span><span class="sxs-lookup"><span data-stu-id="d5eef-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="d5eef-105">CLI</span><span class="sxs-lookup"><span data-stu-id="d5eef-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="d5eef-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5eef-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="d5eef-107">Bu makalede, bir ikincil ağ arabirimi (NIC) üzerinde birden çok IP adresleriyle Azure yük dengeleyici kullanmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="d5eef-107">This article describes how to use Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="d5eef-108">Bu senaryo için Windows, her birincil ve ikincil bir NIC ile çalışan iki VM sahibiz</span><span class="sxs-lookup"><span data-stu-id="d5eef-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="d5eef-109">Her ikincil NIC'ler, iki IP yapılandırmaları vardır.</span><span class="sxs-lookup"><span data-stu-id="d5eef-109">Each of the secondary NICs have two IP configurations.</span></span> <span data-ttu-id="d5eef-110">Her VM Web siteleri contoso.com ve fabrikam.com barındırır. Her Web sitesi IP yapılandırmaları birine ikincil NIC üzerinde bağlı</span><span class="sxs-lookup"><span data-stu-id="d5eef-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound to one of the IP configurations on the secondary NIC.</span></span> <span data-ttu-id="d5eef-111">Azure yük dengeleyici iki ön uç IP adresi, bir Web sitesi için ilgili IP yapılandırmasını trafiğini dağıtmak için her Web sitesi için kullanıma sunmak için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="d5eef-111">We use Azure Load Balancer to expose two frontend IP addresses, one for each website, to distribute traffic to the respective IP configuration for the website.</span></span> <span data-ttu-id="d5eef-112">Bu senaryo aynı bağlantı noktası numarası hem ön uçlar yanı sıra arasında her iki arka uç havuzu IP adreslerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="d5eef-112">This scenario uses the same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![LB senaryo görüntüsü](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-to-load-balance-on-multiple-ip-configurations"></a><span data-ttu-id="d5eef-114">Birden çok IP yapılandırmaları dengelemek için adımları</span><span class="sxs-lookup"><span data-stu-id="d5eef-114">Steps to load balance on multiple IP configurations</span></span>

<span data-ttu-id="d5eef-115">Bu makalede açıklanan senaryo elde etmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d5eef-115">Follow the steps below to achieve the scenario outlined in this article:</span></span>

1. <span data-ttu-id="d5eef-116">Azure PowerShell'i yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d5eef-116">Install Azure PowerShell.</span></span> <span data-ttu-id="d5eef-117">Azure PowerShell’in en son sürümünü yükleme, aboneliğinizi seçme ve hesabınızda oturum açma hakkında bilgi almak için bkz. [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d5eef-117">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>
2. <span data-ttu-id="d5eef-118">Aşağıdaki ayarları kullanarak bir kaynak grubu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="d5eef-118">Create a resource group using the following settings:</span></span>

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    <span data-ttu-id="d5eef-119">Daha fazla bilgi için bkz: 2. adım [bir kaynak grubu oluşturmak](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d5eef-119">For more information, see Step 2 of [Create a Resource Group](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

3. <span data-ttu-id="d5eef-120">[Bir kullanılabilirlik kümesi oluşturmak](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) Vm'leriniz içerecek şekilde.</span><span class="sxs-lookup"><span data-stu-id="d5eef-120">[Create an Availability Set](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) to contain your VMs.</span></span> <span data-ttu-id="d5eef-121">Bu senaryo için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="d5eef-121">For this scenario, use the following command:</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. <span data-ttu-id="d5eef-122">5'te 3 adımları yönergeleri izleyin [bir Windows VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) makale tek bir NIC ile VM oluşturma hazırlama</span><span class="sxs-lookup"><span data-stu-id="d5eef-122">Follow instructions steps 3 through 5 in [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) article to prepare the creation of a VM with a single NIC.</span></span> <span data-ttu-id="d5eef-123">6.1 adımı yürütme ve adım 6.2 yerine aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="d5eef-123">Execute step 6.1, and use the following instead of step 6.2:</span></span>

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    <span data-ttu-id="d5eef-124">Daha sonra tamamlamak [bir Windows VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) 6,8 aracılığıyla 6.3 adımları.</span><span class="sxs-lookup"><span data-stu-id="d5eef-124">Then complete [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) steps 6.3 through 6.8.</span></span>

5. <span data-ttu-id="d5eef-125">İkinci IP yapılandırması her sanal makineleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d5eef-125">Add a second IP configuration to each of the VMs.</span></span> <span data-ttu-id="d5eef-126">' Ndaki yönergeleri izleyin [birden çok IP adresi sanal makinelere atamak](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) makalesi.</span><span class="sxs-lookup"><span data-stu-id="d5eef-126">Follow the instructions in [Assign multiple IP addresses to virtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) article.</span></span> <span data-ttu-id="d5eef-127">Aşağıdaki yapılandırma ayarları kullanın:</span><span class="sxs-lookup"><span data-stu-id="d5eef-127">Use the following configuration settings:</span></span>

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    <span data-ttu-id="d5eef-128">Bu öğretici amacıyla genel IP'ler ikincil IP yapılandırmaları ilişkilendirmek gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d5eef-128">You do not need to associate the secondary IP configurations with public IPs for the purpose of this tutorial.</span></span> <span data-ttu-id="d5eef-129">Genel IP ilişkilendirme bölümü kaldırmak için komutu düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="d5eef-129">Edit the command to remove the public IP association part.</span></span>

6. <span data-ttu-id="d5eef-130">4. adım, bu makalenin 6-VM2 için yeniden tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="d5eef-130">Complete steps 4 through 6 of this article again for VM2.</span></span> <span data-ttu-id="d5eef-131">Bunu yaparken VM2 VM adıyla değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d5eef-131">Be sure to replace the VM name to VM2 when doing this.</span></span> <span data-ttu-id="d5eef-132">İkinci VM için sanal ağ oluşturma gerekmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d5eef-132">Note that you do not need to create a virtual network for the second VM.</span></span> <span data-ttu-id="d5eef-133">Kullanım durumunu temel alarak yeni bir alt ağ oluşturamaz veya olabilir.</span><span class="sxs-lookup"><span data-stu-id="d5eef-133">You may or may not create a new subnet based on your use case.</span></span>

7. <span data-ttu-id="d5eef-134">İki ortak IP adresi oluşturun ve bunları uygun değişkenlerde gösterildiği gibi depolar:</span><span class="sxs-lookup"><span data-stu-id="d5eef-134">Create two public IP addresses and store them in the appropriate variables as shown:</span></span>

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. <span data-ttu-id="d5eef-135">İki ön uç IP yapılandırması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="d5eef-135">Create two frontend IP configurations:</span></span>

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. <span data-ttu-id="d5eef-136">Arka uç adres havuzu, bir araştırma ve Yük Dengeleme kuralları oluşturun:</span><span class="sxs-lookup"><span data-stu-id="d5eef-136">Create your backend address pools, a probe, and your load balancing rules:</span></span>

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. <span data-ttu-id="d5eef-137">Oluşturulan bu kaynakları oluşturduktan sonra yük dengeleyicisi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="d5eef-137">Once you have these resources created, create your load balancer:</span></span>

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. <span data-ttu-id="d5eef-138">İkinci arka uç adres havuzu ve ön uç IP yapılandırması, yeni oluşturulan yük dengeleyiciye ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d5eef-138">Add the second backend address pool and frontend IP configuration to your newly created load balancer:</span></span>

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. <span data-ttu-id="d5eef-139">Aşağıdaki komutları NIC'ler alın ve ardından her iki IP yapılandırmaları her ikincil NIC'in yük dengeleyici arka uç adres havuzuna ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d5eef-139">The commands below get the NICs and then add both IP configurations of each secondary NIC to the backend address pool of the load balancer:</span></span>

    ```powershell
    $nic1 = Get-AzureRmNetworkInterface -Name "VM1-NIC2" -ResourceGroupName "MyResourcegroup";
    $nic2 = Get-AzureRmNetworkInterface -Name "VM2-NIC2" -ResourceGroupName "MyResourcegroup";

    $nic1.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic1.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);
    $nic2.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic2.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);

    $mylb = $mylb | Set-AzureRmLoadBalancer

    $nic1 | Set-AzureRmNetworkInterface
    $nic2 | Set-AzureRmNetworkInterface
    ```

13. <span data-ttu-id="d5eef-140">Son olarak, DNS kaynak kayıtlarını yük dengeleyici ilgili ön uç IP adresine işaret edecek şekilde yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d5eef-140">Finally, you must configure DNS resource records to point to the respective frontend IP address of the Load Balancer.</span></span> <span data-ttu-id="d5eef-141">Azure DNS'de etki alanlarınızı barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="d5eef-141">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="d5eef-142">Azure DNS yük dengeleyici ile kullanma hakkında daha fazla bilgi için bkz: [kullanarak Azure DNS diğer Azure hizmetleriyle](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="d5eef-142">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5eef-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d5eef-143">Next steps</span></span>
- <span data-ttu-id="d5eef-144">Yük Dengeleme Azure hizmetlerinde birleştirme hakkında daha fazla bilgi edinin [Azure'da Yük Dengeleme hizmetlerini kullanarak](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="d5eef-144">Learn more about how to combine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="d5eef-145">Günlükleri farklı türde Azure'da yönetmek ve yük dengeleyici sorunlarını gidermek için nasıl kullanabileceğinizi öğrenin [analytics Azure yük dengeleyici için oturum](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="d5eef-145">Learn how you can use different types of logs in Azure to manage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
