---
title: "aaaAzure CLI komut dosyası örneği - yüksek kullanılabilirlik için Yük Dengeleme trafik tooVMs | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - yüksek kullanılabilirlik için Yük Dengeleme trafiği tooVMs"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 0954b5c261512724dfb9c6e7be123c9d45624f4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a>Bakiye trafiği tooVMs yüksek kullanılabilirlik için yük

Bu komut dosyası örneği gereken her şeyi oluşturur toorun birkaç Ubuntu sanal makineleri yüksek oranda kullanılabilir yapılandırılmış ve yük dengeli yapılandırma. Çalışan hello betik sonra üç sanal makineler, birleştirilmiş tooan Azure kullanılabilirlik kümesi, sahip olur ve bir Azure yük dengeleyici üzerinden erişilebilir. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine, kullanılabilirlik kümesi, yük dengeleyici ve tüm ilgili kaynaklar aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az ağ vnet oluşturma](https://docs.microsoft.com/cli/azure/network/vnet#create) | Bir Azure sanal ağ ve alt ağ oluşturur. |
| [az ağ genel IP oluşturun](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Bir ortak IP adresi statik bir IP adresi ve ilişkili bir DNS adı ile oluşturur. |
| [az ağ lb oluşturma](https://docs.microsoft.com/cli/azure/network/lb#create) | Bir Azure yük dengeleyici oluşturur. |
| [az ağ lb araştırması oluştur](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Bir yük dengeleyici araştırması oluşturur. Yük Dengeleyici araştırmasını hello yük dengeleyici kümesindeki her bir VM kullanılan toomonitor değil. Tüm VM erişilemez hale gelirse, trafik yönlendirilmiş toohello VM değildir. |
| [az ağ lb kuralı oluşturma](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Yük Dengeleyici kuralı oluşturur. Bu örnekte, bağlantı noktası 80 için bir kural oluşturulur. HTTP trafiği hello yük dengeleyicide ulaştığında, yönlendirilmiş tooport 80 olur hello VM'ler hello LB kümesindeki biri. |
| [az ağ lb gelen nat-kuralı oluşturma](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | Yük Dengeleyici ağ adresi çevirisi (NAT) kuralı oluşturur.  NAT kuralları bir bağlantı noktasının hello yük dengeleyici tooa bir VM'de eşleyin. Bu örnekte, hello yük dengeleyici kümesindeki SSH trafiği tooeach VM için NAT kuralı oluşturulur.  |
| [az ağ nsg oluşturma](https://docs.microsoft.com/cli/azure/network/nsg#create) | Merhaba Internet ve hello sanal makine arasında bir güvenlik sınırı olan bir ağ güvenlik grubu (NSG) oluşturur. |
| [az ağ nsg kuralı oluşturma](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Bir NSG kural tooallow oluşturur gelen trafiği. Bu örnekte, bağlantı noktası 22 SSH trafiği için açıldı. |
| [az ağ NIC oluşturun](https://docs.microsoft.com/cli/azure/network/nic#create) | Bir sanal ağ kartı oluşturur ve toohello sanal ağ, alt ağ ve NSG ekler. |
| [az vm kullanılabilirlik kümesi oluştur](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Bir kullanılabilirlik kümesi oluşturur. Kullanılabilirlik kümeleri, sağlayacak şekilde hello kümesinin tamamını değil hatası oluşursa, etkilenen hello sanal makineler arasında fiziksel kaynakları yayarak uygulama çalışma süresi emin olun. |
| [az vm oluşturma](/cli/azure/vm#create) | Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve NSG bağlanır. Bu komut ayrıca kullanılan hello sanal makine görüntü toobe belirtir ve yönetici kimlik bilgileri.  |
| [az grubu Sil](https://docs.microsoft.com/cli/azure/vm/extension#set) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek ağ Azure CLI kod örnekleri hello bulunabilir [Azure ağ belgeleri](../cli-samples.md).
