---
title: "Bir Oracle Linux VHD'yi oluşturup | Microsoft Docs"
description: "Oluşturma ve bir Azure sanal sabit bir Oracle Linux işletim sistemini içeren disk (VHD) yükleme hakkında bilgi edinme."
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
ms.openlocfilehash: c631ddf3acf6df7364c03eb4691b78be0493e0d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="24af1-103">Azure için Oracle Linux sanal makinesi hazırlama</span><span class="sxs-lookup"><span data-stu-id="24af1-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="24af1-104">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="24af1-104">Prerequisites</span></span>
<span data-ttu-id="24af1-105">Bu makalede, bir sanal sabit disk için bir Oracle Linux işletim sistemi zaten yüklediğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="24af1-105">This article assumes that you have already installed an Oracle Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="24af1-106">Birden çok araç, .vhd dosyaları, örneğin bir Hyper-V gibi sanallaştırma çözümü oluşturmak için mevcut.</span><span class="sxs-lookup"><span data-stu-id="24af1-106">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="24af1-107">Yönergeler için bkz: [Hyper-V rolünü yükleyin ve sanal makine yapılandırma](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="24af1-107">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="24af1-108">Oracle Linux yükleme notları</span><span class="sxs-lookup"><span data-stu-id="24af1-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="24af1-109">Ayrıca bkz [genel Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes) Linux Azure için hazırlama hakkında daha fazla ipucu için.</span><span class="sxs-lookup"><span data-stu-id="24af1-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="24af1-110">Oracle'nın Red Hat uyumlu çekirdek ve bunların UEK3 (kesilemeyen kurumsal çekirdek) hem de Hyper-V ve Azure üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="24af1-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="24af1-111">En iyi sonuçlar için lütfen en son çekirdek, Oracle Linux VHD hazırlanırken güncelleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="24af1-111">For best results, please be sure to update to the latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="24af1-112">Gerekli sürücüleri içermez gibi oracle'nın UEK2 Hyper-V ve Azure üzerinde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="24af1-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include the required drivers.</span></span>
* <span data-ttu-id="24af1-113">VHDX biçimi, Azure'da yalnızca desteklenmiyor **VHD sabit**.</span><span class="sxs-lookup"><span data-stu-id="24af1-113">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="24af1-114">Disk Hyper-V Yöneticisi'ni veya convert-vhd cmdlet'ini kullanarak VHD biçimine dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24af1-114">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="24af1-115">Linux sistemini yüklerken LVM (genellikle birçok yüklemeleri için varsayılan) yerine standart bölümlerini kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="24af1-115">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="24af1-116">Özellikle bir işletim sistemi diski şimdiye kadar başka bir VM için sorun giderme için eklenmesi gerekiyorsa, bu kopyalanan VMs LVM ad çakışmalarını önler.</span><span class="sxs-lookup"><span data-stu-id="24af1-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="24af1-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veri disklerde tercih edilen varsa kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="24af1-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="24af1-118">NUMA Linux çekirdek sürümleri 2.6.37 aşağıda bir hata nedeniyle daha büyük VM boyutları için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="24af1-118">NUMA is not supported for larger VM sizes due to a bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="24af1-119">Bu sorun öncelikle Yukarı Akış kullanarak dağıtımları etkiler Red Hat 2.6.32 çekirdek.</span><span class="sxs-lookup"><span data-stu-id="24af1-119">This issue primarily impacts distributions using the upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="24af1-120">Azure Linux Aracısı'nı (waagent) el ile yükleme otomatik olarak NUMA Linux çekirdek kaz yapılandırmasında devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="24af1-120">Manual installation of the Azure Linux agent (waagent) will automatically disable NUMA in the GRUB configuration for the Linux kernel.</span></span> <span data-ttu-id="24af1-121">Aşağıdaki adımlarda bu hakkında daha fazla bilgi bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="24af1-121">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="24af1-122">Bir takas bölüm işletim sistemi disk üzerinde yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="24af1-122">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="24af1-123">Linux Aracısı geçici kaynak disk üzerinde bir takas dosyası oluşturmak için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="24af1-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="24af1-124">Aşağıdaki adımlarda bu hakkında daha fazla bilgi bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="24af1-124">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="24af1-125">Tüm VHD'leri boyutları 1 MB'ün katları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="24af1-125">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="24af1-126">Olduğundan emin olun `Addons` depo etkindir.</span><span class="sxs-lookup"><span data-stu-id="24af1-126">Make sure that the `Addons` repository is enabled.</span></span> <span data-ttu-id="24af1-127">Dosyayı düzenlemek `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) veya `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux), satır değiştirip `enabled=0` için `enabled=1` altında **[ol6_addons]** veya **[ol7_addons]** bu dosyadaki.</span><span class="sxs-lookup"><span data-stu-id="24af1-127">Edit the file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change the line `enabled=0` to `enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="24af1-128">Oracle Linux 6.4 +</span><span class="sxs-lookup"><span data-stu-id="24af1-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="24af1-129">Azure'da çalışması sanal makine için işletim sistemini belirli yapılandırma adımları tamamlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="24af1-129">You must complete specific configuration steps in the operating system for the virtual machine to run in Azure.</span></span>

1. <span data-ttu-id="24af1-130">Hyper-V Yöneticisi'nin Orta bölmede sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="24af1-130">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="24af1-131">Tıklatın **Bağlan** sanal makine için penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="24af1-131">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="24af1-132">Aşağıdaki komutu çalıştırarak NetworkManager kaldırın:</span><span class="sxs-lookup"><span data-stu-id="24af1-132">Uninstall NetworkManager by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="24af1-133">**Not:** paket zaten yüklü değilse, bu komutu bir hata iletisiyle başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="24af1-133">**Note:** If the package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="24af1-134">Bu beklenen bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="24af1-134">This is expected.</span></span>
4. <span data-ttu-id="24af1-135">Adlı bir dosya oluşturun **ağ** içinde `/etc/sysconfig/` aşağıdaki metni içeren dizini:</span><span class="sxs-lookup"><span data-stu-id="24af1-135">Create a file named **network** in the `/etc/sysconfig/` directory that contains the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="24af1-136">Adlı bir dosya oluşturun **ifcfg eth0** içinde `/etc/sysconfig/network-scripts/` aşağıdaki metni içeren dizini:</span><span class="sxs-lookup"><span data-stu-id="24af1-136">Create a file named **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` directory that contains the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="24af1-137">Ethernet arabirimi için statik kuralları oluşturmamak için udev kuralları Değiştir.</span><span class="sxs-lookup"><span data-stu-id="24af1-137">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="24af1-138">Bu kurallar, bir sanal makinede Microsoft Azure veya Hyper-V: kopyalarken sorunlara neden olabilir</span><span class="sxs-lookup"><span data-stu-id="24af1-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="24af1-139">Ağ hizmeti aşağıdaki komutu çalıştırarak önyükleme sırasında başlar emin olun:</span><span class="sxs-lookup"><span data-stu-id="24af1-139">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="24af1-140">Aşağıdaki komutu çalıştırarak Python pyasn1 yükleyin:</span><span class="sxs-lookup"><span data-stu-id="24af1-140">Install python-pyasn1 by running the following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="24af1-141">Azure için ek çekirdek parametreleri içerecek şekilde kaz yapılandırma çekirdek önyükleme satırı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="24af1-141">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="24af1-142">Bu açık yapmak için "/ boot/grub/menu.lst" bir metin düzenleyicisinde ve varsayılan çekirdek aşağıdaki parametreleri içerdiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="24af1-142">To do this open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="24af1-143">Bu tüm konsol iletileri hangi Azure yardımcı olabilecek ilk seri bağlantı noktasına gönderilen sağlayacak sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="24af1-143">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="24af1-144">Bu NUMA Oracle'nın Red Hat uyumlu Çekirdeği'nde bir hata nedeniyle devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="24af1-144">This will disable NUMA due to a bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="24af1-145">Yukarıdakilerin yanı sıra için önerilir *kaldırmak* aşağıdaki parametreleri:</span><span class="sxs-lookup"><span data-stu-id="24af1-145">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="24af1-146">Grafik ve sessiz önyükleme seri bağlantı noktasına gönderilecek tüm günlükleri burada istiyoruz bulut ortamında bulunan kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="24af1-146">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>
   
   <span data-ttu-id="24af1-147">`crashkernel` Seçeneği olabilir sol isterseniz yapılandırılmış, ancak Not küçük VM boyutlarını sorunlu olabilecek bu parametre VM tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır.</span><span class="sxs-lookup"><span data-stu-id="24af1-147">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>
10. <span data-ttu-id="24af1-148">SSH sunucusu yüklü ve önyükleme sırasında başlatılacak şekilde yapılandırılmış olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="24af1-148">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="24af1-149">Bu genellikle varsayılan seçenektir.</span><span class="sxs-lookup"><span data-stu-id="24af1-149">This is usually the default.</span></span>
11. <span data-ttu-id="24af1-150">Aşağıdaki komutu çalıştırarak Azure Linux Aracısı'nı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="24af1-150">Install the Azure Linux Agent by running the following command.</span></span> <span data-ttu-id="24af1-151">En son sürüm 2.0.15 ' dir.</span><span class="sxs-lookup"><span data-stu-id="24af1-151">The latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="24af1-152">WALinuxAgent paketi yükleniyor NetworkManager kaldırır ve bunlar zaten açıklandığı gibi kaldırılmamışsa, NetworkManager gnome paketleri 2. adımda not edin.</span><span class="sxs-lookup"><span data-stu-id="24af1-152">Note that installing the WALinuxAgent package will remove the NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="24af1-153">Takas alanı işletim sistemi disk üzerinde oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="24af1-153">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="24af1-154">Azure Linux Aracısı'nı otomatik olarak takas alanı Azure üzerinde sağladıktan sonra VM'ye bağlı yerel kaynak diski kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24af1-154">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="24af1-155">Yerel kaynak disk Not bir *geçici* disk ve VM sağlaması kaldırılıyor. sağlaması zaman boşaltılabilir.</span><span class="sxs-lookup"><span data-stu-id="24af1-155">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="24af1-156">Azure Linux Aracısı'nı yükledikten sonra (önceki adıma bakın), /etc/waagent.conf aşağıdaki parametrelerinde uygun şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="24af1-156">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
13. <span data-ttu-id="24af1-157">Sanal makine yetkisini kaldırma ve Azure üzerinde sağlamak için hazırlamak için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="24af1-157">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="24af1-158">Tıklatın **eylem -> kapatma aşağı** Hyper-V Yöneticisi'nde.</span><span class="sxs-lookup"><span data-stu-id="24af1-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="24af1-159">Linux VHD Azure'a karşıya yüklenecek artık hazırdır.</span><span class="sxs-lookup"><span data-stu-id="24af1-159">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="24af1-160">Oracle Linux 7.0 +</span><span class="sxs-lookup"><span data-stu-id="24af1-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="24af1-161">**Oracle Linux 7 değişiklikleri**</span><span class="sxs-lookup"><span data-stu-id="24af1-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="24af1-162">Bir Oracle Linux 7 sanal makine için Azure hazırlanıyor çok ancak eşitlenmeyeceği birkaç önemli farklılıklar vardır, Oracle Linux 6 benzer:</span><span class="sxs-lookup"><span data-stu-id="24af1-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar to Oracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="24af1-163">Red Hat uyumlu çekirdek ve Oracle'nın UEK3 Azure üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="24af1-163">Both the Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="24af1-164">UEK3 çekirdek önerilir.</span><span class="sxs-lookup"><span data-stu-id="24af1-164">The UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="24af1-165">NetworkManager paket artık Azure Linux Aracısı ile çakışıyor.</span><span class="sxs-lookup"><span data-stu-id="24af1-165">The NetworkManager package no longer conflicts with the Azure Linux agent.</span></span> <span data-ttu-id="24af1-166">Bu paketi varsayılan olarak yüklenir ve onu kaldırılmaz öneririz.</span><span class="sxs-lookup"><span data-stu-id="24af1-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="24af1-167">Çekirdek parametreleri düzenleme yordamı (aşağıya bakın) değişti biçimde GRUB2 şimdi varsayılan önyükleme yükleyicisi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="24af1-167">GRUB2 is now used as the default bootloader, so the procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="24af1-168">XFS varsayılan dosya sistemi sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="24af1-168">XFS is now the default file system.</span></span> <span data-ttu-id="24af1-169">Ext4 dosya sistemi hala isterseniz kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="24af1-169">The ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="24af1-170">**Yapılandırma adımları**</span><span class="sxs-lookup"><span data-stu-id="24af1-170">**Configuration steps**</span></span>

1. <span data-ttu-id="24af1-171">Hyper-V Yöneticisi'nde sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="24af1-171">In Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="24af1-172">Tıklatın **Bağlan** sanal makine için bir konsol penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="24af1-172">Click **Connect** to open a console window for the virtual machine.</span></span>
3. <span data-ttu-id="24af1-173">Adlı bir dosya oluşturun **ağ** içinde `/etc/sysconfig/` aşağıdaki metni içeren dizini:</span><span class="sxs-lookup"><span data-stu-id="24af1-173">Create a file named **network** in the `/etc/sysconfig/` directory that contains the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="24af1-174">Adlı bir dosya oluşturun **ifcfg eth0** içinde `/etc/sysconfig/network-scripts/` aşağıdaki metni içeren dizini:</span><span class="sxs-lookup"><span data-stu-id="24af1-174">Create a file named **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` directory that contains the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="24af1-175">Ethernet arabirimi için statik kuralları oluşturmamak için udev kuralları Değiştir.</span><span class="sxs-lookup"><span data-stu-id="24af1-175">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="24af1-176">Bu kurallar, bir sanal makinede Microsoft Azure veya Hyper-V: kopyalarken sorunlara neden olabilir</span><span class="sxs-lookup"><span data-stu-id="24af1-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="24af1-177">Ağ hizmeti aşağıdaki komutu çalıştırarak önyükleme sırasında başlar emin olun:</span><span class="sxs-lookup"><span data-stu-id="24af1-177">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="24af1-178">Aşağıdaki komutu çalıştırarak pyasn1 python paketini yükle:</span><span class="sxs-lookup"><span data-stu-id="24af1-178">Install the python-pyasn1 package by running the following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="24af1-179">Geçerli yum meta verileri temizlemek ve tüm güncelleştirmeleri yüklemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="24af1-179">Run the following command to clear the current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="24af1-180">Azure için ek çekirdek parametreleri içerecek şekilde kaz yapılandırma çekirdek önyükleme satırı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="24af1-180">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="24af1-181">Bunu yapmak için Aç "/ etc/varsayılan/kaz" bir metin Düzenleyicisi'ni ve düzenleme `GRUB_CMDLINE_LINUX` parametresi, örneğin:</span><span class="sxs-lookup"><span data-stu-id="24af1-181">To do this open "/etc/default/grub" in a text editor and edit the `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="24af1-182">Bu tüm konsol iletileri hangi Azure yardımcı olabilecek ilk seri bağlantı noktasına gönderilen sağlayacak sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="24af1-182">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="24af1-183">Aynı zamanda NIC için yeni OEL 7 adlandırma kuralları devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="24af1-183">It also turns off the new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="24af1-184">Yukarıdakilerin yanı sıra için önerilir *kaldırmak* aşağıdaki parametreleri:</span><span class="sxs-lookup"><span data-stu-id="24af1-184">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="24af1-185">Grafik ve sessiz önyükleme seri bağlantı noktasına gönderilecek tüm günlükleri burada istiyoruz bulut ortamında bulunan kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="24af1-185">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>
   
   <span data-ttu-id="24af1-186">`crashkernel` Seçeneği olabilir sol isterseniz yapılandırılmış, ancak Not küçük VM boyutlarını sorunlu olabilecek bu parametre VM tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır.</span><span class="sxs-lookup"><span data-stu-id="24af1-186">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>
10. <span data-ttu-id="24af1-187">Tamamladıktan sonra düzenleme "/ etc/varsayılan/kaz" başına, yukarıda kaz yapılandırma yeniden oluşturmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="24af1-187">Once you are done editing "/etc/default/grub" per above, run the following command to rebuild the grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="24af1-188">SSH sunucusu yüklü ve önyükleme sırasında başlatılacak şekilde yapılandırılmış olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="24af1-188">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="24af1-189">Bu genellikle varsayılan seçenektir.</span><span class="sxs-lookup"><span data-stu-id="24af1-189">This is usually the default.</span></span>
12. <span data-ttu-id="24af1-190">Aşağıdaki komutu çalıştırarak Azure Linux Aracısı'nı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="24af1-190">Install the Azure Linux Agent by running the following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="24af1-191">Takas alanı işletim sistemi disk üzerinde oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="24af1-191">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="24af1-192">Azure Linux Aracısı'nı otomatik olarak takas alanı Azure üzerinde sağladıktan sonra VM'ye bağlı yerel kaynak diski kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24af1-192">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="24af1-193">Yerel kaynak disk Not bir *geçici* disk ve VM sağlaması kaldırılıyor. sağlaması zaman boşaltılabilir.</span><span class="sxs-lookup"><span data-stu-id="24af1-193">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="24af1-194">Azure Linux Aracısı'nı yükledikten sonra (önceki adıma bakın), /etc/waagent.conf aşağıdaki parametrelerinde uygun şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="24af1-194">After installing the Azure Linux Agent (see the previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
14. <span data-ttu-id="24af1-195">Sanal makine yetkisini kaldırma ve Azure üzerinde sağlamak için hazırlamak için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="24af1-195">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="24af1-196">Tıklatın **eylem -> kapatma aşağı** Hyper-V Yöneticisi'nde.</span><span class="sxs-lookup"><span data-stu-id="24af1-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="24af1-197">Linux VHD Azure'a karşıya yüklenecek artık hazırdır.</span><span class="sxs-lookup"><span data-stu-id="24af1-197">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24af1-198">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="24af1-198">Next steps</span></span>
<span data-ttu-id="24af1-199">Şimdi yeni sanal makineler oluşturmak için Oracle Linux .vhd kullanmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="24af1-199">You're now ready to use your Oracle Linux .vhd to create new virtual machines in Azure.</span></span> <span data-ttu-id="24af1-200">Adım 2 ve 3'te Azure'a .vhd dosyasını karşıya yüklüyoruz ilk kez kullanıyorsanız bkz [oluşturma ve Linux işletim sistemini içeren bir sanal sabit disk karşıya](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="24af1-200">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

