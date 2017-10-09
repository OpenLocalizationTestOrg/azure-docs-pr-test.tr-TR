---
title: "Windows dosya ve klasörleri tooAzure (Resource Manager) ayarlama aaaBack | Microsoft Docs"
description: "Windows dosya ve klasörleri tooAzure bir Resource Manager dağıtımında yukarı tooback öğrenin."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "nasıl toobackup; nasıl tooback; Yedekleme dosyaları ve klasörleri"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 8/15/2017
ms.author: markgal;
ms.openlocfilehash: 07d6580a84d5092ed2c61bf86ff5fcb148423ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a>İlk bakış: Resource Manager dağıtımında dosya ve klasörleri yedekleme
Bu makalede açıklanır nasıl bir Resource Manager dağıtım kullanarak tooback, Windows Server (veya Windows bilgisayarı) dosyaları ve klasörleri tooAzure. Eğitmen hedeflenen toowalk olan hello temel bilgileri size. Azure Backup ile tooget çalışmaya istiyorsanız hello doğru yerde demektir.

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

    * seçin **Yeni Oluştur** toocreate yeni bir kaynak grubu istiyorsanız.
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

Bir kasa oluşturduğunuza göre dosya ve klasörleri yedeklemek için yapılandırabilirsiniz.

## <a name="configure-hello-vault"></a>Merhaba kasası yapılandırma
1. Açık kurtarma Hizmetleri kasası dikey (Merhaba kasa), yeni oluşturduğunuz, hello Başlarken bölümünde Merhaba, tıklatın **yedekleme**, sonra da hello **yedekleme ile çalışmaya başlama** dikey penceresinde, select  **Yedekleme hedefi**.

    ![Yedekleme hedefi dikey penceresini açma](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    Merhaba **yedekleme hedefi** dikey pencere açılır.

    ![Yedekleme hedefi dikey penceresini açma](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. Merhaba gelen **, iş yükünü çalıştırdığı?** açılır menüsünde, select **şirket içi**.

    Windows Server veya Windows bilgisayarınız Azure üzerinde olmayan fiziksel bir makine olduğu için **Şirket içi** seçeneğini belirlersiniz.

3. Merhaba gelen **neler toobackup istediğiniz?** menüsünde, select **dosya ve klasörleri**, tıklatıp **Tamam**.

    ![Dosya ve klasörleri yedekleme](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

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
> Hello Azure portal üzerinden yedeklemeyi etkinleştirme olanağı henüz kullanılabilir değil. Dosya ve klasörleri Hello Microsoft Azure kurtarma Hizmetleri Aracısı tooback kullanın.
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

## <a name="network-and-connectivity-requirements"></a>Ağ ve Bağlantı Gereksinimleri

Makine/proxy Internet erişimi sınırlı hello mcahine/proxy üzerinde güvenlik duvarı ayarlarını aşağıdaki URL'lere yapılandırılmış tooallow hello olduğundan emin olun: <br>
    1. www.msftncsi.com
    2. *.Microsoft.com
    3. *.WindowsAzure.com
    4. *.microsoftonline.com
    5. *.windows.ne

## <a name="back-up-your-files-and-folders"></a>Dosya ve klasörlerinizi yedekleme
Merhaba ilk yedekleme iki anahtar görev içerir:

* Merhaba yedekleme zamanlaması
* Dosya ve klasörleri hello için ilk kez yedekleme

toocomplete hello ilk yedekleme, kullanım hello Microsoft Azure kurtarma Hizmetleri Aracısı.

### <a name="tooschedule-hello-backup-job"></a>tooschedule hello yedekleme işi
1. Merhaba Microsoft Azure kurtarma Hizmetleri Aracısı'nı açın. Bunu, makinenizde **Microsoft Azure Backup** aramasını yaparak bulabilirsiniz.

    ![Hello Azure kurtarma Hizmetleri aracısını başlatma](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. Merhaba kurtarma Hizmetleri aracısında tıklatın **yedekleme zamanlaması**.

    ![Windows Server yedeklemesini zamanlama](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. Merhaba üzerinde hello yedeklemeyi Zamanlama Sihirbazı sayfasında Başlarken, tıklatın **sonraki**.
4. Merhaba öğeleri seçin tooBackup sayfasında, tıklatın **öğeleri Ekle**.
5. Hello dosya ve klasörlerin tooback yedeklemek istediğiniz ve ardından seçin **Tamam**.
6. **İleri**’ye tıklayın.
7. Merhaba üzerinde **yedekleme zamanlamasını belirtin** sayfasında, hello belirtin **yedekleme zamanlaması** tıklatıp **sonraki**.

    Günlük (en fazla günde üç kez olmak üzere) veya haftalık yedeklemeler zamanlayabilirsiniz.

    ![Windows Server Yedekleme öğeleri](./media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > Merhaba makale nasıl toospecify hello yedekleme zamanlaması hakkında daha fazla bilgi için bkz: [kullanım Azure yedekleme tooreplace bant altyapınızın](backup-azure-backup-cloud-as-tape.md).
   >

8. Merhaba üzerinde **bekletme ilkesi seçin** sayfası, select hello **Bekletme İlkesi** hello yedek kopya.

    Merhaba bekletme ilkesi hello yedekleme verileri ne kadar süreyle depolanacağını belirtir. Tüm yedekleme noktaları için "sabit ilke" belirtmek yerine hello yedekleme gerçekleştiğinde göre farklı bekletme ilkeleri belirtebilirsiniz. Merhaba günlük, haftalık, aylık ve yıllık bekletme ilkeleri toomeet gereksinimlerinizi değiştirebilirsiniz.
9. Merhaba ilk yedekleme türünü seçin sayfasında hello ilk yedekleme türünü seçin. Merhaba seçeneği bırakın **hello ağ üzerinden otomatik olarak** seçili ve ardından **sonraki**.

    Otomatik olarak hello ağ üzerinden yedekleyebilir veya çevrimdışı yedekleme yapabilirsiniz. Bu makalenin sonraki bölümlerinde Hello otomatik olarak yedekleme hello işlemini açıklar. Çevrimdışı Yedekleme toodo tercih ederseniz, hello makalesini inceleyin [Azure backup'ta Çevrimdışı Yedekleme iş akışı](backup-azure-backup-import-export.md) ek bilgi için.
10. Merhaba onay sayfasında hello bilgileri gözden geçirin ve ardından **son**.
11. Merhaba Sihirbazı hello yedekleme zamanlamasını oluşturduktan sonra tıklayın **Kapat**.

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a>Dosya ve klasörleri ilk kez hello için tooback
1. Merhaba kurtarma Hizmetleri aracısında tıklatın **Şimdi Yedekle** toocomplete hello hello ağ üzerinden dengeli ilk.

    ![Windows Server şimdi yedekle](./media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. Merhaba onay sayfasında, Şimdi Yedekle sihirbazı hello hello ayarları gözden geçir hello makineyi tooback kullanır. Ardından **Yedekle**'ye tıklayın.
3. Tıklatın **Kapat** tooclose hello Sihirbazı. Merhaba Sihirbazı Hello yedekleme işlemi tamamlanmadan önce kapatırsanız, Başlangıç Sihirbazı'nı toorun hello arka planda devam eder.

Merhaba ilk Yedekleme tamamlandıktan sonra hello **işi tamamlandı** durum hello yedekleme konsolunda görüntülenir.

![IR tamamlandı](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a>Sorularınız mı var?
Sorularınız varsa veya herhangi bir özellik varsa dahil, toosee istediğiniz [Geri bildirimlerinizi bize gönderin](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Sonraki adımlar
* [Windows makinelerini yedekleme](backup-configure-vault.md) konusunda daha fazla bilgi edinin.
* Dosya ve klasörlerinizi yedeklediğinize göre artık [kasa ve sunucularınızı yönetebilirsiniz](backup-azure-manage-windows-server.md).
* Toorestore yedekleme ihtiyacınız varsa, bu makalede çok kullanmak[dosyaları tooa Windows makinesine geri](backup-azure-restore-windows-server.md).
