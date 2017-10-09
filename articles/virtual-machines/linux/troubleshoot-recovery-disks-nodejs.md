---
title: bir Linux VM hello Azure CLI 1.0 ile sorun giderme aaaUse | Microsoft Docs
description: "Nasıl bağlanan hello işletim sistemi diski tooa kurtarma VM kullanarak Linux VM sorunları tootroubleshoot hello Azure CLI 1.0 öğrenin"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 398f681d1149299d444fcfdab20737315db02855
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-cli-10"></a><span data-ttu-id="6c568-103">Bir Linux VM hello işletim sistemi disk tooa kurtarma VM ekleyerek sorun giderme kullanarak hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6c568-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="6c568-104">Linux sanal makine (VM) önyükleme veya disk bir hatayla karşılaştığında, sorun giderme adımları hello sanal sabit diske kendisini tooperform gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="6c568-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="6c568-105">Geçersiz bir giriş yaygın bir örnek olacaktır `/etc/fstab` engelleyen hello VM mümkün tooboot başarıyla bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="6c568-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="6c568-106">Bu makale ayrıntıları toouse hello nasıl Azure CLI 1.0 tooconnect, sanal sabit hataları tooanother Linux VM toofix disk sonra özgün VM'yi yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c568-106">This article details how toouse hello Azure CLI 1.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="6c568-107">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="6c568-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="6c568-108">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="6c568-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="6c568-109">[Azure CLI 1.0](#recovery-process-overview) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="6c568-109">[Azure CLI 1.0](#recovery-process-overview) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="6c568-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="6c568-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="6c568-111">Kurtarma işlemine genel bakış</span><span class="sxs-lookup"><span data-stu-id="6c568-111">Recovery process overview</span></span>
<span data-ttu-id="6c568-112">sorun giderme işlemi hello aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="6c568-112">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="6c568-113">Merhaba sanal sabit diskleri tutmak hello VM karşılaşmadan sorunları, silin.</span><span class="sxs-lookup"><span data-stu-id="6c568-113">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="6c568-114">Ekleme ve sorun giderme amacıyla hello sanal sabit disk tooanother Linux VM bağlayın.</span><span class="sxs-lookup"><span data-stu-id="6c568-114">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="6c568-115">VM sorun giderme toohello bağlayın.</span><span class="sxs-lookup"><span data-stu-id="6c568-115">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="6c568-116">Dosyaları düzenleyin veya herhangi bir aracı toofix sorunları hello özgün sanal sabit disk üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6c568-116">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="6c568-117">Çıkarın ve VM sorun giderme hello hello sanal sabit diski kullanımdan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="6c568-117">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="6c568-118">Merhaba özgün sanal sabit disk kullanan bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c568-118">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="6c568-119">Bilgisayarınızda yüklü olduğundan emin olun [en son Azure CLI 1.0 hello](../../cli-install-nodejs.md) yüklü ve oturum açmış ve Resource Manager modunu kullanma:</span><span class="sxs-lookup"><span data-stu-id="6c568-119">Make sure that you have [hello latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="6c568-120">Hello aşağıdaki örneklerde, parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6c568-120">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="6c568-121">Örnek parametre adlarında `myResourceGroup`, `mystorageaccount`, ve `myVM`.</span><span class="sxs-lookup"><span data-stu-id="6c568-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="6c568-122">Önyükleme sorunlarını belirleme</span><span class="sxs-lookup"><span data-stu-id="6c568-122">Determine boot issues</span></span>
<span data-ttu-id="6c568-123">Merhaba seri çıkış toodetermine neden VM mümkün tooboot doğru değil inceleyin.</span><span class="sxs-lookup"><span data-stu-id="6c568-123">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="6c568-124">Yaygın bir örnek, geçersiz bir giriş olduğunu `/etc/fstab`, veya sanal sabit diski olan silindiğini veya taşındığını temel hello.</span><span class="sxs-lookup"><span data-stu-id="6c568-124">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="6c568-125">Merhaba aşağıdaki örnek hello seri çıkış adlı VM hello alır `myVM` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="6c568-125">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="6c568-126">Merhaba seri çıkış toodetermine neden hello VM tooboot başarısız oluyor gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="6c568-126">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="6c568-127">Merhaba seri çıkış herhangi bir gösterge sağlayan değil, tooreview günlük dosyalarında gerekebilir `/var/log` hello sanal olduktan sonra sabit disk VM sorun giderme tooa bağlı.</span><span class="sxs-lookup"><span data-stu-id="6c568-127">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="6c568-128">Var olan sanal sabit disk ayrıntılarını görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="6c568-128">View existing virtual hard disk details</span></span>
<span data-ttu-id="6c568-129">Sanal sabit disk tooanother VM ekleyebilmek için tooidentify hello adı hello sanal sabit disk (VHD) gerekir.</span><span class="sxs-lookup"><span data-stu-id="6c568-129">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="6c568-130">Merhaba aşağıdaki örnek alır bilgi hello adlı VM için `myVM` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="6c568-130">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="6c568-131">Ara `Vhd URI` komutu önceki hello hello çıktısını içinde.</span><span class="sxs-lookup"><span data-stu-id="6c568-131">Look for `Vhd URI` in hello output from hello preceding command.</span></span> <span data-ttu-id="6c568-132">Merhaba aşağıdaki kesilmiş örnek çıkış gösterir hello `Vhd URI` hello son satırında:</span><span class="sxs-lookup"><span data-stu-id="6c568-132">hello following truncated example output shows hello `Vhd URI` on hello last line:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myVM"
+ Looking up hello NIC "myNic"
+ Looking up hello public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a><span data-ttu-id="6c568-133">Var olan VM silme</span><span class="sxs-lookup"><span data-stu-id="6c568-133">Delete existing VM</span></span>
<span data-ttu-id="6c568-134">Sanal sabit diskler ve sanal makineler Azure'da iki ayrı kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="6c568-134">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="6c568-135">Bir sanal sabit disk hello işletim sisteminin kendisi, uygulamalar ve yapılandırmalar depolandığı ' dir.</span><span class="sxs-lookup"><span data-stu-id="6c568-135">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="6c568-136">Merhaba VM kendisini hello boyutunu veya konumunu tanımlar ve bir sanal sabit disk veya sanal ağ arabirim kartı (NIC) gibi kaynakları başvuran meta verilerdir.</span><span class="sxs-lookup"><span data-stu-id="6c568-136">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="6c568-137">Her sanal sabit diske bağlı olduğunda atanmış bir kira sahip tooa VM.</span><span class="sxs-lookup"><span data-stu-id="6c568-137">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="6c568-138">Veri diskleri bağlı ve hatta hello VM çalışırken ayrılmış olsa da, hello VM kaynak silinmedikçe hello işletim sistemi diski ayrılamıyor.</span><span class="sxs-lookup"><span data-stu-id="6c568-138">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="6c568-139">Bu VM durduruldu ve deallocated durumda olduğunda bile hello kira tooassociate hello işletim sistemi diski bir VM ile devam eder.</span><span class="sxs-lookup"><span data-stu-id="6c568-139">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="6c568-140">İlk adım toorecover hello VM toodelete hello VM kendisini kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="6c568-140">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="6c568-141">Silme hello VM hello sanal sabit diskleri depolama hesabınızdaki bırakır.</span><span class="sxs-lookup"><span data-stu-id="6c568-141">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="6c568-142">Merhaba, VM silinmiş sonra hello sanal sabit disk tooanother VM tootroubleshoot ekleme ve hello hataları çözümleyin.</span><span class="sxs-lookup"><span data-stu-id="6c568-142">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="6c568-143">Aşağıdaki örnek siler hello hello adlı VM `myVM` adlı hello kaynak grubundan `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="6c568-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="6c568-144">Merhaba VM hello sanal sabit disk tooanother VM eklemeden önce silme tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="6c568-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="6c568-145">Merhaba kira hello sanal sabit diskte hello VM ile ilişkilendiren hello sanal sabit disk tooanother VM iliştirebilirsiniz önce yayınlanan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6c568-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="6c568-146">Var olan sanal sabit disk tooanother VM ekleme</span><span class="sxs-lookup"><span data-stu-id="6c568-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="6c568-147">Sonraki birkaç adımda için Merhaba, sorun giderme amacıyla başka bir VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="6c568-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="6c568-148">VM toobrowse sorun giderme hello varolan sanal sabit disk toothis ekleme ve hello diskin içeriği düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="6c568-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="6c568-149">Bu işlem toocorrect sağlar herhangi bir yapılandırma hataları veya gözden geçirme ek uygulama veya sistem günlük dosyaları, örneğin.</span><span class="sxs-lookup"><span data-stu-id="6c568-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="6c568-150">Seçin veya sorun giderme amacıyla başka bir VM toouse oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c568-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="6c568-151">Merhaba varolan bir sanal sabit diski taktığınızda hello URL toohello disk hello önceki elde belirtin `azure vm show` komutu.</span><span class="sxs-lookup"><span data-stu-id="6c568-151">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `azure vm show` command.</span></span> <span data-ttu-id="6c568-152">Merhaba aşağıdaki örnek iliştirir adlı VM sorun giderme var olan bir sanal sabit disk toohello `myVMRecovery` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="6c568-152">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="6c568-153">Merhaba bağlı veri diski bağlama</span><span class="sxs-lookup"><span data-stu-id="6c568-153">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="6c568-154">Merhaba Aşağıdaki örnekler bir Ubuntu VM gerekli hello adımları ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6c568-154">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="6c568-155">Red Hat Enterprise Linux veya SUSE, gibi farklı Linux distro kullanıyorsanız hello günlük dosyası konumları ve `mount` komutları biraz farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="6c568-155">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="6c568-156">Belirli distro hello uygun değişiklikleri komutları için toohello belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="6c568-156">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="6c568-157">SSH tooyour VM Hello uygun kimlik bilgilerini kullanarak sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="6c568-157">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="6c568-158">Bu disk VM sorun giderme hello ilk veri bağlı disk tooyour ise, hello disk büyük olasılıkla çok bağlı`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="6c568-158">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="6c568-159">Kullanım `dmseg` tooview bağlı diskler:</span><span class="sxs-lookup"><span data-stu-id="6c568-159">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="6c568-160">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="6c568-160">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="6c568-161">Örnek önceki hello hello işletim sistemi disk altındadır `/dev/sda` ve hello geçici disk, her VM için belirtilen `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="6c568-161">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="6c568-162">Birden fazla veri diski varsa, bunlar adresindeki olmalıdır `/dev/sdd`, `/dev/sde`ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="6c568-162">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="6c568-163">Bir dizin toomount, varolan bir sanal sabit diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c568-163">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="6c568-164">Merhaba aşağıdaki örnek adlı bir dizin oluşturur `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="6c568-164">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="6c568-165">Var olan sanal sabit diskin birden çok bölüm varsa, gerekli hello bölüm bağlayın.</span><span class="sxs-lookup"><span data-stu-id="6c568-165">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="6c568-166">Merhaba aşağıdaki örnek bağlar hello ilk birincil bölüm adresindeki `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="6c568-166">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="6c568-167">Evrensel benzersiz tanımlayıcı (UUID) hello sanal sabit disk kullanarak Azure'daki sanal makineleri üzerinde toomount veri diskleri hello en iyi uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="6c568-167">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="6c568-168">Bu kısa sorun giderme senaryosu için bağlama hello sanal sabit disk hello UUID kullanarak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="6c568-168">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="6c568-169">Bununla birlikte, normal kullanım altında düzenleme `/etc/fstab` toomount sanal sabit diskleri yerine UUID neden olabilir, aygıt adı kullanılarak hello VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="6c568-169">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="6c568-170">Özgün sanal sabit diskinde ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="6c568-170">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="6c568-171">Merhaba varolan bir sanal sabit takılı diski ile tüm bakım ve sorun giderme adımları gereken şekilde artık gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c568-171">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="6c568-172">Merhaba sorunlar ele sonra aşağıdaki adımları hello ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="6c568-172">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="6c568-173">Çıkarın ve özgün sanal sabit disk ayırma</span><span class="sxs-lookup"><span data-stu-id="6c568-173">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="6c568-174">Hatalarınızı çözüldükten sonra çıkarın ve sorun giderme VM'den hello varolan sanal sabit disk ayırma.</span><span class="sxs-lookup"><span data-stu-id="6c568-174">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="6c568-175">VM sorun giderme hello sanal sabit disk toohello ekleme hello kira serbest kadar herhangi bir VM ile sanal sabit disk kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="6c568-175">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="6c568-176">SSH oturumu tooyour VM sorun giderme hello hello varolan bir sanal sabit diski çıkarın.</span><span class="sxs-lookup"><span data-stu-id="6c568-176">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="6c568-177">Merhaba ana dizin, bağlama noktası için dışında ilk değiştirin:</span><span class="sxs-lookup"><span data-stu-id="6c568-177">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="6c568-178">Şimdi hello varolan bir sanal sabit diski çıkarın.</span><span class="sxs-lookup"><span data-stu-id="6c568-178">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="6c568-179">Merhaba aşağıdaki örnek çıkarır hello aygıt `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="6c568-179">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="6c568-180">Şimdi hello VM hello sanal sabit diski kullanımdan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="6c568-180">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="6c568-181">VM sorun giderme hello SSH oturumu tooyour çıkın.</span><span class="sxs-lookup"><span data-stu-id="6c568-181">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="6c568-182">Hello Azure CLI'da, ilk liste hello VM sorun giderme veri diskleri tooyour bağlı.</span><span class="sxs-lookup"><span data-stu-id="6c568-182">In hello Azure CLI, first list hello attached data disks tooyour troubleshooting VM.</span></span> <span data-ttu-id="6c568-183">Merhaba listeleri hello veri diskleri aşağıdaki örnek bağlı toohello adlı VM `myVMRecovery` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="6c568-183">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    <span data-ttu-id="6c568-184">Not hello `Lun` , varolan bir sanal sabit disk için değer.</span><span class="sxs-lookup"><span data-stu-id="6c568-184">Note hello `Lun` value for your existing virtual hard disk.</span></span> <span data-ttu-id="6c568-185">Merhaba aşağıdaki örnek komut çıktısı hello varolan sanal diski LUN 0 ekli gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="6c568-185">hello following example command output shows hello existing virtual disk attached at LUN 0:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Looking up hello VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    <span data-ttu-id="6c568-186">Geçerli hello kullanarak VM Hello veri diski kullanımdan çıkarın `Lun` değeri:</span><span class="sxs-lookup"><span data-stu-id="6c568-186">Detach hello data disk from your VM using hello applicable `Lun` value:</span></span>

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="6c568-187">Özgün sabit diskten VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c568-187">Create VM from original hard disk</span></span>
<span data-ttu-id="6c568-188">bir VM, özgün sanal sabit diskten toocreate kullanmak [bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="6c568-188">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="6c568-189">Merhaba gerçek JSON şablon bağlantıyı izleyerek hello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="6c568-189">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="6c568-190">https://RAW.githubusercontent.com/Azure/Azure-QuickStart-Templates/master/201-VM-Specialized-VHD/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="6c568-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="6c568-191">Merhaba şablon hello VHD URL'si hello gelen kullanarak mevcut sanal ağda, bir VM dağıtır önceki komutu.</span><span class="sxs-lookup"><span data-stu-id="6c568-191">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="6c568-192">Merhaba aşağıdaki örnek dağıtır hello şablon toohello kaynak grubu adında `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="6c568-192">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

<span data-ttu-id="6c568-193">Yanıt hello ister VM adı gibi hello şablonunun (`myDeployedVM` hello örnek), işletim sistemi türü (`Linux`) ve VM boyutu (`Standard_DS1_v2`).</span><span class="sxs-lookup"><span data-stu-id="6c568-193">Answer hello prompts for hello template such as VM name (`myDeployedVM` hello following example), OS type (`Linux`), and VM size (`Standard_DS1_v2`).</span></span> <span data-ttu-id="6c568-194">Merhaba `osDiskVhdUri` olduğundan, hello aynı VM sorun giderme hello varolan sanal sabit disk toohello eklerken daha önce kullanılan.</span><span class="sxs-lookup"><span data-stu-id="6c568-194">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span> <span data-ttu-id="6c568-195">Merhaba komutu çıktısı ve istemleri örneği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="6c568-195">An example of hello command output and prompts is as follows:</span></span>

```azurecli
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment toocomplete
+
```


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="6c568-196">Önyükleme tanılaması yeniden etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="6c568-196">Re-enable boot diagnostics</span></span>

<span data-ttu-id="6c568-197">Merhaba varolan sanal sabit diskten VM'nizi oluşturduğunuzda, önyükleme tanılaması otomatik olarak etkinleştirilmemiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="6c568-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="6c568-198">Merhaba aşağıdaki örnek hello tanılama uzantısını hello adlı VM üzerinde etkinleştirir `myDeployedVM` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="6c568-198">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="6c568-199">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6c568-199">Next steps</span></span>
<span data-ttu-id="6c568-200">Tooyour VM bağlantı sorunları yaşıyorsanız, bkz: [sorun giderme SSH bağlantıları tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6c568-200">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="6c568-201">VM üzerinde çalışan uygulamalara erişim sorunları için bkz: [bir Linux VM üzerinde uygulama bağlantı sorunlarını giderme](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6c568-201">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
