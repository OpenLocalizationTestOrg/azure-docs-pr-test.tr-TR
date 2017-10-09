---
title: "aaaManage Azure kurtarma Hizmetleri kasa ve sunucularınızı | Microsoft Docs"
description: "Bu öğretici toolearn nasıl toomanage Azure kurtarma Hizmetleri kasaları ve sunucuları kullanın."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a>Windows makineleri için Azure kurtarma hizmetleri kasaları ile sunucularını izleme ve yönetme
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-manage-windows-server.md)
> * [Klasik](backup-azure-manage-windows-server-classic.md)
>
>

Bu makalede, yedekleme izleme ve yönetim görevlerini hello Azure portal ve hello Microsoft Azure Yedekleme aracısı kullanılabilir hello genel bir bakış bulabilirsiniz. Bu makalede, zaten bir Azure aboneliğiniz varsa ve en az bir kurtarma Hizmetleri kasası oluşturdunuz varsayılır.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a>Kurtarma Hizmetleri kasası açın

Merhaba kurtarma Hizmetleri kasa Panosu hello ayrıntıları veya bir kurtarma Hizmetleri kasası özniteliklerini gösterir.

1. İçinde toohello oturum [Azure Portal](https://portal.azure.com/) Azure aboneliğinizi kullanarak.
2. Merhaba Hub menüsünde **daha Hizmetleri**.

    ![Kurtarma Hizmetleri kasaları adım 1'in açık listesi](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. Kurtarma Hizmetleri kasası tooopen istiyor. Merhaba iletişim kutusunda, yazmaya başlayın **kurtarma Hizmetleri**. Yazmaya başladığınızda, hello filtreleyecek girişinize bağlı. Tıklatın **kurtarma Hizmetleri kasaları** toodisplay hello listesi kurtarma Hizmetleri kasaları aboneliğinizde.

    ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    Merhaba kurtarma Hizmetleri kasalarının listesi açılır.

    ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. Kasa Hello listesinden, hello tooopen istediğiniz kurtarma Hizmetleri kasası hello adını seçin. Merhaba kurtarma Hizmetleri kasası Pano dikey pencere açılır.

    ![Kurtarma Hizmetleri kasa Panosu](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    Merhaba kurtarma Hizmetleri kasası açtığınız, hello izleme veya yönetim görevlerinden herhangi birini deneyin.

## <a name="monitor-backup-jobs-and-alerts"></a>Yedekleme işleri izleme ve uyarılar

İşlerini izleme ve hello uyarıları, gördüğünüz Pano, Kurtarma Hizmetleri Kasası:

* Yedekleme uyarıları ayrıntıları
* Dosyaları ve klasörleri yanı sıra, hello bulutta korunan Azure sanal makineler
* Azure'da tüketilen toplam depolama alanı
* Yedekleme işi durumu

![Yedekleme Pano görevleri](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

Her bu kutucukların Hello bilgi tıklandığında ilgili görevleri yöneteceğiniz hello ilişkili dikey pencere açılır.

Merhaba Pano Hello üst kısmından:

* Ayarları kullanılabilir yedekleme görevleri erişim sağlar.
* Kasa yedekleme - toohello kurtarma Hizmetleri yeni dosyalar ve klasörler (veya Azure VM'ler) yedekleme yardımcı olur.
* Bir kurtarma Hizmetleri kasası silme - artık kullanılmayan, depolama alanı toofree silin. Tüm korumalı sunuculardaki hello kasasından silinmiş sonra Sil yalnızca etkinleştirilir.

![Yedekleme Pano görevleri](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a>Azure Yedekleme aracısı kullanarak yedeklemeler için uyarılar:
| Uyarı düzeyi | Gönderilen uyarıları |
| --- | --- |
| Kritik |Yedekleme hatası, Kurtarma hatası |
| Uyarı |Yedekleme (toocorruption sorunları daha az yüz dosyaları yedeklenmez ve bir milyondan fazla dosyalar başarıyla yedeklendi olduğunda) uyarılarla tamamlandı |
| Bilgilendirme |None |

## <a name="manage-backup-alerts"></a>Yedekleme Uyarıları yönetme
Merhaba tıklatın **yedekleme uyarıları** döşeme tooopen hello **yedekleme uyarıları** dikey uyarıları ve yönetin.

![Yedekleme uyarıları](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

sayısı hello hello yedekleme uyarıları kutucuğu gösterir:

* Son 24 saat içinde çözümlenmemiş kritik uyarılar
* Son 24 saat içinde çözümlenmemiş uyarı bildirimleri

Her bu bağlantıları tıklatarak alır, toohello **yedekleme uyarıları** dikey penceresinde bu uyarıların (kritik veya uyarılan) filtre uygulanmış bir görünümle.

Merhaba yedekleme uyarıları dikey penceresinden:

* Uyarılarınızı ile Merhaba uygun bilgileri tooinclude seçin.

    ![Sütunları seçin](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* Uyarıları önem derecesi, durum ve başlangıç/bitiş zamanlarını filtreleyin.

    ![Filtre uyarıları](./media/backup-azure-manage-windows-server/filter-alerts.png)
* Önem derecesi, sıklığı ve alıcıların bildirimlerini yapılandırma gibi uyarıları Aç veya kapat.

    ![Filtre uyarıları](./media/backup-azure-manage-windows-server/configure-notifications.png)

Varsa **başına uyarı** hello seçilen **bildirim** sıklığı hiçbir gruplandırma veya e-postaları düşüş ortaya çıkar. Her uyarı 1 bildiriminde sonuçlanır. Merhaba varsayılan ayar budur ve hello çözümleme e-posta ayrıca hemen gönderilir.

Varsa **saatlik Özet** hello seçili **bildirim** çözümlenmemiş hello son bir saat oluşturulan yeni uyarılar sıklığı toohello kullanıcı olduğunu söyleyen bir e-posta gönderilir. Merhaba hello saat sonunda çözümleme e-posta gönderilir.

Uyarıları önem dereceleri aşağıdaki Merhaba gönderilebilir:

* Kritik
* Uyarı
* Bilgi

Merhaba ile Merhaba uyarıyı devre dışı bırakmak **devre dışı bırak** hello iş ayrıntıları dikey penceresinde düğmesi. ' I tıklattığınızda devre dışı bırak, çözümleme notları sağlayabilir.

Merhaba sütunları seçin hello hello uyarısıyla bir parçası olarak tooappear istediğiniz **sütunları seçin** düğmesi.

> [!NOTE]
> Merhaba gelen **ayarları** dikey penceresinde seçerek yedekleme Uyarıları yönetme **izleme ve Raporlar > Uyarı ve olayları > Yedekleme uyarıları** ve ardından **filtre** veya  **Bildirimleri Yapılandırma**.
>
>

## <a name="manage-backup-items"></a>Yedekleme öğeleri yönetme
Şirket içi yedeklemeler yönetme hello Yönetim Portalı'nda kullanıma sunulmuştur. Merhaba yedekleme bölümünde hello Pano hello **yedekleme öğeleri** kutucuğunda gösterilir yedekleme öğeleri hello sayısı toohello kasası korumalı.

Tıklatın **dosya klasörleri** yedekleme öğeleri döşeme hello içinde.

![Yedekleme öğeleri döşeme](./media/backup-azure-manage-windows-server/backup-items-tile.png)

Merhaba yedekleme ile Merhaba dikey pencere açılır öğelere kümesi tooFile-klasörü öğesi listelenen her belirli yedekleme gördüğünüz filtre uygulayın.

![Yedekleme öğeleri](./media/backup-azure-manage-windows-server/backup-item-list.png)

Belirli bir yedekleme öğesi hello listeden seçerseniz, bu öğenin temel ayrıntılarını hello bakın.

> [!NOTE]
> Merhaba gelen **ayarları** dikey penceresinde, dosyaları ve klasörleri seçerek yönetme **korumalı öğeler > yedekleme öğeleri** seçilerek **dosya klasörleri** hello açılan menüsünde.
>
>

![Yedekleme öğeleri ayarları](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a>Yedekleme işlerini yönetme
(Merhaba şirket içi sunucu tooAzure yedeklerken) şirket içi ve Azure yedeklemeleri için yedekleme işlerinin başlangıç panosunda görünür.

Hello hello Pano yedekleme bölümü, hello yedekleme işi kutucuğunu işleri hello sayısını gösterir:

* Sürüyor
* Hello son 24 saat başarısız oldu.

toomanage yedekleme işlerinizi tıklatın hello **yedekleme işleri** döşeme, hangi hello yedekleme işleri dikey penceresi açılır.

![Yedekleme öğeleri ayarları](./media/backup-azure-manage-windows-server/backup-jobs.png)

Merhaba bilgi hello yedekleme işleri dikey penceresinde hello ile kullanılabilir değiştirme **sütunları seçin** hello sayfanın üst kısmındaki hello düğmesi.

Kullanım hello **filtre** dosyaları ve klasörleri ve Azure sanal makine yedeklemesi arasındaki düğme tooselect.

Yedeklediğiniz dosya ve klasörleri görmüyorsanız, tıklatın **filtre** hello üst hello sayfasının ve Seç düğmesini **dosya ve klasörleri** hello öğesi türü menüsünde.

> [!NOTE]
> Merhaba gelen **ayarları** dikey penceresinde seçerek yedekleme işlerini yönetme **izleme ve raporlama > işleri > yedekleme işleri** seçilerek **dosya klasörleri** hello açılır Menüyü aşağı.
>
>

## <a name="monitor-backup-usage"></a>Yedekleme kullanımını izleme
Hello hello Pano yedekleme bölümü, hello yedekleme kullanımı kutucuğu Azure'da tüketilen hello depolamayı gösterir. Depolama kullanım için sağlanır:

* Merhaba kasayla ilişkili bulut LRS depolama kullanımı
* Merhaba kasayla ilişkili bulut GRS depolama kullanımı

## <a name="manage-your-production-servers"></a>Üretim sunucularını yönetme
Üretim sunucularınızı toomanage tıklatın **ayarları**.

Altında Yönet'i **yedekleme altyapısı > üretim sunucuları**.

Tüm kullanılabilir üretim sunucularınızın Hello üretim sunucuları dikey listeler. Merhaba listesi tooopen hello sunucu ayrıntıları Server'da tıklayın.

![Korumalı öğeler](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a>Açık hello Azure Yedekleme aracısı
Açık hello **Microsoft Azure Yedekleme aracısı** (, makinenizde arama yaparak Bul *Microsoft Azure yedekleme*).

![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/snap-in-search.png)

Merhaba gelen **Eylemler** yönetim görevleri aşağıdaki hello gerçekleştirdiğiniz hello yedekleme aracısını konsolunun sağ hello bulunabilir:

* Sunucuyu kaydetmek
* Yedekleme zamanlaması
* Şimdi Yedekle
* Özelliklerini değiştir

![Microsoft Azure Yedekleme aracısı konsol Eylemler](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> çok**verileri kurtarabilirsiniz**, bkz: [geri dosyaları tooa Windows server veya Windows istemci makinesi](backup-azure-restore-windows-server.md).
>
>

## <a name="modify-hello-backup-schedule"></a>Merhaba yedekleme zamanlamasını Değiştir
1. Merhaba Microsoft Azure yedekleme Aracısı'nı **yedekleme zamanlaması**.

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. Merhaba, **yedeklemeyi Zamanlama Sihirbazı** hello bırakın **toobackup öğeler veya kez değişiklik yapma** seçeneğe ve tıklatın **sonraki**.

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. Tooadd istediğiniz veya öğelerde hello değiştirme **öğeleri seçin tooBackup** ekran tıklatın **öğeleri Ekle**.

    Ayrıca ayarlayabilirsiniz **dışarıda bırakma ayarları** hello Sihirbazı'nda bu sayfadan. Dosya türlerini eklemek için hello yordamı okuma ya da tooexclude dosyaları istiyorsanız [dışarıda bırakma ayarları](#manage-exclusion-settings).
4. Merhaba dosya ve tooback yedeklemek istediğiniz klasörleri seçin **Tamam**.

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. Merhaba belirtin **yedekleme zamanlaması** tıklatıp **sonraki**.

    (En fazla günde 3 kereye) günlük veya haftalık yedeklemeler zamanlayabilirsiniz.

    ![Windows Server Yedekleme öğeleri](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Bu ayrıntılı açıklanmıştır Hello yedekleme zamanlamasını belirtme [makale](backup-azure-backup-cloud-as-tape.md).
   >

6. Select hello **Bekletme İlkesi** hello yedek kopya ve tıklatın **sonraki**.

    ![Windows Server Yedekleme öğeleri](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. Merhaba üzerinde **onay** ekranında hello bilgileri gözden geçir ve tıklatın **son**.
8. Merhaba oluşturma Hello Sihirbazı tamamlandıktan sonra **yedekleme zamanlaması**, tıklatın **Kapat**.

    Korumayı değiştirdikten sonra yedeklemeler giderek toohello tarafından doğru şekilde tetikleme onaylayabilirsiniz **işleri** sekmesi ve değişiklikler hello yansıtılır onaylayan yedekleme işleri.

## <a name="enable-network-throttling"></a>Ağ azaltmayı etkinleştir

veri aktarımı sırasında ağ bant genişliğinin nasıl kullanıldığını toocontrol sağlayan bir azaltma sekmesi Hello Azure Backup aracısını sağlar. Bu denetim verileri tooback çalışma saatlerinde gerekir, ancak diğer Internet trafiği ile Merhaba yedekleme işlemi toointerfere istiyor musunuz yararlı olabilir. Verilerin azaltma aktarımı yukarıya tooback uygular ve geri yükleme etkinlikleri.  

tooenable azaltma:

1. Merhaba, **Backup Aracısı**, tıklatın **özelliklerini değiştirme**.
2. Merhaba üzerinde ** sekmesini azaltma, seçin **yedekleme işlemleri için Internet bant genişliği kullanımı daraltmayı etkinleştir**.

    ![Ağ azaltma](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    Azaltma etkinleştirdikten sonra sırasında yedek veri aktarımı için bant genişliği izin verilen hello belirtin **çalışma saatleri** ve **çalışılmayan saatler**.

    Merhaba bant genişliği değerler 512 KB / saniye (Kbps) başlar ve too1023 megabayt (Mbps) saniyede yukarı gidebilirsiniz. Ayrıca hello başlangıç belirleyin ve için son **çalışma saatleri**, ve hello haftanın hangi günleri iş dikkate gün. Merhaba çalışma saatleri belirlenmiş hello dışında dikkate alınan toobe İş dışı saatler saattir.
3. **Tamam** düğmesine tıklayın.

## <a name="manage-exclusion-settings"></a>Dışarıda bırakma ayarları yönetme
1. Açık hello **Microsoft Azure Yedekleme aracısı** (makinenizi arayarak bulabilirsiniz *Microsoft Azure yedekleme*).

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. Merhaba Microsoft Azure yedekleme Aracısı'nı **yedekleme zamanlaması**.

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. Merhaba yedeklemeyi Zamanlama Sihirbazı hello bırakın **toobackup öğeler veya kez değişiklik yapma** seçeneğe ve tıklatın **sonraki**.

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. Tıklatın **dışlama ayarları**.

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. Tıklatın **dışlama eklemek**.

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. Merhaba konum seçin ve ardından **Tamam**.

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. Hello Hello dosya uzantısını Ekle **dosya türü** alan.

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    .Mp3 uzantı ekleme

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    tooadd başka bir uzantı tıklatın **dışlama Ekle** ve (.jpeg uzantı eklemeden) başka bir dosya türü uzantısını girin.

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. Tüm hello uzantıları eklediğinizde, tıklatın **Tamam**.
9. Yedeklemeyi zamanlama Sihirbazı Hello tıklayarak devam **sonraki** hello kadar **onay sayfası**, ardından **son**.

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a>Sık sorulan sorular
**S1. neden bunu hemen portalında yansıtılan değil hello Azure Yedekleme aracısı, tamamlandı olarak Hello yedekleme işinin durumunu gösterir?**

Y1. Var. en yüksek gecikmeye hello yedekleme işinin durumu arasında 15 dakika hello Azure Yedekleme aracısı ve hello Azure portal yansıtılır.

**Bir yedekleme işi başarısız olduğunda Q.2 ne kadar süreyle tooraise bir uyarı sürer?**

A.2 bir uyarı hello Azure yedekleme hata 20 dakika içinde oluşturulur.

**S3. Bir e-posta, bildirimleri yapılandırılırsa burada gönderilmez söz konusu var mı?**

Y3. Sipariş tooreduce hello aralığını belirterek uyarı sesini içinde Hello bildirim gönderilmeyecek zaman hello durumlarda aşağıda verilmiştir:

* Bildirimleri saatlik yapılandırıldıysa ve bir uyarı oluşturulur ve hello saat içinde çözümlenen
* İşleri iptal edilir.
* Özgün yedekleme işi devam ettiğinden ikinci yedekleme işi başarısız oldu.

## <a name="troubleshooting-monitoring-issues"></a>İzleme sorunlarını giderme
**Sorun:** işleri ve/veya hello Azure Yedekleme aracısı uyarıları hello Portalı'nda görünmez.

**Sorun giderme adımları:** hello işlemi, ```OBRecoveryServicesManagementAgent```, iş ve uyarı verileri toohello Azure Backup hizmeti hello gönderir. Bu işlem bazen durumunda takılıp kalabilir veya kapatın.

1. tooverify hello işlemi çalışmıyor, açık **Görev Yöneticisi'ni** ve onay hello varsa ```OBRecoveryServicesManagementAgent``` işlem çalışıyor.
2. Merhaba işlemi çalışmıyor varsayılarak açmak **Denetim Masası** ve hizmetlerin listesini hello göz atın. Başlatma veya yeniden **Microsoft Azure kurtarma Hizmetleri yönetim Aracısı**.

    Daha fazla bilgi için hello günlüklerine göz atın:<br/>
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*`Örneğin:<br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a>Sonraki adımlar
* [Windows Server veya Windows İstemcisi Azure'dan geri yükleme](backup-azure-restore-windows-server.md)
* Azure yedekleme hakkında daha fazla toolearn bakın [Azure Yedekleme'ye Genel Bakış](backup-introduction-to-azure-backup.md)
* Merhaba ziyaret [Azure yedekleme Forumu](http://go.microsoft.com/fwlink/p/?LinkId=290933)
