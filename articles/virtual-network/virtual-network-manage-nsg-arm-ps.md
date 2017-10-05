---
title: "Ağ güvenlik grupları - Azure PowerShell yönetme | Microsoft Docs"
description: "Ağ güvenlik grupları PowerShell kullanarak yönetmeyi öğrenin."
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
ms.openlocfilehash: ca7f4926ca4edf9d20612aca74f6ae5f0ed847b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="c677a-103">PowerShell kullanarak ağ güvenlik gruplarını yönet</span><span class="sxs-lookup"><span data-stu-id="c677a-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="c677a-104">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c677a-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c677a-105">Bu makalede, Klasik dağıtım modeli yerine en yeni dağıtımlar için Microsoft önerir Resource Manager dağıtım modelini kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="c677a-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="c677a-106">Bilgi alma</span><span class="sxs-lookup"><span data-stu-id="c677a-106">Retrieve Information</span></span>
<span data-ttu-id="c677a-107">Varolan Nsg'lerinizi görüntülemek için varolan bir NSG kuralları almak ve hangi kaynakların bir NSG için ilişkili olduğunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c677a-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="c677a-108">Varolan Nsg'ler görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="c677a-108">View existing NSGs</span></span>
<span data-ttu-id="c677a-109">Bir Abonelikteki tüm mevcut Nsg'ler görüntülemek için çalıştırın `Get-AzureRmNetworkSecurityGroup` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c677a-109">To view all existing NSGs in a subscription, run the `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="c677a-110">Beklenen sonucu:</span><span class="sxs-lookup"><span data-stu-id="c677a-110">Expected result:</span></span>

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


<span data-ttu-id="c677a-111">Belirli bir kaynak grubunda Nsg'ler listesini görüntülemek için Çalıştır `Get-AzureRmNetworkSecurityGroup` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c677a-111">To view the list of NSGs in a specific resource group, run the `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="c677a-112">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="c677a-112">Expected output:</span></span>

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

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="c677a-113">Bir NSG için tüm kuralları listesinde</span><span class="sxs-lookup"><span data-stu-id="c677a-113">List all rules for an NSG</span></span>
<span data-ttu-id="c677a-114">Adlı bir NSG kurallarını görüntülemek için **NSG ön uç**, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="c677a-114">To view the rules of an NSG named **NSG-FrontEnd**, enter the following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="c677a-115">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="c677a-115">Expected output:</span></span>

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
> <span data-ttu-id="c677a-116">Aynı zamanda `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` varsayılan kurallar listelemek için **NSG ön uç** NSG.</span><span class="sxs-lookup"><span data-stu-id="c677a-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` to list the default rules from the **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="c677a-117">Nsg'ler ilişkilendirmelerini görüntülemek</span><span class="sxs-lookup"><span data-stu-id="c677a-117">View NSGs associations</span></span>
<span data-ttu-id="c677a-118">Hangi kaynakları görüntülemek için **NSG ön uç** NSG olan ilişkilendirmek, aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-118">To view what resources the **NSG-FrontEnd** NSG is associate with, run the following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="c677a-119">Ara **NetworkInterfaces** ve **alt ağlar** aşağıda gösterildiği gibi özellikleri:</span><span class="sxs-lookup"><span data-stu-id="c677a-119">Look for the **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="c677a-120">Önceki örnekte, NSG herhangi ağ arabirimlerine (NIC'ler); ilişkili değil adlı bir alt ağ ile ilişkilendirilene **ön uç**.</span><span class="sxs-lookup"><span data-stu-id="c677a-120">In the previous example, the NSG is not associated to any network interfaces (NICs); it is associated to a subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="c677a-121">Kuralları yönetme</span><span class="sxs-lookup"><span data-stu-id="c677a-121">Manage rules</span></span>
<span data-ttu-id="c677a-122">Varolan bir NSG kuralları ekleme, mevcut kuralları düzenlemek ve kuralları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="c677a-122">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="c677a-123">Kural ekleme</span><span class="sxs-lookup"><span data-stu-id="c677a-123">Add a rule</span></span>
<span data-ttu-id="c677a-124">İzin verme kuralı eklemek için **gelen** bağlantı noktası trafiği **443** için herhangi bir makineden **NSG ön uç** NSG, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="c677a-124">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, complete the following steps:</span></span>

1. <span data-ttu-id="c677a-125">Varolan NSG almak ve bir değişkeni depolamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-125">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="c677a-126">NSG'yi bir kural eklemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-126">Run the following command to add a rule to the NSG:</span></span>

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

3. <span data-ttu-id="c677a-127">NSG'yi yapılan değişiklikleri kaydetmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-127">To save the changes made to the NSG, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="c677a-128">Yalnızca güvenlik kuralları gösteren beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="c677a-128">Expected output showing only the security rules:</span></span>
   
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

### <a name="change-a-rule"></a><span data-ttu-id="c677a-129">Bir kural değiştirme</span><span class="sxs-lookup"><span data-stu-id="c677a-129">Change a rule</span></span>
<span data-ttu-id="c677a-130">Öğesinden gelen trafiğe izin vermek için yukarıda oluşturduğunuz kural değiştirmek için **Internet** yalnızca, aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="c677a-130">To change the rule created above to allow inbound traffic from the **Internet** only, follow the steps below.</span></span>

1. <span data-ttu-id="c677a-131">Varolan NSG almak ve bir değişkeni depolamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-131">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="c677a-132">Yeni Kural ayarlarıyla aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-132">Run the following command with the new rule settings:</span></span>

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

3. <span data-ttu-id="c677a-133">NSG'yi yapılan değişiklikleri kaydetmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-133">To save the changes made to the NSG, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="c677a-134">Yalnızca güvenlik kuralları gösteren beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="c677a-134">Expected output showing only the security rules:</span></span>
   
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

### <a name="delete-a-rule"></a><span data-ttu-id="c677a-135">Kural silme</span><span class="sxs-lookup"><span data-stu-id="c677a-135">Delete a rule</span></span>
1. <span data-ttu-id="c677a-136">Varolan NSG almak ve bir değişkeni depolamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-136">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="c677a-137">NSG kuralı kaldırmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-137">Run the following command to remove the rule from the NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="c677a-138">Aşağıdaki komutu çalıştırarak NSG'yi, yaptığınız değişiklikleri kaydedin:</span><span class="sxs-lookup"><span data-stu-id="c677a-138">Save the changes made to the NSG, by running the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="c677a-139">Beklenen çıktı bildirimi yalnızca güvenlik kuralları gösteren **https kuralı** artık listelenir:</span><span class="sxs-lookup"><span data-stu-id="c677a-139">Expected output showing only the security rules, notice the **https-rule** is no longer listed:</span></span>
   
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

## <a name="manage-associations"></a><span data-ttu-id="c677a-140">İlişkileri yönetme</span><span class="sxs-lookup"><span data-stu-id="c677a-140">Manage associations</span></span>
<span data-ttu-id="c677a-141">Bir NSG'yi alt ağlara ve NIC ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c677a-141">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="c677a-142">Bir NSG'yi ilişkili olduğu herhangi bir kaynaktan ilişkisini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="c677a-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="c677a-143">Bir NSG'yi bir NIC ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="c677a-143">Associate an NSG to a NIC</span></span>
<span data-ttu-id="c677a-144">İlişkilendirilecek **NSG ön uç** NSG'yi **TestNICWeb1** NIC, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="c677a-144">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="c677a-145">Varolan NSG almak ve bir değişkeni depolamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-145">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="c677a-146">Mevcut NIC'in almak ve bir değişkeni depolamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-146">Run the following command to retrieve the existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="c677a-147">Ayarlama **NetworkSecurityGroup** özelliği **NIC** değişken değerini **NSG** değişken, aşağıdaki komutu girerek:</span><span class="sxs-lookup"><span data-stu-id="c677a-147">Set the **NetworkSecurityGroup** property of the **NIC** variable to the value of the **NSG** variable, by entering the following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="c677a-148">NIC'ye yapılan değişiklikleri kaydetmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-148">To save the changes made to the NIC, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="c677a-149">Çıktı yalnızca gösteren beklenen **NetworkSecurityGroup** özelliği:</span><span class="sxs-lookup"><span data-stu-id="c677a-149">Expected output showing only the **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="c677a-150">Bir NSG'yi bir NIC gelen ilişkilendirmesini Kaldır</span><span class="sxs-lookup"><span data-stu-id="c677a-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="c677a-151">İlişkilendirmesini kaldırmak **NSG ön uç** NSG gelen **TestNICWeb1** NIC, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="c677a-151">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="c677a-152">Mevcut NIC'in almak ve bir değişkeni depolamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-152">Run the following command to retrieve the existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="c677a-153">Ayarlama **NetworkSecurityGroup** özelliği **NIC** değişkenini **$null** aşağıdaki komutu çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="c677a-153">Set the **NetworkSecurityGroup** property of the **NIC** variable to **$null** by running the following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="c677a-154">NIC'ye yapılan değişiklikleri kaydetmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-154">To save the changes made to the NIC, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="c677a-155">Çıktı yalnızca gösteren beklenen **NetworkSecurityGroup** özelliği:</span><span class="sxs-lookup"><span data-stu-id="c677a-155">Expected output showing only the **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="c677a-156">Bir NSG'yi bir alt ağdan ilişkilendirmesini Kaldır</span><span class="sxs-lookup"><span data-stu-id="c677a-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="c677a-157">İlişkilendirmesini kaldırmak **NSG ön uç** NSG gelen **ön uç** alt ağ, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="c677a-157">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, complete the following steps:</span></span>

1. <span data-ttu-id="c677a-158">Mevcut VNet almak ve bir değişkeni depolamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-158">Run the following command to retrieve the existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="c677a-159">Almak için aşağıdaki komutu çalıştırın **ön uç** alt ağı ve bir değişkende saklayın:</span><span class="sxs-lookup"><span data-stu-id="c677a-159">Run the following command to retrieve the **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="c677a-160">Ayarlama **NetworkSecurityGroup** özelliği **alt** değişkenini **$null** aşağıdaki komutu girerek:</span><span class="sxs-lookup"><span data-stu-id="c677a-160">Set the **NetworkSecurityGroup** property of the **subnet** variable to **$null** by entering the following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="c677a-161">Alt ağa yapılan değişiklikleri kaydetmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-161">To save the changes made to the subnet, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="c677a-162">Beklenen çıktı yalnızca özelliklerini gösteren **ön uç** alt ağ.</span><span class="sxs-lookup"><span data-stu-id="c677a-162">Expected output showing only the properties of the **FrontEnd** subnet.</span></span> <span data-ttu-id="c677a-163">Bir özellik için hiç duyuru **NetworkSecurityGroup**:</span><span class="sxs-lookup"><span data-stu-id="c677a-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
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

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="c677a-164">Bir NSG'yi bir alt ağ ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="c677a-164">Associate an NSG to a subnet</span></span>
<span data-ttu-id="c677a-165">İlişkilendirilecek **NSG ön uç** NSG'yi **FronEnd** alt yeniden, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="c677a-165">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, complete the following steps:</span></span>

1. <span data-ttu-id="c677a-166">Mevcut VNet almak ve bir değişkeni depolamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-166">Run the following command to retrieve the existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="c677a-167">Almak için aşağıdaki komutu çalıştırın **ön uç** alt ağı ve bir değişkende saklayın:</span><span class="sxs-lookup"><span data-stu-id="c677a-167">Run the following command to retrieve the **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="c677a-168">Varolan NSG almak ve bir değişkeni depolamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-168">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="c677a-169">Ayarlama **NetworkSecurityGroup** özelliği **alt** değişkenini **$null** aşağıdaki komutu çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="c677a-169">Set the **NetworkSecurityGroup** property of the **subnet** variable to **$null** by running the following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="c677a-170">Alt ağa yapılan değişiklikleri kaydetmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-170">To save the changes made to the subnet, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="c677a-171">Çıktı yalnızca gösteren beklenen **NetworkSecurityGroup** özelliği **ön uç** alt ağ:</span><span class="sxs-lookup"><span data-stu-id="c677a-171">Expected output showing only the **NetworkSecurityGroup** property of the **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="c677a-172">Bir NSG'yi Sil</span><span class="sxs-lookup"><span data-stu-id="c677a-172">Delete an NSG</span></span>
<span data-ttu-id="c677a-173">Herhangi bir kaynağa ilişkili olmayan bir NSG'yi yalnızca silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c677a-173">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="c677a-174">Bir NSG'yi silmek için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="c677a-174">To delete an NSG, follow the steps below.</span></span>

1. <span data-ttu-id="c677a-175">Bir NSG'yi ilişkili tüm kaynakları denetlemek için çalıştırın `azure network nsg show` gösterildiği gibi [görünüm Nsg'ler ilişkilendirmeleri](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="c677a-175">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="c677a-176">NSG herhangi NIC'ler ilişkiliyse çalıştırmak `azure network nic set` gösterildiği gibi [bir NSG'yi bir NIC gelen ilişkilendirmesini](#Dissociate-an-NSG-from-a-NIC) her NIC için</span><span class="sxs-lookup"><span data-stu-id="c677a-176">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="c677a-177">NSG herhangi bir alt ağ ile ilişkili ise, çalıştırın `azure network vnet subnet set` gösterildiği gibi [bir NSG bir alt ağdan ilişkilendirmesini](#Dissociate-an-NSG-from-a-subnet) her alt ağ için.</span><span class="sxs-lookup"><span data-stu-id="c677a-177">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="c677a-178">NSG silmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c677a-178">To delete the NSG, run the following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="c677a-179">`-Force` Parametresi sağlar silmeyi onaylamak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c677a-179">The `-Force` parameter ensures you don't need to confirm the deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="c677a-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c677a-180">Next steps</span></span>
* <span data-ttu-id="c677a-181">[Günlük kaydını etkinleştir](virtual-network-nsg-manage-log.md) Nsg'ler için.</span><span class="sxs-lookup"><span data-stu-id="c677a-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

