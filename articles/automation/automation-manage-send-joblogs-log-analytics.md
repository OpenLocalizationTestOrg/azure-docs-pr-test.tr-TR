---
title: "Azure Otomasyonu işi veri tooOMS günlük analizi aaaForward | Microsoft Docs"
description: "Bu makalede, nasıl tooMicrosoft Operations Management Suite günlük analizi toodeliver ek bilgiler ve yönetim toosend iş durumu ve runbook iş akışları gösterilmektedir."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: c12724c6-01a9-4b55-80ae-d8b7b99bd436
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/2017
ms.author: magoedte
ms.openlocfilehash: e78b6c6677d6502711ce828e2d32b7a91922ae26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="forward-job-status-and-job-streams-from-automation-toolog-analytics-oms"></a>İş durumu ve iş akışları Otomasyon tooLog analizi (OMS) iletme
Otomasyon runbook iş durumu ve iş akışları tooyour Microsoft Operations Management Suite (OMS) günlük analizi çalışma alanı gönderebilirsiniz.  İş günlüğe kaydeder ve iş akışları hello Azure portalında görünür olması veya PowerShell ile tek tek işler ve bu tooperform basit araştırmalar sağlar. Şimdi günlük analizi ile şunları yapabilirsiniz:

* Otomasyon işleriniz hakkında bilgi edinme
* Bir e-posta veya uyarı (örneğin, başarısız veya askıya alınmış), runbook işi durumlarına dayalı tetikleyici
* Gelişmiş sorgular, iş akışları yazma
* İşlerini Automation hesaplarında ilişkilendirmek
* İş Geçmişi zaman içinde görselleştirin     

## <a name="prerequisites-and-deployment-considerations"></a>Önkoşulları ve dağıtım hakkında önemli noktalar
Automation'ınızı gönderme toostart tooLog Analytics günlükleri, gereksinim duyduğunuz:

1. Kasım 2016 hello veya sonraki sürümünün [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).
2. Günlük analizi çalışma alanı. Daha fazla bilgi için bkz: [günlük Analytics ile çalışmaya başlama](../log-analytics/log-analytics-get-started.md). 
3. Merhaba ResourceId Azure Automation hesabınız için

Azure Otomasyonu hesabı ve günlük analizi çalışma alanı, PowerShell aşağıdaki hello çalıştırmak için toofind hello ResourceId:

```powershell
# Find hello ResourceId for hello Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"

# Find hello ResourceId for hello Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

Birden çok Automation hesapları varsa veya çalışma alanları, komutları, önceki hello hello çıktısında bulun hello *adı* tooconfigure gerekir ve kopyalamak için başlangıç değeri *ResourceId*.

Toofind hello gerekiyorsa *adı* Automation hesabınız hello Azure portal seçin, Automation hesabınız hello **Otomasyon hesabı** dikey ve seçin **tüm ayarları**.  Merhaba gelen **tüm ayarları** dikey altında **hesap ayarlarını** seçin **özellikleri**.  Merhaba, **özellikleri** dikey penceresinde bu değerleri fark edebilirsiniz.<br> ![Otomasyon hesabı özellikleri](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).

## <a name="set-up-integration-with-log-analytics"></a>Günlük analizi ile tümleştirmeyi ayarlamak
1. Bilgisayarınızda Başlat **Windows PowerShell** hello gelen **Başlat** ekran.  
2. Kopyalayın ve PowerShell aşağıdaki hello yapıştırın ve hello için başlangıç değerini Düzenle `$workspaceId` ve `$automationAccountId`.  Hello için `-Environment` parametre, geçerli değerler *AzureCloud* veya *AzureUSGovernment* içinde çalıştığınız hello bulut ortamı bağlı olarak.     

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }

# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $automationAccountId -WorkspaceId $workspaceId -Enabled $true

```

Bu komut dosyasını çalıştırdıktan sonra 10 dakika içinde yeni JobLogs veya JobStreams yazılan günlük analizi kayıtlarında görürsünüz.

toosee hello günlükleri, günlük analizi günlük arama sorguda aşağıdaki hello çalıştırın:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="verify-configuration"></a>Yapılandırmayı doğrulama
Otomasyon hesabınızı gönderme tooconfirm tooyour günlük analizi çalışma alanı günlükleri, tanılama PowerShell aşağıdaki hello kullanarak hello Otomasyon hesabı üzerinde doğru şekilde ayarlandığından emin olun:

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }
# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Get-AzureRmDiagnosticSetting -ResourceId $automationAccountId
```

Merhaba çıktısında emin olun:
+ Altında *günlükleri*, hello için değer *etkin* olan *True*
+ Merhaba değerini *Workspaceıd* toohello ResourceId günlük analizi çalışma alanınızın ayarlayın


## <a name="log-analytics-records"></a>Log Analytics kayıtları
Azure Otomasyonu tanılama günlük analizi kayıtları iki tür oluşturur ve olarak etiketlenir **türü AzureDiagnostics =**.

### <a name="job-logs"></a>İş günlükleri
| Özellik | Açıklama |
| --- | --- |
| TimeGenerated |Tarih ve saat hello runbook işi zaman yürütülür. |
| RunbookName_s |Merhaba runbook Hello adı. |
| Caller_s |Kimin hello işlemini başlattı.  Olası değerler, bir e-posta adresi veya zamanlanan işlere yönelik bir sistemdir. |
| Tenant_g | Merhaba çağıran hello Kiracı tanımlayan GUID. |
| JobId_g |Merhaba hello runbook işi kimliği olan GUID. |
| ResultType |Merhaba runbook işinin durumunu Hello.  Olası değerler şunlardır:<br>- Başlatıldı<br>- Durduruldu<br>- Askıya alındı<br>- Başarısız oldu<br>-Tamamlandı |
| Kategori | Merhaba tür veri sınıflandırması.  Otomasyon için hello JobLogs değerdir. |
| OperationName | Azure üzerinde gerçekleştirilen işlem Hello türünü belirtir.  Otomasyon için hello iş değerdir. |
| Kaynak | Merhaba Otomasyon hesabı adı |
| SourceSystem | Günlük analizi nasıl hello veri toplanmadı. Her zaman *Azure* Azure tanılama için. |
| ResultDescription |Merhaba runbook iş sonuç durumu açıklar.  Olası değerler şunlardır:<br>- İş başlatıldı<br>- İş Başarısız Oldu<br>- İş Tamamlandı |
| CorrelationId |Merhaba hello runbook işi bağıntı kimliği olan GUID. |
| ResourceId |Hello Azure Otomasyonu hesabı kaynak hello runbook kimliğini belirtir. |
| SubscriptionId | Merhaba hello Otomasyon hesabı için Azure aboneliği kimlik (GUID). |
| ResourceGroup | Merhaba Otomasyon hesabı hello kaynak grubunun adı. |
| ResourceProvider | MICROSOFT. OTOMASYON |
| ResourceType | AUTOMATIONACCOUNTS |


### <a name="job-streams"></a>İş akışları
| Özellik | Açıklama |
| --- | --- |
| TimeGenerated |Tarih ve saat hello runbook işi zaman yürütülür. |
| RunbookName_s |Merhaba runbook Hello adı. |
| Caller_s |Kimin hello işlemini başlattı.  Olası değerler, bir e-posta adresi veya zamanlanan işlere yönelik bir sistemdir. |
| StreamType_s |İş akışı Hello türü. Olası değerler şunlardır:<br>- İlerleme durumu<br>- Çıktı<br>- Uyarı<br>- Hata<br>- Hata ayıklama<br>- Ayrıntılı |
| Tenant_g | Merhaba çağıran hello Kiracı tanımlayan GUID. |
| JobId_g |Merhaba hello runbook işi kimliği olan GUID. |
| ResultType |Merhaba runbook işinin durumunu Hello.  Olası değerler şunlardır:<br>-Devam eden |
| Kategori | Merhaba tür veri sınıflandırması.  Otomasyon için hello JobStreams değerdir. |
| OperationName | Azure üzerinde gerçekleştirilen işlem Hello türünü belirtir.  Otomasyon için hello iş değerdir. |
| Kaynak | Merhaba Otomasyon hesabı adı |
| SourceSystem | Günlük analizi nasıl hello veri toplanmadı. Her zaman *Azure* Azure tanılama için. |
| ResultDescription |Merhaba runbook Hello çıkış akışından içerir. |
| CorrelationId |Merhaba hello runbook işi bağıntı kimliği olan GUID. |
| ResourceId |Hello Azure Otomasyonu hesabı kaynak hello runbook kimliğini belirtir. |
| SubscriptionId | Merhaba hello Otomasyon hesabı için Azure aboneliği kimlik (GUID). |
| ResourceGroup | Merhaba Otomasyon hesabı hello kaynak grubunun adı. |
| ResourceProvider | MICROSOFT. OTOMASYON |
| ResourceType | AUTOMATIONACCOUNTS |

## <a name="viewing-automation-logs-in-log-analytics"></a>Günlük analizi günlüklerini Otomasyon görüntüleme
Otomasyon iş günlükleri tooLog Analytics gönderme başlattığınız, günlük analizi içinde bu günlükleri ile neler yapabileceğinizi görelim.

toosee hello günlükleri, sorgu aşağıdaki hello çalıştırın:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a>Bir runbook işi başarısız olduğunda veya askıya alındığında bir e-posta Gönder
Üst müşterimiz birini ister olduğu hello özelliği toosend için bir e-posta veya bir metin bir şeyler ile bir runbook işi yanlış gittiğinde.   

toocreate bir uyarı kuralı hello uyarı çağıracağı iş kaydı hello runbook için günlük arama oluşturarak başlayın.  Merhaba tıklatın **uyarı** düğmesini toocreate ve hello uyarı kuralı yapılandırın.

1. Merhaba günlük analizi genel bakış sayfasında, **günlük arama**.
2. Arama hello sorgu alanına aşağıdaki hello yazarak, uyarı için bir günlük arama sorgusu oluşturun: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)` kullanarak RunbookName hello göre de gruplandırabilirsiniz:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`   

   Birden fazla Otomasyon hesabı veya abonelik tooyour çalışma günlüklerinden ayarladıysanız uyarılarınızı aboneliği ve Automation hesabı göre gruplandırabilirsiniz.  Automation hesabı adını JobLogs hello arama hello kaynak alanından elde edilebilir.  
3. tooopen hello **uyarı kuralı Ekle** ekranında **uyarı** hello sayfanın üst kısmındaki hello. Başlangıç seçenekleri tooconfigure hello uyarı hakkında daha fazla ayrıntı için bkz: [günlük analizi uyarılarını](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-all-jobs-that-have-completed-with-errors"></a>Hatalarla tamamlandı tüm işleri bulun
Bir runbook işi Sonlandırıcı olmayan bir hata olduğunda ayrıca tooalerting hatalarda bulabilirsiniz. Bu gibi durumlarda, bir hata akışı PowerShell oluşturur, ancak hello Sonlandırıcı olmayan hataları değil, iş toosuspend neden veya başarısız.    

1. Günlük analizi çalışma alanınızda tıklatın **günlük arama**.
2. Merhaba sorgu alanına yazın `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` ve ardından **arama**.

### <a name="view-job-streams-for-a-job"></a>Bir iş için Görünüm iş akışları
Bir işi ayıklarken, toolook hello iş akışlara isteyebilirsiniz.  Merhaba aşağıdaki sorgu tüm hello akışları GUID 2ebd22ea-e05e-4eb9 - 9 d 76-d73cbd4356e0 ile tek bir iş için gösterir:   

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams JobId_g="2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort TimeGenerated | select ResultDescription`

### <a name="view-historical-job-status"></a>Geçmiş işi durumunu görüntüleme
Son olarak, zaman içinde iş geçmişi toovisualize isteyebilirsiniz.  Bu sorgu toosearch zamanla hello işlerinizin durumunu kullanabilirsiniz.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  
<br> ![OMS geçmiş iş durumu grafiği](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)<br>

## <a name="summary"></a>Özet
Otomasyon iş durumu ve akış veri tooLog Analytics göndererek Otomasyon işlerinizin tarafından hello durumunu daha iyi bir anlayış alabilirsiniz:
+ Bir sorun olduğunda uyarıları toonotify ayarlama
+ Özel görünümleri ve arama sorguları toovisualize kullanarak, runbook sonuçları, runbook iş durumu ve diğer anahtar göstergeleri veya ölçümleri ilgili.  

Günlük analizi tooyour Otomasyon işleri büyük işletimsel görünürlük sağlar ve adres olaylar daha hızlı yardımcı olabilir.  

## <a name="next-steps"></a>Sonraki adımlar
* Günlük analizi ile günlükleri nasıl tooconstruct farklı arama sorguları ve gözden geçirme hello Otomasyon iş hakkında daha fazla toolearn bakın [oturum aramaları günlük analizi](../log-analytics/log-analytics-log-searches.md)
* toocreate ve alma çıkış ve hata iletileri, runbook'lardan nasıl görürüm toounderstand [Runbook çıkışı ve iletileri](automation-runbook-output-and-messages.md)
* toolearn hakkında daha fazla runbook yürütme toomonitor runbook işleri ve diğer teknik ayrıntıları görmek nasıl [bir runbook işi izlenemedi](automation-runbook-execution.md)
* OMS günlük analizi ve veri toplama kaynakları hakkında daha fazla toolearn bakın [toplama Azure storage veri günlük analizi genel bakış](../log-analytics/log-analytics-azure-storage.md)
