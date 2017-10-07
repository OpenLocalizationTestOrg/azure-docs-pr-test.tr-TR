---
title: "aaaMonitor Resource Manager tarafından dağıtılan sanal makine yedeklerini | Microsoft Docs"
description: "Olayları ve Resource Manager tarafından dağıtılan sanal makine yedeklerini uyarıları izleyin. Uyarılar temelinde e-posta gönderin."
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: fed32015-2db2-44f8-b204-d89f6fd1bea2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: markgal;trinadhk;giridham;
ms.openlocfilehash: bf45cbaa05621b2365c26bafa1bd8223a444c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-alerts-for-azure-virtual-machine-backups"></a>Azure sanal makine yedekleme uyarılarını izleme
Uyarıları olay eşiği karşıladığında veya aşılan hello hizmetinden yanıtları değildir. Bilerek sorunları başlangıç iş maliyetlerini azaltır kritik tookeeping zaman olabilir. Uyarıları genellikle bir zamanlamaya göre gerçekleşmez ve uyarılar ortaya sonra dolayısıyla yararlı tooknow mümkün olan en kısa sürede taşır. Örneğin, bir yedekleme veya geri yükleme işi başarısız olduğunda bir uyarı hello hatanın beş dakika içinde gerçekleşir. Merhaba kasa panosunda, yedekleme uyarılar kutucuğu hello kritik ve uyarı düzeyi olayları görüntüler. Merhaba yedekleme uyarıları Ayarları'nda, tüm olayları görüntüleyebilirsiniz. Ancak ayrı bir sorunu çalışırken bir uyarı ortaya çıkarsa ne yapacaksınız? Merhaba uyarı gerçekleştiğinde bunu bilmiyorsanız, küçük bir sorundan dolayı olabilir veya veri tehlikeye atabilecek. oluştuğunda, toomake emin hello doğru kişilerin bir uyarının - kullanan hello hizmet toosend Uyarı bildirimlerinin e-posta yoluyla yapılandırın. E-posta bildirimlerini ayarlama hakkında daha fazla bilgi için bkz: [bildirimleri yapılandırmak](backup-azure-monitor-vms.md#configure-notifications).

## <a name="how-do-i-find-information-about-hello-alerts"></a>Merhaba uyarılar hakkında bilgileri nasıl bulabilirim?
tooview bilgileri bir uyarı oluşturdu hello olay hakkında hello yedekleme uyarıları dikey penceresi açmanız gerekir. İki yolu tooopen hello yedekleme uyarıları dikey vardır: yedekleme uyarılar kutucuğu hello kasa panosunda hello gelen veya hello uyarı ve olayları dikey.

tooopen hello yedekleme uyarıları dikey penceresinden yedekleme uyarıları döşeme:

* Merhaba üzerinde **yedekleme uyarıları** döşeme hello kasa panosunda, tıklatın **kritik** veya **uyarı** tooview hello bu önem düzeyi için çalışma olaylarını.

    ![Yedekleme uyarıları kutucuğu](./media/backup-azure-monitor-vms/backup-alerts-tile.png)

tooopen hello yedekleme uyarıları dikey hello uyarı ve olayları dikey penceresinden:

1. Merhaba kasası panodan tıklatın **tüm ayarları**. ![Tüm ayarlar düğmesi](./media/backup-azure-monitor-vms/all-settings-button.png)
2. Merhaba üzerinde **ayarları** dikey penceresinde tıklatın **uyarı ve olayları**. ![Uyarı ve olayları düğmesi](./media/backup-azure-monitor-vms/alerts-and-events-button.png)
3. Merhaba üzerinde **uyarı ve olayları** dikey penceresinde tıklatın **yedekleme uyarıları**. ![Yedekleme uyarıları düğmesi](./media/backup-azure-monitor-vms/backup-alerts.png)

    Merhaba **yedekleme uyarıları** dikey penceresi açılır ve hello filtrelenmiş uyarıları görüntüler.

    ![Yedekleme uyarıları kutucuğu](./media/backup-azure-monitor-vms/backup-alerts-critical.png)
4. tooview ayrıntılı bilgi, olayların hello listesinden belirli bir uyarıyla ilgili hello uyarı tooopen'ı tıklatın, **ayrıntıları** dikey.

    ![Olay Ayrıntıları](./media/backup-azure-monitor-vms/audit-logs-event-detail.png)

    Merhaba listesinde görüntülenen toocustomize hello öznitelikleri [ek olay öznitelikleri görüntüleyin](backup-azure-monitor-vms.md#view-additional-event-attributes)

## <a name="configure-notifications"></a>Bildirimleri yapılandırma
 Merhaba hizmet toosend e-posta bildirimleri hello saati aşan veya belirli türlerdeki olayların ortaya çıktığında oluştu hello uyarılar için yapılandırabilirsiniz.

tooset uyarılar için e-posta bildirimlerini ayarlama

1. Merhaba yedekleme uyarıları menüsünde **bildirimleri yapılandırma**

    ![Yedekleme uyarıları menüsü](./media/backup-azure-monitor-vms/backup-alerts-menu.png)

    Merhaba yapılandırma bildirimleri dikey pencere açılır.

    ![Bildirimleri dikey yapılandırın](./media/backup-azure-monitor-vms/configure-notifications.png)
2. E-posta bildirimlerinin hello yapılandırma bildirimleri dikey tıklatın **üzerinde**.

    Bu bilgiler gereklidir çünkü hello alıcıları ve önem derecesi iletişim kutularındaki yıldız sonraki toothem sahip. En az bir e-posta adresi sağlayın ve en az bir önem derecesini seçin.
3. Merhaba, **alıcılar (e-posta)** iletişim kutusunda, kimin hello bildirimleri almak için türü hello e-posta adresi. Kullanım hello biçimi: username@domainname.com. Birden çok e-posta adresini noktalı virgül (;) ayırın.
4. Merhaba, **bildirim** alanı seçin **başına uyarı** toosend hello değiştiğinde bildirimi belirtilen uyarı oluşur, veya **saatlik Özet** toosend hello son bir saat için bir Özet.
5. Merhaba, **önem** iletişim kutusunda, e-posta bildirimi tootrigger istediğiniz bir veya daha fazla düzeylerini seçin.
6. **Kaydet** düğmesine tıklayın.

   ### <a name="what-alert-types-are-available-for-azure-iaas-vm-backup"></a>Hangi uyarı türleri için Azure Iaas sanal yedekleme var mı?
   | Uyarı düzeyi | Gönderilen uyarıları |
   | --- | --- |
   | Kritik |Yedekleme hatası, Kurtarma hatası |
   | Uyarı |None |
   | Bilgilendirme |None |

### <a name="are-there-situations-where-email-isnt-sent-even-if-notifications-are-configured"></a>Bildirimler yapılandırılmış olsa bile e-postanın gönderilmediği durumlar var mı?
Merhaba bildirimleri düzgün bir şekilde yapılandırmış olmanıza rağmen bir uyarı gönderilmez, durumlar vardır. Hello aşağıdaki durumlarda e-posta bildirimleri tooavoid aralığını belirterek uyarı sesini gönderilmez:

* Bildirimleri yapılandırılmış tooHourly Özet varsa ve bir uyarı oluşturulur ve hello saat içinde çözülür.
* Merhaba işleri iptal edilir.
* Bir yedekleme işi tetiklenir ve sonra başarısız olur ve başka bir yedekleme işi sürüyor.
* Resource Manager etkin bir VM için zamanlanmış bir yedekleme işini başlatır, ancak hello VM artık yok.

## <a name="customize-your-view-of-events"></a>Olayları görünümünü özelleştirme
Merhaba **denetim günlüklerini** ayarı filtreleri ve işletimsel olay bilgilerini gösteren sütunları önceden tanımlanmış bir dizi birlikte gelir. Merhaba görünümünü özelleştirebilirsiniz böylece zaman hello **olayları** dikey penceresi açıldığında, size gösterir hello istediğiniz bilgileri.

1. Merhaba, [kasa Panosu](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), Gözat tooand tıklatın **denetim günlüklerini** tooopen hello **olayları** dikey.

    ![Denetim Günlükleri](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    Merhaba **olayları** toohello çalışma olaylarını yalnızca hello geçerli kasa için filtre dikey pencere açılır.

    ![Denetim günlükleri filtresi](./media/backup-azure-monitor-vms/audit-logs-filter.png)

    Merhaba dikey penceresinde hello listesini kritik, hata, uyarı ve oluştu bilgilendirme olaylarını hello geçen hafta gösterir. Merhaba süresi hello ayarlanmış varsayılan değerdir **filtre**. Merhaba **olayları** dikey penceresinde de hello olaylar meydana geldiğinde izleme bir çubuk grafik gösterir. Merhaba içinde toosee hello çubuk grafik istemiyorsanız **olayları** menüsünde tıklatın **Gizle grafik** tootoggle hello grafik devre dışı. Hello varsayılan olaylarının işlemi, düzey, durum, kaynak ve saat bilgilerini görüntüler. Ek olay öznitelikleri gösterme hakkında daha fazla bilgi için hello bölümüne bakın [olay bilgilerini genişletme](backup-azure-monitor-vms.md#view-additional-event-attributes).
2. Bir işlem olayı hello hakkında ek bilgi için **işlemi** sütun, kendi dikey bir operasyonel olay tooopen tıklayın. Merhaba dikey penceresinde hello olaylarıyla ilgili ayrıntılı bilgiler içerir. Olaylar, kendi bağıntı kimliği ve hello zaman aralığı içinde oluştu hello olaylarının bir listesi göre gruplandırılır.

    ![İşlem ayrıntıları](./media/backup-azure-monitor-vms/audit-logs-details-window.png)
3. tooview ayrıntılı bilgi, olayların hello listesinden belirli bir olay hakkında hello olay tooopen'yı tıklatın, **ayrıntıları** dikey.

    ![Olay Ayrıntıları](./media/backup-azure-monitor-vms/audit-logs-details-window-deep.png)

    Merhaba olay düzeyi bilgileri alır hello olarak ayrıntılı bilgidir. Bu kadar her olay bilgilerini görme tercih ederseniz ve tooadd istiyorsanız bu çok ayrıntı toohello **olayları** dikey penceresinde hello bölümüne bakın [olay bilgilerini genişletme](backup-azure-monitor-vms.md#view-additional-event-attributes).

## <a name="customize-hello-event-filter"></a>Merhaba olay filtresi özelleştirme
Kullanım hello **filtre** tooadjust veya belirli bir dikey pencerede görüntülenir hello bilgilerini seçin. toofilter hello olay bilgileri:

1. Merhaba, [kasa Panosu](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), Gözat tooand tıklatın **denetim günlüklerini** tooopen hello **olayları** dikey.

    ![Denetim Günlükleri](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    Merhaba **olayları** toohello çalışma olaylarını yalnızca hello geçerli kasa için filtre dikey pencere açılır.

    ![Denetim günlükleri filtresi](./media/backup-azure-monitor-vms/audit-logs-filter.png)
2. Merhaba üzerinde **olayları** menüsünde tıklatın **filtre** tooopen o dikey.

    ![Filtre dikey penceresini açın](./media/backup-azure-monitor-vms/audit-logs-filter-button.png)
3. Merhaba üzerinde **filtre** dikey penceresinde hello ayarlamak **düzeyi**, **süresi**, ve **arayan** filtreler. Merhaba kurtarma Hizmetleri kasası için tooprovide hello geçerli bilgileri ayarlanan beri hello diğer filtreleri kullanılabilir değil.

    ![Denetim günlükleri Sorgu Ayrıntıları](./media/backup-azure-monitor-vms/filter-blade.png)

    Merhaba belirtebilirsiniz **düzeyi** olayın: kritik, hata, uyarı veya bilgilendirici. Olay düzeyleri herhangi bir birleşimini seçebilirsiniz, ancak en az bir düzey seçili olması gerekir. Merhaba düzeyi açmak veya kapatmak Değiştir. Merhaba **süresi** filtre toospecify hello süreyi olayları yakalamak için sağlar. Özel bir zaman aralığı kullanırsanız, hello başlangıç ayarlayın ve bitiş saatlerini.
4. Filtre kullanarak hazır tooquery hello işlem günlüklerini olduktan sonra tıklatın **güncelleştirme**. Merhaba sonuçları görüntülemek hello **olayları** dikey.

    ![İşlem ayrıntıları](./media/backup-azure-monitor-vms/edited-list-of-events.png)

### <a name="view-additional-event-attributes"></a>Ek olay öznitelikleri görüntüleyin
Hello kullanarak **sütunları** düğmesi, ek olay öznitelikleri tooappear hello hello listesinde etkinleştirebilirsiniz **olayları** dikey. Merhaba varsayılan olaylarının listesi işlemi, düzey, durum, kaynak ve saat bilgilerini görüntüler. tooenable ek öznitelikler:

1. Merhaba üzerinde **olayları** dikey penceresinde tıklatın **sütunları**.

    ![Açık sütunları](./media/backup-azure-monitor-vms/audi-logs-column-button.png)

    Merhaba **sütunları seçin** dikey pencere açılır.

    ![Sütun dikey penceresi](./media/backup-azure-monitor-vms/columns-blade.png)
2. tooselect hello özniteliği, hello onay kutusuna tıklayın. Merhaba özniteliği onay kutusunu açar ve kapatır.
3. Tıklatın **sıfırlama** tooreset hello hello içinde öznitelik listesi **olayları** dikey. Ekleme veya öznitelikleri hello listesinden kaldırma sonrasında kullanın **sıfırlama** tooview hello yeni olay öznitelikler listesi.
4. Tıklatın **güncelleştirme** tooupdate hello verileri hello olay öznitelikleri. Aşağıdaki tablonun hello her özniteliği hakkında bilgi sağlar.

| Sütun adı | Açıklama |
| --- | --- |
| İşlem |Merhaba işlemin Hello adı |
| Düzey |Merhaba düzeyi hello işleyişini değerler olabilir: bilgi, uyarı, hata veya kritik |
| Durum |Açıklayıcı hello işlemi durumu |
| Kaynak |Merhaba kaynağı tanımlayan URL; olarak da bilinen hello kaynak kimliği |
| Zaman |Hello hello olay gerçekleştiği geçerli saati ölçülen zaman |
| Çağıran |Kim veya ne adlı veya hello olay tetiklenir; Merhaba sistem ya da bir kullanıcı olabilir |
| zaman damgası |Merhaba zaman zaman hello olay tetiklenir |
| Kaynak Grubu |Merhaba ilişkili kaynak grubu |
| Kaynak Türü |Kaynak Yöneticisi tarafından kullanılan hello iç kaynak türü |
| Abonelik Kimliği |Merhaba ilişkili abonelik kimliği |
| Kategori |Merhaba olay kategorisi |
| Bağıntı Kimliği |İlgili olayları ortak kimliği |

## <a name="use-powershell-toocustomize-alerts"></a>PowerShell toocustomize uyarıları kullanın
Merhaba Portalı'nda hello işleri için özel uyarı bildirimleri alabilirsiniz. Bu iş, tooget tanımlayın PowerShell tabanlı uyarı hello işletimsel kurallarında olayları günlüğe kaydeder. Kullanım *PowerShell sürüm 1.3.0 veya daha sonra*.

toodefine yedekleme hataları için özel bildirim tooalert hello komut aşağıdaki gibi bir komutu kullanın:

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.RecoveryServices/recoveryServicesVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/Microsoft.RecoveryServices/vaults/trinadhVault -Actions $actionEmail
```

**ResourceId** : hello ResourceId denetim günlüklerini elde edebilirsiniz. Merhaba ResourceId hello Kaynak sütununda hello işlem günlükleri, sağlanan bir URL'dir.

**OperationName** : OperationName hello biçiminde olan "Microsoft.RecoveryServices/recoveryServicesVault/*EventName*" nerede *EventName* olabilir:<br/>

* Kaydolma <br/>
* Kaydı Kaldır <br/>
* ConfigureProtection <br/>
* Backup <br/>
* Geri Yükleme <br/>
* StopProtection <br/>
* DeleteBackupData <br/>
* CreateProtectionPolicy <br/>
* DeleteProtectionPolicy <br/>
* UpdateProtectionPolicy <br/>

**Durum** : desteklenen değerler başlatıldı, başarılı veya başarısız oldu.

**Kaynak grubu** : Merhaba toowhich hello kaynağa ait kaynak grubu budur. Merhaba kaynak grubu sütununun oluşturulan toohello günlükleri ekleyebilirsiniz. Kaynak grubu hello kullanılabilir türler olay bilgilerinin biridir.

**Ad** : hello uyarı kuralı adı.

**CustomEmail** : hello özel e-posta adresi toowhich toosend bir uyarı bildirimine istediğiniz belirtin

**SendToServiceOwners** : Bu seçenek uyarı bildirimleri tooall yöneticileri ve ortak Yöneticiler hello aboneliğin gönderir. İçinde kullanılabilir **yeni AzureRmAlertRuleEmail** cmdlet'i

### <a name="limitations-on-alerts"></a>Uyarıları sınırlamalar
Olay tabanlı uyarılara sınırlamalar aşağıdaki konu toohello şunlardır:

1. Kurtarma Hizmetleri kasası hello tüm sanal makinelerde uyarıları tetiklenir. Sanal makineler bir kurtarma Hizmetleri kasasına alt kümeleri için hello uyarı özelleştiremezsiniz.
2. Bu özelliğin önizlemede değil. [Daha fazla bilgi](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. Uyarılar gönderilen "alerts-noreply@mail.windowsazure.com". Şu anda hello e-posta gönderen değiştiremezsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Olay günlükleri proje harika Sonrası-Değerlendirme etkinleştirmek ve hello yedekleme işlemleri için destek denetleyebilirsiniz. aşağıdaki işlemleri hello kaydedilir:

* Kaydolma
* Kaydı Kaldır
* Koruma yapılandırma
* Yedekleme (her ikisi de aynı zamanda talep üzerine yedekleme zamanlanmış)
* Geri Yükleme
* Korumayı Durdur
* Yedekleme verilerini sil
* İlke ekleme
* İlkeyi Sil
* Güncelleştirme ilkesi
* İşi iptal et

Azure Hizmetleri, olaylar, operations ve denetim günlüklerini hello arasında geniş kapsamlı bir açıklama için hello makaleye bakın [olayları görüntülemek ve Denetim günlükleri](../monitoring-and-diagnostics/insights-debugging-with-events.md).

Bir sanal makine bir kurtarma noktasından yeniden oluşturma hakkında daha fazla bilgi için kullanıma [geri Azure Vm'leri](backup-azure-restore-vms.md). Sanal makinelerinizi koruma bilgi gerekirse bkz [ilk bakış: geri kurtarma Hizmetleri kasası VM'ler tooa yukarı](backup-azure-vms-first-look-arm.md). Merhaba makalede, VM yedeklemeler için hello yönetim görevleri hakkında bilgi edinin [yönetmek Azure sanal makine yedeklerini](backup-azure-manage-vms.md).
