---
title: "aaaDifferent yolları toocreate azure'da bir Linux VM | Microsoft Azure"
description: "Merhaba farklı şekillerde toocreate bağlantılar tootools ve her bir yöntemin öğreticiler dahil Microsoft Azure Linux sanal makinede öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a>Farklı şekillerde toocreate bir Linux VM
Bir Linux araçları ve iş akışları rahat tooyou kullanarak sanal makine (VM) içinde Azure toocreate hello esneklik sahip. Bu makalede, bu farklar ve hello Azure CLI 2.0 dahil olmak üzere, Linux sanal makineleri oluşturmak için örnekler özetlenmektedir. Merhaba dahil olmak üzere oluşturma seçeneği de görüntüleyebilirsiniz [Azure CLI 1.0](creation-choices-nodejs.md).

Merhaba [Azure CLI 2.0](/cli/azure/install-az-cli2) bir npm paket, sağlanan distro paketleri ya da Docker kapsayıcısı platformlarda kullanılabilir. Ortamınız için en uygun yapı Hello yükleyin ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login)

* [Azure CLI 2.0 hello ile bir Linux VM oluşturma](quick-create-cli.md)
  
  * [az group create](/cli/azure/group#create) ile *myResourceGroup* adlı bir kaynak grubu oluşturun: 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * Bir VM ile oluşturma [az vm oluşturma](/cli/azure/vm#create) adlı *myVM* kullanarak hello son *UbuntuLTS* görüntü ve bunlar zaten içinde yoksa, SSH anahtarları oluştur *~/.ssh*:

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [Azure şablonu ile Linux VM oluşturma](create-ssh-secured-vm-from-template.md)
  
  * Merhaba aşağıdaki örnek kullanır [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create) toocreate GitHub üzerinde depolanan bir şablondan VM:
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [Linux VM oluşturma ve cloud-init ile özelleştirme](tutorial-automate-vm-deployment.md)

* [Birden fazla Linux VM üzerinde yük dengeli ve yüksek oranda kullanılabilir bir uygulama oluşturma](tutorial-load-balancer.md)


## <a name="azure-portal"></a>Azure portalına
Merhaba [Azure portal](https://portal.azure.com) sağlar tooquickly olduğundan hiçbir şey bir VM oluşturun, sisteminizdeki tooinstall. Hello Azure portal toocreate hello VM kullanın:

* [Hello Azure portal kullanarak bir Linux VM oluşturma](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a>İşletim sistemi ve görüntü seçimi
Bir VM oluştururken, işletim sistemi toorun istediğiniz hello üzerinde dayanan bir görüntü seçin. Azure ve ortakları, bazıları önyüklü uygulamalar ve araçlarla gelen çok sayıda görüntü sağlar. Veya, kendi görüntülerinizden birini karşıya yükleyin (bkz [hello bölümde](#use-your-own-image)).

### <a name="azure-images"></a>Azure görüntüleri
Kullanım hello [az vm görüntüsü](/cli/azure/vm/image) toosee komutları, yayımcı, distro yayın ve derlemeleri tarafından kullanılabilir.

Kullanılabilir yayımcıların listesi:

```azurecli
az vm image list-publishers --location eastus
```

Belirli bir yayımcının kullanılabilir ürünlerinin (teklifler) listesi:

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

Belirli bir teklif için kullanılabilir SKU’ların (distro sürümleri) listesi:

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

Belirli bir sürüm için kullanılabilir tüm görüntülerin listesi:

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

Gezinme ve geçerli görüntüleri kullanma hakkında daha fazla örnek için bkz: [erişin ve seçin hello Azure CLI ile Azure sanal makine görüntüleri](cli-ps-findimage.md).

Merhaba [az vm oluşturma](/cli/azure/vm#create) komutu sahip tooquickly erişim kullanabileceğiniz diğer adlar daha yaygın distro'lar ve bunların en son sürümleri hello. Diğer adlar genellikle hello publisher, teklif, SKU ve sürümü her zaman bir VM oluşturma belirtmekten daha hızlı kullanmaktır:

| Diğer ad | Yayımcı | Sunduğu | SKU | Sürüm |
|:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7.2 |en son |
| CoreOS |CoreOS |CoreOS |Dengeli |en son |
| Debian |credativ |Debian |8 |en son |
| openSUSE |SUSE |openSUSE |13.2 |en son |
| RHEL |RedHat |RHEL |7.2 |en son |
| SLES |SLES |SLES |12 SP1 |en son |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |en son |

### <a name="use-your-own-image"></a>Kendi görüntünüzü kullanma
Belirli özelleştirmelere ihtiyaç duyuyorsanız, mevcut bir Azure VM’yi yakalayarak bu VM’yi temel alan bir görüntü kullanabilirsiniz. Şirket içinde oluşturduğunuz bir görüntüyü de yükleyebilirsiniz. Desteklenen distro'lar hakkında daha fazla bilgi ve nasıl toouse kendi görüntüleri görmek hello makaleler:

* [Azure destekli dağıtımlar](endorsed-distros.md)
* [Desteklenmeyen dağıtımlarla ilgili bilgiler](create-upload-generic.md)
* [Nasıl toocreate mevcut bir Azure VM'i görüntüden](tutorial-custom-images.md).
  
  * Hızlı Başlangıç örnek toocreate mevcut bir Azure VM'i görüntüden komutlar:
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba ile bir Linux VM oluşturma [CLI](quick-create-cli.md), hello gelen [portal](quick-create-portal.md), veya kullanarak bir [Azure Resource Manager şablonu](../windows/cli-deploy-templates.md).
* Linux VM oluşturduktan sonra [Azure diskleri ve depolama hakkında bilgi edinin](tutorial-manage-disks.md).
* Hızlı adımlar çok[bir parola veya SSH anahtarlarını sıfırlama ve kullanıcıları yönetme](using-vmaccess-extension.md).
