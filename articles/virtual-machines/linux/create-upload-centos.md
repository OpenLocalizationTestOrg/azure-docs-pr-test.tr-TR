---
title: "aaaCreate ve Azure CentOS tabanlı Linux VHD'yi karşıya yükle"
description: "Bir Azure sanal sabit CentOS tabanlı Linux işletim sistemi içeren disk (VHD) yüklemek ve toocreate öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 0e518e92-e981-43f4-b12c-9cba1064c4bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 78f36be1d36e3d44cb836c912d143f2c9a72aab5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="6aaa8-103">Azure’da CentOS tabanlı bir sanal makine hazırlama</span><span class="sxs-lookup"><span data-stu-id="6aaa8-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="6aaa8-104">Azure için CentOS 6.x sanal makineyi hazırlama</span><span class="sxs-lookup"><span data-stu-id="6aaa8-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="6aaa8-105">Azure için CentOS 7.0 + sanal makineyi hazırlama</span><span class="sxs-lookup"><span data-stu-id="6aaa8-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="6aaa8-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6aaa8-106">Prerequisites</span></span>
<span data-ttu-id="6aaa8-107">Bu makalede, bir CentOS zaten yüklemiş olduğunuz varsayılmaktadır (veya benzer türevi) Linux işletim sistemi tooa sanal sabit disk.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="6aaa8-108">Birden çok araç toocreate .vhd dosyaları, örneğin bir sanallaştırma çözümü Hyper-V gibi mevcut.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-108">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="6aaa8-109">Yönergeler için bkz: [hello Hyper-V rolünü yükleyin ve sanal makine yapılandırma](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="6aaa8-109">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="6aaa8-110">**CentOS yükleme notları**</span><span class="sxs-lookup"><span data-stu-id="6aaa8-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="6aaa8-111">Ayrıca bkz [genel Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes) Linux Azure için hazırlama hakkında daha fazla ipucu için.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="6aaa8-112">Merhaba VHDX biçimi, Azure'da yalnızca desteklenmiyor **VHD sabit**.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-112">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="6aaa8-113">Hyper-V Yöneticisi'ni kullanarak hello disk tooVHD biçimine Dönüştür veya convert-vhd cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-113">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span> <span data-ttu-id="6aaa8-114">VirtualBox kullanıyorsanız bu seçerek gelir **boyutu sabit** olarak hello disk oluşturulurken dinamik olarak ayrılan toohello varsayılan değil.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-114">If you are using VirtualBox this means selecting **Fixed size** as opposed toohello default dynamically allocated when creating hello disk.</span></span>
* <span data-ttu-id="6aaa8-115">Merhaba Linux sistemi yüklerken olan *önerilen* LVM (genellikle birçok yüklemeleri için hello varsayılan) yerine standart bölümleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-115">When installing hello Linux system it is *recommended* that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="6aaa8-116">Özellikle bir işletim sistemi diski bağlı toobe tooanother hiç gerekiyorsa bu kopyalanan VM'ler LVM adıyla çakışıyor kurtulursunuz sorun giderme için aynı VM.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother identical VM for troubleshooting.</span></span> <span data-ttu-id="6aaa8-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veri diskler üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="6aaa8-118">UDF dosya sistemleri bağlanması için çekirdek desteği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="6aaa8-119">Sağlama yapılandırma Azure hello üzerinde ilk önyükleme sırasında toohello Linux VM ekli toohello Konuk UDF biçimli ortamının geçirilir.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-119">At first boot on Azure hello provisioning configuration is passed toohello Linux VM via UDF-formatted media that is attached toohello guest.</span></span> <span data-ttu-id="6aaa8-120">Hello Azure Linux Aracısı yapılandırmasını mümkün toomount hello UDF dosya sistemi tooread olması gerekir ve hello VM sağlayın.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-120">hello Azure Linux agent must be able toomount hello UDF file system tooread its configuration and provision hello VM.</span></span>
* <span data-ttu-id="6aaa8-121">Linux çekirdek sürümleri 2.6.37 aşağıda NUMA ile büyük VM boyutları üzerinde Hyper-V desteklemez.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="6aaa8-122">Eski dağıtımları hello upstream kullanarak bu sorun öncelikle etkileri Red Hat 2.6.32 çekirdek ve RHEL 6.6 (çekirdek 2.6.32 504) giderilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-122">This issue primarily impacts older distributions using hello upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="6aaa8-123">2.6.32-504 ayarlamalısınız daha özel tekrar 2.6.37 eski veya tekrar eski RHEL tabanlı çalıştıran sistemlerde hello önyükleme parametresinin `numa=off` hello çekirdeğini grub.conf içinde komut satırı.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set hello boot parameter `numa=off` on hello kernel command-line in grub.conf.</span></span> <span data-ttu-id="6aaa8-124">Red Hat daha fazla bilgi için bkz: [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="6aaa8-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="6aaa8-125">Bir takas bölüm hello işletim sistemi disk üzerinde yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-125">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="6aaa8-126">Merhaba Linux Aracısı yapılandırılmış toocreate hello geçici kaynak disk üzerinde bir takas dosyası olabilir.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-126">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="6aaa8-127">Merhaba aşağıdaki adımlarda bu hakkında daha fazla bilgi bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-127">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="6aaa8-128">Tüm hello VHD boyutları 1 MB'ün katları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-128">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="6aaa8-129">CentOS 6.x</span><span class="sxs-lookup"><span data-stu-id="6aaa8-129">CentOS 6.x</span></span>

1. <span data-ttu-id="6aaa8-130">Hyper-V Yöneticisi'nde hello sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-130">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="6aaa8-131">Tıklatın **Bağlan** tooopen hello sanal makine için bir konsol penceresi.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-131">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="6aaa8-132">CentOS 6'hello Azure Linux Aracısı ile NetworkManager etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-132">In CentOS 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="6aaa8-133">Merhaba aşağıdaki komutu çalıştırarak bu paketi kaldırma:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-133">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="6aaa8-134">Oluşturma veya hello dosya düzenleme `/etc/sysconfig/network` ve metin aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-134">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="6aaa8-135">Oluşturma veya hello dosya düzenleme `/etc/sysconfig/network-scripts/ifcfg-eth0` ve metin aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-135">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="6aaa8-136">Udev kuralları tooavoid hello Ethernet arabirimi için statik kuralları oluşturma değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-136">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="6aaa8-137">Bu kurallar, bir sanal makinede Microsoft Azure veya Hyper-V: kopyalarken sorunlara neden olabilir</span><span class="sxs-lookup"><span data-stu-id="6aaa8-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="6aaa8-138">Merhaba ağ hizmetini hello aşağıdaki komutu çalıştırarak önyükleme sırasında başlatacak emin olun:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-138">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="6aaa8-139">Hello Azure veri merkezleri içinde barındırılan toouse hello OpenLogic yansıtmalar isterseniz hello yerine `/etc/yum.repos.d/CentOS-Base.repo` depoları aşağıdaki hello dosyasıyla.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-139">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="6aaa8-140">Bu ayrıca hello ekler **[openlogic]** hello Azure Linux aracısı gibi ek paketler içeren depo:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-140">This will also add hello **[openlogic]** repository that includes additional packages such as hello Azure Linux agent:</span></span>

        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #contrib - packages by Centos Users
        [contrib]
        name=CentOS-$releasever - Contrib
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/contrib/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

    >[!Note]
    <span data-ttu-id="6aaa8-141">Merhaba bu kılavuzun ilerleyen kullanmakta olduğunuz varsayacak en az hello `[openlogic]` kullanılan tooinstall hello Azure Linux aracısı aşağıdaki olacaktır deposu.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-141">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>


9. <span data-ttu-id="6aaa8-142">Satır too/etc/yum.conf aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-142">Add hello following line too/etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="6aaa8-143">Komut tooclear hello geçerli yum meta verileri ve güncelleştirme hello sistemi hello son paketleri ile aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-143">Run hello following command tooclear hello current yum metadata and update hello system with hello latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="6aaa8-144">CentOS daha eski bir sürümü için görüntü oluşturmakta olduğunuz sürece, tüm hello tooupdate toohello son paketleri önerilir:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-144">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="6aaa8-145">Bu komutu çalıştırdıktan sonra bir yeniden başlatma gerekli olabilir.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="6aaa8-146">(İsteğe bağlı) Merhaba Linux Tümleştirme hizmetleri (LIS) için Hello sürücüleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-146">(Optional) Install hello drivers for hello Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="6aaa8-147">Merhaba adım **gerekli** için CentOS 6,3 ve önceki ve sonraki sürümler için isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-147">hello step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="6aaa8-148">Alternatif olarak, üzerinde hello hello el ile yükleme yönergeleri izleyebilir [LIS indirme sayfasına](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello VM üzerine RPM.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-148">Alternatively, you can follow hello manual installation instructions on hello [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM onto your VM.</span></span>
 
12. <span data-ttu-id="6aaa8-149">Hello Azure Linux aracısı ve bağımlılıkları yükleyin:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-149">Install hello Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="6aaa8-150">Bunlar zaten 3. adımda açıklandığı gibi kaldırılmamışsa hello WALinuxAgent paketi hello NetworkManager ve NetworkManager gnome paketleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-150">hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="6aaa8-151">Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-151">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="6aaa8-152">toodo Bu, açık `/boot/grub/menu.lst` bir metin düzenleyicisinde ve o hello varsayılan çekirdek şu parametreler hello içerdiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-152">toodo this, open `/boot/grub/menu.lst` in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="6aaa8-153">Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, tüm konsol iletileri gönderilir sağlayacak sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-153">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="6aaa8-154">Ayrıca toohello yukarıdaki, çok önerilir*kaldırmak* hello şu Parametreler:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-154">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="6aaa8-155">Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-155">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="6aaa8-156">Merhaba `crashkernel` seçeneği olabilir sol isterseniz yapılandırılmış, ancak Not hello küçük VM boyutlarını sorunlu olabilecek bu parametre hello hello VM tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-156">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="6aaa8-157">CentOS 6.5 ve daha önceki hello çekirdek parametresi de ayarlamanız gerekir `numa=off`.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-157">CentOS 6.5 and earlier must also set hello kernel parameter `numa=off`.</span></span> <span data-ttu-id="6aaa8-158">Red Hat bkz [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="6aaa8-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="6aaa8-159">Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-159">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="6aaa8-160">Bu genellikle hello varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-160">This is usually hello default.</span></span>

15. <span data-ttu-id="6aaa8-161">Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-161">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="6aaa8-162">Hello Azure Linux Aracısı otomatik olarak takas alanı ekli toohello VM Azure üzerinde sağladıktan sonra hello yerel kaynak diski kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-162">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="6aaa8-163">Bu hello yerel kaynak diski Not bir *geçici* disk ve hello VM deprovisioned olduğunda boşaltılabilir.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-163">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="6aaa8-164">Yükledikten sonra Azure Linux Aracısı hello (önceki adıma bakın), parametreleri aşağıdaki hello değiştirme `/etc/waagent.conf` uygun şekilde:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-164">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="6aaa8-165">Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-165">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="6aaa8-166">Tıklatın **eylem -> kapatma aşağı** Hyper-V Yöneticisi'nde.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="6aaa8-167">Hazır toobe tooAzure karşıya artık Linux VHD olur.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-167">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="6aaa8-168">CentOS 7.0 +</span><span class="sxs-lookup"><span data-stu-id="6aaa8-168">CentOS 7.0+</span></span>
<span data-ttu-id="6aaa8-169">**CentOS 7 (ve benzer türevleri) değişiklikleri**</span><span class="sxs-lookup"><span data-stu-id="6aaa8-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="6aaa8-170">CentOS 7 sanal makine için Azure hazırlanıyor ancak eşitlenmeyeceği birkaç önemli farklılıklar vardır çok benzer tooCentOS 6, şöyledir:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-170">Preparing a CentOS 7 virtual machine for Azure is very similar tooCentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="6aaa8-171">Merhaba NetworkManager paketi artık hello Azure Linux Aracısı ile çakışıyor.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-171">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="6aaa8-172">Bu paketi varsayılan olarak yüklenir ve onu kaldırılmaz öneririz.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="6aaa8-173">GRUB2 şimdi varsayılan önyükleme yükleyicisi, çekirdek parametreleri düzenlemek için hello yordamı (aşağıya bakın) değişti şekilde hello olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-173">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="6aaa8-174">XFS hello varsayılan dosya sistemi sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-174">XFS is now hello default file system.</span></span> <span data-ttu-id="6aaa8-175">Merhaba ext4 dosya sistemi hala isterseniz kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-175">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="6aaa8-176">**Yapılandırma adımları**</span><span class="sxs-lookup"><span data-stu-id="6aaa8-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="6aaa8-177">Hyper-V Yöneticisi'nde hello sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-177">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="6aaa8-178">Tıklatın **Bağlan** tooopen hello sanal makine için bir konsol penceresi.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-178">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="6aaa8-179">Oluşturma veya hello dosya düzenleme `/etc/sysconfig/network` ve metin aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-179">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="6aaa8-180">Oluşturma veya hello dosya düzenleme `/etc/sysconfig/network-scripts/ifcfg-eth0` ve metin aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-180">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="6aaa8-181">Udev kuralları tooavoid hello Ethernet arabirimi için statik kuralları oluşturma değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-181">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="6aaa8-182">Bu kurallar, bir sanal makinede Microsoft Azure veya Hyper-V: kopyalarken sorunlara neden olabilir</span><span class="sxs-lookup"><span data-stu-id="6aaa8-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="6aaa8-183">Hello Azure veri merkezleri içinde barındırılan toouse hello OpenLogic yansıtmalar isterseniz hello yerine `/etc/yum.repos.d/CentOS-Base.repo` depoları aşağıdaki hello dosyasıyla.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-183">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="6aaa8-184">Bu ayrıca hello ekler **[openlogic]** hello Azure Linux Aracısı paketleri içeren depo:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-184">This will also add hello **[openlogic]** repository that includes packages for hello Azure Linux agent:</span></span>
   
        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    >[!Note]
    <span data-ttu-id="6aaa8-185">Merhaba bu kılavuzun ilerleyen kullanmakta olduğunuz varsayacak en az hello `[openlogic]` kullanılan tooinstall hello Azure Linux aracısı aşağıdaki olacaktır deposu.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-185">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>

7. <span data-ttu-id="6aaa8-186">Aşağıdaki komut tooclear hello geçerli yum meta hello çalıştırın ve tüm güncelleştirmeleri yükleyin:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-186">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="6aaa8-187">CentOS daha eski bir sürümü için görüntü oluşturmakta olduğunuz sürece, tüm hello tooupdate toohello son paketleri önerilir:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-187">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="6aaa8-188">Bir yeniden başlatma belki de bu komutu çalıştırdıktan sonra gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="6aaa8-189">Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-189">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="6aaa8-190">toodo Bu, açık `/etc/default/grub` bir metin düzenleyicisi ve düzenleme hello içinde `GRUB_CMDLINE_LINUX` parametresi, örneğin:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-190">toodo this, open `/etc/default/grub` in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="6aaa8-191">Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, tüm konsol iletileri gönderilir sağlayacak sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-191">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="6aaa8-192">Aynı zamanda NIC için hello yeni CentOS 7 adlandırma kuralları devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-192">It also turns off hello new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="6aaa8-193">Ayrıca toohello yukarıdaki, çok önerilir*kaldırmak* hello şu Parametreler:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-193">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="6aaa8-194">Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-194">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="6aaa8-195">Merhaba `crashkernel` seçeneği olabilir sol isterseniz yapılandırılmış, ancak Not hello küçük VM boyutlarını sorunlu olabilecek bu parametre hello hello VM tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-195">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

9. <span data-ttu-id="6aaa8-196">İşiniz bittiğinde düzenleme `/etc/default/grub` başına yukarıdaki komut toorebuild hello kaz yapılandırması aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-196">Once you are done editing `/etc/default/grub` per above, run hello following command toorebuild hello grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="6aaa8-197">Merhaba görüntüden oluşturuluyorsa **VMWare, VirtualBox veya KVM:** olun hello Hyper-V sürücüleri hello initramfs eklenir:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-197">If building hello image from **VMWare, VirtualBox or KVM:** Ensure hello Hyper-V drivers are included in hello initramfs:</span></span>
   
   <span data-ttu-id="6aaa8-198">Düzen `/etc/dracut.conf`, içeriği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="6aaa8-199">Merhaba initramfs yeniden oluşturun:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-199">Rebuild hello initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="6aaa8-200">Hello Azure Linux aracısı ve bağımlılıkları yükleyin:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-200">Install hello Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="6aaa8-201">Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-201">Do not create swap space on hello OS disk.</span></span>
   
   <span data-ttu-id="6aaa8-202">Hello Azure Linux Aracısı otomatik olarak takas alanı ekli toohello VM Azure üzerinde sağladıktan sonra hello yerel kaynak diski kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-202">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="6aaa8-203">Bu hello yerel kaynak diski Not bir *geçici* disk ve hello VM deprovisioned olduğunda boşaltılabilir.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-203">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="6aaa8-204">Yükledikten sonra Azure Linux Aracısı hello (önceki adıma bakın), parametreleri aşağıdaki hello değiştirme `/etc/waagent.conf` uygun şekilde:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-204">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="6aaa8-205">Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="6aaa8-205">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="6aaa8-206">Tıklatın **eylem -> kapatma aşağı** Hyper-V Yöneticisi'nde.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="6aaa8-207">Hazır toobe tooAzure karşıya artık Linux VHD olur.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-207">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6aaa8-208">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6aaa8-208">Next steps</span></span>
<span data-ttu-id="6aaa8-209">Artık hazır toouse, CentOS Linux sanal sabit disk toocreate yeni sanal makineleri azure'da demektir.</span><span class="sxs-lookup"><span data-stu-id="6aaa8-209">You're now ready toouse your CentOS Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="6aaa8-210">Adım 2 ve 3'te bu hello hello .vhd dosyası tooAzure karşıya yüklüyoruz ilk kez kullanıyorsanız, bkz: [oluşturma ve hello Linux işletim sistemini içeren bir sanal sabit disk karşıya](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6aaa8-210">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

