---
title: aaaStorSimple 8000 serisi NetBackup olan yedekleme hedefi olarak | Microsoft Docs
description: "Merhaba StorSimple yedekleme hedefi VERITAS NetBackup yapılandırmayla açıklar."
services: storsimple
documentationcenter: 
author: harshakirank
manager: matd
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: hkanna
ms.openlocfilehash: 7d032bbcf6e40e7609e51437e290fc92b232a48f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-netbackup"></a>Yedekleme hedefi olarak StorSimple NetBackup ile

## <a name="overview"></a>Genel Bakış

Azure StorSimple bir Microsoft karma bulut depolama çözümüdür. StorSimple, şirket içi depolama ve bulut depolama arasında hello şirket içi çözüm ve otomatik olarak katmanlama verilerinin bir uzantısı olarak Azure storage hesabı kullanarak hello karmaşıklık üstel veri büyümesi giderir.

Bu makalede, VERITAS NetBackup ve her iki çözüm de tümleştirmek için en iyi yöntemler StorSimple tümleştirme tartışın. Ayrıca nasıl VERITAS NetBackup toobest yukarı tooset tümleştirme ile StorSimple ilişkin öneriler vermiyoruz. Biz tooVeritas en iyi yöntemler, yedekleme mimarlar ve yöneticiler hello en iyi şekilde tooset VERITAS NetBackup toomeet bireysel yedekleme gereksinimlerini ve hizmet düzeyi sözleşmelerine (SLA) için kabul etmiş olursunuz.

Biz yapılandırma adımları ve temel kavramları göstermeye karşın, bu makalede halinde bir adım adım yapılandırma veya yükleme kılavuzdur. Merhaba temel bileşenleri ve altyapı çalışma sırası ve hazır toosupport biz açıklamak hello kavramları olduğunu varsayalım.

### <a name="who-should-read-this"></a>Bu kimler içindir?

Bu makaledeki bilgiler Hello en yararlı toobackup yöneticileri, depolama yöneticileri ve depolama, Windows Server 2012 R2, Ethernet, bulut Hizmetleri ve VERITAS NetBackup bilgisine sahip depolama mimarları olacaktır.

### <a name="supported-versions"></a>Desteklenen sürümler

-   NetBackup 7.7.x ve sonraki sürümler
-   [StorSimple güncelleştirme 3 ve sonraki sürümler](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a>Neden StorSimple yedekleme hedefi olarak?

StorSimple yedekleme hedefi için iyi bir seçimdir çünkü:

-   Standart, yerel depolama, herhangi bir değişiklik yapılmadan bir hızlı yedekleme hedefi olarak yedekleme uygulamaları toouse sağlar. StorSimple bir hızlı son yedekleri geri yükleme için de kullanabilirsiniz.
-   Kendi bulut katmanlandırma sorunsuz olarak tümleşik bir Azure bulut depolama hesabı toouse ile düşük maliyetli Azure depolama.
-   Otomatik olarak site dışı depolama için olağanüstü durum kurtarma sağlar.

## <a name="key-concepts"></a>Önemli kavramlar

Tüm depolama çözümü ile gibi dikkatli bir değerlendirme hello çözümün depolama performansını SLA, değişiklik ve kapasite büyüme gereksinimlerine kritik toosuccess hızıdır. Merhaba ana bulut katmanı tanımlayarak, erişim zamanları ve kapatma toohello Bulut Temel rol StorSimple toodo hello özelliği işini oynamasını olur.

StorSimple verileri (etkin) iyi tanımlanmış çalışma kümesinde çalışan tasarlanmış tooprovide depolama tooapplications ' dir. Bu modelde, veri hello çalışma kümesi hello yerel katmanları üzerinde depolanır ve hello kalan dışı/soğuk/arşivlenen veri katmanlı toohello bulut kümesidir. Bu model aşağıdaki şekilde hello temsil edilir. Merhaba neredeyse Düz yeşil satır hello üzerinde hello StorSimple cihaz yerel katmanlarda depolanan hello verileri temsil eder. Merhaba kırmızı çizgi hello toplam tüm katmanlar arasında hello StorSimple çözüm üzerinde depolanan veri miktarını temsil eder. Merhaba alanını hello Düz yeşil çizgi ve hello üstel kırmızı eğri arasında hello toplam hello bulutta depolanan veri miktarını temsil eder.

**StorSimple katmanlama**
![StorSimple katmanlama diyagramı](./media/storsimple-configure-backup-target-using-netbackup/image1.jpg)

Aklınızda bu mimari ile StorSimple yedekleme hedefi olarak idealdir toooperate olduğunu göreceksiniz. StorSimple için kullanabilirsiniz:
-   En sık rastlanan geri yüklemeler hello yerel çalışma kümesinden veri gerçekleştirin.
-   Merhaba bulut geri yüklemeler daha az sıklıkta olduğu site dışı olağanüstü durum kurtarma ve eski verileri için kullanın.

## <a name="storsimple-benefits"></a>StorSimple avantajları

Microsoft Azure ile sorunsuz olarak tümleşik bir şirket içi çözüm StorSimple sağlar, sorunsuz yararlanarak tooon içi erişmek ve depolama bulut.

StorSimple katı hal aygıt (SSD) ve seri bağlı SCSI (SAS) depolama sahip hello şirket içi cihaz ve Azure Storage arasında otomatik katmanlama kullanır. Otomatik katmanlama tutar veri hello SSD ve SAS katmanda bulunan yerel sık erişilen. Seyrek erişilen verileri tooAzure depolama taşır.

StorSimple avantajlar sunar:

-   Merhaba bulut tooachieve eşi görülmemiş yinelenenleri kaldırma düzeylerini kullanın benzersiz yinelenenleri kaldırma ve sıkıştırma algoritmaları
-   Yüksek kullanılabilirlik
-   Azure coğrafi çoğaltma kullanarak coğrafi çoğaltma
-   Azure tümleştirme
-   Merhaba bulutta veri şifrelemesi
-   Geliştirilmiş olağanüstü durum kurtarma ve uyumluluk

StorSimple temelde iki ana dağıtım senaryoları (Yedekleme hedefi birincil ve ikincil yedekleme hedefi) gösterir, ama bir düz, blok depolama cihazı vardır. StorSimple tüm sıkıştırma ve yinelenenleri kaldırma hello. Sorunsuz bir şekilde gönderir ve hello bulut ile Merhaba uygulama ve dosya sistemi arasındaki verileri alır.

StorSimple hakkında daha fazla bilgi için bkz: [StorSimple 8000 serisi: karma bulut depolama çözümü](storsimple-overview.md). Ayrıca, hello gözden geçirebilirsiniz [teknik StorSimple 8000 serisi özellikleri](storsimple-technical-specifications-and-compliance.md).

> [!IMPORTANT]
> Bir StorSimple kullanarak aygıt yedekleme hedefi olarak yalnızca StorSimple 8000 güncelleştirme 3 ve sonraki sürümler için desteklenir.

## <a name="architecture-overview"></a>Mimariye genel bakış

Merhaba aşağıdaki tablolarda hello cihaz modeli mimari ilk yönergeleri gösterilmektedir.

**StorSimple kapasiteler, yerel ve bulut depolama**

| Depolama kapasitesi       | 8100          | 8600            |
|------------------------|---------------|-----------------|
| Yerel depolama kapasitesi | &lt;10 Tıb\*  | &lt;20 Tıb\*  |
| Bulut depolama kapasitesi | &gt;200 Tıb\* | &gt;500 Tıb\* |
\*Depolama boyutu hiçbir yinelenenleri kaldırma veya sıkıştırma varsayar.

**Birincil ve ikincil yedeklemeleri StorSimple kapasiteleri**

| Yedekleme senaryosu  | Yerel depolama kapasitesi  | Bulut depolama kapasitesi  |
|---|---|---|
| Birincil yedekleme  | Hızlı Kurtarma toomeet kurtarma noktası hedefi (RPO) için yerel depolama depolanan son yedekleri | Bulut kapasitesi Yedekleme geçmişi (RPO) uygun |
| İkincil yedekleme | İkincil kopya yedekleme verilerinin bulut kapasitesi depolanabilir  | Yok  |

## <a name="storsimple-as-a-primary-backup-target"></a>StorSimple birincil yedekleme hedefi olarak

Bu senaryoda, StorSimple birimlerini toohello yedekleme uygulaması yedeklemeler için hello tek deposu olarak sunulur. Aşağıdaki şekilde hello tüm yedeklemeler kullanım StorSimple birimler yedekleme ve geri yüklemeler için katmanlı bir çözüm mimarisini göstermektedir.

![StorSimple olarak birincil yedekleme hedefi mantıksal diyagramı](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a>Birincil hedef yedekleme mantıksal adımları

1.  Hedef yedekleme aracısını Hello yedekleme sunucusu kişiler hello ve hello yedekleme aracısını veri toohello yedekleme sunucusuna iletir.
2.  Merhaba yedekleme sunucusu veri Yazar toohello StorSimple katmanlı birimler.
3.  Merhaba yedekleme sunucusu hello katalog veritabanını güncelleştirir ve hello yedekleme işi tamamlandıktan.
4.  Bir anlık görüntü betik hello StorSimple anlık görüntü Yöneticisi (başlatma veya silme) tetikler.
5.  Merhaba yedekleme sunucusuna bir bekletme ilkesi temel alınarak süresi dolan yedeklemeleri siler.

### <a name="primary-target-restore-logical-steps"></a>Birincil hedef geri yükleme mantıksal adımları

1.  Merhaba yedekleme sunucusu hello depolama depodan hello uygun veri geri yüklemeyi başlatır.
2.  Merhaba yedekleme aracısını hello yedekleme sunucusundan hello verileri alır.
3.  Merhaba yedekleme sunucusu hello geri yükleme işi tamamlar.

## <a name="storsimple-as-a-secondary-backup-target"></a>İkincil bir yedekleme hedefi olarak StorSimple

Bu senaryoda, StorSimple birimlerini öncelikle uzun vadeli bekletme veya arşivleme için kullanılır.

Merhaba aşağıdaki şekilde bir mimari hangi ilk yedeklemelerin gösterir ve yüksek performanslı hedef birim geri yükler. Bu yedeklemeler kopyalanır ve belirlenmiş bir zamanlamaya birimde arşivlenmiş tooa StorSimple katmanlı.

Önemli toosize olduğu şekilde bekletme ilkesi kapasite ve performans gereksinimlerinizi işleyebilmesi için yüksek performanslı birim.

![StorSimple olarak ikincil yedekleme hedefi mantıksal diyagramı](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a>İkincil hedef yedekleme mantıksal adımları

1.  Hedef yedekleme aracısını Hello yedekleme sunucusu kişiler hello ve hello yedekleme aracısını veri toohello yedekleme sunucusuna iletir.
2.  Merhaba yedekleme sunucusu veri toohigh performanslı depolama yazar.
3.  Merhaba yedekleme sunucusu hello katalog veritabanını güncelleştirir ve hello yedekleme işi tamamlandıktan.
4.  bir bekletme ilkesi temel alınarak yedeklemeleri tooStorSimple Hello yedekleme sunucusuna kopyalar.
5.  Bir anlık görüntü betik hello StorSimple anlık görüntü Yöneticisi (başlatma veya silme) tetikler.
6.  Merhaba yedekleme sunucusu siler hello bir bekletme ilkesi temel alınarak yedeklemeleri süresi.

### <a name="secondary-target-restore-logical-steps"></a>İkincil hedef geri yükleme mantıksal adımları

1.  Merhaba yedekleme sunucusu hello depolama depodan hello uygun veri geri yüklemeyi başlatır.
2.  Merhaba yedekleme aracısını hello yedekleme sunucusundan hello verileri alır.
3.  Merhaba yedekleme sunucusu hello geri yükleme işi tamamlar.

## <a name="deploy-hello-solution"></a>Merhaba çözümü dağıtma

Bu çözümü üç adımı gerektirir:
1. Merhaba ağ altyapısını hazırlayın.
2. StorSimple Cihazınızı yedekleme hedefi olarak dağıtın.
3. VERITAS NetBackup dağıtın.

Her adım ayrıntılı bölümleri aşağıdaki hello olarak ele alınmıştır.

### <a name="set-up-hello-network"></a>Merhaba ağı ayarlama

StorSimple hello Azure bulut ile tümleşik bir çözüm olduğundan, StorSimple etkin ve çalışıyor bağlantı toohello Azure bulut gerektirir. Bu bağlantı, bulut anlık görüntüleri, veri yönetimi ve meta veri aktarımı ve tootier daha eski, daha az erişilen veri tooAzure bulut depolama gibi işlemleri için kullanılır.

Merhaba çözüm tooperform için en iyi şekilde ağ bu en iyi uygulamaları izleyin öneririz:

-   Merhaba StorSimple katmanlama tooAzure bağlayan hello bağlantı, bant genişliği gereksinimlerini karşılaması gerekir. tooachieve bunu hello uygun hizmet kalitesi (QoS) düzeyi tooyour altyapı anahtarları toomatch uygulamak RPO ve kurtarma süresi hedefi (RTO) SLA'ları.

-   Azure Blob Depolama erişimi gecikmelerini en fazla yaklaşık 80 ms olmalıdır.

### <a name="deploy-storsimple"></a>StorSimple dağıtma

Adım adım StorSimple dağıtım yönergeleri için bkz: [şirket içi StorSimple Cihazınızı dağıtma](storsimple-deployment-walkthrough-u2.md).

### <a name="deploy-netbackup"></a>NetBackup dağıtma

Merhaba adım adım NetBackup 7.7.x dağıtım yönergeleri için bkz [NetBackup 7.7.x belgelerine](http://www.veritas.com/docs/000094423).

## <a name="set-up-hello-solution"></a>Merhaba çözümü ayarlama

Bu bölümde bazı yapılandırma örnekleri gösterilmektedir. Merhaba aşağıdaki örnekleri ve öneriler hello en temel ve temel uygulama gösterilmektedir. Bu uygulama tooyour özel yedekleme gereksinimlerini doğrudan geçerli olmayabilir.

### <a name="set-up-storsimple"></a>StorSimple ayarlayın

| StorSimple dağıtım görevleri  | Ek Açıklamalar |
|---|---|
| Şirket içi StorSimple Cihazınızı dağıtma. | Desteklenen sürümleri: Update 3 ve sonraki sürümleri. |
| Merhaba yedekleme hedefinde açın. | Bu komutlar tooturn kullanın veya yedekleme hedefi modu ve tooget durumu devre dışı bırakma. Daha fazla bilgi için bkz: [tooa StorSimple cihazı uzaktan bağlanmak](storsimple-remote-connect.md).</br> Yedekleme modu tooturn: `Set-HCSBackupApplianceMode -enable`. </br> Yedekleme modu devre dışı tooturn: `Set-HCSBackupApplianceMode -disable`. </br> tooget hello geçerli durumunu yedekleme modu ayarları: `Get-HCSBackupApplianceMode`. |
| Merhaba yedekleme verilerini depolayan biriminiz için ortak bir birim kapsayıcısı oluşturun. Tüm veriler bir birim kapsayıcısı, yinelenenleri kaldırılmış. | StorSimple birim kapsayıcıları yinelenenleri kaldırma etki alanlarını tanımlayın.  |
| StorSimple birim oluşturun. | Birim boyutu süresini anlık görüntü bulut etkilediğinden birimleri boyutlarıyla mümkün olduğunca yakın toohello beklenen kullanım olarak oluşturun. Hakkında bilgi için toosize bir birim okuma hakkında [bekletme ilkeleri](#retention-policies).</br> </br> Kullanım StorSimple katmanlı birimler ve select hello **bu birimi daha az sıklıkta erişilen arşiv verileri için kullanın** onay kutusu. </br> Yerel olarak sabitlenmiş birimleri yalnızca kullanılması desteklenmez. |
| Tüm hello yedekleme hedefi birimleri için benzersiz bir StorSimple yedekleme ilkesi oluşturun. | Bir StorSimple yedekleme İlkesi hello birim tutarlılık grubu tanımlar. |
| Merhaba anlık görüntüleri süresi dolacak şekilde hello zamanlama devre dışı bırakın. | Anlık görüntüler işlem sonrası bir işlem olarak tetiklenir. |

### <a name="set-up-hello-host-backup-server-storage"></a>Merhaba konak yedekleme sunucusu depolama ayarlama

Merhaba konak yedekleme sunucusu depolama toothese yönergelerine göre ayarlama ayarlayın:  

- Dağıtılmış birimler (Windows Disk Yönetimi tarafından oluşturulan); kullanmayın Dağıtılmış birimler desteklenmez.
- 64 KB ayırma boyutu NTFS kullanılarak birimlerinizi biçimlendirin.
- Merhaba StorSimple birimlerini eşleme doğrudan toohello NetBackup sunucu.
    - İSCSI fiziksel sunucuları için kullanın.
    - Geçiş disklerini sanal sunucular için kullanın.


## <a name="best-practices-for-storsimple-and-netbackup"></a>StorSimple ve NetBackup için en iyi yöntemler

Çözümünüzü birkaç bölümleri aşağıdaki hello toohello yönergeleri göre ayarlayın.

### <a name="operating-system-best-practices"></a>İşletim sistemi en iyi uygulamalar

-   Windows Server şifreleme ve yinelenenleri kaldırma hello NTFS dosya sistemi için devre dışı bırakın.
-   Windows Server birleştirme hello StorSimple birimlerde devre dışı bırakın.
-   Windows Server üzerinde hello StorSimple birimlerini dizin oluşturma devre dışı bırakın.
-   Virüsten koruma taraması hello kaynak ana bilgisayarı (değil karşı hello StorSimple birimlerini) çalıştırın.
-   Merhaba varsayılan devre dışı bırakma [Windows Server bakım](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) Görev Yöneticisi'nde. Aşağıdaki şekilde hello birini yapın:
    - Merhaba bakım configurator'da Windows Görev Zamanlayıcısı'nı kapatın.
    - Karşıdan [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) Windows SysInternals gelen. PsExec indirdikten sonra Windows PowerShell bir Yöneticiyseniz ve türü çalıştırın:
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a>StorSimple en iyi uygulamalar

-   Merhaba StorSimple cihaz çok güncelleştirilmiş emin olmanız[güncelleştirme 3 veya sonraki](storsimple-install-update-3.md).
-   Yalıtmaya iSCSI ve bulut trafiği. StorSimple ve hello yedekleme sunucusu arasındaki trafik için ayrılmış iSCSI bağlantıları kullanın.
-   StorSimple Cihazınızı adanmış bir yedekleme hedefi olduğundan emin olun. RTO ve RPO etkilediğinden karma iş yükleri desteklenmez.

### <a name="netbackup-best-practices"></a>NetBackup en iyi uygulamalar

-   Merhaba NetBackup veritabanı, yerel toohello sunucu ve bir StorSimple biriminde bulunan değil.
-   Olağanüstü durum kurtarma için bir StorSimple biriminin hello NetBackup veritabanını yedekleyin.
-   Bu çözüm için NetBackup tam ve artımlı yedeklemeler (Ayrıca başvurulan tooas fark artımlı yedeklemeler, NetBackup) destekliyoruz. Yapay ve toplu artımlı yedeklemeler kullanmamanızı öneririz.
-   Yedek veri dosyaları yalnızca hello verileri belirli bir iş için içermelidir. Örneğin, ortam genelinde ekler farklı işleri izin verilir.

Merhaba son NetBackup ayarlarını ve bu gereksinimleri uygulamak için en iyi yöntemler hello NetBackup belgelerine bakın [www.veritas.com](https://www.veritas.com).


## <a name="retention-policies"></a>Elde tutma ilkeleri

Merhaba en yaygın yedekleme bekletme ilkesi türlerinden birini Dedenizin, öğe ve Son (GFS) bir ilkedir. Bir GFS ilke tam yedekleme haftalık ve aylık yapılır ve artımlı yedekleme günlük gerçekleştirilir. Bu ilke sonuçları altı StorSimple katmanlı birimler: bir birimi içeren hello haftalık, aylık ve yıllık tam yedekleme; Merhaba diğer beş birimleri günlük artımlı yedeklemeleri depolar.

Aşağıdaki örneğine hello GFS döndürme kullanırız. Merhaba örneği hello aşağıdakileri varsayar:

-   Olmayan yinelenenleri kaldırılan veya sıkıştırılmış veri kullanılır.
-   Tam yedeklemeler 1 Tıb ' dir.
-   Günlük artımlı yedeklemeler 500 Gib'den ' dir.
-   Dört haftalık yedeklemeler bir ay için tutulur.
-   12 aylık yedeklemeler bir yıl için tutulur.
-   Bir yıllık yedekleme için 10 yıl tutulur.

Varsayımlar önceki hello üzerinde bağlı olarak, 26 Tıb oluşturma StorSimple katmanlı birim hello aylık ve yıllık tam yedeklemeler için. 5 Tıb oluşturma StorSimple katmanlı birim her hello artımlı günlük yedeklemeler için.

| Yedekleme türü bekletme | Boyut (Tıb) | GFS çarpanı\* | Toplam Kapasite (Tıb)  |
|---|---|---|---|
| Haftalık tam | 1 | 4  | 4 |
| Günlük artımlı | 0.5 | 20 (döngüleri eşit hafta sayısı her ay) | (2 ek kota için) 12 |
| Aylık tam | 1 | 12 | 12 |
| Yıllık tam | 1  | 10 | 10 |
| GFS gereksinimi |   | 38 |   |
| Ek kota  | 4  |   | 42 toplam GFS gereksinim  |
\*Merhaba GFS çarpanı hello sayıdır kopyaları tooprotect gerekir ve yedekleme İlkesi gereksinimlerinizi toomeet korur.

## <a name="set-up-netbackup-storage"></a>NetBackup depolama alanı ayarlama

### <a name="tooset-up-netbackup-storage"></a>NetBackup depolamayı tooset

1.  Hello NetBackup yönetim konsolunda, seçin **medya ve Aygıt Yönetimi** > **aygıtları** > **Disk havuzları**. Hello Disk havuzu Yapılandırma Sihirbazı'nı, hello depolama sunucu türünü seçin **AdvancedDisk**ve ardından **sonraki**.

    ![NetBackup yönetim konsolunda, Disk havuzu Yapılandırma Sihirbazı](./media/storsimple-configure-backup-target-using-netbackup/nbimage1.png)

2.  Sunucunuzu seçin ve ardından **sonraki**.

    ![NetBackup yönetim konsolunda, select hello sunucu](./media/storsimple-configure-backup-target-using-netbackup/nbimage2.png)

3.  StorSimple birim seçin.

    ![NetBackup yönetim konsolunda, select hello StorSimple birim disk](./media/storsimple-configure-backup-target-using-netbackup/nbimage3.png)

4.  Merhaba yedekleme hedefi için bir ad girin ve ardından **sonraki** > **sonraki** toofinish hello Sihirbazı.

5.  Hello ayarları gözden geçirin ve ardından **son**.

6.  Her bir birim atama Hello sonunda, bu önerilen hello depolama aygıtı ayarları toomatch değiştirme [en iyi uygulamalar StorSimple ve NetBackup](#best-practices-for-storsimple-and-netbackup).

7. StorSimple birimlerinizi atama tamamlandı olana kadar 1-6 adımlarını yineleyin.

    ![NetBackup yönetim konsolunda, disk yapılandırması](./media/storsimple-configure-backup-target-using-netbackup/nbimage5.png)

## <a name="set-up-storsimple-as-a-primary-backup-target"></a>StorSimple birincil yedekleme hedefi olarak ayarlayın

> [!NOTE]
> Verileri geri yüklemeler katmanlı toohello bulut boyunca yedekten bulut hızlarda oluşur.

Merhaba aşağıdaki şekilde hello eşleme tipik birim tooa yedekleme işinin gösterilmektedir. Bu durumda, tüm hello haftalık yedeklemeler toohello Cumartesi tam disk eşleme ve tooMonday Cuma artımlı diskleri hello artımlı yedeklemeler eşleyin. Tüm yedeklemeler hello ve geri yüklemeler olan bir StorSimple katmanlı birim.

![Birincil yedekleme hedefi yapılandırma mantıksal diyagramı ](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a>StorSimple birincil yedekleme hedefi GFS olarak örnek zamanlama

Aylık ve yıllık dört hafta için GFS döndürme zamanlama bir örneği burada verilmiştir:

| Sıklık/yedekleme türü | Tam | Artımlı (günleri 1-5)  |   
|---|---|---|
| Haftalık (hafta 1-4) | Cumartesi | Pazartesi-Cuma |
| Aylık  | Cumartesi  |   |
| Yıllık | Cumartesi  |   |   |

## <a name="assigning-storsimple-volumes-tooa-netbackup-backup-job"></a>StorSimple birimlerini tooa NetBackup yedekleme işi atama

sıra aşağıdaki hello NetBackup ve hello hedef barındıran hello NetBackup Aracısı yönergelerine uygun olarak yapılandırılmış olan varsayar.

### <a name="tooassign-storsimple-volumes-tooa-netbackup-backup-job"></a>tooassign StorSimple birimlerini tooa NetBackup yedekleme işi

1.  Hello NetBackup yönetim konsolunda, seçin **NetBackup Yönetim**, sağ **ilkeleri**ve ardından **yeni ilke**.

    ![NetBackup yönetim konsolunda, yeni bir ilke oluşturun](./media/storsimple-configure-backup-target-using-netbackup/nbimage6.png)

2.  Merhaba, **yeni bir ilke ekleme** iletişim kutusu, hello ilkesi için bir ad girin ve ardından hello seçin **kullanım ilkesi Yapılandırma Sihirbazı'nı** onay kutusu. **Tamam**’ı seçin.

    ![NetBackup yönetim konsolunda, yeni ilke iletişim kutusu ekleme](./media/storsimple-configure-backup-target-using-netbackup/nbimage7.png)

3.  Hello yedekleme İlkesi Yapılandırma Sihirbazı'nı seçin ve ardından yedekleme türü hello **sonraki**.

    ![NetBackup yönetim konsolunda, yedekleme türünü seçin](./media/storsimple-configure-backup-target-using-netbackup/nbimage8.png)

4.  tooset hello ilke türü, select **standart**ve ardından **sonraki**.

    ![NetBackup yönetim konsolunda, select ilke türü](./media/storsimple-configure-backup-target-using-netbackup/nbimage9.png)

5.  Ana bilgisayar, select hello seçin **istemci işletim sistemini algılar** onay kutusunu işaretleyin ve ardından **Ekle**. Seçin **sonraki**.

    ![NetBackup yönetim konsolunda, yeni bir ilke listesi istemcileri](./media/storsimple-configure-backup-target-using-netbackup/nbimage10.png)

6.  Merhaba sürücüler tooback yedeklemek istediğinizi seçin.

    ![NetBackup yönetim konsolunda, yeni bir ilke için yedekleme seçimleri](./media/storsimple-configure-backup-target-using-netbackup/nbimage11.png)

7.  Merhaba sıklığı ve rotasyon gereksinimlerinizi karşılayan bekletme değerleri seçin.

    ![NetBackup Yönetim Konsolu, yedekleme sıklığı ve yeni bir ilke için bir döndürme](./media/storsimple-configure-backup-target-using-netbackup/nbimage12.png)

8.  Seçin **sonraki** > **sonraki** > **son**.  Hello İlkesi oluşturulduktan sonra hello zamanlamasını değiştirebilirsiniz.

9.  Oluşturulan yeni tooexpand hello ilkesini seçin ve ardından **zamanlamaları**.

    ![NetBackup yönetim konsolunda, yeni bir ilke için zamanlamaları](./media/storsimple-configure-backup-target-using-netbackup/nbimage13.png)

10.  Sağ **fark Inc**seçin **kopyalama toonew**ve ardından **Tamam**.

    ![NetBackup yönetim konsolunda, kopya zamanlama tooa yeni ilke](./media/storsimple-configure-backup-target-using-netbackup/nbimage14.png)

11.  Yeni oluşturulan hello zamanlamayı sağ tıklatın ve ardından **değişiklik**.

12.  Merhaba üzerinde **öznitelikleri** sekmesi, select hello **geçersiz kılma ilkesi depolama seçimi** onay kutusunu ve ardından hello birim Pazartesi artımlı yedeklemeler nereye.

    ![NetBackup yönetim konsolunda, zamanlamasını değiştirme](./media/storsimple-configure-backup-target-using-netbackup/nbimage15.png)

13.  Merhaba üzerinde **Başlat penceresi** sekmesi, yedeklemeleriniz için select hello zaman penceresi.

    ![NetBackup yönetim konsolunda, değişiklik başlangıç penceresi](./media/storsimple-configure-backup-target-using-netbackup/nbimage16.png)

14.  **Tamam**’ı seçin.

15.  Adımları 10-14 her artımlı yedekleme için yineleyin. Merhaba uygun birimi ve oluşturduğunuz her yedekleme için zamanlamayı seçin.

16.  Sağ hello **fark Inc** zamanlamak ve silin.

17.  Yedekleme gerekli, tam zamanlama toomeet değiştirin.

    ![NetBackup yönetim konsolunda, tam zamanlamasını değiştirme](./media/storsimple-configure-backup-target-using-netbackup/nbimage17.png)

18.  Merhaba başlangıç penceresinde değiştirin.

    ![NetBackup yönetim konsolunda, değişiklik hello başlangıç penceresi](./media/storsimple-configure-backup-target-using-netbackup/nbimage18.png)

19.  Merhaba son zamanlama şöyle görünür:

    ![NetBackup Yönetim Konsolu, son zamanlama](./media/storsimple-configure-backup-target-using-netbackup/nbimage19.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a>StorSimple ikincil bir yedekleme hedefi olarak ayarlayın

> [!NOTE]
>Verileri geri yüklemeler katmanlı toohello bulut boyunca yedekten bulut hızlarda oluşur.

Bu modelde, geçici bir önbellek olarak depolama (dışında StorSimple) medya tooserve olması gerekir. Örneğin, bağımsız diskler (RAID) birim tooaccommodate alanı, giriş/çıkış (g/ç) ve bant genişliği yedek dizisi kullanabilirsiniz. RAID 5, 50 ve 10 kullanmanızı öneririz.

Merhaba aşağıdaki şekilde tipik kısa vadeli bekletme yerel (toohello sunucusu) birimler ve uzun vadeli bekletme arşivler birimleri gösterir. Bu senaryoda, tüm yedeklemeler RAID birimi hello üzerinde yerel (toohello sunucusu) çalıştırın. Bu yedeklemeler düzenli olarak çoğaltılır ve birim arşivlenmiş tooan arşivler. Bu önemli toosize (toohello sunucusu) yerel olan RAID birimi böylece kısa vadeli bekletme kapasite ve performans gereksinimlerinizi işleyebilir.

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a>StorSimple ikincil yedekleme hedefi GFS örnek olarak

![StorSimple olarak ikincil yedekleme hedefi mantıksal diyagramı](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetdiagram.png)

Merhaba aşağıdaki tabloda nasıl tooset yedeklemeleri toorun hello yerel ve StorSimple diskleri ayarlama. Tek tek ve toplam kapasite gereksinimlerini içerir.

### <a name="backup-configuration-and-capacity-requirements"></a>Yedekleme Yapılandırması ve kapasite gereksinimleri

| Yedekleme türü ve bekletme | Yapılandırılan depolama | Boyut (Tıb) | GFS çarpanı | Toplam Kapasite\* (Tıb) |
|---|---|---|---|---|
| Hafta 1 (tam ve artımlı) |Yerel disk (kısa vadeli)| 1 | 1 | 1 |
| StorSimple hafta 2-4 |StorSimple disk (uzun süreli) | 1 | 4 | 4 |
| Aylık tam |StorSimple disk (uzun süreli) | 1 | 12 | 12 |
| Yıllık tam |StorSimple disk (uzun süreli) | 1 | 1 | 1 |
|GFS birim boyutu gereksinimini |  |  |  | 18*|
\*Toplam Kapasite 17 TiB, StorSimple diskleri ve yerel RAID birimi 1 TiB içerir.


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a>GFS örnek zamanlama: GFS döndürme haftalık, aylık ve yıllık zamanlama

| Hafta | Tam | Artımlı günü 1 | Artımlı günü 2 | Artımlı Günü 3 | Artımlı günü 4 | Artımlı günü 5 |
|---|---|---|---|---|---|---|
| 1 hafta | Yerel RAID birimi  | Yerel RAID birimi | Yerel RAID birimi | Yerel RAID birimi | Yerel RAID birimi | Yerel RAID birimi |
| 2 hafta | StorSimple hafta 2-4 |   |   |   |   |   |
| Hafta 3 | StorSimple hafta 2-4 |   |   |   |   |   |
| 4 hafta | StorSimple hafta 2-4 |   |   |   |   |   |
| Aylık | StorSimple aylık |   |   |   |   |   |
| Yıllık | StorSimple yıllık  |   |   |   |   |   |   |


## <a name="assign-storsimple-volumes-tooa-netbackup-archive-and-duplication-job"></a>Arşiv ve çoğaltma StorSimple birimlerini tooa NetBackup iş atayın

NetBackup çok çeşitli seçenekler ortamı ve Depolama Yönetimi için sağladığından, VERITAS ile başvurun veya NetBackup Mimarı tooproperly depolama yaşam döngüsü ilkesi (SLP'den) gereksinimlerinizi değerlendirmenize öneririz.

Merhaba ilk disk havuzları tanımladıktan sonra dört ilkeleri toplamı toodefine üç ek depolama alanı yaşam döngüsü ilkeleri gerekir:
* LocalRAIDVolume
* StorSimpleWeek2-4
* StorSimpleMonthlyFulls
* StorSimpleYearlyFulls

### <a name="tooassign-storsimple-volumes-tooa-netbackup-archive-and-duplication-job"></a>Arşiv ve çoğaltma tooassign StorSimple birimlerini tooa NetBackup işi

1.  Hello NetBackup yönetim konsolunda, seçin **depolama** > **depolama yaşam döngüsü ilkeleri** > **yeni depolama yaşam döngüsü ilkesi**.

    ![NetBackup yönetim konsolunda, yeni depolama yaşam döngüsü ilkesi](./media/storsimple-configure-backup-target-using-netbackup/nbimage20.png)

2.  Başlangıç anlık görüntü için bir ad girin ve ardından **Ekle**.

3.  Merhaba, **yeni işlem** iletişim kutusunda, hello **özellikleri** sekmesinde için **işlemi**seçin **yedekleme**. Merhaba değerler için istediğiniz **hedef depolama**, **bekletme türü**, ve **saklama dönemi**. **Tamam**’ı seçin.

    ![NetBackup yönetim konsolunda, yeni işlem iletişim kutusu](./media/storsimple-configure-backup-target-using-netbackup/nbimage22.png)

    Bu, ilk yedekleme işlemi hello ve depo tanımlar.

4.  Toohighlight hello önceki işlemi seçin ve ardından **Ekle**. Merhaba, **değişiklik depolama işlemi** iletişim kutusunda, istediğiniz için select hello değerler **hedef depolama**, **bekletme türü**, ve **saklama süresi** .

    ![NetBackup yönetim konsolunda, değişiklik depolama işlemi iletişim kutusu](./media/storsimple-configure-backup-target-using-netbackup/nbimage23.png)

5.  Toohighlight hello önceki işlemi seçin ve ardından **Ekle**. Merhaba, **yeni depolama yaşam döngüsü ilkesi** iletişim kutusunda, bir yıl için aylık yedeklemeler ekleyin.

    ![NetBackup yönetim konsolunda, yeni depolama yaşam döngüsü ilkesi iletişim kutusu](./media/storsimple-configure-backup-target-using-netbackup/nbimage24.png)

6.  Gereksinim duyduğunuz hello kapsamlı SLP'den bekletme ilkesi oluşturuncaya kadar 4-5 adımlarını tekrarlayın.

    ![NetBackup yönetim konsolunda, Ekle İlkeleri'nde hello yeni depolama yaşam döngüsü ilkesi iletişim kutusu](./media/storsimple-configure-backup-target-using-netbackup/nbimage25.png)

7.  Altında SLP'den bekletme ilkesini tanımlama bittiğinde **İlkesi**, ayrıntılı hello adımları izleyerek bir yedekleme ilkesi tanımlama [atama StorSimple birimlerini tooa NetBackup yedekleme işi](#assigning-storsimple-volumes-to-a-netbackup-backup-job).

8.  Altında **zamanlamaları**, hello içinde **zamanlamasını değiştirme** iletişim kutusu, sağ **tam**ve ardından **değişiklik**.

    ![NetBackup yönetim konsolunda, zamanlamayı Değiştir iletişim kutusu](./media/storsimple-configure-backup-target-using-netbackup/nbimage26.png)

9.  Select hello **geçersiz kılma ilkesi depolama seçimi** onay kutusunu ve 1-6. adımda oluşturduğunuz seçip hello SLP'den bekletme ilkesi.

    ![NetBackup yönetim konsolunda, geçersiz kılma ilkesi depolama seçimi](./media/storsimple-configure-backup-target-using-netbackup/nbimage27.png)

10.  Seçin **Tamam**ve ardından hello artımlı yedekleme zamanlaması için yineleyin.

    ![NetBackup yönetim konsolunda, artımlı yedeklemeler için zamanlamayı Değiştir iletişim kutusu](./media/storsimple-configure-backup-target-using-netbackup/nbimage28.png)


| Yedekleme türü bekletme | Boyut (Tıb) | GFS çarpanı\* | Toplam Kapasite (Tıb)  |
|---|---|---|---|
| Haftalık tam |  1  |  4 | 4  |
| Günlük artımlı  | 0.5  | 20 (döngüleri olan eşit toohello aylık hafta sayısı) | (2 ek kota için) 12 |
| Aylık tam  | 1 | 12 | 12 |
| Yıllık tam | 1  | 10 | 10 |
| GFS gereksinimi  |     |     | 38 |
| Ek kota  | 4  |    | 42 toplam GFS gereksinim |
\*Merhaba GFS çarpanı hello sayıdır kopyaları tooprotect gerekir ve yedekleme İlkesi gereksinimlerinizi toomeet korur.

## <a name="storsimple-cloud-snapshots"></a>StorSimple bulut anlık görüntüleri

StorSimple bulut anlık görüntüleri StorSimple Cihazınızı bulunduğu hello verileri korur. Bir bulut anlık görüntüsü oluşturma eşdeğer tooshipping yerel yedekleme bantlarını tooan site dışı özelliğidir. Azure coğrafi olarak yedekli depolama kullanırsanız, bir bulut anlık görüntüsü oluşturma eşdeğer tooshipping yedekleme bantlarını toomultiple siteleri bağlıdır. Bir olağanüstü durum sonra toorestore bir aygıtı gerekiyorsa, başka bir StorSimple cihaz çevrimiçi duruma getirin ve bir yük devretme işlemi gerçekleştirin. Merhaba yük devretme sonrasında hello en son bulut anlık görüntüsü (bulut hızlarında) mümkün tooaccess hello verileri olacaktır.

bölümden hello nasıl toocreate kısa komut dosyası toostart ve delete StorSimple yedekleme sonrası işleme sırasında anlık görüntüleri bulut açıklar.

> [!NOTE]
> El ile veya program aracılığıyla oluşturulan anlık görüntüleri hello StorSimple anlık görüntü süre sonu ilkesi izlemeyin. Bu anlık görüntüleri el ile veya programlama silinmesi gerekir.

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a>Başlatın ve bir komut dosyası kullanarak bulut anlık görüntüleri silin

> [!NOTE]
> StorSimple anlık görüntü silmeden önce hello uyumluluk ve veri bekletme varsa dikkatle değerlendirin. Hakkında daha fazla bilgi için toorun bir yedekleme sonrası betik bkz hello [NetBackup belgelerine](http://www.veritas.com/docs/000094423).

### <a name="backup-lifecycle"></a>Yedekleme yaşam döngüsü

![Yedekleme yaşam döngüsü diyagramı](./media/storsimple-configure-backup-target-using-netbackup/backuplifecycle.png)

### <a name="requirements"></a>Gereksinimler

-   Merhaba komut dosyasını çalıştırır hello sunucu erişim tooAzure bulut kaynaklarına sahip olmalıdır.
-   Merhaba kullanıcı hesabı hello gerekli izinlere sahip olmalıdır.
-   Merhaba StorSimple yedekleme ilkesiyle birimler ayarlanmış ancak açık StorSimple ilişkili.
-   StorSimple kaynak adı, kayıt anahtarı, cihaz adı ve yedekleme ilkesi kimliği hello gerekir

### <a name="toostart-or-delete-a-cloud-snapshot"></a>toostart ya da delete bir bulut anlık görüntüsü

1.  [Azure PowerShell'i yükleme](/powershell/azure/overview).
2.  [İndirme ve içeri aktarma yayımlama ayarlarını ve abonelik bilgilerini](https://msdn.microsoft.com/library/dn385850.aspx).
3.  Buna Klasik Azure portalı Merhaba, hello kaynak adını almak ve [, StorSimple Yöneticisi hizmetiniz için kayıt anahtarını](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).
4.  Hello komut dosyasını çalıştırır hello sunucuda yönetici olarak PowerShell'i çalıştırın. Bu komutu yazın:

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    Not hello yedekleme ilkesi kimliği
5.  Not Defteri'nde koddan hello kullanarak yeni bir PowerShell komut dosyası oluşturun.

    Kopyalayın ve bu kod parçacığını yapıştırın:
    ```powershell
    Import-AzurePublishSettingsFile "c:\\CloudSnapshot Snapshot\\myAzureSettings.publishsettings"
    Disable-AzureDataCollection
    $ApplianceName = <myStorSimpleApplianceName>
    $RetentionInDays = 20
    $RetentionInDays = -$RetentionInDays
    $Today = Get-Date
    $ExpirationDate = $Today.AddDays($RetentionInDays)
    Select-AzureStorSimpleResource -ResourceName "myResource" –RegistrationKey
    Start-AzureStorSimpleDeviceBackupJob –DeviceName $ApplianceName -BackupType CloudSnapshot -BackupPolicyId <BackupId> -Verbose
    $CompletedSnapshots =@()
    $CompletedSnapshots = Get-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName
    Write-Host "hello Expiration date is " $ExpirationDate
    Write-Host

    ForEach ($SnapShot in $CompletedSnapshots)
    {
        $SnapshotStartTimeStamp = $Snapshot.CreatedOn
        if ($SnapshotStartTimeStamp -lt $ExpirationDate)

        {
            $SnapShotInstanceID = $SnapShot.InstanceId
            Write-Host "This snpashotdate was created on " $SnapshotStartTimeStamp.Date.ToShortDateString()
            Write-Host "Instance ID " $SnapShotInstanceID
            Write-Host "This snpashotdate is older and needs toobe deleted"
            Write-host "\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#"
            Remove-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName -BackupId $SnapShotInstanceID -Force -Verbose
        }
    }
    ```
      Merhaba PowerShell komut dosyası toohello Azure kaydettiğiniz aynı konuma yayımlama ayarları. Örneğin, C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1 kaydedin.
6.  Merhaba betik tooyour yedekleme işi NetBackup ekleyin. toodo Bu, düzenleme, NetBackup proje seçenekleri ön işleme ve sonrası Komutlar'ı işleme.

> [!NOTE]
> Günlük yedekleme işi hello sonunda işlem sonrası bir komut dosyası olarak StorSimple bulut anlık görüntü yedekleme ilkenizi çalıştırmanızı öneririz. Nasıl tooback yedeklemek ve geri yükleme, yedekleme uygulaması ortamı toohelp karşılamak RPO ve RTO, lütfen bakın, yedekleme Mimarı ile hakkında daha fazla bilgi.

## <a name="storsimple-as-a-restore-source"></a>Geri yükleme kaynağı olarak StorSimple

Herhangi bir blok depolama aygıtından geri yüklemeler gibi StorSimple cihazı çalışma alanından geri yükler. Katmanlı toohello bulut veri geri yüklemeler bulut hızlarda oluşur. Yerel veriler için geri yüklemeler hello yerel disk hızında hello cihazın oluşur. Hakkında bilgi için tooperform bir geri yükleme, bkz: Merhaba [NetBackup belgelerine](http://www.veritas.com/docs/000094423). TooNetBackup geri yükleme en iyi yöntemler uygun öneririz.

## <a name="storsimple-failover-and-disaster-recovery"></a>StorSimple yük devretme ve olağanüstü durum kurtarma

> [!NOTE]
> Yedekleme hedefi senaryoları için bir geri yükleme hedefi olarak StorSimple bulut uygulaması desteklenmiyor.

Bir olağanüstü durum çeşitli etkenlere göre neden olabilir. Aşağıdaki tablonun hello olağanüstü durum kurtarma senaryoları listeler.

| Senaryo | Etkisi | Nasıl toorecover | Notlar |
|---|---|---|---|
| StorSimple cihaz hatası | Yedekleme ve geri yükleme işlemleri kesilir. | Merhaba başarısız aygıt değiştirin ve gerçekleştirmek [StorSimple yük devretme ve olağanüstü durum kurtarma](storsimple-device-failover-disaster-recovery.md). | Tooperform aygıt kurtarma işleminden sonra geri yükleme gerekiyorsa, tam veri çalışma kümeleri hello bulut toohello yeni aygıttan alınır. Bulut hızlarda tüm işlemleridir. Başlangıç dizini ve işlemi yeniden tarama işlemi katalog tararken ve bu da zaman alan bir işlem olabilir hello bulut katmanı toohello yerel aygıt katmanından, çekilen tüm yedekleme kümelerini toobe neden olabilir. |
| NetBackup sunucu hatası | Yedekleme ve geri yükleme işlemleri kesilir. | Merhaba yedekleme sunucusunu yeniden oluşturmak ve veritabanı geri yükleme gerçekleştirin. | Yeniden oluşturmanız veya hello NetBackup hello olağanüstü durum kurtarma site sunucusunda geri yükleme. Merhaba veritabanı toohello en son noktası geri yükleyin. Merhaba geri yüklenen NetBackup veritabanı son yedekleme işlerinizi ile eşitlenmiş durumda değilse, dizin oluşturma ve Katalog gereklidir. Bu dizin ve işlemi yeniden tarama işlemi katalog tararken ve hello bulut katmanı toohello yerel aygıt katmanından çekilen tüm yedekleme kümelerini toobe neden olabilir. Bu, daha fazla zaman yoğunluklu kolaylaştırır. |
| Merhaba yedekleme sunucusu ve StorSimple hello kaybı ile sonuçlanır site hatası | Yedekleme ve geri yükleme işlemleri kesilir. | StorSimple önce geri yükleme ve NetBackup geri yükleyin. | StorSimple önce geri yükleme ve NetBackup geri yükleyin. Tooperform aygıt kurtarma işleminden sonra geri yükleme gerekiyorsa, hello tam veri çalışma kümeleri hello bulut toohello yeni aygıttan alınır. Bulut hızlarda tüm işlemleridir. |

## <a name="references"></a>Başvurular

Aşağıdaki belgeler hello için bu makalenin başvurulan:

- [StorSimple çok yollu g/ç Kurulumu](storsimple-configure-mpio-windows-server.md)
- [Depolama senaryoları: ölçülü kaynak sağlama](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [GPT kullanarak sürücüler](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [Paylaşılan klasörler için gölge kopyaları ayarlama](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a>Sonraki adımlar

- Hakkında daha fazla çok bilgi[bir yedekleme kümesi geri](storsimple-restore-from-backup-set-u2.md).
- Hakkında daha fazla bilgi tooperform [aygıt yük devretme ve olağanüstü durum kurtarma](storsimple-device-failover-disaster-recovery.md).
