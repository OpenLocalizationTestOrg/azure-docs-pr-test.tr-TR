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
# <a name="create-network-security-groups-using-the-azure-cli-10"></a>Ağ güvenlik grupları Azure CLI 1.0 kullanarak oluşturma


## <a name="cli-versions-to-complete-the-task"></a>Görevi tamamlamak için kullanılacak CLI sürümleri 

Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz: 

- [Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – bizim CLI Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) -bizim nesil CLI kaynak yönetimi dağıtım modeli için 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Bu makalede Resource Manager dağıtım modeli anlatılmaktadır. Ayrıca [Klasik dağıtım modelinde Nsg'leri oluşturma](virtual-networks-create-nsg-classic-cli.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

Aşağıdaki örnek Azure CLI komutları yukarıda senaryo tabanlı oluşturulmuş basit bir ortam bekler. 

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a>Ön uç alt ağı için NSG oluşturma
Adlı adlı bir NSG oluşturmak için *NSG ön uç* yukarıdaki senaryoya bağlı olarak, aşağıdaki adımları izleyin.

1. Hiç Azure CLI kullanmadıysanız bkz. [Azure CLI’yi Yükleme ve Yapılandırma](../cli-install-nodejs.md); sonra da, Azure hesabınızı ve aboneliğinizi seçtiğiniz noktaya kadar yönergeleri uygulayın.
2. Resource Manager moduna geçmek için **azure config mode** komutunu aşağıda gösterildiği gibi çalıştırın.
   
        azure config mode arm
   
    Beklenen çıktı:
   
        info:    New mode is arm
3. Çalıştırma **azure ağ nsg oluşturma** bir NSG oluşturmak için komutu.
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    Beklenen çıktı:
   
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
   
    Parametreler:
   
   * **-g (veya --resource-group)**. NSG oluşturulacağı kaynak grubunun adı. Bizim senaryomuz için bu *TestRG* ’dir.
   * **-l (veya --location)**. Yeni NSG oluşturulacağı azure bölgesi. Bizim senaryomuz için *westus*.
   * **-n (veya --name)**. Yeni nsg'nin adı. Bizim senaryomuz için *NSG ön uç*.
4. Çalıştırma **azure ağ nsg kuralını** Internet'ten (RDP) 3389 numaralı bağlantı noktasına erişim sağlayan bir kural oluşturmak için komutu.
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    Beklenen çıktı:
   
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
   
    Parametreler:
   
   * **-a (veya--nsg-name)**. Kural oluşturulacak NSG adı. Bizim senaryomuz için *NSG ön uç*.
   * **-n (veya --name)**. Yeni kural için bir ad. Bizim senaryomuz için *rdp kural*.
   * **-c (veya--erişim)**. Kural (Engelle veya izin ver) için erişim düzeyi.
   * **-p (veya--Protokolü)**. Protokolü (Tcp, Udp veya *) kuralı için.
   * **-r (veya--yönü)**. Bağlantı (gelen veya giden) yönü.
   * **-y (veya--öncelik)**. Kural için öncelik.
   * **-f (veya--kaynak adres öneki)**. Kaynak adres ön eki CIDR veya varsayılan etiketleri kullanarak.
   * **-o (veya--kaynak bağlantı noktası aralığı)**. Kaynak bağlantı noktası veya bağlantı noktası aralığı.
   * **-e (veya--hedef adres öneki)**. Hedef adres ön eki CIDR veya varsayılan etiketleri kullanarak.
   * **-u (veya--hedef bağlantı noktası aralığı)**. Hedef bağlantı noktası veya bağlantı noktası aralığı.    
5. Çalıştırma **azure ağ nsg kuralı oluşturma** erişim bağlantı noktası 80 (HTTP) Internet'ten sağlayan bir kural oluşturmak için komutu.
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    Beklenen putput:
   
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
6. Çalıştırma **azure ağ sanal alt ağ kümesi** NSG ön uç alt ağına bağlamak için komutu.
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    Beklenen çıktı:
   
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

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a>Arka uç alt ağı için NSG oluşturma
Adlı adlı bir NSG oluşturmak için *NSG arka uç* yukarıdaki senaryoya bağlı olarak, aşağıdaki adımları izleyin.

1. Çalıştırma **azure ağ nsg oluşturma** bir NSG oluşturmak için komutu.
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    Beklenen çıktı:
   
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
2. Çalıştırma **azure ağ nsg kuralını** ön uç alt ağından bağlantı noktası 1433 (SQL) erişim sağlayan bir kural oluşturmak için komutu.
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    Beklenen çıktı:
   
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
3. Çalıştırma **azure ağ nsg kuralı oluşturma** Internet'ten için erişimini engellediği bir kural oluşturmak için komutu.
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    Beklenen putput:
   
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
4. Çalıştırma **azure ağ sanal alt ağ kümesi** NSG arka uç alt ağına bağlamak için komutu.
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    Beklenen çıktı:
   
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

