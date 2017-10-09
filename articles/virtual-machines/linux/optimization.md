---
title: aaaOptimize, Azure Linux VM'de | Microsoft Docs
description: "Azure ile ilgili en iyi performans için Linux VM oluşturdunuz emin bazı en iyi duruma getirme ipuçları toomake öğrenin"
keywords: Linux sanal makine, sanal makine linux ubuntu sanal makine
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 8baa30c8-d40e-41ac-93d0-74e96fe18d4c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: rclaus
ms.openlocfilehash: 89a9ac022928a2801a9a15e1c172340352745354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-linux-vm-on-azure"></a>Azure’da Linux VM’nizi iyileştirme
Linux sanal makine (VM) oluşturmak kolay toodo hello komut satırından veya hello portalından olur. Bu öğretici nasıl tooensure onu toooptimize performansını hello Microsoft Azure platformu üzerinde ayarladığınız gösterir. Bu konuda bir Ubuntu Server VM kullanır, ancak, Linux kullanarak sanal makine oluşturabilirsiniz [kendi görüntü şablonları olarak](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

## <a name="prerequisites"></a>Ön koşullar
Bu konu çalışan bir Azure aboneliği zaten sahip varsayar ([ücretsiz deneme sürenizde](https://azure.microsoft.com/pricing/free-trial/)) ve bir VM Azure aboneliğinizde zaten sağlanmış. Merhaba son olduğundan emin olun [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooyour içinde Azure aboneliği ile oturum [az oturum açma](/cli/azure/#login) , önce [bir VM oluşturma](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="azure-os-disk"></a>Azure işletim sistemi diski
Azure'da bir Linux VM oluşturduktan sonra kendisiyle ilişkilendirilmiş iki disk var. **/ dev/sda** , işletim sistemi disk **/dev/sdb** geçici disktir.  Merhaba ana işletim sistemi diski kullanmayın (**/dev/sda**) hello işletim sistemi olarak dışında her şey için optimize edilen için hızlı VM önyükleme süresi ve iş yükleriniz için iyi bir performans sağlamaz. Tooattach bir istersiniz veya daha fazla diskler tooyour VM tooget kalıcı ve en iyi duruma getirilmiş depolama verileriniz için. 

## <a name="adding-disks-for-size-and-performance-targets"></a>Disk boyutu ve performans hedefleri için ekleme
VM boyutu Hello üzerinde bağlı olarak, too16 ek A-Series disklerde, D-serisi 32 disklerde ve bir makinede G-serisi - her boyutu too1 TB yedeklemeniz 64 diskleri ekleyebilirsiniz. Ek disk alanı ve IOPS gereksinimlerini gerektiği gibi ekleyin. Her diskin 500 IOPS performans hedefinin Premium Storage için standart depolama ve disk başına too5000 IOPS vardır.  Premium depolama diskler hakkında daha fazla bilgi için bkz: [Premium Storage: Azure VM'ler için yüksek performanslı depolama](../../storage/common/storage-premium-storage.md)

tooachieve hello burada kendi önbellek ayarlarını ayarlanmış tooeither Premium depolama disklerde yüksek IOPS **salt okunur** veya **hiçbiri**, devre dışı bırakmalısınız **engelleri** sırada Linux Hello dosya sisteminde bağlama. Merhaba yedeklenmiş diskleri için bu önbellek ayarlarını dayanıklı tooPremium depolama yazdığından engelleri gerekmez.

* Kullanırsanız **reiserFS**, hello bağlama seçeneği kullanılarak devre dışı bırak engelleri `barrier=none` (engelleri etkinleştirmek için kullanın `barrier=flush`)
* Kullanırsanız **ext3/ext4**, hello bağlama seçeneği kullanılarak devre dışı bırak engelleri `barrier=0` (engelleri etkinleştirmek için kullanın `barrier=1`)
* Kullanırsanız **XFS**, hello bağlama seçeneği kullanılarak devre dışı bırak engelleri `nobarrier` (Merhaba seçeneği engelleri etkinleştirmek için kullanın `barrier`)

## <a name="unmanaged-storage-account-considerations"></a>Yönetilmeyen depolama hesabında dikkate alınacak noktalar
Azure CLI 2.0 hello ile bir VM oluştururken hello varsayılan toouse Azure yönetilen diskleri eylemdir.  Bu diskleri hello Azure platformu tarafından işlenir ve hazırlık veya konumu toostore gerektirmez bunları.  Yönetilmeyen diskler bir depolama hesabı gerektirir ve bazı ek performans konuları vardır.  Yönetilen diskler hakkında daha fazla bilgi için bkz. [Azure Yönetilen Disklere genel bakış](../windows/managed-disks-overview.md).  Yalnızca yönetilmeyen diskleri kullandığınızda hello aşağıdaki bölümde performans özetlemektedir.  Yeniden varsayılan hello ve yönetilen toouse diskleri önerilen depolama çözümüdür.

Yönetilmeyen disklerle VM oluşturursanız, diskleri hello aynı bulunan depolama hesaplarından bağladığınızdan emin olun, VM tooensure bölgeye kapatın yakınlık ve ağ gecikmesini en aza.  Her standart depolama hesabının en fazla 20 sahip k IOPS ve 500 TB boyutu kapasitesi.  Bu sınır hello işletim sistemi disk ve oluşturduğunuz herhangi bir veri diski yoğun olarak kullanılan tooapproximately 40 disklerini çalışır. Premium depolama hesapları için maksimum IOPS sınırı yoktur ancak 32 TB boyut sınırı yoktur. 

Yüksek IOPS iş yükleri ve postalarla seçtiniz, standart depolama diskleriniz için birden çok depolama hesapları toomake 20.000 IOPS standart depolama hesapları için sınırlamak hello ulaşıp değil emin arasında toosplit hello diskleri gerekebilir. VM diskleri bir karışımını farklı depolama hesapları ve depolama hesabı türlerini tooachieve arasında en iyi yapılandırmanızı içerebilir.
 

## <a name="your-vm-temporary-drive"></a>VM geçici sürücünüze
Bir VM oluşturduğunuzda varsayılan olarak Azure, bir işletim sistemi diski ile sağlar (**/dev/sda**) ve geçici bir disk (**/dev/sdb**).  Eklediğiniz Göster yukarı olarak tüm ek diskleri **/dev/sdc**, **/dev/sdd**, **/dev/sde** ve benzeri. Geçici diskteki tüm verileri (**/dev/sdb**) sağlam değildir ve Bakım VM'yi yeniden başlatılmasını zorlar veya belirli olaylar gibi VM yeniden boyutlandırma, yeniden dağıtım, kaybolmuş olabilir.  Merhaba boyutunu ve geçici disk türünü dağıtım sırasında seçtiğiniz ilgili toohello VM boyutu olan. Tüm hello premium boyutu VM'ler (DS, G ve DS_V2 serisi) hello geçici sürücü ek performansını too48k IOPS yedeklemek için yerel bir SSD tarafından desteklenir. 

## <a name="linux-swap-file"></a>Linux takas dosyası
Daha sonra Azure VM Ubuntu veya CoreOS görüntüden ise, bir bulut-config toocloud init CustomData toosend kullanabilirsiniz. Varsa, [özel Linux görüntü karşıya](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) bulut init kullanan, aynı zamanda bulut init kullanarak takas bölümleri yapılandırın.

Ubuntu bulut görüntülerinde bulut init tooconfigure hello takas bölüm kullanmanız gerekir. Daha fazla bilgi için bkz: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).

Bulut init desteği olmadan görüntüler için Azure Marketi hello dağıtılan VM görüntüleri bir VM Linux işletim sistemi hello ile tümleşik aracısına sahip. Bu aracı hello VM toointeract çeşitli Azure hizmetleriyle sağlar. Varsayılarak standart bir hello Azure Market görüntüsünden dağıttıysanız, toodo gerekir toocorrectly aşağıdaki hello Linux takas dosyası ayarlarınızı yapılandırın:

Bulun ve hello iki giriş değiştirme **/etc/waagent.conf** dosya. Bunlar, ayrılmış takas dosyası hello varlığını ve hello takas dosyası boyutunu denetler. Merhaba parametreleri toomodify arayan `ResourceDisk.EnableSwap=N` ve`ResourceDisk.SwapSizeMB=0` 

Merhaba parametreleri toohello ayarları aşağıdaki gibi değiştirin:

* ResourceDisk.EnableSwap=Y
* MB toomeet ResourceDisk.SwapSizeMB={size gereksinimlerinizi} 

Merhaba değişiklik yaptıktan sonra toorestart hello waagent gerekir veya Linux VM tooreflect bu değişiklikleri yeniden başlatın.  Merhaba değişiklikleri uygulanmıştır ve hello kullandığınızda takas dosyası oluşturuldu bildiğiniz `free` tooview boş alan komutu. Merhaba aşağıdaki örnekte sahip hello değiştirme sonucu olarak oluşturulan 512 MB takas dosyası **waagent.conf** dosyası:

```bash
azuseruser@myVM:~$ free
            total       used       free     shared    buffers     cached
Mem:       3525156     804168    2720988        408       8428     633192
-/+ buffers/cache:     162548    3362608
Swap:       524284          0     524284
```

## <a name="io-scheduling-algorithm-for-premium-storage"></a>Premium depolama g/ç zamanlama algoritması
Merhaba 2.6.18 Linux çekirdek ile son tarih tooCFQ (tamamen Orta Sıralama algoritması) hello varsayılan g/ç zamanlama algoritma değiştirildi. Rasgele erişim g/ç modelleri için CFQ ve son tarih arasındaki performans farklar düşünülerek fark yoktur.  SSD tabanlı diskleri hello disk g/ç düzeni daha olduğu sıralı, geri geçiş toohello SEKMEYİ veya son algoritmasını daha iyi g/ç performansı elde edebilirsiniz.

### <a name="view-hello-current-io-scheduler"></a>Görünüm hello geçerli g/ç Zamanlayıcı
Merhaba aşağıdaki komutu kullanın:  

```bash
cat /sys/block/sda/queue/scheduler
```

Merhaba geçerli Zamanlayıcı gösterir çıktı aşağıdaki bakın.  

```bash
noop [deadline] cfq
```

### <a name="change-hello-current-device-devsda-of-io-scheduling-algorithm"></a>Merhaba geçerli aygıtın (/ dev/sda) algoritması zamanlama g/ç değiştirme
Merhaba aşağıdaki komutları kullanın:  

```bash
azureuser@myVM:~$ sudo su -
root@myVM:~# echo "noop" >/sys/block/sda/queue/scheduler
root@myVM:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
root@myVM:~# update-grub
```

> [!NOTE]
> Bu ayar için uygulama **/dev/sda** tek başına kullanışlı değildir. Tüm veri disklerde burada sıralı g/ç hello g/ç düzeni dominates ayarlayın.  

Çıktı aşağıdaki, gösteren hello görmelisiniz **grub.cfg** başarıyla yeniden oluşturuldu ve bu hello varsayılan Zamanlayıcı güncelleştirilmiş tooNOOP olmuştur.  

```bash
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-3.13.0-34-generic
Found initrd image: /boot/initrd.img-3.13.0-34-generic
Found linux image: /boot/vmlinuz-3.13.0-32-generic
Found initrd image: /boot/initrd.img-3.13.0-32-generic
Found memtest86+ image: /memtest86+.elf
Found memtest86+ image: /memtest86+.bin
done
```

Hello Redhat dağıtım ailesi için komutu aşağıdaki hello yalnızca gerekir:   

```bash
echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local
```

## <a name="using-software-raid-tooachieve-higher-iops"></a>Kullanarak yazılım RAID tooachieve daha yüksek g / Ops
İş yüklerinizi tek bir disk sunabileceğinden daha fazla IOPS gerektiriyorsa, toouse birden çok disk yazılım RAID yapılandırması gerekir. Azure disk dayanıklılık hello yerel doku katmanında gerçekleştirdiğinden, yüksek düzeyde performans bir RAID-0 şeritleme yapılandırmadan hello elde edin.  Sağlama ve diskleri hello Azure ortamı oluşturun ve bölümlendirme, biçimlendirme ve bağlama sürücü hello önce bunları tooyour Linux VM ekleyin.  Yazılım RAID kurulumu, Linux VM'de Azure yapılandırma hakkında daha fazla ayrıntı hello bulunabilir  **[yapılandırma yazılım RAID Linux'ta](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**  belge.

## <a name="next-steps"></a>Sonraki Adımlar
, Tüm en iyi duruma getirme tartışmalarını öncesinde tooperform testleri gerekir ve her değişiklik toomeasure hello sonra hello değişiklik etkisi unutmayın.  En iyi duruma getirme, ortamınızdaki farklı makinelerde farklı sonuçlar olan bir adım adım işlemidir.  Bir yapılandırma ile ilgili ne çalışacağı başkaları için çalışmayabilir.

Bazı yararlı bağlantılar tooadditional kaynaklar: 

* [Premium Depolama: Azure Sanal Makine İş Yükleri için Yüksek Performanslı Depolama](../../storage/common/storage-premium-storage.md)
* [Azure Linux Aracısı Kullanıcı Kılavuzu](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure Linux VM'ler MySQL performansı en iyi duruma getirme](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Yazılım RAID Linux üzerinde yapılandırma](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

