---
title: "aaaCreate ve Oracle Linux VHD yüklemek | Microsoft Docs"
description: "Bir Azure sanal sabit bir Oracle Linux işletim sistemini içeren disk (VHD) yüklemek ve toocreate öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: dd96f771-26eb-4391-9a89-8c8b6d691822
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: szark
ms.openlocfilehash: be9cf284d7f5e7122a106506a343e53e9f1ac56e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="ffc71-103">Azure için Oracle Linux sanal makinesi hazırlama</span><span class="sxs-lookup"><span data-stu-id="ffc71-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="ffc71-104">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ffc71-104">Prerequisites</span></span>
<span data-ttu-id="ffc71-105">Bu makalede, bir Oracle Linux işletim sistemi tooa sanal sabit diski zaten yüklemiş olduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="ffc71-105">This article assumes that you have already installed an Oracle Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="ffc71-106">Birden çok araç toocreate .vhd dosyaları, örneğin bir sanallaştırma çözümü Hyper-V gibi mevcut.</span><span class="sxs-lookup"><span data-stu-id="ffc71-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="ffc71-107">Yönergeler için bkz: [hello Hyper-V rolünü yükleyin ve sanal makine yapılandırma](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="ffc71-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="ffc71-108">Oracle Linux yükleme notları</span><span class="sxs-lookup"><span data-stu-id="ffc71-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="ffc71-109">Ayrıca bkz [genel Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes) Linux Azure için hazırlama hakkında daha fazla ipucu için.</span><span class="sxs-lookup"><span data-stu-id="ffc71-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="ffc71-110">Oracle'nın Red Hat uyumlu çekirdek ve bunların UEK3 (kesilemeyen kurumsal çekirdek) hem de Hyper-V ve Azure üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="ffc71-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="ffc71-111">En iyi sonuçlar için Oracle Linux VHD hazırlanırken emin tooupdate toohello son çekirdek Lütfen olabilir.</span><span class="sxs-lookup"><span data-stu-id="ffc71-111">For best results, please be sure tooupdate toohello latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="ffc71-112">Merhaba gerekli sürücüleri içermez gibi oracle'nın UEK2 Hyper-V ve Azure üzerinde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="ffc71-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include hello required drivers.</span></span>
* <span data-ttu-id="ffc71-113">Merhaba VHDX biçimi, Azure'da yalnızca desteklenmiyor **VHD sabit**.</span><span class="sxs-lookup"><span data-stu-id="ffc71-113">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="ffc71-114">Hyper-V Yöneticisi'ni kullanarak hello disk tooVHD biçimine Dönüştür veya convert-vhd cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="ffc71-114">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="ffc71-115">Merhaba Linux sistemi yüklerken LVM (genellikle birçok yüklemeleri için hello varsayılan) yerine standart bölümlerini kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="ffc71-115">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="ffc71-116">Özellikle bir işletim sistemi herhangi bir zamanda ihtiyaçlarını bağlı toobe tooanother VM sorun giderme için disk varsa bu LVM ad çakışmalarını kopyalanan VMs önler.</span><span class="sxs-lookup"><span data-stu-id="ffc71-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="ffc71-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veri disklerde tercih edilen varsa kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ffc71-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="ffc71-118">NUMA Linux çekirdeği sürümlerinde 2.6.37 aşağıda tooa hata nedeniyle daha büyük VM boyutları için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="ffc71-118">NUMA is not supported for larger VM sizes due tooa bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="ffc71-119">Bu sorun öncelikle kullanarak dağıtımları hello Yukarı Akış kırmızı etkileri Hat 2.6.32 çekirdek.</span><span class="sxs-lookup"><span data-stu-id="ffc71-119">This issue primarily impacts distributions using hello upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="ffc71-120">Hello Azure Linux Aracısı'nı (waagent) el ile yükleme otomatik olarak NUMA yapılandırmasında hello kaz hello Linux çekirdek devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="ffc71-120">Manual installation of hello Azure Linux agent (waagent) will automatically disable NUMA in hello GRUB configuration for hello Linux kernel.</span></span> <span data-ttu-id="ffc71-121">Merhaba aşağıdaki adımlarda bu hakkında daha fazla bilgi bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="ffc71-121">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="ffc71-122">Bir takas bölüm hello işletim sistemi disk üzerinde yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="ffc71-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="ffc71-123">Merhaba Linux Aracısı yapılandırılmış toocreate hello geçici kaynak disk üzerinde bir takas dosyası olabilir.</span><span class="sxs-lookup"><span data-stu-id="ffc71-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="ffc71-124">Merhaba aşağıdaki adımlarda bu hakkında daha fazla bilgi bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="ffc71-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="ffc71-125">Tüm hello VHD boyutları 1 MB'ün katları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ffc71-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="ffc71-126">Bu hello emin olun `Addons` depo etkindir.</span><span class="sxs-lookup"><span data-stu-id="ffc71-126">Make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="ffc71-127">Merhaba dosyasını düzenleyin `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) veya `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux) hello satır değiştirip `enabled=0` çok`enabled=1` altında **[ol6_addons]** veya **[ol7_addons]** bu dosya.</span><span class="sxs-lookup"><span data-stu-id="ffc71-127">Edit hello file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="ffc71-128">Oracle Linux 6.4 +</span><span class="sxs-lookup"><span data-stu-id="ffc71-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="ffc71-129">Merhaba işletim sistemi azure'da hello sanal makine toorun için belirli yapılandırma adımları tamamlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ffc71-129">You must complete specific configuration steps in hello operating system for hello virtual machine toorun in Azure.</span></span>

1. <span data-ttu-id="ffc71-130">Merhaba Orta bölmede Hyper-V Yöneticisi'nin hello sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="ffc71-130">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="ffc71-131">Tıklatın **Bağlan** tooopen hello penceresinde hello sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="ffc71-131">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="ffc71-132">NetworkManager hello aşağıdaki komutu çalıştırarak kaldırın:</span><span class="sxs-lookup"><span data-stu-id="ffc71-132">Uninstall NetworkManager by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="ffc71-133">**Not:** hello paket zaten yüklü değilse, bu komutu bir hata iletisiyle başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="ffc71-133">**Note:** If hello package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="ffc71-134">Bu beklenen bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="ffc71-134">This is expected.</span></span>
4. <span data-ttu-id="ffc71-135">Adlı bir dosya oluşturun **ağ** hello içinde `/etc/sysconfig/` metin aşağıdaki hello içeren dizini:</span><span class="sxs-lookup"><span data-stu-id="ffc71-135">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="ffc71-136">Adlı bir dosya oluşturun **ifcfg eth0** hello içinde `/etc/sysconfig/network-scripts/` metin aşağıdaki hello içeren dizini:</span><span class="sxs-lookup"><span data-stu-id="ffc71-136">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="ffc71-137">Udev kuralları tooavoid hello Ethernet arabirimi için statik kuralları oluşturma değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ffc71-137">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="ffc71-138">Bu kurallar, bir sanal makinede Microsoft Azure veya Hyper-V: kopyalarken sorunlara neden olabilir</span><span class="sxs-lookup"><span data-stu-id="ffc71-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="ffc71-139">Merhaba ağ hizmetini hello aşağıdaki komutu çalıştırarak önyükleme sırasında başlatacak emin olun:</span><span class="sxs-lookup"><span data-stu-id="ffc71-139">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="ffc71-140">Python pyasn1 hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="ffc71-140">Install python-pyasn1 by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="ffc71-141">Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ffc71-141">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="ffc71-142">Bu açık toodo "/ boot/grub/menu.lst" bir metin düzenleyicisinde ve o hello varsayılan çekirdek şu parametreler hello içerdiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="ffc71-142">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="ffc71-143">Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, tüm konsol iletileri gönderilir sağlayacak sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="ffc71-143">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="ffc71-144">Bu NUMA Oracle'nın Red Hat uyumlu çekirdek tooa hata nedeniyle devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="ffc71-144">This will disable NUMA due tooa bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="ffc71-145">Ayrıca toohello yukarıdaki, çok önerilir*kaldırmak* hello şu Parametreler:</span><span class="sxs-lookup"><span data-stu-id="ffc71-145">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="ffc71-146">Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir.</span><span class="sxs-lookup"><span data-stu-id="ffc71-146">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="ffc71-147">Merhaba `crashkernel` seçeneği olabilir sol isterseniz yapılandırılmış, ancak Not hello küçük VM boyutlarını sorunlu olabilecek bu parametre hello hello VM tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır.</span><span class="sxs-lookup"><span data-stu-id="ffc71-147">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="ffc71-148">Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun.</span><span class="sxs-lookup"><span data-stu-id="ffc71-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="ffc71-149">Bu genellikle hello varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="ffc71-149">This is usually hello default.</span></span>
11. <span data-ttu-id="ffc71-150">Merhaba aşağıdaki komutu çalıştırarak Hello Azure Linux aracısı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ffc71-150">Install hello Azure Linux Agent by running hello following command.</span></span> <span data-ttu-id="ffc71-151">Merhaba en son sürüm 2.0.15 ' dir.</span><span class="sxs-lookup"><span data-stu-id="ffc71-151">hello latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="ffc71-152">Yükleme hello WALinuxAgent paketi hello NetworkManager kaldırır ve bunlar zaten açıklandığı gibi kaldırılmamışsa, NetworkManager gnome paketleri 2. adımda not edin.</span><span class="sxs-lookup"><span data-stu-id="ffc71-152">Note that installing hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="ffc71-153">Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="ffc71-153">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="ffc71-154">Hello Azure Linux Aracısı otomatik olarak takas alanı ekli toohello VM Azure üzerinde sağladıktan sonra hello yerel kaynak diski kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ffc71-154">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="ffc71-155">Bu hello yerel kaynak diski Not bir *geçici* disk ve hello VM deprovisioned olduğunda boşaltılabilir.</span><span class="sxs-lookup"><span data-stu-id="ffc71-155">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="ffc71-156">Yükledikten sonra Azure Linux Aracısı hello (önceki adıma bakın), /etc/waagent.conf parametrelerinde uygun şekilde aşağıdaki hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ffc71-156">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
13. <span data-ttu-id="ffc71-157">Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="ffc71-157">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="ffc71-158">Tıklatın **eylem -> kapatma aşağı** Hyper-V Yöneticisi'nde.</span><span class="sxs-lookup"><span data-stu-id="ffc71-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="ffc71-159">Hazır toobe tooAzure karşıya artık Linux VHD olur.</span><span class="sxs-lookup"><span data-stu-id="ffc71-159">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="ffc71-160">Oracle Linux 7.0 +</span><span class="sxs-lookup"><span data-stu-id="ffc71-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="ffc71-161">**Oracle Linux 7 değişiklikleri**</span><span class="sxs-lookup"><span data-stu-id="ffc71-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="ffc71-162">Bir Oracle Linux 7 sanal makine için Azure hazırlanıyor çok benzer tooOracle Linux 6, ancak eşitlenmeyeceği birkaç önemli farklılıklar vardır şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ffc71-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar tooOracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="ffc71-163">Azure'da hello Red Hat uyumlu çekirdek ve Oracle'nın UEK3 desteklenir.</span><span class="sxs-lookup"><span data-stu-id="ffc71-163">Both hello Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="ffc71-164">Merhaba UEK3 çekirdek önerilir.</span><span class="sxs-lookup"><span data-stu-id="ffc71-164">hello UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="ffc71-165">Merhaba NetworkManager paketi artık hello Azure Linux Aracısı ile çakışıyor.</span><span class="sxs-lookup"><span data-stu-id="ffc71-165">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="ffc71-166">Bu paketi varsayılan olarak yüklenir ve onu kaldırılmaz öneririz.</span><span class="sxs-lookup"><span data-stu-id="ffc71-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="ffc71-167">GRUB2 şimdi varsayılan önyükleme yükleyicisi, çekirdek parametreleri düzenlemek için hello yordamı (aşağıya bakın) değişti şekilde hello olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ffc71-167">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="ffc71-168">XFS hello varsayılan dosya sistemi sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="ffc71-168">XFS is now hello default file system.</span></span> <span data-ttu-id="ffc71-169">Merhaba ext4 dosya sistemi hala isterseniz kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ffc71-169">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="ffc71-170">**Yapılandırma adımları**</span><span class="sxs-lookup"><span data-stu-id="ffc71-170">**Configuration steps**</span></span>

1. <span data-ttu-id="ffc71-171">Hyper-V Yöneticisi'nde hello sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="ffc71-171">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="ffc71-172">Tıklatın **Bağlan** tooopen hello sanal makine için bir konsol penceresi.</span><span class="sxs-lookup"><span data-stu-id="ffc71-172">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="ffc71-173">Adlı bir dosya oluşturun **ağ** hello içinde `/etc/sysconfig/` metin aşağıdaki hello içeren dizini:</span><span class="sxs-lookup"><span data-stu-id="ffc71-173">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="ffc71-174">Adlı bir dosya oluşturun **ifcfg eth0** hello içinde `/etc/sysconfig/network-scripts/` metin aşağıdaki hello içeren dizini:</span><span class="sxs-lookup"><span data-stu-id="ffc71-174">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="ffc71-175">Udev kuralları tooavoid hello Ethernet arabirimi için statik kuralları oluşturma değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ffc71-175">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="ffc71-176">Bu kurallar, bir sanal makinede Microsoft Azure veya Hyper-V: kopyalarken sorunlara neden olabilir</span><span class="sxs-lookup"><span data-stu-id="ffc71-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="ffc71-177">Merhaba ağ hizmetini hello aşağıdaki komutu çalıştırarak önyükleme sırasında başlatacak emin olun:</span><span class="sxs-lookup"><span data-stu-id="ffc71-177">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="ffc71-178">Merhaba aşağıdaki komutu çalıştırarak Hello pyasn1 python paketini yükle:</span><span class="sxs-lookup"><span data-stu-id="ffc71-178">Install hello python-pyasn1 package by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="ffc71-179">Aşağıdaki komut tooclear hello geçerli yum meta hello çalıştırın ve tüm güncelleştirmeleri yükleyin:</span><span class="sxs-lookup"><span data-stu-id="ffc71-179">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="ffc71-180">Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ffc71-180">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="ffc71-181">Bu açık "/ etc/varsayılan/kaz" toodo bir metin düzenleyicisi ve düzenleme hello içinde `GRUB_CMDLINE_LINUX` parametresi, örneğin:</span><span class="sxs-lookup"><span data-stu-id="ffc71-181">toodo this open "/etc/default/grub" in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="ffc71-182">Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, tüm konsol iletileri gönderilir sağlayacak sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="ffc71-182">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="ffc71-183">Aynı zamanda NIC için hello yeni OEL 7 adlandırma kuralları devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="ffc71-183">It also turns off hello new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="ffc71-184">Ayrıca toohello yukarıdaki, çok önerilir*kaldırmak* hello şu Parametreler:</span><span class="sxs-lookup"><span data-stu-id="ffc71-184">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="ffc71-185">Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir.</span><span class="sxs-lookup"><span data-stu-id="ffc71-185">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="ffc71-186">Merhaba `crashkernel` seçeneği olabilir sol isterseniz yapılandırılmış, ancak Not hello küçük VM boyutlarını sorunlu olabilecek bu parametre hello hello VM tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır.</span><span class="sxs-lookup"><span data-stu-id="ffc71-186">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="ffc71-187">Tamamladıktan sonra düzenleme "/ etc/varsayılan/kaz" başına yukarıdaki komut toorebuild hello kaz yapılandırması aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ffc71-187">Once you are done editing "/etc/default/grub" per above, run hello following command toorebuild hello grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="ffc71-188">Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun.</span><span class="sxs-lookup"><span data-stu-id="ffc71-188">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="ffc71-189">Bu genellikle hello varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="ffc71-189">This is usually hello default.</span></span>
12. <span data-ttu-id="ffc71-190">Hello Azure Linux Aracısı hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="ffc71-190">Install hello Azure Linux Agent by running hello following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="ffc71-191">Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="ffc71-191">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="ffc71-192">Hello Azure Linux Aracısı otomatik olarak takas alanı ekli toohello VM Azure üzerinde sağladıktan sonra hello yerel kaynak diski kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ffc71-192">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="ffc71-193">Bu hello yerel kaynak diski Not bir *geçici* disk ve hello VM deprovisioned olduğunda boşaltılabilir.</span><span class="sxs-lookup"><span data-stu-id="ffc71-193">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="ffc71-194">Yükledikten sonra Azure Linux Aracısı hello (Merhaba önceki adıma bakın), /etc/waagent.conf parametrelerinde uygun şekilde aşağıdaki hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ffc71-194">After installing hello Azure Linux Agent (see hello previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. <span data-ttu-id="ffc71-195">Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="ffc71-195">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="ffc71-196">Tıklatın **eylem -> kapatma aşağı** Hyper-V Yöneticisi'nde.</span><span class="sxs-lookup"><span data-stu-id="ffc71-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="ffc71-197">Hazır toobe tooAzure karşıya artık Linux VHD olur.</span><span class="sxs-lookup"><span data-stu-id="ffc71-197">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffc71-198">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ffc71-198">Next steps</span></span>
<span data-ttu-id="ffc71-199">Artık hazır toouse, Oracle Linux .vhd toocreate yeni sanal makineleri azure'da demektir.</span><span class="sxs-lookup"><span data-stu-id="ffc71-199">You're now ready toouse your Oracle Linux .vhd toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="ffc71-200">Adım 2 ve 3'te bu hello hello .vhd dosyası tooAzure karşıya yüklüyoruz ilk kez kullanıyorsanız, bkz: [oluşturma ve hello Linux işletim sistemini içeren bir sanal sabit disk karşıya](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ffc71-200">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

