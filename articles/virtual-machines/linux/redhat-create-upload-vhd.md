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
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a>Azure için Red Hat tabanlı bir sanal makine hazırlama
Bu makalede, öğreneceksiniz nasıl tooprepare bir Red Hat Enterprise Linux (RHEL) sanal makine için Azure kullanımda. Bu makalede ele alınan hello sürümleri RHEL, 6.7 + ve 7.1 +. Bu makalede ele alınan hello hiper hazırlık için Hyper-V, çekirdek tabanlı sanal makine (KVM) ve VMware ' dir. Red Hat'ın bulut erişimi programına katılmasını için uygunluk gereksinimleri hakkında daha fazla bilgi için bkz: [Red Hat'ın bulut Access Web sitesinin](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) ve [Azure üzerinde çalışan RHEL](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a>Red Hat tabanlı sanal makineyi Hyper-V Yöneticisi'nden hazırlama

### <a name="prerequisites"></a>Ön koşullar
Bu bölümde, zaten bir ISO dosyası hello Red Hat Web sitesi ve yüklü hello RHEL görüntü tooa sanal sabit disk (VHD) aldığınız olduğunu varsayar. Nasıl hakkında daha fazla ayrıntı için toouse Hyper-V Yöneticisi'ni tooinstall bir işletim sistemi görüntüsünü görmek [hello Hyper-V rolünü yükleyin ve sanal makine yapılandırma](http://technet.microsoft.com/library/hh846766.aspx).

**RHEL yükleme notları**

* Azure hello VHDX biçimi desteklemiyor. Azure destekler, VHD yalnızca sabit. Hyper-V Yöneticisi'ni tooconvert hello disk tooVHD biçimini kullanabilirsiniz veya hello convert-vhd cmdlet'ini kullanabilirsiniz. VirtualBox kullanıyorsanız seçin **boyutu sabit** hello disk oluşturduğunuzda seçeneği dinamik olarak ayrılan olarak karşılıklı toohello varsayılan.
* Azure yalnızca 1. nesil sanal makineler destekler. 1. nesil sanal makine VHDX toohello VHD dosyası biçimi ve dinamik olarak genişletilen tooa sabit boyutlu disk dönüştürebilirsiniz. Bir sanal makinenin oluşturma değiştiremezsiniz. Daha fazla bilgi için bkz: [Hyper-V'de 1 veya 2. nesil sanal makine oluşturmalısınız?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).
* VHD hello için izin verilen en büyük boyutu hello 1,023 GB'dir.
* Merhaba Linux işletim sistemi yüklediğinizde, genellikle birçok yüklemeleri için hello varsayılan olduğu mantıksal Birimi Yöneticisi (LVM) yerine standart bölümleri kullanmanızı öneririz. Özellikle erişiminizi tooattach işletim sistemi disk tooanother özdeş bir sanal makine sorun giderme için gerekirse bu yöntem, kopyalanan sanal makineleri LVM adıyla çakışıyor kaçının. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veri diskler üzerinde kullanılabilir.
* Evrensel Disk Biçimi (UDF) dosya sistemleri bağlanması için çekirdek desteği gereklidir. Azure, hello UDF biçimli ortamının üzerinde ilk önyükleme sırasında ekli toohello Konuk hello sağlama yapılandırma toohello Linux sanal makine geçirir. Hello Azure Linux Aracısı hello sanal makine sağlama ve yapılandırmasıyla mümkün toomount hello UDF dosya sistemi tooread olmalıdır.
* Merhaba Linux çekirdek Internet Explorer'ın 2.6.37 önceki sürümlerini Tekdüzen olmayan bellek erişimi (NUMA) üzerinde Hyper-V ile daha büyük sanal makine boyutları desteklemez. Merhaba upstream kullanan eski dağıtımları Bu sorun öncelikle etkileri Red Hat 2.6.32 çekirdek ve RHEL 6.6 (çekirdek 2.6.32 504) giderilmiştir. Özel tekrar çalıştıran sistemleri 2.6.37 eski veya 2.6.32-504 eski olan RHEL tabanlı tekrar hello ayarlamalıdır `numa=off` hello çekirdek komut satırında grub.conf parametresi önyükleme. Red Hat daha fazla bilgi için bkz: [KB 436883](https://access.redhat.com/solutions/436883).
* Bir takas bölüm hello işletim sistemi disk üzerinde yapılandırmayın. Merhaba Linux Aracısı yapılandırılmış toocreate hello geçici kaynak disk üzerinde bir takas dosyası olabilir.  Aşağıdaki adımları hello bu hakkında daha fazla bilgi bulunabilir.
* Tüm VHD'leri boyutları 1 MB'ün katları olmalıdır.

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a>Hyper-V Yöneticisi'nden RHEL 6 sanal makineyi hazırlama

1. Hyper-V Yöneticisi'nde hello sanal makineyi seçin.

2. Tıklatın **Bağlan** tooopen hello sanal makine için bir konsol penceresi.

3. RHEL 6'hello Azure Linux Aracısı ile NetworkManager etkileyebilir. Merhaba aşağıdaki komutu çalıştırarak bu paketi kaldırma:
   
        # sudo rpm -e --nodeps NetworkManager

4. Oluşturma veya düzenleme hello `/etc/sysconfig/network` dosya ve metin aşağıdaki hello ekleyin:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Oluşturma veya düzenleme hello `/etc/sysconfig/network-scripts/ifcfg-eth0` dosya ve metin aşağıdaki hello ekleyin:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Merhaba udev kuralları tooavoid hello Ethernet arabirimi için statik kuralları taşıyın (veya kaldırın). Bir sanal makinede Microsoft Azure veya Hyper-V: kopyaladığınızda, bu kurallar sorunlara neden

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Merhaba ağ hizmeti önyükleme sırasında hello aşağıdaki komutu çalıştırarak başlayacağını emin olun:

        # sudo chkconfig network on

8. Red Hat abonelik tooenable hello yüklemenizin hello RHEL depodan paketler hello aşağıdaki komutu çalıştırarak kaydedin:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. Merhaba WALinuxAgent paket `WALinuxAgent-<version>`, toohello Red Hat ek özellikler deposu gönderilir. Merhaba ek özellikler depo hello aşağıdaki komutu çalıştırarak etkinleştirin:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin. toodo bu değişiklik, açık `/boot/grub/menu.lst` bir metin düzenleyicisinde ve o hello varsayılan çekirdek şu parametreler hello içerdiğinden emin olun:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, gönderilen tüm konsol iletileri sağlayacak sorunları ayıklama desteği.
    
    Ayrıca, şu parametreler hello kaldırmak önerilen:
    
        rhgb quiet crashkernel=auto
    
    Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir.  Merhaba bırakabilirsiniz `crashkernel` isterseniz yapılandırılmış seçeneği. Bu parametre hello hello sanal makine tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır unutmayın. Bu yapılandırma daha küçük sanal makine boyutlarını sorunlu olabilir.

    >[!Important]
    RHEL 6.5 ve daha önceki hello de ayarlamanız gerekir `numa=off` çekirdek parametresi. Red Hat bkz [KB 436883](https://access.redhat.com/solutions/436883).

11. Bu hello güvenli Kabuk (SSH) sunucusu yüklü ve genellikle hello varsayılandır önyükleme sırasında toostart yapılandırılmış emin olun. /Etc/ssh/sshd_config tooinclude hello aşağıdaki satırı değiştirin:

        ClientAliveInterval 180

12. Hello Azure Linux Aracısı hello aşağıdaki komutu çalıştırarak yükleyin:

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    Zaten 3. adımda kaldırılmamışsa, yükleme hello WALinuxAgent paketi hello NetworkManager ve NetworkManager gnome paketleri kaldırır.

13. Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.

    Hello Azure Linux Aracısı, Azure'da hello sanal makine sağlandıktan sonra ekli toohello sanal makine hello yerel kaynak disk kullanarak takas alanı otomatik olarak yapılandırabilirsiniz. Bu hello yerel kaynak disk geçici bir diski olduğundan ve hello sanal makine sağlaması kaldırılıyor. sağlaması zaman, boşaltılabilir olduğunu unutmayın. Merhaba önceki adımda hello Azure Linux Aracısı yüklendikten sonra /etc/waagent.conf parametrelerinde uygun şekilde aşağıdaki hello değiştirin:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. Merhaba abonelik hello aşağıdaki komutu çalıştırarak (gerekirse) kaydı:

        # sudo subscription-manager unregister

15. Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. Tıklatın **eylem** > **kapatma** Hyper-V Yöneticisi'nde. Hazır toobe tooAzure karşıya artık Linux VHD olur.


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a>Hyper-V Yöneticisi'nden RHEL 7 sanal makineyi hazırlama

1. Hyper-V Yöneticisi'nde hello sanal makineyi seçin.

2. Tıklatın **Bağlan** tooopen hello sanal makine için bir konsol penceresi.

3. Oluşturma veya düzenleme hello `/etc/sysconfig/network` dosya ve metin aşağıdaki hello ekleyin:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. Oluşturma veya düzenleme hello `/etc/sysconfig/network-scripts/ifcfg-eth0` dosya ve metin aşağıdaki hello ekleyin:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. Merhaba ağ hizmeti önyükleme sırasında hello aşağıdaki komutu çalıştırarak başlayacağını emin olun:

        # sudo chkconfig network on

6. Red Hat abonelik tooenable hello yüklemenizin hello RHEL depodan paketler hello aşağıdaki komutu çalıştırarak kaydedin:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin. toodo bu değişiklik, açık `/etc/default/grub` bir metin Düzenleyicisi'ni ve düzenleme hello `GRUB_CMDLINE_LINUX` parametresi. Örneğin:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, gönderilen tüm konsol iletileri sağlayacak sorunları ayıklama desteği. Bu yapılandırma aynı zamanda NIC için hello yeni RHEL 7 adlandırma kuralları devre dışı bırakır. Ayrıca, şu parametreler hello kaldırmanızı öneririz:
   
        rhgb quiet crashkernel=auto
   
    Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir. Merhaba bırakabilirsiniz `crashkernel` isterseniz yapılandırılmış seçeneği. Bu parametre, daha küçük sanal makine boyutlarını sorunlu olabilir hello hello sanal makine tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır unutmayın.

8. Tamamlandıktan sonra düzenleme `/etc/default/grub`çalıştırın hello komut toorebuild hello kaz yapılandırması aşağıdaki:

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. Bu hello SSH sunucusu yüklü ve genellikle hello varsayılandır önyükleme sırasında toostart yapılandırılmış emin olun. Değiştirme `/etc/ssh/sshd_config` satır aşağıdaki tooinclude hello:

        ClientAliveInterval 180

10. Merhaba WALinuxAgent paket `WALinuxAgent-<version>`, toohello Red Hat ek özellikler deposu gönderilir. Merhaba ek özellikler depo hello aşağıdaki komutu çalıştırarak etkinleştirin:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. Hello Azure Linux Aracısı hello aşağıdaki komutu çalıştırarak yükleyin:

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.

    Hello Azure Linux Aracısı, Azure'da hello sanal makine sağlandıktan sonra ekli toohello sanal makine hello yerel kaynak disk kullanarak takas alanı otomatik olarak yapılandırabilirsiniz. Merhaba yerel kaynak disk bir geçici diski olduğundan ve hello sanal makine deprovisioned olduğunda boşaltılabilir unutmayın. Parametreleri aşağıdaki hello hello önceki adımda hello Azure Linux Aracısı yüklendikten sonra değiştirmek `/etc/waagent.conf` uygun şekilde:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Toounregister hello abonelik hello aşağıdaki komutu çalıştırın:

        # sudo subscription-manager unregister

14. Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Tıklatın **eylem** > **kapatma** Hyper-V Yöneticisi'nde. Hazır toobe tooAzure karşıya artık Linux VHD olur.


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a>Red Hat tabanlı sanal makineyi KVM hazırlama
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a>KVM RHEL 6 sanal makineyi hazırlama

1. Merhaba KVM RHEL 6 görüntüsü hello Red Hat Web sitesinden indirin.

2. Bir kök parola ayarlayın.

    Şifrelenmiş bir parola oluşturmak ve hello hello komutunun çıktısını kopyalayın:

        # openssl passwd -1 changeme

    Guestfish olan bir kök parola ayarlayın:
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   Değişiklik hello ikinci alanı hello kök kullanıcıdan "!!" toohello şifrelenmiş parola.

3. Bir sanal makine içinde KVM hello qcow2 görüntüden oluşturun. Merhaba disk türü çok ayarlamak**qcow2**, hello sanal ağ arabirimi cihaz modeli çok belirlendiği**virtio**. Ardından, hello sanal makineyi başlatmak ve kök olarak oturum açın.

4. Oluşturma veya düzenleme hello `/etc/sysconfig/network` dosya ve metin aşağıdaki hello ekleyin:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Oluşturma veya düzenleme hello `/etc/sysconfig/network-scripts/ifcfg-eth0` dosya ve metin aşağıdaki hello ekleyin:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. Merhaba udev kuralları tooavoid hello Ethernet arabirimi için statik kuralları taşıyın (veya kaldırın). Bir sanal makinede Azure veya Hyper-V: kopyaladığınızda, bu kurallar sorunlara neden

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. Merhaba ağ hizmeti önyükleme sırasında hello aşağıdaki komutu çalıştırarak başlayacağını emin olun:

        # chkconfig network on

8. Red Hat abonelik tooenable hello yüklemenizin hello RHEL depodan paketler hello aşağıdaki komutu çalıştırarak kaydedin:

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin. toodo bu yapılandırma, açık `/boot/grub/menu.lst` bir metin düzenleyicisinde ve o hello varsayılan çekirdek şu parametreler hello içerdiğinden emin olun:
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, gönderilen tüm konsol iletileri sağlayacak sorunları ayıklama desteği.
    
    Ayrıca, şu parametreler hello kaldırmanızı öneririz:
    
        rhgb quiet crashkernel=auto
    
    Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir. Merhaba bırakabilirsiniz `crashkernel` isterseniz yapılandırılmış seçeneği. Bu parametre, daha küçük sanal makine boyutlarını sorunlu olabilir hello hello sanal makine tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır unutmayın.

    >[!Important]
    RHEL 6.5 ve daha önceki hello de ayarlamanız gerekir `numa=off` çekirdek parametresi. Red Hat bkz [KB 436883](https://access.redhat.com/solutions/436883).

10. Hyper-V modüllerini tooinitramfs ekleyin:  

    Düzen `/etc/dracut.conf`ve içeriği aşağıdaki hello ekleyin:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    İnitramfs yeniden oluşturun:

        # dracut -f -v

11. Bulut init kaldırın:

        # yum remove cloud-init

12. Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun:

        # chkconfig sshd on

    Satırlardan /etc/ssh/sshd_config tooinclude hello değiştirin:

        PasswordAuthentication yes
        ClientAliveInterval 180

13. Merhaba WALinuxAgent paket `WALinuxAgent-<version>`, toohello Red Hat ek özellikler deposu gönderilir. Merhaba ek özellikler depo hello aşağıdaki komutu çalıştırarak etkinleştirin:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. Hello Azure Linux Aracısı hello aşağıdaki komutu çalıştırarak yükleyin:

        # yum install WALinuxAgent

        # chkconfig waagent on

15. Hello Azure Linux Aracısı, Azure'da hello sanal makine sağlandıktan sonra ekli toohello sanal makine hello yerel kaynak disk kullanarak takas alanı otomatik olarak yapılandırabilirsiniz. Merhaba yerel kaynak disk bir geçici diski olduğundan ve hello sanal makine deprovisioned olduğunda boşaltılabilir unutmayın. Parametreleri aşağıdaki hello hello önceki adımda hello Azure Linux Aracısı yüklendikten sonra değiştirmek **/etc/waagent.conf** uygun şekilde:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Merhaba abonelik hello aşağıdaki komutu çalıştırarak (gerekirse) kaydı:

        # subscription-manager unregister

17. Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. KVM hello sanal makineyi kapatın.

19. Merhaba qcow2 görüntü toohello VHD biçimine dönüştürün.

    İlk hello görüntü tooraw biçimine dönüştürün:

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    Merhaba ham görüntü Hello boyutu 1 MB ile hizalanır emin olun. Aksi takdirde 1 MB ile Merhaba boyutu tooalign yukarı yuvarlar:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Merhaba ham disk tooa Dönüştür sabit boyutlu VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a>KVM RHEL 7 sanal makineyi hazırlama

1. Merhaba KVM RHEL 7 görüntüsü hello Red Hat Web sitesinden indirin. Bu yordamda RHEL 7 hello örnek olarak kullanılmıştır.

2. Bir kök parola ayarlayın.

    Şifrelenmiş bir parola oluşturmak ve hello hello komutunun çıktısını kopyalayın:

        # openssl passwd -1 changeme

    Guestfish olan bir kök parola ayarlayın:

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   Değişiklik hello ikinci alanı kök kullanıcıdan "!!" toohello şifrelenmiş parola.

3. Bir sanal makine içinde KVM hello qcow2 görüntüden oluşturun. Merhaba disk türü çok ayarlamak**qcow2**, hello sanal ağ arabirimi cihaz modeli çok belirlendiği**virtio**. Ardından, hello sanal makineyi başlatmak ve kök olarak oturum açın.

4. Oluşturma veya düzenleme hello `/etc/sysconfig/network` dosya ve metin aşağıdaki hello ekleyin:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. Oluşturma veya düzenleme hello `/etc/sysconfig/network-scripts/ifcfg-eth0` dosya ve metin aşağıdaki hello ekleyin:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. Merhaba ağ hizmeti önyükleme sırasında hello aşağıdaki komutu çalıştırarak başlayacağını emin olun:

        # chkconfig network on

7. Red Hat abonelik tooenable yüklemenizin hello RHEL depodan paketler hello aşağıdaki komutu çalıştırarak kaydedin:

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin. toodo bu yapılandırma, açık `/etc/default/grub` bir metin Düzenleyicisi'ni ve düzenleme hello `GRUB_CMDLINE_LINUX` parametresi. Örneğin:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Bu komut, aynı zamanda, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, gönderilen tüm konsol iletileri sağlar sorunları ayıklama desteği. Merhaba komut ayrıca NIC'ler için hello yeni RHEL 7 adlandırma kuralları devre dışı bırakır. Ayrıca, şu parametreler hello kaldırmanızı öneririz:
   
        rhgb quiet crashkernel=auto
   
    Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir. Merhaba bırakabilirsiniz `crashkernel` isterseniz yapılandırılmış seçeneği. Bu parametre, daha küçük sanal makine boyutlarını sorunlu olabilir hello hello sanal makine tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır unutmayın.

9. Tamamlandıktan sonra düzenleme `/etc/default/grub`çalıştırın hello komut toorebuild hello kaz yapılandırması aşağıdaki:

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. Hyper-V modüllerini initramfs ekleyin.

    Düzenleme `/etc/dracut.conf` ve içeriği ekleyin:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    İnitramfs yeniden oluşturun:

        # dracut -f -v

11. Bulut init kaldırın:

        # yum remove cloud-init

12. Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun:

        # systemctl enable sshd

    Satırlardan /etc/ssh/sshd_config tooinclude hello değiştirin:

        PasswordAuthentication yes
        ClientAliveInterval 180

13. Merhaba WALinuxAgent paket `WALinuxAgent-<version>`, toohello Red Hat ek özellikler deposu gönderilir. Merhaba ek özellikler depo hello aşağıdaki komutu çalıştırarak etkinleştirin:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. Hello Azure Linux Aracısı hello aşağıdaki komutu çalıştırarak yükleyin:

        # yum install WALinuxAgent

    Merhaba waagent hizmetini etkinleştirin:

        # systemctl enable waagent.service

15. Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.

    Hello Azure Linux Aracısı, Azure'da hello sanal makine sağlandıktan sonra ekli toohello sanal makine hello yerel kaynak disk kullanarak takas alanı otomatik olarak yapılandırabilirsiniz. Merhaba yerel kaynak disk bir geçici diski olduğundan ve hello sanal makine deprovisioned olduğunda boşaltılabilir unutmayın. Parametreleri aşağıdaki hello hello önceki adımda hello Azure Linux Aracısı yüklendikten sonra değiştirmek `/etc/waagent.conf` uygun şekilde:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. Merhaba abonelik hello aşağıdaki komutu çalıştırarak (gerekirse) kaydı:

        # subscription-manager unregister

17. Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. KVM hello sanal makineyi kapatın.

19. Merhaba qcow2 görüntü toohello VHD biçimine dönüştürün.

    İlk hello görüntü tooraw biçimine dönüştürün:

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    Merhaba ham görüntü Hello boyutu 1 MB ile hizalanır emin olun. Aksi takdirde 1 MB ile Merhaba boyutu tooalign yukarı yuvarlar:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Merhaba ham disk tooa Dönüştür sabit boyutlu VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a>VMware Red Hat tabanlı sanal makineyi hazırlama
### <a name="prerequisites"></a>Ön koşullar
Bu bölümde VMware RHEL sanal makine zaten yüklediğinizi varsayar. Tooinstall VMware, işletim sistemini nasıl görürüm hakkında ayrıntılar için [VMware konuk işletim sistemi Yükleme Kılavuzu](http://partnerweb.vmware.com/GOSIG/home.html).

* Merhaba Linux işletim sistemi yüklediğinizde, birçok yüklemeleri için hello varsayılan olduğu çoğunlukla LVM, yerine standart bölümleri kullanmanızı öneririz. Özellikle bir işletim sistemi diski herhangi bir zamanda bağlı toobe tooanother sanal makine sorun giderme için gerekiyorsa bu kopyalanan sanal makinenin LVM adıyla çakışıyor önler. LVM veya RAID veri disklerde tercih edilen varsa kullanılabilir.
* Bir takas bölüm hello işletim sistemi disk üzerinde yapılandırmayın. Merhaba Linux Aracısı toocreate hello geçici kaynak disk üzerinde bir takas dosyası yapılandırabilirsiniz. İzleyin hello adımlarda bu hakkında daha fazla bilgi bulabilirsiniz.
* Merhaba sanal sabit disk oluşturduğunuzda, seçin **depolama sanal diski tek bir dosya olarak**.

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a>VMware RHEL 6 sanal makineyi hazırlama
1. RHEL 6'hello Azure Linux Aracısı ile NetworkManager etkileyebilir. Merhaba aşağıdaki komutu çalıştırarak bu paketi kaldırma:
   
        # sudo rpm -e --nodeps NetworkManager

2. Adlı bir dosya oluşturun **ağ** metin aşağıdaki içeren hello/etc/sysconfig/dizininde hello:

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. Oluşturma veya düzenleme hello `/etc/sysconfig/network-scripts/ifcfg-eth0` dosya ve metin aşağıdaki hello ekleyin:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. Merhaba udev kuralları tooavoid hello Ethernet arabirimi için statik kuralları taşıyın (veya kaldırın). Bir sanal makinede Azure veya Hyper-V: kopyaladığınızda, bu kurallar sorunlara neden

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. Merhaba ağ hizmeti önyükleme sırasında hello aşağıdaki komutu çalıştırarak başlayacağını emin olun:

        # sudo chkconfig network on

6. Red Hat abonelik tooenable hello yüklemenizin hello RHEL depodan paketler hello aşağıdaki komutu çalıştırarak kaydedin:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. Merhaba WALinuxAgent paket `WALinuxAgent-<version>`, toohello Red Hat ek özellikler deposu gönderilir. Merhaba ek özellikler depo hello aşağıdaki komutu çalıştırarak etkinleştirin:

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin. toodo Bu, açık `/etc/default/grub` bir metin Düzenleyicisi'ni ve düzenleme hello `GRUB_CMDLINE_LINUX` parametresi. Örneğin:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, gönderilen tüm konsol iletileri sağlayacak sorunları ayıklama desteği. Ayrıca, şu parametreler hello kaldırmanızı öneririz:
   
        rhgb quiet crashkernel=auto
   
    Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir. Merhaba bırakabilirsiniz `crashkernel` isterseniz yapılandırılmış seçeneği. Bu parametre, daha küçük sanal makine boyutlarını sorunlu olabilir hello hello sanal makine tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır unutmayın.

9. Hyper-V modüllerini tooinitramfs ekleyin:

    Düzen `/etc/dracut.conf`ve içeriği aşağıdaki hello ekleyin:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    İnitramfs yeniden oluşturun:

        # dracut -f -v

10. Bu hello SSH sunucusu yüklü ve genellikle hello varsayılandır önyükleme sırasında toostart yapılandırılmış emin olun. Değiştirme `/etc/ssh/sshd_config` satır aşağıdaki tooinclude hello:

    ClientAliveInterval 180

11. Hello Azure Linux Aracısı hello aşağıdaki komutu çalıştırarak yükleyin:

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.

    Hello Azure Linux Aracısı, Azure'da hello sanal makine sağlandıktan sonra ekli toohello sanal makine hello yerel kaynak disk kullanarak takas alanı otomatik olarak yapılandırabilirsiniz. Merhaba yerel kaynak disk bir geçici diski olduğundan ve hello sanal makine deprovisioned olduğunda boşaltılabilir unutmayın. Parametreleri aşağıdaki hello hello önceki adımda hello Azure Linux Aracısı yüklendikten sonra değiştirmek `/etc/waagent.conf` uygun şekilde:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. Merhaba abonelik hello aşağıdaki komutu çalıştırarak (gerekirse) kaydı:

        # sudo subscription-manager unregister

14. Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. Merhaba sanal makineyi kapatın ve hello VMDK tooa .vhd dosyası dönüştürün.

    İlk hello görüntü tooraw biçimine dönüştürün:

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    Merhaba ham görüntü Hello boyutu 1 MB ile hizalanır emin olun. Aksi takdirde 1 MB ile Merhaba boyutu tooalign yukarı yuvarlar:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Merhaba ham disk tooa Dönüştür sabit boyutlu VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a>VMware RHEL 7 sanal makineyi hazırlama
1. Oluşturma veya düzenleme hello `/etc/sysconfig/network` dosya ve metin aşağıdaki hello ekleyin:
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. Oluşturma veya düzenleme hello `/etc/sysconfig/network-scripts/ifcfg-eth0` dosya ve metin aşağıdaki hello ekleyin:
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. Merhaba ağ hizmeti önyükleme sırasında hello aşağıdaki komutu çalıştırarak başlayacağını emin olun:

        # sudo chkconfig network on

4. Red Hat abonelik tooenable hello yüklemenizin hello RHEL depodan paketler hello aşağıdaki komutu çalıştırarak kaydedin:

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. Merhaba çekirdek önyükleme kaz yapılandırma tooinclude ek çekirdek parametrelerinizi satırda Azure için değiştirin. toodo bu değişiklik, açık `/etc/default/grub` bir metin Düzenleyicisi'ni ve düzenleme hello `GRUB_CMDLINE_LINUX` parametresi. Örneğin:
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   Bu yapılandırma, aynı zamanda, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, gönderilen tüm konsol iletileri sağlar sorunları ayıklama desteği. Aynı zamanda NIC için hello yeni RHEL 7 adlandırma kuralları devre dışı bırakır. Ayrıca, şu parametreler hello kaldırmanızı öneririz:
   
        rhgb quiet crashkernel=auto
   
    Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir. Merhaba bırakabilirsiniz `crashkernel` isterseniz yapılandırılmış seçeneği. Bu parametre, daha küçük sanal makine boyutlarını sorunlu olabilir hello hello sanal makine tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır unutmayın.

6. Tamamlandıktan sonra düzenleme `/etc/default/grub`çalıştırın hello komut toorebuild hello kaz yapılandırması aşağıdaki:

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. Hyper-V modüllerini tooinitramfs ekleyin.

    Düzen `/etc/dracut.conf`, içeriği ekleyin:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    İnitramfs yeniden oluşturun:

        # dracut -f -v

8. Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun. Bu ayar genellikle hello varsayılandır. Değiştirme `/etc/ssh/sshd_config` satır aşağıdaki tooinclude hello:

        ClientAliveInterval 180

9. Merhaba WALinuxAgent paket `WALinuxAgent-<version>`, toohello Red Hat ek özellikler deposu gönderilir. Merhaba ek özellikler depo hello aşağıdaki komutu çalıştırarak etkinleştirin:

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. Hello Azure Linux Aracısı hello aşağıdaki komutu çalıştırarak yükleyin:

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. Takas alanı hello işletim sistemi disk üzerinde oluşturmayın.

    Hello Azure Linux Aracısı, Azure'da hello sanal makine sağlandıktan sonra ekli toohello sanal makine hello yerel kaynak disk kullanarak takas alanı otomatik olarak yapılandırabilirsiniz. Merhaba yerel kaynak disk bir geçici diski olduğundan ve hello sanal makine deprovisioned olduğunda boşaltılabilir unutmayın. Parametreleri aşağıdaki hello hello önceki adımda hello Azure Linux Aracısı yüklendikten sonra değiştirmek `/etc/waagent.conf` uygun şekilde:

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. Toounregister hello abonelik hello aşağıdaki komutu çalıştırın:

        # sudo subscription-manager unregister

13. Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. Merhaba sanal makineyi kapatın ve hello VMDK dosya toohello VHD biçimine dönüştürün.

    İlk hello görüntü tooraw biçimine dönüştürün:

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    Merhaba ham görüntü Hello boyutu 1 MB ile hizalanır emin olun. Aksi takdirde 1 MB ile Merhaba boyutu tooalign yukarı yuvarlar:

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    Merhaba ham disk tooa Dönüştür sabit boyutlu VHD:

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a>Red Hat tabanlı sanal makineyi kickstart dosyası otomatik olarak kullanarak bir ISO hazırlama
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a>Bir kickstart dosyasından RHEL 7 sanal makineyi hazırlama

1.  İçeriği aşağıdaki hello içeren bir kickstart dosyası oluşturun ve hello dosyasını kaydedin. Merhaba kickstart yükleme hakkında daha fazla bilgi için bkz [Kickstart Yükleme Kılavuzu'na](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).

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

2. Burada hello yükleme sistem erişebildiğinizi hello kickstart dosyasını yerleştirin.

3. Hyper-V Yöneticisi'nde yeni bir sanal makine oluşturun. Merhaba üzerinde **sanal Hard diske Bağlan** sayfasında, **bir sanal sabit diski sonra Ekle**ve tam hello yeni sanal makine Sihirbazı.

4. Merhaba sanal makine ayarlarını açın:

    a.  Yeni bir sanal sabit disk toohello sanal makine ekleyin. Emin tooselect olun **VHD biçimi** ve **sabit boyutlu**.

    b.  Merhaba yükleme ISO toohello DVD sürücüsü ekleyin.

    c.  Merhaba BIOS tooboot CD'den ayarlayın.

5. Merhaba sanal makineyi başlatın. Merhaba Yükleme Kılavuzu'na göründüğünde, basın **sekmesini** tooconfigure hello önyükleme seçenekleri.

6. ENTER `inst.ks=<hello location of hello kickstart file>` sonunda hello hello önyükleme seçenekleri ve tuşuna **Enter**.

7. Merhaba yükleme toofinish bekleyin. Tamamlandığında, hello sanal makine otomatik olarak kapatılacak. Hazır toobe tooAzure karşıya artık Linux VHD olur.

## <a name="known-issues"></a>Bilinen sorunlar
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a>Merhaba Hyper-V sürücü hello başlangıç RAM diski bir Hyper-V olmayan hiper kullanırken eklenemedi

Bir Hyper-V ortamında çalıştığını Linux algılar sürece bazı durumlarda, Linux yükleyicileri hello sürücüleri için Hyper-V hello başlangıç RAM disk (initrd veya initramfs) içermeyebilir.

Farklı sanallaştırma sistem (diğer bir deyişle, Virtualbox, Xen, vb.) tooprepare Linux görüntünüzü kullanırken hv_storvsc çekirdek modülleri hello başlangıç RAM disk üzerindeki kullanılabilir ve en az hv_vmbus hello toorebuild initrd tooensure gerekebilir. Bilinen bir sorun en az hello Yukarı Akış Red Hat dağıtım noktasında tabanlı sistemlerde budur.

tooresolve Bu sorun, Hyper-V modüllerini tooinitramfs ekleyin ve onu yeniden oluşturun:

Düzen `/etc/dracut.conf`ve içeriği aşağıdaki hello ekleyin:

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

İnitramfs yeniden oluşturun:

        # dracut -f -v

Daha fazla ayrıntı için hello bilgi [initramfs yeniden](https://access.redhat.com/solutions/1958).

## <a name="next-steps"></a>Sonraki adımlar
Red Hat Enterprise Linux sanal sabit disk toocreate yeni sanal makinelerinizi Azure şimdi hazır toouse demektir. Adım 2 ve 3'te bu hello hello .vhd dosyası tooAzure karşıya yüklüyoruz ilk kez kullanıyorsanız, bkz: [oluşturma ve hello Linux işletim sistemini içeren bir sanal sabit disk karşıya](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

Red Hat Enterprise Linux toorun olan hello hiper hakkında daha fazla ayrıntı sertifikalı için bkz: [hello Red Hat Web sitesi](https://access.redhat.com/certified-hypervisors).
