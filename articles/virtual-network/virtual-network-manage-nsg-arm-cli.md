---
title: "Azure CLI 2.0 aaaManage ağ güvenlik grupları - | Microsoft Docs"
description: "Azure komut satırı arabirimi (CLI) 2.0 kullanarak toomanage ağ güvenlik grupları nasıl hello öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed17d314-07e6-4c7f-bcf1-a8a2535d7c14
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a3036b465e1e4049cba00e5e13ce1b479a2301d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="13df5-103">Ağ güvenlik grupları Hello Azure CLI 2.0 kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="13df5-103">Manage network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="13df5-104">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="13df5-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="13df5-105">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="13df5-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="13df5-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için</span><span class="sxs-lookup"><span data-stu-id="13df5-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="13df5-107">[Azure CLI 2.0](#View-existing-NSGs) -bizim gelecek nesil CLI hello kaynak yönetimi dağıtım modeli (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="13df5-107">[Azure CLI 2.0](#View-existing-NSGs) - our next generation CLI for hello resource management deployment model (this article)</span></span>


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="13df5-108">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="13df5-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="13df5-109">Bu makalede, Microsoft hello Klasik dağıtım modeli yerine çoğu yeni dağıtımlar için önerir hello Resource Manager dağıtım modeli kullanılarak kapsar.</span><span class="sxs-lookup"><span data-stu-id="13df5-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a><span data-ttu-id="13df5-110">Önkoşul</span><span class="sxs-lookup"><span data-stu-id="13df5-110">Prerequisite</span></span>
<span data-ttu-id="13df5-111">Henüz henüz, yüklemek ve hello son yapılandırırsanız [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="13df5-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 


## <a name="view-existing-nsgs"></a><span data-ttu-id="13df5-112">Varolan Nsg'ler görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="13df5-112">View existing NSGs</span></span>
<span data-ttu-id="13df5-113">tooview hello listesinde Nsg'ler hello çalıştırmak belirli bir kaynak grubunun, [az ağ nsg listesi](/cli/azure/network/nsg#list) komutunu bir `-o table` çıktı biçimi:</span><span class="sxs-lookup"><span data-stu-id="13df5-113">tooview hello list of NSGs in a specific resource group, run hello [az network nsg list](/cli/azure/network/nsg#list) command with a `-o table` output format:</span></span>

```azurecli
az network nsg list -g RG-NSG -o table
```

<span data-ttu-id="13df5-114">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="13df5-114">Expected output:</span></span>

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="13df5-115">Bir NSG için tüm kuralları listesinde</span><span class="sxs-lookup"><span data-stu-id="13df5-115">List all rules for an NSG</span></span>
<span data-ttu-id="13df5-116">adlı bir NSG tooview hello kuralları **NSG ön uç**çalıştırın hello [az ağ nsg Göster](/cli/azure/network/nsg#show) komutunu kullanarak bir [JMESPATH sorgu filtresi](/cli/azure/query-az-cli2) ve hello `-o table` çıktı biçimi:</span><span class="sxs-lookup"><span data-stu-id="13df5-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello [az network nsg show](/cli/azure/network/nsg#show) command using a [JMESPATH query filter](/cli/azure/query-az-cli2) and hello `-o table` output format:</span></span>

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

<span data-ttu-id="13df5-117">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="13df5-117">Expected output:</span></span>

    Name                           Desc                                                    Access    Direction    DestPortRange    DestAddrPrefix    SrcPortRange    SrcAddrPrefix
    -----------------------------  ------------------------------------------------------  --------  -----------  ---------------  ----------------  --------------  -----------------
    AllowVnetInBound               Allow inbound traffic from all VMs in VNET              Allow     Inbound      *                VirtualNetwork    *               VirtualNetwork
    AllowAzureLoadBalancerInBound  Allow inbound traffic from azure load balancer          Allow     Inbound      *                *                 *               AzureLoadBalancer
    DenyAllInBound                 Deny all inbound traffic                                Deny      Inbound      *                *                 *               *
    AllowVnetOutBound              Allow outbound traffic from all VMs tooall VMs in VNET  Allow     Outbound     *                VirtualNetwork    *               VirtualNetwork
    AllowInternetOutBound          Allow outbound traffic from all VMs tooInternet         Allow     Outbound     *                Internet          *               *
    DenyAllOutBound                Deny all outbound traffic                               Deny      Outbound     *                *                 *               *
    rdp-rule                                                                               Allow     Inbound      3389             *                 *               Internet
    web-rule                                                                               Allow     Inbound      80               *                 *               Internet
> [!NOTE]
> <span data-ttu-id="13df5-118">Aynı zamanda [az ağ nsg kural listesi](/cli/azure/network/nsg/rule#list) toolist yalnızca hello özel kuralları bir NSG.</span><span class="sxs-lookup"><span data-stu-id="13df5-118">You can also use [az network nsg rule list](/cli/azure/network/nsg/rule#list) toolist only hello custom rules from an NSG .</span></span>
>

## <a name="view-nsg-associations"></a><span data-ttu-id="13df5-119">Görünüm NSG ilişkilendirmeleri</span><span class="sxs-lookup"><span data-stu-id="13df5-119">View NSG associations</span></span>

<span data-ttu-id="13df5-120">tooview hangi kaynaklara hello **NSG ön uç** NSG ile çalışma hello olduğu `az network nsg show` komutunu aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="13df5-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `az network nsg show` command as shown below.</span></span> 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

<span data-ttu-id="13df5-121">Merhaba Ara **networkInterfaces** ve **alt ağlar** aşağıda gösterildiği gibi özellikleri:</span><span class="sxs-lookup"><span data-stu-id="13df5-121">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

```json
[
  [
    {
      "addressPrefix": null,
      "etag": null,
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
      "ipConfigurations": null,
      "name": null,
      "networkSecurityGroup": null,
      "provisioningState": null,
      "resourceGroup": "RG-NSG",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  null
]
```

<span data-ttu-id="13df5-122">Merhaba yukarıdaki örnekte, NSG değil hello tooany ağ arabirimlerine (NIC'ler) ilişkili ve adlı ilişkili tooa alt ağıdır **ön uç**.</span><span class="sxs-lookup"><span data-stu-id="13df5-122">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="add-a-rule"></a><span data-ttu-id="13df5-123">Kural ekleme</span><span class="sxs-lookup"><span data-stu-id="13df5-123">Add a rule</span></span>
<span data-ttu-id="13df5-124">izin verme kuralı tooadd **gelen** trafiği tooport **443** tüm makine toohello gelen **NSG ön uç** NSG, komutu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="13df5-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

```azurecli
az network nsg rule create  \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd  \
--name allow-https \
--description "Allow access tooport 443 for HTTPS" \
--access Allow \
--protocol Tcp  \
--direction Inbound \
--priority 102 \
--source-address-prefix "*"  \
--source-port-range "*"  \
--destination-address-prefix "*" \
--destination-port-range "443"
```

<span data-ttu-id="13df5-125">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="13df5-125">Expected output:</span></span>

```json
{
  "access": "Allow",
  "description": "Allow access tooport 443 for HTTPS",
  "destinationAddressPrefix": "*",
  "destinationPortRange": "443",
  "direction": "Inbound",
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
  "name": "allow-https",
  "priority": 102,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

## <a name="change-a-rule"></a><span data-ttu-id="13df5-126">Bir kural değiştirme</span><span class="sxs-lookup"><span data-stu-id="13df5-126">Change a rule</span></span>
<span data-ttu-id="13df5-127">tooallow oluşturulan toochange hello kural hello trafiğinden gelen **Internet** yalnızca hello çalıştırmak [az ağ nsg kural güncelleştirmesi](/cli/azure/network/nsg/rule#update) komutu:</span><span class="sxs-lookup"><span data-stu-id="13df5-127">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command:</span></span>

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

<span data-ttu-id="13df5-128">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="13df5-128">Expected output:</span></span>

```json
{
"access": "Allow",
"description": "Allow access tooport 443 for HTTPS",
"destinationAddressPrefix": "*",
"destinationPortRange": "443",
"direction": "Inbound",
"etag": "W/\"<guid>\"",
"id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
"name": "allow-https",
"priority": 102,
"protocol": "Tcp",
"provisioningState": "Succeeded",
"resourceGroup": "RG-NSG",
"sourceAddressPrefix": "Internet",
"sourcePortRange": "*"
}
```

## <a name="delete-a-rule"></a><span data-ttu-id="13df5-129">Kural silme</span><span class="sxs-lookup"><span data-stu-id="13df5-129">Delete a rule</span></span>
<span data-ttu-id="13df5-130">Merhaba aşağıdaki komutu çalıştırın, yukarıda toodelete hello kuralı oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="13df5-130">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="13df5-131">Bir NSG tooa NIC ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="13df5-131">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="13df5-132">tooassociate hello **NSG ön uç** NSG toohello **TestNICWeb1** NIC, kullanım hello [az ağ NIC güncelleştirmesi](/cli/azure/network/nic#update) komutu:</span><span class="sxs-lookup"><span data-stu-id="13df5-132">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, use hello [az network nic update](/cli/azure/network/nic#update) command:</span></span>

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

<span data-ttu-id="13df5-133">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="13df5-133">Expected output:</span></span>

```json
{
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": [],
    "internalDnsNameLabel": null,
    "internalDomainNameSuffix": "k0wkaguidnqrh0ud.gx.internal.cloudapp.net",
    "internalFqdn": null
  },
  "enableAcceleratedNetworking": false,
  "enableIpForwarding": false,
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1",
  "ipConfigurations": [
    {
      "applicationGatewayBackendAddressPools": null,
      "etag": "W/\"<guid>\"",
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1",
      "loadBalancerBackendAddressPools": null,
      "loadBalancerInboundNatRules": null,
      "name": "ipconfig1",
      "primary": true,
      "privateIpAddress": "192.168.1.6",
      "privateIpAddressVersion": "IPv4",
      "privateIpAllocationMethod": "Static",
      "provisioningState": "Succeeded",
      "publicIpAddress": null,
      "resourceGroup": "RG-NSG",
      "subnet": {
        "addressPrefix": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
        "ipConfigurations": null,
        "name": null,
        "networkSecurityGroup": null,
        "provisioningState": null,
        "resourceGroup": "RG-NSG",
        "resourceNavigationLinks": null,
        "routeTable": null
      }
    }
  ],
  "location": "centralus",
  "macAddress": "00-0D-3A-91-A9-60",
  "name": "TestNICWeb1",
  "networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  },
  "primary": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "resourceGuid": "<guid>",
  "tags": {},
  "type": "Microsoft.Network/networkInterfaces",
  "virtualMachine": null
}
```

## <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="13df5-134">Bir NSG'yi bir NIC gelen ilişkilendirmesini Kaldır</span><span class="sxs-lookup"><span data-stu-id="13df5-134">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="13df5-135">toodissociate hello **NSG ön uç** hello gelen NSG **TestNICWeb1** hello çalıştırmak NIC [az ağ nsg kural güncelleştirmesi](/cli/azure/network/nsg/rule#update) komutunu yeniden ancak hello yerine `--network-security-group` boş bir dize değişkeni (`""`).</span><span class="sxs-lookup"><span data-stu-id="13df5-135">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

<span data-ttu-id="13df5-136">Merhaba çıktısında hello `networkSecurityGroup` anahtarı toonull ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="13df5-136">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="13df5-137">Bir NSG'yi bir alt ağdan ilişkilendirmesini Kaldır</span><span class="sxs-lookup"><span data-stu-id="13df5-137">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="13df5-138">toodissociate hello **NSG ön uç** hello gelen NSG **ön uç** alt hello yeniden çalıştırın, [az ağ nsg kural güncelleştirmesi](/cli/azure/network/nsg/rule#update) komutunu yeniden ancak hello yerine `--network-security-group` boş bir dize değişkeni (`""`).</span><span class="sxs-lookup"><span data-stu-id="13df5-138">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, again run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

<span data-ttu-id="13df5-139">Merhaba çıktısında hello `networkSecurityGroup` anahtarı toonull ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="13df5-139">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="13df5-140">Bir NSG tooa alt ağını ilişkilendirin</span><span class="sxs-lookup"><span data-stu-id="13df5-140">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="13df5-141">tooassociate hello **NSG ön uç** NSG toohello **ön uç** alt ağ, komutu aşağıdaki hello yeniden çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="13df5-141">tooassociate hello **NSG-FrontEnd** NSG toohello **FrontEnd** subnet again, run hello following command:</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

<span data-ttu-id="13df5-142">Merhaba çıktısında hello `networkSecurityGroup` anahtarı hello değeri için benzer bir şey yok:</span><span class="sxs-lookup"><span data-stu-id="13df5-142">In hello output, hello `networkSecurityGroup` key has something similar for hello value:</span></span>

```json
"networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  }
  ```

## <a name="delete-an-nsg"></a><span data-ttu-id="13df5-143">Bir NSG'yi Sil</span><span class="sxs-lookup"><span data-stu-id="13df5-143">Delete an NSG</span></span>
<span data-ttu-id="13df5-144">Tooany kaynak ilişkili olmayan bir NSG'yi yalnızca silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13df5-144">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="13df5-145">bir NSG'yi toodelete hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="13df5-145">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="13df5-146">Merhaba çalıştırmak tooan NSG, ilişkili toocheck hello kaynakları `azure network nsg show` gösterildiği gibi [görünüm Nsg'ler ilişkilendirmeleri](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="13df5-146">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="13df5-147">Merhaba NSG ilişkili tooany NIC ise, hello çalıştırın `azure network nic set` gösterildiği gibi [bir NSG'yi bir NIC gelen ilişkilendirmesini](#Dissociate-an-NSG-from-a-NIC) her NIC için</span><span class="sxs-lookup"><span data-stu-id="13df5-147">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="13df5-148">Merhaba NSG ilişkili tooany alt ise, hello çalıştırın `azure network vnet subnet set` gösterildiği gibi [bir NSG bir alt ağdan ilişkilendirmesini](#Dissociate-an-NSG-from-a-subnet) her alt ağ için.</span><span class="sxs-lookup"><span data-stu-id="13df5-148">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="13df5-149">toodelete hello NSG, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="13df5-149">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a><span data-ttu-id="13df5-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="13df5-150">Next steps</span></span>
* <span data-ttu-id="13df5-151">[Günlük kaydını etkinleştir](virtual-network-nsg-manage-log.md) Nsg'ler için.</span><span class="sxs-lookup"><span data-stu-id="13df5-151">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

