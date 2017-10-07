---
title: Azure Automation aaaSchedules | Microsoft Docs
description: "Otomasyon zamanlamaları otomatik olarak Azure Otomasyonu toostart kullanılan tooschedule runbook'larda olursunuz. Açıklar nasıl toocreate ve belirli bir zamanda veya yinelenen bir zamanlamaya göre otomatik olarak bir runbook başlatabilirsiniz bir zamanlama yönetin."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1c2da639-ad20-4848-920b-88e471b2e1d9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2016
ms.author: magoedte
ms.openlocfilehash: 888a5d15fd3442a2b8ab18dd8b0eb4ab9ad0c0d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a>Azure Otomasyonu’nda runbook zamanlama
tooschedule bir runbook belirtilen bir zamanda Azure Otomasyonu toostart içinde tooone ya da daha fazla zamanlama Bağla. Yapılandırılmış tooeither kez veya saatlik yinelenmeye çalışacak bir zamanlama olabilir ya da günlük zamanlama hello Klasik Azure portalı runbook'ları ve hello Azure portalı runbook'ları, ayrıca bunları hello haftada haftalık, aylık, belirli gün veya hello gün için zamanlayabilirsiniz ay veya hello ayın belirli bir gün.  Bir runbook bağlantılı toomultiple zamanlamaları olabilir ve birden çok runbook bağlı tooit bir zamanlama olabilir.

> [!NOTE]
> Zamanlamaları, şu anda Azure Otomasyonu DSC yapılandırmaları desteklemez.
> 
> 

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell cmdlet'leri
Aşağıdaki tablonun hello Hello cmdlet'leri kullanılan toocreate olan ve zamanlamaları Azure automation'da Windows PowerShell ile yönetme. Merhaba bir parçası olarak sevk [Azure PowerShell Modülü](/powershell/azure/overview).

| Cmdlet'leri | Açıklama |
|:--- |:--- |
| **Azure Resource Manager cmdlet'leri** | |
| [Get-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/get-azurermautomationschedule) |Bir zamanlama alır. |
| [AzureRmAutomationSchedule yeni](/powershell/module/azurerm.automation/new-azurermautomationschedule) |Yeni bir zamanlama oluşturur. |
| [Remove-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/remove-azurermautomationschedule) |Bir zamanlama kaldırır. |
| [Set-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) |Mevcut bir zamanlamayı Hello özelliklerini ayarlar. |
| [Get-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/set-azurermautomationscheduledrunbook) |Zamanlanmış runbook'lar alır. |
| [Register-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) |Bir runbook zamanlama ile ilişkilendirir. |
| [Kaydı AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/unregister-azurermautomationscheduledrunbook) |Zamanlama runbook'tan dissociates. |
| **Azure Hizmet Yönetimi cmdlet'leri** | |
| [Get-AzureAutomationSchedule](/powershell/module/azure/get-azureautomationschedule?view=azuresmps-3.7.0) |Bir zamanlama alır. |
| [AzureAutomationSchedule yeni](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) |Yeni bir zamanlama oluşturur. |
| [Remove-AzureAutomationSchedule](/powershell/module/azure/remove-azureautomationschedule?view=azuresmps-3.7.0) |Bir zamanlama kaldırır. |
| [Set-AzureAutomationSchedule](/powershell/module/azure/set-azureautomationschedule?view=azuresmps-3.7.0) |Mevcut bir zamanlamayı Hello özelliklerini ayarlar. |
| [Get-AzureAutomationScheduledRunbook](/powershell/module/azure/get-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Zamanlanmış runbook'lar alır. |
| [Register-AzureAutomationScheduledRunbook](/powershell/module/azure/register-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Bir runbook zamanlama ile ilişkilendirir. |
| [Kaydı AzureAutomationScheduledRunbook](/powershell/module/azure/unregister-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Zamanlama runbook'tan dissociates. |

## <a name="creating-a-schedule"></a>Bir zamanlama oluşturma
Merhaba Klasik portalında veya Windows PowerShell ile hello Azure portal, runbook'lar için yeni bir zamanlama oluşturabilirsiniz. Hello Azure Klasik kullanarak bir runbook tooa zamanlamaya bağladığınızda, yeni bir zamanlama ya da Azure portal oluşturma hello seçeneğiniz de vardır.

> [!NOTE]
> Yeni bir zamanlanan iş çalıştırdığınızda azure Automation Otomasyon hesabınızda hello son modülleri kullanın.  runbook'larınızı ve hello etkileyen tooavoid bunlar süreçlerini otomatikleştirmek, ilk zamanlamaları test etmek için adanmış bir Otomasyon hesabı ile bağlantılı runbook'ları test etmeniz gerekir.  Bu, zamanlanmış doğrulayacak runbook'lar toowork doğru devam edin ve size daha fazla sorun giderme ve uygulayabileceğiniz değil, varsa değişiklikleri önce gerekli geçirme güncelleştirilmiş hello runbook sürüm tooproduction.  
>  Bunları el ile Merhaba seçerek güncelleştirdikten sürece, Automation hesabınız modülleri yeni sürümlerini otomatik olarak almazsınız [Update Azure modülleri](automation-update-azure-modules.md) hello seçeneğinden **modülleri** dikey. 
>  

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a>toocreate hello Azure portal'ın yeni bir zamanlama
1. Hello Azure portalından, automation hesabınızı hello tıklatın **varlıklar** döşeme tooopen hello **varlıklar** dikey.
2. Merhaba tıklatın **zamanlamaları** döşeme tooopen hello **zamanlamaları** dikey.
3. Tıklatın **bir zamanlama Ekle** hello dikey penceresinde hello üstünde.
4. Merhaba üzerinde **yeni zamanlama** dikey penceresinde bir **adı** ve isteğe bağlı olarak bir **açıklama** hello yeni zamanlama için.
5. Bir kez Hello zamanlamanın çalışacağı olup olmadığını veya yeniden zamanlamada seçerek **kez** veya **yineleme**.  Seçerseniz **kez** belirtin bir **başlangıç zamanı** ve ardından **oluşturma**.  Seçerseniz **yineleme**, belirtin bir **başlangıç zamanı** ve ne sıklıkta hello runbook toorepeat - göre istediğiniz hello sıklığı **saat**, **gün**, **hafta**, ya da **ay**.  Seçerseniz **hafta** veya **ay** hello aşağı açılan listeden hello **yineleme seçeneği** hello dikey penceresinde ve seçime bağlı hello görünür **yineleme seçenek** dikey sunulabilir ve seçtiyseniz, haftanın başlangıç günü seçebilirsiniz **hafta**.  Seçtiyseniz, **ay**, tarafından seçebilirsiniz **haftanın günlerini** veya üzerinde hello ayın belirli günlerine hello takvim ve toorun son olarak, istediğiniz üzerinde veya hello ayın son günü hello ve ardından **Tamam** .   

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a>toocreate hello Klasik Azure portalında yeni bir zamanlama
1. Hello Klasik Azure portalı, Otomasyon seçin ve ardından bir Otomasyon hesabı hello adını seçin.
2. Select hello **varlıklar** sekmesi.
3. Merhaba penceresinin Hello altında tıklatın **ayar Ekle**.
4. Tıklatın **zamanlama Ekle**.
5. Tür a **adı** ve isteğe bağlı olarak bir **açıklama** hello yeni schedule.your için zamanlamanın çalışacağı **bir kez**, **saatlik**, **Günlük**, **haftalık**, veya **aylık**.
6. Belirtin bir **başlangıç saati** ve diğer seçenekler, seçtiğiniz zamanlamanın hello türüne bağlı olarak.

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a>toocreate Windows PowerShell ile yeni bir zamanlama
Merhaba kullanabilirsiniz [yeni AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) cmdlet toocreate yeni bir Azure Otomasyonu zamanlama Klasik runbook'lar için veya [yeni AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) hello Azure runbook'lar için cmdlet Portal. Merhaba zamanlama ve hello frekans çalışmalı hello başlangıç zamanını belirtmelisiniz.

Merhaba aşağıdaki örnek komutlar Göster nasıl toocreate hello için bir zamanlama 15 ve bir Azure Resource Manager cmdlet'i kullanılarak her ayın 30.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"

Aşağıdaki örnek komutlar hello Göster nasıl toocreate yeni bir zamanlama her çalıştıran 3:30 Şöyle bir Azure Hizmet Yönetimi cmdlet'iyle 20 Ocak 2015 tarihinde başlayan adresindeki gün.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

## <a name="linking-a-schedule-tooa-runbook"></a>Bir zamanlama tooa runbook bağlama
Bir runbook bağlantılı toomultiple zamanlamaları olabilir ve birden çok runbook bağlı tooit bir zamanlama olabilir. Bir runbook'un parametreleri varsa, daha sonra değerleri kendileri için sağlayabilirsiniz. Zorunlu parametreler için değer sağlamalısınız ve isteğe bağlı parametreler için değerler sağlayabilir.  Bu zamanlama tarafından hello runbook her başlatıldığında bu değerler kullanılır.  Ekleyebilir miyim hello aynı runbook tooanother zamanlaması ve farklı parametre değerlerini belirtin.

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a>toolink zamanlama tooa runbook hello Azure portal ile
1. Hello Azure portalından, automation hesabınızı hello tıklatın **Runbook'lar** döşeme tooopen hello **Runbook'lar** dikey.
2. Merhaba runbook tooschedule Hello adını tıklatın.
3. Sonra Hello runbook şu anda bağlı tooa zamanlama değilse yeni bir zamanlama verilen hello seçeneği toocreate olması veya zamanlama varolan tooan bağlantısını.  
4. Merhaba runbook'un parametreleri varsa hello seçeneği seçebilirsiniz **çalıştırma ayarlarını (varsayılan: Azure) Değiştir** ve hello **parametreleri** dikey penceresinde hello bilgileri buna göre girebilecekleri sunulur.  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a>toolink zamanlama tooa runbook hello Klasik Azure portalı ile
1. Hello Klasik Azure portalı, seçin **Otomasyon** ve ardından bir Otomasyon hesabı hello adına tıklayın.
2. Select hello **Runbook'lar** sekmesi.
3. Merhaba runbook tooschedule Hello adını tıklatın.
4. Merhaba tıklatın **zamanlama** sekmesi.
5. Merhaba runbook şu anda bağlı tooa zamanlama değil sonra çok hello seçeneği sunulur**tooa yeni zamanlama bağlantı** veya **tooan varolan zamanlama bağlantı**.  Merhaba runbook şu anda bağlı tooa zamanlama ise, tıklatın **bağlantı** , bu seçenekleri hello penceresi tooaccess alt hello.
6. Merhaba runbook'un parametreleri varsa, bunların değerleri istenir.  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a>Windows PowerShell ile bir zamanlama tooa runbook toolink
Merhaba kullanabilirsiniz [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink bir zamanlama tooa Klasik runbook veya [Register-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) cmdlet'i hello Azure portalı runbook'ları için.  Merhaba parametreleri parametresiyle hello runbook'un parametreleri için değerler belirtebilirsiniz. Bkz: [Azure Otomasyonu Runbook başlatma](automation-starting-a-runbook.md) parametre değerleri belirtme hakkında daha fazla bilgi için.

Merhaba aşağıdaki örnek komutlar Göster nasıl toolink parametrelere sahip bir Azure Resource Manager cmdlet'i kullanılarak bir zamanlama tooa runbook.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"
Merhaba aşağıdaki örnek komutlar Göster nasıl toolink parametrelere sahip bir Azure Hizmet Yönetimi cmdlet'i kullanılarak bir zamanlama.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

## <a name="disabling-a-schedule"></a>Bir zamanlama devre dışı bırakma
Bir zamanlama devre dışı bıraktığınızda, tüm bağlı olan runbook'lardan tooit artık bu zamanlamaya göre çalıştır. El ile bir zamanlama devre dışı bırakmak veya bunları oluşturduğunuzda bir sıklığı ile zamanlama için sona erme süresi ayarlayın. Merhaba sona erme süresine ulaşıldığında hello zamanlama devre dışı bırakılacak.

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a>toodisable hello Azure portal zamanlamadan
1. Hello Azure portalından, automation hesabınızı hello tıklatın **varlıklar** döşeme tooopen hello **varlıklar** dikey.
2. Merhaba tıklatın **zamanlamaları** döşeme tooopen hello **zamanlamaları** dikey.
3. Bir zamanlama tooopen hello ayrıntıları dikey penceresinde Hello adına tıklayın.
4. Değişiklik **etkin** çok**Hayır**.

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a>toodisable hello Klasik Azure portalı zamanlamadan
Merhaba hello Zamanlama Ayrıntıları sayfası hello zamanlama için Klasik Azure portalından bir zamanlama devre dışı bırakabilirsiniz.

1. Hello Klasik Azure portalı, Otomasyon seçin ve ardından bir Otomasyon hesabı hello adına tıklayın.
2. Merhaba varlıklar sekmesini seçin.
3. Kendi ayrıntı sayfası zamanlama tooopen Hello adına tıklayın.
4. Değişiklik **etkin** çok**Hayır**.

### <a name="toodisable-a-schedule-with-windows-powershell"></a>toodisable Windows PowerShell ile bir zamanlama
Merhaba kullanabilirsiniz [kümesi AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet toochange hello klasik bir runbook için varolan bir zamanlamanın özelliklerini veya [kümesi AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) hello Azure runbook'lar için cmdlet Portal. toodisable hello zamanlama, belirtin **false** hello için **IsEnabled** parametresi.

Merhaba aşağıdaki örnek komutlar Göster nasıl toodisable bir Azure Resource Manager cmdlet'i kullanılarak bir runbook için bir zamanlama.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"

Aşağıdaki örnek komutlar hello nasıl kullanarak bir zamanlama toodisable hello Azure Hizmet Yönetimi cmdlet'ini gösterir.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

## <a name="next-steps"></a>Sonraki adımlar
* Azure Otomasyonu runbook'ları kullanmaya tooget bakın [Azure Otomasyonu Runbook başlatma](automation-starting-a-runbook.md) 

