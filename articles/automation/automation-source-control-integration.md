---
title: "Kaynak denetimi tümleştirmesi Azure Automation | Microsoft Docs"
description: "Bu makalede, Azure automation'da GitHub ile kaynak denetimi tümleştirme açıklanmaktadır."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 224d7375-9887-44dd-b137-06ffe396a4b4
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 763bf5805e3a3cb95ad63c7a354dd3d4cd531b2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="source-control-integration-in-azure-automation"></a>Azure Otomasyonu’nda kaynak denetimi tümleştirmesi
Kaynak denetimi tümleştirmesinin Automation hesabınız GitHub kaynak denetim deponuza runbook'larda ilişkilendirmenizi sağlar. Kaynak denetimi kolayca ekibinizle işbirliği, değişiklikleri izlemek ve runbook'larınızın önceki sürümleri geri sağlar. Örneğin, kaynak denetimi geliştirme ortamınızda Otomasyon üretim test kodu Yükselt kolaylaşır, geliştirme, test veya üretim Automation hesapları, kaynak denetimine farklı dallarda eşitleme sağlar hesabı.

Kaynak denetimi, kod kaynak denetimi için Azure Otomasyon anında ya da kaynak denetiminden larınızın Azure otomasyonu için çekme olanak sağlar. Bu makalede, Azure Automation ortamınızdaki kaynak denetimi ayarlama açıklar. Biz, GitHub deposuna erişmek ve aracılığıyla yapılabilir farklı işlemlerini yol için Azure Otomasyonu yapılandırarak başlatır kaynak denetimi tümleştirmesi kullanılarak. 

> [!NOTE]
> Kaynak denetimi destekleyen çekme ve itme [PowerShell iş akışı runbook'ları](automation-runbook-types.md#powershell-workflow-runbooks) yanı [PowerShell runbook'ları](automation-runbook-types.md#powershell-runbooks). [Grafik runbook'lar](automation-runbook-types.md#graphical-runbooks) henüz desteklenmemektedir.<br><br>
> 
> 

GitHub hesabı zaten varsa, Automation hesabınız ve yalnızca bir kaynak denetimini yapılandırmak için gerekli iki basit adım vardır. Bunlar:

## <a name="step-1--create-a-github-repository"></a>1. adım – GitHub depo oluşturma
GitHub hesabı ve Azure Otomasyonu sonra oturum açma varolan hesabınıza bağlamak ve aşağıdaki 2. adımdaki başlatmak istediğiniz bir depo zaten varsa. Aksi takdirde gidin [GitHub](https://github.com/), yeni bir hesap için kaydolun ve [yeni bir havuz oluşturma](https://help.github.com/articles/create-a-repo/).

## <a name="step-2--set-up-source-control-in-azure-automation"></a>Adım 2 – Azure Otomasyonu'nda kaynak denetimi ayarlama
1. Azure Portalı'nda Automation hesabı dikey penceresinden tıklayın **kaynak denetimi ayarlayın.** 
   
    ![Kaynak denetimini Ayarla](media/automation-source-control-integration/automation_01_SetUpSourceControl.png)
2. **Kaynak denetimi** dikey penceresini açar, buradan GitHub hesabı ayrıntılarınızı yapılandırabilir. Yapılandırılacak parametrelerin listesi aşağıdadır:  
   
   | **Parametre** | **Açıklama** |
   |:--- |:--- |
   | Kaynak Seç |Bir kaynak seçin. Şu anda yalnızca **GitHub** desteklenir. |
   | Yetkilendirme |Tıklatın **Authorize** düğmesi, GitHub deposunu Azure Otomasyonu erişim vermek için. Zaten başka bir pencerede GitHub hesabınızda oturum açtıysanız, bu hesabı kimlik bilgileri kullanılır. Yetkilendirme başarılı olduktan sonra dikey GitHub kullanıcı adınızı altında gösterecektir **yetkilendirme özelliği**. |
   | Depo seçin |GitHub depo kullanılabilir depoları listeden seçin. |
   | Dal seçin |Bir dal kullanılabilir dalları listeden seçin. Yalnızca **ana** şube herhangi dalları oluşturmadıysanız, gösterilir. |
   | Runbook klasörü yolu |Runbook klasörü yolu İtme veya kodunuzu çekmek istediğiniz GitHub deposunda yolunu belirtir. Şu biçimde girilmelidir **/KlasörAdı/altklasöradı**. Yalnızca runbook klasör yolu runbook Otomasyon hesabınızı senkronize edilir. Runbook klasör yolunun alt klasörlerdeki runbook'ları olacak **değil** işlemleri senkronize edilir. Kullanım  **/**  depo altındaki tüm runbook'lar eşitlenecek. |
3. Adlı depo varsa, örneğin, **PowerShellScripts** adlı bir klasör içeren **RootFolder**, adında bir klasör içeren **alt**. Her klasör düzeyinde eşitlemek için aşağıdaki dizelerini kullanabilirsiniz:
   
   1. Eşitleme runbook'lardan için **depo**, runbook klasör yolu*/*
   2. Eşitleme runbook'lardan için **RootFolder**, runbook klasör yolu */RootFolder*
   3. Eşitleme runbook'lardan için **alt**, runbook klasör yolu */RootFolder/alt*.
4. Parametreleri yapılandırdıktan sonra bunlar üzerinde görüntülenir **kaynak denetimini Ayarla dikey.**  
   
    ![Dikey yapılandırın](media/automation-source-control-integration/automation_02_SourceControlConfigure.png)
5. Tamam'ı sonra kaynak denetimi tümleştirmesinin Automation hesabınız için yapılandırılmıştır ve GitHub bilgilerinizle güncelleştirilmesi. Kaynak denetimi eşitlemesi iş geçmişini görüntülemek için bu bölümü artık tıklatabilirsiniz.  
   
    ![Depo değerleri](media/automation-source-control-integration/automation_03_RepoValues.png)
6. Kaynak denetimini Ayarla sonra aşağıdaki Automation kaynaklarını Otomasyon hesabınızda oluşturulacak:  
   İki [değişken varlıkları](automation-variables.md) oluşturulur.  
   
   * Değişkeni **Microsoft.Azure.Automation.SourceControl.Connection** aşağıda gösterildiği gibi bağlantı dizesi değerlerini içerir.  
     
     | **Parametre** | **Değer** |
     |:--- |:--- |
     | Ad |Microsoft.Azure.Automation.SourceControl.Connection |
     | Tür |Dize |
     | Değer |{"Şube":\<*şube adınızı*>, "RunbookFolderPath":\<*klasöründeki*>, "Sağlayıcı türü":\<*1'için ' e kadar bir değere sahip GitHub*>, "Depo":\<*deponuz adını*>, "Kullanıcıadı":\<*bilgisayarınızı GitHub kullanıcı adı*>} |

    * Değişkeni **Microsoft.Azure.Automation.SourceControl.OAuthToken**, sizin OAuthToken güvenli şifreli değerini içerir.  

    |**Parametre**            |**Değer** |
    |:---|:---|
    | Ad  | Microsoft.Azure.Automation.SourceControl.OAuthToken |
    | Tür | Unknown(Encrypted) |
    | Değer | <*Şifrelenmiş OAuthToken*> |  

    ![Değişkenler](media/automation-source-control-integration/automation_04_Variables.png)  

    * **Otomasyon kaynak denetimi** GitHub hesabınızda yetkili bir uygulama olarak eklenir. Uygulamayı görüntülemek için: GitHub giriş sayfasından gidin, **profil** > **ayarları** > **uygulamaları**. Bu uygulama bir Otomasyon hesabı GitHub deponuza eşitlemek Azure Otomasyonu sağlar.  

    ![Git uygulama](media/automation-source-control-integration/automation_05_GitApplication.png)


## <a name="using-source-control-in-automation"></a>Kaynak denetimini otomasyon kullanma
### <a name="check-in-a-runbook-from-azure-automation-to-source-control"></a>Azure Otomasyonu runbook kaynak denetimine iade etme
Runbook iade kaynak denetimi deponuzun Azure Automation runbook yapmış olduğunuz değişiklikleri anında olanak sağlar. Bir runbook'u iade adımları aşağıda verilmiştir:

1. Otomasyon hesabınızdan [yeni metin biçiminde runbook oluşturma](automation-first-runbook-textual.md), veya [varolan, metinsel bir runbook'u düzenlemek](automation-edit-textual-runbook.md). Bu runbook'u bir PowerShell iş akışı veya PowerShell komut dosyası runbook olabilir.  
2. Runbook'unuzda düzenledikten sonra kaydetmeli ve tıklatın **iade** gelen **Düzenle** dikey.  
   
    ![İade etme düğmesi](media/automation-source-control-integration/automation_06_CheckinButton.png)

     > [!NOTE] 
     > Onay bileşeninden Azure Otomasyonu, kaynak denetiminde var olan kodu üzerine yazar. İade Git eşdeğer komut satırı yönergesi olup **git Ekle + git işleme + git itme**  

1. Tıkladığınızda **iade**, bir onay iletisi istenir, devam etmek için Evet'i tıklatın.  
   
    ![İade etme iletisi](media/automation-source-control-integration/automation_07_CheckinMessage.png)
2. Kaynak denetimini runbook başlatır iade: **eşitleme MicrosoftAzureAutomationAccountToGitHubV1**. Bu runbook için GitHub bağlanır ve değişiklikleri deponuza Azure Otomasyon iter. İade iş geçmişini görüntülemek için geri dönüp **kaynak denetimi tümleştirmesinin** sekmesine ve depo eşitleme dikey penceresini açmak için tıklayın. Bu dikey tüm kaynak denetimi işi gösterir.  Görüntülemek istediğiniz ve ayrıntılarını görüntülemek için tıklatın işi seçin.  
   
    ![Runbook iade etme](media/automation-source-control-integration/automation_08_CheckinRunbook.png)
   
   > [!NOTE]
   > Kaynak denetimini runbook'ları görüntülemek veya düzenlemek silemeyeceğiniz özel Otomasyon çalışma kitabı ' dir. Bunlar, runbook listenizde gösterilmez, ancak işler listenizde gösteren eşitleme işlerini görürsünüz.
   > 
   > 
3. Değiştirilen runbook'un adına iade runbook giriş parametresi olarak gönderilir. Yapabilecekleriniz [iş ayrıntılarını görüntüleme](automation-runbook-execution.md#viewing-job-status-from-the-azure-portal) runbook'ta genişleterek **depo eşitleme** dikey.  
   
    ![CheckIn giriş](media/automation-source-control-integration/automation_09_CheckinInput.png)
4. Değişiklikleri görüntülemek için iş tamamlandıktan sonra GitHub deposunu yenileyin.  Bir yürütme iletiyle deponuzun bir yürütme olmalıdır: **güncelleştirilmiş *Runbook adı* Azure Automation.**  

### <a name="sync-runbooks-from-source-control-to-azure-automation"></a>Azure otomasyonu için kaynak denetiminden eşitleme runbook'lar
Depo eşitleme dikey Eşitle düğmesi, tüm runbook'ları deponuz runbook klasörü yolunda Automation hesabınız için çekme olanak sağlar. Aynı deponun birden fazla Automation hesabına eşitlenmiş. Bir runbook eşitlemek için adımları aşağıda verilmiştir:

1. Kaynak denetimini ayarladığınız Otomasyon hesabından **kaynak denetimi tümleştirmesi/deposu eşitlemesi dikey** tıklatıp **eşitleme** ile onay istenir sonra ileti, tıklatın **Evet** devam etmek için.  
   
    ![Eşitle düğmesi](media/automation-source-control-integration/automation_10_SyncButtonwithMessage.png)
2. Eşitleme runbook başlatır: **eşitleme MicrosoftAzureAutomationAccountFromGitHubV1**. Bu runbook için GitHub bağlanır ve değişiklikleri Azure Otomasyonu, depodan çeker. Yeni bir iş görmeniz gerekir **depo eşitleme** dikey penceresinde bu eylem için. Eşitleme işi hakkındaki ayrıntıları görüntülemek için iş ayrıntılarını dikey penceresini açmak için tıklatın.  
   
    ![Eşitleme Runbook](media/automation-source-control-integration/automation_11_SyncRunbook.png)

    > [!NOTE] 
    > Kaynak denetiminden bir eşitleme Automation hesabınız için şu anda mevcut runbook'ları taslak sürümünü üzerine yazar **tüm** halen runbook'ları kaynak denetimi. Eşitleme için Git eşdeğer komut satırı yönerge olduğu **git çekme**


## <a name="troubleshooting-source-control-problems"></a>Kaynak Denetim sorunlarını giderme
Herhangi bir giriş veya eşitleme işi hatalarla varsa iş durumu askıya alınması ve iş dikey penceresinde hata hakkında daha fazla bilgi görüntüleyebilirsiniz.  **Tüm günlükleri** bölümü, bu işle ilişkili tüm PowerShell akışlar, gösterir. Bu size, iade veya eşitleme herhangi bir sorun gidermenize yardımcı olmak için gerekli ayrıntıları sağlar. Bu ayrıca, eşitleme veya bir runbook içindeki denetimi oluştu eylemlerin sırasını gösterir.  

![AllLogs görüntüsü](media/automation-source-control-integration/automation_13_AllLogs.png)

## <a name="disconnecting-source-control"></a>Kaynak denetiminin bağlantısı kesiliyor
GitHub hesabınızdan bağlantısını kesmek için depo eşitleme dikey penceresini açın ve **Bağlantıyı Kes**. Kaynak denetiminin bağlantısını kesmek sonra daha önce eşitlenmiş olan runbook'ları hala Otomasyon hesabınızda kalır ancak havuz eşitleme dikey etkin olmayacak.  

  ![Bağlantıyı kesme düğmesi](media/automation-source-control-integration/automation_12_Disconnect.png)

## <a name="next-steps"></a>Sonraki adımlar
Kaynak denetimi tümleştirmesi hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:  

* [Azure Automation: Azure automation'da kaynak denetimi tümleştirmesi](https://azure.microsoft.com/blog/azure-automation-source-control-13/)  
* [Sık kullanılan kaynak denetim sisteminiz için oy verin](https://www.surveymonkey.com/r/?sm=2dVjdcrCPFdT0dFFI8nUdQ%3d%3d)  
* [Azure Otomasyonu: Runbook kaynak denetimine Visual Studio Team Services kullanarak tümleştirme](https://azure.microsoft.com/blog/azure-automation-integrating-runbook-source-control-using-visual-studio-online/)  

