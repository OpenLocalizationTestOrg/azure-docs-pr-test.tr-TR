---
title: "bir Azure Virtual Network - CLI - Klasik aaaControl yönlendirme | Microsoft Docs"
description: "Nasıl Azure CLI kullanarak Vnet içinde yönlendirme toocontrol hello Klasik dağıtım modelinde hello öğrenin"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 07dde573f1a605bf280156c261d51e213ede0cdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a>Denetim Yönlendirme ve sanal gereçler (Klasik) kullanarak Azure CLI hello

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Azure CLI](virtual-network-create-udr-arm-cli.md)
> * [Şablon](virtual-network-create-udr-arm-template.md)
> * [PowerShell (Klasik)](virtual-network-create-udr-classic-ps.md)
> * [CLI (Klasik)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Bu makalede, hello Klasik dağıtım modeli yer almaktadır. Ayrıca [kontrol Yönlendirme ve hello Resource Manager dağıtım modelinde sanal gereçler kullanma](virtual-network-create-udr-arm-cli.md).

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

Merhaba aşağıdaki örnek Azure CLI komutları zaten senaryosunda hello yukarıdaki göre oluşturulan basit bir ortam bekler. Bu belgede gösterildiği toorun hello komutları istiyorsanız, gösterildiği hello ortamı oluşturmak [hello Azure CLI kullanarak VNet (Klasik) oluşturma](virtual-networks-create-vnet-classic-cli.md).

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Merhaba UDR hello ön uç alt ağ için oluşturma
toocreate hello yol tablosu ve yukarıdaki hello senaryoyu temel hello ön uç alt ağ için gereken rota hello adımları izleyin.

1. Komut tooswitch tooclassic modu aşağıdaki hello çalıştırın:

    ```azurecli
    azure config mode asm
    ```

    Çıktı:

        info:    New mode is asm

2. Komut toocreate aşağıdaki hello hello ön uç alt ağ için yol tablosu çalıştırın:

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    Çıktı:
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    Parametreler:
   
   * **-l (veya --location)**. Merhaba yeni NSG oluşturulacağı azure bölgesi. Bizim senaryomuz için *westus*.
   * **-n (veya --name)**. Hello için ad yeni NSG. Bizim senaryomuz için *NSG ön uç*.
3. Tüm giden trafiğe toohello arka uç alt ağ (192.168.2.0/24) toohello komutu toocreate hello rota tablosu toosend rotadaki aşağıdaki hello çalıştırmak **FW1** VM (192.168.0.4):

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    Çıktı:
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    Parametreler:
   
   * **-r (veya--yol tablosu adı)**. Merhaba rota ekleneceği hello yol tablosu adı. Bizim senaryomuz için *UDR ön uç*.
   * **-a (veya--adres-önek)**. Paketler için burada hedefleyen hello alt ağ adresi öneki. Bizim senaryomuz için *192.168.2.0/24*.
   * **-t (veya--sonraki atlama türü)**. Nesne trafik türü için gönderilir. Olası değerler şunlardır: *değerinin VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, veya *hiçbiri*.
   * **-p (veya--sonraki atlama IP adresi**). Sonraki atlama IP adresi. Bizim senaryomuz için *192.168.0.4*.
4. Çalışma hello şu komutu tooassociate hello yol tablosu ile Merhaba oluşturulan **ön uç** alt ağ:

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    Çıktı:
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    Parametreler:
   
   * **-t (veya--vnet-ad)**. Merhaba hello alt bulunduğu VNet adı. Bizim senaryomuz için bu *TestVNet* ’tir.
   * **-n (veya--alt ağ adı**. Merhaba alt hello yol tablosu adı eklenir. Bizim senaryomuz için bu *FrontEnd* ’dir.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Merhaba UDR hello arka uç alt ağ için oluşturma
toocreate hello yol tablosu ve hello senaryo, aşağıdaki adımları tam hello hello arka uç alt ağ için gereken yolu:

1. Komut toocreate aşağıdaki hello hello arka uç alt ağ için yol tablosu çalıştırın:

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. Tüm giden trafiğe toohello ön uç alt ağı (192.168.1.0/24) toohello komutu toocreate hello rota tablosu toosend rotadaki aşağıdaki hello çalıştırmak **FW1** VM (192.168.0.4):

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. Çalışma hello komutu tooassociate hello yol tablosu hello ile aşağıdaki **arka uç** alt ağ:

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

