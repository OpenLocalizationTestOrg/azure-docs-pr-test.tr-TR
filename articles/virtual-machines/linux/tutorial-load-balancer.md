---
title: aaaHow tooload dengelemek Linux sanal makineleri azure'da | Microsoft Docs
description: "Nasıl toouse hello Azure yük dengeleyici toocreate yüksek oranda kullanılabilir ve güvenli bir uygulama üç Linux VM'ler arasında bilgi edinin"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>Nasıl tooload Bakiye Azure toocreate Linux sanal makineleri yüksek oranda kullanılabilir bir uygulama
Yük Dengeleme, birden çok sanal makine genelinde gelen istekleri yayarak daha yüksek düzeyde kullanılabilirlik sağlar. Bu öğreticide, trafiği dağıtmak ve yüksek kullanılabilirlik sağlamak hello farklı bileşenler hello Azure yük dengeleyici hakkında bilgi edinin. Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:

> [!div class="checklist"]
> * Bir Azure yük dengeleyici oluşturma
> * Bir yük dengeleyici durum araştırması oluştur
> * Yük Dengeleyici trafiği kuralları oluşturma
> * Bulut init toocreate temel bir Node.js uygulama kullanın
> * Sanal makineler oluşturmak ve tooa yük dengeleyici ekleme
> * Bir yük dengeleyici eylemde görüntüleyin
> * Ekleme ve sanal makineleri yük dengeleyiciden kaldırın


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="azure-load-balancer-overview"></a>Azure yük dengeleyici genel bakış
Bir Azure yük dengeleyici gelen trafiği sağlıklı VM'ler arasında dağıtarak yüksek kullanılabilirlik sağlayan bir katman 4 (TCP, UDP) yük dengeleyicidir. Bir yük dengeleyici durum araştırması her VM üzerinde belirli bir bağlantı noktasını izler ve yalnızca trafik tooan dağıtır işletimsel VM.

Bir veya daha fazla ortak IP adreslerini içeren bir ön uç IP yapılandırmasını tanımlayın. Bu ön uç IP yapılandırmasını yük dengeleyici ve uygulamaları toobe hello Internet erişilebilir sağlar. 

Sanal makineler tooa yük dengeleyici, sanal ağ arabirim kartı (NIC) kullanarak bağlanın. toodistribute trafiği toohello VM'ler, bir arka uç adres havuzu hello sanal (NIC) bağlı toohello yük dengeleyici hello IP adreslerini içerir.

toocontrol hello akış trafiği belirli bağlantı noktalarını ve tooyour VM'ler eşleme protokolleri için yük dengeleyici kuralları tanımlayın.

Merhaba önceki öğretici çok izlediyseniz[bir sanal makine ölçek kümesi oluşturma](tutorial-create-vmss.md), bir yük dengeleyici sizin için oluşturuldu. Tüm bu bileşenlerin, hello ölçek kümesinin bir parçası olarak yapılandırıldı.


## <a name="create-azure-load-balancer"></a>Azure yük dengeleyici oluşturma
Bu bölümde, nasıl oluşturma ve her bileşenin hello yük dengeleyicinin yapılandırma ayrıntıları. Yük Dengeleyici oluşturmadan önce bir kaynak grubuyla oluşturmanız [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupLoadBalancer* hello içinde *eastus* konumu:

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a>Genel IP adresi oluşturma
tooaccess uygulamanıza Internet Merhaba, hello yük dengeleyici için bir ortak IP adresi gerekir. Bir ortak IP adresiyle oluşturma [az ağ genel IP oluşturun](/cli/azure/network/public-ip#create). Merhaba aşağıdaki örnekte oluşturur adlı ortak IP adresi *myPublicIP* hello içinde *myResourceGroupLoadBalancer* kaynak grubu:

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a>Yük dengeleyici oluşturma
Bir yük dengeleyici ile oluşturma [az ağ lb oluşturma](/cli/azure/network/lb#create). Merhaba aşağıdaki örnek adlı bir yük dengeleyici oluşturur *myLoadBalancer* ve atar hello *myPublicIP* adresi toohello ön uç IP yapılandırması:

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a>Bir sistem durumu araştırması oluştur
tooallow hello yük dengeleyici toomonitor hello durumu, uygulamanızın bir sistem durumu araştırması kullanın. Merhaba durumu araştırması dinamik olarak ekler veya kendi yanıt toohealth denetimleri temel hello yük dengeleyici döndürme VM'ler kaldırır. Varsayılan olarak, bir VM hello yük dengeleyici dağıtımı 15 saniyelik aralıklarda iki ardışık hatadan sonra kaldırılır. Bir protokol veya belirli bir sistem onay sayfasında uygulamanız için temel bir sistem durumu araştırması oluşturun. 

Aşağıdaki örnek hello bir TCP araştırması oluşturur. Daha fazla hassas sistem durumu denetimlerinin özel HTTP araştırmalara de oluşturabilirsiniz. Özel bir HTTP araştırma kullanırken, hello sistem durumu onay sayfasında, aşağıdaki gibi oluşturmalısınız *healthcheck.js*. Merhaba araştırma döndürmelidir bir **HTTP 200 Tamam** hello yük dengeleyici tookeep hello ana döndürme yanıtı.

toocreate TCP durumu araştırması, kullandığınız [az ağ lb araştırma oluşturmak](/cli/azure/network/lb/probe#create). Merhaba aşağıdaki örnek adlı bir sistem durumu araştırması oluşturur *myHealthProbe*:

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a>Yük Dengeleyici kuralı oluşturma
Yük Dengeleyici kuralı kullanılan toodefine olduğu dağıtılmış toohello VM'ler nasıl trafiğidir. Merhaba ön uç IP yapılandırmasını hello gelen trafiği ve hello arka uç IP havuzu tooreceive hello trafiği için hello gerekli kaynak ve hedef bağlantı noktası ile birlikte tanımlayın. toomake trafiği yalnızca sağlıklı VM'ler aldığınızdan emin, aynı zamanda hello sistem durumu araştırma toouse tanımlar.

Yük Dengeleyici kuralı ile oluşturma [az ağ lb kuralını](/cli/azure/network/lb/rule#create). Merhaba aşağıdaki örnek adlı bir kural oluşturur *myLoadBalancerRule*, kullandığı hello *myHealthProbe* durum araştırması ve bağlantı noktası bakiyelerini trafiğine *80*:

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a>Sanal ağ yapılandırma
Bazı sanal makineleri dağıtmak ve, dengeleyici sınayabilirsiniz önce sanal ağ kaynaklarına destekleme hello oluşturun. Sanal ağlar hakkında daha fazla bilgi için bkz: Merhaba [Azure Sanal Ağları Yönet](tutorial-virtual-network.md) Öğreticisi.

### <a name="create-network-resources"></a>Ağ kaynakları oluşturun
Bir sanal ağ ile oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create). Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* adlı bir alt ağ ile *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

tooadd bir ağ güvenlik grubu, kullandığınız [az ağ nsg oluşturma](/cli/azure/network/nsg#create). Merhaba aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur *myNetworkSecurityGroup*:

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

Ağ güvenlik grubu kural oluştururken [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create). Merhaba aşağıdaki örnekte oluşturur adlı bir ağ güvenlik grubu kural *myNetworkSecurityGroupRule*:

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

Sanal NIC ile oluşturulan [az ağ NIC oluşturma](/cli/azure/network/nic#create). Merhaba aşağıdaki örnek üç sanal NIC oluşturur. (Bir sanal NIC aşağıdaki hello uygulamanızda adımları için oluşturduğunuz her VM için). Ek sanal NIC ve sanal makineleri herhangi bir zamanda oluşturmak ve bunları toohello yük dengeleyici Ekle:

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a>Sanal makineler oluşturma

### <a name="create-cloud-init-config"></a>Bulut init yapılandırma oluşturma
Önceki bir öğretici içinde [nasıl toocustomize Linux sanal bir makinede ilk önyükleme](tutorial-automate-vm-deployment.md), size nasıl öğrenilen tooautomate VM özelleştirme bulut init ile. Kullanabileceğiniz aynı bulut init yapılandırma dosyası tooinstall NGINX hello ve basit bir 'Hello World' Node.js uygulaması çalıştırın.

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

### <a name="create-virtual-machines"></a>Sanal makineler oluşturma
tooimprove hello yüksek kullanılabilirlik, uygulamanızın bir kullanılabilirlik kümesine Vm'leriniz yerleştirin. Kullanılabilirlik kümeleri hakkında daha fazla bilgi için bkz: hello önceki [nasıl toocreate yüksek oranda kullanılabilir sanal makineleri](tutorial-availability-sets.md) Öğreticisi.

Kullanılabilirlik kümesi oluştur [az vm kullanılabilirlik kümesi oluşturma](/cli/azure/vm/availability-set#create). Merhaba aşağıdaki örnekte oluşturur kullanılabilirlik adlandırılmış kümesi *myAvailabilitySet*:

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

Merhaba VM'ler ile oluşturduğunuz artık [az vm oluşturma](/cli/azure/vm#create). Merhaba aşağıdaki örnek üç VM'ler oluşturur ve zaten mevcut değilse SSH anahtarları üretir:

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

Hello Azure CLI toohello istemi döndükten sonra toorun devam arka plan görevleri vardır. Merhaba `--no-wait` parametre değil tüm görevleri toocomplete hello için bekleyin. Başka bir birkaç hello uygulamaya erişmek için dakika olabilir. Merhaba uygulamayı her VM çalıştıran hello yük dengeleyici durum araştırması otomatik olarak algılar. Merhaba uygulama çalışmaya başladıktan sonra hello yük dengeleyici kuralı toodistribute trafiği başlatır.


## <a name="test-load-balancer"></a>Test yük dengeleyici
Merhaba, yük dengeleyici ile genel IP adresi elde [az ağ ortak IP Göster](/cli/azure/network/public-ip#show). Merhaba aşağıdaki örnek alacağı için başlangıç IP adresi *myPublicIP* daha önce oluşturduğunuz:

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

Ardından tooa web tarayıcısında hello genel IP adresi girebilirsiniz. Unutmayın - hello yük dengeleyici toodistribute trafiği toothem başlamadan önce birkaç dakika hello hello VM'ler toobe hazır alır. Merhaba uygulama gösterilir, hello VM hello hostname dahil olmak üzere bu hello yük dengeleyici trafiği tooas aşağıdaki örneğine hello içinde dağıtılmış:

![Çalışan Node.js uygulaması](./media/tutorial-load-balancer/running-nodejs-app.png)

toosee hello yük dengeleyici, uygulamanızı çalıştıran tüm üç VM'ler arasında trafiği dağıtmak, zorla web tarayıcınızı yenileme.


## <a name="add-and-remove-vms"></a>Sanal makineleri ekleyip
Merhaba işletim sistemi güncelleştirmelerini yükleme gibi uygulamanızı çalıştıran VM'ler tooperform bakım gerekebilir. toodeal trafiğinin artmasına tooyour uygulamayla ihtiyacınız olabilecek tooadd ilave VM'ler. Bu bölümde, nasıl gösterilir tooremove veya VM hello yük dengeleyiciden ekleyin.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Bir VM hello yük dengeleyiciden kaldırın
Merhaba arka uç adres havuzu ile bir VM kaldırabilirsiniz [az ağ NIC IP-config adres havuzu kaldırmak](/cli/azure/network/nic/ip-config/address-pool#remove). Aşağıdaki örnek kaldırır hello hello sanal bir NIC'ye **myVM2** gelen *myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

toosee hello yük dengeleyici iki kalan hello arasında trafiği dağıtmak uygulamanızı çalıştıran VM'ler, zorla web tarayıcınızı yenileme. Merhaba işletim sistemi güncelleştirmeleri yükleme veya VM yeniden başlatma gerçekleştirme gibi VM üzerinde bakım artık gerçekleştirebilirsiniz.

### <a name="add-a-vm-toohello-load-balancer"></a>Bir VM toohello yük dengeleyici ekleme
VM bakım gerçekleştirdikten sonra veya tooexpand kapasitesine ihtiyacınız varsa, bir VM toohello arka uç adres havuzuyla ekleyebilirsiniz [az ağ NIC IP-config adres havuzu ekleme](/cli/azure/network/nic/ip-config/address-pool#add). Merhaba aşağıdaki örnek, hello sanal bir NIC'ye **myVM2** çok*myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, bir yük dengeleyici oluşturulur ve sanal makineleri tooit bağlı. Şunları öğrendiniz:

> [!div class="checklist"]
> * Bir Azure yük dengeleyici oluşturma
> * Bir yük dengeleyici durum araştırması oluştur
> * Yük Dengeleyici trafiği kuralları oluşturma
> * Bulut init toocreate temel bir Node.js uygulama kullanın
> * Sanal makineler oluşturmak ve tooa yük dengeleyici ekleme
> * Bir yük dengeleyici eylemde görüntüleyin
> * Ekleme ve sanal makineleri yük dengeleyiciden kaldırın

Toohello sonraki öğretici toolearn Azure sanal ağı bileşenleri hakkında daha fazla ilerleyin.

> [!div class="nextstepaction"]
> [VM’leri ve sanal ağları yönetme](tutorial-virtual-network.md)
