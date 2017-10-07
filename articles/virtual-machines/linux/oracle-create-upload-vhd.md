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
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a>Azure için Oracle Linux sanal makinesi hazırlama
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Ön koşullar
Bu makalede, bir Oracle Linux işletim sistemi tooa sanal sabit diski zaten yüklemiş olduğunuz varsayılır. Birden çok araç toocreate .vhd dosyaları, örneğin bir sanallaştırma çözümü Hyper-V gibi mevcut. Yönergeler için bkz: [hello Hyper-V rolünü yükleyin ve sanal makine yapılandırma](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="oracle-linux-installation-notes"></a>Oracle Linux yükleme notları
* Ayrıca bkz [genel Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes) Linux Azure için hazırlama hakkında daha fazla ipucu için.
* Oracle'nın Red Hat uyumlu çekirdek ve bunların UEK3 (kesilemeyen kurumsal çekirdek) hem de Hyper-V ve Azure üzerinde desteklenir. En iyi sonuçlar için Oracle Linux VHD hazırlanırken emin tooupdate toohello son çekirdek Lütfen olabilir.
* Merhaba gerekli sürücüleri içermez gibi oracle'nın UEK2 Hyper-V ve Azure üzerinde desteklenmiyor.
* Merhaba VHDX biçimi, Azure'da yalnızca desteklenmiyor **VHD sabit**.  Hyper-V Yöneticisi'ni kullanarak hello disk tooVHD biçimine Dönüştür veya convert-vhd cmdlet hello.
* Merhaba Linux sistemi yüklerken LVM (genellikle birçok yüklemeleri için hello varsayılan) yerine standart bölümlerini kullanmanız önerilir. Özellikle bir işletim sistemi herhangi bir zamanda ihtiyaçlarını bağlı toobe tooanother VM sorun giderme için disk varsa bu LVM ad çakışmalarını kopyalanan VMs önler. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veri disklerde tercih edilen varsa kullanılabilir.
* NUMA Linux çekirdeği sürümlerinde 2.6.37 aşağıda tooa hata nedeniyle daha büyük VM boyutları için desteklenmiyor. Bu sorun öncelikle kullanarak dağıtımları hello Yukarı Akış kırmızı etkileri Hat 2.6.32 çekirdek. Hello Azure Linux Aracısı'nı (waagent) el ile yükleme otomatik olarak NUMA yapılandırmasında hello kaz hello Linux çekirdek devre dışı bırakır. Merhaba aşağıdaki adımlarda bu hakkında daha fazla bilgi bulunabilir.
* Bir takas bölüm hello işletim sistemi disk üzerinde yapılandırmayın. Merhaba Linux Aracısı yapılandırılmış toocreate hello geçici kaynak disk üzerinde bir takas dosyası olabilir.  Merhaba aşağıdaki adımlarda bu hakkında daha fazla bilgi bulunabilir.
* Tüm hello VHD boyutları 1 MB'ün katları olmalıdır.
* Bu hello emin olun `Addons` depo etkindir. Merhaba dosyasını düzenleyin `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) veya `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux) hello satır değiştirip `enabled=0` çok`enabled=1` altında **[ol6_addons]** veya **[ol7_addons]** bu dosya.

## <a name="oracle-linux-64"></a>Oracle Linux 6.4 +
Merhaba işletim sistemi azure'da hello sanal makine toorun için belirli yapılandırma adımları tamamlamanız gerekir.

1. Merhaba Orta bölmede Hyper-V Yöneticisi'nin hello sanal makineyi seçin.
2. Tıklatın **Bağlan** tooopen hello penceresinde hello sanal makine için.
3. NetworkManager hello aşağıdaki komutu çalıştırarak kaldırın:
   
        # sudo rpm -e --nodeps NetworkManager
   
    **Not:** hello paket zaten yüklü değilse, bu komutu bir hata iletisiyle başarısız olur. Bu beklenen bir durumdur.
4. Adlı bir dosya oluşturun **ağ** hello içinde `/etc/sysconfig/` metin aşağıdaki hello içeren dizini:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. Adlı bir dosya oluşturun **ifcfg eth0** hello içinde `/etc/sysconfig/network-scripts/` metin aşağıdaki hello içeren dizini:
   
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
   
        # chkconfig network on
8. Python pyasn1 hello aşağıdaki komutu çalıştırarak yükleyin:
   
        # sudo yum install python-pyasn1
9. Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin. Bu açık toodo "/ boot/grub/menu.lst" bir metin düzenleyicisinde ve o hello varsayılan çekirdek şu parametreler hello içerdiğinden emin olun:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, tüm konsol iletileri gönderilir sağlayacak sorunları ayıklama desteği. Bu NUMA Oracle'nın Red Hat uyumlu çekirdek tooa hata nedeniyle devre dışı bırakır.
   
   Ayrıca toohello yukarıdaki, çok önerilir*kaldırmak* hello şu Parametreler:
   
        rhgb quiet crashkernel=auto
   
   Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir.
   
   Merhaba `crashkernel` seçeneği olabilir sol isterseniz yapılandırılmış, ancak Not hello küçük VM boyutlarını sorunlu olabilecek bu parametre hello hello VM tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır.
10. Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun.  Bu genellikle hello varsayılandır.
11. Merhaba aşağıdaki komutu çalıştırarak Hello Azure Linux aracısı yükleyin. Merhaba en son sürüm 2.0.15 ' dir.
    
        # sudo yum install WALinuxAgent
    
    Yükleme hello WALinuxAgent paketi hello NetworkManager kaldırır ve bunlar zaten açıklandığı gibi kaldırılmamışsa, NetworkManager gnome paketleri 2. adımda not edin.
12. Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.
    
    Hello Azure Linux Aracısı otomatik olarak takas alanı ekli toohello VM Azure üzerinde sağladıktan sonra hello yerel kaynak diski kullanarak yapılandırabilirsiniz. Bu hello yerel kaynak diski Not bir *geçici* disk ve hello VM deprovisioned olduğunda boşaltılabilir. Yükledikten sonra Azure Linux Aracısı hello (önceki adıma bakın), /etc/waagent.conf parametrelerinde uygun şekilde aşağıdaki hello değiştirin:
    
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

- - -
## <a name="oracle-linux-70"></a>Oracle Linux 7.0 +
**Oracle Linux 7 değişiklikleri**

Bir Oracle Linux 7 sanal makine için Azure hazırlanıyor çok benzer tooOracle Linux 6, ancak eşitlenmeyeceği birkaç önemli farklılıklar vardır şöyledir:

* Azure'da hello Red Hat uyumlu çekirdek ve Oracle'nın UEK3 desteklenir.  Merhaba UEK3 çekirdek önerilir.
* Merhaba NetworkManager paketi artık hello Azure Linux Aracısı ile çakışıyor. Bu paketi varsayılan olarak yüklenir ve onu kaldırılmaz öneririz.
* GRUB2 şimdi varsayılan önyükleme yükleyicisi, çekirdek parametreleri düzenlemek için hello yordamı (aşağıya bakın) değişti şekilde hello olarak kullanılır.
* XFS hello varsayılan dosya sistemi sunulmuştur. Merhaba ext4 dosya sistemi hala isterseniz kullanılabilir.

**Yapılandırma adımları**

1. Hyper-V Yöneticisi'nde hello sanal makineyi seçin.
2. Tıklatın **Bağlan** tooopen hello sanal makine için bir konsol penceresi.
3. Adlı bir dosya oluşturun **ağ** hello içinde `/etc/sysconfig/` metin aşağıdaki hello içeren dizini:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. Adlı bir dosya oluşturun **ifcfg eth0** hello içinde `/etc/sysconfig/network-scripts/` metin aşağıdaki hello içeren dizini:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. Udev kuralları tooavoid hello Ethernet arabirimi için statik kuralları oluşturma değiştirin. Bu kurallar, bir sanal makinede Microsoft Azure veya Hyper-V: kopyalarken sorunlara neden olabilir
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. Merhaba ağ hizmetini hello aşağıdaki komutu çalıştırarak önyükleme sırasında başlatacak emin olun:
   
        # sudo chkconfig network on
7. Merhaba aşağıdaki komutu çalıştırarak Hello pyasn1 python paketini yükle:
   
        # sudo yum install python-pyasn1
8. Aşağıdaki komut tooclear hello geçerli yum meta hello çalıştırın ve tüm güncelleştirmeleri yükleyin:
   
        # sudo yum clean all
        # sudo yum -y update
9. Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin. Bu açık "/ etc/varsayılan/kaz" toodo bir metin düzenleyicisi ve düzenleme hello içinde `GRUB_CMDLINE_LINUX` parametresi, örneğin:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, tüm konsol iletileri gönderilir sağlayacak sorunları ayıklama desteği. Aynı zamanda NIC için hello yeni OEL 7 adlandırma kuralları devre dışı bırakır. Ayrıca toohello yukarıdaki, çok önerilir*kaldırmak* hello şu Parametreler:
   
       rhgb quiet crashkernel=auto
   
   Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir.
   
   Merhaba `crashkernel` seçeneği olabilir sol isterseniz yapılandırılmış, ancak Not hello küçük VM boyutlarını sorunlu olabilecek bu parametre hello hello VM tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır.
10. Tamamladıktan sonra düzenleme "/ etc/varsayılan/kaz" başına yukarıdaki komut toorebuild hello kaz yapılandırması aşağıdaki hello çalıştırın:
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun.  Bu genellikle hello varsayılandır.
12. Hello Azure Linux Aracısı hello aşağıdaki komutu çalıştırarak yükleyin:
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.
    
    Hello Azure Linux Aracısı otomatik olarak takas alanı ekli toohello VM Azure üzerinde sağladıktan sonra hello yerel kaynak diski kullanarak yapılandırabilirsiniz. Bu hello yerel kaynak diski Not bir *geçici* disk ve hello VM deprovisioned olduğunda boşaltılabilir. Yükledikten sonra Azure Linux Aracısı hello (Merhaba önceki adıma bakın), /etc/waagent.conf parametrelerinde uygun şekilde aşağıdaki hello değiştirin:
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. Tıklatın **eylem -> kapatma aşağı** Hyper-V Yöneticisi'nde. Hazır toobe tooAzure karşıya artık Linux VHD olur.

## <a name="next-steps"></a>Sonraki adımlar
Artık hazır toouse, Oracle Linux .vhd toocreate yeni sanal makineleri azure'da demektir. Adım 2 ve 3'te bu hello hello .vhd dosyası tooAzure karşıya yüklüyoruz ilk kez kullanıyorsanız, bkz: [oluşturma ve hello Linux işletim sistemini içeren bir sanal sabit disk karşıya](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

