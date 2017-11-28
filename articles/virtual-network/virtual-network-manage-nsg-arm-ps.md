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
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="64a55-103">PowerShell kullanarak ağ güvenlik gruplarını yönet</span><span class="sxs-lookup"><span data-stu-id="64a55-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="64a55-104">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="64a55-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="64a55-105">Bu makalede, Microsoft hello Klasik dağıtım modeli yerine çoğu yeni dağıtımlar için önerir hello Resource Manager dağıtım modeli kullanılarak kapsar.</span><span class="sxs-lookup"><span data-stu-id="64a55-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="64a55-106">Bilgi alma</span><span class="sxs-lookup"><span data-stu-id="64a55-106">Retrieve Information</span></span>
<span data-ttu-id="64a55-107">Varolan Nsg'lerinizi görüntülemek için varolan bir NSG kuralları almak ve hangi kaynakların bir NSG için ilişkili olduğunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="64a55-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="64a55-108">Varolan Nsg'ler görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="64a55-108">View existing NSGs</span></span>
<span data-ttu-id="64a55-109">tooview bir Abonelikteki tüm mevcut Nsg'ler çalıştırmak hello `Get-AzureRmNetworkSecurityGroup` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="64a55-109">tooview all existing NSGs in a subscription, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="64a55-110">Beklenen sonucu:</span><span class="sxs-lookup"><span data-stu-id="64a55-110">Expected result:</span></span>

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


<span data-ttu-id="64a55-111">tooview hello listesinde Nsg'ler hello çalıştırmak belirli bir kaynak grubunun, `Get-AzureRmNetworkSecurityGroup` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="64a55-111">tooview hello list of NSGs in a specific resource group, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="64a55-112">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="64a55-112">Expected output:</span></span>

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

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="64a55-113">Bir NSG için tüm kuralları listesinde</span><span class="sxs-lookup"><span data-stu-id="64a55-113">List all rules for an NSG</span></span>
<span data-ttu-id="64a55-114">adlı bir NSG tooview hello kuralları **NSG ön uç**, komutu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="64a55-114">tooview hello rules of an NSG named **NSG-FrontEnd**, enter hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="64a55-115">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="64a55-115">Expected output:</span></span>

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
> <span data-ttu-id="64a55-116">Aynı zamanda `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist hello varsayılan hello kurallardan **NSG ön uç** NSG.</span><span class="sxs-lookup"><span data-stu-id="64a55-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist hello default rules from hello **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="64a55-117">Nsg'ler ilişkilendirmelerini görüntülemek</span><span class="sxs-lookup"><span data-stu-id="64a55-117">View NSGs associations</span></span>
<span data-ttu-id="64a55-118">tooview hangi kaynaklara hello **NSG ön uç** NSG olduğu aşağıdaki komutu ile çalışma hello:</span><span class="sxs-lookup"><span data-stu-id="64a55-118">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="64a55-119">Merhaba Ara **NetworkInterfaces** ve **alt ağlar** aşağıda gösterildiği gibi özellikleri:</span><span class="sxs-lookup"><span data-stu-id="64a55-119">Look for hello **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="64a55-120">Merhaba önceki örnekte hello NSG ilişkili tooany ağ arabirimlerine (NIC'ler); değil adlı ilişkili tooa alt ağıdır **ön uç**.</span><span class="sxs-lookup"><span data-stu-id="64a55-120">In hello previous example, hello NSG is not associated tooany network interfaces (NICs); it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="64a55-121">Kuralları yönetme</span><span class="sxs-lookup"><span data-stu-id="64a55-121">Manage rules</span></span>
<span data-ttu-id="64a55-122">NSG varolan kuralları tooan eklemek, mevcut kuralları düzenlemek ve kuralları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="64a55-122">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="64a55-123">Kural ekleme</span><span class="sxs-lookup"><span data-stu-id="64a55-123">Add a rule</span></span>
<span data-ttu-id="64a55-124">izin verme kuralı tooadd **gelen** trafiği tooport **443** tüm makine toohello gelen **NSG ön uç** NSG, aşağıdaki adımları tam hello:</span><span class="sxs-lookup"><span data-stu-id="64a55-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="64a55-125">NSG varolan komut tooretrieve hello aşağıdaki hello çalıştırın ve bir değişkende saklayın:</span><span class="sxs-lookup"><span data-stu-id="64a55-125">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="64a55-126">Komut tooadd aşağıdaki hello kural toohello NSG çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="64a55-126">Run hello following command tooadd a rule toohello NSG:</span></span>

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

3. <span data-ttu-id="64a55-127">toosave hello değişiklik toohello NSG, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="64a55-127">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="64a55-128">Güvenlik kuralları yalnızca hello gösteren beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="64a55-128">Expected output showing only hello security rules:</span></span>
   
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

### <a name="change-a-rule"></a><span data-ttu-id="64a55-129">Bir kural değiştirme</span><span class="sxs-lookup"><span data-stu-id="64a55-129">Change a rule</span></span>
<span data-ttu-id="64a55-130">tooallow oluşturulan toochange hello kural hello trafiğinden gelen **Internet** yalnızca hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="64a55-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, follow hello steps below.</span></span>

1. <span data-ttu-id="64a55-131">NSG varolan komut tooretrieve hello aşağıdaki hello çalıştırın ve bir değişkende saklayın:</span><span class="sxs-lookup"><span data-stu-id="64a55-131">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="64a55-132">Merhaba yeni kural ayarları komutuyla aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="64a55-132">Run hello following command with hello new rule settings:</span></span>

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

3. <span data-ttu-id="64a55-133">toosave hello değişiklik toohello NSG, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="64a55-133">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="64a55-134">Güvenlik kuralları yalnızca hello gösteren beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="64a55-134">Expected output showing only hello security rules:</span></span>
   
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

### <a name="delete-a-rule"></a><span data-ttu-id="64a55-135">Kural silme</span><span class="sxs-lookup"><span data-stu-id="64a55-135">Delete a rule</span></span>
1. <span data-ttu-id="64a55-136">NSG varolan komut tooretrieve hello aşağıdaki hello çalıştırın ve bir değişkende saklayın:</span><span class="sxs-lookup"><span data-stu-id="64a55-136">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="64a55-137">Hello NSG tooremove hello kuralı çalıştırma hello aşağıdaki komutu:</span><span class="sxs-lookup"><span data-stu-id="64a55-137">Run hello following command tooremove hello rule from hello NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="64a55-138">Merhaba yapılan değişiklikler toohello NSG, komutu aşağıdaki hello çalıştırarak kaydedin:</span><span class="sxs-lookup"><span data-stu-id="64a55-138">Save hello changes made toohello NSG, by running hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="64a55-139">Güvenlik kuralları, bildirim hello yalnızca hello gösteren beklenen çıktı **https kuralı** artık listelenir:</span><span class="sxs-lookup"><span data-stu-id="64a55-139">Expected output showing only hello security rules, notice hello **https-rule** is no longer listed:</span></span>
   
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

## <a name="manage-associations"></a><span data-ttu-id="64a55-140">İlişkileri yönetme</span><span class="sxs-lookup"><span data-stu-id="64a55-140">Manage associations</span></span>
<span data-ttu-id="64a55-141">Bir NSG toosubnets ve NIC ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64a55-141">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="64a55-142">Bir NSG'yi ilişkili olduğu herhangi bir kaynaktan ilişkisini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="64a55-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="64a55-143">Bir NSG tooa NIC ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="64a55-143">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="64a55-144">tooassociate hello **NSG ön uç** NSG toohello **TestNICWeb1** NIC, aşağıdaki adımları tam hello:</span><span class="sxs-lookup"><span data-stu-id="64a55-144">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="64a55-145">NSG varolan komut tooretrieve hello aşağıdaki hello çalıştırın ve bir değişkende saklayın:</span><span class="sxs-lookup"><span data-stu-id="64a55-145">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="64a55-146">NIC varolan komut tooretrieve hello aşağıdaki hello çalıştırın ve bir değişkende saklayın:</span><span class="sxs-lookup"><span data-stu-id="64a55-146">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="64a55-147">Set hello **NetworkSecurityGroup** hello özelliğinin **NIC** hello değişken toohello değerini **NSG** değişken, komut aşağıdaki hello girerek:</span><span class="sxs-lookup"><span data-stu-id="64a55-147">Set hello **NetworkSecurityGroup** property of hello **NIC** variable toohello value of hello **NSG** variable, by entering hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="64a55-148">toosave hello değişiklik toohello NIC, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="64a55-148">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="64a55-149">Beklenen çıktı gösteren yalnızca hello **NetworkSecurityGroup** özelliği:</span><span class="sxs-lookup"><span data-stu-id="64a55-149">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="64a55-150">Bir NSG'yi bir NIC gelen ilişkilendirmesini Kaldır</span><span class="sxs-lookup"><span data-stu-id="64a55-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="64a55-151">toodissociate hello **NSG ön uç** hello gelen NSG **TestNICWeb1** NIC, aşağıdaki adımları tam hello:</span><span class="sxs-lookup"><span data-stu-id="64a55-151">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="64a55-152">NIC varolan komut tooretrieve hello aşağıdaki hello çalıştırın ve bir değişkende saklayın:</span><span class="sxs-lookup"><span data-stu-id="64a55-152">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="64a55-153">Set hello **NetworkSecurityGroup** hello özelliğinin **NIC** değişkeni çok**$null** hello aşağıdaki komutu çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="64a55-153">Set hello **NetworkSecurityGroup** property of hello **NIC** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="64a55-154">toosave hello değişiklik toohello NIC, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="64a55-154">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="64a55-155">Beklenen çıktı gösteren yalnızca hello **NetworkSecurityGroup** özelliği:</span><span class="sxs-lookup"><span data-stu-id="64a55-155">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="64a55-156">Bir NSG'yi bir alt ağdan ilişkilendirmesini Kaldır</span><span class="sxs-lookup"><span data-stu-id="64a55-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="64a55-157">toodissociate hello **NSG ön uç** hello gelen NSG **ön uç** alt ağ, aşağıdaki adımları tam hello:</span><span class="sxs-lookup"><span data-stu-id="64a55-157">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="64a55-158">VNet varolan komut tooretrieve hello aşağıdaki hello çalıştırın ve bir değişkende saklayın:</span><span class="sxs-lookup"><span data-stu-id="64a55-158">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="64a55-159">Çalışma hello komutu tooretrieve hello aşağıdaki **ön uç** alt ağı ve bir değişkende saklayın:</span><span class="sxs-lookup"><span data-stu-id="64a55-159">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="64a55-160">Set hello **NetworkSecurityGroup** hello özelliğinin **alt** değişkeni çok**$null** komutu aşağıdaki hello girerek:</span><span class="sxs-lookup"><span data-stu-id="64a55-160">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by entering hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="64a55-161">toosave hello değişiklik toohello alt ağ, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="64a55-161">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="64a55-162">Yalnızca hello özelliklerini hello gösteren beklenen çıktı **ön uç** alt ağ.</span><span class="sxs-lookup"><span data-stu-id="64a55-162">Expected output showing only hello properties of hello **FrontEnd** subnet.</span></span> <span data-ttu-id="64a55-163">Bir özellik için hiç duyuru **NetworkSecurityGroup**:</span><span class="sxs-lookup"><span data-stu-id="64a55-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
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

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="64a55-164">Bir NSG tooa alt ağını ilişkilendirin</span><span class="sxs-lookup"><span data-stu-id="64a55-164">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="64a55-165">tooassociate hello **NSG ön uç** NSG toohello **FronEnd** yeniden alt ağ, aşağıdaki adımları tam hello:</span><span class="sxs-lookup"><span data-stu-id="64a55-165">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="64a55-166">VNet varolan komut tooretrieve hello aşağıdaki hello çalıştırın ve bir değişkende saklayın:</span><span class="sxs-lookup"><span data-stu-id="64a55-166">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="64a55-167">Çalışma hello komutu tooretrieve hello aşağıdaki **ön uç** alt ağı ve bir değişkende saklayın:</span><span class="sxs-lookup"><span data-stu-id="64a55-167">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="64a55-168">NSG varolan komut tooretrieve hello aşağıdaki hello çalıştırın ve bir değişkende saklayın:</span><span class="sxs-lookup"><span data-stu-id="64a55-168">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="64a55-169">Set hello **NetworkSecurityGroup** hello özelliğinin **alt** değişkeni çok**$null** hello aşağıdaki komutu çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="64a55-169">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="64a55-170">toosave hello değişiklik toohello alt ağ, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="64a55-170">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="64a55-171">Beklenen çıktı gösteren yalnızca hello **NetworkSecurityGroup** hello özelliğinin **ön uç** alt ağ:</span><span class="sxs-lookup"><span data-stu-id="64a55-171">Expected output showing only hello **NetworkSecurityGroup** property of hello **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="64a55-172">Bir NSG'yi Sil</span><span class="sxs-lookup"><span data-stu-id="64a55-172">Delete an NSG</span></span>
<span data-ttu-id="64a55-173">Tooany kaynak ilişkili olmayan bir NSG'yi yalnızca silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64a55-173">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="64a55-174">bir NSG'yi toodelete hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="64a55-174">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="64a55-175">Merhaba çalıştırmak tooan NSG, ilişkili toocheck hello kaynakları `azure network nsg show` gösterildiği gibi [görünüm Nsg'ler ilişkilendirmeleri](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="64a55-175">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="64a55-176">Merhaba NSG ilişkili tooany NIC ise, hello çalıştırın `azure network nic set` gösterildiği gibi [bir NSG'yi bir NIC gelen ilişkilendirmesini](#Dissociate-an-NSG-from-a-NIC) her NIC için</span><span class="sxs-lookup"><span data-stu-id="64a55-176">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="64a55-177">Merhaba NSG ilişkili tooany alt ise, hello çalıştırın `azure network vnet subnet set` gösterildiği gibi [bir NSG bir alt ağdan ilişkilendirmesini](#Dissociate-an-NSG-from-a-subnet) her alt ağ için.</span><span class="sxs-lookup"><span data-stu-id="64a55-177">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="64a55-178">toodelete hello NSG, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="64a55-178">toodelete hello NSG, run hello following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="64a55-179">Merhaba `-Force` parametre sağlar tooconfirm hello silme gerekmez.</span><span class="sxs-lookup"><span data-stu-id="64a55-179">hello `-Force` parameter ensures you don't need tooconfirm hello deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="64a55-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="64a55-180">Next steps</span></span>
* <span data-ttu-id="64a55-181">[Günlük kaydını etkinleştir](virtual-network-nsg-manage-log.md) Nsg'ler için.</span><span class="sxs-lookup"><span data-stu-id="64a55-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

