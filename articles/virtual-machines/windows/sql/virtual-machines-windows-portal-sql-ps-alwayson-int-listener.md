---
title: "aaaConfigure her zaman üzerinde kullanılabilirlik grubu dinleyicileri – Microsoft Azure | Microsoft Docs"
description: "Kullanılabilirlik grubu dinleyicileri hello Azure Resource Manager modeli, iç yük dengeleyiciye sahip bir veya daha fazla IP adresi kullanarak yapılandırın."
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
ms.openlocfilehash: 81edfe2c2ea536d8dcec466f36fccf8bc0e02c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a><span data-ttu-id="d4348-103">Bir veya daha fazla Always On kullanılabilirlik grubu dinleyicileri - Kaynak Yöneticisi'ni yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d4348-103">Configure one or more Always On availability group listeners - Resource Manager</span></span>
<span data-ttu-id="d4348-104">Bu konuda gösterilmektedir nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="d4348-104">This topic shows how to:</span></span>

* <span data-ttu-id="d4348-105">Bir iç yük dengeleyici için PowerShell cmdlet'lerini kullanarak SQL Server kullanılabilirlik gruplarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4348-105">Create an internal load balancer for SQL Server availability groups using PowerShell cmdlets.</span></span>
* <span data-ttu-id="d4348-106">Ek IP adreslerini tooa yük dengeleyici için birden çok kullanılabilirlik grubu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d4348-106">Add additional IP addresses tooa load balancer for more than one availability group.</span></span> 

<span data-ttu-id="d4348-107">Bir kullanılabilirlik grubu dinleyicisi, istemcilerin toofor veritabanı erişimi bağlanmasını bir sanal ağ adıdır.</span><span class="sxs-lookup"><span data-stu-id="d4348-107">An availability group listener is a virtual network name that clients connect toofor database access.</span></span> <span data-ttu-id="d4348-108">Azure sanal makinelerde hello dinleyici için başlangıç IP adresi bir yük dengeleyici tutar.</span><span class="sxs-lookup"><span data-stu-id="d4348-108">On Azure virtual machines, a load balancer holds hello IP address for hello listener.</span></span> <span data-ttu-id="d4348-109">Merhaba yük dengeleyici yollar hello araştırma bağlantı noktasında dinleme SQL Server'ın toohello örneğinin trafiği.</span><span class="sxs-lookup"><span data-stu-id="d4348-109">hello load balancer routes traffic toohello instance of SQL Server that is listening on hello probe port.</span></span> <span data-ttu-id="d4348-110">Genellikle, bir iç yük dengeleyicisi bir kullanılabilirlik grubu kullanır.</span><span class="sxs-lookup"><span data-stu-id="d4348-110">Usually, an availability group uses an internal load balancer.</span></span> <span data-ttu-id="d4348-111">Azure iç yük dengeleyiciye bir veya daha çok IP adreslerini barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="d4348-111">An Azure internal load balancer can host one or many IP addresses.</span></span> <span data-ttu-id="d4348-112">Her IP adresi belirli araştırma bağlantı noktasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="d4348-112">Each IP address uses a specific probe port.</span></span> <span data-ttu-id="d4348-113">Bu belge gösterir nasıl toouse PowerShell toocreate bir yük dengeleyici veya IP adresleri tooan var olan yük dengeleyici için SQL Server kullanılabilirlik gruplarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d4348-113">This document shows how toouse PowerShell toocreate a load balancer, or add IP addresses tooan existing load balancer for SQL Server availability groups.</span></span> 

<span data-ttu-id="d4348-114">birden çok IP adresleri tooan iç yük dengeleyici yeni tooAzure edilmiştir ve yalnızca Resource Manager modelinde kullanılabilir yeteneği tooassign hello.</span><span class="sxs-lookup"><span data-stu-id="d4348-114">hello ability tooassign multiple IP addresses tooan internal load balancer is new tooAzure and is only available in Resource Manager model.</span></span> <span data-ttu-id="d4348-115">toocomplete bu görev bir SQL Server kullanılabilirlik grubu dağıtılan Resource Manager modelinde Azure sanal makinelerde toohave gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4348-115">toocomplete this task, you need toohave a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="d4348-116">Her iki SQL Server sanal makineleri toohello ait olmalıdır aynı kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="d4348-116">Both SQL Server virtual machines must belong toohello same availability set.</span></span> <span data-ttu-id="d4348-117">Merhaba kullanabilirsiniz [Microsoft şablonu](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically Azure Kaynak Yöneticisi'nde hello kullanılabilirlik grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4348-117">You can use hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically create hello availability group in Azure Resource Manager.</span></span> <span data-ttu-id="d4348-118">Bu şablon, sizin için hello iç yük dengeleyici gibi hello kullanılabilirlik grubu otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d4348-118">This template automatically creates hello availability group, including hello internal load balancer for you.</span></span> <span data-ttu-id="d4348-119">İsterseniz, aşağıdakileri yapabilirsiniz [el ile bir Always On kullanılabilirlik grubu yapılandırmak](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="d4348-119">If you prefer, you can [manually configure an Always On availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="d4348-120">Bu konu, kullanılabilirlik grupları zaten yapılandırılmış olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d4348-120">This topic requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="d4348-121">İlgili Konular şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d4348-121">Related topics include:</span></span>

* [<span data-ttu-id="d4348-122">Azure VM (GUI) AlwaysOn Kullanılabilirlik Grupları Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d4348-122">Configure AlwaysOn Availability Groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="d4348-123">Azure Resource Manager ve PowerShell kullanarak VNet-VNet bağlantı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d4348-123">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a><span data-ttu-id="d4348-124">Merhaba Windows Güvenlik Duvarı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d4348-124">Configure hello Windows Firewall</span></span>
<span data-ttu-id="d4348-125">Merhaba Windows Güvenlik Duvarı tooallow SQL Server erişimi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d4348-125">Configure hello Windows Firewall tooallow SQL Server access.</span></span> <span data-ttu-id="d4348-126">Merhaba güvenlik duvarı kuralları hello SQL Server örneği ve hello dinleyicisi yoklama TCP bağlantıları toohello bağlantı noktalarını kullanma izin verir.</span><span class="sxs-lookup"><span data-stu-id="d4348-126">hello firewall rules allow TCP connections toohello ports use by hello SQL Server instance, and hello listener probe.</span></span> <span data-ttu-id="d4348-127">Ayrıntılı yönergeler için bkz: [veritabanı altyapısı erişimi için Windows Güvenlik Duvarı Yapılandırma](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="d4348-127">For detailed instructions, see [Configure a Windows Firewall for Database Engine Access](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span></span> <span data-ttu-id="d4348-128">Merhaba sonda bağlantı noktası ve hello SQL Server bağlantı noktası için bir gelen kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4348-128">Create an inbound rule for hello SQL Server port and for hello probe port.</span></span>

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a><span data-ttu-id="d4348-129">Örnek komut dosyası: PowerShell ile bir iç yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4348-129">Example Script: Create an internal load balancer with PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="d4348-130">Kullanılabilirlik grubu ile Merhaba oluşturduysanız [Microsoft şablonu](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), hello iç yük dengeleyici zaten oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="d4348-130">If you created your availability group with hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), hello internal load balancer was already created.</span></span> 
> 
> 

<span data-ttu-id="d4348-131">Merhaba aşağıdaki PowerShell betiğini bir iç yük dengeleyici oluşturur, hello Yük Dengeleme kuralları yapılandırır ve hello yük dengeleyici için bir IP adresini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d4348-131">hello following PowerShell script creates an internal load balancer, configures hello load balancing rules, and sets an IP address for hello load balancer.</span></span> <span data-ttu-id="d4348-132">toorun hello komut dosyası, Windows PowerShell ISE açın ve hello betik bölmesinde hello betiğini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="d4348-132">toorun hello script, open Windows PowerShell ISE, and paste hello script in hello Script pane.</span></span> <span data-ttu-id="d4348-133">Kullanım `Login-AzureRMAccount` tooPowerShell toolog.</span><span class="sxs-lookup"><span data-stu-id="d4348-133">Use `Login-AzureRMAccount` toolog in tooPowerShell.</span></span> <span data-ttu-id="d4348-134">Birden çok Azure aboneliğiniz varsa, kullanmak `Select-AzureRmSubscription ` tooset hello abonelik.</span><span class="sxs-lookup"><span data-stu-id="d4348-134">If you have multiple Azure subscriptions, use `Select-AzureRmSubscription ` tooset hello subscription.</span></span> 

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

$LBProbeName ="ILBPROBE_$ListenerPort"       # hello Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # hello Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for hello front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for hello back-end configuration

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

## <span data-ttu-id="d4348-135"><a name="Add-IP"></a>Örnek komut dosyası: bir IP adresi tooan varolan yük dengeleyicisi PowerShell ile ekleme</span><span class="sxs-lookup"><span data-stu-id="d4348-135"><a name="Add-IP"></a> Example script: Add an IP address tooan existing load balancer with PowerShell</span></span>
<span data-ttu-id="d4348-136">bir kullanılabilirlik grubu birden çok toouse bir ek IP adresi toohello yük dengeleyiciye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d4348-136">toouse more than one availability group, add an additional IP address toohello load balancer.</span></span> <span data-ttu-id="d4348-137">Her IP adresi, kendi Yük Dengeleme kuralı, araştırma bağlantı noktası ve ön bağlantı noktası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d4348-137">Each IP address requires its own load balancing rule, probe port, and front port.</span></span>

<span data-ttu-id="d4348-138">Merhaba ön uç bağlantı noktası uygulamaları tooconnect toohello SQL Server örneğini kullan hello bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="d4348-138">hello front-end port is hello port that applications use tooconnect toohello SQL Server instance.</span></span> <span data-ttu-id="d4348-139">IP adresleri farklı kullanılabilirlik grupları kullanabilir hello aynı ön uç bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="d4348-139">IP addresses for different availability groups can use hello same front-end port.</span></span>

> [!NOTE]
> <span data-ttu-id="d4348-140">SQL Server kullanılabilirlik grupları için her IP adresi belirli sonda bağlantı noktası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d4348-140">For SQL Server availability groups, each IP address requires a specific probe port.</span></span> <span data-ttu-id="d4348-141">Örneğin, bir IP adresi bir yük dengeleyicideki sonda bağlantı noktası 59999 kullanıyorsa, herhangi bir IP adresi üzerinde bu yük dengeleyici araştırması bağlantı noktası 59999 kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4348-141">For example, if one IP address on a load balancer uses probe port 59999, no other IP addresses on that load balancer can use probe port 59999.</span></span>

* <span data-ttu-id="d4348-142">Yük Dengeleyici sınırları hakkında daha fazla bilgi için bkz: **özel ön uç IP yük dengeleyici başına** altında [ağ sınırları - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="d4348-142">For information about load balancer limits, see **Private front end IP per load balancer** under [Networking Limits - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span></span>
* <span data-ttu-id="d4348-143">Kullanılabilirlik grubu sınırları hakkında daha fazla bilgi için bkz: [kısıtlamaları (kullanılabilirlik grupları)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span><span class="sxs-lookup"><span data-stu-id="d4348-143">For information about availability group limits, see [Restrictions (Availability Groups)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span></span>

<span data-ttu-id="d4348-144">Merhaba aşağıdaki betiği yeni IP adresi tooan var olan yük dengeleyici ekler.</span><span class="sxs-lookup"><span data-stu-id="d4348-144">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="d4348-145">Merhaba ILB hello dinleyicisi bağlantı noktası hello Yükü Dengeleme ön uç bağlantı noktasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="d4348-145">hello ILB uses hello listener port for hello load balancing front-end port.</span></span> <span data-ttu-id="d4348-146">Bu bağlantı noktası, SQL Server üzerinde dinleme hello bağlantı noktası olabilir.</span><span class="sxs-lookup"><span data-stu-id="d4348-146">This port can be hello port that SQL Server is listening on.</span></span> <span data-ttu-id="d4348-147">SQL Server'ın varsayılan örnekleri için başlangıç bağlantı noktası 1433'tür.</span><span class="sxs-lookup"><span data-stu-id="d4348-147">For default instances of SQL Server, hello port is 1433.</span></span> <span data-ttu-id="d4348-148">Merhaba Yük Dengeleme kuralı bir kullanılabilirlik grubu için bir kayan IP (doğrudan sunucu dönüşü) hello arka uç bağlantı noktası olacak şekilde hello aynı hello ön uç bağlantı noktası olarak gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d4348-148">hello load balancing rule for an availability group requires a floating IP (direct server return) so hello back-end port is hello same as hello front-end port.</span></span> <span data-ttu-id="d4348-149">Merhaba değişkenleri ortamınız için güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d4348-149">Update hello variables for your environment.</span></span> 

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

## <a name="configure-hello-listener"></a><span data-ttu-id="d4348-150">Merhaba dinleyicisini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d4348-150">Configure hello listener</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a><span data-ttu-id="d4348-151">SQL Server Management Studio'da Hello dinleyicisi bağlantı noktası ayarlama</span><span class="sxs-lookup"><span data-stu-id="d4348-151">Set hello listener port in SQL Server Management Studio</span></span>

1. <span data-ttu-id="d4348-152">SQL Server Management Studio'yu başlatın ve toohello birincil çoğaltma bağlanın.</span><span class="sxs-lookup"><span data-stu-id="d4348-152">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="d4348-153">Çok gidin**AlwaysOn yüksek kullanılabilirlik** | **kullanılabilirlik grupları** | **kullanılabilirlik grubu dinleyicileri**.</span><span class="sxs-lookup"><span data-stu-id="d4348-153">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span> 

1. <span data-ttu-id="d4348-154">Yük Devretme Kümesi Yöneticisi'nde oluşturulan hello dinleyici adı görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="d4348-154">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="d4348-155">Merhaba dinleyicisi adını sağ tıklatıp **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="d4348-155">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="d4348-156">Merhaba, **bağlantı noktası** kutusunda, daha önce kullandığınız $EndpointPort hello kullanarak hello hello kullanılabilirlik grubu dinleyicisinin bağlantı noktası numarası belirtin (1433 olduğu hello varsayılan), ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="d4348-156">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

## <a name="test-hello-connection-toohello-listener"></a><span data-ttu-id="d4348-157">Test hello bağlantı toohello dinleyicisi</span><span class="sxs-lookup"><span data-stu-id="d4348-157">Test hello connection toohello listener</span></span>

<span data-ttu-id="d4348-158">tootest hello bağlantısı:</span><span class="sxs-lookup"><span data-stu-id="d4348-158">tootest hello connection:</span></span>

1. <span data-ttu-id="d4348-159">RDP tooa hello SQL Server aynı sanal ağ, ancak kendi hello çoğaltma.</span><span class="sxs-lookup"><span data-stu-id="d4348-159">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="d4348-160">Bu olması hello hello kümedeki diğer SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d4348-160">This can be hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="d4348-161">Kullanım **sqlcmd** yardımcı programı tootest hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="d4348-161">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="d4348-162">Örneğin, komut dosyası izleyen hello kurar bir **sqlcmd** bağlantı toohello birincil çoğaltma Windows kimlik doğrulaması ile Merhaba dinleyicisi aracılığıyla:</span><span class="sxs-lookup"><span data-stu-id="d4348-162">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    <span data-ttu-id="d4348-163">Merhaba dinleyicisi dışında bir bağlantı noktası kullanıyorsa, varsayılan hello (1433) bağlantı noktası, başlangıç bağlantı noktası başlangıç bağlantı dizesinde belirtin.</span><span class="sxs-lookup"><span data-stu-id="d4348-163">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="d4348-164">Örneğin, hello aşağıdaki sqlcmd komut tooa dinleyicisi bağlantı noktası 1435 bağlanır:</span><span class="sxs-lookup"><span data-stu-id="d4348-164">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span> 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="d4348-165">Merhaba SQLCMD bağlantı toowhichever örneğini SQL Server konakları hello birincil çoğaltma otomatik olarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="d4348-165">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span> 

> [!NOTE]
> <span data-ttu-id="d4348-166">Belirttiğiniz başlangıç bağlantı noktası hem SQL sunucuları hello güvenlik duvarı açık olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d4348-166">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="d4348-167">Her iki sunucuyu hello kullandığınız TCP bağlantı noktası için bir gelen kuralı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d4348-167">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="d4348-168">Bkz: [Ekle veya güvenlik duvarı kuralını Düzenle](http://technet.microsoft.com/library/cc753558.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="d4348-168">See [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx) for more information.</span></span> 
> 
> 

## <a name="guidelines-and-limitations"></a><span data-ttu-id="d4348-169">Kılavuzlar ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="d4348-169">Guidelines and limitations</span></span>
<span data-ttu-id="d4348-170">Kullanılabilirlik grubu dinleyicisi iç yük dengeleyicisi kullanarak azure'da yönergeleri izleyerek hello dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="d4348-170">Note hello following guidelines on availability group listener in Azure using internal load balancer:</span></span>

* <span data-ttu-id="d4348-171">Bir iç yük dengeleyici ile size yalnızca hello içinde hello dinleyicisi gelen erişim aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="d4348-171">With an internal load balancer, you only access hello listener from within hello same virtual network.</span></span>


## <a name="for-more-information"></a><span data-ttu-id="d4348-172">Daha fazla bilgi için</span><span class="sxs-lookup"><span data-stu-id="d4348-172">For more information</span></span>
<span data-ttu-id="d4348-173">Daha fazla bilgi için bkz: [yapılandırma Always On kullanılabilirlik grubu Azure VM'de el ile](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span><span class="sxs-lookup"><span data-stu-id="d4348-173">For more information, see [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="d4348-174">PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="d4348-174">PowerShell cmdlets</span></span>
<span data-ttu-id="d4348-175">PowerShell cmdlet'leri toocreate Azure sanal makineler için bir iç yük dengeleyici aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4348-175">Use hello following PowerShell cmdlets toocreate an internal load balancer for Azure virtual machines.</span></span>

* <span data-ttu-id="d4348-176">[AzureRmLoadBalancer yeni](http://msdn.microsoft.com/library/mt619450.aspx) bir yük dengeleyici oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d4348-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) creates a load balancer.</span></span> 
* <span data-ttu-id="d4348-177">[AzureRMLoadBalancerFrontendIpConfig yeni](http://msdn.microsoft.com/library/mt603510.aspx) bir yük dengeleyici için bir ön uç IP yapılandırmasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d4348-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) creates a front-end IP configuration for a load balancer.</span></span> 
* <span data-ttu-id="d4348-178">[AzureRmLoadBalancerRuleConfig yeni](http://msdn.microsoft.com/library/mt619391.aspx) bir yük dengeleyici için bir kural yapılandırma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d4348-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) creates a rule configuration for a load balancer.</span></span> 
* <span data-ttu-id="d4348-179">[AzureRmLoadBalancerBackendAddressPoolConfig yeni](http://msdn.microsoft.com/library/mt603791.aspx) bir yük dengeleyici için arka uç adres havuzu yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d4348-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) creates a backend address pool configuration for a load balancer.</span></span> 
* <span data-ttu-id="d4348-180">[AzureRmLoadBalancerProbeConfig yeni](http://msdn.microsoft.com/library/mt603847.aspx) bir yük dengeleyici için bir araştırma yapılandırma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d4348-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) creates a probe configuration for a load balancer.</span></span>
* <span data-ttu-id="d4348-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) bir yük dengeleyici Azure kaynak grubundan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="d4348-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) removes a load balancer from an Azure resource group.</span></span>
