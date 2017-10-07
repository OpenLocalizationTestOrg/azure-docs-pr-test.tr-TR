---
title: "Azure Otomasyon karma Runbook çalışanı aaaRun runbook'larda | Microsoft Docs"
description: "Bu makalede, yerel veri merkezinde veya Bulut sağlayıcısı hello karma Runbook çalışanı rolü ile makinelerde çalışan runbook'ları hakkında bilgi sağlar."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/22/2017
ms.author: magoedte
ms.openlocfilehash: 51961e02603e5690edd11e577594ad2ddea489a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a><span data-ttu-id="7127a-103">Bir karma Runbook çalışanı üzerinde çalışan runbook'ları</span><span class="sxs-lookup"><span data-stu-id="7127a-103">Running runbooks on a Hybrid Runbook Worker</span></span> 
<span data-ttu-id="7127a-104">Azure Automation ve karma Runbook çalışanı üzerinde çalışacak çalışan runbook'ların hello yapısındaki arasında fark yoktur.</span><span class="sxs-lookup"><span data-stu-id="7127a-104">There is no difference in hello structure of runbooks that run in Azure Automation and those that run on a Hybrid Runbook Worker.</span></span> <span data-ttu-id="7127a-105">Her ile kullandığınız runbook'ları kaynakları hello yerel bilgisayarda kendisini veya dağıtıldığı, runbook'ları sırasında hello yerel ortamında kaynaklara karşı bir karma Runbook çalışanı genellikle hedefleyen runbook'ları yönetmek beri büyük olasılıkla ancak önemli ölçüde farklı Azure Otomasyonu'nda genellikle hello Azure bulut kaynakları yönetin.</span><span class="sxs-lookup"><span data-stu-id="7127a-105">Runbooks that you use with each most likely differ significantly though since runbooks targeting a Hybrid Runbook Worker typically manage resources on hello local computer itself or against resources in hello local environment where it is deployed, while runbooks in Azure Automation typically manage resources in hello Azure cloud.</span></span>

<span data-ttu-id="7127a-106">Azure Otomasyon karma Runbook çalışanı için bir runbook düzenleyebilirsiniz ancak tootest hello runbook hello düzenleyicisinde çalışırsanız ilgili sorunlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="7127a-106">You can edit a runbook for Hybrid Runbook Worker in Azure Automation, but you may have difficulties if you try tootest hello runbook in hello editor.</span></span>  <span data-ttu-id="7127a-107">Merhaba yerel kaynakları Azure Otomasyonu ortamınızda; bu durumda yüklenmeyebilir erişen hello PowerShell modülleri hello test başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="7127a-107">hello PowerShell modules that access hello local resources may not be installed in your Azure Automation environment in which case, hello test would fail.</span></span>  <span data-ttu-id="7127a-108">Yüklerseniz hello modülleri, gerekli sonra hello runbook çalışır, ancak tam bir test için yerel kaynak mümkün tooaccess olmaz.</span><span class="sxs-lookup"><span data-stu-id="7127a-108">If you do install hello required modules, then hello runbook will run, but it will not be able tooaccess local resources for a complete test.</span></span>

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a><span data-ttu-id="7127a-109">Karma Runbook çalışanını runbook başlatma</span><span class="sxs-lookup"><span data-stu-id="7127a-109">Starting a runbook on Hybrid Runbook Worker</span></span>
<span data-ttu-id="7127a-110">[Azure Otomasyonu Runbook başlatma](automation-starting-a-runbook.md) bir runbook'u başlatmak için farklı yöntemleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="7127a-110">[Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) describes different methods for starting a runbook.</span></span>  <span data-ttu-id="7127a-111">Karma Runbook çalışanı ekler bir **RunOn** bir karma Runbook çalışan grubu hello adını belirtebileceğiniz seçeneği.</span><span class="sxs-lookup"><span data-stu-id="7127a-111">Hybrid Runbook Worker adds a **RunOn** option where you can specify hello name of a Hybrid Runbook Worker Group.</span></span>  <span data-ttu-id="7127a-112">Bir grubu belirtilirse, ardından hello runbook alınır ve tarafından o gruptaki hello çalışanı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7127a-112">If a group is specified, then hello runbook is retrieved and run by of hello workers in that group.</span></span>  <span data-ttu-id="7127a-113">Bu seçenek belirtilmezse, ardından onu Azure Otomasyonu'nda normal olarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="7127a-113">If this option is not specified, then it is run in Azure Automation as normal.</span></span>

<span data-ttu-id="7127a-114">Hello Azure portalında bir runbook'u başlattığınızda ile sunulan bir **çalıştıracağınız** seçebileceğiniz seçeneği **Azure** veya **karma çalışanı**.</span><span class="sxs-lookup"><span data-stu-id="7127a-114">When you start a runbook in hello Azure portal, you are presented with a **Run on** option where you can select **Azure** or **Hybrid Worker**.</span></span>  <span data-ttu-id="7127a-115">Seçerseniz **karma çalışanı**, hello Grup aşağı açılır listeden seçin, sonra.</span><span class="sxs-lookup"><span data-stu-id="7127a-115">If you select **Hybrid Worker**, then you can select hello group from a dropdown.</span></span>

<span data-ttu-id="7127a-116">Kullanım hello **RunOn** parametresi.</span><span class="sxs-lookup"><span data-stu-id="7127a-116">Use hello **RunOn** parameter.</span></span>  <span data-ttu-id="7127a-117">Komut toostart Windows PowerShell kullanarak MyHybridGroup adlı bir karma Runbook çalışan grubu üzerinde Test-Runbook adlı bir runbook aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7127a-117">You can use hello following command toostart a runbook named Test-Runbook on a Hybrid Runbook Worker Group named MyHybridGroup using Windows PowerShell.</span></span>

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> <span data-ttu-id="7127a-118">Merhaba **RunOn** parametresi toohello eklenen **başlangıç AzureAutomationRunbook** 0.9.1 sürümünde Microsoft Azure PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="7127a-118">hello **RunOn** parameter was added toohello **Start-AzureAutomationRunbook** cmdlet in version 0.9.1 of Microsoft Azure PowerShell.</span></span>  <span data-ttu-id="7127a-119">Yapmanız gerekenler [hello en son sürümü karşıdan](https://azure.microsoft.com/downloads/) yüklü daha önceki bir varsa.</span><span class="sxs-lookup"><span data-stu-id="7127a-119">You should [download hello latest version](https://azure.microsoft.com/downloads/) if you have an earlier one installed.</span></span>  <span data-ttu-id="7127a-120">Yalnızca bu sürümü, Windows Powershell'den hello runbook başlatılıyor bir iş istasyonunda tooinstall gerekir.</span><span class="sxs-lookup"><span data-stu-id="7127a-120">You only need tooinstall this version on a workstation where you are starting hello runbook from Windows PowerShell.</span></span>  <span data-ttu-id="7127a-121">Tooinstall gerekmez hello çalışan bilgisayar üzerinde toostart runbook'lar o bilgisayardan düşünmüyorsanız.</span><span class="sxs-lookup"><span data-stu-id="7127a-121">You do not need tooinstall it on hello worker computer unless you intend toostart runbooks from that computer.</span></span>  <span data-ttu-id="7127a-122">Bu Otomasyon hesabınızda yüklü Azure Powershell toobe en son sürümünü hello gerektiren bu yana bir runbook şu anda başka bir runbook'tan bir karma Runbook çalışanı üzerinde başlatılamıyor.</span><span class="sxs-lookup"><span data-stu-id="7127a-122">You cannot currently start a runbook on a Hybrid Runbook Worker from another runbook since this would require hello latest version of Azure Powershell toobe installed in your Automation account.</span></span>  <span data-ttu-id="7127a-123">Merhaba en son sürümü Azure Otomasyonu'nda otomatik olarak güncelleştirilir ve toohello çalışanları en kısa sürede otomatik olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="7127a-123">hello latest version is automatically updated in Azure Automation and automatically pushed down toohello workers soon.</span></span>
>
>

## <a name="runbook-permissions"></a><span data-ttu-id="7127a-124">Runbook izinleri</span><span class="sxs-lookup"><span data-stu-id="7127a-124">Runbook permissions</span></span>
<span data-ttu-id="7127a-125">Bir karma Runbook çalışanı üzerinde çalışan runbook'ları kullanmak aynı hello olamaz genelde runbook'ları Azure dışında kaynaklara erişmesi beri tooAzure kaynakları kimlik doğrulaması için kullanılan yöntem.</span><span class="sxs-lookup"><span data-stu-id="7127a-125">Runbooks running on a Hybrid Runbook Worker cannot use hello same method that is typically used for runbooks authenticating tooAzure resources, since they are accessing resources outside of Azure.</span></span>  <span data-ttu-id="7127a-126">Merhaba runbook toolocal kaynakları ya da kendi kimlik doğrulaması sağlayabilir veya bir RunAs hesabı tooprovide tüm runbook'lar için bir kullanıcı bağlamı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7127a-126">hello runbook can either provide its own authentication toolocal resources, or you can specify a RunAs account tooprovide a user context for all runbooks.</span></span>

### <a name="runbook-authentication"></a><span data-ttu-id="7127a-127">Runbook kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="7127a-127">Runbook authentication</span></span>
<span data-ttu-id="7127a-128">Bunlar erişecek kendi kimlik doğrulama tooresources sağlamanız gerekir varsayılan olarak, runbook'ları hello şirket içi bilgisayardaki yerel sistem hesabı hello hello bağlamında çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7127a-128">By default, runbooks will run in hello context of hello local System account on hello on-premises computer, so they must provide their own authentication tooresources that they will access.</span></span>  

<span data-ttu-id="7127a-129">Kullanabileceğiniz [kimlik bilgisi](http://msdn.microsoft.com/library/dn940015.aspx) ve [sertifika](http://msdn.microsoft.com/library/dn940013.aspx) runbook'unuzda toodifferent kaynakları doğrulanabilir şekilde toospecify kimlik bilgilerine izin ver cmdlet'leri ile varlıklar.</span><span class="sxs-lookup"><span data-stu-id="7127a-129">You can use [Credential](http://msdn.microsoft.com/library/dn940015.aspx) and [Certificate](http://msdn.microsoft.com/library/dn940013.aspx) assets in your runbook with cmdlets that allow you toospecify credentials so you can authenticate toodifferent resources.</span></span>  <span data-ttu-id="7127a-130">Merhaba aşağıdaki örnek bir bilgisayarı yeniden başlatır bir runbook bir kısmı gösterir.</span><span class="sxs-lookup"><span data-stu-id="7127a-130">hello following example shows a portion of a runbook that restarts a computer.</span></span>  <span data-ttu-id="7127a-131">Kimlik bilgileri bir değişken varlığı hello bilgisayardan kimlik bilgisi varlığı ve hello adını alır ve ardından bu değerleri hello Restart-Computer cmdlet'iyle kullanır.</span><span class="sxs-lookup"><span data-stu-id="7127a-131">It retrieves credentials from a credential asset and hello name of hello computer from a variable asset and then uses these values with hello Restart-Computer cmdlet.</span></span>

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

<span data-ttu-id="7127a-132">Ayrıca yararlanabilirsiniz [Inlinescript](automation-powershell-workflow.md#inlinescript), olanak sağlayan kod toorun blokları başka bir bilgisayarda hello tarafından belirtilen kimlik bilgileriyle [PSCredential ortak parametresi](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="7127a-132">You can also leverage [InlineScript](automation-powershell-workflow.md#inlinescript), which  allows you toorun blocks of code on another computer with credentials specified by hello [PSCredential common parameter](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="runas-account"></a><span data-ttu-id="7127a-133">RunAs hesabı</span><span class="sxs-lookup"><span data-stu-id="7127a-133">RunAs account</span></span>
<span data-ttu-id="7127a-134">Belirleyebileceğiniz toolocal kaynakları kendi kimlik doğrulaması sağlamak runbook'lar sahip olmak yerine bir **RunAs** hesap için bir karma çalışanı grubu.</span><span class="sxs-lookup"><span data-stu-id="7127a-134">Instead of having runbooks provide their own authentication toolocal resources, you can specify a **RunAs** account for a Hybrid worker group.</span></span>  <span data-ttu-id="7127a-135">Belirttiğiniz bir [kimlik bilgisi varlığı](automation-credentials.md) toolocal erişimine sahip ve hello grubundaki bir karma Runbook çalışanı üzerinde çalışan tüm runbook'ları bu kimlik bilgileri altında çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7127a-135">You specify a [credential asset](automation-credentials.md) that has access toolocal resources, and all runbooks run under these credentials when running on a Hybrid Runbook Worker in hello group.</span></span>  

<span data-ttu-id="7127a-136">Merhaba kimlik bilgisi için Hello kullanıcı adı biçimleri aşağıdaki hello biri olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="7127a-136">hello user name for hello credential must be in one of hello following formats:</span></span>

* <span data-ttu-id="7127a-137">etki alanı\kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="7127a-137">domain\username</span></span>
* username@domain
* <span data-ttu-id="7127a-138">Kullanıcı adı (için yerel toohello şirket içi bilgisayar hesapları)</span><span class="sxs-lookup"><span data-stu-id="7127a-138">username (for accounts local toohello on-premises computer)</span></span>

<span data-ttu-id="7127a-139">Aşağıdaki yordam toospecify karma çalışanı grubu için bir RunAs hesabı hello kullan:</span><span class="sxs-lookup"><span data-stu-id="7127a-139">Use hello following procedure toospecify a RunAs account for a Hybrid worker group:</span></span>

1. <span data-ttu-id="7127a-140">Oluşturma bir [kimlik bilgisi varlığı](automation-credentials.md) erişim toolocal kaynaklara sahip.</span><span class="sxs-lookup"><span data-stu-id="7127a-140">Create a [credential asset](automation-credentials.md) with access toolocal resources.</span></span>
2. <span data-ttu-id="7127a-141">Hello Azure portal Hello Automation hesabını açın.</span><span class="sxs-lookup"><span data-stu-id="7127a-141">Open hello Automation account in hello Azure portal.</span></span>
3. <span data-ttu-id="7127a-142">Select hello **karma çalışan grupları** döşeme ve hello grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="7127a-142">Select hello **Hybrid Worker Groups** tile, and then select hello group.</span></span>
4. <span data-ttu-id="7127a-143">Seçin **tüm ayarları** ve ardından **karma çalışanı grubu ayarları**.</span><span class="sxs-lookup"><span data-stu-id="7127a-143">Select **All settings** and then **Hybrid worker group settings**.</span></span>
5. <span data-ttu-id="7127a-144">Değişiklik **Çalıştır** gelen **varsayılan** çok**özel**.</span><span class="sxs-lookup"><span data-stu-id="7127a-144">Change **Run As** from **Default** too**Custom**.</span></span>
6. <span data-ttu-id="7127a-145">Merhaba kimlik bilgisi seçip tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="7127a-145">Select hello credential and click **Save**.</span></span>

### <a name="automation-run-as-account"></a><span data-ttu-id="7127a-146">Automation farklı çalıştır hesabı</span><span class="sxs-lookup"><span data-stu-id="7127a-146">Automation Run As account</span></span>
<span data-ttu-id="7127a-147">Azure'daki kaynakların dağıtımı için otomatik yapı işleminizin bir parçası olarak, erişim tooon içi sistemleri toosupport bir görev veya grup adımı, dağıtım sırası gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="7127a-147">As part of your automated build process for deploying resources in Azure, you may require access tooon-premise systems toosupport a task or set of steps in your deployment sequence.</span></span>  <span data-ttu-id="7127a-148">Merhaba farklı çalıştır hesabını kullanarak Azure karşı kimlik doğrulamasını toosupport, tooinstall hello farklı çalıştır hesabı sertifikası gerekir.</span><span class="sxs-lookup"><span data-stu-id="7127a-148">toosupport authentication against Azure using hello Run As account, you need tooinstall hello Run As account certificate.</span></span>  

<span data-ttu-id="7127a-149">PowerShell runbook aşağıdaki hello *verme RunAsCertificateToHybridWorker*, Azure Otomasyonu hesabınızı hello Çalıştır sertifika verir ve indirir ve bunu hello yerel makine sertifika deposuna aktarır bir Karma çalışanı bağlı toohello aynı hesabı.</span><span class="sxs-lookup"><span data-stu-id="7127a-149">hello following PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exports hello Run As certificate from your Azure Automation account and downloads and imports it into hello local machine certificate store on a Hybrid worker connected toohello same account.</span></span>  <span data-ttu-id="7127a-150">Bu adım tamamlandıktan sonra hello çalışan tooAzure hello farklı çalıştır hesabını kullanarak kimlik doğrulamasını başarıyla doğrular.</span><span class="sxs-lookup"><span data-stu-id="7127a-150">Once that step is completed, it verifies hello worker can successfully authenticate tooAzure using hello Run As account.</span></span>

    <#PSScriptInfo
    .VERSION 1.0
    .GUID 3a796b9a-623d-499d-86c8-c249f10a6986
    .AUTHOR Azure Automation Team
    .COMPANYNAME Microsoft
    .COPYRIGHT 
    .TAGS Azure Automation 
    .LICENSEURI 
    .PROJECTURI 
    .ICONURI 
    .EXTERNALMODULEDEPENDENCIES 
    .REQUIREDSCRIPTS 
    .EXTERNALSCRIPTDEPENDENCIES 
    .RELEASENOTES
    #>

    <#  
    .SYNOPSIS  
    Exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account.
    Run this runbook in hello hybrid worker where you want hello certificate installed.
    This allows hello use of hello AzureRunAsConnection tooauthenticate tooAzure and manage Azure resources from runbooks running in hello hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set hello password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get hello management certificate that will be used toomake calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location toostore temporary certificate in hello Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save hello certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication tooAzure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts tooconfirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

<span data-ttu-id="7127a-151">Merhaba Kaydet *verme RunAsCertificateToHybridWorker* runbook tooyour bilgisayarla bir `.ps1` uzantısı.</span><span class="sxs-lookup"><span data-stu-id="7127a-151">Save hello *Export-RunAsCertificateToHybridWorker* runbook tooyour computer with a `.ps1` extension.</span></span>  <span data-ttu-id="7127a-152">Otomasyon hesabınızda içeri aktarın ve hello hello değişkeninin değerini değiştirme hello runbook düzenleme `$Password` kendi parolanızı ile.</span><span class="sxs-lookup"><span data-stu-id="7127a-152">Import it into your Automation account and edit hello runbook, changing hello value of hello variable `$Password` with your own password.</span></span>  <span data-ttu-id="7127a-153">Yayımlama ve çalıştıran ve runbook'ları hello farklı çalıştır hesabını kullanarak kimlik doğrulaması hello karma çalışanı grubu hedefleme hello runbook çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7127a-153">Publish and then run hello runbook targeting hello Hybrid Worker group that run and authenticate runbooks using hello Run As account.</span></span>  <span data-ttu-id="7127a-154">Merhaba iş akışı raporları hello girişimi tooimport hello sertifika hello yerel makine deposunu ve kaç tane Automation hesapları aboneliğinizde tanımlanır ve kimlik doğrulaması başarılı olup olmadığını bağlı olarak birden fazla satır ile aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="7127a-154">hello job stream reports hello attempt tooimport hello certificate into hello local machine store, and follows with multiple lines depending on how many Automation accounts are defined in your subscription and if authentication is successful.</span></span>  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a><span data-ttu-id="7127a-155">Karma Runbook çalışanı runbook'larda sorun giderme</span><span class="sxs-lookup"><span data-stu-id="7127a-155">Troubleshooting runbooks on Hybrid Runbook Worker</span></span>
<span data-ttu-id="7127a-156">Günlükleri yerel olarak her karma çalışanı C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes konumunda depolanır.</span><span class="sxs-lookup"><span data-stu-id="7127a-156">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span></span>  <span data-ttu-id="7127a-157">Karma çalışanı de kaydeder hatalarını ve olaylarını hello Windows olay günlüğünde altında **uygulama ve Hizmetleri Logs\Microsoft-SMA\Operational**.</span><span class="sxs-lookup"><span data-stu-id="7127a-157">Hybrid worker also records errors and events in hello Windows event log under **Application and Services Logs\Microsoft-SMA\Operational**.</span></span>  <span data-ttu-id="7127a-158">Olaylar ilgili hello çalışan üzerinde yürütülen toorunbooks çok yazılır**uygulama ve Hizmetleri Logs\Microsoft-Automation\Operational**.</span><span class="sxs-lookup"><span data-stu-id="7127a-158">Events related toorunbooks executed on hello worker are written too**Application and Services Logs\Microsoft-Automation\Operational**.</span></span>  <span data-ttu-id="7127a-159">Merhaba **Microsoft SMA** günlük pek çok daha fazla olayları ilgili toohello runbook işi basılmış toohello çalışan ve hello işlenmesini hello runbook içerir.</span><span class="sxs-lookup"><span data-stu-id="7127a-159">hello **Microsoft-SMA** log includes many more events related toohello runbook job pushed toohello worker and hello processing of hello runbook.</span></span>  <span data-ttu-id="7127a-160">Merhaba sırasında **Microsoft Otomasyon** olay günlüğü sahip değil birçok olay runbook yürütülmesi hello sorun giderme konusunda yardımcı ayrıntılarla ve hello sonuçları hello runbook işi, en az bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7127a-160">While hello **Microsoft-Automation** event log does not have many events with details assisting with hello troubleshooting of runbook execution, you will at least find hello results of hello runbook job.</span></span>  

<span data-ttu-id="7127a-161">[Runbook çıkışı ve iletileri](automation-runbook-output-and-messages.md) karma çalışanları yalnızca Otomasyon gibi hello bulutta çalışan runbook işleri tooAzure gönderilir.</span><span class="sxs-lookup"><span data-stu-id="7127a-161">[Runbook output and messages](automation-runbook-output-and-messages.md) are sent tooAzure Automation from hybrid workers just like runbook jobs run in hello cloud.</span></span>  <span data-ttu-id="7127a-162">Merhaba ayrıntılı de etkinleştirebilir ve ilerleme akışları hello aynı diğer runbook'lar için oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="7127a-162">You can also enable hello Verbose and Progress streams hello same way you would for other runbooks.</span></span>  

<span data-ttu-id="7127a-163">Runbook'larınızın başarıyla tamamlanamamasının ve Özet hello iş durumunu gösterir **askıya alındı**, lütfen sorun giderme makalesi hello gözden [karma Runbook çalışanı: durum koduyla bir runbook işi sonlandırır Askıya](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span><span class="sxs-lookup"><span data-stu-id="7127a-163">If your runbooks are not completing successfully and hello job summary shows a status of **Suspended**, please review hello troubleshooting article [Hybrid Runbook Worker: A runbook job terminates with a status of Suspended](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span></span>   

## <a name="next-steps"></a><span data-ttu-id="7127a-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7127a-164">Next steps</span></span>
* <span data-ttu-id="7127a-165">toolearn kullanılan toostart bir runbook olabilecek daha hello farklı yöntemler hakkında bkz [Azure Otomasyonu Runbook başlatma](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="7127a-165">toolearn more about hello different methods that can be used toostart a runbook, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>  
* <span data-ttu-id="7127a-166">PowerShell ve PowerShell iş akışı runbook'ları hello metin düzenleyicisi kullanarak Azure Automation ile çalışma toounderstand hello farklı yordamlara bakın [Azure Otomasyon Runbook'u düzenleme](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="7127a-166">toounderstand hello different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using hello textual editor, see [Editing a Runbook in Azure Automation](automation-edit-textual-runbook.md)</span></span>
