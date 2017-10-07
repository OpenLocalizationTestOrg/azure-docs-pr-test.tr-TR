---
title: "aaaUsing VM için iç DNS ad çözümlemesi Azure üzerinde | Microsoft Docs"
description: "Azure VM ad çözümlemesi için iç DNS kullanarak."
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
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a>Azure VM ad çözümlemesi için iç DNS kullanma

Bu makalede sanal NIC kartları (Vnıc) ve DNS etiket adları kullanarak nasıl tooset Linux VM'ler için statik iç DNS adlarını gösterir. Statik DNS adları, bu belge için kullanılan bir Jenkins yapı sunucusu veya Git sunucusu gibi kalıcı altyapı hizmetleri için kullanılır.

Hello gereksinimleri şunlardır:

* [Bir Azure hesabı](https://azure.microsoft.com/pricing/free-trial/)
* [SSH ortak ve özel anahtar dosyaları](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 1.0](#quick-commands) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için


## <a name="quick-commands"></a>Hızlı komutlar

Tooquickly gerekiyorsa hello görevi, gerekli hello komutları bölümden hello ayrıntıları. Her adım hello belgenin hello kalan bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](#detailed-walkthrough).  

Ön gereksinimlerini: SSH ile kaynak grubu, VNet, NSG gelen, alt ağ.

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a>Statik iç DNS adı ile bir Vnıc'teki oluşturma

Merhaba `-r` hello Vnıc hello statik DNS ad sağlar ayarı hello DNS etiketi CLI bayrağı içindir.

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a>Merhaba VNet, NSG içine Hello VM dağıtmak ve hello Vnıc bağlanın

Merhaba `-N` hello Vnıc toohello bağlayan hello dağıtım tooAzure sırasında yeni VM.

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a>Ayrıntılı kılavuz

Bir tam sürekli tümleştirme ve sürekli dağıtımı (CiCd) altyapısı Azure ile ilgili belirli sunucuları toobe statik veya uzun süreli sunucuları gerektirir.  Merhaba sanal ağlar (Vnet'ler) ve ağ güvenlik grupları (Nsg'ler) gibi Azure varlıklar statik olmalıdır ve nadiren dağıtılan kaynakları uzun ömürlü önerilir.  Bir VNet dağıtıldıktan sonra herhangi bir olumsuz etkiler toohello altyapı olmadan yeni dağıtımlar tarafından yeniden.  Toothis statik ağ Git ekleme deposu sunucusu ve Jenkins Otomasyon sunucusu sunar CiCd tooyour geliştirme veya test ortamları.  

İç DNS adları, yalnızca bir Azure sanal ağı içinde çözülebilir.  Merhaba DNS adlarını iç olduğundan, bunlar dışında ek güvenlik toohello altyapısı sağlayan Internet çözümlenebilir toohello değildir.

_Tüm örnekleri kendi adlandırma ile değiştirin._

## <a name="create-hello-resource-group"></a>Merhaba kaynak grubu oluştur

Bir kaynak grubu gerekli tooorganize bu kılavuzda oluşturuyoruz gereken her şey vardır.  Azure kaynak grupları hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a>Merhaba VNet oluşturma

Merhaba ilk VNet toolaunch hello VM'ler içine toobuild adımdır.  Merhaba VNet Bu izlenecek yol için bir alt ağ içerir.  Azure sanal ağlar hakkında daha fazla bilgi için bkz: [hello Azure CLI kullanarak bir sanal ağ oluşturma](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a>Merhaba NSG oluşturma

Biz hello NSG önce hello alt ağ oluşturmak için varolan bir ağ güvenlik grubu hello alt oluşturulmuştur.  Azure Nsg'ler hello ağ katmanında eşdeğer tooa Güvenlik Duvarı ' dir.  Azure Nsg'ler hakkında daha fazla bilgi için bkz: [nasıl toocreate Nsg'ler Azure CLI hello](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Gelen bir SSH izin ver Kuralı Ekle

Merhaba Linux VM gelen bağlantı noktası 22 trafiği toobe veren bir kural hello ağ tooport 22 hello Linux VM üzerinde geçirilen şekilde Internet gerekli hello erişimden gerekir.

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>Bir alt ağ toohello VNet ekleme

VM'ler hello VNet içindeki bir alt ağda bulunması gerekir.  Her sanal ağ birden çok alt ağa sahip olabilir.  Merhaba alt ağı oluşturup hello NSG tooadd bir güvenlik duvarı toohello alt hello alt ağını ilişkilendirin.

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

Merhaba alt şimdi hello VNet eklenir ve hello NSG ve hello NSG kuralı ile ilişkilendirilmiş.

## <a name="creating-static-dns-names"></a>Statik DNS adları oluşturuluyor

Azure çok esnektir, ancak toouse DNS adlarını VM'ler ad çözümlemesi için sanal olarak etiketleme DNS kullanarak (VNics) ağ kartı toocreate gerekir.  Bunları bağlantı kurarak toodifferent VM'ler hello VM'ler geçici olarak olabileceği, statik bir kaynak olarak hello Vnıc tutan yeniden kullanabileceğiniz gibi VNics önemlidir.  Merhaba VNic üzerinde etiketleme DNS kullanarak, mümkün tooenable basit ad çözümlemesi hello VNet içindeki diğer vm'lerden duyuyoruz.  Hello DNS adı tarafından sağlayan diğer VM'ler tooaccess hello Otomasyon sunucusu çözümlenebilir adları kullanarak `Jenkins` veya hello Git sunucusu olarak `gitrepo`.  Bir Vnıc'teki oluşturun ve alt ağ hello önceki adımda oluşturduğunuz hello ile ilişkilendirin.

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Merhaba VM hello VNet içine ve NSG dağıtma

Şimdi bir sanal ağ, bir alt ağ, sanal ağ ve SSH için bağlantı noktası 22 dışındaki tüm gelen trafiği engelleyerek bizim alt ağ güvenlik duvarı tooprotect davranan bir NSG içinde sunuyoruz.  Merhaba VM şimdi bu mevcut ağ altyapınızda içinde dağıtılabilir.

Kullanarak Azure CLI hello ve hello `azure vm create` hello Linux VM olan Azure kaynak grubu, sanal ağ, alt ağ ve Vnıc varolan dağıtılan toohello komutu.  Hello CLI toodeploy tam VM kullanma hakkında daha fazla bilgi için bkz: [hello Azure CLI kullanarak eksiksiz bir Linux ortamı oluşturma](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

Hello kullanarak CLI toocall var olan kaynakların çıkışı biz hello mevcut ağ içinde Azure toodeploy hello VM istemeniz işaretler.  bir VNet ve alt ağ dağıtıldıktan sonra tooreiterate, bunlar Azure bölgesi içinde statik veya kalıcı kaynaklar olarak bırakılabilir.  

## <a name="next-steps"></a>Sonraki adımlar
* [Azure CLI'si komutlarını doğrudan kullanarak bir Linux VM'si için kendi özel ortamınızı oluşturun](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Şablonları kullanarak Azure'da bir Linux VM oluşturma](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
