---
title: "bir Azure Virtual Network - PowerShell - Klasik aaaControl yönlendirme | Microsoft Docs"
description: "Bilgi nasıl toocontrol PowerShell kullanarak Vnet'lerde yönlendirme | Klasik"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 36edf263fb434d5fb13310d4324da20e57f016a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a>Yönlendirme denetlemek ve PowerShell kullanarak sanal gereçler (Klasik) kullanma

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Azure CLI](virtual-network-create-udr-arm-cli.md)
> * [Şablon](virtual-network-create-udr-arm-template.md)
> * [PowerShell (Klasik)](virtual-network-create-udr-classic-ps.md)
> * [CLI (Klasik)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> Azure kaynaklarıyla çalışmadan önce Azure'da şu anda iki dağıtım modeli olduğunu önemli toounderstand olduğu: Azure Resource Manager ve klasik. Azure kaynaklarıyla çalışmadan önce [dağıtım modellerini ve araçlarlarını](../azure-resource-manager/resource-manager-deployment-model.md) iyice anladığınızdan emin olun. Bu makalede hello üstündeki seçeneklerden birini seçerek hello farklı araçlarla ilgili belgeleri görüntüleyebilirsiniz. Bu makalede, hello Klasik dağıtım modeli yer almaktadır.
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

Azure PowerShell önceden oluşturulmuş basit bir ortam aşağıdaki komutları beklediğiniz Hello örnek senaryosunda hello yukarıdaki temel. Bu belgede gösterildiği toorun hello komutları istiyorsanız, gösterildiği hello ortamı oluşturmak [PowerShell kullanarak bir sanal ağ (Klasik) oluşturmak](virtual-networks-create-vnet-classic-netcfg-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Merhaba UDR hello ön uç alt ağ için oluşturma
toocreate hello yol tablosu ve yukarıdaki hello senaryoyu temel hello ön uç alt ağ için gereken rota hello adımları izleyin.

1. Komut toocreate aşağıdaki hello hello ön uç alt ağ için yol tablosu çalıştırın:

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. Tüm giden trafiğe toohello arka uç alt ağ (192.168.2.0/24) toohello komutu toocreate hello rota tablosu toosend rotadaki aşağıdaki hello çalıştırmak **FW1** VM (192.168.0.4):

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. Çalışma hello komutu tooassociate hello yol tablosu hello ile aşağıdaki **ön uç** alt ağ:

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Merhaba UDR hello arka uç alt ağ için oluşturma
toocreate hello yol tablosu ve rota hello yedekleme için gerekli hello senaryoyu temel alt sonlandırmak için hello aşağıdaki adımları tamamlayın:

1. Komut toocreate aşağıdaki hello hello arka uç alt ağ için yol tablosu çalıştırın:

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. Tüm giden trafiğe toohello ön uç alt ağı (192.168.1.0/24) toohello komutu toocreate hello rota tablosu toosend rotadaki aşağıdaki hello çalıştırmak **FW1** VM (192.168.0.4):

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. Çalışma hello komutu tooassociate hello yol tablosu hello ile aşağıdaki **arka uç** alt ağ:

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-hello-fw1-vm"></a>Merhaba FW1 VM üzerinde IP iletimini etkinleştirme

Merhaba FW1 VM, aşağıdaki adımları tam hello tooenable IP iletme:

1. Komut toocheck hello IP iletimini durumunu izleyen hello çalıştırın:

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. Çalışma hello şu komutu tooenable IP iletme hello için *FW1* VM:

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
