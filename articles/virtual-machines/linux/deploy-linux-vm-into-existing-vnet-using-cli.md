---
title: "mevcut ağ Azure CLI 2.0 ile içine aaaDeploy Linux VM'ler | Microsoft Docs"
description: "Nasıl toodeploy kullanarak varolan bir sanal ağ içinde Linux sanal makine hello Azure CLI 2.0 öğrenin"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a>Nasıl toodeploy mevcut Azure sanal ağda hello Azure CLI ile Linux sanal makine

Bu makale size nasıl toouse hello Azure CLI 2.0 toodeploy bir sanal makine (VM) var olan bir sanal ağı gösterir. Hello gereksinimleri şunlardır:

- [Bir Azure hesabı](https://azure.microsoft.com/pricing/free-trial/)
- [SSH ortak ve özel anahtar dosyaları](mac-create-ssh-keys.md)

Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).


## <a name="quick-commands"></a>Hızlı Komutlar
Tooquickly gerekiyorsa hello görevi, gerekli hello komutları bölümden hello ayrıntıları. Her adım hello belgenin hello kalan bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](#detailed-walkthrough).

toocreate bu özel ortam hello son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).

Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adlarında *myResourceGroup*, *myVnet*, ve *myVM*.

**Ön gereksinimlerini:** Azure kaynak grubu, sanal ağ ve alt ağ, ağ güvenlik grubu SSH ile gelen ve bir sanal ağ arabirim kartı.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Merhaba VM hello sanal ağ altyapısıyla dağıtma

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a>Ayrıntılı kılavuz

Sanal ağlar ve ağ güvenlik grupları gibi Azure varlıklar statik olmalıdır ve nadiren dağıtılan kaynakları uzun ömürlü. Bir sanal ağ dağıtıldıktan sonra herhangi bir olumsuz etkiler toohello altyapı olmadan yeni dağıtımlar tarafından yeniden. Geleneksel donanım ağ anahtarı olarak bir sanal ağ yapılandırmanızda -, yepyeni bir donanım her dağıtımı ile geçiş tooconfigure ihtiyaç duymaz. Doğru şekilde yapılandırılmış bir sanal ağ ile toodeploy devam edebilmeniz için yeni VM'ler bu sanal ağla defalarca az içine, varsa, değişiklikleri gerekli hello sanal ağ hello ömrü boyunca.

toocreate bu özel ortam hello son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).

Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adlarında *myResourceGroup*, *myVnet*, ve *myVM*.

## <a name="create-hello-resource-group"></a>Merhaba kaynak grubu oluştur

İlk olarak, bir Azure kaynak grubu tooorganize bu kılavuzda oluşturduğunuz her şeyi oluşturun. Kaynak grupları hakkında daha fazla bilgi için bkz. [Azure Resource Manager’a genel bakış](../../azure-resource-manager/resource-group-overview.md). Merhaba kaynak grubuyla oluşturma [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a>Merhaba sanal ağ oluşturma

Bir Azure sanal ağı toolaunch hello içine VM'ler yapı sağlar. Sanal ağlar hakkında daha fazla bilgi için bkz: [hello Azure CLI kullanarak bir sanal ağ oluşturma](../../virtual-network/virtual-networks-create-vnet-arm-cli.md). Merhaba sanal ağ ile oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create). Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* ve adlı alt ağ *mySubnet*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a>Merhaba ağ güvenlik grubu oluşturun

Azure ağ güvenlik grupları hello ağ katmanı eşdeğer tooa güvenlik duvarında değildir. Ağ güvenlik grupları hakkında daha fazla bilgi için bkz: [nasıl hello Azure CLI toocreate ağ güvenlik gruplarını](../../virtual-network/virtual-networks-create-nsg-arm-cli.md). Merhaba ağ güvenlik grubu oluşturma [az ağ nsg oluşturma](/cli/azure/network/nsg#create). Merhaba aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Gelen bir SSH izin ver Kuralı Ekle

Merhaba VM gelen bağlantı noktası 22 trafiği toobe veren bir kural hello ağ tooport 22 hello VM üzerinde geçirilen şekilde Internet gerekli hello erişimden gerekir. Merhaba ağ güvenlik grubu için bir gelen kuralı Ekle [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create). Merhaba aşağıdaki örnek adlı bir kural oluşturur *myNetworkSecurityGroupRuleSSH*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a>Merhaba alt toohello ağ güvenlik grubu Ekle

Merhaba ağ güvenlik grubu kural uygulanan tooa alt ağ veya belirli bir sanal ağ arabirimi olabilir. Merhaba ağ güvenlik grubu tooour alt ekleme olanak sağlar. Alt ağ toohello ağ güvenlik grubuyla attach [az ağ sanal ağ alt ağı güncelleştirme](/cli/azure/network/vnet/subnet#update):

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a>Bir sanal ağ arabirim kartı toohello alt ağ Ekle

Sanal ağ arabirimi kartları (VNics), bunları toodifferent VM'ler bağlanarak yeniden gibi önemlidir. Merhaba VM'ler geçici olarak olabileceği bu yeniden tookeep hello Vnıc statik bir kaynak olarak sağlar. Bir Vnıc'teki oluşturun ve hello alt ağ ile ilişkilendirmek [az ağ NIC oluşturma](/cli/azure/network/nic#create). Merhaba aşağıdaki örnekte oluşturur adlı bir Vnıc'teki *myNic*:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Merhaba VM hello sanal ağ altyapısıyla dağıtma

Artık bir sanal ağ ve alt ağ ve bir ağ güvenlik grubu tooprotect hello alt SSH için bağlantı noktası 22 dışındaki tüm gelen trafiği engelleyerek sahipsiniz. Merhaba VM şimdi bu mevcut ağ altyapınızda içinde dağıtılabilir.

İle VM oluşturma [az vm oluşturma](/cli/azure/vm#create). Merhaba hakkında daha fazla bilgi toouse hello Azure CLI 2.0 toodeploy ile tam bir VM bayrakları için bkz: [hello Azure CLI kullanarak eksiksiz bir Linux ortamı oluşturma](create-cli-complete.md).

Aşağıdaki örnek hello Azure yönetilen diskleri kullanan bir VM oluşturur. Bu diskleri hello Azure platformu tarafından işlenir ve hazırlık veya konumu toostore gerektirmez bunları. Yönetilen diskler hakkında daha fazla bilgi için bkz. [Azure Yönetilen Disklere genel bakış](../../storage/storage-managed-disks-overview.md). Yönetilmeyen toouse diskleri istiyorsanız hello ek nota bakın.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

Yönetilen diskleri kullanırsanız, bu adımı atlayın. Yönetilmeyen toouse diskleri istiyorsanız, ek parametreler toohello devam etmeden komutu yönetilmeyen toocreate diskleri adlı hello depolama hesabındaki aşağıdaki tooadd hello gereksinim `mystorageaccount`: 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

Hello kullanarak CLI toocall var olan kaynakların çıkışı hello mevcut ağ içinde Azure toodeploy hello VM toplamasını işaretler. Bir sanal ağ ve alt ağ dağıtıldıktan sonra Azure bölgesi içinde statik veya kalıcı kaynaklar olarak bırakılabilir. Bu örnekte, değil oluşturun ve bu VM hello Internet genel olarak erişilebilir olmamasını sağlayacak şekilde genel bir IP adresi toohello Vnıc, atayın. Daha fazla bilgi için bkz: [hello Azure CLI kullanarak bir statik genel IP ile bir VM oluşturma](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).

## <a name="next-steps"></a>Sonraki adımlar
Azure'da yollar toocreate sanal makineler hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [Azure Resource Manager şablonu toocreate belirli bir dağıtım kullanın](../windows/cli-deploy-templates.md)
* [Azure CLI'si komutlarını doğrudan kullanarak bir Linux VM'si için kendi özel ortamınızı oluşturun](create-cli-complete.md)
* [Şablonları kullanarak Azure'da bir Linux VM oluşturma](create-ssh-secured-vm-from-template.md)
