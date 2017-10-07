---
title: "sanal ağ - Azure PowerShell aaaCreate | Microsoft Docs"
description: "Nasıl toocreate sanal bir ağ PowerShell'i kullanma hakkında bilgi edinin."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a31f4f12-54ee-4339-b968-1a8097ca77d3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8d6e395a77f71de9f94b6304b05450e46b47544f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-powershell"></a>PowerShell kullanarak bir sanal ağ oluşturma

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure'un iki dağıtım modeli vardır: Azure Resource Manager ve klasik. Microsoft, kaynakları hello Resource Manager dağıtım modeli üzerinden oluşturma önerir. Merhaba iki modelleri arasındaki farklar hakkında daha fazla bilgi toolearn hello okuma hello [anlamak Azure dağıtım modelleri](../azure-resource-manager/resource-manager-deployment-model.md) makalesi.
 
Bu makalede nasıl toocreate bir sanal ağ üzerinden hello Resource Manager dağıtım modeli PowerShell kullanarak açıklanmaktadır. Ayrıca, bir VNet kaynak diğer araçları kullanarak Yöneticisi aracılığıyla oluşturabilir veya liste aşağıdaki hello farklı bir seçeneği seçerek hello Klasik dağıtım modeli üzerinden bir VNet oluşturun:

> [!div class="op_single_selector"]
> * [Portal](virtual-networks-create-vnet-arm-pportal.md)
> * [PowerShell](virtual-networks-create-vnet-arm-ps.md)
> * [CLI](virtual-networks-create-vnet-arm-cli.md)
> * [Şablon](virtual-networks-create-vnet-arm-template-click.md)
> * [Portal (Klasik)](virtual-networks-create-vnet-classic-pportal.md)
> * [PowerShell (Klasik)](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [CLI (Klasik)](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a>Sanal ağ oluşturma

PowerShell, aşağıdaki tam hello kullanarak bir sanal ağ adımları toocreate:

1. Yükleme ve Azure PowerShell hello hello adımları izleyerek yapılandırma [nasıl tooInstall ve yapılandırma Azure PowerShell](/powershell/azure/overview) makalesi.

2. Gerekirse, yeni bir kaynak grubunu aşağıda gösterildiği gibi oluşturun. Bu senaryoda, bir kaynak grubu oluşturma *TestRG*. Kaynak grupları hakkında daha fazla bilgi için [Azure Resource Manager’a Genel Bakış](../azure-resource-manager/resource-group-overview.md)’ı ziyaret edin.

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    Beklenen çıktı:

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. Adlı yeni bir VNet oluşturun *TestVNet*:

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    Beklenen çıktı:

        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                   : W/"[Id]"
        ProvisioningState          : Succeeded
        Tags                       : 
        AddressSpace               : {
                                   "AddressPrefixes": [
                                     "192.168.0.0/16"
                                   ]
                                  }
        DhcpOptions                : {}
        Subnets                    : []
        VirtualNetworkPeerings     : []
4. Merhaba sanal ağ nesnesini bir değişkende saklayın:

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > Adım 3 ve 4 çalıştırarak birleştirebilirsiniz `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.
   > 

5. Bir alt ağ toohello yeni VNet değişkenine ekleyin:

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    Beklenen çıktı:
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {}
        Subnets             : [
                                  {
                                    "Name": "FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24"
                                  }
                                ]
        VirtualNetworkPeerings     : []

6. Yukarıdaki 5. adım yineleme toocreate istediğiniz her alt ağ için. Merhaba aşağıdaki komut oluşturur hello *arka uç* hello senaryo için alt ağ:

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. Alt ağları oluşturmuş olsanız da, bunlar şu anda yalnızca hello yerel değişken kullanılan tooretrieve hello yukarıdaki 4. adımda oluşturduğunuz sanal ağ yok. komutu aşağıdaki hello çalıştırmak toosave hello değişiklikleri tooAzure:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    Beklenen çıktı:
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {
                                  "DnsServers": []
                                }
        Subnets               : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  },
                                  {
                                    "Name": "BackEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                    "AddressPrefix": "192.168.2.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  }
                                ]
        VirtualNetworkPeerings : []

## <a name="next-steps"></a>Sonraki adımlar

Bilgi nasıl tooconnect:

- Merhaba okuyarak sanal makine (VM) tooa sanal ağ [bir Windows VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md) makalesi. Merhaba makaleleri hello adımlarda bir VNet ve alt ağ oluşturmak yerine, bir VM'ye mevcut VNet ve alt ağ tooconnect seçebilirsiniz.
- sanal ağ tooother sanal ağlar hello okuyarak hello [sanal ağlara bağlanma](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) makalesi.
- bir siteden siteye sanal özel ağ (VPN) veya expressroute bağlantı hattı kullanarak hello sanal ağ tooan şirket içi ağ. Bilgi hello okuyarak nasıl [bir siteden siteye VPN kullanarak bir VNet tooan şirket içi ağ bağlanmak](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) ve [VNet tooan expressroute bağlantı hattı bağlantı](../expressroute/expressroute-howto-linkvnet-arm.md) makaleleri.
