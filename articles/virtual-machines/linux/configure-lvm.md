---
title: "Linux çalıştıran bir sanal makinede aaaConfigure LVM | Microsoft Docs"
description: "Bilgi nasıl tooconfigure LVM Linux Azure üzerinde."
services: virtual-machines-linux
documentationcenter: na
author: szarkos
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: 7f533725-1484-479d-9472-6b3098d0aecc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 8daf792d87c6bb3d91a2eddcd01cfab34fd28cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a><span data-ttu-id="5092f-103">Azure'da bir Linux VM LVM yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5092f-103">Configure LVM on a Linux VM in Azure</span></span>
<span data-ttu-id="5092f-104">Bu belgede ele alınacaktır nasıl tooconfigure mantıksal Birimi Yöneticisi (LVM), Azure sanal makinesinde.</span><span class="sxs-lookup"><span data-stu-id="5092f-104">This document will discuss how tooconfigure Logical Volume Manager (LVM) in your Azure virtual machine.</span></span> <span data-ttu-id="5092f-105">Herhangi bir disk üzerine LVM toohello sanal makine, varsayılan olarak çoğu bulut görüntüleri sahip bağlı uygun tooconfigure olsa LVM işletim sistemi diski hello üzerinde yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="5092f-105">While it is feasible tooconfigure LVM on any disk attached toohello virtual machine, by default most cloud images will not have LVM configured on hello OS disk.</span></span> <span data-ttu-id="5092f-106">İşletim sistemi diski olduğu herhangi bir zamanda hello tooanother hello VM ekli bu yinelenen birim grupları tooprevent sorunları ise aynı dağıtım ve bir kurtarma senaryosu sırasında yani türü.</span><span class="sxs-lookup"><span data-stu-id="5092f-106">This is tooprevent problems with duplicate volume groups if hello OS disk is ever attached tooanother VM of hello same distribution and type, i.e. during a recovery scenario.</span></span> <span data-ttu-id="5092f-107">Bu nedenle yalnızca toouse LVM hello veri disklerde önerilir.</span><span class="sxs-lookup"><span data-stu-id="5092f-107">Therefore it is recommended only toouse LVM on hello data disks.</span></span>

## <a name="linear-vs-striped-logical-volumes"></a><span data-ttu-id="5092f-108">Doğrusal şeritli mantıksal birimler karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="5092f-108">Linear vs. striped logical volumes</span></span>
<span data-ttu-id="5092f-109">LVM kullanılan toocombine tek bir depolama birimi içine fiziksel disk sayısını olabilir.</span><span class="sxs-lookup"><span data-stu-id="5092f-109">LVM can be used toocombine a number of physical disks into a single storage volume.</span></span> <span data-ttu-id="5092f-110">Varsayılan olarak LVM genellikle doğrusal mantıksal birimler, hello fiziksel depolama birlikte birleştirilmiş yani oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5092f-110">By default LVM will usually create linear logical volumes, which means that hello physical storage is concatenated together.</span></span> <span data-ttu-id="5092f-111">Bu durumda okuma/yazma işlemleri genellikle yalnızca tooa tek disk gönderilir.</span><span class="sxs-lookup"><span data-stu-id="5092f-111">In this case read/write operations will typically only be sent tooa single disk.</span></span> <span data-ttu-id="5092f-112">Buna karşılık, biz de okuma ve yazma işlemleri (yani benzer tooRAID0) hello birim grupta bulunan dağıtılmış toomultiple diskleri nerede şeritli mantıksal birimler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5092f-112">In contrast, we can also create striped logical volumes where reads and writes are distributed toomultiple disks contained in hello volume group (i.e. similar tooRAID0).</span></span> <span data-ttu-id="5092f-113">Olası performans nedenleriyle böylece okuma ve yazma işlemleri tüm eklenen veri disklerini kullanan mantıksal birimler toostripe isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="5092f-113">For performance reasons it is likely you will want toostripe your logical volumes so that reads and writes utilize all your attached data disks.</span></span>

<span data-ttu-id="5092f-114">Bu belge nasıl toocombine birkaç veri diskleri tek bir birimde grubuna açıklamak ve şeritli bir mantıksal birim oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5092f-114">This document will describe how toocombine several data disks into a single volume group, and then create a striped logical volume.</span></span> <span data-ttu-id="5092f-115">Merhaba aşağıdaki çoğu dağıtımları ile biraz genelleştirilmiş toowork adımlardır.</span><span class="sxs-lookup"><span data-stu-id="5092f-115">hello steps below are somewhat generalized toowork with most distributions.</span></span> <span data-ttu-id="5092f-116">Çoğu durumda hello yardımcı programları ve Azure üzerinde LVM yönetmek için iş akışları diğer ortamlara temelde farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="5092f-116">In most cases hello utilities and workflows for managing LVM on Azure are not fundamentally different than other environments.</span></span> <span data-ttu-id="5092f-117">Her zamanki gibi ayrıca Linux satıcınıza için lütfen belgeleri ve LVM belirli dağıtımınız ile kullanmak için en iyi uygulamalar danışın.</span><span class="sxs-lookup"><span data-stu-id="5092f-117">As usual, please also consult your Linux vendor for documentation and best practices for using LVM with your particular distribution.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="5092f-118">Veri diskleri ekleme</span><span class="sxs-lookup"><span data-stu-id="5092f-118">Attaching data disks</span></span>
<span data-ttu-id="5092f-119">LVM kullanırken bir genellikle iki veya daha fazla boş veri disklerle toostart isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="5092f-119">One will usually want toostart with two or more empty data disks when using LVM.</span></span> <span data-ttu-id="5092f-120">G/ç gereksinimlerinize bağlı olarak, standart bizim depolama biriminde, too500 GÇ/ps disk veya too5000 GÇ/ps disk başına yukarı bizim Premium storage ile başına yukarı ile depolanan tooattach diskleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5092f-120">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="5092f-121">Bu makalede ayrıntıya gitmek değil tooprovision ve veri diskleri tooa Linux sanal makine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5092f-121">This article will not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span> <span data-ttu-id="5092f-122">Lütfen bakın hello Microsoft Azure makale [bir diski kullanıma açın](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) nasıl tooattach boş bir veri diski tooa Linux sanal makine Azure ile ilgili ayrıntılı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="5092f-122">Please see hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-lvm-utilities"></a><span data-ttu-id="5092f-123">Merhaba LVM yardımcı programlarını yükleyin</span><span class="sxs-lookup"><span data-stu-id="5092f-123">Install hello LVM utilities</span></span>
* <span data-ttu-id="5092f-124">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="5092f-124">**Ubuntu**</span></span>

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* <span data-ttu-id="5092f-125">**RHEL, CentOS ve Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="5092f-125">**RHEL, CentOS & Oracle Linux**</span></span>

    ```bash   
    sudo yum install lvm2
    ```

* <span data-ttu-id="5092f-126">**SLES 12 ve openSUSE**</span><span class="sxs-lookup"><span data-stu-id="5092f-126">**SLES 12 and openSUSE**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

* <span data-ttu-id="5092f-127">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="5092f-127">**SLES 11**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

    <span data-ttu-id="5092f-128">Ayrıca düzenlemelisiniz üzerinde SLES11 `/etc/sysconfig/lvm` ve `LVM_ACTIVATED_ON_DISCOVERED` çok "etkinleştir":</span><span class="sxs-lookup"><span data-stu-id="5092f-128">On SLES11 you must also edit `/etc/sysconfig/lvm` and set `LVM_ACTIVATED_ON_DISCOVERED` too"enable":</span></span>

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a><span data-ttu-id="5092f-129">LVM'yi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5092f-129">Configure LVM</span></span>
<span data-ttu-id="5092f-130">Bu kılavuzda adlandırdığımız üç veri diskleri ekli varsayacağız tooas `/dev/sdc`, `/dev/sdd` ve `/dev/sde`.</span><span class="sxs-lookup"><span data-stu-id="5092f-130">In this guide we will assume you have attached three data disks, which we'll refer tooas `/dev/sdc`, `/dev/sdd` and `/dev/sde`.</span></span> <span data-ttu-id="5092f-131">Bunlar olmayabilir, Not her zaman aynı yol adları, VM'deki hello olabilir.</span><span class="sxs-lookup"><span data-stu-id="5092f-131">Note that these may not always be hello same path names in your VM.</span></span> <span data-ttu-id="5092f-132">Çalıştırabilirsiniz '`sudo fdisk -l`' veya benzer komutu toolist kullanılabilir diskler.</span><span class="sxs-lookup"><span data-stu-id="5092f-132">You can run '`sudo fdisk -l`' or similar command toolist your available disks.</span></span>

1. <span data-ttu-id="5092f-133">Merhaba fiziksel birimler hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="5092f-133">Prepare hello physical volumes:</span></span>

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. <span data-ttu-id="5092f-134">Bir birim grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5092f-134">Create a volume group.</span></span> <span data-ttu-id="5092f-135">Bu örnekte, biz hello birim grubu aradığınız `data-vg01`:</span><span class="sxs-lookup"><span data-stu-id="5092f-135">In this example we are calling hello volume group `data-vg01`:</span></span>

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. <span data-ttu-id="5092f-136">Merhaba mantıksal birim oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5092f-136">Create hello logical volume(s).</span></span> <span data-ttu-id="5092f-137">Merhaba biz aşağıdaki komutunu adlı tek bir mantıksal birim oluşturacak `data-lv01` toospan hello birimin tamamını grup, bu da uygun toocreate olduğunu unutmayın hello birim grubunda birden çok mantıksal birim.</span><span class="sxs-lookup"><span data-stu-id="5092f-137">hello command below we will create a single logical volume called `data-lv01` toospan hello entire volume group, but note that it is also feasible toocreate multiple logical volumes in hello volume group.</span></span>

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. <span data-ttu-id="5092f-138">Format hello mantıksal birim</span><span class="sxs-lookup"><span data-stu-id="5092f-138">Format hello logical volume</span></span>

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > <span data-ttu-id="5092f-139">SLES11 kullanımıyla `-t ext3` ext4 yerine.</span><span class="sxs-lookup"><span data-stu-id="5092f-139">With SLES11 use `-t ext3` instead of ext4.</span></span> <span data-ttu-id="5092f-140">SLES11 yalnızca salt okunur erişim tooext4 bağlanan dosya sistemlerinin destekler.</span><span class="sxs-lookup"><span data-stu-id="5092f-140">SLES11 only supports read-only access tooext4 filesystems.</span></span>

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="5092f-141">Merhaba yeni dosya sistemi çok/etc/fstab Ekle</span><span class="sxs-lookup"><span data-stu-id="5092f-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5092f-142">Yanlış hello düzenleme `/etc/fstab` dosya önyüklenemez bir sisteme neden.</span><span class="sxs-lookup"><span data-stu-id="5092f-142">Improperly editing hello `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="5092f-143">Emin değilseniz, bu dosyayı tooproperly düzenleme nasıl hakkında bilgi için lütfen toohello dağıtım'ın belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="5092f-143">If unsure, please refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="5092f-144">Ayrıca hello yedeğini önerilen `/etc/fstab` dosyasını düzenlemeden önce oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5092f-144">It is also recommended that a backup of hello `/etc/fstab` file is created before editing.</span></span>

1. <span data-ttu-id="5092f-145">Örneğin, yeni bir dosya sistemi için istenen hello bağlama noktası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="5092f-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash  
    sudo mkdir /data
    ```

2. <span data-ttu-id="5092f-146">Merhaba mantıksal birim yolunu bulun</span><span class="sxs-lookup"><span data-stu-id="5092f-146">Locate hello logical volume path</span></span>

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. <span data-ttu-id="5092f-147">Açık `/etc/fstab` bir metin düzenleyicisinde ve örneğin hello yeni dosya sistemi için bir giriş ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5092f-147">Open `/etc/fstab` in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    <span data-ttu-id="5092f-148">Ardından, Kaydet ve Kapat `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="5092f-148">Then, save and close `/etc/fstab`.</span></span>

4. <span data-ttu-id="5092f-149">Bu hello test `/etc/fstab` giriştir doğru:</span><span class="sxs-lookup"><span data-stu-id="5092f-149">Test that hello `/etc/fstab` entry is correct:</span></span>

    ```bash    
    sudo mount -a
    ```

    <span data-ttu-id="5092f-150">Bu komutu bir hata iletisi sonuçlanırsa hello hello sözdiziminde danışın `/etc/fstab` dosya.</span><span class="sxs-lookup"><span data-stu-id="5092f-150">If this command results in an error message please check hello syntax in hello `/etc/fstab` file.</span></span>
   
    <span data-ttu-id="5092f-151">Merhaba sonraki çalıştırma `mount` komutu tooensure hello dosya sistemi takılı:</span><span class="sxs-lookup"><span data-stu-id="5092f-151">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="5092f-152">(İsteğe bağlı) Hatasız önyükleme parametrelerinde`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="5092f-152">(Optional) Failsafe boot parameters in `/etc/fstab`</span></span>
   
    <span data-ttu-id="5092f-153">Çoğu dağıtımda ya da hello dahil `nobootwait` veya `nofail` bağlama toohello eklenebilir parametreleri `/etc/fstab` dosya.</span><span class="sxs-lookup"><span data-stu-id="5092f-153">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello `/etc/fstab` file.</span></span> <span data-ttu-id="5092f-154">Bu parametreleri oluşturulamıyor tooproperly bağlama hello RAID dosya sistemi olsa bile hello Linux sistem toocontinue tooboot izin ve hataları için belirli dosya sistemi bağlarken izin verin.</span><span class="sxs-lookup"><span data-stu-id="5092f-154">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="5092f-155">Bu parametreler hakkında daha fazla bilgi için lütfen tooyour dağıtım'ın belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="5092f-155">Please refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="5092f-156">Örnek (Ubuntu):</span><span class="sxs-lookup"><span data-stu-id="5092f-156">Example (Ubuntu):</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a><span data-ttu-id="5092f-157">KIRPMA/UNMAP desteği</span><span class="sxs-lookup"><span data-stu-id="5092f-157">TRIM/UNMAP support</span></span>
<span data-ttu-id="5092f-158">Bazı Linux tekrar KIRPMA/UNMAP işlemleri toodiscard destek hello diskte kullanılmayan engeller.</span><span class="sxs-lookup"><span data-stu-id="5092f-158">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="5092f-159">Bu işlemler sayfaları silinmiş Azure artık geçerli değil ve iptal edilecek standart depolama tooinform öncelikle faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="5092f-159">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="5092f-160">Büyük dosyaları oluşturmak ve bunları silerseniz sayfaları atılıyor maliyet kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5092f-160">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="5092f-161">Tooenable KIRPMA desteği, Linux VM'NİZDE iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="5092f-161">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="5092f-162">Her zamanki gibi dağıtımınız için önerilen yaklaşımı hello bakın:</span><span class="sxs-lookup"><span data-stu-id="5092f-162">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="5092f-163">Kullanım hello `discard` bağlama seçeneği `/etc/fstab`, örneğin:</span><span class="sxs-lookup"><span data-stu-id="5092f-163">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="5092f-164">Bazı durumlarda hello içinde `discard` seçeneği performans etkileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="5092f-164">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="5092f-165">Alternatif olarak, hello çalıştırabilirsiniz `fstrim` komutunu el ile Merhaba komut satırından veya tooyour crontab toorun düzenli olarak ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5092f-165">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="5092f-166">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="5092f-166">**Ubuntu**</span></span>

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    <span data-ttu-id="5092f-167">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="5092f-167">**RHEL/CentOS**</span></span>

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
