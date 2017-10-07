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
# <a name="create-a-complete-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="97364-103">Hello Azure CLI ile tam Linux sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="97364-103">Create a complete Linux virtual machine with hello Azure CLI</span></span>
<span data-ttu-id="97364-104">tooquickly Azure'da bir sanal makine (VM) oluşturmak, varsayılan değerleri toocreate kaynakları destekleyen gerekli kullanan tek bir Azure CLI komutu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97364-104">tooquickly create a virtual machine (VM) in Azure, you can use a single Azure CLI command that uses default values toocreate any required supporting resources.</span></span> <span data-ttu-id="97364-105">Bir sanal ağ, genel IP adresi ve ağ güvenlik grubu kuralları gibi kaynakları otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="97364-105">Resources such as a virtual network, public IP address, and network security group rules are automatically created.</span></span> <span data-ttu-id="97364-106">Üretim ortamınızda, daha fazla denetim için kullanın, önceden bu kaynakları oluşturabilir ve ardından VM'ler toothem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="97364-106">For more control of your environment in production use, you may create these resources ahead of time and then add your VMs toothem.</span></span> <span data-ttu-id="97364-107">Bu makalede, nasıl toocreate VM ve her biri destekleyici kaynakları tek tek hello aracılığıyla size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="97364-107">This article guides you through how toocreate a VM and each of hello supporting resources one by one.</span></span>

<span data-ttu-id="97364-108">Merhaba son yüklediğinizden emin olun [Azure CLI 2.0](/cli/azure/install-az-cli2) ve oturum tooan Azure hesabı ile [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="97364-108">Make sure that you have installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged tooan Azure account in with [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="97364-109">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="97364-109">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="97364-110">Örnek parametre adlarında *myResourceGroup*, *myVnet*, ve *myVM*.</span><span class="sxs-lookup"><span data-stu-id="97364-110">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="97364-111">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="97364-111">Create resource group</span></span>
<span data-ttu-id="97364-112">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="97364-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="97364-113">Bir kaynak grubu, bir sanal makine ve destekleyici sanal ağ kaynakları önce oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="97364-113">A resource group must be created before a virtual machine and supporting virtual network resources.</span></span> <span data-ttu-id="97364-114">Merhaba kaynak grubuyla oluşturma [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="97364-114">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="97364-115">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="97364-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="97364-116">Varsayılan olarak, Azure CLI komutlarının hello çıktılarını JSON (JavaScript nesne gösterimi) ' dir.</span><span class="sxs-lookup"><span data-stu-id="97364-116">By default, hello output of Azure CLI commands is in JSON (JavaScript Object Notation).</span></span> <span data-ttu-id="97364-117">toochange hello varsayılan çıkış tooa listesi veya tablo kullanın, örneğin, [az yapılandırmak--çıkış](/cli/azure/#configure).</span><span class="sxs-lookup"><span data-stu-id="97364-117">toochange hello default output tooa list or table, for example, use [az configure --output](/cli/azure/#configure).</span></span> <span data-ttu-id="97364-118">Ayrıca ekleyebileceğiniz `--output` tooany komutu bir kez için çıktı biçiminde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="97364-118">You can also add `--output` tooany command for a one time change in output format.</span></span> <span data-ttu-id="97364-119">Merhaba aşağıdaki örnek hello JSON çıktısını hello gösterir `az group create` komutu:</span><span class="sxs-lookup"><span data-stu-id="97364-119">hello following example shows hello JSON output from hello `az group create` command:</span></span>

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

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="97364-120">Bir sanal ağ ve alt ağ oluşturun</span><span class="sxs-lookup"><span data-stu-id="97364-120">Create a virtual network and subnet</span></span>
<span data-ttu-id="97364-121">Sonraki Azure'da bir sanal ağ oluşturun ve bir alt ağda toowhich Vm'leriniz oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97364-121">Next you create a virtual network in Azure and a subnet in toowhich you can create your VMs.</span></span> <span data-ttu-id="97364-122">Kullanım [az ağ vnet oluşturma](/cli/azure/network/vnet#create) toocreate adlı bir sanal ağ *myVnet* hello ile *192.168.0.0/16* adres öneki.</span><span class="sxs-lookup"><span data-stu-id="97364-122">Use [az network vnet create](/cli/azure/network/vnet#create) toocreate a virtual network named *myVnet* with hello *192.168.0.0/16* address prefix.</span></span> <span data-ttu-id="97364-123">Ayrıca adlı bir alt ağ Ekle *mySubnet* hello adres öneki ile *192.168.1.0/24*:</span><span class="sxs-lookup"><span data-stu-id="97364-123">You also add a subnet named *mySubnet* with hello address prefix of *192.168.1.0/24*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="97364-124">Merhaba çıktısı olarak mantıksal hello sanal ağ içinde oluşturulmuş hello alt ağı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="97364-124">hello output shows hello subnet as logically created inside hello virtual network:</span></span>

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


## <a name="create-a-public-ip-address"></a><span data-ttu-id="97364-125">Genel IP adresi oluşturma</span><span class="sxs-lookup"><span data-stu-id="97364-125">Create a public IP address</span></span>
<span data-ttu-id="97364-126">Şimdi bir genel IP adresiyle oluşturalım [az ağ genel IP oluşturun](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="97364-126">Now let's create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="97364-127">Bu genel IP adresi, tooconnect tooyour VM'ler hello Internet gelen sağlar.</span><span class="sxs-lookup"><span data-stu-id="97364-127">This public IP address enables you tooconnect tooyour VMs from hello Internet.</span></span> <span data-ttu-id="97364-128">Merhaba varsayılan adres dinamik olduğundan, ayrıca adlandırılmış bir DNS girişi ile Merhaba oluşturuyoruz `--domain-name-label` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="97364-128">Because hello default address is dynamic, we also create a named DNS entry with hello `--domain-name-label` option.</span></span> <span data-ttu-id="97364-129">Merhaba aşağıdaki örnekte oluşturur adlı ortak IP *myPublicIP* hello DNS adı ile *mypublicdns*.</span><span class="sxs-lookup"><span data-stu-id="97364-129">hello following example creates a public IP named *myPublicIP* with hello DNS name of *mypublicdns*.</span></span> <span data-ttu-id="97364-130">Merhaba DNS adının benzersiz olması gerektiğinden, kendi benzersiz DNS adını belirtin:</span><span class="sxs-lookup"><span data-stu-id="97364-130">Because hello DNS name must be unique, provide your own unique DNS name:</span></span>

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

<span data-ttu-id="97364-131">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="97364-131">Output:</span></span>

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


## <a name="create-a-network-security-group"></a><span data-ttu-id="97364-132">Bir ağ güvenlik grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="97364-132">Create a network security group</span></span>
<span data-ttu-id="97364-133">toocontrol hello akışı trafiği, sanal makineleri ve ağ güvenlik grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="97364-133">toocontrol hello flow of traffic in and out of your VMs, create a network security group.</span></span> <span data-ttu-id="97364-134">Bir ağ güvenlik grubu uygulanan tooa NIC veya alt ağ olabilir.</span><span class="sxs-lookup"><span data-stu-id="97364-134">A network security group can be applied tooa NIC or subnet.</span></span> <span data-ttu-id="97364-135">Merhaba aşağıdaki örnek kullanır [az ağ nsg oluşturma](/cli/azure/network/nsg#create) bir ağ güvenlik grubu adlı toocreate *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="97364-135">hello following example uses [az network nsg create](/cli/azure/network/nsg#create) toocreate a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="97364-136">İzin veren veya reddeden hello belirli bir trafik kuralları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="97364-136">You define rules that allow or deny hello specific traffic.</span></span> <span data-ttu-id="97364-137">tooallow 22 (toosupport SSH) bağlantı noktasından gelen bağlantıları oluşturma hello ağ güvenlik grubu için bir gelen kuralı [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="97364-137">tooallow inbound connections on port 22 (toosupport SSH), create an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="97364-138">Merhaba aşağıdaki örnek adlı bir kural oluşturur *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="97364-138">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

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

<span data-ttu-id="97364-139">tooallow gelen bağlantı noktası 80 (toosupport web trafiği), bağlantı başka bir ağ güvenlik grubu kural ekleyin.</span><span class="sxs-lookup"><span data-stu-id="97364-139">tooallow inbound connections on port 80 (toosupport web traffic), add another network security group rule.</span></span> <span data-ttu-id="97364-140">Merhaba aşağıdaki örnek adlı bir kural oluşturur *myNetworkSecurityGroupRuleHTTP*:</span><span class="sxs-lookup"><span data-stu-id="97364-140">hello following example creates a rule named *myNetworkSecurityGroupRuleHTTP*:</span></span>

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

<span data-ttu-id="97364-141">Merhaba ağ güvenlik grubu ve kurallarla inceleyin [az ağ nsg Göster](/cli/azure/network/nsg#show):</span><span class="sxs-lookup"><span data-stu-id="97364-141">Examine hello network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span></span>

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="97364-142">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="97364-142">Output:</span></span>

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

## <a name="create-a-virtual-nic"></a><span data-ttu-id="97364-143">Sanal bir NIC'ye oluşturma</span><span class="sxs-lookup"><span data-stu-id="97364-143">Create a virtual NIC</span></span>
<span data-ttu-id="97364-144">Sanal ağ arabirimi kartlarıyla (NIC) program aracılığıyla kullanılabilir olduklarından kuralları tootheir kullanım uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97364-144">Virtual network interface cards (NICs) are programmatically available because you can apply rules tootheir use.</span></span> <span data-ttu-id="97364-145">Birden fazla olabilir.</span><span class="sxs-lookup"><span data-stu-id="97364-145">You can also have more than one.</span></span> <span data-ttu-id="97364-146">Merhaba aşağıdaki [az ağ NIC oluşturma](/cli/azure/network/nic#create) komutunu adlı bir NIC oluşturun *myNic* ve hello ağ güvenlik grubuyla ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="97364-146">In hello following [az network nic create](/cli/azure/network/nic#create) command, you create a NIC named *myNic* and associate it with hello network security group.</span></span> <span data-ttu-id="97364-147">Merhaba genel IP adresi *myPublicIP* de hello sanal NIC ile ilişkilidir</span><span class="sxs-lookup"><span data-stu-id="97364-147">hello public IP address *myPublicIP* is also associated with hello virtual NIC.</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="97364-148">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="97364-148">Output:</span></span>

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


## <a name="create-an-availability-set"></a><span data-ttu-id="97364-149">Kullanılabilirlik kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="97364-149">Create an availability set</span></span>
<span data-ttu-id="97364-150">Kullanılabilirlik Yardım yayılan hata etki alanları ve güncelleştirme etki alanları arasında Vm'leriniz ayarlar.</span><span class="sxs-lookup"><span data-stu-id="97364-150">Availability sets help spread your VMs across fault domains and update domains.</span></span> <span data-ttu-id="97364-151">Yalnızca bir VM şimdi oluşturduğunuz olsa bile, en iyi yöntem toouse kullanılabilirlik kümeleri toomake olan, daha kolay tooexpand hello gelecekteki içinde.</span><span class="sxs-lookup"><span data-stu-id="97364-151">Even though you only create one VM right now, it's best practice toouse availability sets toomake it easier tooexpand in hello future.</span></span> 

<span data-ttu-id="97364-152">Sanal makineler, ortak bir güç kaynağı ve ağ anahtarı paylaşmak gruplandırması hata etki alanlarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="97364-152">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="97364-153">Varsayılan olarak, kullanılabilirlik kümesi içinde yapılandırılmış hello sanal makineleri toothree hata etki alanları arasında ayrılır.</span><span class="sxs-lookup"><span data-stu-id="97364-153">By default, hello virtual machines that are configured within your availability set are separated across up toothree fault domains.</span></span> <span data-ttu-id="97364-154">Bu hata etki alanlarını birinde bir donanım sorunundan uygulamanızı çalıştıran her VM etkilemez.</span><span class="sxs-lookup"><span data-stu-id="97364-154">A hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span>

<span data-ttu-id="97364-155">Güncelleme etki alanına belirtmek sanal makineler ve hello yeniden temel alınan fiziksel donanım grupları aynı anda.</span><span class="sxs-lookup"><span data-stu-id="97364-155">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="97364-156">Planlı bakım sırasında hangi güncelleştirme etki alanlarını yeniden hello sıra sıralı olmayabilir, ancak aynı anda yalnızca tek bir güncelleştirme etki alanı yeniden başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="97364-156">During planned maintenance, hello order in which update domains are rebooted might not be sequential, but only one update domain is rebooted at a time.</span></span>

<span data-ttu-id="97364-157">Azure otomatik olarak VM'ler hello arıza ve güncelleştirme etki alanları arasında bunları bir kullanılabilirlik kümesine yerleştirdiğinizde dağıtır.</span><span class="sxs-lookup"><span data-stu-id="97364-157">Azure automatically distributes VMs across hello fault and update domains when placing them in an availability set.</span></span> <span data-ttu-id="97364-158">Daha fazla bilgi için bkz: [VM'ler hello kullanılabilirliğini yönetme](manage-availability.md).</span><span class="sxs-lookup"><span data-stu-id="97364-158">For more information, see [managing hello availability of VMs](manage-availability.md).</span></span>

<span data-ttu-id="97364-159">Kullanılabilirlik için VM ile kümesi oluştur [az vm kullanılabilirlik kümesi oluşturma](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="97364-159">Create an availability set for your VM with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="97364-160">Merhaba aşağıdaki örnekte oluşturur kullanılabilirlik adlandırılmış kümesi *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="97364-160">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

<span data-ttu-id="97364-161">Çıktı notları hata etki alanlarını hello ve güncelleme etki alanları:</span><span class="sxs-lookup"><span data-stu-id="97364-161">hello output notes fault domains and update domains:</span></span>

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


## <a name="create-hello-linux-vms"></a><span data-ttu-id="97364-162">Merhaba Linux VM'ler oluşturma</span><span class="sxs-lookup"><span data-stu-id="97364-162">Create hello Linux VMs</span></span>
<span data-ttu-id="97364-163">Internet'ten erişilebilen VM'ler hello ağ kaynakları toosupport oluşturduğunuzu düşünün.</span><span class="sxs-lookup"><span data-stu-id="97364-163">You've created hello network resources toosupport Internet-accessible VMs.</span></span> <span data-ttu-id="97364-164">Şimdi bir VM oluşturun ve bir SSH anahtarı ile güvenliğini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="97364-164">Now create a VM and secure it with an SSH key.</span></span> <span data-ttu-id="97364-165">Bu durumda, bir Ubuntu VM tabanlı hello üzerinde toocreate yapacağız en son LTS.</span><span class="sxs-lookup"><span data-stu-id="97364-165">In this case, we're going toocreate an Ubuntu VM based on hello most recent LTS.</span></span> <span data-ttu-id="97364-166">Ek görüntülerle bulabilirsiniz [az vm görüntü listesi](/cli/azure/vm/image#list)açıklandığı gibi [Azure VM görüntülerini bulma](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="97364-166">You can find additional images with [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md).</span></span>

<span data-ttu-id="97364-167">Biz de kimlik doğrulaması için bir SSH anahtarı toouse belirtin.</span><span class="sxs-lookup"><span data-stu-id="97364-167">We also specify an SSH key toouse for authentication.</span></span> <span data-ttu-id="97364-168">SSH ortak anahtar çifti yoksa, şunları yapabilirsiniz [bunları oluşturmanız](mac-create-ssh-keys.md) veya hello `--generate-ssh-keys` parametresi toocreate bunları sizin için.</span><span class="sxs-lookup"><span data-stu-id="97364-168">If you do not have an SSH public key pair, you can [create them](mac-create-ssh-keys.md) or use hello `--generate-ssh-keys` parameter toocreate them for you.</span></span> <span data-ttu-id="97364-169">Varolan anahtarların, zaten bir anahtar çifti, bu parametre kullanıyorsa `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="97364-169">If you already a key pair, this parameter uses existing keys in `~/.ssh`.</span></span>

<span data-ttu-id="97364-170">Bizim tüm kaynaklara ve bilgi ile birlikte hello getirerek Hello VM oluşturma [az vm oluşturma](/cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="97364-170">Create hello VM by bringing all our resources and information together with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="97364-171">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM*:</span><span class="sxs-lookup"><span data-stu-id="97364-171">hello following example creates a VM named *myVM*:</span></span>

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

<span data-ttu-id="97364-172">Merhaba hello genel IP adresi oluştururken sağladığınız DNS girişi ile SSH tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="97364-172">SSH tooyour VM with hello DNS entry you provided when you created hello public IP address.</span></span> <span data-ttu-id="97364-173">Bu `fqdn` , VM oluşturma gibi hello çıktısında gösterilir:</span><span class="sxs-lookup"><span data-stu-id="97364-173">This `fqdn` is shown in hello output as you create your VM:</span></span>

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

<span data-ttu-id="97364-174">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="97364-174">Output:</span></span>

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

<span data-ttu-id="97364-175">NGINX yükleyin ve hello trafik akışı toohello VM bakın.</span><span class="sxs-lookup"><span data-stu-id="97364-175">You can install NGINX and see hello traffic flow toohello VM.</span></span> <span data-ttu-id="97364-176">NGINX gibi yükleyin:</span><span class="sxs-lookup"><span data-stu-id="97364-176">Install NGINX as follows:</span></span>

```bash
sudo apt-get install -y nginx
```

<span data-ttu-id="97364-177">toosee hello varsayılan NGINX eylem, sitede web tarayıcınızı açın ve FQDN değerinizi girin:</span><span class="sxs-lookup"><span data-stu-id="97364-177">toosee hello default NGINX site in action, open your web browser and enter your FQDN:</span></span>

![Varsayılan NGINX sitesinde VM](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a><span data-ttu-id="97364-179">Bir şablon olarak dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="97364-179">Export as a template</span></span>
<span data-ttu-id="97364-180">Şimdi ne toocreate hello bir ek geliştirme ortamı istediğiniz aynı parametreleri veya eşleşecek bir üretim ortamında?</span><span class="sxs-lookup"><span data-stu-id="97364-180">What if you now want toocreate an additional development environment with hello same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="97364-181">Resource Manager, ortamınız için tüm hello parametreleri tanımlayan JSON şablonlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="97364-181">Resource Manager uses JSON templates that define all hello parameters for your environment.</span></span> <span data-ttu-id="97364-182">Bu JSON şablonunu başvurarak tüm ortamlar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="97364-182">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="97364-183">Yapabilecekleriniz [JSON şablonları el ile oluşturabilir](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya var olan bir ortam toocreate hello JSON şablonunu sizin için dışarı aktarma.</span><span class="sxs-lookup"><span data-stu-id="97364-183">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment toocreate hello JSON template for you.</span></span> <span data-ttu-id="97364-184">Kullanım [az grup verme](/cli/azure/group#export) , kaynak grubu gibi tooexport:</span><span class="sxs-lookup"><span data-stu-id="97364-184">Use [az group export](/cli/azure/group#export) tooexport your resource group as follows:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

<span data-ttu-id="97364-185">Bu komut hello oluşturur `myResourceGroup.json` geçerli çalışma dizini dosyasında.</span><span class="sxs-lookup"><span data-stu-id="97364-185">This command creates hello `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="97364-186">Bu şablonu kullanarak bir ortam oluşturmak için tüm hello kaynak adları sorulur.</span><span class="sxs-lookup"><span data-stu-id="97364-186">When you create an environment from this template, you are prompted for all hello resource names.</span></span> <span data-ttu-id="97364-187">Merhaba ekleyerek bu adları şablon dosyanızın doldurabilirsiniz `--include-parameter-default-value` parametresi toohello `az group export` komutu.</span><span class="sxs-lookup"><span data-stu-id="97364-187">You can populate these names in your template file by adding hello `--include-parameter-default-value` parameter toohello `az group export` command.</span></span> <span data-ttu-id="97364-188">JSON şablonunu toospecify hello kaynak adları, düzenlemek veya [parameters.json dosyası oluşturma](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hello kaynak adları belirtir.</span><span class="sxs-lookup"><span data-stu-id="97364-188">Edit your JSON template toospecify hello resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies hello resource names.</span></span>

<span data-ttu-id="97364-189">toocreate kullanım şablonunuzu bir ortamdan [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create) gibi:</span><span class="sxs-lookup"><span data-stu-id="97364-189">toocreate an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span></span>

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

<span data-ttu-id="97364-190">Tooread isteyebilirsiniz [nasıl hakkında daha fazla şablonlardan toodeploy](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="97364-190">You might want tooread [more about how toodeploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="97364-191">Nasıl tooincrementally güncelleştirme ortamlarda, hello parametreleri dosyasını kullanın ve şablonları bir tek bir depolama konumundan erişim hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="97364-191">Learn about how tooincrementally update environments, use hello parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97364-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="97364-192">Next steps</span></span>
<span data-ttu-id="97364-193">Artık birden çok ağ bileşenleri ve VM'ler ile çalışmaya hazır toobegin demektir.</span><span class="sxs-lookup"><span data-stu-id="97364-193">Now you're ready toobegin working with multiple networking components and VMs.</span></span> <span data-ttu-id="97364-194">Burada sunulan hello çekirdek bileşenlerini kullanarak, bu örnek ortamı toobuild uygulamanızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97364-194">You can use this sample environment toobuild out your application by using hello core components introduced here.</span></span>
