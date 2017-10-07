---
title: "aaaWhat StorSimple anlık görüntü Yöneticisi nedir? | Microsoft Belgeleri"
description: "Merhaba StorSimple Snapshot Manager, kendi mimarisi ve özelliklerini açıklar."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6094c31e-e2d9-4592-8a15-76bdcf60a754
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: v-sharos
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79ce7b7e1970ac862038af2a0e67065b6fb6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toostorsimple-snapshot-manager"></a>Bir giriş tooStorSimple anlık görüntü Yöneticisi

## <a name="overview"></a>Genel Bakış
StorSimple Snapshot Manager, veri koruma ve Microsoft Azure StorSimple ortamda yedekleme yönetimini basitleştirir Microsoft Yönetim Konsolu (MMC) ek bileşenidir. StorSimple Snapshot Manager ile Microsoft Azure StorSimple verileri hello veri merkezi ve hello bulut tek bir tümleşik depolama çözümü olarak, bu nedenle yedekleme işlemlerini basitleştirir ve maliyetlerini azaltır yönetebilirsiniz.

Bu genel bakışta hello StorSimple Snapshot Manager sunar, özelliklerini açıklar ve Microsoft Azure StorSimple kendi rolünde açıklanmaktadır. 

Merhaba StorSimple cihazı, StorSimple Yöneticisi hizmetiniz, StorSimple Snapshot Manager ve StorSimple bağdaştırıcısı SharePoint için de dahil olmak üzere hello tüm Microsoft Azure StorSimple sistemi, genel bir bakış için bkz: [StorSimple 8000 serisi: karma bulut depolama çözümü](storsimple-overview.md). 

> [!NOTE]
> * StorSimple Snapshot Manager toomanage Microsoft Azure StorSimple sanal (olarak da bilinen StorSimple sanal cihazlar şirket) diziler kullanamazsınız.
> * StorSimple Cihazınızda tooinstall StorSimple güncelleştirme 2 düşünüyorsanız, emin toodownload hello en son sürümünü StorSimple anlık görüntü Yöneticisi'nin olması ve yüklemeniz **StorSimple güncelleştirme 2 yüklemeden önce**. Merhaba en son sürümünü StorSimple anlık görüntü Yöneticisi'nin geriye dönük olarak uyumludur ve Microsoft Azure StorSimple serbest bırakılmış tüm sürümleri ile çalışır. StorSimple anlık görüntü Yöneticisi'nin hello önceki sürümü kullanıyorsanız, tooupdate gerekir (gerektirmeyen toouninstall hello önceki sürüm hello yeni sürümü yüklemeden önce) BT.
> 
> 

## <a name="storsimple-snapshot-manager-purpose-and-architecture"></a>StorSimple Snapshot Manager amacı ve mimarisi
StorSimple Snapshot Manager sağlar toocreate tutarlı kullanabileceğiniz bir Merkezi Yönetim Konsolu, zaman içinde nokta yedek kopyalarını yerel ve bulut veri. Örneğin, hello konsola kullanabilirsiniz:

* Yapılandırma, yedekleme ve birimleri silin.
* Birimi yedeklenmiş verileri grupları tooensure uygulama tutarlı olduğundan.
* Böylece verilerin belirlenmiş bir zamanlamayla yedeklendiğinden yedekleme ilkelerini yönetin.
* Yerel oluşturun ve bulut hello bulutta depolanan ve olağanüstü durum kurtarma için kullanılan anlık görüntüler.

Merhaba StorSimple Snapshot Manager hello konaktaki hello VSS sağlayıcısı ile kaydedilmiş uygulamaları hello listesini getirir. Ardından, toocreate uygulamayla tutarlı yedeklemeler, hello birimler bir uygulama tarafından kullanılan ve birim grupları tooconfigure öneren denetler. StorSimple Snapshot Manager uygulamayla tutarlı olan bu birim grupları toogenerate yedek kopyaları kullanır. (Tüm ilgili dosyaları ve veritabanları eşitlenir ve zaman içinde belirli bir noktada Merhaba uygulaması hello true durumunu temsil olduğunda uygulama tutarlılığı bulunmaktadır.) 

StorSimple Snapshot Manager yedeklemeler yalnızca hello değişiklikler hello son yedeklemeden yakalama artımlı anlık görüntüleri hello şeklinde. Sonuç olarak, yedeklemeleri daha az depolama alanı gerektirir ve oluşturulabilir ve hızlı bir şekilde geri. StorSimple Snapshot Manager anlık görüntüleri uygulama ile tutarlı verileri yakalama hello Windows Birim Gölge Kopyası Hizmeti (VSS) tooensure kullanır. (Daha fazla bilgi için Windows birim gölge kopyası hizmeti bölümü ile tümleştirme toohello gidin.) StorSimple Snapshot Manager ile yedekleme zamanlamaları oluşturabilir veya gerektiğinde hemen yedek alabilir. Yedekleme, StorSimple Snapshot Manager sağlar toorestore verilerden gerekiyorsa yerel Kataloğu'ndan veya Bulut anlık görüntüleri seçin. Azure StorSimple veri kullanılabilirliği geri yükleme işlemleri sırasında gecikmeler önleyen gerektiğinde, yalnızca gerekli hello verileri geri yükler.)

![StorSimple Snapshot Manager mimarisi](./media/storsimple-what-is-snapshot-manager/HCS_SSM_Overview.png)

**StorSimple Snapshot Manager mimarisi** 

## <a name="support-for-multiple-volume-types"></a>Birden çok birim türleri için destek
Merhaba StorSimple Snapshot Manager tooconfigure ve şu birimlerin türlerini hello geri kullanabilirsiniz: 

* **Temel birimleri** – bir temel disk üzerinde tek bir bölüm temel bir birimdir. 
* **Basit birimler** – basit bir birimi tek bir dinamik diskteki disk alanını içeriyor dinamik bir birimdir. Tek bir bölge diskteki basit birim oluşur veya aynı disk üzerinde birbirine bağlı birden çok bölgeye hello. (Yalnızca dinamik disklerde basit birimler oluşturabilirsiniz.) Basit birimler hataya dayanıklı değildir.
* **Dinamik birimler** – dinamik bir birim bir dinamik disk üzerinde oluşturulan bir birimdir. Dinamik diskler, bir bilgisayarda dinamik diskler üzerinde bulunan birimlerle ilgili bir veritabanı tootrack bilgileri kullanın. 
* **Yansıtma ile dinamik birimler** – yansıtma ile dinamik birimler hello RAID 1 mimarisine yerleşiktir. RAID 1 ile özdeş veriler yansıtılmış kümesini üreten iki veya daha fazla diske yazılır. Merhaba içeren herhangi bir disk okuma isteği daha sonra ele alınabilir veri istedi.
* **Küme Paylaşılan birimleri** – Küme Paylaşılan birimleriyle (CSV), yük devretme kümesinde birden çok düğümün aynı anda okuyabilir veya toohello yazma aynı disk. Yük devretme tek bir düğüm tooanother düğümünden hızlı bir şekilde, sürücü sahipliğinin veya takma, kaldırma ve bir birim kaldırma bir değişiklik gerektirmeden oluşabilir. 

> [!IMPORTANT]
> Csv ve CSV olmayan hello içinde karıştırmamanızı aynı anlık görüntü. Csv ve CSV olmayan bir anlık görüntü içinde karıştırılması desteklenmiyor. 
> 
> 

StorSimple Snapshot Manager toorestore birimin tamamını gruplarını kullanın ya da ayrı birimleri kopyalamak ve tek tek dosyaların kurtarın.

* [Birim ve birim grupları](#volumes-and-volume-groups) 
* [Yedekleme türleri ve yedekleme ilkeleri](#backup-types-and-backup-policies) 

StorSimple Snapshot Manager özellikleri hakkında daha fazla bilgi için ve nasıl toouse, görebileceği [StorSimple Snapshot Manager kullanıcı arabirimini](storsimple-use-snapshot-manager.md).

## <a name="volumes-and-volume-groups"></a>Birim ve birim grupları
Birimler oluşturabilir ve bunları Toplu gruplar halinde yapılandırmanız ile StorSimple Snapshot Manager. 

StorSimple Snapshot Manager uygulamayla tutarlı olan birim grupları toocreate yedek kopyaları kullanır. Tüm ilgili dosyaları ve veritabanları eşitlenir ve hello gerçek bir uygulamada belirli bir noktada zaman durumunu temsil eden olduğunda uygulama tutarlılığı bulunmaktadır. Birim grupları (olarak da bilinen olduğu *tutarlılık grupları*) form hello temel bir yedekleme veya geri yükleme işi.

Birim grupları olan değil hello birim kapsayıcıları aynıdır. Birim kapsayıcısı, bulut depolama hesabı ve şifreleme ve bant genişliği tüketimini gibi diğer öznitelikleri paylaşan bir veya daha fazla birimleri içerir. Tek bir birim kapsayıcısı ölçülü kaynak too256 StorSimple birimleri içerebilir. Birim kapsayıcıları hakkında daha fazla bilgi için çok Git[birim kapsayıcıları yönetmek](storsimple-manage-volume-containers.md). Birim grupları toofacilitate yedekleme işlemlerini yapılandırmak birimleri koleksiyonlarıdır. Toodifferent birim kapsayıcıları ait, tek bir birimde grubunda yerleştirin ve sonra o birim grubu için bir yedekleme ilkesi oluşturmak iki birim seçerseniz, her birim hello uygun birim kapsayıcısı hello uygun depolama kullanarak yedeklenecek hesabı.

> [!NOTE]
> Bir birim grubundaki tüm birimleri, bir tek bulut hizmeti sağlayıcısını gelmesi gerekir.
> 
> 

## <a name="integration-with-windows-volume-shadow-copy-service"></a>Windows birim gölge kopyası hizmeti ile tümleştirme
StorSimple Snapshot Manager hello Windows Birim Gölge Kopyası Hizmeti (VSS) toocapture uygulama ile tutarlı verileri kullanır. VSS, VSS kullanabilen uygulamaların toocoordinate hello artımlı anlık görüntü oluşturmaya ile iletişim kurarak uygulama tutarlılığı kolaylaştırır. VSS anlık görüntülerinin alınma hello uygulamaları geçici olarak devre dışı veya deneniyor, olmasını sağlar. 

VSS Hello StorSimple Snapshot Manager uygulaması, SQL Server ve genel NTFS birimleri ile çalışır. Merhaba işlem aşağıdaki gibidir: 

1. Genellikle veri yönetimi ve koruma çözümü (StorSimple Snapshot Manager gibi) veya bir yedekleme uygulaması olan, bir istek sahibi VSS çağırır ve hello yazan yazılım hello hedef uygulamada toogather bilgileri ister.
2. VSS kişiler yazıcısı bileşeni tooretrieve hello veri açıklamasını hello. Merhaba yazan yedeklenen hello veri toobe hello açıklaması döndürür. 
3. VSS Merhaba yazan tooprepare hello uygulaması yedekleme için işaret eder. Merhaba yazan hello verileri yedekleme açık hareketler tamamlayarak işlem günlüklerinin ve benzeri güncelleştirme hazırlar ve VSS'yi bildirir
4. VSS hello yazan tootemporarily Dur hello uygulama verilerini depolayan ve hello gölge kopya oluşturulurken hiçbir veri toohello birim yazılmaz emin olun ister. Bu adım, veri tutarlılığı sağlar ve 60 saniyeden daha uzun sürer.
5. VSS hello sağlayıcısı toocreate hello gölge kopya bildirir. Yazılım veya donanım tabanlı, olabilir sağlayıcıları çalışmakta olan ve isteğe bağlı olarak bunları gölge kopyalarını oluşturun hello birimleri yönetin. Merhaba sağlayıcısı hello gölge kopyasını oluşturur ve tamamlandığında VSS bildirir.
6. G/ç sürdürebilirsiniz VSS kişiler hello yazan toonotify hello uygulama ve ayrıca g/ç sırasında gölge başarıyla duraklatıldı tooconfirm oluşturma kopyalayın. 
7. Merhaba kopyalama başarılı olduysa, VSS döndürür hello kopyanın konumu toohello istek sahibi. 
8. Merhaba gölge kopya oluşturulduğu sırada veri yazılmışsa hello yedekleme tutarsız olur. VSS hello gölge kopya siler ve hello istek sahibi bildirir. Merhaba istek sahibi hello yedekleme işlemi otomatik olarak yineleyin veya hello yönetici tooretry bildir, daha sonra.

Aşağıdaki çizimde hello bakın.

![VSS işlemi](./media/storsimple-what-is-snapshot-manager/HCS_SSM_VSS_process.png)

**Windows birim gölge kopyası hizmeti işlemi** 

## <a name="backup-types-and-backup-policies"></a>Yedekleme türleri ve yedekleme ilkeleri
StorSimple Snapshot Manager ile verileri yedeklemek ve yerel olarak ve hello bulutta saklayın. StorSimple Snapshot Manager tooback verileri hemen kullanabilirsiniz veya yedekleme İlkesi toocreate bir zamanlama yedek otomatik olarak almak için kullanabilirsiniz. Yedekleme ilkelerini de kaç anlık görüntü tutulacağını toospecify etkinleştirin. 

### <a name="backup-types"></a>Yedekleme türleri
StorSimple Snapshot Manager toocreate hello yedekleme türleri aşağıdaki kullanabilirsiniz:

* **Yerel anlık görüntüleri** – yerel anlık görüntüler hello StorSimple cihazında depolanmış birim verilerini zaman içinde nokta kopyalarını değildir. Genellikle, bu yedekleme türü oluşturulabilir ve hızlı bir şekilde geri. Yerel bir yedek kopya gibi yerel bir anlık görüntü kullanabilirsiniz.
* **Bulut anlık görüntüleri** – bulut anlık görüntüleri olan hello bulutta depolanan birim verilerini zaman içinde nokta kopyalarını. Bir bulut anlık görüntüsü eşdeğerdir farklı, şirket dışı depolama sisteminizde çoğaltılan tooa anlık görüntü. Bulut anlık görüntüleri olağanüstü durum kurtarma senaryolarında özellikle kullanışlıdır.

### <a name="on-demand-and-scheduled-backups"></a>İsteğe bağlı ve zamanlanmış yedeklemeler
StorSimple Snapshot Manager ile oluşturulan hemen bir kerelik yedekleme toobe başlatabilir veya yedekleme işlemleri yinelenen bir yedekleme İlkesi tooschedule kullanabilirsiniz.

Bir yedekleme İlkesi tooschedule düzenli yedeklemeler kullanabileceğiniz otomatik kurallar kümesidir. Bir yedekleme İlkesi toodefine hello sıklığı ve parametreleri bir özel birim grubu anlık görüntülerini almak için sağlar. İçin her iki yerel ilkeleri toospecify başlangıç ve sona erme tarihleri, saat, sıklıklarını ve saklama gereksinimleri kullanabilirsiniz ve bulut anlık görüntüleri. Tanımladığınız hemen sonra bir ilke uygulanır. 

StorSimple Snapshot Manager tooconfigure kullanın veya yedekleme ilkeleri gerektiğinde yeniden yapılandırın. 

Oluşturduğunuz her bir yedekleme ilkesi için bilgisinden hello yapılandırın:

* **Ad** – hello hello benzersiz adı seçili yedekleme ilkesi.
* **Tür** – hello yedekleme İlkesi; yerel anlık görüntü veya Bulut anlık görüntüsü türü.
* **Birim grubu** – hello birim grubu toowhich seçili hello yedekleme İlkesi atanır.
* **Bekletme** – hello yedek kopyaları tooretain sayısı. Merhaba onay **tüm** kutusunda, birim başına yedek kopyaları hello sayısı sınırına kadar tüm yedek kopyaları korunur, hangi noktası hello ilke başarısız olacak ve bir hata iletisi oluşturur. Alternatif olarak, yedeklemeleri tooretain (arasında 1 ile 64) sayısını belirtebilirsiniz.
* **Tarih** – hello yedekleme İlkesi ne zaman oluşturulduğu başlangıç tarihi.

Yedekleme ilkelerini yapılandırma hakkında daha fazla bilgi için çok Git[StorSimple anlık görüntü Yöneticisi'ni kullanın toocreate ve yedekleme ilkelerini yönetme](storsimple-snapshot-manager-manage-backup-policies.md).

### <a name="backup-job-monitoring-and-management"></a>Yedekleme işi izleme ve yönetim
Merhaba StorSimple Snapshot Manager toomonitor kullanın ve yaklaşan, zamanlanmış ve tamamlanan yedekleme işleri yönetin. Ayrıca, StorSimple Snapshot Manager Kataloğu tamamlandı too64 yedekleri kurma sağlar. Merhaba katalog toofind kullanın ve birimleri veya tek tek dosyaları geri yükleyin. 

Yedekleme işlerini izleme hakkında daha fazla bilgi için çok gidin[StorSimple anlık görüntü Yöneticisi'ni kullanın tooview ve yedekleme işlerini yönetme](storsimple-snapshot-manager-manage-backup-jobs.md).

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [StorSimple Snapshot Manager tooadminister StorSimple çözümünüzün kullanarak](storsimple-snapshot-manager-admin.md).
* Karşıdan [StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220).

