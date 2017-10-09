---
title: "kullanarak aaaControl Yönlendirme ve sanal gereçler hello Azure CLI 1.0 | Microsoft Docs"
description: "Azure CLI 1.0 kullanarak toocontrol Yönlendirme ve sanal gereçler nasıl hello öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/18/2017
ms.author: jdial
ms.openlocfilehash: 1c8a552d949521fa554880c00405e65fa47a8162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-10"></a>Kullanıcı tanımlı yolları (UDR) hello Azure CLI 1.0 kullanarak oluşturma

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Azure CLI](virtual-network-create-udr-arm-cli.md)
> * [Şablon](virtual-network-create-udr-arm-template.md)
> * [PowerShell (Klasik)](virtual-network-create-udr-classic-ps.md)
> * [CLI (Klasik)](virtual-network-create-udr-classic-cli.md)

Özel Yönlendirme ve sanal gereçler hello Azure CLI kullanarak oluşturun.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi 

CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak: 

- [Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

Merhaba aşağıdaki örnek Azure CLI komutları zaten senaryosunda hello yukarıdaki göre oluşturulan basit bir ortam bekler. Bu belgede gösterildiği toorun hello komutları istiyorsanız, önce hello test ortamı dağıtarak yapı [bu şablonu](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), tıklatın **tooAzure dağıtmak**, hello varsayılan parametre değerlerini değiştirin Gerekirse ve izleme hello yönergelerinde portal hello durumunda.


## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Merhaba UDR hello ön uç alt ağ için oluşturma
toocreate hello yol tablosu ve yukarıdaki hello senaryoyu temel hello ön uç alt ağ için gereken rota hello adımları izleyin.

1. Komut toocreate aşağıdaki hello hello ön uç alt ağ için yol tablosu çalıştırın:

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    Çıktı:
   
        info:    Executing command network route-table create
        info:    Looking up route table "UDR-FrontEnd"
        info:    Creating route table "UDR-FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    Name                            : UDR-FrontEnd
        data:    Type                            : Microsoft.Network/routeTables
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        info:    network route-table create command OK
   
    Parametreler:
   
   * **-g (veya --resource-group)**. Merhaba UDR oluşturulacağı hello kaynak grubunun adı. Bizim senaryomuz için bu *TestRG* ’dir.
   * **-l (veya --location)**. Merhaba yeni UDR oluşturulacağı azure bölgesi. Bizim senaryomuz için *westus*.
   * **-n (veya --name)**. Hello için ad yeni UDR. Bizim senaryomuz için *UDR ön uç*.
2. Tüm giden trafiğe toohello arka uç alt ağ (192.168.2.0/24) toohello komutu toocreate hello rota tablosu toosend rotadaki aşağıdaki hello çalıştırmak **FW1** VM (192.168.0.4):

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    Çıktı:
   
        info:    Executing command network route-table route create
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        info:    Creating route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd/routes/RouteToBackEnd
        data:    Name                            : RouteToBackEnd
        data:    Provisioning state              : Succeeded
        data:    Next hop type                   : VirtualAppliance
        data:    Next hop IP address             : 192.168.0.4
        data:    Address prefix                  : 192.168.2.0/24
        info:    network route-table route create command OK
   
    Parametreler:
   
   * **-r (veya--yol tablosu adı)**. Merhaba rota ekleneceği hello yol tablosu adı. Bizim senaryomuz için *UDR ön uç*.
   * **-a (veya--adres-önek)**. Paketler için burada hedefleyen hello alt ağ adresi öneki. Bizim senaryomuz için *192.168.2.0/24*.
   * **-y (veya--sonraki atlama türü)**. Nesne trafik türü için gönderilir. Olası değerler şunlardır: *değerinin VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, veya *hiçbiri*.
   * **-p (veya--sonraki atlama IP adresi**). Sonraki atlama IP adresi. Bizim senaryomuz için *192.168.0.4*.
3. Çalışma hello şu komutu tooassociate hello yol tablosu ile Merhaba yukarıda oluşturduğunuz **ön uç** alt ağ:

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    Çıktı:
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    Route Table                     : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConf
        igurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConf
        igurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK
   
    Parametreler:
   
   * **-e (veya--vnet-ad)**. Merhaba hello alt bulunduğu VNet adı. Bizim senaryomuz için bu *TestVNet* ’tir.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Merhaba UDR hello arka uç alt ağ için oluşturma
toocreate hello yol tablosu ve yukarıdaki adımları izleyerek tam hello hello senaryoya göre hello arka uç alt ağ için gereken rota:

1. Komut toocreate aşağıdaki hello hello arka uç alt ağ için yol tablosu çalıştırın:

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. Tüm giden trafiğe toohello ön uç alt ağı (192.168.1.0/24) toohello komutu toocreate hello rota tablosu toosend rotadaki aşağıdaki hello çalıştırmak **FW1** VM (192.168.0.4):

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. Çalışma hello komutu tooassociate hello yol tablosu hello ile aşağıdaki **arka uç** alt ağ:

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a>FW1 üstünde IP iletimini etkinleştirme
Merhaba tarafından kullanılan NIC tooenable IP iletme **FW1**tam hello adımları izleyin:

1. İzleyen ve dikkat edin hello değeri hello komutu çalıştırmak **etkinleştirmek IP iletimini**. Çok ayarlanmalıdır*false*.

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    Çıktı:
   
        info:    Executing command network nic show
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : false
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic show command OK
2. Komut tooenable IP iletimini aşağıdaki hello çalıştırın:

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    Çıktı:
   
        info:    Executing command network nic set
        info:    Looking up hello network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : true
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic set command OK
   
    Parametreler:
   
   * **-f (veya--etkinleştir IP İletimi)**. *doğru* veya *false*.

