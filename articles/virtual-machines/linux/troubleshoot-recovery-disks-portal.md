---
title: "bir Linux VM hello Azure portal sorunlarını giderme aaaUse | Microsoft Docs"
description: "Azure portal kullanarak bağlanan hello işletim sistemi disk tooa kurtarma VM tootroubleshoot Linux sanal makine sorunlarını nasıl hello öğrenin"
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
ms.date: 11/14/2016
ms.author: iainfou
ms.openlocfilehash: 794daa06d7436215af84a61ab9088524254c47df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a><span data-ttu-id="91abf-103">Bir Linux VM hello işletim sistemi disk tooa kurtarma VM ekleyerek sorun giderme hello Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="91abf-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure portal</span></span>
<span data-ttu-id="91abf-104">Linux sanal makine (VM) önyükleme veya disk bir hatayla karşılaştığında, sorun giderme adımları hello sanal sabit diske kendisini tooperform gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="91abf-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="91abf-105">Geçersiz bir giriş yaygın bir örnek olacaktır `/etc/fstab` engelleyen hello VM mümkün tooboot başarıyla bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="91abf-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="91abf-106">Bu makale ayrıntıları toouse hello nasıl Azure portal tooconnect, sanal sabit hataları tooanother Linux VM toofix disk sonra özgün VM'yi yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="91abf-106">This article details how toouse hello Azure portal tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="91abf-107">Kurtarma işlemine genel bakış</span><span class="sxs-lookup"><span data-stu-id="91abf-107">Recovery process overview</span></span>
<span data-ttu-id="91abf-108">sorun giderme işlemi hello aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="91abf-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="91abf-109">Merhaba sanal sabit diskleri tutmak hello VM karşılaşmadan sorunları, silin.</span><span class="sxs-lookup"><span data-stu-id="91abf-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="91abf-110">Ekleme ve sorun giderme amacıyla hello sanal sabit disk tooanother Linux VM bağlayın.</span><span class="sxs-lookup"><span data-stu-id="91abf-110">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="91abf-111">VM sorun giderme toohello bağlayın.</span><span class="sxs-lookup"><span data-stu-id="91abf-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="91abf-112">Dosyaları düzenleyin veya herhangi bir aracı toofix sorunları hello özgün sanal sabit disk üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="91abf-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="91abf-113">Çıkarın ve VM sorun giderme hello hello sanal sabit diski kullanımdan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="91abf-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="91abf-114">Merhaba özgün sanal sabit disk kullanan bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="91abf-114">Create a VM using hello original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="91abf-115">Önyükleme sorunlarını belirleme</span><span class="sxs-lookup"><span data-stu-id="91abf-115">Determine boot issues</span></span>
<span data-ttu-id="91abf-116">Merhaba önyükleme tanılaması ve neden, VM mümkün tooboot doğru değil VM ekran toodetermine inceleyin.</span><span class="sxs-lookup"><span data-stu-id="91abf-116">Examine hello boot diagnostics and VM screenshot toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="91abf-117">Geçersiz bir giriş yaygın bir örnek olacaktır `/etc/fstab`, veya bir temel sanal sabit silindiğinde veya taşındığında disk.</span><span class="sxs-lookup"><span data-stu-id="91abf-117">A common example would be an invalid entry in `/etc/fstab`, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="91abf-118">Merhaba Portalı'nda, VM seçin ve ardından toohello kaydırın **destek + sorun giderme** bölümü.</span><span class="sxs-lookup"><span data-stu-id="91abf-118">Select your VM in hello portal and then scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="91abf-119">Tıklatın **önyükleme tanılama** tooview hello konsol iletileri, VM'den akışı.</span><span class="sxs-lookup"><span data-stu-id="91abf-119">Click **Boot diagnostics** tooview hello console messages streamed from your VM.</span></span> <span data-ttu-id="91abf-120">Neden hello VM bir sorunla karşılaşan karar verirseniz gözden geçirme hello konsol toosee günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="91abf-120">Review hello console logs toosee if you can determine why hello VM is encountering an issue.</span></span> <span data-ttu-id="91abf-121">Merhaba aşağıdaki örnekte bir VM el ile etkileşimi gerektiren bakım moduna takılmış gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="91abf-121">hello following example shows a VM stuck in maintenance mode that requires manual interaction:</span></span>

![Önyükleme tanılaması konsol günlükleri VM görüntüleme](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

<span data-ttu-id="91abf-123">Tıklatarak **ekran** hello önyükleme tanılama günlük toodownload hello VM ekran yakalama hello üstte.</span><span class="sxs-lookup"><span data-stu-id="91abf-123">You can also click **Screenshot** across hello top of hello boot diagnostics log toodownload a capture of hello VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="91abf-124">Var olan sanal sabit disk ayrıntılarını görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="91abf-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="91abf-125">Sanal sabit disk tooanother VM ekleyebilmek için tooidentify hello adı hello sanal sabit disk (VHD) gerekir.</span><span class="sxs-lookup"><span data-stu-id="91abf-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="91abf-126">Merhaba portalından, bir kaynak grubunu seçin, sonra depolama hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="91abf-126">Select your resource group from hello portal, then select your storage account.</span></span> <span data-ttu-id="91abf-127">Tıklatın **BLOB'lar**, aşağıdaki örneğine hello olarak:</span><span class="sxs-lookup"><span data-stu-id="91abf-127">Click **Blobs**, as in hello following example:</span></span>

![Depolama BLOB'ları seçin](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="91abf-129">Adlı bir kapsayıcıya sahip genellikle **VHD'ler** sanal sabit disklerinizi depolar.</span><span class="sxs-lookup"><span data-stu-id="91abf-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="91abf-130">Merhaba kapsayıcı tooview sanal sabit disklerin listesini seçin.</span><span class="sxs-lookup"><span data-stu-id="91abf-130">Select hello container tooview a list of virtual hard disks.</span></span> <span data-ttu-id="91abf-131">Not Merhaba, VHD adını (Merhaba önekidir genellikle VM hello adı):</span><span class="sxs-lookup"><span data-stu-id="91abf-131">Note hello name of your VHD (hello prefix is usually hello name of your VM):</span></span>

![Depolama kapsayıcısı VHD tanımlayın](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="91abf-133">Merhaba listeden, varolan bir sanal sabit diski seçin ve hello URL'sini kullanmak için aşağıdaki adımları hello kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="91abf-133">Select your existing virtual hard disk from hello list and copy hello URL for use in hello following steps:</span></span>

![Var olan sanal sabit disk URL'sini Kopyala](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="91abf-135">Var olan VM silme</span><span class="sxs-lookup"><span data-stu-id="91abf-135">Delete existing VM</span></span>
<span data-ttu-id="91abf-136">Sanal sabit diskler ve sanal makineler Azure'da iki ayrı kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="91abf-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="91abf-137">Bir sanal sabit disk hello işletim sisteminin kendisi, uygulamalar ve yapılandırmalar depolandığı ' dir.</span><span class="sxs-lookup"><span data-stu-id="91abf-137">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="91abf-138">Merhaba VM kendisini hello boyutunu veya konumunu tanımlar ve bir sanal sabit disk veya sanal ağ arabirim kartı (NIC) gibi kaynakları başvuran meta verilerdir.</span><span class="sxs-lookup"><span data-stu-id="91abf-138">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="91abf-139">Her sanal sabit diske bağlı olduğunda atanmış bir kira sahip tooa VM.</span><span class="sxs-lookup"><span data-stu-id="91abf-139">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="91abf-140">Veri diskleri bağlı ve hatta hello VM çalışırken ayrılmış olsa da, hello VM kaynak silinmedikçe hello işletim sistemi diski ayrılamıyor.</span><span class="sxs-lookup"><span data-stu-id="91abf-140">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="91abf-141">Bu VM durduruldu ve deallocated durumda olduğunda bile hello kira tooassociate hello işletim sistemi diski bir VM ile devam eder.</span><span class="sxs-lookup"><span data-stu-id="91abf-141">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="91abf-142">İlk adım toorecover hello VM toodelete hello VM kendisini kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="91abf-142">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="91abf-143">Silme hello VM hello sanal sabit diskleri depolama hesabınızdaki bırakır.</span><span class="sxs-lookup"><span data-stu-id="91abf-143">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="91abf-144">Merhaba, VM silinmiş sonra hello sanal sabit disk tooanother VM tootroubleshoot ekleme ve hello hataları çözümleyin.</span><span class="sxs-lookup"><span data-stu-id="91abf-144">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="91abf-145">Hello Portalı'nda, VM seçin ve ardından **silmek**:</span><span class="sxs-lookup"><span data-stu-id="91abf-145">Select your VM in hello portal, then click **Delete**:</span></span>

![VM önyükleme tanılama önyükleme hatası gösteren ekran görüntüsü](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="91abf-147">Merhaba VM hello sanal sabit disk tooanother VM eklemeden önce silme tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="91abf-147">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="91abf-148">Merhaba kira hello sanal sabit diskte hello VM ile ilişkilendiren hello sanal sabit disk tooanother VM iliştirebilirsiniz önce yayınlanan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="91abf-148">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="91abf-149">Var olan sanal sabit disk tooanother VM ekleme</span><span class="sxs-lookup"><span data-stu-id="91abf-149">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="91abf-150">Sonraki birkaç adımda için Merhaba, sorun giderme amacıyla başka bir VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="91abf-150">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="91abf-151">VM toobe mümkün toobrowse sorun giderme hello varolan sanal sabit disk toothis ekleme ve hello diskin içeriği düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="91abf-151">You attach hello existing virtual hard disk toothis troubleshooting VM toobe able toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="91abf-152">Bu işlem toocorrect sağlar herhangi bir yapılandırma hataları veya gözden geçirme ek uygulama veya sistem günlük dosyaları, örneğin.</span><span class="sxs-lookup"><span data-stu-id="91abf-152">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="91abf-153">Seçin veya sorun giderme amacıyla başka bir VM toouse oluşturun.</span><span class="sxs-lookup"><span data-stu-id="91abf-153">Choose or create another VM toouse for troubleshooting purposes.</span></span>

1. <span data-ttu-id="91abf-154">Merhaba portalından, bir kaynak grubunu seçin, sonra sorun giderme VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="91abf-154">Select your resource group from hello portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="91abf-155">Seçin **diskleri** ve ardından **Attach varolan**:</span><span class="sxs-lookup"><span data-stu-id="91abf-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Merhaba Portalı'nda mevcut diski kullanıma açın](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="91abf-157">tooselect, mevcut sanal sabit diski tıklatın **VHD dosyasını**:</span><span class="sxs-lookup"><span data-stu-id="91abf-157">tooselect your existing virtual hard disk, click **VHD File**:</span></span>

    ![Mevcut bir VHD'ye göz atma](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="91abf-159">Depolama hesabı ve kapsayıcı seçip, varolan bir VHD'Yİ'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="91abf-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="91abf-160">Merhaba tıklatın **seçin** tooconfirm tercih ettiğiniz düğmesi:</span><span class="sxs-lookup"><span data-stu-id="91abf-160">Click hello **Select** button tooconfirm your choice:</span></span>

    ![Mevcut VHD’nizi seçme](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="91abf-162">Artık seçili, VHD ile tıklatın **Tamam** tooattach hello varolan bir sanal sabit disk:</span><span class="sxs-lookup"><span data-stu-id="91abf-162">With your VHD now selected, click **OK** tooattach hello existing virtual hard disk:</span></span>

    ![Varolan bir sanal sabit diski ekleme onaylayın](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="91abf-164">Birkaç saniye sonra hello **diskleri** bölmesi, VM için varolan bir sanal sabit bir veri diski bağlı disk listeler:</span><span class="sxs-lookup"><span data-stu-id="91abf-164">After a few seconds, hello **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Veri diski olarak bağlı olan sanal sabit disk](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="91abf-166">Merhaba bağlı veri diski bağlama</span><span class="sxs-lookup"><span data-stu-id="91abf-166">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="91abf-167">Merhaba Aşağıdaki örnekler bir Ubuntu VM gerekli hello adımları ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="91abf-167">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="91abf-168">Red Hat Enterprise Linux veya SUSE, gibi farklı Linux distro kullanıyorsanız hello günlük dosyası konumları ve `mount` komutları biraz farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="91abf-168">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="91abf-169">Belirli distro hello uygun değişiklikleri komutları için toohello belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="91abf-169">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="91abf-170">SSH tooyour VM Hello uygun kimlik bilgilerini kullanarak sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="91abf-170">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="91abf-171">Bu disk VM sorun giderme hello ilk veri bağlı disk tooyour ise, büyük olasılıkla çok bağlı olduğu`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="91abf-171">If this disk is hello first data disk attached tooyour troubleshooting VM, it is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="91abf-172">Kullanım `dmseg` toolist bağlı diskler:</span><span class="sxs-lookup"><span data-stu-id="91abf-172">Use `dmseg` toolist attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```
    <span data-ttu-id="91abf-173">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="91abf-173">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="91abf-174">Örnek önceki hello hello işletim sistemi disk altındadır `/dev/sda` ve hello geçici disk, her VM için belirtilen `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="91abf-174">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="91abf-175">Birden fazla veri diski varsa, bunlar adresindeki olmalıdır `/dev/sdd`, `/dev/sde`ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="91abf-175">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="91abf-176">Bir dizin toomount, varolan bir sanal sabit diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="91abf-176">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="91abf-177">Merhaba aşağıdaki örnek adlı bir dizin oluşturur `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="91abf-177">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="91abf-178">Var olan sanal sabit diskin birden çok bölüm varsa, gerekli hello bölüm bağlayın.</span><span class="sxs-lookup"><span data-stu-id="91abf-178">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="91abf-179">Merhaba aşağıdaki örnek bağlar hello ilk birincil bölüm adresindeki `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="91abf-179">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="91abf-180">Evrensel benzersiz tanımlayıcı (UUID) hello sanal sabit disk kullanarak Azure'daki sanal makineleri üzerinde toomount veri diskleri hello en iyi uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="91abf-180">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="91abf-181">Bu kısa sorun giderme senaryosu için bağlama hello sanal sabit disk hello UUID kullanarak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="91abf-181">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="91abf-182">Bununla birlikte, normal kullanım altında düzenleme `/etc/fstab` toomount sanal sabit diskleri yerine UUID neden olabilir, aygıt adı kullanılarak hello VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="91abf-182">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="91abf-183">Özgün sanal sabit diskinde ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="91abf-183">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="91abf-184">Merhaba varolan bir sanal sabit takılı diski ile tüm bakım ve sorun giderme adımları gereken şekilde artık gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91abf-184">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="91abf-185">Merhaba sorunlar ele sonra aşağıdaki adımları hello ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="91abf-185">Once you have addressed hello issues, continue with hello following steps.</span></span>

## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="91abf-186">Çıkarın ve özgün sanal sabit disk ayırma</span><span class="sxs-lookup"><span data-stu-id="91abf-186">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="91abf-187">Hatalarınızı çözüldükten sonra hello varolan sanal sabit diskten, sorun giderme VM ayırma.</span><span class="sxs-lookup"><span data-stu-id="91abf-187">Once your errors are resolved, detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="91abf-188">VM sorun giderme hello sanal sabit disk toohello ekleme hello kira serbest kadar herhangi bir VM ile sanal sabit disk kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="91abf-188">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="91abf-189">SSH oturumu tooyour VM sorun giderme hello hello varolan bir sanal sabit diski çıkarın.</span><span class="sxs-lookup"><span data-stu-id="91abf-189">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="91abf-190">Merhaba ana dizin, bağlama noktası için dışında ilk değiştirin:</span><span class="sxs-lookup"><span data-stu-id="91abf-190">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="91abf-191">Şimdi hello varolan bir sanal sabit diski çıkarın.</span><span class="sxs-lookup"><span data-stu-id="91abf-191">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="91abf-192">Merhaba aşağıdaki örnek çıkarır hello aygıt `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="91abf-192">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="91abf-193">Şimdi hello VM hello sanal sabit diski kullanımdan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="91abf-193">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="91abf-194">Hello Portalı'nda VM seçin ve tıklatın **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="91abf-194">Select your VM in hello portal and click **Disks**.</span></span> <span data-ttu-id="91abf-195">Varolan bir sanal sabit diski seçin ve ardından **ayırma**:</span><span class="sxs-lookup"><span data-stu-id="91abf-195">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Varolan bir sanal sabit disk ayırma](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="91abf-197">Merhaba VM başarıyla hello veri diski devam etmeden önce ayrılmış kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="91abf-197">Wait until hello VM has successfully detached hello data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="91abf-198">Özgün sabit diskten VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="91abf-198">Create VM from original hard disk</span></span>
<span data-ttu-id="91abf-199">bir VM, özgün sanal sabit diskten toocreate kullanmak [bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="91abf-199">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="91abf-200">Merhaba şablon hello VHD URL'si hello gelen kullanarak mevcut sanal ağda, bir VM dağıtır önceki komutu.</span><span class="sxs-lookup"><span data-stu-id="91abf-200">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="91abf-201">Merhaba tıklatın **tooAzure dağıtmak** gibi düğmesi:</span><span class="sxs-lookup"><span data-stu-id="91abf-201">Click hello **Deploy tooAzure** button as follows:</span></span>

![Github'dan şablondan VM dağıtma](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="91abf-203">Merhaba şablon dağıtımı için Azure portal hello yüklenir.</span><span class="sxs-lookup"><span data-stu-id="91abf-203">hello template is loaded into hello Azure portal for deployment.</span></span> <span data-ttu-id="91abf-204">Yeni VM ve mevcut Azure kaynaklarını Hello adlarını girin ve hello URL tooyour varolan bir sanal sabit diski yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="91abf-204">Enter hello names for your new VM and existing Azure resources, and paste hello URL tooyour existing virtual hard disk.</span></span> <span data-ttu-id="91abf-205">toobegin hello dağıtım tıklatın **satın alma**:</span><span class="sxs-lookup"><span data-stu-id="91abf-205">toobegin hello deployment, click **Purchase**:</span></span>

![VM şablonu dağıtma](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="91abf-207">Önyükleme tanılaması yeniden etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="91abf-207">Re-enable boot diagnostics</span></span>
<span data-ttu-id="91abf-208">Merhaba varolan sanal sabit diskten VM'nizi oluşturduğunuzda, önyükleme tanılaması otomatik olarak etkinleştirilmemiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="91abf-208">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="91abf-209">toocheck önyükleme tanılaması durumunu hello ve hello Portalı'nda, VM seçin gerekirse açın.</span><span class="sxs-lookup"><span data-stu-id="91abf-209">toocheck hello status of boot diagnostics and turn on if needed, select your VM in hello portal.</span></span> <span data-ttu-id="91abf-210">Altında **izleme**, tıklatın **tanılama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="91abf-210">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="91abf-211">Merhaba durum olduğundan emin olun **üzerinde**, ve onay işareti sonraki çok hello**önyükleme tanılama** seçilir.</span><span class="sxs-lookup"><span data-stu-id="91abf-211">Ensure hello status is **On**, and hello check mark next too**Boot diagnostics** is selected.</span></span> <span data-ttu-id="91abf-212">Herhangi bir değişiklik yaparsanız, tıklatın **kaydetmek**:</span><span class="sxs-lookup"><span data-stu-id="91abf-212">If you make any changes, click **Save**:</span></span>

![Önyükleme tanılaması ayarları güncelleştirme](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="91abf-214">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="91abf-214">Next steps</span></span>
<span data-ttu-id="91abf-215">Tooyour VM bağlantı sorunları yaşıyorsanız, bkz: [sorun giderme SSH bağlantıları tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="91abf-215">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="91abf-216">VM üzerinde çalışan uygulamalara erişim sorunları için bkz: [bir Linux VM üzerinde uygulama bağlantı sorunlarını giderme](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="91abf-216">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="91abf-217">Kaynak Yöneticisi'ni kullanma hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="91abf-217">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
