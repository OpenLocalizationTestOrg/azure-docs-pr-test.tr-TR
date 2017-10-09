---
title: Azure Otomasyonu Visual Stuido Team Services kaynak denetimi ile aaaIntegrate | Microsoft Docs
description: "Senaryo, bir Azure Otomasyonu hesabı ve Visual Stuido Team Services kaynak denetimi tümleştirmesi kurma açıklanmaktadır."
services: automation
documentationcenter: 
author: eamono
manager: 
editor: 
keywords: Azure powershell, VSTS, kaynak denetimi, Otomasyon
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.openlocfilehash: 8f6faa596a5ad1f8b72e820ca320b3e103d83579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a><span data-ttu-id="fdd73-104">Azure otomasyonu senaryosu - Visual Studio Team Services ile Otomasyon kaynak denetimi tümleştirme</span><span class="sxs-lookup"><span data-stu-id="fdd73-104">Azure Automation scenario - Automation source control integration with Visual Studio Team Services</span></span>

<span data-ttu-id="fdd73-105">Bu senaryoda, toomanage Azure Otomasyon çalışma kitabı ya da kaynak denetimi altındaki DSC yapılandırmaları kullanmakta olduğunuz bir Visual Studio Team Services projesi vardır.</span><span class="sxs-lookup"><span data-stu-id="fdd73-105">In this scenario, you have a Visual Studio Team Services project that you are using toomanage Azure Automation runbooks or DSC configurations under source control.</span></span>
<span data-ttu-id="fdd73-106">Bu makalede nasıl toointegrate VSTS ortamınızla her giriş için sürekli tümleştirme olacağı şekilde Azure Otomasyonu.</span><span class="sxs-lookup"><span data-stu-id="fdd73-106">This article describes how toointegrate VSTS with your Azure Automation environment so that continuous integration happens for each check-in.</span></span>

## <a name="getting-hello-scenario"></a><span data-ttu-id="fdd73-107">Merhaba senaryo alma</span><span class="sxs-lookup"><span data-stu-id="fdd73-107">Getting hello scenario</span></span>

<span data-ttu-id="fdd73-108">Bu senaryo doğrudan hello alabileceğiniz iki PowerShell runbook'ları oluşur [Runbook Galerisi](automation-runbook-gallery.md) de Azure portal hello veya indirme hello [PowerShell Galerisi](https://www.powershellgallery.com).</span><span class="sxs-lookup"><span data-stu-id="fdd73-108">This scenario consists of two PowerShell runbooks that you can import directly from hello [Runbook Gallery](automation-runbook-gallery.md) in hello Azure portal or download from hello [PowerShell Gallery](https://www.powershellgallery.com).</span></span>

### <a name="runbooks"></a><span data-ttu-id="fdd73-109">Runbook'lar</span><span class="sxs-lookup"><span data-stu-id="fdd73-109">Runbooks</span></span>

<span data-ttu-id="fdd73-110">Runbook</span><span class="sxs-lookup"><span data-stu-id="fdd73-110">Runbook</span></span> | <span data-ttu-id="fdd73-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdd73-111">Description</span></span>| 
--------|------------|
<span data-ttu-id="fdd73-112">Eşitleme VSTS</span><span class="sxs-lookup"><span data-stu-id="fdd73-112">Sync-VSTS</span></span> | <span data-ttu-id="fdd73-113">Runbook'ları veya yapılandırmaları bir iade yapıldığında VSTS kaynak denetiminden içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="fdd73-113">Import runbooks or configurations from VSTS source control when a check-in is done.</span></span> <span data-ttu-id="fdd73-114">El ile çalıştırırsanız, içeri aktarma ve tüm runbook'ları veya hello Otomasyon hesabı yapılandırmaları yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="fdd73-114">If run manually, it will import and publish all runbooks or configurations into hello Automation account.</span></span>| 
<span data-ttu-id="fdd73-115">Eşitleme VSTSGit</span><span class="sxs-lookup"><span data-stu-id="fdd73-115">Sync-VSTSGit</span></span> | <span data-ttu-id="fdd73-116">Bir iade yapıldığında VSTS Git kaynak denetimi altında yok veya yapılandırmalarını içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="fdd73-116">Import runbooks or configurations from VSTS under Git source control when a check-in is done.</span></span> <span data-ttu-id="fdd73-117">El ile çalıştırırsanız, içeri aktarma ve tüm runbook'ları veya hello Otomasyon hesabı yapılandırmaları yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="fdd73-117">If run manually, it will import and publish all runbooks or configurations into hello Automation account.</span></span>|

### <a name="variables"></a><span data-ttu-id="fdd73-118">Değişkenler</span><span class="sxs-lookup"><span data-stu-id="fdd73-118">Variables</span></span>

<span data-ttu-id="fdd73-119">Değişken</span><span class="sxs-lookup"><span data-stu-id="fdd73-119">Variable</span></span> | <span data-ttu-id="fdd73-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdd73-120">Description</span></span>|
-----------|------------|
<span data-ttu-id="fdd73-121">VSToken</span><span class="sxs-lookup"><span data-stu-id="fdd73-121">VSToken</span></span> | <span data-ttu-id="fdd73-122">Güvenli değişken varlığı hello VSTS kişisel erişim belirteci içeren oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fdd73-122">Secure variable asset you will create that contains hello VSTS personal access token.</span></span> <span data-ttu-id="fdd73-123">Nasıl toocreate VSTS kişisel erişim öğrenebilirsiniz hello üzerinde belirteci [VSTS kimlik doğrulaması sayfası](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview).</span><span class="sxs-lookup"><span data-stu-id="fdd73-123">You can learn how toocreate a VSTS personal access token on hello [VSTS authentication page](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview).</span></span> 
## <a name="installing-and-configuring-this-scenario"></a><span data-ttu-id="fdd73-124">Bu senaryoyu yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fdd73-124">Installing and configuring this scenario</span></span>

<span data-ttu-id="fdd73-125">Oluşturma bir [kişisel erişim belirteci](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) içinde VSTS Otomasyon hesabınızda toosync hello runbook'ları veya yapılandırması kullanır.</span><span class="sxs-lookup"><span data-stu-id="fdd73-125">Create a [personal access token](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) in VSTS that you will use toosync hello runbooks or configurations into your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

<span data-ttu-id="fdd73-126">Oluşturma bir [güvenli değişkeni](automation-variables.md) , Otomasyon hesabı toohold hello kişisel erişim belirteci hello runbook tooVSTS ve eşitleme hello runbook'lar veya hello Otomasyon hesabı yapılandırmaları doğrulanabilmesi.</span><span class="sxs-lookup"><span data-stu-id="fdd73-126">Create a [secure variable](automation-variables.md) in your automation account toohold hello personal access token so that hello runbook can authenticate tooVSTS and sync hello runbooks or configurations into hello Automation account.</span></span> <span data-ttu-id="fdd73-127">Bu VSToken adı verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdd73-127">You can name this VSToken.</span></span> 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

<span data-ttu-id="fdd73-128">Runbook'ları veya hello Otomasyon hesabı yapılandırmaları eşitlenecek hello runbook içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="fdd73-128">Import hello runbook that will sync your runbooks or configurations into hello automation account.</span></span> <span data-ttu-id="fdd73-129">Merhaba kullanabilirsiniz [VSTS örnek runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) veya hello [Git örnek runbook ile VSTS] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) hello PowerShellGallery.com IF bağlı olarak from VSTS kullanın. Kaynak denetimi veya Git ile VSTS ve tooyour Otomasyon hesabı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="fdd73-129">You can use hello [VSTS sample runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) or hello [VSTS with Git sample runbook] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) from hello PowerShellGallery.com depending on if you use VSTS source control or VSTS with Git and deploy tooyour automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

<span data-ttu-id="fdd73-130">Artık [yayımlama](automation-creating-importing-runbook.md#publishing-a-runbook) bir Web kancası oluşturabilmesi için bu runbook.</span><span class="sxs-lookup"><span data-stu-id="fdd73-130">You can now [publish](automation-creating-importing-runbook.md#publishing-a-runbook) this runbook so you can create a webhook.</span></span> 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

<span data-ttu-id="fdd73-131">Oluşturma bir [Web kancası](automation-webhooks.md) bu Eşitleme VSTS runbook ve aşağıda gösterildiği gibi hello parametrelerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="fdd73-131">Create a [webhook](automation-webhooks.md) for this Sync-VSTS runbook and fill in hello parameters as shown below.</span></span> <span data-ttu-id="fdd73-132">VSTS içinde bir hizmet kancası için ihtiyacınız şekilde hello Web kancası URL'si kopyaladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fdd73-132">Make sure you copy hello webhook url as you will need it for a service hook in VSTS.</span></span> <span data-ttu-id="fdd73-133">Merhaba VSAccessTokenVariableName hello (VSToken) önceki toohold hello kişisel erişim belirteci oluşturulan hello güvenli değişkenin adıdır.</span><span class="sxs-lookup"><span data-stu-id="fdd73-133">hello VSAccessTokenVariableName is hello name (VSToken) of hello secure variable that you created earlier toohold hello personal access token.</span></span> 

<span data-ttu-id="fdd73-134">VSTS (Eşitleme-VSTS.ps1) ile tümleştirme şu parametreler hello olur.</span><span class="sxs-lookup"><span data-stu-id="fdd73-134">Integrating with VSTS (Sync-VSTS.ps1) will take hello following parameters.</span></span>
### <a name="sync-vsts-parameters"></a><span data-ttu-id="fdd73-135">Eşitleme VSTS parametreleri</span><span class="sxs-lookup"><span data-stu-id="fdd73-135">Sync-VSTS Parameters</span></span>

<span data-ttu-id="fdd73-136">Parametre</span><span class="sxs-lookup"><span data-stu-id="fdd73-136">Parameter</span></span> | <span data-ttu-id="fdd73-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdd73-137">Description</span></span>| 
--------|------------|
<span data-ttu-id="fdd73-138">WebhookData</span><span class="sxs-lookup"><span data-stu-id="fdd73-138">WebhookData</span></span> | <span data-ttu-id="fdd73-139">Bu hello VSTS hizmet kanca gönderilen hello iade bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="fdd73-139">This will contain hello checkin information sent from hello VSTS service hook.</span></span> <span data-ttu-id="fdd73-140">Bu parametre boş bırakmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdd73-140">You should leave this parameter blank.</span></span>| 
<span data-ttu-id="fdd73-141">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fdd73-141">ResourceGroup</span></span> | <span data-ttu-id="fdd73-142">Bu hello hello Otomasyon hesabı olan hello kaynak grubunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="fdd73-142">This is hello name of hello resource group that hello automation account is in.</span></span>|
<span data-ttu-id="fdd73-143">AutomationAccountName</span><span class="sxs-lookup"><span data-stu-id="fdd73-143">AutomationAccountName</span></span> | <span data-ttu-id="fdd73-144">VSTS ile eşitlenecek hello Otomasyon hesabı Hello adı.</span><span class="sxs-lookup"><span data-stu-id="fdd73-144">hello name of hello automation account that will sync with VSTS.</span></span>|
<span data-ttu-id="fdd73-145">VSFolder</span><span class="sxs-lookup"><span data-stu-id="fdd73-145">VSFolder</span></span> | <span data-ttu-id="fdd73-146">Merhaba runbook'ları ve yapılandırmaların bulunduğu VSTS hello klasöründe adı.</span><span class="sxs-lookup"><span data-stu-id="fdd73-146">The name of hello folder in VSTS where hello runbooks and configurations exist.</span></span>|
<span data-ttu-id="fdd73-147">VSAccount</span><span class="sxs-lookup"><span data-stu-id="fdd73-147">VSAccount</span></span> | <span data-ttu-id="fdd73-148">Visual Studio Team Services hesabı hello Hello adı.</span><span class="sxs-lookup"><span data-stu-id="fdd73-148">hello name of hello Visual Studio Team Services account.</span></span>| 
<span data-ttu-id="fdd73-149">VSAccessTokenVariableName</span><span class="sxs-lookup"><span data-stu-id="fdd73-149">VSAccessTokenVariableName</span></span> | <span data-ttu-id="fdd73-150">Merhaba hello VSTS kişisel erişim belirteci tutan hello güvenli değişkeninin adını (VSToken).</span><span class="sxs-lookup"><span data-stu-id="fdd73-150">hello name of hello secure variable (VSToken) that holds hello VSTS personal access token.</span></span>| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

<span data-ttu-id="fdd73-151">VSTS GIT (Sync-VSTSGit.ps1) ile kullanıyorsanız, şu parametreler hello sürer.</span><span class="sxs-lookup"><span data-stu-id="fdd73-151">If you are using VSTS with GIT (Sync-VSTSGit.ps1) it will take hello following parameters.</span></span>

<span data-ttu-id="fdd73-152">Parametre</span><span class="sxs-lookup"><span data-stu-id="fdd73-152">Parameter</span></span> | <span data-ttu-id="fdd73-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdd73-153">Description</span></span>|
--------|------------|
<span data-ttu-id="fdd73-154">WebhookData</span><span class="sxs-lookup"><span data-stu-id="fdd73-154">WebhookData</span></span> | <span data-ttu-id="fdd73-155">Bu hello VSTS hizmet kanca gönderilen hello iade bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="fdd73-155">This will contain hello checkin information sent from hello VSTS service hook.</span></span> <span data-ttu-id="fdd73-156">Bu parametre boş bırakmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdd73-156">You should leave this parameter blank.</span></span>| <span data-ttu-id="fdd73-157">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fdd73-157">ResourceGroup</span></span> | <span data-ttu-id="fdd73-158">Bu Otomasyon hesabı hello hello kaynak grubunun hello adı kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="fdd73-158">This hello name of hello resource group that hello automation account is in.</span></span>|
<span data-ttu-id="fdd73-159">AutomationAccountName</span><span class="sxs-lookup"><span data-stu-id="fdd73-159">AutomationAccountName</span></span> | <span data-ttu-id="fdd73-160">VSTS ile eşitlenecek hello Otomasyon hesabı Hello adı.</span><span class="sxs-lookup"><span data-stu-id="fdd73-160">hello name of hello automation account that will sync with VSTS.</span></span>|
<span data-ttu-id="fdd73-161">VSAccount</span><span class="sxs-lookup"><span data-stu-id="fdd73-161">VSAccount</span></span> | <span data-ttu-id="fdd73-162">Visual Studio Team Services hesabı hello Hello adı.</span><span class="sxs-lookup"><span data-stu-id="fdd73-162">hello name of hello Visual Studio Team Services account.</span></span>|
<span data-ttu-id="fdd73-163">VSProject</span><span class="sxs-lookup"><span data-stu-id="fdd73-163">VSProject</span></span> | <span data-ttu-id="fdd73-164">Merhaba runbook'ları ve yapılandırmaların bulunduğu VSTS hello projesinde Hello adı.</span><span class="sxs-lookup"><span data-stu-id="fdd73-164">hello name of hello project in VSTS where hello runbooks and configurations exist.</span></span>|
<span data-ttu-id="fdd73-165">GitRepo</span><span class="sxs-lookup"><span data-stu-id="fdd73-165">GitRepo</span></span> | <span data-ttu-id="fdd73-166">Merhaba Git deposu Hello adı.</span><span class="sxs-lookup"><span data-stu-id="fdd73-166">hello name of hello Git repository.</span></span>|
<span data-ttu-id="fdd73-167">GitBranch</span><span class="sxs-lookup"><span data-stu-id="fdd73-167">GitBranch</span></span> | <span data-ttu-id="fdd73-168">VSTS Git deposu hello dalında Hello adı.</span><span class="sxs-lookup"><span data-stu-id="fdd73-168">hello name of hello branch in VSTS Git repository.</span></span>|
<span data-ttu-id="fdd73-169">Klasör</span><span class="sxs-lookup"><span data-stu-id="fdd73-169">Folder</span></span> | <span data-ttu-id="fdd73-170">VSTS Git dal hello klasörünün Hello adı.</span><span class="sxs-lookup"><span data-stu-id="fdd73-170">hello name of hello folder in VSTS Git branch.</span></span>|
<span data-ttu-id="fdd73-171">VSAccessTokenVariableName</span><span class="sxs-lookup"><span data-stu-id="fdd73-171">VSAccessTokenVariableName</span></span> | <span data-ttu-id="fdd73-172">Merhaba hello VSTS kişisel erişim belirteci tutan hello güvenli değişkeninin adını (VSToken).</span><span class="sxs-lookup"><span data-stu-id="fdd73-172">hello name of hello secure variable (VSToken) that holds hello VSTS personal access token.</span></span>|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

<span data-ttu-id="fdd73-173">Hizmet kanca VSTS içinde bu Web kancası kod girişinde tetikler iadeler toohello klasörü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fdd73-173">Create a service hook in VSTS for check-ins toohello folder that triggers this webhook on code check-in.</span></span> <span data-ttu-id="fdd73-174">Yeni bir abonelik oluşturduğunuzda Web Kancalarını ile Merhaba hizmet toointegrate olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="fdd73-174">Select Web Hooks as hello service toointegrate with when you create a new subscription.</span></span> <span data-ttu-id="fdd73-175">Üzerindeki hizmet kancaları hakkında daha fazla bilgiyi [VSTS hizmet kancaları belgelerine](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).</span><span class="sxs-lookup"><span data-stu-id="fdd73-175">You can learn more about service hooks on [VSTS Service Hooks documentation](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).</span></span>
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

<span data-ttu-id="fdd73-176">Runbook'ları ve VSTS yapılandırmaları tüm iadeler mümkün toodo olması ve bunlar otomatik olarak şimdi eşitleme yapması gerektiğini Otomasyon hesabınızda vardı.</span><span class="sxs-lookup"><span data-stu-id="fdd73-176">You should now be able toodo all check-ins of your runbooks and configurations into VSTS and have these automatically sync’d into your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

<span data-ttu-id="fdd73-177">Bu runbook el ile VSTS tarafından tetiklenen olmadan çalıştırırsanız, hello webhookdata parametresi boş bırakabilirsiniz ve belirtilen hello VSTS klasöründen bir tam eşitleme yapar.</span><span class="sxs-lookup"><span data-stu-id="fdd73-177">If you run this runbook manually without being triggered by VSTS, you can leave hello webhookdata parameter empty and it will do a full sync from hello VSTS folder specified.</span></span>

<span data-ttu-id="fdd73-178">Toouninstall hello senaryo istiyorsanız, VSTS hello hizmet kanca kaldırmak için hello VSToken değişkeni silip hello runbook.</span><span class="sxs-lookup"><span data-stu-id="fdd73-178">If you wish toouninstall hello scenario, remove hello service hook from VSTS, delete hello runbook, and hello VSToken variable.</span></span>
