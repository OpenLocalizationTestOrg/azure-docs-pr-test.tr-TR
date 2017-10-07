---
title: aaaAttach disk tooa Azure Linux VM'de | Microsoft Docs
description: "Nasıl tooattach bir veri diski tooa Linux VM öğrenin hello Klasik dağıtım modeli kullanıp kullanıma hazır olacak şekilde hello diski başlatın"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a>Nasıl tooAttach veri diski tooa Linux sanal makine
> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Bkz. nasıl çok[hello Resource Manager dağıtım modelini kullanarak bir veri diskini](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Boş diskleri ve veri tooyour Azure Vm'leri içeren diskleri ekleyebilirsiniz. Her iki disk türleri için bir Azure depolama hesabında bulunan .vhd dosyalarıdır. Olarak tüm disk tooa Linux makine ekleme ile Merhaba disk ekledikten sonra tooinitialize gerekir ve kullanıma hazır olacak şekilde biçimlendirebilirsiniz. Bu makale ayrıntıları boş diskleri ve toothen başlatın ve yeni bir diski biçimlendirmek ne de veri tooyour VM'ler, zaten içeren diskleri ekleme.

> [!NOTE]
> Bir en iyi yöntem toouse biri olan veya daha fazla sanal makinenin veri diskleri toostore ayırın. Bir Azure sanal makine oluşturduğunuzda, bir işletim sistemi diski ve geçici bir disk vardır. **Merhaba geçici disk toostore kalıcı veri kullanmayın.** Merhaba adından da anlaşılacağı gibi yalnızca geçici depolama sağlar. Azure depolama alanında bulunan değil çünkü hiçbir artıklık veya yedekleme sunar.
> Merhaba geçici disk genellikle hello Azure Linux aracısı tarafından yönetilir ve otomatik olarak çok takılı**/mnt/kaynak** (veya **/mnt** Ubuntu görüntülerinde). Üzerindeki diğer yandan Merhaba, bir veri diski hello Linux çekirdek tarafından şöyle adlandırılabilir `/dev/sdc`, ve toopartition, gereksinim duyduğunuz biçimlendirmek ve bu kaynak bağlayın. Merhaba bkz [Azure Linux Aracısı Kullanıcı Kılavuzu] [ Agent] Ayrıntılar için.
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a>Linux içindeki yeni bir veri diski başlatın
1. SSH tooyour VM. Daha fazla bilgi için bkz: [nasıl tooa Linux çalıştıran sanal makine üzerinde toolog][Logon].
2. Ardından toofind hello cihaz tanımlayıcısı hello veri diski tooinitialize için gerekir. İki yolu toodo vardır:
   
    bir) Grep hello SCSI aygıtlar için günlüğe kaydeder, hello komut aşağıdaki gibi:
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    Yeni Ubuntu dağıtımları için toouse gerekebilir `sudo grep SCSI /var/log/syslog` çok oturum`/var/log/messages` varsayılan olarak devre dışı olabilir.
   
    Görüntülenen hello iletileri eklenen hello son veri diski hello tanıtıcısı bulabilirsiniz.
   
    ![Merhaba disk iletileri alma](./media/attach-disk/scsidisklog.png)
   
    OR
   
    b) kullanım hello `lsscsi` komutu toofind hello cihaz kimliği çıkışı. `lsscsi` ya da yüklenebilir `yum install lsscsi` (Red Hat üzerinde dağıtımları bağlı olarak) veya `apt-get install lsscsi` (Debian üzerinde dağıtımları bağlı olarak). Merhaba disk tarafından aradığınız bulabilirsiniz kendi *lun* veya **mantıksal birim numarası**. Örneğin, hello *lun* bağlı hello diskleri gelen kolayca görülebilir için `azure vm disk list <virtual-machine>` olarak:

    ```azurecli
    azure vm disk list myVM
    ```

    Merhaba çıkış benzer toohello aşağıda verilmiştir:

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    Bu verileri hello çıktısını ile karşılaştırmak `lsscsi` Merhaba aynı sanal makine örnek:
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    Merhaba son hello tuple her satırda sayısıdır hello *lun*. Bkz: `man lsscsi` daha fazla bilgi için.
3. Merhaba istemine komut toocreate aşağıdaki hello Cihazınızı yazın:
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. İstendiğinde yazın  **n**  toocreate bir bölüm.

    ![Cihaz oluşturma](./media/attach-disk/fdisknewpartition.png)

5. İstendiğinde yazın **p** toomake hello bölüm hello birincil bölüm. Tür **1** hello ilk bölüm ve ardından toomake hello silindir tooaccept hello varsayılan değer girin. Bazı sistemlerde, bu hello hello varsayılan değerleri ilk Göster ve hello silindir yerine son kesimler hello. Bu varsayılan tooaccept seçebilirsiniz.

    ![Bölümü oluşturma](./media/attach-disk/fdisknewpartdetails.png)


6. Tür **p** toosee hello bölümlenme şekli hello disk ayrıntıları.

    ![Liste disk bilgileri](./media/attach-disk/fdiskpartitiondetails.png)


7. Tür **w** hello disk için toowrite hello ayarları.

    ![Merhaba disk değişiklikleri yazma](./media/attach-disk/fdiskwritedisk.png)

8. Artık hello yeni bölüme hello dosya sistemi oluşturabilirsiniz. Merhaba bölüm numarası toohello cihaz kimliği ekleme (aşağıdaki örneğine hello içinde `/dev/sdc1`). Merhaba aşağıdaki örnekte bir ext4 bölüm üzerinde /dev/sdc1 oluşturur:
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Dosya sistemi oluştur](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > SuSE Linux Enterprise 11 sistemleri yalnızca ext4 dosya sistemleri için salt okunur erişimi de destekler. Bu sistemler için tooformat hello yeni dosya sistemi ext4 yerine ext3 olarak önerilir.

9. Dizin toomount hello yeni bir dosya sistemi, yapın:
   
    ```bash
    sudo mkdir /datadrive
    ```

10. Son olarak hello sürücü şu şekilde bağlayabilirsiniz:
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    Merhaba veri diski olduğu şimdi olarak hazır toouse **/datadrive**.
   
    ![Başlangıç dizini ve bağlama hello disketi oluşturma](./media/attach-disk/mkdirandmount.png)

11. Merhaba yeni sürücü çok/etc/fstab ekleyin:
   
    olması gereken yeniden başlatma toohello /etc/fstab dosya ekleninceye sonra tooensure hello sürücü otomatik olarak yeniden. Ayrıca, bu hello UUID (evrensel benzersiz tanıtıcı) yalnızca hello aygıt adı (yani /dev/sdc1) yerine /etc/fstab toorefer toohello sürücü kullanılır önerilir. Hello kullanarak UUID hello hatalı disk konumu hello işletim sistemi önyükleme sırasında disk hatası algılar ve ardından olan kalan olan veri disklerinin olanlar cihaz kimlikleri atanan verilen takılı tooa olan önler. toofind hello yeni sürücü UUID Merhaba, hello kullanabilirsiniz **blkid** yardımcı programı:
   
    ```bash
    sudo -i blkid
    ```
   
    Hello çıkış benzer toohello örnek aşağıdaki gibidir:
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > Yanlış hello düzenleme **/etc/fstab** dosya önyüklenemez bir sisteme neden. Emin değilseniz, bu dosyayı tooproperly düzenleme nasıl bilgi toohello dağıtım'ın belgelerine başvurun. Ayrıca, düzenlemeye başlamadan önce hello /etc/fstab dosyanızın bir yedeğini oluşturduğunuz önerilir.

    Ardından, hello'ı açmak **/etc/fstab** dosyasını bir metin düzenleyicisinde:

    ```bash
    sudo vi /etc/fstab
    ```

    Bu örnekte, hello UUID değeri Merhaba yeni kullanırız **/dev/sdc1** oluşturulduğu hello önceki adımları ve hello mountpoint aygıt **/datadrive**. Satır toohello hello sonuna aşağıdaki hello eklemek **/etc/fstab** dosyası:

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    Ya da SuSE Linux tabanlı sistemlerde toouse biraz farklı bir biçim gerekebilir:

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > Merhaba `nofail` seçeneği, VM başlatır hello dosya sistemi bozuk veya hello disk önyükleme sırasında yok olsa bile bu hello sağlar. Bu seçenek olmadan, davranış açıklandığı gibi karşılaşabilirsiniz [olamaz SSH tooLinux VM tooFSTAB hatalar nedeniyle](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).

    Merhaba dosya sistemi takılı artık test edebilirsiniz kullanılarak uygun şekilde çıkarma ve hello dosya sistemi çıkarmadan, yani hello örnek bağlama noktası `/datadrive` hello oluşturulan önceki adımları:

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    Merhaba, `mount` komutu, bir hata üretir, hello/etc/fstab doğru sözdizimi için dosyayı denetleyin. Ek veri sürücüleri veya bölümleri oluşturulduğu varsa, bunları/etc/fstab de ayrı olarak girin.

    Merhaba sürücü yazılabilir bu komutu kullanarak yapabilirsiniz:

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > Sonradan bir veri diski fstab düzenlemeden kaldırma hello VM toofail tooboot neden olabilir. Bu sık karşılaşılan bir durumdur, çoğu dağıtımları ya da hello sağlamanız `nofail` ve/veya `nobootwait` hello disk toomount önyükleme sırasında başarısız olsa bile, sistem tooboot izin fstab seçenekleri. Bu parametreler hakkında daha fazla bilgi için dağıtım ait belgelere bakın.

### <a name="trimunmap-support-for-linux-in-azure"></a>KIRPMA/UNMAP Azure Linux desteği
Bazı Linux tekrar KIRPMA/UNMAP işlemleri toodiscard destek hello diskte kullanılmayan engeller. Bu işlemler sayfaları silinmiş Azure artık geçerli değil ve iptal edilecek standart depolama tooinform öncelikle faydalıdır. Büyük dosyaları oluşturmak ve bunları silerseniz sayfaları atılıyor maliyet kaydedebilirsiniz.

Tooenable KIRPMA desteği, Linux VM'NİZDE iki yolu vardır. Her zamanki gibi dağıtımınız için önerilen yaklaşımı hello bakın:

* Kullanım hello `discard` bağlama seçeneği `/etc/fstab`, örneğin:

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* Bazı durumlarda hello içinde `discard` seçeneği performans etkileri olabilir. Alternatif olarak, hello çalıştırabilirsiniz `fstrim` komutunu el ile Merhaba komut satırından veya tooyour crontab toorun düzenli olarak ekleyin:
  
    **Ubuntu**
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    **RHEL/CentOS**
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a>Sorun giderme
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Sonraki Adımlar
Daha fazla bilgiyi aşağıdaki makaleleri hello Linux VM kullanma hakkında:

* [Nasıl toolog Linux çalıştıran tooa sanal makine üzerinde][Logon]
* [Nasıl toodetach bir Linux sanal makineden bir disk](detach-disk.md)
* [Merhaba Klasik dağıtım modeliyle Hello Azure CLI kullanma](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Azure'da bir Linux VM üzerinde RAID yapılandırın](../configure-raid.md)
* [Azure'da bir Linux VM LVM yapılandırın](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
