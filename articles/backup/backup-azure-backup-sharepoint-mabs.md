---
title: "bir SharePoint grubu tooAzure yukarı aaaUse Azure yedekleme sunucusu tooback | Microsoft Docs"
description: "Azure yedekleme sunucusu tooback kullanır ve SharePoint verilerinizi geri yükleyin. Bu makalede, SharePoint grubu hello bilgi tooconfigure sunar, böylece istenen verileri Azure'da saklanabilir. Korumalı SharePoint verileri diskten veya Azure geri yükleyebilirsiniz."
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: 34ba87a4-91f1-4054-a4a1-272af1e15496
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 350c1ac0f3518f400062f3b586bbe9710a79915a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a>Bir SharePoint grubu tooAzure yedekleyin
Bir SharePoint yedekleme tooMicrosoft Azure kadar hello Microsoft Azure yedekleme sunucusu (MABS) kullanarak grubunuz diğer veri kaynaklarını geri aynı şekilde. Azure yedekleme, günlük, haftalık, aylık veya yıllık yedekleme noktaları hello yedekleme zamanlaması toocreate esneklik sağlar ve çeşitli yedekleme noktaları için bekletme ilkesi seçenekler sunar. Hızlı Kurtarma süresi hedefi (RTO) için de hello yetenek toostore yerel disk kopyaları sağlar ve toostore tooAzure ekonomik, uzun vadeli bekletme için kopyalar.

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a>SharePoint desteklenen sürümleri ve ilgili koruma senaryoları
Azure yedekleme DPM için hello aşağıdaki senaryoları destekler:

| İş yükü | Sürüm | SharePoint dağıtımı | Koruma ve kurtarma |
| --- | --- | --- | --- | --- | --- |
| SharePoint |SharePoint 2013, SharePoint 2010, SharePoint 2007'de, SharePoint 3.0 |Bir fiziksel sunucu veya Hyper-V/VMware sanal makinesi dağıtılan SharePoint <br> -------------- <br> SQL AlwaysOn | SharePoint grubu kurtarma seçeneklerini koruma: Kurtarma grubu, veritabanı ve disk kurtarma noktalarından dosya veya liste öğesi.  Azure kurtarma noktalarından grubu ve veritabanı kurtarma. |

## <a name="before-you-start"></a>Başlamadan önce
Bir SharePoint grubu tooAzure yedeklenmeden önce tooconfirm gereken birkaç nokta vardır.

### <a name="prerequisites"></a>Ön koşullar
Devam etmeden önce bilgisayarınızda yüklü olduğundan emin olun [yüklü ve hello Azure yedekleme sunucusu hazırlanan](backup-azure-microsoft-azure-backup.md) tooprotect iş yükleri.

### <a name="protection-agent"></a>Koruma Aracısı
Merhaba koruma Aracısı, SharePoint, SQL Server çalıştıran hello sunucuları ve hello SharePoint grubunun parçası olan diğer tüm sunucuları çalıştıran hello sunucuda yüklenmesi gerekir. Hakkında daha fazla bilgi için tooset hello koruma aracısını kurma bkz [Kurulum koruma Aracısı](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).  Merhaba hello aracı yalnızca bir tek web front end (WFE) sunucusuna yükleyin işlemdir. DPM, koruma için hello giriş noktası olarak bir WFE sunucusu yalnızca tooserve hello aracısında gerekir.

### <a name="sharepoint-farm"></a>SharePoint grubu
Merhaba gruptaki her 10 milyon öğe için en az 2 GB hello biriminde hello MABS klasörünün bulunduğu alan olmalıdır. Bu alanı katalog oluşturma için gereklidir. MABS toorecover belirli öğeleri (site koleksiyonları, siteler, listeler, belge kitaplıkları, klasörler, tek tek belgeler ve liste öğeleri), katalog oluşturma her içerik veritabanında bulunan hello URL'lerin bir listesini oluşturur. Merhaba hello kurtarılabilir öğe bölmesinde hello URL'lerin listesini görüntüleyebilirsiniz **kurtarma** MABS Yönetici Konsolu'nun alanı görev.

### <a name="sql-server"></a>SQL Server
MABS LocalSystem hesabı olarak çalışır. tooback SQL Server veritabanlarını MABS SQL Server çalıştıran hello sunucu için bu hesabı üzerinde sysadmin ayrıcalıkları gerekir. NT AUTHORITY\SYSTEM çok ayarlamak*sysadmin* önce SQL Server çalıştıran hello sunucuda yedekleyin.

Hello SharePoint grubu SQL Server diğer adlarıyla yapılandırılmış SQL Server veritabanları varsa, hello SQL Server istemci bileşenlerini MABS koruyacak hello ön uç Web sunucusuna yükleyin.

### <a name="sharepoint-server"></a>SharePoint Server
Performans SharePoint grubu boyutu gibi birçok faktöre bağlıdır, ancak genel bir yönerge olarak 25 TB SharePoint grubunu bir MABS koruyabilirsiniz.

### <a name="whats-not-supported"></a>Desteklenmeyen durumlar
* Bir SharePoint grubu korur MABS, arama dizinlerini veya uygulama hizmeti veritabanlarını koruma sağlamaz. Bu veritabanlarının tooconfigure hello koruma ayrı olarak gerekir.
* MABS, genişleme dosya sunucusu (SOFS) paylaşımları üzerinde barındırılan SharePoint SQL Server veritabanlarını yedekleme sağlamaz.

## <a name="configure-sharepoint-protection"></a>SharePoint korumasını yapılandırma
MABS tooprotect SharePoint kullanmadan önce kullanarak hello SharePoint VSS yazıcısı hizmetini (WSS yazıcısı hizmeti) yapılandırmanız gerekir **ConfigureSharePoint.exe**.

Bulabileceğiniz **ConfigureSharePoint.exe** hello [MABS yükleme yolu] \bin klasöründe hello ön uç web sunucusunda. Bu araç hello koruma Aracısı hello kimlik bilgileriyle hello SharePoint grubu için sağlar. Bu tek bir WFE sunucusunda çalıştırın. Birden çok WFE sunucunuz varsa, bir koruma grubu yapılandırırken yalnızca bir tanesini seçin.

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a>tooconfigure hello SharePoint VSS Yazıcı hizmeti
1. Bir komut isteminde hello WFE sunucusunda çok Git [MABS yükleme konumu] \bin\
2. ConfigureSharePoint - EnableSharePointProtection girin.
3. Merhaba grubu yönetici kimlik bilgilerini girin. Bu hesap hello WFE sunucusunda hello yerel yönetici grubunun bir üyesi olmalıdır. Merhaba Çiftlik Yöneticisi aşağıdaki izinleri hello WFE sunucusunda yerel yönetici grant hello değilse:
   * Merhaba WSS_Admin_WPG grubu tam denetim toohello DPM klasörünü (% Program Files%\Microsoft Azure Backup\DPM) verin.
   * GRANT hello WSS_Admin_WPG grubu okuma erişimini toohello DPM kayıt defteri anahtarı (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).

> [!NOTE]
> Merhaba SharePoint grubu yönetici kimlik bilgilerinde bir değişiklik olduğunda toorerun ConfigureSharePoint.exe gerekir.
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a>SharePoint grubunun kurulumu MABS kullanarak yedekleyin
MABS ve hello daha önce açıklandığı gibi SharePoint grubu yapılandırdıktan sonra bu SharePoint MABS tarafından korunur.

### <a name="tooprotect-a-sharepoint-farm"></a>tooprotect bir SharePoint grubu
1. Merhaba gelen **koruma** hello MABS Yönetici Konsolu sekmesini **yeni**.
    ![Yeni koruma sekmesi](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)
2. Merhaba üzerinde **koruma grubu türünü seçin** hello sayfasının **yeni koruma grubu oluşturma** seçin **sunucuları**ve ardından **sonraki** .

    ![Koruma grubu seç türü](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. Merhaba üzerinde **grup üyelerini seçin** ekran, select hello onay kutusunu tooprotect istediğiniz hello SharePoint Server **sonraki**.

    ![Grup üyelerini seçin](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > Yüklü hello koruma Aracısı ile Merhaba sunucu hello Sihirbazı'nda görebilirsiniz. MABS da yapısını gösterir. ConfigureSharePoint.exe çalıştırdığınız için MABS hello SharePoint VSS yazıcısı hizmetini ve karşılık gelen SQL Server veritabanlarını ile iletişim kurar ve hello SharePoint grup yapısı tanır, içerik veritabanları ve karşılık gelen tüm öğeleri hello ilişkilendirilmiş.
   >
   >
4. Merhaba üzerinde **veri koruma yöntemini seçin** sayfasında, hello hello adını **koruma grubu**ve tercih ettiğiniz seçin *koruma yöntemleri*. **İleri**’ye tıklayın.

    ![Veri koruma yöntemini seçin](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > Merhaba disk koruma yöntemini toomeet kısa kurtarma zamanı hedeflerine yardımcı olur.
   >
   >
5. Merhaba üzerinde **kısa vadeli hedefleri belirtin** sayfasında, tercih ettiğiniz **bekletme aralığı** ve yedeklemeleri toooccur istediğinizde belirleyin.

    ![Kısa vadeli hedefleri belirtin](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > Kurtarma genellikle beş günden eski olan verileri için gerekli olduğundan, biz diskteki beş günlük bir bekletme aralığı seçili ve bu örnek için üretim dışı saatlerde hello yedekleme olur güvence altına.
   >
   >
6. Merhaba koruma grubu için ayrılmış hello depolama havuzu disk alanını gözden geçirin ve ardından **sonraki**.
7. Her koruma grubu için MABS disk alanı toostore ayırır ve çoğaltmaları yönetin. Bu noktada, MABS seçili hello verilerin bir kopyasını oluşturmanız gerekir. Nasıl ve ne zaman, oluşturulan hello çoğaltma istediğiniz'ı seçin ve **sonraki**.

    ![Çoğaltma oluşturma yöntemini seçin](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > ağ trafiği parametreden etkilenir değil, emin toomake üretim saatleri dışında bir saat seçin.
   >
   >
8. MABS hello çoğaltma üzerinde tutarlılık denetimleri gerçekleştirerek veri bütünlüğü sağlar. Kullanılabilir iki seçenek vardır. Tanımlamak bir zamanlama toorun tutarlılık denetimlerinin veya tutarsız hale her DPM otomatik olarak hello çoğaltma üzerinde tutarlılık denetimleri çalışabilir. Tercih ettiğiniz seçeneği seçin ve ardından **sonraki**.

    ![Tutarlılık denetimi](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. Merhaba üzerinde **çevrimiçi koruma verilerini belirtin** sayfasında, tooprotect istediğiniz ve ardından hello SharePoint grubu seçin **sonraki**.

    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. Merhaba üzerinde **çevrimiçi yedekleme zamanlamasını belirtin** sayfasında, tercih ettiğiniz zamanlamayı seçin ve ardından **sonraki**.

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > MABS en fazla iki günlük yedekleri tooAzure hello silip kullanılabilir en son disk yedekleme noktası sağlar. Azure yedekleme de hello yedeklemeler yoğun ve yoğun olmayan saatler için kullanarak kullanılabilir WAN bant genişliği miktarını kontrol [Azure yedekleme ağ azaltma](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).
    >
    >
11. Merhaba üzerinde seçili hello yedekleme zamanlaması bağlı olarak **çevrimiçi bekletme ilkesini belirtin** sayfası, günlük, haftalık, aylık ve yıllık yedekleme noktaları için select hello bekletme ilkesi.

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > MABS farklı yedekleme noktaları için farklı bir bekletme ilkesi seçilebilir bir üst öğe son bekletme düzeni kullanır.
    >
    >
12. Benzer toodisk bir ilk başvuru noktası çoğaltmasını Azure içinde oluşturulan toobe gerekir. Tercih edilen seçenek toocreate ilk yedek kopyayı tooAzure seçin ve ardından **sonraki**.

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. Merhaba üzerinde seçtiğiniz ayarları gözden **Özet** sayfasında ve ardından **Grup Oluştur**. Merhaba koruma grubu oluşturulduktan sonra bir başarı iletisi görürsünüz.

    ![Özet](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a>Bir SharePoint öğesi MABS kullanarak diskten geri yükleme
Aşağıdaki örneğine hello hello *SharePoint kurtarma öğesi* yanlışlıkla silinmişse ve kurtarılan toobe gerekiyor.
![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)

1. Açık hello **DPM Yönetici Konsolu'nu**. DPM tarafından korunan tüm SharePoint grupları hello gösterilen **koruma** sekmesi.

    ![MABS SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. toobegin toorecover hello öğesi, select hello **kurtarma** sekmesi.

    ![MABS SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. SharePoint için arama yapabilirsiniz *SharePoint kurtarma öğesi* kurtarma içinde bir joker karakter tabanlı arama kullanarak aralığı gösterin.

    ![MABS SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. Merhaba Arama sonuçlarından Hello uygun kurtarma noktası seçin, hello öğeyi sağ tıklatın ve ardından **kurtarmak**.
5. Ayrıca, çeşitli kurtarma noktalarına göz ve bir veritabanı veya öğeyi toorecover seçebilirsiniz. Seçin **tarihi > kurtarma süresini**ve ardından hello doğru **veritabanı > SharePoint grubu > kurtarma noktası > öğesi**.

    ![MABS SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. Merhaba öğeyi sağ tıklatın ve ardından **kurtarmak** tooopen hello **Kurtarma Sihirbazı'nı**. **İleri**’ye tıklayın.

    ![Kurtarma seçimini inceleyin](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. Merhaba tooperform istediğiniz ve ardından Kurtarma türünü seçin **sonraki**.

    ![Kurtarma türü](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > Merhaba seçimi **kurtarmak toooriginal** hello örnek hello öğesi toohello özgün SharePoint sitesini kurtarır.
   >
   >
8. Select hello **kurtarma işlemi** toouse istiyor.

   * Seçin **kurtarma grubu kullanmadan kurtarmak** hello SharePoint grubu değişmemiştir ve aynı hello kurtarma noktası hello geri yükleniyor.
   * Seçin **kurtarma grubu kullanarak kurtarma** hello SharePoint grubu hello kurtarma noktası oluşturulduğundan beri değişmişse.

     ![Kurtarma işlemi](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. Hazırlama bir SQL Server örneğinin konumu toorecover hello veritabanı geçici olarak sağlayın ve SharePoint toorecover hello öğesi çalışan MABS ve hello sunucuya hazırlama bir dosya paylaşımı sağlayın.

    ![Hazırlama Location1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    MABS hello SharePoint öğesi toohello geçici SQL Server örneği barındırma hello içerik veritabanını ekler. Merhaba içerik veritabanından onu hello öğesi kurtarır ve dosya konumuna MABS hazırlama hello üzerinde koyar. Merhaba hazırlama konumuna şimdi hello üzerinde hello SharePoint grubu üzerinde hazırlama gereksinimlerini dışarı toobe toohello öğeyi kurtarıldı.

    ![Hazırlama Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. Seçin **kurtarma seçeneklerini belirtin**, güvenlik ayarları toohello SharePoint grubu uygulamak ve hello kurtarma noktası hello güvenlik ayarlarını uygula. **İleri**’ye tıklayın.

    ![Kurtarma Seçenekleri](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > Toothrottle hello ağ bant genişliği kullanımını seçebilirsiniz. Bu etki toohello üretim sunucusu üretim saatleri dışında en aza indirir.
    >
    >
11. Merhaba özet bilgileri gözden geçirin ve ardından **kurtarmak** hello dosyasının toobegin kurtarma.

    ![Kurtarma özeti](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. Şimdi hello seçin **izleme** hello sekmesinde **MABS Yönetici Konsolu** tooview hello **durum** hello kurtarma.

    ![Kurtarma durumu](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > Merhaba dosya şimdi geri yüklenir. Merhaba SharePoint site toocheck geri hello dosyası yenileyebilirsiniz.
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a>DPM kullanarak bir SharePoint veritabanı Azure'dan geri yükleme
1. bir SharePoint içerik veritabanı toorecover (daha önce gösterildiği gibi) çeşitli kurtarma noktalarına göz ve toorestore istediğiniz hello kurtarma noktası seçin.

    ![MABS SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. Merhaba SharePoint kurtarma noktası tooshow hello kullanılabilir SharePoint katalog bilgileri çift tıklayın.

   > [!NOTE]
   > Merhaba SharePoint grubu Azure uzun vadeli bekletme için korumalı olduğundan, hiçbir Kataloğu bilgi (meta veriler) MABS üzerinde kullanılabilir. Zaman içinde nokta SharePoint içerik veritabanını kurtarılan toobe her gerektiğinde, sonuç olarak, toocatalog hello SharePoint grubu yeniden gerekir.
   >
   >
3. Tıklatın **yeniden kataloglama**.

    ![MABS SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    Merhaba **bulut yeniden katalogla** durum penceresi açar.

    ![MABS SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    Katalog tamamlandıktan sonra hello çok durumuna*başarı*. **Kapat**’a tıklayın.

    ![MABS SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. Merhaba MABS gösterilen hello SharePoint nesnesine tıklayın **kurtarma** sekmesinde tooget hello içerik veritabanı yapısı. Merhaba öğeyi sağ tıklatın ve ardından **kurtarmak**.

    ![MABS SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. Bu noktada, hello izleyin [kurtarma adımları bu makalenin önceki bölümlerinde](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover diskten bir SharePoint içerik veritabanı.

## <a name="faqs"></a>SSS
S: bir SharePoint öğesi toohello özgün konumuna, SharePoint SQL AlwaysOn (disk koruması) kullanılarak yapılandırılmışsa kurtarma?<br>
A: Evet hello öğesi kurtarılan toohello özgün SharePoint sitesi olabilir.

S: bir SharePoint veritabanı toohello özgün konumu, SQL AlwaysOn kullanarak SharePoint yapılandırdıysanız kurtarmak?<br>
A: SharePoint veritabanlarını SQL AlwaysOn yapılandırıldığından, bunlar hello kullanılabilirlik grubu kaldırılmadığı sürece değiştirilemez. Sonuç olarak, MABS veritabanı toohello özgün konumuna geri yükleyemezsiniz. Bir SQL Server veritabanı tooanother SQL Sunucusu örneğine kurtarabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
* SharePoint MABS koruma hakkında daha fazla bilgi - bkz [Video serisi - SharePoint DPM koruma](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)
