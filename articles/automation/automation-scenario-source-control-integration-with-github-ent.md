---
title: "aaaAzure GitHub kuruluş ile Otomasyon kaynak denetimi tümleştirmesi | Microsoft Docs"
description: "Nasıl Hello ayrıntılarını açıklayan Otomasyon runbook'ları kaynak denetimi için GitHub Kurumsal tooconfigure tümleştirmesi."
services: automation
documentationCenter: 
authors: mgoedtel
manager: jwhit
editor: 
ms.assetid: e01d817c-7d38-421c-adf5-647a4b526eb4
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: magoedte
ms.openlocfilehash: 915d36ccabb72fdee1dba663049a0b331249cd73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-github-enterprise"></a>Azure otomasyonu senaryosu - GitHub kuruluş ile Otomasyon kaynak denetimi tümleştirmesi

Otomasyon Otomasyon hesabı tooa GitHub kaynak denetimi deponuza tooassociate runbook'larda sağlayan kaynak denetimi tümleştirmesi, şu anda destekler.  Ancak, dağıtan müşteriler [GitHub Kurumsal](https://enterprise.github.com/home) toosupport kendi DevOps yöntemler, ayrıca toouse istediğiniz onu toomanage hello yaşam olan runbook'ları, geliştirilmiş tooautomate iş süreçlerini ve Hizmet Yönetimi işlemler.  

Bu senaryoda, veri merkezinizdeki karma Runbook çalışanı hello Azure Resource Manager modüllerini ve Git araçlarının yüklü olarak yapılandırılmış bir Windows bilgisayarı vardır.  Merhaba karma çalışanı makine hello yerel Git deposu kopyasını sahiptir.  Merhaba runbook hello karma çalışanı üzerinde çalıştırdığınızda, hello Git dizin eşitlenir ve hello runbook dosyası içeriği Otomasyon hesabı hello alınır.

Bu makalede nasıl tooset bu yapılandırma, Azure Automation ortamınızdaki ayarlama. Merhaba güvenlik kimlik bilgileri ile Otomasyon yapılandırarak başlatmak, runbook'ları toosupport bu senaryo gerekli ve karma Runbook çalışanı verilerinizde dağıtımını toorun hello runbook'ları merkezi ve GitHub Kurumsal depo toosynchronize erişim Otomasyon hesabınızı runbook'larla.  


## <a name="getting-hello-scenario"></a>Merhaba senaryo alma

Bu senaryo doğrudan hello alabileceğiniz iki PowerShell runbook'ları oluşur [Runbook Galerisi](automation-runbook-gallery.md) de Azure portal hello veya indirme hello [PowerShell Galerisi](https://www.powershellgallery.com).

### <a name="runbooks"></a>Runbook'lar

Runbook | Açıklama| 
--------|------------|
Dışarı aktarma RunAsCertificateToHybridWorker | Merhaba çalışan runbook'ları ile Azure sipariş tooimport runbook'larda Otomasyon hesabı hello doğrulanabilmesi Runbook Otomasyon hesabı tooa karma çalışanı RunAs sertifika verir.| 
Eşitleme LocalGitFolderToAutomationAccount | Runbook eşitlemeler hello karma makinede yerel Git klasörü hello ve ardından hello runbook dosyaları (*.ps1) hello Otomasyon dikkate alın.|

### <a name="credentials"></a>Kimlik Bilgileri

Kimlik Bilgisi | Açıklama|
-----------|------------|
GitHRWCredential | Kimlik bilgisi varlığı izinleri toohello karma çalışanı ile toocontain hello kullanıcı adı ve bir kullanıcı için parola oluşturun.|

## <a name="installing-and-configuring-this-scenario"></a>Bu senaryoyu yükleme ve yapılandırma

### <a name="prerequisites"></a>Ön koşullar

1. Merhaba eşitleme LocalGitFolderToAutomationAccount runbook kimliğini doğrulayan hello kullanarak [Azure farklı çalıştır hesabı](automation-sec-configure-azure-runas-account.md). 

2. Microsoft Operations Management Suite (OMS) çalışma hello etkinleştirilmiş ve yapılandırılmış bir Azure Otomasyonu çözüm ile de gereklidir.  Merhaba Otomasyon kullanılan hesap tooinstall ile ilişkili olan ve bu senaryoyu yapılandırmak bir yoksa, oluşturulur ve hello yürüttüğünüzde sizin için yapılandırılmış **yeni OnPremiseHybridWorker.ps1** hello karma betikten runbook worker.        

    > [!NOTE]
    > Şu anda hello aşağıdaki bölgeler yalnızca Otomasyon OMS ile-tümleştirmeyi **Avustralya Güneydoğu**, **Doğu ABD 2**, **Güneydoğu Asya**, ve **Batı Avrupa**. 

3. Bir adanmış karma Runbook de hello GitHub yazılım barındırmak ve hello runbook dosyaları korumak çalışan hizmet verebilir bir bilgisayar (*runbook*.ps1) hello dosya sistemi toosynchronize GitHub arasında bir kaynak dizininde ve Otomasyon hesabı.

### <a name="import-and-publish-hello-runbooks"></a>Alma ve yayımlama hello runbook'ları

tooimport hello *verme RunAsCertificateToHybridWorker* ve *eşitleme LocalGitFolderToAutomationAccount* hello Runbook Galerisi hello Azure portal, Otomasyon hesabınızdaki runbook'lardan Merhaba yordamları izleyin [hello Runbook Galerisi alma Runbook'tan](automation-runbook-gallery.md#to-import-a-runbook-from-the-runbook-gallery-with-the-azure-portal). Otomasyon hesabınızda başarıyla içeri aktarıldıktan sonra hello runbook'ları yayımlayın.

### <a name="deploy-and-configure-hybrid-runbook-worker"></a>Dağıtma ve karma Runbook çalışanı yapılandırma

Veri merkezinizde zaten dağıtılmış bir karma Runbook çalışanı yoksa hello gereksinimleri gözden geçirmeli ve hello yordamda kullanarak otomatik hello yükleme adımları [Azure Otomasyon karma Runbook çalışanları - otomatikleştirmek yükleyin ve yapılandırma](automation-hybrid-runbook-worker.md#automated-deployment).  Bir bilgisayarda hello karma çalışanı başarıyla yüklendikten sonra gerçekleştirme adımları toocomplete yapılandırma toosupport bu senaryo hello.

1. Toohello bilgisayar barındırma hello karma Runbook çalışanı rolü yerel yönetici haklarına sahip bir hesapla oturum açın ve bir dizin toohold hello Git runbook dosyaları oluşturun.  Merhaba iç Git deposu toohello dizinine kopyalayın.
2. Önceden oluşturulmuş bir farklı çalıştır hesabı yok veya bu amaç için adanmış yeni bir tane toocreate istiyorsanız hello Azure portal tooAutomation hesapları gidin, Otomasyon hesabınızı seçin ve oluşturma bir [kimlik bilgisi varlığı](automation-credentials.md) , Merhaba kullanıcı adı ve izinleri toohello karma çalışanı olan bir kullanıcı parolasını içerir.  
3. Otomasyon hesabınızdan [hello runbook'u düzenlemek](automation-edit-textual-runbook.md)**verme RunAsCertificateToHybridWorker** ve hello hello değişkeninin değerini değiştirme *$Password* güçlü bir ile parola.    Merhaba değeri değiştirdikten sonra tıklatın **Yayımla** toohave hello runbook'un taslak sürümünü hello yayımlanan. 
5. Merhaba runbook'u başlatmak **verme RunAsCertificateToHybridWorker**ve hello **Runbook'u Başlat** hello seçeneği altında dikey **çalışma ayarları** hello seçeneğini belirleyin**Karma çalışanı** ve daha önce oluşturduğunuz bu senaryo için hello aşağı açılan listesinde seçin hello karma çalışanı grubu.  

    Merhaba çalışan runbook'ları sipariş toomanage hello farklı çalıştır Bağlantısı'nı kullanarak Azure ile Azure kaynaklarında (Bu senaryo - alma runbook'lar toohello Otomasyon hesabı için belirli) doğrulanabilmesi Bu sertifika toohello karma çalışanı dışa aktarır.

4. Otomasyon hesabınızdan seçin hello karma çalışanı grubu daha önce oluşturduğunuz ve [bir RunAs hesabı belirtin](automation-hrw-run-runbooks.md#runas-account) hello karma çalışanı grubu ve seçtiğiniz hello kimlik bilgisi varlığı yalnızca veya zaten oluşturdunuz.  Başka bir sağlar, bu hello eşitleme runbook Git komutları çalıştırabilirsiniz. 
5. Merhaba runbook'u başlatmak **eşitleme LocalGitFolderToAutomationAccount**, hello aşağıdaki gerekli giriş parametresi değerleri sağlayın ve hello **Runbook'u Başlat** hello seçeneği altında dikey **çalıştırın ayarları** hello seçeneğini belirleyin **karma çalışanı** ve hello aşağı açılan listesinde seçin hello karma çalışanı grubu daha önce oluşturduğunuz bu senaryo için:
    * *Kaynak grubu* - hello Otomasyon hesabınızla ilişkili kaynak grubunun adı
    * *AutomationAccountName* - hello Automation hesabınızın adı
    * *GitPath* - hello yerel klasör veya dosya hello toopull en son değişiklikleri Yukarı Git ayarlandığı karma Runbook çalışanı üzerinde

    Merhaba yerel Git klasörü hello karma çalışan bilgisayarda eşitleme ve hello kaynak dizin toohello Otomasyon hesabı hello .ps1 dosyaları içeri aktarın.

    ![Eşitleme LocalGitFolderToAutomationAccount Runbook başlatın](media/automation-scenario-source-control-integration-with-github-ent/start-runbook-synclocalgitfoldertoautoacct.png)<br>

7. Hello seçerek hello runbook için iş Özet ayrıntıları görüntüleyin **Runbook'lar** dikey penceresinde, Automation hesabı ve ardından hello **işleri** döşeme.  Tamamlanmış başarıyla hello seçerek onaylayın **tüm günlükleri** döşeme ve gözden geçirme hello ayrıntılı günlük akışı.  

## <a name="next-steps"></a>Sonraki adımlar

-  runbook türleri, avantajları ve sınırlamaları, hakkında daha fazla tooknow bakın [Azure Automation runbook türleri](automation-runbook-types.md)
-  PowerShell betik desteği özelliği hakkında daha fazla bilgi için bkz. [Azure Automation’da Yerel PowerShell betik desteği](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)
