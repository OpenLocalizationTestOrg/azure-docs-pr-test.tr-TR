---
title: "aaaUsing bulut init toocustomize azure'da oluşturma sırasında bir Linux VM | Microsoft Docs"
description: "Nasıl ile oluşturma sırasında bir Linux VM toouse bulut init toocustomize hello Azure CLI 1.0"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: v-livech
ms.openlocfilehash: b9f480bd04029956d0593bbef931795733cbc2f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation-with-hello-azure-cli-10"></a>Hello Azure CLI 1.0 ile oluşturma sırasında bulut init toocustomize bir Linux VM kullanın
Bu makalede nasıl toomake bulut init betik tooset hostname Merhaba, güncelleştirme yüklü paketleri ve kullanıcı hesaplarını yönetme gösterir.  Merhaba bulut başlatma komut dosyaları hello Azure clı'dan VM oluşturma sırasında denir.  Merhaba makale gerektirir:

* bir Azure hesabı ([ücretsiz deneme sürümü edinin](https://azure.microsoft.com/pricing/free-trial/)).
* Merhaba [Azure CLI](../../cli-install-nodejs.md) oturum açarken `azure login`.
* Hello Azure CLI *olmalıdır* Azure Resource Manager moduna `azure config mode arm`.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 1.0](#quick-commands) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için

## <a name="quick-commands"></a>Hızlı Komutlar
Merhaba hostname ayarlar, tüm paketleri güncelleştirir ve bir sudo kullanıcı tooLinux ekleyen bir bulut init.txt komut dosyası oluşturun.

```sh
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
Bir kaynak grubu toolaunch içine VM'ler oluşturun.

```azurecli
azure group create myResourceGroup westus
```

Bulut init tooconfigure kullanarak bir Linux VM oluşturun, önyükleme sırasında.

```azurecli
azure vm create \
  -g myResourceGroup \
  -n myVM \
  -l westus \
  -y Linux \
  -f myVMnic \
  -F myVNet \
  -P 10.0.0.0/22 \
  -j mySubnet \
  -k 10.0.0.0/24 \
  -Q canonical:ubuntuserver:14.04.2-LTS:latest \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -C cloud-init.txt
```

## <a name="detailed-walkthrough"></a>Ayrıntılı kılavuz
### <a name="introduction"></a>Giriş
Yeni bir Linux VM başlattığında, özelleştirilmiş veya gereksinimleriniz için hazır herhangi bir şeyin standart bir Linux VM aldıklarından. [Bulut init](https://cloudinit.readthedocs.org) standart yol tooinject ilk kez kaydınızı hello önyükleme yapmak, Linux VM bir komut dosyası veya yapılandırma ayarlarını aynıdır.

Azure üzerinde üç farklı yolla toomake bir değişiklik yoktur bir Linux VM üzerine olarak dağıtılabilir veya önyüklendiğinde.

* Bulut init kullanarak komut dosyalarını yerleştirir.
* Hello Azure'nı kullanarak betikleri Ekle [VMAccess uzantısını](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Bulut init kullanarak bir Azure şablonu.
* Bir Azure şablonu kullanarak [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

önyükleme sonra herhangi bir zamanda tooinject komut dosyaları:

* SSH toorun doğrudan komutları
* Hello Azure'nı kullanarak betikleri Ekle [VMAccess uzantısını](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), imperatively veya bir Azure şablonu
* Yapılandırma yönetimi araçları Ansible, Salt, Chef, Puppet gibi ve.

> [!NOTE]
> : VMAccess uzantısını yürütür hello aynı kök gibi bir komut dosyası yolu SSH kullanarak yapabilirsiniz.  Ancak, hello VM uzantısı kullanılarak çeşitli özellikler senaryonuza bağlı olarak yararlı olabilecek Azure sağladığı sağlar.
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Azure VM bulut init kullanılabilirliğine hızlı Oluştur görüntü diğer adları:
| Diğer ad | Yayımcı | Sunduğu | SKU | Sürüm | Bulut başlatma |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7.2 |en son |Yok |
| CoreOS |CoreOS |CoreOS |Dengeli |en son |Evet |
| Debian |credativ |Debian |8 |en son |Yok |
| openSUSE |SUSE |openSUSE |13.2 |en son |Yok |
| RHEL |RedHat |RHEL |7.2 |en son |Yok |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |en son |Evet |

Microsoft bizim ortakları tooget bulut dahil başlatma çalışmak ve çalışma tooAzure sağladıkları hello görüntülerinde ' dir.

## <a name="adding-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a>Bir bulut init betik toohello VM oluşturma hello Azure CLI ile ekleme
Azure üzerinde bir VM oluştururken, bir bulut init komut dosyası toolaunch hello Azure CLI kullanarak hello bulut init dosyasını belirtin `--custom-data` geçin.

Bir kaynak grubu toolaunch içine VM'ler oluşturun.

```azurecli
azure group create myResourceGroup westus
```

Bulut init tooconfigure kullanarak bir Linux VM oluşturun, önyükleme sırasında.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubnet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud-init.txt
```

## <a name="creating-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a>Bir bulut init betik tooset hello ana bilgisayar adını bir Linux VM oluşturma
Merhaba basit ve herhangi bir Linux VM için en önemli ayarları biri hello ana bilgisayar adı olacaktır. Biz kolayca bu bulut init ile bu komut dosyası kullanarak ayarlayabilirsiniz.  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>Adlı örnek bulut başlatma komut dosyasını `cloud_config_hostname.txt`.
```sh
#cloud-config
hostname: myservername
```

Çok hello hostname Hello ilk başlatılırken hello VM, bu bulut başlatma komut dosyasını ayarlar`myservername`.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_hostname.txt
```

Oturum açma ve hello hello ana doğrulayın yeni VM.

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-tooupdate-linux"></a>Bir bulut init betik tooupdate Linux oluşturma
Güvenlik için Ubuntu VM tooupdate hello ilk önyüklemede istiyor.  Bulut init kullanarak hello ile Merhaba Linux dağıtım kullandığınıza bağlı olarak kod izleyin yapabiliriz.

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a>Örnek bulut init betik `cloud_config_apt_upgrade.txt` hello Debian ailesi için
```sh
#cloud-config
apt_upgrade: true
```

Linux önyüklendikten sonra tüm yüklü hello paketler aracılığıyla güncelleştirilir `apt-get`.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
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

## <a name="creating-a-cloud-init-script-tooadd-a-user-toolinux"></a>Bir kullanıcı tooLinux bulut init betik tooadd oluşturma
Yeni bir Linux VM üzerinde hello ilk görevlerden biridir tooadd kendiniz veya tooavoid kullanmak için bir kullanıcı `root`. SSH anahtarları olan kullanılabilirlik ve güvenlik için en iyi uygulama ve toohello eklenen `~/.ssh/authorized_keys` bu bulut init komut dosyasıyla.

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a>Örnek bulut init betik `cloud_config_add_users.txt` Debian ailesi için
```sh
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

Linux önyüklendikten sonra tüm listelenen hello oluşturulan ve eklenen toohello sudo Grup kullanıcılardır.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
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

## <a name="next-steps"></a>Sonraki Adımlar
Bulut init bir standart yol toomodify önyükleme, Linux VM'de durumundadır. Ayrıca Azure toomodify izin VM uzantıları, LinuxVM önyükleme veya çalışırken sahiptir. Örneğin, Hello VM çalışırken hello Azure VMAccessExtension tooreset SSH veya kullanıcı bilgilerini kullanabilirsiniz. Bulut başlatma ile bir yeniden başlatma tooreset hello parola gerekir.

[Sanal makine uzantıları ve özellikleri hakkında](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Kullanıcılar, SSH ve onay yönetmek veya VMAccess uzantısını kullanarak Azure Linux VM'ler üzerinde onarım diskleri hello](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

