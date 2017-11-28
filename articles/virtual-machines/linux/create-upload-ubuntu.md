---
title: "aaaCreate ve Azure bir Ubuntu Linux VHD karşıya yükle"
description: "Bir Azure sanal sabit bir Ubuntu Linux işletim sistemini içeren disk (VHD) yüklemek ve toocreate öğrenin."
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
ms.openlocfilehash: cc546a487f769b32432a7e80ddcd0f6af44e201f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="4ba4f-103">Azure’da Ubuntu sanal makinesi hazırlama</span><span class="sxs-lookup"><span data-stu-id="4ba4f-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="4ba4f-104">Resmi Ubuntu bulut görüntüleri</span><span class="sxs-lookup"><span data-stu-id="4ba4f-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="4ba4f-105">Ubuntu şimdi adresten resmi Azure VHD'ler yayımlar [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="4ba4f-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="4ba4f-106">Azure için kendi özel bir Ubuntu yansıma toobuild gereksinim yerine, varsa altındaki hello el ile yordamı kullanın Bu bilinen ile önerilen toostart VHD'ler çalışma ve gerektiği gibi özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-106">If you need toobuild your own specialized Ubuntu image for Azure, rather than use hello manual procedure below it is recommended toostart with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="4ba4f-107">Merhaba son görüntü yayımları her zaman aşağıdaki konumlardan hello bulunabilir:</span><span class="sxs-lookup"><span data-stu-id="4ba4f-107">hello latest image releases can always be found at hello following locations:</span></span>

* <span data-ttu-id="4ba4f-108">Ubuntu 12.04/kesin: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="4ba4f-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="4ba4f-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="4ba4f-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="4ba4f-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="4ba4f-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ba4f-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4ba4f-111">Prerequisites</span></span>
<span data-ttu-id="4ba4f-112">Bu makalede, bir Ubuntu Linux işletim sistemi tooa sanal sabit diski zaten yüklemiş olduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-112">This article assumes that you have already installed an Ubuntu Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="4ba4f-113">Birden çok araç toocreate .vhd dosyaları, örneğin bir sanallaştırma çözümü Hyper-V gibi mevcut.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-113">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="4ba4f-114">Yönergeler için bkz: [hello Hyper-V rolünü yükleyin ve sanal makine yapılandırma](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ba4f-114">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="4ba4f-115">**Ubuntu yükleme notları**</span><span class="sxs-lookup"><span data-stu-id="4ba4f-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="4ba4f-116">Ayrıca bkz [genel Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes) Linux Azure için hazırlama hakkında daha fazla ipucu için.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="4ba4f-117">Merhaba VHDX biçimi, Azure'da yalnızca desteklenmiyor **VHD sabit**.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-117">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="4ba4f-118">Hyper-V Yöneticisi'ni kullanarak hello disk tooVHD biçimine Dönüştür veya convert-vhd cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="4ba4f-119">Merhaba Linux sistemi yüklerken LVM (genellikle birçok yüklemeleri için hello varsayılan) yerine standart bölümlerini kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-119">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="4ba4f-120">Özellikle bir işletim sistemi herhangi bir zamanda ihtiyaçlarını bağlı toobe tooanother VM sorun giderme için disk varsa bu LVM ad çakışmalarını kopyalanan VMs önler.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="4ba4f-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veri disklerde tercih edilen varsa kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="4ba4f-122">Bir takas bölüm hello işletim sistemi disk üzerinde yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="4ba4f-123">Merhaba Linux Aracısı yapılandırılmış toocreate hello geçici kaynak disk üzerinde bir takas dosyası olabilir.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="4ba4f-124">Merhaba aşağıdaki adımlarda bu hakkında daha fazla bilgi bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="4ba4f-125">Tüm hello VHD boyutları 1 MB'ün katları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="4ba4f-126">El ile adımlar</span><span class="sxs-lookup"><span data-stu-id="4ba4f-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="4ba4f-127">Toocreate denemeden önce kendi özel Azure, Ubuntu görüntü Lütfen düşünün hello kullanarak önceden oluşturulmuş ve test görüntülerden [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) yerine.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-127">Before attempting toocreate your own custom Ubuntu image for Azure, please consider using hello pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="4ba4f-128">Merhaba Orta bölmede Hyper-V Yöneticisi'nin hello sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-128">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="4ba4f-129">Tıklatın **Bağlan** tooopen hello penceresinde hello sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-129">Click **Connect** tooopen hello window for hello virtual machine.</span></span>

3. <span data-ttu-id="4ba4f-130">Merhaba geçerli depoları hello görüntü toouse Ubuntu'nın Azure depoları olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-130">Replace hello current repositories in hello image toouse Ubuntu's Azure repos.</span></span> <span data-ttu-id="4ba4f-131">Merhaba adımlar hello Ubuntu sürüm bağlı olarak biraz farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-131">hello steps vary slightly depending on hello Ubuntu version.</span></span>
   
    <span data-ttu-id="4ba4f-132">Düzenleme önce `/etc/apt/sources.list`, bu yedekleme toomake önerilir:</span><span class="sxs-lookup"><span data-stu-id="4ba4f-132">Before editing `/etc/apt/sources.list`, it is recommended toomake a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="4ba4f-133">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="4ba4f-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="4ba4f-134">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="4ba4f-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="4ba4f-135">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="4ba4f-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="4ba4f-136">Merhaba Ubuntu Azure görüntüleri şimdi hello takip *donanım etkinleştirme* (HWE) çekirdek.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-136">hello Ubuntu Azure images are now following hello *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="4ba4f-137">Merhaba işletim sistemi toohello son çekirdek hello aşağıdaki komutları çalıştırarak güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="4ba4f-137">Update hello operating system toohello latest kernel by running hello following commands:</span></span>

    <span data-ttu-id="4ba4f-138">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="4ba4f-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="4ba4f-139">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="4ba4f-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="4ba4f-140">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="4ba4f-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="4ba4f-141">**Ayrıca bkz.:**</span><span class="sxs-lookup"><span data-stu-id="4ba4f-141">**See also:**</span></span>
    - [<span data-ttu-id="4ba4f-142">https://Wiki.ubuntu.com/Kernel/LTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="4ba4f-142">https://wiki.ubuntu.com/Kernel/LTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [<span data-ttu-id="4ba4f-143">https://Wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span><span class="sxs-lookup"><span data-stu-id="4ba4f-143">https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack</span></span>](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="4ba4f-144">Merhaba çekirdek önyükleme satırı kaz tooinclude ek çekirdek parametreler için Azure için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-144">Modify hello kernel boot line for Grub tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="4ba4f-145">Bu açık toodo `/etc/default/grub` adlı hello değişken bir metin düzenleyicisinde Bul `GRUB_CMDLINE_LINUX_DEFAULT` (veya gerekirse ekleyin) ve şu parametreler tooinclude hello düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="4ba4f-145">toodo this open `/etc/default/grub` in a text editor, find hello variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it tooinclude hello following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="4ba4f-146">Kaydet ve bu dosyayı kapatın ve ardından çalıştırın `sudo update-grub`.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-146">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="4ba4f-147">Bu, tüm konsol iletileri hangi sorunları ayıklama Azure teknik destek yardımcı olabilecek toohello ilk seri bağlantı noktası, gönderilen güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-147">This will ensure all console messages are sent toohello first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="4ba4f-148">Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="4ba4f-149">Bu genellikle hello varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-149">This is usually hello default.</span></span>

7. <span data-ttu-id="4ba4f-150">Hello Azure Linux aracısı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="4ba4f-150">Install hello Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="4ba4f-151">Merhaba `walinuxagent` paketi hello kaldırmak `NetworkManager` ve `NetworkManager-gnome` yüklenmişlerse paketler.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-151">hello `walinuxagent` package may remove hello `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="4ba4f-152">Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="4ba4f-152">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="4ba4f-153">Tıklatın **eylem -> kapatma aşağı** Hyper-V Yöneticisi'nde.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-153">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="4ba4f-154">Hazır toobe tooAzure karşıya artık Linux VHD olur.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-154">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ba4f-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4ba4f-155">Next steps</span></span>
<span data-ttu-id="4ba4f-156">Artık hazır toouse Ubuntu Linux sanal sabit disk toocreate yeni sanal makinelerinizi Azure demektir.</span><span class="sxs-lookup"><span data-stu-id="4ba4f-156">You're now ready toouse your Ubuntu Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="4ba4f-157">Adım 2 ve 3'te bu hello hello .vhd dosyası tooAzure karşıya yüklüyoruz ilk kez kullanıyorsanız, bkz: [oluşturma ve hello Linux işletim sistemini içeren bir sanal sabit disk karşıya](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4ba4f-157">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="4ba4f-158">Başvurular</span><span class="sxs-lookup"><span data-stu-id="4ba4f-158">References</span></span>
<span data-ttu-id="4ba4f-159">Ubuntu donanım etkinleştirme (HWE) Çekirdek:</span><span class="sxs-lookup"><span data-stu-id="4ba4f-159">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [<span data-ttu-id="4ba4f-160">http://blog.utlemming.org/2015/01/ubuntu-1404-Azure-images-Now-Tracking.HTML</span><span class="sxs-lookup"><span data-stu-id="4ba4f-160">http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html</span></span>](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [<span data-ttu-id="4ba4f-161">http://blog.utlemming.org/2015/02/1204-Azure-cloud-images-Now-using-hwe.HTML</span><span class="sxs-lookup"><span data-stu-id="4ba4f-161">http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html</span></span>](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

