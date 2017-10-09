---
title: "Azure Backup kullanarak VM'ler şifrelenmiş aaaBackup ve geri yükleme"
description: "Bu makalede hello yedekleme hakkında konuşur ve geri yükleme deneyimi VM'ler için Azure Disk şifrelemesi kullanılarak şifrelenmiş."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 8387f186-7d7b-400a-8fc3-88a85403ea63
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/27/2017
ms.author: pajosh;markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c19ef6f58e3259949535dab32a55aaf7a8c658fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-encrypted-virtual-machines-with-azure-backup"></a>Sanal makineler Azure yedekleme ile nasıl tooback yedeklemek ve geri yükleme şifreli
Bu makalede adımları toobackup ve geri yükleme Azure Backup kullanarak sanal makineleri hakkında alınmaktadır. Ayrıca hata durumları için desteklenen senaryolar, ön koşullar ve sorun giderme adımları hakkında ayrıntılar sağlar.

## <a name="supported-scenarios"></a>Desteklenen senaryolar
> [!NOTE]
> * Yedekleme ve geri yükleme şifrelenmiş VM'lerin yalnızca Resource Manager dağıtılan sanal makineler için desteklenir. Klasik sanal makineleri için desteklenmez. <br>
> * Hem Windows hem de Linux hello endüstri standart BitLocker özelliği, Windows ve Linux tooprovide şifreleme disklerin DM-Crypt özelliği yararlanır Azure Disk şifrelemesi kullanarak sanal makineleri için desteklenir. <br>
> * Yalnızca sanal makinelerde BitLocker şifreleme anahtarını ve anahtar şifreleme anahtarı kullanılarak şifrelenmiş desteklenmiyor. BitLocker şifreleme anahtarı yalnızca kullanılarak şifrelenmiş sanal makineler için desteklenmez. <br>
>
>

## <a name="prerequisites"></a>Ön koşullar
1. Sanal makine kullanarak şifrelenmiş [Azure Disk şifrelemesi](../security/azure-security-disk-encryption.md). BitLocker şifreleme anahtarını ve anahtar şifreleme anahtarı kullanılarak şifrelenmesi.
2. Kurtarma Hizmetleri kasası oluşturulur ve depolama çoğaltma kullanarak kümesine adımları hello makalede değinilen [yedekleme için ortamınızı hazırlama](backup-azure-arm-vms-prepare.md).
3. Azure yedekleme verilen [izinleri tooaccess anahtar kasası](#provide-permissions-to-azure-backup) anahtarlarını içeren, VM'ler için gizli şifrelenmiş.

## <a name="backup-encrypted-vm"></a>VM yedekleme şifreli
Aşağıdaki adımları tooset yedekleme hedefi hello kullanın, ilkesini tanımlamak, öğeleri ve tetikleyici yedekleme yapılandırın.

### <a name="configure-backup"></a>Yedeklemeyi yapılandırma
1. Açık bir kurtarma Hizmetleri kasası zaten varsa toonext adıma geçin. Açık kurtarma Hizmetleri kasanız yoksa ancak hello hello Hub menüsünde, Azure portalında bulunan tıklatmak **Gözat**.

   * Kaynakları Hello listesinde yazın **kurtarma Hizmetleri**.
   * Yazmaya başladığınızda liste filtreleri, girişinize göre hello. **Kurtarma Hizmetleri kasaları** seçeneğini gördüğünüzde buna tıklayın.

      ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     Merhaba kurtarma Hizmetleri kasalarının listesi görüntülenir. Kurtarma Hizmetleri kasalarının Hello listesinden bir kasa seçin.

     Merhaba seçilen kasa panosu açılır.
2. Kasa altında görüntülenen hello listeden öğelerinin tıklatın **yedekleme** tooopen hello yedekleme dikey penceresinde.

      ![Yedekleme dikey penceresini açma](./media/backup-azure-vms-encryption/select-backup.png)
3. Merhaba yedekleme dikey penceresinde **yedekleme hedefi** tooopen hello yedekleme hedefi dikey penceresi.

      ![Senaryo dikey penceresini açma](./media/backup-azure-vms-encryption/select-backup-goal-one.png)
4. Merhaba yedekleme hedefi dikey penceresinde ayarlamak **, iş yükünü çalıştırdığı** tooAzure ve **ne toobackup istediğiniz** tooVirtual makine ve ardından **Tamam**.

   Merhaba yedekleme hedefi dikey penceresi kapanır ve hello yedekleme İlkesi dikey penceresi açılır.

   ![Senaryo dikey penceresini açma](./media/backup-azure-vms-encryption/select-backup-goal-two.png)
5. Merhaba yedekleme İlkesi dikey penceresinde, tooapply toohello kasası istediğiniz hello yedekleme ilkesini seçme **Tamam**.

      ![Yedekleme ilkesini seçme](./media/backup-azure-vms-encryption/setting-rs-backup-policy-new.png)

    Merhaba varsayılan ilke Hello ayrıntılarını hello Ayrıntılar listelenir. Bir ilke toocreate istiyorsanız seçin **Yeni Oluştur** hello açılan menüsünden. Tıkladığınızda **Tamam**, hello yedekleme İlkesi hello kasayla ilişkili.

    Sonraki hello VM'ler tooassociate hello kasası ile seçin.
6. Merhaba şifrelenmiş tooassociate hello ile ilke belirtilen ve'ı tıklatın sanal makineleri seçin **Tamam**.

      ![Şifrelenmiş sanal makineleri seçin](./media/backup-azure-vms-encryption/selected-encrypted-vms.png)
7. Bu sayfada şifrelenmiş ilişkili toohello VM'ler seçili anahtar kasası hakkında bir ileti görüntülenir. Yedekleme hizmeti salt okunur erişim toohello anahtarları ve gizli anahtarları hello anahtar kasasında gerektirir. Bu izinleri toobackup anahtarı kullanır ve VM'ler hello birlikte gizli ilişkilendirilmiş. **İzinleri toobackup hizmet tooaccess anahtar kasası için yedeklemeler toowork vermelisiniz**. Kullanarak bu izinleri sağlayabilir [hello aşağıdaki bölümde belirtilen adımlar](#provide-permissions-to-azure-backup).

      ![Şifrelenmiş VM'ler ileti](./media/backup-azure-vms-encryption/encrypted-vm-warning-message.png)

      Merhaba yedekleme dikey penceresinde hello kasa için tüm ayarların hello sayfanın hello sonundaki yedeklemeyi Etkinleştir düğmesini tanımladığınız tıklatın. Etkinleştirme yedekleme hello İlkesi toohello kasası ve hello VM'ler dağıtır.
8. Hello hazırlık sonraki aşamasında hello VM Aracısı yüklüyor veya emin hello VM Aracısı yapmadan yüklenir. toodo aynı Merhaba, hello makalede açıklanan başlangıç adımları kullanın [yedekleme için ortamınızı hazırlama](backup-azure-arm-vms-prepare.md).

### <a name="triggering-backup-job"></a>Yedekleme işini tetiklemeden
Merhaba makalede açıklanan başlangıç adımları kullanın [yedekleme Azure VM'ler toorecovery Hizmetleri kasası](backup-azure-arm-vms.md) tootrigger yedekleme işi.

### <a name="continue-backups-of-already-backed-up-vms-with-encryption-enabled"></a>Zaten etkin şifreleme ile Vm'leri yedeklenen yedeklerini devam  
Zaten kurtarma Hizmetleri kasasına yedekleme yukarı ediliyor VMs varsa ve sonraki bir zamanda şifreleme için etkin, izinleri toobackup hizmet tooaccess anahtar kasası için yedeklemeler toocontinue vermeniz gerekir. Kullanarak bu izinleri sağlayabilir [hello aşağıdaki bölümde adımları](#provide-permissions-to-azure-backup) veya PowerShell kullanarak adımları bölümünde belirtildiği **yedeklemeyi etkinleştir** bölümünü [PowerShell belgelerine](backup-azure-vms-automation.md). 

## <a name="provide-permissions-tooazure-backup"></a>İzinleri tooAzure yedekleme sağlayın
Aşağıdaki adımları tooprovide ilgili izinleri tooAzure yedekleme tooaccess anahtar kasası hello kullanın ve şifrelenmiş VM'ler yedeğini alın:
1. Seçin **daha Hizmetleri** arayın ve **anahtar kasalarını**.

    ![Arama anahtar kasası](./media/backup-azure-vms-encryption/search-key-vault.png)
    
2. Yedeklenen toobe gereken şifrelenmiş VM ile ilişkili hello anahtar kasası anahtar kasalarını Hello listeden seçin.

     ![Anahtar kasası seçin](./media/backup-azure-vms-encryption/select-key-vault.png)
     
3. Tıklatın **erişim ilkeleri** ve ardından **yeni Ekle**.

    ![Erişim İlkesi Ekle](./media/backup-azure-vms-encryption/select-key-vault-access-policy.png)
    
4. Tıklatın **Select asıl** ve türü **yedekleme yönetim hizmeti** hello arama çubuğunda. 

    ![Arama yedekleme hizmeti](./media/backup-azure-vms-encryption/search-backup-service.png)
    
5. Seçin **yedekleme yönetim hizmeti** ve Seç düğmesini tıklatın.

    ![Yedekleme hizmeti seçin](./media/backup-azure-vms-encryption/select-backup-service.png)
    
6. Seçin **Azure Backup** şablondan yapılandırma açılır. Anahtar izinleri hello gerekli izinleri önceden doldurur ve gizli izinleri açılır. 

    ![Azure yedekleme seçin](./media/backup-azure-vms-encryption/select-backup-template.png)
    
7. **Tamam** düğmesine tıklayın. Yedekleme Yönetimi hizmeti erişim ilkeleri dikey penceresinde eklenen dikkat edin. 

    ![Yedekleme hizmeti erişim ilkesi](./media/backup-azure-vms-encryption/backup-service-access-policy.png)
    
8. **Kaydet** düğmesine tıklayın. Bu gerekli hello izinleri tooAzure yedekleme verir.

    ![Yedekleme hizmeti erişim ilkesi](./media/backup-azure-vms-encryption/save-access-policy.png)

İzinleri başarıyla sağlanan sonra yedekleme şifrelenmiş VM'ler için etkinleştirme işlemiyle devam edebilirsiniz.

## <a name="restore-encrypted-vm"></a>Şifrelenmiş VM geri yükleme
toorestore şifreli VM, ilk geri diskler kullanarak adımları bölümünde bahsedildiği bölüm **yedeklenmiş diskleri geri yükleme** içinde [VM seçerek geri yükleme yapılandırmasını](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Bundan sonra aşağıdaki seçenekleri şu hello birini kullanabilirsiniz:
* Belirtilen hello PowerShell adımları kullanın [geri yüklenen disklerden bir VM oluşturmak](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate geri yüklenen disklerden VM tam.
* VEYA, [geri diskleri bir parçası olarak oluşturulan şablonu kullan](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm) toocreate VM'ler geri yüklenen disklerden. Şablonları yalnızca 26 Nisan 2017 sonra oluşturulan kurtarma noktaları için kullanılabilir.

## <a name="troubleshooting-errors"></a>Sorun giderme
| İşlem | Hata ayrıntıları | Çözüm |
| --- | --- | --- |
| Backup |Sanal makine BEK ile tek başına şifrelenmiş olarak doğrulaması başarısız oldu. Yalnızca şifrelenmiş BEK ve KEK ile sanal makineleri için yedeklemeleri etkinleştirilebilir. |Sanal makine BEK ve KEK kullanarak şifrelenmelidir. İlk VM hello şifresini çözmek ve BEK ve KEK kullanarak şifreleyebilirsiniz. VM BEK ve KEK kullanılarak şifrelenmiş bir kez yedekleme etkinleştirin. Ne yapabileceğiniz hakkında daha fazla bilgi edinin [hello VM şifrelemek ve şifresini çözmek](../security/azure-security-disk-encryption.md)  |
| Geri Yükleme |Bu VM ile ilişkili anahtar kasası mevcut olmadığından bu şifrelenmiş VM geri yükleyemezsiniz. |Anahtar kasası kullanarak oluşturduğunuz [Azure anahtar kasası ile çalışmaya başlama](../key-vault/key-vault-get-started.md). Merhaba makalesine başvurun [anahtar kasası anahtarı ve gizli Azure Yedekleme'yi kullanarak geri yükleme](backup-azure-restore-key-secret.md) toorestore anahtar ve olmaları durumunda gizli anahtarı yok. |
| Geri Yükleme |Anahtar ve bu VM ile ilişkili gizli mevcut olduğundan bu şifrelenmiş VM geri yükleyemezsiniz. |Merhaba makalesine başvurun [anahtar kasası anahtarı ve gizli Azure Yedekleme'yi kullanarak geri yükleme](backup-azure-restore-key-secret.md) toorestore anahtar ve olmaları durumunda gizli anahtarı yok. |
| Geri Yükleme |Yedekleme hizmeti yetkilendirme tooaccess kaynakları aboneliğinizde sahip değil. |Bölümünde belirtilen adımları kullanarak ilk olarak, geri yükleme diskleri yukarıda belirtildiği gibi **yedeklenmiş diskleri geri yükleme** içinde [VM seçerek geri yükleme yapılandırmasını](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Bu, kullanıcı PowerShell sonra çok[geri yüklenen disklerden bir VM oluşturmak](backup-azure-vms-automation.md#create-a-vm-from-restored-disks). |
|Backup | Azure Backup hizmeti yedekleme, şifrelenmiş sanal makineler için yeterli izinleri tooKey Kasa yok | Sanal makine, BitLocker şifreleme anahtarını ve anahtar şifreleme anahtarı kullanarak şifrelenmelidir. Bundan sonra yedekleme etkinleştirilmelidir.  Yedekleme hizmeti kullanarak bu izinleri sağlanmalıdır [hello yukarıdaki bölümünde belirtilen adımları](#provide-permissions-to-azure-backup) veya hello bahsedilen PowerShell adımları kullanarak **korumayı etkinleştir** hello PowerShell bölümü belgeleri [kullanım AzureRM.RecoveryServices.Backup cmdlet'leri tooback sanal makineleri yedeklemek](backup-azure-vms-automation.md#back-up-azure-vms). |  
