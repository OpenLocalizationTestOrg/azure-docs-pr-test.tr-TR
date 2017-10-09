---
title: "aaaPlanning VM yedekleme altyapınızı Azure | Microsoft Docs"
description: "Azure'da sanal makineler yukarı tooback planlarken önemli noktalar"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: sanal makineleri yedekleme, sanal makineleri yedekleme
ms.assetid: 19d2cf82-1f60-43e1-b089-9238042887a9
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: d11982431610000293038ee6aa7df8e7bc2d8b70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-your-vm-backup-infrastructure-in-azure"></a>Azure’da sanal makine yedekleme altyapınızı planlama
Bu makalede, performans ve kaynak önerileri toohelp VM yedekleme altyapınızı planlama sağlar. Ayrıca, önemli yönlerini hello Backup hizmeti tanımlar; Bu yönlerinin, mimarisi belirlemede önemli kapasite planlaması ve zamanlama. Seçtiğiniz varsa [ortamınızı hazırlanmış](backup-azure-vms-prepare.md), planlama adımdır hello sonraki başlamadan önce [tooback Vm'leri yedekleme](backup-azure-vms.md). Azure sanal makineler hakkında daha fazla bilgiye ihtiyacınız varsa, hello bkz [Virtual Machines belgeleri](https://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="how-does-azure-back-up-virtual-machines"></a>Azure nasıl mu sanal makineleri yedekleyin?
Hello Azure Backup hizmeti yedekleme işi Zamanlanmış Başlangıç zamanında başlattığında hello yedekleme uzantısını tootake zaman içinde nokta anlık görüntü tetikler. Hello Azure Backup hizmeti kullanan hello _VMSnapshot_ uzantısı'nda Windows ve hello _VMSnapshotLinux_ Linux uzantı. Merhaba uzantısı hello ilk VM yedekleme sırasında yüklenir. tooinstall hello uzantısı hello VM çalıştırması gerekir. Merhaba VM çalışır durumda değilse, hello Backup hizmeti bir anlık görüntüsünü hello bu yana (hiçbir uygulama yazma VM durduruldu hello sırasında gerçekleşir) depolama temel alır.

Windows VM görüntüsünü alırken, hello Backup hizmeti ile Merhaba Birim Gölge Kopyası Hizmeti (VSS) tooget tutarlı bir anlık görüntü hello sanal makinenin disklerinin düzenler. Linux VM'ler yedekliyorsanız, bir VM anlık olduğunda kendi özel komut dosyaları tooensure tutarlılık yazabilirsiniz. Bu komut dosyalarını Çağırma ile ilgili ayrıntılar bu makalenin sonraki bölümlerinde sağlanır.

Hello Azure Backup hizmeti hello anlık görüntüsünü alır sonra hello aktarılan toohello kasası verilerdir. toomaximize verimliliği hello hizmeti tanımlar ve yalnızca hello hello önceki yedeklemeden bu yana değişmiş olan veri bloklarını aktarır.

![Azure sanal makine yedekleme mimarisi](./media/backup-azure-vms-introduction/vmbackup-architecture.png)

Merhaba veri aktarımı tamamlandığında hello anlık görüntü kaldırılır ve bir kurtarma noktası oluşturulur.

> [!NOTE]
> 1. Merhaba yedekleme işlemi sırasında Azure yedekleme hello bağlı geçici disk toohello sanal makine içermez. Daha fazla bilgi için hello blog bakın [geçici depolama](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/).
> 2. Bir depolama düzeyi anlık görüntü ve toovault anlık görüntü aktarımları Azure yedeğini alır beri hello yedekleme işi tamamlanana kadar hello depolama hesabı anahtarlarını değiştirmeyin.
> 3. Premium VM'ler için başlangıç anlık görüntü toostorage hesabı kopyalayın. Azure Backup hizmeti veri toovault aktarmak için yeterli IOPS aldığından emin toomake budur. Bu ek kopyasını depolama VM boyutu ayrılmış hello göre ücretlendirilir. 
>

### <a name="data-consistency"></a>Veri tutarlılığı
İş açısından kritik verileri veri çalıştıran hello üretmek hello uygulamaları sırasında yedeklenmesi hello olgu tarafından yedekleme ve geri yükleme iş açısından kritik verileri karmaşık. tooaddress Bu, Azure Backup destekler uygulamayla tutarlı yedeklemeler hem Windows hem de Linux VM'ler
#### <a name="windows-vm"></a>Windows VM
Azure yedekleme Windows Vm'lerinde VSS tam yedeklemeler gerçekleştirir (daha fazla bilgi edinin [VSS tam yedekleme](http://blogs.technet.com/b/filecab/archive/2008/05/21/what-is-the-difference-between-vss-full-backup-and-vss-copy-backup-in-windows-server-2008.aspx)). tooenable VSS yedeklemeleri, kayıt defteri anahtarı gereksinimlerini toobe ayarlanmış hello VM üzerinde aşağıdaki hello kopyalayın.

```
[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT]
"USEVSSCOPYBACKUP"="TRUE"
```

#### <a name="linux-vms"></a>Linux VM'leri
Azure Backup komut dosyası bir çerçeve sağlar. Linux VM'ler yedeklerken tooensure uygulama tutarlılığı özel öncesi ve yedekleme iş akışı hello ve ortam denetimi sonrası komut dosyaları oluşturun. Azure yedekleme hello VM anlık görüntü çıkarmadan önce hello öncesi betiği çağırır ve hello VM anlık görüntü işi tamamlandıktan sonra hello sonrası komut dosyasını çağırır. Daha fazla ayrıntı için bkz: [öncesi betiği ve sonrası betik kullanarak uygulama tutarlı VM yedeklemeleri](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).
> [!NOTE]
> Azure yedekleme yalnızca müşteri tarafından yazılan hello çağırır öncesi ve sonrası komut dosyaları. Merhaba öncesi betiği ve sonrası betikleri başarıyla çalıştırırsanız, Azure Backup hello kurtarma noktası uygulama tutarlı işaretler. Ancak, hello müşteri özel komut dosyaları kullanırken hello uygulama tutarlılığı için sonuçta sorumludur.
>


Bu tabloda koşulları altında Azure VM yedeklemesi sırasında ortaya ve geri yükleme yordamlarını tutarlılık ve hello hello türleri açıklanmaktadır.

| Tutarlılık | VSS tabanlı | Açıklama ve ayrıntıları |
| --- | --- | --- |
| Uygulama tutarlılığı |Windows için Evet|Uygulama tutarlılığı, sağlar gibi iş yükleri için idealdir:<ol><li> Merhaba VM *ön*. <li>Yoktur *bozulma*. <li>Yoktur *veri kaybı*.<li> Merhaba, VSS veya ön/son betik kullanarak yedekleme--hello zaman Merhaba uygulaması içeren tarafından hello veri kullanan tutarlı toohello uygulamayı verilerdir.</ol> <li>*Windows sanal makineleri*-en Microsoft iş yükleri, iş yüküne özgü eylemler ilgili toodata tutarlılık denetimi yapmak VSS yazıcılarının vardır. Örneğin, Microsoft SQL Server hello yazma toohello işlem günlüğü dosyasını ve hello veritabanı doğru şekilde yapıldığını sağlar bir VSS yazıcısı olduğu. Azure Windows VM yedeklemeler, toocreate bir uygulamayla tutarlı kurtarma noktası hello yedekleme uzantısını hello VSS iş akışının çağırmak ve hello VM anlık görüntü gerçekleştirilmesi için tamamlanması gerekir. Hello Azure VM anlık görüntü toobe için doğru tüm Azure VM uygulamaların hello VSS yazıcılarının da tamamlamanız gerekir. (Merhaba öğrenin [VSS Temelleri](http://blogs.technet.com/b/josebda/archive/2007/10/10/the-basics-of-the-volume-shadow-copy-service-vss.aspx) ve derin hello ayrıntılarını daha yakından inceleyin [nasıl çalıştığını](https://technet.microsoft.com/library/cc785914%28v=ws.10%29.aspx)). </li> <li> *Linux VM'ler*-müşteriler yürütebilir [özel öncesi betiğini ve sonrası betik tooensure uygulama tutarlılığı](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent). </li> |
| Dosya sistemi tutarlılığı |Evet - Windows tabanlı bilgisayarlar için |Merhaba kurtarma noktası olabilir burada iki senaryo vardır *dosya sistemi tutarlı*:<ul><li>Linux VM'ler için Azure'da, yedeklerini öncesi-script/sonrası-script veya öncesi-script/sonrası-script başarısız olduysa olmadan. <li>VSS azure'da Windows VM için yedekleme sırasında hata oluştu.</li></ul> Her iki bu durumda yapılabilir en iyi hello tooensure olup: <ol><li> Merhaba VM *ön*. <li>Yoktur *bozulma*.<li>Yoktur *veri kaybı*.</ol> Uygulamaları geri hello verileri tooimplement kendi "Düzeltme yukarı" mekanizmasına ihtiyaç duyarlar. |
| Kilitlenme tutarlılığı |Hayır |Bu eşdeğer tooa sanal makine "kilitlenme" yaşayan (ya da bir yazılım veya donanım sıfırlama) durumdur. Kilitlenme tutarlılığı normal yedekleme hello aynı anda Hello Azure sanal makine kapatılır ortaya çıkar. Kilitlenme tutarlı bir kurtarma noktası garanti hello hello veri tutarlılığını geçici hello depolama ortamına--hello işletim sistemi veya hello uygulamanın hello açısından ya da sağlar. Yedekleme hello aynı anda hello diskte zaten var. yalnızca hello veriler yakalanan ve yedeklendi. <br/> <br/> Varken hiçbir garanti genellikle, işletim sistemi önyüklemesinde, disk kontrol ederek ve ardından hello yordamı, chkdsk, toofix gibi Bozulması hataları. Herhangi bir bellek içi veri veya aktarılan toohello disk edilmemiş yazma kaybolur. verileri geri alma tamamlandı toobe gerekebileceği Merhaba uygulaması genellikle kendi doğrulama mekanizmasını ile izler. <br><br>Merhaba işlem günlüğü hello veritabanında mevcut olmayan girişleri varsa hello verileri tutarlı olana kadar örnek olarak, hello veritabanı yazılımını bir geri alma sonra yapar. (Gibi Dağıtılmış birimler) birden çok sanal disklere veri dağıldığında kilitlenme tutarlı bir kurtarma noktası hello veri hello doğruluğu garanti sağlar. |

## <a name="performance-and-resource-utilization"></a>Performans ve kaynak kullanımı
Dağıtılan şirket içi yedekleme yazılımı gibi kapasite ve kaynak kullanımı için gereksinimleri azure'da VM yedeklerken planlamanız gerekir. Merhaba [Azure depolama sınırlarını](../azure-subscription-service-limits.md#storage-limits) nasıl toostructure VM dağıtımları tooget en az başarımı toorunning iş yükleri tanımlayın.

Yedekleme performansını planlarken aşağıdaki Azure depolama sınırlarını dikkat toohello ödeme:

* Depolama hesabı başına en fazla çıkış
* Depolama hesabı başına toplam istek oranı

### <a name="storage-account-limits"></a>Depolama hesabı sınırları
Yedekleme verilerini bir depolama hesabından kopyalanır, toohello girdi/çıktı işlemleri / saniye (IOPS) ve çıkış (veya üretilen iş) ölçümleri hello depolama hesabının ekler. AT hello aynı zaman, sanal makineler de IOPS ve üretilen iş kullanma. Merhaba hedef tooensure yedekleme ve sanal makine trafiği depolama hesabı sınırları aşan yok.

### <a name="number-of-disks"></a>Disk sayısı
Merhaba yedekleme işlemi toocomplete bir yedekleme işi mümkün olan en kısa sürede çalışır. Bunu yaparken, mümkün olduğunca fazla kaynak tüketir. Ancak, tüm g/ç işlemleri tarafından hello sınırlı *tek Blob için hedef işleme*, saniye başına 60 MB sınırı vardır. Bir deneme toomaximize kendi hızı hello yedekleme işlemi çalışır her hello VM'in disklerini yukarı tooback *paralel*. VM dört diskler varsa, tüm dört diskleri paralel yukarı tooback hello hizmeti çalışır. Merhaba **diskleri sayısı** , yedeklenen olan depolama hesabı yedekleme trafiği belirlemede en önemli faktör hello.

### <a name="backup-schedule"></a>Yedekleme zamanlaması
Merhaba performansını etkiler ek bir faktörü olan **yedekleme zamanlaması**. Tüm sanal makineleri hello aynı yedeklenir şekilde hello ilkeleri yapılandırın, zaman, trafiği sıkışması zamanlanmış. Merhaba yedekleme işlemi paralel tüm diskleri yukarı tooback çalışır. hiç örtüşmeyen hello günün farklı zamanında farklı Vm'leri yedekleme depolama hesabından tooreduce hello yedekleme trafiği.

## <a name="capacity-planning"></a>Kapasite planlaması
Merhaba önceki Etkenler bir araya getirilmesi, tooplan hello depolama hesabı kullanımı ihtiyaçları için gerekir. Merhaba karşıdan [VM yedekleme kapasite planlama Excel elektronik tablosu](https://gallery.technet.microsoft.com/Azure-Backup-Storage-a46d7e33) toosee hello etkisini disk ve yedekleme zamanlaması seçimi.

### <a name="backup-throughput"></a>Yedekleme işleme
Yedeklenmekte olan her disk için Azure yedekleme hello blokları hello diskteki okur ve depoları yalnızca değiştirilen verileri (artımlı yedeklemeyi) hello. Merhaba aşağıdaki tabloda hello ortalama Yedekleme hizmetini işleme değerleri gösterir. Veri aşağıdaki hello kullanarak, belirtilen boyutta bir disk yukarı tooback hello süreyi gerekli tahmin edebilirsiniz.

| Yedekleme işlemi | İyi verimlilik |
| --- | --- |
| İlk yedekleme |160 MB/sn |
| Artımlı yedekleme (DR) |640 MB/sn <br><br> Verimliliği düşmeye önemli ölçüde hello (yedeklenen toobe gereken) veri değiştirdiyseniz dağınık hello diski.|

## <a name="total-vm-backup-time"></a>Toplam VM yedekleme saati
Çoğu hello yedekleme saati harcanır sırasında okuma ve veri kopyalama, diğer işlemlerin toohello gereken toplam süreyi tooback VM yukarı katkıda:

* Gereken süre çok[yükleyin veya güncelleştirin hello yedekleme uzantısını](backup-azure-vms.md).
* Hello geçen süre tootrigger anlık olduğu anlık görüntü saati. Anlık görüntüler tetiklenen Kapat toohello zamanlanmış yedekleme saati değildir.
* Sıra bekleme süresi. Birden çok müşteri yedeklemelerden işleme Hello yedekleme hizmeti olduğundan, anlık görüntü toohello yedekleme veya kurtarma Hizmetleri yedekleme verileri kopyalayarak kasası hemen başlatılamayabilir. Yoğun yük kez işlenmekte olan yedekleme toohello sayısı nedeniyle tooeight saatlerini hello bekleme uzatabilirsiniz. Ancak, hello toplam VM yedekleme süresini günlük yedekleme ilkeleri için 24 saatten az olur.
* Veri aktarımı saati, yedekleme için gereken hizmet önceki yedekten toocompute hello artımlı değişiklikler ve bu değişiklikleri toovault depolama aktarma.

### <a name="why-am-i-observing-longer12-hours-backup-time"></a>Neden ı Gözlemleme longer(>12 hours) yedekleme zamanı?
Yedekleme iki aşamadan oluşur: anlık görüntüler alma ve aktarma hello anlık görüntüleri toohello kasası. Merhaba yedekleme hizmeti için depolama en iyi duruma getirir. Başlangıç anlık görüntü veri tooa kasası aktarırken hello hizmeti hello önceki anlık görüntüden yalnızca artımlı değişiklikler aktarır.  toodetermine hello artımlı değişiklikler, hello hizmet başlangıç bloklarından hello sağlama toplamı hesaplar. Bir blok değiştirdiyseniz hello blok toohello kasası gönderilen bir blok toobe tanımlanır. Ardından hello hizmet ayrıntısına daha fazla her hello fırsatları toominimize hello veri tootransfer için arayan blokları, tanımlanmış. Tüm değişen blokları değerlendirdikten sonra hello hizmet hello değişiklikleri birleştirir ve bunları toohello kasası gönderir. Bazı eski uygulamalarda küçük, parçalanmış yazma depolama için uygun değildir. Başlangıç anlık görüntü çok sayıda küçük, parçalanmış yazma içeriyorsa, hello hizmet hello uygulamalar tarafından yazılan hello veri işlemek için ek zaman harcadığı. Merhaba hello VM içinde çalışan uygulamalar için uygulama yazma blok Azure'dan, önerilen bir en az 8 KB.. Uygulamanızı değerinden 8 KB'lik bir blok kullanıyorsa, yedekleme performansının parametreden etkilenir. Uygulama tooimprove yedekleme performans ayarlama konusunda daha fazla yardım için bkz: [uygulamalarını Azure storage ile en iyi performans için ayarlama](../storage/common/storage-premium-storage-performance.md). Premium depolama örnekler Hello makale yedekleme performansı kullanılsa da hello Kılavuzu standart depolama diskleri için geçerlidir.

## <a name="total-restore-time"></a>Toplam geri yükleme süresi
Bir geri yükleme işlemi iki ana alt görevden oluşur: geri hello kasası seçilen toohello müşteri depolama hesabından veri kopyalama ve hello sanal makine oluşturma. Geri hello kasadan veri kopyalama, Azure'da hello yedeklemeleri dahili olarak depolandığı ve hello müşteri depolama hesabı depolandığı bağlıdır. Toocopy veri geçen süre bağlıdır:
* Merhaba, birden çok müşterilerden gelen geri yükleme hello hizmet işlemleri işlerini beri sıra bekleme süresi - aynı anda geri yükleme isteklerdir bir kuyruğa koymak.
* Veri kopyalama zamanı - veri hello kasa toohello müşteri depolama hesabından kopyalanır. Geri yükleme süre üzerinde IOPS bağlıdır ve verimlilik Azure Backup hizmeti seçili hello müşteri depolama hesabında alır. tooreduce saati hello geri yükleme işlemi sırasında kopyalama Merhaba, diğer uygulama yazma ve okuma yüklenmemiş bir depolama hesabı seçin.

## <a name="best-practices"></a>En iyi uygulamalar
Sanal makineleri için yedeklemeleri yapılandırılırken bu yöntemler aşağıdaki öneririz:

* Hello aynı bulut hizmeti tooback hello fazla 10 Klasik Vm'lerden zamanlama yok aynı anda. Tooback aynı bulut hizmetinden birden çok sanal makineleri yedeklemek istiyorsanız, bir saate göre hello yedekleme Başlangıç saatlerini basamaklandırma.
* Birden fazla 40 VM'ler tooback yukarı hello zamanlamayın aynı anda.
* VM, yoğun olmayan saatlerde yedeklemelerin. Bu şekilde hello Backup hizmeti IOPS hello müşteri depolama hesabı toohello kasadan veri aktarmak için kullanır.
* Bir ilke farklı depolama hesaplarında yayılan VM'ler uygulanan emin olun. En fazla 20 önerdiğimiz tek bir depolama hesabına toplam disklerden hello tarafından korunan aynı yedekleme zamanlaması. Büyüktür 20 diskleri depolama hesabındaki yayılan varsa bu VM'lerin birden çok ilkeleri tooget arasında hello aktarımı aşaması hello yedekleme işlemi sırasında gerekli IOPS hello.
* Premium depolama toosame depolama hesabı üzerinde çalışan bir VM geri yüklemeyin. Merhaba geri yükleme işlemi işlemi hello yedekleme işlemi ile örtüşür, hello azaltır yedekleme için kullanılabilir IOPS.
* Premium VM yedekleme için bu depolama hesabı konak premium disklerin başarılı bir yedekleme anlık görüntüsü hazırlama en az %50 boş alan olduğundan emin olun. 
* Yedekleme 2.7 için emin olun, python sürümü Linux sanal makineleri üzerinde etkin

## <a name="data-encryption"></a>Veri şifrelemesi
Azure yedekleme verileri hello Yedekleme işleminin bir parçası olarak şifrelemez. Ancak, hello VM içinde verileri şifreleyebilir ve geri hello korumalı verilere sorunsuz bir şekilde (daha fazla bilgi edinin [şifrelenmiş verilerin yedekleme](backup-azure-vms-encryption.md)).

## <a name="calculating-hello-cost-of-protected-instances"></a>Korumalı örnekler Hello maliyetini hesaplama
Azure Backup yedeklenir Azure sanal makineleri konu çok[Azure yedekleme fiyatlandırması](https://azure.microsoft.com/pricing/details/backup/). Merhaba korumalı örnekleri hesaplama hello üzerinde temel *gerçek* hello sanal makine--hello "kaynak disk" hariç tüm hello verileri hello toplamıdır hello sanal makine boyutu

Vm'leri yedekleme için fiyatlandırma *değil* her veri diski ekli toohello sanal makine için desteklenen en fazla hello boyutu göre. Fiyatlandırma hello veri diski depolanan hello gerçek verileri temel alır. Benzer şekilde, hello Yedekleme depolaması faturanızda hello Azure Yedekleme'de her kurtarma noktası gerçek veri hello hello toplamını olduğu depolanan veri miktarına bağlıdır.

Örneğin, bir boyutta A2 standart iki ek veri disklerinin her biri 1 TB maksimum boyuta sahip olan sanal makine alın. Merhaba aşağıdaki tabloda her bu disklere depolanan Merhaba gerçek veriler sağlar:

| Disk türü | En büyük boyutu | Gerçek veri yok |
| --- | --- | --- |
| İşletim sistemi diski |1023 GB |17 GB |
| Yerel disk / kaynak disk |135 GB |5 GB (yedekleme için yer almayan) |
| Veri diski 1 |1023 GB |30 GB |
| Veri diski 2 |1023 GB |0 GB |

Merhaba *gerçek* hello sanal makinesinin boyutu bu durumda olan 17 GB + 30 GB + 0 GB = 47 GB. Bu korumalı örnek boyutu (47 GB) hello aylık fatura hello temelini olur. Hello hello sanal makine veri miktarı artar, fatura değişiklikler için uygun şekilde kullanılan hello korumalı örnek boyutu.

Faturalama Hello ilk başarılı yedekleme tamamlanana kadar başlatılmaz. Bu noktada, hem depolama hem de korumalı örnekleri hello faturalama başlar. Faturalandırma var olduğu sürece devam *herhangi bir kasasında depolanan verileri yedekleme* hello sanal makine için. Merhaba sanal makinede korumayı durdurun, ancak sanal makine yedekleme verilerini bir kasada var olması gerekir, faturalandırma devam eder.

Belirtilen sanal makine yalnızca hello koruma durdurduysanız durdurur faturalama *ve* tüm yedekleme verileri silinir. Koruma durduğunda ve etkin yedek iş yok, hello son başarılı VM yedeğinin boyutu hello hello aylık fatura için kullanılan hello korumalı örnek boyutu olur.

## <a name="questions"></a>Sorularınız mı var?
Sorularınız varsa veya herhangi bir özellik varsa dahil, toosee istediğiniz [Geri bildirimlerinizi bize gönderin](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Sonraki adımlar
* [Sanal makineleri yedekleme](backup-azure-vms.md)
* [Sanal makine yedeklemesi yönetme](backup-azure-manage-vms.md)
* [Sanal makineleri geri yükleme](backup-azure-restore-vms.md)
* [VM yedekleme sorunlarını giderme](backup-azure-vms-troubleshoot.md)
