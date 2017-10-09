---
title: "birden çok NIC ile azure'da bir Linux VM aaaCreate | Microsoft Docs"
description: "Toocreate birden çok NIC içeren bir Linux VM hello Azure CLI ya da Resource Manager şablonları kullanarak tooit nasıl bağlı öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a>İle birden çok NIC hello Azure CLI 1.0 kullanarak bir Linux sanal makine oluşturun
Birden çok sanal ağ arabirimlerine (NIC'ler) bağlı tooit sahip Azure'da bir sanal makine (VM) oluşturabilirsiniz. Yaygın bir senaryo toohave farklı alt ağlar için ön uç ve arka uç bağlantısı olan veya ayrılmış bir ağ tooa izleme veya yedekleme çözümü. Bu makalede Hızlı komutları toocreate birden çok NIC bağlı tooit'yle bir VM'yi sağlar. Ayrıntılı bilgi için kendi içinde birden çok NIC nasıl toocreate Bash de dahil olmak üzere komut dosyaları, daha fazla okuyun hakkında [multi-NIC VM dağıtma](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md). Farklı [VM boyutları](sizes.md) NIC'ler değişen çok sayıda desteği, bu nedenle, VM buna göre boyutu.

> [!WARNING]
> Birden çok NIC VM oluşturma - VM hello Azure CLI 1.0 ile varolan NIC'ler tooan ekleyemezsiniz zaman eklemelisiniz. Yapabilecekleriniz [VM hello Azure CLI 2.0 ile varolan NIC'ler tooan eklemek](multiple-nics.md). Ayrıca [hello özgün sanal diskler üzerinde dayalı bir VM oluşturma](copy-vm.md) ve hello VM dağıtmak gibi birden çok NIC oluşturun.


## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 1.0](#create-supporting-resources) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](multiple-nics.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için


## <a name="create-supporting-resources"></a>Destekleyici kaynakları oluşturun
Merhaba sahip olduğunuzdan emin olun [Azure CLI](../../cli-install-nodejs.md) oturum açmış ve Resource Manager modunu kullanma:

```azurecli
azure config mode arm
```

Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adları dahil *myResourceGroup*, *mystorageaccount*, ve *myVM*.

İlk olarak, bir kaynak grubu oluşturun. Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:

```azurecli
azure group create myResourceGroup --location eastus
```

Bir depolama hesabı toohold Vm'leriniz oluşturun. Merhaba aşağıdaki örnek adlı bir depolama hesabı oluşturur *mystorageaccount*:

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

Bir sanal ağ tooconnect Vm'leriniz için oluşturun. Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* bir adres öneki ile *192.168.0.0/16*:

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

İki sanal ağ alt - oluşturmak ön uç trafik, diğeri arka uç trafiği için. Merhaba aşağıdaki örnekte oluşturur adlı iki alt *mySubnetFrontEnd* ve *mySubnetBackEnd*:

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a>Oluşturma ve birden çok NIC yapılandırma
Hakkında daha fazla ayrıntı okuyabilirsiniz [hello Azure CLI kullanarak birden çok NIC dağıtma](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), tüm hello NIC'ler toocreate döngü hello işlemi komut dosyası gibi.

Merhaba aşağıdaki örnekte oluşturur adlı iki NIC *myNic1* ve *myNic2*, tooeach alt ağı bağlayan bir NIC ile:

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

Genellikle ayrıca oluşturduğunuz bir [ağ güvenlik grubu](../../virtual-network/virtual-networks-nsg.md) veya [yük dengeleyici](../../load-balancer/load-balancer-overview.md) toohelp yönetmek ve Vm'leriniz arasında trafiği dağıtın. Merhaba aşağıdaki örnekte oluşturur adlı bir ağ güvenlik grubu *myNetworkSecurityGroup*:

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

NIC toohello ağ güvenlik grubu kullanarak bağlama `azure network nic set`. Merhaba aşağıdaki örnek bağlar *myNic1* ve *myNic2* ile *myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a>Bir VM oluşturun ve hello NIC ekleme
Merhaba VM oluştururken, artık birden çok NIC belirtin. Yerine `--nic-name` tooprovide tek bir NIC, bunun yerine kullandığınız `--nic-names` ve NIC virgülle ayrılmış bir listesini sağlayın. Merhaba VM boyutu seçtiğinizde tootake dikkatli da gerekir. Merhaba tooa VM ekleyebilirsiniz NIC toplam sayısına yönelik sınırlar vardır. Daha fazla bilgi edinin [Linux VM boyutları](sizes.md). Merhaba aşağıdaki nasıl toospecify kullanarak destekleyen birden çok NIC ve ardından bir VM boyutu birden çok örnekte NIC'ler (*Standard_DS2_v2*):

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
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
Emin tooreview olun [Linux VM boyutları](sizes.md) toocreating birden çok NIC içeren bir VM çalışırken. Dikkat toohello en fazla sayıda her VM boyutu destekliyorsa NIC ücret ödersiniz. 

VM varolan Ek NIC tooan eklenemiyor, hello VM dağıttığınızda tüm hello NIC'ler oluşturmalısınız unutmayın. Merhaba outset tüm gerekli hello ağ bağlantısı olduğundan emin, dağıtımları toomake planlaması yaparken dikkatli olun.

