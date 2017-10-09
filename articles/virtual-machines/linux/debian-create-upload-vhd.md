---
title: aaaPrepare Debian bir Linux Azure VHD | Microsoft Docs
description: "Nasıl toocreate Debian 7 ve 8 VHD dosyalarını Azure dağıtımdaki öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: a6de7a7c-cc70-44e7-aed0-2ae6884d401a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: e67d126de3db146357a6509aedb5f478576768f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-debian-vhd-for-azure"></a>Azure için Debian VHD hazırlama
## <a name="prerequisites"></a>Ön koşullar
Bu bölümde, zaten Debian Linux işletim sistemi hello indirilen bir .iso dosyasından yüklediğinizi varsayar [Debian Web sitesi](https://www.debian.org/distrib/) tooa sanal sabit disk. Birden çok araç toocreate .vhd dosyaları var; Hyper-V yalnızca bir örnektir. Hyper-V kullanma yönergeleri için bkz: [hello Hyper-V rolünü yükleyin ve sanal makine yapılandırma](https://technet.microsoft.com/library/hh846766.aspx).

## <a name="installation-notes"></a>Yükleme notları
* Ayrıca bkz [genel Linux yükleme notları](create-upload-generic.md#general-linux-installation-notes) Linux Azure için hazırlama hakkında daha fazla ipucu için.
* Azure'da Hello yeni VHDX biçimi desteklenmiyor. Hyper-V Yöneticisi'ni veya hello kullanarak hello disk tooVHD biçimine dönüştürebilirsiniz **convert-vhd** cmdlet'i.
* Merhaba Linux sistemi yüklerken LVM (genellikle birçok yüklemeleri için hello varsayılan) yerine standart bölümlerini kullanmanız önerilir. Özellikle bir işletim sistemi herhangi bir zamanda ihtiyaçlarını bağlı toobe tooanother VM sorun giderme için disk varsa bu LVM ad çakışmalarını kopyalanan VMs önler. [LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veri disklerde tercih edilen varsa kullanılabilir.
* Bir takas bölüm hello işletim sistemi disk üzerinde yapılandırmayın. Hello Azure Linux Aracısı yapılandırılmış toocreate hello geçici kaynak disk üzerinde bir takas dosyası olabilir. Merhaba aşağıdaki adımlarda bu hakkında daha fazla bilgi bulunabilir.
* Tüm hello VHD boyutları 1 MB'ün katları olmalıdır.

## <a name="use-azure-manage-toocreate-debian-vhds"></a>Azure yönetmek toocreate Debian VHD'ler kullanın
Araçlar Azure, Debian VHD'ler gibi hello oluşturmak için kullanılabilir [azure-yönetmek](https://github.com/credativ/azure-manage) betikten [credativ](http://www.credativ.com/). Bu önerilen yaklaşımı sıfırdan bir görüntü oluşturma karşı hello olur. Örneğin, toocreate Debian 8 VHD'yi komutları toodownload azure Yönet aşağıdaki hello (ve bağımlılıklarını) çalıştırın ve hello azure_build_image betiğini çalıştırın:

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a>El ile Debian VHD hazırlama
1. Hyper-V Yöneticisi'nde hello sanal makineyi seçin.
2. Tıklatın **Bağlan** tooopen hello sanal makine için bir konsol penceresi.
3. Açıklama hello satırı çıkışı **deb cdrom** içinde `/etc/apt/source.list` hello VM ISO dosyasını karşı ayarlarsanız.
4. Merhaba Düzenle `/etc/default/grub` dosya ve hello değiştirme **GRUB_CMDLINE_LINUX** Azure için tooinclude ek çekirdek parametreleri aşağıdaki gibi parametre.
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. Merhaba kaz yeniden oluşturun ve çalıştırın:
   
        # sudo update-grub
6. Debian'ın Azure depoları too/etc/apt/sources.list Debian 7 veya 8 için ekleyin:
   
    **Wheezy debian 7.x""**
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    **Debian 8.x "Jessie"**

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. Hello Azure Linux aracısı yükleyin:
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. Debian 7 için gerekli toorun hello 3.16 tabanlı çekirdek hello backports wheezy depodan'dir. İlk /etc/apt/preferences.d/linux.pref içeriği aşağıdaki hello ile adlı bir dosya oluşturun:
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    Ardından tooinstall hello yeni çekirdek "apt sudo get yükle linux görüntü amd64" çalıştırın.
3. Merhaba sanal makine yetkisini kaldırma ve Azure üzerinde sağlamak için hazırlayın ve çalıştırın:
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. Tıklatın **eylem** Hyper-V Yöneticisi'nde kapatma aşağı ->. Hazır toobe tooAzure karşıya artık Linux VHD olur.

## <a name="next-steps"></a>Sonraki adımlar
Artık hazır toouse Debian sanal sabit disk toocreate yeni sanal makinelerinizi Azure demektir. Adım 2 ve 3'te bu hello hello .vhd dosyası tooAzure karşıya yüklüyoruz ilk kez kullanıyorsanız, bkz: [oluşturma ve hello Linux işletim sistemini içeren bir sanal sabit disk karşıya](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

