---
title: "İle Azure Automation runbook günlük analizi veri toplama | Microsoft Docs"
description: "Adım adım öğretici, Azure Automation'ın günlük analizi tarafından analiz için OMS depoya verileri toplamak için bir runbook oluşturmada size yol göstermektedir."
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
ms.openlocfilehash: 59f674c9c6404da7f5384539189f41a4ba1a939a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="b4a54-103">Günlük analizi olarak toplamak ve bir Azure Otomasyonu runbook'u</span><span class="sxs-lookup"><span data-stu-id="b4a54-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="b4a54-104">Günlük analizi veri önemli miktarda bir çeşitli kaynaklardan dahil olmak üzere toplayabilirsiniz [veri kaynakları](../log-analytics/log-analytics-data-sources.md) aracılar üzerinde hem de [Azure'dan toplanan veriler](../log-analytics/log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b4a54-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="b4a54-105">Burada veri toplamanız gerekir, bu standart kaynakları aracılığıyla erişilebilir değil ancak bir senaryo vardır.</span><span class="sxs-lookup"><span data-stu-id="b4a54-105">There are a scenarios though where you need to collect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="b4a54-106">Bu durumlarda, kullandığınız [HTTP veri toplayıcı API](../log-analytics/log-analytics-data-collector-api.md) herhangi bir REST API istemciden için günlük analizi veri yazmak için.</span><span class="sxs-lookup"><span data-stu-id="b4a54-106">In these cases, you can use the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) to write data to Log Analytics from any REST API client.</span></span>  <span data-ttu-id="b4a54-107">Bu veri toplama gerçekleştirmek için ortak bir yöntemi, Azure Automation'da bir runbook kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="b4a54-107">A common method to perform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="b4a54-108">Bu öğreticide oluşturma ve bir runbook için günlük analizi veri yazmak için Azure automation'da zamanlama işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b4a54-108">This tutorial walks through the process for creating and scheduling a runbook in Azure Automation to write data to Log Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b4a54-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b4a54-109">Prerequisites</span></span>
<span data-ttu-id="b4a54-110">Bu senaryo, Azure aboneliğinizde yapılandırılmış aşağıdaki kaynaklara gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b4a54-110">This scenario requires the following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="b4a54-111">Her ikisi de ücretsiz bir hesap olabilir.</span><span class="sxs-lookup"><span data-stu-id="b4a54-111">Both can be a free account.</span></span>

- <span data-ttu-id="b4a54-112">[Günlük analizi çalışma alanı](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b4a54-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="b4a54-113">[Azure Otomasyon hesabı](../automation/automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b4a54-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="b4a54-114">Senaryoya genel bakış</span><span class="sxs-lookup"><span data-stu-id="b4a54-114">Overview of scenario</span></span>
<span data-ttu-id="b4a54-115">Bu öğretici için Otomasyon işleri hakkında bilgi toplar bir runbook yazacaksınız.</span><span class="sxs-lookup"><span data-stu-id="b4a54-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="b4a54-116">Azure Otomasyonu runbook'ları yazma ve komut dosyası Azure Otomasyon Düzenleyicisi'nde test tarafından başlayacaksınız şekilde PowerShell ile uygulanır.</span><span class="sxs-lookup"><span data-stu-id="b4a54-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in the Azure Automation editor.</span></span>  <span data-ttu-id="b4a54-117">Gerekli bilgileri topladığınız doğrulayın sonra bu veri yazmak için günlük analizi ve özel veri türü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b4a54-117">Once you verify that you're collecting the required information, you'll write that data to Log Analytics and verify the custom data type.</span></span>  <span data-ttu-id="b4a54-118">Son olarak, düzenli aralıklarla runbook'u başlatmak için bir zamanlama oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="b4a54-118">Finally, you'll create a schedule to start the runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="b4a54-119">Azure Otomasyonu işi bilgisi bu runbook için günlük analizi göndermek için yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4a54-119">You can configure Azure Automation to send job information to Log Analytics without this runbook.</span></span>  <span data-ttu-id="b4a54-120">Bu senaryoda öncelikle öğretici desteklemek için kullanılır ve test çalışma alanına verileri gönder önerilir.</span><span class="sxs-lookup"><span data-stu-id="b4a54-120">This scenario is primarily used to support the tutorial, and it's recommended that you send the data to a test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="b4a54-121">1. Veri Toplayıcı API modülünü yükleme</span><span class="sxs-lookup"><span data-stu-id="b4a54-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="b4a54-122">Her [HTTP veri toplayıcı API isteğinden](../log-analytics/log-analytics-data-collector-api.md#create-a-request) uygun şekilde biçimlendirilmiş olması gerekir ve bir authorization üstbilgisi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b4a54-122">Every [request from the HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="b4a54-123">Bunu runbook'unuzda yapabilirsiniz ancak bu işlemi basitleştirir bir modül kullanarak gerekli kod miktarını düşürebilir.</span><span class="sxs-lookup"><span data-stu-id="b4a54-123">You can do this in your runbook, but you can reduce the amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="b4a54-124">Kullanabileceğiniz bir modül [OMSIngestionAPI Modülü](https://www.powershellgallery.com/packages/OMSIngestionAPI) PowerShell galerisinde.</span><span class="sxs-lookup"><span data-stu-id="b4a54-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in the PowerShell Gallery.</span></span>

<span data-ttu-id="b4a54-125">Kullanılacak bir [Modülü](../automation/automation-integration-modules.md) bir runbook'ta Otomasyon hesabınızda yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="b4a54-125">To use a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="b4a54-126">Aynı hesapta herhangi bir runbook, ardından modülünde işlevlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4a54-126">Any runbook in the same account can then use the functions in the module.</span></span>  <span data-ttu-id="b4a54-127">Yeni bir modül seçerek yükleyebilirsiniz **varlıklar** > **modülleri** > **bir modül Ekle** Otomasyon hesabınızda.</span><span class="sxs-lookup"><span data-stu-id="b4a54-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="b4a54-128">PowerShell Galerisi yine de Bu öğretici için bu seçeneği kullanabilmeniz için bir modül Otomasyon hesabınızı doğrudan dağıtmak için hızlı bir seçeneği sunar.</span><span class="sxs-lookup"><span data-stu-id="b4a54-128">The PowerShell Gallery though gives you a quick option to deploy a module directly to your automation account so you can use that option for this tutorial.</span></span>  

![OMSIngestionAPI Modülü](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="b4a54-130">Git [PowerShell Galerisi](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="b4a54-130">Go to [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="b4a54-131">Arama **OMSIngestionAPI**.</span><span class="sxs-lookup"><span data-stu-id="b4a54-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="b4a54-132">Tıklayın **Azure Otomasyonu Dağıt** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b4a54-132">Click on the **Deploy to Azure Automation** button.</span></span>
4. <span data-ttu-id="b4a54-133">Otomasyon hesabınızı seçin ve tıklatın **Tamam** modülünü yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="b4a54-133">Select your automation account and click **OK** to install the module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="b4a54-134">2. Otomasyon değişkenleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="b4a54-134">2. Create Automation variables</span></span>
<span data-ttu-id="b4a54-135">[Otomasyon değişkenleri](..\automation\automation-variables.md) Otomasyon hesabınızda tüm runbook'lar tarafından kullanılan değerleri tutun.</span><span class="sxs-lookup"><span data-stu-id="b4a54-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="b4a54-136">Runbook'ları gerçek runbook düzenleme olmadan bu değerleri değiştirmek olanak sağlayarak daha esnek hale.</span><span class="sxs-lookup"><span data-stu-id="b4a54-136">They make runbooks more flexible by allowing you to change these values without editing the actual runbook.</span></span> <span data-ttu-id="b4a54-137">HTTP veri toplayıcı API'sinden her istek kimliği ve anahtarı OMS çalışma alanının gerektirir ve bu bilgileri depolamak değişken varlıkları idealdir.</span><span class="sxs-lookup"><span data-stu-id="b4a54-137">Every request from the HTTP Data Collector API requires the ID and key of the OMS workspace, and variable assets are ideal to store this information.</span></span>  

![Değişkenler](media/operations-management-suite-runbook-datacollect/variables.png)

1. <span data-ttu-id="b4a54-139">Azure Portal'da, Automation hesabınızı gidin.</span><span class="sxs-lookup"><span data-stu-id="b4a54-139">In the Azure portal, navigate to your Automation account.</span></span>
2. <span data-ttu-id="b4a54-140">Seçin **değişkenleri** altında **paylaşılan kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="b4a54-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="b4a54-141">Tıklatın **değişken Ekle** ve aşağıdaki tabloda iki değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b4a54-141">Click **Add a variable** and create the two variables in the following table.</span></span>

| <span data-ttu-id="b4a54-142">Özellik</span><span class="sxs-lookup"><span data-stu-id="b4a54-142">Property</span></span> | <span data-ttu-id="b4a54-143">Çalışma alanı kimliği değeri</span><span class="sxs-lookup"><span data-stu-id="b4a54-143">Workspace ID Value</span></span> | <span data-ttu-id="b4a54-144">Çalışma alanı anahtarı değeri</span><span class="sxs-lookup"><span data-stu-id="b4a54-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="b4a54-145">Ad</span><span class="sxs-lookup"><span data-stu-id="b4a54-145">Name</span></span> | <span data-ttu-id="b4a54-146">Workspaceıd</span><span class="sxs-lookup"><span data-stu-id="b4a54-146">WorkspaceId</span></span> | <span data-ttu-id="b4a54-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="b4a54-147">WorkspaceKey</span></span> |
| <span data-ttu-id="b4a54-148">Tür</span><span class="sxs-lookup"><span data-stu-id="b4a54-148">Type</span></span> | <span data-ttu-id="b4a54-149">Dize</span><span class="sxs-lookup"><span data-stu-id="b4a54-149">String</span></span> | <span data-ttu-id="b4a54-150">Dize</span><span class="sxs-lookup"><span data-stu-id="b4a54-150">String</span></span> |
| <span data-ttu-id="b4a54-151">Değer</span><span class="sxs-lookup"><span data-stu-id="b4a54-151">Value</span></span> | <span data-ttu-id="b4a54-152">Günlük analizi çalışma alanınız çalışma Kimliğinde yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b4a54-152">Paste in the Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="b4a54-153">Yapıştırma oturum birincil veya ikincil anahtarı günlük analizi çalışma alanınızın.</span><span class="sxs-lookup"><span data-stu-id="b4a54-153">Paste in with the Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="b4a54-154">Şifreli</span><span class="sxs-lookup"><span data-stu-id="b4a54-154">Encrypted</span></span> | <span data-ttu-id="b4a54-155">Hayır</span><span class="sxs-lookup"><span data-stu-id="b4a54-155">No</span></span> | <span data-ttu-id="b4a54-156">Evet</span><span class="sxs-lookup"><span data-stu-id="b4a54-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="b4a54-157">3. Runbook oluşturma</span><span class="sxs-lookup"><span data-stu-id="b4a54-157">3. Create runbook</span></span>

<span data-ttu-id="b4a54-158">Azure Otomasyonu, düzenlemek ve runbook'unuzu test portalında bir düzenleyici içerir.</span><span class="sxs-lookup"><span data-stu-id="b4a54-158">Azure Automation has an editor in the portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="b4a54-159">Çalışmak için komut dosyası Düzenleyicisi'ni kullanmak için seçeneğiniz [doğrudan PowerShell](../automation/automation-edit-textual-runbook.md) veya [grafik runbook oluşturma](../automation/automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="b4a54-159">You have the option to use the script editor to work with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="b4a54-160">Bu öğreticide, bir PowerShell Betiği ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="b4a54-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Runbook’u düzenleme](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="b4a54-162">Otomasyon hesabınıza gidin.</span><span class="sxs-lookup"><span data-stu-id="b4a54-162">Navigate to your Automation account.</span></span>  
2. <span data-ttu-id="b4a54-163">Tıklatın **Runbook'lar** > **runbook Ekle** > **yeni bir runbook oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="b4a54-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="b4a54-164">Runbook ad için **toplama Otomasyon işleri**.</span><span class="sxs-lookup"><span data-stu-id="b4a54-164">For the runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="b4a54-165">Runbook türü için **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b4a54-165">For the runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="b4a54-166">Tıklatın **oluşturma** runbook oluşturma ve Düzenleyicisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="b4a54-166">Click **Create** to create the runbook and start the editor.</span></span>
5. <span data-ttu-id="b4a54-167">Aşağıdaki kodu kopyalayıp runbook'a yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b4a54-167">Copy and paste the following code into the runbook.</span></span>  <span data-ttu-id="b4a54-168">Kod açıklaması için komut dosyası yer alan yorumlara bakın.</span><span class="sxs-lookup"><span data-stu-id="b4a54-168">Refer to the comments in the script for explanation of the code.</span></span>
    
        # Get information required for the automation account from parameter values when the runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate to the Automation account using the Azure connection created when the Automation account was created.
        # Code copied from the runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set the $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set the name of the record type.
        $logType = "AutomationJob"
        
        # Get the jobs from the past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert the job data to json
            $body = $jobs | ConvertTo-Json
        
            # Write the body to verbose output so we can inspect it if verbose logging is on for the runbook.
            Write-Verbose $body
        
            # Send the data to Log Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="b4a54-169">4. Runbook sınaması</span><span class="sxs-lookup"><span data-stu-id="b4a54-169">4. Test runbook</span></span>
<span data-ttu-id="b4a54-170">Azure Otomasyonu içeren bir ortama [runbook'unuzu test](../automation/automation-testing-runbook.md) yayımlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="b4a54-170">Azure Automation includes an environment to [test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="b4a54-171">Runbook tarafından toplanan verileri incelemek ve üretim yayımlamadan önce beklendiği gibi günlük analizi Yazar olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b4a54-171">You can inspect the data collected by the runbook and verify that it writes to Log Analytics as expected before publishing it to production.</span></span> 
 
![Runbook sınaması](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="b4a54-173">Tıklatın **kaydetmek** runbook'u kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="b4a54-173">Click **Save** to save the runbook.</span></span>
1. <span data-ttu-id="b4a54-174">Tıklatın **Test bölmesi** runbook test ortamında açın.</span><span class="sxs-lookup"><span data-stu-id="b4a54-174">Click **Test pane** to open the runbook in the test environment.</span></span>
3. <span data-ttu-id="b4a54-175">Runbook parametreleri olduğundan, bunlar için değerler girin istenir.</span><span class="sxs-lookup"><span data-stu-id="b4a54-175">Since your runbook has parameters, you're prompted to enter values for them.</span></span>  <span data-ttu-id="b4a54-176">Kaynak grubunun adını girin ve automation hesabı, iş bilgilerini toplamak için olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b4a54-176">Enter the name of the resource group and the automation account that your going to collect job information from.</span></span>
4. <span data-ttu-id="b4a54-177">Tıklatın **Başlat** runbook'u başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="b4a54-177">Click **Start** to the start the runbook.</span></span>
3. <span data-ttu-id="b4a54-178">Runbook durumu ile başlar **sıraya alınan** için geçmeden önce **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="b4a54-178">The runbook will start with a status of **Queued** before it goes to **Running**.</span></span>  
3. <span data-ttu-id="b4a54-179">Json biçiminde toplanan işleri ile runbook ayrıntılı çıktı görüntülemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4a54-179">The runbook should display verbose output with the jobs collected in json format.</span></span>  <span data-ttu-id="b4a54-180">Hiç iş listelenmiyorsa, ardından karşılaşılmış son bir saatte automation hesabında oluşturulan iş yok.</span><span class="sxs-lookup"><span data-stu-id="b4a54-180">If no jobs are listed, then there may have been no jobs created in the automation account in the last hour.</span></span>  <span data-ttu-id="b4a54-181">Herhangi bir runbook Otomasyon hesabında başlatmayı deneyin ve test yeniden gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="b4a54-181">Try starting any runbook in the automation account and then perform the test again.</span></span>
4. <span data-ttu-id="b4a54-182">Çıktı için günlük analizi post komutta hataları göstermez emin olun.</span><span class="sxs-lookup"><span data-stu-id="b4a54-182">Ensure that the output doesn't show any errors in the post command to Log Analytics.</span></span>  <span data-ttu-id="b4a54-183">Aşağıdakine benzer bir ileti olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b4a54-183">You should have a message similar to the following.</span></span>

    ![POST çıktı](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="b4a54-185">5. Günlük analizi kayıtlarını doğrulama</span><span class="sxs-lookup"><span data-stu-id="b4a54-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="b4a54-186">Runbook testi tamamlandı ve çıktı başarıyla alındı doğruladıktan sonra kayıtları kullanılarak oluşturulan doğrulayabilirsiniz bir [günlük analizi günlük aramada](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="b4a54-186">Once the runbook has completed in test, and you verified that the output was successfully received, you can verify that the records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![Günlük çıktısı](media/operations-management-suite-runbook-datacollect/log-output.png)

1. <span data-ttu-id="b4a54-188">Azure portalında günlük analizi çalışma alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="b4a54-188">In the Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="b4a54-189">Tıklayın **oturum arama**.</span><span class="sxs-lookup"><span data-stu-id="b4a54-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="b4a54-190">Aşağıdaki komutu yazın `Type=AutomationJob_CL` ve arama düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b4a54-190">Type the following command `Type=AutomationJob_CL` and click the search button.</span></span> <span data-ttu-id="b4a54-191">Kayıt türü betik belirlenmezse _CL içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b4a54-191">Note that the record type includes _CL that isn't specified in the script.</span></span>  <span data-ttu-id="b4a54-192">Bu soneki özel günlük türü olduğunu belirtmek için günlük türü otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="b4a54-192">That suffix is automatically appended to the log type to indicate that it's a custom log type.</span></span>
4. <span data-ttu-id="b4a54-193">Runbook beklendiği gibi çalıştığını gösteren döndürülen bir veya daha fazla kayıt görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4a54-193">You should see one or more records returned indicating that the runbook is working as expected.</span></span>


## <a name="6-publish-the-runbook"></a><span data-ttu-id="b4a54-194">6. Runbook yayımlama</span><span class="sxs-lookup"><span data-stu-id="b4a54-194">6. Publish the runbook</span></span>
<span data-ttu-id="b4a54-195">Runbook düzgün çalıştığını doğruladıktan sonra üretim ortamında çalışması için yayımlayın gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4a54-195">Once you've verified that the runbook is working correctly, you need to publish it so you can run it in production.</span></span>  <span data-ttu-id="b4a54-196">Düzenle ve yayımlanan sürümü değiştirmeden runbook'u test devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4a54-196">You can continue to edit and test the runbook without modifying the published version.</span></span>  

![Runbook yayımlama](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="b4a54-198">Otomasyon hesabınızı döndür.</span><span class="sxs-lookup"><span data-stu-id="b4a54-198">Return to your automation account.</span></span>
2. <span data-ttu-id="b4a54-199">Tıklayın **Runbook'lar** seçip **toplama Otomasyon işleri**.</span><span class="sxs-lookup"><span data-stu-id="b4a54-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="b4a54-200">Tıklatın **Düzenle** ve ardından **yayımlama**.</span><span class="sxs-lookup"><span data-stu-id="b4a54-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="b4a54-201">Tıklatın **Evet** önceden yayımlanmış sürümün üzerine istediğinizi doğrulamanız istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="b4a54-201">Click **Yes** when asked to verify that you want to overwrite the previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="b4a54-202">7. Günlüğe kaydetme seçeneklerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="b4a54-202">7. Set logging options</span></span> 
<span data-ttu-id="b4a54-203">Test için görmeye [ayrıntılı çıktı](../automation/automation-runbook-output-and-messages.md#message-streams) komut dosyasında $VerbosePreference değişkenini olduğundan.</span><span class="sxs-lookup"><span data-stu-id="b4a54-203">For test, you were able to view [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set the $VerbosePreference variable in the script.</span></span>  <span data-ttu-id="b4a54-204">Üretim için ayrıntılı çıktı görüntülemek istiyorsanız runbook için günlük özelliklerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4a54-204">For production, you need to set the logging properties for the runbook if you want to view verbose output.</span></span>  <span data-ttu-id="b4a54-205">Bu öğreticide kullanılan runbook için bu günlük analizi için gönderilen json verilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b4a54-205">For the runbook used in this tutorial, this will display the json data being sent to Log Analytics.</span></span>

![Günlüğe kaydetme ve izleme](media/operations-management-suite-runbook-datacollect/logging.png)

1. <span data-ttu-id="b4a54-207">Runbook'unuzda özelliklerinde seçin **günlüğe kaydetme ve izleme** altında **Runbook ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="b4a54-207">In the properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="b4a54-208">Ayarını değiştirmek **ayrıntılı kayıtları günlüğe** için **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="b4a54-208">Change the setting for **Log verbose records** to **On**.</span></span>
3. <span data-ttu-id="b4a54-209">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b4a54-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="b4a54-210">8. Runbook zamanlama</span><span class="sxs-lookup"><span data-stu-id="b4a54-210">8. Schedule runbook</span></span>
<span data-ttu-id="b4a54-211">İzleme verilerini toplayan bir runbook'u başlatmak için en yaygın otomatik olarak çalışacak şekilde zamanlamak için yoludur.</span><span class="sxs-lookup"><span data-stu-id="b4a54-211">The most common way to start a runbook that collects monitoring data is to schedule it to run automatically.</span></span>  <span data-ttu-id="b4a54-212">Oluşturarak bunu bir [Azure Otomasyonu zamanlama](../automation/automation-schedules.md) ve runbook'a ekleme.</span><span class="sxs-lookup"><span data-stu-id="b4a54-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it to your runbook.</span></span>

![Runbook zamanlama](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="b4a54-214">Runbook'unuzda özelliklerini seçin **zamanlamaları** altında **kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="b4a54-214">In the properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="b4a54-215">Tıklatın **bir zamanlama Ekle** > **runbook'a bir zamanlama Bağla** > **yeni bir zamanlama oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="b4a54-215">Click **Add a schedule** > **Link a schedule to your runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="b4a54-216">Zamanlama için aşağıdaki değerleri yazın ve'ı tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="b4a54-216">Type in the following values for the schedule and click **Create**.</span></span>

| <span data-ttu-id="b4a54-217">Özellik</span><span class="sxs-lookup"><span data-stu-id="b4a54-217">Property</span></span> | <span data-ttu-id="b4a54-218">Değer</span><span class="sxs-lookup"><span data-stu-id="b4a54-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="b4a54-219">Ad</span><span class="sxs-lookup"><span data-stu-id="b4a54-219">Name</span></span> | <span data-ttu-id="b4a54-220">AutomationJobs saatlik</span><span class="sxs-lookup"><span data-stu-id="b4a54-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="b4a54-221">Başlatır</span><span class="sxs-lookup"><span data-stu-id="b4a54-221">Starts</span></span> | <span data-ttu-id="b4a54-222">Herhangi bir geçerli saati aşan en az 5 dakika zaman'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b4a54-222">Select any time at least 5 minutes past the current time.</span></span> |
| <span data-ttu-id="b4a54-223">Yineleme</span><span class="sxs-lookup"><span data-stu-id="b4a54-223">Recurrence</span></span> | <span data-ttu-id="b4a54-224">Yinelenen</span><span class="sxs-lookup"><span data-stu-id="b4a54-224">Recurring</span></span> |
| <span data-ttu-id="b4a54-225">Tekrarlamayı her</span><span class="sxs-lookup"><span data-stu-id="b4a54-225">Recur every</span></span> | <span data-ttu-id="b4a54-226">1 saat</span><span class="sxs-lookup"><span data-stu-id="b4a54-226">1 hour</span></span> |
| <span data-ttu-id="b4a54-227">Kümesi süre sonu</span><span class="sxs-lookup"><span data-stu-id="b4a54-227">Set expiration</span></span> | <span data-ttu-id="b4a54-228">Hayır</span><span class="sxs-lookup"><span data-stu-id="b4a54-228">No</span></span> |

<span data-ttu-id="b4a54-229">Zamanlama oluşturulduktan sonra bu zamanlamanın runbook her başlatıldığında kullanılacak parametre değerlerini ayarlamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4a54-229">Once the schedule is created, you need to set the parameter values that will be used each time this schedule starts the runbook.</span></span>

6. <span data-ttu-id="b4a54-230">Tıklatın **parametreleri yapılandırmak ve çalıştırma ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="b4a54-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="b4a54-231">Değerlerini doldurun, **ResourceGroupName** ve **AutomationAccountName**.</span><span class="sxs-lookup"><span data-stu-id="b4a54-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="b4a54-232">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b4a54-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="b4a54-233">9. Zamanlama runbook başlatır doğrulayın</span><span class="sxs-lookup"><span data-stu-id="b4a54-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="b4a54-234">Bir runbook başlatıldığında, her [bir iş oluşturulur](../automation/automation-runbook-execution.md) ve oturum herhangi bir çıktı.</span><span class="sxs-lookup"><span data-stu-id="b4a54-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="b4a54-235">Aslında, runbook toplama aynı işleri bunlar.</span><span class="sxs-lookup"><span data-stu-id="b4a54-235">In fact, these are the same jobs that the runbook is collecting.</span></span>  <span data-ttu-id="b4a54-236">Runbook zamanlama için başlangıç saatini geçtikten sonra runbook için iş denetleyerek beklendiği gibi başlatır doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4a54-236">You can verify that the runbook starts as expected by checking the jobs for the runbook after the start time for the schedule has passed.</span></span>

![İşler](media/operations-management-suite-runbook-datacollect/jobs.png)

1. <span data-ttu-id="b4a54-238">Runbook'unuzda özelliklerini seçin **işleri** altında **kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="b4a54-238">In the properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="b4a54-239">İşlerin listesini runbook başlatıldığında her zaman için görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4a54-239">You should see a listing of jobs for each time the runbook was started.</span></span>
3. <span data-ttu-id="b4a54-240">Ayrıntılarını görüntülemek için işleri birini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b4a54-240">Click on one of the jobs to view its details.</span></span>
4. <span data-ttu-id="b4a54-241">Tıklayın **tüm günlükleri** günlükleri görüntülemek ve runbook'tan çıkış.</span><span class="sxs-lookup"><span data-stu-id="b4a54-241">Click on **All logs** to view the logs and output from the runbook.</span></span>
5. <span data-ttu-id="b4a54-242">Bir giriş aşağıdaki görüntü benzer bulmak için aşağıya kaydırın.</span><span class="sxs-lookup"><span data-stu-id="b4a54-242">Scroll to the bottom to find an entry similar to the image below.</span></span><br>![Ayrıntılı](media/operations-management-suite-runbook-datacollect/verbose.png)
6. <span data-ttu-id="b4a54-244">Günlük analizi için gönderilen ayrıntılı json verilerini görüntülemek için bu giriş'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b4a54-244">Click on this entry to view the detailed json data  that was sent to Log Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="b4a54-245">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b4a54-245">Next steps</span></span>
- <span data-ttu-id="b4a54-246">Kullanım [Görünüm Tasarımcısı](../log-analytics/log-analytics-view-designer.md) günlük analizi depoya derledik verileri görüntüleyen bir görünüm oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="b4a54-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) to create a view displaying the data that you've collected to the Log Analytics repository.</span></span>
- <span data-ttu-id="b4a54-247">Runbook'unuzda paketini bir [yönetim çözümü](operations-management-suite-solutions-creating.md) müşterilere dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="b4a54-247">Package your runbook in a [management solution](operations-management-suite-solutions-creating.md) to distribute to customers.</span></span>
- <span data-ttu-id="b4a54-248">Daha fazla bilgi edinmek [günlük analizi](https://docs.microsoft.com/azure/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="b4a54-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="b4a54-249">Daha fazla bilgi edinmek [Azure Otomasyonu](https://docs.microsoft.com/azure/automation/).</span><span class="sxs-lookup"><span data-stu-id="b4a54-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="b4a54-250">Daha fazla bilgi edinmek [HTTP veri toplayıcı API](../log-analytics/log-analytics-data-collector-api.md).</span><span class="sxs-lookup"><span data-stu-id="b4a54-250">Learn more about the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>