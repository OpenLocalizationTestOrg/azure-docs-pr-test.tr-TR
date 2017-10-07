---
title: "SharePoint için StorSimple bağdaştırıcısı aaaInstall | Microsoft Docs"
description: "Açıklar nasıl tooinstall ve yapılandırma veya bir SharePoint sunucu grubundaki SharePoint için StorSimple bağdaştırıcısı hello kaldırın."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 36c20b75-f2e5-4184-a6b5-9c5e618f79b2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: v-sharos
ms.openlocfilehash: 9a7347232fb80156d93212e6382cdd4fab98a2d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-hello-storsimple-adapter-for-sharepoint"></a>Yükleme ve SharePoint için StorSimple bağdaştırıcısı hello yapılandırma
## <a name="overview"></a>Genel Bakış
Merhaba SharePoint için StorSimple bağdaştırıcısı, Microsoft Azure StorSimple esnek depolama ve veri koruma tooSharePoint sunucu grupları sağlamanıza olanak sağlayan bir bileşendir. Merhaba bağdaştırıcısı toomove ikili büyük nesne (BLOB) hello SQL Server veritabanlarını toohello Microsoft Azure StorSimple karma bulut depolama aygıtı içerikten kullanabilirsiniz.

Merhaba SharePoint için StorSimple bağdaştırıcısı işlevler bir Uzak BLOB Depolama (KKY) sağlayıcısı olarak ve kullandığı SQL Server Uzak BLOB Depolama özelliğini toostore hello StorSimple cihaz tarafından yedeklenen bir dosya sunucusunda yapılandırılmamış SharePoint içeriği (biçiminde hello BLOB'lar).

> [!NOTE]
> SharePoint için StorSimple bağdaştırıcısı Hello SharePoint Server 2010 uzaktan BLOB Depolama (KKY) destekler. SharePoint Server 2010 dış BLOB Depolama (EBS) desteklemez.


* SharePoint için StorSimple bağdaştırıcısı toodownload hello Git çok[SharePoint için StorSimple bağdaştırıcısı] [ 1] hello Microsoft Download Center içinde.
* KKY ve KKY için sınırlamalar planlama hakkında daha fazla bilgi için çok Git[toouse SharePoint 2013'te KKY karar] [ 2] veya [planlama KKY (SharePoint Server 2010)] [3].

Merhaba rest bu genel kısaca hello rolü hello SharePoint için StorSimple bağdaştırıcısı ve hello SharePoint kapasite ve performans sınırlarını yükleyip hello bağdaştırıcısı yapılandırmadan önce bilmeniz olduğunu açıklar. Bu bilgileri gözden geçirdikten sonra çok Git[SharePoint yükleme için StorSimple bağdaştırıcısı](#storsimple-adapter-for-sharepoint-installation) hello bağdaştırıcısı toobegin ayarlama.

### <a name="storsimple-adapter-for-sharepoint-benefits"></a>SharePoint avantajları için StorSimple bağdaştırıcısı
Bir SharePoint sitesi içerik yapılandırılmamış BLOB veri bir veya daha fazla içerik veritabanları olarak depolanır. Varsayılan olarak, bu veritabanlarını SQL Server çalıştıran ve hello SharePoint sunucu grubu içinde bulunan bilgisayarlarda barındırılır. BLOB'lar hızlı bir şekilde şirket içi depolama büyük miktarlarda tüketen boyutunu artırabilirsiniz. Bu nedenle, toofind isteyebilirsiniz başka bir, daha az maliyetli depolama çözümü. SQL Server Uzak Blob Storage (BLOB içeriği hello SQL Server veritabanının dışında hello dosya sistemi depolamak olanak sağlayan KKY) adlı bir teknoloji sağlar. KKY, BLOB'ları hello dosya sisteminde SQL Server çalıştıran hello bilgisayarda bulunabilir veya başka bir sunucu bilgisayardaki hello dosya sistemindeki depolanabilir.

KKY, SharePoint, tooenable KKY SharePoint için StorSimple bağdaştırıcısı hello gibi bir KKY sağlayıcısını kullanmanızı gerektirir. SharePoint için StorSimple bağdaştırıcısı Hello BLOB'lar tooa sunucusu hello Microsoft Azure StorSimple sistemi tarafından desteklenen Taşı süreniz KKY ile çalışır. Microsoft Azure StorSimple sonra hello BLOB verilerini yerel olarak veya hello bulutta kullanıma dayalı depolar. Çok etkin BLOB'ları (genellikle başvurulan tooas Katman 1 veya etkin verileri) bulunan yerel olarak. Daha az aktif veri ve Arşiv verileri hello bulutta bulunur. Bir içerik veritabanında KKY etkinleştirdikten sonra SharePoint'te oluşturulan tüm yeni BLOB içerik hello StorSimple cihazı üzerinde alan ve hello içerik veritabanında depolanır.

KKY Hello Microsoft Azure StorSimple uygulamasını hello aşağıdaki avantajları sağlar:

* Taşıma BLOB içerik tooa ayrı sunucu tarafından SQL Server'da SQL Server yanıtlama hızını iyileştirebilen, hello sorgu yükünü azaltabilir. 
* Azure StorSimple yinelenenleri kaldırma ve sıkıştırma tooreduce veri boyutu kullanır.
* Azure StorSimple hello form yerel ve bulut anlık görüntüleri veri koruması sağlar. Merhaba StorSimple cihazında hello veritabanının kendisi yerleştirirseniz, ayrıca, hello içerik veritabanını ve BLOB'lar birlikte kilitlenmeyle tutarlı bir şekilde yedekleyebilirsiniz. (Merhaba içerik veritabanını toohello aygıt taşıma yalnızca hello StorSimple 8000 serisi cihaz için desteklenir. Bu özellik için hello 5000 veya 7000 Serisi desteklenmiyor.)
* Azure StorSimple yük devretme, dosya ve birim kurtarma (test kurtarma dahil) ve verilerin hızlı geri yükleme gibi olağanüstü durum kurtarma özellikleri içerir.
* StorSimple anlık görüntülerini BLOB veri tooperform öğe düzeyinde kurtarma SharePoint içerik ile veri kurtarma yazılım Kroll Ontrack PowerControls gibi kullanabilirsiniz. (Bu veri kurtarma ayrı bir satın alma yazılımıdır.)
* Merhaba SharePoint için StorSimple bağdaştırıcısı toomanage izin vererek hello SharePoint Merkezi Yönetim Portalı'na, tüm SharePoint Çözüm Merkezi bir konumdan takılan.

BLOB içerik toohello dosya sistemi taşıma diğer maliyet tasarrufu ve avantajları sağlayabilir. Örneğin, KKY kullanarak pahalı Katman 1 depolama hello gereksinimini azaltır ve hello içerik veritabanını küçültür çünkü KKY hello SharePoint sunucu grubunda gerekli veritabanlarını hello sayısını azaltabilirsiniz. Ancak, veritabanı boyutu sınırları ve KKY olmayan içerik hello miktarı gibi diğer faktörlere de depolama gereksinimleri etkileyebilir. Hello maliyetleri ve KKY kullanmanın yararları hakkında daha fazla bilgi için bkz: [planlama KKY (SharePoint Foundation 2010)] [ 4] ve [toouse SharePoint 2013'te KKY karar] [ 5].

### <a name="capacity-and-performance-limits"></a>Kapasite ve performans sınırları
SharePoint çözümünüzde KKY kullanmayı önce test hello performans ve kapasite limitlerini SharePoint Server 2010 ve SharePoint Server 2013 ve nasıl bu sınırları tooacceptable performans ile ilgili farkında olmanız gerekir. Daha fazla bilgi için bkz: [yazılım sınırları ve SharePoint 2013 için sınırları](https://technet.microsoft.com/library/cc262787.aspx).

KKY yapılandırmadan önce hello aşağıdakileri gözden geçirin:

* Bu hello toplam boyutu (içerik veritabanı boyutunu hello) artı ilişkili externalized BLOB hello boyutunu SharePoint tarafından desteklenen hello KKY boyut sınırını aşmadığından içerik hello emin olun. Bu sınır 200 GB'tır. 
  
    **toomeasure içerik veritabanı ve BLOB boyutu**
  
  1. Bu sorgu hello Merkezi Yönetim WFE üzerinde çalıştırın. Merhaba SharePoint Yönetim Kabuğu'nu başlatın ve ardından Windows PowerShell komut tooget hello hello içerik veritabanları boyutunu aşağıdaki hello girin:
     
     `Get-SPContentDatabase | Select-Object -ExpandProperty DiskSizeRequired`
     
      Bu adım hello diskte hello hello içerik veritabanı boyutunu alır.
  2. Her içerik veritabanı üzerindeki hello SQL server kutusunda SQL sorguları SQL Management Studio'da aşağıdaki hello birini çalıştırın ve 1. adımda elde hello sonuç toohello numarasını ekleyin.
     
     SharePoint 2013 üzerinde içerik veritabanları, girin:
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[DocStreams] WHERE [Content] IS NULL`
     
     SharePoint 2010 içerik veritabanlarında, girin:
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[AllDocs] WHERE [Content] IS NULL`
     
     Bu adım hello externalized BLOB'lar hello boyutunu alır.
* Tüm BLOB ve veritabanı içeriği yerel olarak hello StorSimple cihazında saklamanızı öneririz. yüksek kullanılabilirlik için iki düğümlü bir küme Hello StorSimple aygıttır. Merhaba içerik veritabanları ve Blobları hello StorSimple cihazında yerleştirme yüksek düzeyde kullanılabilirlik sağlar.
  
    Geleneksel SQL Server Geçiş en iyi yöntemler toomove hello içerik veritabanını toohello StorSimple cihazı kullanın. Yalnızca tüm BLOB içeriğinin hello veritabanından taşınan toohello dosya paylaşımı üzerinden KKY sonra hello veritabanını taşıyın. Toomove hello içerik veritabanını toohello StorSimple cihazı seçerseniz, birincil bir birim olarak hello aygıtta hello içerik veritabanı depolama yapılandırmanızı öneririz.
* Microsoft Azure katmanlı birimleri kullanıyorsanız, StorSimple içinde, içeriği yerel olarak depolanan hello StorSimple cihazında tooguarantee katmanlı tooMicrosoft Azure bulut depolama olmaz yolu yoktur. Bu nedenle, yerel olarak sabitlenmiş StorSimple birimlerini SharePoint KKY birlikte kullanmanızı öneririz. Bu, tüm BLOB içeriğinin hello StorSimple cihazında yerel olarak kalır ve taşınan tooMicrosoft Azure değil garanti eder.
* Merhaba StorSimple cihazında hello içerik veritabanları depolamayın KKY destekleyen geleneksel SQL Server yüksek kullanılabilirlik en iyi uygulamaları kullanın. SQL Server Kümelemesi KKY destekler, SQL Server güncelleştirilirken yansıtmayı desteklemez. 

> [!WARNING]
> KKY etkinleştirmediyseniz hello içerik veritabanını toohello StorSimple cihazı taşıma önermiyoruz. Bu sınanmamış bir yapılandırmadır.

## <a name="storsimple-adapter-for-sharepoint-installation"></a>StorSimple bağdaştırıcısı SharePoint yükleme için
SharePoint için StorSimple bağdaştırıcısı hello yükleyebilmek için önce hello StorSimple cihazı yapılandırma ve hello SharePoint sunucu grubu ve SQL Server örneğini oluşturmada tüm önkoşulları karşıladığından emin olun. Bu öğretici, yükleme ve SharePoint için StorSimple bağdaştırıcısı hello yükseltme yordamları yanı sıra yapılandırma gereksinimlerini açıklar.

## <a name="configure-prerequisites"></a>Önkoşulları yapılandırma
SharePoint için StorSimple bağdaştırıcısı hello yükleyebilmek için önce hello StorSimple cihazı, SharePoint sunucu grubu ve SQL Server örneğini oluşturmada hello aşağıdaki önkoşulları karşıladığından emin olun.

### <a name="system-requirements"></a>Sistem gereksinimleri
Merhaba SharePoint için StorSimple bağdaştırıcısı çalışır hello ile aşağıdaki donanım ve yazılım:

* Desteklenen işletim sistemi-Windows Server 2008 R2 SP1, Windows Server 2012 veya Windows Server 2012 R2
* Desteklenen SharePoint sürümleri – SharePoint Server 2010 veya SharePoint Server 2013
* Desteklenen SQL Server sürümleri – SQL Server 2008 Enterprise Edition, SQL Server 2008 R2 Enterprise Edition veya SQL Server 2012 Enterprise Edition
* StorSimple cihaz-desteklenen StorSimple 8000 serisi, StorSimple 7000 Serisi veya StorSimple 5000 Serisi.

### <a name="storsimple-device-configuration-prerequisites"></a>StorSimple cihaz yapılandırma önkoşulları
Merhaba StorSimple cihazı blok cihazı ve bu nedenle hello veri barındırılabilen bir dosya sunucusu gerekir. Merhaba SharePoint grubundan var olan bir sunucu yerine ayrı bir sunucu kullanmanızı öneririz. Bu dosya sunucusunu gerekir olması üzerinde hello aynı yerel ağ (LAN) hello SQL Server bilgisayarı olarak içerik veritabanlarını barındıran hello.

> [!TIP]
> * Yüksek kullanılabilirlik için SharePoint grubunu yapılandırmak, yüksek kullanılabilirlik için hello dosya sunucusu da dağıtmanız gerekir.
> * Merhaba StorSimple cihazında hello içerik veritabanını depolamayın KKY desteği geleneksel yüksek kullanılabilirlik en iyi uygulamaları kullanın. SQL Server Kümelemesi KKY destekler, SQL Server güncelleştirilirken yansıtmayı desteklemez. 


StorSimple Cihazınızı doğru bir şekilde yapılandırıldığından ve o uygun birimleri toosupport SharePoint dağıtımınızı yapılandırılmış ve SQL Server bilgisayarınızdan erişilebilir olduğundan emin olun. Çok Git[şirket içi StorSimple Cihazınızı dağıtma](storsimple-8000-deployment-walkthrough-u2.md) , henüz dağıtılan ve StorSimple Cihazınızı yapılandırılmışsa. Merhaba StorSimple cihazı Hello IP adresini not edin; Bu SharePoint yükleme sırasında StorSimple bağdaştırıcısı gerekir.

Ek olarak, BLOB externalization için kullanılan bu hello birim toobe hello aşağıdaki gereksinimleri karşıladığından emin olun:

* Merhaba birim 64 KB ayırma birimi boyutu ile biçimlendirilmiş olması gerekir.
* Web front end (WFE) ve uygulama sunucuları bir Evrensel Adlandırma Kuralı (UNC) yolu üzerinden mümkün tooaccess hello birim olması gerekir.
* Merhaba SharePoint sunucu grubu yapılandırılmış toowrite toohello birim olması gerekir.

> [!NOTE]
> Yükleyip hello bağdaştırıcısı yapılandırdıktan sonra tüm BLOB externalization hello StorSimple cihazı üzerinden gitmesi gerekir (Merhaba aygıt hello birimleri tooSQL sunucu sunmak ve hello depolama katmanları yönetme). Diğer hedefler için BLOB externalization kullanamazsınız.


Merhaba BLOB toouse StorSimple Snapshot Manager tootake anlık görüntülerini planlamak ve hello SQL yazıcı hizmeti tooimplement kullanabilmesi için hello veritabanı sunucusunda emin tooinstall StorSimple Snapshot Manager olması veriler, veritabanı, Windows birim gölge kopyası hello Hizmeti (VSS).

> [!IMPORTANT]
> StorSimple Snapshot Manager hello SharePoint VSS yazıcısı desteklemez ve SharePoint verilerinin uygulamayla tutarlı anlık görüntülerini alamıyor. Bir SharePoint senaryosunda, StorSimple Snapshot Manager yalnızca kilitlenme tutarlı yedeklemeler sağlar.


## <a name="sharepoint-farm-configuration-prerequisites"></a>SharePoint grubu yapılandırma önkoşulları
SharePoint sunucu grubunuzu doğru şu şekilde yapılandırıldığından emin olun:

* SharePoint sunucu grubunuzu sağlam durumda olduğunu doğrulayın ve hello aşağıdakileri denetleyin:
* Tüm SharePoint WFE ve uygulama sunucuları hello grubunda kayıtlı çalıştıran ve üzerinde hello StorSimple bağdaştırıcısı SharePoint için yükleyeceğiniz hello sunucusundan ping.
* Merhaba SharePoint Süreölçer hizmeti (SPTimerV3 veya SPTimerV4), her bir WFE sunucusunda ve uygulama sunucusu çalışıyor.
* Merhaba SharePoint Süreölçer hizmeti hem hello IIS uygulama havuzu altında SharePoint Merkezi yönetim sitesinin çalışır durumda Merhaba yönetici ayrıcalıklarına sahip.
* Internet Explorer Artırılmış güvenlik bağlamı (IE ESC) devre dışı bırakıldığından emin olun. Bu adımları toodisable IE ESC izleyin:
  
  1. Internet Explorer'ın tüm örneklerini kapatın.
  2. Merhaba Sunucu Yöneticisi'ni başlatın.
  3. Merhaba sol bölmede **yerel sunucu**.
  4. Üzerinde Hello bölmesini, sonraki çok sağ**IE Artırılmış Güvenlik Yapılandırması**, tıklatın **üzerinde**.
  5. Altında **Yöneticiler**, tıklatın **devre dışı**.
  6. **Tamam** düğmesine tıklayın.

## <a name="remote-blob-storage-rbs-prerequisites"></a>Uzak BLOB Depolama (KKY) Önkoşullar
SQL Server'ın desteklenen bir sürümünü kullandığınızdan emin olun. Yalnızca hello aşağıdaki sürümler açıp açmadığını ve desteklenen toouse KKY şunlardır:

* SQL Server 2008 Enterprise Edition
* SQL Server 2008 R2 Enterprise Edition
* SQL Server 2012 Enterprise Edition

StorSimple cihazı hello bu birimlerin sunar yalnızca tooSQL sunucu BLOB'ları üzerinde externalized. Hiçbir bir hedef BLOB externalization için desteklenir.

Tüm önkoşul yapılandırma adımlarını tamamladıktan sonra çok Git[yükleme hello SharePoint için StorSimple bağdaştırıcısı](#install-the-storsimple-adapter-for-sharepoint).

## <a name="install-hello-storsimple-adapter-for-sharepoint"></a>SharePoint için StorSimple bağdaştırıcısı Hello yükleyin
SharePoint için adımları tooinstall hello StorSimple bağdaştırıcısı aşağıdaki hello kullanın. Merhaba yazılım yeniden yüklüyorsanız, bkz: [yükseltme veya SharePoint için StorSimple bağdaştırıcısı hello yeniden](#upgrade-or-reinstall-the-storsimple-adapter-for-sharepoint). Merhaba, SharePoint sunucu grubundaki SharePoint veritabanlarına toplam sayısı Hello yükleme için gerekli hello zaman bağlıdır.

[!INCLUDE [storsimple-install-sharepoint-adapter](../../includes/storsimple-install-sharepoint-adapter.md)]

## <a name="configure-rbs"></a>KKY yapılandırın
SharePoint için StorSimple bağdaştırıcısı hello yükledikten sonra KKY aşağıdaki yordamı hello açıklandığı gibi yapılandırın.

> [!TIP]
> Merhaba SharePoint Yönetim Merkezi sayfasında, etkin veya devre dışı hello SharePoint grubundaki her bir içerik veritabanına KKY toobe izin vererek içine Hello SharePoint için StorSimple bağdaştırıcısı takılan. Ancak, etkinleştirme veya hello içerik veritabanını KKY devre dışı bırakma, Grup yapılandırmanıza bağlı olarak, kısa bir süre içinde hello SharePoint web ön uç (WFE) hello kullanılabilirliğini kesintiye uğratabilir bir IIS sıfırlama neden olur. (Ön uç yük dengeleyici, hello geçerli sunucu iş yükü ve benzeri hello kullanımı gibi etkenlere sınırlamak veya bu kesintiyi ortadan kaldırmak.) kesilme kullanıcılardan tooprotect, etkinleştirme veya KKY yalnızca bir planlı bakım penceresi sırasında devre dışı öneririz.


[!INCLUDE [storsimple-sharepoint-adapter-configure-rbs](../../includes/storsimple-sharepoint-adapter-configure-rbs.md)]

## <a name="configure-garbage-collection"></a>Çöp toplama yapılandırın
Bir SharePoint sitesinden silinen nesneleri, bunlar otomatik olarak KKY depolama birimi hello silinmez. Bunun yerine, bir zaman uyumsuz, arka plan bakım program yalnız bırakılmış BLOB'lar hello dosya deposundan siler. Sistem yöneticileri bu işlemi toorun düzenli aralıklarla zamanlayabilir veya bunu gerektiğinde başlatabilirsiniz.

KKY etkinleştirdiğinizde bu bakım programı (Microsoft.Data.SqlRemoteBlobs.Maintainer.exe) tüm SharePoint WFE sunucuları ve uygulama sunucuları otomatik olarak yüklenir. Merhaba program konumu aşağıdaki hello yüklü: *önyükleme sürücüsü*: \Program SQL Uzak Blob Depolama 10.50\Maintainer\

Yapılandırma ve hello bakım programı kullanma hakkında daha fazla bilgi için bkz: [korumak KKY SharePoint Server 2013'te][8].

> [!IMPORTANT]
> yoğun kaynak Hello KKY Bakımcı programdır. Toorun yalnızca hello SharePoint grubu üzerinde açık etkinliğin dönemlerde ayarlamanız gerekir.


### <a name="delete-orphaned-blobs-immediately"></a>Yalnız bırakılmış BLOB'ları hemen silme
Yalnız bırakılmış toodelete BLOB'ları hemen gerekiyorsa, yönergeleri izleyerek hello kullanabilirsiniz. Bu yönergeleri nasıl bu bir SharePoint 2013 ortamında bileşenleri aşağıdaki hello ile yapılabilir bir örnek olduğuna dikkat edin:

* WSS_Content Hello içerik veritabanı adı değil.
* Merhaba SQL Server SHRPT13 SQL12\SHRPT13 adıdır.
* Merhaba web uygulaması adı SharePoint – 80 ' dir.

[!INCLUDE [storsimple-sharepoint-adapter-garbage-collection](../../includes/storsimple-sharepoint-adapter-garbage-collection.md)]

## <a name="upgrade-or-reinstall-hello-storsimple-adapter-for-sharepoint"></a>Yükseltme veya SharePoint için StorSimple bağdaştırıcısı hello yeniden
Yordam tooupgrade SharePoint sunucusu aşağıdaki hello kullanın ve sonra SharePoint veya toosimply yükseltme için StorSimple bağdaştırıcısını yeniden veya varolan bir SharePoint sunucu grubuna hello bağdaştırıcısı yeniden yükleyin.

> [!IMPORTANT]
> SharePoint yazılım ve/veya yükseltme tooupgrade denemeden önce aşağıdaki bilgilerle hello gözden geçirmek veya SharePoint için StorSimple bağdaştırıcısı hello yeniden yükleyin:
> 
> * Tüm daha önce KKY aracılığıyla tooexternal depolamaya hello yeniden yükleme işlemi tamamlanana kadar kullanılamaz taşınan dosyaları ve hello KKY özelliği yeniden etkinleştirildi. toolimit kullanıcı etkisi, herhangi bir yükseltme veya planlı bakım penceresi sırasında yeniden gerçekleştirin.
> * Hello yükseltme/yeniden yükleme için gerekli olan hello süresi hello SharePoint sunucu grubundaki SharePoint veritabanlarına toplam sayısı hello bağlı olarak değişebilir.
> * Merhaba yükseltme/yeniden yükleme tamamlandıktan sonra hello içerik veritabanları için tooenable KKY gerekir. Bkz: [yapılandırma KKY](#configure-rbs) daha fazla bilgi için.
> * Veritabanları (200'den büyük) çok sayıda sahip SharePoint grubu için KKY yapılandırıyorsanız, hello **SharePoint Yönetim Merkezi** sayfa zaman aşımına olabilir. Bu gerçekleşirse, hello sayfayı yenileyin. Bu hello yapılandırma işlemi etkilemez.


[!INCLUDE [storsimple-upgrade-sharepoint-adapter](../../includes/storsimple-upgrade-sharepoint-adapter.md)]

## <a name="storsimple-adapter-for-sharepoint-removal"></a>StorSimple bağdaştırıcısı SharePoint kaldırma
yordamları izleyerek hello nasıl hello BLOB'ları toohello SQL Server veritabanlarını yedekleyin ve kaldırın toomove hello StorSimple bağdaştırıcısı SharePoint için açıklanmaktadır. 

> [!IMPORTANT]
> Merhaba bağdaştırıcı yazılımı kaldırmadan önce toomove hello BLOB'lar geri toohello içerik veritabanlarına sahip.


### <a name="before-you-begin"></a>Başlamadan önce
Merhaba veri toohello SQL Server veritabanlarını yedekleyin ve hello bağdaştırıcı kaldırma işlemini başlatmak geçmeden önce aşağıdaki bilgilerle hello Topla:

* KKY etkin olduğu tüm hello veritabanlarının Hello adlarını
* BLOB deposu hello Hello UNC yolunu yapılandırılmış

### <a name="move-hello-blobs-back-toohello-content-databases"></a>Merhaba BLOB'lar geri toohello içerik veritabanlarını taşıma
SharePoint yazılım için StorSimple bağdaştırıcısı hello kaldırmadan önce tüm hello externalized geri toohello SQL Server veritabanlarını olan BLOB'ları geçirmeniz gerekir. Tüm hello BLOB'lar geri toohello içerik veritabanları taşımadan önce SharePoint için StorSimple bağdaştırıcısı toouninstall hello denerseniz, aşağıdaki uyarı iletisi hello görürsünüz.

![Uyarı iletisi](./media/storsimple-adapter-for-sharepoint/sasp1.png)

#### <a name="toomove-hello-blobs-back-toohello-content-databases"></a>toomove hello BLOB'lar geri toohello içerik veritabanları
1. Merhaba externalized nesnelerin her biri indirin.
2. Açık hello **SharePoint Yönetim Merkezi** sayfasında ve çok Gözat**sistem ayarlarını**.
3. Altında **Azure StorSimple**, tıklatın **StorSimple bağdaştırıcısı yapılandırma**.
4. Merhaba üzerinde **StorSimple bağdaştırıcısını yapılandırın** hello sayfasında, **devre dışı** her bir dış BLOB depolama biriminden tooremove istediğiniz hello içerik veritabanı aşağıdaki düğmesine. 
5. SharePoint'ten Hello nesnelerini silin ve ardından yeniden yükleyin.

Alternatif olarak, hello Microsoft kullanabilirsiniz` RBS Migrate()` PowerShell cmdlet'i ile SharePoint dahil. Daha fazla bilgi için bkz: [içine veya dışına KKY İçerik Geçişi](https://technet.microsoft.com/library/ff628255.aspx).

Merhaba BLOB'lar geri toohello içerik veritabanını taşıdıktan sonra toohello sonraki adıma gidin: [kaldırma hello bağdaştırıcısı](#uninstall-the-adapter).

### <a name="uninstall-hello-adapter"></a>Merhaba Bağdaştırıcısı'nı kaldırma
Merhaba BLOB'lar geri toohello SQL Server veritabanlarını taşıdıktan sonra SharePoint için seçenekleri toouninstall hello StorSimple bağdaştırıcısı aşağıdaki hello birini kullanın.

#### <a name="toouse-hello-installation-program-toouninstall-hello-adapter"></a>toouse hello yükleme programı toouninstall hello bağdaştırıcısı
1. Yönetici ayrıcalıkları toolog toohello web ön uç sunucusunda (WFE) sahip bir hesap kullanın.
2. Merhaba StorSimple bağdaştırıcısı SharePoint yükleyici için çift tıklayın. Merhaba Kurulum Sihirbazı'nı başlatır.
   
    ![Kurulum Sihirbazı](./media/storsimple-adapter-for-sharepoint/sasp2.png)
3. **İleri**’ye tıklayın. Sayfa aşağıdaki hello görüntülenir.
   
    ![Kurulum Sihirbazı'nı Kaldır sayfası](./media/storsimple-adapter-for-sharepoint/sasp3.png)
4. Tıklatın **kaldırmak** tooselect hello kaldırma işlemi. Sayfa aşağıdaki hello görüntülenir.
   
    ![Kurulum Sihirbazı onay sayfası](./media/storsimple-adapter-for-sharepoint/sasp4.png)
5. Tıklatın **kaldırmak** tooconfirm hello kaldırma. ilerleme durumu sayfası aşağıdaki hello görüntülenir.
   
    ![Kurulum Sihirbazı'nı ilerleme durumu sayfası](./media/storsimple-adapter-for-sharepoint/sasp5.png)
6. Merhaba kaldırma tamamlandığında hello bitiş sayfası görüntülenir. Tıklatın **son** tooclose hello Kurulum Sihirbazı.

#### <a name="toouse-hello-control-panel-toouninstall-hello-adapter"></a>toouse hello Denetim Masası toouninstall hello bağdaştırıcısı
1. Merhaba Denetim Masası'nı açın ve ardından **programlar ve Özellikler**.
2. Seçin **SharePoint için StorSimple bağdaştırıcısı**ve ardından **kaldırma**.

## <a name="next-steps"></a>Sonraki adımlar
[StorSimple hakkında daha fazla bilgi](storsimple-overview.md).

<!--Reference links-->
[1]: https://www.microsoft.com/download/details.aspx?id=44073
[2]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[3]: https://technet.microsoft.com/library/ff628583(v=office.14).aspx
[4]: https://technet.microsoft.com/library/ff628569(v=office.14).aspx
[5]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[8]: https://technet.microsoft.com/en-us/library/ff943565.aspx
