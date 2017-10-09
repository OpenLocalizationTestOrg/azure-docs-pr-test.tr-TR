---
title: "aaaAzure CLI komut dosyası örneği - rota trafiği ağ sanal gereç aracılığıyla | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - güvenlik duvarı ağ sanal gereç yoluyla trafiği yönlendirme."
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
ms.openlocfilehash: 981d6073be04a7ebaf96b657fbab8a378e7a995e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a>Bir ağ sanal gereç yoluyla trafiği yönlendirme

Bu komut dosyası örneği ön uç ve arka uç alt ağları ile bir sanal ağ oluşturur. Ayrıca hello iki alt ağlar arasında etkin tooroute trafiğinin iletme IP ile VM oluşturur. Merhaba komut dosyasını çalıştırdıktan sonra bir güvenlik duvarı uygulaması toohello VM gibi ağ yazılım dağıtabilirsiniz.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>Örnek komut dosyası


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]

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
| [az ağ alt ağı oluşturun](/cli/azure/network/vnet/subnet#create) | Arka uç ve DMZ alt ağlar oluşturur. |
| [az ağ genel IP oluşturun](/cli/azure/network/public-ip#create) | Ortak IP adresi tooaccess hello VM Internet hello oluşturur. |
| [az ağ NIC oluşturun](/cli/azure/network/nic#create) | Bir sanal ağ arabirimi ve onu için IP iletimini etkinleştirme oluşturur. |
| [az ağ nsg oluşturma](/cli/azure/network/nsg#create) | Bir ağ güvenlik grubu (NSG) oluşturur. |
| [az ağ nsg kuralı oluşturma](/cli/azure/network/nsg/rule#create) | HTTP ve HTTPS bağlantı noktalarını toohello VM gelene izin ver NSG kuralları oluşturur. |
| [az ağ sanal ağ alt ağı güncelleştirme](/cli/azure/network/vnet/subnet#update)| Nsg'ler ilişkilendirilmiş bir hello ve rota toosubnets tabloları. |
| [az ağ rota tablosu oluştur](/cli/azure/network/route-table#create)| Tüm yollar için yol tablosu oluşturur. |
| [az ağ yol tablosu yol oluşturma](/cli/azure/network/route-table/route#create)| Yollar tooroute trafiği alt ağlar arasında ve hello Internet üzerinden hello VM oluşturur. |
| [az vm oluşturma](/cli/azure/vm#create) | Bir sanal makine oluşturur ve hello NIC tooit ekler. Bu komut ayrıca hello sanal makine görüntü toouse ve yönetici kimlik bilgilerini belirtir. |
| [az grubu Sil](/cli/azure/group#delete) | Bir kaynak grubu ve içerdiği tüm kaynakları siler. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](/cli/azure/overview).

Ek ağ CLI kod örnekleri hello bulunabilir [Azure ağ genel görünümü belgeleri](../cli-samples.md)
