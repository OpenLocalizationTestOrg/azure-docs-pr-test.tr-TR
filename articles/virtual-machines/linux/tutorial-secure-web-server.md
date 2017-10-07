---
title: "SSL ile bir web sunucusu sertifikaları Azure'da aaaSecure | Microsoft Docs"
description: "Azure'da bir Linux VM üzerinde nasıl toosecure hello NGINX web sunucusu ile SSL sertifikaları öğrenin"
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
ms.date: 07/17/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d3a62d77ac05c9aa2a44356b7c8e44cb485b81aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a>Bir web sunucusu ile SSL sertifikalarını azure'da bir Linux sanal makinede güvenli
toosecure web sunucuları, bir Güvenli Yuva daha sonra (SSL) sertifikası olabilir tooencrypt web trafiği kullanılır. Bu SSL sertifikalarını Azure anahtar kasası depolanabilir ve Azure'da sertifikaları tooLinux sanal makineleri (VM'ler) güvenli dağıtımlar sağlar. Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:

> [!div class="checklist"]
> * Azure anahtar kasası oluşturma
> * Oluşturmak veya bir sertifika toohello anahtar kasası karşıya yükle
> * Bir VM oluşturun ve hello NGINX web sunucusu yükleme
> * VM hello Hello sertifika Ekle ve NGINX bir SSL bağlaması ile yapılandırma

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).  


## <a name="overview"></a>Genel Bakış
Azure anahtar kasası, şifreleme anahtarlarını ve gizli anahtarları, bu tür sertifikalar veya parolaları koruma sağlar. Anahtar kasası hello sertifika yönetimi işlemini kolaylaştırmaya yardımcı olur ve bu sertifikaları erişim anahtarlarını toomaintain denetim sağlar. Anahtar kasası içinde otomatik olarak imzalanan bir sertifika oluşturun veya zaten sahip olduğunuz bir varolan, güvenilen bir sertifika yükleyin.

Sertifikaları içeren özel bir VM görüntüsü kullanarak yerine desteklenmiş, sertifikaları çalışan VM ekleme. Bu işlem hello en güncel sertifikaları dağıtımı sırasında bir web sunucusunda yüklü olan sağlar. Yenileme veya bir sertifikayı değiştirin, yeni bir özel VM görüntüsü toocreate da yok. Ek VM'ler oluşturmak gibi hello son sertifikaları otomatik olarak eklenmiş. Hello tüm işlem sırasında hiç hello sertifikaları hello Azure platformu bırakın veya bir komut dosyası, komut satırı geçmiş veya şablonda sunulur.


## <a name="create-an-azure-key-vault"></a>Azure anahtar kasası oluşturma
Bir anahtar kasası ve sertifikaları oluşturmadan önce bir kaynak grubuyla oluşturmanız [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupSecureWeb* hello içinde *eastus* konumu:

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

Ardından, bir anahtar kasası ile oluşturma [az keyvault oluşturma](/cli/azure/keyvault#create) ve bir VM dağıttığınızda kullanım için etkinleştirin. Her anahtar kasası benzersiz bir ad gerektirir ve tüm küçük olmalıdır. Değiştir  *<mykeyvault>*  kendi benzersiz bir anahtar kasası ad örnekle aşağıdaki hello içinde:

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>Bir sertifika oluşturmak ve anahtar kasasına depolamak
Üretim kullanımı için güvenilen bir sağlayıcı tarafından imzalanmış geçerli bir sertifika almanız gerekir [az keyvault sertifika alma](/cli/azure/certificate#import). Bu öğretici için hello aşağıdaki örnek otomatik olarak imzalanan bir sertifika ile nasıl oluşturabileceğiniz gösterir [az keyvault sertifika oluştur](/cli/azure/certificate#create) hello varsayılan sertifika ilkesi kullanır:

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a>Bir VM ile kullanılmak üzere bir sertifika hazırlama
toouse hello sertifika hello VM sırasında işlem oluşturma, sertifikanızla hello kimliği elde [az keyvault gizli listesi sürümleri](/cli/azure/keyvault/secret#list-versions). Merhaba sertifikayla Dönüştür [az vm biçimi-gizli](/cli/azure/vm#format-secret). Aşağıdaki örnek hello hello kullanım kolaylığı için bu komutları toovariables hello çıktısını sonraki adımlar atar:

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a>Bir bulut init config toosecure NGINX oluşturma
[Bulut init](https://cloudinit.readthedocs.io) yaygın olarak kullanılan bir yaklaşım toocustomize hello için ilk kez önyükleme bir Linux VM aynıdır. Bulut init tooinstall paketleri ve dosyaları veya tooconfigure kullanıcılar ve güvenlik yazma kullanabilirsiniz. Bulut init hello ilk önyükleme işlemi sırasında çalışırken, hiçbir ek adımlar vardır veya aracıları tooapply yapılandırmanız gerekiyor.

VM, sertifikaları oluşturduğunuzda ve anahtarlar, korumalı hello depolanır */var/lib/waagent/* dizin. tooautomate sertifika toohello VM hello ekleyip hello web sunucusunu yapılandırma bulut init kullanın. Bu örnekte, yükleyin ve hello NGINX web sunucusunu yapılandırın. Merhaba kullanabilirsiniz aynı işlem tooinstall ve Apache yapılandırın. 

Adlı bir dosya oluşturun *bulut-init-web-server.txt* Yapıştır hello izleyerek yapılandırma:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
      }
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
```

### <a name="create-a-secure-vm"></a>Güvenli bir VM oluşturma
Şimdi bir VM oluşturmak [az vm oluşturma](/cli/azure/vm#create). Merhaba sertifika verileri ile Merhaba anahtar Kasası'nı eklenen `--secrets` parametresi. Merhaba bulut init config hello ile geçirin `--custom-data` parametre:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-web-server.txt \
    --secrets "$vm_secret"
```

Oluşturulan, hello VM toobe birkaç dakika sürer hello paketleri tooinstall ve hello uygulama toostart. Merhaba VM oluşturduğunuzda hello not edin `publicIpAddress` hello Azure CLI tarafından görüntülenir. Bu adres kullanılan tooaccess bir web tarayıcısında, sitedir.

açık bağlantı noktası 443 hello Internet gelen ile VM'nizi tooallow güvenli web trafiği tooreach [az vm Aç-port](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a>Test hello güvenli web uygulaması
Bir web tarayıcısı açın ve girin artık *https://<publicIpAddress>*  hello adres çubuğundaki. Kendi ortak sağlamak hello VM IP adresinden oluşturma işlemi. Kendinden imzalı bir sertifika kullanılması durumunda hello güvenlik uyarısı kabul edin:

![Web tarayıcısı güvenlik uyarısını kabul edin](./media/tutorial-secure-web-server/browser-warning.png)

Güvenli NGINX sitenizi sonra aşağıdaki örneğine hello olduğu gibi görüntülenir:

![Çalışan güvenli NGINX sitesini görüntüle](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, Azure anahtar kasasında depolanan bir SSL sertifikası ile bir NGINX web sunucusu güvenli. Şunları öğrendiniz:

> [!div class="checklist"]
> * Azure anahtar kasası oluşturma
> * Oluşturmak veya bir sertifika toohello anahtar kasası karşıya yükle
> * Bir VM oluşturun ve hello NGINX web sunucusu yükleme
> * VM hello Hello sertifika Ekle ve NGINX bir SSL bağlaması ile yapılandırma

Sanal makine kod örnekleri önceden oluşturulmuş Bu bağlantı toosee izleyin.

> [!div class="nextstepaction"]
> [Windows sanal makine kod örnekleri](./cli-samples.md)