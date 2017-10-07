---
title: "aaaAzure CLI komut dosyası örneği - bir iç ve dış NSG ile iki VM oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - iç ve dış NSG ile iki VM oluşturma"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ba6a70200ca2923369e37b13531bd7ca65b05a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a>Sanal makineler arasındaki ağ trafiğini güvenli

Bu komut dosyası iki sanal makine oluşturur ve gelen trafiği tooboth güvenliğini sağlar. Bir sanal makine üzerinde erişilebilir olduğundan hello internet ve ağ güvenlik grubu (NSG) bağlantı noktası 22 ve bağlantı noktası 80 üzerinde tooallow trafiği yapılandırdı. Merhaba ikinci sanal makine üzerinde erişilebilir değil Internet hello ve sahip bir NSG yapılandırılmış tooonly izin hello ilk sanal makineye gelen trafiği. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az ağ vnet oluşturma](https://docs.microsoft.com/cli/azure/network/vnet#create) | Bir Azure sanal ağ ve alt ağ oluşturur. |
| [az ağ sanal alt oluşturma](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | Bir alt ağı oluşturur. |
| [az vm oluşturma](https://docs.microsoft.com/cli/azure/vm#create) | Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve NSG bağlanır. Bu komut ayrıca kullanılan hello sanal makine görüntü toobe ve yönetici kimlik bilgilerini belirtir.  |
| [az ağ nsg kuralı listesi](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | Bir ağ güvenlik grubu kural hakkındaki bilgileri döndürür. Bu örnekte, hello kural adı, daha sonra hello betik kullanmak için bir değişkende depolanır. |
| [az ağ nsg kural güncelleştirmesi](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | Bir NSG kuralını güncelleştirir. Bu örnekte, trafiğin yalnızca hello ön uç alt ağından güncelleştirilmiş toopass hello arka uç kuralıdır. |
| [az grubu Sil](https://docs.microsoft.com/cli/azure/vm/extension#set) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
