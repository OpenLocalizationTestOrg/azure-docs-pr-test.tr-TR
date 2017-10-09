---
title: "Azure Automation denetimi tümleştirmesinin aaaSource | Microsoft Docs"
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
ms.openlocfilehash: 6ceee1de8065fafe85a13bbd7f585e74dbc96b47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="source-control-integration-in-azure-automation"></a>Azure Otomasyonu’nda kaynak denetimi tümleştirmesi
Kaynak denetimi tümleştirmesi, Otomasyon hesabı tooa GitHub kaynak denetimi deponuza tooassociate runbook'larda sağlar. Kaynak denetimi tooeasily verir ekibinizle işbirliği, değişiklikleri izle ve runbook'larınızın tooearlier sürümlerini geri alma. Örneğin, kaynak denetimi geliştirme ortamı tooyour üretim Otomasyon test kolay toopromote kodu yapmak tooyour geliştirme, test veya üretim Automation hesapları, toosync farklı dallarda kaynak denetimi sağlar. hesabı.

Kaynak denetimi Azure Otomasyonu toosource denetim toopush koddan izin verir veya kaynak denetimi tooAzure Otomasyon, runbook'lardan çeker. Bu makalede nasıl tooset kaynağı kontrol Azure Otomasyonu ortamınızda açıklanmaktadır. Biz, GitHub deposunu Azure Otomasyonu tooaccess yapılandırarak başlatmak ve aracılığıyla yapılabilir farklı işlemlerini yol kaynak denetimi tümleştirmesi kullanılarak. 

> [!NOTE]
> Kaynak denetimi destekleyen çekme ve itme [PowerShell iş akışı runbook'ları](automation-runbook-types.md#powershell-workflow-runbooks) yanı [PowerShell runbook'ları](automation-runbook-types.md#powershell-runbooks). [Grafik runbook'lar](automation-runbook-types.md#graphical-runbooks) henüz desteklenmemektedir.<br><br>
> 
> 

Vardır, Automation hesabınız için iki basit adımları gerekli tooconfigure kaynak denetimi ve tek bir GitHub hesabınız zaten varsa. Bunlar:

## <a name="step-1--create-a-github-repository"></a>1. adım – GitHub depo oluşturma
GitHub hesabı ve istediğiniz bir depo zaten varsa toolink tooAzure Otomasyon sonra oturum açma tooyour var olan hesap ve aşağıdaki 2. adımdaki başlatın. Aksi takdirde, çok gidin[GitHub](https://github.com/), yeni bir hesap için kaydolun ve [yeni bir havuz oluşturma](https://help.github.com/articles/create-a-repo/).

## <a name="step-2--set-up-source-control-in-azure-automation"></a>Adım 2 – Azure Otomasyonu'nda kaynak denetimi ayarlama
1. Hello Azure portal'ın Hello Otomasyon hesabı dikey penceresinden tıklayın **kaynak denetimi ayarlayın.** 
   
    ![Kaynak denetimini Ayarla](media/automation-source-control-integration/automation_01_SetUpSourceControl.png)
2. Merhaba **kaynak denetimi** dikey penceresini açar, buradan GitHub hesabı ayrıntılarınızı yapılandırabilir. Parametreleri tooconfigure hello listesi aşağıdadır:  
   
   | **Parametre** | **Açıklama** |
   |:--- |:--- |
   | Kaynak Seç |Merhaba kaynağı seçin. Şu anda yalnızca **GitHub** desteklenir. |
   | Yetkilendirme |Merhaba tıklatın **Authorize** düğmesini toogrant Azure Otomasyonu erişim tooyour GitHub depo. Zaten farklı bir pencere GitHub hesabı tooyour kaydedilir ve yeniden hello o hesabın kimlik bilgileri kullanılır. Yetkilendirme başarılı olduktan sonra hello dikey GitHub kullanıcı adınızı altında gösterecektir **yetkilendirme özelliği**. |
   | Depo seçin |GitHub depo kullanılabilir depoları hello listeden seçin. |
   | Dal seçin |Bir dal kullanılabilir dalları hello listeden seçin. Yalnızca hello **ana** şube herhangi dalları oluşturmadıysanız, gösterilir. |
   | Runbook klasörü yolu |Merhaba runbook klasör yolu içinden toopush istediğiniz veya kodunuzu çekme hello GitHub deposunda hello yolunu belirtir. Merhaba biçimde girilmelidir **/KlasörAdı/altklasöradı**. Yalnızca runbook'lar hello runbook klasörü yolunda eşitlenen tooyour Otomasyon hesabı olacaktır. Merhaba runbook klasör yolu hello alt runbook'ları olacak **değil** işlemleri senkronize edilir. Kullanım  **/**  toosync tüm runbook'ları hello depo altında hello. |
3. Adlı depo varsa, örneğin, **PowerShellScripts** adlı bir klasör içeren **RootFolder**, adında bir klasör içeren **alt**. Her klasör düzeyinde dizeleri toosync aşağıdaki hello kullanabilirsiniz:
   
   1. toosync runbook'lardan **depo**, runbook klasör yolu*/*
   2. toosync runbook'lardan **RootFolder**, runbook klasör yolu */RootFolder*
   3. toosync runbook'lardan **alt**, runbook klasör yolu */RootFolder/alt*.
4. Merhaba parametreleri yapılandırdıktan sonra üzerinde hello görüntülendikleri **kaynak denetimini Ayarla dikey.**  
   
    ![Dikey yapılandırın](media/automation-source-control-integration/automation_02_SourceControlConfigure.png)
5. Tamam'ı sonra kaynak denetimi tümleştirmesinin Automation hesabınız için yapılandırılmıştır ve GitHub bilgilerinizle güncelleştirilmesi. Şimdi tıklayabilirsiniz bu bölümü tooview tüm kaynak denetimi iş geçmişi eşitleme.  
   
    ![Depo değerleri](media/automation-source-control-integration/automation_03_RepoValues.png)
6. Kaynak denetimini Ayarla sonra hello aşağıdaki Automation kaynaklarını Otomasyon hesabınızda oluşturulacak:  
   İki [değişken varlıkları](automation-variables.md) oluşturulur.  
   
   * Merhaba değişkeni **Microsoft.Azure.Automation.SourceControl.Connection** aşağıda gösterildiği gibi hello bağlantı dizesi, hello değerlerini içerir.  
     
     | **Parametre** | **Değer** |
     |:--- |:--- |
     | Ad |Microsoft.Azure.Automation.SourceControl.Connection |
     | Tür |Dize |
     | Değer |{"Şube":\<*şube adınızı*>, "RunbookFolderPath":\<*klasöründeki*>, "Sağlayıcı türü":\<*1'için ' e kadar bir değere sahip GitHub*>, "Depo":\<*deponuz adını*>, "Kullanıcıadı":\<*bilgisayarınızı GitHub kullanıcı adı*>} |

    * Merhaba değişkeni **Microsoft.Azure.Automation.SourceControl.OAuthToken**, güvenli şifrelenmiş değeri, OAuthToken hello içerir.  

    |**Parametre**            |**Değer** |
    |:---|:---|
    | Ad  | Microsoft.Azure.Automation.SourceControl.OAuthToken |
    | Tür | Unknown(Encrypted) |
    | Değer | <*Şifrelenmiş OAuthToken*> |  

    ![Değişkenler](media/automation-source-control-integration/automation_04_Variables.png)  

    * **Otomasyon kaynak denetimi** yetkili uygulama tooyour GitHub hesabı eklenir. tooview Merhaba uygulaması: tooyour GitHub giriş sayfasından gidin **profil** > **ayarları** > **uygulamaları**. Bu uygulama, GitHub depo tooan Automation hesabı Azure Otomasyonu toosync sağlar.  

    ![Git uygulama](media/automation-source-control-integration/automation_05_GitApplication.png)


## <a name="using-source-control-in-automation"></a>Kaynak denetimini otomasyon kullanma
### <a name="check-in-a-runbook-from-azure-automation-toosource-control"></a>Azure Otomasyonu toosource denetimini runbook iade etme
Runbook iade tooa runbook Azure Otomasyonu'nda kaynak denetimi deponuzun yaptığınız toopush hello değişiklikleri sağlar. Aşağıda bir runbook toocheck bileşenini hello adımlar şunlardır:

1. Otomasyon hesabınızdan [yeni metin biçiminde runbook oluşturma](automation-first-runbook-textual.md), veya [varolan, metinsel bir runbook'u düzenlemek](automation-edit-textual-runbook.md). Bu runbook'u bir PowerShell iş akışı veya PowerShell komut dosyası runbook olabilir.  
2. Runbook'unuzda düzenledikten sonra kaydetmeli ve tıklatın **iade** hello gelen **Düzenle** dikey.  
   
    ![İade etme düğmesi](media/automation-source-control-integration/automation_06_CheckinButton.png)

     > [!NOTE] 
     > Onay bileşeninden Azure Otomasyonu, kaynak denetiminde mevcut hello kod üzerine yazar. Merhaba Git eşdeğer komut satırı yönerge toocheck içinde olduğu **git Ekle + git işleme + git itme**  

1. Tıkladığınızda **iade**, bir onay iletisi istenir, Evet toocontinue'ı tıklatın.  
   
    ![İade etme iletisi](media/automation-source-control-integration/automation_07_CheckinMessage.png)
2. Başlatır hello kaynak denetimini runbook iade: **eşitleme MicrosoftAzureAutomationAccountToGitHubV1**. Bu runbook tooGitHub bağlanır ve değişiklikleri Azure Otomasyonu tooyour depodan iter. tooview hello iade iş geçmişi, toohello dönün **kaynak denetimi tümleştirmesinin** sekmesinde ve tooopen hello deposu eşitleme dikey tıklayın. Bu dikey tüm kaynak denetimi işi gösterir.  Tooview istediğiniz ve tooview hello detaylar hello işi seçin.  
   
    ![Runbook iade etme](media/automation-source-control-integration/automation_08_CheckinRunbook.png)
   
   > [!NOTE]
   > Kaynak denetimini runbook'ları görüntülemek veya düzenlemek silemeyeceğiniz özel Otomasyon çalışma kitabı ' dir. Bunlar, runbook listenizde gösterilmez, ancak işler listenizde gösteren eşitleme işlerini görürsünüz.
   > 
   > 
3. değişiklik hello runbook'un Hello adına bir giriş parametresi toohello iade runbook gönderilir. Yapabilecekleriniz [hello iş ayrıntılarını görüntüleyin](automation-runbook-execution.md#viewing-job-status-from-the-azure-portal) runbook'ta genişleterek **depo eşitleme** dikey.  
   
    ![CheckIn giriş](media/automation-source-control-integration/automation_09_CheckinInput.png)
4. Tooview hello değişiklikleri Hello işi tamamlandıktan sonra GitHub deposunu yenileyin.  Bir yürütme iletiyle deponuzun bir yürütme olmalıdır: **güncelleştirilmiş *Runbook adı* Azure Automation.**  

### <a name="sync-runbooks-from-source-control-tooazure-automation"></a>Kaynak denetimi tooAzure Otomasyon eşitleme runbook'lardan
Merhaba deposu eşitleme dikey penceresinde Hello Eşitle düğmesi toopull verir tüm runbook'ları, depo tooyour Otomasyon hesabı hello runbook klasörü yolunda hello. Merhaba aynı deponun bir Automation hesabı daha eşitlenen toomore olabilir. Aşağıda başlangıç adımları toosync bir runbook şunlardır:

1. Merhaba Hello ifadesini kaynak denetimini ayarladığınız Automation hesabını açın **kaynak denetimi tümleştirmesi/deposu eşitlemesi dikey** tıklatıp **eşitleme** ile onay istenir sonra ileti, tıklatın **Evet** toocontinue.  
   
    ![Eşitle düğmesi](media/automation-source-control-integration/automation_10_SyncButtonwithMessage.png)
2. Eşitleme hello runbook başlatır: **eşitleme MicrosoftAzureAutomationAccountFromGitHubV1**. Bu runbook tooGitHub bağlanır ve, depo tooAzure Otomasyon hello değişikliklerden çeker. Yeni bir iş üzerinde hello görmelisiniz **depo eşitleme** dikey penceresinde bu eylem için. Merhaba eşitleme işi, tooview ayrıntılarını tooopen hello iş ayrıntıları dikey penceresinde'ı tıklatın.  
   
    ![Eşitleme Runbook](media/automation-source-control-integration/automation_11_SyncRunbook.png)

    > [!NOTE] 
    > Kaynak denetiminden bir eşitleme hello Taslak sürümü şu anda Automation hesabınız için mevcut hello runbook'ların üzerine yazar **tüm** halen runbook'ları kaynak denetimi. Merhaba eşdeğer komut satırı yönerge toosync olan Git **git çekme**


## <a name="troubleshooting-source-control-problems"></a>Kaynak Denetim sorunlarını giderme
Herhangi bir giriş veya eşitleme işi hatalarla varsa hello iş durumu askıya alınması ve hello iş dikey penceresinde hello hata hakkında daha fazla bilgi görüntüleyebilirsiniz.  Merhaba **tüm günlükleri** bölümü gösterir, tüm bu işle ilişkili PowerShell akışları hello. Bu, hello ayrıntılarla iade veya Eşitleme sorunları düzeltmek toohelp gerekli sağlar. Bunu de gösterilir hello eşitleniyor veya bir runbook içindeki denetimi oluştu eylemlerin sırasını.  

![AllLogs görüntüsü](media/automation-source-control-integration/automation_13_AllLogs.png)

## <a name="disconnecting-source-control"></a>Kaynak denetiminin bağlantısı kesiliyor
GitHub hesabınızdan toodisconnect hello deposu eşitleme dikey açıp **Bağlantıyı Kes**. Kaynak denetiminin bağlantısını kesmek sonra daha önce eşitlenmiş olan runbook'ları hala Otomasyon hesabınızda kalır ancak hello deposu eşitleme dikey etkin olmayacak.  

  ![Bağlantıyı kesme düğmesi](media/automation-source-control-integration/automation_12_Disconnect.png)

## <a name="next-steps"></a>Sonraki adımlar
Kaynak denetimi tümleştirmesi hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:  

* [Azure Automation: Azure automation'da kaynak denetimi tümleştirmesi](https://azure.microsoft.com/blog/azure-automation-source-control-13/)  
* [Sık kullanılan kaynak denetim sisteminiz için oy verin](https://www.surveymonkey.com/r/?sm=2dVjdcrCPFdT0dFFI8nUdQ%3d%3d)  
* [Azure Otomasyonu: Runbook kaynak denetimine Visual Studio Team Services kullanarak tümleştirme](https://azure.microsoft.com/blog/azure-automation-integrating-runbook-source-control-using-visual-studio-online/)  

