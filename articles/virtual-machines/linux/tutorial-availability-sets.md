---
title: "Linux VM'ler için Azure kullanılabilirlik kümeleri Öğreticisi | Microsoft Docs"
description: "Linux VM'ler için Azure kullanılabilirlik kümeleri hakkında bilgi edinin."
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
ms.openlocfilehash: 63fe3f165864f06228604cac56d06cc061ab25f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-availability-sets"></a>Kullanılabilirlik kümeleri kullanma


Bu öğreticide, kullanılabilirlik ve kullanılabilirlik kümeleri adlı bir özelliği kullanarak azure'da sanal makine çözümlerinizi güvenilirliğini artırmak öğreneceksiniz. Kullanılabilirlik kümeleri, Azure üzerinde dağıttığınız VM'ler arasında birden fazla yalıtılmış donanım küme dağıtıldığından emin olmak. Bunun yapılması Azure içinde bir donanım veya yazılım hatası olur, alt kümesini, VM'ler etkilenir ve çözümünüzün genel kullanılabilir ve kullanmaya müşterilerinizin perspektifinden işletim kalacağı sağlar.

Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Kullanılabilirlik kümesi oluşturma
> * Bir kullanılabilirlik kümesine bir VM oluşturma
> * Kullanılabilir VM boyutları denetleyin


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Yüklemek ve CLI yerel olarak kullanmak seçerseniz, Bu öğretici, Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Sürümü bulmak için `az --version` komutunu çalıştırın. Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="availability-set-overview"></a>Kullanılabilirlik kümesi'ne genel bakış

Bir kullanılabilirlik kümesi Azure'da Azure veri merkezi içinde dağıtıldığında içine yerleştirin VM kaynakları birbirinden yalıtılmış olduğundan emin olmak için kullanabileceğiniz bir mantıksal bir gruplandırma bir özelliktir. Azure birden çok fiziksel sunucuda çalıştırmak bir kullanılabilirlik kümesi içinde yerleştirin VM'ler sağlar, işlem rafları, depolama birimi ve ağ anahtarları. Bu bir donanım veya Azure yazılım başarısız olması durumunda yalnızca bir alt kümesini, VM'ler etkilenir ve genel uygulamanız kalması ve müşterileriniz için kullanılabilir olmaya devam sağlar. Kullanılabilirlik kümelerini kullanarak, güvenilir bulut çözümleri oluşturmak istediğinizde yararlanmak için gerekli bir özelliktir.

Şimdi burada 4 ön uç web sunucusu ve bir veritabanı ana bilgisayar 2 arka uç VM kullanmak bir tipik VM tabanlı çözümünü göz önünde bulundurun. Azure ile Vm'leriniz dağıtmadan önce iki kullanılabilirlik kümesi tanımlamak istersiniz: bir kullanılabilirlik kümesi için "web" katmanı ve bir kullanılabilirlik kümesi için "veritabanı" katmanı. Ardından belirtebilirsiniz yeni bir VM oluştururken kullanılabilirlik kümesi az vm parametresi komut oluşturur ve Azure otomatik olarak kullanılabilir kümesi içinde oluşturduğunuz VM'ler ilişkilendirilmesini sağlar yalıtılmış birden çok fiziksel donanım kaynaklarına arasında. Bu, bir Web sunucusu veya veritabanı sunucusu sanal makineleri çalıştıran fiziksel donanımı bir sorun varsa, çünkü bunlar üzerinde farklı donanım diğer örneklerini Web sunucusu ve veritabanı VM'ler düzgün çalışır durumda olduğunu bildiğinizden anlamına gelir.

Azure içinde güvenilir VM tabanlı çözümler dağıtmak istediğinizde kullanılabilirlik kümeleri her zaman kullanmalısınız.


## <a name="create-an-availability-set"></a>Kullanılabilirlik kümesi oluşturma

Kullanılabilirlik kümesi kullanarak oluşturabileceğiniz [az vm kullanılabilirlik kümesi oluşturma](/cli/azure/vm/availability-set#create). Bu örnekte, her iki güncelleştirme ve hata etki alanlarının sayısı ayarlarız *2* kullanılabilirlik adlandırılmış kümesi için *myAvailabilitySet* içinde *myResourceGroupAvailability* kaynak grubu.

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

Kullanılabilirlik kümeleri kaynaklar "hata etki alanları" ve "güncelleme etki alanları" arasında yalıtmanızı sağlar. A **hata etki alanı** sunucu, ağ + depolama yalıtılmış bir koleksiyonunu temsil eder kaynakları. Önceki örnekte bizim kullanılabilirlik bizim VM'ler dağıtıldığında en az iki hata etki alanları arasında dağıtılacak kümesi istiyoruz gösterir. Biz de iki arasında dağıtılmış kümesi bizim kullanılabilirlik istiyoruz belirtmek **güncelleştirme etki alanları**.  İki güncelleştirme etki alanı Azure yazılım güncelleştirmelerini gerçekleştirdiğinde VM KAYNAKLARIMIZI, aynı anda güncelleştirilmiş bizim VM altında çalışan tüm yazılım önleme, yalıtılmış olduğundan emin olun.

## <a name="configure-virtual-network"></a>Sanal ağ yapılandırma
Bazı sanal makineleri dağıtmak ve, dengeleyici sınayabilirsiniz önce destekleyici sanal ağ kaynakları oluşturun. Sanal ağlar hakkında daha fazla bilgi için bkz: [Azure Sanal Ağları Yönet](tutorial-virtual-network.md) Öğreticisi.

### <a name="create-network-resources"></a>Ağ kaynakları oluşturun
Bir sanal ağ ile oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create). Aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* adlı bir alt ağ ile *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
Sanal NIC ile oluşturulan [az ağ NIC oluşturma](/cli/azure/network/nic#create). Aşağıdaki örnek, üç sanal NIC oluşturur. (Her VM için bir sanal NIC için aşağıdaki adımları uygulamayı oluşturduğunuz). Ek sanal NIC ve sanal makineleri herhangi bir zamanda oluşturabilir ve bunları yük dengeleyiciye ekleyin:

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

Sanal makineleri kullanılabilirlik donanım üzerinde doğru şekilde dağıtıldığından emin olmak için kümesini içinde oluşturulmalıdır. Kullanılabilirlik oluşturulduktan sonra kümesi için mevcut bir VM'yi ekleyemezsiniz. 

Kullanarak bir VM oluştururken [az vm oluşturma](/cli/azure/vm#create) kullanılarak ayarlanan kullanılabilirlik belirttiğiniz `--availability-set` kullanılabilirlik kümesinin adını belirtmek için parametre.

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

Şimdi iki sanal makine, yeni oluşturulan kullanılabilirlik kümesinde sahibiz. Aynı kullanılabilirlik kümesinde olduklarından, Azure sanal makineleri ve tüm kaynaklarını (veri diskleri dahil), yalıtılmış fiziksel donanım üzerinde dağıtılmış güvence altına alır. Bu dağıtım kadar yüksek kullanılabilirlik bizim genel VM çözümünün sağlamaya yardımcı olur.

Sanal makineleri ekledikçe karşılaşabileceğiniz bir belirli bir VM boyutu artık kullanılabilirlik kümesi içinde kullanmak için kullanılabilir olan şeydir. Artık kullanılabilirlik kümesi zorlar yalıtım kuralları korurken eklemek için yeterli kapasitesi varsa bu sorun oluşabilir. Hangi VM boyutları varolan kullanılabilirlik kullanarak kümesi içinde kullanmak için kullanılabilir olup olmadığını kontrol edebilirsiniz `--availability-set list-sizes` parametresi.

## <a name="check-for-available-vm-sizes"></a>Kullanılabilir VM boyutları denetle 

Daha fazla sanal makineleri daha sonra ayarlamak kullanılabilirlik ekleyebilirsiniz, ancak hangi VM boyutları donanımda kullanılabilir olduğunu bilmeniz gerekir. Kullanım [az vm kullanılabilirlik kümesi listesi-boyutları](/cli/azure/availability-set#list-sizes) tüm donanım üzerinde kullanılabilir boyutları küme için kullanılabilirlik kümesi listelemek için.

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

Sanal makine ölçek kümeleri hakkında bilgi edinmek için sonraki öğretici ilerleyin.

> [!div class="nextstepaction"]
> [VM ölçek kümesi oluşturma](tutorial-create-vmss.md)

