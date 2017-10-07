---
title: "aaaManage Resource Manager tarafından dağıtılan sanal makine yedeklerini | Microsoft Docs"
description: "Bilgi nasıl toomanage ve İzleyici Resource Manager tarafından dağıtılan sanal makine yedekleme"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a>Azure sanal makine yedeklemelerini yönetme
> [!div class="op_single_selector"]
> * [Azure VM yedeklemeleri yönetme](backup-azure-manage-vms.md)
> * [Klasik VM yedeklemeleri yönetme](backup-azure-manage-vms-classic.md)
>
>

Bu makalede VM yedekleri yönetmeyle ilgili yönergeler sağlar ve hello yedekleme uyarıları bilgi hello portal panosunda kullanılabilir açıklar. Bu makalede Hello yönerge toousing Vm'leri kurtarma Hizmetleri kasaları ile geçerlidir. Bu makalede hello sanal makinelerin oluşturulmasını kapsamaz ya da onu açıklayan nasıl tooprotect sanal makineler. Azure Resource Manager tarafından dağıtılan Vm'leri Azure kurtarma Hizmetleri kasası ile koruma öncü için bkz: [ilk bakış: geri kurtarma Hizmetleri kasası VM'ler tooa yukarı](backup-azure-vms-first-look-arm.md).

## <a name="manage-vaults-and-protected-virtual-machines"></a>Kasa ve korumalı sanal makineleri yönetme
Hello Azure portal, kasa hello dahil olmak üzere ilgili erişim tooinformation hello kurtarma Hizmetleri kasa Panosu sağlar:

* Ayrıca hello en son geri yükleme noktası olan yedekleme anlık görüntüsü, hello en son < br\>
* Yedekleme İlkesi merhaba < br\>
* tüm yedekleme anlık görüntülerinin boyutunu toplam < br\>
* Merhaba kasası ile korunan sanal makineler sayısı < br\>

Bir sanal makine yedekleme ile çok sayıda yönetim görevi hello kasası hello panosunda açma ile başlar. Ancak, birden çok öğe (veya birden çok VM) hakkında belirli bir VM, tooview ayrıntıları açmak kullanılan tooprotect kasalarını olabileceğinden hello kasa öğesi Panosu. Merhaba aşağıdaki yordamda nasıl gösterilmektedir tooopen hello *kasa Panosu* ve toohello devam *kasa öğesi Panosu*. Nasıl tooadd kasası hello öğesi toohello kasa çıkışı Azure Pano hello PIN toodashboard komutunu kullanarak noktası ve her iki yordamı "ipuçları" yoktur. PIN toodashboard öğe veya kısayol toohello kasa oluşturma yoludur. Ayrıca, sık kullanılan komutlar hello kısayoldan yürütebilir.

> [!TIP]
> Birden çok panolar varsa ve dikey pencere açılır hello Koyu mavi kaydırıcı hello penceresi tooslide hello geri ve İleri Azure Pano hello altındaki kullanın.
>
>

![Kaydırıcı ile tam görünümü](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a>Kurtarma Hizmetleri kasası hello panosunda açın:
1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Merhaba Hub menüsünde **Gözat** ve kaynakları hello listesinde yazın **kurtarma Hizmetleri**. Yazmaya başladığınızda liste filtreleri, girişinize göre hello. **Kurtarma Hizmetleri kasası** seçeneğine tıklayın.

    ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    Merhaba kurtarma Hizmetleri kasalarının listesi görüntülenir.

    ![Liste kurtarma Hizmetleri kasaları ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > Kasa toohello Azure Pano sabitlerseniz hello Azure portal'ı açtığınızda, kasa hemen erişilebilir. toopin hello kasa listesinde, bir kasa toohello Panosu hello kasası sağ tıklatın ve seçin **PIN toodashboard**.
   >
   >
3. Kasa Hello listeden hello kasa tooopen kendi Pano seçin. Merhaba kasası, hello kasa panosunu ve hello seçtiğinizde **ayarları** dikey penceresini açın. Görüntü aşağıdaki hello hello **Contoso kasa** Pano vurgulanır.

    ![Kasa panosunu ve ayarlar dikey penceresi açın](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a>Kasa öğesi panosunu açın
Merhaba önceki yordamda hello kasa panosu açılır. tooopen hello kasa öğesi Panosu:

1. Merhaba üzerinde hello kasa panosunda **yedekleme öğeleri** döşeme, tıklatın **Azure sanal makineleri**.

    ![Yedekleme öğeleri Aç döşeme](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    Merhaba **yedekleme öğeleri** dikey penceresinde hello son yedekleme işi her öğe için listelenir. Bu örnekte, bir bu kasası tarafından korunan sanal makinenin, demovm-markgal yoktur.  

    ![Yedekleme öğeleri döşeme](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > Erişim Kolaylığı için bir kasa öğesi toohello Azure Pano sabitleyebilirsiniz. toopin hello kasası öğe listesi, sağ hello öğesini seçip bir kasa öğesi **PIN toodashboard**.
   >
   >
2. Merhaba, **yedekleme öğeleri** dikey penceresinde hello öğesi tooopen hello kasası öğesi panosunu'ı tıklatın.

    ![Yedekleme öğeleri döşeme](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    Merhaba kasası öğesi panosunu ve kendi **ayarları** dikey penceresini açın.

    ![Ayarlar dikey penceresi ile yedekleme öğeleri Panosu](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    Merhaba kasası öğe panodan gibi birçok önemli yönetim görevleri gerçekleştirebilirsiniz:

   * ilkeleri değiştirebilir veya yeni bir yedekleme ilkesi oluşturabilirsiniz < br\>
   * geri yükleme noktaları görüntülemek ve tutarlılık durumlarına bakın < br\>
   * İsteğe bağlı bir sanal makinenin yedeğini < br\>
   * sanal makineler korunmasını durdurmayı < br\>
   * bir sanal makine korumayı sürdürmek < br\>
   * Yedekleme verilerini (veya kurtarma noktası) silme < br\>
   * [Yedekleme diskleri geri](backup-azure-arm-restore-vms.md#restore-backed-up-disks) < br\>

Yordamları izleyerek hello için başlangıç noktası hello hello kasası öğesi panosunu ' dir.

## <a name="manage-backup-policies"></a>Yedekleme ilkelerini yönetme
1. Merhaba üzerinde [kasa öğesi Panosu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), tıklatın **tüm ayarları** tooopen hello **ayarları** dikey.

    ![Yedekleme İlkesi dikey penceresi](./media/backup-azure-manage-vms/all-settings-button.png)
2. Merhaba üzerinde **ayarları** dikey penceresinde tıklatın **yedekleme İlkesi** tooopen o dikey.

    Merhaba dikey penceresinde hello yedekleme sıklığı ve bekletme aralığı ayrıntıları gösterilmiştir.

    ![Yedekleme İlkesi dikey penceresi](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. Merhaba gelen **yedekleme ilkesi seçin** menüsü:

   * toochange ilkeleri, başka bir ilke seçin ve tıklatın **kaydetmek**. Merhaba yeni ilke hemen uygulanan toohello kasası olur. < br\>
   * toocreate bir ilke seçin **Yeni Oluştur**.

     ![Sanal makine yedekleme](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     Bir yedekleme ilkesi oluşturma ile ilgili yönergeler için bkz: [yedekleme ilkesi tanımlama](backup-azure-manage-vms.md#defining-a-backup-policy).

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> Yedekleme ilkelerini yönetirken emin toofollow hello olun [en iyi uygulamalar](backup-azure-vms-introduction.md#best-practices) en iyi yedekleme performansı
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a>Bir sanal makinenin talep üzerine yedekleme
Koruma için yapılandırıldıktan sonra isteğe bağlı bir sanal makine yedekleme devam edebilir. Merhaba ilk yedekleme bekleme durumundaysa, talep üzerine yedekleme kurtarma Hizmetleri kasası hello hello sanal makinenin tam bir kopyasını oluşturur. Merhaba ilk yedekleme tamamlandığında, bir talep üzerine yedekleme değişiklikleri hello önceki anlık görüntüden, toohello kurtarma Hizmetleri kasası yalnızca gönderin. Diğer bir deyişle, sonraki yedeklemeleri her zaman artımlı.

> [!NOTE]
> bir talep üzerine yedekleme için Hello bekletme aralığı hello günlük yedekleme noktası hello İlkesi'nde belirtilen hello bekletme değerdir. Hiçbir günlük yedekleme noktası seçtiyseniz hello haftalık yedekleme noktası kullanılır.
>
>

bir sanal makinenin yedeğini tootrigger isteğe bağlı:

* Merhaba üzerinde [kasa öğesi Panosu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), tıklatın **Şimdi Yedekle**.

    ![Yedekleme şimdi düğmesi](./media/backup-azure-manage-vms/backup-now-button.png)

    Merhaba portal toostart talep üzerine yedekleme işi istediğiniz emin olur. Tıklatın **Evet** toostart hello yedekleme işi.

    ![Yedekleme şimdi düğmesi](./media/backup-azure-manage-vms/backup-now-check.png)

    Merhaba yedekleme işi, bir kurtarma noktası oluşturur. Merhaba bekletme aralığı hello kurtarma noktası olan hello hello sanal makineyle ilişkili hello İlkesi'nde belirtilen bekletme aralığı ile aynı. tootrack hello ilerleme hello kasa panosunda, hello işi için tıklatın hello **yedekleme işlerini** döşeme.  

## <a name="stop-protecting-virtual-machines"></a>Sanal makineleri koruma Durdur
Bir sanal makine koruma toostop seçerseniz, tooretain hello kurtarma noktaları isteyip istemediğinizi istenir. Toostop koruma sanal makineleri iki yolu vardır:

* sonraki tüm yedekleme işleri durdurun ve tüm kurtarma noktalarını silin veya
* sonraki tüm yedekleme işleri durdurmak, ancak kurtarma noktaları hello bırakın <br/>

Depolama birimindeki kurtarma noktaları hello bırakarak ile ilişkili bir maliyeti yoktur. Ancak, Kurtarma noktaları hello bırakarak hello yararı hello sanal makineyi daha sonra geri isterseniz olur. Kurtarma noktaları hello bırakarak hakkında bilgi için hello maliyeti, hello bkz [fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/backup/). Tüm kurtarma noktalarının toodelete seçerseniz, hello sanal makine geri yükleyemezsiniz.

bir sanal makine için korumayı toostop:

1. Merhaba üzerinde [kasa öğesi Panosu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), tıklatın **Dur yedekleme**.

    ![Yedek düğmesini Durdur](./media/backup-azure-manage-vms/stop-backup-button.png)

    Merhaba Durdur yedekleme dikey pencere açılır.

    ![Yedekleme dikey penceresini Durdur](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. Merhaba üzerinde **durdurmak yedekleme** dikey penceresinde tooretain ya da delete yedekleme verilerini hello olup olmadığını seçin. Merhaba bilgileri kutusunda seçiminizi hakkında ayrıntılar sağlar.

    ![Korumayı Durdur](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. Tooretain hello yedekleme verilerini seçerseniz, toostep 4 atlayın. Toodelete yedekleme verilerini seçerseniz, toostop hello yedekleme işleri istediğiniz ve hello kurtarma noktaları - hello öğesinin tür hello adı silme onaylayın.

    ![Doğrulama Durdur](./media/backup-azure-manage-vms/item-verification-box.png)

    Merhaba öğesinin adını emin değilseniz, hello ünlem işareti tooview hello adın üzerine gelin. Ayrıca, hello hello öğesi altında adıdır **durdurmak yedekleme** hello dikey penceresinde hello üstünde.
4. İsteğe bağlı olarak sağlayan bir **neden** veya **açıklama**.
5. Merhaba geçerli öğenin toostop hello yedekleme işini tıklatın ![Dur yedekleme düğmesi](./media/backup-azure-manage-vms/stop-backup-button-blue.png)

    Bir bildirim iletisi, hello yedekleme işleri durduruldu bilmenizi sağlar.

    ![Durdurma onaylayın](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a>Bir sanal makine korumayı Sürdür
Merhaba, **yedekleme verileri koru** seçeneği seçildi hello sanal makine için korumayı durduğunda olası tooresume koruma olur. Merhaba, **yedekleme verilerini Sil** seçeneği seçildi, ardından hello sanal makine için koruma devam edemiyor.

Merhaba sanal makine için tooresume koruma

1. Merhaba üzerinde [kasa öğesi Panosu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), tıklatın **yedeklemeyi Sürdür**.

    ![Korumayı Sürdür](./media/backup-azure-manage-vms/resume-backup-button.png)

    Merhaba yedekleme İlkesi dikey penceresi açılır.

   > [!NOTE]
   > Merhaba sanal makine yeniden korurken, başka bir ilke ile sanal makine başlangıçta korunan hello ilkesinden seçebilirsiniz.
   >
   >
2. Merhaba adımları [yedekleme ilkelerini yönetme](backup-azure-manage-vms.md#manage-backup-policies) tooassign hello İlkesi hello sanal makine için.

    Merhaba yedekleme ilkesi uygulanan toohello sanal makine eklendiğinde, iletiden hello bakın.

    ![Başarıyla korumalı VM](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a>Yedekleme verilerini sil
Başlangıç sırasında sanal makine ile ilişkili hello yedekleme verileri silebilirsiniz **Dur yedekleme** işi, veya hello sonra yedekleme işi tamamlandı zaman. Faydalı toowait gün veya hafta hello kurtarma noktaları silmeden önce bile olabilir. Kurtarma noktaları, yedek verileri silerken geri farklı olarak, belirli bir kurtarma noktaları toodelete seçemezsiniz. Yedek verilerinizin toodelete seçerseniz, hello öğeyle ilişkili tüm kurtarma noktalarını silin.

Merhaba aşağıdaki yordamı hello yedekleme işi hello sanal makinenin durdurulmuş veya devre dışı varsayar. Merhaba yedekleme işini devre dışı bırakıldığında hello **yedeklemeyi Sürdür** ve **Delete yedekleme** hello kasası öğesi panosunda seçenekleri mevcuttur.

![Devam ettirme ve silme düğmeleri](./media/backup-azure-manage-vms/resume-delete-buttons.png)

Merhaba sahip bir sanal makine yedekleme verileri toodelete *yedekleme devre dışı*:

1. Merhaba üzerinde [kasa öğesi Panosu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), tıklatın **Delete yedekleme**.

    ![VM türü](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    Merhaba **yedekleme verilerini Sil** dikey pencere açılır.

    ![VM türü](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. Tür hello adı hello öğesi tooconfirm toodelete hello kurtarma noktaları istiyor.

    ![Doğrulama Durdur](./media/backup-azure-manage-vms/item-verification-box.png)

    Merhaba öğesinin adını emin değilseniz, hello ünlem işareti tooview hello adın üzerine gelin. Ayrıca, hello hello öğesi altında adıdır **yedekleme verilerini Sil** hello dikey penceresinde hello üstünde.
3. İsteğe bağlı olarak sağlayan bir **neden** veya **açıklama**.
4. hello geçerli öğe için toodelete hello yedekleme verileri tıklatın ![Dur yedekleme düğmesi](./media/backup-azure-manage-vms/delete-button.png)

    Bir bildirim iletisi, hello yedekleme verileri silinir bilmenizi sağlar.

## <a name="next-steps"></a>Sonraki adımlar
Bir sanal makine bir kurtarma noktasından yeniden oluşturma hakkında daha fazla bilgi için kullanıma [geri Azure Vm'leri](backup-azure-restore-vms.md). Sanal makinelerinizi koruma bilgi gerekirse bkz [ilk bakış: geri kurtarma Hizmetleri kasası VM'ler tooa yukarı](backup-azure-vms-first-look-arm.md). Olayları izleme hakkında daha fazla bilgi için bkz: [izlemek için Azure sanal makine yedeklerini uyarıları](backup-azure-monitor-vms.md).
