---
title: "Bir Linux VM özelleştirmek için bulut init kullanın | Microsoft Docs"
description: "Azure CLI 2.0 ile oluşturma sırasında bir Linux VM özelleştirmek için bulut init kullanma"
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
ms.openlocfilehash: a7a6daad34525683579e25b9591ed28f2bf29c04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation"></a>Bir Linux VM oluşturma sırasında özelleştirmek için bulut init kullanın
Bu makalede hostname ayarlamak, güncelleştirme yüklü paketleri ve Azure CLI 2.0 olan kullanıcı hesaplarını yönetmek için bir bulut init betik yapılacağını gösterir. Azure CLI üzerinden bir sanal makine (VM) oluşturduğunuzda, bulut Init komut adı verilir. Daha ayrıntılı bir bakış uygulamaları yükleme hakkında bilgi için bkz: yapılandırma dosyaları yazma ve anahtar kasası, anahtarları injecting [Bu öğretici](tutorial-automate-vm-deployment.md). Bu adımları [Azure CLI 1.0](using-cloud-init-nodejs.md) ile de gerçekleştirebilirsiniz.

## <a name="quick-commands"></a>Hızlı komutlar
Ana bilgisayar adını ayarlar, tüm paketleri güncelleştirir ve bir sudo kullanıcı için Linux ekleyen bir bulut init.txt komut dosyası oluşturun.

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

İçine VM'ler ile başlatmak için bir kaynak grubu oluşturmak [az grubu oluşturma](/cli/azure/group#create). Aşağıdaki örnek adlı kaynak grubunu oluşturur *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) ile önyükleme sırasında yapılandırmak için bulut init kullanarak `--custom-data` parametresi.

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
Yeni bir Linux VM başlattığında, özelleştirilmiş veya gereksinimleriniz için hazır herhangi bir şeyin standart bir Linux VM aldıklarından. [Bulut init](https://cloudinit.readthedocs.org) için ilk kez önyükleme gibi bir komut dosyası veya yapılandırma ayarlarını, Linux VM içine eklemesine standart bir yoludur.

Azure üzerinde olarak bir Linux VM üzerine değişiklik yapmak için birkaç farklı yolu vardır dağıtılan veya önyüklendiğinde.

* Bulut init kullanarak komut dosyalarını yerleştirir.
* Azure kullanarak komut dosyalarını Ekle [VMAccess uzantısını](using-vmaccess-extension.md).
* Bulut init kullanarak bir Azure şablonu.
* Bir Azure şablonu kullanarak [CustomScriptExtention](extensions-customscript.md).

Komut dosyaları önyükleme sonra herhangi bir zamanda eklemesine:

* SSH komutları doğrudan çalıştırmak için
* Azure kullanarak komut dosyalarını Ekle [VMAccess uzantısını](using-vmaccess-extension.md), imperatively veya bir Azure şablonu
* Yapılandırma yönetimi araçları Ansible, Salt, Chef, Puppet gibi ve.

> [!NOTE]
> Kök SSH kullanarak aynı şekilde gibi bir komut dosyası VMAccess uzantısını yürütür. Ancak, VM uzantısını kullanarak çeşitli özellikler senaryonuza bağlı olarak yararlı olabilecek Azure sağladığı sağlar.

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Azure VM bulut init kullanılabilirliğine hızlı Oluştur görüntü diğer adları:
| Diğer ad | Yayımcı | Sunduğu | SKU | Sürüm | Bulut başlatma |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7.2 |en son |Yok |
| CoreOS |CoreOS |CoreOS |Dengeli |en son |Evet |
| Debian |credativ |Debian |8 |en son |Yok |
| openSUSE |SUSE |openSUSE |13.2 |en son |Yok |
| RHEL |RedHat |RHEL |7.2 |en son |Yok |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |en son |Evet |

Bulut dahil ve Azure'a sağladıkları görüntülerinde çalışma başlatma almak için ortaklarımızın ile çalışıyoruz.

## <a name="add-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a>Azure CLI ile VM oluşturmak için bir bulut init komut dosyası ekleme
Azure üzerinde bir VM oluştururken, bir bulut başlatma komut dosyasını başlatmak için Azure CLI kullanarak bulut init dosyasını belirtin `--custom-data` geçin.

İçine VM'ler ile başlatmak için bir kaynak grubu oluşturmak [az grubu oluşturma](/cli/azure/group#create). Aşağıdaki örnek adlı kaynak grubunu oluşturur *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) önyükleme sırasında yapılandırmak için bulut init kullanma.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a>Bir Linux VM konak adı ayarlamak için bir bulut init komut dosyası oluşturma
Tüm Linux VM için basit ve en önemli ayarlardan birini ana bilgisayar adı olacaktır. Biz kolayca bu bulut init ile bu komut dosyası kullanarak ayarlayabilirsiniz.  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>Adlı örnek bulut başlatma komut dosyasını `cloud_config_hostname.txt`.
```yaml
#cloud-config
hostname: myservername
```

VM ilk başlatma sırasında bu bulut init komut dosyası ana bilgisayar adını ayarlar *myservername*. Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) önyükleme sırasında yapılandırmak için bulut init kullanma.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Oturum açma ve ana bilgisayar yeni bir VM adını doğrulayın.

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a>Bir bulut init komut dosyası oluşturma
Güvenlik için ilk önyüklemede güncelleştirmek için Ubuntu VM istiyor. Bulut init, kullandığınız Linux dağıtım bağlı olarak izleme komut dosyalarıyla yapabiliriz kullanma.

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a>Örnek bulut init betik `cloud_config_apt_upgrade.txt` Debian ailesi için
```yaml
#cloud-config
apt_upgrade: true
```

Linux önyüklendikten sonra yüklü olan paketlerin aracılığıyla güncelleştirilir **get apt**. Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) önyükleme sırasında yapılandırmak için bulut init kullanma.

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
The following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-to-add-a-user-to-linux"></a>Linux için bir kullanıcı eklemek için bir bulut init komut dosyası oluşturma
Yeni bir Linux VM ilk görevlerde biri kendiniz için bir kullanıcı eklemek veya kullanmaktan kaçınmak için *kök*. SSH anahtarları olan kullanılabilirlik ve güvenlik için en iyi uygulama ve eklendikten *~/.ssh/authorized_keys* bu bulut init komut dosyasıyla.

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

Linux önyüklendikten sonra listelenen tüm kullanıcılar oluşturulur ve sudo grubuna eklenir. Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) önyükleme sırasında yapılandırmak için bulut init kullanma.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

Oturum açma ve yeni oluşturulan kullanıcı doğrulayın.

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
Bulut init Linux VM'NİZDE önyüklemede değiştirmek için bir standart yolu durumundadır. Ayrıca Azure önyükleme veya çalışırken, LinuxVM değiştirmenize izin VM uzantıları sahiptir. Örneğin, VM çalışırken SSH veya kullanıcı bilgilerini sıfırlama Azure VMAccessExtension kullanabilirsiniz. Bulut başlatma ile parolayı sıfırlamak için bir yeniden başlatma gerekir.

[Sanal makine uzantıları ve özellikleri hakkında](extensions-features.md)

[Kullanıcılar, SSH ve onay yönetmek veya VMAccess uzantısını kullanarak Azure Linux VM'ler disklerde onarın](using-vmaccess-extension.md)