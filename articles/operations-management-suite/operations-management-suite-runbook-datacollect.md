---
title: "Günlük analizi veri ile Azure Automation runbook aaaCollecting | Microsoft Docs"
description: "Adım adım öğretici, bir runbook hello OMS havuzunda günlük analizi göre Analiz için Azure Otomasyonu toocollect verilerde oluşturmada size yol göstermektedir."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a>Günlük analizi olarak toplamak ve bir Azure Otomasyonu runbook'u
Günlük analizi veri önemli miktarda bir çeşitli kaynaklardan dahil olmak üzere toplayabilirsiniz [veri kaynakları](../log-analytics/log-analytics-data-sources.md) aracılar üzerinde hem de [Azure'dan toplanan veriler](../log-analytics/log-analytics-azure-storage.md).  Toocollect veri ihtiyaç duyacağınız, bu standart kaynakları aracılığıyla erişilebilir değil ancak bir senaryo vardır.  Bu durumlarda, hello kullanabilirsiniz [HTTP veri toplayıcı API](../log-analytics/log-analytics-data-collector-api.md) herhangi bir REST API istemciden toowrite veri tooLog Analytics.  Ortak bir yöntem tooperform bu veri toplama Azure Otomasyonu'nda bir runbook kullanıyor.   

Bu öğreticide oluşturma ve bir Azure Otomasyonu toowrite veri tooLog Analytics runbook'ta zamanlama hello işlemi açıklanmaktadır.


## <a name="prerequisites"></a>Ön koşullar
Bu senaryo, Azure aboneliğinizde yapılandırılmış kaynakları aşağıdaki hello gerektirir.  Her ikisi de ücretsiz bir hesap olabilir.

- [Günlük analizi çalışma alanı](../log-analytics/log-analytics-get-started.md).
- [Azure Otomasyon hesabı](../automation/automation-offering-get-started.md).

## <a name="overview-of-scenario"></a>Senaryoya genel bakış
Bu öğretici için Otomasyon işleri hakkında bilgi toplar bir runbook yazacaksınız.  Azure Otomasyonu runbook'ları yazma ve komut dosyası hello Azure Otomasyon Düzenleyicisi'nde test tarafından başlayacaksınız şekilde PowerShell ile uygulanır.  Gerekli hello bilgi topladığınız doğrulayın sonra bu veri tooLog Analytics yazma ve hello özel veri türü doğrulayın.  Son olarak, düzenli aralıklarla bir zamanlama toostart hello runbook oluşturacaksınız.

> [!NOTE]
> Bu runbook olmadan Azure Otomasyonu toosend iş bilgi tooLog Analytics yapılandırabilirsiniz.  Bu senaryo birincil olarak kullanılan toosupport hello öğreticidir ve hello veri tooa test çalışma göndermeniz önerilir.  


## <a name="1-install-data-collector-api-module"></a>1. Veri Toplayıcı API modülünü yükleme
Her [hello HTTP veri toplayıcı API isteğinden](../log-analytics/log-analytics-data-collector-api.md#create-a-request) uygun şekilde biçimlendirilmiş olması gerekir ve bir authorization üstbilgisi ekleyin.  Bunu runbook'unuzda yapabilirsiniz ancak bu işlemi basitleştirir bir modül kullanarak gerekli kod hello miktarını düşürebilir.  Kullanabileceğiniz bir modül [OMSIngestionAPI Modülü](https://www.powershellgallery.com/packages/OMSIngestionAPI) hello PowerShell Galerisi içinde.

toouse bir [Modülü](../automation/automation-integration-modules.md) bir runbook'ta Otomasyon hesabınızda yüklenmelidir.  Aynı hesap ardından kullanabileceğiniz hello herhangi bir runbook hello hello modülünde işlevleri.  Yeni bir modül seçerek yükleyebilirsiniz **varlıklar** > **modülleri** > **bir modül Ekle** Otomasyon hesabınızda.  

tooyour Otomasyon hesabı doğrudan Bu öğretici için bu seçeneği kullanabilmeniz için hello PowerShell Galerisi, ancak Hızlı seçeneği toodeploy bir modül sağlar.  

![OMSIngestionAPI Modülü](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. Çok Git[PowerShell Galerisi](https://www.powershellgallery.com/).
2. Arama **OMSIngestionAPI**.
3. Tıklatın hello üzerinde **tooAzure Otomasyon dağıtmak** düğmesi.
4. Otomasyon hesabınızı seçin ve tıklatın **Tamam** tooinstall hello modülü.


## <a name="2-create-automation-variables"></a>2. Otomasyon değişkenleri oluşturma
[Otomasyon değişkenleri](..\automation\automation-variables.md) Otomasyon hesabınızda tüm runbook'lar tarafından kullanılan değerleri tutun.  Daha fazla runbook'ları olun toochange sağlayarak esnek düzenlemeden bu değerleri gerçek runbook hello. Her istekten hello HTTP veri toplayıcı API hello kimliği ve anahtarı hello OMS çalışma alanının gerektirir ve değişken varlıkları olan ideal toostore bu bilgileri.  

![Değişkenler](media/operations-management-suite-runbook-datacollect/variables.png)

1. Hello Azure portal, tooyour Otomasyon hesabı gidin.
2. Seçin **değişkenleri** altında **paylaşılan kaynakları**.
2. Tıklatın **değişken Ekle** ve hello aşağıdaki tablonun hello iki değişken oluşturun.

| Özellik | Çalışma alanı kimliği değeri | Çalışma alanı anahtarı değeri |
|:--|:--|:--|
| Ad | Workspaceıd | WorkspaceKey |
| Tür | Dize | Dize |
| Değer | Merhaba, günlük analizi çalışma alanının çalışma alanı kimliği yapıştırın. | Oturum Hello birincil veya ikincil anahtarı günlük analizi çalışma alanınızın yapıştırın. |
| Şifreli | Hayır | Evet |



## <a name="3-create-runbook"></a>3. Runbook oluşturma

Azure Otomasyonu, düzenlemek ve runbook'unuzu test hello portalında bir düzenleyici içerir.  Merhaba seçeneği toouse hello komut dosyası Düzenleyicisi toowork ile sahip [doğrudan PowerShell](../automation/automation-edit-textual-runbook.md) veya [grafik runbook oluşturma](../automation/automation-graphical-authoring-intro.md).  Bu öğreticide, bir PowerShell Betiği ile çalışır. 

![Runbook’u düzenleme](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. Tooyour Otomasyon hesabı gidin.  
2. Tıklatın **Runbook'lar** > **runbook Ekle** > **yeni bir runbook oluşturmak**.
3. Merhaba runbook ad için **toplama Otomasyon işleri**.  Merhaba runbook türü için **PowerShell**.
4. Tıklatın **oluşturma** toocreate hello runbook'u ve başlangıç hello Düzenleyici.
5. Merhaba runbook'a kod aşağıdaki hello kopyalayıp yeniden açın.  Merhaba betik toohello açıklamaları hello kod açıklaması için bakın.
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a>4. Runbook sınaması
Azure Otomasyonu içeren bir ortamda çok[runbook'unuzu test](../automation/automation-testing-runbook.md) yayımlamadan önce.  Merhaba runbook tarafından toplanan hello verileri incelemek ve onu tooLog yayımlamadan önce beklendiği gibi Analytics tooproduction Yazar doğrulayın. 
 
![Runbook sınaması](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. Tıklatın **kaydetmek** toosave hello runbook.
1. Tıklatın **Test bölmesi** hello test ortamında tooopen hello runbook.
3. Runbook parametreleri olduğundan, bunları istendiğinde tooenter değerlerini olduğunuz.  Hello hello kaynak grubunun adını girin ve hello Otomasyon, devam eden toocollect iş bilgilerinizin hesabı.
4. Tıklatın **Başlat** toohello hello runbook başlatın.
3. Merhaba runbook durumuyla başlayacak **sıraya alınan** çok geçmeden önce**çalıştıran**.  
3. Merhaba runbook ayrıntılı çıktıyı json biçiminde toplanan hello işleriyle görüntülemelidir.  Hiç iş listelenmiyorsa, ardından karşılaşılmış son bir saat hello hello automation hesabında oluşturulan iş yok.  Herhangi bir runbook hello automation hesabında başlatmayı deneyin ve hello test yeniden gerçekleştirin.
4. Merhaba çıktı hello hatalarını komutu tooLog Analytics sonrası göstermiyor emin olun.  İleti benzer toohello şunlara sahip olmanız.

    ![POST çıktı](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a>5. Günlük analizi kayıtlarını doğrulama
Merhaba runbook testi tamamlandı ve hello çıkış başarıyla alındı doğrulandı sonra hello kayıtları kullanılarak oluşturulan doğrulayabilirsiniz bir [günlük analizi günlük aramada](../log-analytics/log-analytics-log-searches.md).

![Günlük çıktısı](media/operations-management-suite-runbook-datacollect/log-output.png)

1. Hello Azure portal, günlük analizi çalışma alanınızı seçin.
2. Tıklayın **oturum arama**.
3. Komutu aşağıdaki türü hello `Type=AutomationJob_CL` ve hello arama düğmesini tıklatın. Merhaba kayıt türü hello komut dosyasında belirlenmezse _CL içerdiğine dikkat edin.  Bu, özel günlük türü olduğunu otomatik olarak eklenen toohello günlük türü tooindicate sonekidir.
4. Bu hello runbook beklendiği gibi çalıştığını gösteren döndürülen bir veya daha fazla kayıt görmeniz gerekir.


## <a name="6-publish-hello-runbook"></a>6. Merhaba runbook yayımlama
Bu hello runbook düzgün çalıştığını doğruladıktan sonra toopublish gerekir, üretim ortamında çalışması için.  Tooedit devam et ve hello yayımlanan sürümü değiştirmeden hello runbook'u test etme.  

![Runbook yayımlama](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. Tooyour Otomasyon hesabı döndür.
2. Tıklayın **Runbook'lar** seçip **toplama Otomasyon işleri**.
3. Tıklatın **Düzenle** ve ardından **yayımlama**.
4. Tıklatın **Evet** zaman toooverwrite hello daha önce istediğiniz sorulan tooverify yayımlanan sürümü.

## <a name="7-set-logging-options"></a>7. Günlüğe kaydetme seçeneklerini ayarlama 
Test için mümkün tooview olan [ayrıntılı çıktı](../automation/automation-runbook-output-and-messages.md#message-streams) hello komut dosyasında hello $VerbosePreference değişkenini ayarlamak için.  Üretim için tooview ayrıntılı çıktı istiyorsanız hello runbook tooset hello günlük özellikleri gerekir.  Bu öğreticide kullanılan hello runbook için bu tooLog Analytics gönderilen hello json verilerini görüntüler.

![Günlüğe kaydetme ve izleme](media/operations-management-suite-runbook-datacollect/logging.png)

1. Runbook'unuzda hello özelliklerinde seçin **günlüğe kaydetme ve izleme** altında **Runbook ayarlarını**.
2. Değiştirmek için hello ayar **ayrıntılı kayıtları günlüğe** çok**üzerinde**.
3. **Kaydet** düğmesine tıklayın.

## <a name="8-schedule-runbook"></a>8. Runbook zamanlama
Merhaba en yaygın şekilde toostart izleme verilerini toplayan bir runbook olan tooschedule, toorun otomatik olarak.  Oluşturarak bunu bir [Azure Otomasyonu zamanlama](../automation/automation-schedules.md) ve tooyour runbook ekleniyor.

![Runbook zamanlama](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. Runbook'unuzda Hello özelliklerinde seçin **zamanlamaları** altında **kaynakları**.
2. Tıklatın **bir zamanlama Ekle** > **bir zamanlama tooyour runbook bağlantı** > **yeni bir zamanlama oluşturmak**.
5. Merhaba zamanlama ve tıklatın değerlerini aşağıdaki hello türü **oluşturma**.

| Özellik | Değer |
|:--|:--|
| Ad | AutomationJobs saatlik |
| Başlatır | En az 5 dakika geçmiş geçerli saati hello saati seçin. |
| Yineleme | Yinelenen |
| Tekrarlamayı her | 1 saat |
| Kümesi süre sonu | Hayır |

Merhaba zamanlama oluşturulduktan sonra bu zamanlamayı hello runbook her başlatıldığında kullanılacak tooset hello parametre değerlerini gerekir.

6. Tıklatın **parametreleri yapılandırmak ve çalıştırma ayarlarını**.
7. Değerlerini doldurun, **ResourceGroupName** ve **AutomationAccountName**.
8. **Tamam** düğmesine tıklayın. 

## <a name="9-verify-runbook-starts-on-schedule"></a>9. Zamanlama runbook başlatır doğrulayın
Bir runbook başlatıldığında, her [bir iş oluşturulur](../automation/automation-runbook-execution.md) ve oturum herhangi bir çıktı.  Aslında, runbook hello aynı işleri toplama hello bunlar.  Merhaba hello zamanlama için başlangıç saatini geçtikten sonra hello runbook için hello işleri denetleyerek beklendiği gibi bu hello runbook başlatır doğrulayabilirsiniz.

![İşler](media/operations-management-suite-runbook-datacollect/jobs.png)

1. Runbook'unuzda Hello özelliklerinde seçin **işleri** altında **kaynakları**.
2. Her zaman hello runbook için iş listesini başlatıldığından görmeniz gerekir.
3. Merhaba işleri tooview birini ayrıntılarını tıklatın.
4. Tıklayın **tüm günlükleri** tooview hello günlükleri ve hello runbook'tan çıkış.
5. Toohello alt toofind bir giriş benzer toohello aşağıdaki görüntü kaydırın.<br>![Ayrıntılı](media/operations-management-suite-runbook-datacollect/verbose.png)
6. Bu girişinde'ı tıklatın tooview hello ayrıntılı tooLog Analytics gönderilen json verilerini.



## <a name="next-steps"></a>Sonraki adımlar
- Kullanım [Görünüm Tasarımcısı](../log-analytics/log-analytics-view-designer.md) görüntüleyen bir görünüm toocreate hello veri toohello günlük analizi deposu derledik.
- Runbook'unuzda paketini bir [yönetim çözümü](operations-management-suite-solutions-creating.md) toodistribute toocustomers.
- Daha fazla bilgi edinmek [günlük analizi](https://docs.microsoft.com/azure/log-analytics/).
- Daha fazla bilgi edinmek [Azure Otomasyonu](https://docs.microsoft.com/azure/automation/).
- Merhaba hakkında daha fazla bilgi [HTTP veri toplayıcı API](../log-analytics/log-analytics-data-collector-api.md).
