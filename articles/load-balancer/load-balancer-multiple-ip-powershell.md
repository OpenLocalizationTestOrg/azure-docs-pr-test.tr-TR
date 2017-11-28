---
title: "birden çok IP yapılandırmaları Azure Dengeleme aaaLoad | Microsoft Docs"
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
ms.openlocfilehash: fe1cdb317350942ff759229491c2025e98dd24a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a><span data-ttu-id="ccfe6-103">PowerShell kullanarak birden fazla IP yapılandırması üzerinde yükdengeleme</span><span class="sxs-lookup"><span data-stu-id="ccfe6-103">Load balancing on multiple IP configurations using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ccfe6-104">Portal</span><span class="sxs-lookup"><span data-stu-id="ccfe6-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="ccfe6-105">CLI</span><span class="sxs-lookup"><span data-stu-id="ccfe6-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="ccfe6-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ccfe6-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="ccfe6-107">Bu makalede, nasıl bir ikincil ağ arabirimi (NIC) toouse Azure yük dengeleyici ile birden çok IP adresleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ccfe6-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="ccfe6-108">Bu senaryo için Windows, her birincil ve ikincil bir NIC ile çalışan iki VM sahibiz</span><span class="sxs-lookup"><span data-stu-id="ccfe6-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="ccfe6-109">Her ikincil hello NIC'lerin iki IP yapılandırmaları vardır.</span><span class="sxs-lookup"><span data-stu-id="ccfe6-109">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="ccfe6-110">Her VM Web siteleri contoso.com ve fabrikam.com barındırır. İlişkili tooone hello IP yapılandırmalarının hello ikincil NIC üzerinde her Web sitesi olan</span><span class="sxs-lookup"><span data-stu-id="ccfe6-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="ccfe6-111">Azure yük dengeleyici tooexpose iki ön uç IP adresi, her bir Web sitesi, toodistribute trafiği toohello ilgili IP hello Web sitesinin yapılandırması için bir tane kullanırız.</span><span class="sxs-lookup"><span data-stu-id="ccfe6-111">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="ccfe6-112">Bu senaryoda hem ön uçlar yanı sıra arasında her iki arka uç havuzu IP adreslerini hello aynı bağlantı noktası numarası kullanır.</span><span class="sxs-lookup"><span data-stu-id="ccfe6-112">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![LB senaryo görüntüsü](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="ccfe6-114">Adımları tooload bakiyesi birden fazla IP yapılandırması</span><span class="sxs-lookup"><span data-stu-id="ccfe6-114">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="ccfe6-115">Bu makalede açıklanan tooachieve hello senaryo Hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="ccfe6-115">Follow hello steps below tooachieve hello scenario outlined in this article:</span></span>

1. <span data-ttu-id="ccfe6-116">Azure PowerShell'i yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ccfe6-116">Install Azure PowerShell.</span></span> <span data-ttu-id="ccfe6-117">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) hello Azure PowerShell'in en son sürümünü yükleme, aboneliğinizi seçme ve tooyour hesabında imzalama hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="ccfe6-117">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>
2. <span data-ttu-id="ccfe6-118">Ayarları aşağıdaki hello kullanarak bir kaynak grubu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ccfe6-118">Create a resource group using hello following settings:</span></span>

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    <span data-ttu-id="ccfe6-119">Daha fazla bilgi için bkz: 2. adım [bir kaynak grubu oluşturmak](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ccfe6-119">For more information, see Step 2 of [Create a Resource Group](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

3. <span data-ttu-id="ccfe6-120">[Bir kullanılabilirlik kümesi oluşturmak](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain Vm'leriniz.</span><span class="sxs-lookup"><span data-stu-id="ccfe6-120">[Create an Availability Set](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain your VMs.</span></span> <span data-ttu-id="ccfe6-121">Bu senaryo için komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ccfe6-121">For this scenario, use hello following command:</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. <span data-ttu-id="ccfe6-122">5'te 3 adımları yönergeleri izleyin [bir Windows VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) makalesi tek bir NIC ile VM tooprepare hello oluşturma</span><span class="sxs-lookup"><span data-stu-id="ccfe6-122">Follow instructions steps 3 through 5 in [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) article tooprepare hello creation of a VM with a single NIC.</span></span> <span data-ttu-id="ccfe6-123">6.1 adımı yürütme ve 6.2 adım yerine hello aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="ccfe6-123">Execute step 6.1, and use hello following instead of step 6.2:</span></span>

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    <span data-ttu-id="ccfe6-124">Daha sonra tamamlamak [bir Windows VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) 6,8 aracılığıyla 6.3 adımları.</span><span class="sxs-lookup"><span data-stu-id="ccfe6-124">Then complete [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) steps 6.3 through 6.8.</span></span>

5. <span data-ttu-id="ccfe6-125">Merhaba VM'ler, ikinci bir IP yapılandırması tooeach ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ccfe6-125">Add a second IP configuration tooeach of hello VMs.</span></span> <span data-ttu-id="ccfe6-126">Merhaba yönergeleri izleyin [toovirtual makineleri birden çok IP adresi atamak](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ccfe6-126">Follow hello instructions in [Assign multiple IP addresses toovirtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) article.</span></span> <span data-ttu-id="ccfe6-127">Yapılandırma ayarları aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ccfe6-127">Use hello following configuration settings:</span></span>

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    <span data-ttu-id="ccfe6-128">Bu öğreticinin hello amaçla tooassociate hello ikincil IP yapılandırmaları olan ve genel IP'ler gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ccfe6-128">You do not need tooassociate hello secondary IP configurations with public IPs for hello purpose of this tutorial.</span></span> <span data-ttu-id="ccfe6-129">Hello komutu tooremove hello ortak IP ilişkilendirme bölümünü düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="ccfe6-129">Edit hello command tooremove hello public IP association part.</span></span>

6. <span data-ttu-id="ccfe6-130">4. adım, bu makalenin 6-VM2 için yeniden tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="ccfe6-130">Complete steps 4 through 6 of this article again for VM2.</span></span> <span data-ttu-id="ccfe6-131">Bunun yapılması emin tooreplace hello VM adı tooVM2 olabilir.</span><span class="sxs-lookup"><span data-stu-id="ccfe6-131">Be sure tooreplace hello VM name tooVM2 when doing this.</span></span> <span data-ttu-id="ccfe6-132">Merhaba toocreate bir sanal ağ gerekmez Not ikinci VM.</span><span class="sxs-lookup"><span data-stu-id="ccfe6-132">Note that you do not need toocreate a virtual network for hello second VM.</span></span> <span data-ttu-id="ccfe6-133">Kullanım durumunu temel alarak yeni bir alt ağ oluşturamaz veya olabilir.</span><span class="sxs-lookup"><span data-stu-id="ccfe6-133">You may or may not create a new subnet based on your use case.</span></span>

7. <span data-ttu-id="ccfe6-134">İki ortak IP adresi oluşturun ve bunları gösterildiği gibi hello uygun değişkenlerde saklayın:</span><span class="sxs-lookup"><span data-stu-id="ccfe6-134">Create two public IP addresses and store them in hello appropriate variables as shown:</span></span>

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. <span data-ttu-id="ccfe6-135">İki ön uç IP yapılandırması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ccfe6-135">Create two frontend IP configurations:</span></span>

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. <span data-ttu-id="ccfe6-136">Arka uç adres havuzu, bir araştırma ve Yük Dengeleme kuralları oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ccfe6-136">Create your backend address pools, a probe, and your load balancing rules:</span></span>

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. <span data-ttu-id="ccfe6-137">Oluşturulan bu kaynakları oluşturduktan sonra yük dengeleyicisi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ccfe6-137">Once you have these resources created, create your load balancer:</span></span>

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. <span data-ttu-id="ccfe6-138">Merhaba ikinci arka uç adres havuzu ve ön uç IP yapılandırması tooyour yeni oluşturulan yük dengeleyici ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ccfe6-138">Add hello second backend address pool and frontend IP configuration tooyour newly created load balancer:</span></span>

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. <span data-ttu-id="ccfe6-139">Aşağıdaki Hello komutları hello NIC'ler alın ve her ikincil NIC toohello arka uç adres havuzu Merhaba, her iki IP yapılandırmalarını yük dengeleyici ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ccfe6-139">hello commands below get hello NICs and then add both IP configurations of each secondary NIC toohello backend address pool of hello load balancer:</span></span>

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

13. <span data-ttu-id="ccfe6-140">Son olarak, DNS kaynak kayıtlarını toopoint toohello ilgili ön uç IP adresi hello yük dengeleyici için yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ccfe6-140">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello Load Balancer.</span></span> <span data-ttu-id="ccfe6-141">Azure DNS'de etki alanlarınızı barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="ccfe6-141">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="ccfe6-142">Azure DNS yük dengeleyici ile kullanma hakkında daha fazla bilgi için bkz: [kullanarak Azure DNS diğer Azure hizmetleriyle](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="ccfe6-142">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccfe6-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ccfe6-143">Next steps</span></span>
- <span data-ttu-id="ccfe6-144">Nasıl toocombine Yük Dengeleme Azure hizmetleri hakkında daha fazla bilgi [Azure'da Yük Dengeleme hizmetlerini kullanarak](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="ccfe6-144">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="ccfe6-145">Nasıl günlükleri farklı türlerde içinde Azure toomanage kullanın ve yük dengeleyici sorun giderme öğrenin [analytics Azure yük dengeleyici için oturum](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="ccfe6-145">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
