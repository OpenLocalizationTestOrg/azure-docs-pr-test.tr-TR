---
title: "Windows server ya da iş istasyonu tooAzure (Klasik modeli) ayarlama aaaBack | Microsoft Docs"
description: "Windows sunucularını veya istemcilerini tooa yedekleme kasasında Azure yedekleme. Dosya ve klasörleri tooa korumak için temel kavramları yedekleme Kasası'hello Azure yedekleme Aracısı'nı kullanma geçer."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "Yedekleme kasası; bir Windows server'ı Yedekle; Yedekleme pencereleri;"
ms.assetid: 3b543bfd-8978-4f11-816a-0498fe14a8ba
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: c8f2a9bed1e5885f5c272c65b9282ededc05850a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-workstation-tooazure-using-hello-classic-portal"></a>Merhaba Klasik portalı kullanarak bir Windows server ya da iş istasyonu tooAzure yedekleyin
> [!div class="op_single_selector"]
> * [Klasik portal](backup-configure-vault-classic.md)
> * [Azure portal](backup-configure-vault.md)
>
>

Bu makalede ortamınızı toofollow tooprepare gerekir ve bir Windows server'ı (ya da iş istasyonu) tooAzure geri hello yordamları açıklanmaktadır. Ayrıca Yedekleme çözümünüzün dağıtma konuları ele alınmaktadır. Azure Backup hello için ilk kez çalışırken düşünüyorsanız, bu makalede hızlı bir şekilde, hello işleminde size kılavuzluk eder.

Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: Resource Manager ve klasik. Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

## <a name="before-you-start"></a>Başlamadan önce
bir sunucu veya istemci tooAzure tooback, bir Azure hesabınızın olması gerekir. Yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.

## <a name="create-a-backup-vault"></a>Yedekleme kasası oluşturma
tooback dosya ve klasörleri bir sunucu veya istemci toocreate toostore hello verilerin istediğiniz hello coğrafi bölgede bir yedekleme kasası gerekir.

> [!IMPORTANT]
> Mart 2017'dan başlayarak, hello Klasik portal toocreate yedekleme kasaları artık kullanabilirsiniz.
>
> Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz. Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.<br/> **15 Ekim 2017**, artık mümkün toouse PowerShell toocreate yedekleme kasaları olacaktır. <br/> **1 Kasım 2017'den itibaren**:
>- Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.
>- Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır. Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.
>


## <a name="download-hello-vault-credential-file"></a>Merhaba kasa kimlik bilgilerini indirin
Merhaba şirket içi makineyi toobe veri tooAzure yedekleyebilirsiniz önce bir yedekleme kasası ile kimlik doğrulaması gerekir. Merhaba kimlik doğrulaması aracılığıyla gerçekleştirilir *kasa kimlik bilgileri*. Merhaba kasa kimlik bilgilerini hello Klasik Portalı'ndan güvenli bir kanal üzerinden indirilir. Merhaba sertifika özel anahtarına hello portalı veya hello hizmetinde kalmaz.

### <a name="toodownload-hello-vault-credential-file-tooa-local-machine"></a>toodownload hello kasa kimlik bilgileri dosyası tooa yerel makine
1. Merhaba sol gezinti bölmesinde **kurtarma Hizmetleri**ve ardından oluşturduğunuz hello yedekleme kasası seçin.

    ![IR tamamlandı](./media/backup-configure-vault-classic/rs-left-nav.png)
2. Merhaba hızlı başlangıç sayfasında, tıklatın **indirme kasa kimlik bilgileri**.

   Hello Klasik portal geçerli tarih yerine hello kasa adı ve hello bir bileşimini kullanarak bir kasa kimlik bilgisi oluşturur. Merhaba kasa kimlik bilgileri dosyası yalnızca hello kayıt iş akışı sırasında kullanılır ve 48 saat sonra süresi dolar.

   Merhaba kasa kimlik bilgilerini hello portalından indirilebilir.
3. Tıklatın **kaydetmek** toodownload hello kasa kimlik bilgileri dosya toohello yüklemeleri klasör hello yerel hesap. Öğesini de seçebilirsiniz **Kaydet** hello gelen **kaydetmek** menü toospecify hello kasa kimlik bilgileri dosyası için bir konum.

   > [!NOTE]
   > Merhaba kasa kimlik bilgilerini makinenizden erişilebilir bir konuma kaydedilir emin olun. Bir dosya paylaşımı veya Sunucu İleti Bloğu'depolanıyorsa hello izinleri tooaccess sahip olduğunuzu doğrulayın.
   >
   >

## <a name="download-install-and-register-hello-backup-agent"></a>İndirme, yükleme ve hello yedekleme aracısını kaydedin
Merhaba yedekleme kasası ve indirme hello kasa kimlik bilgileri dosyasını oluşturduktan sonra her Windows makinelerinizi bir aracı yüklü olmalıdır.

### <a name="toodownload-install-and-register-hello-agent"></a>toodownload, yükleme ve hello Aracısı kaydedin
1. Tıklatın **kurtarma Hizmetleri**ve ardından hello yedekleme kasası bir sunucuyla tooregister istediğinizi seçin.
2. Merhaba Aracısı Hello hızlı başlangıç sayfasında, tıklatın **aracısı için Windows Server veya System Center Data Protection Manager veya Windows İstemcisi**. Daha sonra **Kaydet**'e tıklayın.

    ![Aracı Kaydet](./media/backup-configure-vault-classic/agent.png)
3. Merhaba MARSagentinstaller.exe dosya indirdiği sonra tıklayın **çalıştırmak** (veya çift **MARSAgentInstaller.exe** kaydedilmiş hello konumdan).
4. Merhaba yükleme klasörü ve hello aracı için gerekli olan Önbellek klasörü seçin ve ardından **sonraki**. Belirttiğiniz hello önbellek konumu boş alan eşit tooat en az yüzde 5'hello yedekleme verilerini olması gerekir.
5. Merhaba varsayılan proxy ayarları aracılığıyla tooconnect toohello Internet devam edebilirsiniz.             Bir proxy sunucu tooconnect toohello Internet hello Proxy Yapılandırması sayfasında kullanırsanız, hello seçin **özel proxy ayarlarını kullan** onay kutusunu işaretleyin ve ardından hello proxy sunucusu ayrıntılarını girin. Doğrulanmış bir proxy kullanıyorsanız, hello kullanıcı adı ve parola ayrıntılarını girin ve ardından **sonraki**.
6. Tıklatın **yükleme** toobegin hello Aracısı yükleme. Merhaba Yedekleme aracısı, Windows PowerShell ve .NET Framework 4.5 (zaten yüklüyse) yükler toocomplete hello yükleme.
7. Merhaba Aracısı yüklendikten sonra tıklatın **tooRegistration devam** hello iş akışıyla toocontinue.
8. Merhaba kasa kimlik sayfasında, daha önce yüklediğiniz tooand select hello kasa kimlik bilgileri dosyasını bulun.

    Merhaba kasa kimlik bilgilerini yalnızca 48 saat hello portalından indirdiğiniz sonra geçerli olacaktır. Bir hatayla karşılaşırsanız (örneğin, "sağlanan dosyasının süresi dolmuş kasa kimlik bilgileri"), bu sayfa toohello Portalı'nda oturum açın ve hello kasa kimlik bilgilerini yeniden indirin.

    Bu hello kasa kimlik bilgilerini, hello Kurulum uygulama tarafından erişilebilen bir konumda kullanılabilir olduğundan emin olun. Erişim ile ilgili hatalarla karşılaşırsanız, hello kasa kimlik bilgileri dosyası tooa üzerinde geçici konuma aynı makine ve hello işlemi yeniden deneyin hello kopyalayın.

    "Sağlanan geçersiz kasa kimlik bilgileri"gibi bir kasa kimlik bilgileri hatayla karşılaşırsanız, hello dosyası bozulmuş veya yok sahip hello hello kurtarma hizmetiyle ilişkili son kimlik bilgileri. Yeni bir kasa kimlik bilgileri dosyası hello portalından indirme hello işlemi yeniden deneyin. Merhaba bir kullanıcı, bu hata ayrıca oluşabilir **indirme kasa kimlik bilgileri** seçeneğinde birkaç kez art arda. Bu durumda, yalnızca hello son kasa kimlik bilgilerini geçerli değil.
9. Merhaba şifreleme ayarları sayfasında, bir parola oluşturmak veya bir parola girin (en az 16 karakter ile). Güvenli bir yerde toosave hello parolayı unutmayın.
10. **Son**'a tıklayın. Merhaba sunucuyu Kaydetme Sihirbazı hello server yedekleme ile kaydeder.

    > [!WARNING]
    > Kaybeder veya hello parolayı unutursanız Microsoft hello yedekleme verilerini kurtarmanıza yardımcı olamaz. Sahip olduğunuz şifreleme parolası hello ve Microsoft kullandığınız hello parola görünürlüğe sahip değil. Bir kurtarma işlemi sırasında gerekli olacağı için hello dosyayı güvenli bir konuma kaydedin.
    >
    >

11. Merhaba şifreleme anahtarı ayarlandıktan sonra hello bırakın **Microsoft Azure kurtarma Hizmetleri Aracısı** seçili kutuyu işaretleyin ve ardından **Kapat**.

## <a name="complete-hello-initial-backup"></a>Tam hello ilk yedekleme
Merhaba ilk yedekleme iki anahtar görev içerir:

* Merhaba yedekleme zamanlaması oluşturma
* Dosya ve klasörleri hello için ilk kez yedekleme

Merhaba yedekleme İlkesi hello ilk Yedekleme tamamlandıktan sonra toorecover hello verilere ihtiyacınız varsa, kullanabileceğiniz yedekleme noktaları oluşturur. Merhaba yedekleme İlkesi bu tanımladığınız hello zamanlamaya göre yapar.

### <a name="tooschedule-hello-backup"></a>tooschedule hello yedekleme
1. Merhaba Microsoft Azure yedekleme Aracısı'nı açın. (Merhaba bırakılırsa otomatik olarak açılır **Microsoft Azure kurtarma Hizmetleri Aracısı** hello sunucuyu Kaydetme Sihirbazı kapatıldığında onay kutusunun.) Bunu, makinenizde **Microsoft Azure Backup** aramasını yaparak bulabilirsiniz.

    ![Hello Azure Backup aracısını başlatma](./media/backup-configure-vault-classic/snap-in-search.png)
2. Merhaba yedekleme aracı tıklatın **yedekleme zamanlaması**.

    ![Windows Server yedeklemesini zamanlama](./media/backup-configure-vault-classic/schedule-backup-close.png)
3. Merhaba üzerinde hello yedeklemeyi Zamanlama Sihirbazı sayfasında Başlarken, tıklatın **sonraki**.
4. Merhaba öğeleri seçin tooBackup sayfasında, tıklatın **öğeleri Ekle**.
5. Hello dosya ve klasörlerin tooback yedeklemek istediğiniz ve ardından seçin **Tamam**.
6. **İleri**’ye tıklayın.
7. Merhaba üzerinde **yedekleme zamanlamasını belirtin** sayfasında, hello belirtin **yedekleme zamanlaması** tıklatıp **sonraki**.

    Günlük (en fazla günde üç kez olmak üzere) veya haftalık yedeklemeler zamanlayabilirsiniz.

    ![Windows Server Yedekleme öğeleri](./media/backup-configure-vault-classic/specify-backup-schedule-close.png)

   > [!NOTE]
   > Merhaba makale nasıl toospecify hello yedekleme zamanlaması hakkında daha fazla bilgi için bkz: [kullanım Azure yedekleme tooreplace bant altyapınızın](backup-azure-backup-cloud-as-tape.md).
   >
   >

8. Merhaba üzerinde **bekletme ilkesi seçin** sayfası, select hello **Bekletme İlkesi** hello yedek kopya.

    Merhaba bekletme ilkesi hello yedeklemenin depolanacağı hello süresini belirtir. Yalnızca tüm yedekleme noktaları için "sabit ilke" belirtmek yerine, hello yedekleme gerçekleştiğinde göre farklı bekletme ilkeleri belirtebilirsiniz. Merhaba günlük, haftalık, aylık ve yıllık bekletme ilkeleri toomeet gereksinimlerinizi değiştirebilirsiniz.
9. Merhaba ilk yedekleme türünü seçin sayfasında hello ilk yedekleme türünü seçin. Merhaba seçeneği bırakın **hello ağ üzerinden otomatik olarak** seçili ve ardından **sonraki**.

    Otomatik olarak hello ağ üzerinden yedekleyebilir veya çevrimdışı yedekleme yapabilirsiniz. Bu makalenin sonraki bölümlerinde Hello otomatik olarak yedekleme hello işlemini açıklar. Çevrimdışı Yedekleme toodo tercih ederseniz, hello makalesini inceleyin [Azure backup'ta Çevrimdışı Yedekleme iş akışı](backup-azure-backup-import-export.md) ek bilgi için.
10. Merhaba onay sayfasında hello bilgileri gözden geçirin ve ardından **son**.
11. Merhaba Sihirbazı hello yedekleme zamanlamasını oluşturduktan sonra tıklayın **Kapat**.

### <a name="enable-network-throttling-optional"></a>Ağ (isteğe bağlı) azaltmayı etkinleştir
Merhaba Yedekleme aracısı, ağ azaltma sağlar. Veri aktarımı sırasında ağ bant genişliğinin nasıl kullanıldığını denetimleri azaltma. Bu denetim verileri tooback çalışma saatlerinde gerekir, ancak diğer Internet trafiği ile Merhaba yedekleme işlemi toointerfere istiyor musunuz yararlı olabilir. Azaltma yukarıya tooback uygular ve geri yükleme etkinlikleri.

**tooenable ağ azaltma**

1. Merhaba yedekleme aracı tıklatın **özelliklerini değiştirme**.

    ![Özelliklerini değiştir](./media/backup-configure-vault-classic/change-properties.png)
2. Merhaba üzerinde **azaltma** sekmesi, select hello **yedekleme işlemleri için Internet bant genişliği kullanımı daraltmayı etkinleştir** onay kutusu.

    ![Ağ azaltma](./media/backup-configure-vault-classic/throttling-dialog.png)
3. Azaltma etkinleştirdikten sonra sırasında yedek veri aktarımı için bant genişliği izin verilen hello belirtin **çalışma saatleri** ve **çalışılmayan saatler**.

    Merhaba bant genişliği değerler 512 kilobit / saniye (Kbps) başlar ve too1, 023 megabayt (MBps) saniyede yukarı gidebilirsiniz. Ayrıca hello başlangıç belirleyin ve için son **çalışma saatleri**, ve hello haftanın hangi günleri dikkate alınan iş günlerini. Belirtilen iş saatleri kabul dışında saat saat İş dışı.
4. **Tamam** düğmesine tıklayın.

### <a name="tooback-up-now"></a>tooback şimdi ayarlama
1. Merhaba yedekleme aracı tıklatın **Şimdi Yedekle** toocomplete hello hello ağ üzerinden dengeli ilk.

    ![Windows Server şimdi yedekle](./media/backup-configure-vault-classic/backup-now.png)
2. Merhaba onay sayfasında, Şimdi Yedekle sihirbazı hello hello ayarları gözden geçir hello makineyi tooback kullanır. Ardından **Yedekle**'ye tıklayın.
3. Tıklatın **Kapat** tooclose hello Sihirbazı. Merhaba yedekleme işlemi tamamlanmadan önce bunu yaparsanız, Başlangıç Sihirbazı'nı toorun hello arka planda devam eder.

Merhaba ilk Yedekleme tamamlandıktan sonra hello **işi tamamlandı** durum hello yedekleme konsolunda görüntülenir.

![IR tamamlandı](./media/backup-configure-vault-classic/ircomplete.png)

## <a name="next-steps"></a>Sonraki adımlar
* Kaydolun bir [ücretsiz Azure hesabı](https://azure.microsoft.com/free/).

Sanal makineler veya diğer iş yüklerini yedekleme hakkında ek bilgi için bkz:

* [Iaas Vm'lerini yedekleme](backup-azure-vms-prepare.md)
* [Microsoft Azure yedekleme sunucusu ile iş yüklerini tooAzure yedekleyin](backup-azure-microsoft-azure-backup.md)
* [DPM ile iş yüklerini tooAzure yedekleyin](backup-azure-dpm-introduction.md)
