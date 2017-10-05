---
title: Azure Otomasyon runbook'u zamanlama | Microsoft Docs
description: "Belirli bir zamanda veya yinelenen bir zamanlamaya göre otomatik olarak bir runbook başlatabilirsiniz Azure Otomasyonu'nda bir zamanlama oluşturmak üzere açıklar."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 710979ff-99d8-41e4-ac6d-6bf26b8ea654
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/09/2016
ms.author: bwren
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 52f1d55f141bb1b3948e3b7039cfc131a5e407b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a>Azure Otomasyonu’nda runbook zamanlama
Belirli bir zamanda başlatmak için Azure automation'da bir runbook'u zamanlamak için bir veya daha fazla zamanlamaya bağlayın. Klasik Azure portalı runbook'larda ve runbook'ları Azure portalında bir kez veya bir yinelenmeye saatlik çalıştırma ya da günlük zamanlama için bir zamanlama yapılandırılabilir, ayrıca bunları için haftalık, aylık, haftanın belirli gün veya ayın günleri veya ayın belirli zamanlayabilirsiniz.  Bir runbook için birden çok zamanlama bağlanabilir ve bir zamanlama birden çok runbook bağlı olabilir.

## <a name="creating-a-schedule"></a>Bir zamanlama oluşturma
Azure portalında Klasik portalında veya Windows PowerShell ile runbook'lar için yeni bir zamanlama oluşturabilirsiniz. Ayrıca bir runbook'u Azure Klasik veya Azure portalını kullanarak bir zamanlamaya bağladığınızda, yeni bir zamanlama oluşturma seçeneğiniz vardır.

> [!NOTE]
> Zamanlama runbook ile ilişkilendirdiğinizde, Automation hesabınızı modülleri geçerli sürümleri depolar ve bu zamanlama için bağlar.  Başka bir deyişle, bir zamanlama oluşturuldu ve ardından modülü sürüm 2.0 güncelleştirme hesabınızda sürüm 1.0 sahip bir modül olsaydı, zamanlama 1.0 kullanmaya devam eder.  Güncelleştirilmiş Modül sürümü kullanmak için yeni bir zamanlama oluşturmanız gerekir. 
> 
> 

### <a name="to-create-a-new-schedule-in-the-azure-classic-portal"></a>Klasik Azure portalında yeni bir zamanlama oluşturmak için
1. Azure Klasik portalında Otomasyon seçin ve ardından bir Otomasyon hesabının adını seçin.
2. Seçin **varlıklar** sekmesi.
3. Pencerenin alt kısmındaki tıklatın **ayar Ekle**.
4. Tıklatın **zamanlama Ekle**.
5. Tür a **adı** ve isteğe bağlı olarak bir **açıklama** için yeni schedule.your zamanlamanın çalışacağı **bir kez**, **saatlik**, **günlük**, **haftalık**, veya **aylık**.
6. Belirtin bir **başlangıç saati** ve seçtiğiniz zamanlamanın türüne bağlı olarak diğer seçenekleri.

### <a name="to-create-a-new-schedule-in-the-azure-portal"></a>Azure portalında yeni bir zamanlama oluşturmak için
1. Azure portalından automation hesabınız tıklatın **varlıklar** açmak için kutucuğa **varlıklar** dikey.
2. Tıklatın **zamanlamaları** açmak için kutucuğa **zamanlamaları** dikey.
3. Tıklatın **bir zamanlama Ekle** dikey pencerenin üstündeki.
4. Üzerinde **yeni zamanlama** dikey penceresinde bir **adı** ve isteğe bağlı olarak bir **açıklama** yeni zamanlama için.
5. Bir kez zamanlamanın çalışacağı olup olmadığını veya bir yeniden zamanlamada seçerek **kez** veya **yineleme**.  Seçerseniz **kez** belirtin bir **başlangıç zamanı** ve ardından **oluşturma**.  Seçerseniz **yineleme**, belirtin bir **başlangıç zamanı** ve ne sıklıkta runbook - göre yinelemek istediğiniz sıklığını **saat**, **gün**, **hafta**, ya da **ay**.  Seçerseniz **hafta** veya **ay** aşağı açılan listeden **yineleme seçeneği** dikey penceresinde ve seçime bağlı görünür **yineleme seçeneği** dikey sunulabilir ve seçtiyseniz, haftanın günü seçebilirsiniz **hafta**.  Seçtiyseniz **ay**, tarafından seçebilirsiniz **haftanın günleri** veya takvim ayın belirli günlerine ve son olarak, çalıştırmak ayın son gününde veya ve ardından istiyorsunuz **Tamam**.   

### <a name="to-create-a-new-schedule-with-windows-powershell"></a>Windows PowerShell ile yeni bir zamanlama oluşturmak için
Kullanabileceğiniz [yeni AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) Azure Otomasyonu'nda Klasik runbook'lar için yeni bir zamanlama oluşturmak için cmdlet'i veya [yeni AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet'i Azure portalında runbook'lar için. Zamanlama ve çalışmalı sıklığı için başlangıç saatini belirtmeniz gerekir.

Aşağıdaki örnek komutlar her gün 3:30 Şöyle bir Azure Hizmet Yönetimi cmdlet'iyle 20 Ocak 2015 tarihinde başlatma sırasında çalışan yeni bir zamanlama oluşturmak nasıl gösterir.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

Aşağıdaki örnek komutlar bir Azure Resource Manager cmdlet'i kullanılarak her ayın 30 ve 15'inden için bir zamanlama oluşturmak nasıl gösterilir.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-to-a-runbook"></a>Bir runbook'a bir zamanlama bağlama
Bir runbook için birden çok zamanlama bağlanabilir ve bir zamanlama birden çok runbook bağlı olabilir. Bir runbook'un parametreleri varsa, daha sonra değerleri kendileri için sağlayabilirsiniz. Zorunlu parametreler için değer sağlamalısınız ve isteğe bağlı parametreler için değerler sağlayabilir.  Bu zamanlama tarafından runbook her başlatıldığında bu değerler kullanılır.  Aynı runbook başka bir plana bağlayın ve farklı parametre değerlerini belirtin.

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-classic-portal"></a>Klasik Azure portalı ile runbook için bir zamanlama bağlamak için
1. Klasik Azure portalında seçin **Otomasyon** ve ardından bir Otomasyon hesabı adına tıklayın.
2. Seçin **Runbook'lar** sekmesi.
3. Zamanlamak için runbook'un adına tıklayın.
4. Tıklatın **zamanlama** sekmesi.
5. Runbook şu anda bir zamanlamaya bağlı olmayan sonra seçeneğine verilen **yeni bir zamanlama Bağla** veya **varolan bir zamanlama Bağla**.  Runbook şu anda bir zamanlamaya bağlıysa, tıklatın **bağlantı** bu seçeneklerine erişmek için pencerenin altındaki.
6. Runbook'un parametreleri varsa, bunların değerleri istenir.  

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-portal"></a>Azure portal ile bir runbook için bir zamanlama bağlamak için
1. Azure portalından automation hesabınız tıklatın **Runbook'lar** açmak için kutucuğa **Runbook'lar** dikey.
2. Zamanlamak için runbook'un adına tıklayın.
3. Runbook şu anda bir zamanlamaya bağlı değilse yeni bir zamanlama ya da mevcut bir zamanlamayı bağlantısını oluşturma seçeneğini verilen.  
4. Runbook parametrelere sahipse, seçeneğini seçebilmenize **çalıştırma ayarlarını (varsayılan: Azure) Değiştir** ve **parametreleri** dikey bilgileri buna göre girebilecekleri sunulur.  

### <a name="to-link-a-schedule-to-a-runbook-with-windows-powershell"></a>Windows PowerShell ile bir runbook için bir zamanlama bağlamak için
Kullanabileceğiniz [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) klasik bir runbook'a bir zamanlama bağlamak için veya [Register-AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet'i Azure portalında runbook'lar için.  Parametreleri parametresiyle runbook'un parametreleri için değerler belirtebilirsiniz. Bkz: [Azure Otomasyonu Runbook başlatma](automation-starting-a-runbook.md) parametre değerleri belirtme hakkında daha fazla bilgi için.

Aşağıdaki örnek komutlar parametrelere sahip bir Azure Hizmet Yönetimi cmdlet'i kullanılarak bir zamanlama Bağla gösterilmektedir.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

Aşağıdaki örnek komutlar parametrelere sahip bir Azure Resource Manager cmdlet'i kullanılarak bir runbook'a bir zamanlama Bağla gösterilmektedir.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a>Bir zamanlama devre dışı bırakma
Bir zamanlama devre dışı bıraktığınızda, bağlı tüm runbook artık bu zamanlamaya göre çalıştır. El ile bir zamanlama devre dışı bırakmak veya bunları oluşturduğunuzda bir sıklığı ile zamanlama için sona erme süresi ayarlayın. Sona erme zamanı geldiğinde, zamanlama devre dışı bırakılacak.

### <a name="to-disable-a-schedule-from-the-azure-classic-portal"></a>Azure Klasik portalından bir zamanlama devre dışı bırakmak için
Zamanlama için Zamanlama Ayrıntıları sayfası, Klasik Azure portalından bir zamanlama devre dışı bırakabilirsiniz.

1. Azure Klasik portalında Otomasyon seçin ve ardından bir Otomasyon hesabı adına tıklayın.
2. Varlıklar sekmesini seçin.
3. Kendi ayrıntı sayfası açmak için bir zamanlama adına tıklayın.
4. Değişiklik **etkin** için **Hayır**.

### <a name="to-disable-a-schedule-from-the-azure-portal"></a>Azure portalından bir zamanlama devre dışı bırakmak için
1. Azure portalından automation hesabınız tıklatın **varlıklar** açmak için kutucuğa **varlıklar** dikey.
2. Tıklatın **zamanlamaları** açmak için kutucuğa **zamanlamaları** dikey.
3. Ayrıntılar dikey penceresini açmak için bir zamanlama adına tıklayın.
4. Değişiklik **etkin** için **Hayır**.

### <a name="to-disable-a-schedule-with-windows-powershell"></a>Windows PowerShell ile bir zamanlama devre dışı bırakmak için
Kullanabileceğiniz [kümesi AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) klasik bir runbook için varolan bir zamanlamanın özelliklerini değiştirmek için cmdlet veya [kümesi AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet'i Azure portalında runbook'lar için. Zamanlama devre dışı bırakmak için belirtmek **false** için **IsEnabled** parametresi.

Aşağıdaki örnek komutlar Azure Hizmet Yönetimi cmdlet'ini kullanarak bir zamanlama devre dışı bırakma göstermektedir.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

Aşağıdaki örnek komutlar bir Azure Resource Manager cmdlet'i kullanılarak bir runbook için bir zamanlama devre dışı bırakma göstermektedir.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a>Sonraki adımlar
* Zamanlama ile çalışma hakkında daha fazla bilgi için bkz: [Azure Otomasyonu zamanlama varlıkları](http://msdn.microsoft.com/library/azure/dn940016.aspx)
* Azure Otomasyonu runbook'ları kullanmaya başlamak için bkz: [Azure Otomasyonu Runbook başlatma](automation-starting-a-runbook.md) 

