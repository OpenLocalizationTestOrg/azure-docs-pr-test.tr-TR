---
title: "Ağ güvenlik grupları - Azure CLI 1.0 oluşturma | Microsoft Docs"
description: "Azure CLI 1.0 kullanarak ağ güvenlik grupları oluşturup öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ca8c182651e3c9f2f1f3a85b94361755d8e638d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-the-azure-cli-10"></a><span data-ttu-id="78f97-103">Ağ güvenlik grupları Azure CLI 1.0 kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="78f97-103">Create network security groups using the Azure CLI 1.0</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="78f97-104">Görevi tamamlamak için kullanılacak CLI sürümleri</span><span class="sxs-lookup"><span data-stu-id="78f97-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="78f97-105">Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="78f97-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="78f97-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – bizim CLI Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="78f97-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="78f97-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) -bizim nesil CLI kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="78f97-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - our next-generation CLI for the resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="78f97-108">Bu makalede Resource Manager dağıtım modeli anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="78f97-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="78f97-109">Ayrıca [Klasik dağıtım modelinde Nsg'leri oluşturma](virtual-networks-create-nsg-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="78f97-109">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="78f97-110">Aşağıdaki örnek Azure CLI komutları yukarıda senaryo tabanlı oluşturulmuş basit bir ortam bekler.</span><span class="sxs-lookup"><span data-stu-id="78f97-110">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> 

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="78f97-111">Ön uç alt ağı için NSG oluşturma</span><span class="sxs-lookup"><span data-stu-id="78f97-111">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="78f97-112">Adlı adlı bir NSG oluşturmak için *NSG ön uç* yukarıdaki senaryoya bağlı olarak, aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="78f97-112">To create an NSG named named *NSG-FrontEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="78f97-113">Hiç Azure CLI kullanmadıysanız bkz. [Azure CLI’yi Yükleme ve Yapılandırma](../cli-install-nodejs.md); sonra da, Azure hesabınızı ve aboneliğinizi seçtiğiniz noktaya kadar yönergeleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="78f97-113">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="78f97-114">Resource Manager moduna geçmek için **azure config mode** komutunu aşağıda gösterildiği gibi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="78f97-114">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="78f97-115">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="78f97-115">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="78f97-116">Çalıştırma **azure ağ nsg oluşturma** bir NSG oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="78f97-116">Run the **azure network nsg create** command to create an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    <span data-ttu-id="78f97-117">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="78f97-117">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
        data:    Name                            : NSG-FrontEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
   
    <span data-ttu-id="78f97-118">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="78f97-118">Parameters:</span></span>
   
   * <span data-ttu-id="78f97-119">**-g (veya --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="78f97-119">**-g (or --resource-group)**.</span></span> <span data-ttu-id="78f97-120">NSG oluşturulacağı kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="78f97-120">Name of the resource group where the NSG will be created.</span></span> <span data-ttu-id="78f97-121">Bizim senaryomuz için bu *TestRG* ’dir.</span><span class="sxs-lookup"><span data-stu-id="78f97-121">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="78f97-122">**-l (veya --location)**.</span><span class="sxs-lookup"><span data-stu-id="78f97-122">**-l (or --location)**.</span></span> <span data-ttu-id="78f97-123">Yeni NSG oluşturulacağı azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="78f97-123">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="78f97-124">Bizim senaryomuz için *westus*.</span><span class="sxs-lookup"><span data-stu-id="78f97-124">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="78f97-125">**-n (veya --name)**.</span><span class="sxs-lookup"><span data-stu-id="78f97-125">**-n (or --name)**.</span></span> <span data-ttu-id="78f97-126">Yeni nsg'nin adı.</span><span class="sxs-lookup"><span data-stu-id="78f97-126">Name for the new NSG.</span></span> <span data-ttu-id="78f97-127">Bizim senaryomuz için *NSG ön uç*.</span><span class="sxs-lookup"><span data-stu-id="78f97-127">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="78f97-128">Çalıştırma **azure ağ nsg kuralını** Internet'ten (RDP) 3389 numaralı bağlantı noktasına erişim sağlayan bir kural oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="78f97-128">Run the **azure network nsg rule create** command to create a rule that allows access to port 3389 (RDP) from the Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="78f97-129">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="78f97-129">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        warn:    Using default direction: Inbound
        info:    Looking up the network security rule "rdp-rule"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp
        -rule
        data:    Name                            : rdp-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 3389
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="78f97-130">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="78f97-130">Parameters:</span></span>
   
   * <span data-ttu-id="78f97-131">**-a (veya--nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="78f97-131">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="78f97-132">Kural oluşturulacak NSG adı.</span><span class="sxs-lookup"><span data-stu-id="78f97-132">Name of the NSG in which the rule will be created.</span></span> <span data-ttu-id="78f97-133">Bizim senaryomuz için *NSG ön uç*.</span><span class="sxs-lookup"><span data-stu-id="78f97-133">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="78f97-134">**-n (veya --name)**.</span><span class="sxs-lookup"><span data-stu-id="78f97-134">**-n (or --name)**.</span></span> <span data-ttu-id="78f97-135">Yeni kural için bir ad.</span><span class="sxs-lookup"><span data-stu-id="78f97-135">Name for the new rule.</span></span> <span data-ttu-id="78f97-136">Bizim senaryomuz için *rdp kural*.</span><span class="sxs-lookup"><span data-stu-id="78f97-136">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="78f97-137">**-c (veya--erişim)**.</span><span class="sxs-lookup"><span data-stu-id="78f97-137">**-c (or --access)**.</span></span> <span data-ttu-id="78f97-138">Kural (Engelle veya izin ver) için erişim düzeyi.</span><span class="sxs-lookup"><span data-stu-id="78f97-138">Access level for the rule (Deny or Allow).</span></span>
   * <span data-ttu-id="78f97-139">**-p (veya--Protokolü)**.</span><span class="sxs-lookup"><span data-stu-id="78f97-139">**-p (or --protocol)**.</span></span> <span data-ttu-id="78f97-140">Protokolü (Tcp, Udp veya *) kuralı için.</span><span class="sxs-lookup"><span data-stu-id="78f97-140">Protocol (Tcp, Udp, or *) for the rule.</span></span>
   * <span data-ttu-id="78f97-141">**-r (veya--yönü)**.</span><span class="sxs-lookup"><span data-stu-id="78f97-141">**-r (or --direction)**.</span></span> <span data-ttu-id="78f97-142">Bağlantı (gelen veya giden) yönü.</span><span class="sxs-lookup"><span data-stu-id="78f97-142">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="78f97-143">**-y (veya--öncelik)**.</span><span class="sxs-lookup"><span data-stu-id="78f97-143">**-y (or --priority)**.</span></span> <span data-ttu-id="78f97-144">Kural için öncelik.</span><span class="sxs-lookup"><span data-stu-id="78f97-144">Priority for the rule.</span></span>
   * <span data-ttu-id="78f97-145">**-f (veya--kaynak adres öneki)**.</span><span class="sxs-lookup"><span data-stu-id="78f97-145">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="78f97-146">Kaynak adres ön eki CIDR veya varsayılan etiketleri kullanarak.</span><span class="sxs-lookup"><span data-stu-id="78f97-146">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="78f97-147">**-o (veya--kaynak bağlantı noktası aralığı)**.</span><span class="sxs-lookup"><span data-stu-id="78f97-147">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="78f97-148">Kaynak bağlantı noktası veya bağlantı noktası aralığı.</span><span class="sxs-lookup"><span data-stu-id="78f97-148">Source port, or port range.</span></span>
   * <span data-ttu-id="78f97-149">**-e (veya--hedef adres öneki)**.</span><span class="sxs-lookup"><span data-stu-id="78f97-149">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="78f97-150">Hedef adres ön eki CIDR veya varsayılan etiketleri kullanarak.</span><span class="sxs-lookup"><span data-stu-id="78f97-150">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="78f97-151">**-u (veya--hedef bağlantı noktası aralığı)**.</span><span class="sxs-lookup"><span data-stu-id="78f97-151">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="78f97-152">Hedef bağlantı noktası veya bağlantı noktası aralığı.</span><span class="sxs-lookup"><span data-stu-id="78f97-152">Destination port, or port range.</span></span>    
5. <span data-ttu-id="78f97-153">Çalıştırma **azure ağ nsg kuralı oluşturma** erişim bağlantı noktası 80 (HTTP) Internet'ten sağlayan bir kural oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="78f97-153">Run the **azure network nsg rule create** command to create a rule that allows access to port 80 (HTTP) from the Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="78f97-154">Beklenen putput:</span><span class="sxs-lookup"><span data-stu-id="78f97-154">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 80
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="78f97-155">Çalıştırma **azure ağ sanal alt ağ kümesi** NSG ön uç alt ağına bağlamak için komutu.</span><span class="sxs-lookup"><span data-stu-id="78f97-155">Run the **azure network vnet subnet set** command to link the NSG to the front end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    <span data-ttu-id="78f97-156">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="78f97-156">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up the subnet "FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="78f97-157">Arka uç alt ağı için NSG oluşturma</span><span class="sxs-lookup"><span data-stu-id="78f97-157">How to create the NSG for the back end subnet</span></span>
<span data-ttu-id="78f97-158">Adlı adlı bir NSG oluşturmak için *NSG arka uç* yukarıdaki senaryoya bağlı olarak, aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="78f97-158">To create an NSG named named *NSG-BackEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="78f97-159">Çalıştırma **azure ağ nsg oluşturma** bir NSG oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="78f97-159">Run the **azure network nsg create** command to create an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    <span data-ttu-id="78f97-160">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="78f97-160">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd
        data:    Name                            : NSG-BackEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
2. <span data-ttu-id="78f97-161">Çalıştırma **azure ağ nsg kuralını** ön uç alt ağından bağlantı noktası 1433 (SQL) erişim sağlayan bir kural oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="78f97-161">Run the **azure network nsg rule create** command to create a rule that allows access to port 1433 (SQL) from the front end subnet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="78f97-162">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="78f97-162">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "sql-rule"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule
        data:    Name                            : sql-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 1433
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="78f97-163">Çalıştırma **azure ağ nsg kuralı oluşturma** Internet'ten için erişimini engellediği bir kural oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="78f97-163">Run the **azure network nsg rule create** command to create a rule that denies access to the Internet from.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    <span data-ttu-id="78f97-164">Beklenen putput:</span><span class="sxs-lookup"><span data-stu-id="78f97-164">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : *
        data:    Source Port                     : *
        data:    Destination IP                  : Internet
        data:    Destination Port                : *
        data:    Protocol                        : *
        data:    Direction                       : Outbound
        data:    Access                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="78f97-165">Çalıştırma **azure ağ sanal alt ağ kümesi** NSG arka uç alt ağına bağlamak için komutu.</span><span class="sxs-lookup"><span data-stu-id="78f97-165">Run the **azure network vnet subnet set** command to link the NSG to the back end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    <span data-ttu-id="78f97-166">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="78f97-166">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Setting subnet "BackEnd"
        info:    Looking up the subnet "BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/BackEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : BackEnd
        data:    Address prefix                  : 192.168.2.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL1/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL2/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

