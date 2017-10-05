---
title: "Yazılım RAID Linux çalıştıran bir sanal makinede yapılandırmak | Microsoft Docs"
description: "Mdadm Azure'da RAID Linux'ta yapılandırmak için nasıl kullanılacağını öğrenin."
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
ms.openlocfilehash: 12f540a700fbf85e579e8aadc9f6def039299ff7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="968fa-103">Linux’ta Yazılım RAID yapılandırma</span><span class="sxs-lookup"><span data-stu-id="968fa-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="968fa-104">Yazılım RAID Linux sanal makinelerde tek bir RAID aygıt olarak birden çok eklenen veri disklerini sunmak için Azure içinde kullanmak için ortak bir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="968fa-104">It's a common scenario to use software RAID on Linux virtual machines in Azure to present multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="968fa-105">Genellikle bu performansı artırmak ve yalnızca tek bir disk kullanmaya kıyasla geliştirilmiş işleme için izin vermek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="968fa-105">Typically this can be used to improve performance and allow for improved throughput compared to using just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="968fa-106">Veri diskleri ekleme</span><span class="sxs-lookup"><span data-stu-id="968fa-106">Attaching data disks</span></span>
<span data-ttu-id="968fa-107">İki veya daha fazla boş veri diskler, RAID aygıtı yapılandırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="968fa-107">Two or more empty data disks are needed to configure a RAID device.</span></span>  <span data-ttu-id="968fa-108">Disk GÇ performansı artırmak için bir RAID aygıtı oluşturmak için birincil nedeni olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="968fa-108">The primary reason for creating a RAID device is to improve performance of your disk IO.</span></span>  <span data-ttu-id="968fa-109">G/ç gereksinimlerinize bağlı olarak, en fazla 500 GÇ/ps disk veya bizim Premium storage başına disk başına en fazla 5000 GÇ/ps ile bizim standart depolamada depolanan diskleri ekleme seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="968fa-109">Based on your IO needs, you can choose to attach disks that are stored in our Standard Storage, with up to 500 IO/ps per disk or our Premium storage with up to 5000 IO/ps per disk.</span></span> <span data-ttu-id="968fa-110">Bu makalede, sağlamak ve veri diskleri için Linux sanal makine ekleme konusunda ayrıntıya geçmez.</span><span class="sxs-lookup"><span data-stu-id="968fa-110">This article does not go into detail on how to provision and attach data disks to a Linux virtual machine.</span></span>  <span data-ttu-id="968fa-111">Microsoft Azure makalesine bakın [bir diski kullanıma açın](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Azure Linux sanal makinede boş veri diski ekleme konusunda ayrıntılı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="968fa-111">See the Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how to attach an empty data disk to a Linux virtual machine on Azure.</span></span>

## <a name="install-the-mdadm-utility"></a><span data-ttu-id="968fa-112">Mdadm yardımcı programını yükleyin</span><span class="sxs-lookup"><span data-stu-id="968fa-112">Install the mdadm utility</span></span>
* <span data-ttu-id="968fa-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="968fa-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="968fa-114">**CentOS & Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="968fa-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="968fa-115">**SLES ve openSUSE**</span><span class="sxs-lookup"><span data-stu-id="968fa-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-the-disk-partitions"></a><span data-ttu-id="968fa-116">Disk bölümleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="968fa-116">Create the disk partitions</span></span>
<span data-ttu-id="968fa-117">Bu örnekte, /dev/sdc üzerinde tek disk bölümü oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="968fa-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="968fa-118">Yeni disk bölümü /dev/sdc1 çağrılır.</span><span class="sxs-lookup"><span data-stu-id="968fa-118">The new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="968fa-119">Başlat `fdisk` bölümleri oluşturmaya başlamak için</span><span class="sxs-lookup"><span data-stu-id="968fa-119">Start `fdisk` to begin creating partitions</span></span>

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide to write them.
    After that, of course, the previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off the mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. <span data-ttu-id="968fa-120">Tuşuna 'n' oluşturmak için komut istemine bir  **n** eni bölüm:</span><span class="sxs-lookup"><span data-stu-id="968fa-120">Press 'n' at the prompt to create a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="968fa-121">Ardından, oluşturmak için ' p' tuşuna basın. bir **p**birincil bölüm:</span><span class="sxs-lookup"><span data-stu-id="968fa-121">Next, press 'p' to create a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="968fa-122">Bölüm numarası 1 seçmek için '1' tuşuna basın:</span><span class="sxs-lookup"><span data-stu-id="968fa-122">Press '1' to select partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="968fa-123">Yeni bölüm veya tuşuna başlangıç noktasını seçin `<enter>` sürücüdeki boş alan başına bölüm yerleştirmek için Varsayılanı kabul etmek için:</span><span class="sxs-lookup"><span data-stu-id="968fa-123">Select the starting point of the new partition, or press `<enter>` to accept the default to place the partition at the beginning of the free space on the drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="968fa-124">Bölümün boyutunu seçin, örneğin bir 10 gigabayt bölüm oluşturmak için ' +10G' yazın.</span><span class="sxs-lookup"><span data-stu-id="968fa-124">Select the size of the partition, for example type '+10G' to create a 10 gigabyte partition.</span></span> <span data-ttu-id="968fa-125">Veya basın `<enter>` sürücünün tamamını kapsayan tek bir bölüm oluşturun:</span><span class="sxs-lookup"><span data-stu-id="968fa-125">Or, press `<enter>` create a single partition that spans the entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="968fa-126">Ardından, Tanıtıcıyı değiştirin ve **t**türü bölümün varsayılan Kimliği '83' nden (Linux) kimliği 'fd' (Linux RAID otomatik):</span><span class="sxs-lookup"><span data-stu-id="968fa-126">Next, change the ID and **t**ype of the partition from the default ID '83' (Linux) to ID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L to list codes): fd
    ```

8. <span data-ttu-id="968fa-127">Son olarak, bölümleme tablosu diske yazma ve fdisk Çık:</span><span class="sxs-lookup"><span data-stu-id="968fa-127">Finally, write the partition table to the drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    The partition table has been altered!
    ```

## <a name="create-the-raid-array"></a><span data-ttu-id="968fa-128">RAID dizisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="968fa-128">Create the RAID array</span></span>
1. <span data-ttu-id="968fa-129">Aşağıdaki örnek "stripe üç bölüm üç ayrı veri disk üzerinde (sdc1, sdd1, sde1) bulunan" (RAID Düzey 0).</span><span class="sxs-lookup"><span data-stu-id="968fa-129">The following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="968fa-130">Adlı yeni bir RAID cihaz bu komutu çalıştırdıktan sonra **/dev/md127** oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="968fa-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="968fa-131">Ayrıca bu veri diskleri, biz daha önce başka bir geçersiz RAID dizisi parçası onu eklemek için gereken olabileceğine dikkat edin `--force` parametresi `mdadm` komutu:</span><span class="sxs-lookup"><span data-stu-id="968fa-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary to add the `--force` parameter to the `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="968fa-132">Dosya sistemi yeni RAID cihazda oluştur</span><span class="sxs-lookup"><span data-stu-id="968fa-132">Create the file system on the new RAID device</span></span>
   
    <span data-ttu-id="968fa-133">a.</span><span class="sxs-lookup"><span data-stu-id="968fa-133">a.</span></span> <span data-ttu-id="968fa-134">**CentOS, Oracle Linux SLES 12, openSUSE ve Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="968fa-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="968fa-135">b.</span><span class="sxs-lookup"><span data-stu-id="968fa-135">b.</span></span> <span data-ttu-id="968fa-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="968fa-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="968fa-137">c.</span><span class="sxs-lookup"><span data-stu-id="968fa-137">c.</span></span> <span data-ttu-id="968fa-138">**SLES 11** - boot.md etkinleştirmek ve mdadm.conf oluşturma</span><span class="sxs-lookup"><span data-stu-id="968fa-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="968fa-139">SUSE sistemlerde bu değişiklikleri yaptıktan sonra bir yeniden başlatma gerekli olabilir.</span><span class="sxs-lookup"><span data-stu-id="968fa-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="968fa-140">Bu adım *değil* SLES 12 gerekli.</span><span class="sxs-lookup"><span data-stu-id="968fa-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-the-new-file-system-to-etcfstab"></a><span data-ttu-id="968fa-141">Yeni dosya sistemi için /etc/fstab Ekle</span><span class="sxs-lookup"><span data-stu-id="968fa-141">Add the new file system to /etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="968fa-142">Yanlış /etc/fstab dosyasını düzenleyerek önyüklenemez bir sisteme neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="968fa-142">Improperly editing the /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="968fa-143">Emin değilseniz, düzgün şekilde bu dosyayı düzenlemek hakkında bilgi için dağıtım 's belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="968fa-143">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="968fa-144">Ayrıca, düzenlemeye başlamadan önce /etc/fstab dosyanızın bir yedeğini oluşturduğunuz önerilir.</span><span class="sxs-lookup"><span data-stu-id="968fa-144">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="968fa-145">Örneğin, yeni bir dosya sistemi için istenen bağlama noktası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="968fa-145">Create the desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="968fa-146">/Etc/fstab, düzenlerken **UUID** aygıt adı yerine dosya sistemine başvurmak için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="968fa-146">When editing /etc/fstab, the **UUID** should be used to reference the file system rather than the device name.</span></span>  <span data-ttu-id="968fa-147">Kullanım `blkid` yeni dosya sistemi için UUID belirlemeye yardımcı programı:</span><span class="sxs-lookup"><span data-stu-id="968fa-147">Use the `blkid` utility to determine the UUID for the new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="968fa-148">/Etc/fstab bir metin düzenleyicisinde açın ve yeni dosya sistemi için bir giriş örneğin ekleyin:</span><span class="sxs-lookup"><span data-stu-id="968fa-148">Open /etc/fstab in a text editor and add an entry for the new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="968fa-149">Veya **SLES 11**:</span><span class="sxs-lookup"><span data-stu-id="968fa-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="968fa-150">Ardından, kaydedin ve /etc/fstab kapatın.</span><span class="sxs-lookup"><span data-stu-id="968fa-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="968fa-151">/ Etc/fstab girişin doğru olduğunu sınayın:</span><span class="sxs-lookup"><span data-stu-id="968fa-151">Test that the /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="968fa-152">Bu komutu bir hata iletisi sonuçlanırsa, lütfen /etc/fstab dosyasında sözdizimini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="968fa-152">If this command results in an error message, please check the syntax in the /etc/fstab file.</span></span>
   
    <span data-ttu-id="968fa-153">Sonraki çalıştırma `mount` komutu dosya sistemi takılı emin olun:</span><span class="sxs-lookup"><span data-stu-id="968fa-153">Next run the `mount` command to ensure the file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="968fa-154">(İsteğe bağlı) Hatasız önyükleme parametreleri</span><span class="sxs-lookup"><span data-stu-id="968fa-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="968fa-155">**fstab yapılandırma**</span><span class="sxs-lookup"><span data-stu-id="968fa-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="968fa-156">Çoğu dağıtımda ya da dahil `nobootwait` veya `nofail` bağlama/etc/fstab dosyasına eklenen parametreleri.</span><span class="sxs-lookup"><span data-stu-id="968fa-156">Many distributions include either the `nobootwait` or `nofail` mount parameters that may be added to the /etc/fstab file.</span></span> <span data-ttu-id="968fa-157">Bu parametreler belirli dosya sistemi bağlanması gerektiğinde hataları için izin ve Linux sistemin düzgün RAID dosya sistemi bağlama alamıyor olsa bile önyüklemeye devam etmesini izin ver.</span><span class="sxs-lookup"><span data-stu-id="968fa-157">These parameters allow for failures when mounting a particular file system and allow the Linux system to continue to boot even if it is unable to properly mount the RAID file system.</span></span> <span data-ttu-id="968fa-158">Bu parametreler hakkında daha fazla bilgi için dağıtım 's belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="968fa-158">Refer to your distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="968fa-159">Örnek (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="968fa-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="968fa-160">**Linux önyükleme parametreleri**</span><span class="sxs-lookup"><span data-stu-id="968fa-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="968fa-161">Yukarıdaki parametreler, çekirdek parametresi ek olarak "`bootdegraded=true`" sanal makineden bir veri sürücüsünü yanlışlıkla kaldırdıysanız RAID zarar görmüş veya düşürülmüş için örnek olarak algılanan olsa bile önyükleme sisteme izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="968fa-161">In addition to the above parameters, the kernel parameter "`bootdegraded=true`" can allow the system to boot even if the RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from the virtual machine.</span></span> <span data-ttu-id="968fa-162">Varsayılan olarak bu önyüklenebilir olmayan bir sistemi sonuçlanabilir.</span><span class="sxs-lookup"><span data-stu-id="968fa-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="968fa-163">Lütfen düzgün çekirdek parametrelerini düzenlemek nasıl dağıtım 's belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="968fa-163">Please refer to your distribution's documentation on how to properly edit kernel parameters.</span></span> <span data-ttu-id="968fa-164">Örneğin, çoğu dağıtımda (CentOS, Oracle Linux, SLES 11) Bu parametreleri el ile çok eklenebilir "`/boot/grub/menu.lst`" dosya.</span><span class="sxs-lookup"><span data-stu-id="968fa-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually to the "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="968fa-165">Ubuntu üzerinde bu parametreyi eklenebilir `GRUB_CMDLINE_LINUX_DEFAULT` değişkeninin "/ etc/varsayılan/kaz".</span><span class="sxs-lookup"><span data-stu-id="968fa-165">On Ubuntu this parameter can be added to the `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="968fa-166">KIRPMA/UNMAP desteği</span><span class="sxs-lookup"><span data-stu-id="968fa-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="968fa-167">Bazı Linux tekrar disk üzerindeki kullanılmayan blokları atmak için KIRPMA/UNMAP işlemleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="968fa-167">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="968fa-168">Bu işlemler sayfaları silinmiş Azure artık geçerli değil ve iptal edilecek bildirmek için standart depolama öncelikle faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="968fa-168">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="968fa-169">Büyük dosyaları oluşturmak ve bunları silerseniz sayfaları atılıyor maliyet kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="968fa-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="968fa-170">Dizi öbek boyutu (512 KB) varsayılan değerinden ayarlanırsa RAID atma komutları verin değil.</span><span class="sxs-lookup"><span data-stu-id="968fa-170">RAID may not issue discard commands if the chunk size for the array is set to less than the default (512KB).</span></span> <span data-ttu-id="968fa-171">Ana bilgisayarda unmap ayrıntı düzeyi de 512 KB olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="968fa-171">This is because the unmap granularity on the Host is also 512KB.</span></span> <span data-ttu-id="968fa-172">Dizinin öbek boyutu mdadm'ın aracılığıyla değiştirilmiş varsa `--chunk=` parametresi sonra KIRPMA ve eşlemesini istekleri çekirdekten dikkate.</span><span class="sxs-lookup"><span data-stu-id="968fa-172">If you modified the array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by the kernel.</span></span>

<span data-ttu-id="968fa-173">KIRPMA etkinleştirmenin iki yolu desteği, Linux VM'NİZDE vardır.</span><span class="sxs-lookup"><span data-stu-id="968fa-173">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="968fa-174">Her zamanki gibi dağıtımınız için önerilen yaklaşım bakın:</span><span class="sxs-lookup"><span data-stu-id="968fa-174">As usual, consult your distribution for the recommended approach:</span></span>

- <span data-ttu-id="968fa-175">Kullanım `discard` bağlama seçeneği `/etc/fstab`, örneğin:</span><span class="sxs-lookup"><span data-stu-id="968fa-175">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="968fa-176">Bazı durumlarda `discard` seçeneği performans etkileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="968fa-176">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="968fa-177">Alternatif olarak, çalıştırabilirsiniz `fstrim` komutunu el ile komut satırından veya düzenli olarak çalışacak şekilde crontab için ekleyin:</span><span class="sxs-lookup"><span data-stu-id="968fa-177">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>

    <span data-ttu-id="968fa-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="968fa-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="968fa-179">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="968fa-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
