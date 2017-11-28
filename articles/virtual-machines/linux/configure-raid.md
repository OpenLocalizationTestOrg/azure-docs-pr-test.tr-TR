---
title: "aaaConfigure yazılım RAID Linux çalıştıran bir sanal makinede | Microsoft Docs"
description: "Nasıl toouse mdadm tooconfigure RAID Linux Azure üzerinde öğrenin."
services: virtual-machines-linux
documentationcenter: na
author: rickstercdn
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: f3cb2786-bda6-4d2c-9aaf-2db80f490feb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: rclaus
ms.openlocfilehash: f06e2679d953faf88ffee9991226cdb3cc1cbdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="27660-103">Linux’ta Yazılım RAID yapılandırma</span><span class="sxs-lookup"><span data-stu-id="27660-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="27660-104">Yaygın bir senaryo toouse yazılım RAID Linux sanal makinelerde tek bir RAID aygıt olarak birden çok ekli veri diskleri Azure toopresent ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="27660-104">It's a common scenario toouse software RAID on Linux virtual machines in Azure toopresent multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="27660-105">Genellikle bu kullanılan tooimprove performans ve işleme toousing yalnızca tek bir disk karşılaştırıldığında geliştirilmiş için izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27660-105">Typically this can be used tooimprove performance and allow for improved throughput compared toousing just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="27660-106">Veri diskleri ekleme</span><span class="sxs-lookup"><span data-stu-id="27660-106">Attaching data disks</span></span>
<span data-ttu-id="27660-107">İki veya daha fazla boş veri diskleri gerekli tooconfigure RAID aygıtı içindir.</span><span class="sxs-lookup"><span data-stu-id="27660-107">Two or more empty data disks are needed tooconfigure a RAID device.</span></span>  <span data-ttu-id="27660-108">RAID aygıtı oluşturmak için hello birincil tooimprove, disk g/ç performansını nedenidir.</span><span class="sxs-lookup"><span data-stu-id="27660-108">hello primary reason for creating a RAID device is tooimprove performance of your disk IO.</span></span>  <span data-ttu-id="27660-109">G/ç gereksinimlerinize bağlı olarak, standart bizim depolama biriminde, too500 GÇ/ps disk veya too5000 GÇ/ps disk başına yukarı bizim Premium storage ile başına yukarı ile depolanan tooattach diskleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27660-109">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="27660-110">Bu makalede nasıl ayrıntıya geçmez tooprovision ve veri diskleri tooa Linux sanal makine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="27660-110">This article does not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span>  <span data-ttu-id="27660-111">Bkz: hello Microsoft Azure makale [bir diski kullanıma açın](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) nasıl tooattach boş bir veri diski tooa Linux sanal makine Azure ile ilgili ayrıntılı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="27660-111">See hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-mdadm-utility"></a><span data-ttu-id="27660-112">Merhaba mdadm yardımcı programını yükleyin</span><span class="sxs-lookup"><span data-stu-id="27660-112">Install hello mdadm utility</span></span>
* <span data-ttu-id="27660-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="27660-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="27660-114">**CentOS & Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="27660-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="27660-115">**SLES ve openSUSE**</span><span class="sxs-lookup"><span data-stu-id="27660-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a><span data-ttu-id="27660-116">Merhaba disk bölümleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="27660-116">Create hello disk partitions</span></span>
<span data-ttu-id="27660-117">Bu örnekte, /dev/sdc üzerinde tek disk bölümü oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="27660-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="27660-118">Merhaba yeni disk bölümü /dev/sdc1 çağrılır.</span><span class="sxs-lookup"><span data-stu-id="27660-118">hello new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="27660-119">Başlat `fdisk` toobegin bölümleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="27660-119">Start `fdisk` toobegin creating partitions</span></span>

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide toowrite them.
    After that, of course, hello previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off hello mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. <span data-ttu-id="27660-120">Tuşuna 'n' hello komut istemi toocreate konumunda bir  **n** eni bölüm:</span><span class="sxs-lookup"><span data-stu-id="27660-120">Press 'n' at hello prompt toocreate a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="27660-121">Ardından, 'p' toocreate'e basın bir **p**birincil bölüm:</span><span class="sxs-lookup"><span data-stu-id="27660-121">Next, press 'p' toocreate a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="27660-122">'1' tooselect bölüm numarası 1 tuşuna basın:</span><span class="sxs-lookup"><span data-stu-id="27660-122">Press '1' tooselect partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="27660-123">Select hello hello yeni bölüm basın veya başlangıç noktası `<enter>` tooaccept hello varsayılan tooplace hello bölüm hello başında hello hello sürücüdeki boş disk alanı:</span><span class="sxs-lookup"><span data-stu-id="27660-123">Select hello starting point of hello new partition, or press `<enter>` tooaccept hello default tooplace hello partition at hello beginning of hello free space on hello drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="27660-124">Merhaba bölümü, örneğin türü '+10G' toocreate 10 gigabayt bölüm Hello boyutunu seçin.</span><span class="sxs-lookup"><span data-stu-id="27660-124">Select hello size of hello partition, for example type '+10G' toocreate a 10 gigabyte partition.</span></span> <span data-ttu-id="27660-125">Veya basın `<enter>` hello sürücünün tamamını kapsayan tek bir bölüm oluşturun:</span><span class="sxs-lookup"><span data-stu-id="27660-125">Or, press `<enter>` create a single partition that spans hello entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="27660-126">Ardından, hello Kimliğini değiştirin ve **t**türü hello varsayılan hello bölümünün Kimliği '83' (Linux) tooID 'fd' (Linux RAID otomatik):</span><span class="sxs-lookup"><span data-stu-id="27660-126">Next, change hello ID and **t**ype of hello partition from hello default ID '83' (Linux) tooID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. <span data-ttu-id="27660-127">Son olarak, hello bölüm tablo toohello sürücüsü yazmak ve fdisk Çık:</span><span class="sxs-lookup"><span data-stu-id="27660-127">Finally, write hello partition table toohello drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a><span data-ttu-id="27660-128">Merhaba RAID dizisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="27660-128">Create hello RAID array</span></span>
1. <span data-ttu-id="27660-129">Aşağıdaki örnek "stripe üç bölüm üç ayrı veri disk üzerinde (sdc1, sdd1, sde1) bulunan" (RAID Düzey 0) hello.</span><span class="sxs-lookup"><span data-stu-id="27660-129">hello following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="27660-130">Adlı yeni bir RAID cihaz bu komutu çalıştırdıktan sonra **/dev/md127** oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="27660-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="27660-131">Ayrıca bu veri diskleri, biz daha önce başka bir geçersiz RAID dizisi parçası, gerekli tooadd hello olabileceğine dikkat edin `--force` parametresi toohello `mdadm` komutu:</span><span class="sxs-lookup"><span data-stu-id="27660-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary tooadd hello `--force` parameter toohello `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="27660-132">Merhaba yeni RAID aygıtta Hello dosya sistemi oluşturma</span><span class="sxs-lookup"><span data-stu-id="27660-132">Create hello file system on hello new RAID device</span></span>
   
    <span data-ttu-id="27660-133">a.</span><span class="sxs-lookup"><span data-stu-id="27660-133">a.</span></span> <span data-ttu-id="27660-134">**CentOS, Oracle Linux SLES 12, openSUSE ve Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="27660-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="27660-135">b.</span><span class="sxs-lookup"><span data-stu-id="27660-135">b.</span></span> <span data-ttu-id="27660-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="27660-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="27660-137">c.</span><span class="sxs-lookup"><span data-stu-id="27660-137">c.</span></span> <span data-ttu-id="27660-138">**SLES 11** - boot.md etkinleştirmek ve mdadm.conf oluşturma</span><span class="sxs-lookup"><span data-stu-id="27660-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="27660-139">SUSE sistemlerde bu değişiklikleri yaptıktan sonra bir yeniden başlatma gerekli olabilir.</span><span class="sxs-lookup"><span data-stu-id="27660-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="27660-140">Bu adım *değil* SLES 12 gerekli.</span><span class="sxs-lookup"><span data-stu-id="27660-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="27660-141">Merhaba yeni dosya sistemi çok/etc/fstab Ekle</span><span class="sxs-lookup"><span data-stu-id="27660-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="27660-142">Yanlış hello /etc/fstab dosyasını düzenleyerek önyüklenemez bir sisteme neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="27660-142">Improperly editing hello /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="27660-143">Emin değilseniz, bu dosyayı tooproperly düzenleme nasıl bilgi toohello dağıtım'ın belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="27660-143">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="27660-144">Ayrıca, düzenlemeye başlamadan önce hello /etc/fstab dosyanızın bir yedeğini oluşturduğunuz önerilir.</span><span class="sxs-lookup"><span data-stu-id="27660-144">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="27660-145">Örneğin, yeni bir dosya sistemi için istenen hello bağlama noktası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="27660-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="27660-146">/Etc/fstab düzenlerken hello **UUID** kullanılan tooreference hello dosya hello yerine sistem aygıt adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="27660-146">When editing /etc/fstab, hello **UUID** should be used tooreference hello file system rather than hello device name.</span></span>  <span data-ttu-id="27660-147">Kullanım hello `blkid` yardımcı programı toodetermine hello UUID hello yeni dosya sistemi için:</span><span class="sxs-lookup"><span data-stu-id="27660-147">Use hello `blkid` utility toodetermine hello UUID for hello new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="27660-148">/Etc/fstab bir metin düzenleyicisinde açın ve örneğin hello yeni dosya sistemi için bir giriş ekleyin:</span><span class="sxs-lookup"><span data-stu-id="27660-148">Open /etc/fstab in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="27660-149">Veya **SLES 11**:</span><span class="sxs-lookup"><span data-stu-id="27660-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="27660-150">Ardından, kaydedin ve /etc/fstab kapatın.</span><span class="sxs-lookup"><span data-stu-id="27660-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="27660-151">Bu hello/etc test/fstab girişi doğrudur:</span><span class="sxs-lookup"><span data-stu-id="27660-151">Test that hello /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="27660-152">Lütfen bu komutu bir hata iletisi sonuçlanırsa hello /etc/fstab dosyasında hello sözdizimini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="27660-152">If this command results in an error message, please check hello syntax in hello /etc/fstab file.</span></span>
   
    <span data-ttu-id="27660-153">Merhaba sonraki çalıştırma `mount` komutu tooensure hello dosya sistemi takılı:</span><span class="sxs-lookup"><span data-stu-id="27660-153">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="27660-154">(İsteğe bağlı) Hatasız önyükleme parametreleri</span><span class="sxs-lookup"><span data-stu-id="27660-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="27660-155">**fstab yapılandırma**</span><span class="sxs-lookup"><span data-stu-id="27660-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="27660-156">Çoğu dağıtımda ya da hello dahil `nobootwait` veya `nofail` fstab toohello/etc/dosya eklenebilir parametreleri bağlayın.</span><span class="sxs-lookup"><span data-stu-id="27660-156">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello /etc/fstab file.</span></span> <span data-ttu-id="27660-157">Bu parametreleri oluşturulamıyor tooproperly bağlama hello RAID dosya sistemi olsa bile hello Linux sistem toocontinue tooboot izin ve hataları için belirli dosya sistemi bağlarken izin verin.</span><span class="sxs-lookup"><span data-stu-id="27660-157">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="27660-158">Bu parametreler hakkında daha fazla bilgi için tooyour dağıtım'ın belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="27660-158">Refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="27660-159">Örnek (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="27660-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="27660-160">**Linux önyükleme parametreleri**</span><span class="sxs-lookup"><span data-stu-id="27660-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="27660-161">Çekirdek parametresi parametreleri yukarıda toplama toohello içinde hello "`bootdegraded=true`" Merhaba RAID olarak algılanır zarar görmesi veya hello sanal makineden bir veri sürücüsünü yanlışlıkla kaldırdıysanız örneğin düşürülmüş olsa bile hello sistem tooboot izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27660-161">In addition toohello above parameters, hello kernel parameter "`bootdegraded=true`" can allow hello system tooboot even if hello RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from hello virtual machine.</span></span> <span data-ttu-id="27660-162">Varsayılan olarak bu önyüklenebilir olmayan bir sistemi sonuçlanabilir.</span><span class="sxs-lookup"><span data-stu-id="27660-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="27660-163">Lütfen tooproperly düzenleme çekirdek parametreleri nasıl üzerinde tooyour dağıtım'ın belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="27660-163">Please refer tooyour distribution's documentation on how tooproperly edit kernel parameters.</span></span> <span data-ttu-id="27660-164">Örneğin, çoğu dağıtımda (CentOS, Oracle Linux, SLES 11) Bu parametreleri el ile toohello eklenebilir "`/boot/grub/menu.lst`" dosya.</span><span class="sxs-lookup"><span data-stu-id="27660-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually toohello "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="27660-165">Bu parametre toohello üzerinde ubuntu eklenebilir `GRUB_CMDLINE_LINUX_DEFAULT` değişkeninin "/ etc/varsayılan/kaz".</span><span class="sxs-lookup"><span data-stu-id="27660-165">On Ubuntu this parameter can be added toohello `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="27660-166">KIRPMA/UNMAP desteği</span><span class="sxs-lookup"><span data-stu-id="27660-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="27660-167">Bazı Linux tekrar KIRPMA/UNMAP işlemleri toodiscard destek hello diskte kullanılmayan engeller.</span><span class="sxs-lookup"><span data-stu-id="27660-167">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="27660-168">Bu işlemler sayfaları silinmiş Azure artık geçerli değil ve iptal edilecek standart depolama tooinform öncelikle faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="27660-168">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="27660-169">Büyük dosyaları oluşturmak ve bunları silerseniz sayfaları atılıyor maliyet kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27660-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="27660-170">Merhaba öbek boyutunu hello dizisi için tooless hello varsayılan (512 KB) daha ayarlarsanız RAID atma komutları verin değil.</span><span class="sxs-lookup"><span data-stu-id="27660-170">RAID may not issue discard commands if hello chunk size for hello array is set tooless than hello default (512KB).</span></span> <span data-ttu-id="27660-171">Merhaba eşlemesini olmasıdır ayrıntı düzeyi hello ana bilgisayar üzerinde değil de 512KB.</span><span class="sxs-lookup"><span data-stu-id="27660-171">This is because hello unmap granularity on hello Host is also 512KB.</span></span> <span data-ttu-id="27660-172">Merhaba dizinin öbek boyutu mdadm'ın aracılığıyla değiştirilmiş varsa `--chunk=` parametresi sonra KIRPMA ve eşlemesini istekleri hello çekirdekten dikkate.</span><span class="sxs-lookup"><span data-stu-id="27660-172">If you modified hello array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by hello kernel.</span></span>

<span data-ttu-id="27660-173">Tooenable KIRPMA desteği, Linux VM'NİZDE iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="27660-173">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="27660-174">Her zamanki gibi dağıtımınız için önerilen yaklaşımı hello bakın:</span><span class="sxs-lookup"><span data-stu-id="27660-174">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="27660-175">Kullanım hello `discard` bağlama seçeneği `/etc/fstab`, örneğin:</span><span class="sxs-lookup"><span data-stu-id="27660-175">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="27660-176">Bazı durumlarda hello içinde `discard` seçeneği performans etkileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="27660-176">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="27660-177">Alternatif olarak, hello çalıştırabilirsiniz `fstrim` komutunu el ile Merhaba komut satırından veya tooyour crontab toorun düzenli olarak ekleyin:</span><span class="sxs-lookup"><span data-stu-id="27660-177">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="27660-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="27660-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="27660-179">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="27660-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
