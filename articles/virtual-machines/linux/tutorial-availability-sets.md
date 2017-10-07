---
title: "aaaAvailability öğretici Azure Linux VM'ler için ayarlar | Microsoft Docs"
description: "Azure Linux VM'ler için Hello kullanılabilirlik kümeleri hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a>Nasıl toouse kullanılabilirlik kümeleri


Bu öğreticide, nasıl tooincrease hello kullanılabilirliği ve güvenilirliği bir özelliği kullanarak azure'da sanal makine çözümlerinizi kullanılabilirlik kümeleri adlı öğreneceksiniz. Kullanılabilirlik kümeleri, Azure üzerinde dağıttığınız VM'lerin birden çok yalıtılmış donanım kümeler arasında dağıtılır, hello emin olun. Bunun yapılması Azure içinde bir donanım veya yazılım hatası olur, alt kümesini, VM'ler etkilenir ve çözümünüzün genel kullanılabilir ve işletimsel kullanmadan müşterilerinizin hello açısından kalacak sağlar.

Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Kullanılabilirlik kümesi oluşturma
> * Bir kullanılabilirlik kümesine bir VM oluşturma
> * Kullanılabilir VM boyutları denetleyin


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="availability-set-overview"></a>Kullanılabilirlik kümesi'ne genel bakış

Bir kullanılabilirlik kümesi kullanabileceğiniz bir mantıksal bir gruplandırma bir Azure veri merkezi içinde dağıtıldığında içine yerleştirin hello VM kaynakları birbirinden yalıtılmış Azure tooensure içinde bir özelliktir. Bu hello VM'ler arasında birden fazla fiziksel sunucu çalıştırmak bir kullanılabilirlik kümesi içinde yerleştirin Azure sağlar, işlem rafları, depolama birimi ve ağ anahtarları. Bu hello olay bir donanım ya da Azure yazılım hatası yalnızca bir alt kümesini, VM'ler etkilenir ve genel uygulamanız kalması ve toobe kullanılabilir tooyour müşteriler devam sağlar. Toobuild güvenilir bulut çözümleri istediğiniz kullanılabilirlik kümelerini kullanarak bir önemli özelliği tooleverage durumdur.

Şimdi burada 4 ön uç web sunucusu ve bir veritabanı ana bilgisayar 2 arka uç VM kullanmak bir tipik VM tabanlı çözümünü göz önünde bulundurun. Azure ile Vm'leriniz dağıtmadan önce toodefine iki kullanılabilirlik kümeleri istiyor: hello "web" katmanı ve bir kullanılabilirlik kümesi için hello "veritabanı" katmanı için bir kullanılabilirlik kümesi. Ardından, bir parametre toohello az vm komutu oluşturun ve Azure otomatik olarak o hello hello içinde oluşturduğunuz VM'ler sağlayacak şekilde ayarlayın hello kullanılabilirlik belirtebilirsiniz yeni bir VM oluştururken kümesi yalıtılmış birden çok fiziksel donanım kaynaklarına arasında. Bir Web sunucusu veya veritabanı sunucusu VM'ler üzerinde çalıştığı hello fiziksel donanım bir sorun varsa, o hello bilmeniz yani farklı donanıma olduğundan Web sunucusu ve veritabanı VM'ler diğer örneklerini düzgün çalışır durumda.

Toodeploy güvenilir VM tabanlı çözümler Azure içinde istediğinizde kullanılabilirlik kümeleri her zaman kullanmalısınız.


## <a name="create-an-availability-set"></a>Kullanılabilirlik kümesi oluşturma

Kullanılabilirlik kümesi kullanarak oluşturabileceğiniz [az vm kullanılabilirlik kümesi oluşturma](/cli/azure/vm/availability-set#create). Bu örnekte, güncelleştirme ve hata etki alanları iki hello sayısı ayarlarız *2* hello kullanılabilirlik adlandırılmış kümesi için *myAvailabilitySet* hello içinde *myResourceGroupAvailability*kaynak grubu.

Bir kaynak grubu oluşturun.

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

Kullanılabilirlik kümeleri "hata etki alanları" ve "güncelleme etki alanları" arasında tooisolate kaynaklar sağlar. A **hata etki alanı** sunucu, ağ + depolama yalıtılmış bir koleksiyonunu temsil eder kaynakları. Örnek önceki hello bizim VM'ler dağıtıldığında en az iki hata etki alanları arasında dağıtılan toobe bizim kullanılabilirlik kümesi istiyoruz gösterir. Biz de iki arasında dağıtılmış kümesi bizim kullanılabilirlik istiyoruz belirtmek **güncelleştirme etki alanları**.  İki güncelleştirme etki alanı Azure yazılım güncelleştirmelerini gerçekleştirdiğinde VM KAYNAKLARIMIZI, hello güncelleştirilmiş bizim VM altında çalışan tüm hello yazılım önleme, yalıtılmış olduğundan emin olun aynı anda.

## <a name="configure-virtual-network"></a>Sanal ağ yapılandırma
Bazı sanal makineleri dağıtmak ve, dengeleyici sınayabilirsiniz önce sanal ağ kaynaklarına destekleme hello oluşturun. Sanal ağlar hakkında daha fazla bilgi için bkz: Merhaba [Azure Sanal Ağları Yönet](tutorial-virtual-network.md) Öğreticisi.

### <a name="create-network-resources"></a>Ağ kaynakları oluşturun
Bir sanal ağ ile oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create). Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* adlı bir alt ağ ile *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
Sanal NIC ile oluşturulan [az ağ NIC oluşturma](/cli/azure/network/nic#create). Merhaba aşağıdaki örnek üç sanal NIC oluşturur. (Bir sanal NIC aşağıdaki hello uygulamanızda adımları için oluşturduğunuz her VM için). Ek sanal NIC ve sanal makineleri herhangi bir zamanda oluşturmak ve bunları toohello yük dengeleyici Ekle:

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a>VM'ler içinde bir kullanılabilirlik kümesi oluştur

Sanal makineleri hello kullanılabilirlik kümesi toomake hello donanım üzerinde doğru şekilde dağıtıldığından emin içinde oluşturulmalıdır. Var olan VM tooan kullanılabilirlik kümesi oluşturulduktan sonra eklenemez. 

Kullanarak bir VM oluştururken [az vm oluşturma](/cli/azure/vm#create) hello kullanılarak ayarlanan hello kullanılabilirlik belirttiğiniz `--availability-set` parametresi toospecify hello hello kullanılabilirlik kümesi adını.

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

Şimdi iki sanal makine, yeni oluşturulan kullanılabilirlik kümesinde sahibiz. İçinde olduklarından aynı hello kullanılabilirlik kümesi, Azure uyduğundan emin olabilirsiniz, hello VM'ler ve tüm kaynaklarını (veri diskleri dahil), yalıtılmış fiziksel donanım arasında dağıtılır. Bu dağıtım kadar yüksek kullanılabilirlik bizim genel VM çözümünün sağlamaya yardımcı olur.

Bir şey VM'ler ekledikçe karşılaşabileceğiniz belirli bir VM boyutu artık kullanılabilirlik kümesi içinde kullanılabilir toouse olmasıdır. Artık varsa onu hello yalıtım kuralları hello kullanılabilirlik kümesini korurken zorlar yeterli kapasitesi tooadd Bu sorun oluşabilir. Var olan kullanılabilirlik hello kullanarak kümesi içinde kullanılabilir toouse hangi VM boyutları: toosee denetleyebilirsiniz `--availability-set list-sizes` parametresi.

## <a name="check-for-available-vm-sizes"></a>Kullanılabilir VM boyutları denetle 

Daha fazla sanal makineleri toohello kullanılabilirlik kümesi daha sonra ekleyebilirsiniz, ancak hangi VM boyutları hello donanımda kullanılabilir tooknow gerekir. Kullanım [az vm kullanılabilirlik kümesi listesi-boyutları](/cli/azure/availability-set#list-sizes) tüm hello kullanılabilir boyutları hello donanımda hello kullanılabilirlik kümesi için küme toolist.

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:

> [!div class="checklist"]
> * Kullanılabilirlik kümesi oluşturma
> * Bir kullanılabilirlik kümesine bir VM oluşturma
> * Kullanılabilir VM boyutları denetleyin

Sanal makine ölçek kümeleri hakkında toohello sonraki öğretici toolearn ilerleyin.

> [!div class="nextstepaction"]
> [VM ölçek kümesi oluşturma](tutorial-create-vmss.md)

