---
title: "Mevcut ağ Azure CLI 1.0 ile içine Linux VM'ler dağıtma | Microsoft Docs"
description: "Bir varolan sanal Azure CLI 1.0 kullanarak ağınıza bir Linux VM dağıtma"
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
ms.openlocfilehash: 767a3f7cadba6b1e71e5a8f5995a9db090e419dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli-10"></a>Mevcut Azure sanal ağda Azure CLI 1.0 ile Linux sanal makine dağıtma

Bu makalede Azure CLI 1.0 var olan bir sanal ağa (VNet) sanal makine (VM) dağıtmak için nasıl kullanılacağı gösterilmektedir. Gereksinimler şunlardır:

- [Bir Azure hesabı](https://azure.microsoft.com/pricing/free-trial/)
- [SSH ortak ve özel anahtar dosyaları](mac-create-ssh-keys.md)


## <a name="cli-versions-to-complete-the-task"></a>Görevi tamamlamak için kullanılacak CLI sürümleri
Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:

- [Azure CLI 1.0](#quick-commands) – bizim CLI Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md): Kaynak yönetimi dağıtım modeline yönelik yeni nesil CLI'mız


## <a name="quick-commands"></a>Hızlı Komutlar

Hızlı bir şekilde görevi gerçekleştirmek gerekiyorsa, aşağıdaki bölümde gerekli komutları ayrıntıları verilmektedir. Her adım, belgenin geri kalanında bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).

Ön gereksinimlerini: SSH ile kaynak grubu, VNet, NSG gelen, alt ağ. Tüm örnekleri kendi ayarlarınızla değiştirin.

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a>VM sanal ağ altyapısını dağıtma

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

Sanal ağlar Azure varlıklar gibi ve ağ güvenlik grupları nadiren dağıtılan kaynakları uzun ömürlü ve statik olması gerekir. Bir VNet dağıtıldıktan sonra hiçbir olumsuz etkiler altyapısı olmadan yeni dağıtımlar tarafından yeniden. Geleneksel donanım ağ anahtarı olarak VNet düşünün. Yepyeni bir donanım anahtarı ile her bir dağıtım yapılandırmak ihtiyaç duymaz. Doğru yapılandırılmış bir VNet ile birlikte, yeni sunucuları bu Vnet'i tekrar tekrar VNet ömrü boyunca gereken birkaç varsa, değişikliklerle dağıtmak, devam edebilirsiniz.

## <a name="create-the-resource-group"></a>Kaynak grubunu oluşturma

İlk olarak, bu kılavuzda oluşturduğunuz her şeyi düzenlemek için bir kaynak grubu oluşturun. Kaynak grupları hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md)

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-the-vnet"></a>Sanal ağ oluşturma

İlk adım, içine sanal makineleri başlatmak için bir VNet oluşturmaktır. Sanal ağ Bu izlenecek yol için bir alt ağ içerir. Azure sanal ağlar hakkında daha fazla bilgi için bkz: [Azure CLI kullanarak bir sanal ağ oluşturma](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-the-network-security-group"></a>Ağ güvenlik grubu oluşturun

Alt ardındaki var olan bir ağda yerleşik güvenlik grubu böylece alt önce ağ güvenlik grubu oluşturun. Azure ağ güvenlik grupları, bir Güvenlik Duvarı'nı ağ katmanında eşdeğerdir. Azure ağ güvenlik grupları hakkında daha fazla bilgi için bkz: [ağ güvenlik grupları Azure CLI oluşturma](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Gelen bir SSH izin ver Kuralı Ekle

Gelen bağlantı noktası 22 trafiği ağ üzerinden bağlantı noktası 22 VM geçirilmesine izin veren bir kural gerektiği şekilde VM internet erişimi olmalıdır.

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

## <a name="add-a-subnet-to-the-vnet"></a>Sanal ağ için bir alt ağ Ekle

Sanal ağ içindeki VM'ler bir alt ağda bulunması gerekir. Her sanal ağ birden çok alt ağa sahip olabilir. Alt ağ oluşturmak ve ağ güvenlik grubuyla ilişkilendirin.

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

Alt ağ şimdi VNet eklenir ve ağ güvenlik grubu ve kuralı ile ilişkilendirilmiş.


## <a name="add-a-vnic-to-the-subnet"></a>Alt ağ için bir Vnıc'teki Ekle

Sanal ağ kartları (VNics), bunları farklı VM'ler bağlanarak yeniden gibi önemlidir. Bu yaklaşım VM'ler geçici olarak olabileceği Vnıc statik bir kaynak olarak tutar. Bir Vnıc'teki oluşturun ve önceki adımda oluşturduğunuz alt ağ ile ilişkilendirin.

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a>VNet ve NSG halinde VM dağıtma

Artık bir VNet ve alt ağ, VNet ve alt ağ için SSH bağlantı noktası 22 dışındaki tüm gelen trafiği engelleyerek korumak için davranan bir ağ güvenlik grubu içinde vardır. VM şimdi bu mevcut ağ altyapınızda içinde dağıtılabilir.

Azure CLI kullanarak ve `azure vm create` komutu, var olan Azure kaynak grubu, sanal ağ, alt ağ ve Vnıc için Linux VM dağıtılır. Tam bir VM'yi dağıtmak için CLI kullanma ile ilgili daha fazla bilgi için bkz: [Azure CLI kullanarak eksiksiz bir Linux ortamı oluşturma](create-cli-complete.md)

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

Var olan kaynakları çağırmak için CLI bayrakları kullanarak, varolan ağ içindeki VM dağıtmak için Azure isteyin. Bir VNet ve alt ağ dağıtıldıktan sonra Azure bölgesi içinde statik veya kalıcı kaynaklar olarak bırakılabilir.  

## <a name="next-steps"></a>Sonraki adımlar

* [Belirli bir dağıtımı oluşturmak için Azure Resource Manager şablonu kullanma](../windows/cli-deploy-templates.md)
* [Azure CLI'si komutlarını doğrudan kullanarak bir Linux VM'si için kendi özel ortamınızı oluşturun](create-cli-complete.md)
* [Şablonları kullanarak Azure'da bir Linux VM oluşturma](create-ssh-secured-vm-from-template.md)
