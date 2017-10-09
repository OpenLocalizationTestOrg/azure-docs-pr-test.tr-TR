---
title: "aaaCreate ve Azure SUSE Linux VHD'yi karşıya yükle"
description: "Bir Azure sanal sabit SUSE Linux işletim sistemi içeren disk (VHD) yüklemek ve toocreate öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 066d01a6-2a54-4718-bcd0-90fe7a5303a1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: szark
ms.openlocfilehash: 9185c7e67279357f00db0f43e944e96c58f0dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a><span data-ttu-id="a2b25-103">Azure için SLES veya openSUSE sanal makinesi hazırlama</span><span class="sxs-lookup"><span data-stu-id="a2b25-103">Prepare a SLES or openSUSE virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="a2b25-104">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a2b25-104">Prerequisites</span></span>
<span data-ttu-id="a2b25-105">Bu makale, zaten bir SUSE ya da Linux işletim sistemi tooa sanal sabit disk openSUSE yüklediğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="a2b25-105">This article assumes that you have already installed a SUSE or openSUSE Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="a2b25-106">Birden çok araç toocreate .vhd dosyaları, örneğin bir sanallaştırma çözümü Hyper-V gibi mevcut.</span><span class="sxs-lookup"><span data-stu-id="a2b25-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="a2b25-107">Yönergeler için bkz: [hello Hyper-V rolünü yükleyin ve sanal makine yapılandırma](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2b25-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="sles--opensuse-installation-notes"></a><span data-ttu-id="a2b25-108">SLES / openSUSE yükleme notları</span><span class="sxs-lookup"><span data-stu-id="a2b25-108">SLES / openSUSE installation notes</span></span>
* <span data-ttu-id="a2b25-109">Ayrıca bkz [genel Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes) Linux Azure için hazırlama hakkında daha fazla ipucu için.</span><span class="sxs-lookup"><span data-stu-id="a2b25-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="a2b25-110">Merhaba VHDX biçimi, Azure'da yalnızca desteklenmiyor **VHD sabit**.</span><span class="sxs-lookup"><span data-stu-id="a2b25-110">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="a2b25-111">Hyper-V Yöneticisi'ni kullanarak hello disk tooVHD biçimine Dönüştür veya convert-vhd cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="a2b25-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="a2b25-112">Merhaba Linux sistemi yüklerken LVM (genellikle birçok yüklemeleri için hello varsayılan) yerine standart bölümlerini kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="a2b25-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="a2b25-113">Özellikle bir işletim sistemi herhangi bir zamanda ihtiyaçlarını bağlı toobe tooanother VM sorun giderme için disk varsa bu LVM ad çakışmalarını kopyalanan VMs önler.</span><span class="sxs-lookup"><span data-stu-id="a2b25-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="a2b25-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veri disklerde tercih edilen varsa kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a2b25-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="a2b25-115">Bir takas bölüm hello işletim sistemi disk üzerinde yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="a2b25-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="a2b25-116">Merhaba Linux Aracısı yapılandırılmış toocreate hello geçici kaynak disk üzerinde bir takas dosyası olabilir.</span><span class="sxs-lookup"><span data-stu-id="a2b25-116">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="a2b25-117">Merhaba aşağıdaki adımlarda bu hakkında daha fazla bilgi bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="a2b25-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="a2b25-118">Tüm hello VHD boyutları 1 MB'ün katları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a2b25-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-suse-studio"></a><span data-ttu-id="a2b25-119">SUSE Studio'yu kullanın</span><span class="sxs-lookup"><span data-stu-id="a2b25-119">Use SUSE Studio</span></span>
<span data-ttu-id="a2b25-120">[SUSE Studio](http://www.susestudio.com) kolayca oluşturabilir ve SLES ve openSUSE görüntülerinizi Azure ve Hyper-V için yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2b25-120">[SUSE Studio](http://www.susestudio.com) can easily create and manage your SLES and openSUSE images for Azure and Hyper-V.</span></span> <span data-ttu-id="a2b25-121">Bu önerilen yaklaşımı kendi SLES ve openSUSE görüntülerini özelleştirme hello olur.</span><span class="sxs-lookup"><span data-stu-id="a2b25-121">This is hello recommended approach for customizing your own SLES and openSUSE images.</span></span>

<span data-ttu-id="a2b25-122">Bir alternatif toobuilding kendi VHD, SUSE de yayımlar BYOS (Getir bilgisayarınızı kendi abonelik) görüntüleri SLES için [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span><span class="sxs-lookup"><span data-stu-id="a2b25-122">As an alternative toobuilding your own VHD, SUSE also publishes BYOS (Bring Your Own Subscription) images for SLES at [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span></span>

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a><span data-ttu-id="a2b25-123">SUSE Linux Enterprise Server 11 SP4 hazırlama</span><span class="sxs-lookup"><span data-stu-id="a2b25-123">Prepare SUSE Linux Enterprise Server 11 SP4</span></span>
1. <span data-ttu-id="a2b25-124">Merhaba Orta bölmede Hyper-V Yöneticisi'nin hello sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="a2b25-124">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="a2b25-125">Tıklatın **Bağlan** tooopen hello penceresinde hello sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="a2b25-125">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="a2b25-126">SUSE Linux Enterprise sistem tooallow kaydetmek, toodownload güncelleştirmeleri ve yükleme paketleri.</span><span class="sxs-lookup"><span data-stu-id="a2b25-126">Register your SUSE Linux Enterprise system tooallow it toodownload updates and install packages.</span></span>
4. <span data-ttu-id="a2b25-127">Merhaba sistem hello en son düzeltme eki ile güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="a2b25-127">Update hello system with hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="a2b25-128">Hello Azure Linux Aracısı hello SLES depodan yükleyin:</span><span class="sxs-lookup"><span data-stu-id="a2b25-128">Install hello Azure Linux Agent from hello SLES repository:</span></span>
   
        # sudo zypper install WALinuxAgent
6. <span data-ttu-id="a2b25-129">İçinde chkconfig waagent çok "açık" ayarlanmış olup olmadığını denetleyin ve aksi durumda, için AutoStart'ı etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="a2b25-129">Check if waagent is set too"on" in chkconfig, and if not, enable it for autostart:</span></span>
   
        # sudo chkconfig waagent on
7. <span data-ttu-id="a2b25-130">Waagent hizmeti çalıştıran ve aksi durumda, başlatın kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="a2b25-130">Check if waagent service is running, and if not, start it:</span></span> 
   
        # sudo service waagent start
8. <span data-ttu-id="a2b25-131">Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a2b25-131">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="a2b25-132">Bu açık toodo "/ boot/grub/menu.lst" bir metin düzenleyicisinde ve o hello varsayılan çekirdek şu parametreler hello içerdiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="a2b25-132">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    <span data-ttu-id="a2b25-133">Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, tüm konsol iletileri gönderilir sağlayacak sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="a2b25-133">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
9. <span data-ttu-id="a2b25-134">Bu /boot/grub/menu.lst ve/etc/fstab hello disk kimliği (kimliğine göre) yerine kendi UUID (UUID tarafından) kullanarak her iki başvuru hello disk onaylayın.</span><span class="sxs-lookup"><span data-stu-id="a2b25-134">Confirm that /boot/grub/menu.lst and /etc/fstab both reference hello disk using its UUID (by-uuid) instead of hello disk ID (by-id).</span></span> 
   
    <span data-ttu-id="a2b25-135">Disk UUID'si Al</span><span class="sxs-lookup"><span data-stu-id="a2b25-135">Get disk UUID</span></span>
   
        # ls /dev/disk/by-uuid/
   
    <span data-ttu-id="a2b25-136">Varsa /dev/disk/by-id / kullanılan, /boot/grub/menu.lst hem/etc/fstab hello UUID tarafından uygun değeri ile güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="a2b25-136">If /dev/disk/by-id/ is used, update both /boot/grub/menu.lst and /etc/fstab with hello proper by-uuid value</span></span>
   
    <span data-ttu-id="a2b25-137">Değişiklikten önce</span><span class="sxs-lookup"><span data-stu-id="a2b25-137">Before change</span></span>
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    <span data-ttu-id="a2b25-138">Değişiklikten sonra</span><span class="sxs-lookup"><span data-stu-id="a2b25-138">After change</span></span>
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. <span data-ttu-id="a2b25-139">Udev kuralları tooavoid hello Ethernet arabirimi için statik kuralları oluşturma değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a2b25-139">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="a2b25-140">Bu kurallar, bir sanal makinede Microsoft Azure veya Hyper-V: kopyalarken sorunlara neden olabilir</span><span class="sxs-lookup"><span data-stu-id="a2b25-140">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. <span data-ttu-id="a2b25-141">Tooedit hello dosya önerilir "/ etc/sysconfig/ağ/dhcp" Merhaba değiştirip `DHCLIENT_SET_HOSTNAME` parametresi toohello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="a2b25-141">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
    
     <span data-ttu-id="a2b25-142">DHCLIENT_SET_HOSTNAME = "Hayır"</span><span class="sxs-lookup"><span data-stu-id="a2b25-142">DHCLIENT_SET_HOSTNAME="no"</span></span>
12. <span data-ttu-id="a2b25-143">"/ Etc/sudoers", çıkışı yorum yapmak veya varsa satırlardan hello kaldırın:</span><span class="sxs-lookup"><span data-stu-id="a2b25-143">In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
    
     <span data-ttu-id="a2b25-144">Varsayılan olarak targetpw # isteyin hello hello hedef kullanıcı yani tüm ALL=(ALL) tüm kök parolasını # uyarı!</span><span class="sxs-lookup"><span data-stu-id="a2b25-144">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="a2b25-145">Yalnızca bu 'Varsayılanları targetpw' ile birlikte kullanın!</span><span class="sxs-lookup"><span data-stu-id="a2b25-145">Only use this together with 'Defaults targetpw'!</span></span>
13. <span data-ttu-id="a2b25-146">Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun.</span><span class="sxs-lookup"><span data-stu-id="a2b25-146">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="a2b25-147">Bu genellikle hello varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="a2b25-147">This is usually hello default.</span></span>
14. <span data-ttu-id="a2b25-148">Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="a2b25-148">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="a2b25-149">Hello Azure Linux Aracısı otomatik olarak takas alanı ekli toohello VM Azure üzerinde sağladıktan sonra hello yerel kaynak diski kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2b25-149">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="a2b25-150">Bu hello yerel kaynak diski Not bir *geçici* disk ve hello VM deprovisioned olduğunda boşaltılabilir.</span><span class="sxs-lookup"><span data-stu-id="a2b25-150">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="a2b25-151">Yükledikten sonra Azure Linux Aracısı hello (önceki adıma bakın), /etc/waagent.conf parametrelerinde uygun şekilde aşağıdaki hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="a2b25-151">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="a2b25-152">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Not: ihtiyacınız onu toobe bu toowhatever ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a2b25-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
15. <span data-ttu-id="a2b25-153">Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="a2b25-153">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="a2b25-154">sudo waagent-force - deprovision</span><span class="sxs-lookup"><span data-stu-id="a2b25-154">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="a2b25-155">HISTSIZE ver = 0</span><span class="sxs-lookup"><span data-stu-id="a2b25-155">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="a2b25-156">oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="a2b25-156">logout</span></span>
16. <span data-ttu-id="a2b25-157">Tıklatın **eylem -> kapatma aşağı** Hyper-V Yöneticisi'nde.</span><span class="sxs-lookup"><span data-stu-id="a2b25-157">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="a2b25-158">Hazır toobe tooAzure karşıya artık Linux VHD olur.</span><span class="sxs-lookup"><span data-stu-id="a2b25-158">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="prepare-opensuse-131"></a><span data-ttu-id="a2b25-159">OpenSUSE 13,1 + hazırlama</span><span class="sxs-lookup"><span data-stu-id="a2b25-159">Prepare openSUSE 13.1+</span></span>
1. <span data-ttu-id="a2b25-160">Merhaba Orta bölmede Hyper-V Yöneticisi'nin hello sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="a2b25-160">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="a2b25-161">Tıklatın **Bağlan** tooopen hello penceresinde hello sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="a2b25-161">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="a2b25-162">Hello kabuğu, hello komutu Çalıştır '`zypper lr`'.</span><span class="sxs-lookup"><span data-stu-id="a2b25-162">On hello shell, run hello command '`zypper lr`'.</span></span> <span data-ttu-id="a2b25-163">Bu komut döndürürse hello depoları beklenen--ayarlama yapılmayan gerekli olarak yapılandırılan sonra aşağıdaki benzer toohello (sürüm numaraları değişebilir unutmayın) çıktı:</span><span class="sxs-lookup"><span data-stu-id="a2b25-163">If this command returns output similar toohello following, then hello repositories are configured as expected--no adjustments are necessary (note that version numbers may vary):</span></span>
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    <span data-ttu-id="a2b25-164">Merhaba komut "depoları tanımlanan..." döndürürse komutları tooadd aşağıdaki hello bu depoları kullanın:</span><span class="sxs-lookup"><span data-stu-id="a2b25-164">If hello command returns "No repositories defined..." then use hello following commands tooadd these repos:</span></span>
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    <span data-ttu-id="a2b25-165">Ardından hello depoları eklendi hello komutunu çalıştırarak doğrulayabilirsiniz '`zypper lr`' yeniden.</span><span class="sxs-lookup"><span data-stu-id="a2b25-165">You can then verify hello repositories have been added by running hello command '`zypper lr`' again.</span></span> <span data-ttu-id="a2b25-166">Merhaba ilgili güncelleştirme depoları birini etkin durumda aşağıdaki komutla etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="a2b25-166">In case one of hello relevant update repositories is not enabled, enable it with following command:</span></span>
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. <span data-ttu-id="a2b25-167">Merhaba çekirdek toohello en son sürüme güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="a2b25-167">Update hello kernel toohello latest available version:</span></span>
   
        # sudo zypper up kernel-default
   
    <span data-ttu-id="a2b25-168">Veya tüm hello en son düzeltme eklerinin tooupdate hello sistemiyle:</span><span class="sxs-lookup"><span data-stu-id="a2b25-168">Or tooupdate hello system with all hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="a2b25-169">Hello Azure Linux aracısı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a2b25-169">Install hello Azure Linux Agent.</span></span>
   
   # <a name="sudo-zypper-install-walinuxagent"></a><span data-ttu-id="a2b25-170">sudo zypper yükleme WALinuxAgent</span><span class="sxs-lookup"><span data-stu-id="a2b25-170">sudo zypper install WALinuxAgent</span></span>
6. <span data-ttu-id="a2b25-171">Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a2b25-171">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="a2b25-172">toodo Bu, Aç "/ boot/grub/menu.lst" bir metin düzenleyicisinde ve o hello varsayılan çekirdek şu parametreler hello içerdiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="a2b25-172">toodo this, open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
     <span data-ttu-id="a2b25-173">Konsol ttyS0 earlyprintk = ttyS0 rootdelay = 300 =</span><span class="sxs-lookup"><span data-stu-id="a2b25-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span></span>
   
   <span data-ttu-id="a2b25-174">Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, tüm konsol iletileri gönderilir sağlayacak sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="a2b25-174">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="a2b25-175">Ayrıca, varsa şu parametreler hello çekirdek önyükleme satırından hello kaldırın:</span><span class="sxs-lookup"><span data-stu-id="a2b25-175">In addition, remove hello following parameters from hello kernel boot line if they exist:</span></span>
   
     <span data-ttu-id="a2b25-176">libata.atapi_enabled=0 ayırma 0x1f0, = 0x8</span><span class="sxs-lookup"><span data-stu-id="a2b25-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span></span>
7. <span data-ttu-id="a2b25-177">Tooedit hello dosya önerilir "/ etc/sysconfig/ağ/dhcp" Merhaba değiştirip `DHCLIENT_SET_HOSTNAME` parametresi toohello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="a2b25-177">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
   
     <span data-ttu-id="a2b25-178">DHCLIENT_SET_HOSTNAME = "Hayır"</span><span class="sxs-lookup"><span data-stu-id="a2b25-178">DHCLIENT_SET_HOSTNAME="no"</span></span>
8. <span data-ttu-id="a2b25-179">**Önemli:** "/ etc/sudoers", çıkışı açıklama veya varsa satırlardan hello kaldırın:</span><span class="sxs-lookup"><span data-stu-id="a2b25-179">**Important:** In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
   
     <span data-ttu-id="a2b25-180">Varsayılan olarak targetpw # isteyin hello hello hedef kullanıcı yani tüm ALL=(ALL) tüm kök parolasını # uyarı!</span><span class="sxs-lookup"><span data-stu-id="a2b25-180">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="a2b25-181">Yalnızca bu 'Varsayılanları targetpw' ile birlikte kullanın!</span><span class="sxs-lookup"><span data-stu-id="a2b25-181">Only use this together with 'Defaults targetpw'!</span></span>
9. <span data-ttu-id="a2b25-182">Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun.</span><span class="sxs-lookup"><span data-stu-id="a2b25-182">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="a2b25-183">Bu genellikle hello varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="a2b25-183">This is usually hello default.</span></span>
10. <span data-ttu-id="a2b25-184">Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="a2b25-184">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="a2b25-185">Hello Azure Linux Aracısı otomatik olarak takas alanı ekli toohello VM Azure üzerinde sağladıktan sonra hello yerel kaynak diski kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2b25-185">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="a2b25-186">Bu hello yerel kaynak diski Not bir *geçici* disk ve hello VM deprovisioned olduğunda boşaltılabilir.</span><span class="sxs-lookup"><span data-stu-id="a2b25-186">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="a2b25-187">Yükledikten sonra Azure Linux Aracısı hello (önceki adıma bakın), /etc/waagent.conf parametrelerinde uygun şekilde aşağıdaki hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="a2b25-187">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="a2b25-188">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Not: ihtiyacınız onu toobe bu toowhatever ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a2b25-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
11. <span data-ttu-id="a2b25-189">Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="a2b25-189">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="a2b25-190">sudo waagent-force - deprovision</span><span class="sxs-lookup"><span data-stu-id="a2b25-190">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="a2b25-191">HISTSIZE ver = 0</span><span class="sxs-lookup"><span data-stu-id="a2b25-191">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="a2b25-192">oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="a2b25-192">logout</span></span>
12. <span data-ttu-id="a2b25-193">Başlangıçta Azure Linux Aracısı çalıştıran hello emin olun:</span><span class="sxs-lookup"><span data-stu-id="a2b25-193">Ensure hello Azure Linux Agent runs at startup:</span></span>
    
        # sudo systemctl enable waagent.service
13. <span data-ttu-id="a2b25-194">Tıklatın **eylem -> kapatma aşağı** Hyper-V Yöneticisi'nde.</span><span class="sxs-lookup"><span data-stu-id="a2b25-194">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="a2b25-195">Hazır toobe tooAzure karşıya artık Linux VHD olur.</span><span class="sxs-lookup"><span data-stu-id="a2b25-195">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2b25-196">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a2b25-196">Next steps</span></span>
<span data-ttu-id="a2b25-197">Artık hazır toouse SUSE Linux sanal sabit disk toocreate yeni sanal makinelerinizi Azure demektir.</span><span class="sxs-lookup"><span data-stu-id="a2b25-197">You're now ready toouse your SUSE Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="a2b25-198">Adım 2 ve 3'te bu hello hello .vhd dosyası tooAzure karşıya yüklüyoruz ilk kez kullanıyorsanız, bkz: [oluşturma ve hello Linux işletim sistemini içeren bir sanal sabit disk karşıya](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a2b25-198">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

