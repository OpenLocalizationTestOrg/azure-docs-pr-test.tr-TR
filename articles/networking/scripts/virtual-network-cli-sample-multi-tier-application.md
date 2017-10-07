---
title: "aaaAzure CLI betik örnek - çok katmanlı uygulamalar için bir ağ oluşturun. | Microsoft Docs"
description: "Azure CLI betik örnek - çok katmanlı uygulamalar için bir sanal ağ oluşturun."
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: deeb3f459499cebd1b8ded6a299eb759d49cf08d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a>Çok katmanlı uygulamalar için bir ağ oluşturma

Bu komut dosyası örneği ön uç ve arka uç alt ağları ile bir sanal ağ oluşturur. Trafik toohello ön uç alt sınırlı tooHTTP ve SSH, trafik toohello sırasında arka uç alt sınırlı tooMySQL, bağlantı noktası 3306. Çalışan hello betik sonra iki sanal makine, bir web sunucusu ve MySQL yazılım dağıtabilirsiniz her alt ağda gerekir.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>Örnek komut dosyası


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate aşağıdaki hello bir kaynak grubu, sanal ağ ve ağ güvenlik grupları kullanır. Her komut hello tablosundaki toocommand özgü belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az ağ vnet oluşturma](/cli/azure/network/vnet#create) | Bir Azure sanal ağı ve ön uç alt ağı oluşturur. |
| [az ağ alt ağı oluşturun](/cli/azure/network/vnet/subnet#create) | Bir arka uç alt ağı oluşturur. |
| [az ağ genel IP oluşturun](/cli/azure/network/public-ip#create) | Ortak IP adresi tooaccess hello VM Internet hello oluşturur. |
| [az ağ NIC oluşturun](/cli/azure/network/nic#create) | Sanal ağ arabirimi oluşturur ve bunları toohello sanal ağın ön uç ve arka uç alt ekler. |
| [az ağ nsg oluşturma](/cli/azure/network/nsg#create) | İlişkili toohello ön uç ve arka uç alt ağlar, ağ güvenlik gruplarını (NSG) oluşturur. |
| [az ağ nsg kuralı oluşturma](/cli/azure/network/nsg/rule#create) |İzin verme veya engelleme belirli bağlantı noktalarını toospecific alt NSG kuralları oluşturur. |
| [az vm oluşturma](/cli/azure/vm#create) | Sanal makineler oluşturur ve NIC tooeach VM ekler. Bu komut ayrıca hello sanal makine görüntü toouse ve yönetici kimlik bilgilerini belirtir. |
| [az grubu Sil](/cli/azure/group#delete) | Bir kaynak grubu ve içerdiği tüm kaynakları siler. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](/cli/azure/overview).

Ek ağ CLI kod örnekleri hello bulunabilir [Azure ağ genel görünümü belgeleri](../cli-samples.md)
