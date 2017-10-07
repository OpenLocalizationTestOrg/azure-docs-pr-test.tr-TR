---
title: "birden çok NIC ile azure'da bir Linux VM aaaCreate | Microsoft Docs"
description: "Toocreate birden çok NIC içeren bir Linux VM hello Azure CLI 2.0 veya Resource Manager şablonları kullanarak tooit nasıl bağlı öğrenin."
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
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a>Nasıl toocreate Linux sahip bir sanal makine azure'da birden çok ağ arabirim kartları
Birden çok sanal ağ arabirimlerine (NIC'ler) bağlı tooit sahip Azure'da bir sanal makine (VM) oluşturabilirsiniz. Yaygın bir senaryo toohave farklı alt ağlar için ön uç ve arka uç bağlantısı olan veya ayrılmış bir ağ tooa izleme veya yedekleme çözümü. Bu makalede tooit toocreate birden çok NIC içeren bir VM ekli nasıl ve ne ayrıntıları tooadd veya kaldırma NIC var olan bir VM'den. Ayrıntılı bilgi için kendi içinde birden çok NIC nasıl toocreate Bash de dahil olmak üzere komut dosyaları, daha fazla okuyun hakkında [multi-NIC VM dağıtma](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md). Farklı [VM boyutları](sizes.md) NIC'ler değişen çok sayıda desteği, bu nedenle, VM buna göre boyutu.

Bu makalede nasıl toocreate VM ile birden çok NIC içeren bir hello Azure CLI 2.0 ayrıntıları verilmektedir. Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](multiple-nics-nodejs.md).


## <a name="create-supporting-resources"></a>Destekleyici kaynakları oluşturun
Son yükleme hello [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login).

Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adları dahil *myResourceGroup*, *mystorageaccount*, ve *myVM*.

İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:

```azurecli
az group create --name myResourceGroup --location eastus
```

Merhaba sanal ağ ile oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create). Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* ve adlı alt ağ *mySubnetFrontEnd*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

Merhaba arka uç trafiği için bir alt ağ oluşturmak [az ağ sanal alt oluşturma](/cli/azure/network/vnet/subnet#create). Merhaba aşağıdaki örnek adlı bir alt ağı oluşturur *mySubnetBackEnd*:

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

Bir ağ güvenlik grubu oluşturma [az ağ nsg oluşturma](/cli/azure/network/nsg#create). Merhaba aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a>Oluşturma ve birden çok NIC yapılandırma
İki NIC ile oluşturma [az ağ NIC oluşturma](/cli/azure/network/nic#create). Merhaba aşağıdaki örnekte oluşturur adlı iki NIC *myNic1* ve *myNic2*, bağlı tooeach alt ağı bağlayan bir NIC ile Merhaba ağ güvenlik grubu:

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

## <a name="create-a-vm-and-attach-hello-nics"></a>Bir VM oluşturun ve hello NIC ekleme
Merhaba NIC'ler belirtin hello VM oluşturduğunuzda ile oluşturulan `--nics`. Merhaba VM boyutu seçtiğinizde tootake dikkatli da gerekir. Merhaba tooa VM ekleyebilirsiniz NIC toplam sayısına yönelik sınırlar vardır. Daha fazla bilgi edinin [Linux VM boyutları](sizes.md). 

[az vm create](/cli/azure/vm#create) ile bir VM oluşturun. Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM*:

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

## <a name="add-a-nic-tooa-vm"></a>NIC tooa VM ekleme
Merhaba önceki adımları bir VM ile birden çok NIC oluşturulur. Azure CLI 2.0 hello ile VM varolan NIC'ler tooan de ekleyebilirsiniz. 

Başka bir NIC ile oluşturma [az ağ NIC oluşturma](/cli/azure/network/nic#create). Merhaba aşağıdaki örnekte oluşturur adlı bir NIC *myNic3* bağlı toohello arka uç alt ağı ve hello önceki adımlarda oluşturduğunuz ağ güvenlik grubu:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

tooadd NIC tooan var olan VM ilk ayırması VM ile Merhaba [az vm serbest bırakma](/cli/azure/vm#deallocate). Merhaba aşağıdaki örnek kaldırır hello adlı VM *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Ekleme NIC ile Merhaba [az vm NIC eklemeniz](/cli/azure/vm/nic#add). Merhaba aşağıdaki örnek, *myNic3* çok*myVM*:

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

Başlangıç VM ile Merhaba [az vm başlangıç](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a>Bir NIC bir sanal makineden kaldırın
Mevcut bir VM'yi NIC'den tooremove ilk hello VM serbest bırakma ile [az vm serbest bırakma](/cli/azure/vm#deallocate). Merhaba aşağıdaki örnek kaldırır hello adlı VM *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Kaldırma NIC ile Merhaba [az vm NIC kaldırmak](/cli/azure/vm/nic#remove). Merhaba aşağıdaki örnek kaldırır *myNic3* gelen *myVM*:

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

Başlangıç VM ile Merhaba [az vm başlangıç](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a>Resource Manager şablonları kullanarak birden çok NIC oluşturun
Azure Resource Manager şablonları bildirim temelli JSON dosyaları toodefine ortamınız kullanın. Okuyabilirsiniz bir [genel bakış Azure Kaynak Yöneticisi'nin](../../azure-resource-manager/resource-group-overview.md). Resource Manager şablonları bir şekilde toocreate birden çok NIC oluşturma gibi dağıtım işlemi sırasında birden fazla örneğini bir kaynak sağlayın. Kullandığınız *kopya* toospecify hello örnekleri toocreate sayısı:

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

Daha fazla bilgi edinin [kullanarak birden çok örneği oluşturma *kopya*](../../resource-group-create-multiple.md). 

De kullanabilirsiniz bir `copyIndex()` toothen sona toocreate sağlayan bir numara tooa kaynak adı `myNic1`, `myNic2`, vb. hello aşağıdaki hello dizin değeri ekleyerek bir örnek gösterilmektedir:

```json
"name": "[concat('myNic', copyIndex())]", 
```

Tam örnek okuyabilirsiniz [Resource Manager şablonları kullanarak birden çok NIC oluşturma](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Sonraki adımlar
Gözden geçirme [Linux VM boyutları](sizes.md) toocreating birden çok NIC içeren bir VM çalışırken. Dikkat toohello en fazla sayıda her VM boyutu destekliyorsa NIC ücret ödersiniz. 
