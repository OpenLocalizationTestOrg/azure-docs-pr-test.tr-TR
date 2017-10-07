---
title: "ilk önyükleme azure'da bir Linux VM aaaCustomize | Microsoft Docs"
description: "Nasıl toouse bulut başlatma ve anahtar kasası toocustomze Linux VM'ler hello ilk kez bunlar Azure'da önyükleme öğrenin"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 280189723ac0205226f9c0068bd605da13249ace
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a>Nasıl toocustomize Linux sanal bir makinede ilk önyükleme
Önceki bir öğreticide, nasıl öğrenilen tooSSH tooa sanal makine (VM) ve NGINX el ile yükleyin. hızlı ve tutarlı bir şekilde, tür Otomasyon toocreate VM'ler genellikle istenen. Ortak bir yaklaşım toocustomize ilk önyüklemede VM toouse olan [bulut init](https://cloudinit.readthedocs.io). Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:

> [!div class="checklist"]
> * Bir bulut init yapılandırma dosyası oluşturma
> * Bir bulut init dosyası kullanan bir VM oluşturma
> * Merhaba VM oluşturulduktan sonra çalışan bir Node.js uygulaması görüntüleyin
> * Anahtar kasası toosecurely deposu sertifikaları kullanma
> * Güvenli NGINX dağıtımlarında bulut init otomatikleştirme


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).  



## <a name="cloud-init-overview"></a>Bulut init genel bakış
[Bulut init](https://cloudinit.readthedocs.io) yaygın olarak kullanılan bir yaklaşım toocustomize hello için ilk kez önyükleme bir Linux VM aynıdır. Bulut init tooinstall paketleri ve dosyaları veya tooconfigure kullanıcılar ve güvenlik yazma kullanabilirsiniz. Bulut init hello ilk önyükleme işlemi sırasında çalışırken, hiçbir ek adımlar vardır veya aracıları tooapply yapılandırmanız gerekiyor.

Bulut init dağıtımları üzerinde de çalışır. Örneğin, kullanmadığınız **get apt yükleme** veya **yum yükleme** tooinstall bir paket. Bunun yerine, paketleri tooinstall listesi tanımlayabilirsiniz. Bulut init hello Yerel Paket yönetim aracı için seçtiğiniz hello distro otomatik olarak kullanır.

Bizim ortakları tooget bulut dahil başlatma çalışmak ve çalışma tooAzure sağladıkları hello görüntülerinde duyuyoruz. Aşağıdaki tablonun hello hello geçerli bulut init kullanılabilirlik Azure platform görüntüleri özetlenmektedir:

| Diğer ad | Yayımcı | Sunduğu | SKU | Sürüm |
|:--- |:--- |:--- |:--- |:--- |:--- |
| UbuntuLTS |Canonical |UbuntuServer |16.04 LTS |en son |
| UbuntuLTS |Canonical |UbuntuServer |14.04.5-LTS |en son |
| CoreOS |CoreOS |CoreOS |Dengeli |en son |


## <a name="create-cloud-init-config-file"></a>Bulut init yapılandırma dosyası oluşturma
Eylem toosee bulut başlatma NGINX yükler ve basit bir 'Hello World' Node.js uygulaması çalıştıran bir VM oluşturun. Bulut init yapılandırma aşağıdaki hello hello gerekli paketleri yükler, bir Node.js uygulaması oluşturur sonra başlatmak ve hello uygulama başlatır.

Geçerli kabuğunuzu adlı bir dosya oluşturun *bulut init.txt* Yapıştır hello izleyerek yapılandırma. Örneğin, yerel makinenizde değil hello bulut Kabuk hello dosya oluşturun. İstediğiniz herhangi bir düzenleyicisini kullanabilirsiniz. Girin `sensible-editor cloud-init.txt` toocreate hello dosya ve kullanılabilir düzenleyicileri listesini görebilirsiniz. Merhaba tüm bulut init dosyanın doğru şekilde kopyalandığından emin olun, özellikle ilk satırı hello:

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

Bulut init yapılandırma seçenekleri hakkında daha fazla bilgi için bkz: [bulut init yapılandırma örnekleri](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).

## <a name="create-virtual-machine"></a>Sanal makine oluşturma
Bir VM oluşturmadan önce bir kaynak grubuyla oluşturmanız [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupAutomate* hello içinde *eastus* konumu:

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

Şimdi bir VM oluşturmak [az vm oluşturma](/cli/azure/vm#create). Kullanım hello `--custom-data` parametresi toopass bulut init yapılandırma dosyası. Merhaba tam yolu toohello sağlamak *bulut init.txt* mevcut çalışma dizininizi dışında hello dosyasını kaydettiyseniz yapılandırma. Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myAutomatedVM*:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Oluşturulan, hello VM toobe birkaç dakika sürer hello paketleri tooinstall ve hello uygulama toostart. Hello Azure CLI toohello istemi döndükten sonra toorun devam arka plan görevleri vardır. Başka bir birkaç hello uygulamaya erişmek için dakika olabilir. Merhaba VM oluşturduğunuzda hello not edin `publicIpAddress` hello Azure CLI tarafından görüntülenir. Kullanılan tooaccess hello Node.js uygulaması bir web tarayıcısı aracılığıyla adresidir.

açık bağlantı noktası 80 hello Internet gelen ile VM'nizi tooallow web trafiği tooreach [az vm Aç-port](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a>Test web uygulaması
Bir web tarayıcısı açın ve girin artık *http://<publicIpAddress>*  hello adres çubuğundaki. Kendi ortak sağlamak hello VM IP adresinden oluşturma işlemi. Node.js uygulamanızı aşağıdaki örneğine hello olduğu gibi görüntülenir:

![Çalışan NGINX sitesini görüntüle](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a>Anahtar kasası sertifikaları Ekle
Bu isteğe bağlı bir bölüm nasıl güvenli bir şekilde Azure anahtar kasası sertifikaları depolamak ve hello VM dağıtımı sırasında Ekle gösterir. Merhaba sertifikaları içeren özel bir görüntü kullanarak yerine desteklenmiş, bu işlem hello en güncel sertifikaları tooa VM ilk önyüklemede eklenmiş sağlar. Merhaba işlemi sırasında hiçbir zaman hello sertifika hello Azure platformu bırakır veya bir komut dosyası, komut satırı geçmiş veya şablonda sunulur.

Azure anahtar kasası, şifreleme anahtarlarını ve gizli anahtarları, sertifikalar veya parolaları gibi koruma sağlar. Anahtar kasası hello anahtar yönetimi işlemini kolaylaştırmaya yardımcı olur ve erişmek ve veri şifreleme anahtarları toomaintain denetimini etkinleştirir. Bu senaryo bazı anahtar kasası kavramları toocreate ve bir sertifika kullan sunar, ancak konusunda kapsamlı bir genel bakış değil toouse anahtar kasası.

Aşağıdaki adımları hello nasıl göster:

- Azure anahtar kasası oluşturma
- Oluşturmak veya bir sertifika toohello anahtar kasası karşıya yükle
- Merhaba sertifika tooinject tooa VM içinde bir gizli anahtar oluşturma
- Bir VM oluşturun ve hello sertifika Ekle

### <a name="create-an-azure-key-vault"></a>Azure anahtar kasası oluşturma
İlk olarak, bir anahtar kasası ile oluşturma [az keyvault oluşturma](/cli/azure/keyvault#create) ve bir VM dağıttığınızda kullanım için etkinleştirin. Her anahtar kasası benzersiz bir ad gerektirir ve tüm küçük olmalıdır. Değiştir *mykeyvault* kendi benzersiz bir anahtar kasası ad örnekle aşağıdaki hello içinde:

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a>Sertifika oluşturmak ve anahtar kasasına depolamak
Üretim kullanımı için güvenilen bir sağlayıcı tarafından imzalanmış geçerli bir sertifika almanız gerekir [az keyvault sertifika alma](/cli/azure/keyvault/certificate#import). Bu öğretici için hello aşağıdaki örnek otomatik olarak imzalanan bir sertifika ile nasıl oluşturabileceğiniz gösterir [az keyvault sertifika oluştur](/cli/azure/keyvault/certificate#create) hello varsayılan sertifika ilkesi kullanır:

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a>VM ile kullanmak için sertifika hazırlama
toouse hello sertifika hello VM sırasında işlem oluşturma, sertifikanızla hello kimliği elde [az keyvault gizli listesi sürümleri](/cli/azure/keyvault/secret#list-versions). Merhaba VM hello sertifika gereken belirli bir biçim tooinject önyüklemede, bu nedenle dönüştürmeden hello sertifikayla [az vm biçimi-gizli](/cli/azure/vm#format-secret). Aşağıdaki örnek hello hello kullanım kolaylığı için bu komutları toovariables hello çıktısını sonraki adımlar atar:

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a>Bulut init config toosecure NGINX oluşturma
VM, sertifikaları oluşturduğunuzda ve anahtarlar, korumalı hello depolanır */var/lib/waagent/* dizin. tooautomate ekleme hello sertifika toohello VM ve NGINX yapılandırma, güncelleştirilmiş bulut init config hello önceki örnekteki kullanabilirsiniz.

Adlı bir dosya oluşturun *bulut init secured.txt* Yapıştır hello izleyerek yapılandırma. Yeniden hello bulut Kabuğu'nu kullanırsanız, hello bulut init yapılandırma dosyası yok ve yerel makinenizde değil oluşturun. Kullanım `sensible-editor cloud-init-secured.txt` toocreate hello dosya ve kullanılabilir düzenleyicileri listesini görebilirsiniz. Merhaba tüm bulut init dosyanın doğru şekilde kopyalandığından emin olun, özellikle ilk satırı hello:

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
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
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
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-secure-vm"></a>Güvenli VM oluşturma
Şimdi bir VM oluşturmak [az vm oluşturma](/cli/azure/vm#create). Merhaba sertifika verileri ile Merhaba anahtar Kasası'nı eklenen `--secrets` parametresi. Merhaba önceki örnekte olduğu gibi aynı zamanda hello bulut init config hello ile geçirdiğiniz `--custom-data` parametre:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-secured.txt \
    --secrets "$vm_secret"
```

Oluşturulan, hello VM toobe birkaç dakika sürer hello paketleri tooinstall ve hello uygulama toostart. Hello Azure CLI toohello istemi döndükten sonra toorun devam arka plan görevleri vardır. Başka bir birkaç hello uygulamaya erişmek için dakika olabilir. Merhaba VM oluşturduğunuzda hello not edin `publicIpAddress` hello Azure CLI tarafından görüntülenir. Kullanılan tooaccess hello Node.js uygulaması bir web tarayıcısı aracılığıyla adresidir.

açık bağlantı noktası 443 hello Internet gelen ile VM'nizi tooallow güvenli web trafiği tooreach [az vm Aç-port](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a>Test güvenli web uygulaması
Bir web tarayıcısı açın ve girin artık *https://<publicIpAddress>*  hello adres çubuğundaki. Kendi ortak sağlamak hello VM IP adresinden oluşturma işlemi. Kendinden imzalı bir sertifika kullanılması durumunda hello güvenlik uyarısı kabul edin:

![Web tarayıcısı güvenlik uyarısını kabul edin](./media/tutorial-automate-vm-deployment/browser-warning.png)

Güvenli NGINX siteniz ve Node.js uygulaması ardından aşağıdaki örneğine hello olduğu gibi görüntülenir:

![Çalışan güvenli NGINX sitesini görüntüle](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, VM'ler ilk önyüklemesi bulut init ile yapılandırılır. Şunları öğrendiniz:

> [!div class="checklist"]
> * Bir bulut init yapılandırma dosyası oluşturma
> * Bir bulut init dosyası kullanan bir VM oluşturma
> * Merhaba VM oluşturulduktan sonra çalışan bir Node.js uygulaması görüntüleyin
> * Anahtar kasası toosecurely deposu sertifikaları kullanma
> * Güvenli NGINX dağıtımlarında bulut init otomatikleştirme

Toohello sonraki öğretici toolearn nasıl ilerlemek toocreate özel VM görüntüler.

> [!div class="nextstepaction"]
> [Özel VM görüntüleri oluşturma](./tutorial-custom-images.md)
