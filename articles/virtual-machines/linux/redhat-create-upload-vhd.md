---
title: "aaaCreate ve Red Hat Enterprise Linux VHD Azure kullanmak için karşıya yükleme | Microsoft Docs"
description: "Bir Azure sanal sabit bir Red Hat Linux işletim sistemi içeren disk (VHD) yüklemek ve toocreate öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 6c6b8f72-32d3-47fa-be94-6cb54537c69f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/28/2017
ms.author: szark
ms.openlocfilehash: bdd1bbfbee55b5cc61d69a09b06b6bd2c3de362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="4de4b-103">Azure için Red Hat tabanlı bir sanal makine hazırlama</span><span class="sxs-lookup"><span data-stu-id="4de4b-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="4de4b-104">Bu makalede, öğreneceksiniz nasıl tooprepare bir Red Hat Enterprise Linux (RHEL) sanal makine için Azure kullanımda.</span><span class="sxs-lookup"><span data-stu-id="4de4b-104">In this article, you will learn how tooprepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="4de4b-105">Bu makalede ele alınan hello sürümleri RHEL, 6.7 + ve 7.1 +.</span><span class="sxs-lookup"><span data-stu-id="4de4b-105">hello versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="4de4b-106">Bu makalede ele alınan hello hiper hazırlık için Hyper-V, çekirdek tabanlı sanal makine (KVM) ve VMware ' dir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-106">hello hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="4de4b-107">Red Hat'ın bulut erişimi programına katılmasını için uygunluk gereksinimleri hakkında daha fazla bilgi için bkz: [Red Hat'ın bulut Access Web sitesinin](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) ve [Azure üzerinde çalışan RHEL](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="4de4b-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="4de4b-108">Red Hat tabanlı sanal makineyi Hyper-V Yöneticisi'nden hazırlama</span><span class="sxs-lookup"><span data-stu-id="4de4b-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4de4b-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4de4b-109">Prerequisites</span></span>
<span data-ttu-id="4de4b-110">Bu bölümde, zaten bir ISO dosyası hello Red Hat Web sitesi ve yüklü hello RHEL görüntü tooa sanal sabit disk (VHD) aldığınız olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="4de4b-110">This section assumes that you have already obtained an ISO file from hello Red Hat website and installed hello RHEL image tooa virtual hard disk (VHD).</span></span> <span data-ttu-id="4de4b-111">Nasıl hakkında daha fazla ayrıntı için toouse Hyper-V Yöneticisi'ni tooinstall bir işletim sistemi görüntüsünü görmek [hello Hyper-V rolünü yükleyin ve sanal makine yapılandırma](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="4de4b-111">For more details about how toouse Hyper-V Manager tooinstall an operating system image, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="4de4b-112">**RHEL yükleme notları**</span><span class="sxs-lookup"><span data-stu-id="4de4b-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="4de4b-113">Azure hello VHDX biçimi desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="4de4b-113">Azure does not support hello VHDX format.</span></span> <span data-ttu-id="4de4b-114">Azure destekler, VHD yalnızca sabit.</span><span class="sxs-lookup"><span data-stu-id="4de4b-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="4de4b-115">Hyper-V Yöneticisi'ni tooconvert hello disk tooVHD biçimini kullanabilirsiniz veya hello convert-vhd cmdlet'ini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4de4b-115">You can use Hyper-V Manager tooconvert hello disk tooVHD format, or you can use hello convert-vhd cmdlet.</span></span> <span data-ttu-id="4de4b-116">VirtualBox kullanıyorsanız seçin **boyutu sabit** hello disk oluşturduğunuzda seçeneği dinamik olarak ayrılan olarak karşılıklı toohello varsayılan.</span><span class="sxs-lookup"><span data-stu-id="4de4b-116">If you use VirtualBox, select **Fixed size** as opposed toohello default dynamically allocated option when you create hello disk.</span></span>
* <span data-ttu-id="4de4b-117">Azure yalnızca 1. nesil sanal makineler destekler.</span><span class="sxs-lookup"><span data-stu-id="4de4b-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="4de4b-118">1. nesil sanal makine VHDX toohello VHD dosyası biçimi ve dinamik olarak genişletilen tooa sabit boyutlu disk dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4de4b-118">You can convert a generation 1 virtual machine from VHDX toohello VHD file format and from dynamically expanding tooa fixed-size disk.</span></span> <span data-ttu-id="4de4b-119">Bir sanal makinenin oluşturma değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="4de4b-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="4de4b-120">Daha fazla bilgi için bkz: [Hyper-V'de 1 veya 2. nesil sanal makine oluşturmalısınız?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span><span class="sxs-lookup"><span data-stu-id="4de4b-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="4de4b-121">VHD hello için izin verilen en büyük boyutu hello 1,023 GB'dir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-121">hello maximum size that's allowed for hello VHD is 1,023 GB.</span></span>
* <span data-ttu-id="4de4b-122">Merhaba Linux işletim sistemi yüklediğinizde, genellikle birçok yüklemeleri için hello varsayılan olduğu mantıksal Birimi Yöneticisi (LVM) yerine standart bölümleri kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="4de4b-122">When you install hello Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often hello default for many installations.</span></span> <span data-ttu-id="4de4b-123">Özellikle erişiminizi tooattach işletim sistemi disk tooanother özdeş bir sanal makine sorun giderme için gerekirse bu yöntem, kopyalanan sanal makineleri LVM adıyla çakışıyor kaçının.</span><span class="sxs-lookup"><span data-stu-id="4de4b-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need tooattach an operating system disk tooanother identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="4de4b-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veri diskler üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="4de4b-125">Evrensel Disk Biçimi (UDF) dosya sistemleri bağlanması için çekirdek desteği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="4de4b-126">Azure, hello UDF biçimli ortamının üzerinde ilk önyükleme sırasında ekli toohello Konuk hello sağlama yapılandırma toohello Linux sanal makine geçirir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-126">At first boot on Azure, hello UDF-formatted media that is attached toohello guest passes hello provisioning configuration toohello Linux virtual machine.</span></span> <span data-ttu-id="4de4b-127">Hello Azure Linux Aracısı hello sanal makine sağlama ve yapılandırmasıyla mümkün toomount hello UDF dosya sistemi tooread olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4de4b-127">hello Azure Linux Agent must be able toomount hello UDF file system tooread its configuration and provision hello virtual machine.</span></span>
* <span data-ttu-id="4de4b-128">Merhaba Linux çekirdek Internet Explorer'ın 2.6.37 önceki sürümlerini Tekdüzen olmayan bellek erişimi (NUMA) üzerinde Hyper-V ile daha büyük sanal makine boyutları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="4de4b-128">Versions of hello Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="4de4b-129">Merhaba upstream kullanan eski dağıtımları Bu sorun öncelikle etkileri Red Hat 2.6.32 çekirdek ve RHEL 6.6 (çekirdek 2.6.32 504) giderilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-129">This issue primarily impacts older distributions that use hello upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="4de4b-130">Özel tekrar çalıştıran sistemleri 2.6.37 eski veya 2.6.32-504 eski olan RHEL tabanlı tekrar hello ayarlamalıdır `numa=off` hello çekirdek komut satırında grub.conf parametresi önyükleme.</span><span class="sxs-lookup"><span data-stu-id="4de4b-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set hello `numa=off` boot parameter on hello kernel command line in grub.conf.</span></span> <span data-ttu-id="4de4b-131">Red Hat daha fazla bilgi için bkz: [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="4de4b-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="4de4b-132">Bir takas bölüm hello işletim sistemi disk üzerinde yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-132">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="4de4b-133">Merhaba Linux Aracısı yapılandırılmış toocreate hello geçici kaynak disk üzerinde bir takas dosyası olabilir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-133">hello Linux Agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="4de4b-134">Aşağıdaki adımları hello bu hakkında daha fazla bilgi bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-134">More information about this can be found in hello following steps.</span></span>
* <span data-ttu-id="4de4b-135">Tüm VHD'leri boyutları 1 MB'ün katları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4de4b-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="4de4b-136">Hyper-V Yöneticisi'nden RHEL 6 sanal makineyi hazırlama</span><span class="sxs-lookup"><span data-stu-id="4de4b-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="4de4b-137">Hyper-V Yöneticisi'nde hello sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="4de4b-137">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="4de4b-138">Tıklatın **Bağlan** tooopen hello sanal makine için bir konsol penceresi.</span><span class="sxs-lookup"><span data-stu-id="4de4b-138">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="4de4b-139">RHEL 6'hello Azure Linux Aracısı ile NetworkManager etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-139">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="4de4b-140">Merhaba aşağıdaki komutu çalıştırarak bu paketi kaldırma:</span><span class="sxs-lookup"><span data-stu-id="4de4b-140">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="4de4b-141">Oluşturma veya düzenleme hello `/etc/sysconfig/network` dosya ve metin aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-141">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="4de4b-142">Oluşturma veya düzenleme hello `/etc/sysconfig/network-scripts/ifcfg-eth0` dosya ve metin aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-142">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="4de4b-143">Merhaba udev kuralları tooavoid hello Ethernet arabirimi için statik kuralları taşıyın (veya kaldırın).</span><span class="sxs-lookup"><span data-stu-id="4de4b-143">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="4de4b-144">Bir sanal makinede Microsoft Azure veya Hyper-V: kopyaladığınızda, bu kurallar sorunlara neden</span><span class="sxs-lookup"><span data-stu-id="4de4b-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="4de4b-145">Merhaba ağ hizmeti önyükleme sırasında hello aşağıdaki komutu çalıştırarak başlayacağını emin olun:</span><span class="sxs-lookup"><span data-stu-id="4de4b-145">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="4de4b-146">Red Hat abonelik tooenable hello yüklemenizin hello RHEL depodan paketler hello aşağıdaki komutu çalıştırarak kaydedin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-146">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="4de4b-147">Merhaba WALinuxAgent paket `WALinuxAgent-<version>`, toohello Red Hat ek özellikler deposu gönderilir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-147">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="4de4b-148">Merhaba ek özellikler depo hello aşağıdaki komutu çalıştırarak etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-148">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="4de4b-149">Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4de4b-149">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="4de4b-150">toodo bu değişiklik, açık `/boot/grub/menu.lst` bir metin düzenleyicisinde ve o hello varsayılan çekirdek şu parametreler hello içerdiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="4de4b-150">toodo this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="4de4b-151">Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, gönderilen tüm konsol iletileri sağlayacak sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="4de4b-151">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="4de4b-152">Ayrıca, şu parametreler hello kaldırmak önerilen:</span><span class="sxs-lookup"><span data-stu-id="4de4b-152">In addition, we recommended that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="4de4b-153">Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-153">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="4de4b-154">Merhaba bırakabilirsiniz `crashkernel` isterseniz yapılandırılmış seçeneği.</span><span class="sxs-lookup"><span data-stu-id="4de4b-154">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="4de4b-155">Bu parametre hello hello sanal makine tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-155">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more.</span></span> <span data-ttu-id="4de4b-156">Bu yapılandırma daha küçük sanal makine boyutlarını sorunlu olabilir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="4de4b-157">RHEL 6.5 ve daha önceki hello de ayarlamanız gerekir `numa=off` çekirdek parametresi.</span><span class="sxs-lookup"><span data-stu-id="4de4b-157">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="4de4b-158">Red Hat bkz [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="4de4b-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="4de4b-159">Bu hello güvenli Kabuk (SSH) sunucusu yüklü ve genellikle hello varsayılandır önyükleme sırasında toostart yapılandırılmış emin olun.</span><span class="sxs-lookup"><span data-stu-id="4de4b-159">Ensure that hello secure shell (SSH) server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="4de4b-160">/Etc/ssh/sshd_config tooinclude hello aşağıdaki satırı değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-160">Modify /etc/ssh/sshd_config tooinclude hello following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="4de4b-161">Hello Azure Linux Aracısı hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-161">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    <span data-ttu-id="4de4b-162">Zaten 3. adımda kaldırılmamışsa, yükleme hello WALinuxAgent paketi hello NetworkManager ve NetworkManager gnome paketleri kaldırır.</span><span class="sxs-lookup"><span data-stu-id="4de4b-162">Installing hello WALinuxAgent package removes hello NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="4de4b-163">Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-163">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="4de4b-164">Hello Azure Linux Aracısı, Azure'da hello sanal makine sağlandıktan sonra ekli toohello sanal makine hello yerel kaynak disk kullanarak takas alanı otomatik olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4de4b-164">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="4de4b-165">Bu hello yerel kaynak disk geçici bir diski olduğundan ve hello sanal makine sağlaması kaldırılıyor. sağlaması zaman, boşaltılabilir olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-165">Note that hello local resource disk is a temporary disk and that it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="4de4b-166">Merhaba önceki adımda hello Azure Linux Aracısı yüklendikten sonra /etc/waagent.conf parametrelerinde uygun şekilde aşağıdaki hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-166">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. <span data-ttu-id="4de4b-167">Merhaba abonelik hello aşağıdaki komutu çalıştırarak (gerekirse) kaydı:</span><span class="sxs-lookup"><span data-stu-id="4de4b-167">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="4de4b-168">Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="4de4b-168">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="4de4b-169">Tıklatın **eylem** > **kapatma** Hyper-V Yöneticisi'nde.</span><span class="sxs-lookup"><span data-stu-id="4de4b-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="4de4b-170">Hazır toobe tooAzure karşıya artık Linux VHD olur.</span><span class="sxs-lookup"><span data-stu-id="4de4b-170">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="4de4b-171">Hyper-V Yöneticisi'nden RHEL 7 sanal makineyi hazırlama</span><span class="sxs-lookup"><span data-stu-id="4de4b-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="4de4b-172">Hyper-V Yöneticisi'nde hello sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="4de4b-172">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="4de4b-173">Tıklatın **Bağlan** tooopen hello sanal makine için bir konsol penceresi.</span><span class="sxs-lookup"><span data-stu-id="4de4b-173">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="4de4b-174">Oluşturma veya düzenleme hello `/etc/sysconfig/network` dosya ve metin aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-174">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="4de4b-175">Oluşturma veya düzenleme hello `/etc/sysconfig/network-scripts/ifcfg-eth0` dosya ve metin aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-175">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="4de4b-176">Merhaba ağ hizmeti önyükleme sırasında hello aşağıdaki komutu çalıştırarak başlayacağını emin olun:</span><span class="sxs-lookup"><span data-stu-id="4de4b-176">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="4de4b-177">Red Hat abonelik tooenable hello yüklemenizin hello RHEL depodan paketler hello aşağıdaki komutu çalıştırarak kaydedin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-177">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="4de4b-178">Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4de4b-178">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="4de4b-179">toodo bu değişiklik, açık `/etc/default/grub` bir metin Düzenleyicisi'ni ve düzenleme hello `GRUB_CMDLINE_LINUX` parametresi.</span><span class="sxs-lookup"><span data-stu-id="4de4b-179">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="4de4b-180">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="4de4b-181">Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, gönderilen tüm konsol iletileri sağlayacak sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="4de4b-181">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="4de4b-182">Bu yapılandırma aynı zamanda NIC için hello yeni RHEL 7 adlandırma kuralları devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="4de4b-182">This configuration also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="4de4b-183">Ayrıca, şu parametreler hello kaldırmanızı öneririz:</span><span class="sxs-lookup"><span data-stu-id="4de4b-183">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="4de4b-184">Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-184">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="4de4b-185">Merhaba bırakabilirsiniz `crashkernel` isterseniz yapılandırılmış seçeneği.</span><span class="sxs-lookup"><span data-stu-id="4de4b-185">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="4de4b-186">Bu parametre, daha küçük sanal makine boyutlarını sorunlu olabilir hello hello sanal makine tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-186">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="4de4b-187">Tamamlandıktan sonra düzenleme `/etc/default/grub`çalıştırın hello komut toorebuild hello kaz yapılandırması aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="4de4b-187">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="4de4b-188">Bu hello SSH sunucusu yüklü ve genellikle hello varsayılandır önyükleme sırasında toostart yapılandırılmış emin olun.</span><span class="sxs-lookup"><span data-stu-id="4de4b-188">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="4de4b-189">Değiştirme `/etc/ssh/sshd_config` satır aşağıdaki tooinclude hello:</span><span class="sxs-lookup"><span data-stu-id="4de4b-189">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="4de4b-190">Merhaba WALinuxAgent paket `WALinuxAgent-<version>`, toohello Red Hat ek özellikler deposu gönderilir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-190">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="4de4b-191">Merhaba ek özellikler depo hello aşağıdaki komutu çalıştırarak etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-191">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="4de4b-192">Hello Azure Linux Aracısı hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-192">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="4de4b-193">Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-193">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="4de4b-194">Hello Azure Linux Aracısı, Azure'da hello sanal makine sağlandıktan sonra ekli toohello sanal makine hello yerel kaynak disk kullanarak takas alanı otomatik olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4de4b-194">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="4de4b-195">Merhaba yerel kaynak disk bir geçici diski olduğundan ve hello sanal makine deprovisioned olduğunda boşaltılabilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-195">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="4de4b-196">Parametreleri aşağıdaki hello hello önceki adımda hello Azure Linux Aracısı yüklendikten sonra değiştirmek `/etc/waagent.conf` uygun şekilde:</span><span class="sxs-lookup"><span data-stu-id="4de4b-196">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="4de4b-197">Toounregister hello abonelik hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4de4b-197">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="4de4b-198">Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="4de4b-198">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="4de4b-199">Tıklatın **eylem** > **kapatma** Hyper-V Yöneticisi'nde.</span><span class="sxs-lookup"><span data-stu-id="4de4b-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="4de4b-200">Hazır toobe tooAzure karşıya artık Linux VHD olur.</span><span class="sxs-lookup"><span data-stu-id="4de4b-200">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="4de4b-201">Red Hat tabanlı sanal makineyi KVM hazırlama</span><span class="sxs-lookup"><span data-stu-id="4de4b-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="4de4b-202">KVM RHEL 6 sanal makineyi hazırlama</span><span class="sxs-lookup"><span data-stu-id="4de4b-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="4de4b-203">Merhaba KVM RHEL 6 görüntüsü hello Red Hat Web sitesinden indirin.</span><span class="sxs-lookup"><span data-stu-id="4de4b-203">Download hello KVM image of RHEL 6 from hello Red Hat website.</span></span>

2. <span data-ttu-id="4de4b-204">Bir kök parola ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-204">Set a root password.</span></span>

    <span data-ttu-id="4de4b-205">Şifrelenmiş bir parola oluşturmak ve hello hello komutunun çıktısını kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="4de4b-205">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="4de4b-206">Guestfish olan bir kök parola ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="4de4b-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="4de4b-207">Değişiklik hello ikinci alanı hello kök kullanıcıdan "!!"</span><span class="sxs-lookup"><span data-stu-id="4de4b-207">Change hello second field of hello root user from "!!"</span></span> <span data-ttu-id="4de4b-208">toohello şifrelenmiş parola.</span><span class="sxs-lookup"><span data-stu-id="4de4b-208">toohello encrypted password.</span></span>

3. <span data-ttu-id="4de4b-209">Bir sanal makine içinde KVM hello qcow2 görüntüden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4de4b-209">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="4de4b-210">Merhaba disk türü çok ayarlamak**qcow2**, hello sanal ağ arabirimi cihaz modeli çok belirlendiği**virtio**.</span><span class="sxs-lookup"><span data-stu-id="4de4b-210">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="4de4b-211">Ardından, hello sanal makineyi başlatmak ve kök olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-211">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="4de4b-212">Oluşturma veya düzenleme hello `/etc/sysconfig/network` dosya ve metin aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-212">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="4de4b-213">Oluşturma veya düzenleme hello `/etc/sysconfig/network-scripts/ifcfg-eth0` dosya ve metin aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-213">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="4de4b-214">Merhaba udev kuralları tooavoid hello Ethernet arabirimi için statik kuralları taşıyın (veya kaldırın).</span><span class="sxs-lookup"><span data-stu-id="4de4b-214">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="4de4b-215">Bir sanal makinede Azure veya Hyper-V: kopyaladığınızda, bu kurallar sorunlara neden</span><span class="sxs-lookup"><span data-stu-id="4de4b-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="4de4b-216">Merhaba ağ hizmeti önyükleme sırasında hello aşağıdaki komutu çalıştırarak başlayacağını emin olun:</span><span class="sxs-lookup"><span data-stu-id="4de4b-216">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="4de4b-217">Red Hat abonelik tooenable hello yüklemenizin hello RHEL depodan paketler hello aşağıdaki komutu çalıştırarak kaydedin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-217">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="4de4b-218">Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4de4b-218">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="4de4b-219">toodo bu yapılandırma, açık `/boot/grub/menu.lst` bir metin düzenleyicisinde ve o hello varsayılan çekirdek şu parametreler hello içerdiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="4de4b-219">toodo this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="4de4b-220">Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, gönderilen tüm konsol iletileri sağlayacak sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="4de4b-220">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="4de4b-221">Ayrıca, şu parametreler hello kaldırmanızı öneririz:</span><span class="sxs-lookup"><span data-stu-id="4de4b-221">In addition, we recommend that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="4de4b-222">Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-222">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="4de4b-223">Merhaba bırakabilirsiniz `crashkernel` isterseniz yapılandırılmış seçeneği.</span><span class="sxs-lookup"><span data-stu-id="4de4b-223">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="4de4b-224">Bu parametre, daha küçük sanal makine boyutlarını sorunlu olabilir hello hello sanal makine tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-224">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="4de4b-225">RHEL 6.5 ve daha önceki hello de ayarlamanız gerekir `numa=off` çekirdek parametresi.</span><span class="sxs-lookup"><span data-stu-id="4de4b-225">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="4de4b-226">Red Hat bkz [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="4de4b-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="4de4b-227">Hyper-V modüllerini tooinitramfs ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-227">Add Hyper-V modules tooinitramfs:</span></span>  

    <span data-ttu-id="4de4b-228">Düzen `/etc/dracut.conf`ve içeriği aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-228">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="4de4b-229">İnitramfs yeniden oluşturun:</span><span class="sxs-lookup"><span data-stu-id="4de4b-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="4de4b-230">Bulut init kaldırın:</span><span class="sxs-lookup"><span data-stu-id="4de4b-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="4de4b-231">Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun:</span><span class="sxs-lookup"><span data-stu-id="4de4b-231">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="4de4b-232">Satırlardan /etc/ssh/sshd_config tooinclude hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-232">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="4de4b-233">Merhaba WALinuxAgent paket `WALinuxAgent-<version>`, toohello Red Hat ek özellikler deposu gönderilir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-233">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="4de4b-234">Merhaba ek özellikler depo hello aşağıdaki komutu çalıştırarak etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-234">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="4de4b-235">Hello Azure Linux Aracısı hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-235">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="4de4b-236">Hello Azure Linux Aracısı, Azure'da hello sanal makine sağlandıktan sonra ekli toohello sanal makine hello yerel kaynak disk kullanarak takas alanı otomatik olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4de4b-236">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="4de4b-237">Merhaba yerel kaynak disk bir geçici diski olduğundan ve hello sanal makine deprovisioned olduğunda boşaltılabilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-237">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="4de4b-238">Parametreleri aşağıdaki hello hello önceki adımda hello Azure Linux Aracısı yüklendikten sonra değiştirmek **/etc/waagent.conf** uygun şekilde:</span><span class="sxs-lookup"><span data-stu-id="4de4b-238">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="4de4b-239">Merhaba abonelik hello aşağıdaki komutu çalıştırarak (gerekirse) kaydı:</span><span class="sxs-lookup"><span data-stu-id="4de4b-239">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="4de4b-240">Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="4de4b-240">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="4de4b-241">KVM hello sanal makineyi kapatın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-241">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="4de4b-242">Merhaba qcow2 görüntü toohello VHD biçimine dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="4de4b-242">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="4de4b-243">İlk hello görüntü tooraw biçimine dönüştürün:</span><span class="sxs-lookup"><span data-stu-id="4de4b-243">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="4de4b-244">Merhaba ham görüntü Hello boyutu 1 MB ile hizalanır emin olun.</span><span class="sxs-lookup"><span data-stu-id="4de4b-244">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="4de4b-245">Aksi takdirde 1 MB ile Merhaba boyutu tooalign yukarı yuvarlar:</span><span class="sxs-lookup"><span data-stu-id="4de4b-245">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="4de4b-246">Merhaba ham disk tooa Dönüştür sabit boyutlu VHD:</span><span class="sxs-lookup"><span data-stu-id="4de4b-246">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="4de4b-247">KVM RHEL 7 sanal makineyi hazırlama</span><span class="sxs-lookup"><span data-stu-id="4de4b-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="4de4b-248">Merhaba KVM RHEL 7 görüntüsü hello Red Hat Web sitesinden indirin.</span><span class="sxs-lookup"><span data-stu-id="4de4b-248">Download hello KVM image of RHEL 7 from hello Red Hat website.</span></span> <span data-ttu-id="4de4b-249">Bu yordamda RHEL 7 hello örnek olarak kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="4de4b-249">This procedure uses RHEL 7 as hello example.</span></span>

2. <span data-ttu-id="4de4b-250">Bir kök parola ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-250">Set a root password.</span></span>

    <span data-ttu-id="4de4b-251">Şifrelenmiş bir parola oluşturmak ve hello hello komutunun çıktısını kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="4de4b-251">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="4de4b-252">Guestfish olan bir kök parola ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="4de4b-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="4de4b-253">Değişiklik hello ikinci alanı kök kullanıcıdan "!!"</span><span class="sxs-lookup"><span data-stu-id="4de4b-253">Change hello second field of root user from "!!"</span></span> <span data-ttu-id="4de4b-254">toohello şifrelenmiş parola.</span><span class="sxs-lookup"><span data-stu-id="4de4b-254">toohello encrypted password.</span></span>

3. <span data-ttu-id="4de4b-255">Bir sanal makine içinde KVM hello qcow2 görüntüden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4de4b-255">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="4de4b-256">Merhaba disk türü çok ayarlamak**qcow2**, hello sanal ağ arabirimi cihaz modeli çok belirlendiği**virtio**.</span><span class="sxs-lookup"><span data-stu-id="4de4b-256">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="4de4b-257">Ardından, hello sanal makineyi başlatmak ve kök olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-257">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="4de4b-258">Oluşturma veya düzenleme hello `/etc/sysconfig/network` dosya ve metin aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-258">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="4de4b-259">Oluşturma veya düzenleme hello `/etc/sysconfig/network-scripts/ifcfg-eth0` dosya ve metin aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-259">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="4de4b-260">Merhaba ağ hizmeti önyükleme sırasında hello aşağıdaki komutu çalıştırarak başlayacağını emin olun:</span><span class="sxs-lookup"><span data-stu-id="4de4b-260">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="4de4b-261">Red Hat abonelik tooenable yüklemenizin hello RHEL depodan paketler hello aşağıdaki komutu çalıştırarak kaydedin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-261">Register your Red Hat subscription tooenable installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="4de4b-262">Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4de4b-262">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="4de4b-263">toodo bu yapılandırma, açık `/etc/default/grub` bir metin Düzenleyicisi'ni ve düzenleme hello `GRUB_CMDLINE_LINUX` parametresi.</span><span class="sxs-lookup"><span data-stu-id="4de4b-263">toodo this configuration, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="4de4b-264">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="4de4b-265">Bu komut, aynı zamanda, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, gönderilen tüm konsol iletileri sağlar sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="4de4b-265">This command also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="4de4b-266">Merhaba komut ayrıca NIC'ler için hello yeni RHEL 7 adlandırma kuralları devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="4de4b-266">hello command also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="4de4b-267">Ayrıca, şu parametreler hello kaldırmanızı öneririz:</span><span class="sxs-lookup"><span data-stu-id="4de4b-267">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="4de4b-268">Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-268">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="4de4b-269">Merhaba bırakabilirsiniz `crashkernel` isterseniz yapılandırılmış seçeneği.</span><span class="sxs-lookup"><span data-stu-id="4de4b-269">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="4de4b-270">Bu parametre, daha küçük sanal makine boyutlarını sorunlu olabilir hello hello sanal makine tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-270">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="4de4b-271">Tamamlandıktan sonra düzenleme `/etc/default/grub`çalıştırın hello komut toorebuild hello kaz yapılandırması aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="4de4b-271">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="4de4b-272">Hyper-V modüllerini initramfs ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4de4b-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="4de4b-273">Düzenleme `/etc/dracut.conf` ve içeriği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="4de4b-274">İnitramfs yeniden oluşturun:</span><span class="sxs-lookup"><span data-stu-id="4de4b-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="4de4b-275">Bulut init kaldırın:</span><span class="sxs-lookup"><span data-stu-id="4de4b-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="4de4b-276">Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun:</span><span class="sxs-lookup"><span data-stu-id="4de4b-276">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="4de4b-277">Satırlardan /etc/ssh/sshd_config tooinclude hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-277">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="4de4b-278">Merhaba WALinuxAgent paket `WALinuxAgent-<version>`, toohello Red Hat ek özellikler deposu gönderilir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-278">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="4de4b-279">Merhaba ek özellikler depo hello aşağıdaki komutu çalıştırarak etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-279">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="4de4b-280">Hello Azure Linux Aracısı hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-280">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="4de4b-281">Merhaba waagent hizmetini etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-281">Enable hello waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="4de4b-282">Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-282">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="4de4b-283">Hello Azure Linux Aracısı, Azure'da hello sanal makine sağlandıktan sonra ekli toohello sanal makine hello yerel kaynak disk kullanarak takas alanı otomatik olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4de4b-283">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="4de4b-284">Merhaba yerel kaynak disk bir geçici diski olduğundan ve hello sanal makine deprovisioned olduğunda boşaltılabilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-284">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="4de4b-285">Parametreleri aşağıdaki hello hello önceki adımda hello Azure Linux Aracısı yüklendikten sonra değiştirmek `/etc/waagent.conf` uygun şekilde:</span><span class="sxs-lookup"><span data-stu-id="4de4b-285">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="4de4b-286">Merhaba abonelik hello aşağıdaki komutu çalıştırarak (gerekirse) kaydı:</span><span class="sxs-lookup"><span data-stu-id="4de4b-286">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="4de4b-287">Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="4de4b-287">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="4de4b-288">KVM hello sanal makineyi kapatın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-288">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="4de4b-289">Merhaba qcow2 görüntü toohello VHD biçimine dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="4de4b-289">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="4de4b-290">İlk hello görüntü tooraw biçimine dönüştürün:</span><span class="sxs-lookup"><span data-stu-id="4de4b-290">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="4de4b-291">Merhaba ham görüntü Hello boyutu 1 MB ile hizalanır emin olun.</span><span class="sxs-lookup"><span data-stu-id="4de4b-291">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="4de4b-292">Aksi takdirde 1 MB ile Merhaba boyutu tooalign yukarı yuvarlar:</span><span class="sxs-lookup"><span data-stu-id="4de4b-292">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="4de4b-293">Merhaba ham disk tooa Dönüştür sabit boyutlu VHD:</span><span class="sxs-lookup"><span data-stu-id="4de4b-293">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="4de4b-294">VMware Red Hat tabanlı sanal makineyi hazırlama</span><span class="sxs-lookup"><span data-stu-id="4de4b-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="4de4b-295">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4de4b-295">Prerequisites</span></span>
<span data-ttu-id="4de4b-296">Bu bölümde VMware RHEL sanal makine zaten yüklediğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="4de4b-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="4de4b-297">Tooinstall VMware, işletim sistemini nasıl görürüm hakkında ayrıntılar için [VMware konuk işletim sistemi Yükleme Kılavuzu](http://partnerweb.vmware.com/GOSIG/home.html).</span><span class="sxs-lookup"><span data-stu-id="4de4b-297">For details about how tooinstall an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="4de4b-298">Merhaba Linux işletim sistemi yüklediğinizde, birçok yüklemeleri için hello varsayılan olduğu çoğunlukla LVM, yerine standart bölümleri kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="4de4b-298">When you install hello Linux operating system, we recommend that you use standard partitions rather than LVM, which is often hello default for many installations.</span></span> <span data-ttu-id="4de4b-299">Özellikle bir işletim sistemi diski herhangi bir zamanda bağlı toobe tooanother sanal makine sorun giderme için gerekiyorsa bu kopyalanan sanal makinenin LVM adıyla çakışıyor önler.</span><span class="sxs-lookup"><span data-stu-id="4de4b-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs toobe attached tooanother virtual machine for troubleshooting.</span></span> <span data-ttu-id="4de4b-300">LVM veya RAID veri disklerde tercih edilen varsa kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="4de4b-301">Bir takas bölüm hello işletim sistemi disk üzerinde yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-301">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="4de4b-302">Merhaba Linux Aracısı toocreate hello geçici kaynak disk üzerinde bir takas dosyası yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4de4b-302">You can configure hello Linux agent toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="4de4b-303">İzleyin hello adımlarda bu hakkında daha fazla bilgi bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4de4b-303">You can find more information about this in hello steps that follow.</span></span>
* <span data-ttu-id="4de4b-304">Merhaba sanal sabit disk oluşturduğunuzda, seçin **depolama sanal diski tek bir dosya olarak**.</span><span class="sxs-lookup"><span data-stu-id="4de4b-304">When you create hello virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="4de4b-305">VMware RHEL 6 sanal makineyi hazırlama</span><span class="sxs-lookup"><span data-stu-id="4de4b-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="4de4b-306">RHEL 6'hello Azure Linux Aracısı ile NetworkManager etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-306">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="4de4b-307">Merhaba aşağıdaki komutu çalıştırarak bu paketi kaldırma:</span><span class="sxs-lookup"><span data-stu-id="4de4b-307">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="4de4b-308">Adlı bir dosya oluşturun **ağ** metin aşağıdaki içeren hello/etc/sysconfig/dizininde hello:</span><span class="sxs-lookup"><span data-stu-id="4de4b-308">Create a file named **network** in hello /etc/sysconfig/ directory that contains hello following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="4de4b-309">Oluşturma veya düzenleme hello `/etc/sysconfig/network-scripts/ifcfg-eth0` dosya ve metin aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-309">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="4de4b-310">Merhaba udev kuralları tooavoid hello Ethernet arabirimi için statik kuralları taşıyın (veya kaldırın).</span><span class="sxs-lookup"><span data-stu-id="4de4b-310">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="4de4b-311">Bir sanal makinede Azure veya Hyper-V: kopyaladığınızda, bu kurallar sorunlara neden</span><span class="sxs-lookup"><span data-stu-id="4de4b-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="4de4b-312">Merhaba ağ hizmeti önyükleme sırasında hello aşağıdaki komutu çalıştırarak başlayacağını emin olun:</span><span class="sxs-lookup"><span data-stu-id="4de4b-312">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="4de4b-313">Red Hat abonelik tooenable hello yüklemenizin hello RHEL depodan paketler hello aşağıdaki komutu çalıştırarak kaydedin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-313">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="4de4b-314">Merhaba WALinuxAgent paket `WALinuxAgent-<version>`, toohello Red Hat ek özellikler deposu gönderilir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-314">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="4de4b-315">Merhaba ek özellikler depo hello aşağıdaki komutu çalıştırarak etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-315">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="4de4b-316">Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4de4b-316">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="4de4b-317">toodo Bu, açık `/etc/default/grub` bir metin Düzenleyicisi'ni ve düzenleme hello `GRUB_CMDLINE_LINUX` parametresi.</span><span class="sxs-lookup"><span data-stu-id="4de4b-317">toodo this, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="4de4b-318">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   <span data-ttu-id="4de4b-319">Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, gönderilen tüm konsol iletileri sağlayacak sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="4de4b-319">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="4de4b-320">Ayrıca, şu parametreler hello kaldırmanızı öneririz:</span><span class="sxs-lookup"><span data-stu-id="4de4b-320">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="4de4b-321">Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-321">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="4de4b-322">Merhaba bırakabilirsiniz `crashkernel` isterseniz yapılandırılmış seçeneği.</span><span class="sxs-lookup"><span data-stu-id="4de4b-322">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="4de4b-323">Bu parametre, daha küçük sanal makine boyutlarını sorunlu olabilir hello hello sanal makine tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-323">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="4de4b-324">Hyper-V modüllerini tooinitramfs ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-324">Add Hyper-V modules tooinitramfs:</span></span>

    <span data-ttu-id="4de4b-325">Düzen `/etc/dracut.conf`ve içeriği aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-325">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="4de4b-326">İnitramfs yeniden oluşturun:</span><span class="sxs-lookup"><span data-stu-id="4de4b-326">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="4de4b-327">Bu hello SSH sunucusu yüklü ve genellikle hello varsayılandır önyükleme sırasında toostart yapılandırılmış emin olun.</span><span class="sxs-lookup"><span data-stu-id="4de4b-327">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="4de4b-328">Değiştirme `/etc/ssh/sshd_config` satır aşağıdaki tooinclude hello:</span><span class="sxs-lookup"><span data-stu-id="4de4b-328">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

    <span data-ttu-id="4de4b-329">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="4de4b-329">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="4de4b-330">Hello Azure Linux Aracısı hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-330">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="4de4b-331">Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-331">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="4de4b-332">Hello Azure Linux Aracısı, Azure'da hello sanal makine sağlandıktan sonra ekli toohello sanal makine hello yerel kaynak disk kullanarak takas alanı otomatik olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4de4b-332">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="4de4b-333">Merhaba yerel kaynak disk bir geçici diski olduğundan ve hello sanal makine deprovisioned olduğunda boşaltılabilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-333">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="4de4b-334">Parametreleri aşağıdaki hello hello önceki adımda hello Azure Linux Aracısı yüklendikten sonra değiştirmek `/etc/waagent.conf` uygun şekilde:</span><span class="sxs-lookup"><span data-stu-id="4de4b-334">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="4de4b-335">Merhaba abonelik hello aşağıdaki komutu çalıştırarak (gerekirse) kaydı:</span><span class="sxs-lookup"><span data-stu-id="4de4b-335">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="4de4b-336">Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="4de4b-336">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="4de4b-337">Merhaba sanal makineyi kapatın ve hello VMDK tooa .vhd dosyası dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="4de4b-337">Shut down hello virtual machine, and convert hello VMDK file tooa .vhd file.</span></span>

    <span data-ttu-id="4de4b-338">İlk hello görüntü tooraw biçimine dönüştürün:</span><span class="sxs-lookup"><span data-stu-id="4de4b-338">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="4de4b-339">Merhaba ham görüntü Hello boyutu 1 MB ile hizalanır emin olun.</span><span class="sxs-lookup"><span data-stu-id="4de4b-339">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="4de4b-340">Aksi takdirde 1 MB ile Merhaba boyutu tooalign yukarı yuvarlar:</span><span class="sxs-lookup"><span data-stu-id="4de4b-340">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="4de4b-341">Merhaba ham disk tooa Dönüştür sabit boyutlu VHD:</span><span class="sxs-lookup"><span data-stu-id="4de4b-341">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="4de4b-342">VMware RHEL 7 sanal makineyi hazırlama</span><span class="sxs-lookup"><span data-stu-id="4de4b-342">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="4de4b-343">Oluşturma veya düzenleme hello `/etc/sysconfig/network` dosya ve metin aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-343">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="4de4b-344">Oluşturma veya düzenleme hello `/etc/sysconfig/network-scripts/ifcfg-eth0` dosya ve metin aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-344">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="4de4b-345">Merhaba ağ hizmeti önyükleme sırasında hello aşağıdaki komutu çalıştırarak başlayacağını emin olun:</span><span class="sxs-lookup"><span data-stu-id="4de4b-345">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="4de4b-346">Red Hat abonelik tooenable hello yüklemenizin hello RHEL depodan paketler hello aşağıdaki komutu çalıştırarak kaydedin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-346">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="4de4b-347">Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4de4b-347">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="4de4b-348">toodo bu değişiklik, açık `/etc/default/grub` bir metin Düzenleyicisi'ni ve düzenleme hello `GRUB_CMDLINE_LINUX` parametresi.</span><span class="sxs-lookup"><span data-stu-id="4de4b-348">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="4de4b-349">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-349">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="4de4b-350">Bu yapılandırma, aynı zamanda, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, gönderilen tüm konsol iletileri sağlar sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="4de4b-350">This configuration also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="4de4b-351">Aynı zamanda NIC için hello yeni RHEL 7 adlandırma kuralları devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="4de4b-351">It also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="4de4b-352">Ayrıca, şu parametreler hello kaldırmanızı öneririz:</span><span class="sxs-lookup"><span data-stu-id="4de4b-352">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="4de4b-353">Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-353">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="4de4b-354">Merhaba bırakabilirsiniz `crashkernel` isterseniz yapılandırılmış seçeneği.</span><span class="sxs-lookup"><span data-stu-id="4de4b-354">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="4de4b-355">Bu parametre, daha küçük sanal makine boyutlarını sorunlu olabilir hello hello sanal makine tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-355">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="4de4b-356">Tamamlandıktan sonra düzenleme `/etc/default/grub`çalıştırın hello komut toorebuild hello kaz yapılandırması aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="4de4b-356">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="4de4b-357">Hyper-V modüllerini tooinitramfs ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4de4b-357">Add Hyper-V modules tooinitramfs.</span></span>

    <span data-ttu-id="4de4b-358">Düzen `/etc/dracut.conf`, içeriği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-358">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="4de4b-359">İnitramfs yeniden oluşturun:</span><span class="sxs-lookup"><span data-stu-id="4de4b-359">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="4de4b-360">Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun.</span><span class="sxs-lookup"><span data-stu-id="4de4b-360">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="4de4b-361">Bu ayar genellikle hello varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="4de4b-361">This setting is usually hello default.</span></span> <span data-ttu-id="4de4b-362">Değiştirme `/etc/ssh/sshd_config` satır aşağıdaki tooinclude hello:</span><span class="sxs-lookup"><span data-stu-id="4de4b-362">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="4de4b-363">Merhaba WALinuxAgent paket `WALinuxAgent-<version>`, toohello Red Hat ek özellikler deposu gönderilir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-363">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="4de4b-364">Merhaba ek özellikler depo hello aşağıdaki komutu çalıştırarak etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-364">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="4de4b-365">Hello Azure Linux Aracısı hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-365">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="4de4b-366">Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-366">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="4de4b-367">Hello Azure Linux Aracısı, Azure'da hello sanal makine sağlandıktan sonra ekli toohello sanal makine hello yerel kaynak disk kullanarak takas alanı otomatik olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4de4b-367">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="4de4b-368">Merhaba yerel kaynak disk bir geçici diski olduğundan ve hello sanal makine deprovisioned olduğunda boşaltılabilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-368">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="4de4b-369">Parametreleri aşağıdaki hello hello önceki adımda hello Azure Linux Aracısı yüklendikten sonra değiştirmek `/etc/waagent.conf` uygun şekilde:</span><span class="sxs-lookup"><span data-stu-id="4de4b-369">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. <span data-ttu-id="4de4b-370">Toounregister hello abonelik hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4de4b-370">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="4de4b-371">Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="4de4b-371">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="4de4b-372">Merhaba sanal makineyi kapatın ve hello VMDK dosya toohello VHD biçimine dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="4de4b-372">Shut down hello virtual machine, and convert hello VMDK file toohello VHD format.</span></span>

    <span data-ttu-id="4de4b-373">İlk hello görüntü tooraw biçimine dönüştürün:</span><span class="sxs-lookup"><span data-stu-id="4de4b-373">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="4de4b-374">Merhaba ham görüntü Hello boyutu 1 MB ile hizalanır emin olun.</span><span class="sxs-lookup"><span data-stu-id="4de4b-374">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="4de4b-375">Aksi takdirde 1 MB ile Merhaba boyutu tooalign yukarı yuvarlar:</span><span class="sxs-lookup"><span data-stu-id="4de4b-375">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="4de4b-376">Merhaba ham disk tooa Dönüştür sabit boyutlu VHD:</span><span class="sxs-lookup"><span data-stu-id="4de4b-376">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="4de4b-377">Red Hat tabanlı sanal makineyi kickstart dosyası otomatik olarak kullanarak bir ISO hazırlama</span><span class="sxs-lookup"><span data-stu-id="4de4b-377">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="4de4b-378">Bir kickstart dosyasından RHEL 7 sanal makineyi hazırlama</span><span class="sxs-lookup"><span data-stu-id="4de4b-378">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="4de4b-379">İçeriği aşağıdaki hello içeren bir kickstart dosyası oluşturun ve hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4de4b-379">Create a kickstart file that includes hello following content, and save hello file.</span></span> <span data-ttu-id="4de4b-380">Merhaba kickstart yükleme hakkında daha fazla bilgi için bkz [Kickstart Yükleme Kılavuzu'na](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span><span class="sxs-lookup"><span data-stu-id="4de4b-380">For details about kickstart installation, see hello [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run hello Setup Agent on first boot
        firstboot --disable

        # Keyboard layouts
        keyboard --vckeymap=us --xlayouts='us'

        # System language
        lang en_US.UTF-8

        # Network information
        network  --bootproto=dhcp

        # Root password
        rootpw --plaintext "to_be_disabled"

        # System services
        services --enabled="sshd,waagent,NetworkManager"

        # System timezone
        timezone Etc/UTC --isUtc --ntpservers 0.rhel.pool.ntp.org,1.rhel.pool.ntp.org,2.rhel.pool.ntp.org,3.rhel.pool.ntp.org

        # Partition clearing information
        clearpart --all --initlabel

        # Clear hello MBR
        zerombr

        # Disk partitioning information
        part /boot --fstype="xfs" --size=500
        part / --fstyp="xfs" --size=1 --grow --asprimary

        # System bootloader configuration
        bootloader --location=mbr

        # Firewall configuration
        firewall --disabled

        # Enable SELinux
        selinux --enforcing

        # Don't configure X
        skipx

        # Power down hello machine after install
        poweroff

        %packages
        @base
        @console-internet
        chrony
        sudo
        parted
        -dracut-config-rescue

        %end

        %post --log=/var/log/anaconda/post-install.log

        #!/bin/bash

        # Register Red Hat Subscription
        subscription-manager register --username=XXX --password=XXX --auto-attach --force

        # Install latest repo update
        yum update -y

        # Enable extras repo
        subscription-manager repos --enable=rhel-7-server-extras-rpms

        # Install WALinuxAgent
        yum install -y WALinuxAgent

        # Unregister Red Hat subscription
        subscription-manager unregister

        # Enable waaagent at boot-up
        systemctl enable waagent

        # Disable hello root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set hello cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build hello grub cfg
        grub2-mkconfig -o /boot/grub2/grub.cfg

        # Configure network
        cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no
        EOF

        # Deprovision and prepare for Azure
        waagent -force -deprovision

        %end

2. <span data-ttu-id="4de4b-381">Burada hello yükleme sistem erişebildiğinizi hello kickstart dosyasını yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="4de4b-381">Place hello kickstart file where hello installation system can access it.</span></span>

3. <span data-ttu-id="4de4b-382">Hyper-V Yöneticisi'nde yeni bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4de4b-382">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="4de4b-383">Merhaba üzerinde **sanal Hard diske Bağlan** sayfasında, **bir sanal sabit diski sonra Ekle**ve tam hello yeni sanal makine Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="4de4b-383">On hello **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete hello New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="4de4b-384">Merhaba sanal makine ayarlarını açın:</span><span class="sxs-lookup"><span data-stu-id="4de4b-384">Open hello virtual machine settings:</span></span>

    <span data-ttu-id="4de4b-385">a.</span><span class="sxs-lookup"><span data-stu-id="4de4b-385">a.</span></span>  <span data-ttu-id="4de4b-386">Yeni bir sanal sabit disk toohello sanal makine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4de4b-386">Attach a new virtual hard disk toohello virtual machine.</span></span> <span data-ttu-id="4de4b-387">Emin tooselect olun **VHD biçimi** ve **sabit boyutlu**.</span><span class="sxs-lookup"><span data-stu-id="4de4b-387">Make sure tooselect **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="4de4b-388">b.</span><span class="sxs-lookup"><span data-stu-id="4de4b-388">b.</span></span>  <span data-ttu-id="4de4b-389">Merhaba yükleme ISO toohello DVD sürücüsü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4de4b-389">Attach hello installation ISO toohello DVD drive.</span></span>

    <span data-ttu-id="4de4b-390">c.</span><span class="sxs-lookup"><span data-stu-id="4de4b-390">c.</span></span>  <span data-ttu-id="4de4b-391">Merhaba BIOS tooboot CD'den ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-391">Set hello BIOS tooboot from CD.</span></span>

5. <span data-ttu-id="4de4b-392">Merhaba sanal makineyi başlatın.</span><span class="sxs-lookup"><span data-stu-id="4de4b-392">Start hello virtual machine.</span></span> <span data-ttu-id="4de4b-393">Merhaba Yükleme Kılavuzu'na göründüğünde, basın **sekmesini** tooconfigure hello önyükleme seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="4de4b-393">When hello installation guide appears, press **Tab** tooconfigure hello boot options.</span></span>

6. <span data-ttu-id="4de4b-394">ENTER `inst.ks=<hello location of hello kickstart file>` sonunda hello hello önyükleme seçenekleri ve tuşuna **Enter**.</span><span class="sxs-lookup"><span data-stu-id="4de4b-394">Enter `inst.ks=<hello location of hello kickstart file>` at hello end of hello boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="4de4b-395">Merhaba yükleme toofinish bekleyin.</span><span class="sxs-lookup"><span data-stu-id="4de4b-395">Wait for hello installation toofinish.</span></span> <span data-ttu-id="4de4b-396">Tamamlandığında, hello sanal makine otomatik olarak kapatılacak.</span><span class="sxs-lookup"><span data-stu-id="4de4b-396">When it's finished, hello virtual machine will be shut down automatically.</span></span> <span data-ttu-id="4de4b-397">Hazır toobe tooAzure karşıya artık Linux VHD olur.</span><span class="sxs-lookup"><span data-stu-id="4de4b-397">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="4de4b-398">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="4de4b-398">Known issues</span></span>
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="4de4b-399">Merhaba Hyper-V sürücü hello başlangıç RAM diski bir Hyper-V olmayan hiper kullanırken eklenemedi</span><span class="sxs-lookup"><span data-stu-id="4de4b-399">hello Hyper-V driver could not be included in hello initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="4de4b-400">Bir Hyper-V ortamında çalıştığını Linux algılar sürece bazı durumlarda, Linux yükleyicileri hello sürücüleri için Hyper-V hello başlangıç RAM disk (initrd veya initramfs) içermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-400">In some cases, Linux installers might not include hello drivers for Hyper-V in hello initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="4de4b-401">Farklı sanallaştırma sistem (diğer bir deyişle, Virtualbox, Xen, vb.) tooprepare Linux görüntünüzü kullanırken hv_storvsc çekirdek modülleri hello başlangıç RAM disk üzerindeki kullanılabilir ve en az hv_vmbus hello toorebuild initrd tooensure gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-401">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) tooprepare your Linux image, you might need toorebuild initrd tooensure that at least hello hv_vmbus and hv_storvsc kernel modules are available on hello initial RAM disk.</span></span> <span data-ttu-id="4de4b-402">Bilinen bir sorun en az hello Yukarı Akış Red Hat dağıtım noktasında tabanlı sistemlerde budur.</span><span class="sxs-lookup"><span data-stu-id="4de4b-402">This is a known issue at least on systems that are based on hello upstream Red Hat distribution.</span></span>

<span data-ttu-id="4de4b-403">tooresolve Bu sorun, Hyper-V modüllerini tooinitramfs ekleyin ve onu yeniden oluşturun:</span><span class="sxs-lookup"><span data-stu-id="4de4b-403">tooresolve this issue, add Hyper-V modules tooinitramfs and rebuild it:</span></span>

<span data-ttu-id="4de4b-404">Düzen `/etc/dracut.conf`ve içeriği aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4de4b-404">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="4de4b-405">İnitramfs yeniden oluşturun:</span><span class="sxs-lookup"><span data-stu-id="4de4b-405">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="4de4b-406">Daha fazla ayrıntı için hello bilgi [initramfs yeniden](https://access.redhat.com/solutions/1958).</span><span class="sxs-lookup"><span data-stu-id="4de4b-406">For more details, see hello information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4de4b-407">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4de4b-407">Next steps</span></span>
<span data-ttu-id="4de4b-408">Red Hat Enterprise Linux sanal sabit disk toocreate yeni sanal makinelerinizi Azure şimdi hazır toouse demektir.</span><span class="sxs-lookup"><span data-stu-id="4de4b-408">You're now ready toouse your Red Hat Enterprise Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="4de4b-409">Adım 2 ve 3'te bu hello hello .vhd dosyası tooAzure karşıya yüklüyoruz ilk kez kullanıyorsanız, bkz: [oluşturma ve hello Linux işletim sistemini içeren bir sanal sabit disk karşıya](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4de4b-409">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="4de4b-410">Red Hat Enterprise Linux toorun olan hello hiper hakkında daha fazla ayrıntı sertifikalı için bkz: [hello Red Hat Web sitesi](https://access.redhat.com/certified-hypervisors).</span><span class="sxs-lookup"><span data-stu-id="4de4b-410">For more details about hello hypervisors that are certified toorun Red Hat Enterprise Linux, see [hello Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
