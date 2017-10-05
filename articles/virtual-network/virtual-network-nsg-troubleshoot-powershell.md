---
title: "Ağ güvenlik grupları - PowerShell sorunlarını giderme | Microsoft Docs"
description: "Ağ güvenlik grupları Azure PowerShell kullanarak Azure Resource Manager dağıtım modelinde sorun giderme öğrenin."
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
ms.openlocfilehash: 5edaf7197576ac1c0bd1fc6bed21fd65ed135106
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a><span data-ttu-id="77340-103">Ağ güvenlik grupları Azure PowerShell kullanarak sorun giderme</span><span class="sxs-lookup"><span data-stu-id="77340-103">Troubleshoot Network Security Groups using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="77340-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="77340-104">Azure Portal</span></span>](virtual-network-nsg-troubleshoot-portal.md)
> * [<span data-ttu-id="77340-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="77340-105">PowerShell</span></span>](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="77340-106">Ağ güvenlik grupları (Nsg'ler), sanal makine (VM) üzerinde yapılandırılmış ve VM bağlantı sorunları yaşıyorsanız, bu makalede daha fazla gidermek Nsg'ler tanılama özelliklerine genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="77340-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs to help troubleshoot further.</span></span>

<span data-ttu-id="77340-107">Nsg'ler sanal makineleri (VM'ler) ve akan trafik türlerini denetlemenize sağlar.</span><span class="sxs-lookup"><span data-stu-id="77340-107">NSGs enable you to control the types of traffic that flow in and out of your virtual machines (VMs).</span></span> <span data-ttu-id="77340-108">Nsg'ler alt ağlara bir Azure sanal ağı (VNet), ağ arabirimleri (NIC) ya da her ikisini de uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="77340-108">NSGs can be applied to subnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span></span> <span data-ttu-id="77340-109">Bir NIC uygulanan etkili bir NIC'ye uygulanan Nsg'ler mevcut kurallar ve bağlı olduğu alt ağ bir toplama kurallardır.</span><span class="sxs-lookup"><span data-stu-id="77340-109">The effective rules applied to a NIC are an aggregation of the rules that exist in the NSGs applied to a NIC and the subnet it is connected to.</span></span> <span data-ttu-id="77340-110">Bu Nsg'ler arasında kuralları bazen birbiriyle çelişen ve bir sanal makinenin ağ bağlantısını etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="77340-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span></span>  

<span data-ttu-id="77340-111">VM Nıc'lerde uygulanan olarak, tüm etkin güvenlik kuralları Nsg'lerinizi görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="77340-111">You can view all the effective security rules from your NSGs, as applied on your VM's NICs.</span></span> <span data-ttu-id="77340-112">Bu makalede, bu kurallar Azure Resource Manager dağıtım modelinde kullanarak VM bağlantı sorunlarını gidermek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="77340-112">This article shows how to troubleshoot VM connectivity issues using these rules in the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="77340-113">VNet ve NSG kavramlarına alışık değilseniz, okuma [sanal ağ](virtual-networks-overview.md) ve [ağ güvenlik grupları](virtual-networks-nsg.md) genel bakış makaleleri.</span><span class="sxs-lookup"><span data-stu-id="77340-113">If you're not familiar with VNet and NSG concepts, read the [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span></span>

## <a name="using-effective-security-rules-to-troubleshoot-vm-traffic-flow"></a><span data-ttu-id="77340-114">VM trafik akışı sorun giderme için etkili güvenlik kurallarını kullanma</span><span class="sxs-lookup"><span data-stu-id="77340-114">Using Effective Security Rules to troubleshoot VM traffic flow</span></span>
<span data-ttu-id="77340-115">Aşağıdaki senaryoda, ortak bir bağlantı sorunu örneğidir:</span><span class="sxs-lookup"><span data-stu-id="77340-115">The scenario that follows is an example of a common connection problem:</span></span>

<span data-ttu-id="77340-116">Adlı bir VM'den *VM1* adlı bir alt ağın parçası olan *Subnet1* adlı bir sanal ağ içindeki *WestUS VNet1*.</span><span class="sxs-lookup"><span data-stu-id="77340-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span></span> <span data-ttu-id="77340-117">3389 numaralı TCP bağlantı noktası üzerinden RDP kullanarak VM bağlanma denemesi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="77340-117">An attempt to connect to the VM using RDP over TCP port 3389 fails.</span></span> <span data-ttu-id="77340-118">Nsg'ler, her iki NIC üzerinde uygulanır *VM1 nıc1* ve alt ağ *Subnet1*.</span><span class="sxs-lookup"><span data-stu-id="77340-118">NSGs are applied at both the NIC *VM1-NIC1* and the subnet *Subnet1*.</span></span> <span data-ttu-id="77340-119">TCP bağlantı noktası 3389 trafiği ağ arabirimiyle ilişkilendirilmiş NSG izin verilen *VM1 nıc1*, kullanıcının VM1 ping TCP bağlantı noktası ancak 3389 başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="77340-119">Traffic to TCP port 3389 is allowed in the NSG associated with the network interface *VM1-NIC1*, however TCP ping to VM1's port 3389 fails.</span></span>

<span data-ttu-id="77340-120">Bu örnek 3389 numaralı TCP bağlantı noktasını kullanır, ancak herhangi bir bağlantı noktası gelen ve giden bağlantı hataları belirlemek için aşağıdaki adımları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="77340-120">While this example uses TCP port 3389, the following steps can be used to determine inbound and outbound connection failures over any port.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="77340-121">Ayrıntılı sorun giderme adımları</span><span class="sxs-lookup"><span data-stu-id="77340-121">Detailed Troubleshooting Steps</span></span>
<span data-ttu-id="77340-122">Nsg'leri bir VM için sorun giderme için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="77340-122">Complete the following steps to troubleshoot NSGs for a VM:</span></span>

1. <span data-ttu-id="77340-123">Bir Azure PowerShell oturumu ve Azure oturum açma başlatın.</span><span class="sxs-lookup"><span data-stu-id="77340-123">Start an Azure PowerShell session and login to Azure.</span></span> <span data-ttu-id="77340-124">Azure PowerShell ile bilmiyorsanız okuma [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview) makale.</span><span class="sxs-lookup"><span data-stu-id="77340-124">If you're not familiar with using Azure PowerShell, read the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="77340-125">Adlı bir NIC uygulanan tüm NSG kuralları döndürmek için aşağıdaki komutu girin *VM1 nıc1* kaynak grubunda *RG1*:</span><span class="sxs-lookup"><span data-stu-id="77340-125">Enter the following command to return all NSG rules applied to a NIC named *VM1-NIC1* in the resource group *RG1*:</span></span>
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="77340-126">Bir NIC adını bilmiyorsanız, bir kaynak grubundaki tüm NIC'ler adları almak için aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="77340-126">If you don't know the name of a NIC, enter the following command to retrieve the names of all NICs in a resource group:</span></span> 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    <span data-ttu-id="77340-127">Aşağıdaki metni için döndürülen etkili kuralları çıkış örneğidir *VM1 nıc1* NIC:</span><span class="sxs-lookup"><span data-stu-id="77340-127">The following text is a sample of the effective rules output returned for the *VM1-NIC1* NIC:</span></span>
   
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
   
    <span data-ttu-id="77340-128">Çıktı aşağıdaki bilgileri unutmayın:</span><span class="sxs-lookup"><span data-stu-id="77340-128">Note the following information in the output:</span></span>
   
   * <span data-ttu-id="77340-129">Var olan iki **NetworkSecurityGroup** bölümler: bir alt ağ ile ilişkili biridir (*Subnet1*) ve bir NIC ile ilişkili olduğu (*VM1 nıc1*).</span><span class="sxs-lookup"><span data-stu-id="77340-129">There are two **NetworkSecurityGroup** sections: One is associated with a subnet (*Subnet1*) and one is associated with a NIC (*VM1-NIC1*).</span></span> <span data-ttu-id="77340-130">Bu örnekte, her bir NSG uygulanmıştır.</span><span class="sxs-lookup"><span data-stu-id="77340-130">In this example, an NSG has been applied to each.</span></span>
   * <span data-ttu-id="77340-131">**İlişkilendirme** kaynak (alt ağ veya NIC) belirli bir NSG ile ilişkili olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="77340-131">**Association** shows the resource (subnet or NIC) a given NSG is associated with.</span></span> <span data-ttu-id="77340-132">NSG kaynağı hemen bu komutu çalıştırmadan önce taşınmış ve ilişkilendirmesi ise, komut çıktısında yansıtacak şekilde değiştirmek için birkaç saniye beklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="77340-132">If the NSG resource is moved/disassociated immediately before running this command, you may need to wait a few seconds for the change to reflect in the command output.</span></span> 
   * <span data-ttu-id="77340-133">İle başlayan kuralı adları *defaultSecurityRules*: olduğunda bir NSG oluşturulur, birkaç varsayılan güvenlik kuralları içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="77340-133">The rule names that are prefaced with *defaultSecurityRules*: When an NSG is created, several default security rules are created within it.</span></span> <span data-ttu-id="77340-134">Varsayılan kurallar kaldırılamaz, ancak daha yüksek öncelik kuralları ile geçersiz kılınabilir.</span><span class="sxs-lookup"><span data-stu-id="77340-134">Default rules can't be removed, but they can be overridden with higher priority rules.</span></span>
     <span data-ttu-id="77340-135">Okuma [NSG genel bakış](virtual-networks-nsg.md#default-rules) makale güvenlik kuralları varsayılan NSG hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="77340-135">Read the [NSG overview](virtual-networks-nsg.md#default-rules) article to learn more about NSG default security rules.</span></span>
   * <span data-ttu-id="77340-136">**ExpandedAddressPrefix** NSG varsayılan etiketleri için adres önekleri genişletir.</span><span class="sxs-lookup"><span data-stu-id="77340-136">**ExpandedAddressPrefix** expands the address prefixes for NSG default tags.</span></span> <span data-ttu-id="77340-137">Etiketler, birden çok adres öneklerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="77340-137">Tags represent multiple address prefixes.</span></span> <span data-ttu-id="77340-138">Etiketlerin genişletme denetleyicisinden belirli adres öneklerini VM bağlantı sorunlarını giderirken faydalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="77340-138">Expansion of the tags can be useful when troubleshooting VM connectivity to/from specific address prefixes.</span></span> <span data-ttu-id="77340-139">Örneğin, VNET eşlemesi ile VIRTUAL_NETWORK etiketine eşlenmiş VNet ön önceki çıktısında göstermek için genişletir.</span><span class="sxs-lookup"><span data-stu-id="77340-139">For example, with VNET peering, VIRTUAL_NETWORK tag expands to show peered VNet prefixes in the previous output.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="77340-140">Bir NSG'yi bir alt ağ, bir NIC veya her ikisi ile ilişkili ise, komut yalnızca gösterir etkili kuralları.</span><span class="sxs-lookup"><span data-stu-id="77340-140">The command only shows effective rules if an NSG is associated with either a subnet, a NIC, or both.</span></span> <span data-ttu-id="77340-141">Bir VM uygulanan farklı Nsg'ler ile birden çok NIC olabilir.</span><span class="sxs-lookup"><span data-stu-id="77340-141">A VM may have multiple NICs with different NSGs applied.</span></span> <span data-ttu-id="77340-142">Sorunlarını giderirken, her bir NIC komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="77340-142">When troubleshooting, run the command for each NIC.</span></span>
     > 
     > 
3. <span data-ttu-id="77340-143">Daha fazla sayıda NSG kuralları filtreleme kolaylaştırmak için daha fazla sorun giderme için aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="77340-143">To ease filtering over larger number of NSG rules, enter the following commands to troubleshoot further:</span></span> 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    <span data-ttu-id="77340-144">RDP trafiğine (TCP bağlantı noktası 3389) için bir filtre aşağıdaki resimde gösterildiği gibi kılavuz görünümüne uygulanır:</span><span class="sxs-lookup"><span data-stu-id="77340-144">A filter for RDP traffic (TCP port 3389), is applied to the grid view, as shown in the following picture:</span></span>
   
    ![Kuralları listesi](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. <span data-ttu-id="77340-146">Izgara görünümünde görebileceğiniz gibi vardır her ikisi de izin ver ve Reddet kurallarının için RDP.</span><span class="sxs-lookup"><span data-stu-id="77340-146">As you can see in the grid view, there are both allow and deny rules for RDP.</span></span> <span data-ttu-id="77340-147">2. adım çıktısını gösterir *DenyRDP* alt ağa uygulanan nsg'deki kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="77340-147">The output from step 2 shows that the *DenyRDP* rule is in the NSG applied to the subnet.</span></span> <span data-ttu-id="77340-148">Gelen kuralları için alt ağa uygulanan Nsg'ler önce işlenir.</span><span class="sxs-lookup"><span data-stu-id="77340-148">For inbound rules, NSGs applied to the subnet are processed first.</span></span> <span data-ttu-id="77340-149">Bir eşleşme bulunursa, bir ağ arabirimine uygulanan NSG işlenmez.</span><span class="sxs-lookup"><span data-stu-id="77340-149">If a match is found, the NSG applied to the network interface is not processed.</span></span> <span data-ttu-id="77340-150">Bu durumda, *DenyRDP* alt ağdan kural, VM için RDP engeller (**VM1**).</span><span class="sxs-lookup"><span data-stu-id="77340-150">In this case, the *DenyRDP* rule from the subnet blocks RDP to the VM (**VM1**).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="77340-151">Bir VM ekli birden çok NIC olabilir.</span><span class="sxs-lookup"><span data-stu-id="77340-151">A VM may have multiple NICs attached to it.</span></span> <span data-ttu-id="77340-152">Her farklı bir alt ağa bağlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="77340-152">Each may be connected to a different subnet.</span></span> <span data-ttu-id="77340-153">Önceki adımları komutlar bir NIC karşı çalışır olduğundan, bağlantı hatası yaşıyoruz NIC belirttiğinizden emin olun önemlidir.</span><span class="sxs-lookup"><span data-stu-id="77340-153">Since the commands in the previous steps are run against a NIC, it's important to ensure that you specify the NIC you're having the connectivity failure to.</span></span> <span data-ttu-id="77340-154">Emin değilseniz VM'ye bağlı her NIC karşı komutları her zaman çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="77340-154">If you're not sure, you can always run the commands against each NIC attached to the VM.</span></span>
   > 
   > 
5. <span data-ttu-id="77340-155">VM1 halinde RDP için değiştirme *Reddet RDP (3389)* kuralı *izin RDP(3389)* içinde **Subnet1 NSG** NSG.</span><span class="sxs-lookup"><span data-stu-id="77340-155">To RDP into VM1, change the *Deny RDP (3389)* rule to *Allow RDP(3389)* in the **Subnet1-NSG** NSG.</span></span> <span data-ttu-id="77340-156">TCP bağlantı noktası 3389 VM için RDP bağlantısı açarak veya PsPing aracını kullanarak açık olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="77340-156">Confirm that TCP port 3389 is open by opening an RDP connection to the VM or using the PsPing tool.</span></span> <span data-ttu-id="77340-157">Okuyarak PsPing hakkında daha fazla bilgiyi [PsPing indirme sayfası](https://technet.microsoft.com/sysinternals/psping.aspx)</span><span class="sxs-lookup"><span data-stu-id="77340-157">You can learn more about PsPing by reading the [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx)</span></span>
   
    <span data-ttu-id="77340-158">Aşağıdaki komut çıktısı bilgileri kullanarak bir NSG kuralları kaldırın ve yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="77340-158">You can or remove rules from an NSG by using the information in the output from the following command:</span></span>
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a><span data-ttu-id="77340-159">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="77340-159">Considerations</span></span>
<span data-ttu-id="77340-160">Bağlantı sorunlarını giderme yaparken aşağıdaki noktaları dikkate alın:</span><span class="sxs-lookup"><span data-stu-id="77340-160">Consider the following points when troubleshooting connectivity problems:</span></span>

* <span data-ttu-id="77340-161">Varsayılan NSG kuralları internet'ten gelen erişimi engellemek ve yalnızca VNet izin gelen trafiği.</span><span class="sxs-lookup"><span data-stu-id="77340-161">Default NSG rules will block inbound access from the internet and only permit VNet inbound traffic.</span></span> <span data-ttu-id="77340-162">Internet'ten gelen erişim gerektiğinde izin vermek için açıkça kuralları eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="77340-162">Rules should be explicitly added to allow inbound access from Internet, as required.</span></span>
* <span data-ttu-id="77340-163">Bir sanal makinenin ağ bağlantısı başarısız olmasına neden olan hiçbir NSG güvenlik kuralları varsa, sorunu nedeniyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="77340-163">If there are no NSG security rules causing a VM’s network connectivity to fail, the problem may be due to:</span></span>
  * <span data-ttu-id="77340-164">Sanal makinenin işletim sistemi içinde çalışan güvenlik duvarı yazılımı</span><span class="sxs-lookup"><span data-stu-id="77340-164">Firewall software running within the VM's operating system</span></span>
  * <span data-ttu-id="77340-165">Sanal gereçler veya şirket içi trafiği için yapılandırılmış yollar.</span><span class="sxs-lookup"><span data-stu-id="77340-165">Routes configured for virtual appliances or on-premises traffic.</span></span> <span data-ttu-id="77340-166">Internet trafiği, şirket içi zorlamalı tünel aracılığıyla yönlendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="77340-166">Internet traffic can be redirected to on-premises via forced-tunneling.</span></span> <span data-ttu-id="77340-167">VM Internet'ten bir RDP/SSH bağlantısı nasıl şirket içi ağ donanımı bu trafiği işler bağlı olarak bu ayar ile çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="77340-167">An RDP/SSH connection from the Internet to your VM may not work with this setting, depending on how the on-premises network hardware handles this traffic.</span></span> <span data-ttu-id="77340-168">Okuma [sorun giderme yolları](virtual-network-routes-troubleshoot-powershell.md) makale içeri ve dışarı VM trafik akışını engelleyen rota sorunları tanılamak öğrenin.</span><span class="sxs-lookup"><span data-stu-id="77340-168">Read the [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article to learn how to diagnose route problems that may be impeding the flow of traffic in and out of the VM.</span></span> 
* <span data-ttu-id="77340-169">Varsayılan olarak sanal ağlar, eşlenen, VIRTUAL_NETWORK etiketine önekler için eşlenmiş Vnet'lerde dahil etmek için otomatik olarak genişletilir.</span><span class="sxs-lookup"><span data-stu-id="77340-169">If you have peered VNets, by default, the VIRTUAL_NETWORK tag will automatically expand to include prefixes for peered VNets.</span></span> <span data-ttu-id="77340-170">Bu önekleri görüntüleyebilirsiniz **ExpandedAddressPrefix** VNet eşleme bağlantısı ilgili sorunları gidermek için liste.</span><span class="sxs-lookup"><span data-stu-id="77340-170">You can view these prefixes in the **ExpandedAddressPrefix** list, to troubleshoot any issues related to VNet peering connectivity.</span></span> 
* <span data-ttu-id="77340-171">Etkin güvenlik kuralları yalnızca VM NIC ve veya alt ağ ilişkilendirilmiş bir NSG olup olmadığını gösterilir.</span><span class="sxs-lookup"><span data-stu-id="77340-171">Effective security rules are only shown if there is an NSG associated with the VM’s NIC and or subnet.</span></span> 
* <span data-ttu-id="77340-172">Alt ağ ve NIC ile ilişkili hiçbir Nsg'ler vardır veya VM'nize atanan genel bir IP adresi varsa, tüm bağlantı noktalarına gelen ve giden erişimi açık olacaktır.</span><span class="sxs-lookup"><span data-stu-id="77340-172">If there are no NSGs associated with the NIC or subnet and you have a public IP address assigned to your VM, all ports will be open for inbound and outbound access.</span></span> <span data-ttu-id="77340-173">VM bir ortak IP adresi varsa, NIC veya alt ağ Nsg'ler uygulanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="77340-173">If the VM has a public IP address, applying NSGs to the NIC or subnet is strongly recommended.</span></span>  

