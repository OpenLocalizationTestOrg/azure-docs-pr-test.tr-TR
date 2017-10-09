---
title: "aaaOpen tooa Linux VM Azure CLI 1.0 ile bağlantı noktaları | Microsoft Docs"
description: "Bilgi nasıl tooopen bir bağlantı noktası / bir uç nokta tooyour Linux VM oluşturma hello Azure resource manager dağıtım kullanarak modeli ve Azure CLI 1.0 hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a>Azure kullanarak açma bağlantı noktaları ve uç noktaları tooa Linux VM hello Azure CLI 1.0
Bir bağlantı noktasını açın ya da bir uç nokta oluşturma tooa bir alt ağ veya VM ağ arabirimine bir ağ filtre oluşturarak azure'da sanal makine (VM). Gelen ve giden trafiği denetleyen bu filtreler hello trafiği alan bir bağlı ağ güvenlik grubu toohello kaynakta yerleştirin. Bağlantı noktası 80 üzerinde web trafiği yaygın bir örneği kullanalım. Bu makalede, nasıl bir bağlantı noktası tooa VM kullanarak tooopen hello Azure CLI 1.0 gösterir.


## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 1.0](#quick-commands) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](nsg-quickstart.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için


## <a name="quick-commands"></a>Hızlı komutlar
toocreate bir ağ güvenlik grubu ve gereksinim kurallarını [Azure CLI 1.0 hello](../../cli-install-nodejs.md) yüklü ve kullanarak Resource Manager moduna:

```azurecli
azure config mode arm
```

Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adları dahil *myResourceGroup*, *myNetworkSecurityGroup*, ve *myVnet*.

Kendi ad ve konum uygun şekilde girme, ağ güvenlik grubu oluşturun. Merhaba aşağıdaki örnekte oluşturur adlı bir ağ güvenlik grubu *myNetworkSecurityGroup* hello içinde *eastus* konumu:

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Bir kural tooallow HTTP trafiği tooyour Web ekleme (veya SSH erişim ya da veritabanı bağlantısı gibi kendi senaryosu için ayarlama). Merhaba aşağıdaki örnek adlı bir kural oluşturur *myNetworkSecurityGroupRule* tooallow TCP bağlantı noktası 80 üzerinde trafiği:

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

Ağ güvenlik grubu Hello VM ağ arabirimi (NIC) ile ilişkilendirin. Merhaba aşağıdaki örnek ilişkilendirir adlı mevcut NIC'in *myNic* hello adlı ağ güvenlik grubu ile *myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

Alternatif olarak, ağ güvenlik grubu sadece tek bir VM'de ağ arabirimi toohello yerine bir sanal ağ alt ağ ile ilişkilendirebilirsiniz. Merhaba aşağıdaki örnek ilişkilendirir adlı mevcut bir alt *mySubnet* hello içinde *myVnet* hello adlı ağ güvenlik grubu ile sanal ağ *myNetworkSecurityGroup*:

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a>Ağ güvenlik grupları hakkında daha fazla bilgi
Burada hızlı komutları Hello tooget yukarı ve trafik boyunca tooyour VM ile çalışmaya izin verir. Ağ güvenlik grupları, birçok harika özellikler ve denetleme tooyour kaynaklara erişmek için ayrıntı düzeyi sağlar. Daha fazla bilgi edinebilirsiniz [bir ağ güvenlik grubu ve ACL oluşturma kuralları burada](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).

Azure Resource Manager şablonları bir parçası olarak ağ güvenlik grupları ve ACL kuralları tanımlayabilirsiniz. Daha fazla bilgi edinin [şablonları ile ağ güvenlik grupları oluşturma](../../virtual-network/virtual-networks-create-nsg-arm-template.md).

VM üzerinde toouse bağlantı noktası iletme toomap benzersiz dış bağlantı noktası tooan iç bağlantı noktası gerekiyorsa, bir yük dengeleyici ve ağ adresi çevirisi (NAT) kuralları kullanır. Örneğin, tooexpose TCP bağlantı noktası 8080 dışarıdan istediğiniz ve bir VM üzerinde yönlendirilen trafiği tooTCP bağlantı noktası 80 sahip. Hakkında bilgi alabilirsiniz [bir Internet'e yönelik Yük Dengeleyici oluşturma](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).

## <a name="next-steps"></a>Sonraki adımlar
Bu örnekte, bir basit kural tooallow HTTP trafiği oluşturuldu. Aşağıdaki makaleleri hello ayrıntılı ortamları oluşturma hakkında bilgi bulabilirsiniz:

* [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md)
* [Ağ Güvenlik Grubu (NSG) Nedir?](../../virtual-network/virtual-networks-nsg.md)
* [Yük Dengeleyiciler için Azure Resource Manager'a genel bakış](../../load-balancer/load-balancer-arm.md)

