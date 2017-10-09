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
# <a name="forward-job-status-and-job-streams-from-automation-toolog-analytics-oms"></a><span data-ttu-id="a3ba8-103">İş durumu ve iş akışları Otomasyon tooLog analizi (OMS) iletme</span><span class="sxs-lookup"><span data-stu-id="a3ba8-103">Forward job status and job streams from Automation tooLog Analytics (OMS)</span></span>
<span data-ttu-id="a3ba8-104">Otomasyon runbook iş durumu ve iş akışları tooyour Microsoft Operations Management Suite (OMS) günlük analizi çalışma alanı gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-104">Automation can send runbook job status and job streams tooyour Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>  <span data-ttu-id="a3ba8-105">İş günlüğe kaydeder ve iş akışları hello Azure portalında görünür olması veya PowerShell ile tek tek işler ve bu tooperform basit araştırmalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-105">Job logs and job streams are visible in hello Azure portal, or with PowerShell, for individual jobs and this allows you tooperform simple investigations.</span></span> <span data-ttu-id="a3ba8-106">Şimdi günlük analizi ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a3ba8-106">Now with Log Analytics you can:</span></span>

* <span data-ttu-id="a3ba8-107">Otomasyon işleriniz hakkında bilgi edinme</span><span class="sxs-lookup"><span data-stu-id="a3ba8-107">Get insight on your Automation jobs</span></span>
* <span data-ttu-id="a3ba8-108">Bir e-posta veya uyarı (örneğin, başarısız veya askıya alınmış), runbook işi durumlarına dayalı tetikleyici</span><span class="sxs-lookup"><span data-stu-id="a3ba8-108">Trigger an email or alert based on your runbook job status (for example, failed or suspended)</span></span>
* <span data-ttu-id="a3ba8-109">Gelişmiş sorgular, iş akışları yazma</span><span class="sxs-lookup"><span data-stu-id="a3ba8-109">Write advanced queries across your job streams</span></span>
* <span data-ttu-id="a3ba8-110">İşlerini Automation hesaplarında ilişkilendirmek</span><span class="sxs-lookup"><span data-stu-id="a3ba8-110">Correlate jobs across Automation accounts</span></span>
* <span data-ttu-id="a3ba8-111">İş Geçmişi zaman içinde görselleştirin</span><span class="sxs-lookup"><span data-stu-id="a3ba8-111">Visualize your job history over time</span></span>     

## <a name="prerequisites-and-deployment-considerations"></a><span data-ttu-id="a3ba8-112">Önkoşulları ve dağıtım hakkında önemli noktalar</span><span class="sxs-lookup"><span data-stu-id="a3ba8-112">Prerequisites and deployment considerations</span></span>
<span data-ttu-id="a3ba8-113">Automation'ınızı gönderme toostart tooLog Analytics günlükleri, gereksinim duyduğunuz:</span><span class="sxs-lookup"><span data-stu-id="a3ba8-113">toostart sending your Automation logs tooLog Analytics, you need:</span></span>

1. <span data-ttu-id="a3ba8-114">Kasım 2016 hello veya sonraki sürümünün [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).</span><span class="sxs-lookup"><span data-stu-id="a3ba8-114">hello November 2016 or later release of [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).</span></span>
2. <span data-ttu-id="a3ba8-115">Günlük analizi çalışma alanı.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-115">A Log Analytics workspace.</span></span> <span data-ttu-id="a3ba8-116">Daha fazla bilgi için bkz: [günlük Analytics ile çalışmaya başlama](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a3ba8-116">For more information, see [Get started with Log Analytics](../log-analytics/log-analytics-get-started.md).</span></span> 
3. <span data-ttu-id="a3ba8-117">Merhaba ResourceId Azure Automation hesabınız için</span><span class="sxs-lookup"><span data-stu-id="a3ba8-117">hello ResourceId for your Azure Automation account</span></span>

<span data-ttu-id="a3ba8-118">Azure Otomasyonu hesabı ve günlük analizi çalışma alanı, PowerShell aşağıdaki hello çalıştırmak için toofind hello ResourceId:</span><span class="sxs-lookup"><span data-stu-id="a3ba8-118">toofind hello ResourceId for your Azure Automation account and Log Analytics workspace, run hello following PowerShell:</span></span>

```powershell
# Find hello ResourceId for hello Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"

# Find hello ResourceId for hello Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

<span data-ttu-id="a3ba8-119">Birden çok Automation hesapları varsa veya çalışma alanları, komutları, önceki hello hello çıktısında bulun hello *adı* tooconfigure gerekir ve kopyalamak için başlangıç değeri *ResourceId*.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-119">If you have multiple Automation accounts, or workspaces, in hello output of hello preceding commands, find hello *Name* you need tooconfigure and copy hello value for *ResourceId*.</span></span>

<span data-ttu-id="a3ba8-120">Toofind hello gerekiyorsa *adı* Automation hesabınız hello Azure portal seçin, Automation hesabınız hello **Otomasyon hesabı** dikey ve seçin **tüm ayarları**.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-120">If you need toofind hello *Name* of your Automation account, in hello Azure portal select your Automation account from hello **Automation account** blade and select **All settings**.</span></span>  <span data-ttu-id="a3ba8-121">Merhaba gelen **tüm ayarları** dikey altında **hesap ayarlarını** seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-121">From hello **All settings** blade, under **Account Settings** select **Properties**.</span></span>  <span data-ttu-id="a3ba8-122">Merhaba, **özellikleri** dikey penceresinde bu değerleri fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-122">In hello **Properties** blade, you can note these values.</span></span><br> <span data-ttu-id="a3ba8-123">![Otomasyon hesabı özellikleri](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).</span><span class="sxs-lookup"><span data-stu-id="a3ba8-123">![Automation Account properties](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).</span></span>

## <a name="set-up-integration-with-log-analytics"></a><span data-ttu-id="a3ba8-124">Günlük analizi ile tümleştirmeyi ayarlamak</span><span class="sxs-lookup"><span data-stu-id="a3ba8-124">Set up integration with Log Analytics</span></span>
1. <span data-ttu-id="a3ba8-125">Bilgisayarınızda Başlat **Windows PowerShell** hello gelen **Başlat** ekran.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-125">On your computer, start **Windows PowerShell** from hello **Start** screen.</span></span>  
2. <span data-ttu-id="a3ba8-126">Kopyalayın ve PowerShell aşağıdaki hello yapıştırın ve hello için başlangıç değerini Düzenle `$workspaceId` ve `$automationAccountId`.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-126">Copy and paste hello following PowerShell, and edit hello value for hello `$workspaceId` and `$automationAccountId`.</span></span>  <span data-ttu-id="a3ba8-127">Hello için `-Environment` parametre, geçerli değerler *AzureCloud* veya *AzureUSGovernment* içinde çalıştığınız hello bulut ortamı bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-127">For hello `-Environment` parameter, valid values are *AzureCloud* or *AzureUSGovernment* depending on hello cloud environment you are working in.</span></span>     

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

<span data-ttu-id="a3ba8-128">Bu komut dosyasını çalıştırdıktan sonra 10 dakika içinde yeni JobLogs veya JobStreams yazılan günlük analizi kayıtlarında görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-128">After running this script, you will see records in Log Analytics within 10 minutes of new JobLogs or JobStreams being written.</span></span>

<span data-ttu-id="a3ba8-129">toosee hello günlükleri, günlük analizi günlük arama sorguda aşağıdaki hello çalıştırın:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span><span class="sxs-lookup"><span data-stu-id="a3ba8-129">toosee hello logs, run hello following query in Log Analytics log search: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span></span>

### <a name="verify-configuration"></a><span data-ttu-id="a3ba8-130">Yapılandırmayı doğrulama</span><span class="sxs-lookup"><span data-stu-id="a3ba8-130">Verify configuration</span></span>
<span data-ttu-id="a3ba8-131">Otomasyon hesabınızı gönderme tooconfirm tooyour günlük analizi çalışma alanı günlükleri, tanılama PowerShell aşağıdaki hello kullanarak hello Otomasyon hesabı üzerinde doğru şekilde ayarlandığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="a3ba8-131">tooconfirm that your Automation account is sending logs tooyour Log Analytics workspace, check that diagnostics are set correctly on hello Automation account using hello following PowerShell:</span></span>

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

<span data-ttu-id="a3ba8-132">Merhaba çıktısında emin olun:</span><span class="sxs-lookup"><span data-stu-id="a3ba8-132">In hello output ensure that:</span></span>
+ <span data-ttu-id="a3ba8-133">Altında *günlükleri*, hello için değer *etkin* olan *True*</span><span class="sxs-lookup"><span data-stu-id="a3ba8-133">Under *Logs*, hello value for *Enabled* is *True*</span></span>
+ <span data-ttu-id="a3ba8-134">Merhaba değerini *Workspaceıd* toohello ResourceId günlük analizi çalışma alanınızın ayarlayın</span><span class="sxs-lookup"><span data-stu-id="a3ba8-134">hello value of *WorkspaceId* is set toohello ResourceId of your Log Analytics workspace</span></span>


## <a name="log-analytics-records"></a><span data-ttu-id="a3ba8-135">Log Analytics kayıtları</span><span class="sxs-lookup"><span data-stu-id="a3ba8-135">Log Analytics records</span></span>
<span data-ttu-id="a3ba8-136">Azure Otomasyonu tanılama günlük analizi kayıtları iki tür oluşturur ve olarak etiketlenir **türü AzureDiagnostics =**.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-136">Diagnostics from Azure Automation creates two types of records in Log Analytics and are tagged as **Type=AzureDiagnostics**.</span></span>

### <a name="job-logs"></a><span data-ttu-id="a3ba8-137">İş günlükleri</span><span class="sxs-lookup"><span data-stu-id="a3ba8-137">Job Logs</span></span>
| <span data-ttu-id="a3ba8-138">Özellik</span><span class="sxs-lookup"><span data-stu-id="a3ba8-138">Property</span></span> | <span data-ttu-id="a3ba8-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a3ba8-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a3ba8-140">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="a3ba8-140">TimeGenerated</span></span> |<span data-ttu-id="a3ba8-141">Tarih ve saat hello runbook işi zaman yürütülür.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-141">Date and time when hello runbook job executed.</span></span> |
| <span data-ttu-id="a3ba8-142">RunbookName_s</span><span class="sxs-lookup"><span data-stu-id="a3ba8-142">RunbookName_s</span></span> |<span data-ttu-id="a3ba8-143">Merhaba runbook Hello adı.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-143">hello name of hello runbook.</span></span> |
| <span data-ttu-id="a3ba8-144">Caller_s</span><span class="sxs-lookup"><span data-stu-id="a3ba8-144">Caller_s</span></span> |<span data-ttu-id="a3ba8-145">Kimin hello işlemini başlattı.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-145">Who initiated hello operation.</span></span>  <span data-ttu-id="a3ba8-146">Olası değerler, bir e-posta adresi veya zamanlanan işlere yönelik bir sistemdir.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-146">Possible values are either an email address or system for scheduled jobs.</span></span> |
| <span data-ttu-id="a3ba8-147">Tenant_g</span><span class="sxs-lookup"><span data-stu-id="a3ba8-147">Tenant_g</span></span> | <span data-ttu-id="a3ba8-148">Merhaba çağıran hello Kiracı tanımlayan GUID.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-148">GUID that identifies hello tenant for hello Caller.</span></span> |
| <span data-ttu-id="a3ba8-149">JobId_g</span><span class="sxs-lookup"><span data-stu-id="a3ba8-149">JobId_g</span></span> |<span data-ttu-id="a3ba8-150">Merhaba hello runbook işi kimliği olan GUID.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-150">GUID that is hello Id of hello runbook job.</span></span> |
| <span data-ttu-id="a3ba8-151">ResultType</span><span class="sxs-lookup"><span data-stu-id="a3ba8-151">ResultType</span></span> |<span data-ttu-id="a3ba8-152">Merhaba runbook işinin durumunu Hello.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-152">hello status of hello runbook job.</span></span>  <span data-ttu-id="a3ba8-153">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a3ba8-153">Possible values are:</span></span><br><span data-ttu-id="a3ba8-154">- Başlatıldı</span><span class="sxs-lookup"><span data-stu-id="a3ba8-154">- Started</span></span><br><span data-ttu-id="a3ba8-155">- Durduruldu</span><span class="sxs-lookup"><span data-stu-id="a3ba8-155">- Stopped</span></span><br><span data-ttu-id="a3ba8-156">- Askıya alındı</span><span class="sxs-lookup"><span data-stu-id="a3ba8-156">- Suspended</span></span><br><span data-ttu-id="a3ba8-157">- Başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="a3ba8-157">- Failed</span></span><br><span data-ttu-id="a3ba8-158">-Tamamlandı</span><span class="sxs-lookup"><span data-stu-id="a3ba8-158">- Completed</span></span> |
| <span data-ttu-id="a3ba8-159">Kategori</span><span class="sxs-lookup"><span data-stu-id="a3ba8-159">Category</span></span> | <span data-ttu-id="a3ba8-160">Merhaba tür veri sınıflandırması.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-160">Classification of hello type of data.</span></span>  <span data-ttu-id="a3ba8-161">Otomasyon için hello JobLogs değerdir.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-161">For Automation, hello value is JobLogs.</span></span> |
| <span data-ttu-id="a3ba8-162">OperationName</span><span class="sxs-lookup"><span data-stu-id="a3ba8-162">OperationName</span></span> | <span data-ttu-id="a3ba8-163">Azure üzerinde gerçekleştirilen işlem Hello türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-163">Specifies hello type of operation performed in Azure.</span></span>  <span data-ttu-id="a3ba8-164">Otomasyon için hello iş değerdir.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-164">For Automation, hello value is Job.</span></span> |
| <span data-ttu-id="a3ba8-165">Kaynak</span><span class="sxs-lookup"><span data-stu-id="a3ba8-165">Resource</span></span> | <span data-ttu-id="a3ba8-166">Merhaba Otomasyon hesabı adı</span><span class="sxs-lookup"><span data-stu-id="a3ba8-166">Name of hello Automation account</span></span> |
| <span data-ttu-id="a3ba8-167">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="a3ba8-167">SourceSystem</span></span> | <span data-ttu-id="a3ba8-168">Günlük analizi nasıl hello veri toplanmadı.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-168">How Log Analytics collected hello data.</span></span> <span data-ttu-id="a3ba8-169">Her zaman *Azure* Azure tanılama için.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-169">Always *Azure* for Azure diagnostics.</span></span> |
| <span data-ttu-id="a3ba8-170">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="a3ba8-170">ResultDescription</span></span> |<span data-ttu-id="a3ba8-171">Merhaba runbook iş sonuç durumu açıklar.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-171">Describes hello runbook job result state.</span></span>  <span data-ttu-id="a3ba8-172">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a3ba8-172">Possible values are:</span></span><br><span data-ttu-id="a3ba8-173">- İş başlatıldı</span><span class="sxs-lookup"><span data-stu-id="a3ba8-173">- Job is started</span></span><br><span data-ttu-id="a3ba8-174">- İş Başarısız Oldu</span><span class="sxs-lookup"><span data-stu-id="a3ba8-174">- Job Failed</span></span><br><span data-ttu-id="a3ba8-175">- İş Tamamlandı</span><span class="sxs-lookup"><span data-stu-id="a3ba8-175">- Job Completed</span></span> |
| <span data-ttu-id="a3ba8-176">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="a3ba8-176">CorrelationId</span></span> |<span data-ttu-id="a3ba8-177">Merhaba hello runbook işi bağıntı kimliği olan GUID.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-177">GUID that is hello Correlation Id of hello runbook job.</span></span> |
| <span data-ttu-id="a3ba8-178">ResourceId</span><span class="sxs-lookup"><span data-stu-id="a3ba8-178">ResourceId</span></span> |<span data-ttu-id="a3ba8-179">Hello Azure Otomasyonu hesabı kaynak hello runbook kimliğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-179">Specifies hello Azure Automation account resource id of hello runbook.</span></span> |
| <span data-ttu-id="a3ba8-180">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="a3ba8-180">SubscriptionId</span></span> | <span data-ttu-id="a3ba8-181">Merhaba hello Otomasyon hesabı için Azure aboneliği kimlik (GUID).</span><span class="sxs-lookup"><span data-stu-id="a3ba8-181">hello Azure subscription Id (GUID) for hello Automation account.</span></span> |
| <span data-ttu-id="a3ba8-182">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a3ba8-182">ResourceGroup</span></span> | <span data-ttu-id="a3ba8-183">Merhaba Otomasyon hesabı hello kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-183">Name of hello resource group for hello Automation account.</span></span> |
| <span data-ttu-id="a3ba8-184">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="a3ba8-184">ResourceProvider</span></span> | <span data-ttu-id="a3ba8-185">MICROSOFT. OTOMASYON</span><span class="sxs-lookup"><span data-stu-id="a3ba8-185">MICROSOFT.AUTOMATION</span></span> |
| <span data-ttu-id="a3ba8-186">ResourceType</span><span class="sxs-lookup"><span data-stu-id="a3ba8-186">ResourceType</span></span> | <span data-ttu-id="a3ba8-187">AUTOMATIONACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="a3ba8-187">AUTOMATIONACCOUNTS</span></span> |


### <a name="job-streams"></a><span data-ttu-id="a3ba8-188">İş akışları</span><span class="sxs-lookup"><span data-stu-id="a3ba8-188">Job Streams</span></span>
| <span data-ttu-id="a3ba8-189">Özellik</span><span class="sxs-lookup"><span data-stu-id="a3ba8-189">Property</span></span> | <span data-ttu-id="a3ba8-190">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a3ba8-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a3ba8-191">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="a3ba8-191">TimeGenerated</span></span> |<span data-ttu-id="a3ba8-192">Tarih ve saat hello runbook işi zaman yürütülür.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-192">Date and time when hello runbook job executed.</span></span> |
| <span data-ttu-id="a3ba8-193">RunbookName_s</span><span class="sxs-lookup"><span data-stu-id="a3ba8-193">RunbookName_s</span></span> |<span data-ttu-id="a3ba8-194">Merhaba runbook Hello adı.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-194">hello name of hello runbook.</span></span> |
| <span data-ttu-id="a3ba8-195">Caller_s</span><span class="sxs-lookup"><span data-stu-id="a3ba8-195">Caller_s</span></span> |<span data-ttu-id="a3ba8-196">Kimin hello işlemini başlattı.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-196">Who initiated hello operation.</span></span>  <span data-ttu-id="a3ba8-197">Olası değerler, bir e-posta adresi veya zamanlanan işlere yönelik bir sistemdir.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-197">Possible values are either an email address or system for scheduled jobs.</span></span> |
| <span data-ttu-id="a3ba8-198">StreamType_s</span><span class="sxs-lookup"><span data-stu-id="a3ba8-198">StreamType_s</span></span> |<span data-ttu-id="a3ba8-199">İş akışı Hello türü.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-199">hello type of job stream.</span></span> <span data-ttu-id="a3ba8-200">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a3ba8-200">Possible values are:</span></span><br><span data-ttu-id="a3ba8-201">- İlerleme durumu</span><span class="sxs-lookup"><span data-stu-id="a3ba8-201">-Progress</span></span><br><span data-ttu-id="a3ba8-202">- Çıktı</span><span class="sxs-lookup"><span data-stu-id="a3ba8-202">- Output</span></span><br><span data-ttu-id="a3ba8-203">- Uyarı</span><span class="sxs-lookup"><span data-stu-id="a3ba8-203">- Warning</span></span><br><span data-ttu-id="a3ba8-204">- Hata</span><span class="sxs-lookup"><span data-stu-id="a3ba8-204">- Error</span></span><br><span data-ttu-id="a3ba8-205">- Hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="a3ba8-205">- Debug</span></span><br><span data-ttu-id="a3ba8-206">- Ayrıntılı</span><span class="sxs-lookup"><span data-stu-id="a3ba8-206">- Verbose</span></span> |
| <span data-ttu-id="a3ba8-207">Tenant_g</span><span class="sxs-lookup"><span data-stu-id="a3ba8-207">Tenant_g</span></span> | <span data-ttu-id="a3ba8-208">Merhaba çağıran hello Kiracı tanımlayan GUID.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-208">GUID that identifies hello tenant for hello Caller.</span></span> |
| <span data-ttu-id="a3ba8-209">JobId_g</span><span class="sxs-lookup"><span data-stu-id="a3ba8-209">JobId_g</span></span> |<span data-ttu-id="a3ba8-210">Merhaba hello runbook işi kimliği olan GUID.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-210">GUID that is hello Id of hello runbook job.</span></span> |
| <span data-ttu-id="a3ba8-211">ResultType</span><span class="sxs-lookup"><span data-stu-id="a3ba8-211">ResultType</span></span> |<span data-ttu-id="a3ba8-212">Merhaba runbook işinin durumunu Hello.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-212">hello status of hello runbook job.</span></span>  <span data-ttu-id="a3ba8-213">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a3ba8-213">Possible values are:</span></span><br><span data-ttu-id="a3ba8-214">-Devam eden</span><span class="sxs-lookup"><span data-stu-id="a3ba8-214">- In Progress</span></span> |
| <span data-ttu-id="a3ba8-215">Kategori</span><span class="sxs-lookup"><span data-stu-id="a3ba8-215">Category</span></span> | <span data-ttu-id="a3ba8-216">Merhaba tür veri sınıflandırması.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-216">Classification of hello type of data.</span></span>  <span data-ttu-id="a3ba8-217">Otomasyon için hello JobStreams değerdir.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-217">For Automation, hello value is JobStreams.</span></span> |
| <span data-ttu-id="a3ba8-218">OperationName</span><span class="sxs-lookup"><span data-stu-id="a3ba8-218">OperationName</span></span> | <span data-ttu-id="a3ba8-219">Azure üzerinde gerçekleştirilen işlem Hello türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-219">Specifies hello type of operation performed in Azure.</span></span>  <span data-ttu-id="a3ba8-220">Otomasyon için hello iş değerdir.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-220">For Automation, hello value is Job.</span></span> |
| <span data-ttu-id="a3ba8-221">Kaynak</span><span class="sxs-lookup"><span data-stu-id="a3ba8-221">Resource</span></span> | <span data-ttu-id="a3ba8-222">Merhaba Otomasyon hesabı adı</span><span class="sxs-lookup"><span data-stu-id="a3ba8-222">Name of hello Automation account</span></span> |
| <span data-ttu-id="a3ba8-223">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="a3ba8-223">SourceSystem</span></span> | <span data-ttu-id="a3ba8-224">Günlük analizi nasıl hello veri toplanmadı.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-224">How Log Analytics collected hello data.</span></span> <span data-ttu-id="a3ba8-225">Her zaman *Azure* Azure tanılama için.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-225">Always *Azure* for Azure diagnostics.</span></span> |
| <span data-ttu-id="a3ba8-226">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="a3ba8-226">ResultDescription</span></span> |<span data-ttu-id="a3ba8-227">Merhaba runbook Hello çıkış akışından içerir.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-227">Includes hello output stream from hello runbook.</span></span> |
| <span data-ttu-id="a3ba8-228">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="a3ba8-228">CorrelationId</span></span> |<span data-ttu-id="a3ba8-229">Merhaba hello runbook işi bağıntı kimliği olan GUID.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-229">GUID that is hello Correlation Id of hello runbook job.</span></span> |
| <span data-ttu-id="a3ba8-230">ResourceId</span><span class="sxs-lookup"><span data-stu-id="a3ba8-230">ResourceId</span></span> |<span data-ttu-id="a3ba8-231">Hello Azure Otomasyonu hesabı kaynak hello runbook kimliğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-231">Specifies hello Azure Automation account resource id of hello runbook.</span></span> |
| <span data-ttu-id="a3ba8-232">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="a3ba8-232">SubscriptionId</span></span> | <span data-ttu-id="a3ba8-233">Merhaba hello Otomasyon hesabı için Azure aboneliği kimlik (GUID).</span><span class="sxs-lookup"><span data-stu-id="a3ba8-233">hello Azure subscription Id (GUID) for hello Automation account.</span></span> |
| <span data-ttu-id="a3ba8-234">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a3ba8-234">ResourceGroup</span></span> | <span data-ttu-id="a3ba8-235">Merhaba Otomasyon hesabı hello kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-235">Name of hello resource group for hello Automation account.</span></span> |
| <span data-ttu-id="a3ba8-236">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="a3ba8-236">ResourceProvider</span></span> | <span data-ttu-id="a3ba8-237">MICROSOFT. OTOMASYON</span><span class="sxs-lookup"><span data-stu-id="a3ba8-237">MICROSOFT.AUTOMATION</span></span> |
| <span data-ttu-id="a3ba8-238">ResourceType</span><span class="sxs-lookup"><span data-stu-id="a3ba8-238">ResourceType</span></span> | <span data-ttu-id="a3ba8-239">AUTOMATIONACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="a3ba8-239">AUTOMATIONACCOUNTS</span></span> |

## <a name="viewing-automation-logs-in-log-analytics"></a><span data-ttu-id="a3ba8-240">Günlük analizi günlüklerini Otomasyon görüntüleme</span><span class="sxs-lookup"><span data-stu-id="a3ba8-240">Viewing Automation Logs in Log Analytics</span></span>
<span data-ttu-id="a3ba8-241">Otomasyon iş günlükleri tooLog Analytics gönderme başlattığınız, günlük analizi içinde bu günlükleri ile neler yapabileceğinizi görelim.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-241">Now that you have started sending your Automation job logs tooLog Analytics, let’s see what you can do with these logs inside Log Analytics.</span></span>

<span data-ttu-id="a3ba8-242">toosee hello günlükleri, sorgu aşağıdaki hello çalıştırın:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span><span class="sxs-lookup"><span data-stu-id="a3ba8-242">toosee hello logs, run hello following query: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span></span>

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a><span data-ttu-id="a3ba8-243">Bir runbook işi başarısız olduğunda veya askıya alındığında bir e-posta Gönder</span><span class="sxs-lookup"><span data-stu-id="a3ba8-243">Send an email when a runbook job fails or suspends</span></span>
<span data-ttu-id="a3ba8-244">Üst müşterimiz birini ister olduğu hello özelliği toosend için bir e-posta veya bir metin bir şeyler ile bir runbook işi yanlış gittiğinde.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-244">One of our top customer asks is for hello ability toosend an email or a text when something goes wrong with a runbook job.</span></span>   

<span data-ttu-id="a3ba8-245">toocreate bir uyarı kuralı hello uyarı çağıracağı iş kaydı hello runbook için günlük arama oluşturarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-245">toocreate an alert rule, you start by creating a log search for hello runbook job records that should invoke hello alert.</span></span>  <span data-ttu-id="a3ba8-246">Merhaba tıklatın **uyarı** düğmesini toocreate ve hello uyarı kuralı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-246">Click hello **Alert** button toocreate and configure hello alert rule.</span></span>

1. <span data-ttu-id="a3ba8-247">Merhaba günlük analizi genel bakış sayfasında, **günlük arama**.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-247">From hello Log Analytics Overview page, click **Log Search**.</span></span>
2. <span data-ttu-id="a3ba8-248">Arama hello sorgu alanına aşağıdaki hello yazarak, uyarı için bir günlük arama sorgusu oluşturun: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)` kullanarak RunbookName hello göre de gruplandırabilirsiniz:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`</span><span class="sxs-lookup"><span data-stu-id="a3ba8-248">Create a log search query for your alert by typing hello following search into hello query field:  `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)`  You can also group by hello RunbookName by using: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`</span></span>   

   <span data-ttu-id="a3ba8-249">Birden fazla Otomasyon hesabı veya abonelik tooyour çalışma günlüklerinden ayarladıysanız uyarılarınızı aboneliği ve Automation hesabı göre gruplandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-249">If you have set up logs from more than one Automation account or subscription tooyour workspace, you can group your alerts by subscription and Automation account.</span></span>  <span data-ttu-id="a3ba8-250">Automation hesabı adını JobLogs hello arama hello kaynak alanından elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-250">Automation account name can be derived from hello Resource field in hello search of JobLogs.</span></span>  
3. <span data-ttu-id="a3ba8-251">tooopen hello **uyarı kuralı Ekle** ekranında **uyarı** hello sayfanın üst kısmındaki hello.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-251">tooopen hello **Add Alert Rule** screen, click **Alert** at hello top of hello page.</span></span> <span data-ttu-id="a3ba8-252">Başlangıç seçenekleri tooconfigure hello uyarı hakkında daha fazla ayrıntı için bkz: [günlük analizi uyarılarını](../log-analytics/log-analytics-alerts.md#alert-rules).</span><span class="sxs-lookup"><span data-stu-id="a3ba8-252">For further details on hello options tooconfigure hello alert, see [Alerts in Log Analytics](../log-analytics/log-analytics-alerts.md#alert-rules).</span></span>

### <a name="find-all-jobs-that-have-completed-with-errors"></a><span data-ttu-id="a3ba8-253">Hatalarla tamamlandı tüm işleri bulun</span><span class="sxs-lookup"><span data-stu-id="a3ba8-253">Find all jobs that have completed with errors</span></span>
<span data-ttu-id="a3ba8-254">Bir runbook işi Sonlandırıcı olmayan bir hata olduğunda ayrıca tooalerting hatalarda bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-254">In addition tooalerting on failures, you can find when a runbook job has a non-terminating error.</span></span> <span data-ttu-id="a3ba8-255">Bu gibi durumlarda, bir hata akışı PowerShell oluşturur, ancak hello Sonlandırıcı olmayan hataları değil, iş toosuspend neden veya başarısız.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-255">In these cases PowerShell produces an error stream, but hello non-terminating errors do not cause your job toosuspend or fail.</span></span>    

1. <span data-ttu-id="a3ba8-256">Günlük analizi çalışma alanınızda tıklatın **günlük arama**.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-256">In your Log Analytics workspace, click **Log Search**.</span></span>
2. <span data-ttu-id="a3ba8-257">Merhaba sorgu alanına yazın `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` ve ardından **arama**.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-257">In hello query field, type `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` and then click **Search**.</span></span>

### <a name="view-job-streams-for-a-job"></a><span data-ttu-id="a3ba8-258">Bir iş için Görünüm iş akışları</span><span class="sxs-lookup"><span data-stu-id="a3ba8-258">View job streams for a job</span></span>
<span data-ttu-id="a3ba8-259">Bir işi ayıklarken, toolook hello iş akışlara isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-259">When you are debugging a job, you may also want toolook into hello job streams.</span></span>  <span data-ttu-id="a3ba8-260">Merhaba aşağıdaki sorgu tüm hello akışları GUID 2ebd22ea-e05e-4eb9 - 9 d 76-d73cbd4356e0 ile tek bir iş için gösterir:</span><span class="sxs-lookup"><span data-stu-id="a3ba8-260">hello following query shows all hello streams for a single job with GUID 2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0:</span></span>   

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams JobId_g="2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort TimeGenerated | select ResultDescription`

### <a name="view-historical-job-status"></a><span data-ttu-id="a3ba8-261">Geçmiş işi durumunu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="a3ba8-261">View historical job status</span></span>
<span data-ttu-id="a3ba8-262">Son olarak, zaman içinde iş geçmişi toovisualize isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-262">Finally, you may want toovisualize your job history over time.</span></span>  <span data-ttu-id="a3ba8-263">Bu sorgu toosearch zamanla hello işlerinizin durumunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-263">You can use this query toosearch for hello status of your jobs over time.</span></span>

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  
<br> <span data-ttu-id="a3ba8-264">![OMS geçmiş iş durumu grafiği](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)</span><span class="sxs-lookup"><span data-stu-id="a3ba8-264">![OMS Historical Job Status Chart](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)</span></span><br>

## <a name="summary"></a><span data-ttu-id="a3ba8-265">Özet</span><span class="sxs-lookup"><span data-stu-id="a3ba8-265">Summary</span></span>
<span data-ttu-id="a3ba8-266">Otomasyon iş durumu ve akış veri tooLog Analytics göndererek Otomasyon işlerinizin tarafından hello durumunu daha iyi bir anlayış alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a3ba8-266">By sending your Automation job status and stream data tooLog Analytics, you can get better insight into hello status of your Automation jobs by:</span></span>
+ <span data-ttu-id="a3ba8-267">Bir sorun olduğunda uyarıları toonotify ayarlama</span><span class="sxs-lookup"><span data-stu-id="a3ba8-267">Setting up alerts toonotify you when there is an issue</span></span>
+ <span data-ttu-id="a3ba8-268">Özel görünümleri ve arama sorguları toovisualize kullanarak, runbook sonuçları, runbook iş durumu ve diğer anahtar göstergeleri veya ölçümleri ilgili.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-268">Using custom views and search queries toovisualize your runbook results, runbook job status, and other related key indicators or metrics.</span></span>  

<span data-ttu-id="a3ba8-269">Günlük analizi tooyour Otomasyon işleri büyük işletimsel görünürlük sağlar ve adres olaylar daha hızlı yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a3ba8-269">Log Analytics provides greater operational visibility tooyour Automation jobs and can help address incidents quicker.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="a3ba8-270">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a3ba8-270">Next steps</span></span>
* <span data-ttu-id="a3ba8-271">Günlük analizi ile günlükleri nasıl tooconstruct farklı arama sorguları ve gözden geçirme hello Otomasyon iş hakkında daha fazla toolearn bakın [oturum aramaları günlük analizi](../log-analytics/log-analytics-log-searches.md)</span><span class="sxs-lookup"><span data-stu-id="a3ba8-271">toolearn more about how tooconstruct different search queries and review hello Automation job logs with Log Analytics, see [Log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md)</span></span>
* <span data-ttu-id="a3ba8-272">toocreate ve alma çıkış ve hata iletileri, runbook'lardan nasıl görürüm toounderstand [Runbook çıkışı ve iletileri](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="a3ba8-272">toounderstand how toocreate and retrieve output and error messages from runbooks, see [Runbook output and messages](automation-runbook-output-and-messages.md)</span></span>
* <span data-ttu-id="a3ba8-273">toolearn hakkında daha fazla runbook yürütme toomonitor runbook işleri ve diğer teknik ayrıntıları görmek nasıl [bir runbook işi izlenemedi](automation-runbook-execution.md)</span><span class="sxs-lookup"><span data-stu-id="a3ba8-273">toolearn more about runbook execution, how toomonitor runbook jobs, and other technical details, see [Track a runbook job](automation-runbook-execution.md)</span></span>
* <span data-ttu-id="a3ba8-274">OMS günlük analizi ve veri toplama kaynakları hakkında daha fazla toolearn bakın [toplama Azure storage veri günlük analizi genel bakış](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="a3ba8-274">toolearn more about OMS Log Analytics and data collection sources, see [Collecting Azure storage data in Log Analytics overview](../log-analytics/log-analytics-azure-storage.md)</span></span>
