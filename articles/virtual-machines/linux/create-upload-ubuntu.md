---
title: "Oluşturma ve Azure bir Ubuntu Linux VHD yükleme"
description: "Oluşturma ve bir Azure sanal sabit bir Ubuntu Linux işletim sistemini içeren disk (VHD) yükleme hakkında bilgi edinme."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 3e097959-84fc-4f6a-8cc8-35e087fd1542
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 4496b34ff88ca1e08cc74788ae09d787d4399eaf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="bc184-103">Azure’da Ubuntu sanal makinesi hazırlama</span><span class="sxs-lookup"><span data-stu-id="bc184-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="bc184-104">Resmi Ubuntu bulut görüntüleri</span><span class="sxs-lookup"><span data-stu-id="bc184-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="bc184-105">Ubuntu şimdi adresten resmi Azure VHD'ler yayımlar [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="bc184-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="bc184-106">Azure için kendi özel Ubuntu görüntü oluşturmak gerekiyorsa, bunun yerine el ile aşağıdaki yordamı kullanın daha VHD'ler çalışma bilinen bunlarla başlatmak ve gerektiği şekilde özelleştirmek için önerilir.</span><span class="sxs-lookup"><span data-stu-id="bc184-106">If you need to build your own specialized Ubuntu image for Azure, rather than use the manual procedure below it is recommended to start with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="bc184-107">En son görüntü yayımları her zaman aşağıdaki konumlarda bulunabilir:</span><span class="sxs-lookup"><span data-stu-id="bc184-107">The latest image releases can always be found at the following locations:</span></span>

* <span data-ttu-id="bc184-108">Ubuntu 12.04/kesin: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="bc184-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="bc184-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="bc184-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="bc184-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="bc184-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc184-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bc184-111">Prerequisites</span></span>
<span data-ttu-id="bc184-112">Bu makalede, bir sanal sabit disk için bir Ubuntu Linux işletim sistemi zaten yüklediğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="bc184-112">This article assumes that you have already installed an Ubuntu Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="bc184-113">Birden çok araç, .vhd dosyaları, örneğin bir Hyper-V gibi sanallaştırma çözümü oluşturmak için mevcut.</span><span class="sxs-lookup"><span data-stu-id="bc184-113">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="bc184-114">Yönergeler için bkz: [Hyper-V rolünü yükleyin ve sanal makine yapılandırma](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="bc184-114">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="bc184-115">**Ubuntu yükleme notları**</span><span class="sxs-lookup"><span data-stu-id="bc184-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="bc184-116">Ayrıca bkz [genel Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes) Linux Azure için hazırlama hakkında daha fazla ipucu için.</span><span class="sxs-lookup"><span data-stu-id="bc184-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="bc184-117">VHDX biçimi, Azure'da yalnızca desteklenmiyor **VHD sabit**.</span><span class="sxs-lookup"><span data-stu-id="bc184-117">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="bc184-118">Disk Hyper-V Yöneticisi'ni veya convert-vhd cmdlet'ini kullanarak VHD biçimine dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc184-118">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="bc184-119">Linux sistemini yüklerken LVM (genellikle birçok yüklemeleri için varsayılan) yerine standart bölümlerini kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="bc184-119">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="bc184-120">Özellikle bir işletim sistemi diski şimdiye kadar başka bir VM için sorun giderme için eklenmesi gerekiyorsa, bu kopyalanan VMs LVM ad çakışmalarını önler.</span><span class="sxs-lookup"><span data-stu-id="bc184-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="bc184-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veri disklerde tercih edilen varsa kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bc184-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="bc184-122">Bir takas bölüm işletim sistemi disk üzerinde yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="bc184-122">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="bc184-123">Linux Aracısı geçici kaynak disk üzerinde bir takas dosyası oluşturmak için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="bc184-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="bc184-124">Aşağıdaki adımlarda bu hakkında daha fazla bilgi bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="bc184-124">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="bc184-125">Tüm VHD'leri boyutları 1 MB'ün katları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bc184-125">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="bc184-126">El ile adımlar</span><span class="sxs-lookup"><span data-stu-id="bc184-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="bc184-127">Azure için kendi özel Ubuntu görüntü oluşturmayı denemeden önce lütfen önceden oluşturulmuş ve test edilen görüntülerden kullanmayı [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) yerine.</span><span class="sxs-lookup"><span data-stu-id="bc184-127">Before attempting to create your own custom Ubuntu image for Azure, please consider using the pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="bc184-128">Hyper-V Yöneticisi'nin Orta bölmede sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="bc184-128">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="bc184-129">Tıklatın **Bağlan** sanal makine için penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="bc184-129">Click **Connect** to open the window for the virtual machine.</span></span>

3. <span data-ttu-id="bc184-130">Ubuntu'nın Azure depoları kullanmak üzere görüntüsündeki geçerli depoları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bc184-130">Replace the current repositories in the image to use Ubuntu's Azure repos.</span></span> <span data-ttu-id="bc184-131">Adımlar, Ubuntu sürüm bağlı olarak biraz farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="bc184-131">The steps vary slightly depending on the Ubuntu version.</span></span>
   
    <span data-ttu-id="bc184-132">Düzenleme önce `/etc/apt/sources.list`, yedekleme yapmak için önerilir:</span><span class="sxs-lookup"><span data-stu-id="bc184-132">Before editing `/etc/apt/sources.list`, it is recommended to make a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="bc184-133">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="bc184-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="bc184-134">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="bc184-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="bc184-135">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="bc184-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="bc184-136">Ubuntu Azure görüntüleri şimdi aşağıdaki *donanım etkinleştirme* (HWE) çekirdek.</span><span class="sxs-lookup"><span data-stu-id="bc184-136">The Ubuntu Azure images are now following the *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="bc184-137">İşletim sistemi, aşağıdaki komutları çalıştırarak son çekirdeğe güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="bc184-137">Update the operating system to the latest kernel by running the following commands:</span></span>

    <span data-ttu-id="bc184-138">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="bc184-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="bc184-139">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="bc184-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="bc184-140">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="bc184-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="bc184-141">**Ayrıca bkz.:**</span><span class="sxs-lookup"><span data-stu-id="bc184-141">**See also:**</span></span>
    - [<span data-ttu-id="bc184-142">https://Wiki.ubuntu.com/Kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="bc184-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="bc184-143">https://Wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="bc184-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="bc184-144">Azure için ek çekirdek parametreleri içerecek şekilde kaz için çekirdek önyükleme satırı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bc184-144">Modify the kernel boot line for Grub to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="bc184-145">Bu açık yapmak için `/etc/default/grub` adlı değişken bir metin düzenleyicisinde Bul `GRUB_CMDLINE_LINUX_DEFAULT` (veya gerekirse ekleyin) ve aşağıdaki parametreleri içerecek şekilde düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="bc184-145">To do this open `/etc/default/grub` in a text editor, find the variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it to include the following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="bc184-146">Kaydet ve bu dosyayı kapatın ve ardından çalıştırın `sudo update-grub`.</span><span class="sxs-lookup"><span data-stu-id="bc184-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="bc184-147">Bu, tüm konsol iletileri sorunları ayıklama Azure teknik destek yardımcı olabilecek ilk seri bağlantı noktasına gönderilen güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="bc184-147">This will ensure all console messages are sent to the first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="bc184-148">SSH sunucusu yüklü ve önyükleme sırasında başlatılacak şekilde yapılandırılmış olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bc184-148">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="bc184-149">Bu genellikle varsayılan seçenektir.</span><span class="sxs-lookup"><span data-stu-id="bc184-149">This is usually the default.</span></span>

7. <span data-ttu-id="bc184-150">Azure Linux Aracısı'nı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="bc184-150">Install the Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="bc184-151">`walinuxagent` Paketi kaldırmak `NetworkManager` ve `NetworkManager-gnome` yüklenmişlerse paketler.</span><span class="sxs-lookup"><span data-stu-id="bc184-151">The `walinuxagent` package may remove the `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="bc184-152">Sanal makine yetkisini kaldırma ve Azure üzerinde sağlamak için hazırlamak için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="bc184-152">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="bc184-153">Tıklatın **eylem -> kapatma aşağı** Hyper-V Yöneticisi'nde.</span><span class="sxs-lookup"><span data-stu-id="bc184-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="bc184-154">Linux VHD Azure'a karşıya yüklenecek artık hazırdır.</span><span class="sxs-lookup"><span data-stu-id="bc184-154">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc184-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bc184-155">Next steps</span></span>
<span data-ttu-id="bc184-156">Şimdi yeni sanal makineler oluşturmak için Ubuntu Linux sanal sabit diski kullanmak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="bc184-156">You're now ready to use your Ubuntu Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="bc184-157">Adım 2 ve 3'te Azure'a .vhd dosyasını karşıya yüklüyoruz ilk kez kullanıyorsanız bkz [oluşturma ve Linux işletim sistemini içeren bir sanal sabit disk karşıya](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bc184-157">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="bc184-158">Başvurular</span><span class="sxs-lookup"><span data-stu-id="bc184-158">References</span></span>
<span data-ttu-id="bc184-159">Ubuntu donanım etkinleştirme (HWE) Çekirdek:</span><span class="sxs-lookup"><span data-stu-id="bc184-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="bc184-160">http://blog.utlemming.org/2015/01/ubuntu-1404-Azure-images-Now-Tracking.HTML</span><span class="sxs-lookup"><span data-stu-id="bc184-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="bc184-161">http://blog.utlemming.org/2015/02/1204-Azure-cloud-images-Now-using-hwe.HTML</span><span class="sxs-lookup"><span data-stu-id="bc184-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

