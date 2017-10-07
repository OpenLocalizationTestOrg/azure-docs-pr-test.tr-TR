---
title: "aaaUse VM için iç DNS ad çözümlemesi hello Azure CLI 2.0 ile | Microsoft Docs"
description: "Nasıl toocreate sanal ağ arabirim kartları ve iç DNS hello Azure CLI 2.0 ile Azure VM ad çözümlemesi için kullanın"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a>Sanal ağ arabirim kartları oluşturma ve Azure VM ad çözümlemesi için iç DNS kullanma
Bu makalede nasıl ağ arabirimi kartları (vNics) ve DNS etiket adları'hello Azure CLI 2.0 ile tooset statik iç DNS adlarını Linux sanal kullanarak VM'ler gösterilmektedir. Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Statik DNS adları, bu belge için kullanılan bir Jenkins yapı sunucusu veya Git sunucusu gibi kalıcı altyapı hizmetleri için kullanılır.

Hello gereksinimleri şunlardır:

* [Bir Azure hesabı](https://azure.microsoft.com/pricing/free-trial/)
* [SSH ortak ve özel anahtar dosyaları](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>Hızlı komutlar
Tooquickly gerekiyorsa hello görevi, gerekli hello komutları bölümden hello ayrıntıları. Her adım hello belgenin hello kalan bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](#detailed-walkthrough). Aşağıdaki adımları tooperform ihtiyacınız hello son [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).

Ön gereksinimlerini: Kaynak grubu, sanal ağ ve alt ağ, ağ güvenlik grubu SSH ile gelen.

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a>Bir sanal ağ arabirim kartı statik iç DNS adı ile oluşturma
Merhaba Vnıc ile oluşturma [az ağ NIC oluşturma](/cli/azure/network/nic#create). Merhaba `--internal-dns-name` hello sanal ağ arabirim kartı (Vnıc) hello statik DNS ad sağlar ayarı hello DNS etiketi CLI bayrağı içindir. Merhaba aşağıdaki örnekte oluşturur adlı bir Vnıc'teki `myNic`, toohello bağlayan `myVnet` sanal ağ ve olarak adlandırılan bir iç DNS ad kayıt oluşturur `jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a>Bir VM'yi dağıtmak ve hello Vnıc bağlanın
[az vm create](/cli/azure/vm#create) ile bir VM oluşturun. Merhaba `--nics` bayrağı hello dağıtım tooAzure sırasında hello Vnıc toohello VM bağlanır. Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM` Azure yönetilen disklerle ve adlı ekler hello Vnıc `myNic` adım önceki hello gelen:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a>Ayrıntılı kılavuz

Bir tam sürekli tümleştirme ve sürekli dağıtımı (CiCd) altyapısı Azure ile ilgili belirli sunucuları toobe statik veya uzun süreli sunucuları gerektirir. Sanal ağlar ve ağ güvenlik grupları hello gibi Azure varlıklar statik ve nadiren dağıtılan kaynakları uzun ömürlü önerilir. Bir sanal ağ dağıtıldıktan sonra herhangi bir olumsuz etkiler toohello altyapı olmadan yeni dağıtımlar tarafından yeniden. Daha sonra bir Git deposu sunucusu ekleyebilir veya Jenkins Otomasyon sunucusu CiCd toothis geliştirme veya test ortamları için sanal ağ sunar.  

İç DNS adları, yalnızca bir Azure sanal ağı içinde çözülebilir. Merhaba DNS adlarını iç olduğundan, bunlar dışında ek güvenlik toohello altyapısı sağlayan Internet çözümlenebilir toohello değildir.

Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adlarında `myResourceGroup`, `myNic`, ve `myVM`.

## <a name="create-hello-resource-group"></a>Merhaba kaynak grubu oluştur
İlk olarak, hello kaynak grubuyla oluşturun [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westus` konumu:

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a>Merhaba sanal ağ oluşturma

Merhaba sonraki adım, bir sanal ağ toolaunch hello VM'ler içine toobuild olacaktır. Merhaba sanal ağ Bu izlenecek yol için bir alt ağ içerir. Azure sanal ağlar hakkında daha fazla bilgi için bkz: [hello Azure CLI kullanarak bir sanal ağ oluşturma](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Merhaba sanal ağ ile oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create). Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur `myVnet` ve adlı alt ağ `mySubnet`:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a>Merhaba ağ güvenlik grubu oluşturun
Azure ağ güvenlik grupları hello ağ katmanı eşdeğer tooa güvenlik duvarında değildir. Ağ güvenlik grupları hakkında daha fazla bilgi için bkz: [nasıl toocreate Nsg'ler Azure CLI hello](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Merhaba ağ güvenlik grubu oluşturma [az ağ nsg oluşturma](/cli/azure/network/nsg#create). Merhaba aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur `myNetworkSecurityGroup`:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a>Bir gelen kuralı tooallow SSH ekleme
Merhaba ağ güvenlik grubu için bir gelen kuralı Ekle [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create). Merhaba aşağıdaki örnek adlı bir kural oluşturur `myRuleAllowSSH`:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a>Ağ güvenlik grubu hello ile Merhaba alt ağını ilişkilendirin
Merhaba ağ güvenlik grubu ile tooassociate hello alt ağını [az ağ sanal ağ alt ağı güncelleştirme](/cli/azure/network/vnet/subnet#update). Merhaba aşağıdaki örnek ilişkilendirir hello alt ağ adı `mySubnet` hello adlı ağ güvenlik grubu ile `myNetworkSecurityGroup`:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a>Merhaba sanal ağ arabirim kartı ve statik DNS adları oluşturun
Azure çok esnektir, ancak toouse DNS adlarını VM ad çözümlemesi için bir DNS etiketi içeren toocreate sanal ağ arabirimi kartları (vNics) gerekir. bunları bağlantı kurarak toodifferent VM'ler hello altyapı yaşam döngüsü yeniden kullanabileceğiniz gibi vNics önemlidir. Bu yaklaşım Hello VM'ler geçici olarak olabileceği hello Vnıc statik bir kaynak olarak tutar. Merhaba vNic üzerinde etiketleme DNS kullanarak, mümkün tooenable basit ad çözümlemesi hello VNet içindeki diğer vm'lerden duyuyoruz. Hello DNS adı tarafından sağlayan diğer VM'ler tooaccess hello Otomasyon sunucusu çözümlenebilir adları kullanarak `Jenkins` veya hello Git sunucusu olarak `gitrepo`.  

Merhaba Vnıc ile oluşturma [az ağ NIC oluşturma](/cli/azure/network/nic#create). Merhaba aşağıdaki örnekte oluşturur adlı bir Vnıc'teki `myNic`, toohello bağlayan `myVnet` adlı sanal ağ `myVnet`ve olarak adlandırılan bir iç DNS ad kayıt oluşturur `jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Merhaba VM hello sanal ağ altyapısıyla dağıtma
Şimdi bir sanal ağ ve alt ağ, SSH ve bir Vnıc için bağlantı noktası 22 dışındaki tüm gelen trafiği engelleyerek bizim alt ağ güvenlik duvarı tooprotect davranan bir ağ güvenlik grubu sunuyoruz. Artık bu mevcut ağ altyapınızda içinde bir VM dağıtabilirsiniz.

[az vm create](/cli/azure/vm#create) ile bir VM oluşturun. Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM` Azure yönetilen disklerle ve adlı ekler hello Vnıc `myNic` adım önceki hello gelen:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

Hello kullanarak CLI toocall var olan kaynakların çıkışı biz hello mevcut ağ içinde Azure toodeploy hello VM istemeniz işaretler. bir VNet ve alt ağ dağıtıldıktan sonra tooreiterate, bunlar Azure bölgesi içinde statik veya kalıcı kaynaklar olarak bırakılabilir.  

## <a name="next-steps"></a>Sonraki adımlar
* [Azure CLI'si komutlarını doğrudan kullanarak bir Linux VM'si için kendi özel ortamınızı oluşturun](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Şablonları kullanarak Azure'da bir Linux VM oluşturma](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
