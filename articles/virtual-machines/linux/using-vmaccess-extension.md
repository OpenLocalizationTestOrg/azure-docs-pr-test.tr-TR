---
title: "aaaReset erişim tooan Azure Linux VM'de | Microsoft Docs"
description: "Nasıl toomanage kullanıcılar ve Linux VM'ler kullanma sıfırlama erişim VMAccess uzantısını hello ve Azure CLI 2.0 hello"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/04/2017
ms.author: danlep
ms.openlocfilehash: 2f8db01b9fac20bf547d8b1926e5c0b3c5d18280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a>Kullanıcılar, SSH ve onay yönetmek ya da Linux VM'ler kullanma onarım diskleri VMAccess uzantısını hello Azure CLI 2.0 ile Merhaba
Linux VM Hello diskte hata gösteriliyor. Linux VM için şekilde hello kök parola sıfırlama veya yanlışlıkla SSH özel anahtarınızı silinemez. Geri hello Datacenter hello gün içinde oluştuysa, var. toodrive ihtiyacınız ve ardından hello KVM tooget hello sunucu konsolunda açın. Merhaba Azure VMAccess uzantısını, tooaccess konsol tooreset erişim tooLinux hello ya da disk düzeyinde bakım gerçekleştirmek sağlar, KVM anahtar düşünün.

Bu makalede nasıl toouse Azure VMAccess uzantısını toocheck hello veya bir disk onarım, kullanıcı erişimi sıfırlama, kullanıcı hesaplarını yönetme veya Linux'ta hello SSH yapılandırmasını sıfırlamak gösterilmektedir. Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="ways-toouse-hello-vmaccess-extension"></a>Yolları toouse hello VMAccess uzantısını
Linux Vm'leriniz hello VMAccess uzantısını kullanmanın iki yolu vardır:

* Hello Azure CLI 2.0 ve gerekli hello parametrelerini kullanın.
* [Kullanım ham JSON dosyaları bu hello VMAccess uzantısını işlem](#use-json-files-and-the-vmaccess-extension) ve ardından hareket.

Aşağıdaki örnekler kullan hello [az vm kullanıcı](/cli/azure/vm/user) komutları. Aşağıdaki adımları tooperform ihtiyacınız hello son [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).

## <a name="reset-ssh-key"></a>SSH anahtarını Sıfırla
Merhaba aşağıdaki örnek sıfırlar hello SSH anahtarı hello kullanıcı için `azureuser` hello adlı VM üzerinde `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a>Parola sıfırlama
Merhaba aşağıdaki örnek sıfırlar hello hello kullanıcının parolasını `azureuser` hello adlı VM üzerinde `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a>SSH yeniden başlatma
Merhaba aşağıdaki örnek hello SSH arka plan programı yeniden başlatır ve SSH yapılandırma toodefault adlı bir VM'yi değerlerine sıfırlar hello `myVM`:

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a>Bir kullanıcı oluşturun
Merhaba aşağıdaki örnek adlı bir kullanıcı oluşturur `myNewUser` hello adlı VM kimlik doğrulaması için bir SSH anahtarı kullanarak `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a>Kullanıcı silme
Merhaba aşağıdaki örnek adlı bir kullanıcıyı siler `myNewUser` hello adlı VM üzerinde `myVM`:

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a>VMAccess uzantısını hello ve JSON dosyaları kullanın
Örnek hello ham JSON dosyaları kullanın. Kullanım [az vm uzantısı kümesi](/cli/azure/vm/extension#set) toothen, JSON dosyalarınızın çağırın. Bu JSON dosyaları da Azure şablonlardan çağrılabilir. 

### <a name="reset-user-access"></a>Kullanıcı erişimi sıfırlama
Linux VM üzerinde erişim tooroot kaybettiyseniz, bir kullanıcının SSH anahtarı veya parolayı VMAccess betik tooreset başlatabilirsiniz.

tooreset hello SSH ortak anahtarı bir kullanıcı adlı bir dosya oluşturun `reset_ssh_key.json` ve biçimini izleyen hello ayarlarını ekleyin. Hello için kendi değerlerinizi yerleştirin `username` ve `ssh_key` Parametreler:

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

Merhaba VMAccess betiği yürütün:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

tooreset bir kullanıcı parolasını adlı bir dosya oluşturun `reset_user_password.json` ve biçimini izleyen hello ayarlarını ekleyin. Hello için kendi değerlerinizi yerleştirin `username` ve `password` Parametreler:

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

Merhaba VMAccess betiği yürütün:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a>SSH yeniden başlatma
toorestart SSH arka plan Merhaba ve hello SSH yapılandırma toodefault değerleri sıfırlamak, adlı bir dosya oluşturun `reset_sshd.json`. İçeriği aşağıdaki hello ekleyin:

```json
{
  "reset_ssh": true
}
```

Merhaba VMAccess betiği yürütün:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a>Kullanıcıları yönetme

toocreate kimlik doğrulaması için bir SSH anahtarı kullanan bir kullanıcı adlı bir dosya oluşturun `create_new_user.json` ve biçimini izleyen hello ayarlarını ekleyin. Hello için kendi değerlerinizi yerleştirin `username` ve `ssh_key` Parametreler:

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Merhaba VMAccess betiği yürütün:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

toodelete bir kullanıcı adlı bir dosya oluşturun `delete_user.json` ve içeriği aşağıdaki hello ekleyin. Hello için kendi değer yerine `remove_user` parametre:

```json
{
  "remove_user":"myNewUser"
}
```

Merhaba VMAccess betiği yürütün:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a>Denetleyin veya hello disk onarın
VMAccess kullanarak da denetleyin ve toohello Linux VM eklenen bir disk onarın.

toocheck ve onarım hello disk adlı bir dosya oluşturun `disk_check_repair.json` ve biçimini izleyen hello ayarlarını ekleyin. Kendi hello adı değeri yerine `repair_disk`:

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

Merhaba VMAccess betiği yürütün:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a>Sonraki adımlar
Linux güncelleştirmek hello Azure VMAccess uzantısını kullanarak çalışan bir Linux VM üzerindeki bir yöntem toomake değişiklikleri kullanılır. Linux VM önyüklemede bulut Init ve Azure Resource Manager şablonları toomodify gibi araçları da kullanabilirsiniz.

[Sanal makine uzantıları ve Linux için özellikleri](extensions-features.md)

[Linux VM uzantıları ile Azure Resource Manager şablonları yazma](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Bulut init toocustomize bir Linux VM oluşturma sırasında kullanma](using-cloud-init.md)

