---
title: "İlk Bakış: Azure sanal makinelerini kurtarma hizmetleri kasasıyla koruma | Microsoft Docs"
description: "Sanal makineleri bir kurtarma hizmetleri kasasıyla koruyun. Resource Manager tarafından dağıtılan VM'ler, Klasik dağıtılan VM'lerin ve Premium Storage Vm'lerini, şifrelenmiş VM'ler, yönetilen diskleri tooprotect Vm'lerinde yedeklerini verilerinizi kullanın. Bir kurtarma hizmetleri kasası oluşturun ve kaydedin. Azure'da VM'leri kaydedin, ilke oluşturun ve VM'leri koruyun."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keyword: backups; vm backup
ms.assetid: 45e773d6-c91f-4501-8876-ae57db517cd1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/15/2017
ms.author: markgal;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70e4700abb76e16e32e1ead06ce1dbe277e1f0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-toorecovery-services-vaults"></a>Azure sanal makineleri tooRecovery Hizmetleri kasalarının yedekleyin
> [!div class="op_single_selector"]
> * [VM'leri bir kurtarma hizmetleri kasasıyla koruma](backup-azure-vms-first-look-arm.md)
> * [VM'leri yedekleme kasasıyla koruma](backup-azure-vms-first-look.md)
>
>

Bu öğretici bir kurtarma Hizmetleri kasası oluşturma ve bir Azure sanal makinesini (VM) yedeklemeye hello adımlarını gösterir. Kurtarma hizmetleri kasaları şunları korur:

* Azure Resource Manager tarafından dağıtılan VM'ler
* Klasik VM'ler
* Standart depolama VM'leri
* Premium depolama VM'leri
* Yönetilen Diskler üzerinde çalışan sanal makineler
* Azure Disk Şifrelemesi kullanılarak BEK ve KEK ile şifrelenmiş VM’ler
* Windows sanal makinelerinin VSS, Linux sanal makinelerinin özel anlık görüntü öncesi ve anlık görüntü sonrası betikler kullanılarak uygulamada tutarlı yedeklenmesi

Premium depolama Vm'lerini koruma ile ilgili daha fazla bilgi için hello makalesine bakın [ve Premium Storage Vm'lerini geri yükleme](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup). Yönetilen disk sanal makinelerine yönelik destek hakkında daha fazla bilgi için bkz. [Yönetilen diskler üzerindeki sanal makineleri yedekleme ve geri yükleme](backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup). Linux VM yedekleme için ön ve son betik çerçevesi hakkında daha fazla bilgi için bkz. [Ön betik ve son betik kullanarak uygulamayla tutarlı Linux VM yedekleme] (https://docs.microsoft.com/tr-tr/azure/backup/backup-azure-linux-app-consistent).

daha hakkında yedekleme yapabilirsiniz ve ne yapamazsınız toofind başvuran [burada](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)

> [!NOTE]
> Bu öğretici, Azure aboneliğinizde zaten bir VM olan ve ölçüleri tooallow hello yedekleme hizmeti tooaccess hello VM önlemlerin varsayar.
>
>

[!INCLUDE [learn-about-Azure-Backup-deployment-models](../../includes/backup-deployment-models.md)]

Tooprotect istediğiniz sanal makineleri Hello sayısına bağlı olarak, farklı başlangıç noktalarından başlayabilirsiniz. Toohello kurtarma Hizmetleri kasası tooback tek bir işlemde birden çok sanal makine yedeklemek istiyorsanız gidin ve [hello kasa Panosu yedekleme işinden başlatma hello](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-recovery-services-vault). Tooback tek bir sanal makine yedeklemek istiyorsanız VM yönetim dikey penceresinden hello yedekleme işi başlatabilirsiniz.

## <a name="configure-hello-backup-job-from-hello-vm-management-blade"></a>Merhaba yedekleme işi hello VM yönetim dikey penceresinden yapılandırın

Merhaba sanal makine yönetim dikey penceresinde hello Azure portal adımları tooconfigure hello yedekleme işi yükseltmesinin hello kullanın. Bu adımları toohello sanal makineleri hello Klasik Portalı'ndaki geçerli değildir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Merhaba Hub menüsünde **daha Hizmetleri** ve hello filtre iletişim kutusuna **sanal makineleri**. Siz yazarken, kaynakların hello listesini filtreler. Sanal makineler seçeneğini gördüğünüzde seçin.

  ![Hub menüsünde daha Hizmetleri tooopen metin iletişim tıklayın ve sanal makineleri yazın](./media/backup-azure-vms-first-look-arm/open-vm-from-hub.png)

  sanal makineler (VM) hello Abonelikteki Hello listesi görüntülenir.

  ![sanal makineleri hello Abonelikteki Hello listesi görüntülenir.](./media/backup-azure-vms-first-look-arm/list-of-vms.png)

3. Merhaba listeden VM tooback seçin.

  ![sanal makineleri hello Abonelikteki Hello listesi görüntülenir.](./media/backup-azure-vms-first-look-arm/list-of-vms-selected.png)

  Merhaba VM seçtiğinizde, hello sanal makinelerin listesini toohello sola ve hello sanal makine yönetim dikey ve hello sanal makine Pano kaydırır, açın. </br>
 ![VM Yönetimi dikey penceresi](./media/backup-azure-vms-first-look-arm/vm-management-blade.png)

4. Merhaba, hello VM yönetim dikey **ayarları** 'yi tıklatın **yedekleme**. </br>

  ![VM yönetim dikey penceresindeki yedekle seçeneği](./media/backup-azure-vms-first-look-arm/backup-option-vm-management-blade.png)

  Merhaba etkinleştir yedekleme dikey pencere açılır.

  ![VM yönetim dikey penceresindeki yedekle seçeneği](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

5. Merhaba kurtarma Hizmetleri kasası için tıklatın **Varolanı seç** ve hello kasası hello aşağı açılan listeden seçin.

  ![Yedekleme Sihirbazını Etkinleştirme](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

  Kurtarma Hizmetleri kasalarının vardır veya toouse yeni bir kasa isterseniz tıklayın **Yeni Oluştur** hello ad hello yeni kasa belirtin. Yeni bir kasa aynı hello oluşturulan kaynak grubunu ve hello sanal makine olarak aynı konumu. Toocreate farklı değerleri olan bir kurtarma Hizmetleri kasası istiyorsanız hello bölüm hakkında çok bakın[bir kurtarma Hizmetleri kasası oluşturma](backup-azure-vms-first-look-arm.md#create-a-recovery-services-vault-for-a-vm).

6. Merhaba yedekleme İlkesi tooview hello ayrıntılarını tıklatın **yedekleme İlkesi**.

  Merhaba **yedekleme İlkesi** dikey penceresi açılır ve seçili hello İlkesi hello ayrıntılarını sağlar. Diğer ilkeler varsa hello açılır menü toochoose farklı bir yedekleme İlkesi kullanın. Bir ilke toocreate istiyorsanız seçin **Yeni Oluştur** hello açılan menüsünden. Bir yedekleme ilkesi tanımlamaya yönelik yönergeler için bkz. [Yedekleme ilkesi tanımlama](backup-azure-vms-first-look-arm.md#defining-a-backup-policy). toosave hello değişiklikleri toohello yedekleme İlkesi ve dönüş toohello etkinleştir yedekleme dikey penceresinde'ı **Tamam**.

  ![Yedekleme ilkesini seçme](./media/backup-azure-vms-first-look-arm/setting-rs-backup-policy-new-2.png)

7. Merhaba etkinleştir yedekleme dikey penceresinde **yedeklemeyi etkinleştir** toodeploy hello ilkesi. Hello İlkesi dağıtma bunu hello kasası ve hello sanal makineler ile ilişkilendirir.

  ![Yedeklemeyi Etkinleştir düğmesi](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-button.png)

8. Merhaba yapılandırma hello Portalı'nda görünen hello bildirimleri ilerlemeyi izleyebilirsiniz. Aşağıdaki örnek hello dağıtım başlatıldığını gösterir.

  ![Yedeklemeyi Etkinleştirme bildirimi](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-notification.png)

9. Merhaba VM yönetim dikey penceresinde Hello yapılandırma ilerleme durumu tamamlandığında tıklatın **yedekleme** tooopen hello yedekleme öğesi dikey ve görünüm hello ayrıntıları.

  ![VM Yedekleme Öğesi Görünümü](./media/backup-azure-vms-first-look-arm/backup-item-view.png)

  Merhaba ilk yedekleme tamamlanana kadar **durumu'son yedekleme** olarak gösterir **uyarı (ilk yedekleme bekleme)**. Merhaba sonraki yedekleme işi zamanlandığı toosee oluşur, altında **yedekleme İlkesi** hello İlkesi hello adına tıklayın. Merhaba yedekleme İlkesi dikey penceresi açılır ve hello zamanlanmış yedekleme hello süresini gösterir.

10. toorun bir yedekleme işi ve hello ilk kurtarma noktası oluşturma, dikey penceresinde hello üzerinde yedekleme kasası **Şimdi Yedekle**.

  ![Yedekleme şimdi toorun hello ilk yedekleme tıklayın](./media/backup-azure-vms-first-look-arm/backup-now.png)

  Merhaba Şimdi Yedekle dikey pencere açılır.

  ![Merhaba Şimdi Yedekle dikey gösterir](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

11. Merhaba Şimdi Yedekle dikey penceresinde hello takvim simgesini tıklatın, hello Takvim denetimi tooselect hello bu kurtarma noktası korunur ve tıklatın son günü kullanın **yedekleme**.

  ![set hello son gün hello Şimdi Yedekle kurtarma noktası korunur](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Dağıtım bildirimleri hello yedekleme işi tetiklenir ve hello işinin ilerleme durumunu hello hello yedekleme işleri sayfasında izleyebilirsiniz size bildirmek.

## <a name="configure-hello-backup-job-from-hello-recovery-services-vault"></a>Kurtarma Hizmetleri kasası hello yedekleme işinden Hello yapılandırın
tooconfigure hello yedekleme işi, hello aşağıdaki adımları tamamlayın.  

1. Bir sanal makine için Kurtarma Hizmetleri kasası oluşturun.
2. Kullanım hello Azure portal tooselect bir senaryo, bir yedekleme İlkesi ayarlamak ve öğeleri tooprotect tanımlayın.
3. Merhaba ilk yedeklemeyi çalıştırın.

## <a name="create-a-recovery-services-vault-for-a-vm"></a>Bir VM için kurtarma hizmetleri kasası oluşturma
Kurtarma Hizmetleri kasası tüm hello yedeklemeleri ve zaman içinde oluşturulan kurtarma noktalarını depolayan bir varlıktır. Merhaba kurtarma Hizmetleri kasası ayrıca hello yedekleme İlkesi uygulanmış içeren toohello korumalı VM'ler.

> [!NOTE]
> VM'leri yedekleme işlemi, yerel bir işlemdir. Başka bir konumda tek bir konumda tooa kurtarma Hizmetleri Kasası'ndan Vm'lerini yedekleyemezsiniz. Bu nedenle, VM'ler toobe yedeklenmekte olan her Azure konumu için en az bir kurtarma Hizmetleri kasası ilgili konumda mevcut olmalıdır.
>
>

Kurtarma Hizmetleri kasası toocreate:

1. Zaten yapmadıysanız, toohello içinde oturum [Azure portal](https://portal.azure.com/) Azure aboneliğinizi kullanarak.
2. Merhaba Hub menüsünde **daha fazla hizmet** ve hello filtre iletişim türü **kurtarma Hizmetleri**. Siz yazarken, kaynakların hello listesini filtreler. Kurtarma Hizmetleri kasalarının hello listesinde görüntülendiğinde,'ı tıklatın.

    ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Merhaba abonelikte kurtarma Hizmetleri kasalarının varsa hello kasalarını listelenir.

    ![Kurtarma Hizmetleri Kasası oluşturma 2. adım](./media/backup-azure-vms-first-look-arm/list-of-rs-vault.png)
3. Merhaba üzerinde **kurtarma Hizmetleri kasaları** menüsünde tıklatın **Ekle**.

    ![Kurtarma Hizmetleri Kasası oluşturma 2. adım](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    Merhaba kurtarma Hizmetleri kasası dikey penceresi açılır tooprovide isteyen bir **adı**, **abonelik**, **kaynak grubu**, ve **konumu**.

    ![Kurtarma Hizmetleri Kasası Oluşturma 3. adım](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. İçin **adı**, bir kolay ad tooidentify hello kasası girin. Merhaba adı toobe hello Azure aboneliği için benzersiz olmalıdır. 2 ila 50 karakterden oluşan bir ad yazın. Ad bir harf ile başlamalıdır ve yalnızca harf, rakam ve kısa çizgi içerebilir.

5. Merhaba, **abonelik** bölümünde, hello açılır menü toochoose hello Azure aboneliği kullanın. Yalnızca bir abonelik kullanırsanız, bu abonelik görünür ve toohello sonraki adımı atlayabilirsiniz. Hangi abonelik toouse emin değilseniz, hello varsayılan kullanın (veya önerilen) aboneliği. Yalnızca kuruluş hesabınızın birden çok Azure aboneliği ile ilişkili olması durumunda birden çok seçenek olur.

6. Merhaba, **kaynak grubu** bölümü:

    * seçin **Yeni Oluştur** toocreate bir kaynak grubu istiyorsanız.
    Veya
    * seçin **var olanı kullan** ve hello açılır menü toosee hello kullanılabilir kaynak gruplarının listesini'ı tıklatın.

  Kaynak grupları hakkında tam bilgi için bkz: Merhaba [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).

7. Tıklatın **konumu** tooselect hello hello kasa için coğrafi bölgeyi. Bu seçim, yedekleme verilerinizi burada gönderilen hello coğrafi bölgeyi belirler.

  > [!IMPORTANT]
  > VM bulunduğu hello konumunu emin değilseniz, hello kasa oluşturma iletişim kutusunu kapatmak ve sanal makinelerin listesini toohello hello portalında gidin. Birden çok bölgede sanal makineniz varsa her bölgede bir Kurtarma Hizmetleri kasası oluşturun. Merhaba kasası toohello sonraki konuma geçmeden önce hello ilk konumda oluşturun. Gerek toospecify hello depolama hesabı toostore hello yedekleme verileri--hello kurtarma Hizmetleri kasası kullanılan yoktur ve hello Azure Backup hizmeti hello depolama otomatik olarak işler.
  >

8. Merhaba kurtarma Hizmetleri kasası dikey penceresinde Hello altındaki tıklatın **oluşturma**.

    Oluşturulan toobe kurtarma Hizmetleri kasası hello için birkaç dakika sürebilir. Merhaba portal hello üst sağ bölmesinde Hello durum bildirimlerini izleyin. Kasanız oluşturulduktan sonra hello kurtarma Hizmetleri kasaları listesinde görünür. Birkaç dakika sonra kasayı görmezseniz **Yenile**’ye tıklayın.

    ![Yenile düğmesine tıklayın](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    Kasanızı kurtarma Hizmetleri kasalarının hello listesinde gördüğünüz verdikten sonra hazır tooset hello depolama artıklığı demektir.

Kasanızı oluşturduğunuza göre nasıl tooset hello depolama çoğaltma öğrenin.

### <a name="set-storage-replication"></a>Depolama Çoğaltmayı Ayarlama
Merhaba depolama çoğaltma seçeneği, coğrafi olarak yedekli depolama ve yerel olarak yedekli depolama arasında toochoose sağlar. Varsayılan olarak, kasanız coğrafi olarak yedekli depolamaya sahiptir. Kurtarma Hizmetleri kasası Merhaba, birincil yedeklemenizse hello depolama çoğaltma seçeneği kümesi toogeo yedekli depolama bırakın. Daha düşük dayanıklılık düzeyinde olan daha uygun maliyetli bir seçenek istiyorsanız yerel olarak yedekli depolamayı seçin. Daha fazla bilgi edinin [coğrafi olarak yedekli](../storage/common/storage-redundancy.md#geo-redundant-storage) ve [yerel olarak yedekli](../storage/common/storage-redundancy.md#locally-redundant-storage) hello Depolama Seçenekleri [Azure Storage Çoğaltmaya genel bakış](../storage/common/storage-redundancy.md).

tooedit hello depolama çoğaltma ayarı:

1. Merhaba gelen **kurtarma Hizmetleri kasaları** dikey penceresinde, select hello yeni Kasa.

  ![Kurtarma Hizmetleri kasası hello listeden Hello yeni kasa seçin](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

  Merhaba kasası seçtiğinizde, ayarlar dikey penceresinde hello (*hello üstünde hello Kasası'nın adı olan*) ve hello kasa Ayrıntılar dikey penceresini açın.

  ![Yeni kasa için Görünüm hello depolama yapılandırması](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. Merhaba yeni kasasının ayarlar dikey penceresinde hello dikey slayt tooscroll toohello Yönet bölümüne aşağı kullanın ve'ı tıklatın **Yedekleme Altyapısı**.
    Merhaba yedekleme altyapısı dikey pencere açılır.
3. Merhaba yedekleme altyapısı dikey penceresinde tıklayın **yedekleme yapılandırması** tooopen hello **yedekleme yapılandırması** dikey.

    ![Yeni kasa Hello depolama yapılandırmasını ayarlayın](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. Kasanız için Hello uygun depolama çoğaltma seçeneğini seçin.

    ![depolama yapılandırması seçenekleri](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    Varsayılan olarak, kasanız coğrafi olarak yedekli depolamaya sahiptir. Azure birincil yedekleme alanı uç noktası kullanıyorsanız, toouse devam **coğrafi olarak yedekli**. Birincil yedekleme alanı uç noktası Azure kullanmıyorsanız, ardından **yerel olarak yedekli**, hello Azure depolama maliyetlerini azaltır. [Coğrafi olarak yedekli](../storage/common/storage-redundancy.md#geo-redundant-storage) ve [yerel olarak yedekli](../storage/common/storage-redundancy.md#locally-redundant-storage) depolama seçenekleri hakkında daha fazla bilgiyi [Depolama yedekliliğine genel bakış](../storage/common/storage-redundancy.md) bölümünden edinebilirsiniz.


## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>Yedekleme hedefi seçme, ilke ayarlamak ve öğeleri tooprotect tanımlayın
Bir VM'yi bir kasaya kaydetmeden önce toohello abonelik eklenen yeni sanal makineler tanımlanır hello bulma işlemi tooensure çalıştırın. Merhaba işlem sorgularında Azure hello ek bilgilerle birlikte hello Abonelikteki sanal makinelerin listesini hello bulut hizmeti adı ve hello bölge gibi. Hello Azure portal, senaryo tooput hello kurtarma Hizmetleri kasasına giden toowhat ifade eder. Kurtarma noktalarının ne sıklıkta ve ne zaman alınır hello zamanlamasını ilkesidir. İlke hello bekletme aralığı hello kurtarma noktaları için de içerir.

1. Bir kurtarma Hizmetleri kasası açmak zaten varsa, toostep 2 devam edin. Aksi takdirde hello Hub menüsünde **daha fazla hizmet** ve kaynakları hello listesinde yazın **kurtarma Hizmetleri** tıklatıp **kurtarma Hizmetleri kasaları**.

    ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Kurtarma Hizmetleri kasaları Hello listesi görüntülenir.

    ![Liste Görünümü hello kurtarma Hizmetleri kasaları](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    Kurtarma Hizmetleri kasaları Hello listesinden bir kasa tooopen kendi Pano seçin.

     ![Kasa dikey penceresini açma](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. Merhaba kasa Panosu menüsünden tıklatın **yedekleme** tooopen hello yedekleme dikey penceresinde.

    ![Yedekleme dikey penceresini açma](./media/backup-azure-arm-vms-prepare/backup-button.png)

    Merhaba yedekleme ve yedekleme hedefi dikey pencere açılır.

    ![Senaryo dikey penceresini açma](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)
3. Merhaba gelen hello yedekleme hedefi dikey **, iş yükünü çalıştırdığı** açılır menüsünde, Azure'ı seçin. Merhaba gelen **neler toobackup istediğiniz** açılır, sanal makine seçin ve ardından **Tamam**.

    Bu eylemler hello VM uzantısı hello kasaya yeniden kaydedin. Merhaba yedekleme hedefi dikey penceresi kapanır ve hello **yedekleme İlkesi** dikey pencere açılır.

    ![Senaryo dikey penceresini açma](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)

4. Merhaba yedekleme İlkesi dikey penceresinde, tooapply toohello kasası hello yedekleme ilkesini seçin.

    ![Yedekleme ilkesini seçme](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    Merhaba varsayılan ilke Hello ayrıntılarını hello açılan menüsünün altında listelenir. Bir ilke toocreate istiyorsanız seçin **Yeni Oluştur** hello açılan menüsünden. Bir yedekleme ilkesi tanımlamaya yönelik yönergeler için bkz. [Yedekleme ilkesi tanımlama](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).
    Tıklatın **Tamam** tooassociate hello yedekleme İlkesi hello kasası ile.

    Yedekleme İlkesi dikey penceresi kapanır ve hello hello **sanal makine Seç** dikey pencere açılır.
5. Merhaba, **sanal makine Seç** dikey penceresinde hello sanal makineleri tooassociate hello ile ilke belirtilen tıklatın seçip **Tamam**.

    ![İş yükünü seçme](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    Seçili hello sanal makine doğrulanır. Merhaba sanal görmüyorsanız hello kurtarma Hizmetleri kasası olarak toosee, bunlar mevcut onay beklenen makineler aynı Azure konumuna hello. Kurtarma Hizmetleri kasası hello Hello konumu hello kasa panosunda görüntülenir.

6. Merhaba yedekleme dikey penceresinde hello kasa için tüm ayarların tanımladığınız, tıklatın **yedeklemeyi etkinleştir** toodeploy hello İlkesi toohello kasası ve VM'lerin hello. Merhaba yedekleme İlkesi dağıtma hello hello sanal makine için ilk kurtarma noktası oluşturmaz.

    ![Yedeklemeyi Etkinleştirme](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Başarılı bir şekilde hello yedekleme etkinleştirdikten sonra yedekleme ilkenizi zamanlamaya göre çalıştırır. Ancak, tooinitiate hello ilk yedekleme işini devam edin.

## <a name="initial-backup"></a>İlk yedekleme
Bir yedekleme İlkesi hello sanal anlamına gelmez makinesinde dağıtıldığında hello veri yedeklendi. Varsayılan olarak, ilk zamanlanmış yedekleme hello (Merhaba yedekleme ilkesinde tanımlandığı gibi) hello ilk yedeklemedir. Merhaba ilk yedekleme gerçekleşene kadar son yedekleme durumu hello üzerinde hello **yedekleme işleri** dikey gösterildiğinden **uyarı (ilk yedekleme bekleme)**.

![Yedekleme beklemede](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

İlk yedeklemeniz son olmadığı sürece toobegin yakında önerilir, çalıştırmanız **Şimdi Yedekle**.

toorun hello ilk yedekleme işini:

1. Merhaba kasa Panosu üzerinde hello numarasını altında tıklatın **yedekleme öğeleri**, veya hello **yedekleme öğeleri** döşeme. <br/>
  ![Ayarlar simgesi](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)

  Merhaba **yedekleme öğeleri** dikey pencere açılır.

  ![Öğeleri yedekleme](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. Merhaba üzerinde **yedekleme öğeleri** dikey penceresinde, select hello öğesi.

  ![Ayarlar simgesi](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  Merhaba **yedekleme öğeleri** listesi açılır. <br/>

  ![Tetiklenmiş yedekleme işi](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. Merhaba üzerinde **yedekleme öğeleri** listesinde, hello üç noktaya tıklayın **...**  tooopen hello bağlam menüsü.

  ![Bağlam menüsü](./media/backup-azure-vms-first-look-arm/context-menu.png)

  Merhaba bağlam menüsü görüntülenir.

  ![Bağlam menüsü](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. Merhaba bağlam menüsünde **Şimdi Yedekle**.

  ![Bağlam menüsü](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  Merhaba Şimdi Yedekle dikey pencere açılır.

  ![Merhaba Şimdi Yedekle dikey gösterir](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. Merhaba Şimdi Yedekle dikey penceresinde hello takvim simgesini tıklatın, hello Takvim denetimi tooselect hello bu kurtarma noktası korunur ve tıklatın son günü kullanın **yedekleme**.

  ![set hello son gün hello Şimdi Yedekle kurtarma noktası korunur](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Dağıtım bildirimleri hello yedekleme işi tetiklenir ve hello işinin ilerleme durumunu hello hello yedekleme işleri sayfasında izleyebilirsiniz size bildirmek. VM Hello boyutuna bağlı olarak, hello ilk yedek oluşturulması biraz zaman alabilir.

6. Merhaba üzerinde hello kasa Panosu üzerinde hello ilk yedekleme tooview veya iz hello durumunu **yedekleme işleri** döşeme tıklatın **devam eden**.

  ![Yedekleme İşleri kutucuğu](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  Merhaba yedekleme işleri dikey penceresi açılır.

  ![Yedekleme İşleri kutucuğu](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  Merhaba, **yedekleme işleri** dikey penceresinde hello tüm işlerin durumunu görebilirsiniz. Merhaba, VM için yedekleme işi devam ediyor veya sona erdi kontrol edin. Bir yedekleme işi tamamlandığında, hello durumudur *tamamlandı*.

  > [!NOTE]
  > Merhaba Yedekleme işleminin bir parçası olarak bir komut toohello yedekleme uzantısına tüm yazar ve tutarlı bir anlık görüntüsünü her VM tooflush hello Azure Backup hizmeti verir.
  >
  >


[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Merhaba VM Aracısı hello sanal makineye yükleme
Bu bilgiler, gerekmesi halinde kullanılabilmesi için sağlanmıştır. Hello Azure VM Aracısı hello hello yedekleme uzantısını toowork Azure sanal makinesine yüklenmesi gerekir. VM hello Azure galerisinde oluşturduysanız, ancak ardından hello VM Aracısı hello sanal makineye zaten. Şirket içi veri merkezlerinden değil hello VM aracısı yüklü olmaz geçirilir VM'ler. Böyle bir durumda hello VM aracısı yüklü toobe gerekir. Azure VM hello konusunda sorun yaşarsanız Azure VM Aracısı hello onay doğru hello sanal makinede yüklü (aşağıdaki tablonun hello bakın). Özel bir VM oluşturuyorsanız [hello olun **yükleme hello VM Aracısı** onay kutusunun seçili](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) hello sanal makine sağlanmadan önce.

Merhaba hakkında bilgi edinin [VM Aracısı](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) ve [nasıl tooinstall onu](../virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Aşağıdaki tablonun hello için hello VM Aracısı Windows ve Linux VM'ler hakkında ek bilgi sağlar.

| **İşlem** | **Windows** | **Linux** |
| --- | --- | --- |
| Merhaba VM Aracısı yükleme |<li>Merhaba yükleyip [aracı MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Yönetici ayrıcalıkları toocomplete hello yüklemesi gerekir. <li>[Merhaba VM özelliğini güncelleştirin](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) Aracısı hello tooindicate yüklenir. |<li> Merhaba son yükleme [Linux Aracısı](https://github.com/Azure/WALinuxAgent) github'dan. Yönetici ayrıcalıkları toocomplete hello yüklemesi gerekir. <li> [Merhaba VM özelliğini güncelleştirin](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) Aracısı hello tooindicate yüklenir. |
| Merhaba VM Aracısı güncelleştiriliyor |Güncelleştirme hello VM aracısı yeniden yüklemeyi hello kadar basit [VM Aracısı ikili dosyalarının](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br>Merhaba VM Aracısı güncelleştirilirken herhangi bir yedekleme işleminin çalıştığından emin olun. |Merhaba yönergelerini izleyin [güncelleştirme hello Linux VM Aracısı](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). <br>VM Aracısı güncelleştirilmiş hello sırasında herhangi bir yedekleme işleminin çalıştığından emin olun. |
| Merhaba VM Aracısı yüklemesini doğrulama |<li>Toohello gidin *C:\WindowsAzure\Packages* hello Azure VM klasöründe. <li>Mevcut hello WaAppAgent.exe dosyasını bulmanız gerekir.<li> Merhaba dosyaya sağ tıklayın, çok Git**özellikleri**seçip hello **ayrıntıları** sekmesini hello ürün sürümü alanı 2.6.1198.718 olmalıdır ya da daha yüksek. |Yok |

### <a name="backup-extension"></a>Backup uzantısı
VM Aracısı hello sanal makinede, hello Azure Backup hizmeti yüklü hello bir kez hello yedekleme uzantısını toohello VM aracısı yükler. Hello Azure Backup hizmeti sorunsuz bir şekilde yükseltilir ve ek kullanıcı müdahalesi olmadan hello yedekleme uzantısını düzeltme ekleri.

Hello VM çalışmıyor olsa bile hello Backup hizmeti yedekleme uzantısını Merhaba, yükler. Çalışan bir VM, uygulamayla tutarlı bir kurtarma noktası hello alınma olasılığını en yükseğe. Ancak, hello Azure Backup hizmeti kapalı ve hello uzantısı yüklenmemiş olsa bile hello VM yukarı tooback devam eder. Bu yedekleme türünü çevrimdışı VM adı verilir ve hello kurtarma noktası *kilitlenmeyle tutarlı*.

## <a name="troubleshooting-information"></a>Sorun giderme bilgileri
Bu makalede hello görevlerden bazılarını yerine getirirken sorun yaşıyorsanız, başvurun [sorun giderme kılavuzluğu](backup-azure-vms-troubleshoot.md).

## <a name="pricing"></a>Fiyatlandırma
Azure VM'lerin yedeklenmesi hello maliyetini korumalı örnekler hello sayısına dayalı olarak. Korumalı bir örneğin tanımı için, bkz: [Korumalı örnek nedir](backup-introduction-to-azure-backup.md#what-is-a-protected-instance). Bir sanal makine yedekleme hello maliyetini hesaplama ilişkin bir örnek için bkz: [nasıl korumalı örnekler hesaplanır](backup-azure-vms-introduction.md#calculating-the-cost-of-protected-instances). Hello Azure yedekleme fiyatlandırması bkz hakkında bilgi için sayfa [yedekleme fiyatlandırma](https://azure.microsoft.com/pricing/details/backup/).

## <a name="questions"></a>Sorularınız mı var?
Sorularınız varsa veya herhangi bir özellik varsa dahil, toosee istediğiniz [Geri bildirimlerinizi bize gönderin](http://aka.ms/azurebackup_feedback).
