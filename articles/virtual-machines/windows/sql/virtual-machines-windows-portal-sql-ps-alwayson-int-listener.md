---
title: "Her zaman kullanılabilirlik grubu dinleyicileri – Microsoft Azure yapılandırma | Microsoft Docs"
description: "Kullanılabilirlik grubu dinleyicileri iç yük dengeleyiciye sahip bir veya daha fazla IP adresi kullanarak Azure Resource Manager modeli yapılandırın."
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: 14b39cde-311c-4ddf-98f3-8694e01a7d3b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/22/2017
ms.author: mikeray
ms.openlocfilehash: 74fa1e4c9cfa608a9a385f3dd82a0599fbcc421c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a><span data-ttu-id="cd34e-103">Bir veya daha fazla Always On kullanılabilirlik grubu dinleyicileri - Kaynak Yöneticisi'ni yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cd34e-103">Configure one or more Always On availability group listeners - Resource Manager</span></span>
<span data-ttu-id="cd34e-104">Bu konuda gösterilmektedir nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="cd34e-104">This topic shows how to:</span></span>

* <span data-ttu-id="cd34e-105">Bir iç yük dengeleyici için PowerShell cmdlet'lerini kullanarak SQL Server kullanılabilirlik gruplarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd34e-105">Create an internal load balancer for SQL Server availability groups using PowerShell cmdlets.</span></span>
* <span data-ttu-id="cd34e-106">Birden çok kullanılabilirlik grubu için yük dengeleyici için ek IP adreslerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cd34e-106">Add additional IP addresses to a load balancer for more than one availability group.</span></span> 

<span data-ttu-id="cd34e-107">Bir kullanılabilirlik grubu dinleyicisi veritabanı erişimi için istemcilerin bağlandığı bir sanal ağ adı değil.</span><span class="sxs-lookup"><span data-stu-id="cd34e-107">An availability group listener is a virtual network name that clients connect to for database access.</span></span> <span data-ttu-id="cd34e-108">Azure sanal makinelerde yük dengeleyici için dinleyici IP adresini tutar.</span><span class="sxs-lookup"><span data-stu-id="cd34e-108">On Azure virtual machines, a load balancer holds the IP address for the listener.</span></span> <span data-ttu-id="cd34e-109">Yük Dengeleyici araştırması bağlantı noktasında dinleme SQL Server örneğine trafiğini yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="cd34e-109">The load balancer routes traffic to the instance of SQL Server that is listening on the probe port.</span></span> <span data-ttu-id="cd34e-110">Genellikle, bir iç yük dengeleyicisi bir kullanılabilirlik grubu kullanır.</span><span class="sxs-lookup"><span data-stu-id="cd34e-110">Usually, an availability group uses an internal load balancer.</span></span> <span data-ttu-id="cd34e-111">Azure iç yük dengeleyiciye bir veya daha çok IP adreslerini barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="cd34e-111">An Azure internal load balancer can host one or many IP addresses.</span></span> <span data-ttu-id="cd34e-112">Her IP adresi belirli araştırma bağlantı noktasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="cd34e-112">Each IP address uses a specific probe port.</span></span> <span data-ttu-id="cd34e-113">Bu belgede bir yük dengeleyici oluşturmak veya mevcut bir yük dengeleyici SQL Server kullanılabilirlik grupları için IP adresleri eklemek için PowerShell kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="cd34e-113">This document shows how to use PowerShell to create a load balancer, or add IP addresses to an existing load balancer for SQL Server availability groups.</span></span> 

<span data-ttu-id="cd34e-114">Bir iç yük dengeleyici için birden çok IP adresi atama olanağı Azure için yenidir ve yalnızca Resource Manager modelinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cd34e-114">The ability to assign multiple IP addresses to an internal load balancer is new to Azure and is only available in Resource Manager model.</span></span> <span data-ttu-id="cd34e-115">Bu görevi tamamlamak için Resource Manager modeli Azure sanal makinelerinde dağıtılan bir SQL Server kullanılabilirlik grubu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd34e-115">To complete this task, you need to have a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="cd34e-116">Her iki SQL Server sanal makineleri aynı kullanılabilirlik kümesine ait olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd34e-116">Both SQL Server virtual machines must belong to the same availability set.</span></span> <span data-ttu-id="cd34e-117">Kullanabileceğiniz [Microsoft şablonu](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) otomatik olarak Azure Kaynak Yöneticisi'nde kullanılabilirlik grubu oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="cd34e-117">You can use the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) to automatically create the availability group in Azure Resource Manager.</span></span> <span data-ttu-id="cd34e-118">Bu şablon, iç yük dengeleyicisi sizin için de dahil olmak üzere kullanılabilirlik grubu otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cd34e-118">This template automatically creates the availability group, including the internal load balancer for you.</span></span> <span data-ttu-id="cd34e-119">İsterseniz, aşağıdakileri yapabilirsiniz [el ile bir Always On kullanılabilirlik grubu yapılandırmak](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="cd34e-119">If you prefer, you can [manually configure an Always On availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="cd34e-120">Bu konu, kullanılabilirlik grupları zaten yapılandırılmış olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="cd34e-120">This topic requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="cd34e-121">İlgili Konular şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cd34e-121">Related topics include:</span></span>

* [<span data-ttu-id="cd34e-122">Azure VM (GUI) AlwaysOn Kullanılabilirlik Grupları Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cd34e-122">Configure AlwaysOn Availability Groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="cd34e-123">Azure Resource Manager ve PowerShell kullanarak VNet-VNet bağlantı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cd34e-123">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-the-windows-firewall"></a><span data-ttu-id="cd34e-124">Windows Güvenlik Duvarı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cd34e-124">Configure the Windows Firewall</span></span>
<span data-ttu-id="cd34e-125">Windows Güvenlik Duvarı'nı SQL Server erişime izin verecek şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cd34e-125">Configure the Windows Firewall to allow SQL Server access.</span></span> <span data-ttu-id="cd34e-126">Güvenlik duvarı kuralları SQL Server örneğini ve dinleyicisi yoklama bağlantı noktalarını kullandığı için TCP bağlantılarını izin verir.</span><span class="sxs-lookup"><span data-stu-id="cd34e-126">The firewall rules allow TCP connections to the ports use by the SQL Server instance, and the listener probe.</span></span> <span data-ttu-id="cd34e-127">Ayrıntılı yönergeler için bkz: [veritabanı altyapısı erişimi için Windows Güvenlik Duvarı Yapılandırma](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="cd34e-127">For detailed instructions, see [Configure a Windows Firewall for Database Engine Access](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span></span> <span data-ttu-id="cd34e-128">Sonda bağlantı noktası ve SQL sunucusu bağlantı noktası için bir gelen kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd34e-128">Create an inbound rule for the SQL Server port and for the probe port.</span></span>

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a><span data-ttu-id="cd34e-129">Örnek komut dosyası: PowerShell ile bir iç yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd34e-129">Example Script: Create an internal load balancer with PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="cd34e-130">Kullanılabilirlik grubu ile oluşturduysanız [Microsoft şablonu](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), iç yük dengeleyicisi zaten oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="cd34e-130">If you created your availability group with the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), the internal load balancer was already created.</span></span> 
> 
> 

<span data-ttu-id="cd34e-131">Aşağıdaki PowerShell betiğini bir iç yük dengeleyici oluşturur, Yük Dengeleme kuralları yapılandırır ve yük dengeleyici için bir IP adresini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="cd34e-131">The following PowerShell script creates an internal load balancer, configures the load balancing rules, and sets an IP address for the load balancer.</span></span> <span data-ttu-id="cd34e-132">Komut dosyasını çalıştırmak için Windows PowerShell ISE açın ve komut dosyası betik bölmesine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="cd34e-132">To run the script, open Windows PowerShell ISE, and paste the script in the Script pane.</span></span> <span data-ttu-id="cd34e-133">Kullanım `Login-AzureRMAccount` PowerShell oturum açmak için.</span><span class="sxs-lookup"><span data-stu-id="cd34e-133">Use `Login-AzureRMAccount` to log in to PowerShell.</span></span> <span data-ttu-id="cd34e-134">Birden çok Azure aboneliğiniz varsa, kullanmak `Select-AzureRmSubscription ` aboneliği ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="cd34e-134">If you have multiple Azure subscriptions, use `Select-AzureRmSubscription ` to set the subscription.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<Resource Group Name>" # Resource group name
$VNetName = "<Virtual Network Name>"         # Virtual network name
$SubnetName = "<Subnet Name>"                # Subnet name
$ILBName = "<Load Balancer Name>"            # ILB name
$Location = "<Azure Region>"                 # Azure location
$VMNames = "<VM1>","<VM2>"                   # Virtual machine names

$ILBIP = "<n.n.n.n>"                         # IP address
[int]$ListenerPort = "<nnnn>"                # AG listener port
[int]$ProbePort = "<nnnn>"                   # Probe port

$LBProbeName ="ILBPROBE_$ListenerPort"       # The Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # The Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for the front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for the back-end configuration

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 

$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName 

$FEConfig = New-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.id

$BEConfig = New-AzureRMLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName 

$SQLHealthProbe = New-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -Protocol tcp -Port $ProbePort -IntervalInSeconds 15 -ProbeCount 2

$ILBRule = New-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP 

$ILB= New-AzureRmLoadBalancer -Location $Location -Name $ILBName -ResourceGroupName $ResourceGroupName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -LoadBalancingRule $ILBRule -Probe $SQLHealthProbe 

$bepool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB 

foreach($VMName in $VMNames)
    {
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName 
        $NICName = ($vm.NetworkProfile.NetworkInterfaces.Id.split('/') | select -last 1)
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools = $BEPool
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name 
    }
```

## <span data-ttu-id="cd34e-135"><a name="Add-IP"></a>Örnek komut dosyası: PowerShell ile var olan bir yük dengeleyici için bir IP adresi Ekle</span><span class="sxs-lookup"><span data-stu-id="cd34e-135"><a name="Add-IP"></a> Example script: Add an IP address to an existing load balancer with PowerShell</span></span>
<span data-ttu-id="cd34e-136">Birden çok kullanılabilirlik grubu kullanmak için ek bir IP adresi yük dengeleyiciye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cd34e-136">To use more than one availability group, add an additional IP address to the load balancer.</span></span> <span data-ttu-id="cd34e-137">Her IP adresi, kendi Yük Dengeleme kuralı, araştırma bağlantı noktası ve ön bağlantı noktası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="cd34e-137">Each IP address requires its own load balancing rule, probe port, and front port.</span></span>

<span data-ttu-id="cd34e-138">Ön uç bağlantı uygulamaları SQL Server örneğine bağlanmak için kullandığınız bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="cd34e-138">The front-end port is the port that applications use to connect to the SQL Server instance.</span></span> <span data-ttu-id="cd34e-139">IP adresleri farklı kullanılabilirlik grupları için aynı ön uç bağlantı noktasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd34e-139">IP addresses for different availability groups can use the same front-end port.</span></span>

> [!NOTE]
> <span data-ttu-id="cd34e-140">SQL Server kullanılabilirlik grupları için her IP adresi belirli sonda bağlantı noktası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="cd34e-140">For SQL Server availability groups, each IP address requires a specific probe port.</span></span> <span data-ttu-id="cd34e-141">Örneğin, bir IP adresi bir yük dengeleyicideki sonda bağlantı noktası 59999 kullanıyorsa, herhangi bir IP adresi üzerinde bu yük dengeleyici araştırması bağlantı noktası 59999 kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd34e-141">For example, if one IP address on a load balancer uses probe port 59999, no other IP addresses on that load balancer can use probe port 59999.</span></span>

* <span data-ttu-id="cd34e-142">Yük Dengeleyici sınırları hakkında daha fazla bilgi için bkz: **özel ön uç IP yük dengeleyici başına** altında [ağ sınırları - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="cd34e-142">For information about load balancer limits, see **Private front end IP per load balancer** under [Networking Limits - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span></span>
* <span data-ttu-id="cd34e-143">Kullanılabilirlik grubu sınırları hakkında daha fazla bilgi için bkz: [kısıtlamaları (kullanılabilirlik grupları)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span><span class="sxs-lookup"><span data-stu-id="cd34e-143">For information about availability group limits, see [Restrictions (Availability Groups)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span></span>

<span data-ttu-id="cd34e-144">Aşağıdaki komut dosyasını yeni bir IP adresi için var olan bir yük dengeleyici ekler.</span><span class="sxs-lookup"><span data-stu-id="cd34e-144">The following script adds a new IP address to an existing load balancer.</span></span> <span data-ttu-id="cd34e-145">ILB, yük dengeleyici ön uç bağlantı noktası için dinleyici bağlantı noktasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="cd34e-145">The ILB uses the listener port for the load balancing front-end port.</span></span> <span data-ttu-id="cd34e-146">Bu bağlantı noktası, SQL Server üzerinde dinleme bağlantı noktası olabilir.</span><span class="sxs-lookup"><span data-stu-id="cd34e-146">This port can be the port that SQL Server is listening on.</span></span> <span data-ttu-id="cd34e-147">SQL Server'ın varsayılan örnekleri için bağlantı noktası 1433'tür.</span><span class="sxs-lookup"><span data-stu-id="cd34e-147">For default instances of SQL Server, the port is 1433.</span></span> <span data-ttu-id="cd34e-148">Arka uç bağlantı noktası ön uç bağlantı noktası ile aynı olacak şekilde yük dengeleme kuralını bir kullanılabilirlik grubu için bir kayan IP (doğrudan sunucu dönüşü) gerektirir.</span><span class="sxs-lookup"><span data-stu-id="cd34e-148">The load balancing rule for an availability group requires a floating IP (direct server return) so the back-end port is the same as the front-end port.</span></span> <span data-ttu-id="cd34e-149">Değişkenleri ortamınız için güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="cd34e-149">Update the variables for your environment.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<ResourceGroup>"          # Resource group name
$VNetName = "<VirtualNetwork>"                  # Virtual network name
$SubnetName = "<Subnet>"                        # Subnet name
$ILBName = "<ILBName>"                          # ILB name                      

$ILBIP = "<n.n.n.n>"                            # IP address
[int]$ListenerPort = "<nnnn>"                   # AG listener port
[int]$ProbePort = "<nnnnn>"                     # Probe port 

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName 

$count = $ILB.FrontendIpConfigurations.Count+1
$FrontEndConfigurationName ="FE_SQLAGILB_$count"  

$LBProbeName = "ILBPROBE_$count"
$LBConfigrulename = "ILBCR_$count"

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id 

$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 15  | Set-AzureRmLoadBalancer 

$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB

$SQLHealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $ILB.BackendAddressPools[0].Name -LoadBalancer $ILB 

$ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort  $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP | Set-AzureRmLoadBalancer   
```

## <a name="configure-the-listener"></a><span data-ttu-id="cd34e-150">Dinleyici yapılandırın</span><span class="sxs-lookup"><span data-stu-id="cd34e-150">Configure the listener</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-the-listener-port-in-sql-server-management-studio"></a><span data-ttu-id="cd34e-151">SQL Server Management Studio'da dinleyici bağlantı noktasını ayarla</span><span class="sxs-lookup"><span data-stu-id="cd34e-151">Set the listener port in SQL Server Management Studio</span></span>

1. <span data-ttu-id="cd34e-152">SQL Server Management Studio'yu başlatın ve birincil kopyaya bağlanın.</span><span class="sxs-lookup"><span data-stu-id="cd34e-152">Launch SQL Server Management Studio and connect to the primary replica.</span></span>

1. <span data-ttu-id="cd34e-153">Gidin **AlwaysOn yüksek kullanılabilirlik** | **kullanılabilirlik grupları** | **kullanılabilirlik grubu dinleyicileri**.</span><span class="sxs-lookup"><span data-stu-id="cd34e-153">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span> 

1. <span data-ttu-id="cd34e-154">Yük Devretme Kümesi Yöneticisi'nde oluşturulan dinleyici adı görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="cd34e-154">You should now see the listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="cd34e-155">Dinleyici adına sağ tıklatın ve **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="cd34e-155">Right-click the listener name and click **Properties**.</span></span>

1. <span data-ttu-id="cd34e-156">İçinde **bağlantı noktası** kutusunda, daha önce kullandığınız $EndpointPort kullanarak için kullanılabilirlik grubu dinleyicisinin bağlantı noktası numarası belirtin (1433 olduğu varsayılan), ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="cd34e-156">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.</span></span>

## <a name="test-the-connection-to-the-listener"></a><span data-ttu-id="cd34e-157">Dinleyici bağlantıyı sınayın</span><span class="sxs-lookup"><span data-stu-id="cd34e-157">Test the connection to the listener</span></span>

<span data-ttu-id="cd34e-158">Bağlantıyı sınamak için:</span><span class="sxs-lookup"><span data-stu-id="cd34e-158">To test the connection:</span></span>

1. <span data-ttu-id="cd34e-159">RDP bir SQL Server'a aynı sanal ağda bulunan, ancak çoğaltma kendisine ait değil.</span><span class="sxs-lookup"><span data-stu-id="cd34e-159">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span></span> <span data-ttu-id="cd34e-160">Bu kümedeki diğer SQL Server olabilir.</span><span class="sxs-lookup"><span data-stu-id="cd34e-160">This can be the other SQL Server in the cluster.</span></span>

1. <span data-ttu-id="cd34e-161">Kullanım **sqlcmd** yardımcı programını kullanarak bağlantıyı sınayın.</span><span class="sxs-lookup"><span data-stu-id="cd34e-161">Use **sqlcmd** utility to test the connection.</span></span> <span data-ttu-id="cd34e-162">Örneğin, aşağıdaki komut dosyasını oluşturur. bir **sqlcmd** Windows kimlik doğrulaması dinleyicisiyle aracılığıyla birincil çoğaltma bağlantısı:</span><span class="sxs-lookup"><span data-stu-id="cd34e-162">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span></span>
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    <span data-ttu-id="cd34e-163">Dinleyici varsayılan dışında bir bağlantı noktası kullanıyorsa (1433) bağlantı noktası, bağlantı dizesinde bağlantı noktasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="cd34e-163">If the listener is using a port other than the default port (1433), specify the port in the connection string.</span></span> <span data-ttu-id="cd34e-164">Örneğin, aşağıdaki sqlcmd komut bir dinleyici bağlantı noktası 1435 bağlanır:</span><span class="sxs-lookup"><span data-stu-id="cd34e-164">For example, the following sqlcmd command connects to a listener at port 1435:</span></span> 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="cd34e-165">SQL Server'ın hangi örneğinin birincil çoğaltmayı barındıran için SQLCMD bağlantı otomatik olarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="cd34e-165">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span></span> 

> [!NOTE]
> <span data-ttu-id="cd34e-166">Belirttiğiniz bağlantı noktasının Güvenlik Duvarı'nı her iki SQL sunucularının açık olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="cd34e-166">Make sure that the port you specify is open on the firewall of both SQL Servers.</span></span> <span data-ttu-id="cd34e-167">Her iki sunucuyu kullandığınız TCP bağlantı noktası için bir gelen kuralı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="cd34e-167">Both servers require an inbound rule for the TCP port that you use.</span></span> <span data-ttu-id="cd34e-168">Bkz: [Ekle veya güvenlik duvarı kuralını Düzenle](http://technet.microsoft.com/library/cc753558.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="cd34e-168">See [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx) for more information.</span></span> 
> 
> 

## <a name="guidelines-and-limitations"></a><span data-ttu-id="cd34e-169">Kılavuzlar ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="cd34e-169">Guidelines and limitations</span></span>
<span data-ttu-id="cd34e-170">Kullanılabilirlik grubu dinleyicisi iç kullanarak azure'da aşağıdaki yönergelere yük dengeleyici dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="cd34e-170">Note the following guidelines on availability group listener in Azure using internal load balancer:</span></span>

* <span data-ttu-id="cd34e-171">Bir iç yük dengeleyici ile gelen dinleyicisi aynı sanal ağda yalnızca erişin.</span><span class="sxs-lookup"><span data-stu-id="cd34e-171">With an internal load balancer, you only access the listener from within the same virtual network.</span></span>


## <a name="for-more-information"></a><span data-ttu-id="cd34e-172">Daha fazla bilgi için</span><span class="sxs-lookup"><span data-stu-id="cd34e-172">For more information</span></span>
<span data-ttu-id="cd34e-173">Daha fazla bilgi için bkz: [yapılandırma Always On kullanılabilirlik grubu Azure VM'de el ile](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="cd34e-173">For more information, see [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="cd34e-174">PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="cd34e-174">PowerShell cmdlets</span></span>
<span data-ttu-id="cd34e-175">Azure sanal makineler için bir iç yük dengeleyici oluşturmak için aşağıdaki PowerShell cmdlet'lerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="cd34e-175">Use the following PowerShell cmdlets to create an internal load balancer for Azure virtual machines.</span></span>

* <span data-ttu-id="cd34e-176">[AzureRmLoadBalancer yeni](http://msdn.microsoft.com/library/mt619450.aspx) bir yük dengeleyici oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cd34e-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) creates a load balancer.</span></span> 
* <span data-ttu-id="cd34e-177">[AzureRMLoadBalancerFrontendIpConfig yeni](http://msdn.microsoft.com/library/mt603510.aspx) bir yük dengeleyici için bir ön uç IP yapılandırmasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cd34e-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) creates a front-end IP configuration for a load balancer.</span></span> 
* <span data-ttu-id="cd34e-178">[AzureRmLoadBalancerRuleConfig yeni](http://msdn.microsoft.com/library/mt619391.aspx) bir yük dengeleyici için bir kural yapılandırma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cd34e-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) creates a rule configuration for a load balancer.</span></span> 
* <span data-ttu-id="cd34e-179">[AzureRmLoadBalancerBackendAddressPoolConfig yeni](http://msdn.microsoft.com/library/mt603791.aspx) bir yük dengeleyici için arka uç adres havuzu yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cd34e-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) creates a backend address pool configuration for a load balancer.</span></span> 
* <span data-ttu-id="cd34e-180">[AzureRmLoadBalancerProbeConfig yeni](http://msdn.microsoft.com/library/mt603847.aspx) bir yük dengeleyici için bir araştırma yapılandırma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cd34e-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) creates a probe configuration for a load balancer.</span></span>
* <span data-ttu-id="cd34e-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) bir yük dengeleyici Azure kaynak grubundan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="cd34e-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) removes a load balancer from an Azure resource group.</span></span>
