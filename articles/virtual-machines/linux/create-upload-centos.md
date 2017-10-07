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
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a>Azure’da CentOS tabanlı bir sanal makine hazırlama
* [Azure için CentOS 6.x sanal makineyi hazırlama](#centos-6x)
* [Azure için CentOS 7.0 + sanal makineyi hazırlama](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Ön koşullar
Bu makalede, bir CentOS zaten yüklemiş olduğunuz varsayılmaktadır (veya benzer türevi) Linux işletim sistemi tooa sanal sabit disk. Birden çok araç toocreate .vhd dosyaları, örneğin bir sanallaştırma çözümü Hyper-V gibi mevcut. Yönergeler için bkz: [hello Hyper-V rolünü yükleyin ve sanal makine yapılandırma](http://technet.microsoft.com/library/hh846766.aspx).

**CentOS yükleme notları**

* Ayrıca bkz [genel Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes) Linux Azure için hazırlama hakkında daha fazla ipucu için.
* Merhaba VHDX biçimi, Azure'da yalnızca desteklenmiyor **VHD sabit**.  Hyper-V Yöneticisi'ni kullanarak hello disk tooVHD biçimine Dönüştür veya convert-vhd cmdlet hello. VirtualBox kullanıyorsanız bu seçerek gelir **boyutu sabit** olarak hello disk oluşturulurken dinamik olarak ayrılan toohello varsayılan değil.
* Merhaba Linux sistemi yüklerken olan *önerilen* LVM (genellikle birçok yüklemeleri için hello varsayılan) yerine standart bölümleri kullanın. Özellikle bir işletim sistemi diski bağlı toobe tooanother hiç gerekiyorsa bu kopyalanan VM'ler LVM adıyla çakışıyor kurtulursunuz sorun giderme için aynı VM. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veri diskler üzerinde kullanılabilir.
* UDF dosya sistemleri bağlanması için çekirdek desteği gereklidir. Sağlama yapılandırma Azure hello üzerinde ilk önyükleme sırasında toohello Linux VM ekli toohello Konuk UDF biçimli ortamının geçirilir. Hello Azure Linux Aracısı yapılandırmasını mümkün toomount hello UDF dosya sistemi tooread olması gerekir ve hello VM sağlayın.
* Linux çekirdek sürümleri 2.6.37 aşağıda NUMA ile büyük VM boyutları üzerinde Hyper-V desteklemez. Eski dağıtımları hello upstream kullanarak bu sorun öncelikle etkileri Red Hat 2.6.32 çekirdek ve RHEL 6.6 (çekirdek 2.6.32 504) giderilmiştir. 2.6.32-504 ayarlamalısınız daha özel tekrar 2.6.37 eski veya tekrar eski RHEL tabanlı çalıştıran sistemlerde hello önyükleme parametresinin `numa=off` hello çekirdeğini grub.conf içinde komut satırı. Red Hat daha fazla bilgi için bkz: [KB 436883](https://access.redhat.com/solutions/436883).
* Bir takas bölüm hello işletim sistemi disk üzerinde yapılandırmayın. Merhaba Linux Aracısı yapılandırılmış toocreate hello geçici kaynak disk üzerinde bir takas dosyası olabilir.  Merhaba aşağıdaki adımlarda bu hakkında daha fazla bilgi bulunabilir.
* Tüm hello VHD boyutları 1 MB'ün katları olmalıdır.

## <a name="centos-6x"></a>CentOS 6.x

1. Hyper-V Yöneticisi'nde hello sanal makineyi seçin.

2. Tıklatın **Bağlan** tooopen hello sanal makine için bir konsol penceresi.

3. CentOS 6'hello Azure Linux Aracısı ile NetworkManager etkileyebilir. Merhaba aşağıdaki komutu çalıştırarak bu paketi kaldırma:
   
        # sudo rpm -e --nodeps NetworkManager

4. Oluşturma veya hello dosya düzenleme `/etc/sysconfig/network` ve metin aşağıdaki hello ekleyin:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Oluşturma veya hello dosya düzenleme `/etc/sysconfig/network-scripts/ifcfg-eth0` ve metin aşağıdaki hello ekleyin:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Udev kuralları tooavoid hello Ethernet arabirimi için statik kuralları oluşturma değiştirin. Bu kurallar, bir sanal makinede Microsoft Azure veya Hyper-V: kopyalarken sorunlara neden olabilir
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Merhaba ağ hizmetini hello aşağıdaki komutu çalıştırarak önyükleme sırasında başlatacak emin olun:
   
        # sudo chkconfig network on

8. Hello Azure veri merkezleri içinde barındırılan toouse hello OpenLogic yansıtmalar isterseniz hello yerine `/etc/yum.repos.d/CentOS-Base.repo` depoları aşağıdaki hello dosyasıyla.  Bu ayrıca hello ekler **[openlogic]** hello Azure Linux aracısı gibi ek paketler içeren depo:

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
    Merhaba bu kılavuzun ilerleyen kullanmakta olduğunuz varsayacak en az hello `[openlogic]` kullanılan tooinstall hello Azure Linux aracısı aşağıdaki olacaktır deposu.


9. Satır too/etc/yum.conf aşağıdaki hello ekleyin:
    
        http_caching=packages

10. Komut tooclear hello geçerli yum meta verileri ve güncelleştirme hello sistemi hello son paketleri ile aşağıdaki hello çalıştırın:
    
        # yum clean all

    CentOS daha eski bir sürümü için görüntü oluşturmakta olduğunuz sürece, tüm hello tooupdate toohello son paketleri önerilir:

        # sudo yum -y update

    Bu komutu çalıştırdıktan sonra bir yeniden başlatma gerekli olabilir.

11. (İsteğe bağlı) Merhaba Linux Tümleştirme hizmetleri (LIS) için Hello sürücüleri yükleyin.
   
    >[!IMPORTANT]
    Merhaba adım **gerekli** için CentOS 6,3 ve önceki ve sonraki sürümler için isteğe bağlıdır.

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    Alternatif olarak, üzerinde hello hello el ile yükleme yönergeleri izleyebilir [LIS indirme sayfasına](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello VM üzerine RPM.
 
12. Hello Azure Linux aracısı ve bağımlılıkları yükleyin:
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    Bunlar zaten 3. adımda açıklandığı gibi kaldırılmamışsa hello WALinuxAgent paketi hello NetworkManager ve NetworkManager gnome paketleri kaldırın.


13. Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin. toodo Bu, açık `/boot/grub/menu.lst` bir metin düzenleyicisinde ve o hello varsayılan çekirdek şu parametreler hello içerdiğinden emin olun:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, tüm konsol iletileri gönderilir sağlayacak sorunları ayıklama desteği.
    
    Ayrıca toohello yukarıdaki, çok önerilir*kaldırmak* hello şu Parametreler:
    
        rhgb quiet crashkernel=auto
    
    Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir.  Merhaba `crashkernel` seçeneği olabilir sol isterseniz yapılandırılmış, ancak Not hello küçük VM boyutlarını sorunlu olabilecek bu parametre hello hello VM tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır.

    >[!Important]
    CentOS 6.5 ve daha önceki hello çekirdek parametresi de ayarlamanız gerekir `numa=off`. Red Hat bkz [KB 436883](https://access.redhat.com/solutions/436883).

14. Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun.  Bu genellikle hello varsayılandır.

15. Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.
    
    Hello Azure Linux Aracısı otomatik olarak takas alanı ekli toohello VM Azure üzerinde sağladıktan sonra hello yerel kaynak diski kullanarak yapılandırabilirsiniz. Bu hello yerel kaynak diski Not bir *geçici* disk ve hello VM deprovisioned olduğunda boşaltılabilir. Yükledikten sonra Azure Linux Aracısı hello (önceki adıma bakın), parametreleri aşağıdaki hello değiştirme `/etc/waagent.conf` uygun şekilde:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. Tıklatın **eylem -> kapatma aşağı** Hyper-V Yöneticisi'nde. Hazır toobe tooAzure karşıya artık Linux VHD olur.


- - -
## <a name="centos-70"></a>CentOS 7.0 +
**CentOS 7 (ve benzer türevleri) değişiklikleri**

CentOS 7 sanal makine için Azure hazırlanıyor ancak eşitlenmeyeceği birkaç önemli farklılıklar vardır çok benzer tooCentOS 6, şöyledir:

* Merhaba NetworkManager paketi artık hello Azure Linux Aracısı ile çakışıyor. Bu paketi varsayılan olarak yüklenir ve onu kaldırılmaz öneririz.
* GRUB2 şimdi varsayılan önyükleme yükleyicisi, çekirdek parametreleri düzenlemek için hello yordamı (aşağıya bakın) değişti şekilde hello olarak kullanılır.
* XFS hello varsayılan dosya sistemi sunulmuştur. Merhaba ext4 dosya sistemi hala isterseniz kullanılabilir.

**Yapılandırma adımları**

1. Hyper-V Yöneticisi'nde hello sanal makineyi seçin.

2. Tıklatın **Bağlan** tooopen hello sanal makine için bir konsol penceresi.

3. Oluşturma veya hello dosya düzenleme `/etc/sysconfig/network` ve metin aşağıdaki hello ekleyin:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Oluşturma veya hello dosya düzenleme `/etc/sysconfig/network-scripts/ifcfg-eth0` ve metin aşağıdaki hello ekleyin:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Udev kuralları tooavoid hello Ethernet arabirimi için statik kuralları oluşturma değiştirin. Bu kurallar, bir sanal makinede Microsoft Azure veya Hyper-V: kopyalarken sorunlara neden olabilir
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. Hello Azure veri merkezleri içinde barındırılan toouse hello OpenLogic yansıtmalar isterseniz hello yerine `/etc/yum.repos.d/CentOS-Base.repo` depoları aşağıdaki hello dosyasıyla.  Bu ayrıca hello ekler **[openlogic]** hello Azure Linux Aracısı paketleri içeren depo:
   
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
    Merhaba bu kılavuzun ilerleyen kullanmakta olduğunuz varsayacak en az hello `[openlogic]` kullanılan tooinstall hello Azure Linux aracısı aşağıdaki olacaktır deposu.

7. Aşağıdaki komut tooclear hello geçerli yum meta hello çalıştırın ve tüm güncelleştirmeleri yükleyin:
   
        # sudo yum clean all

    CentOS daha eski bir sürümü için görüntü oluşturmakta olduğunuz sürece, tüm hello tooupdate toohello son paketleri önerilir:

        # sudo yum -y update

    Bir yeniden başlatma belki de bu komutu çalıştırdıktan sonra gerekiyor.

8. Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin. toodo Bu, açık `/etc/default/grub` bir metin düzenleyicisi ve düzenleme hello içinde `GRUB_CMDLINE_LINUX` parametresi, örneğin:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, tüm konsol iletileri gönderilir sağlayacak sorunları ayıklama desteği. Aynı zamanda NIC için hello yeni CentOS 7 adlandırma kuralları devre dışı bırakır. Ayrıca toohello yukarıdaki, çok önerilir*kaldırmak* hello şu Parametreler:
   
        rhgb quiet crashkernel=auto
   
    Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir. Merhaba `crashkernel` seçeneği olabilir sol isterseniz yapılandırılmış, ancak Not hello küçük VM boyutlarını sorunlu olabilecek bu parametre hello hello VM tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır.

9. İşiniz bittiğinde düzenleme `/etc/default/grub` başına yukarıdaki komut toorebuild hello kaz yapılandırması aşağıdaki hello çalıştırın:
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. Merhaba görüntüden oluşturuluyorsa **VMWare, VirtualBox veya KVM:** olun hello Hyper-V sürücüleri hello initramfs eklenir:
   
   Düzen `/etc/dracut.conf`, içeriği ekleyin:
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   Merhaba initramfs yeniden oluşturun:
   
        # sudo dracut –f -v

11. Hello Azure Linux aracısı ve bağımlılıkları yükleyin:

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.
   
   Hello Azure Linux Aracısı otomatik olarak takas alanı ekli toohello VM Azure üzerinde sağladıktan sonra hello yerel kaynak diski kullanarak yapılandırabilirsiniz. Bu hello yerel kaynak diski Not bir *geçici* disk ve hello VM deprovisioned olduğunda boşaltılabilir. Yükledikten sonra Azure Linux Aracısı hello (önceki adıma bakın), parametreleri aşağıdaki hello değiştirme `/etc/waagent.conf` uygun şekilde:
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. Tıklatın **eylem -> kapatma aşağı** Hyper-V Yöneticisi'nde. Hazır toobe tooAzure karşıya artık Linux VHD olur.

## <a name="next-steps"></a>Sonraki adımlar
Artık hazır toouse, CentOS Linux sanal sabit disk toocreate yeni sanal makineleri azure'da demektir. Adım 2 ve 3'te bu hello hello .vhd dosyası tooAzure karşıya yüklüyoruz ilk kez kullanıyorsanız, bkz: [oluşturma ve hello Linux işletim sistemini içeren bir sanal sabit disk karşıya](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

