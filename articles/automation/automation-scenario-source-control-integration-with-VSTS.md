---
title: "Azure Otomasyonu Visual Stuido Team Services kaynak denetimi ile Birleşen | Microsoft Docs"
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
ms.openlocfilehash: 01f9c01c9e04e02dbb548b68cf99684ba6ddd57e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a><span data-ttu-id="e7544-104">Azure otomasyonu senaryosu - Visual Studio Team Services ile Otomasyon kaynak denetimi tümleştirme</span><span class="sxs-lookup"><span data-stu-id="e7544-104">Azure Automation scenario - Automation source control integration with Visual Studio Team Services</span></span>

<span data-ttu-id="e7544-105">Bu senaryoda, Azure Otomasyon çalışma kitabı ya da kaynak denetimi altındaki DSC yapılandırmaları yönetmek için kullandığınız bir Visual Studio Team Services projesi vardır.</span><span class="sxs-lookup"><span data-stu-id="e7544-105">In this scenario, you have a Visual Studio Team Services project that you are using to manage Azure Automation runbooks or DSC configurations under source control.</span></span>
<span data-ttu-id="e7544-106">Bu makalede, böylece her giriş için sürekli tümleştirme gerçekleşir VSTS Azure Otomasyonu ortamınız ile tümleştirmek açıklar.</span><span class="sxs-lookup"><span data-stu-id="e7544-106">This article describes how to integrate VSTS with your Azure Automation environment so that continuous integration happens for each check-in.</span></span>

## <a name="getting-the-scenario"></a><span data-ttu-id="e7544-107">Senaryoyu alma</span><span class="sxs-lookup"><span data-stu-id="e7544-107">Getting the scenario</span></span>

<span data-ttu-id="e7544-108">Bu senaryo, doğrudan aktarabilirsiniz iki PowerShell runbook'ların oluşur [Runbook Galerisi](automation-runbook-gallery.md) Azure portalında veya Merkezi'nden [PowerShell Galerisi](https://www.powershellgallery.com).</span><span class="sxs-lookup"><span data-stu-id="e7544-108">This scenario consists of two PowerShell runbooks that you can import directly from the [Runbook Gallery](automation-runbook-gallery.md) in the Azure portal or download from the [PowerShell Gallery](https://www.powershellgallery.com).</span></span>

### <a name="runbooks"></a><span data-ttu-id="e7544-109">Runbook'lar</span><span class="sxs-lookup"><span data-stu-id="e7544-109">Runbooks</span></span>

<span data-ttu-id="e7544-110">Runbook</span><span class="sxs-lookup"><span data-stu-id="e7544-110">Runbook</span></span> | <span data-ttu-id="e7544-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e7544-111">Description</span></span>| 
--------|------------|
<span data-ttu-id="e7544-112">Eşitleme VSTS</span><span class="sxs-lookup"><span data-stu-id="e7544-112">Sync-VSTS</span></span> | <span data-ttu-id="e7544-113">Runbook'ları veya yapılandırmaları bir iade yapıldığında VSTS kaynak denetiminden içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="e7544-113">Import runbooks or configurations from VSTS source control when a check-in is done.</span></span> <span data-ttu-id="e7544-114">El ile çalıştırırsanız, içeri aktarma ve tüm runbook'ları veya Otomasyon hesabı yapılandırmaları yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="e7544-114">If run manually, it will import and publish all runbooks or configurations into the Automation account.</span></span>| 
<span data-ttu-id="e7544-115">Eşitleme VSTSGit</span><span class="sxs-lookup"><span data-stu-id="e7544-115">Sync-VSTSGit</span></span> | <span data-ttu-id="e7544-116">Bir iade yapıldığında VSTS Git kaynak denetimi altında yok veya yapılandırmalarını içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="e7544-116">Import runbooks or configurations from VSTS under Git source control when a check-in is done.</span></span> <span data-ttu-id="e7544-117">El ile çalıştırırsanız, içeri aktarma ve tüm runbook'ları veya Otomasyon hesabı yapılandırmaları yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="e7544-117">If run manually, it will import and publish all runbooks or configurations into the Automation account.</span></span>|

### <a name="variables"></a><span data-ttu-id="e7544-118">Değişkenler</span><span class="sxs-lookup"><span data-stu-id="e7544-118">Variables</span></span>

<span data-ttu-id="e7544-119">Değişken</span><span class="sxs-lookup"><span data-stu-id="e7544-119">Variable</span></span> | <span data-ttu-id="e7544-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e7544-120">Description</span></span>|
-----------|------------|
<span data-ttu-id="e7544-121">VSToken</span><span class="sxs-lookup"><span data-stu-id="e7544-121">VSToken</span></span> | <span data-ttu-id="e7544-122">Güvenli değişken varlığı VSTS kişisel erişim belirteci içeren oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e7544-122">Secure variable asset you will create that contains the VSTS personal access token.</span></span> <span data-ttu-id="e7544-123">VSTS kişisel erişim belirteci oluşturmak nasıl öğrenebilirsiniz [VSTS kimlik doğrulaması sayfası](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview).</span><span class="sxs-lookup"><span data-stu-id="e7544-123">You can learn how to create a VSTS personal access token on the [VSTS authentication page](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview).</span></span> 
## <a name="installing-and-configuring-this-scenario"></a><span data-ttu-id="e7544-124">Bu senaryoyu yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e7544-124">Installing and configuring this scenario</span></span>

<span data-ttu-id="e7544-125">Oluşturma bir [kişisel erişim belirteci](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) runbook'ları veya automation hesabınız yapılandırmaları eşitlemek için kullanacağınız VSTS içinde.</span><span class="sxs-lookup"><span data-stu-id="e7544-125">Create a [personal access token](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) in VSTS that you will use to sync the runbooks or configurations into your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

<span data-ttu-id="e7544-126">Oluşturma bir [güvenli değişkeni](automation-variables.md) runbook VSTS kimliğini doğrulamak ve runbook'ları ya da Otomasyon hesabı yapılandırmaları eşitleme böylece kişisel erişim belirteci tutmak için Otomasyon hesabınızda.</span><span class="sxs-lookup"><span data-stu-id="e7544-126">Create a [secure variable](automation-variables.md) in your automation account to hold the personal access token so that the runbook can authenticate to VSTS and sync the runbooks or configurations into the Automation account.</span></span> <span data-ttu-id="e7544-127">Bu VSToken adı verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7544-127">You can name this VSToken.</span></span> 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

<span data-ttu-id="e7544-128">Runbook'ları ya da Otomasyon hesabı yapılandırmaları eşitlenecek runbook içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="e7544-128">Import the runbook that will sync your runbooks or configurations into the automation account.</span></span> <span data-ttu-id="e7544-129">Kullanabileceğiniz [VSTS örnek runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) veya [VSTS] Git örnek runbook ile (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) PowerShellGallery.com IF bağlı olarak gelen VSTS kaynak denetimi veya VSTS Git ile kullanın ve automation hesabınız dağıtın.</span><span class="sxs-lookup"><span data-stu-id="e7544-129">You can use the [VSTS sample runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) or the [VSTS with Git sample runbook] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) from the PowerShellGallery.com depending on if you use VSTS source control or VSTS with Git and deploy to your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

<span data-ttu-id="e7544-130">Artık [yayımlama](automation-creating-importing-runbook.md#publishing-a-runbook) bir Web kancası oluşturabilmesi için bu runbook.</span><span class="sxs-lookup"><span data-stu-id="e7544-130">You can now [publish](automation-creating-importing-runbook.md#publishing-a-runbook) this runbook so you can create a webhook.</span></span> 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

<span data-ttu-id="e7544-131">Oluşturma bir [Web kancası](automation-webhooks.md) bu Eşitleme VSTS runbook ve aşağıda gösterildiği gibi parametrelerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="e7544-131">Create a [webhook](automation-webhooks.md) for this Sync-VSTS runbook and fill in the parameters as shown below.</span></span> <span data-ttu-id="e7544-132">VSTS içinde bir hizmet kancası için ihtiyacınız şekilde Web kancası URL'si kopyaladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e7544-132">Make sure you copy the webhook url as you will need it for a service hook in VSTS.</span></span> <span data-ttu-id="e7544-133">VSAccessTokenVariableName (VSToken) kişisel erişim belirteci tutmak için daha önce oluşturduğunuz güvenli değişkeninin adıdır.</span><span class="sxs-lookup"><span data-stu-id="e7544-133">The VSAccessTokenVariableName is the name (VSToken) of the secure variable that you created earlier to hold the personal access token.</span></span> 

<span data-ttu-id="e7544-134">VSTS (Eşitleme-VSTS.ps1) ile tümleştirme aşağıdaki parametreleri olur.</span><span class="sxs-lookup"><span data-stu-id="e7544-134">Integrating with VSTS (Sync-VSTS.ps1) will take the following parameters.</span></span>
### <a name="sync-vsts-parameters"></a><span data-ttu-id="e7544-135">Eşitleme VSTS parametreleri</span><span class="sxs-lookup"><span data-stu-id="e7544-135">Sync-VSTS Parameters</span></span>

<span data-ttu-id="e7544-136">Parametre</span><span class="sxs-lookup"><span data-stu-id="e7544-136">Parameter</span></span> | <span data-ttu-id="e7544-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e7544-137">Description</span></span>| 
--------|------------|
<span data-ttu-id="e7544-138">WebhookData</span><span class="sxs-lookup"><span data-stu-id="e7544-138">WebhookData</span></span> | <span data-ttu-id="e7544-139">Bu VSTS hizmet kanca gönderilen iade bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="e7544-139">This will contain the checkin information sent from the VSTS service hook.</span></span> <span data-ttu-id="e7544-140">Bu parametre boş bırakmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7544-140">You should leave this parameter blank.</span></span>| 
<span data-ttu-id="e7544-141">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e7544-141">ResourceGroup</span></span> | <span data-ttu-id="e7544-142">Otomasyon hesabının bulunduğu kaynak grubunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="e7544-142">This is the name of the resource group that the automation account is in.</span></span>|
<span data-ttu-id="e7544-143">AutomationAccountName</span><span class="sxs-lookup"><span data-stu-id="e7544-143">AutomationAccountName</span></span> | <span data-ttu-id="e7544-144">VSTS ile eşitlenecek Otomasyon hesabının adı.</span><span class="sxs-lookup"><span data-stu-id="e7544-144">The name of the automation account that will sync with VSTS.</span></span>|
<span data-ttu-id="e7544-145">VSFolder</span><span class="sxs-lookup"><span data-stu-id="e7544-145">VSFolder</span></span> | <span data-ttu-id="e7544-146">Runbook'ları ve yapılandırmaları var olduğu VSTS klasöründe adı.</span><span class="sxs-lookup"><span data-stu-id="e7544-146">The name of the folder in VSTS where the runbooks and configurations exist.</span></span>|
<span data-ttu-id="e7544-147">VSAccount</span><span class="sxs-lookup"><span data-stu-id="e7544-147">VSAccount</span></span> | <span data-ttu-id="e7544-148">Visual Studio Team Services hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="e7544-148">The name of the Visual Studio Team Services account.</span></span>| 
<span data-ttu-id="e7544-149">VSAccessTokenVariableName</span><span class="sxs-lookup"><span data-stu-id="e7544-149">VSAccessTokenVariableName</span></span> | <span data-ttu-id="e7544-150">VSTS kişisel erişim belirtecine güvenli değişkeni (VSToken) adı.</span><span class="sxs-lookup"><span data-stu-id="e7544-150">The name of the secure variable (VSToken) that holds the VSTS personal access token.</span></span>| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

<span data-ttu-id="e7544-151">VSTS GIT (Sync-VSTSGit.ps1) ile kullanıyorsanız, aşağıdaki parametreleri sürer.</span><span class="sxs-lookup"><span data-stu-id="e7544-151">If you are using VSTS with GIT (Sync-VSTSGit.ps1) it will take the following parameters.</span></span>

<span data-ttu-id="e7544-152">Parametre</span><span class="sxs-lookup"><span data-stu-id="e7544-152">Parameter</span></span> | <span data-ttu-id="e7544-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e7544-153">Description</span></span>|
--------|------------|
<span data-ttu-id="e7544-154">WebhookData</span><span class="sxs-lookup"><span data-stu-id="e7544-154">WebhookData</span></span> | <span data-ttu-id="e7544-155">Bu VSTS hizmet kanca gönderilen iade bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="e7544-155">This will contain the checkin information sent from the VSTS service hook.</span></span> <span data-ttu-id="e7544-156">Bu parametre boş bırakmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7544-156">You should leave this parameter blank.</span></span>| <span data-ttu-id="e7544-157">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e7544-157">ResourceGroup</span></span> | <span data-ttu-id="e7544-158">Bu Otomasyon hesabı bulunduğu kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="e7544-158">This the name of the resource group that the automation account is in.</span></span>|
<span data-ttu-id="e7544-159">AutomationAccountName</span><span class="sxs-lookup"><span data-stu-id="e7544-159">AutomationAccountName</span></span> | <span data-ttu-id="e7544-160">VSTS ile eşitlenecek Otomasyon hesabının adı.</span><span class="sxs-lookup"><span data-stu-id="e7544-160">The name of the automation account that will sync with VSTS.</span></span>|
<span data-ttu-id="e7544-161">VSAccount</span><span class="sxs-lookup"><span data-stu-id="e7544-161">VSAccount</span></span> | <span data-ttu-id="e7544-162">Visual Studio Team Services hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="e7544-162">The name of the Visual Studio Team Services account.</span></span>|
<span data-ttu-id="e7544-163">VSProject</span><span class="sxs-lookup"><span data-stu-id="e7544-163">VSProject</span></span> | <span data-ttu-id="e7544-164">Runbook'ları ve yapılandırmaları var olduğu VSTS projesinde adı.</span><span class="sxs-lookup"><span data-stu-id="e7544-164">The name of the project in VSTS where the runbooks and configurations exist.</span></span>|
<span data-ttu-id="e7544-165">GitRepo</span><span class="sxs-lookup"><span data-stu-id="e7544-165">GitRepo</span></span> | <span data-ttu-id="e7544-166">Git deposu adı.</span><span class="sxs-lookup"><span data-stu-id="e7544-166">The name of the Git repository.</span></span>|
<span data-ttu-id="e7544-167">GitBranch</span><span class="sxs-lookup"><span data-stu-id="e7544-167">GitBranch</span></span> | <span data-ttu-id="e7544-168">VSTS Git deposu dalında adı.</span><span class="sxs-lookup"><span data-stu-id="e7544-168">The name of the branch in VSTS Git repository.</span></span>|
<span data-ttu-id="e7544-169">Klasör</span><span class="sxs-lookup"><span data-stu-id="e7544-169">Folder</span></span> | <span data-ttu-id="e7544-170">VSTS Git dal klasörün adı.</span><span class="sxs-lookup"><span data-stu-id="e7544-170">The name of the folder in VSTS Git branch.</span></span>|
<span data-ttu-id="e7544-171">VSAccessTokenVariableName</span><span class="sxs-lookup"><span data-stu-id="e7544-171">VSAccessTokenVariableName</span></span> | <span data-ttu-id="e7544-172">VSTS kişisel erişim belirtecine güvenli değişkeni (VSToken) adı.</span><span class="sxs-lookup"><span data-stu-id="e7544-172">The name of the secure variable (VSToken) that holds the VSTS personal access token.</span></span>|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

<span data-ttu-id="e7544-173">Bir hizmet kancası VSTS içinde bu Web kancası kod girişinde tetikler klasörüne iadeler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e7544-173">Create a service hook in VSTS for check-ins to the folder that triggers this webhook on code check-in.</span></span> <span data-ttu-id="e7544-174">Yeni bir abonelik oluşturduğunuzda ile tümleştirmek için hizmet olarak Web Kancalarını'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e7544-174">Select Web Hooks as the service to integrate with when you create a new subscription.</span></span> <span data-ttu-id="e7544-175">Üzerindeki hizmet kancaları hakkında daha fazla bilgiyi [VSTS hizmet kancaları belgelerine](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).</span><span class="sxs-lookup"><span data-stu-id="e7544-175">You can learn more about service hooks on [VSTS Service Hooks documentation](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).</span></span>
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

<span data-ttu-id="e7544-176">Şimdi tüm onay bileşenler runbook'lardan ve VSTS yapılandırmaları yapın ve bu otomatik olarak sahip olmanız gerekir eşitleme 'd Otomasyon hesabınızda.</span><span class="sxs-lookup"><span data-stu-id="e7544-176">You should now be able to do all check-ins of your runbooks and configurations into VSTS and have these automatically sync’d into your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

<span data-ttu-id="e7544-177">Bu runbook el ile VSTS tarafından tetiklenen olmadan çalıştırırsanız, webhookdata parametresi boş bırakabilirsiniz ve belirtilen VSTS klasöründen bir tam eşitleme yapar.</span><span class="sxs-lookup"><span data-stu-id="e7544-177">If you run this runbook manually without being triggered by VSTS, you can leave the webhookdata parameter empty and it will do a full sync from the VSTS folder specified.</span></span>

<span data-ttu-id="e7544-178">Senaryo kaldırmak istiyorsanız hizmet kanca VSTS Kaldır runbook ve VSToken değişkeni silin.</span><span class="sxs-lookup"><span data-stu-id="e7544-178">If you wish to uninstall the scenario, remove the service hook from VSTS, delete the runbook, and the VSToken variable.</span></span>
