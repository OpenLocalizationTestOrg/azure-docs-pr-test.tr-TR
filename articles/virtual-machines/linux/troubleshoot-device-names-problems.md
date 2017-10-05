---
title: "Linux VM aygıt adlarını Azure'da değiştiğinde | Microsoft Docs"
description: "Nedenini açıklayan aygıtı adları değiştirilir ve bu sorun için çözüm sağlar."
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
ms.openlocfilehash: 789f4580901a22dc3aaae9599c7205c76f268403
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a><span data-ttu-id="598e5-103">Sorunlarını giderme: Linux VM aygıt adlarının değişmesi</span><span class="sxs-lookup"><span data-stu-id="598e5-103">Troubleshooting: Linux VM device names are changed</span></span>

<span data-ttu-id="598e5-104">Bu makalede, Linux sanal makine (VM) yeniden başlatın veya diskleri yeniden iliştirmeye sonra aygıt adlarının neden değişmesi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="598e5-104">The article explains why device names are changed after you restart a Linux virtual machine (VM), or reattach the disks.</span></span> <span data-ttu-id="598e5-105">Ayrıca bu sorun için çözüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="598e5-105">It also provides the solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="598e5-106">Belirti</span><span class="sxs-lookup"><span data-stu-id="598e5-106">Symptom</span></span>

<span data-ttu-id="598e5-107">Microsoft Azure Linux VM'ler çalıştırırken aşağıdaki sorunlarla karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="598e5-107">You may experience the following problems when running Linux VMs in Microsoft Azure.</span></span>

- <span data-ttu-id="598e5-108">VM yeniden başlatma sonrasında önyükleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="598e5-108">The VM fails to boot after a restart.</span></span>

- <span data-ttu-id="598e5-109">Veri diskleri ayrılmış ve yeniden, diskler için cihazları adları değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="598e5-109">If data disks are detached and reattached, the devices names for disks are changed.</span></span>

- <span data-ttu-id="598e5-110">Bir uygulama veya aygıt adı kullanarak bir disk başvuruda bulunan komut dosyası başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="598e5-110">An application or script that references a disk by using device name fails.</span></span> <span data-ttu-id="598e5-111">Disk aygıt adına değiştiğini bulun.</span><span class="sxs-lookup"><span data-stu-id="598e5-111">You find that the device name of the disk is changed.</span></span>

## <a name="cause"></a><span data-ttu-id="598e5-112">Nedeni</span><span class="sxs-lookup"><span data-stu-id="598e5-112">Cause</span></span>

<span data-ttu-id="598e5-113">Linux yollarında cihaz yeniden başlatmaları arasındaki tutarlı olması garanti edilmez.</span><span class="sxs-lookup"><span data-stu-id="598e5-113">Device paths in Linux are not guaranteed to be consistent across restarts.</span></span> <span data-ttu-id="598e5-114">Aygıt adlarının (harf) büyük ve küçük sayı oluşur.</span><span class="sxs-lookup"><span data-stu-id="598e5-114">Device names consist of major (letter) and minor numbers.</span></span>  <span data-ttu-id="598e5-115">Linux depolama aygıtı sürücüsü yeni bir cihaz algıladığında, birincil ve ikincil cihaz numaraları kullanılabilir aralıktan atar.</span><span class="sxs-lookup"><span data-stu-id="598e5-115">When the Linux storage device driver detects a new device, it assigns major and minor device numbers to it from the available range.</span></span> <span data-ttu-id="598e5-116">Bir cihaz kaldırıldığında, aygıtı sayıları daha sonra yeniden kurtulurlar.</span><span class="sxs-lookup"><span data-stu-id="598e5-116">When a device is removed, the device numbers are freed to be reused later.</span></span>

<span data-ttu-id="598e5-117">Sorun, Linux SCSI alt sistemi tarafından zamanlanmış tarama aygıt zaman uyumsuz olarak olur nedeniyle oluşur.</span><span class="sxs-lookup"><span data-stu-id="598e5-117">The problem occurs because the device scanning in Linux scheduled by the SCSI subsystem happens asynchronously.</span></span> <span data-ttu-id="598e5-118">Son aygıt adlandırma yolu yeniden başlatmaları arasında farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="598e5-118">The final device path naming may vary across restarts.</span></span> 

## <a name="solution"></a><span data-ttu-id="598e5-119">Çözüm</span><span class="sxs-lookup"><span data-stu-id="598e5-119">Solution</span></span>

<span data-ttu-id="598e5-120">Bu sorunu gidermek için kalıcı adlandırma kullanın.</span><span class="sxs-lookup"><span data-stu-id="598e5-120">To resolve this problem, use persistent naming.</span></span> <span data-ttu-id="598e5-121">Dört yöntem kalıcı adlandırma için - filesystem etiketi, UUID, kimliğe göre ve tarafından yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="598e5-121">There are four methods to persistent naming - by filesystem label, by uuid, by id and by path.</span></span> <span data-ttu-id="598e5-122">Dosya sistemi etiket ve UUID yöntemleri Azure Linux VM'ler için önerilir.</span><span class="sxs-lookup"><span data-stu-id="598e5-122">We recommend the filesystem label and UUID methods for Azure Linux VMs.</span></span> 

<span data-ttu-id="598e5-123">Çoğu dağıtımları da ya da sağlamak **nofail** veya **nobootwait** fstab seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="598e5-123">Most distributions also provide either the **nofail** or **nobootwait** fstab options.</span></span> <span data-ttu-id="598e5-124">Bu seçenekler, başlangıçta bağlamak disk başarısız olsa bile önyükleme sistemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="598e5-124">These options enable a system to boot even if the disk fails to mount at startup.</span></span> <span data-ttu-id="598e5-125">Bu parametreler hakkında daha fazla bilgi için dağıtım ait belgelere bakın.</span><span class="sxs-lookup"><span data-stu-id="598e5-125">Check the distribution's documentation for more information about these parameters.</span></span> <span data-ttu-id="598e5-126">Bir veri diski eklediğinizde bir UUID kullanmak için bir Linux VM yapılandırma hakkında daha fazla bilgi için bkz: [yeni diski Linux VM Bağlan](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="598e5-126">For more information about how to configure a Linux VM to use a UUID when you add a data disk, see [Connect to the Linux VM to mount the new disk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> 

<span data-ttu-id="598e5-127">Azure Linux Aracısı VM üzerinde yüklü olduğunda Udev kuralları altında sembolik bağlantılar kümesi oluşturmak için kullandığı **/dev/disk/azure**.</span><span class="sxs-lookup"><span data-stu-id="598e5-127">When the Azure Linux agent is installed on a VM, it uses Udev rules to construct a set of symbolic links under **/dev/disk/azure**.</span></span> <span data-ttu-id="598e5-128">Udev kurallar uygulamalar tarafından kullanılabilir ve diskleri tanımlamak için komut dosyaları VM, kendi türü ve LUN'a bağlı.</span><span class="sxs-lookup"><span data-stu-id="598e5-128">These Udev rules can be used by applications and scripts to identify disks are attached to the VM, their type, and the LUN.</span></span>

## <a name="more-information"></a><span data-ttu-id="598e5-129">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="598e5-129">More information</span></span>

### <a name="identify-disk-luns"></a><span data-ttu-id="598e5-130">Diski LUN'ları tanımlayın</span><span class="sxs-lookup"><span data-stu-id="598e5-130">Identify disk LUNs</span></span>

<span data-ttu-id="598e5-131">Bir uygulama, tüm dünyada sembolik bağlantılar ve bağlı disklerde bulmak için LUN'ları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="598e5-131">An application can use LUNs to find all the attached disks and constructing symbolic links.</span></span> <span data-ttu-id="598e5-132">Azure Linux Aracısı'nı şimdi sembolik bağlantılar bir LUN cihazlara aşağıdaki gibi ayarlayın udev kurallarını içerir:</span><span class="sxs-lookup"><span data-stu-id="598e5-132">The Azure Linux agent now includes udev rules that set up symbolic links from a LUN to the devices, as follows:</span></span>

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
                                 

<span data-ttu-id="598e5-133">LUN bilgileri de lsscsi veya benzer bir aracı gibi kullanarak Linux konuktaki alınabilir.</span><span class="sxs-lookup"><span data-stu-id="598e5-133">LUN information can also be retrieved from the Linux guest using lsscsi or similar tool as follows.</span></span>

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

<span data-ttu-id="598e5-134">Bu Konuk LUN bilgileri Azure aboneliği meta verileriyle bölüm verileri depolayan VHD Azure depolama alanında konumunu tanımlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="598e5-134">This guest LUN information can be used with Azure subscription metadata to identify the location in Azure storage of the VHD which stores the partition data.</span></span> <span data-ttu-id="598e5-135">Örneğin, az CLI kullanın:</span><span class="sxs-lookup"><span data-stu-id="598e5-135">For example, use the az cli:</span></span>

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

### <a name="discover-filesystem-uuids-by-using-blkid"></a><span data-ttu-id="598e5-136">Dosya sistemi UUID'ler blkid kullanarak Bul</span><span class="sxs-lookup"><span data-stu-id="598e5-136">Discover filesystem UUIDs by using blkid</span></span>

<span data-ttu-id="598e5-137">Bir komut dosyası veya uygulama blkid çıktısını ya da bilgi benzer kaynakları okuyabilir ve sembolik bağlantılar oluşturmak **/dev** kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="598e5-137">A script or application can read the output of blkid, or similar sources of information, and construct symbolic links in **/dev** for use.</span></span> <span data-ttu-id="598e5-138">Çıktı VM ve için ilişkili oldukları aygıt dosyası bağlı tüm diskleri UUID'ler gösterir:</span><span class="sxs-lookup"><span data-stu-id="598e5-138">The output will show the UUIDs of all disks attached to the VM and the device file to which they are associated:</span></span>

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

<span data-ttu-id="598e5-139">Sembolik bağlantılar altında bir dizi waagent udev kuralları oluşturmak **/dev/disk/azure**:</span><span class="sxs-lookup"><span data-stu-id="598e5-139">The waagent udev rules construct a set of symbolic links under **/dev/disk/azure**:</span></span>


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


<span data-ttu-id="598e5-140">Uygulama bu bilgileri kullanabilir önyükleme diski cihaz ve kaynak (kısa ömürlü) disk tanımlar.</span><span class="sxs-lookup"><span data-stu-id="598e5-140">The application can use this information identify the boot disk device and the resource (ephemeral) disk.</span></span> <span data-ttu-id="598e5-141">Azure'da, uygulamalar için başvurmalıdır **/dev/disk/azure/root-part1** veya **/dev/disk/azure-resource-part1** bu bölümler bulmak için.</span><span class="sxs-lookup"><span data-stu-id="598e5-141">In Azure, applications should refer to **/dev/disk/azure/root-part1** or **/dev/disk/azure-resource-part1** to discover these partitions.</span></span>

<span data-ttu-id="598e5-142">Ek bölümlere blkid listede yoksa, bir veri diski bulundukları.</span><span class="sxs-lookup"><span data-stu-id="598e5-142">If there are additional partitions from the blkid list, they reside on a data disk.</span></span> <span data-ttu-id="598e5-143">Uygulamalar bu bölümler UUID'si korumak ve gibi bir yol kullanmak aşağıdaki çalışma zamanında cihaz adını bulmak için:</span><span class="sxs-lookup"><span data-stu-id="598e5-143">Applications can maintain the UUID for these partitions and use a path like the below to discover the device name at runtime:</span></span>

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-the-latest-azure-storage-rules"></a><span data-ttu-id="598e5-144">En son Azure depolama kuralları Al</span><span class="sxs-lookup"><span data-stu-id="598e5-144">Get the latest Azure storage rules</span></span>

<span data-ttu-id="598e5-145">En son Azure depolama kuralları aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="598e5-145">To the latest Azure storage rules, run th following commands:</span></span>

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


<span data-ttu-id="598e5-146">Daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="598e5-146">For more information, see the following articles:</span></span>

- [<span data-ttu-id="598e5-147">Ubuntu: UUID kullanma</span><span class="sxs-lookup"><span data-stu-id="598e5-147">Ubuntu: Using UUID</span></span>](https://help.ubuntu.com/community/UsingUUID)

- [<span data-ttu-id="598e5-148">Red Hat: Kalıcı adlandırma</span><span class="sxs-lookup"><span data-stu-id="598e5-148">Red Hat: Persistent Naming</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [<span data-ttu-id="598e5-149">Linux: UUID'ler için yapabilecekleriniz</span><span class="sxs-lookup"><span data-stu-id="598e5-149">Linux: What UUIDs can do for you</span></span>](https://www.linux.com/news/what-uuids-can-do-you)

- [<span data-ttu-id="598e5-150">Udev: Aygıt Yönetimi Modern Linux sistemindeki giriş</span><span class="sxs-lookup"><span data-stu-id="598e5-150">Udev: Introduction to Device Management In Modern Linux System</span></span>](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

