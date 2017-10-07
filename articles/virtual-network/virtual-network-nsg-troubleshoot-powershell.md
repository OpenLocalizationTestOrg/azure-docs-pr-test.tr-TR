---
title: "aaaTroubleshoot ağ güvenlik grupları - PowerShell | Microsoft Docs"
description: "Azure PowerShell kullanarak nasıl tootroubleshoot ağ güvenlik grupları'hello Azure Resource Manager dağıtımında model öğrenin."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a><span data-ttu-id="11380-103">Ağ güvenlik grupları Azure PowerShell kullanarak sorun giderme</span><span class="sxs-lookup"><span data-stu-id="11380-103">Troubleshoot Network Security Groups using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="11380-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="11380-104">Azure Portal</span></span>](virtual-network-nsg-troubleshoot-portal.md)
> * [<span data-ttu-id="11380-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="11380-105">PowerShell</span></span>](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="11380-106">Ağ güvenlik grupları (Nsg'ler), sanal makine (VM) üzerinde yapılandırılmış ve VM bağlantı sorunları yaşıyorsanız, bu makalede Nsg'ler toohelp daha fazla sorun giderme için tanılama özelliklerine genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="11380-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs toohelp troubleshoot further.</span></span>

<span data-ttu-id="11380-107">Nsg'ler toocontrol hello trafik türlerini ve sanal makineleri (VM'ler) dışındaki akan sağlar.</span><span class="sxs-lookup"><span data-stu-id="11380-107">NSGs enable you toocontrol hello types of traffic that flow in and out of your virtual machines (VMs).</span></span> <span data-ttu-id="11380-108">Nsg'ler uygulanan toosubnets bir Azure sanal ağı (VNet), ağ arabirimleri (NIC) veya her ikisi de olabilir.</span><span class="sxs-lookup"><span data-stu-id="11380-108">NSGs can be applied toosubnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span></span> <span data-ttu-id="11380-109">bir toplama bağlı hello uygulanan Nsg'ler tooa NIC ve hello alt ağda bulunan hello kuralların Hello uygulanacak etkili kurallar tooa NIC var.</span><span class="sxs-lookup"><span data-stu-id="11380-109">hello effective rules applied tooa NIC are an aggregation of hello rules that exist in hello NSGs applied tooa NIC and hello subnet it is connected to.</span></span> <span data-ttu-id="11380-110">Bu Nsg'ler arasında kuralları bazen birbiriyle çelişen ve bir sanal makinenin ağ bağlantısını etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="11380-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span></span>  

<span data-ttu-id="11380-111">VM Nıc'lerde uygulanan olarak Nsg'lerinizi tüm hello etkin güvenlik kuralları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11380-111">You can view all hello effective security rules from your NSGs, as applied on your VM's NICs.</span></span> <span data-ttu-id="11380-112">Bu makalede Azure Resource Manager dağıtım modeli bu kuralları kullanmak tootroubleshoot VM bağlantı sorunları nasıl hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="11380-112">This article shows how tootroubleshoot VM connectivity issues using these rules in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="11380-113">VNet ve NSG kavramlarına alışık değilseniz, hello okuma [sanal ağ](virtual-networks-overview.md) ve [ağ güvenlik grupları](virtual-networks-nsg.md) genel bakış makaleleri.</span><span class="sxs-lookup"><span data-stu-id="11380-113">If you're not familiar with VNet and NSG concepts, read hello [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span></span>

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="11380-114">Etkin güvenlik kuralları tootroubleshoot VM trafik akışı kullanma</span><span class="sxs-lookup"><span data-stu-id="11380-114">Using Effective Security Rules tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="11380-115">izleyen hello senaryo, ortak bir bağlantı sorunu örneğidir:</span><span class="sxs-lookup"><span data-stu-id="11380-115">hello scenario that follows is an example of a common connection problem:</span></span>

<span data-ttu-id="11380-116">Adlı bir VM'den *VM1* adlı bir alt ağın parçası olan *Subnet1* adlı bir sanal ağ içindeki *WestUS VNet1*.</span><span class="sxs-lookup"><span data-stu-id="11380-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span></span> <span data-ttu-id="11380-117">Bir deneme tooconnect toohello 3389 numaralı TCP bağlantı noktası üzerinden RDP kullanarak VM başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="11380-117">An attempt tooconnect toohello VM using RDP over TCP port 3389 fails.</span></span> <span data-ttu-id="11380-118">Nsg'ler NIC hem hello uygulanan *VM1 nıc1* ve alt ağ hello *Subnet1*.</span><span class="sxs-lookup"><span data-stu-id="11380-118">NSGs are applied at both hello NIC *VM1-NIC1* and hello subnet *Subnet1*.</span></span> <span data-ttu-id="11380-119">Trafik tooTCP 3389 numaralı bağlantı noktasını hello hello ağ arabirimiyle ilişkilendirilmiş NSG izin verilen *VM1 nıc1*, TCP ping ancak tooVM1'ın bağlantı noktası 3389 başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="11380-119">Traffic tooTCP port 3389 is allowed in hello NSG associated with hello network interface *VM1-NIC1*, however TCP ping tooVM1's port 3389 fails.</span></span>

<span data-ttu-id="11380-120">Bu örnek 3389 numaralı TCP bağlantı noktasını kullanır, ancak adımları hello kullanılan toodetermine herhangi bir bağlantı noktası gelen ve giden bağlantı hataları olabilir.</span><span class="sxs-lookup"><span data-stu-id="11380-120">While this example uses TCP port 3389, hello following steps can be used toodetermine inbound and outbound connection failures over any port.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="11380-121">Ayrıntılı sorun giderme adımları</span><span class="sxs-lookup"><span data-stu-id="11380-121">Detailed Troubleshooting Steps</span></span>
<span data-ttu-id="11380-122">Bir VM için adımları tootroubleshoot Nsg'ler aşağıdaki hello tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="11380-122">Complete hello following steps tootroubleshoot NSGs for a VM:</span></span>

1. <span data-ttu-id="11380-123">Bir Azure PowerShell oturumu ve oturum açma tooAzure başlatın.</span><span class="sxs-lookup"><span data-stu-id="11380-123">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="11380-124">Azure PowerShell ile bilmiyorsanız hello okuma [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) makalesi.</span><span class="sxs-lookup"><span data-stu-id="11380-124">If you're not familiar with using Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="11380-125">Tooreturn tüm NSG kuralları uygulanan tooa adlı NIC komutu aşağıdaki hello girin *VM1 nıc1* hello kaynak grubunda *RG1*:</span><span class="sxs-lookup"><span data-stu-id="11380-125">Enter hello following command tooreturn all NSG rules applied tooa NIC named *VM1-NIC1* in hello resource group *RG1*:</span></span>
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="11380-126">Bir NIC hello adını bilmiyorsanız, bir kaynak grubundaki tüm NIC'ler komut tooretrieve hello adlarını aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="11380-126">If you don't know hello name of a NIC, enter hello following command tooretrieve hello names of all NICs in a resource group:</span></span> 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    <span data-ttu-id="11380-127">Merhaba aşağıdaki metni Merhaba döndürülen hello etkili kuralları çıkış örneğidir *VM1 nıc1* NIC:</span><span class="sxs-lookup"><span data-stu-id="11380-127">hello following text is a sample of hello effective rules output returned for hello *VM1-NIC1* NIC:</span></span>
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    <span data-ttu-id="11380-128">Aşağıdaki bilgilerle hello çıktısında hello dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="11380-128">Note hello following information in hello output:</span></span>
   
   * <span data-ttu-id="11380-129">Var olan iki **NetworkSecurityGroup** bölümler: bir alt ağ ile ilişkili biridir (*Subnet1*) ve bir NIC ile ilişkili olduğu (*VM1 nıc1*).</span><span class="sxs-lookup"><span data-stu-id="11380-129">There are two **NetworkSecurityGroup** sections: One is associated with a subnet (*Subnet1*) and one is associated with a NIC (*VM1-NIC1*).</span></span> <span data-ttu-id="11380-130">Bu örnekte, bir NSG uygulanan tooeach olmuştur.</span><span class="sxs-lookup"><span data-stu-id="11380-130">In this example, an NSG has been applied tooeach.</span></span>
   * <span data-ttu-id="11380-131">**İlişkilendirme** hello kaynak (alt ağ veya NIC) belirli bir NSG ile ilişkili olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="11380-131">**Association** shows hello resource (subnet or NIC) a given NSG is associated with.</span></span> <span data-ttu-id="11380-132">Merhaba NSG kaynağı hemen bu komutu çalıştırmadan önce taşınmış ve ilişkilendirmesi ise, birkaç saniye toowait hello değişiklik tooreflect hello komut çıktısında için gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="11380-132">If hello NSG resource is moved/disassociated immediately before running this command, you may need toowait a few seconds for hello change tooreflect in hello command output.</span></span> 
   * <span data-ttu-id="11380-133">Merhaba ile başlayan kuralı adları *defaultSecurityRules*: olduğunda bir NSG oluşturulur, birkaç varsayılan güvenlik kuralları içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="11380-133">hello rule names that are prefaced with *defaultSecurityRules*: When an NSG is created, several default security rules are created within it.</span></span> <span data-ttu-id="11380-134">Varsayılan kurallar kaldırılamaz, ancak daha yüksek öncelik kuralları ile geçersiz kılınabilir.</span><span class="sxs-lookup"><span data-stu-id="11380-134">Default rules can't be removed, but they can be overridden with higher priority rules.</span></span>
     <span data-ttu-id="11380-135">Okuma hello [NSG genel bakış](virtual-networks-nsg.md#default-rules) NSG hakkında daha fazla makale toolearn varsayılan güvenlik kuralları.</span><span class="sxs-lookup"><span data-stu-id="11380-135">Read hello [NSG overview](virtual-networks-nsg.md#default-rules) article toolearn more about NSG default security rules.</span></span>
   * <span data-ttu-id="11380-136">**ExpandedAddressPrefix** hello adres öneklerini NSG varsayılan etiketleri için genişletir.</span><span class="sxs-lookup"><span data-stu-id="11380-136">**ExpandedAddressPrefix** expands hello address prefixes for NSG default tags.</span></span> <span data-ttu-id="11380-137">Etiketler, birden çok adres öneklerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="11380-137">Tags represent multiple address prefixes.</span></span> <span data-ttu-id="11380-138">Merhaba etiketleri genişlemesi denetleyicisinden belirli adres öneklerini VM bağlantı sorunlarını giderirken faydalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="11380-138">Expansion of hello tags can be useful when troubleshooting VM connectivity to/from specific address prefixes.</span></span> <span data-ttu-id="11380-139">Örneğin, VNET eşlemesi ile VIRTUAL_NETWORK etiketine tooshow genişletir VNet ön hello önceki çıktısında eşlenen.</span><span class="sxs-lookup"><span data-stu-id="11380-139">For example, with VNET peering, VIRTUAL_NETWORK tag expands tooshow peered VNet prefixes in hello previous output.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="11380-140">bir NSG'yi bir alt ağ, bir NIC veya her ikisi ile ilişkili ise, komut yalnızca gösterir etkili kuralları hello.</span><span class="sxs-lookup"><span data-stu-id="11380-140">hello command only shows effective rules if an NSG is associated with either a subnet, a NIC, or both.</span></span> <span data-ttu-id="11380-141">Bir VM uygulanan farklı Nsg'ler ile birden çok NIC olabilir.</span><span class="sxs-lookup"><span data-stu-id="11380-141">A VM may have multiple NICs with different NSGs applied.</span></span> <span data-ttu-id="11380-142">Sorunlarını giderirken, her bir NIC hello komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="11380-142">When troubleshooting, run hello command for each NIC.</span></span>
     > 
     > 
3. <span data-ttu-id="11380-143">NSG kuralları, fazla sayıda filtreleme tooease başka komutlar tootroubleshoot aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="11380-143">tooease filtering over larger number of NSG rules, enter hello following commands tootroubleshoot further:</span></span> 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    <span data-ttu-id="11380-144">RDP trafiğine (TCP bağlantı noktası 3389) için bir filtre hello resim aşağıdaki gösterildiği gibi toohello Izgara Görünümü uygulanır:</span><span class="sxs-lookup"><span data-stu-id="11380-144">A filter for RDP traffic (TCP port 3389), is applied toohello grid view, as shown in hello following picture:</span></span>
   
    ![Kuralları listesi](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. <span data-ttu-id="11380-146">Merhaba ızgara görünümünde görebileceğiniz gibi vardır her ikisi de izin ver ve Reddet kurallarının için RDP.</span><span class="sxs-lookup"><span data-stu-id="11380-146">As you can see in hello grid view, there are both allow and deny rules for RDP.</span></span> <span data-ttu-id="11380-147">Merhaba 2. adım çıktısını gösterir, hello *DenyRDP* hello NSG uygulanır toohello alt kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="11380-147">hello output from step 2 shows that hello *DenyRDP* rule is in hello NSG applied toohello subnet.</span></span> <span data-ttu-id="11380-148">Gelen kuralları için uygulanan Nsg'ler toohello alt önce işlenir.</span><span class="sxs-lookup"><span data-stu-id="11380-148">For inbound rules, NSGs applied toohello subnet are processed first.</span></span> <span data-ttu-id="11380-149">Bir eşleşme bulunamazsa hello NSG uygulanır toohello ağ arabirimi işlenmedi.</span><span class="sxs-lookup"><span data-stu-id="11380-149">If a match is found, hello NSG applied toohello network interface is not processed.</span></span> <span data-ttu-id="11380-150">Bu durumda, hello *DenyRDP* kural hello alt ağından gelen RDP toohello VM engeller (**VM1**).</span><span class="sxs-lookup"><span data-stu-id="11380-150">In this case, hello *DenyRDP* rule from hello subnet blocks RDP toohello VM (**VM1**).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="11380-151">Bir VM birden çok NIC ekli tooit olabilir.</span><span class="sxs-lookup"><span data-stu-id="11380-151">A VM may have multiple NICs attached tooit.</span></span> <span data-ttu-id="11380-152">Her bağlı tooa farklı alt olabilir.</span><span class="sxs-lookup"><span data-stu-id="11380-152">Each may be connected tooa different subnet.</span></span> <span data-ttu-id="11380-153">Merhaba komutlar hello önceki adımlarda karşı bir NIC çalıştırılır, belirttiğiniz tooensure hello hello bağlantı hatası yaşıyoruz NIC önemlidir.</span><span class="sxs-lookup"><span data-stu-id="11380-153">Since hello commands in hello previous steps are run against a NIC, it's important tooensure that you specify hello NIC you're having hello connectivity failure to.</span></span> <span data-ttu-id="11380-154">Emin değilseniz, her bağlı NIC toohello VM karşı her zaman hello komutları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11380-154">If you're not sure, you can always run hello commands against each NIC attached toohello VM.</span></span>
   > 
   > 
5. <span data-ttu-id="11380-155">VM1, değişiklik hello içine tooRDP *Reddet RDP (3389)* çok kural*izin RDP(3389)* hello içinde **Subnet1 NSG** NSG.</span><span class="sxs-lookup"><span data-stu-id="11380-155">tooRDP into VM1, change hello *Deny RDP (3389)* rule too*Allow RDP(3389)* in hello **Subnet1-NSG** NSG.</span></span> <span data-ttu-id="11380-156">TCP bağlantı noktası 3389 RDP bağlantı toohello VM açma veya hello PsPing aracını kullanarak açık olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="11380-156">Confirm that TCP port 3389 is open by opening an RDP connection toohello VM or using hello PsPing tool.</span></span> <span data-ttu-id="11380-157">Okuma hello tarafından PsPing hakkında daha fazla bilgiyi [PsPing indirme sayfası](https://technet.microsoft.com/sysinternals/psping.aspx)</span><span class="sxs-lookup"><span data-stu-id="11380-157">You can learn more about PsPing by reading hello [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx)</span></span>
   
    <span data-ttu-id="11380-158">Komutu aşağıdaki hello hello çıktısını hello bilgileri kullanarak bir NSG kuralları kaldırın ve yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="11380-158">You can or remove rules from an NSG by using hello information in hello output from hello following command:</span></span>
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a><span data-ttu-id="11380-159">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="11380-159">Considerations</span></span>
<span data-ttu-id="11380-160">Bağlantı sorunları giderirken noktaları aşağıdaki hello göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="11380-160">Consider hello following points when troubleshooting connectivity problems:</span></span>

* <span data-ttu-id="11380-161">Varsayılan NSG kuralları hello'ten gelen erişim engeller Internet ve yalnızca izin VNet gelen trafiği.</span><span class="sxs-lookup"><span data-stu-id="11380-161">Default NSG rules will block inbound access from hello internet and only permit VNet inbound traffic.</span></span> <span data-ttu-id="11380-162">Kuralları açıkça eklenmesi tooallow gelen gerektiği gibi Internet'ten erişim.</span><span class="sxs-lookup"><span data-stu-id="11380-162">Rules should be explicitly added tooallow inbound access from Internet, as required.</span></span>
* <span data-ttu-id="11380-163">Bir sanal makinenin ağ bağlantısı toofail neden hiçbir NSG güvenlik kuralları varsa, hello sorun nedeniyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="11380-163">If there are no NSG security rules causing a VM’s network connectivity toofail, hello problem may be due to:</span></span>
  * <span data-ttu-id="11380-164">Merhaba VM'ın işletim sistemi içinde çalışan güvenlik duvarı yazılımı</span><span class="sxs-lookup"><span data-stu-id="11380-164">Firewall software running within hello VM's operating system</span></span>
  * <span data-ttu-id="11380-165">Sanal gereçler veya şirket içi trafiği için yapılandırılmış yollar.</span><span class="sxs-lookup"><span data-stu-id="11380-165">Routes configured for virtual appliances or on-premises traffic.</span></span> <span data-ttu-id="11380-166">Internet trafiğini yeniden yönlendirilen tooon içi zorlamalı tünel aracılığıyla olabilir.</span><span class="sxs-lookup"><span data-stu-id="11380-166">Internet traffic can be redirected tooon-premises via forced-tunneling.</span></span> <span data-ttu-id="11380-167">Merhaba Internet tooyour VM bir RDP/SSH bağlantısı nasıl hello şirket içi ağ donanımı bu trafiği işler bağlı olarak bu ayar ile çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="11380-167">An RDP/SSH connection from hello Internet tooyour VM may not work with this setting, depending on how hello on-premises network hardware handles this traffic.</span></span> <span data-ttu-id="11380-168">Okuma hello [sorun giderme yolları](virtual-network-routes-troubleshoot-powershell.md) makale toolearn içinde ve dışında trafik akışını engelleyen toodiagnose rota sorunları hello nasıl VM hello.</span><span class="sxs-lookup"><span data-stu-id="11380-168">Read hello [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article toolearn how toodiagnose route problems that may be impeding hello flow of traffic in and out of hello VM.</span></span> 
* <span data-ttu-id="11380-169">Varsayılan olarak sanal ağlar, eşlenen durumdaysa hello VIRTUAL_NETWORK etiketine tooinclude önekleri eşlenmiş Vnet'ler için otomatik olarak genişletin.</span><span class="sxs-lookup"><span data-stu-id="11380-169">If you have peered VNets, by default, hello VIRTUAL_NETWORK tag will automatically expand tooinclude prefixes for peered VNets.</span></span> <span data-ttu-id="11380-170">Bu önekleri hello görüntüleyebilirsiniz **ExpandedAddressPrefix** listesi olan bağlantı eşliği sorunları ilgili tooVNet tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="11380-170">You can view these prefixes in hello **ExpandedAddressPrefix** list, tootroubleshoot any issues related tooVNet peering connectivity.</span></span> 
* <span data-ttu-id="11380-171">Etkin güvenlik kuralları, bir NSG hello VM'in NIC ve veya alt ağ ilişkili olup yalnızca gösterilir.</span><span class="sxs-lookup"><span data-stu-id="11380-171">Effective security rules are only shown if there is an NSG associated with hello VM’s NIC and or subnet.</span></span> 
* <span data-ttu-id="11380-172">Merhaba NIC ile ilişkili hiçbir Nsg'ler vardır veya alt ağ ve tooyour VM atanan genel bir IP adresi varsa, tüm bağlantı noktalarına gelen ve giden erişimi açık olacaktır.</span><span class="sxs-lookup"><span data-stu-id="11380-172">If there are no NSGs associated with hello NIC or subnet and you have a public IP address assigned tooyour VM, all ports will be open for inbound and outbound access.</span></span> <span data-ttu-id="11380-173">Merhaba VM genel bir IP adresi varsa, Nsg'ler toohello NIC veya alt ağ uygulama önemle tavsiye edilir.</span><span class="sxs-lookup"><span data-stu-id="11380-173">If hello VM has a public IP address, applying NSGs toohello NIC or subnet is strongly recommended.</span></span>  

