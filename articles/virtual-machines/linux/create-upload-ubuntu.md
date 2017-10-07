---
title: "aaaCreate ve Azure bir Ubuntu Linux VHD karşıya yükle"
description: "Bir Azure sanal sabit bir Ubuntu Linux işletim sistemini içeren disk (VHD) yüklemek ve toocreate öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 3e097959-84fc-4f6a-8cc8-35e087fd1542
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: cc546a487f769b32432a7e80ddcd0f6af44e201f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a>Azure’da Ubuntu sanal makinesi hazırlama
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a>Resmi Ubuntu bulut görüntüleri
Ubuntu şimdi adresten resmi Azure VHD'ler yayımlar [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/). Azure için kendi özel bir Ubuntu yansıma toobuild gereksinim yerine, varsa altındaki hello el ile yordamı kullanın Bu bilinen ile önerilen toostart VHD'ler çalışma ve gerektiği gibi özelleştirin. Merhaba son görüntü yayımları her zaman aşağıdaki konumlardan hello bulunabilir:

* Ubuntu 12.04/kesin: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](https://cloud-images.ubuntu.com/precise/current/precise-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)
* Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)

## <a name="prerequisites"></a>Ön koşullar
Bu makalede, bir Ubuntu Linux işletim sistemi tooa sanal sabit diski zaten yüklemiş olduğunuz varsayılır. Birden çok araç toocreate .vhd dosyaları, örneğin bir sanallaştırma çözümü Hyper-V gibi mevcut. Yönergeler için bkz: [hello Hyper-V rolünü yükleyin ve sanal makine yapılandırma](http://technet.microsoft.com/library/hh846766.aspx).

**Ubuntu yükleme notları**

* Ayrıca bkz [genel Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes) Linux Azure için hazırlama hakkında daha fazla ipucu için.
* Merhaba VHDX biçimi, Azure'da yalnızca desteklenmiyor **VHD sabit**.  Hyper-V Yöneticisi'ni kullanarak hello disk tooVHD biçimine Dönüştür veya convert-vhd cmdlet hello.
* Merhaba Linux sistemi yüklerken LVM (genellikle birçok yüklemeleri için hello varsayılan) yerine standart bölümlerini kullanmanız önerilir. Özellikle bir işletim sistemi herhangi bir zamanda ihtiyaçlarını bağlı toobe tooanother VM sorun giderme için disk varsa bu LVM ad çakışmalarını kopyalanan VMs önler. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veri disklerde tercih edilen varsa kullanılabilir.
* Bir takas bölüm hello işletim sistemi disk üzerinde yapılandırmayın. Merhaba Linux Aracısı yapılandırılmış toocreate hello geçici kaynak disk üzerinde bir takas dosyası olabilir.  Merhaba aşağıdaki adımlarda bu hakkında daha fazla bilgi bulunabilir.
* Tüm hello VHD boyutları 1 MB'ün katları olmalıdır.

## <a name="manual-steps"></a>El ile adımlar
> [!NOTE]
> Toocreate denemeden önce kendi özel Azure, Ubuntu görüntü Lütfen düşünün hello kullanarak önceden oluşturulmuş ve test görüntülerden [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) yerine.
> 
> 

1. Merhaba Orta bölmede Hyper-V Yöneticisi'nin hello sanal makineyi seçin.

2. Tıklatın **Bağlan** tooopen hello penceresinde hello sanal makine için.

3. Merhaba geçerli depoları hello görüntü toouse Ubuntu'nın Azure depoları olarak değiştirin. Merhaba adımlar hello Ubuntu sürüm bağlı olarak biraz farklılık gösterir.
   
    Düzenleme önce `/etc/apt/sources.list`, bu yedekleme toomake önerilir:
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    Ubuntu 12.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 14.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    Ubuntu 16.04:
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. Merhaba Ubuntu Azure görüntüleri şimdi hello takip *donanım etkinleştirme* (HWE) çekirdek. Merhaba işletim sistemi toohello son çekirdek hello aşağıdaki komutları çalıştırarak güncelleştirin:

    Ubuntu 12.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    Ubuntu 14.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    Ubuntu 16.04:
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    **Ayrıca bkz.:**
    - [https://Wiki.ubuntu.com/Kernel/LTSEnablementStack](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [https://Wiki.ubuntu.com/Kernel/RollingLTSEnablementStack](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. Merhaba çekirdek önyükleme satırı kaz tooinclude ek çekirdek parametreler için Azure için değiştirin. Bu açık toodo `/etc/default/grub` adlı hello değişken bir metin düzenleyicisinde Bul `GRUB_CMDLINE_LINUX_DEFAULT` (veya gerekirse ekleyin) ve şu parametreler tooinclude hello düzenleyin:
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    Kaydet ve bu dosyayı kapatın ve ardından çalıştırın `sudo update-grub`. Bu, tüm konsol iletileri hangi sorunları ayıklama Azure teknik destek yardımcı olabilecek toohello ilk seri bağlantı noktası, gönderilen güvence altına alır.

6. Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun.  Bu genellikle hello varsayılandır.

7. Hello Azure Linux aracısı yükleyin:
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    Merhaba `walinuxagent` paketi hello kaldırmak `NetworkManager` ve `NetworkManager-gnome` yüklenmişlerse paketler.

8. Aşağıdaki komutları toodeprovision hello sanal makine hello çalıştırın ve Azure üzerinde sağlamak için hazırlayın:
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. Tıklatın **eylem -> kapatma aşağı** Hyper-V Yöneticisi'nde. Hazır toobe tooAzure karşıya artık Linux VHD olur.

## <a name="next-steps"></a>Sonraki adımlar
Artık hazır toouse Ubuntu Linux sanal sabit disk toocreate yeni sanal makinelerinizi Azure demektir. Adım 2 ve 3'te bu hello hello .vhd dosyası tooAzure karşıya yüklüyoruz ilk kez kullanıyorsanız, bkz: [oluşturma ve hello Linux işletim sistemini içeren bir sanal sabit disk karşıya](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="references"></a>Başvurular
Ubuntu donanım etkinleştirme (HWE) Çekirdek:

* [http://blog.utlemming.org/2015/01/ubuntu-1404-Azure-images-Now-Tracking.HTML](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [http://blog.utlemming.org/2015/02/1204-Azure-cloud-images-Now-using-hwe.HTML](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

