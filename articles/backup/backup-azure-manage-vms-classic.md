---
title: "aaaManage ve İzleyici Azure sanal makine yedeklerini | Microsoft Docs"
description: "Yedeklemeleri nasıl toomanage ve izleyici bir Azure sanal makine öğrenin"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a>Ortak Azure yedekleme işleri ve tetikleyici uyarıları hello Klasik portalda yönetin
> [!div class="op_single_selector"]
> * [Azure VM yedeklemeleri yönetme](backup-azure-manage-vms.md)
> * [Klasik VM yedeklemeleri yönetme](backup-azure-manage-vms-classic.md)
>
>

Bu makale ortak yönetim ve izleme görevlerini Azure'da korunan Klasik modeli sanal makineler için hakkında bilgi sağlar.  

> [!NOTE]
> Azure'da kaynak oluşturmaya ve kaynaklarla çalışmaya yönelik iki dağıtım modeli mevcuttur: [Resource Manager ve Klasik](../azure-resource-manager/resource-manager-deployment-model.md). Bkz: [Azure sanal makineleri yedeklemek, ortam tooback hazırlama](backup-azure-vms-prepare.md) Klasik dağıtımı ile çalışma hakkında ayrıntılar için model VM'ler.
>
> [!IMPORTANT]
>Mart 2017'dan başlayarak, hello Klasik portal toocreate yedekleme kasaları artık kullanabilirsiniz.
>
> Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz. Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.<br/> 15 Ekim 2017 sonra PowerShell toocreate yedekleme kasaları kullanamazsınız. **1 Kasım 2017’ye kadar**:
>- Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.
>- Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır. Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.

## <a name="manage-protected-virtual-machines"></a>Korumalı sanal makineleri yönetme
toomanage korunan sanal makineler:

1. tooview ve bir sanal makineye tıklayın için hello Yedekleme ayarlarını yönetmeyi **korunan öğeler** sekmesi.
2. Korumalı öğe toosee hello hello adını tıklatın **yedekleme ayrıntıları** sekmesinde hello son yedekleme hakkında bilgi gösterir.

    ![Sanal makine yedekleme](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. tooview ve bir sanal makineye tıklayın için hello yedekleme İlkesi ayarları yönetmek **ilkeleri** sekmesi.

    ![Sanal Makine ilkesi](./media/backup-azure-manage-vms/manage-policy-settings.png)

    Merhaba **yedekleme ilkeleri** sekmesinde varolan ilke hello gösterir. Gerektiği şekilde değiştirebilirsiniz. Toocreate yeni bir ilke gerekiyorsa tıklatın **oluşturma** hello üzerinde **ilkeleri** sayfası. Tooremove istiyorsanız, bir ilke, kendisiyle ilişkilendirilmiş herhangi bir sanal makine olmamalıdır olduğunu unutmayın.

    ![Sanal Makine ilkesi](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. Merhaba üzerinde bir sanal makine için Eylemler veya durumu hakkında daha fazla bilgi edinebilirsiniz **işleri** sayfası. Bir işi hello listesi tooget daha fazla ayrıntı veya filtre işleri belirli bir sanal makine için tıklayın.

    ![İşler](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a>Bir sanal makinenin talep üzerine yedekleme
Koruma için yapılandırıldıktan sonra isteğe bağlı bir sanal makine yedekleme devam edebilir. Merhaba ilk yedekleme bekleme durumundaysa hello sanal makine için talep üzerine yedekleme Azure yedekleme kasasında hello sanal makinenin tam bir kopyasını oluşturur. İlk yedekleme tamamlandığında, gönderme değişikliklerden önceki yedekleme tooAzure yedekleme yani kasa yalnızca talep üzerine yedekleme her zaman artımlıdır.

> [!NOTE]
> Bir talep üzerine yedekleme bekletme aralığını, yedekleme İlkesi karşılık gelen toohello VM içinde günlük bekletme için belirtilen tooretention değer ayarlanır.  
>
>

bir sanal makinenin yedeğini tootake isteğe bağlı:

1. Toohello gidin **korunan öğeler** sayfasından seçim yapıp **Azure sanal makine** olarak **türü** (henüz seçili değilse) ve tıklayın **seçin**düğmesi.

    ![VM türü](./media/backup-azure-manage-vms/vm-type.png)
2. Tootake isteğe bağlı yedekleme istediğiniz ve tıklayın Hello sanal makine seçin **şimdi yedek** hello altındaki hello sayfasının düğmesini.

    ![Şimdi Yedekle](./media/backup-azure-manage-vms/backup-now.png)

    Bu seçili hello sanal makineye bir yedekleme işi oluşturur. Bu iş oluşturulan kurtarma noktası bekletme aralığı hello sanal makineyle ilişkili hello İlkesi'nde belirtilen aynı olacaktır.

    ![Yedekleme işi oluşturma](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > içine hello sanal makinede aşağı ayrıntıya bir sanal makineyle ilişkili tooview hello İlkesi **korunan öğeler** sayfası ve Git toobackup ilke sekmesi.
   >
   >
3. Merhaba işi oluşturulduktan sonra tıklatabilirsiniz **işi görüntüle** hello bildirim toosee hello karşılık gelen iş hello işleri sayfasında çubuğu düğmesini.

    ![Yedekleme işi oluşturuldu](./media/backup-azure-manage-vms/created-job.png)
4. Merhaba iş başarıyla tamamlandıktan sonra bir kurtarma noktası kullanabileceğiniz oluşturulacak toorestore hello sanal makine. Bu ayrıca hello kurtarma noktası sütun değeri 1'tarafından artırır **korunan öğeler** sayfası.

## <a name="stop-protecting-virtual-machines"></a>Sanal makineleri koruma Durdur
Seçenekler aşağıdaki hello ile Merhaba gelecekteki bir sanal makine yedeklerini toostop seçebilirsiniz:

* Azure yedekleme kasasında sanal makineyle ilişkili yedekleme verilerini korur
* Sanal makine ile ilişkili yedekleme verilerini sil

Sanal makine ile ilişkili tooretain yedekleme verilerini seçtiyseniz, hello yedekleme verilerini toorestore hello sanal makine kullanabilirsiniz. Bu tür sanal makineler için ayrıntıları fiyatlandırma için tıklatın [burada](https://azure.microsoft.com/pricing/details/backup/).

bir sanal makine için korumayı tooStop:

1. Çok gidin**korunan öğeler** sayfasından seçim yapıp **Azure sanal makinesi** (henüz seçili değilse) hello filtre türü ve'ı tıklatın **seçin** düğmesi.

    ![VM türü](./media/backup-azure-manage-vms/vm-type.png)
2. Merhaba sanal makineyi seçin ve tıklayın **korumayı Durdur** hello sayfanın hello sonundaki.

    ![Korumayı Durdur](./media/backup-azure-manage-vms/stop-protection.png)
3. Varsayılan olarak, Azure Backup hello sanal makineyle ilişkili hello yedekleme verileri silmez.

    ![Durdurma onaylayın](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    Toodelete yedekleme verilerini istiyorsanız hello onay kutusunu seçin.

    ![Onay kutusu](./media/backup-azure-manage-vms/checkbox.png)

    Lütfen hello yedeklemeyi durdurma nedeni seçin. Bu isteğe bağlı olmakla birlikte, bir nedeni sağlama hello görüşler Azure Backup toowork yardımcı olmak ve hello müşteri senaryoları öncelik.
4. Tıklayın **gönderme** düğmesini toosubmit hello **korumayı** işi. Tıklayın **işi görüntüle** toosee hello karşılık gelen hello işinde **işleri** sayfası.

    ![Korumayı Durdur](./media/backup-azure-manage-vms/stop-protect-success.png)

    Değil seçtiyseniz **Delete ilişkilendirilmiş yedekleme verileri** sırasında seçeneği **korumayı Durdur** sihirbazını sonra post iş tamamlandığında, koruma durumu değişir çok**koruması durdurulmuş**. açıkça silinene kadar hello verileri Azure yedekleme ile kalır. Hello hello sanal makine seçerek hello verileri her zaman silebilir **korunan öğeler** sayfa ve tıklayarak **silmek**.

    ![Durdurulan koruma](./media/backup-azure-manage-vms/protection-stopped-status.png)

    Merhaba seçtiyseniz **Delete ilişkilendirilmiş yedekleme verileri** seçeneği, hello sanal makine hello parçası olmayacaktır **korunan öğeler** sayfası.

## <a name="re-protect-virtual-machine"></a>Sanal makine yeniden koruma
Merhaba seçmediyseniz **ilişkilendirme yedekleme verileri silmek** seçeneğini **korumayı Durdur**, hello sanal makine izleyerek yeniden Koruyabileceğiniz hello adımları benzer toobacking yukarı kayıtlı sanal makineler. Korumalı, bu sanal makine korunur yedek veri önceki toostop korumasına sahip olur ve sonra kurtarma noktaları oluşturulur sonra yeniden koruyun.

Yeniden koruma sonra hello sanal makinenin koruma durumu çok değiştirilecek**korumalı** varsa Kurtarma noktaları önceki çok**korumayı Durdur**.

  ![Korunmuş VM](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> Merhaba sanal makine yeniden korurken, başka bir ilke ile sanal makine başlangıçta korunan hello ilkesinden seçebilirsiniz.
>
>

## <a name="unregister-virtual-machines"></a>Sanal makineler kaydı
Merhaba yedekleme kasası tooremove hello sanal makineden istiyorsanız:

1. Tıklatın hello üzerinde **UNREGISTER** hello altındaki hello sayfasının düğmesini.

    ![Korumayı devre dışı bırakın](./media/backup-azure-manage-vms/unregister-button.png)

    Bir bildirim hello onaylamanızı isteyen hello ekranının altında görüntülenir. Tıklatın **Evet** toocontinue.

    ![Korumayı devre dışı bırakın](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a>Yedekleme verilerini sil
Ya da bir sanal makineyle ilişkili hello yedekleme verileri silebilirsiniz:

* Korumayı Durdur işini sırasında
* Bir sanal makinede durdurma sonra iş tamamlandı

hello olan bir sanal makine, yedekleme verilerini toodelete *koruması durdurulmuş* durumu başarılı şekilde tamamlandığını sonrası bir **durdurmak yedekleme** iş:

1. Toohello gidin **korunan öğeler** sayfasından seçim yapıp **Azure sanal makine** olarak *türü* hello tıklatıp **seçin** düğmesi.

    ![VM türü](./media/backup-azure-manage-vms/vm-type.png)
2. Merhaba sanal makineyi seçin. Merhaba sanal makine olacak **koruması durdurulmuş** durumu.

    ![Koruma durduruldu](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. Merhaba tıklatın **silmek** hello altındaki hello sayfasının düğmesini.

    ![Yedek Sil](./media/backup-azure-manage-vms/delete-backup.png)
4. Merhaba, **yedekleme verileri Sil** Sihirbazı'nı (önemle önerilir) yedekleme verilerini silmek için bir neden seçin ve tıklatın **gönderme**.

    ![Yedekleme verilerini sil](./media/backup-azure-manage-vms/delete-backup-data.png)
5. Bu, seçilen sanal makinenin iş toodelete yedekleme verilerini oluşturur. Tıklatın **işi görüntüle** toosee karşılık gelen iş işleri sayfasında.

    ![Veri silme başarılı](./media/backup-azure-manage-vms/delete-data-success.png)

    Merhaba iş tamamlandıktan sonra karşılık gelen toohello sanal makine kaldırılacak girişi hello **korunan öğeler** sayfası.

## <a name="dashboard"></a>Pano
Merhaba üzerinde **Pano** sayfa Azure sanal makineler, depolama ve hello son 24 saat ilişkili işleri hakkındaki bilgileri gözden geçirebilirsiniz. Yedekleme durumu ve ilişkili yedekleme hataları görüntüleyebilirsiniz.

![Pano](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> Merhaba Pano değerleri her 24 saatte bir yenilenir.
>
>

## <a name="auditing-operations"></a>Denetim işlemleri
Azure backup hello "tam olarak hangi yönetim işlemlerini hello yedekleme kasası üzerinde gerçekleştirilen kolay toosee kolaylaştırarak hello müşteri tarafından tetiklenen işlem günlüklerinin" yedekleme işlemleri incelenmesi sağlar. İşlem günlükleri proje harika Sonrası-Değerlendirme etkinleştirmek ve hello yedekleme işlemleri için destek denetleyebilirsiniz.

hello işlem aşağıdaki işlem günlüklerine kaydedilir:

* Kaydolma
* Kaydı Kaldır
* Koruma yapılandırma
* Yedekleme (Bu her ikisi de talep üzerine yedekleme BackupNow aracılığıyla yanı sıra zamanlanmış)
* Geri Yükleme
* Korumayı Durdur
* Yedekleme verilerini sil
* İlke ekleme
* İlkeyi Sil
* Güncelleştirme ilkesi
* İşi iptal et

tooview işlemi karşılık gelen tooa yedekleme kasası kaydeder:

1. Çok gidin**Yönetim Hizmetleri** Azure portalında ve hello ardından **işlem günlükleri** sekmesi.

    ![İşlem günlükleri](./media/backup-azure-manage-vms/ops-logs.png)
2. Merhaba filtreleri seçin **yedekleme** olarak *türü* ve hello yedekleme kasasının adını belirtin *hizmet adı* ve tıklayın **gönderme**.

    ![İşlem günlükleri filtresi](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. Merhaba işlem günlükleri, herhangi bir işlem seçin ve tıklatın **ayrıntıları** toosee ayrıntıları karşılık gelen tooan işlemi.

    ![İşlem günlükleri getirme ayrıntıları](./media/backup-azure-manage-vms/ops-logs-details.png)

    Merhaba **ayrıntıları Sihirbazı** hello işlemi tetiklenen, iş kimliği, üzerinde bu işlemi tetiklenir ve hello işlem başlatışınızda kaynak hakkında bilgi içerir.

    ![İşlem ayrıntıları](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a>Uyarı bildirimleri
Portalda hello işleri için özel uyarı bildirimleri alabilirsiniz. Bu işlem günlüklerini olaylarına PowerShell'i dayalı olarak uyarı kuralları tanımlayarak sağlanır. Kullanmanızı öneririz *PowerShell sürüm 1.3.0 veya yukarıdaki*.

toodefine özel bildirim tooalert yedekleme hataları için bir örnek komut gibi görünür:

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

**ResourceId**: Bu işlem günlükleri açılır penceresinden bölümde açıklandığı gibi alabilirsiniz. ResourceUri bir işlemin ayrıntıları açılan penceresinde hello ResourceId toobe Bu cmdlet için sağlanan ' dir.

**OperationName**: Bu hello biçimi olacaktır "Microsoft.Backup/backupvault/<EventName>" EventName kayıt, Unregister, ConfigureProtection, yedekleme, geri yükleme, StopProtection, DeleteBackupData, biri olduğu CreateProtectionPolicy, DeleteProtectionPolicy, UpdateProtectionPolicy

**Durum**: değerlerini olduğunuz-başlatıldı, desteklenen başarılı ve başarısız oldu.

**Kaynak grubu**: ResourceGroup hello kaynağın işlemi başlatıldı. Bu ResourceId değeri elde edebilirsiniz. Alanlar arasında değer */resourceGroups/* ve */providers/* içinde ResourceId değeri hello ResourceGroup değeridir.

**Ad**: hello uyarı kuralı adı.

**CustomEmail**: hello özel e-posta adresi toowhich toosend uyarı bildirimi istediğiniz belirtin

**SendToServiceOwners**: Bu seçenek uyarı bildirimi tooall yöneticileri ve ortak Yöneticiler hello aboneliğin gönderir. İçinde kullanılabilir **yeni AzureRmAlertRuleEmail** cmdlet'i

### <a name="limitations-on-alerts"></a>Uyarıları sınırlamalar
Olay tabanlı uyarılara tabi toohello aşağıdaki sınırlamalar vardır:

1. Tüm sanal makinelerde hello yedekleme kasasında uyarıları tetiklenir. Sanal makineler bir yedekleme kasasına belirli kümesi için tooget uyarıları özelleştiremezsiniz.
2. Bu özelliğin önizlemede değil. [Daha fazla bilgi](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. Gelen uyarılar alırsınız "alerts-noreply@mail.windowsazure.com". Şu anda hello e-posta gönderen değiştiremezsiniz.

## <a name="next-steps"></a>Sonraki adımlar
* [Azure sanal makineleri geri yükleme](backup-azure-restore-vms.md)
