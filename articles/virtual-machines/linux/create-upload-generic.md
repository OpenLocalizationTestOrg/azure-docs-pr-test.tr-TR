---
title: "aaaCreate ve azure'da bir Linux VHD karşıya yükle"
description: "Bir Azure sanal sabit Linux işletim sistemi içeren disk (VHD) yüklemek ve toocreate öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: d351396c-95a0-4092-b7bf-c6aae0bbd112
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 208e15c035edb5520fc29ba8e4e71c42b041864d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="information-for-non-endorsed-distributions"></a>Desteklenmeyen Dağıtımlarla ilgili bilgiler
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Hello Azure platformu SLA hello yalnızca bir zaman Linux işletim sistemi çalıştıran toovirtual makineler geçerlidir Merhaba, [destekli dağıtımlar](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) kullanılır. Hello Azure görüntü Galerisi sağlanan olan tüm Linux dağıtımları hello gerekli yapılandırma ile destekli dağıtımlar.

* [Azure - Linux'ta destekli dağıtımlar](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Microsoft Azure Linux görüntüleri için destek](https://support.microsoft.com/kb/2941892)

Azure üzerinde çalışan tüm dağıtımları toomeet Önkoşullar toohave hello platformda çalışması fırsat tooproperly sayısı gerekir.  Her dağıtım farklı olarak bu makalede halinde kapsamlı; ve yine gerekir tüm hello aşağıdaki ölçütlere uyan olsa bile toosignificantly hello platformda düzgün çalışır, Linux sistem tooensure ince ayar oldukça mümkündür.

Biri ile başlamanızı öneririz bu nedenle için bizim [Azure destekli dağıtımlar Linux'ta](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mümkün olduğunda. Merhaba Aşağıdaki makaleler, nasıl tooprepare hello aracılığıyla çeşitli yönlendirecek Azure üzerinde desteklenen Linux dağıtımları destekli:

* **[CentOS tabanlı dağıtımlar](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

Merhaba, bu makalenin kalanında Linux dağıtımınızı Azure üzerinde çalışan için genel rehberlik özelliklere odaklanır.

## <a name="general-linux-installation-notes"></a>Genel Linux yükleme notları
* Merhaba VHDX biçimi, Azure'da yalnızca desteklenmiyor **VHD sabit**.  Hyper-V Yöneticisi'ni kullanarak hello disk tooVHD biçimine Dönüştür veya convert-vhd cmdlet hello. VirtualBox kullanıyorsanız bu seçerek gelir **boyutu sabit** olarak hello disk oluşturulurken dinamik olarak ayrılan toohello varsayılan değil.
* Azure yalnızca 1. nesil sanal makineleri desteklemektedir. Disk 1'sanal makine VHDX toohello VHD dosyası biçimi ve dinamik olarak genişletilen tooa sabit boyutlu bir nesil dönüştürebilirsiniz. Ancak, bir sanal makinenin oluşturma değiştiremezsiniz. Daha fazla bilgi için bkz: [Hyper-V'de 1 veya 2. nesil sanal makine oluşturmalısınız?](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)
* Merhaba en büyük boyutu Merhaba VHD 1,023 GB izin verilir.
* Merhaba Linux sistemi yüklerken olan *önerilen* LVM (genellikle birçok yüklemeleri için hello varsayılan) yerine standart bölümleri kullanın. Özellikle bir işletim sistemi diski bağlı toobe tooanother hiç gerekiyorsa bu kopyalanan VM'ler LVM adıyla çakışıyor kurtulursunuz sorun giderme için aynı VM. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veri diskler üzerinde kullanılabilir.
* UDF dosya sistemleri bağlanması için çekirdek desteği gereklidir. Sağlama yapılandırma Azure hello üzerinde ilk önyükleme sırasında toohello Linux VM ekli toohello Konuk UDF biçimli ortamının geçirilir. Hello Azure Linux Aracısı yapılandırmasını mümkün toomount hello UDF dosya sistemi tooread olması gerekir ve hello VM sağlayın.
* Linux çekirdek sürümleri 2.6.37 aşağıda NUMA ile büyük VM boyutları üzerinde Hyper-V desteklemez. Eski dağıtımları hello upstream kullanarak bu sorun öncelikle etkileri Red Hat 2.6.32 çekirdek ve RHEL 6.6 (çekirdek 2.6.32 504) giderilmiştir. 2.6.32-504 ayarlamalısınız daha özel tekrar 2.6.37 eski veya tekrar eski RHEL tabanlı çalıştıran sistemlerde hello önyükleme parametresinin `numa=off` hello çekirdeğini grub.conf içinde komut satırı. Red Hat daha fazla bilgi için bkz: [KB 436883](https://access.redhat.com/solutions/436883).
* Bir takas bölüm hello işletim sistemi disk üzerinde yapılandırmayın. Merhaba Linux Aracısı yapılandırılmış toocreate hello geçici kaynak disk üzerinde bir takas dosyası olabilir.  Merhaba aşağıdaki adımlarda bu hakkında daha fazla bilgi bulunabilir.
* Tüm hello VHD boyutları 1 MB'ün katları olmalıdır.

### <a name="installing-kernel-modules-without-hyper-v"></a>Hyper-V olmadan çekirdek modülleri yükleme
Azure hello Hyper-V hiper yönetici üzerinde çalışır ve böylece Linux belirli çekirdek modülleri sipariş toorun Azure'nın yüklü olmasını gerektirir. Hyper-V dışında oluşturulmuş bir VM'niz varsa, çalışıp çalışmadığını algılar sürece hello Linux yükleyicileri hello sürücüleri Hyper-V için hello ilk ramdisk (initrd veya initramfs) içinde içeremeyen bir Hyper-V ortamı. Farklı sanallaştırma (yani Virtualbox, KVM, vb.) sistem tooprepare Linux görüntünüzü kullanırken, en az hello toorebuild hello initrd tooensure gerekebilir `hv_vmbus` ve `hv_storvsc` çekirdek modülleri hello ilk ramdisk üzerinde kullanılabilir.  Bilinen bir sorun en az hello Yukarı Akış Red Hat dağıtım noktasında tabanlı sistemlerde budur.

Merhaba initrd veya initramfs görüntüsünü yeniden oluşturma için hello mekanizması hello dağıtım bağlı olarak değişebilir. Lütfen dağıtım ait belgelere bakın veya hello uygun yordamı için destek.  İşte nasıl toorebuild hello hello kullanarak initrd için bir örnek `mkinitrd` yardımcı programı:

İlk hello varolan initrd görüntü yedekleyin:

    # cd /boot
    # sudo cp initrd-`uname -r`.img  initrd-`uname -r`.img.bak

Ardından, hello initrd hello ile yeniden `hv_vmbus` ve `hv_storvsc` çekirdek modülleri:

    # sudo mkinitrd --preload=hv_storvsc --preload=hv_vmbus -v -f initrd-`uname -r`.img `uname -r`


### <a name="resizing-vhds"></a>VHD'ler yeniden boyutlandırma
Azure üzerinde VHD görüntüleri hizalı sanal boyut too1MB olması gerekir.  Genellikle, Hyper-V kullanılarak oluşturulan VHD zaten doğru hizalanmalıdır.  Toocreate çalıştığınızda bir hata iletisi benzer toohello aşağıdaki alabilirsiniz sonra hello VHD düzgün hizalanmış değil, bir *görüntü* , VHD'den:

    "hello VHD http://<mystorageaccount>.blob.core.windows.net/vhds/MyLinuxVM.vhd has an unsupported virtual size of 21475270656 bytes. hello size must be a whole number (in MBs).”

tooremedy bu yeniden boyutlandır hello hello veya hello Hyper-V Manager konsolunu kullanarak VM [yeniden boyutlandırma VHD](http://technet.microsoft.com/library/hh848535.aspx) Powershell cmdlet'i.  Bir Windows ortamında çalıştırmıyorsanız toouse qemu img tooconvert (gerekirse) önerilir ve hello VHD yeniden boyutlandırın.

> [!NOTE]
> Qemu img sürümlerinde bilinen bir hata varsa > düzgün biçimlendirilmemiş bir VHD sonuçları 2.2.1 =. Merhaba sorunu QEMU 2.6 düzeltilmiştir. Toouse önerilen qemu img 2.2.0 veya alt ya da güncelleştirme too2.6 ya da daha yüksek. Başvuru: https://bugs.launchpad.net/qemu/+bug/1490611.
> 
> 

1. Yeniden boyutlandırma hello doğrudan gibi araçları kullanılarak VHD `qemu-img` veya `vbox-manage` önyüklenemez bir VHD neden olabilir.  Bu nedenle toofirst dönüştürme hello VHD tooa ham disk görüntüsü önerilir.  Ham disk görüntüsü (KVM gibi bazı hiper yöneticilerin hello varsayılan) olarak Hello VM görüntüsü zaten oluşturulmuşsa, bu adımı atlayın:
   
       # qemu-img convert -f vpc -O raw MyLinuxVM.vhd MyLinuxVM.raw

2. Merhaba sanal boyut hello hello disk görüntü tooensure boyutunu hizalanmış too1MB gerekli hesaplayın.  bash Kabuk betiği aşağıdaki hello bu ile yardımcı olabilir.  Merhaba betik kullanır "`qemu-img info`" toodetermine hello sanal hello disk görüntü boyutu ve hello boyutu toohello hesaplar sonraki 1 MB:
   
       rawdisk="MyLinuxVM.raw"
       vhddisk="MyLinuxVM.vhd"
   
       MB=$((1024*1024))
       size=$(qemu-img info -f raw --output json "$rawdisk" | \
              gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')
   
       rounded_size=$((($size/$MB + 1)*$MB))
       echo "Rounded Size = $rounded_size"

3. Betik yukarıdaki hello kümesinde olarak $rounded_size kullanarak hello ham disk yeniden boyutlandırma:
   
       # qemu-img resize MyLinuxVM.raw $rounded_size

4. Şimdi, hello ham disk geri tooa Dönüştür sabit boyutlu VHD:
   
       # qemu-img convert -f raw -o subformat=fixed -O vpc MyLinuxVM.raw MyLinuxVM.vhd

   Veya qemu sürümüyle **2.6 +** hello dahil `force_size` seçeneği:

       # qemu-img convert -f raw -o subformat=fixed,force_size -O vpc MyLinuxVM.raw MyLinuxVM.vhd

## <a name="linux-kernel-requirements"></a>Linux çekirdek gereksinimleri
Merhaba Hyper-V ve Microsoft Azure Linux Tümleştirme hizmetleri (LIS) sürücülerini katkısı doğrudan toohello Yukarı Akış Linux çekirdek. Yeni bir Linux çekirdek sürümü (yani 3.x) dahil birçok dağıtımları kullanılabilir bu sürücüleri zaten var veya aksi halde bu sürücüleri backported sürümleri ile bunların çekirdek sağlar.  Mümkün olduğunda toorun önerilir böylece bu sürücüleri sürekli yeni düzeltmeler ve özellikler ile Merhaba Yukarı Akış Çekirdeğinde güncelleştirilen bir [dağıtım destekli](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Bu düzeltmeler ve güncelleştirmeler içerecektir.

Bir değişken Red Hat Enterprise Linux sürümleri çalıştırıyorsanız **6.0 6.3**, Hyper-V için tooinstall hello son LIS sürücüleri gerekir. Merhaba sürücüleri bulunabilir [bu konumda](http://go.microsoft.com/fwlink/p/?LinkID=254263&clcid=0x409). RHEL itibariyle **6.4 +** (ve türevleri) hello LIS sürücüleri hello çekirdek ve bu nedenle hiçbir ek yükleme paketleri dahil zaten gerekli toorun Azure üzerinde sistemlerdir.

Özel bir çekirdek gerekiyorsa, olan daha yeni bir çekirdek sürüm toouse önerilen (yani **3.8 +**). Bu dağıtımları veya kendi çekirdek korumak satıcıları için bazı çaba gerekli tooregularly backport hello LIS sürücülerini hello Yukarı Akış çekirdek tooyour özel çekirdek olacaktır.  Nispeten yeni bir çekirdek sürümü çalışmakta olan olsa bile upstream tookeep izleme herhangi hello LIS sürücüleri ve backport olanlar gerektiğinde giderir önerilir. Merhaba hello LIS sürücü kaynak dosyalarının konumunu hello kullanılabilir [MAINTAINERS](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/MAINTAINERS) hello Linux çekirdek kaynak ağaç dosyasında:

    F:    arch/x86/include/asm/mshyperv.h
    F:    arch/x86/include/uapi/asm/hyperv.h
    F:    arch/x86/kernel/cpu/mshyperv.c
    F:    drivers/hid/hid-hyperv.c
    F:    drivers/hv/
    F:    drivers/input/serio/hyperv-keyboard.c
    F:    drivers/net/hyperv/
    F:    drivers/scsi/storvsc_drv.c
    F:    drivers/video/fbdev/hyperv_fb.c
    F:    include/linux/hyperv.h
    F:    tools/hv/

Bir çok düşük, düzeltme ekleri aşağıdaki hello hello olmaması, toocause sorunları Azure ile ilgili bilinen ve hello Çekirdeği'nde bu nedenle eklenmelidir. Bu liste halinde kapsamlı veya tüm dağıtımlar için tam verilmiştir:

* [ata_piix: varsayılan olarak diskleri toohello Hyper-V sürücüleri erteleme](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/ata/ata_piix.c?id=cd006086fa5d91414d8ff9ff2b78fbb593878e3c)
* [storvsc: hesap hello SIFIRLAMA yolundaki aktarım sırasında paketler için](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/drivers/scsi/storvsc_drv.c?id=5c1b10ab7f93d24f29b5630286e323d1c5802d5c)
* [storvsc: WRITE_SAME kullanımını kaçının](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=3e8f4f4065901c8dfc51407e1984495e1748c090)
* [storvsc: devre dışı yazma aynı RAID ve sanal ana bilgisayar bağdaştırıcısı sürücüleri](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=54b2b50c20a61b51199bedb6e5d2f8ec2568fb43)
* [storvsc: NULL işaretçiye düzeltme](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=b12bb60d6c350b348a4e1460cd68f97ccae9822e)
* [storvsc: halka arabelleği hataları g/ç dondurma neden olabilir](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/storvsc_drv.c?id=e86fb5e8ab95f10ec5f2e9430119d5d35020c951)
* [scsi_sysfs: __scsi_remove_device çift yürütme karşı koruma](https://git.kernel.org/cgit/linux/kernel/git/next/linux-next.git/commit/drivers/scsi/scsi_sysfs.c?id=be821fd8e62765de43cc4f0e2db363d0e30a7e9b)

## <a name="hello-azure-linux-agent"></a>Hello Azure Linux Aracısı
Merhaba [Azure Linux Aracısı](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (waagent) gereklidir tooproperly azure'da bir Linux sanal makine sağlama. Merhaba en son sürümünü alabilir, dosya sorunları veya hello çekme istekleri gönderme [Linux Aracısı GitHub deposuna](https://github.com/Azure/WALinuxAgent).

* Merhaba Linux Aracısı hello Apache 2.0 lisansı altında yayınlanmış. Çoğu dağıtımda zaten RPM veya deb paketleri hello aracı için sağlayın ve bu nedenle bazı durumlarda bu yüklenebilir ve çok az çaba ile güncelleştirilmiştir.
* Python v2.6 + Hello Azure Linux Aracısı gerektirir.
* Merhaba aracı ayrıca hello python pyasn1 modülü gerektirir. Çoğu dağıtımları bu yüklenebilmesi için ayrı bir paket sağlayın.
* Bazı durumlarda hello Azure Linux Aracısı ile NetworkManager uyumlu olmayabilir. Çok sayıda hello RPM/Deb paketi dağıtımları tarafından sağlanan bir çakışma toohello waagent paketi olarak NetworkManager yapılandırın ve NetworkManager hello Linux aracı paketi yüklediğinizde, bu nedenle kaldırır.

## <a name="general-linux-system-requirements"></a>Genel Linux sistem gereksinimleri

* Merhaba çekirdek önyükleme şu parametreler kaz veya GRUB2 tooinclude hello satırda değiştirin. Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, tüm konsol iletileri gönderilir sağlayacak sorunları ayıklama desteği:
  
        console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300
  
    Bu, Azure yardımcı olabilecek toohello ilk seri bağlantı noktasına, tüm konsol iletileri gönderilir sağlayacak sorunları ayıklama desteği.
  
    Ayrıca toohello yukarıdaki, çok önerilir*kaldırmak* varsa şu parametreler hello:
  
        rhgb quiet crashkernel=auto
  
    Grafik ve sessiz önyükleme toohello seri bağlantı noktasına gönderilen tüm hello günlükleri toobe burada istiyoruz bulut ortamında yararlı değildir. Merhaba `crashkernel` seçeneği olabilir sol isterseniz yapılandırılmış, ancak Not hello küçük VM boyutlarını sorunlu olabilecek bu parametre hello hello VM tarafından 128 MB veya daha fazla kullanılabilir bellek miktarını azaltır.

* Hello Azure Linux Aracısı yükleme
  
    Hello Azure Linux Aracısı, Azure Linux görüntüde sağlamak için gereklidir.  Çoğu dağıtımda hello Aracısı RPM ya da Deb bir paket olarak sağlayın (Merhaba paket genellikle 'WALinuxAgent' veya 'walinuxagent' denir).  Merhaba aracı da el ile Merhaba hello adımları izleyerek yüklenebilir [Linux Aracısı Kılavuzu](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

* Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun.  Bu genellikle hello varsayılandır.

* Takas alanı hello işletim sistemi disk üzerinde oluşturma
  
    Hello Azure Linux Aracısı otomatik olarak takas alanı ekli toohello VM Azure üzerinde sağladıktan sonra hello yerel kaynak diski kullanarak yapılandırabilirsiniz. Bu hello yerel kaynak diski Not bir *geçici* disk ve hello VM deprovisioned olduğunda boşaltılabilir. Yükledikten sonra Azure Linux Aracısı hello (önceki adıma bakın), /etc/waagent.conf parametrelerinde uygun şekilde aşağıdaki hello değiştirin:
  
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

* Son adım olarak, aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın:
  
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
  
  > [!NOTE]
  > Üzerinde VirtualBox çalıştırdıktan sonra aşağıdaki hata hello görebilirsiniz ' waagent-force - deprovision': `[Errno 5] Input/output error`. Bu hata iletisini kritik değildir ve göz ardı edilebilir.
  > 
  > 

* Ardından hello sanal makine aşağı tooshut ihtiyacınız ve hello VHD tooAzure yükleyin.

