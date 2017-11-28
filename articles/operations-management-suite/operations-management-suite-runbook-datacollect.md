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
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="694c2-103">Günlük analizi olarak toplamak ve bir Azure Otomasyonu runbook'u</span><span class="sxs-lookup"><span data-stu-id="694c2-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="694c2-104">Günlük analizi veri önemli miktarda bir çeşitli kaynaklardan dahil olmak üzere toplayabilirsiniz [veri kaynakları](../log-analytics/log-analytics-data-sources.md) aracılar üzerinde hem de [Azure'dan toplanan veriler](../log-analytics/log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="694c2-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="694c2-105">Toocollect veri ihtiyaç duyacağınız, bu standart kaynakları aracılığıyla erişilebilir değil ancak bir senaryo vardır.</span><span class="sxs-lookup"><span data-stu-id="694c2-105">There are a scenarios though where you need toocollect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="694c2-106">Bu durumlarda, hello kullanabilirsiniz [HTTP veri toplayıcı API](../log-analytics/log-analytics-data-collector-api.md) herhangi bir REST API istemciden toowrite veri tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="694c2-106">In these cases, you can use hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) toowrite data tooLog Analytics from any REST API client.</span></span>  <span data-ttu-id="694c2-107">Ortak bir yöntem tooperform bu veri toplama Azure Otomasyonu'nda bir runbook kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="694c2-107">A common method tooperform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="694c2-108">Bu öğreticide oluşturma ve bir Azure Otomasyonu toowrite veri tooLog Analytics runbook'ta zamanlama hello işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="694c2-108">This tutorial walks through hello process for creating and scheduling a runbook in Azure Automation toowrite data tooLog Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="694c2-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="694c2-109">Prerequisites</span></span>
<span data-ttu-id="694c2-110">Bu senaryo, Azure aboneliğinizde yapılandırılmış kaynakları aşağıdaki hello gerektirir.</span><span class="sxs-lookup"><span data-stu-id="694c2-110">This scenario requires hello following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="694c2-111">Her ikisi de ücretsiz bir hesap olabilir.</span><span class="sxs-lookup"><span data-stu-id="694c2-111">Both can be a free account.</span></span>

- <span data-ttu-id="694c2-112">[Günlük analizi çalışma alanı](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="694c2-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="694c2-113">[Azure Otomasyon hesabı](../automation/automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="694c2-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="694c2-114">Senaryoya genel bakış</span><span class="sxs-lookup"><span data-stu-id="694c2-114">Overview of scenario</span></span>
<span data-ttu-id="694c2-115">Bu öğretici için Otomasyon işleri hakkında bilgi toplar bir runbook yazacaksınız.</span><span class="sxs-lookup"><span data-stu-id="694c2-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="694c2-116">Azure Otomasyonu runbook'ları yazma ve komut dosyası hello Azure Otomasyon Düzenleyicisi'nde test tarafından başlayacaksınız şekilde PowerShell ile uygulanır.</span><span class="sxs-lookup"><span data-stu-id="694c2-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in hello Azure Automation editor.</span></span>  <span data-ttu-id="694c2-117">Gerekli hello bilgi topladığınız doğrulayın sonra bu veri tooLog Analytics yazma ve hello özel veri türü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="694c2-117">Once you verify that you're collecting hello required information, you'll write that data tooLog Analytics and verify hello custom data type.</span></span>  <span data-ttu-id="694c2-118">Son olarak, düzenli aralıklarla bir zamanlama toostart hello runbook oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="694c2-118">Finally, you'll create a schedule toostart hello runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="694c2-119">Bu runbook olmadan Azure Otomasyonu toosend iş bilgi tooLog Analytics yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="694c2-119">You can configure Azure Automation toosend job information tooLog Analytics without this runbook.</span></span>  <span data-ttu-id="694c2-120">Bu senaryo birincil olarak kullanılan toosupport hello öğreticidir ve hello veri tooa test çalışma göndermeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="694c2-120">This scenario is primarily used toosupport hello tutorial, and it's recommended that you send hello data tooa test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="694c2-121">1. Veri Toplayıcı API modülünü yükleme</span><span class="sxs-lookup"><span data-stu-id="694c2-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="694c2-122">Her [hello HTTP veri toplayıcı API isteğinden](../log-analytics/log-analytics-data-collector-api.md#create-a-request) uygun şekilde biçimlendirilmiş olması gerekir ve bir authorization üstbilgisi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="694c2-122">Every [request from hello HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="694c2-123">Bunu runbook'unuzda yapabilirsiniz ancak bu işlemi basitleştirir bir modül kullanarak gerekli kod hello miktarını düşürebilir.</span><span class="sxs-lookup"><span data-stu-id="694c2-123">You can do this in your runbook, but you can reduce hello amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="694c2-124">Kullanabileceğiniz bir modül [OMSIngestionAPI Modülü](https://www.powershellgallery.com/packages/OMSIngestionAPI) hello PowerShell Galerisi içinde.</span><span class="sxs-lookup"><span data-stu-id="694c2-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in hello PowerShell Gallery.</span></span>

<span data-ttu-id="694c2-125">toouse bir [Modülü](../automation/automation-integration-modules.md) bir runbook'ta Otomasyon hesabınızda yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="694c2-125">toouse a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="694c2-126">Aynı hesap ardından kullanabileceğiniz hello herhangi bir runbook hello hello modülünde işlevleri.</span><span class="sxs-lookup"><span data-stu-id="694c2-126">Any runbook in hello same account can then use hello functions in hello module.</span></span>  <span data-ttu-id="694c2-127">Yeni bir modül seçerek yükleyebilirsiniz **varlıklar** > **modülleri** > **bir modül Ekle** Otomasyon hesabınızda.</span><span class="sxs-lookup"><span data-stu-id="694c2-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="694c2-128">tooyour Otomasyon hesabı doğrudan Bu öğretici için bu seçeneği kullanabilmeniz için hello PowerShell Galerisi, ancak Hızlı seçeneği toodeploy bir modül sağlar.</span><span class="sxs-lookup"><span data-stu-id="694c2-128">hello PowerShell Gallery though gives you a quick option toodeploy a module directly tooyour automation account so you can use that option for this tutorial.</span></span>  

![OMSIngestionAPI Modülü](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="694c2-130">Çok Git[PowerShell Galerisi](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="694c2-130">Go too[PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="694c2-131">Arama **OMSIngestionAPI**.</span><span class="sxs-lookup"><span data-stu-id="694c2-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="694c2-132">Tıklatın hello üzerinde **tooAzure Otomasyon dağıtmak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="694c2-132">Click on hello **Deploy tooAzure Automation** button.</span></span>
4. <span data-ttu-id="694c2-133">Otomasyon hesabınızı seçin ve tıklatın **Tamam** tooinstall hello modülü.</span><span class="sxs-lookup"><span data-stu-id="694c2-133">Select your automation account and click **OK** tooinstall hello module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="694c2-134">2. Otomasyon değişkenleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="694c2-134">2. Create Automation variables</span></span>
<span data-ttu-id="694c2-135">[Otomasyon değişkenleri](..\automation\automation-variables.md) Otomasyon hesabınızda tüm runbook'lar tarafından kullanılan değerleri tutun.</span><span class="sxs-lookup"><span data-stu-id="694c2-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="694c2-136">Daha fazla runbook'ları olun toochange sağlayarak esnek düzenlemeden bu değerleri gerçek runbook hello.</span><span class="sxs-lookup"><span data-stu-id="694c2-136">They make runbooks more flexible by allowing you toochange these values without editing hello actual runbook.</span></span> <span data-ttu-id="694c2-137">Her istekten hello HTTP veri toplayıcı API hello kimliği ve anahtarı hello OMS çalışma alanının gerektirir ve değişken varlıkları olan ideal toostore bu bilgileri.</span><span class="sxs-lookup"><span data-stu-id="694c2-137">Every request from hello HTTP Data Collector API requires hello ID and key of hello OMS workspace, and variable assets are ideal toostore this information.</span></span>  

![Değişkenler](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="694c2-139">Hello Azure portal, tooyour Otomasyon hesabı gidin.</span><span class="sxs-lookup"><span data-stu-id="694c2-139">In hello Azure portal, navigate tooyour Automation account.</span></span>
2. <span data-ttu-id="694c2-140">Seçin **değişkenleri** altında **paylaşılan kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="694c2-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="694c2-141">Tıklatın **değişken Ekle** ve hello aşağıdaki tablonun hello iki değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="694c2-141">Click **Add a variable** and create hello two variables in hello following table.</span></span>

| <span data-ttu-id="694c2-142">Özellik</span><span class="sxs-lookup"><span data-stu-id="694c2-142">Property</span></span> | <span data-ttu-id="694c2-143">Çalışma alanı kimliği değeri</span><span class="sxs-lookup"><span data-stu-id="694c2-143">Workspace ID Value</span></span> | <span data-ttu-id="694c2-144">Çalışma alanı anahtarı değeri</span><span class="sxs-lookup"><span data-stu-id="694c2-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="694c2-145">Ad</span><span class="sxs-lookup"><span data-stu-id="694c2-145">Name</span></span> | <span data-ttu-id="694c2-146">Workspaceıd</span><span class="sxs-lookup"><span data-stu-id="694c2-146">WorkspaceId</span></span> | <span data-ttu-id="694c2-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="694c2-147">WorkspaceKey</span></span> |
| <span data-ttu-id="694c2-148">Tür</span><span class="sxs-lookup"><span data-stu-id="694c2-148">Type</span></span> | <span data-ttu-id="694c2-149">Dize</span><span class="sxs-lookup"><span data-stu-id="694c2-149">String</span></span> | <span data-ttu-id="694c2-150">Dize</span><span class="sxs-lookup"><span data-stu-id="694c2-150">String</span></span> |
| <span data-ttu-id="694c2-151">Değer</span><span class="sxs-lookup"><span data-stu-id="694c2-151">Value</span></span> | <span data-ttu-id="694c2-152">Merhaba, günlük analizi çalışma alanının çalışma alanı kimliği yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="694c2-152">Paste in hello Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="694c2-153">Oturum Hello birincil veya ikincil anahtarı günlük analizi çalışma alanınızın yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="694c2-153">Paste in with hello Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="694c2-154">Şifreli</span><span class="sxs-lookup"><span data-stu-id="694c2-154">Encrypted</span></span> | <span data-ttu-id="694c2-155">Hayır</span><span class="sxs-lookup"><span data-stu-id="694c2-155">No</span></span> | <span data-ttu-id="694c2-156">Evet</span><span class="sxs-lookup"><span data-stu-id="694c2-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="694c2-157">3. Runbook oluşturma</span><span class="sxs-lookup"><span data-stu-id="694c2-157">3. Create runbook</span></span>

<span data-ttu-id="694c2-158">Azure Otomasyonu, düzenlemek ve runbook'unuzu test hello portalında bir düzenleyici içerir.</span><span class="sxs-lookup"><span data-stu-id="694c2-158">Azure Automation has an editor in hello portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="694c2-159">Merhaba seçeneği toouse hello komut dosyası Düzenleyicisi toowork ile sahip [doğrudan PowerShell](../automation/automation-edit-textual-runbook.md) veya [grafik runbook oluşturma](../automation/automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="694c2-159">You have hello option toouse hello script editor toowork with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="694c2-160">Bu öğreticide, bir PowerShell Betiği ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="694c2-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Runbook’u düzenleme](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="694c2-162">Tooyour Otomasyon hesabı gidin.</span><span class="sxs-lookup"><span data-stu-id="694c2-162">Navigate tooyour Automation account.</span></span>  
2. <span data-ttu-id="694c2-163">Tıklatın **Runbook'lar** > **runbook Ekle** > **yeni bir runbook oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="694c2-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="694c2-164">Merhaba runbook ad için **toplama Otomasyon işleri**.</span><span class="sxs-lookup"><span data-stu-id="694c2-164">For hello runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="694c2-165">Merhaba runbook türü için **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="694c2-165">For hello runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="694c2-166">Tıklatın **oluşturma** toocreate hello runbook'u ve başlangıç hello Düzenleyici.</span><span class="sxs-lookup"><span data-stu-id="694c2-166">Click **Create** toocreate hello runbook and start hello editor.</span></span>
5. <span data-ttu-id="694c2-167">Merhaba runbook'a kod aşağıdaki hello kopyalayıp yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="694c2-167">Copy and paste hello following code into hello runbook.</span></span>  <span data-ttu-id="694c2-168">Merhaba betik toohello açıklamaları hello kod açıklaması için bakın.</span><span class="sxs-lookup"><span data-stu-id="694c2-168">Refer toohello comments in hello script for explanation of hello code.</span></span>
    
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


## <a name="4-test-runbook"></a><span data-ttu-id="694c2-169">4. Runbook sınaması</span><span class="sxs-lookup"><span data-stu-id="694c2-169">4. Test runbook</span></span>
<span data-ttu-id="694c2-170">Azure Otomasyonu içeren bir ortamda çok[runbook'unuzu test](../automation/automation-testing-runbook.md) yayımlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="694c2-170">Azure Automation includes an environment too[test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="694c2-171">Merhaba runbook tarafından toplanan hello verileri incelemek ve onu tooLog yayımlamadan önce beklendiği gibi Analytics tooproduction Yazar doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="694c2-171">You can inspect hello data collected by hello runbook and verify that it writes tooLog Analytics as expected before publishing it tooproduction.</span></span> 
 
![Runbook sınaması](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="694c2-173">Tıklatın **kaydetmek** toosave hello runbook.</span><span class="sxs-lookup"><span data-stu-id="694c2-173">Click **Save** toosave hello runbook.</span></span>
1. <span data-ttu-id="694c2-174">Tıklatın **Test bölmesi** hello test ortamında tooopen hello runbook.</span><span class="sxs-lookup"><span data-stu-id="694c2-174">Click **Test pane** tooopen hello runbook in hello test environment.</span></span>
3. <span data-ttu-id="694c2-175">Runbook parametreleri olduğundan, bunları istendiğinde tooenter değerlerini olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="694c2-175">Since your runbook has parameters, you're prompted tooenter values for them.</span></span>  <span data-ttu-id="694c2-176">Hello hello kaynak grubunun adını girin ve hello Otomasyon, devam eden toocollect iş bilgilerinizin hesabı.</span><span class="sxs-lookup"><span data-stu-id="694c2-176">Enter hello name of hello resource group and hello automation account that your going toocollect job information from.</span></span>
4. <span data-ttu-id="694c2-177">Tıklatın **Başlat** toohello hello runbook başlatın.</span><span class="sxs-lookup"><span data-stu-id="694c2-177">Click **Start** toohello start hello runbook.</span></span>
3. <span data-ttu-id="694c2-178">Merhaba runbook durumuyla başlayacak **sıraya alınan** çok geçmeden önce**çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="694c2-178">hello runbook will start with a status of **Queued** before it goes too**Running**.</span></span>  
3. <span data-ttu-id="694c2-179">Merhaba runbook ayrıntılı çıktıyı json biçiminde toplanan hello işleriyle görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="694c2-179">hello runbook should display verbose output with hello jobs collected in json format.</span></span>  <span data-ttu-id="694c2-180">Hiç iş listelenmiyorsa, ardından karşılaşılmış son bir saat hello hello automation hesabında oluşturulan iş yok.</span><span class="sxs-lookup"><span data-stu-id="694c2-180">If no jobs are listed, then there may have been no jobs created in hello automation account in hello last hour.</span></span>  <span data-ttu-id="694c2-181">Herhangi bir runbook hello automation hesabında başlatmayı deneyin ve hello test yeniden gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="694c2-181">Try starting any runbook in hello automation account and then perform hello test again.</span></span>
4. <span data-ttu-id="694c2-182">Merhaba çıktı hello hatalarını komutu tooLog Analytics sonrası göstermiyor emin olun.</span><span class="sxs-lookup"><span data-stu-id="694c2-182">Ensure that hello output doesn't show any errors in hello post command tooLog Analytics.</span></span>  <span data-ttu-id="694c2-183">İleti benzer toohello şunlara sahip olmanız.</span><span class="sxs-lookup"><span data-stu-id="694c2-183">You should have a message similar toohello following.</span></span>

    ![POST çıktı](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="694c2-185">5. Günlük analizi kayıtlarını doğrulama</span><span class="sxs-lookup"><span data-stu-id="694c2-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="694c2-186">Merhaba runbook testi tamamlandı ve hello çıkış başarıyla alındı doğrulandı sonra hello kayıtları kullanılarak oluşturulan doğrulayabilirsiniz bir [günlük analizi günlük aramada](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="694c2-186">Once hello runbook has completed in test, and you verified that hello output was successfully received, you can verify that hello records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![Günlük çıktısı](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="694c2-188">Hello Azure portal, günlük analizi çalışma alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="694c2-188">In hello Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="694c2-189">Tıklayın **oturum arama**.</span><span class="sxs-lookup"><span data-stu-id="694c2-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="694c2-190">Komutu aşağıdaki türü hello `Type=AutomationJob_CL` ve hello arama düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="694c2-190">Type hello following command `Type=AutomationJob_CL` and click hello search button.</span></span> <span data-ttu-id="694c2-191">Merhaba kayıt türü hello komut dosyasında belirlenmezse _CL içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="694c2-191">Note that hello record type includes _CL that isn't specified in hello script.</span></span>  <span data-ttu-id="694c2-192">Bu, özel günlük türü olduğunu otomatik olarak eklenen toohello günlük türü tooindicate sonekidir.</span><span class="sxs-lookup"><span data-stu-id="694c2-192">That suffix is automatically appended toohello log type tooindicate that it's a custom log type.</span></span>
4. <span data-ttu-id="694c2-193">Bu hello runbook beklendiği gibi çalıştığını gösteren döndürülen bir veya daha fazla kayıt görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="694c2-193">You should see one or more records returned indicating that hello runbook is working as expected.</span></span>


## <a name="6-publish-hello-runbook"></a><span data-ttu-id="694c2-194">6. Merhaba runbook yayımlama</span><span class="sxs-lookup"><span data-stu-id="694c2-194">6. Publish hello runbook</span></span>
<span data-ttu-id="694c2-195">Bu hello runbook düzgün çalıştığını doğruladıktan sonra toopublish gerekir, üretim ortamında çalışması için.</span><span class="sxs-lookup"><span data-stu-id="694c2-195">Once you've verified that hello runbook is working correctly, you need toopublish it so you can run it in production.</span></span>  <span data-ttu-id="694c2-196">Tooedit devam et ve hello yayımlanan sürümü değiştirmeden hello runbook'u test etme.</span><span class="sxs-lookup"><span data-stu-id="694c2-196">You can continue tooedit and test hello runbook without modifying hello published version.</span></span>  

![Runbook yayımlama](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="694c2-198">Tooyour Otomasyon hesabı döndür.</span><span class="sxs-lookup"><span data-stu-id="694c2-198">Return tooyour automation account.</span></span>
2. <span data-ttu-id="694c2-199">Tıklayın **Runbook'lar** seçip **toplama Otomasyon işleri**.</span><span class="sxs-lookup"><span data-stu-id="694c2-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="694c2-200">Tıklatın **Düzenle** ve ardından **yayımlama**.</span><span class="sxs-lookup"><span data-stu-id="694c2-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="694c2-201">Tıklatın **Evet** zaman toooverwrite hello daha önce istediğiniz sorulan tooverify yayımlanan sürümü.</span><span class="sxs-lookup"><span data-stu-id="694c2-201">Click **Yes** when asked tooverify that you want toooverwrite hello previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="694c2-202">7. Günlüğe kaydetme seçeneklerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="694c2-202">7. Set logging options</span></span> 
<span data-ttu-id="694c2-203">Test için mümkün tooview olan [ayrıntılı çıktı](../automation/automation-runbook-output-and-messages.md#message-streams) hello komut dosyasında hello $VerbosePreference değişkenini ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="694c2-203">For test, you were able tooview [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set hello $VerbosePreference variable in hello script.</span></span>  <span data-ttu-id="694c2-204">Üretim için tooview ayrıntılı çıktı istiyorsanız hello runbook tooset hello günlük özellikleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="694c2-204">For production, you need tooset hello logging properties for hello runbook if you want tooview verbose output.</span></span>  <span data-ttu-id="694c2-205">Bu öğreticide kullanılan hello runbook için bu tooLog Analytics gönderilen hello json verilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="694c2-205">For hello runbook used in this tutorial, this will display hello json data being sent tooLog Analytics.</span></span>

![Günlüğe kaydetme ve izleme](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="694c2-207">Runbook'unuzda hello özelliklerinde seçin **günlüğe kaydetme ve izleme** altında **Runbook ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="694c2-207">In hello properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="694c2-208">Değiştirmek için hello ayar **ayrıntılı kayıtları günlüğe** çok**üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="694c2-208">Change hello setting for **Log verbose records** too**On**.</span></span>
3. <span data-ttu-id="694c2-209">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="694c2-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="694c2-210">8. Runbook zamanlama</span><span class="sxs-lookup"><span data-stu-id="694c2-210">8. Schedule runbook</span></span>
<span data-ttu-id="694c2-211">Merhaba en yaygın şekilde toostart izleme verilerini toplayan bir runbook olan tooschedule, toorun otomatik olarak.</span><span class="sxs-lookup"><span data-stu-id="694c2-211">hello most common way toostart a runbook that collects monitoring data is tooschedule it toorun automatically.</span></span>  <span data-ttu-id="694c2-212">Oluşturarak bunu bir [Azure Otomasyonu zamanlama](../automation/automation-schedules.md) ve tooyour runbook ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="694c2-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it tooyour runbook.</span></span>

![Runbook zamanlama](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="694c2-214">Runbook'unuzda Hello özelliklerinde seçin **zamanlamaları** altında **kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="694c2-214">In hello properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="694c2-215">Tıklatın **bir zamanlama Ekle** > **bir zamanlama tooyour runbook bağlantı** > **yeni bir zamanlama oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="694c2-215">Click **Add a schedule** > **Link a schedule tooyour runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="694c2-216">Merhaba zamanlama ve tıklatın değerlerini aşağıdaki hello türü **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="694c2-216">Type in hello following values for hello schedule and click **Create**.</span></span>

| <span data-ttu-id="694c2-217">Özellik</span><span class="sxs-lookup"><span data-stu-id="694c2-217">Property</span></span> | <span data-ttu-id="694c2-218">Değer</span><span class="sxs-lookup"><span data-stu-id="694c2-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="694c2-219">Ad</span><span class="sxs-lookup"><span data-stu-id="694c2-219">Name</span></span> | <span data-ttu-id="694c2-220">AutomationJobs saatlik</span><span class="sxs-lookup"><span data-stu-id="694c2-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="694c2-221">Başlatır</span><span class="sxs-lookup"><span data-stu-id="694c2-221">Starts</span></span> | <span data-ttu-id="694c2-222">En az 5 dakika geçmiş geçerli saati hello saati seçin.</span><span class="sxs-lookup"><span data-stu-id="694c2-222">Select any time at least 5 minutes past hello current time.</span></span> |
| <span data-ttu-id="694c2-223">Yineleme</span><span class="sxs-lookup"><span data-stu-id="694c2-223">Recurrence</span></span> | <span data-ttu-id="694c2-224">Yinelenen</span><span class="sxs-lookup"><span data-stu-id="694c2-224">Recurring</span></span> |
| <span data-ttu-id="694c2-225">Tekrarlamayı her</span><span class="sxs-lookup"><span data-stu-id="694c2-225">Recur every</span></span> | <span data-ttu-id="694c2-226">1 saat</span><span class="sxs-lookup"><span data-stu-id="694c2-226">1 hour</span></span> |
| <span data-ttu-id="694c2-227">Kümesi süre sonu</span><span class="sxs-lookup"><span data-stu-id="694c2-227">Set expiration</span></span> | <span data-ttu-id="694c2-228">Hayır</span><span class="sxs-lookup"><span data-stu-id="694c2-228">No</span></span> |

<span data-ttu-id="694c2-229">Merhaba zamanlama oluşturulduktan sonra bu zamanlamayı hello runbook her başlatıldığında kullanılacak tooset hello parametre değerlerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="694c2-229">Once hello schedule is created, you need tooset hello parameter values that will be used each time this schedule starts hello runbook.</span></span>

6. <span data-ttu-id="694c2-230">Tıklatın **parametreleri yapılandırmak ve çalıştırma ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="694c2-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="694c2-231">Değerlerini doldurun, **ResourceGroupName** ve **AutomationAccountName**.</span><span class="sxs-lookup"><span data-stu-id="694c2-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="694c2-232">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="694c2-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="694c2-233">9. Zamanlama runbook başlatır doğrulayın</span><span class="sxs-lookup"><span data-stu-id="694c2-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="694c2-234">Bir runbook başlatıldığında, her [bir iş oluşturulur](../automation/automation-runbook-execution.md) ve oturum herhangi bir çıktı.</span><span class="sxs-lookup"><span data-stu-id="694c2-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="694c2-235">Aslında, runbook hello aynı işleri toplama hello bunlar.</span><span class="sxs-lookup"><span data-stu-id="694c2-235">In fact, these are hello same jobs that hello runbook is collecting.</span></span>  <span data-ttu-id="694c2-236">Merhaba hello zamanlama için başlangıç saatini geçtikten sonra hello runbook için hello işleri denetleyerek beklendiği gibi bu hello runbook başlatır doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="694c2-236">You can verify that hello runbook starts as expected by checking hello jobs for hello runbook after hello start time for hello schedule has passed.</span></span>

![İşler](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="694c2-238">Runbook'unuzda Hello özelliklerinde seçin **işleri** altında **kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="694c2-238">In hello properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="694c2-239">Her zaman hello runbook için iş listesini başlatıldığından görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="694c2-239">You should see a listing of jobs for each time hello runbook was started.</span></span>
3. <span data-ttu-id="694c2-240">Merhaba işleri tooview birini ayrıntılarını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="694c2-240">Click on one of hello jobs tooview its details.</span></span>
4. <span data-ttu-id="694c2-241">Tıklayın **tüm günlükleri** tooview hello günlükleri ve hello runbook'tan çıkış.</span><span class="sxs-lookup"><span data-stu-id="694c2-241">Click on **All logs** tooview hello logs and output from hello runbook.</span></span>
5. <span data-ttu-id="694c2-242">Toohello alt toofind bir giriş benzer toohello aşağıdaki görüntü kaydırın.</span><span class="sxs-lookup"><span data-stu-id="694c2-242">Scroll toohello bottom toofind an entry similar toohello image below.</span></span><br>![Ayrıntılı](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="694c2-244">Bu girişinde'ı tıklatın tooview hello ayrıntılı tooLog Analytics gönderilen json verilerini.</span><span class="sxs-lookup"><span data-stu-id="694c2-244">Click on this entry tooview hello detailed json data  that was sent tooLog Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="694c2-245">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="694c2-245">Next steps</span></span>
- <span data-ttu-id="694c2-246">Kullanım [Görünüm Tasarımcısı](../log-analytics/log-analytics-view-designer.md) görüntüleyen bir görünüm toocreate hello veri toohello günlük analizi deposu derledik.</span><span class="sxs-lookup"><span data-stu-id="694c2-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) toocreate a view displaying hello data that you've collected toohello Log Analytics repository.</span></span>
- <span data-ttu-id="694c2-247">Runbook'unuzda paketini bir [yönetim çözümü](operations-management-suite-solutions-creating.md) toodistribute toocustomers.</span><span class="sxs-lookup"><span data-stu-id="694c2-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) toodistribute toocustomers.</span></span>
- <span data-ttu-id="694c2-248">Daha fazla bilgi edinmek [günlük analizi](https://docs.microsoft.com/azure/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="694c2-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="694c2-249">Daha fazla bilgi edinmek [Azure Otomasyonu](https://docs.microsoft.com/azure/automation/).</span><span class="sxs-lookup"><span data-stu-id="694c2-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="694c2-250">Merhaba hakkında daha fazla bilgi [HTTP veri toplayıcı API](../log-analytics/log-analytics-data-collector-api.md).</span><span class="sxs-lookup"><span data-stu-id="694c2-250">Learn more about hello [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>
