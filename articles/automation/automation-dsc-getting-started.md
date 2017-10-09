---
title: "aaaGetting başlatılan Azure Otomasyonu DSC'ye | Microsoft Docs"
description: "Açıklama ve hello en yaygın görevleri de Azure Otomasyonu istenen durum yapılandırması (DSC) örnekleri"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a>Azure Otomasyonu DSC ile çalışmaya başlama
Bu konu, nasıl toodo hello ile Azure Otomasyonu istenen durum yapılandırması (oluşturma, alma ve yapılandırmaları, onboarding makineleri çok yönetmek, derleme ve raporları görüntüleme gibi DSC), en yaygın görevleri açıklar. Hangi Azure Otomasyonu DSC genel bir bakış için bkz: [Azure Automation DSC genel bakış](automation-dsc-overview.md). DSC belgeler için bkz: [Windows PowerShell istenen durum yapılandırması genel bakış](https://msdn.microsoft.com/PowerShell/dsc/overview).

Bu konu hakkında adım adım kılavuzu toousing Azure Otomasyonu DSC sağlar. Zaten bu konuda açıklanan başlangıç adımları uymadan ayarlanmış bir örnek ortamı istiyorsanız kullanabileceğiniz [hello ARM şablonu](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup). Bu şablon tamamlanmış bir Azure Otomasyonu DSC ortam, Azure Otomasyonu DSC tarafından yönetilen bir Azure VM dahil olmak üzere ayarlar.

## <a name="prerequisites"></a>Ön koşullar
Bu konudaki toocomplete hello örnekleri, hello aşağıdaki gereklidir:

* Azure Otomasyonu hesabı. Bir Azure Otomasyonu Garklı Çalıştır hesabı oluşturma yönergeleri için bkz. [Azure Farklı Çalıştır Hesabı](automation-sec-configure-azure-runas-account.md).
* Bir Azure Kaynak Yöneticisi'ni VM (Klasik değil) Windows Server 2008 R2 çalıştıran veya sonraki bir sürümü. Bir VM oluşturma ile ilgili yönergeler için bkz: [hello Azure portalında, ilk Windows sanal makine oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md)

## <a name="creating-a-dsc-configuration"></a>DSC yapılandırması oluşturma
Basit bir oluşturacağız [DSC Yapılandırması](https://msdn.microsoft.com/powershell/dsc/configurations) hello varlığının veya yokluğunun hello sağlar **Web sunucusu** Windows özelliği (düğümler nasıl atadığınız bağlı olarak IIS).

1. Windows PowerShell ISE Hello (veya herhangi bir metin düzenleyicisi) başlatın.
2. Metin aşağıdaki hello yazın:
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. Merhaba dosyası olarak kaydetmeniz `TestConfig.ps1`.

Bu yapılandırma bir kaynak her düğümü blok hello çağırır [WindowsFeature kaynak](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), hello varlığının veya yokluğunun hello sağlar **Web sunucusu** özelliği.

## <a name="importing-a-configuration-into-azure-automation"></a>Bir yapılandırma Azure Automation'a içeri aktarma
Ardından, biz Otomasyon hesabı hello hello yapılandırma aktaracaksınız.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.
3. Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC yapılandırmaları**.
4. Merhaba üzerinde **DSC yapılandırmaları** dikey penceresinde tıklatın **bir yapılandırma eklemek**.
5. Merhaba üzerinde **alma Yapılandırması** dikey penceresinde, Gözat toohello `TestConfig.ps1` dosyayı bilgisayarınıza.
   
    ![Ekran görüntüsü hello ** alma yapılandırma ** dikey penceresi](./media/automation-dsc-getting-started/AddConfig.png)
6. **Tamam** düğmesine tıklayın.

## <a name="viewing-a-configuration-in-azure-automation"></a>Azure Otomasyonu'nda bir yapılandırmayı görüntüleme
Bir yapılandırma içe aktardıktan sonra hello Azure portal görüntüleyebilirsiniz.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.
3. Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC yapılandırmaları**
4. Merhaba üzerinde **DSC yapılandırmaları** dikey penceresinde tıklatın **TestConfig** (Bu hello aldığınız hello yapılandırma hello önceki yordamda adıdır).
5. Merhaba üzerinde **TestConfig yapılandırma** dikey penceresinde tıklatın **yapılandırma kaynağı görüntüle**.
   
    ![Merhaba TestConfig yapılandırma dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    A **TestConfig yapılandırma kaynağı** hello PowerShell kodu hello yapılandırması için görüntüleme dikey penceresi açılır.

## <a name="compiling-a-configuration-in-azure-automation"></a>Bir Azure Otomasyonu yapılandırmasında derleme
İstenen durumu tooa düğümü uygulayabilmeniz için önce bu duruma tanımlama DSC yapılandırması bir veya daha fazla düğüm yapılandırmaları (MOF belge) derlenmiş ve gerekir Automation DSC çekme sunucusuna hello üzerinde yerleştirilir. Azure Otomasyonu DSC yapılandırmalarında derleme daha ayrıntılı açıklaması için bkz: [Azure Otomasyonu DSC yapılandırmalarında derleme](automation-dsc-compile.md). Derleme yapılandırmaları hakkında daha fazla bilgi için bkz: [DSC yapılandırmaları](https://msdn.microsoft.com/PowerShell/DSC/configurations).

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.
3. Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC yapılandırmaları**
4. Merhaba üzerinde **DSC yapılandırmaları** dikey penceresinde tıklatın **TestConfig** (Merhaba hello adı önceden aktarılmış yapılandırma).
5. Merhaba üzerinde **TestConfig yapılandırma** dikey penceresinde tıklatın **derleme**ve ardından **Evet**. Bu derleme işi başlatır.
   
    ![Derleme düğmesi vurgulama hello TestConfig yapılandırma dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> Bir Azure Otomasyonu yapılandırmasında derlerken herhangi oluşturulan düğümü yapılandırma MOF dosyalarından toohello çekme sunucusuna otomatik olarak dağıtır.
> 
> 

## <a name="viewing-a-compilation-job"></a>Derleme işi görüntüleme
Bir derleme başlattıktan sonra hello görüntüleyebilirsiniz **derleme işleri** döşeme hello **yapılandırma** dikey. Merhaba **derleme işleri** döşeme şu anda çalışan gösterir, tamamlandı ve işleri başarısız oldu. Bir derleme iş dikey penceresi açtığınızda, herhangi bir hata veya uyarı karşılaştı dahil olmak üzere bu iş hakkındaki bilgileri gösterir, giriş parametreleri hello yapılandırma ve derleme günlükleri kullanılan.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.
3. Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC yapılandırmaları**.
4. Merhaba üzerinde **DSC yapılandırmaları** dikey penceresinde tıklatın **TestConfig** (Merhaba hello adı önceden aktarılmış yapılandırma).
5. Merhaba üzerinde **derleme işleri** hello parçasına **TestConfig yapılandırma** dikey penceresinde, listelenen hello işlerin birini tıklatın. A **derleme işi** dikey penceresi açılır ve derleme işi hello hello tarihle etiketli başlatıldı.
   
    ![Merhaba derleme işi dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/CompilationJob.png)
6. Merhaba herhangi bir kutucuğu tıklayın **derleme işi** dikey toosee daha fazla hello işi hakkında ayrıntılar.

## <a name="viewing-node-configurations"></a>Düğüm yapılandırmaları görüntüleme
Derleme işi başarılı şekilde tamamlandığını bir veya daha fazla yeni düğüm yapılandırmaları oluşturur. Düğüm yapılandırması dağıtılan toohello çekme sunucu ve çekilen ve bir veya daha fazla düğüm tarafından uygulanan hazır toobe MOF belgedir. Otomasyon hesabınızda hello hello düğüm yapılandırmaları görüntüleyebileceği **DSC düğüm yapılandırmaları** dikey. Düğüm yapılandırması hello form ile bir ada sahip *ConfigurationName*. *NodeName*.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.
3. Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC düğüm yapılandırmaları**.
   
    ![Merhaba DSC düğüm yapılandırmaları dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a>Azure Otomasyonu DSC ile bir Azure VM yönetimi için hazırlanma
Azure Otomasyonu DSC toomanage Azure VM'ler (Klasik ve Resource Manager), şirket içi sanal makineleri, Linux makineler, AWS VM'ler ve şirket içi fiziksel makineleri kullanabilirsiniz. Bu konuda, biz kapak nasıl tooonboard yalnızca Azure Kaynak Yöneticisi Vm'leri. Ekleme hakkında bilgi için bkz: diğer türleri makine [Azure Otomasyonu DSC tarafından Yönetim için hazırlama makineler](automation-dsc-onboarding.md).

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a>Azure Otomasyonu DSC tarafından Yönetim için bir Azure Kaynak Yöneticisi'ni VM tooonboard
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.
3. Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC düğümleri**.
4. Merhaba, **DSC düğümleri** dikey penceresinde tıklatın **eklemek Azure VM**.
   
    ![Hello Azure VM Ekle düğmesi vurgulama hello DSC düğümleri dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/OnboardVM.png)
5. Merhaba, **eklemek Azure VM'ler** dikey penceresinde'ı tıklatın **seçin sanal makineleri tooonboard**.
6. Merhaba, **seçin VM'ler** dikey penceresinde, select hello tooonboard istediğiniz ve tıklatın VM **Tamam**.
   
   > [!IMPORTANT]
   > Bu Windows Server 2008 R2 çalıştıran bir Azure Kaynak Yöneticisi'ni VM olmalıdır veya sonraki bir sürümü.
   > 
   > 
7. Merhaba, **eklemek Azure VM'ler** dikey penceresinde tıklatın **kayıt verilerini yapılandırmak**.
8. Merhaba, **kayıt** dikey penceresinde hello adı girin hello içinde tooapply toohello VM istediğiniz hello düğüm yapılandırmasını **düğüm yapılandırma adı** kutusu. Bu Otomasyon hesabı hello düğümlü bir yapılandırmada hello adı tam olarak eşleşmelidir. Bu noktada sağlayan bir adı isteğe bağlıdır. Onboarding hello düğümü sonra atanan hello düğüm yapılandırmasını değiştirebilirsiniz.
   Denetleme **gerekirse düğümü yeniden**ve ardından **Tamam**.
   
    ![Merhaba kayıt dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/RegisterVM.png)
   
    Belirttiğiniz hello düğüm yapılandırması hello tarafından belirtilen aralıklarla uygulanan toohello VM olacaktır **yapılandırma modu sıklığı**, ve hello VM için güncelleştirmeleri toohello düğüm yapılandırması hellotarafındanbelirtilenaralıklarladenetleyecek **Yenileme sıklığı**. Bu değerleri nasıl kullanıldığı konusunda daha fazla bilgi için bkz: [yapılandırma hello yerel Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).
9. Merhaba, **eklemek Azure VM'ler** dikey penceresinde tıklatın **oluşturma**.

Azure ekleme hello VM hello işlemi başlar. Bu tamamlandığında hello VM hello görünecek **DSC düğümleri** dikey penceresinde hello Automation hesabı.

## <a name="viewing-hello-list-of-dsc-nodes"></a>DSC düğümleri Hello listesini görüntüleme
Otomasyon hesabınızda hello Yönetimi edildi kaldırılmış tüm makinelerin hello listesini görüntüleyebileceğiniz **DSC düğümleri** dikey.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.
3. Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC düğümleri**.

## <a name="viewing-reports-for-dsc-nodes"></a>DSC düğüm raporları görüntüleme
Azure Otomasyonu DSC yönetilen bir düğüm üzerinde tutarlılık denetimi gerçekleştirir her zaman hello düğüm durumu rapor geri toohello çekme sunucusuna gönderir. Merhaba dikey penceresinde bu düğüm için bu raporları görüntüleyebilirsiniz.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.
3. Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC düğümleri**.
4. Merhaba üzerinde **raporları** döşeme, herhangi bir hello listesinde hello Raporlar'ı tıklatın.
   
    ![Merhaba rapor dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/NodeReport.png)

Merhaba dikey penceresinde tek tek bir rapor, durum bilgisi hello karşılık gelen tutarlılık için aşağıdaki hello denetleyin görebilirsiniz:

* Merhaba rapor durumu — hello düğümdür "Uyumlu", "Başarısız" Merhaba yapılandırma ya da hello düğümdür "Uyumlu olmayan" (Merhaba düğümü olduğunda **applyandmonitor** modu ve hello makine istenen hello durumda değil).
* Merhaba tutarlılık denetimi için Hello başlangıç saati.
* Merhaba toplam çalışma zamanı hello tutarlılığını denetleyin.
* Tutarlılık Hello türünü kontrol edin.
* Merhaba hata kodu ve hata iletisi de dahil olmak üzere tüm hatalar. 
* Merhaba yapılandırması ve hello durumu (Merhaba düğümü bu kaynak için istenen hello durumunda olup) her bir kaynağın kullanılan DSC kaynakları — tıklayabilirsiniz her kaynak tooget daha ayrıntılı bilgi kaynağı için.
* Merhaba adı, IP adresi ve hello düğümünün yapılandırma modu.

Tıklatarak **görüntülemek ham rapor** toohello sunucu düğümü hello toosee hello gerçek verileri gönderir. Bu verileri kullanma hakkında daha fazla bilgi için bkz: [DSC rapor sunucusu kullanarak](https://msdn.microsoft.com/powershell/dsc/reportserver).

Merhaba ilk rapor kullanılabilir olmadan önce bir düğümü edildi sonra biraz zaman alabilir. Toowait too30 dakika yukarı hello ilk rapor için sonra yerleşik bir düğüm gerekebilir.

## <a name="reassigning-a-node-tooa-different-node-configuration"></a>Bir düğüm tooa farklı düğüm yapılandırması yeniden atama
Bir başlangıçta atanan hello daha farklı düğüm yapılandırması düğüme toouse atayabilirsiniz.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.
3. Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC düğümleri**.
4. Merhaba üzerinde **DSC düğümleri** dikey penceresinde hello adına tıklayın hello düğümünün tooreassign istiyor.
5. Bu düğüm için Hello dikey penceresinde **Ata düğümü**.
   
    ![Merhaba atamak düğüm düğmesini vurgulama hello düğümü dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/AssignNode.png)
6. Merhaba üzerinde **atamak düğüm yapılandırması** dikey penceresinde, tooassign hello düğümü istediğiniz ve ardından select hello düğüm yapılandırması toowhich **Tamam**.
   
    ![Merhaba atamak düğüm yapılandırması dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a>Bir düğümün kaydı silinirken
Azure Otomasyonu DSC tarafından yönetilen bir düğüm toobe artık istemiyorsanız kaydını kaldırabilirsiniz.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba Hub menüsünde **tüm kaynakları** ve ardından hello Otomasyon hesabınızın adını.
3. Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde tıklatın **DSC düğümleri**.
4. Merhaba üzerinde **DSC düğümleri** dikey penceresinde hello adına tıklayın hello düğümünün toounregister istiyor.
5. Bu düğüm için Hello dikey penceresinde **Unregister**.
   
    ![Merhaba Unregister düğmesi vurgulama hello düğümü dikey penceresinin ekran görüntüsü](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a>İlgili makaleler
* [Azure Otomasyonu DSC genel bakış](automation-dsc-overview.md)
* [Azure Otomasyonu DSC tarafından Yönetim için hazırlama makineler](automation-dsc-onboarding.md)
* [Windows PowerShell istenen durum yapılandırması genel bakış](https://msdn.microsoft.com/powershell/dsc/overview)
* [Azure Otomasyonu DSC cmdlet'leri](/powershell/module/azurerm.automation/#automation)
* [Azure Otomasyonu DSC fiyatlandırması](https://azure.microsoft.com/pricing/details/automation/)

