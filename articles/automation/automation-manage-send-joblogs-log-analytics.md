---
title: "OMS günlük analizi için Azure Otomasyonu işi veri iletmek | Microsoft Docs"
description: "Bu makalede iş durumu ve runbook iş akışları için ek bilgiler sunmak için Microsoft Operations Management Suite günlük analizi ve Yönetimi nasıl gönderileceğini gösterir."
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
ms.openlocfilehash: 2c0ca7fc332963e5a5db3c20c400ed877ae0cc54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="forward-job-status-and-job-streams-from-automation-to-log-analytics-oms"></a><span data-ttu-id="d2e00-103">İş durumu ve iş akışları Otomasyon günlük analizi (OMS) iletme</span><span class="sxs-lookup"><span data-stu-id="d2e00-103">Forward job status and job streams from Automation to Log Analytics (OMS)</span></span>
<span data-ttu-id="d2e00-104">Otomasyon runbook iş durumu ve iş akışları için Microsoft Operations Management Suite (OMS) günlük analizi çalışma alanınız gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2e00-104">Automation can send runbook job status and job streams to your Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>  <span data-ttu-id="d2e00-105">İş günlüğe kaydeder ve tek tek işler ve bu verir için basit araştırmalar gerçekleştirmek iş akışlarını Azure portalında veya PowerShell ile görünür.</span><span class="sxs-lookup"><span data-stu-id="d2e00-105">Job logs and job streams are visible in the Azure portal, or with PowerShell, for individual jobs and this allows you to perform simple investigations.</span></span> <span data-ttu-id="d2e00-106">Şimdi günlük analizi ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d2e00-106">Now with Log Analytics you can:</span></span>

* <span data-ttu-id="d2e00-107">Otomasyon işleriniz hakkında bilgi edinme</span><span class="sxs-lookup"><span data-stu-id="d2e00-107">Get insight on your Automation jobs</span></span>
* <span data-ttu-id="d2e00-108">Bir e-posta veya uyarı (örneğin, başarısız veya askıya alınmış), runbook işi durumlarına dayalı tetikleyici</span><span class="sxs-lookup"><span data-stu-id="d2e00-108">Trigger an email or alert based on your runbook job status (for example, failed or suspended)</span></span>
* <span data-ttu-id="d2e00-109">Gelişmiş sorgular, iş akışları yazma</span><span class="sxs-lookup"><span data-stu-id="d2e00-109">Write advanced queries across your job streams</span></span>
* <span data-ttu-id="d2e00-110">İşlerini Automation hesaplarında ilişkilendirmek</span><span class="sxs-lookup"><span data-stu-id="d2e00-110">Correlate jobs across Automation accounts</span></span>
* <span data-ttu-id="d2e00-111">İş Geçmişi zaman içinde görselleştirin</span><span class="sxs-lookup"><span data-stu-id="d2e00-111">Visualize your job history over time</span></span>     

## <a name="prerequisites-and-deployment-considerations"></a><span data-ttu-id="d2e00-112">Önkoşulları ve dağıtım hakkında önemli noktalar</span><span class="sxs-lookup"><span data-stu-id="d2e00-112">Prerequisites and deployment considerations</span></span>
<span data-ttu-id="d2e00-113">Günlük analizi için Otomasyon günlüklerinizi göndermeye başla, gerekir:</span><span class="sxs-lookup"><span data-stu-id="d2e00-113">To start sending your Automation logs to Log Analytics, you need:</span></span>

1. <span data-ttu-id="d2e00-114">Kasım 2016 veya sonraki sürümünün [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).</span><span class="sxs-lookup"><span data-stu-id="d2e00-114">The November 2016 or later release of [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).</span></span>
2. <span data-ttu-id="d2e00-115">Günlük analizi çalışma alanı.</span><span class="sxs-lookup"><span data-stu-id="d2e00-115">A Log Analytics workspace.</span></span> <span data-ttu-id="d2e00-116">Daha fazla bilgi için bkz: [günlük Analytics ile çalışmaya başlama](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d2e00-116">For more information, see [Get started with Log Analytics](../log-analytics/log-analytics-get-started.md).</span></span> 
3. <span data-ttu-id="d2e00-117">Azure Automation hesabınız için ResourceId</span><span class="sxs-lookup"><span data-stu-id="d2e00-117">The ResourceId for your Azure Automation account</span></span>

<span data-ttu-id="d2e00-118">Azure Otomasyonu hesabı ve günlük analizi çalışma alanı için ResourceId bulmak için aşağıdaki PowerShell çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d2e00-118">To find the ResourceId for your Azure Automation account and Log Analytics workspace, run the following PowerShell:</span></span>

```powershell
# Find the ResourceId for the Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"

# Find the ResourceId for the Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

<span data-ttu-id="d2e00-119">Birden çok Automation hesapları varsa veya çalışma alanları, önceki komutların çıktısı Bul *adı* değerini kopyalayın ve yapılandırmanız gerekir *ResourceId*.</span><span class="sxs-lookup"><span data-stu-id="d2e00-119">If you have multiple Automation accounts, or workspaces, in the output of the preceding commands, find the *Name* you need to configure and copy the value for *ResourceId*.</span></span>

<span data-ttu-id="d2e00-120">Bulmanız gerekiyorsa *adı* Otomasyon hesabınızı Azure portalında penceresinden Otomasyon hesabınızı seçin. **Otomasyon hesabı** dikey penceresinde ve select **tüm ayarları** .</span><span class="sxs-lookup"><span data-stu-id="d2e00-120">If you need to find the *Name* of your Automation account, in the Azure portal select your Automation account from the **Automation account** blade and select **All settings**.</span></span>  <span data-ttu-id="d2e00-121">**Tüm ayarlar** dikey penceresindeki **Hesap Ayarları** altında **Özellikler**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="d2e00-121">From the **All settings** blade, under **Account Settings** select **Properties**.</span></span>  <span data-ttu-id="d2e00-122">**Özellikler** dikey penceresinde bu değerleri fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2e00-122">In the **Properties** blade, you can note these values.</span></span><br> <span data-ttu-id="d2e00-123">![Otomasyon hesabı özellikleri](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).</span><span class="sxs-lookup"><span data-stu-id="d2e00-123">![Automation Account properties](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).</span></span>

## <a name="set-up-integration-with-log-analytics"></a><span data-ttu-id="d2e00-124">Günlük analizi ile tümleştirmeyi ayarlamak</span><span class="sxs-lookup"><span data-stu-id="d2e00-124">Set up integration with Log Analytics</span></span>
1. <span data-ttu-id="d2e00-125">Bilgisayarınızda Başlat **Windows PowerShell** gelen **Başlat** ekran.</span><span class="sxs-lookup"><span data-stu-id="d2e00-125">On your computer, start **Windows PowerShell** from the **Start** screen.</span></span>  
2. <span data-ttu-id="d2e00-126">Kopyalama ve aşağıdaki PowerShell yapıştırın ve değeri Düzenle `$workspaceId` ve `$automationAccountId`.</span><span class="sxs-lookup"><span data-stu-id="d2e00-126">Copy and paste the following PowerShell, and edit the value for the `$workspaceId` and `$automationAccountId`.</span></span>  <span data-ttu-id="d2e00-127">İçin `-Environment` parametre, geçerli değerler *AzureCloud* veya *AzureUSGovernment* içinde çalıştığınız bulut ortamınıza bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="d2e00-127">For the `-Environment` parameter, valid values are *AzureCloud* or *AzureUSGovernment* depending on the cloud environment you are working in.</span></span>     

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check to see which cloud environment to sign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }

# if you have one Log Analytics workspace you can use the following command to get the resource id of the workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $automationAccountId -WorkspaceId $workspaceId -Enabled $true

```

<span data-ttu-id="d2e00-128">Bu komut dosyasını çalıştırdıktan sonra 10 dakika içinde yeni JobLogs veya JobStreams yazılan günlük analizi kayıtlarında görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d2e00-128">After running this script, you will see records in Log Analytics within 10 minutes of new JobLogs or JobStreams being written.</span></span>

<span data-ttu-id="d2e00-129">Günlükleri görmek için günlük analizi günlük aramada aşağıdaki sorguyu çalıştırın:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span><span class="sxs-lookup"><span data-stu-id="d2e00-129">To see the logs, run the following query in Log Analytics log search: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span></span>

### <a name="verify-configuration"></a><span data-ttu-id="d2e00-130">Yapılandırmayı doğrulama</span><span class="sxs-lookup"><span data-stu-id="d2e00-130">Verify configuration</span></span>
<span data-ttu-id="d2e00-131">Automation hesabınız için günlük analizi çalışma alanınız günlükleri göndermek onaylamak için aşağıdaki PowerShell kullanarak Automation hesabını tanılama doğru ayarlandığından emin denetleyin:</span><span class="sxs-lookup"><span data-stu-id="d2e00-131">To confirm that your Automation account is sending logs to your Log Analytics workspace, check that diagnostics are set correctly on the Automation account using the following PowerShell:</span></span>

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check to see which cloud environment to sign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }
# if you have one Log Analytics workspace you can use the following command to get the resource id of the workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Get-AzureRmDiagnosticSetting -ResourceId $automationAccountId
```

<span data-ttu-id="d2e00-132">Çıktıda emin olun:</span><span class="sxs-lookup"><span data-stu-id="d2e00-132">In the output ensure that:</span></span>
+ <span data-ttu-id="d2e00-133">Altında *günlükleri*, değeri *etkin* olan *True*</span><span class="sxs-lookup"><span data-stu-id="d2e00-133">Under *Logs*, the value for *Enabled* is *True*</span></span>
+ <span data-ttu-id="d2e00-134">Değeri *Workspaceıd* günlük analizi çalışma alanınız ResourceId için ayarlama</span><span class="sxs-lookup"><span data-stu-id="d2e00-134">The value of *WorkspaceId* is set to the ResourceId of your Log Analytics workspace</span></span>


## <a name="log-analytics-records"></a><span data-ttu-id="d2e00-135">Log Analytics kayıtları</span><span class="sxs-lookup"><span data-stu-id="d2e00-135">Log Analytics records</span></span>
<span data-ttu-id="d2e00-136">Azure Otomasyonu tanılama günlük analizi kayıtları iki tür oluşturur ve olarak etiketlenir **türü AzureDiagnostics =**.</span><span class="sxs-lookup"><span data-stu-id="d2e00-136">Diagnostics from Azure Automation creates two types of records in Log Analytics and are tagged as **Type=AzureDiagnostics**.</span></span>

### <a name="job-logs"></a><span data-ttu-id="d2e00-137">İş günlükleri</span><span class="sxs-lookup"><span data-stu-id="d2e00-137">Job Logs</span></span>
| <span data-ttu-id="d2e00-138">Özellik</span><span class="sxs-lookup"><span data-stu-id="d2e00-138">Property</span></span> | <span data-ttu-id="d2e00-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d2e00-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d2e00-140">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="d2e00-140">TimeGenerated</span></span> |<span data-ttu-id="d2e00-141">Runbook işinin yürütüldüğü tarih ve saat.</span><span class="sxs-lookup"><span data-stu-id="d2e00-141">Date and time when the runbook job executed.</span></span> |
| <span data-ttu-id="d2e00-142">RunbookName_s</span><span class="sxs-lookup"><span data-stu-id="d2e00-142">RunbookName_s</span></span> |<span data-ttu-id="d2e00-143">Runbook’un adı.</span><span class="sxs-lookup"><span data-stu-id="d2e00-143">The name of the runbook.</span></span> |
| <span data-ttu-id="d2e00-144">Caller_s</span><span class="sxs-lookup"><span data-stu-id="d2e00-144">Caller_s</span></span> |<span data-ttu-id="d2e00-145">İşlemi başlatandır.</span><span class="sxs-lookup"><span data-stu-id="d2e00-145">Who initiated the operation.</span></span>  <span data-ttu-id="d2e00-146">Olası değerler, bir e-posta adresi veya zamanlanan işlere yönelik bir sistemdir.</span><span class="sxs-lookup"><span data-stu-id="d2e00-146">Possible values are either an email address or system for scheduled jobs.</span></span> |
| <span data-ttu-id="d2e00-147">Tenant_g</span><span class="sxs-lookup"><span data-stu-id="d2e00-147">Tenant_g</span></span> | <span data-ttu-id="d2e00-148">Arayanlar için Kiracı tanımlayan GUID.</span><span class="sxs-lookup"><span data-stu-id="d2e00-148">GUID that identifies the tenant for the Caller.</span></span> |
| <span data-ttu-id="d2e00-149">JobId_g</span><span class="sxs-lookup"><span data-stu-id="d2e00-149">JobId_g</span></span> |<span data-ttu-id="d2e00-150">Runbook işinin Kimliği olan GUID.</span><span class="sxs-lookup"><span data-stu-id="d2e00-150">GUID that is the Id of the runbook job.</span></span> |
| <span data-ttu-id="d2e00-151">ResultType</span><span class="sxs-lookup"><span data-stu-id="d2e00-151">ResultType</span></span> |<span data-ttu-id="d2e00-152">Runbook işinin durumudur.</span><span class="sxs-lookup"><span data-stu-id="d2e00-152">The status of the runbook job.</span></span>  <span data-ttu-id="d2e00-153">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d2e00-153">Possible values are:</span></span><br><span data-ttu-id="d2e00-154">- Başlatıldı</span><span class="sxs-lookup"><span data-stu-id="d2e00-154">- Started</span></span><br><span data-ttu-id="d2e00-155">- Durduruldu</span><span class="sxs-lookup"><span data-stu-id="d2e00-155">- Stopped</span></span><br><span data-ttu-id="d2e00-156">- Askıya alındı</span><span class="sxs-lookup"><span data-stu-id="d2e00-156">- Suspended</span></span><br><span data-ttu-id="d2e00-157">- Başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="d2e00-157">- Failed</span></span><br><span data-ttu-id="d2e00-158">-Tamamlandı</span><span class="sxs-lookup"><span data-stu-id="d2e00-158">- Completed</span></span> |
| <span data-ttu-id="d2e00-159">Kategori</span><span class="sxs-lookup"><span data-stu-id="d2e00-159">Category</span></span> | <span data-ttu-id="d2e00-160">Veri türü sınıflandırması.</span><span class="sxs-lookup"><span data-stu-id="d2e00-160">Classification of the type of data.</span></span>  <span data-ttu-id="d2e00-161">Otomasyon için değer JobLogs olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d2e00-161">For Automation, the value is JobLogs.</span></span> |
| <span data-ttu-id="d2e00-162">OperationName</span><span class="sxs-lookup"><span data-stu-id="d2e00-162">OperationName</span></span> | <span data-ttu-id="d2e00-163">Azure’da gerçekleştirilen işlem türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="d2e00-163">Specifies the type of operation performed in Azure.</span></span>  <span data-ttu-id="d2e00-164">Otomasyon için iş bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="d2e00-164">For Automation, the value is Job.</span></span> |
| <span data-ttu-id="d2e00-165">Kaynak</span><span class="sxs-lookup"><span data-stu-id="d2e00-165">Resource</span></span> | <span data-ttu-id="d2e00-166">Otomasyon hesabının adı</span><span class="sxs-lookup"><span data-stu-id="d2e00-166">Name of the Automation account</span></span> |
| <span data-ttu-id="d2e00-167">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="d2e00-167">SourceSystem</span></span> | <span data-ttu-id="d2e00-168">Günlük analizi nasıl veriler toplanır.</span><span class="sxs-lookup"><span data-stu-id="d2e00-168">How Log Analytics collected the data.</span></span> <span data-ttu-id="d2e00-169">Her zaman *Azure* Azure tanılama için.</span><span class="sxs-lookup"><span data-stu-id="d2e00-169">Always *Azure* for Azure diagnostics.</span></span> |
| <span data-ttu-id="d2e00-170">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="d2e00-170">ResultDescription</span></span> |<span data-ttu-id="d2e00-171">Runbook iş sonucu durumunu açıklar.</span><span class="sxs-lookup"><span data-stu-id="d2e00-171">Describes the runbook job result state.</span></span>  <span data-ttu-id="d2e00-172">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d2e00-172">Possible values are:</span></span><br><span data-ttu-id="d2e00-173">- İş başlatıldı</span><span class="sxs-lookup"><span data-stu-id="d2e00-173">- Job is started</span></span><br><span data-ttu-id="d2e00-174">- İş Başarısız Oldu</span><span class="sxs-lookup"><span data-stu-id="d2e00-174">- Job Failed</span></span><br><span data-ttu-id="d2e00-175">- İş Tamamlandı</span><span class="sxs-lookup"><span data-stu-id="d2e00-175">- Job Completed</span></span> |
| <span data-ttu-id="d2e00-176">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="d2e00-176">CorrelationId</span></span> |<span data-ttu-id="d2e00-177">Runbook işinin Bağıntı Kimliği olan GUID.</span><span class="sxs-lookup"><span data-stu-id="d2e00-177">GUID that is the Correlation Id of the runbook job.</span></span> |
| <span data-ttu-id="d2e00-178">ResourceId</span><span class="sxs-lookup"><span data-stu-id="d2e00-178">ResourceId</span></span> |<span data-ttu-id="d2e00-179">Runbook'un Azure Otomasyon hesabı kaynak kimliğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="d2e00-179">Specifies the Azure Automation account resource id of the runbook.</span></span> |
| <span data-ttu-id="d2e00-180">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="d2e00-180">SubscriptionId</span></span> | <span data-ttu-id="d2e00-181">Otomasyon hesabının Azure abonelik kimliği (GUID).</span><span class="sxs-lookup"><span data-stu-id="d2e00-181">The Azure subscription Id (GUID) for the Automation account.</span></span> |
| <span data-ttu-id="d2e00-182">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d2e00-182">ResourceGroup</span></span> | <span data-ttu-id="d2e00-183">Otomasyon hesabının kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="d2e00-183">Name of the resource group for the Automation account.</span></span> |
| <span data-ttu-id="d2e00-184">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="d2e00-184">ResourceProvider</span></span> | <span data-ttu-id="d2e00-185">MICROSOFT. OTOMASYON</span><span class="sxs-lookup"><span data-stu-id="d2e00-185">MICROSOFT.AUTOMATION</span></span> |
| <span data-ttu-id="d2e00-186">ResourceType</span><span class="sxs-lookup"><span data-stu-id="d2e00-186">ResourceType</span></span> | <span data-ttu-id="d2e00-187">AUTOMATIONACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="d2e00-187">AUTOMATIONACCOUNTS</span></span> |


### <a name="job-streams"></a><span data-ttu-id="d2e00-188">İş akışları</span><span class="sxs-lookup"><span data-stu-id="d2e00-188">Job Streams</span></span>
| <span data-ttu-id="d2e00-189">Özellik</span><span class="sxs-lookup"><span data-stu-id="d2e00-189">Property</span></span> | <span data-ttu-id="d2e00-190">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d2e00-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d2e00-191">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="d2e00-191">TimeGenerated</span></span> |<span data-ttu-id="d2e00-192">Runbook işinin yürütüldüğü tarih ve saat.</span><span class="sxs-lookup"><span data-stu-id="d2e00-192">Date and time when the runbook job executed.</span></span> |
| <span data-ttu-id="d2e00-193">RunbookName_s</span><span class="sxs-lookup"><span data-stu-id="d2e00-193">RunbookName_s</span></span> |<span data-ttu-id="d2e00-194">Runbook’un adı.</span><span class="sxs-lookup"><span data-stu-id="d2e00-194">The name of the runbook.</span></span> |
| <span data-ttu-id="d2e00-195">Caller_s</span><span class="sxs-lookup"><span data-stu-id="d2e00-195">Caller_s</span></span> |<span data-ttu-id="d2e00-196">İşlemi başlatandır.</span><span class="sxs-lookup"><span data-stu-id="d2e00-196">Who initiated the operation.</span></span>  <span data-ttu-id="d2e00-197">Olası değerler, bir e-posta adresi veya zamanlanan işlere yönelik bir sistemdir.</span><span class="sxs-lookup"><span data-stu-id="d2e00-197">Possible values are either an email address or system for scheduled jobs.</span></span> |
| <span data-ttu-id="d2e00-198">StreamType_s</span><span class="sxs-lookup"><span data-stu-id="d2e00-198">StreamType_s</span></span> |<span data-ttu-id="d2e00-199">İş akışı türü.</span><span class="sxs-lookup"><span data-stu-id="d2e00-199">The type of job stream.</span></span> <span data-ttu-id="d2e00-200">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d2e00-200">Possible values are:</span></span><br><span data-ttu-id="d2e00-201">- İlerleme durumu</span><span class="sxs-lookup"><span data-stu-id="d2e00-201">-Progress</span></span><br><span data-ttu-id="d2e00-202">- Çıktı</span><span class="sxs-lookup"><span data-stu-id="d2e00-202">- Output</span></span><br><span data-ttu-id="d2e00-203">- Uyarı</span><span class="sxs-lookup"><span data-stu-id="d2e00-203">- Warning</span></span><br><span data-ttu-id="d2e00-204">- Hata</span><span class="sxs-lookup"><span data-stu-id="d2e00-204">- Error</span></span><br><span data-ttu-id="d2e00-205">- Hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="d2e00-205">- Debug</span></span><br><span data-ttu-id="d2e00-206">- Ayrıntılı</span><span class="sxs-lookup"><span data-stu-id="d2e00-206">- Verbose</span></span> |
| <span data-ttu-id="d2e00-207">Tenant_g</span><span class="sxs-lookup"><span data-stu-id="d2e00-207">Tenant_g</span></span> | <span data-ttu-id="d2e00-208">Arayanlar için Kiracı tanımlayan GUID.</span><span class="sxs-lookup"><span data-stu-id="d2e00-208">GUID that identifies the tenant for the Caller.</span></span> |
| <span data-ttu-id="d2e00-209">JobId_g</span><span class="sxs-lookup"><span data-stu-id="d2e00-209">JobId_g</span></span> |<span data-ttu-id="d2e00-210">Runbook işinin Kimliği olan GUID.</span><span class="sxs-lookup"><span data-stu-id="d2e00-210">GUID that is the Id of the runbook job.</span></span> |
| <span data-ttu-id="d2e00-211">ResultType</span><span class="sxs-lookup"><span data-stu-id="d2e00-211">ResultType</span></span> |<span data-ttu-id="d2e00-212">Runbook işinin durumudur.</span><span class="sxs-lookup"><span data-stu-id="d2e00-212">The status of the runbook job.</span></span>  <span data-ttu-id="d2e00-213">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d2e00-213">Possible values are:</span></span><br><span data-ttu-id="d2e00-214">-Devam eden</span><span class="sxs-lookup"><span data-stu-id="d2e00-214">- In Progress</span></span> |
| <span data-ttu-id="d2e00-215">Kategori</span><span class="sxs-lookup"><span data-stu-id="d2e00-215">Category</span></span> | <span data-ttu-id="d2e00-216">Veri türü sınıflandırması.</span><span class="sxs-lookup"><span data-stu-id="d2e00-216">Classification of the type of data.</span></span>  <span data-ttu-id="d2e00-217">Otomasyon için değer JobStreams olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d2e00-217">For Automation, the value is JobStreams.</span></span> |
| <span data-ttu-id="d2e00-218">OperationName</span><span class="sxs-lookup"><span data-stu-id="d2e00-218">OperationName</span></span> | <span data-ttu-id="d2e00-219">Azure’da gerçekleştirilen işlem türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="d2e00-219">Specifies the type of operation performed in Azure.</span></span>  <span data-ttu-id="d2e00-220">Otomasyon için iş bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="d2e00-220">For Automation, the value is Job.</span></span> |
| <span data-ttu-id="d2e00-221">Kaynak</span><span class="sxs-lookup"><span data-stu-id="d2e00-221">Resource</span></span> | <span data-ttu-id="d2e00-222">Otomasyon hesabının adı</span><span class="sxs-lookup"><span data-stu-id="d2e00-222">Name of the Automation account</span></span> |
| <span data-ttu-id="d2e00-223">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="d2e00-223">SourceSystem</span></span> | <span data-ttu-id="d2e00-224">Günlük analizi nasıl veriler toplanır.</span><span class="sxs-lookup"><span data-stu-id="d2e00-224">How Log Analytics collected the data.</span></span> <span data-ttu-id="d2e00-225">Her zaman *Azure* Azure tanılama için.</span><span class="sxs-lookup"><span data-stu-id="d2e00-225">Always *Azure* for Azure diagnostics.</span></span> |
| <span data-ttu-id="d2e00-226">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="d2e00-226">ResultDescription</span></span> |<span data-ttu-id="d2e00-227">Runbook’un çıktı akışını içerir.</span><span class="sxs-lookup"><span data-stu-id="d2e00-227">Includes the output stream from the runbook.</span></span> |
| <span data-ttu-id="d2e00-228">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="d2e00-228">CorrelationId</span></span> |<span data-ttu-id="d2e00-229">Runbook işinin Bağıntı Kimliği olan GUID.</span><span class="sxs-lookup"><span data-stu-id="d2e00-229">GUID that is the Correlation Id of the runbook job.</span></span> |
| <span data-ttu-id="d2e00-230">ResourceId</span><span class="sxs-lookup"><span data-stu-id="d2e00-230">ResourceId</span></span> |<span data-ttu-id="d2e00-231">Runbook'un Azure Otomasyon hesabı kaynak kimliğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="d2e00-231">Specifies the Azure Automation account resource id of the runbook.</span></span> |
| <span data-ttu-id="d2e00-232">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="d2e00-232">SubscriptionId</span></span> | <span data-ttu-id="d2e00-233">Otomasyon hesabının Azure abonelik kimliği (GUID).</span><span class="sxs-lookup"><span data-stu-id="d2e00-233">The Azure subscription Id (GUID) for the Automation account.</span></span> |
| <span data-ttu-id="d2e00-234">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d2e00-234">ResourceGroup</span></span> | <span data-ttu-id="d2e00-235">Otomasyon hesabının kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="d2e00-235">Name of the resource group for the Automation account.</span></span> |
| <span data-ttu-id="d2e00-236">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="d2e00-236">ResourceProvider</span></span> | <span data-ttu-id="d2e00-237">MICROSOFT. OTOMASYON</span><span class="sxs-lookup"><span data-stu-id="d2e00-237">MICROSOFT.AUTOMATION</span></span> |
| <span data-ttu-id="d2e00-238">ResourceType</span><span class="sxs-lookup"><span data-stu-id="d2e00-238">ResourceType</span></span> | <span data-ttu-id="d2e00-239">AUTOMATIONACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="d2e00-239">AUTOMATIONACCOUNTS</span></span> |

## <a name="viewing-automation-logs-in-log-analytics"></a><span data-ttu-id="d2e00-240">Günlük analizi günlüklerini Otomasyon görüntüleme</span><span class="sxs-lookup"><span data-stu-id="d2e00-240">Viewing Automation Logs in Log Analytics</span></span>
<span data-ttu-id="d2e00-241">Günlük analizi için Otomasyon iş günlüklerinizi gönderme başlattığınız, günlük analizi içinde bu günlükleri ile neler yapabileceğinizi görelim.</span><span class="sxs-lookup"><span data-stu-id="d2e00-241">Now that you have started sending your Automation job logs to Log Analytics, let’s see what you can do with these logs inside Log Analytics.</span></span>

<span data-ttu-id="d2e00-242">Günlükleri görmek için aşağıdaki sorguyu çalıştırın:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span><span class="sxs-lookup"><span data-stu-id="d2e00-242">To see the logs, run the following query: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span></span>

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a><span data-ttu-id="d2e00-243">Bir runbook işi başarısız olduğunda veya askıya alındığında bir e-posta Gönder</span><span class="sxs-lookup"><span data-stu-id="d2e00-243">Send an email when a runbook job fails or suspends</span></span>
<span data-ttu-id="d2e00-244">Üst müşterimiz birini soran bir e-posta veya bir metin bir şeyler ile bir runbook işi yanlış gittiğinde gönderme olanağı içindir.</span><span class="sxs-lookup"><span data-stu-id="d2e00-244">One of our top customer asks is for the ability to send an email or a text when something goes wrong with a runbook job.</span></span>   

<span data-ttu-id="d2e00-245">Bir uyarı kuralı oluşturmak için uyarı çağıracağı runbook iş kaydı için bir günlük arama oluşturarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="d2e00-245">To create an alert rule, you start by creating a log search for the runbook job records that should invoke the alert.</span></span>  <span data-ttu-id="d2e00-246">Tıklatın **uyarı** oluşturmak ve uyarı kuralı yapılandırmak için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d2e00-246">Click the **Alert** button to create and configure the alert rule.</span></span>

1. <span data-ttu-id="d2e00-247">Günlük analizi genel bakış sayfasında **günlük arama**.</span><span class="sxs-lookup"><span data-stu-id="d2e00-247">From the Log Analytics Overview page, click **Log Search**.</span></span>
2. <span data-ttu-id="d2e00-248">Sorgu alanına aşağıdaki arama yazarak, uyarı için bir günlük arama sorgusu oluşturun: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)` kullanarak RunbookName göre de gruplandırabilirsiniz:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`</span><span class="sxs-lookup"><span data-stu-id="d2e00-248">Create a log search query for your alert by typing the following search into the query field:  `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)`  You can also group by the RunbookName by using: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`</span></span>   

   <span data-ttu-id="d2e00-249">Günlüklerini birden fazla Otomasyon hesabı veya abonelik alanınıza ayarladıysanız, uyarılarınızı aboneliği ve Automation hesabı göre gruplandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2e00-249">If you have set up logs from more than one Automation account or subscription to your workspace, you can group your alerts by subscription and Automation account.</span></span>  <span data-ttu-id="d2e00-250">Otomasyon hesabı adı JobLogs arama kaynak alanından elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="d2e00-250">Automation account name can be derived from the Resource field in the search of JobLogs.</span></span>  
3. <span data-ttu-id="d2e00-251">Açmak için **uyarı kuralı Ekle** ekranında **uyarı** sayfanın üst kısmındaki.</span><span class="sxs-lookup"><span data-stu-id="d2e00-251">To open the **Add Alert Rule** screen, click **Alert** at the top of the page.</span></span> <span data-ttu-id="d2e00-252">Uyarı yapılandırmak için seçenekleri hakkında daha fazla ayrıntı için bkz: [günlük analizi uyarılarını](../log-analytics/log-analytics-alerts.md#alert-rules).</span><span class="sxs-lookup"><span data-stu-id="d2e00-252">For further details on the options to configure the alert, see [Alerts in Log Analytics](../log-analytics/log-analytics-alerts.md#alert-rules).</span></span>

### <a name="find-all-jobs-that-have-completed-with-errors"></a><span data-ttu-id="d2e00-253">Hatalarla tamamlandı tüm işleri bulun</span><span class="sxs-lookup"><span data-stu-id="d2e00-253">Find all jobs that have completed with errors</span></span>
<span data-ttu-id="d2e00-254">Hatalarında uyarı ek olarak, bir runbook işi Sonlandırıcı olmayan bir hata olduğunda bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2e00-254">In addition to alerting on failures, you can find when a runbook job has a non-terminating error.</span></span> <span data-ttu-id="d2e00-255">Bu gibi durumlarda, bir hata akışı PowerShell oluşturur, ancak Sonlandırıcı olmayan hataları, işini askıya alma veya başarısız şekilde neden olmaz.</span><span class="sxs-lookup"><span data-stu-id="d2e00-255">In these cases PowerShell produces an error stream, but the non-terminating errors do not cause your job to suspend or fail.</span></span>    

1. <span data-ttu-id="d2e00-256">Günlük analizi çalışma alanınızda tıklatın **günlük arama**.</span><span class="sxs-lookup"><span data-stu-id="d2e00-256">In your Log Analytics workspace, click **Log Search**.</span></span>
2. <span data-ttu-id="d2e00-257">Sorgu alanına yazın `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` ve ardından **arama**.</span><span class="sxs-lookup"><span data-stu-id="d2e00-257">In the query field, type `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` and then click **Search**.</span></span>

### <a name="view-job-streams-for-a-job"></a><span data-ttu-id="d2e00-258">Bir iş için Görünüm iş akışları</span><span class="sxs-lookup"><span data-stu-id="d2e00-258">View job streams for a job</span></span>
<span data-ttu-id="d2e00-259">Bir işi ayıklarken iş akışlara aramak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2e00-259">When you are debugging a job, you may also want to look into the job streams.</span></span>  <span data-ttu-id="d2e00-260">Aşağıdaki sorgu GUID 2ebd22ea-e05e-4eb9 - 9 d 76-d73cbd4356e0 tek bir işin tüm akışlarını gösterir:</span><span class="sxs-lookup"><span data-stu-id="d2e00-260">The following query shows all the streams for a single job with GUID 2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0:</span></span>   

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams JobId_g="2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort TimeGenerated | select ResultDescription`

### <a name="view-historical-job-status"></a><span data-ttu-id="d2e00-261">Geçmiş işi durumunu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="d2e00-261">View historical job status</span></span>
<span data-ttu-id="d2e00-262">Son olarak, zaman içinde iş geçmişi görselleştirmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2e00-262">Finally, you may want to visualize your job history over time.</span></span>  <span data-ttu-id="d2e00-263">Zaman içinde işlerin durumunu aramak için bu sorguyu kullanın.</span><span class="sxs-lookup"><span data-stu-id="d2e00-263">You can use this query to search for the status of your jobs over time.</span></span>

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  
<br> <span data-ttu-id="d2e00-264">![OMS geçmiş iş durumu grafiği](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)</span><span class="sxs-lookup"><span data-stu-id="d2e00-264">![OMS Historical Job Status Chart](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)</span></span><br>

## <a name="summary"></a><span data-ttu-id="d2e00-265">Özet</span><span class="sxs-lookup"><span data-stu-id="d2e00-265">Summary</span></span>
<span data-ttu-id="d2e00-266">Günlük analizi için Otomasyon iş durumu ve akış veri göndererek Otomasyon işlerinizin tarafından durumunu daha iyi bir anlayış alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d2e00-266">By sending your Automation job status and stream data to Log Analytics, you can get better insight into the status of your Automation jobs by:</span></span>
+ <span data-ttu-id="d2e00-267">Bir sorun olduğunda bildirimde bulunacak uyarılar ayarlama</span><span class="sxs-lookup"><span data-stu-id="d2e00-267">Setting up alerts to notify you when there is an issue</span></span>
+ <span data-ttu-id="d2e00-268">Runbook sonuçlarınızı görselleştirmek için özel görünümleri ve arama sorguları kullanarak, runbook iş durumu ve diğer anahtar göstergeleri veya ölçümleri ilgili.</span><span class="sxs-lookup"><span data-stu-id="d2e00-268">Using custom views and search queries to visualize your runbook results, runbook job status, and other related key indicators or metrics.</span></span>  

<span data-ttu-id="d2e00-269">Günlük analizi Otomasyon işleriniz için daha fazla işlem görünürlük sağlar ve adres olaylar daha hızlı yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="d2e00-269">Log Analytics provides greater operational visibility to your Automation jobs and can help address incidents quicker.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d2e00-270">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d2e00-270">Next steps</span></span>
* <span data-ttu-id="d2e00-271">Farklı arama sorguları oluşturma ve Log Analytics ile Otomasyon iş günlüklerini gözden geçirme hakkında daha fazla bilgi edinmek için bkz. [Log Analytics’te günlük aramaları](../log-analytics/log-analytics-log-searches.md)</span><span class="sxs-lookup"><span data-stu-id="d2e00-271">To learn more about how to construct different search queries and review the Automation job logs with Log Analytics, see [Log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md)</span></span>
* <span data-ttu-id="d2e00-272">Oluşturmak ve runbook'lardan çıkış ve hata iletileri almak nasıl anlamak için bkz: [Runbook çıkışı ve iletileri](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="d2e00-272">To understand how to create and retrieve output and error messages from runbooks, see [Runbook output and messages](automation-runbook-output-and-messages.md)</span></span>
* <span data-ttu-id="d2e00-273">Runbook yürütme, runbook işlerini izleme ve diğer teknik ayrıntılar hakkında daha fazla bilgi edinmek için bkz. [Runbook işi izleme](automation-runbook-execution.md)</span><span class="sxs-lookup"><span data-stu-id="d2e00-273">To learn more about runbook execution, how to monitor runbook jobs, and other technical details, see [Track a runbook job](automation-runbook-execution.md)</span></span>
* <span data-ttu-id="d2e00-274">OMS Log Analytics ve veri toplama kaynakları hakkında daha fazla bilgi edinmek için bkz. [Log Analytics’te Azure depolama verileri toplamaya genel bakış](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="d2e00-274">To learn more about OMS Log Analytics and data collection sources, see [Collecting Azure storage data in Log Analytics overview](../log-analytics/log-analytics-azure-storage.md)</span></span>
