---
title: aaaTroubleshoot yollar - PowerShell | Microsoft Docs
description: "Azure PowerShell kullanarak hello Azure Resource Manager dağıtım modelinde tootroubleshoot nasıl yönlendirir öğrenin."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 7a07806df5c1d0caee921187e6ad29f6755ab535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a><span data-ttu-id="b24fd-103">Azure PowerShell kullanarak yolları sorun giderme</span><span class="sxs-lookup"><span data-stu-id="b24fd-103">Troubleshoot routes using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b24fd-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b24fd-104">Azure Portal</span></span>](virtual-network-routes-troubleshoot-portal.md)
> * [<span data-ttu-id="b24fd-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b24fd-105">PowerShell</span></span>](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="b24fd-106">Azure sanal makine (VM) gelen ağ bağlantısı sorunları tooor karşılaşıyorsanız, yolları VM trafik akışına etkiliyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="b24fd-106">If you are experiencing network connectivity issues tooor from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="b24fd-107">Bu makalede rotalar toohelp daha fazla sorun giderme için tanılama özelliklerine genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="b24fd-107">This article provides an overview of diagnostics capabilities for routes toohelp troubleshoot further.</span></span>

<span data-ttu-id="b24fd-108">Yönlendirme tabloları alt ağ ile ilişkili ve tüm ağ arabirimlerindeki (NIC) bu alt ağdaki etkili olur.</span><span class="sxs-lookup"><span data-stu-id="b24fd-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="b24fd-109">şu yolların türlerini hello uygulanan tooeach ağ arabirimi olabilir:</span><span class="sxs-lookup"><span data-stu-id="b24fd-109">hello following types of routes can be applied tooeach network interface:</span></span>

* <span data-ttu-id="b24fd-110">**Sistem yolları:** varsayılan olarak, yerel VNet trafiği, VPN ağ geçitleri üzerinden şirket içi trafik ve Internet trafiğini izin sistem yönlendirme tabloları bir Azure sanal ağı (VNet) içinde oluşturulan her alt ağ vardır.</span><span class="sxs-lookup"><span data-stu-id="b24fd-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="b24fd-111">Sistem yolları da eşlenmiş Vnet'ler için mevcut.</span><span class="sxs-lookup"><span data-stu-id="b24fd-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="b24fd-112">**BGP yolları:** toonetwork arabirimleri ExpressRoute veya siteden siteye VPN bağlantıları üzerinden yayılır.</span><span class="sxs-lookup"><span data-stu-id="b24fd-112">**BGP routes:** Propagated toonetwork interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="b24fd-113">Merhaba okuyarak BGP yönlendirme hakkında daha fazla bilgi [VPN gateways ile BGP'ye](../vpn-gateway/vpn-gateway-bgp-overview.md) ve [ExpressRoute genel bakış](../expressroute/expressroute-introduction.md) makaleleri.</span><span class="sxs-lookup"><span data-stu-id="b24fd-113">Learn more about BGP routing by reading hello [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="b24fd-114">**Kullanıcı tanımlı yolları (UDR):** ağ sanal Gereçleri kullanıyorsanız veya zorlamalı tünel olan trafik tooan içi ağınıza bir siteden siteye VPN aracılığıyla alt yol tablosu ile ilişkili kullanıcı tanımlı yollar (Udr'ler) olabilir.</span><span class="sxs-lookup"><span data-stu-id="b24fd-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic tooan on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="b24fd-115">İle Udr'ler bilmiyorsanız hello okuma [kullanıcı tanımlı yollar](virtual-networks-udr-overview.md#user-defined-routes) makalesi.</span><span class="sxs-lookup"><span data-stu-id="b24fd-115">If you're not familiar with UDRs, read hello [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="b24fd-116">Merhaba ile uygulanan tooa ağ arabirimi, olabilecek çeşitli yollar, zor toodetermine toplama hangi rotalar etkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="b24fd-116">With hello various routes that can be applied tooa network interface, it can be difficult toodetermine which aggregate routes are effective.</span></span> <span data-ttu-id="b24fd-117">toohelp VM ağ bağlantısı sorunlarını giderme, bir ağ arabirimi için tüm hello etkili yollar hello Azure Resource Manager dağıtım modelinde görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b24fd-117">toohelp troubleshoot VM network connectivity, you can view all hello effective routes for a network interface in hello Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="b24fd-118">Etkin yollar tootroubleshoot VM trafik akışı kullanma</span><span class="sxs-lookup"><span data-stu-id="b24fd-118">Using Effective Routes tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="b24fd-119">Bu makalede nasıl tootroubleshoot hello etkili bir ağ arabirimi için yönlendiren bir örnek tooillustrate olarak senaryo aşağıdaki hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="b24fd-119">This article uses hello following scenario as an example tooillustrate how tootroubleshoot hello effective routes for a network interface:</span></span>

<span data-ttu-id="b24fd-120">Bir VM'yi (*VM1*) toohello VNet bağlı (*VNet1*, öneki: 10.9.0.0/16) tooconnect tooa VM(VM3) yeni vnet'teki başarısız (*VNet3*, 10.10.0.0/16 öneki).</span><span class="sxs-lookup"><span data-stu-id="b24fd-120">A VM (*VM1*) connected toohello VNet (*VNet1*, prefix: 10.9.0.0/16) fails tooconnect tooa VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="b24fd-121">Uygulanan tooVM1 nıc1 ağ arabirimi bağlı toohello VM Udr'ler ya da BGP yolları, yalnızca sistem yolları uygulanır vardır.</span><span class="sxs-lookup"><span data-stu-id="b24fd-121">There are no UDRs or BGP routes applied tooVM1-NIC1 network interface connected toohello VM, only system routes are applied.</span></span>

<span data-ttu-id="b24fd-122">Bu makalede nasıl toodetermine hello neden hello bağlantı hatası, Azure kaynak yönetimi dağıtım modelinde etkili yollar özelliği kullanarak, açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b24fd-122">This article explains how toodetermine hello cause of hello connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="b24fd-123">Yalnızca sistem yolları Hello örnek kullanıyor, ancak aynı adımları hello kullanılan toodetermine herhangi bir rota türü gelen ve giden bağlantı hataları olabilir.</span><span class="sxs-lookup"><span data-stu-id="b24fd-123">While hello example uses only system routes, hello same steps can be used toodetermine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> <span data-ttu-id="b24fd-124">VM bağlı birden çok NIC varsa, her hello NIC toodiagnose ağ bağlantısı sorunları tooand bir VM'den etkili yolları denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b24fd-124">If your VM has more than one NIC attached, check effective routes for each of hello NICs toodiagnose network connectivity issues tooand from a VM.</span></span>
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="b24fd-125">Bir sanal makine için Görünüm etkili yolları</span><span class="sxs-lookup"><span data-stu-id="b24fd-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="b24fd-126">uygulanan tooa VM, aşağıdaki adımları tam hello olan toosee hello toplama yollar:</span><span class="sxs-lookup"><span data-stu-id="b24fd-126">toosee hello aggregate routes that are applied tooa VM, complete hello following steps:</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="b24fd-127">Bir ağ arabirimi için Görünüm etkili yolları</span><span class="sxs-lookup"><span data-stu-id="b24fd-127">View effective routes for a network interface</span></span>
<span data-ttu-id="b24fd-128">uygulanan tooa ağ arabirimi, aşağıdaki adımları tam hello olan toosee hello toplama yollar:</span><span class="sxs-lookup"><span data-stu-id="b24fd-128">toosee hello aggregate routes that are applied tooa network interface, complete hello following steps:</span></span>

1. <span data-ttu-id="b24fd-129">Bir Azure PowerShell oturumu ve oturum açma tooAzure başlatın.</span><span class="sxs-lookup"><span data-stu-id="b24fd-129">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="b24fd-130">Azure PowerShell ile bilmiyorsanız hello okuma [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) makalesi.</span><span class="sxs-lookup"><span data-stu-id="b24fd-130">If you’re not familiar with Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="b24fd-131">Merhaba aşağıdaki komut döndürür tüm yollar uygulanan tooa ağ arabirimi adlı *VM1 nıc1* hello kaynak grubunda *RG1*.</span><span class="sxs-lookup"><span data-stu-id="b24fd-131">hello following command returns all routes applied tooa network interface named *VM1-NIC1* in hello resource group *RG1*.</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="b24fd-132">Bir ağ arabirimi hello adını bilmiyorsanız, bir kaynak group.* tüm ağ arabirimlerini komut tooretrieve hello adlarını aşağıdaki hello yazın</span><span class="sxs-lookup"><span data-stu-id="b24fd-132">If you don’t know hello name of a network interface, type hello following command tooretrieve hello names of all network interfaces in a resource group.*</span></span>
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   <span data-ttu-id="b24fd-133">Merhaba aşağıdaki çıkış benzer toohello çıkış NIC bağlı her uygulanan rota toohello alt hello arar:</span><span class="sxs-lookup"><span data-stu-id="b24fd-133">hello following output looks similar toohello output for each route applied toohello subnet hello NIC is connected to:</span></span>
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   <span data-ttu-id="b24fd-134">Merhaba çıktısında Hello aşağıdakilere dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="b24fd-134">Notice hello following in hello output:</span></span>
   
   * <span data-ttu-id="b24fd-135">**Ad**: açıkça belirtilen, kullanıcı tanımlı yollar için sürece hello etkili rotanın adı boş olabilir.</span><span class="sxs-lookup"><span data-stu-id="b24fd-135">**Name**: Name of hello effective route may be empty, unless explicitly specified, for user-defined routes.</span></span> 
   * <span data-ttu-id="b24fd-136">**Durum**: hello etkin yönlendirme durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="b24fd-136">**State**: Indicates state of hello effective route.</span></span> <span data-ttu-id="b24fd-137">"Active" veya "Geçersiz" olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b24fd-137">Possible values are "Active" or "Invalid"</span></span>
   * <span data-ttu-id="b24fd-138">**AddressPrefixes**: CIDR gösteriminde hello etkin yönlendirme hello adres öneki belirtir.</span><span class="sxs-lookup"><span data-stu-id="b24fd-138">**AddressPrefixes**: Specifies hello address prefix of hello effective route in CIDR notation.</span></span> 
   * <span data-ttu-id="b24fd-139">**nextHopType**: yol verilen hello için sonraki atlama hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="b24fd-139">**nextHopType**: Indicates hello next hop for hello given route.</span></span> <span data-ttu-id="b24fd-140">Olası değerler şunlardır: *değerinin VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, veya *Null*.</span><span class="sxs-lookup"><span data-stu-id="b24fd-140">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="b24fd-141">Değerini *Null* için **nextHopType** bir UDR geçersiz bir yol gösteriyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="b24fd-141">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="b24fd-142">Örneğin, varsa **nextHopType** olan *değerinin VirtualAppliance* ve hello ağ sanal gereç VM sağlanan çalışıyor durumda değil.</span><span class="sxs-lookup"><span data-stu-id="b24fd-142">For example, if **nextHopType** is *VirtualAppliance* and hello network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="b24fd-143">Varsa **nextHopType** olan *VPNGateway* ve VNet verilen hello sağlanan/çalışan ağ geçidi yok ise, hello yol geçersiz hale gelebilir.</span><span class="sxs-lookup"><span data-stu-id="b24fd-143">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in hello given VNet, hello route may become invalid.</span></span>
   * <span data-ttu-id="b24fd-144">**Nexthopıpaddress**: hello etkili yolunun sonraki atlama hello hello IP adresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="b24fd-144">**NextHopIpAddress**: Specifies hello IP address of hello next hop of hello effective route.</span></span>
   
   <span data-ttu-id="b24fd-145">Merhaba aşağıdaki komut hello yolları daha kolay bir tooview tabloda döndürür:</span><span class="sxs-lookup"><span data-stu-id="b24fd-145">hello following command returns hello routes in an easier tooview table:</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   <span data-ttu-id="b24fd-146">Merhaba aşağıdaki çıkış daha önce açıklanan hello senaryosu için alınan hello çıkış bazıları verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b24fd-146">hello following output is some of hello output received for hello scenario described previously:</span></span>
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. <span data-ttu-id="b24fd-147">Listelenen rota toohello yok *WestUS VNet3* VNet (10.10.0.0/16)** gelen önek *WestUS VNet1* (10.9.0.0/16 önek) hello önceki adımdaki hello çıkışı.</span><span class="sxs-lookup"><span data-stu-id="b24fd-147">There is no route listed toohello *WestUS-VNet3* VNet (Prefix 10.10.0.0/16)** from *WestUS-VNet1* (Prefix 10.9.0.0/16) in hello output from hello previous step.</span></span> <span data-ttu-id="b24fd-148">Hello resim aşağıdaki gösterildiği gibi VNet eşleme bağlantısı ile Merhaba hello *WestUS VNet3* VNet olan hello *bağlantı kesildi* durumu.</span><span class="sxs-lookup"><span data-stu-id="b24fd-148">As shown in hello following picture, hello VNet peering link with hello *WestUS-VNet3* VNet is in hello *Disconnected* state.</span></span>
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    <span data-ttu-id="b24fd-149">Merhaba çift yönlü bağlantı hello eşliği bozuk için açıklayan neden VM1 hello tooVM3 bağlanamadı *WestUS VNet3* VNet.</span><span class="sxs-lookup"><span data-stu-id="b24fd-149">hello bi-directional link for hello peering is broken, which explains why VM1 could not connect tooVM3 in hello *WestUS-VNet3* VNet.</span></span> <span data-ttu-id="b24fd-150">Çift yönlü bir VNet eşleme bağlantısı yeniden için Kurulum *WestUS VNet1* ve *WestUS VNet3* sanal ağlar.</span><span class="sxs-lookup"><span data-stu-id="b24fd-150">Setup a bi-directional VNet peering link again for *WestUS-VNet1* and *WestUS-VNet3* VNets.</span></span> <span data-ttu-id="b24fd-151">Merhaba VNet eşleme bağlantısı doğru kurulduktan sonra döndürülen hello çıktı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="b24fd-151">hello output returned after hello VNet peering link is correctly established follows:</span></span>
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    <span data-ttu-id="b24fd-152">Ekleyebilir, hello sorunu belirledikten sonra kaldırmak veya yolları değiştirmek ve tabloları rota.</span><span class="sxs-lookup"><span data-stu-id="b24fd-152">Once you determine hello issue, you can add, remove, or change routes and route tables.</span></span> <span data-ttu-id="b24fd-153">Merhaba komutu toosee hello kullanılan komutlar toodo listesini şekilde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="b24fd-153">Type hello following command toosee a list of hello commands used toodo so:</span></span>
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a><span data-ttu-id="b24fd-154">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="b24fd-154">Considerations</span></span>
<span data-ttu-id="b24fd-155">Merhaba yolların listesini gözden geçirirken aklınızda birkaç şey tookeep döndürdü:</span><span class="sxs-lookup"><span data-stu-id="b24fd-155">A few things tookeep in mind when reviewing hello list of routes returned:</span></span>

* <span data-ttu-id="b24fd-156">Yönlendirme üzerinde en uzun ön ek eşleşmesi (LPM) Udr'ler arasında temel BGP ve sistem yolları.</span><span class="sxs-lookup"><span data-stu-id="b24fd-156">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="b24fd-157">Hello sahip birden fazla yol varsa aynı LPM eşleşmesi, sonra da bir yol, özgün sırasının hello göre seçilir:</span><span class="sxs-lookup"><span data-stu-id="b24fd-157">If there is more than one route with hello same LPM match, then a route is selected based on its origin in hello following order:</span></span>
  
  * <span data-ttu-id="b24fd-158">Kullanıcı tanımlı yol</span><span class="sxs-lookup"><span data-stu-id="b24fd-158">User-defined route</span></span>
  * <span data-ttu-id="b24fd-159">BGP yolu</span><span class="sxs-lookup"><span data-stu-id="b24fd-159">BGP route</span></span>
  * <span data-ttu-id="b24fd-160">Sistem (varsayılan) yolu</span><span class="sxs-lookup"><span data-stu-id="b24fd-160">System (Default) route</span></span>
    
    <span data-ttu-id="b24fd-161">Etkin yollar ile LPM eşleşmesine tüm hello kullanılabilir yollarına bağlı olduğundan geçerlilik yollar yalnızca görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b24fd-161">With effective routes, you can only see effective routes that are LPM match based on all hello availble routes.</span></span> <span data-ttu-id="b24fd-162">Nasıl hello yollar için belirli bir NIC gerçekte değerlendirildiği göstererek bu VM/gruptan bağlantı etkileyen çok daha kolay tootroubleshoot belirli yollar sağlar.</span><span class="sxs-lookup"><span data-stu-id="b24fd-162">By showing how hello routes are actually evaluated for a given NIC, this makes it a lot easier tootroubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="b24fd-163">Udr'ler varsa ve trafik tooa ağ sanal gereç (NVA) ile gönderiyor *değerinin VirtualAppliance* olarak **nextHopType**, IP iletimini hello NVA alıcı hello trafiği üzerinde etkinleştirildiğinden emin olun veya paket bırakılır.</span><span class="sxs-lookup"><span data-stu-id="b24fd-163">If you have UDRs and are sending traffic tooa network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on hello NVA receiving hello traffic or packets are dropped.</span></span> 
* <span data-ttu-id="b24fd-164">Zorlamalı tünel etkinleştirildiğinde tüm giden Internet trafiği yönlendirilmiş tooon içi olur.</span><span class="sxs-lookup"><span data-stu-id="b24fd-164">If Forced tunneling is enabled, all outbound Internet traffic will be routed tooon-premises.</span></span> <span data-ttu-id="b24fd-165">RDP/SSH VM nasıl hello şirket içi bağlı olarak bu ayar ile çalışmayabilir Internet tooyour bu trafiği işler.</span><span class="sxs-lookup"><span data-stu-id="b24fd-165">RDP/SSH from Internet tooyour VM may not work with this setting, depending on how hello on-premises handles this traffic.</span></span> 
  <span data-ttu-id="b24fd-166">Zorlamalı tünel etkinleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="b24fd-166">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="b24fd-167">Siteden siteye VPN, VPN ağ geçidi olarak nextHopType ile bir kullanıcı tanımlı yönlendirme (UDR) ayarlayarak kullanıyorsanız</span><span class="sxs-lookup"><span data-stu-id="b24fd-167">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="b24fd-168">Varsayılan rota BGP Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="b24fd-168">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="b24fd-169">Sanal ağ trafiğini toowork doğru eşleme bir sistem rotası için **nextHopType** *VNetPeering* sanal ağınızın önek aralığı hello eşlenen için mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b24fd-169">For VNet peering traffic toowork correctly, a system route with **nextHopType** *VNetPeering* must exist for hello peered VNet’s prefix range.</span></span> <span data-ttu-id="b24fd-170">Böyle bir yol mevcutsa değil ve VNet eşlemesi hello bağlantı Tamam görünür:</span><span class="sxs-lookup"><span data-stu-id="b24fd-170">If such a route doesn’t exist and hello VNet peering link looks OK:</span></span>
  * <span data-ttu-id="b24fd-171">Birkaç saniye bekleyin ve yeni oluşturulmuş bir eşleme bağlantısı ise, yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="b24fd-171">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="b24fd-172">Bazen uzun toopropagate yollar tooall hello ağ arabirimleri bir alt ağdaki alır.</span><span class="sxs-lookup"><span data-stu-id="b24fd-172">It occasionally takes longer toopropagate routes tooall hello network interfaces in a subnet.</span></span>
  * <span data-ttu-id="b24fd-173">Ağ güvenlik grubu (NSG) kuralları hello trafik akışına etkiliyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="b24fd-173">Network Security Group (NSG) rules may be impacting hello traffic flows.</span></span> <span data-ttu-id="b24fd-174">Merhaba daha fazla bilgi için bkz: [sorun giderme ağ güvenlik grupları](virtual-network-nsg-troubleshoot-powershell.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="b24fd-174">For more information, see hello [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-powershell.md) article.</span></span>

