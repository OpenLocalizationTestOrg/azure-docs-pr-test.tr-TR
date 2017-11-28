---
title: Bir Linux VM Azure CLI 1.0 ile sorun giderme kullanma | Microsoft Docs
description: "Kurtarma için Azure CLI 1.0 kullanarak VM işletim sistemi diski bağlanarak Linux VM sorunlarını giderme hakkında bilgi edinin"
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
ms.openlocfilehash: d817358211f123c96d899c5cff88cc47aeb5c9c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-the-azure-cli-10"></a><span data-ttu-id="db2b8-103">Bir Linux VM kurtarma Azure CLI 1.0 kullanarak VM için işletim sistemi diski ekleyerek sorun giderme</span><span class="sxs-lookup"><span data-stu-id="db2b8-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="db2b8-104">Linux sanal makine (VM) önyükleme veya disk bir hatayla karşılaştığında, sanal sabit diskin kendisinde sorun giderme adımları gerçekleştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="db2b8-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="db2b8-105">Geçersiz bir giriş yaygın bir örnek olacaktır `/etc/fstab` engelleyen VM başarıyla önyükleme yapamamasına.</span><span class="sxs-lookup"><span data-stu-id="db2b8-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="db2b8-106">Bu makalede Azure CLI 1.0, sanal sabit diski başka bir Linux hataları düzeltin, sonra özgün VM'yi yeniden oluşturmak için VM'e bağlanmak için nasıl kullanılacağını ayrıntılarını verir.</span><span class="sxs-lookup"><span data-stu-id="db2b8-106">This article details how to use the Azure CLI 1.0 to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="db2b8-107">Görevi tamamlamak için kullanılacak CLI sürümleri</span><span class="sxs-lookup"><span data-stu-id="db2b8-107">CLI versions to complete the task</span></span>
<span data-ttu-id="db2b8-108">Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="db2b8-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="db2b8-109">[Azure CLI 1.0](#recovery-process-overview) – bizim CLI Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="db2b8-109">[Azure CLI 1.0](#recovery-process-overview) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="db2b8-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): Kaynak yönetimi dağıtım modeline yönelik yeni nesil CLI'mız</span><span class="sxs-lookup"><span data-stu-id="db2b8-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="db2b8-111">Kurtarma işlemine genel bakış</span><span class="sxs-lookup"><span data-stu-id="db2b8-111">Recovery process overview</span></span>
<span data-ttu-id="db2b8-112">Sorun giderme işlemi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="db2b8-112">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="db2b8-113">Sorunlarla, sanal sabit diskleri tutmak VM silin.</span><span class="sxs-lookup"><span data-stu-id="db2b8-113">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="db2b8-114">Ekleme ve sorun giderme amacıyla başka bir Linux VM sanal sabit diski bağlayın.</span><span class="sxs-lookup"><span data-stu-id="db2b8-114">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="db2b8-115">Sorun giderme işlemlerini yapacağınız VM'ye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="db2b8-115">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="db2b8-116">Dosyaları düzenleyin veya özgün sanal sabit diskte sorunlarını gidermek için herhangi bir aracı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="db2b8-116">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="db2b8-117">Sorun giderme işlemlerini yaptığınız VM’den sanal sabit diski çıkarın.</span><span class="sxs-lookup"><span data-stu-id="db2b8-117">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="db2b8-118">Özgün sanal sabit disk kullanan bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="db2b8-118">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="db2b8-119">Bilgisayarınızda yüklü olduğundan emin olun [en son Azure CLI 1.0](../../cli-install-nodejs.md) yüklü ve oturum açmış ve Resource Manager modunu kullanma:</span><span class="sxs-lookup"><span data-stu-id="db2b8-119">Make sure that you have [the latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="db2b8-120">Aşağıdaki örneklerde, parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="db2b8-120">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="db2b8-121">Örnek parametre adlarında `myResourceGroup`, `mystorageaccount`, ve `myVM`.</span><span class="sxs-lookup"><span data-stu-id="db2b8-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="db2b8-122">Önyükleme sorunlarını belirleme</span><span class="sxs-lookup"><span data-stu-id="db2b8-122">Determine boot issues</span></span>
<span data-ttu-id="db2b8-123">Neden VM'yi doğru önyükleme mümkün değil belirlemek için seri çıktıyı inceleyin.</span><span class="sxs-lookup"><span data-stu-id="db2b8-123">Examine the serial output to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="db2b8-124">Yaygın bir örnek, geçersiz bir giriş olduğunu `/etc/fstab`, ya da temel sanal silindiğinde veya taşındığında disk.</span><span class="sxs-lookup"><span data-stu-id="db2b8-124">A common example is an invalid entry in `/etc/fstab`, or the underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="db2b8-125">Aşağıdaki örnek adlı VM'den seri çıktısını alır `myVM` kaynak grubunda adlı `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="db2b8-125">The following example gets the serial output from the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="db2b8-126">VM önyükleme neden başarısız olduğunu belirlemek için seri çıkış gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="db2b8-126">Review the serial output to determine why the VM is failing to boot.</span></span> <span data-ttu-id="db2b8-127">Seri çıkış herhangi bir gösterge sağlayan değil, günlük dosyalarını inceleyin gerekebilir `/var/log` sorun giderme bir VM öğesine bağlı sanal sabit diske sahip olduğunda.</span><span class="sxs-lookup"><span data-stu-id="db2b8-127">If the serial output isn't providing any indication, you may need to review log files in `/var/log` once you have the virtual hard disk connected to a troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="db2b8-128">Var olan sanal sabit disk ayrıntılarını görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="db2b8-128">View existing virtual hard disk details</span></span>
<span data-ttu-id="db2b8-129">Sanal sabit disk için başka bir VM iliştirebilirsiniz önce sanal sabit disk (VHD) adını tanımlamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="db2b8-129">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span> 

<span data-ttu-id="db2b8-130">Aşağıdaki örnek adlı VM için bilgilerini alır `myVM` kaynak grubunda adlı `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="db2b8-130">The following example gets information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="db2b8-131">Ara `Vhd URI` yukarıdaki komut çıktısı olarak.</span><span class="sxs-lookup"><span data-stu-id="db2b8-131">Look for `Vhd URI` in the output from the preceding command.</span></span> <span data-ttu-id="db2b8-132">Aşağıdaki örnek çıktısında kesilmiş `Vhd URI` son satırında:</span><span class="sxs-lookup"><span data-stu-id="db2b8-132">The following truncated example output shows the `Vhd URI` on the last line:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "myVM"
+ Looking up the NIC "myNic"
+ Looking up the public ip "myPublicIP"
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


## <a name="delete-existing-vm"></a><span data-ttu-id="db2b8-133">Var olan VM silme</span><span class="sxs-lookup"><span data-stu-id="db2b8-133">Delete existing VM</span></span>
<span data-ttu-id="db2b8-134">Sanal sabit diskler ve sanal makineler Azure'da iki ayrı kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="db2b8-134">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="db2b8-135">Bir sanal sabit disk, işletim sisteminin kendisi, uygulamalar ve yapılandırmalar depolandığı ' dir.</span><span class="sxs-lookup"><span data-stu-id="db2b8-135">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="db2b8-136">VM boyutunu veya konumunu tanımlar ve bir sanal sabit disk veya sanal ağ arabirim kartı (NIC) gibi kaynakları başvuran meta verilerdir.</span><span class="sxs-lookup"><span data-stu-id="db2b8-136">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="db2b8-137">Her sanal sabit disk için bir VM eklendiğinde atanmış bir kira var.</span><span class="sxs-lookup"><span data-stu-id="db2b8-137">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="db2b8-138">Veri diskleri VM çalışırken bile eklenip çıkarılabilir, ancak VM kaynağı silinmedikçe işletim sistemi diski çıkarılamaz.</span><span class="sxs-lookup"><span data-stu-id="db2b8-138">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="db2b8-139">Bu VM durduruldu ve deallocated durumda olduğunda bile işletim sistemi diski bir VM ile ilişkilendirilecek kira sürdürür.</span><span class="sxs-lookup"><span data-stu-id="db2b8-139">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="db2b8-140">VM kurtarmak için ilk adım, VM kaynak silmektir.</span><span class="sxs-lookup"><span data-stu-id="db2b8-140">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="db2b8-141">VM’yi sildiğinizde sanal sabit diskler depolama hesabınızda kalır.</span><span class="sxs-lookup"><span data-stu-id="db2b8-141">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="db2b8-142">VM silindikten sonra sanal sabit diski ve hataları gidermek için başka bir VM'e ekleyin.</span><span class="sxs-lookup"><span data-stu-id="db2b8-142">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="db2b8-143">Aşağıdaki örnek adlı VM siler `myVM` kaynak grubundan adlı `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="db2b8-143">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="db2b8-144">VM için başka bir VM sanal sabit disk eklemeden önce silme tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="db2b8-144">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="db2b8-145">VM ile ilişkilendirir sanal sabit disk üzerindeki kira süresini sanal sabit disk için başka bir VM eklemeden önce yayımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="db2b8-145">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="db2b8-146">Varolan bir sanal sabit diski başka bir VM'e ekleyin</span><span class="sxs-lookup"><span data-stu-id="db2b8-146">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="db2b8-147">Sonraki birkaç adımda için sorun giderme amacıyla başka bir VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="db2b8-147">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="db2b8-148">Varolan bir sanal sabit diski bulun ve diskin içeriği düzenlemek için sorun giderme bu VM'e ekleyin.</span><span class="sxs-lookup"><span data-stu-id="db2b8-148">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="db2b8-149">Bu işlem, yapılandırma hataları düzeltin ya da ek uygulama veya sistem günlük dosyalarını, örneğin gözden olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="db2b8-149">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="db2b8-150">Seçin veya sorun giderme amacıyla kullanmak için başka bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="db2b8-150">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="db2b8-151">Varolan bir sanal sabit diski taktığınızda, önceki elde disk URL'yi belirtmek `azure vm show` komutu.</span><span class="sxs-lookup"><span data-stu-id="db2b8-151">When you attach the existing virtual hard disk, specify the URL to the disk obtained in the preceding `azure vm show` command.</span></span> <span data-ttu-id="db2b8-152">Aşağıdaki örnek sorun giderme VM adlı varolan bir sanal sabit diski iliştirir `myVMRecovery` kaynak grubunda adlı `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="db2b8-152">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="db2b8-153">Bağlı veri diski bağlama</span><span class="sxs-lookup"><span data-stu-id="db2b8-153">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="db2b8-154">Aşağıdaki örnekler bir Ubuntu VM gerekli adımları ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="db2b8-154">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="db2b8-155">Red Hat Enterprise Linux veya SUSE, gibi farklı Linux distro kullanıyorsanız, günlük dosyası konumları ve `mount` komutları biraz farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="db2b8-155">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="db2b8-156">Komutları uygun değişiklikleri, belirli distro belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="db2b8-156">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="db2b8-157">SSH uygun kimlik bilgilerini kullanarak, sorun giderme VM.</span><span class="sxs-lookup"><span data-stu-id="db2b8-157">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="db2b8-158">Bu disk, sorun giderme VM'ye ekli ilk veri diski olduğundan, diskin büyük olasılıkla bağlı `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="db2b8-158">If this disk is the first data disk attached to your troubleshooting VM, the disk is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="db2b8-159">Kullanım `dmseg` bağlı disklerde görüntülemek için:</span><span class="sxs-lookup"><span data-stu-id="db2b8-159">Use `dmseg` to view attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="db2b8-160">Çıktı aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="db2b8-160">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="db2b8-161">Önceki örnekte, işletim sistemi diski altındadır `/dev/sda` ve her bir VM altındadır için sağlanan geçici disk `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="db2b8-161">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="db2b8-162">Birden fazla veri diski varsa, bunlar adresindeki olmalıdır `/dev/sdd`, `/dev/sde`ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="db2b8-162">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="db2b8-163">Varolan bir sanal sabit diski bağlamak için bir dizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="db2b8-163">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="db2b8-164">Aşağıdaki örnek adlı bir dizin oluşturur `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="db2b8-164">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="db2b8-165">Var olan sanal sabit diskin birden çok bölüm varsa, gerekli bir bölüm bağlayın.</span><span class="sxs-lookup"><span data-stu-id="db2b8-165">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="db2b8-166">Aşağıdaki örnekte, ilk birincil bölüm bağlar `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="db2b8-166">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="db2b8-167">Veri diskleri sanal sabit disk evrensel benzersiz tanımlayıcı (UUID) kullanarak Azure vm'lerinde bağlamak en iyi uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="db2b8-167">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="db2b8-168">Sanal sabit disk UUID'si kullanılarak bağlanması özelliği bu kısa sorun giderme senaryo için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="db2b8-168">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="db2b8-169">Bununla birlikte, normal kullanım altında düzenleme `/etc/fstab` sanal sabit diskler bağlayın UUID yerine aygıt adını kullanarak VM önyükleme başarısız olmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="db2b8-169">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="db2b8-170">Özgün sanal sabit diskinde ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="db2b8-170">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="db2b8-171">Varolan bir sanal sabit takılı diski ile tüm bakım ve sorun giderme adımları gereken şekilde artık gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db2b8-171">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="db2b8-172">Sorunları giderdikten sonra aşağıdaki adımlarla devam edin.</span><span class="sxs-lookup"><span data-stu-id="db2b8-172">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="db2b8-173">Çıkarın ve özgün sanal sabit disk ayırma</span><span class="sxs-lookup"><span data-stu-id="db2b8-173">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="db2b8-174">Hatalarınızı çözüldükten sonra çıkarın ve varolan bir sanal sabit diski, sorun giderme sanal makineden ayırın.</span><span class="sxs-lookup"><span data-stu-id="db2b8-174">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="db2b8-175">Sorun giderme VM için sanal sabit disk ekleme kira serbest kadar herhangi bir VM ile sanal sabit disk kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="db2b8-175">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="db2b8-176">Sorun giderme VM için SSH oturumundan varolan bir sanal sabit diski çıkarın.</span><span class="sxs-lookup"><span data-stu-id="db2b8-176">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="db2b8-177">Bağlama noktası üst dizini dışında ilk değiştirin:</span><span class="sxs-lookup"><span data-stu-id="db2b8-177">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="db2b8-178">Şimdi varolan bir sanal sabit diski çıkarın.</span><span class="sxs-lookup"><span data-stu-id="db2b8-178">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="db2b8-179">Aşağıdaki örnek konumunda aygıttan çıkarır `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="db2b8-179">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="db2b8-180">Şimdi VM sanal sabit diski kullanımdan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="db2b8-180">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="db2b8-181">SSH oturumu sorun giderme VM'nize çıkın.</span><span class="sxs-lookup"><span data-stu-id="db2b8-181">Exit the SSH session to your troubleshooting VM.</span></span> <span data-ttu-id="db2b8-182">Azure CLI ilk sorun giderme VM eklenen veri disklerini listeleyin.</span><span class="sxs-lookup"><span data-stu-id="db2b8-182">In the Azure CLI, first list the attached data disks to your troubleshooting VM.</span></span> <span data-ttu-id="db2b8-183">Aşağıdaki örnek adlı VM'ye bağlı veri disklerinden listeler `myVMRecovery` kaynak grubunda adlı `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="db2b8-183">The following example lists the data disks attached to the VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    <span data-ttu-id="db2b8-184">Not `Lun` , varolan bir sanal sabit disk için değer.</span><span class="sxs-lookup"><span data-stu-id="db2b8-184">Note the `Lun` value for your existing virtual hard disk.</span></span> <span data-ttu-id="db2b8-185">Aşağıdaki örnek komut çıktısı bağlı LUN 0 varolan bir sanal disk gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="db2b8-185">The following example command output shows the existing virtual disk attached at LUN 0:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Looking up the VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    <span data-ttu-id="db2b8-186">Geçerli kullanarak VM veri diski kullanımdan çıkarın `Lun` değeri:</span><span class="sxs-lookup"><span data-stu-id="db2b8-186">Detach the data disk from your VM using the applicable `Lun` value:</span></span>

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="db2b8-187">Özgün sabit diskten VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="db2b8-187">Create VM from original hard disk</span></span>
<span data-ttu-id="db2b8-188">Özgün sanal sabit diskten bir VM oluşturmak için kullanmak [bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="db2b8-188">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="db2b8-189">Gerçek JSON şablon aşağıdaki bağlantıda şöyledir:</span><span class="sxs-lookup"><span data-stu-id="db2b8-189">The actual JSON template is at the following link:</span></span>

- <span data-ttu-id="db2b8-190">https://RAW.githubusercontent.com/Azure/Azure-QuickStart-Templates/master/201-VM-Specialized-VHD/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="db2b8-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="db2b8-191">Önceki komutu VHD URL'yi kullanarak mevcut sanal ağda, bir VM şablonu dağıtır.</span><span class="sxs-lookup"><span data-stu-id="db2b8-191">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="db2b8-192">Aşağıdaki örnek adlı kaynak grubunu şablon dağıtır `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="db2b8-192">The following example deploys the template to the resource group named `myResourceGroup`:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

<span data-ttu-id="db2b8-193">VM adı gibi şablonu için istemleri yanıt (`myDeployedVM` aşağıdaki örnek), işletim sistemi türü (`Linux`) ve VM boyutu (`Standard_DS1_v2`).</span><span class="sxs-lookup"><span data-stu-id="db2b8-193">Answer the prompts for the template such as VM name (`myDeployedVM` the following example), OS type (`Linux`), and VM size (`Standard_DS1_v2`).</span></span> <span data-ttu-id="db2b8-194">`osDiskVhdUri` Daha önce kullanıldığında aynı varolan bir sanal sabit diski sorun giderme VM'ye ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="db2b8-194">The `osDiskVhdUri` is the same as previously used when attaching the existing virtual hard disk to the troubleshooting VM.</span></span> <span data-ttu-id="db2b8-195">Komut çıktısı ve istemleri örneği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="db2b8-195">An example of the command output and prompts is as follows:</span></span>

```azurecli
info:    Executing command group deployment create
info:    Supply values for the following parameters
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
+ Waiting for deployment to complete
+
```


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="db2b8-196">Önyükleme tanılaması yeniden etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="db2b8-196">Re-enable boot diagnostics</span></span>

<span data-ttu-id="db2b8-197">Var olan sanal sabit diskten VM'nizi oluşturduğunuzda, önyükleme tanılaması otomatik olarak etkinleştirilmemiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="db2b8-197">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="db2b8-198">Aşağıdaki örnek adlı VM'de tanılama uzantısını etkinleştirir `myDeployedVM` kaynak grubunda adlı `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="db2b8-198">The following example enables the diagnostic extension on the VM named `myDeployedVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="db2b8-199">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="db2b8-199">Next steps</span></span>
<span data-ttu-id="db2b8-200">VM'nize bağlantı sorunları yaşıyorsanız, bkz: [sorun giderme SSH bağlantıları bir Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="db2b8-200">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="db2b8-201">VM üzerinde çalışan uygulamalara erişim sorunları için bkz: [bir Linux VM üzerinde uygulama bağlantı sorunlarını giderme](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="db2b8-201">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>