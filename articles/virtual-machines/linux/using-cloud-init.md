---
title: aaaUse bulut init toocustomize bir Linux VM | Microsoft Docs
description: "Nasıl ile oluşturma sırasında bir Linux VM toouse bulut init toocustomize hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e7297e162fc73f0da42f195bec2fcbe23b310c1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a>Bulut init toocustomize bir Linux VM oluşturma sırasında kullanın
Bu makalede nasıl toomake bulut init betik tooset hostname Merhaba, güncelleştirme yüklü paketleri ve hello Azure CLI 2.0 olan kullanıcı hesaplarını yönetme gösterilmektedir. Azure CLI üzerinden bir sanal makine (VM) oluşturduğunuzda hello bulut Init komut adı verilir. Daha ayrıntılı bir bakış uygulamaları yükleme hakkında bilgi için bkz: yapılandırma dosyaları yazma ve anahtar kasası, anahtarları injecting [Bu öğretici](tutorial-automate-vm-deployment.md). Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](using-cloud-init-nodejs.md).

## <a name="quick-commands"></a>Hızlı komutlar
Merhaba hostname ayarlar, tüm paketleri güncelleştirir ve bir sudo kullanıcı tooLinux ekleyen bir bulut init.txt komut dosyası oluşturun.

```yaml
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```

Bir kaynak grubu toolaunch içine VM'ler ile oluşturmak [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnek adlı hello kaynak grubu oluşturur *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) bulut init tooconfigure kullanarak onu hello önyükleme sırasında `--custom-data` parametresi.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a>Ayrıntılı kılavuz
Yeni bir Linux VM başlattığında, özelleştirilmiş veya gereksinimleriniz için hazır herhangi bir şeyin standart bir Linux VM aldıklarından. [Bulut init](https://cloudinit.readthedocs.org) standart yol tooinject ilk kez kaydınızı hello önyükleme yapmak, Linux VM bir komut dosyası veya yapılandırma ayarlarını aynıdır.

Azure üzerinde birkaç farklı yolu vardır toomake değişiklikleri bir Linux VM üzerine olarak dağıtılabilir veya önyüklendiğinde.

* Bulut init kullanarak komut dosyalarını yerleştirir.
* Hello Azure'nı kullanarak betikleri Ekle [VMAccess uzantısını](using-vmaccess-extension.md).
* Bulut init kullanarak bir Azure şablonu.
* Bir Azure şablonu kullanarak [CustomScriptExtention](extensions-customscript.md).

önyükleme sonra herhangi bir zamanda tooinject komut dosyaları:

* SSH toorun doğrudan komutları
* Hello Azure'nı kullanarak betikleri Ekle [VMAccess uzantısını](using-vmaccess-extension.md), imperatively veya bir Azure şablonu
* Yapılandırma yönetimi araçları Ansible, Salt, Chef, Puppet gibi ve.

> [!NOTE]
> VMAccess uzantısını yürütür hello aynı kök gibi bir komut dosyası yolu SSH kullanarak yapabilirsiniz. Ancak, hello VM uzantısı kullanılarak çeşitli özellikler senaryonuza bağlı olarak yararlı olabilecek Azure sağladığı sağlar.

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Azure VM bulut init kullanılabilirliğine hızlı Oluştur görüntü diğer adları:
| Diğer ad | Yayımcı | Sunduğu | SKU | Sürüm | Bulut başlatma |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7.2 |en son |Yok |
| CoreOS |CoreOS |CoreOS |Dengeli |en son |Evet |
| Debian |credativ |Debian |8 |en son |Yok |
| openSUSE |SUSE |openSUSE |13.2 |en son |Yok |
| RHEL |RedHat |RHEL |7.2 |en son |Yok |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |en son |Evet |

Bizim ortakları tooget bulut dahil başlatma çalışmak ve çalışma tooAzure sağladıkları hello görüntülerinde duyuyoruz.

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a>Bir bulut init betik toohello VM oluşturma hello Azure CLI ile ekleme
Azure üzerinde bir VM oluştururken, bir bulut init komut dosyası toolaunch hello Azure CLI kullanarak hello bulut init dosyasını belirtin `--custom-data` geçin.

Bir kaynak grubu toolaunch içine VM'ler ile oluşturmak [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnek adlı hello kaynak grubu oluşturur *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) bulut init tooconfigure kullanarak, önyükleme sırasında.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a>Bir bulut init betik tooset hello ana bilgisayar adını bir Linux VM oluşturma
Merhaba basit ve herhangi bir Linux VM için en önemli ayarları biri hello ana bilgisayar adı olacaktır. Biz kolayca bu bulut init ile bu komut dosyası kullanarak ayarlayabilirsiniz.  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>Adlı örnek bulut başlatma komut dosyasını `cloud_config_hostname.txt`.
```yaml
#cloud-config
hostname: myservername
```

Çok hello hostname Hello ilk başlatılırken hello VM, bu bulut başlatma komut dosyasını ayarlar*myservername*. Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) bulut init tooconfigure kullanarak, önyükleme sırasında.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Oturum açma ve hello hello ana doğrulayın yeni VM.

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a>Bir bulut init komut dosyası oluşturma
Güvenlik için Ubuntu VM tooupdate hello ilk önyüklemede istiyor. Bulut init kullanarak hello ile Merhaba Linux dağıtım kullandığınıza bağlı olarak kod izleyin yapabiliriz.

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a>Örnek bulut init betik `cloud_config_apt_upgrade.txt` hello Debian ailesi için
```yaml
#cloud-config
apt_upgrade: true
```

Linux önyüklendikten sonra tüm yüklü hello paketler aracılığıyla güncelleştirilir **get apt**. Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) bulut init tooconfigure kullanarak, önyükleme sırasında.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

Oturum açma ve tüm paketler güncelleştirilir doğrulayın.

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a>Bir kullanıcı tooLinux bulut init betik tooadd oluşturma
Yeni bir Linux VM üzerinde hello ilk görevlerden biridir tooadd kendiniz veya tooavoid kullanmak için bir kullanıcı *kök*. SSH anahtarları olan kullanılabilirlik ve güvenlik için en iyi uygulama ve toohello eklenen *~/.ssh/authorized_keys* bu bulut init komut dosyasıyla.

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a>Örnek bulut init betik `cloud_config_add_users.txt` Debian ailesi için
```yaml
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

Linux önyüklendikten sonra tüm listelenen hello oluşturulan ve eklenen toohello sudo Grup kullanıcılardır. Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) bulut init tooconfigure kullanarak, önyükleme sırasında.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

Oturum açma ve yeni oluşturulan hello kullanıcı doğrulayın.

```bash
ssh myVM
cat /etc/group
```

Çıktı

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a>Sonraki adımlar
Bulut init bir standart yol toomodify önyükleme, Linux VM'de durumundadır. Ayrıca Azure toomodify izin VM uzantıları, LinuxVM önyükleme veya çalışırken sahiptir. Örneğin, Hello VM çalışırken hello Azure VMAccessExtension tooreset SSH veya kullanıcı bilgilerini kullanabilirsiniz. Bulut başlatma ile bir yeniden başlatma tooreset hello parola gerekir.

[Sanal makine uzantıları ve özellikleri hakkında](extensions-features.md)

[Kullanıcılar, SSH ve onay yönetmek veya VMAccess uzantısını kullanarak Azure Linux VM'ler üzerinde onarım diskleri hello](using-vmaccess-extension.md)
