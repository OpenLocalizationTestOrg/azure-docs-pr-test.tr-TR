---
title: "iş yükleri tooAzure portal yukarı aaaUse DPM tooback | Microsoft Docs"
description: "Bir giriş toobacking hello Azure Yedekleme hizmetini kullanarak DPM sunucularını ayarlama"
services: backup
documentationcenter: 
author: adigan
manager: nkolli
editor: 
keywords: "System Center Data Protection Manager, veri koruma Yöneticisi, dpm yedekleme"
ms.assetid: c8c322cf-f5eb-422c-a34c-04a4801bfec7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: 1dd988ae55012ac7dc485d2416458542c60b6ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a>DPM ile iş yüklerini tooAzure yukarı tooback hazırlama
> [!div class="op_single_selector"]
> * [Azure Backup Sunucusu](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure Backup sunucusu (Klasik)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (Klasik)](backup-azure-dpm-introduction-classic.md)
>
>

Bu makalede, System Center Data Protection Manager (DPM) sunucuları ve iş yükleri bir giriş toousing Microsoft Azure yedekleme tooprotect sağlar. Bunu okuyarak, anlamanız:

* Azure DPM sunucusu yedek nasıl çalışır
* Merhaba Önkoşullar tooachieve kesintisiz bir yedekleme deneyimi
* Merhaba tipik hatalarla karşılaşıldı ve nasıl onlarla toodeal
* Desteklenen senaryolar

> [!NOTE]
> Azure oluşturmak ve kaynaklarla çalışmak için iki dağıtım modeline sahiptir: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Resource Manager modelini kullanarak dağıtılan VM'ler geri yüklemek için hello bilgi ve yordamlar sağlar.
>
>

System Center DPM dosya ve uygulama verileri yedekler. TooDPM yedeklenen verileri diskte, bantta depolanan veya Microsoft Azure yedekleme ile tooAzure yedeklendi. DPM Azure Backup ile aşağıdaki gibi etkileşim kurar:

* **Fiziksel sunucu veya şirket içi sanal makine olarak dağıtılan DPM** — DPM fiziksel sunucu olarak veya geri veri tooa bir şirket içi Hyper-V sanal makinesi olarak dağıtılırsa, Kurtarma Hizmetleri ayrıca toodisk kasa'yı ve bant yedekleme.
* **Azure sanal makinesi olarak dağıtılan DPM** — güncelleştirme 3 ile System Center 2012 R2'den DPM Azure sanal makinesi olarak dağıtılabilir. DPM yapabilecekleriniz Azure sanal makinesi olarak dağıtılırsa geri veri tooAzure diskleri toohello DPM Azure sanal makinesine bağlı ya da kurtarma Hizmetleri kasası tooa yedekleyerek hello veri depolama boşaltabilir.

## <a name="why-backup-from-dpm-tooazure"></a>Neden DPM tooAzure yedekleme?
DPM sunucularını yedekleme için Azure Yedekleme'yi kullanarak hello iş avantajları şunlardır:

* Şirket içi DPM dağıtımı için bir alternatif toolong terim dağıtım tootape Azure kullanabilirsiniz.
* Azure'da DPM dağıtımları için Azure Backup, toooffload depolama hello Azure disk alanından tooscale yukarı eski verileri kurtarma Hizmetleri kasası ve disk üzerindeki yeni verileri depolayarak olanak tanıyan.

## <a name="prerequisites"></a>Ön koşullar
Azure Backup tooback DPM verilerini aşağıdaki gibi hazırlayın:

1. **Kurtarma Hizmetleri kasası oluşturma** — Azure portalında bir kasa oluşturun.
2. **Kasa kimlik bilgilerini indirme** — tooregister hello DPM sunucusu tooRecovery Hizmetleri kasası kullanan hello kimlik bilgilerini indirin.
3. **Hello Azure Yedekleme aracısı yükleme** — gelen Azure Backup, her DPM sunucusunda hello aracı yükleme.
4. **Merhaba sunucuyu kaydetmek** — kayıt hello DPM sunucusu tooRecovery Hizmetleri kasası.

### <a name="1-create-a-recovery-services-vault"></a>1. Kurtarma hizmetleri kasası oluşturma
Kasa toocreate bir kurtarma Hizmetleri:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Merhaba Hub menüsünde **Gözat** ve kaynakları hello listesinde yazın **kurtarma Hizmetleri**. Yazmaya başladığınızda, hello filtreleyecek girişinize bağlı. **Kurtarma Hizmetleri kasası** seçeneğine tıklayın.

    ![Kurtarma Hizmetleri Kasası oluşturma 1. adım](./media/backup-azure-dpm-introduction/open-recovery-services-vault.png)

    Merhaba kurtarma Hizmetleri kasalarının listesi görüntülenir.
3. Merhaba üzerinde **kurtarma Hizmetleri kasaları** menüsünde tıklatın **Ekle**.

    ![Kurtarma Hizmetleri Kasası oluşturma 2. adım](./media/backup-azure-dpm-introduction/rs-vault-menu.png)

    Merhaba kurtarma Hizmetleri kasası dikey penceresi açılır tooprovide isteyen bir **adı**, **abonelik**, **kaynak grubu**, ve **konumu**.

    ![Kurtarma Hizmetleri kasası oluşturma 5. adım](./media/backup-azure-dpm-introduction/rs-vault-attributes.png)
4. İçin **adı**, bir kolay ad tooidentify hello kasası girin. Merhaba adı toobe hello Azure aboneliği için benzersiz olmalıdır. 2 ila 50 karakterden oluşan bir ad yazın. Ad bir harf ile başlamalıdır ve yalnızca harf, rakam ve kısa çizgi içerebilir.
5. Tıklatın **abonelik** toosee hello kullanılabilir abonelik listesini. Hangi abonelik toouse emin değilseniz, hello varsayılan kullanın (veya önerilen) aboneliği. Ancak kuruluş hesabınızın birden çok Azure aboneliği ile ilişkili olması durumunda birden çok seçenek olacaktır.
6. Tıklatın **kaynak grubu** toosee hello kullanılabilir kaynak gruplarının listesini ya da tıklatın **yeni** toocreate yeni bir kaynak grubu. Kaynak grupları hakkında eksiksiz bilgiler için bkz. [Azure Resource Manager’a genel bakış](../azure-resource-manager/resource-group-overview.md)
7. Tıklatın **konumu** tooselect hello hello kasa için coğrafi bölgeyi.
8. **Oluştur**'a tıklayın. Oluşturulan toobe kurtarma Hizmetleri kasası hello için biraz zaman alabilir. Merhaba üst sağ alanında hello portal Hello durum bildirimlerini izleyin.
   Kasanız oluşturulduktan sonra hello Portalı'nda açılır.

### <a name="set-storage-replication"></a>Depolama Çoğaltmayı Ayarlama
Merhaba depolama çoğaltma seçeneği, coğrafi olarak yedekli depolama ve yerel olarak yedekli depolama arasında toochoose sağlar. Varsayılan olarak, kasanız coğrafi olarak yedekli depolamaya sahiptir. Bu, birincil yedeklemenizse hello seçenek kümesi toogeo yedekli depolama bırakın. Daha düşük dayanıklılık düzeyinde olan daha uygun maliyetli bir seçenek istiyorsanız yerel olarak yedekli depolamayı seçin. Daha fazla bilgi edinin [coğrafi olarak yedekli](../storage/common/storage-redundancy.md#geo-redundant-storage) ve [yerel olarak yedekli](../storage/common/storage-redundancy.md#locally-redundant-storage) hello Depolama Seçenekleri [Azure Storage Çoğaltmaya genel bakış](../storage/common/storage-redundancy.md).

tooedit hello depolama çoğaltma ayarı:

1. Kasa tooopen hello kasa panosu ve hello ayarları dikey seçin. Merhaba, **ayarları** dikey penceresi açılmazsa, tıklatın **tüm ayarları** hello kasa panosunda.
2. Merhaba üzerinde **ayarları** dikey penceresinde tıklatın **Yedekleme Altyapısı** > **yedekleme yapılandırması** tooopen hello **yedekleme yapılandırması** dikey. Merhaba üzerinde **yedekleme yapılandırması** dikey penceresinde kasanızı hello depolama çoğaltma seçeneğini seçin.

    ![Yedekleme kasalarının listesi](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    Merhaba kasanız için depolama seçeneğini belirledikten sonra hazır tooassociate hello VM hello kasası ile demektir. toobegin hello ilişkilendirme bulmak ve gerekir kaydetmek Azure sanal makineleri hello.

### <a name="2-download-vault-credentials"></a>2. Kasa kimlik bilgilerini indirme
Merhaba kasa kimlik bilgileri dosyası, her bir yedekleme kasası için hello portal tarafından oluşturulan bir sertifikadır. Merhaba portal sonra hello ortak anahtar toohello erişim denetimi Hizmeti'nden (ACS) yükler. Merhaba sertifikasının özel anahtarı Hello kullanılabilir toohello kullanıcı bir giriş hello makine kayıt iş akışı olarak belirtilmiş olan hello iş akışının parçası olarak yapılır. Bu hello makine toosend yedekleme verilerini tanımlanan tooan kasaya hello Azure Backup hizmeti kimliğini doğrular.

Merhaba kasa kimlik bilgileri yalnızca hello kayıt iş akışı sırasında kullanılır. Kasa kimlik bilgileri dosyasının gizliliğinin tehlikeye hello hello kullanıcının sorumluluk tooensure olur. Bir kullanıcının hello elinizde kalırsa hello kasa kimlik bilgileri dosyası diğer makinelere karşı kullanılan tooregister olabilir hello aynı kasası. Merhaba yedekleme verilerini toohello müşteriye ait olan bir parola kullanılarak şifrelenir gibi ancak var olan yedekleme verilerinin gizliliği tehlikeye giremez. toomitigate bu sorunu kasa kimlik bilgileri 48hrs tooexpire ayarlanır. Kez – herhangi bir sayıda hello bir kurtarma Hizmetleri kasa kimlik bilgilerini yükleyebilirsiniz, ancak yalnızca hello son kasa kimlik bilgilerini hello kayıt iş akışı sırasında geçerlidir.

Merhaba kasa kimlik bilgilerini hello Azure portal güvenli bir kanaldan aracılığıyla yüklenir. Hello Azure Backup hizmeti hello sertifikasının özel anahtarı Merhaba farkında değildir ve hello özel anahtarı hello portalı veya hello hizmetinde kalıcı yapılmaz. Aşağıdaki adımları toodownload hello kasa kimlik bilgileri dosyası tooa yerel makine hello kullanın.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Tooregister DPM makine istediğiniz açık kurtarma Hizmetleri kasası toowhich toowhich.
3. Varsayılan ayarlar dikey penceresi açılır. Kapalıysa, tıklayın **ayarları** kasa Panosu tooopen hello ayarları dikey. Ayarlar dikey penceresinde tıklayın **özellikleri**.

    ![Kasa dikey penceresini açma](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
4. Merhaba Özellikler sayfasında, tıklatın **karşıdan** altında **yedekleme kimlik**. Merhaba portal indirme için kullanılabilir hale hello kasa kimlik bilgilerini oluşturur.

    ![İndir](./media/backup-azure-dpm-introduction/vault-credentials.png)

Merhaba portal hello kasa adı ve hello geçerli tarih kullanan bir kasa kimlik bilgisi oluşturur. Tıklatın **kaydetmek** toodownload hello kasa kimlik bilgileri toohello Yerel hesabın indirmeleri klasör ya da hello Farklı Kaydet'i seçin hello kasa kimlik bilgileri için bir konum menü toospecify kaydedin. Oluşturulan hello dosya toobe tooa dakikadır yukarı olur.

### <a name="note"></a>Not
* Bu hello kasa kimlik bilgileri dosyası makinenizden erişilebilen bir konuma kaydedildiğinden emin olun. Bir dosya paylaşımı/SMB depolanıyorsa hello erişim izinlerini denetleyin.
* Merhaba kasa kimlik bilgileri dosyası yalnızca hello kayıt iş akışı sırasında kullanılır.
* Merhaba kasa kimlik bilgileri dosyası 48hrs sonra süresi dolar ve hello portalından indirilebilir.

### <a name="3-install-backup-agent"></a>3. Yedekleme aracısını yükleme
Hello Azure yedekleme kasası oluşturduktan sonra bir aracı her yedekleme veri ve uygulamaları sağlayan Windows makinelerinizi (Windows Server, Windows istemci, System Center Data Protection Manager sunucusu veya Azure yedekleme sunucusu makine) yüklü olmalıdır tooAzure.

1. Tooregister DPM makine istediğiniz açık kurtarma Hizmetleri kasası toowhich toowhich.
2. Varsayılan ayarlar dikey penceresi açılır. Kapalıysa, tıklayın **ayarları** tooopen hello ayarlar dikey penceresi. Ayarlar dikey penceresinde tıklayın **özellikleri**.

    ![Kasa dikey penceresini açma](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
3. Hello Ayarları sayfasında, tıklatın **karşıdan** altında **Azure Yedekleme aracısı**.

    ![İndir](./media/backup-azure-dpm-introduction/azure-backup-agent.png)

   Merhaba Aracısı yüklendikten sonra MARSAgentInstaller.exe toolaunch hello yükleme hello Azure yedekleme Aracısı'nın çift'yi tıklatın. Merhaba yükleme klasörü ve hello aracı için gereken geçici klasörü seçin. Belirtilen hello önbellek konumu hello yedekleme verilerini % 5'en az boş alan olması gerekir.
4. Bir proxy sunucu tooconnect toohello kullanırsanız, internet ' hello **Proxy Yapılandırması** ekranında, hello proxy sunucusu ayrıntılarını girin. Doğrulanmış bir proxy kullanıyorsanız, bu ekranda hello kullanıcı adı ve parola bilgilerinizi girin.
5. (Bu zaten mevcut değilse) hello Azure Yedekleme aracısı, .NET Framework 4.5 ve Windows PowerShell toocomplete hello yükleme yükler.
6. Merhaba Aracısı yüklendikten sonra **Kapat** hello penceresi.

   ![Kapat](../../includes/media/backup-install-agent/dpm_FinishInstallation.png)
7. çok**kayıt hello DPM sunucusu** toohello kasasına hello **Yönetim** sekmesi tıklatın üzerinde **çevrimiçi**. Ardından, seçin **kaydetmek**. Merhaba kaydetme Kurulum Sihirbazı açılır.
8. Bir proxy sunucu tooconnect toohello kullanırsanız, internet ' hello **Proxy Yapılandırması** ekranında, hello proxy sunucusu ayrıntılarını girin. Doğrulanmış bir proxy kullanıyorsanız, bu ekranda hello kullanıcı adı ve parola bilgilerinizi girin.

    ![Proxy yapılandırması](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Proxy.png)
9. Merhaba kasa kimlik bilgilerini ekranda, daha önce indirilen tooand select hello kasa kimlik bilgileri dosyası göz atın.

    ![Kasa kimlik bilgileri](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Credentials.jpg)

    Merhaba kasa kimlik bilgileri dosyası yalnızca 48 için geçerlidir (Merhaba portalından yüklendikten sonra) saat. Bu ekranda (örneğin "kasa kimlik bilgileri sağlanan dosyasının süresi doldu"), herhangi bir hatayla karşılaşırsanız oturum açma toohello Azure portal ve indirme hello kasa kimlik bilgileri dosyası yeniden.

    Merhaba Kurulum uygulama tarafından erişilebilen bir konumda bu hello kasa kimlik bilgileri dosyası kullanılabilir olduğundan emin olun. Karşılaşırsanız ilgili hatalar erişim, bu makinede hello kasa kimlik bilgileri dosyası tooa geçici konuma kopyalayın ve hello işlemi yeniden deneyin.

    Geçersiz kasa kimlik bilgileri hatayla karşılaşırsanız (örneğin, "geçersiz kasa sağlanan kimlik bilgileri") hello dosya bozuk veya değil sahip hello hello kurtarma hizmetiyle ilişkili son kimlik bilgileri. Yeni bir kasa kimlik bilgileri dosyası hello portalından indirme hello işlemi yeniden deneyin. Bu hata genellikle Hello kullanıcı üzerinde hello tıklarsa görülür **indirme kasa kimlik bilgileri** hello Azure portalında, art arda seçeneği. Bu durumda, yalnızca hello ikinci kasa kimlik bilgilerini geçerli değil.
10. toocontrol hello iş ve Merhaba, İş dışı saatler sırasında ağ bant genişliği kullanımını **azaltma ayarı** ekranında hello bant genişliği kullanım sınırlarını ayarlama ve hello iş tanımlayabilir ve saat İş dışı.

    ![Azaltma ayarı](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Throttling.png)
11. Merhaba, **kurtarma klasör ayarı** ekranında, hello klasörü hello dosyaları Azure'dan indirdiğiniz geçici olarak hazırlanmış için göz atın.

    ![Kurtarma klasör ayarı](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_RecoveryFolder.png)
12. Merhaba, **şifreleme ayarı** ekran, bir parola oluşturabilir veya bir parola (en fazla 16 karakter) girin. Güvenli bir yerde toosave hello parolayı unutmayın.

    ![Şifreleme](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Encryption.png)

    > [!WARNING]
    > Merhaba, parola kaybolur veya unutulursa; Microsoft, hello yedekleme verilerini kurtarmak yardımcı olamaz. Merhaba son kullanıcı hello şifreleme parolası sahibi ve Microsoft hello son kullanıcı tarafından kullanılan hello parola görünürlüğe sahip değil. Lütfen bir kurtarma işlemi sırasında gerekli olduğu gibi hello dosyayı güvenli bir konuma kaydedin.
    >
    >
13. Merhaba tıkladığınızda **kaydetmek** düğmesini tıklatın, hello makine başarıyla kaydettirildi toohello kasası ve olduğunuzda artık Azure tooMicrosoft yedekleme hazır toostart.
14. Data Protection Manager kullanırken hello tıklayarak hello kayıt iş akışı sırasında belirtilen hello ayarlarını değiştirebilir **yapılandırma** seçerek seçeneği **çevrimiçi** hello altında  **Yönetim** sekmesi.

## <a name="requirements-and-limitations"></a>Gereksinimleri (ve sınırlamaları)
* Bir fiziksel sunucuda veya System Center 2012 SP1 veya System Center 2012 R2'de yüklü bir Hyper-V sanal makinesi olarak DPM çalıştırıyor olabilir. System Center 2012 R2 ile en az çalışan Azure sanal makinesi olarak da çalışabilir DPM 2012 R2 güncelleştirme paketi 3 veya System Center 2012 R2 ile en az çalışan vmware'deki Windows sanal makine Güncelleştirme Paketi 5.
* System Center 2012 SP1 ile DPM çalıştırıyorsanız, güncelleştirme dökümü 2'yi System Center Data Protection Manager SP1 için yüklemeniz gerekir. Hello Azure Backup aracısını yüklemeden önce bu gereklidir.
* Merhaba DPM sunucusu sahip Windows PowerShell ve .net Framework 4.5 yüklü.
* DPM, yedekleme çoğu iş yükleri tooAzure yedekleyebilirsiniz. Bkz: desteklenen sahip bir tam listesi için Azure Backup hello aşağıdaki öğeleri destekler.
* Azure Yedekleme'de depolanan verileri hello "tootape Kopyala" seçeneğiyle kurtarılamıyor.
* Hello Azure Backup özelliği etkinleştirilmiş bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Hakkında bilgi edinin [Azure yedekleme fiyatlandırması](https://azure.microsoft.com/pricing/details/backup/).
* Azure Backup kullanılarak tooback yedeklemek istediğiniz hello sunucularda yüklü hello Azure Yedekleme aracısı toobe gerektirir. Her sunucu, kullanılabilir yerel boş depolama alanı olarak yedeklendiğinden hello verilerin hello boyutu % 5'en az olması gerekir. Örneğin, 100 GB veri yedekleme en az 5 GB boş alan hello karalama konumda gerektirir.
* Veri hello Azure kasası depolama depolanır. Hiçbir sınır toohello miktarda veri tooan Azure Backup kasasını yedekleyebilirsiniz yoktur ancak (örneğin sanal makine ya da veritabanı) veri kaynağının hello boyutunu 54400 GB aşan döndürmemelidir.

Bu dosya türlerini tooAzure yedeklemek için desteklenir:

* Şifrelenmiş (yalnızca tam yedeklemeler)
* Sıkıştırılmış (artımlı yedeklemeler desteklenir)
* Aralıklı (artımlı yedeklemeler desteklenir)
* Sıkıştırılmış ve aralıklı (aralıklı olarak kabul edilir)

Ve bu desteklenmez:

* Büyük küçük harfe duyarlı dosya sistemlerindeki sunucular desteklenmez.
* Sabit bağlantılar (atlanır)
* Yeniden ayrıştırma noktaları (atlanır)
* Şifrelenmiş ve sıkıştırılmış (atlanır)
* Şifrelenmiş ve aralıklı (atlanır)
* Sıkıştırılmış akış
* Aralıklı akış

> [!NOTE]
> Gelen System Center 2012 DPM SP1 ile başlayarak, Microsoft Azure Yedekleme'yi kullanarak DPM tooAzure tarafından korunan iş yüklerini yedekleme.
>
>
