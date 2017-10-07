---
title: aaaOptimize MySQL performans Linux'ta | Microsoft Docs
description: "Bilgi nasıl toooptimize MySQL çalıştıran bir Azure Linux çalıştıran sanal makine üzerinde (VM)."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a><span data-ttu-id="0cf3b-103">Azure Linux VM'ler MySQL performansı en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="0cf3b-103">Optimize MySQL Performance on Azure Linux VMs</span></span>
<span data-ttu-id="0cf3b-104">Hem sanal donanım seçimi ve yazılım yapılandırmasını Azure üzerinde MySQL performansı etkileyen pek çok etken vardır.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-104">There are many factors that affect MySQL performance on Azure, both in virtual hardware selection and software configuration.</span></span> <span data-ttu-id="0cf3b-105">Bu makalede, depolama, sistem ve veritabanı yapılandırmalarını en iyi duruma getirme performans odaklanır.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-105">This article focuses on optimizing performance through storage, system, and database configurations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0cf3b-106">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager](../../../resource-manager-deployment-model.md) ve klasik.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="0cf3b-107">Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="0cf3b-108">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="0cf3b-109">Linux VM iyileştirmeler hello Resource Manager modeli hakkında daha fazla bilgi için bkz: [Linux VM'NİZDE Azure ile ilgili en iyi duruma getirme](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0cf3b-109">For information about Linux VM optimizations with hello Resource Manager model, see [Optimize your Linux VM on Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="utilize-raid-on-an-azure-virtual-machine"></a><span data-ttu-id="0cf3b-110">Bir Azure sanal makinesi üzerinde RAID kullanma</span><span class="sxs-lookup"><span data-stu-id="0cf3b-110">Utilize RAID on an Azure virtual machine</span></span>
<span data-ttu-id="0cf3b-111">Depolama bulut ortamlarında veritabanı performansını etkiler hello anahtar faktördür.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-111">Storage is hello key factor that affects database performance in cloud environments.</span></span> <span data-ttu-id="0cf3b-112">Karşılaştırılan tooa tek disk RAID eşzamanlılık üzerinden daha hızlı erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-112">Compared tooa single disk, RAID can provide faster access via concurrency.</span></span> <span data-ttu-id="0cf3b-113">Daha fazla bilgi için bkz: [standart RAID düzeyleri](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span><span class="sxs-lookup"><span data-stu-id="0cf3b-113">For more information, see [Standard RAID levels](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span></span>   

<span data-ttu-id="0cf3b-114">Disk g/ç işleme ve g/ç yanıt süresi Azure RAID artırılabilir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-114">Disk I/O throughput and I/O response time in Azure can be improved through RAID.</span></span> <span data-ttu-id="0cf3b-115">Bizim Laboratuvar testleri disk g/ç işleme iki katına ve RAID disklerini hello sayısı iki katına olduğunda (iki toofour, dört tooeight, vb.) g/ç yanıt süresi yarı oranında ortalama azaltılabilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-115">Our lab tests show that disk I/O throughput can be doubled and I/O response time can be reduced by half on average when hello number of RAID disks is doubled (from two toofour, four tooeight, etc.).</span></span> <span data-ttu-id="0cf3b-116">Bkz: [ek A](#AppendixA) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-116">See [Appendix A](#AppendixA) for details.</span></span>  

<span data-ttu-id="0cf3b-117">Ayrıca hello RAID düzeyi artırdığınızda toodisk g/ç, MySQL performansı artırır.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-117">In addition toodisk I/O, MySQL performance improves when you increase hello RAID level.</span></span>  <span data-ttu-id="0cf3b-118">Bkz: [ek B](#AppendixB) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-118">See [Appendix B](#AppendixB) for details.</span></span>  

<span data-ttu-id="0cf3b-119">Ayrıca tooconsider hello öbek boyutu isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-119">You might also want tooconsider hello chunk size.</span></span> <span data-ttu-id="0cf3b-120">Daha büyük bir öbek boyutu varsa, genel olarak, ek yükü, özellikle büyük yazmalar için daha düşük sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-120">In general, when you have a larger chunk size, you get lower overhead, especially for large writes.</span></span> <span data-ttu-id="0cf3b-121">Ancak, Hello öbek boyutu çok büyük olduğunda RAID yararlanarak engeller ek yükü ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-121">However, when hello chunk size is too large, it might add additional overhead that prevents you from taking advantage of RAID.</span></span> <span data-ttu-id="0cf3b-122">Merhaba geçerli varsayılan boyutu toobe en genel üretim ortamları için en iyi kanıtlanmış 512 KB ' tır.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-122">hello current default size is 512 KB, which is proven toobe optimal for most general production environments.</span></span> <span data-ttu-id="0cf3b-123">Bkz: [ek C](#AppendixC) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-123">See [Appendix C](#AppendixC) for details.</span></span>   

<span data-ttu-id="0cf3b-124">Başka bir sanal makine türleri için ekleyebilirsiniz kaç disklerde sınırları vardır.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-124">There are limits on how many disks you can add for different virtual machine types.</span></span> <span data-ttu-id="0cf3b-125">Bu sınırlar içinde ayrıntılı [Azure için sanal makine ve bulut hizmeti boyutları](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="0cf3b-125">These limits are detailed in [Virtual machine and cloud service sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="0cf3b-126">Daha az disklerle RAID yukarı tooset seçebilmenize rağmen dört ekli veri diskleri toofollow hello RAID örneği bu makalede, gerekir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-126">You will need four attached data disks toofollow hello RAID example in this article, although you can choose tooset up RAID with fewer disks.</span></span>  

<span data-ttu-id="0cf3b-127">Bu makalede, Linux sanal makine oluşturmuş ve MYSQL yüklenmiş ve yapılandırılmış varsayar.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-127">This article assumes you have already created a Linux virtual machine and have MYSQL installed and configured.</span></span> <span data-ttu-id="0cf3b-128">Kullanmaya başlama hakkında daha fazla bilgi için bkz. nasıl tooinstall Azure üzerinde MySQL.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-128">For more information on getting started, see How tooinstall MySQL on Azure.</span></span>  

### <a name="set-up-raid-on-azure"></a><span data-ttu-id="0cf3b-129">Azure üzerinde RAID ayarlama</span><span class="sxs-lookup"><span data-stu-id="0cf3b-129">Set up RAID on Azure</span></span>
<span data-ttu-id="0cf3b-130">Merhaba aşağıdaki adımlar nasıl toocreate RAID Azure'da hello Azure portal kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-130">hello following steps show how toocreate RAID on Azure by using hello Azure portal.</span></span> <span data-ttu-id="0cf3b-131">Windows PowerShell komut dosyalarını kullanarak RAID de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-131">You can also set up RAID by using Windows PowerShell scripts.</span></span>
<span data-ttu-id="0cf3b-132">Bu örnekte, şu dört disklerle RAID 0 yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-132">In this example, we will configure RAID 0 with four disks.</span></span>  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a><span data-ttu-id="0cf3b-133">Bir veri diski tooyour sanal makine Ekle</span><span class="sxs-lookup"><span data-stu-id="0cf3b-133">Add a data disk tooyour virtual machine</span></span>
<span data-ttu-id="0cf3b-134">Hello Azure portal, toohello panonuzu ve hello sanal makine toowhich tooadd bir veri diski istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-134">In hello Azure portal, go toohello dashboard and select hello virtual machine toowhich you want tooadd a data disk.</span></span> <span data-ttu-id="0cf3b-135">Bu örnekte, mysqlnode1 hello sanal makinedir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-135">In this example, hello virtual machine is mysqlnode1.</span></span>  

<!--![Virtual machines][1]-->

<span data-ttu-id="0cf3b-136">Tıklatın **diskleri** ve ardından **Attach yeni**.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-136">Click **Disks** and then click **Attach New**.</span></span>

![Sanal makineler disk ekleme](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

<span data-ttu-id="0cf3b-138">Yeni bir 500 GB disk oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-138">Create a new 500 GB disk.</span></span> <span data-ttu-id="0cf3b-139">Olduğundan emin olun **konak önbelleği tercihi** çok ayarlanır**hiçbiri**.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-139">Make sure that **Host Cache Preference** is set too**None**.</span></span>  <span data-ttu-id="0cf3b-140">İşiniz bittiğinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-140">When you're finished, click **OK**.</span></span>

![Boş diski kullanıma açın](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


<span data-ttu-id="0cf3b-142">Bu bir boş disk, sanal makineye ekler.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-142">This adds one empty disk into your virtual machine.</span></span> <span data-ttu-id="0cf3b-143">Böylece dört veri diskleri için RAID sahip bu üç kez tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-143">Repeat this step three more times so that you have four data disks for RAID.</span></span>  

<span data-ttu-id="0cf3b-144">Eklenen hello görebilirsiniz hello çekirdek ileti günlüğüne bakarak hello sanal makinede sürücüler.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-144">You can see hello added drives in hello virtual machine by looking at hello kernel message log.</span></span> <span data-ttu-id="0cf3b-145">Örneğin, toosee bu Ubuntu, komutu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-145">For example, toosee this on Ubuntu, use hello following command:</span></span>  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a><span data-ttu-id="0cf3b-146">RAID ile Merhaba ek disk oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-146">Create RAID with hello additional disks</span></span>
<span data-ttu-id="0cf3b-147">Merhaba aşağıdaki adımları nasıl çok açıklamak[yazılım RAID Linux üzerinde yapılandırma](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0cf3b-147">hello following steps describe how too[configure software RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="0cf3b-148">Merhaba XFS dosya sistemi kullanıyorsanız, RAID oluşturduktan sonra aşağıdaki adımları hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-148">If you are using hello XFS file system, execute hello following steps after you have created RAID.</span></span>
>
>

<span data-ttu-id="0cf3b-149">komutu aşağıdaki Debian, Ubuntu ya da Linux Naneli kullanım hello üzerinde tooinstall XFS:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-149">tooinstall XFS on Debian, Ubuntu, or Linux Mint, use hello following command:</span></span>  

    apt-get -y install xfsprogs  

<span data-ttu-id="0cf3b-150">komutu aşağıdaki Fedora, CentOS veya RHEL, kullanım hello üzerinde tooinstall XFS:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-150">tooinstall XFS on Fedora, CentOS, or RHEL, use hello following command:</span></span>  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a><span data-ttu-id="0cf3b-151">Yeni bir depolama yol ayarla</span><span class="sxs-lookup"><span data-stu-id="0cf3b-151">Set up a new storage path</span></span>
<span data-ttu-id="0cf3b-152">Yeni bir depolama yol komutu tooset aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-152">Use hello following command tooset up a new storage path:</span></span>  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a><span data-ttu-id="0cf3b-153">Merhaba özgün veri toohello yeni depolama birimi yolu kopyalayın</span><span class="sxs-lookup"><span data-stu-id="0cf3b-153">Copy hello original data toohello new storage path</span></span>
<span data-ttu-id="0cf3b-154">Komut toocopy veri toohello yeni depolama birimi yolu izleyerek hello kullan:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-154">Use hello following command toocopy data toohello new storage path:</span></span>  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a><span data-ttu-id="0cf3b-155">MySQL erişebilmesi için (okuma ve yazma) değiştirme izinleri hello veri diski</span><span class="sxs-lookup"><span data-stu-id="0cf3b-155">Modify permissions so MySQL can access (read and write) hello data disk</span></span>
<span data-ttu-id="0cf3b-156">Aşağıdaki komut toomodify izinleri hello kullan:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-156">Use hello following command toomodify permissions:</span></span>  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a><span data-ttu-id="0cf3b-157">Merhaba disk g/ç algoritması zamanlama ayarlama</span><span class="sxs-lookup"><span data-stu-id="0cf3b-157">Adjust hello disk I/O scheduling algorithm</span></span>
<span data-ttu-id="0cf3b-158">Linux algoritmaları zamanlama g/ç dört tür uygular:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-158">Linux implements four types of I/O scheduling algorithms:</span></span>  

* <span data-ttu-id="0cf3b-159">SEKMEYİ algoritması (No işlem)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-159">NOOP algorithm (No Operation)</span></span>
* <span data-ttu-id="0cf3b-160">Son tarih algoritması (son)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-160">Deadline algorithm (Deadline)</span></span>
* <span data-ttu-id="0cf3b-161">Tamamen Orta Sıralama algoritması (CFQ)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-161">Completely fair queuing algorithm (CFQ)</span></span>
* <span data-ttu-id="0cf3b-162">Bütçe dönem algoritması (Anticipatory)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-162">Budget period algorithm (Anticipatory)</span></span>  

<span data-ttu-id="0cf3b-163">Farklı senaryolar toooptimize performans altında farklı g/ç zamanlayıcılar seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-163">You can select different I/O schedulers under different scenarios toooptimize performance.</span></span> <span data-ttu-id="0cf3b-164">Tamamen rastgele erişim ortamında değil hello CFQ ve performans için son tarih algoritmaları arasında önemli bir fark yoktur.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-164">In a completely random access environment, there is not a significant difference between hello CFQ and Deadline algorithms for performance.</span></span> <span data-ttu-id="0cf3b-165">Merhaba MySQL veritabanı ortamı tooDeadline kararlılık için ayarlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-165">We recommend that you set hello MySQL database environment tooDeadline for stability.</span></span> <span data-ttu-id="0cf3b-166">Çok sayıda sıralı g/ç ise CFQ disk g/ç performansını düşürebilir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-166">If there is a lot of sequential I/O, CFQ might reduce disk I/O performance.</span></span>   

<span data-ttu-id="0cf3b-167">SSD ve diğer donanım için SEKMEYİ veya son hello varsayılan Zamanlayıcı daha iyi performans elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-167">For SSD and other equipment, NOOP or Deadline can achieve better performance than hello default scheduler.</span></span>   

<span data-ttu-id="0cf3b-168">Önceki toohello çekirdek 2.5, hello varsayılan g/ç algoritması zamanlama son ' dir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-168">Prior toohello kernel 2.5, hello default I/O scheduling algorithm is Deadline.</span></span> <span data-ttu-id="0cf3b-169">Merhaba çekirdek 2.6.18 ile başlayarak, CFQ hello varsayılan g/ç zamanlama algoritma hale geldi.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-169">Starting with hello kernel 2.6.18, CFQ became hello default I/O scheduling algorithm.</span></span>  <span data-ttu-id="0cf3b-170">Bu ayarı çekirdek önyükleme zaman belirtin veya hello sistem çalışırken dinamik olarak bu ayarı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-170">You can specify this setting at kernel boot time or dynamically modify this setting when hello system is running.</span></span>  

<span data-ttu-id="0cf3b-171">Aşağıdaki örneğine hello nasıl toocheck ve kümesi varsayılan Zamanlayıcı toohello SEKMEYİ algoritma hello Debian dağıtım ailesindeki hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-171">hello following example demonstrates how toocheck and set hello default scheduler toohello NOOP algorithm in hello Debian distribution family.</span></span>  

### <a name="view-hello-current-io-scheduler"></a><span data-ttu-id="0cf3b-172">Görünüm hello geçerli g/ç Zamanlayıcı</span><span class="sxs-lookup"><span data-stu-id="0cf3b-172">View hello current I/O scheduler</span></span>
<span data-ttu-id="0cf3b-173">tooview hello Zamanlayıcı hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-173">tooview hello scheduler run hello following command:</span></span>  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

<span data-ttu-id="0cf3b-174">Merhaba geçerli Zamanlayıcı gösterir çıktı aşağıdaki görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-174">You will see following output, which indicates hello current scheduler:</span></span>  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a><span data-ttu-id="0cf3b-175">Merhaba g/ç zamanlama algoritmasının Hello geçerli aygıtı (/ dev/sda) değiştirme</span><span class="sxs-lookup"><span data-stu-id="0cf3b-175">Change hello current device (/dev/sda) of hello I/O scheduling algorithm</span></span>
<span data-ttu-id="0cf3b-176">Aşağıdaki komutları toochange hello geçerli cihaz hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-176">Run hello following commands toochange hello current device:</span></span>  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> <span data-ttu-id="0cf3b-177">Bu/dev/sda için tek başına ayarı kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-177">Setting this for /dev/sda alone is not useful.</span></span> <span data-ttu-id="0cf3b-178">Merhaba veritabanının bulunduğu tüm veri disklerde ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-178">It must be set on all data disks where hello database resides.</span></span>  
>
>

<span data-ttu-id="0cf3b-179">Çıktı aşağıdaki, grub.cfg başarıyla yeniden oluşturuldu ve bu hello varsayılan Zamanlayıcı güncelleştirilmiş tooNOOP bırakıldı gösteren hello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-179">You should see hello following output, indicating that grub.cfg has been rebuilt successfully and that hello default scheduler has been updated tooNOOP:</span></span>  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

<span data-ttu-id="0cf3b-180">Hello Red Hat dağıtım ailesi için aşağıdaki komut yalnızca hello:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-180">For hello Red Hat distribution family, you need only hello following command:</span></span>

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a><span data-ttu-id="0cf3b-181">Sistem dosyası işlemleri ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0cf3b-181">Configure system file operations settings</span></span>
<span data-ttu-id="0cf3b-182">Bir en iyi uygulamadır toodisable hello *atime* hello dosya sistemi günlük kaydı özelliği.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-182">One best practice is toodisable hello *atime* logging feature on hello file system.</span></span> <span data-ttu-id="0cf3b-183">Atime hello son dosya erişim zamanı ' dir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-183">Atime is hello last file access time.</span></span> <span data-ttu-id="0cf3b-184">Bir dosya erişildiğinde hello dosya sistemi kayıtları zaman damgası hello günlüğünde hello.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-184">Whenever a file is accessed, hello file system records hello timestamp in hello log.</span></span> <span data-ttu-id="0cf3b-185">Ancak, bu bilgileri nadiren kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-185">However, this information is rarely used.</span></span> <span data-ttu-id="0cf3b-186">Hangi genel disk erişim süresini azaltır, onu gereksiniminiz yoksa devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-186">You can disable it if you don't need it, which will reduce overall disk access time.</span></span>  

<span data-ttu-id="0cf3b-187">toodisable atime günlüğü, toomodify hello dosya sistemi yapılandırma dosyası /etc/ fstab ve gerekir hello eklemek **noatime** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-187">toodisable atime logging, you need toomodify hello file system configuration file /etc/ fstab and add hello **noatime** option.</span></span>  

<span data-ttu-id="0cf3b-188">Örneğin, aşağıdaki örnek hello gösterildiği gibi hello noatime ekleyerek, hello VIM /etc/fstab dosyasını düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-188">For example, edit hello vim /etc/fstab file, adding hello noatime as shown in hello following sample:</span></span>  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

<span data-ttu-id="0cf3b-189">Ardından, hello dosya sistemi ile komutu aşağıdaki hello yeniden bağlayın:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-189">Then, remount hello file system with hello following command:</span></span>  

    mount -o remount /RAID0

<span data-ttu-id="0cf3b-190">Test hello sonuç değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-190">Test hello modified result.</span></span> <span data-ttu-id="0cf3b-191">Merhaba test dosyasını değiştirdiğinizde, hello erişim zamanı güncelleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-191">When you modify hello test file, hello access time is not updated.</span></span> <span data-ttu-id="0cf3b-192">Aşağıdaki örneklerde gösterildiği hangi hello kodu önce ve sonra değişiklik benzer hello.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-192">hello following examples show what hello code looks like before and after modification.</span></span>

<span data-ttu-id="0cf3b-193">Önce:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-193">Before:</span></span>        

![Erişim değişiklikten önce kod][5]

<span data-ttu-id="0cf3b-195">Sonra:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-195">After:</span></span>

![Erişimi değiştirme sonrasında kod][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a><span data-ttu-id="0cf3b-197">Hello en yüksek eşzamanlılık için sistem işleyicilerin sayısını artırın</span><span class="sxs-lookup"><span data-stu-id="0cf3b-197">Increase hello maximum number of system handles for high concurrency</span></span>
<span data-ttu-id="0cf3b-198">MySQL yüksek eşzamanlılık veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-198">MySQL is a high concurrency database.</span></span> <span data-ttu-id="0cf3b-199">Merhaba varsayılan eşzamanlı tanıtıcıları 1024 Linux için her zaman yeterli olmayan sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-199">hello default number of concurrent handles is 1024 for Linux, which is not always sufficient.</span></span> <span data-ttu-id="0cf3b-200">Adımları tooincrease hello en fazla eş zamanlı tanıtıcıları hello sistem toosupport yüksek eşzamanlılığı MySQL, aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-200">Use hello following steps tooincrease hello maximum concurrent handles of hello system toosupport high concurrency of MySQL.</span></span>

### <a name="modify-hello-limitsconf-file"></a><span data-ttu-id="0cf3b-201">Merhaba limits.conf dosyasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="0cf3b-201">Modify hello limits.conf file</span></span>
<span data-ttu-id="0cf3b-202">tooincrease hello en fazla eş zamanlı tanıtıcıları izin, dört satırlardan hello /etc/security/limits.conf dosyasında hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-202">tooincrease hello maximum allowed concurrent handles, add hello following four lines in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="0cf3b-203">65536 hello sistemin destekleyebileceği en fazla hello olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-203">Note that 65536 is hello maximum number that hello system can support.</span></span>   

    * <span data-ttu-id="0cf3b-204">yazılım nofile 65536</span><span class="sxs-lookup"><span data-stu-id="0cf3b-204">soft nofile 65536</span></span>
    * <span data-ttu-id="0cf3b-205">Sabit nofile 65536</span><span class="sxs-lookup"><span data-stu-id="0cf3b-205">hard nofile 65536</span></span>
    * <span data-ttu-id="0cf3b-206">yazılım nproc 65536</span><span class="sxs-lookup"><span data-stu-id="0cf3b-206">soft nproc 65536</span></span>
    * <span data-ttu-id="0cf3b-207">Sabit nproc 65536</span><span class="sxs-lookup"><span data-stu-id="0cf3b-207">hard nproc 65536</span></span>

### <a name="update-hello-system-for-hello-new-limits"></a><span data-ttu-id="0cf3b-208">Merhaba sistemi hello yeni sınırları için güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="0cf3b-208">Update hello system for hello new limits</span></span>
<span data-ttu-id="0cf3b-209">tooupdate hello sistemi, hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-209">tooupdate hello system, run hello following commands:</span></span>  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a><span data-ttu-id="0cf3b-210">Önyükleme sırasında Hello sınırları güncelleştirildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="0cf3b-210">Ensure that hello limits are updated at boot time</span></span>
<span data-ttu-id="0cf3b-211">Merhaba, önyükleme sırasında etkili şekilde hello /etc/rc.local dosyasındaki başlatma komutları aşağıdaki yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-211">Put hello following startup commands in hello /etc/rc.local file so it will take effect at boot time.</span></span>  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a><span data-ttu-id="0cf3b-212">MySQL veritabanı en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="0cf3b-212">MySQL database optimization</span></span>
<span data-ttu-id="0cf3b-213">Azure üzerinde MySQL tooconfigure, kullanabileceğiniz hello aynı performans ayarlama stratejisi bir şirket içi makinede kullanın.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-213">tooconfigure MySQL on Azure, you can use hello same performance-tuning strategy you use on an on-premises machine.</span></span>  

<span data-ttu-id="0cf3b-214">Merhaba ana g/ç iyileştirme kurallar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-214">hello main I/O optimization rules are:</span></span>   

* <span data-ttu-id="0cf3b-215">Merhaba önbellek boyutunu artırın.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-215">Increase hello cache size.</span></span>
* <span data-ttu-id="0cf3b-216">G/ç yanıt süresini azaltın.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-216">Reduce I/O response time.</span></span>  

<span data-ttu-id="0cf3b-217">toooptimize MySQL sunucu ayarları, hem sunucu hem de istemci bilgisayarlar hello varsayılan yapılandırma dosyası hello my.cnf dosyasını güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-217">toooptimize MySQL server settings, you can update hello my.cnf file, which is hello default configuration file for both server and client computers.</span></span>  

<span data-ttu-id="0cf3b-218">Merhaba aşağıdaki yapılandırma öğelerini hello MySQL performansı etkileyen ana faktörler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-218">hello following configuration items are hello main factors that affect MySQL performance:</span></span>  

* <span data-ttu-id="0cf3b-219">**innodb_buffer_pool_size**: hello arabellek havuzu arabelleğe alınan verileri ve hello dizini içerir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-219">**innodb_buffer_pool_size**: hello buffer pool contains buffered data and hello index.</span></span> <span data-ttu-id="0cf3b-220">Bu, genellikle fiziksel bellek yüzdesi too70 ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-220">This is usually set too70 percent of physical memory.</span></span>
* <span data-ttu-id="0cf3b-221">**innodb_log_file_size**: hello Yinele günlük boyutu budur.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-221">**innodb_log_file_size**: This is hello redo log size.</span></span> <span data-ttu-id="0cf3b-222">Yazma işlemleri hızlı, güvenilir ve kurtarılabilir kilitlenme sonrasında Yinele günlükleri tooensure kullanın.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-222">You use redo logs tooensure that write operations are fast, reliable, and recoverable after a crash.</span></span> <span data-ttu-id="0cf3b-223">Bu yazma işlemleri günlüğe kaydetme için yeterince alan verecektir too512 MB ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-223">This is set too512 MB, which will give you plenty of space for logging write operations.</span></span>
* <span data-ttu-id="0cf3b-224">**max_connections**: bazen uygulamaları bağlantıları düzgün kapatmayın.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-224">**max_connections**: Sometimes applications do not close connections properly.</span></span> <span data-ttu-id="0cf3b-225">Daha büyük bir değer hello sunucu bağlantıları toorecycle idled daha fazla zaman verir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-225">A larger value will give hello server more time toorecycle idled connections.</span></span> <span data-ttu-id="0cf3b-226">Merhaba en fazla bağlantı sayısı, 10.000 olmakla birlikte hello en fazla 5000 önerilir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-226">hello maximum number of connections is 10,000, but hello recommended maximum is 5,000.</span></span>
* <span data-ttu-id="0cf3b-227">**Innodb_file_per_table**: Bu ayar etkinleştirir ya da ayrı dosyalar InnoDB toostore tablolarda hello özelliğini devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-227">**Innodb_file_per_table**: This setting enables or disables hello ability of InnoDB toostore tables in separate files.</span></span> <span data-ttu-id="0cf3b-228">Birçok gelişmiş yönetim işlemleri verimli bir şekilde uygulanabilir hello seçeneği tooensure üzerinde etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-228">Turn on hello option tooensure that several advanced administration operations can be applied efficiently.</span></span> <span data-ttu-id="0cf3b-229">Bir performans açısından bakıldığında, bu hello tablo alanı aktarım hızı ve hello debris yönetim performansı en iyi duruma getirme.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-229">From a performance point of view, it can speed up hello table space transmission and optimize hello debris management performance.</span></span> <span data-ttu-id="0cf3b-230">Merhaba bu seçenek ayarı ON önerilir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-230">hello recommended setting for this option is ON.</span></span></br></br>
<span data-ttu-id="0cf3b-231">MySQL 5.6 hello varsayılan ayarı ON, olduğundan hiçbir eyleme gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-231">From MySQL 5.6, hello default setting is ON, so no action is required.</span></span> <span data-ttu-id="0cf3b-232">Önceki sürümler için OFF hello varsayılan ayardır.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-232">For earlier versions, hello default setting is OFF.</span></span> <span data-ttu-id="0cf3b-233">veriler yüklenmeden önce yalnızca yeni oluşturulan tabloları etkilendiği hello ayarı değiştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-233">hello setting should be changed before data is loaded, because only newly created tables are affected.</span></span>
* <span data-ttu-id="0cf3b-234">**innodb_flush_log_at_trx_commit**: hello varsayılan değer 1'dir, ile Merhaba too0 kapsamını Ayarla ~ 2.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-234">**innodb_flush_log_at_trx_commit**: hello default value is 1, with hello scope set too0~2.</span></span> <span data-ttu-id="0cf3b-235">tek başına MySQL veritabanı için en uygun seçeneği hello Hello varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-235">hello default value is hello most suitable option for standalone MySQL DB.</span></span> <span data-ttu-id="0cf3b-236">Merhaba ayar 2 etkinleştirir, çoğu veri bütünlüğü hello ve MySQL kümesi yöneticisinde için uygundur.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-236">hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL Cluster.</span></span> <span data-ttu-id="0cf3b-237">Merhaba ayarı 0 (daha iyi performans ile bazı durumlarda) güvenilirlik etkileyebilir ve MySQL kümedeki ikincil için uygun veri kaybı sağlar.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-237">hello setting of 0 allows data loss, which can affect reliability (in some cases with better performance), and is suitable for Slave in MySQL Cluster.</span></span>
* <span data-ttu-id="0cf3b-238">**Innodb_log_buffer_size**: hello günlük arabellek tooflush hello günlük toodisk hello işlemleri tamamlama önce gerek kalmadan işlemleri toorun sağlar.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-238">**Innodb_log_buffer_size**: hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit.</span></span> <span data-ttu-id="0cf3b-239">Ancak, ikili büyük nesne veya metin alanını ise hello önbellek hızla dolacaktır ve sık disk g/ç tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-239">However, if there is large binary object or text field, hello cache will be consumed quickly and frequent disk I/O will be triggered.</span></span> <span data-ttu-id="0cf3b-240">Innodb_log_waits durumu değişken değilse daha iyi hello arabellek boyutunu artırın olan 0.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-240">It is better increase hello buffer size if Innodb_log_waits state variable is not 0.</span></span>
* <span data-ttu-id="0cf3b-241">**query_cache_size**: hello en iyi seçenektir toodisable hello outset ondan.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-241">**query_cache_size**: hello best option is toodisable it from hello outset.</span></span> <span data-ttu-id="0cf3b-242">(MySQL 5.6 de hello varsayılan ayar budur) query_cache_size too0 ayarlayabilir ve diğer yöntemleri toospeed sorguları yukarı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-242">Set query_cache_size too0 (this is hello default setting in MySQL 5.6) and use other methods toospeed up queries.</span></span>  

<span data-ttu-id="0cf3b-243">Bkz: [ek D](#AppendixD) önce ve sonra hello iyileştirme performans karşılaştırması.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-243">See [Appendix D](#AppendixD) for a comparison of performance before and after hello optimization.</span></span>

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a><span data-ttu-id="0cf3b-244">Merhaba MySQL yavaş sorgu günlüğü hello performans düşüklüğü çözümlemek için Aç</span><span class="sxs-lookup"><span data-stu-id="0cf3b-244">Turn on hello MySQL slow query log for analyzing hello performance bottleneck</span></span>
<span data-ttu-id="0cf3b-245">Merhaba MySQL yavaş sorgu günlüğü hello yavaş sorgular için MySQL belirlemenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-245">hello MySQL slow query log can help you identify hello slow queries for MySQL.</span></span> <span data-ttu-id="0cf3b-246">Merhaba MySQL yavaş sorgu günlüğü etkinleştirdikten sonra MySQL araçları gibi kullanabilirsiniz **mysqldumpslow** tooidentify hello performans düşüklüğü.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-246">After enabling hello MySQL slow query log, you can use MySQL tools like **mysqldumpslow** tooidentify hello performance bottleneck.</span></span>  

<span data-ttu-id="0cf3b-247">Varsayılan olarak, bu etkin değil.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-247">By default, this is not enabled.</span></span> <span data-ttu-id="0cf3b-248">Merhaba yavaş sorgu oturum açma kapatma bazı CPU kaynaklarını tüketebilir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-248">Turning on hello slow query log might consume some CPU resources.</span></span> <span data-ttu-id="0cf3b-249">Bu geçici olarak performans sorunları gidermek için etkinleştirmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-249">We recommend that you enable this temporarily for troubleshooting performance bottlenecks.</span></span> <span data-ttu-id="0cf3b-250">tooturn hello yavaş sorgu oturum:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-250">tooturn on hello slow query log:</span></span>

1. <span data-ttu-id="0cf3b-251">Merhaba my.cnf dosyası aşağıdaki satırları toohello son hello ekleyerek değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0cf3b-251">Modify hello my.cnf file by adding hello following lines toohello end:</span></span>

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. <span data-ttu-id="0cf3b-252">Merhaba MySQL sunucusunu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-252">Restart hello MySQL server.</span></span>

        service  mysql  restart

3. <span data-ttu-id="0cf3b-253">Hello kullanarak Hello ayarı etkisi sürüyor olup olmadığını denetleyin **Göster** komutu.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-253">Check whether hello setting is taking effect by using hello **show** command.</span></span>

![Yavaş-query-log ON][7]   

![Yavaş-query-günlük sonuçları][8]

<span data-ttu-id="0cf3b-256">Bu örnekte, bu hello yavaş sorgu özelliği etkinleştirildi görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-256">In this example, you can see that hello slow query feature has been turned on.</span></span> <span data-ttu-id="0cf3b-257">Merhaba sonra kullanabileceğiniz **mysqldumpslow** dizinleri ekleme gibi performansı iyileştirmek ve aracı toodetermine performans sorunları.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-257">You can then use hello **mysqldumpslow** tool toodetermine performance bottlenecks and optimize performance, such as adding indexes.</span></span>

## <a name="appendices"></a><span data-ttu-id="0cf3b-258">Ekler</span><span class="sxs-lookup"><span data-stu-id="0cf3b-258">Appendices</span></span>
<span data-ttu-id="0cf3b-259">Merhaba, hedeflenen laboratuvar ortamında üretilen örnek performans test verileri verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-259">hello following are sample performance test data produced in a targeted lab environment.</span></span> <span data-ttu-id="0cf3b-260">Genel arka plan hello performans veri eğilimi üzerinde farklı performans yaklaşımlar ayarlama ile sağlarlar.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-260">They provide general background on hello performance data trend with different performance tuning approaches.</span></span> <span data-ttu-id="0cf3b-261">Merhaba sonuçları altında farklı ortamı veya ürün sürümleri değişebilir.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-261">hello results might vary under different environment or product versions.</span></span>

### <span data-ttu-id="0cf3b-262"><a name="AppendixA"></a>Ek A</span><span class="sxs-lookup"><span data-stu-id="0cf3b-262"><a name="AppendixA"></a>Appendix A</span></span>  
<span data-ttu-id="0cf3b-263">**Farklı RAID düzeyleri ile disk performansı (IOPS)**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-263">**Disk performance (IOPS) with different RAID levels**</span></span>

![IOPS diskle farklı RAID düzeyleri][9]

<span data-ttu-id="0cf3b-265">**Test komutları**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-265">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> <span data-ttu-id="0cf3b-266">Bu test Hello iş yükünü tooreach hello üst sınır RAID çalışırken 64 iş parçacığı kullanır.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-266">hello workload of this test uses 64 threads, trying tooreach hello upper limit of RAID.</span></span>
>
>

### <span data-ttu-id="0cf3b-267"><a name="AppendixB"></a>Ek B</span><span class="sxs-lookup"><span data-stu-id="0cf3b-267"><a name="AppendixB"></a>Appendix B</span></span>  
<span data-ttu-id="0cf3b-268">**Farklı RAID düzeyleri ile MySQL performans (performans) karşılaştırma** </span><span class="sxs-lookup"><span data-stu-id="0cf3b-268">**MySQL performance (throughput) comparison with different RAID levels** </span></span>  
<span data-ttu-id="0cf3b-269">(XFS dosya sistemi)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-269">(XFS file system)</span></span>

![Farklı RAID düzeyleri ile MySQL performans karşılaştırma][10]  
![Farklı RAID düzeyleri ile MySQL performans karşılaştırma][11]

<span data-ttu-id="0cf3b-272">**Test komutları**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-272">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

<span data-ttu-id="0cf3b-273">**Farklı RAID düzeyleri ile MySQL performans (OLTP) karşılaştırma**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-273">**MySQL performance (OLTP) comparison with different RAID levels**</span></span>  
<span data-ttu-id="0cf3b-274">![Farklı RAID düzeyleri ile MySQL performans (OLTP) karşılaştırma][12]</span><span class="sxs-lookup"><span data-stu-id="0cf3b-274">![MySQL performance (OLTP) comparison with different RAID levels][12]</span></span>

<span data-ttu-id="0cf3b-275">**Test komutları**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-275">**Test commands**</span></span>

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <span data-ttu-id="0cf3b-276"><a name="AppendixC"></a>Ek C</span><span class="sxs-lookup"><span data-stu-id="0cf3b-276"><a name="AppendixC"></a>Appendix C</span></span>   
<span data-ttu-id="0cf3b-277">**Farklı öbek boyutları için disk performans (IOPS) karşılaştırması**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-277">**Disk performance (IOPS) comparison for different chunk sizes**</span></span>  
<span data-ttu-id="0cf3b-278">(XFS dosya sistemi)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-278">(XFS file system)</span></span>

![][13]

<span data-ttu-id="0cf3b-279">**Test komutları**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-279">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

<span data-ttu-id="0cf3b-280">Bu test için kullanılan hello dosya boyutları 30 GB ve 1 GB, sırasıyla, RAID 0 (4 disk) ile XFS dosya sistemi.</span><span class="sxs-lookup"><span data-stu-id="0cf3b-280">hello file sizes used for this testing are 30 GB and 1 GB, respectively, with RAID 0 (4 disks) XFS file system.</span></span>

### <span data-ttu-id="0cf3b-281"><a name="AppendixD"></a>Ek D</span><span class="sxs-lookup"><span data-stu-id="0cf3b-281"><a name="AppendixD"></a>Appendix D</span></span>  
<span data-ttu-id="0cf3b-282">**MySQL performans (performans) karşılaştırma önce ve sonra en iyi duruma getirme**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-282">**MySQL performance (throughput) comparison before and after optimization**</span></span>  
<span data-ttu-id="0cf3b-283">(XFS dosya sistemi)</span><span class="sxs-lookup"><span data-stu-id="0cf3b-283">(XFS File System)</span></span>

![MySQL performans (performans) karşılaştırma önce ve sonra en iyi duruma getirme][14]

<span data-ttu-id="0cf3b-285">**Test komutları**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-285">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

<span data-ttu-id="0cf3b-286">**Varsayılan ve en iyi duruma getirme için Hello yapılandırma ayarı aşağıdaki gibidir:**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-286">**hello configuration setting for default and optimization is as follows:**</span></span>

| <span data-ttu-id="0cf3b-287">Parametreler</span><span class="sxs-lookup"><span data-stu-id="0cf3b-287">Parameters</span></span> | <span data-ttu-id="0cf3b-288">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="0cf3b-288">Default</span></span> | <span data-ttu-id="0cf3b-289">İyileştirme</span><span class="sxs-lookup"><span data-stu-id="0cf3b-289">Optimization</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0cf3b-290">**innodb_buffer_pool_size**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-290">**innodb_buffer_pool_size**</span></span> |<span data-ttu-id="0cf3b-291">None</span><span class="sxs-lookup"><span data-stu-id="0cf3b-291">None</span></span> |<span data-ttu-id="0cf3b-292">7 GB</span><span class="sxs-lookup"><span data-stu-id="0cf3b-292">7 GB</span></span> |
| <span data-ttu-id="0cf3b-293">**innodb_log_file_size**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-293">**innodb_log_file_size**</span></span> |<span data-ttu-id="0cf3b-294">5 MB</span><span class="sxs-lookup"><span data-stu-id="0cf3b-294">5 MB</span></span> |<span data-ttu-id="0cf3b-295">512 MB</span><span class="sxs-lookup"><span data-stu-id="0cf3b-295">512 MB</span></span> |
| <span data-ttu-id="0cf3b-296">**max_connections**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-296">**max_connections**</span></span> |<span data-ttu-id="0cf3b-297">100</span><span class="sxs-lookup"><span data-stu-id="0cf3b-297">100</span></span> |<span data-ttu-id="0cf3b-298">5000</span><span class="sxs-lookup"><span data-stu-id="0cf3b-298">5000</span></span> |
| <span data-ttu-id="0cf3b-299">**innodb_file_per_table**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-299">**innodb_file_per_table**</span></span> |<span data-ttu-id="0cf3b-300">0</span><span class="sxs-lookup"><span data-stu-id="0cf3b-300">0</span></span> |<span data-ttu-id="0cf3b-301">1</span><span class="sxs-lookup"><span data-stu-id="0cf3b-301">1</span></span> |
| <span data-ttu-id="0cf3b-302">**innodb_flush_log_at_trx_commit**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-302">**innodb_flush_log_at_trx_commit**</span></span> |<span data-ttu-id="0cf3b-303">1</span><span class="sxs-lookup"><span data-stu-id="0cf3b-303">1</span></span> |<span data-ttu-id="0cf3b-304">2</span><span class="sxs-lookup"><span data-stu-id="0cf3b-304">2</span></span> |
| <span data-ttu-id="0cf3b-305">**innodb_log_buffer_size**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-305">**innodb_log_buffer_size**</span></span> |<span data-ttu-id="0cf3b-306">8 MB</span><span class="sxs-lookup"><span data-stu-id="0cf3b-306">8 MB</span></span> |<span data-ttu-id="0cf3b-307">128 MB</span><span class="sxs-lookup"><span data-stu-id="0cf3b-307">128 MB</span></span> |
| <span data-ttu-id="0cf3b-308">**query_cache_size**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-308">**query_cache_size**</span></span> |<span data-ttu-id="0cf3b-309">16 MB</span><span class="sxs-lookup"><span data-stu-id="0cf3b-309">16 MB</span></span> |<span data-ttu-id="0cf3b-310">0</span><span class="sxs-lookup"><span data-stu-id="0cf3b-310">0</span></span> |

<span data-ttu-id="0cf3b-311">Daha ayrıntılı için [en iyi duruma getirme yapılandırma parametrelerini](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), toohello başvuran [MySQL resmi yönergeleri](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span><span class="sxs-lookup"><span data-stu-id="0cf3b-311">For more detailed [optimization configuration parameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), refer toohello [MySQL official instructions](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span></span>  

  <span data-ttu-id="0cf3b-312">**Test ortamı**</span><span class="sxs-lookup"><span data-stu-id="0cf3b-312">**Test environment**</span></span>  

| <span data-ttu-id="0cf3b-313">Donanım</span><span class="sxs-lookup"><span data-stu-id="0cf3b-313">Hardware</span></span> | <span data-ttu-id="0cf3b-314">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="0cf3b-314">Details</span></span> |
| --- | --- |
| <span data-ttu-id="0cf3b-315">CPU</span><span class="sxs-lookup"><span data-stu-id="0cf3b-315">CPU</span></span> |<span data-ttu-id="0cf3b-316">AMD Opteron(tm) işlemci 4171 HE / 4 çekirdek</span><span class="sxs-lookup"><span data-stu-id="0cf3b-316">AMD Opteron(tm) Processor 4171 HE/4 cores</span></span> |
| <span data-ttu-id="0cf3b-317">Bellek</span><span class="sxs-lookup"><span data-stu-id="0cf3b-317">Memory</span></span> |<span data-ttu-id="0cf3b-318">14 GB</span><span class="sxs-lookup"><span data-stu-id="0cf3b-318">14 GB</span></span> |
| <span data-ttu-id="0cf3b-319">Disk</span><span class="sxs-lookup"><span data-stu-id="0cf3b-319">Disk</span></span> |<span data-ttu-id="0cf3b-320">10 GB/disk</span><span class="sxs-lookup"><span data-stu-id="0cf3b-320">10 GB/disk</span></span> |
| <span data-ttu-id="0cf3b-321">İşletim Sistemi</span><span class="sxs-lookup"><span data-stu-id="0cf3b-321">OS</span></span> |<span data-ttu-id="0cf3b-322">Ubuntu 14.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="0cf3b-322">Ubuntu 14.04.1 LTS</span></span> |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

