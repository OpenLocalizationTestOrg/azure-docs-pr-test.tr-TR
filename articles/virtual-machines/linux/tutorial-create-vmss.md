---
title: "Linux Azure için sanal makine ölçek kümeleri oluşturma | Microsoft Docs"
description: "Bir sanal makine ölçek kümesini kullanarak Linux VM'ler üzerinde yüksek oranda kullanılabilir bir uygulama oluşturun ve dağıtın"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 2b8d519e11f70eda164bd8f6e131a3989f242ab0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a>Bir sanal makine ölçek kümesi oluşturma ve Linux üzerinde yüksek oranda kullanılabilir bir uygulama dağıtma
Bir sanal makine ölçek kümesini dağıtmak ve aynı, otomatik ölçeklendirme sanal makineler kümesi yönetmenize olanak sağlar. Ölçek kümesindeki VM'lerin sayısını elle ölçeklendirme ya da CPU kullanımı, bellek isteğe bağlı veya ağ trafiğini göre otomatik ölçeklendirme kurallarını tanımlayabilirsiniz. Bu öğreticide, Azure üzerinde ayarlanmış bir sanal makine ölçek dağıtın. Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:

> [!div class="checklist"]
> * Bulut init ölçeklendirmek için bir uygulama oluşturmak için kullanın
> * Bir sanal makine ölçek kümesi oluşturma
> * Artırma veya azaltma ölçek kümesindeki örnek sayısı
> * Ölçek kümesi örnekleri için bağlantı bilgileri görüntüle
> * Veri diskleri bir ölçek kümesinde kullanın


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Yüklemek ve CLI yerel olarak kullanmak seçerseniz, Bu öğretici, Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Sürümü bulmak için `az --version` komutunu çalıştırın. Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="scale-set-overview"></a>Ölçek kümesi'ne genel bakış
Bir sanal makine ölçek kümesini dağıtmak ve aynı, otomatik ölçeklendirme sanal makineler kümesi yönetmenize olanak sağlar. Ölçek kümeleri kullanan aynı bileşenleri, ilgili önceki öğreticide öğrenilen [yüksek oranda kullanılabilir sanal makineleri oluşturmak](tutorial-availability-sets.md). VM ölçek kümesindeki bir kullanılabilirlik kümesi ve mantığı arıza ve güncelleştirme etki alanları arasında dağıtılan oluşturulur.

VM ölçek kümesindeki gerektiği şekilde oluşturulur. Nasıl ve ne zaman VM'ler eklendiğinde veya kaldırıldığında ölçek kümesi denetlemek için otomatik ölçeklendirme kurallarını tanımlayın. Bu kurallar temel alınarak ölçümleri CPU yükünü, bellek kullanımı veya ağ trafiğini gibi tetikleyebilir.

Bir Azure platform görüntüsü kullandığınızda ölçek 1.000 VM'ler kadar destek ayarlar. Üretim iş yükleri için istediğiniz [özel bir VM görüntüsü oluşturma](tutorial-custom-images.md). Özel görüntü kullanırken ayarlayın bir ölçek en fazla 100 sanal makineleri oluşturabilirsiniz.


## <a name="create-an-app-to-scale"></a>Ölçeklendirmek için uygulama oluşturma
Üretim kullanımı için istediğiniz [özel bir VM görüntüsü oluşturma](tutorial-custom-images.md) uygulamanızın yüklenmiş ve yapılandırılmış içerir. Bu öğretici için hızlı şekilde ölçeği eylemini Ayarla görmek için sanal makinelerin ilk önyükleme özelleştirme sağlar.

Bir önceki öğreticide öğrenilen [Linux sanal bir makinede ilk önyükleme özelleştirmek nasıl](tutorial-automate-vm-deployment.md) bulut init ile. NGINX yüklemek ve basit bir 'Hello World' Node.js uygulaması çalıştırmak için aynı bulut init yapılandırma dosyası kullanabilirsiniz. 

Geçerli kabuğunuzu adlı bir dosya oluşturun *bulut init.txt* ve aşağıdaki yapılandırma yapıştırın. Örneğin, yerel makinenizde olmayan bulut kabuğunda dosyası oluşturun. Girin `sensible-editor cloud-init.txt` dosyası oluşturun ve kullanılabilir düzenleyicileri listesini görmek için. Tüm bulut init dosyanın doğru şekilde kopyalandığından emin olun özellikle ilk satırı:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```


## <a name="create-a-scale-set"></a>Bir ölçek kümesi oluşturma
Ölçek kümesini oluşturmadan önce bir kaynak grubuyla oluşturmanız [az grubu oluşturma](/cli/azure/group#create). Aşağıdaki örnek, bir kaynak grubu oluşturur *myResourceGroupScaleSet* içinde *eastus* konumu:

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

Şimdi bir sanal makine ölçek kümesi oluşturmak [az vmss oluşturma](/cli/azure/vmss#create). Aşağıdaki örnek, ölçeği adlandırılmış Ayarla oluşturur *myScaleSet*VM özelleştirmek için bulut init dosyasını kullanır ve bunlar yoksa SSH anahtarları oluşturur:

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

Oluşturun ve tüm sanal makineleri ve ölçek kümesi kaynakları yapılandırmak için birkaç dakika sürer. Azure CLI sorusu döndükten sonra çalışmaya devam arka plan görevleri vardır. Başka bir birkaç uygulamaya erişmek için dakika olabilir.


## <a name="allow-web-traffic"></a>Web trafiği izin ver
Bir yük dengeleyici sanal makine ölçek kümesinin bir parçası olarak otomatik olarak oluşturuldu. Yük Dengeleyici trafiği yük dengeleyici kuralları kullanarak tanımlanan VM'ler kümesi arasında dağıtır. Yük Dengeleyici kavramları ve sonraki öğreticide yapılandırma hakkında daha fazla bilgiyi [sanal makinelerin azure'da yük dengelemesini nasıl](tutorial-load-balancer.md).

Web uygulamasına ulaşması trafiğine izin vermek için bir kural oluştururken [az ağ lb kuralını](/cli/azure/network/lb/rule#create). Aşağıdaki örnek, adında bir kural oluşturur *myLoadBalancerRuleWeb*:

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a>Uygulamanızı test etme
Node.js uygulamanızı Web'de görmek için yük dengeleyici ile genel IP adresi elde [az ağ ortak IP Göster](/cli/azure/network/public-ip#show). Aşağıdaki örnek IP adresi alacağı *myScaleSetLBPublicIP* ölçek kümesinin bir parçası olarak oluşturulan:

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

Ortak IP adresini bir web tarayıcısına girin. Ana bilgisayar trafiği için yük dengeleyici dağıtılmış VM adını dahil olmak üzere uygulama gösterilir:

![Çalışan Node.js uygulaması](./media/tutorial-create-vmss/running-nodejs-app.png)

Eylem kümesini görmek için zorla uygulamanızı çalıştıran tüm VM'ler arasında trafiği dağıtmak yük dengeleyici görmek için web tarayıcınızın yenileme.


## <a name="management-tasks"></a>Yönetim görevleri
Ölçek kümesini yaşam döngüsü boyunca, bir veya daha fazla yönetim görevleri çalıştırmanız gerekebilir. Ayrıca, çeşitli yaşam döngüsü görevleri otomatikleştiren komut dosyaları oluşturmak isteyebilirsiniz. Azure CLI 2.0, bu görevleri gerçekleştirmek için hızlı bir yoludur. Birkaç ortak görevler şunlardır.

### <a name="view-vms-in-a-scale-set"></a>Görünüm VM ölçek kümesindeki
Ölçek kümesinde çalışan sanal makineler listesini görüntülemek için kullanın [az vmss listesi-örneklerini](/cli/azure/vmss#list-instances) gibi:

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

Çıktı aşağıdaki örneğe benzer:

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a>Artırma veya azaltma VM örnekleri
Ölçek kümesindeki şu anda sahip örneklerinin sayısını görmek için [az vmss Göster](/cli/azure/vmss#show) ve sorgulayın *sku.capacity*:

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

Daha sonra el ile artırabilir veya sanal makine ölçek kümesi sayısını azaltmak [az vmss ölçek](/cli/azure/vmss#scale). Aşağıdaki örnek VM'lerin sayısını ayarlamak, Ölçek ayarlar *5*:

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

Otomatik ölçeklendirme kurallarını, yukarı veya aşağı VM'lerin sayısını yanıt ağ trafiğini veya CPU kullanımı gibi isteğe bağlı olarak ayarlamak, Ölçek ölçeklendirme tanımlamanıza olanak sağlar. Şu anda, bu kurallar Azure CLI 2. 0'olarak ayarlanamaz. Kullanım [Azure portal](https://portal.azure.com) otomatik ölçeklendirme yapılandırmak için.

### <a name="get-connection-info"></a>Bağlantı bilgilerini al
Ölçek kümesindeki sanal makineleri bağlantı bilgilerini almak için kullanın [az vmss listesi-örnek-bağlantı-bilgisi](/cli/azure/vmss#list-instance-connection-info). Bu komut, SSH ile bağlanmanıza olanak sağlayan her bir VM için genel IP adresi ve bağlantı noktası çıkarır:

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a>Veri diskleri ölçek kümeleri ile kullanma
Oluşturun ve veri diskleri ölçek kümeleri ile kullanın. Bir önceki öğreticide öğrenilen nasıl [yönetmek Azure diskleri](tutorial-manage-disks.md) en iyi uygulamalar ve işletim sistemi diski yerine veri diskleri uygulamaları oluşturmaya yönelik performans geliştirmeleri özetler.

### <a name="create-scale-set-with-data-disks"></a>Veri diskleri ile ölçek kümesi oluşturma
Ölçek kümesi oluşturmak ve veri diskleri eklemek için Ekle `--data-disk-sizes-gb` parametresi [az vmss oluşturma](/cli/azure/vmss#create) komutu. Aşağıdaki örnek, bir ölçek kümesi oluşturur *50*Gb veri disklerinin her örneğine eklenmiş:

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

Ölçek kümesindeki örnekleri kaldırıldığında, eklenen veri disklerini de kaldırılır.

### <a name="add-data-disks"></a>Veri diski Ekle
Örnekler, Ölçek kümesindeki bir veri diski eklemek için kullanın [az vmss diskini](/cli/azure/vmss/disk#attach). Aşağıdaki örnek, bir *50*Gb disk her örneği için:

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a>Veri diskleri ayırma
Ölçek kümesindeki bir veri diski örneklerine kaldırmak için kullanın [az vmss disk ayırma](/cli/azure/vmss/disk#detach). Aşağıdaki örnek veri diski LUN değerine kaldırır *2* her örneğinden:

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, bir sanal makine ölçek kümesi oluşturuldu. Size nasıl öğrenilen için:

> [!div class="checklist"]
> * Bulut init ölçeklendirmek için bir uygulama oluşturmak için kullanın
> * Bir sanal makine ölçek kümesi oluşturma
> * Artırma veya azaltma ölçek kümesindeki örnek sayısı
> * Ölçek kümesi örnekleri için bağlantı bilgileri görüntüle
> * Veri diskleri bir ölçek kümesinde kullanın

Yük Dengeleme sanal makineler için kavramları hakkında daha fazla bilgi için sonraki öğretici ilerleyin.

> [!div class="nextstepaction"]
> [Sanal makinelerin yük dengelemesini](tutorial-load-balancer.md)