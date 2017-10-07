---
title: Klasik mod kullanarak Nsg'ler aaaHow toocreate hello Azure CLI | Microsoft Docs
description: "Bilgi nasıl toocreate ve hello Azure CLI kullanarak Klasik modda Nsg'leri dağıtın"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: eb78861e10a0dd950bb2c3783ee957d1cce55016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-nsgs-classic-in-hello-azure-cli"></a>Azure CLI toocreate Nsg'ler (Klasik) nasıl hello
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Bu makalede, hello Klasik dağıtım modeli yer almaktadır. Ayrıca [hello Resource Manager dağıtım modelinde Nsg'leri oluşturma](virtual-networks-create-nsg-arm-cli.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

Merhaba aşağıdaki örnek Azure CLI komutları zaten senaryosunda hello yukarıdaki göre oluşturulan basit bir ortam bekler. Bu belgede gösterildiği toorun hello komutları istiyorsanız, önce hello test ortamı tarafından yapı [bir VNet oluşturma](virtual-networks-create-vnet-classic-cli.md).

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a>Ön uç alt toocreate hello nasıl için NSG hello
adlı bir NSG adlı toocreate **NSG ön uç** senaryosunda hello yukarıdaki bağlı olarak, aşağıdaki hello adımları izleyin.

1. Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.
2. Merhaba çalıştırmak  **`azure config mode`**  aşağıda gösterildiği gibi komut tooswitch tooclassic modu.
   
        azure config mode asm
   
    Beklenen çıktı:
   
        info:    New mode is asm
3. Merhaba çalıştırmak  **`azure network nsg create`**  komutu toocreate bir NSG.
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    Beklenen çıktı:
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    Parametreler:
   
   * **-l (veya --location)**. Merhaba yeni NSG oluşturulacağı azure bölgesi. Bizim senaryomuz için *westus*.
   * **-n (veya --name)**. Hello için ad yeni NSG. Bizim senaryomuz için *NSG ön uç*.
4. Merhaba çalıştırmak  **`azure network nsg rule create`**  komutu toocreate hello Internet gelen erişim tooport 3389 (RDP) sağlayan bir kural.
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    Beklenen çıktı:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    Parametreler:
   
   * **-a (veya--nsg-name)**. Hangi hello kuralı oluşturulacak hello NSG adı. Bizim senaryomuz için *NSG ön uç*.
   * **-n (veya --name)**. Merhaba yeni kural adı. Bizim senaryomuz için *rdp kural*.
   * **-c (veya--eylem)**. Erişim düzeyi hello kuralın (Engelle veya izin ver).
   * **-p (veya--Protokolü)**. Protokolü (Tcp, Udp veya *) hello kuralı için.
   * **-r (veya--türü)**. Bağlantı (gelen veya giden) yönü.
   * **-y (veya--öncelik)**. Merhaba kuralı için öncelik.
   * **-f (veya--kaynak adres öneki)**. Kaynak adres ön eki CIDR veya varsayılan etiketleri kullanarak.
   * **-o (veya--kaynak bağlantı noktası aralığı)**. Kaynak bağlantı noktası veya bağlantı noktası aralığı.
   * **-e (veya--hedef adres öneki)**. Hedef adres ön eki CIDR veya varsayılan etiketleri kullanarak.
   * **-u (veya--hedef bağlantı noktası aralığı)**. Hedef bağlantı noktası veya bağlantı noktası aralığı.
5. Merhaba çalıştırmak  **`azure network nsg rule create`**  komutu toocreate hello Internet gelen erişim tooport 80 (HTTP) sağlayan bir kural.
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    Beklenen putput:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. Merhaba çalıştırmak  **`azure network nsg subnet add`**  komutu toolink hello NSG toohello ön uç alt.
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    Beklenen çıktı:
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a>Nasıl geri hello toocreate Merhaba NSG bitiş alt ağı
adlı bir NSG adlı toocreate *NSG arka uç* senaryosunda hello yukarıdaki bağlı olarak, aşağıdaki hello adımları izleyin.

1. Merhaba çalıştırmak  **`azure network nsg create`**  komutu toocreate bir NSG.
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    Beklenen çıktı:
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    Parametreler:
   
   * **-l (veya --location)**. Merhaba yeni NSG oluşturulacağı azure bölgesi. Bizim senaryomuz için *westus*.
   * **-n (veya --name)**. Hello için ad yeni NSG. Bizim senaryomuz için *NSG ön uç*.
2. Merhaba çalıştırmak  **`azure network nsg rule create`**  komutu toocreate hello ön uç alt ağından erişim tooport 1433 (SQL) sağlayan bir kural.
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    Beklenen çıktı:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. Merhaba çalıştırmak  **`azure network nsg rule create`**  komutu toocreate erişim toohello Internet engellediği bir kural.
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    Beklenen putput:
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. Merhaba çalıştırmak  **`azure network nsg subnet add`**  toolink hello NSG toohello geri bitiş alt ağı komutu.
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    Beklenen çıktı:
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-BackEndX"
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

