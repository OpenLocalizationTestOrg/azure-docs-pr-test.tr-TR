---
title: "Dosya ve klasörleri aaaUse Azure Yedekleme aracısı tooback | Microsoft Docs"
description: "Windows dosya ve klasörleri tooAzure yukarı Hello Microsoft Azure Yedekleme aracısı tooback kullanın. Kurtarma Hizmetleri kasası oluşturma, hello yedekleme aracısını yüklemek, hello yedekleme ilkenizi tanımlayın ve hello dosyalar ve klasörler üzerinde hello ilk yedeklemeyi çalıştırın."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "Yedekleme kasası; bir Windows server'ı Yedekle; Yedekleme pencereleri;"
ms.assetid: 7f5b1943-b3c1-4ddb-8fb7-3560533c68d5
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: be203c24841971872b5c6e7cf260a2fa5c58ac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-client-tooazure-using-hello-resource-manager-deployment-model"></a>Merhaba Resource Manager dağıtım modelini kullanarak bir Windows Server ya da istemci tooAzure yedekleyin
> [!div class="op_single_selector"]
> * [Azure portal](backup-configure-vault.md)
> * [Klasik portal](backup-configure-vault-classic.md)
>
>

Bu makalede, Resource Manager dağıtım modeli kullanarak Azure Backup ile tooback, Windows Server (veya Windows istemcisi) dosya ve klasörleri tooAzure hello nasıl açıklanmaktadır.

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Yedekleme işlemi adımları](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a>Başlamadan önce
bir sunucu veya istemci tooAzure tooback, bir Azure hesabınızın olması gerekir. Yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.

## <a name="create-a-recovery-services-vault"></a>Kurtarma Hizmetleri kasası oluşturma
Kurtarma Hizmetleri kasası tüm hello yedeklemeleri ve zaman içinde oluşturduğunuz kurtarma noktalarını depolayan bir varlıktır. Hello kurtarma Hizmetleri kasası ayrıca hello uygulanan yedekleme ilkesini toohello korumalı dosyaları ve klasörleri içerir. Kurtarma Hizmetleri kasası oluşturduğunuzda, aynı zamanda hello uygun depolama artıklığı seçeneği işaretlemeniz gerekir.

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


### <a name="set-storage-redundancy"></a>Küme depolama artıklığı
Bir Kurtarma Hizmetleri kasasını ilk oluşturduğunuzda depolamanın nasıl çoğaltılacağını belirlersiniz.

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

Bir kasa oluşturduğunuza göre indirme ve hello Microsoft Azure kurtarma Hizmetleri aracısını yükleyerek, kasa kimlik bilgilerini indirme ve bu kimlik bilgileri tooregister hello aracısını kullanarak, altyapı tooback dosya ve klasörleri hazırlama Merhaba kasası.

## <a name="configure-hello-vault"></a>Merhaba kasası yapılandırma

1. Açık kurtarma Hizmetleri kasası dikey (Merhaba kasa), yeni oluşturduğunuz, hello Başlarken bölümünde Merhaba, tıklatın **yedekleme**, sonra da hello **yedekleme ile çalışmaya başlama** dikey penceresinde, select  **Yedekleme hedefi**.

  ![Yedekleme hedefi dikey penceresini açma](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  Merhaba **yedekleme hedefi** dikey pencere açılır. Kurtarma Hizmetleri kasası hello önceden yapılandırılmışsa, ardından hello **yedekleme hedefi** dikey pencere açılır tıkladığınızda **yedekleme** hello kurtarma Hizmetleri kasası dikey penceresi.

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

Makine/proxy Internet erişimi sınırlı hello makine/proxy üzerinde güvenlik duvarı ayarlarını aşağıdaki URL'lere yapılandırılmış tooallow hello olduğundan emin olun: <br>
    1. www.msftncsi.com
    2. *.Microsoft.com
    3. *.WindowsAzure.com
    4. *.microsoftonline.com
    5. *.windows.ne


## <a name="create-hello-backup-policy"></a>Merhaba yedekleme ilkesi oluşturma
Kurtarma noktaları alınır ve hello kurtarma noktalarının bekletileceği süre hello hello yedekleme İlkesi hello zamanlamadır. Merhaba Microsoft Azure Yedekleme aracısı toocreate hello yedekleme ilkesinin dosya ve klasörler için kullanın.

### <a name="toocreate-a-backup-schedule"></a>toocreate bir yedekleme zamanlaması
1. Merhaba Microsoft Azure yedekleme Aracısı'nı açın. Bunu, makinenizde **Microsoft Azure Backup** aramasını yaparak bulabilirsiniz.

    ![Hello Azure Backup aracısını başlatma](./media/backup-configure-vault/snap-in-search.png)
2. Merhaba yedekleme aracısının içinde **Eylemler** bölmesinde tıklatın **yedekleme zamanlaması** toolaunch hello yedeklemeyi Zamanlama Sihirbazı.

    ![Windows Server yedeklemesini zamanlama](./media/backup-configure-vault/schedule-first-backup.png)

3. Merhaba üzerinde **Başlarken** hello yedeklemeyi Zamanlama Sihirbazı sayfasını tıklatın **sonraki**.
4. Merhaba üzerinde **öğeleri seçin tooBackup** sayfasında, **öğeleri Ekle**.

  Merhaba öğeleri seçin iletişim kutusu açılır.

5. Merhaba dosyalar ve klasörler tooprotect istediğiniz ve ardından seçin **Tamam**.
6. Merhaba, **öğeleri seçin tooBackup** sayfasında, **sonraki**.
7. Merhaba üzerinde **yedekleme zamanlamasını belirtin** sayfasında, hello yedekleme zamanlamasını ve tıklatın belirtin **sonraki**.

    Günlük (en fazla günde üç kez olmak üzere) veya haftalık yedeklemeler zamanlayabilirsiniz.

    ![Windows Server Yedekleme öğeleri](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > Merhaba makale nasıl toospecify hello yedekleme zamanlaması hakkında daha fazla bilgi için bkz: [kullanım Azure yedekleme tooreplace bant altyapınızın](backup-azure-backup-cloud-as-tape.md).
   >
   >

8. Merhaba üzerinde **bekletme ilkesi seçin** sayfasında hello belirli bekletme ilkeleri hello hello yedek kopya seçin ve tıklayın **sonraki**.

    Merhaba bekletme ilkesi hangi hello yedekleme depolanan hello süresini belirtir. Yalnızca tüm yedekleme noktaları için "sabit ilke" belirtmek yerine, hello yedekleme gerçekleştiğinde göre farklı bekletme ilkeleri belirtebilirsiniz. Merhaba günlük, haftalık, aylık ve yıllık bekletme ilkeleri toomeet gereksinimlerinizi değiştirebilirsiniz.
9. Merhaba ilk yedekleme türünü seçin sayfasında hello ilk yedekleme türünü seçin. Merhaba seçeneği bırakın **hello ağ üzerinden otomatik olarak** seçili ve ardından **sonraki**.

    Otomatik olarak hello ağ üzerinden yedekleyebilir veya çevrimdışı yedekleme yapabilirsiniz. Bu makalenin sonraki bölümlerinde Hello otomatik olarak yedekleme hello işlemini açıklar. Çevrimdışı Yedekleme toodo tercih ederseniz, hello makalesini inceleyin [Azure backup'ta Çevrimdışı Yedekleme iş akışı](backup-azure-backup-import-export.md) ek bilgi için.
10. Merhaba onay sayfasında hello bilgileri gözden geçirin ve ardından **son**.
11. Merhaba Sihirbazı hello yedekleme zamanlamasını oluşturduktan sonra tıklayın **Kapat**.

### <a name="enable-network-throttling"></a>Ağ azaltmayı etkinleştir
Merhaba Microsoft Azure Yedekleme aracısı, ağ azaltma sağlar. Veri aktarımı sırasında ağ bant genişliğinin nasıl kullanıldığını denetimleri azaltma. Bu denetim verileri tooback çalışma saatlerinde gerekir, ancak diğer Internet trafiği ile Merhaba yedekleme işlemi toointerfere istiyor musunuz yararlı olabilir. Azaltma yukarıya tooback uygular ve geri yükleme etkinlikleri.

> [!NOTE]
> Ağ azaltma (hizmet paketleri ile) Windows Server 2008 R2 SP1, Windows Server 2008 SP2 veya Windows 7 üzerinde kullanılabilir değil. özellik azaltma hello Azure Backup ağ hizmet kalitesi (QoS) hello yerel işletim sisteminde ilgilenir. Azure Backup bu işletim sistemlerini korumak için de, QoS bu platformlarda kullanılabilir hello sürümü Azure Backup ağ azaltma ile çalışmaz. Ağ azaltma kullanılabilir tüm diğer bağlı [desteklenen işletim sistemleri](backup-azure-backup-faq.md).
>
>

**tooenable ağ azaltma**

1. Merhaba Microsoft Azure yedekleme aracı tıklatın **özelliklerini değiştirme**.

    ![Özelliklerini değiştir](./media/backup-configure-vault/change-properties.png)
2. Merhaba üzerinde **azaltma** sekmesi, select hello **yedekleme işlemleri için Internet bant genişliği kullanımı daraltmayı etkinleştir** onay kutusu.

    ![Ağ azaltma](./media/backup-configure-vault/throttling-dialog.png)
3. Azaltma etkinleştirdikten sonra sırasında yedek veri aktarımı için bant genişliği izin verilen hello belirtin **çalışma saatleri** ve **çalışılmayan saatler**.

    Merhaba bant genişliği değerler 512 kilobit / saniye (Kbps) başlar ve too1, 023 megabayt (MBps) saniyede yukarı gidebilirsiniz. Ayrıca hello başlangıç belirleyin ve için son **çalışma saatleri**, ve hello haftanın hangi günleri dikkate alınan iş günlerini. Belirtilen iş saatleri kabul dışında saat saat İş dışı.
4. **Tamam** düğmesine tıklayın.

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a>Dosya ve klasörleri ilk kez hello için tooback
1. Merhaba yedekleme aracısını içinde tıklatın **Şimdi Yedekle** toocomplete hello hello ağ üzerinden dengeli ilk.

    ![Windows Server şimdi yedekle](./media/backup-configure-vault/backup-now.png)
2. Merhaba onay sayfasında, Şimdi Yedekle sihirbazı hello hello ayarları gözden geçir hello makineyi tooback kullanır. Ardından **Yedekle**'ye tıklayın.
3. Tıklatın **Kapat** tooclose hello Sihirbazı. Merhaba yedekleme işlemi tamamlanmadan önce bunu yaparsanız, Başlangıç Sihirbazı'nı toorun hello arka planda devam eder.

Merhaba ilk Yedekleme tamamlandıktan sonra hello **işi tamamlandı** durum hello yedekleme konsolunda görüntülenir.

![IR tamamlandı](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a>Sorularınız mı var?
Sorularınız varsa veya herhangi bir özellik varsa dahil, toosee istediğiniz [Geri bildirimlerinizi bize gönderin](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Sonraki adımlar
Sanal makineler veya diğer iş yüklerini yedekleme hakkında ek bilgi için bkz:

* Dosya ve klasörlerinizi yedeklediğinize göre artık [kasa ve sunucularınızı yönetebilirsiniz](backup-azure-manage-windows-server.md).
* Toorestore yedekleme ihtiyacınız varsa, bu makalede çok kullanmak[dosyaları tooa Windows makinesine geri](backup-azure-restore-windows-server.md).
