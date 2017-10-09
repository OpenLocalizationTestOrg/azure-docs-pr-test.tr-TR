---
title: "aaaOpen tooa Linux VM Azure CLI 2.0 ile bağlantı noktaları | Microsoft Docs"
description: "Bilgi nasıl tooopen bir bağlantı noktası / bir uç nokta tooyour Linux VM oluşturma hello Azure resource manager dağıtım kullanarak modeli ve Azure CLI 2.0 hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a>Bağlantı noktaları ve uç noktaları tooa Linux VM hello Azure CLI ile Aç
Bir bağlantı noktasını açın ya da bir uç nokta oluşturma tooa bir alt ağ veya VM ağ arabirimine bir ağ filtre oluşturarak azure'da sanal makine (VM). Gelen ve giden trafiği denetleyen bu filtreler hello trafiği alan bir bağlı ağ güvenlik grubu toohello kaynakta yerleştirin. Bağlantı noktası 80 üzerinde web trafiği yaygın bir örneği kullanalım. Bu makale size nasıl gösterir tooopen hello Azure CLI 2.0 ile bir bağlantı noktası tooa VM. Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](nsg-quickstart-nodejs.md).


## <a name="quick-commands"></a>Hızlı komutlar
toocreate bir ağ güvenlik grubu ve ihtiyacınız olan kuralların hello son [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).

Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adlarında *myResourceGroup*, *myNetworkSecurityGroup*, ve *myVnet*.

Merhaba ağ güvenlik grubu oluşturma [az ağ nsg oluşturma](/cli/azure/network/nsg#create). Merhaba aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur *myNetworkSecurityGroup* hello içinde *eastus* konumu:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Olan bir kural eklemek [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create) tooallow HTTP trafiği tooyour Web sunucusu (veya SSH erişim ya da veritabanı bağlantısı gibi kendi senaryosu için ayarlayın). Merhaba aşağıdaki örnek adlı bir kural oluşturur *myNetworkSecurityGroupRule* tooallow TCP bağlantı noktası 80 üzerinde trafiği:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

VM ağ arabirimi (NIC) ilişkilendirmek Hello ağ güvenlik grubu [az ağ NIC güncelleştirmesi](/cli/azure/network/nic#update). Merhaba aşağıdaki örnek ilişkilendirir adlı mevcut NIC'in *myNic* hello adlı ağ güvenlik grubu ile *myNetworkSecurityGroup*:

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

Alternatif olarak, bir sanal ağ alt ağı ile ağ güvenlik grubu ilişkilendirebilirsiniz [az ağ sanal ağ alt ağı güncelleştirme](/cli/azure/network/vnet/subnet#update) yalnızca tek bir VM'de ağ arabirimi toohello yerine. Merhaba aşağıdaki örnek ilişkilendirir adlı mevcut bir alt *mySubnet* hello içinde *myVnet* hello adlı ağ güvenlik grubu ile sanal ağ *myNetworkSecurityGroup*:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a>Ağ güvenlik grupları hakkında daha fazla bilgi
Burada hızlı komutları Hello tooget yukarı ve trafik boyunca tooyour VM ile çalışmaya izin verir. Ağ güvenlik grupları, birçok harika özellikler ve denetleme tooyour kaynaklara erişmek için ayrıntı düzeyi sağlar. Daha fazla bilgi edinebilirsiniz [bir ağ güvenlik grubu ve ACL oluşturma kuralları burada](tutorial-virtual-network.md#secure-network-traffic).

Yüksek oranda kullanılabilir web uygulamaları için Azure yük dengeleyici arkasında Vm'leriniz yerleştirmeniz gerekir. Merhaba yük dengeleyici trafik filtreleme sağlar bir ağ güvenlik grubuyla trafiği tooVMs dağıtır. Daha fazla bilgi için bkz: [nasıl tooload Bakiye Linux sanal yüksek oranda kullanılabilir bir uygulama içinde Azure toocreate makineleri](tutorial-load-balancer.md).

## <a name="next-steps"></a>Sonraki adımlar
Bu örnekte, bir basit kural tooallow HTTP trafiği oluşturuldu. Aşağıdaki makaleleri hello ayrıntılı ortamları oluşturma hakkında bilgi bulabilirsiniz:

* [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md)
* [Ağ Güvenlik Grubu (NSG) Nedir?](../../virtual-network/virtual-networks-nsg.md)
