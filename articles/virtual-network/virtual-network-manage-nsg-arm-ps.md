---
title: "aaaManage ağ güvenlik grupları - Azure PowerShell | Microsoft Docs"
description: "Nasıl toomanage ağ güvenlik grupları PowerShell'i kullanma hakkında bilgi edinin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 930fe5e0827896ad67b24d84e41a5d3f898ba838
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-powershell"></a>PowerShell kullanarak ağ güvenlik gruplarını yönet

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md). Bu makalede, Microsoft hello Klasik dağıtım modeli yerine çoğu yeni dağıtımlar için önerir hello Resource Manager dağıtım modeli kullanılarak kapsar.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a>Bilgi alma
Varolan Nsg'lerinizi görüntülemek için varolan bir NSG kuralları almak ve hangi kaynakların bir NSG için ilişkili olduğunu öğrenin.

### <a name="view-existing-nsgs"></a>Varolan Nsg'ler görüntüleyin
tooview bir Abonelikteki tüm mevcut Nsg'ler çalıştırmak hello `Get-AzureRmNetworkSecurityGroup` cmdlet'i.

Beklenen sonucu:

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


tooview hello listesinde Nsg'ler hello çalıştırmak belirli bir kaynak grubunun, `Get-AzureRmNetworkSecurityGroup` cmdlet'i.

Beklenen çıktı:

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a>Bir NSG için tüm kuralları listesinde
adlı bir NSG tooview hello kuralları **NSG ön uç**, komutu aşağıdaki hello girin:

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

Beklenen çıktı:

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> Aynı zamanda `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist hello varsayılan hello kurallardan **NSG ön uç** NSG.
> 

### <a name="view-nsgs-associations"></a>Nsg'ler ilişkilendirmelerini görüntülemek
tooview hangi kaynaklara hello **NSG ön uç** NSG olduğu aşağıdaki komutu ile çalışma hello:

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

Merhaba Ara **NetworkInterfaces** ve **alt ağlar** aşağıda gösterildiği gibi özellikleri:

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

Merhaba önceki örnekte hello NSG ilişkili tooany ağ arabirimlerine (NIC'ler); değil adlı ilişkili tooa alt ağıdır **ön uç**.

## <a name="manage-rules"></a>Kuralları yönetme
NSG varolan kuralları tooan eklemek, mevcut kuralları düzenlemek ve kuralları kaldırın.

### <a name="add-a-rule"></a>Kural ekleme
izin verme kuralı tooadd **gelen** trafiği tooport **443** tüm makine toohello gelen **NSG ön uç** NSG, aşağıdaki adımları tam hello:

1. NSG varolan komut tooretrieve hello aşağıdaki hello çalıştırın ve bir değişkende saklayın:

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Komut tooadd aşağıdaki hello kural toohello NSG çalıştırın:

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. toosave hello değişiklik toohello NSG, hello aşağıdaki komutu çalıştırın:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    Güvenlik kuralları yalnızca hello gösteren beklenen çıktı:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a>Bir kural değiştirme
tooallow oluşturulan toochange hello kural hello trafiğinden gelen **Internet** yalnızca hello adımları izleyin.

1. NSG varolan komut tooretrieve hello aşağıdaki hello çalıştırın ve bir değişkende saklayın:

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Merhaba yeni kural ayarları komutuyla aşağıdaki hello çalıştırın:

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix Internet `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. toosave hello değişiklik toohello NSG, hello aşağıdaki komutu çalıştırın:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    Güvenlik kuralları yalnızca hello gösteren beklenen çıktı:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a>Kural silme
1. NSG varolan komut tooretrieve hello aşağıdaki hello çalıştırın ve bir değişkende saklayın:

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Hello NSG tooremove hello kuralı çalıştırma hello aşağıdaki komutu:

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. Merhaba yapılan değişiklikler toohello NSG, komutu aşağıdaki hello çalıştırarak kaydedin:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    Güvenlik kuralları, bildirim hello yalnızca hello gösteren beklenen çıktı **https kuralı** artık listelenir:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a>İlişkileri yönetme
Bir NSG toosubnets ve NIC ilişkilendirebilirsiniz. Bir NSG'yi ilişkili olduğu herhangi bir kaynaktan ilişkisini kaldırın.

### <a name="associate-an-nsg-tooa-nic"></a>Bir NSG tooa NIC ilişkilendirme
tooassociate hello **NSG ön uç** NSG toohello **TestNICWeb1** NIC, aşağıdaki adımları tam hello:

1. NSG varolan komut tooretrieve hello aşağıdaki hello çalıştırın ve bir değişkende saklayın:

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. NIC varolan komut tooretrieve hello aşağıdaki hello çalıştırın ve bir değişkende saklayın:

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. Set hello **NetworkSecurityGroup** hello özelliğinin **NIC** hello değişken toohello değerini **NSG** değişken, komut aşağıdaki hello girerek:

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. toosave hello değişiklik toohello NIC, hello aşağıdaki komutu çalıştırın:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    Beklenen çıktı gösteren yalnızca hello **NetworkSecurityGroup** özelliği:
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a>Bir NSG'yi bir NIC gelen ilişkilendirmesini Kaldır
toodissociate hello **NSG ön uç** hello gelen NSG **TestNICWeb1** NIC, aşağıdaki adımları tam hello:

1. NIC varolan komut tooretrieve hello aşağıdaki hello çalıştırın ve bir değişkende saklayın:

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. Set hello **NetworkSecurityGroup** hello özelliğinin **NIC** değişkeni çok**$null** hello aşağıdaki komutu çalıştırarak:

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. toosave hello değişiklik toohello NIC, hello aşağıdaki komutu çalıştırın:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    Beklenen çıktı gösteren yalnızca hello **NetworkSecurityGroup** özelliği:
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a>Bir NSG'yi bir alt ağdan ilişkilendirmesini Kaldır
toodissociate hello **NSG ön uç** hello gelen NSG **ön uç** alt ağ, aşağıdaki adımları tam hello:

1. VNet varolan komut tooretrieve hello aşağıdaki hello çalıştırın ve bir değişkende saklayın:

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. Çalışma hello komutu tooretrieve hello aşağıdaki **ön uç** alt ağı ve bir değişkende saklayın:

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. Set hello **NetworkSecurityGroup** hello özelliğinin **alt** değişkeni çok**$null** komutu aşağıdaki hello girerek:

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. toosave hello değişiklik toohello alt ağ, hello aşağıdaki komutu çalıştırın:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    Yalnızca hello özelliklerini hello gösteren beklenen çıktı **ön uç** alt ağ. Bir özellik için hiç duyuru **NetworkSecurityGroup**:
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-tooa-subnet"></a>Bir NSG tooa alt ağını ilişkilendirin
tooassociate hello **NSG ön uç** NSG toohello **FronEnd** yeniden alt ağ, aşağıdaki adımları tam hello:

1. VNet varolan komut tooretrieve hello aşağıdaki hello çalıştırın ve bir değişkende saklayın:

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. Çalışma hello komutu tooretrieve hello aşağıdaki **ön uç** alt ağı ve bir değişkende saklayın:

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. NSG varolan komut tooretrieve hello aşağıdaki hello çalıştırın ve bir değişkende saklayın:

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. Set hello **NetworkSecurityGroup** hello özelliğinin **alt** değişkeni çok**$null** hello aşağıdaki komutu çalıştırarak:

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. toosave hello değişiklik toohello alt ağ, hello aşağıdaki komutu çalıştırın:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    Beklenen çıktı gösteren yalnızca hello **NetworkSecurityGroup** hello özelliğinin **ön uç** alt ağ:
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a>Bir NSG'yi Sil
Tooany kaynak ilişkili olmayan bir NSG'yi yalnızca silebilirsiniz. bir NSG'yi toodelete hello adımları izleyin.

1. Merhaba çalıştırmak tooan NSG, ilişkili toocheck hello kaynakları `azure network nsg show` gösterildiği gibi [görünüm Nsg'ler ilişkilendirmeleri](#View-NSGs-associations).
2. Merhaba NSG ilişkili tooany NIC ise, hello çalıştırın `azure network nic set` gösterildiği gibi [bir NSG'yi bir NIC gelen ilişkilendirmesini](#Dissociate-an-NSG-from-a-NIC) her NIC için 
3. Merhaba NSG ilişkili tooany alt ise, hello çalıştırın `azure network vnet subnet set` gösterildiği gibi [bir NSG bir alt ağdan ilişkilendirmesini](#Dissociate-an-NSG-from-a-subnet) her alt ağ için.
4. toodelete hello NSG, hello aşağıdaki komutu çalıştırın:

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > Merhaba `-Force` parametre sağlar tooconfirm hello silme gerekmez.
   > 

## <a name="next-steps"></a>Sonraki adımlar
* [Günlük kaydını etkinleştir](virtual-network-nsg-manage-log.md) Nsg'ler için.

