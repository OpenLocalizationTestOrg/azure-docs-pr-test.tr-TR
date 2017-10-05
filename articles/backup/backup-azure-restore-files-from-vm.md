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
ms.openlocfilehash: ae7c345c11a7db25413d60ad822f16f84ca37362
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="recover-files-from-azure-virtual-machine-backup"></a>Dosyaları Azure sanal makinesi yedeklemeden Kurtar

Azure yedekleme geri yükleme yeteneği sağlar [Azure Vm'leri ve diskleri](./backup-azure-arm-restore-vms.md) Azure VM yedeklerden. Şimdi bu makalede, bir Azure VM yedekten dosyalar ve klasörler gibi öğeleri nasıl kurtarabilirsiniz açıklanmaktadır.

> [!Note]
> Bu özellik, Azure Resource Manager modelini kullanarak dağıtılmış ve bir kurtarma Hizmetleri kasası korumalı VM'ler için kullanılabilir.
> Şifrelenmiş bir VM yedeğinin dosya kurtarma desteklenmez.
>

## <a name="mount-the-volume-and-copy-files"></a>Birim ve kopyalama dosyaları bağlama

1. [Azure portal](http://portal.Azure.com) oturum açın. İlgili kurtarma Hizmetleri kasası ve gerekli yedekleme öğesi bulun.

2. Yedekleme öğesinin dikey penceresinde **dosya kurtarma**

    ![Açık kurtarma Hizmetleri kasasına yedekleme öğesi](./media/backup-azure-restore-files-from-vm/open-vault-item.png)

    **Dosya kurtarma** dikey pencere açılır.

    ![Dosya Kurtarma dikey penceresi](./media/backup-azure-restore-files-from-vm/file-recovery-blade.png)

3. Gelen **kurtarma noktası seçin** açılır menüsünde, kullanmak istediğiniz dosyaları içeren kurtarma noktasını seçin. Varsayılan olarak, en son kurtarma noktası zaten seçilidir.

4. ' I tıklatın **karşıdan yürütülebilir** (için Windows Azure VM) veya **karşıdan yükleme komut dosyası** (için Linux Azure VM) kurtarma noktasından dosyaları kopyalamak için kullanacağınız yazılımını indirmek için.

  Yürütülebilir dosya/komut dosyası yerel bilgisayar ve belirtilen kurtarma noktası arasında bir bağlantı oluşturur.

5. İndirilen komut dosyası/yürütülebilir dosyayı çalıştırmak için bir parola gerekir. Oluşturulan parola yanında Kopyala düğmesini kullanarak portalından parolası kopyalama

    ![Oluşturulan parola](./media/backup-azure-restore-files-from-vm/generated-pswd.png)

6. Dosyaları kurtarmak istediğiniz bilgisayarda yürütülebilir/komut dosyasını çalıştırın. Yönetici kimlik bilgileriyle çalıştırmalısınız. Sınırlı erişimi olan bir bilgisayarda bir betik çalıştırırsanız, erişimi olduğundan emin olun:

    - download.microsoft.com
    - Azure VM yedeklemeler için kullandığınız azure uç noktaları
    - Giden bağlantı noktası 3260

   Linux için komut dosyası kurtarma noktasına bağlanmak için 'open-iSCSI' ve 'lshw' bileşenleri gerektirir. Bu nerede çalıştığına makinede yoksa ilgili bileşenlerini yüklemek için izin ister ve bunları izin yükler.
   
   İstendiğinde portalından kopyalandığından parolayı girin. Geçerli parola girildikten sonra komut dosyaları kurtarma noktasına bağlanır.
      
    ![Dosya Kurtarma dikey penceresi](./media/backup-azure-restore-files-from-vm/executable-output.png)
    
   
   Yedeklenen VM olarak aynı (veya uyumlu) işletim sistemine sahip herhangi bir makinede komut dosyasını çalıştırın. Bkz: [uyumlu işletim sistemi tablo](backup-azure-restore-files-from-vm.md#compatible-os) uyumlu işletim sistemleri için. Ardından korumalı Azure sanal makine Windows depolama alanları (için Windows Azure VM) veya LVM/RAID Arrays(for Linux VMs) kullanıyorsa, aynı sanal makineye yürütülebilir/komut dosyası çalıştırılamaz. Bunun yerine, çalıştırın uyumlu bir işletim sistemi ile diğer herhangi bir makinede.

### <a name="compatible-os"></a>Uyumlu işletim sistemi

#### <a name="for-windows"></a>Windows için

Aşağıdaki tabloda, sunucu ve bilgisayar işletim sistemleri arasındaki uyumluluk gösterir. Dosyaları kurtarırken uyumsuz işletim sistemleri arasında dosya geri yüklenemiyor.

|Sunucu işletim sistemi | Uyumlu istemci işletim sistemi  |
| --------------- | ---- |
| Windows Server 2012 R2 | Windows 8.1 |
| Windows Server 2012    | Windows 8  |
| Windows Server 2008 R2 | Windows 7   |

#### <a name="for-linux"></a>Linux için

Linux komut dosyası çalıştırdığı makine işletim sistemini yedeklenen Linux VM'de mevcut dosyaların dosya sistemi desteklemesi gereken temel gereksinimdir. Komut dosyasını çalıştırmak için bir makine seçerken, lütfen bu uyumlu işletim sistemi ve sürümleri aşağıdaki tabloda belirtildiği gibi sahip emin olun.

|Linux işletim sistemi | Sürümler  |
| --------------- | ---- |
| Ubuntu | 12.04 ve üstü |
| CentOS | 6.5 ve üstü  |
| RHEL | 6.7 ve üstü |
| Debian | 7 ve üstü |
| Oracle Linux | 6.4 ve üstü |

Komut dosyası yürütme ve güvenli bir şekilde kurtarma noktasına bağlanmak için python ve bash bileşenleri de gerektirir.

|Bileşen | Sürüm  |
| --------------- | ---- |
| Bash | 4 ve üstü |
| python | 2.6.6 ve üstü  |


### <a name="identifying-volumes"></a>Birimleri tanımlama

#### <a name="for-windows"></a>Windows için

Exectuable çalıştırdığınızda, işletim sistemi yeni birimlere bağlar ve sürücü harfi atar. Bu sürücüleri göz atmak için Windows Gezgini'nde veya dosya Gezgini'ni kullanın. Birimlere atanan sürücü harfleri özgün sanal makine olarak aynı harf olmayabilir, ancak, birim adı korunur. Örneğin, özgün sanal makine birimde ise "veri diski (E:\)", toplu olarak eklenebilecek "veri diski ('Herhangi bir sürücü harfi kullanılabilir':\) yerel bilgisayarda. Komut çıktısında dosya/klasör bulana kadar bahsedilen tüm birimler üzerinden göz atın.  
       
   ![Dosya Kurtarma dikey penceresi](./media/backup-azure-restore-files-from-vm/volumes-attached.png)
           
#### <a name="for-linux"></a>Linux için

Linux komut dosyası çalıştırdığı klasörüne kurtarma noktası birimleri bağlanır. Ekli diskleri, birimleri ve karşılık gelen bağlama yollarını buna uygun olarak gösterilir. Bu yolları bağlama kök düzeyinde erişime sahip kullanıcılar tarafından görülebilir. Komut çıktısında belirtilen birimler göz atın.

  ![Linux dosya kurtarma dikey penceresi](./media/backup-azure-restore-files-from-vm/linux-mount-paths.png)
  

## <a name="closing-the-connection"></a>Bağlantı kesiliyor

Dosyaları tanımlama ve yerel depolama konumuna kopyalanması sonra Kaldır (veya çıkarın) ek sürücüler. Üzerinde sürücülerin kaldırılması **dosya kurtarma** dikey Azure portalında tıklayın **çıkarın diskleri**.

![Diskleri çıkarın](./media/backup-azure-restore-files-from-vm/unmount-disks3.png)

Diskleri kaldırılan işlendikten sonra size başarılı olduğunu bildiren bir ileti alırsınız. Bağlantının diskleri kaldırabilmeniz yenilemek birkaç dakika sürebilir.

Kurtarma noktası için bağlantı zarar görmesi sonra Linux OS karşılık gelen bağlama yolları otomatik olarak kaldırmaz. Bu "artık" birimler olarak var ve görünür ancak, erişim/yazma dosyaları olduğunda hata throw. Bunlar el ile kaldırılabilir. Çalıştırdığınızda, komut dosyası, herhangi bir önceki kurtarma noktasını varolan böyle herhangi bir birimi tanımlar ve onay temizler.

## <a name="special-configurations"></a>Özel yapılandırmalar

### <a name="dynamic-disks"></a>Dinamik diskler

Ardından yedeklenen Azure VM dinamik disklerde (yayılmış ve şeritli birimler) birden çok diske yayılan birimler ve/veya hataya dayanıklı birimler (yansıtılmış veya RAID-5 birimler) varsa, aynı VM yürütülebilir komut dosyası çalıştırılamaz. Bunun yerine, uyumlu bir işletim sistemi ile diğer herhangi bir makinede çalıştırılabilir komut dosyasını çalıştırın.

### <a name="windows-storage-spaces"></a>Windows depolama alanları

Windows depolama alanları, depolamayı sanallaştırmanızı sağlar Windows depolama için kullanılan bir teknolojidir. Windows depolama alanları ile endüstri standardı diskleri depolama havuzları olarak gruplandırdıktan ve ardından bu depolama havuzlarındaki kullanılabilir alandan depolama alanları olarak adlandırılan sanal diskler oluşturursunuz.

Ardından yedeklenen Azure VM Windows depolama alanları kullanıyorsa, aynı VM yürütülebilir komut dosyası çalıştırılamaz. Bunun yerine, uyumlu bir işletim sistemi ile diğer herhangi bir makinede çalıştırılabilir komut dosyasını çalıştırın.

### <a name="lvmraid-arrays"></a>LVM/RAID dizileri

Linux mantıksal birim Yöneticisi (LVM) ve/veya yazılım RAID diziler birden çok disk mantıksal birimleri yönetmek için kullanılır. Yedeklenen Linux VM LVM ve/veya RAID dizileri kullanıyorsa, aynı VM üzerinde komut dosyası çalıştırılamaz. Bunun yerine uyumlu işletim sistemi ile diğer herhangi bir makinede komut dosyasını çalıştırmak ve hangi dosya sistemi yedeklenen VM destekler.

Komut dosyası çıkışını LVM ve/veya RAID dizileri diskleri ve birimleri bölüm türü ile aşağıda gösterildiği gibi görüntüler

   ![Linux LVM çıktı Dikey penceresi](./media/backup-azure-restore-files-from-vm/linux-LVMOutput.png)
   
Aşağıdaki komutlar, bu bölümler çevrimiçi duruma getirmek için kullanıcı tarafından çalıştırılması gerekir. 

**LVM bölümler için**

```
$ pvs <volume name as shown above in the script output> 
```
Birim grubu adları fiziksel bir birimi altında listelenir.

```
$ lvdisplay <volume-group-name from the pvs command’s results> 
```
Bu, tüm mantıksal birimleri, adlarının ve yollarının bir birim grubundaki listeler.

```
$ mount <LV path> </mountpath>
```
Tercih ettiğiniz yolu mantıksal birimlere bağlamak için.


**RAID diziler için**

```
$ mdadm –detail –scan
```
Bu, tüm RAID disklerini hakkındaki ayrıntıları görüntüler. İlgili RAID disk olarak görüntülenir`/dev/mdm/<RAID array name in the backed up VM>`

RAID disk fiziksel birim varsa bağlama komutunu kullanın.
```
$ mount [RAID Disk Path] [/mounthpath]
```

Bu RAID disk sonra yukarıda LVM bölümler için RAID Disk adı olan birim adı ile ana hatlarıyla aynı yordamı izleyin içinde yapılandırılmış başka bir LVM varsa

## <a name="troubleshooting"></a>Sorun giderme

Sanal makinelerden dosyalar kurtarılırken sorunlarınız varsa, ek bilgi için aşağıdaki tabloya bakın.

| Hata iletisi / senaryosu | Olası neden | Önerilen eylem |
| ------------------------ | -------------- | ------------------ |
| Exe çıktı: *hedef bağlanma özel durumu* |Komut dosyası kurtarma noktası erişebilir değil | Makine yukarıda bahsedilen erişim gereksinimlerini karşılayan olup olmadığını denetleyin|  
|   Exe çıktı: *hedef zaten İSCSI oturumu aracılığıyla oturum açıldı.* | Komut dosyası, zaten aynı makinede yürütülen ve sürücüleri bağlı | Kurtarma noktası birimleri zaten eklenmiş. Bunlar orijinal VM ile aynı sürücü harflerini takılması değil. Kullanılabilir tüm birimleri dosyanız için dosya Gezgini'nde göz atın |
| Exe çıktı: *diskleri portal/aşıldı 12 hr sınırı çıkarılmış için bu komut dosyası geçersiz. Lütfen yeni bir betik Portalı'ndan yükleyin.* |  Diskleri portal ya da 12 hr sınırı aşıldı çıkarıldı |    Bu belirli exe artık geçersiz ve çalıştırılamaz. Bu kurtarma noktasını zaman dosyalara erişmek isterseniz yeni bir exe portalını ziyaret edin|
| Exe çalıştırdığı makinede: yeni birimleri çıkarma düğmesine tıklandığında sonra çıkarılmış değil |    İSCSI Başlatıcısı makinede değil yanıt/yenileme bağlantısı hedef için ve önbellek Bakımı |    Çıkarma düğmesine basıldığında sonra için bazı dakika bekleyin. Yeni birimlere hala çıkarılmış değil, tüm birimler üzerinden göz atın. Bu bağlantıyı yenilemek için Başlatıcı zorlar ve birim diskin kullanılabilir olmadığından bir hata iletisi ile çıkarıldı|
| Exe çıktı: komut dosyası başarıyla çalıştırıldı ancak "Yeni birimlerin bağlı" komut dosyası çıktı görüntülenmez | Bu geçici bir hatadır   | Birimleri zaten eklenmiş. Göz atmak için Explorer'ı açın. Her komut dosyaları çalıştırmak için aynı makine kullanıyorsanız, makinenin yeniden başlatılması göz önünde bulundurun ve liste sonraki exe çalıştırmalarında görüntülenmesi gerekir. |
| Linux özel: İstenen birimleri görüntülemek için | Komut dosyası çalıştırdığı makine işletim sistemini temel alınan dosya sistemi yedeklenen VM tanımıyor olabilir | Kurtarma noktası kilitlenme tutarlı veya dosya tutarlı olup olmadığını denetleyin. Yedeklenen dosya tutarlı, başka bir komut dosyasını çalıştırmak, işletim sistemi makine varsa VM'in filesystem tanır |
| Windows özel: İstenen birimleri görüntülemek için | Diskleri ekli ancak birimleri değil yapılandırılmamış | Disk yönetimi ekranından kurtarma noktasıyla ilgili ek diskleri belirleyin. Bu diskleri olarak çevrimdışı olan durumu çevrimiçi disk üzerinde sağ tıklayarak artırmayı deneyin ve 'Çevrimiçi' tıklayın|
