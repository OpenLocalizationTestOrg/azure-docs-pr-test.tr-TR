---
title: "Yedekleme ve geri yükleme Vm'leri Azure Backup kullanılarak şifrelenmiş"
description: "Bu makalede yedekleme hakkında konuşur ve geri yükleme deneyimi VM'ler için Azure Disk şifrelemesi kullanılarak şifrelenmiş."
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
ms.openlocfilehash: 89492cda8eff23509bee7693bb5f7e6ab5eb10d1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-back-up-and-restore-encrypted-virtual-machines-with-azure-backup"></a>Azure yedekleme ile sanal makineleri yedeklemek ve geri yükleme şifreli
Bu makalede yedekleme ve geri yükleme Azure Backup kullanarak sanal makineleri için ilgili adımlar açıklanmaktadır. Ayrıca hata durumları için desteklenen senaryolar, ön koşullar ve sorun giderme adımları hakkında ayrıntılar sağlar.

## <a name="supported-scenarios"></a>Desteklenen senaryolar
> [!NOTE]
> * Yedekleme ve geri yükleme şifrelenmiş VM'lerin yalnızca Resource Manager dağıtılan sanal makineler için desteklenir. Klasik sanal makineleri için desteklenmez. <br>
> * Hem Windows hem de Linux, Windows ve DM-Crypt özelliğinin Linux disk şifreleme sağlamak için endüstri standart BitLocker özelliğinden yararlanır Azure Disk şifrelemesi kullanarak sanal makineleri için desteklenir. <br>
> * Yalnızca sanal makinelerde BitLocker şifreleme anahtarını ve anahtar şifreleme anahtarı kullanılarak şifrelenmiş desteklenmiyor. BitLocker şifreleme anahtarı yalnızca kullanılarak şifrelenmiş sanal makineler için desteklenmez. <br>
>
>

## <a name="prerequisites"></a>Ön koşullar
1. Sanal makine kullanarak şifrelenmiş [Azure Disk şifrelemesi](../security/azure-security-disk-encryption.md). BitLocker şifreleme anahtarını ve anahtar şifreleme anahtarı kullanılarak şifrelenmesi.
2. Kurtarma Hizmetleri kasası oluşturulur ve depolama çoğaltma kullanarak kümesine adımları makalede değinilen [yedekleme için ortamınızı hazırlama](backup-azure-arm-vms-prepare.md).
3. Azure yedekleme verilen [anahtar kasası erişim izinleri](#provide-permissions-to-azure-backup) anahtarlarını içeren, VM'ler için gizli şifrelenmiş.

## <a name="backup-encrypted-vm"></a>VM yedekleme şifreli
Yedekleme hedefi ayarlama, ilke tanımlamak, öğeleri ve tetikleyici yedekleme yapılandırmak için aşağıdaki adımları kullanın.

### <a name="configure-backup"></a>Yedeklemeyi yapılandırma
1. Açık kurtarma Hizmetleri kasası zaten varsa, sonraki adıma geçin. Açık Kurtarma Hizmetleri kasanız yoksa ancak Azure portaldaysanız Hub menüsünde **Gözat**'a tıklayın.

   * Kaynak listesinde **Kurtarma Hizmetleri** yazın.
   * Yazmaya başladığınızda liste, girişinize göre filtrelenir. **Kurtarma Hizmetleri kasaları** seçeneğini gördüğünüzde buna tıklayın.

      ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     Kurtarma Hizmetleri kasalarının listesi görünür. Kurtarma Hizmetleri kasalarının listesinden bir kasa seçin.

     Seçilen kasa panosu açılır.
2. Kasa altında görüntülenen listeden öğelerinin tıklatın **yedekleme** yedekleme dikey penceresini açın.

      ![Yedekleme dikey penceresini açma](./media/backup-azure-vms-encryption/select-backup.png)
3. Yedekleme dikey penceresinde, Yedekleme Hedefi dikey penceresini açmak için **Yedekleme hedefi** seçeneğine tıklayın.

      ![Senaryo dikey penceresini açma](./media/backup-azure-vms-encryption/select-backup-goal-one.png)
4. Yedekleme hedefi dikey penceresinde ayarlamak **, iş yükünü çalıştırdığı** Azure ve **neleri yedeklemek istiyorsunuz** sanal makineye'ye tıklayın **Tamam**.

   Yedekleme Hedefi dikey penceresi kapanır ve Yedekleme ilkesi dikey penceresi açılır.

   ![Senaryo dikey penceresini açma](./media/backup-azure-vms-encryption/select-backup-goal-two.png)
5. Yedekleme ilkesi dikey penceresinde, kasaya uygulamak istediğiniz yedekleme ilkesini seçin ve **Tamam**'a tıklayın.

      ![Yedekleme ilkesini seçme](./media/backup-azure-vms-encryption/setting-rs-backup-policy-new.png)

    Varsayılan ilkenin ayrıntıları, ayrıntılar içinde listelenir. Yeni bir ilke oluşturmak istiyorsanız açılan menüden **Yeni Oluştur**'u seçin. **Tamam**'a tıklamanızın ardından, yedekleme ilkesi kasayla ilişkilendirilir.

    Daha sonra, kasa ile ilişkilendirilecek VM'leri seçin.
6. Belirtilen ilke ile ilişkilendirmek tıklatıp şifrelenmiş sanal makineleri seçin **Tamam**.

      ![Şifrelenmiş sanal makineleri seçin](./media/backup-azure-vms-encryption/selected-encrypted-vms.png)
7. Bu sayfa seçilen şifrelenmiş VM'ler ilişkili anahtar kasası hakkında bir ileti gösterir. Yedekleme hizmeti anahtarlar ve gizli anahtar kasasında salt okunur erişim gerektirir. Bu izinleri yedek anahtarı ve gizli anahtarı, ilişkili sanal makineleri birlikte kullanır. **Yedekleme hizmeti yedeklemelerinin çalışmak anahtar kasası erişmek için izinleri vermeniz gerekir**. Kullanarak bu izinleri sağlayabilir [bölümünde belirtilen adımları](#provide-permissions-to-azure-backup).

      ![Şifrelenmiş VM'ler ileti](./media/backup-azure-vms-encryption/encrypted-vm-warning-message.png)

      Tanımladığınız artık, sayfanın sonundaki yedeklemeyi etkinleştir yedekleme dikey penceresinde, kasaya için tüm ayarlar'ı tıklatın. Yedeklemeyi etkinleştir ilkeyi kasaya ve Vm'lere dağıtır.
8. Hazırlık sonraki aşamasında VM Aracısı yükleme veya VM Aracısı emin yüklü. Aynı işlemi gerçekleştirmek için makalesinde belirtilen adımları kullanın [yedekleme için ortamınızı hazırlama](backup-azure-arm-vms-prepare.md).

### <a name="triggering-backup-job"></a>Yedekleme işini tetiklemeden
Makalede açıklanan adımları kullanın [yedekleme Azure Vm'leri kurtarma Hizmetleri kasasına](backup-azure-arm-vms.md) tetikleyici yedekleme işi için.

### <a name="continue-backups-of-already-backed-up-vms-with-encryption-enabled"></a>Zaten etkin şifreleme ile Vm'leri yedeklenen yedeklerini devam  
Zaten kurtarma Hizmetleri kasasına yedekleme yukarı ediliyor VMs varsa ve sonraki bir zamanda şifreleme için etkin, yedekleme hizmetine devam etmek yedeklemeler için anahtar kasası erişmesine izin vermeniz gerekir. Kullanarak bu izinleri sağlayabilir [aşağıdaki bölümde adımları](#provide-permissions-to-azure-backup) veya PowerShell kullanarak adımları bölümünde belirtildiği **yedeklemeyi etkinleştir** bölümünü [PowerShell belgelerine](backup-azure-vms-automation.md). 

## <a name="provide-permissions-to-azure-backup"></a>Azure Backup için izinler sağlar
Erişim anahtarı için Azure yedekleme için ilgili izinleri kasa ve şifrelenmiş VM'ler yedeğini almanızı sağlamak için aşağıdaki adımları kullanın:
1. Seçin **daha Hizmetleri** arayın ve **anahtar kasalarını**.

    ![Arama anahtar kasası](./media/backup-azure-vms-encryption/search-key-vault.png)
    
2. Yedeklenmesi gereken şifrelenmiş VM ile ilişkili anahtar kasası anahtar kasalarının listesinden seçin.

     ![Anahtar kasası seçin](./media/backup-azure-vms-encryption/select-key-vault.png)
     
3. Tıklatın **erişim ilkeleri** ve ardından **yeni Ekle**.

    ![Erişim İlkesi Ekle](./media/backup-azure-vms-encryption/select-key-vault-access-policy.png)
    
4. Tıklatın **Select asıl** ve türü **yedekleme yönetim hizmeti** arama çubuğunda. 

    ![Arama yedekleme hizmeti](./media/backup-azure-vms-encryption/search-backup-service.png)
    
5. Seçin **yedekleme yönetim hizmeti** ve Seç düğmesini tıklatın.

    ![Yedekleme hizmeti seçin](./media/backup-azure-vms-encryption/select-backup-service.png)
    
6. Seçin **Azure Backup** şablondan yapılandırma açılır. Anahtar izinleri gerekli izinler önceden doldurur ve gizli izinleri açılır. 

    ![Azure yedekleme seçin](./media/backup-azure-vms-encryption/select-backup-template.png)
    
7. **Tamam** düğmesine tıklayın. Yedekleme Yönetimi hizmeti erişim ilkeleri dikey penceresinde eklenen dikkat edin. 

    ![Yedekleme hizmeti erişim ilkesi](./media/backup-azure-vms-encryption/backup-service-access-policy.png)
    
8. **Kaydet** düğmesine tıklayın. Azure Backup için gerekli izinleri verir.

    ![Yedekleme hizmeti erişim ilkesi](./media/backup-azure-vms-encryption/save-access-policy.png)

İzinleri başarıyla sağlanan sonra yedekleme şifrelenmiş VM'ler için etkinleştirme işlemiyle devam edebilirsiniz.

## <a name="restore-encrypted-vm"></a>Şifrelenmiş VM geri yükleme
Şifrelenmiş VM geri yüklemek için ilk geri diskler kullanarak, belirtilen bölüm adımları **yedeklenmiş diskleri geri yükleme** içinde [VM seçerek geri yükleme yapılandırmasını](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Bundan sonra aşağıdaki seçeneklerden birini kullanabilirsiniz:
* Belirtilen PowerShell adımları kullanın [geri yüklenen disklerden bir VM oluşturmak](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) geri yüklenen disklerden tam VM oluşturmak için.
* VEYA, [geri diskleri bir parçası olarak oluşturulan şablonu kullan](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm) geri yüklenen disklerden VM'ler oluşturmak için. Şablonları yalnızca 26 Nisan 2017 sonra oluşturulan kurtarma noktaları için kullanılabilir.

## <a name="troubleshooting-errors"></a>Sorun giderme
| İşlem | Hata ayrıntıları | Çözüm |
| --- | --- | --- |
| Backup |Sanal makine BEK ile tek başına şifrelenmiş olarak doğrulaması başarısız oldu. Yalnızca şifrelenmiş BEK ve KEK ile sanal makineleri için yedeklemeleri etkinleştirilebilir. |Sanal makine BEK ve KEK kullanarak şifrelenmelidir. İlk VM şifresini çözmek ve BEK ve KEK kullanarak şifreleyebilirsiniz. VM BEK ve KEK kullanılarak şifrelenmiş bir kez yedekleme etkinleştirin. Ne yapabileceğiniz hakkında daha fazla bilgi edinin [VM şifrelemek ve şifresini çözmek](../security/azure-security-disk-encryption.md)  |
| Geri Yükleme |Bu VM ile ilişkili anahtar kasası mevcut olmadığından bu şifrelenmiş VM geri yükleyemezsiniz. |Anahtar kasası kullanarak oluşturduğunuz [Azure anahtar kasası ile çalışmaya başlama](../key-vault/key-vault-get-started.md). Makaleyi başvurun [anahtar kasası anahtarı ve gizli Azure Yedekleme'yi kullanarak geri yükleme](backup-azure-restore-key-secret.md) olmadıkları anahtarı ve gizli anahtarını geri yüklemek için. |
| Geri Yükleme |Anahtar ve bu VM ile ilişkili gizli mevcut olduğundan bu şifrelenmiş VM geri yükleyemezsiniz. |Makaleyi başvurun [anahtar kasası anahtarı ve gizli Azure Yedekleme'yi kullanarak geri yükleme](backup-azure-restore-key-secret.md) olmadıkları anahtarı ve gizli anahtarını geri yüklemek için. |
| Geri Yükleme |Yedekleme Hizmeti'nin aboneliğinizdeki kaynaklara erişme yetkisi yok. |Bölümünde belirtilen adımları kullanarak ilk olarak, geri yükleme diskleri yukarıda belirtildiği gibi **yedeklenmiş diskleri geri yükleme** içinde [VM seçerek geri yükleme yapılandırmasını](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Bu, kullanıcı PowerShell sonra için [geri yüklenen disklerden bir VM oluşturmak](backup-azure-vms-automation.md#create-a-vm-from-restored-disks). |
|Backup | Azure Backup hizmeti yedekleme, şifrelenmiş Virtual Machines için yeterli izinleri anahtar kasası için yok | Sanal makine, BitLocker şifreleme anahtarını ve anahtar şifreleme anahtarı kullanarak şifrelenmelidir. Bundan sonra yedekleme etkinleştirilmelidir.  Yedekleme hizmeti kullanarak bu izinleri sağlanmalıdır [yukarıdaki bölümde belirtilen adımlar](#provide-permissions-to-azure-backup) veya belirtilen PowerShell adımları kullanarak **korumayı etkinleştir** PowerShell belgelerine bölümünü [sanal makineleri yedeklemek için kullanım AzureRM.RecoveryServices.Backup cmdlet'leri](backup-azure-vms-automation.md#back-up-azure-vms). |  
