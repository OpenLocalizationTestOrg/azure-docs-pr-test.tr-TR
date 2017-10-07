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
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a><span data-ttu-id="860e3-103">Kullanıcılar, SSH ve onay yönetmek ya da Linux VM'ler kullanma onarım diskleri VMAccess uzantısını hello Azure CLI 2.0 ile Merhaba</span><span class="sxs-lookup"><span data-stu-id="860e3-103">Manage users, SSH, and check or repair disks on Linux VMs using hello VMAccess Extension with hello Azure CLI 2.0</span></span>
<span data-ttu-id="860e3-104">Linux VM Hello diskte hata gösteriliyor.</span><span class="sxs-lookup"><span data-stu-id="860e3-104">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="860e3-105">Linux VM için şekilde hello kök parola sıfırlama veya yanlışlıkla SSH özel anahtarınızı silinemez.</span><span class="sxs-lookup"><span data-stu-id="860e3-105">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="860e3-106">Geri hello Datacenter hello gün içinde oluştuysa, var. toodrive ihtiyacınız ve ardından hello KVM tooget hello sunucu konsolunda açın.</span><span class="sxs-lookup"><span data-stu-id="860e3-106">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="860e3-107">Merhaba Azure VMAccess uzantısını, tooaccess konsol tooreset erişim tooLinux hello ya da disk düzeyinde bakım gerçekleştirmek sağlar, KVM anahtar düşünün.</span><span class="sxs-lookup"><span data-stu-id="860e3-107">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="860e3-108">Bu makalede nasıl toouse Azure VMAccess uzantısını toocheck hello veya bir disk onarım, kullanıcı erişimi sıfırlama, kullanıcı hesaplarını yönetme veya Linux'ta hello SSH yapılandırmasını sıfırlamak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="860e3-108">This article shows you how toouse hello Azure VMAccess Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSH configuration on Linux.</span></span> <span data-ttu-id="860e3-109">Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="860e3-109">You can also perform these steps with hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="ways-toouse-hello-vmaccess-extension"></a><span data-ttu-id="860e3-110">Yolları toouse hello VMAccess uzantısını</span><span class="sxs-lookup"><span data-stu-id="860e3-110">Ways toouse hello VMAccess Extension</span></span>
<span data-ttu-id="860e3-111">Linux Vm'leriniz hello VMAccess uzantısını kullanmanın iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="860e3-111">There are two ways that you can use hello VMAccess Extension on your Linux VMs:</span></span>

* <span data-ttu-id="860e3-112">Hello Azure CLI 2.0 ve gerekli hello parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="860e3-112">Use hello Azure CLI 2.0 and hello required parameters.</span></span>
* <span data-ttu-id="860e3-113">[Kullanım ham JSON dosyaları bu hello VMAccess uzantısını işlem](#use-json-files-and-the-vmaccess-extension) ve ardından hareket.</span><span class="sxs-lookup"><span data-stu-id="860e3-113">[Use raw JSON files that hello VMAccess Extension process](#use-json-files-and-the-vmaccess-extension) and then act on.</span></span>

<span data-ttu-id="860e3-114">Aşağıdaki örnekler kullan hello [az vm kullanıcı](/cli/azure/vm/user) komutları.</span><span class="sxs-lookup"><span data-stu-id="860e3-114">hello following examples use [az vm user](/cli/azure/vm/user) commands.</span></span> <span data-ttu-id="860e3-115">Aşağıdaki adımları tooperform ihtiyacınız hello son [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="860e3-115">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="reset-ssh-key"></a><span data-ttu-id="860e3-116">SSH anahtarını Sıfırla</span><span class="sxs-lookup"><span data-stu-id="860e3-116">Reset SSH key</span></span>
<span data-ttu-id="860e3-117">Merhaba aşağıdaki örnek sıfırlar hello SSH anahtarı hello kullanıcı için `azureuser` hello adlı VM üzerinde `myVM`:</span><span class="sxs-lookup"><span data-stu-id="860e3-117">hello following example resets hello SSH key for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a><span data-ttu-id="860e3-118">Parola sıfırlama</span><span class="sxs-lookup"><span data-stu-id="860e3-118">Reset password</span></span>
<span data-ttu-id="860e3-119">Merhaba aşağıdaki örnek sıfırlar hello hello kullanıcının parolasını `azureuser` hello adlı VM üzerinde `myVM`:</span><span class="sxs-lookup"><span data-stu-id="860e3-119">hello following example resets hello password for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a><span data-ttu-id="860e3-120">SSH yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="860e3-120">Restart SSH</span></span>
<span data-ttu-id="860e3-121">Merhaba aşağıdaki örnek hello SSH arka plan programı yeniden başlatır ve SSH yapılandırma toodefault adlı bir VM'yi değerlerine sıfırlar hello `myVM`:</span><span class="sxs-lookup"><span data-stu-id="860e3-121">hello following example restarts hello SSH daemon and resets hello SSH configuration toodefault values on a VM named `myVM`:</span></span>

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a><span data-ttu-id="860e3-122">Bir kullanıcı oluşturun</span><span class="sxs-lookup"><span data-stu-id="860e3-122">Create a user</span></span>
<span data-ttu-id="860e3-123">Merhaba aşağıdaki örnek adlı bir kullanıcı oluşturur `myNewUser` hello adlı VM kimlik doğrulaması için bir SSH anahtarı kullanarak `myVM`:</span><span class="sxs-lookup"><span data-stu-id="860e3-123">hello following example creates a user named `myNewUser` using an SSH key for authentication on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a><span data-ttu-id="860e3-124">Kullanıcı silme</span><span class="sxs-lookup"><span data-stu-id="860e3-124">Delete a user</span></span>
<span data-ttu-id="860e3-125">Merhaba aşağıdaki örnek adlı bir kullanıcıyı siler `myNewUser` hello adlı VM üzerinde `myVM`:</span><span class="sxs-lookup"><span data-stu-id="860e3-125">hello following example deletes a user named `myNewUser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a><span data-ttu-id="860e3-126">VMAccess uzantısını hello ve JSON dosyaları kullanın</span><span class="sxs-lookup"><span data-stu-id="860e3-126">Use JSON files and hello VMAccess Extension</span></span>
<span data-ttu-id="860e3-127">Örnek hello ham JSON dosyaları kullanın.</span><span class="sxs-lookup"><span data-stu-id="860e3-127">hello following examples use raw JSON files.</span></span> <span data-ttu-id="860e3-128">Kullanım [az vm uzantısı kümesi](/cli/azure/vm/extension#set) toothen, JSON dosyalarınızın çağırın.</span><span class="sxs-lookup"><span data-stu-id="860e3-128">Use [az vm extension set](/cli/azure/vm/extension#set) toothen call your JSON files.</span></span> <span data-ttu-id="860e3-129">Bu JSON dosyaları da Azure şablonlardan çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="860e3-129">These JSON files can also be called from Azure templates.</span></span> 

### <a name="reset-user-access"></a><span data-ttu-id="860e3-130">Kullanıcı erişimi sıfırlama</span><span class="sxs-lookup"><span data-stu-id="860e3-130">Reset user access</span></span>
<span data-ttu-id="860e3-131">Linux VM üzerinde erişim tooroot kaybettiyseniz, bir kullanıcının SSH anahtarı veya parolayı VMAccess betik tooreset başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="860e3-131">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset a user's SSH key or password.</span></span>

<span data-ttu-id="860e3-132">tooreset hello SSH ortak anahtarı bir kullanıcı adlı bir dosya oluşturun `reset_ssh_key.json` ve biçimini izleyen hello ayarlarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="860e3-132">tooreset hello SSH public key of a user, create a file named `reset_ssh_key.json` and add settings in hello following format.</span></span> <span data-ttu-id="860e3-133">Hello için kendi değerlerinizi yerleştirin `username` ve `ssh_key` Parametreler:</span><span class="sxs-lookup"><span data-stu-id="860e3-133">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

<span data-ttu-id="860e3-134">Merhaba VMAccess betiği yürütün:</span><span class="sxs-lookup"><span data-stu-id="860e3-134">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

<span data-ttu-id="860e3-135">tooreset bir kullanıcı parolasını adlı bir dosya oluşturun `reset_user_password.json` ve biçimini izleyen hello ayarlarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="860e3-135">tooreset a user password, create a file named `reset_user_password.json` and add settings in hello following format.</span></span> <span data-ttu-id="860e3-136">Hello için kendi değerlerinizi yerleştirin `username` ve `password` Parametreler:</span><span class="sxs-lookup"><span data-stu-id="860e3-136">Substitute your own values for hello `username` and `password` parameters:</span></span>

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

<span data-ttu-id="860e3-137">Merhaba VMAccess betiği yürütün:</span><span class="sxs-lookup"><span data-stu-id="860e3-137">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a><span data-ttu-id="860e3-138">SSH yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="860e3-138">Restart SSH</span></span>
<span data-ttu-id="860e3-139">toorestart SSH arka plan Merhaba ve hello SSH yapılandırma toodefault değerleri sıfırlamak, adlı bir dosya oluşturun `reset_sshd.json`.</span><span class="sxs-lookup"><span data-stu-id="860e3-139">toorestart hello SSH daemon and reset hello SSH configuration toodefault values, create a file named `reset_sshd.json`.</span></span> <span data-ttu-id="860e3-140">İçeriği aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="860e3-140">Add hello following content:</span></span>

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="860e3-141">Merhaba VMAccess betiği yürütün:</span><span class="sxs-lookup"><span data-stu-id="860e3-141">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a><span data-ttu-id="860e3-142">Kullanıcıları yönetme</span><span class="sxs-lookup"><span data-stu-id="860e3-142">Manage users</span></span>

<span data-ttu-id="860e3-143">toocreate kimlik doğrulaması için bir SSH anahtarı kullanan bir kullanıcı adlı bir dosya oluşturun `create_new_user.json` ve biçimini izleyen hello ayarlarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="860e3-143">toocreate a user that uses an SSH key for authentication, create a file named `create_new_user.json` and add settings in hello following format.</span></span> <span data-ttu-id="860e3-144">Hello için kendi değerlerinizi yerleştirin `username` ve `ssh_key` Parametreler:</span><span class="sxs-lookup"><span data-stu-id="860e3-144">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="860e3-145">Merhaba VMAccess betiği yürütün:</span><span class="sxs-lookup"><span data-stu-id="860e3-145">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

<span data-ttu-id="860e3-146">toodelete bir kullanıcı adlı bir dosya oluşturun `delete_user.json` ve içeriği aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="860e3-146">toodelete a user, create a file named `delete_user.json` and add hello following content.</span></span> <span data-ttu-id="860e3-147">Hello için kendi değer yerine `remove_user` parametre:</span><span class="sxs-lookup"><span data-stu-id="860e3-147">Substitute your own value for hello `remove_user` parameter:</span></span>

```json
{
  "remove_user":"myNewUser"
}
```

<span data-ttu-id="860e3-148">Merhaba VMAccess betiği yürütün:</span><span class="sxs-lookup"><span data-stu-id="860e3-148">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a><span data-ttu-id="860e3-149">Denetleyin veya hello disk onarın</span><span class="sxs-lookup"><span data-stu-id="860e3-149">Check or repair hello disk</span></span>
<span data-ttu-id="860e3-150">VMAccess kullanarak da denetleyin ve toohello Linux VM eklenen bir disk onarın.</span><span class="sxs-lookup"><span data-stu-id="860e3-150">Using VMAccess you can also check and repair a disk that you added toohello Linux VM.</span></span>

<span data-ttu-id="860e3-151">toocheck ve onarım hello disk adlı bir dosya oluşturun `disk_check_repair.json` ve biçimini izleyen hello ayarlarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="860e3-151">toocheck and then repair hello disk, create a file named `disk_check_repair.json` and add settings in hello following format.</span></span> <span data-ttu-id="860e3-152">Kendi hello adı değeri yerine `repair_disk`:</span><span class="sxs-lookup"><span data-stu-id="860e3-152">Substitute your own value for hello name of `repair_disk`:</span></span>

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

<span data-ttu-id="860e3-153">Merhaba VMAccess betiği yürütün:</span><span class="sxs-lookup"><span data-stu-id="860e3-153">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a><span data-ttu-id="860e3-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="860e3-154">Next steps</span></span>
<span data-ttu-id="860e3-155">Linux güncelleştirmek hello Azure VMAccess uzantısını kullanarak çalışan bir Linux VM üzerindeki bir yöntem toomake değişiklikleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="860e3-155">Updating Linux using hello Azure VMAccess Extension is one method toomake changes on a running Linux VM.</span></span> <span data-ttu-id="860e3-156">Linux VM önyüklemede bulut Init ve Azure Resource Manager şablonları toomodify gibi araçları da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="860e3-156">You can also use tools like cloud-init and Azure Resource Manager templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="860e3-157">Sanal makine uzantıları ve Linux için özellikleri</span><span class="sxs-lookup"><span data-stu-id="860e3-157">Virtual machine extensions and features for Linux</span></span>](extensions-features.md)

[<span data-ttu-id="860e3-158">Linux VM uzantıları ile Azure Resource Manager şablonları yazma</span><span class="sxs-lookup"><span data-stu-id="860e3-158">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="860e3-159">Bulut init toocustomize bir Linux VM oluşturma sırasında kullanma</span><span class="sxs-lookup"><span data-stu-id="860e3-159">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md)

