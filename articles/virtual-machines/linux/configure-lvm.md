---
title: "Linux çalıştıran bir sanal makinede aaaConfigure LVM | Microsoft Docs"
description: "Bilgi nasıl tooconfigure LVM Linux Azure üzerinde."
services: virtual-machines-linux
documentationcenter: na
author: szarkos
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: 7f533725-1484-479d-9472-6b3098d0aecc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 8daf792d87c6bb3d91a2eddcd01cfab34fd28cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a>Azure'da bir Linux VM LVM yapılandırın
Bu belgede ele alınacaktır nasıl tooconfigure mantıksal Birimi Yöneticisi (LVM), Azure sanal makinesinde. Herhangi bir disk üzerine LVM toohello sanal makine, varsayılan olarak çoğu bulut görüntüleri sahip bağlı uygun tooconfigure olsa LVM işletim sistemi diski hello üzerinde yapılandırılmış. İşletim sistemi diski olduğu herhangi bir zamanda hello tooanother hello VM ekli bu yinelenen birim grupları tooprevent sorunları ise aynı dağıtım ve bir kurtarma senaryosu sırasında yani türü. Bu nedenle yalnızca toouse LVM hello veri disklerde önerilir.

## <a name="linear-vs-striped-logical-volumes"></a>Doğrusal şeritli mantıksal birimler karşılaştırması
LVM kullanılan toocombine tek bir depolama birimi içine fiziksel disk sayısını olabilir. Varsayılan olarak LVM genellikle doğrusal mantıksal birimler, hello fiziksel depolama birlikte birleştirilmiş yani oluşturur. Bu durumda okuma/yazma işlemleri genellikle yalnızca tooa tek disk gönderilir. Buna karşılık, biz de okuma ve yazma işlemleri (yani benzer tooRAID0) hello birim grupta bulunan dağıtılmış toomultiple diskleri nerede şeritli mantıksal birimler oluşturabilirsiniz. Olası performans nedenleriyle böylece okuma ve yazma işlemleri tüm eklenen veri disklerini kullanan mantıksal birimler toostripe isteyeceksiniz.

Bu belge nasıl toocombine birkaç veri diskleri tek bir birimde grubuna açıklamak ve şeritli bir mantıksal birim oluşturun. Merhaba aşağıdaki çoğu dağıtımları ile biraz genelleştirilmiş toowork adımlardır. Çoğu durumda hello yardımcı programları ve Azure üzerinde LVM yönetmek için iş akışları diğer ortamlara temelde farklı değildir. Her zamanki gibi ayrıca Linux satıcınıza için lütfen belgeleri ve LVM belirli dağıtımınız ile kullanmak için en iyi uygulamalar danışın.

## <a name="attaching-data-disks"></a>Veri diskleri ekleme
LVM kullanırken bir genellikle iki veya daha fazla boş veri disklerle toostart isteyeceksiniz. G/ç gereksinimlerinize bağlı olarak, standart bizim depolama biriminde, too500 GÇ/ps disk veya too5000 GÇ/ps disk başına yukarı bizim Premium storage ile başına yukarı ile depolanan tooattach diskleri seçebilirsiniz. Bu makalede ayrıntıya gitmek değil tooprovision ve veri diskleri tooa Linux sanal makine ekleyin. Lütfen bakın hello Microsoft Azure makale [bir diski kullanıma açın](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) nasıl tooattach boş bir veri diski tooa Linux sanal makine Azure ile ilgili ayrıntılı yönergeler için.

## <a name="install-hello-lvm-utilities"></a>Merhaba LVM yardımcı programlarını yükleyin
* **Ubuntu**

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* **RHEL, CentOS ve Oracle Linux**

    ```bash   
    sudo yum install lvm2
    ```

* **SLES 12 ve openSUSE**

    ```bash   
    sudo zypper install lvm2
    ```

* **SLES 11**

    ```bash   
    sudo zypper install lvm2
    ```

    Ayrıca düzenlemelisiniz üzerinde SLES11 `/etc/sysconfig/lvm` ve `LVM_ACTIVATED_ON_DISCOVERED` çok "etkinleştir":

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a>LVM'yi yapılandırma
Bu kılavuzda adlandırdığımız üç veri diskleri ekli varsayacağız tooas `/dev/sdc`, `/dev/sdd` ve `/dev/sde`. Bunlar olmayabilir, Not her zaman aynı yol adları, VM'deki hello olabilir. Çalıştırabilirsiniz '`sudo fdisk -l`' veya benzer komutu toolist kullanılabilir diskler.

1. Merhaba fiziksel birimler hazırlayın:

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. Bir birim grubu oluşturun. Bu örnekte, biz hello birim grubu aradığınız `data-vg01`:

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. Merhaba mantıksal birim oluşturun. Merhaba biz aşağıdaki komutunu adlı tek bir mantıksal birim oluşturacak `data-lv01` toospan hello birimin tamamını grup, bu da uygun toocreate olduğunu unutmayın hello birim grubunda birden çok mantıksal birim.

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. Format hello mantıksal birim

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > SLES11 kullanımıyla `-t ext3` ext4 yerine. SLES11 yalnızca salt okunur erişim tooext4 bağlanan dosya sistemlerinin destekler.

## <a name="add-hello-new-file-system-tooetcfstab"></a>Merhaba yeni dosya sistemi çok/etc/fstab Ekle
> [!IMPORTANT]
> Yanlış hello düzenleme `/etc/fstab` dosya önyüklenemez bir sisteme neden. Emin değilseniz, bu dosyayı tooproperly düzenleme nasıl hakkında bilgi için lütfen toohello dağıtım'ın belgelerine başvurun. Ayrıca hello yedeğini önerilen `/etc/fstab` dosyasını düzenlemeden önce oluşturulur.

1. Örneğin, yeni bir dosya sistemi için istenen hello bağlama noktası oluşturun:

    ```bash  
    sudo mkdir /data
    ```

2. Merhaba mantıksal birim yolunu bulun

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. Açık `/etc/fstab` bir metin düzenleyicisinde ve örneğin hello yeni dosya sistemi için bir giriş ekleyin:

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    Ardından, Kaydet ve Kapat `/etc/fstab`.

4. Bu hello test `/etc/fstab` giriştir doğru:

    ```bash    
    sudo mount -a
    ```

    Bu komutu bir hata iletisi sonuçlanırsa hello hello sözdiziminde danışın `/etc/fstab` dosya.
   
    Merhaba sonraki çalıştırma `mount` komutu tooensure hello dosya sistemi takılı:

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. (İsteğe bağlı) Hatasız önyükleme parametrelerinde`/etc/fstab`
   
    Çoğu dağıtımda ya da hello dahil `nobootwait` veya `nofail` bağlama toohello eklenebilir parametreleri `/etc/fstab` dosya. Bu parametreleri oluşturulamıyor tooproperly bağlama hello RAID dosya sistemi olsa bile hello Linux sistem toocontinue tooboot izin ve hataları için belirli dosya sistemi bağlarken izin verin. Bu parametreler hakkında daha fazla bilgi için lütfen tooyour dağıtım'ın belgelerine bakın.
   
    Örnek (Ubuntu):

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a>KIRPMA/UNMAP desteği
Bazı Linux tekrar KIRPMA/UNMAP işlemleri toodiscard destek hello diskte kullanılmayan engeller. Bu işlemler sayfaları silinmiş Azure artık geçerli değil ve iptal edilecek standart depolama tooinform öncelikle faydalıdır. Büyük dosyaları oluşturmak ve bunları silerseniz sayfaları atılıyor maliyet kaydedebilirsiniz.

Tooenable KIRPMA desteği, Linux VM'NİZDE iki yolu vardır. Her zamanki gibi dağıtımınız için önerilen yaklaşımı hello bakın:

- Kullanım hello `discard` bağlama seçeneği `/etc/fstab`, örneğin:

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- Bazı durumlarda hello içinde `discard` seçeneği performans etkileri olabilir. Alternatif olarak, hello çalıştırabilirsiniz `fstrim` komutunu el ile Merhaba komut satırından veya tooyour crontab toorun düzenli olarak ekleyin:

    **Ubuntu**

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    **RHEL/CentOS**

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
