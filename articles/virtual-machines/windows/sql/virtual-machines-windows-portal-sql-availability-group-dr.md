---
title: "aaaSQL Server kullanılabilirlik gruplarını - Azure sanal makineleri - olağanüstü durum kurtarma | Microsoft Docs"
description: "Bu makalede nasıl tooconfigure bir SQL Server kullanılabilirlik grubu Azure sanal makinelerinde farklı bir bölgede çoğaltmasıyla açıklanmaktadır."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: df6238dc61c5a56879c75c9bf7314c618f43c0ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a><span data-ttu-id="eab37-103">Azure sanal makinelerinde farklı bölgelerdeki Always On kullanılabilirlik grubu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="eab37-103">Configure an Always On availability group on Azure virtual machines in different regions</span></span>

<span data-ttu-id="eab37-104">Bu makalede, Azure sanal makinelerinde uzak bir Azure konumda çoğaltma tooconfigure bir SQL Server Always On kullanılabilirlik Grup nasıl açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="eab37-104">This article explains how tooconfigure a SQL Server Always On availability group replica on Azure virtual machines in a remote Azure location.</span></span> <span data-ttu-id="eab37-105">Bu yapılandırma toosupport olağanüstü durum kurtarma kullanın.</span><span class="sxs-lookup"><span data-stu-id="eab37-105">Use this configuration toosupport disaster recovery.</span></span>

<span data-ttu-id="eab37-106">Bu makale, Resource Manager moduna tooAzure sanal makineleri geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="eab37-106">This article applies tooAzure Virtual Machines in Resource Manager mode.</span></span>

<span data-ttu-id="eab37-107">Merhaba aşağıdaki resimde bir kullanılabilirlik grubu ortak dağıtımı Azure sanal makinelerde gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="eab37-107">hello following image shows a common deployment of an availability group on Azure virtual machines:</span></span>

   ![Kullanılabilirlik grubu](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

<span data-ttu-id="eab37-109">Bu dağıtımda, tüm sanal makineleri bir Azure bölgesinde ' dir.</span><span class="sxs-lookup"><span data-stu-id="eab37-109">In this deployment, all virtual machines are in one Azure region.</span></span> <span data-ttu-id="eab37-110">Merhaba kullanılabilirlik grubu çoğaltmalarının zaman uyumlu işleme SQL-1 ve 2 SQL otomatik yük devretme ile olabilir.</span><span class="sxs-lookup"><span data-stu-id="eab37-110">hello availability group replicas can have synchronous commit with automatic failover on SQL-1 and SQL-2.</span></span> <span data-ttu-id="eab37-111">toobuild Bu mimarinin bkz [kullanılabilirlik grubu şablon veya öğretici](virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eab37-111">toobuild this architecture, see [Availability Group template or tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

<span data-ttu-id="eab37-112">Bu mimari Hello Azure bölgesi erişilemez duruma karşı savunmasız toodowntime olur.</span><span class="sxs-lookup"><span data-stu-id="eab37-112">This architecture is vulnerable toodowntime if hello Azure region becomes inaccessible.</span></span> <span data-ttu-id="eab37-113">tooovercome bu güvenlik açığından farklı bir Azure bölgesinde bir çoğaltma ekleyin.</span><span class="sxs-lookup"><span data-stu-id="eab37-113">tooovercome this vulnerability, add a replica in a different Azure region.</span></span> <span data-ttu-id="eab37-114">Merhaba Aşağıdaki diyagramda hello yeni mimarisi nasıl görüneceği gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="eab37-114">hello following diagram shows how hello new architecture would look:</span></span>

   ![Kullanılabilirlik grubu DR](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

<span data-ttu-id="eab37-116">Merhaba önceki diyagramda SQL 3 adlı yeni bir sanal makine gösterir.</span><span class="sxs-lookup"><span data-stu-id="eab37-116">hello preceding diagram shows a new virtual machine called SQL-3.</span></span> <span data-ttu-id="eab37-117">SQL-3 farklı bir Azure bölgesinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="eab37-117">SQL-3 is in a different Azure region.</span></span> <span data-ttu-id="eab37-118">SQL 3 toohello Windows Server Yük devretme eklenir.</span><span class="sxs-lookup"><span data-stu-id="eab37-118">SQL-3 is added toohello Windows Server Failover Cluster.</span></span> <span data-ttu-id="eab37-119">SQL 3 bir kullanılabilirlik grubu çoğaltması barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="eab37-119">SQL-3 can host an availability group replica.</span></span> <span data-ttu-id="eab37-120">Son olarak, bu hello Azure bölgesi SQL 3 için yeni bir Azure yük dengeleyici sahip dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="eab37-120">Finally, notice that hello Azure region for SQL-3 has a new Azure load balancer.</span></span>

>[!NOTE]
> <span data-ttu-id="eab37-121">Bir Azure kullanılabilirlik kümesi, sanal makine birden fazla aynı bölgede hello durumlarda gereklidir.</span><span class="sxs-lookup"><span data-stu-id="eab37-121">An Azure availability set is required when more than one virtual machine is in hello same region.</span></span> <span data-ttu-id="eab37-122">Bir sanal makine hello bölgede yalnızca, hello kullanılabilirlik kümesi gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="eab37-122">If only one virtual machine is in hello region, then hello availability set is not required.</span></span> <span data-ttu-id="eab37-123">Yalnızca bir sanal makine kullanılabilirlik kümesi oluşturma zamanında yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eab37-123">You can only place a virtual machine in an availability set at creation time.</span></span> <span data-ttu-id="eab37-124">Merhaba sanal makine zaten bir kullanılabilirlik kümesine ise, daha sonra ek bir çoğaltma için bir sanal makine ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eab37-124">If hello virtual machine is already in an availability set, you can add a virtual machine for an additional replica later.</span></span>

<span data-ttu-id="eab37-125">Bu mimaride hello çoğaltma hello uzak bölgede normalde zaman uyumsuz tamamlama kullanılabilirlik modu ve el ile yük devretme modu ile yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="eab37-125">In this architecture, hello replica in hello remote region is normally configured with asynchronous commit availability mode and manual failover mode.</span></span>

<span data-ttu-id="eab37-126">Kullanılabilirlik grubu çoğaltmalarının Azure sanal makinelerinde farklı Azure bölgelerinde olduğunda, her bölge gerektirir:</span><span class="sxs-lookup"><span data-stu-id="eab37-126">When availability group replicas are on Azure virtual machines in different Azure regions, each region requires:</span></span>

* <span data-ttu-id="eab37-127">Bir sanal ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="eab37-127">A virtual network gateway</span></span>
* <span data-ttu-id="eab37-128">Sanal ağ geçidi bağlantısı</span><span class="sxs-lookup"><span data-stu-id="eab37-128">A virtual network gateway connection</span></span>

<span data-ttu-id="eab37-129">Merhaba Aşağıdaki diyagramda hello ağları veri merkezleri arasında nasıl iletişim kurduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="eab37-129">hello following diagram shows how hello networks communicate between data centers.</span></span>

   ![Kullanılabilirlik grubu](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
><span data-ttu-id="eab37-131">Bu mimarinin Azure bölgeler arasında çoğaltılan veriler için giden veri ücret doğurur.</span><span class="sxs-lookup"><span data-stu-id="eab37-131">This architecture incurs outbound data charges for data replicated between Azure regions.</span></span> <span data-ttu-id="eab37-132">Bkz: [bant genişliği fiyatlandırma](http://azure.microsoft.com/pricing/details/bandwidth/).</span><span class="sxs-lookup"><span data-stu-id="eab37-132">See [Bandwidth Pricing](http://azure.microsoft.com/pricing/details/bandwidth/).</span></span>  

## <a name="create-remote-replica"></a><span data-ttu-id="eab37-133">Uzak bir çoğaltma oluşturma</span><span class="sxs-lookup"><span data-stu-id="eab37-133">Create remote replica</span></span>

<span data-ttu-id="eab37-134">bir uzak veri merkezindeki bir çoğaltma toocreate adımları izleyerek hello:</span><span class="sxs-lookup"><span data-stu-id="eab37-134">toocreate a replica in a remote data center, do hello following steps:</span></span>

1. <span data-ttu-id="eab37-135">[Merhaba yeni bölgede bir sanal ağ oluşturma](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="eab37-135">[Create a virtual network in hello new region](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

1. <span data-ttu-id="eab37-136">[Hello Azure portalını kullanarak VNet-VNet bağlantı yapılandırma](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="eab37-136">[Configure a VNet-to-VNet connection using hello Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span></span>

   >[!NOTE]
   ><span data-ttu-id="eab37-137">Bazı durumlarda, toouse PowerShell toocreate hello VNet-VNet bağlantı olabilir.</span><span class="sxs-lookup"><span data-stu-id="eab37-137">In some cases, you may have toouse PowerShell toocreate hello VNet-to-VNet connection.</span></span> <span data-ttu-id="eab37-138">Örneğin, farklı Azure hesapları kullanıyorsanız hello bağlantı hello Portalı'nda yapılandıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="eab37-138">For example, if you use different Azure accounts you cannot configure hello connection in hello portal.</span></span> <span data-ttu-id="eab37-139">Bu durumda bakın, [hello Azure portal yapılandırma bir VNet-VNet bağlantısı kullanarak](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="eab37-139">In this case see, [Configure a VNet-to-VNet connection using hello Azure portal](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

1. <span data-ttu-id="eab37-140">[Bir etki alanı denetleyicisi hello yeni bölge Oluştur](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="eab37-140">[Create a domain controller in hello new region](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span></span>

   <span data-ttu-id="eab37-141">Merhaba birincil sitedeki Hello etki alanı denetleyicisinin kullanılabilir değilse, bu etki alanı denetleyicisi kimlik doğrulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="eab37-141">This domain controller provides authentication if hello domain controller in hello primary site is not available.</span></span>

1. <span data-ttu-id="eab37-142">[Bir SQL Server sanal makine hello yeni bölge Oluştur](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="eab37-142">[Create a SQL Server virtual machine in hello new region](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

1. <span data-ttu-id="eab37-143">[Bir Azure yük dengeleyici hello ağ hello yeni bölge oluşturma](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="eab37-143">[Create an Azure load balancer in hello network on hello new region](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

   <span data-ttu-id="eab37-144">Bu yük dengeleyici gerekir:</span><span class="sxs-lookup"><span data-stu-id="eab37-144">This load balancer must:</span></span>

   - <span data-ttu-id="eab37-145">Olması yeni bir sanal makine hello gibi aynı ağ ve alt ağ hello.</span><span class="sxs-lookup"><span data-stu-id="eab37-145">Be in hello same network and subnet as hello new virtual machine.</span></span>
   - <span data-ttu-id="eab37-146">Merhaba kullanılabilirlik grubu dinleyicisi için statik bir IP adresi vardır.</span><span class="sxs-lookup"><span data-stu-id="eab37-146">Have a static IP address for hello availability group listener.</span></span>
   - <span data-ttu-id="eab37-147">Yük Dengeleyici hello gibi Hello sanal makinelerin aynı bölgede hello yalnızca oluşan bir arka uç havuzu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="eab37-147">Include a backend pool consisting of only hello virtual machines in hello same region as hello load balancer.</span></span>
   - <span data-ttu-id="eab37-148">Bir TCP bağlantı noktası araştırma belirli toohello IP adresi kullanın.</span><span class="sxs-lookup"><span data-stu-id="eab37-148">Use a TCP port probe specific toohello IP address.</span></span>
   - <span data-ttu-id="eab37-149">Bir Yük Dengeleme kuralı belirli toohello SQL Server hello içinde sahip aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="eab37-149">Have a load balancing rule specific toohello SQL Server in hello same region.</span></span>  

1. <span data-ttu-id="eab37-150">[Yük Devretme Kümelemesi özelliğini toohello ekleme yeni SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="eab37-150">[Add Failover Clustering feature toohello new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

1. <span data-ttu-id="eab37-151">[Merhaba yeni SQL Server toohello etki alanına](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="eab37-151">[Join hello new SQL Server toohello domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

1. <span data-ttu-id="eab37-152">[Bir etki alanı hesabı Hello yeni SQL Server hizmet hesabı toouse ayarlamanız](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span><span class="sxs-lookup"><span data-stu-id="eab37-152">[Set hello new SQL Server service account toouse a domain account](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span></span>

1. <span data-ttu-id="eab37-153">[Merhaba yeni SQL Server toohello Windows Server Yük devretme eklemek](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span><span class="sxs-lookup"><span data-stu-id="eab37-153">[Add hello new SQL Server toohello Windows Server Failover Cluster](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span></span>

1. <span data-ttu-id="eab37-154">Bir IP adresi kaynağı hello kümede oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eab37-154">Create an IP address resource on hello cluster.</span></span>

   <span data-ttu-id="eab37-155">Yük Devretme Kümesi Yöneticisi'nde hello IP adresi kaynağı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eab37-155">You can create hello IP address resource in Failover Cluster Manager.</span></span> <span data-ttu-id="eab37-156">Merhaba kullanılabilirlik grubu role sağ tıklayın, **kaynak ekleme**, **daha kaynakları**, tıklatıp **IP adresi**.</span><span class="sxs-lookup"><span data-stu-id="eab37-156">Right-click hello availability group role, click **Add Resource**, **More Resources**, and click **IP Address**.</span></span>

   ![IP adresi oluşturun](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   <span data-ttu-id="eab37-158">Bu IP adresi gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="eab37-158">Configure this IP address as follows:</span></span>

   - <span data-ttu-id="eab37-159">Merhaba ağ hello uzak veri merkezinden kullanın.</span><span class="sxs-lookup"><span data-stu-id="eab37-159">Use hello network from hello remote data center.</span></span>
   - <span data-ttu-id="eab37-160">Başlangıç IP adresi hello yeni Azure yük dengeleyiciden atayın.</span><span class="sxs-lookup"><span data-stu-id="eab37-160">Assign hello IP address from hello new Azure load balancer.</span></span> 

1. <span data-ttu-id="eab37-161">Üzerinde yeni SQL Server SQL Server Yapılandırma Yöneticisi ' nde hello [Always On kullanılabilirlik grupları etkinleştirmek](http://msdn.microsoft.com/library/ff878259.aspx).</span><span class="sxs-lookup"><span data-stu-id="eab37-161">On hello new SQL Server in SQL Server Configuration Manager, [enable Always On Availability Groups](http://msdn.microsoft.com/library/ff878259.aspx).</span></span>

1. <span data-ttu-id="eab37-162">[Açık güvenlik duvarı bağlantı noktaları hello yeni SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="eab37-162">[Open firewall ports on hello new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

   <span data-ttu-id="eab37-163">başlangıç bağlantı noktası numaralarını tooopen ihtiyacınız ortamınıza bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="eab37-163">hello port numbers you need tooopen depend on your environment.</span></span> <span data-ttu-id="eab37-164">Yansıtma uç noktası ve Azure hello açık bağlantı noktalarını dengeleyici durum araştırması yükleyin.</span><span class="sxs-lookup"><span data-stu-id="eab37-164">Open ports for hello mirroring endpoint and Azure load balancer health probe.</span></span>

1. <span data-ttu-id="eab37-165">[Bir çoğaltma toohello kullanılabilirlik grubu üzerinde hello ekleyin yeni SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span><span class="sxs-lookup"><span data-stu-id="eab37-165">[Add a replica toohello availability group on hello new SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span></span>

   <span data-ttu-id="eab37-166">Uzak bir Azure bölgesindeki bir çoğaltma için el ile yük devretme ile zaman uyumsuz çoğaltma için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="eab37-166">For a replica in a remote Azure region, set it for asynchronous replication with manual failover.</span></span>  

1. <span data-ttu-id="eab37-167">Başlangıç IP adresi kaynağı hello dinleyicisi istemci erişim noktası (ağ adı) küme için bağımlılık olarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="eab37-167">Add hello IP address resource as a dependency for hello listener client access point (network name) cluster.</span></span>

   <span data-ttu-id="eab37-168">Merhaba aşağıdaki ekran görüntüsü düzgün şekilde yapılandırılmış bir IP adresi küme kaynağı gösterir:</span><span class="sxs-lookup"><span data-stu-id="eab37-168">hello following screenshot shows a properly configured IP address cluster resource:</span></span>

   ![Kullanılabilirlik grubu](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   ><span data-ttu-id="eab37-170">Merhaba küme kaynak grubu iki IP adresi içerir.</span><span class="sxs-lookup"><span data-stu-id="eab37-170">hello cluster resource group includes both IP addresses.</span></span> <span data-ttu-id="eab37-171">Bağımlılıklar hello dinleyicisi istemci erişim noktası için her iki IP adresleridir.</span><span class="sxs-lookup"><span data-stu-id="eab37-171">Both IP addresses are dependencies for hello listener client access point.</span></span> <span data-ttu-id="eab37-172">Kullanım hello **veya** hello küme bağımlılık yapılandırmasında işleci.</span><span class="sxs-lookup"><span data-stu-id="eab37-172">Use hello **OR** operator in hello cluster dependency configuration.</span></span>

1. <span data-ttu-id="eab37-173">[PowerShell'de hello küme parametreleri ayarlamak](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span><span class="sxs-lookup"><span data-stu-id="eab37-173">[Set hello cluster parameters in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span></span>

<span data-ttu-id="eab37-174">Merhaba küme ağ adı, IP adresi ve hello yeni bölgede hello yük dengeleyici üzerinde yapılandırılmış yoklama bağlantı noktası ile Merhaba PowerShell betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="eab37-174">Run hello PowerShell script with hello cluster network name, IP address, and probe port that you configured on hello load balancer in hello new region.</span></span>

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster name for hello network in hello new region (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "<IPResourceName>" # hello cluster name for hello new IP Address resource.
   $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB) in hello new region. This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <nnnnn> # hello probe port you set on hello ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a><span data-ttu-id="eab37-175">Birden çok alt ağlar için kümesi bağlantı</span><span class="sxs-lookup"><span data-stu-id="eab37-175">Set connection for multiple subnets</span></span>

<span data-ttu-id="eab37-176">Merhaba çoğaltma hello uzak veri merkezinde hello kullanılabilirlik grubunun parçası olan ancak farklı bir alt ağda değil.</span><span class="sxs-lookup"><span data-stu-id="eab37-176">hello replica in hello remote data center is part of hello availability group but it is in a different subnet.</span></span> <span data-ttu-id="eab37-177">Bu çoğaltma hello birincil çoğaltma olursa, uygulama bağlantı zaman aşımları ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="eab37-177">If this replica becomes hello primary replica, application connection time-outs may occur.</span></span> <span data-ttu-id="eab37-178">Bu davranış olduğu hello bir şirket içi kullanılabilirlik grubunda birden çok alt ağ dağıtımı ile aynı.</span><span class="sxs-lookup"><span data-stu-id="eab37-178">This behavior is hello same as an on-premises availability group in a multi-subnet deployment.</span></span> <span data-ttu-id="eab37-179">istemci uygulamaları tooallow bağlantılarından hello istemci bağlantısını güncelleştirin veya hello küme ağ adı kaynağına bağlı önbelleğe alma ad çözümlemesi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eab37-179">tooallow connections from client applications, either update hello client connection or configure name resolution caching on hello cluster network name resource.</span></span>

<span data-ttu-id="eab37-180">Tercihen Merhaba istemci bağlantı dizeleri tooset güncelleştirme `MultiSubnetFailover=Yes`.</span><span class="sxs-lookup"><span data-stu-id="eab37-180">Preferably, update hello client connection strings tooset `MultiSubnetFailover=Yes`.</span></span> <span data-ttu-id="eab37-181">Bkz: [MultiSubnetFailover ile bağlanma](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="eab37-181">See [Connecting With MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span></span>

<span data-ttu-id="eab37-182">Merhaba bağlantı dizeleri değiştirilemiyor, ad çözümlemesi önbelleğe alma yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eab37-182">If you cannot modify hello connection strings, you can configure name resolution caching.</span></span> <span data-ttu-id="eab37-183">Bkz: [birden çok alt ağ kullanılabilirlik grubundaki zaman aşımları](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span><span class="sxs-lookup"><span data-stu-id="eab37-183">See [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span></span>

## <a name="fail-over-tooremote-region"></a><span data-ttu-id="eab37-184">Tooremote bölge başarısız</span><span class="sxs-lookup"><span data-stu-id="eab37-184">Fail over tooremote region</span></span>

<span data-ttu-id="eab37-185">tootest dinleyici bağlantı toohello uzak bölge, hello çoğaltma toohello uzak bölge başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="eab37-185">tootest listener connectivity toohello remote region, you can fail over hello replica toohello remote region.</span></span> <span data-ttu-id="eab37-186">Merhaba çoğaltma zaman uyumsuz olsa da, yük devretme savunmasız toopotential veri kaybı olmuş.</span><span class="sxs-lookup"><span data-stu-id="eab37-186">While hello replica is asynchronous, failover is vulnerable toopotential data loss.</span></span> <span data-ttu-id="eab37-187">veri kaybı olmadan üzerinden toofail hello kullanılabilirlik modu toosynchronous değiştirmek ve hello yük devretme modu tooautomatic ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="eab37-187">toofail over without data loss, change hello availability mode toosynchronous and set hello failover mode tooautomatic.</span></span> <span data-ttu-id="eab37-188">Merhaba aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="eab37-188">Use hello following steps:</span></span>

1. <span data-ttu-id="eab37-189">İçinde **Nesne Gezgini**, toohello hello birincil çoğaltmayı barındıran SQL Server örneğine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="eab37-189">In **Object Explorer**, connect toohello instance of SQL Server that hosts hello primary replica.</span></span>
1. <span data-ttu-id="eab37-190">Altında **AlwaysOn Kullanılabilirlik grupları**, **kullanılabilirlik grupları**, kullanılabilirlik grubunuzun sağ tıklatın ve **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="eab37-190">Under **AlwaysOn Availability Groups**, **Availability Groups**, right-click your availability group and click **Properties**.</span></span>
1. <span data-ttu-id="eab37-191">Merhaba üzerinde **genel** sayfasında **kullanılabilirlik çoğaltmalarının**, kümesi hello ikincil çoğaltmasında hello DR sitesi toouse **zaman uyumlu yürütme** kullanılabilirlik modu ve **Otomatik** yük devretme modu.</span><span class="sxs-lookup"><span data-stu-id="eab37-191">On hello **General** page, under **Availability Replicas**, set hello secondary replica in hello DR site toouse **Synchronous Commit** availability mode and **Automatic** failover mode.</span></span>
1. <span data-ttu-id="eab37-192">Yüksek kullanılabilirlik için birincil, çoğaltma olarak aynı sitedeki bir ikincil çoğaltma varsa, bu kopya çok kümesi**zaman uyumsuz tamamlama** ve **el ile**.</span><span class="sxs-lookup"><span data-stu-id="eab37-192">If you have a secondary replica in same site as your primary replica for high availability, set this replica too**Asynchronous Commit** and **Manual**.</span></span>
1. <span data-ttu-id="eab37-193">Tamam'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eab37-193">Click OK.</span></span>
1. <span data-ttu-id="eab37-194">İçinde **Object Explorer**, hello kullanılabilirlik grubuna sağ tıklayın ve **Göster Pano**.</span><span class="sxs-lookup"><span data-stu-id="eab37-194">In **Object Explorer**, right-click hello availability group, and click **Show Dashboard**.</span></span>
1. <span data-ttu-id="eab37-195">Bu hello Hello Panoda doğrulayın hello DR sitesi üzerinde çoğaltma eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="eab37-195">On hello dashboard, verify that hello replica on hello DR site is synchronized.</span></span>
1. <span data-ttu-id="eab37-196">İçinde **Object Explorer**, hello kullanılabilirlik grubuna sağ tıklayın ve **yük devretme...** . SQL Server Management stüdyoları Sihirbazı toofail üzerinden SQL Server açar.</span><span class="sxs-lookup"><span data-stu-id="eab37-196">In **Object Explorer**, right-click hello availability group, and click **Failover...**. SQL Server Management Studios opens a wizard toofail over SQL Server.</span></span>  
1. <span data-ttu-id="eab37-197">Tıklatın **sonraki**ve select hello SQL Server örneğinde hello DR sitesi.</span><span class="sxs-lookup"><span data-stu-id="eab37-197">Click **Next**, and select hello SQL Server instance in hello DR site.</span></span> <span data-ttu-id="eab37-198">Tıklatın **sonraki** yeniden.</span><span class="sxs-lookup"><span data-stu-id="eab37-198">Click **Next** again.</span></span>
1. <span data-ttu-id="eab37-199">Merhaba DR sitesi toohello SQL Server örneğinde bağlanmak ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="eab37-199">Connect toohello SQL Server instance in hello DR site and click **Next**.</span></span>
1. <span data-ttu-id="eab37-200">Merhaba üzerinde **Özet** sayfasında hello ayarlarını doğrulayın ve tıklayın **son**.</span><span class="sxs-lookup"><span data-stu-id="eab37-200">On hello **Summary** page, verify hello settings and click **Finish**.</span></span>

<span data-ttu-id="eab37-201">Bağlantı test ediliyor sonra hello birincil çoğaltma geri tooyour birincil veri merkezi ve hello kullanılabilirlik modu geri tootheir normal işletim ayarlar taşıyın.</span><span class="sxs-lookup"><span data-stu-id="eab37-201">After testing connectivity, move hello primary replica back tooyour primary data center and set hello availability mode back tootheir normal operating settings.</span></span> <span data-ttu-id="eab37-202">Merhaba aşağıdaki tabloda bu belgede açıklanan hello mimarisi için normal işletimsel ayarları hello gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="eab37-202">hello following table shows hello normal operational settings for hello architecture described in this document:</span></span>

| <span data-ttu-id="eab37-203">Konum</span><span class="sxs-lookup"><span data-stu-id="eab37-203">Location</span></span> | <span data-ttu-id="eab37-204">Sunucu örneği</span><span class="sxs-lookup"><span data-stu-id="eab37-204">Server Instance</span></span> | <span data-ttu-id="eab37-205">Rol</span><span class="sxs-lookup"><span data-stu-id="eab37-205">Role</span></span> | <span data-ttu-id="eab37-206">Kullanılabilirlik modu</span><span class="sxs-lookup"><span data-stu-id="eab37-206">Availability Mode</span></span> | <span data-ttu-id="eab37-207">Yük devretme modu</span><span class="sxs-lookup"><span data-stu-id="eab37-207">Failover Mode</span></span>
| ----- | ----- | ----- | ----- | -----
| <span data-ttu-id="eab37-208">Birincil veri merkezi</span><span class="sxs-lookup"><span data-stu-id="eab37-208">Primary data center</span></span> | <span data-ttu-id="eab37-209">SQL-1</span><span class="sxs-lookup"><span data-stu-id="eab37-209">SQL-1</span></span> | <span data-ttu-id="eab37-210">Birincil</span><span class="sxs-lookup"><span data-stu-id="eab37-210">Primary</span></span> | <span data-ttu-id="eab37-211">Zaman uyumlu</span><span class="sxs-lookup"><span data-stu-id="eab37-211">Synchronous</span></span> | <span data-ttu-id="eab37-212">Otomatik</span><span class="sxs-lookup"><span data-stu-id="eab37-212">Automatic</span></span>
| <span data-ttu-id="eab37-213">Birincil veri merkezi</span><span class="sxs-lookup"><span data-stu-id="eab37-213">Primary data center</span></span> | <span data-ttu-id="eab37-214">SQL-2</span><span class="sxs-lookup"><span data-stu-id="eab37-214">SQL-2</span></span> | <span data-ttu-id="eab37-215">İkincil</span><span class="sxs-lookup"><span data-stu-id="eab37-215">Secondary</span></span> | <span data-ttu-id="eab37-216">Zaman uyumlu</span><span class="sxs-lookup"><span data-stu-id="eab37-216">Synchronous</span></span> | <span data-ttu-id="eab37-217">Otomatik</span><span class="sxs-lookup"><span data-stu-id="eab37-217">Automatic</span></span>
| <span data-ttu-id="eab37-218">İkincil ya da uzak veri merkezi</span><span class="sxs-lookup"><span data-stu-id="eab37-218">Secondary or remote data center</span></span> | <span data-ttu-id="eab37-219">SQL-3</span><span class="sxs-lookup"><span data-stu-id="eab37-219">SQL-3</span></span> | <span data-ttu-id="eab37-220">İkincil</span><span class="sxs-lookup"><span data-stu-id="eab37-220">Secondary</span></span> | <span data-ttu-id="eab37-221">Zaman uyumsuz</span><span class="sxs-lookup"><span data-stu-id="eab37-221">Asynchronous</span></span> | <span data-ttu-id="eab37-222">El ile</span><span class="sxs-lookup"><span data-stu-id="eab37-222">Manual</span></span>


### <a name="more-information-about-planned-and-forced-manual-failover"></a><span data-ttu-id="eab37-223">Planlanan ve zorunlu el ile yük devretme hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="eab37-223">More information about planned and forced manual failover</span></span>

<span data-ttu-id="eab37-224">Daha fazla bilgi için aşağıdaki konularda hello bakın:</span><span class="sxs-lookup"><span data-stu-id="eab37-224">For more information, see hello following topics:</span></span>

- [<span data-ttu-id="eab37-225">Bir kullanılabilirlik grubu (SQL Server) planlanmış bir el ile yük gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="eab37-225">Perform a Planned Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/hh231018.aspx)
- [<span data-ttu-id="eab37-226">Bir kullanılabilirlik grubu (SQL Server) zorla el ile yük devretme gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="eab37-226">Perform a Forced Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a><span data-ttu-id="eab37-227">Ek bağlantılar</span><span class="sxs-lookup"><span data-stu-id="eab37-227">Additional Links</span></span>

* [<span data-ttu-id="eab37-228">Always On kullanılabilirlik grupları</span><span class="sxs-lookup"><span data-stu-id="eab37-228">Always On Availability Groups</span></span>](http://msdn.microsoft.com/library/hh510230.aspx)
* [<span data-ttu-id="eab37-229">Azure sanal makineler</span><span class="sxs-lookup"><span data-stu-id="eab37-229">Azure Virtual Machines</span></span>](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [<span data-ttu-id="eab37-230">Azure yük dengeleyicileri</span><span class="sxs-lookup"><span data-stu-id="eab37-230">Azure Load Balancers</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [<span data-ttu-id="eab37-231">Azure kullanılabilirlik kümeleri</span><span class="sxs-lookup"><span data-stu-id="eab37-231">Azure Availability Sets</span></span>](../manage-availability.md)
