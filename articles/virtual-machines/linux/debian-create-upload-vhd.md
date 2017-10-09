---
title: aaaPrepare Debian bir Linux Azure VHD | Microsoft Docs
description: "Nasıl toocreate Debian 7 ve 8 VHD dosyalarını Azure dağıtımdaki öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: a6de7a7c-cc70-44e7-aed0-2ae6884d401a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: e67d126de3db146357a6509aedb5f478576768f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a><span data-ttu-id="8fa89-103">Azure için Debian VHD hazırlama</span><span class="sxs-lookup"><span data-stu-id="8fa89-103">Prepare a Debian VHD for Azure</span></span>
## <a name="prerequisites"></a><span data-ttu-id="8fa89-104">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8fa89-104">Prerequisites</span></span>
<span data-ttu-id="8fa89-105">Bu bölümde, zaten Debian Linux işletim sistemi hello indirilen bir .iso dosyasından yüklediğinizi varsayar [Debian Web sitesi](https://www.debian.org/distrib/) tooa sanal sabit disk.</span><span class="sxs-lookup"><span data-stu-id="8fa89-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from hello [Debian website](https://www.debian.org/distrib/) tooa virtual hard disk.</span></span> <span data-ttu-id="8fa89-106">Birden çok araç toocreate .vhd dosyaları var; Hyper-V yalnızca bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="8fa89-106">Multiple tools exist toocreate .vhd files; Hyper-V is only one example.</span></span> <span data-ttu-id="8fa89-107">Hyper-V kullanma yönergeleri için bkz: [hello Hyper-V rolünü yükleyin ve sanal makine yapılandırma](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="8fa89-107">For instructions using Hyper-V, see [Install hello Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

## <a name="installation-notes"></a><span data-ttu-id="8fa89-108">Yükleme notları</span><span class="sxs-lookup"><span data-stu-id="8fa89-108">Installation notes</span></span>
* <span data-ttu-id="8fa89-109">Ayrıca bkz [genel Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes) Linux Azure için hazırlama hakkında daha fazla ipucu için.</span><span class="sxs-lookup"><span data-stu-id="8fa89-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="8fa89-110">Azure'da Hello yeni VHDX biçimi desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="8fa89-110">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="8fa89-111">Hyper-V Yöneticisi'ni veya hello kullanarak hello disk tooVHD biçimine dönüştürebilirsiniz **convert-vhd** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8fa89-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello **convert-vhd** cmdlet.</span></span>
* <span data-ttu-id="8fa89-112">Merhaba Linux sistemi yüklerken LVM (genellikle birçok yüklemeleri için hello varsayılan) yerine standart bölümlerini kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="8fa89-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="8fa89-113">Özellikle bir işletim sistemi herhangi bir zamanda ihtiyaçlarını bağlı toobe tooanother VM sorun giderme için disk varsa bu LVM ad çakışmalarını kopyalanan VMs önler.</span><span class="sxs-lookup"><span data-stu-id="8fa89-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="8fa89-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veri disklerde tercih edilen varsa kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8fa89-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="8fa89-115">Bir takas bölüm hello işletim sistemi disk üzerinde yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="8fa89-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="8fa89-116">Hello Azure Linux Aracısı yapılandırılmış toocreate hello geçici kaynak disk üzerinde bir takas dosyası olabilir.</span><span class="sxs-lookup"><span data-stu-id="8fa89-116">hello Azure Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="8fa89-117">Merhaba aşağıdaki adımlarda bu hakkında daha fazla bilgi bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="8fa89-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="8fa89-118">Tüm hello VHD boyutları 1 MB'ün katları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8fa89-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-azure-manage-toocreate-debian-vhds"></a><span data-ttu-id="8fa89-119">Azure yönetmek toocreate Debian VHD'ler kullanın</span><span class="sxs-lookup"><span data-stu-id="8fa89-119">Use Azure-Manage toocreate Debian VHDs</span></span>
<span data-ttu-id="8fa89-120">Araçlar Azure, Debian VHD'ler gibi hello oluşturmak için kullanılabilir [azure-yönetmek](https://github.com/credativ/azure-manage) betikten [credativ](http://www.credativ.com/).</span><span class="sxs-lookup"><span data-stu-id="8fa89-120">There are tools available for generating Debian VHDs for Azure, such as hello [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span></span> <span data-ttu-id="8fa89-121">Bu önerilen yaklaşımı sıfırdan bir görüntü oluşturma karşı hello olur.</span><span class="sxs-lookup"><span data-stu-id="8fa89-121">This is hello recommended approach versus creating an image from scratch.</span></span> <span data-ttu-id="8fa89-122">Örneğin, toocreate Debian 8 VHD'yi komutları toodownload azure Yönet aşağıdaki hello (ve bağımlılıklarını) çalıştırın ve hello azure_build_image betiğini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8fa89-122">For example, toocreate a Debian 8 VHD run hello following commands toodownload azure-manage (and dependencies) and run hello azure_build_image script:</span></span>

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a><span data-ttu-id="8fa89-123">El ile Debian VHD hazırlama</span><span class="sxs-lookup"><span data-stu-id="8fa89-123">Manually prepare a Debian VHD</span></span>
1. <span data-ttu-id="8fa89-124">Hyper-V Yöneticisi'nde hello sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="8fa89-124">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="8fa89-125">Tıklatın **Bağlan** tooopen hello sanal makine için bir konsol penceresi.</span><span class="sxs-lookup"><span data-stu-id="8fa89-125">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="8fa89-126">Açıklama hello satırı çıkışı **deb cdrom** içinde `/etc/apt/source.list` hello VM ISO dosyasını karşı ayarlarsanız.</span><span class="sxs-lookup"><span data-stu-id="8fa89-126">Comment out hello line for **deb cdrom** in `/etc/apt/source.list` if you set up hello VM against an ISO file.</span></span>
4. <span data-ttu-id="8fa89-127">Merhaba Düzenle `/etc/default/grub` dosya ve hello değiştirme **GRUB_CMDLINE_LINUX** Azure için tooinclude ek çekirdek parametreleri aşağıdaki gibi parametre.</span><span class="sxs-lookup"><span data-stu-id="8fa89-127">Edit hello `/etc/default/grub` file and modify hello **GRUB_CMDLINE_LINUX** parameter as follows tooinclude additional kernel parameters for Azure.</span></span>
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. <span data-ttu-id="8fa89-128">Merhaba kaz yeniden oluşturun ve çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8fa89-128">Rebuild hello grub and run:</span></span>
   
        # sudo update-grub
6. <span data-ttu-id="8fa89-129">Debian'ın Azure depoları too/etc/apt/sources.list Debian 7 veya 8 için ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8fa89-129">Add Debian's Azure repositories too/etc/apt/sources.list for either Debian 7 or 8:</span></span>
   
    <span data-ttu-id="8fa89-130">**Wheezy debian 7.x""**</span><span class="sxs-lookup"><span data-stu-id="8fa89-130">**Debian 7.x "Wheezy"**</span></span>
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    <span data-ttu-id="8fa89-131">**Debian 8.x "Jessie"**</span><span class="sxs-lookup"><span data-stu-id="8fa89-131">**Debian 8.x "Jessie"**</span></span>

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. <span data-ttu-id="8fa89-132">Hello Azure Linux aracısı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="8fa89-132">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. <span data-ttu-id="8fa89-133">Debian 7 için gerekli toorun hello 3.16 tabanlı çekirdek hello backports wheezy depodan'dir.</span><span class="sxs-lookup"><span data-stu-id="8fa89-133">For Debian 7, it is required toorun hello 3.16-based kernel from hello wheezy-backports repository.</span></span> <span data-ttu-id="8fa89-134">İlk /etc/apt/preferences.d/linux.pref içeriği aşağıdaki hello ile adlı bir dosya oluşturun:</span><span class="sxs-lookup"><span data-stu-id="8fa89-134">First create a file called /etc/apt/preferences.d/linux.pref with hello following contents:</span></span>
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    <span data-ttu-id="8fa89-135">Ardından tooinstall hello yeni çekirdek "apt sudo get yükle linux görüntü amd64" çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8fa89-135">Then run "sudo apt-get install linux-image-amd64" tooinstall hello new kernel.</span></span>
3. <span data-ttu-id="8fa89-136">Merhaba sanal makine yetkisini kaldırma ve Azure üzerinde sağlamak için hazırlayın ve çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8fa89-136">Deprovision hello virtual machine and prepare it for provisioning on Azure and run:</span></span>
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. <span data-ttu-id="8fa89-137">Tıklatın **eylem** Hyper-V Yöneticisi'nde kapatma aşağı ->.</span><span class="sxs-lookup"><span data-stu-id="8fa89-137">Click **Action** -> Shut Down in Hyper-V Manager.</span></span> <span data-ttu-id="8fa89-138">Hazır toobe tooAzure karşıya artık Linux VHD olur.</span><span class="sxs-lookup"><span data-stu-id="8fa89-138">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fa89-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8fa89-139">Next steps</span></span>
<span data-ttu-id="8fa89-140">Artık hazır toouse Debian sanal sabit disk toocreate yeni sanal makinelerinizi Azure demektir.</span><span class="sxs-lookup"><span data-stu-id="8fa89-140">You're now ready toouse your Debian virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="8fa89-141">Adım 2 ve 3'te bu hello hello .vhd dosyası tooAzure karşıya yüklüyoruz ilk kez kullanıyorsanız, bkz: [oluşturma ve hello Linux işletim sistemini içeren bir sanal sabit disk karşıya](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8fa89-141">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

