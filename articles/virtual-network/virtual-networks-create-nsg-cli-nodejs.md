---
title: "Azure CLI 1.0 aaaCreate ağ güvenlik grupları - | Microsoft Docs"
description: "Bilgi nasıl toocreate ve ağ güvenlik grupları hello Azure CLI 1.0 kullanarak dağıtın."
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
ms.openlocfilehash: eeb7feedab959d92659e03c5c46d93fdfc08faea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="42b3c-103">Ağ güvenlik grupları hello Azure CLI 1.0 kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="42b3c-103">Create network security groups using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="42b3c-104">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="42b3c-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="42b3c-105">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="42b3c-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="42b3c-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="42b3c-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="42b3c-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="42b3c-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="42b3c-108">Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="42b3c-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="42b3c-109">Ayrıca [hello Klasik dağıtım modelinde Nsg'leri oluşturma](virtual-networks-create-nsg-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="42b3c-109">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="42b3c-110">Merhaba aşağıdaki örnek Azure CLI komutları zaten senaryosunda hello yukarıdaki göre oluşturulan basit bir ortam bekler.</span><span class="sxs-lookup"><span data-stu-id="42b3c-110">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> 

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="42b3c-111">Ön uç alt toocreate hello nasıl için NSG hello</span><span class="sxs-lookup"><span data-stu-id="42b3c-111">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="42b3c-112">adlı bir NSG adlı toocreate *NSG ön uç* senaryosunda hello yukarıdaki bağlı olarak, aşağıdaki hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="42b3c-112">toocreate an NSG named named *NSG-FrontEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="42b3c-113">Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="42b3c-113">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="42b3c-114">Merhaba çalıştırmak **azure config modu** aşağıda gösterildiği gibi komut tooswitch tooResource Yöneticisi modu.</span><span class="sxs-lookup"><span data-stu-id="42b3c-114">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="42b3c-115">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="42b3c-115">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="42b3c-116">Merhaba çalıştırmak **azure ağ nsg oluşturma** komutu toocreate bir NSG.</span><span class="sxs-lookup"><span data-stu-id="42b3c-116">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    <span data-ttu-id="42b3c-117">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="42b3c-117">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="42b3c-118">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="42b3c-118">Parameters:</span></span>
   
   * <span data-ttu-id="42b3c-119">**-g (veya --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="42b3c-119">**-g (or --resource-group)**.</span></span> <span data-ttu-id="42b3c-120">Merhaba NSG oluşturulacağı hello kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="42b3c-120">Name of hello resource group where hello NSG will be created.</span></span> <span data-ttu-id="42b3c-121">Bizim senaryomuz için bu *TestRG* ’dir.</span><span class="sxs-lookup"><span data-stu-id="42b3c-121">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="42b3c-122">**-l (veya --location)**.</span><span class="sxs-lookup"><span data-stu-id="42b3c-122">**-l (or --location)**.</span></span> <span data-ttu-id="42b3c-123">Merhaba yeni NSG oluşturulacağı azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="42b3c-123">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="42b3c-124">Bizim senaryomuz için *westus*.</span><span class="sxs-lookup"><span data-stu-id="42b3c-124">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="42b3c-125">**-n (veya --name)**.</span><span class="sxs-lookup"><span data-stu-id="42b3c-125">**-n (or --name)**.</span></span> <span data-ttu-id="42b3c-126">Hello için ad yeni NSG.</span><span class="sxs-lookup"><span data-stu-id="42b3c-126">Name for hello new NSG.</span></span> <span data-ttu-id="42b3c-127">Bizim senaryomuz için *NSG ön uç*.</span><span class="sxs-lookup"><span data-stu-id="42b3c-127">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="42b3c-128">Merhaba çalıştırmak **azure ağ nsg kuralını** komutu toocreate hello Internet gelen erişim tooport 3389 (RDP) sağlayan bir kural.</span><span class="sxs-lookup"><span data-stu-id="42b3c-128">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="42b3c-129">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="42b3c-129">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        warn:    Using default direction: Inbound
        info:    Looking up hello network security rule "rdp-rule"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="42b3c-130">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="42b3c-130">Parameters:</span></span>
   
   * <span data-ttu-id="42b3c-131">**-a (veya--nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="42b3c-131">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="42b3c-132">Hangi hello kuralı oluşturulacak hello NSG adı.</span><span class="sxs-lookup"><span data-stu-id="42b3c-132">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="42b3c-133">Bizim senaryomuz için *NSG ön uç*.</span><span class="sxs-lookup"><span data-stu-id="42b3c-133">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="42b3c-134">**-n (veya --name)**.</span><span class="sxs-lookup"><span data-stu-id="42b3c-134">**-n (or --name)**.</span></span> <span data-ttu-id="42b3c-135">Merhaba yeni kural adı.</span><span class="sxs-lookup"><span data-stu-id="42b3c-135">Name for hello new rule.</span></span> <span data-ttu-id="42b3c-136">Bizim senaryomuz için *rdp kural*.</span><span class="sxs-lookup"><span data-stu-id="42b3c-136">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="42b3c-137">**-c (veya--erişim)**.</span><span class="sxs-lookup"><span data-stu-id="42b3c-137">**-c (or --access)**.</span></span> <span data-ttu-id="42b3c-138">Erişim düzeyi hello kuralın (Engelle veya izin ver).</span><span class="sxs-lookup"><span data-stu-id="42b3c-138">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="42b3c-139">**-p (veya--Protokolü)**.</span><span class="sxs-lookup"><span data-stu-id="42b3c-139">**-p (or --protocol)**.</span></span> <span data-ttu-id="42b3c-140">Protokolü (Tcp, Udp veya *) hello kuralı için.</span><span class="sxs-lookup"><span data-stu-id="42b3c-140">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="42b3c-141">**-r (veya--yönü)**.</span><span class="sxs-lookup"><span data-stu-id="42b3c-141">**-r (or --direction)**.</span></span> <span data-ttu-id="42b3c-142">Bağlantı (gelen veya giden) yönü.</span><span class="sxs-lookup"><span data-stu-id="42b3c-142">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="42b3c-143">**-y (veya--öncelik)**.</span><span class="sxs-lookup"><span data-stu-id="42b3c-143">**-y (or --priority)**.</span></span> <span data-ttu-id="42b3c-144">Merhaba kuralı için öncelik.</span><span class="sxs-lookup"><span data-stu-id="42b3c-144">Priority for hello rule.</span></span>
   * <span data-ttu-id="42b3c-145">**-f (veya--kaynak adres öneki)**.</span><span class="sxs-lookup"><span data-stu-id="42b3c-145">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="42b3c-146">Kaynak adres ön eki CIDR veya varsayılan etiketleri kullanarak.</span><span class="sxs-lookup"><span data-stu-id="42b3c-146">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="42b3c-147">**-o (veya--kaynak bağlantı noktası aralığı)**.</span><span class="sxs-lookup"><span data-stu-id="42b3c-147">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="42b3c-148">Kaynak bağlantı noktası veya bağlantı noktası aralığı.</span><span class="sxs-lookup"><span data-stu-id="42b3c-148">Source port, or port range.</span></span>
   * <span data-ttu-id="42b3c-149">**-e (veya--hedef adres öneki)**.</span><span class="sxs-lookup"><span data-stu-id="42b3c-149">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="42b3c-150">Hedef adres ön eki CIDR veya varsayılan etiketleri kullanarak.</span><span class="sxs-lookup"><span data-stu-id="42b3c-150">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="42b3c-151">**-u (veya--hedef bağlantı noktası aralığı)**.</span><span class="sxs-lookup"><span data-stu-id="42b3c-151">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="42b3c-152">Hedef bağlantı noktası veya bağlantı noktası aralığı.</span><span class="sxs-lookup"><span data-stu-id="42b3c-152">Destination port, or port range.</span></span>    
5. <span data-ttu-id="42b3c-153">Merhaba çalıştırmak **azure ağ nsg kuralını** komutu toocreate hello Internet gelen erişim tooport 80 (HTTP) sağlayan bir kural.</span><span class="sxs-lookup"><span data-stu-id="42b3c-153">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="42b3c-154">Beklenen putput:</span><span class="sxs-lookup"><span data-stu-id="42b3c-154">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
6. <span data-ttu-id="42b3c-155">Merhaba çalıştırmak **azure ağ sanal alt ağ kümesi** komutu toolink hello NSG toohello ön uç alt.</span><span class="sxs-lookup"><span data-stu-id="42b3c-155">Run hello **azure network vnet subnet set** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    <span data-ttu-id="42b3c-156">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="42b3c-156">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
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

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="42b3c-157">Nasıl geri hello toocreate Merhaba NSG bitiş alt ağı</span><span class="sxs-lookup"><span data-stu-id="42b3c-157">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="42b3c-158">adlı bir NSG adlı toocreate *NSG arka uç* senaryosunda hello yukarıdaki bağlı olarak, aşağıdaki hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="42b3c-158">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="42b3c-159">Merhaba çalıştırmak **azure ağ nsg oluşturma** komutu toocreate bir NSG.</span><span class="sxs-lookup"><span data-stu-id="42b3c-159">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    <span data-ttu-id="42b3c-160">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="42b3c-160">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
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
2. <span data-ttu-id="42b3c-161">Merhaba çalıştırmak **azure ağ nsg kuralını** komutu toocreate hello ön uç alt ağından erişim tooport 1433 (SQL) sağlayan bir kural.</span><span class="sxs-lookup"><span data-stu-id="42b3c-161">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="42b3c-162">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="42b3c-162">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "sql-rule"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
3. <span data-ttu-id="42b3c-163">Merhaba çalıştırmak **azure ağ nsg kuralını** komutu toocreate erişim toohello Internet engellediği bir kural gelen.</span><span class="sxs-lookup"><span data-stu-id="42b3c-163">Run hello **azure network nsg rule create** command toocreate a rule that denies access toohello Internet from.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    <span data-ttu-id="42b3c-164">Beklenen putput:</span><span class="sxs-lookup"><span data-stu-id="42b3c-164">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
4. <span data-ttu-id="42b3c-165">Merhaba çalıştırmak **azure ağ sanal alt ağ kümesi** toolink hello NSG toohello geri bitiş alt ağı komutu.</span><span class="sxs-lookup"><span data-stu-id="42b3c-165">Run hello **azure network vnet subnet set** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    <span data-ttu-id="42b3c-166">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="42b3c-166">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Setting subnet "BackEnd"
        info:    Looking up hello subnet "BackEnd"
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

