---
title: "Birden çok NIC ile azure'da bir Linux VM oluşturma | Microsoft Docs"
description: "Azure CLI 2.0 veya Resource Manager şablonları ile bağlı birden çok NIC içeren bir Linux VM oluşturmayı öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8a2931e462079c101c91497d459d7d3126234244
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a>Linux sanal makine Azure'da ile birden fazla ağ arabirimi kartları oluşturma
Bir sanal makine (VM) bağlı birden çok sanal ağ arabirimlerine (NIC'ler) sahip Azure oluşturabilirsiniz. Ön uç ve arka uç bağlantısı ya da izleme veya yedekleme çözümü için ayrılmış bir ağ için farklı alt ağlara sahip ortak bir senaryodur. Bu makalede, bağlı birden çok NIC içeren bir VM oluşturma ve ekleme veya NIC var olan bir sanal makineden kaldırın ayrıntıları. Ayrıntılı bilgi için kendi Bash betiklerini içinde birden çok NIC oluşturma dahil olmak üzere daha fazla okuyun hakkında [multi-NIC VM dağıtma](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md). Farklı [VM boyutları](sizes.md) NIC'ler değişen çok sayıda desteği, bu nedenle, VM buna göre boyutu.

Bu makalede Azure CLI 2.0 ile birden çok NIC içeren bir VM oluşturmak nasıl ayrıntılarını verir. Bu adımları [Azure CLI 1.0](multiple-nics-nodejs.md) ile de gerçekleştirebilirsiniz.


## <a name="create-supporting-resources"></a>Destekleyici kaynakları oluşturun
En son yükleme [Azure CLI 2.0](/cli/azure/install-az-cli2) ve bir Azure hesabı kullanarak oturum açma [az oturum açma](/cli/azure/#login).

Aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adları dahil *myResourceGroup*, *mystorageaccount*, ve *myVM*.

İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create). Aşağıdaki örnek, bir kaynak grubu oluşturur *myResourceGroup* içinde *eastus* konumu:

```azurecli
az group create --name myResourceGroup --location eastus
```

İle sanal ağ oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create). Aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* ve adlı alt ağ *mySubnetFrontEnd*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

Arka uç trafiği için bir alt ağ oluşturmak [az ağ sanal alt oluşturma](/cli/azure/network/vnet/subnet#create). Aşağıdaki örnek adlı bir alt ağı oluşturur *mySubnetBackEnd*:

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

Bir ağ güvenlik grubu oluşturma [az ağ nsg oluşturma](/cli/azure/network/nsg#create). Aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a>Oluşturma ve birden çok NIC yapılandırma
İki NIC ile oluşturma [az ağ NIC oluşturma](/cli/azure/network/nic#create). Aşağıdaki örnek adlı iki NIC oluşturur *myNic1* ve *myNic2*, her alt ağa bağlanan bir NIC ile ağ güvenlik grubu bağlı:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-the-nics"></a>Bir VM oluşturun ve NIC'ler ekleyin
İle oluşturulan NIC'ler belirtin VM oluşturduğunuzda `--nics`. VM boyutu seçerken dikkatli gerekir. Bir VM'ye ekleyebilirsiniz NIC toplam sayısına yönelik sınırlar vardır. Daha fazla bilgi edinin [Linux VM boyutları](sizes.md). 

[az vm create](/cli/azure/vm#create) ile bir VM oluşturun. Aşağıdaki örnek, adlandırılmış bir VM'nin oluşturur *myVM*:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-to-a-vm"></a>Bir VM için bir NIC eklemeniz
Önceki adımları bir VM ile birden çok NIC oluşturulur. Azure CLI 2.0 ile mevcut bir VM'yi NIC'ler ekleyebilirsiniz. 

Başka bir NIC ile oluşturma [az ağ NIC oluşturma](/cli/azure/network/nic#create). Aşağıdaki örnek, adlandırılmış bir NIC oluşturur *myNic3* önceki adımlarda oluşturduğunuz arka uç alt ağı ve ağ güvenlik grubuna bağlı:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

Mevcut bir VM'yi bir NIC eklemek için önce VM ile serbest bırakma [az vm serbest bırakma](/cli/azure/vm#deallocate). Aşağıdaki örnek adlı VM kaldırır *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

NIC ekleme [az vm NIC eklemeniz](/cli/azure/vm/nic#add). Aşağıdaki örnek, *myNic3* için *myVM*:

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

VM Başlat [az vm başlangıç](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a>Bir NIC bir sanal makineden kaldırın
Bir NIC var olan bir sanal makineden kaldırmak için ilk VM ile serbest bırakma [az vm serbest bırakma](/cli/azure/vm#deallocate). Aşağıdaki örnek adlı VM kaldırır *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

NIC ile Kaldır [az vm NIC kaldırmak](/cli/azure/vm/nic#remove). Aşağıdaki örnek kaldırır *myNic3* gelen *myVM*:

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

VM Başlat [az vm başlangıç](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a>Resource Manager şablonları kullanarak birden çok NIC oluşturun
Azure Resource Manager şablonları bildirim temelli JSON dosyaları ortamınızı tanımlamak için kullanın. Okuyabilirsiniz bir [genel bakış Azure Kaynak Yöneticisi'nin](../../azure-resource-manager/resource-group-overview.md). Resource Manager şablonları birden çok NIC oluşturma gibi dağıtımı sırasında bir kaynağın birden çok örneğini oluşturmak için bir yol sağlar. Kullandığınız *kopyalama* oluşturmak için örnek sayısını belirtmek için:

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

Daha fazla bilgi edinin [kullanarak birden çok örneği oluşturma *kopya*](../../resource-group-create-multiple.md). 

Aynı zamanda bir `copyIndex()` oluşturmanıza olanak tanıyan bir kaynak adı için bir sayı sonuna eklemek için `myNic1`, `myNic2`vb.. Dizin değeri ekleyerek bir örnek gösterilmektedir:

```json
"name": "[concat('myNic', copyIndex())]", 
```

Tam örnek okuyabilirsiniz [Resource Manager şablonları kullanarak birden çok NIC oluşturma](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Sonraki adımlar
Gözden geçirme [Linux VM boyutları](sizes.md) birden çok NIC ile VM oluşturmaya çalışırken. Her VM boyutu destekliyorsa NIC sayısı dikkat edin. 