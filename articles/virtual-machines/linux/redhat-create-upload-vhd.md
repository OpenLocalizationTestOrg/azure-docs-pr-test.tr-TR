---
title: "Red Hat Enterprise Linux VHD kullanılmak üzere Azure oluşturup | Microsoft Docs"
description: "Oluşturma ve bir Azure sanal sabit bir Red Hat Linux işletim sistemi içeren disk (VHD) yükleme hakkında bilgi edinme."
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
ms.openlocfilehash: b753c76b8c3d789c681d7fbff6aa07590b860be5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="78724-103">Azure için Red Hat tabanlı bir sanal makine hazırlama</span><span class="sxs-lookup"><span data-stu-id="78724-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="78724-104">Bu makalede, Azure kullanmak için Red Hat Enterprise Linux (RHEL) sanal makineyi hazırlama öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="78724-104">In this article, you will learn how to prepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="78724-105">Bu makalede ele alınan RHEL sürümleri 6.7 + ve 7.1 +.</span><span class="sxs-lookup"><span data-stu-id="78724-105">The versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="78724-106">Bu makalede ele alınan hiper hazırlık için Hyper-V, çekirdek tabanlı sanal makine (KVM) ve VMware ' dir.</span><span class="sxs-lookup"><span data-stu-id="78724-106">The hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="78724-107">Red Hat'ın bulut erişimi programına katılmasını için uygunluk gereksinimleri hakkında daha fazla bilgi için bkz: [Red Hat'ın bulut Access Web sitesinin](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) ve [Azure üzerinde çalışan RHEL](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="78724-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="78724-108">Red Hat tabanlı sanal makineyi Hyper-V Yöneticisi'nden hazırlama</span><span class="sxs-lookup"><span data-stu-id="78724-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="78724-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="78724-109">Prerequisites</span></span>
<span data-ttu-id="78724-110">Bu bölümde, zaten bir ISO dosyası Red Hat Web sitesinden aldığınız ve RHEL görüntü sanal sabit diske (VHD) yüklü olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="78724-110">This section assumes that you have already obtained an ISO file from the Red Hat website and installed the RHEL image to a virtual hard disk (VHD).</span></span> <span data-ttu-id="78724-111">Bir işletim sistemi görüntüsünü yüklemek için Hyper-V Yöneticisi'ni kullanma hakkında daha fazla ayrıntı için bkz: [Hyper-V rolünü yükleyin ve sanal makine yapılandırma](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="78724-111">For more details about how to use Hyper-V Manager to install an operating system image, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="78724-112">**RHEL yükleme notları**</span><span class="sxs-lookup"><span data-stu-id="78724-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="78724-113">Azure VHDX biçimi desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="78724-113">Azure does not support the VHDX format.</span></span> <span data-ttu-id="78724-114">Azure destekler, VHD yalnızca sabit.</span><span class="sxs-lookup"><span data-stu-id="78724-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="78724-115">Disk VHD biçimine dönüştürmek için Hyper-V Yöneticisi'ni kullanabilirsiniz veya convert-vhd cmdlet'ini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78724-115">You can use Hyper-V Manager to convert the disk to VHD format, or you can use the convert-vhd cmdlet.</span></span> <span data-ttu-id="78724-116">VirtualBox kullanıyorsanız seçin **boyutu sabit** disk oluşturduğunuzda seçeneği dinamik olarak ayrılan varsayılan aksine.</span><span class="sxs-lookup"><span data-stu-id="78724-116">If you use VirtualBox, select **Fixed size** as opposed to the default dynamically allocated option when you create the disk.</span></span>
* <span data-ttu-id="78724-117">Azure yalnızca 1. nesil sanal makineler destekler.</span><span class="sxs-lookup"><span data-stu-id="78724-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="78724-118">1. nesil sanal makine VHD dosya biçimine VHDX ve dinamik olarak genişletilen bir sabit boyutlu disk dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78724-118">You can convert a generation 1 virtual machine from VHDX to the VHD file format and from dynamically expanding to a fixed-size disk.</span></span> <span data-ttu-id="78724-119">Bir sanal makinenin oluşturma değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="78724-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="78724-120">Daha fazla bilgi için bkz: [Hyper-V'de 1 veya 2. nesil sanal makine oluşturmalısınız?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span><span class="sxs-lookup"><span data-stu-id="78724-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="78724-121">VHD için izin verilen en büyük boyutu 1,023 GB'dir.</span><span class="sxs-lookup"><span data-stu-id="78724-121">The maximum size that's allowed for the VHD is 1,023 GB.</span></span>
* <span data-ttu-id="78724-122">Linux işletim sistemi yüklediğinizde, genellikle birçok yüklemeleri için varsayılan olduğu mantıksal Birimi Yöneticisi (LVM) yerine standart bölümleri kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="78724-122">When you install the Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often the default for many installations.</span></span> <span data-ttu-id="78724-123">Özellikle herhangi bir işletim sistemi diski başka bir özdeş sanal sorun giderme için makine ekleme gerekirse bu yöntem, kopyalanan sanal makineleri LVM adıyla çakışıyor kaçının.</span><span class="sxs-lookup"><span data-stu-id="78724-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need to attach an operating system disk to another identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="78724-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veri diskler üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="78724-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="78724-125">Evrensel Disk Biçimi (UDF) dosya sistemleri bağlanması için çekirdek desteği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="78724-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="78724-126">Azure üzerinde ilk önyükleme sırasında Konuk bağlı UDF biçimli medya sağlama yapılandırma Linux sanal makineye iletir.</span><span class="sxs-lookup"><span data-stu-id="78724-126">At first boot on Azure, the UDF-formatted media that is attached to the guest passes the provisioning configuration to the Linux virtual machine.</span></span> <span data-ttu-id="78724-127">Azure Linux Aracısı'nı yapılandırmasını okumak ve sanal makine sağlamak için UDF dosya sistemi bağlama kurabilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="78724-127">The Azure Linux Agent must be able to mount the UDF file system to read its configuration and provision the virtual machine.</span></span>
* <span data-ttu-id="78724-128">Linux çekirdek Internet Explorer'ın 2.6.37 önceki sürümlerini Tekdüzen olmayan bellek erişimi (NUMA) üzerinde Hyper-V ile daha büyük sanal makine boyutları desteklemez.</span><span class="sxs-lookup"><span data-stu-id="78724-128">Versions of the Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="78724-129">Yukarı Akış kullanan eski dağıtımları Bu sorun öncelikle etkileri Red Hat 2.6.32 çekirdek ve RHEL 6.6 (çekirdek 2.6.32 504) giderilmiştir.</span><span class="sxs-lookup"><span data-stu-id="78724-129">This issue primarily impacts older distributions that use the upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="78724-130">Özel tekrar çalıştıran sistemleri 2.6.37 eski veya 2.6.32-504 eski olan RHEL tabanlı tekrar ayarlamalıdır `numa=off` grub.conf çekirdek komut satırında parametre önyükleme.</span><span class="sxs-lookup"><span data-stu-id="78724-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set the `numa=off` boot parameter on the kernel command line in grub.conf.</span></span> <span data-ttu-id="78724-131">Red Hat daha fazla bilgi için bkz: [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="78724-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="78724-132">Bir takas bölüm işletim sistemi disk üzerinde yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-132">Do not configure a swap partition on the operating system disk.</span></span> <span data-ttu-id="78724-133">Linux Aracısı geçici kaynak disk üzerinde bir takas dosyası oluşturmak için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="78724-133">The Linux Agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="78724-134">Aşağıdaki adımlarda bu hakkında daha fazla bilgi bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="78724-134">More information about this can be found in the following steps.</span></span>
* <span data-ttu-id="78724-135">Tüm VHD'leri boyutları 1 MB'ün katları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="78724-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="78724-136">Hyper-V Yöneticisi'nden RHEL 6 sanal makineyi hazırlama</span><span class="sxs-lookup"><span data-stu-id="78724-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="78724-137">Hyper-V Yöneticisi'nde sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="78724-137">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="78724-138">Tıklatın **Bağlan** sanal makine için bir konsol penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="78724-138">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="78724-139">RHEL 6'da, Azure Linux Aracısı ile NetworkManager etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="78724-139">In RHEL 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="78724-140">Bu paket, aşağıdaki komutu çalıştırarak kaldırın:</span><span class="sxs-lookup"><span data-stu-id="78724-140">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="78724-141">Oluşturma veya düzenleme `/etc/sysconfig/network` dosyasını bulun ve aşağıdaki metni ekleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-141">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="78724-142">Oluşturma veya düzenleme `/etc/sysconfig/network-scripts/ifcfg-eth0` dosyasını bulun ve aşağıdaki metni ekleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-142">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="78724-143">Ethernet arabirimi için statik kuralları oluşturulmasını önlemek için udev kuralları taşıyın (veya kaldırın).</span><span class="sxs-lookup"><span data-stu-id="78724-143">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="78724-144">Bir sanal makinede Microsoft Azure veya Hyper-V: kopyaladığınızda, bu kurallar sorunlara neden</span><span class="sxs-lookup"><span data-stu-id="78724-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="78724-145">Ağ hizmeti aşağıdaki komutu çalıştırarak önyükleme sırasında başlayacağını emin olun:</span><span class="sxs-lookup"><span data-stu-id="78724-145">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="78724-146">Aşağıdaki komutu çalıştırarak RHEL depodan paketler yüklemesini etkinleştirmek için Red Hat aboneliğinizin kaydedin:</span><span class="sxs-lookup"><span data-stu-id="78724-146">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="78724-147">WALinuxAgent paket `WALinuxAgent-<version>`, Red Hat ek özellikler depoya gönderilir.</span><span class="sxs-lookup"><span data-stu-id="78724-147">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="78724-148">Ek özellikler deposu, aşağıdaki komutu çalıştırarak etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="78724-148">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="78724-149">Azure için ek çekirdek parametreleri içerecek şekilde kaz yapılandırma çekirdek önyükleme satırı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="78724-149">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="78724-150">Bu değişikliği yapmak için açık `/boot/grub/menu.lst` bir metin düzenleyicisinde ve varsayılan çekirdek aşağıdaki parametreleri içerdiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="78724-150">To do this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="78724-151">Bu, Azure yardımcı olabilecek ilk seri bağlantı noktasına gönderilen tüm konsol iletileri sağlayacak sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="78724-151">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="78724-152">Ayrıca, aşağıdaki parametreleri Kaldır önerilir:</span><span class="sxs-lookup"><span data-stu-id="78724-152">In addition, we recommended that you remove the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="78724-153">Grafik ve sessiz önyükleme seri bağlantı noktasına gönderilecek tüm günlükleri burada istiyoruz bulut ortamında bulunan kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="78724-153">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>  <span data-ttu-id="78724-154">Bırakabilirsiniz `crashkernel` isterseniz yapılandırılmış seçeneği.</span><span class="sxs-lookup"><span data-stu-id="78724-154">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="78724-155">Bu parametre sanal makine tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-155">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more.</span></span> <span data-ttu-id="78724-156">Bu yapılandırma daha küçük sanal makine boyutlarını sorunlu olabilir.</span><span class="sxs-lookup"><span data-stu-id="78724-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="78724-157">RHEL 6.5 ve önceki sürümleri de ayarlamanız gerekir `numa=off` çekirdek parametresi.</span><span class="sxs-lookup"><span data-stu-id="78724-157">RHEL 6.5 and earlier must also set the `numa=off` kernel parameter.</span></span> <span data-ttu-id="78724-158">Red Hat bkz [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="78724-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="78724-159">Güvenli Kabuk (SSH) sunucusu yüklü ve genellikle varsayılan değer önyükleme sırasında başlatılacak şekilde yapılandırılmış olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="78724-159">Ensure that the secure shell (SSH) server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="78724-160">/Etc/ssh/sshd_config aşağıdaki satırı içerecek şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="78724-160">Modify /etc/ssh/sshd_config to include the following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="78724-161">Aşağıdaki komutu çalıştırarak Azure Linux Aracısı'nı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-161">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    <span data-ttu-id="78724-162">WALinuxAgent paketi yükleniyor NetworkManager kaldırır ve zaten kaldırılmadı varsa NetworkManager gnome paketleri adım 3'te.</span><span class="sxs-lookup"><span data-stu-id="78724-162">Installing the WALinuxAgent package removes the NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="78724-163">Takas alanı işletim sistemi disk üzerinde oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-163">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="78724-164">Azure Linux Aracısı, Azure üzerinde sanal makine sağlandıktan sonra sanal makineye bağlı yerel kaynak disk kullanarak takas alanı otomatik olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78724-164">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="78724-165">Yerel kaynak disk geçici bir diski olduğundan ve sanal makine sağlaması kaldırılıyor. sağlaması zaman, boşaltılabilir olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-165">Note that the local resource disk is a temporary disk and that it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="78724-166">Önceki adımda Azure Linux Aracısı'nı yükledikten sonra aşağıdaki /etc/waagent.conf parametrelerinde uygun şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="78724-166">After you install the Azure Linux Agent in the previous step, modify the following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

14. <span data-ttu-id="78724-167">Abonelik, aşağıdaki komutu çalıştırarak (gerekirse) kaydı:</span><span class="sxs-lookup"><span data-stu-id="78724-167">Unregister the subscription (if necessary) by running the following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="78724-168">Sanal makine yetkisini kaldırma ve Azure üzerinde sağlamak için hazırlamak için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="78724-168">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="78724-169">Tıklatın **eylem** > **kapatma** Hyper-V Yöneticisi'nde.</span><span class="sxs-lookup"><span data-stu-id="78724-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="78724-170">Linux VHD Azure'a karşıya yüklenecek artık hazırdır.</span><span class="sxs-lookup"><span data-stu-id="78724-170">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="78724-171">Hyper-V Yöneticisi'nden RHEL 7 sanal makineyi hazırlama</span><span class="sxs-lookup"><span data-stu-id="78724-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="78724-172">Hyper-V Yöneticisi'nde sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="78724-172">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="78724-173">Tıklatın **Bağlan** sanal makine için bir konsol penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="78724-173">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="78724-174">Oluşturma veya düzenleme `/etc/sysconfig/network` dosyasını bulun ve aşağıdaki metni ekleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-174">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="78724-175">Oluşturma veya düzenleme `/etc/sysconfig/network-scripts/ifcfg-eth0` dosyasını bulun ve aşağıdaki metni ekleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-175">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="78724-176">Ağ hizmeti aşağıdaki komutu çalıştırarak önyükleme sırasında başlayacağını emin olun:</span><span class="sxs-lookup"><span data-stu-id="78724-176">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="78724-177">Aşağıdaki komutu çalıştırarak RHEL depodan paketler yüklemesini etkinleştirmek için Red Hat aboneliğinizin kaydedin:</span><span class="sxs-lookup"><span data-stu-id="78724-177">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="78724-178">Azure için ek çekirdek parametreleri içerecek şekilde kaz yapılandırma çekirdek önyükleme satırı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="78724-178">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="78724-179">Bu değişikliği yapmak için açık `/etc/default/grub` bir metin Düzenleyicisi'ni ve düzenleme `GRUB_CMDLINE_LINUX` parametresi.</span><span class="sxs-lookup"><span data-stu-id="78724-179">To do this modification, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="78724-180">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="78724-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="78724-181">Bu, Azure yardımcı olabilecek ilk seri bağlantı noktasına gönderilen tüm konsol iletileri sağlayacak sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="78724-181">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="78724-182">Bu yapılandırma aynı zamanda NIC için yeni RHEL 7 adlandırma kuralları devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="78724-182">This configuration also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="78724-183">Ayrıca, aşağıdaki parametreleri kaldırmanızı öneririz:</span><span class="sxs-lookup"><span data-stu-id="78724-183">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="78724-184">Grafik ve sessiz önyükleme seri bağlantı noktasına gönderilecek tüm günlükleri burada istiyoruz bulut ortamında bulunan kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="78724-184">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="78724-185">Bırakabilirsiniz `crashkernel` isterseniz yapılandırılmış seçeneği.</span><span class="sxs-lookup"><span data-stu-id="78724-185">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="78724-186">Bu parametre, daha küçük sanal makine boyutlarını sorunlu olabilir sanal makine tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-186">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="78724-187">Tamamlandıktan sonra düzenleme `/etc/default/grub`, kaz yapılandırma yeniden oluşturmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="78724-187">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="78724-188">SSH sunucusu yüklü ve genellikle varsayılan değer önyükleme sırasında başlatılacak şekilde yapılandırılmış olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="78724-188">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="78724-189">Değiştirme `/etc/ssh/sshd_config` aşağıdaki satırı eklemek için:</span><span class="sxs-lookup"><span data-stu-id="78724-189">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="78724-190">WALinuxAgent paket `WALinuxAgent-<version>`, Red Hat ek özellikler depoya gönderilir.</span><span class="sxs-lookup"><span data-stu-id="78724-190">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="78724-191">Ek özellikler deposu, aşağıdaki komutu çalıştırarak etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="78724-191">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="78724-192">Aşağıdaki komutu çalıştırarak Azure Linux Aracısı'nı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-192">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="78724-193">Takas alanı işletim sistemi disk üzerinde oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-193">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="78724-194">Azure Linux Aracısı, Azure üzerinde sanal makine sağlandıktan sonra sanal makineye bağlı yerel kaynak disk kullanarak takas alanı otomatik olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78724-194">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="78724-195">Yerel kaynak disk geçici bir diski olduğundan ve sanal makine sağlaması kaldırılıyor. sağlaması zaman boşaltılabilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-195">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="78724-196">Önceki adımda Azure Linux Aracısı'nı yükledikten sonra aşağıdaki parametreleri değiştirmek `/etc/waagent.conf` uygun şekilde:</span><span class="sxs-lookup"><span data-stu-id="78724-196">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="78724-197">Abonelik kaydı istiyorsanız, aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="78724-197">If you want to unregister the subscription, run the following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="78724-198">Sanal makine yetkisini kaldırma ve Azure üzerinde sağlamak için hazırlamak için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="78724-198">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="78724-199">Tıklatın **eylem** > **kapatma** Hyper-V Yöneticisi'nde.</span><span class="sxs-lookup"><span data-stu-id="78724-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="78724-200">Linux VHD Azure'a karşıya yüklenecek artık hazırdır.</span><span class="sxs-lookup"><span data-stu-id="78724-200">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="78724-201">Red Hat tabanlı sanal makineyi KVM hazırlama</span><span class="sxs-lookup"><span data-stu-id="78724-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="78724-202">KVM RHEL 6 sanal makineyi hazırlama</span><span class="sxs-lookup"><span data-stu-id="78724-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="78724-203">RHEL 6 KVM görüntüsü Red Hat Web sitesinden indirin.</span><span class="sxs-lookup"><span data-stu-id="78724-203">Download the KVM image of RHEL 6 from the Red Hat website.</span></span>

2. <span data-ttu-id="78724-204">Bir kök parola ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="78724-204">Set a root password.</span></span>

    <span data-ttu-id="78724-205">Şifrelenmiş bir parola oluşturmak ve komutunun çıktısını kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="78724-205">Generate an encrypted password, and copy the output of the command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="78724-206">Guestfish olan bir kök parola ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="78724-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="78724-207">Kök kullanıcıdan ikinci alanı değiştirme "!!"</span><span class="sxs-lookup"><span data-stu-id="78724-207">Change the second field of the root user from "!!"</span></span> <span data-ttu-id="78724-208">şifrelenmiş parolası.</span><span class="sxs-lookup"><span data-stu-id="78724-208">to the encrypted password.</span></span>

3. <span data-ttu-id="78724-209">Bir sanal makine içinde KVM qcow2 görüntüden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="78724-209">Create a virtual machine in KVM from the qcow2 image.</span></span> <span data-ttu-id="78724-210">Disk türünü ayarlamak **qcow2**, sanal ağ arabirimi cihaz modeli ayarlanmış ve **virtio**.</span><span class="sxs-lookup"><span data-stu-id="78724-210">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span></span> <span data-ttu-id="78724-211">Ardından, sanal makineyi başlatmak ve kök olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="78724-211">Then, start the virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="78724-212">Oluşturma veya düzenleme `/etc/sysconfig/network` dosyasını bulun ve aşağıdaki metni ekleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-212">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="78724-213">Oluşturma veya düzenleme `/etc/sysconfig/network-scripts/ifcfg-eth0` dosyasını bulun ve aşağıdaki metni ekleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-213">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="78724-214">Ethernet arabirimi için statik kuralları oluşturulmasını önlemek için udev kuralları taşıyın (veya kaldırın).</span><span class="sxs-lookup"><span data-stu-id="78724-214">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="78724-215">Bir sanal makinede Azure veya Hyper-V: kopyaladığınızda, bu kurallar sorunlara neden</span><span class="sxs-lookup"><span data-stu-id="78724-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="78724-216">Ağ hizmeti aşağıdaki komutu çalıştırarak önyükleme sırasında başlayacağını emin olun:</span><span class="sxs-lookup"><span data-stu-id="78724-216">Ensure that the network service will start at boot time by running the following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="78724-217">Aşağıdaki komutu çalıştırarak RHEL depodan paketler yüklemesini etkinleştirmek için Red Hat aboneliğinizin kaydedin:</span><span class="sxs-lookup"><span data-stu-id="78724-217">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="78724-218">Azure için ek çekirdek parametreleri içerecek şekilde kaz yapılandırma çekirdek önyükleme satırı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="78724-218">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="78724-219">Bu yapılandırma yapmak için açık `/boot/grub/menu.lst` bir metin düzenleyicisinde ve varsayılan çekirdek aşağıdaki parametreleri içerdiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="78724-219">To do this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="78724-220">Bu, Azure yardımcı olabilecek ilk seri bağlantı noktasına gönderilen tüm konsol iletileri sağlayacak sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="78724-220">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="78724-221">Ayrıca, aşağıdaki parametreleri kaldırmanızı öneririz:</span><span class="sxs-lookup"><span data-stu-id="78724-221">In addition, we recommend that you remove the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="78724-222">Grafik ve sessiz önyükleme seri bağlantı noktasına gönderilecek tüm günlükleri burada istiyoruz bulut ortamında bulunan kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="78724-222">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="78724-223">Bırakabilirsiniz `crashkernel` isterseniz yapılandırılmış seçeneği.</span><span class="sxs-lookup"><span data-stu-id="78724-223">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="78724-224">Bu parametre, daha küçük sanal makine boyutlarını sorunlu olabilir sanal makine tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-224">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="78724-225">RHEL 6.5 ve önceki sürümleri de ayarlamanız gerekir `numa=off` çekirdek parametresi.</span><span class="sxs-lookup"><span data-stu-id="78724-225">RHEL 6.5 and earlier must also set the `numa=off` kernel parameter.</span></span> <span data-ttu-id="78724-226">Red Hat bkz [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="78724-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="78724-227">Hyper-V modüllerini için initramfs ekleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-227">Add Hyper-V modules to initramfs:</span></span>  

    <span data-ttu-id="78724-228">Düzen `/etc/dracut.conf`, aşağıdaki içeriği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-228">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="78724-229">İnitramfs yeniden oluşturun:</span><span class="sxs-lookup"><span data-stu-id="78724-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="78724-230">Bulut init kaldırın:</span><span class="sxs-lookup"><span data-stu-id="78724-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="78724-231">SSH sunucusu yüklü ve önyükleme sırasında başlatılacak şekilde yapılandırılmış olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="78724-231">Ensure that the SSH server is installed and configured to start at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="78724-232">Aşağıdaki satırları içerecek şekilde /etc/ssh/sshd_config değiştirin:</span><span class="sxs-lookup"><span data-stu-id="78724-232">Modify /etc/ssh/sshd_config to include the following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="78724-233">WALinuxAgent paket `WALinuxAgent-<version>`, Red Hat ek özellikler depoya gönderilir.</span><span class="sxs-lookup"><span data-stu-id="78724-233">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="78724-234">Ek özellikler deposu, aşağıdaki komutu çalıştırarak etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="78724-234">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="78724-235">Aşağıdaki komutu çalıştırarak Azure Linux Aracısı'nı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-235">Install the Azure Linux Agent by running the following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="78724-236">Azure Linux Aracısı, Azure üzerinde sanal makine sağlandıktan sonra sanal makineye bağlı yerel kaynak disk kullanarak takas alanı otomatik olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78724-236">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="78724-237">Yerel kaynak disk geçici bir diski olduğundan ve sanal makine sağlaması kaldırılıyor. sağlaması zaman boşaltılabilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-237">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="78724-238">Önceki adımda Azure Linux Aracısı'nı yükledikten sonra aşağıdaki parametre değiştirme **/etc/waagent.conf** uygun şekilde:</span><span class="sxs-lookup"><span data-stu-id="78724-238">After you install the Azure Linux Agent in the previous step, modify the following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="78724-239">Abonelik, aşağıdaki komutu çalıştırarak (gerekirse) kaydı:</span><span class="sxs-lookup"><span data-stu-id="78724-239">Unregister the subscription (if necessary) by running the following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="78724-240">Sanal makine yetkisini kaldırma ve Azure üzerinde sağlamak için hazırlamak için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="78724-240">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="78724-241">KVM sanal makineyi kapatın.</span><span class="sxs-lookup"><span data-stu-id="78724-241">Shut down the virtual machine in KVM.</span></span>

19. <span data-ttu-id="78724-242">Qcow2 görüntü VHD biçimine dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="78724-242">Convert the qcow2 image to the VHD format.</span></span>

    <span data-ttu-id="78724-243">İlk görüntüyü ham biçimine dönüştürün:</span><span class="sxs-lookup"><span data-stu-id="78724-243">First convert the image to raw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="78724-244">Ham görüntü boyutu 1 MB ile hizalanır emin olun.</span><span class="sxs-lookup"><span data-stu-id="78724-244">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="78724-245">Aksi takdirde, boyutu 1 MB ile hizalamak için yukarı yuvarlar:</span><span class="sxs-lookup"><span data-stu-id="78724-245">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="78724-246">Ham disk sabit boyutlu bir VHD'ye Dönüştür:</span><span class="sxs-lookup"><span data-stu-id="78724-246">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="78724-247">KVM RHEL 7 sanal makineyi hazırlama</span><span class="sxs-lookup"><span data-stu-id="78724-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="78724-248">RHEL 7 KVM görüntüsü Red Hat Web sitesinden indirin.</span><span class="sxs-lookup"><span data-stu-id="78724-248">Download the KVM image of RHEL 7 from the Red Hat website.</span></span> <span data-ttu-id="78724-249">Bu yordamda RHEL 7 örnek olarak kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="78724-249">This procedure uses RHEL 7 as the example.</span></span>

2. <span data-ttu-id="78724-250">Bir kök parola ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="78724-250">Set a root password.</span></span>

    <span data-ttu-id="78724-251">Şifrelenmiş bir parola oluşturmak ve komutunun çıktısını kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="78724-251">Generate an encrypted password, and copy the output of the command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="78724-252">Guestfish olan bir kök parola ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="78724-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="78724-253">Kök kullanıcıdan ikinci alanı değiştirme "!!"</span><span class="sxs-lookup"><span data-stu-id="78724-253">Change the second field of root user from "!!"</span></span> <span data-ttu-id="78724-254">şifrelenmiş parolası.</span><span class="sxs-lookup"><span data-stu-id="78724-254">to the encrypted password.</span></span>

3. <span data-ttu-id="78724-255">Bir sanal makine içinde KVM qcow2 görüntüden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="78724-255">Create a virtual machine in KVM from the qcow2 image.</span></span> <span data-ttu-id="78724-256">Disk türünü ayarlamak **qcow2**, sanal ağ arabirimi cihaz modeli ayarlanmış ve **virtio**.</span><span class="sxs-lookup"><span data-stu-id="78724-256">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span></span> <span data-ttu-id="78724-257">Ardından, sanal makineyi başlatmak ve kök olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="78724-257">Then, start the virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="78724-258">Oluşturma veya düzenleme `/etc/sysconfig/network` dosyasını bulun ve aşağıdaki metni ekleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-258">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="78724-259">Oluşturma veya düzenleme `/etc/sysconfig/network-scripts/ifcfg-eth0` dosyasını bulun ve aşağıdaki metni ekleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-259">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="78724-260">Ağ hizmeti aşağıdaki komutu çalıştırarak önyükleme sırasında başlayacağını emin olun:</span><span class="sxs-lookup"><span data-stu-id="78724-260">Ensure that the network service will start at boot time by running the following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="78724-261">Aşağıdaki komutu çalıştırarak RHEL depodan paketler yüklenmesine olanak sağlamak için Red Hat aboneliğinizi kaydedin:</span><span class="sxs-lookup"><span data-stu-id="78724-261">Register your Red Hat subscription to enable installation of packages from the RHEL repository by running the following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="78724-262">Azure için ek çekirdek parametreleri içerecek şekilde kaz yapılandırma çekirdek önyükleme satırı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="78724-262">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="78724-263">Bu yapılandırma yapmak için açık `/etc/default/grub` bir metin Düzenleyicisi'ni ve düzenleme `GRUB_CMDLINE_LINUX` parametresi.</span><span class="sxs-lookup"><span data-stu-id="78724-263">To do this configuration, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="78724-264">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="78724-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="78724-265">Bu komut, aynı zamanda tüm konsol iletileri hangi Azure yardımcı olabilecek ilk seri bağlantı noktasına gönderilir sağlar sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="78724-265">This command also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="78724-266">Komut ayrıca NIC'ler için yeni RHEL 7 adlandırma kuralları devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="78724-266">The command also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="78724-267">Ayrıca, aşağıdaki parametreleri kaldırmanızı öneririz:</span><span class="sxs-lookup"><span data-stu-id="78724-267">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="78724-268">Grafik ve sessiz önyükleme seri bağlantı noktasına gönderilecek tüm günlükleri burada istiyoruz bulut ortamında bulunan kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="78724-268">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="78724-269">Bırakabilirsiniz `crashkernel` isterseniz yapılandırılmış seçeneği.</span><span class="sxs-lookup"><span data-stu-id="78724-269">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="78724-270">Bu parametre, daha küçük sanal makine boyutlarını sorunlu olabilir sanal makine tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-270">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="78724-271">Tamamlandıktan sonra düzenleme `/etc/default/grub`, kaz yapılandırma yeniden oluşturmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="78724-271">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="78724-272">Hyper-V modüllerini initramfs ekleyin.</span><span class="sxs-lookup"><span data-stu-id="78724-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="78724-273">Düzenleme `/etc/dracut.conf` ve içeriği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="78724-274">İnitramfs yeniden oluşturun:</span><span class="sxs-lookup"><span data-stu-id="78724-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="78724-275">Bulut init kaldırın:</span><span class="sxs-lookup"><span data-stu-id="78724-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="78724-276">SSH sunucusu yüklü ve önyükleme sırasında başlatılacak şekilde yapılandırılmış olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="78724-276">Ensure that the SSH server is installed and configured to start at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="78724-277">Aşağıdaki satırları içerecek şekilde /etc/ssh/sshd_config değiştirin:</span><span class="sxs-lookup"><span data-stu-id="78724-277">Modify /etc/ssh/sshd_config to include the following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="78724-278">WALinuxAgent paket `WALinuxAgent-<version>`, Red Hat ek özellikler depoya gönderilir.</span><span class="sxs-lookup"><span data-stu-id="78724-278">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="78724-279">Ek özellikler deposu, aşağıdaki komutu çalıştırarak etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="78724-279">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="78724-280">Aşağıdaki komutu çalıştırarak Azure Linux Aracısı'nı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-280">Install the Azure Linux Agent by running the following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="78724-281">Waagent hizmetini etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="78724-281">Enable the waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="78724-282">Takas alanı işletim sistemi disk üzerinde oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-282">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="78724-283">Azure Linux Aracısı, Azure üzerinde sanal makine sağlandıktan sonra sanal makineye bağlı yerel kaynak disk kullanarak takas alanı otomatik olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78724-283">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="78724-284">Yerel kaynak disk geçici bir diski olduğundan ve sanal makine sağlaması kaldırılıyor. sağlaması zaman boşaltılabilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-284">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="78724-285">Önceki adımda Azure Linux Aracısı'nı yükledikten sonra aşağıdaki parametreleri değiştirmek `/etc/waagent.conf` uygun şekilde:</span><span class="sxs-lookup"><span data-stu-id="78724-285">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="78724-286">Abonelik, aşağıdaki komutu çalıştırarak (gerekirse) kaydı:</span><span class="sxs-lookup"><span data-stu-id="78724-286">Unregister the subscription (if necessary) by running the following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="78724-287">Sanal makine yetkisini kaldırma ve Azure üzerinde sağlamak için hazırlamak için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="78724-287">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="78724-288">KVM sanal makineyi kapatın.</span><span class="sxs-lookup"><span data-stu-id="78724-288">Shut down the virtual machine in KVM.</span></span>

19. <span data-ttu-id="78724-289">Qcow2 görüntü VHD biçimine dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="78724-289">Convert the qcow2 image to the VHD format.</span></span>

    <span data-ttu-id="78724-290">İlk görüntüyü ham biçimine dönüştürün:</span><span class="sxs-lookup"><span data-stu-id="78724-290">First convert the image to raw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="78724-291">Ham görüntü boyutu 1 MB ile hizalanır emin olun.</span><span class="sxs-lookup"><span data-stu-id="78724-291">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="78724-292">Aksi takdirde, boyutu 1 MB ile hizalamak için yukarı yuvarlar:</span><span class="sxs-lookup"><span data-stu-id="78724-292">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="78724-293">Ham disk sabit boyutlu bir VHD'ye Dönüştür:</span><span class="sxs-lookup"><span data-stu-id="78724-293">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="78724-294">VMware Red Hat tabanlı sanal makineyi hazırlama</span><span class="sxs-lookup"><span data-stu-id="78724-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="78724-295">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="78724-295">Prerequisites</span></span>
<span data-ttu-id="78724-296">Bu bölümde VMware RHEL sanal makine zaten yüklediğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="78724-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="78724-297">VMware içinde bir işletim sistemi yükleme hakkında daha fazla bilgi için bkz [VMware konuk işletim sistemi Yükleme Kılavuzu](http://partnerweb.vmware.com/GOSIG/home.html).</span><span class="sxs-lookup"><span data-stu-id="78724-297">For details about how to install an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="78724-298">Linux işletim sistemi yüklediğinizde, birçok yüklemeleri için varsayılan olduğu çoğunlukla LVM, yerine standart bölümleri kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="78724-298">When you install the Linux operating system, we recommend that you use standard partitions rather than LVM, which is often the default for many installations.</span></span> <span data-ttu-id="78724-299">Özellikle bir işletim sistemi diski hiç sorun giderme için başka bir sanal makineye bağlı gerekiyorsa, bu kopyalanan sanal makinenin LVM adıyla çakışıyor önler.</span><span class="sxs-lookup"><span data-stu-id="78724-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs to be attached to another virtual machine for troubleshooting.</span></span> <span data-ttu-id="78724-300">LVM veya RAID veri disklerde tercih edilen varsa kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="78724-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="78724-301">Bir takas bölüm işletim sistemi disk üzerinde yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-301">Do not configure a swap partition on the operating system disk.</span></span> <span data-ttu-id="78724-302">Geçici kaynak disk üzerinde bir takas dosyası oluşturmak için Linux Aracısı yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78724-302">You can configure the Linux agent to create a swap file on the temporary resource disk.</span></span> <span data-ttu-id="78724-303">Aşağıdaki adımlarda bu hakkında daha fazla bilgi bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78724-303">You can find more information about this in the steps that follow.</span></span>
* <span data-ttu-id="78724-304">Sanal sabit disk oluşturduğunuzda, seçin **depolama sanal diski tek bir dosya olarak**.</span><span class="sxs-lookup"><span data-stu-id="78724-304">When you create the virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="78724-305">VMware RHEL 6 sanal makineyi hazırlama</span><span class="sxs-lookup"><span data-stu-id="78724-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="78724-306">RHEL 6'da, Azure Linux Aracısı ile NetworkManager etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="78724-306">In RHEL 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="78724-307">Bu paket, aşağıdaki komutu çalıştırarak kaldırın:</span><span class="sxs-lookup"><span data-stu-id="78724-307">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="78724-308">Adlı bir dosya oluşturun **ağ** aşağıdaki metni içeren/etc/sysconfig/dizininde:</span><span class="sxs-lookup"><span data-stu-id="78724-308">Create a file named **network** in the /etc/sysconfig/ directory that contains the following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="78724-309">Oluşturma veya düzenleme `/etc/sysconfig/network-scripts/ifcfg-eth0` dosyasını bulun ve aşağıdaki metni ekleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-309">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="78724-310">Ethernet arabirimi için statik kuralları oluşturulmasını önlemek için udev kuralları taşıyın (veya kaldırın).</span><span class="sxs-lookup"><span data-stu-id="78724-310">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="78724-311">Bir sanal makinede Azure veya Hyper-V: kopyaladığınızda, bu kurallar sorunlara neden</span><span class="sxs-lookup"><span data-stu-id="78724-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="78724-312">Ağ hizmeti aşağıdaki komutu çalıştırarak önyükleme sırasında başlayacağını emin olun:</span><span class="sxs-lookup"><span data-stu-id="78724-312">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="78724-313">Aşağıdaki komutu çalıştırarak RHEL depodan paketler yüklemesini etkinleştirmek için Red Hat aboneliğinizin kaydedin:</span><span class="sxs-lookup"><span data-stu-id="78724-313">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="78724-314">WALinuxAgent paket `WALinuxAgent-<version>`, Red Hat ek özellikler depoya gönderilir.</span><span class="sxs-lookup"><span data-stu-id="78724-314">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="78724-315">Ek özellikler deposu, aşağıdaki komutu çalıştırarak etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="78724-315">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="78724-316">Azure için ek çekirdek parametreleri içerecek şekilde kaz yapılandırma çekirdek önyükleme satırı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="78724-316">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="78724-317">Bunu yapmak için açın `/etc/default/grub` bir metin Düzenleyicisi'ni ve düzenleme `GRUB_CMDLINE_LINUX` parametresi.</span><span class="sxs-lookup"><span data-stu-id="78724-317">To do this, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="78724-318">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="78724-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   <span data-ttu-id="78724-319">Bu, Azure yardımcı olabilecek ilk seri bağlantı noktasına gönderilen tüm konsol iletileri sağlayacak sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="78724-319">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="78724-320">Ayrıca, aşağıdaki parametreleri kaldırmanızı öneririz:</span><span class="sxs-lookup"><span data-stu-id="78724-320">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="78724-321">Grafik ve sessiz önyükleme seri bağlantı noktasına gönderilecek tüm günlükleri burada istiyoruz bulut ortamında bulunan kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="78724-321">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="78724-322">Bırakabilirsiniz `crashkernel` isterseniz yapılandırılmış seçeneği.</span><span class="sxs-lookup"><span data-stu-id="78724-322">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="78724-323">Bu parametre, daha küçük sanal makine boyutlarını sorunlu olabilir sanal makine tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-323">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="78724-324">Hyper-V modüllerini için initramfs ekleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-324">Add Hyper-V modules to initramfs:</span></span>

    <span data-ttu-id="78724-325">Düzen `/etc/dracut.conf`, aşağıdaki içeriği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-325">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="78724-326">İnitramfs yeniden oluşturun:</span><span class="sxs-lookup"><span data-stu-id="78724-326">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="78724-327">SSH sunucusu yüklü ve genellikle varsayılan değer önyükleme sırasında başlatılacak şekilde yapılandırılmış olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="78724-327">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="78724-328">Değiştirme `/etc/ssh/sshd_config` aşağıdaki satırı eklemek için:</span><span class="sxs-lookup"><span data-stu-id="78724-328">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

    <span data-ttu-id="78724-329">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="78724-329">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="78724-330">Aşağıdaki komutu çalıştırarak Azure Linux Aracısı'nı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-330">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="78724-331">Takas alanı işletim sistemi disk üzerinde oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-331">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="78724-332">Azure Linux Aracısı, Azure üzerinde sanal makine sağlandıktan sonra sanal makineye bağlı yerel kaynak disk kullanarak takas alanı otomatik olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78724-332">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="78724-333">Yerel kaynak disk geçici bir diski olduğundan ve sanal makine sağlaması kaldırılıyor. sağlaması zaman boşaltılabilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-333">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="78724-334">Önceki adımda Azure Linux Aracısı'nı yükledikten sonra aşağıdaki parametreleri değiştirmek `/etc/waagent.conf` uygun şekilde:</span><span class="sxs-lookup"><span data-stu-id="78724-334">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="78724-335">Abonelik, aşağıdaki komutu çalıştırarak (gerekirse) kaydı:</span><span class="sxs-lookup"><span data-stu-id="78724-335">Unregister the subscription (if necessary) by running the following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="78724-336">Sanal makine yetkisini kaldırma ve Azure üzerinde sağlamak için hazırlamak için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="78724-336">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="78724-337">Sanal makineyi kapatın ve VMDK dosyasını bir .vhd dosyasına dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="78724-337">Shut down the virtual machine, and convert the VMDK file to a .vhd file.</span></span>

    <span data-ttu-id="78724-338">İlk görüntüyü ham biçimine dönüştürün:</span><span class="sxs-lookup"><span data-stu-id="78724-338">First convert the image to raw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="78724-339">Ham görüntü boyutu 1 MB ile hizalanır emin olun.</span><span class="sxs-lookup"><span data-stu-id="78724-339">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="78724-340">Aksi takdirde, boyutu 1 MB ile hizalamak için yukarı yuvarlar:</span><span class="sxs-lookup"><span data-stu-id="78724-340">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="78724-341">Ham disk sabit boyutlu bir VHD'ye Dönüştür:</span><span class="sxs-lookup"><span data-stu-id="78724-341">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="78724-342">VMware RHEL 7 sanal makineyi hazırlama</span><span class="sxs-lookup"><span data-stu-id="78724-342">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="78724-343">Oluşturma veya düzenleme `/etc/sysconfig/network` dosyasını bulun ve aşağıdaki metni ekleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-343">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="78724-344">Oluşturma veya düzenleme `/etc/sysconfig/network-scripts/ifcfg-eth0` dosyasını bulun ve aşağıdaki metni ekleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-344">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="78724-345">Ağ hizmeti aşağıdaki komutu çalıştırarak önyükleme sırasında başlayacağını emin olun:</span><span class="sxs-lookup"><span data-stu-id="78724-345">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="78724-346">Aşağıdaki komutu çalıştırarak RHEL depodan paketler yüklemesini etkinleştirmek için Red Hat aboneliğinizin kaydedin:</span><span class="sxs-lookup"><span data-stu-id="78724-346">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="78724-347">Azure için ek çekirdek parametreleri içerecek şekilde kaz yapılandırma çekirdek önyükleme satırı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="78724-347">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="78724-348">Bu değişikliği yapmak için açık `/etc/default/grub` bir metin Düzenleyicisi'ni ve düzenleme `GRUB_CMDLINE_LINUX` parametresi.</span><span class="sxs-lookup"><span data-stu-id="78724-348">To do this modification, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="78724-349">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="78724-349">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="78724-350">Bu yapılandırma, aynı zamanda tüm konsol iletileri hangi Azure yardımcı olabilecek ilk seri bağlantı noktasına gönderilir sağlar sorunları ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="78724-350">This configuration also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="78724-351">Aynı zamanda NIC için yeni RHEL 7 adlandırma kuralları devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="78724-351">It also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="78724-352">Ayrıca, aşağıdaki parametreleri kaldırmanızı öneririz:</span><span class="sxs-lookup"><span data-stu-id="78724-352">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="78724-353">Grafik ve sessiz önyükleme seri bağlantı noktasına gönderilecek tüm günlükleri burada istiyoruz bulut ortamında bulunan kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="78724-353">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="78724-354">Bırakabilirsiniz `crashkernel` isterseniz yapılandırılmış seçeneği.</span><span class="sxs-lookup"><span data-stu-id="78724-354">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="78724-355">Bu parametre, daha küçük sanal makine boyutlarını sorunlu olabilir sanal makine tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-355">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="78724-356">Tamamlandıktan sonra düzenleme `/etc/default/grub`, kaz yapılandırma yeniden oluşturmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="78724-356">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="78724-357">Hyper-V modüllerini initramfs için ekleyin.</span><span class="sxs-lookup"><span data-stu-id="78724-357">Add Hyper-V modules to initramfs.</span></span>

    <span data-ttu-id="78724-358">Düzen `/etc/dracut.conf`, içeriği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-358">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="78724-359">İnitramfs yeniden oluşturun:</span><span class="sxs-lookup"><span data-stu-id="78724-359">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="78724-360">SSH sunucusu yüklü ve önyükleme sırasında başlatılacak şekilde yapılandırılmış olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="78724-360">Ensure that the SSH server is installed and configured to start at boot time.</span></span> <span data-ttu-id="78724-361">Bu genellikle varsayılan ayardır.</span><span class="sxs-lookup"><span data-stu-id="78724-361">This setting is usually the default.</span></span> <span data-ttu-id="78724-362">Değiştirme `/etc/ssh/sshd_config` aşağıdaki satırı eklemek için:</span><span class="sxs-lookup"><span data-stu-id="78724-362">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="78724-363">WALinuxAgent paket `WALinuxAgent-<version>`, Red Hat ek özellikler depoya gönderilir.</span><span class="sxs-lookup"><span data-stu-id="78724-363">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="78724-364">Ek özellikler deposu, aşağıdaki komutu çalıştırarak etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="78724-364">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="78724-365">Aşağıdaki komutu çalıştırarak Azure Linux Aracısı'nı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-365">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="78724-366">Takas alanı işletim sistemi disk üzerinde oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-366">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="78724-367">Azure Linux Aracısı, Azure üzerinde sanal makine sağlandıktan sonra sanal makineye bağlı yerel kaynak disk kullanarak takas alanı otomatik olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78724-367">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="78724-368">Yerel kaynak disk geçici bir diski olduğundan ve sanal makine sağlaması kaldırılıyor. sağlaması zaman boşaltılabilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="78724-368">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="78724-369">Önceki adımda Azure Linux Aracısı'nı yükledikten sonra aşağıdaki parametreleri değiştirmek `/etc/waagent.conf` uygun şekilde:</span><span class="sxs-lookup"><span data-stu-id="78724-369">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

12. <span data-ttu-id="78724-370">Abonelik kaydı istiyorsanız, aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="78724-370">If you want to unregister the subscription, run the following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="78724-371">Sanal makine yetkisini kaldırma ve Azure üzerinde sağlamak için hazırlamak için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="78724-371">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="78724-372">Sanal makineyi kapatın ve VMDK dosyasını VHD biçimine dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="78724-372">Shut down the virtual machine, and convert the VMDK file to the VHD format.</span></span>

    <span data-ttu-id="78724-373">İlk görüntüyü ham biçimine dönüştürün:</span><span class="sxs-lookup"><span data-stu-id="78724-373">First convert the image to raw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="78724-374">Ham görüntü boyutu 1 MB ile hizalanır emin olun.</span><span class="sxs-lookup"><span data-stu-id="78724-374">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="78724-375">Aksi takdirde, boyutu 1 MB ile hizalamak için yukarı yuvarlar:</span><span class="sxs-lookup"><span data-stu-id="78724-375">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="78724-376">Ham disk sabit boyutlu bir VHD'ye Dönüştür:</span><span class="sxs-lookup"><span data-stu-id="78724-376">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="78724-377">Red Hat tabanlı sanal makineyi kickstart dosyası otomatik olarak kullanarak bir ISO hazırlama</span><span class="sxs-lookup"><span data-stu-id="78724-377">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="78724-378">Bir kickstart dosyasından RHEL 7 sanal makineyi hazırlama</span><span class="sxs-lookup"><span data-stu-id="78724-378">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="78724-379">Aşağıdaki içeriği içeren bir kickstart dosyası oluşturun ve dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="78724-379">Create a kickstart file that includes the following content, and save the file.</span></span> <span data-ttu-id="78724-380">Kickstart yükleme hakkında daha fazla ayrıntı için bkz: [Kickstart Yükleme Kılavuzu'na](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span><span class="sxs-lookup"><span data-stu-id="78724-380">For details about kickstart installation, see the [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run the Setup Agent on first boot
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

        # Clear the MBR
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

        # Power down the machine after install
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

        # Disable the root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set the cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build the grub cfg
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

2. <span data-ttu-id="78724-381">Burada yükleme sistem erişebildiğinizi kickstart dosyasını yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="78724-381">Place the kickstart file where the installation system can access it.</span></span>

3. <span data-ttu-id="78724-382">Hyper-V Yöneticisi'nde yeni bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="78724-382">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="78724-383">Üzerinde **sanal Hard diske Bağlan** sayfasında, **bir sanal sabit diski sonra Ekle**ve yeni sanal makine Sihirbazı'nı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="78724-383">On the **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete the New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="78724-384">Sanal makine ayarlarını açın:</span><span class="sxs-lookup"><span data-stu-id="78724-384">Open the virtual machine settings:</span></span>

    <span data-ttu-id="78724-385">a.</span><span class="sxs-lookup"><span data-stu-id="78724-385">a.</span></span>  <span data-ttu-id="78724-386">Yeni bir sanal sabit disk sanal makineye Ekle.</span><span class="sxs-lookup"><span data-stu-id="78724-386">Attach a new virtual hard disk to the virtual machine.</span></span> <span data-ttu-id="78724-387">Seçtiğinizden emin olun **VHD biçimi** ve **sabit boyutlu**.</span><span class="sxs-lookup"><span data-stu-id="78724-387">Make sure to select **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="78724-388">b.</span><span class="sxs-lookup"><span data-stu-id="78724-388">b.</span></span>  <span data-ttu-id="78724-389">ISO yükleme DVD sürücüsü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="78724-389">Attach the installation ISO to the DVD drive.</span></span>

    <span data-ttu-id="78724-390">c.</span><span class="sxs-lookup"><span data-stu-id="78724-390">c.</span></span>  <span data-ttu-id="78724-391">CD'den önyükleme için BIOS ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="78724-391">Set the BIOS to boot from CD.</span></span>

5. <span data-ttu-id="78724-392">Sanal makineyi başlatın.</span><span class="sxs-lookup"><span data-stu-id="78724-392">Start the virtual machine.</span></span> <span data-ttu-id="78724-393">Yükleme Kılavuzu göründüğünde, basın **sekmesini** önyükleme seçeneklerini yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="78724-393">When the installation guide appears, press **Tab** to configure the boot options.</span></span>

6. <span data-ttu-id="78724-394">ENTER `inst.ks=<the location of the kickstart file>` önyükleme seçenekleri ve tuşuna sonunda **Enter**.</span><span class="sxs-lookup"><span data-stu-id="78724-394">Enter `inst.ks=<the location of the kickstart file>` at the end of the boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="78724-395">Yüklemesinin tamamlanması için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="78724-395">Wait for the installation to finish.</span></span> <span data-ttu-id="78724-396">Tamamlandığında, sanal makine otomatik olarak kapatılacak.</span><span class="sxs-lookup"><span data-stu-id="78724-396">When it's finished, the virtual machine will be shut down automatically.</span></span> <span data-ttu-id="78724-397">Linux VHD Azure'a karşıya yüklenecek artık hazırdır.</span><span class="sxs-lookup"><span data-stu-id="78724-397">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="78724-398">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="78724-398">Known issues</span></span>
### <a name="the-hyper-v-driver-could-not-be-included-in-the-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="78724-399">Hyper-V sürücü başlangıç RAM diski, bir Hyper-V olmayan hiper kullanırken eklenemedi</span><span class="sxs-lookup"><span data-stu-id="78724-399">The Hyper-V driver could not be included in the initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="78724-400">Bir Hyper-V ortamında çalıştığını Linux algılar sürece bazı durumlarda, Linux yükleyicileri sürücüleri Hyper-V için başlangıç RAM disk (initrd veya initramfs) içermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="78724-400">In some cases, Linux installers might not include the drivers for Hyper-V in the initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="78724-401">Linux görüntüsünü hazırlamak için farklı sanallaştırma sistem (diğer bir deyişle, Virtualbox, Xen, vb.) kullanırken, en az emin olmak için initrd yeniden oluşturmanız gerekebilir hv_vmbus ve hv_storvsc çekirdek modülleri başlangıç RAM disk üzerindeki kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="78724-401">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) to prepare your Linux image, you might need to rebuild initrd to ensure that at least the hv_vmbus and hv_storvsc kernel modules are available on the initial RAM disk.</span></span> <span data-ttu-id="78724-402">Bilinen bir sorun en az Yukarı Akış Red Hat dağıtım tabanlı sistemlerde budur.</span><span class="sxs-lookup"><span data-stu-id="78724-402">This is a known issue at least on systems that are based on the upstream Red Hat distribution.</span></span>

<span data-ttu-id="78724-403">Bu sorunu çözmek için initramfs Hyper-V modüllerini ekleyin ve yeniden oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="78724-403">To resolve this issue, add Hyper-V modules to initramfs and rebuild it:</span></span>

<span data-ttu-id="78724-404">Düzen `/etc/dracut.conf`, aşağıdaki içeriği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="78724-404">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="78724-405">İnitramfs yeniden oluşturun:</span><span class="sxs-lookup"><span data-stu-id="78724-405">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="78724-406">Daha fazla ayrıntı için bilgi [initramfs yeniden](https://access.redhat.com/solutions/1958).</span><span class="sxs-lookup"><span data-stu-id="78724-406">For more details, see the information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="78724-407">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="78724-407">Next steps</span></span>
<span data-ttu-id="78724-408">Şimdi yeni sanal makineler oluşturmak için Red Hat Enterprise Linux sanal sabit diski kullanmak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="78724-408">You're now ready to use your Red Hat Enterprise Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="78724-409">Adım 2 ve 3'te Azure'a .vhd dosyasını karşıya yüklüyoruz ilk kez kullanıyorsanız bkz [oluşturma ve Linux işletim sistemini içeren bir sanal sabit disk karşıya](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="78724-409">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="78724-410">Red Hat Enterprise Linux çalıştırmak için sertifikalı hiper hakkında daha fazla ayrıntı için bkz: [Red Hat Web sitesi](https://access.redhat.com/certified-hypervisors).</span><span class="sxs-lookup"><span data-stu-id="78724-410">For more details about the hypervisors that are certified to run Red Hat Enterprise Linux, see [the Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
