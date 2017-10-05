---
title: "Azure'da Debian bir Linux VHD hazırlama | Microsoft Docs"
description: "Debian 7 & dağıtımı için 8 VHD dosyalarını Azure'da oluşturmayı öğrenin."
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
ms.openlocfilehash: 63970d162c12984d6476bf0b9fc4ab70160eccdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a><span data-ttu-id="9de39-103">Azure için Debian VHD hazırlama</span><span class="sxs-lookup"><span data-stu-id="9de39-103">Prepare a Debian VHD for Azure</span></span>
## <a name="prerequisites"></a><span data-ttu-id="9de39-104">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9de39-104">Prerequisites</span></span>
<span data-ttu-id="9de39-105">Bu bölümde, zaten Debian Linux işletim sistemi yüklenen bir .iso dosyasından yüklediğinizi varsayar [Debian Web sitesi](https://www.debian.org/distrib/) bir sanal sabit disk için.</span><span class="sxs-lookup"><span data-stu-id="9de39-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from the [Debian website](https://www.debian.org/distrib/) to a virtual hard disk.</span></span> <span data-ttu-id="9de39-106">Birden çok araç, .vhd dosyaları oluşturmak için mevcut; Hyper-V yalnızca bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="9de39-106">Multiple tools exist to create .vhd files; Hyper-V is only one example.</span></span> <span data-ttu-id="9de39-107">Hyper-V kullanma yönergeleri için bkz: [Hyper-V rolünü yükleyin ve sanal makine yapılandırma](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="9de39-107">For instructions using Hyper-V, see [Install the Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

## <a name="installation-notes"></a><span data-ttu-id="9de39-108">Yükleme notları</span><span class="sxs-lookup"><span data-stu-id="9de39-108">Installation notes</span></span>
* <span data-ttu-id="9de39-109">Ayrıca bkz [genel Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes) Linux Azure için hazırlama hakkında daha fazla ipucu için.</span><span class="sxs-lookup"><span data-stu-id="9de39-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="9de39-110">Azure'da yeni VHDX biçimi desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="9de39-110">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="9de39-111">Disk Hyper-V Yöneticisi'ni kullanarak VHD biçimine Dönüştür veya **convert-vhd** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="9de39-111">You can convert the disk to VHD format using Hyper-V Manager or the **convert-vhd** cmdlet.</span></span>
* <span data-ttu-id="9de39-112">Linux sistemini yüklerken LVM (genellikle birçok yüklemeleri için varsayılan) yerine standart bölümlerini kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="9de39-112">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="9de39-113">Özellikle bir işletim sistemi diski şimdiye kadar başka bir VM için sorun giderme için eklenmesi gerekiyorsa, bu kopyalanan VMs LVM ad çakışmalarını önler.</span><span class="sxs-lookup"><span data-stu-id="9de39-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="9de39-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veri disklerde tercih edilen varsa kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9de39-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="9de39-115">Bir takas bölüm işletim sistemi disk üzerinde yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="9de39-115">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="9de39-116">Azure Linux Aracısı geçici kaynak disk üzerinde bir takas dosyası oluşturmak için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="9de39-116">The Azure Linux agent can be configured to create a swap file on the temporary resource disk.</span></span> <span data-ttu-id="9de39-117">Aşağıdaki adımlarda bu hakkında daha fazla bilgi bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="9de39-117">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="9de39-118">Tüm VHD'leri boyutları 1 MB'ün katları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9de39-118">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-azure-manage-to-create-debian-vhds"></a><span data-ttu-id="9de39-119">Debian VHD oluşturmak için Azure yönetmek kullanın</span><span class="sxs-lookup"><span data-stu-id="9de39-119">Use Azure-Manage to create Debian VHDs</span></span>
<span data-ttu-id="9de39-120">Araçlar Azure, Debian VHD'ler gibi oluşturmak için kullanılabilir [azure-yönetmek](https://github.com/credativ/azure-manage) betikten [credativ](http://www.credativ.com/).</span><span class="sxs-lookup"><span data-stu-id="9de39-120">There are tools available for generating Debian VHDs for Azure, such as the [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span></span> <span data-ttu-id="9de39-121">Bu, sıfırdan bir görüntü oluşturma karşı önerilen yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="9de39-121">This is the recommended approach versus creating an image from scratch.</span></span> <span data-ttu-id="9de39-122">Örneğin, oluşturmak için bir Debian 8 yüklemek için aşağıdaki komutları çalıştırın azure-yönetebilirsiniz (ve bağımlılıklarını) ve azure_build_image komut dosyasını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9de39-122">For example, to create a Debian 8 VHD run the following commands to download azure-manage (and dependencies) and run the azure_build_image script:</span></span>

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a><span data-ttu-id="9de39-123">El ile Debian VHD hazırlama</span><span class="sxs-lookup"><span data-stu-id="9de39-123">Manually prepare a Debian VHD</span></span>
1. <span data-ttu-id="9de39-124">Hyper-V Yöneticisi'nde sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="9de39-124">In Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="9de39-125">Tıklatın **Bağlan** sanal makine için bir konsol penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="9de39-125">Click **Connect** to open a console window for the virtual machine.</span></span>
3. <span data-ttu-id="9de39-126">Açıklama satırı çıkışı **deb cdrom** içinde `/etc/apt/source.list` bir ISO dosyası karşı VM ayarlarsanız.</span><span class="sxs-lookup"><span data-stu-id="9de39-126">Comment out the line for **deb cdrom** in `/etc/apt/source.list` if you set up the VM against an ISO file.</span></span>
4. <span data-ttu-id="9de39-127">Düzen `/etc/default/grub` dosya ve değiştirme **GRUB_CMDLINE_LINUX** gibi ek çekirdek parametreleri için Azure içerecek şekilde parametresi.</span><span class="sxs-lookup"><span data-stu-id="9de39-127">Edit the `/etc/default/grub` file and modify the **GRUB_CMDLINE_LINUX** parameter as follows to include additional kernel parameters for Azure.</span></span>
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. <span data-ttu-id="9de39-128">Kaz yeniden oluşturun ve çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9de39-128">Rebuild the grub and run:</span></span>
   
        # sudo update-grub
6. <span data-ttu-id="9de39-129">Debian'ın Azure depoları için /etc/apt/sources.list Debian 7 veya 8 için ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9de39-129">Add Debian's Azure repositories to /etc/apt/sources.list for either Debian 7 or 8:</span></span>
   
    <span data-ttu-id="9de39-130">**Wheezy debian 7.x""**</span><span class="sxs-lookup"><span data-stu-id="9de39-130">**Debian 7.x "Wheezy"**</span></span>
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    <span data-ttu-id="9de39-131">**Debian 8.x "Jessie"**</span><span class="sxs-lookup"><span data-stu-id="9de39-131">**Debian 8.x "Jessie"**</span></span>

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. <span data-ttu-id="9de39-132">Azure Linux Aracısı'nı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="9de39-132">Install the Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. <span data-ttu-id="9de39-133">Debian 7'de, backports wheezy depodan 3.16 tabanlı çekirdek çalıştırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9de39-133">For Debian 7, it is required to run the 3.16-based kernel from the wheezy-backports repository.</span></span> <span data-ttu-id="9de39-134">İlk aşağıdaki içeriğe sahip /etc/apt/preferences.d/linux.pref adlı bir dosya oluşturun:</span><span class="sxs-lookup"><span data-stu-id="9de39-134">First create a file called /etc/apt/preferences.d/linux.pref with the following contents:</span></span>
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    <span data-ttu-id="9de39-135">Yeni çekirdek yüklemek için çalıştırın "sudo, get apt yükleme, linux-görüntü-amd64".</span><span class="sxs-lookup"><span data-stu-id="9de39-135">Then run "sudo apt-get install linux-image-amd64" to install the new kernel.</span></span>
3. <span data-ttu-id="9de39-136">Sanal makine yetkisini kaldırma ve Azure üzerinde sağlamak için hazırlayın ve çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9de39-136">Deprovision the virtual machine and prepare it for provisioning on Azure and run:</span></span>
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. <span data-ttu-id="9de39-137">Tıklatın **eylem** Hyper-V Yöneticisi'nde kapatma aşağı ->.</span><span class="sxs-lookup"><span data-stu-id="9de39-137">Click **Action** -> Shut Down in Hyper-V Manager.</span></span> <span data-ttu-id="9de39-138">Linux VHD Azure'a karşıya yüklenecek artık hazırdır.</span><span class="sxs-lookup"><span data-stu-id="9de39-138">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9de39-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9de39-139">Next steps</span></span>
<span data-ttu-id="9de39-140">Şimdi yeni sanal makineler oluşturmak için Debian, sanal sabit diski kullanmak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="9de39-140">You're now ready to use your Debian virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="9de39-141">Adım 2 ve 3'te Azure'a .vhd dosyasını karşıya yüklüyoruz ilk kez kullanıyorsanız bkz [oluşturma ve Linux işletim sistemini içeren bir sanal sabit disk karşıya](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9de39-141">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

