---
title: "aaaCreate ağ güvenlik grupları - Azure PowerShell | Microsoft Docs"
description: "Bilgi nasıl toocreate ve PowerShell kullanarak ağ güvenlik grupları dağıtın."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9cef62b8-d889-4d16-b4d0-58639539a418
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1c8db773febb163d9cb010d23f2913b5ebe0fa94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-powershell"></a><span data-ttu-id="046b8-103">Ağ güvenlik grupları PowerShell kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="046b8-103">Create network security groups using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

<span data-ttu-id="046b8-104">Azure'un iki dağıtım modeli vardır: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="046b8-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="046b8-105">Microsoft, kaynakları hello Resource Manager dağıtım modeli üzerinden oluşturma önerir.</span><span class="sxs-lookup"><span data-stu-id="046b8-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="046b8-106">Merhaba iki modelleri arasındaki farklar hakkında daha fazla bilgi toolearn hello okuma hello [anlamak Azure dağıtım modelleri](../azure-resource-manager/resource-manager-deployment-model.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="046b8-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="046b8-107">Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="046b8-107">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="046b8-108">Ayrıca [hello Klasik dağıtım modelinde Nsg'leri oluşturma](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="046b8-108">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="046b8-109">Merhaba örnek PowerShell önceden oluşturulmuş basit bir ortam aşağıdaki komutları beklediğiniz senaryosunda hello yukarıdaki temel.</span><span class="sxs-lookup"><span data-stu-id="046b8-109">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="046b8-110">Bu belgede gösterildiği toorun hello komutları istiyorsanız, önce hello test ortamı dağıtarak yapı [bu şablonu](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), tıklatın **tooAzure dağıtmak**, hello varsayılan parametre değerlerini değiştirin Gerekirse ve izleme hello yönergelerinde portal hello durumunda.</span><span class="sxs-lookup"><span data-stu-id="046b8-110">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="046b8-111">Ön uç alt toocreate hello nasıl için NSG hello</span><span class="sxs-lookup"><span data-stu-id="046b8-111">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="046b8-112">toocreate adlı bir NSG *NSG ön uç* hello senaryoya bağlı olarak, hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="046b8-112">toocreate an NSG named *NSG-FrontEnd* based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="046b8-113">Azure PowerShell'i hiç kullanmadıysanız bkz [nasıl tooInstall ve yapılandırma Azure PowerShell](/powershell/azure/overview) ve tüm hello yolu toohello toosign Azure'da sonlandırmak ve aboneliğinizi seçin hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="046b8-113">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="046b8-114">Merhaba Internet tooport 3389 erişimden izin veren bir güvenlik kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="046b8-114">Create a security rule allowing access from hello Internet tooport 3389.</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name rdp-rule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
    ```

3. <span data-ttu-id="046b8-115">Merhaba Internet tooport 80 erişimden izin veren bir güvenlik kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="046b8-115">Create a security rule allowing access from hello Internet tooport 80.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule -Description "Allow HTTP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 101 `
    -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80
    ```

4. <span data-ttu-id="046b8-116">Yeni NSG adlı tooa oluşturulan hello kuralları ekleme **NSG ön uç**.</span><span class="sxs-lookup"><span data-stu-id="046b8-116">Add hello rules created above tooa new NSG named **NSG-FrontEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG -Location westus `
    -Name "NSG-FrontEnd" -SecurityRules $rule1,$rule2
    ```

5. <span data-ttu-id="046b8-117">Merhaba aşağıdakileri yazarak Hello NSG oluşturulan hello kurallar denetleyin:</span><span class="sxs-lookup"><span data-stu-id="046b8-117">Check hello rules created in hello NSG by typing hello following:</span></span>

    ```powershell
    $nsg
    ```
   
    <span data-ttu-id="046b8-118">Gösteren yalnızca hello güvenlik kuralları çıktı:</span><span class="sxs-lookup"><span data-stu-id="046b8-118">Output showing just hello security rules:</span></span>
   
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
                                   "Description": "Allow RDP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "3389",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 100,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 },
                                 {
                                   "Name": "web-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
                                   "Description": "Allow HTTP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "80",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 101,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
6. <span data-ttu-id="046b8-119">NSG toohello oluşturulan ilişkilendirme hello *ön uç* alt ağ.</span><span class="sxs-lookup"><span data-stu-id="046b8-119">Associate hello NSG created above toohello *FrontEnd* subnet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="046b8-120">Çıktı gösteren yalnızca hello *ön uç* alt ağ ayarları, hello için bildirim hello değer **NetworkSecurityGroup** özelliği:</span><span class="sxs-lookup"><span data-stu-id="046b8-120">Output showing only hello *FrontEnd* subnet settings, notice hello value for hello **NetworkSecurityGroup** property:</span></span>
   
                    Subnets           : [
                                          {
                                            "Name": "FrontEnd",
                                            "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                            "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                            "AddressPrefix": "192.168.1.0/24",
                                            "IpConfigurations": [
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                              },
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                              }
                                            ],
                                            "NetworkSecurityGroup": {
                                              "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                            },
                                            "RouteTable": null,
                                            "ProvisioningState": "Succeeded"
                                          }
   
   > [!WARNING]
   > <span data-ttu-id="046b8-121">Yukarıdaki hello komutu için Hello çıktı hello içerik yalnızca PowerShell çalıştırdığınız hello bilgisayarda mevcut hello sanal ağ yapılandırma nesnesi için gösterilir.</span><span class="sxs-lookup"><span data-stu-id="046b8-121">hello output for hello command above shows hello content for hello virtual network configuration object, which only exists on hello computer where you are running PowerShell.</span></span> <span data-ttu-id="046b8-122">Toorun hello gereksinim `Set-AzureRmVirtualNetwork` cmdlet toosave bu ayarları tooAzure.</span><span class="sxs-lookup"><span data-stu-id="046b8-122">You need toorun hello `Set-AzureRmVirtualNetwork` cmdlet toosave these settings tooAzure.</span></span>
   > 
   > 
7. <span data-ttu-id="046b8-123">Merhaba yeni VNet ayarlarını tooAzure kaydedin.</span><span class="sxs-lookup"><span data-stu-id="046b8-123">Save hello new VNet settings tooAzure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="046b8-124">Yalnızca hello NSG kısmını gösteren çıktı:</span><span class="sxs-lookup"><span data-stu-id="046b8-124">Output showing just hello NSG portion:</span></span>
   
        "NetworkSecurityGroup": {
          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
        }

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="046b8-125">Nasıl toocreate hello NSG hello arka uç alt ağ için</span><span class="sxs-lookup"><span data-stu-id="046b8-125">How toocreate hello NSG for hello back-end subnet</span></span>
<span data-ttu-id="046b8-126">toocreate adlı bir NSG *NSG arka uç* senaryosunda hello yukarıdaki bağlı olarak, hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="046b8-126">toocreate an NSG named *NSG-BackEnd* based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="046b8-127">Merhaba ön uç alt tooport 1433 (SQL Server tarafından kullanılan varsayılan bağlantı noktası) erişimden izin veren bir güvenlik kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="046b8-127">Create a security rule allowing access from hello front-end subnet tooport 1433 (default port used by SQL Server).</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name frontend-rule `
    -Description "Allow FE subnet" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix 192.168.1.0/24 -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 1433
    ```

2. <span data-ttu-id="046b8-128">Internet erişimi toohello engelleyen bir güvenlik kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="046b8-128">Create a security rule blocking access toohello Internet.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule `
    -Description "Block Internet" `
    -Access Deny -Protocol * -Direction Outbound -Priority 200 `
    -SourceAddressPrefix * -SourcePortRange * `
    -DestinationAddressPrefix Internet -DestinationPortRange *
    ```

3. <span data-ttu-id="046b8-129">Yeni NSG adlı tooa oluşturulan hello kuralları ekleme **NSG arka uç**.</span><span class="sxs-lookup"><span data-stu-id="046b8-129">Add hello rules created above tooa new NSG named **NSG-BackEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG `
    -Location westus -Name "NSG-BackEnd" `
    -SecurityRules $rule1,$rule2
    ```

4. <span data-ttu-id="046b8-130">NSG toohello oluşturulan ilişkilendirme hello *arka uç* alt ağ.</span><span class="sxs-lookup"><span data-stu-id="046b8-130">Associate hello NSG created above toohello *BackEnd* subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd ` 
    -AddressPrefix 192.168.2.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="046b8-131">Çıktı gösteren yalnızca hello *arka uç* alt ağ ayarları, hello için bildirim hello değer **NetworkSecurityGroup** özelliği:</span><span class="sxs-lookup"><span data-stu-id="046b8-131">Output showing only hello *BackEnd* subnet settings, notice hello value for hello **NetworkSecurityGroup** property:</span></span>
   
        Subnets           : [
                      {
                        "Name": "BackEnd",
                        "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                        "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                        "AddressPrefix": "192.168.2.0/24",
                        "IpConfigurations": [...],
                        "NetworkSecurityGroup": {
                          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "RouteTable": null,
                        "ProvisioningState": "Succeeded"
                      }
5. <span data-ttu-id="046b8-132">Merhaba yeni VNet ayarlarını tooAzure kaydedin.</span><span class="sxs-lookup"><span data-stu-id="046b8-132">Save hello new VNet settings tooAzure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

## <a name="how-tooremove-an-nsg"></a><span data-ttu-id="046b8-133">Nasıl tooremove bir NSG</span><span class="sxs-lookup"><span data-stu-id="046b8-133">How tooremove an NSG</span></span>
<span data-ttu-id="046b8-134">adlı toodelete var olan bir NSG *NSG ön uç* bu durumda, aşağıdaki hello adımı izleyin:</span><span class="sxs-lookup"><span data-stu-id="046b8-134">toodelete an existing NSG, called *NSG-Frontend* in this case, follow hello step below:</span></span>

<span data-ttu-id="046b8-135">Merhaba çalıştırmak **Kaldır AzureRmNetworkSecurityGroup** aşağıda gösterilen ve NSG olduğundan emin tooinclude hello kaynak grubu hello.</span><span class="sxs-lookup"><span data-stu-id="046b8-135">Run hello **Remove-AzureRmNetworkSecurityGroup** shown below and be sure tooinclude hello resource group hello NSG is in.</span></span>

```powershell
Remove-AzureRmNetworkSecurityGroup -Name "NSG-FrontEnd" -ResourceGroupName "TestRG"
```

