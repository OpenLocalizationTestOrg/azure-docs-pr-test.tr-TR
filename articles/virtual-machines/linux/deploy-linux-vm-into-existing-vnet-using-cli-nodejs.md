---
title: "mevcut ağ Azure CLI 1.0 ile içine aaaDeploy Linux VM'ler | Microsoft Docs"
description: "Nasıl toodeploy kullanarak varolan bir sanal ağ içinde bir Linux VM hello Azure CLI 1.0"
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
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a>Nasıl toodeploy mevcut Azure sanal ağda hello Azure CLI 1.0 ile Linux sanal makine

Bu makale size nasıl gösterir toouse Azure CLI 1.0 toodeploy mevcut sanal ağda (VNet) sanal makine (VM). Hello gereksinimleri şunlardır:

- [Bir Azure hesabı](https://azure.microsoft.com/pricing/free-trial/)
- [SSH ortak ve özel anahtar dosyaları](mac-create-ssh-keys.md)


## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 1.0](#quick-commands) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için


## <a name="quick-commands"></a>Hızlı Komutlar

Tooquickly gerekiyorsa hello görevi, gerekli hello komutları bölümden hello ayrıntıları. Her adım hello belgenin hello kalan bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).

Ön gereksinimlerini: SSH ile kaynak grubu, VNet, NSG gelen, alt ağ. Tüm örnekleri kendi ayarlarınızla değiştirin.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Merhaba VM hello sanal ağ altyapısıyla dağıtma

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a>Ayrıntılı kılavuz

Azure varlıklar hello sanal ağlar gibi ve ağ güvenlik grupları nadiren dağıtılan kaynakları uzun ömürlü ve statik olması gerekir. Bir VNet dağıtıldıktan sonra herhangi bir olumsuz etkiler toohello altyapı olmadan yeni dağıtımlar tarafından yeniden. Geleneksel donanım ağ anahtarı olarak VNet düşünün. Yeni donanım ile her bir dağıtım geçiş tooconfigure ihtiyaç duymaz. Doğru yapılandırılmış bir VNet ile birlikte toodeploy yeni sunucuları bu sanal ağ içinde tekrar tekrar hello VNet hello ömrü boyunca gereken birkaç varsa, değişikliklerle devam edebilirsiniz.

## <a name="create-hello-resource-group"></a>Merhaba kaynak grubu oluştur

İlk olarak, bir kaynak grubu tooorganize bu kılavuzda oluşturduğunuz her şeyi oluşturun. Kaynak grupları hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md)

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a>Merhaba VNet oluşturma

Merhaba ilk VNet toolaunch hello VM'ler içine toobuild adımdır. Merhaba VNet Bu izlenecek yol için bir alt ağ içerir. Azure sanal ağlar hakkında daha fazla bilgi için bkz: [hello Azure CLI kullanarak bir sanal ağ oluşturma](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a>Merhaba ağ güvenlik grubu oluşturun

Merhaba alt varolan bir ağ güvenlik grubu yerleşik şekilde hello alt önce hello ağ güvenlik grubu oluşturun. Azure ağ güvenlik grupları hello ağ katmanı eşdeğer tooa güvenlik duvarında değildir. Azure ağ güvenlik grupları hakkında daha fazla bilgi için bkz: [nasıl hello Azure CLI toocreate ağ güvenlik grupları](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Gelen bir SSH izin ver Kuralı Ekle

Merhaba VM gelen bağlantı noktası 22 trafiği toobe veren bir kural hello ağ tooport 22 hello VM üzerinde geçirilen şekilde Internet gerekli hello erişimden gerekir.

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>Bir alt ağ toohello VNet ekleme

VM'ler hello VNet içindeki bir alt ağda bulunması gerekir. Her sanal ağ birden çok alt ağa sahip olabilir. Merhaba alt ağı oluşturup hello ağ güvenlik grubuyla ilişkilendirin.

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

Merhaba alt şimdi hello VNet eklenir ve hello ağ güvenlik grubu ve kuralı ile ilişkilendirilmiş.


## <a name="add-a-vnic-toohello-subnet"></a>Vnıc toohello alt ağ Ekle

Sanal ağ kartları (VNics), bunları toodifferent VM'ler bağlanarak yeniden gibi önemlidir. Bu yaklaşım Hello VM'ler geçici olarak olabileceği hello Vnıc statik bir kaynak olarak tutar. Bir Vnıc'teki oluşturup hello önceki adımda oluşturduğunuz hello alt ağı ile ilişkilendirin.

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Merhaba VM hello VNet içine ve NSG dağıtma

Artık bir VNet ve alt ağ, sanal ağ ve SSH için bağlantı noktası 22 dışındaki tüm gelen trafiği engelleyerek tooprotect hello alt davranan bir ağ güvenlik grubu içinde vardır. Merhaba VM şimdi bu mevcut ağ altyapınızda içinde dağıtılabilir.

Kullanarak Azure CLI hello ve hello `azure vm create` hello Linux VM olan Azure kaynak grubu, sanal ağ, alt ağ ve Vnıc varolan dağıtılan toohello komutu. Hello CLI toodeploy tam VM kullanma hakkında daha fazla bilgi için bkz: [hello Azure CLI kullanarak eksiksiz bir Linux ortamı oluşturma](create-cli-complete.md)

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

Hello kullanarak CLI toocall var olan kaynakların çıkışı hello mevcut ağ içinde Azure toodeploy hello VM toplamasını işaretler. Bir VNet ve alt ağ dağıtıldıktan sonra Azure bölgesi içinde statik veya kalıcı kaynaklar olarak bırakılabilir.  

## <a name="next-steps"></a>Sonraki adımlar

* [Azure Resource Manager şablonu toocreate belirli bir dağıtım kullanın](../windows/cli-deploy-templates.md)
* [Azure CLI'si komutlarını doğrudan kullanarak bir Linux VM'si için kendi özel ortamınızı oluşturun](create-cli-complete.md)
* [Şablonları kullanarak Azure'da bir Linux VM oluşturma](create-ssh-secured-vm-from-template.md)
