---
title: "Windows sistem durumu tooAzure yukarı aaaBack | Microsoft Docs"
description: "Merhaba sistem durumunu Windows Server ve/veya Windows bilgisayarları tooAzure tooback öğrenin."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "nasıl toobackup; nasıl tooback; Yedekleme dosyaları ve klasörleri"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: be5d4be81af981c10de82add9fe962a730753cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a>Resource Manager dağıtım Windows sistem durumu yedekleme
Bu makalede, Windows Server sisteminizi tooback durum tooAzure nasıl açıklanmaktadır. Eğitmen hedeflenen toowalk olan hello temel bilgileri size.

Tooknow Azure yedekleme hakkında daha fazla bilgi istiyorsanız, bu okuma [genel bakış](backup-introduction-to-azure-backup.md).

Azure aboneliğiniz yoksa istediğiniz Azure hizmetine erişmenizi sağlayan [ücretsiz bir hesap](https://azure.microsoft.com/free/) oluşturun.

## <a name="create-a-recovery-services-vault"></a>Kurtarma hizmetleri kasası oluşturma
tooback dosya ve klasörleri toocreate toostore hello verilerin istediğiniz hello bölgede bir kurtarma Hizmetleri kasası gerekir. Çoğaltılan depolama alanınızın nasıl istediğiniz toodetermine de gerekir.

### <a name="toocreate-a-recovery-services-vault"></a>toocreate bir kurtarma Hizmetleri kasası
1. Zaten yapmadıysanız, toohello içinde oturum [Azure Portal](https://portal.azure.com/) Azure aboneliğinizi kullanarak.
2. Merhaba Hub menüsünde **daha fazla hizmet** ve kaynakları hello listesinde yazın **kurtarma Hizmetleri** tıklatıp **kurtarma Hizmetleri kasaları**.

    ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Merhaba abonelikte kurtarma Hizmetleri kasaları varsa hello kasalarını listelenir.
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

8. Merhaba kurtarma Hizmetleri kasası dikey penceresinde Hello altındaki tıklatın **oluşturma**.

    Oluşturulan toobe kurtarma Hizmetleri kasası hello için birkaç dakika sürebilir. Merhaba portal hello üst sağ bölmesinde Hello durum bildirimlerini izleyin. Kasanız oluşturulduktan sonra hello kurtarma Hizmetleri kasaları listesinde görünür. Birkaç dakika sonra kasayı görmezseniz **Yenile**’ye tıklayın.

    ![Yenile düğmesine tıklayın](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    Kasanızı kurtarma Hizmetleri kasalarının hello listesinde gördüğünüz verdikten sonra hazır tooset hello depolama artıklığı demektir.

### <a name="set-storage-redundancy-for-hello-vault"></a>Depolama artıklığı hello kasası için ayarlama
Kurtarma Hizmetleri kasası oluşturduğunuzda, depolama artıklığı istediğiniz yapılandırılmış hello biçimde olduğundan emin olun.

1. Merhaba gelen **kurtarma Hizmetleri kasaları** dikey penceresinde hello yeni kasaya tıklayın.

    ![Kurtarma Hizmetleri kasası hello listeden Hello yeni kasa seçin](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    Merhaba kasası seçtiğinizde hello **kurtarma Hizmetleri kasası** dikey daraltır ve hello ayarları dikey (*hello üstünde hello kasasının hello ada sahip*) ve hello kasa Ayrıntılar dikey penceresini açın.

    ![Yeni kasa için Görünüm hello depolama yapılandırması](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. Merhaba yeni kasasının ayarlar dikey penceresinde hello dikey slayt tooscroll toohello Yönet bölümüne aşağı kullanın ve'ı tıklatın **Yedekleme Altyapısı**.
    Merhaba yedekleme altyapısı dikey pencere açılır.
3. Merhaba yedekleme altyapısı dikey penceresinde tıklayın **yedekleme yapılandırması** tooopen hello **yedekleme yapılandırması** dikey.

    ![Yeni kasa Hello depolama yapılandırmasını ayarlayın](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. Kasanız için Hello uygun depolama çoğaltma seçeneğini seçin.

    ![depolama yapılandırması seçenekleri](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    Varsayılan olarak, kasanız coğrafi olarak yedekli depolamaya sahiptir. Azure birincil yedekleme alanı uç noktası kullanıyorsanız, toouse devam **coğrafi olarak yedekli**. Birincil yedekleme alanı uç noktası Azure kullanmıyorsanız, ardından **yerel olarak yedekli**, hello Azure depolama maliyetlerini azaltır. [Coğrafi olarak yedekli](../storage/common/storage-redundancy.md#geo-redundant-storage) ve [yerel olarak yedekli](../storage/common/storage-redundancy.md#locally-redundant-storage) depolama seçenekleri hakkında daha fazla bilgiyi [Depolama yedekliliğine genel bakış](../storage/common/storage-redundancy.md) bölümünden edinebilirsiniz.

Bir kasa oluşturduğunuza göre Windows sistem durumunu yedekleme için yapılandırın.

## <a name="configure-hello-vault"></a>Merhaba kasası yapılandırma
1. Açık kurtarma Hizmetleri kasası dikey (Merhaba kasa), yeni oluşturduğunuz, hello Başlarken bölümünde Merhaba, tıklatın **yedekleme**, sonra da hello **yedekleme ile çalışmaya başlama** dikey penceresinde, select  **Yedekleme hedefi**.

    ![Yedekleme hedefi dikey penceresini açma](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    Merhaba **yedekleme hedefi** dikey pencere açılır.

    ![Yedekleme hedefi dikey penceresini açma](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. Merhaba gelen **, iş yükünü çalıştırdığı?** açılır menüsünde, select **şirket içi**.

    Windows Server veya Windows bilgisayarınız Azure üzerinde olmayan fiziksel bir makine olduğu için **Şirket içi** seçeneğini belirlersiniz.

3. Merhaba gelen **neler toobackup istediğiniz?** menüsünde, select **sistem durumu**, tıklatıp **Tamam**.

    ![Dosya ve klasörleri yedekleme](./media/backup-azure-system-state/backup-goal-system-state.png)

    Tamam'ı tıklattıktan sonra bir onay işareti çok sonraki görünür**yedekleme hedefi**ve hello **altyapıyı hazırlama** dikey pencere açılır.

    ![Yedekleme hedefi yapılandırılmıştır, bundan sonra altyapıyı hazırlayın](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. Merhaba üzerinde **altyapıyı hazırlama** dikey penceresinde tıklatın **karşıdan aracısı için Windows Server veya Windows İstemcisi**.

    ![altyapıyı hazırlama](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    Windows Server temel kullanıyorsanız, Windows Server temel için toodownload hello Aracısı seçin. Açılır menü toorun komut istemleri veya MARSAgentInstaller.exe kaydedin.

    ![MARSAgentInstaller iletişim kutusu](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. Merhaba indirme açılır menüsünde tıklatın **kaydetmek**.

    Varsayılan olarak, hello **MARSagentinstaller.exe** dosya tooyour indirmeler klasörüne kaydedilir. Merhaba yükleyici tamamladığında, toorun hello yükleyici istediğiniz veya hello klasörünü açın, isteyen bir açılır pencere görürsünüz.

    ![altyapıyı hazırlama](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    Tooinstall hello Aracısı henüz gerekmez. Merhaba kasa kimlik bilgileri indirdikten sonra hello aracısını yükleyebilirsiniz.

6. Merhaba üzerinde **altyapıyı hazırlama** dikey penceresinde tıklatın **karşıdan**.

    ![kasa kimlik bilgilerini indirme](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    Merhaba kasa kimlik bilgileri tooyour indirmeler klasörüne indirin. Hello kasa kimlik bilgilerini indirme işlemini tamamladıktan sonra tooopen istediğiniz veya hello kimlik bilgilerini Kaydet isteyen bir açılır pencere görürsünüz. **Kaydet** düğmesine tıklayın. Yanlışlıkla tıklatırsanız **açık**, tooopen hello kasa kimlik bilgileri çalışır hello iletişim sağlar, başarısız. Merhaba kasa kimlik bilgileri açamıyor. Toohello sonraki adıma geçin. Merhaba kasa kimlik bilgileri hello indirme klasöründe yer alır.   

    ![kasa kimlik bilgilerini indirme tamamlandı](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a>Yükleme ve hello Aracısı kaydedin

> [!NOTE]
> Hello Azure portal üzerinden yedeklemeyi etkinleştirme olanağı henüz kullanılabilir değil. Windows Server sistem durumu yedeklemesi Hello Microsoft Azure kurtarma Hizmetleri Aracısı tooback kullanın.
>

1. Bulun ve çift hello **MARSagentinstaller.exe** hello yükleme klasöründen (veya diğer kayıtlı konumdan).

    Merhaba yükleyici, bir dizi ileti ayıklar gibi yükler ve hello kurtarma Hizmetleri aracısını kaydeder sağlar.

    ![Kurtarma Hizmetleri aracısı yükleyici kimlik bilgilerini çalıştırma](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. Merhaba Microsoft Azure kurtarma Hizmetleri Aracısı Kurulum Sihirbazı tamamlayın. toocomplete Başlangıç Sihirbazı, şunları yapmanız gerekir:

   * Merhaba yükleme ve önbellek klasörü için bir konum seçin.
   * Bir proxy sunucu tooconnect toohello kullanırsanız, Ara sunucu bilgilerinizi sağlayın Internet.
   * Kimliği doğrulanmış bir ara sunucu kullanıyorsanız kullanıcı adı ve parola bilgilerinizi sağlayın.
   * Merhaba indirilen kasa kimlik bilgilerini sağlayın
   * Merhaba şifreleme parolası güvenli bir konuma kaydedin.

     > [!NOTE]
     > Kaybeder veya hello parolayı unutursanız Microsoft hello yedekleme verilerini kurtarmanıza yardımcı olamaz. Merhaba dosyayı güvenli bir konuma kaydedin. Gerekli toorestore bir yedekleme olur.
     >
     >

Merhaba aracı artık yüklenmiş ve kayıtlı toohello kasasına makineniz olduğu. Hazır tooconfigure olduğunuz ve yedekleme zamanlayabilirsiniz.

## <a name="back-up-windows-server-system-state-preview"></a>Windows Server sistem durumunu (Önizleme) yedekleme
Merhaba ilk yedekleme üç görevleri içerir:

* Sistem durumu yedeklemesi hello Azure Backup aracısını kullanan etkinleştir
* Merhaba yedekleme zamanlaması
* Dosya ve klasörleri hello için ilk kez yedekleme

toocomplete hello ilk yedekleme, kullanım hello Microsoft Azure kurtarma Hizmetleri Aracısı.

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a>tooenable sistem durumu yedeklemesi Hello Azure yedekleme Aracısı'nı kullanma

1. Bir PowerShell oturumunda komut toostop hello Azure yedekleme altyapısı aşağıdaki hello çalıştırın.

  ```
  PS C:\> Net stop obengine
  ```

2. Merhaba Windows kayıt defterini açın.

  ```
  PS C:\> regedit.exe
  ```

3. Aşağıdaki kayıt defteri anahtarı hello hello DWord değerini belirtilen ekleyin.

  | Kayıt defteri yolu | Kayıt defteri anahtarı | DWord değeri |
  |---------------|--------------|-------------|
  | HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider | TurnOffSSBFeature | 2 |

4. Yükseltilmiş bir komut istemi komutunda aşağıdaki hello yürüterek Hello Backup altyapısını yeniden başlatın.

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a>tooschedule hello yedekleme işi

1. Merhaba Microsoft Azure kurtarma Hizmetleri Aracısı'nı açın. Bunu, makinenizde **Microsoft Azure Backup** aramasını yaparak bulabilirsiniz.

    ![Hello Azure kurtarma Hizmetleri aracısını başlatma](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. Merhaba kurtarma Hizmetleri aracısında tıklatın **yedekleme zamanlaması**.

    ![Windows Server yedeklemesini zamanlama](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. Merhaba üzerinde hello yedeklemeyi Zamanlama Sihirbazı sayfasında Başlarken, tıklatın **sonraki**.

4. Merhaba öğeleri seçin tooBackup sayfasında, tıklatın **öğeleri Ekle**.

5. Seçin **sistem durumu** ve ardından **Tamam**.

6. **İleri**’ye tıklayın.

7. Merhaba sistem durumu yedekleme ve bekletme zamanlama otomatik olarak her Pazar yukarı tooback 9:00 PM yerel zaman olarak ayarlanır ve hello Bekletme dönemi olarak ayarlanmış too60 gün.

   > [!NOTE]
   > Sistem Durumu yedekleme ve bekletme ilkesi otomatik olarak yapılandırılır. Dosyaları ve klasörleri ayrıca toohello Windows Server sistem durumu yedekleme dosyası yedeklerini hello Sihirbazı'ndan için yalnızca hello yedekleme ve bekletme ilkesi belirtin. 
   >

8. Merhaba onay sayfasında hello bilgileri gözden geçirin ve ardından **son**.

9. Merhaba Sihirbazı hello yedekleme zamanlamasını oluşturduktan sonra tıklayın **Kapat**.

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a>Windows Server sistem durumunun tooback hello ilk kez için

1. Windows Server için bir yeniden başlatma gerektiren bekleyen güncelleştirme bulunmadığından emin olun.

2. Merhaba kurtarma Hizmetleri aracısında tıklatın **Şimdi Yedekle** toocomplete hello hello ağ üzerinden dengeli ilk.

    ![Windows Server şimdi yedekle](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. Merhaba onay sayfasında, Şimdi Yedekle sihirbazı hello hello ayarları gözden geçir hello makineyi tooback kullanır. Ardından **Yedekle**'ye tıklayın.

4. Tıklatın **Kapat** tooclose hello Sihirbazı. Merhaba Sihirbazı Hello yedekleme işlemi tamamlanmadan önce kapatırsanız, Başlangıç Sihirbazı'nı toorun hello arka planda devam eder.

5. Dosya ve klasörleri sunucunuzda, ayrıca toohello Windows Server sistem durumu yedekleme yapıyorsanız, hello Şimdi Yedekle Sihirbazı yalnızca dosyaların yedeğini alın. tooperform geçici bir sistem durumu yedekleme, hello aşağıdaki PowerShell komutunu kullanın:

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  Merhaba ilk Yedekleme tamamlandıktan sonra hello **işi tamamlandı** durum hello yedekleme konsolunda görüntülenir.

  ![IR tamamlandı](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a>Sık sorulan sorular

Merhaba aşağıdaki sorular ve yanıtlar tamamlayıcı bilgiler sağlar.

### <a name="what-is-hello-staging-volume"></a>Merhaba hazırlama toplu nedir?

Merhaba hazırlama toplu burada hello yerel olarak kullanılabilir, Windows Server Yedekleme hello sistem durumu yedeklemesi aşamaları hello Ara konumunu temsil eder. Azure Backup Aracısı sonra sıkıştırır ve bu Ara yedekleme şifreler ve güvenli HTTPS protokolünü toohello ile kurtarma Hizmetleri kasası yapılandırılmış gönderir. **Bir Windows işletim biriminde hello hazırlama toplu oluşturmak önerilir. Sistem durumu yedeklemeleri sorunları gözlemlerseniz, hazırlama biriminiz hello konumunu denetimi hello ilk sorun giderme adımdır.** 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a>Merhaba hazırlama birimi hello Azure Backup aracısını belirtilen yolu nasıl değiştirebilir miyim?

Merhaba hazırlama toplu hello önbellek klasöründe varsayılan olarak bulunur. 

1. toochange bu konum, aşağıdaki komutta (yükseltilmiş bir komut istemi) kullanım hello:
  ```
  PS C:\> Net stop obengine
  ```

2. Ardından klasörle hello yolu toohello yeni hazırlama toplu kayıt defteri girdileri aşağıdaki hello güncelleştirin.

  |Kayıt defteri yolu|Kayıt defteri anahtarı|Değer|
  |-------------|------------|-----|
  |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider | SSBStagingPath | Yeni hazırlama toplu konumu |

Merhaba hazırlama yolu büyük küçük harfe duyarlıdır ve ne hello sunucusunda mevcut olarak hello tam aynı büyük/küçük harf olmalıdır. 

3. Merhaba hazırlama birimi yolu değiştirdiğinizde, hello Backup altyapısını yeniden başlatın:
  ```
  PS C:\> Net start obengine
  ```
4. Değiştirilen hello yolu, açık hello Microsoft Azure kurtarma Hizmetleri aracısını ve tetikleyici geçici bir sistem durumu yedeğini toopick.

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a>Neden hello sistem durumu too60 gün varsayılan saklama ayarlanmış mı?

bir sistem durumu yedeklemesi kullanım ömrünü Hello olduğu hello hello Windows Server Active Directory rol hello "kullanım ömrü" ayarı ile aynı. Merhaba hello silinmiş öğe işareti yaşam süresi girişi için varsayılan değer 60 gündür. Bu değer hello dizin hizmeti (NTDS) yapılandırma nesnesi üzerinde ayarlanabilir.

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a>Merhaba varsayılan yedekleme ve bekletme ilkesi için sistem durumu nasıl değiştiririm?

toochange hello varsayılan yedekleme ve bekletme ilkesi sistem durumu için:
1. Merhaba Backup altyapısını durdurun. Komutu yükseltilmiş komut isteminden aşağıdaki hello çalıştırın.

  ```
  PS C:\> Net stop obengine
  ```

2. Ekleme veya kayıt defteri anahtarı girişleri HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider aşağıdaki hello güncelleştirin.

  |Kayıt defteri adı|Açıklama|Değer|
  |-------------|-----------|-----|
  |SSBScheduleTime|Merhaba yedekleme tooconfigure hello saati kullanılır. 9 yerel saati varsayılandır.|DWord: Biçimi 9:30 yerel saati 2130 örneğin SSDD (ondalık)|
  |SSBScheduleDays|Sistem durumu yedeklemesi sırasında hello zaman gerçekleştirilmelidir kullanılan tooconfigure hello günleri saat belirtildi. Tek tek basamak hello haftanın günleri belirtin. 0 Pazar gösteren, 1. Pazartesi, vb.. Varsayılan yedekleme için Pazar günüdür.|DWord: gün hello hafta toorun yedekleme (örneğin 1230 Pazartesi, Salı, Çarşamba ve Pazar yedeklemeler zamanlar ondalık).|
  |SSBRetentionDays|Kullanılan tooconfigure hello gün tooretain yedekleme. Varsayılan değer 60'tır. Değer izin verilen en fazla 180'dir.|DWord: Gün tooretain yedekleme (ondalık).|

3. Komut toorestart hello yedekleme altyapısı aşağıdaki hello kullanın.
    ```
    PS C:\> Net start obengine
    ```

4. Merhaba Microsoft Kurtarma Hizmetleri Aracısı'nı açın.

5. Tıklatın **yedekleme zamanlaması** ve ardından **sonraki** yansıtılan hello değişiklikleri görene kadar.

6. Tıklatın **son** tooapply hello değişiklikleri.


## <a name="questions"></a>Sorularınız mı var?
Sorularınız varsa veya herhangi bir özellik varsa dahil, toosee istediğiniz [Geri bildirimlerinizi bize gönderin](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Sonraki adımlar
* [Windows makinelerini yedekleme](backup-configure-vault.md) konusunda daha fazla bilgi edinin.
* Dosya ve klasörlerinizi yedeklediğinize göre artık [kasa ve sunucularınızı yönetebilirsiniz](backup-azure-manage-windows-server.md).
* Toorestore yedekleme ihtiyacınız varsa, bu makalede çok kullanmak[dosyaları tooa Windows makinesine geri](backup-azure-restore-windows-server.md).
