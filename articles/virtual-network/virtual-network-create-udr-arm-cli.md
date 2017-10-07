---
title: "kullanarak aaaControl Yönlendirme ve sanal gereçler hello Azure CLI 2.0 | Microsoft Docs"
description: "Azure CLI 2.0 kullanarak toocontrol Yönlendirme ve sanal gereçler nasıl hello öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a>Kullanıcı tanımlı yolları (UDR) hello Azure CLI 2.0 kullanarak oluşturma

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Azure CLI](virtual-network-create-udr-arm-cli.md)
> * [Şablon](virtual-network-create-udr-arm-template.md)
> * [PowerShell (Klasik dağıtımı)](virtual-network-create-udr-classic-ps.md)
> * [CLI (Klasik dağıtımı)](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi 

CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak: 

- [Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için 
- [Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) -bizim gelecek nesil CLI hello kaynak yönetimi dağıtım modeli (Bu makalede)

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

Merhaba aşağıdaki örnek Azure CLI komutları zaten senaryosunda hello yukarıdaki göre oluşturulan basit bir ortam bekler. Bu belgede gösterildiği toorun hello komutları istiyorsanız, önce hello test ortamı dağıtarak yapı [bu şablonu](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), tıklatın **tooAzure dağıtmak**, hello varsayılan parametre değerlerini değiştirin Gerekirse ve izleme hello yönergelerinde portal hello durumunda.


## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Merhaba UDR hello ön uç alt ağ için oluşturma
toocreate hello yol tablosu ve yukarıdaki hello senaryoyu temel hello ön uç alt ağ için gereken rota hello adımları izleyin.

1. Merhaba ile Merhaba ön uç alt ağ için bir yol tablosu oluşturmanız [az ağ yol tablosu oluşturmanız](/cli/azure/network/route-table#create) komutu:

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    Çıktı:

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. Tüm giden trafiğe toohello arka uç alt ağ (192.168.2.0/24) toohello gönderir bir yol oluşturma **FW1** hello kullanarak VM (192.168.0.4) [az ağ yol tablosu yol oluşturma](/cli/azure/network/route-table/route#create) komutu:

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    Çıktı:

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    Parametreler:

    * **--yol tablosu adı**. Merhaba rota ekleneceği hello yol tablosu adı. Bizim senaryomuz için *UDR ön uç*.
    * **--Adres-önek**. Paketler için burada hedefleyen hello alt ağ adresi öneki. Bizim senaryomuz için *192.168.2.0/24*.
    * **--sonraki atlama türü**. Nesne trafik türü için gönderilir. Olası değerler şunlardır: *değerinin VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, veya *hiçbiri*.
    * **--sonraki atlama IP adresi**. Sonraki atlama IP adresi. Bizim senaryomuz için *192.168.0.4*.

3. Merhaba çalıştırmak [az ağ sanal ağ alt ağı güncelleştirme](/cli/azure/network/vnet/subnet#update) komutu tooassociate hello yol tablosu ile Merhaba yukarıda oluşturulan **ön uç** alt ağ:

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    Çıktı:

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    Parametreler:
    
    * **--vnet-ad**. Merhaba hello alt bulunduğu VNet adı. Bizim senaryomuz için bu *TestVNet* ’tir.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Merhaba UDR hello arka uç alt ağ için oluşturma

toocreate hello yol tablosu ve yukarıdaki adımları izleyerek tam hello hello senaryoya göre hello arka uç alt ağ için gereken rota:

1. Komut toocreate aşağıdaki hello hello arka uç alt ağ için yol tablosu çalıştırın:

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. Tüm giden trafiğe toohello ön uç alt ağı (192.168.1.0/24) toohello komutu toocreate hello rota tablosu toosend rotadaki aşağıdaki hello çalıştırmak **FW1** VM (192.168.0.4):

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. Çalışma hello komutu tooassociate hello yol tablosu hello ile aşağıdaki **arka uç** alt ağ:

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a>FW1 üstünde IP iletimini etkinleştirme

Merhaba tarafından kullanılan NIC tooenable IP iletme **FW1**tam hello adımları izleyin:

1. Merhaba çalıştırmak [az ağ NIC Göster](/cli/azure/network/nic#show) bir JMESPATH filtre toodisplay hello geçerli komutunu **etkinleştir IP iletimini** değerini **etkinleştirmek IP iletimini**. Çok ayarlanmalıdır*false*.

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    Çıktı:

        false

2. Komut tooenable IP iletimini aşağıdaki hello çalıştırın:

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    Merhaba çıkış akış toohello konsol incelemek veya yalnızca hello belirli yeniden sınayın **enableIpForwarding** değeri:

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    Çıktı:

        true

    Parametreler:

    **--IP iletimini**: *true* veya *false*.

