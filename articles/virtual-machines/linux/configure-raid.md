---
title: "aaaConfigure yazılım RAID Linux çalıştıran bir sanal makinede | Microsoft Docs"
description: "Nasıl toouse mdadm tooconfigure RAID Linux Azure üzerinde öğrenin."
services: virtual-machines-linux
documentationcenter: na
author: rickstercdn
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: f3cb2786-bda6-4d2c-9aaf-2db80f490feb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: rclaus
ms.openlocfilehash: f06e2679d953faf88ffee9991226cdb3cc1cbdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-software-raid-on-linux"></a>Linux’ta Yazılım RAID yapılandırma
Yaygın bir senaryo toouse yazılım RAID Linux sanal makinelerde tek bir RAID aygıt olarak birden çok ekli veri diskleri Azure toopresent ayarlanır. Genellikle bu kullanılan tooimprove performans ve işleme toousing yalnızca tek bir disk karşılaştırıldığında geliştirilmiş için izin verebilirsiniz.

## <a name="attaching-data-disks"></a>Veri diskleri ekleme
İki veya daha fazla boş veri diskleri gerekli tooconfigure RAID aygıtı içindir.  RAID aygıtı oluşturmak için hello birincil tooimprove, disk g/ç performansını nedenidir.  G/ç gereksinimlerinize bağlı olarak, standart bizim depolama biriminde, too500 GÇ/ps disk veya too5000 GÇ/ps disk başına yukarı bizim Premium storage ile başına yukarı ile depolanan tooattach diskleri seçebilirsiniz. Bu makalede nasıl ayrıntıya geçmez tooprovision ve veri diskleri tooa Linux sanal makine ekleyin.  Bkz: hello Microsoft Azure makale [bir diski kullanıma açın](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) nasıl tooattach boş bir veri diski tooa Linux sanal makine Azure ile ilgili ayrıntılı yönergeler için.

## <a name="install-hello-mdadm-utility"></a>Merhaba mdadm yardımcı programını yükleyin
* **Ubuntu**
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* **CentOS & Oracle Linux**
```bash
sudo yum install mdadm
```

* **SLES ve openSUSE**
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a>Merhaba disk bölümleri oluşturma
Bu örnekte, /dev/sdc üzerinde tek disk bölümü oluşturuyoruz. Merhaba yeni disk bölümü /dev/sdc1 çağrılır.

1. Başlat `fdisk` toobegin bölümleri oluşturma

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide toowrite them.
    After that, of course, hello previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off hello mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. Tuşuna 'n' hello komut istemi toocreate konumunda bir  **n** eni bölüm:

    ```bash
    Command (m for help): n
    ```

3. Ardından, 'p' toocreate'e basın bir **p**birincil bölüm:

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. '1' tooselect bölüm numarası 1 tuşuna basın:

    ```bash
    Partition number (1-4): 1
    ```

5. Select hello hello yeni bölüm basın veya başlangıç noktası `<enter>` tooaccept hello varsayılan tooplace hello bölüm hello başında hello hello sürücüdeki boş disk alanı:

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. Merhaba bölümü, örneğin türü '+10G' toocreate 10 gigabayt bölüm Hello boyutunu seçin. Veya basın `<enter>` hello sürücünün tamamını kapsayan tek bir bölüm oluşturun:

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. Ardından, hello Kimliğini değiştirin ve **t**türü hello varsayılan hello bölümünün Kimliği '83' (Linux) tooID 'fd' (Linux RAID otomatik):

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. Son olarak, hello bölüm tablo toohello sürücüsü yazmak ve fdisk Çık:

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a>Merhaba RAID dizisi oluşturma
1. Aşağıdaki örnek "stripe üç bölüm üç ayrı veri disk üzerinde (sdc1, sdd1, sde1) bulunan" (RAID Düzey 0) hello.  Adlı yeni bir RAID cihaz bu komutu çalıştırdıktan sonra **/dev/md127** oluşturulur. Ayrıca bu veri diskleri, biz daha önce başka bir geçersiz RAID dizisi parçası, gerekli tooadd hello olabileceğine dikkat edin `--force` parametresi toohello `mdadm` komutu:

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. Merhaba yeni RAID aygıtta Hello dosya sistemi oluşturma
   
    a. **CentOS, Oracle Linux SLES 12, openSUSE ve Ubuntu**

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    b. **SLES 11**

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    c. **SLES 11** - boot.md etkinleştirmek ve mdadm.conf oluşturma

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > SUSE sistemlerde bu değişiklikleri yaptıktan sonra bir yeniden başlatma gerekli olabilir. Bu adım *değil* SLES 12 gerekli.
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a>Merhaba yeni dosya sistemi çok/etc/fstab Ekle
> [!IMPORTANT]
> Yanlış hello /etc/fstab dosyasını düzenleyerek önyüklenemez bir sisteme neden olabilir. Emin değilseniz, bu dosyayı tooproperly düzenleme nasıl bilgi toohello dağıtım'ın belgelerine başvurun. Ayrıca, düzenlemeye başlamadan önce hello /etc/fstab dosyanızın bir yedeğini oluşturduğunuz önerilir.

1. Örneğin, yeni bir dosya sistemi için istenen hello bağlama noktası oluşturun:

    ```bash
    sudo mkdir /data
    ```
2. /Etc/fstab düzenlerken hello **UUID** kullanılan tooreference hello dosya hello yerine sistem aygıt adı olmalıdır.  Kullanım hello `blkid` yardımcı programı toodetermine hello UUID hello yeni dosya sistemi için:

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. /Etc/fstab bir metin düzenleyicisinde açın ve örneğin hello yeni dosya sistemi için bir giriş ekleyin:

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    Veya **SLES 11**:

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    Ardından, kaydedin ve /etc/fstab kapatın.

4. Bu hello/etc test/fstab girişi doğrudur:

    ```bash  
    sudo mount -a
    ```

    Lütfen bu komutu bir hata iletisi sonuçlanırsa hello /etc/fstab dosyasında hello sözdizimini denetleyin.
   
    Merhaba sonraki çalıştırma `mount` komutu tooensure hello dosya sistemi takılı:

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. (İsteğe bağlı) Hatasız önyükleme parametreleri
   
    **fstab yapılandırma**
   
    Çoğu dağıtımda ya da hello dahil `nobootwait` veya `nofail` fstab toohello/etc/dosya eklenebilir parametreleri bağlayın. Bu parametreleri oluşturulamıyor tooproperly bağlama hello RAID dosya sistemi olsa bile hello Linux sistem toocontinue tooboot izin ve hataları için belirli dosya sistemi bağlarken izin verin. Bu parametreler hakkında daha fazla bilgi için tooyour dağıtım'ın belgelerine başvurun.
   
    Örnek (Ubuntu):

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    **Linux önyükleme parametreleri**
   
    Çekirdek parametresi parametreleri yukarıda toplama toohello içinde hello "`bootdegraded=true`" Merhaba RAID olarak algılanır zarar görmesi veya hello sanal makineden bir veri sürücüsünü yanlışlıkla kaldırdıysanız örneğin düşürülmüş olsa bile hello sistem tooboot izin verebilirsiniz. Varsayılan olarak bu önyüklenebilir olmayan bir sistemi sonuçlanabilir.
   
    Lütfen tooproperly düzenleme çekirdek parametreleri nasıl üzerinde tooyour dağıtım'ın belgelerine bakın. Örneğin, çoğu dağıtımda (CentOS, Oracle Linux, SLES 11) Bu parametreleri el ile toohello eklenebilir "`/boot/grub/menu.lst`" dosya.  Bu parametre toohello üzerinde ubuntu eklenebilir `GRUB_CMDLINE_LINUX_DEFAULT` değişkeninin "/ etc/varsayılan/kaz".


## <a name="trimunmap-support"></a>KIRPMA/UNMAP desteği
Bazı Linux tekrar KIRPMA/UNMAP işlemleri toodiscard destek hello diskte kullanılmayan engeller. Bu işlemler sayfaları silinmiş Azure artık geçerli değil ve iptal edilecek standart depolama tooinform öncelikle faydalıdır. Büyük dosyaları oluşturmak ve bunları silerseniz sayfaları atılıyor maliyet kaydedebilirsiniz.

> [!NOTE]
> Merhaba öbek boyutunu hello dizisi için tooless hello varsayılan (512 KB) daha ayarlarsanız RAID atma komutları verin değil. Merhaba eşlemesini olmasıdır ayrıntı düzeyi hello ana bilgisayar üzerinde değil de 512KB. Merhaba dizinin öbek boyutu mdadm'ın aracılığıyla değiştirilmiş varsa `--chunk=` parametresi sonra KIRPMA ve eşlemesini istekleri hello çekirdekten dikkate.

Tooenable KIRPMA desteği, Linux VM'NİZDE iki yolu vardır. Her zamanki gibi dağıtımınız için önerilen yaklaşımı hello bakın:

- Kullanım hello `discard` bağlama seçeneği `/etc/fstab`, örneğin:

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- Bazı durumlarda hello içinde `discard` seçeneği performans etkileri olabilir. Alternatif olarak, hello çalıştırabilirsiniz `fstrim` komutunu el ile Merhaba komut satırından veya tooyour crontab toorun düzenli olarak ekleyin:

    **Ubuntu**

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    **RHEL/CentOS**
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
