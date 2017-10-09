---
title: azure'da aaaIntroduction tooLinux | Microsoft Docs
description: "Linux sanal makineleri Azure üzerinde kullanma hakkında bilgi edinin."
services: virtual-machines-linux
documentationcenter: python
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: b13bf305-87bf-4df3-815e-e8f6337aa6ea
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: szark
ms.openlocfilehash: 3a931447ee23ce7000174ca314c3e10abc6b8e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toolinux-on-azure"></a>Azure ile ilgili giriş tooLinux
Bu konuda Linux sanal makineleri hello Azure bulut kullanmanın bazı yönleri genel bir bakış sağlar. Linux sanal makine dağıtma hello Galeriden bir görüntü kullanarak bir işlemdir.

## <a name="authentication-usernames-passwords-and-ssh-keys"></a>Kimlik doğrulaması: Kullanıcı adları, parolalar ve SSH anahtarları
Bir ya da kullanıcı adı tooprovide sorulur hello Azure portal kullanarak bir Linux sanal makine oluştururken ve parola veya SSH ortak anahtarı. Hello Azure Linux sanal makine dağıtmak için bir kullanıcı adı kısıtlaması aşağıdaki konu toohello seçimdir: Sistem hesaplarının adlarını (UID < 100) hello zaten mevcut sanal makine izin verilmez, 'root' örneğin.

* Bkz: [Linux çalıştıran bir sanal makine oluşturma](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Bkz: [nasıl tooUse Linux Azure üzerinde SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="obtaining-superuser-privileges-using-sudo"></a>Süper kullanıcı ayrıcalıkları kullanarak alma`sudo`
Azure üzerinde sanal makine örneği dağıtımı sırasında belirtilen hello kullanıcı hesabı ayrıcalıklı bir hesaptır. Bu hesabı hello kullanarak hello Azure Linux Aracısı toobe mümkün tooelevate ayrıcalıkları tooroot tarafından (Süper kullanıcı hesabı) yapılandırılmış `sudo` yardımcı programı. Bu kullanıcı hesabını kullanarak oturum sonra hello komut sözdizimini kullanarak kök olarak mümkün toorun komutları olacaktır:

    # sudo <COMMAND>

Kök Kabuğu'nu kullanarak isteğe bağlı olarak elde edebilirsiniz **sudo -s**.

* Bkz: [Linux sanal makineleri Azure üzerinde kök ayrıcalıkları kullanma](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="firewall-configuration"></a>Güvenlik duvarı yapılandırması
Azure hello Azure portal belirtilen bağlantı tooports kısıtlayan bir gelen paket filtresi sağlar. Varsayılan olarak, hello yalnızca izin verilen bağlantı noktası SSH şeklindedir. Hello Azure portalında uç noktaları yapılandırarak Linux sanal makinenize erişim tooadditional bağlantı noktalarını açın:

* Bkz: [nasıl tooSet yukarı uç noktaları tooa sanal makine](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

Merhaba Linux hello Azure Galerisi görüntülerinde hello getirmeyin *iptables* Güvenlik Duvarı varsayılan olarak. İsterseniz, hello güvenlik duvarı yapılandırılabilir tooprovide ek filtreleme.

## <a name="hostname-changes"></a>Ana bilgisayar adı değişiklikleri
Linux görüntü örneği başlangıçta dağıtmak için gerekli tooprovide hello sanal makine için bir konak adı olur. Merhaba sanal makine çalışmaya başladıktan sonra bu ana bilgisayar adı yayımlanan toohello platform DNS sunucuları, böylelikle birden çok sanal makineleri bağlı tooeach diğer IP adresi aramalarını ana bilgisayar adları kullanarak gerçekleştirebilirsiniz.

Bir sanal makine dağıtıldıktan sonra ana bilgisayar adı değişiklikleri isterseniz, lütfen hello komutunu kullanın

    # sudo hostname <newname>

Hello Azure Linux Aracısı işlevselliği içerir tooautomatically bu ad değişikliği algılamak uygun şekilde hello sanal makine toopersist bu değişikliği yapılandırmak ve bu değişiklik toohello platform DNS sunucularına yayımlayın.

* [Azure Linux Aracısı Kullanıcı Kılavuzu](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a>Bulut başlatma
**Ubuntu** ve **CoreOS** görüntüleri kullanan bir sanal makine önyükleme için ek özellikler sağlayan Azure ile ilgili bulut başlatma.

* [Nasıl tooInject özel veri](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Özel veri ve bulut-Init Microsoft Azure](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [Bulut Init kullanarak Azure takas bölümleri oluşturma](https://wiki.ubuntu.com/AzureSwapPartitions)
* [Nasıl tooUse CoreOS Azure ile ilgili](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a>Sanal makine görüntü yakalama
Azure görüntüye kullanılan toodeploy ek sanal makine örneklerinin sonradan olabilir hello özelliği toocapture hello var olan bir sanal makinenin durumunu sağlar. Hello Azure Linux Aracısı bazı hello sağlama işlemi sırasında gerçekleştirilen özelleştirme hello kullanılan toorollback olabilir. Bir görüntü olarak toocapture bir sanal makine hello adımları izleyebilir:

1. Çalıştırma **waagent-deprovision** tooundo özelleştirme sağlama. Veya **waagent-deprovision + kullanıcı** toooptionally sağlama ve tüm ilişkili veri sırasında belirtilen hello kullanıcı hesabı silin.
2. Aşağı/güç hello sanal makineyi kapatın.
3. Tıklatın **yakalama** hello Azure portal ya da kullanım hello PowerShell veya CLI toocapture hello sanal makinesini görüntü olarak araçları.
   
   * Bkz: [nasıl tooCapture bir şablon olarak Linux sanal makine tooUse](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="attaching-disks"></a>Diskleri ekleme
Her bir sanal makine geçici, yerel olan *kaynak disk* bağlı. Kaynak disk üzerindeki verileri yeniden başlatmalar arasında dayanıklı olmayabileceğinden, genellikle uygulama ve geçici için hello sanal makinede çalışan işlemleri tarafından kullanılır ve **geçici** depolama alanı. Ayrıca, hello işletim sistemi için kullanılan toostore hello sayfa veya takas dosya sayısıdır.

Linux üzerinde hello kaynak disk genellikle hello Azure Linux aracısı tarafından yönetilmesi ve otomatik olarak çok takılı**/mnt/kaynak** (veya **/mnt** Ubuntu görüntülerinde).

> [!NOTE]
> Bu hello kaynak diski Not bir **geçici** disk ve silinecek ve hello VM yeniden başlatıldığında yeniden biçimlendirilen.
> 
> 

Linux'ta hello veri diski hello çekirdek tarafından adlandırılabilir `/dev/sdc`, ve gereken toopartition, biçimlendirmek ve bu kaynağın bağlayın. Bu başlangıç Öğreticisi Adım adım ele alınmıştır: [nasıl tooAttach bir sanal makine veri diski tooa](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

* **Ayrıca bkz:** [yazılım RAID Linux üzerinde yapılandırma](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [LVM azure'da bir Linux VM yapılandırın](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

