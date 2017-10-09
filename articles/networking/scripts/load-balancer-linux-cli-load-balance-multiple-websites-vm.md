---
title: "aaaAzure CLI komut dosyası örneği - yük dengelemesi hello Azure CLI ile birden çok Web siteleri | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - yük dengelemesi birden çok Web siteleri toohello aynı sanal makine"
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
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a>Yük Dengelemesi birden çok Web sitesi

Bu komut dosyası örneği iki sanal bir kullanılabilirlik kümesi üyesi olan makinelerle (VM) bir sanal ağ oluşturur. Bir yük dengeleyici iki ayrı trafiğini yönlendiren IP adresleri toohello iki VM'ler. Sonra çalışan hello komut dosyası, web sunucusu yazılım toohello VM'ler dağıtın ve her biri kendi IP adresiyle birden çok web sitesini barındırmak.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası toocreate bir kaynak grubu, sanal ağ, yük dengeleyici ve tüm ilişkili kaynakları komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az ağ vnet oluşturma](https://docs.microsoft.com/cli/azure/network/vnet#create) | Bir Azure sanal ağ ve alt ağ oluşturur. |
| [az ağ genel IP oluşturun](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Bir ortak IP adresi statik bir IP adresi ve ilişkili bir DNS adı ile oluşturur. |
| [az ağ lb oluşturma](https://docs.microsoft.com/cli/azure/network/lb#create) | Bir Azure yük dengeleyici oluşturur. |
| [az ağ lb araştırması oluştur](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Bir yük dengeleyici araştırması oluşturur. Yük Dengeleyici araştırmasını hello yük dengeleyici kümesindeki her bir VM kullanılan toomonitor değil. Tüm VM erişilemez hale gelirse, trafik yönlendirilmiş toohello VM değildir. |
| [az ağ lb kuralı oluşturma](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Yük Dengeleyici kuralı oluşturur. Bu örnekte, bağlantı noktası 80 için bir kural oluşturulur. HTTP trafiği hello yük dengeleyicide ulaştığında, yönlendirilmiş tooport 80 olur hello VM'ler hello yük dengeleyici kümesindeki biri. |
| [az ağ lb ön uç-IP oluşturun](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | Merhaba yük dengeleyici için bir ön uç IP adresi oluşturun. |
| [az ağ lb adres havuzu oluşturma](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | Arka uç adres havuzu oluşturur. |
| [az ağ NIC oluşturun](https://docs.microsoft.com/cli/azure/network/nic#create) | Bir sanal ağ kartı oluşturur ve toohello sanal ağ ve alt ekler. |
| [az vm kullanılabilirlik kümesi oluştur](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Bir kullanılabilirlik kümesi oluşturur. Kullanılabilirlik kümeleri, sağlayacak şekilde hello kümesinin tamamını değil hatası oluşursa, etkilenen hello sanal makineler arasında fiziksel kaynakları yayarak uygulama çalışma süresi emin olun. |
| [az ağ NIC IP-config oluşturma](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | Bir IP confiuration oluşturur. Merhaba Microsoft.Network/AllowMultipleIpConfigurationsPerNic özelliği, aboneliğiniz için etkin olması gerekir. Merhaba birincil IP yapılandırması hello--yapma birincil bayrağı kullanarak NIC başına yalnızca bir yapılandırma atanabilir. |
| [az vm oluşturma](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve NSG bağlanır. Bu komut ayrıca kullanılan hello sanal makine görüntü toobe belirtir ve yönetici kimlik bilgileri.  |
| [az grubu Sil](https://docs.microsoft.com/cli/azure/vm/extension#set) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek ağ CLI kod örnekleri hello bulunabilir [Azure ağ genel görünümü belgelerine](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
