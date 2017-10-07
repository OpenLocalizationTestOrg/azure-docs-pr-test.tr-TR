---
title: "Azure Linux VM'ler kullanma aaaReset erişim hello VMAccess uzantısını | Microsoft Docs"
description: "Merhaba VMAccess uzantısını kullanarak Azure Linux VM'ler erişimi sıfırlayın."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: 2636655f3f7d14ba30e1dc62c319e4e278521ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a>Kullanıcılar, SSH ve onay yönetmek veya Azure Linux VM'ler kullanma onarım diskleri VMAccess uzantısını hello Azure CLI 1.0 ile Merhaba
Bu makalede nasıl toouse Azure VMAcesss uzantısı toocheck hello veya bir disk onarım, kullanıcı erişimi sıfırlama, kullanıcı hesaplarını yönetme veya Linux'ta hello SSHD yapılandırmayı sıfırlamak gösterilmektedir. Merhaba makale gerektirir:

* bir Azure hesabı ([ücretsiz deneme sürümü edinin](https://azure.microsoft.com/pricing/free-trial/)).
* Merhaba [Azure CLI](../../cli-install-nodejs.md) oturum açarken `azure login`.
* Hello Azure CLI *olmalıdır* Azure Resource Manager moduna `azure config mode arm`.


## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 1.0](#quick-commands)– bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için


## <a name="quick-commands"></a>Hızlı komutlar
İki yolu toouse Linux sanal makineleri üzerinde VMAccess vardır:

* Hello Azure CLI 1.0 ve hello kullanarak parametreleri gereklidir.
* VMAccess işleyen ve ardından hareket ham JSON dosyaları kullanıyor.

Merhaba hızlı komut bölümü için biz toouse hello Azure CLI 1.0 kalacaklarını `azure vm reset-access` yöntemi. Aşağıdaki komut örnekleri Hello kendi ortamınızdaki hello değerlerle "örnek" içeren hello değerlerini değiştirin.

## <a name="create-a-resource-group-and-linux-vm"></a>Bir kaynak grubu ve Linux VM oluşturun
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a>Debian bir VM oluşturma
```azurecli
azure vm quick-create \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -g myResourceGroup \
  -l westus \
  -y Linux \
  -n myVM \
  -Q Debian
```

## <a name="reset-root-password"></a>Kök parola sıfırlama
tooreset hello kök parola:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a>SSH anahtarı sıfırlama
bir kök olmayan kullanıcının tooreset hello SSH anahtarı:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a>Bir kullanıcı oluşturun
bir kullanıcı toocreate:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a>Kullanıcıyı kaldırma
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a>SSHD Sıfırla
tooreset hello SSHD yapılandırması:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a>Ayrıntılı kılavuz
### <a name="vmaccess-defined"></a>Tanımlanan VMAccess:
Linux VM Hello diskte hata gösteriliyor. Linux VM için şekilde hello kök parola sıfırlama veya yanlışlıkla SSH özel anahtarınızı silinemez. Geri hello Datacenter hello gün içinde oluştuysa, var. toodrive ihtiyacınız ve ardından hello KVM tooget hello sunucu konsolunda açın. Merhaba Azure VMAccess uzantısını, tooaccess konsol tooreset erişim tooLinux hello ya da disk düzeyinde bakım gerçekleştirmek sağlar, KVM anahtar düşünün.

İzlenecek yol, Hello için ayrıntılı biz toouse hello uzun biçiminde ham JSON dosyaları kullanan VMAccess geçiyor.  Bu VMAccess JSON dosyaları da Azure şablonlardan çağrılabilir.

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a>Bir Linux VM VMAccess toocheck veya Onar hello disk kullanma
VMAccess kullanarak bir fsck yapabilirsiniz, Linux VM'NİZDE altında hello diskteki çalıştırın.  Ayrıca, bir disk denetimi ve bir VMAccess kullanarak bir disk onarım yapabilirsiniz.

toocheck ve onarım hello disk bu VMAccess komut dosyasını kullanın:

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

Merhaba VMAccess betiği yürütün:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a>VMAccess tooreset kullanıcı erişimi tooLinux kullanma
Linux VM üzerinde erişim tooroot kaybettiyseniz, Vmaccess'in betik tooreset hello kök parola başlatabilirsiniz.

tooreset hello kök parola, bu VMAccess komut dosyasını kullanın:

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

Merhaba VMAccess betiği yürütün:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

tooreset hello SSH anahtarı bir kök olmayan kullanıcının bu VMAccess komut dosyasını kullanın:

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

Merhaba VMAccess betiği yürütün:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a>Linux'ta VMAccess toomanage kullanıcı hesaplarını kullanarak
VMAccess kullanılan toomanage kullanıcılar oturum açmaya gerek kalmadan sudo veya hello kök hesabı kullanarak, Linux VM'de olabilir bir Python komut dosyasıdır.

toocreate bir kullanıcı bu VMAccess komut dosyasını kullanın:

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Merhaba VMAccess betiği yürütün:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

toodelete bir kullanıcı bu VMAccess komut dosyasını kullanın:

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

Merhaba VMAccess betiği yürütün:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a>VMAccess tooreset hello SSHD Yapılandırması'nı kullanarak
Değişiklikleri toohello Linux VM'ler SSHD yapılandırması ve hello değişiklikleri doğrulama önce Kapat hello SSH bağlantı yaparsanız, SSH'ing engellenebilir geri dönün.  VMAccess SSH üzerinden oturum açılmış olmadan kullanılan tooreset hello SSHD yapılandırması geri tooa bilinen iyi yapılandırması olabilir.

tooreset hello SSHD yapılandırma bu VMAccess komut dosyasını kullanın:

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

Merhaba VMAccess betiği yürütün:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a>Sonraki adımlar
Linux güncelleştirmek Azure VMAccess uzantılarını kullanarak çalışan bir Linux VM üzerindeki bir yöntem toomake değişiklikleri kullanılır.  Linux VM önyüklemede bulut Init ve Azure şablonlarını toomodify gibi araçları da kullanabilirsiniz.

[Sanal makine uzantıları ve özellikleri hakkında](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Linux VM uzantıları ile Azure Resource Manager şablonları yazma](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Bulut init toocustomize bir Linux VM oluşturma sırasında kullanma](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

