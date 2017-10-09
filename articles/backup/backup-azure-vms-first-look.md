---
title: "İlk Bakış: Azure sanal makinelerini bir yedekleme kasasıyla yedekleme | Microsoft Belgeleri"
description: "Azure VM'ler tooa yedekleme kasası yukarı Hello Klasik portal tooback kullanın. Bu öğretici hello yedekleme kasası oluşturma, hello Vm'leri kaydetme, yedekleme ilkesi oluşturma ve hello ilk yedekleme işini çalıştırma dahil olmak üzere tüm aşamalar açıklanmaktadır."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: 77700e69eab9faccbc7ef923e1eb4e1f97be75d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a>İlk bakış: Azure sanal makinelerini yedekleme
> [!div class="op_single_selector"]
> * [VM'leri bir kurtarma hizmetleri kasasıyla koruma](backup-azure-vms-first-look-arm.md)
> * [Azure VM'lerini yedekleme kasasıyla koruma](backup-azure-vms-first-look.md)
>
>

Bu öğretici bir Azure sanal makine (VM) tooa yedekleme kasasına Azure yedekleme için hello adımlarını gösterir. Bu makalede hello Klasik modeli veya VM'lerin yedeklenmesi için Service Manager dağıtım modeli açıklanır. Merhaba aşağıdaki adımlar yalnızca hello Klasik portalında oluşturulan tooBackup kasalarını geçerlidir. Microsoft, yeni dağıtımlar için hello Resource Manager modelini kullanarak önerir.

Tooa kaynak grubuna ait bir VM tooa kurtarma Hizmetleri kasasına yedekleme ilgilendiğiniz olup [ilk bakış: koruma Vm'leri bir kurtarma Hizmetleri kasası ile](backup-azure-vms-first-look-arm.md).

toosuccessfully tamamlamak hello aşağıdaki öğreticide, şu önkoşulların bulunması gerekir:

* Azure aboneliğinizde bir VM oluşturmuş olmanız gerekir.
* Merhaba VM bağlantı tooAzure genel IP adresleri vardır. Ek bilgi için bkz. [Ağ bağlantısı](backup-azure-vms-prepare.md#network-connectivity).


> [!NOTE]
> Azure'da kaynak oluşturmaya ve kaynaklarla çalışmaya yönelik iki dağıtım modeli mevcuttur: [Resource Manager ve Klasik](../azure-resource-manager/resource-manager-deployment-model.md). Bu öğretici için hello Klasik Portalı'nda oluşturulan sanal makineleri ile kullanılır.
>
>

## <a name="create-a-backup-vault"></a>Yedekleme kasası oluşturma
Bir yedekleme kasası tüm hello yedeklemeleri ve zaman içinde oluşturulan kurtarma noktalarını depolayan bir varlıktır. Merhaba yedekleme kasası, yedeklenmekte olan uygulanan toohello sanal makineleri hello yedekleme ilkeleri de içerir.

> [!IMPORTANT]
> Mart 2017'dan başlayarak, hello Klasik portal toocreate yedekleme kasaları artık kullanabilirsiniz.
> Yedekleme kasalarını tooRecovery Hizmetleri kasaları yükseltebilirsiniz. Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.<br/> 15 Ekim 2017 sonra PowerShell toocreate yedekleme kasaları kullanamazsınız. **1 Kasım 2017’ye kadar**:
>- Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.
>- Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır. Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.
>

## <a name="discover-and-register-azure-virtual-machines"></a>Azure sanal makinelerini bulma ve kaydetme
Merhaba VM'yi bir kasaya kaydetmeden önce yeni Vm'leri hello bulma işlemi tooidentify çalıştırın. Bu hello bulut hizmeti adı ve hello bölge gibi ek bilgilerle birlikte hello Abonelikteki sanal makinelerin listesini döndürür.

1. İçinde toohello oturum [Klasik Azure portalı](http://manage.windowsazure.com/)
2. Hello Klasik Azure portalı, tıklatın **kurtarma Hizmetleri** tooopen hello kurtarma Hizmetleri kasalarının listesi.
    ![İş yükünü seçme](./media/backup-azure-vms-first-look/recovery-services-icon.png)
3. Kasa Hello listeden hello kasa tooback VM yukarı seçin.

    Kasanızı seçtiğinizde hello açılır **Hızlı Başlangıç** sayfası
4. Merhaba kasa menüsünden tıklatın **kayıtlı öğeler**.

    ![İş yükünü seçme](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. Merhaba gelen **türü** menüsünde, select **Azure sanal makine**.

    ![İş yükünü seçme](./media/backup-azure-vms/discovery-select-workload.png)
6. Tıklatın **bulma** hello sayfanın hello sonundaki.
    ![Bul düğmesi](./media/backup-azure-vms/discover-button-only.png)

    Merhaba sanal makinelerin tabloya alınması nedeniyle sırada hello bulma işlemi birkaç dakika sürebilir. Merhaba ekranın alt kısmındaki hello işleminin çalıştığını bilmeniz olanak sağlayan hello bir bildirim yoktur.

    ![VM'leri bulma](./media/backup-azure-vms/discovering-vms.png)

    Merhaba işlemi tamamlandığında hello bildirim değiştirir.

    ![Bulma işlemi bitti](./media/backup-azure-vms-first-look/discovery-complete.png)
7. Tıklatın **KAYDETMEK** hello sayfanın hello sonundaki.
    ![Kaydet düğmesi](./media/backup-azure-vms-first-look/register-icon.png)
8. Merhaba, **öğeleri Kaydet** kısayol menüsü, select hello sanal makineleri tooregister istiyor.

   > [!TIP]
   > Birden çok sanal makine aynı anda kaydedilebilir.
   >
   >

    Seçtiğiniz her sanal makine için bir iş oluşturulur.
9. Tıklatın **işi görüntüle** hello bildirim toogo toohello içinde **işleri** sayfası.

    ![İşi kaydetme](./media/backup-azure-vms/register-create-job.png)

    Merhaba sanal makine hello hello kayıt işleminin hello durumu ile birlikte kayıtlı öğeler listesinde de görünür.

    ![Kayıt durumu 1](./media/backup-azure-vms/register-status01.png)

    Merhaba işlemi tamamlandığında hello tooreflect hello durumuna *kayıtlı* durumu.

    ![Kayıt durumu 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Merhaba VM Aracısı hello sanal makineye yükleme
Hello Azure VM Aracısı hello hello yedekleme uzantısını toowork Azure sanal makinesine yüklenmesi gerekir. VM hello Azure galerisinde oluşturduysanız hello VM Aracısı VM hello üzerinde zaten; çok atlayabilirsiniz[Vm'lerinizi koruma](backup-azure-vms-first-look.md#create-the-backup-policy).

VM'NİZİN bir şirket içi merkezinden geçişi sağlandıysa hello VM VM aracısının yüklü hello büyük olasılıkla yok. Devam etmeden tooprotect hello VM önce hello sanal makinedeki hello VM aracısı yüklemeniz gerekir. VM Aracısı yükleme konusunda ayrıntılı adımlar hello hello bakın [hello Vm'leri yedekleme makalesinin VM Aracısı bölümü](backup-azure-vms-prepare.md#vm-agent).

## <a name="create-hello-backup-policy"></a>Merhaba yedekleme ilkesi oluşturma
Merhaba ilk yedekleme işini tetiklemeden önce yedekleme anlık görüntülerinin alınma hello zamanlamasını ayarlayın. Yedekleme anlık görüntülerinin alınır ve bu anlık görüntülerin süre hello hello zamanla korunur, yedekleme İlkesi hello'dır. Merhaba bekletme bilgileri, üst öğe son rotasyon düzenini temel alır.

1. Toohello yedekleme kasasında gidin **kurtarma Hizmetleri** hello Klasik Azure portalı ve tıklatın **kayıtlı öğeler**.
2. Seçin **Azure sanal makine** hello açılan menüsünden.

    ![Portalda iş yükünü seçme](./media/backup-azure-vms/select-workload.png)
3. Tıklatın **koruma** hello sayfanın hello sonundaki.
    ![Koru'ya tıklama](./media/backup-azure-vms-first-look/protect-icon.png)

    Merhaba **öğeleri koruma Sihirbazı'nı** görünür ve listeler *yalnızca* kayıtlı ve korumalı sanal makineler.

    ![Korumayı ölçekli olarak yapılandırma](./media/backup-azure-vms/protect-at-scale.png)
4. Merhaba sanal makineleri tooprotect istediğinizi seçin.

    Merhaba iki veya daha fazla sanal makinelerle varsa aynı adı, kullanım hello bulut hizmeti toodistinguish hello sanal makineler arasında.
5. Merhaba üzerinde **korumasını yapılandırma** menü mevcut bir ilkeyi seçin veya yeni bir ilke tooprotect tanımladığınız hello sanal makineler oluşturun.

    Yeni yedekleme kasaları hello kasayla ilişkili bir varsayılan ilke içerir. Bu ilke her Akşam günlük bir anlık alır ve hello günlük anlık görüntü 30 gün süreyle tutulur. Her bir yedekleme ilkesi, kendisiyle ilişkili birden çok sanal makineye sahip olabilir. Ancak, hello sanal makine yalnızca aynı anda bir ilkeyle ilişkili olabilir.

    ![Yeni ilke ile koruma](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > Bir yedekleme İlkesi hello zamanlanmış yedeklemeler için bir bekletme düzeni içerir. Mevcut bir yedekleme İlkesi seçerseniz, hello sonraki adımda oluşturulamıyor toomodify hello bekletme seçenekleri olacaktır.
   >
   >
6. Üzerinde **bekletme aralığı** tanımlamak hello hello belirli yedekleme noktaları için günlük, haftalık, aylık ve yıllık kapsam.

    ![Sanal makine, kurtarma noktası ile yedeklenir](./media/backup-azure-vms/long-term-retention.png)

    Bekletme İlkesi hello uzun bir yedeklemenin depolanacağı süreyi belirtir. Merhaba yedeklemenin ne zaman göre farklı bekletme ilkeleri belirtebilirsiniz.
7. Tıklatın **işleri** tooview hello listesi **korumayı Yapılandır** işler.

    ![Korumayı yapılandır işi](./media/backup-azure-vms/protect-configureprotection.png)

    Merhaba ilkeyi belirlediğinize göre toohello sonraki adıma gidin ve hello ilk yedeklemeyi çalıştırın.

## <a name="initial-backup"></a>İlk yedekleme
Bir sanal makineye sahip bir ilke korunduktan sonra bu ilişkiyi hello üzerinde görüntüleyebilirsiniz **korunan öğeler** sekmesi. Merhaba ilk yedekleme, hello gerçekleşene kadar **koruma durumu** olarak gösterir **korumalı - (ilk yedekleme bekleniyor)**. Varsayılan olarak, ilk zamanlanmış yedekleme hello hello olan *ilk yedekleme*.

![Yedekleme beklemede](./media/backup-azure-vms-first-look/protection-pending-border.png)

toostart hello ilk yedeklemeyi şimdi:

1. Merhaba üzerinde **korunan öğeler** sayfasında, **Şimdi Yedekle** hello sayfanın hello sonundaki.
    ![Şimdi Yedekle simgesi](./media/backup-azure-vms-first-look/backup-now-icon.png)

    Hello Azure Backup hizmeti hello ilk yedekleme işlemi için bir yedekleme işi oluşturur.
2. Hello tıklatın **işleri** sekmesini tooview hello işlerin listesi.

    ![Yedekleme devam ediyor](./media/backup-azure-vms-first-look/protect-inprogress.png)

    İlk yedekleme tamamlandığında, hello hello hello sanal makinenin durumunu **korunan öğeler** sekmesi *korumalı*.

    ![Sanal makine, kurtarma noktası ile yedeklenir](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > Sanal makineleri yedekleme işlemi, yerel bir işlemdir. Sanal makineleri başka bir bölgede bir bölge tooa yedekleme Kasası'ndan yedekleyemezsiniz. Bu nedenle, yedeklenen toobe gereken VM'lerin bulunduğu her Azure bölgesi için bu bölgede en az bir yedekleme kasası oluşturulmalıdır.
   >
   >

## <a name="next-steps"></a>Sonraki adımlar
Bir VM'yi başarıyla yedeklediğinize göre, sonraki birkaç adım ilginizi çekebilir. Merhaba en mantıklı toofamiliarize kendiniz veri tooa VM geri yükleme ile bir adımdır. Ancak, anlamanıza yardımcı olacak yönetim görevleri vardır nasıl tookeep verilerinizi güvenli ve maliyetleri en aza indirin.

* [Sanal makinelerinizi yönetme ve izleme](backup-azure-manage-vms.md)
* [Sanal makineleri geri yükleme](backup-azure-restore-vms.md)
* [Sorun giderme rehberi](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a>Sorularınız mı var?
Sorularınız varsa veya herhangi bir özellik varsa dahil, toosee istediğiniz [Geri bildirimlerinizi bize gönderin](http://aka.ms/azurebackup_feedback).
