---
title: "Azure yedekleme: Dosya ve klasörleri Azure VM yedekten kurtarma | Microsoft Docs"
description: "Dosyaları bir Azure sanal makinesi kurtarma noktasından kurtarın"
services: backup
documentationcenter: dev-center-name
author: pvrk
manager: shivamg
keywords: "öğe düzeyinde kurtarma; Dosya Kurtarma Azure VM yedekten; Azure VM geri yükleme dosyaları"
ms.assetid: f1c067a2-4826-4da4-b97a-c5fd6c189a77
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pullabhk;markgal
ms.openlocfilehash: 1a62a0ed83d61272c032ac0377a54099ed118db4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="recover-files-from-azure-virtual-machine-backup"></a>Dosyaları Azure sanal makinesi yedeklemeden Kurtar

Azure backup sağlar hello yetenek toorestore [Azure Vm'leri ve diskleri](./backup-azure-arm-restore-vms.md) Azure VM yedeklerden. Şimdi bu makalede, bir Azure VM yedekten dosyalar ve klasörler gibi öğeleri nasıl kurtarabilirsiniz açıklanmaktadır.

> [!Note]
> Bu özellik Azure hello Resource Manager modeli ve korumalı tooa kurtarma Hizmetleri kasası kullanılarak dağıtılan VM'ler için kullanılabilir.
> Şifrelenmiş bir VM yedeğinin dosya kurtarma desteklenmez.
>

## <a name="mount-hello-volume-and-copy-files"></a>Merhaba birim ve kopyalama dosyaları bağlama

1. Merhaba içine oturum [Azure portal](http://portal.Azure.com). Merhaba ilgili kurtarma Hizmetleri kasası ve gerekli hello yedekleme öğesi bulun.

2. Merhaba yedekleme öğesi dikey penceresinde **dosya kurtarma**

    ![Açık kurtarma Hizmetleri kasasına yedekleme öğesi](./media/backup-azure-restore-files-from-vm/open-vault-item.png)

    Merhaba **dosya kurtarma** dikey pencere açılır.

    ![Dosya Kurtarma dikey penceresi](./media/backup-azure-restore-files-from-vm/file-recovery-blade.png)

3. Merhaba gelen **kurtarma noktası seçin** açılır menü, hello dosyaları içeren select hello kurtarma noktası istiyor. Varsayılan olarak, hello en son kurtarma noktası zaten seçilidir.

4. Tıklatın **karşıdan yürütülebilir** (için Windows Azure VM) veya **karşıdan yükleme komut dosyası** (için Linux Azure VM) toocopy dosyaları hello kurtarma noktasından kullanacağınız toodownload hello yazılım.

  Merhaba yürütülebilir/komut dosyası oluşturur hello yerel bilgisayar ve belirtilen hello arasında bir bağlantı kurtarma noktası.

5. Bir parola toorun indirilen hello komut dosyası/yürütülebilir gerekir. Oluşturulan hello parola yanında hello Kopyala düğmesini kullanarak hello portalından hello parolayı kopyalayın

    ![Oluşturulan parola](./media/backup-azure-restore-files-from-vm/generated-pswd.png)

6. Toorecover hello dosyaları istediğiniz hello bilgisayarda hello yürütülebilir/komut dosyasını çalıştırın. Yönetici kimlik bilgileriyle çalıştırmalısınız. Sınırlı erişimi olan bir bilgisayarda hello betik çalıştırırsanız, erişimi olduğundan emin olun:

    - download.microsoft.com
    - Azure VM yedeklemeler için kullandığınız azure uç noktaları
    - Giden bağlantı noktası 3260

   Linux için hello betik 'open-iSCSI' ve 'lshw' bileşenleri gerektirir tooconnect toohello kurtarma noktası. Bu nerede çalıştığına hello makinede yoksa izni tooinstall hello ilgili bileşenleri için ister ve bunları izin yükler.
   
   İstendiğinde hello portalından kopyalandığından hello parolayı girin. Merhaba geçerli parola girildikten sonra hello betikleri toohello kurtarma noktası bağlanır.
      
    ![Dosya Kurtarma dikey penceresi](./media/backup-azure-restore-files-from-vm/executable-output.png)
    
   
   Merhaba VM yedeklenen gibi hello aynı (veya uyumlu) işletim sistemi olan herhangi bir makinede hello komut dosyasını çalıştırabilirsiniz. Merhaba bkz [uyumlu işletim sistemi tablo](backup-azure-restore-files-from-vm.md#compatible-os) uyumlu işletim sistemleri için. Hello Azure sanal koruduysanız hello yürütülebilir/komut dosyası (Windows Azure VM'ler için) Windows depolama alanları veya LVM/RAID Arrays(for Linux VMs) olduktan sonra çalıştırılamaz üzerinde makine kullandığı aynı sanal makine hello. Bunun yerine, çalıştırın uyumlu bir işletim sistemi ile diğer herhangi bir makinede.

### <a name="compatible-os"></a>Uyumlu işletim sistemi

#### <a name="for-windows"></a>Windows için

Sunucu ve bilgisayar işletim sistemleri arasında tablo gösterir hello uyumluluk aşağıdaki hello. Dosyaları kurtarırken uyumsuz işletim sistemleri arasında dosya geri yüklenemiyor.

|Sunucu işletim sistemi | Uyumlu istemci işletim sistemi  |
| --------------- | ---- |
| Windows Server 2012 R2 | Windows 8.1 |
| Windows Server 2012    | Windows 8  |
| Windows Server 2008 R2 | Windows 7   |

#### <a name="for-linux"></a>Linux için

Linux hello temel bu ' % s'hello OS hello betik çalıştırdığı hello makinenin hello filesystem destek gereksinimdir Merhaba dosyaları hello mevcut Linux VM yedeklenen. Bir makine toorun hello betiği seçerken, lütfen hello aşağıdaki tabloda belirtildiği gibi hello uyumlu işletim sistemi ve hello sürümlere sahip olun.

|Linux işletim sistemi | Sürümler  |
| --------------- | ---- |
| Ubuntu | 12.04 ve üstü |
| CentOS | 6.5 ve üstü  |
| RHEL | 6.7 ve üstü |
| Debian | 7 ve üstü |
| Oracle Linux | 6.4 ve üstü |

Merhaba komut dosyası ayrıca python gerektirir ve bileşenleri tooexecute bash ve güvenli toohello kurtarma noktası bağlanmak.

|Bileşen | Sürüm  |
| --------------- | ---- |
| Bash | 4 ve üstü |
| python | 2.6.6 ve üstü  |


### <a name="identifying-volumes"></a>Birimleri tanımlama

#### <a name="for-windows"></a>Windows için

Merhaba exectuable çalıştırdığınızda hello işletim sistemi hello yeni birimleri bağlar ve sürücü harfi atar. Bu sürücüleri Windows Gezgini veya dosya Gezgini'ni toobrowse kullanabilirsiniz. Merhaba toohello birimleri atanan sürücü harfleri aynı harf hello özgün sanal makine, ancak hello gibi birim adı korunur hello olmayabilir. Örneğin, hello hello özgün sanal makine birimde yaptığı "veri diski (E:\)", toplu olarak eklenebilecek "veri diski ('Herhangi bir sürücü harfi kullanılabilir':\) hello yerel bilgisayarda. Dosya/klasör bulana kadar hello komut çıktısında bahsedilen tüm birimler üzerinden göz atın.  
       
   ![Dosya Kurtarma dikey penceresi](./media/backup-azure-restore-files-from-vm/volumes-attached.png)
           
#### <a name="for-linux"></a>Linux için

Linux hello birimler hello kurtarma noktası hello betik çalıştırdığı takılı toohello klasörü listelenmiştir. Merhaba diskleri, birimleri ve hello karşılık gelen bağlama yollar uygun şekilde gösterilen bağlı. Bu yolları bağlama olan görünür toousers kök düzeyinde erişime sahip. Merhaba komut çıktısında bahsedilen hello birimleri göz atın.

  ![Linux dosya kurtarma dikey penceresi](./media/backup-azure-restore-files-from-vm/linux-mount-paths.png)
  

## <a name="closing-hello-connection"></a>Merhaba bağlantı kesiliyor

Merhaba dosyaları tanımlama ve tooa yerel depolama konumuna kopyalanması sonra Kaldır (veya çıkarın) hello ek sürücüler. Merhaba de toounmount hello sürücülerde **dosya kurtarma** dikey penceresinde hello Azure portal'ı tıklatın **çıkarın diskleri**.

![Diskleri çıkarın](./media/backup-azure-restore-files-from-vm/unmount-disks3.png)

Merhaba diskleri kaldırılan işlendikten sonra size başarılı olduğunu bildiren bir ileti alırsınız. Merhaba diskleri kaldırabilmeniz hello bağlantı toorefresh birkaç dakika sürebilir.

Merhaba bağlantı toohello kurtarma noktası zarar görmesi sonra Linux içinde hello OS hello karşılık gelen bağlama yolları otomatik olarak kaldırmaz. Bu "artık" birimler olarak var ve görünür ancak, erişim/yazma hello dosyaları olduğunda hata throw. Bunlar el ile kaldırılabilir. Merhaba çalıştırdığınızda, komut dosyası, herhangi bir önceki kurtarma noktasını varolan böyle herhangi bir birimi tanımlar ve onay temizler.

## <a name="special-configurations"></a>Özel yapılandırmalar

### <a name="dynamic-disks"></a>Dinamik diskler

Merhaba yedeklenen Azure VM hello yürütülebilir komut dosyası çalıştırılamaz birden çok disk (Dağıtılmış veya şeritli birimler) ve/veya dinamik disklerde hataya dayanıklı birimler (yansıtılmış veya RAID-5 birimler) yayılan birimler varsa, aynı VM hello. Bunun yerine, uyumlu bir işletim sistemi ile diğer herhangi bir makinede hello yürütülebilir betiğini çalıştırın.

### <a name="windows-storage-spaces"></a>Windows depolama alanları

Windows depolama alanları Windows depodaki toovirtualize depolama sağlayan bir teknolojidir. Windows depolama alanları ile endüstri standardı diskleri depolama havuzları olarak gruplandırdıktan ve ardından bu depolama havuzlarındaki kullanılabilir alandan hello depolama alanları olarak adlandırılan sanal diskler oluşturursunuz.

Hello yürütülebilir komut dosyası çalıştırılamaz hello yedeklenen Azure VM Windows depolama alanları, kullanırsa, aynı VM hello. Bunun yerine, uyumlu bir işletim sistemi ile diğer herhangi bir makinede hello yürütülebilir betiğini çalıştırın.

### <a name="lvmraid-arrays"></a>LVM/RAID dizileri

Linux, mantıksal birim Yöneticisi (LVM) ve/veya yazılım içinde RAID kullanılan toomanage mantıksal birimler birden çok disk üzerinde dizidir. Linux VM yedeklenen hello LVM ve/veya RAID dizileri kullanıyorsa, üzerinde hello hello komut dosyası çalıştırılamaz aynı VM. Bunun yerine uyumlu işletim sistemi ile diğer herhangi bir makinede hello komut dosyasını çalıştırın ve hangi VM'yi yedeklenen hello filesystem destekler.

Merhaba LVM ve/veya RAID dizileri diskleri ve aşağıda gösterildiği gibi hello bölüm türü ile Merhaba birimleri Hello komut dosyası çıkışını görüntüler

   ![Linux LVM çıktı Dikey penceresi](./media/backup-azure-restore-files-from-vm/linux-LVMOutput.png)
   
Merhaba aşağıdaki komutları, toobe hello kullanıcı toobring tarafından bu bölümler çevrimiçi çalıştırmanız gerekir. 

**LVM bölümler için**

```
$ pvs <volume name as shown above in hello script output> 
```
Merhaba birim grubu adları fiziksel bir birimi altında listelenir.

```
$ lvdisplay <volume-group-name from hello pvs command’s results> 
```
Bu, tüm mantıksal birimleri, adlarının ve yollarının bir birim grubundaki listeler.

```
$ mount <LV path> </mountpath>
```
tercih ettiğiniz toomount hello mantıksal birimler toohello yolu.


**RAID diziler için**

```
$ mdadm –detail –scan
```
Bu, tüm RAID disklerini hakkındaki ayrıntıları görüntüler. Merhaba ilgili RAID disk olarak görüntülenir`/dev/mdm/<RAID array name in hello backed up VM>`

Merhaba RAID disk fiziksel birim varsa hello bağlama komutunu kullanın.
```
$ mount [RAID Disk Path] [/mounthpath]
```

Bu RAID disk içinde yapılandırılmış başka bir LVM varsa sonra izleme yukarıda hello birim adı hello RAID Disk adı olan LVM bölümler için özetlendiği gibi aynı yordamı hello

## <a name="troubleshooting"></a>Sorun giderme

Merhaba sanal makinelerden dosyalar kurtarılırken sorunlarınız varsa, aşağıdaki ek bilgi için tablonun hello denetleyin.

| Hata iletisi / senaryosu | Olası neden | Önerilen eylem |
| ------------------------ | -------------- | ------------------ |
| Exe çıktı: *toohello hedef bağlanma özel durumu* |Komut dosyası mümkün tooaccess hello kurtarma noktası değil | Merhaba makine yukarıda belirtilen hello erişim gereksinimlerini karşılayan olup olmadığını denetleyin|  
|   Exe çıktı: *hello hedef zaten günlüğe kaydedildi İSCSI oturumu aracılığıyla.* |   Merhaba betik aynı makine ve hello sürücüleri bağlı hello üzerinde zaten yürütüldü |   Merhaba birimleri hello kurtarma noktası zaten eklenmiş. Bunlar aynı sürücü harfini hello ile takılması değil özgün VM hello. Merhaba kullanılabilir tüm birimleri dosyanız için hello dosya Gezgini'nde göz atın |
| Exe çıktı: *hello diskleri portal ve aşıldı hello 12 hr sınırı çıkarılmış için bu komut dosyası geçersiz. Lütfen yeni bir betik hello Portalı'ndan yükleyin.* |    Merhaba diskleri hello portalı veya hello 12 hr sınırı aşıldı çıkarıldı |  Bu belirli exe artık geçersiz ve çalıştırılamaz. Bu kurtarma noktası zamanında dosya tooaccess hello istiyorsanız, yeni bir exe için hello portalını ziyaret edin|
| Merhaba exe çalıştırdığı hello makinede: hello çıkarma düğmesine tıklandığında sonra hello yeni birimleri çıkarılmış değil |    Merhaba İSCSI Başlatıcısı hello makinede değil yanıt/yenileme bağlantısı toohello hedefine ve hello önbellek Bakımı |    Merhaba çıkarma düğmesine basıldığında sonra bazı dakika bekleyin. Merhaba yeni birimler hala çıkarılmış değil, tüm hello birimler üzerinden göz atın. Disk hello bağlantısı ve hello hello Başlatıcı toorefresh hello birim bir hata iletisi ile kaldırılmadan önce bu zorlar kullanılabilir değil|
| Exe çıktı: komut dosyası başarıyla çalıştırıldı ancak "Yeni birimlerin bağlı" Merhaba betik Çıkışta görüntülenmez |   Bu geçici bir hatadır   | Merhaba birimleri zaten eklenmiş. Explorer toobrowse açın. Her komut dosyaları çalıştırmak için aynı makine hello kullanıyorsanız, hello makinenin yeniden başlatılması göz önünde bulundurun ve hello listesi hello sonraki exe çalıştırmalarında görüntülenmesi gerekir. |
| Linux özel: erişilemiyor tooview hello istenen birimleri | Merhaba makinenin hello betik çalıştırdığı işletim sistemi Hello hello VM'yi yedeklenen Merhaba, temel alınan dosya sistemi tanımıyor olabilir | Onay kilitlenme tutarlı veya dosya tutarlı olup Hello kurtarma noktası. Merhaba, işletim sistemi tanıdığı başka bir makinede tutarlı, çalışma hello komut dosyasının VM'in filesystem yedeklediyseniz |
| Windows özel: erişilemiyor tooview hello istenen birimleri | Merhaba diskleri ekli ancak hello birimleri değil yapılandırılmamış | Merhaba disk yönetimi ekranından hello ek diskleri ilgili toohello kurtarma noktası belirleyin. Bu diskleri olarak çevrimdışı olan durumu çevrimiçi hello diskte sağ tıklayarak artırmayı deneyin ve 'Çevrimiçi' tıklayın|
