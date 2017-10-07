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
# <a name="manage-network-security-groups-using-hello-azure-cli-20"></a>Ağ güvenlik grupları Hello Azure CLI 2.0 kullanarak yönetme

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi 

CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak: 

- [Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için 
- [Azure CLI 2.0](#View-existing-NSGs) -bizim gelecek nesil CLI hello kaynak yönetimi dağıtım modeli (Bu makalede)


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md). Bu makalede, Microsoft hello Klasik dağıtım modeli yerine çoğu yeni dağıtımlar için önerir hello Resource Manager dağıtım modeli kullanılarak kapsar.
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a>Önkoşul
Henüz henüz, yüklemek ve hello son yapılandırırsanız [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login). 


## <a name="view-existing-nsgs"></a>Varolan Nsg'ler görüntüleyin
tooview hello listesinde Nsg'ler hello çalıştırmak belirli bir kaynak grubunun, [az ağ nsg listesi](/cli/azure/network/nsg#list) komutunu bir `-o table` çıktı biçimi:

```azurecli
az network nsg list -g RG-NSG -o table
```

Beklenen çıktı:

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a>Bir NSG için tüm kuralları listesinde
adlı bir NSG tooview hello kuralları **NSG ön uç**çalıştırın hello [az ağ nsg Göster](/cli/azure/network/nsg#show) komutunu kullanarak bir [JMESPATH sorgu filtresi](/cli/azure/query-az-cli2) ve hello `-o table` çıktı biçimi:

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

Beklenen çıktı:

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
> Aynı zamanda [az ağ nsg kural listesi](/cli/azure/network/nsg/rule#list) toolist yalnızca hello özel kuralları bir NSG.
>

## <a name="view-nsg-associations"></a>Görünüm NSG ilişkilendirmeleri

tooview hangi kaynaklara hello **NSG ön uç** NSG ile çalışma hello olduğu `az network nsg show` komutunu aşağıda gösterildiği gibi. 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

Merhaba Ara **networkInterfaces** ve **alt ağlar** aşağıda gösterildiği gibi özellikleri:

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

Merhaba yukarıdaki örnekte, NSG değil hello tooany ağ arabirimlerine (NIC'ler) ilişkili ve adlı ilişkili tooa alt ağıdır **ön uç**.

## <a name="add-a-rule"></a>Kural ekleme
izin verme kuralı tooadd **gelen** trafiği tooport **443** tüm makine toohello gelen **NSG ön uç** NSG, komutu aşağıdaki hello girin:

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

Beklenen çıktı:

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

## <a name="change-a-rule"></a>Bir kural değiştirme
tooallow oluşturulan toochange hello kural hello trafiğinden gelen **Internet** yalnızca hello çalıştırmak [az ağ nsg kural güncelleştirmesi](/cli/azure/network/nsg/rule#update) komutu:

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

Beklenen çıktı:

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

## <a name="delete-a-rule"></a>Kural silme
Merhaba aşağıdaki komutu çalıştırın, yukarıda toodelete hello kuralı oluşturuldu:

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-tooa-nic"></a>Bir NSG tooa NIC ilişkilendirme
tooassociate hello **NSG ön uç** NSG toohello **TestNICWeb1** NIC, kullanım hello [az ağ NIC güncelleştirmesi](/cli/azure/network/nic#update) komutu:

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

Beklenen çıktı:

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

## <a name="dissociate-an-nsg-from-a-nic"></a>Bir NSG'yi bir NIC gelen ilişkilendirmesini Kaldır

toodissociate hello **NSG ön uç** hello gelen NSG **TestNICWeb1** hello çalıştırmak NIC [az ağ nsg kural güncelleştirmesi](/cli/azure/network/nsg/rule#update) komutunu yeniden ancak hello yerine `--network-security-group` boş bir dize değişkeni (`""`).

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

Merhaba çıktısında hello `networkSecurityGroup` anahtarı toonull ayarlayın.

## <a name="dissociate-an-nsg-from-a-subnet"></a>Bir NSG'yi bir alt ağdan ilişkilendirmesini Kaldır
toodissociate hello **NSG ön uç** hello gelen NSG **ön uç** alt hello yeniden çalıştırın, [az ağ nsg kural güncelleştirmesi](/cli/azure/network/nsg/rule#update) komutunu yeniden ancak hello yerine `--network-security-group` boş bir dize değişkeni (`""`).

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

Merhaba çıktısında hello `networkSecurityGroup` anahtarı toonull ayarlayın.

## <a name="associate-an-nsg-tooa-subnet"></a>Bir NSG tooa alt ağını ilişkilendirin
tooassociate hello **NSG ön uç** NSG toohello **ön uç** alt ağ, komutu aşağıdaki hello yeniden çalıştırın:

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

Merhaba çıktısında hello `networkSecurityGroup` anahtarı hello değeri için benzer bir şey yok:

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

## <a name="delete-an-nsg"></a>Bir NSG'yi Sil
Tooany kaynak ilişkili olmayan bir NSG'yi yalnızca silebilirsiniz. bir NSG'yi toodelete hello adımları izleyin.

1. Merhaba çalıştırmak tooan NSG, ilişkili toocheck hello kaynakları `azure network nsg show` gösterildiği gibi [görünüm Nsg'ler ilişkilendirmeleri](#View-NSGs-associations).
2. Merhaba NSG ilişkili tooany NIC ise, hello çalıştırın `azure network nic set` gösterildiği gibi [bir NSG'yi bir NIC gelen ilişkilendirmesini](#Dissociate-an-NSG-from-a-NIC) her NIC için 
3. Merhaba NSG ilişkili tooany alt ise, hello çalıştırın `azure network vnet subnet set` gösterildiği gibi [bir NSG bir alt ağdan ilişkilendirmesini](#Dissociate-an-NSG-from-a-subnet) her alt ağ için.
4. toodelete hello NSG, hello aşağıdaki komutu çalıştırın:

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a>Sonraki adımlar
* [Günlük kaydını etkinleştir](virtual-network-nsg-manage-log.md) Nsg'ler için.

