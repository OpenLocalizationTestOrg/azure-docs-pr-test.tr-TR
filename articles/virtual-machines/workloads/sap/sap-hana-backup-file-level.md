---
title: "aaaSAP HANA Azure Backup dosya düzeyinde | Microsoft Docs"
description: "İki ana yedekleme olasılıklarını SAP HANA Azure sanal makinelerde vardır, bu makalede, SAP HANA Azure yedekleme dosya düzeyinde yer almaktadır"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: d5a55de5634ac7724e7fd0fa3760c6c408c3db74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-azure-backup-on-file-level"></a>Dosya düzeyinde bir SAP HANA Azure yedekleme

## <a name="introduction"></a>Giriş

Bu üç bölümlük SAP HANA yedeklemede ilgili makaleleri bir parçasıdır. [SAP HANA için yedekleme Kılavuzu Azure sanal makineler üzerinde](./sap-hana-backup-guide.md) Başlarken, genel bir bakış ve bilgi sağlar ve [tabanlı depolama anlık görüntü SAP HANA yedeklemeyi](./sap-hana-backup-storage-snapshots.md) kapsar hello depolama anlık görüntü tabanlı yedekleme seçeneği.

Hello Azure VM boyutlarda baktığınızda, biri bir GS5 64 eklenen veri disklerini izin verdiğini görebilirsiniz. Büyük SAP HANA sistemler için çok sayıda disk zaten veri ve günlük dosyaları için büyük olasılıkla en iyi disk g/ç işleme için RAID yazılım ile birlikte duruma getirilebilir. ardından Hello soru nerede toostore SAP HANA yedek bağlı hello veri diskleri zamanla doldurabilir dosyaları mı? Bkz: [azure'daki Linux sanal makineler için Boyutlar](../../linux/sizes.md) hello Azure VM boyutu tablolar için.

Şu anda Azure Backup hizmeti ile kullanılabilecek hiçbir SAP HANA yedekleme tümleştirme yoktur. SAP HANA Studio aracılığıyla veya SAP HANA SQL deyimlerini üzerinden dosya tabanlı Yedekleme durumdayken toomanage yedekleme/geri yükleme hello dosya düzeyinde hello standart yol. Bkz: [SAP HANA SQL ve sistem görünümleri başvurusu](https://help.sap.com/hana/SAP_HANA_SQL_and_System_Views_Reference_en.pdf) daha fazla bilgi için.

![Bu şekilde hello iletişim hello yedekleme menü öğesinin SAP HANA Studio'da gösterilmektedir.](media/sap-hana-backup-file-level/image022.png)

Bu şekilde hello iletişim hello yedekleme menü öğesinin SAP HANA Studio'da gösterilmektedir. Türü seçerken &quot;dosyası&quot; varsa toospecify bir yolu hello dosya sisteminde SAP HANA hello yedekleme dosyalarının nerede yazar. Geri yükleme çalışır hello aynı şekilde.

Bu seçenek basit ve düz iletme sesleri olsa da, bazı noktalar vardır. Önceden belirtildiği gibi bir Azure VM eklenebilecek veri disklerinin sayısının bir kısıtlaması vardır. Kapasite toostore SAP HANA yedekleme dosyalarını yazılım gerektirebilir hello veritabanı ve disk üretilen iş gereksinimlerini hello boyutuna bağlı olarak VM hello hello dosya sistemi olmayabilir arasında birden çok veri diskleri bölümlemesine kullanarak RAID. Bu yedekleme dosyaları ve yönetme dosya boyutu sınırlamaları ve performans verileri terabayt işlerken taşıma için çeşitli seçenekler bu makalenin sonraki bölümlerinde sağlanır.

Toplam Kapasite ilgili daha fazla özgürlük sunar, başka bir seçenek Azure blob depolama olur. Şu anda tek bir blob kısıtlı too1 TB de olsa da, tek blob kapsayıcısının hello toplam kapasite 500 TB'tır. Buna ek olarak, müşteriler hello seçim tooselect sözde verir &quot;cool&quot; blob depolama maliyeti avantajına sahiptir. Bkz: [Azure Blob Storage: sık erişimli ve seyrek erişimli depolama katmanları](../../../storage/blobs/storage-blob-storage-tiers.md) cool blob depolama hakkında ayrıntılı bilgi için.

Ek güvenlik için coğrafi olarak çoğaltılmış depolama hesabı toostore hello SAP HANA yedeklemeleri kullanın. Bkz: [Azure Storage çoğaltma](../../../storage/common/storage-redundancy.md) depolama hesabı çoğaltma hakkında ayrıntılı bilgi için.

Bir SAP HANA yedeklemeler için ayrılmış VHD'leri coğrafi olarak çoğaltılmış bir özel yedekleme depolama hesabında yerleştir. Aksi takdirde bir hello SAP HANA yedeklemeleri tooa coğrafi olarak çoğaltılmış depolama hesabını tutmak hello VHD'leri veya farklı bir bölgede tooa depolama hesabı kopyalamak.

## <a name="azure-backup-agent"></a>Azure Yedekleme aracısı

Azure yedekleme sunar hello seçeneği toonot yalnızca geri tam VM'ler, ancak ayrıca dosyaları ve dizinleri toobe hello konuk işletim sistemi yüklü olan hello Yedekleme aracısı üzerinden. Ancak aralık 2016 itibariyle, bu aracı yalnızca Windows üzerinde desteklenir (bkz [hello Resource Manager dağıtım modeli kullanılarak geri bir Windows Server ya da istemci tooAzure yukarı](../../../backup/backup-configure-vault.md)).

Geçici bir çözüm toofirst kopyasıdır (örneğin, aracılığıyla SAMBA paylaşım) SAP HANA yedekleme dosyalarını tooa Azure Windows VM ve buradan hello Azure Yedekleme aracısı kullanın. Teknik olarak mümkün olsa da, karmaşıklık eklemek ve hello yedekleme yavaş veya geri yükleme işlemi bir bit toohello kopyalama hello Linux hello Windows VM arasındaki son. Olmayan toofollow bu yaklaşım önerilir.

## <a name="azure-blobxfer-utility-details"></a>Azure blobxfer yardımcı programı ayrıntıları

toostore dizin ve dosyaların Azure depolama, bir kullanabilir CLI veya PowerShell hello birini kullanarak bir araç veya geliştirin [Azure SDK'ları](https://azure.microsoft.com/downloads/). Ayrıca bir kullanıma hazır yardımcı AzCopy, veri tooAzure depolama kopyalamak için ancak Windows ise yalnızca (bkz [hello AzCopy komut satırı yardımcı programı ile veri aktarma](../../../storage/common/storage-use-azcopy.md)).

Bu nedenle blobxfer SAP HANA yedekleme dosyalarını kopyalamak için kullanıldı. Açık kaynak, üretim ortamlarında birçok müşteri tarafından kullanılan ve kullanılabilir olan [GitHub](https://github.com/Azure/blobxfer). Bu araç, tooeither Azure blob depolama veya Azure dosya paylaşımına doğrudan bir toocopy veri sağlar. Ayrıca, çeşitli md5 karma değeri veya bir dizin ile birden çok dosya kopyalarken otomatik paralellik gibi kullanışlı özellikler sunar.

## <a name="sap-hana-backup-performance"></a>SAP HANA yedekleme performansı

![Bu ekran hello SAP HANA yedekleme konsolunda SAP HANA Studio değil](media/sap-hana-backup-file-level/image023.png)

SAP HANA Studio'da hello SAP HANA yedekleme konsolunun bu ekran görüntüsüdür. Yaklaşık 42 dakika toodo hello yedekleme sürdü Merhaba tek bir Azure standart depolama diskteki 230 GB toohello HANA VM ekli XFS dosya sistemini kullanma.

![Bu ekran YaST hello SAP HANA üzerinde VM sınamasıdır](media/sap-hana-backup-file-level/image024.png)

Bu ekran YaST hello SAP HANA test VM üzerinde ' dir. Önceden belirtildiği gibi bir SAP HANA yedekleme için 1 TB'lik tek disk hello görebilirsiniz. Yaklaşık 42 dakika toobackup sürdü 230 GB. Ayrıca, beş 200 GB disk eklenmedi ve bu beş Azure veri diskleri üstünde şeritleme ile yazılım RAID md0 oluşturulmuş.

![Aynı yazılım RAID şeritleme ile beş arasında yedekleme hello yinelenen Azure standart depolama veri diskleri bağlı](media/sap-hana-backup-file-level/image025.png)

Aynı yazılım RAID şeritleme ile beş arasında yedekleme yinelenen hello Azure standart depolama veri diskleri duruma hello yedekleme süresini too10 dakika aşağı 42 dakika bağlı. Merhaba diskleri toohello VM önbelleğe alma olmadan eklenmedi. Dolayısıyla belirgin ne kadar önemli disk yazma üretimi hello yedekleme zamanı taşır. Bir anahtar tooAzure premium depolama toofurther hızlandırmak sonra en iyi performans için hello işlemi başlatılamadı. Genel olarak, Azure premium storage üretim sistemleri için kullanılmalıdır.

## <a name="copy-sap-hana-backup-files-tooazure-blob-storage"></a>SAP HANA yedekleme dosyalarını tooAzure blob depolama kopyalama

Aralık 2016 en iyi şekilde hello gibi seçeneği tooquickly deposu SAP HANA yedekleme dosyalarını Azure blob depolama grubudur. Tek tek blob kapsayıcısı yeterli GS5 VM ile tookeep yeterli SAP HANA yedeklemeler Azure üzerinde çalışan çoğu SAP HANA sistemler için 500 TB'lık bir sınırı vardır. Müşterilerin sahip arasında hello seçim &quot;etkin&quot; ve &quot;soğuk&quot; blob depolamada (bkz [Azure Blob Storage: sık erişimli ve seyrek erişimli depolama katmanları](../../../storage/blobs/storage-blob-storage-tiers.md)).

TooAzure blob doğrudan depolama hello blobxfer aracıyla kolay toocopy hello SAP HANA yedek dosya sayısıdır.

![Bir tam SAP HANA dosya yedekleme hello dosyaları burada görebilirsiniz](media/sap-hana-backup-file-level/image026.png)

Burada bir hello dosyaları bir tam SAP HANA dosya yedekleme görebilirsiniz. Merhaba büyük bir kabaca 230 GB olan ve dört dosyası vardır.

![Toocopy hello 230 GB tooan Azure standart depolama hesabı blob kapsayıcısı kabaca 3000 saniye sürdü](media/sap-hana-backup-file-level/image027.png)

MD5 karma değeri hello ilk testinde kullanmayan, toocopy hello 230 GB tooan Azure standart depolama hesabı blob kapsayıcısı kabaca 3000 saniye sürdü.

![Bu ekran görüntüsünde bir hello Azure portalı üzerinde nasıl göründüğünü görebilirsiniz](media/sap-hana-backup-file-level/image028.png)

Bu ekran görüntüsünde bir hello Azure portalı üzerinde nasıl göründüğünü görebilirsiniz. Adlı bir blob kapsayıcı &quot;sap hana yedeklemeleri&quot; oluşturuldu ve hello SAP HANA yedekleme dosyaları temsil edecek hello dört BLOB'lar içerir. Bunlardan birini kabaca 230 GB bir boyuta sahiptir.

Merhaba HANA Studio yedekleme konsolu bir toorestrict hello en fazla dosya boyutunu HANA yedek dosyaları sağlar. Hello örnek ortamında, birden çok daha küçük yedekleme dosyaları, büyük 230 GB dosya yerine olası toohave yaparak performansı geliştirilmiş.

![Merhaba HANA yan içermiyor &#39; Hello yedek dosya boyutu sınırını ayarlama t artırmak hello yedekleme saati](media/sap-hana-backup-file-level/image029.png)

Merhaba HANA yan içermiyor &#39; Hello yedek dosya boyutu sınırını ayarlama t artırmak hello yedekleme saati hello dosyaları bu şekilde gösterildiği gibi sıralı olarak yazıldığından. Merhaba yedekleme hello 230-GB yerine dört büyük veri dosyaları tek dosyalı oluşmasını hello dosya boyutu sınırını too60 GB ayarlandı.

![tootest paralellik hello blobxfer aracının hello en büyük dosya boyutu HANA yedeklemeler için sonra too15 GB ayarlandı](media/sap-hana-backup-file-level/image030.png)

tootest paralellik hello blobxfer aracının hello en büyük dosya boyutu HANA yedeklemeler için sonra 19 yedekleme dosyalarında sonuçlandı too15 GB olarak ayarlanmış. Bu yapılandırma too875 saniye 3000 saniye gelen hello zaman blobxfer toocopy hello 230 GB tooAzure blob storage için duruma getirdi.

Bir Azure blob yazmak için 60 MB/sn toohello sınırı nedeniyle bu sonucudur. Birden çok BLOB'ları aracılığıyla paralellik hello sorununu çözer, ancak bir dezavantajı yok: Bu HANA yedekleme dosyalarını tooAzure hello blobxfer aracı toocopy performansını artırma blob depolama yükü hello HANA VM hem hello ağ koyar. İşlem HANA sisteminin etkilenmiş haline gelir.

## <a name="blob-copy-of-dedicated-azure-data-disks-in-backup-software-raid"></a>Yedekleme yazılım RAID ayrılmış Azure veri diski BLOB kopyalama

Merhaba el ile VM veri disk yedekleme, bu yaklaşım bir değil tüm hello veri diskleri HANA verileri dahil olmak üzere bir yüklemesinde VM toosave hello tüm SAP, yedekleme HANA dosyaları ve yapılandırma dosyaları günlüğe kaydetmez. Bunun yerine, hello ayrılmış toohave yazılım RAID şeritleme ile birden çok Azure veri VHD'ler arasında tam bir SAP HANA dosya yedekleme depolamak için olur. Bir hello SAP HANA yedeğiniz yalnızca bu diskler, kopyalar. Bir adanmış HANA yedekleme depolama hesabında kolayca tutulması veya ayrılmış tooa bağlı &quot;yönetim VM yedekleme&quot; başka bir işleme için.

![Tüm VHD'leri söz konusu hello kullanarak kopyalanan ** Başlat-azurestorageblobcopy ** PowerShell komutu](media/sap-hana-backup-file-level/image031.png)

Merhaba yedekleme toohello yerel yazılım RAID tamamlandıktan sonra tüm VHD'leri söz konusu hello kullanarak kopyalanan **başlangıç azurestorageblobcopy** PowerShell komutunu (bkz [başlangıç AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy)). Yalnızca hello yedekleme dosyalarını tutmak için ayrılmış hello dosya sistemi etkilediği gibi SAP HANA veri veya günlük dosyası tutarlılık hello disk üzerinde hiçbir endişeniz vardır. Bu komutun hello VM çevrimiçi kalırken çalıştığını avantajdır. toobe hiçbir işlem toohello yedekleme kümesi, yazar belirli olması emin toounmount hello önce blob kopyalama ve daha sonra yeniden bağlayın. Veya bir kullanabilir uygun bir çok&quot;Dondur&quot; hello dosya sistemi. Örneğin, xfs aracılığıyla\_hello XFS dosya sistemi için Dondur.

![Bu ekran, hello Azure portalı üzerinde hello VHD'ler kapsayıcısında BLOB'lar hello listesini gösterir.](media/sap-hana-backup-file-level/image032.png)

Bu ekran hello hello BLOB listesi gösterir &quot;VHD'ler&quot; hello Azure portalı üzerinde kapsayıcı. Merhaba ekran görüntüsü, beş VHD'ler hello gösterir bulundukları toohello SAP HANA server VM tooserve hello yazılım RAID tookeep SAP HANA yedekleme dosyaları eklendi. Ayrıca hello aracılığıyla hello blob kopyalama komut gerçekleştirilen beş kopyaları gösterir.

![Test amacıyla, hello SAP HANA yedekleme yazılımı RAID disklerini hello kopyalarını ekli toohello uygulama sunucusu VM olan](media/sap-hana-backup-file-level/image033.png)

Test amacıyla, hello SAP HANA yedekleme yazılımı RAID disklerini hello kopyalarını ekli toohello uygulama sunucusu VM yoktu.

![Merhaba uygulama sunucusu VM tooattach hello disk kopyaları kapandı](media/sap-hana-backup-file-level/image034.png)

Merhaba uygulama sunucusu VM tooattach hello disk kopyaları kapandı. Merhaba VM başlattıktan sonra hello diskleri ve hello RAID doğru bulunan (UUID bağlanan). Yalnızca hello bağlama noktası hello YaST bölümleyici oluşturulduğu, eksikti. Daha sonra hello SAP HANA yedek dosya kopyalarını işletim sistemi düzeyinde görünür hale geldi.

## <a name="copy-sap-hana-backup-files-toonfs-share"></a>SAP HANA yedekleme dosyalarını tooNFS paylaşmak kopyalayın

toolessen hello olası etkisini hello SAP HANA sistemden bir performans veya disk alanı perspektif, bir NFS paylaşımına hello SAP HANA yedekleme dosyalarını depolamak düşünebilirsiniz. Teknik olarak çalışır, ancak ikinci bir Azure VM NFS paylaşım hello hello konağı olarak kullanılması anlamına gelir. Toohello VM ağ bant genişliği nedeniyle küçük bir VM boyutu olmamalıdır. Algılama sonra bu aşağı tooshut yapacağı &quot;yedekleme VM&quot; ve yalnızca hello SAP HANA yedekleme yürütme kaydınızı duruma getirin. Bir NFS yazma, paylaşım hello ağda yük koyar ve etkileri hello SAP HANA sistem ancak yalnızca yönetme hello hello yedekleme dosyaları daha sonra &quot;yedekleme VM&quot; hello SAP HANA sistem hiç etkilemek değil.

![Başka bir Azure VM NFS paylaşımından takılı toohello SAP HANA server VM edildi](media/sap-hana-backup-file-level/image035.png)

tooverify hello NFS kullanım örneği, başka bir Azure VM NFS paylaşımından takılı toohello SAP HANA server VM. Hiçbir özel vardı uygulanan NFS ayarlama.

![1 saat ve 46 dakika toodo hello yedekleme doğrudan sürdü](media/sap-hana-backup-file-level/image036.png)

Merhaba NFS paylaşım hello SAP HANA sunucuda hello gibi bir hızlı şerit kümesi oluştu. Bununla birlikte, 1 saat ve 46 dakika toodo hello tooa yerel kümesi yazılırken hello NFS paylaşım 10 dakika yerine doğrudan üzerinde yedekleme sürdü.

![Merhaba alternatif 1 saat 43 dakikada çok daha hızlı değildi](media/sap-hana-backup-file-level/image037.png)

Yedekleme tooa yerel kümesi yapılması ve toohello kopyalanması hello alternatif NFS paylaşım işletim sistemi düzeyinde (basit bir **cp - avr** komutu) çok daha hızlı değildi. 1 saat 43 dakika sürdü.

Bu nedenle çalışır ancak performans hello 230 GB yedekleme test için iyi değildi. Görüneceğini çoklu terabayt için daha büyük.

## <a name="copy-sap-hana-backup-files-tooazure-file-service"></a>SAP HANA yedekleme dosyalarını tooAzure dosya hizmeti kopyalayın

Bir Azure dosya paylaşımı içinde Azure Linux VM'de olası toomount olur. Merhaba makale [nasıl toouse Linux Azure File storage](../../../storage/files/storage-how-to-use-files-linux.md) hakkında ayrıntılar sağlar toodo onu. Olduğundan şu anda bir Azure dosya paylaşımı 5 TB kota sınırı ve 1 TB dosya başına bir dosya boyutu sınırını aklınızda bulundurun. Bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](../../../storage/common/storage-scalability-targets.md) depolama sınırları hakkında bilgi için.

Testler, ancak, SAP HANA yedekleme olmayan & #39 göstermiştir; t şu anda doğrudan CIFS bağlama bu tür ile çalışır. İçinde de belirtildiği [SAP Not 1820529](https://launchpad.support.sap.com/#/notes/1820529) , CIFS önerilmez.

![Bu şekil, SAP HANA Studio'da hello yedekleme iletişiminde bir hata gösterir.](media/sap-hana-backup-file-level/image038.png)

Bu şekilde bir hata hello yedekleme iletişim SAP HANA Studio'da tooback doğrudan tooa CIFS monte Azure dosya paylaşımı çalışırken gösterilmektedir. Böylece varsa toodo VM dosya sistemine standart bir SAP HANA yedekleme önce ve sonra kopyalama hello yedekleme dosyalarını orada tooAzure dosya hizmeti.

![Bu şekilde 929 saniye toocopy 19 SAP HANA yedekleme dosyaları hakkında sürdü gösterilmektedir](media/sap-hana-backup-file-level/image039.png)

Bu şekilde işlem hakkında 929 saniye toocopy 19 SAP HANA yedekleme dosyalarının toplam boyutu kabaca 230 GB toohello Azure dosya paylaşımının sürdü gösterilmektedir.

![Kopyalanan toohello Azure dosya paylaşımı Hello kaynak dizin yapısını hello SAP HANA VM edildi](media/sap-hana-backup-file-level/image040.png)

Bu ekran görüntüsünde bir hello kaynak dizin yapısını hello SAP HANA VM kopyalanan toohello Azure dosya paylaşımı olduğunu görebilirsiniz: bir dizin (hana\_yedekleme\_fsl\_15 gb) ve 19 tek tek yedekleme dosyaları.

SAP HANA dosyası yedeklerini doğrudan desteklendiğinde Azure dosyalarda SAP HANA yedekleme dosyalarını depolamak hello gelecekteki ilginç bir seçenek olabilir. Veya olası hale geldiğinde toomount NFS Azure dosyaları ve hello en yüksek kota sınırına 5 TB'den oldukça yüksektir.

## <a name="next-steps"></a>Sonraki adımlar
* [SAP HANA için yedekleme Kılavuzu Azure sanal makineler üzerinde](sap-hana-backup-guide.md) genel bir bakış ve çalışmaya başlama hakkında bilgi sağlar.
* [SAP HANA yedekleme depolama anlık görüntü tabanlı](sap-hana-backup-storage-snapshots.md) hello depolama anlık görüntü tabanlı yedekleme seçeneği açıklar.
* tooestablish yüksek kullanılabilirlik ve olağanüstü durum kurtarma SAP HANA planlama (büyük örnekler), azure'da nasıl görürüm toolearn [SAP HANA (büyük örnekler) Azure üzerinde yüksek kullanılabilirlik ve olağanüstü durum kurtarma](hana-overview-high-availability-disaster-recovery.md).
