---
title: "Azure sanal makineleri Klasik dağıtılan tooa yedekleme kasası yukarı aaaBack | Microsoft Docs"
description: "Bul kaydetmek ve sanal makinelerinizi Azure sanal makine yedeklemesi için bu yordamları ile yedekleyin."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "sanal makine yedeklemesi; sanal makineyi geri; Yedekleme ve olağanüstü durum kurtarma; VM yedekleme"
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a>Azure sanal makineleri yedeklemek (Klasik portalı)
> [!div class="op_single_selector"]
> * [Sanal makineleri tooRecovery Hizmetleri kasasını yedekleyin](backup-azure-arm-vms.md)
> * [Sanal makineleri tooBackup kasasını yedekleyin](backup-azure-vms.md)
>
>

Bu makale, Klasik dağıtılan Azure sanal makine (VM) tooa yedekleme kasasını yedekleme için hello yordamlar sağlar. Bir Azure sanal makinesini yedeklenmeden önce tootake care, gereken bazı görevler vardır. Bunu, tam hello zaten yapmadıysanız [Önkoşullar](backup-azure-vms-prepare.md) tooprepare, VM'lerin yedeklenmesi için ortamınızı.

Ek bilgi için üzerinde hello makalelerine bakın [azure'da VM yedekleme altyapınızı planlama](backup-azure-vms-introduction.md) ve [Azure sanal makineleri](https://azure.microsoft.com/documentation/services/virtual-machines/).

> [!NOTE]
> Azure'da kaynak oluşturmaya ve kaynaklarla çalışmaya yönelik iki dağıtım modeli mevcuttur: [Resource Manager ve Klasik](../azure-resource-manager/resource-manager-deployment-model.md). Bir yedekleme kasası yalnızca klasik dağıtılan VM'ler koruyabilirsiniz. Resource Manager tarafından dağıtılan Vm'leri bir yedekleme kasası ile koruyamazsınız. Bkz: [VM'ler tooRecovery Hizmetleri kasasına yedekleme](backup-azure-arm-vms.md) kurtarma Hizmetleri ile çalışma hakkında ayrıntılar için kasaları.
>
>

Azure sanal makineleri yedekleme üç anahtar adımları içerir:

![Üç adımı tooback Azure Iaas sanal ayarlama](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> Sanal makineleri yedekleme işlemi, yerel bir işlemdir. Başka bir bölgede bir bölge tooa yedekleme kasasında sanal makineleri yedekleyin olamaz. Her Azure bölgesinde bir yedekleme kasası oluşturmanız gerekir böylece yedeklenecek VM'ler olduğu.
>
> [!IMPORTANT]
> Mart 2017'dan başlayarak, hello Klasik portal toocreate yedekleme kasaları artık kullanabilirsiniz.
> Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz. Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.<br/> 15 Ekim 2017 sonra PowerShell toocreate yedekleme kasaları kullanamazsınız. **1 Kasım 2017’ye kadar**:
>- Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.
>- Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır. Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.
>

## <a name="step-1---discover-azure-virtual-machines"></a>1. adım - Azure sanal makineleri Bul
Yeni sanal makineleri (VM'ler) eklenen toohello aboneliklere kaydetmeden önce tanımlanır tooensure hello bulma işlemini çalıştırın. Merhaba işlem sorgularında Azure hello ek bilgilerle birlikte hello Abonelikteki sanal makinelerin listesini hello bulut hizmeti adı ve hello bölge gibi.

1. İçinde toohello oturum [Klasik portal](http://manage.windowsazure.com/)
2. Azure Hizmetleri Hello listesinde tıklayın **kurtarma Hizmetleri** tooopen hello yedekleme ve Site kurtarma kasalarının listesi.
    ![Açık kasası listesi](./media/backup-azure-vms/choose-vault-list.png)
3. Yedekleme kasaları Hello listesinde hello kasa tooback VM yukarı seçin.

    Bu ise yeni bir kasa hello portalı toohello açılır **Hızlı Başlangıç** sayfası.

    ![Kayıtlı Öğeler menüsünü açın](./media/backup-azure-vms/vault-quick-start.png)

    Merhaba kasası önceden yapılandırılmışsa hello portalı en son kullanılan toohello menüsü açılır.
4. Merhaba kasa menüsünden (Merhaba sayfanın en üstündeki hello) tıklatın **kayıtlı öğeler**.

    ![Kayıtlı Öğeler menüsünü açın](./media/backup-azure-vms/vault-menu.png)
5. Merhaba gelen **türü** menüsünde, select **Azure sanal makine**.

    ![İş yükünü seçme](./media/backup-azure-vms/discovery-select-workload.png)
6. Tıklatın **bulma** hello sayfanın hello sonundaki.
    ![Bul düğmesi](./media/backup-azure-vms/discover-button-only.png)

    Merhaba sanal makinelerin tabloya alınması nedeniyle sırada hello bulma işlemi birkaç dakika sürebilir. Merhaba ekranın alt kısmındaki hello işleminin çalıştığını bilmeniz olanak sağlayan hello bir bildirim yoktur.

    ![VM'leri bulma](./media/backup-azure-vms/discovering-vms.png)

    Merhaba işlemi tamamlandığında hello bildirim değiştirir. Merhaba bulma işlemi hello sanal makineleri bulamadı, ilk hello VM'ler mevcut emin olun. Hello VM'ler yoksa, hello VM'ler olan içinde hello aynı olun bölge hello yedekleme kasası olarak. Merhaba, VM'ler var olduğundan ve aynı bölgede Merhaba, hello VM'ler değil zaten kayıtlı tooa yedekleme kasası olduğundan emin olun. Bir VM atanan tooa yedekleme kasası varsa şu atanan kullanılabilir toobe tooother yedekleme kasalarını değil.

    ![Bulma işlemi bitti](./media/backup-azure-vms/discovery-complete.png)

    Merhaba yeni öğeler bulunan sonra tooStep 2 gidin ve Vm'lerinizi kaydedin.

## <a name="step-2---register-azure-virtual-machines"></a>2. adım - kayıt Azure sanal makineler
Bir Azure sanal makinesi tooassociate kaydetmek hello Azure Backup hizmeti ile. Bu genellikle tek seferlik bir etkinliktir.

1. Toohello yedekleme kasasında gidin **kurtarma Hizmetleri** de Azure portal hello ve ardından **kayıtlı öğeler**.
2. Seçin **Azure sanal makine** hello açılan menüsünden.

    ![İş yükünü seçme](./media/backup-azure-vms/discovery-select-workload.png)
3. Tıklatın **KAYDETMEK** hello sayfanın hello sonundaki.
    ![Kaydet düğmesi](./media/backup-azure-vms/register-button-only.png)
4. Merhaba, **öğeleri Kaydet** kısayol menüsü, select hello sanal makineleri tooregister istiyor. İki veya daha fazla sanal makinelerle varsa aynı hello adı, aralarında hello bulut hizmeti toodistinguish kullanın.

   > [!TIP]
   > Birden çok sanal makine aynı anda kaydedilebilir.
   >
   >

    Seçtiğiniz her sanal makine için bir iş oluşturulur.
5. Tıklatın **işi görüntüle** hello bildirim toogo toohello içinde **işleri** sayfası.

    ![İşi kaydetme](./media/backup-azure-vms/register-create-job.png)

    Merhaba sanal makine hello hello kayıt işleminin hello durumu ile birlikte kayıtlı öğeler listesinde de görünür.

    ![Kayıt durumu 1](./media/backup-azure-vms/register-status01.png)

    Merhaba işlemi tamamlandığında hello tooreflect hello durumuna *kayıtlı* durumu.

    ![Kayıt durumu 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a>3. adım - Azure sanal makinelerini koruma
Şimdi hello sanal makine için bir yedekleme ve bekletme ilkesi ayarlayabilirsiniz. Tek bir kullanarak birden çok sanal makineler korunabilir eylem koruyun.

Mayıs 2015 ile birlikte gelir sonra oluşturulan azure yedekleme kasaları varsayılan bir ilke hello kasaya yerleşiktir. Bu varsayılan ilke, varsayılan saklama 30 gün ve bir kez günlük yedekleme zamanlaması ile birlikte gelir.

1. Toohello yedekleme kasasında gidin **kurtarma Hizmetleri** de Azure portal hello ve ardından **kayıtlı öğeler**.
2. Seçin **Azure sanal makine** hello açılan menüsünden.

    ![Portalda iş yükünü seçme](./media/backup-azure-vms/select-workload.png)
3. Tıklatın **koruma** hello sayfanın hello sonundaki.

    Merhaba **öğeleri koruma Sihirbazı'nı** görüntülenir. Merhaba sihirbaz yalnızca kayıtlı ve korumalı sanal makineleri listeler. Merhaba sanal makineleri tooprotect istediğinizi seçin.

    İki veya daha fazla sanal makinelerle varsa aynı hello adı, hello bulut hizmeti toodistinguish hello sanal makineler arasında kullanın.

   > [!TIP]
   > Bir seferde birden fazla sanal makineyi koruyabilir.
   >
   >

    ![Korumayı ölçekli olarak yapılandırma](./media/backup-azure-vms/protect-at-scale.png)

4. Seçin bir **yedekleme zamanlaması** tooback seçtiğiniz hello sanal makineleri ayarlama. Var olan ilkeleri kümesinden seçin veya yeni bir tane tanımlayın.

    Her bir yedekleme ilkesi, kendisiyle ilişkili birden çok sanal makineye sahip olabilir. Ancak, hello sanal makine yalnızca zamanında verilen herhangi bir noktada bir ilkesiyle ilişkili olabilir.

    ![Yeni ilke ile koruma](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > Bir yedekleme İlkesi hello zamanlanmış yedeklemeler için bir bekletme düzeni içerir. Mevcut bir yedekleme İlkesi seçerseniz, hello hello sonraki adımda bekletme seçeneklerini değiştiremezsiniz.
   >
   >

5. Seçin bir **bekletme aralığı** tooassociate hello yedeklemeleri ile.

    ![Esnek bekletme ile koruma](./media/backup-azure-vms/policy-retention.png)

    Bekletme İlkesi hello uzun bir yedeklemenin depolanacağı süreyi belirtir. Merhaba yedeklemenin ne zaman göre farklı bekletme ilkeleri belirtebilirsiniz. Örneğin, (işletimsel kurtarma noktası olarak hizmet veren) günlük mü bir yedekleme noktası 90 gün boyunca korunması. Buna karşılık, her üç aylık dönem (Denetim amacıyla) hello sonunda alınan bir yedekleme noktasının birçok ay veya yıl korunur toobe gerekebilir.

    ![Sanal makine, kurtarma noktası ile yedeklenir](./media/backup-azure-vms/long-term-retention.png)

    Bu örnek görüntüde:

   * **Günlük Bekletme İlkesi**: günlük alınan yedeklemeler 30 gün süreyle depolanır.
   * **Haftalık Bekletme İlkesi**: her hafta Pazar günü alınan yedeklemeler 104 hafta boyunca korunur.
   * **Aylık Bekletme İlkesi**: hello üzerinde her ayın son Pazar alınan yedeklemeler için 120 ayda korunur.
   * **Yıllık Bekletme İlkesi**: hello üzerinde her Ocak ilk Pazar alınan yedeklemeler için 99 yıla korunur.

     Bir iş tooconfigure hello koruma ilkesi oluşturulur ve seçtiğiniz her bir sanal makine için hello sanal makineleri toothat İlkesi ilişkilendirin.
6. tooview hello listesi **korumayı Yapılandır** hello kasa menüsünden işleri tıklatın **işleri** seçip **korumayı Yapılandır** hello gelen **işlemi**  filtre.

    ![Korumayı yapılandır işi](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a>İlk yedekleme
Merhaba sanal makine bir ilke ile korunuyor sonra hello altında görünür **korunan öğeler** hello durumunu sekmesiyle *korumalı - (ilk yedekleme bekleniyor)*. Varsayılan olarak, ilk zamanlanmış yedekleme hello hello olan *ilk yedekleme*.

koruma yapılandırma hemen sonra tootrigger hello ilk yedekleme:

1. Merhaba hello sonundaki **korunan öğeler** sayfasında, **Şimdi Yedekle**.

    Hello Azure Backup hizmeti hello ilk yedekleme işlemi için bir yedekleme işi oluşturur.
2. Hello tıklatın **işleri** sekmesini tooview hello işlerin listesi.

    ![Yedekleme devam ediyor](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> Merhaba yedekleme işlemi sırasında bir komut toohello yedekleme uzantısına tüm işleri yazma ve tutarlı bir anlık görüntüsünü her sanal makine tooflush hello Azure Backup hizmeti verir.
>
>

Merhaba ilk yedekleme tamamlandığında, hello hello hello sanal makinenin durumunu **korunan öğeler** sekmesi *korumalı*.

![Sanal makine, kurtarma noktası ile yedeklenir](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a>Yedekleme durumu ve ayrıntıları görüntüleme
Korumalı sonra hello hello sanal makine sayısı da artar. **Pano** Özet sayfası. Merhaba **Pano** sayfası hello son 24 olan saat işlerden hello sayısını da gösterir *başarılı*, sahip *başarısız*ve *devam eden*. Merhaba üzerinde **işleri** sayfasında, hello kullanın **durum**, **işlemi**, veya **gelen** ve **için** menüleri toofilter Merhaba işler.

![Pano sayfasındaki yedekleme durumu](./media/backup-azure-vms/dashboard-protectedvms.png)

Merhaba Pano değerleri her 24 saatte bir yenilenir.

## <a name="troubleshooting-errors"></a>Sorun giderme
Sanal makineniz yedekleme sırasında sorunları içine çalıştırırsanız hello Ara [VM sorun giderme makalesi](backup-azure-vms-troubleshoot.md) Yardım.

## <a name="next-steps"></a>Sonraki adımlar
* [Sanal makinelerinizi yönetme ve izleme](backup-azure-manage-vms.md)
* [Sanal makineleri geri yükleme](backup-azure-restore-vms.md)
