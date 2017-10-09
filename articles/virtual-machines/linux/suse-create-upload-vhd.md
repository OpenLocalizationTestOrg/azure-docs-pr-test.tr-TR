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
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a>Azure için SLES veya openSUSE sanal makinesi hazırlama
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a>Ön koşullar
Bu makale, zaten bir SUSE ya da Linux işletim sistemi tooa sanal sabit disk openSUSE yüklediğinizi varsayar. Birden çok araç toocreate .vhd dosyaları, örneğin bir sanallaştırma çözümü Hyper-V gibi mevcut. Yönergeler için bkz: [hello Hyper-V rolünü yükleyin ve sanal makine yapılandırma](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="sles--opensuse-installation-notes"></a>SLES / openSUSE yükleme notları
* Ayrıca bkz [genel Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes) Linux Azure için hazırlama hakkında daha fazla ipucu için.
* Merhaba VHDX biçimi, Azure'da yalnızca desteklenmiyor **VHD sabit**.  Hyper-V Yöneticisi'ni kullanarak hello disk tooVHD biçimine Dönüştür veya convert-vhd cmdlet hello.
* Merhaba Linux sistemi yüklerken LVM (genellikle birçok yüklemeleri için hello varsayılan) yerine standart bölümlerini kullanmanız önerilir. Özellikle bir işletim sistemi herhangi bir zamanda ihtiyaçlarını bağlı toobe tooanother VM sorun giderme için disk varsa bu LVM ad çakışmalarını kopyalanan VMs önler. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veri disklerde tercih edilen varsa kullanılabilir.
* Bir takas bölüm hello işletim sistemi disk üzerinde yapılandırmayın. Merhaba Linux Aracısı yapılandırılmış toocreate hello geçici kaynak disk üzerinde bir takas dosyası olabilir.  Merhaba aşağıdaki adımlarda bu hakkında daha fazla bilgi bulunabilir.
* Tüm hello VHD boyutları 1 MB'ün katları olmalıdır.

## <a name="use-suse-studio"></a>SUSE Studio'yu kullanın
[SUSE Studio](http://www.susestudio.com) kolayca oluşturabilir ve SLES ve openSUSE görüntülerinizi Azure ve Hyper-V için yönetebilirsiniz. Bu önerilen yaklaşımı kendi SLES ve openSUSE görüntülerini özelleştirme hello olur.

Bir alternatif toobuilding kendi VHD, SUSE de yayımlar BYOS (Getir bilgisayarınızı kendi abonelik) görüntüleri SLES için [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a>SUSE Linux Enterprise Server 11 SP4 hazırlama
1. Merhaba Orta bölmede Hyper-V Yöneticisi'nin hello sanal makineyi seçin.
2. Tıklatın **Bağlan** tooopen hello penceresinde hello sanal makine için.
3. SUSE Linux Enterprise sistem tooallow kaydetmek, toodownload güncelleştirmeleri ve yükleme paketleri.
4. Merhaba sistem hello en son düzeltme eki ile güncelleştirin:
   
        # sudo zypper update
5. Hello Azure Linux Aracısı hello SLES depodan yükleyin:
   
        # sudo zypper install WALinuxAgent
6. İçinde chkconfig waagent çok "açık" ayarlanmış olup olmadığını denetleyin ve aksi durumda, için AutoStart'ı etkinleştirin:
   
        # sudo chkconfig waagent on
7. Waagent hizmeti çalıştıran ve aksi durumda, başlatın kontrol edin: 
   
        # sudo service waagent start
8. Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin. Bu açık toodo "/ boot/grub/menu.lst" bir metin düzenleyicisinde ve o hello varsayılan çekirdek şu parametreler hello içerdiğinden emin olun:
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, tüm konsol iletileri gönderilir sağlayacak sorunları ayıklama desteği.
9. Bu /boot/grub/menu.lst ve/etc/fstab hello disk kimliği (kimliğine göre) yerine kendi UUID (UUID tarafından) kullanarak her iki başvuru hello disk onaylayın. 
   
    Disk UUID'si Al
   
        # ls /dev/disk/by-uuid/
   
    Varsa /dev/disk/by-id / kullanılan, /boot/grub/menu.lst hem/etc/fstab hello UUID tarafından uygun değeri ile güncelleştirme
   
    Değişiklikten önce
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    Değişiklikten sonra
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. Udev kuralları tooavoid hello Ethernet arabirimi için statik kuralları oluşturma değiştirin. Bu kurallar, bir sanal makinede Microsoft Azure veya Hyper-V: kopyalarken sorunlara neden olabilir
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. Tooedit hello dosya önerilir "/ etc/sysconfig/ağ/dhcp" Merhaba değiştirip `DHCLIENT_SET_HOSTNAME` parametresi toohello aşağıdaki:
    
     DHCLIENT_SET_HOSTNAME = "Hayır"
12. "/ Etc/sudoers", çıkışı yorum yapmak veya varsa satırlardan hello kaldırın:
    
     Varsayılan olarak targetpw # isteyin hello hello hedef kullanıcı yani tüm ALL=(ALL) tüm kök parolasını # uyarı! Yalnızca bu 'Varsayılanları targetpw' ile birlikte kullanın!
13. Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun.  Bu genellikle hello varsayılandır.
14. Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.
    
    Hello Azure Linux Aracısı otomatik olarak takas alanı ekli toohello VM Azure üzerinde sağladıktan sonra hello yerel kaynak diski kullanarak yapılandırabilirsiniz. Bu hello yerel kaynak diski Not bir *geçici* disk ve hello VM deprovisioned olduğunda boşaltılabilir. Yükledikten sonra Azure Linux Aracısı hello (önceki adıma bakın), /etc/waagent.conf parametrelerinde uygun şekilde aşağıdaki hello değiştirin:
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Not: ihtiyacınız onu toobe bu toowhatever ayarlayın.
15. Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo waagent-force - deprovision
    # <a name="export-histsize0"></a>HISTSIZE ver = 0
    # <a name="logout"></a>oturum kapatma
16. Tıklatın **eylem -> kapatma aşağı** Hyper-V Yöneticisi'nde. Hazır toobe tooAzure karşıya artık Linux VHD olur.

- - -
## <a name="prepare-opensuse-131"></a>OpenSUSE 13,1 + hazırlama
1. Merhaba Orta bölmede Hyper-V Yöneticisi'nin hello sanal makineyi seçin.
2. Tıklatın **Bağlan** tooopen hello penceresinde hello sanal makine için.
3. Hello kabuğu, hello komutu Çalıştır '`zypper lr`'. Bu komut döndürürse hello depoları beklenen--ayarlama yapılmayan gerekli olarak yapılandırılan sonra aşağıdaki benzer toohello (sürüm numaraları değişebilir unutmayın) çıktı:
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    Merhaba komut "depoları tanımlanan..." döndürürse komutları tooadd aşağıdaki hello bu depoları kullanın:
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    Ardından hello depoları eklendi hello komutunu çalıştırarak doğrulayabilirsiniz '`zypper lr`' yeniden. Merhaba ilgili güncelleştirme depoları birini etkin durumda aşağıdaki komutla etkinleştirin:
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. Merhaba çekirdek toohello en son sürüme güncelleştirin:
   
        # sudo zypper up kernel-default
   
    Veya tüm hello en son düzeltme eklerinin tooupdate hello sistemiyle:
   
        # sudo zypper update
5. Hello Azure Linux aracısı yükleyin.
   
   # <a name="sudo-zypper-install-walinuxagent"></a>sudo zypper yükleme WALinuxAgent
6. Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin. toodo Bu, Aç "/ boot/grub/menu.lst" bir metin düzenleyicisinde ve o hello varsayılan çekirdek şu parametreler hello içerdiğinden emin olun:
   
     Konsol ttyS0 earlyprintk = ttyS0 rootdelay = 300 =
   
   Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, tüm konsol iletileri gönderilir sağlayacak sorunları ayıklama desteği. Ayrıca, varsa şu parametreler hello çekirdek önyükleme satırından hello kaldırın:
   
     libata.atapi_enabled=0 ayırma 0x1f0, = 0x8
7. Tooedit hello dosya önerilir "/ etc/sysconfig/ağ/dhcp" Merhaba değiştirip `DHCLIENT_SET_HOSTNAME` parametresi toohello aşağıdaki:
   
     DHCLIENT_SET_HOSTNAME = "Hayır"
8. **Önemli:** "/ etc/sudoers", çıkışı açıklama veya varsa satırlardan hello kaldırın:
   
     Varsayılan olarak targetpw # isteyin hello hello hedef kullanıcı yani tüm ALL=(ALL) tüm kök parolasını # uyarı! Yalnızca bu 'Varsayılanları targetpw' ile birlikte kullanın!
9. Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun.  Bu genellikle hello varsayılandır.
10. Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.
    
    Hello Azure Linux Aracısı otomatik olarak takas alanı ekli toohello VM Azure üzerinde sağladıktan sonra hello yerel kaynak diski kullanarak yapılandırabilirsiniz. Bu hello yerel kaynak diski Not bir *geçici* disk ve hello VM deprovisioned olduğunda boşaltılabilir. Yükledikten sonra Azure Linux Aracısı hello (önceki adıma bakın), /etc/waagent.conf parametrelerinde uygun şekilde aşağıdaki hello değiştirin:
    
     ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Not: ihtiyacınız onu toobe bu toowhatever ayarlayın.
11. Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:
    
    # <a name="sudo-waagent--force--deprovision"></a>sudo waagent-force - deprovision
    # <a name="export-histsize0"></a>HISTSIZE ver = 0
    # <a name="logout"></a>oturum kapatma
12. Başlangıçta Azure Linux Aracısı çalıştıran hello emin olun:
    
        # sudo systemctl enable waagent.service
13. Tıklatın **eylem -> kapatma aşağı** Hyper-V Yöneticisi'nde. Hazır toobe tooAzure karşıya artık Linux VHD olur.

## <a name="next-steps"></a>Sonraki adımlar
Artık hazır toouse SUSE Linux sanal sabit disk toocreate yeni sanal makinelerinizi Azure demektir. Adım 2 ve 3'te bu hello hello .vhd dosyası tooAzure karşıya yüklüyoruz ilk kez kullanıyorsanız, bkz: [oluşturma ve hello Linux işletim sistemini içeren bir sanal sabit disk karşıya](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

