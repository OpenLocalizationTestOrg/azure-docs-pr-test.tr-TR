---
title: "aaaLinux VM aygıt adlarını Azure'da değiştiğinde | Microsoft Docs"
description: "Neden aygıt adlarının değiştirilir ve bu sorun için çözüm sağlamak hello açıklanmaktadır."
services: virtual-machines-linux
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: 
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 4d3a5853d61edd2c8e8b85ab69e5ed3b3bc00bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a><span data-ttu-id="f303c-103">Sorunlarını giderme: Linux VM aygıt adlarının değişmesi</span><span class="sxs-lookup"><span data-stu-id="f303c-103">Troubleshooting: Linux VM device names are changed</span></span>

<span data-ttu-id="f303c-104">Linux sanal makine (VM) yeniden başlatın ya da hello diskleri yeniden iliştirmeye sonra aygıt adlarının neden değişmesi Hello makalede açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f303c-104">hello article explains why device names are changed after you restart a Linux virtual machine (VM), or reattach hello disks.</span></span> <span data-ttu-id="f303c-105">Ayrıca bu sorun için hello çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="f303c-105">It also provides hello solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="f303c-106">Belirti</span><span class="sxs-lookup"><span data-stu-id="f303c-106">Symptom</span></span>

<span data-ttu-id="f303c-107">Sorunları Linux VM'ler Microsoft Azure üzerinde çalışırken aşağıdaki hello karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f303c-107">You may experience hello following problems when running Linux VMs in Microsoft Azure.</span></span>

- <span data-ttu-id="f303c-108">Merhaba VM yeniden başlatma sonrasında tooboot başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="f303c-108">hello VM fails tooboot after a restart.</span></span>

- <span data-ttu-id="f303c-109">Veri diskleri ayrılmış ve yeniden, diskleri için hello aygıtları adları değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="f303c-109">If data disks are detached and reattached, hello devices names for disks are changed.</span></span>

- <span data-ttu-id="f303c-110">Bir uygulama veya aygıt adı kullanarak bir disk başvuruda bulunan komut dosyası başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="f303c-110">An application or script that references a disk by using device name fails.</span></span> <span data-ttu-id="f303c-111">Bu hello bulur hello disk aygıt adı değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="f303c-111">You find that hello device name of hello disk is changed.</span></span>

## <a name="cause"></a><span data-ttu-id="f303c-112">Nedeni</span><span class="sxs-lookup"><span data-stu-id="f303c-112">Cause</span></span>

<span data-ttu-id="f303c-113">Linux aygıt yollarında toobe tutarlı yeniden başlatmaları arasındaki garanti edilmez.</span><span class="sxs-lookup"><span data-stu-id="f303c-113">Device paths in Linux are not guaranteed toobe consistent across restarts.</span></span> <span data-ttu-id="f303c-114">Aygıt adlarının (harf) büyük ve küçük sayı oluşur.</span><span class="sxs-lookup"><span data-stu-id="f303c-114">Device names consist of major (letter) and minor numbers.</span></span>  <span data-ttu-id="f303c-115">Yeni bir cihaz Hello Linux depolama aygıtı sürücüsü algıladığında, birincil ve ikincil cihaz numaraları tooit hello kullanılabilir aralığından atar.</span><span class="sxs-lookup"><span data-stu-id="f303c-115">When hello Linux storage device driver detects a new device, it assigns major and minor device numbers tooit from hello available range.</span></span> <span data-ttu-id="f303c-116">Bir cihaz kaldırıldığında, hello aygıt daha sonra yeniden boşaltılmış toobe numaralarıdır.</span><span class="sxs-lookup"><span data-stu-id="f303c-116">When a device is removed, hello device numbers are freed toobe reused later.</span></span>

<span data-ttu-id="f303c-117">Merhaba Linux hello SCSI alt sistemi tarafından zamanlanmış tarama aygıtı zaman uyumsuz olarak olur hello sorun nedeniyle oluşur.</span><span class="sxs-lookup"><span data-stu-id="f303c-117">hello problem occurs because hello device scanning in Linux scheduled by hello SCSI subsystem happens asynchronously.</span></span> <span data-ttu-id="f303c-118">Merhaba son aygıt adlandırma yolu yeniden başlatmaları arasında farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="f303c-118">hello final device path naming may vary across restarts.</span></span> 

## <a name="solution"></a><span data-ttu-id="f303c-119">Çözüm</span><span class="sxs-lookup"><span data-stu-id="f303c-119">Solution</span></span>

<span data-ttu-id="f303c-120">tooresolve bu sorunu kalıcı adlandırma kullanın.</span><span class="sxs-lookup"><span data-stu-id="f303c-120">tooresolve this problem, use persistent naming.</span></span> <span data-ttu-id="f303c-121">Dört yöntemleri toopersistent vardır - filesystem etiketi, UUID, kimliğe göre ve tarafından yolu adlandırma.</span><span class="sxs-lookup"><span data-stu-id="f303c-121">There are four methods toopersistent naming - by filesystem label, by uuid, by id and by path.</span></span> <span data-ttu-id="f303c-122">Merhaba filesystem etiket ve UUID yöntemleri Azure Linux VM'ler için önerilir.</span><span class="sxs-lookup"><span data-stu-id="f303c-122">We recommend hello filesystem label and UUID methods for Azure Linux VMs.</span></span> 

<span data-ttu-id="f303c-123">Çoğu dağıtımları da ya da hello sağlamak **nofail** veya **nobootwait** fstab seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="f303c-123">Most distributions also provide either hello **nofail** or **nobootwait** fstab options.</span></span> <span data-ttu-id="f303c-124">Merhaba disk toomount başlangıçta başarısız olsa bile bu seçenekler sistem tooboot sağlar.</span><span class="sxs-lookup"><span data-stu-id="f303c-124">These options enable a system tooboot even if hello disk fails toomount at startup.</span></span> <span data-ttu-id="f303c-125">Bu parametreler hakkında daha fazla bilgi için Hello dağıtım'ın belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="f303c-125">Check hello distribution's documentation for more information about these parameters.</span></span> <span data-ttu-id="f303c-126">Bir Linux VM toouse bir veri diski eklediğinizde UUID tooconfigure nasıl gördükleri hakkında daha fazla bilgi için [toohello Linux VM toomount hello yeni disk bağlanmak](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="f303c-126">For more information about how tooconfigure a Linux VM toouse a UUID when you add a data disk, see [Connect toohello Linux VM toomount hello new disk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> 

<span data-ttu-id="f303c-127">Hello Azure Linux Aracısı VM üzerinde yüklü olduğunda, sembolik bağlantılar altında bir dizi Udev kuralları tooconstruct kullanan **/dev/disk/azure**.</span><span class="sxs-lookup"><span data-stu-id="f303c-127">When hello Azure Linux agent is installed on a VM, it uses Udev rules tooconstruct a set of symbolic links under **/dev/disk/azure**.</span></span> <span data-ttu-id="f303c-128">Udev kurallar uygulamalar tarafından kullanılabilir ve komut dosyaları tooidentify diskleri ekli toohello VM, kendi türü ve LUN hello.</span><span class="sxs-lookup"><span data-stu-id="f303c-128">These Udev rules can be used by applications and scripts tooidentify disks are attached toohello VM, their type, and hello LUN.</span></span>

## <a name="more-information"></a><span data-ttu-id="f303c-129">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="f303c-129">More information</span></span>

### <a name="identify-disk-luns"></a><span data-ttu-id="f303c-130">Diski LUN'ları tanımlayın</span><span class="sxs-lookup"><span data-stu-id="f303c-130">Identify disk LUNs</span></span>

<span data-ttu-id="f303c-131">Bir uygulama LUN toofind tüm bağlı hello diskleri ve oluşturma sembolik bağlantılar kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f303c-131">An application can use LUNs toofind all hello attached disks and constructing symbolic links.</span></span> <span data-ttu-id="f303c-132">Hello Azure Linux Aracısı şimdi sembolik bağlantılar bir LUN toohello aygıtlardan aşağıdaki gibi ayarlayın udev kurallarını içerir:</span><span class="sxs-lookup"><span data-stu-id="f303c-132">hello Azure Linux agent now includes udev rules that set up symbolic links from a LUN toohello devices, as follows:</span></span>

    $ tree /dev/disk/azure

    /dev/disk/azure
    ├── resource -> ../../sdb
    ├── resource-part1 -> ../../sdb1
    ├── root -> ../../sda
    ├── root-part1 -> ../../sda1
    └── scsi1
        ├── lun0 -> ../../../sdc
        ├── lun0-part1 -> ../../../sdc1
        ├── lun1 -> ../../../sdd
        ├── lun1-part1 -> ../../../sdd1
        ├── lun1-part2 -> ../../../sdd2
        └── lun1-part3 -> ../../../sdd3                                    
                                 

<span data-ttu-id="f303c-133">LUN bilgileri de hello Linux konuktaki lsscsi veya benzer bir aracı gibi kullanılarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="f303c-133">LUN information can also be retrieved from hello Linux guest using lsscsi or similar tool as follows.</span></span>

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

<span data-ttu-id="f303c-134">Bu Konuk LUN bilgileri Azure aboneliği meta veri tooidentify hello konumunu hello hello bölüm verileri depolayan VHD ile Azure depolama alanında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f303c-134">This guest LUN information can be used with Azure subscription metadata tooidentify hello location in Azure storage of hello VHD which stores hello partition data.</span></span> <span data-ttu-id="f303c-135">Örneğin, hello az CLI kullanın:</span><span class="sxs-lookup"><span data-stu-id="f303c-135">For example, use hello az cli:</span></span>

    $ az vm show --resource-group testVM --name testVM | jq -r .storageProfile.dataDisks                                        
    [                                                                                                                                                                  
    {                                                                                                                                                                  
    "caching": "None",                                                                                                                                              
      "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 1023,                                                                                                                                             
      "image": null,                                                                                                                                                   
    "lun": 0,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-114353",                                                                                                                    
    "vhd": {                                                                                                                                                          
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-114353.vhd"                                                       
    }                                                                                                                                                              
    },                                                                                                                                                                
    {                                                                                                                                                                   
    "caching": "None",                                                                                                                                               
    "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 512,                                                                                                                                              
    "image": null,                                                                                                                                                   
    "lun": 1,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-121516",                                                                                                                    
    "vhd": {                                                                                                                                                           
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-121516.vhd"                                                       
      }                                                                                                                                                             
      }                                                                                                                                                             
    ]

### <a name="discover-filesystem-uuids-by-using-blkid"></a><span data-ttu-id="f303c-136">Dosya sistemi UUID'ler blkid kullanarak Bul</span><span class="sxs-lookup"><span data-stu-id="f303c-136">Discover filesystem UUIDs by using blkid</span></span>

<span data-ttu-id="f303c-137">Bir komut dosyası veya uygulama blkid hello çıktısını ya da bilgi benzer kaynakları okuyabilir ve sembolik bağlantılar oluşturmak **/dev** kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="f303c-137">A script or application can read hello output of blkid, or similar sources of information, and construct symbolic links in **/dev** for use.</span></span> <span data-ttu-id="f303c-138">Merhaba çıkış ilişkili toohello VM ve hello aygıt dosya toowhich hello UUID tüm disklerin bağlı gösterir:</span><span class="sxs-lookup"><span data-stu-id="f303c-138">hello output will show hello UUIDs of all disks attached toohello VM and hello device file toowhich they are associated:</span></span>

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

<span data-ttu-id="f303c-139">Merhaba waagent udev kuralları oluşturmak sembolik bağlantılar altında bir dizi **/dev/disk/azure**:</span><span class="sxs-lookup"><span data-stu-id="f303c-139">hello waagent udev rules construct a set of symbolic links under **/dev/disk/azure**:</span></span>


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


<span data-ttu-id="f303c-140">Merhaba uygulaması, bu bilgiyi kullanabilir hello önyükleme disk aygıtı ve hello kaynak (kısa ömürlü) disk tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f303c-140">hello application can use this information identify hello boot disk device and hello resource (ephemeral) disk.</span></span> <span data-ttu-id="f303c-141">Azure'da, uygulamaları çok başvurmalıdır**/dev/disk/azure/root-part1** veya **/dev/disk/azure-resource-part1** toodiscover bu bölümler.</span><span class="sxs-lookup"><span data-stu-id="f303c-141">In Azure, applications should refer too**/dev/disk/azure/root-part1** or **/dev/disk/azure-resource-part1** toodiscover these partitions.</span></span>

<span data-ttu-id="f303c-142">Merhaba blkid listeden ek bölümler varsa, bunlar bir veri diski bulunur.</span><span class="sxs-lookup"><span data-stu-id="f303c-142">If there are additional partitions from hello blkid list, they reside on a data disk.</span></span> <span data-ttu-id="f303c-143">Uygulamalar bu bölümler için hello UUID korumak ve çalışma zamanında toodiscover hello aygıt adı altındaki hello gibi bir yol kullanın:</span><span class="sxs-lookup"><span data-stu-id="f303c-143">Applications can maintain hello UUID for these partitions and use a path like hello below toodiscover hello device name at runtime:</span></span>

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a><span data-ttu-id="f303c-144">Merhaba en son Azure depolama kuralları Al</span><span class="sxs-lookup"><span data-stu-id="f303c-144">Get hello latest Azure storage rules</span></span>

<span data-ttu-id="f303c-145">Azure depolama kuralları son toohello, aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f303c-145">toohello latest Azure storage rules, run th following commands:</span></span>

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


<span data-ttu-id="f303c-146">Daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="f303c-146">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="f303c-147">Ubuntu: UUID kullanma</span><span class="sxs-lookup"><span data-stu-id="f303c-147">Ubuntu: Using UUID</span></span>](https://help.ubuntu.com/community/UsingUUID)

- [<span data-ttu-id="f303c-148">Red Hat: Kalıcı adlandırma</span><span class="sxs-lookup"><span data-stu-id="f303c-148">Red Hat: Persistent Naming</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [<span data-ttu-id="f303c-149">Linux: UUID'ler için yapabilecekleriniz</span><span class="sxs-lookup"><span data-stu-id="f303c-149">Linux: What UUIDs can do for you</span></span>](https://www.linux.com/news/what-uuids-can-do-you)

- [<span data-ttu-id="f303c-150">Udev: Giriş tooDevice yönetim içinde Modern Linux sistemi</span><span class="sxs-lookup"><span data-stu-id="f303c-150">Udev: Introduction tooDevice Management In Modern Linux System</span></span>](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

