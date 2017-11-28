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
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a><span data-ttu-id="3f5b0-103">Kullanıcılar, SSH ve onay yönetmek veya Azure Linux VM'ler kullanma onarım diskleri VMAccess uzantısını hello Azure CLI 1.0 ile Merhaba</span><span class="sxs-lookup"><span data-stu-id="3f5b0-103">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension with hello Azure CLI 1.0</span></span>
<span data-ttu-id="3f5b0-104">Bu makalede nasıl toouse Azure VMAcesss uzantısı toocheck hello veya bir disk onarım, kullanıcı erişimi sıfırlama, kullanıcı hesaplarını yönetme veya Linux'ta hello SSHD yapılandırmayı sıfırlamak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-104">This article shows you how toouse hello Azure VMAcesss Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSHD configuration on Linux.</span></span> <span data-ttu-id="3f5b0-105">Merhaba makale gerektirir:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-105">hello article requires:</span></span>

* <span data-ttu-id="3f5b0-106">bir Azure hesabı ([ücretsiz deneme sürümü edinin](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="3f5b0-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="3f5b0-107">Merhaba [Azure CLI](../../cli-install-nodejs.md) oturum açarken `azure login`.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-107">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="3f5b0-108">Hello Azure CLI *olmalıdır* Azure Resource Manager moduna `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="3f5b0-109">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="3f5b0-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="3f5b0-110">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="3f5b0-111">[Azure CLI 1.0](#quick-commands)– bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="3f5b0-111">[Azure CLI 1.0](#quick-commands)– our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="3f5b0-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="3f5b0-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="3f5b0-113">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="3f5b0-113">Quick commands</span></span>
<span data-ttu-id="3f5b0-114">İki yolu toouse Linux sanal makineleri üzerinde VMAccess vardır:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-114">There are two ways toouse VMAccess on your Linux VMs:</span></span>

* <span data-ttu-id="3f5b0-115">Hello Azure CLI 1.0 ve hello kullanarak parametreleri gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-115">Using hello Azure CLI 1.0 and hello required parameters.</span></span>
* <span data-ttu-id="3f5b0-116">VMAccess işleyen ve ardından hareket ham JSON dosyaları kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-116">Using raw JSON files that VMAccess processes and then act on.</span></span>

<span data-ttu-id="3f5b0-117">Merhaba hızlı komut bölümü için biz toouse hello Azure CLI 1.0 kalacaklarını `azure vm reset-access` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-117">For hello quick command section, we are going toouse hello Azure CLI 1.0 `azure vm reset-access` method.</span></span> <span data-ttu-id="3f5b0-118">Aşağıdaki komut örnekleri Hello kendi ortamınızdaki hello değerlerle "örnek" içeren hello değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-118">In hello following command examples, replace hello values that contain "example" with hello values from your own environment.</span></span>

## <a name="create-a-resource-group-and-linux-vm"></a><span data-ttu-id="3f5b0-119">Bir kaynak grubu ve Linux VM oluşturun</span><span class="sxs-lookup"><span data-stu-id="3f5b0-119">Create a Resource Group and Linux VM</span></span>
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a><span data-ttu-id="3f5b0-120">Debian bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="3f5b0-120">Create a Debian VM</span></span>
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

## <a name="reset-root-password"></a><span data-ttu-id="3f5b0-121">Kök parola sıfırlama</span><span class="sxs-lookup"><span data-stu-id="3f5b0-121">Reset root password</span></span>
<span data-ttu-id="3f5b0-122">tooreset hello kök parola:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-122">tooreset hello root password:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a><span data-ttu-id="3f5b0-123">SSH anahtarı sıfırlama</span><span class="sxs-lookup"><span data-stu-id="3f5b0-123">SSH key reset</span></span>
<span data-ttu-id="3f5b0-124">bir kök olmayan kullanıcının tooreset hello SSH anahtarı:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-124">tooreset hello SSH key of a non-root user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a><span data-ttu-id="3f5b0-125">Bir kullanıcı oluşturun</span><span class="sxs-lookup"><span data-stu-id="3f5b0-125">Create a user</span></span>
<span data-ttu-id="3f5b0-126">bir kullanıcı toocreate:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-126">toocreate a user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a><span data-ttu-id="3f5b0-127">Kullanıcıyı kaldırma</span><span class="sxs-lookup"><span data-stu-id="3f5b0-127">Remove a user</span></span>
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a><span data-ttu-id="3f5b0-128">SSHD Sıfırla</span><span class="sxs-lookup"><span data-stu-id="3f5b0-128">Reset SSHD</span></span>
<span data-ttu-id="3f5b0-129">tooreset hello SSHD yapılandırması:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-129">tooreset hello SSHD configuration:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a><span data-ttu-id="3f5b0-130">Ayrıntılı kılavuz</span><span class="sxs-lookup"><span data-stu-id="3f5b0-130">Detailed walkthrough</span></span>
### <a name="vmaccess-defined"></a><span data-ttu-id="3f5b0-131">Tanımlanan VMAccess:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-131">VMAccess defined:</span></span>
<span data-ttu-id="3f5b0-132">Linux VM Hello diskte hata gösteriliyor.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-132">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="3f5b0-133">Linux VM için şekilde hello kök parola sıfırlama veya yanlışlıkla SSH özel anahtarınızı silinemez.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-133">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="3f5b0-134">Geri hello Datacenter hello gün içinde oluştuysa, var. toodrive ihtiyacınız ve ardından hello KVM tooget hello sunucu konsolunda açın.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-134">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="3f5b0-135">Merhaba Azure VMAccess uzantısını, tooaccess konsol tooreset erişim tooLinux hello ya da disk düzeyinde bakım gerçekleştirmek sağlar, KVM anahtar düşünün.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-135">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="3f5b0-136">İzlenecek yol, Hello için ayrıntılı biz toouse hello uzun biçiminde ham JSON dosyaları kullanan VMAccess geçiyor.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-136">For hello detailed walkthrough, we are going toouse hello long form of VMAccess, which uses raw JSON files.</span></span>  <span data-ttu-id="3f5b0-137">Bu VMAccess JSON dosyaları da Azure şablonlardan çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-137">These VMAccess JSON files can also be called from Azure templates.</span></span>

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a><span data-ttu-id="3f5b0-138">Bir Linux VM VMAccess toocheck veya Onar hello disk kullanma</span><span class="sxs-lookup"><span data-stu-id="3f5b0-138">Using VMAccess toocheck or repair hello disk of a Linux VM</span></span>
<span data-ttu-id="3f5b0-139">VMAccess kullanarak bir fsck yapabilirsiniz, Linux VM'NİZDE altında hello diskteki çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-139">Using VMAccess you can do a fsck run on hello disk under your Linux VM.</span></span>  <span data-ttu-id="3f5b0-140">Ayrıca, bir disk denetimi ve bir VMAccess kullanarak bir disk onarım yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-140">You can also do a disk check and a disk repair using a VMAccess.</span></span>

<span data-ttu-id="3f5b0-141">toocheck ve onarım hello disk bu VMAccess komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-141">toocheck, and then repair hello disk use this VMAccess script:</span></span>

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

<span data-ttu-id="3f5b0-142">Merhaba VMAccess betiği yürütün:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-142">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a><span data-ttu-id="3f5b0-143">VMAccess tooreset kullanıcı erişimi tooLinux kullanma</span><span class="sxs-lookup"><span data-stu-id="3f5b0-143">Using VMAccess tooreset user access tooLinux</span></span>
<span data-ttu-id="3f5b0-144">Linux VM üzerinde erişim tooroot kaybettiyseniz, Vmaccess'in betik tooreset hello kök parola başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-144">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset hello root password.</span></span>

<span data-ttu-id="3f5b0-145">tooreset hello kök parola, bu VMAccess komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-145">tooreset hello root password, use this VMAccess script:</span></span>

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

<span data-ttu-id="3f5b0-146">Merhaba VMAccess betiği yürütün:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-146">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

<span data-ttu-id="3f5b0-147">tooreset hello SSH anahtarı bir kök olmayan kullanıcının bu VMAccess komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-147">tooreset hello SSH key of a non-root user, use this VMAccess script:</span></span>

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

<span data-ttu-id="3f5b0-148">Merhaba VMAccess betiği yürütün:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-148">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a><span data-ttu-id="3f5b0-149">Linux'ta VMAccess toomanage kullanıcı hesaplarını kullanarak</span><span class="sxs-lookup"><span data-stu-id="3f5b0-149">Using VMAccess toomanage user accounts on Linux</span></span>
<span data-ttu-id="3f5b0-150">VMAccess kullanılan toomanage kullanıcılar oturum açmaya gerek kalmadan sudo veya hello kök hesabı kullanarak, Linux VM'de olabilir bir Python komut dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-150">VMAccess is a Python script that can be used toomanage users on your Linux VM without logging in and using sudo or hello root account.</span></span>

<span data-ttu-id="3f5b0-151">toocreate bir kullanıcı bu VMAccess komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-151">toocreate a user, use this VMAccess script:</span></span>

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="3f5b0-152">Merhaba VMAccess betiği yürütün:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-152">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

<span data-ttu-id="3f5b0-153">toodelete bir kullanıcı bu VMAccess komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-153">toodelete a user, use this VMAccess script:</span></span>

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

<span data-ttu-id="3f5b0-154">Merhaba VMAccess betiği yürütün:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-154">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a><span data-ttu-id="3f5b0-155">VMAccess tooreset hello SSHD Yapılandırması'nı kullanarak</span><span class="sxs-lookup"><span data-stu-id="3f5b0-155">Using VMAccess tooreset hello SSHD configuration</span></span>
<span data-ttu-id="3f5b0-156">Değişiklikleri toohello Linux VM'ler SSHD yapılandırması ve hello değişiklikleri doğrulama önce Kapat hello SSH bağlantı yaparsanız, SSH'ing engellenebilir geri dönün.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-156">If you make changes toohello Linux VMs SSHD configuration and close hello SSH connection before verifying hello changes, you may be prevented from SSH'ing back in.</span></span>  <span data-ttu-id="3f5b0-157">VMAccess SSH üzerinden oturum açılmış olmadan kullanılan tooreset hello SSHD yapılandırması geri tooa bilinen iyi yapılandırması olabilir.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-157">VMAccess can be used tooreset hello SSHD configuration back tooa known good configuration without being logged in over SSH.</span></span>

<span data-ttu-id="3f5b0-158">tooreset hello SSHD yapılandırma bu VMAccess komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-158">tooreset hello SSHD configuration use this VMAccess script:</span></span>

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="3f5b0-159">Merhaba VMAccess betiği yürütün:</span><span class="sxs-lookup"><span data-stu-id="3f5b0-159">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a><span data-ttu-id="3f5b0-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3f5b0-160">Next steps</span></span>
<span data-ttu-id="3f5b0-161">Linux güncelleştirmek Azure VMAccess uzantılarını kullanarak çalışan bir Linux VM üzerindeki bir yöntem toomake değişiklikleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-161">Updating Linux using Azure VMAccess Extensions is one method toomake changes on a running Linux VM.</span></span>  <span data-ttu-id="3f5b0-162">Linux VM önyüklemede bulut Init ve Azure şablonlarını toomodify gibi araçları da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f5b0-162">You can also use tools like cloud-init and Azure Templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="3f5b0-163">Sanal makine uzantıları ve özellikleri hakkında</span><span class="sxs-lookup"><span data-stu-id="3f5b0-163">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="3f5b0-164">Linux VM uzantıları ile Azure Resource Manager şablonları yazma</span><span class="sxs-lookup"><span data-stu-id="3f5b0-164">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="3f5b0-165">Bulut init toocustomize bir Linux VM oluşturma sırasında kullanma</span><span class="sxs-lookup"><span data-stu-id="3f5b0-165">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

