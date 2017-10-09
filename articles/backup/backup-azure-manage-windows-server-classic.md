---
title: "aaaManage Azure yedekleme kasaları ve sunucuları Azure hello Klasik dağıtım modeli kullanarak | Microsoft Docs"
description: "Bu öğretici toolearn nasıl toomanage Azure yedekleme kasaları ve sunucuları kullanın."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a>Azure yedekleme kasaları ve hello Klasik dağıtım modelini kullanarak sunucuları yönetme
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-manage-windows-server.md)
> * [Klasik](backup-azure-manage-windows-server-classic.md)
>
>

Bu makalede, hello yedekleme yönetim görevlerini hello Klasik Azure portalı kullanılabilir ve Microsoft Azure Yedekleme aracısı hello genel bakış bulabilirsiniz.

> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

> [!IMPORTANT]
> Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz. Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.<br/> 15 Ekim 2017 sonra PowerShell toocreate yedekleme kasaları kullanamazsınız. **1 Kasım 2017’ye kadar**:
>- Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.
>- Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır. Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.
>

## <a name="management-portal-tasks"></a>Yönetim Portalı görevleri
1. İçinde toohello oturum [Yönetim Portalı](https://manage.windowsazure.com).
2. Tıklatın **kurtarma Hizmetleri**, ardından yedekleme kasası tooview hello hızlı başlangıç sayfası hello adına tıklayın.

    ![Kurtarma Hizmetleri](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

Merhaba sayfanın üst kısmındaki hello hızlı başlangıç Hello seçenekleri belirleyerek, hello kullanılabilir yönetim görevlerini görebilirsiniz.

![Sekmeleri yönetme](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a>Pano
Seçin **Pano** toosee hello kullanım hello sunucusu için genel bakış. Merhaba **kullanıma genel bakış** içerir:

* toocloud kayıtlı Windows sunucuları Hello sayısı
* Azure sanal makine buluta korumalı Hello sayısı
* Azure'da tüketilen hello toplam depolama alanı
* en son işlerin Hello durumu

Hello Pano Hello altındaki hello aşağıdaki görevleri gerçekleştirebilirsiniz:

* **Sertifika yönetmek** - bir sertifika kullanılan tooregister hello sunucu sonra bu tooupdate hello sertifika kullanın. Kasa kimlik bilgileri kullanıyorsanız kullanmayın **Yönet sertifika**.
* **Silme** -siler hello geçerli yedekleme kasası. Bir yedekleme kasası artık kullanılmayan depolama alanını toofree silebilirsiniz. **Silme** tüm kayıtlı sunucuları hello kasasından silinmiş sonra yalnızca etkinleştirilir.

![Yedekleme Pano görevleri](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a>Kayıtlı öğeler
Seçin **kayıtlı öğeler** tooview hello adları olan hello sunucularının toothis kasasına kayıtlı.

![Kayıtlı öğeler](./media/backup-azure-manage-windows-server-classic/registered-items.png)

Merhaba **türü** filtre Varsayılanları tooAzure sanal makine. kayıtlı toothis kasası hello sunucuları tooview hello adlarını seçin **Windows server** hello açılan menüsünde.

Buradan hello aşağıdaki görevleri gerçekleştirebilirsiniz:

* **Yeniden kayda izin** - kullanabileceğiniz bir sunucu için bu seçenek belirlendiğinde, hello **Kayıt Sihirbazı'nı** Server'daki hello şirket içi Microsoft Azure Yedekleme aracısı tooregister hello hello yedekleme kasası ikinci kez . Merhaba sertifika veya bir sunucu yeniden toobe sahip tooan hata nedeniyle toore kaydını gerekebilir.
* **Silme** -hello yedekleme kasasından bir sunucu siler. Tüm hello sunucuyla ilişkili hello depolanan verileri hemen silinir.

    ![Kayıtlı öğeleri görevleri](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a>Korumalı öğeler
Seçin **korunan öğeler** hello sunucularından yedeklenmiş tooview hello öğeleri.

![Korumalı öğeler](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a>Yapılandırma
Merhaba gelen **yapılandırma** sekmesini hello uygun depolama artıklığı seçeneği seçebilirsiniz. Merhaba en iyi zaman tooselect hello depolama artıklığı seçeneği bir kasa oluşturarak hemen sonra ve herhangi bir makine kayıtlı tooit önce ' dir.

> [!WARNING]
> Bir öğe kayıtlı toohello kasası silindikten sonra hello depolama artıklığı seçeneği kilitli ve değiştirilemez.
>
>

![Yapılandırma](./media/backup-azure-manage-windows-server-classic/configure.png)

Bu makalede daha fazla bilgi için bkz: [depolama artıklığı](../storage/common/storage-redundancy.md).

## <a name="microsoft-azure-backup-agent-tasks"></a>Microsoft Azure Yedekleme aracısı görevleri
### <a name="console"></a>Konsol
Açık hello **Microsoft Azure Yedekleme aracısı** (makinenizi arayarak bulabilirsiniz *Microsoft Azure yedekleme*).

![Yedekleme aracısı](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

Merhaba gelen **Eylemler** yönetim görevleri aşağıdaki hello gerçekleştirebilirsiniz hello yedekleme aracısını konsolunun sağ hello bulunabilir:

* Sunucuyu kaydetmek
* Yedekleme zamanlaması
* Şimdi Yedekle
* Özelliklerini değiştir

![Aracı konsol eylemleri](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> çok**verileri kurtarabilirsiniz**, bkz: [geri dosyaları tooa Windows server veya Windows istemci makinesi](backup-azure-restore-windows-server.md).
>
>

### <a name="modify-an-existing-backup"></a>Varolan bir yedeği değiştirme
1. Merhaba Microsoft Azure yedekleme Aracısı'nı **yedekleme zamanlaması**.

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. Merhaba, **yedeklemeyi Zamanlama Sihirbazı** hello bırakın **toobackup öğeler veya kez değişiklik yapma** seçeneğe ve tıklatın **sonraki**.

    ![Zamanlanmış yedekleme değiştirme](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. Tooadd istediğiniz veya öğelerde hello değiştirme **öğeleri seçin tooBackup** ekran tıklatın **öğeleri Ekle**.

    Ayrıca ayarlayabilirsiniz **dışarıda bırakma ayarları** hello Sihirbazı'nda bu sayfadan. Dosya türlerini eklemek için hello yordamı okuma ya da tooexclude dosyaları istiyorsanız [dışarıda bırakma ayarları](#exclusion-settings).
4. Merhaba dosya ve tooback yedeklemek istediğiniz klasörleri seçin **Tamam**.

    ![Öğe ekle](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. Merhaba belirtin **yedekleme zamanlaması** tıklatıp **sonraki**.

    (En fazla günde 3 kereye) günlük veya haftalık yedeklemeler zamanlayabilirsiniz.

    ![Yedekleme zamanlamasını belirtin](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Bu ayrıntılı açıklanmıştır Hello yedekleme zamanlamasını belirtme [makale](backup-azure-backup-cloud-as-tape.md).
   >
   >
6. Select hello **Bekletme İlkesi** hello yedek kopya ve tıklatın **sonraki**.

    ![Bekletme İlkesi seçin](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. Merhaba üzerinde **onay** ekranında hello bilgileri gözden geçir ve tıklatın **son**.
8. Merhaba oluşturma Hello Sihirbazı tamamlandıktan sonra **yedekleme zamanlaması**, tıklatın **Kapat**.

    Korumayı değiştirdikten sonra yedeklemeler giderek toohello tarafından doğru şekilde tetikleme onaylayabilirsiniz **işleri** sekmesi ve değişiklikler hello yansıtılır onaylayan yedekleme işleri.

### <a name="enable-network-throttling"></a>Ağ azaltmayı etkinleştir
veri aktarımı sırasında ağ bant genişliğinin nasıl kullanıldığını toocontrol sağlayan bir azaltma sekmesi Hello Azure Backup aracısını sağlar. Bu denetim verileri tooback çalışma saatlerinde gerekir, ancak diğer Internet trafiği ile Merhaba yedekleme işlemi toointerfere istiyor musunuz yararlı olabilir. Verilerin azaltma aktarımı yukarıya tooback uygular ve geri yükleme etkinlikleri.  

tooenable azaltma:

1. Merhaba, **Backup Aracısı**, tıklatın **özelliklerini değiştirme**.
2. Select hello **yedekleme işlemleri için Internet bant genişliği kullanımı daraltmayı etkinleştir** onay kutusu.

    ![Ağ azaltma](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. Azaltma etkinleştirdikten sonra sırasında yedek veri aktarımı için bant genişliği izin verilen hello belirtin **çalışma saatleri** ve **çalışılmayan saatler**.

    Merhaba bant genişliği değerler 512 KB / saniye (Kbps) başlar ve too1023 megabayt (Mbps) saniyede yukarı gidebilirsiniz. Ayrıca hello başlangıç belirleyin ve için son **çalışma saatleri**, ve hello haftanın hangi günleri iş dikkate gün. Merhaba çalışma saatleri belirlenmiş hello dışında dikkate alınan toobe İş dışı saatler saattir.
4. **Tamam** düğmesine tıklayın.

## <a name="exclusion-settings"></a>Dışlama ayarları
1. Açık hello **Microsoft Azure Yedekleme aracısı** (makinenizi arayarak bulabilirsiniz *Microsoft Azure yedekleme*).

    ![Açık Yedekleme aracısı](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. Merhaba Microsoft Azure yedekleme Aracısı'nı **yedekleme zamanlaması**.

    ![Windows Server yedeklemesini zamanlama](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. Merhaba yedeklemeyi Zamanlama Sihirbazı hello bırakın **toobackup öğeler veya kez değişiklik yapma** seçeneğe ve tıklatın **sonraki**.

    ![Bir zamanlamayı değiştirmek](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. Tıklatın **dışlama ayarları**.

    ![Öğeleri tooexclude seçin](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. Tıklatın **dışlama eklemek**.

    ![Özel durumları ekleme](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. Merhaba konum seçin ve ardından **Tamam**.

    ![Dışlama için bir konum seçin](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. Hello Hello dosya uzantısını Ekle **dosya türü** alan.

    ![Dosya türüne göre Dışla](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    .Mp3 uzantı ekleme

    ![Dosya türü örneği](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    tooadd başka bir uzantı tıklatın **dışlama Ekle** ve (.jpeg uzantı eklemeden) başka bir dosya türü uzantısını girin.

    ![Başka bir dosya türü örneği](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. Tüm hello uzantıları eklediğinizde, tıklatın **Tamam**.
9. Yedeklemeyi zamanlama Sihirbazı Hello tıklayarak devam **sonraki** hello kadar **onay sayfası**, ardından **son**.

    ![Dışlama onayı](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a>Sonraki adımlar
* [Windows Server veya Windows İstemcisi Azure'dan geri yükleme](backup-azure-restore-windows-server.md)
* Azure yedekleme hakkında daha fazla toolearn bakın [Azure Yedekleme'ye Genel Bakış](backup-introduction-to-azure-backup.md)
* Merhaba ziyaret [Azure yedekleme Forumu](http://go.microsoft.com/fwlink/p/?LinkId=290933)
