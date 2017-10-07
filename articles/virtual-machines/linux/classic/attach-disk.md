---
title: aaaAttach disk tooa Azure Linux VM'de | Microsoft Docs
description: "Nasıl tooattach bir veri diski tooa Linux VM öğrenin hello Klasik dağıtım modeli kullanıp kullanıma hazır olacak şekilde hello diski başlatın"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a><span data-ttu-id="46830-103">Nasıl tooAttach veri diski tooa Linux sanal makine</span><span class="sxs-lookup"><span data-stu-id="46830-103">How tooAttach a Data Disk tooa Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="46830-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="46830-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="46830-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="46830-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="46830-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="46830-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="46830-107">Bkz. nasıl çok[hello Resource Manager dağıtım modelini kullanarak bir veri diskini](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="46830-107">See how too[attach a data disk using hello Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="46830-108">Boş diskleri ve veri tooyour Azure Vm'leri içeren diskleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46830-108">You can attach both empty disks and disks that contain data tooyour Azure VMs.</span></span> <span data-ttu-id="46830-109">Her iki disk türleri için bir Azure depolama hesabında bulunan .vhd dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="46830-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="46830-110">Olarak tüm disk tooa Linux makine ekleme ile Merhaba disk ekledikten sonra tooinitialize gerekir ve kullanıma hazır olacak şekilde biçimlendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46830-110">As with adding any disk tooa Linux machine, after you attach hello disk you need tooinitialize and format it so it's ready for use.</span></span> <span data-ttu-id="46830-111">Bu makale ayrıntıları boş diskleri ve toothen başlatın ve yeni bir diski biçimlendirmek ne de veri tooyour VM'ler, zaten içeren diskleri ekleme.</span><span class="sxs-lookup"><span data-stu-id="46830-111">This article details attaching both empty disks and disks already containing data tooyour VMs, as well as how toothen initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="46830-112">Bir en iyi yöntem toouse biri olan veya daha fazla sanal makinenin veri diskleri toostore ayırın.</span><span class="sxs-lookup"><span data-stu-id="46830-112">It's a best practice toouse one or more separate disks toostore a virtual machine's data.</span></span> <span data-ttu-id="46830-113">Bir Azure sanal makine oluşturduğunuzda, bir işletim sistemi diski ve geçici bir disk vardır.</span><span class="sxs-lookup"><span data-stu-id="46830-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="46830-114">**Merhaba geçici disk toostore kalıcı veri kullanmayın.**</span><span class="sxs-lookup"><span data-stu-id="46830-114">**Do not use hello temporary disk toostore persistent data.**</span></span> <span data-ttu-id="46830-115">Merhaba adından da anlaşılacağı gibi yalnızca geçici depolama sağlar.</span><span class="sxs-lookup"><span data-stu-id="46830-115">As hello name implies, it provides temporary storage only.</span></span> <span data-ttu-id="46830-116">Azure depolama alanında bulunan değil çünkü hiçbir artıklık veya yedekleme sunar.</span><span class="sxs-lookup"><span data-stu-id="46830-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="46830-117">Merhaba geçici disk genellikle hello Azure Linux aracısı tarafından yönetilir ve otomatik olarak çok takılı**/mnt/kaynak** (veya **/mnt** Ubuntu görüntülerinde).</span><span class="sxs-lookup"><span data-stu-id="46830-117">hello temporary disk is typically managed by hello Azure Linux Agent and automatically mounted too**/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="46830-118">Üzerindeki diğer yandan Merhaba, bir veri diski hello Linux çekirdek tarafından şöyle adlandırılabilir `/dev/sdc`, ve toopartition, gereksinim duyduğunuz biçimlendirmek ve bu kaynak bağlayın.</span><span class="sxs-lookup"><span data-stu-id="46830-118">On hello other hand, a data disk might be named by hello Linux kernel something like `/dev/sdc`, and you need toopartition, format, and mount this resource.</span></span> <span data-ttu-id="46830-119">Merhaba bkz [Azure Linux Aracısı Kullanıcı Kılavuzu] [ Agent] Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="46830-119">See hello [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="46830-120">Linux içindeki yeni bir veri diski başlatın</span><span class="sxs-lookup"><span data-stu-id="46830-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="46830-121">SSH tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="46830-121">SSH tooyour VM.</span></span> <span data-ttu-id="46830-122">Daha fazla bilgi için bkz: [nasıl tooa Linux çalıştıran sanal makine üzerinde toolog][Logon].</span><span class="sxs-lookup"><span data-stu-id="46830-122">For more information, see [How toolog on tooa virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="46830-123">Ardından toofind hello cihaz tanımlayıcısı hello veri diski tooinitialize için gerekir.</span><span class="sxs-lookup"><span data-stu-id="46830-123">Next you need toofind hello device identifier for hello data disk tooinitialize.</span></span> <span data-ttu-id="46830-124">İki yolu toodo vardır:</span><span class="sxs-lookup"><span data-stu-id="46830-124">There are two ways toodo that:</span></span>
   
    <span data-ttu-id="46830-125">bir) Grep hello SCSI aygıtlar için günlüğe kaydeder, hello komut aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="46830-125">a) Grep for SCSI devices in hello logs, such as in hello following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="46830-126">Yeni Ubuntu dağıtımları için toouse gerekebilir `sudo grep SCSI /var/log/syslog` çok oturum`/var/log/messages` varsayılan olarak devre dışı olabilir.</span><span class="sxs-lookup"><span data-stu-id="46830-126">For recent Ubuntu distributions, you may need toouse `sudo grep SCSI /var/log/syslog` because logging too`/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="46830-127">Görüntülenen hello iletileri eklenen hello son veri diski hello tanıtıcısı bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46830-127">You can find hello identifier of hello last data disk that was added in hello messages that are displayed.</span></span>
   
    ![Merhaba disk iletileri alma](./media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="46830-129">OR</span><span class="sxs-lookup"><span data-stu-id="46830-129">OR</span></span>
   
    <span data-ttu-id="46830-130">b) kullanım hello `lsscsi` komutu toofind hello cihaz kimliği çıkışı. `lsscsi` ya da yüklenebilir `yum install lsscsi` (Red Hat üzerinde dağıtımları bağlı olarak) veya `apt-get install lsscsi` (Debian üzerinde dağıtımları bağlı olarak).</span><span class="sxs-lookup"><span data-stu-id="46830-130">b) Use hello `lsscsi` command toofind out hello device id. `lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="46830-131">Merhaba disk tarafından aradığınız bulabilirsiniz kendi *lun* veya **mantıksal birim numarası**.</span><span class="sxs-lookup"><span data-stu-id="46830-131">You can find hello disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="46830-132">Örneğin, hello *lun* bağlı hello diskleri gelen kolayca görülebilir için `azure vm disk list <virtual-machine>` olarak:</span><span class="sxs-lookup"><span data-stu-id="46830-132">For example, hello *lun* for hello disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="46830-133">Merhaba çıkış benzer toohello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="46830-133">hello output is similar toohello following:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    <span data-ttu-id="46830-134">Bu verileri hello çıktısını ile karşılaştırmak `lsscsi` Merhaba aynı sanal makine örnek:</span><span class="sxs-lookup"><span data-stu-id="46830-134">Compare this data with hello output of `lsscsi` for hello same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="46830-135">Merhaba son hello tuple her satırda sayısıdır hello *lun*.</span><span class="sxs-lookup"><span data-stu-id="46830-135">hello last number in hello tuple in each row is hello *lun*.</span></span> <span data-ttu-id="46830-136">Bkz: `man lsscsi` daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="46830-136">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="46830-137">Merhaba istemine komut toocreate aşağıdaki hello Cihazınızı yazın:</span><span class="sxs-lookup"><span data-stu-id="46830-137">At hello prompt, type hello following command toocreate your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="46830-138">İstendiğinde yazın  **n**  toocreate bir bölüm.</span><span class="sxs-lookup"><span data-stu-id="46830-138">When prompted, type **n** toocreate a partition.</span></span>

    ![Cihaz oluşturma](./media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="46830-140">İstendiğinde yazın **p** toomake hello bölüm hello birincil bölüm.</span><span class="sxs-lookup"><span data-stu-id="46830-140">When prompted, type **p** toomake hello partition hello primary partition.</span></span> <span data-ttu-id="46830-141">Tür **1** hello ilk bölüm ve ardından toomake hello silindir tooaccept hello varsayılan değer girin.</span><span class="sxs-lookup"><span data-stu-id="46830-141">Type **1** toomake it hello first partition, and then type enter tooaccept hello default value for hello cylinder.</span></span> <span data-ttu-id="46830-142">Bazı sistemlerde, bu hello hello varsayılan değerleri ilk Göster ve hello silindir yerine son kesimler hello.</span><span class="sxs-lookup"><span data-stu-id="46830-142">On some systems, it can show hello default values of hello first and hello last sectors, instead of hello cylinder.</span></span> <span data-ttu-id="46830-143">Bu varsayılan tooaccept seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46830-143">You can choose tooaccept these defaults.</span></span>

    ![Bölümü oluşturma](./media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="46830-145">Tür **p** toosee hello bölümlenme şekli hello disk ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="46830-145">Type **p** toosee hello details about hello disk that is being partitioned.</span></span>

    ![Liste disk bilgileri](./media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="46830-147">Tür **w** hello disk için toowrite hello ayarları.</span><span class="sxs-lookup"><span data-stu-id="46830-147">Type **w** toowrite hello settings for hello disk.</span></span>

    ![Merhaba disk değişiklikleri yazma](./media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="46830-149">Artık hello yeni bölüme hello dosya sistemi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46830-149">Now you can create hello file system on hello new partition.</span></span> <span data-ttu-id="46830-150">Merhaba bölüm numarası toohello cihaz kimliği ekleme (aşağıdaki örneğine hello içinde `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="46830-150">Append hello partition number toohello device ID (in hello following example `/dev/sdc1`).</span></span> <span data-ttu-id="46830-151">Merhaba aşağıdaki örnekte bir ext4 bölüm üzerinde /dev/sdc1 oluşturur:</span><span class="sxs-lookup"><span data-stu-id="46830-151">hello following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Dosya sistemi oluştur](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="46830-153">SuSE Linux Enterprise 11 sistemleri yalnızca ext4 dosya sistemleri için salt okunur erişimi de destekler.</span><span class="sxs-lookup"><span data-stu-id="46830-153">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="46830-154">Bu sistemler için tooformat hello yeni dosya sistemi ext4 yerine ext3 olarak önerilir.</span><span class="sxs-lookup"><span data-stu-id="46830-154">For these systems, it is recommended tooformat hello new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="46830-155">Dizin toomount hello yeni bir dosya sistemi, yapın:</span><span class="sxs-lookup"><span data-stu-id="46830-155">Make a directory toomount hello new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="46830-156">Son olarak hello sürücü şu şekilde bağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="46830-156">Finally you can mount hello drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="46830-157">Merhaba veri diski olduğu şimdi olarak hazır toouse **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="46830-157">hello data disk is now ready toouse as **/datadrive**.</span></span>
   
    ![Başlangıç dizini ve bağlama hello disketi oluşturma](./media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="46830-159">Merhaba yeni sürücü çok/etc/fstab ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46830-159">Add hello new drive too/etc/fstab:</span></span>
   
    <span data-ttu-id="46830-160">olması gereken yeniden başlatma toohello /etc/fstab dosya ekleninceye sonra tooensure hello sürücü otomatik olarak yeniden.</span><span class="sxs-lookup"><span data-stu-id="46830-160">tooensure hello drive is remounted automatically after a reboot it must be added toohello /etc/fstab file.</span></span> <span data-ttu-id="46830-161">Ayrıca, bu hello UUID (evrensel benzersiz tanıtıcı) yalnızca hello aygıt adı (yani /dev/sdc1) yerine /etc/fstab toorefer toohello sürücü kullanılır önerilir.</span><span class="sxs-lookup"><span data-stu-id="46830-161">In addition, it is highly recommended that hello UUID (Universally Unique IDentifier) is used in /etc/fstab toorefer toohello drive rather than just hello device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="46830-162">Hello kullanarak UUID hello hatalı disk konumu hello işletim sistemi önyükleme sırasında disk hatası algılar ve ardından olan kalan olan veri disklerinin olanlar cihaz kimlikleri atanan verilen takılı tooa olan önler.</span><span class="sxs-lookup"><span data-stu-id="46830-162">Using hello UUID avoids hello incorrect disk being mounted tooa given location if hello OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="46830-163">toofind hello yeni sürücü UUID Merhaba, hello kullanabilirsiniz **blkid** yardımcı programı:</span><span class="sxs-lookup"><span data-stu-id="46830-163">toofind hello UUID of hello new drive, you can use hello **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="46830-164">Hello çıkış benzer toohello örnek aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="46830-164">hello output looks similar toohello following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="46830-165">Yanlış hello düzenleme **/etc/fstab** dosya önyüklenemez bir sisteme neden.</span><span class="sxs-lookup"><span data-stu-id="46830-165">Improperly editing hello **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="46830-166">Emin değilseniz, bu dosyayı tooproperly düzenleme nasıl bilgi toohello dağıtım'ın belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="46830-166">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="46830-167">Ayrıca, düzenlemeye başlamadan önce hello /etc/fstab dosyanızın bir yedeğini oluşturduğunuz önerilir.</span><span class="sxs-lookup"><span data-stu-id="46830-167">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="46830-168">Ardından, hello'ı açmak **/etc/fstab** dosyasını bir metin düzenleyicisinde:</span><span class="sxs-lookup"><span data-stu-id="46830-168">Next, open hello **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="46830-169">Bu örnekte, hello UUID değeri Merhaba yeni kullanırız **/dev/sdc1** oluşturulduğu hello önceki adımları ve hello mountpoint aygıt **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="46830-169">In this example, we use hello UUID value for hello new **/dev/sdc1** device that was created in hello previous steps, and hello mountpoint **/datadrive**.</span></span> <span data-ttu-id="46830-170">Satır toohello hello sonuna aşağıdaki hello eklemek **/etc/fstab** dosyası:</span><span class="sxs-lookup"><span data-stu-id="46830-170">Add hello following line toohello end of hello **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="46830-171">Ya da SuSE Linux tabanlı sistemlerde toouse biraz farklı bir biçim gerekebilir:</span><span class="sxs-lookup"><span data-stu-id="46830-171">Or, on systems based on SuSE Linux you may need toouse a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="46830-172">Merhaba `nofail` seçeneği, VM başlatır hello dosya sistemi bozuk veya hello disk önyükleme sırasında yok olsa bile bu hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="46830-172">hello `nofail` option ensures that hello VM starts even if hello filesystem is corrupt or hello disk does not exist at boot time.</span></span> <span data-ttu-id="46830-173">Bu seçenek olmadan, davranış açıklandığı gibi karşılaşabilirsiniz [olamaz SSH tooLinux VM tooFSTAB hatalar nedeniyle](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span><span class="sxs-lookup"><span data-stu-id="46830-173">Without this option, you may encounter behavior as described in [Cannot SSH tooLinux VM due tooFSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="46830-174">Merhaba dosya sistemi takılı artık test edebilirsiniz kullanılarak uygun şekilde çıkarma ve hello dosya sistemi çıkarmadan, yani hello örnek bağlama noktası `/datadrive` hello oluşturulan önceki adımları:</span><span class="sxs-lookup"><span data-stu-id="46830-174">You can now test that hello file system is mounted properly by unmounting and then remounting hello file system, i.e. using hello example mount point `/datadrive` created in hello earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="46830-175">Merhaba, `mount` komutu, bir hata üretir, hello/etc/fstab doğru sözdizimi için dosyayı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="46830-175">If hello `mount` command produces an error, check hello /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="46830-176">Ek veri sürücüleri veya bölümleri oluşturulduğu varsa, bunları/etc/fstab de ayrı olarak girin.</span><span class="sxs-lookup"><span data-stu-id="46830-176">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="46830-177">Merhaba sürücü yazılabilir bu komutu kullanarak yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="46830-177">Make hello drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="46830-178">Sonradan bir veri diski fstab düzenlemeden kaldırma hello VM toofail tooboot neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="46830-178">Subsequently removing a data disk without editing fstab could cause hello VM toofail tooboot.</span></span> <span data-ttu-id="46830-179">Bu sık karşılaşılan bir durumdur, çoğu dağıtımları ya da hello sağlamanız `nofail` ve/veya `nobootwait` hello disk toomount önyükleme sırasında başarısız olsa bile, sistem tooboot izin fstab seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="46830-179">If this is a common occurrence, most distributions provide either hello `nofail` and/or `nobootwait` fstab options that allow a system tooboot even if hello disk fails toomount at boot time.</span></span> <span data-ttu-id="46830-180">Bu parametreler hakkında daha fazla bilgi için dağıtım ait belgelere bakın.</span><span class="sxs-lookup"><span data-stu-id="46830-180">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="46830-181">KIRPMA/UNMAP Azure Linux desteği</span><span class="sxs-lookup"><span data-stu-id="46830-181">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="46830-182">Bazı Linux tekrar KIRPMA/UNMAP işlemleri toodiscard destek hello diskte kullanılmayan engeller.</span><span class="sxs-lookup"><span data-stu-id="46830-182">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="46830-183">Bu işlemler sayfaları silinmiş Azure artık geçerli değil ve iptal edilecek standart depolama tooinform öncelikle faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="46830-183">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="46830-184">Büyük dosyaları oluşturmak ve bunları silerseniz sayfaları atılıyor maliyet kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46830-184">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="46830-185">Tooenable KIRPMA desteği, Linux VM'NİZDE iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="46830-185">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="46830-186">Her zamanki gibi dağıtımınız için önerilen yaklaşımı hello bakın:</span><span class="sxs-lookup"><span data-stu-id="46830-186">As usual, consult your distribution for hello recommended approach:</span></span>

* <span data-ttu-id="46830-187">Kullanım hello `discard` bağlama seçeneği `/etc/fstab`, örneğin:</span><span class="sxs-lookup"><span data-stu-id="46830-187">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="46830-188">Bazı durumlarda hello içinde `discard` seçeneği performans etkileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="46830-188">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="46830-189">Alternatif olarak, hello çalıştırabilirsiniz `fstrim` komutunu el ile Merhaba komut satırından veya tooyour crontab toorun düzenli olarak ekleyin:</span><span class="sxs-lookup"><span data-stu-id="46830-189">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>
  
    <span data-ttu-id="46830-190">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="46830-190">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="46830-191">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="46830-191">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="46830-192">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="46830-192">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="46830-193">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="46830-193">Next Steps</span></span>
<span data-ttu-id="46830-194">Daha fazla bilgiyi aşağıdaki makaleleri hello Linux VM kullanma hakkında:</span><span class="sxs-lookup"><span data-stu-id="46830-194">You can read more about using your Linux VM in hello following articles:</span></span>

* <span data-ttu-id="46830-195">[Nasıl toolog Linux çalıştıran tooa sanal makine üzerinde][Logon]</span><span class="sxs-lookup"><span data-stu-id="46830-195">[How toolog on tooa virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="46830-196">Nasıl toodetach bir Linux sanal makineden bir disk</span><span class="sxs-lookup"><span data-stu-id="46830-196">How toodetach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="46830-197">Merhaba Klasik dağıtım modeliyle Hello Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="46830-197">Using hello Azure CLI with hello Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="46830-198">Azure'da bir Linux VM üzerinde RAID yapılandırın</span><span class="sxs-lookup"><span data-stu-id="46830-198">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="46830-199">Azure'da bir Linux VM LVM yapılandırın</span><span class="sxs-lookup"><span data-stu-id="46830-199">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
