---
title: "aaaCreate Linux Azure için sanal makine ölçek kümeleri | Microsoft Docs"
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
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a>Bir sanal makine ölçek kümesi oluşturma ve Linux üzerinde yüksek oranda kullanılabilir bir uygulama dağıtma
Bir sanal makine ölçek kümesi toodeploy sağlar ve aynı, otomatik ölçeklendirme sanal makineler kümesi yönetin. Merhaba hello ölçek kümesindeki VM'lerin sayısını elle ölçeklendirme ya da CPU kullanımı, bellek isteğe bağlı veya ağ trafiğini dayalı kurallar tooautoscale tanımlayabilirsiniz. Bu öğreticide, Azure üzerinde ayarlanmış bir sanal makine ölçek dağıtın. Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:

> [!div class="checklist"]
> * Bulut init toocreate bir uygulama tooscale kullanın
> * Bir sanal makine ölçek kümesi oluşturma
> * Artırma veya azaltma hello ölçek kümesi örneği sayısı
> * Ölçek kümesi örnekleri için bağlantı bilgileri görüntüle
> * Veri diskleri bir ölçek kümesinde kullanın


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="scale-set-overview"></a>Ölçek kümesi'ne genel bakış
Bir sanal makine ölçek kümesi toodeploy sağlar ve aynı, otomatik ölçeklendirme sanal makineler kümesi yönetin. Ölçek, hakkında hello önceki öğreticide çok öğrenilen bu kullanım hello aynı bileşenleri ayarlar[yüksek oranda kullanılabilir sanal makineleri oluşturmak](tutorial-availability-sets.md). VM ölçek kümesindeki bir kullanılabilirlik kümesi ve mantığı arıza ve güncelleştirme etki alanları arasında dağıtılan oluşturulur.

VM ölçek kümesindeki gerektiği şekilde oluşturulur. Otomatik ölçeklendirme kurallarını toocontrol tanımladığınız nasıl ve ne zaman VM'ler eklenir veya hello ölçek kümesinden kaldırılır. Bu kurallar temel alınarak ölçümleri CPU yükünü, bellek kullanımı veya ağ trafiğini gibi tetikleyebilir.

Ölçek too1, Azure platform görüntüsü kullandığınızda 000 VM'ler desteği ayarlar. Üretim iş yükleri için çok isteyebilir[özel bir VM görüntüsü oluşturma](tutorial-custom-images.md). Özel görüntü kullanırken ayarlayın ölçeğinde too100 Vm'leri yedekleme oluşturabilirsiniz.


## <a name="create-an-app-tooscale"></a>Bir uygulama tooscale oluşturma
Üretim kullanımı için çok isteyebilir[özel bir VM görüntüsü oluşturma](tutorial-custom-images.md) uygulamanızın yüklenmiş ve yapılandırılmış içerir. Bu öğretici için ilk önyükleme tooquickly Vm'lerinde ölçeği eylemini Ayarla bkz hello özelleştirme sağlar.

Bir önceki öğreticide öğrenilen [nasıl toocustomize Linux sanal bir makinede ilk önyükleme](tutorial-automate-vm-deployment.md) bulut init ile. Kullanabileceğiniz aynı bulut init yapılandırma dosyası tooinstall NGINX hello ve basit bir 'Hello World' Node.js uygulaması çalıştırın. 

Geçerli kabuğunuzu adlı bir dosya oluşturun *bulut init.txt* Yapıştır hello izleyerek yapılandırma. Örneğin, yerel makinenizde değil hello bulut Kabuk hello dosya oluşturun. Girin `sensible-editor cloud-init.txt` toocreate hello dosya ve kullanılabilir düzenleyicileri listesini görebilirsiniz. Merhaba tüm bulut init dosyanın doğru şekilde kopyalandığından emin olun, özellikle ilk satırı hello:

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
Ölçek kümesini oluşturmadan önce bir kaynak grubuyla oluşturmanız [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupScaleSet* hello içinde *eastus* konumu:

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

Şimdi bir sanal makine ölçek kümesi oluşturmak [az vmss oluşturma](/cli/azure/vmss#create). Merhaba aşağıdaki örnekte oluşturur ölçeği adlandırılmış Ayarla *myScaleSet*hello bulut init dosya toocustomize hello VM kullanır ve mevcut SSH anahtarları oluşturur:

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

Birkaç dakika toocreate alır ve tüm hello ölçek kümesi kaynakları ve VM'ler yapılandırın. Hello Azure CLI toohello istemi döndükten sonra toorun devam arka plan görevleri vardır. Başka bir birkaç hello uygulamaya erişmek için dakika olabilir.


## <a name="allow-web-traffic"></a>Web trafiği izin ver
Bir yük dengeleyici hello sanal makine ölçek kümesinin bir parçası olarak otomatik olarak oluşturuldu. Merhaba yük dengeleyici trafiği yük dengeleyici kuralları kullanarak tanımlanan VM'ler kümesi arasında dağıtır. Yük Dengeleyici kavramları ve hello sonraki öğreticide yapılandırma hakkında daha fazla bilgiyi [nasıl tooload Bakiye azure'daki sanal makinelerde](tutorial-load-balancer.md).

tooallow trafiği tooreach hello web uygulaması, bir kural oluştururken [az ağ lb kuralı oluşturma](/cli/azure/network/lb/rule#create). Merhaba aşağıdaki örnek adlı bir kural oluşturur *myLoadBalancerRuleWeb*:

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
toosee Node.js uygulamanızı hello Web'de elde hello genel IP adresi, yük dengeleyici ile [az ağ ortak IP Göster](/cli/azure/network/public-ip#show). Merhaba aşağıdaki örnek alacağı için başlangıç IP adresi *myScaleSetLBPublicIP* hello ölçek kümesinin bir parçası olarak oluşturulan:

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

Tooa web tarayıcısında Hello genel IP adresi girin. VM bu hello yük dengeleyici dağıtılmış trafiği hello hello ana dahil olmak üzere Hello uygulama görüntülenir:

![Çalışan Node.js uygulaması](./media/tutorial-create-vmss/running-nodejs-app.png)

toosee hello ölçeği, eylemde ayarla, zorla yenileme web tarayıcısı toosee hello yük dengeleyici, uygulamanızı çalıştıran tüm hello VM'ler arasında trafiği dağıtın.


## <a name="management-tasks"></a>Yönetim görevleri
Merhaba ölçek kümesini Hello yaşam döngüsü boyunca toorun gerekebilir bir veya daha fazla yönetim görevleri. Ayrıca, çeşitli yaşam döngüsü görevleri otomatikleştiren toocreate komut dosyaları isteyebilirsiniz. Hello Azure CLI 2.0 hızlı şekilde toodo bu görevleri sağlar. Birkaç ortak görevler şunlardır.

### <a name="view-vms-in-a-scale-set"></a>Görünüm VM ölçek kümesindeki
tooview, Ölçek çalışan sanal makineler listesi ayarlayabilir, kullanabilir [az vmss listesi-örneklerini](/cli/azure/vmss#list-instances) gibi:

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

Merhaba, benzer toohello aşağıdaki örneğine çıktı:

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a>Artırma veya azaltma VM örnekleri
toosee hello örnek sayısı, şu anda bir ölçek kümesindeki, kullanın [az vmss Göster](/cli/azure/vmss#show) ve sorgulayın *sku.capacity*:

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

Daha sonra el ile artırabilir veya sanal makineler kümesi hello ölçeğinde hello sayısını azaltmak [az vmss ölçek](/cli/azure/vmss#scale). Merhaba aşağıdaki örnek hello sayısını VM'ler, ölçeği çok ayarla ayarlar*5*:

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

Otomatik ölçeklendirme kurallarını, ağ trafiğini veya CPU kullanımı gibi yanıt toodemand nasıl tooscale yukarı veya aşağı hello sayısında VM'ler, Ölçek kümesindeki tanımlamanıza olanak sağlar. Şu anda, bu kurallar Azure CLI 2. 0'olarak ayarlanamaz. Kullanım hello [Azure portal](https://portal.azure.com) tooconfigure otomatik ölçeklendirme.

### <a name="get-connection-info"></a>Bağlantı bilgilerini al
tooobtain bağlantı bilgilerini hakkında ölçek kümeleri VM'ler Merhaba, kullanın [az vmss listesi-örnek-bağlantı-bilgisi](/cli/azure/vmss#list-instance-connection-info). Bu komut, SSH ile tooconnect sağlayan her bir VM için hello ortak IP adresi ve bağlantı noktası çıkarır:

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a>Veri diskleri ölçek kümeleri ile kullanma
Oluşturun ve veri diskleri ölçek kümeleri ile kullanın. Önceki bir öğreticide, nasıl çok öğrenilen[yönetmek Azure diskleri](tutorial-manage-disks.md) anahatları en iyi yöntemler ve veri diskleri hello işletim sistemi disk yerine uygulamaları oluşturmak için performans iyileştirmeleri hello.

### <a name="create-scale-set-with-data-disks"></a>Veri diskleri ile ölçek kümesi oluşturma
bir ölçek ayarlamak ve veri diskleri ekleme toocreate eklemek hello `--data-disk-sizes-gb` parametresi toohello [az vmss oluşturma](/cli/azure/vmss#create) komutu. Merhaba aşağıdaki örnekte oluşturur kümesiyle bir ölçek *50*Gb veri diskleri ekli tooeach örneği:

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
bir veri diski tooinstances, Ölçek tooadd ayarlayabilir, kullanabilir [az vmss diskini](/cli/azure/vmss/disk#attach). Merhaba aşağıdaki örnek, bir *50*Gb disk tooeach örneği:

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a>Veri diskleri ayırma
bir veri diski tooinstances, Ölçek tooremove ayarlayabilir, kullanabilir [az vmss disk ayırma](/cli/azure/vmss/disk#detach). Merhaba aşağıdaki örnek kaldırır hello veri diski LUN değerine *2* her örneğinden:

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, bir sanal makine ölçek kümesi oluşturuldu. Şunları öğrendiniz:

> [!div class="checklist"]
> * Bulut init toocreate bir uygulama tooscale kullanın
> * Bir sanal makine ölçek kümesi oluşturma
> * Artırma veya azaltma hello ölçek kümesi örneği sayısı
> * Ölçek kümesi örnekleri için bağlantı bilgileri görüntüle
> * Veri diskleri bir ölçek kümesinde kullanın

Toohello sonraki öğretici toolearn Yük Dengeleme sanal makineler için kavramları hakkında daha fazla ilerleyin.

> [!div class="nextstepaction"]
> [Sanal makinelerin yük dengelemesini](tutorial-load-balancer.md)