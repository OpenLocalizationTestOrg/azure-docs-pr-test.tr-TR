---
title: bir SharePoint grubu tooAzure aaaDPM/Azure yedekleme sunucusu koruma | Microsoft Docs
description: "Bu makalede bir SharePoint grubu tooAzure DPM/Azure yedekleme sunucusu koruma genel bir bakış sağlar"
services: backup
documentationcenter: 
author: adigan
manager: Nkolli1
editor: 
ms.assetid: e0c0c252-dc1d-4072-b777-7222c13950b0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: adigan;giridham;jimpark;trinadhk;markgal
ms.openlocfilehash: 726d59320b8d9f14b38e0f041308019eebcfb77b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a>Bir SharePoint grubu tooAzure yedekleyin
Bir SharePoint yedekleme tooMicrosoft Azure kadar hello System Center Data Protection Manager (DPM) kullanarak grubunuz diğer veri kaynaklarını geri aynı şekilde. Azure yedekleme, günlük, haftalık, aylık veya yıllık yedekleme noktaları hello yedekleme zamanlaması toocreate esneklik sağlar ve çeşitli yedekleme noktaları için bekletme ilkesi seçenekler sunar. DPM, Hızlı Kurtarma süresi hedefi (RTO) için hello yetenek toostore yerel disk kopyaları sağlar ve toostore tooAzure ekonomik, uzun vadeli bekletme için kopyalar.

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a>SharePoint desteklenen sürümleri ve ilgili koruma senaryoları
Azure yedekleme DPM için hello aşağıdaki senaryoları destekler:

| İş yükü | Sürüm | SharePoint dağıtımı | DPM dağıtım türü | DPM - System Center 2012 R2 | Koruma ve kurtarma |
| --- | --- | --- | --- | --- | --- |
| SharePoint |SharePoint 2013, SharePoint 2010, SharePoint 2007'de, SharePoint 3.0 |Bir fiziksel sunucu veya Hyper-V/VMware sanal makinesi dağıtılan SharePoint <br> -------------- <br> SQL AlwaysOn |Fiziksel sunucu veya şirket içi Hyper-V sanal makine |Güncelleştirme Paketi 5'ten Yedekleme tooAzure destekler |SharePoint grubu kurtarma seçeneklerini koruma: Kurtarma grubu, veritabanı ve disk kurtarma noktalarından dosya veya liste öğesi.  Azure kurtarma noktalarından grubu ve veritabanı kurtarma. |

## <a name="before-you-start"></a>Başlamadan önce
Bir SharePoint grubu tooAzure yedeklenmeden önce tooconfirm gereken birkaç nokta vardır.

### <a name="prerequisites"></a>Ön koşullar
Devam etmeden önce tüm hello karşıladığınızdan emin olun [Microsoft Azure Yedekleme kullanılarak önkoşulları](backup-azure-dpm-introduction.md#prerequisites) tooprotect iş yükleri. Önkoşullar için bazı görevler aşağıdakileri içerir: bir yedekleme kasası oluşturun, kasa kimlik bilgilerini indirme, Azure Yedekleme aracısı yükleyin ve DPM/Azure yedekleme sunucusu hello kasayla kaydedin.

### <a name="dpm-agent"></a>DPM Aracısı
Merhaba DPM Aracısı, SharePoint çalıştıran hello server, SQL Server çalıştıran hello sunucuları ve hello SharePoint grubunun parçası olan diğer tüm sunucuları yüklenmelidir. Hakkında daha fazla bilgi için tooset hello koruma aracısını kurma bkz [Kurulum koruma Aracısı](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).  Merhaba hello aracı yalnızca bir tek web front end (WFE) sunucusuna yükleyin işlemdir. DPM, koruma için hello giriş noktası olarak bir WFE sunucusu yalnızca tooserve hello aracısında gerekir.

### <a name="sharepoint-farm"></a>SharePoint grubu
Merhaba gruptaki her 10 milyon öğe için en az 2 GB hello biriminde hello DPM klasörünün bulunduğu alan olmalıdır. Bu alanı katalog oluşturma için gereklidir. DPM toorecover belirli öğeleri (site koleksiyonları, siteler, listeler, belge kitaplıkları, klasörler, tek tek belgeler ve liste öğeleri), katalog oluşturma her içerik veritabanında bulunan hello URL'lerin bir listesini oluşturur. Merhaba hello kurtarılabilir öğe bölmesinde hello URL'lerin listesini görüntüleyebilirsiniz **kurtarma** görev alanındaki DPM Yönetici Konsolu'nun.

### <a name="sql-server"></a>SQL Server
DPM LocalSystem hesabı olarak çalışır. tooback SQL Server veritabanlarını DPM SQL Server çalıştıran hello sunucu için bu hesabı üzerinde sysadmin ayrıcalıkları gerekir. NT AUTHORITY\SYSTEM çok ayarlamak*sysadmin* önce SQL Server çalıştıran hello sunucuda yedekleyin.

Hello SharePoint grubu SQL Server diğer adlarıyla yapılandırılmış SQL Server veritabanlarını ise, DPM koruyacak hello ön uç Web sunucusunda hello SQL Server istemci bileşenlerini yükleyin.

### <a name="sharepoint-server"></a>SharePoint Server
Performans SharePoint grubu boyutu gibi birçok faktöre bağlıdır, ancak genel bir yönerge olarak 25 TB SharePoint grubunu bir DPM sunucusu koruyabilir.

### <a name="dpm-update-rollup-5"></a>DPM Güncelleştirme Paketi 5
bir SharePoint grubu tooAzure toobegin koruma, gereksinim duyduğunuz tooinstall DPM Güncelleştirme Paketi 5 veya üzeri. SQL AlwaysOn kullanarak Hello grubu yapılandırılmışsa Güncelleştirme Paketi 5 hello özelliği tooprotect bir SharePoint grubu tooAzure sağlar.
Daha fazla bilgi için bkz: Merhaba tanıtır blog gönderisi [DPM Güncelleştirme Paketi 5](http://blogs.technet.com/b/dpm/archive/2015/02/11/update-rollup-5-for-system-center-2012-r2-data-protection-manager-is-now-available.aspx)

### <a name="whats-not-supported"></a>Desteklenmeyen durumlar
* Bir SharePoint grubu koruyan DPM arama dizinlerini veya uygulama hizmeti veritabanlarını koruma sağlamaz. Bu veritabanlarının tooconfigure hello koruma ayrı olarak gerekir.
* DPM, genişleme dosya sunucusu (SOFS) paylaşımları üzerinde barındırılan SharePoint SQL Server veritabanlarını yedekleme sağlamaz.

## <a name="configure-sharepoint-protection"></a>SharePoint korumasını yapılandırma
DPM tooprotect SharePoint kullanmadan önce kullanarak hello SharePoint VSS yazıcısı hizmetini (WSS yazıcısı hizmeti) yapılandırmanız gerekir **ConfigureSharePoint.exe**.

Bulabileceğiniz **ConfigureSharePoint.exe** hello [DPM yükleme yolu] \bin klasöründe hello ön uç web sunucusunda. Bu araç hello koruma Aracısı hello kimlik bilgileriyle hello SharePoint grubu için sağlar. Bu tek bir WFE sunucusunda çalıştırın. Birden çok WFE sunucunuz varsa, bir koruma grubu yapılandırırken yalnızca bir tanesini seçin.

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a>tooconfigure hello SharePoint VSS Yazıcı hizmeti
1. Bir komut isteminde hello WFE sunucusunda çok Git [DPM yükleme konumuna] \bin\
2. ConfigureSharePoint - EnableSharePointProtection girin.
3. Merhaba grubu yönetici kimlik bilgilerini girin. Bu hesap hello WFE sunucusunda hello yerel yönetici grubunun bir üyesi olmalıdır. Merhaba Çiftlik Yöneticisi aşağıdaki izinleri hello WFE sunucusunda yerel yönetici grant hello değilse:
   * Merhaba WSS_Admin_WPG grubu tam denetim toohello DPM klasörünü (% Program Files%\Microsoft Data Protection Manager\DPM) verin.
   * GRANT hello WSS_Admin_WPG grubu okuma erişimini toohello DPM kayıt defteri anahtarı (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).

> [!NOTE]
> Merhaba SharePoint grubu yönetici kimlik bilgilerinde bir değişiklik olduğunda toorerun ConfigureSharePoint.exe gerekir.
> 
> 

## <a name="back-up-a-sharepoint-farm-by-using-dpm"></a>DPM kullanarak bir SharePoint grubunun kurulumu yedekleyin
DPM ve hello daha önce açıklandığı gibi SharePoint grubu yapılandırdıktan sonra bu SharePoint DPM tarafından korunur.

### <a name="tooprotect-a-sharepoint-farm"></a>tooprotect bir SharePoint grubu
1. Merhaba gelen **koruma** Merhaba, DPM Yönetici Konsolu'nda sekmesini **yeni**.
    ![Yeni koruma sekmesi](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)
2. Merhaba üzerinde **koruma grubu türünü seçin** hello sayfasının **yeni koruma grubu oluşturma** seçin **sunucuları**ve ardından **sonraki** .
   
    ![Koruma grubu seç türü](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. Merhaba üzerinde **grup üyelerini seçin** ekran, select hello onay kutusunu tooprotect istediğiniz hello SharePoint Server **sonraki**.
   
    ![Grup üyelerini seçin](./media/backup-azure-backup-sharepoint/select-group-members2.png)
   
   > [!NOTE]
   > Yüklü hello DPM Aracısı ile Merhaba sunucu hello Sihirbazı'nda görebilirsiniz. DPM, aynı zamanda yapısını gösterir. ConfigureSharePoint.exe çalıştırdığınız için DPM hello SharePoint VSS yazıcısı hizmetini ve karşılık gelen SQL Server veritabanlarını ile iletişim kurar ve hello SharePoint grup yapısı tanır, içerik veritabanları ve karşılık gelen tüm öğeleri hello ilişkili.
   > 
   > 
4. Merhaba üzerinde **veri koruma yöntemini seçin** sayfasında, hello hello adını **koruma grubu**ve tercih ettiğiniz seçin *koruma yöntemleri*. **İleri**’ye tıklayın.
   
    ![Veri koruma yöntemini seçin](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)
   
   > [!NOTE]
   > Merhaba disk koruma yöntemini toomeet kısa kurtarma zamanı hedeflerine yardımcı olur. Azure ekonomik, uzun vadeli koruma karşılaştırıldığında hedef tootapes ' dir. Daha fazla bilgi için bkz: [Azure Yedekleme'yi tooreplace bant altyapınızın](https://azure.microsoft.com/documentation/articles/backup-azure-backup-cloud-as-tape/)
   > 
   > 
5. Merhaba üzerinde **kısa vadeli hedefleri belirtin** sayfasında, tercih ettiğiniz **bekletme aralığı** ve yedeklemeleri toooccur istediğinizde belirleyin.
   
    ![Kısa vadeli hedefleri belirtin](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)
   
   > [!NOTE]
   > Kurtarma genellikle beş günden eski olan verileri için gerekli olduğundan, biz diskteki beş günlük bir bekletme aralığı seçili ve bu örnek için üretim dışı saatlerde hello yedekleme olur güvence altına.
   > 
   > 
6. Merhaba koruma grubu için ayrılmış hello depolama havuzu disk alanını gözden geçirin ve ardından **sonraki**.
7. DPM, her koruma grubu için disk alanı toostore ayırır ve çoğaltmaları yönetin. Bu noktada, DPM seçili hello verilerin bir kopyasını oluşturmanız gerekir. Nasıl ve ne zaman, oluşturulan hello çoğaltma istediğiniz'ı seçin ve **sonraki**.
   
    ![Çoğaltma oluşturma yöntemini seçin](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)
   
   > [!NOTE]
   > ağ trafiği parametreden etkilenir değil, emin toomake üretim saatleri dışında bir saat seçin.
   > 
   > 
8. DPM, hello çoğaltma üzerinde tutarlılık denetimleri gerçekleştirerek veri bütünlüğü sağlar. Kullanılabilir iki seçenek vardır. Tanımlamak bir zamanlama toorun tutarlılık denetimlerinin veya tutarsız hale her DPM otomatik olarak hello çoğaltma üzerinde tutarlılık denetimleri çalışabilir. Tercih ettiğiniz seçeneği seçin ve ardından **sonraki**.
   
    ![Tutarlılık denetimi](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. Merhaba üzerinde **çevrimiçi koruma verilerini belirtin** sayfasında, tooprotect istediğiniz ve ardından hello SharePoint grubu seçin **sonraki**.
   
    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. Merhaba üzerinde **çevrimiçi yedekleme zamanlamasını belirtin** sayfasında, tercih ettiğiniz zamanlamayı seçin ve ardından **sonraki**.
    
    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)
    
    > [!NOTE]
    > DPM, farklı zamanlarda en fazla iki günlük yedekleri tooAzure sağlar. Azure yedekleme de hello yedeklemeler yoğun ve yoğun olmayan saatler için kullanarak kullanılabilir WAN bant genişliği miktarını kontrol [Azure yedekleme ağ azaltma](https://azure.microsoft.com/en-in/documentation/articles/backup-configure-vault/#enable-network-throttling).
    > 
    > 
11. Merhaba üzerinde seçili hello yedekleme zamanlaması bağlı olarak **çevrimiçi bekletme ilkesini belirtin** sayfası, günlük, haftalık, aylık ve yıllık yedekleme noktaları için select hello bekletme ilkesi.
    
    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)
    
    > [!NOTE]
    > DPM, farklı yedekleme noktaları için farklı bir bekletme ilkesi seçilebilir bir üst öğe son bekletme düzeni kullanır.
    > 
    > 
12. Benzer toodisk bir ilk başvuru noktası çoğaltmasını Azure içinde oluşturulan toobe gerekir. Tercih edilen seçenek toocreate ilk yedek kopyayı tooAzure seçin ve ardından **sonraki**.
    
    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. Merhaba üzerinde seçtiğiniz ayarları gözden **Özet** sayfasında ve ardından **Grup Oluştur**. Merhaba koruma grubu oluşturulduktan sonra bir başarı iletisi görürsünüz.
    
    ![Özet](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-dpm"></a>DPM kullanarak bir SharePoint öğesi diskten geri yükleme
Aşağıdaki örneğine hello hello *SharePoint kurtarma öğesi* yanlışlıkla silinmişse ve kurtarılan toobe gerekiyor.
![DPM SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)

1. Açık hello **DPM Yönetici Konsolu'nu**. DPM tarafından korunan tüm SharePoint grupları hello gösterilen **koruma** sekmesi.
   
    ![DPM SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. toobegin toorecover hello öğesi, select hello **kurtarma** sekmesi.
   
    ![DPM SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. SharePoint için arama yapabilirsiniz *SharePoint kurtarma öğesi* kurtarma içinde bir joker karakter tabanlı arama kullanarak aralığı gösterin.
   
    ![DPM SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. Merhaba Arama sonuçlarından Hello uygun kurtarma noktası seçin, hello öğeyi sağ tıklatın ve ardından **kurtarmak**.
5. Ayrıca, çeşitli kurtarma noktalarına göz ve bir veritabanı veya öğeyi toorecover seçebilirsiniz. Seçin **tarihi > kurtarma süresini**ve ardından hello doğru **veritabanı > SharePoint grubu > kurtarma noktası > öğesi**.
   
    ![DPM SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
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
9. Hazırlama bir SQL Server örneğinin konumu toorecover hello veritabanı geçici olarak sağlayın ve hello DPM sunucusunda ve SharePoint toorecover hello öğesi çalıştıran hello sunucusunda hazırlama bir dosya paylaşımı sağlayın.
   
    ![Hazırlama Location1](./media/backup-azure-backup-sharepoint/staging-location1.png)
   
    DPM hello SharePoint öğesi toohello geçici SQL Server örneği barındırma hello içerik veritabanını ekler. Hello içerik veritabanından hello DPM sunucusu hello öğesi kurtarır ve dosya konumu hello DPM sunucusunda hazırlama hello üzerinde yerleştirir. Merhaba hello DPM sunucusunun konumunu şimdi hazırlama hello üzerinde olduğu Kurtarılan bir öğeye hazırlama konumuna hello SharePoint grubu üzerinde dışarı toobe toohello gerekir.
   
    ![Hazırlama Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. Seçin **kurtarma seçeneklerini belirtin**, güvenlik ayarları toohello SharePoint grubu uygulamak ve hello kurtarma noktası hello güvenlik ayarlarını uygula. **İleri**’ye tıklayın.
    
    ![Kurtarma Seçenekleri](./media/backup-azure-backup-sharepoint/recovery-options.png)
    
    > [!NOTE]
    > Toothrottle hello ağ bant genişliği kullanımını seçebilirsiniz. Bu etki toohello üretim sunucusu üretim saatleri dışında en aza indirir.
    > 
    > 
11. Merhaba özet bilgileri gözden geçirin ve ardından **kurtarmak** hello dosyasının toobegin kurtarma.
    
    ![Kurtarma özeti](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. Şimdi hello seçin **izleme** hello sekmesinde **DPM Yönetici Konsolu'nu** tooview hello **durum** hello kurtarma.
    
    ![Kurtarma durumu](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)
    
    > [!NOTE]
    > Merhaba dosya şimdi geri yüklenir. Merhaba SharePoint site toocheck geri hello dosyası yenileyebilirsiniz.
    > 
    > 

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a>DPM kullanarak bir SharePoint veritabanı Azure'dan geri yükleme
1. bir SharePoint içerik veritabanı toorecover (daha önce gösterildiği gibi) çeşitli kurtarma noktalarına göz ve toorestore istediğiniz hello kurtarma noktası seçin.
   
    ![DPM SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. Merhaba SharePoint kurtarma noktası tooshow hello kullanılabilir SharePoint katalog bilgileri çift tıklayın.
   
   > [!NOTE]
   > Merhaba SharePoint grubu Azure uzun vadeli bekletme için korumalı olduğundan, hiçbir Kataloğu bilgi (meta veriler) hello DPM sunucusunda kullanılabilir. Zaman içinde nokta SharePoint içerik veritabanını kurtarılan toobe her gerektiğinde, sonuç olarak, toocatalog hello SharePoint grubu yeniden gerekir.
   > 
   > 
3. Tıklatın **yeniden kataloglama**.
   
    ![DPM SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)
   
    Merhaba **bulut yeniden katalogla** durum penceresi açar.
   
    ![DPM SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)
   
    Katalog tamamlandıktan sonra hello çok durumuna*başarı*. **Kapat**’a tıklayın.
   
    ![DPM SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. Merhaba DPM gösterilen hello SharePoint nesnesine tıklayın **kurtarma** sekmesinde tooget hello içerik veritabanı yapısı. Merhaba öğeyi sağ tıklatın ve ardından **kurtarmak**.
   
    ![DPM SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. Bu noktada, hello izleyin [kurtarma adımları bu makalenin önceki bölümlerinde](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover diskten bir SharePoint içerik veritabanı.

## <a name="faqs"></a>SSS
S: hangi sürümlerinin DPM, SQL Server 2014 ve SQL 2012 (SP2) destekliyor?<br>
Y: DPM 2012 R2 güncelleştirme paketi 4 ile hem de destekler.

S: bir SharePoint öğesi toohello özgün konumuna, SharePoint SQL AlwaysOn (disk koruması) kullanılarak yapılandırılmışsa kurtarma?<br>
A: Evet hello öğesi kurtarılan toohello özgün SharePoint sitesi olabilir.

S: bir SharePoint veritabanı toohello özgün konumu, SQL AlwaysOn kullanarak SharePoint yapılandırdıysanız kurtarmak?<br>
A: SharePoint veritabanlarını SQL AlwaysOn yapılandırıldığından, bunlar hello kullanılabilirlik grubu kaldırılmadığı sürece değiştirilemez. Sonuç olarak, DPM bir veritabanı toohello özgün konumuna geri yükleyemezsiniz. Bir SQL Server veritabanı tooanother SQL Sunucusu örneğine kurtarabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
* DPM SharePoint koruması hakkında daha fazla bilgi - bkz [Video serisi - SharePoint DPM koruma](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)
* Gözden geçirme [System Center 2012 - Data Protection Manager için sürüm notları](https://technet.microsoft.com/library/jj860415.aspx)
* Gözden geçirme [System Center 2012 SP1 Data Protection Manager için sürüm notları](https://technet.microsoft.com/library/jj860394.aspx)

