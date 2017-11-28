---
title: "Azure yedekleme: Dosya ve klasörleri Azure VM yedekten kurtarma | Microsoft Docs"
description: "Dosyaları bir Azure sanal makinesi kurtarma noktasından kurtarın"
services: backup
documentationcenter: dev-center-name
author: pvrk
manager: shivamg
keywords: "öğe düzeyinde kurtarma; Dosya Kurtarma Azure VM yedekten; Azure VM geri yükleme dosyaları"
ms.assetid: f1c067a2-4826-4da4-b97a-c5fd6c189a77
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pullabhk;markgal
ms.openlocfilehash: ae7c345c11a7db25413d60ad822f16f84ca37362
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="recover-files-from-azure-virtual-machine-backup"></a><span data-ttu-id="95c84-104">Dosyaları Azure sanal makinesi yedeklemeden Kurtar</span><span class="sxs-lookup"><span data-stu-id="95c84-104">Recover files from Azure virtual machine backup</span></span>

<span data-ttu-id="95c84-105">Azure yedekleme geri yükleme yeteneği sağlar [Azure Vm'leri ve diskleri](./backup-azure-arm-restore-vms.md) Azure VM yedeklerden.</span><span class="sxs-lookup"><span data-stu-id="95c84-105">Azure backup provides the capability to restore [Azure VMs and disks](./backup-azure-arm-restore-vms.md) from Azure VM backups.</span></span> <span data-ttu-id="95c84-106">Şimdi bu makalede, bir Azure VM yedekten dosyalar ve klasörler gibi öğeleri nasıl kurtarabilirsiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="95c84-106">Now this article explains how you can recover items such as files and folders from an Azure VM backup.</span></span>

> [!Note]
> <span data-ttu-id="95c84-107">Bu özellik, Azure Resource Manager modelini kullanarak dağıtılmış ve bir kurtarma Hizmetleri kasası korumalı VM'ler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="95c84-107">This feature is available for Azure VMs deployed using the Resource Manager model and protected to a Recovery services vault.</span></span>
> <span data-ttu-id="95c84-108">Şifrelenmiş bir VM yedeğinin dosya kurtarma desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="95c84-108">File recovery from an encrypted VM backup is not supported.</span></span>
>

## <a name="mount-the-volume-and-copy-files"></a><span data-ttu-id="95c84-109">Birim ve kopyalama dosyaları bağlama</span><span class="sxs-lookup"><span data-stu-id="95c84-109">Mount the volume and copy files</span></span>

1. <span data-ttu-id="95c84-110">[Azure portal](http://portal.Azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="95c84-110">Sign into the [Azure portal](http://portal.Azure.com).</span></span> <span data-ttu-id="95c84-111">İlgili kurtarma Hizmetleri kasası ve gerekli yedekleme öğesi bulun.</span><span class="sxs-lookup"><span data-stu-id="95c84-111">Find the relevant Recovery services vault and the required backup item.</span></span>

2. <span data-ttu-id="95c84-112">Yedekleme öğesinin dikey penceresinde **dosya kurtarma**</span><span class="sxs-lookup"><span data-stu-id="95c84-112">On the Backup Item blade, click **File Recovery**</span></span>

    ![Açık kurtarma Hizmetleri kasasına yedekleme öğesi](./media/backup-azure-restore-files-from-vm/open-vault-item.png)

    <span data-ttu-id="95c84-114">**Dosya kurtarma** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="95c84-114">The **File Recovery** blade opens.</span></span>

    ![Dosya Kurtarma dikey penceresi](./media/backup-azure-restore-files-from-vm/file-recovery-blade.png)

3. <span data-ttu-id="95c84-116">Gelen **kurtarma noktası seçin** açılır menüsünde, kullanmak istediğiniz dosyaları içeren kurtarma noktasını seçin.</span><span class="sxs-lookup"><span data-stu-id="95c84-116">From the **Select recovery point** drop-down menu, select the recovery point that contains the files you want.</span></span> <span data-ttu-id="95c84-117">Varsayılan olarak, en son kurtarma noktası zaten seçilidir.</span><span class="sxs-lookup"><span data-stu-id="95c84-117">By default, the latest recovery point is already selected.</span></span>

4. <span data-ttu-id="95c84-118">' I tıklatın **karşıdan yürütülebilir** (için Windows Azure VM) veya **karşıdan yükleme komut dosyası** (için Linux Azure VM) kurtarma noktasından dosyaları kopyalamak için kullanacağınız yazılımını indirmek için.</span><span class="sxs-lookup"><span data-stu-id="95c84-118">Click **Download Executable** (for Windows Azure VM) or **Download Script** (for Linux Azure VM) to download the software that you'll use to copy files from the recovery point.</span></span>

  <span data-ttu-id="95c84-119">Yürütülebilir dosya/komut dosyası yerel bilgisayar ve belirtilen kurtarma noktası arasında bir bağlantı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="95c84-119">The executable/script creates a connection between the local computer and the specified recovery point.</span></span>

5. <span data-ttu-id="95c84-120">İndirilen komut dosyası/yürütülebilir dosyayı çalıştırmak için bir parola gerekir.</span><span class="sxs-lookup"><span data-stu-id="95c84-120">You need a password to run the downloaded script/executable.</span></span> <span data-ttu-id="95c84-121">Oluşturulan parola yanında Kopyala düğmesini kullanarak portalından parolası kopyalama</span><span class="sxs-lookup"><span data-stu-id="95c84-121">You can copy the password from the portal using the copy button beside the generated password</span></span>

    ![Oluşturulan parola](./media/backup-azure-restore-files-from-vm/generated-pswd.png)

6. <span data-ttu-id="95c84-123">Dosyaları kurtarmak istediğiniz bilgisayarda yürütülebilir/komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="95c84-123">On the computer where you want to recover the files, run the executable/script.</span></span> <span data-ttu-id="95c84-124">Yönetici kimlik bilgileriyle çalıştırmalısınız.</span><span class="sxs-lookup"><span data-stu-id="95c84-124">You must run it with Administrator credentials.</span></span> <span data-ttu-id="95c84-125">Sınırlı erişimi olan bir bilgisayarda bir betik çalıştırırsanız, erişimi olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="95c84-125">If you run the script on a computer with restricted access, ensure there is access to:</span></span>

    - <span data-ttu-id="95c84-126">download.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="95c84-126">download.microsoft.com</span></span>
    - <span data-ttu-id="95c84-127">Azure VM yedeklemeler için kullandığınız azure uç noktaları</span><span class="sxs-lookup"><span data-stu-id="95c84-127">Azure endpoints used for Azure VM backups</span></span>
    - <span data-ttu-id="95c84-128">Giden bağlantı noktası 3260</span><span class="sxs-lookup"><span data-stu-id="95c84-128">outbound port 3260</span></span>

   <span data-ttu-id="95c84-129">Linux için komut dosyası kurtarma noktasına bağlanmak için 'open-iSCSI' ve 'lshw' bileşenleri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="95c84-129">For Linux, the script requires 'open-iscsi' and 'lshw' components to connect to the recovery point.</span></span> <span data-ttu-id="95c84-130">Bu nerede çalıştığına makinede yoksa ilgili bileşenlerini yüklemek için izin ister ve bunları izin yükler.</span><span class="sxs-lookup"><span data-stu-id="95c84-130">If those do not exist on the machine where it is run, it asks for permission to install the relevant components and installs them upon consent.</span></span>
   
   <span data-ttu-id="95c84-131">İstendiğinde portalından kopyalandığından parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="95c84-131">Enter the password copied from the portal when prompted.</span></span> <span data-ttu-id="95c84-132">Geçerli parola girildikten sonra komut dosyaları kurtarma noktasına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="95c84-132">Once the valid password is entered the scripts connects to the recovery point.</span></span>
      
    ![Dosya Kurtarma dikey penceresi](./media/backup-azure-restore-files-from-vm/executable-output.png)
    
   
   <span data-ttu-id="95c84-134">Yedeklenen VM olarak aynı (veya uyumlu) işletim sistemine sahip herhangi bir makinede komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="95c84-134">You can run the script on any machine that has the same (or compatible) operating system as the backed-up VM.</span></span> <span data-ttu-id="95c84-135">Bkz: [uyumlu işletim sistemi tablo](backup-azure-restore-files-from-vm.md#compatible-os) uyumlu işletim sistemleri için.</span><span class="sxs-lookup"><span data-stu-id="95c84-135">See the [Compatible OS table](backup-azure-restore-files-from-vm.md#compatible-os) for compatible operating systems.</span></span> <span data-ttu-id="95c84-136">Ardından korumalı Azure sanal makine Windows depolama alanları (için Windows Azure VM) veya LVM/RAID Arrays(for Linux VMs) kullanıyorsa, aynı sanal makineye yürütülebilir/komut dosyası çalıştırılamaz.</span><span class="sxs-lookup"><span data-stu-id="95c84-136">If the protected Azure virtual machine uses Windows Storage Spaces (for Windows Azure VMs) or LVM/RAID Arrays(for Linux VMs), then you can't run the executable/script on the same virtual machine.</span></span> <span data-ttu-id="95c84-137">Bunun yerine, çalıştırın uyumlu bir işletim sistemi ile diğer herhangi bir makinede.</span><span class="sxs-lookup"><span data-stu-id="95c84-137">Instead, run it on any other machine with a compatible operating system.</span></span>

### <a name="compatible-os"></a><span data-ttu-id="95c84-138">Uyumlu işletim sistemi</span><span class="sxs-lookup"><span data-stu-id="95c84-138">Compatible OS</span></span>

#### <a name="for-windows"></a><span data-ttu-id="95c84-139">Windows için</span><span class="sxs-lookup"><span data-stu-id="95c84-139">For Windows</span></span>

<span data-ttu-id="95c84-140">Aşağıdaki tabloda, sunucu ve bilgisayar işletim sistemleri arasındaki uyumluluk gösterir.</span><span class="sxs-lookup"><span data-stu-id="95c84-140">The following table shows the compatibility between server and computer operating systems.</span></span> <span data-ttu-id="95c84-141">Dosyaları kurtarırken uyumsuz işletim sistemleri arasında dosya geri yüklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="95c84-141">When recovering files, you can't restore files between incompatible operating systems.</span></span>

|<span data-ttu-id="95c84-142">Sunucu işletim sistemi</span><span class="sxs-lookup"><span data-stu-id="95c84-142">Server OS</span></span> | <span data-ttu-id="95c84-143">Uyumlu istemci işletim sistemi</span><span class="sxs-lookup"><span data-stu-id="95c84-143">Compatible client OS</span></span>  |
| --------------- | ---- |
| <span data-ttu-id="95c84-144">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="95c84-144">Windows Server 2012 R2</span></span> | <span data-ttu-id="95c84-145">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="95c84-145">Windows 8.1</span></span> |
| <span data-ttu-id="95c84-146">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="95c84-146">Windows Server 2012</span></span>    | <span data-ttu-id="95c84-147">Windows 8</span><span class="sxs-lookup"><span data-stu-id="95c84-147">Windows 8</span></span>  |
| <span data-ttu-id="95c84-148">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="95c84-148">Windows Server 2008 R2</span></span> | <span data-ttu-id="95c84-149">Windows 7</span><span class="sxs-lookup"><span data-stu-id="95c84-149">Windows 7</span></span>   |

#### <a name="for-linux"></a><span data-ttu-id="95c84-150">Linux için</span><span class="sxs-lookup"><span data-stu-id="95c84-150">For Linux</span></span>

<span data-ttu-id="95c84-151">Linux komut dosyası çalıştırdığı makine işletim sistemini yedeklenen Linux VM'de mevcut dosyaların dosya sistemi desteklemesi gereken temel gereksinimdir.</span><span class="sxs-lookup"><span data-stu-id="95c84-151">In Linux, the fundamental requirement is that the OS of the machine where the script is run should support the filesystem of the files present in the backed-up Linux VM.</span></span> <span data-ttu-id="95c84-152">Komut dosyasını çalıştırmak için bir makine seçerken, lütfen bu uyumlu işletim sistemi ve sürümleri aşağıdaki tabloda belirtildiği gibi sahip emin olun.</span><span class="sxs-lookup"><span data-stu-id="95c84-152">While selecting a machine to run the script, please ensure it has the compatible OS and the versions as mentioned in the table below.</span></span>

|<span data-ttu-id="95c84-153">Linux işletim sistemi</span><span class="sxs-lookup"><span data-stu-id="95c84-153">Linux OS</span></span> | <span data-ttu-id="95c84-154">Sürümler</span><span class="sxs-lookup"><span data-stu-id="95c84-154">Versions</span></span>  |
| --------------- | ---- |
| <span data-ttu-id="95c84-155">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="95c84-155">Ubuntu</span></span> | <span data-ttu-id="95c84-156">12.04 ve üstü</span><span class="sxs-lookup"><span data-stu-id="95c84-156">12.04 and above</span></span> |
| <span data-ttu-id="95c84-157">CentOS</span><span class="sxs-lookup"><span data-stu-id="95c84-157">CentOS</span></span> | <span data-ttu-id="95c84-158">6.5 ve üstü</span><span class="sxs-lookup"><span data-stu-id="95c84-158">6.5 and above</span></span>  |
| <span data-ttu-id="95c84-159">RHEL</span><span class="sxs-lookup"><span data-stu-id="95c84-159">RHEL</span></span> | <span data-ttu-id="95c84-160">6.7 ve üstü</span><span class="sxs-lookup"><span data-stu-id="95c84-160">6.7 and above</span></span> |
| <span data-ttu-id="95c84-161">Debian</span><span class="sxs-lookup"><span data-stu-id="95c84-161">Debian</span></span> | <span data-ttu-id="95c84-162">7 ve üstü</span><span class="sxs-lookup"><span data-stu-id="95c84-162">7 and above</span></span> |
| <span data-ttu-id="95c84-163">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="95c84-163">Oracle Linux</span></span> | <span data-ttu-id="95c84-164">6.4 ve üstü</span><span class="sxs-lookup"><span data-stu-id="95c84-164">6.4 and above</span></span> |

<span data-ttu-id="95c84-165">Komut dosyası yürütme ve güvenli bir şekilde kurtarma noktasına bağlanmak için python ve bash bileşenleri de gerektirir.</span><span class="sxs-lookup"><span data-stu-id="95c84-165">The script also requires python and bash components to execute and connect securely to the recovery point.</span></span>

|<span data-ttu-id="95c84-166">Bileşen</span><span class="sxs-lookup"><span data-stu-id="95c84-166">Component</span></span> | <span data-ttu-id="95c84-167">Sürüm</span><span class="sxs-lookup"><span data-stu-id="95c84-167">Version</span></span>  |
| --------------- | ---- |
| <span data-ttu-id="95c84-168">Bash</span><span class="sxs-lookup"><span data-stu-id="95c84-168">bash</span></span> | <span data-ttu-id="95c84-169">4 ve üstü</span><span class="sxs-lookup"><span data-stu-id="95c84-169">4 and above</span></span> |
| <span data-ttu-id="95c84-170">python</span><span class="sxs-lookup"><span data-stu-id="95c84-170">python</span></span> | <span data-ttu-id="95c84-171">2.6.6 ve üstü</span><span class="sxs-lookup"><span data-stu-id="95c84-171">2.6.6 and above</span></span>  |


### <a name="identifying-volumes"></a><span data-ttu-id="95c84-172">Birimleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="95c84-172">Identifying Volumes</span></span>

#### <a name="for-windows"></a><span data-ttu-id="95c84-173">Windows için</span><span class="sxs-lookup"><span data-stu-id="95c84-173">For Windows</span></span>

<span data-ttu-id="95c84-174">Exectuable çalıştırdığınızda, işletim sistemi yeni birimlere bağlar ve sürücü harfi atar.</span><span class="sxs-lookup"><span data-stu-id="95c84-174">When you run the exectuable, the operating system mounts the new volumes and assigns drive letters.</span></span> <span data-ttu-id="95c84-175">Bu sürücüleri göz atmak için Windows Gezgini'nde veya dosya Gezgini'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="95c84-175">You can use Windows Explorer or File Explorer to browse those drives.</span></span> <span data-ttu-id="95c84-176">Birimlere atanan sürücü harfleri özgün sanal makine olarak aynı harf olmayabilir, ancak, birim adı korunur.</span><span class="sxs-lookup"><span data-stu-id="95c84-176">The drive letters assigned to the volumes may not be the same letters as the original virtual machine, however, the volume name is preserved.</span></span> <span data-ttu-id="95c84-177">Örneğin, özgün sanal makine birimde ise "veri diski (E:\)", toplu olarak eklenebilecek "veri diski ('Herhangi bir sürücü harfi kullanılabilir':\) yerel bilgisayarda.</span><span class="sxs-lookup"><span data-stu-id="95c84-177">For example, if the volume on the original virtual machine was “Data Disk (E:\)”, that volume can be attached as “Data Disk ('Any drive letter available':\) on the local computer.</span></span> <span data-ttu-id="95c84-178">Komut çıktısında dosya/klasör bulana kadar bahsedilen tüm birimler üzerinden göz atın.</span><span class="sxs-lookup"><span data-stu-id="95c84-178">Browse through all volumes mentioned in the script output until you find your files/folder.</span></span>  
       
   ![Dosya Kurtarma dikey penceresi](./media/backup-azure-restore-files-from-vm/volumes-attached.png)
           
#### <a name="for-linux"></a><span data-ttu-id="95c84-180">Linux için</span><span class="sxs-lookup"><span data-stu-id="95c84-180">For Linux</span></span>

<span data-ttu-id="95c84-181">Linux komut dosyası çalıştırdığı klasörüne kurtarma noktası birimleri bağlanır.</span><span class="sxs-lookup"><span data-stu-id="95c84-181">In Linux, the volumes of the recovery point are mounted to the folder where the script is run.</span></span> <span data-ttu-id="95c84-182">Ekli diskleri, birimleri ve karşılık gelen bağlama yollarını buna uygun olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="95c84-182">The attached disks, volumes and the corresponding mount paths are shown accordingly.</span></span> <span data-ttu-id="95c84-183">Bu yolları bağlama kök düzeyinde erişime sahip kullanıcılar tarafından görülebilir.</span><span class="sxs-lookup"><span data-stu-id="95c84-183">These mount paths are visible to users having root level access.</span></span> <span data-ttu-id="95c84-184">Komut çıktısında belirtilen birimler göz atın.</span><span class="sxs-lookup"><span data-stu-id="95c84-184">Browse through the volumes mentioned in the script output.</span></span>

  ![Linux dosya kurtarma dikey penceresi](./media/backup-azure-restore-files-from-vm/linux-mount-paths.png)
  

## <a name="closing-the-connection"></a><span data-ttu-id="95c84-186">Bağlantı kesiliyor</span><span class="sxs-lookup"><span data-stu-id="95c84-186">Closing the connection</span></span>

<span data-ttu-id="95c84-187">Dosyaları tanımlama ve yerel depolama konumuna kopyalanması sonra Kaldır (veya çıkarın) ek sürücüler.</span><span class="sxs-lookup"><span data-stu-id="95c84-187">After identifying the files and copying them to a local storage location, remove (or unmount) the additional drives.</span></span> <span data-ttu-id="95c84-188">Üzerinde sürücülerin kaldırılması **dosya kurtarma** dikey Azure portalında tıklayın **çıkarın diskleri**.</span><span class="sxs-lookup"><span data-stu-id="95c84-188">To unmount the drives, on the **File Recovery** blade in the Azure portal, click **Unmount Disks**.</span></span>

![Diskleri çıkarın](./media/backup-azure-restore-files-from-vm/unmount-disks3.png)

<span data-ttu-id="95c84-190">Diskleri kaldırılan işlendikten sonra size başarılı olduğunu bildiren bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="95c84-190">Once the disks have been unmounted, you receive a message letting you know it was successful.</span></span> <span data-ttu-id="95c84-191">Bağlantının diskleri kaldırabilmeniz yenilemek birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="95c84-191">It may take a few minutes for the connection to refresh so that you can remove the disks.</span></span>

<span data-ttu-id="95c84-192">Kurtarma noktası için bağlantı zarar görmesi sonra Linux OS karşılık gelen bağlama yolları otomatik olarak kaldırmaz.</span><span class="sxs-lookup"><span data-stu-id="95c84-192">In Linux, after the connection to the recovery point is severed, the OS doesn't remove the corresponding mount paths automatically.</span></span> <span data-ttu-id="95c84-193">Bu "artık" birimler olarak var ve görünür ancak, erişim/yazma dosyaları olduğunda hata throw.</span><span class="sxs-lookup"><span data-stu-id="95c84-193">These exist as "orphan" volumes and they are visible but throw an error when you access/write the files.</span></span> <span data-ttu-id="95c84-194">Bunlar el ile kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="95c84-194">They can be manually removed.</span></span> <span data-ttu-id="95c84-195">Çalıştırdığınızda, komut dosyası, herhangi bir önceki kurtarma noktasını varolan böyle herhangi bir birimi tanımlar ve onay temizler.</span><span class="sxs-lookup"><span data-stu-id="95c84-195">The script, when run, identifies any such volumes existing from any previous recovery points and cleans them up upon consent.</span></span>

## <a name="special-configurations"></a><span data-ttu-id="95c84-196">Özel yapılandırmalar</span><span class="sxs-lookup"><span data-stu-id="95c84-196">Special configurations</span></span>

### <a name="dynamic-disks"></a><span data-ttu-id="95c84-197">Dinamik diskler</span><span class="sxs-lookup"><span data-stu-id="95c84-197">Dynamic Disks</span></span>

<span data-ttu-id="95c84-198">Ardından yedeklenen Azure VM dinamik disklerde (yayılmış ve şeritli birimler) birden çok diske yayılan birimler ve/veya hataya dayanıklı birimler (yansıtılmış veya RAID-5 birimler) varsa, aynı VM yürütülebilir komut dosyası çalıştırılamaz.</span><span class="sxs-lookup"><span data-stu-id="95c84-198">If the Azure VM that was backed up has volumes that span multiple disks (spanned and striped volumes) and/or fault-tolerant volumes (mirrored and RAID-5 volumes) on dynamic disks, then you can't run the executable script on the same VM.</span></span> <span data-ttu-id="95c84-199">Bunun yerine, uyumlu bir işletim sistemi ile diğer herhangi bir makinede çalıştırılabilir komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="95c84-199">Instead, run the executable script on any other machine with a compatible operating system.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="95c84-200">Windows depolama alanları</span><span class="sxs-lookup"><span data-stu-id="95c84-200">Windows Storage Spaces</span></span>

<span data-ttu-id="95c84-201">Windows depolama alanları, depolamayı sanallaştırmanızı sağlar Windows depolama için kullanılan bir teknolojidir.</span><span class="sxs-lookup"><span data-stu-id="95c84-201">Windows Storage Spaces is a technology in Windows storage that enables you to virtualize storage.</span></span> <span data-ttu-id="95c84-202">Windows depolama alanları ile endüstri standardı diskleri depolama havuzları olarak gruplandırdıktan ve ardından bu depolama havuzlarındaki kullanılabilir alandan depolama alanları olarak adlandırılan sanal diskler oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="95c84-202">With Windows Storage Spaces you can group industry-standard disks into storage pools, and then create virtual disks, called storage spaces, from the available space in those storage pools.</span></span>

<span data-ttu-id="95c84-203">Ardından yedeklenen Azure VM Windows depolama alanları kullanıyorsa, aynı VM yürütülebilir komut dosyası çalıştırılamaz.</span><span class="sxs-lookup"><span data-stu-id="95c84-203">If the Azure VM that was backed up uses Windows Storage Spaces, then you can't run the executable script on the same VM.</span></span> <span data-ttu-id="95c84-204">Bunun yerine, uyumlu bir işletim sistemi ile diğer herhangi bir makinede çalıştırılabilir komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="95c84-204">Instead, run the executable script on any other machine with a compatible operating system.</span></span>

### <a name="lvmraid-arrays"></a><span data-ttu-id="95c84-205">LVM/RAID dizileri</span><span class="sxs-lookup"><span data-stu-id="95c84-205">LVM/RAID Arrays</span></span>

<span data-ttu-id="95c84-206">Linux mantıksal birim Yöneticisi (LVM) ve/veya yazılım RAID diziler birden çok disk mantıksal birimleri yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="95c84-206">In Linux, Logical volume manager (LVM) and/or software RAID Arrays are used to manage logical volumes over multiple disks.</span></span> <span data-ttu-id="95c84-207">Yedeklenen Linux VM LVM ve/veya RAID dizileri kullanıyorsa, aynı VM üzerinde komut dosyası çalıştırılamaz.</span><span class="sxs-lookup"><span data-stu-id="95c84-207">If the backed up Linux VM uses LVM and/or RAID Arrays, you can't run the script on the same VM.</span></span> <span data-ttu-id="95c84-208">Bunun yerine uyumlu işletim sistemi ile diğer herhangi bir makinede komut dosyasını çalıştırmak ve hangi dosya sistemi yedeklenen VM destekler.</span><span class="sxs-lookup"><span data-stu-id="95c84-208">Instead run the script on any other machine with compatible OS and which supports filesystem of the backed up VM.</span></span>

<span data-ttu-id="95c84-209">Komut dosyası çıkışını LVM ve/veya RAID dizileri diskleri ve birimleri bölüm türü ile aşağıda gösterildiği gibi görüntüler</span><span class="sxs-lookup"><span data-stu-id="95c84-209">The script output displays the LVM and/or RAID Arrays disks and the volumes with the partition type as shown below</span></span>

   ![Linux LVM çıktı Dikey penceresi](./media/backup-azure-restore-files-from-vm/linux-LVMOutput.png)
   
<span data-ttu-id="95c84-211">Aşağıdaki komutlar, bu bölümler çevrimiçi duruma getirmek için kullanıcı tarafından çalıştırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="95c84-211">The following commands need to be run by the user to bring these partitions online.</span></span> 

<span data-ttu-id="95c84-212">**LVM bölümler için**</span><span class="sxs-lookup"><span data-stu-id="95c84-212">**For LVM Partitions**</span></span>

```
$ pvs <volume name as shown above in the script output> 
```
<span data-ttu-id="95c84-213">Birim grubu adları fiziksel bir birimi altında listelenir.</span><span class="sxs-lookup"><span data-stu-id="95c84-213">This lists the volume group names under a physical volume.</span></span>

```
$ lvdisplay <volume-group-name from the pvs command’s results> 
```
<span data-ttu-id="95c84-214">Bu, tüm mantıksal birimleri, adlarının ve yollarının bir birim grubundaki listeler.</span><span class="sxs-lookup"><span data-stu-id="95c84-214">This lists all logical volumes, names and their paths in a volume group.</span></span>

```
$ mount <LV path> </mountpath>
```
<span data-ttu-id="95c84-215">Tercih ettiğiniz yolu mantıksal birimlere bağlamak için.</span><span class="sxs-lookup"><span data-stu-id="95c84-215">To mount the logical volumes to the path of your choice.</span></span>


<span data-ttu-id="95c84-216">**RAID diziler için**</span><span class="sxs-lookup"><span data-stu-id="95c84-216">**For RAID Arrays**</span></span>

```
$ mdadm –detail –scan
```
<span data-ttu-id="95c84-217">Bu, tüm RAID disklerini hakkındaki ayrıntıları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="95c84-217">This displays details about all raid disks.</span></span> <span data-ttu-id="95c84-218">İlgili RAID disk olarak görüntülenir`/dev/mdm/<RAID array name in the backed up VM>`</span><span class="sxs-lookup"><span data-stu-id="95c84-218">The relevant RAID disk will be displayed as `/dev/mdm/<RAID array name in the backed up VM>`</span></span>

<span data-ttu-id="95c84-219">RAID disk fiziksel birim varsa bağlama komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="95c84-219">Use the mount command if the RAID disk has physical volumes.</span></span>
```
$ mount [RAID Disk Path] [/mounthpath]
```

<span data-ttu-id="95c84-220">Bu RAID disk sonra yukarıda LVM bölümler için RAID Disk adı olan birim adı ile ana hatlarıyla aynı yordamı izleyin içinde yapılandırılmış başka bir LVM varsa</span><span class="sxs-lookup"><span data-stu-id="95c84-220">If this RAID disk has another LVM configured in it then follow the same procedure as outlined above for LVM partitions with the volume name being the RAID Disk name</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="95c84-221">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="95c84-221">Troubleshooting</span></span>

<span data-ttu-id="95c84-222">Sanal makinelerden dosyalar kurtarılırken sorunlarınız varsa, ek bilgi için aşağıdaki tabloya bakın.</span><span class="sxs-lookup"><span data-stu-id="95c84-222">If you have problems while recovering files from the virtual machines, check the following table for additional information.</span></span>

| <span data-ttu-id="95c84-223">Hata iletisi / senaryosu</span><span class="sxs-lookup"><span data-stu-id="95c84-223">Error Message / Scenario</span></span> | <span data-ttu-id="95c84-224">Olası neden</span><span class="sxs-lookup"><span data-stu-id="95c84-224">Probable Cause</span></span> | <span data-ttu-id="95c84-225">Önerilen eylem</span><span class="sxs-lookup"><span data-stu-id="95c84-225">Recommended action</span></span> |
| ------------------------ | -------------- | ------------------ |
| <span data-ttu-id="95c84-226">Exe çıktı: *hedef bağlanma özel durumu*</span><span class="sxs-lookup"><span data-stu-id="95c84-226">Exe output: *Exception connecting to the target*</span></span> |<span data-ttu-id="95c84-227">Komut dosyası kurtarma noktası erişebilir değil</span><span class="sxs-lookup"><span data-stu-id="95c84-227">Script is not able to access the recovery point</span></span> | <span data-ttu-id="95c84-228">Makine yukarıda bahsedilen erişim gereksinimlerini karşılayan olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="95c84-228">Check whether the machine fulfills the access requirements mentioned above</span></span>|  
|   <span data-ttu-id="95c84-229">Exe çıktı: *hedef zaten İSCSI oturumu aracılığıyla oturum açıldı.*</span><span class="sxs-lookup"><span data-stu-id="95c84-229">Exe output: *The target has already been logged in via an ISCSI session.*</span></span> | <span data-ttu-id="95c84-230">Komut dosyası, zaten aynı makinede yürütülen ve sürücüleri bağlı</span><span class="sxs-lookup"><span data-stu-id="95c84-230">The script was already executed on the same machine and the drives have been attached</span></span> | <span data-ttu-id="95c84-231">Kurtarma noktası birimleri zaten eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="95c84-231">The volumes of the recovery point have already been attached.</span></span> <span data-ttu-id="95c84-232">Bunlar orijinal VM ile aynı sürücü harflerini takılması değil.</span><span class="sxs-lookup"><span data-stu-id="95c84-232">They may NOT be mounted with the same drive letters of the original VM.</span></span> <span data-ttu-id="95c84-233">Kullanılabilir tüm birimleri dosyanız için dosya Gezgini'nde göz atın</span><span class="sxs-lookup"><span data-stu-id="95c84-233">Browse through all the available volumes in the file explorer for your file</span></span> |
| <span data-ttu-id="95c84-234">Exe çıktı: *diskleri portal/aşıldı 12 hr sınırı çıkarılmış için bu komut dosyası geçersiz. Lütfen yeni bir betik Portalı'ndan yükleyin.*</span><span class="sxs-lookup"><span data-stu-id="95c84-234">Exe output: *This script is invalid because the disks have been dismounted via portal/exceeded the 12-hr limit. Please download a new script from the portal.*</span></span> |  <span data-ttu-id="95c84-235">Diskleri portal ya da 12 hr sınırı aşıldı çıkarıldı</span><span class="sxs-lookup"><span data-stu-id="95c84-235">The disks have been dismounted from the portal or the 12-hr limit exceeded</span></span> |    <span data-ttu-id="95c84-236">Bu belirli exe artık geçersiz ve çalıştırılamaz.</span><span class="sxs-lookup"><span data-stu-id="95c84-236">This particular exe is now invalid and can’t be run.</span></span> <span data-ttu-id="95c84-237">Bu kurtarma noktasını zaman dosyalara erişmek isterseniz yeni bir exe portalını ziyaret edin</span><span class="sxs-lookup"><span data-stu-id="95c84-237">If you want to access the files of that recovery point-in-time, visit the portal for a new exe</span></span>|
| <span data-ttu-id="95c84-238">Exe çalıştırdığı makinede: yeni birimleri çıkarma düğmesine tıklandığında sonra çıkarılmış değil</span><span class="sxs-lookup"><span data-stu-id="95c84-238">On the machine where the exe is run: The new volumes are not dismounted after the dismount button is clicked</span></span> |    <span data-ttu-id="95c84-239">İSCSI Başlatıcısı makinede değil yanıt/yenileme bağlantısı hedef için ve önbellek Bakımı</span><span class="sxs-lookup"><span data-stu-id="95c84-239">The ISCSI initiator on the machine is not responding/refreshing its connection to the target and maintaining the cache</span></span> |    <span data-ttu-id="95c84-240">Çıkarma düğmesine basıldığında sonra için bazı dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="95c84-240">Wait for some mins after the dismount button is pressed.</span></span> <span data-ttu-id="95c84-241">Yeni birimlere hala çıkarılmış değil, tüm birimler üzerinden göz atın.</span><span class="sxs-lookup"><span data-stu-id="95c84-241">If the new volumes are still not dismounted, please browse through all the volumes.</span></span> <span data-ttu-id="95c84-242">Bu bağlantıyı yenilemek için Başlatıcı zorlar ve birim diskin kullanılabilir olmadığından bir hata iletisi ile çıkarıldı</span><span class="sxs-lookup"><span data-stu-id="95c84-242">This forces the initiator to refresh the connection and the volume is dismounted with an error message that the disk is not available</span></span>|
| <span data-ttu-id="95c84-243">Exe çıktı: komut dosyası başarıyla çalıştırıldı ancak "Yeni birimlerin bağlı" komut dosyası çıktı görüntülenmez</span><span class="sxs-lookup"><span data-stu-id="95c84-243">Exe output: Script is run successfully but “New volumes attached” is not displayed on the script output</span></span> | <span data-ttu-id="95c84-244">Bu geçici bir hatadır</span><span class="sxs-lookup"><span data-stu-id="95c84-244">This is a transient error</span></span>   | <span data-ttu-id="95c84-245">Birimleri zaten eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="95c84-245">The volumes would have been already attached.</span></span> <span data-ttu-id="95c84-246">Göz atmak için Explorer'ı açın.</span><span class="sxs-lookup"><span data-stu-id="95c84-246">Open Explorer to browse.</span></span> <span data-ttu-id="95c84-247">Her komut dosyaları çalıştırmak için aynı makine kullanıyorsanız, makinenin yeniden başlatılması göz önünde bulundurun ve liste sonraki exe çalıştırmalarında görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="95c84-247">If you are using the same machine for running scripts every time, consider restarting the machine and the list should be displayed in the subsequent exe runs.</span></span> |
| <span data-ttu-id="95c84-248">Linux özel: İstenen birimleri görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="95c84-248">Linux specific: Not able to view the desired volumes</span></span> | <span data-ttu-id="95c84-249">Komut dosyası çalıştırdığı makine işletim sistemini temel alınan dosya sistemi yedeklenen VM tanımıyor olabilir</span><span class="sxs-lookup"><span data-stu-id="95c84-249">The OS of the machine where the script is run may not recognize the underlying filesystem of the backed up VM</span></span> | <span data-ttu-id="95c84-250">Kurtarma noktası kilitlenme tutarlı veya dosya tutarlı olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="95c84-250">Check whether the recovery point is crash consistent or file-consistent.</span></span> <span data-ttu-id="95c84-251">Yedeklenen dosya tutarlı, başka bir komut dosyasını çalıştırmak, işletim sistemi makine varsa VM'in filesystem tanır</span><span class="sxs-lookup"><span data-stu-id="95c84-251">If file consistent, run the script on another machine whose OS recognizes the backed up VM's filesystem</span></span> |
| <span data-ttu-id="95c84-252">Windows özel: İstenen birimleri görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="95c84-252">Windows specific: Not able to view the desired volumes</span></span> | <span data-ttu-id="95c84-253">Diskleri ekli ancak birimleri değil yapılandırılmamış</span><span class="sxs-lookup"><span data-stu-id="95c84-253">The disks may have been attached but the volumes were not configured</span></span> | <span data-ttu-id="95c84-254">Disk yönetimi ekranından kurtarma noktasıyla ilgili ek diskleri belirleyin.</span><span class="sxs-lookup"><span data-stu-id="95c84-254">From the disk management screen, identify the additional disks related to the recovery point.</span></span> <span data-ttu-id="95c84-255">Bu diskleri olarak çevrimdışı olan durumu çevrimiçi disk üzerinde sağ tıklayarak artırmayı deneyin ve 'Çevrimiçi' tıklayın</span><span class="sxs-lookup"><span data-stu-id="95c84-255">If any of these disks are in offline state try making them online by right-clicking on the disk and click 'Online'</span></span>|
