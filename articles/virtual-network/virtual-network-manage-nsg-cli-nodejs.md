---
title: "Azure CLI 1.0 aaaManage ağ güvenlik grupları - | Microsoft Docs"
description: "Azure komut satırı arabirimi (CLI) 1.0 kullanarak toomanage ağ güvenlik grupları nasıl hello öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9a429f947abbcb5fa6adb40c84504f68efd5e20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="e2d26-103">Ağ güvenlik grupları Hello Azure CLI 1.0 kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="e2d26-103">Manage network security groups using hello Azure CLI 1.0</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e2d26-104">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="e2d26-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="e2d26-105">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="e2d26-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="e2d26-106">[Azure CLI 1.0](#View-existing-NSGs) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için</span><span class="sxs-lookup"><span data-stu-id="e2d26-106">[Azure CLI 1.0](#View-existing-NSGs) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="e2d26-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) -bizim gelecek nesil CLI hello kaynak yönetimi dağıtım modeli (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="e2d26-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="e2d26-108">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e2d26-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e2d26-109">Bu makalede, Microsoft hello Klasik dağıtım modeli yerine çoğu yeni dağıtımlar için önerir hello Resource Manager dağıtım modeli kullanılarak kapsar.</span><span class="sxs-lookup"><span data-stu-id="e2d26-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="e2d26-110">Bilgi alma</span><span class="sxs-lookup"><span data-stu-id="e2d26-110">Retrieve Information</span></span>
<span data-ttu-id="e2d26-111">Varolan Nsg'lerinizi görüntülemek için varolan bir NSG kuralları almak ve hangi kaynakların bir NSG için ilişkili olduğunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e2d26-111">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="e2d26-112">Varolan Nsg'ler görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="e2d26-112">View existing NSGs</span></span>
<span data-ttu-id="e2d26-113">tooview hello listesinde Nsg'ler hello çalıştırmak belirli bir kaynak grubunun, `azure network nsg list` komutunu aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="e2d26-113">tooview hello list of NSGs in a specific resource group, run hello `azure network nsg list` command as shown below.</span></span>

```azurecli
azure network nsg list --resource-group RG-NSG
```

<span data-ttu-id="e2d26-114">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="e2d26-114">Expected output:</span></span>

    info:    Executing command network nsg list
    + Getting hello network security groups
    data:    Name          Location
    data:    ------------  --------
    data:    NSG-BackEnd   westus
    data:    NSG-FrontEnd  westus
    info:    network nsg list command OK

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="e2d26-115">Bir NSG için tüm kuralları listesinde</span><span class="sxs-lookup"><span data-stu-id="e2d26-115">List all rules for an NSG</span></span>
<span data-ttu-id="e2d26-116">adlı bir NSG tooview hello kuralları **NSG ön uç**çalıştırın hello `azure network nsg show` komutunu aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="e2d26-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello `azure network nsg show` command as shown below.</span></span> 

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd
```

<span data-ttu-id="e2d26-117">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="e2d26-117">Expected output:</span></span>

    info:    Executing command network nsg show
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Name                            : NSG-FrontEnd
    data:    Type                            : Microsoft.Network/networkSecurityGroups
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    Tags                            : displayName=NSG - Front End
    data:    Security group rules:
    data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
    data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
    data:    rdp-rule                       Internet           *            *               3389              Tcp       Inbound    Allow   100
    data:    web-rule                       Internet           *            *               80                Tcp       Inbound    Allow   101
    data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000
    data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001
    data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500
    data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000
    data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001
    data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500
    info:    network nsg show command OK

> [!NOTE]
> <span data-ttu-id="e2d26-118">Aynı zamanda `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` toolist hello hello kurallardan **NSG ön uç** NSG.</span><span class="sxs-lookup"><span data-stu-id="e2d26-118">You can also use `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` toolist hello rules from hello **NSG-FrontEnd** NSG.</span></span>
>

### <a name="view-nsg-associations"></a><span data-ttu-id="e2d26-119">Görünüm NSG ilişkilendirmeleri</span><span class="sxs-lookup"><span data-stu-id="e2d26-119">View NSG associations</span></span>

<span data-ttu-id="e2d26-120">tooview hangi kaynaklara hello **NSG ön uç** NSG ile çalışma hello olduğu `azure network nsg show` komutunu aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="e2d26-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `azure network nsg show` command as shown below.</span></span> <span data-ttu-id="e2d26-121">Fark hello hello kullanımını, yalnızca o hello fark **--json** parametresi.</span><span class="sxs-lookup"><span data-stu-id="e2d26-121">Notice that hello only difference is hello use of hello **--json** parameter.</span></span>

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json
```

<span data-ttu-id="e2d26-122">Merhaba Ara **networkInterfaces** ve **alt ağlar** aşağıda gösterildiği gibi özellikleri:</span><span class="sxs-lookup"><span data-stu-id="e2d26-122">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

    "networkInterfaces": [],
    ...
    "subnets": [
        {
            "id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
        }
    ],
    ...

<span data-ttu-id="e2d26-123">Merhaba yukarıdaki örnekte, NSG değil hello tooany ağ arabirimlerine (NIC'ler) ilişkili ve adlı ilişkili tooa alt ağıdır **ön uç**.</span><span class="sxs-lookup"><span data-stu-id="e2d26-123">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="e2d26-124">Kuralları yönetme</span><span class="sxs-lookup"><span data-stu-id="e2d26-124">Manage rules</span></span>
<span data-ttu-id="e2d26-125">NSG varolan kuralları tooan eklemek, mevcut kuralları düzenlemek ve kuralları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e2d26-125">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="e2d26-126">Kural ekleme</span><span class="sxs-lookup"><span data-stu-id="e2d26-126">Add a rule</span></span>
<span data-ttu-id="e2d26-127">izin verme kuralı tooadd **gelen** trafiği tooport **443** tüm makine toohello gelen **NSG ön uç** NSG, komutu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="e2d26-127">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

```azurecli
azure network nsg rule create --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --description "Allow access tooport 443 for HTTPS" \
    --protocol Tcp \
    --source-address-prefix * \
    --source-port-range * \
    --destination-address-prefix * \
    --destination-port-range 443 \
    --access Allow \
    --priority 102 \
    --direction Inbound
```

<span data-ttu-id="e2d26-128">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="e2d26-128">Expected output:</span></span>

    info:    Executing command network nsg rule create
    + Looking up hello network security rule "allow-https"
    + Creating a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : *
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule create command OK

### <a name="change-a-rule"></a><span data-ttu-id="e2d26-129">Bir kural değiştirme</span><span class="sxs-lookup"><span data-stu-id="e2d26-129">Change a rule</span></span>
<span data-ttu-id="e2d26-130">tooallow oluşturulan toochange hello kural hello trafiğinden gelen **Internet** yalnızca, çalışma hello komutu aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="e2d26-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello following command:</span></span>

```azurecli
azure network nsg rule set --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --source-address-prefix Internet
```

<span data-ttu-id="e2d26-131">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="e2d26-131">Expected output:</span></span>

    info:    Executing command network nsg rule set
    + Looking up hello network security group "NSG-FrontEnd"
    + Setting a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : Internet
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule set command OK

### <a name="delete-a-rule"></a><span data-ttu-id="e2d26-132">Kural silme</span><span class="sxs-lookup"><span data-stu-id="e2d26-132">Delete a rule</span></span>
<span data-ttu-id="e2d26-133">Merhaba aşağıdaki komutu çalıştırın, yukarıda toodelete hello kuralı oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="e2d26-133">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
azure network nsg rule delete --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --quiet
```

> [!NOTE]
> <span data-ttu-id="e2d26-134">Merhaba `--quiet` parametre sağlar tooconfirm hello silme gerekmez.</span><span class="sxs-lookup"><span data-stu-id="e2d26-134">hello `--quiet` parameter ensures you don't need tooconfirm hello deletion.</span></span>
>

<span data-ttu-id="e2d26-135">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="e2d26-135">Expected output:</span></span>

    info:    Executing command network nsg rule delete
    + Looking up hello network security group "NSG-FrontEnd"
    + Deleting network security rule "allow-https"
    info:    network nsg rule delete command OK

## <a name="manage-associations"></a><span data-ttu-id="e2d26-136">İlişkileri yönetme</span><span class="sxs-lookup"><span data-stu-id="e2d26-136">Manage associations</span></span>
<span data-ttu-id="e2d26-137">Bir NSG toosubnets ve NIC ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2d26-137">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="e2d26-138">Bir NSG'yi ilişkili olduğu herhangi bir kaynaktan ilişkisini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e2d26-138">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="e2d26-139">Bir NSG tooa NIC ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="e2d26-139">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="e2d26-140">tooassociate hello **NSG ön uç** NSG toohello **TestNICWeb1** NIC, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e2d26-140">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, run hello following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG \
    --name TestNICWeb1 \
    --network-security-group-name NSG-FrontEnd
```

<span data-ttu-id="e2d26-141">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="e2d26-141">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Looking up hello network security group "NSG-FrontEnd"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Network security group          : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Virtual machine                 : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="e2d26-142">Bir NSG'yi bir NIC gelen ilişkilendirmesini Kaldır</span><span class="sxs-lookup"><span data-stu-id="e2d26-142">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="e2d26-143">toodissociate hello **NSG ön uç** hello gelen NSG **TestNICWeb1** NIC, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e2d26-143">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG --name TestNICWeb1 --network-security-group-id ""
```

> [!NOTE]
> <span data-ttu-id="e2d26-144">Bildirim hello "" Merhaba (boş) değeri `network-security-group-id` parametresi.</span><span class="sxs-lookup"><span data-stu-id="e2d26-144">Notice hello "" (empty) value for hello `network-security-group-id` parameter.</span></span> <span data-ttu-id="e2d26-145">Bir ilişkilendirme tooan NSG kaldırma olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="e2d26-145">That is how you remove an association tooan NSG.</span></span> <span data-ttu-id="e2d26-146">Yapamayacağınız aynı hello ile Merhaba `network-security-group-name` parametresi.</span><span class="sxs-lookup"><span data-stu-id="e2d26-146">You can't do hello same with hello `network-security-group-name` parameter.</span></span>
> 

<span data-ttu-id="e2d26-147">Beklenen sonucu:</span><span class="sxs-lookup"><span data-stu-id="e2d26-147">Expected result:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="e2d26-148">Bir NSG'yi bir alt ağdan ilişkilendirmesini Kaldır</span><span class="sxs-lookup"><span data-stu-id="e2d26-148">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="e2d26-149">toodissociate hello **NSG ön uç** hello gelen NSG **ön uç** alt ağ, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e2d26-149">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, run hello following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-id ""
```

<span data-ttu-id="e2d26-150">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="e2d26-150">Expected output:</span></span>

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "FrontEnd"
    + Setting subnet "FrontEnd"
    + Looking up hello subnet "FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:    Type                            : Microsoft.Network/virtualNetworks/subnets
    data:    ProvisioningState               : Succeeded
    data:    Name                            : FrontEnd
    data:    Address prefix                  : 192.168.1.0/24
    data:    IP configurations:
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
    data:
    info:    network vnet subnet set command OK

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="e2d26-151">Bir NSG tooa alt ağını ilişkilendirin</span><span class="sxs-lookup"><span data-stu-id="e2d26-151">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="e2d26-152">tooassociate hello **NSG ön uç** NSG toohello **FronEnd** alt ağ, komutu aşağıdaki hello yeniden çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e2d26-152">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, run hello following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-name NSG-FronEnd
```

> [!NOTE]
> <span data-ttu-id="e2d26-153">Merhaba yukarıdaki komutu yalnızca çalışır çünkü hello **NSG ön uç** NSG olan hello hello sanal ağ ile aynı kaynak grubunda **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="e2d26-153">hello command above only works because hello **NSG-FrontEnd** NSG is in hello same resource group as hello virtual network **TestVNet**.</span></span> <span data-ttu-id="e2d26-154">Merhaba NSG farklı bir kaynak grubu içinde ise, toouse hello gereksinim `--network-security-group-id` parametresi bunun yerine ve Merhaba NSG hello tam kimliği sağlayın.</span><span class="sxs-lookup"><span data-stu-id="e2d26-154">If hello NSG is in a different resource group, you need toouse hello `--network-security-group-id` parameter instead, and provide hello full id for hello NSG.</span></span> <span data-ttu-id="e2d26-155">Çalıştırarak hello kimliği alabilir `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` ve Merhaba **kimliği** özelliği.</span><span class="sxs-lookup"><span data-stu-id="e2d26-155">You can retrieve hello id by running `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` and looking for hello **id** property.</span></span> 
> 

<span data-ttu-id="e2d26-156">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="e2d26-156">Expected output:</span></span>

        info:    Executing command network vnet subnet set
        + Looking up hello subnet "FrontEnd"
        + Looking up hello network security group "NSG-FrontEnd"
        + Setting subnet "FrontEnd"
        + Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
        data:
        info:    network vnet subnet set command OK

## <a name="delete-an-nsg"></a><span data-ttu-id="e2d26-157">Bir NSG'yi Sil</span><span class="sxs-lookup"><span data-stu-id="e2d26-157">Delete an NSG</span></span>
<span data-ttu-id="e2d26-158">Tooany kaynak ilişkili olmayan bir NSG'yi yalnızca silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2d26-158">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="e2d26-159">bir NSG'yi toodelete hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e2d26-159">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="e2d26-160">Merhaba çalıştırmak tooan NSG, ilişkili toocheck hello kaynakları `azure network nsg show` gösterildiği gibi [görünüm Nsg'ler ilişkilendirmeleri](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="e2d26-160">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="e2d26-161">Merhaba NSG ilişkili tooany NIC ise, hello çalıştırın `azure network nic set` gösterildiği gibi [bir NSG'yi bir NIC gelen ilişkilendirmesini](#Dissociate-an-NSG-from-a-NIC) her NIC için</span><span class="sxs-lookup"><span data-stu-id="e2d26-161">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="e2d26-162">Merhaba NSG ilişkili tooany alt ise, hello çalıştırın `azure network vnet subnet set` gösterildiği gibi [bir NSG bir alt ağdan ilişkilendirmesini](#Dissociate-an-NSG-from-a-subnet) her alt ağ için.</span><span class="sxs-lookup"><span data-stu-id="e2d26-162">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="e2d26-163">toodelete hello NSG, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e2d26-163">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    azure network nsg delete --resource-group RG-NSG --name NSG-FrontEnd --quiet
    ```

    <span data-ttu-id="e2d26-164">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="e2d26-164">Expected output:</span></span>

        info:    Executing command network nsg delete
        + Looking up hello network security group "NSG-FrontEnd"
        + Deleting network security group "NSG-FrontEnd"
        info:    network nsg delete command OK

## <a name="next-steps"></a><span data-ttu-id="e2d26-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e2d26-165">Next steps</span></span>
* <span data-ttu-id="e2d26-166">[Günlük kaydını etkinleştir](virtual-network-nsg-manage-log.md) Nsg'ler için.</span><span class="sxs-lookup"><span data-stu-id="e2d26-166">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

