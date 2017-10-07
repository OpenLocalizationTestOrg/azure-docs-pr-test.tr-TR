---
title: "aaaCreate hello Azure CLI 2.0 Linux ortamıyla | Microsoft Docs"
description: "Tüm hello Azure CLI 2.0 kullanarak plan hello depolama, bir Linux VM, bir sanal ağ ve alt ağ, bir yük dengeleyici, bir NIC, ortak bir IP ve bir ağ güvenlik grubu oluşturun."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 7287ea178e76001b84dade628ead04a59dc27f40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-hello-azure-cli"></a>Hello Azure CLI ile tam Linux sanal makine oluşturma
tooquickly Azure'da bir sanal makine (VM) oluşturmak, varsayılan değerleri toocreate kaynakları destekleyen gerekli kullanan tek bir Azure CLI komutu kullanabilirsiniz. Bir sanal ağ, genel IP adresi ve ağ güvenlik grubu kuralları gibi kaynakları otomatik olarak oluşturulur. Üretim ortamınızda, daha fazla denetim için kullanın, önceden bu kaynakları oluşturabilir ve ardından VM'ler toothem ekleyin. Bu makalede, nasıl toocreate VM ve her biri destekleyici kaynakları tek tek hello aracılığıyla size yol gösterir.

Merhaba son yüklediğinizden emin olun [Azure CLI 2.0](/cli/azure/install-az-cli2) ve oturum tooan Azure hesabı ile [az oturum açma](/cli/azure/#login).

Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adlarında *myResourceGroup*, *myVnet*, ve *myVM*.

## <a name="create-resource-group"></a>Kaynak grubu oluşturma
Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. Bir kaynak grubu, bir sanal makine ve destekleyici sanal ağ kaynakları önce oluşturulmalıdır. Merhaba kaynak grubuyla oluşturma [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:

```azurecli
az group create --name myResourceGroup --location eastus
```

Varsayılan olarak, Azure CLI komutlarının hello çıktılarını JSON (JavaScript nesne gösterimi) ' dir. toochange hello varsayılan çıkış tooa listesi veya tablo kullanın, örneğin, [az yapılandırmak--çıkış](/cli/azure/#configure). Ayrıca ekleyebileceğiniz `--output` tooany komutu bir kez için çıktı biçiminde değiştirin. Merhaba aşağıdaki örnek hello JSON çıktısını hello gösterir `az group create` komutu:

```json                       
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "location": "eastus",
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-a-virtual-network-and-subnet"></a>Bir sanal ağ ve alt ağ oluşturun
Sonraki Azure'da bir sanal ağ oluşturun ve bir alt ağda toowhich Vm'leriniz oluşturabilirsiniz. Kullanım [az ağ vnet oluşturma](/cli/azure/network/vnet#create) toocreate adlı bir sanal ağ *myVnet* hello ile *192.168.0.0/16* adres öneki. Ayrıca adlı bir alt ağ Ekle *mySubnet* hello adres öneki ile *192.168.1.0/24*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

Merhaba çıktısı olarak mantıksal hello sanal ağ içinde oluşturulmuş hello alt ağı gösterilmektedir:

```json
{
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "location": "eastus",
  "name": "myVnet",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "ed62fd03-e9de-430b-84df-8a3b87cacdbb",
  "subnets": [
    {
      "addressPrefix": "192.168.1.0/24",
      "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
      "ipConfigurations": null,
      "name": "mySubnet",
      "networkSecurityGroup": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  "tags": {},
  "type": "Microsoft.Network/virtualNetworks",
  "virtualNetworkPeerings": null
}
```


## <a name="create-a-public-ip-address"></a>Genel IP adresi oluşturma
Şimdi bir genel IP adresiyle oluşturalım [az ağ genel IP oluşturun](/cli/azure/network/public-ip#create). Bu genel IP adresi, tooconnect tooyour VM'ler hello Internet gelen sağlar. Merhaba varsayılan adres dinamik olduğundan, ayrıca adlandırılmış bir DNS girişi ile Merhaba oluşturuyoruz `--domain-name-label` seçeneği. Merhaba aşağıdaki örnekte oluşturur adlı ortak IP *myPublicIP* hello DNS adı ile *mypublicdns*. Merhaba DNS adının benzersiz olması gerektiğinden, kendi benzersiz DNS adını belirtin:

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

Çıktı:

```json
{
  "publicIp": {
    "dnsSettings": {
      "domainNameLabel": "mypublicdns",
      "fqdn": "mypublicdns.eastus.cloudapp.azure.com",
      "reverseFqdn": null
    },
    "etag": "W/\"2632aa72-3d2d-4529-b38e-b622b4202925\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "idleTimeoutInMinutes": 4,
    "ipAddress": null,
    "ipConfiguration": null,
    "location": "eastus",
    "name": "myPublicIP",
    "provisioningState": "Succeeded",
    "publicIpAddressVersion": "IPv4",
    "publicIpAllocationMethod": "Dynamic",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "4c65de38-71f5-4684-be10-75e605b3e41f",
    "tags": null,
    "type": "Microsoft.Network/publicIPAddresses"
  }
}
```


## <a name="create-a-network-security-group"></a>Bir ağ güvenlik grubu oluşturun
toocontrol hello akışı trafiği, sanal makineleri ve ağ güvenlik grubu oluşturun. Bir ağ güvenlik grubu uygulanan tooa NIC veya alt ağ olabilir. Merhaba aşağıdaki örnek kullanır [az ağ nsg oluşturma](/cli/azure/network/nsg#create) bir ağ güvenlik grubu adlı toocreate *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

İzin veren veya reddeden hello belirli bir trafik kuralları tanımlar. tooallow 22 (toosupport SSH) bağlantı noktasından gelen bağlantıları oluşturma hello ağ güvenlik grubu için bir gelen kuralı [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create). Merhaba aşağıdaki örnek adlı bir kural oluşturur *myNetworkSecurityGroupRuleSSH*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 22 \
    --access allow
```

tooallow gelen bağlantı noktası 80 (toosupport web trafiği), bağlantı başka bir ağ güvenlik grubu kural ekleyin. Merhaba aşağıdaki örnek adlı bir kural oluşturur *myNetworkSecurityGroupRuleHTTP*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleWeb \
    --protocol tcp \
    --priority 1001 \
    --destination-port-range 80 \
    --access allow
```

Merhaba ağ güvenlik grubu ve kurallarla inceleyin [az ağ nsg Göster](/cli/azure/network/nsg#show):

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

Çıktı:

```json
{
  "defaultSecurityRules": [
    {
      "access": "Allow",
      "description": "Allow inbound traffic from all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow inbound traffic from azure load balancer",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowAzureLoadBalancerInBou
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "AzureLoadBalancer",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all inbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooall VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooInternet",
      "destinationAddressPrefix": "Internet",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all outbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
  "location": "eastus",
  "name": "myNetworkSecurityGroup",
  "networkInterfaces": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "47a9964e-23a3-438a-a726-8d60ebbb1c3c",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "22",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleSSH",
      "name": "myNetworkSecurityGroupRuleSSH",
      "priority": 1000,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "80",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleWeb",
      "name": "myNetworkSecurityGroupRuleWeb",
      "priority": 1001,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "subnets": null,
  "tags": null,
  "type": "Microsoft.Network/networkSecurityGroups"
}
```

## <a name="create-a-virtual-nic"></a>Sanal bir NIC'ye oluşturma
Sanal ağ arabirimi kartlarıyla (NIC) program aracılığıyla kullanılabilir olduklarından kuralları tootheir kullanım uygulayabilirsiniz. Birden fazla olabilir. Merhaba aşağıdaki [az ağ NIC oluşturma](/cli/azure/network/nic#create) komutunu adlı bir NIC oluşturun *myNic* ve hello ağ güvenlik grubuyla ilişkilendirin. Merhaba genel IP adresi *myPublicIP* de hello sanal NIC ile ilişkilidir

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

Çıktı:

```json
{
  "NewNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": [],
      "internalDnsNameLabel": null,
      "internalDomainNameSuffix": "brqlt10lvoxedgkeuomc4pm5tb.bx.internal.cloudapp.net",
      "internalFqdn": null
    },
    "enableAcceleratedNetworking": false,
    "enableIpForwarding": false,
    "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic",
    "ipConfigurations": [
      {
        "applicationGatewayBackendAddressPools": null,
        "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic/ipConfigurations/ipconfig1",
        "loadBalancerBackendAddressPools": null,
        "loadBalancerInboundNatRules": null,
        "name": "ipconfig1",
        "primary": true,
        "privateIpAddress": "192.168.1.4",
        "privateIpAddressVersion": "IPv4",
        "privateIpAllocationMethod": "Dynamic",
        "provisioningState": "Succeeded",
        "publicIpAddress": {
          "dnsSettings": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
          "idleTimeoutInMinutes": null,
          "ipAddress": null,
          "ipConfiguration": null,
          "location": null,
          "name": null,
          "provisioningState": null,
          "publicIpAddressVersion": null,
          "publicIpAllocationMethod": null,
          "resourceGroup": "myResourceGroup",
          "resourceGuid": null,
          "tags": null,
          "type": null
        },
        "resourceGroup": "myResourceGroup",
        "subnet": {
          "addressPrefix": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
          "ipConfigurations": null,
          "name": null,
          "networkSecurityGroup": null,
          "provisioningState": null,
          "resourceGroup": "myResourceGroup",
          "resourceNavigationLinks": null,
          "routeTable": null
        }
      }
    ],
    "location": "eastus",
    "macAddress": null,
    "name": "myNic",
    "networkSecurityGroup": {
      "defaultSecurityRules": null,
      "etag": null,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
      "location": null,
      "name": null,
      "networkInterfaces": null,
      "provisioningState": null,
      "resourceGroup": "myResourceGroup",
      "resourceGuid": null,
      "securityRules": null,
      "subnets": null,
      "tags": null,
      "type": null
    },
    "primary": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "b3dbaa0e-2cf2-43be-a814-5cc49fea3304",
    "tags": null,
    "type": "Microsoft.Network/networkInterfaces",
    "virtualMachine": null
  }
}
```


## <a name="create-an-availability-set"></a>Kullanılabilirlik kümesi oluşturma
Kullanılabilirlik Yardım yayılan hata etki alanları ve güncelleştirme etki alanları arasında Vm'leriniz ayarlar. Yalnızca bir VM şimdi oluşturduğunuz olsa bile, en iyi yöntem toouse kullanılabilirlik kümeleri toomake olan, daha kolay tooexpand hello gelecekteki içinde. 

Sanal makineler, ortak bir güç kaynağı ve ağ anahtarı paylaşmak gruplandırması hata etki alanlarını tanımlayın. Varsayılan olarak, kullanılabilirlik kümesi içinde yapılandırılmış hello sanal makineleri toothree hata etki alanları arasında ayrılır. Bu hata etki alanlarını birinde bir donanım sorunundan uygulamanızı çalıştıran her VM etkilemez.

Güncelleme etki alanına belirtmek sanal makineler ve hello yeniden temel alınan fiziksel donanım grupları aynı anda. Planlı bakım sırasında hangi güncelleştirme etki alanlarını yeniden hello sıra sıralı olmayabilir, ancak aynı anda yalnızca tek bir güncelleştirme etki alanı yeniden başlatıldı.

Azure otomatik olarak VM'ler hello arıza ve güncelleştirme etki alanları arasında bunları bir kullanılabilirlik kümesine yerleştirdiğinizde dağıtır. Daha fazla bilgi için bkz: [VM'ler hello kullanılabilirliğini yönetme](manage-availability.md).

Kullanılabilirlik için VM ile kümesi oluştur [az vm kullanılabilirlik kümesi oluşturma](/cli/azure/vm/availability-set#create). Merhaba aşağıdaki örnekte oluşturur kullanılabilirlik adlandırılmış kümesi *myAvailabilitySet*:

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

Çıktı notları hata etki alanlarını hello ve güncelleme etki alanları:

```json
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet",
  "location": "eastus",
  "managed": null,
  "name": "myAvailabilitySet",
  "platformFaultDomainCount": 2,
  "platformUpdateDomainCount": 5,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": null,
    "managed": true,
    "tier": null
  },
  "statuses": null,
  "tags": {},
  "type": "Microsoft.Compute/availabilitySets",
  "virtualMachines": []
}
```


## <a name="create-hello-linux-vms"></a>Merhaba Linux VM'ler oluşturma
Internet'ten erişilebilen VM'ler hello ağ kaynakları toosupport oluşturduğunuzu düşünün. Şimdi bir VM oluşturun ve bir SSH anahtarı ile güvenliğini sağlayın. Bu durumda, bir Ubuntu VM tabanlı hello üzerinde toocreate yapacağız en son LTS. Ek görüntülerle bulabilirsiniz [az vm görüntü listesi](/cli/azure/vm/image#list)açıklandığı gibi [Azure VM görüntülerini bulma](cli-ps-findimage.md).

Biz de kimlik doğrulaması için bir SSH anahtarı toouse belirtin. SSH ortak anahtar çifti yoksa, şunları yapabilirsiniz [bunları oluşturmanız](mac-create-ssh-keys.md) veya hello `--generate-ssh-keys` parametresi toocreate bunları sizin için. Varolan anahtarların, zaten bir anahtar çifti, bu parametre kullanıyorsa `~/.ssh`.

Bizim tüm kaynaklara ve bilgi ile birlikte hello getirerek Hello VM oluşturma [az vm oluşturma](/cli/azure/vm#create) komutu. Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM*:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --availability-set myAvailabilitySet \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

Merhaba hello genel IP adresi oluştururken sağladığınız DNS girişi ile SSH tooyour VM. Bu `fqdn` , VM oluşturma gibi hello çıktısında gösterilir:

```json
{
  "fqdns": "mypublicdns.eastus.cloudapp.azure.com",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-13-71-C8",
  "powerState": "VM running",
  "privateIpAddress": "192.168.1.5",
  "publicIpAddress": "13.90.94.252",
  "resourceGroup": "myResourceGroup"
}
```

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

Çıktı:

```bash
hello authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

toorun a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

NGINX yükleyin ve hello trafik akışı toohello VM bakın. NGINX gibi yükleyin:

```bash
sudo apt-get install -y nginx
```

toosee hello varsayılan NGINX eylem, sitede web tarayıcınızı açın ve FQDN değerinizi girin:

![Varsayılan NGINX sitesinde VM](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a>Bir şablon olarak dışarı aktarma
Şimdi ne toocreate hello bir ek geliştirme ortamı istediğiniz aynı parametreleri veya eşleşecek bir üretim ortamında? Resource Manager, ortamınız için tüm hello parametreleri tanımlayan JSON şablonlarını kullanır. Bu JSON şablonunu başvurarak tüm ortamlar oluşturun. Yapabilecekleriniz [JSON şablonları el ile oluşturabilir](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya var olan bir ortam toocreate hello JSON şablonunu sizin için dışarı aktarma. Kullanım [az grup verme](/cli/azure/group#export) , kaynak grubu gibi tooexport:

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

Bu komut hello oluşturur `myResourceGroup.json` geçerli çalışma dizini dosyasında. Bu şablonu kullanarak bir ortam oluşturmak için tüm hello kaynak adları sorulur. Merhaba ekleyerek bu adları şablon dosyanızın doldurabilirsiniz `--include-parameter-default-value` parametresi toohello `az group export` komutu. JSON şablonunu toospecify hello kaynak adları, düzenlemek veya [parameters.json dosyası oluşturma](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hello kaynak adları belirtir.

toocreate kullanım şablonunuzu bir ortamdan [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create) gibi:

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

Tooread isteyebilirsiniz [nasıl hakkında daha fazla şablonlardan toodeploy](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Nasıl tooincrementally güncelleştirme ortamlarda, hello parametreleri dosyasını kullanın ve şablonları bir tek bir depolama konumundan erişim hakkında bilgi edinin.

## <a name="next-steps"></a>Sonraki adımlar
Artık birden çok ağ bileşenleri ve VM'ler ile çalışmaya hazır toobegin demektir. Burada sunulan hello çekirdek bileşenlerini kullanarak, bu örnek ortamı toobuild uygulamanızı kullanabilirsiniz.
