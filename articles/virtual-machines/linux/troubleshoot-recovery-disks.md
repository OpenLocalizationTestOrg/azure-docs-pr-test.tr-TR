---
title: bir Linux VM hello Azure CLI 2.0 ile sorun giderme aaaUse | Microsoft Docs
description: "Nasıl bağlanan hello işletim sistemi diski tooa kurtarma VM kullanarak Linux VM sorunları tootroubleshoot hello Azure CLI 2.0 öğrenin"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 776d61b61280f46e3699157addcdb1e7dfb6818e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a><span data-ttu-id="2c21e-103">Bir Linux VM hello işletim sistemi disk tooa kurtarma VM hello Azure CLI 2.0 ile ekleyerek sorun giderme</span><span class="sxs-lookup"><span data-stu-id="2c21e-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM with hello Azure CLI 2.0</span></span>
<span data-ttu-id="2c21e-104">Linux sanal makine (VM) önyükleme veya disk bir hatayla karşılaştığında, sorun giderme adımları hello sanal sabit diske kendisini tooperform gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="2c21e-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="2c21e-105">Geçersiz bir giriş yaygın bir örnek olacaktır `/etc/fstab` engelleyen hello VM mümkün tooboot başarıyla bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="2c21e-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="2c21e-106">Bu makale ayrıntıları toouse hello nasıl Azure CLI 2.0 tooconnect, sanal sabit hataları tooanother Linux VM toofix disk sonra özgün VM'yi yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2c21e-106">This article details how toouse hello Azure CLI 2.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span> <span data-ttu-id="2c21e-107">Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c21e-107">You can also perform these steps with hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="2c21e-108">Kurtarma işlemine genel bakış</span><span class="sxs-lookup"><span data-stu-id="2c21e-108">Recovery process overview</span></span>
<span data-ttu-id="2c21e-109">sorun giderme işlemi hello aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="2c21e-109">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="2c21e-110">Merhaba sanal sabit diskleri tutmak hello VM karşılaşmadan sorunları, silin.</span><span class="sxs-lookup"><span data-stu-id="2c21e-110">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="2c21e-111">Ekleme ve sorun giderme amacıyla hello sanal sabit disk tooanother Linux VM bağlayın.</span><span class="sxs-lookup"><span data-stu-id="2c21e-111">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="2c21e-112">VM sorun giderme toohello bağlayın.</span><span class="sxs-lookup"><span data-stu-id="2c21e-112">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="2c21e-113">Dosyaları düzenleyin veya herhangi bir aracı toofix sorunları hello özgün sanal sabit disk üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2c21e-113">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="2c21e-114">Çıkarın ve VM sorun giderme hello hello sanal sabit diski kullanımdan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="2c21e-114">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="2c21e-115">Merhaba özgün sanal sabit disk kullanan bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2c21e-115">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="2c21e-116">tooperform aşağıdaki sorun giderme adımlarını, hello son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="2c21e-116">tooperform these troubleshooting steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="2c21e-117">Hello aşağıdaki örneklerde, parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2c21e-117">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="2c21e-118">Örnek parametre adlarında `myResourceGroup`, `mystorageaccount`, ve `myVM`.</span><span class="sxs-lookup"><span data-stu-id="2c21e-118">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="2c21e-119">Önyükleme sorunlarını belirleme</span><span class="sxs-lookup"><span data-stu-id="2c21e-119">Determine boot issues</span></span>
<span data-ttu-id="2c21e-120">Merhaba seri çıkış toodetermine neden VM mümkün tooboot doğru değil inceleyin.</span><span class="sxs-lookup"><span data-stu-id="2c21e-120">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="2c21e-121">Yaygın bir örnek, geçersiz bir giriş olduğunu `/etc/fstab`, veya sanal sabit diski olan silindiğini veya taşındığını temel hello.</span><span class="sxs-lookup"><span data-stu-id="2c21e-121">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="2c21e-122">Merhaba önyükleme günlükleriyle alma [az vm önyükleme tanılaması get-önyükleme-günlük](/cli/azure/vm/boot-diagnostics#get-boot-log).</span><span class="sxs-lookup"><span data-stu-id="2c21e-122">Get hello boot logs with [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span></span> <span data-ttu-id="2c21e-123">Merhaba aşağıdaki örnek hello seri çıkış adlı VM hello alır `myVM` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2c21e-123">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="2c21e-124">Merhaba seri çıkış toodetermine neden hello VM tooboot başarısız oluyor gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="2c21e-124">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="2c21e-125">Merhaba seri çıkış herhangi bir gösterge sağlayan değil, tooreview günlük dosyalarında gerekebilir `/var/log` hello sanal olduktan sonra sabit disk VM sorun giderme tooa bağlı.</span><span class="sxs-lookup"><span data-stu-id="2c21e-125">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="2c21e-126">Var olan sanal sabit disk ayrıntılarını görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="2c21e-126">View existing virtual hard disk details</span></span>
<span data-ttu-id="2c21e-127">Sanal sabit disk (VHD) tooanother VM ekleyebilmek için tooidentify hello hello işletim sistemi diski URI'sini gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c21e-127">Before you can attach your virtual hard disk (VHD) tooanother VM, you need tooidentify hello URI of hello OS disk.</span></span> 

<span data-ttu-id="2c21e-128">VM ile hakkındaki bilgileri görüntüleyin [az vm Göster](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="2c21e-128">View information about your VM with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="2c21e-129">Kullanım hello `--query` bayrağı tooextract hello URI toohello işletim sistemi disk.</span><span class="sxs-lookup"><span data-stu-id="2c21e-129">Use hello `--query` flag tooextract hello URI toohello OS disk.</span></span> <span data-ttu-id="2c21e-130">Merhaba aşağıdaki örnek alır hello adlı VM için disk bilgileri `myVM` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2c21e-130">hello following example gets disk information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

<span data-ttu-id="2c21e-131">Merhaba URI benzer çok**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span><span class="sxs-lookup"><span data-stu-id="2c21e-131">hello URI is similar too**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span></span>

## <a name="delete-existing-vm"></a><span data-ttu-id="2c21e-132">Var olan VM silme</span><span class="sxs-lookup"><span data-stu-id="2c21e-132">Delete existing VM</span></span>
<span data-ttu-id="2c21e-133">Sanal sabit diskler ve sanal makineler Azure'da iki ayrı kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="2c21e-133">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="2c21e-134">Bir sanal sabit disk hello işletim sisteminin kendisi, uygulamalar ve yapılandırmalar depolandığı ' dir.</span><span class="sxs-lookup"><span data-stu-id="2c21e-134">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="2c21e-135">Merhaba VM kendisini hello boyutunu veya konumunu tanımlar ve bir sanal sabit disk veya sanal ağ arabirim kartı (NIC) gibi kaynakları başvuran meta verilerdir.</span><span class="sxs-lookup"><span data-stu-id="2c21e-135">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="2c21e-136">Her sanal sabit diske bağlı olduğunda atanmış bir kira sahip tooa VM.</span><span class="sxs-lookup"><span data-stu-id="2c21e-136">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="2c21e-137">Veri diskleri bağlı ve hatta hello VM çalışırken ayrılmış olsa da, hello VM kaynak silinmedikçe hello işletim sistemi diski ayrılamıyor.</span><span class="sxs-lookup"><span data-stu-id="2c21e-137">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="2c21e-138">Bu VM durduruldu ve deallocated durumda olduğunda bile hello kira tooassociate hello işletim sistemi diski bir VM ile devam eder.</span><span class="sxs-lookup"><span data-stu-id="2c21e-138">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="2c21e-139">İlk adım toorecover hello VM toodelete hello VM kendisini kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="2c21e-139">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="2c21e-140">Silme hello VM hello sanal sabit diskleri depolama hesabınızdaki bırakır.</span><span class="sxs-lookup"><span data-stu-id="2c21e-140">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="2c21e-141">Merhaba, VM silinmiş sonra hello sanal sabit disk tooanother VM tootroubleshoot ekleme ve hello hataları çözümleyin.</span><span class="sxs-lookup"><span data-stu-id="2c21e-141">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="2c21e-142">Sil VM ile Merhaba [az vm silme](/cli/azure/vm#delete).</span><span class="sxs-lookup"><span data-stu-id="2c21e-142">Delete hello VM with [az vm delete](/cli/azure/vm#delete).</span></span> <span data-ttu-id="2c21e-143">Aşağıdaki örnek siler hello hello adlı VM `myVM` adlı hello kaynak grubundan `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2c21e-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="2c21e-144">Merhaba VM hello sanal sabit disk tooanother VM eklemeden önce silme tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="2c21e-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="2c21e-145">Merhaba kira hello sanal sabit diskte hello VM ile ilişkilendiren hello sanal sabit disk tooanother VM iliştirebilirsiniz önce yayınlanan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c21e-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="2c21e-146">Var olan sanal sabit disk tooanother VM ekleme</span><span class="sxs-lookup"><span data-stu-id="2c21e-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="2c21e-147">Sonraki birkaç adımda için Merhaba, sorun giderme amacıyla başka bir VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="2c21e-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="2c21e-148">VM toobrowse sorun giderme hello varolan sanal sabit disk toothis ekleme ve hello diskin içeriği düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="2c21e-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="2c21e-149">Bu işlem toocorrect sağlar herhangi bir yapılandırma hataları veya gözden geçirme ek uygulama veya sistem günlük dosyaları, örneğin.</span><span class="sxs-lookup"><span data-stu-id="2c21e-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="2c21e-150">Seçin veya sorun giderme amacıyla başka bir VM toouse oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2c21e-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="2c21e-151">Merhaba var olan sanal sabit disk ekleme [az vm yönetilmeyen disk ekleme](/cli/azure/vm/unmanaged-disk#attach).</span><span class="sxs-lookup"><span data-stu-id="2c21e-151">Attach hello existing virtual hard disk with [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span></span> <span data-ttu-id="2c21e-152">Merhaba varolan bir sanal sabit diski taktığınızda hello URI toohello disk hello önceki elde belirtin `az vm show` komutu.</span><span class="sxs-lookup"><span data-stu-id="2c21e-152">When you attach hello existing virtual hard disk, specify hello URI toohello disk obtained in hello preceding `az vm show` command.</span></span> <span data-ttu-id="2c21e-153">Merhaba aşağıdaki örnek iliştirir adlı VM sorun giderme var olan bir sanal sabit disk toohello `myVMRecovery` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2c21e-153">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="2c21e-154">Merhaba bağlı veri diski bağlama</span><span class="sxs-lookup"><span data-stu-id="2c21e-154">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="2c21e-155">Merhaba Aşağıdaki örnekler bir Ubuntu VM gerekli hello adımları ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2c21e-155">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="2c21e-156">Red Hat Enterprise Linux veya SUSE, gibi farklı Linux distro kullanıyorsanız hello günlük dosyası konumları ve `mount` komutları biraz farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="2c21e-156">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="2c21e-157">Belirli distro hello uygun değişiklikleri komutları için toohello belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="2c21e-157">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="2c21e-158">SSH tooyour VM Hello uygun kimlik bilgilerini kullanarak sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="2c21e-158">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="2c21e-159">Bu disk VM sorun giderme hello ilk veri bağlı disk tooyour ise, hello disk büyük olasılıkla çok bağlı`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="2c21e-159">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="2c21e-160">Kullanım `dmseg` tooview bağlı diskler:</span><span class="sxs-lookup"><span data-stu-id="2c21e-160">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="2c21e-161">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="2c21e-161">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="2c21e-162">Örnek önceki hello hello işletim sistemi disk altındadır `/dev/sda` ve hello geçici disk, her VM için belirtilen `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="2c21e-162">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="2c21e-163">Birden fazla veri diski varsa, bunlar adresindeki olmalıdır `/dev/sdd`, `/dev/sde`ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="2c21e-163">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="2c21e-164">Bir dizin toomount, varolan bir sanal sabit diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2c21e-164">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="2c21e-165">Merhaba aşağıdaki örnek adlı bir dizin oluşturur `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="2c21e-165">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="2c21e-166">Var olan sanal sabit diskin birden çok bölüm varsa, gerekli hello bölüm bağlayın.</span><span class="sxs-lookup"><span data-stu-id="2c21e-166">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="2c21e-167">Merhaba aşağıdaki örnek bağlar hello ilk birincil bölüm adresindeki `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="2c21e-167">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="2c21e-168">Evrensel benzersiz tanımlayıcı (UUID) hello sanal sabit disk kullanarak Azure'daki sanal makineleri üzerinde toomount veri diskleri hello en iyi uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="2c21e-168">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="2c21e-169">Bu kısa sorun giderme senaryosu için bağlama hello sanal sabit disk hello UUID kullanarak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="2c21e-169">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="2c21e-170">Bununla birlikte, normal kullanım altında düzenleme `/etc/fstab` toomount sanal sabit diskleri yerine UUID neden olabilir, aygıt adı kullanılarak hello VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="2c21e-170">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="2c21e-171">Özgün sanal sabit diskinde ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="2c21e-171">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="2c21e-172">Merhaba varolan bir sanal sabit takılı diski ile tüm bakım ve sorun giderme adımları gereken şekilde artık gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c21e-172">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="2c21e-173">Merhaba sorunlar ele sonra aşağıdaki adımları hello ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="2c21e-173">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="2c21e-174">Çıkarın ve özgün sanal sabit disk ayırma</span><span class="sxs-lookup"><span data-stu-id="2c21e-174">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="2c21e-175">Hatalarınızı çözüldükten sonra çıkarın ve sorun giderme VM'den hello varolan sanal sabit disk ayırma.</span><span class="sxs-lookup"><span data-stu-id="2c21e-175">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="2c21e-176">VM sorun giderme hello sanal sabit disk toohello ekleme hello kira serbest kadar herhangi bir VM ile sanal sabit disk kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="2c21e-176">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="2c21e-177">SSH oturumu tooyour VM sorun giderme hello hello varolan bir sanal sabit diski çıkarın.</span><span class="sxs-lookup"><span data-stu-id="2c21e-177">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="2c21e-178">Merhaba ana dizin, bağlama noktası için dışında ilk değiştirin:</span><span class="sxs-lookup"><span data-stu-id="2c21e-178">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="2c21e-179">Şimdi hello varolan bir sanal sabit diski çıkarın.</span><span class="sxs-lookup"><span data-stu-id="2c21e-179">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="2c21e-180">Merhaba aşağıdaki örnek çıkarır hello aygıt `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="2c21e-180">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="2c21e-181">Şimdi hello VM hello sanal sabit diski kullanımdan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="2c21e-181">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="2c21e-182">VM sorun giderme hello SSH oturumu tooyour çıkın.</span><span class="sxs-lookup"><span data-stu-id="2c21e-182">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="2c21e-183">Liste hello bağlı VM ile sorun giderme veri diskleri tooyour [az vm yönetilmeyen disk listesi](/cli/azure/vm/unmanaged-disk#list).</span><span class="sxs-lookup"><span data-stu-id="2c21e-183">List hello attached data disks tooyour troubleshooting VM with [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span></span> <span data-ttu-id="2c21e-184">Merhaba listeleri hello veri diskleri aşağıdaki örnek bağlı toohello adlı VM `myVMRecovery` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2c21e-184">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    <span data-ttu-id="2c21e-185">Var olan sanal sabit diskinizin Hello adını not edin.</span><span class="sxs-lookup"><span data-stu-id="2c21e-185">Note hello name for your existing virtual hard disk.</span></span> <span data-ttu-id="2c21e-186">Örneğin, bir diskle hello adını hello URI'sini **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** olan **myVHD**.</span><span class="sxs-lookup"><span data-stu-id="2c21e-186">For example, hello name of a disk with hello URI of **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span></span> 

    <span data-ttu-id="2c21e-187">VM Hello veri diski kullanımdan çıkarın [yönetilmeyen az vm-disk ayırma](/cli/azure/vm/unmanaged-disk#detach).</span><span class="sxs-lookup"><span data-stu-id="2c21e-187">Detach hello data disk from your VM [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span></span> <span data-ttu-id="2c21e-188">Merhaba aşağıdaki örnek ayırır adlı hello disk `myVHD` hello adlı VM gelen `myVMRecovery` hello içinde `myResourceGroup` kaynak grubu:</span><span class="sxs-lookup"><span data-stu-id="2c21e-188">hello following example detaches hello disk named `myVHD` from hello VM named `myVMRecovery` in hello `myResourceGroup` resource group:</span></span>

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="2c21e-189">Özgün sabit diskten VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="2c21e-189">Create VM from original hard disk</span></span>
<span data-ttu-id="2c21e-190">bir VM, özgün sanal sabit diskten toocreate kullanmak [bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="2c21e-190">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="2c21e-191">Merhaba gerçek JSON şablon bağlantıyı izleyerek hello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="2c21e-191">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="2c21e-192">https://RAW.githubusercontent.com/Azure/Azure-QuickStart-Templates/master/201-VM-Specialized-VHD/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="2c21e-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="2c21e-193">Merhaba şablon dağıtır hello VHD URİ'si hello gelen kullanarak bir VM'i önceki komutu.</span><span class="sxs-lookup"><span data-stu-id="2c21e-193">hello template deploys a VM using hello VHD URI from hello earlier command.</span></span> <span data-ttu-id="2c21e-194">Merhaba şablonla dağıtmak [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="2c21e-194">Deploy hello template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="2c21e-195">Merhaba URI tooyour sağlamak özgün VHD hello işletim sistemi türü, VM boyutu ve VM adı aşağıdaki gibi belirtin:</span><span class="sxs-lookup"><span data-stu-id="2c21e-195">Provide hello URI tooyour original VHD and then specify hello OS type, VM size, and VM name as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="2c21e-196">Önyükleme tanılaması yeniden etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="2c21e-196">Re-enable boot diagnostics</span></span>
<span data-ttu-id="2c21e-197">Merhaba varolan sanal sabit diskten VM'nizi oluşturduğunuzda, önyükleme tanılaması otomatik olarak etkinleştirilmemiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="2c21e-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="2c21e-198">Önyükleme Tanılaması ile etkinleştirmek [az vm önyükleme-tanılamayı etkinleştirin](/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="2c21e-198">Enable boot diagnostics with [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="2c21e-199">Merhaba aşağıdaki örnek hello tanılama uzantısını hello adlı VM üzerinde etkinleştirir `myDeployedVM` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2c21e-199">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="2c21e-200">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2c21e-200">Next steps</span></span>
<span data-ttu-id="2c21e-201">Tooyour VM bağlantı sorunları yaşıyorsanız, bkz: [sorun giderme SSH bağlantıları tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c21e-201">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="2c21e-202">VM üzerinde çalışan uygulamalara erişim sorunları için bkz: [bir Linux VM üzerinde uygulama bağlantı sorunlarını giderme](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c21e-202">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
